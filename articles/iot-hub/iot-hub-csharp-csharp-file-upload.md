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
# <a name="upload-files-from-your-device-toohello-cloud-with-iot-hub-using-net"></a><span data-ttu-id="692aa-104">Отправка файлов в облаке toohello устройства с центром IoT, с помощью .NET</span><span class="sxs-lookup"><span data-stu-id="692aa-104">Upload files from your device toohello cloud with IoT Hub using .NET</span></span>

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

<span data-ttu-id="692aa-105">Этот учебник построен на кода hello в hello [отправки сообщений облака на устройство с центром IoT](iot-hub-csharp-csharp-c2d.md) tooshow учебника вы как toouse hello центра IoT возможности передачи файлов.</span><span class="sxs-lookup"><span data-stu-id="692aa-105">This tutorial builds on hello code in hello [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorial tooshow you how toouse hello file upload capabilities of IoT Hub.</span></span> <span data-ttu-id="692aa-106">В нем показано следующее:</span><span class="sxs-lookup"><span data-stu-id="692aa-106">It shows you how to:</span></span>

- <span data-ttu-id="692aa-107">как безопасно предоставить устройству универсальный код ресурса (URI) большого двоичного объекта Azure для передачи файла;</span><span class="sxs-lookup"><span data-stu-id="692aa-107">Securely provide a device with an Azure blob URI for uploading a file.</span></span>
- <span data-ttu-id="692aa-108">Используйте центр IoT файл отправки уведомления tootrigger обработке hello файла в серверной части вашего приложения hello.</span><span class="sxs-lookup"><span data-stu-id="692aa-108">Use hello IoT Hub file upload notifications tootrigger processing hello file in your app back end.</span></span>

<span data-ttu-id="692aa-109">Hello [приступить к работе с центром IoT](iot-hub-csharp-csharp-getstarted.md) и [отправки сообщений облака на устройство с центром IoT](iot-hub-csharp-csharp-c2d.md) руководствах hello основные устройства в облако и облака на устройство обмена сообщениями функции центра IoT.</span><span class="sxs-lookup"><span data-stu-id="692aa-109">hello [Get started with IoT Hub](iot-hub-csharp-csharp-getstarted.md) and [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorials show hello basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span> <span data-ttu-id="692aa-110">Hello [сообщений процесс устройства в облако](iot-hub-csharp-csharp-process-d2c.md) учебнике рассматривается способ tooreliably записи устройства в облако сообщений в хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="692aa-110">hello [Process Device-to-Cloud messages](iot-hub-csharp-csharp-process-d2c.md) tutorial describes a way tooreliably store device-to-cloud messages in Azure blob storage.</span></span> <span data-ttu-id="692aa-111">Однако в некоторых сценариях невозможно сопоставить легко hello данных устройствами отправки на относительно небольшой устройства в облако сообщений hello, которое принимает центр IoT.</span><span class="sxs-lookup"><span data-stu-id="692aa-111">However, in some scenarios you cannot easily map hello data your devices send into hello relatively small device-to-cloud messages that IoT Hub accepts.</span></span> <span data-ttu-id="692aa-112">Например:</span><span class="sxs-lookup"><span data-stu-id="692aa-112">For example:</span></span>

* <span data-ttu-id="692aa-113">Большие файлы, содержащие изображения.</span><span class="sxs-lookup"><span data-stu-id="692aa-113">Large files that contain images</span></span>
* <span data-ttu-id="692aa-114">Видеоролики</span><span class="sxs-lookup"><span data-stu-id="692aa-114">Videos</span></span>
* <span data-ttu-id="692aa-115">Данные вибрации с высокой частотой выборки.</span><span class="sxs-lookup"><span data-stu-id="692aa-115">Vibration data sampled at high frequency</span></span>
* <span data-ttu-id="692aa-116">Некоторые виды предварительно обработанных данных.</span><span class="sxs-lookup"><span data-stu-id="692aa-116">Some form of preprocessed data</span></span>

<span data-ttu-id="692aa-117">Эти файлы обычно являются пакетной обработки в облаке hello, с помощью средств, таких как [фабрики данных Azure](../data-factory/index.md) или hello [Hadoop](../hdinsight/index.md) стека.</span><span class="sxs-lookup"><span data-stu-id="692aa-117">These files are typically batch processed in hello cloud using tools such as [Azure Data Factory](../data-factory/index.md) or hello [Hadoop](../hdinsight/index.md) stack.</span></span> <span data-ttu-id="692aa-118">Если вам требуется tooupload файлы с устройства, по-прежнему можно использовать hello безопасности и надежности центр IoT.</span><span class="sxs-lookup"><span data-stu-id="692aa-118">When you need tooupload files from a device, you can still use hello security and reliability of IoT Hub.</span></span>

<span data-ttu-id="692aa-119">В конце этого учебника в hello запуска двух консольных приложений .NET:</span><span class="sxs-lookup"><span data-stu-id="692aa-119">At hello end of this tutorial you run two .NET console apps:</span></span>

* <span data-ttu-id="692aa-120">**SimulatedDevice**, измененная версия приложения hello, созданного в hello [отправки сообщений облака на устройство с центром IoT](iot-hub-csharp-csharp-c2d.md) учебника.</span><span class="sxs-lookup"><span data-stu-id="692aa-120">**SimulatedDevice**, a modified version of hello app created in hello [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorial.</span></span> <span data-ttu-id="692aa-121">Это приложение передает файл toostorage, с помощью URI SAS, предоставляемые концентратор IoT.</span><span class="sxs-lookup"><span data-stu-id="692aa-121">This app uploads a file toostorage using a SAS URI provided by your IoT hub.</span></span>
* <span data-ttu-id="692aa-122">**ReadFileUploadNotification**— приложение, которое получает уведомления о передаче файлов от Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="692aa-122">**ReadFileUploadNotification**, which receives file upload notifications from your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="692aa-123">Существуют пакеты SDK для устройств Интернета вещей Azure, обеспечивающие поддержку многих платформ устройств и языков (включая C, Java и JavaScript) в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="692aa-123">IoT Hub supports many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="692aa-124">См. toohello [Центр разработчиков Azure IoT] пошаговые инструкции о том, как tooconnect tooAzure вашего устройства центра IoT.</span><span class="sxs-lookup"><span data-stu-id="692aa-124">Refer toohello [Azure IoT Developer Center] for step-by-step instructions on how tooconnect your device tooAzure IoT Hub.</span></span>

<span data-ttu-id="692aa-125">toocomplete этого учебника требуется hello следующие:</span><span class="sxs-lookup"><span data-stu-id="692aa-125">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="692aa-126">Visual Studio 2015 или Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="692aa-126">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="692aa-127">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="692aa-127">An active Azure account.</span></span> <span data-ttu-id="692aa-128">Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="692aa-128">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a><span data-ttu-id="692aa-129">Передача файла из приложения устройства</span><span class="sxs-lookup"><span data-stu-id="692aa-129">Upload a file from a device app</span></span>

<span data-ttu-id="692aa-130">В этом разделе, измените приложение hello устройства, созданный в [отправки сообщений облака на устройство с центром IoT](iot-hub-csharp-csharp-c2d.md) tooreceive сообщений облака на устройство из центра IoT hello.</span><span class="sxs-lookup"><span data-stu-id="692aa-130">In this section, you modify hello device app you created in [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tooreceive cloud-to-device messages from hello IoT hub.</span></span>

1. <span data-ttu-id="692aa-131">В Visual Studio щелкните правой кнопкой мыши hello **SimulatedDevice** проекта, нажмите кнопку **добавить**, а затем нажмите кнопку **существующий элемент**.</span><span class="sxs-lookup"><span data-stu-id="692aa-131">In Visual Studio, right-click hello **SimulatedDevice** project, click **Add**, and then click **Existing Item**.</span></span> <span data-ttu-id="692aa-132">Перейдите tooan файл изображения и включить его в проект.</span><span class="sxs-lookup"><span data-stu-id="692aa-132">Navigate tooan image file and include it in your project.</span></span> <span data-ttu-id="692aa-133">В этом учебнике предполагается hello изображение называется `image.jpg`.</span><span class="sxs-lookup"><span data-stu-id="692aa-133">This tutorial assumes hello image is named `image.jpg`.</span></span>

1. <span data-ttu-id="692aa-134">Щелкните правой кнопкой мыши на изображение hello и нажмите кнопку **свойства**.</span><span class="sxs-lookup"><span data-stu-id="692aa-134">Right-click on hello image, and then click **Properties**.</span></span> <span data-ttu-id="692aa-135">Убедитесь, что **скопируйте каталог tooOutput** задано слишком**всегда Копировать**.</span><span class="sxs-lookup"><span data-stu-id="692aa-135">Make sure that **Copy tooOutput Directory** is set too**Copy always**.</span></span>

    ![][1]

1. <span data-ttu-id="692aa-136">В hello **Program.cs** файл, добавьте следующие инструкции в начале hello файла hello hello:</span><span class="sxs-lookup"><span data-stu-id="692aa-136">In hello **Program.cs** file, add hello following statements at hello top of hello file:</span></span>

    ```csharp
    using System.IO;
    ```

1. <span data-ttu-id="692aa-137">Добавьте следующий метод toohello hello **программы** класса:</span><span class="sxs-lookup"><span data-stu-id="692aa-137">Add hello following method toohello **Program** class:</span></span>

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

    <span data-ttu-id="692aa-138">Hello `UploadToBlobAsync` метод принимает в имени файла hello и источник потока toobe файл hello передачи и обрабатывает toostorage передачи hello.</span><span class="sxs-lookup"><span data-stu-id="692aa-138">hello `UploadToBlobAsync` method takes in hello file name and stream source of hello file toobe uploaded and handles hello upload toostorage.</span></span> <span data-ttu-id="692aa-139">Консольное приложение Hello отображает время hello tooupload hello файла.</span><span class="sxs-lookup"><span data-stu-id="692aa-139">hello console app displays hello time it takes tooupload hello file.</span></span>

1. <span data-ttu-id="692aa-140">Добавьте следующий метод в hello hello **Main** метод прямо перед hello `Console.ReadLine()` строки:</span><span class="sxs-lookup"><span data-stu-id="692aa-140">Add hello following method in hello **Main** method, right before hello `Console.ReadLine()` line:</span></span>

    ```csharp
    SendToBlobAsync();
    ```

> [!NOTE]
> <span data-ttu-id="692aa-141">Для упрощения в этом учебнике не реализуются какие-либо политики повтора.</span><span class="sxs-lookup"><span data-stu-id="692aa-141">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="692aa-142">В рабочем коде следует реализовать политики повтора (например, экспоненциального отката), описанным в статье MSDN hello [обработка временных сбоев].</span><span class="sxs-lookup"><span data-stu-id="692aa-142">In production code, you should implement retry policies (such as exponential backoff), as suggested in hello MSDN article [Transient Fault Handling].</span></span>

## <a name="receive-a-file-upload-notification"></a><span data-ttu-id="692aa-143">Получение уведомления о передачи файла</span><span class="sxs-lookup"><span data-stu-id="692aa-143">Receive a file upload notification</span></span>

<span data-ttu-id="692aa-144">В этом разделе вам предстоит создать консольное приложение для .NET, которое получает уведомления об отправке файлов из Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="692aa-144">In this section, you write a .NET console app that receives file upload notification messages from IoT Hub.</span></span>

1. <span data-ttu-id="692aa-145">В текущем решении Visual Studio hello, Создание проекта Visual C# Windows с помощью hello **консольное приложение** шаблона проекта.</span><span class="sxs-lookup"><span data-stu-id="692aa-145">In hello current Visual Studio solution, create a Visual C# Windows project by using hello **Console Application** project template.</span></span> <span data-ttu-id="692aa-146">Имя проекта hello **ReadFileUploadNotification**.</span><span class="sxs-lookup"><span data-stu-id="692aa-146">Name hello project **ReadFileUploadNotification**.</span></span>

    ![Новый проект в Visual Studio][2]

1. <span data-ttu-id="692aa-148">В обозревателе решений щелкните правой кнопкой мыши hello **ReadFileUploadNotification** проекта, а затем нажмите кнопку **управление пакетами NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="692aa-148">In Solution Explorer, right-click hello **ReadFileUploadNotification** project, and then click **Manage NuGet Packages...**.</span></span>

1. <span data-ttu-id="692aa-149">В hello **диспетчера пакетов NuGet** найдите **Microsoft.Azure.Devices**, нажмите кнопку **установить**и примите условия использования hello.</span><span class="sxs-lookup"><span data-stu-id="692aa-149">In hello **NuGet Package Manager** window, search for **Microsoft.Azure.Devices**, click **Install**, and accept hello terms of use.</span></span>

    <span data-ttu-id="692aa-150">Это действие загружает, устанавливает и добавляет toohello ссылки [пакет SDK NuGet службы Azure IoT] в hello **ReadFileUploadNotification** проекта.</span><span class="sxs-lookup"><span data-stu-id="692aa-150">This action downloads, installs, and adds a reference toohello [Azure IoT service SDK NuGet package] in hello **ReadFileUploadNotification** project.</span></span>

1. <span data-ttu-id="692aa-151">В hello **Program.cs** файл, добавьте следующие инструкции в начале hello файла hello hello:</span><span class="sxs-lookup"><span data-stu-id="692aa-151">In hello **Program.cs** file, add hello following statements at hello top of hello file:</span></span>

    ```csharp
    using Microsoft.Azure.Devices;
    ```

1. <span data-ttu-id="692aa-152">Добавьте следующие поля toohello hello **программы** класса.</span><span class="sxs-lookup"><span data-stu-id="692aa-152">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="692aa-153">Замените значение заполнителя hello со строкой подключения концентратора IoT hello из [Приступая к работе с центра IoT]:</span><span class="sxs-lookup"><span data-stu-id="692aa-153">Substitute hello placeholder value with hello IoT hub connection string from [Get started with IoT Hub]:</span></span>

    ```csharp
    static ServiceClient serviceClient;
    static string connectionString = "{iot hub connection string}";
    ```

1. <span data-ttu-id="692aa-154">Добавьте следующий метод toohello hello **программы** класса:</span><span class="sxs-lookup"><span data-stu-id="692aa-154">Add hello following method toohello **Program** class:</span></span>

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

    <span data-ttu-id="692aa-155">Обратите внимание, этот шаблон receive hello же сообщения облака на устройство tooreceive используется один из приложения hello устройства.</span><span class="sxs-lookup"><span data-stu-id="692aa-155">Note this receive pattern is hello same one used tooreceive cloud-to-device messages from hello device app.</span></span>

1. <span data-ttu-id="692aa-156">Наконец, добавьте следующие строки toohello hello **Main** метод:</span><span class="sxs-lookup"><span data-stu-id="692aa-156">Finally, add hello following lines toohello **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Receive file upload notifications\n");
    serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
    ReceiveFileUploadNotificationAsync();
    Console.WriteLine("Press Enter tooexit\n");
    Console.ReadLine();
    ```

## <a name="run-hello-applications"></a><span data-ttu-id="692aa-157">Запускать приложения hello</span><span class="sxs-lookup"><span data-stu-id="692aa-157">Run hello applications</span></span>

<span data-ttu-id="692aa-158">Теперь все готово toorun приложения hello.</span><span class="sxs-lookup"><span data-stu-id="692aa-158">Now you are ready toorun hello applications.</span></span>

1. <span data-ttu-id="692aa-159">В Visual Studio щелкните правой кнопкой мыши свое решение и выберите пункт **Назначить запускаемые проекты**.</span><span class="sxs-lookup"><span data-stu-id="692aa-159">In Visual Studio, right-click your solution, and select **Set StartUp projects**.</span></span> <span data-ttu-id="692aa-160">Выберите **несколько запускаемых проектов**, а затем выберите hello **запустить** действие для **ReadFileUploadNotification** и **SimulatedDevice**.</span><span class="sxs-lookup"><span data-stu-id="692aa-160">Select **Multiple startup projects**, then select hello **Start** action for **ReadFileUploadNotification** and **SimulatedDevice**.</span></span>

1. <span data-ttu-id="692aa-161">Нажмите клавишу **F5**.</span><span class="sxs-lookup"><span data-stu-id="692aa-161">Press **F5**.</span></span> <span data-ttu-id="692aa-162">Должны запуститься оба приложения.</span><span class="sxs-lookup"><span data-stu-id="692aa-162">Both applications should start.</span></span> <span data-ttu-id="692aa-163">Вы увидите передачи hello завершил работу за один консольное приложение и hello отправки уведомлений сообщение, полученное по hello других консольного приложения.</span><span class="sxs-lookup"><span data-stu-id="692aa-163">You should see hello upload completed in one console app and hello upload notification message received by hello other console app.</span></span> <span data-ttu-id="692aa-164">Можно использовать hello [портал Azure] или обозревателя серверов Visual Studio toocheck наличие hello hello отправки файла в вашей учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="692aa-164">You can use hello [Azure portal] or Visual Studio Server Explorer toocheck for hello presence of hello uploaded file in your Azure Storage account.</span></span>

    ![][50]

## <a name="next-steps"></a><span data-ttu-id="692aa-165">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="692aa-165">Next steps</span></span>

<span data-ttu-id="692aa-166">В этом учебнике вы узнали, как файл hello toouse отправить возможности передачи файлов toosimplify с устройств центра IoT.</span><span class="sxs-lookup"><span data-stu-id="692aa-166">In this tutorial, you learned how toouse hello file upload capabilities of IoT Hub toosimplify file uploads from devices.</span></span> <span data-ttu-id="692aa-167">Можно продолжить tooexplore IoT hub функции и сценарии hello в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="692aa-167">You can continue tooexplore IoT hub features and scenarios with hello following articles:</span></span>

* <span data-ttu-id="692aa-168">[Создание Центра Интернета вещей с помощью PowerShell][lnk-create-hub]</span><span class="sxs-lookup"><span data-stu-id="692aa-168">[Create an IoT hub programmatically][lnk-create-hub]</span></span>
* <span data-ttu-id="692aa-169">[Введение tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="692aa-169">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="692aa-170">[IoT Hub SDKs][lnk-sdks] (Пакеты SDK для Центра Интернета вещей)</span><span class="sxs-lookup"><span data-stu-id="692aa-170">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="692aa-171">Изучение возможностей hello центра IoT toofurther см. в разделе:</span><span class="sxs-lookup"><span data-stu-id="692aa-171">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="692aa-172">[Simulating a device with IoT Edge][lnk-iotedge] (Моделирование устройства с помощью Edge Интернета вещей)</span><span class="sxs-lookup"><span data-stu-id="692aa-172">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

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
