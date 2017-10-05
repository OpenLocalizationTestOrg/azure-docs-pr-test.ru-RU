---
title: "Политики ресурсов Azure | Документация Майкрософт"
description: "Использование политик Azure Resource Manager, обеспечивающих согласованную настройку свойств ресурсов при развертывании. Политики можно применять на уровне подписки или группы ресурсов."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: abde0f73-c0fe-4e6d-a1ee-32a6fce52a2d
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2017
ms.author: tomfitz
ms.openlocfilehash: 0ee2624f45a1de0c23cae4538a38ae3e302eedd3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="resource-policy-overview"></a>Общие сведения о политике ресурсов
Политики ресурсов позволяют настроить определенные соглашения для ресурсов в организации. Это соглашения помогут вам контролировать расходы и управлять ресурсами. Например, можно указать, что разрешены только определенные типы виртуальных машин. Кроме того, можно требовать наличие определенного тега для каждого ресурса. Политики наследуются всеми дочерними ресурсами. Это значит, что политики, применяемые к группе ресурсов, применяются также ко всем ресурсам в этой группе.

При работе с политиками нужно знать две важные концепции:

* определение политики описывает, когда и как политика будет применяться;
* назначение политики привязывает эту политику к определенной области (к подписке или группе ресурсов).

В этой статье рассматривается только определение политики. Сведения о назначении политик см. в статьях [Назначение политик ресурсов и управление ими с помощью портала Azure](resource-manager-policy-portal.md) и [Назначение политик ресурсов и управление ими](resource-manager-policy-create-assign.md).

Политики оцениваются при создании и обновлении ресурсов (операции PUT и PATCH).

> [!NOTE]
> Сейчас политика не вычисляет типы ресурсов, которые не поддерживают теги, вид и расположение, например тип ресурса Microsoft.Resources/deployments. Их поддержка будет добавлена в будущем. Чтобы избежать проблем с обратной совместимостью, необходимо явно указывать тип при создании политик. Например, политика тегов, которая не указывает типы, применяется для всех типов. В этом случае может произойти ошибка развертывания шаблона, если существует вложенный ресурс, который не поддерживает тег, и в вычисление политики был добавлен тип ресурса развертывания. 
> 
> 

## <a name="how-is-it-different-from-rbac"></a>Чем это отличается от управления доступом на основе ролей?
Существует ряд ключевых различий между политиками и управлением доступом на основе ролей (RBAC). RBAC определяет действия **пользователя** в различных областях. Например, если вам назначена роль участника для группы ресурсов в требуемой области, вы можете вносить изменения в эту группу ресурсов. Политика определяет свойства **ресурсов** во время их развертывания. Например, с помощью политик можно управлять типами ресурсов, которые можно подготовить, или ограничить расположения, в которых можно подготовить ресурсы. В отличие от RBAC, политика представляет собой систему разрешения по умолчанию и явного запрета. 

Чтобы использовать политики, нужно пройти аутентификацию с помощью RBAC. В частности, для учетной записи должны быть предоставлены:

* `Microsoft.Authorization/policydefinitions/write` разрешение на создание политики;
* `Microsoft.Authorization/policyassignments/write` разрешение на назначение политики. 

Эти разрешения не включаются в роль **Участник**.

## <a name="built-in-policies"></a>Встроенные политики

В Azure доступно несколько встроенных определений политик, которые сокращают число соответствующих политик. Прежде чем приступить к работе с определениями политик, следует проверить, не обеспечивает ли какая-либо встроенная политика нужные вам ограничения. Определения встроенных политик приведены ниже:

* Allowed locations;
* Допустимые типы ресурсов
* Allowed storage account SKUs;
* Allowed virtual machine SKUs;
* Apply tag and default value;
* Enforce tag and value;
* Not allowed resource types;
* Require SQL Server version 12.0;
* Require storage account encryption.

