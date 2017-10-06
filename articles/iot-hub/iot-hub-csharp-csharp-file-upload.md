---
title: "файлы aaaUpload из устройств tooAzure центр IoT с .NET | Документы Microsoft"
description: "Как tooupload файлы из облака toohello устройства, с помощью устройств Azure IoT SDK для .NET. Отправленные файлы хранятся в контейнере больших двоичных объектов службы хранилища Azure."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 4759d229-f856-4526-abda-414f8b00a56d
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/04/2017
ms.author: elioda
ms.openlocfilehash: 07d555f6ba8b067bbd3233bc8eebaa220ad2388b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-from-your-device-toohello-cloud-with-iot-hub-using-net"></a>Отправка файлов в облаке toohello устройства с центром IoT, с помощью .NET

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

Этот учебник построен на кода hello в hello [отправки сообщений облака на устройство с центром IoT](iot-hub-csharp-csharp-c2d.md) tooshow учебника вы как toouse hello центра IoT возможности передачи файлов. В нем показано следующее:

- как безопасно предоставить устройству универсальный код ресурса (URI) большого двоичного объекта Azure для передачи файла;
- Используйте центр IoT файл отправки уведомления tootrigger обработке hello файла в серверной части вашего приложения hello.

Hello [приступить к работе с центром IoT](iot-hub-csharp-csharp-getstarted.md) и [отправки сообщений облака на устройство с центром IoT](iot-hub-csharp-csharp-c2d.md) руководствах hello основные устройства в облако и облака на устройство обмена сообщениями функции центра IoT. Hello [сообщений процесс устройства в облако](iot-hub-csharp-csharp-process-d2c.md) учебнике рассматривается способ tooreliably записи устройства в облако сообщений в хранилище больших двоичных объектов. Однако в некоторых сценариях невозможно сопоставить легко hello данных устройствами отправки на относительно небольшой устройства в облако сообщений hello, которое принимает центр IoT. Например:

* Большие файлы, содержащие изображения.
* Видеоролики
* Данные вибрации с высокой частотой выборки.
* Некоторые виды предварительно обработанных данных.

Эти файлы обычно являются пакетной обработки в облаке hello, с помощью средств, таких как [фабрики данных Azure](../data-factory/index.md) или hello [Hadoop](../hdinsight/index.md) стека. Если вам требуется tooupload файлы с устройства, по-прежнему можно использовать hello безопасности и надежности центр IoT.

В конце этого учебника в hello запуска двух консольных приложений .NET:

* **SimulatedDevice**, измененная версия приложения hello, созданного в hello [отправки сообщений облака на устройство с центром IoT](iot-hub-csharp-csharp-c2d.md) учебника. Это приложение передает файл toostorage, с помощью URI SAS, предоставляемые концентратор IoT.
* **ReadFileUploadNotification**— приложение, которое получает уведомления о передаче файлов от Центра Интернета вещей.

> [!NOTE]
> Существуют пакеты SDK для устройств Интернета вещей Azure, обеспечивающие поддержку многих платформ устройств и языков (включая C, Java и JavaScript) в Центре Интернета вещей. См. toohello [Центр разработчиков Azure IoT] пошаговые инструкции о том, как tooconnect tooAzure вашего устройства центра IoT.

toocomplete этого учебника требуется hello следующие:

* Visual Studio 2015 или Visual Studio 2017
* Активная учетная запись Azure. Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a>Передача файла из приложения устройства

В этом разделе, измените приложение hello устройства, созданный в [отправки сообщений облака на устройство с центром IoT](iot-hub-csharp-csharp-c2d.md) tooreceive сообщений облака на устройство из центра IoT hello.

1. В Visual Studio щелкните правой кнопкой мыши hello **SimulatedDevice** проекта, нажмите кнопку **добавить**, а затем нажмите кнопку **существующий элемент**. Перейдите tooan файл изображения и включить его в проект. В этом учебнике предполагается hello изображение называется `image.jpg`.

1. Щелкните правой кнопкой мыши на изображение hello и нажмите кнопку **свойства**. Убедитесь, что **скопируйте каталог tooOutput** задано слишком**всегда Копировать**.

    ![][1]

1. В hello **Program.cs** файл, добавьте следующие инструкции в начале hello файла hello hello:

    ```csharp
    using System.IO;
    ```

1. Добавьте следующий метод toohello hello **программы** класса:

    ```csharp
    private static async void SendToBlobAsync()
    {
        string fileName = "image.jpg";
        Console.WriteLine("Uploading file: {0}", fileName);
        var watch = System.Diagnostics.Stopwatch.StartNew();

        using (var sourceData = new FileStream(@"image.jpg", FileMode.Open))
        {
            await deviceClient.UploadToBlobAsync(fileName, sourceData);
        }

        watch.Stop();
        Console.WriteLine("Time tooupload file: {0}ms\n", watch.ElapsedMilliseconds);
    }
    ```

    Hello `UploadToBlobAsync` метод принимает в имени файла hello и источник потока toobe файл hello передачи и обрабатывает toostorage передачи hello. Консольное приложение Hello отображает время hello tooupload hello файла.

