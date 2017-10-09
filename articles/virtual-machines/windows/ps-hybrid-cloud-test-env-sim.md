---
title: "aaaSimulated гибридного облака тестовой среды | Документы Microsoft"
description: "Создание смоделированной гибридной облачной среды для ИТ-специалистов или тестирования разработки с использованием двух виртуальных сетей Azure и подключения тип VNet-to-VNet."
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ca5bf294-8172-44a9-8fed-d6f38d345364
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.openlocfilehash: 6063022e373c2b3564e040c4fbee122e2438974b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-simulated-hybrid-cloud-environment-for-testing"></a><span data-ttu-id="dc974-103">Создание имитации гибридной облачной среды для тестирования</span><span class="sxs-lookup"><span data-stu-id="dc974-103">Set up a simulated hybrid cloud environment for testing</span></span>
<span data-ttu-id="dc974-104">В этом разделе описываются шаги по созданию смоделированной гибридной облачной среды с помощью платформы Microsoft Azure, использующей две виртуальные сети Azure.</span><span class="sxs-lookup"><span data-stu-id="dc974-104">This article steps you through creating a simulated hybrid cloud environment with Microsoft Azure using two Azure virtual networks.</span></span> <span data-ttu-id="dc974-105">Здесь представлена конфигурация полученный hello.</span><span class="sxs-lookup"><span data-stu-id="dc974-105">Here is hello resulting configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

<span data-ttu-id="dc974-106">Она позволяет смоделировать гибридную облачную рабочую среду и состоит из следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="dc974-106">This simulates a hybrid cloud production environment and consists of:</span></span>

* <span data-ttu-id="dc974-107">Имитация и упрощенный локальной сети в виртуальной сети Azure (hello тестовая лаборатория виртуальной сети).</span><span class="sxs-lookup"><span data-stu-id="dc974-107">A simulated and simplified on-premises network hosted in an Azure virtual network (hello TestLab virtual network).</span></span>
* <span data-ttu-id="dc974-108">смоделированная виртуальная сеть с подключением между организациями, размещенная в Azure (TestVNET).</span><span class="sxs-lookup"><span data-stu-id="dc974-108">A simulated cross-premises virtual network hosted in Azure (TestVNET).</span></span>
* <span data-ttu-id="dc974-109">Подключение виртуальной сети для виртуальной сети между hello двух виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="dc974-109">A VNet-to-VNet connection between hello two virtual networks.</span></span>
* <span data-ttu-id="dc974-110">Дополнительный контроллер домена в виртуальной сети TestVNET hello.</span><span class="sxs-lookup"><span data-stu-id="dc974-110">A secondary domain controller in hello TestVNET virtual network.</span></span>

<span data-ttu-id="dc974-111">Это основа и общая начальная точка, на базе которой можно:</span><span class="sxs-lookup"><span data-stu-id="dc974-111">This provides a basis and common starting point from which you can:</span></span>

* <span data-ttu-id="dc974-112">разрабатывать и тестировать приложения в смоделированной гибридной облачной среде.</span><span class="sxs-lookup"><span data-stu-id="dc974-112">Develop and test applications in a simulated hybrid cloud environment.</span></span>
* <span data-ttu-id="dc974-113">Создание конфигураций тестов из компьютеров, некоторые в hello тестовая лаборатория виртуальной сети, а некоторые в виртуальной сети TestVNET hello, toosimulate гибридной облачной ИТ-задач.</span><span class="sxs-lookup"><span data-stu-id="dc974-113">Create test configurations of computers, some within hello TestLab virtual network and some within hello TestVNET virtual network, toosimulate hybrid cloud-based IT workloads.</span></span>

<span data-ttu-id="dc974-114">Существует четыре основных этапа toosetting этой тестовой среды гибридного облака:</span><span class="sxs-lookup"><span data-stu-id="dc974-114">There are four major phases toosetting up this hybrid cloud test environment:</span></span>

1. <span data-ttu-id="dc974-115">Настройка виртуальной сети hello тестовая лаборатория.</span><span class="sxs-lookup"><span data-stu-id="dc974-115">Configure hello TestLab virtual network.</span></span>
2. <span data-ttu-id="dc974-116">Создайте виртуальную сеть между организациями hello.</span><span class="sxs-lookup"><span data-stu-id="dc974-116">Create hello cross-premises virtual network.</span></span>
3. <span data-ttu-id="dc974-117">Создание VPN-подключения hello виртуальной сети для виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="dc974-117">Create hello VNet-to-VNet VPN connection.</span></span>
4. <span data-ttu-id="dc974-118">Настройка DC2.</span><span class="sxs-lookup"><span data-stu-id="dc974-118">Configure DC2.</span></span> 

