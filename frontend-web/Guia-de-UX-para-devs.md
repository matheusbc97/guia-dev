# Guia de UX/Projetos para desenvolvedores frontend

# Lidando com Requisições

1. Sempre mostrar um loading enquanto estiver esperando resposta da requisicao
    1. Somente mostrar loading que ocupe a tela inteira se você quiser que o usuário na faça nenhuma ação a mais 
    *com loading que ocupa a tela interia quero dizer daqueles loadings que ocupam toda a tela (normalmente escurecendo o fundo) e impedem que o usuário faça qualquer ação*
    2. Caso contrário mostrar loading local, somente onde está sendo carregado
2. Sempre mostrar mensagem de erro uma requisição retornar erro
    1. Se possível (principalmente em aplicativos mobile onde não é possível dar um f5) ao dar erro dar possibilidade do usuário refazer requisição
3. Cancelar a requisição caso ela não faça mais sentido (Por exemplo o usuário foi para outra tela)

# Lidando com formulários

1. Implementar validações sempre que relevante
ex 1: o input de email deverá ser validado se o texto está em um formato de email válido (com “@” e “.”)
2. Evitar desabilitar botão de submit
Muitos formulários desabilitam o botão do submit até o formulário estar preenchido e válido, o problema é que normalmente não fica claro ao usuário onde está o problema, o que faz ele perder um tempo até conseguir concertar o que está errado no formulário
    1. Ao clicar no botão de submit mostrar mensagem indicando quais campos não foram preenchidos ou estão inválidos, dandos destaque a este campo e informando quais são os erros
    2. A única exceção é se o formulário for composto por somente um input, a questão aqui é ficar claro o que está impedindo o usuário de dar submit

# Não seja reduntante

Por exemplo se a tela no header já tem o nome da tela, porque repetir novamente o nome?

# Botões

1. Sempre garantir que o botão ocupa espaço suficiente para ser clicado sem problemas
2. Se o botão for um ícone mostrar um tootip ao usuário passar o mouse (WEB)
3. Coloque os botão mais utilizados em areas mais faceis do usuário clicar

# Visibilidade

1. Garanta que todos os componentes estejam visíveis na tela, no mundo mobile é muito comum ter celulares com diferentes designs e portanto em alguns casos os componentes acabam desaparecendo, normalmente os frameworks atuais vem com algum componente para resolver esse problema (Mobile) 
ex 1: No iphone as vezes um componente pode ficar acima da status bar
ex 2: em um 

# Navegação

1. Se usar uma navegação superior colocar funcionalidade do usuário arrastar para outra tela sem ter que clicar de fato no botão
2. Previna que clique duplo abra 2 telas de uma vez só

# Deletando Itens

1. Sempre que for deletar um item ou mostrar um pop up perguntando se o usuário tem certeza que quer deletar o item ou mostrar uma mensagem possiblitando o usuário reaver o item

# Cuidado com o darkmode

1. Por mais que o seu app não utilize darkmode alguns celulares pode forçar o darkmode por isso teste o darkmode mesmo que não tenha sido implementado e se vc tiver algum problema proiba os apps de utilizarem o darkmode

# Limpeza de dados

1. Ao fim de qualquer fluxo limpar os dados (por exemplo logout)

# Recarregando dados

1. Quando criar ou alterar garantir o recarregamento de dados caso necessário (Exemplo uma listagem de produtos ao editar o produto)
2. Sempre dê a possíbilidade do usuário recarregar os dados ao puxar tela para baixo

# Cacheando dados

1. Um sugestão não prioritária mas que melhora a UX é salvar os dados em cache para não recarregar os dados toda vez que o usuário entre em tela (Lembrar de recarregar os dados de tempo em tempo)

# Dados Sensível

1. Caso precisar salvar algum dado sensível offline no celular garantir que os dados estão sendo salvos de forma segura

# Ambiente de Homologação

1. o aplicativo precisará ser instalado como outro aplicativo (homologação) para não conflitar com o ambiente de produção?
2. Algum serviço externo usado pelo app precisa de um ambiente de homologação?

# Loadings

1. Preferir skeleton ao fazer loading pois dá uma experiência melhor ao usuário