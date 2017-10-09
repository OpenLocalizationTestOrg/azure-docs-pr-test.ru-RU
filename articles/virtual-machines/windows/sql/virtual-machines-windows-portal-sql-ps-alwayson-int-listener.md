---
title: "aaaConfigure всегда на прослушиватели группы доступности — Microsoft Azure | Документы Microsoft"
description: "Настройте прослушиватели группы доступности на модели hello диспетчера ресурсов Azure, используя внутренний балансировщик нагрузки с помощью одного или нескольких IP-адресов."
services: virtual-machines
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: monicar
ms.assetid: 14b39cde-311c-4ddf-98f3-8694e01a7d3b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/22/2017
ms.author: mikeray
ms.openlocfilehash: 81edfe2c2ea536d8dcec466f36fccf8bc0e02c2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-one-or-more-always-on-availability-group-listeners---resource-manager"></a>Настройка одного или нескольких прослушивателей групп доступности AlwaysOn в модели Resource Manager
В этой статье вы узнаете, как:

* создать внутренний балансировщик нагрузки для групп доступности SQL Server с помощью командлетов PowerShell;
* Добавление дополнительных IP адресов tooa подсистемы балансировки нагрузки по более чем одной группы доступности. 

Прослушиватель группы доступности является имя виртуальной сети, чтобы клиенты могли подключаться toofor доступ к базе данных. На виртуальных машинах Azure подсистемы балансировки нагрузки содержит hello IP-адрес для прослушивателя hello. маршруты подсистемы балансировки нагрузки Hello трафик toohello экземпляра SQL Server, который прослушивает порт пробы hello. Обычно группа доступности использует внутреннюю подсистему балансировки нагрузки. В такой системе можно разместить один или несколько IP-адресов. Каждый IP-адрес использует определенный порт пробы. В этом документе показано, как toocreate toouse PowerShell подсистему балансировки нагрузки или добавьте IP-адреса tooan существующей подсистемы балансировки нагрузки для группы доступности SQL Server. 

Здравствуйте, возможность tooassign нескольких IP адресов tooan внутренняя Подсистема балансировки нагрузки — новый tooAzure и доступна только в модели диспетчера ресурсов. toocomplete этой задачи необходимо toohave развернуты группы доступности SQL Server на виртуальных машинах Azure в модель диспетчера ресурсов. Обе виртуальные машины SQL Server должны принадлежать toohello одной группе доступности. Можно использовать hello [шаблона Microsoft](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) tooautomatically Создание группы доступности hello в диспетчере ресурсов Azure. Этот шаблон автоматически создает группу доступности hello, включая hello внутренней подсистемы балансировки нагрузки. При необходимости можно [вручную настроить группу доступности AlwaysOn](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).

Здесь предполагается, что группы доступности уже настроены.  

Связанные разделы включают:

