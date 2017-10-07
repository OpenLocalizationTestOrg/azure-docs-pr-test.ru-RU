---
title: "aaaSchedule заданий с центром IoT Azure (Java) | Документы Microsoft"
description: "Как tooschedule центр IoT Azure заданий tooinvoke прямой метод и задать нужное свойство на нескольких устройствах. Для приложений Java tooimplement hello имитируемые устройств и hello Azure IoT служба пакета SDK для Java tooimplement задание службы toorun приложения hello используется пакет SDK устройства Azure IoT hello."
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
ms.date: 07/10/2017
ms.author: dobett
ms.openlocfilehash: b1b05fa56c3ce96af0b33d4cca0dd54da0f4e927
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-and-broadcast-jobs-java"></a>Планирование и трансляция заданий (Java)

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

Используйте центр IoT Azure tooschedule и отслеживать задания, которые обновляют миллионов устройств. Что можно сделать с помощью заданий?

* Обновление требуемых свойств
* Обновление тегов
* Вызов прямых методов

Задание включает одно из следующих действий и отслеживает hello выполнение на наборе устройств. Запрос двойных устройства определяет набор hello hello задание выполняется на основе устройств. Например приложение серверной части можно использовать tooinvoke задания прямой метод на 10 000 устройств, которые перезагрузки устройства hello. Укажите hello устройств с помощью запроса двойных устройства и запланировать задание toorun hello в будущем. отслеживает ход выполнения задания Hello имени каждого из устройств hello получают и выполнить прямой метод перезагрузки hello.

toolearn Дополнительные сведения о каждой из этих возможностей см.:

* Информация о двойниках устройств и их свойствах представлена в статье [Get started with device twins (Java)](iot-hub-java-java-twin-getstarted.md) (Приступая к работе с двойниками устройств).
* Прямые методы: [Общие сведения о прямых методах и информация о вызове этих методов из Центра Интернета вещей](iot-hub-devguide-direct-methods.md) и [Использование прямых методов (Java)](iot-hub-java-java-direct-methods.md).

В этом учебнике описаны следующие процедуры.

* Создание приложения для устройств, которое реализует прямой метод c именем **lockDoor**. приложение Hello устройства также получает изменения требуемое свойство из серверной части приложения hello.
* Создания серверной части приложения, которое создает задание toocall hello **lockDoor** прямой метод на нескольких устройствах. Требуемое свойство обновить устройства toomultiple отправляет другим заданием.

В конце этого учебника hello у вас есть устройство java консольного приложения и внутреннего интерфейса java консольного приложения:

**имитируемые устройства** , соединяет центр IoT tooyour, реализующий hello **lockDoor** прямой метод и обрабатывает требуемого свойства.

**Планирование заданий** , использующие hello задания toocall **lockDoor** прямой метод и обновление двойных hello устройства требуемого свойства на нескольких устройствах.

> [!NOTE]
> статья Hello [пакеты SDK Azure IoT](iot-hub-devguide-sdks.md) предоставляет сведения о hello Azure IoT пакетов SDK, которые можно использовать toobuild устройства и серверной части приложения.

## <a name="prerequisites"></a>Предварительные требования

toocomplete этого учебника, необходимо:

