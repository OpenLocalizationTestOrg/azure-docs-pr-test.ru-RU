---
title: "Перенос учетной записи и ресурсов службы автоматизации | Документация Майкрософт"
description: "В этой статье описывается, как переместить учетную запись в службе автоматизации Azure и связанные с ней ресурсы из одной подписки в другую."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9c2db4a2-f324-48dc-8ce7-3343bf7230d5
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/21/2016
ms.author: magoedte
ms.openlocfilehash: 687da15bdaf854254321b59350f47549781676f5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-automation-account-and-resources"></a><span data-ttu-id="7f133-103">Перенос учетной записи и ресурсов службы автоматизации</span><span class="sxs-lookup"><span data-stu-id="7f133-103">Migrate Automation Account and resources</span></span>
<span data-ttu-id="7f133-104">Созданные на портале Azure учетные записи службы автоматизации и связанные с ней ресурсы (активы, модули Runbook, модули, и т. д.), можно перенести из одной группы ресурсов или подписки в другую с помощью функции [Перемещение ресурсов](../azure-resource-manager/resource-group-move-resources.md), доступной на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="7f133-104">For Automation accounts and its associated resources (i.e. assets, runbooks, modules, etc.) that you have created in the Azure portal and want to migrate from one resource group to another or from one subscription to another, you can accomplish this easily with the [move resources](../azure-resource-manager/resource-group-move-resources.md) feature available in the Azure portal.</span></span> <span data-ttu-id="7f133-105">Тем не менее перед выполнением этого действия необходимо свериться со следующим [контрольным списком перед перемещением ресурсов](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources), а также приведенным ниже списком, относящимся к службе автоматизации.</span><span class="sxs-lookup"><span data-stu-id="7f133-105">However, before proceeding with this action, you should first review the following [checklist before moving resources](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) and additionally, the list below specific to Automation.</span></span>   

1. <span data-ttu-id="7f133-106">Целевая подписка или группа ресурсов должна находиться в том же регионе, что и ресурс.</span><span class="sxs-lookup"><span data-stu-id="7f133-106">The destination subscription/resource group must be in same region as the source.</span></span>  <span data-ttu-id="7f133-107">Это означает, что учетные записи службы автоматизации нельзя перемещать между регионами.</span><span class="sxs-lookup"><span data-stu-id="7f133-107">Meaning, Automation accounts cannot be moved across regions.</span></span>
2. <span data-ttu-id="7f133-108">При перемещении ресурсов (например, модулей Runbook, заданий и т. д.) исходная и целевая группы блокируются на время этой операции.</span><span class="sxs-lookup"><span data-stu-id="7f133-108">When moving resources (e.g. runbooks, jobs, etc.), both the source group and the target group are locked for the duration of the operation.</span></span> <span data-ttu-id="7f133-109">Операции записи и удаления для групп блокируются до завершения перемещения.</span><span class="sxs-lookup"><span data-stu-id="7f133-109">Write and delete operations are blocked on the groups until the move completes.</span></span>  
3. <span data-ttu-id="7f133-110">Любые модули Runbook или переменные, ссылающиеся на идентификатор ресурса или подписки из существующей подписки, после завершения переноса потребуется обновить.</span><span class="sxs-lookup"><span data-stu-id="7f133-110">Any runbooks or variables which reference a resource or subscription ID from the existing subscription will need to be updated after migration is completed.</span></span>   

> [!NOTE]
> <span data-ttu-id="7f133-111">Данная функция не поддерживает перемещение классических ресурсов службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="7f133-111">This feature does not support moving Classic automation resources.</span></span>
>
>

## <a name="to-move-the-automation-account-using-the-portal"></a><span data-ttu-id="7f133-112">Перемещение учетной записи службы автоматизации с помощью портала</span><span class="sxs-lookup"><span data-stu-id="7f133-112">To move the Automation Account using the portal</span></span>
1. <span data-ttu-id="7f133-113">Из учетной записи службы автоматизации щелкните **Переместить** в верхней части колонки.</span><span class="sxs-lookup"><span data-stu-id="7f133-113">From your Automation account, click **Move** at the top of the blade.</span></span><br> <span data-ttu-id="7f133-114">![Параметр "Переместить"](media/automation-migrate-account-subscription/automation-menu-move.png)</span><span class="sxs-lookup"><span data-stu-id="7f133-114">![Move option](media/automation-migrate-account-subscription/automation-menu-move.png)</span></span><br>
2. <span data-ttu-id="7f133-115">Обратите внимание, что в колонке **Перемещение ресурсов** представлены ресурсы, относящиеся к учетной записи службы автоматизации и группам ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7f133-115">On the **Move resources** blade, note that it presents resources related to both your Automation account and your resource group(s).</span></span>  <span data-ttu-id="7f133-116">В раскрывающихся списках выберите **подписку** и **группу ресурсов** или выберите параметр **Создать группу ресурсов** и введите имя новой группы ресурсов в соответствующем поле.</span><span class="sxs-lookup"><span data-stu-id="7f133-116">Select the **subscription** and **resource group** from the drop-down lists, or select the option **create a new resource group** and enter a new resource group name in the field provided.</span></span>  
3. <span data-ttu-id="7f133-117">Просмотрите уведомление и установите флажок *understand tools and scripts will need to be updated to use new resource IDs after resources have been moved* (Я понимаю, что инструменты и сценарии потребуется обновить, чтобы использовать новые идентификаторы ресурсов после их перемещения) для подтверждения этого. Затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="7f133-117">Review and select the checkbox to acknowledge you *understand tools and scripts will need to be updated to use new resource IDs after resources have been moved* and then click **OK**.</span></span><br> <span data-ttu-id="7f133-118">![Колонка "Перемещение ресурсов"](media/automation-migrate-account-subscription/automation-move-resources-blade.png)</span><span class="sxs-lookup"><span data-stu-id="7f133-118">![Move Resources Blade](media/automation-migrate-account-subscription/automation-move-resources-blade.png)</span></span><br>   

