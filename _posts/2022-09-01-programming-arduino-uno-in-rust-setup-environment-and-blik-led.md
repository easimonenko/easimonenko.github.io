---
layout: post
title: "Программируем Arduino Uno на Rust: настраиваем среду и моргаем светодиодом"
author: Evgeny Simonenko
date: 2022-09-01 18:22
category: Tutorial
tags: [Rust, GNU Emacs, Visual Studio Code, Arduino]
---

Полгода назад я вёл в Телеграме канал о языке _Rust_. Канал я закрыл, и сделал выжимку из
материалов, опубликованных в нём. Здесь я расскажу о том, как настроить среду разработчика
на Rust в _Linux_, _GNU Emacs_ и _Visual Studio Code_ и как запрограммировать _Arduino Uno_
на моргание светодиодом.

``` rust
#![no_std]
#![no_main]

use ruduino::Pin;
use ruduino::cores::current::{port};

#[no_mangle]
pub extern fn main() {
    port::B5::set_output();

    loop {
        port::B5::set_high();
        ruduino::delay::delay_ms(1000);
        port::B5::set_low();
        ruduino::delay::delay_ms(1000);
    }
}
```

<!-- end-of-lead -->

Итак, у нас есть Arduino Uno, компьютер с Ubuntu Linux, GNU Emacs (и/или Visual Studio Code).
И мы хотим написать код на Rust, который будет моргать встроенным в плату
светодиодом (LED Blink). Но сначала нужно настроить среду разработки.
Нам потребуется установить инструментарий Rust, LSP-сервер, настроить GNU Emacs.
Также посмотрим как с поддержкой Rust в VS Code.

## Устанавливаем Rust

Точкой входа в мир Rust служит страница на сайте языка
<https://www.rust-lang.org/learn/get-started> Здесь мы узнаем, как установить Rust,
используя утилиту _rustup_. Здесь же рассказывается, как создать проект и запустить
приложение. Установщик создаёт в домашнем каталоге две директории:
`.cargo` для инструментария Rust и `.rustup` для служебной информации rustup.
Для изучения Rust отдадим предпочтение стабильной версии компилятора, но для установки
также доступна ночная сборка.

После установки нам доступны следующие программы:
- `cargo`: менеджер пакетов и проектов на языке Rust
- `cargo-clippy`: инструмент проверки кода на ошибки (линтер)
- `cargo-fmt`: форматирует файлы проекта на Rust, используя rustfmt
- `cargo-miri`: интерпретатор промежуточного кода
- `clippy-driver`: линтер clippy
- `rls`: сервер языка Rust
- `rust-gdb`: отладчик на основе GDB (нужно отдельно установить gdb)
- `rust-lldb`: отладчик на основе LLDB (нужно отдельно установить lldb с llvm)
- `rustc`: компилятор языка Rust
- `rustdoc`: генератор документации проекта на Rust
- `rustfmt`: форматер кода на Rust
- `rustup`: установщик и средство управления инструментами языка Rust

