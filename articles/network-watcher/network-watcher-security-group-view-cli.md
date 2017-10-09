---
title: "Сетевая безопасность aaaAnalyze с представлением группы безопасности Наблюдатель сети Azure - CLI Azure 2.0 | Документы Microsoft"
description: "В этой статье описывается, как tooanalyze toouse Azure CLI 2.0 a виртуальных машин безопасности с представлением группы безопасности."
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
ms.openlocfilehash: 31a4cd628f54d7548f495251fd275f099e79a060
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-azure-cli-20"></a><span data-ttu-id="13ea8-103">Анализ безопасности виртуальных машин с помощью Azure CLI 2.0 и представления группы безопасности</span><span class="sxs-lookup"><span data-stu-id="13ea8-103">Analyze your Virtual Machine security with Security Group View using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="13ea8-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="13ea8-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="13ea8-105">Интерфейс командной строки 1.0</span><span class="sxs-lookup"><span data-stu-id="13ea8-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="13ea8-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="13ea8-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="13ea8-107">REST API</span><span class="sxs-lookup"><span data-stu-id="13ea8-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="13ea8-108">Представление "Группа безопасности" возвращает правила безопасности сети настроены и эффективным, примененные tooa виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="13ea8-108">Security group view returns configured and effective network security rules that are applied tooa virtual machine.</span></span> <span data-ttu-id="13ea8-109">Эта возможность является полезным tooaudit и диагностики сетевых групп безопасности и правила, настроенные на tooensure трафика виртуальных Машин выполняется правильно разрешен или запрещен.</span><span class="sxs-lookup"><span data-stu-id="13ea8-109">This capability is useful tooaudit and diagnose Network Security Groups and rules that are configured on a VM tooensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="13ea8-110">В этой статье мы показано, как настроить tooretrieve hello и эффективной защиты правила tooa виртуальной машины с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="13ea8-110">In this article, we show you how tooretrieve hello configured and effective security rules tooa virtual machine using Azure CLI</span></span>


