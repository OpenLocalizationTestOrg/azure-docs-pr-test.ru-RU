---
title: "функции шаблонов диспетчера ресурсов aaaAzure - ресурсы | Документы Microsoft"
description: "Описывает toouse функции hello значения tooretrieve шаблона диспетчера ресурсов Azure о ресурсах."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/09/2017
ms.author: tomfitz
ms.openlocfilehash: c9d524b338b8b7ea6d8c9e0135d48e4fb8f167c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="resource-functions-for-azure-resource-manager-templates"></a>Функции для работы с ресурсами в шаблонах Azure Resource Manager

Диспетчер ресурсов предоставляет следующие функции для получения значений ресурсов hello:

* [listKeys и list{Value}](#listkeys)
* [providers](#providers)
* [reference](#reference)
* [resourceGroup](#resourcegroup)
* [resourceId](#resourceid)
* [subscription](#subscription)

tooget значения из параметров, переменные или hello текущего развертывания, в разделе [функции развертывания значение](resource-group-template-functions-deployment.md).

<a id="listkeys" />
<a id="list" />

## <a name="listkeys-and-listvalue"></a>listKeys и list{Value}
`listKeys(resourceName or resourceIdentifier, apiVersion)`

`list{Value}(resourceName or resourceIdentifier, apiVersion)`

Возвращает hello значения для любого типа ресурсов, которая поддерживает операции вывода списка hello. Hello наиболее распространенным вариантом применения является `listKeys`. 

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| имя_ресурса или идентификатор_ресурса |Да |string |Уникальный идентификатор для ресурса hello. |
| версия_API |Да |string |Версия API для состояния среды выполнения ресурса. Как правило, в формате hello **гггг мм дд**. |

### <a name="return-value"></a>Возвращаемое значение

Hello вернуть объект из listKeys существует hello следующий формат:

```json
{
  "keys": [
    {
      "keyName": "key1",
      "permissions": "Full",
      "value": "{value}"
    },
    {
      "keyName": "key2",
      "permissions": "Full",
      "value": "{value}"
    }
  ]
}
```

Другие функции list возвращают данные в других форматах. Формат hello toosee функции, включите ее в разделе выходы hello как показано в примере шаблон hello. 

### <a name="remarks"></a>Примечания

Любая операция, которая начинается с **list**, может быть использована в шаблоне как функция. Hello доступные операции включают не только listKeys, но также операции, такие как `list`, `listAdminKeys`, и `listStatus`. Однако нельзя использовать **списка** операции, требующие значения в hello текст запроса. Здравствуйте, например, [список учетных записей SAS](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) операция требует параметров текста запроса, например *signedExpiry*, поэтому его нельзя использовать внутри шаблона.

toodetermine операция списка имеют типы ресурсов, имеются следующие варианты hello.

* Представление hello [операции REST API](/rest/api/) для поставщика ресурсов и найти список операций. Например, учетные записи хранилища имеют hello [listKeys операции](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).
* Используйте hello [Get AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation) командлета PowerShell. Hello следующий пример возвращает все операции списка учетных записей хранилища:

  ```powershell
  Get-AzureRmProviderOperation -OperationSearchString "Microsoft.Storage/*" | where {$_.Operation -like "*list*"} | FT Operation
  ```
* Используйте следующую команду Azure CLI toofilter только hello операции списка hello.

  ```azurecli
  az provider operation show --namespace Microsoft.Storage --query "resourceTypes[?name=='storageAccounts'].operations[].name | [?contains(@, 'list')]"
  ```

Укажите ресурс hello, используя либо hello [функции resourceId](#resourceid), или в формате hello `{providerNamespace}/{resourceType}/{resourceName}`.


### <a name="example"></a>Пример

Hello следующем примере показано, как tooreturn hello первичный и вторичный ключи из учетной записи хранения в hello выводит раздел.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountId": {
            "type": "string"
        }
    },
    "resources": [],
    "outputs": {
        "storageKeysOutput": {
            "value": "[listKeys(parameters('storageAccountId'), '2016-01-01')]",
            "type" : "object"
        }
    }
}
``` 

<a id="providers" />

## <a name="providers"></a>providers
`providers(providerNamespace, [resourceType])`

Возвращает сведения о поставщике ресурсов и поддерживаемых типах ресурсов. Если тип ресурса не указано, функция hello возвращает все типы hello поддерживается для поставщика ресурсов hello.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| пространство_имен_поставщика |Да |string |Пространство имен поставщика hello |
| тип_ресурса |Нет |string |Hello тип ресурса в пределах hello указано пространство имен. |

### <a name="return-value"></a>Возвращаемое значение

Каждый поддерживаемый тип возвращается в hello следующий формат: 

```json
{
    "resourceType": "{name of resource type}",
    "locations": [ all supported locations ],
    "apiVersions": [ all supported API versions ]
}
```

Массив упорядочение hello возвращаемые значения не гарантируется.

### <a name="example"></a>Пример

Hello в следующем примере показано, как toouse hello функция поставщика:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "providerOutput": {
            "value": "[providers('Microsoft.Web', 'sites')]",
            "type" : "object"
        }
    }
}
```

Hello предыдущий пример возвращает объект в hello следующий формат:

```json
{
  "resourceType": "sites",
  "locations": [
    "South Central US",
    "North Europe",
    "West Europe",
    "Southeast Asia",
    ...
  ],
  "apiVersions": [
    "2016-08-01",
    "2016-03-01",
    "2015-08-01-preview",
    "2015-08-01",
    ...
  ]
}
```

<a id="reference" />

## <a name="reference"></a>reference
`reference(resourceName or resourceIdentifier, [apiVersion])`

Возвращает объект, представляющий состояние среды выполнения ресурса.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| имя_ресурса или идентификатор_ресурса |Да |string |Имя или уникальный идентификатор ресурса. |
| версия_API |Нет |string |Версии API-интерфейса hello указанный ресурс. Включите этот параметр, когда ресурс hello не подготовлен в пределах того же шаблона. Как правило, в формате hello **гггг мм дд**. |

### <a name="return-value"></a>Возвращаемое значение

Каждый тип ресурса возвращает различные параметры для функции hello ссылки. функция Hello не возвращает предварительно определенного формата. hello объекта в hello выводит раздела, как показано в примере hello возвращаемое toosee hello свойства для типа ресурса.

### <a name="remarks"></a>Примечания

ссылка функции Hello значения из состояния среды выполнения и таким образом, не может использоваться в разделе переменные hello. Она может использоваться в разделе выходных данных шаблона. 

С помощью функции hello ссылку, вы неявно объявляют зависимость одного ресурса на другой ресурс при hello ссылка на ресурс, предоставляется в рамках того же шаблона. Hello dependsOn tooalso используйте свойство не обязательно. Hello функции не вычисляется до hello ресурс ссылки на них завершения развертывания.

toosee hello имена и значения свойств для типа ресурса, создать шаблон, который возвращает объект hello в разделе hello выходные данные. Если у вас есть существующий ресурс этого типа, шаблон возвращает hello объекта без развертывания никаких новых ресурсов. 

Как правило, использовать hello **ссылки** функции tooreturn определенное значение из объекта, например hello BLOB-объект URI конечной точки или полное доменное имя.

```json
"outputs": {
    "BlobUri": {
        "value": "[reference(concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName')), '2016-01-01').primaryEndpoints.blob]",
        "type" : "string"
    },
    "FQDN": {
        "value": "[reference(concat('Microsoft.Network/publicIPAddresses/', parameters('ipAddressName')), '2016-03-30').dnsSettings.fqdn]",
        "type" : "string"
    }
}
```

### <a name="example"></a>Пример

Справочник и toodeploy ресурс hello в hello того же шаблона, используйте:

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "storageAccountName": { 
          "type": "string"
      }
  },
  "resources": [
    {
      "name": "[parameters('storageAccountName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-12-01",
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {
      }
    }
  ],
  "outputs": {
      "referenceOutput": {
          "type": "object",
          "value": "[reference(parameters('storageAccountName'))]"
      }
    }
}
``` 

Hello предыдущий пример возвращает объект в hello следующий формат:

```json
{
   "creationTime": "2017-06-13T21:24:46.618364Z",
   "primaryEndpoints": {
     "blob": "https://examplestorage.blob.core.windows.net/",
     "file": "https://examplestorage.file.core.windows.net/",
     "queue": "https://examplestorage.queue.core.windows.net/",
     "table": "https://examplestorage.table.core.windows.net/"
   },
   "primaryLocation": "southcentralus",
   "provisioningState": "Succeeded",
   "statusOfPrimary": "available",
   "supportsHttpsTrafficOnly": false
}
```

Hello следующий пример ссылается на учетную запись хранилища, который не развернут в этом шаблоне. Hello учетной записи хранения уже существует в пределах hello же группе ресурсов.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountName": {
            "type": "string"
        }
    },
    "resources": [],
    "outputs": {
        "ExistingStorage": {
            "value": "[reference(concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName')), '2016-01-01')]",
            "type" : "object"
        }
    }
}
```

<a id="resourcegroup" />

## <a name="resourcegroup"></a>resourceGroup
`resourceGroup()`

Возвращает объект, представляющий hello текущей группе ресурсов. 

### <a name="return-value"></a>Возвращаемое значение

Hello вернул объект находится в hello следующий формат:

```json
{
  "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}",
  "name": "{resourceGroupName}",
  "location": "{resourceGroupLocation}",
  "tags": {
  },
  "properties": {
    "provisioningState": "{status}"
  }
}
```

### <a name="remarks"></a>Примечания

Обычно группа ресурсов функции hello используется toocreate ресурсы hello местоположения hello группы ресурсов. Hello следующий пример использует расположение hello tooassign расположение группы ресурсов hello веб-сайта.

```json
"resources": [
   {
      "apiVersion": "2016-08-01",
      "type": "Microsoft.Web/sites",
      "name": "[parameters('siteName')]",
      "location": "[resourceGroup().location]",
      ...
   }
]
```

### <a name="example"></a>Пример

Hello следующий шаблон возвращает hello свойства группы ресурсов hello.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[resourceGroup()]",
            "type" : "object"
        }
    }
}
```

Hello предыдущий пример возвращает объект в hello следующий формат:

```json
{
  "id": "/subscriptions/{subscription-id}/resourceGroups/examplegroup",
  "name": "examplegroup",
  "location": "southcentralus",
  "properties": {
    "provisioningState": "Succeeded"
  }
}
```

<a id="resourceid" />

## <a name="resourceid"></a>resourceId
`resourceId([subscriptionId], [resourceGroupName], resourceType, resourceName1, [resourceName2]...)`

Возвращает hello уникальный идентификатор ресурса. Эта функция используется, когда имя ресурса hello является неоднозначным или не инициализировано внутри hello того же шаблона. 

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| subscriptionId |Нет |строка (в формате GUID) |Значение по умолчанию — hello текущей подписки. Задайте это значение, когда требуется tooretrieve ресурс в другую подписку. |
| имя_группы_ресурсов |Нет |string |Значение по умолчанию — текущая группа ресурсов. Задайте это значение, когда требуется tooretrieve ресурсов в другой группе ресурсов. |
| тип_ресурса |Да |string |Тип ресурса, включая пространство имен поставщика ресурсов. |
| имя_ресурса1 |Да |string |Имя ресурса. |
| имя_ресурса2 |Нет |string |Имя следующего ресурса, если ресурс является вложенным. |

### <a name="return-value"></a>Возвращаемое значение

возвращается идентификатор Hello в hello следующий формат:

```json
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}
```

### <a name="remarks"></a>Примечания

Hello указать значения параметров зависят от того, является ли ресурс hello в hello же группу ресурса и подписки, что текущее развертывание hello.

Идентификатор ресурса hello tooget учетной записи на hello же подписке и группе ресурсов, используйте:

```json
"[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]"
```

Идентификатор ресурса hello tooget для учетной записи хранения в hello ту же подписку, но другой группе ресурсов, используйте:

```json
"[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