Любую из этих политик можно назначить с помощью [портала](resource-manager-policy-portal.md), [PowerShell](resource-manager-policy-create-assign.md#powershell) или [Azure CLI](resource-manager-policy-create-assign.md#azure-cli).

## <a name="policy-definition-structure"></a>Структура определения политики
Для создания определения политики используется JSON. Определение политики содержит следующие элементы:

* parameters
* display name
* description
* policy rule
  * logical evaluation
  * effect

В следующем примере показана политика, которая налагает ограничения на набор расположений для развертывания ресурсов.

```json
{
  "properties": {
    "parameters": {
      "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "The list of locations that can be specified when deploying resources",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
      }
    },
    "displayName": "Allowed locations",
    "description": "This policy enables you to restrict the locations your organization can specify when deploying resources.",
    "policyRule": {
      "if": {
        "not": {
          "field": "location",
          "in": "[parameters('allowedLocations')]"
        }
      },
      "then": {
        "effect": "deny"
      }
    }
  }
}
```

## <a name="parameters"></a>Параметры
Использование параметров помогает упростить управление политиками за счет сокращения числа определений политики. Вы можете определить политику для свойства ресурса (например, чтобы ограничить набор расположений для развертывания этих ресурсов), включив в определение параметры. Затем это определение политики можно неоднократно использовать в разных сценариях, передавая в него разные значения (например, набор расположений для определенной подписки) при назначении политики.

А параметры объявляются при создании определения политики.

```json
"parameters": {
  "allowedLocations": {
    "type": "array",
    "metadata": {
      "description": "The list of allowed locations for resources.",
      "displayName": "Allowed locations"
    }
  }
}
```

Типом параметра может быть строка или массив. Свойство метаданных используется в таких инструментах, как портал Azure, для отображения удобных для пользователя сведений. 

В правилах политики полученные параметры используются так: 

```json
{ 
    "field": "location",
    "in": "[parameters('allowedLocations')]"
}
```

## <a name="display-name-and-description"></a>Отображаемое имя и описание

Параметры **displayName** и **description** позволяют идентифицировать определение политики и описать контекст для ее использования.

## <a name="policy-rule"></a>Правило политики

Правило политики состоит из блоков **If** и **Then**. В блоке **If** указываются одно или несколько условий. Они определяют, когда применяется эта политика. В этих условиях можно использовать логические операторы, чтобы точно определить сценарии для использования политики. В блоке **Then** описываются результаты, которые вступают в силу при соблюдении условий из блока **If**.

```json
{
  "if": {
    <condition> | <logical operator>
  },
  "then": {
    "effect": "deny | audit | append"
  }
}
```

### <a name="logical-operators"></a>Логические операторы
Ниже перечислены поддерживаемые логические операторы.

* `"not": {condition  or operator}`
* `"allOf": [{condition or operator},{condition or operator}]`
* `"anyOf": [{condition or operator},{condition or operator}]`

Оператор **not** инвертирует результат условия. Оператор **allOf** действует как логическая операция **And**, то есть требует соблюдения всех входящих в него условий. Оператор **anyOf** действует как логическая операция **Or**, то есть проверяет соблюдение хотя бы одного из входящих в него условий.

Допускается вложение логических операторов. В следующем примере представлена операция **not**, вложенная в операцию **allOf**. 

```json
"if": {
  "allOf": [
    {
      "not": {
        "field": "tags",
        "containsKey": "application"
      }
    },
    {
      "field": "type",
      "equals": "Microsoft.Storage/storageAccounts"
    }
  ]
},
```

### <a name="conditions"></a>Условия
Условие определяет, соответствует ли свойство **field** определенным параметрам. Поддерживаются такие условия:

* `"equals": "value"`
* `"like": "value"`
* `"match": "value"`
* `"contains": "value"`
* `"in": ["value1","value2"]`
* `"containsKey": "keyName"`
* `"exists": "bool"`

В значении для условия **like** можно использовать подстановочный знак (*).

При использовании условия **match** для цифры используйте `#`, для буквы — `?` и любые другие соответствующие символы. Примеры приведены в разделе [Применение политик ресурсов для имен и текста](resource-manager-policy-naming-convention.md).

### <a name="fields"></a>Поля
Условия создаются на основе полей. Поле представляет свойства в полезных данных запроса ресурса, используемые для описания состояния ресурса.  

Поддерживаются следующие поля.

* `name`
* `kind`
* `type`
* `location`
* `tags`
* `tags.*` 
* Список псевдонимов свойств указан в разделе [Псевдонимы](#aliases).

### <a name="effect"></a>Результат
Политика поддерживает три типа результатов — `deny`, `audit` и `append`. 

* **deny** создает событие в журнале аудита и отклоняет запрос.
* **audit** создает событие в журнале аудита, но выполняет запрос.
* **append** добавляет в запрос некоторый набор полей. 

Для типа **append**необходимо указать следующие сведения:

```json
"effect": "append",
"details": [
  {
    "field": "field name",
    "value": "value of the field"
  }
]
```

Значением может быть строка или объект формата JSON. 

## <a name="aliases"></a>Псевдонимы

Псевдонимы свойств позволяют обращаться к определенным свойствам для типа ресурса. Псевдонимы позволяют ограничить значения или условия, разрешенные для свойства ресурса. Каждый псевдоним сопоставляется с путями в разных версиях API для заданного типа ресурса. Во время оценки политики модуль политики получает путь свойства для этой версии API.

**Microsoft.Cache/Redis**

| Alias | Описание |
| ----- | ----------- |
| Microsoft.Cache/Redis/enableNonSslPort | Указывает, включен ли на сервере Redis порт без поддержки SSL (6379). |
| Microsoft.Cache/Redis/shardCount | Задает число сегментов, создаваемых в кэше кластера уровня "Премиум".  |
| Microsoft.Cache/Redis/sku.capacity | Задает размер развертываемого кэша Redis.  |
| Microsoft.Cache/Redis/sku.family | Задает используемое семейство SKU. |
| Microsoft.Cache/Redis/sku.name | Задает тип развертываемого кэша Redis. |

**Microsoft.Cdn/profiles**

| Alias | Описание |
| ----- | ----------- |
| Microsoft.CDN/profiles/sku.name | Задает имя ценовой категории. |

**Microsoft.Compute/disks**

| Alias | Описание |
| ----- | ----------- |
| Microsoft.Compute/imageOffer | Задает предложение образа платформы или образа Marketplace, используемого для создания виртуальной машины. |
| Microsoft.Compute/imagePublisher | Задает издатель образа платформы или образа Marketplace, используемого для создания виртуальной машины. |
| Microsoft.Compute/imageSku | Задает номер SKU образа платформы или образа Marketplace, используемого для создания виртуальной машины. |
| Microsoft.Compute/imageVersion | Задает версию образа платформы или образа Marketplace, используемого для создания виртуальной машины. |


**Microsoft.Compute/virtualMachines**

| Alias | Описание |
| ----- | ----------- |
| Microsoft.Compute/imageId | Задайте идентификатор образа, используемого для создания виртуальной машины. |
| Microsoft.Compute/imageOffer | Задает предложение образа платформы или образа Marketplace, используемого для создания виртуальной машины. |
| Microsoft.Compute/imagePublisher | Задает издатель образа платформы или образа Marketplace, используемого для создания виртуальной машины. |
| Microsoft.Compute/imageSku | Задает номер SKU образа платформы или образа Marketplace, используемого для создания виртуальной машины. |
| Microsoft.Compute/imageVersion | Задает версию образа платформы или образа Marketplace, используемого для создания виртуальной машины. |
| Microsoft.Compute/licenseType | Указывает, используется ли для образа или диска локальная лицензия. Это значение используется только для образов, содержащих операционную систему Windows Server.  |
| Microsoft.Compute/virtualMachines/imageOffer | Задает предложение образа платформы или образа Marketplace, используемого для создания виртуальной машины. |
| Microsoft.Compute/virtualMachines/imagePublisher | Задает издатель образа платформы или образа Marketplace, используемого для создания виртуальной машины. |
| Microsoft.Compute/virtualMachines/imageSku | Задает номер SKU образа платформы или образа Marketplace, используемого для создания виртуальной машины. |
| Microsoft.Compute/virtualMachines/imageVersion | Задает версию образа платформы или образа Marketplace, используемого для создания виртуальной машины. |
| Microsoft.Compute/virtualMachines/osDisk.Uri | Задает универсальный код ресурса (URI) виртуального жесткого диска. |
| Microsoft.Compute/virtualMachines/sku.name | Задайте размер виртуальной машины. |

**Microsoft.Compute/virtualMachines/extensions**

| Alias | Описание |
| ----- | ----------- |
| Microsoft.Compute/virtualMachines/extensions/publisher | Задает имя издателя расширения. |
| Microsoft.Compute/virtualMachines/extensions/type | Задает тип расширения. |
| Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion | Задает версию расширения. |

**Microsoft.Compute/virtualMachineScaleSets**

| Alias | Описание |
| ----- | ----------- |
| Microsoft.Compute/imageId | Задайте идентификатор образа, используемого для создания виртуальной машины. |
| Microsoft.Compute/imageOffer | Задает предложение образа платформы или образа Marketplace, используемого для создания виртуальной машины. |
| Microsoft.Compute/imagePublisher | Задает издатель образа платформы или образа Marketplace, используемого для создания виртуальной машины. |
| Microsoft.Compute/imageSku | Задает номер SKU образа платформы или образа Marketplace, используемого для создания виртуальной машины. |
| Microsoft.Compute/imageVersion | Задает версию образа платформы или образа Marketplace, используемого для создания виртуальной машины. |
| Microsoft.Compute/licenseType | Указывает, используется ли для образа или диска локальная лицензия. Это значение используется только для образов, содержащих операционную систему Windows Server. |
| Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix | Задает префикс имени компьютера для всех виртуальных машин в масштабируемом наборе. |
| Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl | Задает универсальный код ресурса (URI) большого двоичного объекта для пользовательского образа. |
| Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers | Задает URL-адреса контейнеров, которые используются для хранения ОС для масштабируемого набора. |
| Microsoft.Compute/VirtualMachineScaleSets/sku.name | Задает размер виртуальных машин в масштабируемом наборе. |
| Microsoft.Compute/VirtualMachineScaleSets/sku.tier | Задает уровень виртуальных машин в масштабируемом наборе. |
  
**Microsoft.Network/applicationGateways**

| Alias | Описание |
| ----- | ----------- |
| Microsoft.Network/applicationGateways/sku.name | Задает размер шлюза. |

**Microsoft.Network/virtualNetworkGateways**

| Alias | Описание |
| ----- | ----------- |
| Microsoft.Network/virtualNetworkGateways/gatewayType | Задает тип шлюза виртуальной сети. |
| Microsoft.Network/virtualNetworkGateways/sku.name | Задает номера SKU шлюза. |

**Microsoft.Sql/servers**

| Alias | Описание |
| ----- | ----------- |
| Microsoft.Sql/servers/version | Задает версию сервера. |

**Microsoft.Sql/databases**

| Alias | Описание |
| ----- | ----------- |
| Microsoft.Sql/servers/databases/edition | Задает выпуск базы данных. |
| Microsoft.Sql/servers/databases/elasticPoolName | Задает имя эластичного пула, в котором размещена база данных. |
| Microsoft.Sql/servers/databases/requestedServiceObjectiveId | Задает идентификатор настроенного целевого уровня обслуживания для базы данных. |
| Microsoft.Sql/servers/databases/requestedServiceObjectiveName | Задает имя настроенного целевого уровня обслуживания для базы данных.  |

**Microsoft.Sql/elasticpools**

| Alias | Описание |
| ----- | ----------- |
| servers/elasticpools | Microsoft.Sql/servers/elasticPools/dtu | Задает совокупное число общих единиц DTU для эластичного пула базы данных. |
| servers/elasticpools | Microsoft.Sql/servers/elasticPools/edition | Задает выпуск эластичного пула. |

**Microsoft.Storage/storageAccounts**

| Alias | Описание |
| ----- | ----------- |
| Microsoft.Storage/storageAccounts/accessTier | Задает уровень доступа, используемый для выставления счетов. |
| Microsoft.Storage/storageAccounts/accountType | Задает имя SKU. |
| Microsoft.Storage/storageAccounts/enableBlobEncryption | Указывает, шифрует ли служба данные, хранящиеся в службе хранилища BLOB-объектов. |
| Microsoft.Storage/storageAccounts/enableFileEncryption | Указывает, шифрует ли служба данные, хранящиеся в службе хранилища файлов. |
| Microsoft.Storage/storageAccounts/sku.name | Задает имя SKU. |
| Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly | Позволяет разрешить только передачу трафика HTTPS в службу хранилища. |


## <a name="policy-examples"></a>Примеры политик

Следующие статьи содержат примеры политик.

* Примеры политик для тегов см. в статье [Apply resource policies for tags](resource-manager-policy-tags.md) (Применение политик ресурсов для тегов).
* Примеры именования и шаблоны текста приведены в разделе [Применение политик ресурсов для имен и текста](resource-manager-policy-naming-convention.md).
* Примеры политик для хранения см. в статье [Применение политик ресурсов Azure для учетных записей хранения](resource-manager-policy-storage.md).
* Примеры политик для виртуальных машин есть в статьях о применении политик к виртуальным машинам Azure Resource Manager [для Linux](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) и [для Windows](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json).


## <a name="next-steps"></a>Дальнейшие действия
* Определив правило политики, назначьте эту политику для области. Сведения о назначении политик с помощью портала см. в статье [Назначение политик ресурсов и управление ими с помощью портала Azure](resource-manager-policy-portal.md). Сведения о назначении политик с помощью REST API, PowerShell или Azure CLI см. в статье [Назначение политик ресурсов и управление ими](resource-manager-policy-create-assign.md).
* Руководство по использованию Resource Manager для эффективного управления подписками в организациях см [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md) (Шаблон Azure для организаций. Рекомендуемая система управления подпиской).
* Схема политики опубликована на странице [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json). 

