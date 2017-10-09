---
title: "с помощью портала Azure hello Nsg aaaManage | Документы Microsoft"
description: "Узнайте, как toomanage существующей Nsg, с помощью портала Azure hello."
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
ms.openlocfilehash: ad9a4060bd81bae4597ad5a4f59622e10cd214cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-nsgs-using-hello-portal"></a><span data-ttu-id="7bd89-103">Управление с помощью портала hello Nsg</span><span class="sxs-lookup"><span data-stu-id="7bd89-103">Manage NSGs using hello portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7bd89-104">Портал</span><span class="sxs-lookup"><span data-stu-id="7bd89-104">Portal</span></span>](virtual-network-manage-nsg-arm-portal.md)
> * [<span data-ttu-id="7bd89-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7bd89-105">PowerShell</span></span>](virtual-network-manage-nsg-arm-ps.md)
> * [<span data-ttu-id="7bd89-106">интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="7bd89-106">Azure CLI</span></span>](virtual-network-manage-nsg-arm-cli.md)
>

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="7bd89-107">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="7bd89-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="7bd89-108">В этой статье описан с помощью модели развертывания диспетчера ресурсов hello, который рекомендуется в большинстве случаев новый вместо hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="7bd89-108">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="7bd89-109">Извлечение информации</span><span class="sxs-lookup"><span data-stu-id="7bd89-109">Retrieve Information</span></span>
<span data-ttu-id="7bd89-110">Вы можете просмотреть существующие группы безопасности сети, получить правила для существующей группы и узнать, с какими ресурсами она связана.</span><span class="sxs-lookup"><span data-stu-id="7bd89-110">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="7bd89-111">Просмотр существующих групп безопасности сети</span><span class="sxs-lookup"><span data-stu-id="7bd89-111">View existing NSGs</span></span>

<span data-ttu-id="7bd89-112">tooview все существующие Nsg в подписке, полный hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="7bd89-112">tooview all existing NSGs in a subscription, complete hello following steps:</span></span>

1. <span data-ttu-id="7bd89-113">В браузере перейдите toohttp://portal.azure.com и при необходимости выполните вход с помощью учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="7bd89-113">From a browser, navigate toohttp://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>

2. <span data-ttu-id="7bd89-114">Щелкните **Обзор >** > **Сетевые группы безопасности**.</span><span class="sxs-lookup"><span data-stu-id="7bd89-114">Click **Browse >** > **Network security groups**.</span></span>

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure1.png)

3. <span data-ttu-id="7bd89-116">Проверьте список Nsg hello в hello **сетевых групп безопасности** колонку.</span><span class="sxs-lookup"><span data-stu-id="7bd89-116">Check hello list of NSGs in hello **Network security groups** blade.</span></span>

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure2.png)

### <a name="view-nsgs-in-a-resource-group"></a><span data-ttu-id="7bd89-118">Просмотр групп безопасности сети в группе ресурсов</span><span class="sxs-lookup"><span data-stu-id="7bd89-118">View NSGs in a resource group</span></span>

<span data-ttu-id="7bd89-119">tooview списка Nsg hello в hello **RG NSG** группы ресурсов, полный hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="7bd89-119">tooview hello list of NSGs in hello **RG-NSG** resource group, complete hello following steps:</span></span>

1. <span data-ttu-id="7bd89-120">Щелкните раздел **Группы ресурсов >** > **RG-NSG** > **...**.</span><span class="sxs-lookup"><span data-stu-id="7bd89-120">Click **Resource groups >** > **RG-NSG** > **...**.</span></span>

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure3.png)

2. <span data-ttu-id="7bd89-122">В списке ресурсов hello поиска элементов отображается значок NSG hello, как показано в hello **ресурсов** колонке ниже.</span><span class="sxs-lookup"><span data-stu-id="7bd89-122">In hello list of resources, look for items displaying hello NSG icon, as shown in hello **Resources** blade below.</span></span>

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure4.png)

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="7bd89-124">Перечисление всех правил для группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="7bd89-124">List all rules for an NSG</span></span>

