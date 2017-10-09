---
title: "Сетевая безопасность aaaAnalyze с представлением группы безопасности Наблюдатель сети Azure - Azure CLI 1.0 | Документы Microsoft"
description: "В этой статье описывается, как tooanalyze toouse Azure CLI 1.0 a виртуальных машин безопасности с представлением группы безопасности."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: a986ff4f-7e0c-4994-95e1-4ac824986500
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 96383a734b94d215d5b0f3d47339e46940d700b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-azure-cli-10"></a><span data-ttu-id="1c0ee-103">Анализ безопасности виртуальных машин с помощью Azure CLI 1.0 и представления группы безопасности</span><span class="sxs-lookup"><span data-stu-id="1c0ee-103">Analyze your Virtual Machine security with Security Group View using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="1c0ee-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1c0ee-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="1c0ee-105">Интерфейс командной строки 1.0</span><span class="sxs-lookup"><span data-stu-id="1c0ee-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="1c0ee-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1c0ee-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="1c0ee-107">REST API</span><span class="sxs-lookup"><span data-stu-id="1c0ee-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="1c0ee-108">Представление "Группа безопасности" возвращает правила безопасности сети настроены и эффективным, примененные tooa виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="1c0ee-108">Security group view returns configured and effective network security rules that are applied tooa virtual machine.</span></span> <span data-ttu-id="1c0ee-109">Эта возможность является полезным tooaudit и диагностики сетевых групп безопасности и правила, настроенные на tooensure трафика виртуальных Машин выполняется правильно разрешен или запрещен.</span><span class="sxs-lookup"><span data-stu-id="1c0ee-109">This capability is useful tooaudit and diagnose Network Security Groups and rules that are configured on a VM tooensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="1c0ee-110">В этой статье мы показано, как настроить tooretrieve hello и эффективной защиты правила tooa виртуальной машины с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="1c0ee-110">In this article, we show you how tooretrieve hello configured and effective security rules tooa virtual machine using Azure CLI</span></span>

<span data-ttu-id="1c0ee-111">В этой статье используется кроссплатформенной Azure CLI 1.0, доступный для Windows, Mac и Linux.</span><span class="sxs-lookup"><span data-stu-id="1c0ee-111">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="1c0ee-112">Наблюдатель за сетями в настоящее время использует Azure CLI 1.0 в качестве интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="1c0ee-112">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1c0ee-113">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="1c0ee-113">Before you begin</span></span>

<span data-ttu-id="1c0ee-114">Этот сценарий предполагает уже были выполнены шаги hello в [создать Наблюдатель сети](network-watcher-create.md) toocreate Наблюдатель сети.</span><span class="sxs-lookup"><span data-stu-id="1c0ee-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="1c0ee-115">Сценарий</span><span class="sxs-lookup"><span data-stu-id="1c0ee-115">Scenario</span></span>

<span data-ttu-id="1c0ee-116">Hello сценарий, описанный в этой статье извлекает настроен hello и правила безопасности для данной виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="1c0ee-116">hello scenario covered in this article retrieves hello configured and effective security rules for a given virtual machine.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="1c0ee-117">Получение виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="1c0ee-117">Get a VM</span></span>

<span data-ttu-id="1c0ee-118">Виртуальная машина — hello необходимые toorun `vm list` командлета.</span><span class="sxs-lookup"><span data-stu-id="1c0ee-118">A virtual machine is required toorun hello `vm list` cmdlet.</span></span> <span data-ttu-id="1c0ee-119">Hello следующая команда выводит список виртуальных machinese hello в группе ресурсов:</span><span class="sxs-lookup"><span data-stu-id="1c0ee-119">hello following command lists hello virtual machinese in a resource group:</span></span>

```azurecli
azure vm list -g resourceGroupName
```

<span data-ttu-id="1c0ee-120">Если известно hello виртуальной машины, можно использовать hello `vm show` tooget командлет его идентификатором ресурса:</span><span class="sxs-lookup"><span data-stu-id="1c0ee-120">Once you know hello virtual machine, you can use hello `vm show` cmdlet tooget its resource Id:</span></span>

```azurecli
azure vm show -g resourceGroupName -n virtualMachineName
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="1c0ee-121">Получение представления группы безопасности</span><span class="sxs-lookup"><span data-stu-id="1c0ee-121">Retrieve security group view</span></span>

<span data-ttu-id="1c0ee-122">Hello следующим шагом является результат представления группы безопасности hello tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="1c0ee-122">hello next step is tooretrieve hello security group view result.</span></span> <span data-ttu-id="1c0ee-123">Добавление hello «--json» флаг отформатирует результаты hello в формате json.</span><span class="sxs-lookup"><span data-stu-id="1c0ee-123">Adding hello "--json" flag will format hello results in json.</span></span>

```azurecli
azure network watcher security-group-view -g resourceGroupName -n networkWatcherName -t targetResourceId --json
```

## <a name="viewing-hello-results"></a><span data-ttu-id="1c0ee-124">Просмотр результатов hello</span><span class="sxs-lookup"><span data-stu-id="1c0ee-124">Viewing hello results</span></span>

<span data-ttu-id="1c0ee-125">Hello следующий пример — сокращенный ответа возвращаемых результатов hello.</span><span class="sxs-lookup"><span data-stu-id="1c0ee-125">hello following example is a shortened response of hello results returned.</span></span> <span data-ttu-id="1c0ee-126">Hello результаты показывают все правила безопасности эффективный и примененные hello на виртуальной машине hello разбит на группы **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, и  **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="1c0ee-126">hello results show all hello effective and applied security rules on hello virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

```json
{
  "networkInterfaces": [
    {
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testnic",
      "securityRuleAssociations": {
        "networkInterfaceAssociation": {
          "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testvm",
          "securityRules": [
            {
              "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/test-nsg/securityRules/default-allow-rdp",
              "protocol": "TCP",
              "sourcePortRange": "*",
              "destinationPortRange": "3389",
              "sourceAddressPrefix": "*",
              "destinationAddressPrefix": "*",
              "access": "Allow",
              "priority": 1000,
              "direction": "Inbound",
              "provisioningState": "Succeeded",
              "name": "default-allow-rdp",
              "etag": "W/\"00000000-0000-0000-0000-000000000000\""
            }
          ]
        },
        "defaultSecurityRules": [
          {
            "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/networkSecurityGroups//defaultSecurityRules/",
            "description": "Allow inbound traffic from all VMs in VNET",
            "protocol": "*",
            "sourcePortRange": "*",
            "destinationPortRange": "*",
            "sourceAddressPrefix": "VirtualNetwork",
            "destinationAddressPrefix": "VirtualNetwork",
            "access": "Allow",
            "priority": 65000,
            "direction": "Inbound",
            "provisioningState": "Succeeded",
            "name": "AllowVnetInBound"
          }
        ]
      }
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="1c0ee-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1c0ee-127">Next steps</span></span>

<span data-ttu-id="1c0ee-128">Посетите [аудита безопасности сети группы (NSG) с Наблюдатель сети](network-watcher-nsg-auditing-powershell.md) toolearn способ проверки tooautomate групп безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="1c0ee-128">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) toolearn how tooautomate validation of Network Security Groups.</span></span>

<span data-ttu-id="1c0ee-129">Дополнительные сведения о правилах безопасности hello, которые будут применяться tooyour сетевым ресурсам, посетив [Общие сведения о представлении группы безопасности](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="1c0ee-129">Learn more about hello security rules that are applied tooyour network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
