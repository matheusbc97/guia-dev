# 📚 Padrão de Camadas no NestJS

Este documento define a arquitetura em camadas adotada em projetos NestJS, promovendo separação de responsabilidades, manutenibilidade e testabilidade do código.

## 🧱 Visão Geral da Arquitetura

A aplicação é dividida em três camadas principais:

- **Controller (Controlador)**  
- **Service (Serviço)**
- **Repository (Repositório)**

Cada uma tem responsabilidades bem definidas e comunica-se apenas com as camadas vizinhas, seguindo o princípio de **abstração e desacoplamento**.


## 🧭 Controller (Controlador)

A camada de controller é responsável por **receber e responder requisições HTTP**. Ela atua como ponte entre o cliente (ex: front-end, mobile, API externa) e a lógica de negócio da aplicação.

### Responsabilidades

- Receber requisições HTTP (GET, POST, etc.).
- Validar dados de entrada via DTOs e pipes.
- Acionar os métodos da camada de serviço.
- Retornar uma resposta HTTP adequada ao cliente.

### Regras de Boas Práticas

- Manter **até 5 métodos por controller**, respeitando os principais verbos HTTP.
- Não conter lógica de negócio — apenas delegar ao service.
- Evitar validações manuais — preferir uso de `class-validator` e `Pipes`.
- Retornar apenas os dados tratados pelo service (sem lógica adicional).

### Verbos HTTP utilizados

| Método  | Uso                                                                 |
|---------|----------------------------------------------------------------------|
| `GET`   | Listar itens (ex: `/users`) ou buscar item por ID (ex: `/users/:id`)|
| `POST`  | Criar ou enviar dados (ex: `/users`)                                 |
| `PATCH` | Atualizar parcialmente uma entidade                                  |
| `PUT`   | Substituir totalmente uma entidade                                   |
| `DELETE`| Remover um ou mais itens                                             |

### Exemplo

```ts
// users.controller.ts
@Controller('users')
export class UsersController {
  constructor(private readonly usersService: UsersService) {}

  @Get()
  findAll() {
    return this.usersService.findAll();
  }

  @Get(':id')
  findOne(@Param('id') id: string) {
    return this.usersService.findById(+id);
  }

  @Post()
  create(@Body() dto: CreateUserDto) {
    return this.usersService.create(dto);
  }

  @Patch(':id')
  update(@Param('id') id: string, @Body() dto: UpdateUserDto) {
    return this.usersService.updatePartial(+id, dto);
  }

  @Delete(':id')
  remove(@Param('id') id: string) {
    return this.usersService.deleteById(+id);
  }
}
```

## ⚙️ Service (Serviço)

A camada de serviço é responsável por centralizar a **lógica de negócio** da aplicação. Ela atua como intermediária entre os controladores e os repositórios, aplicando regras e organizando os fluxos de dados.

### Responsabilidades

- Implementar a lógica de negócio.
- Orquestrar chamadas entre repositórios e outros serviços.
- Aplicar regras, validações e transformações nos dados.
- Garantir consistência nas operações da aplicação.

### Regras de Boas Práticas

- Não acessar diretamente o banco de dados (sempre via repositórios).
- Evitar lógica de apresentação (responsabilidade do controller).
- Não duplicar lógica já existente em outros serviços.

### Exemplo

```ts
// users.service.ts
@Injectable()
export class UsersService {
  constructor(private readonly usersRepository: UsersRepository) {}

  async findById(id: number): Promise<User> {
    const user = await this.usersRepository.findById(id);

    if (!user) {
      throw new NotFoundException('Usuário não encontrado');
    }

    return user;
  }
}
```

## 🗃️ Repository (Repositório)

A camada de repositório é responsável por **acessar e manipular dados no banco de dados**, encapsulando todas as operações de persistência. Seu uso facilita a separação da lógica de negócio da lógica de acesso a dados.

### Responsabilidades

- Executar operações de leitura, escrita, atualização e remoção de dados.
- Isolar a lógica de persistência do restante da aplicação.
- Facilitar a substituição ou alteração da estratégia de armazenamento.
- Trabalhar com o ORM configurado no projeto (ex: TypeORM, Prisma).

### Regras de Boas Práticas

- Não conter regras de negócio.
- Retornar objetos de domínio ou entidades.
- Manter os métodos concisos e descritivos.

### Exemplo

```ts
// users.repository.ts
@Injectable()
export class UsersRepository {
  constructor(
    @InjectRepository(User)
    private readonly repo: Repository<User>,
  ) {}

  async findById(id: number): Promise<User | null> {
    return this.repo.findOne({ where: { id } });
  }

  async create(userData: CreateUserDto): Promise<User> {
    const user = this.repo.create(userData);
    return this.repo.save(user);
  }

  async deleteById(id: number): Promise<void> {
    await this.repo.delete(id);
  }
}
```