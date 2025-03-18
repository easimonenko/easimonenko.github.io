---
layout: project
title: Mybuild Mode
name: mybuild-mode
link: https://github.com/easimonenko/mybuild-mode
short: Режим GNU Emancs для редактирования файлов Mybuild из ОС Embox.
author: Evgeny Simonenko
date: 2022-09-07 16:24
status: active
updating_date: 2022-09-25 14:39
---

[![MELPA](https://melpa.org/packages/mybuild-mode-badge.svg)](https://melpa.org/#/mybuild-mode)
[![MELPA Stable](https://stable.melpa.org/packages/mybuild-mode-badge.svg)](https://stable.melpa.org/#/mybuild-mode)

Проект по разработке режима _GNU Emacs_ для редактирования файлов _Mybuild_
из операционный системы [Embox](https://embox.github.io/).

Проект начат в августе 2022. 11 сентября [пакет](https://melpa.org/#/mybuild-mode)
для `mybuild-mode` был [принят в MELPA](https://github.com/melpa/melpa/pull/8188).

Реализованы:
- синтаксическая подсветка (полностью, используется `font-lock-mode`);
- правильные отступы (полностью);
- настройки (<kbd>M</kbd>+<kbd>x</kbd> `customize-group` `mybuild`):
  - ширина отступа `mybuild-indent-offset`.

В планах:
- [x] Избавиться от `c-mode`, так как 1) замедляет загрузку режима; 2) делает неправильные
  отступы для простых инструкций (`c-mode` ожидает, что в конце инструкции будет `;`).
  Для этого нужно написать функцию, которая будет делать правильные отступы.
- [ ] Автодополнение для имён пакетов и модулей.
- [ ] Проверка правильности синтаксиса.

Первое в приоритете. Вторые два пункта постольку-поскольку, так как весьма сложны в реализации.