Используйте идентификатор ресурса hello tooget для учетной записи хранения в другой подписке и группе ресурсов:

```json
"[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

Идентификатор ресурса hello tooget базы данных в другой группе ресурсов, используйте:

```json
"[resourceId('otherResourceGroup', 'Microsoft.SQL/servers/databases', parameters('serverName'), parameters('databaseName'))]"
```

Часто требуется toouse эту функцию при использовании учетной записи хранилища или виртуальной сети в группе ресурсов альтернативный. Hello следующем примере показано, как ресурс из группы внешних ресурсов можно легко использовать:

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "virtualNetworkName": {
          "type": "string"
      },
      "virtualNetworkResourceGroup": {
          "type": "string"
      },
      "subnet1Name": {
          "type": "string"
      },
      "nicName": {
          "type": "string"
      }
  },
  "variables": {
      "vnetID": "[resourceId(parameters('virtualNetworkResourceGroup'), 'Microsoft.Network/virtualNetworks', parameters('virtualNetworkName'))]",
      "subnet1Ref": "[concat(variables('vnetID'),'/subnets/', parameters('subnet1Name'))]"
  },
  "resources": [
  {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[parameters('nicName')]",
      "location": "[parameters('location')]",
      "properties": {
          "ipConfigurations": [{
              "name": "ipconfig1",
              "properties": {
                  "privateIPAllocationMethod": "Dynamic",
                  "subnet": {
                      "id": "[variables('subnet1Ref')]"
                  }
              }
          }]
       }
  }]
}
```

