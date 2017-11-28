---
title: "Создание виртуальной сети (Azure CLI 2.0) | Документация Майкрософт"
description: "Узнайте, как создать виртуальную сеть с помощью Azure CLI 2.0."
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
ms.openlocfilehash: c7d7b3543f488aedff1ea2c68a2b497e0ca744af
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-network-using-the-azure-cli-20"></a><span data-ttu-id="cd641-103">Создание виртуальной сети с помощью Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="cd641-103">Create a virtual network using the Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="cd641-104">Azure предоставляет две модели развертывания: с помощью Azure Resource Manager и классическую.</span><span class="sxs-lookup"><span data-stu-id="cd641-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="cd641-105">Для создания ресурсов корпорация Майкрософт рекомендует использовать модель развертывания с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cd641-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span></span> <span data-ttu-id="cd641-106">Дополнительные сведения о различиях между двумя моделями см. в статье [Azure Resource Manager vs. classic deployment: Understand deployment models and the state of your resources](../azure-resource-manager/resource-manager-deployment-model.md) (Azure Resource Manager и классическое развертывание. Общие сведения о моделях развертывания и состоянии ресурсов).</span><span class="sxs-lookup"><span data-stu-id="cd641-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="cd641-107">Версии интерфейса командной строки для выполнения задачи</span><span class="sxs-lookup"><span data-stu-id="cd641-107">CLI versions to complete the task</span></span>
<span data-ttu-id="cd641-108">Вы можете выполнить задачу, используя одну из следующих версий интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="cd641-108">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="cd641-109">[Azure CLI 1.0](virtual-networks-create-vnet-cli-nodejs.md) — интерфейс командной строки для классической модели развертывания и модели развертывания Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cd641-109">[Azure CLI 1.0](virtual-networks-create-vnet-cli-nodejs.md) – our CLI for the classic and resource management deployment models</span></span>
- <span data-ttu-id="cd641-110">[Azure CLI 2.0](#create-a-virtual-network) — это интерфейс командной строки нового поколения для модели развертывания Resource Manager (описывается в этой статье).</span><span class="sxs-lookup"><span data-stu-id="cd641-110">[Azure CLI 2.0](#create-a-virtual-network) - our next generation CLI for the resource management deployment model (this article)\`</span></span>
 
    <span data-ttu-id="cd641-111">Виртуальную сеть также можно создать с помощью Resource Manager, используя другие инструменты, либо с помощью классической модели развертывания, выбрав другой вариант из следующего списка:</span><span class="sxs-lookup"><span data-stu-id="cd641-111">You can also create a VNet through Resource Manager using other tools or create a VNet through the classic deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="cd641-112">Портал</span><span class="sxs-lookup"><span data-stu-id="cd641-112">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
> * [<span data-ttu-id="cd641-113">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cd641-113">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
> * [<span data-ttu-id="cd641-114">ИНТЕРФЕЙС КОМАНДНОЙ СТРОКИ</span><span class="sxs-lookup"><span data-stu-id="cd641-114">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
> * [<span data-ttu-id="cd641-115">Шаблон</span><span class="sxs-lookup"><span data-stu-id="cd641-115">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
> * [<span data-ttu-id="cd641-116">Портал (классический)</span><span class="sxs-lookup"><span data-stu-id="cd641-116">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
> * [<span data-ttu-id="cd641-117">PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="cd641-117">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [<span data-ttu-id="cd641-118">Интерфейс командной строки (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="cd641-118">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]


## <a name="create-a-virtual-network"></a><span data-ttu-id="cd641-119">Создать виртуальную сеть</span><span class="sxs-lookup"><span data-stu-id="cd641-119">Create a virtual network</span></span>

<span data-ttu-id="cd641-120">Чтобы создать виртуальную сеть с помощью Azure CLI 2.0, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="cd641-120">To create a virtual network using the Azure CLI 2.0, complete the following steps:</span></span>

1. <span data-ttu-id="cd641-121">Установите и настройте последнюю версию [Azure CLI 2.0](/cli/azure/install-az-cli2), а затем войдите в учетную запись Azure, выполнив команду [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="cd641-121">Install and configure the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span>

2. <span data-ttu-id="cd641-122">Создайте группу ресурсов для виртуальной сети, выполнив команду [az group create](/cli/azure/group#create) с аргументами `--name` и `--location`.</span><span class="sxs-lookup"><span data-stu-id="cd641-122">Create a resource group for your VNet using the [az group create](/cli/azure/group#create) command with the `--name` and `--location` arguments:</span></span>

    ```azurecli
    az group create --name TestRG --location centralus
    ```

3. <span data-ttu-id="cd641-123">Создайте виртуальную сеть и подсеть.</span><span class="sxs-lookup"><span data-stu-id="cd641-123">Create a VNet and a subnet:</span></span>

    ```azurecli
    az network vnet create \
    --name TestVNet \
    --resource-group TestRG \
    --location centralus \
    --address-prefix 192.168.0.0/16 \
    --subnet-name FrontEnd \
    --subnet-prefix 192.168.1.0/24
    ```

    <span data-ttu-id="cd641-124">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="cd641-124">Expected output:</span></span>
    
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

    <span data-ttu-id="cd641-125">Используемые параметры:</span><span class="sxs-lookup"><span data-stu-id="cd641-125">Parameters used:</span></span>

    - <span data-ttu-id="cd641-126">`--name TestVNet`: имя виртуальной сети, которую нужно будет создать.</span><span class="sxs-lookup"><span data-stu-id="cd641-126">`--name TestVNet`: Name of the VNet to be created.</span></span>
    - <span data-ttu-id="cd641-127">`--resource-group TestRG`: имя группы ресурсов, которая управляет ресурсом.</span><span class="sxs-lookup"><span data-stu-id="cd641-127">`--resource-group TestRG`: # The resource group name that controls the resource.</span></span> 
    - <span data-ttu-id="cd641-128">`--location centralus`: расположение для развертывания.</span><span class="sxs-lookup"><span data-stu-id="cd641-128">`--location centralus`: The location into which to deploy.</span></span>
    - <span data-ttu-id="cd641-129">`--address-prefix 192.168.0.0/16`: префикс и блок адреса.</span><span class="sxs-lookup"><span data-stu-id="cd641-129">`--address-prefix 192.168.0.0/16`: The address prefix and block.</span></span>  
    - <span data-ttu-id="cd641-130">`--subnet-name FrontEnd`: имя подсети.</span><span class="sxs-lookup"><span data-stu-id="cd641-130">`--subnet-name FrontEnd`: The name of the subnet.</span></span>
    - <span data-ttu-id="cd641-131">`--subnet-prefix 192.168.1.0/24`: префикс и блок адреса.</span><span class="sxs-lookup"><span data-stu-id="cd641-131">`--subnet-prefix 192.168.1.0/24`: The address prefix and block.</span></span>

    <span data-ttu-id="cd641-132">Чтобы вывести на экран основные данные, которые используются в следующей команде, можно отправить запрос к виртуальной сети с помощью [фильтра запроса](/cli/azure/query-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="cd641-132">To list the basic information to use in the next command, you can query the VNet using a [query filter](/cli/azure/query-az-cli2):</span></span>

    ```azurecli
    az network vnet list --query '[?name==`TestVNet`].{Where:location,Name:name,Group:resourceGroup}' -o table
    ```

    <span data-ttu-id="cd641-133">В результате будут возвращены следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="cd641-133">Which produces the following output:</span></span>

        Where      Name      Group

        centralus  TestVNet  TestRG

4. <span data-ttu-id="cd641-134">Создайте подсеть.</span><span class="sxs-lookup"><span data-stu-id="cd641-134">Create a subnet:</span></span>

    ```azurecli
    az network vnet subnet create \
    --address-prefix 192.168.2.0/24 \
    --name BackEnd \
    --resource-group TestRG \
    --vnet-name TestVNet
    ```

    <span data-ttu-id="cd641-135">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="cd641-135">Expected output:</span></span>

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

    <span data-ttu-id="cd641-136">Используемые параметры:</span><span class="sxs-lookup"><span data-stu-id="cd641-136">Parameters used:</span></span>

    - <span data-ttu-id="cd641-137">`--address-prefix 192.168.2.0/24`: блок CIDR подсети.</span><span class="sxs-lookup"><span data-stu-id="cd641-137">`--address-prefix 192.168.2.0/24`: Subnet CIDR block.</span></span>
    - <span data-ttu-id="cd641-138">`--name BackEnd`: имя новой подсети.</span><span class="sxs-lookup"><span data-stu-id="cd641-138">`--name BackEnd`: Name of the new subnet.</span></span>
    - <span data-ttu-id="cd641-139">`--resource-group TestRG`: группа ресурсов.</span><span class="sxs-lookup"><span data-stu-id="cd641-139">`--resource-group TestRG`: The resource group.</span></span>
    - <span data-ttu-id="cd641-140">`--vnet-name TestVNet`: имя виртуальной сети, в которую входит подсеть.</span><span class="sxs-lookup"><span data-stu-id="cd641-140">`--vnet-name TestVNet`: The name of the owning VNet.</span></span>

5. <span data-ttu-id="cd641-141">Запросите свойства новой виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="cd641-141">Query the properties of the new VNet:</span></span>

    ```azurecli
    az network vnet show \
    -g TestRG \
    -n TestVNet \
    --query '{Name:name,Where:location,Group:resourceGroup,Status:provisioningState,SubnetCount:subnets | length(@)}' \
    -o table
    ```

    <span data-ttu-id="cd641-142">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="cd641-142">Expected output:</span></span>

        Name      Where      Group    Status       SubnetCount

        TestVNet  centralus  TestRG   Succeeded              2

6. <span data-ttu-id="cd641-143">Запросите свойства подсетей.</span><span class="sxs-lookup"><span data-stu-id="cd641-143">Query the properties of the subnets:</span></span>

    ```azurecli
    az network vnet subnet list \
    -g TestRG \
    --vnet-name testvnet \
    --query '[].{Name:name,CIDR:addressPrefix,Status:provisioningState}' \
    -o table
    ```

    <span data-ttu-id="cd641-144">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="cd641-144">Expected output:</span></span>

        Name      CIDR            Status

        FrontEnd  192.168.1.0/24  Succeeded
        BackEnd   192.168.2.0/24  Succeeded

## <a name="next-steps"></a><span data-ttu-id="cd641-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cd641-145">Next steps</span></span>

<span data-ttu-id="cd641-146">Инструкции по подключению:</span><span class="sxs-lookup"><span data-stu-id="cd641-146">Learn how to connect:</span></span>

- <span data-ttu-id="cd641-147">Сведения о подключении виртуальной машины к виртуальной сети см. в статье о [создании виртуальной машины Linux](../virtual-machines/linux/quick-create-cli.md).</span><span class="sxs-lookup"><span data-stu-id="cd641-147">A virtual machine (VM) to a virtual network by reading the [Create a Linux VM](../virtual-machines/linux/quick-create-cli.md) article.</span></span> <span data-ttu-id="cd641-148">Вместо создания виртуальной сети и подсети с помощью действий, описанных в этой статье, виртуальную машину можно подключить к имеющейся виртуальной сети и подсети.</span><span class="sxs-lookup"><span data-stu-id="cd641-148">Instead of creating a VNet and subnet in the steps of the articles, you can select an existing VNet and subnet to connect a VM to.</span></span>
- <span data-ttu-id="cd641-149">Сведения об установке подключения между виртуальными сетями см. в статье [Настройка подключения между виртуальными сетями на портале Azure](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="cd641-149">The virtual network to other virtual networks by reading the [Connect VNets](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) article.</span></span>
- <span data-ttu-id="cd641-150">Сведения о подключении виртуальной сети к локальной сети с использованием виртуальной частной сети типа "сеть — сеть" или канала ExpressRoute см. в</span><span class="sxs-lookup"><span data-stu-id="cd641-150">The virtual network to an on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="cd641-151">статьях [Добавление подключения типа "сеть — сеть" к виртуальной сети с помощью существующего подключения VPN-шлюза](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) и [Подключение виртуальной сети к каналу ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="cd641-151">Learn how by reading the [Connect a VNet to an on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet to an ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span></span>