---
title: "aaaHow tooreset сетевого интерфейса для виртуальной Машины Windows Azure | Документы Microsoft"
description: "Показано, как tooreset сетевой интерфейс для виртуальной Машины Windows Azure"
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
ms.openlocfilehash: 1b653820927ef4c3bb8f384a7e752846a8be3da9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-network-interface-for-azure-windows-vm"></a><span data-ttu-id="56b82-103">Как tooreset сетевой интерфейс для виртуальной Машины Windows Azure</span><span class="sxs-lookup"><span data-stu-id="56b82-103">How tooreset network interface for Azure Windows VM</span></span> 

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="56b82-104">Не удается подключиться к виртуальной машине Windows Azure (ВМ) tooMicrosoft после отключения по умолчанию hello сетевого интерфейса (NIC) или вручную устанавливает статический IP-адрес для сетевого адаптера hello.</span><span class="sxs-lookup"><span data-stu-id="56b82-104">You cannot connect tooMicrosoft Azure Windows Virtual Machine (VM) after you disable hello default Network Interface (NIC) or manually sets a static IP for hello NIC.</span></span> <span data-ttu-id="56b82-105">В этой статье показано, как tooreset hello сетевого интерфейса для виртуальной Машины Windows Azure, которая hello удаленного подключения проблема будет устранена.</span><span class="sxs-lookup"><span data-stu-id="56b82-105">This article shows how tooreset hello network interface for Azure Windows VM, which will resolve hello remote connection issue.</span></span>

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]
## <a name="reset-network-interface"></a><span data-ttu-id="56b82-106">Сброс сетевого интерфейса</span><span class="sxs-lookup"><span data-stu-id="56b82-106">Reset network interface</span></span>

### <a name="for-classic-vms"></a><span data-ttu-id="56b82-107">Классические виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="56b82-107">For Classic VMs</span></span>

<span data-ttu-id="56b82-108">tooreset сетевого интерфейса, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="56b82-108">tooreset network interface, follow these steps:</span></span>

