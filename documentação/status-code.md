# Status Codes HTTP: Entendendo sua Importância

## Sumário

1. [Introdução](#introdução)
2. [Por que os Status Codes são importantes?](#por-que-os-status-codes-são-importantes)
3. [Estrutura dos Status Codes](#estrutura-dos-status-codes)
4. [Códigos de Status HTTP Mais Comuns](#códigos-de-status-http-mais-comuns)
5. [Lista Completa de Códigos de Status HTTP](#lista-completa-de-códigos-de-status-http)
6. [Referências](#referências)

---

## Introdução

Os status codes HTTP são códigos numéricos enviados pelo servidor para o cliente (como navegadores ou aplicativos) em resposta a uma requisição HTTP. Eles comunicam o resultado da requisição, indicando se a ação foi bem-sucedida, se houve erro, se é necessário fornecer mais informações ou se o recurso solicitado foi movido. Sem eles, clientes e servidores teriam dificuldade em se comunicar de forma padronizada, tornando a web muito menos confiável e previsível.

---

## Por que os Status Codes são importantes?

- **Comunicação clara:** Um status code informa ao cliente exatamente o que aconteceu, sem precisar decifrar mensagens complexas ou páginas HTML.
- **Automação e scripts:** Programas que interagem com a web dependem dos códigos para tomar decisões, como tentar novamente em caso de falha ou redirecionar para outro endereço.
- **Depuração e monitoramento:** Analistas de sistemas usam status codes para identificar problemas e falhas em aplicativos ou sites.
- **SEO e experiência do usuário:** Motores de busca e navegadores usam esses códigos para indexação e navegação eficiente, impactando a performance e visibilidade de sites.

---

## Estrutura dos Status Codes

Os códigos HTTP são números de três dígitos, onde o primeiro dígito indica a categoria:

| Categoria | Faixa   | Significado                                                                       |
| --------- | ------- | --------------------------------------------------------------------------------- |
| 1xx       | 100–199 | Informativo – a requisição foi recebida e o processo continua                     |
| 2xx       | 200–299 | Sucesso – a ação foi concluída com sucesso                                        |
| 3xx       | 300–399 | Redirecionamento – o cliente deve realizar outra ação para completar a requisição |
| 4xx       | 400–499 | Erro do cliente – a requisição contém algum problema                              |
| 5xx       | 500–599 | Erro do servidor – o servidor falhou ao processar a requisição                    |

---

## Códigos de Status HTTP Mais Comuns

### Sucesso (2xx)

- **200 OK:** A requisição foi bem-sucedida e o servidor retornou os dados solicitados.
- **201 Created:** A requisição foi bem-sucedida e resultou na criação de um novo recurso.
- **204 No Content:** A requisição foi bem-sucedida, mas não há conteúdo para retornar.

### Redirecionamento (3xx)

- **301 Moved Permanently:** O recurso solicitado foi movido permanentemente para outra URL.
- **302 Found:** O recurso solicitado foi temporariamente movido para outra URL.
- **304 Not Modified:** O recurso não foi modificado desde a última requisição, permitindo que o cliente use a versão em cache.

### Erro do Cliente (4xx)

- **400 Bad Request:** A requisição não pôde ser entendida pelo servidor devido a sintaxe inválida.
- **401 Unauthorized:** A requisição requer autenticação do usuário.
- **403 Forbidden:** O servidor entendeu a requisição, mas se recusa a autorizá-la.
- **404 Not Found:** O recurso solicitado não foi encontrado no servidor.

### Erro do Servidor (5xx)

- **500 Internal Server Error:** O servidor encontrou uma condição inesperada que o impediu de atender à requisição.
- **502 Bad Gateway:** O servidor, atuando como gateway ou proxy, recebeu uma resposta inválida do servidor upstream.
- **503 Service Unavailable:** O servidor não está pronto para manipular a requisição devido a manutenção ou sobrecarga temporária.

---

## Lista Completa de Códigos de Status HTTP

### 1xx – Informativo

- 100 Continue
- 101 Switching Protocols

### 2xx – Sucesso

- 200 OK
- 201 Created
- 202 Accepted
- 203 Non-Authoritative Information
- 204 No Content
- 205 Reset Content
- 206 Partial Content

### 3xx – Redirecionamento

- 300 Multiple Choices
- 301 Moved Permanently
- 302 Found
- 303 See Other
- 304 Not Modified
- 305 Use Proxy
- 306 Switch Proxy
- 307 Temporary Redirect
- 308 Permanent Redirect

### 4xx – Erro do Cliente

- 400 Bad Request
- 401 Unauthorized
- 402 Payment Required
- 403 Forbidden
- 404 Not Found
- 405 Method Not Allowed
- 406 Not Acceptable
- 407 Proxy Authentication Required
- 408 Request Timeout
- 409 Conflict
- 410 Gone
- 411 Length Required
- 412 Precondition Failed
- 413 Payload Too Large
- 414 URI Too Long
- 415 Unsupported Media Type
- 416 Range Not Satisfiable
- 417 Expectation Failed
- 418 I'm a teapot
- 421 Misdirected Request
- 422 Unprocessable Entity
- 423 Locked
- 424 Failed Dependency
- 426 Upgrade Required
- 428 Precondition Required
- 429 Too Many Requests
- 431 Request Header Fields Too Large
- 451 Unavailable For Legal Reasons

### 5xx – Erro do Servidor

- 500 Internal Server Error
- 501 Not Implemented
- 502 Bad Gateway
- 503 Service Unavailable
- 504 Gateway Timeout
- 505 HTTP Version Not Supported
- 506 Variant Also Negotiates
- 507 Insufficient Storage
- 508 Loop Detected
- 510 Not Extended
- 511 Network Authentication Required

---

## Referências

1. [MDN Web Docs – Códigos de Status de Resposta HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status?utm_source=chatgpt.com)  
   Referência oficial que lista e explica os códigos de status HTTP, agrupados por categorias.

2. [RFC 9110 – HTTP Semantics](https://datatracker.ietf.org/doc/html/rfc9110)  
   Documento oficial do IETF que define os códigos de status HTTP, suas semânticas e comportamentos esperados.