<span data-ttu-id="7f133-119">Выполнение этого действия может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="7f133-119">This action will take several minutes to complete.</span></span>  <span data-ttu-id="7f133-120">В разделе **Уведомления** будет показано состояние каждого выполняемого действия — проверки, переноса и т. д., после чего отобразится сообщение о завершении операции.</span><span class="sxs-lookup"><span data-stu-id="7f133-120">In **Notifications**, you will be presented with a status of each action that takes place - validation, migration, and then finally when it is completed.</span></span>     

## <a name="to-move-the-automation-account-using-powershell"></a><span data-ttu-id="7f133-121">Перемещение учетной записи службы автоматизации с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="7f133-121">To move the Automation Account using PowerShell</span></span>
<span data-ttu-id="7f133-122">Чтобы переместить существующие ресурсы службы автоматизации в другую группу ресурсов или подписку, используйте командлет **Get-AzureRmResource** для получения определенной учетной записи службы автоматизации, а затем командлет **Move-AzureRmResource** для выполнения переноса.</span><span class="sxs-lookup"><span data-stu-id="7f133-122">To move existing Automation resources to another resource group or subscription, use the  **Get-AzureRmResource** cmdlet to get the specific Automation account and then **Move-AzureRmResource** cmdlet to perform the move.</span></span>

<span data-ttu-id="7f133-123">В первом примере показано, как переместить один учетную запись службы автоматизации в новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7f133-123">The first example shows how to move an Automation account to a new resource group.</span></span>

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup"
   ```

<span data-ttu-id="7f133-124">После выполнения приведенного выше примера кода будет предложено подтвердить, что вы хотите выполнить это действие.</span><span class="sxs-lookup"><span data-stu-id="7f133-124">After you execute the above code example, you will be prompted to verify you want to perform this action.</span></span>  <span data-ttu-id="7f133-125">После нажатия кнопки **Yes** (Да) выполнение сценария будет продолжено и вы не будете получать какие-либо уведомления, пока выполняется перенос.</span><span class="sxs-lookup"><span data-stu-id="7f133-125">Once you click **Yes** and allow the script to proceed, you will not receive any notifications while it's performing the migration.</span></span>  

<span data-ttu-id="7f133-126">Чтобы переместить ресурс в новую подписку, добавьте значение параметра *DestinationSubscriptionId* .</span><span class="sxs-lookup"><span data-stu-id="7f133-126">To move to a new subscription, include a value for the *DestinationSubscriptionId* parameter.</span></span>

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup" -DestinationSubscriptionId "SubscriptionId"
   ```

<span data-ttu-id="7f133-127">Как и в предыдущем примере, вам будет предложено подтвердить перемещение.</span><span class="sxs-lookup"><span data-stu-id="7f133-127">As with the previous example, you will be prompted to confirm the move.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="7f133-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7f133-128">Next steps</span></span>
* <span data-ttu-id="7f133-129">Дополнительные сведения см. в статье [Перемещение ресурсов в новую группу ресурсов или подписку](../azure-resource-manager/resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="7f133-129">For more information about moving resources to new resource group or subscription, see [Move  resources to new resource group or subscription](../azure-resource-manager/resource-group-move-resources.md)</span></span>
* <span data-ttu-id="7f133-130">Дополнительные сведения об управлении доступом на основе ролей в службе автоматизации Azure см. в [этой статье](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="7f133-130">For more information about Role-based Access Control in Azure Automation, refer to [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="7f133-131">Сведения о командлетах PowerShell для управления подпиской см. в статье [Использование Azure PowerShell с Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="7f133-131">To learn about PowerShell cmdlets for managing your subscription, see [Using Azure PowerShell with Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md)</span></span>
* <span data-ttu-id="7f133-132">Сведения о функциях портала для управления подпиской см. в статье [Управление ресурсами Azure через портал](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7f133-132">To learn about portal features for managing your subscription, see [Using the Azure Portal to manage resources](../azure-resource-manager/resource-group-portal.md).</span></span>
