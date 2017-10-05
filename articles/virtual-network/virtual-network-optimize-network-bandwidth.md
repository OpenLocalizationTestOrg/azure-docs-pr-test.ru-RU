---
title: "Оптимизации пропускной способности сети для виртуальной машины | Документация Майкрософт"
description: "Узнайте, как оптимизировать пропускную способность сети для виртуальной машины Azure."
services: virtual-network
documentationcenter: na
author: steveesp
manager: Gerald DeGrace
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: steveesp
ms.openlocfilehash: 914747983d4d974810836be66d6c6af343f58b60
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="optimize-network-throughput-for-azure-virtual-machines"></a><span data-ttu-id="dd7e3-103">Оптимизации пропускной способности сети для виртуальной машины Azure</span><span class="sxs-lookup"><span data-stu-id="dd7e3-103">Optimize network throughput for Azure virtual machines</span></span>

<span data-ttu-id="dd7e3-104">Виртуальные машины Azure имеют сетевые параметры по умолчанию, с помощью которых можно дополнительно оптимизировать пропускную способность сети.</span><span class="sxs-lookup"><span data-stu-id="dd7e3-104">Azure virtual machines (VM) have default network settings that can be further optimized for network throughput.</span></span> <span data-ttu-id="dd7e3-105">В этой статье описывается, как оптимизировать пропускную способность сети для виртуальных машин Microsoft Azure, которые работают под управлением Windows и Linux, включая такие основные дистрибутивы, как Ubuntu, CentOS и Red Hat.</span><span class="sxs-lookup"><span data-stu-id="dd7e3-105">This article describes how to optimize network throughput for Microsoft Azure Windows and Linux VMs, including major distributions such as Ubuntu, CentOS and Red Hat.</span></span>

## <a name="windows-vm"></a><span data-ttu-id="dd7e3-106">Виртуальная машина Windows</span><span class="sxs-lookup"><span data-stu-id="dd7e3-106">Windows VM</span></span>

<span data-ttu-id="dd7e3-107">Если виртуальная машина Windows поддерживается с помощью [ускорения работы в сети](virtual-network-create-vm-accelerated-networking.md), включение этой функции обеспечит оптимальную конфигурацию для пропускной способности.</span><span class="sxs-lookup"><span data-stu-id="dd7e3-107">If your Windows VM is supported with [Accelerated Networking](virtual-network-create-vm-accelerated-networking.md), enabling that feature would be the optimal configuration for throughput.</span></span> <span data-ttu-id="dd7e3-108">Остальные виртуальные машины Windows, использующие масштабирование размера приема (RSS), могут иметь большую максимальную пропускную способность, чем виртуальная машина без RSS.</span><span class="sxs-lookup"><span data-stu-id="dd7e3-108">For all other Windows VMs, using Receive Side Scaling (RSS) can reach higher maximal throughput than a VM without RSS.</span></span> <span data-ttu-id="dd7e3-109">По умолчанию функция RSS может быть отключена на виртуальной машине Windows.</span><span class="sxs-lookup"><span data-stu-id="dd7e3-109">RSS may be disabled by default in a Windows VM.</span></span> <span data-ttu-id="dd7e3-110">Чтобы определить, включена ли эта функция, и включить ее при необходимости, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="dd7e3-110">Complete the following steps to determine whether RSS is enabled and to enable it if it's disabled.</span></span>

1. <span data-ttu-id="dd7e3-111">Выполните команду PowerShell `Get-NetAdapterRss`, чтобы определить, включена ли функция RSS для сетевого адаптера.</span><span class="sxs-lookup"><span data-stu-id="dd7e3-111">Enter the `Get-NetAdapterRss` PowerShell command to see if RSS is enabled for a network adapter.</span></span> <span data-ttu-id="dd7e3-112">В следующем примере показаны результаты выполнения команды `Get-NetAdapterRss`, когда функция RSS не включена.</span><span class="sxs-lookup"><span data-stu-id="dd7e3-112">In the following example output returned from the `Get-NetAdapterRss`, RSS is not enabled.</span></span>

    ```powershell
    Name                    : Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : False
    ```
2. <span data-ttu-id="dd7e3-113">Выполните следующую команду, чтобы включить RSS:</span><span class="sxs-lookup"><span data-stu-id="dd7e3-113">Enter the following command to enable RSS:</span></span>

    ```powershell
    Get-NetAdapter | % {Enable-NetAdapterRss -Name $_.Name}
    ```
    <span data-ttu-id="dd7e3-114">Предыдущая команда не имеет выходные данные.</span><span class="sxs-lookup"><span data-stu-id="dd7e3-114">The previous command does not have an output.</span></span> <span data-ttu-id="dd7e3-115">Команда изменяет параметры сетевого адаптера, в результате чего около одной минуты отсутствует подключение.</span><span class="sxs-lookup"><span data-stu-id="dd7e3-115">The command changed NIC settings, causing temporary connectivity loss for about one minute.</span></span> <span data-ttu-id="dd7e3-116">В это время появится диалоговое окно повторного подключения.</span><span class="sxs-lookup"><span data-stu-id="dd7e3-116">A Reconnecting dialog box appears during the connectivity loss.</span></span> <span data-ttu-id="dd7e3-117">Обычно после третьей попытки подключение восстанавливается.</span><span class="sxs-lookup"><span data-stu-id="dd7e3-117">Connectivity is typically restored after the third attempt.</span></span>
