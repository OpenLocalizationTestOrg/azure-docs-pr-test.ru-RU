---
title: "Подключение Edison Intel (узел) tooAzure IoT — занятия 4: hello Индикатор мигает | Документы Microsoft"
description: "Настройте hello toochange сообщений hello, Индикатор, включение и отключение поведение."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "управление светодиодным индикатором с помощью Arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 387cd97e-b05e-43c4-b252-f68ad45d524a
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: caeabe311fd1698f298c6d2b4a203ecad80ef7df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a><span data-ttu-id="d9cd9-104">Изменить hello и отключать поведение hello Индикатора</span><span class="sxs-lookup"><span data-stu-id="d9cd9-104">Change hello on and off behavior of hello LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="d9cd9-105">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="d9cd9-105">What you will do</span></span>
<span data-ttu-id="d9cd9-106">Настройте hello toochange сообщений hello, Индикатор, включение и отключение поведение.</span><span class="sxs-lookup"><span data-stu-id="d9cd9-106">Customize hello messages toochange hello LED’s on and off behavior.</span></span> <span data-ttu-id="d9cd9-107">Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="d9cd9-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="d9cd9-108">Новые знания</span><span class="sxs-lookup"><span data-stu-id="d9cd9-108">What you will learn</span></span>
<span data-ttu-id="d9cd9-109">Используйте дополнительные функции toochange hello Индикатор, включение и отключение поведение.</span><span class="sxs-lookup"><span data-stu-id="d9cd9-109">Use additional functions toochange hello LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="d9cd9-110">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="d9cd9-110">What you need</span></span>
<span data-ttu-id="d9cd9-111">Необходимо успешно выполнить [запуска примеров приложений в облаке tooreceive Intel Edison сообщения toodevice][receive-cloud-to-device-messages].</span><span class="sxs-lookup"><span data-stu-id="d9cd9-111">You must have successfully completed [Run a sample application on Intel Edison tooreceive cloud toodevice messages][receive-cloud-to-device-messages].</span></span>

## <a name="add-functions-tooappjs-and-gulpfilejs"></a><span data-ttu-id="d9cd9-112">Добавление функций tooapp.js и gulpfile.js</span><span class="sxs-lookup"><span data-stu-id="d9cd9-112">Add functions tooapp.js and gulpfile.js</span></span>
1. <span data-ttu-id="d9cd9-113">Откройте пример приложения hello в коде Visual Studio, выполнив следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="d9cd9-113">Open hello sample application in Visual Studio code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="d9cd9-114">Откройте hello `app.js` файл, а затем добавьте следующие функции после blinkLED() функции hello:</span><span class="sxs-lookup"><span data-stu-id="d9cd9-114">Open hello `app.js` file, and then add hello following functions after blinkLED() function:</span></span>

   ```javascript
   function turnOnLED() {
     myLed.write(1);
   }

   function turnOffLED() {
     myLed.write(0);
   }
   ```

   ![Файл app.js с добавленными функциями](media/iot-hub-intel-edison-lessons/lesson4/updated_app_node.png)
3. <span data-ttu-id="d9cd9-116">Добавить hello следующих условий перед hello «blink» регистром блока switch case hello hello `receiveMessageCallback` функции:</span><span class="sxs-lookup"><span data-stu-id="d9cd9-116">Add hello following conditions before hello 'blink' case in hello switch-case block of hello `receiveMessageCallback` function:</span></span>

   ```javascript
   case 'on':
     turnOnLED();
     break;
   case 'off':
     turnOffLED();
     break;
   ```

   <span data-ttu-id="d9cd9-117">Теперь вы настроили hello образец приложения toorespond toomore инструкции с помощью сообщений.</span><span class="sxs-lookup"><span data-stu-id="d9cd9-117">Now you’ve configured hello sample application toorespond toomore instructions through messages.</span></span> <span data-ttu-id="d9cd9-118">Hello «на «инструкция включает Индикатор hello и hello, «off» инструкция отключает hello Индикатора.</span><span class="sxs-lookup"><span data-stu-id="d9cd9-118">hello "on" instruction turns on hello LED, and hello "off" instruction turns off hello LED.</span></span>
4. <span data-ttu-id="d9cd9-119">Откройте файл gulpfile.js hello, а затем добавьте новую функцию перед функцией hello `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="d9cd9-119">Open hello gulpfile.js file, and then add a new function before hello function `sendMessage`:</span></span>

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

   ![Файл gulpfile.js с добавленной функцией][gulpfile]
5. <span data-ttu-id="d9cd9-121">В hello `sendMessage` функционировать, замените строку hello `var message = buildMessage(sentMessageCount);` с новую строку hello показано hello, следующий фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="d9cd9-121">In hello `sendMessage` function, replace hello line `var message = buildMessage(sentMessageCount);` with hello new line shown in hello following snippet:</span></span>

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="d9cd9-122">Сохраните все изменения hello.</span><span class="sxs-lookup"><span data-stu-id="d9cd9-122">Save all hello changes.</span></span>

### <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="d9cd9-123">Развертывание и запуск образца приложения hello</span><span class="sxs-lookup"><span data-stu-id="d9cd9-123">Deploy and run hello sample application</span></span>
<span data-ttu-id="d9cd9-124">Развертывание и запуск образца приложения hello на Edison, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="d9cd9-124">Deploy and run hello sample application on Edison by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="d9cd9-125">Вы увидите hello Индикатор, включите для двух секунд, а затем выключите для другой две секунды.</span><span class="sxs-lookup"><span data-stu-id="d9cd9-125">You should see hello LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="d9cd9-126">Последнее сообщение Hello «остановить» останавливает образец приложения hello запуск.</span><span class="sxs-lookup"><span data-stu-id="d9cd9-126">hello last "stop" message stops hello sample application from running.</span></span>

![on и off][on-and-off]

<span data-ttu-id="d9cd9-128">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="d9cd9-128">Congratulations!</span></span> <span data-ttu-id="d9cd9-129">Сообщения приветствия, которые отправляются с вашего центра IoT tooEdison успешно настроен.</span><span class="sxs-lookup"><span data-stu-id="d9cd9-129">You’ve successfully customized hello messages that are sent tooEdison from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="d9cd9-130">Сводка</span><span class="sxs-lookup"><span data-stu-id="d9cd9-130">Summary</span></span>
<span data-ttu-id="d9cd9-131">Этот дополнительный раздел показывает способ toocustomize сообщений, чтобы пример приложения hello мог управлять hello и отключать поведение hello Индикатор по-разному.</span><span class="sxs-lookup"><span data-stu-id="d9cd9-131">This optional section demonstrates how toocustomize messages so that hello sample application can control hello on and off behavior of hello LED in a different way.</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-node-lesson4-send-cloud-to-device-messages.md
[gulpfile]: media/iot-hub-intel-edison-lessons/lesson4/updated_gulpfile_node.png
[on-and-off]: media/iot-hub-intel-edison-lessons/lesson4/gulp_on_and_off_node.png
