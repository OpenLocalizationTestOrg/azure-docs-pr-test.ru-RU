---
title: "Обеспечение безопасности с помощью политик на виртуальных машинах Linux в Azure | Документация Майкрософт"
description: "Как применить политику к виртуальной машине Azure Resource Manager на основе Linux"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 06778ab4-f8ff-4eed-ae10-26a276fc3faa
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: singhkay
ms.openlocfilehash: 58eaab4fa03afc1e6a5e38bef691cce62a921ea9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="apply-policies-to-linux-vms-with-azure-resource-manager"></a><span data-ttu-id="bdc9d-103">Применение политик к виртуальным машинам Linux с помощью Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bdc9d-103">Apply policies to Linux VMs with Azure Resource Manager</span></span>
<span data-ttu-id="bdc9d-104">С помощью политик организация может обеспечить выполнение различных норм и правил во всей организации.</span><span class="sxs-lookup"><span data-stu-id="bdc9d-104">By using policies, an organization can enforce various conventions and rules throughout the enterprise.</span></span> <span data-ttu-id="bdc9d-105">Обязательные для выполнения стандарты поведения помогают снизить риск, что способствует успешной деятельности организации.</span><span class="sxs-lookup"><span data-stu-id="bdc9d-105">Enforcement of the desired behavior can help mitigate risk while contributing to the success of the organization.</span></span> <span data-ttu-id="bdc9d-106">В этой статье описано, как определить требуемое поведение для виртуальных машин вашей организации с помощью политик Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bdc9d-106">In this article, we describe how you can use Azure Resource Manager policies to define the desired behavior for your organization's Virtual Machines.</span></span>

