---
layout: post
title: Начальные шаги по миграции с Ruby 2.7 на 3.0
author: Evgeny Simonenko
date: 2022-05-22 23:59
category: Tutorial
tags: [Jekyll, Ruby, Ubuntu, Linux]
---

В недавно вышедшем _Ubuntu Linux 22.04 LTS_ Ruby был обновлён с версии 2.7 на 3.0.
Если вы обновили систему на новую версию без переустановки, то ожидаемо ранее установленные
gem перестали работать. В этой статье будут описаны начальные шаги по реанимации после
обновления Ruby.

<!-- end-of-lead -->

## Шаг 1

Заново установите `bundler` и `jekyll` (если используете):

``` shell
 gem install bundler jekyll --user-install
```

## Шаг 2

Обновите пути в `.profile`:

``` shell
if [ -d "$HOME/.local/share/gem/ruby/3.0.0" ] ; then
  RUBY_PATH="$HOME/.local/share/gem/ruby/3.0.0"
  export RUBY_PATH
  GEM_HOME="$RUBY_PATH"
  export GEM_HOME
  PATH="$RUBY_PATH/bin:$PATH"
fi
```

И перезайдите в систему, чтобы переменные окружения обновились.

## Шаг 3

Перейдите в каталог с вашим проектом на Ruby и установите заново все зависимости:

``` shell
bundle install
```

## Шаг 4

Для проектов на Jekyll придётся добавить зависимость от
[`webrick`](https://rubygems.org/gems/webrick), иначе просмотр сайта
будет невозможен из-за ошибки (`webrick` из третьей версии Ruby был исключён)
(см. также
<https://stackoverflow.com/questions/65989040/bundle-exec-jekyll-serve-cannot-load-such-file>
и <https://jekyllrb.com/docs/#instructions>):

``` shell
bundle add webrick
```

## Шаг 5 (заключительный)

Удалите каталог `~/.local/share/gem/ruby/2.7.0`:

``` shell
rm -r ~/.local/share/gem/ruby/2.7.0
```

## Что дальше

Версия Ruby 3.0 принесла по сравнению с 2.7 много интересного и полезного. Подробнее можно
почитать на
[странице выпуска](https://www.ruby-lang.org/en/news/2020/12/25/ruby-3-0-0-released/).

(c) Симоненко Евгений, 2022
