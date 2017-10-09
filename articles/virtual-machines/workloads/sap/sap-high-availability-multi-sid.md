---
title: "aaaCreate конфигурации multi-SID SAP в Azure | Документы Microsoft"
description: "Конфигурации multi-SID руководство toohigh доступности SAP NetWeaver на виртуальных машинах"
services: virtual-machines-windows, virtual-network, storage
documentationcenter: saponazure
author: goraco
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 0b89b4f8-6d6c-45d7-8d20-fe93430217ca
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/05/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e2a4b12928231743c59af86dab72595ad38d364b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-sap-netweaver-multi-sid-configuration"></a>Создание конфигурации с несколькими идентификаторами безопасности SAP NetWeaver

[load-balancer-multivip-overview]:../../../load-balancer/load-balancer-multivip-overview.md
[sap-ha-guide]:sap-high-availability-guide.md 
[sap-ha-guide-figure-6001]:./media/virtual-machines-shared-sap-high-availability-guide/6001-sap-multi-sid-ascs-scs-sid1.png
[sap-ha-guide-figure-6002]:./media/virtual-machines-shared-sap-high-availability-guide/6002-sap-multi-sid-ascs-scs.png
[sap-ha-guide-figure-6003]:./media/virtual-machines-shared-sap-high-availability-guide/6003-sap-multi-sid-full-landscape.png
[sap-ha-guide-figure-6004]:./media/virtual-machines-shared-sap-high-availability-guide/6004-sap-multi-sid-dns.png
[sap-ha-guide-figure-6005]:./media/virtual-machines-shared-sap-high-availability-guide/6005-sap-multi-sid-azure-portal.png
[sap-ha-guide-figure-6006]:./media/virtual-machines-shared-sap-high-availability-guide/6006-sap-multi-sid-sios-replication.png
[networking-limits-azure-resource-manager]:../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits
[sap-ha-guide-9.1.1]:sap-high-availability-guide.md#a97ad604-9094-44fe-a364-f89cb39bf097 
[sap-ha-guide-8.8]:sap-high-availability-guide.md#f19bd997-154d-4583-a46e-7f5a69d0153c
[sap-ha-guide-8.12.3.3]:sap-high-availability-guide.md#d9c1fc8e-8710-4dff-bec2-1f535db7b006 
[sap-ha-guide-9]:sap-high-availability-guide.md#a06f0b49-8a7a-42bf-8b0d-c12026c5746b
[sap-ha-guide-9.1]:sap-high-availability-guide.md#31c6bd4f-51df-4057-9fdf-3fcbc619c170 
[sap-ha-guide-9.1.2]:sap-high-availability-guide.md#eb5af918-b42f-4803-bb50-eff41f84b0b0 
[sap-ha-guide-9.1.3]:sap-high-availability-guide.md#e4caaab2-e90f-4f2c-bc84-2cd2e12a9556 
[sap-ha-guide-9.1.4]:sap-high-availability-guide.md#10822f4f-32e7-4871-b63a-9b86c76ce761 
[sap-ha-guide-9.4]:sap-high-availability-guide.md#094bc895-31d4-4471-91cc-1513b64e406a 
[sap-ha-guide-9.5]:sap-high-availability-guide.md#2477e58f-c5a7-4a5d-9ae3-7b91022cafb5 
[sap-ha-guide-9.6]:sap-high-availability-guide.md#0ba4a6c1-cc37-4bcf-a8dc-025de4263772 
[sap-ha-guide-10]:sap-high-availability-guide.md#18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9

В сентябре 2016 г. корпорация Майкрософт выпустила функцию, которая дает возможность управлять несколькими виртуальными IP-адресами с помощью внутренней подсистемы балансировки нагрузки Azure. Эта функция уже существует в hello Azure внешней подсистемы балансировки нагрузки.

