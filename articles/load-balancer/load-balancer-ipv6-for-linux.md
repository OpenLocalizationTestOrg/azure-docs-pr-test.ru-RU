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
# <a name="configuring-dhcpv6-for-linux-vms"></a><span data-ttu-id="dfc42-104">Настройка DHCPv6 для виртуальных машин Linux</span><span class="sxs-lookup"><span data-stu-id="dfc42-104">Configuring DHCPv6 for Linux VMs</span></span>

<span data-ttu-id="dfc42-105">Некоторые образы виртуальных машин Linux hello в hello Azure Marketplace нет DHCPv6 настройки по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="dfc42-105">Some of hello Linux virtual machine images in hello Azure Marketplace do not have DHCPv6 configured by default.</span></span> <span data-ttu-id="dfc42-106">IPv6, DHCPv6 toosupport должен находиться в hello ОС Linux распределение, которое вы используете.</span><span class="sxs-lookup"><span data-stu-id="dfc42-106">toosupport IPv6, DHCPv6 must be configured in within hello Linux OS distribution that you are using.</span></span> <span data-ttu-id="dfc42-107">В разных дистрибутивах Linux для настройки DHCPv6 применяются различные способы, так как они используют разные пакеты.</span><span class="sxs-lookup"><span data-stu-id="dfc42-107">Different Linux distributions have different ways of configuring DHCPv6 because they use different packages.</span></span>

> [!NOTE]
> <span data-ttu-id="dfc42-108">Последние SUSE Linux и CoreOS изображения в Azure Marketplace hello были предварительно настроенную DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="dfc42-108">Recent SUSE Linux and CoreOS images in hello Azure Marketplace have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="dfc42-109">При использовании этих образов дополнительные изменения не требуются.</span><span class="sxs-lookup"><span data-stu-id="dfc42-109">No additional changes are required when using those images.</span></span>

<span data-ttu-id="dfc42-110">В этом документе описывается способ tooenable DHCPv6 так, чтобы к виртуальной машине Linux получил IPv6-адрес.</span><span class="sxs-lookup"><span data-stu-id="dfc42-110">This document describes how tooenable DHCPv6 so that your Linux virtual machine obtains an IPv6 address.</span></span>

> [!WARNING]
> <span data-ttu-id="dfc42-111">Неправильное редактирование файлов конфигурации сети может привести к вы toolose сетевого доступа tooyour виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="dfc42-111">Improperly editing network configuration files can cause you toolose network access tooyour VM.</span></span> <span data-ttu-id="dfc42-112">Рекомендуется сначала протестировать изменения конфигурации на нерабочих системах.</span><span class="sxs-lookup"><span data-stu-id="dfc42-112">We recommended that you test your configuration changes on non-production systems.</span></span> <span data-ttu-id="dfc42-113">инструкции Hello в этой статье были проверены на последние версии hello изображений Linux hello в hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="dfc42-113">hello instructions in this article have been tested on hello latest versions of hello Linux images in hello Azure Marketplace.</span></span> <span data-ttu-id="dfc42-114">Hello документации по используемой версии ОС Linux более подробные инструкции.</span><span class="sxs-lookup"><span data-stu-id="dfc42-114">Consult hello documentation for your specific version of Linux for more detailed instructions.</span></span>

## <a name="ubuntu"></a><span data-ttu-id="dfc42-115">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="dfc42-115">Ubuntu</span></span>

1. <span data-ttu-id="dfc42-116">Измените файл hello `/etc/dhcp/dhclient6.conf` и добавить hello, следующей строкой:</span><span class="sxs-lookup"><span data-stu-id="dfc42-116">Edit hello file `/etc/dhcp/dhclient6.conf` and add hello following line:</span></span>

        timeout 10;

