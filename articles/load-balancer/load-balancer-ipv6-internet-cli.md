---
title: "Подсистема балансировки нагрузки aaaCreate с выходом в Интернет с IPv6 - Azure CLI | Документы Microsoft"
description: "Узнайте, как toocreate Интернета с выходом подсистемы балансировки нагрузки с IPv6 с помощью диспетчера ресурсов Azure hello Azure CLI"
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
ms.openlocfilehash: 7ff75ac90d74a74e3d0c27672b36fbd955a086a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internet-facing-load-balancer-with-ipv6-in-azure-resource-manager-using-hello-azure-cli"></a><span data-ttu-id="fa08f-104">Создание подсистемы балансировки нагрузки с IPv6 в диспетчере ресурсов Azure с помощью hello Azure CLI с выходом в Интернет</span><span class="sxs-lookup"><span data-stu-id="fa08f-104">Create an Internet facing load balancer with IPv6 in Azure Resource Manager using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="fa08f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fa08f-105">PowerShell</span></span>](load-balancer-ipv6-internet-ps.md)
> * [<span data-ttu-id="fa08f-106">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="fa08f-106">Azure CLI</span></span>](load-balancer-ipv6-internet-cli.md)
> * [<span data-ttu-id="fa08f-107">Шаблон</span><span class="sxs-lookup"><span data-stu-id="fa08f-107">Template</span></span>](load-balancer-ipv6-internet-template.md)

<span data-ttu-id="fa08f-108">Azure Load Balancer является балансировщиком нагрузки 4-го уровня (TCP, UDP).</span><span class="sxs-lookup"><span data-stu-id="fa08f-108">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer.</span></span> <span data-ttu-id="fa08f-109">Подсистема балансировки нагрузки Hello обеспечивает высокую доступность путем распределения входящего трафика между экземплярами службы работоспособности в облачных службах или виртуальных машин в набор балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="fa08f-109">hello load balancer provides high availability by distributing incoming traffic among healthy service instances in cloud services or virtual machines in a load balancer set.</span></span> <span data-ttu-id="fa08f-110">Azure Load Balancer может также представить данные службы на нескольких портах, нескольких IP-адресах или обоими этими способами.</span><span class="sxs-lookup"><span data-stu-id="fa08f-110">Azure Load Balancer can also present those services on multiple ports, multiple IP addresses, or both.</span></span>

## <a name="example-deployment-scenario"></a><span data-ttu-id="fa08f-111">Пример сценария развертывания</span><span class="sxs-lookup"><span data-stu-id="fa08f-111">Example deployment scenario</span></span>

<span data-ttu-id="fa08f-112">Hello следующей схеме показано решение по балансировке нагрузки hello развертываемого с помощью шаблона пример hello, описанных в этой статье.</span><span class="sxs-lookup"><span data-stu-id="fa08f-112">hello following diagram illustrates hello load balancing solution being deployed using hello example template described in this article.</span></span>

![Сценарий использования балансировщика нагрузки](./media/load-balancer-ipv6-internet-cli/lb-ipv6-scenario-cli.png)

<span data-ttu-id="fa08f-114">В этом случае будут созданы следующие ресурсы Azure hello:</span><span class="sxs-lookup"><span data-stu-id="fa08f-114">In this scenario you will create hello following Azure resources:</span></span>

