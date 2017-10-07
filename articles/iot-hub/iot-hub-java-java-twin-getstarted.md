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
# <a name="get-started-with-device-twins-java"></a><span data-ttu-id="441f9-104">Начало работы с двойниками устройств (Java)</span><span class="sxs-lookup"><span data-stu-id="441f9-104">Get started with device twins (Java)</span></span>

[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="441f9-105">В этом руководстве создаются два консольных приложения для Java:</span><span class="sxs-lookup"><span data-stu-id="441f9-105">In this tutorial, you create two Java console apps:</span></span>

* <span data-ttu-id="441f9-106">**add-tags-query** — внутреннее приложение Java, которое добавляет теги и выполняет запросы к двойникам устройств.</span><span class="sxs-lookup"><span data-stu-id="441f9-106">**add-tags-query**, a Java back-end app that adds tags and queries device twins.</span></span>
* <span data-ttu-id="441f9-107">**имитируемые устройства**, приложения для устройств Java, подключающуюся tooyour центр IoT и отчеты условия его подключения, с помощью свойства отчета.</span><span class="sxs-lookup"><span data-stu-id="441f9-107">**simulated-device**, a Java device app that that connects tooyour IoT hub and reports its connectivity condition using a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="441f9-108">статья Hello [пакеты SDK Azure IoT](iot-hub-devguide-sdks.md) предоставляет сведения о hello Azure IoT пакетов SDK, которые можно использовать toobuild устройства и серверной части приложения.</span><span class="sxs-lookup"><span data-stu-id="441f9-108">hello article [Azure IoT SDKs](iot-hub-devguide-sdks.md) provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>

<span data-ttu-id="441f9-109">toocomplete этого учебника, необходимо:</span><span class="sxs-lookup"><span data-stu-id="441f9-109">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="441f9-110">Здравствуйте, последняя версия [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="441f9-110">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="441f9-111">Maven 3</span><span class="sxs-lookup"><span data-stu-id="441f9-111">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="441f9-112">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="441f9-112">An active Azure account.</span></span> <span data-ttu-id="441f9-113">Если ее нет, можно создать [бесплатную учетную запись](http://azure.microsoft.com/pricing/free-trial/) всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="441f9-113">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="441f9-114">При желании удостоверения устройства hello toocreate программными средствами чтения hello соответствующий раздел в hello [подключиться с помощью Java концентратор IoT tooyour устройства](iot-hub-java-java-getstarted.md#create-a-device-identity) статьи.</span><span class="sxs-lookup"><span data-stu-id="441f9-114">If you prefer toocreate hello device identity programmatically, read hello corresponding section in hello [Connect your device tooyour IoT hub using Java](iot-hub-java-java-getstarted.md#create-a-device-identity) article.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="441f9-115">Создание приложения hello службы</span><span class="sxs-lookup"><span data-stu-id="441f9-115">Create hello service app</span></span>

<span data-ttu-id="441f9-116">В этом разделе создается приложение Java, которое добавляет расположение метаданных, что две устройства тег toohello в центр IoT, связанного с **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="441f9-116">In this section, you create a Java app that adds location metadata as a tag toohello device twin in IoT Hub associated with **myDeviceId**.</span></span> <span data-ttu-id="441f9-117">приложение Hello сначала запрашивается центр IoT для устройств, расположенных в hello США, а затем для устройств, сообщающие сотовой сети.</span><span class="sxs-lookup"><span data-stu-id="441f9-117">hello app first queries IoT hub for devices located in hello US, and then for devices that report a cellular network connection.</span></span>

1. <span data-ttu-id="441f9-118">На компьютере разработки создайте пустую папку с именем `iot-java-twin-getstarted`.</span><span class="sxs-lookup"><span data-stu-id="441f9-118">On your development machine, create an empty folder called `iot-java-twin-getstarted`.</span></span>

1. <span data-ttu-id="441f9-119">В hello `iot-java-twin-getstarted` папки, создайте проект с именем Maven **добавить теги запроса** hello следующую команду в командной строке с помощью.</span><span class="sxs-lookup"><span data-stu-id="441f9-119">In hello `iot-java-twin-getstarted` folder, create a Maven project called **add-tags-query** using hello following command at your command prompt.</span></span> <span data-ttu-id="441f9-120">Обратите внимание, что это одна длинная команда.</span><span class="sxs-lookup"><span data-stu-id="441f9-120">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=add-tags-query -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="441f9-121">В командной строке перейдите toohello `add-tags-query` папки.</span><span class="sxs-lookup"><span data-stu-id="441f9-121">At your command prompt, navigate toohello `add-tags-query` folder.</span></span>

1. <span data-ttu-id="441f9-122">В текстовом редакторе, откройте hello `pom.xml` файла в hello `add-tags-query` папки и добавьте следующие зависимости toohello hello **зависимости** узла.</span><span class="sxs-lookup"><span data-stu-id="441f9-122">Using a text editor, open hello `pom.xml` file in hello `add-tags-query` folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="441f9-123">Эта зависимость позволяет toouse hello **клиента для службы iot** пакет в toocommunicate вашего приложения с вашего центра IoT:</span><span class="sxs-lookup"><span data-stu-id="441f9-123">This dependency enables you toouse hello **iot-service-client** package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="441f9-124">Вы можете проверить наличие hello последнюю версию **клиента для службы iot** с помощью [Maven поиска](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="441f9-124">You can check for hello latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="441f9-125">Добавьте следующее hello **построения** узел после hello **зависимости** узла.</span><span class="sxs-lookup"><span data-stu-id="441f9-125">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="441f9-126">Эта конфигурация указывает, что приложение hello 1,8 toobuild Java toouse Maven:</span><span class="sxs-lookup"><span data-stu-id="441f9-126">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="441f9-127">Сохраните и закройте hello `pom.xml` файла.</span><span class="sxs-lookup"><span data-stu-id="441f9-127">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="441f9-128">В текстовом редакторе, откройте hello `add-tags-query\src\main\java\com\mycompany\app\App.java` файла.</span><span class="sxs-lookup"><span data-stu-id="441f9-128">Using a text editor, open hello `add-tags-query\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="441f9-129">Добавьте следующее hello **импорта** toohello файл инструкций:</span><span class="sxs-lookup"><span data-stu-id="441f9-129">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.*;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.HashSet;
    import java.util.Set;
    ```

1. <span data-ttu-id="441f9-130">Добавьте следующие переменные уровня класса toohello hello **приложения** класса.</span><span class="sxs-lookup"><span data-stu-id="441f9-130">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="441f9-131">Замените `{youriothubconnectionstring}` с IoT строку подключения к концентратору нижеприведенного hello *создать центр IoT* раздела:</span><span class="sxs-lookup"><span data-stu-id="441f9-131">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in hello *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String region = "US";
    public static final String plant = "Redmond43";
    ```

1. <span data-ttu-id="441f9-132">Обновление hello **основной** следующие hello tooinclude подпись метода `throws` предложения:</span><span class="sxs-lookup"><span data-stu-id="441f9-132">Update hello **main** method signature tooinclude hello following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws IOException
    ```

1. <span data-ttu-id="441f9-133">Добавьте следующий код toohello hello **основной** hello метод toocreate **DeviceTwin** и **DeviceTwinDevice** объектов.</span><span class="sxs-lookup"><span data-stu-id="441f9-133">Add hello following code toohello **main** method toocreate hello **DeviceTwin** and **DeviceTwinDevice** objects.</span></span> <span data-ttu-id="441f9-134">Hello **DeviceTwin** объект обрабатывает hello взаимодействие с вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="441f9-134">hello **DeviceTwin** object handles hello communication with your IoT hub.</span></span> <span data-ttu-id="441f9-135">Hello **DeviceTwinDevice** представляет hello двойных устройства с тегами и его свойства:</span><span class="sxs-lookup"><span data-stu-id="441f9-135">hello **DeviceTwinDevice** object represents hello device twin with its properties and tags:</span></span>

    ```java
    // Get hello DeviceTwin and DeviceTwinDevice objects
    DeviceTwin twinClient = DeviceTwin.createFromConnectionString(iotHubConnectionString);
    DeviceTwinDevice device = new DeviceTwinDevice(deviceId);
    ```

1. <span data-ttu-id="441f9-136">Добавьте следующее hello `try/catch` блокировать toohello **основной** метод:</span><span class="sxs-lookup"><span data-stu-id="441f9-136">Add hello following `try/catch` block toohello **main** method:</span></span>

    ```java
    try {
      // Code goes here
    } catch (IotHubException e) {
      System.out.println(e.getMessage());
    } catch (IOException e) {
      System.out.println(e.getMessage());
    }
    ```

1. <span data-ttu-id="441f9-137">tooupdate hello **область** и **растение** тегов двойных устройств в двойных вашего устройства, добавьте следующий код в hello hello `try` блока:</span><span class="sxs-lookup"><span data-stu-id="441f9-137">tooupdate hello **region** and **plant** device twin tags in your device twin, add hello following code in hello `try` block:</span></span>

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

1. <span data-ttu-id="441f9-138">tooquery близнецы устройства hello в центр IoT добавить следующий код toohello hello `try` блок после кода hello, добавленного на предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="441f9-138">tooquery hello device twins in IoT hub, add hello following code toohello `try` block after hello code you added in hello previous step.</span></span> <span data-ttu-id="441f9-139">Hello код выполняется два запроса.</span><span class="sxs-lookup"><span data-stu-id="441f9-139">hello code runs two queries.</span></span> <span data-ttu-id="441f9-140">Каждый запрос возвращает не более 100 устройств:</span><span class="sxs-lookup"><span data-stu-id="441f9-140">Each query returns a maximum of 100 devices:</span></span>

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

1. <span data-ttu-id="441f9-141">Сохраните и закройте hello `add-tags-query\src\main\java\com\mycompany\app\App.java` файла</span><span class="sxs-lookup"><span data-stu-id="441f9-141">Save and close hello `add-tags-query\src\main\java\com\mycompany\app\App.java` file</span></span>

1. <span data-ttu-id="441f9-142">Построение hello **добавить теги запроса** приложения и исправьте все ошибки.</span><span class="sxs-lookup"><span data-stu-id="441f9-142">Build hello **add-tags-query** app and correct any errors.</span></span> <span data-ttu-id="441f9-143">В командной строке перейдите toohello `add-tags-query` папки и выполнения hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="441f9-143">At your command prompt, navigate toohello `add-tags-query` folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a><span data-ttu-id="441f9-144">Создание приложения устройства</span><span class="sxs-lookup"><span data-stu-id="441f9-144">Create a device app</span></span>

<span data-ttu-id="441f9-145">В этом разделе создайте консольное приложение Java, которое задает значение свойства отчета, который отправляется tooIoT концентратора.</span><span class="sxs-lookup"><span data-stu-id="441f9-145">In this section, you create a Java console app that sets a reported property value that is sent tooIoT Hub.</span></span>

1. <span data-ttu-id="441f9-146">В hello `iot-java-twin-getstarted` папки, создайте проект с именем Maven **имитируемые устройства** с помощью hello следующую команду в командной строке.</span><span class="sxs-lookup"><span data-stu-id="441f9-146">In hello `iot-java-twin-getstarted` folder, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="441f9-147">Обратите внимание, что это одна длинная команда.</span><span class="sxs-lookup"><span data-stu-id="441f9-147">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="441f9-148">В командной строке перейдите toohello `simulated-device` папки.</span><span class="sxs-lookup"><span data-stu-id="441f9-148">At your command prompt, navigate toohello `simulated-device` folder.</span></span>

1. <span data-ttu-id="441f9-149">В текстовом редакторе, откройте hello `pom.xml` файла в hello `simulated-device` папки и добавьте следующие зависимости toohello hello **зависимости** узла.</span><span class="sxs-lookup"><span data-stu-id="441f9-149">Using a text editor, open hello `pom.xml` file in hello `simulated-device` folder and add hello following dependencies toohello **dependencies** node.</span></span> <span data-ttu-id="441f9-150">Эта зависимость позволяет toouse hello **клиента для устройства iot** пакет в toocommunicate вашего приложения с вашего центра IoT:</span><span class="sxs-lookup"><span data-stu-id="441f9-150">This dependency enables you toouse hello **iot-device-client** package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="441f9-151">Вы можете проверить наличие hello последнюю версию **клиента для устройства iot** с помощью [Maven поиска](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="441f9-151">You can check for hello latest version of **iot-device-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="441f9-152">Добавьте следующее hello **построения** узел после hello **зависимости** узла.</span><span class="sxs-lookup"><span data-stu-id="441f9-152">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="441f9-153">Эта конфигурация указывает, что приложение hello 1,8 toobuild Java toouse Maven:</span><span class="sxs-lookup"><span data-stu-id="441f9-153">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="441f9-154">Сохраните и закройте hello `pom.xml` файла.</span><span class="sxs-lookup"><span data-stu-id="441f9-154">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="441f9-155">В текстовом редакторе, откройте hello `simulated-device\src\main\java\com\mycompany\app\App.java` файла.</span><span class="sxs-lookup"><span data-stu-id="441f9-155">Using a text editor, open hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="441f9-156">Добавьте следующее hello **импорта** toohello файл инструкций:</span><span class="sxs-lookup"><span data-stu-id="441f9-156">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="441f9-157">Добавьте следующие переменные уровня класса toohello hello **приложения** класса.</span><span class="sxs-lookup"><span data-stu-id="441f9-157">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="441f9-158">Замена `{youriothubname}` на название концентратора IoT и `{yourdevicekey}` со значением ключа устройства hello созданный hello *создать удостоверение устройства* раздела:</span><span class="sxs-lookup"><span data-stu-id="441f9-158">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with hello device key value you generated in hello *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myDeviceId";
    ```

    <span data-ttu-id="441f9-159">Этот пример приложения использует hello **протокола** переменной, когда он создает **DeviceClient** объекта.</span><span class="sxs-lookup"><span data-stu-id="441f9-159">This sample app uses hello **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="441f9-160">В настоящее время toouse двойных функциями устройства необходимо использовать протокол MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="441f9-160">Currently, toouse device twin features you must use hello MQTT protocol.</span></span>

1. <span data-ttu-id="441f9-161">Добавьте следующий код toohello hello **основной** метода:</span><span class="sxs-lookup"><span data-stu-id="441f9-161">Add hello following code toohello **main** method to:</span></span>
    * <span data-ttu-id="441f9-162">Создайте toocommunicate клиента устройства с центром IoT.</span><span class="sxs-lookup"><span data-stu-id="441f9-162">Create a device client toocommunicate with IoT Hub.</span></span>
    * <span data-ttu-id="441f9-163">Создание **устройства** toostore hello устройства двойных свойства объекта.</span><span class="sxs-lookup"><span data-stu-id="441f9-163">Create a **Device** object toostore hello device twin properties.</span></span>

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

1. <span data-ttu-id="441f9-164">Добавьте следующий код toohello hello **основной** toocreate метод **connectivityType** сообщил свойство и отправлять их tooIoT концентратора:</span><span class="sxs-lookup"><span data-stu-id="441f9-164">Add hello following code toohello **main** method toocreate a **connectivityType** reported property and send it tooIoT Hub:</span></span>

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

1. <span data-ttu-id="441f9-165">Добавить следующий код toohello конец hello hello **основной** метод.</span><span class="sxs-lookup"><span data-stu-id="441f9-165">Add hello following code toohello end of hello **main** method.</span></span> <span data-ttu-id="441f9-166">Ожидание hello **ввод** ключ позволяет время центр IoT tooreport hello состояния операций двойных hello устройства:</span><span class="sxs-lookup"><span data-stu-id="441f9-166">Waiting for hello **Enter** key allows time for IoT Hub tooreport hello status of hello device twin operations:</span></span>

    ```java
    System.out.println("Press any key tooexit...");

    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();

    dataCollector.clean();
    client.close();
    ```

1. <span data-ttu-id="441f9-167">Сохраните и закройте hello `simulated-device\src\main\java\com\mycompany\app\App.java` файла.</span><span class="sxs-lookup"><span data-stu-id="441f9-167">Save and close hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="441f9-168">Построение hello **имитируемые устройства** приложения и исправьте все ошибки.</span><span class="sxs-lookup"><span data-stu-id="441f9-168">Build hello **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="441f9-169">В командной строке перейдите toohello `simulated-device` папки и выполнения hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="441f9-169">At your command prompt, navigate toohello `simulated-device` folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a><span data-ttu-id="441f9-170">Запускайте приложения hello</span><span class="sxs-lookup"><span data-stu-id="441f9-170">Run hello apps</span></span>

<span data-ttu-id="441f9-171">Теперь вы находитесь готов toorun hello консольных приложениях.</span><span class="sxs-lookup"><span data-stu-id="441f9-171">You are now ready toorun hello console apps.</span></span>

1. <span data-ttu-id="441f9-172">В командной строке в hello `add-tags-query` папку, следующая команда toorun hello hello **добавить теги запроса** службы приложений:</span><span class="sxs-lookup"><span data-stu-id="441f9-172">At a command prompt in hello `add-tags-query` folder, run hello following command toorun hello **add-tags-query** service app:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Центр IoT Java службы приложения tooupdate отметки значений и выполнять запросы устройства](media/iot-hub-java-java-twin-getstarted/service-app-1.png)

    <span data-ttu-id="441f9-174">Вы увидите hello **растение** и **область** теги добавлены две toohello устройства.</span><span class="sxs-lookup"><span data-stu-id="441f9-174">You can see hello **plant** and **region** tags added toohello device twin.</span></span> <span data-ttu-id="441f9-175">Hello первый запрос возвращает устройства, но hello второй — нет.</span><span class="sxs-lookup"><span data-stu-id="441f9-175">hello first query returns your device, but hello second does not.</span></span>

1. <span data-ttu-id="441f9-176">В командной строке в hello `simulated-device` папку, следующая команда tooadd hello hello **connectivityType** сообщил двойных устройства toohello свойство:</span><span class="sxs-lookup"><span data-stu-id="441f9-176">At a command prompt in hello `simulated-device` folder, run hello following command tooadd hello **connectivityType** reported property toohello device twin:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Добавляет клиент устройства Hello hello ** connectivityType ** сообщила, свойство](media/iot-hub-java-java-twin-getstarted/device-app-1.png)

1. <span data-ttu-id="441f9-178">В командной строке в hello `add-tags-query` папку, следующая команда toorun hello hello **добавить теги запроса** службы приложения еще раз:</span><span class="sxs-lookup"><span data-stu-id="441f9-178">At a command prompt in hello `add-tags-query` folder, run hello following command toorun hello **add-tags-query** service app a second time:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Центр IoT Java службы приложения tooupdate отметки значений и выполнять запросы устройства](media/iot-hub-java-java-twin-getstarted/service-app-2.png)

    <span data-ttu-id="441f9-180">Теперь устройство отправил hello **connectivityType** tooIoT свойство концентратора hello второй запрос возвращает устройство.</span><span class="sxs-lookup"><span data-stu-id="441f9-180">Now your device has sent hello **connectivityType** property tooIoT Hub, hello second query returns your device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="441f9-181">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="441f9-181">Next steps</span></span>

<span data-ttu-id="441f9-182">В этом учебнике настроен центр IoT в hello портал Azure и затем создать удостоверение устройства в реестре удостоверений центра IoT hello.</span><span class="sxs-lookup"><span data-stu-id="441f9-182">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="441f9-183">Добавить метаданные устройства как теги из серверной части приложения, а написал приложения tooreport устройства подключения сведений об устройстве в двойных hello устройства.</span><span class="sxs-lookup"><span data-stu-id="441f9-183">You added device metadata as tags from a back-end app, and wrote a device app tooreport device connectivity information in hello device twin.</span></span> <span data-ttu-id="441f9-184">Вы также узнали, как tooquery hello двойных сведений об устройстве, с помощью языка запросов SQL-подобного центра IoT hello.</span><span class="sxs-lookup"><span data-stu-id="441f9-184">You also learned how tooquery hello device twin information using hello SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="441f9-185">Hello используйте следующие ресурсы toolearn как для:</span><span class="sxs-lookup"><span data-stu-id="441f9-185">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="441f9-186">Отправка данных телеметрии с устройствами с помощью hello [приступить к работе с центром IoT](iot-hub-java-java-getstarted.md) учебника.</span><span class="sxs-lookup"><span data-stu-id="441f9-186">Send telemetry from devices with hello [Get started with IoT Hub](iot-hub-java-java-getstarted.md) tutorial.</span></span>
* <span data-ttu-id="441f9-187">Управление устройствами интерактивно (такие как включение вентилятор из управляемой пользователем приложения) с hello [использовать прямые методы](iot-hub-java-java-direct-methods.md) учебника.</span><span class="sxs-lookup"><span data-stu-id="441f9-187">Control devices interactively (such as turning on a fan from a user-controlled app) with hello [Use direct methods](iot-hub-java-java-direct-methods.md) tutorial.</span></span>

<!-- Images. -->
[7]: ./media/iot-hub-java-java-twin-getstarted/invoke-method.png
[8]: ./media/iot-hub-java-java-twin-getstarted/device-listen.png
[9]: ./media/iot-hub-java-java-twin-getstarted/device-respond.png

<!-- Links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
