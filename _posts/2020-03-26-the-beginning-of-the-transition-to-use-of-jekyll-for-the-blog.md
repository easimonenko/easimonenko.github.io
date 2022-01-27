---
layout: post
title: Начало перехода к использованию для блога Jekyll
author: Evgeny Simonenko
email: easimonenko@gmail.com
date: 2020-03-26
category: Site News
tags: [Jekyll, Static Site Generators, Bloggero, GitHub Pages]
---
Вот, решил отказаться от использования самодельного инструмента
[Bloggero][]. Главная причина: не нужно превращать сайт (блог) в веб-приложение, в
[EWW][] (встроенный в GNU Emacs браузер) такой блог не почитаешь. Далее:
скомпилированный код Bloggero весит больше мегабайта, это много и это приводит
к задержке открытия блога. Затем: Bloggero работает не очень быстро, на
смартфоне с Android это особенно заметно. И наконец: Bloggero давно не
обновляется, с тех пор как вышел Elm 0.19, и всё сломалось.

Теперь сижу и разбираюсь, как вести блог на [Jekyll][]. Почему Jekyll? Как и
когда-то [давно]({% post_url 2013-08-05-static-sites-generators %}),
я рассматривал несколько вариантов, ну и, Вы угадали, я
выбрал Jekyll, потому что для него у GitHub Pages есть автогенерация после
очередного коммита в репозиторий блога.

Пока всё! Если что нарою интересного мне, то всем расскажу. Заглядывайте или
лучше читайте [RSS]({{site.url}}/feed.xml).

[Bloggero]: https://github.com/easimonenko/bloggero "Bloggero"
[EWW]: https://www.gnu.org/software/emacs/manual/html_mono/eww.html "EWW"
[Jekyll]: https://jekyllrb.com/ "Jekyll"

<!-- end-of-lead -->

(c) Симоненко Евгений, 2020