* <span data-ttu-id="fa08f-115">две виртуальные машины;</span><span class="sxs-lookup"><span data-stu-id="fa08f-115">two virtual machines (VMs)</span></span>
* <span data-ttu-id="fa08f-116">виртуальный сетевой интерфейс для каждой виртуальной машины с назначенными IPv4 и IPv6-адресами;</span><span class="sxs-lookup"><span data-stu-id="fa08f-116">a virtual network interface for each VM with both IPv4 and IPv6 addresses assigned</span></span>
* <span data-ttu-id="fa08f-117">балансировщик нагрузки для Интернета с общедоступными IPv4- и IPv6-адресами;</span><span class="sxs-lookup"><span data-stu-id="fa08f-117">an Internet-facing Load Balancer with an IPv4 and an IPv6 Public IP address</span></span>
* <span data-ttu-id="fa08f-118">Группа доступности toothat содержит hello две виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="fa08f-118">an Availability Set toothat contains hello two VMs</span></span>
* <span data-ttu-id="fa08f-119">два загрузить балансировки правила toomap hello открытые виртуальные IP-адреса toohello закрытый конечные точки</span><span class="sxs-lookup"><span data-stu-id="fa08f-119">two load balancing rules toomap hello public VIPs toohello private endpoints</span></span>

## <a name="deploying-hello-solution-using-hello-azure-cli"></a><span data-ttu-id="fa08f-120">Развертывание решения hello, с помощью hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="fa08f-120">Deploying hello solution using hello Azure CLI</span></span>

<span data-ttu-id="fa08f-121">Привет, следующие шаги показывают, как с помощью диспетчера ресурсов Azure с CLI подсистемы балансировки нагрузки, toocreate из Интернета.</span><span class="sxs-lookup"><span data-stu-id="fa08f-121">hello following steps show how toocreate an Internet facing load balancer using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="fa08f-122">С помощью диспетчера ресурсов Azure каждый ресурс создается и настроить отдельно и затем поместить toocreate ресурса.</span><span class="sxs-lookup"><span data-stu-id="fa08f-122">With Azure Resource Manager, each resource is created and configured individually, and then put together toocreate a resource.</span></span>

<span data-ttu-id="fa08f-123">toodeploy подсистемы балансировки нагрузки, создания и настройки hello следующие объекты:</span><span class="sxs-lookup"><span data-stu-id="fa08f-123">toodeploy a load balancer, you create and configure hello following objects:</span></span>

* <span data-ttu-id="fa08f-124">Конфигурация интерфейсных IP-адресов. Содержит общедоступные IP-адреса для входящего сетевого трафика.</span><span class="sxs-lookup"><span data-stu-id="fa08f-124">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="fa08f-125">Пул адресов серверной части - содержит сетевых интерфейсов (NIC) для hello виртуальные машины tooreceive сетевой трафик от подсистемы балансировки нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="fa08f-125">Back-end address pool - contains network interfaces (NICs) for hello virtual machines tooreceive network traffic from hello load balancer.</span></span>
* <span data-ttu-id="fa08f-126">Правила балансировки нагрузки — содержит правила сопоставления открытый порт hello tooport подсистемы балансировки нагрузки в пул адресов серверной части hello.</span><span class="sxs-lookup"><span data-stu-id="fa08f-126">Load balancing rules - contains rules mapping a public port on hello load balancer tooport in hello back-end address pool.</span></span>
* <span data-ttu-id="fa08f-127">Правила NAT для входящих подключений — содержит правила, сопоставление порта открытый порт tooa подсистемы балансировки нагрузки hello для конкретной виртуальной машины в пул адресов серверной части hello.</span><span class="sxs-lookup"><span data-stu-id="fa08f-127">Inbound NAT rules - contains rules mapping a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool.</span></span>
* <span data-ttu-id="fa08f-128">Проверяет — содержит доступность toocheck проверки, используемые работоспособности экземпляров виртуальных машин в пул адресов серверной части hello.</span><span class="sxs-lookup"><span data-stu-id="fa08f-128">Probes - contains health probes used toocheck availability of virtual machines instances in hello back-end address pool.</span></span>

