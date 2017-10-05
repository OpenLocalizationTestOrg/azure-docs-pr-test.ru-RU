---
title: "Пакет SDK для устройств Azure IoT для C — IoTHubClient | Документация Майкрософт"
description: "Узнайте, как использовать библиотеку IoTHubClient в пакете SDK для устройств Azure IoT для C и как создавать приложения для устройств, взаимодействующие с Центром Интернета вещей."
services: iot-hub
documentationcenter: 
author: olivierbloch
manager: timlt
editor: 
ms.assetid: 828cf2bf-999d-4b8a-8a28-c7c901629600
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/06/2016
ms.author: obloch
ms.openlocfilehash: 422d89014511f0d08ba57a893570ff7b253b7bc4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-iot-device-sdk-for-c--more-about-iothubclient"></a><span data-ttu-id="f8e5b-103">Пакет SDK для устройств Azure IoT для C — дополнительные сведения о библиотеке IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="f8e5b-103">Azure IoT device SDK for C – more about IoTHubClient</span></span>
<span data-ttu-id="f8e5b-104">В [первой статье](iot-hub-device-sdk-c-intro.md) этого курса вы познакомились с **пакетом SDK для устройств Azure IoT для C**. В ней объяснялось, что в пакете SDK есть два архитектурных уровня.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-104">The [first article](iot-hub-device-sdk-c-intro.md) in this series introduced the **Azure IoT device SDK for C**. That article explained that there are two architectural layers in SDK.</span></span> <span data-ttu-id="f8e5b-105">В основе лежит библиотека **IoTHubClient** , которая непосредственно управляет связью с центром IoT (IoT — «Интернет вещей»).</span><span class="sxs-lookup"><span data-stu-id="f8e5b-105">At the base is the **IoTHubClient** library which directly manages communication with IoT Hub.</span></span> <span data-ttu-id="f8e5b-106">На втором уровне находится библиотека **serializer** , которая реализована поверх упомянутой выше и предоставляет службы сериализации.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-106">There's also the **serializer** library that builds on top of that to provide serialization services.</span></span> <span data-ttu-id="f8e5b-107">В данной статье мы раскроем дополнительные подробности о библиотеке **IoTHubClient** .</span><span class="sxs-lookup"><span data-stu-id="f8e5b-107">In this article we'll provide additional detail on the **IoTHubClient** library.</span></span>

<span data-ttu-id="f8e5b-108">В предыдущей статье мы рассказали, как с помощью библиотеки **IoTHubClient** отправлять события в Центр Интернета вещей и получать из него сообщения.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-108">The previous article described how to use the **IoTHubClient** library to send events to IoT Hub and receive messages.</span></span> <span data-ttu-id="f8e5b-109">В данной статье продолжается обсуждение этой темы. Мы объясним, как можно с большей точностью управлять *временем* отправки и получения данных, используя **интерфейсы API нижнего уровня**.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-109">This article extends that discussion by explaining how to more precisely manage *when* you send and receive data, introducing you to the **lower-level APIs**.</span></span> <span data-ttu-id="f8e5b-110">Также мы объясним, как прикреплять свойства к событиям (и извлекать их из сообщений) с помощью функций обработки свойств в библиотеке **IoTHubClient**.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-110">We'll also explain how to attach properties to events (and retrieve them from messages) using the property handling features in the **IoTHubClient** library.</span></span> <span data-ttu-id="f8e5b-111">Кроме того, мы предоставим дополнительное описание различных способов обработки сообщений, полученных из центра IoT.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-111">Finally, we'll provide additional explanation of different ways to handle messages received from IoT Hub.</span></span>

<span data-ttu-id="f8e5b-112">В конце статьи будет раскрыто несколько других тем, в частности дополнительные сведения об учетных данных устройства и о том, как изменять поведение **IoTHubClient** через параметры конфигурации.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-112">The article concludes by covering a couple of miscellaneous topics, including more about device credentials and how to change the behavior of the **IoTHubClient** through configuration options.</span></span>

<span data-ttu-id="f8e5b-113">Чтобы раскрыть эти темы на должном уровне, мы будем использовать образцы из пакета SDK для библиотеки **IoTHubClient**.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-113">We'll use the **IoTHubClient** SDK samples to explain these topics.</span></span> <span data-ttu-id="f8e5b-114">Если вы хотите сразу же проверять все, о чем мы рассказываем, найдите приложения **iothub\_client\_sample\_http** и **iothub\_client\_sample\_amqp**. Они входят в пакет SDK для устройств Azure IoT для C. Все, что описано в следующих разделах, продемонстрировано именно в этих примерах.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-114">If you want to follow along, see the **iothub\_client\_sample\_http** and **iothub\_client\_sample\_amqp** applications that are included in the Azure IoT device SDK for C. Everything described in the following sections is demonstrated in these samples.</span></span>

