---
title: "ресурсы концентраторов событий Azure toomanage aaaUse PowerShell | Документы Microsoft"
description: "Использование toocreate модуля PowerShell и управление ими концентраторов событий"
services: event-hubs
documentationcenter: .NET
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: d79cb307c2b4a031d059ce6ca67117ffc0b4600b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomanage-event-hubs-resources"></a><span data-ttu-id="9970e-103">Использовать ресурсы концентраторов событий toomanage PowerShell</span><span class="sxs-lookup"><span data-stu-id="9970e-103">Use PowerShell toomanage Event Hubs resources</span></span>

<span data-ttu-id="9970e-104">Microsoft Azure PowerShell — это среда сценариев, можно использовать toocontrol и автоматизации развертывания hello и управления службами Azure.</span><span class="sxs-lookup"><span data-stu-id="9970e-104">Microsoft Azure PowerShell is a scripting environment that you can use toocontrol and automate hello deployment and management of Azure services.</span></span> <span data-ttu-id="9970e-105">В этой статье описывается как toouse hello [модуль PowerShell диспетчера ресурсов концентраторов событий](/powershell/module/azurerm.eventhub) tooprovision и управлять сущностями концентраторов событий (пространства имен, концентраторы отдельных событий и групп потребителей) с помощью локальной консоли Azure PowerShell или скрипт.</span><span class="sxs-lookup"><span data-stu-id="9970e-105">This article describes how toouse hello [Event Hubs Resource Manager PowerShell module](/powershell/module/azurerm.eventhub) tooprovision and manage Event Hubs entities (namespaces, individual event hubs, and consumer groups) using a local Azure PowerShell console or script.</span></span>

<span data-ttu-id="9970e-106">Вы также можете управлять ресурсами концентраторов событий с помощью шаблонов Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9970e-106">You can also manage Event Hubs resources using Azure Resource Manager templates.</span></span> <span data-ttu-id="9970e-107">Дополнительные сведения см. в статье hello [создать пространство имен концентраторов событий с концентратором и потребитель группа событий с помощью шаблона Azure Resource Manager](event-hubs-resource-manager-namespace-event-hub.md).</span><span class="sxs-lookup"><span data-stu-id="9970e-107">For more information, see hello article [Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9970e-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9970e-108">Prerequisites</span></span>

<span data-ttu-id="9970e-109">Прежде чем начать, необходимо иметь следующие hello:</span><span class="sxs-lookup"><span data-stu-id="9970e-109">Before you begin, you'll need hello following:</span></span>

* <span data-ttu-id="9970e-110">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="9970e-110">An Azure subscription.</span></span> <span data-ttu-id="9970e-111">Дополнительные сведения о получении подписки см. на страницах [Как приобрести Azure][purchase options], [Предложения для участников][member offers] или [Создайте бесплатную учетную запись Azure уже сегодня][free account].</span><span class="sxs-lookup"><span data-stu-id="9970e-111">For more information about obtaining a subscription, see [purchase options][purchase options], [member offers][member offers], or [free account][free account].</span></span>
* <span data-ttu-id="9970e-112">Компьютер с Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9970e-112">A computer with Azure PowerShell.</span></span> <span data-ttu-id="9970e-113">Инструкции см. в статье [Приступая к работе с командлетами Azure PowerShell](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="9970e-113">For instructions, see [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps).</span></span>
* <span data-ttu-id="9970e-114">Общее представление о сценарии PowerShell, пакеты NuGet и hello .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="9970e-114">A general understanding of PowerShell scripts, NuGet packages, and hello .NET Framework.</span></span>

## <a name="get-started"></a><span data-ttu-id="9970e-115">Начало работы</span><span class="sxs-lookup"><span data-stu-id="9970e-115">Get started</span></span>

<span data-ttu-id="9970e-116">Hello первым шагом является toouse toolog PowerShell в tooyour учетная запись Azure и подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="9970e-116">hello first step is toouse PowerShell toolog in tooyour Azure account and Azure subscription.</span></span> <span data-ttu-id="9970e-117">Следуйте инструкциям в разделе hello [приступить к работе с помощью командлетов Azure PowerShell](/powershell/azure/get-started-azureps) toolog в tooyour учетная запись Azure, затем извлекается и получить доступ к ресурсам hello в вашей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="9970e-117">Follow hello instructions in [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps) toolog in tooyour Azure account, then retrieve and access hello resources in your Azure subscription.</span></span>

## <a name="provision-an-event-hubs-namespace"></a><span data-ttu-id="9970e-118">Подготовка пространства имен концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="9970e-118">Provision an Event Hubs namespace</span></span>

