---
title: "Удаление кластера Azure и его ресурсов | Документация Майкрософт"
description: "Сведения о том, как полностью удалить кластер Service Fabric путем удаления содержащей кластер группы ресурсов или выборочного удаления отдельных ресурсов."
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
ms.openlocfilehash: 7672aa12421fbe4ad86e7315d6a7a06c2ff5124d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="delete-a-service-fabric-cluster-on-azure-and-the-resources-it-uses"></a><span data-ttu-id="b1383-103">Удаление кластера Service Fabric в Azure и используемых им ресурсов</span><span class="sxs-lookup"><span data-stu-id="b1383-103">Delete a Service Fabric cluster on Azure and the resources it uses</span></span>
<span data-ttu-id="b1383-104">Кластер Service Fabric состоит из многих других ресурсов Azure помимо собственно ресурса кластера.</span><span class="sxs-lookup"><span data-stu-id="b1383-104">A Service Fabric cluster is made up of many other Azure resources in addition to the cluster resource itself.</span></span> <span data-ttu-id="b1383-105">Чтобы полностью удалить кластер Service Fabric, необходимо также удалить все ресурсы, из которых он состоит.</span><span class="sxs-lookup"><span data-stu-id="b1383-105">So to completely delete a Service Fabric cluster you also need to delete all the resources it is made of.</span></span>
<span data-ttu-id="b1383-106">Вы можете сделать это одним из двух способов: удалить группу ресурсов, в которой находится кластер (при этом будет удален ресурс кластера и другие ресурсы в группе ресурсов), или удалить ресурс кластера и связанные с ним ресурсы по отдельности (но не другие ресурсы в группе ресурсов).</span><span class="sxs-lookup"><span data-stu-id="b1383-106">You have two options: Either delete the resource group that the cluster is in (which deletes the cluster resource and any other resources in the resource group) or specifically delete the cluster resource and it's associated resources (but not other resources in the resource group).</span></span>

> [!NOTE]
> <span data-ttu-id="b1383-107">Удаление ресурса кластера **не** приводит к удалению всех прочих ресурсов, из которых состоит кластер Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b1383-107">Deleting the cluster resource **does not** delete all the other resources that your Service Fabric cluster is composed of.</span></span>
> 
> 

## <a name="delete-the-entire-resource-group-rg-that-the-service-fabric-cluster-is-in"></a><span data-ttu-id="b1383-108">Удаление всей группы ресурсов, в которой находится кластер Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b1383-108">Delete the entire resource group (RG) that the Service Fabric cluster is in</span></span>
<span data-ttu-id="b1383-109">Это самый простой способ, который гарантирует удаление всех ресурсов, связанных с кластером, включая группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b1383-109">This is the easiest way to ensure that you delete all the resources associated with your cluster, including the resource group.</span></span> <span data-ttu-id="b1383-110">Группу ресурсов можно удалить с помощью PowerShell или через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b1383-110">You can delete the resource group using PowerShell or through the Azure portal.</span></span> <span data-ttu-id="b1383-111">Если выбранная группа ресурсов содержит ресурсы, которые не относятся к кластеру Service Fabric, можно удалить отдельные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="b1383-111">If your resource group has resources that are not related to Service fabric cluster, then you can delete specific resources.</span></span>

### <a name="delete-the-resource-group-using-azure-powershell"></a><span data-ttu-id="b1383-112">Удаление группы ресурсов с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b1383-112">Delete the resource group using Azure PowerShell</span></span>
<span data-ttu-id="b1383-113">Группу ресурсов также можно удалить, выполнив следующие командлеты Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b1383-113">You can also delete the resource group by running the following Azure PowerShell cmdlets.</span></span> <span data-ttu-id="b1383-114">Убедитесь, что на компьютере установлена среда Azure PowerShell 1.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="b1383-114">Make sure Azure PowerShell 1.0 or greater is installed on your computer.</span></span> <span data-ttu-id="b1383-115">Если вы не сделали этого ранее, выполните инструкции в статье [Как установить и настроить Azure PowerShell](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="b1383-115">If you have not done this before, follow the steps outlined in [How to install and Configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="b1383-116">Откройте PowerShell и выполните следующие командлеты PowerShell:</span><span class="sxs-lookup"><span data-stu-id="b1383-116">Open a PowerShell window and run the following PS cmdlets:</span></span>

```powershell
Login-AzureRmAccount

Remove-AzureRmResourceGroup -Name <name of ResouceGroup> -Force
```

