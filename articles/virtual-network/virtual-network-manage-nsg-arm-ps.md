---
title: "Управление группами безопасности сети с помощью Azure PowerShell | Документация Майкрософт"
description: "Узнайте, как управлять группами безопасности сети с помощью PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3706ce6c-d9ae-46cb-a048-f0a4e84dc5cc
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/14/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ca7f4926ca4edf9d20612aca74f6ae5f0ed847b3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="manage-network-security-groups-using-powershell"></a><span data-ttu-id="02f31-103">Управление группами безопасности сети с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="02f31-103">Manage network security groups using PowerShell</span></span>

[!INCLUDE [virtual-network-manage-arm-selectors-include.md](../../includes/virtual-network-manage-nsg-arm-selectors-include.md)]

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="02f31-104">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="02f31-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="02f31-105">В этой статье описывается использование модели развертывания c помощью Resource Manager. Для большинства новых развертываний мы рекомендуем использовать эту модель вместо классической.</span><span class="sxs-lookup"><span data-stu-id="02f31-105">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span></span>
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="02f31-106">Извлечение информации</span><span class="sxs-lookup"><span data-stu-id="02f31-106">Retrieve Information</span></span>
<span data-ttu-id="02f31-107">Вы можете просмотреть существующие группы безопасности сети, получить правила для существующей группы и узнать, с какими ресурсами она связана.</span><span class="sxs-lookup"><span data-stu-id="02f31-107">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="02f31-108">Просмотр существующих групп безопасности сети</span><span class="sxs-lookup"><span data-stu-id="02f31-108">View existing NSGs</span></span>
<span data-ttu-id="02f31-109">Чтобы просмотреть все существующие группы безопасности сети в подписке, выполните командлет `Get-AzureRmNetworkSecurityGroup`.</span><span class="sxs-lookup"><span data-stu-id="02f31-109">To view all existing NSGs in a subscription, run the `Get-AzureRmNetworkSecurityGroup` cmdlet.</span></span>

<span data-ttu-id="02f31-110">Ожидаемый результат:</span><span class="sxs-lookup"><span data-stu-id="02f31-110">Expected result:</span></span>

    Name                 : NSG-BackEnd
    ResourceGroupName    : RG-NSG
    Location             : westus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-BackEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 :                            
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : NSG-FrontEnd
    ResourceGroupName    : RG-NSG
    Location             : eastus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/NRP-RG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : WEB1
    ResourceGroupName    : RG101
    Location             : eastus2
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG101/providers/M
                           icrosoft.Network/networkSecurityGroups/WEB1
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]


<span data-ttu-id="02f31-111">Чтобы просмотреть список групп безопасности сети в определенной группе ресурсов, выполните командлет `Get-AzureRmNetworkSecurityGroup`.</span><span class="sxs-lookup"><span data-stu-id="02f31-111">To view the list of NSGs in a specific resource group, run the `Get-AzureRmNetworkSecurityGroup` cmdlet.</span></span>

<span data-ttu-id="02f31-112">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="02f31-112">Expected output:</span></span>

    Name                 : NSG-BackEnd
    ResourceGroupName    : RG-NSG
    Location             : westus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-BackEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 :                            
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : NSG-FrontEnd
    ResourceGroupName    : RG-NSG
    Location             : eastus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/NRP-RG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="02f31-113">Перечисление всех правил для группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="02f31-113">List all rules for an NSG</span></span>
