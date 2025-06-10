# Limitação de Linhas por Arquivo

Para manter a legibilidade, organização e manutenibilidade do código, adotamos uma política de limitação de linhas nos arquivos do projeto NestJS.

## Diretriz

- **Não permitir que um arquivo ultrapasse 300 linhas.**
- A partir de **250 linhas**, deve-se **avaliar e iniciar o particionamento** do conteúdo do arquivo.
- Essa prática visa evitar a concentração de muita lógica em um único local, promovendo:
  - Separação de responsabilidades
  - Maior clareza e facilidade de testes
  - Melhor reutilização de código
  - Redução de conflitos em merge

## Como particionar

Dependendo do tipo de arquivo, seguem algumas estratégias comuns:

### Arquivos de Service

- Extrair métodos auxiliares para **providers reutilizáveis**.
- Criar **sub-services** específicos (por domínio ou responsabilidade).
- Mover validações e regras de negócio para **classes utilitárias** ou **use cases**.

### Arquivos de Controller

- Dividir o controller em **módulos menores** (por recurso, operação ou escopo).
- Extrair lógicas para o **Service**, evitando implementações complexas no controller.

### Arquivos DTOs ou Schemas

- Dividir grandes DTOs em **subclasses** ou **interfaces auxiliares**.
- Separar validações específicas em **arquivos próprios**, mantendo a clareza.

## Exemplo prático

Se um `UserService` estiver crescendo demais, considere:

```bash
src/
└── users/
    ├── user.service.ts              # Orquestra as chamadas principais
    ├── user-validation.service.ts   # Contém regras de validação específicas
    └── user-notification.service.ts # Responsável por envio de e-mails, notificações etc.
