---
layout: post
title: Краткий обзор реализаций Scheme
author: Evgeny Simonenko
date: 2022-05-23 21:48
updating_date: 2022-08-05 20:53
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

| Название                                                   | Компилятор | Интерпретатор | Стандарт | Написано на | Репозиторий                                                     | Число звёзд на GitHub | Последняя версия | Версия в Ubuntu 22.04 LTS | Название пакета в Ubuntu |
|------------------------------------------------------------|:----------:|:-------------:|----------|-------------|-----------------------------------------------------------------|:---------------------:|:----------------:|:-------------------------:|--------------------------|
| [MIT/GNU Scheme](https://www.gnu.org/software/mit-scheme/) | +          | +             | R7RS     | Scheme      |                                                                 |                       | 11.2             | 11.2                      | mit-scheme               |
| [SCM](https://people.csail.mit.edu/jaffer/SCM.html)        | +          | +             | R5RS     | C, Scheme   |                                                                 |                       | 5f3              | 5f3                       | scm                      |
| [Guile](https://www.gnu.org/software/guile/)               | +          | +             | R6RS     | C           |                                                                 |                       | 3.0.8            | 3.0.7                     | guile-3.0                |
| [ChezScheme](https://cisco.github.io/ChezScheme/)          | +          | +             | R6RS     | Scheme, C   | [cisco/chezscheme](https://github.com/cisco/chezscheme)         | 6249                  | 9.5.8            | 9.5.4                     | chezscheme               |
| [Racket](https://racket-lang.org/)                         | -          | +             | R6RS     | Scheme, C   | [racket/racket](https://github.com/racket/racket)               | 4282                  | 8.5              | 8.2                       | racket                   |
| [CHICKEN](https://www.call-cc.org/)                        | +          | -             | R5RS     | Scheme      |                                                                 |                       | 5.3.0            | 5.2.0                     | chicken-bin              |
| [Scheme 48](https://s48.org/)                              | -          | +             | R5RS     | C, Scheme   |                                                                 |                       | 1.9.2            | 1.9.2                     | scheme48                 |
| [Gambit](https://www.gambitscheme.org/)                    | +          | +             | R5RS     | C, Scheme   | [gambit/gambit](https://github.com/gambit/gambit)               | 1070                  | 4.9.4            | 4.9.3                     | gambc                    |
| [Chibi-Scheme](https://synthcode.com/wiki/chibi-scheme)    | -          | +             | R7RS     | Scheme, C   | [ashinn/chibi-scheme](https://github.com/ashinn/chibi-scheme)   | 959                   | 0.10             | 0.9.1                     | chibi-scheme             |
| [Cyclone Scheme](https://justinethier.github.io/cyclone/)  | +          | +             | R7RS     | Scheme, C   | [justinethier/cyclone](https://github.com/justinethier/cyclone) | 723                   | 0.34.0           |                           |                          |
| [Gauche](https://practical-scheme.net/gauche/)             | -          | +             | R7RS     | Scheme, C   | [shirok/Gauche](https://github.com/shirok/Gauche)               | 652                   | 0.9.11           | 0.9.10                    | gauche                   |

## Другие реализации

| Название                                                          | Компилятор | Интерпретатор | Стандарт | Написано на | Репозиторий                                                       | Число звёзд на GitHub | Последняя версия | Версия в Ubuntu 22.04 LTS | Название пакета в Ubuntu |
|-------------------------------------------------------------------|:----------:|:-------------:|----------|-------------|-------------------------------------------------------------------|:---------------------:|:----------------:|:-------------------------:|--------------------------|
| [Stalin](https://engineering.purdue.edu/~qobi/software/)          | +          | -             |          | Scheme, C   |                                                                   |                       | 0.11             | 0.11                      | stalin                   |
| [SISC](http://www.sisc-scheme.org/)                               | -          | +             | R5RS     | Java        |                                                                   |                       | 1.16.6           | 1.16.6                    | sisc                     |
| [Scheme 9 from Empty Space](https://www.t3x.org/s9fes/index.html) | -          | +             | R4RS     | C, Scheme   |                                                                   |                       | 2018.12.05       | 2018.12.05                | scheme9                  |
| Vicare                                                            | +          | -             | R6RS     | Scheme, C   | [marcomaggi/vicare](https://github.com/marcomaggi/vicare)         | 189                   | 0.4.1            |                           |                          |
| [Bigloo](https://www-sop.inria.fr/mimosa/fp/Bigloo/index.html)    | +          | +             | R5RS     | Scheme, C   | [manuel-serrano/bigloo](https://github.com/manuel-serrano/bigloo) | 84                    | 4.4c-4           |                           |                          |
| scheme2c                                                          | +          | +             | R4RS     | C           | [barak/scheme2c](https://github.com/barak/scheme2c)               | 64                    | 2012.10.14       | 2012.10.14                | scheme2c                 |
| [Ikarus](https://sources.debian.org/data/main/i/ikarus/)          | +          | -             | R6RS     | C, Scheme   |                                                                   |                       | 0.0.3            | 0.0.3                     | ikarus                   |
| [Elk](http://sam.zoy.org/elk/)                                    | -          | +             |          | C           |                                                                   |                       | 3.99.8           | 3.99.8                    | elk                      |
| [STklos](https://stklos.net/)                                     |            |               | R7RS     | C           | [egallesio/STklos](https://github.com/egallesio/STklos)           | 46                    | 1.70             |                           |                          |
| SigScheme                                                         | -          | +             | R5RS     | Scheme, C   | [uim/sigscheme](https://github.com/uim/sigscheme)                 | 20                    | 0.9.1            | 0.9.1                     | sigscheme                |
| [TinyScheme](http://tinyscheme.sourceforge.net/home.html)         | -          | +             | R5RS     |             |                                                                   |                       |                  | 1.42                      | tinyscheme               |

## Библиотеки, разное

| Название                                         | Назначение                                                                                        | Стандарт | Написано на | Репозиторий                                                                                 | Число звёзд на GitHub | Последняя версия | Версия в Ubuntu 22.04 LTS | Название пакета в Ubuntu |
|--------------------------------------------------|---------------------------------------------------------------------------------------------------|----------|-------------|---------------------------------------------------------------------------------------------|:---------------------:|:----------------:|:-------------------------:|--------------------------|
| [SLIB](https://people.csail.mit.edu/jaffer/SLIB) | Библиотека                                                                                        |          | Scheme      |                                                                                             |                       | 3b6              | 3b6                       | slib                     |
| [Nanopass Framework](https://nanopass.org/)      | DSL для создания компиляторов                                                                     |          | Scheme      | [nanopass/nanopass-framework-scheme](https://github.com/nanopass/nanopass-framework-scheme) | 417                   | 1.9.2            | 1.9.2                     | r6rs-nanopass-dev        |
| Scheme-to-C                                      | Пример неполного компилятора Scheme, построенного по технологии [Nanopass](https://nanopass.org/) |          | Scheme      | [akeep/scheme-to-c](https://github.com/akeep/scheme-to-c)                                   | 316                   |                  |                           |                          |
| stex                                             | Конвертация кода на Scheme в LaTeX                                                                |          | Scheme      | [dybvig/stex](https://github.com/dybvig/stex)                                               | 82                    | 1.2.2            | 1.2.1                     | stex                     |

## Обновление от 4 августа 2022

* Добавлена информация о реализациях _Cyclone Scheme_, _Vicare_ и _Bigloo_.
* Добавлена информация о примере _Scheme-to-C_.
* Добавлена колонка "Название пакета в Ubuntu":
  часто название пакета не совпадает с названием реализации.
  Кроме того, к основному пакету с компилятором или интерпретатором могут поставляться
  отдельные пакеты с документацией и библиотеками.
* Исправлено форматирование первой таблицы.

(c) Симоненко Евгений, 2022