* [Настройка групп доступности AlwaysOn в виртуальной машине Azure (графический пользовательский интерфейс)](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)   
* [Настройка подключения между виртуальными сетями с помощью Azure Resource Manager и PowerShell](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

[!INCLUDE [Start your PowerShell session](../../../../includes/sql-vm-powershell.md)]

## <a name="configure-hello-windows-firewall"></a>Настройка брандмауэра Windows hello
Настройка доступа к SQL Server tooallow брандмауэра Windows hello. правила брандмауэра Hello разрешить потребление toohello подключений TCP-порты, экземпляр SQL Server hello и пробы прослушивателя hello. Дополнительные сведения см. в разделе [Настройка брандмауэра Windows для доступа к ядру СУБД](http://msdn.microsoft.com/library/ms175043.aspx#Anchor_1). Создайте правило входящего подключения для hello порт SQL Server и для порта пробы hello.

## <a name="example-script-create-an-internal-load-balancer-with-powershell"></a>Пример сценария. Создание внутреннего балансировщика нагрузки с помощью PowerShell
> [!NOTE]
> Если вы создали свою группу доступности с hello [шаблона Microsoft](virtual-machines-windows-portal-sql-alwayson-availability-groups.md), hello внутренней подсистемы балансировки нагрузки уже был создан. 
> 
> 

Hello следующий сценарий PowerShell создает внутренний балансировщик нагрузки, настраивает правила подсистемы балансировки нагрузки hello и задает IP-адрес для hello подсистемы балансировки нагрузки. сценарий toorun hello, откройте Windows PowerShell ISE и вставьте скрипт hello в области сценариев hello. Используйте `Login-AzureRMAccount` toolog в tooPowerShell. Если у вас несколько подписок Azure, используйте `Select-AzureRmSubscription ` tooset hello подписки. 

```powershell
# Login-AzureRmAccount
# Select-AzureRmSubscription -SubscriptionId <xxxxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx>

$ResourceGroupName = "<Resource Group Name>" # Resource group name
$VNetName = "<Virtual Network Name>"         # Virtual network name
$SubnetName = "<Subnet Name>"                # Subnet name
$ILBName = "<Load Balancer Name>"            # ILB name
$Location = "<Azure Region>"                 # Azure location
$VMNames = "<VM1>","<VM2>"                   # Virtual machine names

$ILBIP = "<n.n.n.n>"                         # IP address
[int]$ListenerPort = "<nnnn>"                # AG listener port
[int]$ProbePort = "<nnnn>"                   # Probe port

$LBProbeName ="ILBPROBE_$ListenerPort"       # hello Load balancer Probe Object Name              
$LBConfigRuleName = "ILBCR_$ListenerPort"    # hello Load Balancer Rule Object Name

$FrontEndConfigurationName = "FE_SQLAGILB_1" # Object name for hello front-end configuration 
$BackEndConfigurationName ="BE_SQLAGILB_1"   # Object name for hello back-end configuration

$VNet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName 

$Subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $VNet -Name $SubnetName 

$FEConfig = New-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -PrivateIpAddress $ILBIP -SubnetId $Subnet.id

$BEConfig = New-AzureRMLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName 

$SQLHealthProbe = New-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -Protocol tcp -Port $ProbePort -IntervalInSeconds 15 -ProbeCount 2

$ILBRule = New-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig -BackendAddressPool $BEConfig -Probe $SQLHealthProbe -Protocol tcp -FrontendPort $ListenerPort -BackendPort $ListenerPort -LoadDistribution Default -EnableFloatingIP 

$ILB= New-AzureRmLoadBalancer -Location $Location -Name $ILBName -ResourceGroupName $ResourceGroupName -FrontendIpConfiguration $FEConfig -BackendAddressPool $BEConfig -LoadBalancingRule $ILBRule -Probe $SQLHealthProbe 

$bepool = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB 

foreach($VMName in $VMNames)
    {
        $VM = Get-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VMName 
        $NICName = ($vm.NetworkProfile.NetworkInterfaces.Id.split('/') | select -last 1)
        $NIC = Get-AzureRmNetworkInterface -name $NICName -ResourceGroupName $ResourceGroupName
        $NIC.IpConfigurations[0].LoadBalancerBackendAddressPools = $BEPool
        Set-AzureRmNetworkInterface -NetworkInterface $NIC
        start-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VM.Name 
    }
```

## <a name="Add-IP"></a>Пример сценария: Добавление IP адрес tooan существующей подсистемы балансировки нагрузки с помощью PowerShell
toouse больше, чем к одной группе доступности, добавить дополнительные IP адрес toohello подсистемы балансировки нагрузки. Каждому IP-адресу требуется собственное правило балансировки нагрузки, порт пробы и внешний порт.

Hello переднего плана используется порт hello использование экземпляра SQL Server toohello tooconnect приложениями. IP-адресов для различных групп доступности можно используйте hello же интерфейсный порт.

> [!NOTE]
> Для групп доступности SQL Server для каждого IP-адреса требуется определенный порт пробы. Например, если один IP-адрес в балансировщике нагрузки использует порт пробы 59999, другие IP-адреса не могут использовать этот порт пробы.

* Дополнительные сведения об ограничениях см. в пункте **Частный внешний IP-адрес на балансировщик нагрузки** раздела [Ограничения сети — Azure Resource Manager](../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits).
* Дополнительные сведения об ограничениях групп доступности см. в разделе [Ограничения (группы доступности)](http://msdn.microsoft.com/library/ff878487.aspx#RestrictionsAG).

Hello следующий сценарий добавляет новый IP адрес tooan существующей подсистемы балансировки нагрузки. Hello ILB использует порт прослушивателя hello hello балансировки интерфейсный порт. Этот порт может быть hello порт, прослушиваемый SQL Server. Для экземпляров SQL Server по умолчанию порт hello — 1433. правила для группы доступности балансировки нагрузки Hello требует плавающий IP-адрес (прямой возврат сервера), порт внутренней hello hello же, как интерфейсный порт hello. Обновите hello переменные среды. 

```powershell
# Login-AzureRmAccount
# Select-AzureRmSubscription -SubscriptionId <xxxxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx>

$ResourceGroupName = "<ResourceGroup>"          # Resource group name
$VNetName = "<VirtualNetwork>"                  # Virtual network name
$SubnetName = "<Subnet>"                        # Subnet name
$ILBName = "<ILBName>"                          # ILB name                      

$ILBIP = "<n.n.n.n>"                            # IP address
[int]$ListenerPort = "<nnnn>"                   # AG listener port
[int]$ProbePort = "<nnnnn>"                     # Probe port 

$ILB = Get-AzureRmLoadBalancer -Name $ILBName -ResourceGroupName $ResourceGroupName 

$count = $ILB.FrontendIpConfigurations.Count+1
$FrontEndConfigurationName ="FE_SQLAGILB_$count"  

$LBProbeName = "ILBPROBE_$count"
$LBConfigrulename = "ILBCR_$count"

$VNet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName 
$Subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $VNet -Name $SubnetName

$ILB | Add-AzureRmLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -PrivateIpAddress $ILBIP -SubnetId $Subnet.Id 

$ILB | Add-AzureRmLoadBalancerProbeConfig -Name $LBProbeName  -Protocol Tcp -Port $Probeport -ProbeCount 2 -IntervalInSeconds 15  | Set-AzureRmLoadBalancer 

$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName

$FEConfig = get-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB

$SQLHealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

$BEConfig = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $ILB.BackendAddressPools[0].Name -LoadBalancer $ILB 

$ILB | Add-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig  -BackendAddressPool $BEConfig -Probe $SQLHealthProbe -Protocol tcp -FrontendPort  $ListenerPort -BackendPort $ListenerPort -LoadDistribution Default -EnableFloatingIP | Set-AzureRmLoadBalancer   
```

## <a name="configure-hello-listener"></a>Настройте прослушиватель hello

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-hello-listener-port-in-sql-server-management-studio"></a>Задайте порт прослушивателя hello в SQL Server Management Studio

1. Запустите SQL Server Management Studio и подключитесь toohello первичной реплики.

1. Перейдите в слишком**высокий уровень доступности AlwaysOn** | **группы доступности** | **прослушиватели группы доступности**. 

1. Теперь вы увидите имя прослушивателя hello, созданный в диспетчере отказоустойчивости кластеров. Щелкните правой кнопкой мыши имя прослушивателя hello и нажмите кнопку **свойства**.

1. В hello **порт** укажите hello номер порта для прослушивателя группы доступности hello $EndpointPort ранее с помощью hello (по умолчанию hello — 1433), затем нажмите кнопку **ОК**.

## <a name="test-hello-connection-toohello-listener"></a>Подключение toohello теста hello прослушивателя

подключение к tootest hello:

1. Tooa RDP сервера SQL в hello виртуальных сетевых, но не собственные hello реплики. Это может быть hello другие серверы SQL Server в кластере hello.

1. Используйте **sqlcmd** программа tootest hello соединения. Например, следующий скрипт hello устанавливает **sqlcmd** toohello первичной подключения через прослушиватель hello с проверкой подлинности Windows:
   
    ```
    sqlmd -S <listenerName> -E
    ```
   
    Если прослушиватель hello не использует порт hello по умолчанию порт (1433), укажите порт hello в строке подключения hello. Например hello следующие команды sqlcmd подключается tooa прослушивания по порту 1435: 
   
    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

Hello SQLCMD подключения автоматически подключается toowhichever экземпляра SQL Server узлов hello первичной реплики. 

> [!NOTE]
> Убедитесь, что открыт порт hello, указываемые на брандмауэре hello и серверов SQL. Оба сервера требуют входящее правило для hello TCP-порт, который можно использовать. Дополнительные сведения см. в статье [Добавление и изменение правила брандмауэра](http://technet.microsoft.com/library/cc753558.aspx). 
> 
> 

## <a name="guidelines-and-limitations"></a>Рекомендации и ограничения
Обратите внимание hello следовать рекомендациям прослушивателя группы доступности в Azure с помощью внутренней подсистемы балансировки нагрузки.

* С внутренней подсистемы балансировки нагрузки, только доступ прослушиватель hello в hello одной виртуальной сети.


## <a name="for-more-information"></a>Дополнительные сведения
Дополнительные сведения см. в статье [Введение в группы доступности AlwaysOn SQL Server на виртуальных машинах Azure](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).

## <a name="powershell-cmdlets"></a>Командлеты PowerShell
Используйте следующие командлеты PowerShell toocreate внутренний балансировщик нагрузки для виртуальных машин Azure hello.

* Командлет [New-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt619450.aspx) создает подсистему балансировки нагрузки. 
* Командлет [New-AzureRMLoadBalancerFrontendIpConfig](http://msdn.microsoft.com/library/mt603510.aspx) создает конфигурацию внешних IP-адресов для подсистемы балансировки нагрузки. 
* Командлет [New-AzureRmLoadBalancerRuleConfig](http://msdn.microsoft.com/library/mt619391.aspx) создает конфигурацию правила для подсистемы балансировки нагрузки. 
* Командлет [New-AzureRmLoadBalancerBackendAddressPoolConfig](http://msdn.microsoft.com/library/mt603791.aspx) создает конфигурацию внутреннего пула IP-адресов для подсистемы балансировки нагрузки. 
* Командлет [New-AzureRmLoadBalancerProbeConfig](http://msdn.microsoft.com/library/mt603847.aspx) создает конфигурацию пробы для подсистемы балансировки нагрузки.
* Командлет [Remove-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt603862.aspx) удаляет подсистему балансировки нагрузки из группы ресурсов Azure.
