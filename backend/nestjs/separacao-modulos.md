# 📦 Separação por Módulos no NestJS

Este documento define a convenção de estruturação dos módulos dentro da aplicação NestJS, visando organização, manutenibilidade e prevenção de ciclos de importação.

---

## 📐 Princípios Gerais

- Cada **módulo deve representar um contexto único** do domínio da aplicação.
- Um **módulo deve conter somente uma entidade principal** (ex: `User`, `Project`, `Task`).
- A comunicação entre módulos deve ser feita apenas por meio de **interfaces públicas** (services exportados), evitando referências cruzadas diretas a entidades.

---

## 🧱 Estrutura Recomendada

```
src/
├── user/
│   ├── user.module.ts
│   ├── user.controller.ts
│   ├── user.service.ts
│   ├── user.entity.ts
│   ├── dto/
│   ├── interfaces/
│   └── user.repository.ts
├── task/
│   ├── task.module.ts
│   ├── task.controller.ts
│   ├── task.service.ts
│   ├── task.entity.ts
│   └── ...
```

> 📌 **Nota:** Cada módulo deve conter todos os arquivos relacionados à sua entidade, como controller, service, repository, DTOs, interfaces e testes.

---

## 🧩 Vantagens

- ✅ Evita ciclos de dependência entre entidades.
- ✅ Facilita a reutilização e teste de serviços e regras de negócio.
- ✅ Melhora a legibilidade e o entendimento da estrutura do projeto.
- ✅ Permite organização clara e modular do domínio da aplicação.

---

## 🔁 Comunicação entre Módulos

Utilize **injeção de dependência entre serviços** ao invés de importar entidades diretamente.

```ts
// task.module.ts
@Module({
  providers: [TaskService],
  controllers: [TaskController],
  exports: [TaskService],
})
export class TaskModule {}
```

```ts
// user.module.ts
@Module({
  imports: [forwardRef(() => TaskModule)],
  providers: [UserService],
  controllers: [UserController],
})
export class UserModule {}
```

> ⚠️ Use `forwardRef()` somente quando necessário. Se a dependência circular se repetir com frequência, reavalie a modelagem dos módulos.

---

## 🔒 Acesso à Entidade

A entidade (`*.entity.ts`) **não deve ser utilizada diretamente por outros módulos**.  
O acesso deve ser feito exclusivamente através da **camada de serviço (service)** do módulo proprietário.

---

## ✅ Conclusão

A separação por módulos com uma entidade principal por módulo ajuda a manter o código organizado, desacoplado e sustentável a longo prazo. Essa abordagem favorece a escalabilidade da aplicação e melhora o fluxo de desenvolvimento colaborativo.