<span data-ttu-id="b1383-117">Будет выведен запрос на подтверждение удаления, если вы не использовали параметр *-Force* .</span><span class="sxs-lookup"><span data-stu-id="b1383-117">You will get a prompt to confirm the deletion if you did not use the *-Force* option.</span></span> <span data-ttu-id="b1383-118">После подтверждения группа ресурсов и все содержащиеся в ней ресурсы будут удалены.</span><span class="sxs-lookup"><span data-stu-id="b1383-118">On confirmation the RG and all the resources it contains are deleted.</span></span>

### <a name="delete-a-resource-group-in-the-azure-portal"></a><span data-ttu-id="b1383-119">Удаление группы ресурсов на портале Azure</span><span class="sxs-lookup"><span data-stu-id="b1383-119">Delete a resource group in the Azure portal</span></span>
1. <span data-ttu-id="b1383-120">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b1383-120">Login to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b1383-121">Перейдите к нужному кластеру Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b1383-121">Navigate to the Service Fabric cluster you want to delete.</span></span>
3. <span data-ttu-id="b1383-122">Щелкните имя группы ресурсов на странице "Основные компоненты" кластера.</span><span class="sxs-lookup"><span data-stu-id="b1383-122">Click on the Resource Group name on the cluster essentials page.</span></span>
4. <span data-ttu-id="b1383-123">Откроется страница **Resource Group Essentials** (Основные компоненты группы ресурсов).</span><span class="sxs-lookup"><span data-stu-id="b1383-123">This brings up the **Resource Group Essentials** page.</span></span>
5. <span data-ttu-id="b1383-124">Нажмите кнопку **Delete**(Удалить).</span><span class="sxs-lookup"><span data-stu-id="b1383-124">Click **Delete**.</span></span>
6. <span data-ttu-id="b1383-125">Следуйте инструкциям на этой странице, чтобы завершить удаление группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b1383-125">Follow the instructions on that page to complete the deletion of the resource group.</span></span>

![Удаление группы ресурсов][ResourceGroupDelete]

## <a name="delete-the-cluster-resource-and-the-resources-it-uses-but-not-other-resources-in-the-resource-group"></a><span data-ttu-id="b1383-127">Удаление ресурса кластера и используемых им ресурсов, но не других ресурсов в группе ресурсов</span><span class="sxs-lookup"><span data-stu-id="b1383-127">Delete the cluster resource and the resources it uses, but not other resources in the resource group</span></span>
<span data-ttu-id="b1383-128">Если в группе ресурсов содержатся только ресурсы, связанные с кластером Service Fabric, который требуется удалить, проще всего будет удалить группу ресурсов целиком.</span><span class="sxs-lookup"><span data-stu-id="b1383-128">If your resource group has only resources that are related to the Service Fabric cluster you want to delete, then it is easier to delete the entire resource group.</span></span> <span data-ttu-id="b1383-129">Если требуется выборочно удалить ресурсы в группе ресурсов, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="b1383-129">If you want to selectively delete the resources one-by-one in your resource group, then follow these steps.</span></span>

<span data-ttu-id="b1383-130">Если кластер развернут с помощью портала или с помощью одного из шаблонов Resource Manager для Service Fabric из коллекции шаблонов, то все ресурсы, используемые кластером, помечены следующими двумя тегами.</span><span class="sxs-lookup"><span data-stu-id="b1383-130">If you deployed your cluster using the portal or using one of the Service Fabric Resource Manager templates from the template gallery, then all the resources that the cluster uses are tagged with the following two tags.</span></span> <span data-ttu-id="b1383-131">С их помощью можно определить, какие ресурсы требуется удалить.</span><span class="sxs-lookup"><span data-stu-id="b1383-131">You can use them to decide which resources you want to delete.</span></span>

<span data-ttu-id="b1383-132">***Тег 1:*** ключ = clusterName, значение = "имя кластера".</span><span class="sxs-lookup"><span data-stu-id="b1383-132">***Tag#1:*** Key = clusterName, Value = 'name of the cluster'</span></span>

<span data-ttu-id="b1383-133">***Тег 2:*** ключ = resourceName, значение = ServiceFabric.</span><span class="sxs-lookup"><span data-stu-id="b1383-133">***Tag#2:*** Key = resourceName, Value = ServiceFabric</span></span>

