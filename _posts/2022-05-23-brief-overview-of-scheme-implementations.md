---
layout: post
title: Краткий обзор реализаций Scheme
author: Evgeny Simonenko
date: 2022-05-23 21:48
category: Review
tags: [Scheme, Functional Programming]
---

Наверное все, кто изучал информатику и вычислительную технику в университете, так или иначе,
в курсе функционального программирования, например, столкнулся с _Scheme_ -- языком
функционального программирования, произошедшем от _Lisp_, и известным как язык со скобками,
то есть где всё является так называемыми _S-выражениями_. Скорее всего это был _MIT/GNU Scheme_
или _Racket_. Но на самом деле реализаций Scheme великое множество. В этой статье собраны в
таблицы различные реализации Scheme, указаны поддерживаемые ими версии языка, является ли
реализация компилятором или интерпретатором, и другая информация.

<!-- end-of-lead -->

## Самые значимые реализации

| Название                                                   | Компилятор | Интерпретатор | Стандарт | Написано на | Репозиторий                                                   | Число звёзд на GitHub | Последняя версия | Версия в Ubuntu 22.04 LTS |
|------------------------------------------------------------|------------|---------------|----------|-------------|---------------------------------------------------------------|-----------------------|------------------|---------------------------|
| [MIT/GNU Scheme](https://www.gnu.org/software/mit-scheme/) | +          | +             | R7RS     | Scheme      |                                                               |                       | 11.2             | 11.2                      |
| [SCM](https://people.csail.mit.edu/jaffer/SCM.html)        | +          | +             | R5RS     | C, Scheme   |                                                               |                       | 5f3              | 5f3                       |
| [Guile](https://www.gnu.org/software/guile/)               | +          | +             | R6RS     | C           |                                                               |                       | 3.0.8            | 3.0.7                     |
| [ChezScheme](https://cisco.github.io/ChezScheme/)          | +          | +             | R6RS     | Scheme, C   | [cisco/chezscheme](https://github.com/cisco/chezscheme)       | 6249                  | 9.5.8            | 9.5.4                     |
| [Racket](https://racket-lang.org/)                         | -          | +             | R6RS     | Scheme, C   | [racket/racket](https://github.com/racket/racket)             | 4282                  | 8.5              | 8.2                       |
| [CHICKEN](https://www.call-cc.org/)                        | +          | -             | R5RS     | Scheme      |                                                               |                       | 5.3.0            | 5.2.0                     |
| [Scheme 48](https://s48.org/)                              | -          | +             | R5RS     | C, Scheme   |                                                               |                       | 1.9.2            | 1.9.2                     |
| [Gambit](https://www.gambitscheme.org/)                    | +          | +             | R5RS     | C, Scheme   | [gambit/gambit](https://github.com/gambit/gambit)             | 1070                  | 4.9.4            | 4.9.3                     |
| [Chibi-Scheme](https://synthcode.com/wiki/chibi-scheme)    | -          | +             | R7RS     | Scheme, C   | [ashinn/chibi-scheme](https://github.com/ashinn/chibi-scheme) | 959                   | 0.10             | 0.9.1                     |
| [Gauche](https://practical-scheme.net/gauche/)             | -          | +             | R7RS     | Scheme, C   | [shirok/Gauche](https://github.com/shirok/Gauche)             | 652                   | 0.9.11           | 0.9.10                    |

## Другие реализации

| Название                                                          | Компилятор | Интерпретатор | Стандарт | Написано на | Репозиторий                                             | Число звёзд на GitHub | Последняя версия | Версия в Ubuntu 22.04 LTS |
|-------------------------------------------------------------------|:----------:|:-------------:|----------|-------------|---------------------------------------------------------|:---------------------:|:----------------:|:-------------------------:|
| [Stalin](https://engineering.purdue.edu/~qobi/software/)          | +          | -             |          | Scheme, C   |                                                         |                       | 0.11             | 0.11                      |
| [SISC](http://www.sisc-scheme.org/)                               | -          | +             | R5RS     | Java        |                                                         |                       | 1.16.6           | 1.16.6                    |
| [Scheme 9 from Empty Space](https://www.t3x.org/s9fes/index.html) | -          | +             | R4RS     | C, Scheme   |                                                         |                       | 2018.12.05       | 2018.12.05                |
| scheme2c                                                          | +          | +             | R4RS     | C           | [barak/scheme2c](https://github.com/barak/scheme2c)     | 64                    | 2012.10.14       | 2012.10.14                |
| [Ikarus](https://sources.debian.org/data/main/i/ikarus/)          | +          | -             | R6RS     | C, Scheme   |                                                         |                       | 0.0.3            | 0.0.3                     |
| [Elk](http://sam.zoy.org/elk/)                                    | -          | +             |          | C           |                                                         |                       | 3.99.8           | 3.99.8                    |
| [STklos](https://stklos.net/)                                     |            |               | R7RS     | C           | [egallesio/STklos](https://github.com/egallesio/STklos) | 46                    | 1.70             |                           |
| SigScheme                                                         | -          | +             | R5RS     | Scheme, C   | [uim/sigscheme](https://github.com/uim/sigscheme)       | 20                    | 0.9.1            | 0.9.1                     |
| [TinyScheme](http://tinyscheme.sourceforge.net/home.html)         | -          | +             | R5RS     |             |                                                         |                       |                  | 1.42                      |

## Библиотеки, разное

| Название                                         | Назначение                         | Стандарт | Написано на | Репозиторий                                                                                 | Число звёзд на GitHub | Последняя версия | Версия в Ubuntu 22.04 LTS |
|--------------------------------------------------|------------------------------------|----------|-------------|---------------------------------------------------------------------------------------------|:---------------------:|:----------------:|:-------------------------:|
| [SLIB](https://people.csail.mit.edu/jaffer/SLIB) | Библиотека                         |          | Scheme      |                                                                                             |                       | 3b6              | 3b6                       |
| [nanopass](https://nanopass.org/)                | DSL для создания компиляторов      |          | Scheme      | [nanopass/nanopass-framework-scheme](https://github.com/nanopass/nanopass-framework-scheme) | 417                   | 1.9.2            | 1.9.2                     |
| stex                                             | Конвертация кода на Scheme в LaTeX |          | Scheme      | [dybvig/stex](https://github.com/dybvig/stex)                                               | 82                    | 1.2.2            | 1.2.1                     |

(c) Симоненко Евгений, 2022
