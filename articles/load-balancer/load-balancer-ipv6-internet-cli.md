---
title: "Создание подсистемы балансировки нагрузки для Интернета с поддержкой IPv6 с помощью интерфейса командной строки Azure | Документация Майкрософт"
description: "Узнайте, как создать балансировщик нагрузки для Интернета с поддержкой IPv6 в Azure Resource Manager с помощью Azure CLI."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
keywords: "IPv6, Azure Load Balancer, двойной стек, общедоступный IP-адрес, встроенная поддержка Ipv6, мобильное устройство, Интернет вещей"
ms.assetid: a1957c9c-9c1d-423e-9d5c-d71449bc1f37
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: efb4771800c42df544c3cc37d1d164045fdcaf3e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-internet-facing-load-balancer-with-ipv6-in-azure-resource-manager-using-the-azure-cli"></a><span data-ttu-id="6091f-104">Создание балансировщика нагрузки для Интернета с поддержкой IPv6 в Azure Resource Manager с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="6091f-104">Create an Internet facing load balancer with IPv6 in Azure Resource Manager using the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="6091f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6091f-105">PowerShell</span></span>](load-balancer-ipv6-internet-ps.md)
> * [<span data-ttu-id="6091f-106">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="6091f-106">Azure CLI</span></span>](load-balancer-ipv6-internet-cli.md)
> * [<span data-ttu-id="6091f-107">Шаблон</span><span class="sxs-lookup"><span data-stu-id="6091f-107">Template</span></span>](load-balancer-ipv6-internet-template.md)

<span data-ttu-id="6091f-108">Azure Load Balancer является балансировщиком нагрузки 4-го уровня (TCP, UDP).</span><span class="sxs-lookup"><span data-stu-id="6091f-108">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer.</span></span> <span data-ttu-id="6091f-109">Балансировщик нагрузки обеспечивает высокий уровень доступности, распределяя входящий трафик между работоспособными экземплярами службы в облачных службах или виртуальных машинах, определенных в наборе балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="6091f-109">The load balancer provides high availability by distributing incoming traffic among healthy service instances in cloud services or virtual machines in a load balancer set.</span></span> <span data-ttu-id="6091f-110">Azure Load Balancer может также представить данные службы на нескольких портах, нескольких IP-адресах или обоими этими способами.</span><span class="sxs-lookup"><span data-stu-id="6091f-110">Azure Load Balancer can also present those services on multiple ports, multiple IP addresses, or both.</span></span>

## <a name="example-deployment-scenario"></a><span data-ttu-id="6091f-111">Пример сценария развертывания</span><span class="sxs-lookup"><span data-stu-id="6091f-111">Example deployment scenario</span></span>

<span data-ttu-id="6091f-112">На следующей схеме показано решение балансировки нагрузки, которое развертывается в этой статье с помощью примера шаблона.</span><span class="sxs-lookup"><span data-stu-id="6091f-112">The following diagram illustrates the load balancing solution being deployed using the example template described in this article.</span></span>

![Сценарий использования балансировщика нагрузки](./media/load-balancer-ipv6-internet-cli/lb-ipv6-scenario-cli.png)

<span data-ttu-id="6091f-114">В этом сценарии вы создадите следующие ресурсы Azure:</span><span class="sxs-lookup"><span data-stu-id="6091f-114">In this scenario you will create the following Azure resources:</span></span>

