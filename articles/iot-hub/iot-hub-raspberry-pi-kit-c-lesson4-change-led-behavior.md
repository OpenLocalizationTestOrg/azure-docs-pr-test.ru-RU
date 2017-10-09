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
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a>Изменить hello и отключать поведение hello Индикатора
## <a name="what-you-will-do"></a>Выполняемая задача
Настройте hello toochange сообщений hello, Индикатор, включение и отключение поведение. Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Новые знания
Используйте дополнительные hello toochange функции Node.js, Индикатор, включение и отключение поведение.

## <a name="what-you-need"></a>Необходимые элементы
Необходимо успешно выполнить [запуска примера приложения в облаке tooreceive Raspberry Pi toodevice сообщения](iot-hub-raspberry-pi-kit-c-lesson4-send-cloud-to-device-messages.md).

## <a name="add-functions-toomainc-and-gulpfilejs"></a>Добавление функций toomain.c и gulpfile.js
1. Откройте пример приложения hello в коде Visual Studio, выполнив следующие команды hello:

   ```bash
   cd Lesson4
   code .
   ```
2. Откройте hello `main.c` файл, а затем добавьте следующие функции после blinkLED() функции hello:

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
3. Добавьте следующую команду по умолчанию hello одного условия в hello hello `if` блок hello `receiveMessageCallback` функции:

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

   ![Файл gulpfile.js с добавленной функцией](media/iot-hub-raspberry-pi-lessons/lesson4/updated_gulpfile_c.png)
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

![Пример приложения с сообщениями включения и отключения](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_on_and_off_c.png)

Поздравляем! Сообщения приветствия, которые отправляются с вашего центра IoT tooPi успешно настроен.

### <a name="summary"></a>Сводка
Этот дополнительный раздел показывает способ toocustomize сообщений, чтобы пример приложения hello мог управлять hello и отключать поведение hello Индикатор по-разному.
