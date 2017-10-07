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
# <a name="schedule-jobs-on-multiple-devices"></a><span data-ttu-id="11328-104">Планирование заданий на нескольких устройствах</span><span class="sxs-lookup"><span data-stu-id="11328-104">Schedule jobs on multiple devices</span></span>
## <a name="overview"></a><span data-ttu-id="11328-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="11328-105">Overview</span></span>
<span data-ttu-id="11328-106">Как описано в предыдущих статьях, Центр Интернета вещей Azure включает ряд стандартных блоков ([свойства и теги двойников устройств][lnk-twin-devguide] и [прямые методы][lnk-dev-methods]).</span><span class="sxs-lookup"><span data-stu-id="11328-106">As described by previous articles, Azure IoT Hub enables a number of building blocks ([device twin properties and tags][lnk-twin-devguide] and [direct methods][lnk-dev-methods]).</span></span>  <span data-ttu-id="11328-107">Как правило серверной части приложения включите устройство tooupdate Администраторы и операторы и взаимодействовать с устройствами IoT в пакетном режиме и в запланированное время.</span><span class="sxs-lookup"><span data-stu-id="11328-107">Typically, back-end apps enable device administrators and operators tooupdate and interact with IoT devices in bulk and at a scheduled time.</span></span>  <span data-ttu-id="11328-108">Задания инкапсулируют hello выполнение обновления двойных устройства и непосредственные методы для набора устройств во время расписания.</span><span class="sxs-lookup"><span data-stu-id="11328-108">Jobs encapsulate hello execution of device twin updates and direct methods against a set of devices at a schedule time.</span></span>  <span data-ttu-id="11328-109">Например оператор будет использовать приложение серверной части, которое будет запустите и отслеживайте задания tooreboot на наборе устройств при построении 43 и этаж 3 на время, которое бы не нарушают работу toohello операции построения hello.</span><span class="sxs-lookup"><span data-stu-id="11328-109">For example, an operator would use a back-end app that would initiate and track a job tooreboot a set of devices in building 43 and floor 3 at a time that would not be disruptive toohello operations of hello building.</span></span>

### <a name="when-toouse"></a><span data-ttu-id="11328-110">Когда toouse</span><span class="sxs-lookup"><span data-stu-id="11328-110">When toouse</span></span>
<span data-ttu-id="11328-111">Рассмотрите возможность с помощью заданий при: tooschedule потребностей серверной части решения и отслеживать ход выполнения любой из следующих действий на наборе устройств hello:</span><span class="sxs-lookup"><span data-stu-id="11328-111">Consider using jobs when: a solution back end needs tooschedule and track progress any of hello following activities on a set of device:</span></span>

* <span data-ttu-id="11328-112">Обновление требуемых свойств</span><span class="sxs-lookup"><span data-stu-id="11328-112">Update desired properties</span></span>
* <span data-ttu-id="11328-113">Обновление тегов</span><span class="sxs-lookup"><span data-stu-id="11328-113">Update tags</span></span>
* <span data-ttu-id="11328-114">Вызов прямых методов</span><span class="sxs-lookup"><span data-stu-id="11328-114">Invoke direct methods</span></span>

