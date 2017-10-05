---
title: "Анализ безопасности сети с помощью представления группы безопасности Наблюдателя за сетями (REST API) | Документация Майкрософт"
description: "В этой статье вы узнаете, как проанализировать безопасность виртуальных машин, используя представление группы безопасности, с помощью PowerShell."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: a2f418fe-f5d2-43ed-8dc3-df0ed2a4d4ac
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: afced52b3ae6f3b7f400364f5ec7d049aa166590
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-rest-api"></a><span data-ttu-id="731b3-103">Анализ безопасности виртуальной машины с использованием представления группы безопасности в REST API</span><span class="sxs-lookup"><span data-stu-id="731b3-103">Analyze your Virtual Machine security with Security Group View using REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="731b3-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="731b3-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="731b3-105">Интерфейс командной строки 1.0</span><span class="sxs-lookup"><span data-stu-id="731b3-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="731b3-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="731b3-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="731b3-107">REST API</span><span class="sxs-lookup"><span data-stu-id="731b3-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="731b3-108">Представление группы безопасности возвращает настроенные и действующие правила сетевой безопасности, применяемые к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="731b3-108">Security group view returns configured and effective network security rules that are applied to a virtual machine.</span></span> <span data-ttu-id="731b3-109">Эта возможность полезна для аудита и диагностики групп безопасности сети и настроенных на виртуальной машине правил, позволяющих обеспечить разрешение или отклонение трафика соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="731b3-109">This capability is useful to audit and diagnose Network Security Groups and rules that are configured on a VM to ensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="731b3-110">В этой статье мы покажем, как получить эффективные правила безопасности и применить их к виртуальной машине с помощью REST API.</span><span class="sxs-lookup"><span data-stu-id="731b3-110">In this article, we show you how to retrieve the effective and applied security rules to a virtual machine using REST API</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="731b3-111">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="731b3-111">Before you begin</span></span>

