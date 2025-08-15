# Guia Monorepo

## 📜 Índice

- [📖 Introdução](#introdução)
- [🗂 Estrutura Básica](#estrutura-básica)
- [⚙️ Ferramentas Populares](#ferramentas-populares)
- [✅ Vantagens](#vantagens)
- [⚠️ Desvantagens](#desvantagens)
- [🔄 Fluxo de Trabalho Típico](#fluxo-de-trabalho-típico)
- [📌 Boas Práticas](#boas-práticas)
- [🔗 Comparação com Multirepo](#comparação-com-multirepo)

---

## Introdução

Um **monorepo** (repositório monolítico) é uma estratégia onde múltiplos projetos, bibliotecas e recursos ficam dentro de **um único repositório Git**.  
Aqui, “monolítico” não significa que o código seja todo misturado, mas sim que está centralizado no mesmo repositório, mesmo que cada parte tenha sua própria pasta e funcione de forma independente.

---

## Estrutura Básica

No monorepo, cada aplicação final ou biblioteca fica em um diretório separado.  
Um modelo comum é:

```
/apps       → aplicações finais (web, mobile, API)
/packages   → bibliotecas e módulos reutilizáveis
```

Mas isso não é regra.  
Por exemplo, seu monorepo pode ter tudo dentro de `/packages`:

```
/packages
  /app1      → aplicação
  /app2      → aplicação
  /shared    → módulo comum usado pelas apps
```

O importante é manter a separação clara entre o que é aplicação e o que é código compartilhado.

---

## Ferramentas Populares

Para gerenciar builds, dependências e publicação de forma eficiente, algumas ferramentas se destacam:

- **Nx** – Focado em apps modernas, com suporte a caching inteligente.
- **Turborepo** – Rápido, ideal para projetos JavaScript/TypeScript.
- **Lerna** – Automação de pacotes e publicação.
- **Bazel** – Usado por empresas grandes como Google.

---

## Vantagens

- **Integração facilitada**: Todos os projetos vivem no mesmo lugar.
- **Reuso de código**: Bibliotecas internas compartilhadas facilmente.
- **Padronização**: Mesmo lint, build e testes para todo o código.
- **Histórico único**: Um Git centralizado para todos os projetos.

---

## Desvantagens

- **Escalabilidade**: Repositórios enormes podem ser lentos para clonar e buildar.
- **Complexidade de gestão**: Mudanças precisam ser isoladas com cuidado.
- **Dependência de ferramentas**: Sem automação, a manutenção fica pesada.

---

## Fluxo de Trabalho Típico

1. **Clone único** – O dev baixa todo o repo.
2. **Build seletivo com cache** – Ferramentas reaproveitam resultados já gerados (_caching_) para acelerar builds.
3. **Testes compartilhados** – Rodam para múltiplos projetos de uma vez.
4. **Publicação** – Apps ou pacotes lançados individualmente a partir do mesmo repositório.

---

## Boas Práticas

- Organize pastas de forma clara (apps, libs, shared, etc.).
- Automatize builds e testes via **CI/CD** (_Continuous Integration_ / _Continuous Delivery_).
- Use caching no CI/CD para evitar recompilações desnecessárias.
- Defina convenções para commits, branches e PRs.
- Monitore o tamanho e performance do repo.

---

## Comparação com Multirepo

| Monorepo                         | Multirepo                                    |
| -------------------------------- | -------------------------------------------- |
| Um único repositório para tudo   | Um repositório por projeto                   |
| Fácil compartilhamento de código | Compartilhamento exige publicação de pacotes |
| Histórico centralizado           | Históricos separados                         |
| Build/teste integrados           | Build/teste independentes                    |
