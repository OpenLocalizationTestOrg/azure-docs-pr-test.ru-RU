---
title: "Приступая к работе с Центром Интернета вещей Azure (Java) | Документация Майкрософт"
description: "Узнайте, как отправлять сообщения из устройства на облако в Центр Интернета вещей Azure с помощью пакетов SDK Интернета вещей для Java. Создайте виртуальное устройство и приложения службы для регистрации устройства, отправки сообщений и чтения сообщений из Центра Интернета вещей."
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
ms.openlocfilehash: 707356a49970bcd76a55ee1b8a6fbddf6a6ba390
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="connect-your-device-to-your-iot-hub-using-java"></a><span data-ttu-id="acf8c-104">Подключение устройства к Центру Интернета вещей с помощью Java</span><span class="sxs-lookup"><span data-stu-id="acf8c-104">Connect your device to your IoT hub using Java</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="acf8c-105">В конце этого руководства у вас будет три консольных приложения Java:</span><span class="sxs-lookup"><span data-stu-id="acf8c-105">At the end of this tutorial, you have three Java console apps:</span></span>

* <span data-ttu-id="acf8c-106">**create-device-identity** — создает удостоверение устройства и соответствующий ключ безопасности для подключения к приложению устройства;</span><span class="sxs-lookup"><span data-stu-id="acf8c-106">**create-device-identity**, which creates a device identity and associated security key to connect your device app.</span></span>
* <span data-ttu-id="acf8c-107">**read-d2c-messages** — отображает данные телеметрии, отправляемые приложением устройства;</span><span class="sxs-lookup"><span data-stu-id="acf8c-107">**read-d2c-messages**, which displays the telemetry sent by your device app.</span></span>
* <span data-ttu-id="acf8c-108">**simulated-device** — подключается к Центру Интернета вещей с созданным ранее удостоверением устройства и отправляет сообщения телеметрии с частотой один раз в секунду по протоколу MQTT.</span><span class="sxs-lookup"><span data-stu-id="acf8c-108">**simulated-device**, which connects to your IoT hub with the device identity created earlier, and sends a telemetry message every second using the MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="acf8c-109">Статья о [пакетах SDK для Центра Интернета вещей Azure][lnk-hub-sdks] содержит сведения о средствах, которые можно использовать при создании приложений для мобильных устройств и разработке серверной части решения.</span><span class="sxs-lookup"><span data-stu-id="acf8c-109">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both apps to run on devices and your solution back end.</span></span>

