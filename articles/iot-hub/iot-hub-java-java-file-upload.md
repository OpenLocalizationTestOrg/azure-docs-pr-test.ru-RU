---
title: "файлы aaaUpload из tooAzure устройств IoT Hub с Java | Документы Microsoft"
description: "Как tooupload файлы из облака toohello устройства, с помощью устройств Azure IoT SDK для Java. Отправленные файлы хранятся в контейнере больших двоичных объектов службы хранилища Azure."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4759d229-f856-4526-abda-414f8b00a56d
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: dobett
ms.openlocfilehash: e305fe61bf7ca0aeb2c092bc2c7efebdc78d4f68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-from-your-device-toohello-cloud-with-iot-hub"></a><span data-ttu-id="ca82b-104">Отправка файлов в облаке toohello устройства с центром IoT</span><span class="sxs-lookup"><span data-stu-id="ca82b-104">Upload files from your device toohello cloud with IoT Hub</span></span>

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

<span data-ttu-id="ca82b-105">Этот учебник построен на кода hello в hello [отправки сообщений облака на устройство с центром IoT](iot-hub-java-java-c2d.md) tooshow учебника вы как toouse hello [файла возможности передачи центра IoT](iot-hub-devguide-file-upload.md) tooupload файл слишком[ Хранилище больших двоичных объектов](../storage/index.md).</span><span class="sxs-lookup"><span data-stu-id="ca82b-105">This tutorial builds on hello code in hello [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) tutorial tooshow you how toouse hello [file upload capabilities of IoT Hub](iot-hub-devguide-file-upload.md) tooupload a file too[Azure blob storage](../storage/index.md).</span></span> <span data-ttu-id="ca82b-106">Hello учебнике показано, как для:</span><span class="sxs-lookup"><span data-stu-id="ca82b-106">hello tutorial shows you how to:</span></span>

- <span data-ttu-id="ca82b-107">как безопасно предоставить устройству универсальный код ресурса (URI) большого двоичного объекта Azure для передачи файла;</span><span class="sxs-lookup"><span data-stu-id="ca82b-107">Securely provide a device with an Azure blob URI for uploading a file.</span></span>
- <span data-ttu-id="ca82b-108">Используйте центр IoT файл отправки уведомления tootrigger обработке hello файла в серверной части вашего приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ca82b-108">Use hello IoT Hub file upload notifications tootrigger processing hello file in your app back end.</span></span>

<span data-ttu-id="ca82b-109">Hello [приступить к работе с центром IoT](iot-hub-java-java-getstarted.md) и [отправки сообщений облака на устройство с центром IoT](iot-hub-java-java-c2d.md) руководствах hello основные устройства в облако и облака на устройство обмена сообщениями функции центра IoT.</span><span class="sxs-lookup"><span data-stu-id="ca82b-109">hello [Get started with IoT Hub](iot-hub-java-java-getstarted.md) and [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) tutorials show hello basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span> <span data-ttu-id="ca82b-110">Hello [сообщений процесс устройства в облако](iot-hub-java-java-process-d2c.md) учебнике рассматривается способ tooreliably записи устройства в облако сообщений в хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="ca82b-110">hello [Process Device-to-Cloud messages](iot-hub-java-java-process-d2c.md) tutorial describes a way tooreliably store device-to-cloud messages in Azure blob storage.</span></span> <span data-ttu-id="ca82b-111">Однако в некоторых сценариях невозможно сопоставить легко hello данных устройствами отправки на относительно небольшой устройства в облако сообщений hello, которое принимает центр IoT.</span><span class="sxs-lookup"><span data-stu-id="ca82b-111">However, in some scenarios you cannot easily map hello data your devices send into hello relatively small device-to-cloud messages that IoT Hub accepts.</span></span> <span data-ttu-id="ca82b-112">Например:</span><span class="sxs-lookup"><span data-stu-id="ca82b-112">For example:</span></span>

* <span data-ttu-id="ca82b-113">Большие файлы, содержащие изображения.</span><span class="sxs-lookup"><span data-stu-id="ca82b-113">Large files that contain images</span></span>
* <span data-ttu-id="ca82b-114">Видеоролики</span><span class="sxs-lookup"><span data-stu-id="ca82b-114">Videos</span></span>
* <span data-ttu-id="ca82b-115">Данные вибрации с высокой частотой выборки.</span><span class="sxs-lookup"><span data-stu-id="ca82b-115">Vibration data sampled at high frequency</span></span>
* <span data-ttu-id="ca82b-116">Некоторые виды предварительно обработанных данных.</span><span class="sxs-lookup"><span data-stu-id="ca82b-116">Some form of preprocessed data.</span></span>

