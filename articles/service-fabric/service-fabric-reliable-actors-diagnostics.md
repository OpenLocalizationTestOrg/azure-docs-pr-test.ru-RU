---
title: "aaaActors диагностики и мониторинга | Документы Microsoft"
description: "В этой статье описываются задачи диагностики hello и функций в среде выполнения Service Fabric службы Reliable Actor hello, включая hello события и счетчики производительности, генерируемой его наблюдения за производительностью."
services: service-fabric
documentationcenter: .net
author: abhishekram
manager: timlt
editor: vturecek
ms.assetid: 1c229923-670a-4634-ad59-468ff781ad18
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: abhisram
ms.openlocfilehash: 5b266d67875722feef5c5be8861bda6d8132a7d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-and-performance-monitoring-for-reliable-actors"></a>Диагностика и мониторинг производительности в Reliable Actors
Среда выполнения службы Reliable Actor Hello выдает [EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) событий и [счетчики производительности](https://msdn.microsoft.com/library/system.diagnostics.performancecounter.aspx). Они предоставляют подробные сведения о том, как работает hello среды выполнения и помочь при устранении неполадок и наблюдение за производительностью.

## <a name="eventsource-events"></a>События EventSource
Имя поставщика Hello EventSource для среды выполнения службы Reliable Actor hello является «Microsoft ServiceFabric субъекты». Из этого источника событий отображаются в hello [событий диагностики](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md#view-service-fabric-system-events-in-visual-studio) окна приложения hello субъект, который [отладки в Visual Studio](service-fabric-debugging-your-application.md).

Ниже приведены несколько средств и технологий, которые помогают в сбор и Просмотр событий EventSource [PerfView](http://www.microsoft.com/download/details.aspx?id=28567), [диагностики Azure](../cloud-services/cloud-services-dotnet-diagnostics.md), [семантической ведения журнала](https://msdn.microsoft.com/library/dn774980.aspx)и hello [ Библиотека Microsoft TraceEvent](http://www.nuget.org/packages/Microsoft.Diagnostics.Tracing.TraceEvent).

### <a name="keywords"></a>Ключевые слова
Все события, которые принадлежат toohello надежного EventSource субъекты связаны с один или несколько ключевых слов. Это позволяет фильтровать собранные события. определены следующие биты ключевое слово Hello.

| Bit | Описание |
| --- | --- |
| 0x1 |Набор важные события, объединяющие hello операции среды выполнения субъекты структуры hello. |
| 0x2 |Набор событий, описывающих вызовы методов для субъекта. Дополнительные сведения см. в разделе hello [вводной на субъекты](service-fabric-reliable-actors-introduction.md). |
| 0x4 |Набор связанных tooactor состояние события. Дополнительные сведения см. в разделе hello на [управление состоянием субъекта](service-fabric-reliable-actors-state-management.md). |
| 0x8 |Набор событий связанные зависимости tooturn параллелизма hello субъекта. Дополнительные сведения см. в разделе hello на [параллелизма](service-fabric-reliable-actors-introduction.md#concurrency). |

## <a name="performance-counters"></a>Счетчики производительности
Среда выполнения службы Reliable Actor Hello определяет hello следующие категории счетчиков производительности.

| Категория | Описание |
| --- | --- |
| Субъект Service Fabric |Счетчики субъекты конкретных tooAzure Service Fabric, например время, затраченное toosave состояния субъекта |
| Метод субъекта Service Fabric |Счетчики конкретных toomethods, реализуемый субъекты Service Fabric, например частоту вызывается метод субъекта |

Каждый из hello выше категорий содержит один или несколько счетчиков.

Hello [монитора производительности](https://technet.microsoft.com/library/cc749249.aspx) приложение, доступное в ОС Windows hello по умолчанию может быть используется toocollect и представление данных счетчиков производительности. [Диагностика Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) — еще один параметр для сбора данных счетчиков производительности и передачи их tooAzure таблиц.

### <a name="performance-counter-instance-names"></a>Имена экземпляров счетчиков производительности
В кластере, содержащем большое количество служб или секций служб субъектов, находится большое количество экземпляров счетчиков производительности субъектов. Hello имена экземпляров счетчиков производительности могут помочь в определении конкретных hello [секции](service-fabric-reliable-actors-platform.md#service-fabric-partition-concepts-for-actors) , метод субъекта (если применимо), экземпляр счетчика производительности hello связана с.

#### <a name="service-fabric-actor-category"></a>Категория субъекта Service Fabric
Для категории hello `Service Fabric Actor`, имена экземпляров счетчиков hello находятся в hello следующий формат:

`ServiceFabricPartitionID_ActorsRuntimeInternalID`

*ServiceFabricPartitionID* является строковым представлением hello hello сопоставлен идентификатор секции Service Fabric, hello экземпляр счетчика производительности. Идентификатор секции Hello является идентификатором GUID, и его строковое представление создается с помощью hello [ `Guid.ToString` ](https://msdn.microsoft.com/library/97af8hh4.aspx) метод с описатель формата «D».

*ActorRuntimeInternalID* — hello строковое представление 64-разрядного целого числа, создаваемый средой выполнения hello субъекты структуры для внутреннего использования. Это включается в экземпляр счетчика производительности hello его уникальность имени tooensure и избежать конфликтов с другими имена экземпляров счетчиков производительности. Пользователи не пытайтесь выполнить toointerpret эту часть имени экземпляра счетчика производительности hello.

Hello ниже приведен пример имя экземпляра счетчика для счетчика, который принадлежит toohello `Service Fabric Actor` категории:

`2740af29-78aa-44bc-a20b-7e60fb783264_635650083799324046`

В приведенном выше примере hello `2740af29-78aa-44bc-a20b-7e60fb783264` — hello строковое представление идентификатора секции Service Fabric hello, и `635650083799324046` — использовать hello 64-разрядных идентификатор, который создается для внутренней hello среды выполнения.

#### <a name="service-fabric-actor-method-category"></a>Категория метода субъекта Service Fabric
Для категории hello `Service Fabric Actor Method`, имена экземпляров счетчиков hello находятся в hello следующий формат:

`MethodName_ActorsRuntimeMethodId_ServiceFabricPartitionID_ActorsRuntimeInternalID`

*Имя_метода* hello имя метода hello субъект, который hello экземпляр счетчика производительности, связан с. Формат Hello hello имя метода определяется на основе некоторых логики в структуры субъекты hello среду выполнения, которая распределяет удобочитаемость hello именем hello и ограничения на максимальную длину hello имена экземпляров счетчиков производительности hello в Windows.

*ActorsRuntimeMethodId* — hello строковое представление 32-разрядное целое число, которое создается средой выполнения hello субъекты структуры для внутреннего использования. Это включается в экземпляр счетчика производительности hello его уникальность имени tooensure и избежать конфликтов с другими имена экземпляров счетчиков производительности. Пользователи не пытайтесь выполнить toointerpret эту часть имени экземпляра счетчика производительности hello.

*ServiceFabricPartitionID* является строковым представлением hello hello сопоставлен идентификатор секции Service Fabric, hello экземпляр счетчика производительности. Идентификатор секции Hello является идентификатором GUID, и его строковое представление создается с помощью hello [ `Guid.ToString` ](https://msdn.microsoft.com/library/97af8hh4.aspx) метод с описатель формата «D».

*ActorRuntimeInternalID* — hello строковое представление 64-разрядного целого числа, создаваемый средой выполнения hello субъекты структуры для внутреннего использования. Это включается в экземпляр счетчика производительности hello его уникальность имени tooensure и избежать конфликтов с другими имена экземпляров счетчиков производительности. Пользователи не пытайтесь выполнить toointerpret эту часть имени экземпляра счетчика производительности hello.

Hello ниже приведен пример имя экземпляра счетчика для счетчика, который принадлежит toohello `Service Fabric Actor Method` категории:

`ivoicemailboxactor.leavemessageasync_2_89383d32-e57e-4a9b-a6ad-57c6792aa521_635650083804480486`

В приведенном выше примере hello `ivoicemailboxactor.leavemessageasync` — имя метода hello, `2` — hello использовать 32-разрядных идентификатор, созданный для внутренней hello среды выполнения, `89383d32-e57e-4a9b-a6ad-57c6792aa521` — hello строковое представление идентификатора секции Service Fabric hello, и `635650083804480486` — 64-разрядных идентификатор hello для внутреннего использования среды выполнения hello создан.

## <a name="list-of-events-and-performance-counters"></a>Список событий и счетчиков производительности
### <a name="actor-method-events-and-performance-counters"></a>События и счетчики производительности методов субъектов
Hello службы Reliable Actor среда выполнения выдает следующие события, связанные с слишком hello[методы субъекта](service-fabric-reliable-actors-introduction.md).

| Имя события | Идентификатор события | Уровень | Ключевое слово | Описание |
| --- | --- | --- | --- | --- |
| ActorMethodStart |7 |Подробная информация |0x2 |Среда выполнения субъекты посвящен tooinvoke метод субъекта. |
| ActorMethodStop |8 |Подробная информация |0x2 |Выполнение метода субъекта завершено. То есть вернул метод субъекта toohello hello выполнения асинхронного вызова и завершения задачи hello, возвращенный методом субъекта hello. |
| ActorMethodThrewException |9 |Предупреждение |0x3 |Возникло исключение во время выполнения hello методов субъекта, либо во время выполнения toohello субъекта hello выполнения асинхронного вызова метода или при выполнении hello задачу hello, возвращенный методом субъекта hello. Это событие указывает, какая-либо ошибки в коде hello субъект, который требуется исследование. |

Среда выполнения службы Reliable Actor Hello публикует hello следующих выполнение связанных toohello счетчики производительности методов субъекта.

| Имя категории | Имя счетчика | Описание |
| --- | --- | --- |
| Метод субъекта Service Fabric |Вызовов в секунду |Количество попыток вызова метода службы субъекта hello в секунду |
| Метод субъекта Service Fabric |Среднее время вызова (мс) |Метода службы субъекта hello tooexecute время в миллисекундах |
| Метод субъекта Service Fabric |Исключений в секунду |Количество попыток hello метода службы субъекта вызвал исключение в секунду |

### <a name="concurrency-events-and-performance-counters"></a>События и счетчики производительности для параллелизма
Hello службы Reliable Actor среда выполнения выдает следующие события, связанные с слишком hello[параллелизма](service-fabric-reliable-actors-introduction.md#concurrency).

| Имя события | Идентификатор события | Уровень | Ключевое слово | Описание |
| --- | --- | --- | --- | --- |
| ActorMethodCallsWaitingForLock |12 |Подробная информация |0x8 |Это событие записывается в начале каждого нового Включение в субъект hello. В нем hello, число отложенных вызовов субъекта, ожидающих блокировки субъекта hello tooacquire, обеспечивающий основанных параллелизма. |

Среда выполнения службы Reliable Actor Hello публикует hello, следуя tooconcurrency связанных счетчиков производительности.

| Имя категории | Имя счетчика | Описание |
| --- | --- | --- |
| Субъект Service Fabric |Количество вызовов, ожидающих блокировку субъекта |Количество ожидающих вызовов субъекта, ожидающих блокировки субъекта hello tooacquire, обеспечивающий основанных параллелизма |
| Субъект Service Fabric |Среднее время блокировки (мс) |Блокировки субъекта hello время tooacquire сделанной (в миллисекундах), обеспечивающий основанных параллелизма |
| Субъект Service Fabric |Среднее время (в миллисекундах) удержания блокировки субъекта |Время (в миллисекундах), для которых hello действует блокировка субъекта |

### <a name="actor-state-management-events-and-performance-counters"></a>События и счетчики производительности управления состоянием субъектов
Hello службы Reliable Actor среда выполнения выдает следующие события, связанные с слишком hello[управление состоянием субъекта](service-fabric-reliable-actors-state-management.md).

| Имя события | Идентификатор события | Уровень | Ключевое слово | Описание |
| --- | --- | --- | --- | --- |
| ActorSaveStateStart |10 |Подробная информация |0x4 |Среда выполнения субъекты посвящен состояния субъекта toosave hello. |
| ActorSaveStateStop |11 |Подробная информация |0x4 |Среда выполнения субъекты завершил сохранение состояния субъекта hello. |

Среда выполнения службы Reliable Actor Hello публикует hello, следуя управление состоянием tooactor связанных счетчиков производительности.

| Имя категории | Имя счетчика | Описание |
| --- | --- | --- |
| Субъект Service Fabric |Среднее время операции сохранения состояния (мс) |Время, затраченное toosave состояния субъекта в миллисекундах |
| Субъект Service Fabric |Среднее время операции загрузки состояния (мс) |Время, затраченное tooload состояния субъекта в миллисекундах |

### <a name="events-related-tooactor-replicas"></a>Реплики tooactor связанные события
Hello службы Reliable Actor среда выполнения выдает следующие события, связанные с слишком hello[реплик субъекта](service-fabric-reliable-actors-platform.md#service-fabric-partition-concepts-for-actors).

| Имя события | Идентификатор события | Уровень | Ключевое слово | Описание |
| --- | --- | --- | --- | --- |
| ReplicaChangeRoleToPrimary |1 |Информация |0x1 |Реплика субъект меняет tooPrimary роли. Это означает, что hello субъекты для этой секции будет создан внутри этой реплики. |
| ReplicaChangeRoleFromPrimary |2 |Информация |0x1 |Реплика субъект меняет toonon первичной роли. Это означает, что внутри этой реплики больше нельзя создавать субъекты hello для этой секции. Новые запросы не будут доставлены tooactors, уже созданных в этой реплике. Субъекты Hello уничтожается после завершения всех выполняющихся запросов. |

### <a name="actor-activation-and-deactivation-events-and-performance-counters"></a>События активации и деактивации субъектов и счетчики производительности
Hello службы Reliable Actor среда выполнения выдает следующие события, связанные с слишком hello[субъекта активация и деактивация](service-fabric-reliable-actors-lifecycle.md).

| Имя события | Идентификатор события | Уровень | Ключевое слово | Описание |
| --- | --- | --- | --- | --- |
| ActorActivated |5 |Информация |0x1 |Субъект активирован. |
| ActorDeactivated |6 |Информация |0x1 |Субъект отключен. |

Среда выполнения службы Reliable Actor Hello публикует hello следующие счетчики производительности связанные tooactor активации и деактивации.

| Имя категории | Имя счетчика | Описание |
| --- | --- | --- |
| Субъект Service Fabric |Среднее значение OnActivateAsync в миллисекундах |Время tooexecute метода OnActivateAsync в миллисекундах |

### <a name="actor-request-processing-performance-counters"></a>Счетчики производительности обработки запросов субъекта
Когда клиент вызывает метод через прокси-объект субъекта, в результате сообщение-запрос, отправляемых через сетевой toohello hello субъекта-службы. Служба Hello обрабатывает сообщение hello запрос и отправляет ответ назад toohello клиента. Среда выполнения службы Reliable Actor Hello публикует hello после обработки запроса tooactor связанных счетчиков производительности.

| Имя категории | Имя счетчика | Описание |
| --- | --- | --- |
| Субъект Service Fabric |Число невыполненных запросов |Количество запросов, выполняемых в службе hello |
| Субъект Service Fabric |Среднее время запроса (мс) |Время выполнения (в миллисекундах) tooprocess службы hello запрос |
| Субъект Service Fabric |Среднее время десериализации запроса (мс) |Сообщение запроса сделанной (в миллисекундах) toodeserialize субъекта времени при получении hello службы |
| Субъект Service Fabric |Среднее время сериализации ответа (мс) |Время сделанной (в миллисекундах) tooserialize hello субъекта ответное сообщение hello служба перед отправкой ответа hello toohello клиента |

## <a name="next-steps"></a>Дальнейшие действия
* [Использование службы Reliable Actor hello платформы Service Fabric](service-fabric-reliable-actors-platform.md)
* [Справочная документация по API субъектов](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [Пример кода](https://github.com/Azure/servicefabric-samples)
* [Поставщики EventSource в PerfView](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/)
