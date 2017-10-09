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
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a>Изменить hello и отключать поведение hello Индикатора
## <a name="what-you-will-do"></a>Выполняемая задача
Настройте hello toochange сообщений hello, Индикатор, включение и отключение поведение. Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) Adafruit Растушевка M0 Wi-Fi Arduino плата.

## <a name="what-you-will-learn"></a>Новые знания
Используйте дополнительные hello toochange функции Arduino, Индикатор, включение и отключение поведение.

## <a name="what-you-need"></a>Необходимые элементы
Необходимо успешно выполнить [запуска примеров приложений в облаке tooreceive Arduino доски сообщений toodevice][receive-cloud-to-device-messages].

## <a name="add-functions-toomainc-and-gulpfilejs"></a>Добавление функций toomain.c и gulpfile.js
1. Откройте пример приложения hello в коде Visual Studio, выполнив следующие команды hello:

   ```bash
   cd Lesson4
   code .
   ```
2. Откройте hello `app.ino` файл, а затем добавьте следующие функции после blinkLED() функции hello:

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
3. Добавьте следующие условия перед hello hello `else if` блок hello `receiveMessageCallback` функции:

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
   };
   ```

   ![Файл gulpfile.js с добавленной функцией][gulp-file-js]
5. В hello `sendMessage` функционировать, замените строку hello `var message = buildMessage(sentMessageCount);` с новую строку hello показано hello, следующий фрагмент кода:

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. Сохраните все изменения hello.

### <a name="deploy-and-run-hello-sample-application"></a>Развертывание и запуск образца приложения hello
Развертывание и запуск образца приложения hello на доске Arduino, выполнив следующую команду hello:

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

Вы увидите hello Индикатор, включите для двух секунд, а затем выключите для другой две секунды. Последнее сообщение Hello «остановить» останавливает образец приложения hello запуск.

![on и off][on-and-off]

Поздравляем! Сообщения приветствия, отправляемыми плата Arduino tooyour ваш центр IoT успешно настроен.

### <a name="summary"></a>Сводка
Этот дополнительный раздел показывает способ toocustomize сообщений, чтобы пример приложения hello мог управлять hello и отключать поведение hello Индикатор по-разному.

<!-- Images and links -->

[receive-cloud-to-device-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-send-cloud-to-device-messages.md
[app-ino-file]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_app_ino.png
[gulp-file-js]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_gulpfile_js.png
[on-and-off]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/gulp_on_and_off_arduino.png