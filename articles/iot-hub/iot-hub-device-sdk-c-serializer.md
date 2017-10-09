---
title: "устройств IoT aaaAzure пакета SDK для C — сериализатор | Документы Microsoft"
description: "Как toouse hello сериализатор библиотеки в пакет SDK устройства Azure IoT hello C toocreate для приложений для устройств, которые взаимодействуют с центра IoT."
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
ms.openlocfilehash: c5776e9b50ffea71df96cb2d342ea2fc045f5a0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-device-sdk-for-c--more-about-serializer"></a><span data-ttu-id="8dbe6-103">Пакет SDK для устройств Azure IoT для C — дополнительные сведения о сериализаторе</span><span class="sxs-lookup"><span data-stu-id="8dbe6-103">Azure IoT device SDK for C – more about serializer</span></span>
<span data-ttu-id="8dbe6-104">Hello [сначала статьи](iot-hub-device-sdk-c-intro.md) в этой серии появился hello **устройств Azure IoT SDK для C**. hello следующей статье содержатся более подробное описание hello [ **IoTHubClient** ](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="8dbe6-104">hello [first article](iot-hub-device-sdk-c-intro.md) in this series introduced hello **Azure IoT device SDK for C**. hello next article provided a more detailed description of hello [**IoTHubClient**](iot-hub-device-sdk-c-iothubclient.md).</span></span> <span data-ttu-id="8dbe6-105">В этой статье завершения покрытие hello SDK, предоставляя более подробное описание hello оставшихся компонента: hello **сериализатор** библиотеки.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-105">This article completes coverage of hello SDK by providing a more detailed description of hello remaining component: hello **serializer** library.</span></span>

<span data-ttu-id="8dbe6-106">описано, каким образом вводная статья Hello toouse hello **сериализатор** библиотеки toosend события tooand получать сообщения от центра IoT.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-106">hello introductory article described how toouse hello **serializer** library toosend events tooand receive messages from IoT Hub.</span></span> <span data-ttu-id="8dbe6-107">В этой статье мы расширяют обсуждение этой темы, предоставляя более подробное описание того, как toomodel данных с помощью hello **сериализатор** макрос языка.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-107">In this article, we extend that discussion by providing a more complete explanation of how toomodel your data with hello **serializer** macro language.</span></span> <span data-ttu-id="8dbe6-108">статья Hello также включает более подробные сведения о как библиотека hello сериализацию сообщений (и в некоторых случаях способы управления поведением при сериализации hello).</span><span class="sxs-lookup"><span data-stu-id="8dbe6-108">hello article also includes more detail about how hello library serializes messages (and in some cases how you can control hello serialization behavior).</span></span> <span data-ttu-id="8dbe6-109">Также мы опишем некоторые, можно изменить параметры, определяющие размер hello создаваемые модели hello.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-109">We'll also describe some parameters you can modify that determine hello size of hello models you create.</span></span>

<span data-ttu-id="8dbe6-110">Наконец некоторые разделы, описанные в предыдущих статей, такие как сообщения и обработка свойство последующих посещениях hello статьи.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-110">Finally, hello article revisits some topics covered in previous articles such as message and property handling.</span></span> <span data-ttu-id="8dbe6-111">Как мы объясним, такие рабочие функции в hello же с помощью hello **сериализатор** библиотеки, как с hello **IoTHubClient** библиотеки.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-111">As we'll find out, those features work in hello same way using hello **serializer** library as they do with hello **IoTHubClient** library.</span></span>

<span data-ttu-id="8dbe6-112">Все описанные в этой статье основан на hello **сериализатор** образцов SDK.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-112">Everything described in this article is based on hello **serializer** SDK samples.</span></span> <span data-ttu-id="8dbe6-113">Следует toofollow вдоль разделе hello **simplesample\_amqp** и **simplesample\_http** приложений, включенных в пакет SDK устройства Azure IoT hello C.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-113">If you want toofollow along, see hello **simplesample\_amqp** and **simplesample\_http** applications included in hello Azure IoT device SDK for C.</span></span>

<span data-ttu-id="8dbe6-114">Можно найти hello [ **устройств Azure IoT SDK для C** ](https://github.com/Azure/azure-iot-sdk-c) GitHub репозитория и просмотра сведений из hello API в hello [Справочник по C API](https://azure.github.io/azure-iot-sdk-c/index.html).</span><span class="sxs-lookup"><span data-stu-id="8dbe6-114">You can find hello [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of hello API in hello [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

## <a name="hello-modeling-language"></a><span data-ttu-id="8dbe6-115">языка моделирования Hello</span><span class="sxs-lookup"><span data-stu-id="8dbe6-115">hello modeling language</span></span>
<span data-ttu-id="8dbe6-116">Hello [вводной статье](iot-hub-device-sdk-c-intro.md) в этой серии появился hello **устройств Azure IoT SDK для C** язык через hello примера, приведенного в hello моделирования **simplesample\_amqp**  приложения:</span><span class="sxs-lookup"><span data-stu-id="8dbe6-116">hello [introductory article](iot-hub-device-sdk-c-intro.md) in this series introduced hello **Azure IoT device SDK for C** modeling language through hello example provided in hello **simplesample\_amqp** application:</span></span>

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

<span data-ttu-id="8dbe6-117">Как видите, язык моделирования hello основан на макросов C.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-117">As you can see, hello modeling language is based on C macros.</span></span> <span data-ttu-id="8dbe6-118">Определение всегда начинается с ключевого слова **BEGIN\_NAMESPACE** и всегда заканчивается ключевым словом **END\_NAMESPACE**.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-118">You always begin your definition with **BEGIN\_NAMESPACE** and always end with **END\_NAMESPACE**.</span></span> <span data-ttu-id="8dbe6-119">Это общее tooname hello пространство имен для вашей компании или, как в этом примере hello проекта, над которыми вы работаете.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-119">It's common tooname hello namespace for your company or, as in this example, hello project that you're working on.</span></span>

<span data-ttu-id="8dbe6-120">Что происходит внутри пространства имен hello, определения модели.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-120">What goes inside hello namespace are model definitions.</span></span> <span data-ttu-id="8dbe6-121">В данном случае создается одна модель для анемометра.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-121">In this case, there is a single model for an anemometer.</span></span> <span data-ttu-id="8dbe6-122">Опять же, hello модели можно присвоить любое имя, но обычно это имя для устройства hello или тип данных требуется tooexchange с центром IoT.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-122">Once again, hello model can be named anything, but typically this is named for hello device or type of data you want tooexchange with IoT Hub.</span></span>  

<span data-ttu-id="8dbe6-123">Модели содержат определение hello событий можно tooIoT входящих концентратора (hello *данные*) а также можно получать из центра IoT сообщений hello (hello *действия*).</span><span class="sxs-lookup"><span data-stu-id="8dbe6-123">Models contain a definition of hello events you can ingress tooIoT Hub (hello *data*) as well as hello messages you can receive from IoT Hub (hello *actions*).</span></span> <span data-ttu-id="8dbe6-124">Как видно из примера hello события имеют типом и именем. действия есть имя и необязательные параметры (каждый с типом).</span><span class="sxs-lookup"><span data-stu-id="8dbe6-124">As you can see from hello example, events have a type and a name; actions have a name and optional parameters (each with a type).</span></span>

<span data-ttu-id="8dbe6-125">При этом не демонстрируется в данном примере — дополнительные типы данных, поддерживаемые hello SDK.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-125">What’s not demonstrated in this sample are additional data types that are supported by hello SDK.</span></span> <span data-ttu-id="8dbe6-126">Об этом мы поговорим далее.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-126">We'll cover that next.</span></span>

> [!NOTE]
> <span data-ttu-id="8dbe6-127">Центр IoT ссылается устройство отправляет tooit как данные toohello *события*, в то время язык моделирования hello ссылается tooit как *данные* (определяются с помощью **WITH_DATA**).</span><span class="sxs-lookup"><span data-stu-id="8dbe6-127">IoT Hub refers toohello data a device sends tooit as *events*, while hello modeling language refers tooit as *data* (defined using **WITH_DATA**).</span></span> <span data-ttu-id="8dbe6-128">Аналогично, центр IoT ссылается toohello данных, отправляемых toodevices как *сообщений*, в то время язык моделирования hello ссылается tooit как *действия* (определяются с помощью **WITH_ACTION**).</span><span class="sxs-lookup"><span data-stu-id="8dbe6-128">Likewise, IoT Hub refers toohello data you send toodevices as *messages*, while hello modeling language refers tooit as *actions* (defined using **WITH_ACTION**).</span></span> <span data-ttu-id="8dbe6-129">Помните, что в этой статье данные понятия могут быть взаимозаменяемыми.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-129">Be aware that these terms may be used interchangeably in this article.</span></span>
> 
> 

### <a name="supported-data-types"></a><span data-ttu-id="8dbe6-130">Поддерживаемые типы данных.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-130">Supported data types</span></span>
<span data-ttu-id="8dbe6-131">Привет, следующие типы данных поддерживаются в модели, созданные с помощью hello **сериализатор** библиотеки:</span><span class="sxs-lookup"><span data-stu-id="8dbe6-131">hello following data types are supported in models created with hello **serializer** library:</span></span>

| <span data-ttu-id="8dbe6-132">Тип</span><span class="sxs-lookup"><span data-stu-id="8dbe6-132">Type</span></span> | <span data-ttu-id="8dbe6-133">Описание</span><span class="sxs-lookup"><span data-stu-id="8dbe6-133">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8dbe6-134">double</span><span class="sxs-lookup"><span data-stu-id="8dbe6-134">double</span></span> |<span data-ttu-id="8dbe6-135">число с плавающей запятой двойной точности</span><span class="sxs-lookup"><span data-stu-id="8dbe6-135">double precision floating point number</span></span> |
| <span data-ttu-id="8dbe6-136">int</span><span class="sxs-lookup"><span data-stu-id="8dbe6-136">int</span></span> |<span data-ttu-id="8dbe6-137">32-разрядное целое число</span><span class="sxs-lookup"><span data-stu-id="8dbe6-137">32 bit integer</span></span> |
| <span data-ttu-id="8dbe6-138">float;</span><span class="sxs-lookup"><span data-stu-id="8dbe6-138">float</span></span> |<span data-ttu-id="8dbe6-139">число с плавающей запятой одиночной точности</span><span class="sxs-lookup"><span data-stu-id="8dbe6-139">single precision floating point number</span></span> |
| <span data-ttu-id="8dbe6-140">длинное целое число</span><span class="sxs-lookup"><span data-stu-id="8dbe6-140">long</span></span> |<span data-ttu-id="8dbe6-141">длинное целое число</span><span class="sxs-lookup"><span data-stu-id="8dbe6-141">long integer</span></span> |
| <span data-ttu-id="8dbe6-142">int8\_t</span><span class="sxs-lookup"><span data-stu-id="8dbe6-142">int8\_t</span></span> |<span data-ttu-id="8dbe6-143">8-разрядное целое число</span><span class="sxs-lookup"><span data-stu-id="8dbe6-143">8 bit integer</span></span> |
| <span data-ttu-id="8dbe6-144">int16\_t</span><span class="sxs-lookup"><span data-stu-id="8dbe6-144">int16\_t</span></span> |<span data-ttu-id="8dbe6-145">16-разрядное целое число</span><span class="sxs-lookup"><span data-stu-id="8dbe6-145">16 bit integer</span></span> |
| <span data-ttu-id="8dbe6-146">int32\_t</span><span class="sxs-lookup"><span data-stu-id="8dbe6-146">int32\_t</span></span> |<span data-ttu-id="8dbe6-147">32-разрядное целое число</span><span class="sxs-lookup"><span data-stu-id="8dbe6-147">32 bit integer</span></span> |
| <span data-ttu-id="8dbe6-148">int64\_t</span><span class="sxs-lookup"><span data-stu-id="8dbe6-148">int64\_t</span></span> |<span data-ttu-id="8dbe6-149">64-разрядное целое число</span><span class="sxs-lookup"><span data-stu-id="8dbe6-149">64 bit integer</span></span> |
| <span data-ttu-id="8dbe6-150">bool</span><span class="sxs-lookup"><span data-stu-id="8dbe6-150">bool</span></span> |<span data-ttu-id="8dbe6-151">Логическое</span><span class="sxs-lookup"><span data-stu-id="8dbe6-151">boolean</span></span> |
| <span data-ttu-id="8dbe6-152">ascii\_char\_ptr</span><span class="sxs-lookup"><span data-stu-id="8dbe6-152">ascii\_char\_ptr</span></span> |<span data-ttu-id="8dbe6-153">строка ASCII</span><span class="sxs-lookup"><span data-stu-id="8dbe6-153">ASCII string</span></span> |
| <span data-ttu-id="8dbe6-154">EDM\_DATE\_TIME\_OFFSET</span><span class="sxs-lookup"><span data-stu-id="8dbe6-154">EDM\_DATE\_TIME\_OFFSET</span></span> |<span data-ttu-id="8dbe6-155">смещение даты и времени</span><span class="sxs-lookup"><span data-stu-id="8dbe6-155">date time offset</span></span> |
| <span data-ttu-id="8dbe6-156">EDM\_GUID</span><span class="sxs-lookup"><span data-stu-id="8dbe6-156">EDM\_GUID</span></span> |<span data-ttu-id="8dbe6-157">GUID</span><span class="sxs-lookup"><span data-stu-id="8dbe6-157">GUID</span></span> |
| <span data-ttu-id="8dbe6-158">EDM\_BINARY</span><span class="sxs-lookup"><span data-stu-id="8dbe6-158">EDM\_BINARY</span></span> |<span data-ttu-id="8dbe6-159">binary;</span><span class="sxs-lookup"><span data-stu-id="8dbe6-159">binary</span></span> |
| <span data-ttu-id="8dbe6-160">DECLARE\_STRUCT</span><span class="sxs-lookup"><span data-stu-id="8dbe6-160">DECLARE\_STRUCT</span></span> |<span data-ttu-id="8dbe6-161">сложный тип данных</span><span class="sxs-lookup"><span data-stu-id="8dbe6-161">complex data type</span></span> |

<span data-ttu-id="8dbe6-162">Давайте начнем с типом данных последнего hello.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-162">Let’s start with hello last data type.</span></span> <span data-ttu-id="8dbe6-163">Hello **DECLARE\_СТРУКТУРЫ** позволяет toodefine сложные типы данных, которые группируют hello других типов-примитивов.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-163">hello **DECLARE\_STRUCT** allows you toodefine complex data types, which are groupings of hello other primitive types.</span></span> <span data-ttu-id="8dbe6-164">Такие группы позволяют нам toodefine модель, которая выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="8dbe6-164">These groupings allow us toodefine a model that looks like this:</span></span>

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

<span data-ttu-id="8dbe6-165">Наша модель содержит одно событие, инициируемое изменением данных, типа **TestType**.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-165">Our model contains a single data event of type **TestType**.</span></span> <span data-ttu-id="8dbe6-166">**TestType** — это сложный тип, который включает в себя несколько элементов, которые вместе демонстрируют hello примитивные типы, поддерживаемые hello **сериализатор** язык моделирования.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-166">**TestType** is a complex type that includes several members, which collectively demonstrate hello primitive types supported by hello **serializer** modeling language.</span></span>

<span data-ttu-id="8dbe6-167">С моделью следующим образом можно написать код toosend данных tooIoT концентратор, который выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="8dbe6-167">With a model like this, we can write code toosend data tooIoT Hub that appears as follows:</span></span>

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

<span data-ttu-id="8dbe6-168">По сути, назначение значение tooevery членом hello **теста** структуры и последующего вызова **SendAsync** toosend hello **тест** облако toohello данных события.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-168">Basically, we’re assigning a value tooevery member of hello **Test** structure and then calling **SendAsync** toosend hello **Test** data event toohello cloud.</span></span> <span data-ttu-id="8dbe6-169">**SendAsync** является вспомогательная функция, которая отправляет одно событие tooIoT концентратора:</span><span class="sxs-lookup"><span data-stu-id="8dbe6-169">**SendAsync** is a helper function that sends a single data event tooIoT Hub:</span></span>

```
void SendAsync(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const void *dataEvent)
{
    unsigned char* destination;
    size_t destinationSize;
    if (SERIALIZE(&destination, &destinationSize, *(const unsigned char*)dataEvent) ==
    {
        // null terminate hello string
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

<span data-ttu-id="8dbe6-170">Эта функция сериализует заданное событие данных hello и отправляет его tooIoT концентратора с помощью **IoTHubClient\_SendEventAsync**.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-170">This function serializes hello given data event and sends it tooIoT Hub using **IoTHubClient\_SendEventAsync**.</span></span> <span data-ttu-id="8dbe6-171">Это hello того же кода описано в предыдущей статьи (**SendAsync** инкапсулирует логику hello в удобном функцию).</span><span class="sxs-lookup"><span data-stu-id="8dbe6-171">This is hello same code discussed in previous articles (**SendAsync** encapsulates hello logic into a convenient function).</span></span>

<span data-ttu-id="8dbe6-172">— Одна вспомогательная функция, используемый в предыдущем примере кода hello **GetDateTimeOffset**.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-172">One other helper function used in hello previous code is **GetDateTimeOffset**.</span></span> <span data-ttu-id="8dbe6-173">Эта функция преобразует hello конкретный момент времени в значение типа **EDM\_даты\_время\_СМЕЩЕНИЕ**:</span><span class="sxs-lookup"><span data-stu-id="8dbe6-173">This function transforms hello given time into a value of type **EDM\_DATE\_TIME\_OFFSET**:</span></span>

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

<span data-ttu-id="8dbe6-174">При выполнении этого кода hello сообщением отправляется tooIoT концентратора.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-174">If you run this code, hello following message is sent tooIoT Hub:</span></span>

```
{"aDouble":1.100000000000000, "aInt":2, "aFloat":3.000000, "aLong":4, "aInt8":5, "auInt8":6, "aInt16":7, "aInt32":8, "aInt64":9, "aBool":true, "aAsciiCharPtr":"ascii string 1", "aDateTimeOffset":"2015-09-14T21:18:21Z", "aGuid":"00010203-0405-0607-0809-0A0B0C0D0E0F", "aBinary":"AQID"}
```

<span data-ttu-id="8dbe6-175">Обратите внимание, что hello сериализации JSON, создаваемых hello формата hello по **сериализатор** библиотеки.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-175">Note that hello serialization is JSON, which is hello format generated by hello **serializer** library.</span></span> <span data-ttu-id="8dbe6-176">Также Обратите внимание, что каждый член hello сериализованный объект JSON соответствует hello члены hello **TestType** , определенный в нашей модели.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-176">Also note that each member of hello serialized JSON object matches hello members of hello **TestType** that we defined in our model.</span></span> <span data-ttu-id="8dbe6-177">значения Hello также совпадать тех, которые используются в коде hello.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-177">hello values also exactly match those used in hello code.</span></span> <span data-ttu-id="8dbe6-178">Тем не менее, обратите внимание, что hello двоичных данных в base64-кодировке: «AQID» Здравствуйте, кодирование base64 {0x01, 0x02, 0x03}.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-178">However, note that hello binary data is base64-encoded: "AQID" is hello base64 encoding of {0x01, 0x02, 0x03}.</span></span>

<span data-ttu-id="8dbe6-179">В этом примере демонстрируется hello преимуществом использования hello **сериализатор** библиотеки — это позволяет нам облака toohello toosend JSON, без необходимости иметь дело с сериализацией, в нашем приложении tooexplicitly.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-179">This example demonstrates hello advantage of using hello **serializer** library -- it enables us toosend JSON toohello cloud, without having tooexplicitly deal with serialization in our application.</span></span> <span data-ttu-id="8dbe6-180">Все, что у нас есть tooworry о устанавливать значения hello hello событий данных в нашей модели и затем вызвать простой API-интерфейсы toosend облака toohello этих событий.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-180">All we have tooworry about is setting hello values of hello data events in our model and then calling simple APIs toosend those events toohello cloud.</span></span>

<span data-ttu-id="8dbe6-181">Эти сведения позволяют определить модели, которые включают hello диапазон поддерживаемых типов данных, включая сложные типы (мы может даже содержать сложные типы в других сложных типов).</span><span class="sxs-lookup"><span data-stu-id="8dbe6-181">With this information, we can define models that include hello range of supported data types, including complex types (we could even include complex types within other complex types).</span></span> <span data-ttu-id="8dbe6-182">Тем не менее, он сериализации JSON, созданная по hello приведенном выше примере появится важное правило.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-182">However, he serialized JSON generated by hello example above brings up an important point.</span></span> <span data-ttu-id="8dbe6-183">*Как* мы отправлять данные с hello **сериализатор** библиотека определяет точно, как сформировано hello JSON.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-183">*How* we send data with hello **serializer** library determines exactly how hello JSON is formed.</span></span> <span data-ttu-id="8dbe6-184">Об этом моменте мы поговорим далее.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-184">That particular point is what we'll cover next.</span></span>

## <a name="more-about-serialization"></a><span data-ttu-id="8dbe6-185">Дополнительные сведения о сериализации</span><span class="sxs-lookup"><span data-stu-id="8dbe6-185">More about serialization</span></span>
<span data-ttu-id="8dbe6-186">Пример hello выходных hello выделяет Hello предыдущего раздела **сериализатор** библиотеки.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-186">hello previous section highlights an example of hello output generated by hello **serializer** library.</span></span> <span data-ttu-id="8dbe6-187">В этом разделе объясняется, как библиотека hello сериализует данные и как можно контролировать это поведение, используя hello сериализацией API.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-187">In this section, we'll explain how hello library serializes data and how you can control that behavior using hello serialization APIs.</span></span>

<span data-ttu-id="8dbe6-188">При обсуждении hello tooadvance порядок сериализации мы будем работать с учетом термостат новой модели.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-188">In order tooadvance hello discussion on serialization, we'll work with a new model based on a thermostat.</span></span> <span data-ttu-id="8dbe6-189">Во-первых давайте предоставит некоторые сведения в сценарии hello пытаетесь tooaddress.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-189">First, let's provide some background on hello scenario we're trying tooaddress.</span></span>

<span data-ttu-id="8dbe6-190">Мы хотим toomodel термостат, что меры, температуры и влажности.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-190">We want toomodel a thermostat that measures temperature and humidity.</span></span> <span data-ttu-id="8dbe6-191">Каждый фрагмент данных будет отправлено tooIoT концентратора по-разному toobe.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-191">Each piece of data is going toobe sent tooIoT Hub differently.</span></span> <span data-ttu-id="8dbe6-192">По умолчанию hello термостат ingresses событий температуры каждые 2 минуты; событие влажности ingressed каждые 15 минут.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-192">By default, hello thermostat ingresses a temperature event once every 2 minutes; a humidity event is ingressed once every 15 minutes.</span></span> <span data-ttu-id="8dbe6-193">После любого события ingressed, он должен содержать отметку времени, показывающий время hello соответствующего температура hello или измерялась влажности.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-193">When either event is ingressed, it must include a timestamp that shows hello time that hello corresponding temperature or humidity was measured.</span></span>

<span data-ttu-id="8dbe6-194">Это позволит мы продемонстрируем данных hello toomodel двумя различными способами и мы расскажем hello эффект, что моделирования на hello сериализации выходных данных.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-194">Given this scenario, we'll demonstrate two different ways toomodel hello data, and we'll explain hello effect that modeling has on hello serialized output.</span></span>

### <a name="model-1"></a><span data-ttu-id="8dbe6-195">Модель 1</span><span class="sxs-lookup"><span data-stu-id="8dbe6-195">Model 1</span></span>
<span data-ttu-id="8dbe6-196">Вот hello первой версии модели, поддерживает hello предыдущего сценария.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-196">Here's hello first version of a model that supports hello previous scenario:</span></span>

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

<span data-ttu-id="8dbe6-197">Обратите внимание, что hello модель включает в себя два события данных: **температуры** и **влажность**.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-197">Note that hello model includes two data events: **Temperature** and **Humidity**.</span></span> <span data-ttu-id="8dbe6-198">В отличие от предыдущих примерах hello тип каждого события — это структура, определенная с помощью **DECLARE\_СТРУКТУРЫ**.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-198">Unlike previous examples, hello type of each event is a structure defined using **DECLARE\_STRUCT**.</span></span> <span data-ttu-id="8dbe6-199">Структура **TemperatureEvent** содержит значение измеренной температуры и метку времени, а структура **HumidityEvent** — значение измеренной влажности и метку времени.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-199">**TemperatureEvent** includes a temperature measurement and a timestamp; **HumidityEvent** contains a humidity measurement and a timestamp.</span></span> <span data-ttu-id="8dbe6-200">Эта модель дает нам данных Здравствуй естественным способом toomodel для hello сценария, описанных выше.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-200">This model gives us a natural way toomodel hello data for hello scenario described above.</span></span> <span data-ttu-id="8dbe6-201">Когда мы отправляем в облаке toohello события, либо мы будем отправлять температуры или отметки времени или пару влажности или отметки времени.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-201">When we send an event toohello cloud, we'll either send a temperature/timestamp or a humidity/timestamp pair.</span></span>

<span data-ttu-id="8dbe6-202">Мы можем отправить toohello облака температуры событий с помощью кода, подобного hello далее:</span><span class="sxs-lookup"><span data-stu-id="8dbe6-202">We can send a temperature event toohello cloud using code such as hello following:</span></span>

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

<span data-ttu-id="8dbe6-203">Мы рассмотрим использовать жестко запрограммированные значения температуры и влажности в примере кода hello, но Предположим, что мы фактически извлекаются эти значения с помощью выборки hello соответствующего датчиков термостат hello.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-203">We'll use hard-coded values for temperature and humidity in hello sample code, but imagine that we’re actually retrieving these values by sampling hello corresponding sensors on hello thermostat.</span></span>

<span data-ttu-id="8dbe6-204">Приведенный выше код Hello использует hello **GetDateTimeOffset** помощник, который был введен ранее.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-204">hello code above uses hello **GetDateTimeOffset** helper that was introduced previously.</span></span> <span data-ttu-id="8dbe6-205">По причинам, которые станут снимите более поздней версии этот код явным образом разделяет задачу hello сериализации и отправлять события hello.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-205">For reasons that will become clear later, this code explicitly separates hello task of serializing and sending hello event.</span></span> <span data-ttu-id="8dbe6-206">Hello предыдущий код сериализует событие температуры hello в буфер.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-206">hello previous code serializes hello temperature event into a buffer.</span></span> <span data-ttu-id="8dbe6-207">Затем **sendMessage** — это вспомогательная функция (включен в **simplesample\_amqp**), отправляет hello tooIoT события концентратора:</span><span class="sxs-lookup"><span data-stu-id="8dbe6-207">Then, **sendMessage** is a helper function (included in **simplesample\_amqp**) that sends hello event tooIoT Hub:</span></span>

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

<span data-ttu-id="8dbe6-208">Этот код является подмножеством hello **SendAsync** вспомогательный, описанные в предыдущем разделе hello, поэтому мы не будем останавливаться на него еще раз здесь.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-208">This code is a subset of hello **SendAsync** helper described in hello previous section, so we won’t go over it again here.</span></span>

<span data-ttu-id="8dbe6-209">При запуске hello предыдущего кода toosend hello температуры события, это сериализованную форму события hello отправляется tooIoT концентратора.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-209">When we run hello previous code toosend hello Temperature event, this serialized form of hello event is sent tooIoT Hub:</span></span>

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="8dbe6-210">Мы отправляем значение температуры с типом **TemperatureEvent**. Эта структура содержит элементы **Temperature** и **Time**.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-210">We're sending a temperature which is of type **TemperatureEvent** and that struct contains a **Temperature** and **Time** member.</span></span> <span data-ttu-id="8dbe6-211">Непосредственно отражается в данных сериализации hello.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-211">This is directly reflected in hello serialized data.</span></span>

<span data-ttu-id="8dbe6-212">Точно так же событие влажности можно отправить с помощью следующего кода:</span><span class="sxs-lookup"><span data-stu-id="8dbe6-212">Similarly, we can send a humidity event with this code:</span></span>

```
thermostat->Humidity.Humidity = 45;
thermostat->Humidity.Time = GetDateTimeOffset(now);
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="8dbe6-213">форма сериализации Hello, отправил tooIoT концентратора выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="8dbe6-213">hello serialized form that’s sent tooIoT Hub appears as follows:</span></span>

```
{"Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="8dbe6-214">Опять же, все как и ожидалось.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-214">Again, this is as expected.</span></span>

<span data-ttu-id="8dbe6-215">С помощью этой модели можно понять, как легко добавить дополнительные события.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-215">With this model, you can imagine how additional events can easily be added.</span></span> <span data-ttu-id="8dbe6-216">Определите несколько структур с помощью **DECLARE\_СТРУКТУРЫ**и включить соответствующее событие hello в модели с помощью hello **WITH\_данных**.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-216">You define more structures using **DECLARE\_STRUCT**, and include hello corresponding event in hello model using **WITH\_DATA**.</span></span>

<span data-ttu-id="8dbe6-217">Теперь изменим hello модели, чтобы оно включало hello и те же данные, но с другой структурой.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-217">Now, let’s modify hello model so that it includes hello same data but with a different structure.</span></span>

### <a name="model-2"></a><span data-ttu-id="8dbe6-218">Модель 2</span><span class="sxs-lookup"><span data-stu-id="8dbe6-218">Model 2</span></span>
<span data-ttu-id="8dbe6-219">Рассмотрим этот toohello альтернативные модели один выше.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-219">Consider this alternative model toohello one above:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="8dbe6-220">В этом случае мы исключены hello **DECLARE\_СТРУКТУРЫ** макросы и просто определяете hello элементов данных в нашем сценарии, используя простые типы hello язык моделирования.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-220">In this case we've eliminated hello **DECLARE\_STRUCT** macros and are simply defining hello data items from our scenario using simple types from hello modeling language.</span></span>

<span data-ttu-id="8dbe6-221">Только для hello момента давайте игнорировать hello **время** событий.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-221">Just for hello moment let’s ignore hello **Time** event.</span></span> <span data-ttu-id="8dbe6-222">С этой отдельно от Вот tooingress кода hello **температуры**:</span><span class="sxs-lookup"><span data-stu-id="8dbe6-222">With that aside, here’s hello code tooingress **Temperature**:</span></span>

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

<span data-ttu-id="8dbe6-223">Этот код отправляет следующие hello сериализации событий tooIoT концентратора:</span><span class="sxs-lookup"><span data-stu-id="8dbe6-223">This code sends hello following serialized event tooIoT Hub:</span></span>

```
{"Temperature":75}
```

<span data-ttu-id="8dbe6-224">И hello кода для отправки событий влажности hello имеет следующий вид:</span><span class="sxs-lookup"><span data-stu-id="8dbe6-224">And hello code for sending hello Humidity event appears as follows:</span></span>

```
thermostat->Humidity = 45;
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="8dbe6-225">Этот код отправляет этот tooIoT концентратора:</span><span class="sxs-lookup"><span data-stu-id="8dbe6-225">This code sends this tooIoT Hub:</span></span>

```
{"Humidity":45}
```

<span data-ttu-id="8dbe6-226">По-прежнему ничего непредвиденного.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-226">So far there are still no surprises.</span></span> <span data-ttu-id="8dbe6-227">Теперь изменим, как использовать макрос SERIALIZE hello.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-227">Now let's change how we use hello SERIALIZE macro.</span></span>

<span data-ttu-id="8dbe6-228">Hello **СЕРИАЛИЗАЦИИ** макрос может занять несколько событий данных как аргументы.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-228">hello **SERIALIZE** macro can take multiple data events as arguments.</span></span> <span data-ttu-id="8dbe6-229">Это позволяет нам tooserialize hello **температуры** и **влажность** событий вместе и отправить их tooIoT концентратора в одном вызове:</span><span class="sxs-lookup"><span data-stu-id="8dbe6-229">This enables us tooserialize hello **Temperature** and **Humidity** event together and send them tooIoT Hub in one call:</span></span>

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="8dbe6-230">Вы можете догадаться, что hello этот код образом, два элемента данных события отправляются tooIoT концентратора:</span><span class="sxs-lookup"><span data-stu-id="8dbe6-230">You might guess that hello result of this code is that two data events are sent tooIoT Hub:</span></span>

<span data-ttu-id="8dbe6-231">[</span><span class="sxs-lookup"><span data-stu-id="8dbe6-231">[</span></span>

<span data-ttu-id="8dbe6-232">{"Temperature":75},</span><span class="sxs-lookup"><span data-stu-id="8dbe6-232">{"Temperature":75},</span></span>

<span data-ttu-id="8dbe6-233">{"Humidity":45}</span><span class="sxs-lookup"><span data-stu-id="8dbe6-233">{"Humidity":45}</span></span>

<span data-ttu-id="8dbe6-234">]</span><span class="sxs-lookup"><span data-stu-id="8dbe6-234">]</span></span>

<span data-ttu-id="8dbe6-235">Другими словами, можно предположить, что этот код является hello же, как и отправка **температуры** и **влажность** отдельно.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-235">In other words, you might expect that this code is hello same as sending **Temperature** and **Humidity** separately.</span></span> <span data-ttu-id="8dbe6-236">Это просто toopass удобства обоих событий слишком**СЕРИАЛИЗАЦИИ** в hello же вызвать.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-236">It’s just a convenience toopass both events too**SERIALIZE** in hello same call.</span></span> <span data-ttu-id="8dbe6-237">Однако это не так hello.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-237">However, that’s not hello case.</span></span> <span data-ttu-id="8dbe6-238">Вместо этого приведенный выше код hello отправляет этот tooIoT событий данных single концентратора:</span><span class="sxs-lookup"><span data-stu-id="8dbe6-238">Instead, hello code above sends this single data event tooIoT Hub:</span></span>

<span data-ttu-id="8dbe6-239">{"Temperature":75, "Humidity":45}</span><span class="sxs-lookup"><span data-stu-id="8dbe6-239">{"Temperature":75, "Humidity":45}</span></span>

<span data-ttu-id="8dbe6-240">Это может показаться странным, так как в нашей модели события **Temperature** и **Humidity** определены как два *отдельных* события:</span><span class="sxs-lookup"><span data-stu-id="8dbe6-240">This may seem strange because our model defines **Temperature** and **Humidity** as two *separate* events:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="8dbe6-241">Дополнительные точки toohello, мы не этих событий модели где **температуры** и **влажность** в hello структуру:</span><span class="sxs-lookup"><span data-stu-id="8dbe6-241">More toohello point, we didn’t model these events where **Temperature** and **Humidity** are in hello same structure:</span></span>

```
DECLARE_STRUCT(TemperatureAndHumidityEvent,
int, Temperature,
int, Humidity,
);

DECLARE_MODEL(Thermostat,
WITH_DATA(TemperatureAndHumidityEvent, TemperatureAndHumidity),
);
```

<span data-ttu-id="8dbe6-242">При использовании этой модели, было бы проще toounderstand как **температуры** и **влажность** были бы отправлены в hello же сериализованное сообщение.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-242">If we used this model, it would be easier toounderstand how **Temperature** and **Humidity** would be sent in hello same serialized message.</span></span> <span data-ttu-id="8dbe6-243">Однако он не может очистить почему работает таким образом, при передаче обоих событий данных слишком**СЕРИАЛИЗАЦИИ** с помощью модели 2.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-243">However it may not be clear why it works that way when you pass both data events too**SERIALIZE** using model 2.</span></span>

<span data-ttu-id="8dbe6-244">Это упрощает toounderstand Если известно, hello предположения hello **сериализатор** делает библиотеки.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-244">This behavior is easier toounderstand if you know hello assumptions that hello **serializer** library is making.</span></span> <span data-ttu-id="8dbe6-245">toomake смысле это давайте рассмотрим задней tooour модели:</span><span class="sxs-lookup"><span data-stu-id="8dbe6-245">toomake sense of this let’s go back tooour model:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="8dbe6-246">Взгляните на эту модель в контексте объектно-ориентированного подхода.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-246">Think of this model in object-oriented terms.</span></span> <span data-ttu-id="8dbe6-247">В этом случае мы моделируем физическое устройство (термостат), которое включает некие атрибуты (например, **Temperature** и **Humidity**).</span><span class="sxs-lookup"><span data-stu-id="8dbe6-247">In this case we’re modeling a physical device (a thermostat) and that device includes attributes like **Temperature** and **Humidity**.</span></span>

<span data-ttu-id="8dbe6-248">Мы можем отправить hello полное состояние нашей модели с кодом, например hello следующее:</span><span class="sxs-lookup"><span data-stu-id="8dbe6-248">We can send hello entire state of our model with code such as hello following:</span></span>

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity, thermostat->Time) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="8dbe6-249">При условии, что значения hello температура, влажность и время установлены, можно увидеть события, например, это отправленных tooIoT концентратора:</span><span class="sxs-lookup"><span data-stu-id="8dbe6-249">Assuming hello values of Temperature, Humidity and Time are set, we would see an event like this sent tooIoT Hub:</span></span>

```
{"Temperature":75, "Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="8dbe6-250">Иногда может быть только toosend *некоторые* свойств hello модели toohello облака (Это особенно важно, если модель содержит большое количество данных событий).</span><span class="sxs-lookup"><span data-stu-id="8dbe6-250">Sometimes you may only want toosend *some* properties of hello model toohello cloud (this is especially true if your model contains a large number of data events).</span></span> <span data-ttu-id="8dbe6-251">Это полезно toosend только подмножество данных событий, таких как в примере выше:</span><span class="sxs-lookup"><span data-stu-id="8dbe6-251">It’s useful toosend only a subset of data events, such as in our earlier example:</span></span>

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="8dbe6-252">Это приводит к возникновению ошибки точно hello же сериализации событий, как если мы определили **TemperatureEvent** с **температуры** и **время** члена, так же, как мы с модель 1.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-252">This generates exactly hello same serialized event as if we had defined a **TemperatureEvent** with a **Temperature** and **Time** member, just as we did with model 1.</span></span> <span data-ttu-id="8dbe6-253">В этом случае мы были может toogenerate точно hello же сериализации событий с помощью другой модели (модель 2), так как мы позвонили **СЕРИАЛИЗАЦИИ** по-разному.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-253">In this case we were able toogenerate exactly hello same serialized event by using a different model (model 2) because we called **SERIALIZE** in a different way.</span></span>

<span data-ttu-id="8dbe6-254">Hello важно, что при передаче нескольких событий данных слишком**СЕРИАЛИЗАЦИИ,** то предполагается, что каждое событие — это свойство в единый объект JSON.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-254">hello important point is that if you pass multiple data events too**SERIALIZE,** then it assumes each event is a property in a single JSON object.</span></span>

<span data-ttu-id="8dbe6-255">Hello наилучший подход зависит от того, и каким образом вы думаете о модели.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-255">hello best approach depends on you and how you think about your model.</span></span> <span data-ttu-id="8dbe6-256">Если вы отправляете сообщение «события» toohello облака, и каждое событие содержит определенный набор свойств, hello первый подход делает смысл.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-256">If you’re sending "events" toohello cloud and each event contains a defined set of properties, then hello first approach makes a lot of sense.</span></span> <span data-ttu-id="8dbe6-257">В этом случае используется **DECLARE\_СТРУКТУРЫ** toodefine hello структуру каждого события, а затем включить их в модели с помощью hello **WITH\_данные** макрос.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-257">In that case you would use **DECLARE\_STRUCT** toodefine hello structure of each event and then include them in your model with hello **WITH\_DATA** macro.</span></span> <span data-ttu-id="8dbe6-258">Затем отправить каждого события, как это делалось в первом примере hello выше.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-258">Then you send each event as we did in hello first example above.</span></span> <span data-ttu-id="8dbe6-259">При таком подходе следует только передавать события одного данных слишком**СЕРИАЛИЗАТОР**.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-259">In this approach you would only pass a single data event too**SERIALIZER**.</span></span>

<span data-ttu-id="8dbe6-260">Если вы думаете о модели в виде объекта, hello второй подход может подойти вы.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-260">If you think about your model in an object-oriented fashion, then hello second approach may suit you.</span></span> <span data-ttu-id="8dbe6-261">В этом случае hello элементов, определенных с помощью **WITH\_данные** hello «свойства» объекта.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-261">In this case, hello elements defined using **WITH\_DATA** are hello "properties" of your object.</span></span> <span data-ttu-id="8dbe6-262">Можно передать любое подмножество событий слишком**СЕРИАЛИЗАЦИИ** том, что вам нравится, в зависимости от того сколько состояния «объекта» требуется toosend toohello облака.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-262">You pass whatever subset of events too**SERIALIZE** that you like, depending on how much of your "object’s" state you want toosend toohello cloud.</span></span>

<span data-ttu-id="8dbe6-263">Ни один из подходов нельзя назвать правильным или ошибочным.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-263">Nether approach is right or wrong.</span></span> <span data-ttu-id="8dbe6-264">Необходимо знать, как hello **сериализатор** библиотека работает, а также выбора hello моделирования подход, который наилучшим образом соответствует вашим потребностям.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-264">Just be aware of how hello **serializer** library works, and pick hello modeling approach that best fits your needs.</span></span>

## <a name="message-handling"></a><span data-ttu-id="8dbe6-265">Обработка сообщений</span><span class="sxs-lookup"><span data-stu-id="8dbe6-265">Message handling</span></span>
<span data-ttu-id="8dbe6-266">До сих в этой статье только обсуждались отправки событий tooIoT концентратора и не разрешены получения сообщений.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-266">So far this article has only discussed sending events tooIoT Hub, and hasn't addressed receiving messages.</span></span> <span data-ttu-id="8dbe6-267">Здравствуйте, причина этого является то, что мы должны tooknow о получении сообщений во многом были описаны в [ранее статье](iot-hub-device-sdk-c-intro.md).</span><span class="sxs-lookup"><span data-stu-id="8dbe6-267">hello reason for this is that what we need tooknow about receiving messages has largely been covered in an [earlier article](iot-hub-device-sdk-c-intro.md).</span></span> <span data-ttu-id="8dbe6-268">Как вы помните, обработка сообщений выполняется путем регистрации функции обратного вызова:</span><span class="sxs-lookup"><span data-stu-id="8dbe6-268">Recall from that article that you process messages by registering a message callback function:</span></span>

```
IoTHubClient_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather)
```

<span data-ttu-id="8dbe6-269">Затем создайте hello функции обратного вызова, вызываемый при получении сообщения.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-269">You then write hello callback function that’s invoked when a message is received:</span></span>

```
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable tooIoTHubMessage_GetByteArray\r\n");
        result = EXECUTE_COMMAND_ERROR;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed toomalloc\r\n");
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

