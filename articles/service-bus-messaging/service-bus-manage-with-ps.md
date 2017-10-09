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
# <a name="use-powershell-toomanage-service-bus-resources"></a>Использование ресурсов служебной шины toomanage PowerShell

Microsoft Azure PowerShell — это среда сценариев, можно использовать toocontrol и автоматизации развертывания hello и управления службами Azure. В этой статье описывается как toouse hello [модуль диспетчера ресурсов Service Bus PowerShell](/powershell/module/azurerm.servicebus) tooprovision и управления ими сущностей служебной шины (пространства имен, очереди, разделы и подписки) с помощью локальной консоли Azure PowerShell или скрипт.

Сущностями служебной шины можно также управлять с помощью шаблонов Azure Resource Manager. Дополнительные сведения см. в статье hello [ресурсы создать Service Bus с помощью шаблонов диспетчера ресурсов Azure](service-bus-resource-manager-overview.md).

## <a name="prerequisites"></a>Предварительные требования

Прежде чем начать, необходимо иметь следующие hello:

* Подписка Azure. Дополнительные сведения о получении подписки см. на страницах [Как приобрести Azure][purchase options], [Предложения для участников][member offers] или [Создайте бесплатную учетную запись Azure уже сегодня][free account].
* Компьютер с Azure PowerShell. Инструкции см. в статье [Приступая к работе с командлетами Azure PowerShell](/powershell/azure/get-started-azureps).
* Общее представление о сценарии PowerShell, пакеты NuGet и hello .NET Framework.

## <a name="get-started"></a>Начало работы

Hello первым шагом является toouse toolog PowerShell в tooyour учетная запись Azure и подписку Azure. Следуйте инструкциям в разделе hello [приступить к работе с помощью командлетов Azure PowerShell](/powershell/azure/get-started-azureps) toolog в tooyour учетная запись Azure и получение и доступа к ресурсам hello в вашей подписке Azure.

## <a name="provision-a-service-bus-namespace"></a>Подготовка пространства имен Service Bus

При работе с пространствами имен Service Bus, можно использовать hello [Get AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespace), [New AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespace), [Remove-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespace), и [AzureRmServiceBusNamespace набор](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespace) командлетов.

В этом примере создается несколько локальных переменных в сценарии hello; `$Namespace` и `$Location`.

* `$Namespace`— Имя пространства имен Service Bus hello, с которым мы хотим toowork hello.
* `$Location`Идентифицирует hello центр обработки данных, в котором мы подготовит hello пространства имен.
* `$CurrentNamespace`хранит ссылку hello пространство имен, которое мы извлечения (или создайте).

В фактическом сценарии переменные `$Namespace` и `$Location` могут передаваться как параметры.

Эта часть скрипта hello hello следующие:

1. Попыток tooretrieve пространство имен Service Bus с hello заданное имя.
2. Если hello пространства имен, он сообщает, что был найден.
3. Если пространство имен hello не найден, он создает пространство имен hello и затем извлекает hello вновь создано и пространство имен.
   
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

### <a name="create-a-namespace-authorization-rule"></a>Создание правила авторизации для пространства имен

Hello следующем примере показано, как с помощью правила авторизации пространства имен toomanage hello [New AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespaceauthorizationrule), [Get-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespaceauthorizationrule), [Набор AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespaceauthorizationrule), и [командлеты Remove-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespaceauthorizationrule).

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

## <a name="create-a-queue"></a>Создание очереди

toocreate очереди или раздела, выполните проверку пространства имен, с помощью скрипта hello в предыдущем разделе hello. Затем создайте hello очереди:

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

### <a name="modify-queue-properties"></a>Изменение свойств очереди

После выполнения скрипта hello в hello предшествующий раздела можно использовать hello [AzureRmServiceBusQueue набор](/powershell/module/azurerm.servicebus/set-azurermservicebusqueue) командлет tooupdate hello свойства очереди, как следующий пример hello:

```powershell
$CurrentQ.DeadLetteringOnMessageExpiration = $True
$CurrentQ.MaxDeliveryCount = 7
$CurrentQ.MaxSizeInMegabytes = 2048
$CurrentQ.EnableExpress = $True

Set-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -QueueObj $CurrentQ
```

## <a name="provisioning-other-service-bus-entities"></a>Подготовка других сущностей Service Bus

Можно использовать hello [модуля Service Bus PowerShell](/powershell/module/azurerm.servicebus) tooprovision другие сущности, такие как разделы и подписки. Эти командлеты являются синтаксически аналогичные командлеты создания очереди toohello, показанный в предыдущем разделе hello.

## <a name="next-steps"></a>Дальнейшие действия

- В документации hello завершения PowerShell диспетчера ресурсов шины службы модуля [здесь](/powershell/module/azurerm.servicebus). На этой странице перечислены все доступные командлеты.
- Сведения об использовании шаблонов диспетчера ресурсов Azure см. в статье hello [ресурсы создать Service Bus с помощью шаблонов диспетчера ресурсов Azure](service-bus-resource-manager-overview.md).
- Сведения о [библиотеках управления служебной шины .NET](service-bus-management-libraries.md).

Существует несколько альтернативных способов toomanage сущностей служебной шины, как описано в следующих записях блогов:

* [Как toocreate Service Bus очередей, разделов и подписок с помощью сценария PowerShell](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [Как toocreate в пространство имен служебной шины и концентратор событий с помощью сценария PowerShell](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)
* [Сценарии PowerShell для Service Bus](https://code.msdn.microsoft.com/Service-Bus-PowerShell-a46b7059)

<!--Anchors-->

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
