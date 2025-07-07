---
layout: post
title: Сборка GNU Emacs из исходных текстов
date: 2025-07-07 13:33 +0000
author: Evgeny Simonenko
email: easimonenko@gmail.com
category: Tutorial
tags: [GNU Emacs]
---

Инструкция по сборке [GNU Emacs](https://www.gnu.org/software/emacs/) из исходников, полученных из его репозитория Git. Сборка производилась в среде Ubuntu Linux 22.04.

<!-- lead-ends-here -->

## Загрузка исходников

Оригинальные исходные тексты GNU Emacs можно посмотреть на сайте https://Savannah.GNU.org по ссылке https://cgit.git.savannah.gnu.org/cgit/emacs.git Загрузим их:

``` shell
cd ~/Sources
git clone https://git.savannah.gnu.org/git/emacs.git
cd emacs
```

## Установка необходимых пакетов

Для сборки из исходников GNU Emacs потребуется установить некоторые дополнительные пакеты разработчика. Их список может отличаться в зависимости от конфигурации сборки.

Основные пакеты, необходимые для любой конфигурации:

- GCC
- Make
- Libc
- Autoconf
- Texinfo

``` shell
sudo apt install gcc make libc-dev autoconf texinfo
```

Затем пакеты, соответствующие конфигурации:

``` shell
sudo apt install libgtk-3-dev libgccjit-11-dev libgnutls28-dev libmagickwand-dev libtinfo-dev libtree-sitter-dev libgif-dev libxpm-dev
```

Этот список может отличаться, если будут выбраны другие опции конфигурации.

## Конфигурирование сборки

Сначала нужно запустить скрипт `autogen.sh`:

``` shell
./autogen.sh
```

Этот скрипт сгенерирует `configure.sh`, который нужно вызвать, передав ему нужные опции:

``` shell
./configure --prefix=/home/easimonenko/Software/emacs-2025-07-07 --with-native-compilation --with-x-toolkit=gtk3 --with-tree-sitter --with-wide-int --with-modules --with-gnutls --with-mailutils --with-cairo --with-imagemagick --with-file-notification=yes --without-dbus
```

Опция `--with-x-toolkit=gtk3` указывает собирать графический интерфейс для X Window System с использованием библиотеки Gtk3. Есть и другие варианты, в частности, для сборки под Wayland нужно эту опцию заменить на `--with-pgtk`.

Вероятно, в процессе конфигурирования будет обнаружено, что какие-то требуемые пакеты не установлены. Тогда просто нужно их установить и снова запустить конфигурацию. И так до тех пор, пока скрипт не будет выполнен успешно.

## Сборка

Вызовем `make` с опцией, ограничивающей количество задействуемых ядер (потоков) процессора:

``` shell
make -j2
```

## Установка

Установка собранного Emacs происходит как обычно:

``` shell
make install
```

## Запуск

Переходим в каталог, который был указан в опции `prefix` и запускаем `emacs`:

``` shell
cd ~/Software/emacs-2025-07-07/bin
./emacs
```

(c) Евгений Симоненко, 2025
