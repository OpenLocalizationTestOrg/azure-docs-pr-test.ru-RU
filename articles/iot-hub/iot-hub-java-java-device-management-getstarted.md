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
# <a name="get-started-with-device-management-java"></a><span data-ttu-id="20ebd-104">Начало работы с управлением устройствами (Java)</span><span class="sxs-lookup"><span data-stu-id="20ebd-104">Get started with device management (Java)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="20ebd-105">В этом учебнике описаны следующие процедуры.</span><span class="sxs-lookup"><span data-stu-id="20ebd-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="20ebd-106">Используйте hello Azure портала toocreate центр IoT и создать удостоверение устройства в концентратор IoT.</span><span class="sxs-lookup"><span data-stu-id="20ebd-106">Use hello Azure portal toocreate an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="20ebd-107">Создание приложения имитированное устройство, которое реализует устройства прямой метод tooreboot hello.</span><span class="sxs-lookup"><span data-stu-id="20ebd-107">Create a simulated device app that implements a direct method tooreboot hello device.</span></span> <span data-ttu-id="20ebd-108">Прямой методы вызываются из облака hello.</span><span class="sxs-lookup"><span data-stu-id="20ebd-108">Direct methods are invoked from hello cloud.</span></span>
* <span data-ttu-id="20ebd-109">Создайте приложение, которое вызывает метод прямой перезагрузки hello в приложение hello имитированное устройство через концентратор IoT.</span><span class="sxs-lookup"><span data-stu-id="20ebd-109">Create an app that invokes hello reboot direct method in hello simulated device app through your IoT hub.</span></span> <span data-ttu-id="20ebd-110">Это приложение, а затем мониторы hello выводятся свойства из toosee hello устройств после завершения операции перезагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="20ebd-110">This app then monitors hello reported properties from hello device toosee when hello reboot operation is complete.</span></span>

<span data-ttu-id="20ebd-111">В конце этого учебника hello у вас есть два консольные приложения Java:</span><span class="sxs-lookup"><span data-stu-id="20ebd-111">At hello end of this tutorial, you have two Java console apps:</span></span>

<span data-ttu-id="20ebd-112">**simulated-device**.</span><span class="sxs-lookup"><span data-stu-id="20ebd-112">**simulated-device**.</span></span> <span data-ttu-id="20ebd-113">Это приложение:</span><span class="sxs-lookup"><span data-stu-id="20ebd-113">This app:</span></span>

* <span data-ttu-id="20ebd-114">Центр IoT tooyour подключается с идентификатором hello устройства, созданный ранее.</span><span class="sxs-lookup"><span data-stu-id="20ebd-114">Connects tooyour IoT hub with hello device identity created earlier.</span></span>
* <span data-ttu-id="20ebd-115">получает вызов прямого метода перезагрузки;</span><span class="sxs-lookup"><span data-stu-id="20ebd-115">Receives a reboot direct method call.</span></span>
* <span data-ttu-id="20ebd-116">имитирует физическую перезагрузку;</span><span class="sxs-lookup"><span data-stu-id="20ebd-116">Simulates a physical reboot.</span></span>
* <span data-ttu-id="20ebd-117">Отчеты hello время последней перезагрузки hello через свойство отчета.</span><span class="sxs-lookup"><span data-stu-id="20ebd-117">Reports hello time of hello last reboot through a reported property.</span></span>

<span data-ttu-id="20ebd-118">**trigger-reboot**.</span><span class="sxs-lookup"><span data-stu-id="20ebd-118">**trigger-reboot**.</span></span> <span data-ttu-id="20ebd-119">Это приложение:</span><span class="sxs-lookup"><span data-stu-id="20ebd-119">This app:</span></span>

* <span data-ttu-id="20ebd-120">Вызывает метод с прямой приложение hello имитированное устройство.</span><span class="sxs-lookup"><span data-stu-id="20ebd-120">Calls a direct method in hello simulated device app.</span></span>
* <span data-ttu-id="20ebd-121">Отображает hello ответа toohello непосредственный вызов методов отправленных hello имитированное устройство</span><span class="sxs-lookup"><span data-stu-id="20ebd-121">Displays hello response toohello direct method call sent by hello simulated device</span></span>
* <span data-ttu-id="20ebd-122">Отображает hello обновлены сообщил свойства.</span><span class="sxs-lookup"><span data-stu-id="20ebd-122">Displays hello updated reported properties.</span></span>

