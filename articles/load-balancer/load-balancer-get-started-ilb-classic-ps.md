---
title: "aaaCreate Azure внутренним загрузить балансировки - классический PowerShell | Документы Microsoft"
description: "Узнайте, как с помощью PowerShell в hello классической модели развертывания подсистемы балансировки нагрузки, toocreate во внутренний"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 3be93168-3787-45a5-a194-9124fe386493
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 382db80c42ffab09905513019b72e85a4f9dfeff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-using-powershell"></a>Приступая к созданию внутреннего балансировщика нагрузки (классическая модель) с помощью PowerShell

> [!div class="op_single_selector"]
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [Интерфейс командной строки Azure](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [Облачные службы](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).  В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов. Узнайте, каким образом слишком[выполните следующие действия с помощью диспетчера ресурсов модели hello](load-balancer-get-started-ilb-arm-ps.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-internal-load-balancer-set-for-virtual-machines"></a>Создание набора внутреннего балансировщика нагрузки для виртуальных машин

toocreate внутренний балансировщик нагрузки задать и hello серверов, которые будут отправлять их tooit трафик, у вас есть toodo hello следующее:

1. Создайте экземпляр внутренней балансировки нагрузки, конечную точку hello входящего трафика toobe Балансировка нагрузки для серверов hello набора балансировки нагрузки.
2. Добавьте конечные точки, соответствующие toohello виртуальных машин, которые будут принимать входящий трафик hello.
3. Настройка серверов hello, которые будут отправлять что hello трафика toobe с балансировкой нагрузки toosend их трафика toohello виртуальных IP-адресов (VIP) адрес экземпляра hello внутренней балансировки.

### <a name="step-1-create-an-internal-load-balancing-instance"></a>Шаг 1. Создание экземпляра внутренней балансировки нагрузки

Для существующей облачной службе или облачной службы, развернутой в региональной виртуальной сети можно создать экземпляр внутренней балансировки нагрузки с помощью следующих команд Windows PowerShell hello:

```powershell
$svc="<Cloud Service Name>"
$ilb="<Name of your ILB instance>"
$subnet="<Name of hello subnet within your virtual network>"
$IP="<hello IPv4 address toouse on hello subnet-optional>"

Add-AzureInternalLoadBalancer -ServiceName $svc -InternalLoadBalancerName $ilb –SubnetName $subnet –StaticVNetIPAddress $IP
```

Обратите внимание, что такое использование hello [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx) командлета Windows PowerShell использует набор параметров DefaultProbe hello. Дополнительную информацию о дополнительных наборах параметров см. в документации [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx).

### <a name="step-2-add-endpoints-toohello-internal-load-balancing-instance"></a>Шаг 2: Добавление экземпляра внутренняя Балансировка нагрузки toohello конечных точек

Пример:

```powershell
$svc="mytestcloud"
$vmname="DB1"
$epname="TCP-1433-1433"
$lbsetname="lbset"
$prot="tcp"
$locport=1433
$pubport=1433
$ilb="ilbset"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -Lbset $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM
```

### <a name="step-3-configure-your-servers-toosend-their-traffic-toohello-new-internal-load-balancing-endpoint"></a>Шаг 3: Настройка вашей toosend серверы их трафика toohello новой внутренняя Балансировка нагрузки конечной точки

Иметь слишком настроить серверы hello, трафик которых будет toobe балансировки нагрузки toouse hello новый IP-адрес (hello виртуальных IP-адресов) hello экземпляр внутренней балансировки. Это адрес hello какие hello внутренняя Балансировка нагрузки прослушивается экземпляром. В большинстве случаев требуется toojust добавить или изменить запись DNS для hello виртуального IP-адреса экземпляра внутренняя Балансировка нагрузки hello.

Если вы указали hello IP-адрес во время создания экземпляра внутренняя Балансировка нагрузки hello hello, уже имеется hello виртуальных IP-адресов. В противном случае вы можете увидеть VIP hello из hello, следующие команды:

```powershell
$svc="<Cloud Service Name>"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

toouse эти команды, заполните значения hello и remove hello < и >. Пример:

```powershell
$svc="mytestcloud"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

Из отображения hello hello команды Get-AzureInternalLoadBalancer Обратите внимание, hello IP-адрес и сделайте hello необходимые изменения tooyour серверы или tooensure записей DNS, трафик отправляется toohello виртуальных IP-адресов.

> [!NOTE]
> Hello платформы Microsoft Azure использует статические публично маршрутизируемый IPv4-адрес для различных сценариев администрирования. Hello IP-адрес — 168.63.129.16. Не блокируйте этот IP-адрес брандмауэрами, поскольку это может привести к непредвиденному поведению.
> С учетом tooAzure внутренней балансировки отслеживая проб из состояние работоспособности hello toodetermine подсистемы балансировки нагрузки hello для виртуальных машин в набор балансировки нагрузки используется этот IP-адрес. Если группа безопасности сети является используется toorestrict трафика tooAzure виртуальные машины в наборе внутренне балансировки нагрузки или примененных tooa подсеть виртуальной сети, убедитесь, что правило сетевой безопасности добавлен tooallow трафика из 168.63.129.16.

## <a name="example-of-internal-load-balancing"></a>Пример внутренней балансировки нагрузки

toostep hello окончания tooend процессе создания набор балансировки нагрузки для двух примеров конфигурации появится hello следующие разделы.

### <a name="an-internet-facing-multi-tier-application"></a>Многоуровневое приложение для Интернета

Вы хотите tooprovide базы данных службы балансировки нагрузки для набора веб-серверы с выходом в Интернет. Оба набора серверов размещены в одной облачной службе Azure. TooTCP трафика порт 1433 для веб-сервера необходимо распределить среди двух виртуальных машин на уровне базы данных hello. На рисунке 1 показана конфигурация hello.

![Внутренний набор с балансировкой нагрузки для уровня базы данных hello](./media/load-balancer-internal-getstarted/IC736321.png)

Конфигурация Hello состоит из следующих hello.

* Hello существующей облачной службы размещения виртуальных машин hello называется mytestcloud.
* Hello два существующего сервера базы данных именуются DB1 и DB2.
* Веб-серверов в веб-уровень hello toohello серверы баз данных на уровне базы данных hello подключаться с помощью hello частный IP-адрес. Другой вариант является toouse DNS для виртуальной сети hello и вручную зарегистрировать записи для набора балансировки нагрузки внутренней hello.

Hello следующие команды настраивают новый экземпляр внутренняя Балансировка нагрузки с именем **ILBset** и добавьте виртуальные машины toohello конечные точки, соответствующие toohello двух серверов баз данных:

```powershell
$svc="mytestcloud"
$ilb="ilbset"
Add-AzureInternalLoadBalancer -ServiceName $svc -InternalLoadBalancerName $ilb
$prot="tcp"
$locport=1433
$pubport=1433
$epname="TCP-1433-1433"
$lbsetname="lbset"
$vmname="DB1"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -LbSetName $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM

$epname="TCP-1433-1433-2"
$vmname="DB2"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -LbSetName $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM
```

## <a name="remove-an-internal-load-balancing-configuration"></a>Удаление конфигурации внутренней балансировки нагрузки

tooremove виртуальную машину как конечную точку из экземпляра балансировщик внутренней нагрузки hello используйте следующие команды:

```powershell
$svc="<Cloud service name>"
$vmname="<Name of hello VM>"
$epname="<Name of hello endpoint>"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

toouse эти команды, заполните значения hello и удалите hello < и >.

Пример:

```powershell
$svc="mytestcloud"
$vmname="DB1"
$epname="TCP-1433-1433"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

tooremove экземпляра балансировки внутренней нагрузки из облачной службы, hello используйте следующие команды:

```powershell
$svc="<Cloud service name>"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

toouse эти команды, заполните значения hello и удалите hello < и >.

Пример:

```powershell
$svc="mytestcloud"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

## <a name="additional-information-about-internal-load-balancer-cmdlets"></a>Дополнительная информация о командлетах для внутреннего балансировщика нагрузки

tooobtain Дополнительные сведения о командлетах, внутренняя Балансировка нагрузки, запустите следующие команды в командной строке Windows PowerShell hello:

```powershell
Get-Help New-AzureInternalLoadBalancerConfig -full
Get-Help Add-AzureInternalLoadBalancer -full
Get-Help Get-AzureInternalLoadbalancer -full
Get-Help Remove-AzureInternalLoadBalancer -full
```

## <a name="next-steps"></a>Дальнейшие действия

[Настройка режима распределения балансировщика нагрузки с помощью соответствия исходному IP-адресу](load-balancer-distribution-mode.md)

[Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки](load-balancer-tcp-idle-timeout.md)

