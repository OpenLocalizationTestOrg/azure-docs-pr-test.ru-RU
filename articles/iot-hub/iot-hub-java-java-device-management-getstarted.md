---
title: "aaaGet работы с управлением устройства Azure IoT Hub (Java) | Документы Microsoft"
description: "Как tooinitiate управления устройства Azure IoT Hub toouse перезагрузите удаленного устройства. Использовать устройства Azure IoT hello пакета SDK для Java tooimplement приложение имитированное устройство, которое включает прямой метод и hello Azure IoT служба пакета SDK для Java tooimplement приложение службы, которое вызывает метод прямой hello."
services: iot-hub
documentationcenter: .java
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 7aaeda9d4ff7002e5c66adfd61e2dfd5bcea964f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-management-java"></a>Начало работы с управлением устройствами (Java)

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

В этом учебнике описаны следующие процедуры.

* Используйте hello Azure портала toocreate центр IoT и создать удостоверение устройства в концентратор IoT.
* Создание приложения имитированное устройство, которое реализует устройства прямой метод tooreboot hello. Прямой методы вызываются из облака hello.
* Создайте приложение, которое вызывает метод прямой перезагрузки hello в приложение hello имитированное устройство через концентратор IoT. Это приложение, а затем мониторы hello выводятся свойства из toosee hello устройств после завершения операции перезагрузки hello.

В конце этого учебника hello у вас есть два консольные приложения Java:

**simulated-device**. Это приложение:

* Центр IoT tooyour подключается с идентификатором hello устройства, созданный ранее.
* получает вызов прямого метода перезагрузки;
* имитирует физическую перезагрузку;
* Отчеты hello время последней перезагрузки hello через свойство отчета.

**trigger-reboot**. Это приложение:

* Вызывает метод с прямой приложение hello имитированное устройство.
* Отображает hello ответа toohello непосредственный вызов методов отправленных hello имитированное устройство
* Отображает hello обновлены сообщил свойства.

> [!NOTE]
> Сведения о hello пакетов SDK, которые можно использовать toorun toobuild приложений на устройствах и серверной части вашего решения см. в разделе [пакеты SDK Azure IoT][lnk-hub-sdks].

toocomplete этого учебника, необходимо:

