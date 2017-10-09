---
title: "Приступая к работе с устройством SensorTag и шлюзом Azure IoT. Урок 2. Регистрация устройства | Документация Майкрософт"
description: 
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Центр Интернета вещей, облако Интернета вещей, создание устройства в Центре Интернета вещей Azure, TI SensorTag, TI BLE"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 2c18f5ae-e39a-48ae-a9fe-04bb595740a0
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5d2322268aa18f52f60c2833778323773ac4eec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-azure-iot-hub-and-register-your-device"></a>Создание Центра Интернета вещей Azure и регистрация устройства

## <a name="what-you-will-do"></a>Выполняемая задача

- Создание группы ресурсов
- Создание первого Центра Интернета вещей.
- Регистрация устройства в концентратор IoT с использованием hello Azure CLI. 

При регистрации устройства в концентратор IoT, hello Azure IoT Hub service создает ключ для tooauthenticate toouse вашего устройства с помощью службы hello. 

Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Новые знания

Из этого урока вы узнаете:

- Как toouse hello Azure CLI toocreate центр IoT.
- Как tooregister устройства в центр IoT.

## <a name="what-you-need"></a>Необходимые элементы

- Активная подписка Azure. Если у вас нет учетной записи Azure, можно создать [бесплатную учетную запись Azure](http://azure.microsoft.com/pricing/free-trial/) всего за несколько минут.
- Необходимо иметь hello установлен Azure CLI.

## <a name="create-an-iot-hub"></a>Создание центра IoT

toocreate центра IoT, выполните следующие действия.

1. Войдите в tooyour учетная запись Azure, выполнив следующую команду hello:

   ```bash
   az login
   ```

   После входа отобразится список всех доступных подписок Azure.

2. Значение по умолчанию hello подписки Azure, требуется toouse, выполнив следующую команду hello:

   ```bash
   az account set --subscription {subscription id or name}
   ```

   `subscription ID or name`можно найти в выходных данных hello hello `az login` или hello `az account list` команды.

3. Регистрация поставщика hello, выполнив следующую команду hello. Поставщики ресурсов — это службы, предоставляющие ресурсы для приложения. Перед развертыванием hello ресурс Azure, который hello предложения поставщика необходимо зарегистрировать поставщик hello.

   ```bash
   az provider register -n "Microsoft.Devices"
   ```

4. Создание группы ресурсов с именем `iot-gateway` в регионе hello Запад США, выполнив следующую команду hello:

   ```bash
   az group create --name iot-gateway --location westus
   ```
   
   `westus`— местоположение hello, создайте группу ресурсов. Если требуется toouse другое расположение, можно запустить `az account list-locations -o table` toosee все hello Azure поддерживает расположений.

5. Создать центр IoT в hello `iot-gateway` группы ресурсов, выполнив следующую команду hello:

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-gateway
   ```

По умолчанию hello средство создает центр IoT в ценовую категорию Free hello. Дополнительные сведения см. на странице [Центр Интернета вещей Azure — Цены](https://azure.microsoft.com/pricing/details/iot-hub/).

> [!NOTE]
> имя вашего центра IoT Hello должно быть глобально уникальным. В подписке Azure можно создать только один выпуск Центра Интернета вещей категории F1.

## <a name="register-your-device-in-your-iot-hub"></a>Регистрация устройства в Центре Интернета вещей

Каждое устройство, которое отправляет центр IoT tooyour сообщений и получает сообщения из вашего центра IoT должны быть зарегистрированы в уникальный идентификатор.
Зарегистрируйте устройство в Центре Интернета вещей, используя следующую команду:

```bash
az iot device create --device-id mydevice --hub-name {my hub name} --resource-group iot-gateway
```

## <a name="summary"></a>Сводка

Вы создали Центр Интернета вещей и зарегистрировали в нем логическое устройство с идентификатором устройства. Теперь вы готовы toolearn об облачных tooconfigure и запустите приложение toosend шлюза образец данных из концентратор IoT tooyour физическое устройство hello.

## <a name="next-steps"></a>Дальнейшие действия
[Настройка и запуск примера приложения BLE](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)