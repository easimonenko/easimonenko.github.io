---
layout: post
title: Введение в язык запросов Cypher
author: Evgeny Simonenko
email: easimonenko@gmail.com
date: 2020-05-29 23:24
category: Tutorial
tags: [Cypher, Neo4j, Query Languages, Graph Databases]
---

Язык запросов _Cypher_ изначально разработан специально для графовой СУБД
[Neo4j](https://neo4j.com/). Целью Cypher является предоставить человеко-читаемый
язык запросов к графовым базам данных похожий на SQL. На сегодня Cypher
поддерживается несколькими графовыми СУБД. Для стандартизации Cypher была создана
организация [openCypher](http://www.opencypher.org/).

Основы работы с СУБД Neo4j описаны в
[Основы работы с Neo4j в браузере]({% post_url 2020-04-25-basics-of-working-with-neo4j-in-a-browser%}).

Для знакомства с Cypher рассмотрим пример генеалогического дерева заимствованный
из классического учебника по Прологу за авторством И. Братко. На этом примере
будет показано как добавлять узлы и связи в граф, как им назначать метки и
атрибуты и как задавать вопросы.

<!-- end-of-lead -->

![Генеалогическое дерево в Neo4j, отредактированный вид](/images/neo4j_family_tree_edited_view.png)

Итак, пусть мы имеем генеалогическое дерево, представленное на картинке ниже.

![Генеалогическое дерево](/images/family_tree.png)

Посмотрим как сформировать соответствующий граф на языке Cypher:

``` cypher
CREATE (pam:Person {name: "Pam"}),
  (tom:Person {name: "Tom"}),
  (kate:Person {name: "Kate"}),
  (mary:Person {name: "Mary"}),
  (bob:Person {name: "Bob"}),
  (liz:Person {name: "Liz"}),
  (dick:Person {name: "Dick"}),
  (ann:Person {name: "Ann"}),
  (pat:Person {name: "Pat"}),
  (jack:Person {name: "Jack"}),
  (jim:Person {name: "Jim"}),
  (joli:Person {name: "Joli"}),
  (pam)-[:PARENT]->(bob),
  (tom)-[:PARENT]->(bob),
  (tom)-[:PARENT]->(liz),
  (kate)-[:PARENT]->(liz),
  (mary)-[:PARENT]->(ann),
  (bob)-[:PARENT]->(ann),
  (bob)-[:PARENT]->(pat),
  (dick)-[:PARENT]->(jim),
  (ann)-[:PARENT]->(jim),
  (pat)-[:PARENT]->(joli),
  (jack)-[:PARENT]->(joli)
```

Запрос CREATE на добавление данных в графовую СУБД состоит из двух частей:
добавление узлов и добавление связей между ними. Каждому добавляемому узлу
назначено в рамках данного запроса имя, которое затем использовано при создании
связей. Узлы и связи могут хранить документы. В нашем случае узлы содержат
документы с полями name, а связи документов не содержат. Также узлы и связи могут
быть помечены. В нашем случае узлам назначена метка Person, а связям PARENT. Метка
в запросах выделяется двоеточием перед её названием.

Итак, Neo4j нам сообщил, что: `Added 12 labels, created 12 nodes, set 12
properties, created 11 relationships, completed after 9 ms.`

Посмотрим, что у нас получилось:

``` cypher
MATCH (p:Person) RETURN p
```

![Генеалогическое дерево в Neo4j](/images/neo4j_family_tree.png)

Никто не запрещает нам отредактировать внешний вид получившегося графа:

![Генеалогическое дерево в Neo4j, отредактированный вид](/images/neo4j_family_tree_edited_view.png)

Что с этим можно делать? Можно убедиться в том, что, например, Pam является
родителем Bob'а:

``` cypher
MATCH ans = (:Person {name: "Pam"})-[:PARENT]->(:Person {name: "Bob"})
RETURN ans
```

Получим соответствующий подграф:

![Pam is parent of Bob](/images/pam-parent-bob.png)

Однако это не совсем то, что нам надо. Изменим запрос:

``` cypher
MATCH ans = (:Person {name: "Pam"})-[:PARENT]->(:Person {name: "Bob"})
RETURN ans IS NOT NULL
```

Теперь в ответ получаем `true`. А если спросим:

``` cypher
MATCH ans = (:Person {name: "Pam"})-[:PARENT]->(:Person {name: "Liz"})
RETURN ans IS NOT NULL
```

То ничего не получим... Здесь нужно добавить слово `OPTIONAL`, тогда если
результат будет пуст, то будет возвращаться `false`:

``` cypher
OPTIONAL MATCH ans = (:Person {name: "Pam"})-[:PARENT]->(:Person {name: "Liz"})
RETURN ans IS NOT NULL
```

Теперь получаем ожидаемый ответ `false`.

Далее, можно посмотреть, кто кому является родителем:

``` cypher
MATCH (p1:Person)-[:PARENT]->(p2:Person)
RETURN p1, p2
```

Откроем вкладку результата с надписью `Text` и увидим таблицу с двумя колонками:

``` plain
╒═══════════════╤═══════════════╕
│"p1"           │"p2"           │
╞═══════════════╪═══════════════╡
│{"name":"Pam"} │{"name":"Bob"} │
├───────────────┼───────────────┤
│{"name":"Tom"} │{"name":"Bob"} │
├───────────────┼───────────────┤
│{"name":"Tom"} │{"name":"Liz"} │
├───────────────┼───────────────┤
│{"name":"Kate"}│{"name":"Liz"} │
├───────────────┼───────────────┤
│{"name":"Mary"}│{"name":"Ann"} │
├───────────────┼───────────────┤
│{"name":"Bob"} │{"name":"Ann"} │
├───────────────┼───────────────┤
│{"name":"Bob"} │{"name":"Pat"} │
├───────────────┼───────────────┤
│{"name":"Dick"}│{"name":"Jim"} │
├───────────────┼───────────────┤
│{"name":"Ann"} │{"name":"Jim"} │
├───────────────┼───────────────┤
│{"name":"Pat"} │{"name":"Joli"}│
├───────────────┼───────────────┤
│{"name":"Jack"}│{"name":"Joli"}│
└───────────────┴───────────────┘
```

Что ещё мы можем узнать? Например, кто является родителем конкретного члена рода,
например, для Bob'а:

``` cypher
MATCH (parent:Person)-[:PARENT]->(:Person {name: "Bob"})
RETURN parent.name
```

``` plain
╒═════════════╕
│"parent.name"│
╞═════════════╡
│"Tom"        │
├─────────────┤
│"Pam"        │
└─────────────┘
```

Здесь в качестве ответа мы запрашиваем не весь узел, а только его конкретный атрибут.

Также можем узнать, кто дети Bob'а:

``` cypher
MATCH (:Person {name: "Bob"})-[:PARENT]->(child:Person)
RETURN child.name
```

``` plain
╒════════════╕
│"child.name"│
╞════════════╡
│"Ann"       │
├────────────┤
│"Pat"       │
└────────────┘
```

Ещё мы можем поинтересоваться, у кого есть дети:

``` cypher
MATCH (parent:Person)-[:PARENT]->(:Person)
RETURN parent.name
```

``` plain
╒═════════════╕
│"parent.name"│
╞═════════════╡
│"Pam"        │
├─────────────┤
│"Tom"        │
├─────────────┤
│"Tom"        │
├─────────────┤
│"Kate"       │
├─────────────┤
│"Mary"       │
├─────────────┤
│"Bob"        │
├─────────────┤
│"Bob"        │
├─────────────┤
│"Dick"       │
├─────────────┤
│"Ann"        │
├─────────────┤
│"Pat"        │
├─────────────┤
│"Jack"       │
└─────────────┘
```

Хм, Tom и Bob встретились по два раза, исправим это:

``` cypher
MATCH (parent:Person)-[:PARENT]->(:Person)
RETURN DISTINCT parent.name
```

Мы добавили в возвращаемый результат запроса слово `DISTINCT`, по смыслу
аналогичное таковому в SQL.

``` plain
╒═════════════╕
│"parent.name"│
╞═════════════╡
│"Pam"        │
├─────────────┤
│"Tom"        │
├─────────────┤
│"Kate"       │
├─────────────┤
│"Mary"       │
├─────────────┤
│"Bob"        │
├─────────────┤
│"Dick"       │
├─────────────┤
│"Ann"        │
├─────────────┤
│"Pat"        │
├─────────────┤
│"Jack"       │
└─────────────┘
```

Можно также заметить, что Neo4j возвращает нам родителей в порядке их ввода в
запросе `CREATE`.

Давайте теперь спросим, кто является дедушкой или бабушкой:

``` cypher
MATCH (grandparent:Person)-[:PARENT]->()-[:PARENT]->(:Person)
RETURN DISTINCT grandparent.name
```

Отлично, всё так и есть:

``` plain
╒══════════════════╕
│"grandparent.name"│
╞══════════════════╡
│"Tom"             │
├──────────────────┤
│"Pam"             │
├──────────────────┤
│"Bob"             │
├──────────────────┤
│"Mary"            │
└──────────────────┘
```

В шаблоне запроса мы использовали промежуточный безымянный узел `()` и две связи
типа `PARENT`.

Выясним теперь кто является отцом. Отцом является мужчина, у которого есть ребёнок.
Таким образом, нам не хватает данных о том, кто является мужчиной. Соответственно,
для определения, кто является мамой, потребуется знать, кто является женщиной.
Добавим соответствующие сведения в нашу базы данных. Для этого мы присвоим метки
`Male` и `Female` уже существующим узлам.

``` cypher
MATCH (p:Person)
WHERE p.name IN ["Tom", "Dick", "Bob", "Jim", "Jack"]
SET p:Male
```

``` cypher
MATCH (p:Person)
WHERE p.name IN ["Pam", "Kate", "Mary", "Liz", "Ann", "Pat", "Joli"]
SET p:Female
```

Поясним, что мы здесь сделали: мы выбрали все узлы с меткой `Person`, проверили их
свойство `name` по заданному списку, задаваемому в квадратных скобках, и присвоили
подходящим узлам метку `Male` или `Female` соответственно.

Проверим:

``` cypher
MATCH (p:Person) WHERE p:Male
RETURN p.name
```

``` plain
╒════════╕
│"p.name"│
╞════════╡
│"Tom"   │
├────────┤
│"Bob"   │
├────────┤
│"Dick"  │
├────────┤
│"Jack"  │
├────────┤
│"Jim"   │
└────────┘
```

``` cypher
MATCH (p:Person) WHERE p:Female
RETURN p.name
```

``` plain
╒════════╕
│"p.name"│
╞════════╡
│"Pam"   │
├────────┤
│"Kate"  │
├────────┤
│"Mary"  │
├────────┤
│"Liz"   │
├────────┤
│"Ann"   │
├────────┤
│"Pat"   │
├────────┤
│"Joli"  │
└────────┘
```

Мы запросили все узлы с меткой `Person`, у которой есть также метка `Male` или
`Female`, соответственно. Но мы могли бы составить наши запросы несколько иначе:

``` cypher
MATCH (p:Person:Male) RETURN p.name
MATCH (p:Person:Female) RETURN p.name
```

Давайте ещё раз взглянем на наш граф визуально:

![Генеалогическое дерево с метками Male и Female](/images/neo4j-family-tree-male-female.png)

Neo4j Browser раскрасил узлы в два разных цвета в соответствии с метками Male и
Female.

Отлично, теперь мы можем запросить из базы данных всех отцов:

``` cypher
MATCH (p:Person:Male)-[:PARENT]->(:Person)
RETURN DISTINCT p.name
```

``` plain
╒════════╕
│"p.name"│
╞════════╡
│"Tom"   │
├────────┤
│"Bob"   │
├────────┤
│"Dick"  │
├────────┤
│"Jack"  │
└────────┘
```

И матерей:

``` cypher
MATCH (p:Person:Female)-[:PARENT]->(:Person)
RETURN DISTINCT p.name
```

``` plain
╒════════╕
│"p.name"│
╞════════╡
│"Pam"   │
├────────┤
│"Kate"  │
├────────┤
│"Mary"  │
├────────┤
│"Ann"   │
├────────┤
│"Pat"   │
└────────┘
```

Давайте теперь сформулируем отношения брат и сестра. X является братом для Y,
если он мужчина, и для X и Y имеется хотя бы один общий родитель. Аналогично для
отношения сестры.

Отношение брат на Cypher:

``` cypher
MATCH (brother:Person:Male)<-[:PARENT]-()-[:PARENT]->(p:Person)
RETURN brother.name, p.name
```

``` plain
╒══════════════╤════════╕
│"brother.name"│"p.name"│
╞══════════════╪════════╡
│"Bob"         │"Liz"   │
└──────────────┴────────┘
```

Отношение сестра на Cypher:

``` cypher
MATCH (sister:Person:Female)<-[:PARENT]-()-[:PARENT]->(p:Person)
RETURN sister.name, p.name
```

``` plain
╒═════════════╤════════╕
│"sister.name"│"p.name"│
╞═════════════╪════════╡
│"Liz"        │"Bob"   │
├─────────────┼────────┤
│"Ann"        │"Pat"   │
├─────────────┼────────┤
│"Pat"        │"Ann"   │
└─────────────┴────────┘
```

Итак, мы можем узнавать кто чей родитель, а также кто чей дедушка или бабушка. А
как быть с предками более дальними? С прадедушками, прапрадедушками или так далее?
Не будем же мы для каждого такого случая писать соответствующее правило, да и всё
проблематичней это будет с каждым разом. На самом деле всё просто: X является для
Y предком, если он является предком для родителя Y. Cypher предоставляет паттерн
`*`, позволяющий потребовать последовательность связей любой длины:

``` cypher
MATCH (p:Person)-[*]->(s:Person)
RETURN DISTINCT p.name, s.name
```

Есть в этом правда одна проблема: это будут любые связи. Добавим указание на связь
`PARENT`:

``` cypher
MATCH (p:Person)-[:PARENT*]->(s:Person)
RETURN DISTINCT p.name, s.name
```

Чтобы не увеличивать длину статьи, найдём всех предков `Joli`:

``` cypher
MATCH (p:Person)-[:PARENT*]->(:Person {name: "Joli"})
RETURN DISTINCT p.name
```

``` plain
╒════════╕
│"p.name"│
╞════════╡
│"Jack"  │
├────────┤
│"Pat"   │
├────────┤
│"Bob"   │
├────────┤
│"Pam"   │
├────────┤
│"Tom"   │
└────────┘
```

Рассмотрим более сложное правило для выяснения кто кому является родственником.
Во-первых, родственниками являются предки и потомки, например, сын и мать, бабушка
и внук. Во-вторых, родственниками являются братья и сёстры в том числе двоюродные,
троюродные и так далее, что в терминах предков означает, что у них общий предок.
И, в-третьих, родственниками считаются те, у кого общие потомки, например, муж и
жена.

На Cypher для множества паттернов нужно воспользоваться `UNION`:

``` cypher
MATCH (r1:Person)-[:PARENT*]-(r2:Person)
RETURN DISTINCT r1.name, r2.name
UNION
MATCH (r1:Person)<-[:PARENT*]-(:Person)-[:PARENT*]->(r2:Person)
RETURN DISTINCT r1.name, r2.name
UNION
MATCH (r1:Person)-[:PARENT*]->(:Person)<-[:PARENT*]-(r2:Person)
RETURN DISTINCT r1.name, r2.name
```

Здесь, в первом правиле, использованы связи, направление которых нам неважно.
Указывается такая связь без стрелки, просто тире `-`. Второе и третье правило
записаны очевидным, уже знакомым образом.

Мы не будем здесь приводить результат тотального запроса, скажем только то, что
найденных пар родственников 132, что согласуется с вычисленным значением как число
упорядоченных пар из 12. Мы могли бы также конкретизировать данный запрос, заменив
вхождение переменной `r1` или `r2` на `(:Person {name: "Liz"})` к примеру, однако
в нашем случае в этом нет большого смысла, так как все персоны в нашей базе данных
очевидно являются родственниками.

На этом мы закончим рассматривать выявление связей между персонами в нашей базе
данных.

На последок рассмотрим как удалять узлы и связи.

Для удаления всех наших персон, можно выполнить запрос:

``` cypher
MATCH (p:Person) DELETE p
```

Однако, Neo4j нам сообщит, что нельзя удалить узлы, у которых есть связи.
Поэтому удалим сначала связи и затем повторим удаление узлов:

``` cypher
MATCH (p1:Person)-[r]->(p2:Person) DELETE r
```

Что мы сейчас сделали: сопоставили две персоны, между которыми есть связь,
поименовали эту связь как `r` и затем удалили её.

## Заключение

В статье на простом примере социального графа показано, как использовать
возможности языка запросов Cypher. В частности, мы рассмотрели как добавлять узлы
и связи одним запросом, как искать связанные данные, в том числе с непрямыми
связями, как назначать метки узлам. Более подробная информация о языке Cypher может
быть найдена по ссылкам ниже. Хорошей отправной точкой является "Neo4j Cypher
Refcard".

Neo4j далеко не единственная графовая СУБД. В числе других самых популярных
[Cayley](https://www.cayley.io/), [Dgraph](https://dgraph.io/) с языком запросов
GraphQL, мультимодельные [ArangoDB](https://www.arangodb.com/) и
[OrientDB](http://orientdb.com/). Отдельный интерес может представлять
[Blazegraph](https://www.blazegraph.com/) с поддержкой RDF и SPARQL.

## Ссылки

- [Neo4j: An Introduction to Cypher](https://neo4j.com/developer/cypher-query-language/)
- [Neo4j Cypher Refcard](https://neo4j.com/docs/cypher-refcard/current/)
- [openCypher](http://www.opencypher.org/)

## Библиография

- Робинсон Ян, Вебер Джим, Эифрем Эмиль. Графовые базы данных. Новые возможности
  для работы со связанными данными / пер. с англ. – 2-е изд. – М.: ДМК-Пресс,
  2016 – 256 с.
- Братко И. Программирование на языке Пролог для искусственного интеллекта:
  пер. с англ. – М.: Мир, 1990. – 560 с.: ил.

## Примечания

Эта статья впервые была опубликована мною на
[Habr.com](https://habr.com/ru/post/482418/) 29 декабря 2019. В основу же самой
статьи легло моё исследование
[Введение в язык запросов Cypher с параллельным кодом на Prolog](https://github.com/easimonenko/research-work/blob/master/graph-databases/cypher-intro.md),
опубликованное 7 февраля 2018.

К посту на Habr.com было размещено голосование, в котором нужно было выбрать один
из вариантов. "Вопрос звучал так: Используется ли в вашей компании какая-либо
графовая СУБД?" Ответы распределились слудующим образом:

1. 32,4% -- не обсуждали, но в курсе, что есть такие СУБД
1. 24,3% -- используется в разрабатываемом нами ПО
1. 18,9% -- не используется, но думаем, чтобы внедрить
1. 18,9% -- не используется; думали об этом и решили не применять
1. 5,4% -- не знали, что есть такое
1. 0,0% -- используется в стороннем ПО

(Количество проголосовавших на момент публикации этого поста 37 пользователей.)

18 апреля 2022 года расклад по голосованию в опросе такой:

1. 31,8% -- не обсуждали, но в курсе, что есть такие СУБД
1. 25,0% -- используется в разрабатываемом нами ПО
1. 20,5% -- не используется, но думаем, чтобы внедрить
1. 15,9% -- не используется; думали об этом и решили не применять
1. 6,8% -- не знали, что есть такое
1. 0,0% -- используется в стороннем ПО

Проголосовали 44 пользователя. Воздержались 16 пользователей.

За почти два года проголосоваших прибавилось немного. Делать выводы об изменении
позиций графовых СУБД и о росте интереса к ним сложно.

(c) Симоненко Евгений, 2018, 2019, 2020
