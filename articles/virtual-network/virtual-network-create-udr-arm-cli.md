---
title: "Здравствуйте, aaaControl маршрутизации и виртуальных устройств с помощью Azure CLI 2.0 | Документы Microsoft"
description: "Узнайте, как toocontrol маршрутизации и виртуальных устройств с помощью hello Azure CLI 2.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 5452a0b8-21a6-4699-8d6a-e2d8faf32c25
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/12/2017
ms.author: jdial
ms.openlocfilehash: 79b908848932a4365dab1b7497b6a0dbf44bbaf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-user-defined-routes-udr-using-hello-azure-cli-20"></a><span data-ttu-id="01dee-103">Создайте маршруты определяемые пользователем (UDR) с помощью Azure CLI 2.0 hello</span><span class="sxs-lookup"><span data-stu-id="01dee-103">Create User-Defined Routes (UDR) using hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="01dee-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="01dee-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="01dee-105">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="01dee-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="01dee-106">Шаблон</span><span class="sxs-lookup"><span data-stu-id="01dee-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="01dee-107">PowerShell (классическое развертывание)</span><span class="sxs-lookup"><span data-stu-id="01dee-107">PowerShell (Classic deployment)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="01dee-108">Интерфейс командной строки (классическое развертывание)</span><span class="sxs-lookup"><span data-stu-id="01dee-108">CLI (Classic deployment)</span></span>](virtual-network-create-udr-classic-cli.md)

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="01dee-109">Задача hello toocomplete версии CLI</span><span class="sxs-lookup"><span data-stu-id="01dee-109">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="01dee-110">Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.</span><span class="sxs-lookup"><span data-stu-id="01dee-110">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="01dee-111">[Azure CLI 1.0](virtual-network-create-udr-arm-cli-nodejs.md) — нашей CLI для hello классический и ресурсов развертывания модели управления</span><span class="sxs-lookup"><span data-stu-id="01dee-111">[Azure CLI 1.0](virtual-network-create-udr-arm-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="01dee-112">[Azure CLI 2.0](#Create-the-UDR-for-the-front-end-subnet) -нашей нового поколения CLI для модели развертывания управления hello ресурсов (в этой статье)</span><span class="sxs-lookup"><span data-stu-id="01dee-112">[Azure CLI 2.0](#Create-the-UDR-for-the-front-end-subnet) - our next generation CLI for hello resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="01dee-113">приведенную ниже команду Azure CLI Образец Hello ожидать простой среде уже создан на основании hello сценарии выше.</span><span class="sxs-lookup"><span data-stu-id="01dee-113">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="01dee-114">Toorun hello команд, отображаемых в этом документе, сначала построения необходимо hello тестовой среды, развернув [этот шаблон](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), нажмите кнопку **развертывание tooAzure**, замените значения параметров по умолчанию hello При необходимости и выполнения инструкции hello в hello портала.</span><span class="sxs-lookup"><span data-stu-id="01dee-114">If you want toorun hello commands as they are displayed in this document, first build hello test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>


## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="01dee-115">Создать hello UDR для интерфейса подсети hello</span><span class="sxs-lookup"><span data-stu-id="01dee-115">Create hello UDR for hello front-end subnet</span></span>
<span data-ttu-id="01dee-116">Таблица маршрутов toocreate hello и маршрутов для подсети hello переднего плана, в зависимости от варианта hello выше, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="01dee-116">toocreate hello route table and route needed for hello front end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="01dee-117">Создание таблицы маршрутов для подсети интерфейса hello с hello [создание таблицы маршрутов в сети az](/cli/azure/network/route-table#create) команды:</span><span class="sxs-lookup"><span data-stu-id="01dee-117">Create a route table for hello front-end subnet with hello [az network route-table create](/cli/azure/network/route-table#create) command:</span></span>

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --location centralus \
    --name UDR-FrontEnd
    ```

    <span data-ttu-id="01dee-118">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="01dee-118">Output:</span></span>

    ```json
    {
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd",
    "location": "centralus",
    "name": "UDR-FrontEnd",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "routes": [],
    "subnets": null,
    "tags": null,
    "type": "Microsoft.Network/routeTables"
    }
    ```

2. <span data-ttu-id="01dee-119">Создать маршрут, который отправляет все toohello внутренней подсети (192.168.2.0/24) toohello трафика, предназначенного **FW1** виртуальную Машину (192.168.0.4) с помощью hello [создать маршрут к таблице маршрутов сети az](/cli/azure/network/route-table/route#create) команды:</span><span class="sxs-lookup"><span data-stu-id="01dee-119">Create a route that sends all traffic destined toohello back-end subnet (192.168.2.0/24) toohello **FW1** VM (192.168.0.4) using hello [az network route-table route create](/cli/azure/network/route-table/route#create) command:</span></span>

    ```azurecli 
    az network route-table route create \
    --resource-group testrg \
    --name RouteToBackEnd \
    --route-table-name UDR-FrontEnd \
    --address-prefix 192.168.2.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

    <span data-ttu-id="01dee-120">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="01dee-120">Output:</span></span>

    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd/routes/RouteToBackEnd",
    "name": "RouteToBackEnd",
    "nextHopIpAddress": "192.168.0.4",
    "nextHopType": "VirtualAppliance",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg"
    }
    ```
    <span data-ttu-id="01dee-121">Параметры</span><span class="sxs-lookup"><span data-stu-id="01dee-121">Parameters:</span></span>

    * <span data-ttu-id="01dee-122">**--route-table-name**.</span><span class="sxs-lookup"><span data-stu-id="01dee-122">**--route-table-name**.</span></span> <span data-ttu-id="01dee-123">Имя таблицы маршрутов hello, куда будут добавлены hello маршрута.</span><span class="sxs-lookup"><span data-stu-id="01dee-123">Name of hello route table where hello route will be added.</span></span> <span data-ttu-id="01dee-124">В данном сценарии это *UDR-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="01dee-124">For our scenario, *UDR-FrontEnd*.</span></span>
    * <span data-ttu-id="01dee-125">**--address-prefix**.</span><span class="sxs-lookup"><span data-stu-id="01dee-125">**--address-prefix**.</span></span> <span data-ttu-id="01dee-126">Префикс адреса для подсети hello, где пакеты, предназначенные для.</span><span class="sxs-lookup"><span data-stu-id="01dee-126">Address prefix for hello subnet where packets are destined to.</span></span> <span data-ttu-id="01dee-127">В данном сценарии это *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="01dee-127">For our scenario, *192.168.2.0/24*.</span></span>
    * <span data-ttu-id="01dee-128">**--next-hop-type**.</span><span class="sxs-lookup"><span data-stu-id="01dee-128">**--next-hop-type**.</span></span> <span data-ttu-id="01dee-129">Тип объекта, куда будет отправляться трафик.</span><span class="sxs-lookup"><span data-stu-id="01dee-129">Type of object traffic will be sent to.</span></span> <span data-ttu-id="01dee-130">Возможные значения: *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet* или *None*.</span><span class="sxs-lookup"><span data-stu-id="01dee-130">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
    * <span data-ttu-id="01dee-131">**--next-hop-ip-address**.</span><span class="sxs-lookup"><span data-stu-id="01dee-131">**--next-hop-ip-address**.</span></span> <span data-ttu-id="01dee-132">IP-адрес следующего прыжка.</span><span class="sxs-lookup"><span data-stu-id="01dee-132">IP address for next hop.</span></span> <span data-ttu-id="01dee-133">В нашем случае это *192.168.0.4*.</span><span class="sxs-lookup"><span data-stu-id="01dee-133">For our scenario, *192.168.0.4*.</span></span>

3. <span data-ttu-id="01dee-134">Запустите hello [обновления подсети виртуальной сети сети az](/cli/azure/network/vnet/subnet#update) созданную таблицу маршрутов hello tooassociate команды с hello **переднего плана** подсети:</span><span class="sxs-lookup"><span data-stu-id="01dee-134">Run hello [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) command tooassociate hello route table created above with hello **FrontEnd** subnet:</span></span>

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name FrontEnd \
    --route-table UDR-FrontEnd
    ```

    <span data-ttu-id="01dee-135">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="01dee-135">Output:</span></span>

    ```json
    {
    "addressPrefix": "192.168.1.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testvnet/subnets/FrontEnd",
    "ipConfigurations": null,
    "name": "FrontEnd",
    "networkSecurityGroup": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "resourceNavigationLinks": null,
    "routeTable": {
        "etag": null,
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd",
        "location": null,
        "name": null,
        "provisioningState": null,
        "resourceGroup": "testrg",
        "routes": null,
        "subnets": null,
        "tags": null,
        "type": null
        }
    }
    ```

    <span data-ttu-id="01dee-136">Параметры</span><span class="sxs-lookup"><span data-stu-id="01dee-136">Parameters:</span></span>
    
    * <span data-ttu-id="01dee-137">**--vnet-name**.</span><span class="sxs-lookup"><span data-stu-id="01dee-137">**--vnet-name**.</span></span> <span data-ttu-id="01dee-138">Имя виртуальной сети, где находится подсети hello hello.</span><span class="sxs-lookup"><span data-stu-id="01dee-138">Name of hello VNet where hello subnet is located.</span></span> <span data-ttu-id="01dee-139">В данном сценарии это *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="01dee-139">For our scenario, *TestVNet*.</span></span>

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="01dee-140">Создать hello UDR для hello внутренней подсети</span><span class="sxs-lookup"><span data-stu-id="01dee-140">Create hello UDR for hello back-end subnet</span></span>

<span data-ttu-id="01dee-141">toocreate hello таблицы маршрутов и маршрутизации для подсети hello серверной части, в зависимости от варианта hello выше завершения hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="01dee-141">toocreate hello route table and route needed for hello back-end subnet based on hello scenario above, complete hello following steps:</span></span>

1. <span data-ttu-id="01dee-142">Выполните следующие команды toocreate hello таблицы маршрутов для подсети внутренней hello:</span><span class="sxs-lookup"><span data-stu-id="01dee-142">Run hello following command toocreate a route table for hello back-end subnet:</span></span>

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --name UDR-BackEnd \
    --location centralus
    ```

2. <span data-ttu-id="01dee-143">Запустите все toohello интерфейса подсети (192.168.1.0/24) toohello трафика, предназначенного hello, следующая команда toocreate маршрут в toosend таблицы маршрутов hello **FW1** виртуальной Машины (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="01dee-143">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    az network route-table route create \
    --resource-group testrg \
    --name RouteToFrontEnd \
    --route-table-name UDR-BackEnd \
    --address-prefix 192.168.1.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

3. <span data-ttu-id="01dee-144">Выполнения hello следующие таблицы маршрутов hello tooassociate команды с hello **серверной** подсети:</span><span class="sxs-lookup"><span data-stu-id="01dee-144">Run hello following command tooassociate hello route table with hello **BackEnd** subnet:</span></span>

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name BackEnd \
    --route-table UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="01dee-145">Включение IP-пересылки на FW1</span><span class="sxs-lookup"><span data-stu-id="01dee-145">Enable IP forwarding on FW1</span></span>

<span data-ttu-id="01dee-146">tooenable IP-пересылки в hello сетевой Адаптер, используемый с **FW1**полный hello следующие действия:</span><span class="sxs-lookup"><span data-stu-id="01dee-146">tooenable IP forwarding in hello NIC used by **FW1**, complete hello following steps:</span></span>

1. <span data-ttu-id="01dee-147">Запустите hello [Показать сетевого адаптера сети az](/cli/azure/network/nic#show) с toodisplay JMESPATH фильтра, hello текущей **включить пересылку ip** значение для **включить IP-пересылки**.</span><span class="sxs-lookup"><span data-stu-id="01dee-147">Run hello [az network nic show](/cli/azure/network/nic#show) command with a JMESPATH filter toodisplay hello current **enable-ip-forwarding** value for **Enable IP forwarding**.</span></span> <span data-ttu-id="01dee-148">Оно должно быть задано слишком*false*.</span><span class="sxs-lookup"><span data-stu-id="01dee-148">It should be set too*false*.</span></span>

    ```azurecli
    az network nic show \
    --resource-group testrg \
    --nname nicfw1 \
    --query 'enableIpForwarding' -o tsv
    ```

    <span data-ttu-id="01dee-149">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="01dee-149">Output:</span></span>

        false

2. <span data-ttu-id="01dee-150">Выполните следующие команды tooenable IP-пересылки hello.</span><span class="sxs-lookup"><span data-stu-id="01dee-150">Run hello following command tooenable IP forwarding:</span></span>

    ```azurecli
    az network nic update \
    --resource-group testrg \
    --name nicfw1 \
    --ip-forwarding true
    ```

    <span data-ttu-id="01dee-151">Изучите консоли toohello потокового вывода hello или просто повторное тестирование для конкретных hello **enableIpForwarding** значение:</span><span class="sxs-lookup"><span data-stu-id="01dee-151">You can examine hello output streamed toohello console, or just retest for hello specific **enableIpForwarding** value:</span></span>

    ```azurecli
    az network nic show -g testrg -n nicfw1 --query 'enableIpForwarding' -o tsv
    ```

    <span data-ttu-id="01dee-152">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="01dee-152">Output:</span></span>

        true

    <span data-ttu-id="01dee-153">Параметры</span><span class="sxs-lookup"><span data-stu-id="01dee-153">Parameters:</span></span>

    <span data-ttu-id="01dee-154">**--ip-forwarding**: *true* или *false*.</span><span class="sxs-lookup"><span data-stu-id="01dee-154">**--ip-forwarding**: *true* or *false*.</span></span>