<span data-ttu-id="acf8c-110">Для работы с этим учебником требуется:</span><span class="sxs-lookup"><span data-stu-id="acf8c-110">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="acf8c-111">Последняя версия [пакета SDK для Java SE 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="acf8c-111">The latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span> 
* [<span data-ttu-id="acf8c-112">Maven 3</span><span class="sxs-lookup"><span data-stu-id="acf8c-112">Maven 3</span></span>](https://maven.apache.org/install.html) 
* <span data-ttu-id="acf8c-113">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="acf8c-113">An active Azure account.</span></span> <span data-ttu-id="acf8c-114">Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="acf8c-114">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="acf8c-115">Наконец, запишите значение поля **Первичный ключ**.</span><span class="sxs-lookup"><span data-stu-id="acf8c-115">As a final step, make a note of the **Primary key** value.</span></span> <span data-ttu-id="acf8c-116">После этого щелкните **Конечные точки** и встроенную конечную точку **События**.</span><span class="sxs-lookup"><span data-stu-id="acf8c-116">Then click **Endpoints** and the **Events** built-in endpoint.</span></span> <span data-ttu-id="acf8c-117">В колонке **Свойства** запишите адрес значений полей **Event Hub-compatible name** (Имя, совместимое с концентратором событий) и **Event Hub-compatible endpoint** (Конечная точка, совместимая с концентратором событий).</span><span class="sxs-lookup"><span data-stu-id="acf8c-117">On the **Properties** blade, make a note of the **Event Hub-compatible name** and the **Event Hub-compatible endpoint** address.</span></span> <span data-ttu-id="acf8c-118">Эти три значения понадобятся при создании приложения **read-d2c-messages**.</span><span class="sxs-lookup"><span data-stu-id="acf8c-118">You need these three values when you create your **read-d2c-messages** app.</span></span>

![Колонка "Сообщения" Центра Интернета вещей на портале Azure][6]

<span data-ttu-id="acf8c-120">Теперь Центр Интернета вещей создан.</span><span class="sxs-lookup"><span data-stu-id="acf8c-120">You have now created your IoT hub.</span></span> <span data-ttu-id="acf8c-121">Вы создали все необходимое для работы с этим руководством: имя узла, строку подключения и первичный ключ Центра Интернета вещей, а также имя и конечную точку, совместимые с концентратором событий.</span><span class="sxs-lookup"><span data-stu-id="acf8c-121">You have the IoT Hub host name, IoT Hub connection string, IoT Hub Primary Key, Event Hub-compatible name, and Event Hub-compatible endpoint you need to complete this tutorial.</span></span>

## <a name="create-a-device-identity"></a><span data-ttu-id="acf8c-122">Создание удостоверения устройства</span><span class="sxs-lookup"><span data-stu-id="acf8c-122">Create a device identity</span></span>
<span data-ttu-id="acf8c-123">В этом разделе объясняется, как написать консольное приложение Java, которое создает удостоверение устройства в реестре удостоверений в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="acf8c-123">In this section, you create a Java console app that creates a device identity in the identity registry in your IoT hub.</span></span> <span data-ttu-id="acf8c-124">Устройство может подключиться к Центру Интернета вещей, только если в реестре удостоверений есть соответствующая запись.</span><span class="sxs-lookup"><span data-stu-id="acf8c-124">A device cannot connect to IoT hub unless it has an entry in the identity registry.</span></span> <span data-ttu-id="acf8c-125">Дополнительные сведения см. в разделе, посвященном **реестру удостоверений**, в [руководстве разработчика по Центру Интернета вещей Azure][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="acf8c-125">For more information, see the **Identity Registry** section of the [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="acf8c-126">При запуске этого консольного приложения создается уникальный идентификатор устройства и ключ, с помощью которых выполняется идентификация во время отправки сообщений из устройства в облако для Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="acf8c-126">When you run this console app, it generates a unique device ID and key that your device can use to identify itself when it sends device-to-cloud messages to IoT Hub.</span></span>

1. <span data-ttu-id="acf8c-127">Создайте пустую папку с именем iot-java-get-started.</span><span class="sxs-lookup"><span data-stu-id="acf8c-127">Create an empty folder called iot-java-get-started.</span></span> <span data-ttu-id="acf8c-128">В папке iot-java-get-started создайте проект Maven с именем **create-device-identity**, выполнив в командной строке следующую команду.</span><span class="sxs-lookup"><span data-stu-id="acf8c-128">In the iot-java-get-started folder, create a Maven project called **create-device-identity** using the following command at your command prompt.</span></span> <span data-ttu-id="acf8c-129">Обратите внимание, что это одна длинная команда.</span><span class="sxs-lookup"><span data-stu-id="acf8c-129">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=create-device-identity -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="acf8c-130">В командной строке перейдите к папке create-device-identity.</span><span class="sxs-lookup"><span data-stu-id="acf8c-130">At your command prompt, navigate to the create-device-identity folder.</span></span>

3. <span data-ttu-id="acf8c-131">Откройте в текстовом редакторе файл pom.xml из папки create-device-identity и добавьте приведенные ниже зависимости в узел **dependency** .</span><span class="sxs-lookup"><span data-stu-id="acf8c-131">Using a text editor, open the pom.xml file in the create-device-identity folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="acf8c-132">Эта зависимость позволяет использовать в приложении пакет iot-service-client:</span><span class="sxs-lookup"><span data-stu-id="acf8c-132">This dependency enables you to use the iot-service-client package in your app:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="acf8c-133">Наличие последней версии пакета **iot-service-client** можно проверить с помощью [поиска Maven][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="acf8c-133">You can check for the latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

4. <span data-ttu-id="acf8c-134">Сохраните и закройте файл pom.xml.</span><span class="sxs-lookup"><span data-stu-id="acf8c-134">Save and close the pom.xml file.</span></span>

5. <span data-ttu-id="acf8c-135">Откройте в текстовом редакторе файл create-device-identity\src\main\java\com\mycompany\app\App.jav.</span><span class="sxs-lookup"><span data-stu-id="acf8c-135">Using a text editor, open the create-device-identity\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="acf8c-136">Добавьте в файл следующие инструкции **import** .</span><span class="sxs-lookup"><span data-stu-id="acf8c-136">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;
    import com.microsoft.azure.sdk.iot.service.Device;
    import com.microsoft.azure.sdk.iot.service.RegistryManager;
   
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. <span data-ttu-id="acf8c-137">Добавьте следующие переменные уровня класса в класс **App**, заменив **{yourhubconnectionstring}** значениями, записанными ранее.</span><span class="sxs-lookup"><span data-stu-id="acf8c-137">Add the following class-level variables to the **App** class, replacing **{yourhubconnectionstring}** with the value your noted earlier:</span></span>

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "myFirstJavaDevice";
    ```
[!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

8. <span data-ttu-id="acf8c-138">Измените подпись метода **main** , чтобы включить исключения, указанные ниже.</span><span class="sxs-lookup"><span data-stu-id="acf8c-138">Modify the signature of the **main** method to include the exceptions as follows:</span></span>

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException, Exception
    ```

9. <span data-ttu-id="acf8c-139">Добавьте в текст метода **main** код, приведенный ниже.</span><span class="sxs-lookup"><span data-stu-id="acf8c-139">Add the following code as the body of the **main** method.</span></span> <span data-ttu-id="acf8c-140">Этот код создает устройство с именем *javadevice* в реестре удостоверений Центра Интернета вещей, если оно еще не создано.</span><span class="sxs-lookup"><span data-stu-id="acf8c-140">This code creates a device called *javadevice* in your IoT Hub identity registry if doesn't already exist.</span></span> <span data-ttu-id="acf8c-141">Затем он отобразит идентификатор устройства и ключ, которые понадобятся вам позже:</span><span class="sxs-lookup"><span data-stu-id="acf8c-141">It then displays the device ID and key that you need later:</span></span>

    ```java
    RegistryManager registryManager = RegistryManager.createFromConnectionString(connectionString);
RegistryManager registryManager = RegistryManager.createFromConnectionString(connectionString);

    // Create a device that's enabled by default, 
    // with an autogenerated key.
    Device device = Device.createFromId(deviceId, null, null);
    try {
      device = registryManager.addDevice(device);
    } catch (IotHubException iote) {
      // If the device already exists.
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
      // If the device already exists.
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

10. <span data-ttu-id="acf8c-142">Сохраните и закройте файл App.java.</span><span class="sxs-lookup"><span data-stu-id="acf8c-142">Save and close the App.java file.</span></span>

11. <span data-ttu-id="acf8c-143">Чтобы создать приложение **create-device-identity** с помощью Maven, выполните в командной строке в папке create-device-identity следующую команду:</span><span class="sxs-lookup"><span data-stu-id="acf8c-143">To build the **create-device-identity** app using Maven, execute the following command at the command prompt in the create-device-identity folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

12. <span data-ttu-id="acf8c-144">Чтобы выполнить приложение **create-device-identity** с помощью Maven, выполните в командной строке в папке create-device-identity следующую команду.</span><span class="sxs-lookup"><span data-stu-id="acf8c-144">To run the **create-device-identity** app using Maven, execute the following command at the command prompt in the create-device-identity folder:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

13. <span data-ttu-id="acf8c-145">Запишите значения полей **Идентификатор устройства** и **Device key** (Ключ устройства).</span><span class="sxs-lookup"><span data-stu-id="acf8c-145">Make a note of the **Device ID** and **Device key**.</span></span> <span data-ttu-id="acf8c-146">Эти значения понадобятся вам позже, когда вы будете создавать приложение, которое подключается к Центру Интернета вещей от имени устройства.</span><span class="sxs-lookup"><span data-stu-id="acf8c-146">You need these values later when you create an app that connects to IoT Hub as a device.</span></span>

> [!NOTE]
> <span data-ttu-id="acf8c-147">В реестре удостоверений в Центре Интернета вещей хранятся только идентификаторы устройств, необходимые для безопасного доступа к Центру Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="acf8c-147">The IoT Hub identity registry only stores device identities to enable secure access to the IoT hub.</span></span> <span data-ttu-id="acf8c-148">В этом реестре хранятся идентификаторы и ключи устройств, которые используются в качестве учетных данных безопасности, и флажок включения или выключения, который позволяет вам отключить доступ для отдельного устройства.</span><span class="sxs-lookup"><span data-stu-id="acf8c-148">It stores device IDs and keys to use as security credentials and an enabled/disabled flag that you can use to disable access for an individual device.</span></span> <span data-ttu-id="acf8c-149">Если в приложении необходимо хранить другие метаданные для конкретного устройства, следует использовать хранилище конкретного приложения.</span><span class="sxs-lookup"><span data-stu-id="acf8c-149">If your app needs to store other device-specific metadata, it should use an app-specific store.</span></span> <span data-ttu-id="acf8c-150">Дополнительные сведения см. в [руководстве для разработчиков Центра Интернета вещей][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="acf8c-150">For more information, see the [IoT Hub developer guide][lnk-devguide-identity].</span></span>

## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="acf8c-151">Получение сообщений с устройства в облако</span><span class="sxs-lookup"><span data-stu-id="acf8c-151">Receive device-to-cloud messages</span></span>

<span data-ttu-id="acf8c-152">В этом разделе вы создадите консольное приложение Java, которое считывает сообщения, передаваемые с устройства в облако из Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="acf8c-152">In this section, you create a Java console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="acf8c-153">Центр Интернета вещей предоставляет совместимую с [концентраторами событий][lnk-event-hubs-overview] конечную точку для считывания сообщений, передаваемых с устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="acf8c-153">An IoT hub exposes an [Event Hub][lnk-event-hubs-overview]-compatible endpoint to enable you to read device-to-cloud messages.</span></span> <span data-ttu-id="acf8c-154">Для простоты в этом руководстве создается базовый модуль чтения, который не подходит для развертывания с высокой пропускной способностью.</span><span class="sxs-lookup"><span data-stu-id="acf8c-154">To keep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="acf8c-155">В руководстве по [обработке сообщений, передаваемых с устройства в облако][lnk-process-d2c-tutorial], показано, как обрабатывать такие сообщения в больших количествах.</span><span class="sxs-lookup"><span data-stu-id="acf8c-155">The [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial shows you how to process device-to-cloud messages at scale.</span></span> <span data-ttu-id="acf8c-156">В руководстве по [началу работы с концентраторами событий][lnk-eventhubs-tutorial] приведены дополнительные сведения о том, как обрабатываются сообщения из концентраторов событий. Это руководство применимо к конечным точкам Центра Интернета вещей, совместимым с концентраторами событий.</span><span class="sxs-lookup"><span data-stu-id="acf8c-156">The [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial provides further information on how to process messages from Event Hubs and is applicable to the IoT Hub Event Hub-compatible endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="acf8c-157">Совместимая с концентраторами событий конечная точка для чтения сообщений, отправляемых с устройства в облако, всегда использует протокол AMQP.</span><span class="sxs-lookup"><span data-stu-id="acf8c-157">The Event Hub-compatible endpoint for reading device-to-cloud messages always uses the AMQP protocol.</span></span>

1. <span data-ttu-id="acf8c-158">В папке iot-java-get-started, созданной в разделе *Создание удостоверения устройства*, создайте проект Maven с именем **read-d2c-messages**, выполнив в командной строке следующую команду.</span><span class="sxs-lookup"><span data-stu-id="acf8c-158">In the iot-java-get-started folder you created in the *Create a device identity* section, create a Maven project called **read-d2c-messages** using the following command at your command prompt.</span></span> <span data-ttu-id="acf8c-159">Обратите внимание, что это одна длинная команда.</span><span class="sxs-lookup"><span data-stu-id="acf8c-159">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-d2c-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="acf8c-160">В командной строке перейдите к папке read-d2c-messages.</span><span class="sxs-lookup"><span data-stu-id="acf8c-160">At your command prompt, navigate to the read-d2c-messages folder.</span></span>

3. <span data-ttu-id="acf8c-161">Откройте в текстовом редакторе файл pom.xml из папки read-d2c-messages и добавьте зависимости, приведенные ниже, в узел **dependency** .</span><span class="sxs-lookup"><span data-stu-id="acf8c-161">Using a text editor, open the pom.xml file in the read-d2c-messages folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="acf8c-162">Эта зависимость позволяет использовать пакет eventhubs-client в приложении, чтобы считывать данные с конечной точки, совместимой с концентраторами событий.</span><span class="sxs-lookup"><span data-stu-id="acf8c-162">This dependency enables you to use the eventhubs-client package in your app to read from the Event Hub-compatible endpoint:</span></span>

    ```xml
    <dependency> 
        <groupId>com.microsoft.azure</groupId> 
        <artifactId>azure-eventhubs</artifactId> 
        <version>0.13.0</version> 
    </dependency>
    ```

4. <span data-ttu-id="acf8c-163">Сохраните и закройте файл pom.xml.</span><span class="sxs-lookup"><span data-stu-id="acf8c-163">Save and close the pom.xml file.</span></span>

5. <span data-ttu-id="acf8c-164">Откройте в текстовом редакторе файл read-d2c-messages\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="acf8c-164">Using a text editor, open the read-d2c-messages\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="acf8c-165">Добавьте в файл следующие инструкции **import** .</span><span class="sxs-lookup"><span data-stu-id="acf8c-165">Add the following **import** statements to the file:</span></span>

    ```java
    import java.io.IOException;
    import com.microsoft.azure.eventhubs.*;
    import com.microsoft.azure.servicebus.*;

    import java.nio.charset.Charset;
    import java.time.*;
    import java.util.function.*;
    ```

7. <span data-ttu-id="acf8c-166">Добавьте приведенную ниже переменную уровня класса в класс **App** .</span><span class="sxs-lookup"><span data-stu-id="acf8c-166">Add the following class-level variable to the **App** class.</span></span> <span data-ttu-id="acf8c-167">Замените значения **{youriothubkey}**, **{youreventhubcompatibleendpoint}** и **{youreventhubcompatiblename}** значениями, записанными ранее.</span><span class="sxs-lookup"><span data-stu-id="acf8c-167">Replace **{youriothubkey}**, **{youreventhubcompatibleendpoint}**, and **{youreventhubcompatiblename}** with the values you noted previously:</span></span>

    ```java
    private static String connStr = "Endpoint={youreventhubcompatibleendpoint};EntityPath={youreventhubcompatiblename};SharedAccessKeyName=iothubowner;SharedAccessKey={youriothubkey}";
    ```

8. <span data-ttu-id="acf8c-168">Добавьте приведенный ниже метод **receiveMessages** в класс **App**.</span><span class="sxs-lookup"><span data-stu-id="acf8c-168">Add the following **receiveMessages** method to the **App** class.</span></span> <span data-ttu-id="acf8c-169">Этот метод создает экземпляр **EventHubClient**, чтобы подключиться к конечной точке, совместимой с концентраторами событий, а затем асинхронно создает экземпляр **PartitionReceiver** для чтения из секции концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="acf8c-169">This method creates an **EventHubClient** instance to connect to the Event Hub-compatible endpoint and then asynchronously creates a **PartitionReceiver** instance to read from an Event Hub partition.</span></span> <span data-ttu-id="acf8c-170">Он выполняет непрерывную циклическую обработку, выводя сведения о сообщении, пока приложение не завершит работу.</span><span class="sxs-lookup"><span data-stu-id="acf8c-170">It loops continuously and prints the message details until the app terminates.</span></span>

    ```java
    // Create a receiver on a partition.
    private static EventHubClient receiveMessages(final String partitionId) {
      EventHubClient client = null;
      try {
        client = EventHubClient.createFromConnectionStringSync(connStr);
      } catch (Exception e) {
        System.out.println("Failed to create client: " + e.getMessage());
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
                System.out.println("Failed to receive messages: " + e.getMessage());
              }
            }
          });
        } catch (Exception e) {
          System.out.println("Failed to create receiver: " + e.getMessage());
      }
      return client;
    }
    ```

   > [!NOTE]
   > <span data-ttu-id="acf8c-171">Этот метод использует фильтр во время создания получателя, чтобы получатель читал только сообщения, отправленные в Центр Интернета вещей после запуска получателя.</span><span class="sxs-lookup"><span data-stu-id="acf8c-171">This method uses a filter when it creates the receiver so that the receiver only reads messages sent to IoT Hub after the receiver starts running.</span></span> <span data-ttu-id="acf8c-172">Этот метод удобно использовать в тестовой среде для просмотра текущего набора сообщений.</span><span class="sxs-lookup"><span data-stu-id="acf8c-172">This technique is useful in a test environment so you can see the current set of messages.</span></span> <span data-ttu-id="acf8c-173">В рабочей среде код должен обеспечивать обработку всех сообщений. Дополнительные сведения см. в руководстве по [обработке сообщений Центра Интернета вещей, отправляемых с устройства в облако, с помощью .NET][lnk-process-d2c-tutorial].</span><span class="sxs-lookup"><span data-stu-id="acf8c-173">In a production environment, your code should make sure that it processes all the messages - for more information, see the [How to process IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>

9. <span data-ttu-id="acf8c-174">Измените подпись метода **main** , чтобы включить исключения, указанные ниже.</span><span class="sxs-lookup"><span data-stu-id="acf8c-174">Modify the signature of the **main** method to include the exception as follows:</span></span>

    ```java
    public static void main( String[] args ) throws IOException
    ```

10. <span data-ttu-id="acf8c-175">В метод **main** в классе **App** добавьте приведенный ниже код.</span><span class="sxs-lookup"><span data-stu-id="acf8c-175">Add the following code to the **main** method in the **App** class.</span></span> <span data-ttu-id="acf8c-176">Этот код создает два экземпляра, **EventHubClient** и **PartitionReceiver**, позволяя закрыть приложение, когда обработка сообщений будет завершена.</span><span class="sxs-lookup"><span data-stu-id="acf8c-176">This code creates the two **EventHubClient** and **PartitionReceiver** instances and enables you to close the app when you have finished processing messages:</span></span>

    ```java
    // Create receivers for partitions 0 and 1.
    EventHubClient client0 = receiveMessages("0");
    EventHubClient client1 = receiveMessages("1");
    System.out.println("Press ENTER to exit.");
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
    > <span data-ttu-id="acf8c-177">Предполагается, что вы создали Центр Интернета вещей на уровне F1 (Бесплатный).</span><span class="sxs-lookup"><span data-stu-id="acf8c-177">This code assumes you created your IoT hub in the F1 (free) tier.</span></span> <span data-ttu-id="acf8c-178">Бесплатный Центр Интернета вещей содержит два раздела с именами "0" и "1".</span><span class="sxs-lookup"><span data-stu-id="acf8c-178">A free IoT hub has two partitions named "0" and "1".</span></span>

11. <span data-ttu-id="acf8c-179">Сохраните и закройте файл App.java.</span><span class="sxs-lookup"><span data-stu-id="acf8c-179">Save and close the App.java file.</span></span>

12. <span data-ttu-id="acf8c-180">Чтобы создать приложение **read-d2c-messages** с помощью Maven, выполните в командной строке в папке read-d2c-messages следующую команду:</span><span class="sxs-lookup"><span data-stu-id="acf8c-180">To build the **read-d2c-messages** app using Maven, execute the following command at the command prompt in the read-d2c-messages folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="create-a-device-app"></a><span data-ttu-id="acf8c-181">Создание приложения устройства</span><span class="sxs-lookup"><span data-stu-id="acf8c-181">Create a device app</span></span>
<span data-ttu-id="acf8c-182">В этом разделе вы создаете консольное приложение Java, которое имитирует устройство, отправляющее сообщения с устройства в облако в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="acf8c-182">In this section, you create a Java console app that simulates a device that sends device-to-cloud messages to an IoT hub.</span></span>

1. <span data-ttu-id="acf8c-183">В папке iot-java-get-started, созданной в разделе *Создание удостоверения устройства*, создайте проект Maven с именем **simulated-device**, выполнив в командной строке следующую команду.</span><span class="sxs-lookup"><span data-stu-id="acf8c-183">In the iot-java-get-started folder you created in the *Create a device identity* section, create a Maven project called **simulated-device** using the following command at your command prompt.</span></span> <span data-ttu-id="acf8c-184">Обратите внимание, что это одна длинная команда.</span><span class="sxs-lookup"><span data-stu-id="acf8c-184">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="acf8c-185">В командной строке перейдите к папке simulated-device.</span><span class="sxs-lookup"><span data-stu-id="acf8c-185">At your command prompt, navigate to the simulated-device folder.</span></span>

3. <span data-ttu-id="acf8c-186">Откройте в текстовом редакторе файл pom.xml из папки simulated-device и добавьте приведенные ниже зависимости в узел **dependency** .</span><span class="sxs-lookup"><span data-stu-id="acf8c-186">Using a text editor, open the pom.xml file in the simulated-device folder and add the following dependencies to the **dependencies** node.</span></span> <span data-ttu-id="acf8c-187">Эта зависимость позволит вам использовать в приложении пакет iothub-java-client для обмена данными с Центром Интернета вещей и сериализации объектов Java в JSON.</span><span class="sxs-lookup"><span data-stu-id="acf8c-187">This dependency enables you to use the iothub-java-client package in your app to communicate with your IoT hub and to serialize Java objects to JSON:</span></span>

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
    > <span data-ttu-id="acf8c-188">Наличие последней версии пакета **iot-device-client** можно проверить с помощью [поиска Maven][lnk-maven-device-search].</span><span class="sxs-lookup"><span data-stu-id="acf8c-188">You can check for the latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

4. <span data-ttu-id="acf8c-189">Сохраните и закройте файл pom.xml.</span><span class="sxs-lookup"><span data-stu-id="acf8c-189">Save and close the pom.xml file.</span></span>

5. <span data-ttu-id="acf8c-190">Откройте в текстовом редакторе файл simulated-device\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="acf8c-190">Using a text editor, open the simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="acf8c-191">Добавьте в файл следующие инструкции **import** .</span><span class="sxs-lookup"><span data-stu-id="acf8c-191">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.google.gson.Gson;

    import java.io.*;
    import java.net.URISyntaxException;
    import java.util.Random;
    import java.util.concurrent.Executors;
    import java.util.concurrent.ExecutorService;
    ```

7. <span data-ttu-id="acf8c-192">Добавьте в класс **App** .</span><span class="sxs-lookup"><span data-stu-id="acf8c-192">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="acf8c-193">Замените значение **{youriothubname}** именем Центра Интернета вещей, а **{yourdevicekey}** — значением ключа устройства, сформированным при работе с разделом *Создание удостоверения устройства*.</span><span class="sxs-lookup"><span data-stu-id="acf8c-193">Replacing **{youriothubname}** with your IoT hub name, and **{yourdevicekey}** with the device key value you generated in the *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myFirstJavaDevice;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myFirstJavaDevice";
    private static DeviceClient client;
    ```
   
    <span data-ttu-id="acf8c-194">При создании экземпляра объекта **DeviceClient** в этом примере приложения используется переменная **protocol**.</span><span class="sxs-lookup"><span data-stu-id="acf8c-194">This sample app uses the **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="acf8c-195">Для взаимодействия с Центром Интернета вещей можно использовать протокол MQTT, AMQP или HTTP.</span><span class="sxs-lookup"><span data-stu-id="acf8c-195">You can use either the MQTT, AMQP, or HTTP protocol to communicate with IoT Hub.</span></span>

8. <span data-ttu-id="acf8c-196">Чтобы указать данные телеметрии, которые устройство отправляет в Центр Интернета вещей, добавьте в класс **App** следующий вложенный класс **TelemetryDataPoint**.</span><span class="sxs-lookup"><span data-stu-id="acf8c-196">Add the following nested **TelemetryDataPoint** class inside the **App** class to specify the telemetry data your device sends to your IoT hub:</span></span>

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
9. <span data-ttu-id="acf8c-197">Чтобы отобразить состояние подтверждения, возвращаемое Центром Интернета вещей при обработке сообщения с устройства приложения, добавьте в класс **App** приведенный ниже вложенный класс **EventCallback**.</span><span class="sxs-lookup"><span data-stu-id="acf8c-197">Add the following nested **EventCallback** class inside the **App** class to display the acknowledgement status that the IoT hub returns when it processes a message from the device app.</span></span> <span data-ttu-id="acf8c-198">Этот метод также уведомляет основной поток в приложении о том, что сообщение обработано.</span><span class="sxs-lookup"><span data-stu-id="acf8c-198">This method also notifies the main thread in the app when the message has been processed:</span></span>
   
    ```java
    private static class EventCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded to message with status: " + status.name());
   
        if (context != null) {
          synchronized (context) {
            context.notify();
          }
        }
      }
    }
    ```

10. <span data-ttu-id="acf8c-199">Добавьте приведенный ниже вложенный класс **MessageSender** в класс **App**.</span><span class="sxs-lookup"><span data-stu-id="acf8c-199">Add the following nested **MessageSender** class inside the **App** class.</span></span> <span data-ttu-id="acf8c-200">Метод **run** в этом классе создает пример данных телеметрии для отправки в Центр Интернета вещей и ожидает подтверждения перед отправкой следующего сообщения:</span><span class="sxs-lookup"><span data-stu-id="acf8c-200">The **run** method in this class generates sample telemetry data to send to your IoT hub and waits for an acknowledgement before sending the next message:</span></span>

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

    <span data-ttu-id="acf8c-201">Этот метод отправляет новое сообщение с устройства в облако через одну секунду после того, как Центр Интернета вещей подтверждает получение предыдущего сообщения.</span><span class="sxs-lookup"><span data-stu-id="acf8c-201">This method sends a new device-to-cloud message one second after the IoT hub acknowledges the previous message.</span></span> <span data-ttu-id="acf8c-202">Сообщение содержит объект сериализации JSON с идентификатором устройства и случайные числа, что позволяет имитировать датчик температуры и влажности.</span><span class="sxs-lookup"><span data-stu-id="acf8c-202">The message contains a JSON-serialized object with the deviceId and randomly generated numbers to simulate a temperature sensor, and a humidity sensor.</span></span>

11. <span data-ttu-id="acf8c-203">Замените метод **main** следующим кодом, который создает поток для отправки сообщений с устройства в облако в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="acf8c-203">Replace the **main** method with the following code that creates a thread to send device-to-cloud messages to your IoT hub:</span></span>

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException {
      client = new DeviceClient(connString, protocol);
      client.open();
    
      MessageSender sender = new MessageSender();
    
      ExecutorService executor = Executors.newFixedThreadPool(1);
      executor.execute(sender);
    
      System.out.println("Press ENTER to exit.");
      System.in.read();
      executor.shutdownNow();
      client.closeNow();
    }
    ```

12. <span data-ttu-id="acf8c-204">Сохраните и закройте файл App.java.</span><span class="sxs-lookup"><span data-stu-id="acf8c-204">Save and close the App.java file.</span></span>

13. <span data-ttu-id="acf8c-205">Чтобы создать приложение **simulated-device** с помощью Maven, выполните в командной строке в папке simulated-device следующую команду:</span><span class="sxs-lookup"><span data-stu-id="acf8c-205">To build the **simulated-device** app using Maven, execute the following command at the command prompt in the simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

> [!NOTE]
> <span data-ttu-id="acf8c-206">Для простоты в этом руководстве не реализуются политики повтора.</span><span class="sxs-lookup"><span data-stu-id="acf8c-206">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="acf8c-207">В рабочем коде следует реализовать политики повторных попыток (например, с экспоненциальной задержкой), как указано в статье [Обработка временного сбоя][lnk-transient-faults] на сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="acf8c-207">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-the-apps"></a><span data-ttu-id="acf8c-208">Запуск приложений</span><span class="sxs-lookup"><span data-stu-id="acf8c-208">Run the apps</span></span>

<span data-ttu-id="acf8c-209">Теперь все готово к запуску приложений.</span><span class="sxs-lookup"><span data-stu-id="acf8c-209">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="acf8c-210">Чтобы начать мониторинг первой секции в Центре Интернета вещей, в командной строке в папке read-d2c выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="acf8c-210">At a command prompt in the read-d2c folder, run the following command to begin monitoring the first partition in your IoT hub:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![Приложение службы Центра Интернета вещей на языке Java для мониторинга сообщений, отправляемых с устройства в облако][7]

2. <span data-ttu-id="acf8c-212">В командной строке в папке simulated-device выполните следующую команду, чтобы начать отправку данных телеметрии в Центр Интернета вещей:</span><span class="sxs-lookup"><span data-stu-id="acf8c-212">At a command prompt in the simulated-device folder, run the following command to begin sending telemetry data to your IoT hub:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![Приложение устройства Центра Интернета вещей на языке Java для отправки сообщений с устройства в облако][8]

3. <span data-ttu-id="acf8c-214">На плитке **Использование** на [портале Azure][lnk-portal] отображается количество сообщений, отправленных в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="acf8c-214">The **Usage** tile in the [Azure portal][lnk-portal] shows the number of messages sent to the IoT hub:</span></span>

    ![Плитка "Использование" на портале Azure, отображающая количество сообщений, отправленных в Центр Интернета вещей][43]

## <a name="next-steps"></a><span data-ttu-id="acf8c-216">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="acf8c-216">Next steps</span></span>
<span data-ttu-id="acf8c-217">В этом руководстве мы настроили новый Центр Интернета вещей на портале Azure и создали удостоверение устройства в реестре удостоверений Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="acf8c-217">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="acf8c-218">Это удостоверение позволяет приложению устройства отправлять в Центр Интернета вещей сообщения, передаваемые из устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="acf8c-218">You used this device identity to enable the device app to send device-to-cloud messages to the IoT hub.</span></span> <span data-ttu-id="acf8c-219">Кроме того, мы создали приложение, которое отображает сообщения, полученные Центром Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="acf8c-219">You also created an app that displays the messages received by the IoT hub.</span></span>

<span data-ttu-id="acf8c-220">Чтобы продолжить знакомство с Центром Интернета вещей и изучить другие сценарии Интернета вещей, см. следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="acf8c-220">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="acf8c-221">[Подключение устройства к Azure IoT][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="acf8c-221">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="acf8c-222">[How to get started with device management (Node)][lnk-device-management] (Начало работы с управлением устройствами (Node))</span><span class="sxs-lookup"><span data-stu-id="acf8c-222">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="acf8c-223">[Explore Azure IoT Edge architecture on Linux][lnk-iot-edge] (Приступая к работе с архитектурой Azure IoT Edge в Linux)</span><span class="sxs-lookup"><span data-stu-id="acf8c-223">[Getting started with Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="acf8c-224">Сведения о том, как расширить решение для Интернета вещей и обрабатывать сообщения, отправляемые с устройства в облако в большом количестве, см. [здесь][lnk-process-d2c-tutorial].</span><span class="sxs-lookup"><span data-stu-id="acf8c-224">To learn how to extend your IoT solution and process device-to-cloud messages at scale, see the [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
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
