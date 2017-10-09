---
title: "Статистическая обработка проводится работоспособности для объектов в aaaHow tooview Azure Service Fabric | Документы Microsoft"
description: "Описывается порядок просмотра tooquery и оценить сводной работоспособности Azure Service Fabric сущностей через запросов о работоспособности и общих запросов."
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: fa34c52d-3a74-4b90-b045-ad67afa43fe5
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: oanapl
ms.openlocfilehash: add810551cac26d2b4ff81b57d94ddd780c2cc2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="view-service-fabric-health-reports"></a>Просмотр отчетов о работоспособности Service Fabric
В платформе Azure Service Fabric используется [модель работоспособности](service-fabric-health-introduction.md) с сущностями работоспособности, на основе которых компоненты системы и модули наблюдения создают отчеты о состоянии отслеживаемых локальных условий. Hello [базе данных health store](service-fabric-health-introduction.md#health-store) агрегирует все toodetermine данных работоспособности ли сущности находятся в работоспособном состоянии.

Hello кластера автоматически заполняется работоспособности отчеты, отправляемые компонентами системы hello. Дополнительные сведения по [tootroubleshoot отчетов работоспособности системы используйте](service-fabric-understand-and-troubleshoot-with-system-health-reports.md).

Service Fabric предоставляет hello суммарный работоспособности способов tooget hello сущностей:

* [обозреватель Service Fabric](service-fabric-visualizing-your-cluster.md) или другие средства визуализации;
* запросы работоспособности (с помощью PowerShell, API или REST);
* Общие запросов, которые возвращают список сущностей, которые имеют работоспособности в качестве одного из свойств hello (с помощью PowerShell, API или REST)

такими параметрами, давайте toodemonstrate используйте локальный кластер с пятью узлами и hello [fabric: / приложения WordCount](http://aka.ms/servicefabric-wordcountapp). Hello **fabric: / WordCount** приложение содержит две службы по умолчанию, службы с отслеживанием состояния типа `WordCountServiceType`и службы без отслеживания состояния типа `WordCountWebServiceType`. После изменения hello `ApplicationManifest.xml` toorequire семь целевые реплики для службы с отслеживанием состояния hello и одну секцию. Так как существует только пять узлов в кластере hello, компоненты системы hello отчет предупреждение на hello служебного раздела, поскольку находится ниже числа целевых hello.

```xml
<Service Name="WordCountService">
<<<<<<< HEAD
    <StatefulService ServiceTypeName="WordCountServiceType" TargetReplicaSetSize="7" MinReplicaSetSize="3">
      <UniformInt64Partition PartitionCount="1" LowKey="1" HighKey="26" />
    </StatefulService>
=======
  <StatefulService ServiceTypeName="WordCountServiceType" TargetReplicaSetSize="7" MinReplicaSetSize="2">
    <UniformInt64Partition PartitionCount="[WordCountService_PartitionCount]" LowKey="1" HighKey="26" />
  </StatefulService>
>>>>>>> 5e84dbdd8e45a5d6b36f435a550b7433b873bf11
</Service>
```

## <a name="health-in-service-fabric-explorer"></a>Работоспособность в обозревателе Service Fabric
Обозреватель Service Fabric предоставляет представление visual hello кластера. На hello ниже рисунке можно видеть, что:

* Здравствуйте, приложения **fabric: / WordCount** — красным (по ошибке), так как он содержит событие ошибки, о которых сообщили **MyWatchdog** свойства hello **доступности**.
* Одна из его служб **fabric:/WordCount/WordCountService** выделена желтым (предупреждение). При настройке службы Hello семь реплик и hello кластера имеет пять узлов, поэтому не могут находиться два repicas. Несмотря на то, что это не показано, из-за системных отчета из раздела службы hello желтый `System.FM` о том, что `Partition is below target replica or instance count`. триггеры желтый секции Hello hello желтый службы.
* из-за приложения hello красный Hello кластера — красным.

Вычисление Hello использует политики по умолчанию hello манифест кластера и манифест приложения. Это строгие политики, при которых не допускаются сбои.

Представление hello кластера Service Fabric Explorer:

![Представление hello кластера Service Fabric Explorer.][1]

[1]: ./media/service-fabric-view-entities-aggregated-health/servicefabric-explorer-cluster-health.png


> [!NOTE]
> Дополнительные сведения об [обозревателе Service Fabric](service-fabric-visualizing-your-cluster.md).
>
>

## <a name="health-queries"></a>Запросы о работоспособности
Service Fabric предоставляет запросов о работоспособности для каждого hello поддерживается [типов сущностей](service-fabric-health-introduction.md#health-entities-and-hierarchy). Они доступны через API-Интерфейс, с помощью методов hello [FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet), командлеты PowerShell и REST. Эти запросы возвращают сведения о сущности hello завершения работоспособности: hello суммарный состояние работоспособности, события работоспособности сущности, дочерних состояний работоспособности (если применимо), оценки неисправностей (когда сущность hello неработоспособен) и статистики исправности дочерних элементов (когда применимо).

> [!NOTE]
> Сущности работоспособности возвращается в том случае, если она будет заполнена в базе данных health store hello. Hello объекта должен быть активной (но не удалена) и иметь отчета системы. Его родительской сущности hello цепочку иерархии также необходимо иметь отчеты системы. Если любое из этих условий не выполняется, возвращаемых запросами работоспособности hello [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception) с [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound` , показывает, почему hello сущности не возвращаются.
>
>

идентификатор сущности hello, который зависит от типа сущности hello необходимо передавать запросов о работоспособности Hello. запросы Hello принимают параметры политики работоспособности необязательно. Если указаны политики работоспособности, hello [политики работоспособности](service-fabric-health-introduction.md#health-policies) hello кластера или манифест приложения, используются для оценки. Если манифесты hello не содержит определение для политики работоспособности, политик работоспособности по умолчанию hello используются для оценки. политики работоспособности по умолчанию Hello не допускают наличие каких-либо ошибок. запросы Hello также принимает фильтры для возвращения только частичные дочерние элементы или события--hello из них, учитывают hello указанным фильтрам. Другой фильтр позволяет исключить статистики hello дочерних элементов.

> [!NOTE]
> Hello вывода фильтров на стороне сервера hello, чтобы уменьшить размер ответного сообщения hello. Рекомендуется использовать фильтры выхода hello toolimit hello данные возвращаются, а не применять фильтры на стороне клиента hello.
>
>

Данные о работоспособности сущности содержат:

* Здравствуйте, общее состояние работоспособности hello сущности. Вычисляется по hello работоспособности хранилища на основе сущности отчеты о работоспособности, дочерних состояний работоспособности (если применимо) и политики работоспособности. См. дополнительные сведения об [оценке работоспособности сущности](service-fabric-health-introduction.md#health-evaluation).  
* события работоспособности Hello hello сущности.
* Коллекция Hello состояний работоспособности всех дочерних элементов для hello сущностей, которые могут иметь дочерние элементы. состояния работоспособности Hello содержать идентификаторов сущностей и hello общее состояние работоспособности. tooget завершения работоспособности для дочернего объекта, вызвать hello запросов исправности для hello дочернего объекта типа и передать идентификатор hello дочернего элемента.
* оценки неисправностей Hello в этой точке toohello о том, что запускается hello состояние сущности hello, если hello сущность находится в неработоспособном состоянии. Hello вычисления выполняются рекурсивно, содержащий оценки работоспособности hello дочерние элементы, которые происходят в текущем состоянии работоспособности. Например, модуль наблюдения сообщил об ошибке реплики. работоспособность приложения Hello показывает неработоспособное оценку из-за неработоспособности службы tooan; Hello служба неисправна из-за tooa секции в сообщение об ошибке. раздел Hello неисправна из-за tooa реплики в сообщение об ошибке. Hello реплики неисправна из-за отчет о работоспособности toohello контрольного ошибки.
* Статистика Hello работоспособности для всех типов hello сущностей, которые имеют дочерние элементы дочерних элементов. Например работоспособность кластера показывает hello общее число приложений, служб, разделы, реплики и развертывания сущностей в кластере hello. Работоспособность службы показана hello общее число разделов и реплик в группе hello задается службы.

## <a name="get-cluster-health"></a>Получение сведений о работоспособности кластера
Возвращает hello работоспособности hello объекта кластера и содержит hello состояния работоспособности приложений и узлы (потомков hello кластера). Входные данные:

* [Необязательно] hello политика работоспособности кластера используется tooevaluate hello узлов и события кластера hello.
* [Необязательно] hello сопоставления политики работоспособности приложения, с помощью политик работоспособности hello использовать политики манифеста приложения hello toooverride.
* [Необязательно] Фильтры для событий, узлов и приложений, которые указывают, какие операции представляют интерес и должны возвращаться в результате hello (например, только ошибки или предупреждения и ошибки). Все события, узлов и приложений, используемых tooevaluate hello суммарный работоспособность, независимо от того, фильтр hello.
* [Необязательно] Фильтрация статистики исправности tooexclude.
* [Необязательно] Фильтрация tooinclude fabric: / статистику работоспособности системы в hello статистики исправности. Применяется, только если статистики исправности hello не исключаются. По умолчанию hello работоспособности Статистика включает только статистики для пользовательских приложений и не системное приложение hello.

### <a name="api"></a>API
tooget кластера работоспособности, создайте `FabricClient` и вызова hello [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) метод для его **HealthManager**.

Hello следующий вызов возвращает hello работоспособности кластера:

```csharp
ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync();
```

Hello следующий код возвращает hello работоспособности кластера с помощью политики работоспособности кластера пользовательские и фильтрует узлы и приложения. Он указывает, включать структуры hello статистики исправности hello: / статистику системы. Он создает [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription), который содержит входные данные для hello.

```csharp
var policy = new ClusterHealthPolicy()
{
    MaxPercentUnhealthyNodes = 20
};
var nodesFilter = new NodeHealthStatesFilter()
{
    HealthStateFilterValue = HealthStateFilter.Error | HealthStateFilter.Warning
};
var applicationsFilter = new ApplicationHealthStatesFilter()
{
    HealthStateFilterValue = HealthStateFilter.Error
};
var healthStatisticsFilter = new ClusterHealthStatisticsFilter()
{
    ExcludeHealthStatistics = false,
    IncludeSystemApplicationHealthStatistics = true
};
var queryDescription = new ClusterHealthQueryDescription()
{
    HealthPolicy = policy,
    ApplicationsFilter = applicationsFilter,
    NodesFilter = nodesFilter,
    HealthStatisticsFilter = healthStatisticsFilter
};

ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync(queryDescription);
```

### <a name="powershell"></a>PowerShell
командлет tooget Hello hello-состояние кластера — [Get ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth). Сначала подключите toohello кластера с помощью hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) командлета.

Hello hello кластера находится в состоянии пятью узлами, Системное приложение hello и fabric: / WordCount настроена, как описано.

Привет, выполнив командлет возвращает работоспособности кластера с помощью политики работоспособности по умолчанию. Hello общее состояние работоспособности — предупреждение, поскольку hello fabric: / приложения WordCount находится в состоянии предупреждения. Обратите внимание на то, как оценки неисправностей hello содержат сведения о hello условий, вызвавших работоспособности hello статистическая обработка.

```xml
PS D:\ServiceFabric> Get-ServiceFabricClusterHealth


AggregatedHealthState   : Warning
UnhealthyEvaluations    : 
                          Unhealthy applications: 100% (1/1), MaxPercentUnhealthyApplications=0%.
                          
                          Unhealthy application: ApplicationName='fabric:/WordCount', AggregatedHealthState='Warning'.
                          
                            Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                          
                            Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Warning'.
                          
                                Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                          
                                Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                          
                                    Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                          
                          
NodeHealthStates        : 
                          NodeName              : _Node_4
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_3
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_2
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_1
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_0
                          AggregatedHealthState : Ok
                          
ApplicationHealthStates : 
                          ApplicationName       : fabric:/System
                          AggregatedHealthState : Ok
                          
                          ApplicationName       : fabric:/WordCount
                          AggregatedHealthState : Warning
                          
HealthEvents            : None
HealthStatistics        : 
                          Node                  : 5 Ok, 0 Warning, 0 Error
                          Replica               : 6 Ok, 0 Warning, 0 Error
                          Partition             : 1 Ok, 1 Warning, 0 Error
                          Service               : 1 Ok, 1 Warning, 0 Error
                          DeployedServicePackage : 6 Ok, 0 Warning, 0 Error
                          DeployedApplication   : 5 Ok, 0 Warning, 0 Error
                          Application           : 0 Ok, 1 Warning, 0 Error
```

Hello следующий командлет PowerShell возвращает состояние hello hello кластера с помощью политики пользовательское приложение. Фильтрует результаты tooget только приложения и узлов в ошибку или предупреждение. В результате ни один узел не будет возвращен, так как все узлы работоспособны. Только hello fabric: / приложения WordCount соблюдает фильтра приложения hello. Поскольку пользовательской политики hello указывает tooconsider предупреждения как ошибки для структуры hello: / приложения WordCount, приложение hello вычисляется как ошибочное, и поэтому является hello кластера.

```powershell
PS D:\ServiceFabric> $appHealthPolicy = New-Object -TypeName System.Fabric.Health.ApplicationHealthPolicy
$appHealthPolicy.ConsiderWarningAsError = $true
$appHealthPolicyMap = New-Object -TypeName System.Fabric.Health.ApplicationHealthPolicyMap
$appUri1 = New-Object -TypeName System.Uri -ArgumentList "fabric:/WordCount"
$appHealthPolicyMap.Add($appUri1, $appHealthPolicy)
Get-ServiceFabricClusterHealth -ApplicationHealthPolicyMap $appHealthPolicyMap -ApplicationsFilter "Warning,Error" -NodesFilter "Warning,Error" -ExcludeHealthStatistics


AggregatedHealthState   : Error
UnhealthyEvaluations    : 
                          Unhealthy applications: 100% (1/1), MaxPercentUnhealthyApplications=0%.
                          
                          Unhealthy application: ApplicationName='fabric:/WordCount', AggregatedHealthState='Error'.
                          
                            Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                          
                            Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                          
                                Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                          
                                Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                          
                                    Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=true.
                          
                          
NodeHealthStates        : None
ApplicationHealthStates : 
                          ApplicationName       : fabric:/WordCount
                          AggregatedHealthState : Error
                          
HealthEvents            : None
```

### <a name="rest"></a>REST
Можно получить состояние работоспособности кластера с помощью [запрос GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster) или [запрос POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy) , включающего политики работоспособности, описанные в теле hello.

## <a name="get-node-health"></a>Получение сведений о работоспособности узла
Возвращает hello работоспособности узла сущности и содержит событий работоспособности hello, о которых сообщается в узле hello. Входные данные:

* Имя узла [обязательно] hello, указывающее узел hello.
* Параметры политики работоспособности кластера [необязательно] hello используется tooevaluate работоспособности.
* [Необязательно] Фильтровать события, указывающие, какие операции представляют интерес и должны возвращаться в результате hello (например, только ошибки или предупреждения и ошибки). Все события, используемые tooevaluate hello суммарный работоспособность, независимо от того, фильтр hello.

### <a name="api"></a>API
состояние работоспособности узла tooget через hello API, создайте `FabricClient` и вызова hello [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) метод для его HealthManager.

Hello следующий код возвращает состояние работоспособности узла hello для имени указанного узла hello:

```csharp
NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(nodeName);
```

Hello следующий код возвращает состояние работоспособности узла hello для hello указанное имя узла и передает в фильтр событий и пользовательской политики с помощью [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):

```csharp
var queryDescription = new NodeHealthQueryDescription(nodeName)
{
    HealthPolicy = new ClusterHealthPolicy() {  ConsiderWarningAsError = true },
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.Warning },
};

NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(queryDescription);
```

### <a name="powershell"></a>PowerShell
состояние работоспособности узла hello Hello командлет tooget — [Get ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth). Сначала подключите toohello кластера с помощью hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) командлета.
Привет, выполнив командлет возвращает состояние работоспособности узла hello с помощью политики работоспособности по умолчанию:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricNodeHealth _Node_1


NodeName              : _Node_1
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 3
                        SentAt                : 7/13/2017 4:39:23 PM
                        ReceivedAt            : 7/13/2017 4:40:47 PM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 4:40:47 PM, LastWarning = 1/1/0001 12:00:00 AM
```

Hello следующий командлет возвращает hello работоспособности всех узлов в кластере hello:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricNode | Get-ServiceFabricNodeHealth | select NodeName, AggregatedHealthState | ft -AutoSize

NodeName AggregatedHealthState
-------- ---------------------
_Node_4                     Ok
_Node_3                     Ok
_Node_2                     Ok
_Node_1                     Ok
_Node_0                     Ok
```

### <a name="rest"></a>REST
Можно получить состояние работоспособности узла с [запрос GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node) или [запрос POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy) , включающего политики работоспособности, описанные в теле hello.

## <a name="get-application-health"></a>Получение сведений о работоспособности приложения
Возвращает hello работоспособности приложения сущности. Он содержит состояние работоспособности hello hello развертывания приложения и службы дочерних элементов. Входные данные:

* [Обязательно] hello имя приложения (URI), идентифицирующий приложение hello.
* Политика работоспособности приложения hello [необязательно] использовать политики манифеста приложения hello toooverride.
* [Необязательно] Фильтры для событий, служб и развернутых приложений, которые указывают, какие операции представляют интерес и должны возвращаться в результате hello (например, только ошибки или предупреждения и ошибки). Все события, службы и развернутых приложений, используемых tooevaluate hello суммарный работоспособность, независимо от того, фильтр hello.
* [Необязательно] Фильтрация статистики исправности tooexclude hello. Если не указан, статистики исправности hello включают ОК hello, предупреждения и количество ошибок для всех дочерних элементов приложения: службы, разделы, реплики, развернутых приложений и развертывания пакетов служб.

### <a name="api"></a>API
работоспособность приложения tooget, создать `FabricClient` и вызова hello [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) метод для его HealthManager.

Hello следующий код возвращает работоспособности приложения hello для hello указанное имя приложения (URI):

```csharp
ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(applicationName);
```

Hello следующий код возвращает работоспособности приложения hello для hello указанное имя приложения (URI) с фильтрами и пользовательских политик указанного с помощью [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription).

```csharp
HealthStateFilter warningAndErrors = HealthStateFilter.Error | HealthStateFilter.Warning;
var serviceTypePolicy = new ServiceTypeHealthPolicy()
{
    MaxPercentUnhealthyPartitionsPerService = 0,
    MaxPercentUnhealthyReplicasPerPartition = 5,
    MaxPercentUnhealthyServices = 0,
};
var policy = new ApplicationHealthPolicy()
{
    ConsiderWarningAsError = false,
    DefaultServiceTypeHealthPolicy = serviceTypePolicy,
    MaxPercentUnhealthyDeployedApplications = 0,
};

var queryDescription = new ApplicationHealthQueryDescription(applicationName)
{
    HealthPolicy = policy,
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = warningAndErrors },
    ServicesFilter = new ServiceHealthStatesFilter() { HealthStateFilterValue = warningAndErrors },
    DeployedApplicationsFilter = new DeployedApplicationHealthStatesFilter() { HealthStateFilterValue = warningAndErrors },
};

ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(queryDescription);
```

### <a name="powershell"></a>PowerShell
Контроль работоспособности приложения hello Hello командлет tooget [Get ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps). Сначала подключите toohello кластера с помощью hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) командлета.

Hello следующий командлет возвращает hello работоспособности hello **fabric: / WordCount** приложения:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth fabric:/WordCount


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Warning
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Warning'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                                  
                                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                                  
ServiceHealthStates             : 
                                  ServiceName           : fabric:/WordCount/WordCountWebService
                                  AggregatedHealthState : Ok
                                  
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Warning
                                  
DeployedApplicationHealthStates : 
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_4
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_3
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_0
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_2
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_1
                                  AggregatedHealthState : Ok
                                  
HealthEvents                    : 
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 282
                                  SentAt                : 7/13/2017 5:57:05 PM
                                  ReceivedAt            : 7/13/2017 5:57:05 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 7/13/2017 5:57:05 PM, LastWarning = 1/1/0001 12:00:00 AM
                                  
HealthStatistics                : 
                                  Replica               : 6 Ok, 0 Warning, 0 Error
                                  Partition             : 1 Ok, 1 Warning, 0 Error
                                  Service               : 1 Ok, 1 Warning, 0 Error
                                  DeployedServicePackage : 6 Ok, 0 Warning, 0 Error
                                  DeployedApplication   : 5 Ok, 0 Warning, 0 Error
```

Здравствуйте, следующие передает командлет PowerShell в пользовательских политик. Кроме того, он выполняет фильтрацию дочерних элементов и событий.

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth -ApplicationName fabric:/WordCount -ConsiderWarningAsError $true -ServicesFilter Error -EventsFilter Error -DeployedApplicationsFilter Error -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                                  
                                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=true.
                                  
ServiceHealthStates             : 
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Error
                                  
DeployedApplicationHealthStates : None
HealthEvents                    : None
```

### <a name="rest"></a>REST
Вы можете получить работоспособности приложения с помощью [запрос GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application) или [запрос POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy) , включающего политики работоспособности, описанные в теле hello.

## <a name="get-service-health"></a>Получение сведений о работоспособности службы
Возвращает работоспособности hello объекта службы. Он содержит состояния работоспособности hello секции. Входные данные:

* [Обязательно] hello имя службы (URI), определяющий службу hello.
* Политика работоспособности приложения hello [необязательно] используется политика манифеста приложения hello toooverride.
* [Необязательно] Фильтры для событий и секции, которые указывают, какие операции представляют интерес и должны возвращаться в результате hello (например, только ошибки или предупреждения и ошибки). Все события и секций, используемых tooevaluate hello суммарный работоспособность, независимо от того, фильтр hello.
* [Необязательно] Фильтрация статистики исправности tooexclude. Если не указан, hello hello Показать статистику работоспособности ОК, предупреждения и ошибки подсчета для всех секций и реплик службы hello.

### <a name="api"></a>API
работоспособность службы tooget через hello API, создайте `FabricClient` и вызова hello [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) метод для его HealthManager.

Hello следующий пример возвращает hello работоспособности службы с указанным именем службы (URI):

```charp
ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(serviceName);
```

Hello следующий код возвращает работоспособность службы hello hello указанное имя службы (URI), указывая фильтры и пользовательской политики через [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):

```csharp
var queryDescription = new ServiceHealthQueryDescription(serviceName)
{
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.All },
    PartitionsFilter = new PartitionHealthStatesFilter() { HealthStateFilterValue = HealthStateFilter.Error },
};

ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(queryDescription);
```

### <a name="powershell"></a>PowerShell
работоспособность службы hello tooget командлет Hello — [Get ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth). Сначала подключите toohello кластера с помощью hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) командлета.

Привет, выполнив командлет возвращает hello службы работоспособности с помощью политики работоспособности по умолчанию:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricServiceHealth -ServiceName fabric:/WordCount/WordCountService


ServiceName           : fabric:/WordCount/WordCountService
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                        
                        Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                        
                            Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
PartitionHealthStates : 
                        PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
                        AggregatedHealthState : Warning
                        
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 15
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Service has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                        
HealthStatistics      : 
                        Replica               : 5 Ok, 0 Warning, 0 Error
                        Partition             : 0 Ok, 1 Warning, 0 Error
```

### <a name="rest"></a>REST
Можно получить состояние работоспособности службы с [запрос GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service) или [запрос POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy) , включающего политики работоспособности, описанные в теле hello.

## <a name="get-partition-health"></a>Получение сведений о работоспособности раздела
Возвращает работоспособности hello объекта секции. Он содержит состояния работоспособности реплики hello. Входные данные:

* Секции [обязательно] hello идентификатор (GUID), который идентифицирует секцию hello.
* Политика работоспособности приложения hello [необязательно] используется политика манифеста приложения hello toooverride.
* [Необязательно] Фильтры для событий и реплик, которые указывают, какие операции представляют интерес и должны возвращаться в результате hello (например, только ошибки или предупреждения и ошибки). Все события и реплики представляют используется tooevaluate hello суммарный работоспособность, независимо от того, фильтр hello.
* [Необязательно] Фильтрация статистики исправности tooexclude. Если не указан, Статистика работоспособности hello показывает, сколько реплики находятся в ОК, предупреждения и ошибки состояния.

### <a name="api"></a>API
Создание работоспособности раздела tooget через API, hello `FabricClient` и вызова hello [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) метод для его HealthManager. Создание toospecify необязательные параметры, [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription).

```csharp
PartitionHealth partitionHealth = await fabricClient.HealthManager.GetPartitionHealthAsync(partitionId);
```

### <a name="powershell"></a>PowerShell
— работоспособности раздела hello tooget командлет Hello [Get ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth). Сначала подключите toohello кластера с помощью hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) командлета.

