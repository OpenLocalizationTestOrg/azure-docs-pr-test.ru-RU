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
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a>Изменить hello и отключать поведение hello Индикатора
## <a name="what-you-will-do"></a>Выполняемая задача
Настройте hello toochange сообщений hello, Индикатор, включение и отключение поведение. Если у вас возникнут проблемы, поиска решения на hello [страницу устранения неполадок](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>Новые знания
Используйте дополнительные hello toochange функции Node.js, Индикатор, включение и отключение поведение.

## <a name="what-you-need"></a>Необходимые элементы
Необходимо успешно выполнить [запуска примера приложения на Raspberry Pi tooreceive сообщений облака на устройство](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md).

## <a name="add-nodejs-functions"></a>Добавление функций Node.js
1. Откройте пример приложения hello в коде Visual Studio, выполнив следующие команды hello:
   
   ```bash
   cd Lesson4
   code .
   ```
2. Откройте hello `app.js` файл, а затем добавьте следующие функции в конце hello hello:
   
   ```javascript
   function turnOnLED() {
     wpi.digitalWrite(CONFIG_PIN, 1);
   }
   
   function turnOffLED() {
     wpi.digitalWrite(CONFIG_PIN, 0);
   }
   ```
   
   ![Файл app.js с добавленными функциями](media/iot-hub-raspberry-pi-lessons/lesson4/updated_app_js.png)
3. Добавьте следующие условия по умолчанию hello один в блоке смены регистра hello hello hello `receiveMessageCallback` функции:
   
   ```javascript
   case 'on':
     turnOnLED();
     break;
   case 'off':
     turnOffLED();
     break;
   ```
   
   Теперь вы настроили hello образец приложения toorespond toomore инструкции с помощью сообщений. Hello «на «инструкция включает Индикатор hello и hello, «off» инструкция отключает hello Индикатора.
4. Откройте файл gulpfile.js hello, а затем добавьте новую функцию перед функцией hello `sendMessage`:
   
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
5. В hello `sendMessage` функционировать, замените строку hello `var message = buildMessage(sentMessageCount);` с новую строку hello показано hello, следующий фрагмент кода:
   
   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. Сохраните все изменения hello.

### <a name="deploy-and-run-hello-sample-application"></a>Развертывание и запуск образца приложения hello
Развертывание и запуск образца приложения hello на Pi, выполнив следующую команду hello:

```bash
gulp deploy && gulp run
```

Вы увидите hello Индикатор, включите для двух секунд, а затем выключите для другой две секунды. Последнее сообщение Hello «остановить» останавливает образец приложения hello запуск.

![Пример приложения с сообщениями включения и отключения](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_on_and_off.png)

Поздравляем! Сообщения приветствия, которые отправляются с вашего центра IoT tooPi успешно настроен.

### <a name="summary"></a>Сводка
Этот дополнительный раздел показывает способ toocustomize сообщений, чтобы пример приложения hello мог управлять hello и отключать поведение hello Индикатор по-разному.