2. <span data-ttu-id="dfc42-117">Измените конфигурацию сети hello интерфейс eth0 hello с hello следующая конфигурация:</span><span class="sxs-lookup"><span data-stu-id="dfc42-117">Edit hello network configuration for hello eth0 interface with hello following configuration:</span></span>

   * <span data-ttu-id="dfc42-118">На **Ubuntu 12.04 и 14.04**, измените файл hello`/etc/network/interfaces.d/eth0.cfg`</span><span class="sxs-lookup"><span data-stu-id="dfc42-118">On **Ubuntu 12.04 and 14.04**, edit hello file `/etc/network/interfaces.d/eth0.cfg`</span></span>
   * <span data-ttu-id="dfc42-119">На **Ubuntu 16.04**, измените файл hello`/etc/network/interfaces.d/50-cloud-init.cfg`</span><span class="sxs-lookup"><span data-stu-id="dfc42-119">On **Ubuntu 16.04**, edit hello file `/etc/network/interfaces.d/50-cloud-init.cfg`</span></span>

         iface eth0 inet6 auto
             up sleep 5
             up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. <span data-ttu-id="dfc42-120">Обновите IPv6-адрес:</span><span class="sxs-lookup"><span data-stu-id="dfc42-120">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="debian"></a><span data-ttu-id="dfc42-121">Debian</span><span class="sxs-lookup"><span data-stu-id="dfc42-121">Debian</span></span>

1. <span data-ttu-id="dfc42-122">Измените файл hello `/etc/dhcp/dhclient6.conf` и добавить hello, следующей строкой:</span><span class="sxs-lookup"><span data-stu-id="dfc42-122">Edit hello file `/etc/dhcp/dhclient6.conf` and add hello following line:</span></span>

        timeout 10;

2. <span data-ttu-id="dfc42-123">Измените файл hello `/etc/network/interfaces` и добавить hello следующая конфигурация:</span><span class="sxs-lookup"><span data-stu-id="dfc42-123">Edit hello file `/etc/network/interfaces` and add hello following configuration:</span></span>

        iface eth0 inet6 auto
            up sleep 5
            up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. <span data-ttu-id="dfc42-124">Обновите IPv6-адрес:</span><span class="sxs-lookup"><span data-stu-id="dfc42-124">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="rhel--centos--oracle-linux"></a><span data-ttu-id="dfc42-125">RHEL / CentOS / Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="dfc42-125">RHEL / CentOS / Oracle Linux</span></span>

1. <span data-ttu-id="dfc42-126">Измените файл hello `/etc/sysconfig/network` и добавьте следующий параметр hello:</span><span class="sxs-lookup"><span data-stu-id="dfc42-126">Edit hello file `/etc/sysconfig/network` and add hello following parameter:</span></span>

        NETWORKING_IPV6=yes

2. <span data-ttu-id="dfc42-127">Измените файл hello `/etc/sysconfig/network-scripts/ifcfg-eth0` и добавить hello, следующие два параметра:</span><span class="sxs-lookup"><span data-stu-id="dfc42-127">Edit hello file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add hello following two parameters:</span></span>

        IPV6INIT=yes
        DHCPV6C=yes

3. <span data-ttu-id="dfc42-128">Обновите IPv6-адрес:</span><span class="sxs-lookup"><span data-stu-id="dfc42-128">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-11--opensuse-13"></a><span data-ttu-id="dfc42-129">SLES 11 и openSUSE 13</span><span class="sxs-lookup"><span data-stu-id="dfc42-129">SLES 11 & openSUSE 13</span></span>

<span data-ttu-id="dfc42-130">В недавно выпущенных образах SLES и openSUSE в Azure протокол DHCPv6 предварительно настроен.</span><span class="sxs-lookup"><span data-stu-id="dfc42-130">Recent SLES and openSUSE images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="dfc42-131">При использовании этих образов дополнительные изменения не требуются.</span><span class="sxs-lookup"><span data-stu-id="dfc42-131">No additional changes are required when using those images.</span></span> <span data-ttu-id="dfc42-132">При наличии на основе SUSE старую или пользовательского образа виртуальной Машины, используйте hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="dfc42-132">If you have a VM based on an older or custom SUSE image, use hello following steps:</span></span>

1. <span data-ttu-id="dfc42-133">Установка hello `dhcp-client` пакет, при необходимости:</span><span class="sxs-lookup"><span data-stu-id="dfc42-133">Install hello `dhcp-client` package, if needed:</span></span>

    ```bash
    sudo zypper install dhcp-client
    ```

