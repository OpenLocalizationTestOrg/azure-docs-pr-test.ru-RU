---
title: "Подключения Arduino tooAzure IoT — Lesson 2: регистрации устройства | Документы Microsoft"
description: "Создание группы ресурсов, создать центр Azure IoT и зарегистрировать Wi-Fi M0 Растушевка Adafruit в центр Azure IoT hello с помощью hello Azure CLI."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "подключение arduino toocloud, центр azure iot, Интернет вещей облака, центр azure iot создать устройство, arduino облака"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 5edc690b-7a1d-4ebc-b011-ff27bfffe6e8
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ca362f9c143dd3a98bf47a66b63a9725a0ffc2d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-your-adafruit-feather-m0-wifi-arduino-board"></a>Создание Центра Интернета вещей Azure и регистрация платы Adafruit Feather M0 WiFi

## <a name="what-you-will-do"></a>Выполняемая задача
* Создайте группу ресурсов.
* Создайте концентратор Azure IoT в группе ресурсов hello.
* Добавьте концентратор Azure IoT toohello Arduino доски с помощью hello Azure командной строки (CLI Azure).

При использовании hello Azure CLI tooadd ваш центр IoT Arduino tooyour плата hello службы создает ключ для вашей tooauthenticate плата Arduino со службой hello. Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок][troubleshoot].

## <a name="what-you-will-learn"></a>Новые знания
В этой статье вы узнаете следующее:
* Как toouse hello Azure CLI toocreate центр IoT.
* Как toocreate удостоверение устройства для вашей Arduino плата в концентратор IoT.

## <a name="what-you-need"></a>Необходимые элементы
* Учетная запись Azure.
* Установлены на компьютере с hello Azure CLI

## <a name="create-your-iot-hub"></a>Создание Центра Интернета вещей
Центр Интернета вещей Azure позволяет подключать и отслеживать миллионы ресурсов Интернета вещей и управлять ими. toocreate концентратор IoT, выполните следующие действия:

1. Войдите в tooyour учетная запись Azure, выполнив следующую команду hello:

   ```bash
   az login
   ```

   После входа отобразится список всех доступных подписок Azure.

2. Установить подписку по умолчанию hello требуется toouse, выполнив следующую команду hello:

   ```bash
   az account set --subscription {subscription id or name}
   ```

   `subscription ID or name`можно найти в выходных данных hello hello `az login` или hello `az account list` команды.

3. Регистрация поставщика hello, выполнив следующую команду hello. Поставщики ресурсов — это службы, предоставляющие ресурсы для приложения. Перед развертыванием hello ресурс Azure, который hello предложения поставщика необходимо зарегистрировать поставщик hello.

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. Создайте группу ресурсов с именем iot образца в области hello Запад США, выполнив следующую команду hello:

   ```bash
   az group create --name iot-sample --location westus
   ```

   `westus`— местоположение hello, создайте группу ресурсов. Если требуется toouse другое расположение, можно запустить `az account list-locations -o table` toosee все hello Azure поддерживает расположений.

5. Создаете центр IoT в группе ресурсов iot образец hello, выполнив следующую команду hello:

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

По умолчанию hello средство создает центр IoT в ценовую категорию Free hello. Дополнительные сведения см. на странице [Центр Интернета вещей Azure — Цены](https://azure.microsoft.com/pricing/details/iot-hub/).

> [!NOTE]
> имя вашего центра IoT Hello должно быть глобально уникальным.
> В подписке Azure можно создать только один выпуск Центра Интернета вещей категории F1.

## <a name="register-your-arduino-board-in-your-iot-hub"></a>Регистрация платы Arduino в Центре Интернета вещей
Каждое устройство, которое отправляет центр IoT tooyour сообщений и получает сообщения из вашего центра IoT должны быть зарегистрированы в уникальный идентификатор.

Зарегистрируйте плату Arduino в Центре Интернета вещей, используя следующую команду:

```bash
az iot device create --device-id mym0wifi --hub-name {my hub name}
```

## <a name="summary"></a>Сводка
Вы создали Центр Интернета вещей и зарегистрировали в этом центре плату Arduino с идентификатором устройства. Вы готовы toolearn способ toosend сообщений из вашего центра IoT Arduino tooyour платы.

## <a name="next-steps"></a>Дальнейшие действия
[Создание приложения Azure функции и центра IoT tooprocess и хранилище учетной записи хранилища Azure сообщения][process-and-store-iot-hub-messages].


<!-- Images and links -->

[troubleshoot]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md