При наличии развертывания SAP можно использовать toocreate подсистемы балансировки нагрузки внутренней конфигурации кластера Windows для SAP ASCS/SCS, как описано в hello [руководство для высокого уровня доступности SAP NetWeaver на виртуальных машинах Windows] [ sap-ha-guide].

Эта статья посвящена как toomove из одного ASCS/SCS установки tooan SAP multi-SID конфигурации, установив дополнительные SAP ASCS/SCS кластеризованных экземпляров в существующий кластер сервера отказоустойчивой кластеризации Windows (WSFC). Выполнив эти действия, вы настроите кластер SAP с несколькими ИД безопасности.


## <a name="prerequisites"></a>Предварительные требования
Вы уже настроили кластер WSFC, который используется для одного экземпляра SAP ASCS/SCS, как описано в hello [руководство для высокого уровня доступности SAP NetWeaver на виртуальных машинах Windows] [ sap-ha-guide] и, как показано на этой диаграмме.

![Высокодоступный экземпляр SAP ASCS/SCS][sap-ha-guide-figure-6001]

## <a name="target-architecture"></a>Целевая архитектура

Hello цель — tooinstall несколько ABAP SAP ASCS или SAP Java SCS кластеризованных экземпляров в hello же кластера WSFC, как показано ниже:

![Несколько кластеризованных экземпляров SAP ASCS/SCS в Azure][sap-ha-guide-figure-6002]

> [!NOTE]
>Нет toohello предельное число частных IP-адресов интерфейса для каждого Azure внутренней подсистемы балансировки нагрузки.
>
>Hello максимального числа экземпляров SAP ASCS/SCS в одном кластере WSFC — максимальное количество равно toohello частного IP-адреса переднего плана для каждого Azure внутренней подсистемы балансировки нагрузки.
>

Дополнительные сведения об ограничениях подсистемы балансировки нагрузки см. в пункте "Частный внешний IP-адрес на балансировщик нагрузки" раздела [Ограничения сети — Azure Resource Manager][networking-limits-azure-resource-manager].

Полный список Hello с двумя системами SAP высокого уровня доступности будет выглядеть следующим образом:

![Установка SAP высокого уровня доступности с несколькими ИД безопасности и с двумя ИД безопасности системы SAP][sap-ha-guide-figure-6003]

> [!IMPORTANT]
> Программа установки Hello должен соответствовать hello следующие условия:
> - Hello SAP ASCS/SCS экземпляры должны совместно использовать hello же кластера WSFC.
> - Для каждого ИД безопасности СУБД должен быть выделен кластер WSFC.
> - Серверы приложений SAP, принадлежащих системе SAP tooone SID должен иметь свои собственные выделенные виртуальные машины.


## <a name="prepare-hello-infrastructure"></a>Подготовка инфраструктуры hello
tooprepare инфраструктуры, можно установить дополнительный экземпляр SAP ASCS/SCS с hello следующие параметры:

| Имя параметра | Значение |
| --- | --- |
| ИД безопасности SAP ASCS/SCS |pr1-lb-ascs |
| Внутренний балансировщик нагрузки экземпляра СУБД SAP | PR5 |
| Имя виртуального узла SAP | pr5-sap-cl |
| IP-адрес виртуального узла SAP ASCS/SCS (IP-адрес дополнительной подсистемы Azure Load Balancer) | 10.0.0.50 |
| Количество экземпляров SAP ASCS/SCS | 50 |
| Порт пробы внутренней подсистемы балансировки нагрузки для дополнительного экземпляра SAP ASCS/SCS | 62350 |

> [!NOTE]
> В случае с экземплярами кластера SAP ASCS/SCS каждому IP-адресу требуется уникальный порт пробы. Например, если один IP-адрес во внутренней подсистеме балансировки нагрузки Azure использует порт пробы 62300, другой IP-адрес не может использовать этот порт.
>
>Так как порт пробы 62300 уже зарезервирован, для наших целей мы используем порт пробы 62350.

