---
title: "сообщения aaaCloud на устройство с центром IoT Azure (Java) | Документы Microsoft"
description: "Способ toosend облака на устройство сообщений tooa устройств из центра Azure IoT с помощью hello Azure IoT, пакеты SDK для Java. Изменение сообщений облака на устройство имитированное устройство tooreceive приложения и изменения сообщений облака на устройство hello toosend серверной части приложения."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 7f785ea8-e7c2-40c5-87ef-96525e9b9e1e
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: dobett
ms.openlocfilehash: 8721f18428c849ed9a04aa2e45c65605c3e38101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-to-device-messages-with-iot-hub-java"></a><span data-ttu-id="02067-104">Отправка сообщений из облака на устройство с помощью Центра Интернета вещей (Java)</span><span class="sxs-lookup"><span data-stu-id="02067-104">Send cloud-to-device messages with IoT Hub (Java)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

<span data-ttu-id="02067-105">Центр Интернета вещей Azure — это полностью управляемая служба, которая обеспечивает надежный и защищенный двунаправленный обмен данными между миллионами устройств и серверной частью решения.</span><span class="sxs-lookup"><span data-stu-id="02067-105">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="02067-106">Hello [приступить к работе с центром IoT] учебнике показано, как подготовить удостоверение устройства в нем toocreate центр IoT и кода приложения имитацию устройств, которое отправляет сообщения из устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="02067-106">hello [Get started with IoT Hub] tutorial shows how toocreate an IoT hub, provision a device identity in it, and code a simulated device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="02067-107">Это руководство является логическим продолжением статьи [приступить к работе с центром IoT].</span><span class="sxs-lookup"><span data-stu-id="02067-107">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="02067-108">В нем показано следующее:</span><span class="sxs-lookup"><span data-stu-id="02067-108">It shows you how to:</span></span>

* <span data-ttu-id="02067-109">Из серверной части вашего решения отправьте сообщения облака на устройство tooa одно устройство через Центр IoT.</span><span class="sxs-lookup"><span data-stu-id="02067-109">From your solution back end, send cloud-to-device messages tooa single device through IoT Hub.</span></span>
* <span data-ttu-id="02067-110">Получение на устройстве сообщений, передаваемых из облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="02067-110">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="02067-111">Из вашего решения внутренний запрос подтверждения доставки (*отзывы*) для сообщений отправленных tooa устройств из центра IoT.</span><span class="sxs-lookup"><span data-stu-id="02067-111">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent tooa device from IoT Hub.</span></span>

