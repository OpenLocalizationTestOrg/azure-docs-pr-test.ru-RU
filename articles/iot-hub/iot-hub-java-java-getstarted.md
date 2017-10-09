---
title: "aaaGet работы с Azure IoT Hub (Java) | Документы Microsoft"
description: "Узнайте, как toosend устройства в облако сообщений tooAzure центр IoT с помощью IoT пакеты SDK для Java. Создать имитированное устройство и службы приложений tooregister устройства, отправлять сообщения и чтения сообщений из центра IoT."
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
ms.openlocfilehash: ac954f0522b46ed2a5b4a819bc611c13be0b9a9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-tooyour-iot-hub-using-java"></a><span data-ttu-id="911e5-104">Подключиться с помощью Java концентратор IoT tooyour устройства</span><span class="sxs-lookup"><span data-stu-id="911e5-104">Connect your device tooyour IoT hub using Java</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="911e5-105">В конце этого учебника hello у вас есть три консольные приложения Java:</span><span class="sxs-lookup"><span data-stu-id="911e5-105">At hello end of this tutorial, you have three Java console apps:</span></span>

* <span data-ttu-id="911e5-106">**Создание устройства идентификаторов**, которая создает удостоверения устройства и связана защита ключа tooconnect приложение устройства.</span><span class="sxs-lookup"><span data-stu-id="911e5-106">**create-device-identity**, which creates a device identity and associated security key tooconnect your device app.</span></span>
* <span data-ttu-id="911e5-107">**чтение d2c сообщений**, которая отображает hello телеметрии, отправленные приложение устройства.</span><span class="sxs-lookup"><span data-stu-id="911e5-107">**read-d2c-messages**, which displays hello telemetry sent by your device app.</span></span>
* <span data-ttu-id="911e5-108">**имитируемые устройства**, который подключается центра IoT tooyour с идентификатором hello устройства, созданный ранее и будет отправлять данные телеметрии каждый второй с помощью протокола MQTT "hello".</span><span class="sxs-lookup"><span data-stu-id="911e5-108">**simulated-device**, which connects tooyour IoT hub with hello device identity created earlier, and sends a telemetry message every second using hello MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="911e5-109">статья Hello [пакеты SDK Azure IoT] [ lnk-hub-sdks] предоставляет сведения о hello Azure IoT пакетов SDK, которые можно использовать toobuild toorun обоих приложений на устройствах и серверной части вашего решения.</span><span class="sxs-lookup"><span data-stu-id="911e5-109">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both apps toorun on devices and your solution back end.</span></span>

