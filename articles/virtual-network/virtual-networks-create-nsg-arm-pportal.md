---
title: "группы безопасности сети aaaCreate - портал Azure | Документы Microsoft"
description: "Узнайте, как toocreate и развертывание сетевых групп безопасности с помощью портала Azure hello."
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
ms.openlocfilehash: f74ecc7db06bb69f2041aa64d7b38b63eb379a70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-hello-azure-portal"></a><span data-ttu-id="24694-103">Создание группы безопасности с помощью портала Azure hello сети</span><span class="sxs-lookup"><span data-stu-id="24694-103">Create network security groups using hello Azure portal</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="24694-104">В этой статье рассматриваются hello модели развертывания диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="24694-104">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="24694-105">Вы также можете [создать Nsg в hello классической модели развертывания](virtual-networks-create-nsg-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="24694-105">You can also [create NSGs in hello classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="24694-106">Образец Hello PowerShell приведенную ниже команду ожидать простой среде уже создан на основании hello сценарии выше.</span><span class="sxs-lookup"><span data-stu-id="24694-106">hello sample PowerShell commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="24694-107">Toorun hello команд, отображаемых в этом документе, сначала построения необходимо hello тестовой среды, развернув [этот шаблон](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), нажмите кнопку **развертывание tooAzure**, замените значения параметров по умолчанию hello При необходимости и выполнения инструкции hello в hello портала.</span><span class="sxs-lookup"><span data-stu-id="24694-107">If you want toorun hello commands as they are displayed in this document, first build hello test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span> <span data-ttu-id="24694-108">ниже используйте шагов Hello **RG NSG** как hello имя hello ресурсов группы hello шаблона было развернуто.</span><span class="sxs-lookup"><span data-stu-id="24694-108">hello steps below use **RG-NSG** as hello name of hello resource group hello template was deployed to.</span></span>

## <a name="create-hello-nsg-frontend-nsg"></a><span data-ttu-id="24694-109">Создать hello переднего плана NSG NSG</span><span class="sxs-lookup"><span data-stu-id="24694-109">Create hello NSG-FrontEnd NSG</span></span>
<span data-ttu-id="24694-110">toocreate hello **NSG-FrontEnd** NSG, как показано в приведенном выше сценарии hello, выполните шаги hello.</span><span class="sxs-lookup"><span data-stu-id="24694-110">toocreate hello **NSG-FrontEnd** NSG as shown in hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="24694-111">В браузере перейдите toohttp://portal.azure.com и при необходимости выполните вход с помощью учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="24694-111">From a browser, navigate toohttp://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="24694-112">Щелкните **Обзор >** > **Сетевые группы безопасности**.</span><span class="sxs-lookup"><span data-stu-id="24694-112">Click **Browse >** > **Network Security Groups**.</span></span>
   
    ![Портал Azure — группы безопасности сети](./media/virtual-networks-create-nsg-arm-pportal/figure11.png)
3. <span data-ttu-id="24694-114">В hello **сетевых групп безопасности** колонка, щелкните **добавить**.</span><span class="sxs-lookup"><span data-stu-id="24694-114">In hello **Network security groups** blade, click **Add**.</span></span>
   
    ![Портал Azure — группы безопасности сети](./media/virtual-networks-create-nsg-arm-pportal/figure12.png)
4. <span data-ttu-id="24694-116">В hello **создать группу безопасности сети** колонке создать NSG с именем *NSG-FrontEnd* в hello *RG NSG* группы ресурсов, а затем щелкните **создать**.</span><span class="sxs-lookup"><span data-stu-id="24694-116">In hello **Create network security group** blade, create an NSG named *NSG-FrontEnd* in hello *RG-NSG* resource group, and then click **Create**.</span></span>
   
    ![Портал Azure — группы безопасности сети](./media/virtual-networks-create-nsg-arm-pportal/figure13.png)

