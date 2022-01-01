---
layout: post
title:  "Lazy horizontal scroll"
date:   2021-10-23 17:09:20 -0300
---

Recently I came across with the following scenario: a management software of workflows that allow the user to dynamic create its kanbans (like the one in the image below). One of the users set its kanban to have 38 columns.

The software was design in a way that every kanban column made a request to the backend, in this scenario 38 new requests were made every time a user access the kanban page. This not only overload the server but also the database.

![Kanban image with five columns. The columsn in the sequence: stories, todo, in progress, testing, done](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/6ui3slceaoxqovpxm1uo.jpg)

First we needed to decrease the number of requests, limiting the requests to the columns that were visible to the user. After that we had to make sure that if the user scrolls to the end of the page at once, the columns would not request the data unless they were visible for a certain amount of time.

## Limiting loading to visible cards

Javascript offers an API called [IntersectionObserver](https://developer.mozilla.org/en-US/docs/Web/API/IntersectionObserver) that allow us to watch HTML elements and check its visibility on screen. The code below shows its most basic operation.

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

The function `onIntersection` is responsable for the logic that will be applied to the visible elements, it takes a list of elements and checks that if they're visible  (` element.isIntersecting `) then something will be done, in which case a console message is displayed.

The ` IntersectionObserver ` API call is made and set to the ` observer ` variable. The ` observer ` object will then be able to observe elements in the HTML and execute logic only when they are visible on the user's screen. In my case, for the giant kanban, this was enough to limit the 38 requests as the page loaded to just 5, but if the user scrolled the page to its end at once several requests would be made (the other 33 requests).

## Load only after a certain time of the visible element on the page

The ` IntersectionObserver ` API has a [version 2](https://web.dev/intersectionobserver-v2/) that allows capturing how long a certain HTML element was visible on the screen and this would easily solve the element loading problem HTML only after a certain amount of time. However, version 2 still doesn't have its implementations compatible with most browsers.

In my specific case I was using a parent component that rendered the 38 child elements and I couldn't check when those 38 child elements were finished rendering to observe them with the ` InsertersectionObserver `, so control how long each element was visible in the screen got a little more complicated.

Each of the 38 child elements knew when they were rendering themselves, so you could use the ` IntersectionObserver ` internally on each of them. Using the ` setTimeout ` function of the javascript you can observe the element after a certain time specified in milliseconds.

We have 38 elements, but most are not visible on the screen and become visible when scrolling, with the ` setTimeout ` delay this action still takes some time to be executed. During scrolling, when the element visible on the screen has not yet triggered the specified `setTimeout` and the user has already scrolled to the next element, it is possible to remove the timeout of the previous element from the stack and then load only the next element. The following code shows this strategy.

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

When the component is loaded into the page it already starts looking at itself using the ` loadColumn ` function. Such function removes the previous timeouts (which were not triggered) from the execution stack and adds a new timeout which after 750 milliseconds does something and removes the observation to not redo the same logic if the element becomes visible again.

In my case the logic was the request to the server so I only needed to load the data once and then ignore it if the element was visible again on the page.

> Did you find the above code syntax strange? This javascript microframework is called [AlpineJS](https://alpinejs.dev/) and that's what I used to develop the complete solution. 

A simpler POC, without the request to the server, can be seen below. After being visible on your screen the white squares will turn black indicating the request to the server.

{% include codepen.html hash="PoKqGPm" title="Carregamento lento com scroll horizontal" %}

If you are interested in seeing a solution with vanilla javascript [this was my reference](https://www.codeguage.com/tutorials/lazy-loading/intersection-observer).
 