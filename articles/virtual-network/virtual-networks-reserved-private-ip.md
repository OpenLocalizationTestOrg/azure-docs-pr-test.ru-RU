---
title: "aaaStatic внутренних частных IP - Azure VM - классический"
description: "Основные сведения о статического внутреннего IP-адреса (DIP) и как toomanage их"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 93444c6f-af1b-41f8-a035-77f5c0302bf0
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2016
ms.author: jdial
ms.openlocfilehash: 5abe1c59f2f3ed19bcf56c269dfe57ac32d4f601
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-a-static-internal-private-ip-address-using-powershell-classic"></a>Как tooset статический внутренний частного IP адрес, с помощью PowerShell (классические)
В большинстве случаев нет необходимости toospecify статический внутренний IP-адрес для виртуальной машины. Виртуальные машины в виртуальной сети будут автоматически получать внутренний IP-адрес из указанного вами диапазона. Однако в некоторых случаях указание статического IP-адреса для конкретной виртуальной машины имеет смысл. Например, если ВМ является постоянной toorun DNS или будет контроллером домена. Статический внутренний IP-адрес остается с hello виртуальной Машины, даже в состоянии остановки или отзыва. 

> [!IMPORTANT]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания hello [модели развертывания диспетчера ресурсов](virtual-networks-static-private-ip-arm-ps.md).
> 
> 

## <a name="how-tooverify-if-a-specific-ip-address-is-available"></a>Как tooverify, если доступен определенный IP-адрес
tooverify Если hello IP-адрес *10.0.0.7* доступен в виртуальной сети с именем *TestVnet*, запустите следующую команду PowerShell hello и проверьте значение hello *IsAvailable*:

    Test-AzureStaticVNetIP –VNetName TestVNet –IPAddress 10.0.0.7 

    IsAvailable          : True
    AvailableAddresses   : {}
    OperationDescription : Test-AzureStaticVNetIP
    OperationId          : fd3097e1-5f4b-9cac-8afa-bba1e3492609
    OperationStatus      : Succeeded

> [!NOTE]
> Команда hello tootest выше в безопасной среде выполните рекомендации hello в [Создание виртуальной сети (классические)](virtual-networks-create-vnet-classic-pportal.md) toocreate виртуальную сеть с именем *TestVnet* и убедитесь, он использует hello  *10.0.0.0/8* адресное пространство.
> 
> 

## <a name="how-toospecify-a-static-internal-ip-when-creating-a-vm"></a>Как toospecify статического внутреннего IP-адреса при создании виртуальной Машины
Приведенный ниже сценарий PowerShell Hello создает новую облачную службу с именем *TestService*, затем извлекает изображение из Azure, а затем создает Виртуальную машину с именем *TestVM* в hello новой облачной службы с помощью образа получить hello Задает hello toobe виртуальной Машины в подсеть с именем *Subnet-1*и задает *10.0.0.7* как статический внутренний IP-адрес, для hello виртуальной Машины:

    New-AzureService -ServiceName TestService -Location "Central US"
    $image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}
    New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
    | Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
    | Set-AzureSubnet –SubnetNames Subnet-1 `
    | Set-AzureStaticVNetIP -IPAddress 10.0.0.7 `
    | New-AzureVM -ServiceName "TestService" –VNetName TestVnet

## <a name="how-tooretrieve-static-internal-ip-information-for-a-vm"></a>Как tooretrieve статические внутренние IP сведения для виртуальной Машины
tooview hello статические внутренние IP сведения для hello создания ВМ с hello-сценарий, приведенный выше, запустите следующую команду PowerShell hello и просмотрите значения hello *IP-адрес*:

    Get-AzureVM -Name TestVM -ServiceName TestService

    DeploymentName              : TestService
    Name                        : TestVM
    Label                       : 
    VM                          : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.PersistentVM
    InstanceStatus              : Provisioning
    IpAddress                   : 10.0.0.7
    InstanceStateDetails        : Windows is preparing your computer for first use...
    PowerState                  : Started
    InstanceErrorCode           : 
    InstanceFaultDomain         : 0
    InstanceName                : TestVM
    InstanceUpgradeDomain       : 0
    InstanceSize                : Small
    HostName                    : rsR2-797
    AvailabilitySetName         : 
    DNSName                     : http://testservice000.cloudapp.net/
    Status                      : Provisioning
    GuestAgentStatus            : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.GuestAgentStatus
    ResourceExtensionStatusList : {Microsoft.Compute.BGInfo}
    PublicIPAddress             : 
    PublicIPName                : 
    NetworkInterfaces           : {}
    ServiceName                 : TestService
    OperationDescription        : Get-AzureVM
    OperationId                 : 34c1560a62f0901ab75cde4fed8e8bd1
    OperationStatus             : OK

## <a name="how-tooremove-a-static-internal-ip-from-a-vm"></a>Как tooremove статического внутреннего IP-адреса, от виртуальной Машины
tooremove hello статический внутренний IP-адрес добавлен toohello ВМ в скрипте hello выше, выполните следующую команду PowerShell hello:

    Get-AzureVM -ServiceName TestService -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM

## <a name="how-tooadd-a-static-internal-ip-tooan-existing-vm"></a>Как tooadd статического внутреннего IP tooan существующей виртуальной Машины
tooadd статические внутренние toohello IP виртуальной Машины, созданной с помощью скрипта hello выше runt следующей команды:

    Get-AzureVM -ServiceName TestService000 -Name TestVM `
    | Set-AzureStaticVNetIP -IPAddress 10.10.0.7 `
    | Update-AzureVM

## <a name="next-steps"></a>Дальнейшие действия
[Зарезервированный IP-адрес](virtual-networks-reserved-public-ip.md)

[Общедоступный IP-адрес уровня экземпляра (ILPIP)](virtual-networks-instance-level-public-ip.md)

[API REST зарезервированных IP-адресов](https://msdn.microsoft.com/library/azure/dn722420.aspx)

