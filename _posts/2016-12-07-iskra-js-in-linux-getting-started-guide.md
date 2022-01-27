---
layout: post
title: Начало работы с Iskra JS в Linux
author: Evgeny Simonenko
email: easimonenko@gmail.com
date: 2016-12-07
category: Tutorial
tags: [Iskra JS, Espruino, Linux, Amperka]
---

В статье рассматривается как начать работать с [Iskra JS][] в среде
Linux, как настроить доступ к плате по USB, как установить и использовать
среду Espruino IDE.

<!-- end-of-lead -->

## Предварительная подготовка

Iskra JS подключается к компьютеру как виртуальное последовательное устройство.
Чтобы после физического подключения его, мы могли начать с ним работать,
необходимо добавить пользователя в группу-владельца соответствующего файла
устройства. Делается это так:

``` sh
sudo usermod -a -G dialout username
```

Где _username_ имя Вашего пользователя Linux.

После этого нужно выйти и вновь зайти в систему.

Для большего удобства работы с файлами устройств, представляющих подключённые
устройства Espruino, к коим относится и Iskra JS, можно скачать и установить
настройки для udev:

``` sh
wget https://github.com/espruino/Espruino/raw/master/misc/45-espruino.rules
sudo cp 45-espruino.rules /etc/udev/rules.d/
sudo service udev restart
```

## Подключение Iskra JS

Подключите физически Вашу Iskra JS в компьютеру с помощь USB кабеля и выполните
в консоли следующую команду:

``` sh
dmesg | tail
```

Вы должны увидеть текст следующего содержания:

``` plain
[15638.463029] usb 1-1.1: new full-speed USB device number 3 using ehci-pci
[15638.558070] usb 1-1.1: New USB device found, idVendor=0483, idProduct=5740
[15638.558079] usb 1-1.1: New USB device strings: Mfr=1, Product=2, SerialNumber=3
[15638.558085] usb 1-1.1: Product: STM32 Virtual ComPort
[15638.558090] usb 1-1.1: Manufacturer: STMicroelectronics
[15638.558094] usb 1-1.1: SerialNumber: 00000000001A
[15638.578357] cdc_acm 1-1.1:1.0: ttyACM0: USB ACM device
[15638.579818] usbcore: registered new interface driver cdc_acm
[15638.579822] cdc_acm: USB Abstract Control Model driver for USB modems and ISDN adapters
```

Отсюда можно выяснить, какой файл устройства отвечает за подключённую Iskra JS,
скорее всего это будет `/dev/ttyACM0`.

Выполните также

``` sh
lsusb
```

В числе прочих строк Вы должны увидеть и такую:

``` plain
Bus 001 Device 003: ID 0483:5740 STMicroelectronics STM32F407
```

## Установка Espruino Web IDE

Основной средой разработки для Iskra JS является Espruino Web IDE. Эта среда
является приложением для браузера Chromium, который в Ubuntu можно установить
как родной пакет из APT:

``` sh
sudo apt install chromium-browser
```

Если в репозитории используемого Вами дистрибутива нет Chromium, то Вы можете
скачать его по
[ссылке](http://www.chromium.org/getting-involved/download-chromium).

После установки и запуска Chromium нужно пройти по
[ссылке](https://chrome.google.com/webstore/detail/espruino-web-ide/bleoifhkdalbjfbobjackfdifdneehpo).
Вы увидете диалог установки приложения Espruino Web IDE. После его установки
также пройдите по
[ссылке](http://www.espruino.com/webide?settings=%7B%22MODULE_URL%22%3A%22http%3A%2F%2Fjs.amperka.ru%2Fmodules%22%2C%22BOARD_JSON_URL%22%3A%22http%3A%2F%2Fjs.amperka.ru%2Fjson%22%2C%22SAVE_ON_SEND%22%3Atrue%7D).
Это нужно для добавления в Web IDE настроек для Iskra JS.

## Начало работы в Espruino Web IDE

После установки Espruino Web IDE в Chromium добавится соответствующая кнопка
для запуска приложения. Также, после запуска приложения, Вы сможете добавить
его в избранное Вашей среды, например, такую возможность предоставляет Gnome 3.

Если предыдущие шаги Вы осуществили правильно, то Вы сможете подключиться к
Вашей Iskra JS, и поэкспериментировать в REPL, а также загрузить предложенную
самой средой простую программу.

Дальнейшие подробности смотри в
[официальном руководстве](http://wiki.amperka.ru/js:ide).

## Приложение Serial Projector

Разработчики Iskra JS также разработали для нас клёвое приложение
_Serial Projector_ для красивого отображения информации, поступающей с Iskra JS
по последовательному соединению. Serial Projector также является приложением
для Chromium, и для его установки нужно пройти по
[ссылке](http://amperka.ru/chrome/serial-projector).

## Ссылки

[Iskra JS]: http://amperka.ru/product/iskra-js
[Yodo]: http://amperka.ru/product/yodo
[О JavaScript на Amperka]: http://wiki.amperka.ru/js:start
[Espruino Web IDE на Amperka]: http://wiki.amperka.ru/js:ide

* [Iskra JS][]
* [Yodo][]
* [О JavaScript на Amperka][]
* [Espruino Web IDE на Amperka][]

(c) Симоненко Евгений, 2016
