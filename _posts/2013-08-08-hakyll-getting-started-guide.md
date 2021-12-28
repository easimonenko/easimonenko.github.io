---
layout: post
title: Hakyll. Руководство по началу использования
author: Evgeny Simonenko
email: easimonenko@gmail.com
date: 2013-08-08,
updating_date: 2013-08-21
category: Tutorial
tags: [Hakyll, Haskell, Static Site Generator, Web Development]
---

В заметке описывается процесс подготовки к использованию [Hakyll][] для
создания статических сайтов.

<!-- end-of-lead -->

## Установка _Hakyll_

Для работы с _Hakyll_ потребуется сначала установить [Haskell][]. Для Windows
можно воспользоваться [Haskell Platform][]. Для установки _Haskell Plarform_
требуется около 2 Гб дискового пространста и несколько минут времени. После
чего можно устанавливать _Hakyll_.

_Hakyll_ устанавливается как пакет [Cabal][], системы управления пакетами для
_Haskell_. Перед установкой пакета для _Hakyll_ рекоменуется сначала обновить
базу данных пакетов _Cabal_ и сам _Cabal_:

``` bash
cabal update
cabal install cabal-install
cabal install hakyll
```

Вам потребуется терпение, чтобы дождаться окончания процесса установки
_Hakyll_, так как _Hakyll_ тянет за собой множество пакетов, и каждый из них
должен быть перед установкой скомпилирован, так как _Haskell_ компилируемый
язык программирования, как, например, _C++_ или _Pascal_.

## Создание проекта сайта

Если Вам повезло, и _Hakyll_ был установлен (у меня из трёх систем он
установился только на _Windows 7_, а на _Windows XP_ и _Fedora 18_ - нет,
возникали ошибки компиляции разных пакетов; правда повторноя попытка
установки под _Windows XP_ завершилась успехом), то Вы можете начать создавать
сайты с помощью _Hakyll_. Делается это очень просто:

``` bash
hakyll-init PROJECT
```

где PROJECT это название Вашего проекта.

(Если после установки _Hakyll_ система не находит команду `hakyll-init`, то Вам
просто нужно прописать путь к каталогу `bin` _Cabal_ в системной переменной
`PATH`. В _Windows 7_ этот путь будет выглядеть так
`C:\Users\EvAn\AppData\Roaming\cabal\bin`.)

В результате в текущем каталоге будет создана папка с названием `PROJECT`, и,
перейдя в неё, Вы сможете лицезреть исходные тексты заготовки сайта:

``` bash
cd PROJECT
dir
```

Структура дерева файлов и каталогов проекта следующая:

- `css/`: Стилевые файлы CSS.

- `images/`: Изображения.

- `posts/`: Файлы постов.

- `templates/`: Шаблоны.

- `about.rst`: Пример файла _about_ в формате [reStructuredText][].

- `contact.markdown`: Пример файла _contact_ в формате [Markdown][].

- `index.html`: Заготовка файла _index_.

- `site.hs`: Собственно генератор сайта на языке _Haskell_.

## Генерация сайта

Перед тем как начать собственно генерацию Вашего сайта, нужно скомпилировать
утилиту `site.hs`:

``` bash
ghc --make site.hs
```

Через секунд десять Вы сможете запустить процесс генерации сайта:

``` bash
site build
```

Процесс генерации сопровождается сообщениями.

После генерации в каталог проекта сайта добавятся ещё две папки:

- `_site/`: Содержит сгенерированный сайт.

- `_cache/`: Содержит кеш сайта для утилиты _site_.

## Просмотр сайта

Утилита _site_ по совместительству ещё является и веб-сервером, чтобы нам было
удобно просматривать сайт локально.

Запустите команду:

``` bash
site preview
```

И откройте в браузере ссылку <http://localhost:8000/>.

Если выполнение последней команды не удалось, то попробуйте следующую:

``` bash
site server --port=5050
```

И откройте в браузере ссылку <http://localhost:5050/>.

## Редактирование сайта

Редактировать содержимое проекта сайта можно в любом текстовом редакторе. Лично
я предпочитаю [Emacs][], а также [Far][] с [Colorer][].

Каждый раз после правки перед просмотром результата следует повторять процесс
генерации командой:

``` bash
site build
```

Важно, что перегенерироваться будут не все компоненты сайта, а только те, что
изменились с момента последней сборки.

Если потребовалось внести изменения в `site.hs`, то не забудьте его
перекомпилировать:

``` bash
ghc --make site.hs
```

## Публикация сайта

Сайт можно опубликовать просто скопировав содержимое папки `_site/` проекта на
Ваш хостинг. Если Вы не гнушетесь бесплатных хостингов, то можете разместить
свой сайт на одном из _Git_-сервисов. Но об этом другой раз.

Пока всё!

## Что ещё почитать

- [Hakyll для начинающих](http://habrahabr.ru/post/175877/)
- [Hakyll setup](http://yannesposito.com/Scratch/en/blog/Hakyll-setup/)
- [Markdown - гаечный ключ для забивания треугольных болтов](http://mydebianblog.blogspot.com.au/2012/09/markdown.html)

## История изменений

_2015-06-18_ С тех пор как была опубликована эта заметка в Сети были
опубликованы ещё пара неплохих на ту же тему:

- [Создаем блог с помощью Hakyll](http://dimchansky.github.io/posts/2014/10/07/getting-started-with-hakyll/)
- [Красноглазый Блог: посты с тегом Hakyll](http://livid.pp.ru/tags/Hakyll.html)

## Ссылки

[Hakyll]: http://jaspervdj.be/hakyll/
[Git]: http://git-scm.com/
[Haskell]: http://www.haskell.org/
[Haskell Platform]: http://www.haskell.org/platform/windows.html
[Cabal]: http://www.haskell.org/cabal/
[Markdown]: http://daringfireball.net/projects/markdown/
[reStructuredText]: http://docutils.sourceforge.net/rst.html
[Emacs]: http://www.gnu.org/software/emacs/
[Far]: http://www.farmanager.com/
[Colorer]: http://sourceforge.net/projects/colorer/

- [Hakyll][]
- [Git][]
- [Haskell][]
- [Haskell Platform][]
- [Cabal][]
- [Markdown][]
- [reStructuredText][]
- [Emacs][]
- [Far][]
- [Colorer][]

(c) Симоненко Евгений, 2013
