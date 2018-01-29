---
title: "Структура и синтаксис шаблона Azure Resource Manager | Документация Майкрософт"
description: "Описывается создание структуры и свойств шаблонов Azure Resource Manager с помощью декларативного синтаксиса JSON."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/13/2017
ms.author: tomfitz
ms.openlocfilehash: 89e4b52e7d306bd495c426bcf775f59d0f30eb55
ms.sourcegitcommit: 0e4491b7fdd9ca4408d5f2d41be42a09164db775
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="resources-section-of-azure-resource-manager-templates"></a>Раздел ресурсов шаблонов диспетчера ресурсов Azure

В разделе resources определяются ресурсы, которые развертываются или обновляются. Этот раздел может еще больше усложниться, так как вы должны понимать принципы работы развертываемых типов для предоставления правильных значений.

## <a name="available-properties"></a>Доступные свойства

Ресурсы определяются с помощью следующей структуры:

```json
"resources": [
  {
      "condition": "<boolean-value-whether-to-deploy>",
      "apiVersion": "<api-version-of-resource>",
      "type": "<resource-provider-namespace/resource-type-name>",
      "name": "<name-of-the-resource>",
      "location": "<location-of-resource>",
      "tags": {
          "<tag-name1>": "<tag-value1>",
          "<tag-name2>": "<tag-value2>"
      },
      "comments": "<your-reference-notes>",
      "copy": {
          "name": "<name-of-copy-loop>",
          "count": "<number-of-iterations>",
          "mode": "<serial-or-parallel>",
          "batchSize": "<number-to-deploy-serially>"
      },
      "dependsOn": [
          "<array-of-related-resource-names>"
      ],
      "properties": {
          "<settings-for-the-resource>",
          "copy": [
              {
                  "name": ,
                  "count": ,
                  "input": {}
              }
          ]
      },
      "resources": [
          "<array-of-child-resources>"
      ]
  }
]
```

| Имя элемента | Требуется | ОПИСАНИЕ |
|:--- |:--- |:--- |
| condition | Нет  | Логическое значение, указывающее, развернут ли ресурс. |
| версия_API |Yes |Версия REST API, которая будет использована для создания ресурса. |
| Тип |Yes |Тип ресурса. Это значение представляет собой сочетание пространства имен поставщика ресурсов и типа ресурса (например, **Microsoft.Storage/storageAccounts**). |
| name |Yes |Имя ресурса. Имя должно соответствовать ограничениям компонентов URI, определенным в RFC3986. Кроме того, службы Azure, которые предоставляют имя ресурса внешним пользователям, проверяют это имя, чтобы убедиться, что это не попытка подделки другого удостоверения. |
| location |Varies |Поддерживаемые географические расположения указанного ресурса. Вы можете выбрать любое из доступных расположений. Но обычно имеет смысл выбрать расположение, которое находится недалеко от пользователей. Кроме того, целесообразно разместить взаимодействующие ресурсы в одном регионе. Большинству типов ресурсов нужно расположение, но некоторым типам (например, назначению роли) оно не требуется. |
| tags |Нет  |Теги, связанные с ресурсом. Примените теги для логической организации ресурсов через подписку. |
| комментарии |Нет  |Заметки по ресурсам в шаблоне |
| копирование |Нет  |Количество создаваемых ресурсов (если нужно несколько экземпляров). Параллельный режим используется по умолчанию. Используйте последовательный режим, если вы не хотите развертывать все ресурсы одновременно. Дополнительные сведения см. в статье [Создание нескольких экземпляров ресурсов в Azure Resource Manager](resource-group-create-multiple.md). |
| Свойство dependsOn |Нет  |Ресурсы, которые должны быть развернуты перед развертыванием этого ресурса. Resource Manager оценивает зависимости между ресурсами и развертывает эти ресурсы в правильном порядке. Если ресурсы не зависят друг от друга, они развертываются параллельно. Значение может представлять собой разделенный запятыми список имен ресурсов или уникальных идентификаторов ресурсов. Выводится только список ресурсов, развертываемых в этом шаблоне. Ресурсы, которые не определены в этом шаблоне, уже должны существовать. Избегайте добавления ненужных зависимостей, так как это может замедлить развертывание и привести к созданию циклических зависимостей. Рекомендации по настройке зависимостей см. в статье [Определение зависимостей в шаблонах диспетчера ресурсов Azure](resource-group-define-dependencies.md). |
| properties |Нет  |Параметры конфигурации ресурса. Значения свойств совпадают со значениями, указываемыми в тексте запроса для операции REST API (метод PUT) для создания ресурса. Кроме того, можно указать массив copy для создания нескольких экземпляров свойства. |
| ресурсов |Нет  |Дочерние ресурсы, которые зависят от определяемого ресурса. Следует указать только те типы ресурсов, которые разрешены в схеме родительского ресурса. Полное имя типа дочернего ресурса содержит тип родительского ресурса, например **Microsoft.Web/sites/extensions**. Зависимость от родительского ресурса не подразумевается. Ее необходимо определить явным образом. |

