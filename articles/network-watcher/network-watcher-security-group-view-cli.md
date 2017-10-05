---
title: "Анализ безопасности сети с помощью представления группы безопасности в Наблюдателе за сетями (Azure CLI 2.0) | Документация Майкрософт"
description: "Из этой статьи вы узнаете, как с помощью Azure CLI 2.0 анализировать безопасность виртуальных машин, используя представление группы безопасности."
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
ms.openlocfilehash: 1756e14819e3b7c79361c193413a1fcd7f24a4e6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-azure-cli-20"></a><span data-ttu-id="e7d23-103">Анализ безопасности виртуальных машин с помощью Azure CLI 2.0 и представления группы безопасности</span><span class="sxs-lookup"><span data-stu-id="e7d23-103">Analyze your Virtual Machine security with Security Group View using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="e7d23-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7d23-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="e7d23-105">Интерфейс командной строки 1.0</span><span class="sxs-lookup"><span data-stu-id="e7d23-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="e7d23-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e7d23-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="e7d23-107">REST API</span><span class="sxs-lookup"><span data-stu-id="e7d23-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="e7d23-108">Представление группы безопасности возвращает настроенные и действующие правила сетевой безопасности, применяемые к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="e7d23-108">Security group view returns configured and effective network security rules that are applied to a virtual machine.</span></span> <span data-ttu-id="e7d23-109">Эта возможность полезна для аудита и диагностики групп безопасности сети и настроенных на виртуальной машине правил, позволяющих обеспечить разрешение или отклонение трафика соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="e7d23-109">This capability is useful to audit and diagnose Network Security Groups and rules that are configured on a VM to ensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="e7d23-110">В этой статье мы покажем, как получить настроенные и действующие правила безопасности, применяемые к виртуальной машине, с помощью Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="e7d23-110">In this article, we show you how to retrieve the configured and effective security rules to a virtual machine using Azure CLI</span></span>


<span data-ttu-id="e7d23-111">В этой статье мы используем наш новейший интерфейс командной строки для модели развертывания ресурсов и управления ими, а именно Azure CLI 2.0. Этот интерфейс доступен для Windows, Mac и Linux.</span><span class="sxs-lookup"><span data-stu-id="e7d23-111">This article uses our next generation CLI for the resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="e7d23-112">Для выполнения действий, описанных в этой статье, требуется [установить интерфейс командной строки Azure для Mac, Linux и Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="e7d23-112">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e7d23-113">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="e7d23-113">Before you begin</span></span>

<span data-ttu-id="e7d23-114">В этом сценарии предполагается, что вы создали Наблюдатель за сетями в соответствии с инструкциями в статье [Create a Network Watcher](network-watcher-create.md) (Создание Наблюдателя за сетями).</span><span class="sxs-lookup"><span data-stu-id="e7d23-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="e7d23-115">Сценарий</span><span class="sxs-lookup"><span data-stu-id="e7d23-115">Scenario</span></span>

<span data-ttu-id="e7d23-116">В сценарии, описанном в этой статье, вы получите настроенные и действующие правила безопасности для указанной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="e7d23-116">The scenario covered in this article retrieves the configured and effective security rules for a given virtual machine.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="e7d23-117">Получение виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="e7d23-117">Get a VM</span></span>

<span data-ttu-id="e7d23-118">Для выполнения командлета `vm list` требуется виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="e7d23-118">A virtual machine is required to run the `vm list` cmdlet.</span></span> <span data-ttu-id="e7d23-119">Следующая команда выводит список виртуальных машин в группе ресурсов:</span><span class="sxs-lookup"><span data-stu-id="e7d23-119">The following command lists the virtual machines in a resource group:</span></span>

```azurecli
az vm list -resource-group resourceGroupName
```

<span data-ttu-id="e7d23-120">Определив виртуальную машину, можно получить ее идентификатор ресурса, используя команду `vm show`:</span><span class="sxs-lookup"><span data-stu-id="e7d23-120">Once you know the virtual machine, you can use the `vm show` cmdlet to get its resource Id:</span></span>

```azurecli
az vm show -resource-group resourceGroupName -name virtualMachineName
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="e7d23-121">Получение представления группы безопасности</span><span class="sxs-lookup"><span data-stu-id="e7d23-121">Retrieve security group view</span></span>

<span data-ttu-id="e7d23-122">Далее необходимо получить результат представления группы безопасности.</span><span class="sxs-lookup"><span data-stu-id="e7d23-122">The next step is to retrieve the security group view result.</span></span>

```azurecli
az network watcher show-security-group-view --resource-group resourceGroupName --vm vmName
```

## <a name="viewing-the-results"></a><span data-ttu-id="e7d23-123">Просмотр результатов</span><span class="sxs-lookup"><span data-stu-id="e7d23-123">Viewing the results</span></span>

<span data-ttu-id="e7d23-124">Далее приведен пример сокращенного ответа возвращенных результатов.</span><span class="sxs-lookup"><span data-stu-id="e7d23-124">The following example is a shortened response of the results returned.</span></span> <span data-ttu-id="e7d23-125">В результатах приводятся все действующие и применяемые правила безопасности на виртуальной машине, разделенные по группам **NetworkInterfaceSecurityRules**, **DefaultSecurityRules** и **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="e7d23-125">The results show all the effective and applied security rules on the virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="e7d23-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e7d23-126">Next steps</span></span>

<span data-ttu-id="e7d23-127">Сведения об автоматизации проверки групп безопасности сети см. в статье [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) (Выполнение аудита групп безопасности сети с помощью Наблюдателя за сетями).</span><span class="sxs-lookup"><span data-stu-id="e7d23-127">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) to learn how to automate validation of Network Security Groups.</span></span>

<span data-ttu-id="e7d23-128">Дополнительные сведения о правилах безопасности, применяемых к сетевым ресурсам, см. в статье [Security group view overview](network-watcher-security-group-view-overview.md) (Обзор представления группы безопасности).</span><span class="sxs-lookup"><span data-stu-id="e7d23-128">Learn more about the security rules that are applied to your network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