Hello следующий командлет возвращает hello работоспособности для всех секций hello **fabric: / WordCount/WordCountService** службы и отфильтровывает состояния работоспособности реплики:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricPartitionHealth -ReplicasFilter None

PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Warning
                        SequenceNumber        : 72
                        SentAt                : 7/13/2017 5:57:29 PM
                        ReceivedAt            : 7/13/2017 5:57:48 PM
                        TTL                   : Infinite
                        Description           : Partition is below target replica or instance count.
                        fabric:/WordCount/WordCountService 7 2 af2e3e44-a8f8-45ac-9f31-4093eb897600
                          N/P RD _Node_2 Up 131444422260002646
                          N/S RD _Node_4 Up 131444422293113678
                          N/S RD _Node_3 Up 131444422293113679
                          N/S RD _Node_1 Up 131444422293118720
                          N/S RD _Node_0 Up 131444422293118721
                          (Showing 5 out of 5 replicas. Total available replicas: 5.)
                        
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Ok->Warning = 7/13/2017 5:57:48 PM, LastError = 1/1/0001 12:00:00 AM
                        
                        SourceId              : System.PLB
                        Property              : ServiceReplicaUnplacedHealth_Secondary_af2e3e44-a8f8-45ac-9f31-4093eb897600
                        HealthState           : Warning
                        SequenceNumber        : 131444445174851664
                        SentAt                : 7/13/2017 6:35:17 PM
                        ReceivedAt            : 7/13/2017 6:35:18 PM
                        TTL                   : 00:01:05
                        Description           : hello Load Balancer was unable toofind a placement for one or more of hello Service's Replicas:
                        Secondary replica could not be placed due toohello following constraints and properties:  
                        TargetReplicaSetSize: 7
                        Placement Constraint: N/A
                        Parent Service: N/A
                        
                        Constraint Elimination Sequence:
                        Existing Secondary Replicas eliminated 4 possible node(s) for placement -- 1/5 node(s) remain.
                        Existing Primary Replica eliminated 1 possible node(s) for placement -- 0/5 node(s) remain.
                        
                        Nodes Eliminated By Constraints:
                        
                        Existing Secondary Replicas -- Nodes with Partition's Existing Secondary Replicas/Instances:
                        --
                        FaultDomain:fd:/4 NodeName:_Node_4 NodeType:NodeType4 UpgradeDomain:4 UpgradeDomain: ud:/4 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/3 NodeName:_Node_3 NodeType:NodeType3 UpgradeDomain:3 UpgradeDomain: ud:/3 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/1 NodeName:_Node_1 NodeType:NodeType1 UpgradeDomain:1 UpgradeDomain: ud:/1 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/0 NodeName:_Node_0 NodeType:NodeType0 UpgradeDomain:0 UpgradeDomain: ud:/0 Deactivation Intent/Status: None/None
                        
                        Existing Primary Replica -- Nodes with Partition's Existing Primary Replica or Secondary Replicas:
                        --
                        FaultDomain:fd:/2 NodeName:_Node_2 NodeType:NodeType2 UpgradeDomain:2 UpgradeDomain: ud:/2 Deactivation Intent/Status: None/None
                        
                        
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/13/2017 5:57:48 PM, LastOk = 1/1/0001 12:00:00 AM
                        
