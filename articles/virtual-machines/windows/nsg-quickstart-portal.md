---
title: "Открытие портов для виртуальной машины Linux с помощью портала Azure | Документация Майкрософт"
description: "Узнайте, как открыть порт или создать конечную точку для виртуальной машины Windows, используя модель развертывания с помощью Resource Manager и портал Azure."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: f7cf0319-5ee7-435e-8f94-c484bf5ee6f1
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: 33bc0be0aeae6d0276fd8999b9ac0a010e3067ba
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-open-ports-to-a-virtual-machine-with-the-azure-portal"></a><span data-ttu-id="8a77f-103">Как открыть порты для виртуальной машины Windows с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="8a77f-103">How to open ports to a virtual machine with the Azure portal</span></span>
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a><span data-ttu-id="8a77f-104">Быстрые команды</span><span class="sxs-lookup"><span data-stu-id="8a77f-104">Quick commands</span></span>
<span data-ttu-id="8a77f-105">Эти действия также можно [выполнить с помощью Azure PowerShell](nsg-quickstart-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="8a77f-105">You can also [perform these steps using Azure PowerShell](nsg-quickstart-powershell.md).</span></span>

<span data-ttu-id="8a77f-106">Сначала создайте группу безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="8a77f-106">First, create your Network Security Group.</span></span> <span data-ttu-id="8a77f-107">Выберите группу ресурсов на портале, щелкните **Добавить**, а затем найдите и выберите **Группа безопасности сети**:</span><span class="sxs-lookup"><span data-stu-id="8a77f-107">Select a resource group in the portal, choose **Add**, then search for and select **Network security group**:</span></span>

![Добавление группы безопасности сети](./media/nsg-quickstart-portal/add-nsg.png)

<span data-ttu-id="8a77f-109">Введите имя группы безопасности сети, выберите или создайте группу ресурсов и выберите расположение.</span><span class="sxs-lookup"><span data-stu-id="8a77f-109">Enter a name for your Network Security Group, select or create a resource group, and select a location.</span></span> <span data-ttu-id="8a77f-110">По завершении выберите **Создание**:</span><span class="sxs-lookup"><span data-stu-id="8a77f-110">Select **Create** when finished:</span></span>

![Создание группы безопасности сети](./media/nsg-quickstart-portal/create-nsg.png)

<span data-ttu-id="8a77f-112">Выберите созданную группу безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="8a77f-112">Select your new Network Security Group.</span></span> <span data-ttu-id="8a77f-113">Выберите "Правила безопасности для входящего трафика" и нажмите кнопку **Добавить**, чтобы создать правило:</span><span class="sxs-lookup"><span data-stu-id="8a77f-113">Select 'Inbound security rules', then select the **Add** button to create a rule:</span></span>

![Добавление правила для входящих подключений](./media/nsg-quickstart-portal/add-inbound-rule.png)

<span data-ttu-id="8a77f-115">Выберите общую **службу** в раскрывающемся меню, например *HTTP*.</span><span class="sxs-lookup"><span data-stu-id="8a77f-115">Choose a common **Service** from the drop-down menu, such as *HTTP*.</span></span> <span data-ttu-id="8a77f-116">Кроме того, можно выбрать *Настраиваемый*, чтобы указать конкретный порт для использования.</span><span class="sxs-lookup"><span data-stu-id="8a77f-116">You can also select *Custom* to provide a specific port to use.</span></span> <span data-ttu-id="8a77f-117">При необходимости измените приоритет или имя.</span><span class="sxs-lookup"><span data-stu-id="8a77f-117">If desired, change the priority or name.</span></span> <span data-ttu-id="8a77f-118">Приоритет влияет на порядок, в котором применяются правила: чем ниже числовое значение, тем раньше применяется правило.</span><span class="sxs-lookup"><span data-stu-id="8a77f-118">The priority affects the order in which rules are applied - the lower the numerical value, the earlier the rule is applied.</span></span> <span data-ttu-id="8a77f-119">В верхней части экрана можно также выбрать **Дополнительно** для ввода определенного блока исходных IP-адресов или, например, диапазона портов.</span><span class="sxs-lookup"><span data-stu-id="8a77f-119">You can also select **Advanced** at the top of this screen to enter a specific source IP block or port range, for example.</span></span> <span data-ttu-id="8a77f-120">Когда все будет готово, нажмите кнопку **ОК** для создания правила:</span><span class="sxs-lookup"><span data-stu-id="8a77f-120">When you are ready, select **OK** to create the rule:</span></span>

![Создание правила для входящих подключений](./media/nsg-quickstart-portal/create-inbound-rule.png)

<span data-ttu-id="8a77f-122">Последний шаг — связывание группы безопасности сети с подсетью или определенным сетевым интерфейсом.</span><span class="sxs-lookup"><span data-stu-id="8a77f-122">Your final step is to associate your Network Security Group with a subnet or a specific network interface.</span></span> <span data-ttu-id="8a77f-123">Давайте свяжем группу безопасности сети с подсетью.</span><span class="sxs-lookup"><span data-stu-id="8a77f-123">Let's associate the Network Security Group with a subnet.</span></span> <span data-ttu-id="8a77f-124">Выберите **Подсети**, а затем — **Привязать**:</span><span class="sxs-lookup"><span data-stu-id="8a77f-124">Select **Subnets**, then choose **Associate**:</span></span>

![Связывание группы безопасности сети с подсетью](./media/nsg-quickstart-portal/associate-subnet.png)

<span data-ttu-id="8a77f-126">Выберите виртуальную сеть, а затем — соответствующую подсеть.</span><span class="sxs-lookup"><span data-stu-id="8a77f-126">Select your virtual network, and then select the appropriate subnet:</span></span>

![Связывание группы безопасности сети с виртуальной сетью](./media/nsg-quickstart-portal/select-vnet-subnet.png)

<span data-ttu-id="8a77f-128">Вы создали группу безопасности сети, создали правило для входящих подключений, которое пропускает трафик через порт 80, и связали эту группу с подсетью.</span><span class="sxs-lookup"><span data-stu-id="8a77f-128">You have now created a Network Security Group, created an inbound rule that allows traffic on port 80, and associated it with a subnet.</span></span> <span data-ttu-id="8a77f-129">Любые виртуальные машины, подключаемые к этой подсети, будут доступны через порт 80.</span><span class="sxs-lookup"><span data-stu-id="8a77f-129">Any VMs you connect to that subnet are reachable on port 80.</span></span>

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="8a77f-130">Дополнительная информация о группах безопасности сети</span><span class="sxs-lookup"><span data-stu-id="8a77f-130">More information on Network Security Groups</span></span>
<span data-ttu-id="8a77f-131">Приведенные здесь быстрые команды позволят настроить трафик, поступающий в виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="8a77f-131">The quick commands here allow you to get up and running with traffic flowing to your VM.</span></span> <span data-ttu-id="8a77f-132">Группы безопасности сети предоставляют множество полезных функций и всевозможные настройки для управления доступом к ресурсам.</span><span class="sxs-lookup"><span data-stu-id="8a77f-132">Network Security Groups provide many great features and granularity for controlling access to your resources.</span></span> <span data-ttu-id="8a77f-133">[Здесь](../../virtual-network/virtual-networks-create-nsg-arm-ps.md)вы можете больше прочитать о создании группы безопасности сети и правил ACL.</span><span class="sxs-lookup"><span data-stu-id="8a77f-133">You can read more about [creating a Network Security Group and ACL rules here](../../virtual-network/virtual-networks-create-nsg-arm-ps.md).</span></span>

<span data-ttu-id="8a77f-134">Для веб-приложений с высокой доступностью необходимо поместить виртуальную машину за Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="8a77f-134">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span></span> <span data-ttu-id="8a77f-135">Балансировщик нагрузки распределяет трафик между виртуальными машинами с группой безопасности сети, обеспечивающей фильтрацию трафика.</span><span class="sxs-lookup"><span data-stu-id="8a77f-135">The load balancer distributes traffic to VMs, with a Network Security Group that provides traffic filtering.</span></span> <span data-ttu-id="8a77f-136">Подробные сведения см. в статье [Балансировка нагрузки виртуальных машин Windows в Azure для создания высокодоступного приложения](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="8a77f-136">For more information, see [How to load balance Linux virtual machines in Azure to create a highly available application](tutorial-load-balancer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8a77f-137">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8a77f-137">Next steps</span></span>
<span data-ttu-id="8a77f-138">В этом примере создано простое правило, разрешающее трафик HTTP.</span><span class="sxs-lookup"><span data-stu-id="8a77f-138">In this example, you created a simple rule to allow HTTP traffic.</span></span> <span data-ttu-id="8a77f-139">Информацию о создании более детализированных сред можно найти в следующих статьях.</span><span class="sxs-lookup"><span data-stu-id="8a77f-139">You can find information on creating more detailed environments in the following articles:</span></span>

* [<span data-ttu-id="8a77f-140">Общие сведения об Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8a77f-140">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="8a77f-141">Группа безопасности сети</span><span class="sxs-lookup"><span data-stu-id="8a77f-141">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)