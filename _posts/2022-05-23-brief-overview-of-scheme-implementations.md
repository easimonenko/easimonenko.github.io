---
layout: post
title: Краткий обзор реализаций Scheme
author: Evgeny Simonenko
date: 2022-05-23 21:48
updating_date: 2025-06-11 21:12
category: Review
tags: [Scheme, Functional Programming]
---

Наверное все, кто изучал информатику и вычислительную технику в университете, так или иначе,
в курсе функционального программирования, например, столкнулся с _Scheme_ -- языком
функционального программирования, произошедшем от _Lisp_, и известным как язык со скобками,
то есть где всё является так называемыми _S-выражениями_. Скорее всего это был _MIT/GNU Scheme_
или _Racket_. Но на самом деле реализаций Scheme большое количество. В этой статье собраны в
таблицы различные реализации Scheme, указаны поддерживаемые ими версии языка, является ли
реализация компилятором или интерпретатором, и другая информация.

<!-- end-of-lead -->

## Самые значимые реализации

| Название                                                   | Компилятор | Интерпретатор | Стандарт | Написано на | Лицензия                               | Репозиторий                                                                                                    | Число звёзд на GitHub | Последняя версия | Название пакета в Ubuntu | Версия в Ubuntu 24.04 LTS | Название пакета в Nix | Версия в Nix | Название пакета в Guix | Версия в Guix |
|------------------------------------------------------------|:----------:|:-------------:|----------|-------------|----------------------------------------|----------------------------------------------------------------------------------------------------------------|:---------------------:|:----------------:|--------------------------|:-------------------------:|-----------------------|--------------|------------------------|---------------|
| [MIT/GNU Scheme](https://www.gnu.org/software/mit-scheme/) | +          | +             | R7RS     | Scheme      | GNU General Public License v2.0        | [https://cgit.git.savannah.gnu.org/cgit/mit-scheme.git](https://cgit.git.savannah.gnu.org/cgit/mit-scheme.git) |                       | 12.1             | mit-scheme               | 12.1                      | mitscheme             | 12.1         | mit-scheme             | 11.2          |
| [SCM](https://people.csail.mit.edu/jaffer/SCM.html)        | +          | +             | R5RS     | C, Scheme   | GNU General Public License v3.0        |                                                                                                                |                       | 5f4              | scm                      | --                        |                       |              | scm                    | 5f4           |
| [Guile](https://www.gnu.org/software/guile/)               | +          | +             | R6RS     | C           | GNU General Public License v3.0        |                                                                                                                |                       | 3.0.10           | guile-3.0                | 3.0.9                     | guile                 | 3.0.9        | guile                  | 3.0.9         |
| [Chez Scheme](https://cisco.github.io/ChezScheme/)         | +          | +             | R6RS     | Scheme, C   | Apache License 2.0                     | [cisco/chezscheme](https://github.com/cisco/chezscheme)                                                        | 7109                  | 10.2.0           | chezscheme               | 9.5.8                     | chez                  | 9.6.4        | chez-scheme            | 10.2.0        |
| [Racket](https://racket-lang.org/)                         | -          | +             | R6RS     | Scheme, C   | MIT License                            | [racket/racket](https://github.com/racket/racket)                                                              | 4970                  | 8.17             | racket                   | 8.10                      | racket                | 8.10         | racket                 | 8.17          |
| [CHICKEN](https://www.call-cc.org/)                        | +          | -             | R5RS     | Scheme      | BSD License (3-Clause)                 | [https://code.call-cc.org/git/chicken-core.git/](https://code.call-cc.org/git/chicken-core.git/)               |                       | 5.4.0            | chicken-bin              | 5.3.0                     | chicken               | 5.3.0        | chicken                | 5.4.0         |
| [Scheme 48](https://s48.org/)                              | -          | +             | R5RS     | C, Scheme   | BSD License (3-Clause)                 |                                                                                                                |                       | 1.9.3            | scheme48                 | 1.9.2                     | scheme48              | 1.9.2        | scheme48               | 1.9.2         |
| [Gambit](https://www.gambitscheme.org/)                    | +          | +             | R5RS     | C, Scheme   | Apache License 2.0                     | [gambit/gambit](https://github.com/gambit/gambit)                                                              | 1375                  | 4.9.5            | gambc                    | 4.9.3                     | gambit                | 4.9.5        | gambit-c               | 4.9.5         |
| [Chibi-Scheme](https://synthcode.com/wiki/chibi-scheme)    | -          | +             | R7RS     | Scheme, C   | BSD License (3-Clause)                 | [ashinn/chibi-scheme](https://github.com/ashinn/chibi-scheme)                                                  | 1145                  | 0.10             | chibi-scheme             | 0.9.1                     | chibi                 | 0.10         | chibi-scheme           | 0.10          |
| [Gerbil](https://cons.io/)                                 | +          | +             | R7RS     | Scheme      | GNU Lesser General Public License v2.1 | [vyzo/gerbil](https://github.com/vyzo/gerbil)                                                                  | 1047                  | 0.18.1           |                          |                           | gerbil                | 0.18         | gerbil                 | 0.17.0        |
| [Cyclone Scheme](https://justinethier.github.io/cyclone/)  | +          | +             | R7RS     | Scheme, C   | MIT License                            | [justinethier/cyclone](https://github.com/justinethier/cyclone)                                                | 788                   | 0.35.0           |                          |                           | cycle-scheme          | 0.34.0       |                        |               |
| [Gauche](https://practical-scheme.net/gauche/)             | -          | +             | R7RS     | Scheme, C   | BSD License (3-Clause)                 | [shirok/Gauche](https://github.com/shirok/Gauche)                                                              | 755                   | 0.9.13           | gauche                   | 0.9.10                    | gauche                | 0.9.10       | gauche                 | 0.9.12        |
| [BiwaScheme](https://www.biwascheme.org/)                  | -          | +             | R7RS     | JavaScript  | MIT License                            | [biwascheme/biwascheme](https://github.com/biwascheme/biwascheme)                                              | 713                   | 0.8.0            |                          |                           |                       |              |                        |               |

## Другие реализации

| Название                                                          | Компилятор | Интерпретатор | Стандарт | Написано на    | Лицензия                           | Репозиторий                                                                         | Число звёзд на GitHub | Последняя версия | Версия в Ubuntu 22.04 LTS | Название пакета в Ubuntu | Версия в Nix | Название пакета в Nix     | Версия в Guix | Название пакета в Guix |
|-------------------------------------------------------------------|:----------:|:-------------:|----------|----------------|------------------------------------|-------------------------------------------------------------------------------------|:---------------------:|:----------------:|:-------------------------:|--------------------------|--------------|---------------------------|---------------|------------------------|
| [Stalin](https://engineering.purdue.edu/~qobi/software/)          | +          | -             |          | Scheme, C      | GNU General Public License v2.0    |                                                                                     |                       | 0.11             | 0.11                      | stalin                   | 0.11         | stalin                    | 0.11          | stalin                 |
| [SISC](http://www.sisc-scheme.org/)                               | -          | +             | R5RS     | Java           | Mozilla Public License Version 1.1 |                                                                                     |                       | 1.16.6           | 1.16.6                    | sisc                     |              |                           |               |                        |
| [Scheme 9 from Empty Space](https://www.t3x.org/s9fes/index.html) | -          | +             | R4RS     | C, Scheme      | Public Domain                      |                                                                                     |                       | 2018.12.05       | 2018.12.05                | scheme9                  |              |                           |               |                        |
| Picrin                                                            | -          | +             | R7RS     | Scheme, C      | MIT License                        | [picrin-scheme/picrin](https://github.com/picrin-scheme/picrin)                     | 409                   | 0.1              |                           |                          |              |                           |               |                        |
| Ribbit                                                            | +          | -             | R4RS     | Scheme         | BSD License (3-Clause)             | [udem-dlteam/ribbit](https://github.com/udem-dlteam/ribbit)                         | 409                   |                  |                           |                          |              |                           |               |                        |
| Swift LispKit                                                     | +          | -             | R7RS     | Swift, Scheme  | Apache License 2.0                 | [objecthub/swift-lispkit](https://github.com/objecthub/swift-lispkit)               | 362                   |                  |                           |                          |              |                           |               |                        |
| IronScheme                                                        |            |               | R6RS     | C#, Scheme     | BSD License (3-Clause)             | [IronScheme/IronScheme](https://github.com/IronScheme/IronScheme)                   | 356                   |                  |                           |                          |              |                           |               |                        |
| Calysto Scheme                                                    | -          | +             |          | Scheme, Python | BSD License (3-Clause)             | [Calysto/calysto_scheme](https://github.com/Calysto/calysto_scheme)                 | 256                   | 1.4.8            |                           |                          | 1.0.6        | python311Packages.calysto |               |                        |
| [Irken](https://nightmare.com/rushing/irken.html)                 | +          | -             |          | Scheme         | BSD License (2-Clause)             | [samrushing/irken-compiler](https://github.com/samrushing/irken-compiler)           | 207                   |                  |                           |                          |              |                           |               |                        |
| [Larceny Scheme](http://www.larcenists.org/)                      | +          | +             | R7RS     | Scheme, C      |                                    | [larcenists/larceny](https://github.com/larcenists/larceny)                         | 198                   | 1.3              |                           |                          |              |                           |               |                        |
| Vicare                                                            | +          | -             | R6RS     | Scheme, C      | GNU General Public License v3.0    | [marcomaggi/vicare](https://github.com/marcomaggi/vicare)                           | 196                   | 0.4.1            |                           |                          |              |                           |               |                        |
| Picobit                                                           | +          | +             |          | C, Racket      | GNU General Public License v3.0    | [stamourv/picobit](https://github.com/stamourv/picobit)                             | 177                   |                  |                           |                          |              |                           |               |                        |
| [Mosh](https://mosh.monaos.org/files/doc/text/About-txt.html)     |            |               | R6RS     | Rust, Scheme   | BSD License (2-Clause)             | [higepon/mosh](https://github.com/higepon/mosh)                                     | 172                   | 0.2.9            |                           |                          |              |                           |               |                        |
| lisp-interpreter                                                  | -          | +             | R5RS     | Scheme, C      | ISC License                        | [justinmeiners/lisp-interpreter](https://github.com/justinmeiners/lisp-interpreter) | 130                   |                  |                           |                          |              |                           |               |                        |
| [Bigloo](https://www-sop.inria.fr/mimosa/fp/Bigloo/index.html)    | +          | +             | R5RS     | Scheme, C      | GNU General Public License v2.0    | [manuel-serrano/bigloo](https://github.com/manuel-serrano/bigloo)                   | 120                   | 4.5a-1           |                           |                          | 4.4b         | bigloo                    | 4.3g          | bigloo                 |
| scheme2c                                                          | +          | +             | R4RS     | C              |                                    | [barak/scheme2c](https://github.com/barak/scheme2c)                                 | 76                    | 2012.10.14       | 2012.10.14                | scheme2c                 |              |                           |               |                        |
| [Ikarus](https://sources.debian.org/data/main/i/ikarus/)          | +          | -             | R6RS     | C, Scheme      | GNU General Public License v3.0    |                                                                                     |                       | 0.0.3            | 0.0.3                     | ikarus                   |              |                           |               |                        |
| [Elk](http://sam.zoy.org/elk/)                                    | -          | +             |          | C              |                                    |                                                                                     |                       | 3.99.8           | 3.99.8                    | elk                      |              |                           |               |                        |
| [STklos](https://stklos.net/)                                     |            |               | R7RS     | C, Scheme      | GNU General Public License v2.0    | [egallesio/STklos](https://github.com/egallesio/STklos)                             | 64                    | 2.0              |                           |                          |              |                           | 1.70          | stklos                 |
| [Kawa](https://www.gnu.org/software/kawa/)                        | +          | +             |          | Java, Scheme   | MIT License                        | [kashell/Kawa](https://gitlab.com/kashell/Kawa)                                     | 51 (GitLab)           | 3.1.1            |                           |                          |              |                           | 3.1.1         | kawa                   |
| Ypsilon                                                           |            |               | R7RS     | Scheme, C++    | BSD License (2-Clause)             | [fujita-y/ypsilon](https://github.com/fujita-y/ypsilon)                             | 47                    | 2.0.8            |                           |                          |              |                           |               |                        |
| Sagittarius Scheme                                                |            |               | R7RS     | Scheme, C      | BSD License (2-Clause)             | [ktakashi/sagittarius-scheme](https://github.com/ktakashi/sagittarius-scheme)       | 42                    | 0.9.10           |                           |                          | 0.9.10       | sagittarius-scheme        |               |                        |
| SigScheme                                                         | -          | +             | R5RS     | Scheme, C      | BSD License (3-Clause)             | [uim/sigscheme](https://github.com/uim/sigscheme)                                   | 23                    | 0.9.1            | 0.9.1                     | sigscheme                |              |                           |               |                        |
| [TinyScheme](http://tinyscheme.sourceforge.net/home.html)         | -          | +             | R5RS     |                |                                    |                                                                                     |                       |                  | 1.42                      | tinyscheme               | 1.42         | tinyscheme                | 1.42          | tinyscheme             |
| [RScheme](https://www.rscheme.org/rs/)                            | +          |               |          | Scheme, C      |                                    |                                                                                     |                       | 0.7.3.4          |                           |                          |              |                           |               |                        |

## Библиотеки, разное

| Название                                                            | Назначение                                                                                        | Стандарт | Написано на   | Лицензия                               | Репозиторий                                                                                 | Число звёзд на GitHub | Последняя версия | Версия в Ubuntu 22.04 LTS | Название пакета в Ubuntu |
|---------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|----------|---------------|----------------------------------------|---------------------------------------------------------------------------------------------|:---------------------:|:----------------:|:-------------------------:|--------------------------|
| [SLIB](https://people.csail.mit.edu/jaffer/SLIB)                    | Библиотека                                                                                        |          | Scheme        | Public Domain                          |                                                                                             |                       | 3b7              | 3b6                       | slib                     |
| [](GNU TeXmacs)(https://www.texmacs.org/tmweb/home/welcome.en.html) | Wysiwyg редактор TeX.                                                                             | R6RS     |               | GNU General Public License v3.0        |                                                                                             |                       | 2.1.2            |                           |                          |
| [Nanopass Framework](https://nanopass.org/)                         | DSL для создания компиляторов                                                                     |          | Scheme        | MIT License                            | [nanopass/nanopass-framework-scheme](https://github.com/nanopass/nanopass-framework-scheme) | 452                   | 1.9.2            | 1.9.2                     | r6rs-nanopass-dev        |
| [Scsh](https://scsh.net/)                                           | Оболочка (Shell) на базе Scheme 48                                                                | R5RS     | Scheme, C     | BSD License (3-Clause)                 | [scheme/scsh](https://github.com/scheme/scsh)                                               | 356                   | 0.6.7            |                           |                          |
| Scheme-to-C                                                         | Пример неполного компилятора Scheme, построенного по технологии [Nanopass](https://nanopass.org/) |          | Scheme        | MIT License                            | [akeep/scheme-to-c](https://github.com/akeep/scheme-to-c)                                   | 331                   |                  |                           |                          |
| zkeme80                                                             | Ассемблер и операционная система для Z80.                                                         | R6RS     | Scheme, Forth | MIT License                            | [siraben/zkeme80](https://github.com/siraben/zkeme80)                                       | 222                   |                  |                           |                          |
| chez-exe                                                            | Утилита для создания исполняемого файла путём сключения ChezScheme.                               |          | Scheme, C     | ISC License                            | [gwatt/chez-exe](https://github.com/gwatt/chez-exe)                                         | 173                   |                  |                           |                          |
| Raven                                                               | Менеджер пакетов для ChezScheme.                                                                  |          | Scheme        | MIT License                            | [guenchi/Raven](https://github.com/guenchi/Raven)                                           | 118                   | 0.3.6            |                           |                          |
| stex                                                                | Конвертация кода на Scheme в LaTeX                                                                |          | Scheme        | MIT License                            | [dybvig/stex](https://github.com/dybvig/stex)                                               | 84                    | 1.2.2            | 1.2.1                     | stex                     |
| Gerbil Utilities                                                    | Коллекция дополнительных модулей для Gerbil                                                       | R7RS     | Scheme        | GNU Lesser General Public License v2.1 | [fare/gerbil-utils](https://github.com/fare/gerbil-utils)                                   | 41                    | 0.2              |                           |                          |

## Обновления

### Обновление от 4 августа 2022

* Добавлена информация о реализациях _Cyclone Scheme_, _Vicare_ и _Bigloo_.
* Добавлена информация о примере _Scheme-to-C_.
* Добавлена колонка "Название пакета в Ubuntu":
  часто название пакета не совпадает с названием реализации.
  Кроме того, к основному пакету с компилятором или интерпретатором могут поставляться
  отдельные пакеты с документацией и библиотеками.
* Исправлено форматирование первой таблицы.

### Обновление от 14 ноября 2022

* Добавлена информация о реализациях _Gerbil_ и _BiwaScheme_.
* Добавлена колонка "Лицензия".
* Обновлены число звёзд и последние версии.

### Обновление от 19 ноября 2022

* Добавлена информация о реализациях _Kawa_, _Sagittarius_, _Larceny_, _Picobit_.

### Обновление от 23 ноября 2022

* Добавлена информация об оболочке _Scsh_.

### Обновление от 7 мая 2023

* Обновлена информация о версиях. Вышли новые версии MIT/GNU Scheme, Guile,
  ChezScheme, Racket, BiwaScheme, SLIB.
* Обновлена информация о числе звёзд на GitHub. У всех их число выросло, только
  у Bigloo не изменилось, а у Sagittarius даже на одну снизилось.  Gauche обошел
  BiwaScheme (но это не принципиально, т.к. у них разное назначение).
* Добавлена информация о реализации RScheme.
* Добавлена колонка "Лицензия" в таблицу "Библиотеки, разное".

### Обновление от 6 января 2024

* Пожалуй самое значимое изменение -- выход версии 2.0 STklos, в которой осуществлен переход
  на стандарт R7RS и в которой добаленго большое количество стандартных библиотек.
* Добавлена информация о реализациях Mosh, Ypsilon.
* Добавлены колонки о версиях и названиях пакетов в Nix и Guix.
* Обновлена информация о версиях. Вышли новые версии ChezScheme, Racket, Gambit, Gerbil, Sagittarius.
* Обновлена информация о числе звёзд на GitHub. У всех их число выросло. Larceny обошел Vicare.
* Сайт SISC оказался недоступен.
* Репозиторий Vicare заархивирован.

### Обновление от 9 января 2024

* Добавлена информация о реализациях: Picrin, Ribbit, Swift LispKit, IronScheme, Calysto, Irken,
  lisp-interpreter.
* Добавлена информация о проектах:  GNU TeXmacs, zkeme80, chez-exe, Raven.

### Обновление от 11 июня 2025

* Обновлена информация о версиях.

(c) Симоненко Евгений, 2022, 2023, 2024, 2025