HealthStatistics      : 
                        Replica               : 5 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a>REST
Можно получить состояние работоспособности раздела с [запрос GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition) или [запрос POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy) , включающего политики работоспособности, описанные в теле hello.

## <a name="get-replica-health"></a>Получение сведений о работоспособности реплики
Возвращает hello работоспособности реплики службы с отслеживанием состояния или экземпляра службы без отслеживания состояния. Входные данные:

* [Обязательно] hello секции идентификатор (GUID) и реплика идентификатор, определяющий hello реплики.
* Параметры политики работоспособности приложения hello [необязательно] использовать политики манифеста приложения hello toooverride.
* [Необязательно] Фильтровать события, указывающие, какие операции представляют интерес и должны возвращаться в результате hello (например, только ошибки или предупреждения и ошибки). Все события, используемые tooevaluate hello суммарный работоспособность, независимо от того, фильтр hello.

### <a name="api"></a>API
создать работоспособности реплики hello tooget через API, hello `FabricClient` и вызова hello [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) метод для его HealthManager. дополнительных параметров, используйте toospecify [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription).

```csharp
ReplicaHealth replicaHealth = await fabricClient.HealthManager.GetReplicaHealthAsync(partitionId, replicaId);
```

### <a name="powershell"></a>PowerShell
Hello командлет tooget hello реплики находятся в [Get ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth). Сначала подключите toohello кластера с помощью hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) командлета.

