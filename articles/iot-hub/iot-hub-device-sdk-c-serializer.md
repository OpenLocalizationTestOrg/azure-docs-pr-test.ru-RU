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
# <a name="azure-iot-device-sdk-for-c--more-about-serializer"></a>Пакет SDK для устройств Azure IoT для C — дополнительные сведения о сериализаторе
Hello [сначала статьи](iot-hub-device-sdk-c-intro.md) в этой серии появился hello **устройств Azure IoT SDK для C**. hello следующей статье содержатся более подробное описание hello [ **IoTHubClient** ](iot-hub-device-sdk-c-iothubclient.md). В этой статье завершения покрытие hello SDK, предоставляя более подробное описание hello оставшихся компонента: hello **сериализатор** библиотеки.

описано, каким образом вводная статья Hello toouse hello **сериализатор** библиотеки toosend события tooand получать сообщения от центра IoT. В этой статье мы расширяют обсуждение этой темы, предоставляя более подробное описание того, как toomodel данных с помощью hello **сериализатор** макрос языка. статья Hello также включает более подробные сведения о как библиотека hello сериализацию сообщений (и в некоторых случаях способы управления поведением при сериализации hello). Также мы опишем некоторые, можно изменить параметры, определяющие размер hello создаваемые модели hello.

Наконец некоторые разделы, описанные в предыдущих статей, такие как сообщения и обработка свойство последующих посещениях hello статьи. Как мы объясним, такие рабочие функции в hello же с помощью hello **сериализатор** библиотеки, как с hello **IoTHubClient** библиотеки.

Все описанные в этой статье основан на hello **сериализатор** образцов SDK. Следует toofollow вдоль разделе hello **simplesample\_amqp** и **simplesample\_http** приложений, включенных в пакет SDK устройства Azure IoT hello C.