3. <span data-ttu-id="dd7e3-118">Убедитесь, что функция RSS включена на виртуальной машине. Для этого еще раз выполните команду `Get-NetAdapterRss`.</span><span class="sxs-lookup"><span data-stu-id="dd7e3-118">Confirm that RSS is enabled in the VM by entering the `Get-NetAdapterRss` command again.</span></span> <span data-ttu-id="dd7e3-119">При успешном выполнении возвращается следующий результат:</span><span class="sxs-lookup"><span data-stu-id="dd7e3-119">If successful, the following example output is returned:</span></span>

    ```powershell
    Name                    :Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : True
    ```

## <a name="linux-vm"></a><span data-ttu-id="dd7e3-120">Виртуальная машина Linux</span><span class="sxs-lookup"><span data-stu-id="dd7e3-120">Linux VM</span></span>

<span data-ttu-id="dd7e3-121">Функция RSS по умолчанию всегда включена на виртуальной машине Azure по управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="dd7e3-121">RSS is always enabled by default in an Azure Linux VM.</span></span> <span data-ttu-id="dd7e3-122">Ядра Linux, выпущенные после января 2017 года, включают новые параметры оптимизации сети, которые обеспечивают более высокую пропускную способность сети для виртуальной машины Linux.</span><span class="sxs-lookup"><span data-stu-id="dd7e3-122">Linux kernels released since January, 2017 include new network optimization options that enable a Linux VM to achieve higher network throughput.</span></span>

### <a name="ubuntu"></a><span data-ttu-id="dd7e3-123">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="dd7e3-123">Ubuntu</span></span>

<span data-ttu-id="dd7e3-124">Чтобы получить параметры оптимизации, сначала обновите систему до последней поддерживаемой версии состоянием на январь 2017 года:</span><span class="sxs-lookup"><span data-stu-id="dd7e3-124">In order to get the optimization, first update to the latest supported version, as of June 2017, which is:</span></span>
```json
"Publisher": "Canonical",
"Offer": "UbuntuServer",
"Sku": "16.04-LTS",
"Version": "latest"
```
<span data-ttu-id="dd7e3-125">Завершив обновление, выполните следующие команды, чтобы получить последнюю версию ядра:</span><span class="sxs-lookup"><span data-stu-id="dd7e3-125">After the update is complete, enter the following commands to get the latest kernel:</span></span>

```bash
apt-get -f install
apt-get --fix-missing install
apt-get clean
apt-get -y update
apt-get -y upgrade
```

<span data-ttu-id="dd7e3-126">Необязательная команда:</span><span class="sxs-lookup"><span data-stu-id="dd7e3-126">Optional command:</span></span>

`apt-get -y dist-upgrade`
#### <a name="ubuntu-azure-preview-kernel"></a><span data-ttu-id="dd7e3-127">Ядро предварительной версии Azure Ubuntu</span><span class="sxs-lookup"><span data-stu-id="dd7e3-127">Ubuntu Azure Preview kernel</span></span>
> [!WARNING]
> <span data-ttu-id="dd7e3-128">Это ядро предварительной версии Azure Linux может не отличаться таким же уровнем доступности и надежности, как общедоступные версии образов и ядер из Marketplace.</span><span class="sxs-lookup"><span data-stu-id="dd7e3-128">This Azure Linux Preview kernel may not have the same level of availability and reliability as Marketplace images and kernels that are in general availability release.</span></span> <span data-ttu-id="dd7e3-129">Это ядро не поддерживается, может иметь ограничения и может быть не таким надежным, как стандартное ядро.</span><span class="sxs-lookup"><span data-stu-id="dd7e3-129">The feature is not supported, may have constrained capabilities, and may not be as reliable as the default kernel.</span></span> <span data-ttu-id="dd7e3-130">Не используйте это ядро для производственных задач.</span><span class="sxs-lookup"><span data-stu-id="dd7e3-130">Do not use this kernel for production workloads.</span></span>

<span data-ttu-id="dd7e3-131">Существенно повысить пропускную способность можно за счет установки предложенного ядра Azure Linux.</span><span class="sxs-lookup"><span data-stu-id="dd7e3-131">Significant throughput performance can be achieved by installing the proposed Azure Linux kernel.</span></span> <span data-ttu-id="dd7e3-132">Чтобы попробовать поработать с этим ядром, добавьте в файл /etc/apt/sources.list следующую строку:</span><span class="sxs-lookup"><span data-stu-id="dd7e3-132">To try this kernel, add this line to /etc/apt/sources.list</span></span>

```bash
#add this to the end of /etc/apt/sources.list (requires elevation)
deb http://archive.ubuntu.com/ubuntu/ xenial-proposed restricted main multiverse universe
```

