---
title: "Центр IoT Azure задания aaaUnderstand | Документы Microsoft"
description: "Руководство разработчика - планирования заданий toorun на нескольких устройствах подключен tooyour центр IoT. Задания могут обновлять теги и требуемые свойства, а также вызывать прямые методы на нескольких устройствах."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: fe78458f-4f14-4358-ac83-4f7bd14ee8da
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/30/2016
ms.author: juanpere
ms.openlocfilehash: 8be134e6c379feae5087df8f562a74505c57afee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-jobs-on-multiple-devices"></a>Планирование заданий на нескольких устройствах
## <a name="overview"></a>Обзор
Как описано в предыдущих статьях, Центр Интернета вещей Azure включает ряд стандартных блоков ([свойства и теги двойников устройств][lnk-twin-devguide] и [прямые методы][lnk-dev-methods]).  Как правило серверной части приложения включите устройство tooupdate Администраторы и операторы и взаимодействовать с устройствами IoT в пакетном режиме и в запланированное время.  Задания инкапсулируют hello выполнение обновления двойных устройства и непосредственные методы для набора устройств во время расписания.  Например оператор будет использовать приложение серверной части, которое будет запустите и отслеживайте задания tooreboot на наборе устройств при построении 43 и этаж 3 на время, которое бы не нарушают работу toohello операции построения hello.

### <a name="when-toouse"></a>Когда toouse
Рассмотрите возможность с помощью заданий при: tooschedule потребностей серверной части решения и отслеживать ход выполнения любой из следующих действий на наборе устройств hello:

* Обновление требуемых свойств
* Обновление тегов
* Вызов прямых методов

## <a name="job-lifecycle"></a>Жизненный цикл задания
Заданий инициированных серверной части решения hello и обслуживается центр IoT.  Вы можете инициировать задание, используя обращенный к службе универсальный код ресурса (URI) `{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14` и запросить данные о выполнении задания, используя аналогичный URI `{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`.  После запуска задания, запрос для задания позволяет hello серверной части приложения toorefresh hello статуса выполняемых заданий.

> [!NOTE]
> При отправке задания имен и значений свойств может содержать только печатаемые US-ASCII буквенно-цифровых, за исключением в следующий набор hello: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.
> 
> 

## <a name="reference-topics"></a>Справочные материалы
Hello следующие справочные разделы предоставляют дополнительные сведения об использовании заданий.

## <a name="jobs-tooexecute-direct-methods"></a>Методы прямой tooexecute заданий
Hello ниже приводится сведения о запросе hello HTTP 1.1 для выполнения [прямой метод] [ lnk-dev-methods] на наборе устройств с помощью задания:

    ```
    PUT /jobs/v2/<jobId>?api-version=2016-11-14

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>

    {
        jobId: '<jobId>',
        type: 'scheduleDirectRequest', 
        cloudToDeviceMethod: {
            methodName: '<methodName>',
            payload: <payload>,                 
            responseTimeoutInSeconds: methodTimeoutInSeconds 
        },
        queryCondition: '<queryOrDevices>', // query condition
        startTime: <jobStartTime>,          // as an ISO-8601 date string
        maxExecutionTimeInSeconds: <maxExecutionTimeInSeconds>        
    }
    ```
условия запроса Hello также может быть на одном устройстве идентификатор списка идентификаторов устройств как показано ниже

**Примеры**
```
queryCondition = "deviceId = 'MyDevice1'"
queryCondition = "deviceId IN ['MyDevice1','MyDevice2']"
queryCondition = "deviceId IN ['MyDevice1']
```
В статье [Справочник по языку запросов Центр Интернета вещей для двойников устройств и заданий][lnk-query] подробно рассматривается язык запросов Центра Интернета вещей.

## <a name="jobs-tooupdate-device-twin-properties"></a>Свойства двойных устройства tooupdate заданий
Hello Вот hello HTTP 1.1 сведения о запросе для обновления с помощью задания свойств двойных устройства:

    ```
    PUT /jobs/v2/<jobId>?api-version=2016-11-14
    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>

    {
        jobId: '<jobId>',
        type: 'scheduleTwinUpdate', 
        updateTwin: <patch>                 // Valid JSON object
        queryCondition: '<queryOrDevices>', // query condition
        startTime: <jobStartTime>,          // as an ISO-8601 date string
        maxExecutionTimeInSeconds: <maxExecutionTimeInSeconds>        // format TBD
    }
    ```

