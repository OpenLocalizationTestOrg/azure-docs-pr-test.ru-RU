---
title: "Справочник по командлетам PowerShell планировщика"
description: "Справочник по командлетам PowerShell планировщика"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 9a26c457-d7a1-4e4a-bc79-f26592155218
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 141919ab4506b3de4c4a69670dcf54c60ee6409c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="scheduler-powershell-cmdlets-reference"></a><span data-ttu-id="9bc86-103">Справочник по командлетам PowerShell планировщика</span><span class="sxs-lookup"><span data-stu-id="9bc86-103">Scheduler PowerShell Cmdlets Reference</span></span>
<span data-ttu-id="9bc86-104">В следующей таблице приведено описание и ссылки на справочную страницу для каждого из основных командлетов в планировщике Azure.</span><span class="sxs-lookup"><span data-stu-id="9bc86-104">The following table describes and links to the reference page of each of the major cmdlets in Azure Scheduler.</span></span>

<span data-ttu-id="9bc86-105">Чтобы установить решение Azure PowerShell и связать его с подпиской Azure, см. статью [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9bc86-105">To install Azure PowerShell and associate it with your Azure subscription, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> 

<span data-ttu-id="9bc86-106">Дополнительные сведения о [командлетах Azure Resource Manager](/powershell/azure/overview) см. в статье [Использование Azure PowerShell с Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="9bc86-106">For more information about [Azure Resource Manager cmdlets](/powershell/azure/overview), see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

| <span data-ttu-id="9bc86-107">Командлет</span><span class="sxs-lookup"><span data-stu-id="9bc86-107">Cmdlet</span></span> | <span data-ttu-id="9bc86-108">Описание командлета</span><span class="sxs-lookup"><span data-stu-id="9bc86-108">Cmdlet Description</span></span> |
| --- | --- |
| [<span data-ttu-id="9bc86-109">Disable-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="9bc86-109">Disable-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/disable-azurermschedulerjobcollection) |<span data-ttu-id="9bc86-110">Отключает коллекцию заданий.</span><span class="sxs-lookup"><span data-stu-id="9bc86-110">Disables a job collection.</span></span> |
| [<span data-ttu-id="9bc86-111">Enable-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="9bc86-111">Enable-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/enable-azurermschedulerjobcollection) |<span data-ttu-id="9bc86-112">Включает коллекцию заданий.</span><span class="sxs-lookup"><span data-stu-id="9bc86-112">Enables a job collection.</span></span> |
| [<span data-ttu-id="9bc86-113">Get-AzureRmSchedulerJob</span><span class="sxs-lookup"><span data-stu-id="9bc86-113">Get-AzureRmSchedulerJob</span></span>](/powershell/module/azurerm.scheduler/get-azurermschedulerjob) |<span data-ttu-id="9bc86-114">Получает задания планировщика.</span><span class="sxs-lookup"><span data-stu-id="9bc86-114">Gets Scheduler jobs.</span></span> |
| [<span data-ttu-id="9bc86-115">Get-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="9bc86-115">Get-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/get-azurermschedulerjobcollection) |<span data-ttu-id="9bc86-116">Получает коллекции заданий.</span><span class="sxs-lookup"><span data-stu-id="9bc86-116">Gets job collections.</span></span> |
| [<span data-ttu-id="9bc86-117">Get-AzureRmSchedulerJobHistory</span><span class="sxs-lookup"><span data-stu-id="9bc86-117">Get-AzureRmSchedulerJobHistory</span></span>](/powershell/module/azurerm.scheduler/get-azurermschedulerjobhistory) |<span data-ttu-id="9bc86-118">Получает журнал заданий.</span><span class="sxs-lookup"><span data-stu-id="9bc86-118">Gets job history.</span></span> |
| [<span data-ttu-id="9bc86-119">New-AzureRmSchedulerHttpJob</span><span class="sxs-lookup"><span data-stu-id="9bc86-119">New-AzureRmSchedulerHttpJob</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerhttpjob) |<span data-ttu-id="9bc86-120">Создает задание HTTP.</span><span class="sxs-lookup"><span data-stu-id="9bc86-120">Creates an HTTP job.</span></span> |
| [<span data-ttu-id="9bc86-121">New-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="9bc86-121">New-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerjobcollection) |<span data-ttu-id="9bc86-122">Создает коллекцию заданий.</span><span class="sxs-lookup"><span data-stu-id="9bc86-122">Creates a job collection.</span></span> |
| [<span data-ttu-id="9bc86-123">New-AzureRmSchedulerServiceBusQueueJob</span><span class="sxs-lookup"><span data-stu-id="9bc86-123">New-AzureRmSchedulerServiceBusQueueJob</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerservicebusqueuejob) |<span data-ttu-id="9bc86-124">Создает задание очереди служебной шины.</span><span class="sxs-lookup"><span data-stu-id="9bc86-124">Creates a service bus queue job.</span></span> |
| [<span data-ttu-id="9bc86-125">New-AzureRmSchedulerServiceBusTopicJob</span><span class="sxs-lookup"><span data-stu-id="9bc86-125">New-AzureRmSchedulerServiceBusTopicJob</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerservicebustopicjob) |<span data-ttu-id="9bc86-126">Создает задание раздела служебной шины.</span><span class="sxs-lookup"><span data-stu-id="9bc86-126">Creates a service bus topic job.</span></span> |
| [<span data-ttu-id="9bc86-127">New-AzureRmSchedulerStorageQueueJob</span><span class="sxs-lookup"><span data-stu-id="9bc86-127">New-AzureRmSchedulerStorageQueueJob</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerstoragequeuejob) |<span data-ttu-id="9bc86-128">Создает задание очереди хранилища.</span><span class="sxs-lookup"><span data-stu-id="9bc86-128">Creates a storage queue job.</span></span> |
| [<span data-ttu-id="9bc86-129">Remove-AzureRmSchedulerJob</span><span class="sxs-lookup"><span data-stu-id="9bc86-129">Remove-AzureRmSchedulerJob</span></span>](/powershell/module/azurerm.scheduler/remove-azurermschedulerjob) |<span data-ttu-id="9bc86-130">Удаляет задание планировщика.</span><span class="sxs-lookup"><span data-stu-id="9bc86-130">Removes a Scheduler job.</span></span> |
| [<span data-ttu-id="9bc86-131">Remove-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="9bc86-131">Remove-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/remove-azurermschedulerjobcollection) |<span data-ttu-id="9bc86-132">Удаляет коллекцию заданий.</span><span class="sxs-lookup"><span data-stu-id="9bc86-132">Removes a job collection.</span></span> |
| [<span data-ttu-id="9bc86-133">Set-AzureRmSchedulerHttpJob</span><span class="sxs-lookup"><span data-stu-id="9bc86-133">Set-AzureRmSchedulerHttpJob</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerhttpjob) |<span data-ttu-id="9bc86-134">Изменяет задание HTTP планировщика.</span><span class="sxs-lookup"><span data-stu-id="9bc86-134">Modifies a Scheduler HTTP job.</span></span> |
| [<span data-ttu-id="9bc86-135">Set-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="9bc86-135">Set-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerjobcollection) |<span data-ttu-id="9bc86-136">Изменяет коллекцию заданий.</span><span class="sxs-lookup"><span data-stu-id="9bc86-136">Modifies a job collection.</span></span> |
| [<span data-ttu-id="9bc86-137">Set-AzureRmSchedulerServiceBusQueueJob</span><span class="sxs-lookup"><span data-stu-id="9bc86-137">Set-AzureRmSchedulerServiceBusQueueJob</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerservicebusqueuejob) |<span data-ttu-id="9bc86-138">Изменяет задание очереди служебной шины.</span><span class="sxs-lookup"><span data-stu-id="9bc86-138">Modifies a service bus queue job.</span></span> |
| [<span data-ttu-id="9bc86-139">Set-AzureRmSchedulerServiceBusTopicJob</span><span class="sxs-lookup"><span data-stu-id="9bc86-139">Set-AzureRmSchedulerServiceBusTopicJob</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerservicebustopicjob) |<span data-ttu-id="9bc86-140">Изменяет задание раздела служебной шины.</span><span class="sxs-lookup"><span data-stu-id="9bc86-140">Modifies a service bus topic job.</span></span> |
| [<span data-ttu-id="9bc86-141">Set-AzureRmSchedulerStorageQueueJob</span><span class="sxs-lookup"><span data-stu-id="9bc86-141">Set-AzureRmSchedulerStorageQueueJob</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerstoragequeuejob) |<span data-ttu-id="9bc86-142">Изменяет задание очереди хранилища.</span><span class="sxs-lookup"><span data-stu-id="9bc86-142">Modifies a storage queue job.</span></span> |

<span data-ttu-id="9bc86-143">Для получения более подробных сведений можно выполнить следующие командлеты:</span><span class="sxs-lookup"><span data-stu-id="9bc86-143">For more detailed information, you can run any of the following cmdlets:</span></span> 

```
Get-Help <cmdlet name> -Detailed
```
```
Get-Help <cmdlet name> -Examples
```
```
Get-Help <cmdlet name> -Full
```

## <a name="see-also"></a><span data-ttu-id="9bc86-144">См. также</span><span class="sxs-lookup"><span data-stu-id="9bc86-144">See Also</span></span>
 [<span data-ttu-id="9bc86-145">Что такое планировщик?</span><span class="sxs-lookup"><span data-stu-id="9bc86-145">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="9bc86-146">Основные понятия, терминология и иерархия сущностей планировщика Azure</span><span class="sxs-lookup"><span data-stu-id="9bc86-146">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="9bc86-147">Приступая к работе с планировщиком Azure на портале Azure</span><span class="sxs-lookup"><span data-stu-id="9bc86-147">Get started using Scheduler in the Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="9bc86-148">Планы и выставление счетов в планировщике Azure</span><span class="sxs-lookup"><span data-stu-id="9bc86-148">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="9bc86-149">Справочник по API REST планировщика Azure</span><span class="sxs-lookup"><span data-stu-id="9bc86-149">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="9bc86-150">Высокая доступность и надежность планировщика Azure</span><span class="sxs-lookup"><span data-stu-id="9bc86-150">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="9bc86-151">Ограничения, значения по умолчанию и коды ошибок планировщика Azure</span><span class="sxs-lookup"><span data-stu-id="9bc86-151">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="9bc86-152">Исходящая аутентификация планировщика Azure</span><span class="sxs-lookup"><span data-stu-id="9bc86-152">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

