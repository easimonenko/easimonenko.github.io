---
layout: post
title: Ручное создание веб-проекта на JavaScript
author: Evgeny Simonenko
email: easimonenko@gmail.com
date: 2016-01-26
updating_date: 2016-02-15
category: Tutorial
tags: [JavaScript, TypeScript, Node.js, Bower, NPM, Web Development]
---

Шпаргалка по ручному созданию проекта JavaScript или TypeScript
с использованием Visual Studio Code.

<!-- end-of-lead -->

## Проект на GitHub

Регистрируем репозиторий на GitHub (кроме имени, задаём репозиторию краткое, в
одну строчку описание проекта на английском языке; выбираем лицензию; выбираем
опцию создания файла README).

Клонируем репозиторий на компьютер:

``` bash
git clone path_to_repository
```

## Редактирование README

Открываем папку репозитория в Visual Studio Code.

Редактируем README.md (указываем данные разработчика, применяемые технологии).
При редактировании документов Markdown удобно разбить окно редактора на два
(кнопка Split Editor) и во втором окне включить режим предпросмотра (кнопка
Open Preview). Тогда прямо во время редактирования можно будет наблюдать, как
будет выглядеть результат.

Добавляем README.RU.md на русском языке (не обязательно).

## Настройка окружения Node.js

Добавляем файл *package.json*:

``` bash
npm init
```

По этой команде будут заданы несколько вопросов, на часть из которых утилита
сама найдёт ответ и предложит их по-умолчанию. Не забудьте добавить в
`package.json` поле `"private": true`, чтобы предотвратить, пусть и
маловероятную, непреднамеренную публикацию пакета в Сети.

Добавляем файл .gitignore и вписываем в него строки:

```
node_modules
build
dist
```

В папке `node_modules` находятся загруженные модули Node.js, их не обязательно
сохранять в репозитории, так как после клонирования репозитория они могут быть
вновь загружены командой

``` bash
npm install
```

При этом в зависимости от настройки будут загружены более свежие версии, чем
использовались в момент разработки. Обратной стороной медали будет более
медленная загрузка кода модулей, чем если бы они были сохранены в репозиторий.
В папке `build` будет сохраняться промежуточные файлы сборки проекта, в основном
файлы JavaScript, полученные в результате компиляции кода TypeScript. В папке
`dist` будет находится код, готовый к работе. Его также не будем сохранять в
репозиторий, так как он может быть получен командой (которая будет настроена
позже).

## Настройка bower

Для разработки клиентов на JavaScript возможно удобнее будет
использовать *bower* вместо npm. Уставка bower:

``` bash
npm install bower -g
```

В Windows 7/8/10 "глобально" устанавливаемые пакеты размещаются в папке
`C:\Users\UserName\AppData\Roaming\npm`.

Перед использованием bower в проекте нужно произвести его инициализацию
с помощью интерактивной утилиты:

``` bash
bower init
```

При этом потребуется ответить на несколько вопросов. Часть ответов на них
утилита возьмёт из раннее созданного *package.json*. В результате будет
сформирован файл *bower.json* в корне проекта аналогичный файлу package.json.

Установка пакетов bower:

``` bash
bower install jquery --save
```

Устанавливаемые пакеты размещаются в папке *bower_components*.

## Проект в Visual Studio Code

Добавим в проект папку *src*. В ней будут находиться исходные тексты проекта.

Добавим в папку src первый исходник *main.ts*:

``` typescript
console.log("TODO main.ts");
```

Настроем Task Runner на компиляцию кода TypeScript. Для этого добавим в проект
папку *.vscode* и в неё файл *tasks.json*:

``` json
{
  "version": "0.1.0",
  "command": "tsc",
  "isShellCommand": true,
  "showOutput": "silent",
  "args": ["-p", "src"],
  "problemMatcher": "$tsc"
}
```

Если вызвать командную строку Code, нажав *F1*, набрав в ней `tasks` и выбрав в
списке `Configure Task Runner`, то можно получить пример файла *tasks.json* с
комментариями, который затем можно отредактировать.

Настроем компилятор TypeScript. Сначала вызовем в папке *src* команду

``` bash
tsc --init
```

Эта команда создаст файл настройки *tsconfig.json*:

``` json
{
    "compilerOptions": {
        "module": "commonjs",
        "target": "es3",
        "noImplicitAny": false,
        "outDir": "built",
        "rootDir": ".",
        "sourceMap": false
    },
    "exclude": [
        "node_modules"
    ]
}
```

Отредактируем его:

``` json
{
    "compilerOptions": {
        "module": "commonjs",
        "target": "es6",
        "noImplicitAny": false,
        "outDir": "../build",
        "rootDir": ".",
        "sourceMap": true,
        "removeComments": true
    },
    "exclude": [
        "node_modules"
    ]
}
```

Теперь нажав в Code *Ctrl-Shift-B* или вызвав командную строку Code (*F1*) и
выбрав *Tasks: Run Build Task* можем запускать процесс компиляции исходников на
TypeScript.

## Настройка TypeScript

Если TypeScript в системе ещё не установлен, то это нужно сделать командой:

``` bash
npm install typescript -g
```

После выполнения этой команды в системе появится компилятор TypeScript,
вызываемый командой *tsc*.

Для качественной работы с кодом на TypeScript с использованием библиотек
JavaScript, да и с кодом на JavaScript в среде Code, необходимо установить для
каждого модуля декларации. Делается это командой tsd. Установим её:

``` bash
npm install tsd -g
```

Теперь можно установить требуемые декларации:

``` bash
tsd install node gulp --save
```

Декларации будут размещены в подкаталоге проекта *typings*. А корне каталога
проекта появится файл *tsd.json* с описаниями загруженных деклараций.

Узнать о наличии декларации для модуля можно командой:

``` bash
tsd query node
```

Более общий запрос:

``` bash
tsd query *node*
```

Для ссылок на декларации в коде на TypeScript и JavaScript нужно добавлять в
начало каждого файла исходных текстов строки вида:

``` xml
/// <reference path="../typings/node/node.d.ts"/>
```

Переустановка всех загруженных деклараций осуществляется по команде:

``` bash
tsd install
```

Таким образом, также как и модули npm декларации можно не сохранять в
репозитории проекта, а после клонирования просто занова скачивать.

Обновление деклараций осуществляется по команде:

``` bash
tsd update
```

## Настройка системы сборки Gulp

Gulp требует как глобальной, так и локальной установки:

``` bash
npm install -g gulp
npm install gulp
```

Установим также пакет для поддержки TypeScript, если разработка будет вестись
на нём:

``` bash
npm install gulp-typescript --save-dev
```

Для удобства написания `gulpfile.js` нужно установить также необходимые
декларации:

``` bash
tsd install gulp gulp-typescript typescript --save
```

## Ссылки

* Хороший пример создания сервера на Node.js и TypeScript:
    [Writing a chat server using Node.js, TypeScript, and WebSockets](http://www.codeproject.com/Articles/871622/Writing-a-chat-server-using-Node-js-TypeScript-and)

(c) Симоненко Евгений, 2016
