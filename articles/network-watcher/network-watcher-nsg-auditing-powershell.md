---
title: "Наблюдатель за сетями Azure: автоматизация аудита NSG с помощью представления группы безопасности службы | Документация Майкрософт"
description: "На этой странице представлены инструкции по настройке аудита группы безопасности сети"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 78a01bcf-74fe-402a-9812-285f3501f877
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: a91da330e677c85f16f6f4e506613576b6507d7c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="automate-nsg-auditing-with-azure-network-watcher-security-group-view"></a><span data-ttu-id="54be3-103">Автоматизация аудита группы безопасности сети с помощью представления группы безопасности в Наблюдателе за сетями Azure</span><span class="sxs-lookup"><span data-stu-id="54be3-103">Automate NSG auditing with Azure Network Watcher Security group view</span></span>

<span data-ttu-id="54be3-104">Клиенты часто сталкиваются с проблемами при проверке показателей системы безопасности своей инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="54be3-104">Customers are often faced with the challenge of verifying the security posture of their infrastructure.</span></span> <span data-ttu-id="54be3-105">Это же характерно и для виртуальных машин в Azure.</span><span class="sxs-lookup"><span data-stu-id="54be3-105">This challenge is no different for their VMs in Azure.</span></span> <span data-ttu-id="54be3-106">Очень важно иметь одинаковый профиль безопасности, основанный на применении правил группы безопасности сети (NSG).</span><span class="sxs-lookup"><span data-stu-id="54be3-106">It is important to have a similar security profile based on the Network Security Group (NSG) rules applied.</span></span> <span data-ttu-id="54be3-107">Теперь с помощью представления группы безопасности можно получить список правил, применяемых к виртуальной машине в NSG.</span><span class="sxs-lookup"><span data-stu-id="54be3-107">Using the Security Group View, you can now get the list of rules applied to a VM within an NSG.</span></span> <span data-ttu-id="54be3-108">Вы можете определить золотой профиль безопасности NSG и инициировать представление группы безопасности с еженедельной периодичностью, а также сравнивать выходные данные в золотом профиле и составлять отчет.</span><span class="sxs-lookup"><span data-stu-id="54be3-108">You can define a golden NSG security profile and initiate Security Group View on a weekly cadence and compare the output to the golden profile and create a report.</span></span> <span data-ttu-id="54be3-109">Таким образом вы сможете с легкостью определить все виртуальные машины, которые не соответствуют предписанному профилю безопасности.</span><span class="sxs-lookup"><span data-stu-id="54be3-109">This way you can identify with ease all the VMs that do not conform to the prescribed security profile.</span></span>

