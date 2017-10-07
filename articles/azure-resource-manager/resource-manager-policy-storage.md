---
title: "политики aaaAzure ресурсов для учетных записей хранения | Документы Microsoft"
description: "Описание политик диспетчера ресурсов Azure для управления развертыванием hello учетных записей хранения."
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
ms.date: 07/05/2017
ms.author: tomfitz
ms.openlocfilehash: d37fc4bcf7cdec71b0e14f6231fc138bfb6a7893
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-toostorage-accounts"></a>Применение учетных записей ресурсов политики toostorage
В этом разделе показано несколько [политики ресурсов](resource-manager-policy.md) можно применить tooAzure учетные записи хранения. Эти политики обеспечения согласованности для учетных записей хранения hello развернута в вашей организации. 

## <a name="define-permitted-storage-account-types"></a>Определение разрешенных типов учетных записей хранения

Hello следующая политика ограничивает которой [типы учетных записей хранения](../storage/common/storage-redundancy.md) можно развернуть:

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/sku.name",
          "in": [
            "Standard_LRS",
            "Standard_GRS"
          ]
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

Аналогичные правила политики с параметром для приема hello допускается SKU доступна как определение встроенной политики. встроенная политика Hello имеет идентификатор ресурса hello `/providers/Microsoft.Authorization/policyDefinitions/7433c107-6db4-4ad1-b57a-a76dce0154a1`. 

## <a name="define-permitted-access-tier"></a>Определение разрешенного уровня доступа

Hello следующую политику указывает тип hello [уровень доступа к](../storage/blobs/storage-blob-storage-tiers.md) , могут быть указаны для учетных записей хранения:

```json
{
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
}
```

## <a name="ensure-encryption-is-enabled"></a>Включение шифрования

Hello следующая политика требует всех tooenable учетных записей хранилища [шифрование службы хранилища](../storage/common/storage-service-encryption.md):

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/enableBlobEncryption",
          "equals": "true"
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

Это правило политики также доступна как определение встроенной политики с Идентификатором ресурса hello `/providers/Microsoft.Authorization/policyDefinitions/7c5a74bf-ae94-4a74-8fcf-644d1e0e6e6f`.

## <a name="next-steps"></a>Дальнейшие действия
* После определения правила политики (как показано в предыдущих примерах hello), требуется определение политики toocreate hello и назначьте его tooa области. Hello область может быть подписки, группы ресурсов или ресурсов. политики tooassign через портал hello см. [tooassign портала используйте Azure и управление политиками ресурсов](resource-manager-policy-portal.md). политики tooassign через API-Интерфейс REST, PowerShell или Azure CLI см. [назначение политики и управлять ими через сценарий](resource-manager-policy-create-assign.md). 
* Для получения рекомендаций по как предприятия могут использовать диспетчер ресурсов tooeffectively управление подписками см. в разделе [корпоративные функции формирования шаблонов - управление конкретные подписки](resource-manager-subscription-governance.md).

