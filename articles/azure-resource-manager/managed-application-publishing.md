---
title: "aaaCreate и публикации каталога управляемого приложения службы Azure | Документы Microsoft"
description: "Показывает, как toocreate Azure управляемые приложения, предназначенные для членов вашей организации."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/23/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 31f2f9e3b50f57dae7f4dcf2edefa7366bfff25c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-managed-application-for-internal-consumption"></a>Публикация управляемого приложения для внутреннего использования

Вы можете создавать и публиковать [управляемые приложения Azure](managed-application-overview.md), предназначенные для членов вашей организации. Например, отдел ИТ может публиковать управляемые приложения, которые обеспечивают соответствие стандартам организации. Эти управляемые приложения доступны через каталог услуг hello, hello Azure Marketplace.

toopublish для каталога услуг hello управляемого приложения, необходимо выполнить следующее:

* Создайте ZIP-пакете, содержащий три файла требуемый шаблон hello.
* Определите, какой пользователь, группа или приложения должен получить доступ к toohello группы ресурсов в подписке hello пользователя.
* Создание определения hello управляемого приложения, которое указывает toohello ZIP-архив и запрашивает доступ к идентификатору hello.

## <a name="create-a-managed-application-package"></a>Создание пакета управляемого приложения

Hello прежде всего три файла требуемый шаблон toocreate hello. Упаковать все три файла в ZIP-файл и отправьте его tooan доступном месте, например в учетной записи хранилища. При создании hello управляемое определение приложения передать ссылку toothis ZIP-файл.

* **applianceMainTemplate.json**: этот файл определяет hello Azure ресурсов, предоставляемых в составе приветствия управляемого приложения. шаблон Hello ничем не отличается от обычных шаблона диспетчера ресурсов. Например toocreate учетной записи хранилища через управляемого приложения applianceMainTemplate.json содержит:

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountNamePrefix": {
            "type": "string"
        }
    },
    "resources": [
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat(parameters('storageAccountNamePrefix'), uniqueString(resourceGroup().id))]",
            "apiVersion": "2016-01-01",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {}
        }
    ],
    "outputs": {}
  }
  ```

* **mainTemplate.json**: пользователи развертывают этот шаблон при создании hello управляемых приложений. Он определяет ресурса hello управляемого приложения, который является Microsoft.Solutions/appliances типа ресурса. Этот файл содержит все параметры hello, необходимое для ресурсов hello в applianceMainTemplate.json.

  В этом шаблоне задаются два важных свойства. Во-первых, hello **applianceDefinitionId** свойство — идентификатор hello определение hello управляемого приложения. Создайте определение hello далее в этом разделе. При установке этого параметра, необходимо решить, какие подписки и toouse группы ресурсов для хранения hello определения управляемого приложения. И необходимо решить, имя определения hello. Идентификатор Hello имеет формат hello:

  `/subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Solutions/applianceDefinitions/<definition-name>`

  Во-вторых, hello **managedResourceGroupId** свойство — идентификатор hello hello группы ресурсов, где hello Azure ресурсы создаются. Можно назначить значение для этого имени группы ресурсов или позволить hello пользователя введите имя. Hello с идентификатором hello выглядит следующим образом:

  `/subscriptions/<subscription-id>/resourceGroups/<resoure-group-name>`.

  Привет, в следующем примере показан файл mainTemplate.json. Он указывает группу ресурсов для hello развертывания ресурсов. Hello идентификатор определения — toouse набор с именем определения **storageApp** в группу ресурсов с именем **managedApplicationGroup**. Можно изменить эти значения toouse разные имена. Укажите идентификатор подписки в идентификатор определения hello.

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountNamePrefix": {
            "type": "string"
        }
    },
    "variables": {
        "managedRGId": "[concat(resourceGroup().id,'-application-resources')]",
        "managedAppName": "[concat('managedStorage', uniqueString(resourceGroup().id))]"
    },
    "resources": [
        {
            "type": "Microsoft.Solutions/appliances",
            "name": "[variables('managedAppName')]",
            "apiVersion": "2016-09-01-preview",
            "location": "[resourceGroup().location]",
            "kind": "ServiceCatalog",
            "properties": {
                "managedResourceGroupId": "[variables('managedRGId')]",
                "applianceDefinitionId": "/subscriptions/<subscription-id>/resourceGroups/managedApplicationGroup/providers/Microsoft.Solutions/applianceDefinitions/storageApp",
                "parameters": {
                    "storageAccountNamePrefix": {
                        "value": "[parameters('storageAccountNamePrefix')]"
                    }
                }
            }
        }
    ]
  }
  ```