<span data-ttu-id="7bd89-125">tooview hello правила NSG с именем **NSG-FrontEnd**полный hello следующие действия:</span><span class="sxs-lookup"><span data-stu-id="7bd89-125">tooview hello rules of an NSG named **NSG-FrontEnd**, complete hello following steps:</span></span>

1. <span data-ttu-id="7bd89-126">Из hello **сетевых групп безопасности** колонке или hello **ресурсов** колонки, показанном выше, нажмите кнопку **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="7bd89-126">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>

2. <span data-ttu-id="7bd89-127">В hello **параметры** щелкните **безопасности правила для входящих подключений**.</span><span class="sxs-lookup"><span data-stu-id="7bd89-127">In hello **Settings** tab, click **Inbound security rules**.</span></span>

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure5.png)

3. <span data-ttu-id="7bd89-129">Hello **безопасности правила для входящих подключений** колонке отображается, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="7bd89-129">hello **Inbound security rules** blade is displayed as shown below.</span></span>

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure6.png)

4. <span data-ttu-id="7bd89-131">В hello **параметры** щелкните **правила безопасности для исходящего трафика** toosee hello правила для исходящих подключений.</span><span class="sxs-lookup"><span data-stu-id="7bd89-131">In hello **Settings** tab, click **Outbound security rules** toosee hello outbound rules.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7bd89-132">tooview правила по умолчанию, нажмите кнопку hello **по умолчанию правила** значок hello верхней части колонки hello, которое отображает hello правила.</span><span class="sxs-lookup"><span data-stu-id="7bd89-132">tooview default rules, click hello **Default rules** icon at hello top of hello blade that displays hello rules.</span></span>
    >

### <a name="view-nsgs-associations"></a><span data-ttu-id="7bd89-133">Просмотр связей для группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="7bd89-133">View NSGs associations</span></span>

<span data-ttu-id="7bd89-134">tooview какие ресурсы hello **NSG-FrontEnd** NSG — связан с, завершенной hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="7bd89-134">tooview what resources hello **NSG-FrontEnd** NSG is associate with, complete hello following steps:</span></span>

1. <span data-ttu-id="7bd89-135">Из hello **сетевых групп безопасности** колонке или hello **ресурсов** колонки, показанном выше, нажмите кнопку **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="7bd89-135">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>

2. <span data-ttu-id="7bd89-136">В hello **параметры** щелкните **подсети** tooview какие подсети — это связанные toohello NSG.</span><span class="sxs-lookup"><span data-stu-id="7bd89-136">In hello **Settings** tab, click **Subnets** tooview what subnets are associated toohello NSG.</span></span>

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure7.png)

3. <span data-ttu-id="7bd89-138">В hello **параметры** щелкните **сетевых интерфейсов** tooview новые сетевые адаптеры — это связанные toohello NSG.</span><span class="sxs-lookup"><span data-stu-id="7bd89-138">In hello **Settings** tab, click **Network interfaces** tooview what NICs are associated toohello NSG.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="7bd89-139">Управление правилами</span><span class="sxs-lookup"><span data-stu-id="7bd89-139">Manage rules</span></span>
<span data-ttu-id="7bd89-140">Добавление существующей NSG tooan правила, изменять существующие правила и удалять правила.</span><span class="sxs-lookup"><span data-stu-id="7bd89-140">You can add rules tooan existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="7bd89-141">Добавление правила</span><span class="sxs-lookup"><span data-stu-id="7bd89-141">Add a rule</span></span>
<span data-ttu-id="7bd89-142">tooadd правила, что позволяет **входящих** tooport трафика **443** с любого компьютера toohello **NSG-FrontEnd** NSG завершения hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="7bd89-142">tooadd a rule allowing **inbound** traffic tooport **443** from any machine toohello **NSG-FrontEnd** NSG, complete hello following steps:</span></span>

