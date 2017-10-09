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
# <a name="use-powershell-toomanage-event-hubs-resources"></a>Использовать ресурсы концентраторов событий toomanage PowerShell

Microsoft Azure PowerShell — это среда сценариев, можно использовать toocontrol и автоматизации развертывания hello и управления службами Azure. В этой статье описывается как toouse hello [модуль PowerShell диспетчера ресурсов концентраторов событий](/powershell/module/azurerm.eventhub) tooprovision и управлять сущностями концентраторов событий (пространства имен, концентраторы отдельных событий и групп потребителей) с помощью локальной консоли Azure PowerShell или скрипт.

Вы также можете управлять ресурсами концентраторов событий с помощью шаблонов Azure Resource Manager. Дополнительные сведения см. в статье hello [создать пространство имен концентраторов событий с концентратором и потребитель группа событий с помощью шаблона Azure Resource Manager](event-hubs-resource-manager-namespace-event-hub.md).

## <a name="prerequisites"></a>Предварительные требования

Прежде чем начать, необходимо иметь следующие hello:

* Подписка Azure. Дополнительные сведения о получении подписки см. на страницах [Как приобрести Azure][purchase options], [Предложения для участников][member offers] или [Создайте бесплатную учетную запись Azure уже сегодня][free account].
* Компьютер с Azure PowerShell. Инструкции см. в статье [Приступая к работе с командлетами Azure PowerShell](/powershell/azure/get-started-azureps).
* Общее представление о сценарии PowerShell, пакеты NuGet и hello .NET Framework.

## <a name="get-started"></a>Начало работы

Hello первым шагом является toouse toolog PowerShell в tooyour учетная запись Azure и подписку Azure. Следуйте инструкциям в разделе hello [приступить к работе с помощью командлетов Azure PowerShell](/powershell/azure/get-started-azureps) toolog в tooyour учетная запись Azure, затем извлекается и получить доступ к ресурсам hello в вашей подписке Azure.

## <a name="provision-an-event-hubs-namespace"></a>Подготовка пространства имен концентраторов событий

При работе с пространствами имен концентраторов событий можно использовать hello [Get AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/get-azurermeventhubnamespace), [New AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/new-azurermeventhubnamespace), [AzureRmEventHubNamespace удаление](/powershell/module/azurerm.eventhub/remove-azurermeventhubnamespace) , и [AzureRmEventHubNamespace набор](/powershell/module/azurerm.eventhub/set-azurermeventhubnamespace) командлетов.

В этом примере создается несколько локальных переменных в сценарии hello; `$Namespace` и `$Location`.

* `$Namespace`— Имя пространства имен hello концентраторов событий, с которым мы хотим toowork hello.
* `$Location`Идентифицирует hello центр обработки данных, в котором мы подготовит hello пространства имен.
* `$CurrentNamespace`хранит ссылку hello пространство имен, которое мы извлечения (или создайте).

В фактическом сценарии переменные `$Namespace` и `$Location` могут передаваться как параметры.

Эта часть скрипта hello hello следующие:

1. Попыток tooretrieve пространстве имен концентраторы событий с hello заданное имя.
2. Если hello пространства имен, он сообщает, что был найден.
3. Если пространство имен hello не найден, он создает пространство имен hello и затем извлекает hello вновь создано и пространство имен.

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

## <a name="create-an-event-hub"></a>Создание концентратора событий

toocreate концентратора событий, выполните проверку пространства имен, с помощью скрипта hello в предыдущем разделе hello. Затем с помощью hello [New AzureRmEventHub](/powershell/module/azurerm.eventhub/new-azurermeventhub) концентратора событий hello toocreate командлета:

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

### <a name="create-a-consumer-group"></a>Создание группы потребителей

toocreate группы потребителей в концентраторе событий проверки hello пространства имен и события концентратора с помощью сценариев hello в предыдущем разделе hello. Затем с помощью hello [New AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/new-azurermeventhubconsumergroup) группы потребителей hello toocreate командлета в концентраторе событий hello. Например:

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

#### <a name="set-user-metadata"></a>Определение метаданных пользователей

После выполнения скриптов hello в предыдущих разделах hello, можно использовать hello [AzureRmEventHubConsumerGroup набор](/powershell/module/azurerm.eventhub/set-azurermeventhubconsumergroup) командлет tooupdate hello свойств группы потребителей, как следующий пример hello:

```powershell
# Set some user metadata on hello CG
Write-Host "Setting hello UserMetadata field too'Testing'"
Set-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName -UserMetadata "Testing"
# Show result
Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
```

## <a name="remove-event-hub"></a>Удаление концентратора событий

концентраторы событий hello tooremove был создан, можно использовать hello `Remove-*` командлеты, как следующий пример hello:

```powershell
# Clean up
Remove-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
Remove-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
Remove-AzureRmEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
```

## <a name="next-steps"></a>Дальнейшие действия

- В документации hello завершения PowerShell диспетчера ресурсов концентраторов событий модуля [здесь](/powershell/module/azurerm.eventhub). На этой странице перечислены все доступные командлеты.
- Сведения об использовании шаблонов диспетчера ресурсов Azure см. в статье hello [создать пространство имен концентраторов событий с концентратором и потребитель группа событий с помощью шаблона Azure Resource Manager](event-hubs-resource-manager-namespace-event-hub.md).
- Сведения о [библиотеках управления .NET для концентраторов событий](event-hubs-management-libraries.md).

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
