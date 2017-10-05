---
title: "Подключение Arduino к Интернету вещей Azure. Урок 2. Регистрация устройства | Документация Майкрософт"
description: "Создайте группу ресурсов и Центр Интернета вещей Azure, а также зарегистрируйте плату Adafruit Feather M0 WiFi в Центре Интернета вещей Azure, используя Azure CLI."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "подключение Arduino к облаку, Центр Интернета вещей Azure, облако Интернета вещей, создание устройства Центра Интернета вещей Azure, облако Arduino"
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
ms.openlocfilehash: c5ad5e900671c7cedd3cdad2c2aa345315de223b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-iot-hub-and-register-your-adafruit-feather-m0-wifi-arduino-board"></a>Создание Центра Интернета вещей Azure и регистрация платы Adafruit Feather M0 WiFi

## <a name="what-you-will-do"></a>Выполняемая задача
* Создайте группу ресурсов.
* Создайте Центр Интернета вещей Azure в группе ресурсов.
* Добавьте плату Arduino в Центр Интернета вещей Azure, используя интерфейс командной строки Azure (Azure CLI).

При использовании интерфейса командной строки Azure для добавления платы Arduino в Центр Интернета вещей служба создает ключ для платы Arduino, чтобы аутентифицировать его в службе. Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок][troubleshoot].

## <a name="what-you-will-learn"></a>Новые знания
В этой статье вы узнаете следующее:
* Как создать Центр Интернета вещей с помощью Azure CLI.
* Создание удостоверения устройства для платы Arduino в Центре Интернета вещей Azure.

## <a name="what-you-need"></a>Необходимые элементы
* Учетная запись Azure.
* Компьютер с установленным интерфейсом командной строки Azure.

## <a name="create-your-iot-hub"></a>Создание Центра Интернета вещей
Центр Интернета вещей Azure позволяет подключать и отслеживать миллионы ресурсов Интернета вещей и управлять ими. Выполните следующие действия, чтобы создать Центр Интернета вещей:

1. Войдите в свою учетную запись Azure с помощью следующей команды:

   ```bash
   az login
   ```

   После входа отобразится список всех доступных подписок Azure.

2. Укажите подписку, которую необходимо использовать по умолчанию, выполнив следующую команду.

   ```bash
   az account set --subscription {subscription id or name}
   ```

   Значение `subscription ID or name` можно найти в выходных данных команды `az login` или `az account list`.

3. Зарегистрируйте поставщик с помощью следующей команды. Поставщики ресурсов — это службы, предоставляющие ресурсы для приложения. Поставщик следует регистрировать перед развертыванием ресурса Azure, предлагаемого поставщиком.

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. Создайте группу ресурсов с именем iot-sample в западном регионе США, выполнив следующую команду:

   ```bash
   az group create --name iot-sample --location westus
   ```

   `westus` — это расположение, в котором создается группа ресурсов. Чтобы использовать другое расположение, выполните команду `az account list-locations -o table` и просмотрите все расположения, поддерживаемые Azure.

5. Создайте Центр Интернета вещей в группе ресурсов iot-sample, выполнив следующую команду:

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

По умолчанию создается Центр Интернета вещей уровня "Бесплатный". Дополнительные сведения см. на странице [Центр Интернета вещей Azure — Цены](https://azure.microsoft.com/pricing/details/iot-hub/).

> [!NOTE]
> Имя Центра Интернета вещей должно быть глобально уникальным.
> В подписке Azure можно создать только один выпуск Центра Интернета вещей категории F1.

## <a name="register-your-arduino-board-in-your-iot-hub"></a>Регистрация платы Arduino в Центре Интернета вещей
Каждое устройство, которое отправляет сообщения в ваш Центр Интернета вещей и получает сообщения из него, должно быть зарегистрировано с использованием уникального идентификатора.

Зарегистрируйте плату Arduino в Центре Интернета вещей, используя следующую команду:

```bash
az iot device create --device-id mym0wifi --hub-name {my hub name}
```

## <a name="summary"></a>Сводка
Вы создали Центр Интернета вещей и зарегистрировали в этом центре плату Arduino с идентификатором устройства. Теперь можно перейти к отправке сообщений с платы Arduino в Центр Интернета вещей.

## <a name="next-steps"></a>Дальнейшие действия
[Создание приложения-функции Azure и учетной записи хранения Azure][process-and-store-iot-hub-messages].


<!-- Images and links -->

[troubleshoot]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md