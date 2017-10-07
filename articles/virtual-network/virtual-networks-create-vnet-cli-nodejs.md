---
title: "Здравствуйте, aaaCreate виртуальной сети с помощью Azure CLI 1.0 | Документы Microsoft"
description: "Узнайте, как toocreate виртуальной сети с помощью hello Azure CLI 1.0 | Диспетчер ресурсов."
services: virtual-network
documentationcenter: 
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: jdial
ms.openlocfilehash: f48a8b23a5994164b71c9b51ee8a6810d17f9392
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-hello-azure-cli"></a><span data-ttu-id="84bc0-103">Создание виртуальной сети с помощью hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="84bc0-103">Create a virtual network using hello Azure CLI</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="84bc0-104">Azure предоставляет две модели развертывания: с помощью Azure Resource Manager и классическую.</span><span class="sxs-lookup"><span data-stu-id="84bc0-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="84bc0-105">Корпорация Майкрософт рекомендует создать ресурсы с помощью модели развертывания диспетчера ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="84bc0-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="84bc0-106">Дополнительные сведения о toolearn hello различий между моделями hello двух чтения hello [модели развертывания Azure понять](../azure-resource-manager/resource-manager-deployment-model.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="84bc0-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="84bc0-107">Задача hello toocomplete версии CLI</span><span class="sxs-lookup"><span data-stu-id="84bc0-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="84bc0-108">Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.</span><span class="sxs-lookup"><span data-stu-id="84bc0-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="84bc0-109">[Azure CLI 2.0](virtual-networks-create-vnet-arm-cli.md) -нашей нового поколения CLI для модели развертывания hello ресурсов управления</span><span class="sxs-lookup"><span data-stu-id="84bc0-109">[Azure CLI 2.0](virtual-networks-create-vnet-arm-cli.md) - our next generation CLI for hello resource management deployment model</span></span>
- <span data-ttu-id="84bc0-110">[Azure CLI 1.0](#create-a-virtual-network) — нашей CLI для hello классический и ресурса управления развертывания моделей (в этой статье)</span><span class="sxs-lookup"><span data-stu-id="84bc0-110">[Azure CLI 1.0](#create-a-virtual-network) – our CLI for hello classic and resource management deployment models (this article)</span></span>

 
[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a><span data-ttu-id="84bc0-111">Создать виртуальную сеть</span><span class="sxs-lookup"><span data-stu-id="84bc0-111">Create a virtual network</span></span>

<span data-ttu-id="84bc0-112">в виртуальной сети с помощью toocreate hello Azure CLI, полный hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="84bc0-112">toocreate a virtual network using hello Azure CLI, complete hello following steps:</span></span>

1. <span data-ttu-id="84bc0-113">Установка и настройка hello Azure CLI, hello следующие шаги в hello [Установка и настройка hello Azure CLI](../cli-install-nodejs.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="84bc0-113">Install and configure hello Azure CLI by following hello steps in hello [Install and Configure hello Azure CLI](../cli-install-nodejs.md) article.</span></span>

2. <span data-ttu-id="84bc0-114">Создайте виртуальную сеть и подсеть.</span><span class="sxs-lookup"><span data-stu-id="84bc0-114">Create a VNet and a subnet:</span></span>

    ```azurecli
    azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
    ```

    <span data-ttu-id="84bc0-115">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="84bc0-115">Expected output:</span></span>
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK

    <span data-ttu-id="84bc0-116">Используемые параметры:</span><span class="sxs-lookup"><span data-stu-id="84bc0-116">Parameters used:</span></span>

   * <span data-ttu-id="84bc0-117">**--vnet**.</span><span class="sxs-lookup"><span data-stu-id="84bc0-117">**--vnet**.</span></span> <span data-ttu-id="84bc0-118">Имя создания toobe виртуальной сети hello.</span><span class="sxs-lookup"><span data-stu-id="84bc0-118">Name of hello VNet toobe created.</span></span> <span data-ttu-id="84bc0-119">В данном сценарии это *TestVNet*</span><span class="sxs-lookup"><span data-stu-id="84bc0-119">For our scenario, *TestVNet*</span></span>
   * <span data-ttu-id="84bc0-120">**-e (или --address-space)**.</span><span class="sxs-lookup"><span data-stu-id="84bc0-120">**-e (or --address-space)**.</span></span> <span data-ttu-id="84bc0-121">Адресное пространство виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="84bc0-121">VNet address space.</span></span> <span data-ttu-id="84bc0-122">В данном сценарии это *192.168.0.0*</span><span class="sxs-lookup"><span data-stu-id="84bc0-122">For our scenario, *192.168.0.0*</span></span>
   * <span data-ttu-id="84bc0-123">**-i (или -cidr)**.</span><span class="sxs-lookup"><span data-stu-id="84bc0-123">**-i (or -cidr)**.</span></span> <span data-ttu-id="84bc0-124">Маска подсети в формате CIDR.</span><span class="sxs-lookup"><span data-stu-id="84bc0-124">Network mask in CIDR format.</span></span> <span data-ttu-id="84bc0-125">В данном сценарии это *16*.</span><span class="sxs-lookup"><span data-stu-id="84bc0-125">For our scenario, *16*.</span></span>
   * <span data-ttu-id="84bc0-126">**-n (или --subnet-name**).</span><span class="sxs-lookup"><span data-stu-id="84bc0-126">**-n (or --subnet-name**).</span></span> <span data-ttu-id="84bc0-127">Имя первой подсети hello.</span><span class="sxs-lookup"><span data-stu-id="84bc0-127">Name of hello first subnet.</span></span> <span data-ttu-id="84bc0-128">В данном сценарии это *FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="84bc0-128">For our scenario, *FrontEnd*.</span></span>
   * <span data-ttu-id="84bc0-129">**-p (или --subnet-start-ip)**.</span><span class="sxs-lookup"><span data-stu-id="84bc0-129">**-p (or --subnet-start-ip)**.</span></span> <span data-ttu-id="84bc0-130">Начальный IP-адрес для подсети или адресное пространство подсети.</span><span class="sxs-lookup"><span data-stu-id="84bc0-130">Starting IP address for subnet, or subnet address space.</span></span> <span data-ttu-id="84bc0-131">В нашем сценарии это *192.168.1.0*.</span><span class="sxs-lookup"><span data-stu-id="84bc0-131">For our scenario, *192.168.1.0*.</span></span>
   * <span data-ttu-id="84bc0-132">**-r (или --subnet-cidr)**.</span><span class="sxs-lookup"><span data-stu-id="84bc0-132">**-r (or --subnet-cidr)**.</span></span> <span data-ttu-id="84bc0-133">Маска подсети в формате CIDR для подсети.</span><span class="sxs-lookup"><span data-stu-id="84bc0-133">Network mask in CIDR format for subnet.</span></span> <span data-ttu-id="84bc0-134">В данном сценарии это *24*.</span><span class="sxs-lookup"><span data-stu-id="84bc0-134">For our scenario, *24*.</span></span>
   * <span data-ttu-id="84bc0-135">**-l (или --location)**.</span><span class="sxs-lookup"><span data-stu-id="84bc0-135">**-l (or --location)**.</span></span> <span data-ttu-id="84bc0-136">Регион Azure, где создается hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="84bc0-136">Azure region where hello VNet is created.</span></span> <span data-ttu-id="84bc0-137">В данном сценарии это *Central US*.</span><span class="sxs-lookup"><span data-stu-id="84bc0-137">For our scenario, *Central US*.</span></span>

3. <span data-ttu-id="84bc0-138">Создайте подсеть.</span><span class="sxs-lookup"><span data-stu-id="84bc0-138">Create a subnet:</span></span>

    ```azurecli
    azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
    ```
   
    <span data-ttu-id="84bc0-139">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="84bc0-139">Expected output:</span></span>

            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up hello subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK

    <span data-ttu-id="84bc0-140">Используемые параметры:</span><span class="sxs-lookup"><span data-stu-id="84bc0-140">Parameters used:</span></span>

   * <span data-ttu-id="84bc0-141">**-t (или --vnet-name**.</span><span class="sxs-lookup"><span data-stu-id="84bc0-141">**-t (or --vnet-name**.</span></span> <span data-ttu-id="84bc0-142">Имя виртуальной сети, где будут создаваться подсети hello hello.</span><span class="sxs-lookup"><span data-stu-id="84bc0-142">Name of hello VNet where hello subnet will be created.</span></span> <span data-ttu-id="84bc0-143">В данном сценарии это *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="84bc0-143">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="84bc0-144">**-n (или --name)**.</span><span class="sxs-lookup"><span data-stu-id="84bc0-144">**-n (or --name)**.</span></span> <span data-ttu-id="84bc0-145">Имя новой подсети hello.</span><span class="sxs-lookup"><span data-stu-id="84bc0-145">Name of hello new subnet.</span></span> <span data-ttu-id="84bc0-146">В нашем сценарии это *BackEnd*.</span><span class="sxs-lookup"><span data-stu-id="84bc0-146">For our scenario, *BackEnd*.</span></span>
   * <span data-ttu-id="84bc0-147">**-a (или --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="84bc0-147">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="84bc0-148">Блок подсети CIDR.</span><span class="sxs-lookup"><span data-stu-id="84bc0-148">Subnet CIDR block.</span></span> <span data-ttu-id="84bc0-149">В данном сценарии это *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="84bc0-149">Four our scenario, *192.168.2.0/24*.</span></span>
   
4. <span data-ttu-id="84bc0-150">свойства hello tooview hello новой виртуальной сети:</span><span class="sxs-lookup"><span data-stu-id="84bc0-150">tooview hello properties of hello new VNet:</span></span>

    ```azurecli
    azure network vnet show
    ```
   
    <span data-ttu-id="84bc0-151">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="84bc0-151">Expected output:</span></span>
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up hello virtual network sites
            data:    Name                            : TestVNet
            data:    Location                        : Central US
            data:    State                           : Created
            data:    Address space                   : 192.168.0.0/16
            data:    Subnets:
            data:      Name                          : FrontEnd
            data:      Address prefix                : 192.168.1.0/24
            data:
            data:      Name                          : BackEnd
            data:      Address prefix                : 192.168.2.0/24
            data:
            info:    network vnet show command OK

## <a name="next-steps"></a><span data-ttu-id="84bc0-152">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="84bc0-152">Next steps</span></span>

<span data-ttu-id="84bc0-153">Узнайте, как tooconnect:</span><span class="sxs-lookup"><span data-stu-id="84bc0-153">Learn how tooconnect:</span></span>

- <span data-ttu-id="84bc0-154">Виртуальная сеть виртуальной машины (VM) tooa, считывая hello [создания виртуальной Машины Linux](../virtual-machines/linux/quick-create-cli.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="84bc0-154">A virtual machine (VM) tooa virtual network by reading hello [Create a Linux VM](../virtual-machines/linux/quick-create-cli.md) article.</span></span> <span data-ttu-id="84bc0-155">Вместо создания виртуальной сети и подсети в шагах hello hello статей, можно выбрать существующей виртуальной сети и подсети tooconnect для виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="84bc0-155">Instead of creating a VNet and subnet in hello steps of hello articles, you can select an existing VNet and subnet tooconnect a VM to.</span></span>
- <span data-ttu-id="84bc0-156">Здравствуйте, считывая hello виртуальных сетей в виртуальной сети tooother [подключение виртуальных сетей](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="84bc0-156">hello virtual network tooother virtual networks by reading hello [Connect VNets](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) article.</span></span>
- <span data-ttu-id="84bc0-157">tooan Hello виртуальной сети в локальной сети с помощью виртуальной частной сети сеть сеть (VPN) или канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="84bc0-157">hello virtual network tooan on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="84bc0-158">Дополнительные сведения в разделе hello [подключения локальной сети tooan виртуальной сети с помощью VPN сайтами](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) и [связывание виртуальной сети tooan канал ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="84bc0-158">Learn how by reading hello [Connect a VNet tooan on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet tooan ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span></span>
