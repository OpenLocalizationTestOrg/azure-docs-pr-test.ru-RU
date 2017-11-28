---
title: "aaaControl маршрутизации в классической виртуальной сети Azure - PowerShell - | Документы Microsoft"
description: "Узнайте, как toocontrol маршрутизации в виртуальных сетей с помощью PowerShell | Классический"
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
ms.openlocfilehash: 36edf263fb434d5fb13310d4324da20e57f016a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-powershell"></a><span data-ttu-id="931e0-103">Управление маршрутизацией и использование виртуальных модулей (классический режим) с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="931e0-103">Control routing and use virtual appliances (classic) using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="931e0-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="931e0-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="931e0-105">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="931e0-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="931e0-106">Шаблон</span><span class="sxs-lookup"><span data-stu-id="931e0-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="931e0-107">PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="931e0-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="931e0-108">Интерфейс командной строки (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="931e0-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="931e0-109">Перед началом работы с ресурсами Azure, он является важным toounderstand, что Azure в данный момент существуют две модели развертывания: диспетчера ресурсов Azure и классическом.</span><span class="sxs-lookup"><span data-stu-id="931e0-109">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="931e0-110">Обязательно изучите [модели и инструменты развертывания](../azure-resource-manager/resource-manager-deployment-model.md) , прежде чем приступить к работе с какими бы то ни было ресурсами Azure.</span><span class="sxs-lookup"><span data-stu-id="931e0-110">Make sure you understand [deployment models and tools](../azure-resource-manager/resource-manager-deployment-model.md) before you work with any Azure resource.</span></span> <span data-ttu-id="931e0-111">Для просмотра документации hello для различных средств, выбрав параметр hello верхней части этой статьи.</span><span class="sxs-lookup"><span data-stu-id="931e0-111">You can view hello documentation for different tools by selecting an option at hello top of this article.</span></span> <span data-ttu-id="931e0-112">В этой статье рассматриваются hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="931e0-112">This article covers hello classic deployment model.</span></span>
> 

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="931e0-113">Образец Hello Azure PowerShell приведенную ниже команду ожидать простой среде уже создан на основании hello сценарии выше.</span><span class="sxs-lookup"><span data-stu-id="931e0-113">hello sample Azure PowerShell commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="931e0-114">Toorun hello команд, отображаемых в этом документе, создать среды hello, показанный на [Создание виртуальной сети (классические), с помощью PowerShell](virtual-networks-create-vnet-classic-netcfg-ps.md).</span><span class="sxs-lookup"><span data-stu-id="931e0-114">If you want toorun hello commands as they are displayed in this document, create hello environment shown in [create a VNet (classic) using PowerShell](virtual-networks-create-vnet-classic-netcfg-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="931e0-115">Создать hello UDR для подсети hello переднего плана</span><span class="sxs-lookup"><span data-stu-id="931e0-115">Create hello UDR for hello front end subnet</span></span>
<span data-ttu-id="931e0-116">Таблица маршрутов toocreate hello и маршрутов для подсети hello переднего плана, в зависимости от варианта hello выше, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="931e0-116">toocreate hello route table and route needed for hello front end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="931e0-117">Выполните следующие команды toocreate hello таблицы маршрутов для подсети интерфейса hello:</span><span class="sxs-lookup"><span data-stu-id="931e0-117">Run hello following command toocreate a route table for hello front-end subnet:</span></span>

    ```powershell
    New-AzureRouteTable -Name UDR-FrontEnd -Location uswest `
    -Label "Route table for front end subnet"
    ```

2. <span data-ttu-id="931e0-118">Запустите все toohello внутренней подсети (192.168.2.0/24) toohello трафика, предназначенного hello, следующая команда toocreate маршрут в toosend таблицы маршрутов hello **FW1** виртуальной Машины (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="931e0-118">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello back-end subnet (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```powershell
    Get-AzureRouteTable UDR-FrontEnd `
    |Set-AzureRoute -RouteName RouteToBackEnd -AddressPrefix 192.168.2.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. <span data-ttu-id="931e0-119">Выполнения hello следующие таблицы маршрутов hello tooassociate команды с hello **переднего плана** подсети:</span><span class="sxs-lookup"><span data-stu-id="931e0-119">Run hello following command tooassociate hello route table with hello **FrontEnd** subnet:</span></span>

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName FrontEnd `
    -RouteTableName UDR-FrontEnd
    ```

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="931e0-120">Создать hello UDR для hello внутренней подсети</span><span class="sxs-lookup"><span data-stu-id="931e0-120">Create hello UDR for hello back-end subnet</span></span>
<span data-ttu-id="931e0-121">Таблица маршрутов toocreate hello и маршрута, необходимые для повторного hello завершить подсети, в зависимости от варианта hello, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="931e0-121">toocreate hello route table and route needed for hello back end subnet based on hello scenario, complete hello following steps:</span></span>

1. <span data-ttu-id="931e0-122">Выполните следующие команды toocreate hello таблицы маршрутов для подсети внутренней hello:</span><span class="sxs-lookup"><span data-stu-id="931e0-122">Run hello following command toocreate a route table for hello back-end subnet:</span></span>

    ```powershell
    New-AzureRouteTable -Name UDR-BackEnd `
    -Location uswest `
    -Label "Route table for back end subnet"
    ```

2. <span data-ttu-id="931e0-123">Запустите все toohello интерфейса подсети (192.168.1.0/24) toohello трафика, предназначенного hello, следующая команда toocreate маршрут в toosend таблицы маршрутов hello **FW1** виртуальной Машины (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="931e0-123">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```powershell
    Get-AzureRouteTable UDR-BackEnd
    | Set-AzureRoute `
    -RouteName RouteToFrontEnd `
    -AddressPrefix 192.168.1.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. <span data-ttu-id="931e0-124">Выполнения hello следующие таблицы маршрутов hello tooassociate команды с hello **серверной** подсети:</span><span class="sxs-lookup"><span data-stu-id="931e0-124">Run hello following command tooassociate hello route table with hello **BackEnd** subnet:</span></span>

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName BackEnd `
    -RouteTableName UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-hello-fw1-vm"></a><span data-ttu-id="931e0-125">Включить IP-пересылки на приветствия FW1 виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="931e0-125">Enable IP forwarding on hello FW1 VM</span></span>

<span data-ttu-id="931e0-126">tooenable IP-пересылки в hello FW1 ВМ, полный hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="931e0-126">tooenable IP forwarding in hello FW1 VM, complete hello following steps:</span></span>

1. <span data-ttu-id="931e0-127">Выполните следующие команды toocheck hello состояние IP-пересылки hello.</span><span class="sxs-lookup"><span data-stu-id="931e0-127">Run hello following command toocheck hello status of IP forwarding:</span></span>

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Get-AzureIPForwarding
    ```

2. <span data-ttu-id="931e0-128">Выполнения hello следующая команда tooenable IP-пересылки для hello *FW1* виртуальной Машины:</span><span class="sxs-lookup"><span data-stu-id="931e0-128">Run hello following command tooenable IP forwarding for hello *FW1* VM:</span></span>

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Set-AzureIPForwarding -Enable
    ```