<span data-ttu-id="dc974-119">Для этой конфигурации требуется подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="dc974-119">This configuration requires an Azure subscription.</span></span> <span data-ttu-id="dc974-120">Если у вас есть подписка MSDN или Visual Studio, ознакомьтесь с разделом [Ежемесячная сумма денег на счете в Azure для подписчиков Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="dc974-120">If you have an MSDN or Visual Studio subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span>

> [!NOTE]
> <span data-ttu-id="dc974-121">Виртуальные машины и шлюзы виртуальных сетей в Azure создают текущие расходы во время своей работы.</span><span class="sxs-lookup"><span data-stu-id="dc974-121">Virtual machines and virtual network gateways in Azure incur an ongoing monetary cost when they are running.</span></span> <span data-ttu-id="dc974-122">На эти затраты выставляется счет при использовании подписки MSDN или платной подписки.</span><span class="sxs-lookup"><span data-stu-id="dc974-122">This cost is billed against your MSDN or paid subscription.</span></span> <span data-ttu-id="dc974-123">Шлюз Azure VPN реализован как набор двух виртуальных машин Azure.</span><span class="sxs-lookup"><span data-stu-id="dc974-123">An Azure VPN gateway is implemented as a set of two Azure virtual machines.</span></span> <span data-ttu-id="dc974-124">toominimize hello затрат, создание тестовой среды hello и как можно быстрее выполнить необходимые попробовать и демонстрацию.</span><span class="sxs-lookup"><span data-stu-id="dc974-124">toominimize hello costs, create hello test environment and perform your needed testing and demonstration as quickly as possible.</span></span>
> 
> 

## <a name="phase-1-configure-hello-testlab-virtual-network"></a><span data-ttu-id="dc974-125">Этап 1: Настройка hello тестовая лаборатория виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="dc974-125">Phase 1: Configure hello TestLab virtual network</span></span>
<span data-ttu-id="dc974-126">Используйте инструкции hello в hello [базовая конфигурация тестовой среды](https://technet.microsoft.com/library/mt771177.aspx) разделе tooconfigure hello DC1, APP1 и CLIENT1 компьютеров в виртуальной сети Azure, с именем тестовая лаборатория hello.</span><span class="sxs-lookup"><span data-stu-id="dc974-126">Use hello instructions in hello [Base Configuration test environment](https://technet.microsoft.com/library/mt771177.aspx) topic tooconfigure hello DC1, APP1, and CLIENT1 computers in hello Azure virtual network named TestLab.</span></span> 

<span data-ttu-id="dc974-127">Затем запустите командную строку Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dc974-127">Next, start an Azure PowerShell prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="dc974-128">Следующая команда задает Hello использовать Azure PowerShell версии 1.0 и более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="dc974-128">hello following command sets use Azure PowerShell 1.0 and later.</span></span>
> 
> 

<span data-ttu-id="dc974-129">Войдите в учетную запись tooyour.</span><span class="sxs-lookup"><span data-stu-id="dc974-129">Sign in tooyour account.</span></span>

    Login-AzureRMAccount

<span data-ttu-id="dc974-130">Получите имя своей подписки, используя следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="dc974-130">Get your subscription name using hello following command.</span></span>

    Get-AzureRMSubscription | Sort SubscriptionName | Select SubscriptionName

<span data-ttu-id="dc974-131">Настройте свою подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="dc974-131">Set your Azure subscription.</span></span> <span data-ttu-id="dc974-132">Используйте hello же подписку, которая использовалась toobuild базовой конфигурации на этапе 1.</span><span class="sxs-lookup"><span data-stu-id="dc974-132">Use hello same subscription that you used toobuild your base configuration in Phase 1.</span></span> <span data-ttu-id="dc974-133">Замените весь код внутри кавычек hello, включая hello < и > символы, с правильным именем hello.</span><span class="sxs-lookup"><span data-stu-id="dc974-133">Replace everything within hello quotes, including hello < and > characters, with hello correct name.</span></span>

    $subscr="<subscription name>"
    Get-AzureRmSubscription –SubscriptionName $subscr | Select-AzureRmSubscription

<span data-ttu-id="dc974-134">Далее следует добавьте шлюз подсети toohello тестовая лаборатория виртуальной сети для базовой конфигурации, которой будет hello toohost используется шлюз Azure.</span><span class="sxs-lookup"><span data-stu-id="dc974-134">Next, add a gateway subnet toohello TestLab virtual network of your base configuration, which will be used toohost hello Azure gateway.</span></span>

    $rgName="<name of your resource group that you used for your TestLab virtual network>"
    $locName="<Azure location name where you placed hello TestLab virtual network, such as West US>"
    $vnet=Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name TestLab
    Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix 10.255.255.248/29 -VirtualNetwork $vnet
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet

<span data-ttu-id="dc974-135">Далее запрос открытый IP адрес tooassign toohello шлюза виртуальной сети hello тестовая лаборатория.</span><span class="sxs-lookup"><span data-stu-id="dc974-135">Next, request a public IP address tooassign toohello gateway for hello TestLab virtual network.</span></span>

    $gwpip=New-AzureRmPublicIpAddress -Name TestLab_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic

<span data-ttu-id="dc974-136">Создайте шлюз.</span><span class="sxs-lookup"><span data-stu-id="dc974-136">Next, create your gateway.</span></span>

    $vnet=Get-AzureRmVirtualNetwork -Name TestLab -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name TestLab_GWConfig -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id 
    New-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

<span data-ttu-id="dc974-137">Имейте в виду, что для новых шлюзов может потребоваться 20 минут или более toocreate.</span><span class="sxs-lookup"><span data-stu-id="dc974-137">Keep in mind that new gateways can take 20 minutes or more toocreate.</span></span>

<span data-ttu-id="dc974-138">Подключитесь tooDC1 с учетные данные CORP\User1 hello hello портал Azure на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="dc974-138">From hello Azure portal on your local computer, connect tooDC1 with hello CORP\User1 credentials.</span></span> <span data-ttu-id="dc974-139">домен CORP tooconfigure hello, чтобы компьютеры и пользователи используют их локального контроллера домена для проверки подлинности, выполняйте эти команды из командной строки Windows PowerShell с правами администратора на компьютере DC1.</span><span class="sxs-lookup"><span data-stu-id="dc974-139">tooconfigure hello CORP domain so that computers and users use their local domain controller for authentication, run these commands from an administrator-level Windows PowerShell command prompt on DC1.</span></span>

    New-ADReplicationSite -Name "TestLab" 
    New-ADReplicationSite -Name "TestVNET"
    New-ADReplicationSubnet -Name "10.0.0.0/8" -Site "TestLab"
    New-ADReplicationSubnet -Name "192.168.0.0/16" -Site "TestVNET"

<span data-ttu-id="dc974-140">Это текущая конфигурация.</span><span class="sxs-lookup"><span data-stu-id="dc974-140">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph1.png)

## <a name="phase-2-create-hello-testvnet-virtual-network"></a><span data-ttu-id="dc974-141">Этап 2: Создайте виртуальную сеть TestVNET hello</span><span class="sxs-lookup"><span data-stu-id="dc974-141">Phase 2: Create hello TestVNET virtual network</span></span>
<span data-ttu-id="dc974-142">Во-первых создайте виртуальную сеть TestVNET hello и защитите его с сетевой группой безопасности.</span><span class="sxs-lookup"><span data-stu-id="dc974-142">First, create hello TestVNET virtual network and protect it with a network security group.</span></span>

    $rgName="<name of hello resource group that you used for your TestLab virtual network>"
    $locName="<Azure location name where you placed hello TestLab virtual network, such as West US>"
    $locShortName="<Azure location name from $locName in all lowercase letters with spaces removed. Example:  westus>"
    $testSubnet=New-AzureRMVirtualNetworkSubnetConfig -Name "TestSubnet" -AddressPrefix 192.168.0.0/24
    $gatewaySubnet=New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix 192.168.255.248/29
    New-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName -Location $locName -AddressPrefix 192.168.0.0/16 -Subnet $testSubnet,$gatewaySubnet –DNSServer 10.0.0.4
    $rule1=New-AzureRMNetworkSecurityRuleConfig -Name "RDPTraffic" -Description "Allow RDP tooall VMs on hello subnet" -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 -SourceAddressPrefix Internet -SourcePortRange * -DestinationAddressPrefix * -DestinationPortRange 3389
    New-AzureRMNetworkSecurityGroup -Name "TestSubnet" -ResourceGroupName $rgName -Location $locShortName -SecurityRules $rule1
    $vnet=Get-AzureRMVirtualNetwork -ResourceGroupName $rgName -Name TestVNET
    $nsg=Get-AzureRMNetworkSecurityGroup -Name "TestSubnet" -ResourceGroupName $rgName
    Set-AzureRMVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet" -AddressPrefix 192.168.0.0/24 -NetworkSecurityGroup $nsg

<span data-ttu-id="dc974-143">Далее запрос открытый toobe адрес IP выделенный toohello шлюз для виртуальной сети TestVNET hello и создания шлюза.</span><span class="sxs-lookup"><span data-stu-id="dc974-143">Next, request a public IP address toobe allocated toohello gateway for hello TestVNET virtual network and create your gateway.</span></span>

    $gwpip=New-AzureRmPublicIpAddress -Name TestVNET_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $vnet=Get-AzureRmVirtualNetwork -Name TestVNET -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name "TestVNET_GWConfig" -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
    New-AzureRmVirtualNetworkGateway -Name "TestVNET_GW" -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

<span data-ttu-id="dc974-144">Это текущая конфигурация.</span><span class="sxs-lookup"><span data-stu-id="dc974-144">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph2.png)

