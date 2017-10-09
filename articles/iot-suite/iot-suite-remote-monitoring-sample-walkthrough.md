---
title: "Пошаговое руководство по решениям предварительно настроен мониторинг aaaRemote | Документы Microsoft"
description: "Описание удаленный мониторинг hello Azure IoT предварительно настроенное решение и его архитектуры."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 31fe13af-0482-47be-b4c8-e98e36625855
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 57a336bd94938c2b9ee5d3456ea8e45446cf3d33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="remote-monitoring-preconfigured-solution-walkthrough"></a>Пошаговое руководство по работе с настроенным решением для удаленного мониторинга

Здравствуйте, удаленное наблюдение за IoT Suite [предварительно настроенное решение] [ lnk-preconfigured-solutions] является реализация end-to-end решением для мониторинга нескольких машинах в удаленных расположениях. решение Hello объединяет tooprovide ключа служб Azure универсальную реализацию hello бизнес-сценария. Hello решения можно использовать в качестве отправной точки для свою собственную реализацию и [настроить] [ lnk-customize] его toomeet требованиями бизнеса.

В этой статье поможет выполнить некоторые ключевые элементы hello hello удаленного мониторинга решения tooenable toounderstand ее работы. Эти знания помогут вам:

* Устранение неполадок в решении hello.
* Планирование как toocustomize toohello решения toomeet конкретным требованиям. 
* спроектировать собственное решение IoT, использующее службы Azure.

## <a name="logical-architecture"></a>Логическая архитектура

Следующая схема Hello представлен краткий обзор hello логические компоненты hello предварительно настроенных решений.

![Логическая архитектура](media/iot-suite-remote-monitoring-sample-walkthrough/remote-monitoring-architecture.png)

## <a name="simulated-devices"></a>Виртуальные устройства

В решении предварительно настроенных hello hello имитированное устройство представляет устройство охлаждения (например, здания кондиционер или единица обработки воздуху территории). При развертывании решения hello предварительно настроен, также автоматически подготовить четыре имитацию устройствами под управлением в [веб-задания Azure][lnk-webjobs]. Hello имитируемые устройства облегчают вы tooexplore hello поведение hello решения без необходимости toodeploy hello все физические устройства. toodeploy физического устройства в разделе hello [подключения вашего устройства toohello удаленное наблюдение предварительно настроенных решений] [ lnk-connect-rm] учебника.

### <a name="device-to-cloud-messages"></a>Отправка сообщений с устройства в облако

Каждый имитированное устройство может отправлять hello следующие типы сообщений tooIoT концентратора:

| Сообщение | Описание |
| --- | --- |
| Запуск |При запуске hello устройство отправляет **сведения об устройстве** сообщение, содержащее сведения о себе toohello серверной части. Эти данные включают идентификатор устройства hello и список команд hello и методы hello поддерживает устройства. |
| Присутствие |Устройство периодически отправляет **наличие** сообщений tooreport ли hello устройства могут быть наличие hello датчика. |
| Телеметрия |Устройство периодически отправляет **телеметрии** сообщение, уведомляющее имитацию значения для hello температуры и влажности, собранных с устройств hello смоделированные датчиков. |

> [!NOTE]
> решение Hello хранит hello список команд, поддерживаемых устройств hello Cosmos DB базы данных, а не в двойных устройства hello.

### <a name="properties-and-device-twins"></a>Свойства и двойники устройств

Hello имитации устройства отправляют hello следующие устройства свойства toohello [двойных] [ lnk-device-twins] в центр IoT hello как *сообщил свойства*. Hello устройство отправляет отчет свойства во время запуска, а также в ответ tooa **изменение состояния устройства** команды или метода.

| Свойство | Назначение |
| --- | --- |
| Config.TelemetryInterval | Частота (в секундах) hello устройство отправляет данные телеметрии |
| Config.TemperatureMeanValue | Указывает среднее значение hello имитируемые температуры телеметрии hello |
| Device.DeviceID |Идентификатор, который будет предоставлен или назначенный при создании устройства в решении hello |
| Device.DeviceState | Состояние устройства hello |
| Device.CreatedTime |Время hello устройства был создан в решении hello |
| Device.StartupTime |Время hello устройство было запущено |
| Device.LastDesiredPropertyChange |изменить номер версии последнего нужное свойство hello Hello |
| Device.Location.Latitude |Широта местоположение устройства hello |
| Device.Location.Longitude |Долгота местоположение устройства hello |
| System.Manufacturer |Производитель устройства |
| System.ModelNumber |Номер модели устройства hello |
| System.SerialNumber |Серийный номер устройства hello |
| System.FirmwareVersion |Текущая версия встроенного по на устройстве hello |
| System.Platform |Архитектура платформы устройства hello |
| System.Processor |Процессор работающего устройства hello |
| System.InstalledRAM |Объем ОЗУ, установленного на устройстве hello |

