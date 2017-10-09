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
# <a name="load-balancing-on-multiple-ip-configurations-using-powershell"></a>Балансировка нагрузки в конфигурациях с несколькими IP-адресами с помощью PowerShell

> [!div class="op_single_selector"]
> * [Портал](load-balancer-multiple-ip.md)
> * [ИНТЕРФЕЙС КОМАНДНОЙ СТРОКИ](load-balancer-multiple-ip-cli.md)
> * [PowerShell](load-balancer-multiple-ip-powershell.md)

В этой статье описывается, как toouse подсистемы балансировки нагрузки Azure с несколькими IP-адресов для дополнительного сетевого интерфейса (NIC). В этом сценарии у нас есть две виртуальные машины под управлением Windows, оснащенные основной и дополнительной сетевыми картами. Каждый дополнительный hello сетевые адаптеры имеют два IP-конфигурации. На каждой виртуальной машине размещены веб-сайты contoso.com и fabrikam.com. Каждый веб-сайт имеет связанный tooone hello IP-конфигурации сетевого адаптера hello получателей. Мы используем подсистемы балансировки нагрузки Azure tooexpose два интерфейсных IP-адреса, один для каждого веб-сайта, toodistribute трафик toohello соответствующие IP-конфигурацию для веб-сайта hello. Этот сценарий использует hello одинаковый номер порта на серверах переднего плана, как, так и обоих внутренний пул IP-адресов.

![Схема балансировки нагрузки для сценария](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

## <a name="steps-tooload-balance-on-multiple-ip-configurations"></a>Баланс tooload действия на нескольких IP-конфигурации

Выполните действия hello ниже tooachieve hello сценарий, описанный в этой статье.

1. Установите Azure PowerShell. В разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) сведения об установке hello последнюю версию Azure PowerShell, выбрав подписку и вход в учетную запись tooyour.
2. Создание группы ресурсов с помощью hello следующие параметры:

    ```powershell
    $location = "westcentralus".
    $myResourceGroup = "contosofabrikam"
    ```

    Чтобы узнать больше, ознакомьтесь с шагом 2 в разделе [Создание группы ресурсов](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).

3. [Создание группы доступности](../virtual-machines/windows/tutorial-availability-sets.md?toc=%2fazure%2fload-balancer%2ftoc.json) toocontain виртуальных машин. В этом случае используйте hello следующую команду:

    ```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset" -Location "West Central US"
    ```

4. Следуйте инструкциям шаги 3 – 5 в [создания виртуальной Машины Windows](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) статью tooprepare hello Создание виртуальной Машины с одной сетевой картой. Выполните шаг 6.1 и используйте ниже hello вместо шаг 6.2:

    ```powershell
    $availset = Get-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset"
    New-AzureRmVMConfig -VMName "VM1" -VMSize "Standard_DS1_v2" -AvailabilitySetId $availset.Id
    ```

    После этого выполните шаги 6.3–6.8 раздела [Создание виртуальной машины Windows](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).

5. Добавьте второй tooeach конфигурации IP для hello виртуальных машин. Следуйте инструкциям в разделе hello [назначить несколько IP-адресов для машин toovirtual](../virtual-network/virtual-network-multiple-ip-addresses-powershell.md#add) статьи. Используйте следующие параметры конфигурации hello.

    ```powershell
    $NicName = "VM1-NIC2"
    $RgName = "contosofabrikam"
    $NicLocation = "West Central US"
    $IPConfigName4 = "VM1-ipconfig2"
    $Subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "mySubnet" -VirtualNetwork $myVnet
    ```

    Не обязательно tooassociate hello дополнительный IP-конфигурации с общедоступных IP-адресов для hello целей этого учебника. Измените hello команда tooremove hello открытый IP ассоциации часть.

6. Повторите шаги 4–6 данной статьи для VM2. Быть tooVM2 имя виртуальной Машины hello tooreplace убедиться, что при выполнении этого действия. Обратите внимание, что вы не toocreate виртуальной сети для hello второй виртуальной Машины. Вы можете создать или не создавать новую подсеть в зависимости от требований ситуации.

7. Создание общих IP-адресов и сохранять их в соответствующих переменных hello, как показано:

    ```powershell
    $publicIP1 = New-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel contoso
    $publicIP2 = New-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel fabrikam

    $publicIP1 = Get-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam
    $publicIP2 = Get-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam
    ```

8. Создайте две интерфейсные IP-конфигурации.

    ```powershell
    $frontendIP1 = New-AzureRmLoadBalancerFrontendIpConfig -Name contosofe -PublicIpAddress $publicIP1
    $frontendIP2 = New-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2
    ```

9. Создайте внутренние пулы адресов, пробу и правила балансировки нагрузки.

    ```powershell
    $beaddresspool1 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name contosopool
    $beaddresspool2 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool

    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HTTP -RequestPath 'index.html' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

    $lbrule1 = New-AzureRmLoadBalancerRuleConfig -Name HTTPc -FrontendIpConfiguration $frontendIP1 -BackendAddressPool $beaddresspool1 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    $lbrule2 = New-AzureRmLoadBalancerRuleConfig -Name HTTPf -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

10. После создания этих ресурсов создайте подсистему балансировки нагрузки.

    ```powershell
    $mylb = New-AzureRmLoadBalancer -ResourceGroupName contosofabrikam -Name mylb -Location 'West Central US' -FrontendIpConfiguration $frontendIP1 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

11. Добавление hello второй внутренний адрес пула и переднего плана IP конфигурации tooyour только что созданный подсистемы балансировки нагрузки:

    ```powershell
    $mylb = Get-AzureRmLoadBalancer -Name "mylb" -ResourceGroupName $myResourceGroup | Add-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool | Set-AzureRmLoadBalancer

    $mylb | Add-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2 | Set-AzureRmLoadBalancer
    
    Add-AzureRmLoadBalancerRuleConfig -Name HTTP -LoadBalancer $mylb -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80 | Set-AzureRmLoadBalancer
    ```

12. приведенную ниже команду Hello получить hello сетевых адаптеров и затем добавить каждый дополнительный сетевой Адаптер toohello серверный пул адресов из hello оба IP-конфигурации подсистемы балансировки нагрузки:

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

13. Наконец необходимо настроить DNS ресурса записи toopoint toohello соответствующих интерфейсный IP-адрес hello подсистемы балансировки нагрузки. Домены можно разместить в Azure DNS. Дополнительные сведения об использовании Azure DNS с подсистемой балансировки нагрузки см. в разделе [Использование Azure DNS с другими службами Azure](../dns/dns-for-azure-services.md).

## <a name="next-steps"></a>Дальнейшие действия
- Дополнительные сведения о как Балансировка нагрузки toocombine службами в Azure в [с помощью службы балансировки нагрузки в Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).
- Узнайте, как использовать различные типы журналов в Azure toomanage и устранение неполадок подсистемы балансировки нагрузки в [аналитика журналов для балансировки нагрузки Azure](../load-balancer/load-balancer-monitor-log.md).