* Java SE 8. <br/> [Подготовка среды разработки] [ lnk-dev-setup] описывает способ tooinstall Java для этого учебника в Windows или Linux.
* Maven 3.  <br/> [Подготовка среды разработки] [ lnk-dev-setup] описывает способ tooinstall [Maven] [ lnk-maven] для этого учебника в Windows или Linux.
* [Node.js версии 0.10.0 или более поздней](http://nodejs.org).

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a>Триггер удаленной перезагрузки на устройстве hello, с помощью прямой метод

В этом разделе приведена процедура создания консольного приложения Java, которое выполняет следующие действия:

1. Вызывает метод прямой перезагрузки hello в приложение hello имитированное устройство.
1. Отображает hello ответа.
1. Опрашивает hello сообщила, отправленных из устройства toodetermine hello после завершения перезагрузки hello свойств.

Это консольное приложение подключается tooyour центр IoT прямой метод tooinvoke hello и чтения hello сообщил свойства.

1. Создайте пустую папку с именем dm-get-started.

1. В папке dm get started hello создайте Maven проект с именем **триггер перезагрузки** с помощью hello следующую команду в командной строке. Hello ниже показан один, long команды:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=trigger-reboot -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. В командной строке перейдите папку toohello перезагрузки триггера.

1. В текстовом редакторе, откройте файл pom.xml hello в папке триггер перезагрузки hello и добавьте следующие зависимости toohello hello **зависимости** узла. Эта зависимость позволяет вам toouse hello клиента для службы iot пакета в toocommunicate вашего приложения с вашего центра IoT:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > Вы можете проверить наличие hello последнюю версию **клиента для службы iot** с помощью [поиска Maven][lnk-maven-service-search].

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

1. Сохраните и закройте файл pom.xml hello.

1. В текстовом редакторе откройте файл источника trigger-reboot\src\main\java\com\mycompany\app\App.java hello.

1. Добавьте следующее hello **импорта** toohello файл инструкций:

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceMethod;
    import com.microsoft.azure.sdk.iot.service.devicetwin.MethodResult;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceTwin;
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceTwinDevice;

    import java.io.IOException;
    import java.util.concurrent.TimeUnit;
    import java.util.concurrent.Executors;
    import java.util.concurrent.ExecutorService;
    ```

1. Добавьте следующие переменные уровня класса toohello hello **приложения** класса. Замените `{youriothubconnectionstring}` с IoT строку подключения к концентратору нижеприведенного hello *создать центр IoT* раздела:

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    private static final String methodName = "reboot";
    private static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    private static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    ```

1. tooimplement поток, который считывает hello сообщил свойства из устройства двойных hello каждые 10 секунд, добавьте следующее hello вложенных классов toohello **приложения** класса:

    ```java
    private static class ShowReportedProperties implements Runnable {
      public void run() {
        try {
          DeviceTwin deviceTwins = DeviceTwin.createFromConnectionString(iotHubConnectionString);
          DeviceTwinDevice twinDevice = new DeviceTwinDevice(deviceId);
          while (true) {
            System.out.println("Get reported properties from device twin");
            deviceTwins.getTwin(twinDevice);
            System.out.println(twinDevice.reportedPropertiesToString());
            Thread.sleep(10000);
          }
        } catch (Exception ex) {
          System.out.println("Exception reading reported properties: " + ex.getMessage());
        }
      }
    }
    ```

1. прямой метод tooinvoke hello перезагрузки на устройстве имитацию hello, добавить следующие toohello кода hello **основной** метод:

    ```java
    System.out.println("Starting sample...");
    DeviceMethod methodClient = DeviceMethod.createFromConnectionString(iotHubConnectionString);

    try
    {
      System.out.println("Invoke reboot direct method");
      MethodResult result = methodClient.invoke(deviceId, methodName, responseTimeout, connectTimeout, null);

      if(result == null)
      {
        throw new IOException("Invoke direct method reboot returns null");
      }
      System.out.println("Invoked reboot on device");
      System.out.println("Status for device:   " + result.getStatus());
      System.out.println("Message from device: " + result.getPayload());
    }
    catch (IotHubException e)
    {
        System.out.println(e.getMessage());
    }
    ```

1. поток toopoll toostart hello Здравствуйте выводятся свойства из hello имитированное устройство, добавьте следующий код toohello hello **основной** метод:

    ```java
    ShowReportedProperties showReportedProperties = new ShowReportedProperties();
    ExecutorService executor = Executors.newFixedThreadPool(1);
    executor.execute(showReportedProperties);
    ```

1. tooenable вы toostop приложение hello, добавьте следующий код toohello hello **основной** метод:

    ```java
    System.out.println("Press ENTER tooexit.");
    System.in.read();
    executor.shutdownNow();
    System.out.println("Shutting down sample...");
    ```

1. Сохраните и закройте файл trigger-reboot\src\main\java\com\mycompany\app\App.java hello.

1. Построение hello **триггер перезагрузки** серверной части приложения и исправьте все ошибки. В командной строке перейдите папку триггер перезагрузки toohello и выполнения hello следующую команду:

    `mvn clean package -DskipTests`

## <a name="create-a-simulated-device-app"></a>Создание приложения виртуального устройства

В этом разделе приведена процедура создания консольного приложения Java, которое имитирует устройство. приложение Hello прослушивает hello перезагрузки непосредственный вызов методов из вашего центра IoT и немедленно отвечает, toothat вызова. Здравствуйте, приложения, а затем бездействует в течение некоторого времени процесса перезагрузки toosimulate hello до начала использования типа hello toonotify выводятся свойства **триггер перезагрузки** серверной части приложения, которое hello перезагрузка завершена.

1. В папке dm get started hello создайте Maven проект с именем **имитируемые устройства** с помощью hello следующую команду в командной строке. Hello ниже приведен один, long команды.

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. В командной строке перейдите папку toohello имитируемые устройства.

1. В текстовом редакторе, откройте файл pom.xml hello в папке имитируемые устройства hello и добавьте следующие зависимости toohello hello **зависимости** узла. Эта зависимость позволяет вам toouse hello клиента для службы iot пакета в toocommunicate вашего приложения с вашего центра IoT:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > Вы можете проверить наличие hello последнюю версию **клиента для устройства iot** с помощью [поиска Maven][lnk-maven-device-search].

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

1. Сохраните и закройте файл pom.xml hello.

1. В текстовом редакторе откройте файл источника simulated-device\src\main\java\com\mycompany\app\App.java hello.

1. Добавьте следующее hello **импорта** toohello файл инструкций:

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.time.LocalDateTime;
    import java.util.Scanner;
    import java.util.Set;
    import java.util.HashSet;
    ```

1. Добавьте следующие переменные уровня класса toohello hello **приложения** класса. Замените `{yourdeviceconnectionstring}` со строкой подключения устройства hello, записанное в hello *создать удостоверение устройства* раздела:

    ```java
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;

    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String connString = "{yourdeviceconnectionstring}";
    private static DeviceClient client;
    ```

1. tooimplement обратного вызова обработчика для события состояния прямой метод, добавьте следующее hello вложенных классов toohello **приложения** класса:

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded toodevice method operation with status " + status.name());
      }
    }
    ```

1. tooimplement обратного вызова обработчика для события состояния двойных устройство, добавьте следующее hello вложенных классов toohello **приложения** класса:

    ```java
    protected static class DeviceTwinStatusCallback implements IotHubEventCallback
    {
        public void execute(IotHubStatusCode status, Object context)
        {
            System.out.println("IoT Hub responded toodevice twin operation with status " + status.name());
        }
    }
    ```

1. tooimplement обработчик обратного вызова для событий свойства, добавьте следующее hello вложенных классов toohello **приложения** класса:

    ```java
    protected static class PropertyCallback implements PropertyCallBack<String, String>
    {
      public void PropertyCall(String propertyKey, String propertyValue, Object context)
      {
        System.out.println("PropertyKey:     " + propertyKey);
        System.out.println("PropertyKvalue:  " + propertyKey);
      }
    }
    ```

1. tooimplement поток toosimulate hello перезагрузка устройства, добавьте следующее hello вложенных классов toohello **приложения** класса. Hello поток бездействует в течение 5 секунд, а затем задает hello **lastReboot** сообщил свойство:

    ```java
    protected static class RebootDeviceThread implements Runnable {
      public void run() {
        try {
          System.out.println("Rebooting...");
          Thread.sleep(5000);
          Property property = new Property("lastReboot", LocalDateTime.now());
          Set<Property> properties = new HashSet<Property>();
          properties.add(property);
          client.sendReportedProperties(properties);
          System.out.println("Rebooted");
        }
        catch (Exception ex) {
          System.out.println("Exception in reboot thread: " + ex.getMessage());
        }
      }
    }
    ```

1. прямой метод tooimplement hello на устройстве hello, добавьте следующее hello вложенных классов toohello **приложения** класса. Когда имитацию приложение hello получает toohello вызов **перезагрузить** прямой метод возвращает вызывающий объект подтверждения toohello и запускает поток tooprocess hello перезагрузите:

    ```java
    protected static class DirectMethodCallback implements com.microsoft.azure.sdk.iot.device.DeviceTwin.DeviceMethodCallback
    {
      @Override
      public DeviceMethodData call(String methodName, Object methodData, Object context)
      {
        DeviceMethodData deviceMethodData;
        switch (methodName)
        {
          case "reboot" :
          {
            int status = METHOD_SUCCESS;
            System.out.println("Received reboot request");
            deviceMethodData = new DeviceMethodData(status, "Started reboot");
            RebootDeviceThread rebootThread = new RebootDeviceThread();
            Thread t = new Thread(rebootThread);
            t.start();
            break;
          }
          default:
          {
            int status = METHOD_NOT_DEFINED;
            deviceMethodData = new DeviceMethodData(status, "Not defined direct method " + methodName);
          }
        }
        return deviceMethodData;
      }
    }
    ```

1. Измените сигнатуру hello объекта hello **основной** метод toothrow hello следующие исключения:

    ```java
    public static void main(String[] args) throws IOException, URISyntaxException
    ```

1. tooinstantiate **DeviceClient**, добавьте следующий код toohello hello **основной** метод:

    ```java
    System.out.println("Starting device client sample...");
    client = new DeviceClient(connString, protocol);
    ```

1. toostart прослушивание прямых вызовов, добавьте следующий код toohello hello **основной** метод:

    ```java
    try
    {
      client.open();
      client.subscribeToDeviceMethod(new DirectMethodCallback(), null, new DirectMethodStatusCallback(), null);
      client.startDeviceTwin(new DeviceTwinStatusCallback(), null, new PropertyCallback(), null);
      System.out.println("Subscribed toodirect methods and polling for reported properties. Waiting...");
    }
    catch (Exception e)
    {
      System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" +  e.getMessage());
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. tooshut работу имитатора устройства hello, добавьте следующий код toohello hello **основной** метод:

    ```java
    System.out.println("Press any key tooexit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    scanner.close();
    client.close();
    System.out.println("Shutting down...");
    ```

1. Сохраните и закройте файл simulated-device\src\main\java\com\mycompany\app\App.java hello.

1. Построение hello **имитируемые устройства** серверной части приложения и исправьте все ошибки. В командной строке перейдите папка имитируемые устройства toohello и выполнения hello следующую команду:

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a>Запускайте приложения hello

Теперь вы находитесь toorun готовности приложения hello.

1. В командной строке в папке имитируемые устройства hello выполните следующие команды toobegin Ожидание перезагрузки вызовы методов из вашего центра IoT hello:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Центр IoT Java имитируемые устройства toolisten приложения для прямых вызовов перезагрузки][1]

1. В командной строке в папке hello перезагрузки триггер выполните следующую метод перезагрузки hello toocall команды на устройстве имитацию из вашего центра IoT hello:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Центр IoT Java службы приложения toocall hello перезагрузить прямой метод][2]

1. имитированное устройство Hello в ответ отправляет toohello перезагрузки непосредственный вызов методов:

    ![Приложение для имитации устройства центра IoT Java отвечает toohello непосредственный вызов методов][3]

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[1]: ./media/iot-hub-java-java-device-management-getstarted/launchsimulator.png
[2]: ./media/iot-hub-java-java-device-management-getstarted/triggerreboot.png
[3]: ./media/iot-hub-java-java-device-management-getstarted/respondtoreboot.png
<!-- Links -->

[lnk-maven]: https://maven.apache.org/what-is-maven.html

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java/blob/master/doc/java-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md

[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-device-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22