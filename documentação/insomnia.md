# Insomnia: o que é e como funciona

## Sumário

- [O que é o Insomnia?](#o-que-é-o-insomnia)
- [Por que usar o Insomnia?](#por-que-usar-o-insomnia)
- [Como funciona na prática?](#como-funciona-na-prática)
- [Onde usar o Insomnia?](#onde-usar-o-insomnia)
- [Conclusão](#conclusão)
- [Referências](#referências)

---

## O que é o Insomnia?

O **Insomnia** é uma aplicação de código aberto voltada para o **desenvolvimento e teste de APIs**.  
Assim como o Postman, ele permite criar, organizar e enviar requisições HTTP e gRPC, facilitando a análise das respostas.

Sua proposta é oferecer uma experiência **rápida, minimalista e focada em produtividade**, com menos distrações e uma interface limpa, sem perder funcionalidades importantes.

---

## Por que usar o Insomnia?

O Insomnia se destaca por alguns pontos em relação a outras ferramentas:

- **Interface minimalista**: simples e direta, reduzindo a curva de aprendizado.
- **Suporte a múltiplos protocolos**: além de REST (HTTP), também suporta gRPC, GraphQL e WebSockets.
- **Gerenciamento de variáveis e ambientes**: útil para trabalhar com diferentes servidores (desenvolvimento, homologação, produção).
- **Automação via scripts**: permite usar JavaScript para manipular variáveis e dados em tempo de execução.
- **Open Source**: a comunidade pode contribuir e adaptar a ferramenta.
- **Integração com Git**: facilita o versionamento e colaboração em times.

---

## Como funciona na prática?

Imagine que você precisa consultar informações de usuários em uma API pública. No Insomnia, basta:

1. Abrir o Insomnia e criar um novo **Workspace** (espaço de trabalho).
2. Adicionar uma nova requisição e escolher o método HTTP (GET, POST, etc.).
3. Inserir a URL, por exemplo:

`https://jsonplaceholder.typicode.com/users/1`

4. Clicar em **Send** e visualizar a resposta em JSON.

A interface exibe os dados de forma organizada e, se necessário, você pode configurar **headers**, **parâmetros** e **body** facilmente.

---

## Onde usar o Insomnia?

- **Desenvolvimento**: testar APIs durante a criação de aplicações.
- **QA e Testes**: validar endpoints e simular cenários com variáveis.
- **APIs modernas**: trabalhar com GraphQL, gRPC e WebSockets de forma integrada.
- **Times que versionam coleções**: integração nativa com Git facilita o controle de mudanças.
- **Automação de fluxos**: uso de scripts para preparar dados antes do envio da requisição.

---

## Conclusão

O Insomnia é uma ferramenta poderosa e prática para quem trabalha com APIs.  
Sua proposta minimalista, aliada ao suporte a múltiplos protocolos e à filosofia open source, faz dele uma excelente alternativa ao Postman.  
A escolha entre Insomnia e Postman geralmente depende das preferências da equipe: **Postman tende a ser mais completo em ecossistema, enquanto o Insomnia aposta em simplicidade e leveza**.

Caso queira saber também sobre a alternativa mais popular Postman, você encontra [neste artigo](https://github.com/matheusbc97/guia-dev/blob/main/documenta%C3%A7%C3%A3o/postman.md)

---

## Referências

- [Documentação oficial do Insomnia](https://docs.insomnia.rest/)
- [Insomnia API Client](https://insomnia.rest/)
- [JSONPlaceholder – Fake Online REST API](https://jsonplaceholder.typicode.com/)
- [MDN Web Docs – HTTP](https://developer.mozilla.org/pt-BR/docs/Web/HTTP)