<span data-ttu-id="731b3-112">В этом сценарии вы вызовите REST API Наблюдателя за сетями, чтобы получить представление группы безопасности для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="731b3-112">In this scenario, you call the Network Watcher Rest API to get the security group view for a virtual machine.</span></span> <span data-ttu-id="731b3-113">Чтобы вызвать REST API при помощи командлетов PowerShell, вам потребуется ARMClient.</span><span class="sxs-lookup"><span data-stu-id="731b3-113">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="731b3-114">Пакет ARMClient можно скачать на сайте [Chocolatey](https://chocolatey.org/packages/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="731b3-114">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="731b3-115">В этом сценарии предполагается, что вы создали Наблюдатель за сетями в соответствии с инструкциями в статье [Create an Azure Network Watcher instance](network-watcher-create.md) (Наблюдатель за сетями: создание экземпляра службы).</span><span class="sxs-lookup"><span data-stu-id="731b3-115">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="731b3-116">Предполагается также, что у вас есть группа ресурсов с допустимой виртуальной машиной.</span><span class="sxs-lookup"><span data-stu-id="731b3-116">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="731b3-117">Сценарий</span><span class="sxs-lookup"><span data-stu-id="731b3-117">Scenario</span></span>

<span data-ttu-id="731b3-118">В сценарии, описанном в этой статье, вы получите эффективные правила безопасности и примените их к указанной виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="731b3-118">The scenario covered in this article retrieves the effective and applied security rules for a given virtual machine.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="731b3-119">Вход с помощью ARMClient</span><span class="sxs-lookup"><span data-stu-id="731b3-119">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="731b3-120">Получение виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="731b3-120">Retrieve a virtual machine</span></span>

<span data-ttu-id="731b3-121">Чтобы получить сведения о виртуальной машине, выполните приведенный ниже скрипт, указав в нем следующие переменные:</span><span class="sxs-lookup"><span data-stu-id="731b3-121">Run the following script to return a virtual machineThe following code needs variables:</span></span>

- <span data-ttu-id="731b3-122">**subscriptionId** — идентификатор подписки, который можно получить с помощью командлета **Get-AzureRMSubscription**;</span><span class="sxs-lookup"><span data-stu-id="731b3-122">**subscriptionId** - The subscription id can also be retrieved with the **Get-AzureRMSubscription** cmdlet.</span></span>
- <span data-ttu-id="731b3-123">**resourceGroupName** — имя группы ресурсов, в которой содержатся виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="731b3-123">**resourceGroupName** - The name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="731b3-124">Вам потребуется **идентификатор**, расположенный под строкой `Microsoft.Compute/virtualMachines` в ответе, как показано в примере ниже.</span><span class="sxs-lookup"><span data-stu-id="731b3-124">The information that is needed is the **id** under the type `Microsoft.Compute/virtualMachines` in response, as seen in the following example:</span></span>

```json
...,
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft
.Network/networkInterfaces/{nicName}"
            }
          ]
        },
        "provisioningState": "Succeeded"
      },
      "resources": [
        {
          "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Com
pute/virtualMachines/{vmName}/extensions/CustomScriptExtension"
        }
      ],
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute
/virtualMachines/{vmName}",
      "name": "{vmName}"
    }
  ]
}
```

## <a name="get-security-group-view-for-virtual-machine"></a><span data-ttu-id="731b3-125">Получение представления группы безопасности для виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="731b3-125">Get security group view for virtual machine</span></span>

<span data-ttu-id="731b3-126">Приведенный ниже пример запрашивает представление группы безопасности целевой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="731b3-126">The following example requests the security group view of a targeted virtual machine.</span></span> <span data-ttu-id="731b3-127">Полученный после выполнения результат можно использовать, чтобы сравнить правила и параметры безопасности, определенные источником. Это позволит оценить изменения конфигурации.</span><span class="sxs-lookup"><span data-stu-id="731b3-127">The results from this example can be used to compare to the rules and security defined by the origination to look for configuration drift.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"
$networkWatcherName = "<network watcher name>"
$targetUri = "<uri of target resource>" # Example: /subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.compute/virtualMachine/$vmName

$requestBody = @"
{
    'targetResourceId': '${targetUri}'

}
"@
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/securityGroupView?api-version=2016-12-01" $requestBody -verbose
```

## <a name="view-the-response"></a><span data-ttu-id="731b3-128">Просмотр ответа</span><span class="sxs-lookup"><span data-stu-id="731b3-128">View the response</span></span>

<span data-ttu-id="731b3-129">Ниже приведен пример ответа, возвращенного после выполнения предыдущей команды.</span><span class="sxs-lookup"><span data-stu-id="731b3-129">The following sample is the response returned from the preceding command.</span></span> <span data-ttu-id="731b3-130">В результатах приводятся все действующие и применяемые правила безопасности на виртуальной машине, разделенные по группам **NetworkInterfaceSecurityRules**, **DefaultSecurityRules** и **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="731b3-130">The results show all the effective and applied security rules on the virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

```json

{
  "networkInterfaces": [
    {
      "securityRuleAssociations": {
        "networkInterfaceAssociation": {
          "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkInterfaces/{nicName}",
          "securityRules": [
            {
              "name": "default-allow-rdp",
              "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}/securityRules/default-allow-rdp",
              "etag": "W/\"d4c411d4-0d62-49dc-8092-3d4b57825740\"",
              "properties": {
                "provisioningState": "Succeeded",
                "protocol": "TCP",
                "sourcePortRange": "*",
                "destinationPortRange": "3389",
                "sourceAddressPrefix": "*",
                "destinationAddressPrefix": "*",
                "access": "Allow",
                "priority": 1000,
                "direction": "Inbound"
              }
            }
          ]
        },
        "defaultSecurityRules": [
          {
            "name": "AllowVnetInBound",
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}/defaultSecurityRules/",
            "properties": {
              "provisioningState": "Succeeded",
              "description": "Allow inbound traffic from all VMs in VNET",
              "protocol": "*",
              "sourcePortRange": "*",
              "destinationPortRange": "*",
              "sourceAddressPrefix": "VirtualNetwork",
              "destinationAddressPrefix": "VirtualNetwork",
              "access": "Allow",
              "priority": 65000,
              "direction": "Inbound"
            }
          },
          ...
        ],
        "effectiveSecurityRules": [
          {
            "name": "DefaultOutboundDenyAll",
            "protocol": "All",
            "sourcePortRange": "0-65535",
            "destinationPortRange": "0-65535",
            "sourceAddressPrefix": "*",
            "destinationAddressPrefix": "*",
            "access": "Deny",
            "priority": 65500,
            "direction": "Outbound"
          },
          ...
        ]
      }
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="731b3-131">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="731b3-131">Next steps</span></span>

<span data-ttu-id="731b3-132">Сведения об автоматизации проверки групп безопасности сети см. в статье [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-security-group-view-powershell.md) (Выполнение аудита групп безопасности сети с помощью Наблюдателя за сетями).</span><span class="sxs-lookup"><span data-stu-id="731b3-132">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-security-group-view-powershell.md) to learn how to automate validation of Network Security Groups.</span></span>


