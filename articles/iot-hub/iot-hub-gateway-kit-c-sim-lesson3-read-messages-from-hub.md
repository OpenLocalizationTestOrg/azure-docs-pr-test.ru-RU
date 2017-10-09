---
title: "Приступая к работе с имитацией устройства и шлюзом Azure IoT. Урок 3. Чтение сообщений | Документация Майкрософт"
description: "Запустите образец кода на сообщения hello tooread компьютера узла из вашего центра IoT."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "данные в облако hello, сбор данных облака, iot облачной службы, iot данных"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 5a6ec9c1-d83c-41c1-beaf-7c0d3395d77f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 540575724bb5cdac4db581a226d8a02a59004d8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-from-your-iot-hub"></a>Чтение сообщений из Центра Интернета вещей

## <a name="what-you-will-do"></a>Выполняемая задача

- Запустите образец кода на вашем узле компьютер tooread сообщения из вашего центра IoT.

Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>Новые знания

Как toouse hello gulp средство tooread сообщения от вашего центра IoT.

## <a name="what-you-need"></a>Необходимые элементы

- Образец Hello имитированное устройство в [настроить и запустить имитированное устройство облака отправить образец приложения](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).

## <a name="get-your-iot-hub-and-device-connection-strings"></a>Получение строк подключения Центра Интернета вещей и устройства

Строка подключения устройства Hello используется ваш центр IoT tooyour tooconnect имитированное устройство. Строка подключения концентратора IoT Hello — реестра удостоверений toohello tooconnect используется в вашей IoT hub toomanage hello устройства, которым разрешен центра IoT tooyour tooconnect.

- Перечислить все центры IoT в группе ресурсов, выполнив следующую команду hello:

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   Используйте `iot-gateway` в качестве значения hello `{resource group name}` Если вы не были изменены.
- Получите строку подключения концентратора IoT hello, выполнив следующую команду hello:

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   `{my hub name}`— Имя hello, указаны в занятии 2.

## <a name="configure-hello-device-connection-for-hello-sample-code"></a>Настройка подключения устройства hello hello образец кода

Обновить IoT hub устройства подключения конфигураций и в `config-azure.json` , выполнив следующие шаги hello:

1. Откройте `config-azure.json` в коде Visual Studio, выполнив следующую команду в окне консоли hello:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. Сделать после замены в hello hello `config-azure.json` файла:

   ![снимок экрана настройки Azure](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   Замените `[IoT hub connection string]` с hello строка подключения концентратора IoT.

## <a name="read-messages-from-your-iot-hub"></a>Чтение сообщений из Центра Интернета вещей

Запустить образец приложения hello имитируемые устройства и прочитаны центра IoT сообщений hello следующую команду:

```bash
gulp run --iot-hub
```

Команда Hello выполняет приложение hello, отправляет сообщения центр IoT tooyour каждые 2 секунды. Оно также создает сообщение hello tooreceive дочерних процесса.

сообщения приветствия, отправки и получения всех отображаемых мгновенно на hello же консоли окна в hello хост-компьютера. приложение Hello завершит работу в 40 секунд.

![Имитация примера приложения с отправленными и полученными сообщениями](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub_simudev.png)

## <a name="summary"></a>Сводка

После успешного выполнения tooyour центр IoT приложений toosend hello образец данных с устройств, имитация. Также прочтения сообщений hello, которые были отправлены tooyour центр IoT.

## <a name="next-steps"></a>Дальнейшие действия
[Создание учетной записи хранения Azure и приложения-функции Azure](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)