* **applianceCreateUiDefinition.json**: hello портал Azure использует этот файл toogenerate hello пользовательский интерфейс для пользователей, создающих hello управляемого приложения. Можно определить способ ввода каждого параметра пользователями. например раскрывающийся список, текстовое поле, поле ввода пароля или другие средства ввода. toocreate файл определения пользовательского интерфейса для управляемого приложения. в статье toolearn [Приступая к работе с CreateUiDefinition](managed-application-createuidefinition-overview.md).

  Hello следующем примере показан файл applianceCreateUiDefinition.json, позволяющий пользователям toospecify hello хранилища учетной записи префикс имени через текстового поля.

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json",
    "handler": "Microsoft.Compute.MultiVm",
    "version": "0.1.2-preview",
    "parameters": {
        "basics": [
            {
                "name": "storageAccounts",
                "type": "Microsoft.Common.TextBox",
                "label": "Storage account name prefix",
                "defaultValue": "storage",
                "toolTip": "Provide a value that is used for hello prefix of your storage account. Limit too11 characters.",
                "constraints": {
                    "required": true,
                    "regex": "^[a-z0-9A-Z]{1,11}$",
                    "validationMessage": "Only alphanumeric characters are allowed, and hello value must be 1-11 characters long."
                },
                "visible": true
            }
        ],
        "steps": [],
        "outputs": {
            "storageAccountNamePrefix": "[basics('storageAccounts')]"
        }
    }
  }
  ```

При готовности все файлы hello требуется упаковать их как ZIP-файл. Hello три файлы должны находиться на корневом уровне hello hello ZIP-файл. Если поместить их в папке при создании hello управляемых определение приложения о том, что файлы отсутствуют требуемые hello сообщение об ошибке. Отправьте hello пакета tooan доступное расположение, из которых могут быть использованы. Hello оставшейся части этой статьи предполагается, что существует hello ZIP-файла в контейнер больших двоичных объектов хранилища общего доступа.

## <a name="create-an-azure-active-directory-user-group-or-application"></a>Создание группы пользователей или приложения Azure Active Directory

второй шаг Hello — tooselect группы пользователей или приложения для управления ресурсами hello от имени клиента hello. Данной группы пользователей или приложения имеет разрешения на hello управляемого ресурса группы соответствующим toohello роль, назначенная. Hello роль может быть любой встроенной роли управления доступом на основе ролей (RBAC), например владельца или участника. Также можно предоставить отдельному пользователю разрешение toomanage hello ресурсов, но обычно назначается разрешение tooa пользователя группы. toocreate группу пользователей Active Directory в разделе [Создание группы и добавление членов в Azure Active Directory](../active-directory/active-directory-groups-create-azure-portal.md).

Требуется идентификатор hello объекта группы toouse hello пользователя для управления ресурсами hello. Hello в следующем примере показано, как tooget hello идентификатор объекта из группы hello отображаемого имени:

```azurecli-interactive
az ad group show --group exampleGroupName
```

Hello примере команда возвращает hello следующие выходные данные:

```azurecli
{
    "displayName": "exampleGroupName",
    "mail": null,
    "objectId": "9aabd3ad-3716-4242-9d8e-a85df479d5d9",
    "objectType": "Group",
    "securityEnabled": true
}
```

Идентификатор объекта просто hello tooretrieve, использование

```azurecli-interactive
groupid=$(az ad group show --group exampleGroupName --query objectId --output tsv)
```

## <a name="get-hello-role-definition-id"></a>Получить идентификатор определения роли hello

Далее необходимо идентификатор определения роли hello hello RBAC встроенная роль, нужно toogrant доступа toohello пользователей, группы пользователей или приложение. Как правило используется hello владельца или роль участника или чтения. Hello, следующая команда показывает, как tooget hello идентификатор определения роли для роли владельца hello:


```azurecli-interactive
az role definition list --name owner
```

Эта команда возвращает hello следующие выходные данные:

```azurecli
{
    "id": "/subscriptions/<subscription-id>/providers/Microsoft.Authorization/roleDefinitions/8e3af657-a8ff-443c-a75c-2fe8c4bcb635",
    "name": "8e3af657-a8ff-443c-a75c-2fe8c4bcb635",
    "properties": {
      "assignableScopes": [
        "/"
      ],
      "description": "Lets you manage everything, including access tooresources.",
      "permissions": [
        {
          "actions": [
            "*"
         ],
         "notActions": []
        }
      ],
      "roleName": "Owner",
      "type": "BuiltInRole"
    },
    "type": "Microsoft.Authorization/roleDefinitions"
}
```

Вы должны hello значение свойства «имя» hello из предшествующих пример hello. Вы можете получить только это свойство, выполнив следующую команду.

```azurecli-interactive
roleid=$(az role definition list --name Owner --query [].name --output tsv)
```

## <a name="create-hello-managed-application-definition"></a>Создайте определение приложения hello управляемых

Если у вас еще нет группы ресурсов для хранения определения управляемого приложения, создайте ее.

```azurecli-interactive
az group create --name managedApplicationGroup --location westcentralus
```

Теперь можно Создайте определение ресурса hello управляемого приложения.

```azurecli-interactive
az managedapp definition create \
  --name storageApp \
  --location "westcentralus" \
  --resource-group managedApplicationGroup \
  --lock-level ReadOnly \
  --display-name myteststorageapp \
  --description storageapp \
  --authorizations "$groupid:$roleid" \
  --package-file-uri <uri-path-to-zip-file>
