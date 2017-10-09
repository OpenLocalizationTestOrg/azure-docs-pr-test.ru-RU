---
title: "aaaEnforce безопасности с помощью политик на виртуальных машинах Windows в Azure | Документы Microsoft"
description: "Как tooapply tooan политики виртуальной машины Windows Azure Resource Manager"
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0b71ba54-01db-43ad-9bca-8ab358ae141b
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: kasing
ms.openlocfilehash: b31c8a03ecf8eed6a929f97fe4146ea14364404f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="apply-policies-toowindows-vms-with-azure-resource-manager"></a><span data-ttu-id="32b93-103">Применение политики tooWindows виртуальных машин с помощью диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="32b93-103">Apply policies tooWindows VMs with Azure Resource Manager</span></span>
<span data-ttu-id="32b93-104">С помощью политик, организации могут применять различные соглашения и правила организации hello.</span><span class="sxs-lookup"><span data-stu-id="32b93-104">By using policies, an organization can enforce various conventions and rules throughout hello enterprise.</span></span> <span data-ttu-id="32b93-105">Применение hello требуемого поведения снижения риска принимая участие toohello успех hello организации.</span><span class="sxs-lookup"><span data-stu-id="32b93-105">Enforcement of hello desired behavior can help mitigate risk while contributing toohello success of hello organization.</span></span> <span data-ttu-id="32b93-106">В этой статье описывается использование диспетчера ресурсов Azure политики toodefine hello требуемого поведения для виртуальных машин вашей организации.</span><span class="sxs-lookup"><span data-stu-id="32b93-106">In this article, we describe how you can use Azure Resource Manager policies toodefine hello desired behavior for your organization’s Virtual Machines.</span></span>