## <a name="create-rules-in-an-existing-nsg"></a><span data-ttu-id="24694-118">Создание правил в существующей сетевой группе безопасности</span><span class="sxs-lookup"><span data-stu-id="24694-118">Create rules in an existing NSG</span></span>
<span data-ttu-id="24694-119">правила toocreate в существующей NSG из hello портал Azure, выполните шаги hello.</span><span class="sxs-lookup"><span data-stu-id="24694-119">toocreate rules in an existing NSG from hello Azure portal, follow hello steps below.</span></span>

1. <span data-ttu-id="24694-120">Щелкните **Обзор >** > **Сетевые группы безопасности**.</span><span class="sxs-lookup"><span data-stu-id="24694-120">Click **Browse >** > **Network security groups**.</span></span>
2. <span data-ttu-id="24694-121">В списке hello Nsg, выберите **NSG-FrontEnd** > **безопасности правила для входящих подключений**</span><span class="sxs-lookup"><span data-stu-id="24694-121">In hello list of NSGs, click **NSG-FrontEnd** > **Inbound security rules**</span></span>
   
    ![Портал Azure — NSG-FrontEnd](./media/virtual-networks-create-nsg-arm-pportal/figure2.png)
3. <span data-ttu-id="24694-123">В списке hello **безопасности правила для входящих подключений**, нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="24694-123">In hello list of **Inbound security rules**, click **Add**.</span></span>
   
    ![Портал Azure — добавление правила](./media/virtual-networks-create-nsg-arm-pportal/figure3.png)
4. <span data-ttu-id="24694-125">В hello **добавить правило безопасности для входящего трафика** колонки, создать правило с именем *правило web* с приоритетом *200* доступ через *TCP* tooport *80* tooany виртуальной Машины из любого источника и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="24694-125">In hello **Add inbound security rule** blade, create a rule named *web-rule* with priority of *200* allowing access via *TCP* tooport *80* tooany VM from any source, and then click **OK**.</span></span> <span data-ttu-id="24694-126">Обратите внимание, что для большинства этих параметров уже заданы значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="24694-126">Notice that most of these settings are default values already.</span></span>
   
    ![Портал Azure — параметры правила](./media/virtual-networks-create-nsg-arm-pportal/figure4.png)
5. <span data-ttu-id="24694-128">Через несколько секунд hello новое правило появится в hello NSG.</span><span class="sxs-lookup"><span data-stu-id="24694-128">After a few seconds you will see hello new rule in hello NSG.</span></span>
   
    ![Портал Azure — новое правило](./media/virtual-networks-create-nsg-arm-pportal/figure5.png)
6. <span data-ttu-id="24694-130">Повторите шаги too6 toocreate входящее правило с именем *rdp правило* с приоритетом *250* доступ через *TCP* tooport *3389* tooany виртуальной Машины из любого источника.</span><span class="sxs-lookup"><span data-stu-id="24694-130">Repeat steps  too6 toocreate an inbound rule named *rdp-rule* with a priority of *250* allowing access via *TCP* tooport *3389* tooany VM from any source.</span></span>

## <a name="associate-hello-nsg-toohello-frontend-subnet"></a><span data-ttu-id="24694-131">Связать hello NSG toohello внешней подсети</span><span class="sxs-lookup"><span data-stu-id="24694-131">Associate hello NSG toohello FrontEnd subnet</span></span>
1. <span data-ttu-id="24694-132">Щелкните **Обзор >** > **Группы ресурсов** > **RG NSG**.</span><span class="sxs-lookup"><span data-stu-id="24694-132">Click **Browse >** > **Resource groups** > **RG-NSG**.</span></span>
2. <span data-ttu-id="24694-133">В hello **RG NSG** колонка, щелкните **...**   >  **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="24694-133">In hello **RG-NSG** blade, click **...** > **TestVNet**.</span></span>
   
    ![Портал Azure — TestVNet](./media/virtual-networks-create-nsg-arm-pportal/figure14.png)
