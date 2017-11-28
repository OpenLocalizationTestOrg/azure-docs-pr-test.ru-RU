---
title: "Подключение Arduino (C) к Интернету вещей Azure. Урок 4. Изменение приложения | Документация Майкрософт"
description: "Настроив сообщения, вы сможете изменять режим включения и отключения светодиодного индикатора."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "управление светодиодным индикатором с помощью Arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: d7a25430-450e-43c4-a3ed-1eed995b8b7e
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5009a0466f2c5689b8ab426049f4c4f02272512b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-on-and-off-behavior-of-the-led"></a><span data-ttu-id="bc6f1-104">Изменение режима включения и отключения светодиодного индикатора</span><span class="sxs-lookup"><span data-stu-id="bc6f1-104">Change the on and off behavior of the LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="bc6f1-105">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="bc6f1-105">What you will do</span></span>
<span data-ttu-id="bc6f1-106">Настроив сообщения, вы сможете изменять режим включения и отключения светодиодного индикатора.</span><span class="sxs-lookup"><span data-stu-id="bc6f1-106">Customize the messages to change the LED’s on and off behavior.</span></span> <span data-ttu-id="bc6f1-107">Если возникнут какие-либо проблемы в работе платы Adafruit Feather M0 WiFi Arduino, решения можно найти на [странице со сведениями об устранении неполадок](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="bc6f1-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) for your Adafruit Feather M0 WiFi Arduino board.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="bc6f1-108">Новые знания</span><span class="sxs-lookup"><span data-stu-id="bc6f1-108">What you will learn</span></span>
<span data-ttu-id="bc6f1-109">Использование дополнительных функций Arduino для изменения режима включения и отключения светодиодного индикатора.</span><span class="sxs-lookup"><span data-stu-id="bc6f1-109">Use additional Arduino functions to change the LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="bc6f1-110">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="bc6f1-110">What you need</span></span>
<span data-ttu-id="bc6f1-111">Необходимо успешно выполнить [запуск примера приложения на плате Arduino для получения сообщений из облака на устройство][receive-cloud-to-device-messages].</span><span class="sxs-lookup"><span data-stu-id="bc6f1-111">You must have successfully completed [Run a sample application on your Arduino board to receive cloud to device messages][receive-cloud-to-device-messages].</span></span>

## <a name="add-functions-to-mainc-and-gulpfilejs"></a><span data-ttu-id="bc6f1-112">Добавление функций в файлы main.c и gulpfile.js</span><span class="sxs-lookup"><span data-stu-id="bc6f1-112">Add functions to main.c and gulpfile.js</span></span>
1. <span data-ttu-id="bc6f1-113">Откройте пример приложения в Visual Studio Code, выполнив следующие команды:</span><span class="sxs-lookup"><span data-stu-id="bc6f1-113">Open the sample application in Visual Studio code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="bc6f1-114">Откройте файл `app.ino` и после функции blinkLED() добавьте следующие функции:</span><span class="sxs-lookup"><span data-stu-id="bc6f1-114">Open the `app.ino` file, and then add the following functions after blinkLED() function:</span></span>

   ```arduino
   static void turnOnLED()
   {
     digitalWrite(LED_PIN, HIGH);
   }

   static void turnOffLED()
   {
     digitalWrite(LED_PIN, LOW);
   }
   ```

   ![Файл app.ino с добавленными функциями][app-ino-file]
3. <span data-ttu-id="bc6f1-116">Добавьте следующие условия перед блоком `else if` функции `receiveMessageCallback`:</span><span class="sxs-lookup"><span data-stu-id="bc6f1-116">Add the following conditions before the `else if` block of the `receiveMessageCallback` function:</span></span>

   ```arduino
   else if (strcmp((const char*)value, "\"on\"") == 0)
   {
       turnOnLED();
   }
   else if (0 == strcmp((const char*)value, "\"off\"") == 0)
   {
       turnOffLED();
   }
   ```

   <span data-ttu-id="bc6f1-117">Теперь пример приложения настроен для ответа на дополнительные инструкции с помощью сообщений.</span><span class="sxs-lookup"><span data-stu-id="bc6f1-117">Now you’ve configured the sample application to respond to more instructions through messages.</span></span> <span data-ttu-id="bc6f1-118">Инструкция on включает светодиодный индикатор, а инструкция off его отключает.</span><span class="sxs-lookup"><span data-stu-id="bc6f1-118">The "on" instruction turns on the LED, and the "off" instruction turns off the LED.</span></span>
4. <span data-ttu-id="bc6f1-119">Откройте файл gulpfile.js и добавьте новую функцию перед функцией `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="bc6f1-119">Open the gulpfile.js file, and then add a new function before the function `sendMessage`:</span></span>

   ```javascript
   var buildCustomMessage = function (messageId) {
     if ((messageId & 1) && (messageId < MAX_MESSAGE_COUNT)) {
       return new Message(JSON.stringify({ command: 'on', messageId: messageId }));
     } else if (messageId < MAX_MESSAGE_COUNT) {
       return new Message(JSON.stringify({ command: 'off', messageId: messageId }));
     } else {
       return new Message(JSON.stringify({ command: 'stop', messageId: messageId }));
     }
   };
   ```

   ![Файл gulpfile.js с добавленной функцией][gulp-file-js]
5. <span data-ttu-id="bc6f1-121">В функции `sendMessage` замените строку `var message = buildMessage(sentMessageCount);` новой строкой, показанной в следующем фрагменте:</span><span class="sxs-lookup"><span data-stu-id="bc6f1-121">In the `sendMessage` function, replace the line `var message = buildMessage(sentMessageCount);` with the new line shown in the following snippet:</span></span>

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="bc6f1-122">Сохраните все изменения.</span><span class="sxs-lookup"><span data-stu-id="bc6f1-122">Save all the changes.</span></span>

### <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="bc6f1-123">Развертывание и запуск примера приложения</span><span class="sxs-lookup"><span data-stu-id="bc6f1-123">Deploy and run the sample application</span></span>
<span data-ttu-id="bc6f1-124">Разверните и запустите пример приложения на плате Arduino, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="bc6f1-124">Deploy and run the sample application on your Arduino board by running the following command:</span></span>

```bash
gulp run
# You can monitor the serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

<span data-ttu-id="bc6f1-125">Светодиодный индикатор должен включиться на две секунды, а затем на две секунды выключиться.</span><span class="sxs-lookup"><span data-stu-id="bc6f1-125">You should see the LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="bc6f1-126">Последнее сообщение stop останавливает выполнение примера приложения.</span><span class="sxs-lookup"><span data-stu-id="bc6f1-126">The last "stop" message stops the sample application from running.</span></span>

![on и off][on-and-off]

<span data-ttu-id="bc6f1-128">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="bc6f1-128">Congratulations!</span></span> <span data-ttu-id="bc6f1-129">Вы успешно настроили сообщения, отправляемые на плату Arduino из Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="bc6f1-129">You’ve successfully customized the messages that are sent to your Arduino board from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="bc6f1-130">Сводка</span><span class="sxs-lookup"><span data-stu-id="bc6f1-130">Summary</span></span>
<span data-ttu-id="bc6f1-131">В этом дополнительном разделе показано, как настроить сообщения таким образом, чтобы пример приложения мог управлять включением и отключением светодиодного индикатора разными способами.</span><span class="sxs-lookup"><span data-stu-id="bc6f1-131">This optional section demonstrates how to customize messages so that the sample application can control the on and off behavior of the LED in a different way.</span></span>

<!-- Images and links -->

[receive-cloud-to-device-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-send-cloud-to-device-messages.md
[app-ino-file]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_app_ino.png
[gulp-file-js]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_gulpfile_js.png
[on-and-off]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/gulp_on_and_off_arduino.png