## <a name="phase-3-create-hello-vnet-to-vnet-connection"></a><span data-ttu-id="dc974-145">Этап 3: Создание подключения hello виртуальной сети для виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="dc974-145">Phase 3: Create hello VNet-to-VNet connection</span></span>
<span data-ttu-id="dc974-146">Сначала получите случайный, надежно зашифрованный 32-значный общий ключ у администратора сети или администратора безопасности.</span><span class="sxs-lookup"><span data-stu-id="dc974-146">First, obtain a random, cryptographically strong, 32-character pre-shared key from your network or security administrator.</span></span> <span data-ttu-id="dc974-147">Можно также использовать информацию hello в [Создание произвольной строки предварительного ключа IPsec](http://social.technet.microsoft.com/wiki/contents/articles/32330.create-a-random-string-for-an-ipsec-preshared-key.aspx) tooobtain общий ключ.</span><span class="sxs-lookup"><span data-stu-id="dc974-147">Alternately, use hello information at [Create a random string for an IPsec preshared key](http://social.technet.microsoft.com/wiki/contents/articles/32330.create-a-random-string-for-an-ipsec-preshared-key.aspx) tooobtain a pre-shared key.</span></span>

<span data-ttu-id="dc974-148">Затем используйте эти команды toocreate hello виртуальная сеть — сеть VPN-подключения, что может занять некоторое время toocomplete.</span><span class="sxs-lookup"><span data-stu-id="dc974-148">Next, use these commands toocreate hello VNet-to-VNet VPN connection, which can take some time toocomplete.</span></span>

    $sharedKey="<pre-shared key value>"
    $gwTestLab=Get-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName
    $gwTestVNET=Get-AzureRmVirtualNetworkGateway -Name TestVNET_GW -ResourceGroupName $rgName
    New-AzureRmVirtualNetworkGatewayConnection -Name TestLab_to_TestVNET -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestLab -VirtualNetworkGateway2 $gwTestVNET -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey
    New-AzureRmVirtualNetworkGatewayConnection -Name TestVNET_to_TestLab -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestVNET -VirtualNetworkGateway2 $gwTestLab -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey

<span data-ttu-id="dc974-149">Через несколько минут hello подключение должно быть установлено.</span><span class="sxs-lookup"><span data-stu-id="dc974-149">After a few minutes, hello connection should be established.</span></span>

<span data-ttu-id="dc974-150">Это текущая конфигурация.</span><span class="sxs-lookup"><span data-stu-id="dc974-150">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph3.png)

