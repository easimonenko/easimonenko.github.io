---
layout: post
title: Добавил на сайт раздел "Проекты"
author: Evgeny Simonenko
email: easimonenko@gmail.com
date: 2022-01-24 22:55
category: Site News
tags: Jekyll
---

Добавил раздел ["Проекты"](/projects/) для публикации информации о своих актуальных проектах. Давно хотел реализовать такую штуку. Но как? Было неочевидно. День работы и всё получилось. Теперь вкратце расскажу как это было сделано.

![Меню сайта с разделом "Проекты"](/images/projects-section.png)

<!-- end-of-lead -->

Из документации на [Jekyll](https://jekyllrb.com/docs/) стало понятно, что в этом мне помогут так называемые [коллекции](https://jekyllrb.com/docs/collections/). Это концепция Jekyll для группировки сходных по смыслу сущностей. В нашем случае это проекты. Коллекции декларируются в `_config.yml`:

``` yaml
collections:
  projects:
    output: true
    title: Projects
```

Далее, создаём директорию для файлов, в которых будут описываться данные и контент сущностей коллекции. Имя директории должно начинаться с подчёркивания `_` и далее называться так, как называется коллекция. В нашем случае `_projects`. На каждый элементы коллекции заводим отдельный файл. Опция `output` говорит Jekyll генерировать из этих файлов страницы.

Наконец, создаём страницу для списка всех проектов и соответствующий раздел на главной. Все коллекции доступны через объект `site`. Коллекция для проектов будет доступна под `site.projects`. Остальное дело техники, то есть пишем обычный код на [Liquid](https://jekyllrb.com/docs/liquid/).

Подробности смотри в [исходниках](https://github.com/easimonenko/easimonenko.github.io) этого блога, а также в репозитории [шаблона](https://github.com/easimonenko/jekyll-template-for-a-personal-website), куда я помещаю все свои находки.

(c) Симоненко Евгений, 2022