<span data-ttu-id="911e5-110">toocomplete этого учебника требуется hello следующие:</span><span class="sxs-lookup"><span data-stu-id="911e5-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="911e5-111">Здравствуйте, последняя версия [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="911e5-111">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span> 
* [<span data-ttu-id="911e5-112">Maven 3</span><span class="sxs-lookup"><span data-stu-id="911e5-112">Maven 3</span></span>](https://maven.apache.org/install.html) 
* <span data-ttu-id="911e5-113">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="911e5-113">An active Azure account.</span></span> <span data-ttu-id="911e5-114">Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="911e5-114">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="911e5-115">В качестве последнего шага, запишите hello **первичного ключа** значение.</span><span class="sxs-lookup"><span data-stu-id="911e5-115">As a final step, make a note of hello **Primary key** value.</span></span> <span data-ttu-id="911e5-116">Нажмите кнопку **конечные точки** и hello **события** встроенные конечной точки.</span><span class="sxs-lookup"><span data-stu-id="911e5-116">Then click **Endpoints** and hello **Events** built-in endpoint.</span></span> <span data-ttu-id="911e5-117">На hello **свойства** колонке запомните hello **концентратора событий-совместимое имя** и hello **конечной точки концентратора событий в совместимом** адрес.</span><span class="sxs-lookup"><span data-stu-id="911e5-117">On hello **Properties** blade, make a note of hello **Event Hub-compatible name** and hello **Event Hub-compatible endpoint** address.</span></span> <span data-ttu-id="911e5-118">Эти три значения понадобятся при создании приложения **read-d2c-messages**.</span><span class="sxs-lookup"><span data-stu-id="911e5-118">You need these three values when you create your **read-d2c-messages** app.</span></span>

![Колонка "Сообщения" Центра Интернета вещей на портале Azure][6]

<span data-ttu-id="911e5-120">Теперь Центр Интернета вещей создан.</span><span class="sxs-lookup"><span data-stu-id="911e5-120">You have now created your IoT hub.</span></span> <span data-ttu-id="911e5-121">У вас есть hello центра IoT имя узла, центр IoT строку подключения, IoT Hub первичный ключ, имя совместимое концентратора событий и концентратора событий-совместимой конечной точки необходимо toocomplete этого учебника.</span><span class="sxs-lookup"><span data-stu-id="911e5-121">You have hello IoT Hub host name, IoT Hub connection string, IoT Hub Primary Key, Event Hub-compatible name, and Event Hub-compatible endpoint you need toocomplete this tutorial.</span></span>

## <a name="create-a-device-identity"></a><span data-ttu-id="911e5-122">Создание удостоверения устройства</span><span class="sxs-lookup"><span data-stu-id="911e5-122">Create a device identity</span></span>
<span data-ttu-id="911e5-123">В этом разделе создайте консольное приложение Java, которое создает удостоверение устройства в реестре hello identity в вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="911e5-123">In this section, you create a Java console app that creates a device identity in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="911e5-124">Устройство не удается подключиться tooIoT концентратора, если оно не имеет запись в реестре удостоверений hello.</span><span class="sxs-lookup"><span data-stu-id="911e5-124">A device cannot connect tooIoT hub unless it has an entry in hello identity registry.</span></span> <span data-ttu-id="911e5-125">Дополнительные сведения см. в разделе hello **реестра удостоверений** раздел hello [руководстве для разработчиков центра IoT][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="911e5-125">For more information, see hello **Identity Registry** section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="911e5-126">При запуске это консольное приложение, он создает уникальный идентификатор устройства и ключ, что при отправке устройства в облако, устройство может использовать tooidentify самого сообщения tooIoT концентратора.</span><span class="sxs-lookup"><span data-stu-id="911e5-126">When you run this console app, it generates a unique device ID and key that your device can use tooidentify itself when it sends device-to-cloud messages tooIoT Hub.</span></span>

1. <span data-ttu-id="911e5-127">Создайте пустую папку с именем iot-java-get-started.</span><span class="sxs-lookup"><span data-stu-id="911e5-127">Create an empty folder called iot-java-get-started.</span></span> <span data-ttu-id="911e5-128">В папке iot-java-get-started hello создайте Maven проект с именем **создать устройство идентификаторов** с помощью hello следующую команду в командной строке.</span><span class="sxs-lookup"><span data-stu-id="911e5-128">In hello iot-java-get-started folder, create a Maven project called **create-device-identity** using hello following command at your command prompt.</span></span> <span data-ttu-id="911e5-129">Обратите внимание, что это одна длинная команда.</span><span class="sxs-lookup"><span data-stu-id="911e5-129">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=create-device-identity -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="911e5-130">В командной строке перейдите папку toohello создать устройство идентификаторов.</span><span class="sxs-lookup"><span data-stu-id="911e5-130">At your command prompt, navigate toohello create-device-identity folder.</span></span>

3. <span data-ttu-id="911e5-131">В текстовом редакторе, откройте файл pom.xml hello в папке создайте устройств удостоверений hello и добавьте следующие зависимости toohello hello **зависимости** узла.</span><span class="sxs-lookup"><span data-stu-id="911e5-131">Using a text editor, open hello pom.xml file in hello create-device-identity folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="911e5-132">Эта зависимость позволяет вам toouse hello клиента для службы iot пакета в приложении:</span><span class="sxs-lookup"><span data-stu-id="911e5-132">This dependency enables you toouse hello iot-service-client package in your app:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="911e5-133">Вы можете проверить наличие hello последнюю версию **клиента для службы iot** с помощью [поиска Maven][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="911e5-133">You can check for hello latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

4. <span data-ttu-id="911e5-134">Сохраните и закройте файл pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="911e5-134">Save and close hello pom.xml file.</span></span>

5. <span data-ttu-id="911e5-135">В текстовом редакторе откройте файл create-device-identity\src\main\java\com\mycompany\app\App.java hello.</span><span class="sxs-lookup"><span data-stu-id="911e5-135">Using a text editor, open hello create-device-identity\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="911e5-136">Добавьте следующее hello **импорта** toohello файл инструкций:</span><span class="sxs-lookup"><span data-stu-id="911e5-136">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;
    import com.microsoft.azure.sdk.iot.service.Device;
    import com.microsoft.azure.sdk.iot.service.RegistryManager;
   
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. <span data-ttu-id="911e5-137">Добавьте следующие переменные уровня класса toohello hello **приложения** класса, заменив **{yourhubconnectionstring}** с hello значение на указанное выше:</span><span class="sxs-lookup"><span data-stu-id="911e5-137">Add hello following class-level variables toohello **App** class, replacing **{yourhubconnectionstring}** with hello value your noted earlier:</span></span>

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "myFirstJavaDevice";
    ```
[!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

8. <span data-ttu-id="911e5-138">Измените сигнатуру hello объекта hello **основной** tooinclude метод hello исключения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="911e5-138">Modify hello signature of hello **main** method tooinclude hello exceptions as follows:</span></span>

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException, Exception
    ```

9. <span data-ttu-id="911e5-139">Добавьте следующий код как текст hello hello hello **основной** метод.</span><span class="sxs-lookup"><span data-stu-id="911e5-139">Add hello following code as hello body of hello **main** method.</span></span> <span data-ttu-id="911e5-140">Этот код создает устройство с именем *javadevice* в реестре удостоверений Центра Интернета вещей, если оно еще не создано.</span><span class="sxs-lookup"><span data-stu-id="911e5-140">This code creates a device called *javadevice* in your IoT Hub identity registry if doesn't already exist.</span></span> <span data-ttu-id="911e5-141">Затем отображается идентификатор устройства hello и ключ, которые понадобятся позднее:</span><span class="sxs-lookup"><span data-stu-id="911e5-141">It then displays hello device ID and key that you need later:</span></span>

    ```java
    RegistryManager registryManager = RegistryManager.createFromConnectionString(connectionString);
RegistryManager registryManager = RegistryManager.createFromConnectionString(connectionString);

    // Create a device that's enabled by default, 
    // with an autogenerated key.
    Device device = Device.createFromId(deviceId, null, null);
    try {
      device = registryManager.addDevice(device);
    } catch (IotHubException iote) {
      // If hello device already exists.
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
      // If hello device already exists.
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

10. <span data-ttu-id="911e5-142">Сохраните и закройте файл App.java hello.</span><span class="sxs-lookup"><span data-stu-id="911e5-142">Save and close hello App.java file.</span></span>

11. <span data-ttu-id="911e5-143">toobuild hello **создать устройство идентификаторов** приложения с помощью Maven, выполните следующую команду в командной строке hello в папке создайте устройств удостоверений hello hello:</span><span class="sxs-lookup"><span data-stu-id="911e5-143">toobuild hello **create-device-identity** app using Maven, execute hello following command at hello command prompt in hello create-device-identity folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

12. <span data-ttu-id="911e5-144">toorun hello **создать устройство идентификаторов** приложения с помощью Maven, выполните следующую команду в командной строке hello в папке создайте устройств удостоверений hello hello:</span><span class="sxs-lookup"><span data-stu-id="911e5-144">toorun hello **create-device-identity** app using Maven, execute hello following command at hello command prompt in hello create-device-identity folder:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

13. <span data-ttu-id="911e5-145">Запишите hello **идентификатор устройства** и **ключ устройства**.</span><span class="sxs-lookup"><span data-stu-id="911e5-145">Make a note of hello **Device ID** and **Device key**.</span></span> <span data-ttu-id="911e5-146">Эти значения должны позже при создании приложения, которое подключается tooIoT концентратора как устройство.</span><span class="sxs-lookup"><span data-stu-id="911e5-146">You need these values later when you create an app that connects tooIoT Hub as a device.</span></span>

> [!NOTE]
> <span data-ttu-id="911e5-147">Hello реестра удостоверений центра IoT хранится только toohello устройства удостоверения tooenable безопасного доступа центра IoT.</span><span class="sxs-lookup"><span data-stu-id="911e5-147">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="911e5-148">Он сохраняет идентификаторы и ключи toouse устройства как учетные данные безопасности и включение или отключение флага, что toodisable доступа можно использовать для отдельных устройств.</span><span class="sxs-lookup"><span data-stu-id="911e5-148">It stores device IDs and keys toouse as security credentials and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="911e5-149">Если ваше приложение должно toostore другие метаданные для конкретного устройства, его следует использовать хранилище конкретного приложения.</span><span class="sxs-lookup"><span data-stu-id="911e5-149">If your app needs toostore other device-specific metadata, it should use an app-specific store.</span></span> <span data-ttu-id="911e5-150">Дополнительные сведения см. в разделе hello [руководстве для разработчиков центра IoT][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="911e5-150">For more information, see hello [IoT Hub developer guide][lnk-devguide-identity].</span></span>

## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="911e5-151">Получение сообщений с устройства в облако</span><span class="sxs-lookup"><span data-stu-id="911e5-151">Receive device-to-cloud messages</span></span>

<span data-ttu-id="911e5-152">В этом разделе вы создадите консольное приложение Java, которое считывает сообщения, передаваемые с устройства в облако из Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="911e5-152">In this section, you create a Java console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="911e5-153">Центр IoT предоставляет [концентратора событий][lnk-event-hubs-overview]-совместимую конечную точку tooenable вам сообщения tooread устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="911e5-153">An IoT hub exposes an [Event Hub][lnk-event-hubs-overview]-compatible endpoint tooenable you tooread device-to-cloud messages.</span></span> <span data-ttu-id="911e5-154">простые действия tookeep, данный учебник создает основные средства чтения, не подходит для развертывания высокой пропускной способностью.</span><span class="sxs-lookup"><span data-stu-id="911e5-154">tookeep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="911e5-155">Hello [обрабатывать сообщения из устройства в облако] [ lnk-process-d2c-tutorial] учебнике показано, как сообщения tooprocess устройства в облако в масштабе.</span><span class="sxs-lookup"><span data-stu-id="911e5-155">hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial shows you how tooprocess device-to-cloud messages at scale.</span></span> <span data-ttu-id="911e5-156">Hello [Приступая к работе с концентраторами событий] [ lnk-eventhubs-tutorial] учебника содержатся дополнительные сведения о предоставлении tooprocess сообщений из концентраторов событий и определяется применимо toohello конечными точками события концентратора IoT Hub совместимой.</span><span class="sxs-lookup"><span data-stu-id="911e5-156">hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial provides further information on how tooprocess messages from Event Hubs and is applicable toohello IoT Hub Event Hub-compatible endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="911e5-157">Hello концентратора событий-совместимой конечной точки для чтения сообщения из устройства в облако, всегда использует протокол AMQP hello.</span><span class="sxs-lookup"><span data-stu-id="911e5-157">hello Event Hub-compatible endpoint for reading device-to-cloud messages always uses hello AMQP protocol.</span></span>

1. <span data-ttu-id="911e5-158">В папке iot-java-get-started hello, созданные в hello *создать удостоверение устройства* статьи, создайте проект с именем Maven **чтение d2c сообщений** hello следующую команду в командной строке с помощью.</span><span class="sxs-lookup"><span data-stu-id="911e5-158">In hello iot-java-get-started folder you created in hello *Create a device identity* section, create a Maven project called **read-d2c-messages** using hello following command at your command prompt.</span></span> <span data-ttu-id="911e5-159">Обратите внимание, что это одна длинная команда.</span><span class="sxs-lookup"><span data-stu-id="911e5-159">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-d2c-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="911e5-160">В командной строке перейдите toohello чтение d2c сообщений папки.</span><span class="sxs-lookup"><span data-stu-id="911e5-160">At your command prompt, navigate toohello read-d2c-messages folder.</span></span>

3. <span data-ttu-id="911e5-161">В текстовом редакторе, откройте файл pom.xml hello в папке чтения d2c – сообщений hello и добавьте следующие зависимости toohello hello **зависимости** узла.</span><span class="sxs-lookup"><span data-stu-id="911e5-161">Using a text editor, open hello pom.xml file in hello read-d2c-messages folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="911e5-162">Эта зависимость позволяет пакет клиента eventhubs toouse hello в tooread вашего приложения из конечной точки концентратора событий-совместимой hello:</span><span class="sxs-lookup"><span data-stu-id="911e5-162">This dependency enables you toouse hello eventhubs-client package in your app tooread from hello Event Hub-compatible endpoint:</span></span>

    ```xml
    <dependency> 
        <groupId>com.microsoft.azure</groupId> 
        <artifactId>azure-eventhubs</artifactId> 
        <version>0.13.0</version> 
    </dependency>
    ```

4. <span data-ttu-id="911e5-163">Сохраните и закройте файл pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="911e5-163">Save and close hello pom.xml file.</span></span>

5. <span data-ttu-id="911e5-164">В текстовом редакторе откройте файл read-d2c-messages\src\main\java\com\mycompany\app\App.java hello.</span><span class="sxs-lookup"><span data-stu-id="911e5-164">Using a text editor, open hello read-d2c-messages\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="911e5-165">Добавьте следующее hello **импорта** toohello файл инструкций:</span><span class="sxs-lookup"><span data-stu-id="911e5-165">Add hello following **import** statements toohello file:</span></span>

    ```java
    import java.io.IOException;
    import com.microsoft.azure.eventhubs.*;
    import com.microsoft.azure.servicebus.*;

    import java.nio.charset.Charset;
    import java.time.*;
    import java.util.function.*;
    ```

7. <span data-ttu-id="911e5-166">Добавьте следующие toohello переменной уровня класса hello **приложения** класса.</span><span class="sxs-lookup"><span data-stu-id="911e5-166">Add hello following class-level variable toohello **App** class.</span></span> <span data-ttu-id="911e5-167">Замените **{youriothubkey}**, **{youreventhubcompatibleendpoint}**, и **{youreventhubcompatiblename}** со значениями hello, записанное ранее:</span><span class="sxs-lookup"><span data-stu-id="911e5-167">Replace **{youriothubkey}**, **{youreventhubcompatibleendpoint}**, and **{youreventhubcompatiblename}** with hello values you noted previously:</span></span>

    ```java
    private static String connStr = "Endpoint={youreventhubcompatibleendpoint};EntityPath={youreventhubcompatiblename};SharedAccessKeyName=iothubowner;SharedAccessKey={youriothubkey}";
    ```

8. <span data-ttu-id="911e5-168">Добавьте следующее hello **receiveMessages** toohello метод **приложения** класса.</span><span class="sxs-lookup"><span data-stu-id="911e5-168">Add hello following **receiveMessages** method toohello **App** class.</span></span> <span data-ttu-id="911e5-169">Этот метод создает **EventHubClient** экземпляр конечной точки tooconnect toohello совместимое концентратора событий и асинхронно создает **PartitionReceiver** tooread экземпляр из концентратора событий секции.</span><span class="sxs-lookup"><span data-stu-id="911e5-169">This method creates an **EventHubClient** instance tooconnect toohello Event Hub-compatible endpoint and then asynchronously creates a **PartitionReceiver** instance tooread from an Event Hub partition.</span></span> <span data-ttu-id="911e5-170">Он постоянно циклы и выводит сведения о сообщении hello до завершения приложение hello.</span><span class="sxs-lookup"><span data-stu-id="911e5-170">It loops continuously and prints hello message details until hello app terminates.</span></span>

    ```java
    // Create a receiver on a partition.
    private static EventHubClient receiveMessages(final String partitionId) {
      EventHubClient client = null;
      try {
        client = EventHubClient.createFromConnectionStringSync(connStr);
      } catch (Exception e) {
        System.out.println("Failed toocreate client: " + e.getMessage());
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
                System.out.println("Failed tooreceive messages: " + e.getMessage());
              }
            }
          });
        } catch (Exception e) {
          System.out.println("Failed toocreate receiver: " + e.getMessage());
      }
      return client;
    }
    ```

   > [!NOTE]
   > <span data-ttu-id="911e5-171">Этот метод использует фильтр при создании приемника hello, чтобы hello приемник считывает только сообщения, отправленные tooIoT концентратора после hello получатель начинает выполнение.</span><span class="sxs-lookup"><span data-stu-id="911e5-171">This method uses a filter when it creates hello receiver so that hello receiver only reads messages sent tooIoT Hub after hello receiver starts running.</span></span> <span data-ttu-id="911e5-172">Этот метод полезен в тестовой среде, чтобы можно было видеть текущий набор сообщений hello.</span><span class="sxs-lookup"><span data-stu-id="911e5-172">This technique is useful in a test environment so you can see hello current set of messages.</span></span> <span data-ttu-id="911e5-173">В рабочей среде кода следует убедитесь в том, что обработке всех сообщений hello - Дополнительные сведения см. в разделе hello [как tooprocess сообщения из устройства в облако центра IoT] [ lnk-process-d2c-tutorial] учебника.</span><span class="sxs-lookup"><span data-stu-id="911e5-173">In a production environment, your code should make sure that it processes all hello messages - for more information, see hello [How tooprocess IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>

9. <span data-ttu-id="911e5-174">Измените сигнатуру hello объекта hello **основной** tooinclude метод hello исключения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="911e5-174">Modify hello signature of hello **main** method tooinclude hello exception as follows:</span></span>

    ```java
    public static void main( String[] args ) throws IOException
    ```

10. <span data-ttu-id="911e5-175">Добавьте следующий код toohello hello **основной** метод в hello **приложения** класса.</span><span class="sxs-lookup"><span data-stu-id="911e5-175">Add hello following code toohello **main** method in hello **App** class.</span></span> <span data-ttu-id="911e5-176">Этот код создает два hello **EventHubClient** и **PartitionReceiver** экземпляров и включает приложение hello tooclose после завершения обработки сообщений:</span><span class="sxs-lookup"><span data-stu-id="911e5-176">This code creates hello two **EventHubClient** and **PartitionReceiver** instances and enables you tooclose hello app when you have finished processing messages:</span></span>

    ```java
    // Create receivers for partitions 0 and 1.
    EventHubClient client0 = receiveMessages("0");
    EventHubClient client1 = receiveMessages("1");
    System.out.println("Press ENTER tooexit.");
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
    > <span data-ttu-id="911e5-177">Данный код предполагает, что вы создали концентратор IoT hello F1 (бесплатно) уровня.</span><span class="sxs-lookup"><span data-stu-id="911e5-177">This code assumes you created your IoT hub in hello F1 (free) tier.</span></span> <span data-ttu-id="911e5-178">Бесплатный Центр Интернета вещей содержит два раздела с именами "0" и "1".</span><span class="sxs-lookup"><span data-stu-id="911e5-178">A free IoT hub has two partitions named "0" and "1".</span></span>

