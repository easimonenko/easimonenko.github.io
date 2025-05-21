---
layout: post
title: Создание режима GNU Emacs для C-подобного языка
date: 2025-05-20 17:30 +0000
author: Evgeny Simonenko
email: easimonenko@gmail.com
category: Tutorial
tags: [GNU Emacs, Emacs Lisp, C2]
---

Недавно я разработал ещё один [режим](https://github.com/easimonenko/c2-mode) [GNU Emacs](https://www.gnu.org/software/emacs/) для C-подобного языка программирования [C2](http://c2lang.org/). Если в предыдущий раз для другого C-подобного языка я написал [код](https://github.com/easimonenko/mybuild-mode) с нуля, то в этот раз решил воспользоваться возможностью так называемого наследования режимов. В этой статье хочу поделиться с вами как это делается, и что у меня из этого вышло. (Предполагается, что читатель ознакомился с материалом предыдущей статьи [Как написать свой режим для GNU Emacs и опубликовать его в MELPA]({% post_url  2023-08-18-how-to-write-your-own-mode-for-gnu-emacs-and-publish-it-in-melpa %}) или имеет собственный уникальный опыт разработки режимов GNU Emacs.)

![Обложка с фрагментом кода режима](/images/creating-gnu-emacs-mode-for-a-c-like-language-cover.png)

<!-- end-of-lead -->

## Введение

Как рассказывалось в предыдущей статье, я уже пытался использовать наследование режимов для C-подобного языка. Однако в тот раз из этого ничего хорошего не вышло. Основная причина была в том, что тот язык не использовал символ точки с запятой в качестве признака завершения некоторых конструкций, что приводило к неверной расстановке отступов при переходе на новую строку. Тогда мне пришлось сделать полное описание синтаксиса языка и написать ту самую функцию, обеспечивавшую правильность отступов.

Язык C2 позиционируется как эволюция языка C. Наиболее заметным отличием является отказ от препроцессора с его `#include` и `#define`. Есть и другие новшества, за которыми отсылаю читателя к [документации](http://c2lang.org/site/). Также рекомендую обратиться к примерам кода и тестам в коде его [компилятора](https://github.com/c2lang/c2compiler).

Язык C2 сохранил обязательность точки с запятой, что вселяло надежду на быструю реализацию режима GNU Emacs. Однако, оказалось, что следующая простая конструкция работает, но не так как надо:

``` elisp
;;;###autoload
(define-derived-mode c2-mode c-mode "C2"
  "Major mode for editing code written in the C2 Programming Language.")
```

Проблема была в том, что в этом случае файлы C2 воспринимаются как файлы C! Соответствено и обрабатываются они как файлы C, и все режимы настроенные для C будут запускаться для C2. А значит мы увидим море проблем и ложных сообщений об ошибках в коде на C2. Непорядок!

Тогда я решил ознакомиться с кодом режимов для других C-подобных языков, чтобы разобраться, а как они были реализованы? Вот эти языки и их режимы: [D](https://github.com/Emacs-D-Mode-Maintainers/Emacs-D-Mode), [Dart](https://github.com/emacsorphanage/dart-mode), [C#](https://github.com/emacs-csharp/csharp-mode), [Go](https://github.com/dominikh/go-mode.el), [JavaScript](https://github.com/mooz/js2-mode), [Kotlin](https://github.com/Emacs-Kotlin-Mode-Maintainers/kotlin-mode), [Rust](https://github.com/rust-lang/rust-mode). Смотрел также в код встроенных режимов для C++, Java, Perl. И оказалось всё очень неоднозначно! Во-первых, лишь часть режимов использовали это самое наследование от C. Во-вторых, это наследование -- ну такое...

В общем, пришлось мне изрядно попотеть. Ещё одну проблему подбрасывал сам C2. Оказалось, что для него нет грамматики! А значит за описанием его конструкций нужно идти в документацию. Анализ примеров из кода компилятора навёл на мысль, что между документацией и тестами есть расхождение... Ну да ладно.

## Структура кода режима

Рассказ будет вестись с примерами [кода](https://github.com/easimonenko/c2-mode/blob/main/c2-mode.el) из написанного мною режима.

В самом начале кода режима производим загрузку необходимых модулей:

``` elisp
(require 'cc-bytecomp)
(require 'cc-fonts)
(require 'cc-langs)
(require 'cc-mode)
(require 'compile)

(eval-when-compile
  (let ((load-path (if (and (boundp 'byte-compile-dest-file)
                            (stringp byte-compile-dest-file))
                       (cons (file-name-directory byte-compile-dest-file)
                             load-path)
                     load-path)))
    (load "cc-mode" nil t)
    (load "cc-fonts" nil t)
    (load "cc-langs" nil t)
    (load "cc-bytecomp" nil t)))
```

И объявляем наш режим как наследник режима c-mode:

``` elisp
(eval-and-compile
  (c-add-language 'c2-mode 'c-mode))
```

На время пропустим последующий код и перейдём в его конец. Как обычно, основная часть кода режима заключается в следующих строках:

``` elisp
;;;###autoload
(define-derived-mode c2-mode prog-mode "C2"
  "Major mode for editing code written in the C2 Programming Language.

  Key bindings:
  \\{c2-mode-map}"
  :after-hook (c-update-modeline)
  (c-initialize-cc-mode t)
  (use-local-map c2-mode-map)
  (c-init-language-vars c2-mode)
  (c-common-init 'c2-mode)
  (c-run-mode-hooks 'c-mode-common-hook)
  (setq-local comment-start "// "
              comment-end ""
              block-comment-start "/*"
              block-comment-end "*/"))

;;;###autoload
(add-to-list 'auto-mode-alist '("\\.\\(c2\\|c2i\\|c2t\\)\\'" . c2-mode))

(provide 'c2-mode)
```

Здесь в `define-derived-mode` создаётся новый режим, именуемый в коде `c2-mode`, наследуемый от `prog-mode`, имеющий название `C2`, которое будет отображаться в mode line, и строка документации со включением описания привязок к клавишам, которое описывается в переменной `c2-mode-map`:

``` elisp
(defvar c2-mode-map () "Keymap for C2 mode buffers.")
(if c2-mode-map nil (setq c2-mode-map (c-make-inherited-keymap)))
```

Я не стал добавлять никаких дополнительных комбинацией клавиш, а просто наследую их вызовом `c-make-inherited-keymap`.

Вернёмся к `define-derived-mode` и продолжим разбирать код построчно.

``` elisp
:after-hook (c-update-modeline)
```

`c-update-modeline` будет вызвано после срабатывания всех hook режима. Как я понял из кода, эта недокументированная функция настраивает mode line для нашего режима.

Вызов `(c-initialize-cc-mode t)` по-сути осуществляет то самое наследование от cc-mode, базового режима для C-подобных языков. Эта функция инициализирует cc-mode для текущего буфера. Опциональный параметр указывает, что нам нужна только базовая инициализация, а остальное мы сделаем сами.

Вызов `(use-local-map c2-mode-map)` задаёт для нашего режима клавиатурные комбинации, описанные раннее в переменной `c2-mode-map`.

Макрос `(c-init-language-vars c2-mode)` инициализирует для нашего режима все необходимые переменные.

Вызов `(c-common-init 'c2-mode)` выполняет инициализацию дополнительных возможностей для нашего режима. Внутри себя вызывает `c-basic-common-init`, выполняющую базовую инициализацию режима.

Вызов `(c-run-mode-hooks 'c-mode-common-hook)` вызывает общий hook для cc-mode.

В коде ниже настраивается подсветка комментариев:

``` elisp
(setq-local comment-start "// "
            comment-end ""
            block-comment-start "/*"
            block-comment-end "*/")
```

Но, как и следующий код, это не дало должного эффекта. Я так и не смог заставить cc-mode обрабатывать комментарии как комментарии. Хотя подобный код присутствовал в референсных режимах.

``` elisp
(c-lang-defconst c-block-comment-starter c2 "/*")
(c-lang-defconst c-block-comment-ender c2 "*/")
(c-lang-defconst c-comment-start-regexp c2 "/[*+/]")
(c-lang-defconst c-block-comment-start-regexp c2 "/[*+]")
(c-lang-defconst c-line-comment-starter c2 "//")
```

В следующей строке, как обычно, происходит связывание режима с определёнными расширениями имён файлов:

``` elisp
;;;###autoload
(add-to-list 'auto-mode-alist '("\\.\\(c2\\|c2i\\|c2t\\)\\'" . c2-mode))
```

Наконец, экспортируем наш режим:

``` elisp
(provide 'c2-mode)
```

### Декларация синтаксических элементов

Вернёмся к пропущенному коду.

``` elisp
(defvar c-syntactic-element)
```

`c-syntactic-element` хранит синтаксические элементы и как-то используется внутри cc-mode.

``` elisp
(declare-function c-populate-syntax-table "cc-langs.el" (table))
```

`c-populate-syntax-table` содержит код обработки синтаксиса C-подобных языков, в частности для комментариев (!). Спрашивается, а что ж оно тогда не работает-то?

Далее идёт серия использования макроса `c-lang-defconst`, с помощью которого декларируются ключевые слова языка и прочие синтаксические элементы, такие как операторы.

``` elisp
(c-lang-defconst c-identifier-ops c2 '((left-assoc ".")))
```

Оператор точка объявляется левоассоциативным.

Дальше идёт описание всех ключевых слов для правильной интерпретации и подсветки. Не буду подробно комментировать, здесь довольно понятно, хотя и не всегда очевидно.

``` elisp
(c-lang-defconst c-ref-list-kwds
  c2 '("import" "local" "module"))

(c-lang-defconst c-protection-kwds
  c2 '("public"))

(c-lang-defconst c-constant-kwds
  c2 '("false" "true" "nil"))

(c-lang-defconst c-primitive-type-kwds
  c2 '("bool" "char" "f32" "f64" "i8" "i16" "i32" "i64" "isize" "u8" "u16" "u32" "u64" "usize" "void"))

(c-lang-defconst c-decl-start-kwds
  c2 '("fn" "module" "type"))

(c-lang-defconst c-type-prefix-kwds
  c2 '("enum" "struct" "union"))

(c-lang-defconst c-class-decl-kwds
  c2 '("enum" "struct" "union"))

(c-lang-defconst c-typedef-decl-kwds
  c2 '("type"))

(c-lang-defconst c-brace-list-decl-kwds
  c2 '("enum"))

(c-lang-defconst c-modifier-kwds
  c2 '("const" "local" "volatile"))

(c-lang-defconst c-block-stmt-1-kwds
  c2 '("as" "case" "do" "else"))

(c-lang-defconst c-block-stmt-2-kwds
  c2 '("for" "if" "sswitch" "switch" "while"))

(c-lang-defconst c-simple-stmt-kwds
  c2 '("assert" "break" "continue" "default" "elemsof" "fallthrough" "return" "sizeof" "static_assert"))

(c-lang-defconst c-paren-type-kwds
  c2 '("cast"))

(c-lang-defconst c-decl-hangon-kwds
  c2 '("as" "local"))

(c-lang-defconst c-paren-nontype-kwds
  c2 '("assert" "elemsof" "sizeof" "static_assert"))

(c-lang-defconst c-paren-stmt-kwds
  c2 '("for" "if" "sswitch" "swtich" "while"))

(c-lang-defconst c-label-kwds
  c2 '("case" "default"))

(c-lang-defconst c-before-label-kwds
  c2 '("goto"))

(c-lang-defconst c-return-kwds
  c2 '("return"))
```

Перечисляем операторы присваивания:

``` elisp
(c-lang-defconst c-assignment-operators
  c2 '("=" "*=" "/=" "%=" "+=" "-=" "<<=" ">>=" "&=" "^=" "|="))
```

Описываем операторы (здесь тоже всё довольно понятно):

``` elisp
(c-lang-defconst c-operators
  c2 `(
       (left-assoc ".")
       (postfix "(" ")" "[" "]" "++" "--")
       (prefix "!" "-" "~" "*" "&" "++" "--")
       (infix "." "*" "/" "%" "<<" ">>" "^" "|" "&" "+" "-")
       (infix "==" "!=" ">=" "<=" ">" "<" "&&" "||")
       (ternary "?:")
       (infix "=" "*=" "/=" "%=" "+=" "-=" "<<=" ">>=" "&=" "^=" "|=")
       (infix ",")))
```

Описываем операторы-скобки и звёздочку:

``` elisp
(c-lang-defconst c-opt-type-suffix-key
  c2 (concat "\\(\\[" (c-lang-const c-simple-ws) "*\\]\\|\\*\\)"))
```

Описываем уровни подсветки, чтобы управлять скоростью и качеством:

``` elisp
(defconst c2-font-lock-keywords-1 (c-lang-const c-matchers-1 c2)
  "Minimal highlighting for C2 mode.")
(defconst c2-font-lock-keywords-2 (c-lang-const c-matchers-2 c2)
  "Fast normal highlighting for C2 mode.")
(defconst c2-font-lock-keywords-3 (c-lang-const c-matchers-3 c2)
  "Accurate normal highlighting for C2 mode.")
(defvar c2-font-lock-keywords c2-font-lock-keywords-3
  "Default expressions to highlight in C2 mode.")
```

Фух! Код режима закончился.

## Заключение 

Лёгкой прогулки не вышло. Как обычно сложность кода перенесли из одного места в другое. Не знаю, стоит ли использовать этот подход для очередного C-подобного языка или нет. Вот разработчики rust-mode написали весь код с нуля. А ещё есть [SMIE](https://github.com/emacs-mirror/emacs/blob/master/lisp/emacs-lisp/smie.el) и [Tree Sitter](https://github.com/emacs-mirror/emacs/blob/master/lisp/treesit.el). Так что не прощаемся, я думаю...

(c) Симоненко Евгений, 2025
