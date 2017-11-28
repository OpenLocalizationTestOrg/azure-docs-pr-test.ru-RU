---
title: "Как сбросить сетевой интерфейс для виртуальной машины Azure под управлением Windows | Документация Майкрософт"
description: "В этой статье показано, как сбросить сетевой интерфейс для виртуальной машины Azure под управлением Windows."
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: genlin
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: genli
ms.openlocfilehash: 220e426be20086841854d89831f6c9d67529867f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-reset-network-interface-for-azure-windows-vm"></a><span data-ttu-id="8f548-103">Как сбросить сетевой интерфейс для виртуальной машины Azure под управлением Windows</span><span class="sxs-lookup"><span data-stu-id="8f548-103">How to reset network interface for Azure Windows VM</span></span> 

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="8f548-104">Вы не можете подключиться к виртуальной машине Microsoft Azure под управлением Windows после того, как отключили стандартный сетевой интерфейс (NIC) или установили статический IP-адрес для NIC вручную.</span><span class="sxs-lookup"><span data-stu-id="8f548-104">You cannot connect to Microsoft Azure Windows Virtual Machine (VM) after you disable the default Network Interface (NIC) or manually sets a static IP for the NIC.</span></span> <span data-ttu-id="8f548-105">В этой статье показано, как сбросить сетевой интерфейс для виртуальной машины Azure под управлением Windows, что устранит проблему удаленного подключения.</span><span class="sxs-lookup"><span data-stu-id="8f548-105">This article shows how to reset the network interface for Azure Windows VM, which will resolve the remote connection issue.</span></span>

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]
## <a name="reset-network-interface"></a><span data-ttu-id="8f548-106">Сброс сетевого интерфейса</span><span class="sxs-lookup"><span data-stu-id="8f548-106">Reset network interface</span></span>

### <a name="for-classic-vms"></a><span data-ttu-id="8f548-107">Классические виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="8f548-107">For Classic VMs</span></span>

<span data-ttu-id="8f548-108">Чтобы сбросить сетевой интерфейс, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="8f548-108">To reset network interface, follow these steps:</span></span>

