---
layout: post
title: "Deploy Your ipynb/rmarkdown with GitHub Pages and Quarto"
date:  2026-03-24 17:00:00 -5
excerpt: "Amazing tech! share your project with others"
mathjax: true
math: true
hidden: false
categories: [Quarto]
tags: [Quarto, GitHub Pages, notebook, python, R]
---

I created two websites by quarto: some R language notes at [R Note for Statistics Learning and Computing](https://r.danieldata.com/), and some projects will be posted at [Daniel Cheung's Projects](https://project.danieldata.com/)


You can download it at [quarto.org](https://quarto.org/docs/download/) and then install. Quarto can help you deploy. You can also download Position as an IDE to use together with quarto.

In your project: use either command to preview or publish

```
quarto preview
```


```
quarto publish gh-pages
```

If you have document that have a lot of computing, emember attach this in your qmd file to avoid execute every time when you don't modify it:

```
---
execute:
  freeze: true
---
```

The last thing is, always remember to clean your memory. Quarto has very terrible design for garbage collection, especially you frequently preview the document.