---
title: "Connect Arduino (C) tooAzure IoT — занятия 4: изменить приложение | Документы Microsoft"
description: "Настройте hello toochange сообщений hello, Индикатор, включение и отключение поведение."
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
ms.openlocfilehash: 8cc438650f01ae4335d91c94df6a29e0ffbdc508
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a><span data-ttu-id="51935-104">Изменить hello и отключать поведение hello Индикатора</span><span class="sxs-lookup"><span data-stu-id="51935-104">Change hello on and off behavior of hello LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="51935-105">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="51935-105">What you will do</span></span>
<span data-ttu-id="51935-106">Настройте hello toochange сообщений hello, Индикатор, включение и отключение поведение.</span><span class="sxs-lookup"><span data-stu-id="51935-106">Customize hello messages toochange hello LED’s on and off behavior.</span></span> <span data-ttu-id="51935-107">Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) Adafruit Растушевка M0 Wi-Fi Arduino плата.</span><span class="sxs-lookup"><span data-stu-id="51935-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) for your Adafruit Feather M0 WiFi Arduino board.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="51935-108">Новые знания</span><span class="sxs-lookup"><span data-stu-id="51935-108">What you will learn</span></span>
<span data-ttu-id="51935-109">Используйте дополнительные hello toochange функции Arduino, Индикатор, включение и отключение поведение.</span><span class="sxs-lookup"><span data-stu-id="51935-109">Use additional Arduino functions toochange hello LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="51935-110">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="51935-110">What you need</span></span>
<span data-ttu-id="51935-111">Необходимо успешно выполнить [запуска примеров приложений в облаке tooreceive Arduino доски сообщений toodevice][receive-cloud-to-device-messages].</span><span class="sxs-lookup"><span data-stu-id="51935-111">You must have successfully completed [Run a sample application on your Arduino board tooreceive cloud toodevice messages][receive-cloud-to-device-messages].</span></span>

## <a name="add-functions-toomainc-and-gulpfilejs"></a><span data-ttu-id="51935-112">Добавление функций toomain.c и gulpfile.js</span><span class="sxs-lookup"><span data-stu-id="51935-112">Add functions toomain.c and gulpfile.js</span></span>
1. <span data-ttu-id="51935-113">Откройте пример приложения hello в коде Visual Studio, выполнив следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="51935-113">Open hello sample application in Visual Studio code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="51935-114">Откройте hello `app.ino` файл, а затем добавьте следующие функции после blinkLED() функции hello:</span><span class="sxs-lookup"><span data-stu-id="51935-114">Open hello `app.ino` file, and then add hello following functions after blinkLED() function:</span></span>

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
3. <span data-ttu-id="51935-116">Добавьте следующие условия перед hello hello `else if` блок hello `receiveMessageCallback` функции:</span><span class="sxs-lookup"><span data-stu-id="51935-116">Add hello following conditions before hello `else if` block of hello `receiveMessageCallback` function:</span></span>

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

   <span data-ttu-id="51935-117">Теперь вы настроили hello образец приложения toorespond toomore инструкции с помощью сообщений.</span><span class="sxs-lookup"><span data-stu-id="51935-117">Now you’ve configured hello sample application toorespond toomore instructions through messages.</span></span> <span data-ttu-id="51935-118">Hello «на «инструкция включает Индикатор hello и hello, «off» инструкция отключает hello Индикатора.</span><span class="sxs-lookup"><span data-stu-id="51935-118">hello "on" instruction turns on hello LED, and hello "off" instruction turns off hello LED.</span></span>
4. <span data-ttu-id="51935-119">Откройте файл gulpfile.js hello, а затем добавьте новую функцию перед функцией hello `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="51935-119">Open hello gulpfile.js file, and then add a new function before hello function `sendMessage`:</span></span>

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
5. <span data-ttu-id="51935-121">В hello `sendMessage` функционировать, замените строку hello `var message = buildMessage(sentMessageCount);` с новую строку hello показано hello, следующий фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="51935-121">In hello `sendMessage` function, replace hello line `var message = buildMessage(sentMessageCount);` with hello new line shown in hello following snippet:</span></span>

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="51935-122">Сохраните все изменения hello.</span><span class="sxs-lookup"><span data-stu-id="51935-122">Save all hello changes.</span></span>

### <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="51935-123">Развертывание и запуск образца приложения hello</span><span class="sxs-lookup"><span data-stu-id="51935-123">Deploy and run hello sample application</span></span>
<span data-ttu-id="51935-124">Развертывание и запуск образца приложения hello на доске Arduino, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="51935-124">Deploy and run hello sample application on your Arduino board by running hello following command:</span></span>

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

<span data-ttu-id="51935-125">Вы увидите hello Индикатор, включите для двух секунд, а затем выключите для другой две секунды.</span><span class="sxs-lookup"><span data-stu-id="51935-125">You should see hello LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="51935-126">Последнее сообщение Hello «остановить» останавливает образец приложения hello запуск.</span><span class="sxs-lookup"><span data-stu-id="51935-126">hello last "stop" message stops hello sample application from running.</span></span>

![on и off][on-and-off]

<span data-ttu-id="51935-128">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="51935-128">Congratulations!</span></span> <span data-ttu-id="51935-129">Сообщения приветствия, отправляемыми плата Arduino tooyour ваш центр IoT успешно настроен.</span><span class="sxs-lookup"><span data-stu-id="51935-129">You’ve successfully customized hello messages that are sent tooyour Arduino board from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="51935-130">Сводка</span><span class="sxs-lookup"><span data-stu-id="51935-130">Summary</span></span>
<span data-ttu-id="51935-131">Этот дополнительный раздел показывает способ toocustomize сообщений, чтобы пример приложения hello мог управлять hello и отключать поведение hello Индикатор по-разному.</span><span class="sxs-lookup"><span data-stu-id="51935-131">This optional section demonstrates how toocustomize messages so that hello sample application can control hello on and off behavior of hello LED in a different way.</span></span>

<!-- Images and links -->

[receive-cloud-to-device-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-send-cloud-to-device-messages.md
[app-ino-file]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_app_ino.png
[gulp-file-js]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_gulpfile_js.png
[on-and-off]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/gulp_on_and_off_arduino.png