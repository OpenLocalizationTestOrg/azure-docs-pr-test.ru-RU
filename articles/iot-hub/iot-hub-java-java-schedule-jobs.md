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
# <a name="schedule-and-broadcast-jobs-java"></a><span data-ttu-id="2e7eb-104">Планирование и трансляция заданий (Java)</span><span class="sxs-lookup"><span data-stu-id="2e7eb-104">Schedule and broadcast jobs (Java)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="2e7eb-105">Используйте центр IoT Azure tooschedule и отслеживать задания, которые обновляют миллионов устройств.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-105">Use Azure IoT Hub tooschedule and track jobs that update millions of devices.</span></span> <span data-ttu-id="2e7eb-106">Что можно сделать с помощью заданий?</span><span class="sxs-lookup"><span data-stu-id="2e7eb-106">Use jobs to:</span></span>

* <span data-ttu-id="2e7eb-107">Обновление требуемых свойств</span><span class="sxs-lookup"><span data-stu-id="2e7eb-107">Update desired properties</span></span>
* <span data-ttu-id="2e7eb-108">Обновление тегов</span><span class="sxs-lookup"><span data-stu-id="2e7eb-108">Update tags</span></span>
* <span data-ttu-id="2e7eb-109">Вызов прямых методов</span><span class="sxs-lookup"><span data-stu-id="2e7eb-109">Invoke direct methods</span></span>

<span data-ttu-id="2e7eb-110">Задание включает одно из следующих действий и отслеживает hello выполнение на наборе устройств.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-110">A job wraps one of these actions and tracks hello execution against a set of devices.</span></span> <span data-ttu-id="2e7eb-111">Запрос двойных устройства определяет набор hello hello задание выполняется на основе устройств.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-111">A device twin query defines hello set of devices hello job executes against.</span></span> <span data-ttu-id="2e7eb-112">Например приложение серверной части можно использовать tooinvoke задания прямой метод на 10 000 устройств, которые перезагрузки устройства hello.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-112">For example, a back-end app can use a job tooinvoke a direct method on 10,000 devices that reboots hello devices.</span></span> <span data-ttu-id="2e7eb-113">Укажите hello устройств с помощью запроса двойных устройства и запланировать задание toorun hello в будущем.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-113">You specify hello set of devices with a device twin query and schedule hello job toorun at a future time.</span></span> <span data-ttu-id="2e7eb-114">отслеживает ход выполнения задания Hello имени каждого из устройств hello получают и выполнить прямой метод перезагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-114">hello job tracks progress as each of hello devices receive and execute hello reboot direct method.</span></span>

<span data-ttu-id="2e7eb-115">toolearn Дополнительные сведения о каждой из этих возможностей см.:</span><span class="sxs-lookup"><span data-stu-id="2e7eb-115">toolearn more about each of these capabilities, see:</span></span>

* <span data-ttu-id="2e7eb-116">Информация о двойниках устройств и их свойствах представлена в статье [Get started with device twins (Java)](iot-hub-java-java-twin-getstarted.md) (Приступая к работе с двойниками устройств).</span><span class="sxs-lookup"><span data-stu-id="2e7eb-116">Device twin and properties: [Get started with device twins](iot-hub-java-java-twin-getstarted.md)</span></span>
* <span data-ttu-id="2e7eb-117">Прямые методы: [Общие сведения о прямых методах и информация о вызове этих методов из Центра Интернета вещей](iot-hub-devguide-direct-methods.md) и [Использование прямых методов (Java)](iot-hub-java-java-direct-methods.md).</span><span class="sxs-lookup"><span data-stu-id="2e7eb-117">Direct methods: [IoT Hub developer guide - direct methods](iot-hub-devguide-direct-methods.md) and [Tutorial: Use direct methods](iot-hub-java-java-direct-methods.md)</span></span>

<span data-ttu-id="2e7eb-118">В этом учебнике описаны следующие процедуры.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-118">This tutorial shows you how to:</span></span>

