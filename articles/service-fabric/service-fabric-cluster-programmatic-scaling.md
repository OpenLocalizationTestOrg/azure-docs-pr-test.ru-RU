---
title: "Масштабирование программный структуры службы aaaAzure | Документы Microsoft"
description: "Масштабировать кластер Azure Service Fabric in или out программными средствами, в соответствии с toocustom триггеров"
services: service-fabric
documentationcenter: .net
author: mjrousos
manager: jonjung
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: mikerou
ms.openlocfilehash: a0c6499b1a143a173006248cf8a15380632637e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-service-fabric-cluster-programmatically"></a>Программное масштабирование кластера Service Fabric 

Основы масштабирования кластера Service Fabric в Azure рассматриваются в статье [Масштабирование кластера Service Fabric с помощью правил автомасштабирования](./service-fabric-cluster-scale-up-down.md). В этой статье описано устройство кластеров Service Fabric, состоящих из масштабируемых наборов виртуальных машин. Масштабирование этих кластеров может выполняться вручную или с помощью правил автомасштабирования. В текущем документе рассматриваются программные методы выполнения операций масштабирования Azure для более сложных сценариев. 

## <a name="reasons-for-programmatic-scaling"></a>Причины для программного масштабирования
В большинстве сценариев масштабирование вручную или с помощью правил автомасштабирования — это оптимальное решение. В других сценариях, они нельзя прямо размеру hello. Потенциальные недостатки toothese подходы включают в себя:

- Масштабирование вручную требует toolog в явно запрос и масштабирования операций. Если операции масштабирования нужно выполнять часто или в непредвиденные моменты, этот подход может оказаться не лучшим решением.
- Если правил автоматического масштабирования удалить экземпляр из набора масштабирования виртуальных машин, они не удаляется автоматически знаний этого узла из кластера Service Fabric hello связанные Если тип узла hello имеет уровень устойчивости серебряные и золотые. Поскольку правил автоматического масштабирования работают в масштабе hello, установите уровень (а не на уровне Service Fabric hello), правил автоматического масштабирования можно удалить узлы Service Fabric без верного завершения их работы. При таком грубом удалении узла остается фантомное состояние узла Service Fabric после операций уменьшения масштаба. Лицо (или службы), должны tooperiodically очистки состояния удаленный узел в кластер Service Fabric hello.
  - Обратите внимание, что на узлах с уровнем устойчивости Gold или Silver удаленные узлы очищаются автоматически.  
- Правила автомасштабирования поддерживают [многие метрики](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md), но их число все еще ограниченно. Если в вашем сценарии требуется масштабирование на основе метрики, которой нет в этом наборе, правила автомасштабирования могут оказаться не самым подходящим вариантом.

На основании этих ограничений, вы можете tooimplement более пользовательские автоматического масштабирования модели. 

## <a name="scaling-apis"></a>Масштабирование API-интерфейсов
Существуют Azure интерфейсы API, которая разрешает tooprogrammatically работы приложений с кластера Service Fabric и наборы масштабирования виртуальных машин. Если существующие параметры автоматического масштабирования не работает для вашего сценария, эти API-интерфейсы позволяют возможных tooimplement пользовательской логики масштабирования. 

Одним из подходов tooimplementing это «домашняя сделанное» автоматическое масштабирование функциональности является tooadd новый без отслеживания состояния службы toohello Service Fabric приложения toomanage масштабирования операций. В службе hello `RunAsync` метода набора триггеров можно определить необходимость масштабирования (включая проверки параметров, таких как максимальный размер кластера и масштабирование cooldowns).   

Hello API, используемый для взаимодействия на набор масштабирования виртуальной машины (оба toocheck hello текущее количество экземпляров виртуальных машин и toomodify его) — hello [fluent вычислений Azure управления библиотеки](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/). Библиотека fluent вычислений Hello предоставляет простые в использовании API для взаимодействия с наборы масштабирования виртуальных машин.

