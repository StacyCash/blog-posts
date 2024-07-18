---
title: Widgets - How to Make Custom Elements
published: false
description: Custom Elements are a great way of getting your code onto someones site, without them having to install anything. This article will show you how to make your own custom elements.
tags: custom elements, web components, vue, javascript
series: Custom Elements
# cover_image: https://direct_url_to_image.jpg
# Use a ratio of 100:42 for best results.
# published_at: 2024-03-11 15:28 +0000
---

First up... If I am going to talk about widgets then I also have to show my age...

<iframe width="560" height="315" src="https://www.youtube.com/embed/VsiWQ4xm5-Q?si=LwFZNPz10tQL6bE1" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

back in the early 90s lots of beer started to be served with widgets to make them foamier... I'm too young to tell you if it was a good idea or not, but I can tell you that widgets in the web are a great idea!

## So What Is A Widget

Widgets, or more accurately **Custom Elements** are a way of exposing your code to other people's websites without them having to install anything. They are a way of creating reusable components that can be dropped into any website with just a link to your script, and a simple script tag.

For more information about Custom Elements, you can check out the [MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_custom_elements).

In this series we are going to look at how to create custom elements using different frameworks, starting with Vue.js.

## Starting our Vue application

> Full disclosure: I am not a Vue developer, I code in C# for my day job. This post is about how I got the Vue custom elements working for me, if I have done something hideously wrong - please **politely** let me know in the comments. I am always looking to learn.

We need to make a Vue application - but when I tried this using the Vue CLI I found that the scaffolded application was just over the top. So here I am going to start from scratch and hope for the best 😅 (If there is a way of scaffolding an app without all the extra things I don't need, then please let me know!)

In an empty folder, I ran the following commands:

``` ps
git init
mkdir src
mkdir public
npm init -y
npm install -D @vue/compiler-sfc
npm install -D vite
npm install @vue/tsconfig
```
