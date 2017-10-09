---
title: "aaaAutomate NSG аудита и представление \"Группа безопасности Наблюдатель сети Azure\" | Документы Microsoft"
description: "Эта страница содержит инструкции о том, как аудит tooconfigure группы безопасности сети"
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
ms.openlocfilehash: 24fc418c433fceaf55a74b7c3b0e354dc46c8729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="automate-nsg-auditing-with-azure-network-watcher-security-group-view"></a><span data-ttu-id="2deaf-103">Автоматизация аудита группы безопасности сети с помощью представления группы безопасности в Наблюдателе за сетями Azure</span><span class="sxs-lookup"><span data-stu-id="2deaf-103">Automate NSG auditing with Azure Network Watcher Security group view</span></span>

<span data-ttu-id="2deaf-104">Пользователи часто сталкиваются с проблемой hello проверки уровня безопасности hello своей инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="2deaf-104">Customers are often faced with hello challenge of verifying hello security posture of their infrastructure.</span></span> <span data-ttu-id="2deaf-105">Это же характерно и для виртуальных машин в Azure.</span><span class="sxs-lookup"><span data-stu-id="2deaf-105">This challenge is no different for their VMs in Azure.</span></span> <span data-ttu-id="2deaf-106">Это важные toohave как профиль безопасности на основе hello группы безопасности сети (NSG) правил применения.</span><span class="sxs-lookup"><span data-stu-id="2deaf-106">It is important toohave a similar security profile based on hello Network Security Group (NSG) rules applied.</span></span> <span data-ttu-id="2deaf-107">Используя представление "Группа безопасности" hello, теперь вы можете получить список правил, применяемых tooa ВМ в NSG hello.</span><span class="sxs-lookup"><span data-stu-id="2deaf-107">Using hello Security Group View, you can now get hello list of rules applied tooa VM within an NSG.</span></span> <span data-ttu-id="2deaf-108">Можно определить профиль безопасности золотой NSG и инициировать представление группы безопасности в еженедельно ритме и сравнить профиль toohello золотой вывода hello и создать отчет.</span><span class="sxs-lookup"><span data-stu-id="2deaf-108">You can define a golden NSG security profile and initiate Security Group View on a weekly cadence and compare hello output toohello golden profile and create a report.</span></span> <span data-ttu-id="2deaf-109">Таким образом можно определить с легкостью все виртуальные машины hello, которые не соответствуют toohello предписанные профиля безопасности.</span><span class="sxs-lookup"><span data-stu-id="2deaf-109">This way you can identify with ease all hello VMs that do not conform toohello prescribed security profile.</span></span>