3. <span data-ttu-id="24694-135">В hello **параметры** колонка, щелкните **подсети** > **переднего плана** > **сетевой группы безопасности**  >  **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="24694-135">In hello **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **NSG-FrontEnd**.</span></span>
   
    ![Портал Azure — параметры подсети](./media/virtual-networks-create-nsg-arm-pportal/figure15.png)
4. <span data-ttu-id="24694-137">В hello **переднего плана** колонка, щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="24694-137">In hello **FrontEnd** blade, click **Save**.</span></span>
   
    ![Портал Azure — параметры подсети](./media/virtual-networks-create-nsg-arm-pportal/figure16.png)

## <a name="create-hello-nsg-backend-nsg"></a><span data-ttu-id="24694-139">Создать hello серверной NSG NSG</span><span class="sxs-lookup"><span data-stu-id="24694-139">Create hello NSG-BackEnd NSG</span></span>
<span data-ttu-id="24694-140">toocreate hello **NSG серверной** NSG и связать его toohello **серверной** подсети, выполните следующие действия hello.</span><span class="sxs-lookup"><span data-stu-id="24694-140">toocreate hello **NSG-BackEnd** NSG and associate it toohello **BackEnd** subnet, follow hello steps below.</span></span>

1. <span data-ttu-id="24694-141">Повторите hello шагов в [hello Создание внешнего интерфейса NSG NSG](#Create-the-NSG-FrontEnd-NSG) toocreate NSG с именем *серверной NSG*</span><span class="sxs-lookup"><span data-stu-id="24694-141">Repeat hello steps in [Create hello NSG-FrontEnd NSG](#Create-the-NSG-FrontEnd-NSG) toocreate an NSG named *NSG-BackEnd*</span></span>
2. <span data-ttu-id="24694-142">Повторите hello шагов в [создавать правила в существующей NSG](#Create-rules-in-an-existing-NSG) toocreate hello **входящих** правила в следующей таблице hello.</span><span class="sxs-lookup"><span data-stu-id="24694-142">Repeat hello steps in [Create rules in an existing NSG](#Create-rules-in-an-existing-NSG) toocreate hello **inbound** rules in hello table below.</span></span>
   
   | <span data-ttu-id="24694-143">Правило входящих подключений</span><span class="sxs-lookup"><span data-stu-id="24694-143">Inbound rule</span></span> | <span data-ttu-id="24694-144">Правило исходящих подключений</span><span class="sxs-lookup"><span data-stu-id="24694-144">Outbound rule</span></span> |
   | --- | --- |
   | ![Портал Azure — правило входящих подключений](./media/virtual-networks-create-nsg-arm-pportal/figure17.png) |![Портал Azure — правило исходящих подключений](./media/virtual-networks-create-nsg-arm-pportal/figure18.png) |
3. <span data-ttu-id="24694-147">Повторите hello шагов в [связать hello NSG toohello внешней подсети](#Associate-the-NSG-to-the-FrontEnd-subnet) tooassociate hello **NSG серверной** NSG toohello **серверной** подсети.</span><span class="sxs-lookup"><span data-stu-id="24694-147">Repeat hello steps in [Associate hello NSG toohello FrontEnd subnet](#Associate-the-NSG-to-the-FrontEnd-subnet) tooassociate hello **NSG-Backend** NSG toohello **BackEnd** subnet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="24694-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="24694-148">Next Steps</span></span>
* <span data-ttu-id="24694-149">Узнайте, каким образом слишком[Управление существующей Nsg](virtual-network-manage-nsg-arm-portal.md)</span><span class="sxs-lookup"><span data-stu-id="24694-149">Learn how too[manage existing NSGs](virtual-network-manage-nsg-arm-portal.md)</span></span>
* <span data-ttu-id="24694-150">[Включите ведение журнала](virtual-network-nsg-manage-log.md) для групп безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="24694-150">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

