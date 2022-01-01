---
layout: post
title:  "Carregamento lento com scroll horizontal"
date:   2021-10-23 17:09:20 -0300
---

Recentemente me deparei com o seguinte cenário: um sistema de gerenciamentos de fluxos de trabalho que permite configuração  de kanbans, como o da imagem abaixo, sendo que um usuário em particular configurou seu kanban com 38 colunas.

Cada coluna do kanban realizava uma requisição e do jeito que o sistema tinha sido desenvolvido gerava-se 38 requisições assim que a página era carregada, o que acabava espancando o banco de dados e o servidor.

![Ilustração de um kanban com cinco colunas na sequência: stories, todo, in progress, testing, done](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/6ui3slceaoxqovpxm1uo.jpg)

Inicialmente precisavamos diminuir a quantidade de requisições, limitando apenas aos cards visíveis na tela do usuário. Depois precisavamos fazer com que, caso o usuário rolasse para o fim da página de uma vez, as colunas que ficaram visíveis não carregassem a menos que estivessem a um certo tempo visíveis.

## Limitando o carregamento aos cards visíveis

O javascript oferece uma API chamada [IntersectionObserver](https://developer.mozilla.org/en-US/docs/Web/API/IntersectionObserver) que permite monitorar elementos HTML e verificar sua visibilidade na tela. O código abaixo mostra o funcionamento mais básico dela.

```javascript
const onIntersection = (elements) => {
    elements.forEach(element => {
      if (element.isIntersecting) {
          console.log(element, 'is visible');
      }
  });
};

const observer = new IntersectionObserver(onIntersection);

observer.observe(document.querySelector('.my-elements'));
```

A função `onIntersection` é responsável pela lógica que será aplicada aos elementos visiveis, ela recebe uma lista de elementos e verifica que se forem visiveis (` element.isIntersecting `) então algo será feito, nesse caso uma mensagem no console é exibida.

A chamada da API ` IntersectionObserver ` é feita e atribuida a variável ` observer `. O objeto ` observer ` conseguirá a partir dali observar elementos no HTML e executar uma lógica somente quando eles forem visíveis na tela do usuário. No meu caso, do kanban gigante, isso foi suficiente para limitar as 38 requisições assim que a página carregava para apenas 5, mas caso o usuário rolasse a página rapidamente várias requisições seriam feitas, ou seja, se eu fosse até o fim da página de uma vez as outras 33 requisições seriam chamadas também de uma vez só.

## Carregamento apenas após certo tempo do elemento visível na página

A API ` IntersectionObserver ` tem uma [versão 2](https://web.dev/intersectionobserver-v2/) que permite a captura de quanto tempo um certo elemento HTML ficou visível na tela e isso resolveria facilmente o problema de carregar o elemento HTML apenas depois de certo tempo. Entretanto, a versão 2 ainda não tem suas implementações compativeis com a maioria dos navegadores.

No meu caso específico eu estava utilizando um componente pai que renderizava os 38 elementos filhos e eu não conseguia verificar quando esses 38 elementos filhos terminaram de ser renderizados para observa-los com o ` InsertersectionObserver `, então controlar o tempo que cada elemento ficou visível na tela ficou um pouco mais complicado.

Cada um dos 38 elementos filhos sabiam quando eles mesmos eram renderizados, então conseguia-se utilizar a ` IntersectionObserver ` internamente em cada um deles. Utilizando a função ` setTimeout ` do javascript consegue-se observação o elemento após um certo tempo especificado em milisegundos.

Temos 38 elementos ao todo, só que a maioria não é visível na tela e se torna visível ao scrollar, com o delay do ` setTimeout ` essa ação leva ainda algum tempo a ser executada. Durante o scroll, quando o elemento visível na tela ainda não disparou o `setTimeout` especificado e o usuário já scrollou para um elemento seguinte consegue-se remover o timeout do elemento anterior da pilha de execução e então carregar somente o elemento seguinte. O código a seguir mostra essa estratégia.

```javascript
<div class="border border-black m-1 p-10 min-w-max h-10"
       x-data=""
       x-init="() => {
           let timeout;
           let loadColumn = function (elements) {
               clearTimeout(timeout);
               
               timeout = setTimeout(function() {
                   elements.forEach(element => {
                       if (element.isIntersecting) {
                           // do something
                           observer.unobserve(element.target);
                       }
                   });
               }, 750);
           }
           
           let observer = new IntersectionObserver(loadColumn);
           let target = $el;
           observer.observe(target);
       }">
  </div>
```

Quando o componente é carregado na página ele já começa a observar a si mesmo utilizando a função ` loadColumn `. Tal função remove os timeouts anteriores (que não foram acionados) da pilha de execução e adiciona um novo timeout que após 750 milisegundos faz algo e remove a observação para não refazer a mesma lógica se o elemento se tornar visível novamente.

No meu caso a lógica era a requisição para o servidor então eu só precisava carregar o dado uma vez e depois ignorar se o elemento ficasse visível novamente na página, por isso ele remove a própria observação.

Achou a sintaxe do código acima estranha? Esse microframework javascript se chama [AlpineJS](https://alpinejs.dev/) e foi o que utilizei para desenvolver a solução completa. Uma POC mais simples, sem a requisição pro servidor, pode ser vista logo abaixo. Após ficar visível na sua tela os quadrados brancos se tornarão pretos indicando a requisição pro servidor.

{% include codepen.html hash="PoKqGPm" title="Carregamento lento com scroll horizontal" %}

Caso se interesse por ver uma solução com vanilla javascript  a minha referência [foi essa](https://www.codeguage.com/tutorials/lazy-loading/intersection-observer). 
 