<span data-ttu-id="8dbe6-270">Эта реализация **IoTHubMessage** вызовы hello определенную функцию для каждого действия в модели.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-270">This implementation of **IoTHubMessage** calls hello specific function for each action in your model.</span></span> <span data-ttu-id="8dbe6-271">Например, если модель определяет следующее действие:</span><span class="sxs-lookup"><span data-stu-id="8dbe6-271">For example, if your model defines this action:</span></span>

```
WITH_ACTION(SetAirResistance, int, Position)
```

<span data-ttu-id="8dbe6-272">Вам нужно определить функцию со следующей сигнатурой:</span><span class="sxs-lookup"><span data-stu-id="8dbe6-272">You must define a function with this signature:</span></span>

```
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position too%d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

<span data-ttu-id="8dbe6-273">**SetAirResistance** вызывается, когда это сообщение отправляется tooyour устройства.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-273">**SetAirResistance** is then called when that message is sent tooyour device.</span></span>

<span data-ttu-id="8dbe6-274">Еще какие еще не описано: hello сериализации версии выглядит сообщение.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-274">What we haven't explained yet is what hello serialized version of message looks like.</span></span> <span data-ttu-id="8dbe6-275">Другими словами Если требуется, чтобы toosend **SetAirResistance** устройства tooyour сообщения, как выглядит этот?</span><span class="sxs-lookup"><span data-stu-id="8dbe6-275">In other words, if you want toosend a **SetAirResistance** message tooyour device, what does that look like?</span></span>

<span data-ttu-id="8dbe6-276">При отправке сообщения tooa устройство, это следует делать через службу hello Azure IoT SDK.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-276">If you're sending a message tooa device, you would do so through hello Azure IoT service SDK.</span></span> <span data-ttu-id="8dbe6-277">По-прежнему необходимо tooknow какая строка toosend tooinvoke определенное действие.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-277">You still need tooknow what string toosend tooinvoke a particular action.</span></span> <span data-ttu-id="8dbe6-278">общий формат Hello отправляет сообщение выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="8dbe6-278">hello general format for sending a message appears as follows:</span></span>

```
{"Name" : "", "Parameters" : "" }
```

<span data-ttu-id="8dbe6-279">Вы отправляете сообщение сериализованный объект JSON с двумя свойствами: **имя** — имя hello действие hello (сообщение) и **параметры** содержит параметры hello этого действия.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-279">You're sending a serialized JSON object with two properties: **Name** is hello name of hello action (message) and **Parameters** contains hello parameters of that action.</span></span>

<span data-ttu-id="8dbe6-280">Например, tooinvoke **SetAirResistance** можно отправить это сообщение tooa устройство:</span><span class="sxs-lookup"><span data-stu-id="8dbe6-280">For example, tooinvoke **SetAirResistance** you can send this message tooa device:</span></span>

```
{"Name" : "SetAirResistance", "Parameters" : { "Position" : 5 }}
```

<span data-ttu-id="8dbe6-281">Имя действия Hello должен точно соответствовать действие, определенный в модели.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-281">hello action name must exactly match an action defined in your model.</span></span> <span data-ttu-id="8dbe6-282">также должны совпадать имена параметров Hello.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-282">hello parameter names must match as well.</span></span> <span data-ttu-id="8dbe6-283">Также обратите внимание на чувствительность к регистру.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-283">Also note case sensitivity.</span></span> <span data-ttu-id="8dbe6-284">Параметры **Name** и **Parameters** всегда пишутся с прописной буквы.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-284">**Name** and **Parameters** are always uppercase.</span></span> <span data-ttu-id="8dbe6-285">Убедиться, что вариант hello toomatch имя действия и параметров в модели.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-285">Make sure toomatch hello case of your action name and parameters in your model.</span></span> <span data-ttu-id="8dbe6-286">В этом примере hello действие названо «SetAirResistance» и не «setairresistance».</span><span class="sxs-lookup"><span data-stu-id="8dbe6-286">In this example, hello action name is "SetAirResistance" and not "setairresistance".</span></span>

<span data-ttu-id="8dbe6-287">Здравствуйте, два действия **TurnFanOn** и **TurnFanOff** можно вызвать путем отправки этих сообщений tooa устройства:</span><span class="sxs-lookup"><span data-stu-id="8dbe6-287">hello two other actions **TurnFanOn** and **TurnFanOff** can be invoked by sending these messages tooa device:</span></span>

```
{"Name" : "TurnFanOn", "Parameters" : {}}
{"Name" : "TurnFanOff", "Parameters" : {}}
```

<span data-ttu-id="8dbe6-288">В этом разделе описано все, что нужно tooknow при отправки событий и получение сообщений с использованием hello **сериализатор** библиотеки.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-288">This section described everything you need tooknow when sending events and receiving messages with hello **serializer** library.</span></span> <span data-ttu-id="8dbe6-289">Прежде чем продолжить, давайте рассмотрим ряд изменяемых параметров, которые позволяют управлять размером модели.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-289">Before moving on, let's cover some parameters you can configure that control how large your model is.</span></span>

## <a name="macro-configuration"></a><span data-ttu-id="8dbe6-290">Конфигурация макросов</span><span class="sxs-lookup"><span data-stu-id="8dbe6-290">Macro configuration</span></span>
<span data-ttu-id="8dbe6-291">Если вы используете hello **сериализатор** библиотеки важной частью учитывать toobe SDK hello, найденной в hello azure-c общей-библиотека программы.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-291">If you’re using hello **Serializer** library an important part of hello SDK toobe aware of is found in hello azure-c-shared-utility library.</span></span>
<span data-ttu-id="8dbe6-292">При клонировании репозитория hello Azure iot-sdk c из GitHub, с помощью параметра--рекурсивные hello вы найдете Эта библиотека общей программы.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-292">If you have cloned hello Azure-iot-sdk-c repository from GitHub using hello --recursive option, then you will find this shared utility library here:</span></span>

```
.\\c-utility
```

<span data-ttu-id="8dbe6-293">Если вы не клонировали hello библиотеки, его можно будет найти [здесь](https://github.com/Azure/azure-c-shared-utility).</span><span class="sxs-lookup"><span data-stu-id="8dbe6-293">If you have not cloned hello library, you can find it [here](https://github.com/Azure/azure-c-shared-utility).</span></span>

<span data-ttu-id="8dbe6-294">Библиотека общих программы hello приведена hello следующие папки:</span><span class="sxs-lookup"><span data-stu-id="8dbe6-294">Within hello shared utility library, you will find hello following folder:</span></span>

```
azure-c-shared-utility\\macro\_utils\_h\_generator.
```

<span data-ttu-id="8dbe6-295">Эта папка содержит решение Visual Studio с именем **macro\_utils\_h\_generator.sln**:</span><span class="sxs-lookup"><span data-stu-id="8dbe6-295">This folder contains a Visual Studio solution called **macro\_utils\_h\_generator.sln**:</span></span>

  ![](media/iot-hub-device-sdk-c-serializer/01-macro_utils_h_generator.PNG)

<span data-ttu-id="8dbe6-296">Программа Hello в это решение создает hello **макрос\_utils.h** файла.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-296">hello program in this solution generates hello **macro\_utils.h** file.</span></span> <span data-ttu-id="8dbe6-297">Что представляет собой макрос, по умолчанию\_utils.h файл, входящий в состав пакета SDK для hello.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-297">There’s a default macro\_utils.h file included with hello SDK.</span></span> <span data-ttu-id="8dbe6-298">Это решение позволяет toomodify некоторых параметров и затем повторно создайте hello файл заголовка, на основе этих параметров.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-298">This solution allows you toomodify some parameters and then recreate hello header file based on these parameters.</span></span>

<span data-ttu-id="8dbe6-299">являются Hello двух ключевых параметров, посвящена toobe **nArithmetic** и **nMacroParameters** которые определены в эти две строки, найден в макросе\_utils.tt:</span><span class="sxs-lookup"><span data-stu-id="8dbe6-299">hello two key parameters toobe concerned with are **nArithmetic** and **nMacroParameters** which are defined in these two lines found in macro\_utils.tt:</span></span>

```
<#int nArithmetic=1024;#>
<#int nMacroParameters=124;/*127 parameters in one macro deﬁnition in C99 in chapter 5.2.4.1 Translation limits*/#>