<span data-ttu-id="dd7e3-133">Затем выполните следующие команды (требуется доступ с правами root):</span><span class="sxs-lookup"><span data-stu-id="dd7e3-133">Then run these commands as root.</span></span>
```bash
apt-get update
apt-get install "linux-azure"
reboot
```

### <a name="centos"></a><span data-ttu-id="dd7e3-134">CentOS</span><span class="sxs-lookup"><span data-stu-id="dd7e3-134">CentOS</span></span>

<span data-ttu-id="dd7e3-135">Чтобы получить возможность оптимизации, сначала установите последнюю поддерживаемую версию системы. По состоянию на июль 2017 года последняя версия такая:</span><span class="sxs-lookup"><span data-stu-id="dd7e3-135">In order to get the optimization, first update to the latest supported version, as of July 2017, which is:</span></span>
```json
"Publisher": "OpenLogic",
"Offer": "CentOS",
"Sku": "7.3",
"Version": "latest"
```
<span data-ttu-id="dd7e3-136">После завершения обновления установите последнюю версию служб интеграции Linux (LIS).</span><span class="sxs-lookup"><span data-stu-id="dd7e3-136">After the update is complete, install the latest Linux Integration Services (LIS).</span></span>
<span data-ttu-id="dd7e3-137">Возможность оптимизации пропускной способности предусмотрена в службах LIS начиная с версии 4.2.2-2.</span><span class="sxs-lookup"><span data-stu-id="dd7e3-137">The throughput optimization is in LIS, starting from 4.2.2-2.</span></span> <span data-ttu-id="dd7e3-138">Введите следующие команды для установки LIS:</span><span class="sxs-lookup"><span data-stu-id="dd7e3-138">Enter the following commands to install LIS:</span></span>

```bash
sudo yum update
sudo reboot
sudo yum install microsoft-hyper-v
```

### <a name="red-hat"></a><span data-ttu-id="dd7e3-139">Red Hat</span><span class="sxs-lookup"><span data-stu-id="dd7e3-139">Red Hat</span></span>

<span data-ttu-id="dd7e3-140">Чтобы получить возможность оптимизации, сначала установите последнюю поддерживаемую версию системы. По состоянию на июль 2017 года последняя версия такая:</span><span class="sxs-lookup"><span data-stu-id="dd7e3-140">In order to get the optimization, first update to the latest supported version, as of July 2017, which is:</span></span>
```json
"Publisher": "RedHat"
"Offer": "RHEL"
"Sku": "7.3"
"Version": "7.3.2017071923"
```
<span data-ttu-id="dd7e3-141">После завершения обновления установите последнюю версию служб интеграции Linux (LIS).</span><span class="sxs-lookup"><span data-stu-id="dd7e3-141">After the update is complete, install the latest Linux Integration Services (LIS).</span></span>
<span data-ttu-id="dd7e3-142">Возможность оптимизации пропускной способности предусмотрена в службах LIS начиная с версии 4.2.</span><span class="sxs-lookup"><span data-stu-id="dd7e3-142">The throughput optimization is in LIS, starting from 4.2.</span></span> <span data-ttu-id="dd7e3-143">Выполните следующие команды, чтобы загрузить и установить LIS:</span><span class="sxs-lookup"><span data-stu-id="dd7e3-143">Enter the following commands to download and install LIS:</span></span>

```bash
mkdir lis4.2.2-2
cd lis4.2.2-2
wget https://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
tar xvzf lis-rpms-4.2.2-2.tar.gz
cd LISISO
install.sh #or upgrade.sh if prior LIS was previously installed
```

<span data-ttu-id="dd7e3-144">Дополнительные сведения о версии 4.2 служб интеграции Linux (LIS) для Hyper-V см. на [странице скачивания](https://www.microsoft.com/download/details.aspx?id=55106).</span><span class="sxs-lookup"><span data-stu-id="dd7e3-144">Learn more about Linux Integration Services Version 4.2 for Hyper-V by viewing the [download page](https://www.microsoft.com/download/details.aspx?id=55106).</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd7e3-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dd7e3-145">Next steps</span></span>
* <span data-ttu-id="dd7e3-146">Теперь, когда виртуальная машина оптимизирована, просмотрите результаты для своего сценария, используя сведения в статье [Проверка пропускной способности (NTTTCP)](virtual-network-bandwidth-testing.md).</span><span class="sxs-lookup"><span data-stu-id="dd7e3-146">Now that the VM is optimized, see the result with [Bandwidth/Throughput testing Azure VM](virtual-network-bandwidth-testing.md) for your scenario.</span></span>
* <span data-ttu-id="dd7e3-147">Дополнительные сведения см. в статье [Виртуальная сеть Azure: часто задаваемые вопросы](virtual-networks-faq.md).</span><span class="sxs-lookup"><span data-stu-id="dd7e3-147">Learn more with [Azure Virtual Network frequently asked questions (FAQ)](virtual-networks-faq.md)</span></span>