**Предупреждение:** RLS официально
[объявлен устаревшим](https://blog.rust-lang.org/2022/07/01/RLS-deprecation.html),
и вместо него должен использоваться [rust-analyzer](https://rust-analyzer.github.io/).

## Настраиваем GNU Emacs

В качестве основной среды разработки я использую GNU Emacs. Команда Rust разрабатывает
официальный пакет для Emacs `rust-mode`. Но есть и аналог интегрированный среды
[**Rustic**](https://github.com/brotzeit/rustic). Этот пакет не требует никакой настройки,
и из коробки предоставляет массу удобностей. С него и начнём.

Ставим `rustic` обычным образом из репозитория MELPA и прописываем его инициализацию
при запуске Emacs в `~/.emacs.d/init.el`:

- если используем пакет `use-package`:

``` lisp
(use-package rustic)
```

- если используем стандартный метод подключения пакетов:

``` lisp
(require 'rustic)
```

Для создания проекта вызываем команду `rustic-cargo-init`, которая запросит у нас, где создать
проект (поэтому сначала заготовьте для него новую пустую директорию).

Команда `rustic-cargo-new`, которая по идее должна также запросить название проекта и создать
для него директорию, не сработала.

При попытке открыть файл на Rust `./hello_rust/src/main.rs` получим ошибку запуска LSP-сервера
`rls`. Для более подробной информации заглядывем в буфер `*rls::stderr*` и видим сообщение о том,
что `rls` не установлен (хотя команда такая есть). Проверяем в командной строке:

``` shell
rls --version
```

Действительно, та же самая ошибка:

``` plain
error: 'rls' is not installed for the toolchain 'stable-x86_64-unknown-linux-gnu'
To install, run `rustup component add rls`
```

Так и поступим:

``` shell
rustup component add rls
```

Повторяем проверку версии `rls` и теперь получаем то, что нужно:

``` plain
rls 1.41.0 (bf88026 2021-09-07)
```

Закрываем буфер с `main.rs` и снова его открываем: теперь всё хорошо, LSP-сервер запустился,
интерфейс редактора изменился.

Для запуска программы вызываем команду `rustic-cargo-run` и ничего не видим:
почему-то консольный вывод нашей программы не отображается...

Но можно запустить напрямую в консоли. Для этого откроем её прямо в Emacs:
запускаем встроенную оболочку `eshell` и вызываем в открывшейся консоли команду

``` shell
cargo run
```

Теперь наш `Hello, world!` на экране.

### Управление пакетами Cargo в GNU Emacs

Проекты на Rust управляются утилитой _Cargo_, которая конфигурируется файлами в формате
[**TOML**](https://ru.wikipedia.org/wiki/TOML). Для работы LSP-клиента GNU Emacs нам потребуется
LSP-сервер для TOML [taplo](https://github.com/tamasfe/taplo). Установим его:

``` shell
cargo install taplo-lsp
```

Сборка прервалась с ошибкой: не найдена библиотека `openssl`. Установим её:

``` shell
sudo apt install libssl-dev
```

и запустим сборку заново.

И снова ошибка, теперь уже в коде на Rust пакета `taplo-lsp`
(все зависимости собрались без вопросов):


``` shell
error[E0599]: no method named `about` found for struct `Arg` in the current scope
```

На это уже с месяц назад был заведён [ишью](https://github.com/tamasfe/taplo/issues/197).
Опытные товарищи подсказывают там, что сборку нужно запускать с опцией `--locked`.
И это сработало, сервер установился.

``` shell
cargo install --locked taplo-lsp
```

Команда `cargo install` описывается
[здесь](https://doc.rust-lang.org/cargo/commands/cargo-install.html).
Опция `--locked` требует, чтобы `cargo` не обращался к репозиторию пакетов за свежими версиями.
Без этой опции cargo будет обновлять `Cargo.lock`.

После установки LSP-сервера и перезапуска GNU Emacs ничего видимо не изменилось:
сообщение о запуске LSP-сервера не появляется, ни в статусе, ни в буфере `*lsp-log*`;
никаких новых возможностей к базовой поддержке не добавилось. _Непонятно._


## Настраиваем Visual Studio Code

_Visual Studio Code_ последние несколько лет очень популярен среди программистов как
легковестная и настраиваемая альтернатива интегрированным средам разработки (IDE).
Когда-то и я был его постоянным пользователем, но последние года два я им не пользовался,
полностью перейдя на GNU Emacs. Так как мои коллеги и студенты часто отдают ему предпочтение,
то буквально совсем недавно я его снова поставил в свой Ubuntu Linux, чтобы разговаривать
на общем языке, так сказать. Поэтому сегодня посмотрим, что нам приготовила команда Rust
как пользователям Code. Собственно, это расширение с коротким названием
[**Rust**](https://marketplace.visualstudio.com/items?itemName=rust-lang.rust).
Как и пакет для GNU Emacs расширение для Code базируется на _rls_ или _rust-analyzer_.

С отладкой и запуском программы у меня здесь не заладилось. При нажатии на `F5` или `Ctrl-F5`
выскакивает сообщение, что расширение для отладки не установлено. И такового, как я понял, нет.
В общем, интереса личного у меня к работе в Code нет, ~~поэтому дальше копать, что да как,
я не намерен, по крайней мере пока~~.

Спустя некоторое время, после того как я пытался настроить VS Code, На Хабре вышел
[пост](https://habr.com/ru/post/645797/) о том, как настроить VS Code для Rust.
Отладка в нём таки доступна, но нужно вместо родного расширения установить базирующийся
на _rust-analyzer_. Возможно есть смысл использовать оный и в GNU Emacs.

По итогу изучения материала поста вышло следующие:

- [_rust-analyzer_](https://rust-analyzer.github.io/) устанавливать не стал,
  ни [сервер](https://github.com/rust-analyzer/rust-analyzer), ни
  [расширение для Code](https://marketplace.visualstudio.com/items?itemName=rust-lang.rust-analyzer). ~~Как я понял он ещё в разработке, в стабильную поставку ещё не включён. Подождём.~~
  После выпуска статьи выяснилось, что RSL объявлен устаревшим, и теперь всё же нужно переходить
  на _rust-analyzer_.

- Оказалось, что для отладки кода на Rust _rust-analyzer_ и не нужен. Всё работает
  и со стандартным _RLS_, нужно только:

1. установить в систему **LLDB**:
  ``` shell
  sudo apt install lldb
  ```

2. установить в Code расширение
  [**CodeLLDB**](https://marketplace.visualstudio.com/items?itemName=vadimcn.vscode-lldb)

3. и добавить конфигурацию запуска в Code: воспользовавшись генератором из Code
  или вручную, создав в директории проекта файл `.vscode/launch.json` со следующим содержанием:
  ``` json
  {
      "configurations": [
          {
          "type": "lldb",
          "request": "launch",
          "name": "Launch",
          "program": "${workspaceFolder}/target/debug/hello_rust",
          "args": [],
          "cwd": "${workspaceFolder}"
          }
      ]
  }
  ```

4. установить точку останова в нужном месте кода на Rust и нажать `F5` -- отладка запущена.
  Дальше всё как обычно.

Стоит заметить, что так мы можем отлаживать код, работающий в среде Linux. Код же запущенный
на Arduino так не отладить. Здесь можно посмотреть в сторону Qemu с поддержкой AVR, но там
используется `gdb`.

- Для работы с `Cargo.toml` ставим три расширения:

  - [**Even Better TOML**](https://marketplace.visualstudio.com/items?itemName=tamasfe.even-better-toml)
  для редактирования файлов в формате TOML

  - [**crates**](https://marketplace.visualstudio.com/items?itemName=serayuzgur.crates)
  для редактирования зависимостей: расширение использует [API](https://crates.io)
  для поиска пакетов

  - [**Crates Completer**](https://marketplace.visualstudio.com/items?itemName=jedeop.crates-completer)
  для автоподстановки названий пакетов в `Cargo.toml`, также использует [API](https://crates.io)

Ну и, как я писал ранее, для работы с файлами TOML нужно установить LSP-сервер
[**Taplo**](https://taplo.tamasfe.dev/).


## Настраиваем инструментарий для программирования Arduino Uno

Для программирования контроллеров на базе _AVR_ был создан специальный проект
[**AVR-Rust**](https://www.avr-rust.com/), одной из задач которого является разработка
поддержки AVR в Rust. Также в рамках данного проекта разрабатывается
[поддержка _Arduino_](https://github.com/avr-rust/ruduino) и ведётся
[список библиотек и проектов](https://github.com/avr-rust/awesome-avr-rust).

Начать изучение _AVR-Rust_ лучше всего с [официального руководства](https://book.avr-rust.com/).
В разделе ["Installing the compiler"](https://book.avr-rust.com/002-installing-the-compiler.html)
описывается, как установить компилятор Rust с поддержкой AVR. Но перед тем как это сделать
нужно установить
[стороннее ПО, которое потребуется для работы](https://book.avr-rust.com/002.1-installing-required-third-party-tools.html).

В _Ubuntu Linux_ нам потребуется установить пакеты `binutils`, `gcc-avr`, `avr-libc` и `avrdude`:

``` shell
sudo apt-get install binutils gcc-avr avr-libc avrdude
```

Далее нужно воспользоваться `rustup` и поставить с его помощью ночную сборку инструментария
и исходники Rust:

``` shell
rustup toolchain install nightly
rustup component add rust-src --toolchain nightly
```

## Моргаем светодиодом на Arduino Uno

Наконец разоберёмся с примером моргания встроенным светодиодом Arduino Uno на Rust.
Собственно, пример кода можно найти
[здесь](https://book.avr-rust.com/003.3-example-building-blink.html):

``` rust
#![no_std]
#![no_main]

use ruduino::Pin;
use ruduino::cores::current::{port};

#[no_mangle]
pub extern fn main() {
    port::B5::set_output();

    loop {
        port::B5::set_high();
        ruduino::delay::delay_ms(1000);
        port::B5::set_low();
        ruduino::delay::delay_ms(1000);
    }
}
```

Действуем строго по инструкции:

``` shell
git clone https://github.com/avr-rust/blink.git
cd blink
rustup override set nightly
export AVR_CPU_FREQUENCY_HZ=16000000
cargo build -Z build-std=core --target avr-atmega328p.json --release
```

~~И получаем ошибку компиляции, которая описана вот в этих ишью:~~
<https://github.com/avr-rust/blink/issues/37> и <https://github.com/avr-rust/delay/issues/10>
~~Проблема решается установкой ночной сборки компилятора годичной давности:~~
(Ишью закрыты по причине исправления бага, так что шаг ниже не понадобится.)

``` shell
rustup toolchain install nightly-2021-01-05
rustup override set nightly-2021-01-05
```

Неайс, конечно: будет установлена версия Rust 1.51.0.

Теперь повторим шаг:

``` shell
cargo build -Z build-std=core --target avr-atmega328p.json --release
```

И снова получим ошибку, только другую и с рекомендацией установить `rust-src`. Давайте поставим:

``` shell
rustup component add rust-src
```

И повторим попытку сборки. Кажется прошло успешно: `target/avr-atmega328p/release/blink.elf`
создан. Его размер примерно 9 Кб. Многовато, конечно, при 32 Кб доступной Flash-памяти.

Руководство по прожигу чипа Arduino Uno смотрим
[здесь](https://book.avr-rust.com/004-flashing-a-crate-to-chip.html).
Будем использовать раннее установленную нами утилиту `avrdude`, только сначала узнаем порт
для опции `-P`:

- убеждаемся, что устройство успешно подключено:

``` shell
lsusb
```

- смотрим номер порта:

``` shell
sudo dmesg | tail
```

Запускаем прожиг:

``` shell
avrdude -patmega328p -carduino -P/dev/ttyACM0 -b115200 -D -Uflash:w:target/avr-atmega328p/release/blink.elf:e
```

Фух! Всё прошло благополучно, светодиод мигает, **только как-то быстро**.
Во flash-память было записано примерно 2 Кб.

В опции `-c` указывается название программатора. Мы используем встроенный в Arduino на базе USB.

Наша Arduino Uno слишком быстро моргает своим светодиодом. И на это уже есть своя
[ишью](https://github.com/avr-rust/blink/issues/34).
В комментариях к ней рекомендуют добавить опцию сборки:

``` toml
[profile.release]
lto = true
```

Проверяем: работает, моргает в ожидаемом ритме. При этом размер прошивки уменьшился до менее чем
1 Кб. Недурно.

Что делает опция `lto`? Название расшифровывается как
[**Link Time Optimization**](https://llvm.org/docs/LinkTimeOptimization.html).
Это технология **LLVM**, которая оптимизирует результирующий код в процессе сборки.
Как я понял, при включении этой опции, линкер удаляет из кода неиспользуемые части,
за счёт чего наша прошивка и похудела. Вот только непонятно, почему эта опция влияет
на правильность работы нашего кода? Ведь этого не должно происходить.

Попробуем другие значения для опции `lto`:

- `false`: образ "жирный", светодиод моргает слишком часто.
- `"thin"`: эффект как при true (она же `"fat"`): размер и ритм такие же.
- `"off"`: при отключённой оптимизации при сборке такой же эффект, как при `false`.

Вот собственно и всё, что я хотел рассказать. Надеюсь, это руководство кому-то поможет стартануть
с Rust на Arduino.

## Что ещё почитать

- Интересный пост про
  [программирование на Rust микроконтроллеров семейства PIC32](https://habr.com/ru/company/ruvds/blog/645253/).
- [Configuring Emacs for Rust development](https://robert.kra.hn/posts/rust-emacs-setup/).

(c) 2022 Симоненко Евгений
