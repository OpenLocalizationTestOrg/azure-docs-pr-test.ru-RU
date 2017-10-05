---
title: "Начало работы с двойниками устройств Центра Интернета вещей (Java) | Документация Майкрософт"
description: "Добавление тегов и последующее использование запроса Центра Интернета вещей с помощью двойников устройств Центра Интернета вещей. Используйте пакет SDK для устройств Центра Интернета вещей Azure для Java, чтобы реализовать приложение устройства, и пакет SDK для служб Интернета вещей Azure для Java, чтобы реализовать приложение-службу, которое добавит теги и выполнит запрос к Центру Интернета вещей."
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
ms.openlocfilehash: 583cfcb9442c7be0a41aa1bc0f743bf8cf863665
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-device-twins-java"></a><span data-ttu-id="6e429-104">Начало работы с двойниками устройств (Java)</span><span class="sxs-lookup"><span data-stu-id="6e429-104">Get started with device twins (Java)</span></span>

[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="6e429-105">В этом руководстве создаются два консольных приложения для Java:</span><span class="sxs-lookup"><span data-stu-id="6e429-105">In this tutorial, you create two Java console apps:</span></span>

* <span data-ttu-id="6e429-106">**add-tags-query** — внутреннее приложение Java, которое добавляет теги и выполняет запросы к двойникам устройств.</span><span class="sxs-lookup"><span data-stu-id="6e429-106">**add-tags-query**, a Java back-end app that adds tags and queries device twins.</span></span>
* <span data-ttu-id="6e429-107">**simulated-device** — это приложение устройства Java, которое подключается к Центру Интернета вещей и сообщает о его условии подключения c помощью сообщаемого свойства.</span><span class="sxs-lookup"><span data-stu-id="6e429-107">**simulated-device**, a Java device app that that connects to your IoT hub and reports its connectivity condition using a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="6e429-108">Статья [Общие сведения о пакетах SDK для Azure IoT и их использование](iot-hub-devguide-sdks.md) содержит сведения о разных пакетах SDK для Интернета вещей Azure, с помощью которых можно создать приложения для устройств и внутренние приложения.</span><span class="sxs-lookup"><span data-stu-id="6e429-108">The article [Azure IoT SDKs](iot-hub-devguide-sdks.md) provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>

<span data-ttu-id="6e429-109">Для работы с этим руководством необходимы указанные ниже компоненты.</span><span class="sxs-lookup"><span data-stu-id="6e429-109">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="6e429-110">Последняя версия [пакета SDK для Java SE 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="6e429-110">The latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="6e429-111">Maven 3</span><span class="sxs-lookup"><span data-stu-id="6e429-111">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="6e429-112">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="6e429-112">An active Azure account.</span></span> <span data-ttu-id="6e429-113">Если ее нет, можно создать [бесплатную учетную запись](http://azure.microsoft.com/pricing/free-trial/) всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="6e429-113">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="6e429-114">Если требуется создать удостоверение устройства программным способом, см. соответствующий раздел в разделе [Подключение устройства к Центру Интернета вещей с помощью Java](iot-hub-java-java-getstarted.md#create-a-device-identity).</span><span class="sxs-lookup"><span data-stu-id="6e429-114">If you prefer to create the device identity programmatically, read the corresponding section in the [Connect your device to your IoT hub using Java](iot-hub-java-java-getstarted.md#create-a-device-identity) article.</span></span>

## <a name="create-the-service-app"></a><span data-ttu-id="6e429-115">Создание приложения службы</span><span class="sxs-lookup"><span data-stu-id="6e429-115">Create the service app</span></span>

<span data-ttu-id="6e429-116">В этом разделе вы создадите приложение Java, которое добавляет метаданные расположения в виде тега в двойник устройства в Центре Интернета вещей, связанный с **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="6e429-116">In this section, you create a Java app that adds location metadata as a tag to the device twin in IoT Hub associated with **myDeviceId**.</span></span> <span data-ttu-id="6e429-117">Сначала приложение запрашивает в Центре Интернета вещей устройства, расположенные в США, а затем устройства, подключенные к сотовой сети.</span><span class="sxs-lookup"><span data-stu-id="6e429-117">The app first queries IoT hub for devices located in the US, and then for devices that report a cellular network connection.</span></span>

1. <span data-ttu-id="6e429-118">На компьютере разработки создайте пустую папку с названием `iot-java-twin-getstarted`.</span><span class="sxs-lookup"><span data-stu-id="6e429-118">On your development machine, create an empty folder called `iot-java-twin-getstarted`.</span></span>

1. <span data-ttu-id="6e429-119">В папке `iot-java-twin-getstarted` создайте проект Maven **add-tags-query**, выполнив следующую команду в командной строке.</span><span class="sxs-lookup"><span data-stu-id="6e429-119">In the `iot-java-twin-getstarted` folder, create a Maven project called **add-tags-query** using the following command at your command prompt.</span></span> <span data-ttu-id="6e429-120">Обратите внимание, что это одна длинная команда.</span><span class="sxs-lookup"><span data-stu-id="6e429-120">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=add-tags-query -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="6e429-121">В командной строке перейдите к папке `add-tags-query`.</span><span class="sxs-lookup"><span data-stu-id="6e429-121">At your command prompt, navigate to the `add-tags-query` folder.</span></span>

1. <span data-ttu-id="6e429-122">Откройте в текстовом редакторе файл `pom.xml` из папки `add-tags-query` и добавьте зависимости, приведенные ниже, в узел **dependencies**.</span><span class="sxs-lookup"><span data-stu-id="6e429-122">Using a text editor, open the `pom.xml` file in the `add-tags-query` folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="6e429-123">Эта зависимость позволит вам использовать в приложении пакет **iot-service-client** для обмена данными с Центром Интернета вещей:</span><span class="sxs-lookup"><span data-stu-id="6e429-123">This dependency enables you to use the **iot-service-client** package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="6e429-124">Наличие последней версии пакета **iot-service-client** можно проверить с помощью [поиска Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="6e429-124">You can check for the latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="6e429-125">Добавьте следующий узел, **build**, после узла **dependencies**.</span><span class="sxs-lookup"><span data-stu-id="6e429-125">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="6e429-126">Эта конфигурация дает указание Maven использовать Java версии 1.8 для создания приложения:</span><span class="sxs-lookup"><span data-stu-id="6e429-126">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

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

1. <span data-ttu-id="6e429-127">Сохраните и закройте файл `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="6e429-127">Save and close the `pom.xml` file.</span></span>

1. <span data-ttu-id="6e429-128">Откройте в текстовом редакторе файл `add-tags-query\src\main\java\com\mycompany\app\App.java`.</span><span class="sxs-lookup"><span data-stu-id="6e429-128">Using a text editor, open the `add-tags-query\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="6e429-129">Добавьте в файл следующие инструкции **import** .</span><span class="sxs-lookup"><span data-stu-id="6e429-129">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.*;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.HashSet;
    import java.util.Set;
    ```

1. <span data-ttu-id="6e429-130">Добавьте в класс **App** .</span><span class="sxs-lookup"><span data-stu-id="6e429-130">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="6e429-131">Замените `{youriothubconnectionstring}` строкой подключения к вашему Центру Интернета вещей, которую вы записали, выполняя инструкции в разделе *Создание Центра Интернета вещей*:</span><span class="sxs-lookup"><span data-stu-id="6e429-131">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in the *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String region = "US";
    public static final String plant = "Redmond43";
    ```

1. <span data-ttu-id="6e429-132">Обновите подпись метода **main**, добавив следующее предложение `throws`:</span><span class="sxs-lookup"><span data-stu-id="6e429-132">Update the **main** method signature to include the following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws IOException
    ```

1. <span data-ttu-id="6e429-133">Добавьте следующий код в метод **main** для создания объектов **DeviceTwin** и **DeviceTwinDevice**.</span><span class="sxs-lookup"><span data-stu-id="6e429-133">Add the following code to the **main** method to create the **DeviceTwin** and **DeviceTwinDevice** objects.</span></span> <span data-ttu-id="6e429-134">Объект **DeviceTwin** обрабатывает взаимодействие с вашим Центром Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="6e429-134">The **DeviceTwin** object handles the communication with your IoT hub.</span></span> <span data-ttu-id="6e429-135">Объект **DeviceTwinDevice** представляет двойник устройства, его свойства и теги:</span><span class="sxs-lookup"><span data-stu-id="6e429-135">The **DeviceTwinDevice** object represents the device twin with its properties and tags:</span></span>

    ```java
    // Get the DeviceTwin and DeviceTwinDevice objects
    DeviceTwin twinClient = DeviceTwin.createFromConnectionString(iotHubConnectionString);
    DeviceTwinDevice device = new DeviceTwinDevice(deviceId);
    ```

1. <span data-ttu-id="6e429-136">Добавьте следующий блок `try/catch` в метод **main**:</span><span class="sxs-lookup"><span data-stu-id="6e429-136">Add the following `try/catch` block to the **main** method:</span></span>

    ```java
    try {
      // Code goes here
    } catch (IotHubException e) {
      System.out.println(e.getMessage());
    } catch (IOException e) {
      System.out.println(e.getMessage());
    }
    ```

1. <span data-ttu-id="6e429-137">Чтобы обновить теги **region** и **plant** двойника устройства, добавьте следующий код в блок `try`:</span><span class="sxs-lookup"><span data-stu-id="6e429-137">To update the **region** and **plant** device twin tags in your device twin, add the following code in the `try` block:</span></span>

    ```java
    // Get the device twin from IoT Hub
    System.out.println("Device twin before update:");
    twinClient.getTwin(device);
    System.out.println(device);

    // Update device twin tags if they are different
    // from the existing values
    String currentTags = device.tagsToString();
    if ((!currentTags.contains("region=" + region) && !currentTags.contains("plant=" + plant))) {
      // Create the tags and attach them to the DeviceTwinDevice object
      Set<Pair> tags = new HashSet<Pair>();
      tags.add(new Pair("region", region));
      tags.add(new Pair("plant", plant));
      device.setTags(tags);

      // Update the device twin in IoT Hub
      System.out.println("Updating device twin");
      twinClient.updateTwin(device);
    }

    // Retrieve the device twin with the tag values from IoT Hub
    System.out.println("Device twin after update:");
    twinClient.getTwin(device);
    System.out.println(device);
    ```

1. <span data-ttu-id="6e429-138">Чтобы отправить запрос к двойникам устройств в Центре Интернета вещей, добавьте следующий код в блок `try` после кода, добавленного на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="6e429-138">To query the device twins in IoT hub, add the following code to the `try` block after the code you added in the previous step.</span></span> <span data-ttu-id="6e429-139">Код выполняет два запроса.</span><span class="sxs-lookup"><span data-stu-id="6e429-139">The code runs two queries.</span></span> <span data-ttu-id="6e429-140">Каждый запрос возвращает не более 100 устройств:</span><span class="sxs-lookup"><span data-stu-id="6e429-140">Each query returns a maximum of 100 devices:</span></span>

    ```java
    // Query the device twins in IoT Hub
    System.out.println("Devices in Redmond:");

    // Construct the query
    SqlQuery sqlQuery = SqlQuery.createSqlQuery("*", SqlQuery.FromType.DEVICES, "tags.plant='Redmond43'", null);

    // Run the query, returning a maximum of 100 devices
    Query twinQuery = twinClient.queryTwin(sqlQuery.getQuery(), 100);
    while (twinClient.hasNextDeviceTwin(twinQuery)) {
      DeviceTwinDevice d = twinClient.getNextDeviceTwin(twinQuery);
      System.out.println(d.getDeviceId());
    }

    System.out.println("Devices in Redmond using a cellular network:");

    // Construct the query
    sqlQuery = SqlQuery.createSqlQuery("*", SqlQuery.FromType.DEVICES, "tags.plant='Redmond43' AND properties.reported.connectivityType = 'cellular'", null);

    // Run the query, returning a maximum of 100 devices
    twinQuery = twinClient.queryTwin(sqlQuery.getQuery(), 3);
    while (twinClient.hasNextDeviceTwin(twinQuery)) {
      DeviceTwinDevice d = twinClient.getNextDeviceTwin(twinQuery);
      System.out.println(d.getDeviceId());
    }
    ```

1. <span data-ttu-id="6e429-141">Сохраните и закройте файл `add-tags-query\src\main\java\com\mycompany\app\App.java`.</span><span class="sxs-lookup"><span data-stu-id="6e429-141">Save and close the `add-tags-query\src\main\java\com\mycompany\app\App.java` file</span></span>

1. <span data-ttu-id="6e429-142">Создайте приложение **add-tags-query** и исправьте все ошибки.</span><span class="sxs-lookup"><span data-stu-id="6e429-142">Build the **add-tags-query** app and correct any errors.</span></span> <span data-ttu-id="6e429-143">В командной строке перейдите к папке `add-tags-query` и выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="6e429-143">At your command prompt, navigate to the `add-tags-query` folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a><span data-ttu-id="6e429-144">Создание приложения устройства</span><span class="sxs-lookup"><span data-stu-id="6e429-144">Create a device app</span></span>

<span data-ttu-id="6e429-145">В этом разделе вы создадите консольное приложение Java, которое задает значение сообщаемого свойства, отправляемое в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="6e429-145">In this section, you create a Java console app that sets a reported property value that is sent to IoT Hub.</span></span>

1. <span data-ttu-id="6e429-146">В папке `iot-java-twin-getstarted` создайте проект Maven с именем **simulated-device**, выполнив в командной строке следующую команду.</span><span class="sxs-lookup"><span data-stu-id="6e429-146">In the `iot-java-twin-getstarted` folder, create a Maven project called **simulated-device** using the following command at your command prompt.</span></span> <span data-ttu-id="6e429-147">Обратите внимание, что это одна длинная команда.</span><span class="sxs-lookup"><span data-stu-id="6e429-147">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="6e429-148">В командной строке перейдите к папке `simulated-device`.</span><span class="sxs-lookup"><span data-stu-id="6e429-148">At your command prompt, navigate to the `simulated-device` folder.</span></span>

1. <span data-ttu-id="6e429-149">Откройте в текстовом редакторе файл `pom.xml` из папки `simulated-device` и добавьте зависимости, приведенные ниже, в узел **dependencies**.</span><span class="sxs-lookup"><span data-stu-id="6e429-149">Using a text editor, open the `pom.xml` file in the `simulated-device` folder and add the following dependencies to the **dependencies** node.</span></span> <span data-ttu-id="6e429-150">Эта зависимость позволит вам использовать в приложении пакет **iot-device-client** для обмена данными с Центром Интернета вещей:</span><span class="sxs-lookup"><span data-stu-id="6e429-150">This dependency enables you to use the **iot-device-client** package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="6e429-151">Наличие последней версии пакета **iot-device-client** можно проверить с помощью [поиска Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="6e429-151">You can check for the latest version of **iot-device-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="6e429-152">Добавьте следующий узел, **build**, после узла **dependencies**.</span><span class="sxs-lookup"><span data-stu-id="6e429-152">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="6e429-153">Эта конфигурация дает указание Maven использовать Java версии 1.8 для создания приложения:</span><span class="sxs-lookup"><span data-stu-id="6e429-153">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

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

1. <span data-ttu-id="6e429-154">Сохраните и закройте файл `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="6e429-154">Save and close the `pom.xml` file.</span></span>

1. <span data-ttu-id="6e429-155">Откройте в текстовом редакторе файл `simulated-device\src\main\java\com\mycompany\app\App.java`.</span><span class="sxs-lookup"><span data-stu-id="6e429-155">Using a text editor, open the `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="6e429-156">Добавьте в файл следующие инструкции **import** .</span><span class="sxs-lookup"><span data-stu-id="6e429-156">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="6e429-157">Добавьте в класс **App** .</span><span class="sxs-lookup"><span data-stu-id="6e429-157">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="6e429-158">Замените значение `{youriothubname}` именем Центра Интернета вещей, а `{yourdevicekey}` — значением ключа устройства, сформированным при работе с разделом *Создание удостоверения устройства*:</span><span class="sxs-lookup"><span data-stu-id="6e429-158">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with the device key value you generated in the *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myDeviceId";
    ```

    <span data-ttu-id="6e429-159">При создании экземпляра объекта **DeviceClient** в этом примере приложения используется переменная **protocol**.</span><span class="sxs-lookup"><span data-stu-id="6e429-159">This sample app uses the **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="6e429-160">Сейчас использование функций двойников устройств возможно только с протоколом MQTT.</span><span class="sxs-lookup"><span data-stu-id="6e429-160">Currently, to use device twin features you must use the MQTT protocol.</span></span>

1. <span data-ttu-id="6e429-161">Добавьте в конец метода **main** следующий код, чтобы:</span><span class="sxs-lookup"><span data-stu-id="6e429-161">Add the following code to the **main** method to:</span></span>
    * <span data-ttu-id="6e429-162">Создать клиент устройства для взаимодействия с Центром Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="6e429-162">Create a device client to communicate with IoT Hub.</span></span>
    * <span data-ttu-id="6e429-163">Создать объект **Device** для хранения свойств двойника устройства.</span><span class="sxs-lookup"><span data-stu-id="6e429-163">Create a **Device** object to store the device twin properties.</span></span>

    ```java
    DeviceClient client = new DeviceClient(connString, protocol);

    // Create a Device object to store the device twin properties
    Device dataCollector = new Device() {
      // Print details when a property value changes
      @Override
      public void PropertyCall(String propertyKey, Object propertyValue, Object context) {
        System.out.println(propertyKey + " changed to " + propertyValue);
      }
    };
    ```

1. <span data-ttu-id="6e429-164">Добавьте следующий код в метод **main**, чтобы создать сообщаемое свойство **connectivityType** и отправить его в Центр Интернета вещей:</span><span class="sxs-lookup"><span data-stu-id="6e429-164">Add the following code to the **main** method to create a **connectivityType** reported property and send it to IoT Hub:</span></span>

    ```java
    try {
      // Open the DeviceClient and start the device twin services.
      client.open();
      client.startDeviceTwin(new DeviceTwinStatusCallBack(), null, dataCollector, null);

      // Create a reported property and send it to your IoT hub.
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

1. <span data-ttu-id="6e429-165">Добавьте в конец метода **main** следующий код:</span><span class="sxs-lookup"><span data-stu-id="6e429-165">Add the following code to the end of the **main** method.</span></span> <span data-ttu-id="6e429-166">Во время ожидания нажатия клавиши **ВВОД** Центр Интернета вещей сообщает состояние операций двойника устройства:</span><span class="sxs-lookup"><span data-stu-id="6e429-166">Waiting for the **Enter** key allows time for IoT Hub to report the status of the device twin operations:</span></span>

    ```java
    System.out.println("Press any key to exit...");

    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();

    dataCollector.clean();
    client.close();
    ```

1. <span data-ttu-id="6e429-167">Сохраните и закройте файл `simulated-device\src\main\java\com\mycompany\app\App.java`.</span><span class="sxs-lookup"><span data-stu-id="6e429-167">Save and close the `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="6e429-168">Создайте приложение **simulated-device** и исправьте все ошибки.</span><span class="sxs-lookup"><span data-stu-id="6e429-168">Build the **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="6e429-169">В командной строке перейдите к папке `simulated-device` и выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="6e429-169">At your command prompt, navigate to the `simulated-device` folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-the-apps"></a><span data-ttu-id="6e429-170">Запуск приложений</span><span class="sxs-lookup"><span data-stu-id="6e429-170">Run the apps</span></span>

<span data-ttu-id="6e429-171">Теперь все готово к запуску консоли приложений.</span><span class="sxs-lookup"><span data-stu-id="6e429-171">You are now ready to run the console apps.</span></span>

1. <span data-ttu-id="6e429-172">В командной строке в папке `add-tags-query` выполните следующую команду, чтобы запустить приложение службы **add-tags-query**:</span><span class="sxs-lookup"><span data-stu-id="6e429-172">At a command prompt in the `add-tags-query` folder, run the following command to run the **add-tags-query** service app:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Обновление значений тегов и выполнение запросов устройств с помощью приложения службы Центра Интернета вещей](media/iot-hub-java-java-twin-getstarted/service-app-1.png)

    <span data-ttu-id="6e429-174">Вы увидите теги **plant** и **region**, добавленные в двойник устройства.</span><span class="sxs-lookup"><span data-stu-id="6e429-174">You can see the **plant** and **region** tags added to the device twin.</span></span> <span data-ttu-id="6e429-175">Первый запрос возвращает устройство, а второй — нет.</span><span class="sxs-lookup"><span data-stu-id="6e429-175">The first query returns your device, but the second does not.</span></span>

1. <span data-ttu-id="6e429-176">В командной строке в папке `simulated-device` выполните следующую команду, чтобы добавить в двойник устройства сообщаемое свойство **connectivityType**:</span><span class="sxs-lookup"><span data-stu-id="6e429-176">At a command prompt in the `simulated-device` folder, run the following command to add the **connectivityType** reported property to the device twin:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Клиент устройства добавляет сообщаемое свойство **connectivityType**](media/iot-hub-java-java-twin-getstarted/device-app-1.png)

1. <span data-ttu-id="6e429-178">В командной строке в папке `add-tags-query` выполните следующую команду, чтобы повторно запустить приложение службы **add-tags-query**:</span><span class="sxs-lookup"><span data-stu-id="6e429-178">At a command prompt in the `add-tags-query` folder, run the following command to run the **add-tags-query** service app a second time:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Обновление значений тегов и выполнение запросов устройств с помощью приложения службы Центра Интернета вещей](media/iot-hub-java-java-twin-getstarted/service-app-2.png)

    <span data-ttu-id="6e429-180">Теперь устройство отправило свойство **connectivityType** в Центр Интернета вещей, и второй запрос возвращает устройство.</span><span class="sxs-lookup"><span data-stu-id="6e429-180">Now your device has sent the **connectivityType** property to IoT Hub, the second query returns your device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e429-181">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6e429-181">Next steps</span></span>

<span data-ttu-id="6e429-182">В этом руководстве мы настроили новый Центр Интернета вещей на портале Azure и создали удостоверение устройства в реестре удостоверений Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="6e429-182">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="6e429-183">Вы добавили метаданные устройства в качестве тегов из внутреннего приложения и написали код приложения устройства, чтобы сообщить сведения о подключении в двойнике устройства.</span><span class="sxs-lookup"><span data-stu-id="6e429-183">You added device metadata as tags from a back-end app, and wrote a device app to report device connectivity information in the device twin.</span></span> <span data-ttu-id="6e429-184">Вы также узнали, как запрашивать сведения о двойнике устройства, используя похожий на SQL язык запросов Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="6e429-184">You also learned how to query the device twin information using the SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="6e429-185">Ознакомьтесь со следующими материалами, чтобы узнать как:</span><span class="sxs-lookup"><span data-stu-id="6e429-185">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="6e429-186">отправить данные телеметрии с устройств (руководство [Подключение устройства к Центру Интернета вещей с помощью Java](iot-hub-java-java-getstarted.md));</span><span class="sxs-lookup"><span data-stu-id="6e429-186">Send telemetry from devices with the [Get started with IoT Hub](iot-hub-java-java-getstarted.md) tutorial.</span></span>
* <span data-ttu-id="6e429-187">управлять устройствами в интерактивном режиме, например включить вентилятор из управляемого пользователем приложения (руководство [Использование прямых методов (Java)](iot-hub-java-java-direct-methods.md)).</span><span class="sxs-lookup"><span data-stu-id="6e429-187">Control devices interactively (such as turning on a fan from a user-controlled app) with the [Use direct methods](iot-hub-java-java-direct-methods.md) tutorial.</span></span>

<!-- Images. -->
[7]: ./media/iot-hub-java-java-twin-getstarted/invoke-method.png
[8]: ./media/iot-hub-java-java-twin-getstarted/device-listen.png
[9]: ./media/iot-hub-java-java-twin-getstarted/device-respond.png

<!-- Links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
