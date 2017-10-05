---
title: "Приступая к работе с имитацией устройства и шлюзом Azure IoT. Урок 2. Регистрация устройства | Документация Майкрософт"
description: 
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Центр Интернета вещей, облако Интернета вещей, создание устройства в Центре Интернета вещей Azure, TI SensorTag, TI BLE"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 23cfbe21-22c6-4fe1-ae41-63714a897f12
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5557989453eb47e4c3a287b26603eff040eb1d96
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-azure-iot-hub-and-register-your-device"></a>Создание Центра Интернета вещей Azure и регистрация устройства

## <a name="what-you-will-do"></a>Выполняемая задача

- Создание группы ресурсов
- Создание первого Центра Интернета вещей.
- Регистрация устройства в собственном Центре Интернета вещей с помощью Azure CLI. 

При регистрации устройства в собственном Центре Интернета вещей служба Центра Интернета вещей Azure создает ключ для устройства, используемый для аутентификации в службе. 

Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>Новые знания

Из этого урока вы узнаете:

- Как создать Центр Интернета вещей с помощью Azure CLI.
- Как зарегистрировать устройство в Центре Интернета вещей.

## <a name="what-you-need"></a>Необходимые элементы

- Активная подписка Azure. Если у вас нет учетной записи Azure, можно создать [бесплатную учетную запись Azure](http://azure.microsoft.com/pricing/free-trial/) всего за несколько минут.
- У вас должен быть установлен Azure CLI.

## <a name="create-an-iot-hub"></a>Создание центра IoT

Чтобы создать Центр Интернета вещей, сделайте следующее:

1. Войдите в свою учетную запись Azure с помощью следующей команды:

   ```bash
   az login
   ```

   После входа отобразится список всех доступных подписок Azure.

2. Определите подписку Azure, которую необходимо использовать по умолчанию, выполнив следующую команду:

   ```bash
   az account set --subscription {subscription id or name}
   ```

   Значение `subscription ID or name` можно найти в выходных данных команды `az login` или `az account list`.

3. Зарегистрируйте поставщик с помощью следующей команды. Поставщики ресурсов — это службы, предоставляющие ресурсы для приложения. Поставщик следует регистрировать перед развертыванием ресурса Azure, предлагаемого поставщиком.

   ```bash
   az provider register -n "Microsoft.Devices"
   ```

4. Создайте группу ресурсов с именем `iot-gateway` в регионе "Западная часть США", выполнив следующую команду:

   ```bash
   az group create --name iot-gateway --location westus
   ```
   
   `westus` — это расположение, в котором создается группа ресурсов. Чтобы использовать другое расположение, выполните команду `az account list-locations -o table` и просмотрите все расположения, поддерживаемые Azure.

5. Создайте Центр Интернета вещей в группе ресурсов `iot-gateway`, выполнив следующую команду:

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-gateway
   ```

По умолчанию создается Центр Интернета вещей уровня "Бесплатный". Дополнительные сведения см. на странице [Центр Интернета вещей Azure — Цены](https://azure.microsoft.com/pricing/details/iot-hub/).

> [!NOTE]
> Имя Центра Интернета вещей должно быть глобально уникальным. В подписке Azure можно создать только один выпуск Центра Интернета вещей категории F1.

## <a name="register-your-device-in-your-iot-hub"></a>Регистрация устройства в Центре Интернета вещей

Каждое устройство, которое отправляет сообщения в ваш Центр Интернета вещей и получает сообщения из него, должно быть зарегистрировано с использованием уникального идентификатора.
Зарегистрируйте устройство в Центре Интернета вещей, используя следующую команду:

```bash
az iot device create --device-id mydevice --hub-name {my hub name} --resource-group iot-gateway
```

## <a name="summary"></a>Сводка

Вы создали Центр Интернета вещей и зарегистрировали в нем логическое устройство с идентификатором устройства. Теперь можно перейти к настройке и запуску примера приложения шлюза, используемого для отправки данных с физического устройства в Центр Интернета вещей, находящийся в облаке.

## <a name="next-steps"></a>Дальнейшие действия
[Configure and run a simulated device cloud upload sample application](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md) (Настройка и запуск примера приложения отправки в облако для имитации устройства)