<span data-ttu-id="02f31-114">Чтобы просмотреть правила группы безопасности сети с именем **NSG-FrontEnd**, введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="02f31-114">To view the rules of an NSG named **NSG-FrontEnd**, enter the following command:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd | Select SecurityRules -ExpandProperty SecurityRules
```

<span data-ttu-id="02f31-115">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="02f31-115">Expected output:</span></span>

    Name                     : rdp-rule
    Id                       : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp-rule
    Etag                     : W/"[Id]"
    ProvisioningState        : Succeeded
    Description              : Allow RDP
    Protocol                 : Tcp
    SourcePortRange          : *
    DestinationPortRange     : 3389
    SourceAddressPrefix      : Internet
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 100
    Direction                : Inbound

    Name                     : web-rule
    Id                       : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule
    Etag                     : W/"[Id]"
    ProvisioningState        : Succeeded
    Description              : Allow HTTP
    Protocol                 : Tcp
    SourcePortRange          : *
    DestinationPortRange     : 80
    SourceAddressPrefix      : Internet
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 101
    Direction                : Inbound

> [!NOTE]
> <span data-ttu-id="02f31-116">Можно также использовать `Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name "NSG-FrontEnd" | Select DefaultSecurityRules -ExpandProperty DefaultSecurityRules` для получения списка правил по умолчанию из группы безопасности сети **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="02f31-116">You can also use `Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name "NSG-FrontEnd" | Select DefaultSecurityRules -ExpandProperty DefaultSecurityRules` to list the default rules from the **NSG-FrontEnd** NSG.</span></span>
> 

### <a name="view-nsgs-associations"></a><span data-ttu-id="02f31-117">Просмотр связей для группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="02f31-117">View NSGs associations</span></span>
<span data-ttu-id="02f31-118">Чтобы просмотреть, к каким ресурсам привязана группа безопасности сети **NSG-FrontEnd**, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="02f31-118">To view what resources the **NSG-FrontEnd** NSG is associate with, run the following command:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
```

<span data-ttu-id="02f31-119">Найдите свойства **NetworkInterfaces** и **Subnets**, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="02f31-119">Look for the **NetworkInterfaces** and **Subnets** properties as shown below:</span></span>

    NetworkInterfaces    : []
    Subnets              : [
                             {
                               "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                               "IpConfigurations": []
                             }
                           ]

<span data-ttu-id="02f31-120">В предыдущем примере группа безопасности сети не привязана к сетевым интерфейсам, но связана с подсетью **FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="02f31-120">In the previous example, the NSG is not associated to any network interfaces (NICs); it is associated to a subnet named **FrontEnd**.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="02f31-121">Управление правилами</span><span class="sxs-lookup"><span data-stu-id="02f31-121">Manage rules</span></span>
<span data-ttu-id="02f31-122">Можно добавлять правила для существующей группы безопасности сети, изменять существующие правила и удалять их.</span><span class="sxs-lookup"><span data-stu-id="02f31-122">You can add rules to an existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="02f31-123">Добавление правила</span><span class="sxs-lookup"><span data-stu-id="02f31-123">Add a rule</span></span>
<span data-ttu-id="02f31-124">Чтобы добавить правило, разрешающее **входящий** трафик через порт **443** с любого компьютера в группу безопасности сети **NSG-FrontEnd**, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="02f31-124">To add a rule allowing **inbound** traffic to port **443** from any machine to the **NSG-FrontEnd** NSG, complete the following steps:</span></span>

1. <span data-ttu-id="02f31-125">Чтобы получить существующую группу безопасности сети и сохранить ее в переменной, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="02f31-125">Run the following command to retrieve the existing NSG and store it in a variable:</span></span>

    ```powershell   
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="02f31-126">Чтобы добавить правило к группе безопасности сети, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="02f31-126">Run the following command to add a rule to the NSG:</span></span>

    ```powershell
    Add-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg `
    -Name https-rule `
    -Description "Allow HTTPS" `
    -Access Allow `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 102 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443
    ```

3. <span data-ttu-id="02f31-127">Чтобы сохранить изменения в группе безопасности сети, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="02f31-127">To save the changes made to the NSG, run the following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```
    <span data-ttu-id="02f31-128">Ожидаемый результат, показаны только правила безопасности:</span><span class="sxs-lookup"><span data-stu-id="02f31-128">Expected output showing only the security rules:</span></span>
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 },
                                 {
                                   "Name": "https-rule",
                                   "Etag": "W/\"[Id]\"",
                                   "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/https-rule",
                                   "Description": "Allow HTTPS",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "443",
                                   "SourceAddressPrefix": "*",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 102,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]

### <a name="change-a-rule"></a><span data-ttu-id="02f31-129">Изменение правила</span><span class="sxs-lookup"><span data-stu-id="02f31-129">Change a rule</span></span>
<span data-ttu-id="02f31-130">Чтобы изменить ранее созданное правило, разрешающее входящий трафик только из **Интернета** , выполните шаги ниже.</span><span class="sxs-lookup"><span data-stu-id="02f31-130">To change the rule created above to allow inbound traffic from the **Internet** only, follow the steps below.</span></span>

