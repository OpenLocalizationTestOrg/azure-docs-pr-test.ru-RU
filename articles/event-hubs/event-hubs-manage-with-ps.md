---
title: "Управление ресурсами концентраторов событий Azure с помощью PowerShell | Документация Майкрософт"
description: "Создание концентраторов событий и управление ими с помощью модуля PowerShell"
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
ms.openlocfilehash: 2b49c01153b1104612e6ebf9c88566fc40d1f635
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="use-powershell-to-manage-event-hubs-resources"></a><span data-ttu-id="48b5c-103">Управление ресурсами концентраторов событий с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="48b5c-103">Use PowerShell to manage Event Hubs resources</span></span>

<span data-ttu-id="48b5c-104">Microsoft Azure PowerShell — это среда сценариев, которую можно использовать для контроля и автоматизации развертывания служб Azure, а также для управления ими.</span><span class="sxs-lookup"><span data-stu-id="48b5c-104">Microsoft Azure PowerShell is a scripting environment that you can use to control and automate the deployment and management of Azure services.</span></span> <span data-ttu-id="48b5c-105">В этой статье описывается, как с помощью [модуля Resource Manager PowerShell для концентраторов событий](/powershell/module/azurerm.eventhub) подготавливать сущности концентраторов событий (пространства имен, отдельные концентраторы событий и группы потребителей) и управлять ими, используя локальную консоль или сценарий Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="48b5c-105">This article describes how to use the [Event Hubs Resource Manager PowerShell module](/powershell/module/azurerm.eventhub) to provision and manage Event Hubs entities (namespaces, individual event hubs, and consumer groups) using a local Azure PowerShell console or script.</span></span>

