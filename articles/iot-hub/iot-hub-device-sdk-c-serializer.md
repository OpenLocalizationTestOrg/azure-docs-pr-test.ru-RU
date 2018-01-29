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
ms.openlocfilehash: d8b9e147b68d16c6c166e92cbabf5b5b63e23e8d
ms.sourcegitcommit: 933af6219266cc685d0c9009f533ca1be03aa5e9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/18/2017
---
# <a name="azure-iot-device-sdk-for-c--more-about-serializer"></a>Пакет SDK для устройств Azure IoT для C — дополнительные сведения о сериализаторе
В [первой статье](iot-hub-device-sdk-c-intro.md) этого курса вы познакомились с **пакетом SDK для устройств Azure IoT для C**. В следующей статье содержится более подробное описание библиотеки [**IoTHubClient**](iot-hub-device-sdk-c-iothubclient.md). Этой статьей завершается изучение пакета SDK, в ней более подробно рассматривается оставшийся компонент — библиотека **serializer** .

В первой статье описывается, как использовать библиотеку **serializer** для отправки событий в Центр Интернета вещей и получения сообщений из него. В этой статье мы углубим свои знания, более подробно изучив моделирование данных с помощью макроязыка библиотеки **serializer** . В этой статье также подробнее рассматриваются механизмы, используемые библиотекой для сериализации сообщений (которые в некоторых случаях позволяют управлять поведением сериализации). Также здесь описываются некоторые параметры, доступные для изменения и определяющие размер создаваемой модели.

Кроме того, в статье мы вернемся к некоторым рассмотренным ранее вопросам, включая обработку сообщений и свойств. Вы узнаете, что при использовании библиотеки **serializer** эти функции работают так же, как и при использовании библиотеки **IoTHubClient**.

Все приведенные здесь инструкции основаны на примерах использования примеров **serializer** из пакета SDK. Чтобы перейти к выполнению действий, просмотрите приложения **simplesample\_amqp** и **simplesample\_http**, включенные в пакет SDK для устройств Azure IoT для C.

