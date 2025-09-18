# O que é WebSocket?

WebSocket é um protocolo que cria uma **conexão TCP persistente** entre cliente e servidor, permitindo comunicação **bidirecional** em tempo real. Diferente do HTTP tradicional — que abre um canal, responde e fecha — o WebSocket mantém o canal aberto e ambos os lados podem enviar mensagens quando quiserem.

* **HTTP:** conexão curta; request → response → desconecta.
* **WebSocket:** conexão longa; envio/recebimento a qualquer momento.

> Obs: dá pra simular WebSocket com *long polling* (ex.: cliente pergunta ao servidor a cada 1s), embora a latência seja maior.

# O que é Socket.IO

Socket.IO é uma biblioteca JavaScript que abstrai WebSocket e adiciona recursos úteis. Ela surgiu quando navegadores tinham suporte incerto a WebSocket — por isso faz **fallback** automático para *long-polling* quando necessário.

Recursos importantes:

* API por **eventos** (`emit` / `on`).
* **Fallback** para polling quando WebSocket não é suportado.
* **Salas (rooms)** para agrupar clientes.
* **Buffering / retry**: guarda mensagens não entregues e tenta reenviar.
* **Recuperação de estado**: mantém mensagens por um tempo para clientes que desconectam e reconectam.
*  **representacao do cliente como uma instancia, sendo facil enxergar e guardar informações sobre ele
* Adapters (ex.: Redis) para escalar entre instâncias e não depender apenas do cache da RAM.

## Aplicações comuns

* Notificações / filas (quando o backend precisa notificar o cliente)

  *Obs:* conexões WebSocket em segundo plano em celular consomem muita bateria; para notificações use serviços como FCM.

* Jogos (baixa latência e eventos em tempo real)

* Chat, dashboards, colaboração em tempo real

# Exemplo mínimo

**Servidor (node + socket.io)**

```js
// server.js
const { Server } = require('socket.io');
const io = new Server(3000);

io.on('connection', (socket) => {
  console.log('cliente conectado', socket.id);
  socket.on('mensagem', (msg) => {
    console.log('recebeu:', msg);
    socket.emit('resposta', 'ok');
  });
});
```

**Cliente (browser)**

```html
<script src="/socket.io/socket.io.js"></script>
<script>
  const socket = io('http://localhost:3000');
  socket.emit('mensagem', 'oi');
  socket.on('resposta', r => console.log(r));
</script>
```

# Como proteger / identificar quem se conecta

Antes de abrir a conexão, o Socket.IO faz um **handshake**. É aí que você valida o JWT e decide permitir ou recusar a conexão.

No NestJS, você pode criar um *adapter* customizado e usar [allowRequest](https://socket.io/docs/v3/server-initialization/#allowrequest) no handshake para validar o token. Se o token for válido, os dados do usuário são adicionados ao objeto cliente; se não, a conexão é fechada.

```ts
import { INestApplicationContext } from '@nestjs/common';
import { IoAdapter } from '@nestjs/platform-socket.io';
import { ServerOptions } from 'socket.io';
import { JwtAuthService } from '../auth/jwt.service';
import { ConfigService } from '@nestjs/config';

export class AuthenticatedSocketIoAdapter extends IoAdapter {
  private jwtService: JwtAuthService;
  private configService: ConfigService;

  constructor(private app: INestApplicationContext) {
    super(app);
    this.jwtService = this.app.get(JwtAuthService);
    this.configService = this.app.get(ConfigService);
  }

  createIOServer(port: number, options?: ServerOptions): any {
    options = options || {};

    options.allowRequest = async (request: any, allowFunction) => {
      const token = request.headers.authorization?.split(' ')[1] || request._query?.token;
      const { status, payload } = this.jwtService.validateToken(token);
      request.user = payload;
      return allowFunction(status, status === 'VALID');
    };

    options.connectionStateRecovery = {
      maxDisconnectionDuration: +this.configService.get('TIMEOUT_TO_RECONNECT'),
    };

    return super.createIOServer(port, options);
  }
}
```


# Como usamos no NestJS?

No NestJS usamos **Gateways** (módulo `@nestjs/websockets`) para organizar a lógica de sockets. O Gateway abstrai a integração com Socket.IO e permite declarar handlers de eventos.


```ts
@WebSocketGateway({ cors: true, namespace: 'match' })
export class MatchGateway implements OnGatewayConnection, OnGatewayDisconnect {
  @WebSocketServer() io: Server;

  constructor(private matchFinalizerService: MatchFinalizerService) {}

  handleConnection(socket: Socket) {
    socket.data.userId = socket.request.user.uuid;
  }

  async finishMatch(socketsPlayer: Socket[], matchId: string, loser: string, status: string) {
    const endMatch = await this.matchFinalizerService.setWinner(matchId, loser, status);

    socketsPlayer.forEach((socket) => {
      socket.emit('match:finish', endMatch);
      socket.data.matchId = null;
      socket.data.iAmPlayer = null;
      socket.disconnect();
    });
  }

  @SubscribeMessage('match:quit')
  async leaveMatch(@ConnectedSocket() socket: Socket) {
    const { iAmPlayer, matchId } = socket.data;
    const pSockets = await this.io.in(matchId).fetchSockets();
    await this.matchFinalizerService.finishMatch(pSockets, matchId, iAmPlayer, 'resign');
  }
}
```