<span data-ttu-id="54be3-110">Подробную информацию о группах безопасности сети см. в статье [Управление потоком сетевого трафика с помощью групп безопасности сети](../virtual-network/virtual-networks-nsg.md)</span><span class="sxs-lookup"><span data-stu-id="54be3-110">If you are unfamiliar with Network Security Groups, visit [Network Security Overview](../virtual-network/virtual-networks-nsg.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="54be3-111">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="54be3-111">Before you begin</span></span>

<span data-ttu-id="54be3-112">В нашем примере вам предлагается сравнить известные базовые показатели и результаты в представлении группы безопасности, возвращаемые для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="54be3-112">In this scenario, you compare a known good baseline to the security group view results returned for a virtual machine.</span></span>

<span data-ttu-id="54be3-113">В этом сценарии предполагается, что вы создали Наблюдатель за сетями в соответствии с инструкциями в статье [Create an Azure Network Watcher instance](network-watcher-create.md) (Наблюдатель за сетями: создание экземпляра службы).</span><span class="sxs-lookup"><span data-stu-id="54be3-113">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="54be3-114">Предполагается также, что у вас есть группа ресурсов с допустимой виртуальной машиной.</span><span class="sxs-lookup"><span data-stu-id="54be3-114">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="54be3-115">Сценарий</span><span class="sxs-lookup"><span data-stu-id="54be3-115">Scenario</span></span>

<span data-ttu-id="54be3-116">В рамках сценария, описанного в этой статье, вы получаете представление группы безопасности для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="54be3-116">The scenario covered in this article gets the security group view for a virtual machine.</span></span>

<span data-ttu-id="54be3-117">Вам предстоит:</span><span class="sxs-lookup"><span data-stu-id="54be3-117">In this scenario, you will:</span></span>

- <span data-ttu-id="54be3-118">получить набор известных проверенных правил;</span><span class="sxs-lookup"><span data-stu-id="54be3-118">Retrieve a known good rule set</span></span>
- <span data-ttu-id="54be3-119">получить виртуальную машину с помощью REST API;</span><span class="sxs-lookup"><span data-stu-id="54be3-119">Retrieve a virtual machine with Rest API</span></span>
- <span data-ttu-id="54be3-120">получить представление группы безопасности для виртуальной машины;</span><span class="sxs-lookup"><span data-stu-id="54be3-120">Get security group view for virtual machine</span></span>
- <span data-ttu-id="54be3-121">оценить ответ.</span><span class="sxs-lookup"><span data-stu-id="54be3-121">Evaluate Response</span></span>

## <a name="retrieve-rule-set"></a><span data-ttu-id="54be3-122">Получение набора правил</span><span class="sxs-lookup"><span data-stu-id="54be3-122">Retrieve rule set</span></span>

<span data-ttu-id="54be3-123">Первый шаг в этом примере — это работа с существующими базовыми показателями.</span><span class="sxs-lookup"><span data-stu-id="54be3-123">The first step in this example is to work with an existing baseline.</span></span> <span data-ttu-id="54be3-124">В следующем примере показан объект JSON, извлеченный из существующей группы безопасности сети с помощью командлета `Get-AzureRmNetworkSecurityGroup`. Он представляет базовые показатели.</span><span class="sxs-lookup"><span data-stu-id="54be3-124">The following example is some json extracted from an existing Network Security Group using the `Get-AzureRmNetworkSecurityGroup` cmdlet that is used as the baseline for this example.</span></span>

```json
[
    {
        "Description":  null,
        "Protocol":  "TCP",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "3389",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Allow",
        "Priority":  1000,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "default-allow-rdp",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/default-allow-rdp"
    },
    {
        "Description":  null,
        "Protocol":  "*",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "111",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Allow",
        "Priority":  1010,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "MyRuleDoNotDelete",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/MyRuleDoNotDelete"
    },
    {
        "Description":  null,
        "Protocol":  "*",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "112",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Allow",
        "Priority":  1020,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "My2ndRuleDoNotDelete",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/My2ndRuleDoNotDelete"
    },
    {
        "Description":  null,
        "Protocol":  "TCP",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "5672",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Deny",
        "Priority":  1030,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "ThisRuleNeedsToStay",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/ThisRuleNeedsToStay"
    }
]
```

## <a name="convert-rule-set-to-powershell-objects"></a><span data-ttu-id="54be3-125">Преобразование набора правил в объекты PowerShell</span><span class="sxs-lookup"><span data-stu-id="54be3-125">Convert rule set to PowerShell objects</span></span>

<span data-ttu-id="54be3-126">На этом шаге необходимо прочитать файл JSON, который создан ранее с помощью правил, которые должны быть включены в группу безопасности сети для этого примера.</span><span class="sxs-lookup"><span data-stu-id="54be3-126">In this step, we are reading a json file that was created earlier with the rules that are expected to be on the Network Security Group for this example.</span></span>

```powershell
$nsgbaserules = Get-Content -Path C:\temp\testvm1-nsg.json | ConvertFrom-Json
```

## <a name="retrieve-network-watcher"></a><span data-ttu-id="54be3-127">Извлечение Наблюдателя за сетями</span><span class="sxs-lookup"><span data-stu-id="54be3-127">Retrieve Network Watcher</span></span>

<span data-ttu-id="54be3-128">Далее необходимо получить экземпляр Наблюдателя за сетями.</span><span class="sxs-lookup"><span data-stu-id="54be3-128">The next step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="54be3-129">Переменная `$networkWatcher` передается в командлет `AzureRmNetworkWatcherSecurityGroupView`.</span><span class="sxs-lookup"><span data-stu-id="54be3-129">The `$networkWatcher` variable is passed to the `AzureRmNetworkWatcherSecurityGroupView` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a><span data-ttu-id="54be3-130">Получение виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="54be3-130">Get a VM</span></span>

<span data-ttu-id="54be3-131">Для повторного выполнения командлета `Get-AzureRmNetworkWatcherSecurityGroupView` необходима виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="54be3-131">A virtual machine is required to run the `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet against.</span></span> <span data-ttu-id="54be3-132">Ниже приведен пример получения объекта виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="54be3-132">The following example gets a VM object.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="54be3-133">Получение представления группы безопасности</span><span class="sxs-lookup"><span data-stu-id="54be3-133">Retrieve security group view</span></span>

<span data-ttu-id="54be3-134">Далее необходимо получить результат представления группы безопасности.</span><span class="sxs-lookup"><span data-stu-id="54be3-134">The next step is to retrieve the security group view result.</span></span> <span data-ttu-id="54be3-135">Этот результат сравнивается с "базовым" объектом JSON (см. выше).</span><span class="sxs-lookup"><span data-stu-id="54be3-135">This result is compared to the "baseline" json that was shown earlier.</span></span>

```powershell
$secgroup = Get-AzureRmNetworkWatcherSecurityGroupView -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id
```

## <a name="analyzing-the-results"></a><span data-ttu-id="54be3-136">Анализ результатов</span><span class="sxs-lookup"><span data-stu-id="54be3-136">Analyzing the results</span></span>

<span data-ttu-id="54be3-137">Ответ группируется по сетевым интерфейсам.</span><span class="sxs-lookup"><span data-stu-id="54be3-137">The response is grouped by Network interfaces.</span></span> <span data-ttu-id="54be3-138">Разные типы возвращаемых правил, являются действительными правилами безопасности по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="54be3-138">The different types of rules returned are effective and default security rules.</span></span> <span data-ttu-id="54be3-139">Далее результат разбивается на основе особенностей применения: в подсети или на виртуальной сетевой карте.</span><span class="sxs-lookup"><span data-stu-id="54be3-139">The result is further broken down by how it is applied, either on a subnet or a virtual NIC.</span></span>

<span data-ttu-id="54be3-140">Следующий сценарий PowerShell сравнивает результаты представления группы безопасности с существующими выходными данными группы NSG.</span><span class="sxs-lookup"><span data-stu-id="54be3-140">The following PowerShell script compares the results of the Security Group View to an existing output of an NSG.</span></span> <span data-ttu-id="54be3-141">Ниже приведен простой пример того, как можно сравнить результаты с помощью командлета `Compare-Object`.</span><span class="sxs-lookup"><span data-stu-id="54be3-141">The following example is a simple example of how the results can be compared with `Compare-Object` cmdlet.</span></span>

```powershell
Compare-Object -ReferenceObject $nsgbaserules `
-DifferenceObject $secgroup.NetworkInterfaces[0].NetworkInterfaceSecurityRules `
-Property Name,Description,Protocol,SourcePortRange,DestinationPortRange,SourceAddressPrefix,DestinationAddressPrefix,Access,Priority,Direction
```

<span data-ttu-id="54be3-142">Пример ниже является результатом.</span><span class="sxs-lookup"><span data-stu-id="54be3-142">The following example is the result.</span></span> <span data-ttu-id="54be3-143">Вы можете увидеть, что два правила, заданные в первом наборе правил не присутствовали в сравнении.</span><span class="sxs-lookup"><span data-stu-id="54be3-143">You can see two of the rules that were in the first rule set were not present in the comparison.</span></span>

```
Name                     : My2ndRuleDoNotDelete
Description              : 
Protocol                 : *
SourcePortRange          : *
DestinationPortRange     : 112
SourceAddressPrefix      : *
DestinationAddressPrefix : *
Access                   : Allow
Priority                 : 1020
Direction                : Inbound
SideIndicator            : <=

Name                     : ThisRuleNeedsToStay
Description              : 
Protocol                 : TCP
SourcePortRange          : *
DestinationPortRange     : 5672
SourceAddressPrefix      : *
DestinationAddressPrefix : *
Access                   : Deny
Priority                 : 1030
Direction                : Inbound
SideIndicator            : <=
```

## <a name="next-steps"></a><span data-ttu-id="54be3-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="54be3-144">Next steps</span></span>

<span data-ttu-id="54be3-145">Если параметры изменены, см. статью об [управлении группами безопасности сети с помощью портала](../virtual-network/virtual-network-manage-nsg-arm-portal.md). В ней содержатся сведения об отслеживании группы безопасности сети и нужных правил безопасности.</span><span class="sxs-lookup"><span data-stu-id="54be3-145">If settings have been changed, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that are in question.</span></span>













