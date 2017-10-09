---
title: "aaaManage сетевых групп безопасности - Azure PowerShell | Документы Microsoft"
description: "Узнайте, как toomanage сетевых групп безопасности, с помощью PowerShell."
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
ms.openlocfilehash: 930fe5e0827896ad67b24d84e41a5d3f898ba838
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-powershell"></a><span data-ttu-id="10258-103">Управление группами безопасности сети с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="10258-103">Manage network security groups using PowerShell</span></span>

[!INCLUDE [virtual-network-manage-arm-selectors-include.md](../../includes/virtual-network-manage-nsg-arm-selectors-include.md)]

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="10258-104">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="10258-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="10258-105">В этой статье описан с помощью модели развертывания диспетчера ресурсов hello, который рекомендуется в большинстве случаев новый вместо hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="10258-105">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="10258-106">Извлечение информации</span><span class="sxs-lookup"><span data-stu-id="10258-106">Retrieve Information</span></span>
<span data-ttu-id="10258-107">Вы можете просмотреть существующие группы безопасности сети, получить правила для существующей группы и узнать, с какими ресурсами она связана.</span><span class="sxs-lookup"><span data-stu-id="10258-107">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="10258-108">Просмотр существующих групп безопасности сети</span><span class="sxs-lookup"><span data-stu-id="10258-108">View existing NSGs</span></span>
<span data-ttu-id="10258-109">tooview все существующие Nsg в подписке, запустите hello `Get-AzureRmNetworkSecurityGroup` командлета.</span><span class="sxs-lookup"><span data-stu-id="10258-109">tooview all existing NSGs in a subscription, run hello `Get-AzureRmNetworkSecurityGroup` cmdlet.</span></span>

<span data-ttu-id="10258-110">Ожидаемый результат:</span><span class="sxs-lookup"><span data-stu-id="10258-110">Expected result:</span></span>

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


<span data-ttu-id="10258-111">tooview списка Nsg hello в определенной группе ресурсов, запустите hello `Get-AzureRmNetworkSecurityGroup` командлета.</span><span class="sxs-lookup"><span data-stu-id="10258-111">tooview hello list of NSGs in a specific resource group, run hello `Get-AzureRmNetworkSecurityGroup` cmdlet.</span></span>

<span data-ttu-id="10258-112">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="10258-112">Expected output:</span></span>

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

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="10258-113">Перечисление всех правил для группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="10258-113">List all rules for an NSG</span></span>
<span data-ttu-id="10258-114">tooview hello правила NSG с именем **NSG-FrontEnd**, введите следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="10258-114">tooview hello rules of an NSG named **NSG-FrontEnd**, enter hello following command:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd | Select SecurityRules -ExpandProperty SecurityRules
```

<span data-ttu-id="10258-115">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="10258-115">Expected output:</span></span>

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
> <span data-ttu-id="10258-116">Можно также использовать `Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name "NSG-FrontEnd" | Select DefaultSecurityRules -ExpandProperty DefaultSecurityRules` toolist правила по умолчанию hello из hello **NSG-FrontEnd** NSG.</span><span class="sxs-lookup"><span data-stu-id="10258-116">You can also use `Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name "NSG-FrontEnd" | Select DefaultSecurityRules -ExpandProperty DefaultSecurityRules` toolist hello default rules from hello **NSG-FrontEnd** NSG.</span></span>
> 

### <a name="view-nsgs-associations"></a><span data-ttu-id="10258-117">Просмотр связей для группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="10258-117">View NSGs associations</span></span>
<span data-ttu-id="10258-118">tooview какие ресурсы hello **NSG-FrontEnd** NSG — связан с, запустите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="10258-118">tooview what resources hello **NSG-FrontEnd** NSG is associate with, run hello following command:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
```

<span data-ttu-id="10258-119">Найдите hello **сетевых интерфейсов** и **подсети** свойства, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="10258-119">Look for hello **NetworkInterfaces** and **Subnets** properties as shown below:</span></span>

    NetworkInterfaces    : []
    Subnets              : [
                             {
                               "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                               "IpConfigurations": []
                             }
                           ]

