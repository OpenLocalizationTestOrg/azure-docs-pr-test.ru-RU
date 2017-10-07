---
title: "политики aaaAzure ресурсов для тегов | Документы Microsoft"
description: "Статья содержит примеры политик ресурсов для управления тегами ресурсов."
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
ms.date: 08/24/2017
ms.author: tomfitz
ms.openlocfilehash: 5a5b3d5ed52b47544b397694b9da0070f61b1faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-for-tags"></a>Применение политик ресурсов для тегов

В этом разделе предоставляет политики общих правил, которые можно применять tooensure согласованное использование тегов для ресурсов.

Применение группы ресурсов tooa политики тег или подписки с существующими ресурсами не применяются задним числом hello политики toothose ресурсов. политика hello tooenforce на эти ресурсы включать обновления toohello существующие ресурсы. Эта статья содержит пример PowerShell для активации обновления.

## <a name="ensure-all-resources-in-a-resource-group-have-a-tagvalue"></a>Обеспечение всех ресурсов в группе ресурсов значением или тегом

Общим требованием является наличие определенного тега и значения у всех ресурсов в группе ресурсов. Это требование не часто необходимые tootrack затраты по отделам. должны быть выполнены следующие условия Hello.

* Hello требуется тег значение присоединенных toonew и являются обновленные ресурсы, у которых нет тегов hello.
* Hello необходимые тега и значение нельзя удалить из любые существующие ресурсы.

Это требование можно сделать путем применения две группы ресурсов tooa встроенных политик.

| ИД | Описание |
| ---- | ---- |
| 2a0e14a6-b0a6-4fab-991a-187a4f81c498 | Применяет обязательный тег и его значение по умолчанию, если она не указана пользователем hello. |
| 1e30110a-5ceb-460c-a204-c1c3969c6d62 | Принудительно применяет обязательный тег и его значение. |

### <a name="powershell"></a>PowerShell

Следующий сценарий PowerShell Hello назначает hello две встроенные определения tooa ресурсов группы политики. Перед выполнением сценария hello, назначьте группе ресурсов toohello все требуемые теги. Каждый тег в группе ресурсов hello является обязательным для hello ресурсов в группе hello. группы ресурсов tooall tooassign в вашей подписке не предоставляют hello `-Name` параметр при получении групп ресурсов hello.

```powershell
$appendpolicy = Get-AzureRmPolicyDefinition | Where-Object {$_.Name -eq '2a0e14a6-b0a6-4fab-991a-187a4f81c498'}
$denypolicy = Get-AzureRmPolicyDefinition | Where-Object {$_.Name -eq '1e30110a-5ceb-460c-a204-c1c3969c6d62'}

$rgs = Get-AzureRMResourceGroup -Name ExampleGroup

foreach($rg in $rgs)
{
    $tags = $rg.Tags
    foreach($key in $tags.Keys){
        $key 
        $tags[$key]
        New-AzureRmPolicyAssignment -Name ("append"+$key+"tag") -PolicyDefinition $appendpolicy -Scope $rg.ResourceId -tagName $key -tagValue  $tags[$key]
        New-AzureRmPolicyAssignment -Name ("denywithout"+$key+"tag") -PolicyDefinition $denypolicy -Scope $rg.ResourceId -tagName $key -tagValue  $tags[$key]
    }
}
```

После назначения политики hello, вы можете активировать tooall обновления существующих политик тег hello tooenforce ресурсов, добавленных вами. Hello следующий сценарий сохраняет все прочие теги, существовавшие в hello ресурсы:

```powershell
$group = Get-AzureRmResourceGroup -Name "ExampleGroup" 

$resources = Find-AzureRmResource -ResourceGroupName $group.ResourceGroupName 

foreach($r in $resources)
{
    try{
        $r | Set-AzureRmResource -Tags ($a=if($r.Tags -eq $NULL) { @{}} else {$r.Tags}) -Force -UsePatchSemantics
    }
    catch{
        Write-Host  $r.ResourceId + "can't be updated"
    }
}
```

## <a name="require-tags-for-a-resource-type"></a>Требование тегов для типа ресурса
Hello в следующем примере показано, как тег toorequire логические операторы toonest приложения для только указанный тип ресурса (в этом случае учетных записей хранилища).

```json
{
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
    "then": {
        "effect": "audit"
    }
}
```

## <a name="require-tag"></a>Требование тега
Hello следующая политика запрещает запросы, у которых нет тега, содержащего ключ «Центр затрат» (могут применяться любое значение):

```json
{
  "if": {
    "not" : {
      "field" : "tags",
      "containsKey" : "costCenter"
    }
  },
  "then" : {
    "effect" : "deny"
  }
}
```

## <a name="next-steps"></a>Дальнейшие действия
* После определения правила политики (как показано в предыдущих примерах hello), требуется определение политики toocreate hello и назначьте его tooa области. Hello область может быть подписки, группы ресурсов или ресурсов. политики tooassign через портал hello см. [tooassign портала используйте Azure и управление политиками ресурсов](resource-manager-policy-portal.md). политики tooassign через API-Интерфейс REST, PowerShell или Azure CLI см. [назначение политики и управлять ими через сценарий](resource-manager-policy-create-assign.md).
* Введение tooresource политики, в разделе [Общие сведения о политике ресурсов](resource-manager-policy.md).
* Для получения рекомендаций по как предприятия могут использовать диспетчер ресурсов tooeffectively управление подписками см. в разделе [корпоративные функции формирования шаблонов - управление конкретные подписки](resource-manager-subscription-governance.md).