* <span data-ttu-id="6091f-115">две виртуальные машины;</span><span class="sxs-lookup"><span data-stu-id="6091f-115">two virtual machines (VMs)</span></span>
* <span data-ttu-id="6091f-116">виртуальный сетевой интерфейс для каждой виртуальной машины с назначенными IPv4 и IPv6-адресами;</span><span class="sxs-lookup"><span data-stu-id="6091f-116">a virtual network interface for each VM with both IPv4 and IPv6 addresses assigned</span></span>
* <span data-ttu-id="6091f-117">балансировщик нагрузки для Интернета с общедоступными IPv4- и IPv6-адресами;</span><span class="sxs-lookup"><span data-stu-id="6091f-117">an Internet-facing Load Balancer with an IPv4 and an IPv6 Public IP address</span></span>
* <span data-ttu-id="6091f-118">группу доступности, которая содержит две виртуальные машины;</span><span class="sxs-lookup"><span data-stu-id="6091f-118">an Availability Set to that contains the two VMs</span></span>
* <span data-ttu-id="6091f-119">два правила балансировки нагрузки для сопоставления общедоступных виртуальных IP-адресов с частными конечными точками.</span><span class="sxs-lookup"><span data-stu-id="6091f-119">two load balancing rules to map the public VIPs to the private endpoints</span></span>

## <a name="deploying-the-solution-using-the-azure-cli"></a><span data-ttu-id="6091f-120">Развертывание решения с помощью интерфейса командной строки Azure (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="6091f-120">Deploying the solution using the Azure CLI</span></span>

<span data-ttu-id="6091f-121">Ниже описана процедура создания балансировщика нагрузки для Интернета с помощью Azure Resource Manager и интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="6091f-121">The following steps show how to create an Internet facing load balancer using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="6091f-122">Azure Resource Manager позволяет по отдельности создавать и настраивать ресурсы, после чего на их основе создается единый ресурс.</span><span class="sxs-lookup"><span data-stu-id="6091f-122">With Azure Resource Manager, each resource is created and configured individually, and then put together to create a resource.</span></span>

<span data-ttu-id="6091f-123">Чтобы развернуть балансировщик нагрузки, необходимо создать и настроить следующие объекты:</span><span class="sxs-lookup"><span data-stu-id="6091f-123">To deploy a load balancer, you create and configure the following objects:</span></span>

* <span data-ttu-id="6091f-124">Конфигурация интерфейсных IP-адресов. Содержит общедоступные IP-адреса для входящего сетевого трафика.</span><span class="sxs-lookup"><span data-stu-id="6091f-124">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="6091f-125">Пул внутренних адресов. Содержит сетевые интерфейсы (сетевые карты) для получения виртуальными машинами трафика от балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="6091f-125">Back-end address pool - contains network interfaces (NICs) for the virtual machines to receive network traffic from the load balancer.</span></span>
* <span data-ttu-id="6091f-126">Правила балансировки нагрузки. Содержат правила сопоставления общего порта в балансировщике нагрузки с портом в пуле внутренних адресов.</span><span class="sxs-lookup"><span data-stu-id="6091f-126">Load balancing rules - contains rules mapping a public port on the load balancer to port in the back-end address pool.</span></span>
* <span data-ttu-id="6091f-127">Правила NAT для входящего трафика. Содержат правила сопоставления общего порта в балансировщике нагрузки с портом на конкретной виртуальной машине в пуле внутренних адресов.</span><span class="sxs-lookup"><span data-stu-id="6091f-127">Inbound NAT rules - contains rules mapping a public port on the load balancer to a port for a specific virtual machine in the back-end address pool.</span></span>
* <span data-ttu-id="6091f-128">Пробы. Содержат пробы работоспособности, с помощью которых можно проверить доступность экземпляров виртуальных машин в пуле внутренних адресов.</span><span class="sxs-lookup"><span data-stu-id="6091f-128">Probes - contains health probes used to check availability of virtual machines instances in the back-end address pool.</span></span>