<span data-ttu-id="10258-120">В предыдущем примере hello hello NSG не связан tooany сетевых интерфейсов (NIC); Это связанный tooa подсеть с именем **переднего плана**.</span><span class="sxs-lookup"><span data-stu-id="10258-120">In hello previous example, hello NSG is not associated tooany network interfaces (NICs); it is associated tooa subnet named **FrontEnd**.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="10258-121">Управление правилами</span><span class="sxs-lookup"><span data-stu-id="10258-121">Manage rules</span></span>
<span data-ttu-id="10258-122">Добавление существующей NSG tooan правила, изменять существующие правила и удалять правила.</span><span class="sxs-lookup"><span data-stu-id="10258-122">You can add rules tooan existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="10258-123">Добавление правила</span><span class="sxs-lookup"><span data-stu-id="10258-123">Add a rule</span></span>
<span data-ttu-id="10258-124">tooadd правила, что позволяет **входящих** tooport трафика **443** с любого компьютера toohello **NSG-FrontEnd** NSG завершения hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="10258-124">tooadd a rule allowing **inbound** traffic tooport **443** from any machine toohello **NSG-FrontEnd** NSG, complete hello following steps:</span></span>

1. <span data-ttu-id="10258-125">Выполните hello, следующая команда tooretrieve hello существующей NSG и сохранить его в переменной.</span><span class="sxs-lookup"><span data-stu-id="10258-125">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell   
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="10258-126">Выполните следующие команды tooadd hello toohello правила NSG:</span><span class="sxs-lookup"><span data-stu-id="10258-126">Run hello following command tooadd a rule toohello NSG:</span></span>

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

