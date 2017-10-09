---
title: "Сетевая безопасность aaaAnalyze с представлением группы безопасности Наблюдатель сети Azure - PowerShell | Документы Microsoft"
description: "В этой статье описывается, как toouse tooanalyze PowerShell в виртуальной машины, безопасность в представление \"Группа безопасности\"."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 04e76b49-6a1b-4d0f-9a9b-51cf2f4df5a2
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 5e1990d97899bd8585025ec13dd556ab2e034c3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-powershell"></a><span data-ttu-id="ffb86-103">Анализ безопасности виртуальной машины с использованием представления группы безопасности (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="ffb86-103">Analyze your Virtual Machine security with Security Group View using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="ffb86-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ffb86-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="ffb86-105">Интерфейс командной строки 1.0</span><span class="sxs-lookup"><span data-stu-id="ffb86-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="ffb86-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ffb86-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="ffb86-107">REST API</span><span class="sxs-lookup"><span data-stu-id="ffb86-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="ffb86-108">Представление "Группа безопасности" возвращает правила безопасности сети настроены и эффективным, примененные tooa виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="ffb86-108">Security group view returns configured and effective network security rules that are applied tooa virtual machine.</span></span> <span data-ttu-id="ffb86-109">Эта возможность является полезным tooaudit и диагностики сетевых групп безопасности и правила, настроенные на tooensure трафика виртуальных Машин выполняется правильно разрешен или запрещен.</span><span class="sxs-lookup"><span data-stu-id="ffb86-109">This capability is useful tooaudit and diagnose Network Security Groups and rules that are configured on a VM tooensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="ffb86-110">В этой статье мы показано, как настроить tooretrieve hello и эффективной защиты правила tooa виртуальной машины с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="ffb86-110">In this article, we show you how tooretrieve hello configured and effective security rules tooa virtual machine using PowerShell</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ffb86-111">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="ffb86-111">Before you begin</span></span>

<span data-ttu-id="ffb86-112">В этом сценарии запуска hello `Get-AzureRmNetworkWatcherSecurityGroupView` сведения о правиле безопасности командлет tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="ffb86-112">In this scenario, you run hello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet tooretrieve hello security rule information.</span></span>

<span data-ttu-id="ffb86-113">Этот сценарий предполагает уже были выполнены шаги hello в [создать Наблюдатель сети](network-watcher-create.md) toocreate Наблюдатель сети.</span><span class="sxs-lookup"><span data-stu-id="ffb86-113">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="ffb86-114">Сценарий</span><span class="sxs-lookup"><span data-stu-id="ffb86-114">Scenario</span></span>

<span data-ttu-id="ffb86-115">Hello сценарий, описанный в этой статье извлекает настроен hello и правила безопасности для данной виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="ffb86-115">hello scenario covered in this article retrieves hello configured and effective security rules for a given virtual machine.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="ffb86-116">Извлечение Наблюдателя за сетями</span><span class="sxs-lookup"><span data-stu-id="ffb86-116">Retrieve Network Watcher</span></span>

<span data-ttu-id="ffb86-117">Первым шагом Hello — экземпляр Наблюдатель сети tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="ffb86-117">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="ffb86-118">Эта переменная передается toohello `Get-AzureRmNetworkWatcherSecurityGroupView` командлета.</span><span class="sxs-lookup"><span data-stu-id="ffb86-118">This variable is passed toohello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="get-a-vm"></a><span data-ttu-id="ffb86-119">Получение виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="ffb86-119">Get a VM</span></span>

<span data-ttu-id="ffb86-120">Виртуальная машина — hello необходимые toorun `Get-AzureRmNetworkWatcherSecurityGroupView` командлета для.</span><span class="sxs-lookup"><span data-stu-id="ffb86-120">A virtual machine is required toorun hello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet against.</span></span> <span data-ttu-id="ffb86-121">Следующий пример Hello получает объект виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="ffb86-121">hello following example gets a VM object.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName testrg -Name testvm1
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="ffb86-122">Получение представления группы безопасности</span><span class="sxs-lookup"><span data-stu-id="ffb86-122">Retrieve security group view</span></span>

<span data-ttu-id="ffb86-123">Hello следующим шагом является результат представления группы безопасности hello tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="ffb86-123">hello next step is tooretrieve hello security group view result.</span></span>

```powershell
$secgroup = Get-AzureRmNetworkWatcherSecurityGroupView -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id
```

## <a name="viewing-hello-results"></a><span data-ttu-id="ffb86-124">Просмотр результатов hello</span><span class="sxs-lookup"><span data-stu-id="ffb86-124">Viewing hello results</span></span>

<span data-ttu-id="ffb86-125">Hello следующий пример — сокращенный ответа возвращаемых результатов hello.</span><span class="sxs-lookup"><span data-stu-id="ffb86-125">hello following example is a shortened response of hello results returned.</span></span> <span data-ttu-id="ffb86-126">Hello результаты показывают все правила безопасности эффективный и примененные hello на виртуальной машине hello разбит на группы **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, и  **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="ffb86-126">hello results show all hello effective and applied security rules on hello virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

```
NetworkInterfaces : [
                      {
                        "NetworkInterfaceSecurityRules": [
                          {
                            "Name": "default-allow-rdp",
                            "Etag": "W/\"d4c411d4-0d62-49dc-8092-3d4b57825740\"",
                            "Id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg2/providers/Microsoft.Network/networkSecurityGroups/testvm2-nsg/securityRules/default-allow-rdp",
                            "Protocol": "TCP",
                            "SourcePortRange": "*",
                            "DestinationPortRange": "3389",
                            "SourceAddressPrefix": "*",
                            "DestinationAddressPrefix": "*",
                            "Access": "Allow",
                            "Priority": 1000,
                            "Direction": "Inbound",
                            "ProvisioningState": "Succeeded"
                          }
                          ...
                        ],
                        "DefaultSecurityRules": [
                          {
                            "Name": "AllowVnetInBound",
                            "Id": "/subscriptions00000000-0000-0000-0000-000000000000/resourceGroups/testrg2/providers/Microsoft.Network/networkSecurityGroups/testvm2-nsg/defaultSecurityRules/",
                            "Description": "Allow inbound traffic from all VMs in VNET",
                            "Protocol": "*",
                            "SourcePortRange": "*",
                            "DestinationPortRange": "*",
                            "SourceAddressPrefix": "VirtualNetwork",
                            "DestinationAddressPrefix": "VirtualNetwork",
                            "Access": "Allow",
                            "Priority": 65000,
                            "Direction": "Inbound",
                            "ProvisioningState": "Succeeded"
                          }
                          ...
                        ],
                        "EffectiveSecurityRules": [
                          {
                            "Name": "DefaultOutboundDenyAll",
                            "Protocol": "All",
                            "SourcePortRange": "0-65535",
                            "DestinationPortRange": "0-65535",
                            "SourceAddressPrefix": "*",
                            "DestinationAddressPrefix": "*",
                            "ExpandedSourceAddressPrefix": [],
                            "ExpandedDestinationAddressPrefix": [],
                            "Access": "Deny",
                            "Priority": 65500,
                            "Direction": "Outbound"
                          },
                          ...
                        ]
                      }
                    ]
```

## <a name="next-steps"></a><span data-ttu-id="ffb86-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ffb86-127">Next steps</span></span>

<span data-ttu-id="ffb86-128">Посетите [аудита безопасности сети группы (NSG) с Наблюдатель сети](network-watcher-nsg-auditing-powershell.md) toolearn способ проверки tooautomate групп безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="ffb86-128">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) toolearn how tooautomate validation of Network Security Groups.</span></span>


