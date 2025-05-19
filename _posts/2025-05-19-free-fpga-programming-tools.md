---
layout: post
title: Свободные инструменты для программирования FPGA
date: 2025-05-19 11:38 +0000
author: Evgeny Simonenko
email: easimonenko@gmail.com
category: Review
tags: [FPGA, HDL, Verilog, VHDL, FPGA Tools, LSP]
---

Подборка свободных инструментов для программирования FPGA, включающая в себя средства поддержки языков HDL, синтезаторы, симуляторы и некоторые другие.

![Обложка](/images/free-fpga-programming-tools-cover.png)

<!-- end-of-lead -->

## Yosys

**[Yosys](https://yosyshq.net)** -- проект по созданию свободного набора инструментов для программирования FPGA. В состав этих инструментов входят: yosys, nextpnr, icestorm, apicula, trellis. Подробнее ниже в соответствующих разделах обзора.

## OSS CAD Suite

**[OSS CAD Suite](https://github.com/YosysHQ/oss-cad-suite-build)** -- сборка свободно-распространяемых инструментов для разработки программ для FPGA. Собирается в рамках проекта Yosys. Доступны сборки для GNU/Linux, MacOS X и Windows. Включает в себя в частности: GHDL, Icarus Verilog, nextpnr, openFPGALoader, OpenOCD, Verilator, Yosys и множество других программ.

## GHDL

**[GHDL](https://github.com/ghdl)** -- проект по разработке свободных инструментов для VHDL. Подробнее ниже в соответствующих разделах обзора.

## Verilog и SystemVerilog

**[Yosys](https://yosyshq.net/yosys/)** -- синтезатор для Verilog.

**[Icarus Verilog](https://steveicarus.github.io/iverilog/)** -- компилятор для Verilog.

**[Verilator](https://www.veripool.org/verilator/)** -- компилятор, симулятор и линтер для Verilog и SystemVerilog.

**[Verible](https://chipsalliance.github.io/verible/)** -- свободный набор инструментов для SystemVerilog от организации [CHIPS Alliance](https://www.chipsalliance.org/). Включает в себя: линтер, форматер и сервер LSP.

**[SVLS](https://github.com/dalance/svls)** -- сервер LSP для языка SystemVerilog.

**[SVLint](https://github.com/dalance/svlint)** -- линтер для языка SystemVerilog.

**[Veridian](https://github.com/vivekmalneedi/veridian)** -- сервер LSP для языка SystemVerilog.

## VHDL

**[GHDL](https://ghdl.github.io/ghdl/)** -- компилятор, анализатор, симулятор и синтезатор для VHDL.

**[NVC](https://www.nickg.me.uk/nvc/)** -- компилятор и симулятор для VHDL. Использует LLVM для компиляции в машинный код.

**[VHDL Language Server](https://github.com/VHDL-LS/rust_hdl)** -- сервер LSP для VHDL.

**[GHDL Yosys Plugin](https://github.com/ghdl/ghdl-yosys-plugin)** -- дополнение к Yosys для поддержки VHDL с использованием GHDL.

## Другие языки HDL

**[Chisel](https://www.chisel-lang.org/)** -- HDL для описания цифровых схем уровня RTL. Chisel является DSL на базе языка программирования Scala.

**[SpinalHDL](https://github.com/SpinalHDL/SpinalHDL)** -- HDL, являющийся DSL на базе языка Scala. Позиционируется как альтернатива для VHDL, Verilog и SystemVerilog.

**[Clash](https://clash-lang.org/)** -- язык HDL, имеющий синтаксис и семантику языка Haskell. Компилируется в VHDL, Verilog, SystemVerilog.

**[Veryl](https://veryl-lang.org/)** -- HDL, написанный на Rust и заимствующий из него синтаксис и некоторые возможности. Позиционируется как альтернатива SystemVerilog.

**[SystemC](https://systemc.org/)** -- средства разработки на языке C++ для FPGA.

**[Intel Compiler for SystemC](https://github.com/intel/systemc-compiler)** -- компилятор компании Intel языка SystemC в SystemVerilog.

## Place & Route

### nextpnr

**[nextpnr](https://github.com/YosysHQ/nextpnr)** -- универсальная утилита, обеспечивающая этап [Place & Route](https://en.wikipedia.org/wiki/Place_and_route). Поддерживаются следующие чипы: Lattice iCE40, ECP5, Nexus; Gowin; Altera Cyclone V и некоторые другие. Является частью проекта Yosys.

## Программаторы

**[openFPGALoader](https://trabucayre.github.io/openFPGALoader/)** -- универсальная утилита для записи прошивок в FPGA различных производителей, включая Anlogic, Cologne Chip, Efinix, Gowin, Intel (Altera), Lattice, Xilinx.

## Проекты поддержки чипов

**[IceStorm](https://clifford.fm/icestorm)** -- реверс-инжениринг, документация и примеры для чипов Lattice iCE40. Является частью проекта Yosys.

**[Apicula](https://github.com/YosysHQ/apicula)** -- проект, добавляющий к Yosys поддержку чипов компании Gowin семейств LittleBe и Arora.

**[Trellis](https://github.com/YosysHQ/prjtrellis)** -- проект, добавляющий к Yosys поддержку чипов Lattice ECP5.

**[Oxide](https://github.com/gatecat/prjoxide)** -- проект по добавлению в Yosys поддержки для чипов Lattice Nexus.

**[Mistral](https://github.com/Ravenslofty/mistral)** -- проект по добавлению к Yosys поддержки чипов Cyclone V.

## Управление проектами

**[PYNQ](https://www.pynq.io/)** -- полный цикл разработки для чипов Xilinx на языке Python с использованием сервера Jupyter.

**[F4PGA](https://f4pga.org/)** -- управление проектами с использованием только свободного ПО. Разрабатывается CHIPS Alliance.

**[PyFPGA](https://pyfpga.github.io/pyfpga/)** -- управление проектами разработки под FPGA, используя язык Python.

## Разное

**[netlistsvg](https://github.com/nturley/netlistsvg)** -- программа построения диаграммы связей между электронными компонентами на основе файла netlist, сгенерированного Yosys.

## Сводная таблица свободных инструментов

Для удобства и оценки масштаба составил сводную таблицу, упорядочив по количеству звёзд на GitHub на момент написания статьи.


| #  | Звёздность | Название                                                       | GitHub                                                                        | Язык разработки | Лицензия     |
|----|------------|----------------------------------------------------------------|-------------------------------------------------------------------------------|-----------------|--------------|
| 1  | 4269       | [Chisel](https://www.chisel-lang.org/)                         | [chipsalliance/chisel](https://github.com/chipsalliance/chisel)               | Scala           | Apache 2.0   |
| 2  | 3813       | [Yosys](https://yosyshq.net/yosys/)                            | [YosysHQ/yosys](https://github.com/YosysHQ/yosys)                             | C++             | ISC          |
| 3  | 3042       | [Icarus Verilog](https://steveicarus.github.io/iverilog/)      | [steveicarus/iverilog](https://github.com/steveicarus/iverilog)               | C++             | GNU GPL v2   |
| 4  | 2888       | [Verilator](https://www.veripool.org/verilator/)               | [verilator/verilator](https://github.com/verilator/verilator)                 | C++             | GNU LGPL v3  |
| 5  | 2556       | [GHDL](https://ghdl.github.io/ghdl/)                           | [ghdl/ghdl](https://github.com/ghdl/ghdl)                                     | Ada             | GNU GPL v2   |
| 6  | 2132       | [PYNQ](https://www.pynq.io/)                                   | [Xilinx/PYNQ](https://github.com/Xilinx/PYNQ)                                 | Python          | BSD 3-Clause |
| 7  | 1786       | SpinalHDL                                                      | [SpinalHDL/SpinalHDL](https://github.com/SpinalHDL/SpinalHDL)                 | Scala           | GNU LGPL v3  |
| 8  | 1537       | [Verible](https://chipsalliance.github.io/verible/)            | [chipsalliance/verible](https://github.com/chipsalliance/verible)             | C++             | Apache 2.0   |
| 9  | 1498       | [Clash](https://clash-lang.org/)                               | [clash-lang/clash-compiler](https://github.com/clash-lang/clash-compiler)     | Haskell         | BSD 2-Clause |
| 10 | 1439       | nextpnr                                                        | [YosysHQ/nextpnr](https://github.com/YosysHQ/nextpnr)                         | C++             | ISC          |
| 11 | 1327       | [openFPGALoader](https://trabucayre.github.io/openFPGALoader/) | [trabucayre/openFPGALoader](https://github.com/trabucayre/openFPGALoader)     | C++             | Apache 2.0   |
| 12 | 1058       | [IceStorm](https://clifford.fm/icestorm)                       | [YosysHQ/icestorm/](https://github.com/YosysHQ/icestorm/)                     | Python          | ISC          |
| 13 | 1051       | OSS CAD Suite                                                  | [YosysHQ/oss-cad-suite-build](https://github.com/YosysHQ/oss-cad-suite-build) | --              | ISC          |
| 14 | 696        | netlistsvg                                                     | [nturley/netlistsvg](https://github.com/nturley/netlistsvg)                   | JavaScript      | MIT          |
| 15 | 693        | [NVC](https://www.nickg.me.uk/nvc/)                            | [nickg/nvc](https://github.com/nickg/nvc)                                     | C               | GNU GPL v3   |
| 16 | 627        | [Veryl](https://veryl-lang.org/)                               | [veryl-lang/veryl](https://github.com/veryl-lang/veryl)                       | Rust            | Apache 2.0   |
| 17 | 552        | Apicula                                                        | [YosysHQ/apicula](https://github.com/YosysHQ/apicula)                         | Python          | MIT          |
| 18 | 550        | [SystemC](https://systemc.org/)                                | [accellera-official/systemc](https://github.com/accellera-official/systemc)   | C++             | Apache 2.0   |
| 19 | 507        | SVLS                                                           | [dalance/svls](https://github.com/dalance/svls)                               | Rust            | MIT          |
| 20 | 411        | Trellis                                                        | [YosysHQ/prjtrellis](https://github.com/YosysHQ/prjtrellis)                   | Python          | Разные       |
| 21 | 398        | VHDL Language Server                                           | [VHDL-LS/rust_hdl](https://github.com/VHDL-LS/rust_hdl)                       | Rust            | MPL 2.0      |
| 22 | 387        | [F4PGA](https://f4pga.org/)                                    | [chipsalliance/f4pga](https://github.com/chipsalliance/f4pga)                 | Python          | Apache 2.0   |
| 23 | 345        | SVLint                                                         | [dalance/svlint](https://github.com/dalance/svlint)                           | Rust            | MIT          |
| 24 | 334        | GHDL Yosys Plugin                                              | [ghdl/ghdl-yosys-plugin](https://github.com/ghdl/ghdl-yosys-plugin)           | C++             | GNU GPL v3   |
| 25 | 272        | Intel Compiler for SystemC                                     | [intel/systemc-compiler](https://github.com/intel/systemc-compiler)           | C++             | Apache 2.0   |
| 26 | 170        | Veridian                                                       | [vivekmalneedi/veridian](https://github.com/vivekmalneedi/veridian)           | Rust            | MIT          |
| 27 | 142        | Oxide                                                          | [gatecat/prjoxide](https://github.com/gatecat/prjoxide)                       | Python          | ISC          |
| 28 | 133        | [PyFPGA](https://pyfpga.github.io/pyfpga/)                     | [PyFPGA/pyfpga](https://github.com/PyFPGA/pyfpga)                             | Python          | GNU GPL v3   |
| 29 | 122        | Mistral                                                        | [Ravenslofty/mistral](https://github.com/Ravenslofty/mistral)                 | C++             | BSD 3-Clause |

Как мы видим, свободно-распространяемых инструментов набралось немало, а здесь перечислены не все. Эти инструменты покрывают все основные потребности разработчиков под FPGA, при этом нетребовательны к ресурсам, работают в различных операционных системах и постоянно развиваются. Но главное, они не привязаны к производителям чипов и могут использоваться с различными из них, хотя и не со всеми.

(c) Симоненко Евгений, 2025
