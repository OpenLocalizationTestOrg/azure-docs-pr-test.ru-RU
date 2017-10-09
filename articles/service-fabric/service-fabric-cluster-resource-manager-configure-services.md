---
title: "aaaSpecify метрики и параметры положения в Azure микрослужбами | Документы Microsoft"
description: "Описание службы Service Fabric с указанием метрик, ограничений на размещение и других политик размещения."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 16e135c1-a00a-4c6f-9302-6651a090571a
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: c633518b5dbf0c7b84e0d46c06bf1f92365d184d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-cluster-resource-manager-settings-for-service-fabric-services"></a>Настройка параметров Cluster Resource Manager для служб Service Fabric
Диспетчер ресурсов кластера Service Fabric Hello обеспечивает точный контроль hello правила, управляющие каждый человек с именем службы. Каждой службы можно указать правила для как его следует выделить в кластере hello. Каждой службы можно также определить hello набор показателей, что ему tooreport, включая, как они важны toothat службы. Настройка служб делится на три задачи:

1. настройка ограничений на размещение;
2. настройка метрик;
3. настройка расширенных политик размещения и других правил (мало распространено).

## <a name="placement-constraints"></a>Ограничения на размещение
Ограничения размещения, используемые toocontrol, какие узлы в кластере hello службы могут выполняться в. Как правило, называется конкретного экземпляра службы или все службы заданного типа, ограниченного toorun определенного типа узла. Ограничения размещения можно расширять. Можно определить любой набор свойств для каждого типа узла, а затем выбирать их и ограничения при создании служб. Ограничения размещения службы можно также изменить, когда она запущена. Это позволяет toochanges toorespond в кластере hello или hello требования к службе hello. Hello свойства данного узла также может обновляться динамически в кластере hello. Дополнительные сведения об ограничения размещения и как tooconfigure их можно найти в [в данной статье](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints)

## <a name="metrics"></a>Метрики
Метрики являются ресурсы, необходимые для данной службы именованный набор hello. Конфигурация метрик службы включает в себя информацию о том, какую часть ресурса использует по умолчанию каждая реплика с отслеживанием состояния или экземпляр без отслеживания состояния этой службы. Метрики также включают вес, который определяет важность балансировки эта метрика службы toothat на случай необходимости компромиссы.

## <a name="advanced-placement-rules"></a>Расширенные правила размещения
Существуют другие типы правил размещения, которые могут использоваться в менее распространенных сценариях. Ниже приведены некоторые примеры.
- Ограничения, которые помогают в работе с географически распределенными кластерами.
- Определенные архитектуры приложений.

Другие правила размещения настраиваются с помощью корреляций или политик.

## <a name="next-steps"></a>Дальнейшие действия
- Показатели, как hello диспетчера ресурсов кластера Service Fabric управляет потребления и мощность в кластере hello. Дополнительные сведения о метриках toolearn как tooconfigure, извлечение и возврат [в данной статье](service-fabric-cluster-resource-manager-metrics.md)
- Сходство — один режимов, который можно настроить для служб. Этот режим редко используется; узнать о нем подробнее можно [здесь](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md)
- Существует много различных размещения правила, которые можно настроить на дополнительные сценарии toohandle службы. Узнать о разных политиках размещения можно [здесь](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md)
- Начать с начала hello и [получить введение toohello диспетчер ресурсов кластера Service Fabric](service-fabric-cluster-resource-manager-introduction.md)
- toofind out о управляет hello диспетчер ресурсов кластера и балансировку нагрузки в кластере hello Извлеките hello статьи на [балансировки нагрузки](service-fabric-cluster-resource-manager-balancing.md)
- Hello диспетчер ресурсов кластера позволяет настраивать различные параметры для описания кластера hello. toofind подробные сведения о них, извлеките в этой статье на [описания кластера Service Fabric](service-fabric-cluster-resource-manager-cluster-description.md)