### <a name="example"></a>Пример

Hello следующий пример возвращает идентификатор ресурса hello для учетной записи хранилища в группе ресурсов hello.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "sameRGOutput": {
            "value": "[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "differentRGOutput": {
            "value": "[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "differentSubOutput": {
            "value": "[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "nestedResourceOutput": {
            "value": "[resourceId('Microsoft.SQL/servers/databases', 'serverName', 'databaseName')]",
            "type" : "string"
        }
    }
}
```

Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:

| Имя | Тип | Значение |
| ---- | ---- | ----- |
| sameRGOutput | Строка | /subscriptions/{ИД_текущей_подписки}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage |
| differentRGOutput | Строка | /subscriptions/{ИД_текущей_подписки}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage |
| differentSubOutput | Строка | /subscriptions/{ИД_другой_подписки}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage |
| nestedResourceOutput | Строка | /subscriptions/{ИД_текущей_подписки}/resourceGroups/examplegroup/providers/Microsoft.SQL/servers/serverName/databases/databaseName |

<a id="subscription" />

## <a name="subscription"></a>Подписка
`subscription()`

Возвращает сведения о подписке hello для текущего развертывания hello. 

### <a name="return-value"></a>Возвращаемое значение

функция Hello возвращает hello следующий формат:

```json
{
    "id": "/subscriptions/{subscription-id}",
    "subscriptionId": "{subscription-id}",
    "tenantId": "{tenant-id}",
    "displayName": "{name-of-subscription}"
}
```

### <a name="example"></a>Пример

Hello пример hello подписки функцию с именем раздела hello выходные данные. 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[subscription()]",
            "type" : "object"
        }
    }
}
```

## <a name="next-steps"></a>Дальнейшие действия
* Описание разделов hello в шаблоне диспетчера ресурсов Azure см. в разделе [шаблоны разработки Azure Resource Manager](resource-group-authoring-templates.md).
* toomerge несколько шаблонов, см. раздел [с помощью шаблонов, связанных с диспетчером ресурсов Azure](resource-group-linked-templates.md).
* tooiterate указанное число раз при создании типа ресурса в разделе [создание нескольких экземпляров ресурсов в диспетчере ресурсов Azure](resource-group-create-multiple.md).
* toosee toodeploy hello шаблон был создан, в статье [развернуть приложение с помощью шаблона Azure Resource Manager](resource-group-template-deploy.md).

