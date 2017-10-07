---
title: "aaaDelete Azure кластера и его ресурсам | Документы Microsoft"
description: "Сведения об использовании delete toocompletely структуры службы кластера либо удаление группы ресурсов hello, содержащий hello кластера или путем выборочного удаления ресурсов."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: de422950-2d22-4ddb-ac47-dd663a946a7e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/24/2017
ms.author: chackdan
ms.openlocfilehash: 5c15a4184644da715cd69397f2150de86ab433ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="delete-a-service-fabric-cluster-on-azure-and-hello-resources-it-uses"></a><span data-ttu-id="2b1b0-103">Удаление кластера Service Fabric на Azure и hello ресурсы, используемые в нем</span><span class="sxs-lookup"><span data-stu-id="2b1b0-103">Delete a Service Fabric cluster on Azure and hello resources it uses</span></span>
<span data-ttu-id="2b1b0-104">Кластера Service Fabric состоит из многих других ресурсов Azure в дополнение к этому toohello сам ресурс кластера.</span><span class="sxs-lookup"><span data-stu-id="2b1b0-104">A Service Fabric cluster is made up of many other Azure resources in addition toohello cluster resource itself.</span></span> <span data-ttu-id="2b1b0-105">Поэтому toocompletely Удаление кластера Service Fabric требуется также toodelete Здравствуйте, все ресурсы, которые оно состоит из.</span><span class="sxs-lookup"><span data-stu-id="2b1b0-105">So toocompletely delete a Service Fabric cluster you also need toodelete all hello resources it is made of.</span></span>
<span data-ttu-id="2b1b0-106">У вас есть два варианта: либо удаление hello группы ресурсов, hello кластера находится в (которая удаляет hello кластерных ресурсов и другие ресурсы в группе ресурсов hello) или специально удалить ресурс кластера hello и связанные с ним ресурсы (но не другие ресурсы в группе ресурсов hello).</span><span class="sxs-lookup"><span data-stu-id="2b1b0-106">You have two options: Either delete hello resource group that hello cluster is in (which deletes hello cluster resource and any other resources in hello resource group) or specifically delete hello cluster resource and it's associated resources (but not other resources in hello resource group).</span></span>

> [!NOTE]
> <span data-ttu-id="2b1b0-107">Удаление ресурса кластера hello **не** удаления всех hello другие ресурсы, которые состоят из кластера Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="2b1b0-107">Deleting hello cluster resource **does not** delete all hello other resources that your Service Fabric cluster is composed of.</span></span>
> 
> 

## <a name="delete-hello-entire-resource-group-rg-that-hello-service-fabric-cluster-is-in"></a><span data-ttu-id="2b1b0-108">Удалите hello весь ресурс (группа Ресурсов), hello кластера Service Fabric</span><span class="sxs-lookup"><span data-stu-id="2b1b0-108">Delete hello entire resource group (RG) that hello Service Fabric cluster is in</span></span>
<span data-ttu-id="2b1b0-109">Это простой способ tooensure hello удалить все ресурсы hello, связанной с кластером, включая группу ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="2b1b0-109">This is hello easiest way tooensure that you delete all hello resources associated with your cluster, including hello resource group.</span></span> <span data-ttu-id="2b1b0-110">Можно удалить группу ресурсов hello, с помощью PowerShell или с помощью портала Azure hello.</span><span class="sxs-lookup"><span data-stu-id="2b1b0-110">You can delete hello resource group using PowerShell or through hello Azure portal.</span></span> <span data-ttu-id="2b1b0-111">Если группы ресурсов содержит ресурсы, которые не являются связанные tooService структуры кластера, можно удалить отдельные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="2b1b0-111">If your resource group has resources that are not related tooService fabric cluster, then you can delete specific resources.</span></span>

