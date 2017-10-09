---
title: "aaaGet работы с Azure IoT Hub (Java) | Документы Microsoft"
description: "Узнайте, как toosend устройства в облако сообщений tooAzure центр IoT с помощью IoT пакеты SDK для Java. Создать имитированное устройство и службы приложений tooregister устройства, отправлять сообщения и чтения сообщений из центра IoT."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 70dae4a8-0e98-4c53-b5a5-9d6963abb245
ms.service: iot-hub
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac954f0522b46ed2a5b4a819bc611c13be0b9a9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-tooyour-iot-hub-using-java"></a>Подключиться с помощью Java концентратор IoT tooyour устройства
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

В конце этого учебника hello у вас есть три консольные приложения Java:

* **Создание устройства идентификаторов**, которая создает удостоверения устройства и связана защита ключа tooconnect приложение устройства.
* **чтение d2c сообщений**, которая отображает hello телеметрии, отправленные приложение устройства.
* **имитируемые устройства**, который подключается центра IoT tooyour с идентификатором hello устройства, созданный ранее и будет отправлять данные телеметрии каждый второй с помощью протокола MQTT "hello".

> [!NOTE]
> статья Hello [пакеты SDK Azure IoT] [ lnk-hub-sdks] предоставляет сведения о hello Azure IoT пакетов SDK, которые можно использовать toobuild toorun обоих приложений на устройствах и серверной части вашего решения.

toocomplete этого учебника требуется hello следующие:

