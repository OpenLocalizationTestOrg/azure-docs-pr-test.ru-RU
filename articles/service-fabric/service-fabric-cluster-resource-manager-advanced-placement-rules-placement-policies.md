---
title: "aaaService диспетчер ресурсов кластера структуры - политики размещения | Документы Microsoft"
description: "Общие сведения о дополнительных политиках размещения и правилах для служб Service Fabric"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 5c2d19c6-dd40-4c4b-abd3-5c5ec0abed38
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: bb58642520085ab3000f3929cf9aea7a8f6e3070
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="placement-policies-for-service-fabric-services"></a>Политики размещения для служб Service Fabric
Политики размещения, дополнительные правила, которые могут быть используется toogovern размещение службы в некоторых конкретных, менее типичных сценариях. Вот несколько примеров.

- Кластер Service Fabric охватывает значительные географические расстояния. Например, он распределен между несколькими локальными центрами обработки данных или регионами Azure.
- Среде охватывает несколько областей геополитические или юридическое элемента управления, или в другой ситуации при наличии границы политики необходимо tooenforce
- Существуют рекомендации производительность и задержка связи из-за toolarge расстояния или использование медленнее или менее надежной связи.
- Требуется tookeep уверенности, что совместного размещения рабочих нагрузок, как максимум усилий с другими рабочими нагрузками или в toocustomers выражение с учетом расположения

Большинство этих требований выравнивание с физическим размещением hello кластера hello, представленные hello домены сбоя кластера hello. 

Hello Углубленное изучение политик, которые позволяют адрес к таким сценариям относятся:

1. с недопустимыми доменами;
2. с обязательными доменами;
3. с предпочтительными доменами;
4. при запрете упаковки реплик.

Большинство hello следующие элементы управления могут настраиваться с помощью свойства узла и ограничения размещения, но некоторые являются более сложным. toomake предметах проще hello диспетчер ресурсов кластера Service Fabric предоставляет эти дополнительные размещения политики. Политики размещения настаиваются для отдельных экземпляров именованных служб. Они могут также обновляться динамически.

## <a name="specifying-invalid-domains"></a>Указание недопустимых доменов
Hello **InvalidDomain** политика размещения позволяет toospecify недоступность определенного домена сбоя для конкретной службы. Эта политика предотвращает выполнение определенной службы в определенном регионе, что может быть связано с геополитическими причинами или корпоративной политикой организации. Используя отдельные политики, можно указать несколько недопустимых доменов.

<center>
![Пример недопустимого домена][Image1]
</center>

Код:

```csharp
ServicePlacementInvalidDomainPolicyDescription invalidDomain = new ServicePlacementInvalidDomainPolicyDescription();
invalidDomain.DomainName = "fd:/DCEast"; //regulations prohibit this workload here
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

PowerShell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("InvalidDomain,fd:/DCEast”)
```
## <a name="specifying-required-domains"></a>Указание обязательных доменов
Размещение политика домена требует, что служба hello присутствует только в указанных доменах hello обязательные Hello. Используя отдельные политики, можно указать несколько обязательных доменов.

<center>
![Пример обязательного домена][Image2]
</center>

Код:

```csharp
ServicePlacementRequiredDomainPolicyDescription requiredDomain = new ServicePlacementRequiredDomainPolicyDescription();
requiredDomain.DomainName = "fd:/DC01/RK03/BL2";
serviceDescription.PlacementPolicies.Add(requiredDomain);
```

PowerShell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomain,fd:/DC01/RK03/BL2")
```

## <a name="specifying-a-preferred-domain-for-hello-primary-replicas-of-a-stateful-service"></a>Указание основной домен для hello основной реплики службы с отслеживанием состояния
Hello предпочитаемый основного домена указывает tooplace домена сбоя hello hello Primary in. Hello основной заканчивается в этом домене, когда все, что находится в работоспособном состоянии. Если домен hello или hello первичной реплики завершается ошибкой или завершает работу, hello основной перемещает toosome другое местоположение, в идеальном случае в hello того же домена. Если это новое местоположение не в домене предпочтительный hello, hello диспетчер ресурсов кластера переходит обратно предпочтительный домена toohello как можно быстрее. Обычно этот параметр имеет смысл только для служб с отслеживанием состояния. Эту политику особенно полезно использовать в кластерах, которые охватывают несколько регионов Azure или центров обработки данных, но содержат службы, для которых предпочтительно размещение в определенном расположении. Сохранение в источниках закройте tootheir пользователи или другие службы, который помогает обеспечивать более низкой задержке, особенно для операций чтения, которые обрабатываются первичные цвета по умолчанию.

<center>
![Предпочтительные домены для первичных реплик и отработка отказа][Image3]
</center>

```csharp
ServicePlacementPreferPrimaryDomainPolicyDescription primaryDomain = new ServicePlacementPreferPrimaryDomainPolicyDescription();
primaryDomain.DomainName = "fd:/EastUS/";
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

