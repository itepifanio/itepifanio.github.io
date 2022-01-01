---
layout: post
title:  "TALL - Uma nova stack para PHP"
date:   2020-06-19 17:09:20 -0300
---

[**T**ailwind](https://tailwindcss.com/), [**A**lpinejs](https://github.com/alpinejs/alpine), [**L**aravel](https://laravel.com/) e [**L**ivewire](https://laravel-livewire.com/) (**TALL**) é uma solução para desenvolvedores full stack [construída pela comunidade laravel](https://tallstack.dev/) que foca principalmente no desenvolvimento backend, mas que permite o desenvolvimento de sistemas ditos "reativos".

A stack TALL é ótima para desenvolvimento rápido de sistemas web. A facilidade de estilizar páginas com o Tailwind, o poder da reatividade do Alpinejs, aliado com a componentização do Livewire, realmente dá um boost de produtividade no desenvolvimento.

Nesse artigo falarei um pouco sobre as 4 tecnologias e minha experiência com a stack.

## Livewire

É muito comum encontrar sistemas que utilizam Laravel em conjunto com o Vuejs. A utilização de componentes Vue remove muito da responsabilidade da blade, por exemplo, é comum encontrarmos blades do tipo:

```php
@extends(‘layouts.base’)

@section(‘content’)
    <some-vue-component></some-vue-component>
@endsection
```

Caleb, criador do Alpinejs e Livewire, [chama](https://www.youtube.com/watch?v=uQO4Xh1gMpY) esses componentes de "assassinos de blades". Vue é uma ferramenta poderosa, mas o tempo gasto tratando eventos assíncronos, adicionando v-ifs, atualizando bibliotecas, atrasa o desenvolvimento e torna a experiência um pouco maçante. Parte do atraso mencionado se deve a falta de testes unitários, eu, particularmente, não conheço ninguém que utilize testes unitários com Vue e isso é bem problemático quando encontramos blades e blades como a exibida acima.

Quanto mais se trabalha com Vue e Laravel mais sentimos a necessidade de escrever um código javascript melhor, aprender Vuex, utilizar testes unitários nele usando Jest ou outra lib. Vamos adicionando camadas e camadas de complexidade para algo que deveria ser simples: requisição e exibição de dados (o pior dos casos é quando regra de negócio entra em front-end, debugar um erro em um código assim é uma grande dor de cabeça).

Caleb propõe uma solução voltada mais ao backend, intrínseca ao Laravel, o Livewire. É difícil definir a ferramenta, mas é como se escrevessemos código Laravel como componentes. A definição oficial é: ` Livewire is a full-stack framework for Laravel that makes building dynamic interfaces simple, without leaving the comfort of Laravel. `.

O Livewire é ótimo para situações em que o nosso usuário interage com a tela e espera uma ação imediata, ele irá fazer uma requisição ajax e atualizar o front automaticamente (como se a página fosse reativa). Um exemplo, visto abaixo, retirado do [artigo do Branick](https://medium.com/@branick/search-with-laravel-livewire-cb6dcd4ad541).

![Search with Laravel Livewire](https://miro.medium.com/max/1400/1*vTfmPgyEaCmPgqpR8DDWzw.gif)

O Livewire é uma ferramenta muito poderosa que permite reaproveitar código através dos componentes, além de facilitar e agilizar o desenvolvimento de interfaces ricas, sem ter que chamar bibliotecas JS externas, sem sair do arcabouço Laravel e podendo realizar testes unitários nos componentes. Entretanto todas essas facilidades tem um preço, que é o custo de renderizar novamente HTML toda vez que se faz uma requisição. O Livewire não é uma “bala de prata” e deve ser utilizado com cautela. 

## Tailwind

O Tailwind é um framework CSS com uma abordagem *utility-first*
, o código CSS é abstraído no HTML como classes. Por exemplo, o código ` <div style="background-color:black; border-radius: 100%"></div> ` no Tailwind ficaria ` <div class="bg-black round-full"><div> `. 

O primeiro contato com o framework é estranho porque o HTML se torna extenso de escrever, mas a medida que vamos utilizando vemos o quão ágil é utilizar o Tailwind. As páginas são escritas eficientemente, se inspeciona elemento, muda as classes, copia para o código e em minutos você tem algo funcional que levaria  mais tempo para fazer utilizando Bootstrap.

Esse esquema quase de prototipação de páginas é ótimo para fábricas de software. Uma vez que os desenvolvedores pegam o jeito como o framework se torna fácil pegar um design do Adobe XD e dar vida no HTML.

## AlpineJS

O Alpinejs é um microframework JS, reativo, muito parecido com Vue (só que bem mais simples) que facilita manipulações do DOM. Por ter sido criado pela mesma pessoa, o Alpinejs funciona muito bem com integrações com o Livewire. Todos os gargalos de performance encontrados no Livewire eu consegui contornar utilizando o Alpine em conjunto. 

Um exemplo de utilização do Alpine em conjunto com o Tailwind pode ser visto abaixo. Note que o código HTML mantém a estilização e o JS embutido, é muito simples e rápido estilizar e modificar o DOM utilizando as duas ferramentas em conjunto.

{% include codepen.html hash="VwvreoP" title="Simple CRUD" %}

A curva de aprendizado do framework é muito baixa porque ele é bem pequeno, além de procurar se aproximar bastante da sintaxe do Vue (velho conhecido dos devs fullstack Laravel).

## Conclusão

Estou trabalhando com a stack a cerca de três ou quatro meses, escrevendo uma nova versão de um sistema que antes era feito com Laravel e Vue. O design foi criado no Adobe XD e em questão de uma a duas semanas já tínhamos passado completamente pro Tailwind. A utilização do Livewire foi feita a medida da necessidade, em geral, situações que exigiria requisições ajax ou que apelariamos para o Vue, se tornaram componentes Livewire.

A impressão é que o novo sistema de componentes blade do Laravel 6 e as novas funcionalidades do Laravel 7 também colaboraram muito para essa nova forma de escrever sistemas, tornando natural codar no Laravel componentizado e associar o Livewire nas blades. 

No começo do projeto eu não conhecia Livewire, Alpinejs e nem o Tailwind, mas é muito bom sair do conforto com esses três. Como o Tailwind é mais "baixo nível" que o Bootstrap eu acabei aprendendo flexbox e vários outros detalhes de CSS que eu desconhecia. O mesmo aconteceu com o Alpinejs, por ser pequeno boa parte do código feito com ele é JS puro.

O Tall potencializa as tecnologias básicas que usamos no dia a dia (JS, CSS, PHP) tornando o desenvolvimento bem mais divertido e sem necessidade de adicionar bibliotecas terceiras que acabam complicando a manutenção posterior do sistema. Além disso, o que mais curto na stack, é que se aproveita ao máximo o uso do Laravel.