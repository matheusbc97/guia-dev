# Estrutura de pastas no React Native

## Nomenclatura
Sempre utilizar Kebab case (nome-da-pasta) para pastas quando forem somente pastas de organização, Pascal case (NomeDoComponente) para componentes para deixar intuitivo para quem está lendo

## Exemplo estrutura de pastas
Segue abaixo exemplo de estrutura de pastas simulando a estrutura de um ecomerce

<code>
- core  <br>
&nbsp;&nbsp;- components<br>
&nbsp;&nbsp;- configs<br>
&nbsp;&nbsp;- hooks<br>
&nbsp;&nbsp;- providers<br>
- features <br>
&nbsp;&nbsp;- auth<br>
&nbsp;&nbsp;&nbsp;&nbsp;- pages<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- LoginPage<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- RegisterPage<br>
&nbsp;&nbsp;- home<br>
&nbsp;&nbsp;- products<br>
- shared <br>
&nbsp;&nbsp;- components<br>
&nbsp;&nbsp;- constants<br>
&nbsp;&nbsp;- hooks<br>
&nbsp;&nbsp;- types<br>
&nbsp;&nbsp;- utils<br>
</code>