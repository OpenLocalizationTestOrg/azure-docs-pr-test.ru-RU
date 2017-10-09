---
title: "изменения tooprevent aaaLock ресурсы Azure | Документы Microsoft"
description: "Запрет на обновление или удаление критических ресурсов Azure для пользователей путем применения блокировки для всех пользователей и ролей."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 53c57e8f-741c-4026-80e0-f4c02638c98b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: tomfitz
ms.openlocfilehash: 1f0d8911b2b129069bd2f01a9a4ec0a3cf700118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="lock-resources-tooprevent-unexpected-changes"></a>Заблокировать tooprevent ресурсы непредвиденные изменения 
С правами администратора может потребоваться toolock подписки, группы ресурсов или ресурсов tooprevent другим пользователям в организации от случайного удаления или изменения критическим ресурсам. Можно задать уровень блокировки hello слишком**CanNotDelete** или **ReadOnly**. 

* **CanNotDelete** означает авторизованные пользователи по-прежнему можно считывать и изменять ресурс, но они не могут удалить ресурс hello. 
* **Только для чтения** означает авторизованные пользователи могут читать ресурс, но их нельзя удалить или обновить ресурс hello. Применение этой блокировкой — примерно toorestricting всех авторизованных пользователей toohello разрешения, предоставляемые hello **чтения** роли. 

## <a name="how-locks-are-applied"></a>Применение блокировок

При применении блокировки в родительской области всех ресурсов в этой области наследуют hello же блокировку. Даже ресурсы, которые позже можно добавить блокировки hello наследовать родительской hello. наиболее строгие блокировки Hello в наследовании hello имеет более высокий приоритет.

В отличие от управления доступом на основе ролей используйте tooapply блокировки управления ограничение для всех пользователей и ролей. toolearn о предоставлении разрешений пользователям и ролям, в разделе [управления доступом на основе ролей Azure](../active-directory/role-based-access-control-configure.md).

Диспетчер ресурсов блокировка применяется только toooperations возможно в плоскости управления hello, который состоит из операции, отправленные слишком`https://management.azure.com`. Hello блокировки не ограничивают как ресурсы выполнять свои функции. Ограничиваются изменения ресурсов, но не операции с ними. Например блокировку только для чтения для базы данных SQL предотвращает удаление или изменение hello базы данных, но он не препятствуют создание, обновление или удаление данных в базе данных hello. Данные транзакций разрешены, так как эти операции не отправляются слишком`https://management.azure.com`.

Применение **ReadOnly** может привести toounexpected результатов, так как некоторые операции могут показаться чтения операции фактически требуют дополнительных действий. Например, поместив **ReadOnly** блокировку учетной записи хранилища запрещает всем пользователям со списком ключей hello. Список Hello ключи операция обрабатывается с помощью запроса POST, поскольку hello вернул ключи будут доступны для операций записи. Еще один пример размещения **ReadOnly** блокировка на ресурс приложения службы предотвращает отображение файлов для ресурсов hello, так как для этого диалога требуется доступ на запись обозревателя серверов Visual Studio.

## <a name="who-can-create-or-delete-locks-in-your-organization"></a>Кто может создавать и удалять блокировки в вашей организации
блокировки управления toocreate или delete, необходимо иметь доступ слишком`Microsoft.Authorization/*` или `Microsoft.Authorization/locks/*` действия. Hello встроенных ролей, только **владельца** и **администратор доступа пользователя** предоставляются эти действия.