<span data-ttu-id="48b5c-106">Вы также можете управлять ресурсами концентраторов событий с помощью шаблонов Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="48b5c-106">You can also manage Event Hubs resources using Azure Resource Manager templates.</span></span> <span data-ttu-id="48b5c-107">Дополнительные сведения см. в статье [Создание пространства имен концентраторов событий с концентратором событий и группой потребителей с помощью шаблона Azure Resource Manager](event-hubs-resource-manager-namespace-event-hub.md).</span><span class="sxs-lookup"><span data-stu-id="48b5c-107">For more information, see the article [Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="48b5c-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="48b5c-108">Prerequisites</span></span>

<span data-ttu-id="48b5c-109">Для этого потребуются следующие компоненты.</span><span class="sxs-lookup"><span data-stu-id="48b5c-109">Before you begin, you'll need the following:</span></span>

* <span data-ttu-id="48b5c-110">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="48b5c-110">An Azure subscription.</span></span> <span data-ttu-id="48b5c-111">Дополнительные сведения о получении подписки см. на страницах [Как приобрести Azure][purchase options], [Предложения для участников][member offers] или [Создайте бесплатную учетную запись Azure уже сегодня][free account].</span><span class="sxs-lookup"><span data-stu-id="48b5c-111">For more information about obtaining a subscription, see [purchase options][purchase options], [member offers][member offers], or [free account][free account].</span></span>
* <span data-ttu-id="48b5c-112">Компьютер с Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="48b5c-112">A computer with Azure PowerShell.</span></span> <span data-ttu-id="48b5c-113">Инструкции см. в статье [Приступая к работе с командлетами Azure PowerShell](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="48b5c-113">For instructions, see [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps).</span></span>
* <span data-ttu-id="48b5c-114">Общее представление о сценариях PowerShell, пакетах NuGet и платформе .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="48b5c-114">A general understanding of PowerShell scripts, NuGet packages, and the .NET Framework.</span></span>

## <a name="get-started"></a><span data-ttu-id="48b5c-115">Начало работы</span><span class="sxs-lookup"><span data-stu-id="48b5c-115">Get started</span></span>

<span data-ttu-id="48b5c-116">Сначала мы используем PowerShell для входа в учетную запись Azure и подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="48b5c-116">The first step is to use PowerShell to log in to your Azure account and Azure subscription.</span></span> <span data-ttu-id="48b5c-117">Выполните инструкции, приведенные в руководстве по [началу работы с командлетами Azure PowerShell](/powershell/azure/get-started-azureps), чтобы войти в учетную запись Azure, а также получить и просмотреть ресурсы в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="48b5c-117">Follow the instructions in [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps) to log in to your Azure account, then retrieve and access the resources in your Azure subscription.</span></span>

## <a name="provision-an-event-hubs-namespace"></a><span data-ttu-id="48b5c-118">Подготовка пространства имен концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="48b5c-118">Provision an Event Hubs namespace</span></span>

<span data-ttu-id="48b5c-119">При работе с пространствами имен концентраторов событий можно использовать командлеты [Get-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/get-azurermeventhubnamespace), [New-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/new-azurermeventhubnamespace), [Remove-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/remove-azurermeventhubnamespace) и [Set-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/set-azurermeventhubnamespace).</span><span class="sxs-lookup"><span data-stu-id="48b5c-119">When working with Event Hubs namespaces, you can use the [Get-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/get-azurermeventhubnamespace), [New-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/new-azurermeventhubnamespace), [Remove-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/remove-azurermeventhubnamespace), and [Set-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/set-azurermeventhubnamespace) cmdlets.</span></span>

<span data-ttu-id="48b5c-120">В этом примере мы создадим несколько локальных переменных в сценарии, в частности `$Namespace` и `$Location`.</span><span class="sxs-lookup"><span data-stu-id="48b5c-120">This example creates a few local variables in the script; `$Namespace` and `$Location`.</span></span>

* <span data-ttu-id="48b5c-121">`$Namespace` — имя пространства имен концентраторов событий, которое мы будем использовать.</span><span class="sxs-lookup"><span data-stu-id="48b5c-121">`$Namespace` is the name of the Event Hubs namespace with which we want to work.</span></span>
* <span data-ttu-id="48b5c-122">`$Location` — центр обработки данных, в котором мы подготовим пространство имен к работе.</span><span class="sxs-lookup"><span data-stu-id="48b5c-122">`$Location` identifies the data center in which will we provision the namespace.</span></span>
* <span data-ttu-id="48b5c-123">`$CurrentNamespace` — место хранения полученного (или созданного) исходного пространства имен.</span><span class="sxs-lookup"><span data-stu-id="48b5c-123">`$CurrentNamespace` stores the reference namespace that we retrieve (or create).</span></span>

<span data-ttu-id="48b5c-124">В фактическом сценарии переменные `$Namespace` и `$Location` могут передаваться как параметры.</span><span class="sxs-lookup"><span data-stu-id="48b5c-124">In an actual script, `$Namespace` and `$Location` can be passed as parameters.</span></span>

<span data-ttu-id="48b5c-125">Эта часть сценария выполняет следующее:</span><span class="sxs-lookup"><span data-stu-id="48b5c-125">This part of the script does the following:</span></span>

1. <span data-ttu-id="48b5c-126">Пытается получить пространство имен концентраторов событий с заданным именем.</span><span class="sxs-lookup"><span data-stu-id="48b5c-126">Attempts to retrieve an Event Hubs namespace with the specified name.</span></span>
2. <span data-ttu-id="48b5c-127">Если пространство имен найдено, появляется сообщение о том, что именно нашел сценарий.</span><span class="sxs-lookup"><span data-stu-id="48b5c-127">If the namespace is found, it reports what was found.</span></span>
3. <span data-ttu-id="48b5c-128">Если пространство имен не найдено, сценарий создает его и возвращает созданное пространство.</span><span class="sxs-lookup"><span data-stu-id="48b5c-128">If the namespace is not found, it creates the namespace and then retrieves the newly created namespace.</span></span>

    ```powershell
    # Query to see if the namespace currently exists
    $CurrentNamespace = Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
   
    # Check if the namespace already exists or needs to be created
    if ($CurrentNamespace)
    {
        Write-Host "The namespace $Namespace already exists in the $Location region:"
        # Report what was found
        Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
    }
    else
    {
        Write-Host "The $Namespace namespace does not exist."
        Write-Host "Creating the $Namespace namespace in the $Location region..."
        New-AzureRmEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace -Location $Location
        $CurrentNamespace = Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
        Write-Host "The $Namespace namespace in Resource Group $ResGrpName in the $Location region has been successfully created."
    }
    ```

## <a name="create-an-event-hub"></a><span data-ttu-id="48b5c-129">Создание концентратора событий</span><span class="sxs-lookup"><span data-stu-id="48b5c-129">Create an event hub</span></span>

<span data-ttu-id="48b5c-130">Чтобы создать концентратор событий, проверьте пространство имен с помощью сценария, приведенного в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="48b5c-130">To create an event hub, perform a namespace check using the script in the previous section.</span></span> <span data-ttu-id="48b5c-131">Затем создайте концентратор событий, используя командлет [New-AzureRmEventHub](/powershell/module/azurerm.eventhub/new-azurermeventhub):</span><span class="sxs-lookup"><span data-stu-id="48b5c-131">Then, use the [New-AzureRmEventHub](/powershell/module/azurerm.eventhub/new-azurermeventhub) cmdlet to create the event hub:</span></span>

```powershell
# Check if event hub already exists
$CurrentEH = Get-AzureRMEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName

if($CurrentEH)
{
    Write-Host "The event hub $EventHubName already exists in the $Location region:"
    # Report what was found
    Get-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
}
else
{
    Write-Host "The $EventHubName event hub does not exist."
    Write-Host "Creating the $EventHubName event hub in the $Location region..."
    New-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -Location $Location -MessageRetentionInDays 3
    $CurrentEH = Get-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
    Write-Host "The $EventHubName event hub in Resource Group $ResGrpName in the $Location region has been successfully created."
}
```

### <a name="create-a-consumer-group"></a><span data-ttu-id="48b5c-132">Создание группы потребителей</span><span class="sxs-lookup"><span data-stu-id="48b5c-132">Create a consumer group</span></span>

<span data-ttu-id="48b5c-133">Чтобы создать в концентраторе событий группу потребителей, проверьте пространство имен и концентратор событий с помощью сценариев, приведенных в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="48b5c-133">To create a consumer group within an event hub, perform the namespace and event hub checks using the scripts in the previous section.</span></span> <span data-ttu-id="48b5c-134">Затем создайте группу потребителей в концентраторе событий, используя командлет [New-AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/new-azurermeventhubconsumergroup).</span><span class="sxs-lookup"><span data-stu-id="48b5c-134">Then, use the [New-AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/new-azurermeventhubconsumergroup) cmdlet to create the consumer group within the event hub.</span></span> <span data-ttu-id="48b5c-135">Например:</span><span class="sxs-lookup"><span data-stu-id="48b5c-135">For example:</span></span>

```powershell
# Check if consumer group already exists
$CurrentCG = Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName -ErrorAction Ignore

if($CurrentCG)
{
    Write-Host "The consumer group $ConsumerGroupName in event hub $EventHubName already exists in the $Location region:"
    # Report what was found
    Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
}
else
{
    Write-Host "The $ConsumerGroupName consumer group does not exist."
    Write-Host "Creating the $ConsumerGroupName consumer group in the $Location region..."
    New-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
    $CurrentCG = Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
    Write-Host "The $ConsumerGroupName consumer group in event hub $EventHubName in Resource Group $ResGrpName in the $Location region has been successfully created."
}
```

#### <a name="set-user-metadata"></a><span data-ttu-id="48b5c-136">Определение метаданных пользователей</span><span class="sxs-lookup"><span data-stu-id="48b5c-136">Set user metadata</span></span>

<span data-ttu-id="48b5c-137">После выполнения сценариев из предыдущих разделов можно воспользоваться командлетом [Set-AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/set-azurermeventhubconsumergroup), чтобы обновить свойства группы потребителей, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="48b5c-137">After executing the scripts in the preceding sections, you can use the [Set-AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/set-azurermeventhubconsumergroup) cmdlet to update the properties of a consumer group, as in the following example:</span></span>

```powershell
# Set some user metadata on the CG
Write-Host "Setting the UserMetadata field to 'Testing'"
Set-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName -UserMetadata "Testing"
# Show result
Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
```

## <a name="remove-event-hub"></a><span data-ttu-id="48b5c-138">Удаление концентратора событий</span><span class="sxs-lookup"><span data-stu-id="48b5c-138">Remove event hub</span></span>

<span data-ttu-id="48b5c-139">Чтобы удалить созданные вами концентраторы событий, используйте командлеты `Remove-*`, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="48b5c-139">To remove the event hubs you created, you can use the `Remove-*` cmdlets, as in the following example:</span></span>

```powershell
# Clean up
Remove-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
Remove-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
Remove-AzureRmEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
```

## <a name="next-steps"></a><span data-ttu-id="48b5c-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="48b5c-140">Next steps</span></span>

- <span data-ttu-id="48b5c-141">С полной документацией по модулю Resource Manager PowerShell для концентраторов событий можно ознакомиться [здесь](/powershell/module/azurerm.eventhub).</span><span class="sxs-lookup"><span data-stu-id="48b5c-141">See the complete Event Hubs Resource Manager PowerShell module documentation [here](/powershell/module/azurerm.eventhub).</span></span> <span data-ttu-id="48b5c-142">На этой странице перечислены все доступные командлеты.</span><span class="sxs-lookup"><span data-stu-id="48b5c-142">This page lists all available cmdlets.</span></span>
- <span data-ttu-id="48b5c-143">Дополнительные сведения об использовании шаблонов Azure Resource Manager см. в статье [Создание пространства имен концентраторов событий с концентратором событий и группой потребителей с помощью шаблона Azure Resource Manager](event-hubs-resource-manager-namespace-event-hub.md).</span><span class="sxs-lookup"><span data-stu-id="48b5c-143">For information about using Azure Resource Manager templates, see the article [Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub.md).</span></span>
- <span data-ttu-id="48b5c-144">Сведения о [библиотеках управления .NET для концентраторов событий](event-hubs-management-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="48b5c-144">Information about [Event Hubs .NET management libraries](event-hubs-management-libraries.md).</span></span>

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
