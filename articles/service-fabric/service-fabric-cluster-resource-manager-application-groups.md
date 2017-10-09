---
title: "aaaService диспетчер ресурсов кластера структуры - групп приложений | Документы Microsoft"
description: "Общие сведения о функции группы приложений в диспетчер ресурсов кластера Service Fabric hello hello"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 4cae2370-77b3-49ce-bf40-030400c4260d
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: b4f068862d962b53a0b3ea813b89bb13ee395681
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooapplication-groups"></a>Введение tooApplication групп
Диспетчер ресурсов кластера Service Fabric обычно управляет ресурсы кластера, распределяя нагрузки hello (представить так [метрики](service-fabric-cluster-resource-manager-metrics.md)) равномерно по всему hello кластера. Service Fabric управляет емкости hello hello узлов в кластер hello и кластер hello в целом через [емкость](service-fabric-cluster-resource-manager-cluster-description.md). Метрики и емкость отлично работают для большинства рабочих нагрузок, но для структур, активно использующих разные экземпляры приложений Service Fabric, иногда возникают дополнительные требования. Например, может потребоваться следующее.

- Резервирование какого hello узлах кластера hello hello службы в некоторых именованный экземпляр приложения
- Ограничить общее число узлов, работающих служб hello в именованный экземпляр приложения на (вместо рассредоточения их через весь кластер hello) для hello
- Определить емкость для hello именованный экземпляр приложения сам toolimit hello число служб или общее потребление ресурсов hello служб внутри него

toomeet эти требования hello диспетчер ресурсов кластера Service Fabric поддерживает функцию групп приложений.

## <a name="limiting-hello-maximum-number-of-nodes"></a>Ограничивая максимальное количество узлов hello
Hello простейший вариант использования емкости приложения при экземпляр приложения должен toobe ограниченную tooa определенных максимальное количество узлов. Это позволяет объединить все службы, выполняющиеся в этом экземпляре приложения, на заданном количестве компьютеров. Консолидация полезно, когда вы пытаетесь toopredict или ограничения максимального физических ресурсов, используемых службами hello в этот именованный экземпляр приложения. 

Hello иллюстрации показан экземпляр приложения с и без максимальное количество узлов, определенных.

<center>
![Определение максимального количества узлов для экземпляров приложения][Image1]
</center>

В примере hello левой приложения hello не имеет максимальное количество узлов, определенных и он имеет три службы. Hello диспетчер ресурсов кластера разбросаны все реплики шесть доступные узлы tooachieve hello оптимальный баланс в кластере hello (поведение по умолчанию hello). В примере справа hello, мы увидим hello того же приложения ограниченных узлов toothree.

параметр Hello, управляющий такое поведение называется максимальное число узлов. Этот параметр можно задать при создании приложения или изменить для уже выполняющегося экземпляра приложения.

PowerShell

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MaximumNodes 3
Update-ServiceFabricApplication –Name fabric:/AppName –MaximumNodes 5
```

C#

``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";
ad.MaximumNodes = 3;
await fc.ApplicationManager.CreateApplicationAsync(ad);

ApplicationUpdateDescription adUpdate = new ApplicationUpdateDescription(new Uri("fabric:/AppName"));
adUpdate.MaximumNodes = 5;
await fc.ApplicationManager.UpdateApplicationAsync(adUpdate);

```

В рамках hello набора узлов hello диспетчер ресурсов кластера не гарантирует, какие объекты службы достаточная вместе или использовать, какие узлы.

## <a name="application-metrics-load-and-capacity"></a>Метрики, нагрузка и емкость приложения
Группы приложений также позволяют toodefine показатели, связанные с данной именованный экземпляр приложения, а емкость данного экземпляра приложения для этих показателей. Метрики приложения позволяют tootrack, резервировать и предел потребления ресурсов hello hello служб внутри данного экземпляра приложения.

Для каждой метрики приложения можно установить два значения.

- **Общая емкость приложения** — этот параметр представляет hello общая емкость приложения hello для конкретного показателя. Диспетчер ресурсов кластера Hello запрещает hello создания новых служб в пределах данного экземпляра приложения, которое вызовет tooexceed общую нагрузку это значение. Например предположим, что экземпляр приложения hello составляет 10 и уже имеется пять загрузку. Hello создании службы с загрузкой по умолчанию всего 10 будет запрещено.
- **Максимальная емкость узла** — этот параметр определяет максимальное hello общую нагрузку для приложения hello на одном узле. Если нагрузки переходит по емкости, hello диспетчер ресурсов кластера перемещает узлы tooother реплики так, чтобы hello уменьшения нагрузки.


