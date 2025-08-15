# Guia Monorepo

## 📜 Índice

- [📖 Introdução](#introdução)
- [🗂 Estrutura Básica](#estrutura-básica)
- [📊 Tipos e Estratégias de Monorepo](#tipos-e-estratégias-de-monorepo)
- [✅ Vantagens](#vantagens)
- [⚠️ Desvantagens](#desvantagens)
- [🔄 Fluxo de Trabalho Típico](#fluxo-de-trabalho-típico)
- [📌 Boas Práticas](#boas-práticas)
- [🔗 Comparação com Multirepo](#comparação-com-multirepo)
- [⚙️ Ferramentas Populares](#ferramentas-populares)
- [📚 Referências](#referências)

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

## Tipos e Estratégias de Monorepo

Existem diferentes formas de organizar e gerenciar um monorepo, especialmente no mundo JavaScript/TypeScript:

Yarn Workspaces – Permite que múltiplos pacotes compartilhem dependências instaladas em um único lugar, reduzindo duplicações e facilitando a resolução de versões.

PNPM Workspaces – Similar ao Yarn Workspaces, mas com links simbólicos inteligentes, tornando builds e instalações mais rápidas e eficientes.

npm Workspaces – A solução nativa do npm para gerenciar múltiplos pacotes em um único repositório.

Lerna com Workspaces – Combina o versionamento e publicação automática do Lerna com Workspaces para dependências compartilhadas.

Cada estratégia tem suas vantagens e limitações, mas todas ajudam a manter dependências centralizadas, acelerar builds e simplificar o desenvolvimento dentro do monorepo.

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

## Ferramentas Populares

Existem algumas ferramentas que facilitam o gerenciamento de monorepos. Elas ajudam a organizar múltiplos projetos e bibliotecas dentro de um único repositório, permitindo compartilhar dependências de forma eficiente e padronizar configurações de build e teste. Além disso, essas ferramentas podem acelerar processos de compilação e integração contínua, garantindo que mudanças em uma parte do código não quebrem outras aplicações ou módulos. Elas também simplificam tarefas como versionamento, publicação de pacotes e execução de scripts em diferentes projetos simultaneamente. A seguir, listamos algumas das mais populares no ecossistema moderno.

- **Nx** ([nx.dev](https://nx.dev)) – Uma plataforma completa para organizar, construir e testar projetos dentro de um monorepo, com suporte a caching inteligente e execução paralela de tarefas.
- **Turborepo** ([turbo.build/repo](https://turbo.build/repo)) – Focado em performance, ideal para projetos JavaScript/TypeScript; ajuda a executar builds e testes rapidamente reaproveitando resultados anteriores.
- **Lerna** ([lerna.js.org](https://lerna.js.org/)) – Facilita a gestão de múltiplos pacotes dentro de um mesmo repositório, cuidando de versionamento, dependências internas e publicação.
- **Bazel** ([bazel.build](https://bazel.build)) – Ferramenta de build poderosa, usada em grandes empresas como Google, capaz de gerenciar projetos enormes e heterogêneos com alta eficiência.

## Referências

- [Monorepo.tools](https://monorepo.tools) – Guia abrangente sobre monorepos, vantagens, desvantagens e ferramentas.
- [Google Research – Why Google Stores Billions of Lines of Code in a Single Repository](https://research.google/pubs/pub45424/) – Estudo sobre a abordagem do Google.
- [Trunk-based Development – Monorepos](https://trunkbaseddevelopment.com/monorepos/) – Monorepos no contexto de integração contínua.