использовать toointeract с кластером Service Fabric hello, [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient).

Конечно, масштабирование кода hello не требует toorun как служба в масштабировании toobe кластера hello. Оба `IAzure` и `FabricClient` tootheir связанные ресурсы Azure удаленного подключения, поэтому hello масштабирование службы может легко консольное приложение или служба Windows запущена из приложения вне hello Service Fabric. 

## <a name="credential-management"></a>Управление учетными данными
Одна из проблем написания масштабирование службы toohandle: hello службы должно иметь ресурсы набор масштабирования виртуальной машины может tooaccess без интерактивного входа в систему. Доступ к hello Service Fabric кластера очень просто изменяет собственное приложение Service Fabric hello масштабирование службы, но учетные данные, необходимые tooaccess hello набора масштабирования. toolog в использовании [участника-службы](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure) созданными hello [Azure CLI 2.0](https://github.com/azure/azure-cli).

Можно создать участника службы с hello следующие шаги:

1. Войдите в Azure CLI toohello (`az login`) как пользователя с масштабирования виртуальных машин доступа toohello задать
2. Создание участника с помощью службы hello`az ad sp create-for-rbac`
    1. Запишите appId hello (называемые «идентификатор клиента» в другом месте), имя, пароль и клиента для последующего использования.
    2. Также вам понадобится идентификатор подписки, который можно просмотреть с помощью `az account list`.

Hello библиотеки fluent вычислений можно войти в систему с эти учетные данные следующим образом (Обратите внимание, что core fluent Azure типов, таких как `IAzure` в hello [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/) пакет):

```C#
var credentials = new AzureCredentials(new ServicePrincipalLoginInformation {
                ClientId = AzureClientId,
                ClientSecret = 
                AzureClientKey }, AzureTenantId, AzureEnvironment.AzureGlobalCloud);
IAzure AzureClient = Azure.Authenticate(credentials).WithSubscription(AzureSubscriptionId);

if (AzureClient?.SubscriptionId == AzureSubscriptionId)
{
    ServiceEventSource.Current.ServiceMessage(Context, "Successfully logged into Azure");
}
else
{
    ServiceEventSource.Current.ServiceMessage(Context, "ERROR: Failed toologin tooAzure");
}
```

После входа в систему можно запросить подсчет экземпляров масштабируемого набора с помощью `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`.

## <a name="scaling-out"></a>Развертывание
С помощью плавного hello вычислений Azure SDK, экземпляры могут добавляться набор с несколькими вызовами - масштабирования виртуальных машин toohello

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);
var newCapacity = (int)Math.Min(MaximumNodeCount, scaleSet.Capacity + 1);
scaleSet.Update().WithCapacity(newCapacity).Apply(); 
``` 

Кроме того, размер масштабируемого набора виртуальных машин можно изменить с помощью командлетов PowerShell. [`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss)можно получить объект набора масштабирования виртуальной машины hello. текущая емкость Hello будет храниться в hello `.sku.capacity` свойство. После изменения toohello емкости hello необходимое значение, можно обновить набор в Azure масштабирования виртуальных машин hello hello [ `Update-AzureRmVmss` ](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss) команды.

Как при добавлении узла вручную, добавляя экземпляр набора масштабирования должно быть Service Fabric новый узел, поскольку hello в наборе шаблон включает в себя все с необходимые toostart tooautomatically расширения Присоединение нового кластера Service Fabric toohello экземпляров. 

## <a name="scaling-in"></a>Уменьшение масштаба

Масштабирование в — примерно tooscaling out. Hello фактический набор виртуальных машин масштаб изменений, практически hello таким же. Но, как было описано ранее, служба Service Fabric автоматически очищает только удаленные узлы с уровнем устойчивости Gold или Silver. Поэтому hello бронза устойчивость масштабирования в случае, при необходимости toointeract с hello Service Fabric tooshut вниз toobe узел hello удалены, а затем tooremove его состояние кластера.

