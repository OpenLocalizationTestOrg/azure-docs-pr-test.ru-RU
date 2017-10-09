---
title: "aaaCreate центр IoT с помощью Azure CLI (azure.js) | Документы Microsoft"
description: "Как toocreate концентратора Azure IoT с помощью hello кросс платформенных Azure CLI (azure.js)."
services: iot-hub
documentationcenter: .net
author: BeatriceOltean
manager: timlt
editor: 
ms.assetid: 46a17831-650c-41d9-b228-445c5bb423d3
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/04/2017
ms.author: boltean
ms.openlocfilehash: c2a7ea98500b0a0e55a39f4cdfea4605c92add94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-cli"></a>Создать центр IoT с помощью hello Azure CLI

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a>Введение

Можно использовать toocreate Azure CLI (azure.js) и программно управлять центры Azure IoT. В этой статье показано, как toouse hello Azure CLI (azure.js) toocreate центр IoT.

Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.

* Azure CLI (azure.js) — hello CLI для классического hello и моделями развертывания ресурсов управления как описано в этой статье.
* [2.0 Azure CLI (az.py)](iot-hub-create-using-cli.md) -hello следующего поколения CLI для модели развертывания hello ресурса управления.

toocomplete этого учебника требуется hello следующие:

* Активная учетная запись Azure. Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.
* [Интерфейс командной строки Azure 0.10.4][lnk-CLI-install] или более поздней версии. Если уже hello Azure CLI установлен, можно проверить hello текущей версии hello командной строки с hello следующую команду:

```azurecli
azure --version
```

> [!NOTE]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Azure Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md). Hello Azure CLI должен находиться в режиме диспетчера ресурсов Azure:
>
> ```azurecli
> azure config mode arm
> ```

## <a name="set-your-azure-account-and-subscription"></a>Настройка учетной записи и подписки Azure

1. В командной строке hello входа, введя следующую команду hello:

   ```azurecli
    azure login
   ```

   Используйте hello предлагаемые веб-браузер и tooauthenticate кода.
1. Если у вас несколько подписок Azure, подключение tooAzure предоставляет вам доступ tooall hello подписок Azure, связанных с учетными данными. Можно просмотреть hello подписок Azure и определить, какой из них по умолчанию hello, с помощью команды hello:

   ```azurecli
    azure account list
   ```

   контекст hello подписки tooset из которой требуется rest hello toorun hello команд с помощью:

   ```azurecli
    azure account set <subscription name>
   ```

1. Создайте группу ресурсов с именем **exampleResourceGroup**, если она не создана:

   ```azurecli
    azure group create -n exampleResourceGroup -l westus
   ```

> [!TIP]
> статья Hello [использовать toomanage Azure CLI hello Azure ресурсов и групп ресурсов] [ lnk-CLI-arm] предоставляет дополнительные сведения о том, как toouse hello Azure CLI toomanage Azure ресурсы.

## <a name="create-an-iot-hub"></a>Создание Центра Интернета вещей

Ниже перечислены необходимые параметры:

```azurecli
azure iothub create -g <resource-group> -n <name> -l <location> -s <sku-name> -u <units>
```

* **resource-group**. Имя группы ресурсов Hello. Формат Hello — без учета регистра алфавитно-цифровой символ подчеркивания и дефиса, длина 1-64.
* **name**. Имя Hello hello IoT hub toobe создан. Формат Hello — без учета регистра алфавитно-цифровой символ подчеркивания и дефиса, длиной 3 50.
* **location**. Hello местоположение (регион/центра обработки данных azure) tooprovision hello центр IoT.
* **sku-name**. Имя Hello hello SKU, один из: [F1, S1, S2 и S3]. См. последний полный список hello, toohello странице цен для центра IoT.
* **units**. Hello число подготовленных единиц. Диапазон: F1 [1]; S1, S2 [1–200]; S3 [1–10]. Единицы центра IoT основаны на общее число сообщений номер count и hello устройств будет tooconnect.

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

toosee все Здравствуйте, параметры, доступные для создания, можно использовать команду hello справки в командной строке:

```azurecli
azure iothub create -h
```

Краткий пример: вызывается центра IoT toocreate **exampleIoTHubName** в группе ресурсов hello **exampleResourceGroup**, запустите hello следующую команду:

```azurecli
azure iothub create -g exampleResourceGroup -n exampleIoTHubName -l westus -k s1 -u 1
```

> [!NOTE]
> Эта команда интерфейса командной строки Azure создает стандартный центр Интернета вещей S1, за который взимается плата. Вы можете удалить центр IoT hello **exampleIoTHubName** , используя следующую команду:
>
> ```azurecli
> azure iothub delete -g exampleResourceGroup -n exampleIoTHubName
> ```

## <a name="next-steps"></a>Дальнейшие действия

toolearn Дополнительные сведения о разработке приложений для центра IoT см. в следующей статьей hello:

* [Пакеты SDK для Центра Интернета вещей][lnk-sdks]

Изучение возможностей hello центра IoT toofurther см. в разделе:

* [С помощью hello Azure портала toomanage центра IoT][lnk-portal]

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-CLI-install]:../cli-install-nodejs.md
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-CLI-arm]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md

[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-portal]: iot-hub-create-through-portal.md 
