# 🧾 Presenters no NestJS

## 💡 O que são?

**Presenters** são classes (ou funções) responsáveis por **formatar a resposta** que será entregue ao cliente, separando a lógica de apresentação da lógica de negócio.

Eles são utilizados geralmente nas camadas de controller ou use case, e têm como objetivo transformar entidades ou objetos internos em formatos apropriados para a camada externa (como APIs REST ou GraphQL).

## 🧠 Para que servem?

- ✅ **Evitar exposição de dados sensíveis**, como `password`, `accessToken`, `internalFlags`, etc.
- 🔁 **Adaptar nomes de campos** para seguir convenções de front-end, como `createdAt` → `created_at`.
- 🧹 **Organizar a estrutura da resposta**, tornando-a mais clara e legível.
- 📦 **Encapsular regras de apresentação**, mantendo o domínio focado apenas na lógica de negócio.


## 📦 Exemplo de Presenter

```ts
// user.presenter.ts
export class UserPresenter {
  @ApiProperty({
    description: 'Unique identifier of the user',
    example: 1,
  })
  id: number;

  @ApiProperty({
    description: 'Full name of the user',
    example: 'John Doe',
  })
  name: string;

  @ApiProperty({
    description: 'Email address of the user',
    example: 'john.doe@example.com',
  })
  email: string;

  static fromEntity(entity: User): UserPresenter {
    const presenter = new UserPresenter();

    presenter.id = entity.id;
    presenter.name = entity.name;
    presenter.email = entity.email;

    return presenter;
  }

  static fromEntities(entities: User[]): UserPresenter[] {
    return entities.map((entity) => this.fromEntity(entity));
  }
}
```