Подготовка узла hello для завершения работы включает в себя поиск toobe hello узел удален (hello недавно добавленных узел) и его отключение. В случае с неначальными узлами более новые узлы можно найти с помощью сравнения `NodeInstanceId`. 

```C#
using (var client = new FabricClient())
{
    var mostRecentLiveNode = (await client.QueryManager.GetNodeListAsync())
        .Where(n => n.NodeType.Equals(NodeTypeToScale, StringComparison.OrdinalIgnoreCase))
        .Where(n => n.NodeStatus == System.Fabric.Query.NodeStatus.Up)
        .OrderByDescending(n => n.NodeInstanceId)
        .FirstOrDefault();
```

Имейте в виду, что *начальное значение* узлы Непохоже tooalways соглашению hello сначала удалить больше идентификаторов экземпляров.

После обнаружения toobe узел hello удалены могут быть деактивированы и удален с помощью hello же `FabricClient` экземпляра и hello `IAzure` экземпляр из более ранних версий.

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);

// Remove hello node from hello Service Fabric cluster
ServiceEventSource.Current.ServiceMessage(Context, $"Disabling node {mostRecentLiveNode.NodeName}");
await client.ClusterManager.DeactivateNodeAsync(mostRecentLiveNode.NodeName, NodeDeactivationIntent.RemoveNode);

// Wait (up tooa timeout) for hello node toogracefully shutdown
var timeout = TimeSpan.FromMinutes(5);
var waitStart = DateTime.Now;
while ((mostRecentLiveNode.NodeStatus == System.Fabric.Query.NodeStatus.Up || mostRecentLiveNode.NodeStatus == System.Fabric.Query.NodeStatus.Disabling) &&
        DateTime.Now - waitStart < timeout)
{
    mostRecentLiveNode = (await client.QueryManager.GetNodeListAsync()).FirstOrDefault(n => n.NodeName == mostRecentLiveNode.NodeName);
    await Task.Delay(10 * 1000);
}

// Decrement VMSS capacity
var newCapacity = (int)Math.Max(MinimumNodeCount, scaleSet.Capacity - 1); // Check min count 

scaleSet.Update().WithCapacity(newCapacity).Apply(); 
```

Как и при развертывании, можно использовать командлеты PowerShell для изменения емкости масштабируемого набора виртуальных машин, если подход с использованием скриптов предпочтительнее. После удаления экземпляра виртуальной машины hello Service Fabric состояния узла может быть удален.

```C#
await client.ClusterManager.RemoveNodeStateAsync(mostRecentLiveNode.NodeName);
```

## <a name="potential-drawbacks"></a>Потенциальные недостатки

Как показано в предшествующих фрагменты кода hello, создание масштабирования службы предоставляет наивысшую степень контроля и подлежит через приложение hello масштабирование. Это может быть полезно в сценариях, в которых необходим точный контроль над временем или способом изменения масштаба приложения. Тем не менее этот элемент управления отличается сложностью кода. При таком подходе означает, что вы должны tooown масштабирование код, который является нетривиальной.

Подход к масштабированию Service Fabric зависит от сценария. При масштабировании редко, hello возможность tooadd или удаление узлов вручную, возможно, недостаточно. Для более сложных сценариев правил автоматического масштабирования и пакеты SDK, программным путем предоставления tooscale возможность hello обеспечивают широкие возможности.

## <a name="next-steps"></a>Дальнейшие действия

использовать собственную логику автоматического масштабирования tooget ознакомиться с hello следующие основные понятия и полезные API-интерфейсы:

- [Масштабирование кластера Service Fabric с помощью правил автомасштабирования](./service-fabric-cluster-scale-up-down.md)
- [Свободные библиотеки управления Azure для .NET](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (для взаимодействия с базовыми масштабируемыми наборами виртуальных машин для кластеров Service Fabric)
- [System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (для взаимодействия с кластером Service Fabric и его узлами)
