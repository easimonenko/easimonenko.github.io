---
layout: post
title: Hakyll. Синтаксическая подсветка
date: 2013-08-14
category: Tutorial
tags: [Hakyll, Static Site Generator, Web Development]
---

В этой заметке рассказывается как добавить синтаксическую подсветку в _Hakyll_
для файлов в формате _Markdown_ .

## Включение синтаксической подсветки

Поддержка синтаксической подсветки поставляется вместе с _Hakyll_, и, чтобы её
включить, потребуется произвести несколько простейших действий.

- загрузите репозиторий _Hakyll_:

``` bash
git clone https://github.com/jaspervdj/hakyll.git
```

- скопируйте в каталог `css` Вашего проекта файл из загруженного репозитория:

```
web/css/syntax.css
```

- добавьте соответствующий тег `link` в шаблон
    `templates/default.html` (или в какой другой на Ваше усмотрение):

``` xml
<link rel="stylesheet" type="text/css" href="/css/syntax.css" />
```

- оформите примеры исходных текстов в следующем формате:

\`\`\` язык<br />
исходный код<br />
\`\`\`

## Примеры подсветки

Ниже я привёл примеры работы синтаксической подсветки на разных языках. В
скобках для каждого из языков указано его обозначение.

- Haskell (haskell)

``` haskell
main = print "Hello!"
```

- C++ (cpp)

``` cpp
#include <cstdio>

int main() {
    puts("Hello!");
    return 0;
}
```

- Bash (bash)

``` bash
echo "Hello!"
```

- Pascal (pascal)

``` pascal
begin
  WriteLn "Hello!";
end.
```

- Ruby (ruby)

``` ruby
puts "Hello!"
```

- Perl (perl)

``` perl
print "Hello!\n";
```

## Настройка подсветки

Вы можете изменять тему оформления исходников просто редактируя
файл стилей `css/syntax.css`. Если Вы хотите получить такое же обрамление
как у меня добавьте в этот файл стилей следующие строчки и подкорректируйте
стиль на свой вкус:

``` css
pre.sourceCode {
    background-color: #F6F6F6;
    box-shadow: inset 0 1pt 1pt #999999;
    padding: 3pt;
    border-radius: 3pt;
    display: inline-block;
}
```

Пока всё!

## Примечание от 6 апреля 2020

Примеры синтаксической подсветки, наблюдаемые в текущей версии сайта,
соответствуют предоставляемой Jekyll с темой Emacs из пакета Pygments
<https://github.com/richleland/pygments-css>, а не Hakyll.

(c) Симоненко Евгений, 2013
