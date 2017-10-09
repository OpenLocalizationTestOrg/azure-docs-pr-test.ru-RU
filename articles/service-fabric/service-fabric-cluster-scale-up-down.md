---
title: "кластер Service Fabric aaaScale in или out | Документы Microsoft"
description: "Масштабирование кластера Service Fabric in или out запросу toomatch правилами автоматического масштабирования для каждого шкалы набор узлов типа или виртуальная машина. Добавление или удаление кластера Service Fabric tooa узлов"
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: aeb76f63-7303-4753-9c64-46146340b83d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/22/2017
ms.author: chackdan
ms.openlocfilehash: 37cfeaf80edc016cf6de017d1c2dc6fbcb8acc2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-service-fabric-cluster-in-or-out-using-auto-scale-rules"></a>Масштабирование кластера Service Fabric с помощью правил автомасштабирования
Наборы масштабирования виртуальных машин являются ресурсом вычислений Azure можно использовать toodeploy и управлять коллекцией виртуальных машин как набор. Каждый тип узла, определенный в кластере Service Fabric, настроен как отдельный масштабируемый набор виртуальных машин. Каждый тип узла поддерживает возможность независимого масштабирования, имеет разные наборы открытых портов и собственные метрики емкости. Дополнительные сведения о нем в hello [nodetypes Service Fabric](service-fabric-cluster-nodetypes.md) документа. Так как типы узлов Service Fabric hello в кластере состоят из набора масштабирования виртуальной машины в серверной части hello, необходимы tooset автоматически масштабировать правила для каждого узла типа или виртуальная машины масштабного набора.

> [!NOTE]
> Подписки должен иметь достаточно tooadd ядер hello новые виртуальные машины, входящие в состав этого кластера. Чтобы получить сбой время развертывания, если обнаруживаются любые hello квоты в настоящее время отсутствует проверка модели.
> 
> 

## <a name="choose-hello-node-typevirtual-machine-scale-set-tooscale"></a>Выберите тип узла hello или виртуальная машина шкалы набора tooscale
В настоящее время вы не могли toospecify hello автоматически масштабировать правила для набора масштабирования виртуальной машины с помощью портала hello, таким образом сообщить нам использовать типы узлов hello toolist Azure PowerShell (1.0 +) и добавьте toothem правила автоматического масштабирования.

Список hello tooget виртуальной машины в наборе, входящие в состав кластера, запустите следующие командлеты hello:

```powershell
Get-AzureRmResource -ResourceGroupName <RGname> -ResourceType Microsoft.Compute/VirtualMachineScaleSets

Get-AzureRmVmss -ResourceGroupName <RGname> -VMScaleSetName <Virtual Machine scale set name>
```

## <a name="set-auto-scale-rules-for-hello-node-typevirtual-machine-scale-set"></a>Задать правила автоматического масштабирования для набора масштабирования hello узел типа и виртуальных машин
Если кластер имеет несколько типов узлов, затем повторите это действие для каждого типы узел или виртуальная машина шкалы задает требуется tooscale (входящий или исходящий). Учитывает hello учетной записи, количество узлов, которые необходимы до настройки автоматического масштабирования. Минимальное число узлов, которые необходимы для типа первичного узла hello Hello определяется уровень надежности hello выбрано. См. дополнительные сведения об [уровнях надежности](service-fabric-cluster-capacity.md).

> [!NOTE]
> Масштабировании с уменьшением сборки типа hello основного узла, чем минимальное число hello сделать hello кластер работает нестабильно или переведите его в. Это может привести к потере данных для приложений, а также для hello системных служб.
> 
> 

В настоящее время функция автоматического масштабирования hello не определяется загружает hello, что приложения могут сообщать о tooService структуры. Поэтому в это время hello автоматическое масштабирование, получаемых исключительно определяется hello счетчики производительности, создаваемых каждый из экземпляров набора масштабирования виртуальных машин hello.  

