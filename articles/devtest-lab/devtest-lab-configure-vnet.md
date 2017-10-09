---
title: "aaaConfigure виртуальной сети в Azure DevTest Labs | Документы Microsoft"
description: "Узнайте, как tooconfigure существующую виртуальную сеть и подсети и использовать их на виртуальной машине с Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 6cda99c2-b87e-4047-90a0-5df10d8e9e14
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: tarcher
ms.openlocfilehash: a11ce8315e3c540e44aeacc9c5ee3dde014d4621
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-in-azure-devtest-labs"></a><span data-ttu-id="d0b83-103">Настройка виртуальной сети в Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="d0b83-103">Configure a virtual network in Azure DevTest Labs</span></span>
<span data-ttu-id="d0b83-104">Как описано в статье hello [добавить виртуальную Машину с артефакты лаборатории tooa](devtest-lab-add-vm-with-artifacts.md)при создании виртуальной Машины в лаборатории, можно указать настроенная виртуальная сеть.</span><span class="sxs-lookup"><span data-stu-id="d0b83-104">As explained in hello article, [Add a VM with artifacts tooa lab](devtest-lab-add-vm-with-artifacts.md), when you create a VM in a lab, you can specify a configured virtual network.</span></span> <span data-ttu-id="d0b83-105">Один сценарий для этого является hello при необходимости tooaccess ресурсам корпоративной сети из виртуальных машин с помощью виртуальной сети, которая была настроена с помощью ExpressRoute или VPN сайтами.</span><span class="sxs-lookup"><span data-stu-id="d0b83-105">One scenario for doing this is if you need tooaccess your corpnet resources from your VMs using hello virtual network that was configured with ExpressRoute or site-to-site VPN.</span></span> <span data-ttu-id="d0b83-106">Hello следующих разделах приведены как tooadd существующей виртуальной сети в параметры виртуальной сети лаборатории, чтобы он был доступен toochoose при создании виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="d0b83-106">hello following sections illustrate how tooadd your existing virtual network into a lab's Virtual Network settings so that it is available toochoose when creating VMs.</span></span>

## <a name="configure-a-virtual-network-for-a-lab-using-hello-azure-portal"></a><span data-ttu-id="d0b83-107">Настройка виртуальной сети для лаборатории, используя hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="d0b83-107">Configure a virtual network for a lab using hello Azure portal</span></span>
<span data-ttu-id="d0b83-108">Hello следующие шаги содержат пошаговые инструкции по добавлению существующей виртуальной сети (и подсети) tooa лаборатории, чтобы его можно использовать при создании виртуальной Машины в hello же лаборатории.</span><span class="sxs-lookup"><span data-stu-id="d0b83-108">hello following steps walk you through adding an existing virtual network (and subnet) tooa lab so that it can be used when creating a VM in hello same lab.</span></span> 

1. <span data-ttu-id="d0b83-109">Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="d0b83-109">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="d0b83-110">Выберите **более служб**, а затем выберите **DevTest Labs** из списка hello.</span><span class="sxs-lookup"><span data-stu-id="d0b83-110">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="d0b83-111">Выберите из списка hello лабораториям hello требуемой лаборатории.</span><span class="sxs-lookup"><span data-stu-id="d0b83-111">From hello list of labs, select hello desired lab.</span></span> 
4. <span data-ttu-id="d0b83-112">В колонке hello лаборатории выберите **конфигурации**.</span><span class="sxs-lookup"><span data-stu-id="d0b83-112">On hello lab's blade, select **Configuration**.</span></span>
5. <span data-ttu-id="d0b83-113">В лаборатории hello **конфигурации** колонке выберите **виртуальные сети**.</span><span class="sxs-lookup"><span data-stu-id="d0b83-113">On hello lab's **Configuration** blade, select **Virtual networks**.</span></span>
6. <span data-ttu-id="d0b83-114">На hello **виртуальные сети** колонки, отображается список виртуальных сетей, настроенных для текущей лаборатории hello, а также виртуальной сети по умолчанию hello, который создается для лаборатории.</span><span class="sxs-lookup"><span data-stu-id="d0b83-114">On hello **Virtual networks** blade, you see a list of virtual networks configured for hello current lab as well as hello default virtual network that is created for your lab.</span></span> 
7. <span data-ttu-id="d0b83-115">Щелкните **+ Добавить**.</span><span class="sxs-lookup"><span data-stu-id="d0b83-115">Select **+ Add**.</span></span>
   
    ![Добавление существующей виртуальной сети лаборатории tooyour](./media/devtest-lab-configure-vnet/lab-settings-vnet-add.png)
8. <span data-ttu-id="d0b83-117">На hello **виртуальная сеть** колонке выберите **[выберите виртуальную сеть]**.</span><span class="sxs-lookup"><span data-stu-id="d0b83-117">On hello **Virtual network** blade, select **[Select virtual network]**.</span></span>
   
    ![Выбор существующей виртуальной сети](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet1.png)