## <a name="phase-4-configure-dc2"></a><span data-ttu-id="dc974-151">Этап 4. Настройка DC2</span><span class="sxs-lookup"><span data-stu-id="dc974-151">Phase 4: Configure DC2</span></span>
<span data-ttu-id="dc974-152">Прежде всего создайте виртуальную машину для DC2.</span><span class="sxs-lookup"><span data-stu-id="dc974-152">First, create a virtual machine for DC2.</span></span> <span data-ttu-id="dc974-153">Выполняйте эти команды в командной строке hello Azure PowerShell на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="dc974-153">Run these commands at hello Azure PowerShell command prompt on your local computer.</span></span>

    $rgName="<your resource group name>"
    $locName="<your Azure location, such as West US>"
    $saName="<hello storage account name for hello base configuration>"
    $vnet=Get-AzureRMVirtualNetwork -Name TestVNET -ResourceGroupName $rgName
    $pip=New-AzureRMPublicIpAddress -Name DC2-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name DC2-NIC -ResourceGroupName $rgName -Location $locName -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -PrivateIpAddress 192.168.0.4
    $vm=New-AzureRMVMConfig -VMName DC2 -VMSize Standard_A1
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $vhdURI=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/DC2-TestVNET-ADDSDisk.vhd"
    Add-AzureRMVMDataDisk -VM $vm -Name ADDS-Data -DiskSizeInGB 20 -VhdUri $vhdURI  -CreateOption empty
    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account for DC2."
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName DC2 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/DC2-TestLab-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name DC2-TestVNET-OSDisk -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

