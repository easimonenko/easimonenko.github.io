---
layout: project
title: C2 Mode
date: 2025-02-25 17:24 +0000
name: c2-mode
link: https://github.com/easimonenko/c2-mode
short: Режим GNU Emancs для редактирования кода, написанного на языке C2.
author: Evgeny Simonenko
email: easimonenko@gmail.com
status: active
---

[![MELPA](https://melpa.org/packages/c2-mode-badge.svg)](https://melpa.org/#/c2-mode)

Проект по разработке режима _GNU Emacs_ для редактирования кода, написанного на языке [C2](http://c2lang.org).

Проект начат в конце февраля 2025. [Подана](https://github.com/melpa/melpa/pull/9374) и [одобрена](https://melpa.org/#/c2-mode) заявка на добавление пакета в MELPA.

Реализованы:

- синтаксическая подсветка (неполностью, используется `cc-mode`);
- правильные отступы (полностью);
- настройки (<kbd>M</kbd>+<kbd>x</kbd> `customize-group` `c2`):
  - ширина отступа `c2-indent-offset`.
  
В планах:

- [ ] Добавить автопроверку кода с использованием компилятора c2c и Flymake, Flycheck.
- [ ] Исправить подсветку для комментариев (код написан, но почему-то не работает).
- [ ] Реализовать подсветку для атрибутов (начинаются с @).
- [ ] Реализовать подсветку для директив (начинаются с #).