[**Пакет SDK для устройств Интернета вещей Azure для C**](https://github.com/Azure/azure-iot-sdk-c) доступен в репозитории на сайте GitHub. Дополнительные сведения об API см. в [справочной документации по API для C](https://azure.github.io/azure-iot-sdk-c/index.html).

## <a name="the-modeling-language"></a>Язык моделирования
В [вводной статье](iot-hub-device-sdk-c-intro.md) этого курса вы познакомились с языком моделирования **пакета SDK для устройств Azure IoT для C** на примере приложения **simplesample\_amqp**.

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

Как вы видите, язык моделирования основан на макросах C. Определение всегда начинается с ключевого слова **BEGIN\_NAMESPACE** и всегда заканчивается ключевым словом **END\_NAMESPACE**. Зачастую для пространства имен выбирается название компании или, как в этом примере, название рабочего проекта.

Все, что происходит «внутри» пространства имен, определяет модель. В данном случае создается одна модель для анемометра. Опять-таки, модели может быть присвоено любое имя, но обычно оно соответствует имени устройства или типу данных для взаимодействия с Центром Интернета вещей.  

Модели содержат определение событий, которые вы можете отправить в Центр Интернета вещей (*данные*), и сообщений, которые вы можете получить из Центра Интернета вещей (*действия*). Как видно из примера, для событий указываются тип и имя; а для действий — имя и необязательные параметры (каждый с указанием типа).

Стоит отметить, что этот пример не демонстрирует дополнительные типы данных, поддерживаемые пакетом SDK. Об этом мы поговорим далее.

> [!NOTE]
> Данные, отправляемые устройством, рассматриваются Центром Интернета вещей как *события*, тогда как в языке моделирования они называются *данными* (определяются макросом **WITH_DATA**). Данные, отправляемые устройству, рассматриваются Центром как *сообщения*, а в языке моделирования они называются *действиями* (определяются макросом **WITH_ACTION**). Помните, что в этой статье данные понятия могут быть взаимозаменяемыми.
> 
> 

### <a name="supported-data-types"></a>Поддерживаемые типы данных.
В моделях, созданных с помощью библиотеки **serializer** , поддерживаются следующие типы данных:

| Тип | Описание |
| --- | --- |
| double |число с плавающей запятой двойной точности |
| int |32-разрядное целое число |
| float; |число с плавающей запятой одиночной точности |
| длинное целое число |длинное целое число |
| int8\_t |8-разрядное целое число |
| int16\_t |16-разрядное целое число |
| int32\_t |32-разрядное целое число |
| int64\_t |64-разрядное целое число |
| bool |Логическое |
| ascii\_char\_ptr |строка ASCII |
| EDM\_DATE\_TIME\_OFFSET |смещение даты и времени |
| EDM\_GUID |GUID |
| EDM\_BINARY |binary; |
| DECLARE\_STRUCT |сложный тип данных |

Давайте начнем с последнего типа данных. Макрос **DECLARE\_STRUCT** позволяет определять сложные типы данных, которые являются группировками других простых типов. Эти группировки позволяют определить модель, которая выглядит следующим образом.

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

Наша модель содержит одно событие, инициируемое изменением данных, типа **TestType**. **TestType** является сложным типом, который содержит несколько элементов, совокупно представляющих простые типы, поддерживаемые языком моделирования **serializer**.

С помощью такой модели мы можем отправлять данные в Центр Интернета вещей, используя следующий код:

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

Фактически мы присваиваем значение каждому элементу структуры **Test**, а затем вызываем **SendAsync** для отправки события **Test** в облако. 
            **SendAsync** является вспомогательной и служит для отправки одного события, инициируемого изменением данных, в Центр Интернета вещей:

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

Эта функция сериализует нужное нам событие, инициируемое изменением данных, и отправляет его в Центр Интернета вещей с помощью функции **IoTHubClient\_SendEventAsync**. Этот код мы уже использовали в предыдущих статьях (**SendAsync** просто заключает логику в удобную функцию).

В приведенном выше коде используется еще одна вспомогательная функция — **GetDateTimeOffset**. Эта функция преобразует заданное значение времени в значение типа **EDM\_DATE\_TIME\_OFFSET**:

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

Если запустить этот код, в Центр Интернета вещей будет отправлено следующее сообщение:

```
{"aDouble":1.100000000000000, "aInt":2, "aFloat":3.000000, "aLong":4, "aInt8":5, "auInt8":6, "aInt16":7, "aInt32":8, "aInt64":9, "aBool":true, "aAsciiCharPtr":"ascii string 1", "aDateTimeOffset":"2015-09-14T21:18:21Z", "aGuid":"00010203-0405-0607-0809-0A0B0C0D0E0F", "aBinary":"AQID"}
```

Обратите внимание, что сериализация выполняется в формате JSON. В библиотеке **serializer** для сериализации используется именно этот формат. Также обратите внимание, что каждый элемент сериализованного объекта JSON соответствует элементам типа **TestType**, определенного в нашей модели. Значения также совпадают с теми, которые использовались в коде. Однако учтите, что двоичные данные имеют кодировку base64. В данном случае значению AQID соответствует строка {0x01, 0x02, 0x03} в кодировке base64.

В этом примере показаны преимущества использования библиотеки **serializer**. Она позволяет отправлять данные JSON в облако без необходимости выполнять явную сериализацию в коде приложения. Все, что от нас требуется, — это задать в модели значения для событий, инициируемых изменением данных, а затем вызвать простые API для отправки этих событий в облако.

Используя эту информацию, вы сможете определять модели с использованием различных типов данных, включая сложные типы (мы даже можем включить одни сложные типы в другие). Но сериализованный код JSON, созданный в этом примере, поднимает один важный вопрос. *Каким образом* при отправке данных библиотека **serializer** определяет способ формирования JSON? Об этом моменте мы поговорим далее.

## <a name="more-about-serialization"></a>Дополнительные сведения о сериализации
В предыдущем разделе был приведен пример выходных данных, созданных библиотекой **serializer** . В этом разделе мы объясним, как библиотека сериализует данные и как вы можете управлять этим поведением с помощью API сериализации.

Чтобы продолжить изучение сериализации, мы создадим новую модель на основе термостата. Сначала мы приведем более подробную информацию о сценарии, который мы пытаемся реализовать.

Нам нужна модель термостата, который измеряет температуру и влажность. Каждый блок данных будет отправляться в Центр Интернета вещей по отдельности. По умолчанию термостат генерирует событие температуры каждые 2 минуты, а событие влажности — каждые 15 минут. В каждое генерируемое событие необходимо включить метку времени, в которое были измерены соответствующие показатели температуры или влажности.

На основании этого сценария мы покажем два способа моделирования данных и объясним влияние каждого из этих способов на сериализованные выходные данные.

### <a name="model-1"></a>Модель 1
Вот первый вариант модели, которая поддерживает предыдущий сценарий.

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

Обратите внимание, что модель включает два события, инициируемых изменением данных: **Temperature** и **Humidity**. В отличие от предыдущих примеров, тип каждого события представлен структурой, определенной с помощью макроса **DECLARE\_STRUCT**. Структура **TemperatureEvent** содержит значение измеренной температуры и метку времени, а структура **HumidityEvent** — значение измеренной влажности и метку времени. Эта модель естественным образом моделирует данные для описанного выше сценария. Когда мы отправляем событие в облако, мы будем отправлять либо пару значений "температура/время", либо пару значений "влажность/время".

Событие температуры можно отправить в облако с помощью следующего кода:

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

В этом примере мы используем жестко заданные значения температуры и влажности. Но предположим, что эти значения поступают от соответствующих датчиков реального термостата.

В приведенном выше примере используется вспомогательный метод **GetDateTimeOffset** , о котором было сказано ранее. По причинам, о которых будет сказано позже, задачи сериализации и отправки события в этом коде выполняются раздельно. Событие температуры сериализуется предыдущим кодом в буфер. Затем вспомогательная функция **sendMessage** (включена в приложение **simplesample\_amqp**) отправляет событие в Центр Интернета вещей:

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

Этот код является частью вспомогательного метода **SendAsync** , описанного в предыдущем разделе, поэтому мы не будем повторно рассказывать о нем.

Если запустить приведенный код для отправки события температуры, в Центр Интернета вещей отправится следующая сериализованная строка:

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

Мы отправляем значение температуры с типом **TemperatureEvent**. Эта структура содержит элементы **Temperature** и **Time**. Это напрямую отражается в сериализованных данных.

Точно так же событие влажности можно отправить с помощью следующего кода:

```
thermostat->Humidity.Humidity = 45;
thermostat->Humidity.Time = GetDateTimeOffset(now);
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

Сериализованная форма, которая отправляется в Центр Интернета вещей, выглядит так:

```
{"Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

Опять же, все как и ожидалось.

С помощью этой модели можно понять, как легко добавить дополнительные события. Можно определить дополнительные структуры с помощью макроса **DECLARE\_STRUCT** и включить соответствующее событие в модель с помощью макроса **WITH\_DATA**.

Теперь давайте изменим модель, включив в нее те же данные, но с другой структурой.

### <a name="model-2"></a>Модель 2
Рассмотрим следующую измененную модель:

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

Здесь мы убрали макрос **DECLARE\_STRUCT** и определили элементы данных из нашего сценария с помощью простых типов языка моделирования.

В данный момент не обращайте внимание на событие **Time** . Следовательно, код вызова события **Temperature**будет выглядеть так:

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

Этот код отправляет в Центр Интернета вещей следующее сериализованное событие:

```
{"Temperature":75}
```

Код для отправки события влажности выглядит так:

```
thermostat->Humidity = 45;
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

В Центр Интернета вещей отправляется следующее:

```
{"Humidity":45}
```

По-прежнему ничего непредвиденного. Теперь давайте изменим способ использования макроса SERIALIZE.

Макрос **SERIALIZE** может принимать несколько событий, инициируемых изменением данных, в качестве аргументов. Это позволит нам одновременно сериализовать события **Temperature** и **Humidity** и отправить их в Центр Интернета вещей в рамках одного вызова:

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

Как вы можете догадаться, результатом выполнения этого кода является отправка двух событий, инициируемых изменением данных, в Центр Интернета вещей:

[

{"Temperature":75},

{"Humidity":45}

]

Другими словами, можно предположить, что этот код равнозначен отправке событий **Temperature** и **Humidity** по отдельности. Это просто удобный способ передачи обоих событий в метод **SERIALIZE** одним вызовом. Однако это не так. Вместо этого, приведенный выше код отправляет в Центр Интернета вещей одно событие, инициируемое изменением данных:

{"Temperature":75, "Humidity":45}

Это может показаться странным, так как в нашей модели события **Temperature** и **Humidity** определены как два *отдельных* события:

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

Более того, в нашей модели мы не включали события **Temperature** и **Humidity** в одну структуру:

```
DECLARE_STRUCT(TemperatureAndHumidityEvent,
int, Temperature,
int, Humidity,
);

DECLARE_MODEL(Thermostat,
WITH_DATA(TemperatureAndHumidityEvent, TemperatureAndHumidity),
);
```

На примере использования этой модели будет проще понять, каким образом события **Temperature** и **Humidity** отправляются в одном сериализованном сообщении. При этом механизм действия при передаче обоих событий, инициируемых изменением данных, в метод **SERIALIZE** с помощью модели 2 может быть непонятным.

Это поведение проще понять, если знать о допущениях библиотеки **serializer** . Чтобы все прояснить, давайте вернемся к нашей модели:

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

Взгляните на эту модель в контексте объектно-ориентированного подхода. В этом случае мы моделируем физическое устройство (термостат), которое включает некие атрибуты (например, **Temperature** и **Humidity**).

Мы можем отправить общее состояние нашей модели с помощью следующего кода:

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity, thermostat->Time) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

Если указаны значения температуры, влажности и времени, в Центр Интернета вещей будет отправлено событие со следующим содержимым:

```
{"Temperature":75, "Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

Иногда вам нужно отправлять в облако значения только *некоторых* свойств модели (особенно это касается случаев, когда модель содержит большое количество событий, инициируемых изменением данных). Полезно отправлять только некоторые события, инициируемые изменением данных, как это было в примере выше:

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

В результате будет создано такое же сериализованное событие, как и при определении **TemperatureEvent** с атрибутами **Temperature** и **Time**(модель 1). За счет вызова метода **SERIALIZE** другим способом мы можем создать такое же сериализованное событие с помощью другой модели (модель 2).

Важно помнить, что при передаче в метод **SERIALIZE** нескольких событий, инициируемых изменением данных, каждое такое событие рассматривается как отдельное свойство одного объекта JSON.

Выбор наиболее подходящего подхода зависит от того, как вы воспринимаете модель. Если вы отправляете "события" в облако, когда каждое событие содержит определенный набор свойств, вам лучше выбрать первый подход. В этом случае с помощью макроса **DECLARE\_STRUCT** определяется структура каждого события, а затем они включаются в модель с помощью макроса **WITH\_DATA**. Теперь события можно отправлять, как описано в первом примере. При использовании этого подхода в метод **SERIALIZER**будет передаваться только одно событие, инициируемое изменением данных.

Если вы рассматриваете свою модель с точки зрения объектно-ориентированного подхода, вам лучше использовать второй метод. В этом случае элементы, определенные с помощью макроса **WITH\_DATA**, будут свойствами вашего объекта. В метод **SERIALIZE** вы можете передавать любое подмножество событий на основе требований к передаче данных о состоянии объекта в облако.

Ни один из подходов нельзя назвать правильным или ошибочным. Просто нужно знать о принципах работы библиотеки **serializer** и использовать тот подход к моделированию, который подходит именно вам.

## <a name="message-handling"></a>Обработка сообщений
До сих пор в этой статье рассказывалось только об отправке событий в Центр Интернета вещей, но не об их получении. Это связано с тем, что большая часть информации о получении сообщений была изложена в [предыдущей статье](iot-hub-device-sdk-c-intro.md). Как вы помните, обработка сообщений выполняется путем регистрации функции обратного вызова:

```
IoTHubClient_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather)
```

Затем вы создаете функцию обратного вызова, которая вызывается при получении сообщения:

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

Эта реализация **IoTHubMessage** обеспечивает вызов нужной функции для каждого действия, определенного в модели. Например, если модель определяет следующее действие:

```
WITH_ACTION(SetAirResistance, int, Position)
```

Вам нужно определить функцию со следующей сигнатурой:

```
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position to %d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

**SetAirResistance** вызывается при отправке сообщения устройству.

Но мы все еще не рассказали вам о том, как выглядит сериализованная версия сообщения. Другими словами, если вы хотите отправить устройству сообщение **SetAirResistance** , как оно будет выглядеть?

При отправке сообщения устройству вы используете пакет SDK для службы Azure IoT. Вам по-прежнему необходимо знать, какую строку отправить для вызова определенного действия. Общий формат отправки сообщения выглядит следующим образом:

```
{"Name" : "", "Parameters" : "" }
```

Вы отправляете сериализованный объект JSON с двумя свойствами: **Name** (имя действия/сообщения) и **Parameters** (параметры этого действия).

Например, чтобы вызвать функцию **SetAirResistance** , вам нужно отправить устройству следующее сообщение:

```
{"Name" : "SetAirResistance", "Parameters" : { "Position" : 5 }}
```

Имя действия должно совпадать с именем, определенным в модели. Имена параметров должны совпадать. Также обратите внимание на чувствительность к регистру. Параметры **Name** и **Parameters** всегда пишутся с прописной буквы. Также следите за соответствием регистра в именах действий и параметров, определенных в модели. В этом примере действие называется SetAirResistance (не setairresistance).

Два других действия **TurnFanOn** и **TurnFanOff** могут вызываться при отправке этих сообщений на устройство:

```
{"Name" : "TurnFanOn", "Parameters" : {}}
{"Name" : "TurnFanOff", "Parameters" : {}}
```

Вот и все, что вам нужно знать об отправке событий и получении сообщений с помощью библиотеки **serializer** . Прежде чем продолжить, давайте рассмотрим ряд изменяемых параметров, которые позволяют управлять размером модели.

## <a name="macro-configuration"></a>Конфигурация макросов
Если вы используете библиотеку **Serializer** , помните, что нужную вам часть пакета SDK можно найти в библиотеке azure-c-shared-utility.
Если вы клонировали репозиторий Azure-iot-sdk-с сайта GitHub, использовав параметр --recursive, то эту общедоступную библиотеку служебных программ можно найти здесь:

```
.\\c-utility
```

Если вы не клонировали библиотеку, ее можно найти [здесь](https://github.com/Azure/azure-c-shared-utility).

В общедоступной библиотеке служебных программ вы найдете следующую папку:

```
azure-c-shared-utility\\macro\_utils\_h\_generator.
```

Эта папка содержит решение Visual Studio с именем **macro\_utils\_h\_generator.sln**:

  ![](media/iot-hub-device-sdk-c-serializer/01-macro_utils_h_generator.PNG)

Программа в этом решении создает файл **macro\_utils.h**. Вместе с пакетом SDK поставляется стандартная версия файла macro\_utils.h. Это решение позволяет изменить ряд параметров, а затем повторно создать файл заголовка с учетом этих изменений.

Два ключевых параметра, о которых вам нужно знать, это **nArithmetic** и **nMacroParameters**. Они определяются в следующих двух строках кода в файле macro\_utils.tt:

```
<#int nArithmetic=1024;#>
<#int nMacroParameters=124;/*127 parameters in one macro deﬁnition in C99 in chapter 5.2.4.1 Translation limits*/#>

```

Эти значения являются стандартными для пакета SDK. Параметры означают следующее:

* nMacroParameters — определяет количество параметров в одном определении макроса DECLARE\_MODEL.
* nArithmetic — общее разрешенное количество элементов в модели.

Важность этих параметров объясняется тем, что с их помощью можно управлять размером модели. Например, возьмем следующее определение модели:

```
DECLARE_MODEL(MyModel,
WITH_DATA(int, MyData)
);
```

Как говорилось ранее, **DECLARE\_MODEL** является обычным макросом C. Имя модели и инструкция **WITH\_DATA** (еще один макрос) являются параметрами макроса **DECLARE\_MODEL**. **nMacroParameters** определяет, сколько параметров можно включить в макрос **DECLARE\_MODEL**. Фактически этот параметр определяет максимальное количество событий, инициируемых изменением данных, и объявлений действий. Таким образом, ограничение в 124 элемента означает возможность определения модели, в которой будет приблизительно по 60 действий и событий, инициируемых изменением данных. Если превысить этот предел, вы получите следующую ошибку компиляции:

  ![](media/iot-hub-device-sdk-c-serializer/02-nMacroParametersCompilerErrors.PNG)

Параметр **nArithmetic** скорее предназначен для настройки внутренних механизмов макроязыка, чем для работы приложения.  Он определяет общее допустимое количество элементов в модели, включая макрос **DECLARE_STRUCT**. Если при компиляции программы вы получаете подобные сообщения об ошибках, попробуйте увеличить значение **nArithmetic**.

   ![](media/iot-hub-device-sdk-c-serializer/03-nArithmeticCompilerErrors.PNG)

Чтобы изменить параметры, отредактируйте соответствующие значения в файле macro\_utils.tt. После этого повторно скомпилируйте решение macro\_utils\_h\_generator.sln и запустите скомпилированную программу. Будет создан новый файл macro\_utils.h, который помещается в каталог .\\common\\inc.

Чтобы использовать новую версию macro\_utils.h, удалите пакет NuGet **serializer** из решения, заменив его проектом Visual Studio **serializer**. Это позволяет вашему коду выполнить компиляцию для исходного кода библиотеки serializer. Сюда входит обновленный macro\_utils.h. Если необходимо выполнить это действие для **simplesample\_amqp**, следует сначала удалить из решения пакет NuGet для библиотеки serializer:

   ![](media/iot-hub-device-sdk-c-serializer/04-serializer-github-package.PNG)

Затем добавьте этот проект в свое решение Visual Studio:

> .\\c\\serializer\\build\\windows\\serializer.vcxproj
> 
> 

Когда все будет готово, ваше решение должно выглядеть следующим образом:

   ![](media/iot-hub-device-sdk-c-serializer/05-serializer-project.PNG)

Теперь при компиляции решения в двоичный файл будет включен обновленный macro\_utils.h.

Обратите внимание, что установка слишком большого значения может привести к превышению ограничений компилятора. Поэтому лучше сосредоточиться на параметре **nMacroParameters**. В спецификации C99 сказано, что в определении макроса допускается не менее 127 параметров. Компилятор Майкрософт точно следует этой спецификации, а также налагает максимальное ограничение в 127 параметров. Поэтому вы не сможете увеличить значение **nMacroParameters** по умолчанию. Другие компиляторы могут позволить сделать это (например, компилятор GNU поддерживает более высокое ограничение).

Таким образом, мы рассмотрели практически все, что нужно знать о написании кода при использовании библиотеки **serializer** . Прежде чем закончить, давайте вернемся к некоторым темам из предыдущих статей, которые могут вызвать у вас вопросы.

## <a name="the-lower-level-apis"></a>Интерфейсы API нижнего уровня
В этой статье мы рассмотрели пример приложения **simplesample\_amqp**. В этом примере для отправки событий и получения сообщений используется API высокого уровня (не LL). При использовании таких API запускается фоновый поток, который отвечает и за отправку событий, и за получение сообщений. Однако мы можем использовать API низкого уровня (LL), чтобы остановить этот фоновый поток и явно управлять отправкой событий или получением сообщений из облака.

Как сказано в [предыдущей статье](iot-hub-device-sdk-c-iothubclient.md), есть набор функций, которые включают в себя интерфейсы API высокого уровня:

* IoTHubClient\_CreateFromConnectionString
* IoTHubClient\_SendEventAsync
* IoTHubClient\_SetMessageCallback
* IoTHubClient\_Destroy

В примере **simplesample\_amqp** показывается, как использовать эти API.

Существует аналогичный набор API низкого уровня.

* IoTHubClient\_LL\_CreateFromConnectionString
* IoTHubClient\_LL\_SendEventAsync
* IoTHubClient\_LL\_SetMessageCallback
* IoTHubClient\_LL\_Destroy

Обратите внимание, что API низкого уровня работают точно так же, как это описано в предыдущих статьях. Первый набор API используется, когда вам нужно управлять операциями отправки событий и получения сообщений с помощью фонового потока. Но если вы хотите явно управлять отправкой и получением данных из Центра Интернета вещей, вам следует использовать второй набор API. Любой из этих наборов API работает с библиотекой **serializer** одинаково хорошо.

Пример использования интерфейсов API низкого уровня с библиотекой **serializer** см. в приложении **simplesample\_http**.

## <a name="additional-topics"></a>Дополнительные разделы
Также стоит упомянуть об обработке свойств, параметрах конфигурации и использовании дополнительных учетных данных устройства. Все эти вопросы рассматриваются в [предыдущей статье](iot-hub-device-sdk-c-iothubclient.md). Самое главное, что все эти возможности работают при использовании библиотеки **serializer** точно так же, как и при использовании библиотеки **IoTHubClient**. Например, если вы хотите присоединить свойства к событию из модели, вы можете воспользоваться функциями **IoTHubMessage\_Properties** и **Map**\_**AddorUpdate** в соответствии с описанием выше.

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

Не имеет значения, было ли создано событие вручную с помощью библиотеки **IoTHubClient** или автоматически с помощью библиотеки **serializer**.

В случае с дополнительными учетными данными для устройства функция **IoTHubClient\_LL\_Create** для выделения **IOTHUB\_CLIENT\_HANDLE** работает точно так же, как функция **IoTHubClient\_CreateFromConnectionString**.

Наконец, используя библиотеку **serializer**, вы можете настраивать параметры конфигурации с помощью функции **IoTHubClient\_LL\_SetOption** точно так же, как при использовании библиотеки **IoTHubClient**.

Единственным отличием возможностей библиотеки **serializer** является наличие API-интерфейсов инициализации. Перед началом работы с библиотекой необходимо вызвать **serializer\_init**:

```
serializer_init(NULL);
```

Это делается непосредственно перед вызовом метода **IoTHubClient\_CreateFromConnectionString**.

Соответственно, после завершения работы с библиотекой вызывается метод **serializer\_deinit**:

```
serializer_deinit();
```

Все прочие описанные выше функции работают с библиотекой **serializer** точно так же, как и с библиотекой **IoTHubClient**. Дополнительные сведения см. в [предыдущей статье](iot-hub-device-sdk-c-iothubclient.md) этого цикла.

## <a name="next-steps"></a>Дальнейшие действия
В этой статье подробно рассматриваются уникальные возможности библиотеки **serializer**, включенной в **пакет SDK для устройств Azure IoT для C**. Прочитав эту статью, вы узнаете, как использовать модели для отправки событий и получения сообщений из Центра Интернета вещей.

Эта статья завершает цикл из трех частей, посвященный разработке приложений с помощью **пакета SDK для устройств Azure IoT для C**. Приведенной информации должно быть достаточно для того, чтобы вы могли не только приступить к работе, но и лучше понять принципы работы API. Дополнительные сведения можно получить из нескольких примеров в пакете SDK, не описанных в этой статье. Еще одним источником дополнительной информации является [документация по пакету SDK](https://github.com/Azure/azure-iot-sdk-c) .

Дополнительные сведения о разработке для Центра Интернета вещей см. в статье [Пакеты SDK для Центра Интернета вещей][lnk-sdks].

Для дальнейшего изучения возможностей Центра Интернета вещей см. следующие статьи:

* [Развертывание Azure IoT Edge на имитированном устройстве в Linux (предварительная версия)][lnk-iotedge]

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: ../iot-edge/tutorial-simulate-device-linux.md
