---
title: "Общие сведения о заданиях Центра Интернета вещей Azure | Документация Майкрософт"
description: "Руководство разработчика. Планирование выполнения заданий на нескольких устройствах, подключенных к Центру Интернета вещей. Задания могут обновлять теги и требуемые свойства, а также вызывать прямые методы на нескольких устройствах."
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
ms.openlocfilehash: abb7f80662650efa8f158f32125ebc5350cb4f62
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="schedule-jobs-on-multiple-devices"></a><span data-ttu-id="7c392-104">Планирование заданий на нескольких устройствах</span><span class="sxs-lookup"><span data-stu-id="7c392-104">Schedule jobs on multiple devices</span></span>
## <a name="overview"></a><span data-ttu-id="7c392-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="7c392-105">Overview</span></span>
<span data-ttu-id="7c392-106">Как описано в предыдущих статьях, Центр Интернета вещей Azure включает ряд стандартных блоков ([свойства и теги двойников устройств][lnk-twin-devguide] и [прямые методы][lnk-dev-methods]).</span><span class="sxs-lookup"><span data-stu-id="7c392-106">As described by previous articles, Azure IoT Hub enables a number of building blocks ([device twin properties and tags][lnk-twin-devguide] and [direct methods][lnk-dev-methods]).</span></span>  <span data-ttu-id="7c392-107">Как правило, внутренние приложения позволяют администраторам и операторам устройств массово и в запланированное время обновлять устройства Интернета вещей и взаимодействовать с ними.</span><span class="sxs-lookup"><span data-stu-id="7c392-107">Typically, back-end apps enable device administrators and operators to update and interact with IoT devices in bulk and at a scheduled time.</span></span>  <span data-ttu-id="7c392-108">На запланированное время задания инкапсулируют выполнение обновлений двойников устройств и прямых методов для ряда устройств.</span><span class="sxs-lookup"><span data-stu-id="7c392-108">Jobs encapsulate the execution of device twin updates and direct methods against a set of devices at a schedule time.</span></span>  <span data-ttu-id="7c392-109">Например, оператор использует внутреннее приложение, которое инициирует задание перезапуска ряда устройств на третьем этаже в здании №43 в определенное время и отслеживает ход его выполнения. При этом задание не будет нарушать выполнение других операций в здании.</span><span class="sxs-lookup"><span data-stu-id="7c392-109">For example, an operator would use a back-end app that would initiate and track a job to reboot a set of devices in building 43 and floor 3 at a time that would not be disruptive to the operations of the building.</span></span>

### <a name="when-to-use"></a><span data-ttu-id="7c392-110">Сценарии использования</span><span class="sxs-lookup"><span data-stu-id="7c392-110">When to use</span></span>
<span data-ttu-id="7c392-111">Используйте задания, если в серверной части решения необходимо запланировать выполнение задания на ряде устройств, а также настроить отслеживание выполнения действий:</span><span class="sxs-lookup"><span data-stu-id="7c392-111">Consider using jobs when: a solution back end needs to schedule and track progress any of the following activities on a set of device:</span></span>

* <span data-ttu-id="7c392-112">Обновление требуемых свойств</span><span class="sxs-lookup"><span data-stu-id="7c392-112">Update desired properties</span></span>
* <span data-ttu-id="7c392-113">Обновление тегов</span><span class="sxs-lookup"><span data-stu-id="7c392-113">Update tags</span></span>
* <span data-ttu-id="7c392-114">Вызов прямых методов</span><span class="sxs-lookup"><span data-stu-id="7c392-114">Invoke direct methods</span></span>

