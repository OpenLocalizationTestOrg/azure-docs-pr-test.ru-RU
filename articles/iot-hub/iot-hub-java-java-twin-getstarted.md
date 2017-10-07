---
title: "aaaGet к работе с близнецы устройства Azure IoT Hub (Java) | Документы Microsoft"
description: "Как tooadd близнецы устройства Azure IoT Hub toouse теги и затем использовать запрос центр IoT. Использовать устройства Azure IoT hello SDK для Java tooimplement hello устройства и приложения hello служба Azure IoT SDK для Java tooimplement приложение службы, которое добавляет теги hello и запускает hello центра IoT запроса."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/04/2017
ms.author: dobett
ms.openlocfilehash: 25f6fc81471d59c62bcdc3766bb5c33f5733c930
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-java"></a>Начало работы с двойниками устройств (Java)

[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

В этом руководстве создаются два консольных приложения для Java:

* **add-tags-query** — внутреннее приложение Java, которое добавляет теги и выполняет запросы к двойникам устройств.
* **имитируемые устройства**, приложения для устройств Java, подключающуюся tooyour центр IoT и отчеты условия его подключения, с помощью свойства отчета.

> [!NOTE]
> статья Hello [пакеты SDK Azure IoT](iot-hub-devguide-sdks.md) предоставляет сведения о hello Azure IoT пакетов SDK, которые можно использовать toobuild устройства и серверной части приложения.

toocomplete этого учебника, необходимо:

* Здравствуйте, последняя версия [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* Активная учетная запись Azure. Если ее нет, можно создать [бесплатную учетную запись](http://azure.microsoft.com/pricing/free-trial/) всего за несколько минут.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

При желании удостоверения устройства hello toocreate программными средствами чтения hello соответствующий раздел в hello [подключиться с помощью Java концентратор IoT tooyour устройства](iot-hub-java-java-getstarted.md#create-a-device-identity) статьи.

## <a name="create-hello-service-app"></a>Создание приложения hello службы

В этом разделе создается приложение Java, которое добавляет расположение метаданных, что две устройства тег toohello в центр IoT, связанного с **myDeviceId**. приложение Hello сначала запрашивается центр IoT для устройств, расположенных в hello США, а затем для устройств, сообщающие сотовой сети.

1. На компьютере разработки создайте пустую папку с именем `iot-java-twin-getstarted`.

1. В hello `iot-java-twin-getstarted` папки, создайте проект с именем Maven **добавить теги запроса** hello следующую команду в командной строке с помощью. Обратите внимание, что это одна длинная команда.

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=add-tags-query -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. В командной строке перейдите toohello `add-tags-query` папки.

1. В текстовом редакторе, откройте hello `pom.xml` файла в hello `add-tags-query` папки и добавьте следующие зависимости toohello hello **зависимости** узла. Эта зависимость позволяет toouse hello **клиента для службы iot** пакет в toocommunicate вашего приложения с вашего центра IoT:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > Вы можете проверить наличие hello последнюю версию **клиента для службы iot** с помощью [Maven поиска](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).

1. Добавьте следующее hello **построения** узел после hello **зависимости** узла. Эта конфигурация указывает, что приложение hello 1,8 toobuild Java toouse Maven:

    ```xml
    <build>
      <plugins>
        <plugin>
          <groupId>org.apache.maven.plugins</groupId>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.3</version>
          <configuration>
            <source>1.8</source>
            <target>1.8</target>
          </configuration>
        </plugin>
      </plugins>
    </build>
    ```

1. Сохраните и закройте hello `pom.xml` файла.

1. В текстовом редакторе, откройте hello `add-tags-query\src\main\java\com\mycompany\app\App.java` файла.

1. Добавьте следующее hello **импорта** toohello файл инструкций:

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.*;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.HashSet;
    import java.util.Set;
    ```

1. Добавьте следующие переменные уровня класса toohello hello **приложения** класса. Замените `{youriothubconnectionstring}` с IoT строку подключения к концентратору нижеприведенного hello *создать центр IoT* раздела:

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String region = "US";
    public static final String plant = "Redmond43";
    ```

1. Обновление hello **основной** следующие hello tooinclude подпись метода `throws` предложения:

    ```java
    public static void main( String[] args ) throws IOException
    ```

1. Добавьте следующий код toohello hello **основной** hello метод toocreate **DeviceTwin** и **DeviceTwinDevice** объектов. Hello **DeviceTwin** объект обрабатывает hello взаимодействие с вашего центра IoT. Hello **DeviceTwinDevice** представляет hello двойных устройства с тегами и его свойства:

    ```java
    // Get hello DeviceTwin and DeviceTwinDevice objects
    DeviceTwin twinClient = DeviceTwin.createFromConnectionString(iotHubConnectionString);
    DeviceTwinDevice device = new DeviceTwinDevice(deviceId);
    ```

1. Добавьте следующее hello `try/catch` блокировать toohello **основной** метод:

    ```java
    try {
      // Code goes here
    } catch (IotHubException e) {
      System.out.println(e.getMessage());
    } catch (IOException e) {
      System.out.println(e.getMessage());
    }
    ```

1. tooupdate hello **область** и **растение** тегов двойных устройств в двойных вашего устройства, добавьте следующий код в hello hello `try` блока:

    ```java
    // Get hello device twin from IoT Hub
    System.out.println("Device twin before update:");
    twinClient.getTwin(device);
    System.out.println(device);

    // Update device twin tags if they are different
    // from hello existing values
    String currentTags = device.tagsToString();
    if ((!currentTags.contains("region=" + region) && !currentTags.contains("plant=" + plant))) {
      // Create hello tags and attach them toohello DeviceTwinDevice object
      Set<Pair> tags = new HashSet<Pair>();
      tags.add(new Pair("region", region));
      tags.add(new Pair("plant", plant));
      device.setTags(tags);

      // Update hello device twin in IoT Hub
      System.out.println("Updating device twin");
      twinClient.updateTwin(device);
    }

    // Retrieve hello device twin with hello tag values from IoT Hub
    System.out.println("Device twin after update:");
    twinClient.getTwin(device);
    System.out.println(device);
    ```

1. tooquery близнецы устройства hello в центр IoT добавить следующий код toohello hello `try` блок после кода hello, добавленного на предыдущем шаге hello. Hello код выполняется два запроса. Каждый запрос возвращает не более 100 устройств:

    ```java
    // Query hello device twins in IoT Hub
    System.out.println("Devices in Redmond:");

    // Construct hello query
    SqlQuery sqlQuery = SqlQuery.createSqlQuery("*", SqlQuery.FromType.DEVICES, "tags.plant='Redmond43'", null);

    // Run hello query, returning a maximum of 100 devices
    Query twinQuery = twinClient.queryTwin(sqlQuery.getQuery(), 100);
    while (twinClient.hasNextDeviceTwin(twinQuery)) {
      DeviceTwinDevice d = twinClient.getNextDeviceTwin(twinQuery);
      System.out.println(d.getDeviceId());
    }

    System.out.println("Devices in Redmond using a cellular network:");

    // Construct hello query
    sqlQuery = SqlQuery.createSqlQuery("*", SqlQuery.FromType.DEVICES, "tags.plant='Redmond43' AND properties.reported.connectivityType = 'cellular'", null);

    // Run hello query, returning a maximum of 100 devices
    twinQuery = twinClient.queryTwin(sqlQuery.getQuery(), 3);
    while (twinClient.hasNextDeviceTwin(twinQuery)) {
      DeviceTwinDevice d = twinClient.getNextDeviceTwin(twinQuery);
      System.out.println(d.getDeviceId());
    }
    ```

1. Сохраните и закройте hello `add-tags-query\src\main\java\com\mycompany\app\App.java` файла

1. Построение hello **добавить теги запроса** приложения и исправьте все ошибки. В командной строке перейдите toohello `add-tags-query` папки и выполнения hello следующую команду:

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a>Создание приложения устройства

В этом разделе создайте консольное приложение Java, которое задает значение свойства отчета, который отправляется tooIoT концентратора.

1. В hello `iot-java-twin-getstarted` папки, создайте проект с именем Maven **имитируемые устройства** с помощью hello следующую команду в командной строке. Обратите внимание, что это одна длинная команда.

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. В командной строке перейдите toohello `simulated-device` папки.

1. В текстовом редакторе, откройте hello `pom.xml` файла в hello `simulated-device` папки и добавьте следующие зависимости toohello hello **зависимости** узла. Эта зависимость позволяет toouse hello **клиента для устройства iot** пакет в toocommunicate вашего приложения с вашего центра IoT:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > Вы можете проверить наличие hello последнюю версию **клиента для устройства iot** с помощью [Maven поиска](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).

1. Добавьте следующее hello **построения** узел после hello **зависимости** узла. Эта конфигурация указывает, что приложение hello 1,8 toobuild Java toouse Maven:

    ```xml
    <build>
      <plugins>
        <plugin>
          <groupId>org.apache.maven.plugins</groupId>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.3</version>
          <configuration>
            <source>1.8</source>
            <target>1.8</target>
          </configuration>
        </plugin>
      </plugins>
    </build>
    ```

1. Сохраните и закройте hello `pom.xml` файла.

1. В текстовом редакторе, откройте hello `simulated-device\src\main\java\com\mycompany\app\App.java` файла.

1. Добавьте следующее hello **импорта** toohello файл инструкций:

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. Добавьте следующие переменные уровня класса toohello hello **приложения** класса. Замена `{youriothubname}` на название концентратора IoT и `{yourdevicekey}` со значением ключа устройства hello созданный hello *создать удостоверение устройства* раздела:

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myDeviceId";
    ```

    Этот пример приложения использует hello **протокола** переменной, когда он создает **DeviceClient** объекта. В настоящее время toouse двойных функциями устройства необходимо использовать протокол MQTT hello.

1. Добавьте следующий код toohello hello **основной** метода:
    * Создайте toocommunicate клиента устройства с центром IoT.
    * Создание **устройства** toostore hello устройства двойных свойства объекта.

    ```java
    DeviceClient client = new DeviceClient(connString, protocol);

    // Create a Device object toostore hello device twin properties
    Device dataCollector = new Device() {
      // Print details when a property value changes
      @Override
      public void PropertyCall(String propertyKey, Object propertyValue, Object context) {
        System.out.println(propertyKey + " changed too" + propertyValue);
      }
    };
    ```

1. Добавьте следующий код toohello hello **основной** toocreate метод **connectivityType** сообщил свойство и отправлять их tooIoT концентратора:

    ```java
    try {
      // Open hello DeviceClient and start hello device twin services.
      client.open();
      client.startDeviceTwin(new DeviceTwinStatusCallBack(), null, dataCollector, null);

      // Create a reported property and send it tooyour IoT hub.
      dataCollector.setReportedProp(new Property("connectivityType", "cellular"));
      client.sendReportedProperties(dataCollector.getReportedProp());
    }
    catch (Exception e) {
      System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" + e.getMessage());
      dataCollector.clean();
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. Добавить следующий код toohello конец hello hello **основной** метод. Ожидание hello **ввод** ключ позволяет время центр IoT tooreport hello состояния операций двойных hello устройства:

    ```java
    System.out.println("Press any key tooexit...");

    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();

    dataCollector.clean();
    client.close();
    ```

1. Сохраните и закройте hello `simulated-device\src\main\java\com\mycompany\app\App.java` файла.

1. Построение hello **имитируемые устройства** приложения и исправьте все ошибки. В командной строке перейдите toohello `simulated-device` папки и выполнения hello следующую команду:

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a>Запускайте приложения hello

Теперь вы находитесь готов toorun hello консольных приложениях.

1. В командной строке в hello `add-tags-query` папку, следующая команда toorun hello hello **добавить теги запроса** службы приложений:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Центр IoT Java службы приложения tooupdate отметки значений и выполнять запросы устройства](media/iot-hub-java-java-twin-getstarted/service-app-1.png)

    Вы увидите hello **растение** и **область** теги добавлены две toohello устройства. Hello первый запрос возвращает устройства, но hello второй — нет.

1. В командной строке в hello `simulated-device` папку, следующая команда tooadd hello hello **connectivityType** сообщил двойных устройства toohello свойство:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Добавляет клиент устройства Hello hello ** connectivityType ** сообщила, свойство](media/iot-hub-java-java-twin-getstarted/device-app-1.png)

1. В командной строке в hello `add-tags-query` папку, следующая команда toorun hello hello **добавить теги запроса** службы приложения еще раз:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Центр IoT Java службы приложения tooupdate отметки значений и выполнять запросы устройства](media/iot-hub-java-java-twin-getstarted/service-app-2.png)

    Теперь устройство отправил hello **connectivityType** tooIoT свойство концентратора hello второй запрос возвращает устройство.

## <a name="next-steps"></a>Дальнейшие действия

В этом учебнике настроен центр IoT в hello портал Azure и затем создать удостоверение устройства в реестре удостоверений центра IoT hello. Добавить метаданные устройства как теги из серверной части приложения, а написал приложения tooreport устройства подключения сведений об устройстве в двойных hello устройства. Вы также узнали, как tooquery hello двойных сведений об устройстве, с помощью языка запросов SQL-подобного центра IoT hello.

Hello используйте следующие ресурсы toolearn как для:

* Отправка данных телеметрии с устройствами с помощью hello [приступить к работе с центром IoT](iot-hub-java-java-getstarted.md) учебника.
* Управление устройствами интерактивно (такие как включение вентилятор из управляемой пользователем приложения) с hello [использовать прямые методы](iot-hub-java-java-direct-methods.md) учебника.

<!-- Images. -->
[7]: ./media/iot-hub-java-java-twin-getstarted/invoke-method.png
[8]: ./media/iot-hub-java-java-twin-getstarted/device-listen.png
[9]: ./media/iot-hub-java-java-twin-getstarted/device-respond.png

<!-- Links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