```

используются следующие параметры Hello, используемый в предыдущих пример hello.

* **Группа ресурсов**: hello имя группы ресурсов hello, где hello управляемое определение приложения создается.
* **уровень блокировки**: hello тип блокировки включен в группу hello управляемых ресурсов. Они препятствуют клиента hello нежелательных операций в этой группе ресурсов. В настоящее время только для чтения — hello поддерживается только уровень блокировки. Если указан только для чтения, hello клиентов можно только для чтения hello ресурсы в группе hello управляемых ресурсов.
* **параметры авторизации**: описывает идентификатор участника hello и hello идентификатор определения роли, которые toohello управляемого ресурса используется toogrant разрешений группы. Он указан в формате hello `<principalId>:<roleDefinitionId>`. Для него можно указать несколько значений. Если требуются несколько значений, их следует указывать в форме hello `<principalId1>:<roleDefinitionId1> <principalId2>:<roleDefinitionId2>`. Разные значения разделяются пробелами.
* **uri для файла пакета**: hello расположение пакета управляемого приложения hello, содержащего файлы шаблона hello, которые могут быть BLOB-объект хранилища Azure.

## <a name="next-steps"></a>Дальнейшие действия

* Введение toomanaged приложений, в разделе [Обзор управляемого приложения](managed-application-overview.md).
* Примеры файлов hello в разделе [управляемых образцы приложений](https://github.com/Azure/azure-managedapp-samples/tree/master/samples).
* Дополнительные сведения об использовании управляемых приложений из каталога услуг см. в разделе [Использование управляемого приложения Azure](managed-application-consumption.md).
* Сведения о публикации toohello управляемые приложения Azure Marketplace см. в разделе [Azure управляемого приложения в hello Marketplace](managed-application-author-marketplace.md).
* Сведения о использование управляемого приложения из hello Marketplace в разделе [использовать Azure управляемого приложения в hello Marketplace](managed-application-consume-marketplace.md).
* toocreate файл определения пользовательского интерфейса для управляемого приложения. в статье toolearn [Приступая к работе с CreateUiDefinition](managed-application-createuidefinition-overview.md).
