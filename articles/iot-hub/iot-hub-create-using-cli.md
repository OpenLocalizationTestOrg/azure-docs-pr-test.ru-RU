---
title: "aaaCreate центр IoT с помощью Azure CLI (az.py) | Документы Microsoft"
description: "Как toocreate концентратора Azure IoT с помощью hello кросс платформенных Azure CLI 2.0 (az.py)."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-hub
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 9c9639235c2ac343e6ceb9578291dafaea26ea24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-cli-20"></a>Создать центр IoT с помощью Azure CLI 2.0 hello

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a>Введение

Можно использовать toocreate Azure CLI 2.0 (az.py) и программно управлять центры Azure IoT. В этой статье показано, как toouse hello Azure CLI 2.0 (az.py) toocreate центр IoT.

Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.

* [Azure CLI (azure.js)](iot-hub-create-using-cli-nodejs.md) — hello CLI для hello классический и ресурсов развертывания модели управления.
* Azure CLI 2.0 (az.py) - hello следующего поколения CLI для управления развертывания ресурсов hello модели, как описано в этой статье.

toocomplete этого учебника требуется hello следующие:

* Активная учетная запись Azure. Если у вас нет учетной записи, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.
* [Azure CLI 2.0][lnk-CLI-install].

## <a name="sign-in-and-set-your-azure-account"></a>Выполнение входа и установка учетной записи Azure

Войдите в tooyour учетная запись Azure и выберите свою подписку.

1. Hello командной строки, выполнив hello [входа команда][lnk-login-command]:
    
    ```azurecli
    az login
    ```

    Выполните инструкции tooauthenticate hello, с помощью кода hello и войдите в tooyour учетная запись Azure через веб-браузер.

2. Если у вас несколько подписок Azure, предоставляет доступ tooall вход tooAzure hello Azure учетные записи, связанные с учетными данными. Используйте следующие hello [toolist команда hello учетных записей Azure] [ lnk-az-account-command] для toouse вы:
    
    ```azurecli
    az account list 
    ```

    Используется следующая команда tooselect подписки требуется toouse toorun hello команды toocreate концентратор IoT hello. Можно использовать имя подписки hello или идентификатор из hello выходные данные предыдущей команды hello:

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="create-an-iot-hub"></a>Создание Центра Интернета вещей

Используйте hello Azure CLI toocreate группы ресурсов, а затем добавьте центра IoT.

1. Создайте Центр Интернета вещей в группе ресурсов. Использовать существующую группу ресурсов, либо выполнить следующие hello [toocreate команда группу ресурсов][lnk-az-resource-command]:
    
    ```azurecli
     az group create --name {your resource group name} --location westus
    ```

    > [!TIP]
    > Hello предыдущего примера создает группы ресурсов hello в hello расположение Запад США. Можно просмотреть список доступных расположений, выполнив команду hello `az account list-locations -o table`.
    >
    >

2. Запустите следующие hello [toocreate команда центра IoT] [ lnk-az-iot-command] в группе ресурсов, с помощью глобальное уникальное имя для вашего центра IoT:
    
    ```azurecli
    az iot hub create --name {your iot hub name} --resource-group {your resource group name} --sku S1
    ```

   [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


> [!NOTE]
> Предыдущая команда Hello создает центр IoT в ценовой категории, для которой выставляются hello S1. Дополнительные сведения см. на странице с [ценами на Центр Интернета вещей Azure][lnk-iot-pricing].
>
>

## <a name="remove-an-iot-hub"></a>Удаление Центра Интернета вещей

Можно также использовать hello Azure CLI[удалить конкретный ресурс][lnk-az-resource-command], например центр IoT или удалить группу ресурсов и его ресурсам, включая все центры IoT.

toodelete центр IoT запуска hello следующую команду:

```azurecli
az iot hub delete --name {your iot hub name} --resource-group {your resource group name}
```

toodelete группу ресурсов и всех его ресурсов, выполнения hello следующих команд:

```azurecli
az group delete --name {your resource group name}
```

## <a name="next-steps"></a>Дальнейшие действия
toolearn Дополнительные сведения о разработке приложений для центра IoT см. следующие статьи hello.

* [Руководство разработчика для Центра Интернета вещей][lnk-devguide]

Изучение возможностей hello центра IoT toofurther см. в разделе:

* [С помощью hello Azure портала toomanage центра IoT][lnk-portal]

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-CLI-install]: https://docs.microsoft.com/cli/azure/install-az-cli2
[lnk-login-command]: https://docs.microsoft.com/cli/azure/get-started-with-az-cli2
[lnk-az-account-command]: https://docs.microsoft.com/cli/azure/account
[lnk-az-register-command]: https://docs.microsoft.com/cli/azure/provider
[lnk-az-addcomponent-command]: https://docs.microsoft.com/cli/azure/component
[lnk-az-resource-command]: https://docs.microsoft.com/cli/azure/resource
[lnk-az-iot-command]: https://docs.microsoft.com/cli/azure/iot
[lnk-iot-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-devguide]: iot-hub-devguide.md
[lnk-portal]: iot-hub-create-through-portal.md 
