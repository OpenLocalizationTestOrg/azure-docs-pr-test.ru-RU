---
title: "Настройка DHCPv6 для виртуальных машин Linux | Документация Майкрософт"
description: "Узнайте, как настроить DHCPv6 для виртуальных машин Linux."
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
ms.openlocfilehash: 5c591e7f1838c86ca74caea9dd3a5e8f874fd8a7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-dhcpv6-for-linux-vms"></a><span data-ttu-id="f8ac6-104">Настройка DHCPv6 для виртуальных машин Linux</span><span class="sxs-lookup"><span data-stu-id="f8ac6-104">Configuring DHCPv6 for Linux VMs</span></span>

<span data-ttu-id="f8ac6-105">В некоторых образах виртуальных машин Linux в Azure Marketplace протокол DHCPv6 не настроен по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="f8ac6-105">Some of the Linux virtual machine images in the Azure Marketplace do not have DHCPv6 configured by default.</span></span> <span data-ttu-id="f8ac6-106">Для поддержки IPv6 в используемом дистрибутиве ОС Linux необходимо настроить DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="f8ac6-106">To support IPv6, DHCPv6 must be configured in within the Linux OS distribution that you are using.</span></span> <span data-ttu-id="f8ac6-107">В разных дистрибутивах Linux для настройки DHCPv6 применяются различные способы, так как они используют разные пакеты.</span><span class="sxs-lookup"><span data-stu-id="f8ac6-107">Different Linux distributions have different ways of configuring DHCPv6 because they use different packages.</span></span>

> [!NOTE]
> <span data-ttu-id="f8ac6-108">В недавно выпущенных образах SUSE Linux и CoreOS в Azure Marketplace протокол DHCPv6 предварительно настроен.</span><span class="sxs-lookup"><span data-stu-id="f8ac6-108">Recent SUSE Linux and CoreOS images in the Azure Marketplace have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="f8ac6-109">При использовании этих образов дополнительные изменения не требуются.</span><span class="sxs-lookup"><span data-stu-id="f8ac6-109">No additional changes are required when using those images.</span></span>

<span data-ttu-id="f8ac6-110">В этом документе описывается, как включить DHCPv6, чтобы виртуальная машина Linux получила IPv6-адрес.</span><span class="sxs-lookup"><span data-stu-id="f8ac6-110">This document describes how to enable DHCPv6 so that your Linux virtual machine obtains an IPv6 address.</span></span>

> [!WARNING]
> <span data-ttu-id="f8ac6-111">Неправильное изменение файлов конфигурации сети может привести к тому, что виртуальная машина утратит доступ к сети.</span><span class="sxs-lookup"><span data-stu-id="f8ac6-111">Improperly editing network configuration files can cause you to lose network access to your VM.</span></span> <span data-ttu-id="f8ac6-112">Рекомендуется сначала протестировать изменения конфигурации на нерабочих системах.</span><span class="sxs-lookup"><span data-stu-id="f8ac6-112">We recommended that you test your configuration changes on non-production systems.</span></span> <span data-ttu-id="f8ac6-113">Приведенные в этой статье инструкции были протестированы на последних версиях образов Linux в Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f8ac6-113">The instructions in this article have been tested on the latest versions of the Linux images in the Azure Marketplace.</span></span> <span data-ttu-id="f8ac6-114">Подробные инструкции см. в документации к своей версии Linux.</span><span class="sxs-lookup"><span data-stu-id="f8ac6-114">Consult the documentation for your specific version of Linux for more detailed instructions.</span></span>

## <a name="ubuntu"></a><span data-ttu-id="f8ac6-115">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="f8ac6-115">Ubuntu</span></span>

1. <span data-ttu-id="f8ac6-116">Измените файл `/etc/dhcp/dhclient6.conf` , добавив следующую строку:</span><span class="sxs-lookup"><span data-stu-id="f8ac6-116">Edit the file `/etc/dhcp/dhclient6.conf` and add the following line:</span></span>

        timeout 10;

