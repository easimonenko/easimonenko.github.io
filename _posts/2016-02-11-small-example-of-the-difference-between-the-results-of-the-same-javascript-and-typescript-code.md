---
layout: post
title: Маленький пример различия результатов одного и того же кода на JavaScript и TypeScript
author: Evgeny Simonenko
email: easimonenko@gmail.com
date: 2016-02-11
category: Tutorial
tags: [JavaScript, TypeScript, Programming Languages]
---

Без лишних слов маленький пример различия результов одного и того же кода
на JavaScript и TypeScript.

``` javascript
const a = [1, 2, 3, 4, 5];

var s = 0;
for (var v in a) {
  s += v;
}
console.log(s);
```

JavaScript выводит (WTF? Неожиданно? Для специалиста JavaScript нет...):

```
001234
```

TypeScript даже не компилируется (и это хорошо!):

```
sample.ts(5,3): error TS2322: Type 'string' is not assignable to type 'number'.
```

<!-- end-of-lead -->

(c) Симоненко Евгений, 2016