* <span data-ttu-id="2e7eb-119">Создание приложения для устройств, которое реализует прямой метод c именем **lockDoor**.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-119">Create a device app that implements a direct method called **lockDoor**.</span></span> <span data-ttu-id="2e7eb-120">приложение Hello устройства также получает изменения требуемое свойство из серверной части приложения hello.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-120">hello device app also receives desired property changes from hello back-end app.</span></span>
* <span data-ttu-id="2e7eb-121">Создания серверной части приложения, которое создает задание toocall hello **lockDoor** прямой метод на нескольких устройствах.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-121">Create a back-end app that creates a job toocall hello **lockDoor** direct method on multiple devices.</span></span> <span data-ttu-id="2e7eb-122">Требуемое свойство обновить устройства toomultiple отправляет другим заданием.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-122">Another job sends desired property updates toomultiple devices.</span></span>

<span data-ttu-id="2e7eb-123">В конце этого учебника hello у вас есть устройство java консольного приложения и внутреннего интерфейса java консольного приложения:</span><span class="sxs-lookup"><span data-stu-id="2e7eb-123">At hello end of this tutorial, you have a java console device app and a java console back-end app:</span></span>

<span data-ttu-id="2e7eb-124">**имитируемые устройства** , соединяет центр IoT tooyour, реализующий hello **lockDoor** прямой метод и обрабатывает требуемого свойства.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-124">**simulated-device** that connects tooyour IoT hub, implements hello **lockDoor** direct method, and handles desired property changes.</span></span>

<span data-ttu-id="2e7eb-125">**Планирование заданий** , использующие hello задания toocall **lockDoor** прямой метод и обновление двойных hello устройства требуемого свойства на нескольких устройствах.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-125">**schedule-jobs** that use jobs toocall hello **lockDoor** direct method and update hello device twin desired properties on multiple devices.</span></span>

> [!NOTE]
> <span data-ttu-id="2e7eb-126">статья Hello [пакеты SDK Azure IoT](iot-hub-devguide-sdks.md) предоставляет сведения о hello Azure IoT пакетов SDK, которые можно использовать toobuild устройства и серверной части приложения.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-126">hello article [Azure IoT SDKs](iot-hub-devguide-sdks.md) provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2e7eb-127">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="2e7eb-127">Prerequisites</span></span>

