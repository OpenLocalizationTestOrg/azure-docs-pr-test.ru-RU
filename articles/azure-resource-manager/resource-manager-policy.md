---
title: "политики ресурсов aaaAzure | Документы Microsoft"
description: "Описывает, каким образом toouse диспетчера ресурсов Azure политики tooensure согласованное ресурсов задано во время развертывания. Политики могут применяться для групп hello подписка или ресурс."
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
ms.openlocfilehash: f1b0bbb5f838f6bb70721e1040ad3eac2d881cea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="resource-policy-overview"></a>Общие сведения о политике ресурсов
Политики ресурсов позволяют tooestablish соглашения для ресурсов в вашей организации. Это соглашения помогут вам контролировать расходы и управлять ресурсами. Например, можно указать, что разрешены только определенные типы виртуальных машин. Кроме того, можно требовать наличие определенного тега для каждого ресурса. Политики наследуются всеми дочерними ресурсами. Таким образом Если политика не применяется tooa группы ресурсов, это применимо tooall hello ресурсов в этой группе ресурсов.

Существует два toounderstand основные понятия о политиках.

* Определение политики — описывается при hello включена политика и какие действия tootake
* Назначение политики - применить область tooa политики определения hello (подписка или группа ресурсов)

В этой статье рассматривается только определение политики. Сведения о назначении политики см. в разделе [tooassign портала используйте Azure и управление политиками ресурсов](resource-manager-policy-portal.md) или [назначение политики и управлять ими через сценарий](resource-manager-policy-create-assign.md).

Политики оцениваются при создании и обновлении ресурсов (операции PUT и PATCH).

> [!NOTE]
> В настоящее время политики не вычисляет типы ресурсов, которые не поддерживают теги, тип и расположение, например тип ресурса Microsoft.Resources/deployments hello. Их поддержка будет добавлена в будущем. проблемы совместимости с предыдущими версиями tooavoid, следует явно указать тип при создании политики. Например, политика тегов, которая не указывает типы, применяется для всех типов. В этом случае шаблона-развертывания может завершиться ошибкой, если вложенные ресурс, который не поддерживает теги и тип ресурса развертывания hello добавлен toopolicy оценки. 
> 
> 

## <a name="how-is-it-different-from-rbac"></a>Чем это отличается от управления доступом на основе ролей?
Существует ряд ключевых различий между политиками и управлением доступом на основе ролей (RBAC). RBAC определяет действия **пользователя** в различных областях. Например вы добавляются toohello роль участника для группы ресурсов в области hello требуемого для внесения изменений группы ресурсов toothat. Политика определяет свойства **ресурсов** во время их развертывания. Например через политики, можно управлять hello типы ресурсов, которые могут быть подготовлены. Или вы можете ограничить hello расположения, в которых можно подготовить ресурсы hello. В отличие от RBAC, политика представляет собой систему разрешения по умолчанию и явного запрета. 

политики toouse, вы должны пройти проверку подлинности через RBAC. В частности, для учетной записи должны быть предоставлены:

* `Microsoft.Authorization/policydefinitions/write`разрешение toodefine политики
* `Microsoft.Authorization/policyassignments/write`разрешение tooassign политики 

Эти разрешения не включаются в hello **участника** роли.

## <a name="built-in-policies"></a>Встроенные политики

Azure предоставляет некоторые определения встроенных политик, которые может сократить число hello политик имеют toodefine. Перед продолжением определения политик, следует ли встроенные политики уже предоставляет определение hello, что нужно. используются Hello встроенная политика определения.

* Allowed locations;
* Допустимые типы ресурсов
* Allowed storage account SKUs;
* Allowed virtual machine SKUs;
* Apply tag and default value;
* Enforce tag and value;
* Not allowed resource types;
* Require SQL Server version 12.0;
* Require storage account encryption.

