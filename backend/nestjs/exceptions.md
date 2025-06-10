# Padrão de Exceptions no NestJS

Este documento descreve o padrão adotado para tratamento de exceções nos projetos desenvolvidos com NestJS. O objetivo é garantir consistência, clareza e padronização nas respostas de erro da API.

## Estrutura Base

Todas as exceções customizadas devem herdar de uma classe base chamada `BaseException`, que estende `HttpException` do NestJS e permite padronizar o payload de erro.

### Classe `BaseException`

```ts
import { HttpException, HttpStatus } from '@nestjs/common';

interface AppExceptionParams {
  status: HttpStatus;
  errors?: ErrorDetail[];
}

export interface ErrorDetail<T = unknown> {
  code: string;
  message: string;
  data?: T;
}

export class BaseException extends HttpException {
  constructor({ status, ...params }: AppExceptionParams) {
    super(params, status);
  }
}
```

### Exemplo de resposta de erro

```json
{
  "statusCode": 404,
  "errors": [
    {
      "code": "USER_NOT_FOUND",
      "message": "Usuário não encontrado"
    }
  ]
}
```

## Exceções Customizadas

Cada exceção específica do domínio da aplicação deve extender `BaseException` e ser definida em um arquivo próprio.

### Exemplo: `UserNotFoundException`

```ts
import { HttpStatus } from '@nestjs/common';
import { ERRORS_DETAILS } from 'src/shared/constants/app-errors';
import { BaseException } from 'src/shared/exceptions/app-exception';

export class UserNotFoundException extends BaseException {
  constructor() {
    super({
      status: HttpStatus.NOT_FOUND,
      errors: [ERRORS_DETAILS.USER_NOT_FOUND],
    });
  }
}
```

## Centralização dos Detalhes de Erro

Os detalhes dos erros devem ser centralizados em um arquivo de constantes para reutilização e consistência.

### Exemplo: `app-errors.ts`

```ts
export const ERRORS_DETAILS = {
  USER_NOT_FOUND: {
    code: 'USER_NOT_FOUND',
    message: 'Usuário não encontrado',
  },
  EMAIL_ALREADY_EXISTS: {
    code: 'EMAIL_ALREADY_EXISTS',
    message: 'Este e-mail já está em uso',
  },
  // outros erros...
};
```

## Boas Práticas

- Centralize os códigos e mensagens de erro em um único arquivo de constantes (`app-errors.ts`).
- Crie uma classe de exceção para cada tipo de erro esperado, com nomes descritivos.
- Utilize os status HTTP corretos da enum `HttpStatus` do NestJS.
- Mantenha o formato `{ code, message, data? }` em todos os erros para garantir consistência.

## Benefícios do Padrão

- **Clareza na resposta da API:** facilita o entendimento dos erros por consumidores da API.
- **Facilidade de manutenção:** centralização dos códigos e mensagens permite ajustes rápidos.
- **Padronização:** todas as exceções seguem o mesmo modelo, reduzindo ambiguidade.

