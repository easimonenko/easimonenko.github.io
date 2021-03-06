---
layout: post
title: Начало перехода к использованию для блога Jekyll
date: 2020-03-26
category: Site News
tags: [Jekyll, Static Site Generator, Bloggero, GitHub Pages]
---
Вот, решил отказаться от использования самодельного инструмента
[Bloggero](https://github.com/easimonenko/bloggero). Главная причина: не нужно
превращать сайт (блог) в веб-приложение, в
[EWW](https://www.gnu.org/software/emacs/manual/html_mono/eww.html)
(встроенный в GNU Emacs браузер) такой блог не почитаешь. Далее:
скомпилированный код Bloggero весит больше мегабайта, это много и это приводит
к задержке открытия блога. Затем: Bloggero работает не очень быстро, на
смартфоне с Android это особенно заметно. И наконец: Bloggero давно не
обновляется, с тех пор как вышел Elm 0.19, и всё сломалось.

Теперь сижу и разбираюсь, как вести блог на [Jekyll][]. Почему Jekyll? Как и
когда-то давно, я рассматривал несколько вариантов, ну и, Вы угадали, я
выбрал Jekyll, потому что для него у GitHub Pages есть автогенерация после
очередного коммита в репозиторий блога.

Пока всё! Если что нарою интересного мне, то всем расскажу. Заглядывайте, или
лучше читайте RSS.

[Jekyll]: https://jekyllrb.com/ "Jekyll"

(c) Симоненко Евгений, 2020
