---
title: "aaaService структуры и типов узлов набора масштабирования виртуальных Машин | Документы Microsoft"
description: "Описывает, как типы узлов Service Fabric связаны наборы tooVM масштабирования и способ подключения tooremote tooa набора масштабирования виртуальных Машин экземпляра или узла кластера."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 5441e7e0-d842-4398-b060-8c9d34b07c48
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/05/2017
ms.author: chackdan
ms.openlocfilehash: 830ea2816f5864de146a77483c85de26f91c2425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="hello-relationship-between-service-fabric-node-types-and-virtual-machine-scale-sets"></a>Hello связь между Service Fabric типы узлов и наборы масштабирования виртуальных машин
Наборы масштабирования виртуальных машин, Azure Compute ресурсов можно использовать toodeploy и управлять коллекцией виртуальных машин как набор. Каждый тип узла, определенный в кластере Service Fabric, настроен как отдельный набор масштабирования виртуальных машин. Каждый тип узла поддерживает возможность независимого масштабирования, имеет разные наборы открытых портов и собственные метрики емкости.

Следующий снимок экрана приветствия показан кластер с двумя типами узлов: внешнего и внутреннего.  Каждый тип узла имеет пять узлов.

![Снимок экрана с двумя типами узлов][NodeTypes]

## <a name="mapping-vm-scale-set-instances-toonodes"></a>Сопоставление toonodes экземпляров набора масштабирования виртуальных Машин
Как видно выше hello набора масштабирования виртуальных Машин экземпляры начинаются с экземпляра 0, а затем возрастает. Нумерация Hello отражается в имена hello. Например BackEnd_0 — экземпляр 0 hello набора масштабирования виртуальных Машин серверной части. Этот конкретный масштабируемый набор ВМ имеет пять экземпляров с именами BackEnd_0, BackEnd_1, BackEnd_2, BackEnd_3 и BackEnd_4.

При увеличении масштаба масштабируемого набора ВМ создается новый экземпляр. Имя экземпляра нового набора масштабирования виртуальных Машин Hello обычно будет имя набора масштабирования виртуальных Машин hello + hello следующий номер экземпляра. В нашем примере это BackEnd_5.

## <a name="mapping-vm-scale-set-load-balancers-tooeach-node-typevm-scale-set"></a>Сопоставление виртуальной Машины набора масштабирования загрузить балансировки нагрузки tooeach узел типа или виртуальной Машины набора масштабирования
Если вы развернули кластера с портала hello или использовали шаблона диспетчера ресурсов образец hello, мы предоставлен, затем при получении списка всех ресурсов в группе ресурсов вы увидите hello подсистему балансировки нагрузки для каждого типа узла или набора масштабирования виртуальных Машин.

Hello имя будет примерно так: **балансировки Нагрузки -&lt;имя NodeType&gt;**. Например, LB-sfcluster4doc-0, как показано на следующем снимке экрана:

![Ресурсы][Resources]

## <a name="remote-connect-tooa-vm-scale-set-instance-or-a-cluster-node"></a>Удаленное подключение tooa набора масштабирования виртуальных Машин экземпляра или узла кластера
Каждый тип узла, определенный в кластере, настроен как отдельный набор масштабирования виртуальных машин.  Что означает hello типов узлов может масштабироваться вверх или вниз независимо друг от друга и может быть выполнен из различных конфигураций виртуальных Машин. В отличие от одного экземпляра виртуальные машины экземпляры набора масштабирования виртуальных Машин hello не получают виртуальный IP-адрес своих собственных. Поэтому он может быть немного сложной задачей, если вам нужны дополнительные IP-адреса адрес и номер порта, которые можно использовать tooremote подключения tooa конкретного экземпляра.

Ниже приведены шаги hello, можно выполнить toodiscover их.

### <a name="step-1-find-out-hello-virtual-ip-address-for-hello-node-type-and-then-inbound-nat-rules-for-rdp"></a>Шаг 1: Узнайте hello виртуальный IP-адрес для hello типа узла, а затем правила NAT для входящего трафика для протокола удаленного рабочего СТОЛА
В порядке tooget потребуется tooget hello NAT для входящего трафика правила значения, которые были определены как часть определения ресурса hello **Microsoft.Network/loadBalancers**.

Hello портала перейдите в колонку подсистемы балансировки нагрузки toohello и затем **параметры**.

![LBBlade][LBBlade]

