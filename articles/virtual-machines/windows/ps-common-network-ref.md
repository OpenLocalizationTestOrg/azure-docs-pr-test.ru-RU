---
title: "команды aaaCommon PowerShell виртуальных сетей Azure | Документы Microsoft"
description: "Общие tooget команд PowerShell, вы начали создание виртуальной сети и его связанные ресурсы для виртуальных машин."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 56e1a73c-8299-4996-bd03-f74585caa1dc
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: b46b78f1b7c5a0c5ba917fb48f568d871e5e8789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="common-powershell-commands-for-azure-virtual-networks"></a>Общие команды PowerShell для виртуальных сетей Azure

Если требуется, чтобы toocreate виртуальной машины, необходимо toocreate [виртуальной сети](../../virtual-network/virtual-networks-overview.md) или знать о существующей виртуальной сети, в которой hello виртуальной Машины может быть добавлен. Как правило при создании виртуальной Машины, необходимо также tooconsider Создание ресурсов hello, описанных в этой статье.

В разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) сведения об установке hello последнюю версию Azure PowerShell, выбрав подписку и вход в учетную запись tooyour.

Некоторые переменные могут быть полезными для вас, если работает несколько команд hello в этой статье:

- $location - расположение hello hello сетевых ресурсов. Можно использовать [Get AzureRmLocation](https://docs.microsoft.com/powershell/module/azurerm.resources/get-azurermlocation) toofind [географический регион](https://azure.microsoft.com/regions/) , которые работают для вас.
- $myResourceGroup - hello имя группы ресурсов hello, где расположены hello сетевым ресурсам.

## <a name="create-network-resources"></a>Создание сетевых ресурсов

| Задача | Команда |
| ---- | ------- |
| Создание конфигураций подсети |$subnet1 = [New-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) -Name "mySubnet1" -AddressPrefix XX.X.X.X/XX<BR>$subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnet2" -AddressPrefix XX.X.X.X/XX<BR><BR>В обычной сети может быть подсеть для [балансировщика нагрузки с выходом в Интернет](../../load-balancer/load-balancer-internet-overview.md) и отдельная подсеть для [внутреннего балансировщика нагрузки](../../load-balancer/load-balancer-internal-overview.md). |
| Создать виртуальную сеть |$vnet = [New-AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermvirtualnetwork) -Name "myVNet" -ResourceGroupName $myResourceGroup -Location $location -AddressPrefix XX.X.X.X/XX -Subnet $subnet1, $subnet2 |
| Проверка доменного имени на уникальность |[Test-AzureRmDnsAvailability](https://docs.microsoft.com/powershell/module/azurerm.network/test-azurermdnsavailability) -DomainNameLabel "myDNS" -Location $location<BR><BR>Можно указать имя домена DNS для [открытый IP-ресурс](../../virtual-network/virtual-network-ip-addresses-overview-arm.md), который создает сопоставление для domainname.location.cloudapp.azure.com toohello общедоступный IP-адрес в hello Azure под управлением DNS-серверов. Hello имя может содержать только буквы, цифры и дефисы. Hello первый и последний символ должен быть буквой или цифрой и hello доменное имя должно быть уникальным в пределах его расположение в Azure. Если возвращается значение **True**, то предложенное имя является глобально уникальным. |
| Создание общедоступного IP-адреса |$pip = [New-AzureRmPublicIpAddress](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermpublicipaddress) -Name "myPublicIp" -ResourceGroupName $myResourceGroup -DomainNameLabel "myDNS" -Location $location -AllocationMethod Dynamic<BR><BR>Hello общедоступный IP-адрес использует hello доменное имя, которое ранее протестированы и использования конфигурации hello переднего плана подсистемы балансировки нагрузки hello. |
| Создание интерфейсной IP-конфигурации |$frontendIP = [New-AzureRmLoadBalancerFrontendIpConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig) -Name "myFrontendIP" -PublicIpAddress $pip<BR><BR>Конфигурация внешнего интерфейса Hello включает hello общедоступный IP-адрес, созданный ранее для входящего сетевого трафика. |
| Создание внутреннего пула адресов |$beAddressPool = [New-AzureRmLoadBalancerBackendAddressPoolConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig) -Name "myBackendAddressPool"<BR><BR>Предоставляет внутренние адреса для внутреннего hello объекта hello нагрузки балансировки, осуществляется через сетевой интерфейс. |
| Создание пробы |$healthProbe = [New-AzureRmLoadBalancerProbeConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) -Name "myProbe" -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2<BR><BR>Содержит доступность toocheck проверки, используемые работоспособности экземпляров виртуальных машин в hello серверный пул адресов. |
| Создание правила балансировки нагрузки |$lbRule = [New-AzureRmLoadBalancerRuleConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) -Name HTTP -FrontendIpConfiguration $frontendIP -BackendAddressPool $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80<BR><BR>Содержит правила, назначить общий порт в подсистеме балансировки нагрузки hello tooa порт в hello серверный пул адресов. |
| Создание правила NAT для входящего трафика |$inboundNATRule = [New-AzureRmLoadBalancerInboundNatRuleConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerinboundnatruleconfig) -Name "myInboundRule1" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389<BR><BR>Содержит правила, сопоставление порта открытый порт tooa подсистемы балансировки нагрузки hello для конкретной виртуальной машины в hello серверный пул адресов. |
| Создание балансировщика нагрузки |$loadBalancer = [New-AzureRmLoadBalancer](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancer) -ResourceGroupName $myResourceGroup -Name "myLoadBalancer" -Location $location -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule -LoadBalancingRule $lbRule -BackendAddressPool $beAddressPool -Probe $healthProbe |
| Создание сетевого интерфейса |$nic1= [New-AzureRmNetworkInterface](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermnetworkinterface) -ResourceGroupName $myResourceGroup -Name "myNIC" -Location $location -PrivateIpAddress XX.X.X.X -Subnet $subnet2 -LoadBalancerBackendAddressPool $loadBalancer.BackendAddressPools[0] -LoadBalancerInboundNatRule $loadBalancer.InboundNatRules[0]<BR><BR>Создание сетевого интерфейса с помощью hello общедоступный IP-адрес и подсеть виртуальной сети, созданный ранее. |

## <a name="get-information-about-network-resources"></a>Получение сведений о сетевых ресурсах

| Задача | Команда |
| ---- | ------- |
| Получение списка виртуальных сетей |[Get-AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermvirtualnetwork) -ResourceGroupName $myResourceGroup<BR><BR>Список всех виртуальных сетей hello в группе ресурсов hello. |
| Получение сведений о виртуальной сети |Get-AzureRmVirtualNetwork -Name "myVNet" -ResourceGroupName $myResourceGroup |
| Получение списка подсетей в виртуальной сети |Get-AzureRmVirtualNetwork -Name "myVNet" -ResourceGroupName $myResourceGroup &#124; Select Subnets |
| Получение сведений о подсети |[Get-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) -Name "mySubnet1" -VirtualNetwork $vnet<BR><BR>Возвращает сведения о подсети hello в hello указанной виртуальной сети. значение Hello $vnet представляет hello объекта, возвращаемого Get-AzureRmVirtualNetwork. |
| Получение списка IP-адресов |[Get-AzureRmPublicIpAddress](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermpublicipaddress) -ResourceGroupName $myResourceGroup<BR><BR>Список общих IP-адресов hello в группе ресурсов hello. |
| Получение списка балансировщиков нагрузки |[Get-AzureRmLoadBalancer](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermloadbalancer) -ResourceGroupName $myResourceGroup<BR><BR>Список всех подсистем балансировки нагрузки hello в группе ресурсов hello. |
| Получение списка сетевых интерфейсов |[Get-AzureRmNetworkInterface](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermnetworkinterface) -ResourceGroupName $myResourceGroup<BR><BR>Список всех сетевых интерфейсов hello в группе ресурсов hello. |
| Получение сведений о виртуальном интерфейсе |Get-AzureRmNetworkInterface -Name "myNIC" -ResourceGroupName $myResourceGroup<BR><BR>Получение сведений об определенном сетевом интерфейсе. |
| Получить hello IP-конфигурации сетевого интерфейса |[Get-AzureRmNetworkInterfaceIPConfig](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermnetworkinterfaceipconfig) -Name "myNICIP" -NetworkInterface $nic<BR><BR>Получает сведения о конфигурации IP hello hello указанного сетевого интерфейса. значение Hello $nic представляет hello объекта, возвращаемого Get-AzureRmNetworkInterface. |

## <a name="manage-network-resources"></a>Управление сетевыми ресурсами

| Задача | Команда |
| ---- | ------- |
| Добавить виртуальную сеть tooa подсети |[Add-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig) -AddressPrefix XX.X.X.X/XX -Name "mySubnet1" -VirtualNetwork $vnet<BR><BR>Добавляет подсети tooan существующей виртуальной сети. значение Hello $vnet представляет hello объекта, возвращаемого Get-AzureRmVirtualNetwork. |
| Удаление виртуальной сети |[Remove-AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/module/azurerm.network/remove-azurermvirtualnetwork) -Name "myVNet" -ResourceGroupName $myResourceGroup<BR><BR>Удаляет указанный виртуальный сетевой hello из группы ресурсов hello. |
| Удаление сетевого интерфейса |[Remove-AzureRmNetworkInterface](https://docs.microsoft.com/powershell/module/azurerm.network/remove-azurermnetworkinterface) -Name "myNIC" -ResourceGroupName $myResourceGroup<BR><BR>Удаляет указанного сетевого интерфейса hello из группы ресурсов hello. |
| Удаление балансировщика нагрузки |[Remove-AzureRmLoadBalancer](https://docs.microsoft.com/powershell/module/azurerm.network/remove-azurermloadbalancer) -Name "myLoadBalancer" -ResourceGroupName $myResourceGroup<BR><BR>Удаляет hello указан балансировки нагрузки из группы ресурсов hello. |
| Удаление общедоступного IP-адреса |[Remove-AzureRmPublicIpAddress](https://docs.microsoft.com/powershell/module/azurerm.network/remove-azurermpublicipaddress)-Name "myIPAddress" -ResourceGroupName $myResourceGroup<BR><BR>Удаляет hello указан общедоступный IP-адрес из группы ресурсов hello. |

## <a name="next-steps"></a>Дальнейшие действия
* Используйте hello сетевого интерфейса, который только что созданным при вы [создания виртуальной Машины](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Узнайте, как можно [создать виртуальную машину с несколькими сетевыми интерфейсами](../../virtual-network/virtual-networks-multiple-nics.md).