Можно найти hello [ **устройств Azure IoT SDK для C** ](https://github.com/Azure/azure-iot-sdk-c) GitHub репозитория и просмотра сведений из hello API в hello [Справочник по C API](https://azure.github.io/azure-iot-sdk-c/index.html).

## <a name="hello-modeling-language"></a>языка моделирования Hello
Hello [вводной статье](iot-hub-device-sdk-c-intro.md) в этой серии появился hello **устройств Azure IoT SDK для C** язык через hello примера, приведенного в hello моделирования **simplesample\_amqp**  приложения:

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

Как видите, язык моделирования hello основан на макросов C. Определение всегда начинается с ключевого слова **BEGIN\_NAMESPACE** и всегда заканчивается ключевым словом **END\_NAMESPACE**. Это общее tooname hello пространство имен для вашей компании или, как в этом примере hello проекта, над которыми вы работаете.

Что происходит внутри пространства имен hello, определения модели. В данном случае создается одна модель для анемометра. Опять же, hello модели можно присвоить любое имя, но обычно это имя для устройства hello или тип данных требуется tooexchange с центром IoT.  

Модели содержат определение hello событий можно tooIoT входящих концентратора (hello *данные*) а также можно получать из центра IoT сообщений hello (hello *действия*). Как видно из примера hello события имеют типом и именем. действия есть имя и необязательные параметры (каждый с типом).

При этом не демонстрируется в данном примере — дополнительные типы данных, поддерживаемые hello SDK. Об этом мы поговорим далее.

> [!NOTE]
> Центр IoT ссылается устройство отправляет tooit как данные toohello *события*, в то время язык моделирования hello ссылается tooit как *данные* (определяются с помощью **WITH_DATA**). Аналогично, центр IoT ссылается toohello данных, отправляемых toodevices как *сообщений*, в то время язык моделирования hello ссылается tooit как *действия* (определяются с помощью **WITH_ACTION**). Помните, что в этой статье данные понятия могут быть взаимозаменяемыми.
> 
> 

### <a name="supported-data-types"></a>Поддерживаемые типы данных.
Привет, следующие типы данных поддерживаются в модели, созданные с помощью hello **сериализатор** библиотеки:

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

Давайте начнем с типом данных последнего hello. Hello **DECLARE\_СТРУКТУРЫ** позволяет toodefine сложные типы данных, которые группируют hello других типов-примитивов. Такие группы позволяют нам toodefine модель, которая выглядит следующим образом:

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

Наша модель содержит одно событие, инициируемое изменением данных, типа **TestType**. **TestType** — это сложный тип, который включает в себя несколько элементов, которые вместе демонстрируют hello примитивные типы, поддерживаемые hello **сериализатор** язык моделирования.

С моделью следующим образом можно написать код toosend данных tooIoT концентратор, который выглядит следующим образом:

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

По сути, назначение значение tooevery членом hello **теста** структуры и последующего вызова **SendAsync** toosend hello **тест** облако toohello данных события. **SendAsync** является вспомогательная функция, которая отправляет одно событие tooIoT концентратора:

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

Эта функция сериализует заданное событие данных hello и отправляет его tooIoT концентратора с помощью **IoTHubClient\_SendEventAsync**. Это hello того же кода описано в предыдущей статьи (**SendAsync** инкапсулирует логику hello в удобном функцию).

— Одна вспомогательная функция, используемый в предыдущем примере кода hello **GetDateTimeOffset**. Эта функция преобразует hello конкретный момент времени в значение типа **EDM\_даты\_время\_СМЕЩЕНИЕ**:

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

При выполнении этого кода hello сообщением отправляется tooIoT концентратора.

```
{"aDouble":1.100000000000000, "aInt":2, "aFloat":3.000000, "aLong":4, "aInt8":5, "auInt8":6, "aInt16":7, "aInt32":8, "aInt64":9, "aBool":true, "aAsciiCharPtr":"ascii string 1", "aDateTimeOffset":"2015-09-14T21:18:21Z", "aGuid":"00010203-0405-0607-0809-0A0B0C0D0E0F", "aBinary":"AQID"}
```

Обратите внимание, что hello сериализации JSON, создаваемых hello формата hello по **сериализатор** библиотеки. Также Обратите внимание, что каждый член hello сериализованный объект JSON соответствует hello члены hello **TestType** , определенный в нашей модели. значения Hello также совпадать тех, которые используются в коде hello. Тем не менее, обратите внимание, что hello двоичных данных в base64-кодировке: «AQID» Здравствуйте, кодирование base64 {0x01, 0x02, 0x03}.

В этом примере демонстрируется hello преимуществом использования hello **сериализатор** библиотеки — это позволяет нам облака toohello toosend JSON, без необходимости иметь дело с сериализацией, в нашем приложении tooexplicitly. Все, что у нас есть tooworry о устанавливать значения hello hello событий данных в нашей модели и затем вызвать простой API-интерфейсы toosend облака toohello этих событий.

Эти сведения позволяют определить модели, которые включают hello диапазон поддерживаемых типов данных, включая сложные типы (мы может даже содержать сложные типы в других сложных типов). Тем не менее, он сериализации JSON, созданная по hello приведенном выше примере появится важное правило. *Как* мы отправлять данные с hello **сериализатор** библиотека определяет точно, как сформировано hello JSON. Об этом моменте мы поговорим далее.

## <a name="more-about-serialization"></a>Дополнительные сведения о сериализации
Пример hello выходных hello выделяет Hello предыдущего раздела **сериализатор** библиотеки. В этом разделе объясняется, как библиотека hello сериализует данные и как можно контролировать это поведение, используя hello сериализацией API.

При обсуждении hello tooadvance порядок сериализации мы будем работать с учетом термостат новой модели. Во-первых давайте предоставит некоторые сведения в сценарии hello пытаетесь tooaddress.

Мы хотим toomodel термостат, что меры, температуры и влажности. Каждый фрагмент данных будет отправлено tooIoT концентратора по-разному toobe. По умолчанию hello термостат ingresses событий температуры каждые 2 минуты; событие влажности ingressed каждые 15 минут. После любого события ingressed, он должен содержать отметку времени, показывающий время hello соответствующего температура hello или измерялась влажности.

Это позволит мы продемонстрируем данных hello toomodel двумя различными способами и мы расскажем hello эффект, что моделирования на hello сериализации выходных данных.

### <a name="model-1"></a>Модель 1
Вот hello первой версии модели, поддерживает hello предыдущего сценария.

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

Обратите внимание, что hello модель включает в себя два события данных: **температуры** и **влажность**. В отличие от предыдущих примерах hello тип каждого события — это структура, определенная с помощью **DECLARE\_СТРУКТУРЫ**. Структура **TemperatureEvent** содержит значение измеренной температуры и метку времени, а структура **HumidityEvent** — значение измеренной влажности и метку времени. Эта модель дает нам данных Здравствуй естественным способом toomodel для hello сценария, описанных выше. Когда мы отправляем в облаке toohello события, либо мы будем отправлять температуры или отметки времени или пару влажности или отметки времени.

Мы можем отправить toohello облака температуры событий с помощью кода, подобного hello далее:

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

Мы рассмотрим использовать жестко запрограммированные значения температуры и влажности в примере кода hello, но Предположим, что мы фактически извлекаются эти значения с помощью выборки hello соответствующего датчиков термостат hello.

Приведенный выше код Hello использует hello **GetDateTimeOffset** помощник, который был введен ранее. По причинам, которые станут снимите более поздней версии этот код явным образом разделяет задачу hello сериализации и отправлять события hello. Hello предыдущий код сериализует событие температуры hello в буфер. Затем **sendMessage** — это вспомогательная функция (включен в **simplesample\_amqp**), отправляет hello tooIoT события концентратора:

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

Этот код является подмножеством hello **SendAsync** вспомогательный, описанные в предыдущем разделе hello, поэтому мы не будем останавливаться на него еще раз здесь.

При запуске hello предыдущего кода toosend hello температуры события, это сериализованную форму события hello отправляется tooIoT концентратора.

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

Мы отправляем значение температуры с типом **TemperatureEvent**. Эта структура содержит элементы **Temperature** и **Time**. Непосредственно отражается в данных сериализации hello.

Точно так же событие влажности можно отправить с помощью следующего кода:

```
thermostat->Humidity.Humidity = 45;
thermostat->Humidity.Time = GetDateTimeOffset(now);
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

форма сериализации Hello, отправил tooIoT концентратора выглядит следующим образом:

```
{"Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

Опять же, все как и ожидалось.

С помощью этой модели можно понять, как легко добавить дополнительные события. Определите несколько структур с помощью **DECLARE\_СТРУКТУРЫ**и включить соответствующее событие hello в модели с помощью hello **WITH\_данных**.

Теперь изменим hello модели, чтобы оно включало hello и те же данные, но с другой структурой.

### <a name="model-2"></a>Модель 2
Рассмотрим этот toohello альтернативные модели один выше.

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

В этом случае мы исключены hello **DECLARE\_СТРУКТУРЫ** макросы и просто определяете hello элементов данных в нашем сценарии, используя простые типы hello язык моделирования.

Только для hello момента давайте игнорировать hello **время** событий. С этой отдельно от Вот tooingress кода hello **температуры**:

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

Этот код отправляет следующие hello сериализации событий tooIoT концентратора:

```
{"Temperature":75}
```

И hello кода для отправки событий влажности hello имеет следующий вид:

```
thermostat->Humidity = 45;
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

Этот код отправляет этот tooIoT концентратора:

```
{"Humidity":45}
```

По-прежнему ничего непредвиденного. Теперь изменим, как использовать макрос SERIALIZE hello.

Hello **СЕРИАЛИЗАЦИИ** макрос может занять несколько событий данных как аргументы. Это позволяет нам tooserialize hello **температуры** и **влажность** событий вместе и отправить их tooIoT концентратора в одном вызове:

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

Вы можете догадаться, что hello этот код образом, два элемента данных события отправляются tooIoT концентратора:

[

{"Temperature":75},

{"Humidity":45}

]

Другими словами, можно предположить, что этот код является hello же, как и отправка **температуры** и **влажность** отдельно. Это просто toopass удобства обоих событий слишком**СЕРИАЛИЗАЦИИ** в hello же вызвать. Однако это не так hello. Вместо этого приведенный выше код hello отправляет этот tooIoT событий данных single концентратора:

{"Temperature":75, "Humidity":45}

Это может показаться странным, так как в нашей модели события **Temperature** и **Humidity** определены как два *отдельных* события:

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

Дополнительные точки toohello, мы не этих событий модели где **температуры** и **влажность** в hello структуру:

```
DECLARE_STRUCT(TemperatureAndHumidityEvent,
int, Temperature,
int, Humidity,
);

DECLARE_MODEL(Thermostat,
WITH_DATA(TemperatureAndHumidityEvent, TemperatureAndHumidity),
);
```

При использовании этой модели, было бы проще toounderstand как **температуры** и **влажность** были бы отправлены в hello же сериализованное сообщение. Однако он не может очистить почему работает таким образом, при передаче обоих событий данных слишком**СЕРИАЛИЗАЦИИ** с помощью модели 2.

Это упрощает toounderstand Если известно, hello предположения hello **сериализатор** делает библиотеки. toomake смысле это давайте рассмотрим задней tooour модели:

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

Взгляните на эту модель в контексте объектно-ориентированного подхода. В этом случае мы моделируем физическое устройство (термостат), которое включает некие атрибуты (например, **Temperature** и **Humidity**).

Мы можем отправить hello полное состояние нашей модели с кодом, например hello следующее:

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity, thermostat->Time) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

При условии, что значения hello температура, влажность и время установлены, можно увидеть события, например, это отправленных tooIoT концентратора:

```
{"Temperature":75, "Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

Иногда может быть только toosend *некоторые* свойств hello модели toohello облака (Это особенно важно, если модель содержит большое количество данных событий). Это полезно toosend только подмножество данных событий, таких как в примере выше:

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

Это приводит к возникновению ошибки точно hello же сериализации событий, как если мы определили **TemperatureEvent** с **температуры** и **время** члена, так же, как мы с модель 1. В этом случае мы были может toogenerate точно hello же сериализации событий с помощью другой модели (модель 2), так как мы позвонили **СЕРИАЛИЗАЦИИ** по-разному.

Hello важно, что при передаче нескольких событий данных слишком**СЕРИАЛИЗАЦИИ,** то предполагается, что каждое событие — это свойство в единый объект JSON.

Hello наилучший подход зависит от того, и каким образом вы думаете о модели. Если вы отправляете сообщение «события» toohello облака, и каждое событие содержит определенный набор свойств, hello первый подход делает смысл. В этом случае используется **DECLARE\_СТРУКТУРЫ** toodefine hello структуру каждого события, а затем включить их в модели с помощью hello **WITH\_данные** макрос. Затем отправить каждого события, как это делалось в первом примере hello выше. При таком подходе следует только передавать события одного данных слишком**СЕРИАЛИЗАТОР**.

Если вы думаете о модели в виде объекта, hello второй подход может подойти вы. В этом случае hello элементов, определенных с помощью **WITH\_данные** hello «свойства» объекта. Можно передать любое подмножество событий слишком**СЕРИАЛИЗАЦИИ** том, что вам нравится, в зависимости от того сколько состояния «объекта» требуется toosend toohello облака.

Ни один из подходов нельзя назвать правильным или ошибочным. Необходимо знать, как hello **сериализатор** библиотека работает, а также выбора hello моделирования подход, который наилучшим образом соответствует вашим потребностям.

## <a name="message-handling"></a>Обработка сообщений
До сих в этой статье только обсуждались отправки событий tooIoT концентратора и не разрешены получения сообщений. Здравствуйте, причина этого является то, что мы должны tooknow о получении сообщений во многом были описаны в [ранее статье](iot-hub-device-sdk-c-intro.md). Как вы помните, обработка сообщений выполняется путем регистрации функции обратного вызова:

```
IoTHubClient_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather)
```

Затем создайте hello функции обратного вызова, вызываемый при получении сообщения.

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

Эта реализация **IoTHubMessage** вызовы hello определенную функцию для каждого действия в модели. Например, если модель определяет следующее действие:

```
WITH_ACTION(SetAirResistance, int, Position)
```

Вам нужно определить функцию со следующей сигнатурой:

```
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position too%d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

**SetAirResistance** вызывается, когда это сообщение отправляется tooyour устройства.

Еще какие еще не описано: hello сериализации версии выглядит сообщение. Другими словами Если требуется, чтобы toosend **SetAirResistance** устройства tooyour сообщения, как выглядит этот?

При отправке сообщения tooa устройство, это следует делать через службу hello Azure IoT SDK. По-прежнему необходимо tooknow какая строка toosend tooinvoke определенное действие. общий формат Hello отправляет сообщение выглядит следующим образом:

```
{"Name" : "", "Parameters" : "" }
```

Вы отправляете сообщение сериализованный объект JSON с двумя свойствами: **имя** — имя hello действие hello (сообщение) и **параметры** содержит параметры hello этого действия.

Например, tooinvoke **SetAirResistance** можно отправить это сообщение tooa устройство:

```
{"Name" : "SetAirResistance", "Parameters" : { "Position" : 5 }}
```

Имя действия Hello должен точно соответствовать действие, определенный в модели. также должны совпадать имена параметров Hello. Также обратите внимание на чувствительность к регистру. Параметры **Name** и **Parameters** всегда пишутся с прописной буквы. Убедиться, что вариант hello toomatch имя действия и параметров в модели. В этом примере hello действие названо «SetAirResistance» и не «setairresistance».

Здравствуйте, два действия **TurnFanOn** и **TurnFanOff** можно вызвать путем отправки этих сообщений tooa устройства:

```
{"Name" : "TurnFanOn", "Parameters" : {}}
{"Name" : "TurnFanOff", "Parameters" : {}}
```

В этом разделе описано все, что нужно tooknow при отправки событий и получение сообщений с использованием hello **сериализатор** библиотеки. Прежде чем продолжить, давайте рассмотрим ряд изменяемых параметров, которые позволяют управлять размером модели.

## <a name="macro-configuration"></a>Конфигурация макросов
Если вы используете hello **сериализатор** библиотеки важной частью учитывать toobe SDK hello, найденной в hello azure-c общей-библиотека программы.
При клонировании репозитория hello Azure iot-sdk c из GitHub, с помощью параметра--рекурсивные hello вы найдете Эта библиотека общей программы.

```
.\\c-utility
```

Если вы не клонировали hello библиотеки, его можно будет найти [здесь](https://github.com/Azure/azure-c-shared-utility).

Библиотека общих программы hello приведена hello следующие папки:

```
azure-c-shared-utility\\macro\_utils\_h\_generator.
```

Эта папка содержит решение Visual Studio с именем **macro\_utils\_h\_generator.sln**:

  ![](media/iot-hub-device-sdk-c-serializer/01-macro_utils_h_generator.PNG)

Программа Hello в это решение создает hello **макрос\_utils.h** файла. Что представляет собой макрос, по умолчанию\_utils.h файл, входящий в состав пакета SDK для hello. Это решение позволяет toomodify некоторых параметров и затем повторно создайте hello файл заголовка, на основе этих параметров.

являются Hello двух ключевых параметров, посвящена toobe **nArithmetic** и **nMacroParameters** которые определены в эти две строки, найден в макросе\_utils.tt:

```
<#int nArithmetic=1024;#>
<#int nMacroParameters=124;/*127 parameters in one macro deﬁnition in C99 in chapter 5.2.4.1 Translation limits*/#>

```

Эти значения являются параметрами по умолчанию hello, входящий в состав пакета SDK для hello. Каждый параметр имеет hello следующие значения:

* nMacroParameters — определяет количество параметров в одном определении макроса DECLARE\_MODEL.
* nArithmetic — элементы управления hello общее количество элементов, допустимое в модели.

Hello эти параметры важны, поскольку они управляют размер может быть модели. Например, возьмем следующее определение модели:

```
DECLARE_MODEL(MyModel,
WITH_DATA(int, MyData)
);
```

Как говорилось ранее, **DECLARE\_MODEL** является обычным макросом C. Здравствуйте, имена модели hello и hello **WITH\_данные** инструкции (пока еще другой макрос) — параметры **DECLARE\_МОДЕЛИ**. **nMacroParameters** определяет, сколько параметров можно включить в макрос **DECLARE\_MODEL**. Фактически этот параметр определяет максимальное количество событий, инициируемых изменением данных, и объявлений действий. Таким образом ограничение по умолчанию hello в 124 это означает, что можно определить модель используется сочетание около 60 действия и данные события. При попытке tooexceed это ограничение, вы получите ошибки компилятора, которые выглядят примерно toothis:

  ![](media/iot-hub-device-sdk-c-serializer/02-nMacroParametersCompilerErrors.PNG)

Hello **nArithmetic** параметра приведены дополнительные сведения о механизмах hello языка макрос hello, чем приложения.  Он управляет hello общее количество элементов, что в модели, включая **DECLARE_STRUCT** макросы. Если при компиляции программы вы получаете подобные сообщения об ошибках, попробуйте увеличить значение **nArithmetic**.

   ![](media/iot-hub-device-sdk-c-serializer/03-nArithmeticCompilerErrors.PNG)

Toochange эти параметры, изменить значения hello в макросе hello\_utils.tt файл, макрос hello recompile\_utils\_h\_generator.sln решение, а также выполнения hello скомпилированная программа. После этого, макрос\_utils.h файл создается и помещается в hello.\\ Общие\\inc каталога.

В новой версии заказа toouse hello макроса\_utils.h, удалите hello **сериализатор** пакет NuGet из решения и вместо него включают hello **сериализатор** проекта Visual Studio. Это позволяет toocompile ваш код от исходного кода hello hello сериализатор библиотеки. Сюда входят hello обновлены макрос\_utils.h. Если требуется toodo для **simplesample\_amqp**, удалите пакет NuGet hello hello сериализатор библиотеки из hello решения:

   ![](media/iot-hub-device-sdk-c-serializer/04-serializer-github-package.PNG)

Затем добавьте этот tooyour проект решения Visual Studio:

> .\\c\\serializer\\build\\windows\\serializer.vcxproj
> 
> 

Когда все будет готово, ваше решение должно выглядеть следующим образом:

   ![](media/iot-hub-device-sdk-c-serializer/05-serializer-project.PNG)

Теперь при компиляции решения, hello обновлены макрос\_utils.h включается в двоичный файл.

Обратите внимание, что установка слишком большого значения может привести к превышению ограничений компилятора. toothis точки hello **nMacroParameters** hello основной параметр с какой toobe беспокоиться. спецификации C99 Hello указывает, что допускается менее 127 параметров в определении макроса. Hello компилятор Microsoft точно соответствует спецификации hello (и существует ограничение в 127), поэтому его нельзя будет tooincrease **nMacroParameters** за пределы по умолчанию hello. Другие компиляторы могут позволять toodo так (например, компилятор GNU hello поддерживает более высокий предел).

Пока мы рассмотрели практически все, что нужно tooknow о том, как код toowrite с hello **сериализатор** библиотеки. Прежде чем закончить, давайте вернемся к некоторым темам из предыдущих статей, которые могут вызвать у вас вопросы.

## <a name="hello-lower-level-apis"></a>Hello более низкого уровня API-интерфейсы
Пример приложения Hello фокусе в этой статье — **simplesample\_amqp**. Этот образец использует hello более высокого уровня (hello не — "LL») API-интерфейсы toosend события и получать сообщения. При использовании таких API запускается фоновый поток, который отвечает и за отправку событий, и за получение сообщений. Тем не менее можно использовать hello более низкого уровня (все) API-интерфейсы tooeliminate это фоновый поток и занять явный контроль над при отправки событий или получения сообщений из облака hello.

Как описано в [предыдущей статьи](iot-hub-device-sdk-c-iothubclient.md), имеется ряд функций, состоящий из hello более высокого уровня API-интерфейсы:

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

Обратите внимание, что точно hello hello более низкого уровня API-интерфейсы рабочих, так же, как описано в предыдущей статьи hello. Hello первый набор API-интерфейсов можно использовать, если требуется, чтобы фоновый поток toohandle события отправки и получения сообщений. Hello второй набор API-интерфейсов используется в том случае, если требуется явный контроль над при отправке и получении данных из центра IoT. Любой набор API-интерфейсы работы одинаково хорошо с hello **сериализатор** библиотеки.

Пример того, как hello более низкого уровня API используются с hello **сериализатор** библиотеки, в разделе hello **simplesample\_http** приложения.

## <a name="additional-topics"></a>Дополнительные разделы
Также стоит упомянуть об обработке свойств, параметрах конфигурации и использовании дополнительных учетных данных устройства. Все эти вопросы рассматриваются в [предыдущей статье](iot-hub-device-sdk-c-iothubclient.md). Hello главное, что все эти возможности работать в hello таким же образом с hello **сериализатор** библиотеки, как с hello **IoTHubClient** библиотеки. Например, если нужно tooattach свойства tooan событие из модели используется **IoTHubMessage\_свойства** и **карты**\_**AddorUpdate**, hello так же, как было описано выше:

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

Было ли создано событие hello из hello **сериализатор** библиотеки или создан вручную с помощью hello **IoTHubClient** библиотека не имеет значения.

Для hello альтернативные учетные данные устройства, с помощью **IoTHubClient\_LL\_создать** работает точно так же как **IoTHubClient\_CreateFromConnectionString** для Выделение **центром IOT\_КЛИЕНТА\_ОБРАБОТКИ**.

Наконец Если вы используете hello **сериализатор** библиотеки, можно задать параметры конфигурации с **IoTHubClient\_LL\_SetOption** так же, как это было сделано при использовании hello **IoTHubClient** библиотеки.

Функцию, которая уникальным toohello **сериализатор** библиотеки являются hello инициализации API-интерфейсы. Перед началом работы с библиотекой hello, необходимо вызвать **сериализатор\_init**:

```
serializer_init(NULL);
```

Это делается непосредственно перед вызовом метода **IoTHubClient\_CreateFromConnectionString**.

Аналогичным образом, после завершения работы с библиотекой hello последнего вызова hello вносятся задано слишком**сериализатор\_deinit**:

```
serializer_deinit();
```

В противном случае все hello другие функции, перечисленные выше рабочие же hello в hello **сериализатор** библиотеки, как в hello **IoTHubClient** библиотеки. Дополнительные сведения о каких-либо из следующих разделов в статье hello [предыдущей статьи](iot-hub-device-sdk-c-iothubclient.md) этой серии.

## <a name="next-steps"></a>Дальнейшие действия
В этой статье описывается в подробности hello уникальные характеристики hello **сериализатор** библиотеки, содержащихся в hello **устройств Azure IoT SDK для C**. С hello сведения, предоставленные нужно хорошо понимать как toouse моделирует toosend события и получать сообщения от центра IoT.

Это также завершает hello трех выпусков на как hello toodevelop приложений с помощью **устройств Azure IoT SDK для C**. Это должен быть достаточно только get сведения toonot которой была начата, но позволяют глубокого понимания принципов работы hello API-интерфейсы. Дополнительные сведения существует несколько образцов в приветствия SDK здесь не описаны. В противном случае hello [документации по пакету SDK](https://github.com/Azure/azure-iot-sdk-c) является ценным ресурсом для получения дополнительных сведений.

toolearn Дополнительные сведения о разработке приложений для центра IoT. в разделе hello [пакеты SDK Azure IoT][lnk-sdks].

Изучение возможностей hello центра IoT toofurther см. в разделе:

* [Отправка сообщений с устройства в облако с помощью имитации устройства (Linux) с использованием Edge Интернета вещей Azure][lnk-iotedge]

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