Можно установить дополнительные экземпляры SAP ASCS/SCS hello существующего кластера WSFC, состоящие из двух узлов:

| Роль виртуальной машины | Имя узла виртуальной машины | Статический IP-адрес |
| --- | --- | --- |
| 1-й узел кластера для экземпляра ASCS/SCS |pr1-ascs-0 |10.0.0.10 |
| 2-й узел кластера для экземпляра ASCS/SCS |pr1-ascs-1 |10.0.0.9 |

### <a name="create-a-virtual-host-name-for-hello-clustered-sap-ascsscs-instance-on-hello-dns-server"></a>Создание виртуального имени узла для экземпляра SAP ASCS/SCS hello clustered на DNS-сервере hello

Можно создать запись DNS для имени виртуального узла hello hello ASCS/SCS экземпляра с помощью hello следующие параметры:

| Новое имя виртуального узла SAP ASCS/SCS | Связанный IP-адрес |
| --- | --- | --- |
|pr5-sap-cl |10.0.0.50 |

Hello новым именем узла и IP-адреса отображаются в hello диспетчер DNS, как показано на следующий снимок экрана приветствия:

![Определить список диспетчер DNS, выделение hello запись DNS для hello новый SAP ASCS/SCS виртуальное имя кластера и TCP/IP-адрес][sap-ha-guide-figure-6004]

Hello процедура создания записи DNS является также подробно в главном hello [руководство для высокого уровня доступности SAP NetWeaver на виртуальных машинах Windows][sap-ha-guide-9.1.1].

> [!NOTE]
> Hello назначении toohello виртуальное имя узла экземпляра hello дополнительных ASCS/SCS новый IP-адрес должен быть hello то же, что новый IP-адрес hello назначенный toohello балансировки нагрузки Azure для SAP.
>
>В нашем сценарии hello IP-адрес — 10.0.0.50.

### <a name="add-an-ip-address-tooan-existing-azure-internal-load-balancer-by-using-powershell"></a>Добавьте IP адрес tooan существующие внутренней балансировки нагрузки Azure с помощью PowerShell

Здравствуйте, же WSFC toocreate более одного экземпляра SAP ASCS/SCS, в кластер, используйте PowerShell tooadd tooan IP адрес, существующие Azure внутренней подсистемы балансировки нагрузки. Каждому IP-адресу требуются собственные правила балансировки нагрузки, порт пробы, пул внешних IP-адресов и внутренний пул.

Hello следующий сценарий добавляет новый IP адрес tooan существующей подсистемы балансировки нагрузки. Обновите переменные PowerShell hello для вашей среды. Hello скрипт создает все необходимые правила балансировки нагрузки для всех портов SAP ASCS/SCS.

