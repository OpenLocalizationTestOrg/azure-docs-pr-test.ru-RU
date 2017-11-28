---
title: "пропускная способность сети виртуальной Машины aaaOptimize | Документы Microsoft"
description: "Узнайте, как виртуальная машина Azure toooptimize сетевой пропускной способности."
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
ms.openlocfilehash: a5cff2d0ab6e3553c3f90d99629521a431477de0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-network-throughput-for-azure-virtual-machines"></a><span data-ttu-id="d963d-103">Оптимизации пропускной способности сети для виртуальной машины Azure</span><span class="sxs-lookup"><span data-stu-id="d963d-103">Optimize network throughput for Azure virtual machines</span></span>

<span data-ttu-id="d963d-104">Виртуальные машины Azure имеют сетевые параметры по умолчанию, с помощью которых можно дополнительно оптимизировать пропускную способность сети.</span><span class="sxs-lookup"><span data-stu-id="d963d-104">Azure virtual machines (VM) have default network settings that can be further optimized for network throughput.</span></span> <span data-ttu-id="d963d-105">В этой статье описывается, как toooptimize сетевой пропускной способности для Microsoft Azure Windows и виртуальных машин Linux, включая основные распределения, например Ubuntu, CentOS и Red Hat.</span><span class="sxs-lookup"><span data-stu-id="d963d-105">This article describes how toooptimize network throughput for Microsoft Azure Windows and Linux VMs, including major distributions such as Ubuntu, CentOS and Red Hat.</span></span>

## <a name="windows-vm"></a><span data-ttu-id="d963d-106">Виртуальная машина Windows</span><span class="sxs-lookup"><span data-stu-id="d963d-106">Windows VM</span></span>

<span data-ttu-id="d963d-107">Если ВМ Windows поддерживается с [Accelerated сети](virtual-network-create-vm-accelerated-networking.md), включение этой функции будет hello оптимальную конфигурацию для пропускной способности.</span><span class="sxs-lookup"><span data-stu-id="d963d-107">If your Windows VM is supported with [Accelerated Networking](virtual-network-create-vm-accelerated-networking.md), enabling that feature would be hello optimal configuration for throughput.</span></span> <span data-ttu-id="d963d-108">Остальные виртуальные машины Windows, использующие масштабирование размера приема (RSS), могут иметь большую максимальную пропускную способность, чем виртуальная машина без RSS.</span><span class="sxs-lookup"><span data-stu-id="d963d-108">For all other Windows VMs, using Receive Side Scaling (RSS) can reach higher maximal throughput than a VM without RSS.</span></span> <span data-ttu-id="d963d-109">По умолчанию функция RSS может быть отключена на виртуальной машине Windows.</span><span class="sxs-lookup"><span data-stu-id="d963d-109">RSS may be disabled by default in a Windows VM.</span></span> <span data-ttu-id="d963d-110">Выполните следующие шаги toodetermine RSS, включен ли hello и tooenable его, если она отключена.</span><span class="sxs-lookup"><span data-stu-id="d963d-110">Complete hello following steps toodetermine whether RSS is enabled and tooenable it if it's disabled.</span></span>

1. <span data-ttu-id="d963d-111">Введите hello `Get-NetAdapterRss` toosee команду PowerShell, если для сетевого адаптера включена технология RSS.</span><span class="sxs-lookup"><span data-stu-id="d963d-111">Enter hello `Get-NetAdapterRss` PowerShell command toosee if RSS is enabled for a network adapter.</span></span> <span data-ttu-id="d963d-112">В hello следующий пример выходных данных, возвращенные hello `Get-NetAdapterRss`, не включена технология RSS.</span><span class="sxs-lookup"><span data-stu-id="d963d-112">In hello following example output returned from hello `Get-NetAdapterRss`, RSS is not enabled.</span></span>

    ```powershell
    Name                    : Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : False
    ```
2. <span data-ttu-id="d963d-113">Введите следующие команды tooenable RSS hello:</span><span class="sxs-lookup"><span data-stu-id="d963d-113">Enter hello following command tooenable RSS:</span></span>

    ```powershell
    Get-NetAdapter | % {Enable-NetAdapterRss -Name $_.Name}
    ```
    <span data-ttu-id="d963d-114">Предыдущая команда Hello не имеет выходных данных.</span><span class="sxs-lookup"><span data-stu-id="d963d-114">hello previous command does not have an output.</span></span> <span data-ttu-id="d963d-115">Команда Hello изменить параметры сетевого Адаптера, вызывая потери подключения временных около одной минуты.</span><span class="sxs-lookup"><span data-stu-id="d963d-115">hello command changed NIC settings, causing temporary connectivity loss for about one minute.</span></span> <span data-ttu-id="d963d-116">Диалоговое окно Reconnecting отображается во время потери подключения hello.</span><span class="sxs-lookup"><span data-stu-id="d963d-116">A Reconnecting dialog box appears during hello connectivity loss.</span></span> <span data-ttu-id="d963d-117">Обычно восстановление подключения после попытки третий hello.</span><span class="sxs-lookup"><span data-stu-id="d963d-117">Connectivity is typically restored after hello third attempt.</span></span>