Имитатор Hello начальные значения этих свойств в имитации устройствами с помощью образцов значений. Каждый раз, симулятор hello инициализирует имитации устройства, устройства hello tooIoT предварительно определенных метаданных hello концентратора отчеты в виде отчета свойства. Свойства отчета можно обновлять только hello устройства. toochange свойство отчета, необходимо задать нужное свойство в решение портала. Он несет hello hello устройства:

1. Периодически загрузить нужные свойства из центра IoT hello.
2. Обновите конфигурацию с значение hello требуемого свойства.
3. Отправьте hello новый концентратор задней toohello значение как свойство отчета.

На панели мониторинга решения hello, можно использовать *требуемого свойства* tooset свойства на устройстве с помощью hello [двойных устройства][lnk-device-twins]. Как правило устройство считывает значению свойства из tooupdate концентратора hello, его внутреннее состояние и hello отчета изменения обратно в качестве свойства отчета.

> [!NOTE]
> Hello имитированное устройство код использует только hello **Desired.Config.TemperatureMeanValue** и **Desired.Config.TelemetryInterval** hello tooupdate нужными свойствами сообщил отправил обратно свойства tooIoT концентратора. Имитированное устройство hello пропускаются все остальные запросы на изменение нужного свойства.

### <a name="methods"></a>Методы

Hello имитации устройства можно обрабатывать следующие методы hello ([прямой методы][lnk-direct-methods]) из портала решения hello через Центр IoT hello:

| Метод | Описание |
| --- | --- |
| InitiateFirmwareUpdate |Указывает, что устройство hello tooperform обновление встроенного по |
| Reboot |Указывает, что устройство tooreboot hello |
| FactoryReset |Указывает, что tooperform устройство hello сброса |

Некоторые методы используют tooreport свойства отчета о ходе выполнения. Например, hello **InitiateFirmwareUpdate** метод Моделирует выполнение обновления hello асинхронно на устройстве hello. метод Hello немедленно возвращает на устройстве hello прерывая toosend обратно обновления состояния асинхронной задачи hello toohello решений мониторинга с помощью команды сообщил свойства.

### <a name="commands"></a>Команды

Hello имитируемые устройства можно обрабатывать следующие команды (облака на устройство сообщений), отправляемые из портала решения hello через Центр IoT hello hello.

| Команда | Описание |
| --- | --- |
| PingDevice |Отправляет *ping* toocheck toohello устройство, он работоспособен |
| StartTelemetry |Запускает hello устройство, отправляющее телеметрии |
| StopTelemetry |Останавливает отправку телеметрии hello устройстве |
| ChangeSetPointTemp |Изменения hello пороговое значение значение, вокруг которой hello случайные данные |
| DiagnosticTelemetry |Триггеры hello toosend симулятор устройства значение дополнительных телеметрии (externalTemp) |
| ChangeDeviceState |Изменяет свойство расширенном состоянии для устройства hello и отправляет информационное сообщение hello устройства с устройства hello |

> [!NOTE]
> Сравнение этих команд (сообщений, отправляемых из облака на устройство) и методов (прямых методов) см. в статье [Руководство по обмену данными между облаком и устройством][lnk-c2d-guidance].

## <a name="iot-hub"></a>Центр IoT

Hello [центр IoT] [ lnk-iothub] принимает данные, отправленные с устройств hello в облаке hello и делает ее доступной toohello задания Azure Stream Analytics (ASA). Каждое задание ASA поток использует отдельный центр IoT потребителя группы tooread hello поток сообщений из устройства.

Здравствуйте центр IoT в решении hello также:

- Хранит в реестре удостоверений, сохраняет идентификаторы hello и ключей проверки подлинности всех устройств hello допускается tooconnect toohello портала. Можно включить и отключить устройствами с помощью реестра удостоверений hello.
- Отправляет команды tooyour устройства от имени hello решение портала.
- Вызывает методы на устройствах, от имени hello решение портала.
- Поддерживает двойники устройств для всех зарегистрированных устройств. Двойных устройство сохраняет значения свойств hello, сообщаемые устройства. Двойных устройства также хранит нужный набор hello решение портала для hello tooretrieve устройства при подключении рядом свойств.
- Расписания заданий tooset свойства для нескольких устройств или вызвать методы на нескольких устройствах.