1. <span data-ttu-id="7bd89-143">Из hello **сетевых групп безопасности** колонке или hello **ресурсов** колонки, показанном выше, нажмите кнопку **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="7bd89-143">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="7bd89-144">В hello **параметры** щелкните **безопасности правила для входящих подключений**.</span><span class="sxs-lookup"><span data-stu-id="7bd89-144">In hello **Settings** tab, click **Inbound security rules**.</span></span>
3. <span data-ttu-id="7bd89-145">В hello **безопасности правила для входящих подключений** колонка, щелкните **добавить**.</span><span class="sxs-lookup"><span data-stu-id="7bd89-145">In hello **Inbound security rules** blade, click **Add**.</span></span> <span data-ttu-id="7bd89-146">Затем в hello **добавить правило безопасности для входящего трафика** колонке заполнения hello значения, как показано ниже и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="7bd89-146">Then, in hello **Add inbound security rule** blade, fill hello values as shown below, and then click **OK**.</span></span>

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure8.png)

    <span data-ttu-id="7bd89-148">Через несколько секунд, обратите внимание, hello новое правило в hello **безопасности правила для входящих подключений** колонку.</span><span class="sxs-lookup"><span data-stu-id="7bd89-148">After a few seconds, notice hello new rule in hello **Inbound security rules** blade.</span></span>

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure9.png)

### <a name="change-a-rule"></a><span data-ttu-id="7bd89-150">Изменение правила</span><span class="sxs-lookup"><span data-stu-id="7bd89-150">Change a rule</span></span>
<span data-ttu-id="7bd89-151">правило toochange hello, созданной ранее tooallow входящий трафик от hello **Internet** только, завершенной hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="7bd89-151">toochange hello rule created above tooallow inbound traffic from hello **Internet** only, complete hello following steps:</span></span>

1. <span data-ttu-id="7bd89-152">Из hello **сетевых групп безопасности** колонке или hello **ресурсов** колонки, показанном выше, нажмите кнопку **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="7bd89-152">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="7bd89-153">В hello **параметры** щелкните правило hello, созданной ранее.</span><span class="sxs-lookup"><span data-stu-id="7bd89-153">In hello **Settings** tab, click hello rule created above.</span></span>
3. <span data-ttu-id="7bd89-154">В hello **разрешить https** колонки, изменение hello **источника** свойства, как показано ниже, а затем щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="7bd89-154">In hello **allow-https** blade, change hello **Source** property as shown below, and then click **Save**.</span></span>

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure10.png)

### <a name="delete-a-rule"></a><span data-ttu-id="7bd89-156">Удаление правила</span><span class="sxs-lookup"><span data-stu-id="7bd89-156">Delete a rule</span></span>

<span data-ttu-id="7bd89-157">toodelete hello правило созданной выше, завершенной hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="7bd89-157">toodelete hello rule created above, complete hello following steps:</span></span>

1. <span data-ttu-id="7bd89-158">Из hello **сетевых групп безопасности** колонке или hello **ресурсов** колонки, показанном выше, нажмите кнопку **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="7bd89-158">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="7bd89-159">В hello **параметры** щелкните правило hello, созданной ранее.</span><span class="sxs-lookup"><span data-stu-id="7bd89-159">In hello **Settings** tab, click hello rule created above.</span></span>
3. <span data-ttu-id="7bd89-160">В hello **разрешить https** колонке нажмите кнопку **удаление**, а затем нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="7bd89-160">In hello **allow-https** blade, click **Delete**, and then click **Yes**.</span></span>

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure11.png)