3. <span data-ttu-id="d963d-118">Убедитесь, что RSS включена в hello виртуальной Машины, введя hello `Get-NetAdapterRss` еще раз.</span><span class="sxs-lookup"><span data-stu-id="d963d-118">Confirm that RSS is enabled in hello VM by entering hello `Get-NetAdapterRss` command again.</span></span> <span data-ttu-id="d963d-119">В случае успешного выполнения возвращается hello следующий пример выходных данных:</span><span class="sxs-lookup"><span data-stu-id="d963d-119">If successful, hello following example output is returned:</span></span>

    ```powershell
    Name                    :Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : True
    ```

## <a name="linux-vm"></a><span data-ttu-id="d963d-120">Виртуальная машина Linux</span><span class="sxs-lookup"><span data-stu-id="d963d-120">Linux VM</span></span>

<span data-ttu-id="d963d-121">Функция RSS по умолчанию всегда включена на виртуальной машине Azure по управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="d963d-121">RSS is always enabled by default in an Azure Linux VM.</span></span> <span data-ttu-id="d963d-122">Ядро Linux, выпущенные после января 2017 г. включает новые параметры оптимизации сети, позволяющие виртуальной Машине Linux tooachieve выше пропускную способность сети.</span><span class="sxs-lookup"><span data-stu-id="d963d-122">Linux kernels released since January, 2017 include new network optimization options that enable a Linux VM tooachieve higher network throughput.</span></span>

### <a name="ubuntu"></a><span data-ttu-id="d963d-123">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="d963d-123">Ubuntu</span></span>

<span data-ttu-id="d963d-124">В порядке tooget hello оптимизации необходимо сначала обновите версию toohello последней поддерживается, начиная с июня 2017 г., который является:</span><span class="sxs-lookup"><span data-stu-id="d963d-124">In order tooget hello optimization, first update toohello latest supported version, as of June 2017, which is:</span></span>
```json
"Publisher": "Canonical",
"Offer": "UbuntuServer",
"Sku": "16.04-LTS",
"Version": "latest"
```
<span data-ttu-id="d963d-125">После завершения обновления hello, введите следующие команды tooget hello последнюю ядра hello:</span><span class="sxs-lookup"><span data-stu-id="d963d-125">After hello update is complete, enter hello following commands tooget hello latest kernel:</span></span>

```bash
apt-get -f install
apt-get --fix-missing install
apt-get clean
apt-get -y update
apt-get -y upgrade
```

<span data-ttu-id="d963d-126">Необязательная команда:</span><span class="sxs-lookup"><span data-stu-id="d963d-126">Optional command:</span></span>

`apt-get -y dist-upgrade`
#### <a name="ubuntu-azure-preview-kernel"></a><span data-ttu-id="d963d-127">Ядро предварительной версии Azure Ubuntu</span><span class="sxs-lookup"><span data-stu-id="d963d-127">Ubuntu Azure Preview kernel</span></span>
> [!WARNING]
> <span data-ttu-id="d963d-128">Эта предварительная версия Linux Azure ядра не может иметь hello того же уровня доступности и надежности Marketplace образов и ядра, в целом доступности выпуска.</span><span class="sxs-lookup"><span data-stu-id="d963d-128">This Azure Linux Preview kernel may not have hello same level of availability and reliability as Marketplace images and kernels that are in general availability release.</span></span> <span data-ttu-id="d963d-129">функция Hello не поддерживается, могут ограничены возможности и не может быть как можно надежней ядра по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="d963d-129">hello feature is not supported, may have constrained capabilities, and may not be as reliable as hello default kernel.</span></span> <span data-ttu-id="d963d-130">Не используйте это ядро для производственных задач.</span><span class="sxs-lookup"><span data-stu-id="d963d-130">Do not use this kernel for production workloads.</span></span>

<span data-ttu-id="d963d-131">Значительно пропускную способность производительности достигается путем установки hello предложенные ядра Azure Linux.</span><span class="sxs-lookup"><span data-stu-id="d963d-131">Significant throughput performance can be achieved by installing hello proposed Azure Linux kernel.</span></span> <span data-ttu-id="d963d-132">tootry этот ядра, добавьте этот too/etc/apt/sources.list строки</span><span class="sxs-lookup"><span data-stu-id="d963d-132">tootry this kernel, add this line too/etc/apt/sources.list</span></span>

```bash
#add this toohello end of /etc/apt/sources.list (requires elevation)
deb http://archive.ubuntu.com/ubuntu/ xenial-proposed restricted main multiverse universe
```