1.  <span data-ttu-id="56b82-109">Go toohello [портал Azure]( https://ms.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="56b82-109">Go toohello [Azure portal]( https://ms.portal.azure.com).</span></span>
2.  <span data-ttu-id="56b82-110">Выберите **Виртуальные машины (классика)**.</span><span class="sxs-lookup"><span data-stu-id="56b82-110">Select **Virtual Machines (Classic)**.</span></span>
3.  <span data-ttu-id="56b82-111">Выберите hello влияет на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="56b82-111">Select hello affected Virtual Machine.</span></span>
4.  <span data-ttu-id="56b82-112">Выберите **IP-адреса**.</span><span class="sxs-lookup"><span data-stu-id="56b82-112">Select **IP addresses**.</span></span>
5.  <span data-ttu-id="56b82-113">Если hello **частный IP-адрес назначения** не **статических**, измените его слишком**статических**.</span><span class="sxs-lookup"><span data-stu-id="56b82-113">If hello **Private IP assignment**  is not  **Static**, change it too**Static**.</span></span>
6.  <span data-ttu-id="56b82-114">Изменение hello **IP-адрес** tooanother IP-адрес, доступный в подсети hello.</span><span class="sxs-lookup"><span data-stu-id="56b82-114">Change hello **IP address** tooanother IP address that is available in hello Subnet.</span></span>
7.  <span data-ttu-id="56b82-115">Щелкните "Сохранить".</span><span class="sxs-lookup"><span data-stu-id="56b82-115">Select Save.</span></span>
8.  <span data-ttu-id="56b82-116">Hello виртуальная машина будет перезагружена toohello системы tooinitialize hello новый сетевой Адаптер.</span><span class="sxs-lookup"><span data-stu-id="56b82-116">hello virtual machine will restart tooinitialize hello new NIC toohello system.</span></span>
9.  <span data-ttu-id="56b82-117">Попробуйте tooRDP tooyour машины.</span><span class="sxs-lookup"><span data-stu-id="56b82-117">Try tooRDP tooyour machine.</span></span> <span data-ttu-id="56b82-118">В случае успешного выполнения при желании можно изменить hello частный IP-адрес адрес обратной toohello исходного.</span><span class="sxs-lookup"><span data-stu-id="56b82-118">If successful, you can change hello Private IP address back toohello original if you would like.</span></span> <span data-ttu-id="56b82-119">или использовать прежний.</span><span class="sxs-lookup"><span data-stu-id="56b82-119">Otherwise, you can keep it.</span></span> 

### <a name="for-vms-deployed-in-resource-group-model"></a><span data-ttu-id="56b82-120">Виртуальные машины, развернутые в модели группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="56b82-120">For VMs deployed in Resource group model</span></span>

1.  <span data-ttu-id="56b82-121">Go toohello [портал Azure]( https://ms.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="56b82-121">Go toohello [Azure portal]( https://ms.portal.azure.com).</span></span>
2.  <span data-ttu-id="56b82-122">Выберите hello влияет на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="56b82-122">Select hello affected Virtual Machine.</span></span>
3.  <span data-ttu-id="56b82-123">Выберите **Сетевые интерфейсы**.</span><span class="sxs-lookup"><span data-stu-id="56b82-123">Select **Network Interfaces**.</span></span>
4.  <span data-ttu-id="56b82-124">Выберите hello сетевого интерфейса, связанного с компьютера</span><span class="sxs-lookup"><span data-stu-id="56b82-124">Select hello Network Interface associated with your machine</span></span>
5.  <span data-ttu-id="56b82-125">Щелкните **IP configurations** (Конфигурации IP).</span><span class="sxs-lookup"><span data-stu-id="56b82-125">Select **IP configurations**.</span></span>
6.  <span data-ttu-id="56b82-126">Выберите IP-адрес hello.</span><span class="sxs-lookup"><span data-stu-id="56b82-126">Select hello IP.</span></span> 
7.  <span data-ttu-id="56b82-127">Если hello **частный IP-адрес назначения** не **статических**, измените его слишком**статических**.</span><span class="sxs-lookup"><span data-stu-id="56b82-127">If hello **Private IP assignment**  is not  **Static**, change it too**Static**.</span></span>
8.  <span data-ttu-id="56b82-128">Изменение hello **IP-адрес** tooanother IP-адрес, доступный в подсети hello.</span><span class="sxs-lookup"><span data-stu-id="56b82-128">Change hello **IP address** tooanother IP address that is available in hello Subnet.</span></span>
9. <span data-ttu-id="56b82-129">Hello виртуальная машина будет перезагружена toohello системы tooinitialize hello новый сетевой Адаптер.</span><span class="sxs-lookup"><span data-stu-id="56b82-129">hello virtual machine will restart tooinitialize hello new NIC toohello system.</span></span>
10. <span data-ttu-id="56b82-130">Попробуйте tooRDP tooyour машины.</span><span class="sxs-lookup"><span data-stu-id="56b82-130">Try tooRDP tooyour machine.</span></span> <span data-ttu-id="56b82-131">В случае успешного выполнения при желании можно изменить hello частный IP-адрес адрес обратной toohello исходного.</span><span class="sxs-lookup"><span data-stu-id="56b82-131">If successful, you can change hello Private IP address back toohello original if you would like.</span></span> <span data-ttu-id="56b82-132">или использовать прежний.</span><span class="sxs-lookup"><span data-stu-id="56b82-132">Otherwise, you can keep it.</span></span> 

## <a name="delete-hello-unavailable-nics"></a><span data-ttu-id="56b82-133">Удалить hello недоступен сетевых адаптеров</span><span class="sxs-lookup"><span data-stu-id="56b82-133">Delete hello unavailable NICs</span></span>
<span data-ttu-id="56b82-134">После можно удаленного рабочего стола toohello машины необходимо удалить hello старых сетевых адаптеров tooavoid hello потенциальная проблема:</span><span class="sxs-lookup"><span data-stu-id="56b82-134">After you can remote desktop toohello machine, you must delete hello old NICs tooavoid hello potential problem:</span></span>

1.  <span data-ttu-id="56b82-135">Откройте диспетчер устройств.</span><span class="sxs-lookup"><span data-stu-id="56b82-135">Open Device Manager.</span></span>
2.  <span data-ttu-id="56b82-136">Выберите **Просмотреть** > **Показать скрытые устройства**.</span><span class="sxs-lookup"><span data-stu-id="56b82-136">Select **View** > **Show hidden devices**.</span></span>
3.  <span data-ttu-id="56b82-137">Выберите **Сетевые адаптеры**.</span><span class="sxs-lookup"><span data-stu-id="56b82-137">Select **Network Adapters**.</span></span> 
4.  <span data-ttu-id="56b82-138">Проверьте наличие hello адаптеров с именем «Сетевой адаптер Microsoft Hyper-V».</span><span class="sxs-lookup"><span data-stu-id="56b82-138">Check for hello adapters named as "Microsoft Hyper-V Network Adapter".</span></span>
5.  <span data-ttu-id="56b82-139">Вы можете увидеть неактивный адаптер. Щелкните правой кнопкой мыши hello адаптера, а затем выберите Удалить.</span><span class="sxs-lookup"><span data-stu-id="56b82-139">You might see an unavailable adapter that is grayed out. Right-click hello adapter and then select Uninstall.</span></span>

    ![изображение Hello hello сетевого Адаптера](media/reset-network-interface/nicpage.png)

    > [!NOTE]
    > <span data-ttu-id="56b82-141">Удаление только hello недоступен адаптеры с именами hello «Сетевой адаптер Microsoft Hyper-V».</span><span class="sxs-lookup"><span data-stu-id="56b82-141">Only uninstall hello unavailable adapters that have hello name "Microsoft Hyper-V Network Adapter".</span></span> <span data-ttu-id="56b82-142">При удалении любой hello другие скрытые адаптеры, может возникнуть дополнительные проблемы.</span><span class="sxs-lookup"><span data-stu-id="56b82-142">If you uninstall any of hello other hidden adapters, it could cause additional issues.</span></span>
    >
    >

6.  <span data-ttu-id="56b82-143">Теперь все отключенные адаптеры должны быть удалены из системы.</span><span class="sxs-lookup"><span data-stu-id="56b82-143">Now all unavailable adapter should be cleared out from your system.</span></span>