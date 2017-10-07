---
title: "aaaConfigure частных IP-адресов для виртуальных машин - Azure PowerShell | Документы Microsoft"
description: "Узнайте, как tooconfigure частных IP-адресов виртуальных машин с помощью PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: d5f18929-15e3-40a2-9ee3-8188bc248ed8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4a3eb67de583e08208fcab40de1c2a8a9b65618c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-powershell"></a>Настройка частных IP-адресов для виртуальной машины с помощью PowerShell

[!INCLUDE [virtual-networks-static-private-ip-selectors-arm-include](../../includes/virtual-networks-static-private-ip-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

Azure предоставляет две модели развертывания: с помощью Azure Resource Manager и классическую. Корпорация Майкрософт рекомендует создать ресурсы с помощью модели развертывания диспетчера ресурсов hello. Дополнительные сведения о toolearn hello различий между моделями hello двух чтения hello [модели развертывания Azure понять](../azure-resource-manager/resource-manager-deployment-model.md) статьи. В этой статье рассматриваются hello модели развертывания диспетчера ресурсов. Вы также можете [управление статический частный IP-адрес в hello классической модели развертывания](virtual-networks-static-private-ip-classic-ps.md).

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

Образец Hello PowerShell приведенную ниже команду ожидать простой среде уже создан на основании hello сценарии выше. Если требуется toorun hello команд, отображаемых в этом документе, вначале построить hello тестовой среды, описанные в [создании виртуальной сети](virtual-networks-create-vnet-arm-ps.md).

## <a name="create-a-vm-with-a-static-private-ip-address"></a>Создание виртуальной машины со статическим частным IP-адресом
toocreate Виртуальную машину с именем *DNS01* в hello *переднего плана* подсети виртуальной сети с именем *TestVNet* с статических частного IP-адреса *192.168.1.101*, выполните следующие действия hello.

1. Задайте переменные для учетной записи хранилища hello, местоположение, группа ресурсов и toobe учетные данные используются. Необходимо будет tooenter имя пользователя и пароль для hello виртуальной Машины. Группа учетных записей и ресурсов хранилища Hello уже должна существовать.

    ```powershell
    $stName  = "vnetstorage"
    $locName = "Central US"
    $rgName  = "TestRG"
    $cred    = Get-Credential -Message "Type hello name and password of hello local administrator account."
    ```

2. Получение hello виртуальной сети и подсети требуется toocreate hello виртуальной Машины в.

    ```powershell
    $vnet   = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    $subnet = $vnet.Subnets[0].Id
    ```

3. При необходимости создайте открытый tooaccess hello IP адрес виртуальной Машины из Интернета hello.

    ```powershell
    $pip = New-AzureRmPublicIpAddress -Name TestPIP -ResourceGroupName $rgName `
    -Location $locName -AllocationMethod Dynamic
    ```

4. Создайте сетевую КАРТУ с помощью hello статический частный IP-адрес нужно tooassign toohello виртуальной Машины. Убедитесь, что hello IP из диапазона подсети hello, добавляемый hello виртуальной Машины для. Это основной шаг hello для данной статьи, задаются hello частного IP toobe статический.

    ```powershell
    $nic = New-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName $rgName `
    -Location $locName -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id `
    -PrivateIpAddress 192.168.1.101
    ```

5. Создайте приветствия созданную виртуальную Машину с помощью hello сетевого Адаптера.

    ```powershell
    $vm = New-AzureRmVMConfig -VMName DNS01 -VMSize "Standard_A1"
    $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName DNS01 `
    -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm = Set-AzureRmVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri = $storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/WindowsVMosDisk.vhd"
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name "windowsvmosdisk" -VhdUri $osDiskUri `
    -CreateOption fromImage
    New-AzureRmVM -ResourceGroupName $rgName -Location $locName -VM $vm 
    ```

    Ожидаемые выходные данные:
    
        EndTime             : [Date and time]
        Error               : 
        Output              : 
        StartTime           : [Date and time]
        Status              : Succeeded
        TrackingOperationId : [Id]
        RequestId           : [Id]
        StatusCode          : OK 

## <a name="retrieve-static-private-ip-address-information-for-a-network-interface"></a>Получение сведений о статическом частном IP-адресе сетевого интерфейса
tooview hello статических частного IP-адреса сведения для hello создания ВМ с hello-сценарий, приведенный выше, запустите следующую команду PowerShell hello и просмотрите значения hello для *адрес PrivateIpAddress* и  *Метод PrivateIpAllocationMethod*:

```powershell
Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
```

Ожидаемые выходные данные:

    Name                 : TestNIC
    ResourceGroupName    : TestRG
    Location             : centralus
    Id                   : /subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC
    Etag                 : W/"[Id]"
    ProvisioningState    : Succeeded
    Tags                 : 
    VirtualMachine       : {
                             "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01"
                           }
    IpConfigurations     : [
                             {
                               "Name": "ipconfig1",
                               "Etag": "W/\"[Id]\"",
                               "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
                               "PrivateIpAddress": "192.168.1.101",
                               "PrivateIpAllocationMethod": "Static",
                               "Subnet": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
                               },
                               "PublicIpAddress": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP"
                               },
                               "LoadBalancerBackendAddressPools": [],
                               "LoadBalancerInboundNatRules": [],
                               "ProvisioningState": "Succeeded"
                             }
                           ]
    DnsSettings          : {
                             "DnsServers": [],
                             "AppliedDnsServers": [],
                             "InternalDnsNameLabel": null,
                             "InternalFqdn": null
                           }
    EnableIPForwarding   : False
    NetworkSecurityGroup : null
    Primary              : True

## <a name="remove-a-static-private-ip-address-from-a-network-interface"></a>Удаление статического частного IP-адреса из сетевого интерфейса
tooremove hello статический частный IP-адрес добавлен toohello ВМ в скрипте hello выше выполнения hello, следующие команды PowerShell:

```powershell
$nic=Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
$nic.IpConfigurations[0].PrivateIpAllocationMethod = "Dynamic"
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

Ожидаемые выходные данные:

    Name                 : TestNIC
    ResourceGroupName    : TestRG
    Location             : centralus
    Id                   : /subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC
    Etag                 : W/"[Id]"
    ProvisioningState    : Succeeded
    Tags                 : 
    VirtualMachine       : {
                             "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/WindowsVM"
                           }
    IpConfigurations     : [
                             {
                               "Name": "ipconfig1",
                               "Etag": "W/\"[Id]\"",
                               "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
                               "PrivateIpAddress": "192.168.1.101",
                               "PrivateIpAllocationMethod": "Dynamic",
                               "Subnet": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
                               },
                               "PublicIpAddress": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP"
                               },
                               "LoadBalancerBackendAddressPools": [],
                               "LoadBalancerInboundNatRules": [],
                               "ProvisioningState": "Succeeded"
                             }
                           ]
    DnsSettings          : {
                             "DnsServers": [],
                             "AppliedDnsServers": [],
                             "InternalDnsNameLabel": null,
                             "InternalFqdn": null
                           }
    EnableIPForwarding   : False
    NetworkSecurityGroup : null
    Primary              : True

