---
title: "Настройка виртуальной сети в Azure DevTest Labs | Документация Майкрософт"
description: "Узнайте, как настроить существующую виртуальную сеть и подсеть и использовать их на виртуальной машине в Azure DevTest Labs."
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
ms.openlocfilehash: 848752085729df7d98a3a4b7be36d894c12cd033
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-virtual-network-in-azure-devtest-labs"></a><span data-ttu-id="6bc09-103">Настройка виртуальной сети в Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="6bc09-103">Configure a virtual network in Azure DevTest Labs</span></span>
<span data-ttu-id="6bc09-104">Как описано в статье [Добавление виртуальной машины с артефактами в лабораторию](devtest-lab-add-vm-with-artifacts.md), при создании виртуальной машины в лаборатории можно указать настроенную виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="6bc09-104">As explained in the article, [Add a VM with artifacts to a lab](devtest-lab-add-vm-with-artifacts.md), when you create a VM in a lab, you can specify a configured virtual network.</span></span> <span data-ttu-id="6bc09-105">Это может потребоваться, например, когда необходим доступ к ресурсам корпоративной сети с виртуальных машин через виртуальную сеть, которая была настроена с помощью ExpressRoute или через VPN-подключение типа "сеть — сеть".</span><span class="sxs-lookup"><span data-stu-id="6bc09-105">One scenario for doing this is if you need to access your corpnet resources from your VMs using the virtual network that was configured with ExpressRoute or site-to-site VPN.</span></span> <span data-ttu-id="6bc09-106">В следующих разделах показано, как добавить существующую виртуальную сеть в настройки виртуальной сети лаборатории, чтобы она предлагалась для выбора при создании виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="6bc09-106">The following sections illustrate how to add your existing virtual network into a lab's Virtual Network settings so that it is available to choose when creating VMs.</span></span>

## <a name="configure-a-virtual-network-for-a-lab-using-the-azure-portal"></a><span data-ttu-id="6bc09-107">Настройка виртуальной сети для лаборатории с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="6bc09-107">Configure a virtual network for a lab using the Azure portal</span></span>
<span data-ttu-id="6bc09-108">Ниже пошагово описывается процедура добавления существующей виртуальной сети (и подсети) в лабораторию, чтобы ее можно было использовать при создании виртуальной машины в этой лаборатории.</span><span class="sxs-lookup"><span data-stu-id="6bc09-108">The following steps walk you through adding an existing virtual network (and subnet) to a lab so that it can be used when creating a VM in the same lab.</span></span> 

