---
title: "сообщения aaaCloud на устройство с Azure IoT Hub (.NET) | Документы Microsoft"
description: "Способ toosend облака на устройство сообщений tooa устройств из центра Azure IoT с помощью hello Azure IoT, пакеты SDK для .NET. Изменение сообщений облака на устройство устройства tooreceive приложения и изменения сообщений облака на устройство hello toosend серверной части приложения."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: a31c05ed-6ec0-40f3-99ab-8fdd28b1a89a
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.openlocfilehash: f6a7618b164d95c8ddaf28943f244aeeb568217f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="send-messages-from-hello-cloud-tooyour-device-with-iot-hub-net"></a>Отправлять сообщения с устройства tooyour hello облака с IoT Hub (.NET)
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a>Введение
Центр Интернета вещей Azure — это полностью управляемая служба, которая обеспечивает надежный и защищенный двунаправленный обмен данными между миллионами устройств и серверной частью решения. Hello [приступить к работе с центром IoT] учебнике показано, как подготовить удостоверение устройства в нем toocreate центр IoT и кода приложения для устройств, отправляет сообщения из устройства в облако.

Это руководство является логическим продолжением статьи [приступить к работе с центром IoT]. В нем показано следующее:

* Из серверной части вашего решения отправьте сообщения облака на устройство tooa одно устройство через Центр IoT.
* Получение на устройстве сообщений, передаваемых из облака на устройство.
* Из вашего решения внутренний запрос подтверждения доставки (*отзывы*) для сообщений отправленных tooa устройств из центра IoT.

Дополнительные сведения о сообщениях облака на устройство можно найти в hello [руководстве для разработчиков центра IoT][IoT Hub developer guide - C2D].

В конце этого учебника hello выполните два консольных приложений .NET:

* **SimulatedDevice**, измененная версия приложения hello, созданного в [приступить к работе с центром IoT], который подключается tooyour центр IoT и получает сообщения облака на устройство.
* **SendCloudToDevice**, который отправляет приложения устройства toohello сообщение облака на устройство с помощью центра IoT, а затем получает подтверждение его доставки.

> [!NOTE]
> В Центре Интернета вещей реализована поддержка для пакетов SDK для многих платформ устройств и языков (включая C, Java и Javascript). Эти пакеты работают на основе [пакетов SDK для устройств Интернета вещей Azure]. Пошаговые инструкции по tooconnect кода учебник toothis устройства и обычно tooAzure центр IoT. в статье hello [руководстве для разработчиков центра IoT].
> 
> 

toocomplete этого учебника требуется hello следующие:

* Visual Studio 2015 или Visual Studio 2017
* Активная учетная запись Azure. Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.

## <a name="receive-messages-in-hello-device-app"></a>Получать сообщения в приложение hello устройства
В этом разделе необходимо изменить приложение hello устройства, созданный в [приступить к работе с центром IoT] tooreceive сообщений облака на устройство из центра IoT hello.

