---
title: "Управление группами безопасности сети с помощью портала Azure | Документация Майкрософт"
description: "Сведения об управлении существующими группами безопасности сети с помощью портала Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 5d55679d-57da-457c-97dc-1e1973909ee5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/14/2016
ms.author: jdial
ms.openlocfilehash: e9bcf8a893ff209337f6a5763b631a22f8514e20
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="manage-nsgs-using-the-portal"></a><span data-ttu-id="c9736-103">Управление группами безопасности сети с помощью портала</span><span class="sxs-lookup"><span data-stu-id="c9736-103">Manage NSGs using the portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c9736-104">Портал</span><span class="sxs-lookup"><span data-stu-id="c9736-104">Portal</span></span>](virtual-network-manage-nsg-arm-portal.md)
> * [<span data-ttu-id="c9736-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c9736-105">PowerShell</span></span>](virtual-network-manage-nsg-arm-ps.md)
> * [<span data-ttu-id="c9736-106">интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="c9736-106">Azure CLI</span></span>](virtual-network-manage-nsg-arm-cli.md)
>

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="c9736-107">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c9736-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="c9736-108">В этой статье описывается использование модели развертывания c помощью Resource Manager. Для большинства новых развертываний мы рекомендуем использовать эту модель вместо классической.</span><span class="sxs-lookup"><span data-stu-id="c9736-108">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span></span>
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="c9736-109">Извлечение информации</span><span class="sxs-lookup"><span data-stu-id="c9736-109">Retrieve Information</span></span>
<span data-ttu-id="c9736-110">Вы можете просмотреть существующие группы безопасности сети, получить правила для существующей группы и узнать, с какими ресурсами она связана.</span><span class="sxs-lookup"><span data-stu-id="c9736-110">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="c9736-111">Просмотр существующих групп безопасности сети</span><span class="sxs-lookup"><span data-stu-id="c9736-111">View existing NSGs</span></span>

<span data-ttu-id="c9736-112">Чтобы просмотреть список всех существующих групп безопасности сети в подписке, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="c9736-112">To view all existing NSGs in a subscription, complete the following steps:</span></span>

1. <span data-ttu-id="c9736-113">В браузере откройте адрес http://portal.azure.com и войдите с помощью учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="c9736-113">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>

2. <span data-ttu-id="c9736-114">Щелкните **Обзор >** > **Сетевые группы безопасности**.</span><span class="sxs-lookup"><span data-stu-id="c9736-114">Click **Browse >** > **Network security groups**.</span></span>

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure1.png)

3. <span data-ttu-id="c9736-116">Проверьте список группы безопасности сети в **группы безопасности сети** колонки.</span><span class="sxs-lookup"><span data-stu-id="c9736-116">Check the list of NSGs in the **Network security groups** blade.</span></span>

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure2.png)

### <a name="view-nsgs-in-a-resource-group"></a><span data-ttu-id="c9736-118">Просмотр групп безопасности сети в группе ресурсов</span><span class="sxs-lookup"><span data-stu-id="c9736-118">View NSGs in a resource group</span></span>

<span data-ttu-id="c9736-119">Чтобы просмотреть список групп безопасности сети в группе ресурсов **RG-NSG**, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="c9736-119">To view the list of NSGs in the **RG-NSG** resource group, complete the following steps:</span></span>

1. <span data-ttu-id="c9736-120">Щелкните раздел **Группы ресурсов >** > **RG-NSG** > **...**.</span><span class="sxs-lookup"><span data-stu-id="c9736-120">Click **Resource groups >** > **RG-NSG** > **...**.</span></span>

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure3.png)

2. <span data-ttu-id="c9736-122">В список ресурсов найдите элементы со значком NSG, как показано в колонке **Ресурсы** ниже.</span><span class="sxs-lookup"><span data-stu-id="c9736-122">In the list of resources, look for items displaying the NSG icon, as shown in the **Resources** blade below.</span></span>

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure4.png)

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="c9736-124">Перечисление всех правил для группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="c9736-124">List all rules for an NSG</span></span>

<span data-ttu-id="c9736-125">Чтобы просмотреть правила группы безопасности сети **NSG-FrontEnd**, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="c9736-125">To view the rules of an NSG named **NSG-FrontEnd**, complete the following steps:</span></span>

1. <span data-ttu-id="c9736-126">В колонке **Сетевые группы безопасности** или **Ресурсы**, как показано выше, щелкните **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="c9736-126">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>

2. <span data-ttu-id="c9736-127">На вкладке **Параметры** выберите **Правила безопасности для входящего трафика**.</span><span class="sxs-lookup"><span data-stu-id="c9736-127">In the **Settings** tab, click **Inbound security rules**.</span></span>

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure5.png)