3. <span data-ttu-id="10258-127">Запустите следующую команду hello toohello NSG, внесены изменения toosave hello.</span><span class="sxs-lookup"><span data-stu-id="10258-127">toosave hello changes made toohello NSG, run hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```
    <span data-ttu-id="10258-128">Отображение только hello правила безопасности ожидаемый результат:</span><span class="sxs-lookup"><span data-stu-id="10258-128">Expected output showing only hello security rules:</span></span>
   
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

### <a name="change-a-rule"></a><span data-ttu-id="10258-129">Изменение правила</span><span class="sxs-lookup"><span data-stu-id="10258-129">Change a rule</span></span>
<span data-ttu-id="10258-130">правило toochange hello, созданной ранее tooallow входящий трафик от hello **Internet** , выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="10258-130">toochange hello rule created above tooallow inbound traffic from hello **Internet** only, follow hello steps below.</span></span>

1. <span data-ttu-id="10258-131">Выполните hello, следующая команда tooretrieve hello существующей NSG и сохранить его в переменной.</span><span class="sxs-lookup"><span data-stu-id="10258-131">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell 
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="10258-132">Выполните следующую команду с новыми настройками правило hello hello.</span><span class="sxs-lookup"><span data-stu-id="10258-132">Run hello following command with hello new rule settings:</span></span>

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

3. <span data-ttu-id="10258-133">Запустите следующую команду hello toohello NSG, внесены изменения toosave hello.</span><span class="sxs-lookup"><span data-stu-id="10258-133">toosave hello changes made toohello NSG, run hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="10258-134">Отображение только hello правила безопасности ожидаемый результат:</span><span class="sxs-lookup"><span data-stu-id="10258-134">Expected output showing only hello security rules:</span></span>
   
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

### <a name="delete-a-rule"></a><span data-ttu-id="10258-135">Удаление правила</span><span class="sxs-lookup"><span data-stu-id="10258-135">Delete a rule</span></span>
1. <span data-ttu-id="10258-136">Выполните hello, следующая команда tooretrieve hello существующей NSG и сохранить его в переменной.</span><span class="sxs-lookup"><span data-stu-id="10258-136">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="10258-137">Выполните следующую команду tooremove hello правила из hello NSG hello.</span><span class="sxs-lookup"><span data-stu-id="10258-137">Run hello following command tooremove hello rule from hello NSG:</span></span>

    ```powershell
    Remove-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg -Name https-rule
    ```

3. <span data-ttu-id="10258-138">Сохраните изменения, внесенные hello toohello NSG, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="10258-138">Save hello changes made toohello NSG, by running hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="10258-139">Ожидаемый результат, отображаются только hello правил безопасности, уведомление hello **https правило** больше не отображается:</span><span class="sxs-lookup"><span data-stu-id="10258-139">Expected output showing only hello security rules, notice hello **https-rule** is no longer listed:</span></span>
   
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

## <a name="manage-associations"></a><span data-ttu-id="10258-140">Управление связями</span><span class="sxs-lookup"><span data-stu-id="10258-140">Manage associations</span></span>
<span data-ttu-id="10258-141">Можно связать NSG toosubnets и сетевых адаптеров.</span><span class="sxs-lookup"><span data-stu-id="10258-141">You can associate an NSG toosubnets and NICs.</span></span> <span data-ttu-id="10258-142">Можно также отменить связь группы безопасности сети с любым ресурсом.</span><span class="sxs-lookup"><span data-stu-id="10258-142">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-tooa-nic"></a><span data-ttu-id="10258-143">Связывание NSG tooa сетевого Адаптера</span><span class="sxs-lookup"><span data-stu-id="10258-143">Associate an NSG tooa NIC</span></span>
<span data-ttu-id="10258-144">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** сетевого Адаптера, полный hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="10258-144">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, complete hello following steps:</span></span>

1. <span data-ttu-id="10258-145">Выполните hello, следующая команда tooretrieve hello существующей NSG и сохранить его в переменной.</span><span class="sxs-lookup"><span data-stu-id="10258-145">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="10258-146">Выполните hello, следующая команда tooretrieve hello существующего сетевого Адаптера и сохранить его в переменной.</span><span class="sxs-lookup"><span data-stu-id="10258-146">Run hello following command tooretrieve hello existing NIC and store it in a variable:</span></span>

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

3. <span data-ttu-id="10258-147">Набор hello **NetworkSecurityGroup** свойство hello **Сетевых** значение переменной toohello hello **NSG** переменных, введя следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="10258-147">Set hello **NetworkSecurityGroup** property of hello **NIC** variable toohello value of hello **NSG** variable, by entering hello following command:</span></span>

    ```powershell
    $nic.NetworkSecurityGroup = $nsg
    ```

4. <span data-ttu-id="10258-148">toohello сетевого Адаптера, запустите следующую команду hello внесены изменения toosave hello.</span><span class="sxs-lookup"><span data-stu-id="10258-148">toosave hello changes made toohello NIC, run hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    <span data-ttu-id="10258-149">Ожидаемый результат отображение только hello **NetworkSecurityGroup** свойства:</span><span class="sxs-lookup"><span data-stu-id="10258-149">Expected output showing only hello **NetworkSecurityGroup** property:</span></span>
   
        NetworkSecurityGroup : {
                                 "SecurityRules": [],
                                 "DefaultSecurityRules": [],
                                 "NetworkInterfaces": [],
                                 "Subnets": [],
                                 "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                               }

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="10258-150">Отмена связи с сетевым адаптером для группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="10258-150">Dissociate an NSG from a NIC</span></span>
<span data-ttu-id="10258-151">toodissociate hello **NSG-FrontEnd** NSG из hello **TestNICWeb1** сетевого Адаптера, полный hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="10258-151">toodissociate hello **NSG-FrontEnd** NSG from hello **TestNICWeb1** NIC, complete hello following steps:</span></span>

1. <span data-ttu-id="10258-152">Выполните hello, следующая команда tooretrieve hello существующего сетевого Адаптера и сохранить его в переменной.</span><span class="sxs-lookup"><span data-stu-id="10258-152">Run hello following command tooretrieve hello existing NIC and store it in a variable:</span></span>

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

2. <span data-ttu-id="10258-153">Набор hello **NetworkSecurityGroup** свойство hello **Сетевых** переменной слишком**$null** , выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="10258-153">Set hello **NetworkSecurityGroup** property of hello **NIC** variable too**$null** by running hello following command:</span></span>

    ```powershell
    $nic.NetworkSecurityGroup = $null
    ```

3. <span data-ttu-id="10258-154">toohello сетевого Адаптера, запустите следующую команду hello внесены изменения toosave hello.</span><span class="sxs-lookup"><span data-stu-id="10258-154">toosave hello changes made toohello NIC, run hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    <span data-ttu-id="10258-155">Ожидаемый результат отображение только hello **NetworkSecurityGroup** свойства:</span><span class="sxs-lookup"><span data-stu-id="10258-155">Expected output showing only hello **NetworkSecurityGroup** property:</span></span>
   
        NetworkSecurityGroup : null

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="10258-156">Отмена связи с подсетью для группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="10258-156">Dissociate an NSG from a subnet</span></span>
<span data-ttu-id="10258-157">toodissociate hello **NSG-FrontEnd** NSG из hello **переднего плана** подсети, полный hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="10258-157">toodissociate hello **NSG-FrontEnd** NSG from hello **FrontEnd** subnet, complete hello following steps:</span></span>

1. <span data-ttu-id="10258-158">Выполните hello, следующая команда tooretrieve hello существующей виртуальной сети и сохранить его в переменной.</span><span class="sxs-lookup"><span data-stu-id="10258-158">Run hello following command tooretrieve hello existing VNet and store it in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. <span data-ttu-id="10258-159">Выполнения hello следующие команда hello tooretrieve **переднего плана** подсети и сохранить его в переменной:</span><span class="sxs-lookup"><span data-stu-id="10258-159">Run hello following command tooretrieve hello **FrontEnd** subnet and store it in a variable:</span></span>

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. <span data-ttu-id="10258-160">Набор hello **NetworkSecurityGroup** свойство hello **подсети** переменной слишком**$null** , введя hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="10258-160">Set hello **NetworkSecurityGroup** property of hello **subnet** variable too**$null** by entering hello following command:</span></span>

    ```powershell
    $subnet.NetworkSecurityGroup = $null
    ```

4. <span data-ttu-id="10258-161">toohello подсети, запустите следующую команду hello внесены изменения toosave hello.</span><span class="sxs-lookup"><span data-stu-id="10258-161">toosave hello changes made toohello subnet, run hello following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="10258-162">Ожидаемый результат, отображаются только hello свойств hello **переднего плана** подсети.</span><span class="sxs-lookup"><span data-stu-id="10258-162">Expected output showing only hello properties of hello **FrontEnd** subnet.</span></span> <span data-ttu-id="10258-163">Обратите внимание, что свойства **NetworkSecurityGroup**нет:</span><span class="sxs-lookup"><span data-stu-id="10258-163">Notice there isn't a property for **NetworkSecurityGroup**:</span></span>
   
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

### <a name="associate-an-nsg-tooa-subnet"></a><span data-ttu-id="10258-164">Связывание NSG tooa подсети</span><span class="sxs-lookup"><span data-stu-id="10258-164">Associate an NSG tooa subnet</span></span>
<span data-ttu-id="10258-165">tooassociate hello **NSG-FrontEnd** NSG toohello **FronEnd** снова подсети, полный hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="10258-165">tooassociate hello **NSG-FrontEnd** NSG toohello **FronEnd** subnet again, complete hello following steps:</span></span>

1. <span data-ttu-id="10258-166">Выполните hello, следующая команда tooretrieve hello существующей виртуальной сети и сохранить его в переменной.</span><span class="sxs-lookup"><span data-stu-id="10258-166">Run hello following command tooretrieve hello existing VNet and store it in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. <span data-ttu-id="10258-167">Выполнения hello следующие команда hello tooretrieve **переднего плана** подсети и сохранить его в переменной:</span><span class="sxs-lookup"><span data-stu-id="10258-167">Run hello following command tooretrieve hello **FrontEnd** subnet and store it in a variable:</span></span>

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. <span data-ttu-id="10258-168">Выполните hello, следующая команда tooretrieve hello существующей NSG и сохранить его в переменной.</span><span class="sxs-lookup"><span data-stu-id="10258-168">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

4. <span data-ttu-id="10258-169">Набор hello **NetworkSecurityGroup** свойство hello **подсети** переменной слишком**$null** , выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="10258-169">Set hello **NetworkSecurityGroup** property of hello **subnet** variable too**$null** by running hello following command:</span></span>

    ```powershell
    $subnet.NetworkSecurityGroup = $nsg
    ```

5. <span data-ttu-id="10258-170">toohello подсети, запустите следующую команду hello внесены изменения toosave hello.</span><span class="sxs-lookup"><span data-stu-id="10258-170">toosave hello changes made toohello subnet, run hello following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="10258-171">Ожидаемый результат отображение только hello **NetworkSecurityGroup** свойство hello **переднего плана** подсети:</span><span class="sxs-lookup"><span data-stu-id="10258-171">Expected output showing only hello **NetworkSecurityGroup** property of hello **FrontEnd** subnet:</span></span>
   
        ...
        "NetworkSecurityGroup": {
                                  "SecurityRules": [],
                                  "DefaultSecurityRules": [],
                                  "NetworkInterfaces": [],
                                  "Subnets": [],
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                }
        ...

## <a name="delete-an-nsg"></a><span data-ttu-id="10258-172">Удаление группы NSG</span><span class="sxs-lookup"><span data-stu-id="10258-172">Delete an NSG</span></span>
<span data-ttu-id="10258-173">NSG можно удалить только в том случае, если она не сопоставлена tooany ресурсов.</span><span class="sxs-lookup"><span data-stu-id="10258-173">You can only delete an NSG if it's not associated tooany resource.</span></span> <span data-ttu-id="10258-174">toodelete NSG, выполните следующие действия hello.</span><span class="sxs-lookup"><span data-stu-id="10258-174">toodelete an NSG, follow hello steps below.</span></span>

1. <span data-ttu-id="10258-175">ресурсы hello toocheck связанные tooan NSG, запустите hello `azure network nsg show` как показано в [связи Nsg представление](#View-NSGs-associations).</span><span class="sxs-lookup"><span data-stu-id="10258-175">toocheck hello resources associated tooan NSG, run hello `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span></span>
2. <span data-ttu-id="10258-176">Если hello NSG связанные tooany сетевых адаптеров, запустите hello `azure network nic set` как показано в [связь между Сетевыми NSG](#Dissociate-an-NSG-from-a-NIC) для каждого сетевого адаптера.</span><span class="sxs-lookup"><span data-stu-id="10258-176">If hello NSG is associated tooany NICs, run hello `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span></span> 
3. <span data-ttu-id="10258-177">Если hello NSG связанные tooany подсети, запустите hello `azure network vnet subnet set` как показано в [связь NSG из подсети](#Dissociate-an-NSG-from-a-subnet) для каждой подсети.</span><span class="sxs-lookup"><span data-stu-id="10258-177">If hello NSG is associated tooany subnet, run hello `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span></span>
4. <span data-ttu-id="10258-178">hello toodelete NSG, запустите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="10258-178">toodelete hello NSG, run hello following command:</span></span>

    ```powershell
    Remove-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd -Force
    ```
   
   > [!NOTE]
   > <span data-ttu-id="10258-179">Hello `-Force` параметр гарантирует удаление hello tooconfirm не требуется.</span><span class="sxs-lookup"><span data-stu-id="10258-179">hello `-Force` parameter ensures you don't need tooconfirm hello deletion.</span></span>
   > 

## <a name="next-steps"></a><span data-ttu-id="10258-180">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="10258-180">Next steps</span></span>
* <span data-ttu-id="10258-181">[Включите ведение журнала](virtual-network-nsg-manage-log.md) для групп безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="10258-181">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

