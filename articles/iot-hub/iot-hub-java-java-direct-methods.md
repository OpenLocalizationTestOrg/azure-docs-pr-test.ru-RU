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
# <a name="use-direct-methods-java"></a><span data-ttu-id="14a60-104">Использование прямых методов (Java)</span><span class="sxs-lookup"><span data-stu-id="14a60-104">Use direct methods (Java)</span></span>

[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="14a60-105">В этом руководстве создаются два консольных приложения для Java:</span><span class="sxs-lookup"><span data-stu-id="14a60-105">In this tutorial, you create two Java console apps:</span></span>

* <span data-ttu-id="14a60-106">**Invoke-direct метод**, Java серверная часть приложения, который вызывает метод в приложение hello имитированное устройство и отображает hello ответа.</span><span class="sxs-lookup"><span data-stu-id="14a60-106">**invoke-direct-method**, a Java back-end app that calls a method in hello simulated device app and displays hello response.</span></span>
* <span data-ttu-id="14a60-107">**имитируемые устройства**, приложения Java, которое имитирует устройство соединение центра IoT tooyour с помощью создания удостоверения устройства hello.</span><span class="sxs-lookup"><span data-stu-id="14a60-107">**simulated-device**, a Java app that simulates a device connecting tooyour IoT hub with hello device identity you create.</span></span> <span data-ttu-id="14a60-108">Это приложение отвечает toohello напрямую вызван из hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="14a60-108">This app responds toohello direct invoked from hello back end.</span></span>

> [!NOTE]
> <span data-ttu-id="14a60-109">Сведения о hello пакетов SDK, которые можно использовать toorun toobuild приложений на устройствах и серверной части вашего решения см. в разделе [пакеты SDK Azure IoT][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="14a60-109">For information about hello SDKs that you can use toobuild applications toorun on devices and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="14a60-110">toocomplete этого учебника, необходимо:</span><span class="sxs-lookup"><span data-stu-id="14a60-110">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="14a60-111">Java SE 8.</span><span class="sxs-lookup"><span data-stu-id="14a60-111">Java SE 8.</span></span> <br/> <span data-ttu-id="14a60-112">[Подготовка среды разработки] [ lnk-dev-setup] описывает способ tooinstall Java для этого учебника в Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="14a60-112">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Java for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="14a60-113">Maven 3.</span><span class="sxs-lookup"><span data-stu-id="14a60-113">Maven 3.</span></span>  <br/> <span data-ttu-id="14a60-114">[Подготовка среды разработки] [ lnk-dev-setup] описывает способ tooinstall [Maven] [ lnk-maven] для этого учебника в Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="14a60-114">[Prepare your development environment][lnk-dev-setup] describes how tooinstall [Maven][lnk-maven] for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="14a60-115">[Node.js версии 0.10.0 или более поздней](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="14a60-115">[Node.js version 0.10.0 or later](http://nodejs.org).</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="14a60-116">Создание приложения виртуального устройства</span><span class="sxs-lookup"><span data-stu-id="14a60-116">Create a simulated device app</span></span>

<span data-ttu-id="14a60-117">В этом разделе создайте консольное приложение Java, которое отвечает tooa методе, вызванном обратно в решение hello end.</span><span class="sxs-lookup"><span data-stu-id="14a60-117">In this section, you create a Java console app that responds tooa method called by hello solution back end.</span></span>

1. <span data-ttu-id="14a60-118">Создайте пустую папку с именем iot-java-direct-method.</span><span class="sxs-lookup"><span data-stu-id="14a60-118">Create an empty folder called iot-java-direct-method.</span></span>

1. <span data-ttu-id="14a60-119">В папке iot java непосредственного метода hello, создайте проект Maven с именем **имитируемые устройства** с помощью hello следующую команду в командной строке.</span><span class="sxs-lookup"><span data-stu-id="14a60-119">In hello iot-java-direct-method folder, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="14a60-120">Hello следующую команду — один, long команда:</span><span class="sxs-lookup"><span data-stu-id="14a60-120">hello following command is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="14a60-121">В командной строке перейдите папку toohello имитируемые устройства.</span><span class="sxs-lookup"><span data-stu-id="14a60-121">At your command prompt, navigate toohello simulated-device folder.</span></span>

1. <span data-ttu-id="14a60-122">В текстовом редакторе, откройте файл pom.xml hello в папке имитируемые устройства hello и добавьте следующие зависимости toohello hello **зависимости** узла.</span><span class="sxs-lookup"><span data-stu-id="14a60-122">Using a text editor, open hello pom.xml file in hello simulated-device folder and add hello following dependencies toohello **dependencies** node.</span></span> <span data-ttu-id="14a60-123">Эта зависимость позволяет вам toouse hello клиента для устройства iot пакета в toocommunicate вашего приложения с вашего центра IoT:</span><span class="sxs-lookup"><span data-stu-id="14a60-123">This dependency enables you toouse hello iot-device-client package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="14a60-124">Вы можете проверить наличие hello последнюю версию **клиента для устройства iot** с помощью [поиска Maven][lnk-maven-device-search].</span><span class="sxs-lookup"><span data-stu-id="14a60-124">You can check for hello latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

1. <span data-ttu-id="14a60-125">Добавьте следующее hello **построения** узел после hello **зависимости** узла.</span><span class="sxs-lookup"><span data-stu-id="14a60-125">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="14a60-126">Эта конфигурация указывает, что приложение hello 1,8 toobuild Java toouse Maven:</span><span class="sxs-lookup"><span data-stu-id="14a60-126">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="14a60-127">Сохраните и закройте файл pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="14a60-127">Save and close hello pom.xml file.</span></span>

1. <span data-ttu-id="14a60-128">В текстовом редакторе откройте файл simulated-device\src\main\java\com\mycompany\app\App.java hello.</span><span class="sxs-lookup"><span data-stu-id="14a60-128">Using a text editor, open hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="14a60-129">Добавьте следующее hello **импорта** toohello файл инструкций:</span><span class="sxs-lookup"><span data-stu-id="14a60-129">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="14a60-130">Добавьте следующие переменные уровня класса toohello hello **приложения** класса.</span><span class="sxs-lookup"><span data-stu-id="14a60-130">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="14a60-131">Замена `{youriothubname}` на название концентратора IoT и `{yourdevicekey}` со значением ключа устройства hello созданный hello *создать удостоверение устройства* раздела:</span><span class="sxs-lookup"><span data-stu-id="14a60-131">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with hello device key value you generated in hello *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myDeviceId";
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    <span data-ttu-id="14a60-132">Этот пример приложения использует hello **протокола** переменной, когда он создает **DeviceClient** объекта.</span><span class="sxs-lookup"><span data-stu-id="14a60-132">This sample app uses hello **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="14a60-133">В настоящее время toouse направлять методы, которые необходимо использовать протокол MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="14a60-133">Currently, toouse direct methods you must use hello MQTT protocol.</span></span>

1. <span data-ttu-id="14a60-134">tooreturn центр IoT для tooyour код состояния, добавьте следующее hello вложенных классов toohello **приложения** класса:</span><span class="sxs-lookup"><span data-stu-id="14a60-134">tooreturn a status code tooyour IoT hub, add hello following nested class toohello **App** class:</span></span>

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded toodevice method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="14a60-135">toohandle hello прямых вызовов из серверной части решения hello, добавьте следующее hello вложенных классов toohello **приложения** класса:</span><span class="sxs-lookup"><span data-stu-id="14a60-135">toohandle hello direct method invocations from hello solution back end, add hello following nested class toohello **App** class:</span></span>

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

1. <span data-ttu-id="14a60-136">toocreate **DeviceClient** и прослушивать прямых вызовов, добавьте **основной** toohello метод **приложения** класса:</span><span class="sxs-lookup"><span data-stu-id="14a60-136">toocreate a **DeviceClient** and listen for direct method invocations, add a **main** method toohello **App** class:</span></span>

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

1. <span data-ttu-id="14a60-137">Сохраните и закройте файл simulated-device\src\main\java\com\mycompany\app\App.java hello</span><span class="sxs-lookup"><span data-stu-id="14a60-137">Save and close hello simulated-device\src\main\java\com\mycompany\app\App.java file</span></span>

1. <span data-ttu-id="14a60-138">Построение hello **имитируемые устройства** приложения и исправьте все ошибки.</span><span class="sxs-lookup"><span data-stu-id="14a60-138">Build hello **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="14a60-139">В командной строке перейдите папка имитируемые устройства toohello и выполнения hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="14a60-139">At your command prompt, navigate toohello simulated-device folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="14a60-140">Вызов прямого метода на устройстве</span><span class="sxs-lookup"><span data-stu-id="14a60-140">Call a direct method on a device</span></span>

<span data-ttu-id="14a60-141">В этом разделе создайте консольное приложение Java, которое вызывает прямой метод, а затем отображает hello ответа.</span><span class="sxs-lookup"><span data-stu-id="14a60-141">In this section, you create a Java console app that invokes a direct method and then displays hello response.</span></span> <span data-ttu-id="14a60-142">Это консольное приложение подключается tooyour прямой метод центра IoT tooinvoke hello.</span><span class="sxs-lookup"><span data-stu-id="14a60-142">This console app connects tooyour IoT Hub tooinvoke hello direct method.</span></span>

1. <span data-ttu-id="14a60-143">В папке iot java непосредственного метода hello, создайте проект Maven с именем **вызвать direct метод** с помощью hello следующую команду в командной строке.</span><span class="sxs-lookup"><span data-stu-id="14a60-143">In hello iot-java-direct-method folder, create a Maven project called **invoke-direct-method** using hello following command at your command prompt.</span></span> <span data-ttu-id="14a60-144">Hello следующую команду — один, long команда:</span><span class="sxs-lookup"><span data-stu-id="14a60-144">hello following command is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=invoke-direct-method -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="14a60-145">В командной строке перейдите toohello invoke-direct метод папки.</span><span class="sxs-lookup"><span data-stu-id="14a60-145">At your command prompt, navigate toohello invoke-direct-method folder.</span></span>

1. <span data-ttu-id="14a60-146">В текстовом редакторе, откройте файл pom.xml hello в папке hello вызвать direct метод и добавьте следующие зависимости toohello hello **зависимости** узла.</span><span class="sxs-lookup"><span data-stu-id="14a60-146">Using a text editor, open hello pom.xml file in hello invoke-direct-method folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="14a60-147">Эта зависимость позволяет вам toouse hello клиента для службы iot пакета в toocommunicate вашего приложения с вашего центра IoT:</span><span class="sxs-lookup"><span data-stu-id="14a60-147">This dependency enables you toouse hello iot-service-client package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="14a60-148">Вы можете проверить наличие hello последнюю версию **клиента для службы iot** с помощью [поиска Maven][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="14a60-148">You can check for hello latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

1. <span data-ttu-id="14a60-149">Добавьте следующее hello **построения** узел после hello **зависимости** узла.</span><span class="sxs-lookup"><span data-stu-id="14a60-149">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="14a60-150">Эта конфигурация указывает, что приложение hello 1,8 toobuild Java toouse Maven:</span><span class="sxs-lookup"><span data-stu-id="14a60-150">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="14a60-151">Сохраните и закройте файл pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="14a60-151">Save and close hello pom.xml file.</span></span>

1. <span data-ttu-id="14a60-152">В текстовом редакторе откройте файл invoke-direct-method\src\main\java\com\mycompany\app\App.java hello.</span><span class="sxs-lookup"><span data-stu-id="14a60-152">Using a text editor, open hello invoke-direct-method\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="14a60-153">Добавьте следующее hello **импорта** toohello файл инструкций:</span><span class="sxs-lookup"><span data-stu-id="14a60-153">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceMethod;
    import com.microsoft.azure.sdk.iot.service.devicetwin.MethodResult;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.concurrent.TimeUnit;
    ```

1. <span data-ttu-id="14a60-154">Добавьте следующие переменные уровня класса toohello hello **приложения** класса.</span><span class="sxs-lookup"><span data-stu-id="14a60-154">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="14a60-155">Замените `{youriothubconnectionstring}` с IoT строку подключения к концентратору нижеприведенного hello *создать центр IoT* раздела:</span><span class="sxs-lookup"><span data-stu-id="14a60-155">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in hello *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String methodName = "writeLine";
    public static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    public static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    public static final String payload = "a line toobe written";
    ```

1. <span data-ttu-id="14a60-156">метод hello tooinvoke на hello имитированное устройство, добавьте следующие toohello кода hello **основной** метод:</span><span class="sxs-lookup"><span data-stu-id="14a60-156">tooinvoke hello method on hello simulated device, add hello following code toohello **main** method:</span></span>

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

1. <span data-ttu-id="14a60-157">Сохраните и закройте файл invoke-direct-method\src\main\java\com\mycompany\app\App.java hello</span><span class="sxs-lookup"><span data-stu-id="14a60-157">Save and close hello invoke-direct-method\src\main\java\com\mycompany\app\App.java file</span></span>

1. <span data-ttu-id="14a60-158">Построение hello **вызвать direct метод** приложения и исправьте все ошибки.</span><span class="sxs-lookup"><span data-stu-id="14a60-158">Build hello **invoke-direct-method** app and correct any errors.</span></span> <span data-ttu-id="14a60-159">В командной строке перейдите папку toohello вызвать direct метод и выполнения hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="14a60-159">At your command prompt, navigate toohello invoke-direct-method folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a><span data-ttu-id="14a60-160">Запускайте приложения hello</span><span class="sxs-lookup"><span data-stu-id="14a60-160">Run hello apps</span></span>

<span data-ttu-id="14a60-161">Теперь вы находитесь готов toorun hello консольных приложениях.</span><span class="sxs-lookup"><span data-stu-id="14a60-161">You are now ready toorun hello console apps.</span></span>

1. <span data-ttu-id="14a60-162">В командной строке в папке имитируемые устройства hello выполните следующие команды toobegin прослушивание вызовы методов из вашего центра IoT hello:</span><span class="sxs-lookup"><span data-stu-id="14a60-162">At a command prompt in hello simulated-device folder, run hello following command toobegin listening for method calls from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Центр IoT Java имитируемые устройства toolisten приложения для прямых вызовов][8]

1. <span data-ttu-id="14a60-164">В командной строке в папке вызвать direct метод hello запуск hello, следующая команда toocall метода для имитации устройства из вашего центра IoT:</span><span class="sxs-lookup"><span data-stu-id="14a60-164">At a command prompt in hello invoke-direct-method folder, run hello following command toocall a method on your simulated device from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Центр IoT Java службы приложения toocall прямой метод][7]

1. <span data-ttu-id="14a60-166">имитированное устройство Hello в ответ отправляет toohello непосредственный вызов методов:</span><span class="sxs-lookup"><span data-stu-id="14a60-166">hello simulated device responds toohello direct method call:</span></span>

    ![Приложение для имитации устройства центра IoT Java отвечает toohello непосредственный вызов методов][9]

## <a name="next-steps"></a><span data-ttu-id="14a60-168">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="14a60-168">Next steps</span></span>

<span data-ttu-id="14a60-169">В этом учебнике настроен центр IoT в hello портал Azure и затем создать удостоверение устройства в реестре удостоверений центра IoT hello.</span><span class="sxs-lookup"><span data-stu-id="14a60-169">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="14a60-170">Вы использовали этот устройства удостоверения tooenable hello имитируемые устройства приложения tooreact toomethods вызываемая hello облака.</span><span class="sxs-lookup"><span data-stu-id="14a60-170">You used this device identity tooenable hello simulated device app tooreact toomethods invoked by hello cloud.</span></span> <span data-ttu-id="14a60-171">Также было создано приложение, которое вызывает методы на устройстве hello и отображает hello ответа от устройства hello.</span><span class="sxs-lookup"><span data-stu-id="14a60-171">You also created an app that invokes methods on hello device and displays hello response from hello device.</span></span>

<span data-ttu-id="14a60-172">tooexplore см. другие сценарии IoT [расписание заданий на нескольких устройствах][lnk-devguide-jobs].</span><span class="sxs-lookup"><span data-stu-id="14a60-172">tooexplore other IoT scenarios, see [Schedule jobs on multiple devices][lnk-devguide-jobs].</span></span>

<span data-ttu-id="14a60-173">toolearn tooextend IoT решения и расписание метод вызывает на нескольких устройствах и разделе hello [расписание и широковещательных задания] [ lnk-tutorial-jobs] учебника.</span><span class="sxs-lookup"><span data-stu-id="14a60-173">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

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
