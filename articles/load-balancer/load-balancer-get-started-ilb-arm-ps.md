---
title: "aaaCreate Azure внутренним загрузить балансировки - PowerShell | Документы Microsoft"
description: "Узнайте, как с помощью PowerShell в диспетчере ресурсов подсистемы балансировки нагрузки, toocreate во внутренний"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: c6c98981-df9d-4dd7-a94b-cc7d1dc99369
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 4b9657c77aa32a142de49ff7871ed6a396b22223
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-using-powershell"></a>Создание внутреннего балансировщика нагрузки с помощью PowerShell

> [!div class="op_single_selector"]
> * [портале Azure](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [Интерфейс командной строки Azure](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [Шаблон](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).  В этой статье описывается использование модели развертывания диспетчера ресурсов hello, который рекомендуется в большинстве случаев новый вместо hello [классической модели развертывания](load-balancer-get-started-ilb-classic-ps.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

Hello следующие шаги поясняют, как с помощью диспетчера ресурсов Azure с помощью PowerShell подсистемы балансировки нагрузки, toocreate во внутренней. С помощью диспетчера ресурсов Azure toocreate элементы hello внутренний балансировщик настраиваются отдельно, а затем объединяются toocreate подсистемы балансировки нагрузки.

Требуется toocreate и настроить hello следующие объекты toodeploy подсистемы балансировки нагрузки:

* Внешняя конечного IP-конфигурации — настроит hello частный IP-адрес для входящего сетевого трафика
* Серверный пул адресов - настроит hello сетевых интерфейсов, которые получат трафик с балансировкой нагрузки hello из пула IP-адресов внешнего интерфейса
* Правила балансировки нагрузки - источника и конфигурацию локального порта для hello подсистемы балансировки нагрузки.
* Проверяет - настраивает модуль проверки состояния работоспособности hello для экземпляров виртуальных машин hello.
* Правила NAT для входящих подключений - настраивает hello правила порта toodirectly доступа одного из экземпляров виртуальных машин hello.

Дополнительные сведения о настройке компонентов балансировщика нагрузки с помощью Azure Resource Manager см. в статье [Поддержка диспетчера ресурсов Azure для подсистемы балансировки нагрузки](load-balancer-arm.md).

Hello следующие шаги поясняют, как tooconfigure балансировки нагрузки между двумя виртуальными машинами.

## <a name="setup-powershell-toouse-resource-manager"></a>Toouse установки PowerShell диспетчера ресурсов

Убедитесь, что имеется hello последнюю рабочей версии hello модуль Azure для PowerShell и приняты установки правильно tooaccess подписки Azure PowerShell.

### <a name="step-1"></a>Шаг 1

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a>Шаг 2

Проверьте hello подписки для учетной записи hello

```powershell
Get-AzureRmSubscription
```

Запрос tooAuthenticate можно с помощью учетных данных.

### <a name="step-3"></a>Шаг 3.

Выберите, какие toouse вашей подписки Azure.

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="create-resource-group-for-load-balancer"></a>Создание группы ресурсов для подсистемы балансировки нагрузки

Создайте группу ресурсов (пропустите этот шаг, если вы используете существующую группу).

```powershell
New-AzureRmResourceGroup -Name NRP-RG -location "West US"
```

В диспетчере ресурсов Azure для всех групп ресурсов должно быть указано расположение. Используется как расположение по умолчанию hello для ресурсов в этой группе ресурсов. Убедитесь, что все команды, которые будет использовать подсистему балансировки нагрузки toocreate hello же группе ресурсов.

В hello в примере выше мы создали группу ресурсов под названием «NRP RG» и расположение «West US».

## <a name="create-virtual-network-and-a-private-ip-address-for-front-end-ip-pool"></a>Создание виртуальной сети и общедоступного IP-адреса для пула IP-адресов клиентской части

Создает подсеть для виртуальной сети hello и назначает toovariable $backendSubnet

```powershell
$backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
```

Создайте виртуальную сеть:

```powershell
$vnet= New-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
```

Создает виртуальную сеть hello и добавляет hello подсети toohello быть балансировки нагрузки подсети виртуальной сети NRPVNet и назначает toovariable $vnet

## <a name="create-front-end-ip-pool-and-backend-address-pool"></a>Создание пула IP-адресов клиентской части и пула адресов серверной части

Настройка пулу IP-интерфейса для входящих hello загрузить балансировки сетевой трафик и трафик с балансировкой нагрузки внутренний адрес пула tooreceive hello.

### <a name="step-1"></a>Шаг 1

Создайте пул IP-интерфейс, с помощью hello частный IP-адрес 10.0.2.5 для hello подсети 10.0.2.0/24 которого будет конечной точкой входящего сетевого трафика hello.

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PrivateIpAddress 10.0.2.5 -SubnetId $vnet.subnets[0].Id
```

### <a name="step-2"></a>Шаг 2

Настройте пул адресов серверной части использования tooreceive входящего трафика из пула IP-адресов внешнего интерфейса:

```powershell
$beaddresspool= New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "LB-backend"
```

## <a name="create-lb-rules-nat-rules-probe-and-load-balancer"></a>Создание правил балансировки нагрузки, правил преобразования сетевых адресов, пробы и подсистемы балансировки нагрузки

После создания пула IP-адресов внешнего интерфейса hello и hello серверный пул адресов, вам потребуется toocreate hello правил, которые будут принадлежать ресурс балансировки нагрузки toohello:

### <a name="step-1"></a>Шаг 1

```powershell
$inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP1" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

$inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP2" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389

$healthProbe = New-AzureRmLoadBalancerProbeConfig -Name "HealthProbe" -RequestPath "HealthProbe.aspx" -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name "HTTP" -FrontendIpConfiguration $frontendIP -BackendAddressPool $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
```

приведенном выше примере Hello создает hello следующих элементов:

* Правило NAT, которое все входящие трафика tooport 3441 перейдет tooport 3389.
* Второе правило NAT, которой все входящие трафика tooport 3442 перейдет tooport 3389.
* правило подсистемы балансировки нагрузки, которая будет загружать сбалансировать весь входящий трафик на открытый порт 80 toolocal порт 80 в пул адресов серверной части hello.
* правило проверки, которое будет проверять состояние работоспособности hello для пути «HealthProbe.aspx»

### <a name="step-2"></a>Шаг 2

Создайте балансировки нагрузки hello сложения всех объектов (правил NAT, правила подсистемы балансировки нагрузки, проверки конфигурации):

```powershell
$NRPLB = New-AzureRmLoadBalancer -ResourceGroupName "NRP-RG" -Name "NRP-LB" -Location "West US" -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
```

## <a name="create-network-interfaces"></a>Создание сетевых интерфейсов

После создания hello внутренней подсистемы балансировки нагрузки, необходимо определить, какие сетевые интерфейсы будет получать hello входящих сетевой трафик с балансировкой нагрузки, правила преобразования сетевых адресов и проверки. в этом случае Hello сетевой интерфейс настраивается индивидуально и могут назначаться tooa виртуальной машины позднее.

### <a name="step-1"></a>Шаг 1

Получите ресурс hello виртуальной сети и подсети toocreate сетевых интерфейсов:

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG

$backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
```

На этом шаге создается сетевого интерфейса, которой будет принадлежать пула серверной части подсистемы балансировки нагрузки toohello и свяжите hello первого правила NAT для протокола удаленного рабочего СТОЛА для данного сетевого интерфейса:

```powershell
$backendnic1= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic1-be -Location "West US" -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
```

### <a name="step-2"></a>Шаг 2

Создайте второй сетевой интерфейс с названием «LB-Nic2-BE»:

На этом шаге создается второго сетевого интерфейса, назначение toohello же балансировки нагрузки обратно завершить пула и связывание hello второе правило NAT для протокола удаленного рабочего СТОЛА:

```powershell
$backendnic2= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic2-be -Location "West US" -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
```

конечным результатом Hello отобразится hello следующее:

    $backendnic1

Ожидаемые выходные данные:

    Name                 : lb-nic1-be
    ResourceGroupName    : NRP-RG
    Location             : westus
    Id                   : /subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
    Etag                 : W/"d448256a-e1df-413a-9103-a137e07276d1"
    ProvisioningState    : Succeeded
    Tags                 :
    VirtualMachine       : null
    IpConfigurations     : [
                         {
                           "PrivateIpAddress": "10.0.2.6",
                           "PrivateIpAllocationMethod": "Static",
                           "Subnet": {
                             "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/virtualNetworks/NRPVNet/subnets/LB-Subnet-BE"
                           },
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
                           "ProvisioningState": "Succeeded",
                           "Name": "ipconfig1",
                           "Etag": "W/\"d448256a-e1df-413a-9103-a137e07276d1\"",
                           "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/ipconfig1"
                         }
                       ]
    DnsSettings          : {
                         "DnsServers": [],
                         "AppliedDnsServers": []
                       }
    AppliedDnsSettings   :
    NetworkSecurityGroup : null
    Primary              : False



### <a name="step-3"></a>Шаг 3.

Используйте hello команду Add-AzureRmVMNetworkInterface tooassign hello Сетевых tooa виртуальную машину.

Здравствуйте, пошаговые процедуры toocreate виртуальной машины и назначить tooa сетевого Адаптера можно найти следующие документации hello: [создать ВМ Azure с помощью PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).

## <a name="add-hello-network-interface"></a>Добавьте сетевой интерфейс hello

Если уже имеется созданная виртуальная машина, вы можете добавить hello сетевого интерфейса с hello следующие шаги:

### <a name="step-1"></a>Шаг 1

Загрузка ресурсов подсистемы балансировки нагрузки hello в переменной (Если вы еще не сделали, еще). Hello переменная, используемая является именем $lb и приветствия используйте одинаковые имена из ресурса подсистемы балансировки нагрузки hello созданной ранее.

```powershell
$lb = Get-AzureRmLoadBalancer –name NRP-LB -resourcegroupname NRP-RG
```

### <a name="step-2"></a>Шаг 2

Загрузка конфигурации tooa hello серверной переменной.

```powershell
$backend = Get-AzureRmLoadBalancerBackendAddressPoolConfig -name backendpool1 -LoadBalancer $lb
```

### <a name="step-3"></a>Шаг 3.

Загрузка сетевого интерфейса hello уже созданы в переменной. использовать имя переменной Hello — $ сетевого адаптера. в приведенном выше примере hello Hello используется имя сетевого интерфейса является hello таким же.

```powershell
$nic = Get-AzureRmNetworkInterface –name lb-nic1-be -resourcegroupname NRP-RG
```

### <a name="step-4"></a>Шаг 4.

Измените конфигурацию серверной части hello в сетевом интерфейсе hello.

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
```

### <a name="step-5"></a>Шаг 5

Сохраните объект сетевого интерфейса hello.

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

После добавления сетевого интерфейса внутренний пул подсистемы балансировки нагрузки toohello запуске получения сетевого трафика на основе правила для этого ресурса подсистемы балансировки нагрузки подсистемы балансировки нагрузки hello.

## <a name="update-an-existing-load-balancer"></a>Обновление существующего балансировщика нагрузки

### <a name="step-1"></a>Шаг 1
С помощью подсистемы балансировки нагрузки hello в приведенном выше примере hello, назначьте toovariable объект подсистемы балансировки нагрузки с помощью Get-AzureRmLoadBalancer $slb

```powershell
$slb = Get-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

### <a name="step-2"></a>Шаг 2

В следующем примере hello будет добавить новое правило NAT для входящего трафика через порт 81 в hello переднего плана и порт 8181 резервному hello окончания пула tooan существующей подсистемы балансировки нагрузки

```powershell
$slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol Tcp
```

### <a name="step-3"></a>Шаг 3.

Сохранить hello новую конфигурацию с помощью набора AzureLoadBalancer

```powershell
$slb | Set-AzureRmLoadBalancer
```

## <a name="remove-a-load-balancer"></a>Удалите балансировщика нагрузки.

Используйте hello команду Remove-AzureRmLoadBalancer toodelete подсистемы балансировки нагрузки начатую с именем «NRP-балансировки Нагрузки» в группе ресурсов называется «NRP RG»

```powershell
Remove-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

> [!NOTE]
> Можно использовать необязательный hello переключения - Force tooavoid hello строки для удаления.

## <a name="next-steps"></a>Дальнейшие действия

[Настройка режима распределения подсистемы балансировки нагрузки](load-balancer-distribution-mode.md)

[Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки](load-balancer-tcp-idle-timeout.md)