<span data-ttu-id="9970e-119">При работе с пространствами имен концентраторов событий можно использовать hello [Get AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/get-azurermeventhubnamespace), [New AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/new-azurermeventhubnamespace), [AzureRmEventHubNamespace удаление](/powershell/module/azurerm.eventhub/remove-azurermeventhubnamespace) , и [AzureRmEventHubNamespace набор](/powershell/module/azurerm.eventhub/set-azurermeventhubnamespace) командлетов.</span><span class="sxs-lookup"><span data-stu-id="9970e-119">When working with Event Hubs namespaces, you can use hello [Get-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/get-azurermeventhubnamespace), [New-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/new-azurermeventhubnamespace), [Remove-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/remove-azurermeventhubnamespace), and [Set-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/set-azurermeventhubnamespace) cmdlets.</span></span>

<span data-ttu-id="9970e-120">В этом примере создается несколько локальных переменных в сценарии hello; `$Namespace` и `$Location`.</span><span class="sxs-lookup"><span data-stu-id="9970e-120">This example creates a few local variables in hello script; `$Namespace` and `$Location`.</span></span>

* <span data-ttu-id="9970e-121">`$Namespace`— Имя пространства имен hello концентраторов событий, с которым мы хотим toowork hello.</span><span class="sxs-lookup"><span data-stu-id="9970e-121">`$Namespace` is hello name of hello Event Hubs namespace with which we want toowork.</span></span>
* <span data-ttu-id="9970e-122">`$Location`Идентифицирует hello центр обработки данных, в котором мы подготовит hello пространства имен.</span><span class="sxs-lookup"><span data-stu-id="9970e-122">`$Location` identifies hello data center in which will we provision hello namespace.</span></span>
* <span data-ttu-id="9970e-123">`$CurrentNamespace`хранит ссылку hello пространство имен, которое мы извлечения (или создайте).</span><span class="sxs-lookup"><span data-stu-id="9970e-123">`$CurrentNamespace` stores hello reference namespace that we retrieve (or create).</span></span>

<span data-ttu-id="9970e-124">В фактическом сценарии переменные `$Namespace` и `$Location` могут передаваться как параметры.</span><span class="sxs-lookup"><span data-stu-id="9970e-124">In an actual script, `$Namespace` and `$Location` can be passed as parameters.</span></span>

<span data-ttu-id="9970e-125">Эта часть скрипта hello hello следующие:</span><span class="sxs-lookup"><span data-stu-id="9970e-125">This part of hello script does hello following:</span></span>

1. <span data-ttu-id="9970e-126">Попыток tooretrieve пространстве имен концентраторы событий с hello заданное имя.</span><span class="sxs-lookup"><span data-stu-id="9970e-126">Attempts tooretrieve an Event Hubs namespace with hello specified name.</span></span>
2. <span data-ttu-id="9970e-127">Если hello пространства имен, он сообщает, что был найден.</span><span class="sxs-lookup"><span data-stu-id="9970e-127">If hello namespace is found, it reports what was found.</span></span>
3. <span data-ttu-id="9970e-128">Если пространство имен hello не найден, он создает пространство имен hello и затем извлекает hello вновь создано и пространство имен.</span><span class="sxs-lookup"><span data-stu-id="9970e-128">If hello namespace is not found, it creates hello namespace and then retrieves hello newly created namespace.</span></span>

    ```powershell
    # Query toosee if hello namespace currently exists
    $CurrentNamespace = Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
   
    # Check if hello namespace already exists or needs toobe created
    if ($CurrentNamespace)
    {
        Write-Host "hello namespace $Namespace already exists in hello $Location region:"
        # Report what was found
        Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
    }
    else
    {
        Write-Host "hello $Namespace namespace does not exist."
        Write-Host "Creating hello $Namespace namespace in hello $Location region..."
        New-AzureRmEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace -Location $Location
        $CurrentNamespace = Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
        Write-Host "hello $Namespace namespace in Resource Group $ResGrpName in hello $Location region has been successfully created."
    }
    ```

## <a name="create-an-event-hub"></a><span data-ttu-id="9970e-129">Создание концентратора событий</span><span class="sxs-lookup"><span data-stu-id="9970e-129">Create an event hub</span></span>

<span data-ttu-id="9970e-130">toocreate концентратора событий, выполните проверку пространства имен, с помощью скрипта hello в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="9970e-130">toocreate an event hub, perform a namespace check using hello script in hello previous section.</span></span> <span data-ttu-id="9970e-131">Затем с помощью hello [New AzureRmEventHub](/powershell/module/azurerm.eventhub/new-azurermeventhub) концентратора событий hello toocreate командлета:</span><span class="sxs-lookup"><span data-stu-id="9970e-131">Then, use hello [New-AzureRmEventHub](/powershell/module/azurerm.eventhub/new-azurermeventhub) cmdlet toocreate hello event hub:</span></span>

