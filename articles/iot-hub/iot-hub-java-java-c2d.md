---
title: "сообщения aaaCloud на устройство с центром IoT Azure (Java) | Документы Microsoft"
description: "Способ toosend облака на устройство сообщений tooa устройств из центра Azure IoT с помощью hello Azure IoT, пакеты SDK для Java. Изменение сообщений облака на устройство имитированное устройство tooreceive приложения и изменения сообщений облака на устройство hello toosend серверной части приложения."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 7f785ea8-e7c2-40c5-87ef-96525e9b9e1e
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: dobett
ms.openlocfilehash: 8721f18428c849ed9a04aa2e45c65605c3e38101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-to-device-messages-with-iot-hub-java"></a>Отправка сообщений из облака на устройство с помощью Центра Интернета вещей (Java)
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

Центр Интернета вещей Azure — это полностью управляемая служба, которая обеспечивает надежный и защищенный двунаправленный обмен данными между миллионами устройств и серверной частью решения. Hello [приступить к работе с центром IoT] учебнике показано, как подготовить удостоверение устройства в нем toocreate центр IoT и кода приложения имитацию устройств, которое отправляет сообщения из устройства в облако.

Это руководство является логическим продолжением статьи [приступить к работе с центром IoT]. В нем показано следующее:

* Из серверной части вашего решения отправьте сообщения облака на устройство tooa одно устройство через Центр IoT.
* Получение на устройстве сообщений, передаваемых из облака на устройство.
* Из вашего решения внутренний запрос подтверждения доставки (*отзывы*) для сообщений отправленных tooa устройств из центра IoT.

Дополнительные сведения о сообщениях облака на устройство можно найти в hello [руководстве для разработчиков центра IoT][IoT Hub developer guide - C2D].

В конце этого учебника hello выполните два консольные приложения Java:

* **имитируемые устройства**, измененную версию приложения hello, созданного в [приступить к работе с центром IoT], который подключается tooyour центр IoT и получает сообщения облака на устройство.
* **отправлять c2d сообщения**, который отправляет приложения имитированное устройство toohello сообщение облака на устройство с помощью центра IoT, а затем получает подтверждение его доставки.

> [!NOTE]
> Для центра IoT существуют пакеты SDK для многих платформ устройств и языков (включая C, Java и Javascript). Эти пакеты работают на основе пакетов SDK для устройств Azure IoT. Пошаговые инструкции по tooconnect кода учебник toothis устройства и обычно tooAzure центр IoT. в статье hello [Центр разработчиков Azure IoT].

toocomplete этого учебника требуется hello следующие:

