---
layout: post
title: Основы работы с Neo4j в браузере
author: Evgeny Simonenko
email: easimonenko@gmail.com
date: 2020-04-25 22:56
category: Tutorial
tags: [Neo4j, Graph Databases]
---

В статье рассматривается как начать работать с графовой СУБД
[Neo4j](https://neo4j.com/), используя *Neo4j Browser*. Это руководство может быть
полезным как дополнение к книге Редмонда и Уилсона "Семь баз данных за семь
недель", так как рассматриваемый веб-интерфейс был полностью переработан, а также
к книге "Графовые базы данных" (Робинсон, Вебер, Эифрем), так как в ней этот вопрос
вообще не рассматривается. Статья рассчитана на приступающих к изучению Neo4j. Те,
кто уже знаком с этой СУБД, могут смело её пропустить.

![Neo4j Browser: home screen](/images/neo4j-browser-home.png)

<!-- end-of-lead -->

*Примечание*. В статье не рассматривается как установить и настроить Neo4j. Если
Вы хотите узнать, как это сделать, прочитайте пост
[Установка и запуск Neo4j]({% post_url 2018-01-20-installing-and-running-neo4j %}).
Рассматриваемые версии Neo4j 3.3.2 и 3.4.0, Neo4j Browser 3.1.4 и 3.1.12,
соответственно.

## Начало работы

Для начала убедимся, что Neo4j запущена (пример для Linux):

``` sh
service --status-all | grep neo4j
```

``` plain
 [ + ]  neo4j
```

Знак "плюс" означает, что СУБД уже запущена, "минус" -- ещё нет.

Или с использованием systemctl:

``` sh
systemctl status neo4j
```

Для запуска Neo4j выполните команду:

``` sh
sudo service neo4j start
```

Или с использованием systemctl:

``` sh
sudo systemctl start neo4j
```

После запуска перейдите по ссылке <http://localhost:7474/browser/>. Вы должны
увидеть интерфейс Neo4j Browser представленный на изображении выше.

Сейчас нас будут интересовать два элементы интерфейса, изображённые ниже: редактор
и учебник.

![Neo4j Browser: play](/images/neo4j-browser-play.png)

## Учебник

Neo4j предоставляет великолепный интерактивный учебник для начинающих. Очень
рекомендую его пройти. Для этого просто щёлкните на **Start Learning** и сначала
ознакомьтесь с основными понятиями Neo4j:

![Neo4j Browser: graph fundamentals](/images/neo4j-play-concepts-fundamentals.png)

![Neo4j Browser: graph relationships](/images/neo4j-play-concepts-relationships.png)

По достижению последнего шага щёлкните на **Intro** и ознакомьтесь с возможностями
Neo4j Browser:

![Neo4j Browser: next steps](/images/neo4j-play-next-steps.png)

![Neo4j Browser: introduction](/images/neo4j-play-introduction.png)

## Редактор

В верхней части окна Neo4j Browser располагается строка так называемого редактора:

![Neo4j Browser: editor](/images/neo4j-browser-editor.png)

Начиная набор команд с двоеточия, увидим список всех доступных команд с кратким
описанием:

![Neo4j Browser: list of commands](/images/neo4j-editor-list.png)

Вызовем команду `:help`:

![Neo4j Browser: help command](/images/neo4j-editor-help.png)

![Neo4j Browser: help](/images/neo4j-browser-help.png)

Чтобы ознакомиться с примерами работы с графами можно выбрать
`:play movie graph` или `:play northwind graph`.

Мы не будем здесь рассматривать эти примеры, а рассмотрим как создать свой граф с
помощью языка _Cypher_.

## Создаём граф

Для начала можно ознакомиться с языком Cypher, вызвав команду:

``` neo4j
:play cypher
```

![Neo4j Browser: play cypher](/images/neo4j-play-cypher.png)

Итак, начнём. Создадим небольшой социальный граф. Перейдём в редактор и наберём
первую команду на языке Cypher:

``` cypher
CREATE (u1:Person {name: "Evgeny", from: "Krasnodar"})
```

После выполнения команды Browser сообщит нам результат:

![Neo4j Browser: create result](/images/neo4j-browser-create-result.png)

Добавим ещё один узел:

``` cypher
CREATE (u2:Person {name: "Dmitry", from: "Tula"})
```

Теперь запросим все узлы типа `Person` и извлечём значения свойства `name`:

``` cypher
MATCH (ee:Person) RETURN ee.name
```

![Neo4j Browser: property match result](/images/neo4j-cypher-match-property.png)

_Примечание._ Как и в SQL есть возможность упорядочить извлекаемые данные по
какому-либо полю:

``` cypher
MATCH (ee:Person) RETURN ee.name ORDER BY ee.name
```

Далее, можем запросить все узлы данного типа:

``` cypher
MATCH (ee:Person) RETURN ee
```

![Neo4j Browser: edges match result](/images/neo4j-cypher-match-edges.png)

Обратите внимание на появившуюся кнопку **Graph**. Щёлкним на ней и увидим наши
узлы в графическом виде:

![Neo4j Browser: graph match result](/images/neo4j-cypher-match-graph.png)

_Примечание._ В версии 3.4 по-умолчанию как-раз открывается графическое
представление. Для получения табличного представления нужно щёлкнуть на кнопку с
надписью "Table". Хотя, бывает и наоборот.

Добавим связь между узлами:

``` cypher
MATCH (e:Person) WHERE e.name = "Evgeny"
MATCH (d:Person) WHERE d.name = "Dmitry"
CREATE (e)-[:KNOWS]->(d),
  (d)-[:KNOWS]->(e)
```

И вновь запросим наш граф:

![Neo4j Browser: graph with relationships](/images/neo4j-cypher-with-relationships.png)

С помощью Cypher можно также выполнять различные операции над графами, например,
запрашивать смежные вершины, друзей друзей в социальном графе, удалять рёбра и
вершины и многое другое, но это тема для отдельного разговора.

Также можно настраивать Neo4j Browser на различный стиль отображения узлов и
связей в зависимости от заданных им меток.

## Ссылки

- [Установка и запуск Neo4j // Симоненко Е.А.]({% post_url 2018-01-20-installing-and-running-neo4j %})
- [Neo4j Browser User Interface Guide](https://neo4j.com/developer/neo4j-browser/)
- [The Neo4j Developer Manual v3.4](https://neo4j.com/docs/developer-manual/3.4/)
- [The Neo4j Developer Manual v3.3](https://neo4j.com/docs/developer-manual/3.3/)
- [Neo4j Graph Database Sandbox](https://neo4j.com/sandbox-v2/)
- [Neo4j GraphGists](https://neo4j.com/graphgists/)

## Примечание

Этот пост был написан и выложен в мой репозиторий
[research-work](https://github.com/easimonenko/research-work)
1 февраля 2018, затем обновлён там же 6 июня 2018, и, наконец,
опубликован на [Хабр](https://habr.com/ru/post/470541/) 7 октября 2019. Редакция
от 25 апреля 2020, опубликованная в этом блоге, имеет лишь косметические правки.

(c) Симоненко Евгений, 2018, 2019, 2020