1. В Visual Studio в hello **SimulatedDevice** , добавьте следующий метод toohello hello **программы** класса.
   
        private static async void ReceiveC2dAsync()
        {
            Console.WriteLine("\nReceiving cloud toodevice messages from service");
            while (true)
            {
                Message receivedMessage = await deviceClient.ReceiveAsync();
                if (receivedMessage == null) continue;
   
                Console.ForegroundColor = ConsoleColor.Yellow;
                Console.WriteLine("Received message: {0}", Encoding.ASCII.GetString(receivedMessage.GetBytes()));
                Console.ResetColor();
   
                await deviceClient.CompleteAsync(receivedMessage);
            }
        }
   
    Hello `ReceiveAsync` метод асинхронно возвращает сообщение hello получено во время hello, получаемой устройством hello. Он возвращает *null* после задаваемого ожидания (в этом случае используется значение по умолчанию hello в минуту). При получении приложение hello *null*, должен быть продолжен toowait для новых сообщений. Это требование является причиной hello hello `if (receivedMessage == null) continue` строки.
   
    Здравствуйте вызов слишком`CompleteAsync()` уведомляет центра IoT успешно обработал сообщение hello. приветственное сообщение можно безопасно удалить из очереди устройства hello. Если что-то произошло, приложение устройства предотвращено hello из завершение обработки приветственное сообщение hello, центр IoT доставляет его еще раз. Очень важно затем этой логики в приложение hello устройства обработки сообщений был *идемпотентными*, после чего получение hello повторяется несколько раз выводятся hello того же результата. Приложения можно также временно отказ от сообщения, которое приводит к центра IoT, сохраняя приветственное сообщение hello очереди для последующей обработки. Или hello приложение может отклонить сообщение, которое окончательно удаляет приветственное сообщение из очереди hello. Дополнительные сведения о жизненного цикла облака на устройство сообщение hello. в разделе hello [руководстве для разработчиков центра IoT][IoT Hub developer guide - C2D].
   
   > [!NOTE]
   > При использовании HTTP вместо MQTT или AMQP, как транспорт, hello `ReceiveAsync` метод возвращается немедленно. шаблон Hello поддерживается для облака на устройство сообщений с HTTP является периодически подключенные устройства, которые проверьте редко сообщений (менее чем каждые 25 минут). Выдача дополнительные HTTP Получает результаты в центр IoT регулирования запросов hello. Дополнительные сведения об отличиях hello поддержки MQTT, AMQP и HTTP и центр IoT регулирования см. в разделе hello [руководстве для разработчиков центра IoT][IoT Hub developer guide - C2D].
   > 
   > 
2. Добавьте следующий метод в hello hello **Main** метод прямо перед hello `Console.ReadLine()` строки:
   
        ReceiveC2dAsync();

> [!NOTE]
> Для упрощения в этом учебнике не реализуются какие-либо политики повтора. В рабочем коде следует реализовать политики повтора (например, экспоненциального отката), описанным в статье MSDN hello [обработка временных сбоев].
> 
> 

## <a name="send-a-cloud-to-device-message"></a>Отправка сообщения из облака на устройство
В этом разделе записи .NET консольное приложение, которое отправляет приложения для устройств toohello сообщений облака на устройство.

1. В текущем решении Visual Studio hello, создайте проект приложения рабочего стола Visual C# с помощью hello **консольное приложение** шаблона проекта. Имя проекта hello **SendCloudToDevice**.
   
    ![Новый проект в Visual Studio][20]
2. В обозревателе решений щелкните правой кнопкой мыши решение hello затем **управление пакетами NuGet для решения...** . 
   
    Это действие открывает hello **управление пакетами NuGet** окна.
3. Поиск **Microsoft.Azure.Devices**, нажмите кнопку **установить**и примите условия использования hello. 
   
    Это загружает, устанавливает и добавляет toohello ссылки [пакет SDK NuGet службы Azure IoT].

4. Добавьте следующее hello `using` инструкции вверху hello hello **Program.cs** файла:
   
        using Microsoft.Azure.Devices;
5. Добавьте следующие поля toohello hello **программы** класса. Замените значение заполнителя hello со строкой подключения концентратора IoT hello из [приступить к работе с центром IoT]:
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. Добавьте следующий метод toohello hello **программы** класса:
   
        private async static Task SendCloudToDeviceMessageAsync()
        {
            var commandMessage = new Message(Encoding.ASCII.GetBytes("Cloud toodevice message."));
            await serviceClient.SendAsync("myFirstDevice", commandMessage);
        }
   
    Этот метод отправляет новое устройство toohello облака на устройство сообщение с Идентификатором hello `myFirstDevice`. Измените этот параметр только в том случае, если он изменен из hello календарем, используемым в [приступить к работе с центром IoT].
7. Наконец, добавьте следующие строки toohello hello **Main** метод:
   
        Console.WriteLine("Send Cloud-to-Device message\n");
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
   
        Console.WriteLine("Press any key toosend a C2D message.");
        Console.ReadLine();
        SendCloudToDeviceMessageAsync().Wait();
        Console.ReadLine();
