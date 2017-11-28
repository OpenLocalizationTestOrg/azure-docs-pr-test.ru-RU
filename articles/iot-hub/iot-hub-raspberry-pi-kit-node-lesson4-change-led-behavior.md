---
title: "Подключение Raspberry Pi (Node) к Интернету вещей Azure. Урок 4. Изменение приложения | Документация Майкрософт"
description: "Настроив сообщения, вы сможете изменять режим включения и отключения светодиодного индикатора."
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
ms.openlocfilehash: b2ae23ac9cc1723936c4b4e1900b95cdcde744df
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-on-and-off-behavior-of-the-led"></a><span data-ttu-id="5d2a5-104">Изменение режима включения и отключения светодиодного индикатора</span><span class="sxs-lookup"><span data-stu-id="5d2a5-104">Change the on and off behavior of the LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="5d2a5-105">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="5d2a5-105">What you will do</span></span>
<span data-ttu-id="5d2a5-106">Настроив сообщения, вы сможете изменять режим включения и отключения светодиодного индикатора.</span><span class="sxs-lookup"><span data-stu-id="5d2a5-106">Customize the messages to change the LED’s on and off behavior.</span></span> <span data-ttu-id="5d2a5-107">Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="5d2a5-107">If you have any problems, seek solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5d2a5-108">Новые знания</span><span class="sxs-lookup"><span data-stu-id="5d2a5-108">What you will learn</span></span>
<span data-ttu-id="5d2a5-109">Использование дополнительных функций Node.js для изменения режима включения и отключения светодиодного индикатора.</span><span class="sxs-lookup"><span data-stu-id="5d2a5-109">Use additional Node.js functions to change the LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5d2a5-110">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="5d2a5-110">What you need</span></span>
<span data-ttu-id="5d2a5-111">Необходимо успешно выполнить [запуск примера приложения на устройстве Raspberry Pi для получения сообщений из облака на устройство](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md).</span><span class="sxs-lookup"><span data-stu-id="5d2a5-111">You must have successfully completed [Run a sample application on Raspberry Pi to receive cloud-to-device messages](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md).</span></span>

## <a name="add-nodejs-functions"></a><span data-ttu-id="5d2a5-112">Добавление функций Node.js</span><span class="sxs-lookup"><span data-stu-id="5d2a5-112">Add Node.js functions</span></span>
1. <span data-ttu-id="5d2a5-113">Откройте пример приложения в Visual Studio Code, выполнив следующие команды:</span><span class="sxs-lookup"><span data-stu-id="5d2a5-113">Open the sample application in Visual Studio code by running the following commands:</span></span>
   
   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="5d2a5-114">Откройте файл `app.js` и добавьте в конце следующие функции:</span><span class="sxs-lookup"><span data-stu-id="5d2a5-114">Open the `app.js` file, and then add the following functions at the end:</span></span>
   
   ```javascript
   function turnOnLED() {
     wpi.digitalWrite(CONFIG_PIN, 1);
   }
   
   function turnOffLED() {
     wpi.digitalWrite(CONFIG_PIN, 0);
   }
   ```
   
   ![Файл app.js с добавленными функциями](media/iot-hub-raspberry-pi-lessons/lesson4/updated_app_js.png)
3. <span data-ttu-id="5d2a5-116">Добавьте следующие условия перед условием по умолчанию в блоке переключения функции `receiveMessageCallback`:</span><span class="sxs-lookup"><span data-stu-id="5d2a5-116">Add the following conditions before the default one in the switch-case block of the `receiveMessageCallback` function:</span></span>
   
   ```javascript
   case 'on':
     turnOnLED();
     break;
   case 'off':
     turnOffLED();
     break;
   ```
   
   <span data-ttu-id="5d2a5-117">Теперь пример приложения настроен для ответа на дополнительные инструкции с помощью сообщений.</span><span class="sxs-lookup"><span data-stu-id="5d2a5-117">Now you’ve configured the sample application to respond to more instructions through messages.</span></span> <span data-ttu-id="5d2a5-118">Инструкция on включает светодиодный индикатор, а инструкция off его отключает.</span><span class="sxs-lookup"><span data-stu-id="5d2a5-118">The "on" instruction turns on the LED, and the "off" instruction turns off the LED.</span></span>
4. <span data-ttu-id="5d2a5-119">Откройте файл gulpfile.js и добавьте новую функцию перед функцией `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="5d2a5-119">Open the gulpfile.js file, and then add a new function before the function `sendMessage`:</span></span>
   
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
5. <span data-ttu-id="5d2a5-121">В функции `sendMessage` замените строку `var message = buildMessage(sentMessageCount);` новой строкой, показанной в следующем фрагменте:</span><span class="sxs-lookup"><span data-stu-id="5d2a5-121">In the `sendMessage` function, replace the line `var message = buildMessage(sentMessageCount);` with the new line shown in the following snippet:</span></span>
   
   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="5d2a5-122">Сохраните все изменения.</span><span class="sxs-lookup"><span data-stu-id="5d2a5-122">Save all the changes.</span></span>

### <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="5d2a5-123">Развертывание и запуск примера приложения</span><span class="sxs-lookup"><span data-stu-id="5d2a5-123">Deploy and run the sample application</span></span>
<span data-ttu-id="5d2a5-124">Разверните и запустите пример приложения на устройстве Pi, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="5d2a5-124">Deploy and run the sample application on Pi by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="5d2a5-125">Светодиодный индикатор должен включиться на две секунды, а затем на две секунды выключиться.</span><span class="sxs-lookup"><span data-stu-id="5d2a5-125">You should see the LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="5d2a5-126">Последнее сообщение stop останавливает выполнение примера приложения.</span><span class="sxs-lookup"><span data-stu-id="5d2a5-126">The last "stop" message stops the sample application from running.</span></span>

![Пример приложения с сообщениями включения и отключения](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_on_and_off.png)

<span data-ttu-id="5d2a5-128">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="5d2a5-128">Congratulations!</span></span> <span data-ttu-id="5d2a5-129">Вы успешно настроили сообщения, отправляемые на устройство Pi из Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="5d2a5-129">You’ve successfully customized the messages that are sent to Pi from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="5d2a5-130">Сводка</span><span class="sxs-lookup"><span data-stu-id="5d2a5-130">Summary</span></span>
<span data-ttu-id="5d2a5-131">В этом дополнительном разделе показано, как настроить сообщения таким образом, чтобы пример приложения мог управлять включением и отключением светодиодного индикатора разными способами.</span><span class="sxs-lookup"><span data-stu-id="5d2a5-131">This optional section demonstrates how to customize messages so that the sample application can control the on and off behavior of the LED in a different way.</span></span>

