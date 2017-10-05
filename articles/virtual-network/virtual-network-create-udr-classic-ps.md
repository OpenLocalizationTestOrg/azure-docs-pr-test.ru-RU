---
title: "Контроль маршрутизации в виртуальной сети Azure с помощью PowerShell (классическая модель) | Документация Майкрософт"
description: "Сведения об управлении маршрутизацией в виртуальных сетях с помощью PowerShell | классическая модель"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: d8d07c16-cbe5-4536-acd6-870269346fe3
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: e9564d223cb85529f1fa97bc398d35c6debcedae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-powershell"></a><span data-ttu-id="34767-103">Управление маршрутизацией и использование виртуальных модулей (классический режим) с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="34767-103">Control routing and use virtual appliances (classic) using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="34767-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="34767-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="34767-105">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="34767-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="34767-106">Шаблон</span><span class="sxs-lookup"><span data-stu-id="34767-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="34767-107">PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="34767-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="34767-108">Интерфейс командной строки (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="34767-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="34767-109">Прежде чем приступить к работе с ресурсами Azure, обратите внимание на то, что в настоящее время в Azure существует две модели развертывания: классическая модель развертывания и модель развертывания с помощью Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="34767-109">Before you work with Azure resources, it's important to understand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="34767-110">Обязательно изучите [модели и инструменты развертывания](../azure-resource-manager/resource-manager-deployment-model.md) , прежде чем приступить к работе с какими бы то ни было ресурсами Azure.</span><span class="sxs-lookup"><span data-stu-id="34767-110">Make sure you understand [deployment models and tools](../azure-resource-manager/resource-manager-deployment-model.md) before you work with any Azure resource.</span></span> <span data-ttu-id="34767-111">Для просмотра документации о различных средствах выберите соответствующий параметр в верхней части данной статьи.</span><span class="sxs-lookup"><span data-stu-id="34767-111">You can view the documentation for different tools by selecting an option at the top of this article.</span></span> <span data-ttu-id="34767-112">В этой статье рассматривается классическая модель развертывания.</span><span class="sxs-lookup"><span data-stu-id="34767-112">This article covers the classic deployment model.</span></span>
> 

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="34767-113">Для приведенных ниже примеров команд Azure PowerShell требуется уже созданная простая среда, основанная на приведенном выше сценарии.</span><span class="sxs-lookup"><span data-stu-id="34767-113">The sample Azure PowerShell commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="34767-114">Для выполнения команд в том виде, в каком они представлены в данном документе, создайте среду, описанную в разделе о [создании виртуальной сети (классический режим) с помощью PowerShell](virtual-networks-create-vnet-classic-netcfg-ps.md).</span><span class="sxs-lookup"><span data-stu-id="34767-114">If you want to run the commands as they are displayed in this document, create the environment shown in [create a VNet (classic) using PowerShell](virtual-networks-create-vnet-classic-netcfg-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-the-udr-for-the-front-end-subnet"></a><span data-ttu-id="34767-115">Создание определяемого пользователем маршрута для подсети переднего плана</span><span class="sxs-lookup"><span data-stu-id="34767-115">Create the UDR for the front end subnet</span></span>
<span data-ttu-id="34767-116">Чтобы создать таблицу маршрутов и маршрут, необходимые для подсети переднего плана, на основании приведенного выше сценария, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="34767-116">To create the route table and route needed for the front end subnet based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="34767-117">Чтобы создать таблицу маршрутов для интерфейсной подсети, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="34767-117">Run the following command to create a route table for the front-end subnet:</span></span>

    ```powershell
    New-AzureRouteTable -Name UDR-FrontEnd -Location uswest `
    -Label "Route table for front end subnet"
    ```

2. <span data-ttu-id="34767-118">Чтобы создать маршрут в таблице маршрутов для отправки всего трафика, предназначенного для серверной подсети (192.168.2.0/24), в виртуальную машину **FW1** (192.168.0.4), выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="34767-118">Run the following command to create a route in the route table to send all traffic destined to the back-end subnet (192.168.2.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```powershell
    Get-AzureRouteTable UDR-FrontEnd `
    |Set-AzureRoute -RouteName RouteToBackEnd -AddressPrefix 192.168.2.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. <span data-ttu-id="34767-119">Чтобы сопоставить таблицу маршрутов с подсетью **FrontEnd**, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="34767-119">Run the following command to associate the route table with the **FrontEnd** subnet:</span></span>

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName FrontEnd `
    -RouteTableName UDR-FrontEnd
    ```

## <a name="create-the-udr-for-the-back-end-subnet"></a><span data-ttu-id="34767-120">Создание определяемого пользователем маршрута для серверной подсети</span><span class="sxs-lookup"><span data-stu-id="34767-120">Create the UDR for the back-end subnet</span></span>
<span data-ttu-id="34767-121">Чтобы создать таблицу маршрутов и маршрут, необходимые для серверной подсети, на основании сценария, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="34767-121">To create the route table and route needed for the back end subnet based on the scenario, complete the following steps:</span></span>

1. <span data-ttu-id="34767-122">Чтобы создать таблицу маршрутов для серверной подсети, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="34767-122">Run the following command to create a route table for the back-end subnet:</span></span>

    ```powershell
    New-AzureRouteTable -Name UDR-BackEnd `
    -Location uswest `
    -Label "Route table for back end subnet"
    ```

2. <span data-ttu-id="34767-123">Чтобы создать маршрут в таблице маршрутов для отправки всего трафика, предназначенного для интерфейсной подсети (192.168.1.0/24), в виртуальную машину **FW1** (192.168.0.4), выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="34767-123">Run the following command to create a route in the route table to send all traffic destined to the front-end subnet (192.168.1.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```powershell
    Get-AzureRouteTable UDR-BackEnd
    | Set-AzureRoute `
    -RouteName RouteToFrontEnd `
    -AddressPrefix 192.168.1.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. <span data-ttu-id="34767-124">Чтобы сопоставить таблицу маршрутов с подсетью **BackEnd**, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="34767-124">Run the following command to associate the route table with the **BackEnd** subnet:</span></span>

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName BackEnd `
    -RouteTableName UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-the-fw1-vm"></a><span data-ttu-id="34767-125">Включение IP-пересылки на виртуальной машине FW1</span><span class="sxs-lookup"><span data-stu-id="34767-125">Enable IP forwarding on the FW1 VM</span></span>

<span data-ttu-id="34767-126">Чтобы включить IP-пересылку на виртуальной машине FW1, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="34767-126">To enable IP forwarding in the FW1 VM, complete the following steps:</span></span>

1. <span data-ttu-id="34767-127">Чтобы проверить состояние IP-пересылки, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="34767-127">Run the following command to check the status of IP forwarding:</span></span>

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Get-AzureIPForwarding
    ```

2. <span data-ttu-id="34767-128">Чтобы включить IP-пересылку для виртуальной машины *FW1*, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="34767-128">Run the following command to enable IP forwarding for the *FW1* VM:</span></span>

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Set-AzureIPForwarding -Enable
    ```