<span data-ttu-id="ca82b-117">Эти файлы обычно являются пакетной обработки в облаке hello, с помощью средств, таких как [фабрики данных Azure](../data-factory/index.md) или hello [Hadoop](../hdinsight/index.md) стека.</span><span class="sxs-lookup"><span data-stu-id="ca82b-117">These files are typically batch processed in hello cloud using tools such as [Azure Data Factory](../data-factory/index.md) or hello [Hadoop](../hdinsight/index.md) stack.</span></span> <span data-ttu-id="ca82b-118">Если вам требуется tooupland файлы с устройства, по-прежнему можно использовать hello безопасности и надежности центр IoT.</span><span class="sxs-lookup"><span data-stu-id="ca82b-118">When you need tooupland files from a device, you can still use hello security and reliability of IoT Hub.</span></span>

<span data-ttu-id="ca82b-119">В конце этого учебника в hello выполните две консольные приложения Java:</span><span class="sxs-lookup"><span data-stu-id="ca82b-119">At hello end of this tutorial you run two Java console apps:</span></span>

* <span data-ttu-id="ca82b-120">**имитируемые устройства**, измененная версия приложения hello, созданного в учебнике hello [сообщений Send облака на устройство с центром IoT].</span><span class="sxs-lookup"><span data-stu-id="ca82b-120">**simulated-device**, a modified version of hello app created in hello [Send Cloud-to-Device messages with IoT Hub] tutorial.</span></span> <span data-ttu-id="ca82b-121">Это приложение передает файл toostorage, с помощью URI SAS, предоставляемые концентратор IoT.</span><span class="sxs-lookup"><span data-stu-id="ca82b-121">This app uploads a file toostorage using a SAS URI provided by your IoT hub.</span></span>
* <span data-ttu-id="ca82b-122">**read-file-upload-notification** — приложение, которое получает уведомления о передаче файлов от Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="ca82b-122">**read-file-upload-notification**, which receives file upload notifications from your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="ca82b-123">Существуют пакеты SDK для устройств Центра Интернета вещей Azure, обеспечивающие поддержку многих платформ устройств и языков (включая C, .NET и JavaScript) в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="ca82b-123">IoT Hub supports many device platforms and languages (including C, .NET, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="ca82b-124">См. toohello [Центр разработчиков Azure IoT] пошаговые инструкции о том, как tooconnect tooAzure вашего устройства центра IoT.</span><span class="sxs-lookup"><span data-stu-id="ca82b-124">Refer toohello [Azure IoT Developer Center] for step-by-step instructions on how tooconnect your device tooAzure IoT Hub.</span></span>

<span data-ttu-id="ca82b-125">toocomplete этого учебника требуется hello следующие:</span><span class="sxs-lookup"><span data-stu-id="ca82b-125">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="ca82b-126">Здравствуйте, последняя версия [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="ca82b-126">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="ca82b-127">Maven 3</span><span class="sxs-lookup"><span data-stu-id="ca82b-127">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="ca82b-128">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="ca82b-128">An active Azure account.</span></span> <span data-ttu-id="ca82b-129">Если ее нет, можно создать [бесплатную учетную запись](http://azure.microsoft.com/pricing/free-trial/) всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="ca82b-129">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a><span data-ttu-id="ca82b-130">Передача файла из приложения устройства</span><span class="sxs-lookup"><span data-stu-id="ca82b-130">Upload a file from a device app</span></span>

<span data-ttu-id="ca82b-131">В этом разделе, измените приложение hello устройства, созданный в [отправки сообщений облака на устройство с центром IoT](iot-hub-java-java-c2d.md) tooupload концентратор tooIoT файла.</span><span class="sxs-lookup"><span data-stu-id="ca82b-131">In this section, you modify hello device app you created in [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) tooupload a file tooIoT hub.</span></span>

1. <span data-ttu-id="ca82b-132">Скопируйте файл изображения toohello `simulated-device` папку и переименуйте его в `myimage.png`.</span><span class="sxs-lookup"><span data-stu-id="ca82b-132">Copy an image file toohello `simulated-device` folder and rename it `myimage.png`.</span></span>

1. <span data-ttu-id="ca82b-133">В текстовом редакторе, откройте hello `simulated-device\src\main\java\com\mycompany\app\App.java` файла.</span><span class="sxs-lookup"><span data-stu-id="ca82b-133">Using a text editor, open hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="ca82b-134">Добавьте объявление переменной toohello hello **приложения** класса:</span><span class="sxs-lookup"><span data-stu-id="ca82b-134">Add hello variable declaration toohello **App** class:</span></span>

    ```java
    private static String fileName = "myimage.png";
    ```

1. <span data-ttu-id="ca82b-135">tooprocess обратного вызова сообщения о состоянии передачи файлов, добавьте следующее hello вложенных классов toohello **приложения** класса:</span><span class="sxs-lookup"><span data-stu-id="ca82b-135">tooprocess file upload status callback messages, add hello following nested class toohello **App** class:</span></span>

    ```java
    // Define a callback method tooprint status codes from IoT Hub.
    protected static class FileUploadStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toofile upload for " + fileName
            + " operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="ca82b-136">tooIoT изображения tooupload концентратора, добавьте следующий метод toohello hello **приложения** tooupload класс образы tooIoT концентратора:</span><span class="sxs-lookup"><span data-stu-id="ca82b-136">tooupload images tooIoT Hub, add hello following method toohello **App** class tooupload images tooIoT Hub:</span></span>

    ```java
    // Use IoT Hub tooupload a file asynchronously tooAzure blob storage.
    private static void uploadFile(String fullFileName) throws FileNotFoundException, IOException
    {
      File file = new File(fullFileName);
      InputStream inputStream = new FileInputStream(file);
      long streamLength = file.length();

      client.uploadToBlobAsync(fileName, inputStream, streamLength, new FileUploadStatusCallBack(), null);
    }
    ```

1. <span data-ttu-id="ca82b-137">Изменение hello **основной** hello метод toocall **uploadFile** метода, как показано в следующий фрагмент кода hello:</span><span class="sxs-lookup"><span data-stu-id="ca82b-137">Modify hello **main** method toocall hello **uploadFile** method as shown in hello following snippet:</span></span>

    ```java
    client.open();

    try
    {
      // Get hello filename and start hello upload.
      String fullFileName = System.getProperty("user.dir") + File.separator + fileName;
      uploadFile(fullFileName);
      System.out.println("File upload started with success");
    }
    catch (Exception e)
    {
      System.out.println("Exception uploading file: " + e.getCause() + " \nERROR: " + e.getMessage());
    }

    MessageSender sender = new MessageSender();
    ```

1. <span data-ttu-id="ca82b-138">Используйте hello следующая команда toobuild hello **имитируемые устройства** приложение и проверьте наличие ошибок:</span><span class="sxs-lookup"><span data-stu-id="ca82b-138">Use hello following command toobuild hello **simulated-device** app and check for errors:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="receive-a-file-upload-notification"></a><span data-ttu-id="ca82b-139">Получение уведомления о передачи файла</span><span class="sxs-lookup"><span data-stu-id="ca82b-139">Receive a file upload notification</span></span>

<span data-ttu-id="ca82b-140">В этом разделе вам предстоит создать консольное приложение для Java, которое получает уведомления об отправке файлов из Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="ca82b-140">In this section, you create a Java console app that receives file upload notification messages from IoT Hub.</span></span>

<span data-ttu-id="ca82b-141">Требуется hello **iothubowner** строка соединения для вашего центра IoT toocomplete в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="ca82b-141">You need hello **iothubowner** connection string for your IoT Hub toocomplete this section.</span></span> <span data-ttu-id="ca82b-142">Строка подключения hello можно найти в hello [портал Azure](https://portal.azure.com/) на hello **политики общего доступа** колонку.</span><span class="sxs-lookup"><span data-stu-id="ca82b-142">You can find hello connection string in hello [Azure portal](https://portal.azure.com/) on hello **Shared access policy** blade.</span></span>

1. <span data-ttu-id="ca82b-143">Создайте проект с именем Maven **чтение файла Отправка уведомления** с помощью hello следующую команду в командной строке.</span><span class="sxs-lookup"><span data-stu-id="ca82b-143">Create a Maven project called **read-file-upload-notification** using hello following command at your command prompt.</span></span> <span data-ttu-id="ca82b-144">Обратите внимание, что это одна длинная команда.</span><span class="sxs-lookup"><span data-stu-id="ca82b-144">Note this command is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-file-upload-notification -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

1. <span data-ttu-id="ca82b-145">В командной строке перейдите toohello новый `read-file-upload-notification` папки.</span><span class="sxs-lookup"><span data-stu-id="ca82b-145">At your command prompt, navigate toohello new `read-file-upload-notification` folder.</span></span>

1. <span data-ttu-id="ca82b-146">В текстовом редакторе, откройте hello `pom.xml` файла в hello `read-file-upload-notification` папки и добавьте следующие зависимости toohello hello **зависимости** узла.</span><span class="sxs-lookup"><span data-stu-id="ca82b-146">Using a text editor, open hello `pom.xml` file in hello `read-file-upload-notification` folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="ca82b-147">Добавление зависимости hello позволяет toouse hello **центром IOT java служба клиента** пакета в toocommunicate вашего приложения в службе концентратора IoT:</span><span class="sxs-lookup"><span data-stu-id="ca82b-147">Adding hello dependency enables you toouse hello **iothub-java-service-client** package in your application toocommunicate with your IoT hub service:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="ca82b-148">Вы можете проверить наличие hello последнюю версию **клиента для службы iot** с помощью [Maven поиска](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="ca82b-148">You can check for hello latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="ca82b-149">Сохраните и закройте hello `pom.xml` файла.</span><span class="sxs-lookup"><span data-stu-id="ca82b-149">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="ca82b-150">В текстовом редакторе, откройте hello `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` файла.</span><span class="sxs-lookup"><span data-stu-id="ca82b-150">Using a text editor, open hello `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="ca82b-151">Добавьте следующее hello **импорта** toohello файл инструкций:</span><span class="sxs-lookup"><span data-stu-id="ca82b-151">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.concurrent.ExecutorService;
    import java.util.concurrent.Executors;
    ```

1. <span data-ttu-id="ca82b-152">Добавьте следующие переменные уровня класса toohello hello **приложения** класса:</span><span class="sxs-lookup"><span data-stu-id="ca82b-152">Add hello following class-level variables toohello **App** class:</span></span>

    ```java
    private static final String connectionString = "{Your IoT Hub connection string}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    private static FileUploadNotificationReceiver fileUploadNotificationReceiver = null;
    ```

1. <span data-ttu-id="ca82b-153">tooprint сведения о консоли toohello передачи файла hello, добавьте следующее hello вложенных классов toohello **приложения** класса:</span><span class="sxs-lookup"><span data-stu-id="ca82b-153">tooprint information about hello file upload toohello console, add hello following nested class toohello **App** class:</span></span>

    ```java
    // Create a thread tooreceive file upload notifications.
    private static class ShowFileUploadNotifications implements Runnable {
      public void run() {
        try {
          while (true) {
            System.out.println("Recieve file upload notifications...");
            FileUploadNotification fileUploadNotification = fileUploadNotificationReceiver.receive();
            if (fileUploadNotification != null) {
              System.out.println("File Upload notification received");
              System.out.println("Device Id : " + fileUploadNotification.getDeviceId());
              System.out.println("Blob Uri: " + fileUploadNotification.getBlobUri());
              System.out.println("Blob Name: " + fileUploadNotification.getBlobName());
              System.out.println("Last Updated : " + fileUploadNotification.getLastUpdatedTimeDate());
              System.out.println("Blob Size (Bytes): " + fileUploadNotification.getBlobSizeInBytes());
              System.out.println("Enqueued Time: " + fileUploadNotification.getEnqueuedTimeUtcDate());
            }
          }
        } catch (Exception ex) {
          System.out.println("Exception reading reported properties: " + ex.getMessage());
        }
      }
    }
    ```

1. <span data-ttu-id="ca82b-154">toostart hello поток, который осуществляет прослушивание уведомлений передачи файла, добавьте следующий код toohello hello **основной** метод:</span><span class="sxs-lookup"><span data-stu-id="ca82b-154">toostart hello thread that listens for file upload notifications, add hello following code toohello **main** method:</span></span>

    ```java
    public static void main(String[] args) throws IOException, URISyntaxException, Exception {
      ServiceClient serviceClient = ServiceClient.createFromConnectionString(connectionString, protocol);

      if (serviceClient != null) {
        serviceClient.open();

        // Get a file upload notification receiver from hello ServiceClient.
        fileUploadNotificationReceiver = serviceClient.getFileUploadNotificationReceiver();
        fileUploadNotificationReceiver.open();

        // Start hello thread tooreceive file upload notifications.
        ShowFileUploadNotifications showFileUploadNotifications = new ShowFileUploadNotifications();
        ExecutorService executor = Executors.newFixedThreadPool(1);
        executor.execute(showFileUploadNotifications);

        System.out.println("Press ENTER tooexit.");
        System.in.read();
        executor.shutdownNow();
        System.out.println("Shutting down sample...");
        fileUploadNotificationReceiver.close();
        serviceClient.close();
      }
    }
    ```

1. <span data-ttu-id="ca82b-155">Сохраните и закройте hello `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` файла.</span><span class="sxs-lookup"><span data-stu-id="ca82b-155">Save and close hello `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="ca82b-156">Используйте hello следующая команда toobuild hello **чтение файла Отправка уведомления** приложение и проверьте наличие ошибок:</span><span class="sxs-lookup"><span data-stu-id="ca82b-156">Use hello following command toobuild hello **read-file-upload-notification** app and check for errors:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-hello-applications"></a><span data-ttu-id="ca82b-157">Запускать приложения hello</span><span class="sxs-lookup"><span data-stu-id="ca82b-157">Run hello applications</span></span>

<span data-ttu-id="ca82b-158">Теперь все готово toorun приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ca82b-158">Now you are ready toorun hello applications.</span></span>

<span data-ttu-id="ca82b-159">В командной строке в hello `read-file-upload-notification` папки, запустите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ca82b-159">At a command prompt in hello `read-file-upload-notification` folder, run hello following command:</span></span>

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

<span data-ttu-id="ca82b-160">В командной строке в hello `simulated-device` папки, запустите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ca82b-160">At a command prompt in hello `simulated-device` folder, run hello following command:</span></span>

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

<span data-ttu-id="ca82b-161">Hello следующем снимке экрана показан вывод hello hello **имитируемые устройства** приложения:</span><span class="sxs-lookup"><span data-stu-id="ca82b-161">hello following screenshot shows hello output from hello **simulated-device** app:</span></span>

![Выходные данные приложения simulated-device](media/iot-hub-java-java-upload/simulated-device.png)

<span data-ttu-id="ca82b-163">Hello следующем снимке экрана показан вывод hello hello **чтение файла Отправка уведомления** приложения:</span><span class="sxs-lookup"><span data-stu-id="ca82b-163">hello following screenshot shows hello output from hello **read-file-upload-notification** app:</span></span>

![Выходные данные приложения read-file-upload-notification](media/iot-hub-java-java-upload/read-file-upload-notification.png)

<span data-ttu-id="ca82b-165">Можно использовать файл загружен hello портала tooview hello в контейнере хранилища hello, настроенному:</span><span class="sxs-lookup"><span data-stu-id="ca82b-165">You can use hello portal tooview hello uploaded file in hello storage container you configured:</span></span>

![Отправленный файл](media/iot-hub-java-java-upload/uploaded-file.png)

## <a name="next-steps"></a><span data-ttu-id="ca82b-167">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ca82b-167">Next steps</span></span>

<span data-ttu-id="ca82b-168">В этом учебнике вы узнали, как файл hello toouse отправить возможности передачи файлов toosimplify с устройств центра IoT.</span><span class="sxs-lookup"><span data-stu-id="ca82b-168">In this tutorial, you learned how toouse hello file upload capabilities of IoT Hub toosimplify file uploads from devices.</span></span> <span data-ttu-id="ca82b-169">Можно продолжить tooexplore IoT hub функции и сценарии hello в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="ca82b-169">You can continue tooexplore IoT hub features and scenarios with hello following articles:</span></span>

* <span data-ttu-id="ca82b-170">[Создание Центра Интернета вещей с помощью PowerShell][lnk-create-hub]</span><span class="sxs-lookup"><span data-stu-id="ca82b-170">[Create an IoT hub programmatically][lnk-create-hub]</span></span>
* <span data-ttu-id="ca82b-171">[Введение tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="ca82b-171">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="ca82b-172">[IoT Hub SDKs][lnk-sdks] (Пакеты SDK для Центра Интернета вещей)</span><span class="sxs-lookup"><span data-stu-id="ca82b-172">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="ca82b-173">Изучение возможностей hello центра IoT toofurther см. в разделе:</span><span class="sxs-lookup"><span data-stu-id="ca82b-173">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="ca82b-174">[Simulating a device with IoT Edge][lnk-iotedge] (Моделирование устройства с помощью Edge Интернета вещей)</span><span class="sxs-lookup"><span data-stu-id="ca82b-174">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

<!-- Images. -->

[50]: ./media/iot-hub-csharp-csharp-file-upload/run-apps1.png
[1]: ./media/iot-hub-csharp-csharp-file-upload/image-properties.png
[2]: ./media/iot-hub-csharp-csharp-file-upload/file-upload-project-csharp1.png
[3]: ./media/iot-hub-csharp-csharp-file-upload/enable-file-notifications.png

<!-- Links -->



[Центр разработчиков Azure IoT]: http://www.azure.com/develop/iot

[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[Azure Storage]:../storage/common/storage-create-storage-account.md#create-a-storage-account
[lnk-configure-upload]: iot-hub-configure-file-upload.md
[Azure IoT service SDK NuGet package]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-windows-iot-edge-simulated-device.md