Hello следующий командлет возвращает работоспособности hello hello первичной реплики для всех секций hello службы:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricReplica | where {$_.ReplicaRole -eq "Primary"} | Get-ServiceFabricReplicaHealth


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422260002646
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131444422263668344
                        SentAt                : 7/13/2017 5:57:06 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_2
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a>REST
Можно получить состояние работоспособности реплики с [запрос GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica) или [запрос POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy) , включающего политики работоспособности, описанные в теле hello.

## <a name="get-deployed-application-health"></a>Получение сведений о работоспособности развернутого приложения
Работоспособность hello возвращает приложение, развернутое в сущности узла. Он содержит состояния работоспособности пакета службы развернуты hello. Входные данные:

* Имя приложения hello [обязательно] (URI) и имя узла (string), определяющие hello развернутого приложения.
* Политика работоспособности приложения hello [необязательно] использовать политики манифеста приложения hello toooverride.
* [Необязательно] Фильтры для событий и развернутые пакеты служб, указывающие, какие операции представляют интерес и должны возвращаться в результате hello (например, только ошибки или предупреждения и ошибки). Все события и развернутые пакеты служб, используемых tooevaluate hello суммарный работоспособность, независимо от того, фильтр hello.
* [Необязательно] Фильтрация статистики исправности tooexclude. Если не указан, статистики исправности hello показывают hello количество развернутым пакетам в ОК, предупреждения и ошибки состояния работоспособности.

