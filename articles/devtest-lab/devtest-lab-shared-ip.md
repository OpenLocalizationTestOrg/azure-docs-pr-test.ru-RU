---
title: "aaaUnderstand общих IP-адресов в Azure DevTest Labs | Документы Microsoft"
description: "Узнайте, как Azure DevTest Labs использует общий IP адресов toominimize hello открытый IP адресов требуется tooaccess лаборатории виртуальных машин."
services: devtest-lab
documentationcenter: na
author: camsoper
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: casoper
ms.openlocfilehash: 8756410117a9d550d567d372174bf1ea96703c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="understand-shared-ip-addresses-in-azure-devtest-labs"></a><span data-ttu-id="bb460-103">Общие IP-адреса в Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="bb460-103">Understand shared IP addresses in Azure DevTest Labs</span></span>

<span data-ttu-id="bb460-104">Позволяет лаборатории Azure DevTest Labs виртуальные машины общую папку hello же открытый IP-адрес toominimize hello номер открытого IP адресов требуется tooaccess лабораторной отдельных виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="bb460-104">Azure DevTest Labs lets lab VMs share hello same public IP address toominimize hello number of public IP addresses required tooaccess your individual lab VMs.</span></span>  <span data-ttu-id="bb460-105">В этой статье описывается принцип работы общих IP-адресов и варианты их настройки.</span><span class="sxs-lookup"><span data-stu-id="bb460-105">This article describes how shared IPs work and their related configuration options.</span></span>

## <a name="shared-ip-setting"></a><span data-ttu-id="bb460-106">Настройка общих IP-адресов</span><span class="sxs-lookup"><span data-stu-id="bb460-106">Shared IP setting</span></span>

