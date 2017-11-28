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
# <a name="apply-resource-policies-toostorage-accounts"></a><span data-ttu-id="7ad00-103">Применение учетных записей ресурсов политики toostorage</span><span class="sxs-lookup"><span data-stu-id="7ad00-103">Apply resource policies toostorage accounts</span></span>
<span data-ttu-id="7ad00-104">В этом разделе показано несколько [политики ресурсов](resource-manager-policy.md) можно применить tooAzure учетные записи хранения.</span><span class="sxs-lookup"><span data-stu-id="7ad00-104">This topic shows several [resource policies](resource-manager-policy.md) you can apply tooAzure storage accounts.</span></span> <span data-ttu-id="7ad00-105">Эти политики обеспечения согласованности для учетных записей хранения hello развернута в вашей организации.</span><span class="sxs-lookup"><span data-stu-id="7ad00-105">These policies ensure consistency for hello storage accounts deployed in your organization.</span></span> 

## <a name="define-permitted-storage-account-types"></a><span data-ttu-id="7ad00-106">Определение разрешенных типов учетных записей хранения</span><span class="sxs-lookup"><span data-stu-id="7ad00-106">Define permitted storage account types</span></span>

<span data-ttu-id="7ad00-107">Hello следующая политика ограничивает которой [типы учетных записей хранения](../storage/common/storage-redundancy.md) можно развернуть:</span><span class="sxs-lookup"><span data-stu-id="7ad00-107">hello following policy restricts which [storage account types](../storage/common/storage-redundancy.md) can be deployed:</span></span>

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

<span data-ttu-id="7ad00-108">Аналогичные правила политики с параметром для приема hello допускается SKU доступна как определение встроенной политики.</span><span class="sxs-lookup"><span data-stu-id="7ad00-108">A similar policy rule with a parameter for accepting hello allowed SKUs is available as a built-in policy definition.</span></span> <span data-ttu-id="7ad00-109">встроенная политика Hello имеет идентификатор ресурса hello `/providers/Microsoft.Authorization/policyDefinitions/7433c107-6db4-4ad1-b57a-a76dce0154a1`.</span><span class="sxs-lookup"><span data-stu-id="7ad00-109">hello built-in policy has hello resource ID of `/providers/Microsoft.Authorization/policyDefinitions/7433c107-6db4-4ad1-b57a-a76dce0154a1`.</span></span> 

## <a name="define-permitted-access-tier"></a><span data-ttu-id="7ad00-110">Определение разрешенного уровня доступа</span><span class="sxs-lookup"><span data-stu-id="7ad00-110">Define permitted access tier</span></span>

<span data-ttu-id="7ad00-111">Hello следующую политику указывает тип hello [уровень доступа к](../storage/blobs/storage-blob-storage-tiers.md) , могут быть указаны для учетных записей хранения:</span><span class="sxs-lookup"><span data-stu-id="7ad00-111">hello following policy specifies hello type of [access tier](../storage/blobs/storage-blob-storage-tiers.md) that can be specified for storage accounts:</span></span>

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

## <a name="ensure-encryption-is-enabled"></a><span data-ttu-id="7ad00-112">Включение шифрования</span><span class="sxs-lookup"><span data-stu-id="7ad00-112">Ensure encryption is enabled</span></span>

<span data-ttu-id="7ad00-113">Hello следующая политика требует всех tooenable учетных записей хранилища [шифрование службы хранилища](../storage/common/storage-service-encryption.md):</span><span class="sxs-lookup"><span data-stu-id="7ad00-113">hello following policy requires all storage accounts tooenable [Storage service encryption](../storage/common/storage-service-encryption.md):</span></span>

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

<span data-ttu-id="7ad00-114">Это правило политики также доступна как определение встроенной политики с Идентификатором ресурса hello `/providers/Microsoft.Authorization/policyDefinitions/7c5a74bf-ae94-4a74-8fcf-644d1e0e6e6f`.</span><span class="sxs-lookup"><span data-stu-id="7ad00-114">This policy rule is also available as a built-in policy definition with hello resource ID of `/providers/Microsoft.Authorization/policyDefinitions/7c5a74bf-ae94-4a74-8fcf-644d1e0e6e6f`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ad00-115">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7ad00-115">Next steps</span></span>
* <span data-ttu-id="7ad00-116">После определения правила политики (как показано в предыдущих примерах hello), требуется определение политики toocreate hello и назначьте его tooa области.</span><span class="sxs-lookup"><span data-stu-id="7ad00-116">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="7ad00-117">Hello область может быть подписки, группы ресурсов или ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7ad00-117">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="7ad00-118">политики tooassign через портал hello см. [tooassign портала используйте Azure и управление политиками ресурсов](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7ad00-118">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="7ad00-119">политики tooassign через API-Интерфейс REST, PowerShell или Azure CLI см. [назначение политики и управлять ими через сценарий](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="7ad00-119">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="7ad00-120">Для получения рекомендаций по как предприятия могут использовать диспетчер ресурсов tooeffectively управление подписками см. в разделе [корпоративные функции формирования шаблонов - управление конкретные подписки](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="7ad00-120">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

