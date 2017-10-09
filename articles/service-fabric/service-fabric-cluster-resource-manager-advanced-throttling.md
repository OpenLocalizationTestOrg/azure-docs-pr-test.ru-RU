---
title: "aaaThrottling в диспетчер ресурсов кластера Service Fabric hello | Документы Microsoft"
description: "Дополнительные интервалы повтора tooconfigure hello, предоставляемые hello диспетчер ресурсов кластера Service Fabric."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 4a44678b-a5aa-4d30-958f-dc4332ebfb63
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: f418536911d3e3814e78a4d9f057dfb867ca7c63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="throttling-hello-service-fabric-cluster-resource-manager"></a>Регулирование hello диспетчер ресурсов кластера Service Fabric
Даже если вы настроили hello диспетчер ресурсов кластера неправильно, можно получить разрыва hello кластера. Например может быть одновременных узла и отказоустойчивость домена отказов - что произойдет, если возникшее во время обновления? Hello диспетчер ресурсов кластера всегда пытается toofix все потребление ресурсов кластера hello попытки tooreorganize и исправление hello кластера. Регулирования обеспечивают поддержку, чтобы hello кластера можно использовать ресурсы toostabilize - вернитесь узлы hello, автоматическое восстановление секций сети hello, исправленный bits развертывается.

toohelp такого рода ситуациях hello диспетчер ресурсов кластера Service Fabric включает несколько регулирования. Все это достаточно масштабные средства. Обычно они не должны изменяться без тщательного планирования и тестирования.

При изменении ограничителей hello диспетчер ресурсов кластера его необходимо настроить их tooyour ожидаемый реальную нагрузку. Можно определить, необходимые toohave некоторые регулирует на месте, даже если это означает, что кластера hello занимает больше времени, toostabilize в некоторых ситуациях. Проверка является обязательным toodetermine hello правильные значения для регулирования. Интервалы повтора должны toobe находится достаточно высоко tooallow hello кластера toorespond toochanges в разумные сроки, а нижнее достаточно tooactually предотвращения слишком большой объем потребления ресурсов. 

Большую часть времени hello, мы видели клиентов используйте ограничителей которого она была, так как они уже были в ограниченной среде ресурсов. Некоторые примеры, будет ограниченной пропускной способности сети для отдельных узлов или диски, которые не могут toobuild много реплики с отслеживанием состояния в параллельных из-за ограничения toothroughput. Без регулирования операции может переполнить эти ресурсы, вызывая toofail операций или медленно. В таких ситуациях пользователи используется ограничителей и знал, что они расширение hello количество времени, потребуется tooreach кластера hello стабильного состояния. и что регулирование может привести к понижению общей надежности.


## <a name="configuring-hello-throttles"></a>Настройка регулирования hello

Service Fabric имеет два механизма регулирования hello число перемещений реплики. механизм по умолчанию Hello, существовавшие до Service Fabric 5.7 представляет регулирования в виде абсолютного числа перемещений разрешено. Это подходит не для всех размеров кластеров. В частности для больших кластеров hello значения по умолчанию значение может быть слишком мал, значительно замедляя Балансировка даже в том случае, когда это необходимо, при необходимости в более мелкие кластеры не влияет. Этот механизм предыдущих был заменен по проценту регулирования, масштабирует лучше при динамической кластеров, в какой номер hello служб и регулярно менять узлов.

Hello ограничителей основаны на процент hello число реплик в кластерах hello. Производится на основе Percetage включить выражения hello правило: «не перемещать более 10% реплик в течение 10 минут», например.