1. <span data-ttu-id="6bc09-109">Войдите на [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="6bc09-109">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="6bc09-110">Щелкните **Больше служб**, а затем выберите в списке **DevTest Labs**.</span><span class="sxs-lookup"><span data-stu-id="6bc09-110">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="6bc09-111">Из списка лабораторий выберите нужную лабораторию.</span><span class="sxs-lookup"><span data-stu-id="6bc09-111">From the list of labs, select the desired lab.</span></span> 
4. <span data-ttu-id="6bc09-112">В колонке лаборатории выберите **Конфигурация**.</span><span class="sxs-lookup"><span data-stu-id="6bc09-112">On the lab's blade, select **Configuration**.</span></span>
5. <span data-ttu-id="6bc09-113">В колонке **Конфигурация** лаборатории выберите **Виртуальные сети**.</span><span class="sxs-lookup"><span data-stu-id="6bc09-113">On the lab's **Configuration** blade, select **Virtual networks**.</span></span>
6. <span data-ttu-id="6bc09-114">В колонке **Виртуальные сети** отобразится список виртуальных сетей, настроенных для текущей лаборатории, а также виртуальная сеть по умолчанию, созданная для лаборатории.</span><span class="sxs-lookup"><span data-stu-id="6bc09-114">On the **Virtual networks** blade, you see a list of virtual networks configured for the current lab as well as the default virtual network that is created for your lab.</span></span> 
7. <span data-ttu-id="6bc09-115">Щелкните **+ Добавить**.</span><span class="sxs-lookup"><span data-stu-id="6bc09-115">Select **+ Add**.</span></span>
   
    ![Добавление существующей виртуальной сети в лабораторию](./media/devtest-lab-configure-vnet/lab-settings-vnet-add.png)
8. <span data-ttu-id="6bc09-117">В колонке **Виртуальная сеть** выберите **[Выбрать виртуальную сеть]**.</span><span class="sxs-lookup"><span data-stu-id="6bc09-117">On the **Virtual network** blade, select **[Select virtual network]**.</span></span>
   
    ![Выбор существующей виртуальной сети](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet1.png)
9. <span data-ttu-id="6bc09-119">В колонке **Выбор виртуальной сети** выберите нужную виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="6bc09-119">On the **Choose virtual network** blade, select the desired virtual network.</span></span> <span data-ttu-id="6bc09-120">В колонке отображаются все виртуальные сети, которые находятся в том же регионе подписки, что и лаборатория.</span><span class="sxs-lookup"><span data-stu-id="6bc09-120">The blade shows all the virtual networks that are under the same region in the subscription as the lab.</span></span>  
10. <span data-ttu-id="6bc09-121">После выбора виртуальной сети вы вернетесь к колонке **Виртуальная сеть**. Выберите подсеть из списка в нижней части колонки.</span><span class="sxs-lookup"><span data-stu-id="6bc09-121">After selecting a virtual network, you are returned to the **Virtual network** Click the subnet in the list at the bottom of the blade.</span></span>

    ![Список подсетей](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet2.png)
    
    <span data-ttu-id="6bc09-123">Отобразится колонка "Lab Subnet" (Подсеть лаборатории).</span><span class="sxs-lookup"><span data-stu-id="6bc09-123">The Lab Subnet blade is displayed.</span></span>

    ![Колонка "Lab Subnet" (Подсеть лаборатории)](./media/devtest-lab-configure-vnet/lab-subnet.png)

11. <span data-ttu-id="6bc09-125">Укажите **Lab subnet name** (Имя подсети лаборатории).</span><span class="sxs-lookup"><span data-stu-id="6bc09-125">Specify a **Lab subnet name**.</span></span>
12. <span data-ttu-id="6bc09-126">Чтобы подсеть можно было использовать при создании виртуальной машины лаборатории, выберите **Use in virtual machine creation** (Использовать при создании виртуальной машины).</span><span class="sxs-lookup"><span data-stu-id="6bc09-126">To allow a subnet to be used in lab VM creation, select **Use in virtual machine creation**.</span></span>
13. <span data-ttu-id="6bc09-127">Чтобы включить [совместное использование общедоступного IP-адреса](devtest-lab-shared-ip.md), выберите **Enable shared public IP** (Включить совместное использование общедоступного IP-адреса).</span><span class="sxs-lookup"><span data-stu-id="6bc09-127">To enable a [shared public IP address](devtest-lab-shared-ip.md), select **Enable shared public IP**.</span></span>
14. <span data-ttu-id="6bc09-128">Чтобы разрешить использование общедоступных IP-адресов в подсети, выберите **Allow public IP creation** (Разрешить создание общедоступных IP-адресов).</span><span class="sxs-lookup"><span data-stu-id="6bc09-128">To allow public IP addresses in a subnet, select **Allow public IP creation**.</span></span>
15. <span data-ttu-id="6bc09-129">В поле **Maximum virtual machines per user** (Максимальное число виртуальных машин на пользователя) укажите максимальное число виртуальных машин на пользователя для каждой подсети.</span><span class="sxs-lookup"><span data-stu-id="6bc09-129">In the **Maximum virtual machines per user** field, specify the maximum VMs per user for each subnet.</span></span> <span data-ttu-id="6bc09-130">Чтобы разрешить использовать неограниченное число виртуальных машин, оставьте это поле пустым.</span><span class="sxs-lookup"><span data-stu-id="6bc09-130">If you want an unrestricted number of VMs, leave this field blank.</span></span>
16. <span data-ttu-id="6bc09-131">Нажмите кнопку **ОК**, чтобы закрыть колонку "Lab Subnet" (Подсеть лаборатории).</span><span class="sxs-lookup"><span data-stu-id="6bc09-131">Select **OK** to close the Lab Subnet blade.</span></span>
17. <span data-ttu-id="6bc09-132">Нажмите кнопку **Сохранить**, чтобы закрыть колонку "Виртуальная сеть".</span><span class="sxs-lookup"><span data-stu-id="6bc09-132">Select **Save** to close the Virtual network blade.</span></span>
18. <span data-ttu-id="6bc09-133">После настройки виртуальной сети ее можно выбирать при создании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="6bc09-133">Now that the virtual network is configured, it can be selected when creating a VM.</span></span> 
    <span data-ttu-id="6bc09-134">Сведения о создании виртуальной машины и о выборе виртуальной сети см. в статье [Добавление виртуальной машины с артефактами в лабораторию в Azure DevTest Labs](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="6bc09-134">To see how to create a VM and specify a virtual network, refer to the article, [Add a VM with artifacts to a lab](devtest-lab-add-vm-with-artifacts.md).</span></span> 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="6bc09-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6bc09-135">Next steps</span></span>
<span data-ttu-id="6bc09-136">После добавления в лабораторию нужной виртуальной сети следует [добавить виртуальную машину в лабораторию](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="6bc09-136">Once you have added the desired virtual network to your lab, the next step is to [add a VM to your lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