Можно назначить любой из этих политик через hello [портала](resource-manager-policy-portal.md), [PowerShell](resource-manager-policy-create-assign.md#powershell), или [Azure CLI](resource-manager-policy-create-assign.md#azure-cli).

## <a name="policy-definition-structure"></a>Структура определения политики
Использовании JSON toocreate определения политики. Определение политики Hello содержит элементы для:

* parameters
* display name
* description
* policy rule
  * logical evaluation
  * effect

Следующий пример Hello показано политику, которая ограничивает, где развернуты ресурсы.

```json
{
  "properties": {
    "parameters": {
      "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "hello list of locations that can be specified when deploying resources",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
      }
    },
    "displayName": "Allowed locations",
    "description": "This policy enables you toorestrict hello locations your organization can specify when deploying resources.",
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
С помощью параметров помогает упростить управление политики за счет сокращения числа hello определения политик. Определить политику для свойства ресурса (например, ограничение расположения hello, где может развертываться ресурсы) и включения параметров в определении hello. Затем можно повторно использовать определения политик для различных сценариев, передавая различные значения (например, указать один набор расположений для подписки) при назначении политики hello.

А параметры объявляются при создании определения политики.

```json
"parameters": {
  "allowedLocations": {
    "type": "array",
    "metadata": {
      "description": "hello list of allowed locations for resources.",
      "displayName": "Allowed locations"
    }
  }
}
```

Тип Hello параметра может быть строка или массив. Свойство метаданных Hello используется для средств, таких как Azure портала toodisplay понятные сведения. 

В правиле политики hello параметры ссылок с hello, используя синтаксис: 

```json
{ 
    "field": "location",
    "in": "[parameters('allowedLocations')]"
}
```

## <a name="display-name-and-description"></a>Отображаемое имя и описание

Использовать hello **displayName** и **описание** tooidentify hello определения политики и обеспечения при использовании контекста.

## <a name="policy-rule"></a>Правило политики

правило политики Hello состоит из **Если** и **затем** блоков. В hello **Если** блока, можно определить одно или несколько условий, указывающие, когда применяется политика hello. Логические операторы toothese условия можно применить tooprecisely определить hello сценарий для политики. В hello **затем** блок, определяется hello эффект, который происходит, когда hello **Если** условия будут выполнены.

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
Hello поддерживается логическим операторам относятся:

* `"not": {condition  or operator}`
* `"allOf": [{condition or operator},{condition or operator}]`
* `"anyOf": [{condition or operator},{condition or operator}]`

Hello **не** синтаксис Инвертирует результат hello hello условия. Hello **все** синтаксис (аналогично toohello логических **и** операции) требует true toobe все условия. Hello **anyOf** синтаксис (аналогично toohello логических **или** операции) требует одного или нескольких toobe условия значение true.

Допускается вложение логических операторов. Следующий пример показывает Hello **не** операции, вложенные в **все** операции. 

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
условие Hello ли **поле** заданным критериям. Hello поддерживается условиям относятся:

* `"equals": "value"`
* `"like": "value"`
* `"match": "value"`
* `"contains": "value"`
* `"in": ["value1","value2"]`
* `"containsKey": "keyName"`
* `"exists": "bool"`

При использовании hello **как** условие, можно указать подстановочный знак (*) в значение hello.

При использовании hello **соответствует** условия, укажите `#` toorepresent цифры, `?` для письма и любой другой символ toorepresent, фактический символ. Примеры приведены в разделе [Применение политик ресурсов для имен и текста](resource-manager-policy-naming-convention.md).

### <a name="fields"></a>Поля
Условия создаются на основе полей. Поле представляет свойства в полезных данных запроса hello ресурсов, используемых toodescribe hello состояние hello ресурса.  

поддерживаются следующие поля Hello:

* `name`
* `kind`
* `type`
* `location`
* `tags`
* `tags.*` 
* Список псевдонимов свойств указан в разделе [Псевдонимы](#aliases).

### <a name="effect"></a>Результат
Политика поддерживает три типа результатов — `deny`, `audit` и `append`. 

* **Запретить** создает событие в журнал аудита hello и происходит сбой запроса hello
* **Аудит** приводит к возникновению события предупреждения в журнал аудита, но не позволяет hello запроса
* **Добавление** добавляет набор hello определенные поля toohello запроса 

Для **append**, необходимо предоставить hello, приведенные ниже сведения:

```json
"effect": "append",
"details": [
  {
    "field": "field name",
    "value": "value of hello field"
  }
]
```

Hello значение может быть строка или объект формата JSON. 

## <a name="aliases"></a>Псевдонимы

Используйте свойство псевдонимы tooaccess определенных свойств для типа ресурса. Псевдонимы включают toorestrict, какие значения или условия являются допустимыми для свойства ресурса. Каждый псевдоним сопоставляет toopaths в различных версиях API для заданного типа ресурса. Во время оценки политики hello модуль политики возвращает путь к свойству hello для этой версии API.

**Microsoft.Cache/Redis**

| Alias | Описание |
| ----- | ----------- |
| Microsoft.Cache/Redis/enableNonSslPort | Задать ли сервер Redis hello не ssl-порта (6379) включен. |
| Microsoft.Cache/Redis/shardCount | Задайте количество hello toobe сегментов, созданные на кластер кэша Premium.  |
| Microsoft.Cache/Redis/sku.capacity | Задать размер hello toodeploy кэша Redis hello.  |
| Microsoft.Cache/Redis/sku.family | Задать семейства toouse hello SKU. |
| Microsoft.Cache/Redis/sku.name | Выбор типа hello toodeploy кэша Redis. |

**Microsoft.Cdn/profiles**

| Alias | Описание |
| ----- | ----------- |
| Microsoft.CDN/profiles/sku.name | Имя набора hello hello ценовой категории. |

**Microsoft.Compute/disks**

| Alias | Описание |
| ----- | ----------- |
| Microsoft.Compute/imageOffer | Предложение SET hello hello платформы образа или образа marketplace используется toocreate hello виртуальной машины. |
| Microsoft.Compute/imagePublisher | Набор hello издатель образа платформы hello или образа marketplace используется toocreate hello виртуальной машины. |
| Microsoft.Compute/imageSku | Набор hello номер SKU образа платформы hello или образа marketplace используется toocreate hello виртуальной машины. |
| Microsoft.Compute/imageVersion | Версия набора hello hello платформы образа или образа marketplace используется toocreate hello виртуальной машины. |


**Microsoft.Compute/virtualMachines**

| Alias | Описание |
| ----- | ----------- |
| Microsoft.Compute/imageId | Задать идентификатор hello hello изображение, используемое toocreate hello виртуальной машины. |
| Microsoft.Compute/imageOffer | Предложение SET hello hello платформы образа или образа marketplace используется toocreate hello виртуальной машины. |
| Microsoft.Compute/imagePublisher | Набор hello издатель образа платформы hello или образа marketplace используется toocreate hello виртуальной машины. |
| Microsoft.Compute/imageSku | Набор hello номер SKU образа платформы hello или образа marketplace используется toocreate hello виртуальной машины. |
| Microsoft.Compute/imageVersion | Версия набора hello hello платформы образа или образа marketplace используется toocreate hello виртуальной машины. |
| Microsoft.Compute/licenseType | Заданы, hello образа или диска лицензированного в локальной среде. Это значение используется только для образов, содержащих hello ОС Windows Server.  |
| Microsoft.Compute/virtualMachines/imageOffer | Предложение SET hello hello платформы образа или образа marketplace используется toocreate hello виртуальной машины. |
| Microsoft.Compute/virtualMachines/imagePublisher | Набор hello издатель образа платформы hello или образа marketplace используется toocreate hello виртуальной машины. |
| Microsoft.Compute/virtualMachines/imageSku | Набор hello номер SKU образа платформы hello или образа marketplace используется toocreate hello виртуальной машины. |
| Microsoft.Compute/virtualMachines/imageVersion | Версия набора hello hello платформы образа или образа marketplace используется toocreate hello виртуальной машины. |
| Microsoft.Compute/virtualMachines/osDisk.Uri | Задайте hello vhd URI. |
| Microsoft.Compute/virtualMachines/sku.name | Задайте размер hello hello виртуальной машины. |

**Microsoft.Compute/virtualMachines/extensions**

| Alias | Описание |
| ----- | ----------- |
| Microsoft.Compute/virtualMachines/extensions/publisher | Задайте имя издателя расширения hello hello. |
| Microsoft.Compute/virtualMachines/extensions/type | Задайте тип hello расширения. |
| Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion | Задает версию расширения hello hello. |

**Microsoft.Compute/virtualMachineScaleSets**

| Alias | Описание |
| ----- | ----------- |
| Microsoft.Compute/imageId | Задать идентификатор hello hello изображение, используемое toocreate hello виртуальной машины. |
| Microsoft.Compute/imageOffer | Предложение SET hello hello платформы образа или образа marketplace используется toocreate hello виртуальной машины. |
| Microsoft.Compute/imagePublisher | Набор hello издатель образа платформы hello или образа marketplace используется toocreate hello виртуальной машины. |
| Microsoft.Compute/imageSku | Набор hello номер SKU образа платформы hello или образа marketplace используется toocreate hello виртуальной машины. |
| Microsoft.Compute/imageVersion | Версия набора hello hello платформы образа или образа marketplace используется toocreate hello виртуальной машины. |
| Microsoft.Compute/licenseType | Заданы, hello образа или диска лицензированного в локальной среде. Это значение используется только для образов, содержащих hello ОС Windows Server. |
| Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix | Задать hello с префиксом имени компьютера для всех виртуальных машин hello в наборе масштабирования hello. |
| Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl | Набор hello URI большого двоичного объекта для пользовательского образа. |
| Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers | Набор hello контейнера URL-адреса, используемые toostore дисков операционной системы для набора масштабирования hello. |
| Microsoft.Compute/VirtualMachineScaleSets/sku.name | Установите размер hello виртуальных машин в наборе масштабирования. |
| Microsoft.Compute/VirtualMachineScaleSets/sku.tier | Задайте уровень hello виртуальных машин в наборе масштабирования. |
  
**Microsoft.Network/applicationGateways**

| Alias | Описание |
| ----- | ----------- |
| Microsoft.Network/applicationGateways/sku.name | Задайте размер hello hello шлюза. |

**Microsoft.Network/virtualNetworkGateways**

| Alias | Описание |
| ----- | ----------- |
| Microsoft.Network/virtualNetworkGateways/gatewayType | Задайте тип hello этого шлюза виртуальной сети. |
| Microsoft.Network/virtualNetworkGateways/sku.name | Задайте имя SKU шлюза hello. |

**Microsoft.Sql/servers**

| Alias | Описание |
| ----- | ----------- |
| Microsoft.Sql/servers/version | Задает версию сервера hello hello. |

**Microsoft.Sql/databases**

| Alias | Описание |
| ----- | ----------- |
| Microsoft.Sql/servers/databases/edition | Установите выпуск hello hello базы данных. |
| Microsoft.Sql/servers/databases/elasticPoolName | Имя набора hello hello эластичного пула hello, базы данных находится в. |
| Microsoft.Sql/servers/databases/requestedServiceObjectiveId | Задайте настройки hello уровня идентификатор цели службы hello базы данных. |
| Microsoft.Sql/servers/databases/requestedServiceObjectiveName | Имя набора hello hello настроить цель уровня обслуживания базы данных hello.  |

**Microsoft.Sql/elasticpools**

| Alias | Описание |
| ----- | ----------- |
| servers/elasticpools | Microsoft.Sql/servers/elasticPools/dtu | Всего hello набор общих DTU для эластичного пула hello базы данных. |
| servers/elasticpools | Microsoft.Sql/servers/elasticPools/edition | Установите выпуск hello hello эластичного пула. |

**Microsoft.Storage/storageAccounts**

| Alias | Описание |
| ----- | ----------- |
| Microsoft.Storage/storageAccounts/accessTier | Уровень доступа к hello набор используется для выставления счетов. |
| Microsoft.Storage/storageAccounts/accountType | Задайте имя SKU hello. |
| Microsoft.Storage/storageAccounts/enableBlobEncryption | Задается ли служба hello шифрует данные, hello, хранящегося в службе хранилища больших двоичных объектов hello. |
| Microsoft.Storage/storageAccounts/enableFileEncryption | Задается ли служба hello шифрует данные, hello, хранящегося в службе хранилища файла hello. |
| Microsoft.Storage/storageAccounts/sku.name | Задайте имя SKU hello. |
| Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly | Установите службы toostorage трафика tooallow только https. |


## <a name="policy-examples"></a>Примеры политик

Привет, следующие разделы содержат примеры политики:

* Примеры политик для тегов см. в статье [Apply resource policies for tags](resource-manager-policy-tags.md) (Применение политик ресурсов для тегов).
* Примеры именования и шаблоны текста приведены в разделе [Применение политик ресурсов для имен и текста](resource-manager-policy-naming-convention.md).
* Примеры политик хранения см. в разделе [применения учетных записей ресурсов политики toostorage](resource-manager-policy-storage.md).
* Примеры политик виртуальной машины в разделе [применить tooLinux политики ресурсов виртуальных машин](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) и [применить tooWindows политики ресурсов виртуальных машин](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)


## <a name="next-steps"></a>Дальнейшие действия
* После определения правила политики, назначьте его tooa область. политики tooassign через портал hello см. [tooassign портала используйте Azure и управление политиками ресурсов](resource-manager-policy-portal.md). политики tooassign через API-Интерфейс REST, PowerShell или Azure CLI см. [назначение политики и управлять ими через сценарий](resource-manager-policy-create-assign.md).
* Для получения рекомендаций по как предприятия могут использовать диспетчер ресурсов tooeffectively управление подписками см. в разделе [корпоративные функции формирования шаблонов - управление конкретные подписки](resource-manager-subscription-governance.md).
* Схема политики Hello опубликованы по адресу [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json). 