3. <span data-ttu-id="c9736-129">Колонка **Правила безопасности для входящего трафика** отображается, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="c9736-129">The **Inbound security rules** blade is displayed as shown below.</span></span>

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure6.png)

4. <span data-ttu-id="c9736-131">На вкладке **Параметры** выберите **Правила безопасности для исходящего трафика**, чтобы просмотреть правила для исходящего трафика.</span><span class="sxs-lookup"><span data-stu-id="c9736-131">In the **Settings** tab, click **Outbound security rules** to see the outbound rules.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c9736-132">Чтобы просмотреть правила по умолчанию, щелкните значок **Правила по умолчанию** в верхней части колонки, где показаны правила.</span><span class="sxs-lookup"><span data-stu-id="c9736-132">To view default rules, click the **Default rules** icon at the top of the blade that displays the rules.</span></span>
    >

### <a name="view-nsgs-associations"></a><span data-ttu-id="c9736-133">Просмотр связей для группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="c9736-133">View NSGs associations</span></span>

<span data-ttu-id="c9736-134">Чтобы просмотреть, к каким ресурсам привязана группа безопасности сети **NSG-FrontEnd**, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="c9736-134">To view what resources the **NSG-FrontEnd** NSG is associate with, complete the following steps:</span></span>

1. <span data-ttu-id="c9736-135">В колонке **Сетевые группы безопасности** или **Ресурсы**, как показано выше, щелкните **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="c9736-135">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>

2. <span data-ttu-id="c9736-136">На вкладке **Параметры** выберите **Подсети**, чтобы узнать, какие подсети связаны с группой безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="c9736-136">In the **Settings** tab, click **Subnets** to view what subnets are associated to the NSG.</span></span>

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure7.png)

3. <span data-ttu-id="c9736-138">На вкладке **Параметры** выберите **Сетевые интерфейсы**, чтобы узнать, какие сетевые интерфейсы связаны с группой безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="c9736-138">In the **Settings** tab, click **Network interfaces** to view what NICs are associated to the NSG.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="c9736-139">Управление правилами</span><span class="sxs-lookup"><span data-stu-id="c9736-139">Manage rules</span></span>
<span data-ttu-id="c9736-140">Можно добавлять правила для существующей группы безопасности сети, изменять существующие правила и удалять их.</span><span class="sxs-lookup"><span data-stu-id="c9736-140">You can add rules to an existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="c9736-141">Добавление правила</span><span class="sxs-lookup"><span data-stu-id="c9736-141">Add a rule</span></span>
<span data-ttu-id="c9736-142">Чтобы добавить правило, разрешающее **входящий** трафик через порт **443** с любого компьютера в группу безопасности сети **NSG-FrontEnd**, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="c9736-142">To add a rule allowing **inbound** traffic to port **443** from any machine to the **NSG-FrontEnd** NSG, complete the following steps:</span></span>

1. <span data-ttu-id="c9736-143">В колонке **Сетевые группы безопасности** или **Ресурсы**, как показано выше, щелкните **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="c9736-143">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="c9736-144">На вкладке **Параметры** выберите **Правила безопасности для входящего трафика**.</span><span class="sxs-lookup"><span data-stu-id="c9736-144">In the **Settings** tab, click **Inbound security rules**.</span></span>
3. <span data-ttu-id="c9736-145">В колонке **Правила безопасности для входящего трафика** нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c9736-145">In the **Inbound security rules** blade, click **Add**.</span></span> <span data-ttu-id="c9736-146">Затем в колонке **Добавление правила безопасности для входящего трафика** введите значения, как показано ниже, и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c9736-146">Then, in the **Add inbound security rule** blade, fill the values as shown below, and then click **OK**.</span></span>

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure8.png)

    <span data-ttu-id="c9736-148">Через несколько секунд вы сможете увидеть новое правило в колонке **Правила безопасности для входящего трафика** .</span><span class="sxs-lookup"><span data-stu-id="c9736-148">After a few seconds, notice the new rule in the **Inbound security rules** blade.</span></span>

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure9.png)

### <a name="change-a-rule"></a><span data-ttu-id="c9736-150">Изменение правила</span><span class="sxs-lookup"><span data-stu-id="c9736-150">Change a rule</span></span>
<span data-ttu-id="c9736-151">Чтобы изменить ранее созданное правило, разрешающее входящий трафик только из **Интернета**, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="c9736-151">To change the rule created above to allow inbound traffic from the **Internet** only, complete the following steps:</span></span>

1. <span data-ttu-id="c9736-152">В колонке **Сетевые группы безопасности** или **Ресурсы**, как показано выше, щелкните **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="c9736-152">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="c9736-153">На вкладке **Параметры** щелкните созданное ранее правило.</span><span class="sxs-lookup"><span data-stu-id="c9736-153">In the **Settings** tab, click the rule created above.</span></span>
3. <span data-ttu-id="c9736-154">В колонке **allow-https** измените свойство **Source**, как показано ниже, а затем нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="c9736-154">In the **allow-https** blade, change the **Source** property as shown below, and then click **Save**.</span></span>

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure10.png)

