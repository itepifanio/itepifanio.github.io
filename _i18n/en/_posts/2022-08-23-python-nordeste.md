---
layout: post
title: "Python Nordeste 2022 Recap"
date: 2022-09-09 13:09:20 -0300
---

From August 26th to August 28th 2022 I attended the Python Nordeste,
the biggest Python event in northeast of Brazil. It was the return of in-person
conferences in the country. Focused on the communities, the event slogan was
"People > Technology".

<img style="width: 60%; margin-left: auto; margin-right: auto; display: block;"
     alt="Python Nordeste entry. A big and light panel with the title 'PyNE 2022' and a pacman game design"
     src="/assets/python-nordeste-entrance.jpg">
<p style="text-align: center">
Event entry. Picture by <a href="https://www.linkedin.com/in/raphaelfontes/" target="_blank">Rafael Fontes</a>
</p>

With a good mix of technical talks and community discussions the event happened in 
[Aracaju](https://goo.gl/maps/2hvCA44yKiJPBdDv9), 
the city with the "most beautiful beachfront" 
(a controversial topic since most of the principal cities are coastal).

I gave a talk that showed how [Ipyannotator](https://github.com/palaimon/ipyannotator) 
can be used for traffic annotations and presented the results 
of our R&D project CityCount.

Here's a quick overview of some talks I attended:

- Community, diversity and inclusion: challenges and strategy
- Algorithmic biases and how to combat them
- How AI can impact the population's health? 
- Using Ipyannotator for traffic annotation

## Community, diversity and inclusion: challenges and strategy

Brazil has a very diverse population that is not completely represented 
in the technological field. Multiple communities were built to create safe-spaces 
and encourage underrepresented people to move into the area. This 
talk was an open discussion about strategies and challenges to use technology 
as a tool for social transformation.

> Technology can be a tool for social transformation

The discussion was conducted by four members of the [Pyladies Brasil](http://brasil.pyladies.com/), 
a group that encourages, trains and helps women to enter and grow on technology. 
The group [Afro Python](https://afropython.org/), that works on increasing the representation 
of black people within the technology area, was also represented in the discussion.

The pandemic had a huge impact on local meetings and the members talked about their 
experience in managing the community, engaging people and dealing with 
[zoom fatigue](https://en.wikipedia.org/wiki/Zoom_fatigue). 
The return of in-person activities also brought new demands like recording the talks,
sync and async activities and sanitary measures against COVID.

Brazil is one of the most unequal countries in the world, part of the discussion was 
focused on how technology can provide social transformation for underrepresented groups. 
The whole Python Nordeste organization focused on diversity and inclusion by offering tickets 
to communities and non-governmental organizations, centered the attention on the LGBTQIA+ 
community and on how to provide a safe and welcoming environment for everyone. 

## Algorithmic biases and how to combat them

Algorithms can discriminate. Racism and sexism are some of the bias that can exist in AI algorithms. 
[Luiz Fernando](https://www.linkedin.com/in/luiz-fernando-de-lima/) presented his master's research 
about how to build fair machine learning models.

> Algorithms can discriminate. How to combat them?

Fairness algorithms try to remove or mitigate biases skewed towards a particular group of people. 
There are multiple methodologies to make algorithms more fair, from the most naive approaches like 
omitting variables from the model to most advanced approaches like fairness by design.

Luiz's research was focused on fairness by design strategies that can be applied to change 
machine learning models in a way that guarantees the expected fairness.

AI development is a very interdisciplinary field but few companies have interdisciplinary teams. 
Beyond technical strategies a diverse team helps to instigate social and ethical debates about how a model need to be adapted.

## How AI can impact the population's health? 

Fernanda Wanderley talked about how AI can be applied in healthcare solutions. She presented a computer vision
application that reads an x-ray and detects lung damage, increasing the priority in the emergency 
service.

> The AI isn't developed to replace doctors but to assistant healthcare workers

The application introduced by her was using doctors as annotators for medical images. The doctors were 
annotating the regions where they detect pleural effusion. The efforts of the annotators and the data science team 
enabled reducing the service time and increasing the agility to attend risk cases.

## Using Ipyannotator for traffic annotation

[Ipyannotator](https://github.com/palaimon/ipyannotator) is an annotation framework design which is customizable 
and runs in the [Jupyter notebook environment](https://jupyter.org/). The tool allows users to create their own 
datasets, improve existing ones or explore the data. 

Machine learning applications combine code and data to generate results. For many years, the industry has 
focused on the code aspect and was using data as a static asset. Now, the industry is moving to a more 
[data-centric AI](https://datacentricai.org/)
approach.

Ipyannotator is one of the tools that can be very helpful for data science teams to understand, create and improve 
their data. In this presentation I talked about the technologies used to develop Ipyannotator and how it was used in the 
[CityCount project](https://www.bmvi.de/SharedDocs/DE/Artikel/DG/mfund-projekte/citycount.html), which developed a cost-effective, mobile
AI-based counting device that provides data and insights for traffic planning.

## Conclusion

<img style="width: 20%; float: left; margin-right: 1em"
     alt="Python Nordeste logo. A 'Caju' (fruit) with a snake around"
     src="/assets/pyne-logo.png">
<p style="text-align: center">
Python Nordeste logo
</p>

The return of in-person conferences in Brazil couldn't be done in a better way than 
Python Nordeste did. It was an inclusive and well-rounded event. The organization really did a good job.
Any pythonista or person interested in technology would be happy to attend Python Nordeste.