<span data-ttu-id="13ea8-111">В этой статье используется нашей следующего поколения CLI для модели развертывания управления ресурса hello Azure CLI 2.0, которая доступна для Windows, Mac и Linux.</span><span class="sxs-lookup"><span data-stu-id="13ea8-111">This article uses our next generation CLI for hello resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="13ea8-112">tooperform hello шаги в этой статье, вы должны слишком[Установка hello интерфейса командной строки Azure для Mac, Linux и Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="13ea8-112">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="13ea8-113">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="13ea8-113">Before you begin</span></span>

<span data-ttu-id="13ea8-114">Этот сценарий предполагает уже были выполнены шаги hello в [создать Наблюдатель сети](network-watcher-create.md) toocreate Наблюдатель сети.</span><span class="sxs-lookup"><span data-stu-id="13ea8-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="13ea8-115">Сценарий</span><span class="sxs-lookup"><span data-stu-id="13ea8-115">Scenario</span></span>

<span data-ttu-id="13ea8-116">Hello сценарий, описанный в этой статье извлекает настроен hello и правила безопасности для данной виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="13ea8-116">hello scenario covered in this article retrieves hello configured and effective security rules for a given virtual machine.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="13ea8-117">Получение виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="13ea8-117">Get a VM</span></span>

<span data-ttu-id="13ea8-118">Виртуальная машина — hello необходимые toorun `vm list` командлета.</span><span class="sxs-lookup"><span data-stu-id="13ea8-118">A virtual machine is required toorun hello `vm list` cmdlet.</span></span> <span data-ttu-id="13ea8-119">Hello следующая команда перечисляет hello виртуальных машин в группе ресурсов:</span><span class="sxs-lookup"><span data-stu-id="13ea8-119">hello following command lists hello virtual machines in a resource group:</span></span>

```azurecli
az vm list -resource-group resourceGroupName
```

<span data-ttu-id="13ea8-120">Если известно hello виртуальной машины, можно использовать hello `vm show` tooget командлет его идентификатором ресурса:</span><span class="sxs-lookup"><span data-stu-id="13ea8-120">Once you know hello virtual machine, you can use hello `vm show` cmdlet tooget its resource Id:</span></span>

```azurecli
az vm show -resource-group resourceGroupName -name virtualMachineName
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="13ea8-121">Получение представления группы безопасности</span><span class="sxs-lookup"><span data-stu-id="13ea8-121">Retrieve security group view</span></span>

<span data-ttu-id="13ea8-122">Hello следующим шагом является результат представления группы безопасности hello tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="13ea8-122">hello next step is tooretrieve hello security group view result.</span></span>

```azurecli
az network watcher show-security-group-view --resource-group resourceGroupName --vm vmName
```

## <a name="viewing-hello-results"></a><span data-ttu-id="13ea8-123">Просмотр результатов hello</span><span class="sxs-lookup"><span data-stu-id="13ea8-123">Viewing hello results</span></span>

<span data-ttu-id="13ea8-124">Hello следующий пример — сокращенный ответа возвращаемых результатов hello.</span><span class="sxs-lookup"><span data-stu-id="13ea8-124">hello following example is a shortened response of hello results returned.</span></span> <span data-ttu-id="13ea8-125">Hello результаты показывают все правила безопасности эффективный и примененные hello на виртуальной машине hello разбит на группы **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, и  **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="13ea8-125">hello results show all hello effective and applied security rules on hello virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

```json
{
  "networkInterfaces": [
    {
      "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkInterfaces/{nicName}",
      "resourceGroup": "{resourceGroupName}",
      "securityRuleAssociations": {
        "defaultSecurityRules": [
          {
            "access": "Allow",
            "description": "Allow inbound traffic from all VMs in VNET",
            "destinationAddressPrefix": "VirtualNetwork",
            "destinationPortRange": "*",
            "direction": "Inbound",
            "etag": null,
            "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups//providers/Microsoft.Network/networkSecurityGroups/{nsgName}/defaultSecurityRules/AllowVnetInBound",
            "name": "AllowVnetInBound",
            "priority": 65000,
            "protocol": "*",
            "provisioningState": "Succeeded",
            "resourceGroup": "",
            "sourceAddressPrefix": "VirtualNetwork",
            "sourcePortRange": "*"
          }...
        ],
        "effectiveSecurityRules": [
          {
            "access": "Deny",
            "destinationAddressPrefix": "*",
            "destinationPortRange": "0-65535",
            "direction": "Outbound",
            "expandedDestinationAddressPrefix": null,
            "expandedSourceAddressPrefix": null,
            "name": "DefaultOutboundDenyAll",
            "priority": 65500,
            "protocol": "All",
            "sourceAddressPrefix": "*",
            "sourcePortRange": "0-65535"
          },
          {
            "access": "Allow",
            "destinationAddressPrefix": "VirtualNetwork",
            "destinationPortRange": "0-65535",
            "direction": "Outbound",
            "expandedDestinationAddressPrefix": [
              "10.1.0.0/24",
              "168.63.129.16/32"
            ],
            "expandedSourceAddressPrefix": [
              "10.1.0.0/24",
              "168.63.129.16/32"
            ],
            "name": "DefaultRule_AllowVnetOutBound",
            "priority": 65000,
            "protocol": "All",
            "sourceAddressPrefix": "VirtualNetwork",
            "sourcePortRange": "0-65535"
          },...
        ],
        "networkInterfaceAssociation": {
          "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkInterfaces/{nicName}",
          "resourceGroup": "{resourceGroupName}",
          "securityRules": [
            {
              "access": "Allow",
              "description": null,
              "destinationAddressPrefix": "*",
              "destinationPortRange": "3389",
              "direction": "Inbound",
              "etag": "W/\"efb606c1-2d54-475a-ab20-da3f80393577\"",
              "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}/securityRules/default-allow-rdp",
              "name": "default-allow-rdp",
              "priority": 1000,
              "protocol": "TCP",
              "provisioningState": "Succeeded",
              "resourceGroup": "{resourceGroupName}",
              "sourceAddressPrefix": "*",
              "sourcePortRange": "*"
            }
          ]
        },
        "subnetAssociation": null
      }
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="13ea8-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="13ea8-126">Next steps</span></span>

<span data-ttu-id="13ea8-127">Посетите [аудита безопасности сети группы (NSG) с Наблюдатель сети](network-watcher-nsg-auditing-powershell.md) toolearn способ проверки tooautomate групп безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="13ea8-127">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) toolearn how tooautomate validation of Network Security Groups.</span></span>

<span data-ttu-id="13ea8-128">Дополнительные сведения о правилах безопасности hello, которые будут применяться tooyour сетевым ресурсам, посетив [Общие сведения о представлении группы безопасности](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="13ea8-128">Learn more about hello security rules that are applied tooyour network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
