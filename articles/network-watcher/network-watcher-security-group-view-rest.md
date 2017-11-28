---
title: "Сетевая безопасность aaaAnalyze с представлением группы безопасности Наблюдатель сети Azure — REST API | Документы Microsoft"
description: "В этой статье описывается, как toouse tooanalyze PowerShell в виртуальной машины, безопасность в представление \"Группа безопасности\"."
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
ms.openlocfilehash: 0858a64a9454816e05f06dadb9536ad0c755e90e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-rest-api"></a><span data-ttu-id="a1a1d-103">Анализ безопасности виртуальной машины с использованием представления группы безопасности в REST API</span><span class="sxs-lookup"><span data-stu-id="a1a1d-103">Analyze your Virtual Machine security with Security Group View using REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="a1a1d-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a1a1d-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="a1a1d-105">Интерфейс командной строки 1.0</span><span class="sxs-lookup"><span data-stu-id="a1a1d-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="a1a1d-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a1a1d-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="a1a1d-107">REST API</span><span class="sxs-lookup"><span data-stu-id="a1a1d-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="a1a1d-108">Представление "Группа безопасности" возвращает правила безопасности сети настроены и эффективным, примененные tooa виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="a1a1d-108">Security group view returns configured and effective network security rules that are applied tooa virtual machine.</span></span> <span data-ttu-id="a1a1d-109">Эта возможность является полезным tooaudit и диагностики сетевых групп безопасности и правила, настроенные на tooensure трафика виртуальных Машин выполняется правильно разрешен или запрещен.</span><span class="sxs-lookup"><span data-stu-id="a1a1d-109">This capability is useful tooaudit and diagnose Network Security Groups and rules that are configured on a VM tooensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="a1a1d-110">В этой статье мы покажем, как tooretrieve безопасности hello эффективный и примененные правила tooa виртуальной машины, с помощью API-интерфейса REST</span><span class="sxs-lookup"><span data-stu-id="a1a1d-110">In this article, we show you how tooretrieve hello effective and applied security rules tooa virtual machine using REST API</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a1a1d-111">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="a1a1d-111">Before you begin</span></span>

<span data-ttu-id="a1a1d-112">В этом случае вызов представление группы безопасности hello tooget hello API-интерфейса Rest Наблюдатель сети для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="a1a1d-112">In this scenario, you call hello Network Watcher Rest API tooget hello security group view for a virtual machine.</span></span> <span data-ttu-id="a1a1d-113">ARMclient — используется toocall hello REST API с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a1a1d-113">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="a1a1d-114">Пакет ARMClient можно скачать на сайте [Chocolatey](https://chocolatey.org/packages/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="a1a1d-114">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="a1a1d-115">Этот сценарий предполагает уже были выполнены шаги hello в [создать Наблюдатель сети](network-watcher-create.md) toocreate Наблюдатель сети.</span><span class="sxs-lookup"><span data-stu-id="a1a1d-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="a1a1d-116">сценарий Hello также предполагается, что группа ресурсов с действительной виртуальной машиной существует toobe используется.</span><span class="sxs-lookup"><span data-stu-id="a1a1d-116">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="a1a1d-117">Сценарий</span><span class="sxs-lookup"><span data-stu-id="a1a1d-117">Scenario</span></span>

<span data-ttu-id="a1a1d-118">Hello сценарий, описанный в этой статье извлекает hello эффективный и примененных правил для данной виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="a1a1d-118">hello scenario covered in this article retrieves hello effective and applied security rules for a given virtual machine.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="a1a1d-119">Вход с помощью ARMClient</span><span class="sxs-lookup"><span data-stu-id="a1a1d-119">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="a1a1d-120">Получение виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="a1a1d-120">Retrieve a virtual machine</span></span>

<span data-ttu-id="a1a1d-121">Запустите следующий сценарий tooreturn виртуальных machineThe hello после кода требуется переменных:</span><span class="sxs-lookup"><span data-stu-id="a1a1d-121">Run hello following script tooreturn a virtual machineThe following code needs variables:</span></span>

- <span data-ttu-id="a1a1d-122">**subscriptionId** -идентификатор подписки hello также можно получить с помощью hello **Get AzureRMSubscription** командлета.</span><span class="sxs-lookup"><span data-stu-id="a1a1d-122">**subscriptionId** - hello subscription id can also be retrieved with hello **Get-AzureRMSubscription** cmdlet.</span></span>
- <span data-ttu-id="a1a1d-123">**resourceGroupName** — hello имя группы ресурсов, содержащем виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="a1a1d-123">**resourceGroupName** - hello name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="a1a1d-124">Hello сведения, необходимые — hello **идентификатор** под типа hello `Microsoft.Compute/virtualMachines` в ответ, как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="a1a1d-124">hello information that is needed is hello **id** under hello type `Microsoft.Compute/virtualMachines` in response, as seen in hello following example:</span></span>

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

## <a name="get-security-group-view-for-virtual-machine"></a><span data-ttu-id="a1a1d-125">Получение представления группы безопасности для виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="a1a1d-125">Get security group view for virtual machine</span></span>

<span data-ttu-id="a1a1d-126">Следующий пример Hello запрашивает представление группы безопасности hello целевой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="a1a1d-126">hello following example requests hello security group view of a targeted virtual machine.</span></span> <span data-ttu-id="a1a1d-127">Hello результаты из этого примера может быть используется toocompare toohello правила и определяется toolook происхождения hello изменение параметров безопасности.</span><span class="sxs-lookup"><span data-stu-id="a1a1d-127">hello results from this example can be used toocompare toohello rules and security defined by hello origination toolook for configuration drift.</span></span>

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

## <a name="view-hello-response"></a><span data-ttu-id="a1a1d-128">Просмотреть ответ hello</span><span class="sxs-lookup"><span data-stu-id="a1a1d-128">View hello response</span></span>

<span data-ttu-id="a1a1d-129">Следующий образец Hello — hello ответ, возвращаемый из предшествующих команда hello.</span><span class="sxs-lookup"><span data-stu-id="a1a1d-129">hello following sample is hello response returned from hello preceding command.</span></span> <span data-ttu-id="a1a1d-130">Hello результаты показывают все правила безопасности эффективный и примененные hello на виртуальной машине hello разбит на группы **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, и  **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="a1a1d-130">hello results show all hello effective and applied security rules on hello virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="a1a1d-131">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a1a1d-131">Next steps</span></span>

<span data-ttu-id="a1a1d-132">Посетите [аудита безопасности сети группы (NSG) с Наблюдатель сети](network-watcher-security-group-view-powershell.md) toolearn способ проверки tooautomate групп безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="a1a1d-132">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-security-group-view-powershell.md) toolearn how tooautomate validation of Network Security Groups.</span></span>