2. <span data-ttu-id="dfc42-134">Измените файл hello `/etc/sysconfig/network/ifcfg-eth0` и добавьте следующий параметр hello:</span><span class="sxs-lookup"><span data-stu-id="dfc42-134">Edit hello file `/etc/sysconfig/network/ifcfg-eth0` and add hello following parameter:</span></span>

        DHCLIENT6_MODE='managed'

3. <span data-ttu-id="dfc42-135">Обновите hello IPv6-адрес:</span><span class="sxs-lookup"><span data-stu-id="dfc42-135">Renew hello IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-12-and-opensuse-leap"></a><span data-ttu-id="dfc42-136">SLES 12 и openSUSE Leap</span><span class="sxs-lookup"><span data-stu-id="dfc42-136">SLES 12 and openSUSE Leap</span></span>

<span data-ttu-id="dfc42-137">В недавно выпущенных образах SLES и openSUSE в Azure протокол DHCPv6 предварительно настроен.</span><span class="sxs-lookup"><span data-stu-id="dfc42-137">Recent SLES and openSUSE images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="dfc42-138">При использовании этих образов дополнительные изменения не требуются.</span><span class="sxs-lookup"><span data-stu-id="dfc42-138">No additional changes are required when using those images.</span></span> <span data-ttu-id="dfc42-139">При наличии на основе SUSE старую или пользовательского образа виртуальной Машины, используйте hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="dfc42-139">If you have a VM based on an older or custom SUSE image, use hello following steps:</span></span>

1. <span data-ttu-id="dfc42-140">Измените файл hello `/etc/sysconfig/network/ifcfg-eth0` и замените этот параметр</span><span class="sxs-lookup"><span data-stu-id="dfc42-140">Edit hello file `/etc/sysconfig/network/ifcfg-eth0` and replace this parameter</span></span>

        #BOOTPROTO='dhcp4'

    <span data-ttu-id="dfc42-141">с hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="dfc42-141">with hello following value:</span></span>

        BOOTPROTO='dhcp'

2. <span data-ttu-id="dfc42-142">Добавьте следующий параметр слишком hello`/etc/sysconfig/network/ifcfg-eth0`:</span><span class="sxs-lookup"><span data-stu-id="dfc42-142">Add hello following parameter too`/etc/sysconfig/network/ifcfg-eth0`:</span></span>

        DHCLIENT6_MODE='managed'

3. <span data-ttu-id="dfc42-143">Обновите hello IPv6-адрес:</span><span class="sxs-lookup"><span data-stu-id="dfc42-143">Renew hello IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="coreos"></a><span data-ttu-id="dfc42-144">CoreOS</span><span class="sxs-lookup"><span data-stu-id="dfc42-144">CoreOS</span></span>

<span data-ttu-id="dfc42-145">В недавно выпущенных образах CoreOS в Azure протокол DHCPv6 предварительно настроен.</span><span class="sxs-lookup"><span data-stu-id="dfc42-145">Recent CoreOS images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="dfc42-146">При использовании этих образов дополнительные изменения не требуются.</span><span class="sxs-lookup"><span data-stu-id="dfc42-146">No additional changes are required when using those images.</span></span> <span data-ttu-id="dfc42-147">При наличии на основе CoreOS более раннюю версию или пользовательского образа виртуальной Машины, используйте hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="dfc42-147">If you have a VM based on an older or custom CoreOS image, use hello following steps:</span></span>

1. <span data-ttu-id="dfc42-148">Измените файл hello`/etc/systemd/network/10_dhcp.network`</span><span class="sxs-lookup"><span data-stu-id="dfc42-148">Edit hello file `/etc/systemd/network/10_dhcp.network`</span></span>

        [Match]
        eth0

        [Network]
        DHCP=ipv6

2. <span data-ttu-id="dfc42-149">Обновите hello IPv6-адрес:</span><span class="sxs-lookup"><span data-stu-id="dfc42-149">Renew hello IPv6 address:</span></span>

    ```bash
    sudo systemctl restart systemd-networkd
    ```