2. <span data-ttu-id="f8ac6-117">Замените конфигурацию сети для интерфейса eth0 следующей конфигурацией:</span><span class="sxs-lookup"><span data-stu-id="f8ac6-117">Edit the network configuration for the eth0 interface with the following configuration:</span></span>

   * <span data-ttu-id="f8ac6-118">В **Ubuntu 12.04 и 14.04** измените файл `/etc/network/interfaces.d/eth0.cfg`.</span><span class="sxs-lookup"><span data-stu-id="f8ac6-118">On **Ubuntu 12.04 and 14.04**, edit the file `/etc/network/interfaces.d/eth0.cfg`</span></span>
   * <span data-ttu-id="f8ac6-119">В **Ubuntu 16.04** измените файл `/etc/network/interfaces.d/50-cloud-init.cfg`.</span><span class="sxs-lookup"><span data-stu-id="f8ac6-119">On **Ubuntu 16.04**, edit the file `/etc/network/interfaces.d/50-cloud-init.cfg`</span></span>

         iface eth0 inet6 auto
             up sleep 5
             up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. <span data-ttu-id="f8ac6-120">Обновите IPv6-адрес:</span><span class="sxs-lookup"><span data-stu-id="f8ac6-120">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="debian"></a><span data-ttu-id="f8ac6-121">Debian</span><span class="sxs-lookup"><span data-stu-id="f8ac6-121">Debian</span></span>

1. <span data-ttu-id="f8ac6-122">Измените файл `/etc/dhcp/dhclient6.conf` , добавив следующую строку:</span><span class="sxs-lookup"><span data-stu-id="f8ac6-122">Edit the file `/etc/dhcp/dhclient6.conf` and add the following line:</span></span>

        timeout 10;

2. <span data-ttu-id="f8ac6-123">Измените файл `/etc/network/interfaces` , добавив следующую конфигурацию:</span><span class="sxs-lookup"><span data-stu-id="f8ac6-123">Edit the file `/etc/network/interfaces` and add the following configuration:</span></span>

        iface eth0 inet6 auto
            up sleep 5
            up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. <span data-ttu-id="f8ac6-124">Обновите IPv6-адрес:</span><span class="sxs-lookup"><span data-stu-id="f8ac6-124">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="rhel--centos--oracle-linux"></a><span data-ttu-id="f8ac6-125">RHEL / CentOS / Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="f8ac6-125">RHEL / CentOS / Oracle Linux</span></span>

1. <span data-ttu-id="f8ac6-126">Измените файл `/etc/sysconfig/network` , добавив следующий параметр:</span><span class="sxs-lookup"><span data-stu-id="f8ac6-126">Edit the file `/etc/sysconfig/network` and add the following parameter:</span></span>

        NETWORKING_IPV6=yes

2. <span data-ttu-id="f8ac6-127">Измените файл `/etc/sysconfig/network-scripts/ifcfg-eth0` , добавив следующие два параметра:</span><span class="sxs-lookup"><span data-stu-id="f8ac6-127">Edit the file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add the following two parameters:</span></span>

        IPV6INIT=yes
        DHCPV6C=yes

3. <span data-ttu-id="f8ac6-128">Обновите IPv6-адрес:</span><span class="sxs-lookup"><span data-stu-id="f8ac6-128">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-11--opensuse-13"></a><span data-ttu-id="f8ac6-129">SLES 11 и openSUSE 13</span><span class="sxs-lookup"><span data-stu-id="f8ac6-129">SLES 11 & openSUSE 13</span></span>

<span data-ttu-id="f8ac6-130">В недавно выпущенных образах SLES и openSUSE в Azure протокол DHCPv6 предварительно настроен.</span><span class="sxs-lookup"><span data-stu-id="f8ac6-130">Recent SLES and openSUSE images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="f8ac6-131">При использовании этих образов дополнительные изменения не требуются.</span><span class="sxs-lookup"><span data-stu-id="f8ac6-131">No additional changes are required when using those images.</span></span> <span data-ttu-id="f8ac6-132">Если у вас есть виртуальная машина, использующая более старый или пользовательский образ SUSE, то выполните описанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="f8ac6-132">If you have a VM based on an older or custom SUSE image, use the following steps:</span></span>

1. <span data-ttu-id="f8ac6-133">При необходимости установите пакет `dhcp-client` :</span><span class="sxs-lookup"><span data-stu-id="f8ac6-133">Install the `dhcp-client` package, if needed:</span></span>

    ```bash
    sudo zypper install dhcp-client
    ```

