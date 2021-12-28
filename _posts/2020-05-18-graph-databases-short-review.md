---
layout: post
title: Краткий обзор свободно-распространяемых графовых СУБД
author: Evgeny Simonenko
email: easimonenko@gmail.com
date: 2020-05-18 22:36
category: Research Work
tags: [Graph Databases, Databases]
---

На сегодняшний день графовых СУБД стало настолько много, что аж глаза разбегаются.
Они написаны на различных языках, предлагают различные языки запросов, некоторые
не ограничиваются одной только графовой моделью. Давайте пройдёмся по наиболее
популярным и известным, свободно-распространяемым из них. Сначала мы рассмотрим
полноценные СУБД, а затем -- встраиваемые.

<!-- end-of-lead -->

_Сначала полноценные СУБД в порядке числа звёзд на GitHub._

| # | Name | Repository | Stars | Language | License | Last Commit | Created |
|-|-|-|-|-|-|-|-|
| 1 | [Cayley](https://cayley.io) | [cayleygraph/cayley](https://github.com/cayleygraph/cayley) | 13358 | Go | Apache License 2.0 | 2020-04-30 | 2014-06-05 |
| 2 | [Dgraph](https://dgraph.io) | [dgraph-io/dgraph](https://github.com/dgraph-io/dgraph) | 13095 | Go | Other | 2020-05-05 | 2015-08-25 |
| 3 | [ArangoDB](https://www.arangodb.com) | [arangodb/arangodb](https://github.com/arangodb/arangodb) | 9510 | C++ | Apache License 2.0 | 2020-05-05 | 2011-10-26 |
| 4 | [Neo4j](http://neo4j.com) | [neo4j/neo4j](https://github.com/neo4j/neo4j) | 7683 | Java |  | 2020-05-04 | 2012-11-12 |
| 5 | [Titan](http://titandb.io) | [thinkaurelius/titan](https://github.com/thinkaurelius/titan) | 5035 | Java | Apache License 2.0 | 2015-12-03 | 2012-02-26 |
| 6 | [OrientDB](http://orientdb.com) | [orientechnologies/orientdb](https://github.com/orientechnologies/orientdb) | 4131 | Java | Apache License 2.0 | 2020-05-05 | 2012-12-10 |
| 7 | [JanusGraph](https://janusgraph.org) | [JanusGraph/janusgraph](https://github.com/JanusGraph/janusgraph) | 3288 | Java | Other | 2020-05-02 | 2016-12-26 |
| 8 | FlockDB | [twitter-archive/flockdb](https://github.com/twitter-archive/flockdb) | 3227 | Scala | Other | 2017-03-17 | 2010-04-12 |
| 9 | [NebulaGraph](https://nebula-graph.io) | [vesoft-inc/nebula](https://github.com/vesoft-inc/nebula) | 2802 | C++ | Apache License 2.0 | 2020-04-30 | 2018-08-28 |
| 10 | [Grakn](https://grakn.ai) | [graknlabs/grakn](https://github.com/graknlabs/grakn) | 2047 | Java | GNU Affero General Public License v3.0 | 2020-05-05 | 2016-07-12 |
| 11 | HugeGraph | [hugegraph/hugegraph](https://github.com/hugegraph/hugegraph) | 1175 | Java | Apache License 2.0 | 2020-04-24 | 2018-07-18 |
| 12 | [AgensGraph](http://www.agensgraph.org) | [bitnine-oss/agensgraph](https://github.com/bitnine-oss/agensgraph) | 942 | C | Other | 2020-01-25 | 2016-04-29 |
| 13 | [Virtuoso](http://virtuoso.openlinksw.com/dataspace/dav/wiki/Main/) | [openlink/virtuoso-opensource](https://github.com/openlink/virtuoso-opensource) | 628 | C | Other | 2020-01-20 | 2012-03-21 |
| 14 | TerminusDB | [terminusdb/terminus-server](https://github.com/terminusdb/terminus-server) | 504 | Prolog | GNU General Public License v3.0 | 2020-04-29 | 2019-07-23 |
| 15 | Blazegraph | [blazegraph/database](https://github.com/blazegraph/database) | 473 | Java | GNU General Public License v2.0 | 2019-03-19 | 2015-12-22 |
| 16 | VertexDB | [stevedekorte/vertexdb](https://github.com/stevedekorte/vertexdb) | 288 | C | Other | 2018-01-21 | 2009-06-29 |
| 17 | HGraphDB | [rayokota/hgraphdb](https://github.com/rayokota/hgraphdb) | 201 | Java | Apache License 2.0 | 2020-05-05 | 2016-11-09 |

## Cayley

- версия: 0.7.7
- в качестве языков запросов доступны JavaScript и
  [MQL](https://ru.wikipedia.org/wiki/MQL)
- в качестве движков хранения данных использует другие СУБД
- сайт с документацией пуст, есть документация среди исходников на GitHub
- предлагает несколько вариантов для хранения данных, используя другие СУБД

## Dgraph

- версия: 1.2.3 и 20.03.1
- язык запросов GraphQL
- лицензия: Apache 2.0 и собственная

## ArangoDB

- версия: 3.6.3.1
- язык запросов [AQL](https://docs.arangodb.com/latest/AQL/index.html)
- хорошая документация
- есть пакеты для многих операционных систем
- веб-интерфейс с графическим редактором

## Neo4j

- версия: 3.5.16 и 4.0.3
- язык запросов [Cypher](http://www.opencypher.org/)
- ~~дополнительно поддерживается язык
  [Gremlin](https://neo4j-contrib.github.io/gremlin-plugin/)~~ (в версии 3
  поддержка полностью удалена; потребуется
  [Gremlin Server](http://tinkerpop.apache.org/))
- дополнительно поддерживается язык
  [GraphQL](https://github.com/neo4j-contrib/neo4j-graphql)
- дополнительно поддерживается язык
  [SPARQL](https://github.com/neo4j-contrib/sparql-plugin)
- легко установить и легко запустить
- веб-интерфейс с графическим редактором
- краткий курс для ознакомления, встроенный в веб-интерфейс
- лицензия: GPLv3 (community) или AGPLv3 (enterprise)

## Titan

- версия: 1.0.0
- поддерживается язык [Gremlin](https://tinkerpop.apache.org/) как основное
  средство работы с базой данных
- в качестве движков хранения данных использует другие СУБД
- _не обновляется с 2015 года_

## OrientDB

- версия: 3.0.31
- в качестве основного языка запросов используется расширенный
  [SQL](http://orientdb.com/docs/last/SQL.html)

## JanusGraph

- версия: 0.5.2
- лицензия: Apache 2.0

## FlockDB

- версия: 1.8.5
- _не поддерживается, новые версии не выходят с 2012 года_
- _не обновляется с 2017 года_
- требуется сборка из исходников
- лицензия: Apache 2.0

## NebulaGraph

- версия: 1.0.0-RC4

## Grakn

- версия: 1.7.1

## HugeGraph

- версия: 0.10.4

## AgensGraph

- версия: 2.1.2
- базируется на PostgreSQL
- в качестве языков запросов доступны SQL и Cypher
- требует сборки из исходных текстов
- лицензия: Apache 2.0

## Virtuoso

- версия: 7.2.5.1

## TerminusDB

- версия: 1.1.3

## Blazegraph

- версия: 2.1.6
- поддержка RDF/SPARQL: есть
- поддержка Apache TinkerPop: есть

## VertexDB

- требует сборки из исходных текстов
- _нет выпусков на GitHub_
- _не обновляется с 2018 года_
- лицензия: BSD

## HGraphDB

- версия: 3.0.0

_Теперь движки для встраивания._

| # | Name | Repository | Stars | Language | License | Last Commit | Created |
|-|-|-|-|-|-|-|-|
| 1 | [GraphEngine](https://www.graphengine.io/) | [microsoft/GraphEngine](https://github.com/microsoft/GraphEngine) | 1855 | C# | Other | 2019-11-13 | 2017-02-09 |
| 2 | [Tinkerpop](https://tinkerpop.apache.org/) | [apache/tinkerpop](https://github.com/apache/tinkerpop) | 1097 | Java | Apache License 2.0 | 2020-04-29 | 2015-02-07 |
| 3 | [RedisGraph](https://redisgraph.io) | [RedisGraph/RedisGraph](https://github.com/RedisGraph/RedisGraph) | 1010 | C | Other | 2020-05-05 | 2017-03-09 |
| 4 | Morpheus | [opencypher/morpheus](https://github.com/opencypher/morpheus) | 270 | Scala | Apache License 2.0 | 2019-10-16 | 2016-08-02 |
| 5 | Bitsy | [lambdazen/bitsy](https://github.com/lambdazen/bitsy) | 82 | Java | Apache License 2.0 | 2020-03-06 | 2017-03-16 |

## GraphEngine

- не является СУБД, это движок для .Net и Visual Studio
- _нет выпусков на GitHub_
- лицензия: MIT

## Tinkerpop

- версия: 3.4.6
- это скорее язык запросов к графовым СУБД, нежели движок

## RedisGraph

- версия: 2.0.11
- является модулем для Redis
- требует сборки из исходных текстов
- лицензия: Redis Source Available License

## Redis Graph (obsolete)

- <http://redisgraph.io/>
- <https://github.com/swilly22/redis-graph>
- 405 звёзд на GitHub
- написана на C
- является модулем для Redis
- требует сборки из исходных текстов
- _нет выпусков на GitHub_
- не видно активной разработки с июня 2018
- репозиторий заархивирован, автор рекомендует
  <https://github.com/RedisGraph/RedisGraph>
- лицензия: AGPL 3.0

## Morpheus (Cypher for Apache Spark)

- <https://github.com/opencypher/morpheus>
  (ранее <https://github.com/opencypher/cypher-for-apache-spark>)
- версия: 0.4.2
- является дополнением к Apache Spark

## Bitsy v3

- версия: 3.2.2
- встраиваемая СУБД

## Bitsy v2

- <https://bitbucket.org/lambdazen/bitsy/wiki/Home>
- <https://bitbucket.org/lambdazen/bitsy>
- написана на Java
- встраиваемая СУБД
- _не обновляется с 2016 года_
- лицензия: Apache 2.0

## Примечание

Этот пост базируется на соответствующем исследовании, проведённом в 2017 году и
опубликованном в моём репозитории с исследовательскими материалами. Ссылка на
оригинал:

<https://github.com/easimonenko/research-work/blob/master/graph-databases/graph-databases-short-review.md>

Таблицы сгенерированы с использованием скриптов, которые доступны в том же
репозитории: <https://github.com/easimonenko/research-work/tree/master/scripts>

(c) Симоненко Евгений, 2017-2020