* Здравствуйте, последняя версия [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) 
* [Maven 3](https://maven.apache.org/install.html) 
* Активная учетная запись Azure. Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

В качестве последнего шага, запишите hello **первичного ключа** значение. Нажмите кнопку **конечные точки** и hello **события** встроенные конечной точки. На hello **свойства** колонке запомните hello **концентратора событий-совместимое имя** и hello **конечной точки концентратора событий в совместимом** адрес. Эти три значения понадобятся при создании приложения **read-d2c-messages**.

![Колонка "Сообщения" Центра Интернета вещей на портале Azure][6]

Теперь Центр Интернета вещей создан. У вас есть hello центра IoT имя узла, центр IoT строку подключения, IoT Hub первичный ключ, имя совместимое концентратора событий и концентратора событий-совместимой конечной точки необходимо toocomplete этого учебника.

## <a name="create-a-device-identity"></a>Создание удостоверения устройства
В этом разделе создайте консольное приложение Java, которое создает удостоверение устройства в реестре hello identity в вашего центра IoT. Устройство не удается подключиться tooIoT концентратора, если оно не имеет запись в реестре удостоверений hello. Дополнительные сведения см. в разделе hello **реестра удостоверений** раздел hello [руководстве для разработчиков центра IoT][lnk-devguide-identity]. При запуске это консольное приложение, он создает уникальный идентификатор устройства и ключ, что при отправке устройства в облако, устройство может использовать tooidentify самого сообщения tooIoT концентратора.

1. Создайте пустую папку с именем iot-java-get-started. В папке iot-java-get-started hello создайте Maven проект с именем **создать устройство идентификаторов** с помощью hello следующую команду в командной строке. Обратите внимание, что это одна длинная команда.

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=create-device-identity -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. В командной строке перейдите папку toohello создать устройство идентификаторов.

3. В текстовом редакторе, откройте файл pom.xml hello в папке создайте устройств удостоверений hello и добавьте следующие зависимости toohello hello **зависимости** узла. Эта зависимость позволяет вам toouse hello клиента для службы iot пакета в приложении:

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

5. В текстовом редакторе откройте файл create-device-identity\src\main\java\com\mycompany\app\App.java hello.

6. Добавьте следующее hello **импорта** toohello файл инструкций:

    ```java
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;
    import com.microsoft.azure.sdk.iot.service.Device;
    import com.microsoft.azure.sdk.iot.service.RegistryManager;
   
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. Добавьте следующие переменные уровня класса toohello hello **приложения** класса, заменив **{yourhubconnectionstring}** с hello значение на указанное выше:

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "myFirstJavaDevice";
    ```
[!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

8. Измените сигнатуру hello объекта hello **основной** tooinclude метод hello исключения следующим образом:

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException, Exception
    ```

9. Добавьте следующий код как текст hello hello hello **основной** метод. Этот код создает устройство с именем *javadevice* в реестре удостоверений Центра Интернета вещей, если оно еще не создано. Затем отображается идентификатор устройства hello и ключ, которые понадобятся позднее:

    ```java
    RegistryManager registryManager = RegistryManager.createFromConnectionString(connectionString);
RegistryManager registryManager = RegistryManager.createFromConnectionString(connectionString);

    // Create a device that's enabled by default, 
    // with an autogenerated key.
    Device device = Device.createFromId(deviceId, null, null);
    try {
      device = registryManager.addDevice(device);
    } catch (IotHubException iote) {
      // If hello device already exists.
      try {
        device = registryManager.getDevice(deviceId);
      } catch (IotHubException iotf) {
        iotf.printStackTrace();
      }
    }

    // Display information about the
    // device you created.
    System.out.println("Device Id: " + device.getDeviceId());
    System.out.println("Device key: " + device.getPrimaryKey());
    // Create a device that's enabled by default, 
    // with an autogenerated key.
    Device device = Device.createFromId(deviceId, null, null);
    try {
      device = registryManager.addDevice(device);
    } catch (IotHubException iote) {
      // If hello device already exists.
      try {
        device = registryManager.getDevice(deviceId);
      } catch (IotHubException iotf) {
        iotf.printStackTrace();
      }
    }

    // Display information about the
    // device you created.
    System.out.println("Device Id: " + device.getDeviceId());
    System.out.println("Device key: " + device.getPrimaryKey());
    ```

10. Сохраните и закройте файл App.java hello.

11. toobuild hello **создать устройство идентификаторов** приложения с помощью Maven, выполните следующую команду в командной строке hello в папке создайте устройств удостоверений hello hello:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

12. toorun hello **создать устройство идентификаторов** приложения с помощью Maven, выполните следующую команду в командной строке hello в папке создайте устройств удостоверений hello hello:

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

13. Запишите hello **идентификатор устройства** и **ключ устройства**. Эти значения должны позже при создании приложения, которое подключается tooIoT концентратора как устройство.

> [!NOTE]
> Hello реестра удостоверений центра IoT хранится только toohello устройства удостоверения tooenable безопасного доступа центра IoT. Он сохраняет идентификаторы и ключи toouse устройства как учетные данные безопасности и включение или отключение флага, что toodisable доступа можно использовать для отдельных устройств. Если ваше приложение должно toostore другие метаданные для конкретного устройства, его следует использовать хранилище конкретного приложения. Дополнительные сведения см. в разделе hello [руководстве для разработчиков центра IoT][lnk-devguide-identity].

## <a name="receive-device-to-cloud-messages"></a>Получение сообщений с устройства в облако

В этом разделе вы создадите консольное приложение Java, которое считывает сообщения, передаваемые с устройства в облако из Центра Интернета вещей. Центр IoT предоставляет [концентратора событий][lnk-event-hubs-overview]-совместимую конечную точку tooenable вам сообщения tooread устройства в облако. простые действия tookeep, данный учебник создает основные средства чтения, не подходит для развертывания высокой пропускной способностью. Hello [обрабатывать сообщения из устройства в облако] [ lnk-process-d2c-tutorial] учебнике показано, как сообщения tooprocess устройства в облако в масштабе. Hello [Приступая к работе с концентраторами событий] [ lnk-eventhubs-tutorial] учебника содержатся дополнительные сведения о предоставлении tooprocess сообщений из концентраторов событий и определяется применимо toohello конечными точками события концентратора IoT Hub совместимой.

> [!NOTE]
> Hello концентратора событий-совместимой конечной точки для чтения сообщения из устройства в облако, всегда использует протокол AMQP hello.

1. В папке iot-java-get-started hello, созданные в hello *создать удостоверение устройства* статьи, создайте проект с именем Maven **чтение d2c сообщений** hello следующую команду в командной строке с помощью. Обратите внимание, что это одна длинная команда.

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-d2c-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. В командной строке перейдите toohello чтение d2c сообщений папки.

3. В текстовом редакторе, откройте файл pom.xml hello в папке чтения d2c – сообщений hello и добавьте следующие зависимости toohello hello **зависимости** узла. Эта зависимость позволяет пакет клиента eventhubs toouse hello в tooread вашего приложения из конечной точки концентратора событий-совместимой hello:

    ```xml
    <dependency> 
        <groupId>com.microsoft.azure</groupId> 
        <artifactId>azure-eventhubs</artifactId> 
        <version>0.13.0</version> 
    </dependency>
    ```

4. Сохраните и закройте файл pom.xml hello.

5. В текстовом редакторе откройте файл read-d2c-messages\src\main\java\com\mycompany\app\App.java hello.

6. Добавьте следующее hello **импорта** toohello файл инструкций:

    ```java
    import java.io.IOException;
    import com.microsoft.azure.eventhubs.*;
    import com.microsoft.azure.servicebus.*;

    import java.nio.charset.Charset;
    import java.time.*;
    import java.util.function.*;
    ```

7. Добавьте следующие toohello переменной уровня класса hello **приложения** класса. Замените **{youriothubkey}**, **{youreventhubcompatibleendpoint}**, и **{youreventhubcompatiblename}** со значениями hello, записанное ранее:

    ```java
    private static String connStr = "Endpoint={youreventhubcompatibleendpoint};EntityPath={youreventhubcompatiblename};SharedAccessKeyName=iothubowner;SharedAccessKey={youriothubkey}";
    ```

8. Добавьте следующее hello **receiveMessages** toohello метод **приложения** класса. Этот метод создает **EventHubClient** экземпляр конечной точки tooconnect toohello совместимое концентратора событий и асинхронно создает **PartitionReceiver** tooread экземпляр из концентратора событий секции. Он постоянно циклы и выводит сведения о сообщении hello до завершения приложение hello.

    ```java
    // Create a receiver on a partition.
    private static EventHubClient receiveMessages(final String partitionId) {
      EventHubClient client = null;
      try {
        client = EventHubClient.createFromConnectionStringSync(connStr);
      } catch (Exception e) {
        System.out.println("Failed toocreate client: " + e.getMessage());
        System.exit(1);
      }
      try {
        // Create a receiver using the
        // default Event Hubs consumer group
        // that listens for messages from now on.
        client.createReceiver(EventHubClient.DEFAULT_CONSUMER_GROUP_NAME, partitionId, Instant.now())
          .thenAccept(new Consumer<PartitionReceiver>() {
            public void accept(PartitionReceiver receiver) {
              System.out.println("** Created receiver on partition " + partitionId);
              try {
                while (true) {
                  Iterable<EventData> receivedEvents = receiver.receive(100).get();
                  int batchSize = 0;
                  if (receivedEvents != null) {
                    System.out.println("Got some evenst");
                    for (EventData receivedEvent : receivedEvents) {
                      System.out.println(String.format("Offset: %s, SeqNo: %s, EnqueueTime: %s",
                        receivedEvent.getSystemProperties().getOffset(),
                        receivedEvent.getSystemProperties().getSequenceNumber(),
                        receivedEvent.getSystemProperties().getEnqueuedTime()));
                      System.out.println(String.format("| Device ID: %s",
                        receivedEvent.getSystemProperties().get("iothub-connection-device-id")));
                      System.out.println(String.format("| Message Payload: %s",
                        new String(receivedEvent.getBytes(), Charset.defaultCharset())));
                      batchSize++;
                    }
                  }
                  System.out.println(String.format("Partition: %s, ReceivedBatch Size: %s", partitionId, batchSize));
                }
              } catch (Exception e) {
                System.out.println("Failed tooreceive messages: " + e.getMessage());
              }
            }
          });
        } catch (Exception e) {
          System.out.println("Failed toocreate receiver: " + e.getMessage());
      }
      return client;
    }
    ```

   > [!NOTE]
   > Этот метод использует фильтр при создании приемника hello, чтобы hello приемник считывает только сообщения, отправленные tooIoT концентратора после hello получатель начинает выполнение. Этот метод полезен в тестовой среде, чтобы можно было видеть текущий набор сообщений hello. В рабочей среде кода следует убедитесь в том, что обработке всех сообщений hello - Дополнительные сведения см. в разделе hello [как tooprocess сообщения из устройства в облако центра IoT] [ lnk-process-d2c-tutorial] учебника.

9. Измените сигнатуру hello объекта hello **основной** tooinclude метод hello исключения следующим образом:

    ```java
    public static void main( String[] args ) throws IOException
    ```

10. Добавьте следующий код toohello hello **основной** метод в hello **приложения** класса. Этот код создает два hello **EventHubClient** и **PartitionReceiver** экземпляров и включает приложение hello tooclose после завершения обработки сообщений:

    ```java
    // Create receivers for partitions 0 and 1.
    EventHubClient client0 = receiveMessages("0");
    EventHubClient client1 = receiveMessages("1");
    System.out.println("Press ENTER tooexit.");
    System.in.read();
    try {
      client0.closeSync();
      client1.closeSync();
      System.exit(0);
    } catch (ServiceBusException sbe) {
      System.exit(1);
    }
    ```

    > [!NOTE]
    > Данный код предполагает, что вы создали концентратор IoT hello F1 (бесплатно) уровня. Бесплатный Центр Интернета вещей содержит два раздела с именами "0" и "1".

11. Сохраните и закройте файл App.java hello.

12. toobuild hello **чтение d2c сообщений** приложения с помощью Maven, выполните следующую команду в командной строке hello в папке чтения d2c сообщения hello hello:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="create-a-device-app"></a>Создание приложения устройства
В этом разделе создайте консольное приложение Java, которое имитирует устройство, которое отправляет центр IoT tooan сообщения из устройства в облако.

1. В папке iot-java-get-started hello, созданные в hello *создать удостоверение устройства* статьи, создайте проект с именем Maven **имитируемые устройства** hello следующую команду в командной строке с помощью. Обратите внимание, что это одна длинная команда.

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. В командной строке перейдите папку toohello имитируемые устройства.

3. В текстовом редакторе, откройте файл pom.xml hello в папке имитируемые устройства hello и добавьте следующие зависимости toohello hello **зависимости** узла. Эта зависимость позволяет вам toouse hello центром IOT java-пакет клиента по toocommunicate вашего приложения с центр IoT и tooserialize tooJSON объектов Java:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    <dependency>
      <groupId>com.google.code.gson</groupId>
      <artifactId>gson</artifactId>
      <version>2.3.1</version>
    </dependency>
    ```

    > [!NOTE]
    > Вы можете проверить наличие hello последнюю версию **клиента для устройства iot** с помощью [поиска Maven][lnk-maven-device-search].

4. Сохраните и закройте файл pom.xml hello.

5. В текстовом редакторе откройте файл simulated-device\src\main\java\com\mycompany\app\App.java hello.

6. Добавьте следующее hello **импорта** toohello файл инструкций:

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.google.gson.Gson;

    import java.io.*;
    import java.net.URISyntaxException;
    import java.util.Random;
    import java.util.concurrent.Executors;
    import java.util.concurrent.ExecutorService;
    ```

7. Добавьте следующие переменные уровня класса toohello hello **приложения** класса. Замена **{youriothubname}** на название концентратора IoT и **{yourdevicekey}** со значением ключа устройства hello созданный hello *создать удостоверение устройства* раздела:

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myFirstJavaDevice;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myFirstJavaDevice";
    private static DeviceClient client;
    ```
   
    Этот пример приложения использует hello **протокола** переменной, когда он создает **DeviceClient** объекта. Можно использовать либо toocommunicate hello MQTT, AMQP или HTTP-протокол с центром IoT.

8. Добавьте следующее hello вложенные **TelemetryDataPoint** класс внутри hello **приложения** устройство отправляет центр IoT tooyour данные телеметрии hello toospecify класса:

    ```java
    private static class TelemetryDataPoint {
      public String deviceId;
      public double temperature;
      public double humidity;
   
      public String serialize() {
        Gson gson = new Gson();
        return gson.toJson(this);
      }
    }
    ```
9. Добавьте следующее hello вложенные **EventCallback** класс внутри hello **приложения** класс hello toodisplay подтверждения состояния, hello центра IoT возвращает при обработке сообщения из устройства приложение hello. Этот метод также сообщает о hello основного потока в приложение hello после обработки сообщения hello:
   
    ```java
    private static class EventCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toomessage with status: " + status.name());
   
        if (context != null) {
          synchronized (context) {
            context.notify();
          }
        }
      }
    }
    ```

10. Добавьте следующее hello вложенные **MessageSender** класс внутри hello **приложения** класса. Hello **запуска** метода в данном классе создает образец данных телеметрии toosend tooyour IoT hub и ожидает подтверждения перед отправкой hello следующее сообщение:

    ```java
    private static class MessageSender implements Runnable {
      public void run()  {
        try {
          double minTemperature = 20;
          double minHumidity = 60;
          Random rand = new Random();
    
          while (true) {
            double currentTemperature = minTemperature + rand.nextDouble() * 15;
            double currentHumidity = minHumidity + rand.nextDouble() * 20;
            TelemetryDataPoint telemetryDataPoint = new TelemetryDataPoint();
            telemetryDataPoint.deviceId = deviceId;
            telemetryDataPoint.temperature = currentTemperature;
            telemetryDataPoint.humidity = currentHumidity;
    
            String msgStr = telemetryDataPoint.serialize();
            Message msg = new Message(msgStr);
            msg.setProperty("temperatureAlert", (currentTemperature > 30) ? "true" : "false");
            msg.setMessageId(java.util.UUID.randomUUID().toString()); 
            System.out.println("Sending: " + msgStr);
    
            Object lockobj = new Object();
            EventCallback callback = new EventCallback();
            client.sendEventAsync(msg, callback, lockobj);
    
            synchronized (lockobj) {
              lockobj.wait();
            }
            Thread.sleep(1000);
          }
        } catch (InterruptedException e) {
          System.out.println("Finished.");
        }
      }
    }
    ```

    Этот метод отправляет новое сообщение устройства в облако одной секунды после центра IoT hello подтверждает предыдущее сообщение hello. приветственное сообщение содержит объект сериализации JSON с hello deviceId и случайным образом toosimulate номера датчика температуры и влажности датчика.

11. Замените hello **основной** метод с hello, следующий код, создающий концентратор IoT tooyour поток toosend сообщения из устройства в облако:

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException {
      client = new DeviceClient(connString, protocol);
      client.open();
    
      MessageSender sender = new MessageSender();
    
      ExecutorService executor = Executors.newFixedThreadPool(1);
      executor.execute(sender);
    
      System.out.println("Press ENTER tooexit.");
      System.in.read();
      executor.shutdownNow();
      client.closeNow();
    }
    ```

12. Сохраните и закройте файл App.java hello.

13. toobuild hello **имитируемые устройства** приложения с помощью Maven, выполните следующую команду в командной строке hello в папке имитируемые устройства hello hello:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

> [!NOTE]
> простые действия tookeep, этот учебник не реализует никакую политику повтора. В рабочем коде следует реализовать политики повтора (например экспоненциальную отсрочку), описанным в статье MSDN hello [обработка временных сбоев][lnk-transient-faults].

## <a name="run-hello-apps"></a>Запускайте приложения hello

Теперь вы находитесь toorun готовности приложения hello.

1. В командной строке в папке d2c чтения hello выполните следующие команды toobegin мониторинг hello первую секцию в концентратор IoT hello:

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![Центр IoT Java службы приложения toomonitor устройства в облако сообщений][7]

2. В командной строке в папке hello имитируемые устройства выполните hello, следующая команда toobegin отправки центра IoT tooyour данных телеметрии:

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![Сообщения из устройства в облако toosend приложения центра IoT Java устройства][8]

3. Hello **использование** плитки в hello [портал Azure] [ lnk-portal] показано hello число сообщений, отправляемых toohello центр IoT:

    ![Azure портала использование плитки, показывающего количество сообщений, отправляемых tooIoT концентратора][43]

## <a name="next-steps"></a>Дальнейшие действия
В этом учебнике настроен центр IoT в hello портал Azure и затем создать удостоверение устройства в реестре удостоверений центра IoT hello. Вы использовали устройства удостоверения tooenable hello устройства приложения toosend сообщения из устройства в облако toohello центр IoT. Также было создано приложение, которое отображает hello сообщений, полученных центра IoT hello.

Приступая к работе toocontinue центр IoT и tooexplore других сценариев IoT просмотреть:

* [Подключение устройства к Azure IoT][lnk-connect-device]
* [How to get started with device management (Node)][lnk-device-management] (Начало работы с управлением устройствами (Node))
* [Explore Azure IoT Edge architecture on Linux][lnk-iot-edge] (Приступая к работе с архитектурой Azure IoT Edge в Linux)

toolearn tooextend сообщений в масштабе, IoT решение и процесс устройства в облако. в статье hello [обрабатывать сообщения из устройства в облако] [ lnk-process-d2c-tutorial] учебника.
[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

<!-- Images. -->
[6]: ./media/iot-hub-java-java-getstarted/create-iot-hub6.png
[7]: ./media/iot-hub-java-java-getstarted/runapp1.png
[8]: ./media/iot-hub-java-java-getstarted/runapp2.png
[43]: ./media/iot-hub-java-java-getstarted/usage.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-device-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-eventhubs-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22
