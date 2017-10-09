---
title: "aaaAzure Media Services телеметрии | Документы Microsoft"
description: "В этой статье приводится обзор телеметрии служб мультимедиа Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 95c20ec4-c782-4063-8042-b79f95741d28
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 659e1c947a77aad0e4acacb541d95714da4775ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-telemetry"></a>Телеметрия служб мультимедиа Azure

Службы мультимедиа Azure (AMS) позволяет tooaccess данные телеметрии и показатели для служб. Текущая версия Hello AMS позволяет собирать данные телеметрии для динамическую **канала**, **конечной точки потоковой передачи**и динамической **архив** сущностей. 

Данные телеметрии записывается tooa хранения таблицы в указанной вами учетной записи хранилища Azure (как правило, используется учетная запись хранения hello, связанные с учетной записью AMS). 

Hello телеметрии системы не поддерживает управление хранением данных. Можно удалить старые данные телеметрии hello, удалив hello хранилища таблиц.

В этом разделе рассматриваются как tooconfigure и использовать hello AMS телеметрии.

## <a name="configuring-telemetry"></a>Настройка телеметрии

Телеметрию можно настроить на уровне компонента. Существует два уровня детализации: "Обычный" и "Подробный". В настоящее время обоих уровней возвращают hello одинаковые сведения. Рекомендуется toouse «Normal. 

Здравствуйте, следующие разделы Показать как телеметрии tooenable:

[Включение телеметрии с помощью .NET](media-services-dotnet-telemetry.md) 

[Включение телеметрии с помощью REST](media-services-rest-telemetry.md)

## <a name="consuming-telemetry-information"></a>Использование данных телеметрии

Данные телеметрии записывается tooan таблицу хранилища Azure в учетной записи хранения hello, указанный вами при настройке данные телеметрии для hello учетная запись служб мультимедиа. В этом разделе описываются hello хранилище таблиц для метрик hello.

Его можно использовать данные телеметрии в одном из следующих способов hello:

- Чтение данных непосредственно из табличного хранилища Azure (например, при использовании hello SDK хранилища). Описание hello телеметрии хранилища таблиц см. hello **потребляет данные телеметрии** в [это](https://msdn.microsoft.com/library/mt742089.aspx) раздела.

Или

- Использовать поддержку hello в hello Media Services .NET SDK для чтения данных из хранилища, как описано в [это](media-services-dotnet-telemetry.md) раздела. 


Схема телеметрии Hello, описанных ниже — спроектированный toogive высокую производительность в пределах hello хранилища таблиц Azure:

- Данные секционируются по учетной записи, идентификатор и идентификатор службы tooallow телеметрии из каждой службы toobe, запросы независимо друг от друга.
- Разделы содержат toogive даты hello разумного верхняя граница hello размер раздела.
- Ключей строк в обратного времени заказа tooallow hello самые последние данные телеметрии элементы toobe запрашиваются для данной службы.

Это следует выполнять многие из распространенных запросов toobe hello эффективно:

- Параллельное, независимое скачивание данных для разных служб.
- Получение всех данных для заданной службы в диапазоне дат.
- Получение hello самые последние данные для службы.

### <a name="telemetry-table-storage-output-schema"></a>Схема вывода данных телеметрии хранилища таблиц

Данные телеметрии хранится в статистической функции в одной таблице, «TelemetryMetrics20160321», где «20160321» — Дата создания hello таблицы. Система телеметрии создает отдельную таблицу для данных по каждому новому дню в 00:00 (UTC). Таблица Hello используется toostore повторяющихся значений, таких как приема скоростью в пределах заданного периода времени, Отправлено байт, и т. д. 

Свойство|Значение|Примеры и примечания
---|---|---
PartitionKey|{ИД_учетной_записи}_{ИД_сущности}|e49bef329c29495f9b9570989682069d_64435281c50a4dd8ab7011cb0f4cdf66<br/<br/>Здравствуйте, идентификатор включается в рабочих процессах toosimplify ключа секции hello где несколько учетных записей служб мультимедиа записи toohello учетной записи учетную запись хранения.
RowKey|{секунд toomidnight} _ {случайное значение}|01688_00199<br/><br/>ключ строки Hello начинается с hello количество секунд toomidnight tooallow top n запросы внутри секции. Дополнительные сведения см. в [этой статье](../cosmos-db/table-storage-design-guide.md#log-tail-pattern). 
Timestamp|Дата и время|Auto отметки времени из таблицы Azure 2016 hello-09-09T22:43:42.241Z
Тип|Тип Hello hello объектом, предоставляющим данные телеметрии|Channel, StreamingEndpoint, Archive.<br/><br/>Тип события — это просто строковое значение.
Имя|Имя события телеметрии hello Hello|ChannelHeartbeat, StreamingEndpointRequestLog.
ObservedTime|Hello время hello телеметрии произошло событие (UTC)|2016-09-09T22:42:36.924Z<br/><br/>Hello наблюдаемых время обеспечивается телеметрии отправку hello hello сущности (например, канал). Возможны проблемы синхронизации между компонентами, поэтому данное значение является приблизительным.
ServiceID|{ИД_службы}|f70bd731-691d-41c6-8f2d-671d0bdc9c7e
Свойства, относящиеся к сущности|В соответствии с определением события hello|StreamName: stream1, Bitrate 10123…<br/><br/>остальные свойства Hello определены для данного типа событий hello. Таблица Azure содержит пары "ключ-значение".  (то есть, различными строками в таблице hello имеют разные наборы свойств).

### <a name="entity-specific-schema"></a>Схемы сущности

Существует три типа записей telemetric данных конкретной сущности, которое каждый отправлена с hello следующие частоты:

- конечные точки потоковой передачи: каждые 30 секунд;
- динамические каналы: каждую минуту;
- динамический архив: каждую минуту.

**Конечная точка потоковой передачи**

Свойство|Значение|Примеры
---|---|---
PartitionKey|PartitionKey|e49bef329c29495f9b9570989682069d_64435281c50a4dd8ab7011cb0f4cdf66
RowKey|RowKey|01688_00199
Timestamp|Timestamp|Создаваемая автоматически метка времени из таблицы Azure: 2016-Auto-09-09T22:43:42.241Z.
Тип|Тип|StreamingEndpoint
Имя|Имя|StreamingEndpointRequestLog
ObservedTime|ObservedTime|2016-09-09T22:42:36.924Z
ServiceID|Идентификатор службы.|f70bd731-691d-41c6-8f2d-671d0bdc9c7e
HostName|Имя узла конечной точки hello|builddemoserver.origin.mediaservices.windows.net
StatusCode|Состояние HTTP.|200
ResultCode|Сведения о коде результата.|S_OK
RequestCount|Общий запрос в агрегате hello|3
Передано байт|Совокупное число отправленных байтов.|2987358
ServerLatency|Средняя задержка сервера (включая хранилище).|129
E2ELatency|Средняя совокупная задержка.|250

**Динамический канал**

Свойство|Значение|Примеры и примечания
---|---|---
PartitionKey|PartitionKey|e49bef329c29495f9b9570989682069d_64435281c50a4dd8ab7011cb0f4cdf66
RowKey|RowKey|01688_00199
Timestamp|Timestamp|Auto отметки времени из таблицы Azure 2016 hello-09-09T22:43:42.241Z
Тип|Тип|Канал
Имя|Имя|ChannelHeartbeat
ObservedTime|ObservedTime|2016-09-09T22:42:36.924Z
ServiceID|Идентификатор службы.|f70bd731-691d-41c6-8f2d-671d0bdc9c7e
TrackType|Тип дорожки: видео, звук или текст.|video/audio
TrackName|Имя отслеживания hello|video/audio_1
Bitrate|Скорость дорожки.|785000
CustomAttributes||   
IncomingBitrate|Фактическая входящая скорость.|784548
OverlapCount|Перекрытие hello приема|0
DiscontinuityCount|Прерывание дорожки.|0
LastTimestamp|Метка времени последнего получения данных.|1800488800
NonincreasingCount|Количество фрагментов отброшены из-за увеличения toonon отметки времени|2
UnalignedKeyFrames|Получены ли фрагменты (для уровней качества), в которых ключевые кадры не выровнены. |Да
UnalignedPresentationTime|Получены ли фрагменты (для уровней качества или дорожек), в которых время презентации не согласовано.|Да
UnexpectedBitrate|Значение True, если расчетная или фактическая скорость для аудио- или видеодорожки превышает 40 000 бит/с и значение IncomingBitrate равно 0 ЛИБО значения IncomingBitrate и actualBitrate отличаются на 50 %. |Да
Healthy|Значение True, если значения <br/>overlapCount, <br/>DiscontinuityCount, <br/>NonIncreasingCount, <br/>UnalignedKeyFrames, <br/>UnalignedPresentationTime и <br/>UnexpectedBitrate<br/> равны 0.|Да<br/><br/>Составной функции, которая возвращает false, если любой из следующих условий удержания hello работоспособно:<br/><br/>- OverlapCount > 0<br/>- DiscontinuityCount > 0<br/>- NonincreasingCount > 0<br/>- UnalignedKeyFrames = True<br/>- UnalignedPresentationTime = True<br/>- UnexpectedBitrate = True

**Динамический архив**

Свойство|Значение|Примеры и примечания
---|---|---
PartitionKey|PartitionKey|e49bef329c29495f9b9570989682069d_64435281c50a4dd8ab7011cb0f4cdf66
RowKey|RowKey|01688_00199
Timestamp|Timestamp|Auto отметки времени из таблицы Azure 2016 hello-09-09T22:43:42.241Z
Тип|Тип|Архив
Имя|Имя|ArchiveHeartbeat
ObservedTime|ObservedTime|2016-09-09T22:42:36.924Z
ServiceID|Идентификатор службы.|f70bd731-691d-41c6-8f2d-671d0bdc9c7e
ManifestName|URL-адрес программы.|asset-eb149703-ed0a-483c-91c4-e4066e72cce3/a0a5cfbf-71ec-4bd2-8c01-a92a2b38c9ba.ism
TrackName|Имя отслеживания hello|audio_1
TrackType|Тип дорожки hello|Audio/video
CustomAttribute|Шестнадцатеричная строка, позволяющая различать разные дорожки с одинаковым именем и скоростью (при многокамерной съемке).|
Bitrate|Скорость дорожки.|785000
Healthy|Значение True, если FragmentDiscardedCount = 0 и ArchiveAcquisitionError = False.|True (эти два значения не существуют в hello метрики, но они присутствуют в hello исходного события)<br/><br/>Составной функции, которая возвращает false, если любой из следующих условий удержания hello работоспособно:<br/><br/>- FragmentDiscardedCount > 0<br/>- ArchiveAcquisitionError = True

## <a name="general-qa"></a>Общие вопросы и ответы

### <a name="how-tooconsume-metrics-data"></a>Каким образом данные метрик tooconsume?

Данные метрик сохраняется как ряд таблиц Azure в hello пользовательской учетной записи хранения. Эти данные могут быть использованы с помощью hello следующие средства:

- пакет SDK для AMS;
- Microsoft Azure Storage Explorer (поддерживает формат экспорта toocomma запятыми и обработанные в Excel)
- Интерфейс REST API

### <a name="how-toofind-average-bandwidth-consumption"></a>Как toofind среднее потребление пропускной способности?

Средняя пропускная способность потребления Hello — среднее hello BytesSent за период времени.

### <a name="how-toodefine-streaming-unit-count"></a>Как количество модулей потоковой передачи toodefine?

Привет, число единиц потоковой передачи может определяться как пропускной пиковое hello из конечных точек потоковой передачи служб hello, разделенное на пропускную способность hello пиковых нагрузок, одной конечной точки потоковой передачи. Hello (пик) использования пропускной способности одной конечной точки потоковой передачи составляет 160 Мбит/с.
Например предположим, что пропускная способность пиковых нагрузок hello из клиента службы — 40 Мбит/с (hello максимальное значение BytesSent за период времени). Число единиц потоковой передачи hello будет, равно too(40 MBps) * (8 бит-байтные) /(160 Mbps) = 2 единицы потоковой передачи.

### <a name="how-toofind-average-requestssecond"></a>Как среднее toofind запросов в секунду?

toofind hello среднее число запросов в секунду, за период времени, вычислений hello среднее количество запросов (RequestCount).

### <a name="how-toodefine-channel-health"></a>Как toodefine канала работоспособности?

Таким образом, что он имеет значение false, при проведении любой из следующих условий hello работоспособности канала можно определить как составной логической функции:

- OverlapCount > 0
- DiscontinuityCount > 0
- NonincreasingCount > 0
- UnalignedKeyFrames = True 
- UnalignedPresentationTime = True 
- UnexpectedBitrate = True


### <a name="how-toodetect-discontinuities"></a>Как нарушения непрерывности toodetect?

нарушения непрерывности toodetect, найти все записи данных канала где DiscontinuityCount > 0. Hello соответствующий ObservedTime, метка времени указывает время hello, в которых произошло нарушение непрерывности hello.

### <a name="how-toodetect-timestamp-overlaps"></a>Как перекрывается toodetect отметка времени?

перекрытия toodetect отметки времени, найти все записи данных канала где OverlapCount > 0. соответствующий ObservedTime timestamp Hello указывает hello произошла раз, в какие hello перекрывается отметки времени.

### <a name="how-toofind-streaming-request-failures-and-reasons"></a>Способ toofind потоковой передачи запроса сбоев и причины?

toofind потоковой передачи ошибок запросов и причины, найти все операции конечной точки потоковой передачи данных, когда код результата не равен tooS_OK. соответствующее поле StatusCode Hello указывает hello причину сбоя запроса hello.

### <a name="how-tooconsume-data-with-external-tools"></a>Как tooconsume данных с помощью внешних средств?

Telemetric данных можно обработать и визуализируется с hello следующие средства:

- PowerBI
- Application Insights
- Azure Monitor (прежнее название — Shoebox);
- динамическая панель мониторинга AMS;
- портал Azure (ожидается выпуск).

### <a name="how-toomanage-data-retention"></a>Способ хранения данных toomanage?

Hello телеметрии система осуществляет управление хранением данных или автоматического удаления старых записей. Таким образом требуется toomanage и вручную удалить старые записи из таблицы хранилища hello. Toostorage SDK можно ссылаться как toodo его.

## <a name="next-steps"></a>Дальнейшие действия

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