### <a name="api"></a>API
работоспособность hello tooget приложение, развернутое на узле через hello API, создайте `FabricClient` и вызова hello [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) метод для его HealthManager. toospecify необязательные параметры, используйте [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription).

```csharp
DeployedApplicationHealth health = await fabricClient.HealthManager.GetDeployedApplicationHealthAsync(
    new DeployedApplicationHealthQueryDescription(applicationName, nodeName));
```

### <a name="powershell"></a>PowerShell
Hello работоспособности приложения hello развернут tooget командлета — [Get ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps). Сначала подключите toohello кластера с помощью hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) командлета. toofind, где развертывается приложение, запустите [Get ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) и рассмотрим hello развернутых приложений дочерних элементов.

Hello следующий командлет возвращает hello работоспособности hello **fabric: / WordCount** приложение, развернутое на **_Node_2**.

```powershell
PS D:\ServiceFabric> Get-ServiceFabricDeployedApplicationHealth -ApplicationName fabric:/WordCount -NodeName _Node_0


ApplicationName                    : fabric:/WordCount
NodeName                           : _Node_0
AggregatedHealthState              : Ok
DeployedServicePackageHealthStates : 
                                     ServiceManifestName   : WordCountServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_0
                                     AggregatedHealthState : Ok
                                     
                                     ServiceManifestName   : WordCountWebServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_0
                                     AggregatedHealthState : Ok
                                     
HealthEvents                       : 
                                     SourceId              : System.Hosting
                                     Property              : Activation
                                     HealthState           : Ok
                                     SequenceNumber        : 131444422261848308
                                     SentAt                : 7/13/2017 5:57:06 PM
                                     ReceivedAt            : 7/13/2017 5:57:17 PM
                                     TTL                   : Infinite
                                     Description           : hello application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/13/2017 5:57:17 PM, LastWarning = 1/1/0001 12:00:00 AM
                                     
HealthStatistics                   : 
                                     DeployedServicePackage : 2 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a>REST
Вы можете получить состояние работоспособности развернутого приложения с [запрос GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application) или [запрос POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy) , включающего политики работоспособности, описанные в теле hello.

## <a name="get-deployed-service-package-health"></a>Получение сведений о работоспособности развернутого пакета службы
Возвращает hello работоспособности развернутой службы пакета сущности. Входные данные:

* Имя приложения hello [обязательно] (URI), имя узла (string) и имя манифеста службы (string), определяющие hello развернутого пакета службы.
* Политика работоспособности приложения hello [необязательно] используется политика манифеста приложения hello toooverride.
* [Необязательно] Фильтровать события, указывающие, какие операции представляют интерес и должны возвращаться в результате hello (например, только ошибки или предупреждения и ошибки). Все события, используемые tooevaluate hello суммарный работоспособность, независимо от того, фильтр hello.

### <a name="api"></a>API
работоспособность hello tooget к развернутому пакету служб через hello API, создайте `FabricClient` и вызова hello [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) метод для его HealthManager. toospecify необязательные параметры, используйте [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription).

```csharp
DeployedServicePackageHealth health = await fabricClient.HealthManager.GetDeployedServicePackageHealthAsync(
    new DeployedServicePackageHealthQueryDescription(applicationName, nodeName, serviceManifestName));
```

### <a name="powershell"></a>PowerShell
Hello работоспособности пакета службы развернуты hello tooget командлета — [Get ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth). Сначала подключите toohello кластера с помощью hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) командлета. toosee, где развертывается приложение, запустите [Get ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) и поиска hello развертывания приложений. toosee, которого пакеты обновления имеют в приложении, просмотрите hello развернуть дочерние элементы пакета службы в hello [Get ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps) выходных данных.

Hello следующий командлет возвращает hello работоспособности hello **WordCountServicePkg** пакет службы hello **fabric: / WordCount** приложение, развернутое на **_Node_2**. Hello сущность имеет **System.Hosting** отчеты для успешной активации пакета службы и точки входа и успешной регистрации типа службы.

```powershell
PS D:\ServiceFabric> Get-ServiceFabricDeployedApplication -ApplicationName fabric:/WordCount -NodeName _Node_2 | Get-ServiceFabricDeployedServicePackageHealth -ServiceManifestName WordCountServicePkg


ApplicationName            : fabric:/WordCount
ServiceManifestName        : WordCountServicePkg
ServicePackageActivationId : 
NodeName                   : _Node_2
AggregatedHealthState      : Ok
HealthEvents               : 
                             SourceId              : System.Hosting
                             Property              : Activation
                             HealthState           : Ok
                             SequenceNumber        : 131444422267693359
                             SentAt                : 7/13/2017 5:57:06 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : hello ServicePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : CodePackageActivation:Code:EntryPoint
                             HealthState           : Ok
                             SequenceNumber        : 131444422267903345
                             SentAt                : 7/13/2017 5:57:06 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : hello CodePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : ServiceTypeRegistration:WordCountServiceType
                             HealthState           : Ok
                             SequenceNumber        : 131444422272458374
                             SentAt                : 7/13/2017 5:57:07 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : hello ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a>REST
Вы можете получить развернутой службы работоспособности пакета с помощью [запрос GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package) или [запрос POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy) , включающего политики работоспособности, описанные в теле hello.

## <a name="health-chunk-queries"></a>Запросы фрагментов данных о работоспособности
Hello работоспособности блока запросы могут возвращать детей многоуровневого кластера (рекурсивно) в фильтры входа. Он поддерживает расширенные фильтры, позволяющие большую гибкость в выборе дочерние элементы hello toobe возвращается. Hello фильтры могут определять дочерние элементы, с уникальным идентификатором hello или другие идентификаторы группы или состояния работоспособности. По умолчанию дочерние элементы не включаются, в противоположность toohealth команды, которые всегда содержит дочерние элементы первого уровня.

