---
title: "методы прямой aaaUnderstand центр IoT Azure | Документы Microsoft"
description: "Руководство разработчика - использовать прямые методы tooinvoke код на устройствах из приложения службы."
services: iot-hub
documentationcenter: .net
author: nberdy
manager: timlt
editor: 
ms.assetid: 9f0535f1-02e6-467a-9fc4-c0950702102d
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0d15d44a0c3e1d1cda1669c1ed011c2f932e3d92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-invoke-direct-methods-from-iot-hub"></a><span data-ttu-id="836a5-103">Общие сведения о прямых методах и информация о вызове этих методов из Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="836a5-103">Understand and invoke direct methods from IoT Hub</span></span>
## <a name="overview"></a><span data-ttu-id="836a5-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="836a5-104">Overview</span></span>
<span data-ttu-id="836a5-105">Центр IoT дает возможность tooinvoke непосредственные методы на устройствах из облака hello.</span><span class="sxs-lookup"><span data-stu-id="836a5-105">IoT Hub gives you ability tooinvoke direct methods on devices from hello cloud.</span></span> <span data-ttu-id="836a5-106">Непосредственные методы представляют взаимодействия запрос ответ с аналогичные tooan устройства, вызовите HTTP, в том, что они завершаются успехом или сбоем немедленно (после указанного пользователем времени ожидания).</span><span class="sxs-lookup"><span data-stu-id="836a5-106">Direct methods represent a request-reply interaction with a device similar tooan HTTP call in that they succeed or fail immediately (after a user-specified timeout).</span></span> <span data-ttu-id="836a5-107">Это полезно в сценариях, где hello набор действий, немедленно отличается в зависимости от того, было ли устройство hello может toorespond, например отправлять SMS tooa пробуждения устройства, если устройство находится в автономном режиме (SMS, дороже, чем вызов метода).</span><span class="sxs-lookup"><span data-stu-id="836a5-107">This is useful for scenarios where hello course of immediate action is different depending on whether hello device was able toorespond, such as sending an SMS wake-up tooa device if a device is offline (SMS being more expensive than a method call).</span></span>

<span data-ttu-id="836a5-108">Каждый метод устройства предназначен для одного устройства.</span><span class="sxs-lookup"><span data-stu-id="836a5-108">Each device method targets a single device.</span></span> <span data-ttu-id="836a5-109">[Задания] [ lnk-devguide-jobs] предоставляют прямые методы tooinvoke способом на нескольких устройствах и запланировать вызов метода для отключенных устройств.</span><span class="sxs-lookup"><span data-stu-id="836a5-109">[Jobs][lnk-devguide-jobs] provide a way tooinvoke direct methods on multiple devices, and schedule method invocation for disconnected devices.</span></span>

<span data-ttu-id="836a5-110">Любой пользователь с разрешениями на **подключение службы** в Центре Интернета вещей может вызвать метод на устройстве.</span><span class="sxs-lookup"><span data-stu-id="836a5-110">Anyone with **service connect** permissions on IoT Hub may invoke a method on a device.</span></span>

### <a name="when-toouse"></a><span data-ttu-id="836a5-111">Когда toouse</span><span class="sxs-lookup"><span data-stu-id="836a5-111">When toouse</span></span>
<span data-ttu-id="836a5-112">Непосредственные методы соответствуют шаблону запрос ответ и предназначены для обмена данными, которые требуют немедленного подтверждения их результат обычно интерактивного управления hello устройства, например tooturn на вентилятора.</span><span class="sxs-lookup"><span data-stu-id="836a5-112">Direct methods follow a request-response pattern and are meant for communications that require immediate confirmation of their result, usually interactive control of hello device, for example tooturn on a fan.</span></span>

<span data-ttu-id="836a5-113">См. слишком[руководство связи облака на устройство] [ lnk-c2d-guidance] в случае неясностей между нужными свойствами с помощью прямой методов или сообщения облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="836a5-113">Refer too[Cloud-to-device communication guidance][lnk-c2d-guidance] if in doubt between using desired properties, direct methods, or cloud-to-device messages.</span></span>

