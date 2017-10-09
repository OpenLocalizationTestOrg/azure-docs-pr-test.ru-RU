---
title: "ресурсы Azure Service Bus toomanage aaaUse PowerShell | Документы Microsoft"
description: "Использовать toocreate модуля PowerShell и управлять ресурсами Service Bus"
services: service-bus-messaging
documentationcenter: .NET
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/06/2017
ms.author: sethm
ms.openlocfilehash: 737044def913c5798e7e05fc4f1aeece76c8f4dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomanage-service-bus-resources"></a><span data-ttu-id="4be05-103">Использование ресурсов служебной шины toomanage PowerShell</span><span class="sxs-lookup"><span data-stu-id="4be05-103">Use PowerShell toomanage Service Bus resources</span></span>

<span data-ttu-id="4be05-104">Microsoft Azure PowerShell — это среда сценариев, можно использовать toocontrol и автоматизации развертывания hello и управления службами Azure.</span><span class="sxs-lookup"><span data-stu-id="4be05-104">Microsoft Azure PowerShell is a scripting environment that you can use toocontrol and automate hello deployment and management of Azure services.</span></span> <span data-ttu-id="4be05-105">В этой статье описывается как toouse hello [модуль диспетчера ресурсов Service Bus PowerShell](/powershell/module/azurerm.servicebus) tooprovision и управления ими сущностей служебной шины (пространства имен, очереди, разделы и подписки) с помощью локальной консоли Azure PowerShell или скрипт.</span><span class="sxs-lookup"><span data-stu-id="4be05-105">This article describes how toouse hello [Service Bus Resource Manager PowerShell module](/powershell/module/azurerm.servicebus) tooprovision and manage Service Bus entities (namespaces, queues, topics, and subscriptions) using a local Azure PowerShell console or script.</span></span>