## <a name="azure-stream-analytics"></a>Azure Stream Analytics

В удаленное наблюдение решения, hello [Azure Stream Analytics] [ lnk-asa] (ASA) отправляет устройства сообщений, полученных hello IoT hub tooother внутренней компонентов для обработки или хранения. Разные задания ASA выполнения конкретных функций на основе содержимого hello сообщений hello.

**Задания 1: Сведения об устройстве** фильтрует сообщения сведения устройства из входящего потока сообщений hello и отправляет их конечной точки tooan концентратора событий. Устройство отправляет устройства информационных сообщений во время запуска и в ответ tooa **SendDeviceInfo** команды. Это задание использует следующий запрос определения tooidentify hello **сведения об устройстве** сообщения:

```
SELECT * FROM DeviceDataStream Partition By PartitionId WHERE  ObjectType = 'DeviceInfo'
```

Эта задача отправляет его выходные данные tooan концентратор событий для дальнейшей обработки.

**Задание 2. Правила.** Оценивает входящие телеметрические значения температуры и влажности и сравнивает с пороговым значением для устройства. Пороговые значения задаются в редакторе правил hello доступна на портале hello решения. Каждая пара "устройство/значение" хранится с меткой времени в большом двоичном объекте, который обработчик Stream Analytics считывает как **ссылочные данные**. Задание Hello сравнивает значение любой непустой hello заданное пороговое значение для hello устройства. При превышении hello ">" условие выходных задания hello **сигнала** событие, указывающее hello пороговое значение превышено и предоставляет hello устройства, значения и значения отметок времени. Это задание использует следующий запрос определения tooidentify телеметрии сообщений, которые должны запускать оповещение hello:

```
WITH AlarmsData AS 
(
SELECT
     Stream.IoTHub.ConnectionDeviceId AS DeviceId,
     'Temperature' as ReadingType,
     Stream.Temperature as Reading,
     Ref.Temperature as Threshold,
     Ref.TemperatureRuleOutput as RuleOutput,
     Stream.EventEnqueuedUtcTime AS [Time]
FROM IoTTelemetryStream Stream
JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
WHERE
     Ref.Temperature IS NOT null AND Stream.Temperature > Ref.Temperature

UNION ALL

SELECT
     Stream.IoTHub.ConnectionDeviceId AS DeviceId,
     'Humidity' as ReadingType,
     Stream.Humidity as Reading,
     Ref.Humidity as Threshold,
     Ref.HumidityRuleOutput as RuleOutput,
     Stream.EventEnqueuedUtcTime AS [Time]
FROM IoTTelemetryStream Stream
JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
WHERE
     Ref.Humidity IS NOT null AND Stream.Humidity > Ref.Humidity
)

SELECT *
INTO DeviceRulesMonitoring
FROM AlarmsData

SELECT *
INTO DeviceRulesHub
FROM AlarmsData
```

Hello задания отправляет его выходные данные tooan концентратора событий для дальнейшей обработки и сохраняет сведения о каждой предупреждения tooblob хранилища из портала hello решения могут быть прочитаны hello сведений о предупреждениях.

**Задание 3: Телеметрии** обрабатывает входящий поток телеметрии устройства hello двумя способами. Hello сначала отправляет все сообщения телеметрии из хранилища больших двоичных объектов toopersistent hello устройств для долговременного хранения. Во-вторых, Hello вычисляет влажности среднее, минимальное и максимальное значения для скользящего окна каждые пять минут и отправляет этот tooblob хранения данных. портал решения Hello считывает данные телеметрии hello из диаграммы hello toopopulate хранилища больших двоичных объектов. Это задание использует hello после определения запроса:

```
WITH 
    [StreamData]
AS (
    SELECT
        *
    FROM [IoTHubStream]
    WHERE
        [ObjectType] IS NULL -- Filter out device info and command responses
) 

SELECT
    IoTHub.ConnectionDeviceId AS DeviceId,
    Temperature,
    Humidity,
    ExternalTemperature,
    EventProcessedUtcTime,
    PartitionId,
    EventEnqueuedUtcTime,
    * 
INTO
    [Telemetry]
FROM
    [StreamData]

SELECT
    IoTHub.ConnectionDeviceId AS DeviceId,
    AVG (Humidity) AS [AverageHumidity],
    MIN(Humidity) AS [MinimumHumidity],
    MAX(Humidity) AS [MaxHumidity],
    5.0 AS TimeframeMinutes 
INTO
    [TelemetrySummary]
FROM [StreamData]
WHERE
    [Humidity] IS NOT NULL
GROUP BY
    IoTHub.ConnectionDeviceId,
    SlidingWindow (mi, 5)
```

## <a name="event-hubs"></a>Концентраторы событий

Hello **сведения об устройстве** и **правила** задания ASA выводят их данных tooEvent концентраторов tooreliably вперед на toohello **обработчик событий** в hello веб-задания.

## <a name="azure-storage"></a>Хранилище Azure

Hello решение использует все данные телеметрии необработанные и сводных данных о hello из устройств hello toopersist хранилища BLOB-объектов Azure в решении hello. портал Hello считывает данные телеметрии hello из диаграммы hello toopopulate хранилища больших двоичных объектов. оповещения toodisplay hello решение портала считывает hello данные из хранилища больших двоичных объектов, записываемых при телеметрии превысил значения hello настроить пороговые значения. решение Hello также использует больших двоичных объектов хранилища toorecord hello пороговые значения, заданные в портал hello решения.

## <a name="webjobs"></a>Веб-задания

Кроме эмуляторах устройств toohosting hello, hello веб-заданий в решение hello также hello узла **обработчик событий** работает в веб-задания Azure, обрабатывающему команду ответов. Он использует команду ответа сообщения tooupdate hello устройства команда журнала (хранятся в базе данных Cosmos DB hello).

## <a name="cosmos-db"></a>База данных Cosmos

Hello решение использует сведения о toostore Cosmos DB базы данных о решении toohello подключенных устройств hello. Эти сведения включают hello журнала команды, отправляемые toodevices из портала решения hello и методы, вызываемые из портала hello решения.

## <a name="solution-portal"></a>Портал решения

портал Hello решение — веб-приложения, развернутые как часть hello предварительно настроенных решений. Hello ключа страницы портала решения hello: hello панели мониторинга и hello список устройств.

### <a name="dashboard"></a>Панель мониторинга

Эта страница в веб-приложения hello использует элементы управления javascript PowerBI (см. [репозитория визуальных элементов PowerBI](https://www.github.com/Microsoft/PowerBI-visuals)) данные телеметрии hello toovisualize с устройств hello. Hello решение использует hello ASA телеметрии задания toowrite hello телеметрии tooblob хранения данных.

### <a name="device-list"></a>Список устройств

На этой странице hello решение портала можно:

* Подготовка нового устройства. Это действие задает hello уникальный идентификатор устройства и приводит к возникновению ошибки hello ключ проверки подлинности. Записывает сведения о hello устройства tooboth hello реестра удостоверений центр IoT и базы данных Cosmos DB конкретного решения hello.
* Управление свойствами устройства. Это действие выполняет просмотр имеющихся свойств и их обновление.
* Отправка команд tooa устройства.
* Просмотр журнала hello команд для устройства.
* Включение и отключение устройств.

## <a name="next-steps"></a>Дальнейшие действия

Hello следующих записях блога TechNet содержат более подробные сведения о hello удаленное наблюдение предварительно настроенных решений:

* [Удаленный мониторинг IoT Suite - в разделе hello изнутри-](http://social.technet.microsoft.com/wiki/contents/articles/32941.iot-suite-under-the-hood-remote-monitoring.aspx)
* [IoT Suite - Remote Monitoring - Adding Live and Simulated Devices (IoT Suite. Удаленный мониторинг: добавление реальных и виртуальных устройств).](http://social.technet.microsoft.com/wiki/contents/articles/32975.iot-suite-remote-monitoring-adding-live-and-simulated-devices.aspx)

Вы можете продолжить, Приступая к работе с IoT Suite, считывая hello следующих статей.

* [Подключиться с вашего устройства toohello удаленное наблюдение предварительно настроенных решений][lnk-connect-rm]
* [Разрешения на сайт azureiotsuite.com hello][lnk-permissions]

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-iothub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-webjobs]: https://azure.microsoft.com/documentation/articles/websites-webjobs-resources/
[lnk-connect-rm]: iot-suite-connecting-devices.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-device-twins]:  ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
