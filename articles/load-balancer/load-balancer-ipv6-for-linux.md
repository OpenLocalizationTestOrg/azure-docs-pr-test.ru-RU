---
title: "aaaConfiguring DHCPv6 для виртуальных машин Linux | Документы Microsoft"
description: "Как tooconfigure DHCPv6 для виртуальных машин Linux."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
keywords: "IPv6, Azure Load Balancer, двойной стек, общедоступный IP-адрес, встроенная поддержка Ipv6, мобильное устройство, Интернет вещей"
ms.assetid: b32719b6-00e8-4cd0-ba7f-e60e8146084b
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/14/2016
ms.author: kumud
ms.openlocfilehash: abd5a98c3496b189946f59bab1d9c20dcd0aa2c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-dhcpv6-for-linux-vms"></a>Настройка DHCPv6 для виртуальных машин Linux

Некоторые образы виртуальных машин Linux hello в hello Azure Marketplace нет DHCPv6 настройки по умолчанию. IPv6, DHCPv6 toosupport должен находиться в hello ОС Linux распределение, которое вы используете. В разных дистрибутивах Linux для настройки DHCPv6 применяются различные способы, так как они используют разные пакеты.

> [!NOTE]
> Последние SUSE Linux и CoreOS изображения в Azure Marketplace hello были предварительно настроенную DHCPv6. При использовании этих образов дополнительные изменения не требуются.

В этом документе описывается способ tooenable DHCPv6 так, чтобы к виртуальной машине Linux получил IPv6-адрес.

> [!WARNING]
> Неправильное редактирование файлов конфигурации сети может привести к вы toolose сетевого доступа tooyour виртуальной Машины. Рекомендуется сначала протестировать изменения конфигурации на нерабочих системах. инструкции Hello в этой статье были проверены на последние версии hello изображений Linux hello в hello Azure Marketplace. Hello документации по используемой версии ОС Linux более подробные инструкции.

## <a name="ubuntu"></a>Ubuntu

1. Измените файл hello `/etc/dhcp/dhclient6.conf` и добавить hello, следующей строкой:

        timeout 10;

2. Измените конфигурацию сети hello интерфейс eth0 hello с hello следующая конфигурация:

   * На **Ubuntu 12.04 и 14.04**, измените файл hello`/etc/network/interfaces.d/eth0.cfg`
   * На **Ubuntu 16.04**, измените файл hello`/etc/network/interfaces.d/50-cloud-init.cfg`

         iface eth0 inet6 auto
             up sleep 5
             up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. Обновите IPv6-адрес:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="debian"></a>Debian

1. Измените файл hello `/etc/dhcp/dhclient6.conf` и добавить hello, следующей строкой:

        timeout 10;

2. Измените файл hello `/etc/network/interfaces` и добавить hello следующая конфигурация:

        iface eth0 inet6 auto
            up sleep 5
            up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. Обновите IPv6-адрес:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="rhel--centos--oracle-linux"></a>RHEL / CentOS / Oracle Linux

1. Измените файл hello `/etc/sysconfig/network` и добавьте следующий параметр hello:

        NETWORKING_IPV6=yes

2. Измените файл hello `/etc/sysconfig/network-scripts/ifcfg-eth0` и добавить hello, следующие два параметра:

        IPV6INIT=yes
        DHCPV6C=yes

3. Обновите IPv6-адрес:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-11--opensuse-13"></a>SLES 11 и openSUSE 13

В недавно выпущенных образах SLES и openSUSE в Azure протокол DHCPv6 предварительно настроен. При использовании этих образов дополнительные изменения не требуются. При наличии на основе SUSE старую или пользовательского образа виртуальной Машины, используйте hello следующие шаги:

1. Установка hello `dhcp-client` пакет, при необходимости:

    ```bash
    sudo zypper install dhcp-client
    ```

2. Измените файл hello `/etc/sysconfig/network/ifcfg-eth0` и добавьте следующий параметр hello:

        DHCLIENT6_MODE='managed'

3. Обновите hello IPv6-адрес:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-12-and-opensuse-leap"></a>SLES 12 и openSUSE Leap

В недавно выпущенных образах SLES и openSUSE в Azure протокол DHCPv6 предварительно настроен. При использовании этих образов дополнительные изменения не требуются. При наличии на основе SUSE старую или пользовательского образа виртуальной Машины, используйте hello следующие шаги:

1. Измените файл hello `/etc/sysconfig/network/ifcfg-eth0` и замените этот параметр

        #BOOTPROTO='dhcp4'

    с hello следующие значения:

        BOOTPROTO='dhcp'

2. Добавьте следующий параметр слишком hello`/etc/sysconfig/network/ifcfg-eth0`:

        DHCLIENT6_MODE='managed'

3. Обновите hello IPv6-адрес:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="coreos"></a>CoreOS

В недавно выпущенных образах CoreOS в Azure протокол DHCPv6 предварительно настроен. При использовании этих образов дополнительные изменения не требуются. При наличии на основе CoreOS более раннюю версию или пользовательского образа виртуальной Машины, используйте hello следующие шаги:

1. Измените файл hello`/etc/systemd/network/10_dhcp.network`

        [Match]
        eth0

        [Network]
        DHCP=ipv6

2. Обновите hello IPv6-адрес:

    ```bash
    sudo systemctl restart systemd-networkd
    ```