> [!NOTE]
> <span data-ttu-id="20ebd-123">Сведения о hello пакетов SDK, которые можно использовать toorun toobuild приложений на устройствах и серверной части вашего решения см. в разделе [пакеты SDK Azure IoT][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="20ebd-123">For information about hello SDKs that you can use toobuild applications toorun on devices and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="20ebd-124">toocomplete этого учебника, необходимо:</span><span class="sxs-lookup"><span data-stu-id="20ebd-124">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="20ebd-125">Java SE 8.</span><span class="sxs-lookup"><span data-stu-id="20ebd-125">Java SE 8.</span></span> <br/> <span data-ttu-id="20ebd-126">[Подготовка среды разработки] [ lnk-dev-setup] описывает способ tooinstall Java для этого учебника в Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="20ebd-126">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Java for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="20ebd-127">Maven 3.</span><span class="sxs-lookup"><span data-stu-id="20ebd-127">Maven 3.</span></span>  <br/> <span data-ttu-id="20ebd-128">[Подготовка среды разработки] [ lnk-dev-setup] описывает способ tooinstall [Maven] [ lnk-maven] для этого учебника в Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="20ebd-128">[Prepare your development environment][lnk-dev-setup] describes how tooinstall [Maven][lnk-maven] for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="20ebd-129">[Node.js версии 0.10.0 или более поздней](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="20ebd-129">[Node.js version 0.10.0 or later](http://nodejs.org).</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a><span data-ttu-id="20ebd-130">Триггер удаленной перезагрузки на устройстве hello, с помощью прямой метод</span><span class="sxs-lookup"><span data-stu-id="20ebd-130">Trigger a remote reboot on hello device using a direct method</span></span>

<span data-ttu-id="20ebd-131">В этом разделе приведена процедура создания консольного приложения Java, которое выполняет следующие действия:</span><span class="sxs-lookup"><span data-stu-id="20ebd-131">In this section, you create a Java console app that:</span></span>

1. <span data-ttu-id="20ebd-132">Вызывает метод прямой перезагрузки hello в приложение hello имитированное устройство.</span><span class="sxs-lookup"><span data-stu-id="20ebd-132">Invokes hello reboot direct method in hello simulated device app.</span></span>
1. <span data-ttu-id="20ebd-133">Отображает hello ответа.</span><span class="sxs-lookup"><span data-stu-id="20ebd-133">Displays hello response.</span></span>
1. <span data-ttu-id="20ebd-134">Опрашивает hello сообщила, отправленных из устройства toodetermine hello после завершения перезагрузки hello свойств.</span><span class="sxs-lookup"><span data-stu-id="20ebd-134">Polls hello reported properties sent from hello device toodetermine when hello reboot is complete.</span></span>

<span data-ttu-id="20ebd-135">Это консольное приложение подключается tooyour центр IoT прямой метод tooinvoke hello и чтения hello сообщил свойства.</span><span class="sxs-lookup"><span data-stu-id="20ebd-135">This console app connects tooyour IoT Hub tooinvoke hello direct method and read hello reported properties.</span></span>

1. <span data-ttu-id="20ebd-136">Создайте пустую папку с именем dm-get-started.</span><span class="sxs-lookup"><span data-stu-id="20ebd-136">Create an empty folder called dm-get-started.</span></span>

1. <span data-ttu-id="20ebd-137">В папке dm get started hello создайте Maven проект с именем **триггер перезагрузки** с помощью hello следующую команду в командной строке.</span><span class="sxs-lookup"><span data-stu-id="20ebd-137">In hello dm-get-started folder, create a Maven project called **trigger-reboot** using hello following command at your command prompt.</span></span> <span data-ttu-id="20ebd-138">Hello ниже показан один, long команды:</span><span class="sxs-lookup"><span data-stu-id="20ebd-138">hello following shows a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=trigger-reboot -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="20ebd-139">В командной строке перейдите папку toohello перезагрузки триггера.</span><span class="sxs-lookup"><span data-stu-id="20ebd-139">At your command prompt, navigate toohello trigger-reboot folder.</span></span>

1. <span data-ttu-id="20ebd-140">В текстовом редакторе, откройте файл pom.xml hello в папке триггер перезагрузки hello и добавьте следующие зависимости toohello hello **зависимости** узла.</span><span class="sxs-lookup"><span data-stu-id="20ebd-140">Using a text editor, open hello pom.xml file in hello trigger-reboot folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="20ebd-141">Эта зависимость позволяет вам toouse hello клиента для службы iot пакета в toocommunicate вашего приложения с вашего центра IoT:</span><span class="sxs-lookup"><span data-stu-id="20ebd-141">This dependency enables you toouse hello iot-service-client package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="20ebd-142">Вы можете проверить наличие hello последнюю версию **клиента для службы iot** с помощью [поиска Maven][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="20ebd-142">You can check for hello latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

1. <span data-ttu-id="20ebd-143">Добавьте следующее hello **построения** узел после hello **зависимости** узла.</span><span class="sxs-lookup"><span data-stu-id="20ebd-143">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="20ebd-144">Эта конфигурация указывает, что приложение hello 1,8 toobuild Java toouse Maven:</span><span class="sxs-lookup"><span data-stu-id="20ebd-144">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="20ebd-145">Сохраните и закройте файл pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="20ebd-145">Save and close hello pom.xml file.</span></span>

1. <span data-ttu-id="20ebd-146">В текстовом редакторе откройте файл источника trigger-reboot\src\main\java\com\mycompany\app\App.java hello.</span><span class="sxs-lookup"><span data-stu-id="20ebd-146">Using a text editor, open hello trigger-reboot\src\main\java\com\mycompany\app\App.java source file.</span></span>

1. <span data-ttu-id="20ebd-147">Добавьте следующее hello **импорта** toohello файл инструкций:</span><span class="sxs-lookup"><span data-stu-id="20ebd-147">Add hello following **import** statements toohello file:</span></span>

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

1. <span data-ttu-id="20ebd-148">Добавьте следующие переменные уровня класса toohello hello **приложения** класса.</span><span class="sxs-lookup"><span data-stu-id="20ebd-148">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="20ebd-149">Замените `{youriothubconnectionstring}` с IoT строку подключения к концентратору нижеприведенного hello *создать центр IoT* раздела:</span><span class="sxs-lookup"><span data-stu-id="20ebd-149">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in hello *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    private static final String methodName = "reboot";
    private static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    private static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    ```

1. <span data-ttu-id="20ebd-150">tooimplement поток, который считывает hello сообщил свойства из устройства двойных hello каждые 10 секунд, добавьте следующее hello вложенных классов toohello **приложения** класса:</span><span class="sxs-lookup"><span data-stu-id="20ebd-150">tooimplement a thread that reads hello reported properties from hello device twin every 10 seconds, add hello following nested class toohello **App** class:</span></span>

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

1. <span data-ttu-id="20ebd-151">прямой метод tooinvoke hello перезагрузки на устройстве имитацию hello, добавить следующие toohello кода hello **основной** метод:</span><span class="sxs-lookup"><span data-stu-id="20ebd-151">tooinvoke hello reboot direct method on hello simulated device, add hello following code toohello **main** method:</span></span>

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

1. <span data-ttu-id="20ebd-152">поток toopoll toostart hello Здравствуйте выводятся свойства из hello имитированное устройство, добавьте следующий код toohello hello **основной** метод:</span><span class="sxs-lookup"><span data-stu-id="20ebd-152">toostart hello thread toopoll hello reported properties from hello simulated device, add hello following code toohello **main** method:</span></span>

    ```java
    ShowReportedProperties showReportedProperties = new ShowReportedProperties();
    ExecutorService executor = Executors.newFixedThreadPool(1);
    executor.execute(showReportedProperties);
    ```

1. <span data-ttu-id="20ebd-153">tooenable вы toostop приложение hello, добавьте следующий код toohello hello **основной** метод:</span><span class="sxs-lookup"><span data-stu-id="20ebd-153">tooenable you toostop hello app, add hello following code toohello **main** method:</span></span>

    ```java
    System.out.println("Press ENTER tooexit.");
    System.in.read();
    executor.shutdownNow();
    System.out.println("Shutting down sample...");
    ```

1. <span data-ttu-id="20ebd-154">Сохраните и закройте файл trigger-reboot\src\main\java\com\mycompany\app\App.java hello.</span><span class="sxs-lookup"><span data-stu-id="20ebd-154">Save and close hello trigger-reboot\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="20ebd-155">Построение hello **триггер перезагрузки** серверной части приложения и исправьте все ошибки.</span><span class="sxs-lookup"><span data-stu-id="20ebd-155">Build hello **trigger-reboot** back-end app and correct any errors.</span></span> <span data-ttu-id="20ebd-156">В командной строке перейдите папку триггер перезагрузки toohello и выполнения hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="20ebd-156">At your command prompt, navigate toohello trigger-reboot folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="20ebd-157">Создание приложения виртуального устройства</span><span class="sxs-lookup"><span data-stu-id="20ebd-157">Create a simulated device app</span></span>

<span data-ttu-id="20ebd-158">В этом разделе приведена процедура создания консольного приложения Java, которое имитирует устройство.</span><span class="sxs-lookup"><span data-stu-id="20ebd-158">In this section, you create a Java console app that simulates a device.</span></span> <span data-ttu-id="20ebd-159">приложение Hello прослушивает hello перезагрузки непосредственный вызов методов из вашего центра IoT и немедленно отвечает, toothat вызова.</span><span class="sxs-lookup"><span data-stu-id="20ebd-159">hello app listens for hello reboot direct method call from your IoT hub and immediately responds toothat call.</span></span> <span data-ttu-id="20ebd-160">Здравствуйте, приложения, а затем бездействует в течение некоторого времени процесса перезагрузки toosimulate hello до начала использования типа hello toonotify выводятся свойства **триггер перезагрузки** серверной части приложения, которое hello перезагрузка завершена.</span><span class="sxs-lookup"><span data-stu-id="20ebd-160">hello app then sleeps for a while toosimulate hello reboot process before it uses a reported property toonotify hello **trigger-reboot** back-end app that hello reboot is complete.</span></span>

1. <span data-ttu-id="20ebd-161">В папке dm get started hello создайте Maven проект с именем **имитируемые устройства** с помощью hello следующую команду в командной строке.</span><span class="sxs-lookup"><span data-stu-id="20ebd-161">In hello dm-get-started folder, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="20ebd-162">Hello ниже приведен один, long команды.</span><span class="sxs-lookup"><span data-stu-id="20ebd-162">hello following is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="20ebd-163">В командной строке перейдите папку toohello имитируемые устройства.</span><span class="sxs-lookup"><span data-stu-id="20ebd-163">At your command prompt, navigate toohello simulated-device folder.</span></span>

1. <span data-ttu-id="20ebd-164">В текстовом редакторе, откройте файл pom.xml hello в папке имитируемые устройства hello и добавьте следующие зависимости toohello hello **зависимости** узла.</span><span class="sxs-lookup"><span data-stu-id="20ebd-164">Using a text editor, open hello pom.xml file in hello simulated-device folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="20ebd-165">Эта зависимость позволяет вам toouse hello клиента для службы iot пакета в toocommunicate вашего приложения с вашего центра IoT:</span><span class="sxs-lookup"><span data-stu-id="20ebd-165">This dependency enables you toouse hello iot-service-client package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="20ebd-166">Вы можете проверить наличие hello последнюю версию **клиента для устройства iot** с помощью [поиска Maven][lnk-maven-device-search].</span><span class="sxs-lookup"><span data-stu-id="20ebd-166">You can check for hello latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

1. <span data-ttu-id="20ebd-167">Добавьте следующее hello **построения** узел после hello **зависимости** узла.</span><span class="sxs-lookup"><span data-stu-id="20ebd-167">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="20ebd-168">Эта конфигурация указывает, что приложение hello 1,8 toobuild Java toouse Maven:</span><span class="sxs-lookup"><span data-stu-id="20ebd-168">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="20ebd-169">Сохраните и закройте файл pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="20ebd-169">Save and close hello pom.xml file.</span></span>

1. <span data-ttu-id="20ebd-170">В текстовом редакторе откройте файл источника simulated-device\src\main\java\com\mycompany\app\App.java hello.</span><span class="sxs-lookup"><span data-stu-id="20ebd-170">Using a text editor, open hello simulated-device\src\main\java\com\mycompany\app\App.java source file.</span></span>

1. <span data-ttu-id="20ebd-171">Добавьте следующее hello **импорта** toohello файл инструкций:</span><span class="sxs-lookup"><span data-stu-id="20ebd-171">Add hello following **import** statements toohello file:</span></span>

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

1. <span data-ttu-id="20ebd-172">Добавьте следующие переменные уровня класса toohello hello **приложения** класса.</span><span class="sxs-lookup"><span data-stu-id="20ebd-172">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="20ebd-173">Замените `{yourdeviceconnectionstring}` со строкой подключения устройства hello, записанное в hello *создать удостоверение устройства* раздела:</span><span class="sxs-lookup"><span data-stu-id="20ebd-173">Replace `{yourdeviceconnectionstring}` with hello device connection string you noted in hello *Create a device identity* section:</span></span>

    ```java
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;

    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String connString = "{yourdeviceconnectionstring}";
    private static DeviceClient client;
    ```

1. <span data-ttu-id="20ebd-174">tooimplement обратного вызова обработчика для события состояния прямой метод, добавьте следующее hello вложенных классов toohello **приложения** класса:</span><span class="sxs-lookup"><span data-stu-id="20ebd-174">tooimplement a callback handler for direct method status events, add hello following nested class toohello **App** class:</span></span>

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded toodevice method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="20ebd-175">tooimplement обратного вызова обработчика для события состояния двойных устройство, добавьте следующее hello вложенных классов toohello **приложения** класса:</span><span class="sxs-lookup"><span data-stu-id="20ebd-175">tooimplement a callback handler for device twin status events, add hello following nested class toohello **App** class:</span></span>

    ```java
    protected static class DeviceTwinStatusCallback implements IotHubEventCallback
    {
        public void execute(IotHubStatusCode status, Object context)
        {
            System.out.println("IoT Hub responded toodevice twin operation with status " + status.name());
        }
    }
    ```

1. <span data-ttu-id="20ebd-176">tooimplement обработчик обратного вызова для событий свойства, добавьте следующее hello вложенных классов toohello **приложения** класса:</span><span class="sxs-lookup"><span data-stu-id="20ebd-176">tooimplement a callback handler for property events, add hello following nested class toohello **App** class:</span></span>

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

1. <span data-ttu-id="20ebd-177">tooimplement поток toosimulate hello перезагрузка устройства, добавьте следующее hello вложенных классов toohello **приложения** класса.</span><span class="sxs-lookup"><span data-stu-id="20ebd-177">tooimplement a thread toosimulate hello device reboot, add hello following nested class toohello **App** class.</span></span> <span data-ttu-id="20ebd-178">Hello поток бездействует в течение 5 секунд, а затем задает hello **lastReboot** сообщил свойство:</span><span class="sxs-lookup"><span data-stu-id="20ebd-178">hello thread sleeps for five seconds and then sets hello **lastReboot** reported property:</span></span>

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

1. <span data-ttu-id="20ebd-179">прямой метод tooimplement hello на устройстве hello, добавьте следующее hello вложенных классов toohello **приложения** класса.</span><span class="sxs-lookup"><span data-stu-id="20ebd-179">tooimplement hello direct method on hello device, add hello following nested class toohello **App** class.</span></span> <span data-ttu-id="20ebd-180">Когда имитацию приложение hello получает toohello вызов **перезагрузить** прямой метод возвращает вызывающий объект подтверждения toohello и запускает поток tooprocess hello перезагрузите:</span><span class="sxs-lookup"><span data-stu-id="20ebd-180">When hello simulated app receives a call toohello **reboot** direct method, it returns an acknowledgement toohello caller and then starts a thread tooprocess hello reboot:</span></span>

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

1. <span data-ttu-id="20ebd-181">Измените сигнатуру hello объекта hello **основной** метод toothrow hello следующие исключения:</span><span class="sxs-lookup"><span data-stu-id="20ebd-181">Modify hello signature of hello **main** method toothrow hello following exceptions:</span></span>

    ```java
    public static void main(String[] args) throws IOException, URISyntaxException
    ```

1. <span data-ttu-id="20ebd-182">tooinstantiate **DeviceClient**, добавьте следующий код toohello hello **основной** метод:</span><span class="sxs-lookup"><span data-stu-id="20ebd-182">tooinstantiate a **DeviceClient**, add hello following code toohello **main** method:</span></span>

    ```java
    System.out.println("Starting device client sample...");
    client = new DeviceClient(connString, protocol);
    ```

1. <span data-ttu-id="20ebd-183">toostart прослушивание прямых вызовов, добавьте следующий код toohello hello **основной** метод:</span><span class="sxs-lookup"><span data-stu-id="20ebd-183">toostart listening for direct method calls, add hello following code toohello **main** method:</span></span>

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

1. <span data-ttu-id="20ebd-184">tooshut работу имитатора устройства hello, добавьте следующий код toohello hello **основной** метод:</span><span class="sxs-lookup"><span data-stu-id="20ebd-184">tooshut down hello device simulator, add hello following code toohello **main** method:</span></span>

    ```java
    System.out.println("Press any key tooexit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    scanner.close();
    client.close();
    System.out.println("Shutting down...");
    ```

1. <span data-ttu-id="20ebd-185">Сохраните и закройте файл simulated-device\src\main\java\com\mycompany\app\App.java hello.</span><span class="sxs-lookup"><span data-stu-id="20ebd-185">Save and close hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="20ebd-186">Построение hello **имитируемые устройства** серверной части приложения и исправьте все ошибки.</span><span class="sxs-lookup"><span data-stu-id="20ebd-186">Build hello **simulated-device** back-end app and correct any errors.</span></span> <span data-ttu-id="20ebd-187">В командной строке перейдите папка имитируемые устройства toohello и выполнения hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="20ebd-187">At your command prompt, navigate toohello simulated-device folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a><span data-ttu-id="20ebd-188">Запускайте приложения hello</span><span class="sxs-lookup"><span data-stu-id="20ebd-188">Run hello apps</span></span>

<span data-ttu-id="20ebd-189">Теперь вы находитесь toorun готовности приложения hello.</span><span class="sxs-lookup"><span data-stu-id="20ebd-189">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="20ebd-190">В командной строке в папке имитируемые устройства hello выполните следующие команды toobegin Ожидание перезагрузки вызовы методов из вашего центра IoT hello:</span><span class="sxs-lookup"><span data-stu-id="20ebd-190">At a command prompt in hello simulated-device folder, run hello following command toobegin listening for reboot method calls from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Центр IoT Java имитируемые устройства toolisten приложения для прямых вызовов перезагрузки][1]

1. <span data-ttu-id="20ebd-192">В командной строке в папке hello перезагрузки триггер выполните следующую метод перезагрузки hello toocall команды на устройстве имитацию из вашего центра IoT hello:</span><span class="sxs-lookup"><span data-stu-id="20ebd-192">At a command prompt in hello trigger-reboot folder, run hello following command toocall hello reboot method on your simulated device from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Центр IoT Java службы приложения toocall hello перезагрузить прямой метод][2]

1. <span data-ttu-id="20ebd-194">имитированное устройство Hello в ответ отправляет toohello перезагрузки непосредственный вызов методов:</span><span class="sxs-lookup"><span data-stu-id="20ebd-194">hello simulated device responds toohello reboot direct method call:</span></span>

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