## <a name="resource-specific-values"></a>Значения определенных ресурсов

**ApiVersion**, **тип**, и **свойства** различны для каждого типа ресурсов. Чтобы определить значения для этих свойств, см. [ссылка на шаблон](/azure/templates/).

## <a name="resource-names"></a>Имена ресурсов
Обычно в Resource Manager вы работаете с именами ресурсов трех типов:

* имена ресурсов, которые должны быть уникальными;
* Имена ресурсов, которые не должны быть уникальными, но возможность указать имя, которое может помочь выявить ресурса.
* имена ресурсов, которые могут быть универсальными.

### <a name="unique-resource-names"></a>Уникальные имена ресурсов
Необходимо указать уникальное имя для любого типа ресурса, который имеет конечную точку доступа к данным. Ниже приведено несколько распространенных типов ресурсов, для которых требуются уникальные имена:

* служба хранилища Azure<sup>1</sup>; 
* веб-приложения службы приложений Azure;
* SQL Server;
* Хранилище ключей Azure
* кэш Azure Redis
* Пакетная служба Azure
* Azure Traffic Manager
* поиск Azure;
* Azure HDInsight

<sup>1</sup> Имена учетных записей хранения также должны содержать до 24 знаков в нижнем регистре без дефисов.

При задании имени, можно вручную создать уникальное имя или используйте [uniqueString()](resource-group-template-functions-string.md#uniquestring) функции для создания имени. Вам также может потребоваться добавить префикс или суффикс к результату **uniqueString**. Измените уникальное имя, чтобы было проще определить тип ресурса по его имени. Например, можно создать уникальное имя учетной записи хранения с помощью следующей переменной:

```json
"variables": {
    "storageAccountName": "[concat(uniqueString(resourceGroup().id),'storage')]"
}
```

### <a name="resource-names-for-identification"></a>Имена ресурсов для идентификации
Для некоторых типов ресурсов необязательно указывать уникальные имена. Вы можете просто указать имя, которое определяет контекст и тип ресурса.

```json
"parameters": {
    "vmName": { 
        "type": "string",
        "defaultValue": "demoLinuxVM",
        "metadata": {
            "description": "The name of the VM to create."
        }
    }
}
```

### <a name="generic-resource-names"></a>Универсальные имена ресурсов
Для типов ресурсов, к которым часто обращаются через другой ресурс, можно использовать универсальное имя, жестко заданное в шаблоне. Например, можно задать стандартное универсальное имя для правил брандмауэра на SQL Server:

```json
{
    "type": "firewallrules",
    "name": "AllowAllWindowsAzureIps",
    ...
}
```

## <a name="location"></a>Расположение
При развертывании шаблона вам нужно указать расположение для каждого ресурса. Различные типы ресурсов, поддерживаются в разных местах. Чтобы просмотреть список адресов, доступных для вашей подписки для определенного типа ресурсов, используйте Azure PowerShell или Azure CLI. 

В следующем примере список расположений для типа ресурса `Microsoft.Web\sites` отображается с помощью PowerShell:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

В следующем примере список расположений для типа ресурса `Microsoft.Web\sites` отображается с помощью Azure CLI 2.0.

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

После определения поддерживаемые расположения для ресурсов, установите это расположение в шаблоне. Самый простой способ задать это значение — это создать группу ресурсов в расположении, которое поддерживает типы ресурсов, а затем указать для каждого расположения `[resourceGroup().location]`. Можно развернуть шаблон в группы ресурсов в разных расположениях, но при этом не изменять параметры или значения в шаблоне. 

В следующем примере показана учетная запись хранения, которая развертывается в том же расположении, что и группа ресурсов:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
      "storageName": "[concat('storage', uniqueString(resourceGroup().id))]"
    },
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageName')]",
      "location": "[resourceGroup().location]",
      "tags": {
        "Dept": "Finance",
        "Environment": "Production"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```

Если необходимо жестко определить расположение в шаблоне, укажите имя одного из поддерживаемых регионов. В следующем примере показано учетная запись хранения, которая всегда развертывается в Северо-центральном регионе США:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storageloc', uniqueString(resourceGroup().id))]",
      "location": "North Central US",
      "tags": {
        "Dept": "Finance",
        "Environment": "Production"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```

## <a name="tags"></a>Теги
[!INCLUDE [resource-manager-tag-introduction](../../includes/resource-manager-tag-introduction.md)]

### <a name="add-tags-to-your-template"></a>Добавление тегов в шаблон

[!INCLUDE [resource-manager-tags-in-templates](../../includes/resource-manager-tags-in-templates.md)]

## <a name="child-resources"></a>Дочерние ресурсы

В некоторых типов ресурсов можно также определить массив дочерние ресурсы. Дочерние ресурсы — это ресурсы, которые существуют только в контексте другого ресурса. Например база данных SQL не может существовать без SQL server, базы данных является дочерним для сервера. Можно определить в определении для сервера базы данных.

```json
{
  "name": "exampleserver",
  "type": "Microsoft.Sql/servers",
  "apiVersion": "2014-04-01",
  ...
  "resources": [
    {
      "name": "exampledatabase",
      "type": "databases",
      "apiVersion": "2014-04-01",
      ...
    }
  ]
}
```

При вложенными, присваивается тип `databases` , но его тип ресурсов — `Microsoft.Sql/servers/databases`. `Microsoft.Sql/servers/` не указывается, так как предполагается из типа родительского ресурса. Дочернему ресурсу присваивается имя `exampledatabase`, но его полное имя включает в себя имя родительского ресурса. `exampleserver` не указывается, так как предполагается из родительского ресурса.

Формат типа дочернего ресурса: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`

Формат имени дочернего ресурса: `{parent-resource-name}/{child-resource-name}`

Однако необходимо определить базу данных в пределах сервера. Дочерний ресурс можно определить на верхнем уровне. Этот подход можно использовать, если родительский ресурс не развертывается в том же шаблоне или требуется использовать `copy` для создания нескольких дочерних ресурсов. В этом случае нужно указать полный тип ресурса и добавить в имя дочернего ресурса имя родительского ресурса.

```json
{
  "name": "exampleserver",
  "type": "Microsoft.Sql/servers",
  "apiVersion": "2014-04-01",
  "resources": [ 
  ],
  ...
},
{
  "name": "exampleserver/exampledatabase",
  "type": "Microsoft.Sql/servers/databases",
  "apiVersion": "2014-04-01",
  ...
}
```

При создании полной ссылки на ресурс порядок объединения сегментов из типа и имени представляет собой не только использование этих двух вариантов.  Вместо этого после пространства имен используйте пары *типа и имени*, начиная от наименее подходящей к наиболее подходящей.

```json
{resource-provider-namespace}/{parent-resource-type}/{parent-resource-name}[/{child-resource-type}/{child-resource-name}]*
```

Например: 

`Microsoft.Compute/virtualMachines/myVM/extensions/myExt` — правильно, `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` — неправильно.

## <a name="recommendations"></a>Рекомендации
Ниже приведены некоторые рекомендации по работе с ресурсами.

* Чтобы другим участникам было проще понять назначение этого ресурса, укажите **комментарии** для каждого ресурса в шаблоне:
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "comments": "This storage account is used to store the VM disks.",
         ...
     }
   ]
   ```

* Если вы используете в шаблоне *общедоступную конечную точку* (например, общедоступную конечную точку хранилища BLOB-объектов Azure), то *не следует жестко задавать* пространство имен. Используйте функцию **reference** для динамического извлечения пространства имен. Вы можете использовать этот подход, чтобы развернуть шаблон в другом общедоступном пространстве имен, не изменяя конечную точку в шаблоне вручную. Задайте для версии API ту же версию, которая указана в учетной записи хранения в вашем шаблоне.
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   Если учетная запись хранения развертывается в том же создаваемом шаблоне, то при указании ссылки на ресурс нет необходимости указывать пространство имен поставщика. В следующем примере показано упрощенный синтаксис:
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(variables('storageAccountName'), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   Если в шаблоне имеются другие значения, настроенные для использования общедоступного пространства имен, измените их, указав одну и ту же функцию **reference**. Например, можно задать свойство **storageUri** диагностического профиля виртуальной машины:
   
   ```json
   "diagnosticsProfile": {
       "bootDiagnostics": {
           "enabled": "true",
           "storageUri": "[reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob]"
       }
   }
   ```
   
   Вы также можете использовать функцию reference для ссылки на учетную запись хранения в другой группе ресурсов:

   ```json
   "osDisk": {
       "name": "osdisk", 
       "vhd": {
           "uri":"[concat(reference(resourceId(parameters('existingResourceGroup'), 'Microsoft.Storage/storageAccounts/', parameters('existingStorageAccountName')), '2016-01-01').primaryEndpoints.blob,  variables('vmStorageAccountContainerName'), '/', variables('OSDiskName'),'.vhd')]"
       }
   }
   ```

* Назначайте общедоступные IP-адреса виртуальной машине только в том случае, если это требуется для работы приложения. Чтобы подключиться к виртуальной машине с целью отладки, управления или администрирования, используйте правила преобразования сетевых адресов для входящих подключений, шлюз виртуальной машины или jumpbox.
   
     Дополнительные сведения о подключении к виртуальным машинам можно получить в приведенных ниже статьях.
   
   * [Run Windows VMs for an N-tier application](../guidance/guidance-compute-n-tier-vm.md) (Запуск виртуальных машин Windows в n-уровневом приложении)
   * [Настройка доступа WinRM для виртуальных машин в Azure Resource Manager](../virtual-machines/windows/winrm.md)
   * [Открытие портов для виртуальной машины в Azure с помощью портала Azure](../virtual-machines/windows/nsg-quickstart-portal.md)
   * [Открытие портов и конечных точек для виртуальной машины в Azure с помощью PowerShell](../virtual-machines/windows/nsg-quickstart-powershell.md)
   * [Открытие портов и конечных точек для виртуальной машины Linux с помощью интерфейса командной строки Azure](../virtual-machines/virtual-machines-linux-nsg-quickstart.md)
* Свойство **DomainNameLabel** для общедоступных IP-адресов должно быть уникальным. Свойство **domainNameLabel** должно содержать то 3 до 63 знаков и соответствовать правилам, определенным этим регулярным выражением: `^[a-z][a-z0-9-]{1,61}[a-z0-9]$`. Так как функция **uniqueString** создает строку длиной 13 знаков, в параметре **dnsPrefixString** можно использовать не более 50 знаков:

   ```json
   "parameters": {
       "dnsPrefixString": {
           "type": "string",
           "maxLength": 50,
           "metadata": {
               "description": "The DNS label for the public IP address. It must be lowercase. It should match the following regular expression, or it will raise an error: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$"
           }
       }
   },
   "variables": {
       "dnsPrefix": "[concat(parameters('dnsPrefixString'),uniquestring(resourceGroup().id))]"
   }
   ```

* При добавлении пароля в расширение пользовательских скриптов используйте свойство **commandToExecute** в **protectedSettings**:
   
   ```json
   "properties": {
       "publisher": "Microsoft.Azure.Extensions",
       "type": "CustomScript",
       "typeHandlerVersion": "2.0",
       "autoUpgradeMinorVersion": true,
       "settings": {
           "fileUris": [
               "[concat(variables('template').assets, '/lamp-app/install_lamp.sh')]"
           ]
       },
       "protectedSettings": {
           "commandToExecute": "[concat('sh install_lamp.sh ', parameters('mySqlPassword'))]"
       }
   }
   ```
   
   > [!NOTE]
   > Чтобы обеспечить шифрование секретов, которые передаются как параметры в виртуальные машины и расширения, необходимо использовать свойство **protectedSettings** соответствующих расширений.
   > 
   > 


## <a name="next-steps"></a>Дальнейшие действия
* Полные шаблоны для различных типов решений доступны на странице [Шаблоны быстрого запуска Azure](https://azure.microsoft.com/documentation/templates/).
* Дополнительные сведения о функциях, которые можно использовать в шаблонах, см. в статье [Функции шаблонов Azure Resource Manager](resource-group-template-functions.md).
* Инструкции по объединению нескольких шаблонов при развертывании см. в статье [Использование связанных шаблонов в Azure Resource Manager](resource-group-linked-templates.md).
* Может потребоваться использовать ресурсы, которые существуют в другой группе ресурсов. Это распространенная ситуация при работе с учетными записями хранения или виртуальными сетями, которые совместно используются в нескольких группах ресурсов. Дополнительные сведения см. в описании [функции resourceId](resource-group-template-functions-resource.md#resourceid).
* Сведения об ограничениях имен ресурсов см. в статье [Рекомендуемые соглашения об именовании для ресурсов Azure](../guidance/guidance-naming-conventions.md).