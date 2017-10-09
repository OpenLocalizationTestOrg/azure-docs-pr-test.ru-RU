---
title: "aaaProcess сообщения из устройства в облако Azure IoT Hub (Java) | Документы Microsoft"
description: "Способ tooprocess сообщения из устройства в облако центр IoT с помощью правила маршрутизации и toodispatch пользовательские конечные точки сообщений tooother серверными службами."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: bd9af5f9-a740-4780-a2a6-8c0e2752cf48
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: dobett
ms.openlocfilehash: 084e84e721ca4297c4d7d6cb06a43b0bed9bce85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="process-iot-hub-device-to-cloud-messages-java"></a>Обработка сообщений Центра Интернета вещей, отправляемых с устройства в облако (Java)

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

Центр Интернета вещей Azure —это полностью управляемая служба, которая обеспечивает надежный и защищенный двунаправленный обмен данными между миллионами устройств Интернета вещей и серверной частью решения. Другие учебники ([приступить к работе с центром IoT] и [отправки сообщений облака на устройство с центром IoT][lnk-c2d]) показано, как toouse hello основные устройства для облака и облака для устройства обмен сообщениями из центра IoT.

Этот учебник построен на hello код, показываемый в hello [приступить к работе с центром IoT] учебника и показано, как toouse сообщений маршрутизации сообщения из устройства в облако tooprocess масштабируемой способом. Hello учебник демонстрирует, как tooprocess сообщений, которые требуют немедленных действий из решения hello серверной части. Например, устройство может отправить аварийный сигнал, который активирует вставку билета в системе CRM. При этом обычные сообщения от точек данных просто поступают в модуль аналитики. Например температура телеметрии с устройства, которое является toobe сохранить для последующего анализа — это сообщение точки данных.

В конце этого учебника hello выполните три консольные приложения Java:

* **имитируемые устройства**, измененная версия приложения hello, созданного в hello [приступить к работе с центром IoT] учебник, отправляет сообщения из устройства в облако точки данных каждую секунду и интерактивные устройства в облако сообщений каждые 10 количество секунд. Это приложение использует toocommunicate протокол AMQP hello с центром IoT.
* **чтение d2c сообщений** отображает hello телеметрии, отправленные приложение устройства.
* **чтение критического очередь** исключении из очереди hello важные сообщения из toohello присоединенного очереди Service Bus hello центр IoT.

> [!NOTE]
> Для Центра Интернета вещей существуют пакеты SDK для многих платформ устройств и языков (включая C, Java и JavaScript). Инструкции по как tooreplace hello устройства в этом учебнике с физическим устройством и tooan устройств tooconnect центр IoT. в статье hello [Центр разработчиков Azure IoT].

toocomplete этого учебника требуется hello следующие:

* Полные рабочую версию hello [приступить к работе с центром IoT] учебника.
* Здравствуйте, последняя версия [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* Активная учетная запись Azure. (Если ее нет, можно создать [бесплатную учетную запись] [lnk-free-trial] всего за несколько минут.)

Кроме того, у вас должны быть базовые знания о [службе хранилища Azure] и [служебной шине Azure].

## <a name="send-interactive-messages-from-a-device-app"></a>Отправка интерактивных сообщений из приложения устройства
В этом разделе, измените приложение hello устройства, созданный в hello [приступить к работе с центром IoT] учебника toooccasionally отправлять сообщения, которые требуют немедленного обработки.

1. Используйте текстовый редактор tooopen hello simulated-device\src\main\java\com\mycompany\app\App.java файл. Этот файл содержит код hello для hello **имитируемые устройства** приложения, созданного в hello [приступить к работе с центром IoT] учебника.

2. Замените hello **MessageSender** класса hello, следующий код:

    ```java
    private static class MessageSender implements Runnable {

        public void run()  {
            try {
                double minTemperature = 20;
                double minHumidity = 60;
                Random rand = new Random();

                while (true) {
                    String msgStr;
                    Message msg;
                    if (new Random().nextDouble() > 0.7) {
                        msgStr = "This is a critical message.";
                        msg = new Message(msgStr);
                        msg.setProperty("level", "critical");
                    } else {
                        double currentTemperature = minTemperature + rand.nextDouble() * 15;
                        double currentHumidity = minHumidity + rand.nextDouble() * 20; 
                        TelemetryDataPoint telemetryDataPoint = new TelemetryDataPoint();
                        telemetryDataPoint.deviceId = deviceId;
                        telemetryDataPoint.temperature = currentTemperature;
                        telemetryDataPoint.humidity = currentHumidity;

                        msgStr = telemetryDataPoint.serialize();
                        msg = new Message(msgStr);
                    }
                    
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
   
    Этот метод случайным образом добавляет свойство hello `"level": "critical"` toomessages отправленных hello устройство, которое имитирует сообщение, которое требуется немедленное вмешательство с серверной части приложения hello. приложение Hello передает данные в свойствах сообщения hello, вместо в тело сообщения hello, поэтому этот центр IoT может направлять toohello соответствующее сообщение hello сообщения целевой.
   
   > [!NOTE]
   > Сообщения tooroute свойства сообщения можно использовать для различных сценариев, включая холодного путь к обработке, кроме приведенном здесь примере toohello критический путь.

2. Сохраните и закройте файл simulated-device\src\main\java\com\mycompany\app\App.java hello.

    > [!NOTE]
    > Ради hello простоты этого учебника не реализует никакую политику повтора. В рабочем коде следует реализовать политику повтора, например экспоненциальной отсрочки, описанным в статье MSDN hello [обработка временных сбоев].

3. toobuild hello **имитируемые устройства** приложения с помощью Maven, выполните следующую команду в командной строке hello в папке имитируемые устройства hello hello:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="add-a-queue-tooyour-iot-hub-and-route-messages-tooit"></a>Добавление очереди tooyour IoT hub и маршрутизации сообщений tooit

В этом разделе Создание очереди служебной шины, подключите его tooyour центр IoT и настройка вашей IoT концентратора toosend сообщения toohello очередь на основе наличия свойства на приветственное сообщение hello. Дополнительные сведения о как tooprocess сообщений из очереди Service Bus см. в разделе [приступить к работе с очередями][lnk-sb-queues-java].

1. Создайте очередь служебной шины, как описано в статье [Начало работы с очередями служебной шины][lnk-sb-queues-java]. Запишите hello пространство имен и имя очереди.

2. В hello портал Azure, откройте ваш центр IoT и щелкните **конечные точки**.

    ![Конечные точки в Центре Интернета вещей][30]

3. В hello **конечные точки** колонке нажмите кнопку **добавить** в hello top tooadd концентратор IoT tooyour очереди. Конечная точка hello имя **CriticalQueue** и используйте раскрывающиеся tooselect hello **очереди Service Bus**hello имен Service Bus, в котором находится Ваша очередь и hello именем очереди. Закончив, нажмите кнопку **Сохранить** внизу hello.

    ![Добавление конечной точки][31]

4. Теперь щелкните **Маршруты** в Центре Интернета вещей. Нажмите кнопку **добавить** вверху hello toocreate колонке hello правило маршрутизации сообщений, toohello очередь вы только что добавлен. Выберите **DeviceTelemetry** как hello источник данных. Введите `level="critical"` в качестве условия hello и выберите только что добавленный как настраиваемую конечную точку как конечную точку правила маршрутизации hello очереди hello. Закончив, нажмите кнопку **Сохранить** внизу hello.

    ![Добавление правила][32]

    Убедитесь, что резервный маршрута hello задано слишком**ON**. Этот параметр является конфигурацией по умолчанию hello центра IoT.

    ![Резервный маршрут][33]

## <a name="optional-read-from-hello-queue-endpoint"></a>(Необязательно) Чтение из конечной очереди hello

При необходимости можно читать сообщения hello из конечной очереди hello, следуя инструкциям hello [приступить к работе с очередями][lnk-sb-queues-java]. Имя приложения hello **чтение критического очередь**.

## <a name="run-hello-applications"></a>Запускать приложения hello

Теперь все три приложения hello toorun готовности.

1. toorun hello **чтение d2c сообщений** приложения, в командной строке или оболочки перейдите toohello d2c чтения папку и запустите hello следующую команду:

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```

   ![Запуск read-d2c-messages][readd2c]

2. toorun hello **чтение критического очередь** приложения, в командной строке или оболочки перейдите toohello чтение критического очередь папку и запустите hello следующую команду:

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Запуск read-critical-messages][readqueue]

3. toorun hello **имитируемые устройства** приложения, в командной строке или оболочки перейдите toohello имитируемые устройства папку и запустите hello следующую команду:

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Запуск приложения simulated-device][simulateddevice]

## <a name="next-steps"></a>Дальнейшие действия

В этом учебнике вы узнали, каким образом tooreliably отправки сообщения из устройства в облако с помощью средства маршрутизации сообщений hello из центра IoT.

Hello [способ сообщений toosend облака на устройство с центром IoT] [ lnk-c2d] показано, как toosend сообщений tooyour устройств из серверной части вашего решения.

см. Примеры toosee полное и всестороннее решений, использующих центр IoT [Azure IoT Suite][lnk-suite].

toolearn Дополнительные сведения о разработке решений с центром IoT разделе hello [руководстве для разработчиков центра IoT].

. в разделе toolearn Дополнительные сведения о маршрутизации сообщений в центре IoT [отправлять и получать сообщения с центром IoT][lnk-devguide-messaging].

<!-- Images. -->
<!-- TODO: UPDATE PICTURES -->
[simulateddevice]: ./media/iot-hub-java-java-process-d2c/runsimulateddevice.png
[readd2c]: ./media/iot-hub-java-java-process-d2c/runprocessinteractive.png
[readqueue]: ./media/iot-hub-java-java-process-d2c/runprocessd2c.png

[30]: ./media/iot-hub-java-java-process-d2c/click-endpoints.png
[31]: ./media/iot-hub-java-java-process-d2c/endpoint-creation.png
[32]: ./media/iot-hub-java-java-process-d2c/route-creation.png
[33]: ./media/iot-hub-java-java-process-d2c/fallback-route.png

<!-- Links -->

[lnk-sb-queues-java]: ../service-bus-messaging/service-bus-java-how-to-use-queues.md

[службе хранилища Azure]: https://azure.microsoft.com/documentation/services/storage/
[служебной шине Azure]: https://azure.microsoft.com/documentation/services/service-bus/

[руководстве для разработчиков центра IoT]: iot-hub-devguide.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
[приступить к работе с центром IoT]: iot-hub-java-java-getstarted.md
[Центр разработчиков Azure IoT]: https://azure.microsoft.com/develop/iot
[обработка временных сбоев]: https://msdn.microsoft.com/library/hh675232.aspx

<!-- Links -->
[Обработка временного сбоя]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-c2d]: iot-hub-java-java-c2d.md
[lnk-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