Hello [запросов о работоспособности](service-fabric-view-entities-aggregated-health.md#health-queries) возврата только первого уровня дочерних элементов hello указанного лица необходимые фильтры. tooget hello дочерние элементы дочерних элементов hello, необходимо вызвать дополнительные работоспособности API-интерфейсов для каждой сущности, представляющие интерес. Аналогичным образом tooget hello работоспособности определенных сущностей, необходимо вызвать один работоспособности API для каждого нужного объекта. Hello Расширенная фильтрация запросов блоков позволяет toorequest несколько элементов в один запрос, сводя к минимуму размер сообщения hello и hello количество сообщений.

Hello hello фрагмент запроса значение можно получить состояние работоспособности для нескольких сущностей кластера (потенциально всех кластеров сущности начиная обязательный корневой) в одном вызове. Например, можно составить сложный запрос на сведения о работоспособности.

* Возвращать только приложения с ошибками и включать для таких приложений все службы с предупреждением или ошибкой. Для возвращенных служб включать все разделы.
* Возвращать только hello работоспособности четыре указанные по имени приложения.
* Возвращать только hello работоспособности приложений типа нужное приложение.
* Возвращать все развернутые сущности на узле. Возвращает все приложения все развернутые на указанном узле hello и все пакеты обновления hello развернуты на этом узле.
* Возвращать все реплики с ошибками. Возвращает все приложения, службы, разделы и только реплики с ошибками.
* Возвращать все приложения. Включить все разделы для указанной службы.

В настоящее время hello работоспособности фрагмент запроса предоставляется только для hello объекта кластера. Этот запрос возвращает фрагмент данных о работоспособности кластера, который содержит:

* состояние работоспособности кластера суммарный Hello.
* Hello работоспособности состояние фрагмента список узлов, которые учитывают фильтры входа.
* Hello работоспособности состояние фрагмента список приложений, которые учитывают фильтры входа. Каждый блок состояния работоспособности приложения содержит список блоков со всеми службами, которые используют фильтры входа и список блоков со всех развернутых приложений, которые учитывают hello фильтры. То же для детей hello служб и развернутых приложений. Таким образом, все сущности в кластере hello могут потенциально возвращаться при запросе в иерархическом виде.

### <a name="cluster-health-chunk-query"></a>Запрос фрагмента данных о работоспособности кластера
Возвращает hello работоспособности hello объекта кластера и содержит блоки состояние работоспособности иерархических hello необходимые дочерние элементы. Входные данные:

* [Необязательно] hello политика работоспособности кластера используется tooevaluate hello узлов и события кластера hello.
* [Необязательно] hello сопоставления политики работоспособности приложения, с помощью политик работоспособности hello использовать политики манифеста приложения hello toooverride.
* [Необязательно] Фильтры для узлов и приложений, которые указывают, какие операции представляют интерес и должны возвращаться в результате hello. фильтры Hello являются tooan определенной сущности или группу сущностей или применимо tooall сущности на этом уровне. Hello список фильтров может содержать один общие фильтра или фильтры для сущностей особые идентификаторы toofine фрагментов данных, возвращаемых запросом hello. Если не указано, по умолчанию hello дочерние элементы не возвращаются.
  Дополнительные сведения о фильтры hello [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) и [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter). Hello приложения фильтров может рекурсивно укажите расширенные фильтры для дочерних элементов.

результат Hello фрагмента данных включает в себя hello дочерних элементов, которые учитывают hello фильтры.

В настоящее время hello фрагмента данных запрос возвращает оценки неисправностей или события объектов. Эти дополнительные сведения можно получить с помощью hello существующего запроса работоспособности кластера.

### <a name="api"></a>API
работоспособность кластера tooget фрагмента данных, создайте `FabricClient` и вызова hello [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) метод для его **HealthManager**. Можно передать в [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) toodescribe политики работоспособности и дополнительные фильтры.

Hello следующий код возвращает фрагмент работоспособности кластера с расширенными фильтрами.

```csharp
var queryDescription = new ClusterHealthChunkQueryDescription();
queryDescription.ApplicationFilters.Add(new ApplicationHealthStateFilter()
    {
        // Return applications only if they are in error
        HealthStateFilter = HealthStateFilter.Error
    });

// Return all replicas
var wordCountServiceReplicaFilter = new ReplicaHealthStateFilter()
    {
        HealthStateFilter = HealthStateFilter.All
    };

// Return all replicas and all partitions
var wordCountServicePartitionFilter = new PartitionHealthStateFilter()
    {
        HealthStateFilter = HealthStateFilter.All
    };
wordCountServicePartitionFilter.ReplicaFilters.Add(wordCountServiceReplicaFilter);

// For specific service, return all partitions and all replicas
var wordCountServiceFilter = new ServiceHealthStateFilter()
{
    ServiceNameFilter = new Uri("fabric:/WordCount/WordCountService"),
};
wordCountServiceFilter.PartitionFilters.Add(wordCountServicePartitionFilter);

// Application filter: for specific application, return no services except hello ones of interest
var wordCountApplicationFilter = new ApplicationHealthStateFilter()
    {
        // Always return fabric:/WordCount application
        ApplicationNameFilter = new Uri("fabric:/WordCount"),
    };
wordCountApplicationFilter.ServiceFilters.Add(wordCountServiceFilter);

queryDescription.ApplicationFilters.Add(wordCountApplicationFilter);

var result = await fabricClient.HealthManager.GetClusterHealthChunkAsync(queryDescription);
```

### <a name="powershell"></a>PowerShell
командлет tooget Hello hello-состояние кластера — [Get ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk). Сначала подключите toohello кластера с помощью hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) командлета.

Hello следующий код возвращает узлы только в том случае, если они вызывают ошибки, за исключением конкретный узел, всегда должны быть возвращены.

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$nodeFilter1 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{HealthStateFilter=$errorFilter}
$nodeFilter2 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{NodeNameFilter="_Node_1";HealthStateFilter=$allFilter}
# Create node filter list that will be passed in hello cmdlet
$nodeFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.NodeHealthStateFilter]
$nodeFilters.Add($nodeFilter1)
$nodeFilters.Add($nodeFilter2)

Get-ServiceFabricClusterHealthChunk -NodeFilters $nodeFilters


HealthState                  : Warning
NodeHealthStateChunks        : 
                               TotalCount            : 1
                               
                               NodeName              : _Node_1
                               HealthState           : Ok
                               
ApplicationHealthStateChunks : None
```

Привет, выполнив командлет возвращает фрагмент кластера с фильтрами приложения.

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

# All replicas
$replicaFilter = New-Object System.Fabric.Health.ReplicaHealthStateFilter -Property @{HealthStateFilter=$allFilter}

# All partitions
$partitionFilter = New-Object System.Fabric.Health.PartitionHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$partitionFilter.ReplicaFilters.Add($replicaFilter)

# For WordCountService, return all partitions and all replicas
$svcFilter1 = New-Object System.Fabric.Health.ServiceHealthStateFilter -Property @{ServiceNameFilter="fabric:/WordCount/WordCountService"}
$svcFilter1.PartitionFilters.Add($partitionFilter)

$svcFilter2 = New-Object System.Fabric.Health.ServiceHealthStateFilter -Property @{HealthStateFilter=$errorFilter}

$appFilter = New-Object System.Fabric.Health.ApplicationHealthStateFilter -Property @{ApplicationNameFilter="fabric:/WordCount"}
$appFilter.ServiceFilters.Add($svcFilter1)
$appFilter.ServiceFilters.Add($svcFilter2)

$appFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.ApplicationHealthStateFilter]
$appFilters.Add($appFilter)

Get-ServiceFabricClusterHealthChunk -ApplicationFilters $appFilters


HealthState                  : Error
NodeHealthStateChunks        : None
ApplicationHealthStateChunks : 
                               TotalCount            : 1
                               
                               ApplicationName       : fabric:/WordCount
                               ApplicationTypeName   : WordCount
                               HealthState           : Error
                               ServiceHealthStateChunks : 
                                TotalCount            : 1
                               
                                ServiceName           : fabric:/WordCount/WordCountService
                                HealthState           : Error
                                PartitionHealthStateChunks : 
                                    TotalCount            : 1
                               
                                    PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
                                    HealthState           : Error
                                    ReplicaHealthStateChunks : 
                                        TotalCount            : 5
                               
                                        ReplicaOrInstanceId   : 131444422293118720
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293118721
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293113678
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293113679
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422260002646
                                        HealthState           : Error
```