PowerShell:

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -Metrics @("MetricName:Metric1,MaximumNodeCapacity:100,MaximumApplicationCapacity:1000")
```

C#:

``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";

var appMetric = new ApplicationMetricDescription();
appMetric.Name = "Metric1";
appMetric.TotalApplicationCapacity = 1000;
appMetric.MaximumNodeCapacity = 100;
ad.Metrics.Add(appMetric);
await fc.ApplicationManager.CreateApplicationAsync(ad);
```

## <a name="reserving-capacity"></a>Резервирование емкости
Еще одно распространенное использование групп приложений является tooensure hello, ресурсов в кластере зарезервированы для экземпляров данного приложения. При создании экземпляра приложения hello всегда резервируется место Hello.

Резервирование пространства в кластере hello для приложения hello произойдет немедленно, даже когда:
- создается экземпляр приложения Hello, но не сопоставлено ни одной службы в ней еще
- Hello нескольким службам внутри экземпляра приложения hello изменяется каждый раз 
- Hello службы существует, но не использует ресурсы hello 

Чтобы зарезервировать ресурсы для экземпляра приложения, следует использовать два дополнительных параметра: *MinimumNodes* и *NodeReservationCapacity*.

- **Минимальное число узлов** -определяет hello минимальное число узлов, которые приложение hello экземпляр должен работать.  
- **NodeReservationCapacity** -эта настройка выполняется на уровне метрики для приложения hello. значение Hello — hello объем эта метрика зарезервированы для приложения hello на любом узле, где, hello службами этого запуска приложения.

Объединение **минимальное число узлов** и **NodeReservationCapacity** гарантирует резервирование минимальное нагрузки для приложения hello в кластере hello. Если осталось меньше емкости в hello кластера требуется общее резервирование hello, происходит сбой создания приложения hello. 

Рассмотрим пример резервирования емкости.

<center>
![Определение резервируемой емкости для экземпляров приложения][Image2]
</center>

В примере hello левой приложения не все пространство приложения определены. Диспетчер ресурсов кластера Hello сальдо все данные в соответствии с правилами toonormal.

В примере hello на правом hello Предположим, что Application1 создавался hello следующие параметры:

- Tootwo набор узлов
- для приложения определена метрика со следующими значениями:
  - NodeReservationCapacity = 20;

PowerShell

 ``` posh
 New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MinimumNodes 2 -Metrics @("MetricName:Metric1,NodeReservationCapacity:20")
 ```

C#

 ``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";
ad.MinimumNodes = 2;

var appMetric = new ApplicationMetricDescription();
appMetric.Name = "Metric1";
appMetric.NodeReservationCapacity = 20;

ad.Metrics.Add(appMetric);

await fc.ApplicationManager.CreateApplicationAsync(ad);
```

Service Fabric резервирует мощность на двух узлах для Application1 и не допускает служб из Application2 tooconsume его емкость, даже если существуют нагрузки не поглощается hello служб внутри Application1 во время hello. Зарезервированные приложения емкости считается потребляет и вычитается hello оставшихся емкости на этом узле и в кластере hello.  Резервирование Hello вычитается из оставшихся емкость кластера немедленно hello, однако зарезервированные hello потребление вычитается из hello емкость конкретного узла только в том случае, если по крайней мере одна служба объект помещается на нем. Этот второй этап резервирования позволяет более гибко и более эффективно использовать ресурсы, поскольку на конкретных узлах резервирование происходит только по мере необходимости.

## <a name="obtaining-hello-application-load-information"></a>Получение сведений о нагрузки приложения hello
Для каждого приложения, которое емкостью приложения, определенные для одну или несколько метрик можно получить hello сведения о hello суммарную нагрузку, о которых сообщили реплик службы.

PowerShell:

``` posh
Get-ServiceFabricApplicationLoad –ApplicationName fabric:/MyApplication1
```

C#

``` csharp
var v = await fc.QueryManager.GetApplicationLoadInformationAsync("fabric:/MyApplication1");
var metrics = v.ApplicationLoadMetricInformation;
foreach (ApplicationLoadMetricInformation metric in metrics)
{
    Console.WriteLine(metric.ApplicationCapacity);  //total capacity for this metric in this application instance
    Console.WriteLine(metric.ReservationCapacity);  //reserved capacity for this metric in this application instance
    Console.WriteLine(metric.ApplicationLoad);  //current load for this metric in this application instance
}
```

Hello ApplicationLoad запрос возвращает hello основные сведения о производительности приложения, указанная для приложения hello. Эти сведения включают hello минимальное и максимальное узлам сведений и hello число, которое в настоящее время занимает приложения hello. Также вы получите информацию по каждой метрике нагрузки для приложения, в том числе перечисленные ниже сведения.

* Имя метрики: Имя метрики hello.
* Емкость резервирования: Емкость кластера, зарезервированный для данного приложения в кластере hello.
* Application Load: общая нагрузка, создаваемая дочерними репликами этого приложения.
* Application Capacity: максимально допустимое значение нагрузки приложения.

## <a name="removing-application-capacity"></a>Удаление емкости приложения
После настройки параметров производительности приложения hello для приложения, их можно удалить с помощью API-интерфейсы для обновления приложения или командлеты PowerShell. Например:

``` posh
Update-ServiceFabricApplication –Name fabric:/MyApplication1 –RemoveApplicationCapacity

