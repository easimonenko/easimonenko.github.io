---
layout: post
title: 'Source Based GNU/Linux Distributions: Alpine'
author: Evgeny Simonenko
email: easimonenko@gmail.com
category: Research Work
tags: [GNU, Linux, LifeBook, Notebooks, Laptops, Free Software]
---

...

Это третья статья из цикла, и в ней будет рассказано про эксперименты с дистрибутивом Alpine. В первой статье рассказывается про эксперименты с Void, а во второй -- с Gentoo.

![Alpine на Fujitsu Siemens LifeBook S7210](/images/alpine-on-lifebook-s7210.jpg)

<!-- end-of-lead -->

## Об Alpine

Основные системные особенности Alpine:

- Использование [OpenRC](https://wiki.gentoo.org/wiki/Project:OpenRC) в качестве системы инициализации.
- Собственный менеджер пакетов [APK](https://gitlab.alpinelinux.org/alpine/apk-tools).
- Использование библиотеки [musl](https://musl.libc.org/) вместо GNU C Library.
- Использование [BusyBox](https://busybox.net/).

**OpenRC** -- система инициализации с поддержкой зависимостей для Unix-подобных операционных систем. Написана на языке C и распространяется под лицензией BSD 2-clause. Изначально создана для дистрибутива Gentoo.

**Alpine Package Keeper** -- менеджер пакетов, специально разработанный для дистрибутива Alpine. Написан на языке C и распространяется под лицензией GNU GPL v2.

**musl** -- реализация стандартной библиотеки языка C. Распространяется под лицензией MIT.

**BusyBox** -- набор утилит, традиционно присутствующих в Unix-подобных операционных системах, и компилируемых в один исполняемый файл. Ориентирован на использование во встраиваемых системах, но может также использоваться на ПК и серверах. Распространяется под лицензией GNU GPL v2.

Расширенная установочная система включает в себя следующие пакеты (исключено большинство подпакетов):

| Название                | Описание                                                                                        |
|-------------------------|-------------------------------------------------------------------------------------------------|
| acct                    | The GNU Accounting Utilities                                                                    |
| acl                     | Access control list utilities                                                                   |
| agetty                  | `util-linux` subpackage                                                                         |
| alpine-base             | Meta package for minimal alpine base                                                            |
| alpine-baselayout       | Alpine base dir structure and init scripts                                                      |
| alpine-conf             | Alpine configuration management scripts                                                         |
| alpine-keys             | Public keys for Alpine packages                                                                 |
| alpine-release          | Alpine release data                                                                             |
| apk-cron                | Periodic software updates                                                                       |
| apk-tools               | Alpine Package Keeper - package manager for Alpine                                              |
| arpon                   | Arp handler inspectiON is a handler daemon with tools to handle all ARP aspects                 |
| arpwatch                | Ethernet monitoring program                                                                     |
| awall                   | Alpine Wall                                                                                     |
| bash                    | The GNU Bourne Again shell                                                                      |
| blkid                   | `util-linux` subpackage                                                                         |
| bonding                 | Scripts for network interface bonding                                                           |
| bridge                  | Scripts for configuring network bridge interfaces                                               |
| bridge-utils            | Tools for configuring the Linux kernel 802.1d Ethernet Bridge                                   |
| brotli                  | Generic lossless compressor                                                                     |
| btrfs-progs             | BTRFS filesystem utilities                                                                      |
| busybox                 | Size optimized toolbox of many common UNIX utilities                                            |
| bwm-ng                  | A small and simple console-based live bandwidth monitor                                         |
| ca-certificates         | Common CA certificates PEM files from Mozilla                                                   |
| c-ares                  | Asynchronous DNS/names resolver library                                                         |
| cfdisk                  | `util-linux` subpackage                                                                         |
| chrony                  | NTP client and server programs                                                                  |
| cksfv                   | Simple File Verification                                                                        |
| conntrack-tools         | Connection tracking userspace tools                                                             |
| coreutils               | The basic file, shell and text manipulation utilities                                           |
| cryptsetup              | Userspace setup tool for transparent encryption of block devices using the Linux 2.6 cryptoapi  |
| curl                    | URL retrieval utility and library                                                               |
| cutter                  | A program that allows firewall administrators to abort TCP/IP connections                       |
| cyrus-sasl              | Cyrus Simple Authentication Service Layer (SASL)                                                |
| dbus                    | Freedesktop.org message bus system                                                              |
| device-mapper           | Device mapper userspace library and tools from LVM2                                             |
| dhcpcd                  | RFC2131 compliant DHCP client                                                                   |
| dmesg                   | `util-linux` subpackage                                                                         |
| dnsmasq                 | A lightweight DNS, DHCP, RA, TFTP and PXE server                                                |
| dnssec-root             | The DNSSEC root key(s)                                                                          |
| doas                    | OpenBSD's temporary privilege escalation tool                                                   |
| dosfstools              | DOS filesystem utilities                                                                        |
| drill                   |                                                                                                 |
| e2fsprogs               | Standard Ext2/3/4 filesystem utilities                                                          |
| efibootmgr              | Linux user-space application to modify the Intel Extensible Firmware Interface                  |
| efivar                  | Tools and library to manipulate EFI variables                                                   |
| ethtool                 | Utility for controlling network drivers and hardware                                            |
| eudev                   | Init system agnostic fork of systemd-udev                                                       |
| f2fs-tools              | Tools for the Flash-Friendly File System (F2FS)                                                 |
| findmnt                 | `util-linux` subpackage                                                                         |
| flock                   | `util-linux` subpackage                                                                         |
| fping                   | A utility to ping multiple hosts at once                                                        |
| fprobe                  | libpcap-based tool that collect network traffic                                                 |
| fstrim                  | `util-linux` subpackage                                                                         |
| gdbm                    | GNU dbm is a set of database routines that use extensible hashing                               |
| gmp                     | Free library for arbitrary precision arithmetic                                                 |
| grub                    | Bootloader with support for Linux, Multiboot and more                                           |
| heimdal                 | Implementation of Kerberos 5                                                                    |
| hexdump                 | `util-linux` subpackage                                                                         |
| hiredis                 | Minimalistic C client library for Redis                                                         |
| htop                    | Interactive process viewer                                                                      |
| hwdate                  | Hardware identification and configuration data                                                  |
| ifupdown-ng             | Tools for managing network configuration                                                        |
| igmpproxy               | A simple dynamic Multicast Routing Daemon using only IGMP signalling                            |
| inih                    | Simple .INI file parser for embedded systems                                                    |
| iproute2                | IP Routing Utilities                                                                            |
| iproute2-qos            | Scripts to set up quality of service with iproute2                                              |
| ipset                   | Manage Linux IP sets                                                                            |
| iptables                | Linux kernel firewall, NAT and packet mangling tools                                            |
| iputils                 | IP Configuration Utilities                                                                      |
| iw                      | nl80211 based CLI configuration utility for wireless devices                                    |
| jansson                 | Lightweight JSON library                                                                        |
| jitterentropy-library   | Jitterentropy library                                                                           |
| json-c                  | A JSON implementation in C                                                                      |
| kbd                     | Tools for configuring the console (keyboard, virtual terminals, etc.)                           |
| kea                     | DHCPv4 and DHCPv6 server from ISC                                                               |
| keyutils                | Linux Key Management Utilities                                                                  |
| kmod                    | Linux kernel module management utilities                                                        |
| krb5                    | The Kerberos network authentication system                                                      |
| krb5-conf               | Shared krb5.conf for both MIT krb5 and heimdal                                                  |
| lddtree                 | List dynamic dependencies as a tree                                                             |
| ldns                    | Lowlevel DNS(SEC) library                                                                       |
| libaio                  | Asynchronous input/output library                                                               |
| libcap2                 | POSIX 1003.1e capabilities                                                                      |
| libcap-ng               | POSIX capabilities library                                                                      |
| libdnet                 | Simplified, portable interface to several low-level networking routines                         |
| libeconf                | Enhanced Config File Parser                                                                     |
| libedit                 | BSD line editing library                                                                        |
| libev                   | Event dispatch library                                                                          |
| libevent                | An event notification library                                                                   |
| libffi                  | Portable, high level programming interface to various calling conventions                       |
| libidn2                 | Encode/Decode library for internationalized domain names                                        |
| libmnl                  | Library for minimalistic netlink                                                                |
| libnet                  | A generic networking API that provides access to several protocols                              |
| libnetfilter\_conntrack | Programming interface (API) to the in-kernel connection tracking state table                    |
| libnetfilter\_cthelper  | A Netfilter netlink library for connection tracking helpers                                     |
| libnetfilter\_cttimeout | Library for the connection tracking timeout infrastructure                                      |
| libnetfilter\_queue     | API to packets that have been queued by the kernel packet filter                                |
| libnfnetlink            | Low-level library for netfilter related kernel/userspace communication                          |
| libnftnl                | Netfilter library providing interface to the nf\_tables subsystem                               |
| libnl3                  | Library for applications dealing with netlink sockets                                           |
| libpcap                 | Portable library for network traffic capture                                                    |
| libpsl                  | C library for the Publix Suffix List                                                            |
| libseccomp              | Interface to the Linux Kernel's syscall filtering mechanism                                     |
| libtirpc                | Transport Independent RPC library (SunRPC replacement)                                          |
| libunistring            | Library for manipulating Unicode strings and C strings                                          |
| libusb                  | Library that enables userspace access to USB devices                                            |
| libverto                | Main loop abstraction library                                                                   |
| links                   | Web browser running in both graphics and text mode                                              |
| linux-firmware          | Firmware files for linux                                                                        |
| linux-lts               | Linux LTS kernel                                                                                |
| linux-pam               | Linux PAM (Pluggable Authentication Modules for Linux)                                          |
| lm-sensors              | Collection of user space tools for general SMBus access and hardware monitoring                 |
| log4cplus               | Logging Framework for C++                                                                       |
| logger                  | `util-linux` subpackage                                                                         |
| logrotate               | Tool to rotate logfiles                                                                         |
| losetup                 | `util-linux` subpackage                                                                         |
| lsblk                   | `util-linux` subpackage                                                                         |
| lscpu                   | `util-linux` subpackage                                                                         |
| lsof                    | LiSt Open Files                                                                                 |
| lua5.4                  | Powerful light-weight programming language                                                      |
| lvm2                    | Logical Volume Manager 2 utilities                                                              |
| lxc                     | Userspace interface for the Linux kernel containment features                                   |
| lz4                     | LZ4 is lossless compression algorithm with fast decoder @ multiple GB/s per core                |
| lzo                     | LZO -- a real-time data compression library                                                     |
| mcookie                 | `util-linux` subpackage                                                                         |
| mdadm                   | A tool for managing Linux Software RAID arrays                                                  |
| mdev-conf               | Configuration files for mdev and mdevd                                                          |
| mkinitfs                | Tool to generate initramfs images for Alpine                                                    |
| mount                   |                                                                                                 |
| mpdecimal               | Complete implementation of the General Decimal Arithmetic Specification                         |
| mtools                  | Collection of utilities to access MS-DOS disks from Unix without mounting them                  |
| musl                    | The musl C library (libc) implementation                                                        |
| musl-fts                | fts(3) functions, which are missing in musl libc                                                |
| nano                    | Enhanced clone of the Pico text editor                                                          |
| ncurses                 | Console display library                                                                         |
| net-snmp                | Simple Network Management Protocol                                                              |
| network-extras          | Meta package to pull in ppp, vlan, bonding, bridge and wifi support                             |
| nfs-utils               | Kernel-mode NFS                                                                                 |
| nftables                | Netfilter tables userspace tools                                                                |
| nghttp2                 | HTTP/2 C client, server and proxy                                                               |
| nrpe                    | NRPE allows you to remotely execute Nagios plugins on other Linux/Unix machines                 |
| nsd                     | Authoritative only, high performance and simple DNS server                                      |
| opennhrp                | NBMA Next Hop Resolution Protocol daemon                                                        |
| openntpd                | Lightweight NTP server ported from OpenBSD                                                      |
| openrc                  | OpenRC manages the services, startup and shutdown of a host                                     |
| openresolv              | A framework for managing DNS information                                                        |
| openssh                 | Port of OpenBSD's free SSH release                                                              |
| openssl                 | Toolkit for Transport Layer Security (TLS)                                                      |
| openvpn                 | Robust, and highly configurable VPN (Virtual Private Network)                                   |
| parted                  | Utility to create, destroy, resize, check and copy partitions                                   |
| partx                   | `util-linux` subpackage                                                                         |
| pciutils                | PCI bus configuration space access library and tools                                            |
| pcre2                   | Perl-compatible regular expression library                                                      |
| pcsc-lite               | Middleware to access a smart card using SCard API (PC/SC)                                       |
| pingu                   | Small daemon that pings hosts and executes a script when status change                          |
| pkcs11-helper           | Library that simplifies the interaction with PKCS#11 providers                                  |
| popt                    | Commandline option parser                                                                       |
| ppp                     | A daemon which implements the PPP protocol for dial-up networking                               |
| protobuf-c              | Protocol Buffers implementation in C                                                            |
| python3                 | High-level scripting language                                                                   |
| quagga                  | A free routing daemon replacing Zebra supporting RIP, OSPF, BGP and NHRP                        |
| readline                | GNU readline library                                                                            |
| rng-tools               | Random number generator daemon                                                                  |
| rpcbind                 | Portmap replacement which supports RPC over various protocols                                   |
| rsync                   | A file transfer program to keep remote files in sync                                            |
| runuser                 | `util-linux` subpackage                                                                         |
| scanelf                 |                                                                                                 |
| setarch                 |                                                                                                 |
| setpriv                 | `util-linux` subpackage                                                                         |
| sfdisk                  | `util-linux` subpackage                                                                         |
| skalibs                 | Set of general-purpose C programming libraries for skarnet.org software                         |
| sntpc                   | Simple NTP client                                                                               |
| socat                   | Multipurpose relay for binary protocols                                                         |
| sqlite                  | C library that implements an SQL database engine                                                |
| ssmtp                   | Extremely simple MTA to get mail off the system to a mail hub                                   |
| strace                  | Diagnostic, debugging and instructional userspace tracer                                        |
| strongswan              | IPsec-based VPN solution focused on security and ease of use, supporting IKEv1/IKEv2 and MOBIKE |
| sysfsutils              | System Utilities Based on Sysfs                                                                 |
| sysklogd                | System and kernel log daemons                                                                   |
| syslinux                | Boot loader for the Linux operating system                                                      |
| tar                     | Utility used to store, backup, and transport files                                              |
| tcpdump                 | Command-line packet analyzer                                                                    |
| tiny-cloud              | Tiny Cloud instance bootstrapper                                                                |
| tinyproxy               | Lightweight HTTP proxy                                                                          |
| tmux                    | Tool to control multiple terminals from a single terminal                                       |
| tzdata                  | Timezone data                                                                                   |
| umount                  |                                                                                                 |
| unbound                 | Unbound is a validating, recursive, and caching DNS resolver                                    |
| usb-modeswitch          | A mode switching tool for controlling flip flop (multiple device) USB gear                      |
| usbutils                | USB Device Utilities                                                                            |
| userspace-rcu           | Userspace RCU (read-copy-update) library                                                        |
| util-linux              | Random collection of Linux utilities                                                            |
| utmps                   | A secure utmp/wtmp implementation                                                               |
| uuidgen                 | `util-linux` subpackage                                                                         |
| v86d                    | Userspace helper for uvesafb that runs x86 code in an emulated environment                      |
| vlan                    | Scripts for configuring VLAN network interfaces                                                 |
| wget                    | Network utility to retrieve files from the Web                                                  |
| wiperfs                 | `util-linux` subpackage                                                                         |
| wireguard-tools         | Next generation secure network tunnel: userspace tools                                          |
| wireless-tools          | Open Source wireless tools                                                                      |
| wpa\_supplicant         | Utility providing key negotiation for WPA wireless networks                                     |
| xfsprogs                | XFS filesystem utilities                                                                        |
| xtables-addons          | Netfilter userspace extensions for iptables                                                     |
| xtables-addons-lts      | Iptables extensions kernel modules                                                              |
| xz                      | Library and CLI tools for XZ and LZMA compressed files                                          |
| yaml                    | YAML 1.1 parser and emitter written in C                                                        |
| yx                      | A small shell tool that allows extraction of targeted data from YAML"                           |
| zfs                     | Advanced filesystem and volume manager                                                          |
| zfs-lts                 | ZFS Linux kernel modules                                                                        |
| zlib                    | A compression/decompression Library                                                             |
| zonenotify              | Utility to send NS_NOTIFY packets to slave DNS servers                                          |
| zstd                    | Zstandard - Fast real-time compression algorithm                                                |

Как видно, присутствует большое количество сетевых утилит и библиотек. Полагаю, что изрядное количество из них большинству пользователей не пригодится.

Для подготовки диска потребуется установить следующие пакеты: `e2fsprogs`, `e2fsprogs-extra`, `lvm2`, `cryptsetup`.

``` sh
apk add cryptsetup
```

Отформатируем ранее созданный раздел /dev/sda3:

``` sh
mkfs.ext4 -c -L ALPINE /dev/sda3
```

Подключим ранее созданный раздел SWAP:

``` sh
cryptsetup luksOpen /dev/sda4 data
rc-service lvm start
swapon /dev/mapper/data-swap
```

...

## Ссылки

- Домашняя страничка Alpine: https://alpinelinux.org/
- Alpine Wiki: https://wiki.alpinelinux.org/wiki/Main_Page
- Каталог пакетов Alpine: https://pkgs.alpinelinux.org/
- Сервер закачки Alpine: 
- Зеркало сервера закачки Alpine: https://mirror.yandex.ru/mirrors/alpine/
- Репозитории Git: https://gitlab.alpinelinux.org/alpine
- Wikipedia [RU]​: https://ru.wikipedia.org/wiki/Alpine_Linux
- Wikipedia [EN]: https://en.wikipedia.org/wiki/Alpine_Linux

(c) Симоненко Е.А., 2026

Буквальное копирование и распространение этого произведения разрешается на любом носителе при условии сохранения вышеуказанного уведомления об авторских правах, этого лицензионного уведомления и нижеуказанного уведомления об отказе от ответственности. Авторские права на все изображения в этом произведении принадлежат автору этого произведения и являются его неотъемлемой частью. Фрагменты программного кода из этого произведения, если не оговорено иное, разрешается распространять и использовать без ограничений с или без изменений и без указания авторских прав.

Информация в этом произведении, включая также изображения и фрагменты программного кода, предоставляется как есть, без какой либо гарантии и обещания пригодности для чего либо. Автор не несёт ответственность за любой ущерб, возникший в результате использования данного произведения.

Разрешается использование текста данной лицензии иными авторами в своих произведениях как в буквальном виде, так и в изменённом или адаптированном под нужды автора виде без указания оригинального авторства данной лицензии.