## <a name="method-lifecycle"></a><span data-ttu-id="836a5-114">Жизненный цикл метода</span><span class="sxs-lookup"><span data-stu-id="836a5-114">Method lifecycle</span></span>
<span data-ttu-id="836a5-115">Прямой методы реализуются на устройстве hello и может потребовать ноль или более входов в полезных данных toocorrectly hello метод создания экземпляра.</span><span class="sxs-lookup"><span data-stu-id="836a5-115">Direct methods are implemented on hello device and may require zero or more inputs in hello method payload toocorrectly instantiate.</span></span> <span data-ttu-id="836a5-116">Вызов прямого метода осуществляется через обращенный к службе URI (`{iot hub}/twins/{device id}/methods/`).</span><span class="sxs-lookup"><span data-stu-id="836a5-116">You invoke a direct method through a service-facing URI (`{iot hub}/twins/{device id}/methods/`).</span></span> <span data-ttu-id="836a5-117">Устройство получает прямые методы через раздел MQTT для устройства (`$iothub/methods/POST/{method name}/`).</span><span class="sxs-lookup"><span data-stu-id="836a5-117">A device receives direct methods through a device-specific MQTT topic (`$iothub/methods/POST/{method name}/`).</span></span> <span data-ttu-id="836a5-118">Корпорация Майкрософт может поддерживает прямой методов на дополнительные сетевые протоколы стороне устройства в будущем hello.</span><span class="sxs-lookup"><span data-stu-id="836a5-118">We may support direct methods on additional device-side networking protocols in hello future.</span></span>

> [!NOTE]
> <span data-ttu-id="836a5-119">При вызове прямого метода на устройстве, имена и значения свойств может содержать только печатаемые US-ASCII буквенно-цифровых, за исключением в следующий набор hello: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span><span class="sxs-lookup"><span data-stu-id="836a5-119">When you invoke a direct method on a device, property names and values can only contain US-ASCII printable alphanumeric, except any in hello following set: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span></span>
> 
> 

<span data-ttu-id="836a5-120">Прямое синхронных методов и либо выполняются успешно или не истечет время ожидания hello (по умолчанию: 30 секунд, можно задать вверх too3600 секунд).</span><span class="sxs-lookup"><span data-stu-id="836a5-120">Direct methods are synchronous and either succeed or fail after hello timeout period (default: 30 seconds, settable up too3600 seconds).</span></span> <span data-ttu-id="836a5-121">Прямой методы полезны в интерактивных сценариев место tooact устройства только в том случае, если hello устройство находится в сети и получения команд, такие как включение индикатор с помощью мобильного телефона.</span><span class="sxs-lookup"><span data-stu-id="836a5-121">Direct methods are useful in interactive scenarios where you want a device tooact if and only if hello device is online and receiving commands, such as turning on a light from a phone.</span></span> <span data-ttu-id="836a5-122">В этих сценариях необходимо toosee немедленно успешное выполнение или сбой, как можно быстрее hello облачная служба может действовать на результат hello.</span><span class="sxs-lookup"><span data-stu-id="836a5-122">In these scenarios, you want toosee an immediate success or failure so hello cloud service can act on hello result as soon as possible.</span></span> <span data-ttu-id="836a5-123">Hello устройство может возвращать некоторые сообщения, в результате метод hello, но это не требуется для метода toodo hello.</span><span class="sxs-lookup"><span data-stu-id="836a5-123">hello device may return some message body as a result of hello method, but it isn't required for hello method toodo so.</span></span> <span data-ttu-id="836a5-124">Упорядочивание или обеспечение какой-либо семантики параллелизма при вызове метода не гарантировано.</span><span class="sxs-lookup"><span data-stu-id="836a5-124">There is no guarantee on ordering or any concurrency semantics on method calls.</span></span>

<span data-ttu-id="836a5-125">Прямой метод HTTP-только со стороны облачной hello и только со стороны устройства hello MQTT.</span><span class="sxs-lookup"><span data-stu-id="836a5-125">Direct method are HTTP-only from hello cloud side, and MQTT-only from hello device side.</span></span>

<span data-ttu-id="836a5-126">полезные данные Hello метод запросов и ответов является документ JSON вверх too8KB.</span><span class="sxs-lookup"><span data-stu-id="836a5-126">hello payload for method requests and responses is a JSON document up too8KB.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="836a5-127">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="836a5-127">Reference topics:</span></span>
<span data-ttu-id="836a5-128">Hello следующие справочные разделы предоставляют дополнительные сведения об использовании непосредственные методы.</span><span class="sxs-lookup"><span data-stu-id="836a5-128">hello following reference topics provide you with more information about using direct methods.</span></span>

## <a name="invoke-a-direct-method-from-a-back-end-app"></a><span data-ttu-id="836a5-129">Вызов прямого метода из серверного приложения</span><span class="sxs-lookup"><span data-stu-id="836a5-129">Invoke a direct method from a back-end app</span></span>
### <a name="method-invocation"></a><span data-ttu-id="836a5-130">Вызов метода</span><span class="sxs-lookup"><span data-stu-id="836a5-130">Method invocation</span></span>
<span data-ttu-id="836a5-131">Вызов прямого метода на устройстве является вызовом HTTP, включающим следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="836a5-131">Direct method invocations on a device are HTTP calls which comprise:</span></span>