В разделе **Параметры** щелкните **Правила NAT для входящего трафика**. Теперь предоставляет hello IP-адреса и порта, которые можно использовать tooremote подключения toohello первый экземпляр набора масштабирования виртуальных Машин. В приведенном далее снимке экрана приветствия, это **104.42.106.156** и **3389**

![NATRules][NATRules]

### <a name="step-2-find-out-hello-port-that-you-can-use-tooremote-connect-toohello-specific-vm-scale-set-instancenode"></a>Шаг 2: Узнайте hello портов, которые можно использовать tooremote подключение toohello определенного набора масштабирования виртуальных Машин и узла экземпляра
Ранее в этом документе описывалось сопоставление узлов toohello hello экземпляров набора масштабирования виртуальных Машин. Мы будем использовать этот toofigure out hello точный номер порта.

порты Hello выделяются в порядке возрастания hello экземпляра набора масштабирования виртуальных Машин. Таким образом в нашем примере для hello интерфейсный тип узла hello портов для каждого из пяти экземпляров hello являются следующие hello. Вы теперь toodo требуется hello одно сопоставление для экземпляра набора масштабирования виртуальных Машин.

| **Экземпляр масштабируемого набора ВМ** | **Порт** |
| --- | --- |
| FrontEnd_0 |3389 |
| FrontEnd_1 |3390 |
| FrontEnd_2 |3391 |
| FrontEnd_3 |3392 |
| FrontEnd_4 |3393 |
| FrontEnd_5 |3394 |

### <a name="step-3-remote-connect-toohello-specific-vm-scale-set-instance"></a>Шаг 3: Удаленное подключение toohello конкретного экземпляра набора масштабирования виртуальных Машин
В следующем снимке экрана приветствия используется удаленный рабочий стол tooconnect toohello FrontEnd_1:

![RDP][RDP]

## <a name="how-toochange-hello-rdp-port-range-values"></a>Как toochange hello RDP-порту диапазон значений
### <a name="before-cluster-deployment"></a>Перед развертыванием кластера
При настройке кластера hello, с помощью шаблона диспетчера ресурсов, можно указать диапазон hello в hello **inboundNatPools**.

Go определения ресурса toohello **Microsoft.Network/loadBalancers**. В списке, найдите описание hello **inboundNatPools**.  Замените hello *frontendPortRangeStart* и *значение frontendPortRangeEnd* значения.

![inboundNatPools][InboundNatPools]

### <a name="after-cluster-deployment"></a>После развертывания кластера
Это немного сложнее и может привести к перезаписывание ВМ hello. Теперь вы можете tooset новые значения с помощью Azure PowerShell. Убедитесь, что на компьютере установлена среда Azure PowerShell 1.0 или более поздней версии. Если вы не выполнили это перед, настоятельно рекомендуется выполнить hello действия, описанные в [как tooinstall и настройка Azure PowerShell.](/powershell/azure/overview)

Войдите в tooyour учетная запись Azure. Если команды PowerShell по какой-то причине завершаются неудачно, проверьте, правильно ли установлен Azure PowerShell.

```
Login-AzureRmAccount
```

Запустите hello, приведенные ниже сведения tooget на балансировки нагрузки и отображаются значения hello hello описание **inboundNatPools**:

```
Get-AzureRmResource -ResourceGroupName <RGname> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load balancer name>
```

Теперь значение *значение frontendPortRangeEnd* и *frontendPortRangeStart* toohello значения, которые требуются.

```
$PropertiesObject = @{
    #Property = value;
}
Set-AzureRmResource -PropertyObject $PropertiesObject -ResourceGroupName <RG name> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load Balancer name> -ApiVersion <use hello API version that get returned> -Force
```


## <a name="next-steps"></a>Дальнейшие действия
* [Обзор компонента «В любом развертывание» hello и сравнение с кластерами под управлением Azure](service-fabric-deploy-anywhere.md)
* [Безопасность кластера](service-fabric-cluster-security.md)
* [ Пакет SDK для Service Fabric и начало работы](service-fabric-get-started.md)

<!--Image references-->
[NodeTypes]: ./media/service-fabric-cluster-nodetypes/NodeTypes.png
[Resources]: ./media/service-fabric-cluster-nodetypes/Resources.png
[InboundNatPools]: ./media/service-fabric-cluster-nodetypes/InboundNatPools.png
[LBBlade]: ./media/service-fabric-cluster-nodetypes/LBBlade.png
[NATRules]: ./media/service-fabric-cluster-nodetypes/NATRules.png
[RDP]: ./media/service-fabric-cluster-nodetypes/RDP.png
