---
title: "aaaMigrate учетной записи автоматизации и ресурсам | Документы Microsoft"
description: "В этой статье описывается, как toomove автоматизации учетной записи в службе автоматизации Azure и связанных ресурсов из tooanother одна подписка."
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
ms.openlocfilehash: 201c9091cd2d78d7ea407c1e5fb27f366bb4fa8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-automation-account-and-resources"></a><span data-ttu-id="7f3e6-103">Перенос учетной записи и ресурсов службы автоматизации</span><span class="sxs-lookup"><span data-stu-id="7f3e6-103">Migrate Automation Account and resources</span></span>
<span data-ttu-id="7f3e6-104">Для учетных записей автоматизации и его связанные ресурсы (т. е. ресурсы, модули Runbook, модули, т. д.), которые вы создали в hello портал Azure и хотите toomigrate из одного ресурса группы tooanother или из tooanother одна подписка для этого можно легко с Hello [перемещение ресурсов](../azure-resource-manager/resource-group-move-resources.md) компонент, доступный в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="7f3e6-104">For Automation accounts and its associated resources (i.e. assets, runbooks, modules, etc.) that you have created in hello Azure portal and want toomigrate from one resource group tooanother or from one subscription tooanother, you can accomplish this easily with hello [move resources](../azure-resource-manager/resource-group-move-resources.md) feature available in hello Azure portal.</span></span> <span data-ttu-id="7f3e6-105">Тем не менее, прежде чем выполнять это действие, необходимо просмотреть следующие hello [контрольный список до перемещения ресурсов](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) и Кроме того, список hello ниже определенного tooAutomation.</span><span class="sxs-lookup"><span data-stu-id="7f3e6-105">However, before proceeding with this action, you should first review hello following [checklist before moving resources](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) and additionally, hello list below specific tooAutomation.</span></span>   

1. <span data-ttu-id="7f3e6-106">Hello назначения подписку или группу ресурсов должен быть в одном регионе, что источник hello.</span><span class="sxs-lookup"><span data-stu-id="7f3e6-106">hello destination subscription/resource group must be in same region as hello source.</span></span>  <span data-ttu-id="7f3e6-107">Это означает, что учетные записи службы автоматизации нельзя перемещать между регионами.</span><span class="sxs-lookup"><span data-stu-id="7f3e6-107">Meaning, Automation accounts cannot be moved across regions.</span></span>
2. <span data-ttu-id="7f3e6-108">При перемещении ресурсов (например, модули Runbook, заданий, т. д.), исходная группа hello и целевая группа hello блокируются hello время выполнения операции hello.</span><span class="sxs-lookup"><span data-stu-id="7f3e6-108">When moving resources (e.g. runbooks, jobs, etc.), both hello source group and hello target group are locked for hello duration of hello operation.</span></span> <span data-ttu-id="7f3e6-109">Записи и удаления операций блокируются на группах hello до завершения перемещения hello.</span><span class="sxs-lookup"><span data-stu-id="7f3e6-109">Write and delete operations are blocked on hello groups until hello move completes.</span></span>  
3. <span data-ttu-id="7f3e6-110">Модулей Runbook или переменные, которые ссылаются идентификатор ресурса или подписки из существующей подписки hello потребуется toobe обновлена после завершения миграции.</span><span class="sxs-lookup"><span data-stu-id="7f3e6-110">Any runbooks or variables which reference a resource or subscription ID from hello existing subscription will need toobe updated after migration is completed.</span></span>   

> [!NOTE]
> <span data-ttu-id="7f3e6-111">Данная функция не поддерживает перемещение классических ресурсов службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="7f3e6-111">This feature does not support moving Classic automation resources.</span></span>
>
>

## <a name="toomove-hello-automation-account-using-hello-portal"></a><span data-ttu-id="7f3e6-112">Учетная запись службы автоматизации с помощью портала hello hello toomove</span><span class="sxs-lookup"><span data-stu-id="7f3e6-112">toomove hello Automation Account using hello portal</span></span>
1. <span data-ttu-id="7f3e6-113">Ваша учетная запись автоматизации щелкните **переместить** hello верхней части колонки hello.</span><span class="sxs-lookup"><span data-stu-id="7f3e6-113">From your Automation account, click **Move** at hello top of hello blade.</span></span><br> <span data-ttu-id="7f3e6-114">![Параметр "Переместить"](media/automation-migrate-account-subscription/automation-menu-move.png)</span><span class="sxs-lookup"><span data-stu-id="7f3e6-114">![Move option](media/automation-migrate-account-subscription/automation-menu-move.png)</span></span><br>
2. <span data-ttu-id="7f3e6-115">На hello **перемещение ресурсов** колонки, обратите внимание, что она представляет tooboth связанные ресурсы, ваша учетная запись автоматизации и вашей группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7f3e6-115">On hello **Move resources** blade, note that it presents resources related tooboth your Automation account and your resource group(s).</span></span>  <span data-ttu-id="7f3e6-116">Выберите hello **подписки** и **группы ресурсов** из раскрывающихся списков hello или hello выберите параметр **создать новую группу ресурсов** и введите новое имя группы ресурсов в поле Hello.</span><span class="sxs-lookup"><span data-stu-id="7f3e6-116">Select hello **subscription** and **resource group** from hello drop-down lists, or select hello option **create a new resource group** and enter a new resource group name in hello field provided.</span></span>  
3. <span data-ttu-id="7f3e6-117">Просмотрите и выберите hello флажок tooacknowledge вы *понять средства и сценарии, будет необходимости обновить toobe toouse новые идентификаторы ресурсов после перемещения ресурсов* и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="7f3e6-117">Review and select hello checkbox tooacknowledge you *understand tools and scripts will need toobe updated toouse new resource IDs after resources have been moved* and then click **OK**.</span></span><br> <span data-ttu-id="7f3e6-118">![Колонка "Перемещение ресурсов"](media/automation-migrate-account-subscription/automation-move-resources-blade.png)</span><span class="sxs-lookup"><span data-stu-id="7f3e6-118">![Move Resources Blade](media/automation-migrate-account-subscription/automation-move-resources-blade.png)</span></span><br>   

