---
title: "Connect Intel Edison (C) tooAzure IoT — занятия 4: hello Индикатор мигает | Документы Microsoft"
description: "Настройте hello toochange сообщений hello, Индикатор, включение и отключение поведение."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "управление светодиодным индикатором с помощью Arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 9826c55a-0e24-4296-ae54-29b7fe66436a
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c51acb42aa297ca91cfe76d7b0361ad95e2fb2e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a>Изменить hello и отключать поведение hello Индикатора
## <a name="what-you-will-do"></a>Выполняемая задача
Настройте hello toochange сообщений hello, Индикатор, включение и отключение поведение. Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок][troubleshooting].

## <a name="what-you-will-learn"></a>Новые знания
Используйте дополнительные функции toochange hello Индикатор, включение и отключение поведение.

## <a name="what-you-need"></a>Необходимые элементы
Необходимо успешно выполнить [запуска примеров приложений в облаке tooreceive Intel Edison сообщения toodevice][receive-cloud-to-device-messages].

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
     mraa_gpio_write(context, 1);
   }

   static void turnOffLED()
   {
     mraa_gpio_write(context, 0);
   }
   ```

   ![Файл main.c с добавленными функциями](media/iot-hub-intel-edison-lessons/lesson4/updated_app_c.png)

3. Добавьте следующие условия перед hello hello `else if` блок hello `receiveMessageCallback` функции:

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

   ![Файл gulpfile.js с добавленной функцией][gulpfile]
5. В hello `sendMessage` функционировать, замените строку hello `var message = buildMessage(sentMessageCount);` с новую строку hello показано hello, следующий фрагмент кода:

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. Сохраните все изменения hello.

### <a name="deploy-and-run-hello-sample-application"></a>Развертывание и запуск образца приложения hello
Развертывание и запуск образца приложения hello на Edison, выполнив следующую команду hello:

```bash
gulp deploy && gulp run
```

Вы увидите hello Индикатор, включите для двух секунд, а затем выключите для другой две секунды. Последнее сообщение Hello «остановить» останавливает образец приложения hello запуск.

![on и off][on-and-off]

Поздравляем! Сообщения приветствия, которые отправляются с вашего центра IoT tooEdison успешно настроен.

### <a name="summary"></a>Сводка
Этот дополнительный раздел показывает способ toocustomize сообщений, чтобы пример приложения hello мог управлять hello и отключать поведение hello Индикатор по-разному.

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-c-lesson4-send-cloud-to-device-messages.md
[gulpfile]: media/iot-hub-intel-edison-lessons/lesson4/updated_gulpfile_c.png
[on-and-off]: media/iot-hub-intel-edison-lessons/lesson4/gulp_on_and_off_c.png