## <a name="job-lifecycle"></a><span data-ttu-id="7c392-115">Жизненный цикл задания</span><span class="sxs-lookup"><span data-stu-id="7c392-115">Job lifecycle</span></span>
<span data-ttu-id="7c392-116">Задания инициируются в серверной части решения, а осуществляются с помощью Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="7c392-116">Jobs are initiated by the solution back end and maintained by IoT Hub.</span></span>  <span data-ttu-id="7c392-117">Вы можете инициировать задание, используя обращенный к службе универсальный код ресурса (URI) `{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14` и запросить данные о выполнении задания, используя аналогичный URI `{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`.</span><span class="sxs-lookup"><span data-stu-id="7c392-117">You can initiate a job through a service-facing URI (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) and query for progress on an executing job through a service-facing URI (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`).</span></span>  <span data-ttu-id="7c392-118">Если запросить задание после запуска, внутреннее приложение обновит состояние выполняемых заданий.</span><span class="sxs-lookup"><span data-stu-id="7c392-118">Once a job is initiated, querying for jobs enables the back-end app to refresh the status of running jobs.</span></span>

> [!NOTE]
> <span data-ttu-id="7c392-119">При запуске задания в именах и значениях свойств должны содержаться только печатаемые буквенно-цифровые символы US-ASCII, кроме следующих: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span><span class="sxs-lookup"><span data-stu-id="7c392-119">When you initiate a job, property names and values can only contain US-ASCII printable alphanumeric, except any in the following set: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span></span>
> 
> 

## <a name="reference-topics"></a><span data-ttu-id="7c392-120">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="7c392-120">Reference topics:</span></span>
<span data-ttu-id="7c392-121">Далее предоставлены дополнительные сведения об использовании заданий.</span><span class="sxs-lookup"><span data-stu-id="7c392-121">The following reference topics provide you with more information about using jobs.</span></span>

## <a name="jobs-to-execute-direct-methods"></a><span data-ttu-id="7c392-122">Задания для выполнения прямого метода</span><span class="sxs-lookup"><span data-stu-id="7c392-122">Jobs to execute direct methods</span></span>
<span data-ttu-id="7c392-123">Приведенный ниже запрос HTTP 1.1 предназначен для выполнения [прямого метода][lnk-dev-methods] с использованием задания на ряде устройств:</span><span class="sxs-lookup"><span data-stu-id="7c392-123">The following is the HTTP 1.1 request details for executing a [direct method][lnk-dev-methods] on a set of devices using a job:</span></span>

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
<span data-ttu-id="7c392-124">Условие запроса также может находиться в одном идентификаторе устройства или в списке идентификаторов устройств, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="7c392-124">The query condition can also be on a single device Id or on a list of device Ids as shown below</span></span>

<span data-ttu-id="7c392-125">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="7c392-125">**Examples**</span></span>
```
queryCondition = "deviceId = 'MyDevice1'"
queryCondition = "deviceId IN ['MyDevice1','MyDevice2']"
queryCondition = "deviceId IN ['MyDevice1']
```
<span data-ttu-id="7c392-126">В статье [Справочник по языку запросов Центр Интернета вещей для двойников устройств и заданий][lnk-query] подробно рассматривается язык запросов Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="7c392-126">[IoT Hub Query Language][lnk-query] covers IoT Hub query language in additional detail.</span></span>

## <a name="jobs-to-update-device-twin-properties"></a><span data-ttu-id="7c392-127">Задания для обновления свойств устройств-двойников</span><span class="sxs-lookup"><span data-stu-id="7c392-127">Jobs to update device twin properties</span></span>
<span data-ttu-id="7c392-128">Запрос HTTP 1.1 ниже предполагает обновление свойств устройства-двойника с использованием задания:</span><span class="sxs-lookup"><span data-stu-id="7c392-128">The following is the HTTP 1.1 request details for updating device twin properties using a job:</span></span>

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

## <a name="querying-for-progress-on-jobs"></a><span data-ttu-id="7c392-129">Запрос на отслеживание выполнения заданий</span><span class="sxs-lookup"><span data-stu-id="7c392-129">Querying for progress on jobs</span></span>
<span data-ttu-id="7c392-130">Приведенный ниже запрос HTTP 1.1 предусматривает [получение данных о ходе выполнения заданий][lnk-query]:</span><span class="sxs-lookup"><span data-stu-id="7c392-130">The following is the HTTP 1.1 request details for [querying for jobs][lnk-query]:</span></span>

    ```
    GET /jobs/v2/query?api-version=2016-11-14[&jobType=<jobType>][&jobStatus=<jobStatus>][&pageSize=<pageSize>][&continuationToken=<continuationToken>]

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>
    ```

<span data-ttu-id="7c392-131">Объект continuationToken получен в рамках ответа.</span><span class="sxs-lookup"><span data-stu-id="7c392-131">The continuationToken is provided from the response.</span></span>  

## <a name="jobs-properties"></a><span data-ttu-id="7c392-132">Свойства заданий</span><span class="sxs-lookup"><span data-stu-id="7c392-132">Jobs Properties</span></span>
<span data-ttu-id="7c392-133">В таблице ниже содержится список свойств, которые можно использовать при выполнении запросов на задания и их результаты, а также описание этих свойств.</span><span class="sxs-lookup"><span data-stu-id="7c392-133">The following is a list of properties and corresponding descriptions, which can be used when querying for jobs or job results.</span></span>

| <span data-ttu-id="7c392-134">Свойство</span><span class="sxs-lookup"><span data-stu-id="7c392-134">Property</span></span> | <span data-ttu-id="7c392-135">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="7c392-135">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7c392-136">**jobId**</span><span class="sxs-lookup"><span data-stu-id="7c392-136">**jobId**</span></span> |<span data-ttu-id="7c392-137">Идентификатор задания, указанный в приложении.</span><span class="sxs-lookup"><span data-stu-id="7c392-137">Application provided ID for the job.</span></span> |
| <span data-ttu-id="7c392-138">**startTime**</span><span class="sxs-lookup"><span data-stu-id="7c392-138">**startTime**</span></span> |<span data-ttu-id="7c392-139">Время начала задания (ISO-8601), указанное в приложении.</span><span class="sxs-lookup"><span data-stu-id="7c392-139">Application provided start time (ISO-8601) for the job.</span></span> |
| <span data-ttu-id="7c392-140">**endTime**</span><span class="sxs-lookup"><span data-stu-id="7c392-140">**endTime**</span></span> |<span data-ttu-id="7c392-141">Дата завершения задания (ISO-8601), указанная в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="7c392-141">IoT Hub provided date (ISO-8601) for when the job completed.</span></span> <span data-ttu-id="7c392-142">Она допустима только после перехода задания в завершенное состояние.</span><span class="sxs-lookup"><span data-stu-id="7c392-142">Valid only after the job reaches the 'completed' state.</span></span> |
| <span data-ttu-id="7c392-143">**type**</span><span class="sxs-lookup"><span data-stu-id="7c392-143">**type**</span></span> |<span data-ttu-id="7c392-144">Типы заданий:</span><span class="sxs-lookup"><span data-stu-id="7c392-144">Types of jobs:</span></span> |
| <span data-ttu-id="7c392-145">**scheduledUpdateTwin** — задание по обновлению набора требуемых свойств или тегов.</span><span class="sxs-lookup"><span data-stu-id="7c392-145">**scheduledUpdateTwin**: A job used to update a set of desired properties or tags.</span></span> | |
| <span data-ttu-id="7c392-146">**scheduledDeviceMethod** — задание по вызову метода устройства для набора двойников устройств.</span><span class="sxs-lookup"><span data-stu-id="7c392-146">**scheduledDeviceMethod**: A job used to invoke a device method on a set of device twins.</span></span> | |
| <span data-ttu-id="7c392-147">**состояние**</span><span class="sxs-lookup"><span data-stu-id="7c392-147">**status**</span></span> |<span data-ttu-id="7c392-148">Текущее состояние задания.</span><span class="sxs-lookup"><span data-stu-id="7c392-148">Current state of the job.</span></span> <span data-ttu-id="7c392-149">Возможные значения состояния:</span><span class="sxs-lookup"><span data-stu-id="7c392-149">Possible values for status:</span></span> |
| <span data-ttu-id="7c392-150">**pending** — задание запланировано и ожидает действий от службы заданий.</span><span class="sxs-lookup"><span data-stu-id="7c392-150">**pending** : Scheduled and waiting to be picked up by the job service.</span></span> | |
| <span data-ttu-id="7c392-151">**scheduled** — задание запланировано на будущее.</span><span class="sxs-lookup"><span data-stu-id="7c392-151">**scheduled** : Scheduled for a time in the future.</span></span> | |
| <span data-ttu-id="7c392-152">**running** — задание сейчас активно.</span><span class="sxs-lookup"><span data-stu-id="7c392-152">**running** : Currently active job.</span></span> | |
| <span data-ttu-id="7c392-153">**cancelled** — задание отменено.</span><span class="sxs-lookup"><span data-stu-id="7c392-153">**cancelled** : Job has been cancelled.</span></span> | |
| <span data-ttu-id="7c392-154">**failed** — произошел сбой задания.</span><span class="sxs-lookup"><span data-stu-id="7c392-154">**failed** : Job failed.</span></span> | |
| <span data-ttu-id="7c392-155">**completed** — задание завершено.</span><span class="sxs-lookup"><span data-stu-id="7c392-155">**completed** : Job has completed.</span></span> | |
| <span data-ttu-id="7c392-156">**deviceJobStatistics**</span><span class="sxs-lookup"><span data-stu-id="7c392-156">**deviceJobStatistics**</span></span> |<span data-ttu-id="7c392-157">Статистика задания.</span><span class="sxs-lookup"><span data-stu-id="7c392-157">Statistics about the job's execution.</span></span> |

<span data-ttu-id="7c392-158">Свойства **deviceJobStatistics**.</span><span class="sxs-lookup"><span data-stu-id="7c392-158">**deviceJobStatistics** properties.</span></span>

| <span data-ttu-id="7c392-159">Свойство</span><span class="sxs-lookup"><span data-stu-id="7c392-159">Property</span></span> | <span data-ttu-id="7c392-160">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="7c392-160">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7c392-161">**deviceJobStatistics.deviceCount**</span><span class="sxs-lookup"><span data-stu-id="7c392-161">**deviceJobStatistics.deviceCount**</span></span> |<span data-ttu-id="7c392-162">Количество устройств в задании.</span><span class="sxs-lookup"><span data-stu-id="7c392-162">Number of devices in the job.</span></span> |
| <span data-ttu-id="7c392-163">**deviceJobStatistics.failedCount**</span><span class="sxs-lookup"><span data-stu-id="7c392-163">**deviceJobStatistics.failedCount**</span></span> |<span data-ttu-id="7c392-164">Количество устройств, на которых произошел сбой задания.</span><span class="sxs-lookup"><span data-stu-id="7c392-164">Number of devices where the job failed.</span></span> |
| <span data-ttu-id="7c392-165">**deviceJobStatistics.succeededCount**</span><span class="sxs-lookup"><span data-stu-id="7c392-165">**deviceJobStatistics.succeededCount**</span></span> |<span data-ttu-id="7c392-166">Количество устройств, на которых задание выполнено успешно.</span><span class="sxs-lookup"><span data-stu-id="7c392-166">Number of devices where the job succeeded.</span></span> |
| <span data-ttu-id="7c392-167">**deviceJobStatistics.runningCount**</span><span class="sxs-lookup"><span data-stu-id="7c392-167">**deviceJobStatistics.runningCount**</span></span> |<span data-ttu-id="7c392-168">Количество устройств, на которых сейчас выполняется задание.</span><span class="sxs-lookup"><span data-stu-id="7c392-168">Number of devices that are currently running the job.</span></span> |
| <span data-ttu-id="7c392-169">**deviceJobStatistics.pendingCount**</span><span class="sxs-lookup"><span data-stu-id="7c392-169">**deviceJobStatistics.pendingCount**</span></span> |<span data-ttu-id="7c392-170">Количество устройств, на которых сейчас ожидается выполнение задания.</span><span class="sxs-lookup"><span data-stu-id="7c392-170">Number of devices that are pending to run the job.</span></span> |

### <a name="additional-reference-material"></a><span data-ttu-id="7c392-171">Дополнительные справочные материалы</span><span class="sxs-lookup"><span data-stu-id="7c392-171">Additional reference material</span></span>
<span data-ttu-id="7c392-172">Другие справочные статьи в руководстве разработчика для Центра Интернета вещей:</span><span class="sxs-lookup"><span data-stu-id="7c392-172">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="7c392-173">Статья [IoT Hub endpoints][lnk-endpoints] (Конечные точки Центра Интернета вещей) содержит сведения о конечных точках, которые каждый Центр Интернета вещей предоставляет для операций управления и среды выполнения.</span><span class="sxs-lookup"><span data-stu-id="7c392-173">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="7c392-174">Статья [Throttling and quotas][lnk-quotas] (Регулирование и квоты) содержит сведения о квотах, применимых к службе Центра Интернета вещей, и ожидаемом поведении регулирования при использовании службы.</span><span class="sxs-lookup"><span data-stu-id="7c392-174">[Throttling and quotas][lnk-quotas] describes the quotas that apply to the IoT Hub service and the throttling behavior to expect when you use the service.</span></span>
* <span data-ttu-id="7c392-175">В статье [Azure IoT device and service SDKs][lnk-sdks] (Пакеты SDK для устройств и служб Azure IoT) указаны различные языковые пакеты SDK, которые можно использовать при разработке приложений для устройств и служб, взаимодействующих с Центром Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="7c392-175">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you an use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="7c392-176">[Справочник по языку запросов Центра Интернета вещей для двойников устройств, заданий и маршрутизации сообщений][lnk-query] содержит сведения о языке запросов, который можно использовать для получения сведений о двойниках устройств и заданиях из Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="7c392-176">[IoT Hub query language for device twins, jobs, and message routing][lnk-query] describes the IoT Hub query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="7c392-177">Статья [Поддержка MQTT в Центре Интернета вещей][lnk-devguide-mqtt] содержит дополнительные сведения о поддержке протокола MQTT в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="7c392-177">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7c392-178">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7c392-178">Next steps</span></span>
<span data-ttu-id="7c392-179">Если вы хотели бы применить на практике некоторые основные понятия, описанные в этой статье, можно просмотреть следующее руководство по Центру Интернета вещей:</span><span class="sxs-lookup"><span data-stu-id="7c392-179">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorial:</span></span>

* <span data-ttu-id="7c392-180">[Планирование и трансляция заданий][lnk-jobs-tutorial]</span><span class="sxs-lookup"><span data-stu-id="7c392-180">[Schedule and broadcast jobs][lnk-jobs-tutorial]</span></span>

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
