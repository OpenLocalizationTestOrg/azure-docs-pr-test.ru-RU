---
title: "Виртуальная сеть — Azure CLI 2.0 aaaCreate | Документы Microsoft"
description: "Узнайте, как toocreate виртуальной сети с помощью hello Azure CLI 2.0."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 75966bcc-0056-4667-8482-6f08ca38e77a
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e79b7fe780fc81f4866f810d830824e43a5a43b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-hello-azure-cli-20"></a><span data-ttu-id="fbff0-103">Создание виртуальной сети с помощью Azure CLI 2.0 hello</span><span class="sxs-lookup"><span data-stu-id="fbff0-103">Create a virtual network using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="fbff0-104">Azure предоставляет две модели развертывания: с помощью Azure Resource Manager и классическую.</span><span class="sxs-lookup"><span data-stu-id="fbff0-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="fbff0-105">Корпорация Майкрософт рекомендует создать ресурсы с помощью модели развертывания диспетчера ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="fbff0-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="fbff0-106">Дополнительные сведения о toolearn hello различий между моделями hello двух чтения hello [модели развертывания Azure понять](../azure-resource-manager/resource-manager-deployment-model.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="fbff0-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="fbff0-107">Задача hello toocomplete версии CLI</span><span class="sxs-lookup"><span data-stu-id="fbff0-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="fbff0-108">Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.</span><span class="sxs-lookup"><span data-stu-id="fbff0-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="fbff0-109">[Azure CLI 1.0](virtual-networks-create-vnet-cli-nodejs.md) — нашей CLI для hello классический и ресурсов развертывания модели управления</span><span class="sxs-lookup"><span data-stu-id="fbff0-109">[Azure CLI 1.0](virtual-networks-create-vnet-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span>
- <span data-ttu-id="fbff0-110">[Azure CLI 2.0](#create-a-virtual-network) -нашей нового поколения CLI для модели развертывания управления hello ресурсов (в этой статье) "</span><span class="sxs-lookup"><span data-stu-id="fbff0-110">[Azure CLI 2.0](#create-a-virtual-network) - our next generation CLI for hello resource management deployment model (this article)\`</span></span>
 
    <span data-ttu-id="fbff0-111">Также можно создать виртуальную сеть через диспетчер ресурсов с помощью других средств или создайте виртуальную сеть через hello классической модели развертывания, выбрав другой вариант hello после списка:</span><span class="sxs-lookup"><span data-stu-id="fbff0-111">You can also create a VNet through Resource Manager using other tools or create a VNet through hello classic deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="fbff0-112">Портал</span><span class="sxs-lookup"><span data-stu-id="fbff0-112">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
> * [<span data-ttu-id="fbff0-113">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fbff0-113">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
> * [<span data-ttu-id="fbff0-114">ИНТЕРФЕЙС КОМАНДНОЙ СТРОКИ</span><span class="sxs-lookup"><span data-stu-id="fbff0-114">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
> * [<span data-ttu-id="fbff0-115">Шаблон</span><span class="sxs-lookup"><span data-stu-id="fbff0-115">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
> * [<span data-ttu-id="fbff0-116">Портал (классический)</span><span class="sxs-lookup"><span data-stu-id="fbff0-116">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
> * [<span data-ttu-id="fbff0-117">PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="fbff0-117">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [<span data-ttu-id="fbff0-118">Интерфейс командной строки (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="fbff0-118">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]


## <a name="create-a-virtual-network"></a><span data-ttu-id="fbff0-119">Создать виртуальную сеть</span><span class="sxs-lookup"><span data-stu-id="fbff0-119">Create a virtual network</span></span>

<span data-ttu-id="fbff0-120">в виртуальной сети с помощью toocreate hello Azure CLI 2.0 завершения hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="fbff0-120">toocreate a virtual network using hello Azure CLI 2.0, complete hello following steps:</span></span>

1. <span data-ttu-id="fbff0-121">Установка и настройка hello последней [Azure CLI 2.0](/cli/azure/install-az-cli2) и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="fbff0-121">Install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

2. <span data-ttu-id="fbff0-122">Создание группы ресурсов для виртуальной сети с помощью hello [Создание группы az](/cli/azure/group#create) с hello `--name` и `--location` аргументов:</span><span class="sxs-lookup"><span data-stu-id="fbff0-122">Create a resource group for your VNet using hello [az group create](/cli/azure/group#create) command with hello `--name` and `--location` arguments:</span></span>

    ```azurecli
    az group create --name TestRG --location centralus
    ```

3. <span data-ttu-id="fbff0-123">Создайте виртуальную сеть и подсеть.</span><span class="sxs-lookup"><span data-stu-id="fbff0-123">Create a VNet and a subnet:</span></span>

    ```azurecli
    az network vnet create \
    --name TestVNet \
    --resource-group TestRG \
    --location centralus \
    --address-prefix 192.168.0.0/16 \
    --subnet-name FrontEnd \
    --subnet-prefix 192.168.1.0/24
    ```

    <span data-ttu-id="fbff0-124">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="fbff0-124">Expected output:</span></span>
    
    ```json
    {
        "newVNet": {
            "addressSpace": {
            "addressPrefixes": [
            "192.168.0.0/16"
            ]
            },
            "dhcpOptions": {
            "dnsServers": []
            },
            "provisioningState": "Succeeded",
            "resourceGuid": "<guid>",
            "subnets": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                "name": "FrontEnd",
                "properties": {
                "addressPrefix": "192.168.1.0/24",
                "provisioningState": "Succeeded"
                },
                "resourceGroup": "TestRG"
            }
            ]
            }
    }
    ```

    <span data-ttu-id="fbff0-125">Используемые параметры:</span><span class="sxs-lookup"><span data-stu-id="fbff0-125">Parameters used:</span></span>

    - <span data-ttu-id="fbff0-126">`--name TestVNet`: Имя toobe виртуальной сети hello создан.</span><span class="sxs-lookup"><span data-stu-id="fbff0-126">`--name TestVNet`: Name of hello VNet toobe created.</span></span>
    - <span data-ttu-id="fbff0-127">`--resource-group TestRG`: имя группы ресурсов hello #, управляющий hello ресурсов.</span><span class="sxs-lookup"><span data-stu-id="fbff0-127">`--resource-group TestRG`: # hello resource group name that controls hello resource.</span></span> 
    - <span data-ttu-id="fbff0-128">`--location centralus`: hello расположение, в которой toodeploy.</span><span class="sxs-lookup"><span data-stu-id="fbff0-128">`--location centralus`: hello location into which toodeploy.</span></span>
    - <span data-ttu-id="fbff0-129">`--address-prefix 192.168.0.0/16`: hello префикс адреса и блока.</span><span class="sxs-lookup"><span data-stu-id="fbff0-129">`--address-prefix 192.168.0.0/16`: hello address prefix and block.</span></span>  
    - <span data-ttu-id="fbff0-130">`--subnet-name FrontEnd`: имя подсети hello hello.</span><span class="sxs-lookup"><span data-stu-id="fbff0-130">`--subnet-name FrontEnd`: hello name of hello subnet.</span></span>
    - <span data-ttu-id="fbff0-131">`--subnet-prefix 192.168.1.0/24`: hello префикс адреса и блока.</span><span class="sxs-lookup"><span data-stu-id="fbff0-131">`--subnet-prefix 192.168.1.0/24`: hello address prefix and block.</span></span>

    <span data-ttu-id="fbff0-132">toolist toouse основные сведения hello в hello Далее команды можно запросить с помощью виртуальной сети hello [фильтр запроса](/cli/azure/query-az-cli2):</span><span class="sxs-lookup"><span data-stu-id="fbff0-132">toolist hello basic information toouse in hello next command, you can query hello VNet using a [query filter](/cli/azure/query-az-cli2):</span></span>

    ```azurecli
    az network vnet list --query '[?name==`TestVNet`].{Where:location,Name:name,Group:resourceGroup}' -o table
    ```

    <span data-ttu-id="fbff0-133">Что порождает hello следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="fbff0-133">Which produces hello following output:</span></span>

        Where      Name      Group

        centralus  TestVNet  TestRG

4. <span data-ttu-id="fbff0-134">Создайте подсеть.</span><span class="sxs-lookup"><span data-stu-id="fbff0-134">Create a subnet:</span></span>

    ```azurecli
    az network vnet subnet create \
    --address-prefix 192.168.2.0/24 \
    --name BackEnd \
    --resource-group TestRG \
    --vnet-name TestVNet
    ```

    <span data-ttu-id="fbff0-135">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="fbff0-135">Expected output:</span></span>

    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid> \"",
    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
    "ipConfigurations": null,
    "name": "BackEnd",
    "networkSecurityGroup": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "TestRG",
    "resourceNavigationLinks": null,
    "routeTable": null
    }
    ```

    <span data-ttu-id="fbff0-136">Используемые параметры:</span><span class="sxs-lookup"><span data-stu-id="fbff0-136">Parameters used:</span></span>

    - <span data-ttu-id="fbff0-137">`--address-prefix 192.168.2.0/24`: блок CIDR подсети.</span><span class="sxs-lookup"><span data-stu-id="fbff0-137">`--address-prefix 192.168.2.0/24`: Subnet CIDR block.</span></span>
    - <span data-ttu-id="fbff0-138">`--name BackEnd`: Имя hello новую подсеть.</span><span class="sxs-lookup"><span data-stu-id="fbff0-138">`--name BackEnd`: Name of hello new subnet.</span></span>
    - <span data-ttu-id="fbff0-139">`--resource-group TestRG`: hello группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="fbff0-139">`--resource-group TestRG`: hello resource group.</span></span>
    - <span data-ttu-id="fbff0-140">`--vnet-name TestVNet`: имя hello hello, которой принадлежит виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="fbff0-140">`--vnet-name TestVNet`: hello name of hello owning VNet.</span></span>

5. <span data-ttu-id="fbff0-141">Свойства запроса hello hello новой виртуальной сети:</span><span class="sxs-lookup"><span data-stu-id="fbff0-141">Query hello properties of hello new VNet:</span></span>

    ```azurecli
    az network vnet show \
    -g TestRG \
    -n TestVNet \
    --query '{Name:name,Where:location,Group:resourceGroup,Status:provisioningState,SubnetCount:subnets | length(@)}' \
    -o table
    ```

    <span data-ttu-id="fbff0-142">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="fbff0-142">Expected output:</span></span>

        Name      Where      Group    Status       SubnetCount

        TestVNet  centralus  TestRG   Succeeded              2

6. <span data-ttu-id="fbff0-143">Свойства запроса hello hello подсетей:</span><span class="sxs-lookup"><span data-stu-id="fbff0-143">Query hello properties of hello subnets:</span></span>

    ```azurecli
    az network vnet subnet list \
    -g TestRG \
    --vnet-name testvnet \
    --query '[].{Name:name,CIDR:addressPrefix,Status:provisioningState}' \
    -o table
    ```

    <span data-ttu-id="fbff0-144">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="fbff0-144">Expected output:</span></span>

        Name      CIDR            Status

        FrontEnd  192.168.1.0/24  Succeeded
        BackEnd   192.168.2.0/24  Succeeded

## <a name="next-steps"></a><span data-ttu-id="fbff0-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fbff0-145">Next steps</span></span>

<span data-ttu-id="fbff0-146">Узнайте, как tooconnect:</span><span class="sxs-lookup"><span data-stu-id="fbff0-146">Learn how tooconnect:</span></span>

- <span data-ttu-id="fbff0-147">Виртуальная сеть виртуальной машины (VM) tooa, считывая hello [создания виртуальной Машины Linux](../virtual-machines/linux/quick-create-cli.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="fbff0-147">A virtual machine (VM) tooa virtual network by reading hello [Create a Linux VM](../virtual-machines/linux/quick-create-cli.md) article.</span></span> <span data-ttu-id="fbff0-148">Вместо создания виртуальной сети и подсети в шагах hello hello статей, можно выбрать существующей виртуальной сети и подсети tooconnect для виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="fbff0-148">Instead of creating a VNet and subnet in hello steps of hello articles, you can select an existing VNet and subnet tooconnect a VM to.</span></span>
- <span data-ttu-id="fbff0-149">Здравствуйте, считывая hello виртуальных сетей в виртуальной сети tooother [подключение виртуальных сетей](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="fbff0-149">hello virtual network tooother virtual networks by reading hello [Connect VNets](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) article.</span></span>
- <span data-ttu-id="fbff0-150">tooan Hello виртуальной сети в локальной сети с помощью виртуальной частной сети сеть сеть (VPN) или канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="fbff0-150">hello virtual network tooan on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="fbff0-151">Дополнительные сведения в разделе hello [подключения локальной сети tooan виртуальной сети с помощью VPN сайтами](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) и [связывание виртуальной сети tooan канал ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="fbff0-151">Learn how by reading hello [Connect a VNet tooan on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet tooan ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span></span>