1. Добавьте следующий метод в hello hello **Main** метод прямо перед hello `Console.ReadLine()` строки:

    ```csharp
    SendToBlobAsync();
    ```

> [!NOTE]
> Для упрощения в этом учебнике не реализуются какие-либо политики повтора. В рабочем коде следует реализовать политики повтора (например, экспоненциального отката), описанным в статье MSDN hello [обработка временных сбоев].

## <a name="receive-a-file-upload-notification"></a>Получение уведомления о передачи файла

В этом разделе вам предстоит создать консольное приложение для .NET, которое получает уведомления об отправке файлов из Центра Интернета вещей.

1. В текущем решении Visual Studio hello, Создание проекта Visual C# Windows с помощью hello **консольное приложение** шаблона проекта. Имя проекта hello **ReadFileUploadNotification**.

    ![Новый проект в Visual Studio][2]

1. В обозревателе решений щелкните правой кнопкой мыши hello **ReadFileUploadNotification** проекта, а затем нажмите кнопку **управление пакетами NuGet...** .

1. В hello **диспетчера пакетов NuGet** найдите **Microsoft.Azure.Devices**, нажмите кнопку **установить**и примите условия использования hello.

    Это действие загружает, устанавливает и добавляет toohello ссылки [пакет SDK NuGet службы Azure IoT] в hello **ReadFileUploadNotification** проекта.

1. В hello **Program.cs** файл, добавьте следующие инструкции в начале hello файла hello hello:

    ```csharp
    using Microsoft.Azure.Devices;
    ```

1. Добавьте следующие поля toohello hello **программы** класса. Замените значение заполнителя hello со строкой подключения концентратора IoT hello из [Приступая к работе с центра IoT]:

    ```csharp
    static ServiceClient serviceClient;
    static string connectionString = "{iot hub connection string}";
    ```

1. Добавьте следующий метод toohello hello **программы** класса:

    ```csharp
    private async static void ReceiveFileUploadNotificationAsync()
    {
        var notificationReceiver = serviceClient.GetFileNotificationReceiver();

        Console.WriteLine("\nReceiving file upload notification from service");
        while (true)
        {
            var fileUploadNotification = await notificationReceiver.ReceiveAsync();
            if (fileUploadNotification == null) continue;

            Console.ForegroundColor = ConsoleColor.Yellow;
            Console.WriteLine("Received file upload noticiation: {0}", string.Join(", ", fileUploadNotification.BlobName));
            Console.ResetColor();

            await notificationReceiver.CompleteAsync(fileUploadNotification);
        }
    }
    ```

    Обратите внимание, этот шаблон receive hello же сообщения облака на устройство tooreceive используется один из приложения hello устройства.

1. Наконец, добавьте следующие строки toohello hello **Main** метод:

    ```csharp
    Console.WriteLine("Receive file upload notifications\n");
    serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
    ReceiveFileUploadNotificationAsync();
    Console.WriteLine("Press Enter tooexit\n");
    Console.ReadLine();
    ```

## <a name="run-hello-applications"></a>Запускать приложения hello

Теперь все готово toorun приложения hello.

1. В Visual Studio щелкните правой кнопкой мыши свое решение и выберите пункт **Назначить запускаемые проекты**. Выберите **несколько запускаемых проектов**, а затем выберите hello **запустить** действие для **ReadFileUploadNotification** и **SimulatedDevice**.

1. Нажмите клавишу **F5**. Должны запуститься оба приложения. Вы увидите передачи hello завершил работу за один консольное приложение и hello отправки уведомлений сообщение, полученное по hello других консольного приложения. Можно использовать hello [портал Azure] или обозревателя серверов Visual Studio toocheck наличие hello hello отправки файла в вашей учетной записи хранилища Azure.

    ![][50]

## <a name="next-steps"></a>Дальнейшие действия

В этом учебнике вы узнали, как файл hello toouse отправить возможности передачи файлов toosimplify с устройств центра IoT. Можно продолжить tooexplore IoT hub функции и сценарии hello в следующих статьях:

* [Создание Центра Интернета вещей с помощью PowerShell][lnk-create-hub]
* [Введение tooC SDK][lnk-c-sdk]
* [IoT Hub SDKs][lnk-sdks] (Пакеты SDK для Центра Интернета вещей)

Изучение возможностей hello центра IoT toofurther см. в разделе:

* [Simulating a device with IoT Edge][lnk-iotedge] (Моделирование устройства с помощью Edge Интернета вещей)

<!-- Images. -->

[50]: ./media/iot-hub-csharp-csharp-file-upload/run-apps1.png
[1]: ./media/iot-hub-csharp-csharp-file-upload/image-properties.png
[2]: ./media/iot-hub-csharp-csharp-file-upload/file-upload-project-csharp1.png

<!-- Links -->

[портал Azure]: https://portal.azure.com/

[Центр разработчиков Azure IoT]: http://www.azure.com/develop/iot

[обработка временных сбоев]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[пакет SDK NuGet службы Azure IoT]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-windows-iot-edge-simulated-device.md
