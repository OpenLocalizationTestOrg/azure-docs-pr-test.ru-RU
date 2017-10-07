---
title: "Connect Intel Edison (C) tooAzure IoT — Lesson 2: регистрации устройства | Документы Microsoft"
description: "Создание группы ресурсов, создать центр Azure IoT и зарегистрируйте Edison в центр Azure IoT hello с помощью hello Azure CLI."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: 
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 80bfc3cd-a1fc-4775-8994-d8033381dd3d
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 9635e916425883d65793d0ed46843ab49b3f35ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-intel-edison"></a>Создание Центра Интернета вещей и регистрация Intel Edison
## <a name="what-you-will-do"></a>Выполняемая задача
* Создайте группу ресурсов.
* Создайте концентратор Azure IoT в группе ресурсов hello.
* Центр Azure IoT toohello Intel Edison добавьте с помощью hello Azure командной строки (CLI Azure).

При использовании hello Azure CLI tooadd центр IoT tooyour Edison hello службы создает ключ для tooauthenticate Edison со службой hello. Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок][troubleshooting].

## <a name="what-you-will-learn"></a>Новые знания
В этой статье вы узнаете следующее:
* Как toouse hello Azure CLI toocreate центр IoT.
* Как toocreate удостоверение устройства для Edison в ваш центр IoT.

## <a name="what-you-need"></a>Необходимые элементы
* Учетная запись Azure. Если ее нет, можно создать [бесплатную пробную учетную запись Azure](http://azure.microsoft.com/pricing/free-trial/) всего за несколько минут.
* Необходимо иметь hello установлен Azure CLI.

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


## <a name="register-edison-in-your-iot-hub"></a>Регистрация устройства Edison в Центре Интернета вещей
Каждое устройство, которое отправляет центр IoT tooyour сообщений и получает сообщения из вашего центра IoT должны быть зарегистрированы в уникальный идентификатор.

Зарегистрируйте устройство Edison в Центре Интернета вещей, выполнив следующую команду:

```bash
az iot device create --device-id myinteledison --hub-name {my hub name}
```

## <a name="summary"></a>Сводка
Вы создали Центр Интернета вещей и зарегистрировали в нем устройство Edison с идентификатором устройства. Теперь вы готовы toolearn как toosend сообщений из центра IoT tooyour Edison.

## <a name="next-steps"></a>Дальнейшие действия
[Создание приложения Azure функции и центра IoT tooprocess и хранилище учетной записи хранилища Azure сообщения][process-and-store-iot-hub-messages].


<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-c-lesson3-deploy-resource-manager-template.md