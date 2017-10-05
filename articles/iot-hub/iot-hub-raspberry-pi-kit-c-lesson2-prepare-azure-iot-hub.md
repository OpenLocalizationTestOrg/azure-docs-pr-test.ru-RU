---
title: "Подключение Raspberry Pi (C) к Интернету вещей Azure. Урок 2. Регистрация устройства | Документация Майкрософт"
description: "Создание группы ресурсов и Центра Интернета вещей Azure, а также регистрация устройства Pi в Центре Интернета вещей Azure с помощью Azure CLI."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "облако raspberry pi, облачное подключение pi"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 4bcfb071-b3ae-48cc-8ea5-7e7434732287
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d7bfd8f6ae8d15dfe09f06a40a4ab415ff2e0a7c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-iot-hub-and-register-raspberry-pi-3"></a>Создание Центра Интернета вещей и регистрация Raspberry Pi 3
## <a name="what-you-will-do"></a>Выполняемая задача
* Создайте группу ресурсов.
* Создайте Центр Интернета вещей Azure в группе ресурсов.
* Добавьте устройство Raspberry Pi 3 в Центр Интернета вещей Azure с помощью интерфейса командной строки Azure (Azure CLI).

При использовании Azure CLI для добавления Pi в Центр Интернета вещей служба создает ключ для устройства Pi, чтобы выполнить в службе его аутентификацию. Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Новые знания
В этой статье вы узнаете следующее:
* Как создать Центр Интернета вещей с помощью Azure CLI.
* Создание удостоверения устройства для Pi в Центре Интернета вещей.

## <a name="what-you-need"></a>Необходимые элементы
* Учетная запись Azure.
* Компьютер под управлением Mac или Windows с установленным интерфейсом командной строки Azure.

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
> Имя Центра Интернета вещей должно быть глобально уникальным. В подписке Azure можно создать только один выпуск Центра Интернета вещей категории F1.

## <a name="register-pi-in-your-iot-hub"></a>Регистрация устройства Pi в Центре Интернета вещей
Каждое устройство, которое отправляет сообщения в ваш Центр Интернета вещей и получает сообщения из него, должно быть зарегистрировано с использованием уникального идентификатора.

Зарегистрируйте устройство Pi в центре, используя следующую команду:

```bash
az iot device create --device-id myraspberrypi --hub {my hub name} --resource-group iot-sample
```

## <a name="summary"></a>Сводка
Вы создали Центр Интернета вещей и зарегистрировали в этом центре устройство Pi с идентификатором устройства. Теперь можно перейти к отправке сообщений с устройства Pi в Центр Интернета вещей.

## <a name="next-steps"></a>Дальнейшие действия
[Создание приложения-функции Azure и учетной записи хранения Azure](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).

