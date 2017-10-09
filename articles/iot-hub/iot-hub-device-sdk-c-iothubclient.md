---
title: "устройств IoT aaaAzure пакета SDK для C - IoTHubClient | Документы Microsoft"
description: "Как библиотеки IoTHubClient toouse hello в пакет SDK устройства Azure IoT hello C toocreate для приложений для устройств, которые взаимодействуют с центра IoT."
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
ms.openlocfilehash: d1ece79e9ba6d1e5fd45cabb8fca393b24052e07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-device-sdk-for-c--more-about-iothubclient"></a>Пакет SDK для устройств Azure IoT для C — дополнительные сведения о библиотеке IoTHubClient
Hello [сначала статьи](iot-hub-device-sdk-c-intro.md) в этой серии появился hello **устройств Azure IoT SDK для C**. В ней объяснялось, что в пакете SDK есть два архитектурных уровня. Является базовым hello hello **IoTHubClient** библиотеки, который непосредственно управляет связью с центром IoT. Имеется также hello **сериализатор** библиотеки, созданный на основе этой tooprovide службы сериализации. В этой статье мы предоставим Дополнительные сведения на hello **IoTHubClient** библиотеки.

Hello предыдущей статье описано, как toouse hello **IoTHubClient** tooIoT события toosend библиотеки концентратора и получать сообщения. В этой статье расширяет обсуждение этой темы, объясняющий, как точно управлять toomore *при* отправки и получения данных, общие сведения о toohello **более низкого уровня API-интерфейсы**. Вы также узнаете как tooevents свойства tooattach (и извлекать их из сообщений) с помощью свойства hello обработки возможности hello **IoTHubClient** библиотеки. Наконец, мы предоставим дополнительное объяснение способов toohandle сообщения, полученные из центра IoT.

Hello статьи по завершении охватывают несколько различные разделы, включая дополнительные сведения об устройстве, и как toochange hello поведение hello **IoTHubClient** через параметры конфигурации.

Мы будем использовать hello **IoTHubClient** SDK образцы tooexplain эти разделы. Следует toofollow вдоль разделе hello **центром IOT\_клиента\_пример\_http** и **центром IOT\_клиента\_пример\_amqp** приложений, включенных в пакет SDK устройства Azure IoT hello для C. все описанные в следующих разделах hello показано в этих примерах.

