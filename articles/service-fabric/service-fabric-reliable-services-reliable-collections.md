---
title: "tooReliable aaaIntroduction коллекций с отслеживанием состояния служб Azure Service Fabric | Документы Microsoft"
description: "С отслеживанием состояния службы Service Fabric обеспечивают надежный коллекций, которые позволяют toowrite высокой доступны, масштабируемый и низкой задержкой облачных приложений."
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: masnider,rajak
ms.assetid: 62857523-604b-434e-bd1c-2141ea4b00d1
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/1/2017
ms.author: mcoskun
ms.openlocfilehash: 9f67c48f13e8b91b84977e127e2545cbb9d9a158
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooreliable-collections-in-azure-service-fabric-stateful-services"></a>Введение tooReliable коллекций с отслеживанием состояния служб Azure Service Fabric
Надежные коллекций позволяют toowrite высокой доступны, масштабируемый и низкой задержкой облачных приложений так, будто бы вы создавали приложения на одном компьютере. Здравствуйте, классы в hello **Microsoft.ServiceFabric.Data.Collections** пространства имен предоставляют набор коллекций, обеспечить высокую надежность состояния. Разработчики должны только toohello tooprogram надежные API-интерфейсов коллекции и позволить надежного коллекций управления hello репликации и локальное состояние.

Hello ключевое различие между надежного коллекций и других технологий высокого уровня доступности (например, Redis, служба таблиц Azure и службы очередей Azure) — что hello состояние сохраняется локально в экземпляре службы hello при также выполняется высокой надежности. Это означает следующее:

* Все операции чтения выполняются локально, что позволяет достичь низкой задержки и высокой пропускной способности при чтении.
* Все операции записи существенно hello минимальное количество операций ввода-вывода сети, что приводит к низкой задержкой и высокой пропускной способностью записывает.

![Изображение развития коллекций.](media/service-fabric-reliable-services-reliable-collections/ReliableCollectionsEvolution.png)

Надежные коллекций можно рассматривать как hello развитием hello **System.Collections** классы: новый набор, предназначенных для приложения hello облака и несколькими компьютерами без повышения сложности для коллекций Разработчик Hello. Таким образом, надежные коллекции являются:

* реплицируемыми (изменения состояния реплицируются для обеспечения высокой доступности);
* PERSISTED: Данные — это материализованный toodisk для обеспечения надежности от крупных сбоев (например, отключения питания центра обработки данных).
* Асинхронное: API-интерфейсы являются асинхронной tooensure не блокируются потоков при дополнительных операций ввода-ВЫВОДА.
* Транзакций: API-интерфейсы используют абстракции hello транзакций, можно легко управлять несколько надежного коллекций в службе.

Надежная согласованность гарантирует недостаточно toomake поле hello рассуждения о состоянии приложения проще обеспечивают надежный коллекций.
Строгая согласованность достигается за счет того, транзакции, которую фиксации завершения только после того, вся транзакция hello выполнил вход кворума большинства реплик, включая основной hello.
tooachieve слабый согласованности, приложения можно подтвердить задней toohello клиента и инициатора запроса перед возвратом hello асинхронной фиксации.

Hello надежного коллекций API-интерфейсы являются развитием параллельных коллекций API-интерфейсы (в hello **System.Collections.Concurrent** пространства имен):

* Асинхронные: Возвращает задачу, поскольку в отличие от параллельных коллекций операций hello реплицируются и сохраняются.
* Параметры out не: использует `ConditionalValue<T>` tooreturn bool и значение, а не выходные параметры. `ConditionalValue<T>`Подобно `Nullable<T>` , но не требует toobe T структуры.
* Транзакции: Использует транзакции объекта tooenable hello toogroup действия пользователя в нескольких коллекциях надежного транзакции.

Сейчас пространство имен **Microsoft.ServiceFabric.Data.Collections** содержит три коллекции:

* [надежный словарь](https://msdn.microsoft.com/library/azure/dn971511.aspx) (реплицируемая, транзакционная и асинхронная коллекция пар "ключ-значение"; Аналогичные слишком**ConcurrentDictionary**, оба hello ключ и значение hello может быть любого типа.
* [надежная очередь](https://msdn.microsoft.com/library/azure/dn971527.aspx) (реплицируемая, транзакционная и асинхронная очередь, функционирующая строго по методу FIFO; Аналогичные слишком**ConcurrentQueue**, hello значение может быть любого типа.
* [Надежная параллельная очередь](service-fabric-reliable-services-reliable-concurrent-queue.md) — реплицируемая, транзакционная и асинхронная упорядочивающая очередь для обеспечения высокой пропускной способности. Аналогичные toohello **ConcurrentQueue**, hello значение может быть любого типа.

## <a name="next-steps"></a>Дальнейшие действия
* [Reliable Collections: руководства и рекомендации](service-fabric-reliable-services-reliable-collections-guidelines.md)
* [Работа с Reliable Collections](service-fabric-work-with-reliable-collections.md)
* [Транзакции и блокировки](service-fabric-reliable-services-reliable-collections-transactions-locks.md)
* [Внутренние компоненты Reliable State Manager и Reliable Collections](service-fabric-reliable-services-reliable-collections-internals.md)
* Управление данными
  * [Резервное копирование и восстановление](service-fabric-reliable-services-backup-restore.md)
  * [Notifications](service-fabric-reliable-services-notifications.md)
  * [Сериализация надежной коллекции](service-fabric-reliable-services-reliable-collections-serialization.md)
  * [Влияние сериализации данных на обновление приложений](service-fabric-application-upgrade-data-serialization.md)
  * [Конфигурация диспетчера надежных состояний](service-fabric-reliable-services-configuration.md)
* Прочее
  * [Краткое руководство по надежным службам Reliable Services](service-fabric-reliable-services-quick-start.md)
  * [Справочник разработчика по надежным коллекциям](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