<span data-ttu-id="2e7eb-128">toocomplete этого учебника, необходимо:</span><span class="sxs-lookup"><span data-stu-id="2e7eb-128">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="2e7eb-129">Здравствуйте, последняя версия [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="2e7eb-129">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="2e7eb-130">Maven 3</span><span class="sxs-lookup"><span data-stu-id="2e7eb-130">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="2e7eb-131">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-131">An active Azure account.</span></span> <span data-ttu-id="2e7eb-132">Если ее нет, можно создать [бесплатную учетную запись](http://azure.microsoft.com/pricing/free-trial/) всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-132">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="2e7eb-133">При желании удостоверения устройства hello toocreate программными средствами чтения hello соответствующий раздел в hello [подключиться с помощью Java концентратор IoT tooyour устройства](iot-hub-java-java-getstarted.md#create-a-device-identity) статьи.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-133">If you prefer toocreate hello device identity programmatically, read hello corresponding section in hello [Connect your device tooyour IoT hub using Java](iot-hub-java-java-getstarted.md#create-a-device-identity) article.</span></span> <span data-ttu-id="2e7eb-134">Можно также использовать hello [explorer центром IOT](https://github.com/Azure/iothub-explorer) tooadd средство концентратор IoT tooyour устройства.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-134">You can also use hello [iothub-explorer](https://github.com/Azure/iothub-explorer) tool tooadd a device tooyour IoT hub.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="2e7eb-135">Создание приложения hello службы</span><span class="sxs-lookup"><span data-stu-id="2e7eb-135">Create hello service app</span></span>

<span data-ttu-id="2e7eb-136">В этом разделе приведена процедура создания консольного приложения Java, которое с помощью заданий выполняет следующие действия.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-136">In this section, you create a Java console app that uses jobs to:</span></span>

* <span data-ttu-id="2e7eb-137">Вызовите hello **lockDoor** прямой метод на нескольких устройствах.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-137">Call hello **lockDoor** direct method on multiple devices.</span></span>
* <span data-ttu-id="2e7eb-138">Отправьте toomultiple нужные свойства устройства.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-138">Send desired properties toomultiple devices.</span></span>

<span data-ttu-id="2e7eb-139">приложение hello toocreate:</span><span class="sxs-lookup"><span data-stu-id="2e7eb-139">toocreate hello app:</span></span>

1. <span data-ttu-id="2e7eb-140">На компьютере разработки создайте пустую папку с именем `iot-java-schedule-jobs`.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-140">On your development machine, create an empty folder called `iot-java-schedule-jobs`.</span></span>

1. <span data-ttu-id="2e7eb-141">В hello `iot-java-schedule-jobs` папки, создайте проект с именем Maven **расписания заданий** с помощью hello следующую команду в командной строке.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-141">In hello `iot-java-schedule-jobs` folder, create a Maven project called **schedule-jobs** using hello following command at your command prompt.</span></span> <span data-ttu-id="2e7eb-142">Обратите внимание, что это одна длинная команда.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-142">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=schedule-jobs -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="2e7eb-143">В командной строке перейдите toohello `schedule-jobs` папки.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-143">At your command prompt, navigate toohello `schedule-jobs` folder.</span></span>

1. <span data-ttu-id="2e7eb-144">В текстовом редакторе, откройте hello `pom.xml` файла в hello `schedule-jobs` папки и добавьте следующие зависимости toohello hello **зависимости** узла.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-144">Using a text editor, open hello `pom.xml` file in hello `schedule-jobs` folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="2e7eb-145">Эта зависимость позволяет toouse hello **клиента для службы iot** пакет в toocommunicate вашего приложения с вашего центра IoT:</span><span class="sxs-lookup"><span data-stu-id="2e7eb-145">This dependency enables you toouse hello **iot-service-client** package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="2e7eb-146">Вы можете проверить наличие hello последнюю версию **клиента для службы iot** с помощью [Maven поиска](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="2e7eb-146">You can check for hello latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="2e7eb-147">Добавьте следующее hello **построения** узел после hello **зависимости** узла.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-147">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="2e7eb-148">Эта конфигурация указывает, что приложение hello 1,8 toobuild Java toouse Maven:</span><span class="sxs-lookup"><span data-stu-id="2e7eb-148">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="2e7eb-149">Сохраните и закройте hello `pom.xml` файла.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-149">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="2e7eb-150">В текстовом редакторе, откройте hello `schedule-jobs\src\main\java\com\mycompany\app\App.java` файла.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-150">Using a text editor, open hello `schedule-jobs\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="2e7eb-151">Добавьте следующее hello **импорта** toohello файл инструкций:</span><span class="sxs-lookup"><span data-stu-id="2e7eb-151">Add hello following **import** statements toohello file:</span></span>

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

1. <span data-ttu-id="2e7eb-152">Добавьте следующие переменные уровня класса toohello hello **приложения** класса.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-152">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="2e7eb-153">Замените `{youriothubconnectionstring}` с IoT строку подключения к концентратору нижеприведенного hello *создать центр IoT* раздела:</span><span class="sxs-lookup"><span data-stu-id="2e7eb-153">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in hello *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    // How long hello job is permitted toorun without
    // completing its work on hello set of devices
    private static final long maxExecutionTimeInSeconds = 30;
    ```

1. <span data-ttu-id="2e7eb-154">Добавьте следующий метод toohello hello **приложения** tooschedule класс типа hello tooupdate задания **построение** и **Floor** требуемого свойства в двойных hello устройства:</span><span class="sxs-lookup"><span data-stu-id="2e7eb-154">Add hello following method toohello **App** class tooschedule a job tooupdate hello **Building** and **Floor** desired properties in hello device twin:</span></span>

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

1. <span data-ttu-id="2e7eb-155">tooschedule hello задания toocall **lockDoor** метод, добавьте следующий метод toohello hello **приложения** класса:</span><span class="sxs-lookup"><span data-stu-id="2e7eb-155">tooschedule a job toocall hello **lockDoor** method, add hello following method toohello **App** class:</span></span>

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

1. <span data-ttu-id="2e7eb-156">toomonitor задания, добавьте следующий метод toohello hello **приложения** класса:</span><span class="sxs-lookup"><span data-stu-id="2e7eb-156">toomonitor a job, add hello following method toohello **App** class:</span></span>

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

1. <span data-ttu-id="2e7eb-157">tooquery подробности hello hello заданий после предыдущего запуска, добавьте следующий метод hello:</span><span class="sxs-lookup"><span data-stu-id="2e7eb-157">tooquery for hello details of hello jobs you ran, add hello following method:</span></span>

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

1. <span data-ttu-id="2e7eb-158">Обновление hello **основной** следующие hello tooinclude подпись метода `throws` предложения:</span><span class="sxs-lookup"><span data-stu-id="2e7eb-158">Update hello **main** method signature tooinclude hello following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws Exception
    ```

1. <span data-ttu-id="2e7eb-159">монитора и toorun два задания последовательно, добавьте следующий код toohello hello **основной** метод:</span><span class="sxs-lookup"><span data-stu-id="2e7eb-159">toorun and monitor two jobs sequentially, add hello following code toohello **main** method:</span></span>

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

1. <span data-ttu-id="2e7eb-160">Сохраните и закройте hello `schedule-jobs\src\main\java\com\mycompany\app\App.java` файла</span><span class="sxs-lookup"><span data-stu-id="2e7eb-160">Save and close hello `schedule-jobs\src\main\java\com\mycompany\app\App.java` file</span></span>

1. <span data-ttu-id="2e7eb-161">Построение hello **расписания заданий** приложения и исправьте все ошибки.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-161">Build hello **schedule-jobs** app and correct any errors.</span></span> <span data-ttu-id="2e7eb-162">В командной строке перейдите toohello `schedule-jobs` папки и выполнения hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="2e7eb-162">At your command prompt, navigate toohello `schedule-jobs` folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a><span data-ttu-id="2e7eb-163">Создание приложения устройства</span><span class="sxs-lookup"><span data-stu-id="2e7eb-163">Create a device app</span></span>

<span data-ttu-id="2e7eb-164">В этом разделе создайте консольное приложение Java, которое обрабатывает hello нужными свойствами, отправленные центр IoT и реализует hello непосредственный вызов методов.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-164">In this section, you create a Java console app that handles hello desired properties sent from IoT Hub and implements hello direct method call.</span></span>

1. <span data-ttu-id="2e7eb-165">В hello `iot-java-schedule-jobs` папки, создайте проект с именем Maven **имитируемые устройства** с помощью hello следующую команду в командной строке.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-165">In hello `iot-java-schedule-jobs` folder, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="2e7eb-166">Обратите внимание, что это одна длинная команда.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-166">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="2e7eb-167">В командной строке перейдите toohello `simulated-device` папки.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-167">At your command prompt, navigate toohello `simulated-device` folder.</span></span>

1. <span data-ttu-id="2e7eb-168">В текстовом редакторе, откройте hello `pom.xml` файла в hello `simulated-device` папки и добавьте следующие зависимости toohello hello **зависимости** узла.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-168">Using a text editor, open hello `pom.xml` file in hello `simulated-device` folder and add hello following dependencies toohello **dependencies** node.</span></span> <span data-ttu-id="2e7eb-169">Эта зависимость позволяет toouse hello **клиента для устройства iot** пакет в toocommunicate вашего приложения с вашего центра IoT:</span><span class="sxs-lookup"><span data-stu-id="2e7eb-169">This dependency enables you toouse hello **iot-device-client** package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="2e7eb-170">Вы можете проверить наличие hello последнюю версию **клиента для устройства iot** с помощью [Maven поиска](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="2e7eb-170">You can check for hello latest version of **iot-device-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="2e7eb-171">Добавьте следующее hello **построения** узел после hello **зависимости** узла.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-171">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="2e7eb-172">Эта конфигурация указывает, что приложение hello 1,8 toobuild Java toouse Maven:</span><span class="sxs-lookup"><span data-stu-id="2e7eb-172">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="2e7eb-173">Сохраните и закройте hello `pom.xml` файла.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-173">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="2e7eb-174">В текстовом редакторе, откройте hello `simulated-device\src\main\java\com\mycompany\app\App.java` файла.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-174">Using a text editor, open hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="2e7eb-175">Добавьте следующее hello **импорта** toohello файл инструкций:</span><span class="sxs-lookup"><span data-stu-id="2e7eb-175">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="2e7eb-176">Добавьте следующие переменные уровня класса toohello hello **приложения** класса.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-176">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="2e7eb-177">Замена `{youriothubname}` на название концентратора IoT и `{yourdevicekey}` со значением ключа устройства hello созданный hello *создать удостоверение устройства* раздела:</span><span class="sxs-lookup"><span data-stu-id="2e7eb-177">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with hello device key value you generated in hello *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    <span data-ttu-id="2e7eb-178">Этот пример приложения использует hello **протокола** переменной, когда он создает **DeviceClient** объекта.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-178">This sample app uses hello **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="2e7eb-179">В настоящее время toouse двойных функциями устройства необходимо использовать протокол MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-179">Currently, toouse device twin features you must use hello MQTT protocol.</span></span>

1. <span data-ttu-id="2e7eb-180">tooprint устройства двойных уведомления toohello консоли, добавьте следующее hello вложенных классов toohello **приложения** класса:</span><span class="sxs-lookup"><span data-stu-id="2e7eb-180">tooprint device twin notifications toohello console, add hello following nested class toohello **App** class:</span></span>

    ```java
    // Handler for device twin operation notifications from IoT Hub
    protected static class DeviceTwinStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toodevice twin operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="2e7eb-181">tooprint прямой метод уведомления toohello консоли, добавьте следующее hello вложенных классов toohello **приложения** класса:</span><span class="sxs-lookup"><span data-stu-id="2e7eb-181">tooprint direct method notifications toohello console, add hello following nested class toohello **App** class:</span></span>

    ```java
    // Handler for direct method notifications from IoT Hub
    protected static class DirectMethodStatusCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toodirect method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="2e7eb-182">toohandle прямых вызовов из центра IoT, добавьте следующее hello вложенных классов toohello **приложения** класса:</span><span class="sxs-lookup"><span data-stu-id="2e7eb-182">toohandle direct method calls from IoT Hub, add hello following nested class toohello **App** class:</span></span>

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

1. <span data-ttu-id="2e7eb-183">Обновление hello **основной** следующие hello tooinclude подпись метода `throws` предложения:</span><span class="sxs-lookup"><span data-stu-id="2e7eb-183">Update hello **main** method signature tooinclude hello following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException
    ```

1. <span data-ttu-id="2e7eb-184">Добавьте следующий код toohello hello **основной** метода:</span><span class="sxs-lookup"><span data-stu-id="2e7eb-184">Add hello following code toohello **main** method to:</span></span>
    * <span data-ttu-id="2e7eb-185">Создайте toocommunicate клиента устройства с центром IoT.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-185">Create a device client toocommunicate with IoT Hub.</span></span>
    * <span data-ttu-id="2e7eb-186">Создание **устройства** toostore hello устройства двойных свойства объекта.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-186">Create a **Device** object toostore hello device twin properties.</span></span>

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

1. <span data-ttu-id="2e7eb-187">службы клиентских устройств toostart hello, добавьте следующие toohello кода hello **основной** метод:</span><span class="sxs-lookup"><span data-stu-id="2e7eb-187">toostart hello device client services, add hello following code toohello **main** method:</span></span>

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

1. <span data-ttu-id="2e7eb-188">toowait для hello пользователя toopress hello **ввод** ключа перед завершением работы, добавьте после окончания toohello кода hello hello **основной** метод:</span><span class="sxs-lookup"><span data-stu-id="2e7eb-188">toowait for hello user toopress hello **Enter** key before shutting down, add hello following code toohello end of hello **main** method:</span></span>

    ```java
    // Close hello app
    System.out.println("Press any key tooexit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    dataCollector.clean();
    client.closeNow();
    scanner.close();
    ```

1. <span data-ttu-id="2e7eb-189">Сохраните и закройте hello `simulated-device\src\main\java\com\mycompany\app\App.java` файла.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-189">Save and close hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="2e7eb-190">Построение hello **имитируемые устройства** приложения и исправьте все ошибки.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-190">Build hello **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="2e7eb-191">В командной строке перейдите toohello `simulated-device` папки и выполнения hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="2e7eb-191">At your command prompt, navigate toohello `simulated-device` folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a><span data-ttu-id="2e7eb-192">Запускайте приложения hello</span><span class="sxs-lookup"><span data-stu-id="2e7eb-192">Run hello apps</span></span>

<span data-ttu-id="2e7eb-193">Теперь вы находитесь готов toorun hello консольных приложениях.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-193">You are now ready toorun hello console apps.</span></span>

1. <span data-ttu-id="2e7eb-194">В командной строке в hello `simulated-device` папки, запустите следующие команды toostart hello устройства app прослушивание изменений нужное свойство и его прямых вызовов hello:</span><span class="sxs-lookup"><span data-stu-id="2e7eb-194">At a command prompt in hello `simulated-device` folder, run hello following command toostart hello device app listening for desired property changes and direct method calls:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![запускает Hello устройства клиента](media/iot-hub-java-java-schedule-jobs/device-app-1.png)

1. <span data-ttu-id="2e7eb-196">В командной строке в hello `schedule-jobs` папку, следующая команда toorun hello hello **расписания заданий** службы приложения toorun два задания.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-196">At a command prompt in hello `schedule-jobs` folder, run hello following command toorun hello **schedule-jobs** service app toorun two jobs.</span></span> <span data-ttu-id="2e7eb-197">Hello сначала задает значения свойств требуемого hello, второй вызовы hello hello прямой метод:</span><span class="sxs-lookup"><span data-stu-id="2e7eb-197">hello first sets hello desired property values, hello second calls hello direct method:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java-приложение службы Центра Интернета вещей создает два задания](media/iot-hub-java-java-schedule-jobs/service-app-1.png)

1. <span data-ttu-id="2e7eb-199">приложение Hello устройство обрабатывает изменение свойства требуемого hello и hello непосредственный вызов методов:</span><span class="sxs-lookup"><span data-stu-id="2e7eb-199">hello device app handles hello desired property change and hello direct method call:</span></span>

    ![Hello устройства клиент отвечает toohello изменения](media/iot-hub-java-java-schedule-jobs/device-app-2.png)

## <a name="next-steps"></a><span data-ttu-id="2e7eb-201">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2e7eb-201">Next steps</span></span>

<span data-ttu-id="2e7eb-202">В этом учебнике настроен центр IoT в hello портал Azure и затем создать удостоверение устройства в реестре удостоверений центра IoT hello.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-202">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="2e7eb-203">Вы создали приложение серверной части toorun два задания.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-203">You created a back-end app toorun two jobs.</span></span> <span data-ttu-id="2e7eb-204">первое задание Hello задать необходимые значения свойств, а второе задание hello называется прямой метод.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-204">hello first job set desired property values, and hello second job called a direct method.</span></span>

<span data-ttu-id="2e7eb-205">Hello используйте следующие ресурсы toolearn как для:</span><span class="sxs-lookup"><span data-stu-id="2e7eb-205">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="2e7eb-206">Отправка данных телеметрии с устройствами с помощью hello [приступить к работе с центром IoT](iot-hub-java-java-getstarted.md) учебника.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-206">Send telemetry from devices with hello [Get started with IoT Hub](iot-hub-java-java-getstarted.md) tutorial.</span></span>
* <span data-ttu-id="2e7eb-207">Управление устройствами интерактивно (такие как включение вентилятор из управляемой пользователем приложения) с hello [использовать прямые методы](iot-hub-java-java-direct-methods.md) учебника.</span><span class="sxs-lookup"><span data-stu-id="2e7eb-207">Control devices interactively (such as turning on a fan from a user-controlled app) with hello [Use direct methods](iot-hub-java-java-direct-methods.md) tutorial.</span></span>