* <span data-ttu-id="836a5-132">Hello *URI* toohello конкретного устройства (`{iot hub}/twins/{device id}/methods/`)</span><span class="sxs-lookup"><span data-stu-id="836a5-132">hello *URI* specific toohello device (`{iot hub}/twins/{device id}/methods/`)</span></span>
* <span data-ttu-id="836a5-133">Hello POST *метод*</span><span class="sxs-lookup"><span data-stu-id="836a5-133">hello POST *method*</span></span>
* <span data-ttu-id="836a5-134">*Заголовки* которого содержит hello авторизации, необходимо запросить идентификатор, тип содержимого и кодировку содержимого</span><span class="sxs-lookup"><span data-stu-id="836a5-134">*Headers* which contain hello authorization, request ID, content type, and content encoding</span></span>
* <span data-ttu-id="836a5-135">Прозрачный JSON *текст* в hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="836a5-135">A transparent JSON *body* in hello following format:</span></span>

```
{
    "methodName": "reboot",
    "responseTimeoutInSeconds": 200,
    "payload": {
        "input1": "someInput",
        "input2": "anotherInput"
    }
}
```

<span data-ttu-id="836a5-136">Время ожидания измеряется в секундах.</span><span class="sxs-lookup"><span data-stu-id="836a5-136">Timeout is in seconds.</span></span> <span data-ttu-id="836a5-137">Если время ожидания не задано, то по умолчанию too30 секунд.</span><span class="sxs-lookup"><span data-stu-id="836a5-137">If timeout is not set, it defaults too30 seconds.</span></span>

### <a name="response"></a><span data-ttu-id="836a5-138">Ответ</span><span class="sxs-lookup"><span data-stu-id="836a5-138">Response</span></span>
<span data-ttu-id="836a5-139">приложение Hello внутренней получает ответ, который включает в себя:</span><span class="sxs-lookup"><span data-stu-id="836a5-139">hello back-end app receives a response which comprises:</span></span>

* <span data-ttu-id="836a5-140">*Код состояния HTTP*, который используется для ошибок, поступающих от hello центра IoT, включая ошибки 404 для устройств в настоящее время не подключен</span><span class="sxs-lookup"><span data-stu-id="836a5-140">*HTTP status code*, which is used for errors coming from hello IoT Hub, including a 404 error for devices not currently connected</span></span>
* <span data-ttu-id="836a5-141">*Заголовки* которой содержат hello ETag, необходимо запросить идентификатор, тип содержимого и кодировку содержимого</span><span class="sxs-lookup"><span data-stu-id="836a5-141">*Headers* which contain hello ETag, request ID, content type, and content encoding</span></span>
* <span data-ttu-id="836a5-142">JSON *текст* в hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="836a5-142">A JSON *body* in hello following format:</span></span>

```
{
    "status" : 201,
    "payload" : {...}
}
```

   <span data-ttu-id="836a5-143">Оба `status` и `body` предоставляются устройством hello и использовать toorespond с кодом состояния устройства собственные hello или описание.</span><span class="sxs-lookup"><span data-stu-id="836a5-143">Both `status` and `body` are provided by hello device and used toorespond with hello device's own status code and/or description.</span></span>

## <a name="handle-a-direct-method-on-a-device"></a><span data-ttu-id="836a5-144">Обработка прямого метода на устройстве</span><span class="sxs-lookup"><span data-stu-id="836a5-144">Handle a direct method on a device</span></span>
### <a name="method-invocation"></a><span data-ttu-id="836a5-145">Вызов метода</span><span class="sxs-lookup"><span data-stu-id="836a5-145">Method invocation</span></span>
<span data-ttu-id="836a5-146">Прямой метод запросов на разделе MQTT hello получение устройств:`$iothub/methods/POST/{method name}/?$rid={request id}`</span><span class="sxs-lookup"><span data-stu-id="836a5-146">Devices receive direct method requests on hello MQTT topic: `$iothub/methods/POST/{method name}/?$rid={request id}`</span></span>

<span data-ttu-id="836a5-147">текст Hello, какое устройство hello получает имеет hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="836a5-147">hello body which hello device receives is in hello following format:</span></span>

```
{
    "input1": "someInput",
    "input2": "anotherInput"
}
```

<span data-ttu-id="836a5-148">Запросы метода имеют нулевой уровень качества обслуживания.</span><span class="sxs-lookup"><span data-stu-id="836a5-148">Method requests are QoS 0.</span></span>

