---
title: "Диспетчер кластерных ресурсов Service Fabric: стоимость перемещения | Документация Майкрософт"
description: "Общие сведения о стоимости перемещения служб Service Fabric."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: f022f258-7bc0-4db4-aa85-8c6c8344da32
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 65d4ac73efffcf7b25b1e95da6f9012a9238cb75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="service-movement-cost"></a>Затраты на перемещение служб
Коэффициент, на который hello диспетчер ресурсов кластера Service Fabric считает, что при попытке toodetermine, какие изменения toomake tooa кластер находится стоимость hello этих изменений. Hello понятие «стоимость», проданные отключение от можно повысить, сколько кластеров hello. Затраты учитываются при перемещении служб для балансировки, дефрагментации и выполнения других требований. Задача Hello — toomeet требований hello в hello наименьших нарушают работу или ресурсоемкие способом. 

Как минимум перемещение служб требует затрат процессорного времени и пропускной способности сети. Для служб с отслеживанием состояния требуется копирование hello состояние эти службы, использование дополнительной памяти и диска. Снижают стоимость hello решений приветствия, рассматриваемых в диспетчер ресурсов Azure Service Fabric кластера гарантирует ресурсы кластера hello не затраченное без необходимости. Тем не менее также не следует tooignore решений, которые позволяет значительно улучшить hello выделения ресурсов в кластере hello.

Диспетчер ресурсов кластера Hello предоставляет два способа вычисления затрат и ограничить их допуск при попытке toomanage hello кластера. Первый механизм Hello просто подсчет каждом переходе, он делает. Если два решения, создаваемые с помощью о hello же балансировку (оценка), то диспетчер ресурсов кластера hello предпочтительный hello один hello дешевый (общее число ходов).

Эта стратегия хорошо работает. Но, как и в случае нагрузок по умолчанию или статических нагрузок, маловероятно, что в любой сложной системе все будут перемещения равнозначны. Некоторые, скорее всего, toobe гораздо более затратным.

## <a name="setting-move-costs"></a>Настройка затрат на перемещение 
Hello стоимость перемещения по умолчанию для службы можно указать при ее создании.

PowerShell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -DefaultMoveCost Medium
```

C#: 

```csharp
FabricClient fabricClient = new FabricClient();
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
//set up hello rest of hello ServiceDescription
serviceDescription.DefaultMoveCost = MoveCost.Medium;
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

Также можно указать или MoveCost динамическое обновление для службы после создания службы hello: 

PowerShell: 

```posh
Update-ServiceFabricService -Stateful -ServiceName "fabric:/AppName/ServiceName" -DefaultMoveCost High
```

C#:

```csharp
StatefulServiceUpdateDescription updateDescription = new StatefulServiceUpdateDescription();
updateDescription.DefaultMoveCost = MoveCost.High;
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/AppName/ServiceName"), updateDescription);
```

## <a name="dynamically-specifying-move-cost-on-a-per-replica-basis"></a>Динамическое указание затрат на перемещение на уровне реплики

Hello выше фрагменты кода, для указания MoveCost для всей службы за один раз из самой службы вне hello. Тем не менее, переместить затраты являются наиболее полезен при стоимость перемещения hello объекта конкретной службы меняются с течением времени его существования. Так как сами службы, возможно, hello hello наиболее знать о том, насколько дорогостоящим их toomove определенный момент времени, существует API-Интерфейс для службы tooreport стоимость отдельных Переход во время выполнения. 

C#:

```csharp
this.Partition.ReportMoveCost(MoveCost.Medium);
```

## <a name="impact-of-move-cost"></a>Влияние затрат на перемещение
MoveCost имеет четыре уровня: Zero, Low, Medium и High. MoveCosts — относительный tooeach другими, кроме нуля. Ноль стоимость перемещения означает, что перемещение предоставляется бесплатно и следует не подпадают оценка hello hello решения. Параметр tooHigh стоимости и переместить *не* гарантирует, hello реплика остается в одном месте.

<center>
![Влияние стоимости перемещения на выбор реплик для перемещения][Image1]
</center>

MoveCost помогает найти hello решения, что причина hello наименьших перебоев в целом и простым tooachieve при по-прежнему поступающих в эквивалентные баланс. Понятие службы затраты могут быть относительные toomany сущности. Hello наиболее распространенные факторы при расчете затрат перемещения являются:

- Hello объем состояния или данные, что служба hello имеет toomove.
- стоимость Hello отключения клиентов. Перемещение первичной реплики, обычно дороже, чем hello стоимость перемещения вторичной реплики.
- Hello затраты на лету операции прерывания. Некоторые операции hello данных хранения уровня или операции, выполняемые в ответ tooa клиентский вызов являются ресурсоемкими. В определенный момент вы не хотите toostop их, если не нужно. Поэтому во время операции hello происходит, увеличить стоимость перемещения hello этой службы объекта tooreduce hello вероятность того, что он перемещается. По завершении операции hello задаются задней toonormal hello затрат.

## <a name="enabling-move-cost-in-your-cluster"></a>Включение учета затрат на перемещение в кластере
Чтобы Здравствуйте более детального toobe MoveCosts принимать в расчет, MoveCost необходимо включить в кластер. Без этого параметра режима по умолчанию hello подсчета перемещает используется для расчета MoveCost и MoveCost отчеты игнорируются.


ClusterManifest.xml:

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="UseMoveCostReports" Value="true" />
        </Section>
```

Для автономных развертываний используется ClusterConfig.json, а для размещенных в Azure кластеров — Template.json.

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "UseMoveCostReports",
          "value": "true"
      }
    ]
  }
]
```

## <a name="next-steps"></a>Дальнейшие действия
- Диспетчера ресурсов кластера Service Fabric использует потребления toomanage метрик и емкости в кластере hello. Дополнительные сведения о метриках toolearn как tooconfigure, извлечение и возврат [Управление потреблением ресурсов и загрузки в Service Fabric с метриками](service-fabric-cluster-resource-manager-metrics.md).
- toolearn о hello диспетчер ресурсов кластера управляет и балансировку нагрузки в кластере hello, извлечь [балансировки кластера Service Fabric](service-fabric-cluster-resource-manager-balancing.md).

[Image1]:./media/service-fabric-cluster-resource-manager-movement-cost/service-most-cost-example.png