* Здравствуйте, последняя версия [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* Активная учетная запись Azure. Если ее нет, можно создать [бесплатную учетную запись](http://azure.microsoft.com/pricing/free-trial/) всего за несколько минут.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

При желании удостоверения устройства hello toocreate программными средствами чтения hello соответствующий раздел в hello [подключиться с помощью Java концентратор IoT tooyour устройства](iot-hub-java-java-getstarted.md#create-a-device-identity) статьи. Можно также использовать hello [explorer центром IOT](https://github.com/Azure/iothub-explorer) tooadd средство концентратор IoT tooyour устройства.

## <a name="create-hello-service-app"></a>Создание приложения hello службы

В этом разделе приведена процедура создания консольного приложения Java, которое с помощью заданий выполняет следующие действия.

* Вызовите hello **lockDoor** прямой метод на нескольких устройствах.
* Отправьте toomultiple нужные свойства устройства.

приложение hello toocreate:

1. На компьютере разработки создайте пустую папку с именем `iot-java-schedule-jobs`.

1. В hello `iot-java-schedule-jobs` папки, создайте проект с именем Maven **расписания заданий** с помощью hello следующую команду в командной строке. Обратите внимание, что это одна длинная команда.

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=schedule-jobs -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. В командной строке перейдите toohello `schedule-jobs` папки.

1. В текстовом редакторе, откройте hello `pom.xml` файла в hello `schedule-jobs` папки и добавьте следующие зависимости toohello hello **зависимости** узла. Эта зависимость позволяет toouse hello **клиента для службы iot** пакет в toocommunicate вашего приложения с вашего центра IoT:

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

1. В текстовом редакторе, откройте hello `schedule-jobs\src\main\java\com\mycompany\app\App.java` файла.

1. Добавьте следующее hello **импорта** toohello файл инструкций:

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceTwinDevice;
    import com.microsoft.azure.sdk.iot.service.devicetwin.Pair;
    import com.microsoft.azure.sdk.iot.service.devicetwin.Query;
    import com.microsoft.azure.sdk.iot.service.devicetwin.SqlQuery;
    import com.microsoft.azure.sdk.iot.service.jobs.JobClient;
    import com.microsoft.azure.sdk.iot.service.jobs.JobResult;
    import com.microsoft.azure.sdk.iot.service.jobs.JobStatus;

    import java.util.Date;
    import java.time.Instant;
    import java.util.HashSet;
    import java.util.Set;
    import java.util.UUID;
    ```

1. Добавьте следующие переменные уровня класса toohello hello **приложения** класса. Замените `{youriothubconnectionstring}` с IoT строку подключения к концентратору нижеприведенного hello *создать центр IoT* раздела:

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    // How long hello job is permitted toorun without
    // completing its work on hello set of devices
    private static final long maxExecutionTimeInSeconds = 30;
    ```

1. Добавьте следующий метод toohello hello **приложения** tooschedule класс типа hello tooupdate задания **построение** и **Floor** требуемого свойства в двойных hello устройства:

    ```java
    private static JobResult scheduleJobSetDesiredProperties(JobClient jobClient, String jobId) {
      DeviceTwinDevice twin = new DeviceTwinDevice(deviceId);
      Set<Pair> desiredProperties = new HashSet<Pair>();
      desiredProperties.add(new Pair("Building", 43));
      desiredProperties.add(new Pair("Floor", 3));
      twin.setDesiredProperties(desiredProperties);
      // Optimistic concurrency control
      twin.setETag("*");

      // Schedule hello update twin job toorun now
      // against a single device
      System.out.println("Schedule job " + jobId + " for device " + deviceId);
      try {
        JobResult jobResult = jobClient.scheduleUpdateTwin(jobId, 
          "deviceId='" + deviceId + "'",
          twin,
          new Date(),
          maxExecutionTimeInSeconds);
        return jobResult;
      } catch (Exception e) {
        System.out.println("Exception scheduling desired properties job: " + jobId);
        System.out.println(e.getMessage());
        return null;
      }
    }
    ```

1. tooschedule hello задания toocall **lockDoor** метод, добавьте следующий метод toohello hello **приложения** класса:

    ```java
    private static JobResult scheduleJobCallDirectMethod(JobClient jobClient, String jobId) {
      // Schedule a job now toocall hello lockDoor direct method
      // against a single device. Response and connection
      // timeouts are set too5 seconds.
      System.out.println("Schedule job " + jobId + " for device " + deviceId);
      try {
        JobResult jobResult = jobClient.scheduleDeviceMethod(jobId,
          "deviceId='" + deviceId + "'",
          "lockDoor",
          5L, 5L, null,
          new Date(),
          maxExecutionTimeInSeconds);
        return jobResult;
      } catch (Exception e) {
        System.out.println("Exception scheduling direct method job: " + jobId);
        System.out.println(e.getMessage());
        return null;
      }
    };
    ```

1. toomonitor задания, добавьте следующий метод toohello hello **приложения** класса:

    ```java
    private static void monitorJob(JobClient jobClient, String jobId) {
      try {
        JobResult jobResult = jobClient.getJob(jobId);
        if(jobResult == null)
        {
          System.out.println("No JobResult for: " + jobId);
          return;
        }
        // Check hello job result until it's completed
        while(jobResult.getJobStatus() != JobStatus.completed)
        {
          Thread.sleep(100);
          jobResult = jobClient.getJob(jobId);
          System.out.println("Status " + jobResult.getJobStatus() + " for job " + jobId);
        }
        System.out.println("Final status " + jobResult.getJobStatus() + " for job " + jobId);
      } catch (Exception e) {
        System.out.println("Exception monitoring job: " + jobId);
        System.out.println(e.getMessage());
        return;
      }
    }
    ```

1. tooquery подробности hello hello заданий после предыдущего запуска, добавьте следующий метод hello:

    ```java
    private static void queryDeviceJobs(JobClient jobClient, String start) throws Exception {
      System.out.println("\nQuery device jobs since " + start);

      // Create a jobs query using hello time hello jobs started
      Query deviceJobQuery = jobClient
          .queryDeviceJob(SqlQuery.createSqlQuery("*", SqlQuery.FromType.JOBS, "devices.jobs.startTimeUtc > '" + start + "'", null).getQuery());

      // Iterate over hello list of jobs and print hello details
      while (jobClient.hasNextJob(deviceJobQuery)) {
        System.out.println(jobClient.getNextJob(deviceJobQuery));
      }
    }
    ```

1. Обновление hello **основной** следующие hello tooinclude подпись метода `throws` предложения:

    ```java
    public static void main( String[] args ) throws Exception
    ```

1. монитора и toorun два задания последовательно, добавьте следующий код toohello hello **основной** метод:

    ```java
    // Record hello start time
    String start = Instant.now().toString();

    // Create JobClient
    JobClient jobClient = JobClient.createFromConnectionString(iotHubConnectionString);
    System.out.println("JobClient created with success");

    // Schedule twin job desired properties
    // Maximum concurrent jobs is 1 for Free and S1 tiers
    String desiredPropertiesJobId = "DPCMD" + UUID.randomUUID();
    scheduleJobSetDesiredProperties(jobClient, desiredPropertiesJobId);
    monitorJob(jobClient, desiredPropertiesJobId);

    // Schedule twin job direct method
    String directMethodJobId = "DMCMD" + UUID.randomUUID();
    scheduleJobCallDirectMethod(jobClient, directMethodJobId);
    monitorJob(jobClient, directMethodJobId);

    // Run a query tooshow hello job detail
    queryDeviceJobs(jobClient, start);

    System.out.println("Shutting down schedule-jobs app");
    ```

1. Сохраните и закройте hello `schedule-jobs\src\main\java\com\mycompany\app\App.java` файла

1. Построение hello **расписания заданий** приложения и исправьте все ошибки. В командной строке перейдите toohello `schedule-jobs` папки и выполнения hello следующую команду:

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a>Создание приложения устройства

В этом разделе создайте консольное приложение Java, которое обрабатывает hello нужными свойствами, отправленные центр IoT и реализует hello непосредственный вызов методов.

1. В hello `iot-java-schedule-jobs` папки, создайте проект с именем Maven **имитируемые устройства** с помощью hello следующую команду в командной строке. Обратите внимание, что это одна длинная команда.

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
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    Этот пример приложения использует hello **протокола** переменной, когда он создает **DeviceClient** объекта. В настоящее время toouse двойных функциями устройства необходимо использовать протокол MQTT hello.

1. tooprint устройства двойных уведомления toohello консоли, добавьте следующее hello вложенных классов toohello **приложения** класса:

    ```java
    // Handler for device twin operation notifications from IoT Hub
    protected static class DeviceTwinStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toodevice twin operation with status " + status.name());
      }
    }
    ```

1. tooprint прямой метод уведомления toohello консоли, добавьте следующее hello вложенных классов toohello **приложения** класса:

    ```java
    // Handler for direct method notifications from IoT Hub
    protected static class DirectMethodStatusCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toodirect method operation with status " + status.name());
      }
    }
    ```

1. toohandle прямых вызовов из центра IoT, добавьте следующее hello вложенных классов toohello **приложения** класса:

    ```java
    // Handler for direct method calls from IoT Hub
    protected static class DirectMethodCallback
        implements DeviceMethodCallback {
      @Override
      public DeviceMethodData call(String methodName, Object methodData, Object context) {
        DeviceMethodData deviceMethodData;
        switch (methodName) {
          case "lockDoor": {
            System.out.println("Executing direct method: " + methodName);
            deviceMethodData = new DeviceMethodData(METHOD_SUCCESS, "Executed direct method " + methodName);
            break;
          }
          default: {
            deviceMethodData = new DeviceMethodData(METHOD_NOT_DEFINED, "Not defined direct method " + methodName);
          }
        }
        // Notify IoT Hub of result
        return deviceMethodData;
      }
    }
    ```

1. Обновление hello **основной** следующие hello tooinclude подпись метода `throws` предложения:

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException
    ```

1. Добавьте следующий код toohello hello **основной** метода:
    * Создайте toocommunicate клиента устройства с центром IoT.
    * Создание **устройства** toostore hello устройства двойных свойства объекта.

    ```java
    // Create a device client
    DeviceClient client = new DeviceClient(connString, protocol);

    // An object toomanage device twin desired and reported properties
    Device dataCollector = new Device() {
      @Override
      public void PropertyCall(String propertyKey, Object propertyValue, Object context)
      {
        System.out.println("Received desired property change: " + propertyKey + " " + propertyValue);
      }
    };
    ```

1. службы клиентских устройств toostart hello, добавьте следующие toohello кода hello **основной** метод:

    ```java
    try {
      // Open hello DeviceClient
      // Start hello device twin services
      // Subscribe toodirect method calls
      client.open();
      client.startDeviceTwin(new DeviceTwinStatusCallBack(), null, dataCollector, null);
      client.subscribeToDeviceMethod(new DirectMethodCallback(), null, new DirectMethodStatusCallback(), null);
    } catch (Exception e) {
      System.out.println("Exception, shutting down \n" + " Cause: " + e.getCause() + " \n" + e.getMessage());
      dataCollector.clean();
      client.closeNow();
      System.out.println("Shutting down...");
    }
    ```

1. toowait для hello пользователя toopress hello **ввод** ключа перед завершением работы, добавьте после окончания toohello кода hello hello **основной** метод:

    ```java
    // Close hello app
    System.out.println("Press any key tooexit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    dataCollector.clean();
    client.closeNow();
    scanner.close();
    ```

1. Сохраните и закройте hello `simulated-device\src\main\java\com\mycompany\app\App.java` файла.

1. Построение hello **имитируемые устройства** приложения и исправьте все ошибки. В командной строке перейдите toohello `simulated-device` папки и выполнения hello следующую команду:

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a>Запускайте приложения hello

Теперь вы находитесь готов toorun hello консольных приложениях.

1. В командной строке в hello `simulated-device` папки, запустите следующие команды toostart hello устройства app прослушивание изменений нужное свойство и его прямых вызовов hello:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![запускает Hello устройства клиента](media/iot-hub-java-java-schedule-jobs/device-app-1.png)

1. В командной строке в hello `schedule-jobs` папку, следующая команда toorun hello hello **расписания заданий** службы приложения toorun два задания. Hello сначала задает значения свойств требуемого hello, второй вызовы hello hello прямой метод:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java-приложение службы Центра Интернета вещей создает два задания](media/iot-hub-java-java-schedule-jobs/service-app-1.png)

1. приложение Hello устройство обрабатывает изменение свойства требуемого hello и hello непосредственный вызов методов:

    ![Hello устройства клиент отвечает toohello изменения](media/iot-hub-java-java-schedule-jobs/device-app-2.png)

## <a name="next-steps"></a>Дальнейшие действия

В этом учебнике настроен центр IoT в hello портал Azure и затем создать удостоверение устройства в реестре удостоверений центра IoT hello. Вы создали приложение серверной части toorun два задания. первое задание Hello задать необходимые значения свойств, а второе задание hello называется прямой метод.

Hello используйте следующие ресурсы toolearn как для:

* Отправка данных телеметрии с устройствами с помощью hello [приступить к работе с центром IoT](iot-hub-java-java-getstarted.md) учебника.
* Управление устройствами интерактивно (такие как включение вентилятор из управляемой пользователем приложения) с hello [использовать прямые методы](iot-hub-java-java-direct-methods.md) учебника.
