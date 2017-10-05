---
title: "Политики ресурсов Azure для учетных записей хранения | Документация Майкрософт"
description: "Описывает политики Azure Resource Manager для управления развертыванием учетных записей хранения."
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
ms.openlocfilehash: 6612ee61f5c50e743241b92030660cea7ae7094d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="apply-resource-policies-to-storage-accounts"></a><span data-ttu-id="fd482-103">Применение политик ресурсов к учетным записям хранения</span><span class="sxs-lookup"><span data-stu-id="fd482-103">Apply resource policies to storage accounts</span></span>
<span data-ttu-id="fd482-104">В этом разделе показано несколько [политик ресурсов](resource-manager-policy.md), которые можно применить к учетным записям хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="fd482-104">This topic shows several [resource policies](resource-manager-policy.md) you can apply to Azure storage accounts.</span></span> <span data-ttu-id="fd482-105">Эти политики обеспечивают согласованность данных в учетных записях хранения, развернутых в организации.</span><span class="sxs-lookup"><span data-stu-id="fd482-105">These policies ensure consistency for the storage accounts deployed in your organization.</span></span> 

## <a name="define-permitted-storage-account-types"></a><span data-ttu-id="fd482-106">Определение разрешенных типов учетных записей хранения</span><span class="sxs-lookup"><span data-stu-id="fd482-106">Define permitted storage account types</span></span>

<span data-ttu-id="fd482-107">Приведенная ниже политика ограничивает [типы развертываемых учетных записей хранения](../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="fd482-107">The following policy restricts which [storage account types](../storage/common/storage-redundancy.md) can be deployed:</span></span>

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

<span data-ttu-id="fd482-108">Аналогичное правило политики с параметром для принятия допустимых номеров SKU доступно в виде встроенного определения политики.</span><span class="sxs-lookup"><span data-stu-id="fd482-108">A similar policy rule with a parameter for accepting the allowed SKUs is available as a built-in policy definition.</span></span> <span data-ttu-id="fd482-109">Встроенная политика имеет идентификатор ресурса `/providers/Microsoft.Authorization/policyDefinitions/7433c107-6db4-4ad1-b57a-a76dce0154a1`.</span><span class="sxs-lookup"><span data-stu-id="fd482-109">The built-in policy has the resource ID of `/providers/Microsoft.Authorization/policyDefinitions/7433c107-6db4-4ad1-b57a-a76dce0154a1`.</span></span> 

## <a name="define-permitted-access-tier"></a><span data-ttu-id="fd482-110">Определение разрешенного уровня доступа</span><span class="sxs-lookup"><span data-stu-id="fd482-110">Define permitted access tier</span></span>

<span data-ttu-id="fd482-111">Следующая политика задает тип [уровня доступа](../storage/blobs/storage-blob-storage-tiers.md), который можно указать для учетных записей хранения.</span><span class="sxs-lookup"><span data-stu-id="fd482-111">The following policy specifies the type of [access tier](../storage/blobs/storage-blob-storage-tiers.md) that can be specified for storage accounts:</span></span>

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

## <a name="ensure-encryption-is-enabled"></a><span data-ttu-id="fd482-112">Включение шифрования</span><span class="sxs-lookup"><span data-stu-id="fd482-112">Ensure encryption is enabled</span></span>

<span data-ttu-id="fd482-113">Следующая политика указывает, что для всех учетных записей хранения должно быть включено [шифрование службы хранилища](../storage/common/storage-service-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="fd482-113">The following policy requires all storage accounts to enable [Storage service encryption](../storage/common/storage-service-encryption.md):</span></span>

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

<span data-ttu-id="fd482-114">Это правило политики также доступно в виде встроенного определения политики с идентификатором ресурса `/providers/Microsoft.Authorization/policyDefinitions/7c5a74bf-ae94-4a74-8fcf-644d1e0e6e6f`.</span><span class="sxs-lookup"><span data-stu-id="fd482-114">This policy rule is also available as a built-in policy definition with the resource ID of `/providers/Microsoft.Authorization/policyDefinitions/7c5a74bf-ae94-4a74-8fcf-644d1e0e6e6f`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fd482-115">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fd482-115">Next steps</span></span>
* <span data-ttu-id="fd482-116">После определения правила политики (как показано в приведенных выше примерах) необходимо создать определение политики и назначить ей область.</span><span class="sxs-lookup"><span data-stu-id="fd482-116">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span></span> <span data-ttu-id="fd482-117">Областью может быть подписка, группа ресурсов или ресурс.</span><span class="sxs-lookup"><span data-stu-id="fd482-117">The scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="fd482-118">Сведения о назначении политик с помощью портала см. в статье [Назначение политик ресурсов и управление ими с помощью портала Azure](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fd482-118">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="fd482-119">Сведения о назначении политик с помощью REST API, PowerShell или Azure CLI см. в статье [Назначение политик ресурсов и управление ими](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="fd482-119">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="fd482-120">Руководство по использованию Resource Manager для эффективного управления подписками в организациях см [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md) (Шаблон Azure для организаций. Рекомендуемая система управления подпиской).</span><span class="sxs-lookup"><span data-stu-id="fd482-120">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

