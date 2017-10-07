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
# <a name="upload-files-from-your-device-toohello-cloud-with-iot-hub"></a>Отправка файлов в облаке toohello устройства с центром IoT

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

Этот учебник построен на кода hello в hello [отправки сообщений облака на устройство с центром IoT](iot-hub-java-java-c2d.md) tooshow учебника вы как toouse hello [файла возможности передачи центра IoT](iot-hub-devguide-file-upload.md) tooupload файл слишком[ Хранилище больших двоичных объектов](../storage/index.md). Hello учебнике показано, как для:

- как безопасно предоставить устройству универсальный код ресурса (URI) большого двоичного объекта Azure для передачи файла;
- Используйте центр IoT файл отправки уведомления tootrigger обработке hello файла в серверной части вашего приложения hello.

Hello [приступить к работе с центром IoT](iot-hub-java-java-getstarted.md) и [отправки сообщений облака на устройство с центром IoT](iot-hub-java-java-c2d.md) руководствах hello основные устройства в облако и облака на устройство обмена сообщениями функции центра IoT. Hello [сообщений процесс устройства в облако](iot-hub-java-java-process-d2c.md) учебнике рассматривается способ tooreliably записи устройства в облако сообщений в хранилище больших двоичных объектов. Однако в некоторых сценариях невозможно сопоставить легко hello данных устройствами отправки на относительно небольшой устройства в облако сообщений hello, которое принимает центр IoT. Например:

* Большие файлы, содержащие изображения.
* Видеоролики
* Данные вибрации с высокой частотой выборки.
* Некоторые виды предварительно обработанных данных.

Эти файлы обычно являются пакетной обработки в облаке hello, с помощью средств, таких как [фабрики данных Azure](../data-factory/index.md) или hello [Hadoop](../hdinsight/index.md) стека. Если вам требуется tooupland файлы с устройства, по-прежнему можно использовать hello безопасности и надежности центр IoT.

В конце этого учебника в hello выполните две консольные приложения Java:

* **имитируемые устройства**, измененная версия приложения hello, созданного в учебнике hello [сообщений Send облака на устройство с центром IoT]. Это приложение передает файл toostorage, с помощью URI SAS, предоставляемые концентратор IoT.
* **read-file-upload-notification** — приложение, которое получает уведомления о передаче файлов от Центра Интернета вещей.

> [!NOTE]
> Существуют пакеты SDK для устройств Центра Интернета вещей Azure, обеспечивающие поддержку многих платформ устройств и языков (включая C, .NET и JavaScript) в Центре Интернета вещей. См. toohello [Центр разработчиков Azure IoT] пошаговые инструкции о том, как tooconnect tooAzure вашего устройства центра IoT.

toocomplete этого учебника требуется hello следующие:

* Здравствуйте, последняя версия [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* Активная учетная запись Azure. Если ее нет, можно создать [бесплатную учетную запись](http://azure.microsoft.com/pricing/free-trial/) всего за несколько минут.

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a>Передача файла из приложения устройства

В этом разделе, измените приложение hello устройства, созданный в [отправки сообщений облака на устройство с центром IoT](iot-hub-java-java-c2d.md) tooupload концентратор tooIoT файла.

1. Скопируйте файл изображения toohello `simulated-device` папку и переименуйте его в `myimage.png`.

1. В текстовом редакторе, откройте hello `simulated-device\src\main\java\com\mycompany\app\App.java` файла.

1. Добавьте объявление переменной toohello hello **приложения** класса:

    ```java
    private static String fileName = "myimage.png";
    ```

1. tooprocess обратного вызова сообщения о состоянии передачи файлов, добавьте следующее hello вложенных классов toohello **приложения** класса:

    ```java
    // Define a callback method tooprint status codes from IoT Hub.
    protected static class FileUploadStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toofile upload for " + fileName
            + " operation with status " + status.name());
      }
    }
    ```

1. tooIoT изображения tooupload концентратора, добавьте следующий метод toohello hello **приложения** tooupload класс образы tooIoT концентратора:

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

1. Изменение hello **основной** hello метод toocall **uploadFile** метода, как показано в следующий фрагмент кода hello:

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

1. Используйте hello следующая команда toobuild hello **имитируемые устройства** приложение и проверьте наличие ошибок:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="receive-a-file-upload-notification"></a>Получение уведомления о передачи файла

В этом разделе вам предстоит создать консольное приложение для Java, которое получает уведомления об отправке файлов из Центра Интернета вещей.

Требуется hello **iothubowner** строка соединения для вашего центра IoT toocomplete в этом разделе. Строка подключения hello можно найти в hello [портал Azure](https://portal.azure.com/) на hello **политики общего доступа** колонку.

1. Создайте проект с именем Maven **чтение файла Отправка уведомления** с помощью hello следующую команду в командной строке. Обратите внимание, что это одна длинная команда.

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-file-upload-notification -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

1. В командной строке перейдите toohello новый `read-file-upload-notification` папки.

1. В текстовом редакторе, откройте hello `pom.xml` файла в hello `read-file-upload-notification` папки и добавьте следующие зависимости toohello hello **зависимости** узла. Добавление зависимости hello позволяет toouse hello **центром IOT java служба клиента** пакета в toocommunicate вашего приложения в службе концентратора IoT:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > Вы можете проверить наличие hello последнюю версию **клиента для службы iot** с помощью [Maven поиска](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).

1. Сохраните и закройте hello `pom.xml` файла.

1. В текстовом редакторе, откройте hello `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` файла.

1. Добавьте следующее hello **импорта** toohello файл инструкций:

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.concurrent.ExecutorService;
    import java.util.concurrent.Executors;
    ```

1. Добавьте следующие переменные уровня класса toohello hello **приложения** класса:

    ```java
    private static final String connectionString = "{Your IoT Hub connection string}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    private static FileUploadNotificationReceiver fileUploadNotificationReceiver = null;
    ```

1. tooprint сведения о консоли toohello передачи файла hello, добавьте следующее hello вложенных классов toohello **приложения** класса:

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

1. toostart hello поток, который осуществляет прослушивание уведомлений передачи файла, добавьте следующий код toohello hello **основной** метод:

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

1. Сохраните и закройте hello `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` файла.

1. Используйте hello следующая команда toobuild hello **чтение файла Отправка уведомления** приложение и проверьте наличие ошибок:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-hello-applications"></a>Запускать приложения hello

Теперь все готово toorun приложения hello.

В командной строке в hello `read-file-upload-notification` папки, запустите hello следующую команду:

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

В командной строке в hello `simulated-device` папки, запустите hello следующую команду:

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

Hello следующем снимке экрана показан вывод hello hello **имитируемые устройства** приложения:

![Выходные данные приложения simulated-device](media/iot-hub-java-java-upload/simulated-device.png)

Hello следующем снимке экрана показан вывод hello hello **чтение файла Отправка уведомления** приложения:

![Выходные данные приложения read-file-upload-notification](media/iot-hub-java-java-upload/read-file-upload-notification.png)

Можно использовать файл загружен hello портала tooview hello в контейнере хранилища hello, настроенному:

![Отправленный файл](media/iot-hub-java-java-upload/uploaded-file.png)

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


