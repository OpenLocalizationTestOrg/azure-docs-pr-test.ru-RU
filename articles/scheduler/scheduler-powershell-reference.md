---
title: "aaaScheduler Справочник по командлетам PowerShell"
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
ms.openlocfilehash: a2b23bcd3e4493ffba1dbf21fbb87818be7c01e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-powershell-cmdlets-reference"></a><span data-ttu-id="de663-103">Справочник по командлетам PowerShell планировщика</span><span class="sxs-lookup"><span data-stu-id="de663-103">Scheduler PowerShell Cmdlets Reference</span></span>
<span data-ttu-id="de663-104">Hello в следующей таблице описаны и ссылки на справочной странице toohello каждого из основных командлетов hello в планировщике Azure.</span><span class="sxs-lookup"><span data-stu-id="de663-104">hello following table describes and links toohello reference page of each of hello major cmdlets in Azure Scheduler.</span></span>

<span data-ttu-id="de663-105">tooinstall Azure PowerShell и связать ее с подпиской Azure см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="de663-105">tooinstall Azure PowerShell and associate it with your Azure subscription, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> 

<span data-ttu-id="de663-106">Дополнительные сведения о [командлетах Azure Resource Manager](/powershell/azure/overview) см. в статье [Использование Azure PowerShell с Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="de663-106">For more information about [Azure Resource Manager cmdlets](/powershell/azure/overview), see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

| <span data-ttu-id="de663-107">Командлет</span><span class="sxs-lookup"><span data-stu-id="de663-107">Cmdlet</span></span> | <span data-ttu-id="de663-108">Описание командлета</span><span class="sxs-lookup"><span data-stu-id="de663-108">Cmdlet Description</span></span> |
| --- | --- |
| [<span data-ttu-id="de663-109">Disable-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="de663-109">Disable-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/disable-azurermschedulerjobcollection) |<span data-ttu-id="de663-110">Отключает коллекцию заданий.</span><span class="sxs-lookup"><span data-stu-id="de663-110">Disables a job collection.</span></span> |
| [<span data-ttu-id="de663-111">Enable-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="de663-111">Enable-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/enable-azurermschedulerjobcollection) |<span data-ttu-id="de663-112">Включает коллекцию заданий.</span><span class="sxs-lookup"><span data-stu-id="de663-112">Enables a job collection.</span></span> |
| [<span data-ttu-id="de663-113">Get-AzureRmSchedulerJob</span><span class="sxs-lookup"><span data-stu-id="de663-113">Get-AzureRmSchedulerJob</span></span>](/powershell/module/azurerm.scheduler/get-azurermschedulerjob) |<span data-ttu-id="de663-114">Получает задания планировщика.</span><span class="sxs-lookup"><span data-stu-id="de663-114">Gets Scheduler jobs.</span></span> |
| [<span data-ttu-id="de663-115">Get-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="de663-115">Get-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/get-azurermschedulerjobcollection) |<span data-ttu-id="de663-116">Получает коллекции заданий.</span><span class="sxs-lookup"><span data-stu-id="de663-116">Gets job collections.</span></span> |
| [<span data-ttu-id="de663-117">Get-AzureRmSchedulerJobHistory</span><span class="sxs-lookup"><span data-stu-id="de663-117">Get-AzureRmSchedulerJobHistory</span></span>](/powershell/module/azurerm.scheduler/get-azurermschedulerjobhistory) |<span data-ttu-id="de663-118">Получает журнал заданий.</span><span class="sxs-lookup"><span data-stu-id="de663-118">Gets job history.</span></span> |
| [<span data-ttu-id="de663-119">New-AzureRmSchedulerHttpJob</span><span class="sxs-lookup"><span data-stu-id="de663-119">New-AzureRmSchedulerHttpJob</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerhttpjob) |<span data-ttu-id="de663-120">Создает задание HTTP.</span><span class="sxs-lookup"><span data-stu-id="de663-120">Creates an HTTP job.</span></span> |
| [<span data-ttu-id="de663-121">New-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="de663-121">New-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerjobcollection) |<span data-ttu-id="de663-122">Создает коллекцию заданий.</span><span class="sxs-lookup"><span data-stu-id="de663-122">Creates a job collection.</span></span> |
| [<span data-ttu-id="de663-123">New-AzureRmSchedulerServiceBusQueueJob</span><span class="sxs-lookup"><span data-stu-id="de663-123">New-AzureRmSchedulerServiceBusQueueJob</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerservicebusqueuejob) |<span data-ttu-id="de663-124">Создает задание очереди служебной шины.</span><span class="sxs-lookup"><span data-stu-id="de663-124">Creates a service bus queue job.</span></span> |
| [<span data-ttu-id="de663-125">New-AzureRmSchedulerServiceBusTopicJob</span><span class="sxs-lookup"><span data-stu-id="de663-125">New-AzureRmSchedulerServiceBusTopicJob</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerservicebustopicjob) |<span data-ttu-id="de663-126">Создает задание раздела служебной шины.</span><span class="sxs-lookup"><span data-stu-id="de663-126">Creates a service bus topic job.</span></span> |
| [<span data-ttu-id="de663-127">New-AzureRmSchedulerStorageQueueJob</span><span class="sxs-lookup"><span data-stu-id="de663-127">New-AzureRmSchedulerStorageQueueJob</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerstoragequeuejob) |<span data-ttu-id="de663-128">Создает задание очереди хранилища.</span><span class="sxs-lookup"><span data-stu-id="de663-128">Creates a storage queue job.</span></span> |
| [<span data-ttu-id="de663-129">Remove-AzureRmSchedulerJob</span><span class="sxs-lookup"><span data-stu-id="de663-129">Remove-AzureRmSchedulerJob</span></span>](/powershell/module/azurerm.scheduler/remove-azurermschedulerjob) |<span data-ttu-id="de663-130">Удаляет задание планировщика.</span><span class="sxs-lookup"><span data-stu-id="de663-130">Removes a Scheduler job.</span></span> |
| [<span data-ttu-id="de663-131">Remove-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="de663-131">Remove-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/remove-azurermschedulerjobcollection) |<span data-ttu-id="de663-132">Удаляет коллекцию заданий.</span><span class="sxs-lookup"><span data-stu-id="de663-132">Removes a job collection.</span></span> |
| [<span data-ttu-id="de663-133">Set-AzureRmSchedulerHttpJob</span><span class="sxs-lookup"><span data-stu-id="de663-133">Set-AzureRmSchedulerHttpJob</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerhttpjob) |<span data-ttu-id="de663-134">Изменяет задание HTTP планировщика.</span><span class="sxs-lookup"><span data-stu-id="de663-134">Modifies a Scheduler HTTP job.</span></span> |
| [<span data-ttu-id="de663-135">Set-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="de663-135">Set-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerjobcollection) |<span data-ttu-id="de663-136">Изменяет коллекцию заданий.</span><span class="sxs-lookup"><span data-stu-id="de663-136">Modifies a job collection.</span></span> |
| [<span data-ttu-id="de663-137">Set-AzureRmSchedulerServiceBusQueueJob</span><span class="sxs-lookup"><span data-stu-id="de663-137">Set-AzureRmSchedulerServiceBusQueueJob</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerservicebusqueuejob) |<span data-ttu-id="de663-138">Изменяет задание очереди служебной шины.</span><span class="sxs-lookup"><span data-stu-id="de663-138">Modifies a service bus queue job.</span></span> |
| [<span data-ttu-id="de663-139">Set-AzureRmSchedulerServiceBusTopicJob</span><span class="sxs-lookup"><span data-stu-id="de663-139">Set-AzureRmSchedulerServiceBusTopicJob</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerservicebustopicjob) |<span data-ttu-id="de663-140">Изменяет задание раздела служебной шины.</span><span class="sxs-lookup"><span data-stu-id="de663-140">Modifies a service bus topic job.</span></span> |
| [<span data-ttu-id="de663-141">Set-AzureRmSchedulerStorageQueueJob</span><span class="sxs-lookup"><span data-stu-id="de663-141">Set-AzureRmSchedulerStorageQueueJob</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerstoragequeuejob) |<span data-ttu-id="de663-142">Изменяет задание очереди хранилища.</span><span class="sxs-lookup"><span data-stu-id="de663-142">Modifies a storage queue job.</span></span> |

<span data-ttu-id="de663-143">Для получения дополнительных сведений запустите любой hello следующие командлеты:</span><span class="sxs-lookup"><span data-stu-id="de663-143">For more detailed information, you can run any of hello following cmdlets:</span></span> 

```
Get-Help <cmdlet name> -Detailed
```
```
Get-Help <cmdlet name> -Examples
```
```
Get-Help <cmdlet name> -Full
```

## <a name="see-also"></a><span data-ttu-id="de663-144">См. также</span><span class="sxs-lookup"><span data-stu-id="de663-144">See Also</span></span>
 [<span data-ttu-id="de663-145">Что такое планировщик?</span><span class="sxs-lookup"><span data-stu-id="de663-145">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="de663-146">Основные понятия, терминология и иерархия сущностей планировщика Azure</span><span class="sxs-lookup"><span data-stu-id="de663-146">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="de663-147">Начало работы с планировщиком в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="de663-147">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="de663-148">Планы и выставление счетов в планировщике Azure</span><span class="sxs-lookup"><span data-stu-id="de663-148">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="de663-149">Справочник по API REST планировщика Azure</span><span class="sxs-lookup"><span data-stu-id="de663-149">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="de663-150">Высокая доступность и надежность планировщика Azure</span><span class="sxs-lookup"><span data-stu-id="de663-150">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="de663-151">Ограничения, значения по умолчанию и коды ошибок планировщика Azure</span><span class="sxs-lookup"><span data-stu-id="de663-151">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="de663-152">Исходящая аутентификация планировщика Azure</span><span class="sxs-lookup"><span data-stu-id="de663-152">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