Hello следующий командлет возвращает все развернутые сущности на узле.

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$dspFilter = New-Object System.Fabric.Health.DeployedServicePackageHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$daFilter =  New-Object System.Fabric.Health.DeployedApplicationHealthStateFilter -Property @{HealthStateFilter=$allFilter;NodeNameFilter="_Node_2"}
$daFilter.DeployedServicePackageFilters.Add($dspFilter)

$appFilter = New-Object System.Fabric.Health.ApplicationHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$appFilter.DeployedApplicationFilters.Add($daFilter)

$appFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.ApplicationHealthStateFilter]
$appFilters.Add($appFilter)
Get-ServiceFabricClusterHealthChunk -ApplicationFilters $appFilters


HealthState                  : Error
NodeHealthStateChunks        : None
ApplicationHealthStateChunks : 
                               TotalCount            : 2
                               
                               ApplicationName       : fabric:/System
                               HealthState           : Ok
                               DeployedApplicationHealthStateChunks : 
                                TotalCount            : 1
                               
                                NodeName              : _Node_2
                                HealthState           : Ok
                                DeployedServicePackageHealthStateChunks :
                                    TotalCount            : 1
                               
                                    ServiceManifestName   : FAS
                                    ServicePackageActivationId : 
                                    HealthState           : Ok
                               
                               
                               
                               ApplicationName       : fabric:/WordCount
                               ApplicationTypeName   : WordCount
                               HealthState           : Error
                               DeployedApplicationHealthStateChunks : 
                                TotalCount            : 1
                               
                                NodeName              : _Node_2
                                HealthState           : Ok
                                DeployedServicePackageHealthStateChunks :
                                    TotalCount            : 1
                               
                                    ServiceManifestName   : WordCountServicePkg
                                    ServicePackageActivationId : 
                                    HealthState           : Ok
```

### <a name="rest"></a>REST
Вы можете получить блок работоспособности кластера с [запрос GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks) или [запрос POST](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster) политики работоспособности, и расширенные фильтры, описанные в теле hello.

## <a name="general-queries"></a>Общие запросы
Общие запросы возвращают перечень сущностей Service Fabric указанного типа. Они доступны через hello API (посредством методов hello на **FabricClient.QueryManager**), командлеты PowerShell и REST. Эти запросы состоят из вложенных запросов от нескольких компонентов. Один из них — hello [базе данных health store](service-fabric-health-introduction.md#health-store), который заполняет hello суммарный состояние работоспособности для каждого результата запроса.  

> [!NOTE]
> Общие запросы возвращают состояние работоспособности hello суммарный hello объекта и не содержат данных о работоспособности широкие возможности. Если объект не находится в работоспособном состоянии, можно обрабатывать с tooget запросов работоспособности все его данные работоспособности, включая события, дочерних состояний работоспособности и оценки неисправностей.
>
>

Общие запросы возвращают состояние работоспособности неизвестно, для сущности, возможно, это хранилище работоспособности hello не имеет полные данные о сущности hello. Можно также в хранилище работоспособности toohello вложенный запрос не был успешно (например, произошла ошибка связи или базе данных health store hello подверглась регулированию). Дальнейшие с запросом работоспособности для hello сущности. Если вложенный запрос hello обнаружил временные ошибки, например неполадки с сетевым дальнейших запрос может завершиться успешно. Он может также содержат дополнительные сведения из хранилища работоспособности hello о почему hello сущности не предоставляется.

Здравствуйте, запросы, содержащие **HealthState** для сущности являются:

* Список узлов: возвращает hello список узлов в кластере hello (разбиением на страницы).
  * API — [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)
  * PowerShell: Get-ServiceFabricNode.
* Список приложений: Возвращает список hello приложений в кластере hello (разбиением на страницы).
  * API — [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)
  * PowerShell: Get-ServiceFabricApplication.
* Список служб: hello возвращает список служб в приложении (разбиением на страницы).
  * API — [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)
  * PowerShell: Get-ServiceFabricService.
* Список секций: Возвращает список hello секций в службе (разбиением на страницы).
  * API — [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)
  * PowerShell: Get-ServiceFabricPartition.
* Список реплик: Возвращает список hello реплик в секции (разбиением на страницы).
  * API — [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)
  * PowerShell: Get-ServiceFabricReplica.
* Развернуть список приложений: hello возвращает список развернутых приложений на узле.
  * API — [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)
  * PowerShell: Get-ServiceFabricDeployedApplication.
* Развернуть список пакетов службы: hello возвращает список пакетов служб в развернутом приложении.
  * API — [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)
  * PowerShell: Get-ServiceFabricDeployedApplication.

> [!NOTE]
> Некоторые запросы hello возвращать результатов по страницам. Hello этих запросов, возвращается список, производный от [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1). Если сообщение hello результаты не соответствуют, возвращается только страница и ContinuationToken, отслеживает, когда перечисление было остановлено. По-прежнему hello toocall же запроса и передачи в токен продолжения hello из hello предыдущих tooget Далее результаты запроса.
>
>

### <a name="examples"></a>Примеры
Hello следующий код возвращает hello неработоспособности приложения hello кластера:

```csharp
var applications = fabricClient.QueryManager.GetApplicationListAsync().Result.Where(
  app => app.HealthState == HealthState.Error);
```

Hello следующий командлет возвращает подробные сведения о приложении hello для структуры hello: / приложения WordCount. Обратите внимание, что состояние работоспособности — "Предупреждение".

```powershell
PS C:\> Get-ServiceFabricApplication -ApplicationName fabric:/WordCount

ApplicationName        : fabric:/WordCount
ApplicationTypeName    : WordCount
ApplicationTypeVersion : 1.0.0
ApplicationStatus      : Ready
HealthState            : Warning
ApplicationParameters  : { "WordCountWebService_InstanceCount" = "1";
                         "_WFDebugParams_" = "[{"ServiceManifestName":"WordCountWebServicePkg","CodePackageName":"Code","EntryPointType":"Main","Debug
                         ExePath":"C:\\Program Files (x86)\\Microsoft Visual Studio
                         14.0\\Common7\\Packages\\Debugger\\VsDebugLaunchNotify.exe","DebugArguments":" {74f7e5d5-71a9-47e2-a8cd-1878ec4734f1} -p
                         [ProcessId] -tid [ThreadId]","EnvironmentBlock":"_NO_DEBUG_HEAP=1\u0000"},{"ServiceManifestName":"WordCountServicePkg","CodeP
                         ackageName":"Code","EntryPointType":"Main","DebugExePath":"C:\\Program Files (x86)\\Microsoft Visual Studio
                         14.0\\Common7\\Packages\\Debugger\\VsDebugLaunchNotify.exe","DebugArguments":" {2ab462e6-e0d1-4fda-a844-972f561fe751} -p
                         [ProcessId] -tid [ThreadId]","EnvironmentBlock":"_NO_DEBUG_HEAP=1\u0000"}]" }
