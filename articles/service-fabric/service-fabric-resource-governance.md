---
title: "aaaAzure ресурсами структуры службы для контейнеров и службы | Документы Microsoft"
description: "Azure Service Fabric позволяет toospecify ограничения ресурсов для служб, выполняемых внутри или вне контейнеров."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 34e368211d98ff6b5b294c9c8b3af5ca30eeb20c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="resource-governance"></a>управление ресурсами; 

При нескольких служб hello одного узла или кластера, возможно, что одна служба может потреблять больше ресурсов, лишить другие службы. Эта проблема является ссылка tooas hello шумный сосед проблемой. Service Fabric позволяет резервирования toospecify разработчика hello и ограничения на ресурсы tooguarantee службы и также ограничить его использование ресурсов. 

## <a name="resource-governance-metrics"></a>Метрики управления ресурсами 

Управление ресурсами поддерживается в Service Fabric для каждого [пакета службы](service-fabric-application-model.md). Hello ресурсов, назначенных tooService пакета можно разделить между пакетами кода. ограничения ресурсов Hello, заданные также означать hello резервирования ресурсов hello. Service Fabric поддерживает указание ЦП и памяти для каждого пакета службы с помощью двух встроенных [метрик](service-fabric-cluster-resource-manager-metrics.md):

* ЦП (Имя метрики `ServiceFabric:/_CpuCores`): лежит логического ядра, которая доступна на компьютере размещения hello и все ядра для всех узлов, считаются одинаковыми hello.
* Память (Имя метрики `ServiceFabric:/_MemoryInMB`): памяти измеряется в мегабайтах, и он был сопоставлен toophysical памяти, которая доступна на компьютере hello.

Только гарантированное резервирование мягкий предоставляются - среды выполнения hello отклоняет открытия превышены доступные ресурсы пакеты новой службы. Тем не менее другой исполняемого файла или контейнера, помещенного на узле hello, нарушить исходное гарантированное резервирование hello.

Эти две метрики hello [диспетчер ресурсов кластера](service-fabric-cluster-resource-manager-cluster-description.md) отслеживает емкость всего кластера, hello нагрузки на каждом узле в кластере hello и оставшихся ресурсы в кластере hello. Эти две метрики эквивалентные tooany других пользователей или пользовательская метрика и все существующие возможности можно использовать с ними:
* Кластер может представлять [балансировки](service-fabric-cluster-resource-manager-balancing.md) toothese двух метрики (по умолчанию) в соответствии с.
* Кластер может представлять [дефрагментировать](service-fabric-cluster-resource-manager-defragmentation-metrics.md) toothese двух показатели в соответствии с.
* При [описании кластера](service-fabric-cluster-resource-manager-cluster-description.md) для этих двух метрик можно задать емкость буфера.

[Передача данных о динамической нагрузке](service-fabric-cluster-resource-manager-metrics.md) не поддерживается этими метриками, и нагрузка для них определяется во время создания.

## <a name="cluster-set-up-for-enabling-resource-governance"></a>Настройка кластера для включения управления ресурсами

Емкость должен быть определен вручную в каждом типе узла в кластере hello следующим образом:

```xml
    <NodeType Name="MyNodeType">
      <Capacities>
        <Capacity Name="ServiceFabric:/_CpuCores" Value="4"/>
        <Capacity Name="ServiceFabric:/_MemoryInMB" Value="2048"/>
      </Capacities>
    </NodeType>
```
 
Управление ресурсами допускается только в пользовательских службах, но не в каких-либо системных службах. При указании емкости некоторые ядра и память должны оставаться нераспределенными для системных служб. Для достижения оптимальной производительности hello после параметра необходимо также включить в манифесте кластера hello: 

```xml
<Section Name="PlacementAndLoadBalancing">
    <Parameter Name="PreventTransientOvercommit" Value="true" /> 
    <Parameter Name="AllowConstraintCheckFixesDuringApplicationUpgrade" Value="true" />
</Section>
```


## <a name="specifying-resource-governance"></a>Указание управления ресурсами 

Ограничения ресурсов системы управления указаны в манифесте приложения hello (раздел ServiceManifestImport), как показано в следующий пример hello:

```xml
<?xml version='1.0' encoding='UTF-8'?>
<ApplicationManifest ApplicationTypeName='TestAppTC1' ApplicationTypeVersion='vTC1' xsi:schemaLocation='http://schemas.microsoft.com/2011/01/fabric ServiceFabricServiceModel.xsd' xmlns='http://schemas.microsoft.com/2011/01/fabric' xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance'>
  <Parameters>
  </Parameters>
  <!--
  ServicePackageA has hello number of CPU cores defined, but doesn't have hello MemoryInMB defined.
  In this case, Service Fabric will sum hello limits on code packages and uses hello sum as 
  hello overall ServicePackage limit.
  -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName='ServicePackageA' ServiceManifestVersion='v1'/>
    <Policies>
      <ServicePackageResourceGovernancePolicy CpuCores="1"/>
      <ResourceGovernancePolicy CodePackageRef="CodeA1" CpuShares="512" MemoryInMB="1000" />
      <ResourceGovernancePolicy CodePackageRef="CodeA2" CpuShares="256" MemoryInMB="1000" />
    </Policies>
  </ServiceManifestImport>
```
  
В этом примере пакет службы ServicePackageA получает одно ядро на узлах hello, где размещается. Этот пакет обновления содержит два пакета кода (CodeA1 и CodeA2), и обе конечные точки задают hello `CpuShares` параметра. Hello долю CpuShares 512:256 делит hello core в двух пакетах кода hello. Таким образом в этом примере CodeA1 возвращает две трети ядра, CodeA2 возвращает трети ядра (и резервирование программной гарантии hello же). В случае, если при CpuShares для пакетов кода не указаны, Service Fabric делит ядер hello поровну между ними.

Ограничения памяти может абсолютным, поэтому оба пакета кода, ограниченный too1024 МБ памяти (и гарантии программной резервирование же hello). Пакеты кода (контейнеров или процессов) не может tooallocate, который больше памяти, чем это ограничение, попытка toodo таким образом вызывает исключение нехватки памяти. Toowork принудительного применения ограничения ресурсов все пакеты кода, в пакет службы должен иметь ограничения памяти.


## <a name="next-steps"></a>Дальнейшие действия
* toolearn более о диспетчер ресурсов кластера, см. в этой [статьи](service-fabric-cluster-resource-manager-introduction.md).
* прочитать этот текст toolearn Дополнительные сведения о модели приложения, пакеты обновления, пакеты кода и сопоставление реплик toothem [статьи](service-fabric-application-model.md).