11. <span data-ttu-id="911e5-179">Сохраните и закройте файл App.java hello.</span><span class="sxs-lookup"><span data-stu-id="911e5-179">Save and close hello App.java file.</span></span>

12. <span data-ttu-id="911e5-180">toobuild hello **чтение d2c сообщений** приложения с помощью Maven, выполните следующую команду в командной строке hello в папке чтения d2c сообщения hello hello:</span><span class="sxs-lookup"><span data-stu-id="911e5-180">toobuild hello **read-d2c-messages** app using Maven, execute hello following command at hello command prompt in hello read-d2c-messages folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="create-a-device-app"></a><span data-ttu-id="911e5-181">Создание приложения устройства</span><span class="sxs-lookup"><span data-stu-id="911e5-181">Create a device app</span></span>
<span data-ttu-id="911e5-182">В этом разделе создайте консольное приложение Java, которое имитирует устройство, которое отправляет центр IoT tooan сообщения из устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="911e5-182">In this section, you create a Java console app that simulates a device that sends device-to-cloud messages tooan IoT hub.</span></span>

1. <span data-ttu-id="911e5-183">В папке iot-java-get-started hello, созданные в hello *создать удостоверение устройства* статьи, создайте проект с именем Maven **имитируемые устройства** hello следующую команду в командной строке с помощью.</span><span class="sxs-lookup"><span data-stu-id="911e5-183">In hello iot-java-get-started folder you created in hello *Create a device identity* section, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="911e5-184">Обратите внимание, что это одна длинная команда.</span><span class="sxs-lookup"><span data-stu-id="911e5-184">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="911e5-185">В командной строке перейдите папку toohello имитируемые устройства.</span><span class="sxs-lookup"><span data-stu-id="911e5-185">At your command prompt, navigate toohello simulated-device folder.</span></span>