## <a name="querying-for-progress-on-jobs"></a>Запрос на отслеживание выполнения заданий
Hello Вот hello сведений о запросе HTTP 1.1 для [запрос для задания][lnk-query]:

    ```
    GET /jobs/v2/query?api-version=2016-11-14[&jobType=<jobType>][&jobStatus=<jobStatus>][&pageSize=<pageSize>][&continuationToken=<continuationToken>]

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>
    ```

Hello continuationToken предоставляется из ответа hello.  

## <a name="jobs-properties"></a>Свойства заданий
Hello ниже приведен список свойств и соответствующие описания, которые могут быть использованы при выполнении запроса для заданий или результаты задания.

| Свойство | Description (Описание) |
| --- | --- |
| **jobId** |Идентификатор для задания hello, предоставляемые приложением. |
| **startTime** |Время начала (ISO 8601) задания hello, предоставляемые приложением. |
| **endTime** |Центр IoT обеспечивает даты (ISO 8601) после завершения задания hello. Допустимо, только после задания hello достигает состояния hello «завершено». |
| **type** |Типы заданий: |
| **scheduledUpdateTwin**: tooupdate задания используемого набора требуемые свойства или теги. | |
| **scheduledDeviceMethod**: tooinvoke задания используется метод на наборе устройств близнецы устройства. | |
| **состояние** |Текущее состояние задания hello. Возможные значения состояния: |
| **Ожидание** : запланированное и ожидания toobe заберет службы заданий hello. | |
| **запланированные** : запланирована на время в будущем hello. | |
| **running** — задание сейчас активно. | |
| **cancelled** — задание отменено. | |
| **failed** — произошел сбой задания. | |
| **completed** — задание завершено. | |
| **deviceJobStatistics** |Статистика выполнения задания hello. |

Свойства **deviceJobStatistics**.

| Свойство | Description (Описание) |
| --- | --- |
| **deviceJobStatistics.deviceCount** |Количество устройств в задании hello. |
| **deviceJobStatistics.failedCount** |Количество устройств, где hello не удалась. |
| **deviceJobStatistics.succeededCount** |Количество устройств, где hello задание успешно выполнено. |
| **deviceJobStatistics.runningCount** |Количество устройств, которые в данный момент выполняются задания hello. |
| **deviceJobStatistics.pendingCount** |Количество устройств, ожидающих toorun hello задания. |

### <a name="additional-reference-material"></a>Дополнительные справочные материалы
Другие разделы ссылку в hello центра IoT руководстве для разработчиков:

* [Конечные точки центра IoT] [ lnk-endpoints] описывает hello различные конечные точки, предоставляемые каждый центр IoT для операций времени выполнения и управления.
* [Регулирование и квоты] [ lnk-quotas] сведения о квотах hello, применять toohello службы центр IoT и hello регулирования tooexpect поведение при использовании службы hello.
* [Пакеты SDK устройств и служб Azure IoT] [ lnk-sdks] списки hello языка различных пакетов SDK можно использовать при разработке приложений, устройств и служб, которые взаимодействуют с центром IoT.
* [Центр IoT язык запросов для близнецы устройства, задания и маршрутизация сообщений] [ lnk-query] описывает hello tooretrieve сведения из центра IoT близнецы устройства и заданий можно использовать язык запросов центра IoT.
* [Поддержка MQTT концентратора IoT] [ lnk-devguide-mqtt] приведены более подробные сведения о поддержке центра IoT протокола MQTT hello.

## <a name="next-steps"></a>Дальнейшие действия
При желании tootry некоторые основные понятия hello, описанных в этой статье, могут быть интересны следующие учебника центра IoT hello параметры:

* [Планирование и трансляция заданий][lnk-jobs-tutorial]

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-jobs-tutorial]: iot-hub-node-node-schedule-jobs.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-devguide]: iot-hub-devguide-device-twins.md