1. <span data-ttu-id="02f31-131">Чтобы получить существующую группу безопасности сети и сохранить ее в переменной, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="02f31-131">Run the following command to retrieve the existing NSG and store it in a variable:</span></span>

    ```powershell 
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="02f31-132">Выполните следующую команду с новыми параметрами правила:</span><span class="sxs-lookup"><span data-stu-id="02f31-132">Run the following command with the new rule settings:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg `
    -Name https-rule `
    -Description "Allow HTTPS" `
    -Access Allow `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 102 `
    -SourceAddressPrefix Internet `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443
    ```

3. <span data-ttu-id="02f31-133">Чтобы сохранить изменения в группе безопасности сети, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="02f31-133">To save the changes made to the NSG, run the following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="02f31-134">Ожидаемый результат, показаны только правила безопасности:</span><span class="sxs-lookup"><span data-stu-id="02f31-134">Expected output showing only the security rules:</span></span>
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 },
                                 {
                                   "Name": "https-rule",
                                   "Etag": "W/\"[Id]\"",
                                   "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/https-rule",
                                   "Description": "Allow HTTPS",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "443",
                                   "SourceAddressPrefix": "Internet",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 102,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]

### <a name="delete-a-rule"></a><span data-ttu-id="02f31-135">Удаление правила</span><span class="sxs-lookup"><span data-stu-id="02f31-135">Delete a rule</span></span>
1. <span data-ttu-id="02f31-136">Чтобы получить существующую группу безопасности сети и сохранить ее в переменной, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="02f31-136">Run the following command to retrieve the existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="02f31-137">Чтобы удалить правило из группы безопасности сети, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="02f31-137">Run the following command to remove the rule from the NSG:</span></span>

    ```powershell
    Remove-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg -Name https-rule
    ```

3. <span data-ttu-id="02f31-138">Чтобы сохранить изменения в группе безопасности сети, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="02f31-138">Save the changes made to the NSG, by running the following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="02f31-139">Ожидаемый результат, показаны только правила безопасности. Обратите внимание, что **https-rule** больше не отображается.</span><span class="sxs-lookup"><span data-stu-id="02f31-139">Expected output showing only the security rules, notice the **https-rule** is no longer listed:</span></span>
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 }
                               ]

## <a name="manage-associations"></a><span data-ttu-id="02f31-140">Управление связями</span><span class="sxs-lookup"><span data-stu-id="02f31-140">Manage associations</span></span>
<span data-ttu-id="02f31-141">Группу безопасности сети можно связать с сетевыми адаптерами и подсетями.</span><span class="sxs-lookup"><span data-stu-id="02f31-141">You can associate an NSG to subnets and NICs.</span></span> <span data-ttu-id="02f31-142">Можно также отменить связь группы безопасности сети с любым ресурсом.</span><span class="sxs-lookup"><span data-stu-id="02f31-142">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-to-a-nic"></a><span data-ttu-id="02f31-143">Связывание группы безопасности сети с сетевым адаптером</span><span class="sxs-lookup"><span data-stu-id="02f31-143">Associate an NSG to a NIC</span></span>
<span data-ttu-id="02f31-144">Чтобы привязать группу безопасности сети **NSG-FrontEnd** к сетевому интерфейсу **TestNICWeb1**, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="02f31-144">To associate the **NSG-FrontEnd** NSG to the **TestNICWeb1** NIC, complete the following steps:</span></span>

1. <span data-ttu-id="02f31-145">Чтобы получить существующую группу безопасности сети и сохранить ее в переменной, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="02f31-145">Run the following command to retrieve the existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="02f31-146">Чтобы получить сетевой интерфейс и сохранить его в переменной, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="02f31-146">Run the following command to retrieve the existing NIC and store it in a variable:</span></span>

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

3. <span data-ttu-id="02f31-147">Задайте для свойства **NetworkSecurityGroup** переменной **NIC** значение переменной **NSG** с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="02f31-147">Set the **NetworkSecurityGroup** property of the **NIC** variable to the value of the **NSG** variable, by entering the following command:</span></span>

    ```powershell
    $nic.NetworkSecurityGroup = $nsg
    ```