параметры конфигурации Hello процентных регулирования не:

  - GlobalMovementThrottleThresholdPercentage - максимальное число перемещений допускается в кластер в любое время, выраженное в процентном допустимое количество реплик в кластере hello. Значение 0 означает, что ограничения отсутствуют. значение по умолчанию Hello — 0. Если GlobalMovementThrottleThreshold и этот параметр заданы, то hello меньшем ограничение будет использоваться.
  - GlobalMovementThrottleThresholdPercentageForPlacement - максимальное число перемещений допускается во время фазы размещения hello, выраженное в процентах общему количеству реплики в кластере hello. Значение 0 означает, что ограничения отсутствуют. значение по умолчанию Hello — 0. Если GlobalMovementThrottleThresholdForPlacement и этот параметр заданы, то hello меньшем ограничение будет использоваться.
  - GlobalMovementThrottleThresholdPercentageForBalancing - максимальное число перемещений, разрешены в ходе hello балансировки этап, выраженное в процентах общему количеству реплики в кластере hello. Значение 0 означает, что ограничения отсутствуют. значение по умолчанию Hello — 0. Если GlobalMovementThrottleThresholdForBalancing и этот параметр заданы, то hello меньшем ограничение будет использоваться.

При указании hello скорости в процентах, следует указать как 0,05 5%. Интервал приветствия, на котором определены эти регулирования — hello GlobalMovementThrottleCountingInterval, который указывается в секундах.


``` xml
<Section Name="PlacementAndLoadBalancing">
     <Parameter Name="GlobalMovementThrottleThresholdPercentage" Value="0" />
     <Parameter Name="GlobalMovementThrottleThresholdPercentageForPlacement" Value="0" />
     <Parameter Name="GlobalMovementThrottleThresholdPercentageForBalancing" Value="0" />
     <Parameter Name="GlobalMovementThrottleCountingInterval" Value="600" />
</Section>
```

Для автономных развертываний используется ClusterConfig.json, а для размещенных в Azure кластеров — Template.json.

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "GlobalMovementThrottleThresholdPercentage",
          "value": "0.0"
      },
      {
          "name": "GlobalMovementThrottleThresholdPercentageForPlacement",
          "value": "0.0"
      },
      {
          "name": "GlobalMovementThrottleThresholdPercentageForBalancing",
          "value": "0.0"
      },
      {
          "name": "GlobalMovementThrottleCountingInterval",
          "value": "600"
      }
    ]
  }
]
```

### <a name="default-count-based-throttles"></a>Регулирование на основе количества по умолчанию
Эти сведения предоставляются на случай, если у вас имеются устаревшие кластеры или в обновленных кластерах по-прежнему используются такие конфигурации. Как правило рекомендуется, они заменяются hello процентных ограничителей выше. Так процентных регулирования отключена по умолчанию, эти регулирования остаются hello регулирования по умолчанию для кластера, пока отключаются и заменены ограничителей процентных hello. 

  - GlobalMovementThrottleThreshold — этот параметр управляет hello общее число перемещений в кластере hello через некоторое время. Hello количество времени, указывается в секундах в виде hello GlobalMovementThrottleCountingInterval. значение по умолчанию Hello hello GlobalMovementThrottleThreshold равно 1000 и значение по умолчанию hello hello GlobalMovementThrottleCountingInterval равно 600.
  - MovementPerPartitionThrottleThreshold — этот параметр управляет hello общее число перемещений для любого раздела службы через некоторое время. Hello количество времени, указывается в секундах в виде hello MovementPerPartitionThrottleCountingInterval. значение по умолчанию Hello hello MovementPerPartitionThrottleThreshold равно 50 и значение по умолчанию hello hello MovementPerPartitionThrottleCountingInterval равно 600.

Конфигурация Hello эти hello следующим регулирования, же шаблон как hello процентных регулирования.

## <a name="next-steps"></a>Дальнейшие действия
- toofind out о управляет hello диспетчер ресурсов кластера и балансировку нагрузки в кластере hello Извлеките hello статьи на [балансировки нагрузки](service-fabric-cluster-resource-manager-balancing.md)
- Hello диспетчер ресурсов кластера позволяет настраивать различные параметры для описания кластера hello. toofind подробные сведения о них, извлеките в этой статье на [описания кластера Service Fabric](service-fabric-cluster-resource-manager-cluster-description.md)