* Полные рабочую версию hello [приступить к работе с центром IoT](iot-hub-java-java-getstarted.md) или [сообщения из устройства в облако центра IoT процесс](iot-hub-java-java-process-d2c.md) учебника.
* Здравствуйте, последняя версия [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* Активная учетная запись Azure. Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.

## <a name="receive-messages-in-hello-simulated-device-app"></a>Получать сообщения в приложение hello имитированное устройство

В этом разделе, измените приложение hello имитированное устройство, вы создали в [приступить к работе с центром IoT] tooreceive сообщений облака на устройство из центра IoT hello.

1. В текстовом редакторе откройте файл simulated-device\src\main\java\com\mycompany\app\App.java hello.

2. Добавьте следующее hello **MessageCallback** класс как класс является вложенным в hello **приложения** класса. Hello **выполнение** метод вызывается, когда устройство hello получает сообщение из центра IoT. В этом примере hello устройства всегда уведомляет центра IoT hello о завершении приветственное сообщение:

    ```java
    private static class AppMessageCallback implements MessageCallback {
      public IotHubMessageResult execute(Message msg, Object context) {
        System.out.println("Received message from hub: "
          + new String(msg.getBytes(), Message.DEFAULT_IOTHUB_MESSAGE_CHARSET));
    
        return IotHubMessageResult.COMPLETE;
      }
    }
    ```
3. Изменение hello **основной** toocreate метод **AppMessageCallback** экземпляра и вызова hello **setMessageCallback** метод перед открытием hello клиента следующим образом:

    ```java
    client = new DeviceClient(connString, protocol);
   
    MessageCallback callback = new AppMessageCallback();
    client.setMessageCallback(callback, null);
    client.open();
    ```

    > [!NOTE]
    > При использовании HTTP вместо MQTT или AMQP транспорта hello hello **DeviceClient** экземпляра проверяет наличие сообщений от редко центр IoT (меньше, чем каждые 25 минут). Дополнительные сведения об отличиях hello поддержки MQTT, AMQP и HTTP и центр IoT регулирования см. в разделе hello [руководстве для разработчиков центра IoT][IoT Hub developer guide - C2D].

4. toobuild hello **имитируемые устройства** приложения с помощью Maven, выполните следующую команду в командной строке hello в папке имитируемые устройства hello hello:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="send-a-cloud-to-device-message"></a>Отправка сообщения из облака на устройство

В этом разделе создайте консольное приложение Java, которое отправляет сообщения облака на устройство toohello имитированное устройство приложения. Требуется hello идентификатор устройства устройства hello, добавленного в hello [приступить к работе с центром IoT] учебника. Строка подключения концентратора IoT требуется hello для концентратору, который можно найти в hello [портал Azure].

1. Создайте проект с именем Maven **сообщений send-c2d** с помощью hello следующую команду в командной строке. Обратите внимание, что это одна длинная команда.

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=send-c2d-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. В командной строке перейдите toohello новую папку отправлять c2d-сообщения.

3. В текстовом редакторе, откройте файл pom.xml hello в папке отправки c2d – сообщений hello и добавьте следующие зависимости toohello hello **зависимости** узла. Добавление зависимости hello позволяет toouse hello **центром IOT java служба клиента** пакета в toocommunicate вашего приложения в службе концентратора IoT:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > Вы можете проверить наличие hello последнюю версию **клиента для службы iot** с помощью [поиска Maven][lnk-maven-service-search].

4. Сохраните и закройте файл pom.xml hello.

5. В текстовом редакторе откройте файл send-c2d-messages\src\main\java\com\mycompany\app\App.java hello.

6. Добавьте следующее hello **импорта** toohello файл инструкций:

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. Добавьте следующие переменные уровня класса toohello hello **приложения** класса, заменив **{yourhubconnectionstring}** и **{yourdeviceid}** с hello значения на указанное выше:

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "{yourdeviceid}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    ```

8. Замените hello **основной** метод после кода hello. Этот код подключается центра IoT tooyour, отправляет сообщения tooyour устройство и ждет подтверждения, приветственное сообщение hello полученных и обработанных устройств:
   
    ```java
    public static void main(String[] args) throws IOException,
        URISyntaxException, Exception {
      ServiceClient serviceClient = ServiceClient.createFromConnectionString(
        connectionString, protocol);
   
      if (serviceClient != null) {
        serviceClient.open();
        FeedbackReceiver feedbackReceiver = serviceClient
          .getFeedbackReceiver();
        if (feedbackReceiver != null) feedbackReceiver.open();
   
        Message messageToSend = new Message("Cloud toodevice message.");
        messageToSend.setDeliveryAcknowledgement(DeliveryAcknowledgement.Full);
   
        serviceClient.send(deviceId, messageToSend);
        System.out.println("Message sent toodevice");
   
        FeedbackBatch feedbackBatch = feedbackReceiver.receive(10000);
        if (feedbackBatch != null) {
          System.out.println("Message feedback received, feedback time: "
            + feedbackBatch.getEnqueuedTimeUtc().toString());
        }
   
        if (feedbackReceiver != null) feedbackReceiver.close();
        serviceClient.close();
      }
    }
    ```

    > [!NOTE]
    > Для упрощения в этом учебнике не реализуются какие-либо политики повтора. В рабочем коде следует реализовать политики повтора (например, экспоненциального отката), описанным в статье MSDN hello [обработка временных сбоев].


9. toobuild hello **имитируемые устройства** приложения с помощью Maven, выполните следующую команду в командной строке hello в папке имитируемые устройства hello hello:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-hello-applications"></a>Запускать приложения hello

Теперь вы находитесь toorun готовности приложения hello.

1. В командной строке в папке hello имитируемые устройства выполните hello после отправки центр IoT tooyour телеметрии и toolisten для облака на устройство сообщений, отправляемых из концентратор toobegin команды:

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![Запустить имитированное устройство приложение hello][img-simulated-device]

2. В командной строке в папке сообщений send-c2d hello выполните hello, следующая команда toosend сообщение облака на устройство и ожидания подтверждения обратной связи.

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![Запустите приветственное сообщение hello команда toosend облака на устройство][img-send-command]

## <a name="next-steps"></a>Дальнейшие действия

В этом учебнике вы узнали, как toosend и получать сообщения облака на устройство. 

см. Примеры toosee полное и всестороннее решений, использующих центр IoT [Azure IoT Suite].

toolearn Дополнительные сведения о разработке решений с центром IoT разделе hello [руководстве для разработчиков центра IoT].

<!-- Images -->
[img-simulated-device]: media/iot-hub-java-java-c2d/receivec2d.png
[img-send-command]:  media/iot-hub-java-java-c2d/sendc2d.png
<!-- Links -->

[приступить к работе с центром IoT]: iot-hub-java-java-getstarted.md
[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md
[руководстве для разработчиков центра IoT]: iot-hub-devguide.md
[Центр разработчиков Azure IoT]: http://www.azure.com/develop/iot
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java
[обработка временных сбоев]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[портал Azure]: https://portal.azure.com
[Azure IoT Suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22