### <a name="response"></a><span data-ttu-id="836a5-149">Ответ</span><span class="sxs-lookup"><span data-stu-id="836a5-149">Response</span></span>
<span data-ttu-id="836a5-150">Hello устройство отправляет ответы слишком`$iothub/methods/res/{status}/?$rid={request id}`, где:</span><span class="sxs-lookup"><span data-stu-id="836a5-150">hello device sends responses too`$iothub/methods/res/{status}/?$rid={request id}`, where:</span></span>

* <span data-ttu-id="836a5-151">Hello `status` свойство — hello устройства указано состояние выполнения метода.</span><span class="sxs-lookup"><span data-stu-id="836a5-151">hello `status` property is hello device-supplied status of method execution.</span></span>
* <span data-ttu-id="836a5-152">Hello `$rid` свойство является идентификатор запроса hello из вызова метода hello, полученный от центра IoT.</span><span class="sxs-lookup"><span data-stu-id="836a5-152">hello `$rid` property is hello request ID from hello method invocation received from IoT Hub.</span></span>

<span data-ttu-id="836a5-153">текст Hello задается hello устройства и может быть любым состоянием.</span><span class="sxs-lookup"><span data-stu-id="836a5-153">hello body is set by hello device and can be any status.</span></span>

## <a name="additional-reference-material"></a><span data-ttu-id="836a5-154">Дополнительные справочные материалы</span><span class="sxs-lookup"><span data-stu-id="836a5-154">Additional reference material</span></span>
<span data-ttu-id="836a5-155">Другие разделы ссылку в hello центра IoT руководстве для разработчиков:</span><span class="sxs-lookup"><span data-stu-id="836a5-155">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="836a5-156">[Конечные точки центра IoT] [ lnk-endpoints] описывает hello различные конечные точки, предоставляемые каждый центр IoT для операций времени выполнения и управления.</span><span class="sxs-lookup"><span data-stu-id="836a5-156">[IoT Hub endpoints][lnk-endpoints] describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="836a5-157">[Регулирование и квоты] [ lnk-quotas] сведения о квотах hello, применять toohello службы центр IoT и hello регулирования tooexpect поведение при использовании службы hello.</span><span class="sxs-lookup"><span data-stu-id="836a5-157">[Throttling and quotas][lnk-quotas] describes hello quotas that apply toohello IoT Hub service and hello throttling behavior tooexpect when you use hello service.</span></span>
* <span data-ttu-id="836a5-158">[Пакеты SDK устройств и служб Azure IoT] [ lnk-sdks] списки hello языка различных пакетов SDK, которые можно использовать при разработке приложений, устройств и служб, которые взаимодействуют с центром IoT.</span><span class="sxs-lookup"><span data-stu-id="836a5-158">[Azure IoT device and service SDKs][lnk-sdks] lists hello various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="836a5-159">[Центр IoT язык запросов для близнецы устройства, задания и маршрутизация сообщений] [ lnk-query] описывает hello tooretrieve сведения из центра IoT близнецы устройства и заданий можно использовать язык запросов центра IoT.</span><span class="sxs-lookup"><span data-stu-id="836a5-159">[IoT Hub query language for device twins, jobs, and message routing][lnk-query] describes hello IoT Hub query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="836a5-160">[Поддержка MQTT концентратора IoT] [ lnk-devguide-mqtt] приведены более подробные сведения о поддержке центра IoT протокола MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="836a5-160">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="836a5-161">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="836a5-161">Next steps</span></span>
<span data-ttu-id="836a5-162">Теперь вы узнали, как toouse непосредственные методы, можно получить в разделе руководства разработчика центра IoT hello:</span><span class="sxs-lookup"><span data-stu-id="836a5-162">Now you have learned how toouse direct methods, you may be interested in hello following IoT Hub developer guide topic:</span></span>

* <span data-ttu-id="836a5-163">[Schedule jobs on multiple devices][lnk-devguide-jobs] (Планирование заданий на нескольких устройствах)</span><span class="sxs-lookup"><span data-stu-id="836a5-163">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="836a5-164">При желании tootry некоторые основные понятия hello, описанных в этой статье, могут быть интересны следующие учебника центра IoT hello параметры:</span><span class="sxs-lookup"><span data-stu-id="836a5-164">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorial:</span></span>

* <span data-ttu-id="836a5-165">[Use direct methods (Node)][lnk-methods-tutorial] (Использование прямых методов (Node))</span><span class="sxs-lookup"><span data-stu-id="836a5-165">[Use direct methods][lnk-methods-tutorial]</span></span>

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-devguide-messages]: iot-hub-devguide-messaging.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