## <a name="add-a-static-private-ip-address-tooa-network-interface"></a>Добавьте статический частного IP адрес tooa сетевой интерфейс
tooadd статические частного IP адрес toohello виртуальной Машины, созданной с помощью скрипта hello выше, запустите hello, следующие команды:

```powershell
$nic=Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
$nic.IpConfigurations[0].PrivateIpAllocationMethod = "Static"
$nic.IpConfigurations[0].PrivateIpAddress = "192.168.1.101"
Set-AzureRmNetworkInterface -NetworkInterface $nic
```
## <a name="change-hello-allocation-method-for-a-private-ip-address-assigned-tooa-network-interface"></a>Изменение способа выделения hello частный IP-адрес, назначенный tooa сетевого интерфейса

Частный IP-адрес назначается tooa сетевого Адаптера с помощью метода выделения статической или динамической hello. Динамические IP-адреса можно изменить после запуска виртуальной Машины, который ранее был в hello остановлена (освобождена) состояние. Это потенциально может вызвать проблемы, если hello виртуальной Машины размещается служба, которая требует hello же IP-адрес, даже после перезагрузки компьютера из остановлена (освобождена). Статические IP-адреса, сохраняются до удаления hello виртуальной Машины. метод распределения hello toochange IP-адреса, запустите следующий сценарий, который изменяет способ распределения hello из динамического toostatic hello. Если метод распределения hello для hello текущего частный IP-адрес является статическим, измените *статических* слишком*динамического* перед выполнением скрипта hello.

```powershell
$RG = "TestRG"
$NIC_name = "testnic1"

$nic = Get-AzureRmNetworkInterface -ResourceGroupName $RG -Name $NIC_name
$nic.IpConfigurations[0].PrivateIpAllocationMethod = 'Static'
Set-AzureRmNetworkInterface -NetworkInterface $nic 
$IP = $nic.IpConfigurations[0].PrivateIpAddress

Write-Host "hello allocation method is now set to"$nic.IpConfigurations[0].PrivateIpAllocationMethod"for hello IP address" $IP"." -NoNewline
```

Если вы не знаете имя hello hello сетевого Адаптера, можно просмотреть список сетевых адаптеров в группу ресурсов, введя hello следующую команду:

```powershell
Get-AzureRmNetworkInterface -ResourceGroupName $RG | Where-Object {$_.ProvisioningState -eq 'Succeeded'} 
```

## <a name="next-steps"></a>Дальнейшие действия
* Ознакомьтесь с информацией о [зарезервированных общедоступных IP-адресах](virtual-networks-reserved-public-ip.md) .
* Узнайте об [общедоступных IP-адресах уровня экземпляра (ILPIP)](virtual-networks-instance-level-public-ip.md) .
* Обратитесь к hello [зарезервированные интерфейсы REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx).