```

Hello следующий командлет возвращает hello службы с состоянием работоспособности ошибки:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplication | Get-ServiceFabricService | where {$_.HealthState -eq "Error"}


ServiceName            : fabric:/WordCount/WordCountService
ServiceKind            : Stateful
ServiceTypeName        : WordCountServiceType
IsServiceGroup         : False
ServiceManifestVersion : 1.0.0
HasPersistedState      : True
ServiceStatus          : Active
HealthState            : Error
```

## <a name="cluster-and-application-upgrades"></a>Обновление кластера и приложений
Во время обновления отслеживаемых hello кластера и приложения Service Fabric проверяет tooensure работоспособности, что все, что остается работоспособным. Если сущность неработоспособен, как вычисляется с помощью настроенными политиками работоспособности, hello обновление применяется следующее действие политики, предназначенные для обновления toodetermine hello. Hello обновления может быть приостановлена tooallow взаимодействия с пользователем (например, исправления ошибок или изменении политик), или он может автоматически отката предыдущей версии хорошо toohello.

Во время *кластера* обновления, вы можете получить состояние обновления кластера hello. Состояние обновления Hello включает оценки неисправностей, в какой точке toowhat находится в неисправном состоянии, в кластере hello. Если hello обновление выполняется откат из-за проблем с toohealth, состояние обновления hello запоминает последние неработоспособное причин hello. Эти сведения могут помочь администраторам определить, что пошло не так, после обновления hello откат или прекращения.

Аналогичным образом, во время *приложения* обновления, оценки неисправностей в любой находятся в состоянии обновления приложения hello.

Hello Далее показано состояние обновления приложения hello для изменения структуры: / приложения WordCount. Устройство наблюдения сообщило об ошибке на одной из реплик. Обновление Hello в настоящее время переходит назад, так как не накладывается ограничение на проверку работоспособности hello.

```powershell
PS C:\> Get-ServiceFabricApplicationUpgrade fabric:/WordCount

ApplicationName               : fabric:/WordCount
ApplicationTypeName           : WordCount
TargetApplicationTypeVersion  : 1.0.0.0
ApplicationParameters         : {}
StartTimestampUtc             : 4/21/2017 5:23:26 PM
FailureTimestampUtc           : 4/21/2017 5:23:37 PM
FailureReason                 : HealthCheck
UpgradeState                  : RollingBackInProgress
UpgradeDuration               : 00:00:23
CurrentUpgradeDomainDuration  : 00:00:00
CurrentUpgradeDomainProgress  : UD1

                                NodeName            : _Node_1
                                UpgradePhase        : Upgrading

                                NodeName            : _Node_2
                                UpgradePhase        : Upgrading

                                NodeName            : _Node_3
                                UpgradePhase        : PreUpgradeSafetyCheck
                                PendingSafetyChecks :
                                EnsurePartitionQuorum - PartitionId: 30db5be6-4e20-4698-8185-4bd7ca744020
NextUpgradeDomain             : UD2
UpgradeDomainsStatus          : { "UD1" = "Completed";
                                "UD2" = "Pending";
                                "UD3" = "Pending";
                                "UD4" = "Pending" }
UnhealthyEvaluations          :
                                Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.

                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.

                                      Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                      Unhealthy partition: PartitionId='a1f83a35-d6bf-4d39-b90d-28d15f39599b', AggregatedHealthState='Error'.

                                          Unhealthy replicas: 20% (1/5), MaxPercentUnhealthyReplicasPerPartition=0%.

                                          Unhealthy replica: PartitionId='a1f83a35-d6bf-4d39-b90d-28d15f39599b',
                                  ReplicaOrInstanceId='131031502346844058', AggregatedHealthState='Error'.

                                              Error event: SourceId='DiskWatcher', Property='Disk'.

UpgradeKind                   : Rolling
RollingUpgradeMode            : UnmonitoredAuto
ForceRestart                  : False
UpgradeReplicaSetCheckTimeout : 00:15:00
```

Дополнительные сведения о hello [обновление приложения Service Fabric](service-fabric-application-upgrade.md).

## <a name="use-health-evaluations-tootroubleshoot"></a>Использовать tootroubleshoot аттестации работоспособности
При наличии проблемы с hello кластеров или приложение, взгляните на toopinpoint работоспособности кластера или приложение hello проблема. оценки неисправностей Hello содержат сведения о какой триггеру hello текущего неработоспособное состояние. Если необходимо, можно выполнить детализацию в неработоспособные дочерние объекты tooidentify hello основную причину.

Например предположим, что приложение неработоспособно, так как поступил отчет об ошибке в одной из ее реплик. Hello следующий командлет Powershell показано оценки неисправностей hello.

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth fabric:/WordCount -EventsFilter None -ServicesFilter None -DeployedApplicationsFilter None -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                                  
                                        Unhealthy replicas: 20% (1/5), MaxPercentUnhealthyReplicasPerPartition=0%.
                                  
                                        Unhealthy replica: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', ReplicaOrInstanceId='131444422260002646', AggregatedHealthState='Error'.
                                  
                                            Error event: SourceId='MyWatchdog', Property='Memory'.
                                  
ServiceHealthStates             : None
DeployedApplicationHealthStates : None
HealthEvents                    : None
```

Tooget hello реплики можно просмотреть дополнительные сведения:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricReplicaHealth -ReplicaOrInstanceId 131444422260002646 -PartitionId af2e3e44-a8f8-45ac-9f31-4093eb897600


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422260002646
AggregatedHealthState : Error
UnhealthyEvaluations  : 
                        Error event: SourceId='MyWatchdog', Property='Memory'.
                        
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131444422263668344
                        SentAt                : 7/13/2017 5:57:06 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_2
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                        
                        SourceId              : MyWatchdog
                        Property              : Memory
                        HealthState           : Error
                        SequenceNumber        : 131444451657749403
                        SentAt                : 7/13/2017 6:46:05 PM
                        ReceivedAt            : 7/13/2017 6:46:05 PM
                        TTL                   : Infinite
                        Description           : 
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Warning->Error = 7/13/2017 6:46:05 PM, LastOk = 1/1/0001 12:00:00 AM
```

> [!NOTE]
> Hello оценки неисправностей Показать hello первый причина, по которой hello сущность является оценка toocurrent состояние работоспособности. Может быть несколько событий, которые вызывают это состояние, но они, не отражаются в hello оценок. tooget Дополнительные сведения, детализации углублением в toofigure сущностей работоспособности hello out все отчеты неработоспособное hello в кластере hello.
>
>

## <a name="next-steps"></a>Дальнейшие действия
[Использовать tootroubleshoot отчеты о работоспособности системы](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[Добавление настраиваемых отчетов о работоспособности Service Fabric](service-fabric-report-health.md)

[Как tooreport и проверки службы работоспособности](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[Мониторинг и диагностика состояния служб в локальной среде разработки](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Обновление приложения Service Fabric](service-fabric-application-upgrade.md)