<span data-ttu-id="2deaf-110">Подробную информацию о группах безопасности сети см. в статье [Управление потоком сетевого трафика с помощью групп безопасности сети](../virtual-network/virtual-networks-nsg.md)</span><span class="sxs-lookup"><span data-stu-id="2deaf-110">If you are unfamiliar with Network Security Groups, visit [Network Security Overview](../virtual-network/virtual-networks-nsg.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2deaf-111">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="2deaf-111">Before you begin</span></span>

<span data-ttu-id="2deaf-112">В этом случае сравнение группу безопасности toohello известного хорошую основу просматривать результаты, возвращаемые для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="2deaf-112">In this scenario, you compare a known good baseline toohello security group view results returned for a virtual machine.</span></span>

<span data-ttu-id="2deaf-113">Этот сценарий предполагает уже были выполнены шаги hello в [создать Наблюдатель сети](network-watcher-create.md) toocreate Наблюдатель сети.</span><span class="sxs-lookup"><span data-stu-id="2deaf-113">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="2deaf-114">сценарий Hello также предполагается, что группа ресурсов с действительной виртуальной машиной существует toobe используется.</span><span class="sxs-lookup"><span data-stu-id="2deaf-114">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="2deaf-115">Сценарий</span><span class="sxs-lookup"><span data-stu-id="2deaf-115">Scenario</span></span>

<span data-ttu-id="2deaf-116">Hello сценарий, описанный в этой статье возвращает hello представление группы безопасности для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="2deaf-116">hello scenario covered in this article gets hello security group view for a virtual machine.</span></span>

<span data-ttu-id="2deaf-117">Вам предстоит:</span><span class="sxs-lookup"><span data-stu-id="2deaf-117">In this scenario, you will:</span></span>

- <span data-ttu-id="2deaf-118">получить набор известных проверенных правил;</span><span class="sxs-lookup"><span data-stu-id="2deaf-118">Retrieve a known good rule set</span></span>
- <span data-ttu-id="2deaf-119">получить виртуальную машину с помощью REST API;</span><span class="sxs-lookup"><span data-stu-id="2deaf-119">Retrieve a virtual machine with Rest API</span></span>
- <span data-ttu-id="2deaf-120">получить представление группы безопасности для виртуальной машины;</span><span class="sxs-lookup"><span data-stu-id="2deaf-120">Get security group view for virtual machine</span></span>
- <span data-ttu-id="2deaf-121">оценить ответ.</span><span class="sxs-lookup"><span data-stu-id="2deaf-121">Evaluate Response</span></span>

## <a name="retrieve-rule-set"></a><span data-ttu-id="2deaf-122">Получение набора правил</span><span class="sxs-lookup"><span data-stu-id="2deaf-122">Retrieve rule set</span></span>

<span data-ttu-id="2deaf-123">Первым шагом Hello в этом примере является toowork с существующего шаблона.</span><span class="sxs-lookup"><span data-stu-id="2deaf-123">hello first step in this example is toowork with an existing baseline.</span></span> <span data-ttu-id="2deaf-124">Hello следующий пример — некоторые json, извлеченных из существующей группы безопасности сети с помощью hello `Get-AzureRmNetworkSecurityGroup` командлет, который используется в качестве базовой hello в этом примере.</span><span class="sxs-lookup"><span data-stu-id="2deaf-124">hello following example is some json extracted from an existing Network Security Group using hello `Get-AzureRmNetworkSecurityGroup` cmdlet that is used as hello baseline for this example.</span></span>

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

## <a name="convert-rule-set-toopowershell-objects"></a><span data-ttu-id="2deaf-125">Преобразование объектов tooPowerShell набора правил</span><span class="sxs-lookup"><span data-stu-id="2deaf-125">Convert rule set tooPowerShell objects</span></span>

<span data-ttu-id="2deaf-126">На этом шаге мы читаете json-файл, который был создан ранее с правилами hello, ожидаемый toobe на hello сетевой группы безопасности для этого примера.</span><span class="sxs-lookup"><span data-stu-id="2deaf-126">In this step, we are reading a json file that was created earlier with hello rules that are expected toobe on hello Network Security Group for this example.</span></span>

```powershell
$nsgbaserules = Get-Content -Path C:\temp\testvm1-nsg.json | ConvertFrom-Json
```

## <a name="retrieve-network-watcher"></a><span data-ttu-id="2deaf-127">Извлечение Наблюдателя за сетями</span><span class="sxs-lookup"><span data-stu-id="2deaf-127">Retrieve Network Watcher</span></span>

<span data-ttu-id="2deaf-128">Hello следующим шагом является экземпляр Наблюдатель сети tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="2deaf-128">hello next step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="2deaf-129">Hello `$networkWatcher` переменной передается toohello `AzureRmNetworkWatcherSecurityGroupView` командлета.</span><span class="sxs-lookup"><span data-stu-id="2deaf-129">hello `$networkWatcher` variable is passed toohello `AzureRmNetworkWatcherSecurityGroupView` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a><span data-ttu-id="2deaf-130">Получение виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="2deaf-130">Get a VM</span></span>

<span data-ttu-id="2deaf-131">Виртуальная машина — hello необходимые toorun `Get-AzureRmNetworkWatcherSecurityGroupView` командлета для.</span><span class="sxs-lookup"><span data-stu-id="2deaf-131">A virtual machine is required toorun hello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet against.</span></span> <span data-ttu-id="2deaf-132">Следующий пример Hello получает объект виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="2deaf-132">hello following example gets a VM object.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="2deaf-133">Получение представления группы безопасности</span><span class="sxs-lookup"><span data-stu-id="2deaf-133">Retrieve security group view</span></span>

<span data-ttu-id="2deaf-134">Hello следующим шагом является результат представления группы безопасности hello tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="2deaf-134">hello next step is tooretrieve hello security group view result.</span></span> <span data-ttu-id="2deaf-135">Этот результат является json сравниваемых toohello «базовые показатели», показанном выше.</span><span class="sxs-lookup"><span data-stu-id="2deaf-135">This result is compared toohello "baseline" json that was shown earlier.</span></span>

```powershell
$secgroup = Get-AzureRmNetworkWatcherSecurityGroupView -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id
```

## <a name="analyzing-hello-results"></a><span data-ttu-id="2deaf-136">Анализ результатов hello</span><span class="sxs-lookup"><span data-stu-id="2deaf-136">Analyzing hello results</span></span>

<span data-ttu-id="2deaf-137">ответ Hello группируются по сетевых интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="2deaf-137">hello response is grouped by Network interfaces.</span></span> <span data-ttu-id="2deaf-138">различные типы возвращаемых правил Hello, вступают в силу и по умолчанию правила безопасности.</span><span class="sxs-lookup"><span data-stu-id="2deaf-138">hello different types of rules returned are effective and default security rules.</span></span> <span data-ttu-id="2deaf-139">результат Hello дальнейшей разбивкой на способы применения, либо в подсети или виртуальный сетевой адаптер.</span><span class="sxs-lookup"><span data-stu-id="2deaf-139">hello result is further broken down by how it is applied, either on a subnet or a virtual NIC.</span></span>

<span data-ttu-id="2deaf-140">Hello следующий сценарий PowerShell сравнивает результаты hello hello представление группы безопасности tooan существующие выходные данные NSG.</span><span class="sxs-lookup"><span data-stu-id="2deaf-140">hello following PowerShell script compares hello results of hello Security Group View tooan existing output of an NSG.</span></span> <span data-ttu-id="2deaf-141">Hello ниже приведен простой пример сравнение результатов hello с `Compare-Object` командлета.</span><span class="sxs-lookup"><span data-stu-id="2deaf-141">hello following example is a simple example of how hello results can be compared with `Compare-Object` cmdlet.</span></span>

```powershell
Compare-Object -ReferenceObject $nsgbaserules `
-DifferenceObject $secgroup.NetworkInterfaces[0].NetworkInterfaceSecurityRules `
-Property Name,Description,Protocol,SourcePortRange,DestinationPortRange,SourceAddressPrefix,DestinationAddressPrefix,Access,Priority,Direction
```

<span data-ttu-id="2deaf-142">Следующий пример Hello является результатом hello.</span><span class="sxs-lookup"><span data-stu-id="2deaf-142">hello following example is hello result.</span></span> <span data-ttu-id="2deaf-143">Вы увидите два hello правил, которые были в hello первый набор правил, которые не hello сравнения.</span><span class="sxs-lookup"><span data-stu-id="2deaf-143">You can see two of hello rules that were in hello first rule set were not present in hello comparison.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="2deaf-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2deaf-144">Next steps</span></span>

<span data-ttu-id="2deaf-145">Если параметры были изменены, см. раздел [Управление группами безопасности сети](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack вниз hello правила сетевой безопасности группы и безопасности, в вопросе.</span><span class="sxs-lookup"><span data-stu-id="2deaf-145">If settings have been changed, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are in question.</span></span>