### <a name="delete-a-rule"></a><span data-ttu-id="c9736-156">Удаление правила</span><span class="sxs-lookup"><span data-stu-id="c9736-156">Delete a rule</span></span>

<span data-ttu-id="c9736-157">Чтобы удалить ранее созданное правило, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="c9736-157">To delete the rule created above, complete the following steps:</span></span>

1. <span data-ttu-id="c9736-158">В колонке **Сетевые группы безопасности** или **Ресурсы**, как показано выше, щелкните **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="c9736-158">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="c9736-159">На вкладке **Параметры** щелкните созданное ранее правило.</span><span class="sxs-lookup"><span data-stu-id="c9736-159">In the **Settings** tab, click the rule created above.</span></span>
3. <span data-ttu-id="c9736-160">В колонке **allow-https** нажмите кнопку **Удалить**, а затем — **Да**.</span><span class="sxs-lookup"><span data-stu-id="c9736-160">In the **allow-https** blade, click **Delete**, and then click **Yes**.</span></span>

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure11.png)

## <a name="manage-associations"></a><span data-ttu-id="c9736-162">Управление связями</span><span class="sxs-lookup"><span data-stu-id="c9736-162">Manage associations</span></span>
<span data-ttu-id="c9736-163">Группу безопасности сети можно связать с сетевыми адаптерами и подсетями.</span><span class="sxs-lookup"><span data-stu-id="c9736-163">You can associate an NSG to subnets and NICs.</span></span> <span data-ttu-id="c9736-164">Можно также отменить связь группы безопасности сети с любым ресурсом.</span><span class="sxs-lookup"><span data-stu-id="c9736-164">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-to-a-nic"></a><span data-ttu-id="c9736-165">Связывание группы безопасности сети с сетевым адаптером</span><span class="sxs-lookup"><span data-stu-id="c9736-165">Associate an NSG to a NIC</span></span>
<span data-ttu-id="c9736-166">Чтобы привязать группу безопасности сети **NSG-FrontEnd** к сетевому интерфейсу **TestNICWeb1**, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="c9736-166">To associate the **NSG-FrontEnd** NSG to the **TestNICWeb1** NIC, complete the following steps:</span></span>

1. <span data-ttu-id="c9736-167">В колонке **Сетевые группы безопасности** или **Ресурсы**, как показано выше, щелкните **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="c9736-167">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="c9736-168">На вкладке **Параметры** щелкните пункты **Сетевые интерфейсы** > **Привязать** > **TestNICWeb1**.</span><span class="sxs-lookup"><span data-stu-id="c9736-168">In the **Settings** tab, click **Network interfaces** > **Associate** > **TestNICWeb1**.</span></span>

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure12.png)

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="c9736-170">Отмена связи с сетевым адаптером для группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="c9736-170">Dissociate an NSG from a NIC</span></span>

<span data-ttu-id="c9736-171">Чтобы отменить связь группы безопасности сети **NSG-FrontEnd** с сетевым интерфейсом **TestNICWeb1**, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="c9736-171">To dissociate the **NSG-FrontEnd** NSG from the **TestNICWeb1** NIC, complete the following steps:</span></span>

1. <span data-ttu-id="c9736-172">На портале Azure выберите пункты **Группы ресурсов >** > **RG-NSG** > **...** > **TestNICWeb1**.</span><span class="sxs-lookup"><span data-stu-id="c9736-172">From the Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestNICWeb1**.</span></span>

2. <span data-ttu-id="c9736-173">В колонке **TestNICWeb1** выберите пункты **Изменить группу...** > **Нет**.</span><span class="sxs-lookup"><span data-stu-id="c9736-173">In the **TestNICWeb1** blade, click **Change security...** > **None**.</span></span>

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure13.png)

> [!NOTE]
> <span data-ttu-id="c9736-175">Можно также использовать эту колонку для связывания сетевого адаптера с существующей группой безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="c9736-175">You can also use this blade to associate the NIC to any existing NSG.</span></span>
>

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="c9736-176">Отмена связи с подсетью для группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="c9736-176">Dissociate an NSG from a subnet</span></span>

<span data-ttu-id="c9736-177">Чтобы отменить связь группы безопасности сети **NSG-FrontEnd** с подсетью **FrontEnd**, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="c9736-177">To dissociate the **NSG-FrontEnd** NSG from the **FrontEnd** subnet, complete the following steps:</span></span>

1. <span data-ttu-id="c9736-178">На портале Azure выберите пункты **Группы ресурсов >** > **RG-NSG** > **...** > **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="c9736-178">From the Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestVNet**.</span></span>

