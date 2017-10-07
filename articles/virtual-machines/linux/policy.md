---
title: "aaaEnforce безопасности с помощью политик на виртуальных машинах Linux в Azure | Документы Microsoft"
description: "Как tooapply tooan политики виртуальная машина Azure Resource Manager Linux"
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
ms.openlocfilehash: 5abd0c937578aba7e72b62c65b4eef9a9737aa2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="apply-policies-toolinux-vms-with-azure-resource-manager"></a>Применение политики tooLinux виртуальных машин с помощью диспетчера ресурсов Azure
С помощью политик, организации могут применять различные соглашения и правила организации hello. Применение hello требуемого поведения снижения риска принимая участие toohello успех hello организации. В этой статье описывается использование диспетчера ресурсов Azure политики toodefine hello требуемого поведения для виртуальных машин вашей организации.

Toopolicies введение в разделе [политика использования ресурсов toomanage и контроля доступа](../../azure-resource-manager/resource-manager-policy.md).

## <a name="permitted-virtual-machines"></a>Разрешенные виртуальные машины
tooensure виртуальные машины для вашей организации, совместимы с приложением, можно ограничить hello допускается в операционных системах. В следующий пример политики hello, разрешить только Ubuntu 14.04.2-LTS виртуальным машинам toobe создан.

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

Используйте hello toomodify подстановочный знак, перед tooallow политики любое изображение Ubuntu LTS: 

```json
{
  "field": "Microsoft.Compute/virtualMachines/imageSku",
  "like": "*LTS"
}
```

Сведения о полях политики см. в разделе [Псевдонимы](../../azure-resource-manager/resource-manager-policy.md#aliases).

## <a name="managed-disks"></a>Управляемые диски

toorequire hello использование управляемых дисков hello используйте следующие политики:

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

## <a name="images-for-virtual-machines"></a>Образы виртуальных машин

По соображениям безопасности можно требовать, чтобы в среде развертывались только утвержденные пользовательские образы. Можно указать группы ресурсов hello, содержащее изображения hello утверждения или конкретных утвержденные образы hello.

Следующий пример Hello требует изображений из группы утвержденных ресурсов:

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

Hello следующий пример задает изображение hello утвержденные идентификаторы:

```json
{
    "field": "Microsoft.Compute/imageId",
    "in": ["{imageId1}","{imageId2}"]
}
```

## <a name="virtual-machine-extensions"></a>Расширения виртуальной машины

Вы можете tooforbid использование некоторых типов расширения. Например, расширение может оказаться несовместимым с некоторыми пользовательскими образами виртуальной машины. Следующий пример показывает как Hello tooblock определенное расширение. В нем издателям и типам toodetermine какие tooblock расширения.

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


## <a name="next-steps"></a>Дальнейшие действия
* После определения правила политики (как показано в предыдущих примерах hello), требуется определение политики toocreate hello и назначьте его tooa области. Hello область может быть подписки, группы ресурсов или ресурсов. политики tooassign через портал hello см. [tooassign портала используйте Azure и управление политиками ресурсов](../../azure-resource-manager/resource-manager-policy-portal.md). политики tooassign через API-Интерфейс REST, PowerShell или Azure CLI см. [назначение политики и управлять ими через сценарий](../../azure-resource-manager/resource-manager-policy-create-assign.md).
* Введение tooresource политики, в разделе [Общие сведения о политике ресурсов](../../azure-resource-manager/resource-manager-policy.md).
* Для получения рекомендаций по как предприятия могут использовать диспетчер ресурсов tooeffectively управление подписками см. в разделе [корпоративные функции формирования шаблонов - управление конкретные подписки](../../azure-resource-manager/resource-manager-subscription-governance.md).