<span data-ttu-id="dc974-154">Затем подключитесь toohello Новая виртуальная машина DC2 из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="dc974-154">Next, connect toohello new DC2 virtual machine from hello Azure portal.</span></span>

<span data-ttu-id="dc974-155">Настройте трафика tooallow правило брандмауэра Windows для тестирования связности.</span><span class="sxs-lookup"><span data-stu-id="dc974-155">Next, configure a Windows Firewall rule tooallow traffic for basic connectivity testing.</span></span> <span data-ttu-id="dc974-156">Из командной строки Windows PowerShell с правами администратора на DC2 выполните следующие команды.</span><span class="sxs-lookup"><span data-stu-id="dc974-156">From an administrator-level Windows PowerShell command prompt on DC2, run these commands.</span></span>

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc1.corp.contoso.com

<span data-ttu-id="dc974-157">команда ping Hello должны появиться четыре успешного ответа от IP-адрес 10.0.0.4.</span><span class="sxs-lookup"><span data-stu-id="dc974-157">hello ping command should result in four successful replies from IP address 10.0.0.4.</span></span> <span data-ttu-id="dc974-158">Это тест трафика между hello подключения VNet-VNet.</span><span class="sxs-lookup"><span data-stu-id="dc974-158">This is a test of traffic across hello VNet-to-VNet connection.</span></span>

<span data-ttu-id="dc974-159">Добавьте hello дополнительный диск данных на DC2 как новый том с буквой hello диска «f:».</span><span class="sxs-lookup"><span data-stu-id="dc974-159">Next, add hello extra data disk on DC2 as a new volume with hello drive letter F:.</span></span>

1. <span data-ttu-id="dc974-160">Hello левой панели диспетчера сервера щелкните **файловых служб и служб хранилища**, а затем нажмите кнопку **дисков**.</span><span class="sxs-lookup"><span data-stu-id="dc974-160">In hello left pane of Server Manager, click **File and Storage Services**, and then click **Disks**.</span></span>
2. <span data-ttu-id="dc974-161">В области содержимого hello в hello **дисков** щелкните **диск 2** (с hello **секции** значение слишком**Неизвестный**).</span><span class="sxs-lookup"><span data-stu-id="dc974-161">In hello contents pane, in hello **Disks** group, click **disk 2** (with hello **Partition** set too**Unknown**).</span></span>
3. <span data-ttu-id="dc974-162">Щелкните **Задачи**, а затем **Новый том**.</span><span class="sxs-lookup"><span data-stu-id="dc974-162">Click **Tasks**, and then click **New Volume**.</span></span>
4. <span data-ttu-id="dc974-163">Hello перед началом страница приветствия мастера создания тома, щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="dc974-163">On hello Before you begin page of hello New Volume Wizard, click **Next**.</span></span>
5. <span data-ttu-id="dc974-164">На сервере выберите hello hello и страницы с диска, нажмите кнопку **диск 2**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="dc974-164">On hello Select hello server and disk page, click **Disk 2**, and then click **Next**.</span></span> <span data-ttu-id="dc974-165">При появлении запроса нажмите кнопку **OK**.</span><span class="sxs-lookup"><span data-stu-id="dc974-165">When prompted, click **OK**.</span></span>
6. <span data-ttu-id="dc974-166">Щелкните hello задать hello размер страницы приветствия тома, **Далее**.</span><span class="sxs-lookup"><span data-stu-id="dc974-166">On hello Specify hello size of hello volume page, click **Next**.</span></span>
7. <span data-ttu-id="dc974-167">На hello Assign tooa диска буква или папка "нажмите" **Далее**.</span><span class="sxs-lookup"><span data-stu-id="dc974-167">On hello Assign tooa drive letter or folder page, click **Next**.</span></span>
8. <span data-ttu-id="dc974-168">На странице параметров системы hello выберите файл, нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="dc974-168">On hello Select file system settings page, click **Next**.</span></span>
9. <span data-ttu-id="dc974-169">На странице подтверждения выбранных элементов hello щелкните **создать**.</span><span class="sxs-lookup"><span data-stu-id="dc974-169">On hello Confirm selections page, click **Create**.</span></span>
10. <span data-ttu-id="dc974-170">После завершения нажмите кнопку **Закрыть**.</span><span class="sxs-lookup"><span data-stu-id="dc974-170">When complete, click **Close**.</span></span>