4. <span data-ttu-id="02f31-148">Чтобы сохранить изменения в сетевом интерфейсе, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="02f31-148">To save the changes made to the NIC, run the following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    <span data-ttu-id="02f31-149">Ожидаемый результат, показано только свойство **NetworkSecurityGroup** :</span><span class="sxs-lookup"><span data-stu-id="02f31-149">Expected output showing only the **NetworkSecurityGroup** property:</span></span>
   
        NetworkSecurityGroup : {
                                 "SecurityRules": [],
                                 "DefaultSecurityRules": [],
                                 "NetworkInterfaces": [],
                                 "Subnets": [],
                                 "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                               }

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="02f31-150">Отмена связи с сетевым адаптером для группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="02f31-150">Dissociate an NSG from a NIC</span></span>
<span data-ttu-id="02f31-151">Чтобы отменить связь группы безопасности сети **NSG-FrontEnd** с сетевым интерфейсом **TestNICWeb1**, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="02f31-151">To dissociate the **NSG-FrontEnd** NSG from the **TestNICWeb1** NIC, complete the following steps:</span></span>

1. <span data-ttu-id="02f31-152">Чтобы получить сетевой интерфейс и сохранить его в переменной, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="02f31-152">Run the following command to retrieve the existing NIC and store it in a variable:</span></span>

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

2. <span data-ttu-id="02f31-153">Задайте для свойства **NetworkSecurityGroup** переменной **NIC** значение **$null** с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="02f31-153">Set the **NetworkSecurityGroup** property of the **NIC** variable to **$null** by running the following command:</span></span>

    ```powershell
    $nic.NetworkSecurityGroup = $null
    ```

3. <span data-ttu-id="02f31-154">Чтобы сохранить изменения в сетевом интерфейсе, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="02f31-154">To save the changes made to the NIC, run the following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    <span data-ttu-id="02f31-155">Ожидаемый результат, показано только свойство **NetworkSecurityGroup** :</span><span class="sxs-lookup"><span data-stu-id="02f31-155">Expected output showing only the **NetworkSecurityGroup** property:</span></span>
   
        NetworkSecurityGroup : null

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="02f31-156">Отмена связи с подсетью для группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="02f31-156">Dissociate an NSG from a subnet</span></span>
<span data-ttu-id="02f31-157">Чтобы отменить связь группы безопасности сети **NSG-FrontEnd** с подсетью **FrontEnd**, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="02f31-157">To dissociate the **NSG-FrontEnd** NSG from the **FrontEnd** subnet, complete the following steps:</span></span>

1. <span data-ttu-id="02f31-158">Чтобы получить существующую виртуальную сеть и сохранить ее в переменной, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="02f31-158">Run the following command to retrieve the existing VNet and store it in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. <span data-ttu-id="02f31-159">Чтобы получить подсеть **FrontEnd** и сохранить ее в переменной, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="02f31-159">Run the following command to retrieve the **FrontEnd** subnet and store it in a variable:</span></span>

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. <span data-ttu-id="02f31-160">Задайте для свойства **NetworkSecurityGroup** переменной **subnet** значение **$null** с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="02f31-160">Set the **NetworkSecurityGroup** property of the **subnet** variable to **$null** by entering the following command:</span></span>

    ```powershell
    $subnet.NetworkSecurityGroup = $null
    ```

4. <span data-ttu-id="02f31-161">Чтобы сохранить изменения в подсети, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="02f31-161">To save the changes made to the subnet, run the following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="02f31-162">Ожидаемый результат, показаны только свойства подсети **FrontEnd** .</span><span class="sxs-lookup"><span data-stu-id="02f31-162">Expected output showing only the properties of the **FrontEnd** subnet.</span></span> <span data-ttu-id="02f31-163">Обратите внимание, что свойства **NetworkSecurityGroup**нет:</span><span class="sxs-lookup"><span data-stu-id="02f31-163">Notice there isn't a property for **NetworkSecurityGroup**:</span></span>
   
            ...
            Subnets           : [
                                  {
                                    "Name": "FrontEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24",
                                    "IpConfigurations": [
                                      {
                                        "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1"
                                      },
                                      {
                                        "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1"
                                      }
                                    ],
                                    "ProvisioningState": "Succeeded"
                                  },
                                    ...
                                ]

### <a name="associate-an-nsg-to-a-subnet"></a><span data-ttu-id="02f31-164">Связывание группы NSG с подсетью</span><span class="sxs-lookup"><span data-stu-id="02f31-164">Associate an NSG to a subnet</span></span>
<span data-ttu-id="02f31-165">Чтобы привязать группу безопасности сети **NSG-FrontEnd** к подсети **FronEnd** снова, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="02f31-165">To associate the **NSG-FrontEnd** NSG to the **FronEnd** subnet again, complete the following steps:</span></span>

1. <span data-ttu-id="02f31-166">Чтобы получить существующую виртуальную сеть и сохранить ее в переменной, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="02f31-166">Run the following command to retrieve the existing VNet and store it in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. <span data-ttu-id="02f31-167">Чтобы получить подсеть **FrontEnd** и сохранить ее в переменной, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="02f31-167">Run the following command to retrieve the **FrontEnd** subnet and store it in a variable:</span></span>

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. <span data-ttu-id="02f31-168">Чтобы получить существующую группу безопасности сети и сохранить ее в переменной, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="02f31-168">Run the following command to retrieve the existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

4. <span data-ttu-id="02f31-169">Чтобы задать для свойства **NetworkSecurityGroup** переменной **subnet** значение **$null**, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="02f31-169">Set the **NetworkSecurityGroup** property of the **subnet** variable to **$null** by running the following command:</span></span>

    ```powershell
    $subnet.NetworkSecurityGroup = $nsg
    ```

5. <span data-ttu-id="02f31-170">Чтобы сохранить изменения в подсети, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="02f31-170">To save the changes made to the subnet, run the following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="02f31-171">Ожидаемый результат, показано только свойство **NetworkSecurityGroup** для подсети **FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="02f31-171">Expected output showing only the **NetworkSecurityGroup** property of the **FrontEnd** subnet:</span></span>
   
        ...
        "NetworkSecurityGroup": {
                                  "SecurityRules": [],
                                  "DefaultSecurityRules": [],
                                  "NetworkInterfaces": [],
                                  "Subnets": [],
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                }
        ...

## <a name="delete-an-nsg"></a><span data-ttu-id="02f31-172">Удаление группы NSG</span><span class="sxs-lookup"><span data-stu-id="02f31-172">Delete an NSG</span></span>
<span data-ttu-id="02f31-173">Группу безопасности сети можно удалить только в том случае, если она не связана с ресурсами.</span><span class="sxs-lookup"><span data-stu-id="02f31-173">You can only delete an NSG if it's not associated to any resource.</span></span> <span data-ttu-id="02f31-174">Чтобы удалить группу безопасности сети, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="02f31-174">To delete an NSG, follow the steps below.</span></span>

1. <span data-ttu-id="02f31-175">Чтобы проверить ресурсы, связанные с группой, выполните команду `azure network nsg show` , как показано в разделе [Просмотр связей для группы безопасности сети](#View-NSGs-associations).</span><span class="sxs-lookup"><span data-stu-id="02f31-175">To check the resources associated to an NSG, run the `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span></span>
2. <span data-ttu-id="02f31-176">Если группа связана с сетевыми адаптерами, выполните `azure network nic set` , как показано в разделе [Отмена связи с сетевым адаптером для группы безопасности сети](#Dissociate-an-NSG-from-a-NIC) , для каждого сетевого адаптера.</span><span class="sxs-lookup"><span data-stu-id="02f31-176">If the NSG is associated to any NICs, run the `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span></span> 
3. <span data-ttu-id="02f31-177">Если группа связана с подсетью, выполните `azure network vnet subnet set` , как показано в разделе [Отмена связи с подсетью для группы безопасности сети](#Dissociate-an-NSG-from-a-subnet) , для каждой подсети.</span><span class="sxs-lookup"><span data-stu-id="02f31-177">If the NSG is associated to any subnet, run the `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span></span>
4. <span data-ttu-id="02f31-178">Чтобы удалить группу безопасности сети, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="02f31-178">To delete the NSG, run the following command:</span></span>

    ```powershell
    Remove-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd -Force
    ```
   
   > [!NOTE]
   > <span data-ttu-id="02f31-179">Параметр `-Force` гарантирует, что удаление не потребуется подтверждать.</span><span class="sxs-lookup"><span data-stu-id="02f31-179">The `-Force` parameter ensures you don't need to confirm the deletion.</span></span>
   > 

## <a name="next-steps"></a><span data-ttu-id="02f31-180">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="02f31-180">Next steps</span></span>
* <span data-ttu-id="02f31-181">[Включите ведение журнала](virtual-network-nsg-manage-log.md) для групп безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="02f31-181">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