<span data-ttu-id="f8e5b-115">[**Пакет SDK для устройств Интернета вещей Azure для C**](https://github.com/Azure/azure-iot-sdk-c) доступен в репозитории на сайте GitHub. Дополнительные сведения об API см. в [справочной документации по API для C](https://azure.github.io/azure-iot-sdk-c/index.html).</span><span class="sxs-lookup"><span data-stu-id="f8e5b-115">You can find the [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of the API in the [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

## <a name="the-lower-level-apis"></a><span data-ttu-id="f8e5b-116">Интерфейсы API нижнего уровня</span><span class="sxs-lookup"><span data-stu-id="f8e5b-116">The lower-level APIs</span></span>
<span data-ttu-id="f8e5b-117">В предыдущей статье были описаны основные операции библиотеки **IotHubClient** в контексте приложения **iothub\_client\_sample\_amqp**.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-117">The previous article described the basic operation of the **IotHubClient** within the context of the **iothub\_client\_sample\_amqp** application.</span></span> <span data-ttu-id="f8e5b-118">В частности, в ней объяснялось, как инициализировать библиотеку с помощью следующего кода.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-118">For example, it explained how to initialize the library using this code.</span></span>

```
IOTHUB_CLIENT_HANDLE iotHubClientHandle;
iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, AMQP_Protocol);
```

<span data-ttu-id="f8e5b-119">В ней также было описано, как отправлять события с помощью следующего вызова функции.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-119">It also described how to send events using this function call.</span></span>

```
IoTHubClient_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message);
```

<span data-ttu-id="f8e5b-120">Также в статье описано, как получать сообщения путем регистрации функции обратного вызова.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-120">The article also described how to receive messages by registering a callback function.</span></span>

```
int receiveContext = 0;
IoTHubClient_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext);
```

<span data-ttu-id="f8e5b-121">В статье также показано, как освободить ресурсы с помощью следующего кода.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-121">The article also showed how to free resources using code such as the following.</span></span>

```
IoTHubClient_Destroy(iotHubClientHandle);
```

<span data-ttu-id="f8e5b-122">Для каждого из этих интерфейсов API существуют сопутствующие функции:</span><span class="sxs-lookup"><span data-stu-id="f8e5b-122">However there are companion functions to each of these APIs:</span></span>

* <span data-ttu-id="f8e5b-123">IoTHubClient\_LL\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="f8e5b-123">IoTHubClient\_LL\_CreateFromConnectionString</span></span>
* <span data-ttu-id="f8e5b-124">IoTHubClient\_LL\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="f8e5b-124">IoTHubClient\_LL\_SendEventAsync</span></span>
* <span data-ttu-id="f8e5b-125">IoTHubClient\_LL\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="f8e5b-125">IoTHubClient\_LL\_SetMessageCallback</span></span>
* <span data-ttu-id="f8e5b-126">IoTHubClient\_LL\_Destroy</span><span class="sxs-lookup"><span data-stu-id="f8e5b-126">IoTHubClient\_LL\_Destroy</span></span>

<span data-ttu-id="f8e5b-127">В имени API всех этих функций содержатся символы LL (Lower Level — нижний уровень).</span><span class="sxs-lookup"><span data-stu-id="f8e5b-127">These functions all include “LL” in the API name.</span></span> <span data-ttu-id="f8e5b-128">За исключением этого, параметры каждой из этих функций идентичны их аналогам без символов LL.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-128">Other than that, the parameters of each of these functions are identical to their non-LL counterparts.</span></span> <span data-ttu-id="f8e5b-129">Однако в работе этих функций есть одна важная особенность.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-129">However, the behavior of these functions is different in one important way.</span></span>

<span data-ttu-id="f8e5b-130">При вызове **IoTHubClient\_CreateFromConnectionString** базовые библиотеки создают новый поток, выполняемый в фоновом режиме.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-130">When you call **IoTHubClient\_CreateFromConnectionString**, the underlying libraries create a new thread that runs in the background.</span></span> <span data-ttu-id="f8e5b-131">Этот поток отправляет события в центр IoT и принимает сообщения из него.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-131">This thread sends events to, and receives messages from, IoT Hub.</span></span> <span data-ttu-id="f8e5b-132">При работе с интерфейсами API нижнего уровня (LL) такой поток не создается.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-132">No such thread is created when working with the "LL" APIs.</span></span> <span data-ttu-id="f8e5b-133">Создание фонового потока — это удобный инструмент для разработчиков.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-133">The creation of the background thread is a convenience to the developer.</span></span> <span data-ttu-id="f8e5b-134">Вам не нужно беспокоиться о явной отправке событий и получении сообщений из центра IoT — это происходит автоматически в фоновом режиме.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-134">You don’t have to worry about explicitly sending events and receiving messages from IoT Hub -- it happens automatically in the background.</span></span> <span data-ttu-id="f8e5b-135">Напротив, интерфейсы API нижнего уровня (LL) позволяют контролировать обмен данными с центром IoT, если это необходимо.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-135">In contrast, the "LL" APIs give you explicit control over communication with IoT Hub, if you need it.</span></span>

<span data-ttu-id="f8e5b-136">Чтобы лучше понять это, рассмотрим пример.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-136">To understand this better, let’s look at an example:</span></span>

<span data-ttu-id="f8e5b-137">При вызове **IoTHubClient\_SendEventAsync** вы фактически помещаете событие в буфер.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-137">When you call **IoTHubClient\_SendEventAsync**, what you're actually doing is putting the event in a buffer.</span></span> <span data-ttu-id="f8e5b-138">Фоновый поток, созданный при вызове **IoTHubClient\_CreateFromConnectionString**, постоянно отслеживает этот буфер и отправляет любые содержащиеся в нем данные в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-138">The background thread created when you call **IoTHubClient\_CreateFromConnectionString** continually monitors this buffer and sends any data that it contains to IoT Hub.</span></span> <span data-ttu-id="f8e5b-139">Это происходит в фоновом режиме в то же время, когда основной поток выполняет другую работу.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-139">This happens in the background at the same time that the main thread is performing other work.</span></span>

<span data-ttu-id="f8e5b-140">Аналогичным образом, когда вы регистрируете функцию обратного вызова для сообщений с помощью **IoTHubClient\_SetMessageCallback**, вы указываете пакету SDK, что фоновый поток должен вызвать функцию обратного вызова, когда будет получено сообщение, независимо от того, что в это время будет делать основной поток.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-140">Similarly, when you register a callback function for messages using **IoTHubClient\_SetMessageCallback**, you're instructing the SDK to have the background thread invoke the callback function when a message is received, independent of the main thread.</span></span>

<span data-ttu-id="f8e5b-141">Интерфейсы API нижнего уровня не создают фоновый поток.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-141">The "LL" APIs don’t create a background thread.</span></span> <span data-ttu-id="f8e5b-142">Вместо этого для явной отправки и получения данных из центра IoT необходимо вызывать новый интерфейс API.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-142">Instead, a new API must be called to explicitly send and receive data from IoT Hub.</span></span> <span data-ttu-id="f8e5b-143">Это продемонстрировано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-143">This is demonstrated in the following example.</span></span>

<span data-ttu-id="f8e5b-144">Приложение **iothub\_client\_sample\_http**, включенное в пакет SDK, демонстрирует интерфейсы API нижнего уровня.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-144">The **iothub\_client\_sample\_http** application that’s included in the SDK demonstrates the lower-level APIs.</span></span> <span data-ttu-id="f8e5b-145">В этом примере мы отправляем события в центр IoT с помощью кода, аналогичного приведенному ниже.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-145">In that sample, we send events to IoT Hub with code such as the following:</span></span>

```
EVENT_INSTANCE message;
sprintf_s(msgText, sizeof(msgText), "Message_%d_From_IoTHubClient_LL_Over_HTTP", i);
message.messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText));

IoTHubClient_LL_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message)
```

<span data-ttu-id="f8e5b-146">Первые три строки создают сообщение, а последняя строка отправляет событие.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-146">The first three lines create the message, and the last line sends the event.</span></span> <span data-ttu-id="f8e5b-147">Тем не менее, как было сказано ранее, "отправка" события означает, что данные просто помещаются в буфер.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-147">However, as mentioned previously, "sending" the event means that the data is simply placed in a buffer.</span></span> <span data-ttu-id="f8e5b-148">При вызове **IoTHubClient\_LL\_SendEventAsync** ничего не передается по сети.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-148">Nothing is transmitted on the network when we call **IoTHubClient\_LL\_SendEventAsync**.</span></span> <span data-ttu-id="f8e5b-149">Чтобы фактически передать данные в Центр Интернета вещей, необходимо вызвать **IoTHubClient\_LL\_DoWork**, как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="f8e5b-149">In order to actually ingress the data to IoT Hub, you must call **IoTHubClient\_LL\_DoWork**, as in this example:</span></span>

```
while (1)
{
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1000);
}
```

<span data-ttu-id="f8e5b-150">Этот код (из приложения **iothub\_client\_sample\_http**) многократно вызывает функцию **IoTHubClient\_LL\_DoWork**.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-150">This code (from the **iothub\_client\_sample\_http** application) repeatedly calls **IoTHubClient\_LL\_DoWork**.</span></span> <span data-ttu-id="f8e5b-151">При каждом вызове функции **IoTHubClient\_LL\_DoWork** она отправляет некоторые события из буфера в Центр Интернета вещей и получает сообщение из очереди, отправляемое на устройство.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-151">Each time **IoTHubClient\_LL\_DoWork** is called, it sends some events from the buffer to IoT Hub and it retrieves a queued message being sent to the device.</span></span> <span data-ttu-id="f8e5b-152">В последнем случае это означает, что если мы зарегистрировали функцию обратного вызова для сообщений, то выполняется обратный вызов (предполагается, что в очереди есть сообщения).</span><span class="sxs-lookup"><span data-stu-id="f8e5b-152">The latter case means that if we registered a callback function for messages, then the callback is invoked (assuming any messages are queued up).</span></span> <span data-ttu-id="f8e5b-153">Такую функцию обратного вызова мы зарегистрируем с помощью следующего кода:</span><span class="sxs-lookup"><span data-stu-id="f8e5b-153">We would have registered such a callback function with code such as the following:</span></span>

```
IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext)
```

<span data-ttu-id="f8e5b-154">Причина частого циклического вызова **IoTHubClient\_LL\_DoWork** в том, что при каждом вызове этой функции она отправляет *некоторые* буферизованные события в Центр Интернета вещей и извлекает *следующее* сообщение из очереди для устройства.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-154">The reason that **IoTHubClient\_LL\_DoWork** is often called in a loop is that each time it’s called, it sends *some* buffered events to IoT Hub and retrieves *the next* message queued up for the device.</span></span> <span data-ttu-id="f8e5b-155">Отправка всех буферизованных событий каждым вызовом или получение всех сообщений из очереди не гарантируется.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-155">Each call isn’t guaranteed to send all buffered events or to retrieve all queued messages.</span></span> <span data-ttu-id="f8e5b-156">Если вам нужно отправить все события из буфера, а затем заняться другой обработкой, замените этот цикл следующим кодом.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-156">If you want to send all events in the buffer and then continue on with other processing you can replace this loop with code such as the following:</span></span>

```
IOTHUB_CLIENT_STATUS status;

while ((IoTHubClient_LL_GetSendStatus(iotHubClientHandle, &status) == IOTHUB_CLIENT_OK) && (status == IOTHUB_CLIENT_SEND_STATUS_BUSY))
{
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1000);
}
```

<span data-ttu-id="f8e5b-157">Этот код вызывает **IoTHubClient\_LL\_DoWork** до тех пор, пока все события из буфера не будут отправлены в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-157">This code calls **IoTHubClient\_LL\_DoWork** until all events in the buffer have been sent to IoT Hub.</span></span> <span data-ttu-id="f8e5b-158">Обратите внимание, что это не означает, что все сообщения из очереди получены.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-158">Note this does not also imply that all queued messages have been received.</span></span> <span data-ttu-id="f8e5b-159">Отчасти это объясняется тем, что проверка «всех» сообщений не является настолько детерминированным действием.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-159">Part of the reason for this is that checking for "all" messages isn’t as deterministic an action.</span></span> <span data-ttu-id="f8e5b-160">Что происходит при извлечении «всех» сообщений и отправке другого сообщения на устройство непосредственно после этого?</span><span class="sxs-lookup"><span data-stu-id="f8e5b-160">What happens if you retrieve "all" of the messages, but then another one is sent to the device immediately after?</span></span> <span data-ttu-id="f8e5b-161">Лучше такие моменты решать через запрограммированное время ожидания.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-161">A better way to deal with that is with a programmed timeout.</span></span> <span data-ttu-id="f8e5b-162">Например, функция обратного вызова сообщений может сбрасывать таймер при каждом вызове.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-162">For example, the message callback function could reset a timer every time it’s invoked.</span></span> <span data-ttu-id="f8e5b-163">Затем можно написать логику для продолжения обработки, если, например, ни одно сообщение не было получено за последние *X* секунд.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-163">You can then write logic to continue processing if, for example, no messages have been received in the last *X* seconds.</span></span>

<span data-ttu-id="f8e5b-164">После завершения передачи событий и получения сообщений не забудьте вызвать функцию для очистки ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-164">When you’re finished ingressing events and receiving messages, be sure to call the corresponding function to clean up resources.</span></span>

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

<span data-ttu-id="f8e5b-165">По сути существует только один набор интерфейсов API для отправки и получения данных в фоновом потоке и другой набор интерфейсов API, который делает то же самое без фонового потока.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-165">Basically there’s only one set of APIs to send and receive data with a background thread and another set of APIs that does the same thing without the background thread.</span></span> <span data-ttu-id="f8e5b-166">Многие разработчики предпочитают интерфейсы API, не относящие к нижнему уровню. Тем не менее, API нижнего уровня полезны, когда разработчику нужно контролировать передачу данных по сети.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-166">A lot of developers may prefer the non-LL APIs, but the lower-level APIs are useful when the developer wants explicit control over network transmissions.</span></span> <span data-ttu-id="f8e5b-167">Например, некоторые устройства собирают данные в течение продолжительного периода и передают события только через заданные интервалы времени (скажем, раз в час или раз в день).</span><span class="sxs-lookup"><span data-stu-id="f8e5b-167">For example, some devices collect data over time and only ingress events at specified intervals (for example, once an hour or once a day).</span></span> <span data-ttu-id="f8e5b-168">Интерфейсы API нижнего уровня позволяют вам четко контролировать, когда будут отправляться и приниматься данные из центра IoT.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-168">The lower-level APIs give you the ability to explicitly control when you send and receive data from IoT Hub.</span></span> <span data-ttu-id="f8e5b-169">Другие разработчики отдадут предпочтение простоте интерфейсов API нижнего уровня.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-169">Others will simply prefer the simplicity that the lower-level APIs provide.</span></span> <span data-ttu-id="f8e5b-170">Все действия происходят в основном потоке, а не в фоновом режиме.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-170">Everything happens on the main thread rather than some work happening in the background.</span></span>

<span data-ttu-id="f8e5b-171">Выбрав ту или иную модель, обязательно используйте соответствующие интерфейсы API.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-171">Whichever model you choose, be sure to be consistent in which APIs you use.</span></span> <span data-ttu-id="f8e5b-172">Если вы начнете с вызова **IoTHubClient\_LL\_CreateFromConnectionString**, то в последующей работе используйте только соответствующие интерфейсы API нижнего уровня:</span><span class="sxs-lookup"><span data-stu-id="f8e5b-172">If you start by calling **IoTHubClient\_LL\_CreateFromConnectionString**, be sure you only use the corresponding lower-level APIs for any follow-up work:</span></span>

* <span data-ttu-id="f8e5b-173">IoTHubClient\_LL\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="f8e5b-173">IoTHubClient\_LL\_SendEventAsync</span></span>
* <span data-ttu-id="f8e5b-174">IoTHubClient\_LL\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="f8e5b-174">IoTHubClient\_LL\_SetMessageCallback</span></span>
* <span data-ttu-id="f8e5b-175">IoTHubClient\_LL\_Destroy</span><span class="sxs-lookup"><span data-stu-id="f8e5b-175">IoTHubClient\_LL\_Destroy</span></span>
* <span data-ttu-id="f8e5b-176">IoTHubClient\_LL\_DoWork</span><span class="sxs-lookup"><span data-stu-id="f8e5b-176">IoTHubClient\_LL\_DoWork</span></span>

<span data-ttu-id="f8e5b-177">И наоборот,</span><span class="sxs-lookup"><span data-stu-id="f8e5b-177">The opposite is true as well.</span></span> <span data-ttu-id="f8e5b-178">если вы начали с **IoTHubClient\_CreateFromConnectionString**, то для любой дополнительной обработки используйте интерфейсы API, не относящиеся к нижнему уровню.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-178">If you start with **IoTHubClient\_CreateFromConnectionString**, then use the non-LL APIs for any additional processing.</span></span>

<span data-ttu-id="f8e5b-179">В пакете SDK для устройств Azure IoT для C найдите приложение **iothub\_client\_sample\_http**, в котором содержится полный пример использования интерфейсов API нижнего уровня.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-179">In the Azure IoT device SDK for C, see the **iothub\_client\_sample\_http** application for a complete example of the lower-level APIs.</span></span> <span data-ttu-id="f8e5b-180">Приложение **iothub\_client\_sample\_amqp** служит полным примером использования интерфейсов API, не относящихся к нижнему уровню.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-180">The **iothub\_client\_sample\_amqp** application can be referenced for a full example of the non-LL APIs.</span></span>

## <a name="property-handling"></a><span data-ttu-id="f8e5b-181">Обработка свойств</span><span class="sxs-lookup"><span data-stu-id="f8e5b-181">Property handling</span></span>
<span data-ttu-id="f8e5b-182">До сих пор для описания отправки данных мы использовали текст сообщения.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-182">So far when we've described sending data, we've been referring to the body of the message.</span></span> <span data-ttu-id="f8e5b-183">Рассмотрим для примера такой код:</span><span class="sxs-lookup"><span data-stu-id="f8e5b-183">For example, consider this code:</span></span>

```
EVENT_INSTANCE message;
sprintf_s(msgText, sizeof(msgText), "Hello World");
message.messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText));
IoTHubClient_LL_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message)
```

<span data-ttu-id="f8e5b-184">Этот код отправляет в центр IoT сообщение с текстом "Hello World".</span><span class="sxs-lookup"><span data-stu-id="f8e5b-184">This example sends a message to IoT Hub with the text "Hello World."</span></span> <span data-ttu-id="f8e5b-185">Но центр IoT также позволяет к каждому сообщению прикреплять свойства.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-185">However, IoT Hub also allows properties to be attached to each message.</span></span> <span data-ttu-id="f8e5b-186">Свойства — это пары "имя-значение", которые можно присоединять к сообщению.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-186">Properties are name/value pairs that can be attached to the message.</span></span> <span data-ttu-id="f8e5b-187">Например, мы можем прикрепить свойство к сообщению, изменив приведенный выше код.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-187">For example, we can modify the previous code to attach a property to the message:</span></span>

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

<span data-ttu-id="f8e5b-188">Сначала мы вызываем функцию **IoTHubMessage\_Properties** и передаем ей дескриптор сообщения.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-188">We start by calling **IoTHubMessage\_Properties** and passing it the handle of our message.</span></span> <span data-ttu-id="f8e5b-189">Обратно мы получаем ссылку **MAP\_HANDLE**, которая позволяет добавлять свойства.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-189">What we get back is a **MAP\_HANDLE** reference that enables us to start adding properties.</span></span> <span data-ttu-id="f8e5b-190">Для добавления свойств мы вызываем метод **Map\_AddOrUpdate**, который принимает ссылку на MAP\_HANDLE, имя свойства и значение свойства.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-190">The latter is accomplished by calling **Map\_AddOrUpdate**, which takes a reference to a MAP\_HANDLE, the property name, and the property value.</span></span> <span data-ttu-id="f8e5b-191">С помощью этого API мы можем добавить сколько угодно свойств.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-191">With this API we can add as many properties as we like.</span></span>

<span data-ttu-id="f8e5b-192">Когда событие считывается из **концентраторов событий**, получатель может перечислить свойства и извлечь их соответствующие значения.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-192">When the event is read from **Event Hubs**, the receiver can enumerate the properties and retrieve their corresponding values.</span></span> <span data-ttu-id="f8e5b-193">Например, в среде .NET это можно реализовать путем обращения к [коллекции свойств в объекте EventData](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.eventdata.properties.aspx).</span><span class="sxs-lookup"><span data-stu-id="f8e5b-193">For example, in .NET this would be accomplished by accessing the [Properties collection on the EventData object](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.eventdata.properties.aspx).</span></span>

<span data-ttu-id="f8e5b-194">В предыдущем примере мы прикрепляем свойства к событию, которое отправляем в центр IoT.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-194">In the previous example, we’re attaching properties to an event that we send to IoT Hub.</span></span> <span data-ttu-id="f8e5b-195">Свойства можно также прикреплять к сообщениям, получаемым из центра IoT.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-195">Properties can also be attached to messages received from IoT Hub.</span></span> <span data-ttu-id="f8e5b-196">Чтобы извлечь свойства из сообщения, в функции обратного вызова сообщения используйте код, подобный указанному ниже.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-196">If we want to retrieve properties from a message, we can use code such as the following in our message callback function:</span></span>

```
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    . . .

    // Retrieve properties from the message
    MAP_HANDLE mapProperties = IoTHubMessage_Properties(message);
    if (mapProperties != NULL)
    {
        const char*const* keys;
        const char*const* values;
        size_t propertyCount = 0;
        if (Map_GetInternals(mapProperties, &keys, &values, &propertyCount) == MAP_OK)
        {
            if (propertyCount > 0)
            {
                printf("Message Properties:\r\n");
                for (size_t index = 0; index < propertyCount; index++)
                {
                    printf("\tKey: %s Value: %s\r\n", keys[index], values[index]);
                }
                printf("\r\n");
            }
        }
    }

    . . .
}
```

<span data-ttu-id="f8e5b-197">Вызов **IoTHubMessage\_Properties** возвращает ссылку **MAP\_HANDLE**,</span><span class="sxs-lookup"><span data-stu-id="f8e5b-197">The call to **IoTHubMessage\_Properties** returns the **MAP\_HANDLE** reference.</span></span> <span data-ttu-id="f8e5b-198">которую мы передаем в метод **Map\_GetInternals**, чтобы получить ссылку на массив пар "имя-значение" (и количество свойств).</span><span class="sxs-lookup"><span data-stu-id="f8e5b-198">We then pass that reference to **Map\_GetInternals** to obtain a reference to an array of the name/value pairs (as well as a count of the properties).</span></span> <span data-ttu-id="f8e5b-199">На этом этапе для получения нужных значений достаточно просто перебрать свойства.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-199">At that point it's a simple matter of enumerating the properties to get to the values we want.</span></span>

<span data-ttu-id="f8e5b-200">Использовать свойства в приложении не обязательно,</span><span class="sxs-lookup"><span data-stu-id="f8e5b-200">You don't have to use properties in your application.</span></span> <span data-ttu-id="f8e5b-201">но если вам нужно указывать их для событий или получать из сообщений, с библиотекой **IoTHubClient** сделать это будет просто.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-201">However, if you need to set them on events or retrieve them from messages, the **IoTHubClient** library makes it easy.</span></span>

## <a name="message-handling"></a><span data-ttu-id="f8e5b-202">Обработка сообщений</span><span class="sxs-lookup"><span data-stu-id="f8e5b-202">Message handling</span></span>
<span data-ttu-id="f8e5b-203">Как упоминалось ранее, когда сообщения поступают из центра IoT, библиотека **IoTHubClient** отвечает вызовом зарегистрированной функции обратного вызова.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-203">As stated previously, when messages arrive from IoT Hub the **IoTHubClient** library responds by invoking a registered callback function.</span></span> <span data-ttu-id="f8e5b-204">У этой функции есть параметр возврата, который требует дополнительного пояснения.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-204">There is a return parameter of this function that deserves some additional explanation.</span></span> <span data-ttu-id="f8e5b-205">Вот фрагмент функции обратного вызова из приложения **iothub\_client\_sample\_http**:</span><span class="sxs-lookup"><span data-stu-id="f8e5b-205">Here’s an excerpt of the callback function in the **iothub\_client\_sample\_http** sample application:</span></span>

```
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    . . .
    return IOTHUBMESSAGE_ACCEPTED;
}
```

<span data-ttu-id="f8e5b-206">Обратите внимание, что тип возврата — **IOTHUBMESSAGE\_DISPOSITION\_RESULT**, а в данном случае мы возвращаем **IOTHUBMESSAGE\_ACCEPTED**.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-206">Note that the return type is **IOTHUBMESSAGE\_DISPOSITION\_RESULT** and in this particular case we return **IOTHUBMESSAGE\_ACCEPTED**.</span></span> <span data-ttu-id="f8e5b-207">Из этой функции мы можем возвращать другие значения, которые изменяют способ реакции библиотеки **IoTHubClient** на обратный вызов сообщения.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-207">There are other values we can return from this function that change how the **IoTHubClient** library reacts to the message callback.</span></span> <span data-ttu-id="f8e5b-208">Вот эти другие значения:</span><span class="sxs-lookup"><span data-stu-id="f8e5b-208">Here are the options.</span></span>

* <span data-ttu-id="f8e5b-209">**IOTHUBMESSAGE\_ACCEPTED** — сообщение успешно обработано.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-209">**IOTHUBMESSAGE\_ACCEPTED** – The message has been processed successfully.</span></span> <span data-ttu-id="f8e5b-210">Библиотека **IoTHubClient** не будет вызывать функцию обратного вызова еще раз для того же сообщения.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-210">The **IoTHubClient** library will not invoke the callback function again with the same message.</span></span>
* <span data-ttu-id="f8e5b-211">**IOTHUBMESSAGE\_REJECTED** — сообщение не обработано и обрабатываться не будет.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-211">**IOTHUBMESSAGE\_REJECTED** – The message was not processed and there is no desire to do so in the future.</span></span> <span data-ttu-id="f8e5b-212">Библиотеке **IoTHubClient** не нужно вызывать функцию обратного вызова еще раз для того же сообщения.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-212">The **IoTHubClient** library should not invoke the callback function again with the same message.</span></span>
* <span data-ttu-id="f8e5b-213">**IOTHUBMESSAGE\_ABANDONED** — сообщение не было обработано успешно, но библиотека **IoTHubClient** должна вызвать функцию обратного вызова еще раз для того же сообщения.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-213">**IOTHUBMESSAGE\_ABANDONED** – The message was not processed successfully, but the **IoTHubClient** library should invoke the callback function again with the same message.</span></span>

<span data-ttu-id="f8e5b-214">Для первых двух кодов возврата библиотека **IoTHubClient** отправляет сообщение в центр IoT, указывая, что сообщение следует удалить из очереди устройства и не доставлять повторно.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-214">For the first two return codes, the **IoTHubClient** library sends a message to IoT Hub indicating that the message should be deleted from the device queue and not delivered again.</span></span> <span data-ttu-id="f8e5b-215">Совокупный эффект оказывается таким же (сообщение удаляется из очереди устройства), но все так же делается запись о том, было ли сообщение принято или отклонено.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-215">The net effect is the same (the message is deleted from the device queue), but whether the message was accepted or rejected is still recorded.</span></span>  <span data-ttu-id="f8e5b-216">Такая запись полезна для отправителей сообщения, которые принимают обратную связь, чтобы выяснить, приняло ли устройство определенное сообщение или отклонило.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-216">Recording this distinction is useful to senders of the message who can listen for feedback and find out if a device has accepted or rejected a particular message.</span></span>

<span data-ttu-id="f8e5b-217">Если сообщение отклонено, оно также отправляется в центр IoT, но при этом указывается, что сообщение следует доставить повторно.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-217">In the last case a message is also sent to IoT Hub, but it indicates that the message should be redelivered.</span></span> <span data-ttu-id="f8e5b-218">Обычно отказ от сообщения выполняется тогда, когда возникла какая-то ошибка, но при этом то же сообщение нужно попытаться обработать снова.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-218">Typically you’ll abandon a message if you encounter some error but want to try to process the message again.</span></span> <span data-ttu-id="f8e5b-219">С другой стороны, отклонение сообщения уместно при возникновении неустранимой ошибки (или если вы просто определили, что это сообщение не нужно обрабатывать).</span><span class="sxs-lookup"><span data-stu-id="f8e5b-219">In contrast, rejecting a message is appropriate when you encounter an unrecoverable error (or if you simply decide you don’t want to process the message).</span></span>

<span data-ttu-id="f8e5b-220">В любом случае помните о различных кодах возврата, позволяющих обеспечить требуемое поведение библиотеки **IoTHubClient** .</span><span class="sxs-lookup"><span data-stu-id="f8e5b-220">In any case, be aware of the different return codes so that you can elicit the behavior you want from the **IoTHubClient** library.</span></span>

## <a name="alternate-device-credentials"></a><span data-ttu-id="f8e5b-221">Альтернативные учетные данные устройств</span><span class="sxs-lookup"><span data-stu-id="f8e5b-221">Alternate device credentials</span></span>
<span data-ttu-id="f8e5b-222">Как отмечалось ранее, первое, что необходимо сделать при работе с библиотекой **IoTHubClient**, — получить дескриптор **IOTHUB\_CLIENT\_HANDLE** с помощью такого вызова:</span><span class="sxs-lookup"><span data-stu-id="f8e5b-222">As explained previously, the first thing to do when working with the **IoTHubClient** library is to obtain a **IOTHUB\_CLIENT\_HANDLE** with a call such as the following:</span></span>

```
IOTHUB_CLIENT_HANDLE iotHubClientHandle;
iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, AMQP_Protocol);
```

<span data-ttu-id="f8e5b-223">Аргументами **IoTHubClient\_CreateFromConnectionString** выступают строка подключения устройства и параметр, указывающий протокол, который используется для связи с Центром Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-223">The arguments to **IoTHubClient\_CreateFromConnectionString** are the device connection string and a parameter that indicates the protocol we use to communicate with IoT Hub.</span></span> <span data-ttu-id="f8e5b-224">Строка подключения для устройства имеет следующий формат.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-224">The device connection string has a format that appears as follows:</span></span>

```
HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY
```

<span data-ttu-id="f8e5b-225">В этой строке указаны четыре значения: имя центра IoT, суффикс центра IoT, идентификатор устройства и ключ общего доступа.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-225">There are four pieces of information in this string: IoT Hub name, IoT Hub suffix, device ID, and shared access key.</span></span> <span data-ttu-id="f8e5b-226">При создании экземпляра центра IoT на портале Azure вы получаете полное доменное имя (FQDN) центра IoT. Из этого имени мы получаем имя центра IoT (первая часть FQDN) и суффикс центра IoT (остальная часть FQDN).</span><span class="sxs-lookup"><span data-stu-id="f8e5b-226">You obtain the fully qualified domain name (FQDN) of an IoT hub when you create your IoT hub instance in the Azure portal — this gives you the IoT hub name (the first part of the FQDN) and the IoT hub suffix (the rest of the FQDN).</span></span> <span data-ttu-id="f8e5b-227">Идентификатор устройства и общий ключ доступа получаются при регистрации устройства в Центре Интернета вещей (см. [предыдущую статью](iot-hub-device-sdk-c-intro.md)).</span><span class="sxs-lookup"><span data-stu-id="f8e5b-227">You get the device ID and the shared access key when you register your device with IoT Hub (as described in the [previous article](iot-hub-device-sdk-c-intro.md)).</span></span>

<span data-ttu-id="f8e5b-228">**IoTHubClient\_CreateFromConnectionString** — это всего лишь один из способов инициализации библиотеки.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-228">**IoTHubClient\_CreateFromConnectionString** gives you one way to initialize the library.</span></span> <span data-ttu-id="f8e5b-229">При желании вы можете создать дескриптор **IOTHUB\_CLIENT\_HANDLE**, используя вместо строки подключения устройства отдельные параметры.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-229">If you prefer, you can create a new **IOTHUB\_CLIENT\_HANDLE** by using these individual parameters rather than the device connection string.</span></span> <span data-ttu-id="f8e5b-230">Для этого используется такой код:</span><span class="sxs-lookup"><span data-stu-id="f8e5b-230">This is achieved with the following code:</span></span>

```
IOTHUB_CLIENT_CONFIG iotHubClientConfig;
iotHubClientConfig.iotHubName = "";
iotHubClientConfig.deviceId = "";
iotHubClientConfig.deviceKey = "";
iotHubClientConfig.iotHubSuffix = "";
iotHubClientConfig.protocol = HTTP_Protocol;
IOTHUB_CLIENT_HANDLE iotHubClientHandle = IoTHubClient_LL_Create(&iotHubClientConfig);
```

<span data-ttu-id="f8e5b-231">Этот код выполняет то же самое, что и **IoTHubClient\_CreateFromConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-231">This accomplishes the same thing as **IoTHubClient\_CreateFromConnectionString**.</span></span>

<span data-ttu-id="f8e5b-232">Вы, вероятно, решите, что использовать **IoTHubClient\_CreateFromConnectionString** удобнее, чем такой подробный метод инициализации.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-232">It may seem obvious that you would want to use **IoTHubClient\_CreateFromConnectionString** rather than this more verbose method of initialization.</span></span> <span data-ttu-id="f8e5b-233">Но не стоит забывать, что при регистрации устройства в центре IoT вы получаете только идентификатор и ключ устройства (а не строку подключения).</span><span class="sxs-lookup"><span data-stu-id="f8e5b-233">Keep in mind, however, that when you register a device in IoT Hub what you get is a device ID and device key (not a connection string).</span></span> <span data-ttu-id="f8e5b-234">Пакет SDK для *обозревателя устройств*, который мы упоминали в [предыдущей статье](iot-hub-device-sdk-c-intro.md), создает строку подключения устройства на основе идентификатора и ключа устройства, а также имени узла Центра Интернета вещей с помощью библиотек из **пакета SDK для служб Azure IoT**.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-234">The *device explorer* SDK tool introduced in the [previous article](iot-hub-device-sdk-c-intro.md) uses libraries in the **Azure IoT service SDK** to create the device connection string from the device ID, device key, and IoT Hub host name.</span></span> <span data-ttu-id="f8e5b-235">Поэтому метод с вызовом **IoTHubClient\_LL\_Create** может быть предпочтительнее, так как он позволяет исключить этап создания строки подключения.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-235">So calling **IoTHubClient\_LL\_Create** may be preferable because it saves you the step of generating a connection string.</span></span> <span data-ttu-id="f8e5b-236">Используйте тот метод, который для вас удобнее.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-236">Use whichever method is convenient.</span></span>

## <a name="configuration-options"></a><span data-ttu-id="f8e5b-237">Варианты настройки</span><span class="sxs-lookup"><span data-stu-id="f8e5b-237">Configuration options</span></span>
<span data-ttu-id="f8e5b-238">До сих пор все описываемые способы работы библиотеки **IoTHubClient** отражали ее стандартное поведение.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-238">So far everything described about the way the **IoTHubClient** library works reflects its default behavior.</span></span> <span data-ttu-id="f8e5b-239">Однако существует несколько параметров, позволяющих изменить то, как работает библиотека.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-239">However, there are a few options that you can set to change how the library works.</span></span> <span data-ttu-id="f8e5b-240">Для этого используется API **IoTHubClient\_LL\_SetOption**.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-240">This is accomplished by leveraging the **IoTHubClient\_LL\_SetOption** API.</span></span> <span data-ttu-id="f8e5b-241">Рассмотрим следующий пример.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-241">Consider this example:</span></span>

```
unsigned int timeout = 30000;
IoTHubClient_LL_SetOption(iotHubClientHandle, "timeout", &timeout);
```

<span data-ttu-id="f8e5b-242">Существует несколько часто используемых параметров:</span><span class="sxs-lookup"><span data-stu-id="f8e5b-242">There are a couple of options that are commonly used:</span></span>

* <span data-ttu-id="f8e5b-243">**SetBatching** (логическое значение). Если значение равно **true**, то данные, отправляемые в Центр Интернета вещей, передаются пакетами.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-243">**SetBatching** (bool) – If **true**, then data sent to IoT Hub is sent in batches.</span></span> <span data-ttu-id="f8e5b-244">При значении **false** сообщения отправляются по отдельности.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-244">If **false**, then messages are sent individually.</span></span> <span data-ttu-id="f8e5b-245">Значение по умолчанию — **false**.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-245">The default is **false**.</span></span> <span data-ttu-id="f8e5b-246">Обратите внимание, что параметр **SetBatching** применяется только для протокола HTTP, а не для протоколов MQTT и AMQP.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-246">Note that the **SetBatching** option only applies to the HTTP protocol and not to the MQTT or AMQP protocols.</span></span>
* <span data-ttu-id="f8e5b-247">**Timeout** (целое число без знака). Это значение указывается в миллисекундах.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-247">**Timeout** (unsigned int) – This value is represented in milliseconds.</span></span> <span data-ttu-id="f8e5b-248">Если отправка HTTP-запроса или прием ответа выполняется дольше этого времени, время ожидания соединения заканчивается.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-248">If sending an HTTP request or receiving a response takes longer than this time, then the connection times out.</span></span>

<span data-ttu-id="f8e5b-249">Параметр пакетной обработки является важным параметром.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-249">The batching option is important.</span></span> <span data-ttu-id="f8e5b-250">По умолчанию библиотека передает события по отдельности (одно событие — это то, что вы передаете в **IoTHubClient\_LL\_SendEventAsync**).</span><span class="sxs-lookup"><span data-stu-id="f8e5b-250">By default, the library ingresses events individually (a single event is whatever you pass to **IoTHubClient\_LL\_SendEventAsync**).</span></span> <span data-ttu-id="f8e5b-251">Если параметр пакетной обработки имеет значение **true**, библиотека собирает из буфера максимально возможное количество событий (вплоть до максимального размера сообщения, который принимается центром IoT).</span><span class="sxs-lookup"><span data-stu-id="f8e5b-251">If the batching option is **true**, the library collects as many events as it can from the buffer (up to the maximum message size that IoT Hub will accept).</span></span>  <span data-ttu-id="f8e5b-252">Пакет событий отправляется в центр IoT за один вызов HTTP (отдельные события объединяются в массив JSON).</span><span class="sxs-lookup"><span data-stu-id="f8e5b-252">The event batch is sent to IoT Hub in a single HTTP call (the individual events are bundled into a JSON array).</span></span> <span data-ttu-id="f8e5b-253">Включение пакетной обработки обычно позволяет существенно увеличить производительность, так как уменьшается число сетевых круговых путей.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-253">Enabling batching typically results in big performance gains since you’re reducing network round-trips.</span></span> <span data-ttu-id="f8e5b-254">При этом также существенно экономится пропускная способность, так как вы отправляете с пакетом событий только один набор заголовков HTTP, а не набор заголовков для каждого отдельного события.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-254">It also significantly reduces bandwidth since you are sending one set of HTTP headers with an event batch rather than a set of headers for each individual event.</span></span> <span data-ttu-id="f8e5b-255">Мы рекомендуем включать пакетную обработку при условии, что у вас нет веских причин поступать иначе.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-255">Unless you have a specific reason to do otherwise, typically you’ll want to enable batching.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8e5b-256">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f8e5b-256">Next steps</span></span>
<span data-ttu-id="f8e5b-257">В этой статье подробно описывается работа библиотеки **IoTHubClient**, содержащейся в **пакете SDK для устройств Azure IoT для C**. Эти сведения позволят вам хорошо изучить возможности библиотеки **IoTHubClient**.</span><span class="sxs-lookup"><span data-stu-id="f8e5b-257">This article describes in detail the behavior of the **IoTHubClient** library found in the **Azure IoT device SDK for C**. With this information, you should have a good understanding of the capabilities of the **IoTHubClient** library.</span></span> <span data-ttu-id="f8e5b-258">В [следующей статье](iot-hub-device-sdk-c-serializer.md) мы подробно расскажем о библиотеке **serializer** .</span><span class="sxs-lookup"><span data-stu-id="f8e5b-258">The [next article](iot-hub-device-sdk-c-serializer.md) provides similar detail on the **serializer** library.</span></span>

<span data-ttu-id="f8e5b-259">Дополнительные сведения о разработке для Центра Интернета вещей см. в статье [Пакеты SDK для центра IoT][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="f8e5b-259">To learn more about developing for IoT Hub, see the [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="f8e5b-260">Для дальнейшего изучения возможностей центра IoT см. следующие статьи:</span><span class="sxs-lookup"><span data-stu-id="f8e5b-260">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="f8e5b-261">[Отправка сообщений с устройства в облако с помощью имитации устройства (Linux) с использованием Edge Интернета вещей Azure][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="f8e5b-261">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