1.  <span data-ttu-id="8f548-109">Перейдите на [портал Azure]( https://ms.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8f548-109">Go to the [Azure portal]( https://ms.portal.azure.com).</span></span>
2.  <span data-ttu-id="8f548-110">Выберите **Виртуальные машины (классика)**.</span><span class="sxs-lookup"><span data-stu-id="8f548-110">Select **Virtual Machines (Classic)**.</span></span>
3.  <span data-ttu-id="8f548-111">Выберите задействованную виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="8f548-111">Select the affected Virtual Machine.</span></span>
4.  <span data-ttu-id="8f548-112">Выберите **IP-адреса**.</span><span class="sxs-lookup"><span data-stu-id="8f548-112">Select **IP addresses**.</span></span>
5.  <span data-ttu-id="8f548-113">Если для **назначения частного IP-адреса** не установлено значение **Статический**, установите **его**.</span><span class="sxs-lookup"><span data-stu-id="8f548-113">If the **Private IP assignment**  is not  **Static**, change it to **Static**.</span></span>
6.  <span data-ttu-id="8f548-114">Изменение **IP-адреса** на другой, который доступен в подсети.</span><span class="sxs-lookup"><span data-stu-id="8f548-114">Change the **IP address** to another IP address that is available in the Subnet.</span></span>
7.  <span data-ttu-id="8f548-115">Щелкните "Сохранить".</span><span class="sxs-lookup"><span data-stu-id="8f548-115">Select Save.</span></span>
8.  <span data-ttu-id="8f548-116">Виртуальная машина будет перезапущена, чтобы инициализировать новый NIC в системе.</span><span class="sxs-lookup"><span data-stu-id="8f548-116">The virtual machine will restart to initialize the new NIC to the system.</span></span>
9.  <span data-ttu-id="8f548-117">Попробуйте подключиться к компьютеру по протоколу удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="8f548-117">Try to RDP to your machine.</span></span> <span data-ttu-id="8f548-118">В случае успешного подключения при необходимости можно изменить частный IP-адрес на исходный</span><span class="sxs-lookup"><span data-stu-id="8f548-118">If successful, you can change the Private IP address back to the original if you would like.</span></span> <span data-ttu-id="8f548-119">или использовать прежний.</span><span class="sxs-lookup"><span data-stu-id="8f548-119">Otherwise, you can keep it.</span></span> 

### <a name="for-vms-deployed-in-resource-group-model"></a><span data-ttu-id="8f548-120">Виртуальные машины, развернутые в модели группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="8f548-120">For VMs deployed in Resource group model</span></span>

1.  <span data-ttu-id="8f548-121">Перейдите на [портал Azure]( https://ms.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8f548-121">Go to the [Azure portal]( https://ms.portal.azure.com).</span></span>
2.  <span data-ttu-id="8f548-122">Выберите задействованную виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="8f548-122">Select the affected Virtual Machine.</span></span>
3.  <span data-ttu-id="8f548-123">Выберите **Сетевые интерфейсы**.</span><span class="sxs-lookup"><span data-stu-id="8f548-123">Select **Network Interfaces**.</span></span>
4.  <span data-ttu-id="8f548-124">Выберите сетевой интерфейс, связанный с компьютером.</span><span class="sxs-lookup"><span data-stu-id="8f548-124">Select the Network Interface associated with your machine</span></span>
5.  <span data-ttu-id="8f548-125">Щелкните **IP configurations** (Конфигурации IP).</span><span class="sxs-lookup"><span data-stu-id="8f548-125">Select **IP configurations**.</span></span>
6.  <span data-ttu-id="8f548-126">Выберите IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="8f548-126">Select the IP.</span></span> 
7.  <span data-ttu-id="8f548-127">Если для **назначения частного IP-адреса** не установлено значение **Статический**, установите **его**.</span><span class="sxs-lookup"><span data-stu-id="8f548-127">If the **Private IP assignment**  is not  **Static**, change it to **Static**.</span></span>
8.  <span data-ttu-id="8f548-128">Изменение **IP-адреса** на другой, который доступен в подсети.</span><span class="sxs-lookup"><span data-stu-id="8f548-128">Change the **IP address** to another IP address that is available in the Subnet.</span></span>
9. <span data-ttu-id="8f548-129">Виртуальная машина будет перезапущена, чтобы инициализировать новый NIC в системе.</span><span class="sxs-lookup"><span data-stu-id="8f548-129">The virtual machine will restart to initialize the new NIC to the system.</span></span>
10. <span data-ttu-id="8f548-130">Попробуйте подключиться к компьютеру по протоколу удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="8f548-130">Try to RDP to your machine.</span></span> <span data-ttu-id="8f548-131">В случае успешного подключения при необходимости можно изменить частный IP-адрес на исходный</span><span class="sxs-lookup"><span data-stu-id="8f548-131">If successful, you can change the Private IP address back to the original if you would like.</span></span> <span data-ttu-id="8f548-132">или использовать прежний.</span><span class="sxs-lookup"><span data-stu-id="8f548-132">Otherwise, you can keep it.</span></span> 

## <a name="delete-the-unavailable-nics"></a><span data-ttu-id="8f548-133">Удаление недоступных сетевых интерфейсов</span><span class="sxs-lookup"><span data-stu-id="8f548-133">Delete the unavailable NICs</span></span>
<span data-ttu-id="8f548-134">После подключения к компьютеру с помощью удаленного рабочего стола необходимо удалить устарелые сетевые интерфейсы во избежание возможных проблем.</span><span class="sxs-lookup"><span data-stu-id="8f548-134">After you can remote desktop to the machine, you must delete the old NICs to avoid the potential problem:</span></span>

1.  <span data-ttu-id="8f548-135">Откройте диспетчер устройств.</span><span class="sxs-lookup"><span data-stu-id="8f548-135">Open Device Manager.</span></span>
2.  <span data-ttu-id="8f548-136">Выберите **Просмотреть** > **Показать скрытые устройства**.</span><span class="sxs-lookup"><span data-stu-id="8f548-136">Select **View** > **Show hidden devices**.</span></span>
3.  <span data-ttu-id="8f548-137">Выберите **Сетевые адаптеры**.</span><span class="sxs-lookup"><span data-stu-id="8f548-137">Select **Network Adapters**.</span></span> 
4.  <span data-ttu-id="8f548-138">Найдите адаптеры с именем "Сетевой адаптер Hyper-V (Майкрософт)".</span><span class="sxs-lookup"><span data-stu-id="8f548-138">Check for the adapters named as "Microsoft Hyper-V Network Adapter".</span></span>
5.  <span data-ttu-id="8f548-139">Вы можете увидеть неактивный адаптер.</span><span class="sxs-lookup"><span data-stu-id="8f548-139">You might see an unavailable adapter that is grayed out.</span></span> <span data-ttu-id="8f548-140">Щелкните его правой кнопкой, а затем выберите "Удалить".</span><span class="sxs-lookup"><span data-stu-id="8f548-140">Right-click the adapter and then select Uninstall.</span></span>

    ![изображение сетевого интерфейса](media/reset-network-interface/nicpage.png)

    > [!NOTE]
    > <span data-ttu-id="8f548-142">Удалите только отключенные адаптеры с именем "Сетевой адаптер Hyper-V (Майкрософт)".</span><span class="sxs-lookup"><span data-stu-id="8f548-142">Only uninstall the unavailable adapters that have the name "Microsoft Hyper-V Network Adapter".</span></span> <span data-ttu-id="8f548-143">Удаление других скрытых адаптеров может привести к дополнительным проблемам.</span><span class="sxs-lookup"><span data-stu-id="8f548-143">If you uninstall any of the other hidden adapters, it could cause additional issues.</span></span>
    >
    >

6.  <span data-ttu-id="8f548-144">Теперь все отключенные адаптеры должны быть удалены из системы.</span><span class="sxs-lookup"><span data-stu-id="8f548-144">Now all unavailable adapter should be cleared out from your system.</span></span>