```powershell

# Select-AzureRmSubscription -SubscriptionId <xxxxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx>
Clear-Host
$ResourceGroupName = "SAP-MULTI-SID-Landscape"      # Existing resource group name
$VNetName = "pr2-vnet"                        # Existing virtual network name
$SubnetName = "Subnet"                        # Existing subnet name
$ILBName = "pr2-lb-ascs"                      # Existing ILB name                      
$ILBIP = "10.0.0.50"                          # New IP address
$VMNames = "pr2-ascs-0","pr2-ascs-1"          # Existing cluster virtual machine names
$SAPInstanceNumber = 50                       # SAP ASCS/SCS instance number: must be a unique value for each cluster
[int]$ProbePort = "623$SAPInstanceNumber"     # Probe port: must be a unique value for each IP and load balancer

$ILB = Get-AzureRmLoadBalancer -Name $ILBName -ResourceGroupName $ResourceGroupName

$count = $ILB.FrontendIpConfigurations.Count + 1
$FrontEndConfigurationName ="lbFrontendASCS$count"
$LBProbeName = "lbProbeASCS$count"

# Get hello Azure VNet and subnet
$VNet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName
$Subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $VNet -Name $SubnetName

# Add second front-end and probe configuration
Write-Host "Adding new front end IP Pool '$FrontEndConfigurationName' ..." -ForegroundColor Green
$ILB | Add-AzureRmLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -PrivateIpAddress $ILBIP -SubnetId $Subnet.Id
$ILB | Add-AzureRmLoadBalancerProbeConfig -Name $LBProbeName  -Protocol Tcp -Port $Probeport -ProbeCount 2 -IntervalInSeconds 10  | Set-AzureRmLoadBalancer

# Get new updated configuration
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName
# Get new updated LP FrontendIP COnfig
$FEConfig = Get-AzureRmLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB
$HealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

# Add new back-end configuration into existing ILB
$BackEndConfigurationName  = "backendPoolASCS$count"
Write-Host "Adding new backend Pool '$BackEndConfigurationName' ..." -ForegroundColor Green
$BEConfig = Add-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB | Set-AzureRmLoadBalancer

# Get new updated config
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName

# Assign VM NICs toobackend pool
$BEPool = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB
foreach($VMName in $VMNames){
        $VM = Get-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VMName
        $NICName = ($VM.NetworkInterfaceIDs[0].Split('/') | select -last 1)        
        $NIC = Get-AzureRmNetworkInterface -name $NICName -ResourceGroupName $ResourceGroupName                
        $NIC.IpConfigurations[0].LoadBalancerBackendAddressPools += $BEPool
        Write-Host "Assigning network card '$NICName' of hello '$VMName' VM toohello backend pool '$BackEndConfigurationName' ..." -ForegroundColor Green
        Set-AzureRmNetworkInterface -NetworkInterface $NIC
        #start-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VM.Name
}


# Create load-balancing rules
$Ports = "445","32$SAPInstanceNumber","33$SAPInstanceNumber","36$SAPInstanceNumber","39$SAPInstanceNumber","5985","81$SAPInstanceNumber","5$SAPInstanceNumber`13","5$SAPInstanceNumber`14","5$SAPInstanceNumber`16"
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName
$FEConfig = get-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB
$BEConfig = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB
$HealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

Write-Host "Creating load balancing rules for hello ports: '$Ports' ... " -ForegroundColor Green

foreach ($Port in $Ports) {

        $LBConfigrulename = "lbrule$Port" + "_$count"
        Write-Host "Creating load balancing rule '$LBConfigrulename' for hello port '$Port' ..." -ForegroundColor Green

        $ILB | Add-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig  -BackendAddressPool $BEConfig -Probe $HealthProbe -Protocol tcp -FrontendPort  $Port -BackendPort $Port -IdleTimeoutInMinutes 30 -LoadDistribution Default -EnableFloatingIP   
}

$ILB | Set-AzureRmLoadBalancer

Write-Host "Succesfully added new IP '$ILBIP' toohello internal load balancer '$ILBName'!" -ForegroundColor Green