## <a name="job-lifecycle"></a><span data-ttu-id="11328-115">Жизненный цикл задания</span><span class="sxs-lookup"><span data-stu-id="11328-115">Job lifecycle</span></span>
<span data-ttu-id="11328-116">Заданий инициированных серверной части решения hello и обслуживается центр IoT.</span><span class="sxs-lookup"><span data-stu-id="11328-116">Jobs are initiated by hello solution back end and maintained by IoT Hub.</span></span>  <span data-ttu-id="11328-117">Вы можете инициировать задание, используя обращенный к службе универсальный код ресурса (URI) `{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14` и запросить данные о выполнении задания, используя аналогичный URI `{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`.</span><span class="sxs-lookup"><span data-stu-id="11328-117">You can initiate a job through a service-facing URI (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) and query for progress on an executing job through a service-facing URI (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`).</span></span>  <span data-ttu-id="11328-118">После запуска задания, запрос для задания позволяет hello серверной части приложения toorefresh hello статуса выполняемых заданий.</span><span class="sxs-lookup"><span data-stu-id="11328-118">Once a job is initiated, querying for jobs enables hello back-end app toorefresh hello status of running jobs.</span></span>

> [!NOTE]
> <span data-ttu-id="11328-119">При отправке задания имен и значений свойств может содержать только печатаемые US-ASCII буквенно-цифровых, за исключением в следующий набор hello: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span><span class="sxs-lookup"><span data-stu-id="11328-119">When you initiate a job, property names and values can only contain US-ASCII printable alphanumeric, except any in hello following set: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span></span>
> 
> 

## <a name="reference-topics"></a><span data-ttu-id="11328-120">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="11328-120">Reference topics:</span></span>
<span data-ttu-id="11328-121">Hello следующие справочные разделы предоставляют дополнительные сведения об использовании заданий.</span><span class="sxs-lookup"><span data-stu-id="11328-121">hello following reference topics provide you with more information about using jobs.</span></span>

## <a name="jobs-tooexecute-direct-methods"></a><span data-ttu-id="11328-122">Методы прямой tooexecute заданий</span><span class="sxs-lookup"><span data-stu-id="11328-122">Jobs tooexecute direct methods</span></span>
<span data-ttu-id="11328-123">Hello ниже приводится сведения о запросе hello HTTP 1.1 для выполнения [прямой метод] [ lnk-dev-methods] на наборе устройств с помощью задания:</span><span class="sxs-lookup"><span data-stu-id="11328-123">hello following is hello HTTP 1.1 request details for executing a [direct method][lnk-dev-methods] on a set of devices using a job:</span></span>

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
<span data-ttu-id="11328-124">условия запроса Hello также может быть на одном устройстве идентификатор списка идентификаторов устройств как показано ниже</span><span class="sxs-lookup"><span data-stu-id="11328-124">hello query condition can also be on a single device Id or on a list of device Ids as shown below</span></span>

<span data-ttu-id="11328-125">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="11328-125">**Examples**</span></span>
```
queryCondition = "deviceId = 'MyDevice1'"
queryCondition = "deviceId IN ['MyDevice1','MyDevice2']"
queryCondition = "deviceId IN ['MyDevice1']
```
<span data-ttu-id="11328-126">В статье [Справочник по языку запросов Центр Интернета вещей для двойников устройств и заданий][lnk-query] подробно рассматривается язык запросов Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="11328-126">[IoT Hub Query Language][lnk-query] covers IoT Hub query language in additional detail.</span></span>

## <a name="jobs-tooupdate-device-twin-properties"></a><span data-ttu-id="11328-127">Свойства двойных устройства tooupdate заданий</span><span class="sxs-lookup"><span data-stu-id="11328-127">Jobs tooupdate device twin properties</span></span>
<span data-ttu-id="11328-128">Hello Вот hello HTTP 1.1 сведения о запросе для обновления с помощью задания свойств двойных устройства:</span><span class="sxs-lookup"><span data-stu-id="11328-128">hello following is hello HTTP 1.1 request details for updating device twin properties using a job:</span></span>

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

## <a name="querying-for-progress-on-jobs"></a><span data-ttu-id="11328-129">Запрос на отслеживание выполнения заданий</span><span class="sxs-lookup"><span data-stu-id="11328-129">Querying for progress on jobs</span></span>
<span data-ttu-id="11328-130">Hello Вот hello сведений о запросе HTTP 1.1 для [запрос для задания][lnk-query]:</span><span class="sxs-lookup"><span data-stu-id="11328-130">hello following is hello HTTP 1.1 request details for [querying for jobs][lnk-query]:</span></span>

    ```
    GET /jobs/v2/query?api-version=2016-11-14[&jobType=<jobType>][&jobStatus=<jobStatus>][&pageSize=<pageSize>][&continuationToken=<continuationToken>]

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>
    ```

<span data-ttu-id="11328-131">Hello continuationToken предоставляется из ответа hello.</span><span class="sxs-lookup"><span data-stu-id="11328-131">hello continuationToken is provided from hello response.</span></span>  

## <a name="jobs-properties"></a><span data-ttu-id="11328-132">Свойства заданий</span><span class="sxs-lookup"><span data-stu-id="11328-132">Jobs Properties</span></span>
<span data-ttu-id="11328-133">Hello ниже приведен список свойств и соответствующие описания, которые могут быть использованы при выполнении запроса для заданий или результаты задания.</span><span class="sxs-lookup"><span data-stu-id="11328-133">hello following is a list of properties and corresponding descriptions, which can be used when querying for jobs or job results.</span></span>

| <span data-ttu-id="11328-134">Свойство</span><span class="sxs-lookup"><span data-stu-id="11328-134">Property</span></span> | <span data-ttu-id="11328-135">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="11328-135">Description</span></span> |
| --- | --- |
| <span data-ttu-id="11328-136">**jobId**</span><span class="sxs-lookup"><span data-stu-id="11328-136">**jobId**</span></span> |<span data-ttu-id="11328-137">Идентификатор для задания hello, предоставляемые приложением.</span><span class="sxs-lookup"><span data-stu-id="11328-137">Application provided ID for hello job.</span></span> |
| <span data-ttu-id="11328-138">**startTime**</span><span class="sxs-lookup"><span data-stu-id="11328-138">**startTime**</span></span> |<span data-ttu-id="11328-139">Время начала (ISO 8601) задания hello, предоставляемые приложением.</span><span class="sxs-lookup"><span data-stu-id="11328-139">Application provided start time (ISO-8601) for hello job.</span></span> |
| <span data-ttu-id="11328-140">**endTime**</span><span class="sxs-lookup"><span data-stu-id="11328-140">**endTime**</span></span> |<span data-ttu-id="11328-141">Центр IoT обеспечивает даты (ISO 8601) после завершения задания hello.</span><span class="sxs-lookup"><span data-stu-id="11328-141">IoT Hub provided date (ISO-8601) for when hello job completed.</span></span> <span data-ttu-id="11328-142">Допустимо, только после задания hello достигает состояния hello «завершено».</span><span class="sxs-lookup"><span data-stu-id="11328-142">Valid only after hello job reaches hello 'completed' state.</span></span> |
| <span data-ttu-id="11328-143">**type**</span><span class="sxs-lookup"><span data-stu-id="11328-143">**type**</span></span> |<span data-ttu-id="11328-144">Типы заданий:</span><span class="sxs-lookup"><span data-stu-id="11328-144">Types of jobs:</span></span> |
| <span data-ttu-id="11328-145">**scheduledUpdateTwin**: tooupdate задания используемого набора требуемые свойства или теги.</span><span class="sxs-lookup"><span data-stu-id="11328-145">**scheduledUpdateTwin**: A job used tooupdate a set of desired properties or tags.</span></span> | |
| <span data-ttu-id="11328-146">**scheduledDeviceMethod**: tooinvoke задания используется метод на наборе устройств близнецы устройства.</span><span class="sxs-lookup"><span data-stu-id="11328-146">**scheduledDeviceMethod**: A job used tooinvoke a device method on a set of device twins.</span></span> | |
| <span data-ttu-id="11328-147">**состояние**</span><span class="sxs-lookup"><span data-stu-id="11328-147">**status**</span></span> |<span data-ttu-id="11328-148">Текущее состояние задания hello.</span><span class="sxs-lookup"><span data-stu-id="11328-148">Current state of hello job.</span></span> <span data-ttu-id="11328-149">Возможные значения состояния:</span><span class="sxs-lookup"><span data-stu-id="11328-149">Possible values for status:</span></span> |
| <span data-ttu-id="11328-150">**Ожидание** : запланированное и ожидания toobe заберет службы заданий hello.</span><span class="sxs-lookup"><span data-stu-id="11328-150">**pending** : Scheduled and waiting toobe picked up by hello job service.</span></span> | |
| <span data-ttu-id="11328-151">**запланированные** : запланирована на время в будущем hello.</span><span class="sxs-lookup"><span data-stu-id="11328-151">**scheduled** : Scheduled for a time in hello future.</span></span> | |
| <span data-ttu-id="11328-152">**running** — задание сейчас активно.</span><span class="sxs-lookup"><span data-stu-id="11328-152">**running** : Currently active job.</span></span> | |
| <span data-ttu-id="11328-153">**cancelled** — задание отменено.</span><span class="sxs-lookup"><span data-stu-id="11328-153">**cancelled** : Job has been cancelled.</span></span> | |
| <span data-ttu-id="11328-154">**failed** — произошел сбой задания.</span><span class="sxs-lookup"><span data-stu-id="11328-154">**failed** : Job failed.</span></span> | |
| <span data-ttu-id="11328-155">**completed** — задание завершено.</span><span class="sxs-lookup"><span data-stu-id="11328-155">**completed** : Job has completed.</span></span> | |
| <span data-ttu-id="11328-156">**deviceJobStatistics**</span><span class="sxs-lookup"><span data-stu-id="11328-156">**deviceJobStatistics**</span></span> |<span data-ttu-id="11328-157">Статистика выполнения задания hello.</span><span class="sxs-lookup"><span data-stu-id="11328-157">Statistics about hello job's execution.</span></span> |

<span data-ttu-id="11328-158">Свойства **deviceJobStatistics**.</span><span class="sxs-lookup"><span data-stu-id="11328-158">**deviceJobStatistics** properties.</span></span>

| <span data-ttu-id="11328-159">Свойство</span><span class="sxs-lookup"><span data-stu-id="11328-159">Property</span></span> | <span data-ttu-id="11328-160">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="11328-160">Description</span></span> |
| --- | --- |
| <span data-ttu-id="11328-161">**deviceJobStatistics.deviceCount**</span><span class="sxs-lookup"><span data-stu-id="11328-161">**deviceJobStatistics.deviceCount**</span></span> |<span data-ttu-id="11328-162">Количество устройств в задании hello.</span><span class="sxs-lookup"><span data-stu-id="11328-162">Number of devices in hello job.</span></span> |
| <span data-ttu-id="11328-163">**deviceJobStatistics.failedCount**</span><span class="sxs-lookup"><span data-stu-id="11328-163">**deviceJobStatistics.failedCount**</span></span> |<span data-ttu-id="11328-164">Количество устройств, где hello не удалась.</span><span class="sxs-lookup"><span data-stu-id="11328-164">Number of devices where hello job failed.</span></span> |
| <span data-ttu-id="11328-165">**deviceJobStatistics.succeededCount**</span><span class="sxs-lookup"><span data-stu-id="11328-165">**deviceJobStatistics.succeededCount**</span></span> |<span data-ttu-id="11328-166">Количество устройств, где hello задание успешно выполнено.</span><span class="sxs-lookup"><span data-stu-id="11328-166">Number of devices where hello job succeeded.</span></span> |
| <span data-ttu-id="11328-167">**deviceJobStatistics.runningCount**</span><span class="sxs-lookup"><span data-stu-id="11328-167">**deviceJobStatistics.runningCount**</span></span> |<span data-ttu-id="11328-168">Количество устройств, которые в данный момент выполняются задания hello.</span><span class="sxs-lookup"><span data-stu-id="11328-168">Number of devices that are currently running hello job.</span></span> |
| <span data-ttu-id="11328-169">**deviceJobStatistics.pendingCount**</span><span class="sxs-lookup"><span data-stu-id="11328-169">**deviceJobStatistics.pendingCount**</span></span> |<span data-ttu-id="11328-170">Количество устройств, ожидающих toorun hello задания.</span><span class="sxs-lookup"><span data-stu-id="11328-170">Number of devices that are pending toorun hello job.</span></span> |

### <a name="additional-reference-material"></a><span data-ttu-id="11328-171">Дополнительные справочные материалы</span><span class="sxs-lookup"><span data-stu-id="11328-171">Additional reference material</span></span>
<span data-ttu-id="11328-172">Другие разделы ссылку в hello центра IoT руководстве для разработчиков:</span><span class="sxs-lookup"><span data-stu-id="11328-172">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="11328-173">[Конечные точки центра IoT] [ lnk-endpoints] описывает hello различные конечные точки, предоставляемые каждый центр IoT для операций времени выполнения и управления.</span><span class="sxs-lookup"><span data-stu-id="11328-173">[IoT Hub endpoints][lnk-endpoints] describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="11328-174">[Регулирование и квоты] [ lnk-quotas] сведения о квотах hello, применять toohello службы центр IoT и hello регулирования tooexpect поведение при использовании службы hello.</span><span class="sxs-lookup"><span data-stu-id="11328-174">[Throttling and quotas][lnk-quotas] describes hello quotas that apply toohello IoT Hub service and hello throttling behavior tooexpect when you use hello service.</span></span>
* <span data-ttu-id="11328-175">[Пакеты SDK устройств и служб Azure IoT] [ lnk-sdks] списки hello языка различных пакетов SDK можно использовать при разработке приложений, устройств и служб, которые взаимодействуют с центром IoT.</span><span class="sxs-lookup"><span data-stu-id="11328-175">[Azure IoT device and service SDKs][lnk-sdks] lists hello various language SDKs you an use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="11328-176">[Центр IoT язык запросов для близнецы устройства, задания и маршрутизация сообщений] [ lnk-query] описывает hello tooretrieve сведения из центра IoT близнецы устройства и заданий можно использовать язык запросов центра IoT.</span><span class="sxs-lookup"><span data-stu-id="11328-176">[IoT Hub query language for device twins, jobs, and message routing][lnk-query] describes hello IoT Hub query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="11328-177">[Поддержка MQTT концентратора IoT] [ lnk-devguide-mqtt] приведены более подробные сведения о поддержке центра IoT протокола MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="11328-177">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="11328-178">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="11328-178">Next steps</span></span>
<span data-ttu-id="11328-179">При желании tootry некоторые основные понятия hello, описанных в этой статье, могут быть интересны следующие учебника центра IoT hello параметры:</span><span class="sxs-lookup"><span data-stu-id="11328-179">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorial:</span></span>

* <span data-ttu-id="11328-180">[Планирование и трансляция заданий][lnk-jobs-tutorial]</span><span class="sxs-lookup"><span data-stu-id="11328-180">[Schedule and broadcast jobs][lnk-jobs-tutorial]</span></span>

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