<span data-ttu-id="dc974-171">Затем настройте DC2 в качестве реплики контроллера домена для домена corp.contoso.com hello.</span><span class="sxs-lookup"><span data-stu-id="dc974-171">Next, configure DC2 as a replica domain controller for hello corp.contoso.com domain.</span></span> <span data-ttu-id="dc974-172">Выполните следующие команды из командной строки Windows PowerShell hello на DC2.</span><span class="sxs-lookup"><span data-stu-id="dc974-172">Run these commands from hello Windows PowerShell command prompt on DC2.</span></span>

    Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
    Install-ADDSDomainController -Credential (Get-Credential CORP\User1) -DomainName "corp.contoso.com" -InstallDns:$true -DatabasePath "F:\NTDS" -LogPath "F:\Logs" -SysvolPath "F:\SYSVOL"

<span data-ttu-id="dc974-173">Обратите внимание, что вы запрашиваемые toosupply оба hello CORP\User1 пароль и пароль режима восстановления служб каталогов (DSRM) и toorestart DC2.</span><span class="sxs-lookup"><span data-stu-id="dc974-173">Note that you are prompted toosupply both hello CORP\User1 password and a Directory Services Restore Mode (DSRM) password, and toorestart DC2.</span></span>

<span data-ttu-id="dc974-174">Теперь, когда hello TestVNET виртуальной сети имеет свой собственный DNS-сервер (DC2), необходимо настроить hello TestVNET виртуальной сети toouse этого DNS-сервера.</span><span class="sxs-lookup"><span data-stu-id="dc974-174">Now that hello TestVNET virtual network has its own DNS server (DC2), you must configure hello TestVNET virtual network toouse this DNS server.</span></span>

1. <span data-ttu-id="dc974-175">Hello левой части hello портал Azure, щелкните значок hello виртуальные сети и нажмите кнопку **TestVNET**.</span><span class="sxs-lookup"><span data-stu-id="dc974-175">In hello left pane of hello Azure portal, click hello virtual networks icon, and then click **TestVNET**.</span></span>
2. <span data-ttu-id="dc974-176">На hello **параметры** щелкните **DNS-серверы**.</span><span class="sxs-lookup"><span data-stu-id="dc974-176">On hello **Settings** tab, click **DNS servers**.</span></span>
3. <span data-ttu-id="dc974-177">В **основной DNS-сервер**, тип **192.168.0.4** tooreplace 10.0.0.4.</span><span class="sxs-lookup"><span data-stu-id="dc974-177">In **Primary DNS server**, type **192.168.0.4** tooreplace 10.0.0.4.</span></span>
4. <span data-ttu-id="dc974-178">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="dc974-178">Click **Save**.</span></span>

<span data-ttu-id="dc974-179">Это текущая конфигурация.</span><span class="sxs-lookup"><span data-stu-id="dc974-179">This is your current configuration.</span></span> 

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

<span data-ttu-id="dc974-180">Смоделированная гибридная облачная среда готова для тестирования.</span><span class="sxs-lookup"><span data-stu-id="dc974-180">Your simulated hybrid cloud environment is now ready for testing.</span></span>

## <a name="next-step"></a><span data-ttu-id="dc974-181">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dc974-181">Next step</span></span>
* <span data-ttu-id="dc974-182">Настройте в этой среде [специализированное веб-приложение](ps-hybrid-cloud-test-env-lob.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dc974-182">Set up a [web-based, line of business application](ps-hybrid-cloud-test-env-lob.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) in this environment.</span></span>