PowerShell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("PreferredPrimaryDomain,fd:/EastUS")
```

## <a name="requiring-replica-distribution-and-disallowing-packing"></a>Требование распределения реплик и запрещение группирования
Реплика — _обычно_ распределения в доменах сбоя и обновления при hello кластера находится в работоспособном состоянии. Тем не менее существуют ситуации, в которых более одной реплики для заданной секции может быть временно сгруппировано в одном домене. Например, предположим, что этот кластер hello имеет девять узлов в трех ошибочных доменах, fd: / 0, fd: / 1 и fd: / 2. Предположим, что у вашей службы три реплики. Предположим, что hello узлы, которые использовались для этих реплик в fd: / 1 и fd: / 2 вышел из строя. Обычно hello диспетчер ресурсов кластера хотите использовать другие узлы в тех же доменах сбоя. В этом случае предположим, что из-за проблем с toocapacity none hello использовались другие узлы в этих доменах. Если диспетчер ресурсов кластера hello построение выполнено замен для этих реплик, он будет иметь toochoose узла в fd: / 0. Тем не менее, выполнив _,_ возникает ситуация, где нарушается ограничение домен сбоя hello. Упаковки реплик увеличивается вероятность hello hello всей реплика может сократиться или будут утеряны. 

> [!NOTE]
> Дополнительные сведения об общих ограничениях и приоритетах ограничений см. в [этом разделе](service-fabric-cluster-resource-manager-management-integration.md#constraint-priorities).
>

Если вы увидели сообщение о работоспособности наподобие такого: `hello Load Balancer has detected a Constraint Violation for this Replica:fabric:/<some service name> Secondary Partition <some partition ID> is violating hello Constraint: FaultDomain`, это значит, что у вас возникла описанная ошибка или сходная с ней. Обычно временно группируется только одна или две реплики. Пока число реплик в заданном домене не превышает кворум, все в порядке. Упаковки редко, но это может случиться, и обычно такие ситуации являются временными, так как узлы hello вернуться. Если узлы hello оставаться вниз и hello диспетчер ресурсов кластера должна toobuild замены, обычно существуют другие узлы в доменах сбоя идеальный hello.

Для некоторых рабочих нагрузок предпочитаете всегда с числом hello целевой реплики, даже если они упакованы в небольшого числа доменов. Такие рабочие нагрузки обеспечивают защиту от общего числа постоянных одновременных сбоев в домене, позволяя восстановить локальное состояние. Другие рабочие нагрузки вместо займет время простоя hello более ранних, чем правильность риска и потери данных. Большинство производственных рабочих нагрузок работает больше чем с тремя репликами, больше чем с тремя доменами сбоя и множеством допустимых узлов в каждом домене сбоя. По этой причине поведение по умолчанию hello позволяет упаковки домена по умолчанию. поведение по умолчанию Hello позволяет обычный балансировки и toohandle отработки отказа эти крайних случаях, даже если это означает упаковки временный домен.

Если вы хотите toodisable такой способ упаковки для заданной рабочей нагрузки, можно указать hello `RequireDomainDistribution` политики службы hello. Если этот параметр установлен, hello диспетчер ресурсов кластера гарантирует не две реплики из hello запуск одной секции в hello же ошибок или домен обновления.

Код:

```csharp
ServicePlacementRequireDomainDistributionPolicyDescription distributeDomain = new ServicePlacementRequireDomainDistributionPolicyDescription();
serviceDescription.PlacementPolicies.Add(distributeDomain);
```

PowerShell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomainDistribution")
```

Теперь, было бы быть toouse возможных конфигураций службы в кластере, который не был географически охваченных? Можно, но не нужно. Hello конфигурации требуется, недопустимый и основного домена следует избегать, если hello сценарии требуют их. Он не становится все tooforce tootry смысле toorun заданной рабочей нагрузки в одной стойке или tooprefer некоторых сегментов локального кластера на другой. Разные аппаратные конфигурации следует распределить между доменами сбоя и обрабатывать с использованием обычных ограничений размещения и свойств узлов.

## <a name="next-steps"></a>Дальнейшие действия
- Дополнительные сведения о настройке служб см. в разделе [Настройка параметров Cluster Resource Manager для служб Service Fabric](service-fabric-cluster-resource-manager-configure-services.md).

[Image1]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-invalid-placement-domain.png
[Image2]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-required-placement-domain.png
[Image3]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-preferred-primary-domain.png