8. В Visual Studio щелкните правой кнопкой мыши свое решение и выберите пункт **Назначить запускаемые проекты**. Выберите **несколько запускаемых проектов**, а затем выберите hello **запустить** действие для **ReadDeviceToCloudMessages**, **SimulatedDevice**, и **SendCloudToDevice**.
9. Нажмите клавишу **F5**. Должны запуститься все три приложения. Выберите hello **SendCloudToDevice** windows и клавишу **ввод**. Вы увидите приветственных сообщений, полученных приложение hello устройства.
   
   ![Приложение получает сообщение][21]

## <a name="receive-delivery-feedback"></a>Получение подтверждений доставки
Это возможно toorequest доставки (или истечения срока действия) подтверждений от центра IoT для каждого сообщения облака на устройство. Этот параметр включает hello решения серверной части tooeasily сообщают логику повтора или компенсации. Дополнительные сведения об обратной связи облака на устройство см. в разделе hello [руководстве для разработчиков центра IoT][IoT Hub developer guide - C2D].

В этом разделе можно изменить hello **SendCloudToDevice** toorequest отзыва о приложении и его получения с центра IoT.

1. В Visual Studio в hello **SendCloudToDevice** , добавьте следующий метод toohello hello **программы** класса.
   
        private async static void ReceiveFeedbackAsync()
        {
            var feedbackReceiver = serviceClient.GetFeedbackReceiver();
   
            Console.WriteLine("\nReceiving c2d feedback from service");
            while (true)
            {
                var feedbackBatch = await feedbackReceiver.ReceiveAsync();
                if (feedbackBatch == null) continue;
   
                Console.ForegroundColor = ConsoleColor.Yellow;
                Console.WriteLine("Received feedback: {0}", string.Join(", ", feedbackBatch.Records.Select(f => f.StatusCode)));
                Console.ResetColor();
   
                await feedbackReceiver.CompleteAsync(feedbackBatch);
            }
        }
   
    Обратите внимание, этот шаблон receive hello же сообщения облака на устройство tooreceive используется один из приложения hello устройства.
2. Добавьте следующий метод в hello hello **Main** метод сразу же после hello `serviceClient = ServiceClient.CreateFromConnectionString(connectionString)` строки:
   
        ReceiveFeedbackAsync();
3. отзыв toorequest hello доставки сообщения облака на устройство, у вас есть toospecify свойство в hello **SendCloudToDeviceMessageAsync** метод. Добавьте следующие строки, сразу после hello hello `var commandMessage = new Message(...);` строки:
   
        commandMessage.Ack = DeliveryAcknowledgement.Full;
4. Запускайте приложения hello, нажав клавишу **F5**. Должны запуститься все три приложения. Выберите hello **SendCloudToDevice** windows и клавишу **ввод**. Вы увидите hello сообщений, принимаемых приложением устройства hello и через несколько секунд, hello сообщение отзывов, полученных на **SendCloudToDevice** приложения.
   
   ![Приложение получает сообщение][22]

> [!NOTE]
> Для упрощения в этом учебнике не реализуются какие-либо политики повтора. В рабочем коде следует реализовать политики повтора (например, экспоненциального отката), описанным в статье MSDN hello [обработка временных сбоев].
> 
> 

## <a name="next-steps"></a>Дальнейшие действия
В этом учебнике вы узнали, как toosend и получать сообщения облака на устройство. 

см. Примеры toosee полное и всестороннее решений, использующих центр IoT [Azure IoT Suite].

toolearn Дополнительные сведения о разработке решений с центром IoT разделе hello [руководстве для разработчиков центра IoT].

<!-- Images -->
[20]: ./media/iot-hub-csharp-csharp-c2d/create-identity-csharp1.png
[21]: ./media/iot-hub-csharp-csharp-c2d/sendc2d1.png
[22]: ./media/iot-hub-csharp-csharp-c2d/sendc2d2.png

<!-- Links -->

[пакет SDK NuGet службы Azure IoT]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[обработка временных сбоев]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md

[руководстве для разработчиков центра IoT]: iot-hub-devguide.md
[приступить к работе с центром IoT]: iot-hub-csharp-csharp-getstarted.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure IoT Suite]: https://docs.microsoft.com/en-us/azure/iot-suite/
[пакетов SDK для устройств Интернета вещей Azure]: iot-hub-devguide-sdks.md