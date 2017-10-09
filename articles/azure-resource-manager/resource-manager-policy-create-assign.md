---
title: "aaaAssign и управления политиками ресурсов Azure | Документы Microsoft"
description: "Описывает способ tooapply группы ресурсов Azure политики toosubscriptions и ресурсов и как политики tooview ресурсов."
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
ms.date: 07/26/2017
ms.author: tomfitz
ms.openlocfilehash: b6999b43bbcc80d2fde9911352fd4352fa453443
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="assign-and-manage-resource-policies"></a>Назначение политик ресурсов и управление ими

tooimplement политики, необходимо выполнить следующие действия:

1. Проверьте политики toosee определения (включая встроенных политик, предоставленное Azure), если он уже существует в подписке, отвечающего вашим требованиям.
2. Если такая политика существует, получите ее имя.
3. Если он не существует, определите правила политики hello с JSON и добавить его в качестве определения политики в вашей подписке. Этот шаг делает доступными для назначения политики hello, но не применяется hello правила tooyour подписки.
4. Для обоих случаях назначьте область tooa hello политики (например, подписка или группа ресурсов). правила Hello hello политики теперь будут применены.

В этой статье основное внимание уделяется toocreate действия hello определения политики и назначьте этой области определения tooa через API-Интерфейс REST, PowerShell или Azure CLI. При желании toouse hello портала tooassign политики в разделе [tooassign портала используйте Azure и управление политиками ресурсов](resource-manager-policy-portal.md). В этой статье не рассматривается hello синтаксис для создания определения политики hello. Сведения о синтаксисе политики см. в разделе [Общие сведения о политике ресурсов](resource-manager-policy.md).

## <a name="rest-api"></a>Интерфейс REST API

### <a name="create-policy-definition"></a>Создание определения политики

Можно создать политику с hello [API REST для определения политик](/rest/api/resources/policydefinitions). Hello REST API позволяет toocreate и удалять определения политики, а также получение сведений о существующих определений.

Запустите toocreate Определение политики:

```HTTP
PUT https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.authorization/policydefinitions/{policyDefinitionName}?api-version={api-version}
```

Включить запрос текст аналогичные toohello, следующий пример:

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

### <a name="assign-policy"></a>Назначение политики

Можно применить определения политики hello в области hello требуемого по hello [API REST для назначения политик](/rest/api/resources/policyassignments). Hello REST API позволяет toocreate и удалять назначения политики, а также получение сведений о существующих назначений.

Запустите toocreate назначение политики:

```HTTP
PUT https://management.azure.com /subscriptions/{subscription-id}/providers/Microsoft.authorization/policyassignments/{policyAssignmentName}?api-version={api-version}
```

Hello {назначение политики} — hello имя назначения политики hello.

Включить запрос текст аналогичные toohello, следующий пример:

```json
{
  "properties":{
    "displayName":"West US only policy assignment on hello subscription ",
    "description":"Resources can only be provisioned in West US regions",
    "parameters": {
      "allowedLocations": { "value": ["northeurope", "westus"] }
     },
    "policyDefinitionId":"/subscriptions/{subscription-id}/providers/Microsoft.Authorization/policyDefinitions/{definition-name}",
      "scope":"/subscriptions/{subscription-id}"
  },
}
```

### <a name="view-policy"></a>Просмотр политики
использовать политику, tooget hello [получить определения политики](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get) операции.

### <a name="get-aliases"></a>Получение псевдонимов
Вы можете получить псевдонимы через hello REST API:

```HTTP
GET /subscriptions/{id}/providers?$expand=resourceTypes/aliases&api-version=2015-11-01
```

Привет, в следующем примере показано определение псевдонима. Как видите, псевдоним определяет пути в различных версиях API, даже если имя свойства изменено. 

```json
"aliases": [
    {
      "name": "Microsoft.Storage/storageAccounts/sku.name",
      "paths": [
        {
          "path": "properties.accountType",
          "apiVersions": [
            "2015-06-15",
            "2015-05-01-preview"
          ]
        },
        {
          "path": "sku.name",
          "apiVersions": [
            "2016-01-01"
          ]
        }
      ]
    }
]
```

## <a name="powershell"></a>PowerShell

Прежде чем продолжить с примерами PowerShell hello, убедитесь, что у вас есть [установлена последняя версия hello](/powershell/azure/install-azurerm-ps) из Azure PowerShell. Параметры политики были добавлены в версии 3.6.0. При наличии более ранней версии, примеры hello возврата не удается найти параметр, указывающий, hello ошибки.

### <a name="view-policy-definitions"></a>Просмотр определений политик
toosee все определения политики в вашей подписке hello используйте следующие команды:

```powershell
Get-AzureRmPolicyDefinition
```

Она возвращает все доступные определения политик, включая встроенные политики. Каждая политика возвращается в hello следующий формат:

```powershell
Name               : e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceId         : /providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceName       : e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceType       : Microsoft.Authorization/policyDefinitions
Properties         : @{displayName=Allowed locations; policyType=BuiltIn; description=This policy enables you to
                     restrict hello locations your organization can specify when deploying resources. Use tooenforce
                     your geo-compliance requirements.; parameters=; policyRule=}
PolicyDefinitionId : /providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c
```

