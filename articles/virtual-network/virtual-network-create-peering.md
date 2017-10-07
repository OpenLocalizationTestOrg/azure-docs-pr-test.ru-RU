---
title: "пиринг виртуальная сеть Azure - aaaCreate диспетчера ресурсов - одной подписке | Документы Microsoft"
description: "Узнайте, как toocreate пиринг виртуальной сети между виртуальными сетями создан через диспетчер ресурсов, существует hello же подписки Azure."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 026bca75-2946-4c03-b4f6-9f3c5809c69a
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: jdial;narayan;annahar
ms.openlocfilehash: c2d24fdc8103c09c3bfb8e59be12e301d9e9a55a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---resource-manager-same-subscription"></a><span data-ttu-id="7afd3-103">Создание пиринга между виртуальными сетями, развернутыми с помощью Resource Manager в одной подписке</span><span class="sxs-lookup"><span data-stu-id="7afd3-103">Create a virtual network peering - Resource Manager, same subscription</span></span>

<span data-ttu-id="7afd3-104">В этом учебнике вы узнаете, toocreate виртуальную сеть пиринга между виртуальных сетей, созданные с помощью диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7afd3-104">In this tutorial, you learn toocreate a virtual network peering between virtual networks created through Resource Manager.</span></span> <span data-ttu-id="7afd3-105">Обе виртуальные сети существуют в hello же подписки.</span><span class="sxs-lookup"><span data-stu-id="7afd3-105">Both virtual networks exist in hello same subscription.</span></span> <span data-ttu-id="7afd3-106">Пиринг два ресурса включает виртуальные сети в разных виртуальных сетей toocommunicate друг с другом и с hello же полосы пропускания и задержки, как будто hello ресурсы в hello одной виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="7afd3-106">Peering two virtual networks enables resources in different virtual networks toocommunicate with each other with hello same bandwidth and latency as though hello resources were in hello same virtual network.</span></span> <span data-ttu-id="7afd3-107">Узнайте больше о [пиринге виртуальных сетей](virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7afd3-107">Learn more about [Virtual network peering](virtual-network-peering-overview.md).</span></span> 