## <a name="manage-associations"></a><span data-ttu-id="7bd89-162">Управление связями</span><span class="sxs-lookup"><span data-stu-id="7bd89-162">Manage associations</span></span>
<span data-ttu-id="7bd89-163">Можно связать NSG toosubnets и сетевых адаптеров.</span><span class="sxs-lookup"><span data-stu-id="7bd89-163">You can associate an NSG toosubnets and NICs.</span></span> <span data-ttu-id="7bd89-164">Можно также отменить связь группы безопасности сети с любым ресурсом.</span><span class="sxs-lookup"><span data-stu-id="7bd89-164">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-tooa-nic"></a><span data-ttu-id="7bd89-165">Связывание NSG tooa сетевого Адаптера</span><span class="sxs-lookup"><span data-stu-id="7bd89-165">Associate an NSG tooa NIC</span></span>
<span data-ttu-id="7bd89-166">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** сетевого Адаптера, полный hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="7bd89-166">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, complete hello following steps:</span></span>

1. <span data-ttu-id="7bd89-167">Из hello **сетевых групп безопасности** колонке или hello **ресурсов** колонки, показанном выше, нажмите кнопку **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="7bd89-167">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="7bd89-168">В hello **параметры** щелкните **сетевых интерфейсов** > **связать** > **TestNICWeb1**.</span><span class="sxs-lookup"><span data-stu-id="7bd89-168">In hello **Settings** tab, click **Network interfaces** > **Associate** > **TestNICWeb1**.</span></span>

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure12.png)

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="7bd89-170">Отмена связи с сетевым адаптером для группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="7bd89-170">Dissociate an NSG from a NIC</span></span>

<span data-ttu-id="7bd89-171">toodissociate hello **NSG-FrontEnd** NSG из hello **TestNICWeb1** сетевого Адаптера, полный hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="7bd89-171">toodissociate hello **NSG-FrontEnd** NSG from hello **TestNICWeb1** NIC, complete hello following steps:</span></span>

1. <span data-ttu-id="7bd89-172">Hello портал Azure, щелкните **групп ресурсов >** > **RG NSG** > **...**   >  **TestNICWeb1**.</span><span class="sxs-lookup"><span data-stu-id="7bd89-172">From hello Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestNICWeb1**.</span></span>

2. <span data-ttu-id="7bd89-173">В hello **TestNICWeb1** колонка, щелкните **изменения безопасности...**   >  **Нет**.</span><span class="sxs-lookup"><span data-stu-id="7bd89-173">In hello **TestNICWeb1** blade, click **Change security...** > **None**.</span></span>

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure13.png)

> [!NOTE]
> <span data-ttu-id="7bd89-175">Можно также использовать этой колонке tooassociate hello Сетевых tooany существующей NSG.</span><span class="sxs-lookup"><span data-stu-id="7bd89-175">You can also use this blade tooassociate hello NIC tooany existing NSG.</span></span>
>

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="7bd89-176">Отмена связи с подсетью для группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="7bd89-176">Dissociate an NSG from a subnet</span></span>

<span data-ttu-id="7bd89-177">toodissociate hello **NSG-FrontEnd** NSG из hello **переднего плана** подсети, полный hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="7bd89-177">toodissociate hello **NSG-FrontEnd** NSG from hello **FrontEnd** subnet, complete hello following steps:</span></span>

1. <span data-ttu-id="7bd89-178">Hello портал Azure, щелкните **групп ресурсов >** > **RG NSG** > **...**   >  **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="7bd89-178">From hello Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestVNet**.</span></span>

2. <span data-ttu-id="7bd89-179">В hello **параметры** колонка, щелкните **подсети** > **переднего плана** > **сетевой группы безопасности**  >  **Нет**.</span><span class="sxs-lookup"><span data-stu-id="7bd89-179">In hello **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **None**.</span></span>

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure14.png)

3. <span data-ttu-id="7bd89-181">В hello **переднего плана** колонка, щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="7bd89-181">In hello **FrontEnd** blade, click **Save**.</span></span>

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure15.png)

### <a name="associate-an-nsg-tooa-subnet"></a><span data-ttu-id="7bd89-183">Связывание NSG tooa подсети</span><span class="sxs-lookup"><span data-stu-id="7bd89-183">Associate an NSG tooa subnet</span></span>