3. <span data-ttu-id="911e5-186">В текстовом редакторе, откройте файл pom.xml hello в папке имитируемые устройства hello и добавьте следующие зависимости toohello hello **зависимости** узла.</span><span class="sxs-lookup"><span data-stu-id="911e5-186">Using a text editor, open hello pom.xml file in hello simulated-device folder and add hello following dependencies toohello **dependencies** node.</span></span> <span data-ttu-id="911e5-187">Эта зависимость позволяет вам toouse hello центром IOT java-пакет клиента по toocommunicate вашего приложения с центр IoT и tooserialize tooJSON объектов Java:</span><span class="sxs-lookup"><span data-stu-id="911e5-187">This dependency enables you toouse hello iothub-java-client package in your app toocommunicate with your IoT hub and tooserialize Java objects tooJSON:</span></span>

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
    > <span data-ttu-id="911e5-188">Вы можете проверить наличие hello последнюю версию **клиента для устройства iot** с помощью [поиска Maven][lnk-maven-device-search].</span><span class="sxs-lookup"><span data-stu-id="911e5-188">You can check for hello latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

4. <span data-ttu-id="911e5-189">Сохраните и закройте файл pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="911e5-189">Save and close hello pom.xml file.</span></span>

5. <span data-ttu-id="911e5-190">В текстовом редакторе откройте файл simulated-device\src\main\java\com\mycompany\app\App.java hello.</span><span class="sxs-lookup"><span data-stu-id="911e5-190">Using a text editor, open hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="911e5-191">Добавьте следующее hello **импорта** toohello файл инструкций:</span><span class="sxs-lookup"><span data-stu-id="911e5-191">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.google.gson.Gson;

    import java.io.*;
    import java.net.URISyntaxException;
    import java.util.Random;
    import java.util.concurrent.Executors;
    import java.util.concurrent.ExecutorService;
    ```

7. <span data-ttu-id="911e5-192">Добавьте следующие переменные уровня класса toohello hello **приложения** класса.</span><span class="sxs-lookup"><span data-stu-id="911e5-192">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="911e5-193">Замена **{youriothubname}** на название концентратора IoT и **{yourdevicekey}** со значением ключа устройства hello созданный hello *создать удостоверение устройства* раздела:</span><span class="sxs-lookup"><span data-stu-id="911e5-193">Replacing **{youriothubname}** with your IoT hub name, and **{yourdevicekey}** with hello device key value you generated in hello *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myFirstJavaDevice;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myFirstJavaDevice";
    private static DeviceClient client;
    ```
   
    <span data-ttu-id="911e5-194">Этот пример приложения использует hello **протокола** переменной, когда он создает **DeviceClient** объекта.</span><span class="sxs-lookup"><span data-stu-id="911e5-194">This sample app uses hello **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="911e5-195">Можно использовать либо toocommunicate hello MQTT, AMQP или HTTP-протокол с центром IoT.</span><span class="sxs-lookup"><span data-stu-id="911e5-195">You can use either hello MQTT, AMQP, or HTTP protocol toocommunicate with IoT Hub.</span></span>