<span data-ttu-id="7afd3-108">Hello действия toocreate виртуальную сеть пиринга различаются, в зависимости от того, являются ли виртуальные сети hello hello в одном или разных, подписки и который [модели развертывания Azure](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello виртуальные сети создаются через.</span><span class="sxs-lookup"><span data-stu-id="7afd3-108">hello steps toocreate a virtual network peering are different, depending on whether hello virtual networks are in hello same, or different, subscriptions, and which [Azure deployment model](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello virtual networks are created through.</span></span> <span data-ttu-id="7afd3-109">Узнайте, как toocreate в виртуальной сети пиринг в других сценариях, щелкнув hello сценарий из hello в следующей таблице:</span><span class="sxs-lookup"><span data-stu-id="7afd3-109">Learn how toocreate a virtual network peering in other scenarios by clicking hello scenario from hello following table:</span></span>

|<span data-ttu-id="7afd3-110">Модель развертывания Azure</span><span class="sxs-lookup"><span data-stu-id="7afd3-110">Azure deployment model</span></span>  | <span data-ttu-id="7afd3-111">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="7afd3-111">Azure subscription</span></span>  |
|--------- |---------|
|[<span data-ttu-id="7afd3-112">Обе Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7afd3-112">Both Resource Manager</span></span>](create-peering-different-subscriptions.md) |<span data-ttu-id="7afd3-113">Разные</span><span class="sxs-lookup"><span data-stu-id="7afd3-113">Different</span></span>|
|[<span data-ttu-id="7afd3-114">Одна виртуальная сеть Resource Manager, одна классическая виртуальная сеть</span><span class="sxs-lookup"><span data-stu-id="7afd3-114">One Resource Manager, one classic</span></span>](create-peering-different-deployment-models.md) |<span data-ttu-id="7afd3-115">Аналогично</span><span class="sxs-lookup"><span data-stu-id="7afd3-115">Same</span></span>|
|[<span data-ttu-id="7afd3-116">Одна виртуальная сеть Resource Manager, одна классическая виртуальная сеть</span><span class="sxs-lookup"><span data-stu-id="7afd3-116">One Resource Manager, one classic</span></span>](create-peering-different-deployment-models-subscriptions.md) |<span data-ttu-id="7afd3-117">Разные</span><span class="sxs-lookup"><span data-stu-id="7afd3-117">Different</span></span>|

<span data-ttu-id="7afd3-118">Невозможно создать виртуальную сеть пиринга между двумя виртуальными сетями, развернутые с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="7afd3-118">A virtual network peering cannot be created between two virtual networks deployed through hello classic deployment model.</span></span> <span data-ttu-id="7afd3-119">Пиринг виртуальной сети могут быть созданы только между двумя виртуальными сетями, существующие в hello же регионе Azure.</span><span class="sxs-lookup"><span data-stu-id="7afd3-119">A virtual network peering can only be created between two virtual networks that exist in hello same Azure region.</span></span> <span data-ttu-id="7afd3-120">Если вам требуется tooconnect виртуальных сетей, оба созданным с помощью hello классической модели развертывания или существуют в разных регионах Azure, можно использовать Azure [VPN-шлюз](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect hello виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="7afd3-120">If you need tooconnect virtual networks that were both created through hello classic deployment model, or that exist in different Azure regions, you can use an Azure [VPN Gateway](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect hello virtual networks.</span></span> 

<span data-ttu-id="7afd3-121">Можно использовать hello [портал Azure](#portal), hello Azure [интерфейс командной строки](#cli) (CLI), Azure [PowerShell](#powershell), или [шаблона Azure Resource Manager](#template) toocreate пиринг виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="7afd3-121">You can use hello [Azure portal](#portal), hello Azure [command-line interface](#cli) (CLI), Azure [PowerShell](#powershell), or an [Azure Resource Manager template](#template) toocreate a virtual network peering.</span></span> <span data-ttu-id="7afd3-122">Щелкните любой hello предыдущего средства ссылки toogo напрямую toohello шаги для создания виртуальной сети пиринг с помощью нравятся.</span><span class="sxs-lookup"><span data-stu-id="7afd3-122">Click any of hello previous tool links toogo directly toohello steps for creating a virtual network peering using your tool of choice.</span></span>

## <span data-ttu-id="7afd3-123"><a name="portal"></a>Создание пиринга с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="7afd3-123"><a name="portal"></a>Create peering - Azure portal</span></span>

1. <span data-ttu-id="7afd3-124">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7afd3-124">Log in toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="7afd3-125">Hello учетной записи, использованной для входа в систему должен иметь необходимые разрешения toocreate hello пиринг виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="7afd3-125">hello account you log in with must have hello necessary permissions toocreate a virtual network peering.</span></span> <span data-ttu-id="7afd3-126">В разделе hello [разрешения](#permissions) Дополнительные сведения см.</span><span class="sxs-lookup"><span data-stu-id="7afd3-126">See hello [Permissions](#permissions) section of this article for details.</span></span>
2. <span data-ttu-id="7afd3-127">Щелкните **+ Создать**, выберите **Сети** и щелкните **Виртуальная сеть**.</span><span class="sxs-lookup"><span data-stu-id="7afd3-127">Click **+ New**, click **Networking**, then click **Virtual network**.</span></span>
3. <span data-ttu-id="7afd3-128">В hello **Создание виртуальной сети** колонки, введите, или выбрать значения для hello следующие параметры, а затем нажмите кнопку **создать**:</span><span class="sxs-lookup"><span data-stu-id="7afd3-128">In hello **Create virtual network** blade, enter, or select values for hello following settings, then click **Create**:</span></span>
    - <span data-ttu-id="7afd3-129">**Имя**: *myVnet1*.</span><span class="sxs-lookup"><span data-stu-id="7afd3-129">**Name**: *myVnet1*</span></span>
    - <span data-ttu-id="7afd3-130">**Адресное пространство**: *10.0.0.0/16*.</span><span class="sxs-lookup"><span data-stu-id="7afd3-130">**Address space**: *10.0.0.0/16*</span></span>
    - <span data-ttu-id="7afd3-131">**Имя подсети**: *по умолчанию*.</span><span class="sxs-lookup"><span data-stu-id="7afd3-131">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="7afd3-132">**Диапазон адресов подсети**: *10.0.0.0/24*.</span><span class="sxs-lookup"><span data-stu-id="7afd3-132">**Subnet address range**: *10.0.0.0/24*</span></span>
    - <span data-ttu-id="7afd3-133">**Подписка**: выберите свою подписку.</span><span class="sxs-lookup"><span data-stu-id="7afd3-133">**Subscription**: Select your subscription</span></span>
    - <span data-ttu-id="7afd3-134">**Группа ресурсов**: установите флажок **Создать** и введите *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="7afd3-134">**Resource group**: Select **Create new** and enter *myResourceGroup*</span></span>
    - <span data-ttu-id="7afd3-135">**Расположение**: *Восточная часть США*.</span><span class="sxs-lookup"><span data-stu-id="7afd3-135">**Location**: *East US*</span></span>
4. <span data-ttu-id="7afd3-136">Выполните шаги 2 – 3 опять же указать hello последующих значений на шаге 3.</span><span class="sxs-lookup"><span data-stu-id="7afd3-136">Complete steps 2-3 again specifying hello following values in step 3:</span></span>
    - <span data-ttu-id="7afd3-137">**Имя**: *myVnet2*.</span><span class="sxs-lookup"><span data-stu-id="7afd3-137">**Name**: *myVnet2*</span></span>
    - <span data-ttu-id="7afd3-138">**Адресное пространство**: *10.1.0.0/16*.</span><span class="sxs-lookup"><span data-stu-id="7afd3-138">**Address space**: *10.1.0.0/16*</span></span>
    - <span data-ttu-id="7afd3-139">**Имя подсети**: *по умолчанию*.</span><span class="sxs-lookup"><span data-stu-id="7afd3-139">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="7afd3-140">**Диапазон адресов подсети:** *10.1.0.0/24*.</span><span class="sxs-lookup"><span data-stu-id="7afd3-140">**Subnet address range**: *10.1.0.0/24*</span></span>
    - <span data-ttu-id="7afd3-141">**Подписка**: выберите свою подписку.</span><span class="sxs-lookup"><span data-stu-id="7afd3-141">**Subscription**: Select your subscription</span></span>
    - <span data-ttu-id="7afd3-142">**Группа ресурсов**: установите флажок **Использовать существующий** и выберите *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="7afd3-142">**Resource group**: Select **Use existing** and select *myResourceGroup*</span></span>
    - <span data-ttu-id="7afd3-143">**Расположение**: *Восточная часть США*.</span><span class="sxs-lookup"><span data-stu-id="7afd3-143">**Location**: *East US*</span></span>
5. <span data-ttu-id="7afd3-144">В hello **Найдите ресурсы** поле вверху hello портала hello, тип *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="7afd3-144">In hello **Search resources** box at hello top of hello portal, type *myResourceGroup*.</span></span> <span data-ttu-id="7afd3-145">Нажмите кнопку **myResourceGroup** когда он появится в результатах поиска hello.</span><span class="sxs-lookup"><span data-stu-id="7afd3-145">Click **myResourceGroup** when it appears in hello search results.</span></span> <span data-ttu-id="7afd3-146">Стоечный модуль появится для hello **myresourcegroup** группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7afd3-146">A blade appears for hello **myresourcegroup** resource group.</span></span> <span data-ttu-id="7afd3-147">Группа ресурсов Hello содержит hello двух виртуальных сетей в предыдущих шагах.</span><span class="sxs-lookup"><span data-stu-id="7afd3-147">hello resource group contains hello two virtual networks created in previous steps.</span></span>
6. <span data-ttu-id="7afd3-148">Щелкните сеть **myVNet1**.</span><span class="sxs-lookup"><span data-stu-id="7afd3-148">Click **myVNet1**.</span></span>
7. <span data-ttu-id="7afd3-149">В hello **myVnet1** колонки, отображается, нажмите кнопку **Пиринги** из hello вертикальной список параметров в hello левая сторона колонка hello.</span><span class="sxs-lookup"><span data-stu-id="7afd3-149">In hello **myVnet1** blade that appears, click **Peerings** from hello vertical list of options on hello left side of hello blade.</span></span>
8. <span data-ttu-id="7afd3-150">В hello **myVnet1 - Пиринги** колонки, которое было открыто, нажмите кнопку **+ добавить**</span><span class="sxs-lookup"><span data-stu-id="7afd3-150">In hello **myVnet1 - Peerings** blade that appeared, click **+ Add**</span></span>
9. <span data-ttu-id="7afd3-151">В hello **пиринг добавить** колонки, отображается, введите, или выберите hello следующие параметры, а затем нажмите кнопку **ОК**:</span><span class="sxs-lookup"><span data-stu-id="7afd3-151">In hello **Add peering** blade that appears, enter, or select hello following options, then click **OK**:</span></span>
     - <span data-ttu-id="7afd3-152">**Имя**: *myVnet1ToMyVnet2*.</span><span class="sxs-lookup"><span data-stu-id="7afd3-152">**Name**: *myVnet1ToMyVnet2*</span></span>
     - <span data-ttu-id="7afd3-153">**Модель развертывания виртуальной сети**: выберите **Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="7afd3-153">**Virtual network deployment model**:  Select **Resource Manager**.</span></span> 
     - <span data-ttu-id="7afd3-154">**Подписка**: выберите свою подписку.</span><span class="sxs-lookup"><span data-stu-id="7afd3-154">**Subscription**: Select your subscription</span></span>
     - <span data-ttu-id="7afd3-155">**Виртуальная сеть**: щелкните **Выбор виртуальной сети**, затем выберите **myVnet2**.</span><span class="sxs-lookup"><span data-stu-id="7afd3-155">**Virtual network**:  Click **Choose a virtual network**, then click **myVnet2**.</span></span>
     - <span data-ttu-id="7afd3-156">**Разрешить доступ к виртуальным сетям**: убедитесь, что выбрано значение **Включено**.</span><span class="sxs-lookup"><span data-stu-id="7afd3-156">**Allow virtual network access:** Ensure that **Enabled** is selected.</span></span>
    <span data-ttu-id="7afd3-157">Другие параметры в этом руководстве не используются.</span><span class="sxs-lookup"><span data-stu-id="7afd3-157">No other settings are used in this tutorial.</span></span> <span data-ttu-id="7afd3-158">чтение toolearn обо всех параметрах пиринга, [управления пиринги виртуальных сетей](virtual-network-manage-peering.md#create-a-peering).</span><span class="sxs-lookup"><span data-stu-id="7afd3-158">toolearn about all peering settings, read [Manage virtual network peerings](virtual-network-manage-peering.md#create-a-peering).</span></span>
10. <span data-ttu-id="7afd3-159">После нажатия кнопки **ОК** hello в предыдущем шаге, hello **пиринг добавить** колонке закрывается, и вы увидите hello **myVnet1 - Пиринги** колонке еще раз.</span><span class="sxs-lookup"><span data-stu-id="7afd3-159">After clicking **OK** in hello previous step, hello **Add peering** blade closes and you see hello **myVnet1 - Peerings** blade again.</span></span> <span data-ttu-id="7afd3-160">Через несколько секунд hello пиринг был создан появится в колонке hello.</span><span class="sxs-lookup"><span data-stu-id="7afd3-160">After a few seconds, hello peering you created appears in hello blade.</span></span> <span data-ttu-id="7afd3-161">**Инициировано** перечисленные в hello **ПИРИНГ состояние** столбца для hello **myVnet1ToMyVnet2** пиринг можно создать.</span><span class="sxs-lookup"><span data-stu-id="7afd3-161">**Initiated** is listed in hello **PEERING STATUS** column for hello **myVnet1ToMyVnet2** peering you created.</span></span> <span data-ttu-id="7afd3-162">Одноранговыми Vnet1 tooVnet2, но теперь необходимо однорангового узла myVnet2 toomyVnet1.</span><span class="sxs-lookup"><span data-stu-id="7afd3-162">You've peered Vnet1 tooVnet2, but now you must peer myVnet2 toomyVnet1.</span></span> <span data-ttu-id="7afd3-163">пиринг Hello должны создаваться в обоих направлениях tooenable ресурсов в виртуальные сети toocommunicate hello друг с другом.</span><span class="sxs-lookup"><span data-stu-id="7afd3-163">hello peering must be created in both directions tooenable resources in hello virtual networks toocommunicate with each other.</span></span>
11. <span data-ttu-id="7afd3-164">Выполните шаги 5–10 для myVnet2.</span><span class="sxs-lookup"><span data-stu-id="7afd3-164">Complete steps 5-10 again for myVnet2.</span></span>  <span data-ttu-id="7afd3-165">Имя пиринга hello *myVnet2ToMyVnet1*.</span><span class="sxs-lookup"><span data-stu-id="7afd3-165">Name hello peering *myVnet2ToMyVnet1*.</span></span>
12. <span data-ttu-id="7afd3-166">Через несколько секунд после нажатия кнопки **ОК** toocreate hello пиринг для MyVnet2, hello **myVnet2ToMyVnet1** отмечены только что созданный план для пиринга **подключен** в hello  **СОСТОЯНИЕ ПИРИНГА** столбца.</span><span class="sxs-lookup"><span data-stu-id="7afd3-166">A few seconds after clicking **OK** toocreate hello peering for MyVnet2, hello **myVnet2ToMyVnet1** peering you just created is listed with **Connected** in hello **PEERING STATUS** column.</span></span>
13. <span data-ttu-id="7afd3-167">Выполните шаги 5–7 для myVnet1.</span><span class="sxs-lookup"><span data-stu-id="7afd3-167">Complete steps 5-7 again for MyVnet1.</span></span> <span data-ttu-id="7afd3-168">Hello **ПИРИНГ состояние** для hello **myVnet1ToVNet2** пиринг теперь также является **подключен**.</span><span class="sxs-lookup"><span data-stu-id="7afd3-168">hello **PEERING STATUS** for hello **myVnet1ToVNet2** peering is now also **Connected**.</span></span> <span data-ttu-id="7afd3-169">пиринг Hello успешно установлено, проверив **подключен** в hello **ПИРИНГ состояние** столбца для обеих виртуальных сетей в пиринге hello.</span><span class="sxs-lookup"><span data-stu-id="7afd3-169">hello peering is successfully established after you see **Connected** in hello **PEERING STATUS** column for both virtual networks in hello peering.</span></span>
14. <span data-ttu-id="7afd3-170">**Необязательный**: хотя Создание виртуальных машин не освещены в учебнике, можно создать виртуальную машину в каждой виртуальной сети и подключение из одной виртуальной машины toohello других, toovalidate подключения.</span><span class="sxs-lookup"><span data-stu-id="7afd3-170">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
15. <span data-ttu-id="7afd3-171">**Необязательный**: ресурсов hello toodelete, созданных в этом учебнике, hello завершения шагов в hello [удаление ресурсов](#delete-portal) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="7afd3-171">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in hello [Delete resources](#delete-portal) section of this article.</span></span>

<span data-ttu-id="7afd3-172">Все ресурсы Azure, созданные в любой виртуальной сети, теперь может toocommunicate друг с другом через свои IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="7afd3-172">Any Azure resources you create in either virtual network are now able toocommunicate with each other through their IP addresses.</span></span> <span data-ttu-id="7afd3-173">При использовании разрешение имен Azure по умолчанию для виртуальных сетей hello hello ресурсы в виртуальных сетях hello не может tooresolve имен между виртуальными сетями hello.</span><span class="sxs-lookup"><span data-stu-id="7afd3-173">If you're using default Azure name resolution for hello virtual networks, hello resources in hello virtual networks are not able tooresolve names across hello virtual networks.</span></span> <span data-ttu-id="7afd3-174">Если требуется tooresolve имен между виртуальными сетями в пиринге необходимо создать собственный DNS-сервер.</span><span class="sxs-lookup"><span data-stu-id="7afd3-174">If you want tooresolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="7afd3-175">Узнайте, как tooset копирование [разрешение имен с помощью DNS-сервере](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span><span class="sxs-lookup"><span data-stu-id="7afd3-175">Learn how tooset up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

## <span data-ttu-id="7afd3-176"><a name="cli"></a>Создание пиринга с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7afd3-176"><a name="cli"></a>Create peering - Azure CLI</span></span>

<span data-ttu-id="7afd3-177">Здравствуйте, следующий скрипт:</span><span class="sxs-lookup"><span data-stu-id="7afd3-177">hello following script:</span></span>

- <span data-ttu-id="7afd3-178">Требуется hello Azure CLI версия 2.0.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="7afd3-178">Requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="7afd3-179">версия toofind hello, запустите hello `az --version` команды.</span><span class="sxs-lookup"><span data-stu-id="7afd3-179">toofind hello version, run hello `az --version` command.</span></span> <span data-ttu-id="7afd3-180">Получить tooupgrade [установить CLI Azure 2.0]( /cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7afd3-180">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
- <span data-ttu-id="7afd3-181">Этот сценарий работает в оболочке Bash.</span><span class="sxs-lookup"><span data-stu-id="7afd3-181">Works in a Bash shell.</span></span> <span data-ttu-id="7afd3-182">Параметры запуска на клиенте Windows Azure CLI скриптов см [работающих в Windows Azure CLI hello](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7afd3-182">For options on running Azure CLI scripts on Windows client, see [Running hello Azure CLI in Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> 

<span data-ttu-id="7afd3-183">Вместо установки hello CLI и его зависимости, можно использовать hello оболочки облако Azure.</span><span class="sxs-lookup"><span data-stu-id="7afd3-183">Instead of installing hello CLI and its dependencies, you can use hello Azure Cloud Shell.</span></span> <span data-ttu-id="7afd3-184">Hello оболочки облако Azure — это бесплатные Bash, который выполняется непосредственно в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="7afd3-184">hello Azure Cloud Shell is a free Bash shell that you can run directly within hello Azure portal.</span></span> <span data-ttu-id="7afd3-185">Он имеет hello Azure CLI предварительно установить и настроить toouse с вашей учетной записью.</span><span class="sxs-lookup"><span data-stu-id="7afd3-185">It has hello Azure CLI preinstalled and configured toouse with your account.</span></span> <span data-ttu-id="7afd3-186">Нажмите кнопку hello **опробовать** кнопку в скрипте hello, показано ниже, которые вызывает облака оболочке, которая будет входить tooyour учетная запись Azure с.</span><span class="sxs-lookup"><span data-stu-id="7afd3-186">Click hello **Try it** button in hello script that follows, which invokes a Cloud Shell that logs you can log in tooyour Azure account with.</span></span> <span data-ttu-id="7afd3-187">tooexecute Здравствуйте сценарий, нажмите кнопку hello **копирования** кнопку и вставьте содержимое hello в облаке оболочка.</span><span class="sxs-lookup"><span data-stu-id="7afd3-187">tooexecute hello script, click hello **Copy** button and paste hello contents into your Cloud Shell.</span></span>

1. <span data-ttu-id="7afd3-188">Создайте группу ресурсов и две виртуальные сети.</span><span class="sxs-lookup"><span data-stu-id="7afd3-188">Create a resource group and two virtual networks.</span></span>

    ```azurecli-interactive
    #!/bin/bash

    # Variables for common values used throughout hello script.
    rgName="myResourceGroup"
    location="eastus"

    # Create a resource group.
    az group create \
      --name $rgName \
      --location $location

    # Create virtual network 1.
    az network vnet create \
      --name myVnet1 \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.0.0.0/16

    # Create virtual network 2.
    az network vnet create \
      --name myVnet2 \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.1.0.0/16
    ```

2. <span data-ttu-id="7afd3-189">Создайте виртуальную сеть пиринга между двумя виртуальными сетями hello.</span><span class="sxs-lookup"><span data-stu-id="7afd3-189">Create a virtual network peering between hello two virtual networks.</span></span>
 
    ```azurecli-interactive
    # Get hello id for VNet1.
    vnet1Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet1 \
      --query id --out tsv)

    # Get hello id for VNet2.
    vnet2Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet2 \
      --query id \
      --out tsv)

    # Peer VNet1 tooVNet2.
    az network vnet peering create \
      --name myVnet1ToMyVnet2 \
      --resource-group $rgName \
      --vnet-name myVnet1 \
      --remote-vnet-id $vnet2Id \
      --allow-vnet-access

    # Peer VNet2 tooVNet1.
    az network vnet peering create \
      --name myVnet2ToMyVnet1 \
      --resource-group $rgName \
      --vnet-name myVnet2 \
      --remote-vnet-id $vnet1Id \
      --allow-vnet-access
    ```

3. <span data-ttu-id="7afd3-190">После выполнения скрипта hello, просмотрите hello пиринги для каждой виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="7afd3-190">After hello script executes, review hello peerings for each virtual network.</span></span> 

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --output table
    ```
    
    <span data-ttu-id="7afd3-191">Hello предыдущего снова выполните команду, заменив *myVnet1* с *myVnet2*.</span><span class="sxs-lookup"><span data-stu-id="7afd3-191">Run hello previous command again, replacing *myVnet1* with *myVnet2*.</span></span> <span data-ttu-id="7afd3-192">выходные данные Hello обоих команд показано **подключен** в hello **PeeringState** столбца.</span><span class="sxs-lookup"><span data-stu-id="7afd3-192">hello output of both commands shows **Connected** in hello **PeeringState** column.</span></span>

     <span data-ttu-id="7afd3-193">Все ресурсы Azure, созданные в любой виртуальной сети, теперь может toocommunicate друг с другом через свои IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="7afd3-193">Any Azure resources you create in either virtual network are now able toocommunicate with each other through their IP addresses.</span></span> <span data-ttu-id="7afd3-194">При использовании разрешение имен Azure по умолчанию для виртуальных сетей hello hello ресурсы в виртуальных сетях hello не может tooresolve имен между виртуальными сетями hello.</span><span class="sxs-lookup"><span data-stu-id="7afd3-194">If you're using default Azure name resolution for hello virtual networks, hello resources in hello virtual networks are not able tooresolve names across hello virtual networks.</span></span> <span data-ttu-id="7afd3-195">Если требуется tooresolve имен между виртуальными сетями в пиринге необходимо создать собственный DNS-сервер.</span><span class="sxs-lookup"><span data-stu-id="7afd3-195">If you want tooresolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="7afd3-196">Узнайте, как tooset копирование [разрешение имен с помощью DNS-сервере](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span><span class="sxs-lookup"><span data-stu-id="7afd3-196">Learn how tooset up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

4. <span data-ttu-id="7afd3-197">**Необязательный**: хотя Создание виртуальных машин не освещены в учебнике, можно создать виртуальную машину в каждой виртуальной сети и подключение из одной виртуальной машины toohello других, toovalidate подключения.</span><span class="sxs-lookup"><span data-stu-id="7afd3-197">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
5. <span data-ttu-id="7afd3-198">**Необязательный**: ресурсов hello toodelete, созданных в этом учебнике, hello завершения шагов в [удаление ресурсов](#delete-cli) в этой статье.</span><span class="sxs-lookup"><span data-stu-id="7afd3-198">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in [Delete resources](#delete-cli) in this article.</span></span>


## <span data-ttu-id="7afd3-199"><a name="powershell"></a>Создание пиринга с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="7afd3-199"><a name="powershell"></a>Create peering - PowerShell</span></span>

1. <span data-ttu-id="7afd3-200">Установите последнюю версию hello hello PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) модуля.</span><span class="sxs-lookup"><span data-stu-id="7afd3-200">Install hello latest version of hello PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="7afd3-201">Если у вас отсутствует новый tooAzure PowerShell, [Обзор Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7afd3-201">If you're new tooAzure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="7afd3-202">toostart сеанс PowerShell перейдите слишком**запустить**, введите **powershell**и нажмите кнопку **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="7afd3-202">toostart a PowerShell session, go too**Start**, enter **powershell**, and then click **PowerShell**.</span></span>
3. <span data-ttu-id="7afd3-203">В PowerShell, войдите в tooAzure, указав hello `login-azurermaccount` команды.</span><span class="sxs-lookup"><span data-stu-id="7afd3-203">In PowerShell, log in tooAzure by entering hello `login-azurermaccount` command.</span></span> <span data-ttu-id="7afd3-204">Hello учетной записи, использованной для входа в систему должен иметь необходимые разрешения toocreate hello пиринг виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="7afd3-204">hello account you log in with must have hello necessary permissions toocreate a virtual network peering.</span></span> <span data-ttu-id="7afd3-205">В разделе hello [разрешения](#permissions) Дополнительные сведения см.</span><span class="sxs-lookup"><span data-stu-id="7afd3-205">See hello [Permissions](#permissions) section of this article for details.</span></span>
4. <span data-ttu-id="7afd3-206">Создайте группу ресурсов и две виртуальные сети.</span><span class="sxs-lookup"><span data-stu-id="7afd3-206">Create a resource group and two virtual networks.</span></span> <span data-ttu-id="7afd3-207">сценарий tooexecute hello, копировать hello следующую скрипта, вставьте его в PowerShell и нажмите клавишу `Enter` после последняя строка hello отображается на экране приветствия:</span><span class="sxs-lookup"><span data-stu-id="7afd3-207">tooexecute hello script, copy hello following script, paste it into PowerShell, and then press `Enter` after hello last line appears on hello screen:</span></span>

    ```powershell
    # Variables for common values used throughout hello script.
    $rgName='myResourceGroup'
    $location='eastus'

    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name $rgName `
      -Location $location

    # Create virtual network 1.
    $vnet1 = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnet1' `
      -AddressPrefix '10.0.0.0/16' `
      -Location $location

    # Create virtual network 2.
    $vnet2 = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnet2' `
      -AddressPrefix '10.1.0.0/16' `
      -Location $location
    ```

5. <span data-ttu-id="7afd3-208">Создайте виртуальную сеть пиринга между двумя виртуальными сетями hello.</span><span class="sxs-lookup"><span data-stu-id="7afd3-208">Create a virtual network peering between hello two virtual networks.</span></span> <span data-ttu-id="7afd3-209">Копирования hello следующий скрипт, вставьте в tooPowerShell и нажмите клавишу `Enter` после последняя строка hello отображается на экране приветствия:</span><span class="sxs-lookup"><span data-stu-id="7afd3-209">Copy hello following script, paste in tooPowerShell, and then press `Enter` after hello last line appears on hello screen:</span></span>
    ```powershell
    # Peer VNet1 tooVNet2.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet1ToMyVnet2' `
      -VirtualNetwork $vnet1 `
      -RemoteVirtualNetworkId $vnet2.Id

    # Peer VNet2 tooVNet1.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet2ToMyVnet1' `
      -VirtualNetwork $vnet2 `
      -RemoteVirtualNetworkId $vnet1.Id
    ```
6. <span data-ttu-id="7afd3-210">tooreview hello подсетей для виртуальной сети hello, копировать hello следующую команду, вставьте в tooPowerShell и нажмите клавишу `Enter`:</span><span class="sxs-lookup"><span data-stu-id="7afd3-210">tooreview hello subnets for hello virtual network, copy hello following command, paste in tooPowerShell, and then press `Enter`:</span></span>

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroup `
      -VirtualNetworkName myVnet1 `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    <span data-ttu-id="7afd3-211">Hello предыдущего снова выполните команду, заменив *myVnet1* с *myVnet2*.</span><span class="sxs-lookup"><span data-stu-id="7afd3-211">Run hello previous command again, replacing *myVnet1* with *myVnet2*.</span></span> <span data-ttu-id="7afd3-212">выходные данные Hello обоих команд показано **подключен** в hello **PeeringState** столбца.</span><span class="sxs-lookup"><span data-stu-id="7afd3-212">hello output of both commands shows **Connected** in hello **PeeringState** column.</span></span>
7. <span data-ttu-id="7afd3-213">**Необязательный**: хотя Создание виртуальных машин не освещены в учебнике, можно создать виртуальную машину в каждой виртуальной сети и подключение из одной виртуальной машины toohello других, toovalidate подключения.</span><span class="sxs-lookup"><span data-stu-id="7afd3-213">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
8. <span data-ttu-id="7afd3-214">**Необязательный**: ресурсов hello toodelete, созданных в этом учебнике, hello завершения шагов в [удаление ресурсов](#delete-powershell) в этой статье.</span><span class="sxs-lookup"><span data-stu-id="7afd3-214">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in [Delete resources](#delete-powershell) in this article.</span></span>

<span data-ttu-id="7afd3-215">Все ресурсы Azure, созданные в любой виртуальной сети, теперь может toocommunicate друг с другом через свои IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="7afd3-215">Any Azure resources you create in either virtual network are now able toocommunicate with each other through their IP addresses.</span></span> <span data-ttu-id="7afd3-216">При использовании разрешение имен Azure по умолчанию для виртуальных сетей hello hello ресурсы в виртуальных сетях hello не может tooresolve имен между виртуальными сетями hello.</span><span class="sxs-lookup"><span data-stu-id="7afd3-216">If you're using default Azure name resolution for hello virtual networks, hello resources in hello virtual networks are not able tooresolve names across hello virtual networks.</span></span> <span data-ttu-id="7afd3-217">Если требуется tooresolve имен между виртуальными сетями в пиринге необходимо создать собственный DNS-сервер.</span><span class="sxs-lookup"><span data-stu-id="7afd3-217">If you want tooresolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="7afd3-218">Узнайте, как tooset копирование [разрешение имен с помощью DNS-сервере](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span><span class="sxs-lookup"><span data-stu-id="7afd3-218">Learn how tooset up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

## <span data-ttu-id="7afd3-219"><a name="template"></a>Создание пиринга с помощью шаблона Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7afd3-219"><a name="template"></a>Create peering - Resource Manager template</span></span>

1. <span data-ttu-id="7afd3-220">В качестве примера используйте шаблон Azure Resource Manager для [создания пиринга виртуальных сетей](https://azure.microsoft.com/resources/templates/201-vnet-to-vnet-peering).</span><span class="sxs-lookup"><span data-stu-id="7afd3-220">Reference [Create a virtual network peering](https://azure.microsoft.com/resources/templates/201-vnet-to-vnet-peering) Resource Manager template.</span></span> <span data-ttu-id="7afd3-221">Инструкции приведены шаблоном hello развертывания hello шаблона с помощью hello портал Azure, PowerShell или Azure CLI hello.</span><span class="sxs-lookup"><span data-stu-id="7afd3-221">Instructions are provided with hello template for deploying hello template using hello Azure portal, PowerShell, or hello Azure CLI.</span></span> <span data-ttu-id="7afd3-222">Журнал в средстве toowhichever выбранный шаблон hello toodeploy с учетной записью, обладающей hello toocreate необходимые разрешения пиринг виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="7afd3-222">Log in toowhichever tool you choose toodeploy hello template with using an account that has hello necessary permissions toocreate a virtual network peering.</span></span> <span data-ttu-id="7afd3-223">В разделе hello [разрешения](#permissions) Дополнительные сведения см.</span><span class="sxs-lookup"><span data-stu-id="7afd3-223">See hello [Permissions](#permissions) section of this article for details.</span></span>
2. <span data-ttu-id="7afd3-224">**Необязательный**: хотя Создание виртуальных машин не освещены в учебнике, можно создать виртуальную машину в каждой виртуальной сети и подключение из одной виртуальной машины toohello других, toovalidate подключения.</span><span class="sxs-lookup"><span data-stu-id="7afd3-224">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
3. <span data-ttu-id="7afd3-225">**Необязательный**: ресурсов hello toodelete, созданных в этом учебнике, hello завершения шагов в hello [удаление ресурсов](#delete) hello данной статьи с помощью портала Azure, PowerShell или Azure CLI hello.</span><span class="sxs-lookup"><span data-stu-id="7afd3-225">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in hello [Delete resources](#delete) section of this article, using either hello Azure portal, PowerShell, or hello Azure CLI.</span></span>

## <span data-ttu-id="7afd3-226"><a name="permissions"></a>Разрешения</span><span class="sxs-lookup"><span data-stu-id="7afd3-226"><a name="permissions"></a>Permissions</span></span>

<span data-ttu-id="7afd3-227">Привет, используется toocreate пиринг виртуальной сети должны иметь hello необходимые роли и разрешения.</span><span class="sxs-lookup"><span data-stu-id="7afd3-227">hello accounts you use toocreate a virtual network peering must have hello necessary role or permissions.</span></span> <span data-ttu-id="7afd3-228">Например если две виртуальные сети, с именем VNet1 и VNet2 пиринг, учетной записи должно быть назначено hello следующие минимальные роли или разрешения для каждой виртуальной сети:</span><span class="sxs-lookup"><span data-stu-id="7afd3-228">For example, if you were peering two virtual networks named VNet1 and VNet2, your account must be assigned hello following minimum role or permissions for each virtual network:</span></span>
    
|<span data-ttu-id="7afd3-229">Виртуальная сеть</span><span class="sxs-lookup"><span data-stu-id="7afd3-229">Virtual network</span></span>|<span data-ttu-id="7afd3-230">Роль</span><span class="sxs-lookup"><span data-stu-id="7afd3-230">Role</span></span>|<span data-ttu-id="7afd3-231">Разрешения</span><span class="sxs-lookup"><span data-stu-id="7afd3-231">Permissions</span></span>|
|---|---|---|
|<span data-ttu-id="7afd3-232">VNet1</span><span class="sxs-lookup"><span data-stu-id="7afd3-232">VNet1</span></span>|[<span data-ttu-id="7afd3-233">Участник сети</span><span class="sxs-lookup"><span data-stu-id="7afd3-233">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="7afd3-234">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span><span class="sxs-lookup"><span data-stu-id="7afd3-234">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span></span>|
|<span data-ttu-id="7afd3-235">VNet2</span><span class="sxs-lookup"><span data-stu-id="7afd3-235">VNet2</span></span>|[<span data-ttu-id="7afd3-236">Участник сети</span><span class="sxs-lookup"><span data-stu-id="7afd3-236">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="7afd3-237">Microsoft.Network/virtualNetworks/peer</span><span class="sxs-lookup"><span data-stu-id="7afd3-237">Microsoft.Network/virtualNetworks/peer</span></span>|

<span data-ttu-id="7afd3-238">Дополнительные сведения о [встроенные роли](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) и назначение разрешений для конкретного слишком[пользовательские роли](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (только для диспетчера ресурсов).</span><span class="sxs-lookup"><span data-stu-id="7afd3-238">Learn more about [built-in roles](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) and assigning specific permissions too[custom roles](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (Resource Manager only).</span></span>

## <span data-ttu-id="7afd3-239"><a name="delete"></a>Удаление ресурсов</span><span class="sxs-lookup"><span data-stu-id="7afd3-239"><a name="delete"></a>Delete resources</span></span>
<span data-ttu-id="7afd3-240">После завершения этого учебника вы можете toodelete hello ресурсы, созданный в учебнике hello, поэтому не приводит к дополнительным расходам.</span><span class="sxs-lookup"><span data-stu-id="7afd3-240">When you've finished this tutorial, you might want toodelete hello resources you created in hello tutorial, so you don't incur usage charges.</span></span> <span data-ttu-id="7afd3-241">При удалении группы ресурсов также удаляются все ресурсы, которые находятся в группе ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="7afd3-241">Deleting a resource group also deletes all resources that are in hello resource group.</span></span>

### <span data-ttu-id="7afd3-242"><a name="delete-portal"></a>Портал Azure</span><span class="sxs-lookup"><span data-stu-id="7afd3-242"><a name="delete-portal"></a>Azure portal</span></span>

1. <span data-ttu-id="7afd3-243">Введите в поле поиска портала hello, **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="7afd3-243">In hello portal search box, enter **myResourceGroup**.</span></span> <span data-ttu-id="7afd3-244">В результатах поиска hello, нажмите кнопку **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="7afd3-244">In hello search results, click **myResourceGroup**.</span></span>
2. <span data-ttu-id="7afd3-245">На hello **myResourceGroup** колонка, щелкните hello **удалить** значок.</span><span class="sxs-lookup"><span data-stu-id="7afd3-245">On hello **myResourceGroup** blade, click hello **Delete** icon.</span></span>
3. <span data-ttu-id="7afd3-246">Удаление hello tooconfirm, в hello **ТИПА hello имя группы РЕСУРСОВ** введите **myResourceGroup**и нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="7afd3-246">tooconfirm hello deletion, in hello **TYPE hello RESOURCE GROUP NAME** box, enter **myResourceGroup**, and then click **Delete**.</span></span>

### <span data-ttu-id="7afd3-247"><a name="delete-cli"></a>Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="7afd3-247"><a name="delete-cli"></a>Azure CLI</span></span>

<span data-ttu-id="7afd3-248">Введите следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="7afd3-248">Enter hello following command:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

### <span data-ttu-id="7afd3-249"><a name="delete-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="7afd3-249"><a name="delete-powershell"></a>PowerShell</span></span>

<span data-ttu-id="7afd3-250">Введите следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="7afd3-250">Enter hello following command:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -force
```

## <a name="next-steps"></a><span data-ttu-id="7afd3-251">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7afd3-251">Next steps</span></span>

- <span data-ttu-id="7afd3-252">Внимательно ознакомьтесь с важными [ограничениями и особенностями работы пиринга виртуальных сетей](virtual-network-manage-peering.md#requirements-and-constraints), прежде чем создавать пиринг виртуальных сетей для рабочей среды.</span><span class="sxs-lookup"><span data-stu-id="7afd3-252">Thoroughly familiarize yourself with important [virtual network peering constraints and behaviors](virtual-network-manage-peering.md#requirements-and-constraints) before creating a virtual network peering for production use.</span></span>
- <span data-ttu-id="7afd3-253">Узнайте о [параметрах пиринга виртуальных сетей](virtual-network-manage-peering.md#create-a-peering).</span><span class="sxs-lookup"><span data-stu-id="7afd3-253">Learn about all [virtual network peering settings](virtual-network-manage-peering.md#create-a-peering).</span></span>
- <span data-ttu-id="7afd3-254">Узнайте, каким образом слишком[создать концентратор и топология сети резервный](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) с пиринг виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="7afd3-254">Learn how too[create a hub and spoke network topology](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) with virtual network peering.</span></span>