<span data-ttu-id="7f3e6-119">Это действие займет несколько минут toocomplete.</span><span class="sxs-lookup"><span data-stu-id="7f3e6-119">This action will take several minutes toocomplete.</span></span>  <span data-ttu-id="7f3e6-120">В разделе **Уведомления** будет показано состояние каждого выполняемого действия — проверки, переноса и т. д., после чего отобразится сообщение о завершении операции.</span><span class="sxs-lookup"><span data-stu-id="7f3e6-120">In **Notifications**, you will be presented with a status of each action that takes place - validation, migration, and then finally when it is completed.</span></span>     

## <a name="toomove-hello-automation-account-using-powershell"></a><span data-ttu-id="7f3e6-121">toomove hello учетной записи автоматизации с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="7f3e6-121">toomove hello Automation Account using PowerShell</span></span>
<span data-ttu-id="7f3e6-122">toomove существующую группу ресурсов tooanother ресурсов автоматизации или подписку, используйте hello **Get-AzureRmResource** командлет tooget hello конкретных учетная запись службы автоматизации и затем **Move-AzureRmResource** Переместите hello tooperform командлета.</span><span class="sxs-lookup"><span data-stu-id="7f3e6-122">toomove existing Automation resources tooanother resource group or subscription, use hello  **Get-AzureRmResource** cmdlet tooget hello specific Automation account and then **Move-AzureRmResource** cmdlet tooperform hello move.</span></span>

<span data-ttu-id="7f3e6-123">Hello первом примере показано, как toomove автоматизации учетной записи tooa новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7f3e6-123">hello first example shows how toomove an Automation account tooa new resource group.</span></span>

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup"
   ```

<span data-ttu-id="7f3e6-124">После выполнения hello выше примере можно запрашиваемые tooverify требуется tooperform это действие.</span><span class="sxs-lookup"><span data-stu-id="7f3e6-124">After you execute hello above code example, you will be prompted tooverify you want tooperform this action.</span></span>  <span data-ttu-id="7f3e6-125">После нажатия кнопки **Да** и разрешить Здравствуйте tooproceed скрипт, пользователь не будет получать уведомления при выполнении миграции hello.</span><span class="sxs-lookup"><span data-stu-id="7f3e6-125">Once you click **Yes** and allow hello script tooproceed, you will not receive any notifications while it's performing hello migration.</span></span>  

<span data-ttu-id="7f3e6-126">toomove tooa новую подписку, добавьте значение hello *DestinationSubscriptionId* параметра.</span><span class="sxs-lookup"><span data-stu-id="7f3e6-126">toomove tooa new subscription, include a value for hello *DestinationSubscriptionId* parameter.</span></span>

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup" -DestinationSubscriptionId "SubscriptionId"
   ```

<span data-ttu-id="7f3e6-127">Как и в предыдущем примере hello будет запрашиваемые tooconfirm hello перемещения.</span><span class="sxs-lookup"><span data-stu-id="7f3e6-127">As with hello previous example, you will be prompted tooconfirm hello move.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="7f3e6-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7f3e6-128">Next steps</span></span>
* <span data-ttu-id="7f3e6-129">Дополнительные сведения о перемещения группы ресурсов toonew ресурсов или подписки см. в разделе [переместить группу ресурсов toonew ресурсов или подписку](../azure-resource-manager/resource-group-move-resources.md)</span><span class="sxs-lookup"><span data-stu-id="7f3e6-129">For more information about moving resources toonew resource group or subscription, see [Move  resources toonew resource group or subscription](../azure-resource-manager/resource-group-move-resources.md)</span></span>
* <span data-ttu-id="7f3e6-130">Дополнительные сведения об элементе управления доступом на основе ролей в службе автоматизации Azure дополнительную информацию слишком[управления доступом на основе ролей в службе автоматизации Azure](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="7f3e6-130">For more information about Role-based Access Control in Azure Automation, refer too[Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="7f3e6-131">в разделе toolearn о командлетах PowerShell для управления подпиской, [с помощью Azure PowerShell с помощью диспетчера ресурсов](../azure-resource-manager/powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="7f3e6-131">toolearn about PowerShell cmdlets for managing your subscription, see [Using Azure PowerShell with Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md)</span></span>
* <span data-ttu-id="7f3e6-132">toolearn портала возможности для управления подпиской, в разделе [использование ресурсов toomanage портала Azure hello](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7f3e6-132">toolearn about portal features for managing your subscription, see [Using hello Azure Portal toomanage resources](../azure-resource-manager/resource-group-portal.md).</span></span>
