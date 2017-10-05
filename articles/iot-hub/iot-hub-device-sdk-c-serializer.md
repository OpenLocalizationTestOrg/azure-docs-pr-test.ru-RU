---
title: "Пакет SDK для устройств Azure IoT для C — Serializer | Документация Майкрософт"
description: "Узнайте, как использовать библиотеку Serializer в пакете SDK для устройств Azure IoT для C и как создавать приложения для устройств, взаимодействующие с Центром Интернета вещей."
services: iot-hub
documentationcenter: 
author: olivierbloch
manager: timlt
editor: 
ms.assetid: defbed34-de73-429c-8592-cd863a38e4dd
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/06/2016
ms.author: obloch
ms.openlocfilehash: aa03c29c54d75538b1fdf987cac5f09d5d344f73
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-iot-device-sdk-for-c--more-about-serializer"></a><span data-ttu-id="b9f58-103">Пакет SDK для устройств Azure IoT для C — дополнительные сведения о сериализаторе</span><span class="sxs-lookup"><span data-stu-id="b9f58-103">Azure IoT device SDK for C – more about serializer</span></span>
<span data-ttu-id="b9f58-104">В [первой статье](iot-hub-device-sdk-c-intro.md) этого курса вы познакомились с **пакетом SDK для устройств Azure IoT для C**. В следующей статье содержится более подробное описание библиотеки [**IoTHubClient**](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="b9f58-104">The [first article](iot-hub-device-sdk-c-intro.md) in this series introduced the **Azure IoT device SDK for C**. The next article provided a more detailed description of the [**IoTHubClient**](iot-hub-device-sdk-c-iothubclient.md).</span></span> <span data-ttu-id="b9f58-105">Этой статьей завершается изучение пакета SDK, в ней более подробно рассматривается оставшийся компонент — библиотека **serializer** .</span><span class="sxs-lookup"><span data-stu-id="b9f58-105">This article completes coverage of the SDK by providing a more detailed description of the remaining component: the **serializer** library.</span></span>

<span data-ttu-id="b9f58-106">В первой статье описывается, как использовать библиотеку **serializer** для отправки событий в центр IoT и получения сообщений из него.</span><span class="sxs-lookup"><span data-stu-id="b9f58-106">The introductory article described how to use the **serializer** library to send events to and receive messages from IoT Hub.</span></span> <span data-ttu-id="b9f58-107">В этой статье мы углубим свои знания, более подробно изучив моделирование данных с помощью макроязыка библиотеки **serializer** .</span><span class="sxs-lookup"><span data-stu-id="b9f58-107">In this article, we extend that discussion by providing a more complete explanation of how to model your data with the **serializer** macro language.</span></span> <span data-ttu-id="b9f58-108">В этой статье также подробнее рассматриваются механизмы, используемые библиотекой для сериализации сообщений (которые в некоторых случаях позволяют управлять поведением сериализации).</span><span class="sxs-lookup"><span data-stu-id="b9f58-108">The article also includes more detail about how the library serializes messages (and in some cases how you can control the serialization behavior).</span></span> <span data-ttu-id="b9f58-109">Также здесь описываются некоторые параметры, доступные для изменения и определяющие размер создаваемой модели.</span><span class="sxs-lookup"><span data-stu-id="b9f58-109">We'll also describe some parameters you can modify that determine the size of the models you create.</span></span>

<span data-ttu-id="b9f58-110">Кроме того, в статье мы вернемся к некоторым рассмотренным ранее вопросам, включая обработку сообщений и свойств.</span><span class="sxs-lookup"><span data-stu-id="b9f58-110">Finally, the article revisits some topics covered in previous articles such as message and property handling.</span></span> <span data-ttu-id="b9f58-111">Вы узнаете, что при использовании библиотеки **serializer** эти функции работают так же, как и при использовании библиотеки **IoTHubClient**.</span><span class="sxs-lookup"><span data-stu-id="b9f58-111">As we'll find out, those features work in the same way using the **serializer** library as they do with the **IoTHubClient** library.</span></span>

<span data-ttu-id="b9f58-112">Все приведенные здесь инструкции основаны на примерах использования примеров **serializer** из пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="b9f58-112">Everything described in this article is based on the **serializer** SDK samples.</span></span> <span data-ttu-id="b9f58-113">Чтобы перейти к выполнению действий, просмотрите приложения **simplesample\_amqp** и **simplesample\_http**, включенные в пакет SDK для устройств Azure IoT для C.</span><span class="sxs-lookup"><span data-stu-id="b9f58-113">If you want to follow along, see the **simplesample\_amqp** and **simplesample\_http** applications included in the Azure IoT device SDK for C.</span></span>

<span data-ttu-id="b9f58-114">[**Пакет SDK для устройств Интернета вещей Azure для C**](https://github.com/Azure/azure-iot-sdk-c) доступен в репозитории на сайте GitHub. Дополнительные сведения об API см. в [справочной документации по API для C](https://azure.github.io/azure-iot-sdk-c/index.html).</span><span class="sxs-lookup"><span data-stu-id="b9f58-114">You can find the [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of the API in the [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

## <a name="the-modeling-language"></a><span data-ttu-id="b9f58-115">Язык моделирования</span><span class="sxs-lookup"><span data-stu-id="b9f58-115">The modeling language</span></span>
<span data-ttu-id="b9f58-116">В [вводной статье](iot-hub-device-sdk-c-intro.md) этого курса вы познакомились с языком моделирования **пакета SDK для устройств Azure IoT для C** на примере приложения **simplesample\_amqp**.</span><span class="sxs-lookup"><span data-stu-id="b9f58-116">The [introductory article](iot-hub-device-sdk-c-intro.md) in this series introduced the **Azure IoT device SDK for C** modeling language through the example provided in the **simplesample\_amqp** application:</span></span>

```
BEGIN_NAMESPACE(WeatherStation);

DECLARE_MODEL(ContosoAnemometer,
WITH_DATA(ascii_char_ptr, DeviceId),
WITH_DATA(double, WindSpeed),
WITH_ACTION(TurnFanOn),
WITH_ACTION(TurnFanOff),
WITH_ACTION(SetAirResistance, int, Position)
);

END_NAMESPACE(WeatherStation);
```

<span data-ttu-id="b9f58-117">Как вы видите, язык моделирования основан на макросах C.</span><span class="sxs-lookup"><span data-stu-id="b9f58-117">As you can see, the modeling language is based on C macros.</span></span> <span data-ttu-id="b9f58-118">Определение всегда начинается с ключевого слова **BEGIN\_NAMESPACE** и всегда заканчивается ключевым словом **END\_NAMESPACE**.</span><span class="sxs-lookup"><span data-stu-id="b9f58-118">You always begin your definition with **BEGIN\_NAMESPACE** and always end with **END\_NAMESPACE**.</span></span> <span data-ttu-id="b9f58-119">Зачастую для пространства имен выбирается название компании или, как в этом примере, название рабочего проекта.</span><span class="sxs-lookup"><span data-stu-id="b9f58-119">It's common to name the namespace for your company or, as in this example, the project that you're working on.</span></span>

<span data-ttu-id="b9f58-120">Все, что происходит «внутри» пространства имен, определяет модель.</span><span class="sxs-lookup"><span data-stu-id="b9f58-120">What goes inside the namespace are model definitions.</span></span> <span data-ttu-id="b9f58-121">В данном случае создается одна модель для анемометра.</span><span class="sxs-lookup"><span data-stu-id="b9f58-121">In this case, there is a single model for an anemometer.</span></span> <span data-ttu-id="b9f58-122">Опять-таки, модели может быть присвоено любое имя, но обычно оно соответствует имени устройства или типу данных для взаимодействия с центром IoT.</span><span class="sxs-lookup"><span data-stu-id="b9f58-122">Once again, the model can be named anything, but typically this is named for the device or type of data you want to exchange with IoT Hub.</span></span>  

<span data-ttu-id="b9f58-123">Модели содержат определение событий, которые вы можете отправить в центр IoT (*данные*), и сообщений, которые вы можете получить из Центра Интернета вещей (*действия*).</span><span class="sxs-lookup"><span data-stu-id="b9f58-123">Models contain a definition of the events you can ingress to IoT Hub (the *data*) as well as the messages you can receive from IoT Hub (the *actions*).</span></span> <span data-ttu-id="b9f58-124">Как видно из примера, для событий указываются тип и имя; а для действий — имя и необязательные параметры (каждый с указанием типа).</span><span class="sxs-lookup"><span data-stu-id="b9f58-124">As you can see from the example, events have a type and a name; actions have a name and optional parameters (each with a type).</span></span>

<span data-ttu-id="b9f58-125">Стоит отметить, что этот пример не демонстрирует дополнительные типы данных, поддерживаемые пакетом SDK.</span><span class="sxs-lookup"><span data-stu-id="b9f58-125">What’s not demonstrated in this sample are additional data types that are supported by the SDK.</span></span> <span data-ttu-id="b9f58-126">Об этом мы поговорим далее.</span><span class="sxs-lookup"><span data-stu-id="b9f58-126">We'll cover that next.</span></span>

> [!NOTE]
> <span data-ttu-id="b9f58-127">Данные, отправляемые устройством, рассматриваются Центром Интернета вещей как *события*, тогда как в языке моделирования они называются *данными* (определяются макросом **WITH_DATA**).</span><span class="sxs-lookup"><span data-stu-id="b9f58-127">IoT Hub refers to the data a device sends to it as *events*, while the modeling language refers to it as *data* (defined using **WITH_DATA**).</span></span> <span data-ttu-id="b9f58-128">Данные, отправляемые устройству, рассматриваются центром как *сообщения*, а в языке моделирования они называются *действиями* (определяются макросом **WITH_ACTION**).</span><span class="sxs-lookup"><span data-stu-id="b9f58-128">Likewise, IoT Hub refers to the data you send to devices as *messages*, while the modeling language refers to it as *actions* (defined using **WITH_ACTION**).</span></span> <span data-ttu-id="b9f58-129">Помните, что в этой статье данные понятия могут быть взаимозаменяемыми.</span><span class="sxs-lookup"><span data-stu-id="b9f58-129">Be aware that these terms may be used interchangeably in this article.</span></span>
> 
> 

### <a name="supported-data-types"></a><span data-ttu-id="b9f58-130">Поддерживаемые типы данных.</span><span class="sxs-lookup"><span data-stu-id="b9f58-130">Supported data types</span></span>
<span data-ttu-id="b9f58-131">В моделях, созданных с помощью библиотеки **serializer** , поддерживаются следующие типы данных:</span><span class="sxs-lookup"><span data-stu-id="b9f58-131">The following data types are supported in models created with the **serializer** library:</span></span>

| <span data-ttu-id="b9f58-132">Тип</span><span class="sxs-lookup"><span data-stu-id="b9f58-132">Type</span></span> | <span data-ttu-id="b9f58-133">Описание</span><span class="sxs-lookup"><span data-stu-id="b9f58-133">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b9f58-134">double</span><span class="sxs-lookup"><span data-stu-id="b9f58-134">double</span></span> |<span data-ttu-id="b9f58-135">число с плавающей запятой двойной точности</span><span class="sxs-lookup"><span data-stu-id="b9f58-135">double precision floating point number</span></span> |
| <span data-ttu-id="b9f58-136">int</span><span class="sxs-lookup"><span data-stu-id="b9f58-136">int</span></span> |<span data-ttu-id="b9f58-137">32-разрядное целое число</span><span class="sxs-lookup"><span data-stu-id="b9f58-137">32 bit integer</span></span> |
| <span data-ttu-id="b9f58-138">float;</span><span class="sxs-lookup"><span data-stu-id="b9f58-138">float</span></span> |<span data-ttu-id="b9f58-139">число с плавающей запятой одиночной точности</span><span class="sxs-lookup"><span data-stu-id="b9f58-139">single precision floating point number</span></span> |
| <span data-ttu-id="b9f58-140">длинное целое число</span><span class="sxs-lookup"><span data-stu-id="b9f58-140">long</span></span> |<span data-ttu-id="b9f58-141">длинное целое число</span><span class="sxs-lookup"><span data-stu-id="b9f58-141">long integer</span></span> |
| <span data-ttu-id="b9f58-142">int8\_t</span><span class="sxs-lookup"><span data-stu-id="b9f58-142">int8\_t</span></span> |<span data-ttu-id="b9f58-143">8-разрядное целое число</span><span class="sxs-lookup"><span data-stu-id="b9f58-143">8 bit integer</span></span> |
| <span data-ttu-id="b9f58-144">int16\_t</span><span class="sxs-lookup"><span data-stu-id="b9f58-144">int16\_t</span></span> |<span data-ttu-id="b9f58-145">16-разрядное целое число</span><span class="sxs-lookup"><span data-stu-id="b9f58-145">16 bit integer</span></span> |
| <span data-ttu-id="b9f58-146">int32\_t</span><span class="sxs-lookup"><span data-stu-id="b9f58-146">int32\_t</span></span> |<span data-ttu-id="b9f58-147">32-разрядное целое число</span><span class="sxs-lookup"><span data-stu-id="b9f58-147">32 bit integer</span></span> |
| <span data-ttu-id="b9f58-148">int64\_t</span><span class="sxs-lookup"><span data-stu-id="b9f58-148">int64\_t</span></span> |<span data-ttu-id="b9f58-149">64-разрядное целое число</span><span class="sxs-lookup"><span data-stu-id="b9f58-149">64 bit integer</span></span> |
| <span data-ttu-id="b9f58-150">bool</span><span class="sxs-lookup"><span data-stu-id="b9f58-150">bool</span></span> |<span data-ttu-id="b9f58-151">Логическое</span><span class="sxs-lookup"><span data-stu-id="b9f58-151">boolean</span></span> |
| <span data-ttu-id="b9f58-152">ascii\_char\_ptr</span><span class="sxs-lookup"><span data-stu-id="b9f58-152">ascii\_char\_ptr</span></span> |<span data-ttu-id="b9f58-153">строка ASCII</span><span class="sxs-lookup"><span data-stu-id="b9f58-153">ASCII string</span></span> |
| <span data-ttu-id="b9f58-154">EDM\_DATE\_TIME\_OFFSET</span><span class="sxs-lookup"><span data-stu-id="b9f58-154">EDM\_DATE\_TIME\_OFFSET</span></span> |<span data-ttu-id="b9f58-155">смещение даты и времени</span><span class="sxs-lookup"><span data-stu-id="b9f58-155">date time offset</span></span> |
| <span data-ttu-id="b9f58-156">EDM\_GUID</span><span class="sxs-lookup"><span data-stu-id="b9f58-156">EDM\_GUID</span></span> |<span data-ttu-id="b9f58-157">GUID</span><span class="sxs-lookup"><span data-stu-id="b9f58-157">GUID</span></span> |
| <span data-ttu-id="b9f58-158">EDM\_BINARY</span><span class="sxs-lookup"><span data-stu-id="b9f58-158">EDM\_BINARY</span></span> |<span data-ttu-id="b9f58-159">binary;</span><span class="sxs-lookup"><span data-stu-id="b9f58-159">binary</span></span> |
| <span data-ttu-id="b9f58-160">DECLARE\_STRUCT</span><span class="sxs-lookup"><span data-stu-id="b9f58-160">DECLARE\_STRUCT</span></span> |<span data-ttu-id="b9f58-161">сложный тип данных</span><span class="sxs-lookup"><span data-stu-id="b9f58-161">complex data type</span></span> |

<span data-ttu-id="b9f58-162">Давайте начнем с последнего типа данных.</span><span class="sxs-lookup"><span data-stu-id="b9f58-162">Let’s start with the last data type.</span></span> <span data-ttu-id="b9f58-163">Макрос **DECLARE\_STRUCT** позволяет определять сложные типы данных, которые являются группировками других простых типов.</span><span class="sxs-lookup"><span data-stu-id="b9f58-163">The **DECLARE\_STRUCT** allows you to define complex data types, which are groupings of the other primitive types.</span></span> <span data-ttu-id="b9f58-164">Эти группировки позволяют определить модель, которая выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="b9f58-164">These groupings allow us to define a model that looks like this:</span></span>

```
DECLARE_STRUCT(TestType,
double, aDouble,
int, aInt,
float, aFloat,
long, aLong,
int8_t, aInt8,
uint8_t, auInt8,
int16_t, aInt16,
int32_t, aInt32,
int64_t, aInt64,
bool, aBool,
ascii_char_ptr, aAsciiCharPtr,
EDM_DATE_TIME_OFFSET, aDateTimeOffset,
EDM_GUID, aGuid,
EDM_BINARY, aBinary
);

DECLARE_MODEL(TestModel,
WITH_DATA(TestType, Test)
);
```

<span data-ttu-id="b9f58-165">Наша модель содержит одно событие, инициируемое изменением данных, типа **TestType**.</span><span class="sxs-lookup"><span data-stu-id="b9f58-165">Our model contains a single data event of type **TestType**.</span></span> <span data-ttu-id="b9f58-166">**TestType** является сложным типом, который содержит несколько элементов, совокупно представляющих простые типы, поддерживаемые языком моделирования **serializer**.</span><span class="sxs-lookup"><span data-stu-id="b9f58-166">**TestType** is a complex type that includes several members, which collectively demonstrate the primitive types supported by the **serializer** modeling language.</span></span>

<span data-ttu-id="b9f58-167">С помощью такой модели мы можем отправлять данные в центр IoT, используя следующий код:</span><span class="sxs-lookup"><span data-stu-id="b9f58-167">With a model like this, we can write code to send data to IoT Hub that appears as follows:</span></span>

```
TestModel* testModel = CREATE_MODEL_INSTANCE(MyThermostat, TestModel);

testModel->Test.aDouble = 1.1;
testModel->Test.aInt = 2;
testModel->Test.aFloat = 3.0f;
testModel->Test.aLong = 4;
testModel->Test.aInt8 = 5;
testModel->Test.auInt8 = 6;
testModel->Test.aInt16 = 7;
testModel->Test.aInt32 = 8;
testModel->Test.aInt64 = 9;
testModel->Test.aBool = true;
testModel->Test.aAsciiCharPtr = "ascii string 1";

time_t now;
time(&now);
testModel->Test.aDateTimeOffset = GetDateTimeOffset(now);

EDM_GUID guid = { { 0x00, 0x01, 0x02, 0x03, 0x04, 0x05, 0x06, 0x07, 0x08, 0x09, 0x0A, 0x0B, 0x0C, 0x0D, 0x0E, 0x0F } };
testModel->Test.aGuid = guid;

unsigned char binaryArray[3] = { 0x01, 0x02, 0x03 };
EDM_BINARY binaryData = { sizeof(binaryArray), &binaryArray };
testModel->Test.aBinary = binaryData;

SendAsync(iotHubClientHandle, (const void*)&(testModel->Test));
```

<span data-ttu-id="b9f58-168">Фактически мы присваиваем значение каждому элементу структуры **Test**, а затем вызываем **SendAsync** для отправки события **Test** в облако.</span><span class="sxs-lookup"><span data-stu-id="b9f58-168">Basically, we’re assigning a value to every member of the **Test** structure and then calling **SendAsync** to send the **Test** data event to the cloud.</span></span> <span data-ttu-id="b9f58-169">**SendAsync** является вспомогательной и служит для отправки одного события, инициируемого изменением данных, в центр IoT:</span><span class="sxs-lookup"><span data-stu-id="b9f58-169">**SendAsync** is a helper function that sends a single data event to IoT Hub:</span></span>

```
void SendAsync(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const void *dataEvent)
{
    unsigned char* destination;
    size_t destinationSize;
    if (SERIALIZE(&destination, &destinationSize, *(const unsigned char*)dataEvent) ==
    {
        // null terminate the string
        char* destinationAsString = (char*)malloc(destinationSize + 1);
        if (destinationAsString != NULL)
        {
            memcpy(destinationAsString, destination, destinationSize);
            destinationAsString[destinationSize] = '\0';
            IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromString(destinationAsString);
            if (messageHandle != NULL)
            {
                IoTHubClient_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)0);

                IoTHubMessage_Destroy(messageHandle);
            }
            free(destinationAsString);
        }
        free(destination);
    }
}
```

<span data-ttu-id="b9f58-170">Эта функция сериализует нужное нам событие, инициируемое изменением данных, и отправляет его в Центр Интернета вещей с помощью функции **IoTHubClient\_SendEventAsync**.</span><span class="sxs-lookup"><span data-stu-id="b9f58-170">This function serializes the given data event and sends it to IoT Hub using **IoTHubClient\_SendEventAsync**.</span></span> <span data-ttu-id="b9f58-171">Этот код мы уже использовали в предыдущих статьях (**SendAsync** просто заключает логику в удобную функцию).</span><span class="sxs-lookup"><span data-stu-id="b9f58-171">This is the same code discussed in previous articles (**SendAsync** encapsulates the logic into a convenient function).</span></span>

<span data-ttu-id="b9f58-172">В приведенном выше коде используется еще одна вспомогательная функция — **GetDateTimeOffset**.</span><span class="sxs-lookup"><span data-stu-id="b9f58-172">One other helper function used in the previous code is **GetDateTimeOffset**.</span></span> <span data-ttu-id="b9f58-173">Эта функция преобразует заданное значение времени в значение типа **EDM\_DATE\_TIME\_OFFSET**:</span><span class="sxs-lookup"><span data-stu-id="b9f58-173">This function transforms the given time into a value of type **EDM\_DATE\_TIME\_OFFSET**:</span></span>

```
EDM_DATE_TIME_OFFSET GetDateTimeOffset(time_t time)
{
    struct tm newTime;
    gmtime_s(&newTime, &time);
    EDM_DATE_TIME_OFFSET dateTimeOffset;
    dateTimeOffset.dateTime = newTime;
    dateTimeOffset.fractionalSecond = 0;
    dateTimeOffset.hasFractionalSecond = 0;
    dateTimeOffset.hasTimeZone = 0;
    dateTimeOffset.timeZoneHour = 0;
    dateTimeOffset.timeZoneMinute = 0;
    return dateTimeOffset;
}
```

<span data-ttu-id="b9f58-174">Если запустить этот код, в центр IoT будет отправлено следующее сообщение:</span><span class="sxs-lookup"><span data-stu-id="b9f58-174">If you run this code, the following message is sent to IoT Hub:</span></span>

```
{"aDouble":1.100000000000000, "aInt":2, "aFloat":3.000000, "aLong":4, "aInt8":5, "auInt8":6, "aInt16":7, "aInt32":8, "aInt64":9, "aBool":true, "aAsciiCharPtr":"ascii string 1", "aDateTimeOffset":"2015-09-14T21:18:21Z", "aGuid":"00010203-0405-0607-0809-0A0B0C0D0E0F", "aBinary":"AQID"}
```

<span data-ttu-id="b9f58-175">Обратите внимание, что сериализация выполняется в формате JSON. В библиотеке **serializer** для сериализации используется именно этот формат.</span><span class="sxs-lookup"><span data-stu-id="b9f58-175">Note that the serialization is JSON, which is the format generated by the **serializer** library.</span></span> <span data-ttu-id="b9f58-176">Также обратите внимание, что каждый элемент сериализованного объекта JSON соответствует элементам типа **TestType**, определенного в нашей модели.</span><span class="sxs-lookup"><span data-stu-id="b9f58-176">Also note that each member of the serialized JSON object matches the members of the **TestType** that we defined in our model.</span></span> <span data-ttu-id="b9f58-177">Значения также совпадают с теми, которые использовались в коде.</span><span class="sxs-lookup"><span data-stu-id="b9f58-177">The values also exactly match those used in the code.</span></span> <span data-ttu-id="b9f58-178">Однако учтите, что двоичные данные имеют кодировку base64. В данном случае значению AQID соответствует строка {0x01, 0x02, 0x03} в кодировке base64.</span><span class="sxs-lookup"><span data-stu-id="b9f58-178">However, note that the binary data is base64-encoded: "AQID" is the base64 encoding of {0x01, 0x02, 0x03}.</span></span>

<span data-ttu-id="b9f58-179">В этом примере показаны преимущества использования библиотеки **serializer**. Она позволяет отправлять данные JSON в облако без необходимости выполнять явную сериализацию в коде приложения.</span><span class="sxs-lookup"><span data-stu-id="b9f58-179">This example demonstrates the advantage of using the **serializer** library -- it enables us to send JSON to the cloud, without having to explicitly deal with serialization in our application.</span></span> <span data-ttu-id="b9f58-180">Все, что от нас требуется, — это задать в модели значения для событий, инициируемых изменением данных, а затем вызвать простые API для отправки этих событий в облако.</span><span class="sxs-lookup"><span data-stu-id="b9f58-180">All we have to worry about is setting the values of the data events in our model and then calling simple APIs to send those events to the cloud.</span></span>

<span data-ttu-id="b9f58-181">Используя эту информацию, вы сможете определять модели с использованием различных типов данных, включая сложные типы (мы даже можем включить одни сложные типы в другие).</span><span class="sxs-lookup"><span data-stu-id="b9f58-181">With this information, we can define models that include the range of supported data types, including complex types (we could even include complex types within other complex types).</span></span> <span data-ttu-id="b9f58-182">Но сериализованный код JSON, созданный в этом примере, поднимает один важный вопрос.</span><span class="sxs-lookup"><span data-stu-id="b9f58-182">However, he serialized JSON generated by the example above brings up an important point.</span></span> <span data-ttu-id="b9f58-183">*Каким образом* при отправке данных библиотека **serializer** определяет способ формирования JSON?</span><span class="sxs-lookup"><span data-stu-id="b9f58-183">*How* we send data with the **serializer** library determines exactly how the JSON is formed.</span></span> <span data-ttu-id="b9f58-184">Об этом моменте мы поговорим далее.</span><span class="sxs-lookup"><span data-stu-id="b9f58-184">That particular point is what we'll cover next.</span></span>

## <a name="more-about-serialization"></a><span data-ttu-id="b9f58-185">Дополнительные сведения о сериализации</span><span class="sxs-lookup"><span data-stu-id="b9f58-185">More about serialization</span></span>
<span data-ttu-id="b9f58-186">В предыдущем разделе был приведен пример выходных данных, созданных библиотекой **serializer** .</span><span class="sxs-lookup"><span data-stu-id="b9f58-186">The previous section highlights an example of the output generated by the **serializer** library.</span></span> <span data-ttu-id="b9f58-187">В этом разделе мы объясним, как библиотека сериализует данные и как вы можете управлять этим поведением с помощью API сериализации.</span><span class="sxs-lookup"><span data-stu-id="b9f58-187">In this section, we'll explain how the library serializes data and how you can control that behavior using the serialization APIs.</span></span>

<span data-ttu-id="b9f58-188">Чтобы продолжить изучение сериализации, мы создадим новую модель на основе термостата.</span><span class="sxs-lookup"><span data-stu-id="b9f58-188">In order to advance the discussion on serialization, we'll work with a new model based on a thermostat.</span></span> <span data-ttu-id="b9f58-189">Сначала мы приведем более подробную информацию о сценарии, который мы пытаемся реализовать.</span><span class="sxs-lookup"><span data-stu-id="b9f58-189">First, let's provide some background on the scenario we're trying to address.</span></span>

<span data-ttu-id="b9f58-190">Нам нужна модель термостата, который измеряет температуру и влажность.</span><span class="sxs-lookup"><span data-stu-id="b9f58-190">We want to model a thermostat that measures temperature and humidity.</span></span> <span data-ttu-id="b9f58-191">Каждый блок данных будет отправляться в центр IoT по отдельности.</span><span class="sxs-lookup"><span data-stu-id="b9f58-191">Each piece of data is going to be sent to IoT Hub differently.</span></span> <span data-ttu-id="b9f58-192">По умолчанию термостат генерирует событие температуры каждые 2 минуты, а событие влажности — каждые 15 минут.</span><span class="sxs-lookup"><span data-stu-id="b9f58-192">By default, the thermostat ingresses a temperature event once every 2 minutes; a humidity event is ingressed once every 15 minutes.</span></span> <span data-ttu-id="b9f58-193">В каждое генерируемое событие необходимо включить метку времени, в которое были измерены соответствующие показатели температуры или влажности.</span><span class="sxs-lookup"><span data-stu-id="b9f58-193">When either event is ingressed, it must include a timestamp that shows the time that the corresponding temperature or humidity was measured.</span></span>

<span data-ttu-id="b9f58-194">На основании этого сценария мы покажем два способа моделирования данных и объясним влияние каждого из этих способов на сериализованные выходные данные.</span><span class="sxs-lookup"><span data-stu-id="b9f58-194">Given this scenario, we'll demonstrate two different ways to model the data, and we'll explain the effect that modeling has on the serialized output.</span></span>

### <a name="model-1"></a><span data-ttu-id="b9f58-195">Модель 1</span><span class="sxs-lookup"><span data-stu-id="b9f58-195">Model 1</span></span>
<span data-ttu-id="b9f58-196">Вот первый вариант модели, которая поддерживает предыдущий сценарий.</span><span class="sxs-lookup"><span data-stu-id="b9f58-196">Here's the first version of a model that supports the previous scenario:</span></span>

```
BEGIN_NAMESPACE(Contoso);

DECLARE_STRUCT(TemperatureEvent,
int, Temperature,
EDM_DATE_TIME_OFFSET, Time);

DECLARE_STRUCT(HumidityEvent,
int, Humidity,
EDM_DATE_TIME_OFFSET, Time);

DECLARE_MODEL(Thermostat,
WITH_DATA(TemperatureEvent, Temperature),
WITH_DATA(HumidityEvent, Humidity)
);

END_NAMESPACE(Contoso);
```

<span data-ttu-id="b9f58-197">Обратите внимание, что модель включает два события, инициируемых изменением данных: **Temperature** и **Humidity**.</span><span class="sxs-lookup"><span data-stu-id="b9f58-197">Note that the model includes two data events: **Temperature** and **Humidity**.</span></span> <span data-ttu-id="b9f58-198">В отличие от предыдущих примеров, тип каждого события представлен структурой, определенной с помощью макроса **DECLARE\_STRUCT**.</span><span class="sxs-lookup"><span data-stu-id="b9f58-198">Unlike previous examples, the type of each event is a structure defined using **DECLARE\_STRUCT**.</span></span> <span data-ttu-id="b9f58-199">Структура **TemperatureEvent** содержит значение измеренной температуры и метку времени, а структура **HumidityEvent** — значение измеренной влажности и метку времени.</span><span class="sxs-lookup"><span data-stu-id="b9f58-199">**TemperatureEvent** includes a temperature measurement and a timestamp; **HumidityEvent** contains a humidity measurement and a timestamp.</span></span> <span data-ttu-id="b9f58-200">Эта модель естественным образом моделирует данные для описанного выше сценария.</span><span class="sxs-lookup"><span data-stu-id="b9f58-200">This model gives us a natural way to model the data for the scenario described above.</span></span> <span data-ttu-id="b9f58-201">Когда мы отправляем событие в облако, мы будем отправлять либо пару значений "температура/время", либо пару значений "влажность/время".</span><span class="sxs-lookup"><span data-stu-id="b9f58-201">When we send an event to the cloud, we'll either send a temperature/timestamp or a humidity/timestamp pair.</span></span>

<span data-ttu-id="b9f58-202">Событие температуры можно отправить в облако с помощью следующего кода:</span><span class="sxs-lookup"><span data-stu-id="b9f58-202">We can send a temperature event to the cloud using code such as the following:</span></span>

```
time_t now;
time(&now);
thermostat->Temperature.Temperature = 75;
thermostat->Temperature.Time = GetDateTimeOffset(now);

unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="b9f58-203">В этом примере мы используем жестко заданные значения температуры и влажности. Но предположим, что эти значения поступают от соответствующих датчиков реального термостата.</span><span class="sxs-lookup"><span data-stu-id="b9f58-203">We'll use hard-coded values for temperature and humidity in the sample code, but imagine that we’re actually retrieving these values by sampling the corresponding sensors on the thermostat.</span></span>

<span data-ttu-id="b9f58-204">В приведенном выше примере используется вспомогательный метод **GetDateTimeOffset** , о котором было сказано ранее.</span><span class="sxs-lookup"><span data-stu-id="b9f58-204">The code above uses the **GetDateTimeOffset** helper that was introduced previously.</span></span> <span data-ttu-id="b9f58-205">По причинам, о которых будет сказано позже, задачи сериализации и отправки события в этом коде выполняются раздельно.</span><span class="sxs-lookup"><span data-stu-id="b9f58-205">For reasons that will become clear later, this code explicitly separates the task of serializing and sending the event.</span></span> <span data-ttu-id="b9f58-206">Событие температуры сериализуется предыдущим кодом в буфер.</span><span class="sxs-lookup"><span data-stu-id="b9f58-206">The previous code serializes the temperature event into a buffer.</span></span> <span data-ttu-id="b9f58-207">Затем вспомогательная функция **sendMessage** (включена в приложение **simplesample\_amqp**) отправляет событие в Центр Интернета вещей:</span><span class="sxs-lookup"><span data-stu-id="b9f58-207">Then, **sendMessage** is a helper function (included in **simplesample\_amqp**) that sends the event to IoT Hub:</span></span>

```
static void sendMessage(IOTHUB_CLIENT_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
{
    static unsigned int messageTrackingId;
    IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
    if (messageHandle != NULL)
    {
        IoTHubClient_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)(uintptr_t)messageTrackingId);

        IoTHubMessage_Destroy(messageHandle);
    }
    free((void*)buffer);
}
```

<span data-ttu-id="b9f58-208">Этот код является частью вспомогательного метода **SendAsync** , описанного в предыдущем разделе, поэтому мы не будем повторно рассказывать о нем.</span><span class="sxs-lookup"><span data-stu-id="b9f58-208">This code is a subset of the **SendAsync** helper described in the previous section, so we won’t go over it again here.</span></span>

<span data-ttu-id="b9f58-209">Если запустить приведенный код для отправки события температуры, в центр IoT отправится следующая сериализованная строка:</span><span class="sxs-lookup"><span data-stu-id="b9f58-209">When we run the previous code to send the Temperature event, this serialized form of the event is sent to IoT Hub:</span></span>

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="b9f58-210">Мы отправляем значение температуры с типом **TemperatureEvent**. Эта структура содержит элементы **Temperature** и **Time**.</span><span class="sxs-lookup"><span data-stu-id="b9f58-210">We're sending a temperature which is of type **TemperatureEvent** and that struct contains a **Temperature** and **Time** member.</span></span> <span data-ttu-id="b9f58-211">Это напрямую отражается в сериализованных данных.</span><span class="sxs-lookup"><span data-stu-id="b9f58-211">This is directly reflected in the serialized data.</span></span>

<span data-ttu-id="b9f58-212">Точно так же событие влажности можно отправить с помощью следующего кода:</span><span class="sxs-lookup"><span data-stu-id="b9f58-212">Similarly, we can send a humidity event with this code:</span></span>

```
thermostat->Humidity.Humidity = 45;
thermostat->Humidity.Time = GetDateTimeOffset(now);
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="b9f58-213">Сериализованная форма, которая отправляется в центр IoT, выглядит так:</span><span class="sxs-lookup"><span data-stu-id="b9f58-213">The serialized form that’s sent to IoT Hub appears as follows:</span></span>

```
{"Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="b9f58-214">Опять же, все как и ожидалось.</span><span class="sxs-lookup"><span data-stu-id="b9f58-214">Again, this is as expected.</span></span>

<span data-ttu-id="b9f58-215">С помощью этой модели можно понять, как легко добавить дополнительные события.</span><span class="sxs-lookup"><span data-stu-id="b9f58-215">With this model, you can imagine how additional events can easily be added.</span></span> <span data-ttu-id="b9f58-216">Можно определить дополнительные структуры с помощью макроса **DECLARE\_STRUCT** и включить соответствующее событие в модель с помощью макроса **WITH\_DATA**.</span><span class="sxs-lookup"><span data-stu-id="b9f58-216">You define more structures using **DECLARE\_STRUCT**, and include the corresponding event in the model using **WITH\_DATA**.</span></span>

<span data-ttu-id="b9f58-217">Теперь давайте изменим модель, включив в нее те же данные, но с другой структурой.</span><span class="sxs-lookup"><span data-stu-id="b9f58-217">Now, let’s modify the model so that it includes the same data but with a different structure.</span></span>

### <a name="model-2"></a><span data-ttu-id="b9f58-218">Модель 2</span><span class="sxs-lookup"><span data-stu-id="b9f58-218">Model 2</span></span>
<span data-ttu-id="b9f58-219">Рассмотрим следующую измененную модель:</span><span class="sxs-lookup"><span data-stu-id="b9f58-219">Consider this alternative model to the one above:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="b9f58-220">Здесь мы убрали макрос **DECLARE\_STRUCT** и определили элементы данных из нашего сценария с помощью простых типов языка моделирования.</span><span class="sxs-lookup"><span data-stu-id="b9f58-220">In this case we've eliminated the **DECLARE\_STRUCT** macros and are simply defining the data items from our scenario using simple types from the modeling language.</span></span>

<span data-ttu-id="b9f58-221">В данный момент не обращайте внимание на событие **Time** .</span><span class="sxs-lookup"><span data-stu-id="b9f58-221">Just for the moment let’s ignore the **Time** event.</span></span> <span data-ttu-id="b9f58-222">Следовательно, код вызова события **Temperature**будет выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="b9f58-222">With that aside, here’s the code to ingress **Temperature**:</span></span>

```
time_t now;
time(&now);
thermostat->Temperature = 75;

unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="b9f58-223">Этот код отправляет в центр IoT следующее сериализованное событие:</span><span class="sxs-lookup"><span data-stu-id="b9f58-223">This code sends the following serialized event to IoT Hub:</span></span>

```
{"Temperature":75}
```

<span data-ttu-id="b9f58-224">Код для отправки события влажности выглядит так:</span><span class="sxs-lookup"><span data-stu-id="b9f58-224">And the code for sending the Humidity event appears as follows:</span></span>

```
thermostat->Humidity = 45;
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="b9f58-225">В центр IoT отправляется следующее:</span><span class="sxs-lookup"><span data-stu-id="b9f58-225">This code sends this to IoT Hub:</span></span>

```
{"Humidity":45}
```

<span data-ttu-id="b9f58-226">По-прежнему ничего непредвиденного.</span><span class="sxs-lookup"><span data-stu-id="b9f58-226">So far there are still no surprises.</span></span> <span data-ttu-id="b9f58-227">Теперь давайте изменим способ использования макроса SERIALIZE.</span><span class="sxs-lookup"><span data-stu-id="b9f58-227">Now let's change how we use the SERIALIZE macro.</span></span>

<span data-ttu-id="b9f58-228">Макрос **SERIALIZE** может принимать несколько событий, инициируемых изменением данных, в качестве аргументов.</span><span class="sxs-lookup"><span data-stu-id="b9f58-228">The **SERIALIZE** macro can take multiple data events as arguments.</span></span> <span data-ttu-id="b9f58-229">Это позволит нам одновременно сериализовать события **Temperature** и **Humidity** и отправить их в Центр Интернета вещей в рамках одного вызова:</span><span class="sxs-lookup"><span data-stu-id="b9f58-229">This enables us to serialize the **Temperature** and **Humidity** event together and send them to IoT Hub in one call:</span></span>

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="b9f58-230">Как вы можете догадаться, результатом выполнения этого кода является отправка двух событий, инициируемых изменением данных, в центр IoT:</span><span class="sxs-lookup"><span data-stu-id="b9f58-230">You might guess that the result of this code is that two data events are sent to IoT Hub:</span></span>

<span data-ttu-id="b9f58-231">[</span><span class="sxs-lookup"><span data-stu-id="b9f58-231">[</span></span>

<span data-ttu-id="b9f58-232">{"Temperature":75},</span><span class="sxs-lookup"><span data-stu-id="b9f58-232">{"Temperature":75},</span></span>

<span data-ttu-id="b9f58-233">{"Humidity":45}</span><span class="sxs-lookup"><span data-stu-id="b9f58-233">{"Humidity":45}</span></span>

<span data-ttu-id="b9f58-234">]</span><span class="sxs-lookup"><span data-stu-id="b9f58-234">]</span></span>

<span data-ttu-id="b9f58-235">Другими словами, можно предположить, что этот код равнозначен отправке событий **Temperature** и **Humidity** по отдельности.</span><span class="sxs-lookup"><span data-stu-id="b9f58-235">In other words, you might expect that this code is the same as sending **Temperature** and **Humidity** separately.</span></span> <span data-ttu-id="b9f58-236">Это просто удобный способ передачи обоих событий в метод **SERIALIZE** одним вызовом.</span><span class="sxs-lookup"><span data-stu-id="b9f58-236">It’s just a convenience to pass both events to **SERIALIZE** in the same call.</span></span> <span data-ttu-id="b9f58-237">Однако это не так.</span><span class="sxs-lookup"><span data-stu-id="b9f58-237">However, that’s not the case.</span></span> <span data-ttu-id="b9f58-238">Вместо этого, приведенный выше код отправляет в центр IoT одно событие, инициируемое изменением данных:</span><span class="sxs-lookup"><span data-stu-id="b9f58-238">Instead, the code above sends this single data event to IoT Hub:</span></span>

<span data-ttu-id="b9f58-239">{"Temperature":75, "Humidity":45}</span><span class="sxs-lookup"><span data-stu-id="b9f58-239">{"Temperature":75, "Humidity":45}</span></span>

<span data-ttu-id="b9f58-240">Это может показаться странным, так как в нашей модели события **Temperature** и **Humidity** определены как два *отдельных* события:</span><span class="sxs-lookup"><span data-stu-id="b9f58-240">This may seem strange because our model defines **Temperature** and **Humidity** as two *separate* events:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="b9f58-241">Более того, в нашей модели мы не включали события **Temperature** и **Humidity** в одну структуру:</span><span class="sxs-lookup"><span data-stu-id="b9f58-241">More to the point, we didn’t model these events where **Temperature** and **Humidity** are in the same structure:</span></span>

```
DECLARE_STRUCT(TemperatureAndHumidityEvent,
int, Temperature,
int, Humidity,
);

DECLARE_MODEL(Thermostat,
WITH_DATA(TemperatureAndHumidityEvent, TemperatureAndHumidity),
);
```

<span data-ttu-id="b9f58-242">На примере использования этой модели будет проще понять, каким образом события **Temperature** и **Humidity** отправляются в одном сериализованном сообщении.</span><span class="sxs-lookup"><span data-stu-id="b9f58-242">If we used this model, it would be easier to understand how **Temperature** and **Humidity** would be sent in the same serialized message.</span></span> <span data-ttu-id="b9f58-243">При этом механизм действия при передаче обоих событий, инициируемых изменением данных, в метод **SERIALIZE** с помощью модели 2 может быть непонятным.</span><span class="sxs-lookup"><span data-stu-id="b9f58-243">However it may not be clear why it works that way when you pass both data events to **SERIALIZE** using model 2.</span></span>

<span data-ttu-id="b9f58-244">Это поведение проще понять, если знать о допущениях библиотеки **serializer** .</span><span class="sxs-lookup"><span data-stu-id="b9f58-244">This behavior is easier to understand if you know the assumptions that the **serializer** library is making.</span></span> <span data-ttu-id="b9f58-245">Чтобы все прояснить, давайте вернемся к нашей модели:</span><span class="sxs-lookup"><span data-stu-id="b9f58-245">To make sense of this let’s go back to our model:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="b9f58-246">Взгляните на эту модель в контексте объектно-ориентированного подхода.</span><span class="sxs-lookup"><span data-stu-id="b9f58-246">Think of this model in object-oriented terms.</span></span> <span data-ttu-id="b9f58-247">В этом случае мы моделируем физическое устройство (термостат), которое включает некие атрибуты (например, **Temperature** и **Humidity**).</span><span class="sxs-lookup"><span data-stu-id="b9f58-247">In this case we’re modeling a physical device (a thermostat) and that device includes attributes like **Temperature** and **Humidity**.</span></span>

<span data-ttu-id="b9f58-248">Мы можем отправить общее состояние нашей модели с помощью следующего кода:</span><span class="sxs-lookup"><span data-stu-id="b9f58-248">We can send the entire state of our model with code such as the following:</span></span>

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity, thermostat->Time) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="b9f58-249">Если указаны значения температуры, влажности и времени, в центр IoT будет отправлено событие со следующим содержимым:</span><span class="sxs-lookup"><span data-stu-id="b9f58-249">Assuming the values of Temperature, Humidity and Time are set, we would see an event like this sent to IoT Hub:</span></span>

```
{"Temperature":75, "Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="b9f58-250">Иногда вам нужно отправлять в облако значения только *некоторых* свойств модели (особенно это касается случаев, когда модель содержит большое количество событий, инициируемых изменением данных).</span><span class="sxs-lookup"><span data-stu-id="b9f58-250">Sometimes you may only want to send *some* properties of the model to the cloud (this is especially true if your model contains a large number of data events).</span></span> <span data-ttu-id="b9f58-251">Полезно отправлять только некоторые события, инициируемые изменением данных, как это было в примере выше:</span><span class="sxs-lookup"><span data-stu-id="b9f58-251">It’s useful to send only a subset of data events, such as in our earlier example:</span></span>

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="b9f58-252">В результате будет создано такое же сериализованное событие, как и при определении **TemperatureEvent** с атрибутами **Temperature** и **Time**(модель 1).</span><span class="sxs-lookup"><span data-stu-id="b9f58-252">This generates exactly the same serialized event as if we had defined a **TemperatureEvent** with a **Temperature** and **Time** member, just as we did with model 1.</span></span> <span data-ttu-id="b9f58-253">За счет вызова метода **SERIALIZE** другим способом мы можем создать такое же сериализованное событие с помощью другой модели (модель 2).</span><span class="sxs-lookup"><span data-stu-id="b9f58-253">In this case we were able to generate exactly the same serialized event by using a different model (model 2) because we called **SERIALIZE** in a different way.</span></span>

<span data-ttu-id="b9f58-254">Важно помнить, что при передаче в метод **SERIALIZE** нескольких событий, инициируемых изменением данных, каждое такое событие рассматривается как отдельное свойство одного объекта JSON.</span><span class="sxs-lookup"><span data-stu-id="b9f58-254">The important point is that if you pass multiple data events to **SERIALIZE,** then it assumes each event is a property in a single JSON object.</span></span>

<span data-ttu-id="b9f58-255">Выбор наиболее подходящего подхода зависит от того, как вы воспринимаете модель.</span><span class="sxs-lookup"><span data-stu-id="b9f58-255">The best approach depends on you and how you think about your model.</span></span> <span data-ttu-id="b9f58-256">Если вы отправляете "события" в облако, когда каждое событие содержит определенный набор свойств, вам лучше выбрать первый подход.</span><span class="sxs-lookup"><span data-stu-id="b9f58-256">If you’re sending "events" to the cloud and each event contains a defined set of properties, then the first approach makes a lot of sense.</span></span> <span data-ttu-id="b9f58-257">В этом случае с помощью макроса **DECLARE\_STRUCT** определяется структура каждого события, а затем они включаются в модель с помощью макроса **WITH\_DATA**.</span><span class="sxs-lookup"><span data-stu-id="b9f58-257">In that case you would use **DECLARE\_STRUCT** to define the structure of each event and then include them in your model with the **WITH\_DATA** macro.</span></span> <span data-ttu-id="b9f58-258">Теперь события можно отправлять, как описано в первом примере.</span><span class="sxs-lookup"><span data-stu-id="b9f58-258">Then you send each event as we did in the first example above.</span></span> <span data-ttu-id="b9f58-259">При использовании этого подхода в метод **SERIALIZER**будет передаваться только одно событие, инициируемое изменением данных.</span><span class="sxs-lookup"><span data-stu-id="b9f58-259">In this approach you would only pass a single data event to **SERIALIZER**.</span></span>

<span data-ttu-id="b9f58-260">Если вы рассматриваете свою модель с точки зрения объектно-ориентированного подхода, вам лучше использовать второй метод.</span><span class="sxs-lookup"><span data-stu-id="b9f58-260">If you think about your model in an object-oriented fashion, then the second approach may suit you.</span></span> <span data-ttu-id="b9f58-261">В этом случае элементы, определенные с помощью макроса **WITH\_DATA**, будут свойствами вашего объекта.</span><span class="sxs-lookup"><span data-stu-id="b9f58-261">In this case, the elements defined using **WITH\_DATA** are the "properties" of your object.</span></span> <span data-ttu-id="b9f58-262">В метод **SERIALIZE** вы можете передавать любое подмножество событий на основе требований к передаче данных о состоянии объекта в облако.</span><span class="sxs-lookup"><span data-stu-id="b9f58-262">You pass whatever subset of events to **SERIALIZE** that you like, depending on how much of your "object’s" state you want to send to the cloud.</span></span>

<span data-ttu-id="b9f58-263">Ни один из подходов нельзя назвать правильным или ошибочным.</span><span class="sxs-lookup"><span data-stu-id="b9f58-263">Nether approach is right or wrong.</span></span> <span data-ttu-id="b9f58-264">Просто нужно знать о принципах работы библиотеки **serializer** и использовать тот подход к моделированию, который подходит именно вам.</span><span class="sxs-lookup"><span data-stu-id="b9f58-264">Just be aware of how the **serializer** library works, and pick the modeling approach that best fits your needs.</span></span>

## <a name="message-handling"></a><span data-ttu-id="b9f58-265">Обработка сообщений</span><span class="sxs-lookup"><span data-stu-id="b9f58-265">Message handling</span></span>
<span data-ttu-id="b9f58-266">До сих пор в этой статье рассказывалось только об отправке событий в центр IoT, но не об их получении.</span><span class="sxs-lookup"><span data-stu-id="b9f58-266">So far this article has only discussed sending events to IoT Hub, and hasn't addressed receiving messages.</span></span> <span data-ttu-id="b9f58-267">Это связано с тем, что большая часть информации о получении сообщений была изложена в [предыдущей статье](iot-hub-device-sdk-c-intro.md).</span><span class="sxs-lookup"><span data-stu-id="b9f58-267">The reason for this is that what we need to know about receiving messages has largely been covered in an [earlier article](iot-hub-device-sdk-c-intro.md).</span></span> <span data-ttu-id="b9f58-268">Как вы помните, обработка сообщений выполняется путем регистрации функции обратного вызова:</span><span class="sxs-lookup"><span data-stu-id="b9f58-268">Recall from that article that you process messages by registering a message callback function:</span></span>

```
IoTHubClient_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather)
```

<span data-ttu-id="b9f58-269">Затем вы создаете функцию обратного вызова, которая вызывается при получении сообщения:</span><span class="sxs-lookup"><span data-stu-id="b9f58-269">You then write the callback function that’s invoked when a message is received:</span></span>

```
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable to IoTHubMessage_GetByteArray\r\n");
        result = EXECUTE_COMMAND_ERROR;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed to malloc\r\n");
            result = EXECUTE_COMMAND_ERROR;
        }
        else
        {
            memcpy(temp, buffer, size);
            temp[size] = '\0';
            EXECUTE_COMMAND_RESULT executeCommandResult = EXECUTE_COMMAND(userContextCallback, temp);
            result =
                (executeCommandResult == EXECUTE_COMMAND_ERROR) ? IOTHUBMESSAGE_ABANDONED :
                (executeCommandResult == EXECUTE_COMMAND_SUCCESS) ? IOTHUBMESSAGE_ACCEPTED :
                IOTHUBMESSAGE_REJECTED;
            free(temp);
        }
    }
    return result;
}
```

<span data-ttu-id="b9f58-270">Эта реализация **IoTHubMessage** обеспечивает вызов нужной функции для каждого действия, определенного в модели.</span><span class="sxs-lookup"><span data-stu-id="b9f58-270">This implementation of **IoTHubMessage** calls the specific function for each action in your model.</span></span> <span data-ttu-id="b9f58-271">Например, если модель определяет следующее действие:</span><span class="sxs-lookup"><span data-stu-id="b9f58-271">For example, if your model defines this action:</span></span>

```
WITH_ACTION(SetAirResistance, int, Position)
```

<span data-ttu-id="b9f58-272">Вам нужно определить функцию со следующей сигнатурой:</span><span class="sxs-lookup"><span data-stu-id="b9f58-272">You must define a function with this signature:</span></span>

```
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position to %d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

<span data-ttu-id="b9f58-273">**SetAirResistance** вызывается при отправке сообщения устройству.</span><span class="sxs-lookup"><span data-stu-id="b9f58-273">**SetAirResistance** is then called when that message is sent to your device.</span></span>

<span data-ttu-id="b9f58-274">Но мы все еще не рассказали вам о том, как выглядит сериализованная версия сообщения.</span><span class="sxs-lookup"><span data-stu-id="b9f58-274">What we haven't explained yet is what the serialized version of message looks like.</span></span> <span data-ttu-id="b9f58-275">Другими словами, если вы хотите отправить устройству сообщение **SetAirResistance** , как оно будет выглядеть?</span><span class="sxs-lookup"><span data-stu-id="b9f58-275">In other words, if you want to send a **SetAirResistance** message to your device, what does that look like?</span></span>

<span data-ttu-id="b9f58-276">При отправке сообщения устройству вы используете пакет SDK для службы Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="b9f58-276">If you're sending a message to a device, you would do so through the Azure IoT service SDK.</span></span> <span data-ttu-id="b9f58-277">Вам по-прежнему необходимо знать, какую строку отправить для вызова определенного действия.</span><span class="sxs-lookup"><span data-stu-id="b9f58-277">You still need to know what string to send to invoke a particular action.</span></span> <span data-ttu-id="b9f58-278">Общий формат отправки сообщения выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b9f58-278">The general format for sending a message appears as follows:</span></span>

```
{"Name" : "", "Parameters" : "" }
```

<span data-ttu-id="b9f58-279">Вы отправляете сериализованный объект JSON с двумя свойствами: **Name** (имя действия/сообщения) и **Parameters** (параметры этого действия).</span><span class="sxs-lookup"><span data-stu-id="b9f58-279">You're sending a serialized JSON object with two properties: **Name** is the name of the action (message) and **Parameters** contains the parameters of that action.</span></span>

<span data-ttu-id="b9f58-280">Например, чтобы вызвать функцию **SetAirResistance** , вам нужно отправить устройству следующее сообщение:</span><span class="sxs-lookup"><span data-stu-id="b9f58-280">For example, to invoke **SetAirResistance** you can send this message to a device:</span></span>

```
{"Name" : "SetAirResistance", "Parameters" : { "Position" : 5 }}
```

<span data-ttu-id="b9f58-281">Имя действия должно совпадать с именем, определенным в модели.</span><span class="sxs-lookup"><span data-stu-id="b9f58-281">The action name must exactly match an action defined in your model.</span></span> <span data-ttu-id="b9f58-282">Имена параметров должны совпадать.</span><span class="sxs-lookup"><span data-stu-id="b9f58-282">The parameter names must match as well.</span></span> <span data-ttu-id="b9f58-283">Также обратите внимание на чувствительность к регистру.</span><span class="sxs-lookup"><span data-stu-id="b9f58-283">Also note case sensitivity.</span></span> <span data-ttu-id="b9f58-284">Параметры **Name** и **Parameters** всегда пишутся с прописной буквы.</span><span class="sxs-lookup"><span data-stu-id="b9f58-284">**Name** and **Parameters** are always uppercase.</span></span> <span data-ttu-id="b9f58-285">Также следите за соответствием регистра в именах действий и параметров, определенных в модели.</span><span class="sxs-lookup"><span data-stu-id="b9f58-285">Make sure to match the case of your action name and parameters in your model.</span></span> <span data-ttu-id="b9f58-286">В этом примере действие называется SetAirResistance (не setairresistance).</span><span class="sxs-lookup"><span data-stu-id="b9f58-286">In this example, the action name is "SetAirResistance" and not "setairresistance".</span></span>

<span data-ttu-id="b9f58-287">Два других действия **TurnFanOn** и **TurnFanOff** могут вызываться при отправке этих сообщений на устройство:</span><span class="sxs-lookup"><span data-stu-id="b9f58-287">The two other actions **TurnFanOn** and **TurnFanOff** can be invoked by sending these messages to a device:</span></span>

```
{"Name" : "TurnFanOn", "Parameters" : {}}
{"Name" : "TurnFanOff", "Parameters" : {}}
```

<span data-ttu-id="b9f58-288">Вот и все, что вам нужно знать об отправке событий и получении сообщений с помощью библиотеки **serializer** .</span><span class="sxs-lookup"><span data-stu-id="b9f58-288">This section described everything you need to know when sending events and receiving messages with the **serializer** library.</span></span> <span data-ttu-id="b9f58-289">Прежде чем продолжить, давайте рассмотрим ряд изменяемых параметров, которые позволяют управлять размером модели.</span><span class="sxs-lookup"><span data-stu-id="b9f58-289">Before moving on, let's cover some parameters you can configure that control how large your model is.</span></span>

## <a name="macro-configuration"></a><span data-ttu-id="b9f58-290">Конфигурация макросов</span><span class="sxs-lookup"><span data-stu-id="b9f58-290">Macro configuration</span></span>
<span data-ttu-id="b9f58-291">Если вы используете библиотеку **Serializer** , помните, что нужную вам часть пакета SDK можно найти в библиотеке azure-c-shared-utility.</span><span class="sxs-lookup"><span data-stu-id="b9f58-291">If you’re using the **Serializer** library an important part of the SDK to be aware of is found in the azure-c-shared-utility library.</span></span>
<span data-ttu-id="b9f58-292">Если вы клонировали репозиторий Azure-iot-sdk-с сайта GitHub, использовав параметр --recursive, то эту общедоступную библиотеку служебных программ можно найти здесь:</span><span class="sxs-lookup"><span data-stu-id="b9f58-292">If you have cloned the Azure-iot-sdk-c repository from GitHub using the --recursive option, then you will find this shared utility library here:</span></span>

```
.\\c-utility
```

<span data-ttu-id="b9f58-293">Если вы не клонировали библиотеку, ее можно найти [здесь](https://github.com/Azure/azure-c-shared-utility).</span><span class="sxs-lookup"><span data-stu-id="b9f58-293">If you have not cloned the library, you can find it [here](https://github.com/Azure/azure-c-shared-utility).</span></span>

<span data-ttu-id="b9f58-294">В общедоступной библиотеке служебных программ вы найдете следующую папку:</span><span class="sxs-lookup"><span data-stu-id="b9f58-294">Within the shared utility library, you will find the following folder:</span></span>

```
azure-c-shared-utility\\macro\_utils\_h\_generator.
```

<span data-ttu-id="b9f58-295">Эта папка содержит решение Visual Studio с именем **macro\_utils\_h\_generator.sln**:</span><span class="sxs-lookup"><span data-stu-id="b9f58-295">This folder contains a Visual Studio solution called **macro\_utils\_h\_generator.sln**:</span></span>

  ![](media/iot-hub-device-sdk-c-serializer/01-macro_utils_h_generator.PNG)

<span data-ttu-id="b9f58-296">Программа в этом решении создает файл **macro\_utils.h**.</span><span class="sxs-lookup"><span data-stu-id="b9f58-296">The program in this solution generates the **macro\_utils.h** file.</span></span> <span data-ttu-id="b9f58-297">Вместе с пакетом SDK поставляется стандартная версия файла macro\_utils.h.</span><span class="sxs-lookup"><span data-stu-id="b9f58-297">There’s a default macro\_utils.h file included with the SDK.</span></span> <span data-ttu-id="b9f58-298">Это решение позволяет изменить ряд параметров, а затем повторно создать файл заголовка с учетом этих изменений.</span><span class="sxs-lookup"><span data-stu-id="b9f58-298">This solution allows you to modify some parameters and then recreate the header file based on these parameters.</span></span>

<span data-ttu-id="b9f58-299">Два ключевых параметра, о которых вам нужно знать, это **nArithmetic** и **nMacroParameters**. Они определяются в следующих двух строках кода в файле macro\_utils.tt:</span><span class="sxs-lookup"><span data-stu-id="b9f58-299">The two key parameters to be concerned with are **nArithmetic** and **nMacroParameters** which are defined in these two lines found in macro\_utils.tt:</span></span>

```
<#int nArithmetic=1024;#>
<#int nMacroParameters=124;/*127 parameters in one macro deﬁnition in C99 in chapter 5.2.4.1 Translation limits*/#>

```

<span data-ttu-id="b9f58-300">Эти значения являются стандартными для пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="b9f58-300">These values are the default parameters included with the SDK.</span></span> <span data-ttu-id="b9f58-301">Параметры означают следующее:</span><span class="sxs-lookup"><span data-stu-id="b9f58-301">Each parameter has the following meaning:</span></span>

* <span data-ttu-id="b9f58-302">nMacroParameters — определяет количество параметров в одном определении макроса DECLARE\_MODEL.</span><span class="sxs-lookup"><span data-stu-id="b9f58-302">nMacroParameters – Controls how many parameters you can have in one DECLARE\_MODEL macro definition.</span></span>
* <span data-ttu-id="b9f58-303">nArithmetic — общее разрешенное количество элементов в модели.</span><span class="sxs-lookup"><span data-stu-id="b9f58-303">nArithmetic – Controls the total number of members allowed in a model.</span></span>

<span data-ttu-id="b9f58-304">Важность этих параметров объясняется тем, что с их помощью можно управлять размером модели.</span><span class="sxs-lookup"><span data-stu-id="b9f58-304">The reason these parameters are important is because they control how large your model can be.</span></span> <span data-ttu-id="b9f58-305">Например, возьмем следующее определение модели:</span><span class="sxs-lookup"><span data-stu-id="b9f58-305">For example, consider this model definition:</span></span>

```
DECLARE_MODEL(MyModel,
WITH_DATA(int, MyData)
);
```

<span data-ttu-id="b9f58-306">Как говорилось ранее, **DECLARE\_MODEL** является обычным макросом C.</span><span class="sxs-lookup"><span data-stu-id="b9f58-306">As mentioned previously, **DECLARE\_MODEL** is just a C macro.</span></span> <span data-ttu-id="b9f58-307">Имя модели и инструкция **WITH\_DATA** (еще один макрос) являются параметрами макроса **DECLARE\_MODEL**.</span><span class="sxs-lookup"><span data-stu-id="b9f58-307">The names of the model and the **WITH\_DATA** statement (yet another macro) are parameters of **DECLARE\_MODEL**.</span></span> <span data-ttu-id="b9f58-308">**nMacroParameters** определяет, сколько параметров можно включить в макрос **DECLARE\_MODEL**.</span><span class="sxs-lookup"><span data-stu-id="b9f58-308">**nMacroParameters** defines how many parameters can be included in **DECLARE\_MODEL**.</span></span> <span data-ttu-id="b9f58-309">Фактически этот параметр определяет максимальное количество событий, инициируемых изменением данных, и объявлений действий.</span><span class="sxs-lookup"><span data-stu-id="b9f58-309">Effectively, this defines how many data event and action declarations you can have.</span></span> <span data-ttu-id="b9f58-310">Таким образом, ограничение в 124 элемента означает возможность определения модели, в которой будет приблизительно по 60 действий и событий, инициируемых изменением данных.</span><span class="sxs-lookup"><span data-stu-id="b9f58-310">As such, with the default limit of 124 this means that you can define a model with a combination of about 60 actions and data events.</span></span> <span data-ttu-id="b9f58-311">Если превысить этот предел, вы получите следующую ошибку компиляции:</span><span class="sxs-lookup"><span data-stu-id="b9f58-311">If you try to exceed this limit, you'll receive compiler errors that look similar to this:</span></span>

  ![](media/iot-hub-device-sdk-c-serializer/02-nMacroParametersCompilerErrors.PNG)

<span data-ttu-id="b9f58-312">Параметр **nArithmetic** скорее предназначен для настройки внутренних механизмов макроязыка, чем для работы приложения.</span><span class="sxs-lookup"><span data-stu-id="b9f58-312">The **nArithmetic** parameter is more about the internal workings of the macro language than your application.</span></span>  <span data-ttu-id="b9f58-313">Он определяет общее допустимое количество элементов в модели, включая макрос **DECLARE_STRUCT**.</span><span class="sxs-lookup"><span data-stu-id="b9f58-313">It controls the total number of members you can have in your model, including **DECLARE_STRUCT** macros.</span></span> <span data-ttu-id="b9f58-314">Если при компиляции программы вы получаете подобные сообщения об ошибках, попробуйте увеличить значение **nArithmetic**.</span><span class="sxs-lookup"><span data-stu-id="b9f58-314">If you start seeing compiler errors such as this, then you should try increasing **nArithmetic**:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/03-nArithmeticCompilerErrors.PNG)

<span data-ttu-id="b9f58-315">Чтобы изменить параметры, отредактируйте соответствующие значения в файле macro\_utils.tt. После этого повторно скомпилируйте решение macro\_utils\_h\_generator.sln и запустите скомпилированную программу.</span><span class="sxs-lookup"><span data-stu-id="b9f58-315">If you want to change these parameters, modify the values in the macro\_utils.tt file, recompile the macro\_utils\_h\_generator.sln solution, and run the compiled program.</span></span> <span data-ttu-id="b9f58-316">Будет создан новый файл macro\_utils.h, который помещается в каталог .\\common\\inc.</span><span class="sxs-lookup"><span data-stu-id="b9f58-316">When you do so, a new macro\_utils.h file is generated and placed in the .\\common\\inc directory.</span></span>

<span data-ttu-id="b9f58-317">Чтобы использовать новую версию macro\_utils.h, удалите пакет NuGet **serializer** из решения, заменив его проектом Visual Studio **serializer**.</span><span class="sxs-lookup"><span data-stu-id="b9f58-317">In order to use the new version of macro\_utils.h, remove the **serializer** NuGet package from your solution and in its place include the **serializer** Visual Studio project.</span></span> <span data-ttu-id="b9f58-318">Это позволяет вашему коду выполнить компиляцию для исходного кода библиотеки serializer.</span><span class="sxs-lookup"><span data-stu-id="b9f58-318">This enables your code to compile against the source code of the serializer library.</span></span> <span data-ttu-id="b9f58-319">Сюда входит обновленный macro\_utils.h.</span><span class="sxs-lookup"><span data-stu-id="b9f58-319">This includes the updated macro\_utils.h.</span></span> <span data-ttu-id="b9f58-320">Если необходимо выполнить это действие для **simplesample\_amqp**, следует сначала удалить из решения пакет NuGet для библиотеки serializer:</span><span class="sxs-lookup"><span data-stu-id="b9f58-320">If you want to do this for **simplesample\_amqp**, start by removing the NuGet package for the serializer library from the solution:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/04-serializer-github-package.PNG)

<span data-ttu-id="b9f58-321">Затем добавьте этот проект в свое решение Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="b9f58-321">Then add this project to your Visual Studio solution:</span></span>

> <span data-ttu-id="b9f58-322">.\\c\\serializer\\build\\windows\\serializer.vcxproj</span><span class="sxs-lookup"><span data-stu-id="b9f58-322">.\\c\\serializer\\build\\windows\\serializer.vcxproj</span></span>
> 
> 

<span data-ttu-id="b9f58-323">Когда все будет готово, ваше решение должно выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b9f58-323">When you're done, your solution should look like this:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/05-serializer-project.PNG)

<span data-ttu-id="b9f58-324">Теперь при компиляции решения в двоичный файл будет включен обновленный macro\_utils.h.</span><span class="sxs-lookup"><span data-stu-id="b9f58-324">Now when you compile your solution, the updated macro\_utils.h is included in your binary.</span></span>

<span data-ttu-id="b9f58-325">Обратите внимание, что установка слишком большого значения может привести к превышению ограничений компилятора.</span><span class="sxs-lookup"><span data-stu-id="b9f58-325">Note that increasing these values high enough can exceed compiler limits.</span></span> <span data-ttu-id="b9f58-326">Поэтому лучше сосредоточиться на параметре **nMacroParameters**.</span><span class="sxs-lookup"><span data-stu-id="b9f58-326">To this point, the **nMacroParameters** is the main parameter with which to be concerned.</span></span> <span data-ttu-id="b9f58-327">В спецификации C99 сказано, что в определении макроса допускается не менее 127 параметров.</span><span class="sxs-lookup"><span data-stu-id="b9f58-327">The C99 spec specifies that a minimum of 127 parameters are allowed in a macro definition.</span></span> <span data-ttu-id="b9f58-328">Компилятор Майкрософт точно следует этой спецификации, а также налагает максимальное ограничение в 127 параметров. Поэтому вы не сможете увеличить значение **nMacroParameters** по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="b9f58-328">The Microsoft compiler follows the spec exactly (and has a limit of 127), so you won't be able to increase **nMacroParameters** beyond the default.</span></span> <span data-ttu-id="b9f58-329">Другие компиляторы могут позволить сделать это (например, компилятор GNU поддерживает более высокое ограничение).</span><span class="sxs-lookup"><span data-stu-id="b9f58-329">Other compilers might allow you to do so (for example, the GNU compiler supports a higher limit).</span></span>

<span data-ttu-id="b9f58-330">Таким образом, мы рассмотрели практически все, что нужно знать о написании кода при использовании библиотеки **serializer** .</span><span class="sxs-lookup"><span data-stu-id="b9f58-330">So far we've covered just about everything you need to know about how to write code with the **serializer** library.</span></span> <span data-ttu-id="b9f58-331">Прежде чем закончить, давайте вернемся к некоторым темам из предыдущих статей, которые могут вызвать у вас вопросы.</span><span class="sxs-lookup"><span data-stu-id="b9f58-331">Before concluding, let's revisit some topics from previous articles that you may be wondering about.</span></span>

## <a name="the-lower-level-apis"></a><span data-ttu-id="b9f58-332">Интерфейсы API нижнего уровня</span><span class="sxs-lookup"><span data-stu-id="b9f58-332">The lower-level APIs</span></span>
<span data-ttu-id="b9f58-333">В этой статье мы рассмотрели пример приложения **simplesample\_amqp**.</span><span class="sxs-lookup"><span data-stu-id="b9f58-333">The sample application on which this article focused is **simplesample\_amqp**.</span></span> <span data-ttu-id="b9f58-334">В этом примере для отправки событий и получения сообщений используется API высокого уровня (не LL).</span><span class="sxs-lookup"><span data-stu-id="b9f58-334">This sample uses the higher-level (the non-"LL") APIs to send events and receive messages.</span></span> <span data-ttu-id="b9f58-335">При использовании таких API запускается фоновый поток, который отвечает и за отправку событий, и за получение сообщений.</span><span class="sxs-lookup"><span data-stu-id="b9f58-335">If you use these APIs, a background thread runs which takes care of both sending events and receiving messages.</span></span> <span data-ttu-id="b9f58-336">Однако мы можем использовать API низкого уровня (LL), чтобы остановить этот фоновый поток и явно управлять отправкой событий или получением сообщений из облака.</span><span class="sxs-lookup"><span data-stu-id="b9f58-336">However, you can use the lower-level (LL) APIs to eliminate this background thread and take explicit control over when you send events or receive messages from the cloud.</span></span>

<span data-ttu-id="b9f58-337">Как сказано в [предыдущей статье](iot-hub-device-sdk-c-iothubclient.md), есть набор функций, которые включают в себя интерфейсы API высокого уровня:</span><span class="sxs-lookup"><span data-stu-id="b9f58-337">As described in a [previous article](iot-hub-device-sdk-c-iothubclient.md), there is a set of functions that consists of the higher-level APIs:</span></span>

* <span data-ttu-id="b9f58-338">IoTHubClient\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="b9f58-338">IoTHubClient\_CreateFromConnectionString</span></span>
* <span data-ttu-id="b9f58-339">IoTHubClient\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="b9f58-339">IoTHubClient\_SendEventAsync</span></span>
* <span data-ttu-id="b9f58-340">IoTHubClient\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="b9f58-340">IoTHubClient\_SetMessageCallback</span></span>
* <span data-ttu-id="b9f58-341">IoTHubClient\_Destroy</span><span class="sxs-lookup"><span data-stu-id="b9f58-341">IoTHubClient\_Destroy</span></span>

<span data-ttu-id="b9f58-342">В примере **simplesample\_amqp** показывается, как использовать эти API.</span><span class="sxs-lookup"><span data-stu-id="b9f58-342">These APIs are demonstrated in **simplesample\_amqp**.</span></span>

<span data-ttu-id="b9f58-343">Существует аналогичный набор API низкого уровня.</span><span class="sxs-lookup"><span data-stu-id="b9f58-343">There is also an analogous set of lower-level APIs.</span></span>

* <span data-ttu-id="b9f58-344">IoTHubClient\_LL\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="b9f58-344">IoTHubClient\_LL\_CreateFromConnectionString</span></span>
* <span data-ttu-id="b9f58-345">IoTHubClient\_LL\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="b9f58-345">IoTHubClient\_LL\_SendEventAsync</span></span>
* <span data-ttu-id="b9f58-346">IoTHubClient\_LL\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="b9f58-346">IoTHubClient\_LL\_SetMessageCallback</span></span>
* <span data-ttu-id="b9f58-347">IoTHubClient\_LL\_Destroy</span><span class="sxs-lookup"><span data-stu-id="b9f58-347">IoTHubClient\_LL\_Destroy</span></span>

<span data-ttu-id="b9f58-348">Обратите внимание, что API низкого уровня работают точно так же, как это описано в предыдущих статьях.</span><span class="sxs-lookup"><span data-stu-id="b9f58-348">Note that the lower-level APIs work exactly the same way as described in the previous articles.</span></span> <span data-ttu-id="b9f58-349">Первый набор API используется, когда вам нужно управлять операциями отправки событий и получения сообщений с помощью фонового потока.</span><span class="sxs-lookup"><span data-stu-id="b9f58-349">You can use the first set of APIs if you want a background thread to handle sending events and receiving messages.</span></span> <span data-ttu-id="b9f58-350">Но если вы хотите явно управлять отправкой и получением данных из центра IoT, вам следует использовать второй набор API.</span><span class="sxs-lookup"><span data-stu-id="b9f58-350">You use the second set of APIs if you want explicit control over when you send and receive data from IoT Hub.</span></span> <span data-ttu-id="b9f58-351">Любой из этих наборов API работает с библиотекой **serializer** одинаково хорошо.</span><span class="sxs-lookup"><span data-stu-id="b9f58-351">Either set of APIs work equally well with the **serializer** library.</span></span>

<span data-ttu-id="b9f58-352">Пример использования интерфейсов API низкого уровня с библиотекой **serializer** см. в приложении **simplesample\_http**.</span><span class="sxs-lookup"><span data-stu-id="b9f58-352">For an example of how the lower-level APIs are used with the **serializer** library, see the **simplesample\_http** application.</span></span>

## <a name="additional-topics"></a><span data-ttu-id="b9f58-353">Дополнительные разделы</span><span class="sxs-lookup"><span data-stu-id="b9f58-353">Additional topics</span></span>
<span data-ttu-id="b9f58-354">Также стоит упомянуть об обработке свойств, параметрах конфигурации и использовании дополнительных учетных данных устройства.</span><span class="sxs-lookup"><span data-stu-id="b9f58-354">A few other topics worth mentioning again are property handling, using alternate device credentials, and configuration options.</span></span> <span data-ttu-id="b9f58-355">Все эти вопросы рассматриваются в [предыдущей статье](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="b9f58-355">These are all topics covered in a [previous article](iot-hub-device-sdk-c-iothubclient.md).</span></span> <span data-ttu-id="b9f58-356">Самое главное, что все эти возможности работают при использовании библиотеки **serializer** точно так же, как и при использовании библиотеки **IoTHubClient**.</span><span class="sxs-lookup"><span data-stu-id="b9f58-356">The main point is that all of these features work in the same way with the **serializer** library as they do with the **IoTHubClient** library.</span></span> <span data-ttu-id="b9f58-357">Например, если вы хотите присоединить свойства к событию из модели, вы можете воспользоваться функциями **IoTHubMessage\_Properties** и **Map**\_**AddorUpdate** в соответствии с описанием выше.</span><span class="sxs-lookup"><span data-stu-id="b9f58-357">For example, if you want to attach properties to an event from your model, you use **IoTHubMessage\_Properties** and **Map**\_**AddorUpdate**, the same way as described previously:</span></span>

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

<span data-ttu-id="b9f58-358">Не имеет значения, было ли создано событие вручную с помощью библиотеки **IoTHubClient** или автоматически с помощью библиотеки **serializer**.</span><span class="sxs-lookup"><span data-stu-id="b9f58-358">Whether the event was generated from the **serializer** library or created manually using the **IoTHubClient** library does not matter.</span></span>

<span data-ttu-id="b9f58-359">В случае с дополнительными учетными данными для устройства функция **IoTHubClient\_LL\_Create** для выделения **IOTHUB\_CLIENT\_HANDLE** работает точно так же, как функция **IoTHubClient\_CreateFromConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="b9f58-359">For the alternate device credentials, using **IoTHubClient\_LL\_Create** works just as well as **IoTHubClient\_CreateFromConnectionString** for allocating an **IOTHUB\_CLIENT\_HANDLE**.</span></span>

<span data-ttu-id="b9f58-360">Наконец, используя библиотеку **serializer**, вы можете настраивать параметры конфигурации с помощью функции **IoTHubClient\_LL\_SetOption** точно так же, как при использовании библиотеки **IoTHubClient**.</span><span class="sxs-lookup"><span data-stu-id="b9f58-360">Finally, if you're using the **serializer** library, you can set configuration options with **IoTHubClient\_LL\_SetOption** just as you did when using the **IoTHubClient** library.</span></span>

<span data-ttu-id="b9f58-361">Единственным отличием возможностей библиотеки **serializer** является наличие API-интерфейсов инициализации.</span><span class="sxs-lookup"><span data-stu-id="b9f58-361">A feature that is unique to the **serializer** library are the initialization APIs.</span></span> <span data-ttu-id="b9f58-362">Перед началом работы с библиотекой необходимо вызвать **serializer\_init**:</span><span class="sxs-lookup"><span data-stu-id="b9f58-362">Before you can start working with the library, you must call **serializer\_init**:</span></span>

```
serializer_init(NULL);
```

<span data-ttu-id="b9f58-363">Это делается непосредственно перед вызовом метода **IoTHubClient\_CreateFromConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="b9f58-363">This is done just before you call **IoTHubClient\_CreateFromConnectionString**.</span></span>

<span data-ttu-id="b9f58-364">Соответственно, после завершения работы с библиотекой вызывается метод **serializer\_deinit**:</span><span class="sxs-lookup"><span data-stu-id="b9f58-364">Similarly, when you're done working with the library, the last call you’ll make is to **serializer\_deinit**:</span></span>

```
serializer_deinit();
```

<span data-ttu-id="b9f58-365">Все прочие описанные выше функции работают с библиотекой **serializer** точно так же, как и с библиотекой **IoTHubClient**.</span><span class="sxs-lookup"><span data-stu-id="b9f58-365">Otherwise, all of the other features listed above work the same in the **serializer** library as they do in the **IoTHubClient** library.</span></span> <span data-ttu-id="b9f58-366">Дополнительные сведения см. в [предыдущей статье](iot-hub-device-sdk-c-iothubclient.md) этого цикла.</span><span class="sxs-lookup"><span data-stu-id="b9f58-366">For more information about any of these topics, see the [previous article](iot-hub-device-sdk-c-iothubclient.md) in this series.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b9f58-367">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b9f58-367">Next steps</span></span>
<span data-ttu-id="b9f58-368">В этой статье подробно рассматриваются уникальные возможности библиотеки **serializer**, включенной в **пакет SDK для устройств Azure IoT для C**. Прочитав эту статью, вы узнаете, как использовать модели для отправки событий и получения сообщений из центра IoT.</span><span class="sxs-lookup"><span data-stu-id="b9f58-368">This article describes in detail the unique aspects of the **serializer** library contained in the **Azure IoT device SDK for C**. With the information provided you should have a good understanding of how to use models to send events and receive messages from IoT Hub.</span></span>

<span data-ttu-id="b9f58-369">Эта статья завершает цикл из трех частей, посвященный разработке приложений с помощью **пакета SDK для устройств Azure IoT для C**. Приведенной информации должно быть достаточно для того, чтобы вы могли не только приступить к работе, но и лучше понять принципы работы API.</span><span class="sxs-lookup"><span data-stu-id="b9f58-369">This also concludes the three-part series on how to develop applications with the **Azure IoT device SDK for C**. This should be enough information to not only get you started but give you a thorough understanding of how the APIs work.</span></span> <span data-ttu-id="b9f58-370">Дополнительные сведения можно получить из нескольких примеров в пакете SDK, не описанных в этой статье.</span><span class="sxs-lookup"><span data-stu-id="b9f58-370">For additional information, there are a few samples in the SDK not covered here.</span></span> <span data-ttu-id="b9f58-371">Еще одним источником дополнительной информации является [документация по пакету SDK](https://github.com/Azure/azure-iot-sdk-c) .</span><span class="sxs-lookup"><span data-stu-id="b9f58-371">Otherwise, the [SDK documentation](https://github.com/Azure/azure-iot-sdk-c) is a good resource for additional information.</span></span>

<span data-ttu-id="b9f58-372">Дополнительные сведения о разработке для Центра Интернета вещей см. в статье [Пакеты SDK для центра IoT][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="b9f58-372">To learn more about developing for IoT Hub, see the [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="b9f58-373">Для дальнейшего изучения возможностей центра IoT см. следующие статьи:</span><span class="sxs-lookup"><span data-stu-id="b9f58-373">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="b9f58-374">[Отправка сообщений с устройства в облако с помощью имитации устройства (Linux) с использованием Edge Интернета вещей Azure][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="b9f58-374">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
