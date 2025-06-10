# Padrão de Uso de DTOs no NestJS

## O que é um DTO?

DTO (Data Transfer Object) é um padrão de projeto utilizado para transportar dados entre as camadas da aplicação. No contexto do NestJS, ele é amplamente utilizado para definir a estrutura esperada de dados recebidos ou transmitidos entre camadas como:

- `Client` → `Controller`
- `Controller` → `Service`
- `Service` → `Repository`

> ⚠️ Os DTOs **não devem conter lógica de negócio**. Seu único objetivo é estruturar dados de forma segura e previsível.

## Diretrizes da Equipe

Nosso time adota os seguintes padrões de uso para DTOs:

1. **Somente usar DTOs para receber dados**, especialmente dados de entrada de requisições HTTP.
2. **Limitar o uso de DTOs às camadas `Controller` e `Service`**.
3. **Na camada de `Repository`**, recomendamos utilizar interfaces/classes simples denominados `params` (ex: CreateUserParams), em vez de DTOs (caso os parâmetros esperados no repository sejam diferentes, caso o contrário pode reutilizar o mesmo dto).

## Exemplo de DTO

```ts
// src/modules/users/dto/create-user.dto.ts

import { IsEmail, IsNotEmpty, MinLength } from 'class-validator';

export class CreateUserDto {
  @IsNotEmpty()
  name: string;

  @IsEmail()
  email: string;

  @MinLength(6)
  password: string;
}
```