9. <span data-ttu-id="d0b83-119">На hello **виртуальной сети выберите** колонки, выберите hello требуемой виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="d0b83-119">On hello **Choose virtual network** blade, select hello desired virtual network.</span></span> <span data-ttu-id="d0b83-120">Hello колонке показывает все hello виртуальными сетями, которые находятся в группе hello же региона в подписке hello hello лаборатории.</span><span class="sxs-lookup"><span data-stu-id="d0b83-120">hello blade shows all hello virtual networks that are under hello same region in hello subscription as hello lab.</span></span>  
10. <span data-ttu-id="d0b83-121">После выбора виртуальной сети, возвращаются toohello **виртуальная сеть** выберите подсеть hello в списке hello hello нижней части колонки hello.</span><span class="sxs-lookup"><span data-stu-id="d0b83-121">After selecting a virtual network, you are returned toohello **Virtual network** Click hello subnet in hello list at hello bottom of hello blade.</span></span>

    ![Список подсетей](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet2.png)
    
    <span data-ttu-id="d0b83-123">Откроется колонка подсети лаборатории Hello.</span><span class="sxs-lookup"><span data-stu-id="d0b83-123">hello Lab Subnet blade is displayed.</span></span>

    ![Колонка "Lab Subnet" (Подсеть лаборатории)](./media/devtest-lab-configure-vnet/lab-subnet.png)

11. <span data-ttu-id="d0b83-125">Укажите **Lab subnet name** (Имя подсети лаборатории).</span><span class="sxs-lookup"><span data-stu-id="d0b83-125">Specify a **Lab subnet name**.</span></span>
12. <span data-ttu-id="d0b83-126">Выберите tooallow toobe подсети, используемых в лаборатории Создание виртуальной Машины **используется при создании виртуальной машины**.</span><span class="sxs-lookup"><span data-stu-id="d0b83-126">tooallow a subnet toobe used in lab VM creation, select **Use in virtual machine creation**.</span></span>
13. <span data-ttu-id="d0b83-127">tooenable [общих общедоступный IP-адрес](devtest-lab-shared-ip.md)выберите **включить общую общедоступный IP-адрес**.</span><span class="sxs-lookup"><span data-stu-id="d0b83-127">tooenable a [shared public IP address](devtest-lab-shared-ip.md), select **Enable shared public IP**.</span></span>
14. <span data-ttu-id="d0b83-128">Выберите tooallow общих IP-адресов в подсети, **разрешение на создание открытый IP**.</span><span class="sxs-lookup"><span data-stu-id="d0b83-128">tooallow public IP addresses in a subnet, select **Allow public IP creation**.</span></span>
15. <span data-ttu-id="d0b83-129">В hello **максимум виртуальных машин на пользователя** укажите hello максимальное виртуальных машин на пользователя для каждой подсети.</span><span class="sxs-lookup"><span data-stu-id="d0b83-129">In hello **Maximum virtual machines per user** field, specify hello maximum VMs per user for each subnet.</span></span> <span data-ttu-id="d0b83-130">Чтобы разрешить использовать неограниченное число виртуальных машин, оставьте это поле пустым.</span><span class="sxs-lookup"><span data-stu-id="d0b83-130">If you want an unrestricted number of VMs, leave this field blank.</span></span>
16. <span data-ttu-id="d0b83-131">Выберите **ОК** tooclose hello подсети лаборатории колонку.</span><span class="sxs-lookup"><span data-stu-id="d0b83-131">Select **OK** tooclose hello Lab Subnet blade.</span></span>
17. <span data-ttu-id="d0b83-132">Выберите **Сохранить** tooclose hello виртуальной сети колонку.</span><span class="sxs-lookup"><span data-stu-id="d0b83-132">Select **Save** tooclose hello Virtual network blade.</span></span>
18. <span data-ttu-id="d0b83-133">Теперь, когда hello виртуальная сеть настроена, ее можно выбрать при создании виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="d0b83-133">Now that hello virtual network is configured, it can be selected when creating a VM.</span></span> 
    <span data-ttu-id="d0b83-134">toosee как toocreate виртуальной Машины и указания виртуальной сети см. в статье toohello [добавить виртуальную Машину с артефакты лаборатории tooa](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="d0b83-134">toosee how toocreate a VM and specify a virtual network, refer toohello article, [Add a VM with artifacts tooa lab](devtest-lab-add-vm-with-artifacts.md).</span></span> 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="d0b83-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d0b83-135">Next steps</span></span>
<span data-ttu-id="d0b83-136">После добавления hello требуемого виртуальной сети лаборатории tooyour hello следующим шагом является слишком[добавления виртуальных Машин лаборатории tooyour](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="d0b83-136">Once you have added hello desired virtual network tooyour lab, hello next step is too[add a VM tooyour lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