2. <span data-ttu-id="c9736-179">В колонке **Параметры** выберите пункты **Подсети** > **FrontEnd** > **Группа безопасности сети** > **Нет**.</span><span class="sxs-lookup"><span data-stu-id="c9736-179">In the **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **None**.</span></span>

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure14.png)

3. <span data-ttu-id="c9736-181">В колонке **FrontEnd** нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="c9736-181">In the **FrontEnd** blade, click **Save**.</span></span>

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure15.png)

### <a name="associate-an-nsg-to-a-subnet"></a><span data-ttu-id="c9736-183">Связывание группы NSG с подсетью</span><span class="sxs-lookup"><span data-stu-id="c9736-183">Associate an NSG to a subnet</span></span>

<span data-ttu-id="c9736-184">Чтобы привязать группу безопасности сети **NSG-FrontEnd** к подсети **FronEnd** снова, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="c9736-184">To associate the **NSG-FrontEnd** NSG to the **FronEnd** subnet again, complete the following steps:</span></span>

1. <span data-ttu-id="c9736-185">На портале Azure выберите пункты **Группы ресурсов >** > **RG-NSG** > **...** > **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="c9736-185">From the Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestVNet**.</span></span>
2. <span data-ttu-id="c9736-186">В колонке **Параметры** выберите пункты **Подсети** > **FrontEnd** > **Группа безопасности сети** > **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="c9736-186">In the **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **NSG-FrontEnd**.</span></span>
3. <span data-ttu-id="c9736-187">В колонке **FrontEnd** нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="c9736-187">In the **FrontEnd** blade, click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="c9736-188">Можно также связать группу безопасности сети с подсетью в колонке **Параметры** этой группы.</span><span class="sxs-lookup"><span data-stu-id="c9736-188">You can also associate an NSG to a subnet from thh NSG's **Settings** blade.</span></span>
>

## <a name="delete-an-nsg"></a><span data-ttu-id="c9736-189">Удаление группы NSG</span><span class="sxs-lookup"><span data-stu-id="c9736-189">Delete an NSG</span></span>
<span data-ttu-id="c9736-190">Группу безопасности сети можно удалить только в том случае, если она не связана с ресурсами.</span><span class="sxs-lookup"><span data-stu-id="c9736-190">You can only delete an NSG if it's not associated to any resource.</span></span> <span data-ttu-id="c9736-191">Чтобы удалить группу безопасности сети, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="c9736-191">To delete an NSG, complete the following steps:.</span></span>

1. <span data-ttu-id="c9736-192">На портале Azure выберите пункты **Группы ресурсов >** > **RG-NSG** > **...** > **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="c9736-192">From the Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="c9736-193">В колонке **Параметры** выберите **Сетевые интерфейсы**.</span><span class="sxs-lookup"><span data-stu-id="c9736-193">In the **Settings** blade, click **Network interfaces**.</span></span>
3. <span data-ttu-id="c9736-194">Если в списке есть сетевые адаптеры, щелкните один из них и выполните шаг 2 из раздела [Отмена связи с сетевым адаптером для группы безопасности сети](#Dissociate-an-NSG-from-a-NIC).</span><span class="sxs-lookup"><span data-stu-id="c9736-194">If there are any NICs listed, click the NIC, and follow step 2 in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC).</span></span>
4. <span data-ttu-id="c9736-195">Повторите шаг 3 для каждого сетевого адаптера.</span><span class="sxs-lookup"><span data-stu-id="c9736-195">Repeat step 3 for each NIC.</span></span>
5. <span data-ttu-id="c9736-196">В колонке **Параметры** щелкните **Подсети**.</span><span class="sxs-lookup"><span data-stu-id="c9736-196">In the **Settings** blade, click **Subnets**.</span></span>
6. <span data-ttu-id="c9736-197">Если в списке есть подсети, щелкните одну из них и выполните шаги 2 и 3 из раздела [Отмена связи с подсетью для группы безопасности сети](#Dissociate-an-NSG-from-a-subnet).</span><span class="sxs-lookup"><span data-stu-id="c9736-197">If there are any subnets listed, click the subnet and follow steps 2 and 3 in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet).</span></span>
7. <span data-ttu-id="c9736-198">Прокрутите страницу влево к колонке **NSG-FrontEnd** и нажмите кнопки **Удалить** > **Да**.</span><span class="sxs-lookup"><span data-stu-id="c9736-198">Scrolls left to the **NSG-FrontEnd** blade, then click **Delete** > **Yes**.</span></span>

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure16.png)

## <a name="next-steps"></a><span data-ttu-id="c9736-200">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c9736-200">Next steps</span></span>
* <span data-ttu-id="c9736-201">[Включите ведение журнала](virtual-network-nsg-manage-log.md) для групп безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="c9736-201">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>