## <a name="portal"></a>Microsoft Azure
[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="template"></a>Шаблон
Hello примере показан шаблон, который создает блокировку для учетной записи хранилища. на какие tooapply блокировки hello предоставляется как параметр учетной записи хранилища Hello. Hello имя hello блокировок создается путем объединения hello имя ресурса с **/Microsoft.Authorization/** и в этом случае hello имя блокировки hello **myLock**.

предоставленный тип Hello — toohello определенного типа ресурсов. Для хранения данных значение too"Microsoft.Storage/storageaccounts/providers/locks типа hello».

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "lockedResource": {
          "type": "string"
        }
      },
      "resources": [
        {
          "name": "[concat(parameters('lockedResource'), '/Microsoft.Authorization/myLock')]",
          "type": "Microsoft.Storage/storageAccounts/providers/locks",
          "apiVersion": "2015-01-01",
          "properties": {
            "level": "CannotDelete"
          }
        }
      ]
    }

## <a name="powershell"></a>PowerShell
Блокировку можно развернуть ресурсы с помощью Azure PowerShell с помощью hello [New AzureRmResourceLock](/powershell/module/azurerm.resources/new-azurermresourcelock) команды.

toolock ресурс, укажите имя hello hello ресурса, его тип ресурса и его имя группы ресурсов.

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockSite `
  -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

toolock группу ресурсов, укажите имя hello hello группы ресурсов.

```powershell
New-AzureRmResourceLock -LockName LockGroup -LockLevel CanNotDelete `
  -ResourceGroupName exampleresourcegroup
```

tooget сведения о блокировке. Используйте [Get AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock). tooget все блокировки hello в подписке, используйте:

```powershell
Get-AzureRmResourceLock
```

tooget все блокировки для ресурса, используйте:

```powershell
Get-AzureRmResourceLock -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

tooget все блокировки для группы ресурсов, используйте:

```powershell
Get-AzureRmResourceLock -ResourceGroupName exampleresourcegroup
```

Azure PowerShell предоставляет другие команды для блокировки работы, таких как [набор AzureRmResourceLock](/powershell/module/azurerm.resources/set-azurermresourcelock) tooupdate блокировку, и [AzureRmResourceLock удаление](/powershell/module/azurerm.resources/remove-azurermresourcelock) toodelete блокировку.

## <a name="azure-cli"></a>Инфраструктура CLI Azure

Блокировку можно развернуть ресурсами с помощью Azure CLI с помощью hello [az блокировки создания](/cli/azure/lock#create) команды.

toolock ресурс, укажите имя hello hello ресурса, его тип ресурса и его имя группы ресурсов.

```azurecli
az lock create --name LockSite --lock-type CanNotDelete \
  --resource-group exampleresourcegroup --resource-name examplesite \
  --resource-type Microsoft.Web/sites
```

toolock группу ресурсов, укажите имя hello hello группы ресурсов.

```azurecli
az lock create --name LockGroup --lock-type CanNotDelete \
  --resource-group exampleresourcegroup
```

tooget сведения о блокировке. Используйте [списку блокировки az](/cli/azure/lock#list). tooget все блокировки hello в подписке, используйте:

```azurecli
az lock list
```

tooget все блокировки для ресурса, используйте:

```azurecli
az lock list --resource-group exampleresourcegroup --resource-name examplesite \
  --namespace Microsoft.Web --resource-type sites --parent ""
```

tooget все блокировки для группы ресурсов, используйте:

```azurecli
az lock list --resource-group exampleresourcegroup
```

Azure CLI предоставляет другие команды для блокировки работы, таких как [az блокировки обновления](/cli/azure/lock#update) tooupdate блокировку, и [удалить блокировки az](/cli/azure/lock#delete) toodelete блокировку.

## <a name="rest-api"></a>Интерфейс REST API
Можно заблокировать развернутые ресурсы с hello [API REST для управления блокировками](https://docs.microsoft.com/rest/api/resources/managementlocks). Hello REST API позволяет toocreate и удаление блокировок и получать сведения о существующей блокировки.

toocreate блокировку, запустите:

    PUT https://management.azure.com/{scope}/providers/Microsoft.Authorization/locks/{lock-name}?api-version={api-version}

Hello область может быть подписки, группы ресурсов или ресурсов. Hello имя блокировки — вы можете toocall hello блокировки. В качестве версии API (api-version) используйте значение **2015-01-01**.

В запросе hello включите объект JSON, задающий набор свойств hello hello блокировки.

    {
      "properties": {
        "level": "CanNotDelete",
        "notes": "Optional text notes."
      }
    } 

## <a name="next-steps"></a>Дальнейшие действия
* Дополнительные сведения о работе с блокировкой ресурсов см. в статье [Блокировка ресурсов Azure](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx).
* toolearn о логически организации ресурсов, в разделе [Using теги tooorganize ресурсов](resource-group-using-tags.md)
* toochange, какую группу ресурсов ресурс находится в разделе [переместить группу ресурсов toonew ресурсов](resource-group-move-resources.md)
* Ограничения и соглашения можно применять внутри подписки с помощью настраиваемых политик. Дополнительные сведения см. в разделе [политика использования ресурсов toomanage и контроля доступа](resource-manager-policy.md).
* Для получения рекомендаций по как предприятия могут использовать диспетчер ресурсов tooeffectively управление подписками см. в разделе [корпоративные функции формирования шаблонов - управление конкретные подписки](resource-manager-subscription-governance.md).