<span data-ttu-id="02067-112">Дополнительные сведения о сообщениях облака на устройство можно найти в hello [руководстве для разработчиков центра IoT][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="02067-112">You can find more information on cloud-to-device messages in hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="02067-113">В конце этого учебника hello выполните два консольные приложения Java:</span><span class="sxs-lookup"><span data-stu-id="02067-113">At hello end of this tutorial, you run two Java console apps:</span></span>

* <span data-ttu-id="02067-114">**имитируемые устройства**, измененную версию приложения hello, созданного в [приступить к работе с центром IoT], который подключается tooyour центр IoT и получает сообщения облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="02067-114">**simulated-device**, a modified version of hello app created in [Get started with IoT Hub], which connects tooyour IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="02067-115">**отправлять c2d сообщения**, который отправляет приложения имитированное устройство toohello сообщение облака на устройство с помощью центра IoT, а затем получает подтверждение его доставки.</span><span class="sxs-lookup"><span data-stu-id="02067-115">**send-c2d-messages**, which sends a cloud-to-device message toohello simulated device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="02067-116">Для центра IoT существуют пакеты SDK для многих платформ устройств и языков (включая C, Java и Javascript). Эти пакеты работают на основе пакетов SDK для устройств Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="02067-116">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="02067-117">Пошаговые инструкции по tooconnect кода учебник toothis устройства и обычно tooAzure центр IoT. в статье hello [Центр разработчиков Azure IoT].</span><span class="sxs-lookup"><span data-stu-id="02067-117">For step-by-step instructions on how tooconnect your device toothis tutorial's code, and generally tooAzure IoT Hub, see hello [Azure IoT Developer Center].</span></span>

<span data-ttu-id="02067-118">toocomplete этого учебника требуется hello следующие:</span><span class="sxs-lookup"><span data-stu-id="02067-118">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="02067-119">Полные рабочую версию hello [приступить к работе с центром IoT](iot-hub-java-java-getstarted.md) или [сообщения из устройства в облако центра IoT процесс](iot-hub-java-java-process-d2c.md) учебника.</span><span class="sxs-lookup"><span data-stu-id="02067-119">A complete working version of hello [Get started with IoT Hub](iot-hub-java-java-getstarted.md) or [Process IoT Hub device-to-cloud messages](iot-hub-java-java-process-d2c.md) tutorial.</span></span>
* <span data-ttu-id="02067-120">Здравствуйте, последняя версия [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="02067-120">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="02067-121">Maven 3</span><span class="sxs-lookup"><span data-stu-id="02067-121">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="02067-122">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="02067-122">An active Azure account.</span></span> <span data-ttu-id="02067-123">Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="02067-123">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-hello-simulated-device-app"></a><span data-ttu-id="02067-124">Получать сообщения в приложение hello имитированное устройство</span><span class="sxs-lookup"><span data-stu-id="02067-124">Receive messages in hello simulated device app</span></span>

<span data-ttu-id="02067-125">В этом разделе, измените приложение hello имитированное устройство, вы создали в [приступить к работе с центром IoT] tooreceive сообщений облака на устройство из центра IoT hello.</span><span class="sxs-lookup"><span data-stu-id="02067-125">In this section, you modify hello simulated device app you created in [Get started with IoT Hub] tooreceive cloud-to-device messages from hello IoT hub.</span></span>

1. <span data-ttu-id="02067-126">В текстовом редакторе откройте файл simulated-device\src\main\java\com\mycompany\app\App.java hello.</span><span class="sxs-lookup"><span data-stu-id="02067-126">Using a text editor, open hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

2. <span data-ttu-id="02067-127">Добавьте следующее hello **MessageCallback** класс как класс является вложенным в hello **приложения** класса.</span><span class="sxs-lookup"><span data-stu-id="02067-127">Add hello following **MessageCallback** class as a nested class inside hello **App** class.</span></span> <span data-ttu-id="02067-128">Hello **выполнение** метод вызывается, когда устройство hello получает сообщение из центра IoT.</span><span class="sxs-lookup"><span data-stu-id="02067-128">hello **execute** method is invoked when hello device receives a message from IoT Hub.</span></span> <span data-ttu-id="02067-129">В этом примере hello устройства всегда уведомляет центра IoT hello о завершении приветственное сообщение:</span><span class="sxs-lookup"><span data-stu-id="02067-129">In this example, hello device always notifies hello IoT hub that it has completed hello message:</span></span>

    ```java
    private static class AppMessageCallback implements MessageCallback {
      public IotHubMessageResult execute(Message msg, Object context) {
        System.out.println("Received message from hub: "
          + new String(msg.getBytes(), Message.DEFAULT_IOTHUB_MESSAGE_CHARSET));
    
        return IotHubMessageResult.COMPLETE;
      }
    }
    ```
3. <span data-ttu-id="02067-130">Изменение hello **основной** toocreate метод **AppMessageCallback** экземпляра и вызова hello **setMessageCallback** метод перед открытием hello клиента следующим образом:</span><span class="sxs-lookup"><span data-stu-id="02067-130">Modify hello **main** method toocreate an **AppMessageCallback** instance and call hello **setMessageCallback** method before it opens hello client as follows:</span></span>

    ```java
    client = new DeviceClient(connString, protocol);
   
    MessageCallback callback = new AppMessageCallback();
    client.setMessageCallback(callback, null);
    client.open();
    ```

    > [!NOTE]
    > <span data-ttu-id="02067-131">При использовании HTTP вместо MQTT или AMQP транспорта hello hello **DeviceClient** экземпляра проверяет наличие сообщений от редко центр IoT (меньше, чем каждые 25 минут).</span><span class="sxs-lookup"><span data-stu-id="02067-131">If you use HTTP instead of MQTT or AMQP as hello transport, hello **DeviceClient** instance checks for messages from IoT Hub infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="02067-132">Дополнительные сведения об отличиях hello поддержки MQTT, AMQP и HTTP и центр IoT регулирования см. в разделе hello [руководстве для разработчиков центра IoT][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="02067-132">For more information about hello differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

4. <span data-ttu-id="02067-133">toobuild hello **имитируемые устройства** приложения с помощью Maven, выполните следующую команду в командной строке hello в папке имитируемые устройства hello hello:</span><span class="sxs-lookup"><span data-stu-id="02067-133">toobuild hello **simulated-device** app using Maven, execute hello following command at hello command prompt in hello simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="02067-134">Отправка сообщения из облака на устройство</span><span class="sxs-lookup"><span data-stu-id="02067-134">Send a cloud-to-device message</span></span>

<span data-ttu-id="02067-135">В этом разделе создайте консольное приложение Java, которое отправляет сообщения облака на устройство toohello имитированное устройство приложения.</span><span class="sxs-lookup"><span data-stu-id="02067-135">In this section, you create a Java console app that sends cloud-to-device messages toohello simulated device app.</span></span> <span data-ttu-id="02067-136">Требуется hello идентификатор устройства устройства hello, добавленного в hello [приступить к работе с центром IoT] учебника.</span><span class="sxs-lookup"><span data-stu-id="02067-136">You need hello device ID of hello device you added in hello [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="02067-137">Строка подключения концентратора IoT требуется hello для концентратору, который можно найти в hello [портал Azure].</span><span class="sxs-lookup"><span data-stu-id="02067-137">You also need hello IoT Hub connection string for your hub that you can find in hello [Azure portal].</span></span>

1. <span data-ttu-id="02067-138">Создайте проект с именем Maven **сообщений send-c2d** с помощью hello следующую команду в командной строке.</span><span class="sxs-lookup"><span data-stu-id="02067-138">Create a Maven project called **send-c2d-messages** using hello following command at your command prompt.</span></span> <span data-ttu-id="02067-139">Обратите внимание, что это одна длинная команда.</span><span class="sxs-lookup"><span data-stu-id="02067-139">Note this command is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=send-c2d-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="02067-140">В командной строке перейдите toohello новую папку отправлять c2d-сообщения.</span><span class="sxs-lookup"><span data-stu-id="02067-140">At your command prompt, navigate toohello new send-c2d-messages folder.</span></span>

3. <span data-ttu-id="02067-141">В текстовом редакторе, откройте файл pom.xml hello в папке отправки c2d – сообщений hello и добавьте следующие зависимости toohello hello **зависимости** узла.</span><span class="sxs-lookup"><span data-stu-id="02067-141">Using a text editor, open hello pom.xml file in hello send-c2d-messages folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="02067-142">Добавление зависимости hello позволяет toouse hello **центром IOT java служба клиента** пакета в toocommunicate вашего приложения в службе концентратора IoT:</span><span class="sxs-lookup"><span data-stu-id="02067-142">Adding hello dependency enables you toouse hello **iothub-java-service-client** package in your application toocommunicate with your IoT hub service:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="02067-143">Вы можете проверить наличие hello последнюю версию **клиента для службы iot** с помощью [поиска Maven][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="02067-143">You can check for hello latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

4. <span data-ttu-id="02067-144">Сохраните и закройте файл pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="02067-144">Save and close hello pom.xml file.</span></span>

5. <span data-ttu-id="02067-145">В текстовом редакторе откройте файл send-c2d-messages\src\main\java\com\mycompany\app\App.java hello.</span><span class="sxs-lookup"><span data-stu-id="02067-145">Using a text editor, open hello send-c2d-messages\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="02067-146">Добавьте следующее hello **импорта** toohello файл инструкций:</span><span class="sxs-lookup"><span data-stu-id="02067-146">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. <span data-ttu-id="02067-147">Добавьте следующие переменные уровня класса toohello hello **приложения** класса, заменив **{yourhubconnectionstring}** и **{yourdeviceid}** с hello значения на указанное выше:</span><span class="sxs-lookup"><span data-stu-id="02067-147">Add hello following class-level variables toohello **App** class, replacing **{yourhubconnectionstring}** and **{yourdeviceid}** with hello values your noted earlier:</span></span>

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "{yourdeviceid}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    ```

8. <span data-ttu-id="02067-148">Замените hello **основной** метод после кода hello.</span><span class="sxs-lookup"><span data-stu-id="02067-148">Replace hello **main** method with hello following code.</span></span> <span data-ttu-id="02067-149">Этот код подключается центра IoT tooyour, отправляет сообщения tooyour устройство и ждет подтверждения, приветственное сообщение hello полученных и обработанных устройств:</span><span class="sxs-lookup"><span data-stu-id="02067-149">This code connects tooyour IoT hub, sends a message tooyour device, and then waits for an acknowledgment that hello device received and processed hello message:</span></span>
   
    ```java
    public static void main(String[] args) throws IOException,
        URISyntaxException, Exception {
      ServiceClient serviceClient = ServiceClient.createFromConnectionString(
        connectionString, protocol);
   
      if (serviceClient != null) {
        serviceClient.open();
        FeedbackReceiver feedbackReceiver = serviceClient
          .getFeedbackReceiver();
        if (feedbackReceiver != null) feedbackReceiver.open();
   
        Message messageToSend = new Message("Cloud toodevice message.");
        messageToSend.setDeliveryAcknowledgement(DeliveryAcknowledgement.Full);
   
        serviceClient.send(deviceId, messageToSend);
        System.out.println("Message sent toodevice");
   
        FeedbackBatch feedbackBatch = feedbackReceiver.receive(10000);
        if (feedbackBatch != null) {
          System.out.println("Message feedback received, feedback time: "
            + feedbackBatch.getEnqueuedTimeUtc().toString());
        }
   
        if (feedbackReceiver != null) feedbackReceiver.close();
        serviceClient.close();
      }
    }
    ```

    > [!NOTE]
    > <span data-ttu-id="02067-150">Для упрощения в этом учебнике не реализуются какие-либо политики повтора.</span><span class="sxs-lookup"><span data-stu-id="02067-150">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="02067-151">В рабочем коде следует реализовать политики повтора (например, экспоненциального отката), описанным в статье MSDN hello [обработка временных сбоев].</span><span class="sxs-lookup"><span data-stu-id="02067-151">In production code, you should implement retry policies (such as exponential backoff), as suggested in hello MSDN article [Transient Fault Handling].</span></span>


9. <span data-ttu-id="02067-152">toobuild hello **имитируемые устройства** приложения с помощью Maven, выполните следующую команду в командной строке hello в папке имитируемые устройства hello hello:</span><span class="sxs-lookup"><span data-stu-id="02067-152">toobuild hello **simulated-device** app using Maven, execute hello following command at hello command prompt in hello simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-hello-applications"></a><span data-ttu-id="02067-153">Запускать приложения hello</span><span class="sxs-lookup"><span data-stu-id="02067-153">Run hello applications</span></span>

<span data-ttu-id="02067-154">Теперь вы находитесь toorun готовности приложения hello.</span><span class="sxs-lookup"><span data-stu-id="02067-154">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="02067-155">В командной строке в папке hello имитируемые устройства выполните hello после отправки центр IoT tooyour телеметрии и toolisten для облака на устройство сообщений, отправляемых из концентратор toobegin команды:</span><span class="sxs-lookup"><span data-stu-id="02067-155">At a command prompt in hello simulated-device folder, run hello following command toobegin sending telemetry tooyour IoT hub and toolisten for cloud-to-device messages sent from your hub:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![Запустить имитированное устройство приложение hello][img-simulated-device]

2. <span data-ttu-id="02067-157">В командной строке в папке сообщений send-c2d hello выполните hello, следующая команда toosend сообщение облака на устройство и ожидания подтверждения обратной связи.</span><span class="sxs-lookup"><span data-stu-id="02067-157">At a command prompt in hello send-c2d-messages folder, run hello following command toosend a cloud-to-device message and wait for a feedback acknowledgment:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![Запустите приветственное сообщение hello команда toosend облака на устройство][img-send-command]

## <a name="next-steps"></a><span data-ttu-id="02067-159">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="02067-159">Next steps</span></span>

<span data-ttu-id="02067-160">В этом учебнике вы узнали, как toosend и получать сообщения облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="02067-160">In this tutorial, you learned how toosend and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="02067-161">см. Примеры toosee полное и всестороннее решений, использующих центр IoT [Azure IoT Suite].</span><span class="sxs-lookup"><span data-stu-id="02067-161">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="02067-162">toolearn Дополнительные сведения о разработке решений с центром IoT разделе hello [руководстве для разработчиков центра IoT].</span><span class="sxs-lookup"><span data-stu-id="02067-162">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

<!-- Images -->
[img-simulated-device]: media/iot-hub-java-java-c2d/receivec2d.png
[img-send-command]:  media/iot-hub-java-java-c2d/sendc2d.png
<!-- Links -->

[приступить к работе с центром IoT]: iot-hub-java-java-getstarted.md
[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md
[руководстве для разработчиков центра IoT]: iot-hub-devguide.md
[Центр разработчиков Azure IoT]: http://www.azure.com/develop/iot
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java
[обработка временных сбоев]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[портал Azure]: https://portal.azure.com
[Azure IoT Suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22