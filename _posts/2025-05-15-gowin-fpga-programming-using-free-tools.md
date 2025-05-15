---
layout: post
title: Программирование FPGA Gowin с использованием свободных инструментов
date: 2025-05-15 14:22 +0000
author: Evgeny Simonenko
email: easimonenko@gmail.com
category: Tutorial
tags: [Gowin, Yosys, FPGA, Linux]
---

Краткая инструкция, о том, как запрограммировать чип FPGA Gowin с использованием только свободных программных инструментов и комплекта Sipeed Tang Primer 20K Dock.

![Комплект Sipeed Tang Primer 20K Dock](/images/sipeed-tang-primer-20k-dock-ext-board.jpg)

<!-- end-of-lead -->

## Введение

Sipeed Tang Primer 20K с Dock ext-board -- доступный комплект [FPGA](https://en.wikipedia.org/wiki/Field-programmable_gate_array) на базе чипа GW2A-LV18PG256C8/I7 семейства [Arora](https://www.gowinsemi.com/en/product/detail/38/) компании [Gowin](https://www.gowinsemi.com/en/), включающий в себя плату Dock ext-board со множеством внешних интерфейсов, встроенным программатором JTAG и разъёмом для [SoM](https://en.wikipedia.org/wiki/System_on_module), собственно SoM с чипом Gowin и разъёмом для подключения программатора, кабель USB и кабель программатора. Более подробный обзор этого комплекта по [ссылке](https://habr.com/ru/companies/timeweb/articles/747346/).

В качестве инструментальной операционной системы используется Fedora Linux, но должно работать в большинстве других дистрибутивов Linux, включая Ubuntu.

Компания Gowin для производимых ею чипов FPGA предлагает собственные проприетарные инструменты, про которые подробнее можно прочитать по [ссылке](https://habr.com/ru/companies/timeweb/articles/748594/). Но нас будет интересовать набор свободно-распространяемых инструментов [Yosys](https://yosyshq.net/yosys/).

## Подключение к компьютеру с Linux

Используем прилагающийся кабель Type-C -> Type-A. После подключения к ПК с Linux смотрим лог:

``` shell
sudo dmesg | tail -20
```

```
[ 4187.370979] Purging GPU memory, 0 pages freed, 0 pages still pinned, 4 pages left available.
[ 4187.466512] Purging GPU memory, 0 pages freed, 0 pages still pinned, 4 pages left available.
[ 4188.026603] Purging GPU memory, 0 pages freed, 0 pages still pinned, 4 pages left available.
[ 4188.330211] Purging GPU memory, 0 pages freed, 0 pages still pinned, 4 pages left available.
[ 4188.716163] oom_reaper: reaped process 3490 (ptyxis), now anon-rss:60kB, file-rss:68kB, shmem-rss:8kB
[ 8195.983177] usb 1-1: new full-speed USB device number 2 using uhci_hcd
[ 8196.332263] usb 1-1: not running at top speed; connect to a high speed hub
[ 8196.364257] usb 1-1: New USB device found, idVendor=0403, idProduct=6010, bcdDevice= 5.00
[ 8196.364273] usb 1-1: New USB device strings: Mfr=1, Product=2, SerialNumber=3
[ 8196.364281] usb 1-1: Product: JTAG Debugger
[ 8196.364288] usb 1-1: Manufacturer: SIPEED
[ 8196.364294] usb 1-1: SerialNumber: FactoryAIOT Pro
[ 8196.524255] usbcore: registered new interface driver ftdi_sio
[ 8196.524280] usbserial: USB Serial support registered for FTDI USB Serial Device
[ 8196.524393] ftdi_sio 1-1:1.0: FTDI USB Serial Device converter detected
[ 8196.524433] usb 1-1: Detected FT2232C/D
[ 8196.528351] usb 1-1: FTDI USB Serial Device converter now attached to ttyUSB0
[ 8196.528445] ftdi_sio 1-1:1.1: FTDI USB Serial Device converter detected
[ 8196.528483] usb 1-1: Detected FT2232C/D
[ 8196.530308] usb 1-1: FTDI USB Serial Device converter now attached to ttyUSB1
```

Устройство определилось как программатор подключённый к `ttyUSB1`.

Посмотрим ещё командой `lsusb`:

```
Bus 001 Device 002: ID 0403:6010 Future Technology Devices International, Ltd FT2232C/D/H Dual UART/FIFO IC
```

## Программные инструменты

Команда Yosys осуществляет ежесуточную сборку пакета инструментов, которую можно загружать из раздела релизов репозитория по [ссылке](https://github.com/YosysHQ/oss-cad-suite-build/). Предоставляются сборки для трёх основных операционных систем. Загружаем и распаковываем в подходящее место в домашнем каталоге архив для Linux.

Для настройки пакета, нужно запустить следующий скрипт:

``` shell
source oss-cad-suite/environment
```

Другой путь установки инструментов -- воспользоваться пакетом Python `Apycula`:

``` shell
pip3 install Apycula
```

Также загрузим исходники Apicula, проекта поддержки Gowin в Yosys. Они нам потребуются ради примеров.

``` shell
git clone https://github.com/YosysHQ/apicula
```

## Стадии

Перейдём в каталог `examples` исходников Apicula и займёмся примером `blinky.v` на языке [Verilog](https://en.wikipedia.org/wiki/Verilog). Ниже все стадии.

### Synthesis

На Dock ext-board шесть светодиодов, поэтому параметр ниже `LEDS_NR=6`.

``` shell
yosys -D LEDS_NR=6 -p "read_verilog blinky.v; synth_gowin -json blinky.json"
```

Результат будет записан в файл `blinky.json`.

### Place & Route

Зададим значения переменным DEVICE и BOARD:

``` shell
DEVICE="GW2A-LV18PG256C8/I7"
BOARD="primer20k"
```

`DEVICE` это наименование чипа FPGA Gowin, его можно найти на самом чипе, а также на странице проекта по названию модели платы.

`BOARD` это условное наименование платы SoM Tang Primer 20K.

И вызовем команду `nextpnr-himbaechel`, предназначенную для чипов Gowin:

``` shell
nextpnr-himbaechel --json blinky.json --write pnrblinky.json --device $DEVICE --vopt cst=$BOARD.cst --vopt family=GW2A-18
```

Результат будет записан в файл `prnblinky.json`.

На этом этапе дополнительно можно построить диаграмму блоков с помощью программы `netlistsvg`, которую нужно устанавливать отдельно:

``` shell
netlistsvg pnrblinky.json -o blinky.svg
```

### Bitstream Generation

Генерируем прошивку на основе информации, полученной на предыдущем этапе:

``` shell
gowin_pack -d $DEVICE -o pack.fs pnrblinky.json
```

### Programming

Прошиваем чип Gowin:

``` shell
openFPGALoader -b tangprimer20k pack.fs
```

И наблюдаем моргающий `LED0 FPGA_DONE` и замысловато моргающую линейку светодиодов `LED2`-`LED5`.

![Моргающий светодиодами Sipeed Tang Primer 20K Dock](/images/sipeed-tang-primer-20k-dock-ext-board_with-leds-flashing.jpg)

(c) Симоненко Евгений, 2025
