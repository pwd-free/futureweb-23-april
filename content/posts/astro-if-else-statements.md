---
author: Sean Emerson
title: "Astro if...else statements"
description: "Using iff..else statements within a .astro file isnt so straight forward. This post will show you how you can get around thsi limitation and easily use if...else statements with a jsx style hack"
categories: ["Astro"]
date: 2022-02-18
draft: false
tags: [conditional, if, else]
---

While conditional ternary operators are convienient and supported in astro and react, there are times where you can get more readable code by using if..else statements. 

if..else statements aren't supported in astro and react {as inline js/ts}, so we need to wrap them in an anonymous function and return values for each condition.

Here's an example:

```astro
---
const value = 10
---
<h1>if..else statements in astro</h1>

{ 
  ()=> {
    if (value > 5) {
      const result = value - 9
      return(`The new value is ${result}`)
    } else {
      return('The value was too low.. not processing')
    }
  }
}
```