### <a name="delete-hello-resource-group-using-azure-powershell"></a><span data-ttu-id="2b1b0-112">Удаление группы ресурсов hello, с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2b1b0-112">Delete hello resource group using Azure PowerShell</span></span>
<span data-ttu-id="2b1b0-113">Можно также удалить группу ресурсов hello, выполнив следующие командлеты Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="2b1b0-113">You can also delete hello resource group by running hello following Azure PowerShell cmdlets.</span></span> <span data-ttu-id="2b1b0-114">Убедитесь, что на компьютере установлена среда Azure PowerShell 1.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="2b1b0-114">Make sure Azure PowerShell 1.0 or greater is installed on your computer.</span></span> <span data-ttu-id="2b1b0-115">Если вы не выполнили это перед, выполните hello действия, описанные в [как tooinstall и настройка Azure PowerShell.](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="2b1b0-115">If you have not done this before, follow hello steps outlined in [How tooinstall and Configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="2b1b0-116">Откройте окно PowerShell и выполните следующие командлеты PS hello:</span><span class="sxs-lookup"><span data-stu-id="2b1b0-116">Open a PowerShell window and run hello following PS cmdlets:</span></span>

```powershell
Login-AzureRmAccount

Remove-AzureRmResourceGroup -Name <name of ResouceGroup> -Force
```

<span data-ttu-id="2b1b0-117">Удаление hello prompt tooconfirm будет работать, если вы не использовали hello *-Force* параметр.</span><span class="sxs-lookup"><span data-stu-id="2b1b0-117">You will get a prompt tooconfirm hello deletion if you did not use hello *-Force* option.</span></span> <span data-ttu-id="2b1b0-118">На подтверждение hello RG и все ресурсы hello, содержащиеся в нем удаляются.</span><span class="sxs-lookup"><span data-stu-id="2b1b0-118">On confirmation hello RG and all hello resources it contains are deleted.</span></span>

### <a name="delete-a-resource-group-in-hello-azure-portal"></a><span data-ttu-id="2b1b0-119">Удаление группы ресурсов в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="2b1b0-119">Delete a resource group in hello Azure portal</span></span>
1. <span data-ttu-id="2b1b0-120">Имя входа toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2b1b0-120">Login toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="2b1b0-121">Переход кластера Service Fabric toohello требуется toodelete.</span><span class="sxs-lookup"><span data-stu-id="2b1b0-121">Navigate toohello Service Fabric cluster you want toodelete.</span></span>
3. <span data-ttu-id="2b1b0-122">Щелкните имя группы ресурсов на странице essentials кластера hello hello.</span><span class="sxs-lookup"><span data-stu-id="2b1b0-122">Click on hello Resource Group name on hello cluster essentials page.</span></span>
4. <span data-ttu-id="2b1b0-123">Откроется окно hello **Essentials группы ресурсов** страницы.</span><span class="sxs-lookup"><span data-stu-id="2b1b0-123">This brings up hello **Resource Group Essentials** page.</span></span>
5. <span data-ttu-id="2b1b0-124">Нажмите кнопку **Delete**(Удалить).</span><span class="sxs-lookup"><span data-stu-id="2b1b0-124">Click **Delete**.</span></span>
6. <span data-ttu-id="2b1b0-125">Следуйте инструкциям hello на этой странице toocomplete hello удаления группы ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="2b1b0-125">Follow hello instructions on that page toocomplete hello deletion of hello resource group.</span></span>

![Удаление группы ресурсов][ResourceGroupDelete]

## <a name="delete-hello-cluster-resource-and-hello-resources-it-uses-but-not-other-resources-in-hello-resource-group"></a><span data-ttu-id="2b1b0-127">Удалить ресурс кластера hello и hello ресурсы, используемые в нем, но не другие ресурсы в группе ресурсов hello</span><span class="sxs-lookup"><span data-stu-id="2b1b0-127">Delete hello cluster resource and hello resources it uses, but not other resources in hello resource group</span></span>
<span data-ttu-id="2b1b0-128">Если группы ресурсов содержит только ресурсы, связанные toohello кластера Service Fabric требуется toodelete, а затем проще toodelete hello весь ресурс группа.</span><span class="sxs-lookup"><span data-stu-id="2b1b0-128">If your resource group has only resources that are related toohello Service Fabric cluster you want toodelete, then it is easier toodelete hello entire resource group.</span></span> <span data-ttu-id="2b1b0-129">Если вы собираетесь tooselectively delete hello ресурсы по одному в группе ресурсов, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="2b1b0-129">If you want tooselectively delete hello resources one-by-one in your resource group, then follow these steps.</span></span>

<span data-ttu-id="2b1b0-130">При развертывании кластера с помощью портала hello, или с помощью одного из шаблонов диспетчера ресурсов структуры службы hello из галереи шаблонов hello ресурсами hello, hello кластера использует помечены hello, следующие два теги.</span><span class="sxs-lookup"><span data-stu-id="2b1b0-130">If you deployed your cluster using hello portal or using one of hello Service Fabric Resource Manager templates from hello template gallery, then all hello resources that hello cluster uses are tagged with hello following two tags.</span></span> <span data-ttu-id="2b1b0-131">Их можно использовать, какие ресурсы должны toodecide toodelete.</span><span class="sxs-lookup"><span data-stu-id="2b1b0-131">You can use them toodecide which resources you want toodelete.</span></span>

<span data-ttu-id="2b1b0-132">***Тег #1:*** ключ = clusterName, значение = «имя кластера hello»</span><span class="sxs-lookup"><span data-stu-id="2b1b0-132">***Tag#1:*** Key = clusterName, Value = 'name of hello cluster'</span></span>

<span data-ttu-id="2b1b0-133">***Тег 2:*** ключ = resourceName, значение = ServiceFabric.</span><span class="sxs-lookup"><span data-stu-id="2b1b0-133">***Tag#2:*** Key = resourceName, Value = ServiceFabric</span></span>

### <a name="delete-specific-resources-in-hello-azure-portal"></a><span data-ttu-id="2b1b0-134">Удаление конкретных ресурсов hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="2b1b0-134">Delete specific resources in hello Azure portal</span></span>
1. <span data-ttu-id="2b1b0-135">Имя входа toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2b1b0-135">Login toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="2b1b0-136">Переход кластера Service Fabric toohello требуется toodelete.</span><span class="sxs-lookup"><span data-stu-id="2b1b0-136">Navigate toohello Service Fabric cluster you want toodelete.</span></span>
3. <span data-ttu-id="2b1b0-137">Go слишком**все параметры** колонке essentials hello.</span><span class="sxs-lookup"><span data-stu-id="2b1b0-137">Go too**All settings** on hello essentials blade.</span></span>
4. <span data-ttu-id="2b1b0-138">Щелкните **теги** под **управление ресурсами** в колонке параметров hello.</span><span class="sxs-lookup"><span data-stu-id="2b1b0-138">Click on **Tags** under **Resource Management** in hello settings blade.</span></span>
5. <span data-ttu-id="2b1b0-139">Выберите одну из hello **теги** в tooget колонки теги hello список всех ресурсов hello с этим тегом.</span><span class="sxs-lookup"><span data-stu-id="2b1b0-139">Click on one of hello **Tags** in hello tags blade tooget a list of all hello resources with that tag.</span></span>
   
    ![Теги ресурсов][ResourceTags]
6. <span data-ttu-id="2b1b0-141">Получив hello перечень ресурсов, заключенное в теги, щелкните на каждом из ресурсов hello и удалите их.</span><span class="sxs-lookup"><span data-stu-id="2b1b0-141">Once you have hello list of tagged resources, click on each of hello resources and delete them.</span></span>
   
    ![Ресурсы с тегами][TaggedResources]

### <a name="delete-hello-resources-using-azure-powershell"></a><span data-ttu-id="2b1b0-143">Удаление hello ресурсов с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2b1b0-143">Delete hello resources using Azure PowerShell</span></span>
<span data-ttu-id="2b1b0-144">Hello ресурсы по одному можно удалить, выполнив следующие командлеты Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="2b1b0-144">You can delete hello resources one-by-one by running hello following Azure PowerShell cmdlets.</span></span> <span data-ttu-id="2b1b0-145">Убедитесь, что на компьютере установлена среда Azure PowerShell 1.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="2b1b0-145">Make sure Azure PowerShell 1.0 or greater is installed on your computer.</span></span> <span data-ttu-id="2b1b0-146">Если вы не выполнили это перед, выполните hello действия, описанные в [как tooinstall и настройка Azure PowerShell.](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="2b1b0-146">If you have not done this before, follow hello steps outlined in [How tooinstall and Configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="2b1b0-147">Откройте окно PowerShell и выполните следующие командлеты PS hello:</span><span class="sxs-lookup"><span data-stu-id="2b1b0-147">Open a PowerShell window and run hello following PS cmdlets:</span></span>

```powershell
Login-AzureRmAccount
```
<span data-ttu-id="2b1b0-148">Для каждого ресурса hello нужны toodelete, hello следующей:</span><span class="sxs-lookup"><span data-stu-id="2b1b0-148">For each of hello resources you want toodelete, run hello following:</span></span>

```powershell
Remove-AzureRmResource -ResourceName "<name of hello Resource>" -ResourceType "<Resource Type>" -ResourceGroupName "<name of hello resource group>" -Force
```

<span data-ttu-id="2b1b0-149">toodelete hello ресурса кластера, запустите следующие hello:</span><span class="sxs-lookup"><span data-stu-id="2b1b0-149">toodelete hello cluster resource, run hello following:</span></span>

```powershell
Remove-AzureRmResource -ResourceName "<name of hello Resource>" -ResourceType "Microsoft.ServiceFabric/clusters" -ResourceGroupName "<name of hello resource group>" -Force
```

## <a name="next-steps"></a><span data-ttu-id="2b1b0-150">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2b1b0-150">Next steps</span></span>
<span data-ttu-id="2b1b0-151">После tooalso hello чтения сведения о обновлением кластера и секционирование службы:</span><span class="sxs-lookup"><span data-stu-id="2b1b0-151">Read hello following tooalso learn about upgrading a cluster and partitioning services:</span></span>

* [<span data-ttu-id="2b1b0-152">Узнайте об обновлениях кластера.</span><span class="sxs-lookup"><span data-stu-id="2b1b0-152">Learn about cluster upgrades</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="2b1b0-153">Узнайте о секционировании служб с отслеживанием для максимального масштабирования.</span><span class="sxs-lookup"><span data-stu-id="2b1b0-153">Learn about partitioning stateful services for maximum scale</span></span>](service-fabric-concepts-partitioning.md)

<!--Image references-->
[ResourceGroupDelete]: ./media/service-fabric-cluster-delete/ResourceGroupDelete.PNG

[ResourceTags]: ./media/service-fabric-cluster-delete/ResourceTags.png

[TaggedResources]: ./media/service-fabric-cluster-delete/TaggedResources.PNG