<span data-ttu-id="bdc9d-107">Общие сведения о политиках см. в статье [Применение политик для управления ресурсами и контроля доступа](../../azure-resource-manager/resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="bdc9d-107">For an introduction to policies, see [Use Policy to manage resources and control access](../../azure-resource-manager/resource-manager-policy.md).</span></span>

## <a name="permitted-virtual-machines"></a><span data-ttu-id="bdc9d-108">Разрешенные виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="bdc9d-108">Permitted Virtual Machines</span></span>
<span data-ttu-id="bdc9d-109">Чтобы обеспечить совместимость виртуальных машин вашей организации с приложением, вы можете ограничить допустимые операционные системы.</span><span class="sxs-lookup"><span data-stu-id="bdc9d-109">To ensure that virtual machines for your organization are compatible with an application, you can restrict the permitted operating systems.</span></span> <span data-ttu-id="bdc9d-110">В этом примере политики вы разрешите только создание виртуальных машин на основе Ubuntu 14.04.2-LTS.</span><span class="sxs-lookup"><span data-stu-id="bdc9d-110">In the following policy example, you allow only Ubuntu 14.04.2-LTS Virtual Machines to be created.</span></span>

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "in": [
          "Microsoft.Compute/disks",
          "Microsoft.Compute/virtualMachines",
          "Microsoft.Compute/VirtualMachineScaleSets"
        ]
      },
      {
        "not": {
          "allOf": [
            {
              "field": "Microsoft.Compute/imagePublisher",
              "in": [
                "Canonical"
              ]
            },
            {
              "field": "Microsoft.Compute/imageOffer",
              "in": [
                "UbuntuServer"
              ]
            },
            {
              "field": "Microsoft.Compute/imageSku",
              "in": [
                "14.04.2-LTS"
              ]
            },
            {
              "field": "Microsoft.Compute/imageVersion",
              "in": [
                "latest"
              ]
            }
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

<span data-ttu-id="bdc9d-111">Чтобы разрешить любой образ Ubuntu LTS, измените предыдущую политику, используя подстановочный знак:</span><span class="sxs-lookup"><span data-stu-id="bdc9d-111">Use a wild card to modify the preceding policy to allow any Ubuntu LTS image:</span></span> 

```json
{
  "field": "Microsoft.Compute/virtualMachines/imageSku",
  "like": "*LTS"
}
```

<span data-ttu-id="bdc9d-112">Сведения о полях политики см. в разделе [Псевдонимы](../../azure-resource-manager/resource-manager-policy.md#aliases).</span><span class="sxs-lookup"><span data-stu-id="bdc9d-112">For information about policy fields, see [Policy aliases](../../azure-resource-manager/resource-manager-policy.md#aliases).</span></span>

## <a name="managed-disks"></a><span data-ttu-id="bdc9d-113">Управляемые диски</span><span class="sxs-lookup"><span data-stu-id="bdc9d-113">Managed disks</span></span>

<span data-ttu-id="bdc9d-114">Чтобы задать использование управляемых дисков, используйте следующую политику:</span><span class="sxs-lookup"><span data-stu-id="bdc9d-114">To require the use of managed disks, use the following policy:</span></span>

```json
{
  "if": {
    "anyOf": [
      {
        "allOf": [
          {
            "field": "type",
            "equals": "Microsoft.Compute/virtualMachines"
          },
          {
            "field": "Microsoft.Compute/virtualMachines/osDisk.uri",
            "exists": true
          }
        ]
      },
      {
        "allOf": [
          {
            "field": "type",
            "equals": "Microsoft.Compute/VirtualMachineScaleSets"
          },
          {
            "anyOf": [
              {
                "field": "Microsoft.Compute/VirtualMachineScaleSets/osDisk.vhdContainers",
                "exists": true
              },
              {
                "field": "Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl",
                "exists": true
              }
            ]
          }
        ]
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="images-for-virtual-machines"></a><span data-ttu-id="bdc9d-115">Образы виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="bdc9d-115">Images for Virtual Machines</span></span>

<span data-ttu-id="bdc9d-116">По соображениям безопасности можно требовать, чтобы в среде развертывались только утвержденные пользовательские образы.</span><span class="sxs-lookup"><span data-stu-id="bdc9d-116">For security reasons, you can require that only approved custom images are deployed in your environment.</span></span> <span data-ttu-id="bdc9d-117">Вы можете указать группу ресурсов, содержащую утвержденные образы, или конкретные утвержденные образы.</span><span class="sxs-lookup"><span data-stu-id="bdc9d-117">You can specify either the resource group that contains the approved images, or the specific approved images.</span></span>

<span data-ttu-id="bdc9d-118">В следующем примере требуются образы из группы утвержденных ресурсов:</span><span class="sxs-lookup"><span data-stu-id="bdc9d-118">The following example requires images from an approved resource group:</span></span>

```json
{
    "if": {
        "allOf": [
            {
                "field": "type",
                "in": [
                    "Microsoft.Compute/virtualMachines",
                    "Microsoft.Compute/VirtualMachineScaleSets"
                ]
            },
            {
                "not": {
                    "field": "Microsoft.Compute/imageId",
                    "contains": "resourceGroups/CustomImage"
                }
            }
        ]
    },
    "then": {
        "effect": "deny"
    }
} 
```

<span data-ttu-id="bdc9d-119">В следующем примере задаются идентификаторы утвержденных образов:</span><span class="sxs-lookup"><span data-stu-id="bdc9d-119">The following example specifies the approved image IDs:</span></span>

```json
{
    "field": "Microsoft.Compute/imageId",
    "in": ["{imageId1}","{imageId2}"]
}
```

## <a name="virtual-machine-extensions"></a><span data-ttu-id="bdc9d-120">Расширения виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="bdc9d-120">Virtual Machine extensions</span></span>

<span data-ttu-id="bdc9d-121">Вам может потребоваться запретить использование некоторых типов расширений.</span><span class="sxs-lookup"><span data-stu-id="bdc9d-121">You may want to forbid usage of certain types of extensions.</span></span> <span data-ttu-id="bdc9d-122">Например, расширение может оказаться несовместимым с некоторыми пользовательскими образами виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="bdc9d-122">For example, an extension may not be compatible with certain custom virtual machine images.</span></span> <span data-ttu-id="bdc9d-123">В следующем примере показано, как заблокировать определенное расширение.</span><span class="sxs-lookup"><span data-stu-id="bdc9d-123">The following example shows how to block a specific extension.</span></span> <span data-ttu-id="bdc9d-124">Чтобы определить модули, которые следует заблокировать, он использует издателя и тип.</span><span class="sxs-lookup"><span data-stu-id="bdc9d-124">It uses publisher and type to determine which extension to block.</span></span>

```json
{
    "if": {
        "allOf": [
            {
                "field": "type",
                "equals": "Microsoft.Compute/virtualMachines/extensions"
            },
            {
                "field": "Microsoft.Compute/virtualMachines/extensions/publisher",
                "equals": "Microsoft.Compute"
            },
            {
                "field": "Microsoft.Compute/virtualMachines/extensions/type",
                "equals": "{extension-type}"

      }
        ]
    },
    "then": {
        "effect": "deny"
    }
}
```


## <a name="next-steps"></a><span data-ttu-id="bdc9d-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bdc9d-125">Next steps</span></span>
* <span data-ttu-id="bdc9d-126">После определения правила политики (как показано в приведенных выше примерах) необходимо создать определение политики и назначить ей область.</span><span class="sxs-lookup"><span data-stu-id="bdc9d-126">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span></span> <span data-ttu-id="bdc9d-127">Областью может быть подписка, группа ресурсов или ресурс.</span><span class="sxs-lookup"><span data-stu-id="bdc9d-127">The scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="bdc9d-128">Сведения о назначении политик с помощью портала см. в статье [Назначение политик ресурсов и управление ими с помощью портала Azure](../../azure-resource-manager/resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="bdc9d-128">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](../../azure-resource-manager/resource-manager-policy-portal.md).</span></span> <span data-ttu-id="bdc9d-129">Сведения о назначении политик с помощью REST API, PowerShell или Azure CLI см. в статье [Назначение политик ресурсов и управление ими](../../azure-resource-manager/resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="bdc9d-129">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](../../azure-resource-manager/resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="bdc9d-130">Введение в политики ресурсов представлено в разделе [Общие сведения о политике ресурсов](../../azure-resource-manager/resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="bdc9d-130">For an introduction to resource policies, see [Resource policy overview](../../azure-resource-manager/resource-manager-policy.md).</span></span>
* <span data-ttu-id="bdc9d-131">Руководство по использованию Resource Manager для эффективного управления подписками в организациях см [Azure enterprise scaffold - prescriptive subscription governance](../../azure-resource-manager/resource-manager-subscription-governance.md) (Шаблон Azure для организаций. Рекомендуемая система управления подпиской).</span><span class="sxs-lookup"><span data-stu-id="bdc9d-131">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](../../azure-resource-manager/resource-manager-subscription-governance.md).</span></span>