<span data-ttu-id="fa08f-129">Дополнительные сведения см. в статье [Поддержка диспетчера ресурсов Azure для подсистемы балансировки нагрузки](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="fa08f-129">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-your-cli-environment-toouse-azure-resource-manager"></a><span data-ttu-id="fa08f-130">Настройка вашей toouse среды интерфейс командной строки диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="fa08f-130">Set up your CLI environment toouse Azure Resource Manager</span></span>

<span data-ttu-id="fa08f-131">В этом примере мы запущены средства CLI hello в окне команд PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fa08f-131">For this example, we are running hello CLI tools in a PowerShell command window.</span></span> <span data-ttu-id="fa08f-132">Командлеты Azure PowerShell hello не используются, но мы используем PowerShell сценариев возможности tooimprove удобочитаемость и повторного использования.</span><span class="sxs-lookup"><span data-stu-id="fa08f-132">We are not using hello Azure PowerShell cmdlets but we use PowerShell's scripting capabilities tooimprove readability and reuse.</span></span>

1. <span data-ttu-id="fa08f-133">Если ранее не пользовались Azure CLI, см. раздел [Установка и настройка hello Azure CLI](../cli-install-nodejs.md) и следуйте инструкциям hello toohello точку, где выбирается учетная запись Azure и подписки.</span><span class="sxs-lookup"><span data-stu-id="fa08f-133">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="fa08f-134">Запустите hello **azure конфигурации режима** режим Manager tooResource tooswitch команд.</span><span class="sxs-lookup"><span data-stu-id="fa08f-134">Run hello **azure config mode** command tooswitch tooResource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="fa08f-135">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="fa08f-135">Expected output:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="fa08f-136">Войдите в tooAzure и получить список подписок.</span><span class="sxs-lookup"><span data-stu-id="fa08f-136">Sign in tooAzure and get a list of subscriptions.</span></span>

    ```azurecli
    azure login
    ```

    <span data-ttu-id="fa08f-137">При появлении запроса введите свои учетные данные Azure.</span><span class="sxs-lookup"><span data-stu-id="fa08f-137">Enter your Azure credentials when prompted.</span></span>

    ```azurecli
    azure account list
    ```

    <span data-ttu-id="fa08f-138">Выберите подписку hello toouse.</span><span class="sxs-lookup"><span data-stu-id="fa08f-138">Pick hello subscription you want toouse.</span></span> <span data-ttu-id="fa08f-139">Запишите идентификатор hello подписки для следующего шага hello.</span><span class="sxs-lookup"><span data-stu-id="fa08f-139">Make note of hello subscription Id for hello next step.</span></span>

4. <span data-ttu-id="fa08f-140">Настройка переменных PowerShell для использования с командами CLI hello.</span><span class="sxs-lookup"><span data-stu-id="fa08f-140">Set up PowerShell variables for use with hello CLI commands.</span></span>

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

## <a name="create-a-resource-group-a-load-balancer-a-virtual-network-and-subnets"></a><span data-ttu-id="fa08f-141">Создание группы ресурсов, балансировщика нагрузки, виртуальной сети и подсетей</span><span class="sxs-lookup"><span data-stu-id="fa08f-141">Create a resource group, a load balancer, a virtual network, and subnets</span></span>

1. <span data-ttu-id="fa08f-142">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="fa08f-142">Create a resource group</span></span>

    ```azurecli
    azure group create $rgName $location
    ```

2. <span data-ttu-id="fa08f-143">Создание балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="fa08f-143">Create a load balancer</span></span>

    ```azurecli
    $lb = azure network lb create --resource-group $rgname --location $location --name $lbName
    ```

3. <span data-ttu-id="fa08f-144">Создайте виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="fa08f-144">Create a virtual network (VNet).</span></span>

    ```azurecli
    $vnet = azure network vnet create  --resource-group $rgname --name $vnetName --location $location --address-prefixes $vnetPrefix
    ```

    <span data-ttu-id="fa08f-145">Создайте две подсети в этой виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="fa08f-145">Create two subnets in this VNet.</span></span>

    ```azurecli
    $subnet1 = azure network vnet subnet create --resource-group $rgname --name $subnet1Name --address-prefix $subnet1Prefix --vnet-name $vnetName
    $subnet2 = azure network vnet subnet create --resource-group $rgname --name $subnet2Name --address-prefix $subnet2Prefix --vnet-name $vnetName
    ```

## <a name="create-public-ip-addresses-for-hello-front-end-pool"></a><span data-ttu-id="fa08f-146">Создание общих IP-адресов для пула переднего плана hello</span><span class="sxs-lookup"><span data-stu-id="fa08f-146">Create public IP addresses for hello front-end pool</span></span>

1. <span data-ttu-id="fa08f-147">Настройка переменных PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="fa08f-147">Set up hello PowerShell variables</span></span>

    ```powershell
    $publicIpv4Name = "myIPv4Vip"
    $publicIpv6Name = "myIPv6Vip"
    ```

2. <span data-ttu-id="fa08f-148">Создайте открытый пул IP-адресов hello интерфейсный IP.</span><span class="sxs-lookup"><span data-stu-id="fa08f-148">Create a public IP address hello front-end IP pool.</span></span>

    ```azurecli
    $publicipV4 = azure network public-ip create --resource-group $rgname --name $publicIpv4Name --location $location --ip-version IPv4 --allocation-method Dynamic --domain-name-label $dnsLabel
    $publicipV6 = azure network public-ip create --resource-group $rgname --name $publicIpv6Name --location $location --ip-version IPv6 --allocation-method Dynamic --domain-name-label $dnsLabel
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="fa08f-149">Hello балансировки нагрузки использует метку домена hello hello общедоступный IP-адрес в качестве его полное доменное имя.</span><span class="sxs-lookup"><span data-stu-id="fa08f-149">hello load balancer uses hello domain label of hello public IP as its FQDN.</span></span> <span data-ttu-id="fa08f-150">Это изменение по сравнению с классической развертывания с использованием имени облачной службы hello как hello балансировки нагрузки полное доменное имя.</span><span class="sxs-lookup"><span data-stu-id="fa08f-150">This a change from classic deployment, which uses hello cloud service name as hello load balancer FQDN.</span></span>
    > <span data-ttu-id="fa08f-151">В этом примере hello полное доменное имя — *contoso09152016.southcentralus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="fa08f-151">In this example, hello FQDN is *contoso09152016.southcentralus.cloudapp.azure.com*.</span></span>

## <a name="create-front-end-and-back-end-pools"></a><span data-ttu-id="fa08f-152">Создание интерфейсного и внутреннего пулов</span><span class="sxs-lookup"><span data-stu-id="fa08f-152">Create front-end and back-end pools</span></span>

<span data-ttu-id="fa08f-153">Этот пример создает hello переднего плана пула IP-адресов, получающий hello входящего сетевого трафика в подсистеме балансировки нагрузки hello и hello серверной части пула IP-адресов где переднего плана пула hello отправляет hello балансировки нагрузки сетевого трафика.</span><span class="sxs-lookup"><span data-stu-id="fa08f-153">This example creates hello front-end IP pool that receives hello incoming network traffic on hello load balancer and hello back-end IP pool where hello front-end pool sends hello load balanced network traffic.</span></span>

1. <span data-ttu-id="fa08f-154">Настройка переменных PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="fa08f-154">Set up hello PowerShell variables</span></span>

    ```powershell
    $frontendV4Name = "FrontendVipIPv4"
    $frontendV6Name = "FrontendVipIPv6"
    $backendAddressPoolV4Name = "BackendPoolIPv4"
    $backendAddressPoolV6Name = "BackendPoolIPv6"
    ```

2. <span data-ttu-id="fa08f-155">Создайте пул IP переднего плана, связывание hello общедоступный IP-адрес создан в предыдущем шаге hello и Подсистема балансировки нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="fa08f-155">Create a front-end IP pool associating hello public IP created in hello previous step and hello load balancer.</span></span>

    ```azurecli
    $frontendV4 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV4Name --public-ip-name $publicIpv4Name --lb-name $lbName
    $frontendV6 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV6Name --public-ip-name $publicIpv6Name --lb-name $lbName
    $backendAddressPoolV4 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV4Name --lb-name $lbName
    $backendAddressPoolV6 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV6Name --lb-name $lbName
    ```

## <a name="create-hello-probe-nat-rules-and-lb-rules"></a><span data-ttu-id="fa08f-156">Создание hello пробы, правил NAT и правила балансировки Нагрузки</span><span class="sxs-lookup"><span data-stu-id="fa08f-156">Create hello probe, NAT rules, and LB rules</span></span>

<span data-ttu-id="fa08f-157">В этом примере создается hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="fa08f-157">This example creates hello following items:</span></span>

* <span data-ttu-id="fa08f-158">toocheck правила проверки для подключения к tooTCP порта 80</span><span class="sxs-lookup"><span data-stu-id="fa08f-158">a probe rule toocheck for connectivity tooTCP port 80</span></span>
* <span data-ttu-id="fa08f-159">преобразование сетевых адресов правила tootranslate весь входящий трафик на порт 3389 tooport 3389 для протокола удаленного рабочего СТОЛА<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="fa08f-159">a NAT rule tootranslate all incoming traffic on port 3389 tooport 3389 for RDP<sup>1</sup></span></span>
* <span data-ttu-id="fa08f-160">преобразование сетевых адресов правила tootranslate весь входящий трафик на tooport 3391 порт 3389 для протокола удаленного рабочего СТОЛА<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="fa08f-160">a NAT rule tootranslate all incoming traffic on port 3391 tooport 3389 for RDP<sup>1</sup></span></span>
* <span data-ttu-id="fa08f-161">toobalance правило балансировки нагрузки весь входящий трафик на порт 80 tooport 80 на hello адресов серверной части пула hello.</span><span class="sxs-lookup"><span data-stu-id="fa08f-161">a load balancer rule toobalance all incoming traffic on port 80 tooport 80 on hello addresses in hello back-end pool.</span></span>

<span data-ttu-id="fa08f-162"><sup>1</sup> NAT правила, связанные tooa конкретного экземпляра виртуальной машины за подсистемой балансировки нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="fa08f-162"><sup>1</sup> NAT rules are associated tooa specific virtual machine instance behind hello load balancer.</span></span> <span data-ttu-id="fa08f-163">Hello сетевой трафик, поступающий на порт 3389 отправляется toohello отдельную виртуальную машину и порт, связанный с правилом NAT hello.</span><span class="sxs-lookup"><span data-stu-id="fa08f-163">hello network traffic arriving on port 3389 is sent toohello specific virtual machine and port associated with hello NAT rule.</span></span> <span data-ttu-id="fa08f-164">Для правила NAT необходимо указать протокол (UDP или TCP).</span><span class="sxs-lookup"><span data-stu-id="fa08f-164">You must specify a protocol (UDP or TCP) for a NAT rule.</span></span> <span data-ttu-id="fa08f-165">Оба эти протокола не может быть назначен toohello тот же порт.</span><span class="sxs-lookup"><span data-stu-id="fa08f-165">Both protocols can't be assigned toohello same port.</span></span>

1. <span data-ttu-id="fa08f-166">Настройка переменных PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="fa08f-166">Set up hello PowerShell variables</span></span>

    ```powershell
    $probeV4V6Name = "ProbeForIPv4AndIPv6"
    $natRule1V4Name = "NatRule-For-Rdp-VM1"
    $natRule2V4Name = "NatRule-For-Rdp-VM2"
    $lbRule1V4Name = "LBRuleForIPv4-Port80"
    $lbRule1V6Name = "LBRuleForIPv6-Port80"
    ```

2. <span data-ttu-id="fa08f-167">Создать пробу hello</span><span class="sxs-lookup"><span data-stu-id="fa08f-167">Create hello probe</span></span>

    <span data-ttu-id="fa08f-168">Hello следующий пример создает проверки зонда TCP для подключения к конечным tooback TCP-порт 80 каждые 15 секунд.</span><span class="sxs-lookup"><span data-stu-id="fa08f-168">hello following example creates a TCP probe that checks for connectivity tooback-end TCP port 80 every 15 seconds.</span></span> <span data-ttu-id="fa08f-169">Он помечает hello внутренний ресурс недоступен после двух последовательных сбоев.</span><span class="sxs-lookup"><span data-stu-id="fa08f-169">It will mark hello back-end resource unavailable after two consecutive failures.</span></span>

    ```azurecli
    $probeV4V6 = azure network lb probe create --resource-group $rgname --name $probeV4V6Name --protocol tcp --port 80 --interval 15 --count 2 --lb-name $lbName
    ```

3. <span data-ttu-id="fa08f-170">Создание правила для входящих подключений NAT, поддерживающих соединения протокола удаленного рабочего СТОЛА toohello серверным ресурсам</span><span class="sxs-lookup"><span data-stu-id="fa08f-170">Create inbound NAT rules that allow RDP connections toohello back-end resources</span></span>

    ```azurecli
    $inboundNatRuleRdp1 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule1V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3389 --backend-port 3389 --lb-name $lbName
    $inboundNatRuleRdp2 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule2V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3391 --backend-port 3389 --lb-name $lbName
    ```

4. <span data-ttu-id="fa08f-171">Создание правил, которые отправлять трафик порты внутренней toodifferent в зависимости от того, какой запрос hello полученных переднего плана подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="fa08f-171">Create a load balancer rules that send traffic toodifferent back-end ports depending on which front end received hello request</span></span>

    ```azurecli
    $lbruleIPv4 = azure network lb rule create --resource-group $rgname --name $lbRule1V4Name --frontend-ip-name $frontendV4Name --backend-address-pool-name $backendAddressPoolV4Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 80 --lb-name $lbName
    $lbruleIPv6 = azure network lb rule create --resource-group $rgname --name $lbRule1V6Name --frontend-ip-name $frontendV6Name --backend-address-pool-name $backendAddressPoolV6Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 8080 --lb-name $lbName
    ```

5. <span data-ttu-id="fa08f-172">Проверьте параметры.</span><span class="sxs-lookup"><span data-stu-id="fa08f-172">Check your settings</span></span>

    ```azurecli
    azure network lb show --resource-group $rgName --name $lbName
    ```

    <span data-ttu-id="fa08f-173">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="fa08f-173">Expected output:</span></span>

        info:    Executing command network lb show
        info:    Looking up hello load balancer "myIPv4IPv6Lb"
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

## <a name="create-nics"></a><span data-ttu-id="fa08f-174">Создание сетевых адаптеров</span><span class="sxs-lookup"><span data-stu-id="fa08f-174">Create NICs</span></span>

<span data-ttu-id="fa08f-175">Создать сетевые адаптеры и связать их tooNAT правила, правила подсистемы балансировки нагрузки и зонды.</span><span class="sxs-lookup"><span data-stu-id="fa08f-175">Create NICs and associate them tooNAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="fa08f-176">Настройка переменных PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="fa08f-176">Set up hello PowerShell variables</span></span>

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

2. <span data-ttu-id="fa08f-177">Создайте сетевую карту для каждой серверной части и добавьте конфигурацию IPv6.</span><span class="sxs-lookup"><span data-stu-id="fa08f-177">Create a NIC for each back-end and add an IPv6 configuration.</span></span>

    ```azurecli
    $nic1 = azure network nic create --name $nic1Name --resource-group $rgname --location $location --private-ip-version "IPv4" --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule1V4Id
    $nic1IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic1Name

    $nic2 = azure network nic create --name $nic2Name --resource-group $rgname --location $location --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule2V4Id
    $nic2IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic2Name
    ```

## <a name="create-hello-back-end-vm-resources-and-attach-each-nic"></a><span data-ttu-id="fa08f-178">Создать ресурсы виртуальной Машины сервера hello и присоединить каждый сетевой Адаптер</span><span class="sxs-lookup"><span data-stu-id="fa08f-178">Create hello back-end VM resources and attach each NIC</span></span>

<span data-ttu-id="fa08f-179">toocreate виртуальные машины, необходимо иметь учетную запись хранилища.</span><span class="sxs-lookup"><span data-stu-id="fa08f-179">toocreate VMs, you must have a storage account.</span></span> <span data-ttu-id="fa08f-180">Для балансировки нагрузки, hello виртуальные машины должны toobe члены группы доступности.</span><span class="sxs-lookup"><span data-stu-id="fa08f-180">For load balancing, hello VMs need toobe members of an availability set.</span></span> <span data-ttu-id="fa08f-181">Дополнительные сведения о создании виртуальных машин см. в статье [Создание виртуальной машины в Azure с помощью PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fa08f-181">For more information about creating VMs, see [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span></span>

1. <span data-ttu-id="fa08f-182">Настройка переменных PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="fa08f-182">Set up hello PowerShell variables</span></span>

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
    > <span data-ttu-id="fa08f-183">В этом примере используется hello имя пользователя и пароль для виртуальных машин hello в виде открытого текста.</span><span class="sxs-lookup"><span data-stu-id="fa08f-183">This example uses hello username and password for hello VMs in clear text.</span></span> <span data-ttu-id="fa08f-184">При с помощью учетные данные в hello снимите следует принять соответствующие меры.</span><span class="sxs-lookup"><span data-stu-id="fa08f-184">Appropriate care must be taken when using credentials in hello clear.</span></span> <span data-ttu-id="fa08f-185">Это более безопасный способ обработки учетных данных в PowerShell, в разделе hello [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) командлета.</span><span class="sxs-lookup"><span data-stu-id="fa08f-185">For a more secure method of handling credentials in PowerShell, see hello [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

2. <span data-ttu-id="fa08f-186">Создание учетной записи и доступности набора hello хранилища</span><span class="sxs-lookup"><span data-stu-id="fa08f-186">Create hello storage account and availability set</span></span>

    <span data-ttu-id="fa08f-187">Вы можете использовать существующую учетную запись хранилища при создании hello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="fa08f-187">You may use an existing storage account when you create hello VMs.</span></span> <span data-ttu-id="fa08f-188">Привет, следующая команда создает новую учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="fa08f-188">hello following command creates a new storage account.</span></span>

    ```azurecli
    $storageAcc = azure storage account create $storageAccountName --resource-group $rgName --location $location --sku-name "LRS" --kind "Storage"
    ```

    <span data-ttu-id="fa08f-189">Создайте группу доступности hello.</span><span class="sxs-lookup"><span data-stu-id="fa08f-189">Next, create hello availability set.</span></span>

    ```azurecli
    $availabilitySet = azure availset create --name $availabilitySetName --resource-group $rgName --location $location
    ```

3. <span data-ttu-id="fa08f-190">Создание виртуальных машин hello с сетевыми адаптерами связанные hello</span><span class="sxs-lookup"><span data-stu-id="fa08f-190">Create hello virtual machines with hello associated NICs</span></span>

    ```azurecli
    $vm1 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm1Name --nic-id $nic1Id --os-disk-vhd $osDisk1Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension

    $vm2 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm2Name --nic-id $nic2Id --os-disk-vhd $osDisk2Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension
    ```

## <a name="next-steps"></a><span data-ttu-id="fa08f-191">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fa08f-191">Next steps</span></span>

[<span data-ttu-id="fa08f-192">Приступая к настройке внутренней подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="fa08f-192">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-cli.md)

[<span data-ttu-id="fa08f-193">Настройка режима распределения подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="fa08f-193">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="fa08f-194">Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="fa08f-194">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
