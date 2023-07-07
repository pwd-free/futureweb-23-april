---
title: "Basic Maths Operations"
date: 2023-07-07T21:35:49+10:00
draft: false
categories: [hugo]
tags: [maths, operations]
images: []
description: A guide to using Hugo to perform basic maths operations
---
Hugo can perform the following BASIC math operations. (this post does not focus on advanced math operations)

## Addition

```go-html-template
{{ add 1 2 }} -> 2
{{ add 1 2 3 4 }} -> 10
{{ add 1 1.1 }} -> 2.1 (result is a float)
```
## Subtraction

```go-html-template
{{ sub 2 1 }} -> 1 or
{{ sub 3 2 1 }} -> 0
{{ sub 2 1.1 }} -> 0.9 (result is a float)
```

## Multiply

```go-html-template
{{ mul 2 2 }} -> 4
{{ mul 2 2 2 }} -> 8
{{ mul 10 1.1 }} -> 11 (result is float)
```

## Divide

```go-html-template
{{ div 4 2 }} -> 2
{{ div 8 2 2 }} -> 2
{{ div 7 3.5 }} -> 2 (result is float)
{{ div 5 2 }} -> 2 (result is integer)
{{ div 5 2.0 }} -> 2.5 (result is float)
```

You must be careful when dividing. If you want the result to be an float/decimal, one of the numbers divided must be a float.

If working with variables you can use the `float` function to convert an integer to a float e.g.

```go-html-template
{{ $first := 5 }}
{{ $second := 2 }}
{{ div $first (float $second) }} -> 2.5
```





