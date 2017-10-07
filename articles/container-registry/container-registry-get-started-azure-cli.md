---
title: "aaaCreate частного реестра контейнера Docker - Azure CLI | Документы Microsoft"
description: "Начать создание и управление ими частных реестрах контейнера Docker с hello Azure CLI 2.0"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 29e20d75-bf39-4f7d-815f-a2e47209be7d
ms.service: container-registry
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/06/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f0d876a70b71a5e1bd564fbc9198f693dfe8a347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-cli-20"></a>Создание частного реестра контейнера Docker, с помощью Azure CLI 2.0 hello
Использование команд в hello [Azure CLI 2.0](https://github.com/Azure/azure-cli) toocreate реестре контейнеров и управлять его параметрами с компьютера Windows, Mac или Linux. Можно также создать и управлять контейнера реестры с помощью hello [портал Azure](container-registry-get-started-portal.md) или программным путем с контейнер реестра hello [API-интерфейса REST](https://go.microsoft.com/fwlink/p/?linkid=834376).


* Сведения и основные понятия, в разделе [Здравствуйте, Обзор](container-registry-intro.md)
* Для получения справки о командах CLI реестра контейнера (`az acr` команды), передать hello `-h` параметр tooany команды.


## <a name="prerequisites"></a>Предварительные требования
* **Azure CLI 2.0**: tooinstall и приступить к работе с hello CLI 2.0 см. в разделе hello [инструкции по установке](/cli/azure/install-azure-cli). Войдите в tooyour подписки Azure, выполнив `az login`. Дополнительные сведения см. в разделе [Приступая к работе с hello CLI 2.0](/cli/azure/get-started-with-azure-cli).
* **Группа ресурсов.** Перед созданием реестра контейнеров создайте [группу ресурсов](../azure-resource-manager/resource-group-overview.md#resource-groups) или используйте имеющуюся. Убедитесь, что группа ресурсов hello в место, где будет hello реестра контейнера службы [доступных](https://azure.microsoft.com/regions/services/). группы ресурсов с помощью toocreate hello CLI версии 2.0, в разделе [hello CLI 2.0 ссылка](/cli/azure/group).
* **Учетная запись хранения** (необязательно): создание стандартной Azure [учетной записи хранилища](../storage/common/storage-introduction.md) реестр контейнера hello tooback hello местоположения. Если не указать учетную запись хранилища при создании реестр с помощью `az acr create`, hello команда создает ее автоматически. учетную запись хранилища, используя toocreate hello CLI 2.0 см. в разделе [hello CLI 2.0 ссылка](/cli/azure/storage/account). Хранилище класса Premium сейчас не поддерживается.
* **Субъект-служба** (необязательно): при создании файла реестра с hello CLI по умолчанию он не настроен для доступа. В зависимости от потребностей, можно назначить существующий реестр tooa основной службы Azure Active Directory (или создать и назначить новый), или включить учетную запись пользователя admin hello реестра. Hello разделах данной статьи. Дополнительные сведения о доступе к реестра см. в разделе [аутентификация с помощью реестра контейнера hello](container-registry-authentication.md).

## <a name="create-a-container-registry"></a>Создание реестра контейнеров
Запустите hello `az acr create` toocreate команда реестра контейнера.

> [!TIP]
> При создании реестра укажите глобально уникальное доменное имя верхнего уровня, содержащее только буквы и цифры. Имя реестра Hello в примерах hello `myRegistry1`, но заменить собственным уникальное имя.
>
>

Здравствуйте, следующая команда использует hello минимальные параметры toocreate контейнер реестра `myRegistry1` в группе ресурсов hello `myResourceGroup`и с помощью hello *основные* sku:

```azurecli
az acr create --name myRegistry1 --resource-group myResourceGroup --sku Basic
```

* `--storage-account-name` является необязательным. Если не указано, учетную запись хранения создается с именем, содержащим имя реестра hello и отметка времени в hello указал группу ресурсов.

При создании реестра hello hello выводится примерно следующее toohello:

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-06T18:36:29.124842+00:00",
  "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myResourceGroup/providers/Microsoft.ContainerRegistry
/registries/myRegistry1",
  "location": "southcentralus",
  "loginServer": "myregistry1.azurecr.io",
  "name": "myRegistry1",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "myregistry123456789"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}

```


Обратите внимание на следующее.

* `id`-Идентификатор для раздела реестра hello в вашей подписке, требуется, если вы хотите tooassign участника службы.
* `loginServer`-Полное имя hello указании слишком[входа в реестре toohello](container-registry-authentication.md). В этом примере имеет имя hello `myregistry1.exp.azurecr.io` (прописными буквами).

## <a name="assign-a-service-principal"></a>Назначение субъекта-службы
С помощью команды CLI 2.0 tooassign реестр tooa основной службы Azure Active Directory. Hello участника-службы в этих примерах назначается роль владельца hello, но можно назначить [других ролей](../active-directory/role-based-access-control-configure.md) Если требуется.

### <a name="create-a-service-principal-and-assign-access-toohello-registry"></a>Создание участника службы и назначение доступа toohello реестра
В hello следующую команду, субъекта-службы назначается идентификатор владельца роли доступа toohello реестра, переданный с hello `--scopes` параметра. Укажите надежный пароль для hello `--password` параметра.

```azurecli
az ad sp create-for-rbac --scopes /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --password myPassword
```



### <a name="assign-an-existing-service-principal"></a>Назначение имеющегося субъекта-службы
Если вы уже участника службы и хотите tooassign его владельца роли доступа toohello реестра, запустите команду аналогичные toohello, следующий пример. Передайте идентификатор основного приложения службы hello, с помощью hello `--assignee` параметр:

```azurecli
az role assignment create --scope /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --assignee myAppId
```



## <a name="manage-admin-credentials"></a>Управление учетными данными администратора
Учетная запись администратора автоматически создается для каждого реестра контейнеров, но по умолчанию она отключена. Здравствуйте, следующие примеры `az acr` CLI команды toomanage hello учетные данные администратора для реестра контейнера.

### <a name="obtain-admin-user-credentials"></a>Получение учетных данных пользователя с правами администратора
```azurecli
az acr credential show -n myRegistry1
```

### <a name="enable-admin-user-for-an-existing-registry"></a>Включение пользователя с правами администратора для имеющегося реестра
```azurecli
az acr update -n myRegistry1 --admin-enabled true
```

### <a name="disable-admin-user-for-an-existing-registry"></a>Отключение пользователя с правами администратора для имеющегося реестра
```azurecli
az acr update -n myRegistry1 --admin-enabled false
```

## <a name="list-images-and-tags"></a>Вывод списка образов и тегов
Используйте hello `az acr` CLI команды tooquery hello изображения и теги в репозитории.

> [!NOTE]
> В настоящее время реестре контейнеров не поддерживает hello `docker search` tooquery команды для изображений и теги.


### <a name="list-repositories"></a>Вывод списка репозиториев
Hello следующий пример формирует список репозиториев hello в реестре, в формате JSON (JavaScript Object Notation).

```azurecli
az acr repository list -n myRegistry1 -o json
```

### <a name="list-tags"></a>Вывод списка тегов
Hello следующий пример отображает список тегов hello на hello **образцы/nginx** репозитория, в формате JSON:

```azurecli
az acr repository show-tags -n myRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a>Дальнейшие действия
* [Принудительная первый образ с помощью hello Docker CLI](container-registry-get-started-docker-cli.md)