8. <span data-ttu-id="911e5-196">Добавьте следующее hello вложенные **TelemetryDataPoint** класс внутри hello **приложения** устройство отправляет центр IoT tooyour данные телеметрии hello toospecify класса:</span><span class="sxs-lookup"><span data-stu-id="911e5-196">Add hello following nested **TelemetryDataPoint** class inside hello **App** class toospecify hello telemetry data your device sends tooyour IoT hub:</span></span>

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
9. <span data-ttu-id="911e5-197">Добавьте следующее hello вложенные **EventCallback** класс внутри hello **приложения** класс hello toodisplay подтверждения состояния, hello центра IoT возвращает при обработке сообщения из устройства приложение hello.</span><span class="sxs-lookup"><span data-stu-id="911e5-197">Add hello following nested **EventCallback** class inside hello **App** class toodisplay hello acknowledgement status that hello IoT hub returns when it processes a message from hello device app.</span></span> <span data-ttu-id="911e5-198">Этот метод также сообщает о hello основного потока в приложение hello после обработки сообщения hello:</span><span class="sxs-lookup"><span data-stu-id="911e5-198">This method also notifies hello main thread in hello app when hello message has been processed:</span></span>
   
    ```java
    private static class EventCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toomessage with status: " + status.name());
   
        if (context != null) {
          synchronized (context) {
            context.notify();
          }
        }
      }
    }
    ```

