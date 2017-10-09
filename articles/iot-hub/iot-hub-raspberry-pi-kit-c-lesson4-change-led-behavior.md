---
title: "Connect Raspberry PI (C) tooAzure IoT — занятия 4: изменить приложение | Документы Microsoft"
description: "Настройте hello toochange сообщений hello, Индикатор, включение и отключение поведение."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "управление светодиодным индикатором с помощью raspberry pi, raspberry pi управление индикатором, управлять светодиодным индикатором raspberry pi"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 0201b8ed-d5e6-4445-9a4d-1305003d1eff
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: f4739c4e9a58b4b0fe964b5c3c81e5918982099f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a><span data-ttu-id="d6211-104">Изменить hello и отключать поведение hello Индикатора</span><span class="sxs-lookup"><span data-stu-id="d6211-104">Change hello on and off behavior of hello LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="d6211-105">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="d6211-105">What you will do</span></span>
<span data-ttu-id="d6211-106">Настройте hello toochange сообщений hello, Индикатор, включение и отключение поведение.</span><span class="sxs-lookup"><span data-stu-id="d6211-106">Customize hello messages toochange hello LED’s on and off behavior.</span></span> <span data-ttu-id="d6211-107">Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="d6211-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="d6211-108">Новые знания</span><span class="sxs-lookup"><span data-stu-id="d6211-108">What you will learn</span></span>
<span data-ttu-id="d6211-109">Используйте дополнительные hello toochange функции Node.js, Индикатор, включение и отключение поведение.</span><span class="sxs-lookup"><span data-stu-id="d6211-109">Use additional Node.js functions toochange hello LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="d6211-110">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="d6211-110">What you need</span></span>
<span data-ttu-id="d6211-111">Необходимо успешно выполнить [запуска примера приложения в облаке tooreceive Raspberry Pi toodevice сообщения](iot-hub-raspberry-pi-kit-c-lesson4-send-cloud-to-device-messages.md).</span><span class="sxs-lookup"><span data-stu-id="d6211-111">You must have successfully completed [Run a sample application on Raspberry Pi tooreceive cloud toodevice messages](iot-hub-raspberry-pi-kit-c-lesson4-send-cloud-to-device-messages.md).</span></span>

## <a name="add-functions-toomainc-and-gulpfilejs"></a><span data-ttu-id="d6211-112">Добавление функций toomain.c и gulpfile.js</span><span class="sxs-lookup"><span data-stu-id="d6211-112">Add functions toomain.c and gulpfile.js</span></span>
1. <span data-ttu-id="d6211-113">Откройте пример приложения hello в коде Visual Studio, выполнив следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="d6211-113">Open hello sample application in Visual Studio code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="d6211-114">Откройте hello `main.c` файл, а затем добавьте следующие функции после blinkLED() функции hello:</span><span class="sxs-lookup"><span data-stu-id="d6211-114">Open hello `main.c` file, and then add hello following functions after blinkLED() function:</span></span>

   ```c
   static void turnOnLED()
   {
     digitalWrite(LED_PIN, HIGH);
   }

   static void turnOffLED()
   {
     digitalWrite(LED_PIN, LOW);
   }
   ```

   ![Файл main.c с добавленными функциями](media/iot-hub-raspberry-pi-lessons/lesson4/updated_app_c.png)
3. <span data-ttu-id="d6211-116">Добавьте следующую команду по умолчанию hello одного условия в hello hello `if` блок hello `receiveMessageCallback` функции:</span><span class="sxs-lookup"><span data-stu-id="d6211-116">Add hello following conditions before hello default one in hello `if` block of hello `receiveMessageCallback` function:</span></span>

   ```c
   else if (0 == strcmp((const char*)value, "\"on\""))
   {
       turnOnLED();
   }
   else if (0 == strcmp((const char*)value, "\"off\""))
   {
       turnOffLED();
   }
   ```

   <span data-ttu-id="d6211-117">Теперь вы настроили hello образец приложения toorespond toomore инструкции с помощью сообщений.</span><span class="sxs-lookup"><span data-stu-id="d6211-117">Now you’ve configured hello sample application toorespond toomore instructions through messages.</span></span> <span data-ttu-id="d6211-118">Hello «на «инструкция включает Индикатор hello и hello, «off» инструкция отключает hello Индикатора.</span><span class="sxs-lookup"><span data-stu-id="d6211-118">hello "on" instruction turns on hello LED, and hello "off" instruction turns off hello LED.</span></span>
4. <span data-ttu-id="d6211-119">Откройте файл gulpfile.js hello, а затем добавьте новую функцию перед функцией hello `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="d6211-119">Open hello gulpfile.js file, and then add a new function before hello function `sendMessage`:</span></span>

   ```javascript
   var buildCustomMessage = function (messageId) {
     if ((messageId & 1) && (messageId < MAX_MESSAGE_COUNT)) {
       return new Message(JSON.stringify({ command: 'on', messageId: messageId }));
     } else if (messageId < MAX_MESSAGE_COUNT) {
       return new Message(JSON.stringify({ command: 'off', messageId: messageId }));
     } else {
       return new Message(JSON.stringify({ command: 'stop', messageId: messageId }));
     }
   }
   ```

   ![Файл gulpfile.js с добавленной функцией](media/iot-hub-raspberry-pi-lessons/lesson4/updated_gulpfile_c.png)
5. <span data-ttu-id="d6211-121">В hello `sendMessage` функционировать, замените строку hello `var message = buildMessage(sentMessageCount);` с новую строку hello показано hello, следующий фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="d6211-121">In hello `sendMessage` function, replace hello line `var message = buildMessage(sentMessageCount);` with hello new line shown in hello following snippet:</span></span>

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="d6211-122">Сохраните все изменения hello.</span><span class="sxs-lookup"><span data-stu-id="d6211-122">Save all hello changes.</span></span>

### <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="d6211-123">Развертывание и запуск образца приложения hello</span><span class="sxs-lookup"><span data-stu-id="d6211-123">Deploy and run hello sample application</span></span>
<span data-ttu-id="d6211-124">Развертывание и запуск образца приложения hello на Pi, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="d6211-124">Deploy and run hello sample application on Pi by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="d6211-125">Вы увидите hello Индикатор, включите для двух секунд, а затем выключите для другой две секунды.</span><span class="sxs-lookup"><span data-stu-id="d6211-125">You should see hello LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="d6211-126">Последнее сообщение Hello «остановить» останавливает образец приложения hello запуск.</span><span class="sxs-lookup"><span data-stu-id="d6211-126">hello last "stop" message stops hello sample application from running.</span></span>

![Пример приложения с сообщениями включения и отключения](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_on_and_off_c.png)

<span data-ttu-id="d6211-128">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="d6211-128">Congratulations!</span></span> <span data-ttu-id="d6211-129">Сообщения приветствия, которые отправляются с вашего центра IoT tooPi успешно настроен.</span><span class="sxs-lookup"><span data-stu-id="d6211-129">You’ve successfully customized hello messages that are sent tooPi from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="d6211-130">Сводка</span><span class="sxs-lookup"><span data-stu-id="d6211-130">Summary</span></span>
<span data-ttu-id="d6211-131">Этот дополнительный раздел показывает способ toocustomize сообщений, чтобы пример приложения hello мог управлять hello и отключать поведение hello Индикатор по-разному.</span><span class="sxs-lookup"><span data-stu-id="d6211-131">This optional section demonstrates how toocustomize messages so that hello sample application can control hello on and off behavior of hello LED in a different way.</span></span>
