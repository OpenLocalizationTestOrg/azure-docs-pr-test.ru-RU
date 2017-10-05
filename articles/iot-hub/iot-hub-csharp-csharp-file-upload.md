---
title: "Отправка файлов с устройств в Центр Интернета вещей Azure | Документация Майкрософт"
description: "Сведения об отправке файлов с устройства в облако с помощью пакета SDK для устройств Azure IoT для .NET. Отправленные файлы хранятся в контейнере больших двоичных объектов службы хранилища Azure."
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
ms.openlocfilehash: b45d85d0d77cf47f36cb793bc8c0dbe2d5c12634
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="upload-files-from-your-device-to-the-cloud-with-iot-hub-using-net"></a><span data-ttu-id="8b721-104">Передача файлов с устройства в облако с помощью Центра Интернета вещей и .NET</span><span class="sxs-lookup"><span data-stu-id="8b721-104">Upload files from your device to the cloud with IoT Hub using .NET</span></span>

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

<span data-ttu-id="8b721-105">В этом учебнике используется код учебника [Отправка сообщений из облака на устройства с помощью Центра Интернета вещей](iot-hub-csharp-csharp-c2d.md) , чтобы показать, как использовать возможности передачи файлов в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="8b721-105">This tutorial builds on the code in the [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorial to show you how to use the file upload capabilities of IoT Hub.</span></span> <span data-ttu-id="8b721-106">В нем показано следующее:</span><span class="sxs-lookup"><span data-stu-id="8b721-106">It shows you how to:</span></span>

- <span data-ttu-id="8b721-107">как безопасно предоставить устройству универсальный код ресурса (URI) большого двоичного объекта Azure для передачи файла;</span><span class="sxs-lookup"><span data-stu-id="8b721-107">Securely provide a device with an Azure blob URI for uploading a file.</span></span>
- <span data-ttu-id="8b721-108">как использовать уведомления о передаче файлов Центра Интернета вещей для активации обработки файла в серверной части приложения.</span><span class="sxs-lookup"><span data-stu-id="8b721-108">Use the IoT Hub file upload notifications to trigger processing the file in your app back end.</span></span>

<span data-ttu-id="8b721-109">В руководствах [Подключение устройства к Центру Интернета вещей с помощью .NET](iot-hub-csharp-csharp-getstarted.md) и [Отправка сообщений из облака в виртуальное устройство с помощью Центра Интернета вещей (.NET)](iot-hub-csharp-csharp-c2d.md) описаны базовые функции Центра Интернета вещей для обмена сообщениями между устройством и облаком.</span><span class="sxs-lookup"><span data-stu-id="8b721-109">The [Get started with IoT Hub](iot-hub-csharp-csharp-getstarted.md) and [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorials show the basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span> <span data-ttu-id="8b721-110">В статье [Руководство. Как обрабатывать сообщения, отправляемые с устройства Центра Интернета вещей в облако, с помощью .NET](iot-hub-csharp-csharp-process-d2c.md) описан способ надежного хранения сообщений, отправляемых с устройства в облако, в хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="8b721-110">The [Process Device-to-Cloud messages](iot-hub-csharp-csharp-process-d2c.md) tutorial describes a way to reliably store device-to-cloud messages in Azure blob storage.</span></span> <span data-ttu-id="8b721-111">Тем не менее в некоторых случаях не просто сопоставить данные, отправляемые устройством, с относительно небольшими сообщениями, отправляемыми из устройства в облако, которые принимает Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="8b721-111">However, in some scenarios you cannot easily map the data your devices send into the relatively small device-to-cloud messages that IoT Hub accepts.</span></span> <span data-ttu-id="8b721-112">Например:</span><span class="sxs-lookup"><span data-stu-id="8b721-112">For example:</span></span>

* <span data-ttu-id="8b721-113">Большие файлы, содержащие изображения.</span><span class="sxs-lookup"><span data-stu-id="8b721-113">Large files that contain images</span></span>
* <span data-ttu-id="8b721-114">Видеоролики</span><span class="sxs-lookup"><span data-stu-id="8b721-114">Videos</span></span>
* <span data-ttu-id="8b721-115">Данные вибрации с высокой частотой выборки.</span><span class="sxs-lookup"><span data-stu-id="8b721-115">Vibration data sampled at high frequency</span></span>
* <span data-ttu-id="8b721-116">Некоторые виды предварительно обработанных данных.</span><span class="sxs-lookup"><span data-stu-id="8b721-116">Some form of preprocessed data</span></span>

<span data-ttu-id="8b721-117">Эти файлы обычно обрабатываются в виде пакета в облаке с помощью таких инструментов, как [фабрика данных Azure](../data-factory/index.md) или стек [Hadoop](../hdinsight/index.md).</span><span class="sxs-lookup"><span data-stu-id="8b721-117">These files are typically batch processed in the cloud using tools such as [Azure Data Factory](../data-factory/index.md) or the [Hadoop](../hdinsight/index.md) stack.</span></span> <span data-ttu-id="8b721-118">При передаче файлов с устройства вы можете рассчитывать на безопасность и надежность Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="8b721-118">When you need to upload files from a device, you can still use the security and reliability of IoT Hub.</span></span>

<span data-ttu-id="8b721-119">В конце этого руководства запускаются два консольных приложения для .NET:</span><span class="sxs-lookup"><span data-stu-id="8b721-119">At the end of this tutorial you run two .NET console apps:</span></span>

* <span data-ttu-id="8b721-120">**SimulatedDevice** — измененная версия приложения, созданного в руководстве [Как отправлять сообщения из облака на устройства с помощью Центра Интернета вещей и .NET](iot-hub-csharp-csharp-c2d.md).</span><span class="sxs-lookup"><span data-stu-id="8b721-120">**SimulatedDevice**, a modified version of the app created in the [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorial.</span></span> <span data-ttu-id="8b721-121">Это приложение передает файл в хранилище с помощью универсального кода ресурса (URI) SAS, предоставленного вашим Центром Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="8b721-121">This app uploads a file to storage using a SAS URI provided by your IoT hub.</span></span>
* <span data-ttu-id="8b721-122">**ReadFileUploadNotification**— приложение, которое получает уведомления о передаче файлов от Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="8b721-122">**ReadFileUploadNotification**, which receives file upload notifications from your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="8b721-123">Существуют пакеты SDK для устройств Интернета вещей Azure, обеспечивающие поддержку многих платформ устройств и языков (включая C, Java и JavaScript) в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="8b721-123">IoT Hub supports many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="8b721-124">Пошаговые инструкции по подключению устройства к Центру Интернета вещей Azure см. в [Центре разработчика Центра Интернета вещей Azure].</span><span class="sxs-lookup"><span data-stu-id="8b721-124">Refer to the [Azure IoT Developer Center] for step-by-step instructions on how to connect your device to Azure IoT Hub.</span></span>

<span data-ttu-id="8b721-125">Для работы с этим учебником требуется:</span><span class="sxs-lookup"><span data-stu-id="8b721-125">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="8b721-126">Visual Studio 2015 или Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="8b721-126">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="8b721-127">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="8b721-127">An active Azure account.</span></span> <span data-ttu-id="8b721-128">Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="8b721-128">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a><span data-ttu-id="8b721-129">Передача файла из приложения устройства</span><span class="sxs-lookup"><span data-stu-id="8b721-129">Upload a file from a device app</span></span>

<span data-ttu-id="8b721-130">В этом разделе вы измените приложение устройства, созданное в руководстве [Отправка сообщений из облака в виртуальное устройство с помощью Центра Интернета вещей (.NET)](iot-hub-csharp-csharp-c2d.md), чтобы с помощью Центра Интернета вещей передавать сообщения из облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="8b721-130">In this section, you modify the device app you created in [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) to receive cloud-to-device messages from the IoT hub.</span></span>

1. <span data-ttu-id="8b721-131">В Visual Studio щелкните правой кнопкой мыши проект **SimulatedDevice**, а затем последовательно выберите **Добавить** и **Существующий элемент**.</span><span class="sxs-lookup"><span data-stu-id="8b721-131">In Visual Studio, right-click the **SimulatedDevice** project, click **Add**, and then click **Existing Item**.</span></span> <span data-ttu-id="8b721-132">Перейдите к файлу образа и добавьте его в проект.</span><span class="sxs-lookup"><span data-stu-id="8b721-132">Navigate to an image file and include it in your project.</span></span> <span data-ttu-id="8b721-133">В этом учебнике используется образ `image.jpg`.</span><span class="sxs-lookup"><span data-stu-id="8b721-133">This tutorial assumes the image is named `image.jpg`.</span></span>

1. <span data-ttu-id="8b721-134">Щелкните его правой кнопкой мыши и выберите пункт **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="8b721-134">Right-click on the image, and then click **Properties**.</span></span> <span data-ttu-id="8b721-135">Убедитесь, что параметр **Копировать в выходной каталог** имеет значение **Всегда копировать**.</span><span class="sxs-lookup"><span data-stu-id="8b721-135">Make sure that **Copy to Output Directory** is set to **Copy always**.</span></span>

    ![][1]

1. <span data-ttu-id="8b721-136">Добавьте в начало файла **Program.cs** следующие инструкции:</span><span class="sxs-lookup"><span data-stu-id="8b721-136">In the **Program.cs** file, add the following statements at the top of the file:</span></span>

    ```csharp
    using System.IO;
    ```

1. <span data-ttu-id="8b721-137">Добавьте следующий метод в класс **Program** .</span><span class="sxs-lookup"><span data-stu-id="8b721-137">Add the following method to the **Program** class:</span></span>

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
        Console.WriteLine("Time to upload file: {0}ms\n", watch.ElapsedMilliseconds);
    }
    ```

    <span data-ttu-id="8b721-138">Метод `UploadToBlobAsync` принимает имя передаваемого файла и источник его передачи и обрабатывает передачу в хранилище.</span><span class="sxs-lookup"><span data-stu-id="8b721-138">The `UploadToBlobAsync` method takes in the file name and stream source of the file to be uploaded and handles the upload to storage.</span></span> <span data-ttu-id="8b721-139">Консольное приложение отображает время, необходимое для отправки файла.</span><span class="sxs-lookup"><span data-stu-id="8b721-139">The console app displays the time it takes to upload the file.</span></span>

1. <span data-ttu-id="8b721-140">Добавьте в метод **Main** непосредственно перед строкой `Console.ReadLine()` следующий метод:</span><span class="sxs-lookup"><span data-stu-id="8b721-140">Add the following method in the **Main** method, right before the `Console.ReadLine()` line:</span></span>

    ```csharp
    SendToBlobAsync();
    ```

> [!NOTE]
> <span data-ttu-id="8b721-141">Для упрощения в этом руководстве не реализуются какие-либо политики повтора.</span><span class="sxs-lookup"><span data-stu-id="8b721-141">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="8b721-142">В рабочем коде следует реализовать политики повтора (например, экспоненциальную задержку), как указано в статье MSDN [Transient Fault Handling](Обработка временного сбоя).</span><span class="sxs-lookup"><span data-stu-id="8b721-142">In production code, you should implement retry policies (such as exponential backoff), as suggested in the MSDN article [Transient Fault Handling].</span></span>

## <a name="receive-a-file-upload-notification"></a><span data-ttu-id="8b721-143">Получение уведомления о передачи файла</span><span class="sxs-lookup"><span data-stu-id="8b721-143">Receive a file upload notification</span></span>

<span data-ttu-id="8b721-144">В этом разделе вам предстоит создать консольное приложение для .NET, которое получает уведомления об отправке файлов из Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="8b721-144">In this section, you write a .NET console app that receives file upload notification messages from IoT Hub.</span></span>

1. <span data-ttu-id="8b721-145">В текущем решении Visual Studio создайте проект Windows на языке Visual C#, используя шаблон проекта **Консольное приложение** .</span><span class="sxs-lookup"><span data-stu-id="8b721-145">In the current Visual Studio solution, create a Visual C# Windows project by using the **Console Application** project template.</span></span> <span data-ttu-id="8b721-146">Назовите проект **ReadFileUploadNotification**.</span><span class="sxs-lookup"><span data-stu-id="8b721-146">Name the project **ReadFileUploadNotification**.</span></span>

    ![Создание проекта в Visual Studio][2]

1. <span data-ttu-id="8b721-148">В обозревателе решений щелкните правой кнопкой мыши проект **ReadFileUploadNotification** и выберите пункт **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="8b721-148">In Solution Explorer, right-click the **ReadFileUploadNotification** project, and then click **Manage NuGet Packages...**.</span></span>

1. <span data-ttu-id="8b721-149">В окне **Диспетчер пакетов NuGet** найдите **Microsoft.Azure.Devices**, а затем щелкните **Установить** и примите условия использования.</span><span class="sxs-lookup"><span data-stu-id="8b721-149">In the **NuGet Package Manager** window, search for **Microsoft.Azure.Devices**, click **Install**, and accept the terms of use.</span></span>

    <span data-ttu-id="8b721-150">После этого действия будет скачан и установлен [пакет SDK NuGet для служб Azure IoT] и добавлены ссылки на него в проект **ReadFileUploadNotification**.</span><span class="sxs-lookup"><span data-stu-id="8b721-150">This action downloads, installs, and adds a reference to the [Azure IoT service SDK NuGet package] in the **ReadFileUploadNotification** project.</span></span>

1. <span data-ttu-id="8b721-151">Добавьте в начало файла **Program.cs** следующие инструкции:</span><span class="sxs-lookup"><span data-stu-id="8b721-151">In the **Program.cs** file, add the following statements at the top of the file:</span></span>

    ```csharp
    using Microsoft.Azure.Devices;
    ```

1. <span data-ttu-id="8b721-152">Добавьте следующие поля в класс **Program** .</span><span class="sxs-lookup"><span data-stu-id="8b721-152">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="8b721-153">Замените значение заполнителя строкой подключения центра Интернета вещей из статьи "Подключение устройства к Центру Интернета вещей с помощью .NET".</span><span class="sxs-lookup"><span data-stu-id="8b721-153">Substitute the placeholder value with the IoT hub connection string from [Get started with IoT Hub]:</span></span>

    ```csharp
    static ServiceClient serviceClient;
    static string connectionString = "{iot hub connection string}";
    ```

1. <span data-ttu-id="8b721-154">Добавьте следующий метод в класс **Program** .</span><span class="sxs-lookup"><span data-stu-id="8b721-154">Add the following method to the **Program** class:</span></span>

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

    <span data-ttu-id="8b721-155">Обратите внимание, что шаблон получения здесь аналогичен шаблону, использовавшемуся для получения сообщений из облака на устройство из приложения устройства.</span><span class="sxs-lookup"><span data-stu-id="8b721-155">Note this receive pattern is the same one used to receive cloud-to-device messages from the device app.</span></span>

1. <span data-ttu-id="8b721-156">Наконец, добавьте следующие строки в метод **Main** :</span><span class="sxs-lookup"><span data-stu-id="8b721-156">Finally, add the following lines to the **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Receive file upload notifications\n");
    serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
    ReceiveFileUploadNotificationAsync();
    Console.WriteLine("Press Enter to exit\n");
    Console.ReadLine();
    ```

## <a name="run-the-applications"></a><span data-ttu-id="8b721-157">Запуск приложений</span><span class="sxs-lookup"><span data-stu-id="8b721-157">Run the applications</span></span>

<span data-ttu-id="8b721-158">Теперь все готово к запуску приложений.</span><span class="sxs-lookup"><span data-stu-id="8b721-158">Now you are ready to run the applications.</span></span>

1. <span data-ttu-id="8b721-159">В Visual Studio щелкните правой кнопкой мыши свое решение и выберите пункт **Назначить запускаемые проекты**.</span><span class="sxs-lookup"><span data-stu-id="8b721-159">In Visual Studio, right-click your solution, and select **Set StartUp projects**.</span></span> <span data-ttu-id="8b721-160">Выберите **Несколько запускаемых проектов**, а затем выберите действие **Запуск** для обоих приложений — **ReadFileUploadNotification** и **SimulatedDevice**.</span><span class="sxs-lookup"><span data-stu-id="8b721-160">Select **Multiple startup projects**, then select the **Start** action for **ReadFileUploadNotification** and **SimulatedDevice**.</span></span>

1. <span data-ttu-id="8b721-161">Нажмите клавишу **F5**.</span><span class="sxs-lookup"><span data-stu-id="8b721-161">Press **F5**.</span></span> <span data-ttu-id="8b721-162">Должны запуститься оба приложения.</span><span class="sxs-lookup"><span data-stu-id="8b721-162">Both applications should start.</span></span> <span data-ttu-id="8b721-163">Вы должны увидеть, как завершится передача в одном консольном приложении и как другое консольное приложение получит уведомление о передаче.</span><span class="sxs-lookup"><span data-stu-id="8b721-163">You should see the upload completed in one console app and the upload notification message received by the other console app.</span></span> <span data-ttu-id="8b721-164">Наличие отправленного файла в учетной записи хранения Azure можно проверить с помощью [портала Azure] или обозревателя серверов Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8b721-164">You can use the [Azure portal] or Visual Studio Server Explorer to check for the presence of the uploaded file in your Azure Storage account.</span></span>

    ![][50]

## <a name="next-steps"></a><span data-ttu-id="8b721-165">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8b721-165">Next steps</span></span>

<span data-ttu-id="8b721-166">В этом руководство показано, как использовать возможности передачи файлов Центра Интернета вещей, чтобы упростить передачу файлов из устройств.</span><span class="sxs-lookup"><span data-stu-id="8b721-166">In this tutorial, you learned how to use the file upload capabilities of IoT Hub to simplify file uploads from devices.</span></span> <span data-ttu-id="8b721-167">Изучение функций и сценариев Центра Интернета вещей можно продолжить в следующих руководствах:</span><span class="sxs-lookup"><span data-stu-id="8b721-167">You can continue to explore IoT hub features and scenarios with the following articles:</span></span>

* <span data-ttu-id="8b721-168">[Создание Центра Интернета вещей с помощью PowerShell][lnk-create-hub]</span><span class="sxs-lookup"><span data-stu-id="8b721-168">[Create an IoT hub programmatically][lnk-create-hub]</span></span>
* <span data-ttu-id="8b721-169">[Знакомство с пакетом SDK для устройств Центра Интернета вещей Azure для C][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="8b721-169">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="8b721-170">[IoT Hub SDKs][lnk-sdks] (Пакеты SDK для Центра Интернета вещей)</span><span class="sxs-lookup"><span data-stu-id="8b721-170">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="8b721-171">Для дальнейшего изучения возможностей Центра Интернета вещей см. следующие статьи:</span><span class="sxs-lookup"><span data-stu-id="8b721-171">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="8b721-172">[Simulating a device with IoT Edge][lnk-iotedge] (Моделирование устройства с помощью Edge Интернета вещей)</span><span class="sxs-lookup"><span data-stu-id="8b721-172">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

<!-- Images. -->

[50]: ./media/iot-hub-csharp-csharp-file-upload/run-apps1.png
[1]: ./media/iot-hub-csharp-csharp-file-upload/image-properties.png
[2]: ./media/iot-hub-csharp-csharp-file-upload/file-upload-project-csharp1.png

<!-- Links -->

<span data-ttu-id="8b721-173">[портала Azure]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="8b721-173">[Azure portal]: https://portal.azure.com/</span></span>

<span data-ttu-id="8b721-174">[Центре разработчика Центра Интернета вещей Azure]: http://www.azure.com/develop/iot</span><span class="sxs-lookup"><span data-stu-id="8b721-174">[Azure IoT Developer Center]: http://www.azure.com/develop/iot</span></span>

<span data-ttu-id="8b721-175">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span><span class="sxs-lookup"><span data-stu-id="8b721-175">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span></span>
<span data-ttu-id="8b721-176">[пакет SDK NuGet для служб Azure IoT]: https://www.nuget.org/packages/Microsoft.Azure.Devices/</span><span class="sxs-lookup"><span data-stu-id="8b721-176">[Azure IoT service SDK NuGet package]: https://www.nuget.org/packages/Microsoft.Azure.Devices/</span></span>
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-windows-iot-edge-simulated-device.md
