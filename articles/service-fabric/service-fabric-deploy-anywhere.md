---
title: "aaaCreate Azure Service Fabric кластеров в Windows Server и Linux | Документы Microsoft"
description: "Кластеров Service Fabric на Windows Server и Linux, поэтому вы будете иметь доступ приложения Service Fabric toodeploy и узла в любом месте, вы можете запустить сервер Windows или Linux."
services: service-fabric
documentationcenter: .net
author: Chackdan
manager: timlt
editor: 
ms.assetid: 19ca51e8-69b9-4952-b4b5-4bf04cded217
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/08/2017
ms.author: chackdan
ms.openlocfilehash: 46d5f3d019339c57a0024f5a9d47d9018cca01a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-service-fabric-clusters-on-windows-server-or-linux"></a>Создание кластеров Service Fabric в Windows Server или Linux
Кластер Azure Service Fabric — это подключенный к сети набор виртуальных машин или физических компьютеров, в котором вы развертываете микрослужбы и управляете ими. Узлом кластера называется компьютер или виртуальная машина, которая входит в состав кластера. Кластеры можно масштабировать toothousands узлов. При добавлении новых узлов toohello кластера Service Fabric балансировку реплики разделов службы hello и экземпляров через hello увеличить количество узлов. В целом улучшает производительность приложения и уменьшает конкуренцию за toomemory доступа. Если hello узлов в кластере hello эффективно не используются, можно уменьшить hello количество узлов в кластере hello. Service Fabric снова балансировку реплики разделов hello и экземпляров, в рамках hello уменьшить количество узлов toomake более эффективного использования оборудования hello на каждом узле.

Service Fabric позволяет создавать hello кластеров Service Fabric на виртуальных машинах или компьютерах под управлением Windows Server или Linux. Это означает, может toodeploy и запустить приложения Service Fabric в любой среде, где есть набор компьютеров Windows Server или Linux, которые связаны между собой, будь то в локальной среде Microsoft Azure или с любого поставщика облачных служб.

## <a name="create-service-fabric-clusters-on-azure"></a>Создание кластеров Service Fabric в Azure
Для создания кластера в Azure выполняется через модель ресурсов шаблона или hello портал Azure. Чтение [создание кластера Service Fabric с помощью шаблона диспетчера ресурсов](service-fabric-cluster-creation-via-arm.md) или [создание кластера Service Fabric из портала Azure hello](service-fabric-cluster-creation-via-portal.md) для получения дополнительной информации.

## <a name="supported-operating-systems-for-clusters-on-azure"></a>Поддерживаемые операционные системы для кластеров в Azure
Сейчас будет toocreate кластеров на виртуальные машины под управлением этих операционных систем:

* Windows Server 2012 R2
* Windows Server 2016 
* Ubuntu Linux 16.04 (общедоступная предварительная версия). 

## <a name="create-service-fabric-standalone-clusters-on-premises-or-with-any-cloud-provider"></a>Создание автономных кластеров Service Fabric локально или у другого поставщика облачных служб
Service Fabric предоставляет пакета установки вы toocreate автономный Service Fabric кластеров в локальной среде или на любой поставщика облачных служб

Дополнительные сведения о настройке автономных кластеров Service Fabric в Windows Server см. в статье [Создание кластера под управлением Windows Server и управление им](service-fabric-cluster-creation-for-windows-server.md).

### <a name="any-cloud-deployments-vs-on-premises-deployments"></a>Сравнение локальных и облачных развертываний
Hello процесс создания локального кластера Service Fabric — аналогичные toohello процесс создания кластера в любом облаке по своему усмотрению с набором виртуальных машин. hello облачного поставщика или в локальной среде, в которых используется управляются Hello начальных этапах tooprovision hello виртуальных машин. Получив набор виртуальных машин с сетевого подключения включен между ними, затем hello tooset действия пакет Service Fabric hello, изменить параметры кластера hello и запустить процесс создания кластера hello и скрипты управления идентичны. Это гарантирует, что знания и опыт эксплуатации и управлению кластерами Service Fabric может передаваться при выборе tootarget новой среды размещения.

### <a name="benefits-of-creating-standalone-service-fabric-clusters"></a>Преимущества создания автономных кластеров Service Fabric
* Являются свободного toochoose любой облако поставщика toohost кластера.
* Service Fabric приложениях, один раз, может выполняться в нескольких средах размещения, с минимальными toono изменениями.
* Знания о построении приложений Service Fabric переносится из одного размещения tooanother среды.
* Эксплуатационные качества запуска и управления Service Fabric кластерах выполняет над из одной среды tooanother.
* Широкий охват клиентов не ограничен средой размещения.
* Обеспечивает дополнительный уровень надежности и защиты от сбоев широко существует, потому что можно перемещать службы hello над tooanother среду развертывания, если центр обработки данных или поставщика облачных служб имеет отключения.

## <a name="supported-operating-systems-for-standalone-clusters"></a>Поддерживаемые операционные системы для автономных кластеров
Сейчас будет toocreate кластеров на виртуальные машины или компьютеры под управлением этих операционных систем:

* Windows Server 2012 R2
* Windows Server 2016 
* Linux (ожидается в ближайшее время).

## <a name="advantages-of-service-fabric-clusters-on-azure-over-standalone-service-fabric-clusters-created-on-premises"></a>Преимущества кластеров Service Fabric в Azure над автономными кластерами Service Fabric, созданными локально
Запуск кластеров Service Fabric в Azure предоставляет преимущества по сравнению с hello локальный вариант, поэтому если у вас нет конкретных потребностей, для которой запущена кластеров, рекомендуется выполнять в Azure. В Azure обеспечивают интеграцию с другими компоненты Azure и служб, которые делает операций кластера и управление им hello проще и надежнее.

* **Портал Azure:** портал Azure позволяет легко toocreate кластеров и управления ими.
* **Диспетчер ресурсов Azure:** использование диспетчера ресурсов Azure позволяет легко управлять все ресурсы, используемые hello кластера как единое целое и упрощает отслеживание стоимость и выставление счетов.
* **Кластер Service Fabric как ресурс Azure:** кластер Service Fabric является ресурсом ARM, поэтому его можно моделировать, как и другие ресурсы ARM в Azure.
* **Интеграцию с инфраструктурой Azure** Service Fabric координирует с hello базовой инфраструктуры Azure для операционной системы, сети и другие обновления tooimprove доступности и надежность приложений.  
* **Диагностика:** в Azure мы предоставляем интеграцию с системой диагностики Azure и Log Analytics.
* **Автоматическое масштабирование:** для кластеров в Azure, мы предоставляем встроенную функцию автоматического масштабирования из-за tooVirtual машины-наборы масштабирования. В локальных и других облачных средах имеется toobuild собственные автоматического масштабирования компонент или масштаб вручную с помощью hello API, которые предоставляет Service Fabric для масштабирования кластеров.

## <a name="next-steps"></a>Дальнейшие действия

* Создание кластера на основе виртуальных машин или компьютеров под управлением Windows Server: [Create an Azure Service Fabric cluster on-premises or in the cloud](service-fabric-cluster-creation-for-windows-server.md)
* Создание кластера на основе виртуальных машин или компьютеров под управлением Linux: [Service Fabric в Linux](service-fabric-linux-overview.md)
* [Сведения о вариантах поддержки Service Fabric](service-fabric-support.md)

