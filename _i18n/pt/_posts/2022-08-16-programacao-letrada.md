---
layout: post
title: 'Programação letrada com Jupyter Notebook e Nbdev'
date: 2022-08-16 17:09:20 -0300
---

O ambiente de desenvolvimento [Jupyter notebook](https://jupyter.org/) é muito popular entre a comunidade científica. Com essa ferramenta você consegue escrever texto em formato markdown e código Python (R ou Julia) no mesmo arquivo, algo que pode melhorar a legibilidade e entendimento do seu programa. Esse paradigma, que mistura texto e código, é chamado de [programação letrada](https://pt.wikipedia.org/wiki/Programa%C3%A7%C3%A3o_letrada).

Um exemplo de Jupyter notebook pode ser vista na imagem abaixo:

![Parte de um Jupyter notebook que inclui uma seção com texto em formato markdown e código python](/assets/jupyter-markdown-and-code.png)

Programação letrada é um paradigma muito bem conceituado, formalmente discutido por muitos pesquisadores respeitados mundialmente como o [Donald Knuth](https://pt.wikipedia.org/wiki/Donald_Knuth). Ao mesmo tempo, Jupyter notebooks são considerados ineficientes para o desenvolvimento de software. Essa controversia levou a criação da famosa palestra "[Eu não gosto de notebooks](https://www.youtube.com/watch?v=7jiPeIFXb6U)", respondida por outra palestra intitulada "[Eu gosto de Jupyter notebooks](https://www.youtube.com/watch?v=7jiPeIFXb6U)" que gerou [bastante drama]((https://www.fast.ai/2020/10/28/code-of-conduct/)) na comunidade Python.

![Capa do vídeo "Eu gosto de Jupyter notebooks" que, além do título garrafal, mostra ao fundo o Lula Molusco em cima de um palco, se esquivando de tomates sendo jogados pela plateia](/assets/i-like-notebooks.jpg)

Jupyter notebooks tem sido limitados a exploração de dados, pequenos scripts e materiais educacionais. A recente introdução da [Nbdev](https://nbdev.fast.ai/), uma biblioteca python, expandiu as possibilidades desses notebooks. Nbdev permite o desenvolvimento e distribuição de pacotes python enquanto se beneficia do paradigma de programação letrada, permitindo a execução de testes, documentação do software em tempo real (unindo texto e código), publicação da documentação como arquivos estáticos ou simplesmente o desenvolvimento de material técnico.

> Nbdev permite que você conte uma história com o seu código. É uma ferramenta prática e poderosa!

Nbdev tem se provado útil no desenvolvimento de grandes e sérios projetos como o [FastAi](https://github.com/fastai/fastai). A utilização da biblioteca Nbdev com Jupyter notebooks permite o desenvolvimento de softwares com qualidade e com os benefícios da programação letrada.

## Experiência

Minha primeira experiência com Nbdev foi a de estranhamento. Trabalhar com Jupyter notebooks para desenvolvimento sério de software não me parecia natural, algo esperado, afinal é um novo paradigma de programação.

A ferramenta em que estou trabalhando atualmente, [Ipyannotator](https://github.com/palaimon/ipyannotator), é um framework de anotações open source que contém interfaces gráficas que funcionam no Jupyter notebook. O desenvolvimento do Ipyannotator só foi possível graças a ferramenta Nbdev que permitiu o time testar o software em notebooks e exportar o código como uma biblioteca python.

> Depois de um ano desenvolvendo software com Jupyter notebook eu sinto que isso melhorou minha produtividade

Esse paradigma de desenvolvimento de software me permitiu manter a minha documentação atualizada, uma vez que a documentação está naturalmente acima do meu bloco de código Python. O paradigma também reduziu o lapso mental de voltar a um código antigo, facilitando o entendimento do código uma vez que decisões prévias estavam documentadas em blocos markdown.

## Quarto

No dia 28 de Julho, Nbdev lançou sua segunda versão, incorporando outra ferramenta open source no seu arsenal: [Quarto](https://quarto.org/). Quarto é uma ferramenta que permite a criação de conteúdo técnico utilizando Python, R ou Julia, utilizando diversos tipos de arquivo, seja markdown, Jupyter notebooks, R notebooks e permitindo exportar esses arquivos como arquivos, websites, blogs, HTML, PDFs, EPubs e até slides.

> Quarto é uma solução completa para escrever qualquer material técnico, utilizando as ferramentas que você já conhece.

Essa ferramenta é tão legal que estou planejando migrar [o meu blog pessoal](https://itepifanio.github.io) de Jekyll para Quarto. O design clean, de fácil usabilidade e com a funcionalidade de executar código embutido em blocos de texto, se encaixa perfeitamente em qualquer requisito de escrita técnica.

Nbdev notou o quão poderoso Quarto pode ser. Essa adição do Quarto ao core do Nbdev ajudou a renderizar melhor sites e documentações. A primeira versão da biblioteca Nbdev já continha essas funcionalidades, mas elas eram rudimentares e precisavam de diversas gambiarras. 

## Conclusão

Desenvolvimento com Nbdev e Quarto pode melhorar a produtividade de diversos times, ajudando a documentar e contar a história do seu código. Essas ferramentas ajudam a expandir as possibilidades de desenvolvimento de software, assim como foi o caso do já exemplificado [Ipyannotator](https://github.com/palaimon/ipyannotator).

Como qualquer ferramenta, Nbdev também tem lados negativos. Um deles é a falta do auto completar em Jupyter notebooks, algo que pode ser remediado com a utilização de extensões do Visual Code, por exemplo. Outro problema é que, por conta dos Jupyter notebooks serem escritos em formato json, um formato que dificulta a resolução de conflitos git por conta de todos os metadados extras. Dificultar a resolução de conflitos minimiza as chances de grandes equipes de trabalhar no mesmo software.

Felizmente, a adição de Quarto mostra que Nbdev já planeja dar suporte a outros tipos de arquivos além de Jupyter notebooks. Isso permitiria que times maiores conseguissem desenvolver software com programação letrada, diminuindo o maior defeito da ferramenta, que é a resolução de conflitos.

Se você se interessou em tentar usar Nbdev você pode checar as seguintes referências:
[Nbdev+Quarto: Uma nova arma secreta de produtividade](https://www.fast.ai/2022/07/28/nbdev-v2/).

Se ficou curioso sobre como é o código Jupyter notebook para desenvolvimento de software você pode olhar o [código do Ipyannotator](https://github.com/palaimon/ipyannotator/tree/main/nbs).

Post originalmente postado no blog Palaimon: https://blog.palaimon.io/posts/literate-programming-nbdev/