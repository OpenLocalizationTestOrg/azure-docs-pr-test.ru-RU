---
title: "Здравствуйте, aaaOpen порты tooa виртуальной Машины с помощью портала Azure | Документы Microsoft"
description: "Узнайте, как tooopen порт / create tooyour конечной точки виртуальной Машины Windows с помощью модели развертывания диспетчера ресурсов hello в hello портала Azure"
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
ms.openlocfilehash: aba789c65254651899aa688f256fe616c3d0126d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-ports-tooa-virtual-machine-with-hello-azure-portal"></a><span data-ttu-id="96b77-103">Как tooopen порты tooa виртуальную машину с портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="96b77-103">How tooopen ports tooa virtual machine with hello Azure portal</span></span>
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a><span data-ttu-id="96b77-104">Быстрые команды</span><span class="sxs-lookup"><span data-stu-id="96b77-104">Quick commands</span></span>
<span data-ttu-id="96b77-105">Эти действия также можно [выполнить с помощью Azure PowerShell](nsg-quickstart-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="96b77-105">You can also [perform these steps using Azure PowerShell](nsg-quickstart-powershell.md).</span></span>

<span data-ttu-id="96b77-106">Сначала создайте группу безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="96b77-106">First, create your Network Security Group.</span></span> <span data-ttu-id="96b77-107">Выберите группу ресурсов в портале hello, выберите **добавить**, а затем найдите и выберите **сетевой группы безопасности**:</span><span class="sxs-lookup"><span data-stu-id="96b77-107">Select a resource group in hello portal, choose **Add**, then search for and select **Network security group**:</span></span>

![Добавление группы безопасности сети](./media/nsg-quickstart-portal/add-nsg.png)

<span data-ttu-id="96b77-109">Введите имя группы безопасности сети, выберите или создайте группу ресурсов и выберите расположение.</span><span class="sxs-lookup"><span data-stu-id="96b77-109">Enter a name for your Network Security Group, select or create a resource group, and select a location.</span></span> <span data-ttu-id="96b77-110">По завершении выберите **Создание**:</span><span class="sxs-lookup"><span data-stu-id="96b77-110">Select **Create** when finished:</span></span>

![Создание группы безопасности сети](./media/nsg-quickstart-portal/create-nsg.png)

<span data-ttu-id="96b77-112">Выберите созданную группу безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="96b77-112">Select your new Network Security Group.</span></span> <span data-ttu-id="96b77-113">Выберите «Правила для входящих подключений безопасности», а затем hello **добавить** кнопку toocreate правила:</span><span class="sxs-lookup"><span data-stu-id="96b77-113">Select 'Inbound security rules', then select hello **Add** button toocreate a rule:</span></span>

![Добавление правила для входящих подключений](./media/nsg-quickstart-portal/add-inbound-rule.png)

<span data-ttu-id="96b77-115">Выберите общий **службы** hello раскрывающегося меню, таких как *HTTP*.</span><span class="sxs-lookup"><span data-stu-id="96b77-115">Choose a common **Service** from hello drop-down menu, such as *HTTP*.</span></span> <span data-ttu-id="96b77-116">Можно также выбрать *настраиваемый* tooprovide toouse определенный порт.</span><span class="sxs-lookup"><span data-stu-id="96b77-116">You can also select *Custom* tooprovide a specific port toouse.</span></span> <span data-ttu-id="96b77-117">При необходимости, измените приоритет hello, или имя.</span><span class="sxs-lookup"><span data-stu-id="96b77-117">If desired, change hello priority or name.</span></span> <span data-ttu-id="96b77-118">Hello приоритет влияет на порядок hello, в котором применяются правила - числовое значение нижней hello hello, hello предыдущих hello применяется правило.</span><span class="sxs-lookup"><span data-stu-id="96b77-118">hello priority affects hello order in which rules are applied - hello lower hello numerical value, hello earlier hello rule is applied.</span></span> <span data-ttu-id="96b77-119">Можно также выбрать **Дополнительно** вверху hello этот экран tooenter конкретного источника IP-диапазон блока или порта, например.</span><span class="sxs-lookup"><span data-stu-id="96b77-119">You can also select **Advanced** at hello top of this screen tooenter a specific source IP block or port range, for example.</span></span> <span data-ttu-id="96b77-120">Когда будете готовы, выберите **ОК** toocreate hello правила:</span><span class="sxs-lookup"><span data-stu-id="96b77-120">When you are ready, select **OK** toocreate hello rule:</span></span>

![Создание правила для входящих подключений](./media/nsg-quickstart-portal/create-inbound-rule.png)

<span data-ttu-id="96b77-122">Последняя операция — tooassociate группы безопасности сети с подсетью или определенного сетевого интерфейса.</span><span class="sxs-lookup"><span data-stu-id="96b77-122">Your final step is tooassociate your Network Security Group with a subnet or a specific network interface.</span></span> <span data-ttu-id="96b77-123">Давайте связать hello сетевой группы безопасности с подсетью.</span><span class="sxs-lookup"><span data-stu-id="96b77-123">Let's associate hello Network Security Group with a subnet.</span></span> <span data-ttu-id="96b77-124">Выберите **Подсети**, а затем — **Привязать**:</span><span class="sxs-lookup"><span data-stu-id="96b77-124">Select **Subnets**, then choose **Associate**:</span></span>

![Связывание группы безопасности сети с подсетью](./media/nsg-quickstart-portal/associate-subnet.png)

<span data-ttu-id="96b77-126">Выберите виртуальную сеть, а затем выберите соответствующую подсеть hello:</span><span class="sxs-lookup"><span data-stu-id="96b77-126">Select your virtual network, and then select hello appropriate subnet:</span></span>

![Связывание группы безопасности сети с виртуальной сетью](./media/nsg-quickstart-portal/select-vnet-subnet.png)

<span data-ttu-id="96b77-128">Вы создали группу безопасности сети, создали правило для входящих подключений, которое пропускает трафик через порт 80, и связали эту группу с подсетью.</span><span class="sxs-lookup"><span data-stu-id="96b77-128">You have now created a Network Security Group, created an inbound rule that allows traffic on port 80, and associated it with a subnet.</span></span> <span data-ttu-id="96b77-129">Все виртуальные машины, подключение toothat подсети должны быть доступны через порт 80.</span><span class="sxs-lookup"><span data-stu-id="96b77-129">Any VMs you connect toothat subnet are reachable on port 80.</span></span>

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="96b77-130">Дополнительная информация о группах безопасности сети</span><span class="sxs-lookup"><span data-stu-id="96b77-130">More information on Network Security Groups</span></span>
<span data-ttu-id="96b77-131">Hello здесь Быстрые команды позволяют tooget вверх и работает с tooyour передачу трафика виртуальных Машин.</span><span class="sxs-lookup"><span data-stu-id="96b77-131">hello quick commands here allow you tooget up and running with traffic flowing tooyour VM.</span></span> <span data-ttu-id="96b77-132">Сетевые группы безопасности предоставляют много замечательных функций и гранулярности для управления доступа к ресурсам tooyour.</span><span class="sxs-lookup"><span data-stu-id="96b77-132">Network Security Groups provide many great features and granularity for controlling access tooyour resources.</span></span> <span data-ttu-id="96b77-133">[Здесь](../../virtual-network/virtual-networks-create-nsg-arm-ps.md)вы можете больше прочитать о создании группы безопасности сети и правил ACL.</span><span class="sxs-lookup"><span data-stu-id="96b77-133">You can read more about [creating a Network Security Group and ACL rules here](../../virtual-network/virtual-networks-create-nsg-arm-ps.md).</span></span>

<span data-ttu-id="96b77-134">Для веб-приложений с высокой доступностью необходимо поместить виртуальную машину за Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="96b77-134">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span></span> <span data-ttu-id="96b77-135">Подсистема балансировки нагрузки Hello распределяет трафик tooVMs, с группой безопасности сети, которая обеспечивает фильтрацию трафика.</span><span class="sxs-lookup"><span data-stu-id="96b77-135">hello load balancer distributes traffic tooVMs, with a Network Security Group that provides traffic filtering.</span></span> <span data-ttu-id="96b77-136">Дополнительные сведения см. в разделе [как баланс tooload Linux виртуальных машин в Azure toocreate приложение с высокой доступностью](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="96b77-136">For more information, see [How tooload balance Linux virtual machines in Azure toocreate a highly available application](tutorial-load-balancer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="96b77-137">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="96b77-137">Next steps</span></span>
<span data-ttu-id="96b77-138">В этом примере вы создали трафика tooallow HTTP простое правило.</span><span class="sxs-lookup"><span data-stu-id="96b77-138">In this example, you created a simple rule tooallow HTTP traffic.</span></span> <span data-ttu-id="96b77-139">Можно найти сведения о создании более подробные сред в hello в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="96b77-139">You can find information on creating more detailed environments in hello following articles:</span></span>

* [<span data-ttu-id="96b77-140">Общие сведения об Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="96b77-140">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="96b77-141">Группа безопасности сети</span><span class="sxs-lookup"><span data-stu-id="96b77-141">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)