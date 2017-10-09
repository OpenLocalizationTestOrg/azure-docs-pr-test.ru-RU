---
featureFlags: usabilla
title: "Подключения Raspberry Pi (узел) tooAzure IoT — Lesson 2: регистрации устройства | Документы Microsoft"
description: "Создание группы ресурсов, создать центр Azure IoT и зарегистрировать Pi в hello центра IoT реестра удостоверений с помощью Azure CLI."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "облако raspberry pi, облачное подключение pi"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 736215b6-e7e4-46f9-af30-0ded9ffa5204
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 97533298d52d1187c49a4c35ddda922d6e45c87d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-raspberry-pi-3"></a>Создание Центра Интернета вещей и регистрация Raspberry Pi 3
## <a name="what-you-will-do"></a>Выполняемая задача
* Создайте группу ресурсов.
* Создайте концентратор Azure IoT в группе ресурсов hello.
* Добавление центра Azure IoT toohello Raspberry Pi 3 с помощью hello Azure командной строки (CLI Azure).

При использовании центра IoT tooyour Pi tooadd Azure CLI hello службы создает ключ для tooauthenticate Pi со службой hello. Если у вас возникнут проблемы, поиска решения на hello [страницу устранения неполадок](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>Новые знания
В этой статье вы узнаете следующее:
* Как Azure CLI toouse toocreate центра IoT
* Как toocreate удостоверение устройства пи в концентратор IoT

## <a name="what-you-need"></a>Необходимые элементы
* Учетная запись Azure.
* Установить Mac и Windows с hello Azure CLI

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
> имя вашего центра IoT Hello должно быть глобально уникальным. В подписке Azure можно создать только один выпуск Центра Интернета вещей категории F1.

## <a name="register-pi-in-your-iot-hub"></a>Регистрация устройства Pi в Центре Интернета вещей
Каждое устройство, которое отправляет центр IoT tooyour сообщений и получает сообщения из вашего центра IoT должны быть зарегистрированы в уникальный идентификатор. Будет использоваться на Pi tooregister Azure CLI и создать самозаверяющий сертификат X.509 для проверки подлинности устройства.

Выполните следующую команду hello.

```bash
# For Windows command prompt
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir %USERPROFILE%\.iot-hub-getting-started
 
# For macOS or Ubuntu
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir ~/.iot-hub-getting-started
```

## <a name="summary"></a>Сводка
Вы создали Центр Интернета вещей и зарегистрировали в этом центре устройство Pi с идентификатором устройства. Теперь вы готовы toolearn как toosend сообщений из центра IoT tooyour Pi.

## <a name="next-steps"></a>Дальнейшие действия
[Создание приложения Azure функции и tooprocess учетной записи хранилища Azure и хранения сообщений концентратора IoT](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md)

