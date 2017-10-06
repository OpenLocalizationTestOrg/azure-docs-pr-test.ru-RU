---
title: "aaaCreate Azure с выходом в Интернет загрузить балансировки - PowerShell | Документы Microsoft"
description: "Узнайте, как в toocreate из Интернета в диспетчере ресурсов подсистемы балансировки нагрузки с помощью PowerShell"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 8257f548-7019-417f-b15f-d004a1eec826
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: e4e0e5271bc83c23fc62c0910e784c57d2b30065
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started"></a>Создание балансировщика нагрузки для Интернета в Resource Manager с помощью PowerShell

> [!div class="op_single_selector"]
> * [Портал](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [Интерфейс командной строки Azure](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [Шаблон](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

В этой статье рассматриваются hello модели развертывания диспетчера ресурсов. Вы также можете [узнать, как из Интернета toocreate подсистемы балансировки нагрузки с помощью hello классической модели развертывания](load-balancer-get-started-internet-classic-cli.md).

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-hello-solution-by-using-azure-powershell"></a>Развертывание решения hello с помощью Azure PowerShell

Hello следующих процедур объясняется, как из Интернета toocreate подсистемы балансировки нагрузки с помощью диспетчера ресурсов Azure с помощью PowerShell. С помощью диспетчера ресурсов Azure каждый ресурс создается и настроить отдельно и затем поместить toocreate подсистемы балансировки нагрузки.

Необходимо создать и настроить hello следующие объекты toodeploy подсистемы балансировки нагрузки:

* Конфигурация внешних IP-адресов. Содержит общедоступные IP-адреса для входящего сетевого трафика.
* Пул адресов серверной части: содержит сетевых интерфейсов (NIC) для hello виртуальные машины tooreceive сетевой трафик от подсистемы балансировки нагрузки hello.
* Правила балансировки нагрузки: содержит правила, которые сопоставляют открытый порт на порт tooa подсистемы балансировки нагрузки hello в пул адресов серверной части hello.
* Правила NAT для входящих подключений: содержит правила, которые сопоставляют открытый порт на порт tooa подсистемы балансировки нагрузки hello для конкретной виртуальной машины в пул адресов серверной части hello.
* Зонды: содержит доступность toocheck проверки, используемые работоспособности экземпляров виртуальной машины в пул адресов серверной части hello.

Дополнительные сведения см. в статье [Поддержка диспетчера ресурсов Azure для подсистемы балансировки нагрузки](load-balancer-arm.md).

## <a name="set-up-powershell-toouse-resource-manager"></a>Настройка toouse PowerShell диспетчера ресурсов

Убедитесь, что у вас есть hello последнюю версию рабочего модуля hello Azure Resource Manager для PowerShell:

1. Войдите в tooAzure.

    ```powershell
    Login-AzureRmAccount
    ```

    При появлении запроса введите свои учетные данные.

2. Проверьте hello подписки для учетной записи hello.

    ```powershell
    Get-AzureRmSubscription
    ```

3. Выберите, какие toouse вашей подписки Azure.

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. Создайте группу ресурсов. Если используется существующая группа ресурсов, пропустите этот шаг.

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a>Создайте виртуальную сеть и общедоступный IP-адрес пула IP-интерфейса hello

1. Создайте подсеть и виртуальную сеть.

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    New-AzureRmvirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. Создание Azure открытый ресурс IP-адреса, с именем **общедоступный IP-адрес**, toobe, используемый пулом IP-интерфейса с именем DNS hello **loadbalancernrp.westus.cloudapp.azure.com**. hello, следующая команда использует hello Тип статического выделения.

    ```powershell
    $publicIP = New-AzureRmPublicIpAddress -Name PublicIp -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -DomainNameLabel loadbalancernrp
    ```

   > [!IMPORTANT]
   > Подсистема балансировки нагрузки Hello использует метку домена hello hello общедоступный IP-адрес как префикс для его полного доменного ИМЕНИ. Это отличается от hello классической модели развертывания, который использует hello облачной службы как hello балансировки нагрузки полное доменное имя.
   > В этом примере hello полное доменное имя — **loadbalancernrp.westus.cloudapp.azure.com**.

## <a name="create-a-front-end-ip-pool-and-a-back-end-address-pool"></a>Создание пула внешних IP-адресов и пула внутренних адресов

1. Создание интерфейса пула IP-с именем **внешнего интерфейса балансировки Нагрузки** , использующий hello **общедоступный IP-адрес** ресурсов.

    ```powershell
    $frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PublicIpAddress $publicIP
    ```

2. Создайте пул адресов серверной части с именем **LB-backend**.

    ```powershell
    $beaddresspool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name LB-backend
    ```

## <a name="create-nat-rules-a-load-balancer-rule-a-probe-and-a-load-balancer"></a>Создание правил NAT, правила балансировщика нагрузки, пробы и балансировщика нагрузки

В этом примере создается hello следующих элементов:

* Tootranslate правило NAT, все входящего трафика на tooport 3441 порт 3389
* Tootranslate правило NAT, все входящего трафика на tooport 3442 порт 3389
* Состояние проверки правила toocheck hello работоспособности на страницу с именем **HealthProbe.aspx**
* Toobalance правило балансировки нагрузки весь входящий трафик на порт 80 tooport 80 на hello адресов в пуле hello серверной части
* балансировщик нагрузки, который использует все эти объекты.

Выполните следующие действия.

1. Создание правил NAT hello.

    ```powershell
    $inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP1 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

    $inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP2 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389
    ```

2. Создайте пробу работоспособности. Существует два способа tooconfigure зонда.

    проба HTTP

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    проба TCP.

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -Protocol Tcp -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

3. Создайте правило балансировщика нагрузки.

    ```powershell
    $lbrule = New-AzureRmLoadBalancerRuleConfig -Name HTTP -FrontendIpConfiguration $frontendIP -BackendAddressPool  $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

4. Создайте hello балансировки нагрузки с помощью hello ранее созданных объектов.

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name NRP-LB -Location 'West US' -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

## <a name="create-nics"></a>Создание сетевых адаптеров

Создайте сетевых интерфейсов (или изменить существующие) и связать их tooNAT правила, правила подсистемы балансировки нагрузки и зондов:

1. Получение hello виртуальной сети и подсети виртуальной сети, где hello сетевые адаптеры должны toobe создан.

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. Создайте сетевую КАРТУ с именем **быть балансировки нагрузки сетевого адаптера 1**и связать его с первого правила NAT hello и пул адресов серверной части первый (и единственный) hello.

    ```powershell
    $backendnic1= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic1-be -Location 'West US' -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
    ```

3. Создайте сетевую КАРТУ с именем **балансировки нагрузки nic2 быть**и связать его с hello второе правило NAT и пул адресов серверной части первый (и единственный) hello.

    ```powershell
    $backendnic2= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic2-be -Location 'West US' -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
    ```

4. Проверьте сетевые адаптеры hello.

        $backendnic1

    Ожидаемые выходные данные:

        Name                 : lb-nic1-be
        ResourceGroupName    : NRP-RG
        Location             : westus
        Id                   : /subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
        Etag                 : W/"d448256a-e1df-413a-9103-a137e07276d1"
        ResourceGuid         : 896cac4f-152a-40b9-b079-3e2201a5906e
        ProvisioningState    : Succeeded
        Tags                 :
        VirtualMachine       : null
        IpConfigurations     : [
                            {
                            "Name": "ipconfig1",
                            "Etag": "W/\"d448256a-e1df-413a-9103-a137e07276d1\"",
                            "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/ipconfig1",
                            "PrivateIpAddress": "10.0.2.6",
                            "PrivateIpAllocationMethod": "Static",
                            "Subnet": {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/virtualNetworks/NRPVNet/subnets/LB-Subnet-BE"
                            },
                            "ProvisioningState": "Succeeded",
                            "PrivateIpAddressVersion": "IPv4",
                            "PublicIpAddress": {
                                "Id": null
                            },
                            "LoadBalancerBackendAddressPools": [
                                {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/loadBalancers/NRPlb/backendAddressPools/LB-backend"
                                }
                            ],
                            "LoadBalancerInboundNatRules": [
                                {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/loadBalancers/NRPlb/inboundNatRules/RDP1"
                                }
                            ],
                            "Primary": true,
                            "ApplicationGatewayBackendAddressPools": []
                            }
                        ]
        DnsSettings          : {
                            "DnsServers": [],
                            "AppliedDnsServers": [],
                            "InternalDomainNameSuffix": "prcwibzcuvie5hnxav0yjks2cd.dx.internal.cloudapp.net"
                        }
        EnableIPForwarding   : False
        NetworkSecurityGroup : null
        Primary              :

5. Используйте hello `Add-AzureRmVMNetworkInterface` командлет tooassign hello сетевых адаптеров toodifferent виртуальных машин.

## <a name="create-a-virtual-machine"></a>Создание виртуальной машины

Рекомендации по созданию виртуальной машины и назначении сетевой карты см. в статье [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) (Создание виртуальной машины в Azure с помощью PowerShell).

## <a name="add-hello-network-interface-toohello-load-balancer"></a>Добавление подсистемы балансировки нагрузки toohello hello сетевого интерфейса

1. Получить подсистемы балансировки нагрузки hello из Azure.

    Загрузка ресурсов подсистемы балансировки нагрузки hello в переменной (Если вы еще не сделали, еще). переменная приветствия называется **$lb**. Используйте hello такими же именами из ресурса подсистемы балансировки нагрузки hello, созданного ранее.

    ```powershell
    $lb= get-azurermloadbalancer -name NRP-LB -resourcegroupname NRP-RG
    ```

2. Загрузка hello внутренней tooa переменной конфигурации.

    ```powershell
    $backend=Get-AzureRmLoadBalancerBackendAddressPoolConfig -name LB-backend -LoadBalancer $lb
    ```

3. Загрузка сетевого интерфейса hello уже созданы в переменной. Имя переменной Hello **$nic**. Hello имя сетевого интерфейса является hello один из hello предыдущего примера.

    ```powershell
    $nic =get-azurermnetworkinterface -name lb-nic1-be -resourcegroupname NRP-RG
    ```

4. Изменить конфигурацию серверной части hello в сетевом интерфейсе hello.

    ```powershell
    $nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
    ```

5. Сохраните объект сетевого интерфейса hello.

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```

    После добавления пула внутренней подсистемы балансировки нагрузки toohello сетевого интерфейса, она запускает получения сетевого трафика на основе правил балансировки нагрузки hello для этого ресурса подсистемы балансировки нагрузки.

## <a name="update-an-existing-load-balancer"></a>Обновление существующего балансировщика нагрузки

1. С помощью hello загрузить балансировки из Здравствуйте предыдущий пример, присвоить значение переменной toohello объект подсистемы балансировки нагрузки **$slb** с помощью `Get-AzureLoadBalancer`.

    ```powershell
    $slb = get-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
    ```

2. В следующем примере hello добавьте во входящем правиле NAT — с помощью порт 81 в пуле переднего плана hello и порт 8181 для пула внутренней hello--tooan существующей подсистемы балансировки нагрузки.

    ```powershell
    $slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol TCP
    ```

3. Сохранение hello новую конфигурацию с помощью `Set-AzureLoadBalancer`.

    ```powershell
    $slb | Set-AzureRmLoadBalancer
    ```

## <a name="remove-a-load-balancer"></a>Удалите балансировщика нагрузки.

Команда hello `Remove-AzureLoadBalancer` toodelete подсистемы балансировки нагрузки, начатую с именем **балансировки Нагрузки NRP** в группу ресурсов с именем **NRP RG**.

```powershell
Remove-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
```

> [!NOTE]
> Можно использовать необязательный ключ hello **-Force** tooavoid hello строки для удаления.

## <a name="next-steps"></a>Дальнейшие действия

[Приступая к настройке внутренней подсистемы балансировки нагрузки](load-balancer-get-started-ilb-arm-ps.md)

[Настройка режима распределения подсистемы балансировки нагрузки](load-balancer-distribution-mode.md)

[Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки](load-balancer-tcp-idle-timeout.md)