2. <span data-ttu-id="f8ac6-134">Измените файл `/etc/sysconfig/network/ifcfg-eth0` , добавив следующий параметр:</span><span class="sxs-lookup"><span data-stu-id="f8ac6-134">Edit the file `/etc/sysconfig/network/ifcfg-eth0` and add the following parameter:</span></span>

        DHCLIENT6_MODE='managed'

3. <span data-ttu-id="f8ac6-135">Обновите IPv6-адрес:</span><span class="sxs-lookup"><span data-stu-id="f8ac6-135">Renew the IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-12-and-opensuse-leap"></a><span data-ttu-id="f8ac6-136">SLES 12 и openSUSE Leap</span><span class="sxs-lookup"><span data-stu-id="f8ac6-136">SLES 12 and openSUSE Leap</span></span>

<span data-ttu-id="f8ac6-137">В недавно выпущенных образах SLES и openSUSE в Azure протокол DHCPv6 предварительно настроен.</span><span class="sxs-lookup"><span data-stu-id="f8ac6-137">Recent SLES and openSUSE images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="f8ac6-138">При использовании этих образов дополнительные изменения не требуются.</span><span class="sxs-lookup"><span data-stu-id="f8ac6-138">No additional changes are required when using those images.</span></span> <span data-ttu-id="f8ac6-139">Если у вас есть виртуальная машина, использующая более старый или пользовательский образ SUSE, то выполните описанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="f8ac6-139">If you have a VM based on an older or custom SUSE image, use the following steps:</span></span>

1. <span data-ttu-id="f8ac6-140">Измените файл `/etc/sysconfig/network/ifcfg-eth0` , заменив параметр</span><span class="sxs-lookup"><span data-stu-id="f8ac6-140">Edit the file `/etc/sysconfig/network/ifcfg-eth0` and replace this parameter</span></span>

        #BOOTPROTO='dhcp4'

    <span data-ttu-id="f8ac6-141">следующим значением:</span><span class="sxs-lookup"><span data-stu-id="f8ac6-141">with the following value:</span></span>

        BOOTPROTO='dhcp'

2. <span data-ttu-id="f8ac6-142">Добавьте следующий параметр в `/etc/sysconfig/network/ifcfg-eth0`:</span><span class="sxs-lookup"><span data-stu-id="f8ac6-142">Add the following parameter to `/etc/sysconfig/network/ifcfg-eth0`:</span></span>

        DHCLIENT6_MODE='managed'

3. <span data-ttu-id="f8ac6-143">Обновите IPv6-адрес:</span><span class="sxs-lookup"><span data-stu-id="f8ac6-143">Renew the IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="coreos"></a><span data-ttu-id="f8ac6-144">CoreOS</span><span class="sxs-lookup"><span data-stu-id="f8ac6-144">CoreOS</span></span>

<span data-ttu-id="f8ac6-145">В недавно выпущенных образах CoreOS в Azure протокол DHCPv6 предварительно настроен.</span><span class="sxs-lookup"><span data-stu-id="f8ac6-145">Recent CoreOS images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="f8ac6-146">При использовании этих образов дополнительные изменения не требуются.</span><span class="sxs-lookup"><span data-stu-id="f8ac6-146">No additional changes are required when using those images.</span></span> <span data-ttu-id="f8ac6-147">Если у вас есть виртуальная машина, использующая более старый или пользовательский образ CoreOS, то выполните описанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="f8ac6-147">If you have a VM based on an older or custom CoreOS image, use the following steps:</span></span>

1. <span data-ttu-id="f8ac6-148">Измените файл `/etc/systemd/network/10_dhcp.network`</span><span class="sxs-lookup"><span data-stu-id="f8ac6-148">Edit the file `/etc/systemd/network/10_dhcp.network`</span></span>

        [Match]
        eth0

        [Network]
        DHCP=ipv6

2. <span data-ttu-id="f8ac6-149">Обновите IPv6-адрес:</span><span class="sxs-lookup"><span data-stu-id="f8ac6-149">Renew the IPv6 address:</span></span>

    ```bash
    sudo systemctl restart systemd-networkd
    ```