Можно найти hello [ **устройств Azure IoT SDK для C** ](https://github.com/Azure/azure-iot-sdk-c) GitHub репозитория и просмотра сведений из hello API в hello [Справочник по C API](https://azure.github.io/azure-iot-sdk-c/index.html).

## <a name="hello-lower-level-apis"></a>Hello более низкого уровня API-интерфейсы
Hello предыдущей статьи описано hello основные операции hello **IotHubClient** в контексте hello hello **центром IOT\_клиента\_пример\_amqp** приложение. Например описано, как tooinitialize hello библиотеки с помощью следующего кода.

```
IOTHUB_CLIENT_HANDLE iotHubClientHandle;
iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, AMQP_Protocol);
```

Также описывается, как с помощью этого события toosend вызов функции.

```
IoTHubClient_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message);
```

Hello статье также описывается способ tooreceive сообщений путем регистрации функции обратного вызова.

```
int receiveContext = 0;
IoTHubClient_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext);
```

статья Hello также показал, как toofree ресурсов с помощью кода hello ниже.

```
IoTHubClient_Destroy(iotHubClientHandle);
```

Однако существует дополнительное tooeach функции этих API-интерфейсов:

* IoTHubClient\_LL\_CreateFromConnectionString
* IoTHubClient\_LL\_SendEventAsync
* IoTHubClient\_LL\_SetMessageCallback
* IoTHubClient\_LL\_Destroy

Все эти функции включают «LL» в имени API hello. За исключением этого каждая из этих функций hello параметры являются аналогами идентичные tootheir не LL. Тем не менее поведение этих функций hello отличается одно важное отличие.

При вызове **IoTHubClient\_CreateFromConnectionString**, библиотеки базовых hello создать новый поток, который выполняется в фоновом режиме hello. Этот поток отправляет события в центр IoT и принимает сообщения из него. Потока не создается при работе с hello «LL» API-интерфейсы. Создание Hello hello фонового потока — разработчик toohello удобства. У вас нет tooworry о явно отправки событий и получения сообщений от центра IoT — это происходит автоматически в фоновом режиме hello. Напротив hello «LL» API-интерфейсы позволяют явный контроль над связи с центром IoT, при необходимости.

toounderstand этого лучше, давайте рассмотрим пример:

При вызове **IoTHubClient\_SendEventAsync**, фактически это помещает hello событий в буфере. Здравствуйте, фоновый поток, созданные при вызове **IoTHubClient\_CreateFromConnectionString** постоянно отслеживает этот буфер и отправлять любые данные, он содержит tooIoT концентратора. Это происходит в фоновом режиме hello в hello одновременную, hello основной поток выполняет другую работу.

Аналогично, при регистрации функции обратного вызова для сообщения с помощью **IoTHubClient\_SetMessageCallback**, указывающей hello SDK toohave hello фона потока вызвать функцию обратного вызова hello после сообщения Получено, независимо от основного потока hello.

Hello «LL» API-интерфейсов нельзя создавать в фоновом потоке. Вместо этого новый API необходимо вызвать tooexplicitly отправки и получения данных из центра IoT. Это показано в следующий пример hello.

Hello **центром IOT\_клиента\_пример\_http** приложения, включенного в SDK демонстрирует hello hello API-интерфейсы более низкого уровня. В этом примере мы отправлять tooIoT события концентратора с кодом, например hello следующее:

```
EVENT_INSTANCE message;
sprintf_s(msgText, sizeof(msgText), "Message_%d_From_IoTHubClient_LL_Over_HTTP", i);
message.messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText));

IoTHubClient_LL_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message)
```

Hello первых трех строк создания приветственных сообщений и последнюю строку hello отправляет событие hello. Тем не менее как упоминалось ранее, «отправка» hello событий означает, что данные hello просто помещаются в буфер. Ничего не передается в сети hello при мы называем **IoTHubClient\_LL\_SendEventAsync**. Порядок tooactually входящих сообщений hello данных tooIoT концентратора, необходимо вызвать **IoTHubClient\_LL\_DoWork**, как показано в этом примере:

```
while (1)
{
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1000);
}
```

Этот код (от hello **центром IOT\_клиента\_пример\_http** приложения) многократно вызывает **IoTHubClient\_LL\_DoWork** . Каждый раз **IoTHubClient\_LL\_DoWork** — вызывается, он отправляет некоторые события из буфера hello tooIoT концентратора, он получает сообщение из очереди отправки toohello устройства. Hello последнем случае означает, что если мы регистрации функции обратного вызова для сообщения, а затем hello обратном вызове (при условии, что все сообщения в очередь). Мы бы регистрации функции обратного вызова с кодом, например hello следующее:

```
IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext)
```

Hello причина, по которой **IoTHubClient\_LL\_DoWork** обычно вызывается цикле является при каждом вызове, он отправляет *некоторые* буферизованный tooIoT события концентратора и извлекает *hello рядом* сообщения в очередь для устройства hello. Каждый вызов функции не гарантируется события toosend в буфер или tooretrieve всех обновляемых посредством очередей сообщений. Если требуется, чтобы toosend все события в hello буфер и затем продолжите на другие операции по обработке этого цикла можно заменить кода, подобного hello далее:

```
IOTHUB_CLIENT_STATUS status;

while ((IoTHubClient_LL_GetSendStatus(iotHubClientHandle, &status) == IOTHUB_CLIENT_OK) && (status == IOTHUB_CLIENT_SEND_STATUS_BUSY))
{
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1000);
}
```

Этот код вызывает **IoTHubClient\_LL\_DoWork** до всех событий в буфере hello отправки tooIoT концентратора. Обратите внимание, что это не означает, что все сообщения из очереди получены. Часть hello причина этого состоит в том, что проверка сообщений, «все» не как детерминированные действие. Что происходит при извлечении «all» сообщений hello, но еще один отправляется toohello устройства сразу же после? Лучше toodeal способом, — с программируемых истечения времени ожидания. Например функция обратного вызова сообщение hello могли сбросить таймер при каждом вызове. После этого можно написать обработки логики toocontinue Если, например, сообщения не были получены в hello последнего *X* секунд.

Все события завершения ingressing при получение сообщений, быть tooclean hello соответствующий toocall убедиться, что функция ресурсов.

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

По сути является только один набор API-интерфейсов toosend и получения данных в фоновом потоке и другой набор API, hello же без hello фонового потока. Много разработчики могут предпочесть hello не - LL API-интерфейсов, но hello более низкого уровня API-интерфейсы полезны, когда hello разработчику явный контроль над обмена данными по сети. Например, некоторые устройства собирают данные в течение продолжительного периода и передают события только через заданные интервалы времени (скажем, раз в час или раз в день). Здравствуйте, более низкого уровня API-интерфейсы позволяют hello возможность управления tooexplicitly при отправке и получении данных из центра IoT. Другие будут предпочтительности простоты hello, более низкого уровня API обеспечивают приветствия. Все, что происходит на основной поток hello, а не некоторых рабочих происходит в фоновом режиме hello.

Независимо от модели, можно выбрать, будет убедиться, что toobe согласованное в какие интерфейсы API используются. Если запускается путем вызова **IoTHubClient\_LL\_CreateFromConnectionString**, убедитесь, что вы используете только hello соответствующий API-интерфейс более низкого уровня для никаких дальнейших действий:

* IoTHubClient\_LL\_SendEventAsync
* IoTHubClient\_LL\_SetMessageCallback
* IoTHubClient\_LL\_Destroy
* IoTHubClient\_LL\_DoWork

Hello противоположной также имеет значение true. Если начать с **IoTHubClient\_CreateFromConnectionString**, а затем используйте hello не - LL API-интерфейсы для дополнительной обработки.

В hello Azure устройств IoT пакета SDK для языка C, в разделе hello **центром IOT\_клиента\_пример\_http** полный пример hello нижнего уровня приложения API-интерфейсы. Hello **центром IOT\_клиента\_пример\_amqp** приложения могут ссылаться полный пример hello не - LL интерфейсов API.

## <a name="property-handling"></a>Обработка свойств
До сих при отправке данных уже было сказано ранее, мы ссылка toohello тело сообщения hello. Рассмотрим для примера такой код:

```
EVENT_INSTANCE message;
sprintf_s(msgText, sizeof(msgText), "Hello World");
message.messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText));
IoTHubClient_LL_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message)
```

Этот пример отправляет сообщение tooIoT концентратора с текстом hello «Hello World». Однако центр IoT также позволяет свойства toobe вложенного tooeach сообщения. Свойства являются пары имя/значение, которые могут быть вложенные toohello сообщения. Например можно изменять tooattach предыдущего кода hello toohello свойства сообщения:

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

Мы начнем с вызова **IoTHubMessage\_свойства** и передав его дескриптор сообщений hello. Мы получаем обратно **КАРТЫ\_ОБРАБОТКИ** ссылку, которая позволяет нам toostart, Добавление свойств. последний Hello достигается посредством вызова **карты\_AddOrUpdate**, который принимает ссылку tooa КАРТЫ\_ДЕСКРИПТОР hello имя свойства и значение свойства hello. С помощью этого API мы можем добавить сколько угодно свойств.

Когда событие hello считывается из **концентраторов событий**, hello получатель сообщения может перечислять свойства hello и извлечения их значений. Например, в .NET это будет выполняться доступ к hello [коллекцию свойств для объекта EventData hello](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.eventdata.properties.aspx).

В предыдущем примере hello мы прикрепим отправку tooIoT концентратора событий tooan свойства. Свойства также могут быть вложенные toomessages, полученный от центра IoT. Если мы хотим tooretrieve свойства из сообщения, мы используем кода, подобного hello далее в нашем функции обратного вызова для сообщения:

```
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    . . .

    // Retrieve properties from hello message
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

Здравствуйте вызов слишком**IoTHubMessage\_свойства** возвращает hello **КАРТЫ\_ОБРАБОТКИ** ссылки. Затем передается этой ссылки слишком**карты\_GetInternals** tooobtain tooan ссылку, массив hello имя значение пары (а также число свойств hello). На этом этапе это простой вопрос перечисления hello свойства tooget toohello значениям, которые требуется.

В приложении нет toouse свойства. Тем не менее если вам требуется tooset их на события или получать их из сообщений hello **IoTHubClient** библиотека позволяет легко.

## <a name="message-handling"></a>Обработка сообщений
Как уже говорилось ранее, при поступлении сообщений от центра IoT hello **IoTHubClient** библиотеки отвечает, генерируя функция регистрируемого обратного вызова. У этой функции есть параметр возврата, который требует дополнительного пояснения. Ниже приведен фрагмент кода hello функции обратного вызова в hello **центром IOT\_клиента\_пример\_http** образец приложения:

```
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    . . .
    return IOTHUBMESSAGE_ACCEPTED;
}
```

Обратите внимание, что возвращаемый тип hello **IOTHUBMESSAGE\_DISPOSITION\_РЕЗУЛЬТАТ** и в данном случае мы возвращаем **IOTHUBMESSAGE\_ПРИНЯТО**. Существуют другие значения, мы можем вернуться из этой функции, как hello изменение **IoTHubClient** библиотеки реагирует обратного вызова toohello сообщения. Ниже приведены варианты hello.

* **IOTHUBMESSAGE\_ПРИНЯТО** — успешно обработал сообщение hello. Hello **IoTHubClient** библиотеки не будет вызывать функцию обратного вызова hello снова с hello одного сообщения.
* **IOTHUBMESSAGE\_Отклонено** — приветственное сообщение не было обработано и отсутствует в toodo нет желания hello будущих. Hello **IoTHubClient** библиотеки не должен вызывать функцию обратного вызова hello снова с hello одного сообщения.
* **IOTHUBMESSAGE\_ОТБРОШЕНО** — не был обработан приветственное сообщение, но hello **IoTHubClient** библиотеки следует вызвать функцию обратного вызова hello снова с hello одного сообщения.

Hello первых двух кодах возврата, hello **IoTHubClient** библиотеки отправляет сообщение tooIoT концентратора, указывающее, что сообщение hello следует удаляется из очереди устройства hello и снова не доставлено. суммарным эффектом Hello Здравствуйте, же (приветственное сообщение удаляется из очереди hello устройства), но по-прежнему записывается ли приветственное сообщение было принято или отклонено.  Запись это различие — полезные toosenders приветственное сообщение, кто может прослушивать отзывы и узнать, если устройство принял или отклонил определенного сообщения.

В последнем случае hello также отправляется сообщение tooIoT концентратора, но это означает, что это сообщение hello должны доставляться. Обычно будет прерывания сообщение, если некоторые ошибки, но хотите tootry tooprocess hello сообщение еще раз. Напротив отклоняет сообщение подходит при возникновении неустранимой ошибки (или вы просто решить, что вы не хотите tooprocess приветственное сообщение).

В любом случае помните о hello различных кодов возврата, чтобы вы, которые заставляют назвать hello поведение в hello **IoTHubClient** библиотеки.

## <a name="alternate-device-credentials"></a>Альтернативные учетные данные устройств
Как отмечалось ранее, Здравствуйте, первое, что toodo при работе с hello **IoTHubClient** библиотека — tooobtain **центром IOT\_КЛИЕНТА\_ОБРАБОТКИ** с помощью вызова, например hello следующие:

```
IOTHUB_CLIENT_HANDLE iotHubClientHandle;
iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, AMQP_Protocol);
```

Здравствуйте аргументы слишком**IoTHubClient\_CreateFromConnectionString** : строка подключения устройства hello и параметр, указывающий протокол hello, мы используем toocommunicate с центром IoT. Строка подключения устройства Hello имеет формат, который выглядит следующим образом:

```
HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY
```

В этой строке указаны четыре значения: имя центра IoT, суффикс центра IoT, идентификатор устройства и ключ общего доступа. При создании экземпляра концентратора IoT в hello портал Azure, получить hello полное доменное имя (FQDN) из центра IoT — это дает вам имя концентратора IoT hello (hello первой части hello полное доменное имя) и суффикс концентратора IoT hello (hello остальные hello полное доменное имя). При регистрации устройства с центром IoT получить идентификатор устройства hello и hello общий ключ доступа (как описано в hello [предыдущей статьи](iot-hub-device-sdk-c-intro.md)).

**IoTHubClient\_CreateFromConnectionString** предоставляет один из способов tooinitialize hello библиотеки. При желании можно создать новую **центром IOT\_КЛИЕНТА\_ОБРАБОТКИ** при помощи этих отдельных параметров, а не строку подключения устройства hello. Это достигается с hello, следующий код:

```
IOTHUB_CLIENT_CONFIG iotHubClientConfig;
iotHubClientConfig.iotHubName = "";
iotHubClientConfig.deviceId = "";
iotHubClientConfig.deviceKey = "";
iotHubClientConfig.iotHubSuffix = "";
iotHubClientConfig.protocol = HTTP_Protocol;
IOTHUB_CLIENT_HANDLE iotHubClientHandle = IoTHubClient_LL_Create(&iotHubClientConfig);
```

Это достигается hello идентичен **IoTHubClient\_CreateFromConnectionString**.

Он может казаться очевидным, что нужно toouse **IoTHubClient\_CreateFromConnectionString** вместо этого более подробным метод инициализации. Но не стоит забывать, что при регистрации устройства в центре IoT вы получаете только идентификатор и ключ устройства (а не строку подключения). Hello *обозреватель устройств* средства SDK, представленные в hello [предыдущей статьи](iot-hub-device-sdk-c-intro.md) использует библиотеки в hello **пакета SDK службы Azure IoT** toocreate hello устройства строка подключения Идентификатор устройства Hello, ключ устройства и центр IoT имени узла. Поэтому вызов **IoTHubClient\_LL\_создать** может быть предпочтительнее, так как избавляет вас hello шаг создания строки подключения. Используйте тот метод, который для вас удобнее.

## <a name="configuration-options"></a>Варианты настройки
Пока все описанные о hello способом hello **IoTHubClient** работает библиотека отражает поведения по умолчанию. Однако существует несколько параметров, задаваемых toochange, как работает библиотека hello. Это достигается за счет использования hello **IoTHubClient\_LL\_SetOption** API. Рассмотрим следующий пример.

```
unsigned int timeout = 30000;
IoTHubClient_LL_SetOption(iotHubClientHandle, "timeout", &timeout);
```

Существует несколько часто используемых параметров:

* **SetBatching** (логическое значение) — Если **true**, данные, отправляемые tooIoT концентратора, отправляется в виде пакетов. При значении **false** сообщения отправляются по отдельности. по умолчанию Hello — **false**. Обратите внимание, что hello **SetBatching** параметр применяется только протокол toohello HTTP и не toohello MQTT или AMQP протоколов.
* **Timeout** (целое число без знака). Это значение указывается в миллисекундах. Если отправка HTTP-запроса или ответа выполняется дольше этого времени, то время ожидания соединения hello.

Пакетная обработка параметр Hello важен. По умолчанию hello события ingresses библиотеки по отдельности (одно событие — все передаваемые слишком**IoTHubClient\_LL\_SendEventAsync**). Если пакетная обработка параметр hello **true**, библиотека hello собирает столько событий из буфера hello (вверх toohello максимальный размер сообщения, принимается центр IoT).  Hello событий выполняется отправка пакета tooIoT концентратора за один вызов HTTP (отдельные события hello объединены в массив JSON). Включение пакетной обработки обычно позволяет существенно увеличить производительность, так как уменьшается число сетевых круговых путей. При этом также существенно экономится пропускная способность, так как вы отправляете с пакетом событий только один набор заголовков HTTP, а не набор заголовков для каждого отдельного события. При отсутствии toodo определенной причине в противном случае, обычно стоит tooenable пакетной обработки.

## <a name="next-steps"></a>Дальнейшие действия
В этой статье описывается в поведении hello детализации hello **IoTHubClient** найти библиотеку в hello **устройств Azure IoT SDK для C**. С этой информацией, необходимо хорошо понимать возможности hello hello **IoTHubClient** библиотеки. Hello [следующей статье](iot-hub-device-sdk-c-serializer.md) содержит аналогичные сведения о hello **сериализатор** библиотеки.

toolearn Дополнительные сведения о разработке приложений для центра IoT. в разделе hello [пакеты SDK Azure IoT][lnk-sdks].

Изучение возможностей hello центра IoT toofurther см. в разделе:

* [Отправка сообщений с устройства в облако с помощью имитации устройства (Linux) с использованием Edge Интернета вещей Azure][lnk-iotedge]

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
