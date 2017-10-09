---
title: "aaaCreate частного реестра контейнера Docker - Azure CLI | Документы Microsoft"
description: "Начать создание и управление ими частных реестрах контейнера Docker с hello Azure CLI 2.0"
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: na
tags: 
keywords: 
ms.assetid: 29e20d75-bf39-4f7d-815f-a2e47209be7d
ms.service: container-registry
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: nepeters
ms.custom: na
ms.openlocfilehash: 2cadf42db0681a09c95486510f1e65c6f87c5280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-container-registry-using-hello-azure-cli"></a>Создание управляемого контейнера реестра, с помощью hello Azure CLI

Реестр контейнеров Azure — это управляемая служба реестра контейнеров Docker, используемая для хранения частных образов контейнеров Docker. В этом руководстве рассматривается создание экземпляра управляемого реестра контейнера Azure с помощью hello Azure CLI.

Управляемые реестры контейнеров Azure находятся на стадии предварительной версии и не доступны во всех регионах.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Если выбрать tooinstall и использовать hello CLI локально, краткого руководства требуется управлением hello Azure CLI версия 2.0.4 или более поздней версии. Запустите `az --version` версии toofind hello. Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-a-resource-group"></a>Создание группы ресурсов

Создание группы ресурсов с hello [Создание группы az](/cli/azure/group#create) команды. Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими. 

Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *westcentralus* расположение.

```azurecli-interactive 
az group create --name myResourceGroup --location westcentralus
```

## <a name="create-a-container-registry"></a>Создание реестра контейнеров

Создание экземпляра контроля доступа с помощью hello [создать az acr](/cli/azure/acr#create) команды.

> [!NOTE]
> При создании реестра укажите глобально уникальное доменное имя верхнего уровня, содержащее только буквы и цифры.

 Имя реестра Hello в примере hello *myContainerRegistry1*, подставьте собственные уникальное имя.

```azurecli
az acr create --name myContainerRegistry1 --resource-group myResourceGroup --sku Managed_Standard
```

При создании реестра hello hello выводится примерно следующее toohello:

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-29T04:50:28.607134+00:00",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myContainerRegistry1",
  "location": "westcentralus",
  "loginServer": "mycontainerregistry1.azurecr.io",
  "name": "myContainerRegistry1",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "sku": {
    "name": "Managed_Standard",
    "tier": "Managed"
  },
  "storageAccount": null,
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

## <a name="log-in-tooacr-instance"></a>Войдите в экземпляр tooACR

Перед принудительной отправки и извлекать образы контейнеров, необходимо войти в экземпляр toohello контроля доступа. toodo таким образом, используйте hello [входа acr az](/cli/azure/acr#login) команды.

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

Команда Hello возвращает сообщение «Успешно выполнен вход» после завершения.

## <a name="use-azure-container-registry"></a>Использование реестра контейнеров Azure

### <a name="list-container-images"></a>Список образов контейнеров

Используйте hello `az acr` CLI команды tooquery hello изображения и теги в репозитории.

> [!NOTE]
> В настоящее время реестре контейнеров не поддерживает hello `docker search` tooquery команды для изображений и теги.

### <a name="list-repositories"></a>Вывод списка репозиториев

Hello следующий пример формирует список репозиториев hello в реестре, в формате JSON (JavaScript Object Notation).

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a>Вывод списка тегов

Hello следующий пример отображает список тегов hello на hello **образцы/nginx** репозитория, в формате JSON:

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a>Дальнейшие действия

В этом кратком руководстве вы создали экземпляр управляемого реестра контейнера Azure, используя hello Azure CLI.

> [!div class="nextstepaction"]
> [Принудительная первый образ с помощью hello Docker CLI](container-registry-get-started-docker-cli.md)