10. <span data-ttu-id="911e5-199">Добавьте следующее hello вложенные **MessageSender** класс внутри hello **приложения** класса.</span><span class="sxs-lookup"><span data-stu-id="911e5-199">Add hello following nested **MessageSender** class inside hello **App** class.</span></span> <span data-ttu-id="911e5-200">Hello **запуска** метода в данном классе создает образец данных телеметрии toosend tooyour IoT hub и ожидает подтверждения перед отправкой hello следующее сообщение:</span><span class="sxs-lookup"><span data-stu-id="911e5-200">hello **run** method in this class generates sample telemetry data toosend tooyour IoT hub and waits for an acknowledgement before sending hello next message:</span></span>

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

    <span data-ttu-id="911e5-201">Этот метод отправляет новое сообщение устройства в облако одной секунды после центра IoT hello подтверждает предыдущее сообщение hello.</span><span class="sxs-lookup"><span data-stu-id="911e5-201">This method sends a new device-to-cloud message one second after hello IoT hub acknowledges hello previous message.</span></span> <span data-ttu-id="911e5-202">приветственное сообщение содержит объект сериализации JSON с hello deviceId и случайным образом toosimulate номера датчика температуры и влажности датчика.</span><span class="sxs-lookup"><span data-stu-id="911e5-202">hello message contains a JSON-serialized object with hello deviceId and randomly generated numbers toosimulate a temperature sensor, and a humidity sensor.</span></span>

