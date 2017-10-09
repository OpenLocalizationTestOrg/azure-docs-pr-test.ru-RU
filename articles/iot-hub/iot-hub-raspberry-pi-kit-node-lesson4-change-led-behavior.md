---
title: "Подключение Raspberry Pi (узел) tooAzure IoT — занятия 4: изменить приложение | Документы Microsoft"
description: "Настройте hello toochange сообщений hello, Индикатор, включение и отключение поведение."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "управление светодиодным индикатором с помощью raspberry pi, raspberry pi управление индикатором, управлять светодиодным индикатором raspberry pi"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 3b42a4ad-0197-42f6-8ca9-04c883e879e8
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 99b542fcb8639add0f5a0f7a49dd8abd0e224a51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a><span data-ttu-id="1f889-104">Изменить hello и отключать поведение hello Индикатора</span><span class="sxs-lookup"><span data-stu-id="1f889-104">Change hello on and off behavior of hello LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="1f889-105">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="1f889-105">What you will do</span></span>
<span data-ttu-id="1f889-106">Настройте hello toochange сообщений hello, Индикатор, включение и отключение поведение.</span><span class="sxs-lookup"><span data-stu-id="1f889-106">Customize hello messages toochange hello LED’s on and off behavior.</span></span> <span data-ttu-id="1f889-107">Если у вас возникнут проблемы, поиска решения на hello [страницу устранения неполадок](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="1f889-107">If you have any problems, seek solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="1f889-108">Новые знания</span><span class="sxs-lookup"><span data-stu-id="1f889-108">What you will learn</span></span>
<span data-ttu-id="1f889-109">Используйте дополнительные hello toochange функции Node.js, Индикатор, включение и отключение поведение.</span><span class="sxs-lookup"><span data-stu-id="1f889-109">Use additional Node.js functions toochange hello LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="1f889-110">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="1f889-110">What you need</span></span>
<span data-ttu-id="1f889-111">Необходимо успешно выполнить [запуска примера приложения на Raspberry Pi tooreceive сообщений облака на устройство](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md).</span><span class="sxs-lookup"><span data-stu-id="1f889-111">You must have successfully completed [Run a sample application on Raspberry Pi tooreceive cloud-to-device messages](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md).</span></span>

## <a name="add-nodejs-functions"></a><span data-ttu-id="1f889-112">Добавление функций Node.js</span><span class="sxs-lookup"><span data-stu-id="1f889-112">Add Node.js functions</span></span>
1. <span data-ttu-id="1f889-113">Откройте пример приложения hello в коде Visual Studio, выполнив следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="1f889-113">Open hello sample application in Visual Studio code by running hello following commands:</span></span>
   
   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="1f889-114">Откройте hello `app.js` файл, а затем добавьте следующие функции в конце hello hello:</span><span class="sxs-lookup"><span data-stu-id="1f889-114">Open hello `app.js` file, and then add hello following functions at hello end:</span></span>
   
   ```javascript
   function turnOnLED() {
     wpi.digitalWrite(CONFIG_PIN, 1);
   }
   
   function turnOffLED() {
     wpi.digitalWrite(CONFIG_PIN, 0);
   }
   ```
   
   ![Файл app.js с добавленными функциями](media/iot-hub-raspberry-pi-lessons/lesson4/updated_app_js.png)
3. <span data-ttu-id="1f889-116">Добавьте следующие условия по умолчанию hello один в блоке смены регистра hello hello hello `receiveMessageCallback` функции:</span><span class="sxs-lookup"><span data-stu-id="1f889-116">Add hello following conditions before hello default one in hello switch-case block of hello `receiveMessageCallback` function:</span></span>
   
   ```javascript
   case 'on':
     turnOnLED();
     break;
   case 'off':
     turnOffLED();
     break;
   ```
   
   <span data-ttu-id="1f889-117">Теперь вы настроили hello образец приложения toorespond toomore инструкции с помощью сообщений.</span><span class="sxs-lookup"><span data-stu-id="1f889-117">Now you’ve configured hello sample application toorespond toomore instructions through messages.</span></span> <span data-ttu-id="1f889-118">Hello «на «инструкция включает Индикатор hello и hello, «off» инструкция отключает hello Индикатора.</span><span class="sxs-lookup"><span data-stu-id="1f889-118">hello "on" instruction turns on hello LED, and hello "off" instruction turns off hello LED.</span></span>
4. <span data-ttu-id="1f889-119">Откройте файл gulpfile.js hello, а затем добавьте новую функцию перед функцией hello `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="1f889-119">Open hello gulpfile.js file, and then add a new function before hello function `sendMessage`:</span></span>
   
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
   
   ![Файл gulpfile.js с добавленной функцией](media/iot-hub-raspberry-pi-lessons/lesson4/updated_gulpfile.png)
5. <span data-ttu-id="1f889-121">В hello `sendMessage` функционировать, замените строку hello `var message = buildMessage(sentMessageCount);` с новую строку hello показано hello, следующий фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="1f889-121">In hello `sendMessage` function, replace hello line `var message = buildMessage(sentMessageCount);` with hello new line shown in hello following snippet:</span></span>
   
   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="1f889-122">Сохраните все изменения hello.</span><span class="sxs-lookup"><span data-stu-id="1f889-122">Save all hello changes.</span></span>

### <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="1f889-123">Развертывание и запуск образца приложения hello</span><span class="sxs-lookup"><span data-stu-id="1f889-123">Deploy and run hello sample application</span></span>
<span data-ttu-id="1f889-124">Развертывание и запуск образца приложения hello на Pi, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="1f889-124">Deploy and run hello sample application on Pi by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="1f889-125">Вы увидите hello Индикатор, включите для двух секунд, а затем выключите для другой две секунды.</span><span class="sxs-lookup"><span data-stu-id="1f889-125">You should see hello LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="1f889-126">Последнее сообщение Hello «остановить» останавливает образец приложения hello запуск.</span><span class="sxs-lookup"><span data-stu-id="1f889-126">hello last "stop" message stops hello sample application from running.</span></span>

![Пример приложения с сообщениями включения и отключения](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_on_and_off.png)

<span data-ttu-id="1f889-128">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="1f889-128">Congratulations!</span></span> <span data-ttu-id="1f889-129">Сообщения приветствия, которые отправляются с вашего центра IoT tooPi успешно настроен.</span><span class="sxs-lookup"><span data-stu-id="1f889-129">You’ve successfully customized hello messages that are sent tooPi from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="1f889-130">Сводка</span><span class="sxs-lookup"><span data-stu-id="1f889-130">Summary</span></span>
<span data-ttu-id="1f889-131">Этот дополнительный раздел показывает способ toocustomize сообщений, чтобы пример приложения hello мог управлять hello и отключать поведение hello Индикатор по-разному.</span><span class="sxs-lookup"><span data-stu-id="1f889-131">This optional section demonstrates how toocustomize messages so that hello sample application can control hello on and off behavior of hello LED in a different way.</span></span>

