---
title: "aaaControl маршрутизации в классической виртуальной сети Azure - CLI - | Документы Microsoft"
description: "Узнайте, как toocontrol маршрутизации в виртуальных сетей с помощью hello Azure CLI в hello классической модели развертывания"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: ca2b4638-8777-4d30-b972-eb790a7c804f
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: 07dde573f1a605bf280156c261d51e213ede0cdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-hello-azure-cli"></a><span data-ttu-id="5e262-103">Маршрутизация управления и использования виртуальных устройств (классической) с помощью hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5e262-103">Control routing and use virtual appliances (classic) using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5e262-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5e262-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="5e262-105">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="5e262-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="5e262-106">Шаблон</span><span class="sxs-lookup"><span data-stu-id="5e262-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="5e262-107">PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="5e262-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="5e262-108">Интерфейс командной строки (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="5e262-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="5e262-109">В этой статье рассматриваются hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="5e262-109">This article covers hello classic deployment model.</span></span> <span data-ttu-id="5e262-110">Вы также можете [управлять маршрутизацией и использования виртуальных устройств в модели развертывания диспетчера ресурсов hello](virtual-network-create-udr-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="5e262-110">You can also [control routing and use virtual appliances in hello Resource Manager deployment model](virtual-network-create-udr-arm-cli.md).</span></span>

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="5e262-111">приведенную ниже команду Azure CLI Образец Hello ожидать простой среде уже создан на основании hello сценарии выше.</span><span class="sxs-lookup"><span data-stu-id="5e262-111">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="5e262-112">Toorun hello команд, отображаемых в этом документе, создать среды hello, показанный на [Создание виртуальной сети (классические), с помощью Azure CLI hello](virtual-networks-create-vnet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="5e262-112">If you want toorun hello commands as they are displayed in this document, create hello environment shown in [create a VNet (classic) using hello Azure CLI](virtual-networks-create-vnet-classic-cli.md).</span></span>

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="5e262-113">Создать hello UDR для подсети hello переднего плана</span><span class="sxs-lookup"><span data-stu-id="5e262-113">Create hello UDR for hello front end subnet</span></span>
<span data-ttu-id="5e262-114">Таблица маршрутов toocreate hello и маршрутов для подсети hello переднего плана, в зависимости от варианта hello выше, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="5e262-114">toocreate hello route table and route needed for hello front end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="5e262-115">Следующая команда tooswitch tooclassic режим выполнения hello:</span><span class="sxs-lookup"><span data-stu-id="5e262-115">Run hello following command tooswitch tooclassic mode:</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="5e262-116">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="5e262-116">Output:</span></span>

        info:    New mode is asm

2. <span data-ttu-id="5e262-117">Выполните следующие команды toocreate hello таблицы маршрутов для подсети интерфейса hello:</span><span class="sxs-lookup"><span data-stu-id="5e262-117">Run hello following command toocreate a route table for hello front-end subnet:</span></span>

    ```azurecli
    azure network route-table create -n UDR-FrontEnd -l uswest
    ```
   
    <span data-ttu-id="5e262-118">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="5e262-118">Output:</span></span>
   
        info:    Executing command network route-table create
        info:    Creating route table "UDR-FrontEnd"
        info:    Getting route table "UDR-FrontEnd"
        data:    Name                            : UDR-FrontEnd
        data:    Location                        : West US
        info:    network route-table create command OK
   
    <span data-ttu-id="5e262-119">Параметры</span><span class="sxs-lookup"><span data-stu-id="5e262-119">Parameters:</span></span>
   
   * <span data-ttu-id="5e262-120">**-l (или --location)**.</span><span class="sxs-lookup"><span data-stu-id="5e262-120">**-l (or --location)**.</span></span> <span data-ttu-id="5e262-121">Регион Azure, где hello новой NSG будет создан.</span><span class="sxs-lookup"><span data-stu-id="5e262-121">Azure region where hello new NSG will be created.</span></span> <span data-ttu-id="5e262-122">В нашем случае это *westus*.</span><span class="sxs-lookup"><span data-stu-id="5e262-122">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="5e262-123">**-n (или --name)**.</span><span class="sxs-lookup"><span data-stu-id="5e262-123">**-n (or --name)**.</span></span> <span data-ttu-id="5e262-124">Имя для hello новая NSG.</span><span class="sxs-lookup"><span data-stu-id="5e262-124">Name for hello new NSG.</span></span> <span data-ttu-id="5e262-125">В данном сценарии это *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="5e262-125">For our scenario, *NSG-FrontEnd*.</span></span>
3. <span data-ttu-id="5e262-126">Запустите все toohello внутренней подсети (192.168.2.0/24) toohello трафика, предназначенного hello, следующая команда toocreate маршрут в toosend таблицы маршрутов hello **FW1** виртуальной Машины (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="5e262-126">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello back-end subnet (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route set -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

    <span data-ttu-id="5e262-127">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="5e262-127">Output:</span></span>
   
        info:    Executing command network route-table route set
        info:    Getting route table "UDR-FrontEnd"
        info:    Setting route "RouteToBackEnd" in a route table "UDR-FrontEnd"
        info:    network route-table route set command OK
   
    <span data-ttu-id="5e262-128">Параметры</span><span class="sxs-lookup"><span data-stu-id="5e262-128">Parameters:</span></span>
   
   * <span data-ttu-id="5e262-129">**-r (или --route-table-name)**.</span><span class="sxs-lookup"><span data-stu-id="5e262-129">**-r (or --route-table-name)**.</span></span> <span data-ttu-id="5e262-130">Имя таблицы маршрутов hello, куда будут добавлены hello маршрута.</span><span class="sxs-lookup"><span data-stu-id="5e262-130">Name of hello route table where hello route will be added.</span></span> <span data-ttu-id="5e262-131">В данном сценарии это *UDR-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="5e262-131">For our scenario, *UDR-FrontEnd*.</span></span>
   * <span data-ttu-id="5e262-132">**-a (или --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="5e262-132">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="5e262-133">Префикс адреса для подсети hello, где пакеты, предназначенные для.</span><span class="sxs-lookup"><span data-stu-id="5e262-133">Address prefix for hello subnet where packets are destined to.</span></span> <span data-ttu-id="5e262-134">В данном сценарии это *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="5e262-134">For our scenario, *192.168.2.0/24*.</span></span>
   * <span data-ttu-id="5e262-135">**-t (или --next-hop-type)**.</span><span class="sxs-lookup"><span data-stu-id="5e262-135">**-t (or --next-hop-type)**.</span></span> <span data-ttu-id="5e262-136">Тип объекта, куда будет отправляться трафик.</span><span class="sxs-lookup"><span data-stu-id="5e262-136">Type of object traffic will be sent to.</span></span> <span data-ttu-id="5e262-137">Возможные значения: *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet* или *None*.</span><span class="sxs-lookup"><span data-stu-id="5e262-137">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
   * <span data-ttu-id="5e262-138">**-p (или --next-hop-ip-address**).</span><span class="sxs-lookup"><span data-stu-id="5e262-138">**-p (or --next-hop-ip-address**).</span></span> <span data-ttu-id="5e262-139">IP-адрес следующего прыжка.</span><span class="sxs-lookup"><span data-stu-id="5e262-139">IP address for next hop.</span></span> <span data-ttu-id="5e262-140">В нашем случае это *192.168.0.4*.</span><span class="sxs-lookup"><span data-stu-id="5e262-140">For our scenario, *192.168.0.4*.</span></span>
4. <span data-ttu-id="5e262-141">Выполнения hello следующая команда таблицы маршрутов hello tooassociate, созданных с помощью hello **переднего плана** подсети:</span><span class="sxs-lookup"><span data-stu-id="5e262-141">Run hello following command tooassociate hello route table created with hello **FrontEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    <span data-ttu-id="5e262-142">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="5e262-142">Output:</span></span>
   
        info:    Executing command network vnet subnet route-table add
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        info:    Associating route table "UDR-FrontEnd" and subnet "FrontEnd"
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        data:    Route table name                : UDR-FrontEnd
        data:      Location                      : West US
        data:      Routes:
        info:    network vnet subnet route-table add command OK    
   
    <span data-ttu-id="5e262-143">Параметры</span><span class="sxs-lookup"><span data-stu-id="5e262-143">Parameters:</span></span>
   
   * <span data-ttu-id="5e262-144">**-t (или --vnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="5e262-144">**-t (or --vnet-name)**.</span></span> <span data-ttu-id="5e262-145">Имя виртуальной сети, где находится подсети hello hello.</span><span class="sxs-lookup"><span data-stu-id="5e262-145">Name of hello VNet where hello subnet is located.</span></span> <span data-ttu-id="5e262-146">В данном сценарии это *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="5e262-146">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="5e262-147">**-n (или --subnet-name**).</span><span class="sxs-lookup"><span data-stu-id="5e262-147">**-n (or --subnet-name**.</span></span> <span data-ttu-id="5e262-148">Имя таблицы маршрутов hello hello подсеть будет добавлено к.</span><span class="sxs-lookup"><span data-stu-id="5e262-148">Name of hello subnet hello route table will be added to.</span></span> <span data-ttu-id="5e262-149">В данном сценарии это *FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="5e262-149">For our scenario, *FrontEnd*.</span></span>

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="5e262-150">Создать hello UDR для hello внутренней подсети</span><span class="sxs-lookup"><span data-stu-id="5e262-150">Create hello UDR for hello back-end subnet</span></span>
<span data-ttu-id="5e262-151">Таблица маршрутов toocreate hello и маршрута, необходимые для hello конечной подсети в зависимости от варианта hello, полный hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="5e262-151">toocreate hello route table and route needed for hello back-end subnet based on hello scenario, complete hello following steps:</span></span>

1. <span data-ttu-id="5e262-152">Выполните следующие команды toocreate hello таблицы маршрутов для подсети внутренней hello:</span><span class="sxs-lookup"><span data-stu-id="5e262-152">Run hello following command toocreate a route table for hello back-end subnet:</span></span>

    ```azurecli
    azure network route-table create -n UDR-BackEnd -l uswest
    ```

2. <span data-ttu-id="5e262-153">Запустите все toohello интерфейса подсети (192.168.1.0/24) toohello трафика, предназначенного hello, следующая команда toocreate маршрут в toosend таблицы маршрутов hello **FW1** виртуальной Машины (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="5e262-153">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route set -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

3. <span data-ttu-id="5e262-154">Выполнения hello следующие таблицы маршрутов hello tooassociate команды с hello **серверной** подсети:</span><span class="sxs-lookup"><span data-stu-id="5e262-154">Run hello following command tooassociate hello route table with hello **BackEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n BackEnd -r UDR-BackEnd
    ```

