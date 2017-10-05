---
title: "Создание групп безопасности сети с помощью портала Azure | Документация Майкрософт"
description: "Узнайте, как создавать и развертывать группы безопасности сети с помощью портала Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 5bc8fc2e-1e81-40e2-8231-0484cd5605cb
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 865032f350735d35668bb199ccf1ef3f0fae81de
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-network-security-groups-using-the-azure-portal"></a><span data-ttu-id="d6e79-103">Создание групп безопасности сети с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="d6e79-103">Create network security groups using the Azure portal</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="d6e79-104">В этой статье описывается модель развертывания с использованием менеджера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d6e79-104">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="d6e79-105">Вы также можете [создавать группы безопасности сети с помощью классической модели развертывания](virtual-networks-create-nsg-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="d6e79-105">You can also [create NSGs in the classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="d6e79-106">Для приведенных ниже примеров команд PowerShell требуется уже созданная простая среда, основанная на приведенном выше сценарии.</span><span class="sxs-lookup"><span data-stu-id="d6e79-106">The sample PowerShell commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="d6e79-107">Чтобы выполнять команды в том виде, в котором они представлены в этом документе, сначала создайте тестовую среду, развернув [этот шаблон](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), нажмите **Deploy to Azure**(Развернуть в Azure), при необходимости замените значения параметров по умолчанию и следуйте указаниям на портале.</span><span class="sxs-lookup"><span data-stu-id="d6e79-107">If you want to run the commands as they are displayed in this document, first build the test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span> <span data-ttu-id="d6e79-108">В описанных ниже действиях используйте **RG-NSG** в качестве имени группы ресурсов, в которой был развернут шаблон.</span><span class="sxs-lookup"><span data-stu-id="d6e79-108">The steps below use **RG-NSG** as the name of the resource group the template was deployed to.</span></span>

## <a name="create-the-nsg-frontend-nsg"></a><span data-ttu-id="d6e79-109">Создание группы безопасности сети NSG-FrontEnd</span><span class="sxs-lookup"><span data-stu-id="d6e79-109">Create the NSG-FrontEnd NSG</span></span>
<span data-ttu-id="d6e79-110">Чтобы создать группу безопасности сети **NSG-FrontEnd** , как показано в описанном выше сценарии, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="d6e79-110">To create the **NSG-FrontEnd** NSG as shown in the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="d6e79-111">В браузере откройте адрес http://portal.azure.com и войдите с помощью учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="d6e79-111">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="d6e79-112">Щелкните **Обзор >** > **Сетевые группы безопасности**.</span><span class="sxs-lookup"><span data-stu-id="d6e79-112">Click **Browse >** > **Network Security Groups**.</span></span>
   
    ![Портал Azure — группы безопасности сети](./media/virtual-networks-create-nsg-arm-pportal/figure11.png)
3. <span data-ttu-id="d6e79-114">В колонке **Сетевые группы безопасности** выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="d6e79-114">In the **Network security groups** blade, click **Add**.</span></span>
   
    ![Портал Azure — группы безопасности сети](./media/virtual-networks-create-nsg-arm-pportal/figure12.png)
4. <span data-ttu-id="d6e79-116">В колонке **Создание группы безопасности сети** создайте группу безопасности *NSG-FrontEnd* в группе ресурсов *RG-NSG*, а затем щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="d6e79-116">In the **Create network security group** blade, create an NSG named *NSG-FrontEnd* in the *RG-NSG* resource group, and then click **Create**.</span></span>
   
    ![Портал Azure — группы безопасности сети](./media/virtual-networks-create-nsg-arm-pportal/figure13.png)

## <a name="create-rules-in-an-existing-nsg"></a><span data-ttu-id="d6e79-118">Создание правил в существующей сетевой группе безопасности</span><span class="sxs-lookup"><span data-stu-id="d6e79-118">Create rules in an existing NSG</span></span>
<span data-ttu-id="d6e79-119">Чтобы создать правила в существующей группе безопасности сети с помощью портала Azure, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="d6e79-119">To create rules in an existing NSG from the Azure portal, follow the steps below.</span></span>

1. <span data-ttu-id="d6e79-120">Щелкните **Обзор >** > **Сетевые группы безопасности**.</span><span class="sxs-lookup"><span data-stu-id="d6e79-120">Click **Browse >** > **Network security groups**.</span></span>
2. <span data-ttu-id="d6e79-121">В списке групп выберите **NSG-FrontEnd** > **Правила безопасности для входящего трафика**</span><span class="sxs-lookup"><span data-stu-id="d6e79-121">In the list of NSGs, click **NSG-FrontEnd** > **Inbound security rules**</span></span>
   
    ![Портал Azure — NSG-FrontEnd](./media/virtual-networks-create-nsg-arm-pportal/figure2.png)
3. <span data-ttu-id="d6e79-123">В списке **Правила безопасности для входящего трафика**, нажмите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="d6e79-123">In the list of **Inbound security rules**, click **Add**.</span></span>
   
    ![Портал Azure — добавление правила](./media/virtual-networks-create-nsg-arm-pportal/figure3.png)
4. <span data-ttu-id="d6e79-125">В колонке **Добавление правила безопасности для входящего трафика** создайте правило под названием *web-rule* с приоритетом *200*, которое разрешает доступ по протоколу *TCP* к порту *80* на любой виртуальной машине из любого источника, и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d6e79-125">In the **Add inbound security rule** blade, create a rule named *web-rule* with priority of *200* allowing access via *TCP* to port *80* to any VM from any source, and then click **OK**.</span></span> <span data-ttu-id="d6e79-126">Обратите внимание, что для большинства этих параметров уже заданы значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d6e79-126">Notice that most of these settings are default values already.</span></span>
   
    ![Портал Azure — параметры правила](./media/virtual-networks-create-nsg-arm-pportal/figure4.png)
5. <span data-ttu-id="d6e79-128">Через несколько секунд новое правило появится в сетевой группе безопасности.</span><span class="sxs-lookup"><span data-stu-id="d6e79-128">After a few seconds you will see the new rule in the NSG.</span></span>
   
    ![Портал Azure — новое правило](./media/virtual-networks-create-nsg-arm-pportal/figure5.png)
6. <span data-ttu-id="d6e79-130">Повторите действия до шага 6, чтобы создать правило входящих подключений *rdp-rule* с приоритетом *250*, которое разрешает доступ через *TCP*-порт *3389* к любой виртуальной машине из любого источника.</span><span class="sxs-lookup"><span data-stu-id="d6e79-130">Repeat steps  to 6 to create an inbound rule named *rdp-rule* with a priority of *250* allowing access via *TCP* to port *3389* to any VM from any source.</span></span>

## <a name="associate-the-nsg-to-the-frontend-subnet"></a><span data-ttu-id="d6e79-131">Связывание группы безопасности сети с подсетью FrontEnd</span><span class="sxs-lookup"><span data-stu-id="d6e79-131">Associate the NSG to the FrontEnd subnet</span></span>
1. <span data-ttu-id="d6e79-132">Щелкните **Обзор >** > **Группы ресурсов** > **RG NSG**.</span><span class="sxs-lookup"><span data-stu-id="d6e79-132">Click **Browse >** > **Resource groups** > **RG-NSG**.</span></span>
2. <span data-ttu-id="d6e79-133">В колонке **RG-NSG** выберите **...** > **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="d6e79-133">In the **RG-NSG** blade, click **...** > **TestVNet**.</span></span>
   
    ![Портал Azure — TestVNet](./media/virtual-networks-create-nsg-arm-pportal/figure14.png)
3. <span data-ttu-id="d6e79-135">В колонке **Параметры** выберите пункты **Подсети** > **FrontEnd** > **Группа безопасности сети** > **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="d6e79-135">In the **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **NSG-FrontEnd**.</span></span>
   
    ![Портал Azure — параметры подсети](./media/virtual-networks-create-nsg-arm-pportal/figure15.png)
4. <span data-ttu-id="d6e79-137">В колонке **FrontEnd** нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="d6e79-137">In the **FrontEnd** blade, click **Save**.</span></span>
   
    ![Портал Azure — параметры подсети](./media/virtual-networks-create-nsg-arm-pportal/figure16.png)

## <a name="create-the-nsg-backend-nsg"></a><span data-ttu-id="d6e79-139">Создание группы безопасности сети NSG-BackEnd</span><span class="sxs-lookup"><span data-stu-id="d6e79-139">Create the NSG-BackEnd NSG</span></span>
<span data-ttu-id="d6e79-140">Чтобы создать группу безопасности сети **NSG-BackEnd** и связать ее с подсетью **BackEnd**, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="d6e79-140">To create the **NSG-BackEnd** NSG and associate it to the **BackEnd** subnet, follow the steps below.</span></span>

1. <span data-ttu-id="d6e79-141">Повторите шаги раздела [Создание группы безопасности сети NSG-FrontEnd](#Create-the-NSG-FrontEnd-NSG) , чтобы создать группу безопасности сети *NSG-FrontEnd*</span><span class="sxs-lookup"><span data-stu-id="d6e79-141">Repeat the steps in [Create the NSG-FrontEnd NSG](#Create-the-NSG-FrontEnd-NSG) to create an NSG named *NSG-BackEnd*</span></span>
2. <span data-ttu-id="d6e79-142">Повторите шаги раздела [Создание правил в существующей сетевой группе безопасности](#Create-rules-in-an-existing-NSG) , чтобы создать правила **входящих подключений** , приведенные в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="d6e79-142">Repeat the steps in [Create rules in an existing NSG](#Create-rules-in-an-existing-NSG) to create the **inbound** rules in the table below.</span></span>
   
   | <span data-ttu-id="d6e79-143">Правило входящих подключений</span><span class="sxs-lookup"><span data-stu-id="d6e79-143">Inbound rule</span></span> | <span data-ttu-id="d6e79-144">Правило исходящих подключений</span><span class="sxs-lookup"><span data-stu-id="d6e79-144">Outbound rule</span></span> |
   | --- | --- |
   | ![Портал Azure — правило входящих подключений](./media/virtual-networks-create-nsg-arm-pportal/figure17.png) |![Портал Azure — правило исходящих подключений](./media/virtual-networks-create-nsg-arm-pportal/figure18.png) |
3. <span data-ttu-id="d6e79-147">Повторите шаги раздела [Связывание группы безопасности сети с подсетью FrontEnd](#Associate-the-NSG-to-the-FrontEnd-subnet), чтобы связать группу безопасности сети **NSG-BackEnd** с подсетью **BackEnd**.</span><span class="sxs-lookup"><span data-stu-id="d6e79-147">Repeat the steps in [Associate the NSG to the FrontEnd subnet](#Associate-the-NSG-to-the-FrontEnd-subnet) to associate the **NSG-Backend** NSG to the **BackEnd** subnet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6e79-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d6e79-148">Next Steps</span></span>
* <span data-ttu-id="d6e79-149">Узнайте, как [управлять существующими группами безопасности сети](virtual-network-manage-nsg-arm-portal.md)</span><span class="sxs-lookup"><span data-stu-id="d6e79-149">Learn how to [manage existing NSGs](virtual-network-manage-nsg-arm-portal.md)</span></span>
* <span data-ttu-id="d6e79-150">[Включите ведение журнала](virtual-network-nsg-manage-log.md) для групп безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="d6e79-150">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

