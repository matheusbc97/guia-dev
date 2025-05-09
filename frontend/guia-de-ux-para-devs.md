# Guia de UX/Projetos para Desenvolvedores Frontend

## Lidando com Requisições

1. **Mostre um _loading_ enquanto aguarda a resposta da requisição:**
   - Use um _loading_ que ocupa a tela inteira **apenas** se deseja impedir ações adicionais do usuário.
     - _Exemplo:_ Um _loading_ que escurece o fundo e bloqueia interações.
   - Caso contrário, utilize _loading_ local, apenas na área onde o conteúdo está sendo carregado.

2. **Exiba mensagens de erro sempre que uma requisição falhar:**
   - Permita que o usuário tente novamente, especialmente em apps _mobile_ onde não há como atualizar a tela (F5).

3. **Cancele requisições que não fazem mais sentido:**
   - _Exemplo:_ O usuário mudou de tela antes da conclusão da requisição.

4. **Configuração de timeouts:**
   - Sempre defina um tempo limite para as requisições para evitar que o app fique travado aguardando indefinidamente.
      - _Exemplo:_ Cancelar Requisições que demoram mais de 60 segundos automaticamente.
---

## Lidando com Formulários

1. **Implemente validações relevantes:**
   - _Exemplo:_ O campo de e-mail deve validar se o texto está em um formato válido (com "@" e ".").

2. **Evite desabilitar o botão de envio (_submit_):**
   - Se o botão for clicado com erros, destaque os campos inválidos e informe os erros ao usuário.
   - **Exceção:** Formulários com apenas um campo, onde o erro é óbvio.

---

## Não Seja Redundante

- Se o nome da tela já está no _header_, não o repita no conteúdo principal.

---

## Botões

1. **Garanta que os botões sejam fáceis de clicar:**
   - O tamanho deve permitir cliques precisos.

2. **Se for um botão com ícone, mostre um _tooltip_ ao passar o mouse (WEB).**

3. **Posicione os botões mais utilizados em áreas de fácil acesso.**

---

## Visibilidade

1. **Garanta que todos os componentes estejam visíveis:**
   - No _mobile_, diferentes tamanhos de tela podem ocultar componentes.
   - _Exemplo 1:_ Um elemento acima da _status bar_ no iPhone.
   - _Exemplo 2:_ Componentes cortados por layouts incompatíveis.

---

## Navegação

1. **Implemente navegação por gesto:**
   - Permita que o usuário deslize para trocar de tela, além de usar os botões.

2. **Previna cliques duplos:**
   - Evite que cliques repetidos abram múltiplas telas.

---

## Deletando Itens

- Mostre uma confirmação antes de deletar:
  - Pode ser um _popup_ ou uma mensagem que permita desfazer a ação.

---

## Cuidado com o Dark Mode

1. Mesmo que o app não implemente o _dark mode_, teste-o:
   - Alguns dispositivos forçam o _dark mode_, o que pode causar problemas.
   - Se necessário, bloqueie o _dark mode_ no app.

---

## Limpeza de Dados

- Ao finalizar um fluxo, limpe os dados armazenados:
  - _Exemplo:_ Após o logout.

---

## Recarregando Dados

1. **Garanta o recarregamento dos dados após ações relevantes:**
   - _Exemplo:_ Atualizar uma lista de produtos ao editar um item.

2. **Ofereça a possibilidade de recarregar a tela com _pull-to-refresh_.**

---

## Cacheando Dados

- **Sugestão:** Utilize cache para melhorar a experiência do usuário:
  - Salve dados localmente para evitar carregamentos desnecessários.
  - Recarregue os dados periodicamente para mantê-los atualizados.

---

## Dados Sensíveis

- Caso precise armazenar dados sensíveis offline, garanta que eles estejam seguros.

---

## Ambiente de Homologação

1. **Verifique se o app de homologação precisa ser instalado como um app separado:**
   - Evite conflitos com o ambiente de produção.

2. **Garanta que os serviços externos suportem ambientes de homologação.**

---

## Loadings

- Prefira **skeletons** em vez de _loadings_ genéricos:
  - Skeletons melhoram a experiência visual do usuário enquanto os dados carregam.