<span data-ttu-id="bb460-107">Когда создается лаборатория, она размещается в подсети виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="bb460-107">When you create a lab, it resides in a subnet of a virtual network.</span></span>  <span data-ttu-id="bb460-108">По умолчанию, созданными данной подсети **включить общую общедоступный IP-адрес** значение слишком*Да*.</span><span class="sxs-lookup"><span data-stu-id="bb460-108">By default, this subnet is created with **Enable shared public IP** set too*Yes*.</span></span>  <span data-ttu-id="bb460-109">Эта конфигурация создает один общий IP-адрес для hello всей подсети.</span><span class="sxs-lookup"><span data-stu-id="bb460-109">This configuration creates one public IP address for hello entire subnet.</span></span>  <span data-ttu-id="bb460-110">Дополнительные сведения о настройке виртуальных сетей и подсетей см. в статье [Настройка виртуальной сети в Azure DevTest Labs](devtest-lab-configure-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="bb460-110">For more information about configuring virtual networks and subnets, see [Configure a virtual network in Azure DevTest Labs](devtest-lab-configure-vnet.md).</span></span>

![Создание подсети лаборатории](media/devtest-lab-shared-ip/lab-subnet.png)

<span data-ttu-id="bb460-112">Вы можете включить этот параметр для всех имеющихся лабораторий, выбрав **Configuration and Policies (Конфигурация и политики) > Virtual Networks (Виртуальные сети)**.</span><span class="sxs-lookup"><span data-stu-id="bb460-112">For existing labs, you can enable this option by selecting **Configuration and policies > Virtual Networks**.</span></span> <span data-ttu-id="bb460-113">Затем выберите виртуальную сеть из списка hello и выберите **ВКЛЮЧИТЬ общие ОБЩЕДОСТУПНЫЙ IP-адрес** для выбранной подсети.</span><span class="sxs-lookup"><span data-stu-id="bb460-113">Then, select a virtual network from hello list and choose **ENABLE SHARED PUBLIC IP** for a selected subnet.</span></span> <span data-ttu-id="bb460-114">Если вы не хотите tooshare общедоступный IP-адрес через лаборатории виртуальных машин, можно также отключить этот параметр в любой лаборатории.</span><span class="sxs-lookup"><span data-stu-id="bb460-114">You can also disable this option in any lab if you don't want tooshare a public IP address across lab VMs.</span></span>

<span data-ttu-id="bb460-115">Все виртуальные машины, созданные в этой лаборатории по умолчанию toousing имеет общий IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="bb460-115">Any VMs created in this lab default toousing a shared IP.</span></span>  <span data-ttu-id="bb460-116">При создании виртуальной Машины hello, этот параметр можно наблюдать в hello **Дополнительные параметры** колонке под **конфигурацию IP-адресов**.</span><span class="sxs-lookup"><span data-stu-id="bb460-116">When creating hello VM, this setting can be observed in hello **Advanced settings** blade under **IP address configuration**.</span></span>

![Создание виртуальной машины](media/devtest-lab-shared-ip/new-vm.png)

- <span data-ttu-id="bb460-118">**Общий.** Все виртуальные машины, созданные в качестве **общедоступных**, помещаются в одну группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="bb460-118">**Shared:** All VMs created as **Shared** are placed into one resource group (RG).</span></span> <span data-ttu-id="bb460-119">Один IP-адрес, назначенный для этой группы Маршрутизации и все виртуальные машины в hello RG будет использовать этот IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="bb460-119">A single IP address is assigned for that RG and all VMs in hello RG will use that IP address.</span></span>
- <span data-ttu-id="bb460-120">**Общедоступный.** Каждая созданная виртуальная машина имеет личный IP-адрес и создается в собственной группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="bb460-120">**Public:** Every VM you create has its own IP address and is created in its own resource group.</span></span>
- <span data-ttu-id="bb460-121">**Частный.** Каждая созданная виртуальная машина использует частный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="bb460-121">**Private:** Every VM you create uses a private IP address.</span></span> <span data-ttu-id="bb460-122">Не будет возможности tooconnect toothis виртуальную Машину непосредственно из hello Интернета с помощью удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="bb460-122">You will not be able tooconnect toothis VM directly from hello internet with Remote Desktop.</span></span>

<span data-ttu-id="bb460-123">Виртуальную Машину с общего IP включен при добавлении toohello подсети, DevTest Labs автоматически добавляет подсистему балансировки нагрузки tooa ВМ hello и назначает номер TCP-порта на hello общедоступный IP-адрес пересылки toohello RDP-порту на hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="bb460-123">Whenever a VM with shared IP enabled is added toohello subnet, DevTest Labs automatically adds hello VM tooa load balancer and assigns a TCP port number on hello public IP address, forwarding toohello RDP port on hello VM.</span></span>  

## <a name="using-hello-shared-ip"></a><span data-ttu-id="bb460-124">Использование hello общих IP</span><span class="sxs-lookup"><span data-stu-id="bb460-124">Using hello shared IP</span></span>

- <span data-ttu-id="bb460-125">**Пользователи Linux:** toohello SSH виртуальной Машины с помощью hello IP-адрес или полное доменное имя, за которым следует двоеточие, следуют hello порта.</span><span class="sxs-lookup"><span data-stu-id="bb460-125">**Linux users:** SSH toohello VM by using hello IP address or fully qualified domain name, followed by a colon, followed by hello port.</span></span> <span data-ttu-id="bb460-126">Например, ниже рисунке hello, hello RDP адресов toohello tooconnect виртуальная машина — `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.</span><span class="sxs-lookup"><span data-stu-id="bb460-126">For example, in hello image below, hello RDP address tooconnect toohello VM is `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.</span></span>

  ![Пример виртуальной машины](media/devtest-lab-shared-ip/vm-info.png)

- <span data-ttu-id="bb460-128">**Пользователи Windows:** выберите hello **Connect** кнопку hello Azure портала toodownload предварительно настроенных RDP-файл и получить доступ к hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="bb460-128">**Windows users:** Select hello **Connect** button on hello Azure portal toodownload a pre-configured RDP file and access hello VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bb460-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bb460-129">Next steps</span></span>

* [<span data-ttu-id="bb460-130">Управление всеми политиками лаборатории в Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="bb460-130">Define lab policies in Azure DevTest Labs</span></span>](devtest-lab-set-lab-policy.md)
* [<span data-ttu-id="bb460-131">Настройка виртуальной сети в Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="bb460-131">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md)