<span data-ttu-id="4be05-106">Сущностями служебной шины можно также управлять с помощью шаблонов Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4be05-106">You can also manage Service Bus entities using Azure Resource Manager templates.</span></span> <span data-ttu-id="4be05-107">Дополнительные сведения см. в статье hello [ресурсы создать Service Bus с помощью шаблонов диспетчера ресурсов Azure](service-bus-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4be05-107">For more information, see hello article [Create Service Bus resources using Azure Resource Manager templates](service-bus-resource-manager-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4be05-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4be05-108">Prerequisites</span></span>

<span data-ttu-id="4be05-109">Прежде чем начать, необходимо иметь следующие hello:</span><span class="sxs-lookup"><span data-stu-id="4be05-109">Before you begin, you'll need hello following:</span></span>

* <span data-ttu-id="4be05-110">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="4be05-110">An Azure subscription.</span></span> <span data-ttu-id="4be05-111">Дополнительные сведения о получении подписки см. на страницах [Как приобрести Azure][purchase options], [Предложения для участников][member offers] или [Создайте бесплатную учетную запись Azure уже сегодня][free account].</span><span class="sxs-lookup"><span data-stu-id="4be05-111">For more information about obtaining a subscription, see [purchase options][purchase options], [member offers][member offers], or [free account][free account].</span></span>
* <span data-ttu-id="4be05-112">Компьютер с Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4be05-112">A computer with Azure PowerShell.</span></span> <span data-ttu-id="4be05-113">Инструкции см. в статье [Приступая к работе с командлетами Azure PowerShell](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="4be05-113">For instructions, see [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps).</span></span>
* <span data-ttu-id="4be05-114">Общее представление о сценарии PowerShell, пакеты NuGet и hello .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="4be05-114">A general understanding of PowerShell scripts, NuGet packages, and hello .NET Framework.</span></span>

## <a name="get-started"></a><span data-ttu-id="4be05-115">Начало работы</span><span class="sxs-lookup"><span data-stu-id="4be05-115">Get started</span></span>

<span data-ttu-id="4be05-116">Hello первым шагом является toouse toolog PowerShell в tooyour учетная запись Azure и подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="4be05-116">hello first step is toouse PowerShell toolog in tooyour Azure account and Azure subscription.</span></span> <span data-ttu-id="4be05-117">Следуйте инструкциям в разделе hello [приступить к работе с помощью командлетов Azure PowerShell](/powershell/azure/get-started-azureps) toolog в tooyour учетная запись Azure и получение и доступа к ресурсам hello в вашей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="4be05-117">Follow hello instructions in [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps) toolog in tooyour Azure account, and retrieve and access hello resources in your Azure subscription.</span></span>

## <a name="provision-a-service-bus-namespace"></a><span data-ttu-id="4be05-118">Подготовка пространства имен Service Bus</span><span class="sxs-lookup"><span data-stu-id="4be05-118">Provision a Service Bus namespace</span></span>

<span data-ttu-id="4be05-119">При работе с пространствами имен Service Bus, можно использовать hello [Get AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespace), [New AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespace), [Remove-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespace), и [AzureRmServiceBusNamespace набор](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespace) командлетов.</span><span class="sxs-lookup"><span data-stu-id="4be05-119">When working with Service Bus namespaces, you can use hello [Get-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespace), [New-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespace), [Remove-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespace), and [Set-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespace) cmdlets.</span></span>

<span data-ttu-id="4be05-120">В этом примере создается несколько локальных переменных в сценарии hello; `$Namespace` и `$Location`.</span><span class="sxs-lookup"><span data-stu-id="4be05-120">This example creates a few local variables in hello script; `$Namespace` and `$Location`.</span></span>

* <span data-ttu-id="4be05-121">`$Namespace`— Имя пространства имен Service Bus hello, с которым мы хотим toowork hello.</span><span class="sxs-lookup"><span data-stu-id="4be05-121">`$Namespace` is hello name of hello Service Bus namespace with which we want toowork.</span></span>
* <span data-ttu-id="4be05-122">`$Location`Идентифицирует hello центр обработки данных, в котором мы подготовит hello пространства имен.</span><span class="sxs-lookup"><span data-stu-id="4be05-122">`$Location` identifies hello data center in which will we provision hello namespace.</span></span>
* <span data-ttu-id="4be05-123">`$CurrentNamespace`хранит ссылку hello пространство имен, которое мы извлечения (или создайте).</span><span class="sxs-lookup"><span data-stu-id="4be05-123">`$CurrentNamespace` stores hello reference namespace that we retrieve (or create).</span></span>

<span data-ttu-id="4be05-124">В фактическом сценарии переменные `$Namespace` и `$Location` могут передаваться как параметры.</span><span class="sxs-lookup"><span data-stu-id="4be05-124">In an actual script, `$Namespace` and `$Location` can be passed as parameters.</span></span>

<span data-ttu-id="4be05-125">Эта часть скрипта hello hello следующие:</span><span class="sxs-lookup"><span data-stu-id="4be05-125">This part of hello script does hello following:</span></span>

1. <span data-ttu-id="4be05-126">Попыток tooretrieve пространство имен Service Bus с hello заданное имя.</span><span class="sxs-lookup"><span data-stu-id="4be05-126">Attempts tooretrieve a Service Bus namespace with hello specified name.</span></span>
2. <span data-ttu-id="4be05-127">Если hello пространства имен, он сообщает, что был найден.</span><span class="sxs-lookup"><span data-stu-id="4be05-127">If hello namespace is found, it reports what was found.</span></span>
3. <span data-ttu-id="4be05-128">Если пространство имен hello не найден, он создает пространство имен hello и затем извлекает hello вновь создано и пространство имен.</span><span class="sxs-lookup"><span data-stu-id="4be05-128">If hello namespace is not found, it creates hello namespace and then retrieves hello newly created namespace.</span></span>
   
    ``` powershell
    # Query toosee if hello namespace currently exists
    $CurrentNamespace = Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
   
    # Check if hello namespace already exists or needs toobe created
    if ($CurrentNamespace)
    {
        Write-Host "hello namespace $Namespace already exists in hello $Location region:"
        # Report what was found
        Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
    }
    else
    {
        Write-Host "hello $Namespace namespace does not exist."
        Write-Host "Creating hello $Namespace namespace in hello $Location region..."
        New-AzureRmServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace -Location $Location
        $CurrentNamespace = Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
        Write-Host "hello $Namespace namespace in Resource Group $ResGrpName in hello $Location region has been successfully created."
                
    }
    ```

### <a name="create-a-namespace-authorization-rule"></a><span data-ttu-id="4be05-129">Создание правила авторизации для пространства имен</span><span class="sxs-lookup"><span data-stu-id="4be05-129">Create a namespace authorization rule</span></span>

<span data-ttu-id="4be05-130">Hello следующем примере показано, как с помощью правила авторизации пространства имен toomanage hello [New AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespaceauthorizationrule), [Get-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespaceauthorizationrule), [Набор AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespaceauthorizationrule), и [командлеты Remove-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespaceauthorizationrule).</span><span class="sxs-lookup"><span data-stu-id="4be05-130">hello following example shows how toomanage namespace authorization rules using hello [New-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespaceauthorizationrule), [Get-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespaceauthorizationrule), [Set-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespaceauthorizationrule), and [Remove-AzureRmServiceBusNamespaceAuthorizationRule cmdlets](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespaceauthorizationrule).</span></span>

```powershell
# Query toosee if rule exists
$CurrentRule = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule

# Check if hello rule already exists or needs toobe created
if ($CurrentRule)
{
    Write-Host "hello $AuthRule rule already exists for hello namespace $Namespace."
}
else
{
    Write-Host "hello $AuthRule rule does not exist."
    Write-Host "Creating hello $AuthRule rule for hello $Namespace namespace..."
    New-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule -Rights @("Listen","Send")
    $CurrentRule = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
    Write-Host "hello $AuthRule rule for hello $Namespace namespace has been successfully created."

    Write-Host "Setting rights on hello namespace"
    $authRuleObj = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule

    Write-Host "Remove Send rights"
    $authRuleObj.Rights.Remove("Send")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj

    Write-Host "Add Send and Manage rights toohello namespace"
    $authRuleObj.Rights.Add("Send")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj
    $authRuleObj.Rights.Add("Manage")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj

    Write-Host "Show value of primary key"
    $CurrentKey = Get-AzureRmServiceBusNamespaceKey -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
        
    Write-Host "Remove this authorization rule"
    Remove-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
}
```

## <a name="create-a-queue"></a><span data-ttu-id="4be05-131">Создание очереди</span><span class="sxs-lookup"><span data-stu-id="4be05-131">Create a queue</span></span>

<span data-ttu-id="4be05-132">toocreate очереди или раздела, выполните проверку пространства имен, с помощью скрипта hello в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="4be05-132">toocreate a queue or topic, perform a namespace check using hello script in hello previous section.</span></span> <span data-ttu-id="4be05-133">Затем создайте hello очереди:</span><span class="sxs-lookup"><span data-stu-id="4be05-133">Then, create hello queue:</span></span>

```powershell
# Check if queue already exists
$CurrentQ = Get-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName

if($CurrentQ)
{
    Write-Host "hello queue $QueueName already exists in hello $Location region:"
}
else
{
    Write-Host "hello $QueueName queue does not exist."
    Write-Host "Creating hello $QueueName queue in hello $Location region..."
    New-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -EnablePartitioning $True
    $CurrentQ = Get-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName
    Write-Host "hello $QueueName queue in Resource Group $ResGrpName in hello $Location region has been successfully created."
}
```

### <a name="modify-queue-properties"></a><span data-ttu-id="4be05-134">Изменение свойств очереди</span><span class="sxs-lookup"><span data-stu-id="4be05-134">Modify queue properties</span></span>

<span data-ttu-id="4be05-135">После выполнения скрипта hello в hello предшествующий раздела можно использовать hello [AzureRmServiceBusQueue набор](/powershell/module/azurerm.servicebus/set-azurermservicebusqueue) командлет tooupdate hello свойства очереди, как следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="4be05-135">After executing hello script in hello preceding section, you can use hello [Set-AzureRmServiceBusQueue](/powershell/module/azurerm.servicebus/set-azurermservicebusqueue) cmdlet tooupdate hello properties of a queue, as in hello following example:</span></span>

```powershell
$CurrentQ.DeadLetteringOnMessageExpiration = $True
$CurrentQ.MaxDeliveryCount = 7
$CurrentQ.MaxSizeInMegabytes = 2048
$CurrentQ.EnableExpress = $True

Set-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -QueueObj $CurrentQ
```

## <a name="provisioning-other-service-bus-entities"></a><span data-ttu-id="4be05-136">Подготовка других сущностей Service Bus</span><span class="sxs-lookup"><span data-stu-id="4be05-136">Provisioning other Service Bus entities</span></span>

<span data-ttu-id="4be05-137">Можно использовать hello [модуля Service Bus PowerShell](/powershell/module/azurerm.servicebus) tooprovision другие сущности, такие как разделы и подписки.</span><span class="sxs-lookup"><span data-stu-id="4be05-137">You can use hello [Service Bus PowerShell module](/powershell/module/azurerm.servicebus) tooprovision other entities, such as topics and subscriptions.</span></span> <span data-ttu-id="4be05-138">Эти командлеты являются синтаксически аналогичные командлеты создания очереди toohello, показанный в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="4be05-138">These cmdlets are syntactically similar toohello queue creation cmdlets demonstrated in hello previous section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4be05-139">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4be05-139">Next steps</span></span>

- <span data-ttu-id="4be05-140">В документации hello завершения PowerShell диспетчера ресурсов шины службы модуля [здесь](/powershell/module/azurerm.servicebus).</span><span class="sxs-lookup"><span data-stu-id="4be05-140">See hello complete Service Bus Resource Manager PowerShell module documentation [here](/powershell/module/azurerm.servicebus).</span></span> <span data-ttu-id="4be05-141">На этой странице перечислены все доступные командлеты.</span><span class="sxs-lookup"><span data-stu-id="4be05-141">This page lists all available cmdlets.</span></span>
- <span data-ttu-id="4be05-142">Сведения об использовании шаблонов диспетчера ресурсов Azure см. в статье hello [ресурсы создать Service Bus с помощью шаблонов диспетчера ресурсов Azure](service-bus-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4be05-142">For information about using Azure Resource Manager templates, see hello article [Create Service Bus resources using Azure Resource Manager templates](service-bus-resource-manager-overview.md).</span></span>
- <span data-ttu-id="4be05-143">Сведения о [библиотеках управления служебной шины .NET](service-bus-management-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="4be05-143">Information about [Service Bus .NET management libraries](service-bus-management-libraries.md).</span></span>

<span data-ttu-id="4be05-144">Существует несколько альтернативных способов toomanage сущностей служебной шины, как описано в следующих записях блогов:</span><span class="sxs-lookup"><span data-stu-id="4be05-144">There are some alternate ways toomanage Service Bus entities, as described in these blog posts:</span></span>

* [<span data-ttu-id="4be05-145">Как toocreate Service Bus очередей, разделов и подписок с помощью сценария PowerShell</span><span class="sxs-lookup"><span data-stu-id="4be05-145">How toocreate Service Bus queues, topics and subscriptions using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [<span data-ttu-id="4be05-146">Как toocreate в пространство имен служебной шины и концентратор событий с помощью сценария PowerShell</span><span class="sxs-lookup"><span data-stu-id="4be05-146">How toocreate a Service Bus Namespace and an Event Hub using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)
* [<span data-ttu-id="4be05-147">Сценарии PowerShell для Service Bus</span><span class="sxs-lookup"><span data-stu-id="4be05-147">Service Bus PowerShell Scripts</span></span>](https://code.msdn.microsoft.com/Service-Bus-PowerShell-a46b7059)

<!--Anchors-->

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