<span data-ttu-id="7bd89-184">tooassociate hello **NSG-FrontEnd** NSG toohello **FronEnd** снова подсети, полный hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="7bd89-184">tooassociate hello **NSG-FrontEnd** NSG toohello **FronEnd** subnet again, complete hello following steps:</span></span>

1. <span data-ttu-id="7bd89-185">Hello портал Azure, щелкните **групп ресурсов >** > **RG NSG** > **...**   >  **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="7bd89-185">From hello Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestVNet**.</span></span>
2. <span data-ttu-id="7bd89-186">В hello **параметры** колонка, щелкните **подсети** > **переднего плана** > **сетевой группы безопасности**  >  **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="7bd89-186">In hello **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **NSG-FrontEnd**.</span></span>
3. <span data-ttu-id="7bd89-187">В hello **переднего плана** колонка, щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="7bd89-187">In hello **FrontEnd** blade, click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="7bd89-188">Можно также связать подсети tooa NSG из thh NSG **параметры** колонку.</span><span class="sxs-lookup"><span data-stu-id="7bd89-188">You can also associate an NSG tooa subnet from thh NSG's **Settings** blade.</span></span>
>

## <a name="delete-an-nsg"></a><span data-ttu-id="7bd89-189">Удаление группы NSG</span><span class="sxs-lookup"><span data-stu-id="7bd89-189">Delete an NSG</span></span>
<span data-ttu-id="7bd89-190">NSG можно удалить только в том случае, если она не сопоставлена tooany ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7bd89-190">You can only delete an NSG if it's not associated tooany resource.</span></span> <span data-ttu-id="7bd89-191">toodelete NSG, полный hello, следующие шаги:.</span><span class="sxs-lookup"><span data-stu-id="7bd89-191">toodelete an NSG, complete hello following steps:.</span></span>

1. <span data-ttu-id="7bd89-192">Hello портал Azure, щелкните **групп ресурсов >** > **RG NSG** > **...**   >  **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="7bd89-192">From hello Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="7bd89-193">В hello **параметры** колонка, щелкните **сетевых интерфейсов**.</span><span class="sxs-lookup"><span data-stu-id="7bd89-193">In hello **Settings** blade, click **Network interfaces**.</span></span>
3. <span data-ttu-id="7bd89-194">Если все сетевые адаптеры в списке, щелкните сетевой Адаптер hello и выполнить шаг 2 [связь между Сетевыми NSG](#Dissociate-an-NSG-from-a-NIC).</span><span class="sxs-lookup"><span data-stu-id="7bd89-194">If there are any NICs listed, click hello NIC, and follow step 2 in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC).</span></span>
4. <span data-ttu-id="7bd89-195">Повторите шаг 3 для каждого сетевого адаптера.</span><span class="sxs-lookup"><span data-stu-id="7bd89-195">Repeat step 3 for each NIC.</span></span>
5. <span data-ttu-id="7bd89-196">В hello **параметры** колонка, щелкните **подсети**.</span><span class="sxs-lookup"><span data-stu-id="7bd89-196">In hello **Settings** blade, click **Subnets**.</span></span>
6. <span data-ttu-id="7bd89-197">Если в списке подсетей, выберите подсеть hello и выполните шаги 2 и 3 в [связь NSG из подсети](#Dissociate-an-NSG-from-a-subnet).</span><span class="sxs-lookup"><span data-stu-id="7bd89-197">If there are any subnets listed, click hello subnet and follow steps 2 and 3 in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet).</span></span>
7. <span data-ttu-id="7bd89-198">Прокрутка влево toohello **NSG-FrontEnd** колонке нажмите кнопку **удаление** > **Да**.</span><span class="sxs-lookup"><span data-stu-id="7bd89-198">Scrolls left toohello **NSG-FrontEnd** blade, then click **Delete** > **Yes**.</span></span>

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure16.png)

## <a name="next-steps"></a><span data-ttu-id="7bd89-200">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7bd89-200">Next steps</span></span>
* <span data-ttu-id="7bd89-201">[Включите ведение журнала](virtual-network-nsg-manage-log.md) для групп безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="7bd89-201">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>