```

Эта команда удаляет все параметры управления емкостью приложения из экземпляра приложения hello. Включает минимальное число узлов, узлов и показатели приложения hello, если таковые имеются. Hello hello команда действует немедленно. После выполнения этой команды, hello диспетчер ресурсов кластера использует поведение по умолчанию hello для управления приложениями. Параметры емкости приложения можно задать снова, используя команду `Update-ServiceFabricApplication`/`System.Fabric.FabricClient.ApplicationManagementClient.UpdateApplicationAsync()`.

### <a name="restrictions-on-application-capacity"></a>Ограничения на емкость приложений
Существует ряд ограничений на параметры емкости приложений, которые необходимо соблюдать. При обнаружении ошибок во время проверки изменения не применяются.

- Все числовые параметры должны иметь неотрицательные значения.
- MinimumNodes не может иметь значение больше, чем MaximumNodes.
- Если определены емкости для метрики нагрузки, они должны соответствовать следующим правилам.
  - NodeReservationCapacity не может иметь значение больше, чем MaximumNodeCapacity. Например нельзя ограничить hello емкости для hello метрики «CPU» на устройствах tootwo hello узла и повторите tooreserve три единицы на каждом узле.
  - Если указано максимальное число узлов, затем hello продукт максимальное число узлов и максимальная емкость узла не поддерживает больше, чем общая емкость приложения. Например предположим, что максимальная емкость узла для метрики нагрузки «CPU» имеет значение tooeight hello. Также предположим, что значение hello too10 максимальное число узлов. В этом случае общая емкость приложения для этой метрики нагрузки должна быть больше 80.

Hello ограничения применяются как во время создания приложений и обновлений.

## <a name="how-not-toouse-application-capacity"></a>Как toouse емкость приложения
- Не предпринимайте toouse hello группы приложений функции tooconstrain приложения hello tooa _конкретных_ ограниченного набора узлов. Другими словами, можно указать, что приложение hello должно выполняться не более пяти узлов, но не какие конкретных пяти узлов в кластере hello. Ограничение toospecific приложения узлов может осуществляться с помощью ограничений размещения для службы.
- Не предпринимайте tooensure емкость приложения hello toouse, что две службы из того же приложения размещаются на hello hello разным узлам. Вместо этого используйте [сходство](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md) или [ограничения размещения](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints).

## <a name="next-steps"></a>Дальнейшие действия
- Дополнительные сведения о настройке служб см. в разделе [Настройка параметров Cluster Resource Manager для служб Service Fabric](service-fabric-cluster-resource-manager-configure-services.md).
- toofind out о управляет hello диспетчер ресурсов кластера и балансировку нагрузки в кластере hello Извлеките hello статьи на [балансировки нагрузки](service-fabric-cluster-resource-manager-balancing.md)
- Начать с начала hello и [получить введение toohello диспетчер ресурсов кластера Service Fabric](service-fabric-cluster-resource-manager-introduction.md)
- Дополнительные сведения об использовании метрик см. в статье [Управление потреблением ресурсов и нагрузкой в Service Fabric с помощью метрик](service-fabric-cluster-resource-manager-metrics.md).
- Hello диспетчер ресурсов кластера позволяет настраивать различные параметры для описания кластера hello. toofind подробные сведения о них, извлеките в этой статье на [описания кластера Service Fabric](service-fabric-cluster-resource-manager-cluster-description.md)

[Image1]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-max-nodes.png
[Image2]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-reserved-capacity.png
