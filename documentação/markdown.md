# 📚 Guia Prático de Markdown

Um manual rápido e prático para dominar a escrita em Markdown.  
Markdown é uma linguagem de marcação simples que permite formatar texto de forma clara, prática, rápida e compatível com várias plataformas, como GitHub, Notion, Reddit e geradores de sites estáticos.

---

## 📌 Tópicos

- [O que é Markdown?](#o-que-e-markdown)
- [Formatação](#formatacao)
  - [Títulos](#titulos)
  - [Textos](#textos)
- [Listas](#listas)
- [Links](#links)
- [Imagens](#imagens)
- [Códigos](#codigos)
- [Citações](#citacoes)
- [Tabelas](#tabelas)
- [Linhas Horizontais](#linhas-horizontais)
- [Checklists](#checklists)
- [Conclusão](#conclusao)

---

## 📝 O que é Markdown?

Markdown é uma **linguagem de marcação leve** criada por John Gruber em 2004, projetada para ser fácil de escrever e ler no formato puro, mas que se converte em HTML para exibição na web.

✅ **Principais vantagens**:

- Sintaxe simples e intuitiva
- Compatível com diversas plataformas
- Perfeito para documentações, anotações e README de projetos

---

## #️⃣ Títulos

Para criar títulos, use o caractere `#` seguido de um espaço.  
Quanto mais `#`, menor o tamanho do título (de 1 a 6).

```markdown
# Título tamanho 1

## Título tamanho 2

### Título tamanho 3

#### Título tamanho 4

##### Título tamanho 5

###### Título tamanho 6
```

Exemplo de título renderizado:

# Título tamanho 1

## Título tamanho 2

### Título tamanho 3

---

## #️⃣ Textos

### Formatando texto para itálico e negrito

No Markdown, podemos dar destaque a partes do texto usando asteriscos ou underscores.
A quantidade e a combinação desses símbolos definem se o texto ficará em itálico, negrito ou ambos.

Mas para formatar o texto em itálico e negrito não importa **se** estamos usando underscore ou asteriscos mas sim **quantos** deles estamos usando.

### Para itálico usamos `_` ou `*` **uma** vez no início e final da palavra.

```markdown
_itálico_ ou _itálico_
```

> _itálico_ ou _itálico_

---

### Já para negrito usamos `_` ou `*` **duas** vezes no início e final da palavra.

```markdown
**negrito** ou **negrito**
```

> **negrito** ou **negrito**

## 📋 Listas

Listas organizam informações em itens ordenados ou não ordenados, facilitando a leitura e compreensão de sequências ou agrupamentos.

### Lista não ordenada:

```markdown
- Item 1
- Item 2
  - Subitem 2.1
  - Subitem 2.2
```

> - Item 1
> - Item 2
>   - Subitem 2.1
>   - Subitem 2.2

### Lista ordenada:

```markdown
1. Passo um
2. Passo dois
3. Passo três
```

> 1. Passo um
> 2. Passo dois
> 3. Passo três

## 🔗 Links

Para inserir links, o Markdown usa colchetes para o texto clicável e parênteses para o endereço da URL, podendo incluir títulos opcionais.

```markdown
[Texto do link](https://exemplo.com)
[OpenAI](https://openai.com "Visite a OpenAI")
```

> [Texto do link](https://exemplo.com)  
> [OpenAI](https://openai.com "Visite a OpenAI")

Como pode notar, além do texto clicável e do endereço, é possível adicionar um título opcional entre aspas depois da URL.  
Esse título funciona como uma pequena mensagem que aparece quando o mouse passa sobre o link (_tooltip_), ajudando a dar mais contexto ou informação sem deixar o texto poluído.

## 🖼️ Imagens

Inserir imagens no Markdown é semelhante a links, mas precedido de um ponto de exclamação, contendo uma descrição alternativa e o endereço da imagem.

```markdown
![descrição da imagem](https://rseat.pics/)
```

> ![descrição da imagem](https://rseat.pics/)

## 💻 Códigos

Podemos facilitar a leitura de códigos em linha usando `crases simples`, tornando a explicação em documentações mais clara, o que
também pode ser útil para destacar texto de forma geral.

```markdown
Use o comando `npm install`
```

> Use o comando `npm install`

Também é possível criar blocos de código com três crases, com indicação opcional da linguagem a ser exibida.

````markdown
```javascript
function ola() {
  console.log("Olá, mundo!");
}
```
````

```javascript
function ola() {
  console.log("Olá, mundo!");
}
```

## 💬 Citações

Citações são criadas com o símbolo de maior `>` e servem para destacar trechos ou referências dentro do texto.

```markdown
> Isto é uma citação
```

> Isto é uma citação

Também é possível fazer uma citação dentro de outra:

```markdown
> Isto é uma citação
>
> > Citação dentro de citação
```

> Isto é uma citação
>
> > Citação dentro de citação

## 📊 Tabelas

Tabelas organizam dados em linhas e colunas, usando pipes `|` para separar células e hífens `-` para definir os cabeçalhos.

```markdown
| Nome   | Idade | Cidade         |
| ------ | ----- | -------------- |
| Ana    | 25    | São Paulo      |
| Carlos | 30    | Rio de Janeiro |
```

> | Nome   | Idade | Cidade         |
> | ------ | ----- | -------------- |
> | Ana    | 25    | São Paulo      |
> | Carlos | 30    | Rio de Janeiro |

## ➖ Linhas Horizontais

Linhas horizontais são usadas para separar seções no texto e podem ser feitas de 3 formas diferentes:

```markdown
---
---

---
```

---

---

---

## ✅ Checklists

Checklists são listas com caixas de seleção, muito úteis para mostrar tarefas concluídas ou pendentes, e são feitas dessa forma:

```markdown
[x] Tarefa concluída
[ ] Tarefa pendente
```

> [x] Tarefa concluída  
> [ ] Tarefa pendente

## 🎯 Conclusão

O Markdown é uma ferramenta simples, versátil e poderosa para criar textos formatados de forma rápida.
Ele é amplamente usado para documentação de projetos, anotações pessoais, blogs e qualquer conteúdo que precise ser lido tanto no formato cru quanto renderizado.

---

## 📖 Referências

- [The Markdown Guide](https://www.markdownguide.org/) — Guia completo e atualizado para Markdown.
