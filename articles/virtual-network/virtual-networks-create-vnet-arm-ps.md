---
title: "aaaCreate виртуальной сети - Azure PowerShell | Документы Microsoft"
description: "Узнайте, как toocreate в виртуальной сети с помощью PowerShell."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a31f4f12-54ee-4339-b968-1a8097ca77d3
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8d6e395a77f71de9f94b6304b05450e46b47544f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-powershell"></a><span data-ttu-id="8180b-103">Создание виртуальной сети с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="8180b-103">Create a virtual network using PowerShell</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="8180b-104">Azure предоставляет две модели развертывания: с помощью Azure Resource Manager и классическую.</span><span class="sxs-lookup"><span data-stu-id="8180b-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="8180b-105">Корпорация Майкрософт рекомендует создать ресурсы с помощью модели развертывания диспетчера ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="8180b-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="8180b-106">Дополнительные сведения о toolearn hello различий между моделями hello двух чтения hello [модели развертывания Azure понять](../azure-resource-manager/resource-manager-deployment-model.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="8180b-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>
 
<span data-ttu-id="8180b-107">В этой статье объясняется, как toocreate виртуальной сети путем развертывания диспетчера ресурсов hello модели с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8180b-107">This article explains how toocreate a VNet through hello Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="8180b-108">Также можно создать виртуальную сеть через диспетчер ресурсов с помощью других средств или создайте виртуальную сеть через hello классической модели развертывания, выбрав другой вариант hello после списка:</span><span class="sxs-lookup"><span data-stu-id="8180b-108">You can also create a VNet through Resource Manager using other tools or create a VNet through hello classic deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8180b-109">Портал</span><span class="sxs-lookup"><span data-stu-id="8180b-109">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
> * [<span data-ttu-id="8180b-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8180b-110">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
> * [<span data-ttu-id="8180b-111">ИНТЕРФЕЙС КОМАНДНОЙ СТРОКИ</span><span class="sxs-lookup"><span data-stu-id="8180b-111">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
> * [<span data-ttu-id="8180b-112">Шаблон</span><span class="sxs-lookup"><span data-stu-id="8180b-112">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
> * [<span data-ttu-id="8180b-113">Портал (классический)</span><span class="sxs-lookup"><span data-stu-id="8180b-113">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
> * [<span data-ttu-id="8180b-114">PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="8180b-114">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [<span data-ttu-id="8180b-115">Интерфейс командной строки (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="8180b-115">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a><span data-ttu-id="8180b-116">Создать виртуальную сеть</span><span class="sxs-lookup"><span data-stu-id="8180b-116">Create a virtual network</span></span>

<span data-ttu-id="8180b-117">toocreate, виртуальной сети, с помощью PowerShell, полные hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="8180b-117">toocreate a virtual network using PowerShell, complete hello following steps:</span></span>

1. <span data-ttu-id="8180b-118">Установка и настройка Azure PowerShell, выполнив указанные ниже действия hello в hello [как tooInstall и настройка Azure PowerShell](/powershell/azure/overview) статьи.</span><span class="sxs-lookup"><span data-stu-id="8180b-118">Install and configure Azure PowerShell, by following hello steps in hello [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) article.</span></span>

2. <span data-ttu-id="8180b-119">При необходимости создайте новую группу ресурсов, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="8180b-119">If necessary, create a new resource group, as shown below.</span></span> <span data-ttu-id="8180b-120">В этом случае нужно создать группу ресурсов с именем *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="8180b-120">For this scenario, create a resource group named *TestRG*.</span></span> <span data-ttu-id="8180b-121">Дополнительные сведения о группах ресурсов см. в разделе "Группы ресурсов" [обзора Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8180b-121">For more information about resource groups, visit [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    ```powershell   
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    <span data-ttu-id="8180b-122">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="8180b-122">Expected output:</span></span>

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/[Subscription Id]/resourceGroups/TestRG    
3. <span data-ttu-id="8180b-123">Создайте новую виртуальную сеть с именем *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="8180b-123">Create a new VNet named *TestVNet*:</span></span>

    ```powershell
    New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet `
    -AddressPrefix 192.168.0.0/16 -Location centralus
    ```

    <span data-ttu-id="8180b-124">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="8180b-124">Expected output:</span></span>

        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                   : W/"[Id]"
        ProvisioningState          : Succeeded
        Tags                       : 
        AddressSpace               : {
                                   "AddressPrefixes": [
                                     "192.168.0.0/16"
                                   ]
                                  }
        DhcpOptions                : {}
        Subnets                    : []
        VirtualNetworkPeerings     : []
4. <span data-ttu-id="8180b-125">Сохранить hello объекта виртуальной сети в переменной:</span><span class="sxs-lookup"><span data-stu-id="8180b-125">Store hello virtual network object in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

   > [!TIP]
   > <span data-ttu-id="8180b-126">Можно объединить шаги 3 и 4, выполнив команду `$vnet = New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet -AddressPrefix 192.168.0.0/16 -Location centralus`.</span><span class="sxs-lookup"><span data-stu-id="8180b-126">You can combine steps 3 and 4 by running `$vnet = New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet -AddressPrefix 192.168.0.0/16 -Location centralus`.</span></span>
   > 

5. <span data-ttu-id="8180b-127">Добавьте переменную подсети toohello новой виртуальной сети:</span><span class="sxs-lookup"><span data-stu-id="8180b-127">Add a subnet toohello new VNet variable:</span></span>

    ```powershell
    Add-AzureRmVirtualNetworkSubnetConfig -Name FrontEnd `
    -VirtualNetwork $vnet -AddressPrefix 192.168.1.0/24
    ```

    <span data-ttu-id="8180b-128">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="8180b-128">Expected output:</span></span>
   
        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                  : W/"[Id]"
        ProvisioningState     : Succeeded
        Tags                  :
        AddressSpace          : {
                                  "AddressPrefixes": [
                                    "192.168.0.0/16"
                                  ]
                                }
        DhcpOptions           : {}
        Subnets             : [
                                  {
                                    "Name": "FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24"
                                  }
                                ]
        VirtualNetworkPeerings     : []

6. <span data-ttu-id="8180b-129">Повторите шаг 5 выше для каждой подсети требуется toocreate.</span><span class="sxs-lookup"><span data-stu-id="8180b-129">Repeat step 5 above for each subnet you want toocreate.</span></span> <span data-ttu-id="8180b-130">Hello следующая команда создает hello *серверной* подсети для hello сценария:</span><span class="sxs-lookup"><span data-stu-id="8180b-130">hello following command creates hello *BackEnd* subnet for hello scenario:</span></span>

    ```powershell
    Add-AzureRmVirtualNetworkSubnetConfig -Name BackEnd `
    -VirtualNetwork $vnet -AddressPrefix 192.168.2.0/24
    ```

7. <span data-ttu-id="8180b-131">Несмотря на то, что вы создаете подсетей, они в настоящее время только существуют в локальной переменной используется tooretrieve hello hello виртуальной сети, созданных на шаге 4 выше.</span><span class="sxs-lookup"><span data-stu-id="8180b-131">Although you create subnets, they currently only exist in hello local variable used tooretrieve hello VNet you create in step 4 above.</span></span> <span data-ttu-id="8180b-132">hello изменения toosave tooAzure, запустите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="8180b-132">toosave hello changes tooAzure, run hello following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```
   
    <span data-ttu-id="8180b-133">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="8180b-133">Expected output:</span></span>
   
        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                  : W/"[Id]"
        ProvisioningState     : Succeeded
        Tags                  :
        AddressSpace          : {
                                  "AddressPrefixes": [
                                    "192.168.0.0/16"
                                  ]
                                }
        DhcpOptions           : {
                                  "DnsServers": []
                                }
        Subnets               : [
                                  {
                                    "Name": "FrontEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24",
                                    "IpConfigurations": [],
                                    "ProvisioningState": "Succeeded"
                                  },
                                  {
                                    "Name": "BackEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                                    "AddressPrefix": "192.168.2.0/24",
                                    "IpConfigurations": [],
                                    "ProvisioningState": "Succeeded"
                                  }
                                ]
        VirtualNetworkPeerings : []

## <a name="next-steps"></a><span data-ttu-id="8180b-134">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8180b-134">Next steps</span></span>

<span data-ttu-id="8180b-135">Узнайте, как tooconnect:</span><span class="sxs-lookup"><span data-stu-id="8180b-135">Learn how tooconnect:</span></span>

- <span data-ttu-id="8180b-136">Виртуальная сеть виртуальной машины (VM) tooa, считывая hello [создания виртуальной Машины Windows](../virtual-machines/virtual-machines-windows-ps-create.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="8180b-136">A virtual machine (VM) tooa virtual network by reading hello [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md) article.</span></span> <span data-ttu-id="8180b-137">Вместо создания виртуальной сети и подсети в шагах hello hello статей, можно выбрать существующей виртуальной сети и подсети tooconnect для виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="8180b-137">Instead of creating a VNet and subnet in hello steps of hello articles, you can select an existing VNet and subnet tooconnect a VM to.</span></span>
- <span data-ttu-id="8180b-138">Здравствуйте, считывая hello виртуальных сетей в виртуальной сети tooother [подключение виртуальных сетей](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="8180b-138">hello virtual network tooother virtual networks by reading hello [Connect VNets](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) article.</span></span>
- <span data-ttu-id="8180b-139">tooan Hello виртуальной сети в локальной сети с помощью виртуальной частной сети сеть сеть (VPN) или канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="8180b-139">hello virtual network tooan on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="8180b-140">Дополнительные сведения в разделе hello [подключения локальной сети tooan виртуальной сети с помощью VPN сайтами](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) и [связывание виртуальной сети tooan канал ExpressRoute](../expressroute/expressroute-howto-linkvnet-arm.md) статей.</span><span class="sxs-lookup"><span data-stu-id="8180b-140">Learn how by reading hello [Connect a VNet tooan on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet tooan ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-arm.md) articles.</span></span>
