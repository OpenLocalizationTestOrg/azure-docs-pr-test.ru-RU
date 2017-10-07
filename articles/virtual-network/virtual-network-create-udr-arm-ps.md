---
title: "aaaControl маршрутизации и виртуальных устройств в Azure — PowerShell | Документы Microsoft"
description: "Узнайте, как toocontrol маршрутизации и виртуальные устройства, с помощью PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 9582fdaa-249c-4c98-9618-8c30d496940f
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.openlocfilehash: b7b8717529eb2cd8b1d28b8ab9c6e21159d14882
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-user-defined-routes-udr-using-powershell"></a><span data-ttu-id="42233-103">Создание определяемых пользователем маршрутов с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="42233-103">Create User-Defined Routes (UDR) using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="42233-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="42233-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="42233-105">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="42233-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="42233-106">Шаблон</span><span class="sxs-lookup"><span data-stu-id="42233-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="42233-107">PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="42233-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="42233-108">Интерфейс командной строки (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="42233-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)


[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="42233-109">Перед началом работы с ресурсами Azure, он является важным toounderstand, что Azure в данный момент существуют две модели развертывания: диспетчера ресурсов Azure и классическом.</span><span class="sxs-lookup"><span data-stu-id="42233-109">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="42233-110">Обязательно изучите [модели и инструменты развертывания](../azure-resource-manager/resource-manager-deployment-model.md) , прежде чем приступить к работе с какими бы то ни было ресурсами Azure.</span><span class="sxs-lookup"><span data-stu-id="42233-110">Make sure you understand [deployment models and tools](../azure-resource-manager/resource-manager-deployment-model.md) before you work with any Azure resource.</span></span> <span data-ttu-id="42233-111">Для просмотра документации hello для различных средств, щелкнув вкладки hello hello верхней части этой статьи.</span><span class="sxs-lookup"><span data-stu-id="42233-111">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span>
>

<span data-ttu-id="42233-112">В этой статье рассматриваются hello модели развертывания диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="42233-112">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="42233-113">Вы также можете [создать UDRs в hello классической модели развертывания](virtual-network-create-udr-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="42233-113">You can also [create UDRs in hello classic deployment model](virtual-network-create-udr-classic-ps.md).</span></span>

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="42233-114">Образец Hello PowerShell приведенную ниже команду ожидать простой среде уже создан на основании hello сценарии выше.</span><span class="sxs-lookup"><span data-stu-id="42233-114">hello sample PowerShell commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="42233-115">Toorun hello команд, отображаемых в этом документе, сначала построения необходимо hello тестовой среды, развернув [этот шаблон](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), нажмите кнопку **развертывание tooAzure**, замените значения параметров по умолчанию hello При необходимости и выполнения инструкции hello в hello портала.</span><span class="sxs-lookup"><span data-stu-id="42233-115">If you want toorun hello commands as they are displayed in this document, first build hello test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="42233-116">Создать hello UDR для интерфейса подсети hello</span><span class="sxs-lookup"><span data-stu-id="42233-116">Create hello UDR for hello front-end subnet</span></span>
<span data-ttu-id="42233-117">Таблица маршрутов toocreate hello и маршрутов для подсети интерфейса hello в зависимости от hello варианта выше завершения hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="42233-117">toocreate hello route table and route needed for hello front-end subnet based on hello scenario above, complete hello following steps:</span></span>

1. <span data-ttu-id="42233-118">Создание toosend маршрут использоваться все toohello toobe маршрутизации трафика, предназначенного toohello внутренней подсети (192.168.2.0/24) **FW1** виртуальное устройство (192.168.0.4).</span><span class="sxs-lookup"><span data-stu-id="42233-118">Create a route used toosend all traffic destined toohello back-end subnet (192.168.2.0/24) toobe routed toohello **FW1** virtual appliance (192.168.0.4).</span></span>

    ```powershell
    $route = New-AzureRmRouteConfig -Name RouteToBackEnd `
    -AddressPrefix 192.168.2.0/24 -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

2. <span data-ttu-id="42233-119">Создайте таблицу маршрут с именем **UDR-FrontEnd** в hello **westus** область, которая содержит маршрут hello.</span><span class="sxs-lookup"><span data-stu-id="42233-119">Create a route table named **UDR-FrontEnd** in hello **westus** region that contains hello route.</span></span>

    ```powershell
    $routeTable = New-AzureRmRouteTable -ResourceGroupName TestRG -Location westus `
    -Name UDR-FrontEnd -Route $route
    ```

3. <span data-ttu-id="42233-120">Создайте переменную, содержащую hello где hello подсети виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="42233-120">Create a variable that contains hello VNet where hello subnet is.</span></span> <span data-ttu-id="42233-121">В нашем сценарии hello виртуальной сети называется **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="42233-121">In our scenario, hello VNet is named **TestVNet**.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

4. <span data-ttu-id="42233-122">Свяжите hello таблицы маршрутов, созданной ранее toohello **переднего плана** подсети.</span><span class="sxs-lookup"><span data-stu-id="42233-122">Associate hello route table created above toohello **FrontEnd** subnet.</span></span>

    ```powershell
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
    -AddressPrefix 192.168.1.0/24 -RouteTable $routeTable
    ```

    > [!WARNING]
    > <span data-ttu-id="42233-123">Hello для приведенных выше команд hello видно содержимое hello hello объекта конфигурации виртуальной сети, который существует только на компьютере hello, где запускается PowerShell.</span><span class="sxs-lookup"><span data-stu-id="42233-123">hello output for hello command above shows hello content for hello virtual network configuration object, which only exists on hello computer where you are running PowerShell.</span></span> <span data-ttu-id="42233-124">Требуется toorun hello **AzureVirtualNetwork набор** toosave командлет tooAzure эти параметры.</span><span class="sxs-lookup"><span data-stu-id="42233-124">You need toorun hello **Set-AzureVirtualNetwork** cmdlet toosave these settings tooAzure.</span></span>
    > 

5. <span data-ttu-id="42233-125">Сохраните новую конфигурацию подсети hello в Azure.</span><span class="sxs-lookup"><span data-stu-id="42233-125">Save hello new subnet configuration in Azure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="42233-126">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="42233-126">Expected output:</span></span>
   
        Name              : TestVNet
        ResourceGroupName : TestRG
        Location          : westus
        Id                : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag              : W/"[Id]"
        ProvisioningState : Succeeded
        Tags              : 
                            Name         Value
                            ===========  =====
                            displayName  VNet 
   
        AddressSpace      : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptions       : {
                              "DnsServers": null
                            }
        NetworkInterfaces : null
        Subnets           : [
                                ...,
                              {
                                "Name": "FrontEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                "AddressPrefix": "192.168.1.0/24",
                                "IpConfigurations": [
                                  {
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB2/ipConfigurations/ipconfig1"
                                  },
                                  {
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB1/ipConfigurations/ipconfig1"
                                  }
                                ],
                                "NetworkSecurityGroup": {
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                },
                                "RouteTable": {
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-FrontEnd"
                                },
                                "ProvisioningState": "Succeeded"
                              },
                                ...
                            ]    

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="42233-127">Создать hello UDR для hello внутренней подсети</span><span class="sxs-lookup"><span data-stu-id="42233-127">Create hello UDR for hello back-end subnet</span></span>

<span data-ttu-id="42233-128">Таблица маршрутов toocreate hello и маршрутов для подсети hello серверной части, в зависимости от варианта hello выше, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="42233-128">toocreate hello route table and route needed for hello back-end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="42233-129">Создание toosend маршрут использоваться все toohello toobe маршрутизации трафика, предназначенного toohello интерфейса подсети (192.168.1.0/24) **FW1** виртуальное устройство (192.168.0.4).</span><span class="sxs-lookup"><span data-stu-id="42233-129">Create a route used toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toobe routed toohello **FW1** virtual appliance (192.168.0.4).</span></span>

    ```powershell
    $route = New-AzureRmRouteConfig -Name RouteToFrontEnd `
    -AddressPrefix 192.168.1.0/24 -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

2. <span data-ttu-id="42233-130">Создайте таблицу маршрут с именем **UDR серверной** в hello **uswest** область, которая содержит маршрут hello созданной выше.</span><span class="sxs-lookup"><span data-stu-id="42233-130">Create a route table named **UDR-BackEnd** in hello **uswest** region that contains hello route created above.</span></span>

    ```
    $routeTable = New-AzureRmRouteTable -ResourceGroupName TestRG -Location westus `
    -Name UDR-BackEnd -Route $route
    ```

3. <span data-ttu-id="42233-131">Свяжите hello таблицы маршрутов, созданной ранее toohello **серверной** подсети.</span><span class="sxs-lookup"><span data-stu-id="42233-131">Associate hello route table created above toohello **BackEnd** subnet.</span></span>

    ```powershell
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name BackEnd `
    -AddressPrefix 192.168.2.0/24 -RouteTable $routeTable
    ```

4. <span data-ttu-id="42233-132">Сохраните новую конфигурацию подсети hello в Azure.</span><span class="sxs-lookup"><span data-stu-id="42233-132">Save hello new subnet configuration in Azure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="42233-133">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="42233-133">Expected output:</span></span>
   
        Name              : TestVNet
        ResourceGroupName : TestRG
        Location          : westus
        Id                : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag              : W/"[Id]"
        ProvisioningState : Succeeded
        Tags              : 
                            Name         Value
                            ===========  =====
                            displayName  VNet 
   
        AddressSpace      : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptions       : {
                              "DnsServers": null
                            }
        NetworkInterfaces : null
        Subnets           : [
                              ...,
                              {
                                "Name": "BackEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                                "AddressPrefix": "192.168.2.0/24",
                                "IpConfigurations": [
                                  {
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICSQL2/ipConfigurations/ipconfig1"
                                  },
                                  {
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICSQL1/ipConfigurations/ipconfig1"
                                  }
                                ],
                                "NetworkSecurityGroup": {
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BacEnd"
                                },
                                "RouteTable": {
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd"
                                },
                                "ProvisioningState": "Succeeded"
                              }
                            ]

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="42233-134">Включение IP-пересылки на FW1</span><span class="sxs-lookup"><span data-stu-id="42233-134">Enable IP forwarding on FW1</span></span>
<span data-ttu-id="42233-135">tooenable IP-пересылки в hello сетевой Адаптер, используемый с **FW1**, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="42233-135">tooenable IP forwarding in hello NIC used by **FW1**, follow hello steps below.</span></span>

1. <span data-ttu-id="42233-136">Создайте переменную, которая содержит параметры hello для сетевого Адаптера, используемого FW1 hello.</span><span class="sxs-lookup"><span data-stu-id="42233-136">Create a variable that contains hello settings for hello NIC used by FW1.</span></span> <span data-ttu-id="42233-137">В нашем сценарии hello сетевого Адаптера с именем **NICFW1**.</span><span class="sxs-lookup"><span data-stu-id="42233-137">In our scenario, hello NIC is named **NICFW1**.</span></span>

    ```powershell
    $nicfw1 = Get-AzureRmNetworkInterface -ResourceGroupName TestRG -Name NICFW1
    ```

2. <span data-ttu-id="42233-138">Включить IP-пересылку и сохраните параметры сетевого Адаптера hello.</span><span class="sxs-lookup"><span data-stu-id="42233-138">Enable IP forwarding, and save hello NIC settings.</span></span>

    ```powershell
    $nicfw1.EnableIPForwarding = 1
    Set-AzureRmNetworkInterface -NetworkInterface $nicfw1
    ```
   
    <span data-ttu-id="42233-139">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="42233-139">Expected output:</span></span>
   
        Name                 : NICFW1
        ResourceGroupName    : TestRG
        Location             : westus
        Id                   : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICFW1
        Etag                 : W/"[Id]"
        ProvisioningState    : Succeeded
        Tags                 : 
                               Name         Value                  
                               ===========  =======================
                               displayName  NetworkInterfaces - DMZ
   
        VirtualMachine       : {
                                 "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/FW1"
                               }
        IpConfigurations     : [
                                 {
                                   "Name": "ipconfig1",
                                   "Etag": "W/\"[Id]\"",
                                   "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICFW1/ipConfigurations/ipconfig1",
                                   "PrivateIpAddress": "192.168.0.4",
                                   "PrivateIpAllocationMethod": "Static",
                                   "Subnet": {
                                     "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/DMZ"
                                   },
                                   "PublicIpAddress": {
                                     "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/PIPFW1"
                                   },
                                   "LoadBalancerBackendAddressPools": [],
                                   "LoadBalancerInboundNatRules": [],
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]
        DnsSettings          : {
                                 "DnsServers": [],
                                 "AppliedDnsServers": [],
                                 "InternalDnsNameLabel": null,
                                 "InternalFqdn": null
                               }
        EnableIPForwarding   : True
        NetworkSecurityGroup : null
        Primary              : True

