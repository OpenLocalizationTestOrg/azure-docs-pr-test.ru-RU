---
title: "aaaAzure ServiceFabric диагностики и мониторинга | Документы Microsoft"
description: "В этой статье описаны функции мониторинга производительности hello в hello надежного ServiceRemoting структуры службы среды выполнения, как счетчики производительности, генерируемой его."
services: service-fabric
documentationcenter: .net
author: suchiagicha
manager: timlt
editor: suchiagicha
ms.assetid: 1c229923-670a-4634-ad59-468ff781ad18
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: suchiagicha
ms.openlocfilehash: 64db9a890bd59a1326e587d14b89c007b71a9059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-and-performance-monitoring-for-reliable-service-remoting"></a>Диагностика и мониторинг производительности в модели Reliable Service Remoting
Среда выполнения надежного ServiceRemoting Hello выдает [счетчики производительности](https://msdn.microsoft.com/library/system.diagnostics.performancecounter.aspx). Они предоставляют подробные сведения о том, как работает hello ServiceRemoting и помогают устранять неполадки и наблюдения за производительностью.


## <a name="performance-counters"></a>Счетчики производительности
Среда выполнения надежного ServiceRemoting Hello определяет hello следующие категории счетчиков производительности:

| Категория | Описание |
| --- | --- |
| Service Fabric Service |Счетчики конкретных tooAzure удаленного взаимодействия службы структуры службы, к примеру, tooprocess среднее время запроса |
| Service Fabric Service Method |Toomethods определенных счетчиков реализуемый служба Service Fabric удаленного взаимодействия, например, как часто вызова метода службы |

Каждый из предыдущих категорий hello имеет один или несколько счетчиков.

Hello [монитора производительности](https://technet.microsoft.com/library/cc749249.aspx) приложение, доступное в ОС Windows hello по умолчанию может быть используется toocollect и представление данных счетчиков производительности. [Диагностика Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) — еще один параметр для сбора данных счетчиков производительности и передачи их tooAzure таблиц.

### <a name="performance-counter-instance-names"></a>Имена экземпляров счетчиков производительности
В кластере, содержащем большое количество служб или секций ServiceRemoting, находится большое количество экземпляров счетчиков производительности. экземпляр счетчика производительности Hello имена могут помочь в идентификации определенной секции hello и метод службы (если применимо), с которым связан этот экземпляр счетчика производительности hello.

#### <a name="service-fabric-service-category"></a>Категория Service Fabric Service
Для категории hello `Service Fabric Service`, имена экземпляров счетчиков hello находятся в hello следующий формат:

`ServiceFabricPartitionID_ServiceReplicaOrInstanceId_ServiceRuntimeInternalID`

*ServiceFabricPartitionID* является строковым представлением hello hello сопоставлен идентификатор секции Service Fabric, hello экземпляр счетчика производительности. Идентификатор секции Hello является идентификатором GUID, и его строковое представление создается с помощью hello [ `Guid.ToString` ](https://msdn.microsoft.com/library/97af8hh4.aspx) метод с описатель формата «D».

*ServiceReplicaOrInstanceId* является строковым представлением hello код реплику или экземпляр структуры службы, hello экземпляр счетчика производительности, связанные с hello.

*ServiceRuntimeInternalID* — hello строковое представление 64-разрядного целого числа, создаваемый средой выполнения Fabric Service hello для внутреннего использования. Это включается в экземпляр счетчика производительности hello его уникальность имени tooensure и избежать конфликтов с другими имена экземпляров счетчиков производительности. Пользователи не пытайтесь выполнить toointerpret эту часть имени экземпляра счетчика производительности hello.

Hello ниже приведен пример имя экземпляра счетчика для счетчика, который принадлежит toohello `Service Fabric Service` категории:

`2740af29-78aa-44bc-a20b-7e60fb783264_635650083799324046_5008379932`

В предыдущих примере hello `2740af29-78aa-44bc-a20b-7e60fb783264` — hello строковое представление идентификатора секции Service Fabric hello, `635650083799324046` является строковым представлением реплики/InstanceId и `5008379932` — hello 64-разрядных идентификатор, который создается для внутренней hello среды выполнения используете.

#### <a name="service-fabric-service-method-category"></a>Категория Service Fabric Service Method
Для категории hello `Service Fabric Service Method`, имена экземпляров счетчиков hello находятся в hello следующий формат:

`MethodName_ServiceRuntimeMethodId_ServiceFabricPartitionID_ServiceReplicaOrInstanceId_ServiceRuntimeInternalID`

*Имя_метода* имя hello метод службы hello, hello экземпляр счетчика производительности, связан с. Формат Hello hello имя метода определяется на основе некоторых логики в среде выполнения Fabric Service hello, распределяет удобочитаемость hello именем hello и ограничения на максимальную длину hello имена экземпляров счетчиков производительности hello в Windows.

*ServiceRuntimeMethodId* — hello строковое представление 32-разрядное целое число, которое создается средой выполнения Fabric Service hello для внутреннего использования. Это включается в экземпляр счетчика производительности hello его уникальность имени tooensure и избежать конфликтов с другими имена экземпляров счетчиков производительности. Пользователи не пытайтесь выполнить toointerpret эту часть имени экземпляра счетчика производительности hello.

*ServiceFabricPartitionID* является строковым представлением hello hello сопоставлен идентификатор секции Service Fabric, hello экземпляр счетчика производительности. Идентификатор секции Hello является идентификатором GUID, и его строковое представление создается с помощью hello [ `Guid.ToString` ](https://msdn.microsoft.com/library/97af8hh4.aspx) метод с описатель формата «D».

*ServiceReplicaOrInstanceId* является строковым представлением hello код реплику или экземпляр структуры службы, hello экземпляр счетчика производительности, связанные с hello.

*ServiceRuntimeInternalID* — hello строковое представление 64-разрядного целого числа, создаваемый средой выполнения Fabric Service hello для внутреннего использования. Это включается в экземпляр счетчика производительности hello его уникальность имени tooensure и избежать конфликтов с другими имена экземпляров счетчиков производительности. Пользователи не пытайтесь выполнить toointerpret эту часть имени экземпляра счетчика производительности hello.

Hello ниже приведен пример имя экземпляра счетчика для счетчика, который принадлежит toohello `Service Fabric Service Method` категории:

`ivoicemailboxservice.leavemessageasync_2_89383d32-e57e-4a9b-a6ad-57c6792aa521_635650083804480486_5008380`

В предшествующих примере hello `ivoicemailboxservice.leavemessageasync` — имя метода hello, `2` — использовать 32-разрядных идентификатор, созданный для внутренней hello среды выполнения, hello `89383d32-e57e-4a9b-a6ad-57c6792aa521` — hello строковое представление идентификатора секции Service Fabric hello,`635650083804480486` является строка hello представление hello идентификатор реплику или экземпляр структуры службы и `5008380` — использовать идентификатор hello 64-разрядной, созданный для внутренней hello среды выполнения.

## <a name="list-of-performance-counters"></a>Список счетчиков производительности
### <a name="service-method-performance-counters"></a>Счетчики производительности метода службы

Надежные службы среды выполнения Hello публикует hello следующих выполнение связанных toohello счетчики производительности службы методов.

| Имя категории | Имя счетчика | Описание |
| --- | --- | --- |
| Service Fabric Service Method |Вызовов в секунду |Количество попыток вызова метода службы hello в секунду |
| Service Fabric Service Method |Среднее время вызова (мс) |Время метод службы tooexecute hello в миллисекундах |
| Service Fabric Service Method |Исключений в секунду |Количество попыток hello метода службы произошло исключение в секунду |

### <a name="service-request-processing-performance-counters"></a>Счетчики производительности обработки запросов службы
Когда клиент вызывает метод через прокси-объект службы, в результате сообщение-запрос, отправляемых через службу удаленного взаимодействия toohello сети hello. Служба Hello обрабатывает сообщение hello запрос и отправляет ответ назад toohello клиента. Среда выполнения надежного ServiceRemoting Hello публикует hello после обработки запроса tooservice связанных счетчиков производительности.

| Имя категории | Имя счетчика | Описание |
| --- | --- | --- |
| Service Fabric Service |Число невыполненных запросов |Количество запросов, выполняемых в службе hello |
| Service Fabric Service |Среднее время запроса (мс) |Время выполнения (в миллисекундах) tooprocess службы hello запрос |
| Service Fabric Service |Среднее время десериализации запроса (мс) |Сообщение запроса сделанной (в миллисекундах) toodeserialize службы времени при получении hello службы |
| Service Fabric Service |Среднее время сериализации ответа (мс) |Время сделанной (в миллисекундах) tooserialize hello ответное сообщение hello служба перед отправкой ответа hello toohello клиента |

## <a name="next-steps"></a>Дальнейшие действия
* [Пример кода](https://github.com/Azure/servicefabric-samples)
* [Поставщики EventSource в PerfView](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/)