```

<span data-ttu-id="8dbe6-300">Эти значения являются параметрами по умолчанию hello, входящий в состав пакета SDK для hello.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-300">These values are hello default parameters included with hello SDK.</span></span> <span data-ttu-id="8dbe6-301">Каждый параметр имеет hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="8dbe6-301">Each parameter has hello following meaning:</span></span>

* <span data-ttu-id="8dbe6-302">nMacroParameters — определяет количество параметров в одном определении макроса DECLARE\_MODEL.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-302">nMacroParameters – Controls how many parameters you can have in one DECLARE\_MODEL macro definition.</span></span>
* <span data-ttu-id="8dbe6-303">nArithmetic — элементы управления hello общее количество элементов, допустимое в модели.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-303">nArithmetic – Controls hello total number of members allowed in a model.</span></span>

<span data-ttu-id="8dbe6-304">Hello эти параметры важны, поскольку они управляют размер может быть модели.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-304">hello reason these parameters are important is because they control how large your model can be.</span></span> <span data-ttu-id="8dbe6-305">Например, возьмем следующее определение модели:</span><span class="sxs-lookup"><span data-stu-id="8dbe6-305">For example, consider this model definition:</span></span>

```
DECLARE_MODEL(MyModel,
WITH_DATA(int, MyData)
);
```

<span data-ttu-id="8dbe6-306">Как говорилось ранее, **DECLARE\_MODEL** является обычным макросом C.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-306">As mentioned previously, **DECLARE\_MODEL** is just a C macro.</span></span> <span data-ttu-id="8dbe6-307">Здравствуйте, имена модели hello и hello **WITH\_данные** инструкции (пока еще другой макрос) — параметры **DECLARE\_МОДЕЛИ**.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-307">hello names of hello model and hello **WITH\_DATA** statement (yet another macro) are parameters of **DECLARE\_MODEL**.</span></span> <span data-ttu-id="8dbe6-308">**nMacroParameters** определяет, сколько параметров можно включить в макрос **DECLARE\_MODEL**.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-308">**nMacroParameters** defines how many parameters can be included in **DECLARE\_MODEL**.</span></span> <span data-ttu-id="8dbe6-309">Фактически этот параметр определяет максимальное количество событий, инициируемых изменением данных, и объявлений действий.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-309">Effectively, this defines how many data event and action declarations you can have.</span></span> <span data-ttu-id="8dbe6-310">Таким образом ограничение по умолчанию hello в 124 это означает, что можно определить модель используется сочетание около 60 действия и данные события.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-310">As such, with hello default limit of 124 this means that you can define a model with a combination of about 60 actions and data events.</span></span> <span data-ttu-id="8dbe6-311">При попытке tooexceed это ограничение, вы получите ошибки компилятора, которые выглядят примерно toothis:</span><span class="sxs-lookup"><span data-stu-id="8dbe6-311">If you try tooexceed this limit, you'll receive compiler errors that look similar toothis:</span></span>

  ![](media/iot-hub-device-sdk-c-serializer/02-nMacroParametersCompilerErrors.PNG)

<span data-ttu-id="8dbe6-312">Hello **nArithmetic** параметра приведены дополнительные сведения о механизмах hello языка макрос hello, чем приложения.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-312">hello **nArithmetic** parameter is more about hello internal workings of hello macro language than your application.</span></span>  <span data-ttu-id="8dbe6-313">Он управляет hello общее количество элементов, что в модели, включая **DECLARE_STRUCT** макросы.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-313">It controls hello total number of members you can have in your model, including **DECLARE_STRUCT** macros.</span></span> <span data-ttu-id="8dbe6-314">Если при компиляции программы вы получаете подобные сообщения об ошибках, попробуйте увеличить значение **nArithmetic**.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-314">If you start seeing compiler errors such as this, then you should try increasing **nArithmetic**:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/03-nArithmeticCompilerErrors.PNG)

<span data-ttu-id="8dbe6-315">Toochange эти параметры, изменить значения hello в макросе hello\_utils.tt файл, макрос hello recompile\_utils\_h\_generator.sln решение, а также выполнения hello скомпилированная программа.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-315">If you want toochange these parameters, modify hello values in hello macro\_utils.tt file, recompile hello macro\_utils\_h\_generator.sln solution, and run hello compiled program.</span></span> <span data-ttu-id="8dbe6-316">После этого, макрос\_utils.h файл создается и помещается в hello.\\ Общие\\inc каталога.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-316">When you do so, a new macro\_utils.h file is generated and placed in hello .\\common\\inc directory.</span></span>

<span data-ttu-id="8dbe6-317">В новой версии заказа toouse hello макроса\_utils.h, удалите hello **сериализатор** пакет NuGet из решения и вместо него включают hello **сериализатор** проекта Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-317">In order toouse hello new version of macro\_utils.h, remove hello **serializer** NuGet package from your solution and in its place include hello **serializer** Visual Studio project.</span></span> <span data-ttu-id="8dbe6-318">Это позволяет toocompile ваш код от исходного кода hello hello сериализатор библиотеки.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-318">This enables your code toocompile against hello source code of hello serializer library.</span></span> <span data-ttu-id="8dbe6-319">Сюда входят hello обновлены макрос\_utils.h.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-319">This includes hello updated macro\_utils.h.</span></span> <span data-ttu-id="8dbe6-320">Если требуется toodo для **simplesample\_amqp**, удалите пакет NuGet hello hello сериализатор библиотеки из hello решения:</span><span class="sxs-lookup"><span data-stu-id="8dbe6-320">If you want toodo this for **simplesample\_amqp**, start by removing hello NuGet package for hello serializer library from hello solution:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/04-serializer-github-package.PNG)

<span data-ttu-id="8dbe6-321">Затем добавьте этот tooyour проект решения Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="8dbe6-321">Then add this project tooyour Visual Studio solution:</span></span>

> <span data-ttu-id="8dbe6-322">.\\c\\serializer\\build\\windows\\serializer.vcxproj</span><span class="sxs-lookup"><span data-stu-id="8dbe6-322">.\\c\\serializer\\build\\windows\\serializer.vcxproj</span></span>
> 
> 

<span data-ttu-id="8dbe6-323">Когда все будет готово, ваше решение должно выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="8dbe6-323">When you're done, your solution should look like this:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/05-serializer-project.PNG)

<span data-ttu-id="8dbe6-324">Теперь при компиляции решения, hello обновлены макрос\_utils.h включается в двоичный файл.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-324">Now when you compile your solution, hello updated macro\_utils.h is included in your binary.</span></span>

<span data-ttu-id="8dbe6-325">Обратите внимание, что установка слишком большого значения может привести к превышению ограничений компилятора.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-325">Note that increasing these values high enough can exceed compiler limits.</span></span> <span data-ttu-id="8dbe6-326">toothis точки hello **nMacroParameters** hello основной параметр с какой toobe беспокоиться.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-326">toothis point, hello **nMacroParameters** is hello main parameter with which toobe concerned.</span></span> <span data-ttu-id="8dbe6-327">спецификации C99 Hello указывает, что допускается менее 127 параметров в определении макроса.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-327">hello C99 spec specifies that a minimum of 127 parameters are allowed in a macro definition.</span></span> <span data-ttu-id="8dbe6-328">Hello компилятор Microsoft точно соответствует спецификации hello (и существует ограничение в 127), поэтому его нельзя будет tooincrease **nMacroParameters** за пределы по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-328">hello Microsoft compiler follows hello spec exactly (and has a limit of 127), so you won't be able tooincrease **nMacroParameters** beyond hello default.</span></span> <span data-ttu-id="8dbe6-329">Другие компиляторы могут позволять toodo так (например, компилятор GNU hello поддерживает более высокий предел).</span><span class="sxs-lookup"><span data-stu-id="8dbe6-329">Other compilers might allow you toodo so (for example, hello GNU compiler supports a higher limit).</span></span>

<span data-ttu-id="8dbe6-330">Пока мы рассмотрели практически все, что нужно tooknow о том, как код toowrite с hello **сериализатор** библиотеки.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-330">So far we've covered just about everything you need tooknow about how toowrite code with hello **serializer** library.</span></span> <span data-ttu-id="8dbe6-331">Прежде чем закончить, давайте вернемся к некоторым темам из предыдущих статей, которые могут вызвать у вас вопросы.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-331">Before concluding, let's revisit some topics from previous articles that you may be wondering about.</span></span>

## <a name="hello-lower-level-apis"></a><span data-ttu-id="8dbe6-332">Hello более низкого уровня API-интерфейсы</span><span class="sxs-lookup"><span data-stu-id="8dbe6-332">hello lower-level APIs</span></span>
<span data-ttu-id="8dbe6-333">Пример приложения Hello фокусе в этой статье — **simplesample\_amqp**.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-333">hello sample application on which this article focused is **simplesample\_amqp**.</span></span> <span data-ttu-id="8dbe6-334">Этот образец использует hello более высокого уровня (hello не — "LL») API-интерфейсы toosend события и получать сообщения.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-334">This sample uses hello higher-level (hello non-"LL") APIs toosend events and receive messages.</span></span> <span data-ttu-id="8dbe6-335">При использовании таких API запускается фоновый поток, который отвечает и за отправку событий, и за получение сообщений.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-335">If you use these APIs, a background thread runs which takes care of both sending events and receiving messages.</span></span> <span data-ttu-id="8dbe6-336">Тем не менее можно использовать hello более низкого уровня (все) API-интерфейсы tooeliminate это фоновый поток и занять явный контроль над при отправки событий или получения сообщений из облака hello.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-336">However, you can use hello lower-level (LL) APIs tooeliminate this background thread and take explicit control over when you send events or receive messages from hello cloud.</span></span>

<span data-ttu-id="8dbe6-337">Как описано в [предыдущей статьи](iot-hub-device-sdk-c-iothubclient.md), имеется ряд функций, состоящий из hello более высокого уровня API-интерфейсы:</span><span class="sxs-lookup"><span data-stu-id="8dbe6-337">As described in a [previous article](iot-hub-device-sdk-c-iothubclient.md), there is a set of functions that consists of hello higher-level APIs:</span></span>

* <span data-ttu-id="8dbe6-338">IoTHubClient\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="8dbe6-338">IoTHubClient\_CreateFromConnectionString</span></span>
* <span data-ttu-id="8dbe6-339">IoTHubClient\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="8dbe6-339">IoTHubClient\_SendEventAsync</span></span>
* <span data-ttu-id="8dbe6-340">IoTHubClient\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="8dbe6-340">IoTHubClient\_SetMessageCallback</span></span>
* <span data-ttu-id="8dbe6-341">IoTHubClient\_Destroy</span><span class="sxs-lookup"><span data-stu-id="8dbe6-341">IoTHubClient\_Destroy</span></span>

<span data-ttu-id="8dbe6-342">В примере **simplesample\_amqp** показывается, как использовать эти API.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-342">These APIs are demonstrated in **simplesample\_amqp**.</span></span>

<span data-ttu-id="8dbe6-343">Существует аналогичный набор API низкого уровня.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-343">There is also an analogous set of lower-level APIs.</span></span>

* <span data-ttu-id="8dbe6-344">IoTHubClient\_LL\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="8dbe6-344">IoTHubClient\_LL\_CreateFromConnectionString</span></span>
* <span data-ttu-id="8dbe6-345">IoTHubClient\_LL\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="8dbe6-345">IoTHubClient\_LL\_SendEventAsync</span></span>
* <span data-ttu-id="8dbe6-346">IoTHubClient\_LL\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="8dbe6-346">IoTHubClient\_LL\_SetMessageCallback</span></span>
* <span data-ttu-id="8dbe6-347">IoTHubClient\_LL\_Destroy</span><span class="sxs-lookup"><span data-stu-id="8dbe6-347">IoTHubClient\_LL\_Destroy</span></span>

<span data-ttu-id="8dbe6-348">Обратите внимание, что точно hello hello более низкого уровня API-интерфейсы рабочих, так же, как описано в предыдущей статьи hello.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-348">Note that hello lower-level APIs work exactly hello same way as described in hello previous articles.</span></span> <span data-ttu-id="8dbe6-349">Hello первый набор API-интерфейсов можно использовать, если требуется, чтобы фоновый поток toohandle события отправки и получения сообщений.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-349">You can use hello first set of APIs if you want a background thread toohandle sending events and receiving messages.</span></span> <span data-ttu-id="8dbe6-350">Hello второй набор API-интерфейсов используется в том случае, если требуется явный контроль над при отправке и получении данных из центра IoT.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-350">You use hello second set of APIs if you want explicit control over when you send and receive data from IoT Hub.</span></span> <span data-ttu-id="8dbe6-351">Любой набор API-интерфейсы работы одинаково хорошо с hello **сериализатор** библиотеки.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-351">Either set of APIs work equally well with hello **serializer** library.</span></span>

<span data-ttu-id="8dbe6-352">Пример того, как hello более низкого уровня API используются с hello **сериализатор** библиотеки, в разделе hello **simplesample\_http** приложения.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-352">For an example of how hello lower-level APIs are used with hello **serializer** library, see hello **simplesample\_http** application.</span></span>

## <a name="additional-topics"></a><span data-ttu-id="8dbe6-353">Дополнительные разделы</span><span class="sxs-lookup"><span data-stu-id="8dbe6-353">Additional topics</span></span>
<span data-ttu-id="8dbe6-354">Также стоит упомянуть об обработке свойств, параметрах конфигурации и использовании дополнительных учетных данных устройства.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-354">A few other topics worth mentioning again are property handling, using alternate device credentials, and configuration options.</span></span> <span data-ttu-id="8dbe6-355">Все эти вопросы рассматриваются в [предыдущей статье](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="8dbe6-355">These are all topics covered in a [previous article](iot-hub-device-sdk-c-iothubclient.md).</span></span> <span data-ttu-id="8dbe6-356">Hello главное, что все эти возможности работать в hello таким же образом с hello **сериализатор** библиотеки, как с hello **IoTHubClient** библиотеки.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-356">hello main point is that all of these features work in hello same way with hello **serializer** library as they do with hello **IoTHubClient** library.</span></span> <span data-ttu-id="8dbe6-357">Например, если нужно tooattach свойства tooan событие из модели используется **IoTHubMessage\_свойства** и **карты**\_**AddorUpdate**, hello так же, как было описано выше:</span><span class="sxs-lookup"><span data-stu-id="8dbe6-357">For example, if you want tooattach properties tooan event from your model, you use **IoTHubMessage\_Properties** and **Map**\_**AddorUpdate**, hello same way as described previously:</span></span>

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

<span data-ttu-id="8dbe6-358">Было ли создано событие hello из hello **сериализатор** библиотеки или создан вручную с помощью hello **IoTHubClient** библиотека не имеет значения.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-358">Whether hello event was generated from hello **serializer** library or created manually using hello **IoTHubClient** library does not matter.</span></span>

<span data-ttu-id="8dbe6-359">Для hello альтернативные учетные данные устройства, с помощью **IoTHubClient\_LL\_создать** работает точно так же как **IoTHubClient\_CreateFromConnectionString** для Выделение **центром IOT\_КЛИЕНТА\_ОБРАБОТКИ**.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-359">For hello alternate device credentials, using **IoTHubClient\_LL\_Create** works just as well as **IoTHubClient\_CreateFromConnectionString** for allocating an **IOTHUB\_CLIENT\_HANDLE**.</span></span>

<span data-ttu-id="8dbe6-360">Наконец Если вы используете hello **сериализатор** библиотеки, можно задать параметры конфигурации с **IoTHubClient\_LL\_SetOption** так же, как это было сделано при использовании hello **IoTHubClient** библиотеки.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-360">Finally, if you're using hello **serializer** library, you can set configuration options with **IoTHubClient\_LL\_SetOption** just as you did when using hello **IoTHubClient** library.</span></span>

<span data-ttu-id="8dbe6-361">Функцию, которая уникальным toohello **сериализатор** библиотеки являются hello инициализации API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-361">A feature that is unique toohello **serializer** library are hello initialization APIs.</span></span> <span data-ttu-id="8dbe6-362">Перед началом работы с библиотекой hello, необходимо вызвать **сериализатор\_init**:</span><span class="sxs-lookup"><span data-stu-id="8dbe6-362">Before you can start working with hello library, you must call **serializer\_init**:</span></span>

```
serializer_init(NULL);
```

<span data-ttu-id="8dbe6-363">Это делается непосредственно перед вызовом метода **IoTHubClient\_CreateFromConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-363">This is done just before you call **IoTHubClient\_CreateFromConnectionString**.</span></span>

<span data-ttu-id="8dbe6-364">Аналогичным образом, после завершения работы с библиотекой hello последнего вызова hello вносятся задано слишком**сериализатор\_deinit**:</span><span class="sxs-lookup"><span data-stu-id="8dbe6-364">Similarly, when you're done working with hello library, hello last call you’ll make is too**serializer\_deinit**:</span></span>

```
serializer_deinit();
```

<span data-ttu-id="8dbe6-365">В противном случае все hello другие функции, перечисленные выше рабочие же hello в hello **сериализатор** библиотеки, как в hello **IoTHubClient** библиотеки.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-365">Otherwise, all of hello other features listed above work hello same in hello **serializer** library as they do in hello **IoTHubClient** library.</span></span> <span data-ttu-id="8dbe6-366">Дополнительные сведения о каких-либо из следующих разделов в статье hello [предыдущей статьи](iot-hub-device-sdk-c-iothubclient.md) этой серии.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-366">For more information about any of these topics, see hello [previous article](iot-hub-device-sdk-c-iothubclient.md) in this series.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8dbe6-367">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8dbe6-367">Next steps</span></span>
<span data-ttu-id="8dbe6-368">В этой статье описывается в подробности hello уникальные характеристики hello **сериализатор** библиотеки, содержащихся в hello **устройств Azure IoT SDK для C**. С hello сведения, предоставленные нужно хорошо понимать как toouse моделирует toosend события и получать сообщения от центра IoT.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-368">This article describes in detail hello unique aspects of hello **serializer** library contained in hello **Azure IoT device SDK for C**. With hello information provided you should have a good understanding of how toouse models toosend events and receive messages from IoT Hub.</span></span>

<span data-ttu-id="8dbe6-369">Это также завершает hello трех выпусков на как hello toodevelop приложений с помощью **устройств Azure IoT SDK для C**. Это должен быть достаточно только get сведения toonot которой была начата, но позволяют глубокого понимания принципов работы hello API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-369">This also concludes hello three-part series on how toodevelop applications with hello **Azure IoT device SDK for C**. This should be enough information toonot only get you started but give you a thorough understanding of how hello APIs work.</span></span> <span data-ttu-id="8dbe6-370">Дополнительные сведения существует несколько образцов в приветствия SDK здесь не описаны.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-370">For additional information, there are a few samples in hello SDK not covered here.</span></span> <span data-ttu-id="8dbe6-371">В противном случае hello [документации по пакету SDK](https://github.com/Azure/azure-iot-sdk-c) является ценным ресурсом для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="8dbe6-371">Otherwise, hello [SDK documentation](https://github.com/Azure/azure-iot-sdk-c) is a good resource for additional information.</span></span>

<span data-ttu-id="8dbe6-372">toolearn Дополнительные сведения о разработке приложений для центра IoT. в разделе hello [пакеты SDK Azure IoT][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="8dbe6-372">toolearn more about developing for IoT Hub, see hello [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="8dbe6-373">Изучение возможностей hello центра IoT toofurther см. в разделе:</span><span class="sxs-lookup"><span data-stu-id="8dbe6-373">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="8dbe6-374">[Отправка сообщений с устройства в облако с помощью имитации устройства (Linux) с использованием Edge Интернета вещей Azure][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="8dbe6-374">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