<span data-ttu-id="32b93-107">Toopolicies введение в разделе [политика использования ресурсов toomanage и контроля доступа](../../azure-resource-manager/resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="32b93-107">For an introduction toopolicies, see [Use Policy toomanage resources and control access](../../azure-resource-manager/resource-manager-policy.md).</span></span>

## <a name="permitted-virtual-machines"></a><span data-ttu-id="32b93-108">Разрешенные виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="32b93-108">Permitted Virtual Machines</span></span>
<span data-ttu-id="32b93-109">tooensure виртуальные машины для вашей организации, совместимы с приложением, можно ограничить hello допускается в операционных системах.</span><span class="sxs-lookup"><span data-stu-id="32b93-109">tooensure that virtual machines for your organization are compatible with an application, you can restrict hello permitted operating systems.</span></span> <span data-ttu-id="32b93-110">В следующий пример политики hello разрешить только виртуальные машины Windows Server 2012 R2 Datacenter toobe создан:</span><span class="sxs-lookup"><span data-stu-id="32b93-110">In hello following policy example, you allow only Windows Server 2012 R2 Datacenter Virtual Machines toobe created:</span></span>

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
                "MicrosoftWindowsServer"
              ]
            },
            {
              "field": "Microsoft.Compute/imageOffer",
              "in": [
                "WindowsServer"
              ]
            },
            {
              "field": "Microsoft.Compute/imageSku",
              "in": [
                "2012-R2-Datacenter"
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

<span data-ttu-id="32b93-111">Используйте hello toomodify подстановочный знак, перед любой образ Windows Server Datacenter tooallow политики:</span><span class="sxs-lookup"><span data-stu-id="32b93-111">Use a wild card toomodify hello preceding policy tooallow any Windows Server Datacenter image:</span></span>

```json
{
  "field": "Microsoft.Compute/imageSku",
  "like": "*Datacenter"
}
```

<span data-ttu-id="32b93-112">Используйте hello toomodify anyOf предшествующий tooallow политики любой Windows Server 2012 R2 Datacenter или более поздней версии образа:</span><span class="sxs-lookup"><span data-stu-id="32b93-112">Use anyOf toomodify hello preceding policy tooallow any Windows Server 2012 R2 Datacenter or higher image:</span></span>

```json
{
  "anyOf": [
    {
      "field": "Microsoft.Compute/imageSku",
      "like": "2012-R2-Datacenter*"
    },
    {
      "field": "Microsoft.Compute/imageSku",
      "like": "2016-Datacenter*"
    }
  ]
}
```

<span data-ttu-id="32b93-113">Сведения о полях политики см. в разделе [Псевдонимы](../../azure-resource-manager/resource-manager-policy.md#aliases).</span><span class="sxs-lookup"><span data-stu-id="32b93-113">For information about policy fields, see [Policy aliases](../../azure-resource-manager/resource-manager-policy.md#aliases).</span></span>

## <a name="managed-disks"></a><span data-ttu-id="32b93-114">Управляемые диски</span><span class="sxs-lookup"><span data-stu-id="32b93-114">Managed disks</span></span>

<span data-ttu-id="32b93-115">toorequire hello использование управляемых дисков hello используйте следующие политики:</span><span class="sxs-lookup"><span data-stu-id="32b93-115">toorequire hello use of managed disks, use hello following policy:</span></span>

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

## <a name="images-for-virtual-machines"></a><span data-ttu-id="32b93-116">Образы виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="32b93-116">Images for Virtual Machines</span></span>

<span data-ttu-id="32b93-117">По соображениям безопасности можно требовать, чтобы в среде развертывались только утвержденные пользовательские образы.</span><span class="sxs-lookup"><span data-stu-id="32b93-117">For security reasons, you can require that only approved custom images are deployed in your environment.</span></span> <span data-ttu-id="32b93-118">Можно указать группы ресурсов hello, содержащее изображения hello утверждения или конкретных утвержденные образы hello.</span><span class="sxs-lookup"><span data-stu-id="32b93-118">You can specify either hello resource group that contains hello approved images, or hello specific approved images.</span></span>

<span data-ttu-id="32b93-119">Следующий пример Hello требует изображений из группы утвержденных ресурсов:</span><span class="sxs-lookup"><span data-stu-id="32b93-119">hello following example requires images from an approved resource group:</span></span>

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

<span data-ttu-id="32b93-120">Hello следующий пример задает изображение hello утвержденные идентификаторы:</span><span class="sxs-lookup"><span data-stu-id="32b93-120">hello following example specifies hello approved image IDs:</span></span>

```json
{
    "field": "Microsoft.Compute/imageId",
    "in": ["{imageId1}","{imageId2}"]
}
```

## <a name="virtual-machine-extensions"></a><span data-ttu-id="32b93-121">Расширения виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="32b93-121">Virtual Machine extensions</span></span>

<span data-ttu-id="32b93-122">Вы можете tooforbid использование некоторых типов расширения.</span><span class="sxs-lookup"><span data-stu-id="32b93-122">You may want tooforbid usage of certain types of extensions.</span></span> <span data-ttu-id="32b93-123">Например, расширение может оказаться несовместимым с некоторыми пользовательскими образами виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="32b93-123">For example, an extension may not be compatible with certain custom virtual machine images.</span></span> <span data-ttu-id="32b93-124">Следующий пример показывает как Hello tooblock определенное расширение.</span><span class="sxs-lookup"><span data-stu-id="32b93-124">hello following example shows how tooblock a specific extension.</span></span> <span data-ttu-id="32b93-125">В нем издателям и типам toodetermine какие tooblock расширения.</span><span class="sxs-lookup"><span data-stu-id="32b93-125">It uses publisher and type toodetermine which extension tooblock.</span></span>

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


## <a name="azure-hybrid-use-benefit"></a><span data-ttu-id="32b93-126">Программа преимуществ гибридного использования Azure</span><span class="sxs-lookup"><span data-stu-id="32b93-126">Azure Hybrid Use Benefit</span></span>

<span data-ttu-id="32b93-127">При наличии лицензии локальной плата за лицензии hello можно сохранить на виртуальных машинах.</span><span class="sxs-lookup"><span data-stu-id="32b93-127">When you have an on-premise license, you can save hello license fee on your virtual machines.</span></span> <span data-ttu-id="32b93-128">При отсутствии лицензии hello следует запрещать параметр hello.</span><span class="sxs-lookup"><span data-stu-id="32b93-128">When you don't have hello license, you should forbid hello option.</span></span> <span data-ttu-id="32b93-129">следующие политики Hello запрещает использование преимуществ использования гибридной Azure (AHUB):</span><span class="sxs-lookup"><span data-stu-id="32b93-129">hello following policy forbids usage of Azure Hybrid Use Benefit (AHUB):</span></span>

```json
{
    "if": {
        "allOf": [
            {
                "field": "type",
                "in":[ "Microsoft.Compute/virtualMachines","Microsoft.Compute/VirtualMachineScaleSets"]
            },
            {
                "field": "Microsoft.Compute/licenseType",
                "exists": true
            }
        ]
    },
    "then": {
        "effect": "deny"
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="32b93-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="32b93-130">Next steps</span></span>
* <span data-ttu-id="32b93-131">После определения правила политики (как показано в предыдущих примерах hello), требуется определение политики toocreate hello и назначьте его tooa области.</span><span class="sxs-lookup"><span data-stu-id="32b93-131">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="32b93-132">Hello область может быть подписки, группы ресурсов или ресурсов.</span><span class="sxs-lookup"><span data-stu-id="32b93-132">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="32b93-133">политики tooassign через портал hello см. [tooassign портала используйте Azure и управление политиками ресурсов](../../azure-resource-manager/resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="32b93-133">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](../../azure-resource-manager/resource-manager-policy-portal.md).</span></span> <span data-ttu-id="32b93-134">политики tooassign через API-Интерфейс REST, PowerShell или Azure CLI см. [назначение политики и управлять ими через сценарий](../../azure-resource-manager/resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="32b93-134">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](../../azure-resource-manager/resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="32b93-135">Введение tooresource политики, в разделе [Общие сведения о политике ресурсов](../../azure-resource-manager/resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="32b93-135">For an introduction tooresource policies, see [Resource policy overview](../../azure-resource-manager/resource-manager-policy.md).</span></span>
* <span data-ttu-id="32b93-136">Для получения рекомендаций по как предприятия могут использовать диспетчер ресурсов tooeffectively управление подписками см. в разделе [корпоративные функции формирования шаблонов - управление конкретные подписки](../../azure-resource-manager/resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="32b93-136">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](../../azure-resource-manager/resource-manager-subscription-governance.md).</span></span>