Следуйте этим инструкциям [tooset копирование Автомасштабирование для каждого набора масштабирования виртуальных машин](../virtual-machine-scale-sets/virtual-machine-scale-sets-autoscale-overview.md).

> [!NOTE]
> На шкале работу сценария, если узел имеет свой уровень устойчивости Gold или Silver требуется toocall hello [командлет Remove-ServiceFabricNodeState](https://msdn.microsoft.com/library/azure/mt125993.aspx) с именем hello соответствующего узла.
> 
> 

## <a name="manually-add-vms-tooa-node-typevirtual-machine-scale-set"></a>Вручную добавьте виртуальные машины tooa узел типа или виртуальная машина масштабного набора
Выполните образец hello/инструкции hello [коллекции шаблонов краткого](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing) toochange hello число виртуальных машин в каждом Nodetype. 

> [!NOTE]
> Добавление виртуальных машин занимает некоторое время, так не ожидается toobe дополнения hello мгновенно. Поэтому Планирование емкости tooadd также вовремя, tooallow более 10 минут перед hello емкость виртуальной Машины доступен для реплик hello / service разместить tooget экземпляров.
> 
> 

## <a name="manually-remove-vms-from-hello-primary-node-typevirtual-machine-scale-set"></a>Вручную удалите виртуальные машины из набор масштабирования hello основного узла типа или виртуальной машины
> [!NOTE]
> Hello service fabric системные службы выполняются в hello тип основного узла кластера. Меньше, чем уровень надежности какие hello гарантирует так, чтобы никогда не завершена или масштабировать hello число экземпляров в, типы узлов. См. слишком[hello сведения о надежности уровней здесь](service-fabric-cluster-capacity.md). 
> 
> 

Требуется tooexecute hello следующие шаги один экземпляр виртуальной Машины одновременно. Это позволяет для hello системных служб (и служб с отслеживанием состояния) toobe Мягкое отключение экземпляра виртуальной Машины hello, удалении и новых реплик, созданные на других узлах.

1. Запустите [Disable ServiceFabricNode](https://msdn.microsoft.com/library/mt125852.aspx) с намерением «RemoveNode» toodisable hello узлом ты tooremove (hello наибольший экземпляр в этом типе узла).
2. Запустите [Get ServiceFabricNode](https://msdn.microsoft.com/library/mt125856.aspx) toomake убедиться, что этот узел hello перешло на самом деле toodisabled. Если нет, подождите, пока узел hello отключен. Эту операцию невозможно ускорить.
3. Выполните образец hello/инструкции hello [коллекции шаблонов краткого](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing) toochange hello число виртуальных машин на единицу при этом Nodetype. удалить экземпляр Hello имеет наивысший ВМ hello. 
4. Повторите шаги 1 – 3, при необходимости, но никогда не масштабировать hello число экземпляров в hello основного узла типы меньше, чем гарантирует, что какой уровень надежности hello. См. слишком[hello сведения о надежности уровней здесь](service-fabric-cluster-capacity.md). 

## <a name="manually-remove-vms-from-hello-non-primary-node-typevirtual-machine-scale-set"></a>Вручную удалите данные из hello дополнительный узел типа или виртуальная машина масштабный набор виртуальных машин
> [!NOTE]
> Для службы с отслеживанием состояния требуется определенное количество узлов toobe всегда toomaintain доступности и сохранение состояния службы. По крайней мере hello необходимо hello числом узлов равно toohello целевой реплики набора hello секции или службы. 
> 
> 

Требуется hello выполните следующие шаги один экземпляр виртуальной Машины одновременно hello. Это обеспечивает hello системных служб (и служб с отслеживанием состояния) toobe надлежащего прекращения работы на hello экземпляра виртуальной Машины, которые удаляются и else where создания новых реплик.

1. Запустите [Disable ServiceFabricNode](https://msdn.microsoft.com/library/mt125852.aspx) с намерением «RemoveNode» toodisable hello узлом ты tooremove (hello наибольший экземпляр в этом типе узла).
2. Запустите [Get ServiceFabricNode](https://msdn.microsoft.com/library/mt125856.aspx) toomake убедиться, что этот узел hello перешло на самом деле toodisabled. В противном случае дождитесь hello узлов отключено. Эту операцию невозможно ускорить.
3. Выполните образец hello/инструкции hello [коллекции шаблонов краткого](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing) toochange hello число виртуальных машин на единицу при этом Nodetype. Сейчас будут удалены hello наибольший экземпляр виртуальной Машины. 
4. Повторите шаги 1 – 3, при необходимости, но никогда не масштабировать hello число экземпляров в hello основного узла типы меньше, чем гарантирует, что какой уровень надежности hello. См. слишком[hello сведения о надежности уровней здесь](service-fabric-cluster-capacity.md).

## <a name="behaviors-you-may-observe-in-service-fabric-explorer"></a>Возможные варианты поведения в обозревателе Service Fabric
При вертикальном масштабировании hello кластера Service Fabric Explorer отразят hello количество узлов (экземпляров набора масштабирования виртуальных машин), которые являются частью кластера hello.  Тем не менее, при масштабировании кластера вниз вы увидите hello удалены узла или виртуальной Машины, отображаемый в неработоспособное состояние только при вызове [Remove ServiceFabricNodeState cmd](https://msdn.microsoft.com/library/mt125993.aspx) с именем hello соответствующего узла.   

Ниже приводится объяснение hello такого поведения.

Hello узлов, упомянутых в обозреватель Service Fabric — это отражение какие hello Service Fabric системных служб (FM специально) знает о числе узлов hello кластера имели имеет hello. При масштабировании hello набор масштабирования виртуальных машин hello виртуальной Машины была удалена, но FM Системная служба по-прежнему полагает, что этот узел hello (которая была сопоставленных toohello виртуальной Машины, которая была удалена) будут возвращены. Поэтому Service Fabric Explorer продолжается toodisplay этого узла (хотя hello состояние работоспособности может быть ошибка или unknown).

В порядке toomake том, что узел удаляется при удалении виртуальной Машины у вас есть два варианта:

1) Выберите уровень устойчивости Gold или серебряный (доступных скоро) для hello типов узлов в кластере, которое позволяет hello интеграции инфраструктуры. Которой затем автоматически удалит hello узлы из нашей службы (FM) состояние системы при уменьшать масштаб.
См. слишком[hello сведения об уровнях устойчивость здесь](service-fabric-cluster-capacity.md)

2) После усеченная hello экземпляр виртуальной Машины вам потребуется toocall hello [командлет Remove-ServiceFabricNodeState](https://msdn.microsoft.com/library/mt125993.aspx).

> [!NOTE]
> Службы структуры кластеры требуют определенного числа узлов toobe вверх на все время hello в порядке toomaintain доступности и сохранение состояния — ссылка tooas «поддержания кворума». Таким образом, она будет обычно небезопасных tooshut работу всех машин hello в кластере hello, пока вы выполнили сначала [полного резервного копирования состояния](service-fabric-reliable-services-backup-restore.md).
> 
> 

## <a name="next-steps"></a>Дальнейшие действия
После tooalso hello чтения сведения о планирование емкости кластера, обновлением кластера и секций служб:

* [Планирование емкости кластера](service-fabric-cluster-capacity.md)
* [Обновления кластера](service-fabric-cluster-upgrade.md)
* [Секционирование служб с отслеживанием состояния для максимального масштабирования](service-fabric-concepts-partitioning.md)

<!--Image references-->
[BrowseServiceFabricClusterResource]: ./media/service-fabric-cluster-scale-up-down/BrowseServiceFabricClusterResource.png
[ClusterResources]: ./media/service-fabric-cluster-scale-up-down/ClusterResources.png