### <a name="delete-specific-resources-in-the-azure-portal"></a><span data-ttu-id="b1383-134">Удаление отдельных ресурсов на портале Azure</span><span class="sxs-lookup"><span data-stu-id="b1383-134">Delete specific resources in the Azure portal</span></span>
1. <span data-ttu-id="b1383-135">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b1383-135">Login to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b1383-136">Перейдите к нужному кластеру Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b1383-136">Navigate to the Service Fabric cluster you want to delete.</span></span>
3. <span data-ttu-id="b1383-137">В колонке "Основные компоненты" перейдите к элементу **Все параметры** .</span><span class="sxs-lookup"><span data-stu-id="b1383-137">Go to **All settings** on the essentials blade.</span></span>
4. <span data-ttu-id="b1383-138">В разделе **Управление ресурсами** колонки параметров щелкните **Теги**.</span><span class="sxs-lookup"><span data-stu-id="b1383-138">Click on **Tags** under **Resource Management** in the settings blade.</span></span>
5. <span data-ttu-id="b1383-139">Щелкните один из **тегов** в колонке тегов, чтобы получить список всех ресурсов с этим тегом.</span><span class="sxs-lookup"><span data-stu-id="b1383-139">Click on one of the **Tags** in the tags blade to get a list of all the resources with that tag.</span></span>
   
    ![Теги ресурсов][ResourceTags]
6. <span data-ttu-id="b1383-141">Получив список ресурсов с тегом, вы можете выбрать и удалить нужные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="b1383-141">Once you have the list of tagged resources, click on each of the resources and delete them.</span></span>
   
    ![Ресурсы с тегами][TaggedResources]

### <a name="delete-the-resources-using-azure-powershell"></a><span data-ttu-id="b1383-143">Удаление ресурсов с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b1383-143">Delete the resources using Azure PowerShell</span></span>
<span data-ttu-id="b1383-144">Отдельные ресурсы также можно удалить, выполнив следующие командлеты Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b1383-144">You can delete the resources one-by-one by running the following Azure PowerShell cmdlets.</span></span> <span data-ttu-id="b1383-145">Убедитесь, что на компьютере установлена среда Azure PowerShell 1.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="b1383-145">Make sure Azure PowerShell 1.0 or greater is installed on your computer.</span></span> <span data-ttu-id="b1383-146">Если вы не сделали этого ранее, выполните инструкции в статье [Как установить и настроить Azure PowerShell](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="b1383-146">If you have not done this before, follow the steps outlined in [How to install and Configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="b1383-147">Откройте PowerShell и выполните следующие командлеты PowerShell:</span><span class="sxs-lookup"><span data-stu-id="b1383-147">Open a PowerShell window and run the following PS cmdlets:</span></span>

```powershell
Login-AzureRmAccount
```
<span data-ttu-id="b1383-148">Для каждого ресурса, который требуется удалить, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b1383-148">For each of the resources you want to delete, run the following:</span></span>

```powershell
Remove-AzureRmResource -ResourceName "<name of the Resource>" -ResourceType "<Resource Type>" -ResourceGroupName "<name of the resource group>" -Force
```

<span data-ttu-id="b1383-149">Чтобы удалить ресурс кластера, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b1383-149">To delete the cluster resource, run the following:</span></span>

```powershell
Remove-AzureRmResource -ResourceName "<name of the Resource>" -ResourceType "Microsoft.ServiceFabric/clusters" -ResourceGroupName "<name of the resource group>" -Force
```

## <a name="next-steps"></a><span data-ttu-id="b1383-150">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b1383-150">Next steps</span></span>
<span data-ttu-id="b1383-151">Дополнительные сведения об обновлении кластера и секционировании служб см. в следующих статьях.</span><span class="sxs-lookup"><span data-stu-id="b1383-151">Read the following to also learn about upgrading a cluster and partitioning services:</span></span>

* [<span data-ttu-id="b1383-152">Узнайте об обновлениях кластера.</span><span class="sxs-lookup"><span data-stu-id="b1383-152">Learn about cluster upgrades</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="b1383-153">Узнайте о секционировании служб с отслеживанием для максимального масштабирования.</span><span class="sxs-lookup"><span data-stu-id="b1383-153">Learn about partitioning stateful services for maximum scale</span></span>](service-fabric-concepts-partitioning.md)

<!--Image references-->
[ResourceGroupDelete]: ./media/service-fabric-cluster-delete/ResourceGroupDelete.PNG

[ResourceTags]: ./media/service-fabric-cluster-delete/ResourceTags.png

[TaggedResources]: ./media/service-fabric-cluster-delete/TaggedResources.PNG
