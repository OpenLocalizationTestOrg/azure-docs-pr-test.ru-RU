---
title: "Центр IoT Azure aaaUse прямой методы (Java) | Документы Microsoft"
description: "Как toouse центр IoT Azure направлять методы. Использовать устройства Azure IoT hello пакета SDK для Java tooimplement приложение имитированное устройство, которое включает прямой метод и hello Azure IoT служба пакета SDK для Java tooimplement приложение службы, которое вызывает метод прямой hello."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: b6f2f4a64535ab649a3965cd9c5a19bebaf88eef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-java"></a>Использование прямых методов (Java)

[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

В этом руководстве создаются два консольных приложения для Java:

* **Invoke-direct метод**, Java серверная часть приложения, который вызывает метод в приложение hello имитированное устройство и отображает hello ответа.
* **имитируемые устройства**, приложения Java, которое имитирует устройство соединение центра IoT tooyour с помощью создания удостоверения устройства hello. Это приложение отвечает toohello напрямую вызван из hello серверной части.

> [!NOTE]
> Сведения о hello пакетов SDK, которые можно использовать toorun toobuild приложений на устройствах и серверной части вашего решения см. в разделе [пакеты SDK Azure IoT][lnk-hub-sdks].

toocomplete этого учебника, необходимо:

* Java SE 8. <br/> [Подготовка среды разработки] [ lnk-dev-setup] описывает способ tooinstall Java для этого учебника в Windows или Linux.
* Maven 3.  <br/> [Подготовка среды разработки] [ lnk-dev-setup] описывает способ tooinstall [Maven] [ lnk-maven] для этого учебника в Windows или Linux.
* [Node.js версии 0.10.0 или более поздней](http://nodejs.org).

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>Создание приложения виртуального устройства

В этом разделе создайте консольное приложение Java, которое отвечает tooa методе, вызванном обратно в решение hello end.

1. Создайте пустую папку с именем iot-java-direct-method.

1. В папке iot java непосредственного метода hello, создайте проект Maven с именем **имитируемые устройства** с помощью hello следующую команду в командной строке. Hello следующую команду — один, long команда:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. В командной строке перейдите папку toohello имитируемые устройства.

1. В текстовом редакторе, откройте файл pom.xml hello в папке имитируемые устройства hello и добавьте следующие зависимости toohello hello **зависимости** узла. Эта зависимость позволяет вам toouse hello клиента для устройства iot пакета в toocommunicate вашего приложения с вашего центра IoT:

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

1. В текстовом редакторе откройте файл simulated-device\src\main\java\com\mycompany\app\App.java hello.

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
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    Этот пример приложения использует hello **протокола** переменной, когда он создает **DeviceClient** объекта. В настоящее время toouse направлять методы, которые необходимо использовать протокол MQTT hello.

1. tooreturn центр IoT для tooyour код состояния, добавьте следующее hello вложенных классов toohello **приложения** класса:

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded toodevice method operation with status " + status.name());
      }
    }
    ```

1. toohandle hello прямых вызовов из серверной части решения hello, добавьте следующее hello вложенных классов toohello **приложения** класса:

    ```java
    protected static class DirectMethodCallback implements com.microsoft.azure.sdk.iot.device.DeviceTwin.DeviceMethodCallback
    {
      @Override
      public DeviceMethodData call(String methodName, Object methodData, Object context)
      {
        DeviceMethodData deviceMethodData;
        switch (methodName)
        {
          case "writeLine" :
          {
            int status = METHOD_SUCCESS;
            System.out.println(new String((byte[])methodData));
            deviceMethodData = new DeviceMethodData(status, "Executed direct method " + methodName);
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

1. toocreate **DeviceClient** и прослушивать прямых вызовов, добавьте **основной** toohello метод **приложения** класса:

    ```java
    public static void main(String[] args)
      throws IOException, URISyntaxException
    {
      System.out.println("Starting device sample...");

      DeviceClient client = new DeviceClient(connString, protocol);

      try
      {
        client.open();
        client.subscribeToDeviceMethod(new DirectMethodCallback(), null, new DirectMethodStatusCallback(), null);
        System.out.println("Subscribed toodirect methods. Waiting...");
      }
      catch (Exception e)
      {
        System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" +  e.getMessage());
        client.close();
        System.out.println("Shutting down...");
      }

      System.out.println("Press any key tooexit...");
      Scanner scanner = new Scanner(System.in);
      scanner.nextLine();
      scanner.close();
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. Сохраните и закройте файл simulated-device\src\main\java\com\mycompany\app\App.java hello

1. Построение hello **имитируемые устройства** приложения и исправьте все ошибки. В командной строке перейдите папка имитируемые устройства toohello и выполнения hello следующую команду:

    `mvn clean package -DskipTests`

## <a name="call-a-direct-method-on-a-device"></a>Вызов прямого метода на устройстве

В этом разделе создайте консольное приложение Java, которое вызывает прямой метод, а затем отображает hello ответа. Это консольное приложение подключается tooyour прямой метод центра IoT tooinvoke hello.

1. В папке iot java непосредственного метода hello, создайте проект Maven с именем **вызвать direct метод** с помощью hello следующую команду в командной строке. Hello следующую команду — один, long команда:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=invoke-direct-method -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. В командной строке перейдите toohello invoke-direct метод папки.

1. В текстовом редакторе, откройте файл pom.xml hello в папке hello вызвать direct метод и добавьте следующие зависимости toohello hello **зависимости** узла. Эта зависимость позволяет вам toouse hello клиента для службы iot пакета в toocommunicate вашего приложения с вашего центра IoT:

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

1. В текстовом редакторе откройте файл invoke-direct-method\src\main\java\com\mycompany\app\App.java hello.

1. Добавьте следующее hello **импорта** toohello файл инструкций:

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceMethod;
    import com.microsoft.azure.sdk.iot.service.devicetwin.MethodResult;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.concurrent.TimeUnit;
    ```

1. Добавьте следующие переменные уровня класса toohello hello **приложения** класса. Замените `{youriothubconnectionstring}` с IoT строку подключения к концентратору нижеприведенного hello *создать центр IoT* раздела:

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String methodName = "writeLine";
    public static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    public static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    public static final String payload = "a line toobe written";
    ```

1. метод hello tooinvoke на hello имитированное устройство, добавьте следующие toohello кода hello **основной** метод:

    ```java
    System.out.println("Starting sample...");
    DeviceMethod methodClient = DeviceMethod.createFromConnectionString(iotHubConnectionString);

    try
    {
        System.out.println("Invoke direct method");
        MethodResult result = methodClient.invoke(deviceId, methodName, responseTimeout, connectTimeout, payload);

        if(result == null)
        {
            throw new IOException("Direct method invoke returns null");
        }
        System.out.println("Status=" + result.getStatus());
        System.out.println("Payload=" + result.getPayload());
    }
    catch (IotHubException e)
    {
        System.out.println(e.getMessage());
    }

    System.out.println("Shutting down sample...");
    ```

1. Сохраните и закройте файл invoke-direct-method\src\main\java\com\mycompany\app\App.java hello

1. Построение hello **вызвать direct метод** приложения и исправьте все ошибки. В командной строке перейдите папку toohello вызвать direct метод и выполнения hello следующую команду:

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a>Запускайте приложения hello

Теперь вы находитесь готов toorun hello консольных приложениях.

1. В командной строке в папке имитируемые устройства hello выполните следующие команды toobegin прослушивание вызовы методов из вашего центра IoT hello:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Центр IoT Java имитируемые устройства toolisten приложения для прямых вызовов][8]

1. В командной строке в папке вызвать direct метод hello запуск hello, следующая команда toocall метода для имитации устройства из вашего центра IoT:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Центр IoT Java службы приложения toocall прямой метод][7]

1. имитированное устройство Hello в ответ отправляет toohello непосредственный вызов методов:

    ![Приложение для имитации устройства центра IoT Java отвечает toohello непосредственный вызов методов][9]

## <a name="next-steps"></a>Дальнейшие действия

В этом учебнике настроен центр IoT в hello портал Azure и затем создать удостоверение устройства в реестре удостоверений центра IoT hello. Вы использовали этот устройства удостоверения tooenable hello имитируемые устройства приложения tooreact toomethods вызываемая hello облака. Также было создано приложение, которое вызывает методы на устройстве hello и отображает hello ответа от устройства hello.

tooexplore см. другие сценарии IoT [расписание заданий на нескольких устройствах][lnk-devguide-jobs].

toolearn tooextend IoT решения и расписание метод вызывает на нескольких устройствах и разделе hello [расписание и широковещательных задания] [ lnk-tutorial-jobs] учебника.

<!-- Images. -->
[7]: ./media/iot-hub-java-java-direct-methods/invoke-method.png
[8]: ./media/iot-hub-java-java-direct-methods/device-listen.png
[9]: ./media/iot-hub-java-java-direct-methods/device-respond.png

<!-- Links -->
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java/blob/master/doc/java-devbox-setup.md
[lnk-maven]: https://maven.apache.org/what-is-maven.html
[lnk-hub-sdks]: iot-hub-devguide-sdks.md

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-device-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