Перед продолжением toocreate определения политики просмотрите hello встроенных политик. Если встроенные политику, которая применяет ограничения hello, что нужно найти, можно пропустить Создание определения политики. Вместо этого назначьте область toohello требуемого hello встроенные политики.

### <a name="create-policy-definition"></a>Создание определения политики
Можно создать с помощью hello определения политики `New-AzureRmPolicyDefinition` командлета.

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy toospecify access tier." -Policy '{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "field": "kind",
        "equals": "BlobStorage"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/accessTier",
          "equals": "cool"
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}'
```            

Hello выходные данные, хранящиеся в `$definition` объект, который используется при назначении политики. 

Вместо того чтобы задавать hello JSON в качестве параметра, чтобы обеспечить hello путь tooa .json файл, содержащий правила политики hello.

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy toospecify access tier." -Policy "c:\policies\coolAccessTier.json"
```

Hello следующем примере создается определение политики, содержащий параметры.

```powershell
$policy = '{
    "if": {
        "allOf": [
            {
                "field": "type",
                "equals": "Microsoft.Storage/storageAccounts"
            },
            {
                "not": {
                    "field": "location",
                    "in": "[parameters(''allowedLocations'')]"
                }
            }
        ]
    },
    "then": {
        "effect": "Deny"
    }
}'

$parameters = '{
    "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "hello list of locations that can be specified when deploying storage accounts.",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
    }
}' 

$definition = New-AzureRmPolicyDefinition -Name storageLocations -Description "Policy toospecify locations for storage accounts." -Policy $policy -Parameter $parameters 
```

### <a name="assign-policy"></a>Назначение политики

Применение политики hello в hello требуемой области с помощью hello `New-AzureRmPolicyAssignment` командлета. Следующий пример Hello назначает группы ресурсов tooa политики hello.

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
New-AzureRMPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId -PolicyDefinition $definition
```

tooassign политику, которая требует наличия параметров, создания и объекта с этими значениями. Hello следующий пример извлекает встроенные политики и передается в значениях параметров:

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
$definition = Get-AzureRmPolicyDefinition -Id /providers/Microsoft.Authorization/policyDefinitions/e5662a6-4747-49cd-b67b-bf8b01975c4c
$array = @("West US", "West US 2")
$param = @{"listOfAllowedLocations"=$array}
New-AzureRMPolicyAssignment -Name locationAssignment -Scope $rg.ResourceId -PolicyDefinition $definition -PolicyParameterObject $param
```

### <a name="view-policy-assignment"></a>Просмотр назначения политики

Используйте tooget назначение определенные политики.

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
(Get-AzureRmPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId
```

правило политики hello tooview для определения политики, используйте:

```powershell
(Get-AzureRmPolicyDefinition -Name coolAccessTier).Properties.policyRule | ConvertTo-Json
```

### <a name="remove-policy-assignment"></a>Удаление назначения политики 

Используйте tooremove назначение политики:

```powershell
Remove-AzureRmPolicyAssignment -Name regionPolicyAssignment -Scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="azure-cli"></a>Инфраструктура CLI Azure

### <a name="view-policy-definitions"></a>Просмотр определений политик
toosee все определения политики в вашей подписке hello используйте следующие команды:

```azurecli
az policy definition list
```

Она возвращает все доступные определения политик, включая встроенные политики. Каждая политика возвращается в hello следующий формат:

```azurecli
{                                                            
  "description": "This policy enables you toorestrict hello locations your organization can specify when deploying resources. Use tooenforce your geo-compliance requirements.",                      
  "displayName": "Allowed locations",
  "id": "/providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c",
  "name": "e56962a6-4747-49cd-b67b-bf8b01975c4c",
  "policyRule": {
    "if": {
      "not": {
        "field": "location",
        "in": "[parameters('listOfAllowedLocations')]"
      }
    },
    "then": {
      "effect": "Deny"
    }
  },
  "policyType": "BuiltIn"
}
```

Перед продолжением toocreate определения политики просмотрите hello встроенных политик. Если встроенные политику, которая применяет ограничения hello, что нужно найти, можно пропустить Создание определения политики. Вместо этого назначьте область toohello требуемого hello встроенные политики.

### <a name="create-policy-definition"></a>Создание определения политики

Можно создать с помощью Azure CLI с помощью команды определения политики hello определения политики.

```azurecli
az policy definition create --name coolAccessTier --description "Policy toospecify access tier." --rules '{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "field": "kind",
        "equals": "BlobStorage"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/accessTier",
          "equals": "cool"
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}'    
```

### <a name="assign-policy"></a>Назначение политики

Можно задать область toohello требуемого hello политики с помощью команды назначения политики hello. Следующий пример Hello Назначение группы ресурсов tooa политики.

```azurecli
az policy assignment create --name coolAccessTierAssignment --policy coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

### <a name="view-policy-assignment"></a>Просмотр назначения политики

tooview назначение политики предоставить имя назначения политики hello и область hello.

```azurecli
az policy assignment show --name coolAccessTierAssignment --scope "/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}"
```

### <a name="remove-policy-assignment"></a>Удаление назначения политики 

Используйте tooremove назначение политики:

```azurecli
az policy assignment delete --name coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="next-steps"></a>Дальнейшие действия
* Для получения рекомендаций по как предприятия могут использовать диспетчер ресурсов tooeffectively управление подписками см. в разделе [корпоративные функции формирования шаблонов - управление конкретные подписки](resource-manager-subscription-governance.md).