```
После завершения выполнения сценария hello, hello, отображаются результаты hello портал Azure, как показано на следующий снимок экрана приветствия:

![Новый пул интерфейсный IP в hello портал Azure][sap-ha-guide-figure-6005]

### <a name="add-disks-toocluster-machines-and-configure-hello-sios-cluster-share-disk"></a>Добавление машины toocluster дисков и настройка диска общего ресурса кластера SIOS hello

Для каждого дополнительного экземпляра SAP ASCS/SCS необходимо добавить новый общий диск кластера. Для Windows Server 2012 R2 диск общего ресурса кластера WSFC hello в настоящее время — hello SIOS DataKeeper программное решение.

Здравствуйте, следующие:
1. Добавить дополнительный диск или диски hello одинакового размера (необходимо toostripe) tooeach из hello узлы кластера и отформатировать его.
2. Настройте репликацию хранилища с помощью SIOS DataKeeper.

Эта процедура предполагает, что SIOS DataKeeper на машин кластера WSFC hello уже установлены. Если он установлен, теперь необходимо настроить репликацию между машинами hello. Hello процесс описан в главном hello подробно [руководство для высокого уровня доступности SAP NetWeaver на виртуальных машинах Windows][sap-ha-guide-8.12.3.3].  

![DataKeeper синхронного зеркального отображения для hello новый диск SAP ASCS/SCS общей папки][sap-ha-guide-figure-6006]

### <a name="deploy-vms-for-sap-application-servers-and-dbms-cluster"></a>Развертывание виртуальных машин для серверов приложений SAP и кластера СУБД

Подготовка инфраструктуры hello toocomplete для hello второй системы SAP, hello следующие:

1. Разверните выделенные виртуальные машины для серверов приложений SAP и поместите их в отдельную выделенную группу доступности.
2. Разверните выделенные виртуальные машины для кластера СУБД и поместите их в отдельную выделенную группу доступности.


## <a name="install-hello-second-sap-sid2-netweaver-system"></a>Установка второго системы SAP SID2 NetWeaver hello

Hello завершения процесса установки второй системы SAP SID2 описан в главном hello [руководство для высокого уровня доступности SAP NetWeaver на виртуальных машинах Windows][sap-ha-guide-9].

высокоуровневые процедуры Hello выглядит следующим образом:

1. [Установите первый узел кластера hello SAP][sap-ha-guide-9.1.2].  
 На этом шаге вы устанавливаете SAP ASCS/SCS экземпляр высокой доступности на hello **СУЩЕСТВУЮЩИХ WSFC узлу кластера 1**.

2. [Изменение профиля hello SAP ASCS/SCS экземпляра hello][sap-ha-guide-9.1.3].

3. [Настройка порта пробы][sap-ha-guide-9.1.4].  
 На этом шаге настраивается порт пробы SAP-SID2-IP кластерного ресурса SAP с помощью PowerShell. Выполнение этой конфигурации на одном из узлов кластера SAP ASCS/SCS hello.

4. [Установка hello экземпляр базы данных] [sap-ha руководство-9.2].  
 На этом шаге в выделенном кластере WSFC устанавливается СУБД.

5. [Установка hello второго узла кластер] [sap-ha руководство-9.3].  
 На этом шаге вы устанавливаете SAP ASCS/SCS экземпляр высокой доступности на hello существующего узла WSFC 2.

6. Открыть порты брандмауэра Windows для экземпляра SAP ASCS/SCS hello и ProbePort.  
 На обоих узлах кластера, используемых для экземпляров SAP ASCS/SCS, откройте все порты брандмауэра Windows, используемые SAP ASCS/SCS. Эти порты, перечислены в hello [руководство для высокого уровня доступности SAP NetWeaver на виртуальных машинах Windows][sap-ha-guide-8.8].  
 Также можно откройте hello нагрузки Azure внутренней балансировки пробы портом 62350 в нашем сценарии.

7. [Изменить тип запуска hello экземпляра службы SAP ющих Методов Windows hello][sap-ha-guide-9.4].

8. [Установка сервера основного приложения SAP hello] [ sap-ha-guide-9.5] на hello новой выделенной виртуальной Машины.

9. [Установка сервера дополнительное приложение hello SAP] [ sap-ha-guide-9.6] на hello новой выделенной виртуальной Машины.

10. [Тестирование отработки отказа экземпляра SAP ASCS/SCS hello и репликации SIOS][sap-ha-guide-10].

## <a name="next-steps"></a>Дальнейшие действия

- [Ограничения сети — Azure Resource Manager][networking-limits-azure-resource-manager]
- [Несколько виртуальных IP-адресов для Azure Load Balancer][load-balancer-multivip-overview]
- [SAP NetWeaver на виртуальных машинах Windows. Руководство по обеспечению высокого уровня доступности][sap-ha-guide]