11. <span data-ttu-id="911e5-203">Замените hello **основной** метод с hello, следующий код, создающий концентратор IoT tooyour поток toosend сообщения из устройства в облако:</span><span class="sxs-lookup"><span data-stu-id="911e5-203">Replace hello **main** method with hello following code that creates a thread toosend device-to-cloud messages tooyour IoT hub:</span></span>

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException {
      client = new DeviceClient(connString, protocol);
      client.open();
    
      MessageSender sender = new MessageSender();
    
      ExecutorService executor = Executors.newFixedThreadPool(1);
      executor.execute(sender);
    
      System.out.println("Press ENTER tooexit.");
      System.in.read();
      executor.shutdownNow();
      client.closeNow();
    }
    ```

12. <span data-ttu-id="911e5-204">Сохраните и закройте файл App.java hello.</span><span class="sxs-lookup"><span data-stu-id="911e5-204">Save and close hello App.java file.</span></span>

13. <span data-ttu-id="911e5-205">toobuild hello **имитируемые устройства** приложения с помощью Maven, выполните следующую команду в командной строке hello в папке имитируемые устройства hello hello:</span><span class="sxs-lookup"><span data-stu-id="911e5-205">toobuild hello **simulated-device** app using Maven, execute hello following command at hello command prompt in hello simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

> [!NOTE]
> <span data-ttu-id="911e5-206">простые действия tookeep, этот учебник не реализует никакую политику повтора.</span><span class="sxs-lookup"><span data-stu-id="911e5-206">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="911e5-207">В рабочем коде следует реализовать политики повтора (например экспоненциальную отсрочку), описанным в статье MSDN hello [обработка временных сбоев][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="911e5-207">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="911e5-208">Запускайте приложения hello</span><span class="sxs-lookup"><span data-stu-id="911e5-208">Run hello apps</span></span>

<span data-ttu-id="911e5-209">Теперь вы находитесь toorun готовности приложения hello.</span><span class="sxs-lookup"><span data-stu-id="911e5-209">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="911e5-210">В командной строке в папке d2c чтения hello выполните следующие команды toobegin мониторинг hello первую секцию в концентратор IoT hello:</span><span class="sxs-lookup"><span data-stu-id="911e5-210">At a command prompt in hello read-d2c folder, run hello following command toobegin monitoring hello first partition in your IoT hub:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![Центр IoT Java службы приложения toomonitor устройства в облако сообщений][7]

2. <span data-ttu-id="911e5-212">В командной строке в папке hello имитируемые устройства выполните hello, следующая команда toobegin отправки центра IoT tooyour данных телеметрии:</span><span class="sxs-lookup"><span data-stu-id="911e5-212">At a command prompt in hello simulated-device folder, run hello following command toobegin sending telemetry data tooyour IoT hub:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![Сообщения из устройства в облако toosend приложения центра IoT Java устройства][8]

3. <span data-ttu-id="911e5-214">Hello **использование** плитки в hello [портал Azure] [ lnk-portal] показано hello число сообщений, отправляемых toohello центр IoT:</span><span class="sxs-lookup"><span data-stu-id="911e5-214">hello **Usage** tile in hello [Azure portal][lnk-portal] shows hello number of messages sent toohello IoT hub:</span></span>

    ![Azure портала использование плитки, показывающего количество сообщений, отправляемых tooIoT концентратора][43]

## <a name="next-steps"></a><span data-ttu-id="911e5-216">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="911e5-216">Next steps</span></span>
<span data-ttu-id="911e5-217">В этом учебнике настроен центр IoT в hello портал Azure и затем создать удостоверение устройства в реестре удостоверений центра IoT hello.</span><span class="sxs-lookup"><span data-stu-id="911e5-217">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="911e5-218">Вы использовали устройства удостоверения tooenable hello устройства приложения toosend сообщения из устройства в облако toohello центр IoT.</span><span class="sxs-lookup"><span data-stu-id="911e5-218">You used this device identity tooenable hello device app toosend device-to-cloud messages toohello IoT hub.</span></span> <span data-ttu-id="911e5-219">Также было создано приложение, которое отображает hello сообщений, полученных центра IoT hello.</span><span class="sxs-lookup"><span data-stu-id="911e5-219">You also created an app that displays hello messages received by hello IoT hub.</span></span>

<span data-ttu-id="911e5-220">Приступая к работе toocontinue центр IoT и tooexplore других сценариев IoT просмотреть:</span><span class="sxs-lookup"><span data-stu-id="911e5-220">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="911e5-221">[Подключение устройства к Azure IoT][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="911e5-221">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="911e5-222">[How to get started with device management (Node)][lnk-device-management] (Начало работы с управлением устройствами (Node))</span><span class="sxs-lookup"><span data-stu-id="911e5-222">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="911e5-223">[Explore Azure IoT Edge architecture on Linux][lnk-iot-edge] (Приступая к работе с архитектурой Azure IoT Edge в Linux)</span><span class="sxs-lookup"><span data-stu-id="911e5-223">[Getting started with Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="911e5-224">toolearn tooextend сообщений в масштабе, IoT решение и процесс устройства в облако. в статье hello [обрабатывать сообщения из устройства в облако] [ lnk-process-d2c-tutorial] учебника.</span><span class="sxs-lookup"><span data-stu-id="911e5-224">toolearn how tooextend your IoT solution and process device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
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
