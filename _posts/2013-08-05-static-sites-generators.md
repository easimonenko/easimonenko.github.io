---
layout: post
title: Генераторы статических сайтов
author: Evgeny Simonenko
email: easimonenko@gmail.com
date: 2013-08-05
category: Tutorial
tags: [Static Site Generators, Web Development]
---

В этой заметке даётся краткий обзор статических генераторов, с которыми автор
познакомился за последние несколько дней, окончательно решив перейти с
доморощенной системы генерации на промышленную (см. об этом мой пост
[Два точка ноль](https://easimonenko.bitbucket.io/#!news/two-dot-zero)).

Я потратил несколько дней на ознакомление с различными системами
управления статическими сайтами. Здесь же хочу выделить особо:

- [Jekyll][]
- [Sphinx][]
- [GitHub Pages][]
- [Hakyll][]

Несколько слов о каждой.

<!-- end-of-lead -->

## Jekyll

Система написана на *Ruby* и основана на некоторых идеях *Ruby On Rails*.
Основным форматом публикаций здесь является [Markdown][], но есть и поддержка
некоторых других, в том числе и *HTML-шаблонизатора*. Очевидно, что для работы
*Jekyll* потребуется установить *Ruby* (в Windows можно воспользоваться
[Ruby Installer][]), а затем установить соответствующий *Gem*-пакет.

Плюсом *Jekyll* является его поддержка [GitHub Pages][]. Правда поддержка эта
урезанная, точнее: запрещено использовать нестандартные дополнения, а это
значит, что расширять и изменять систему генерации не выйдет.

## Sphinx

Система написана на *Python* и изначально предназначена для системы
документации.  Очень удобна кроме документации также для любых других текстовых
публикаций. Плюсов два:

- встроенная система поиска, написанная на *JavaScript*;
- сайт можно разместить на сервисе [Read the Docs][];
- у *Read the Docs* есть интеграция с [GitHub][] и [Bitbucket][].

Основной минус - жёстко заданная структура сайта, ориентированная на
документацию.

## GitHub Pages

Вообще говоря, *GitHub Pages* позволяет использовать три подхода:

- использовать встроенный *Jekyll* (см. выше);
- размещать готовые страницы;
- использовать автогенерацию страниц по шаблону на основе *Markdown*.

Немного о третьем подходе. Здесь всё очень просто. Создаёте на [GitHub][]
репозиторий с именем *LOGIN.github.io*, где *LOGIN* это Ваш логин на *GitHub*,
и в настройках репозитория в разделе *GitHub Pages* щёлкаете кнопку
*Automatic Page Generator*. После чего выбираете тему оформления, и сайт готов.

Огромный плюс системы заключается в том, что сайт является *Git*-репозиторием.

## Hakyll

Для своего сайта после экспериментов с разными системами я выбрал *Hakyll*.
Эта система написана на [Haskell][]. Гибкость достигается как поддержкой
различных форматов документов, а также шаблонизатора, так и возможностью
вносить изменения в генератор сайта.

Для изменения процесса генерации сайта, а также для добавления новых
возможностей по генерации, нужно вносить изменения в файл, который в дереве
проекта сайта называется *site.hs*. Структура его достаточно ясна, при
необходимости можно обратиться к документации *Hakyll* (
<http://www.jaspervdj.be/hakyll/reference/index.html>).

К сожалению, я не нашёл ни одного бесплатного хостинга с поддержкой не то,
чтобы *Haskell*, а хотя бы *Hakyll*. Но в принципе можно обойтись и локальной
генерацией с последующим выкладыванием на любой статический хостинг. Очень
удобно, однако, использовать хостинги типа *[GitHub Pages]*. Я же решил
размещаться на [Bitbucket][], но об этом другой раз.

[Hakyll]: http://jaspervdj.be/hakyll/
[Jekyll]: http://jekyllrb.com/
[Sphinx]: http://sphinx-doc.org/
[GitHub Pages]: http://pages.github.com/
[GitHub]: https://github.com/
[Ruby Installer]: http://rubyinstaller.org/
[Markdown]: http://daringfireball.net/projects/markdown/
[Read the Docs]: https://readthedocs.org/
[Haskell]: http://www.haskell.org/
[Bitbucket]: https://bitbucket.org/

(c) Симоненко Евгений, 2013