```powershell
# Check if event hub already exists
$CurrentEH = Get-AzureRMEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName

if($CurrentEH)
{
    Write-Host "hello event hub $EventHubName already exists in hello $Location region:"
    # Report what was found
    Get-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
}
else
{
    Write-Host "hello $EventHubName event hub does not exist."
    Write-Host "Creating hello $EventHubName event hub in hello $Location region..."
    New-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -Location $Location -MessageRetentionInDays 3
    $CurrentEH = Get-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
    Write-Host "hello $EventHubName event hub in Resource Group $ResGrpName in hello $Location region has been successfully created."
}
```

### <a name="create-a-consumer-group"></a><span data-ttu-id="9970e-132">Создание группы потребителей</span><span class="sxs-lookup"><span data-stu-id="9970e-132">Create a consumer group</span></span>

<span data-ttu-id="9970e-133">toocreate группы потребителей в концентраторе событий проверки hello пространства имен и события концентратора с помощью сценариев hello в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="9970e-133">toocreate a consumer group within an event hub, perform hello namespace and event hub checks using hello scripts in hello previous section.</span></span> <span data-ttu-id="9970e-134">Затем с помощью hello [New AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/new-azurermeventhubconsumergroup) группы потребителей hello toocreate командлета в концентраторе событий hello.</span><span class="sxs-lookup"><span data-stu-id="9970e-134">Then, use hello [New-AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/new-azurermeventhubconsumergroup) cmdlet toocreate hello consumer group within hello event hub.</span></span> <span data-ttu-id="9970e-135">Например:</span><span class="sxs-lookup"><span data-stu-id="9970e-135">For example:</span></span>

```powershell
# Check if consumer group already exists
$CurrentCG = Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName -ErrorAction Ignore

if($CurrentCG)
{
    Write-Host "hello consumer group $ConsumerGroupName in event hub $EventHubName already exists in hello $Location region:"
    # Report what was found
    Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
}
else
{
    Write-Host "hello $ConsumerGroupName consumer group does not exist."
    Write-Host "Creating hello $ConsumerGroupName consumer group in hello $Location region..."
    New-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
    $CurrentCG = Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
    Write-Host "hello $ConsumerGroupName consumer group in event hub $EventHubName in Resource Group $ResGrpName in hello $Location region has been successfully created."
}
```

#### <a name="set-user-metadata"></a><span data-ttu-id="9970e-136">Определение метаданных пользователей</span><span class="sxs-lookup"><span data-stu-id="9970e-136">Set user metadata</span></span>

<span data-ttu-id="9970e-137">После выполнения скриптов hello в предыдущих разделах hello, можно использовать hello [AzureRmEventHubConsumerGroup набор](/powershell/module/azurerm.eventhub/set-azurermeventhubconsumergroup) командлет tooupdate hello свойств группы потребителей, как следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="9970e-137">After executing hello scripts in hello preceding sections, you can use hello [Set-AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/set-azurermeventhubconsumergroup) cmdlet tooupdate hello properties of a consumer group, as in hello following example:</span></span>

```powershell
# Set some user metadata on hello CG
Write-Host "Setting hello UserMetadata field too'Testing'"
Set-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName -UserMetadata "Testing"
# Show result
Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
```

## <a name="remove-event-hub"></a><span data-ttu-id="9970e-138">Удаление концентратора событий</span><span class="sxs-lookup"><span data-stu-id="9970e-138">Remove event hub</span></span>

<span data-ttu-id="9970e-139">концентраторы событий hello tooremove был создан, можно использовать hello `Remove-*` командлеты, как следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="9970e-139">tooremove hello event hubs you created, you can use hello `Remove-*` cmdlets, as in hello following example:</span></span>

```powershell
# Clean up
Remove-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
Remove-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
Remove-AzureRmEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
```

## <a name="next-steps"></a><span data-ttu-id="9970e-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9970e-140">Next steps</span></span>

- <span data-ttu-id="9970e-141">В документации hello завершения PowerShell диспетчера ресурсов концентраторов событий модуля [здесь](/powershell/module/azurerm.eventhub).</span><span class="sxs-lookup"><span data-stu-id="9970e-141">See hello complete Event Hubs Resource Manager PowerShell module documentation [here](/powershell/module/azurerm.eventhub).</span></span> <span data-ttu-id="9970e-142">На этой странице перечислены все доступные командлеты.</span><span class="sxs-lookup"><span data-stu-id="9970e-142">This page lists all available cmdlets.</span></span>
- <span data-ttu-id="9970e-143">Сведения об использовании шаблонов диспетчера ресурсов Azure см. в статье hello [создать пространство имен концентраторов событий с концентратором и потребитель группа событий с помощью шаблона Azure Resource Manager](event-hubs-resource-manager-namespace-event-hub.md).</span><span class="sxs-lookup"><span data-stu-id="9970e-143">For information about using Azure Resource Manager templates, see hello article [Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub.md).</span></span>
- <span data-ttu-id="9970e-144">Сведения о [библиотеках управления .NET для концентраторов событий](event-hubs-management-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="9970e-144">Information about [Event Hubs .NET management libraries](event-hubs-management-libraries.md).</span></span>

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