<span data-ttu-id="6091f-129">Дополнительные сведения см. в статье [Поддержка диспетчера ресурсов Azure для подсистемы балансировки нагрузки](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="6091f-129">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-your-cli-environment-to-use-azure-resource-manager"></a><span data-ttu-id="6091f-130">Настройка среды интерфейса командной строки для использования Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6091f-130">Set up your CLI environment to use Azure Resource Manager</span></span>

<span data-ttu-id="6091f-131">В этом примере программы командной строки выполняются в командном окне PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6091f-131">For this example, we are running the CLI tools in a PowerShell command window.</span></span> <span data-ttu-id="6091f-132">Мы не используем командлеты Azure PowerShell, но применяем возможности сценариев PowerShell для улучшения удобства чтения и повторного использования.</span><span class="sxs-lookup"><span data-stu-id="6091f-132">We are not using the Azure PowerShell cmdlets but we use PowerShell's scripting capabilities to improve readability and reuse.</span></span>

1. <span data-ttu-id="6091f-133">Если вы еще не пользовались Azure CLI, ознакомьтесь со статьей [Установка и настройка CLI Azure](../cli-install-nodejs.md) и следуйте инструкциям вплоть до выбора учетной записи Azure и подписки.</span><span class="sxs-lookup"><span data-stu-id="6091f-133">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="6091f-134">Выполните команду **azure config mode** , чтобы переключиться в режим Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6091f-134">Run the **azure config mode** command to switch to Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="6091f-135">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="6091f-135">Expected output:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="6091f-136">Войдите в Azure и получите список подписок.</span><span class="sxs-lookup"><span data-stu-id="6091f-136">Sign in to Azure and get a list of subscriptions.</span></span>

    ```azurecli
    azure login
    ```

    <span data-ttu-id="6091f-137">При появлении запроса введите свои учетные данные Azure.</span><span class="sxs-lookup"><span data-stu-id="6091f-137">Enter your Azure credentials when prompted.</span></span>

    ```azurecli
    azure account list
    ```

    <span data-ttu-id="6091f-138">Выберите подписку, которая будет использоваться.</span><span class="sxs-lookup"><span data-stu-id="6091f-138">Pick the subscription you want to use.</span></span> <span data-ttu-id="6091f-139">Запишите идентификатор подписки для использования на следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="6091f-139">Make note of the subscription Id for the next step.</span></span>

4. <span data-ttu-id="6091f-140">Настройте переменные PowerShell для использования с командами интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="6091f-140">Set up PowerShell variables for use with the CLI commands.</span></span>

    ```powershell
    $subscriptionid = "########-####-####-####-############"  # enter subscription id
    $location = "southcentralus"
    $rgName = "pscontosorg1southctrlus09152016"
    $vnetName = "contosoIPv4Vnet"
    $vnetPrefix = "10.0.0.0/16"
    $subnet1Name = "clicontosoIPv4Subnet1"
    $subnet1Prefix = "10.0.0.0/24"
    $subnet2Name = "clicontosoIPv4Subnet2"
    $subnet2Prefix = "10.0.1.0/24"
    $dnsLabel = "contoso09152016"
    $lbName = "myIPv4IPv6Lb"
    ```

## <a name="create-a-resource-group-a-load-balancer-a-virtual-network-and-subnets"></a><span data-ttu-id="6091f-141">Создание группы ресурсов, балансировщика нагрузки, виртуальной сети и подсетей</span><span class="sxs-lookup"><span data-stu-id="6091f-141">Create a resource group, a load balancer, a virtual network, and subnets</span></span>

1. <span data-ttu-id="6091f-142">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="6091f-142">Create a resource group</span></span>

    ```azurecli
    azure group create $rgName $location
    ```

2. <span data-ttu-id="6091f-143">Создание балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="6091f-143">Create a load balancer</span></span>

    ```azurecli
    $lb = azure network lb create --resource-group $rgname --location $location --name $lbName
    ```

3. <span data-ttu-id="6091f-144">Создайте виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="6091f-144">Create a virtual network (VNet).</span></span>

    ```azurecli
    $vnet = azure network vnet create  --resource-group $rgname --name $vnetName --location $location --address-prefixes $vnetPrefix
    ```

    <span data-ttu-id="6091f-145">Создайте две подсети в этой виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="6091f-145">Create two subnets in this VNet.</span></span>

    ```azurecli
    $subnet1 = azure network vnet subnet create --resource-group $rgname --name $subnet1Name --address-prefix $subnet1Prefix --vnet-name $vnetName
    $subnet2 = azure network vnet subnet create --resource-group $rgname --name $subnet2Name --address-prefix $subnet2Prefix --vnet-name $vnetName
    ```

## <a name="create-public-ip-addresses-for-the-front-end-pool"></a><span data-ttu-id="6091f-146">Создание общедоступных IP-адресов для интерфейсного пула</span><span class="sxs-lookup"><span data-stu-id="6091f-146">Create public IP addresses for the front-end pool</span></span>

1. <span data-ttu-id="6091f-147">Настройте переменные PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6091f-147">Set up the PowerShell variables</span></span>

    ```powershell
    $publicIpv4Name = "myIPv4Vip"
    $publicIpv6Name = "myIPv6Vip"
    ```

2. <span data-ttu-id="6091f-148">Создайте общедоступный IP-адрес для интерфейсного пула IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="6091f-148">Create a public IP address the front-end IP pool.</span></span>

    ```azurecli
    $publicipV4 = azure network public-ip create --resource-group $rgname --name $publicIpv4Name --location $location --ip-version IPv4 --allocation-method Dynamic --domain-name-label $dnsLabel
    $publicipV6 = azure network public-ip create --resource-group $rgname --name $publicIpv6Name --location $location --ip-version IPv6 --allocation-method Dynamic --domain-name-label $dnsLabel
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="6091f-149">Балансировщик нагрузки использует метку домена общедоступного IP-адреса в качестве своего полного доменного имени (FQDN).</span><span class="sxs-lookup"><span data-stu-id="6091f-149">The load balancer uses the domain label of the public IP as its FQDN.</span></span> <span data-ttu-id="6091f-150">В этом заключается отличие от классического развертывания, при котором в качестве полного доменного имени балансировщика нагрузки используется имя облачной службы.</span><span class="sxs-lookup"><span data-stu-id="6091f-150">This a change from classic deployment, which uses the cloud service name as the load balancer FQDN.</span></span>
    > <span data-ttu-id="6091f-151">В этом примере используется полное доменное имя *contoso09152016.southcentralus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="6091f-151">In this example, the FQDN is *contoso09152016.southcentralus.cloudapp.azure.com*.</span></span>

## <a name="create-front-end-and-back-end-pools"></a><span data-ttu-id="6091f-152">Создание интерфейсного и внутреннего пулов</span><span class="sxs-lookup"><span data-stu-id="6091f-152">Create front-end and back-end pools</span></span>

<span data-ttu-id="6091f-153">В этом примере создается интерфейсный пул IP-адресов, который принимает входящий сетевой трафик в балансировщик нагрузки, а также внутренний пул IP-адресов, куда интерфейсный пул отправляет сетевой трафик с балансировкой нагрузки.</span><span class="sxs-lookup"><span data-stu-id="6091f-153">This example creates the front-end IP pool that receives the incoming network traffic on the load balancer and the back-end IP pool where the front-end pool sends the load balanced network traffic.</span></span>

1. <span data-ttu-id="6091f-154">Настройте переменные PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6091f-154">Set up the PowerShell variables</span></span>

    ```powershell
    $frontendV4Name = "FrontendVipIPv4"
    $frontendV6Name = "FrontendVipIPv6"
    $backendAddressPoolV4Name = "BackendPoolIPv4"
    $backendAddressPoolV6Name = "BackendPoolIPv6"
    ```

2. <span data-ttu-id="6091f-155">Создайте пул интерфейсных IP-адресов, связывающий общедоступный IP-адрес, созданный на предыдущем этапе, и балансировщик нагрузки.</span><span class="sxs-lookup"><span data-stu-id="6091f-155">Create a front-end IP pool associating the public IP created in the previous step and the load balancer.</span></span>

    ```azurecli
    $frontendV4 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV4Name --public-ip-name $publicIpv4Name --lb-name $lbName
    $frontendV6 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV6Name --public-ip-name $publicIpv6Name --lb-name $lbName
    $backendAddressPoolV4 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV4Name --lb-name $lbName
    $backendAddressPoolV6 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV6Name --lb-name $lbName
    ```

## <a name="create-the-probe-nat-rules-and-lb-rules"></a><span data-ttu-id="6091f-156">Создание пробы, правил NAT и правил балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="6091f-156">Create the probe, NAT rules, and LB rules</span></span>

<span data-ttu-id="6091f-157">В этом примере создаются следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="6091f-157">This example creates the following items:</span></span>

* <span data-ttu-id="6091f-158">правило пробы для проверки подключения к TCP-порту 80;</span><span class="sxs-lookup"><span data-stu-id="6091f-158">a probe rule to check for connectivity to TCP port 80</span></span>
* <span data-ttu-id="6091f-159">правило NAT, которое направляет весь входящий трафик с порта 3389 на порт 3389 для RDP<sup>1</sup>;</span><span class="sxs-lookup"><span data-stu-id="6091f-159">a NAT rule to translate all incoming traffic on port 3389 to port 3389 for RDP<sup>1</sup></span></span>
* <span data-ttu-id="6091f-160">правило NAT, которое направляет весь входящий трафик с порта 3391 на порт 3389 для RDP<sup>1</sup>;</span><span class="sxs-lookup"><span data-stu-id="6091f-160">a NAT rule to translate all incoming traffic on port 3391 to port 3389 for RDP<sup>1</sup></span></span>
* <span data-ttu-id="6091f-161">правило балансировщика нагрузки, которое балансирует весь входящий трафик на порту 80, перенаправляя трафик на порт 80 других адресов во внутреннем пуле;</span><span class="sxs-lookup"><span data-stu-id="6091f-161">a load balancer rule to balance all incoming traffic on port 80 to port 80 on the addresses in the back-end pool.</span></span>

<span data-ttu-id="6091f-162"><sup>1</sup> Правила NAT сопоставлены с конкретным экземпляром виртуальной машины, находящимся в зоне действия балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="6091f-162"><sup>1</sup> NAT rules are associated to a specific virtual machine instance behind the load balancer.</span></span> <span data-ttu-id="6091f-163">Сетевой трафик, поступающий на порт 3389, отправляется на определенную виртуальную машину и порт, которые связанны с правилом NAT.</span><span class="sxs-lookup"><span data-stu-id="6091f-163">The network traffic arriving on port 3389 is sent to the specific virtual machine and port associated with the NAT rule.</span></span> <span data-ttu-id="6091f-164">Для правила NAT необходимо указать протокол (UDP или TCP).</span><span class="sxs-lookup"><span data-stu-id="6091f-164">You must specify a protocol (UDP or TCP) for a NAT rule.</span></span> <span data-ttu-id="6091f-165">Нельзя назначить оба протокола одному и тому же порту.</span><span class="sxs-lookup"><span data-stu-id="6091f-165">Both protocols can't be assigned to the same port.</span></span>

1. <span data-ttu-id="6091f-166">Настройте переменные PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6091f-166">Set up the PowerShell variables</span></span>

    ```powershell
    $probeV4V6Name = "ProbeForIPv4AndIPv6"
    $natRule1V4Name = "NatRule-For-Rdp-VM1"
    $natRule2V4Name = "NatRule-For-Rdp-VM2"
    $lbRule1V4Name = "LBRuleForIPv4-Port80"
    $lbRule1V6Name = "LBRuleForIPv6-Port80"
    ```

2. <span data-ttu-id="6091f-167">Создать пробу.</span><span class="sxs-lookup"><span data-stu-id="6091f-167">Create the probe</span></span>

    <span data-ttu-id="6091f-168">В следующем примере создается проба TCP, которая каждые 15 секунд проверяет подключение к внутреннему TCP-порту 80.</span><span class="sxs-lookup"><span data-stu-id="6091f-168">The following example creates a TCP probe that checks for connectivity to back-end TCP port 80 every 15 seconds.</span></span> <span data-ttu-id="6091f-169">После двух последовательных неудавшихся подключений она пометит внутренний ресурс как недоступный.</span><span class="sxs-lookup"><span data-stu-id="6091f-169">It will mark the back-end resource unavailable after two consecutive failures.</span></span>

    ```azurecli
    $probeV4V6 = azure network lb probe create --resource-group $rgname --name $probeV4V6Name --protocol tcp --port 80 --interval 15 --count 2 --lb-name $lbName
    ```

3. <span data-ttu-id="6091f-170">Создайте правила NAT для входящего трафика, позволяющие RDP-подключения к внутренним ресурсам.</span><span class="sxs-lookup"><span data-stu-id="6091f-170">Create inbound NAT rules that allow RDP connections to the back-end resources</span></span>

    ```azurecli
    $inboundNatRuleRdp1 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule1V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3389 --backend-port 3389 --lb-name $lbName
    $inboundNatRuleRdp2 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule2V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3391 --backend-port 3389 --lb-name $lbName
    ```

4. <span data-ttu-id="6091f-171">Создайте правила балансировщика нагрузки, которые отправляют трафик на разные внутренние порты в зависимости от того, какой интерфейс получил запрос.</span><span class="sxs-lookup"><span data-stu-id="6091f-171">Create a load balancer rules that send traffic to different back-end ports depending on which front end received the request</span></span>

    ```azurecli
    $lbruleIPv4 = azure network lb rule create --resource-group $rgname --name $lbRule1V4Name --frontend-ip-name $frontendV4Name --backend-address-pool-name $backendAddressPoolV4Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 80 --lb-name $lbName
    $lbruleIPv6 = azure network lb rule create --resource-group $rgname --name $lbRule1V6Name --frontend-ip-name $frontendV6Name --backend-address-pool-name $backendAddressPoolV6Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 8080 --lb-name $lbName
    ```

5. <span data-ttu-id="6091f-172">Проверьте параметры.</span><span class="sxs-lookup"><span data-stu-id="6091f-172">Check your settings</span></span>

    ```azurecli
    azure network lb show --resource-group $rgName --name $lbName
    ```

    <span data-ttu-id="6091f-173">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="6091f-173">Expected output:</span></span>

        info:    Executing command network lb show
        info:    Looking up the load balancer "myIPv4IPv6Lb"
        data:    Id                              : /subscriptions/########-####-####-####-############/resourceGroups/pscontosorg1southctrlus09152016/providers/Microsoft.Network/loadBalancers/myIPv4IPv6Lb
        data:    Name                            : myIPv4IPv6Lb
        data:    Type                            : Microsoft.Network/loadBalancers
        data:    Location                        : southcentralus
        data:    Provisioning state              : Succeeded
        data:
        data:    Frontend IP configurations:
        data:    Name             Provisioning state  Private IP allocation  Private IP   Subnet  Public IP
        data:    ---------------  ------------------  ---------------------  -----------  ------  ---------
        data:    FrontendVipIPv4  Succeeded           Dynamic                                     myIPv4Vip
        data:    FrontendVipIPv6  Succeeded           Dynamic                                     myIPv6Vip
        data:
        data:    Probes:
        data:    Name                 Provisioning state  Protocol  Port  Path  Interval  Count
        data:    -------------------  ------------------  --------  ----  ----  --------  -----
        data:    ProbeForIPv4AndIPv6  Succeeded           Tcp       80          15        2
        data:
        data:    Backend Address Pools:
        data:    Name             Provisioning state
        data:    ---------------  ------------------
        data:    BackendPoolIPv4  Succeeded
        data:    BackendPoolIPv6  Succeeded
        data:
        data:    Load Balancing Rules:
        data:    Name                  Provisioning state  Load distribution  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes
        data:    --------------------  ------------------  -----------------  --------  -------------  ------------  ------------------  -----------------------
        data:    LBRuleForIPv4-Port80  Succeeded           Default            Tcp       80             80            false               4
        data:    LBRuleForIPv6-Port80  Succeeded           Default            Tcp       80             8080          false               4
        data:
        data:    Inbound NAT Rules:
        data:    Name                 Provisioning state  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes
        data:    -------------------  ------------------  --------  -------------  ------------  ------------------  -----------------------
        data:    NatRule-For-Rdp-VM1  Succeeded           Tcp       3389           3389          false               4
        data:    NatRule-For-Rdp-VM2  Succeeded           Tcp       3391           3389          false               4
        info:    network lb show

## <a name="create-nics"></a><span data-ttu-id="6091f-174">Создание сетевых адаптеров</span><span class="sxs-lookup"><span data-stu-id="6091f-174">Create NICs</span></span>

<span data-ttu-id="6091f-175">Создайте сетевые карты и свяжите их с правилами NAT, правилами балансировщика нагрузки и пробами.</span><span class="sxs-lookup"><span data-stu-id="6091f-175">Create NICs and associate them to NAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="6091f-176">Настройте переменные PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6091f-176">Set up the PowerShell variables</span></span>

    ```powershell
    $nic1Name = "myIPv4IPv6Nic1"
    $nic2Name = "myIPv4IPv6Nic2"
    $subnet1Id = "/subscriptions/$subscriptionid/resourceGroups/$rgName/providers/Microsoft.Network/VirtualNetworks/$vnetName/subnets/$subnet1Name"
    $subnet2Id = "/subscriptions/$subscriptionid/resourceGroups/$rgName/providers/Microsoft.Network/VirtualNetworks/$vnetName/subnets/$subnet2Name"
    $backendAddressPoolV4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/backendAddressPools/$backendAddressPoolV4Name"
    $backendAddressPoolV6Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/backendAddressPools/$backendAddressPoolV6Name"
    $natRule1V4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/inboundNatRules/$natRule1V4Name"
    $natRule2V4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/inboundNatRules/$natRule2V4Name"
    ```

2. <span data-ttu-id="6091f-177">Создайте сетевую карту для каждой серверной части и добавьте конфигурацию IPv6.</span><span class="sxs-lookup"><span data-stu-id="6091f-177">Create a NIC for each back-end and add an IPv6 configuration.</span></span>

    ```azurecli
    $nic1 = azure network nic create --name $nic1Name --resource-group $rgname --location $location --private-ip-version "IPv4" --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule1V4Id
    $nic1IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic1Name

    $nic2 = azure network nic create --name $nic2Name --resource-group $rgname --location $location --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule2V4Id
    $nic2IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic2Name
    ```

## <a name="create-the-back-end-vm-resources-and-attach-each-nic"></a><span data-ttu-id="6091f-178">Создание внутренних ресурсов виртуальных машин и присоединение каждой сетевой карты</span><span class="sxs-lookup"><span data-stu-id="6091f-178">Create the back-end VM resources and attach each NIC</span></span>

<span data-ttu-id="6091f-179">Чтобы создать виртуальные машины, необходима учетная запись хранения.</span><span class="sxs-lookup"><span data-stu-id="6091f-179">To create VMs, you must have a storage account.</span></span> <span data-ttu-id="6091f-180">Для балансировки нагрузки виртуальные машины должны входить в группу доступности.</span><span class="sxs-lookup"><span data-stu-id="6091f-180">For load balancing, the VMs need to be members of an availability set.</span></span> <span data-ttu-id="6091f-181">Дополнительные сведения о создании виртуальных машин см. в статье [Создание виртуальной машины в Azure с помощью PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6091f-181">For more information about creating VMs, see [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span></span>

1. <span data-ttu-id="6091f-182">Настройте переменные PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6091f-182">Set up the PowerShell variables</span></span>

    ```powershell
    $storageAccountName = "ps08092016v6sa0"
    $availabilitySetName = "myIPv4IPv6AvailabilitySet"
    $vm1Name = "myIPv4IPv6VM1"
    $vm2Name = "myIPv4IPv6VM2"
    $nic1Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/networkInterfaces/$nic1Name"
    $nic2Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/networkInterfaces/$nic2Name"
    $disk1Name = "WindowsVMosDisk1"
    $disk2Name = "WindowsVMosDisk2"
    $osDisk1Uri = "https://$storageAccountName.blob.core.windows.net/vhds/$disk1Name.vhd"
    $osDisk2Uri = "https://$storageAccountName.blob.core.windows.net/vhds/$disk2Name.vhd"
    $imageurn "MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest"
    $vmUserName = "vmUser"
    $mySecurePassword = "PlainTextPassword*1"
    ```

    > [!WARNING]
    > <span data-ttu-id="6091f-183">В этом примере для виртуальных машин используются имя пользователя и пароль в виде открытого текста.</span><span class="sxs-lookup"><span data-stu-id="6091f-183">This example uses the username and password for the VMs in clear text.</span></span> <span data-ttu-id="6091f-184">При использовании учетных данных в незашифрованном виде следует принять соответствующие меры предосторожности.</span><span class="sxs-lookup"><span data-stu-id="6091f-184">Appropriate care must be taken when using credentials in the clear.</span></span> <span data-ttu-id="6091f-185">Более безопасный способ обработки учетных данных в PowerShell приводится в описании командлета [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) .</span><span class="sxs-lookup"><span data-stu-id="6091f-185">For a more secure method of handling credentials in PowerShell, see the [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

2. <span data-ttu-id="6091f-186">Создайте учетную запись хранения и группу доступности.</span><span class="sxs-lookup"><span data-stu-id="6091f-186">Create the storage account and availability set</span></span>

    <span data-ttu-id="6091f-187">При создании виртуальных машин можно использовать существующую учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="6091f-187">You may use an existing storage account when you create the VMs.</span></span> <span data-ttu-id="6091f-188">Следующая команда создает учетную запись хранения:</span><span class="sxs-lookup"><span data-stu-id="6091f-188">The following command creates a new storage account.</span></span>

    ```azurecli
    $storageAcc = azure storage account create $storageAccountName --resource-group $rgName --location $location --sku-name "LRS" --kind "Storage"
    ```

    <span data-ttu-id="6091f-189">Теперь создайте группу доступности.</span><span class="sxs-lookup"><span data-stu-id="6091f-189">Next, create the availability set.</span></span>

    ```azurecli
    $availabilitySet = azure availset create --name $availabilitySetName --resource-group $rgName --location $location
    ```

3. <span data-ttu-id="6091f-190">Создайте виртуальные машины со связанными сетевыми картами.</span><span class="sxs-lookup"><span data-stu-id="6091f-190">Create the virtual machines with the associated NICs</span></span>

    ```azurecli
    $vm1 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm1Name --nic-id $nic1Id --os-disk-vhd $osDisk1Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension

    $vm2 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm2Name --nic-id $nic2Id --os-disk-vhd $osDisk2Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension
    ```

## <a name="next-steps"></a><span data-ttu-id="6091f-191">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6091f-191">Next steps</span></span>

[<span data-ttu-id="6091f-192">Приступая к настройке внутренней подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="6091f-192">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-cli.md)

[<span data-ttu-id="6091f-193">Настройка режима распределения подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="6091f-193">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="6091f-194">Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="6091f-194">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
