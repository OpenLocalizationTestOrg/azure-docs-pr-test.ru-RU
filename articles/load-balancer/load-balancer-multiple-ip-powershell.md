---
title: "aaaLoad балансировки на несколько IP-конфигурации в Azure | Документы Microsoft"
description: "Балансировка нагрузки между основной и дополнительной IP-конфигурациями."
services: load-balancer
documentationcenter: na
author: anavinahar
manager: narayan
editor: na
ms.assetid: 244907cd-b275-4494-aaf7-dcfc4d93edfe
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: annahar
ms.openlocfilehash: fe1cdb317350942ff759229491c2025e98dd24a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="load-balancing-on-multiple-ip-configurations-using-powershell"></a><span data-ttu-id="82209-103">Балансировка нагрузки в конфигурациях с несколькими IP-адресами с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="82209-103">Load balancing on multiple IP configurations using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="82209-104">Портал</span><span class="sxs-lookup"><span data-stu-id="82209-104">Portal</span></span>](load-balancer-multiple-ip.md)
> * [<span data-ttu-id="82209-105">ИНТЕРФЕЙС КОМАНДНОЙ СТРОКИ</span><span class="sxs-lookup"><span data-stu-id="82209-105">CLI</span></span>](load-balancer-multiple-ip-cli.md)
> * [<span data-ttu-id="82209-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="82209-106">PowerShell</span></span>](load-balancer-multiple-ip-powershell.md)

<span data-ttu-id="82209-107">В этой статье описывается, как toouse подсистемы балансировки нагрузки Azure с несколькими IP-адресов для дополнительного сетевого интерфейса (NIC).</span><span class="sxs-lookup"><span data-stu-id="82209-107">This article describes how toouse Azure Load Balancer with multiple IP addresses on a secondary network interface (NIC).</span></span> <span data-ttu-id="82209-108">В этом сценарии у нас есть две виртуальные машины под управлением Windows, оснащенные основной и дополнительной сетевыми картами.</span><span class="sxs-lookup"><span data-stu-id="82209-108">For this scenario, we have two VMs running Windows, each with a primary and a secondary NIC.</span></span> <span data-ttu-id="82209-109">Каждый дополнительный hello сетевые адаптеры имеют два IP-конфигурации.</span><span class="sxs-lookup"><span data-stu-id="82209-109">Each of hello secondary NICs have two IP configurations.</span></span> <span data-ttu-id="82209-110">На каждой виртуальной машине размещены веб-сайты contoso.com и fabrikam.com. Каждый веб-сайт имеет связанный tooone hello IP-конфигурации сетевого адаптера hello получателей.</span><span class="sxs-lookup"><span data-stu-id="82209-110">Each VM hosts both websites contoso.com and fabrikam.com. Each website is bound tooone of hello IP configurations on hello secondary NIC.</span></span> <span data-ttu-id="82209-111">Мы используем подсистемы балансировки нагрузки Azure tooexpose два интерфейсных IP-адреса, один для каждого веб-сайта, toodistribute трафик toohello соответствующие IP-конфигурацию для веб-сайта hello.</span><span class="sxs-lookup"><span data-stu-id="82209-111">We use Azure Load Balancer tooexpose two frontend IP addresses, one for each website, toodistribute traffic toohello respective IP configuration for hello website.</span></span> <span data-ttu-id="82209-112">Этот сценарий использует hello одинаковый номер порта на серверах переднего плана, как, так и обоих внутренний пул IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="82209-112">This scenario uses hello same port number across both frontends, as well as both backend pool IP addresses.</span></span>

![Схема балансировки нагрузки для сценария](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

## <a name="steps-tooload-balance-on-multiple-ip-configurations"></a><span data-ttu-id="82209-114">Баланс tooload действия на нескольких IP-конфигурации</span><span class="sxs-lookup"><span data-stu-id="82209-114">Steps tooload balance on multiple IP configurations</span></span>

<span data-ttu-id="82209-115">Выполните действия hello ниже tooachieve hello сценарий, описанный в этой статье.</span><span class="sxs-lookup"><span data-stu-id="82209-115">Follow hello steps below tooachieve hello scenario outlined in this article:</span></span>

1. <span data-ttu-id="82209-116">Установите Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="82209-116">Install Azure PowerShell.</span></span> <span data-ttu-id="82209-117">В разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) сведения об установке hello последнюю версию Azure PowerShell, выбрав подписку и вход в учетную запись tooyour.</span><span class="sxs-lookup"><span data-stu-id="82209-117">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for information about installing hello latest version of Azure PowerShell, selecting your subscription, and signing in tooyour account.</span></span>
2. <span data-ttu-id="82209-118">Создание группы ресурсов с помощью hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="82209-118">Create a resource group using hello following settings:</span></span>

    ```powershell
    $location = "westcentralus".
    $myResourceGroup = "contosofabrikam"
    ```

    <span data-ttu-id="82209-119">Чтобы узнать больше, ознакомьтесь с шагом 2 в разделе [Создание группы ресурсов](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="82209-119">For more information, see Step 2 of [Create a Resource Group](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

3. <span data-ttu-id="82209-120">[Создание группы доступности](../virtual-machines/windows/tutorial-availability-sets.md?toc=%2fazure%2fload-balancer%2ftoc.json) toocontain виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="82209-120">[Create an Availability Set](../virtual-machines/windows/tutorial-availability-sets.md?toc=%2fazure%2fload-balancer%2ftoc.json) toocontain your VMs.</span></span> <span data-ttu-id="82209-121">В этом случае используйте hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="82209-121">For this scenario, use hello following command:</span></span>

    ```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset" -Location "West Central US"
    ```

4. <span data-ttu-id="82209-122">Следуйте инструкциям шаги 3 – 5 в [создания виртуальной Машины Windows](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) статью tooprepare hello Создание виртуальной Машины с одной сетевой картой.</span><span class="sxs-lookup"><span data-stu-id="82209-122">Follow instructions steps 3 through 5 in [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) article tooprepare hello creation of a VM with a single NIC.</span></span> <span data-ttu-id="82209-123">Выполните шаг 6.1 и используйте ниже hello вместо шаг 6.2:</span><span class="sxs-lookup"><span data-stu-id="82209-123">Execute step 6.1, and use hello following instead of step 6.2:</span></span>

    ```powershell
    $availset = Get-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset"
    New-AzureRmVMConfig -VMName "VM1" -VMSize "Standard_DS1_v2" -AvailabilitySetId $availset.Id
    ```

    <span data-ttu-id="82209-124">После этого выполните шаги 6.3–6.8 раздела [Создание виртуальной машины Windows](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="82209-124">Then complete [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) steps 6.3 through 6.8.</span></span>

5. <span data-ttu-id="82209-125">Добавьте второй tooeach конфигурации IP для hello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="82209-125">Add a second IP configuration tooeach of hello VMs.</span></span> <span data-ttu-id="82209-126">Следуйте инструкциям в разделе hello [назначить несколько IP-адресов для машин toovirtual](../virtual-network/virtual-network-multiple-ip-addresses-powershell.md#add) статьи.</span><span class="sxs-lookup"><span data-stu-id="82209-126">Follow hello instructions in [Assign multiple IP addresses toovirtual machines](../virtual-network/virtual-network-multiple-ip-addresses-powershell.md#add) article.</span></span> <span data-ttu-id="82209-127">Используйте следующие параметры конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="82209-127">Use hello following configuration settings:</span></span>

    ```powershell
    $NicName = "VM1-NIC2"
    $RgName = "contosofabrikam"
    $NicLocation = "West Central US"
    $IPConfigName4 = "VM1-ipconfig2"
    $Subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "mySubnet" -VirtualNetwork $myVnet
    ```

    <span data-ttu-id="82209-128">Не обязательно tooassociate hello дополнительный IP-конфигурации с общедоступных IP-адресов для hello целей этого учебника.</span><span class="sxs-lookup"><span data-stu-id="82209-128">You do not need tooassociate hello secondary IP configurations with public IPs for hello purpose of this tutorial.</span></span> <span data-ttu-id="82209-129">Измените hello команда tooremove hello открытый IP ассоциации часть.</span><span class="sxs-lookup"><span data-stu-id="82209-129">Edit hello command tooremove hello public IP association part.</span></span>

6. <span data-ttu-id="82209-130">Повторите шаги 4–6 данной статьи для VM2.</span><span class="sxs-lookup"><span data-stu-id="82209-130">Complete steps 4 through 6 of this article again for VM2.</span></span> <span data-ttu-id="82209-131">Быть tooVM2 имя виртуальной Машины hello tooreplace убедиться, что при выполнении этого действия.</span><span class="sxs-lookup"><span data-stu-id="82209-131">Be sure tooreplace hello VM name tooVM2 when doing this.</span></span> <span data-ttu-id="82209-132">Обратите внимание, что вы не toocreate виртуальной сети для hello второй виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="82209-132">Note that you do not need toocreate a virtual network for hello second VM.</span></span> <span data-ttu-id="82209-133">Вы можете создать или не создавать новую подсеть в зависимости от требований ситуации.</span><span class="sxs-lookup"><span data-stu-id="82209-133">You may or may not create a new subnet based on your use case.</span></span>

7. <span data-ttu-id="82209-134">Создание общих IP-адресов и сохранять их в соответствующих переменных hello, как показано:</span><span class="sxs-lookup"><span data-stu-id="82209-134">Create two public IP addresses and store them in hello appropriate variables as shown:</span></span>

    ```powershell
    $publicIP1 = New-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel contoso
    $publicIP2 = New-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel fabrikam

    $publicIP1 = Get-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam
    $publicIP2 = Get-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam
    ```

8. <span data-ttu-id="82209-135">Создайте две интерфейсные IP-конфигурации.</span><span class="sxs-lookup"><span data-stu-id="82209-135">Create two frontend IP configurations:</span></span>

    ```powershell
    $frontendIP1 = New-AzureRmLoadBalancerFrontendIpConfig -Name contosofe -PublicIpAddress $publicIP1
    $frontendIP2 = New-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2
    ```

9. <span data-ttu-id="82209-136">Создайте внутренние пулы адресов, пробу и правила балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="82209-136">Create your backend address pools, a probe, and your load balancing rules:</span></span>

    ```powershell
    $beaddresspool1 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name contosopool
    $beaddresspool2 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool

    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HTTP -RequestPath 'index.html' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

    $lbrule1 = New-AzureRmLoadBalancerRuleConfig -Name HTTPc -FrontendIpConfiguration $frontendIP1 -BackendAddressPool $beaddresspool1 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    $lbrule2 = New-AzureRmLoadBalancerRuleConfig -Name HTTPf -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

10. <span data-ttu-id="82209-137">После создания этих ресурсов создайте подсистему балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="82209-137">Once you have these resources created, create your load balancer:</span></span>

    ```powershell
    $mylb = New-AzureRmLoadBalancer -ResourceGroupName contosofabrikam -Name mylb -Location 'West Central US' -FrontendIpConfiguration $frontendIP1 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

11. <span data-ttu-id="82209-138">Добавление hello второй внутренний адрес пула и переднего плана IP конфигурации tooyour только что созданный подсистемы балансировки нагрузки:</span><span class="sxs-lookup"><span data-stu-id="82209-138">Add hello second backend address pool and frontend IP configuration tooyour newly created load balancer:</span></span>

    ```powershell
    $mylb = Get-AzureRmLoadBalancer -Name "mylb" -ResourceGroupName $myResourceGroup | Add-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool | Set-AzureRmLoadBalancer

    $mylb | Add-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2 | Set-AzureRmLoadBalancer
    
    Add-AzureRmLoadBalancerRuleConfig -Name HTTP -LoadBalancer $mylb -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80 | Set-AzureRmLoadBalancer
    ```

12. <span data-ttu-id="82209-139">приведенную ниже команду Hello получить hello сетевых адаптеров и затем добавить каждый дополнительный сетевой Адаптер toohello серверный пул адресов из hello оба IP-конфигурации подсистемы балансировки нагрузки:</span><span class="sxs-lookup"><span data-stu-id="82209-139">hello commands below get hello NICs and then add both IP configurations of each secondary NIC toohello backend address pool of hello load balancer:</span></span>

    ```powershell
    $nic1 = Get-AzureRmNetworkInterface -Name "VM1-NIC2" -ResourceGroupName "MyResourcegroup";
    $nic2 = Get-AzureRmNetworkInterface -Name "VM2-NIC2" -ResourceGroupName "MyResourcegroup";

    $nic1.IpConfigurations[0].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[0]);
    $nic1.IpConfigurations[1].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[1]);
    $nic2.IpConfigurations[0].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[0]);
    $nic2.IpConfigurations[1].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[1]);

    $mylb = $mylb | Set-AzureRmLoadBalancer

    $nic1 | Set-AzureRmNetworkInterface
    $nic2 | Set-AzureRmNetworkInterface
    ```

13. <span data-ttu-id="82209-140">Наконец необходимо настроить DNS ресурса записи toopoint toohello соответствующих интерфейсный IP-адрес hello подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="82209-140">Finally, you must configure DNS resource records toopoint toohello respective frontend IP address of hello Load Balancer.</span></span> <span data-ttu-id="82209-141">Домены можно разместить в Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="82209-141">You may host your domains in Azure DNS.</span></span> <span data-ttu-id="82209-142">Дополнительные сведения об использовании Azure DNS с подсистемой балансировки нагрузки см. в разделе [Использование Azure DNS с другими службами Azure](../dns/dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="82209-142">For more information about using Azure DNS with Load Balancer, see [Using Azure DNS with other Azure services](../dns/dns-for-azure-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="82209-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="82209-143">Next steps</span></span>
- <span data-ttu-id="82209-144">Дополнительные сведения о как Балансировка нагрузки toocombine службами в Azure в [с помощью службы балансировки нагрузки в Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span><span class="sxs-lookup"><span data-stu-id="82209-144">Learn more about how toocombine load balancing services in Azure in [Using load-balancing services in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span></span>
- <span data-ttu-id="82209-145">Узнайте, как использовать различные типы журналов в Azure toomanage и устранение неполадок подсистемы балансировки нагрузки в [аналитика журналов для балансировки нагрузки Azure](../load-balancer/load-balancer-monitor-log.md).</span><span class="sxs-lookup"><span data-stu-id="82209-145">Learn how you can use different types of logs in Azure toomanage and troubleshoot load balancer in [Log analytics for Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).</span></span>