<span data-ttu-id="d963d-133">Затем выполните следующие команды (требуется доступ с правами root):</span><span class="sxs-lookup"><span data-stu-id="d963d-133">Then run these commands as root.</span></span>
```bash
apt-get update
apt-get install "linux-azure"
reboot
```

### <a name="centos"></a><span data-ttu-id="d963d-134">CentOS</span><span class="sxs-lookup"><span data-stu-id="d963d-134">CentOS</span></span>

<span data-ttu-id="d963d-135">В порядке tooget hello оптимизации необходимо сначала обновите версию toohello последней поддерживается, начиная с июля 2017 г., который является:</span><span class="sxs-lookup"><span data-stu-id="d963d-135">In order tooget hello optimization, first update toohello latest supported version, as of July 2017, which is:</span></span>
```json
"Publisher": "OpenLogic",
"Offer": "CentOS",
"Sku": "7.3",
"Version": "latest"
```
<span data-ttu-id="d963d-136">После завершения обновления hello установки hello последние службы интеграции Linux (LIS).</span><span class="sxs-lookup"><span data-stu-id="d963d-136">After hello update is complete, install hello latest Linux Integration Services (LIS).</span></span>
<span data-ttu-id="d963d-137">оптимизации пропускной способности Hello находится в LIS, начиная с 4.2.2-2.</span><span class="sxs-lookup"><span data-stu-id="d963d-137">hello throughput optimization is in LIS, starting from 4.2.2-2.</span></span> <span data-ttu-id="d963d-138">Введите следующие команды tooinstall LIS hello:</span><span class="sxs-lookup"><span data-stu-id="d963d-138">Enter hello following commands tooinstall LIS:</span></span>

```bash
sudo yum update
sudo reboot
sudo yum install microsoft-hyper-v
```

### <a name="red-hat"></a><span data-ttu-id="d963d-139">Red Hat</span><span class="sxs-lookup"><span data-stu-id="d963d-139">Red Hat</span></span>

<span data-ttu-id="d963d-140">В порядке tooget hello оптимизации необходимо сначала обновите версию toohello последней поддерживается, начиная с июля 2017 г., который является:</span><span class="sxs-lookup"><span data-stu-id="d963d-140">In order tooget hello optimization, first update toohello latest supported version, as of July 2017, which is:</span></span>
```json
"Publisher": "RedHat"
"Offer": "RHEL"
"Sku": "7.3"
"Version": "7.3.2017071923"
```
<span data-ttu-id="d963d-141">После завершения обновления hello установки hello последние службы интеграции Linux (LIS).</span><span class="sxs-lookup"><span data-stu-id="d963d-141">After hello update is complete, install hello latest Linux Integration Services (LIS).</span></span>
<span data-ttu-id="d963d-142">оптимизации пропускной способности Hello находится в LIS, начиная с 4.2.</span><span class="sxs-lookup"><span data-stu-id="d963d-142">hello throughput optimization is in LIS, starting from 4.2.</span></span> <span data-ttu-id="d963d-143">Введите следующие команды toodownload hello и устанавливать LIS:</span><span class="sxs-lookup"><span data-stu-id="d963d-143">Enter hello following commands toodownload and install LIS:</span></span>

```bash
mkdir lis4.2.2-2
cd lis4.2.2-2
wget https://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
tar xvzf lis-rpms-4.2.2-2.tar.gz
cd LISISO
install.sh #or upgrade.sh if prior LIS was previously installed
```

<span data-ttu-id="d963d-144">Дополнительные сведения о 4.2 версию служб интеграции Linux для Hyper-V, просмотрев hello [страница загрузки](https://www.microsoft.com/download/details.aspx?id=55106).</span><span class="sxs-lookup"><span data-stu-id="d963d-144">Learn more about Linux Integration Services Version 4.2 for Hyper-V by viewing hello [download page](https://www.microsoft.com/download/details.aspx?id=55106).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d963d-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d963d-145">Next steps</span></span>
* <span data-ttu-id="d963d-146">Hello ВМ оптимизирован, см. статью hello результат с [пропускной способности и пропускной способности тестирования виртуальной Машины Azure](virtual-network-bandwidth-testing.md) для вашего сценария.</span><span class="sxs-lookup"><span data-stu-id="d963d-146">Now that hello VM is optimized, see hello result with [Bandwidth/Throughput testing Azure VM](virtual-network-bandwidth-testing.md) for your scenario.</span></span>
* <span data-ttu-id="d963d-147">Дополнительные сведения см. в статье [Виртуальная сеть Azure: часто задаваемые вопросы](virtual-networks-faq.md).</span><span class="sxs-lookup"><span data-stu-id="d963d-147">Learn more with [Azure Virtual Network frequently asked questions (FAQ)](virtual-networks-faq.md)</span></span>
