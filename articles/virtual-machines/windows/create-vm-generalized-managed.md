---
title: "aaaCreate виртуальной Машины из управляемый образ виртуальной Машины в Azure | Документы Microsoft"
description: "Создание виртуальной машины Windows из общего управляемого образа виртуальной Машины с помощью Azure PowerShell, в модели развертывания диспетчера ресурсов hello."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: cynthn
ms.openlocfilehash: 5036ef1533c144a9a328e94599b359e0166f337d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-from-a-managed-image"></a>Создание виртуальной машины из управляемого образа

Можно создать несколько виртуальных машин из управляемого образа виртуальной машины в Azure. Управляемый образ ВМ содержит toocreate необходимые сведения hello виртуальной Машины, включая hello ОС и дисков данных. Здравствуйте, виртуальные жесткие диски, составляющие hello изображения, включая диски hello ОС и дисков данных, хранятся в виде управляемых дисков. 


## <a name="prerequisites"></a>Предварительные требования

Требуется toohave уже [создан управляемый образ виртуальной Машины](capture-image-resource.md) Здравствуйте, toouse для создания новой виртуальной Машины. 

Убедитесь, что последние версии hello hello AzureRM.Compute и AzureRM.Network модули PowerShell. Откройте командную строку PowerShell с правами администратора и выполните следующие команды tooinstall hello их.

```powershell
Install-Module AzureRM.Compute,AzureRM.Network
```
Дополнительные сведения см. в разделе [об управлении версиями Azure PowerShell](/powershell/azure/overview).



## <a name="collect-information-about-hello-image"></a>Собирать данные об образе hello

Сначала нам нужна toogather основные сведения о hello и создайте переменную для hello образа. В этом примере используется управляемый образ виртуальной Машины с именем **myImage** именно в hello **myResourceGroup** группы ресурсов в hello **Западная центральной части США** расположение. 

```powershell
$rgName = "myResourceGroup"
$location = "West Central US"
$imageName = "myImage"
$image = Get-AzureRMImage -ImageName $imageName -ResourceGroupName $rgName
```

## <a name="create-a-virtual-network"></a>Создать виртуальную сеть
Создание виртуальной сети hello и подсеть hello [виртуальной сети](../../virtual-network/virtual-networks-overview.md).

1. Создайте подсеть hello. В этом примере создается подсеть с именем **mySubnet** с префикс адреса hello **10.0.0.0/24**.  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. Создайте виртуальную сеть hello. В этом примере создается виртуальная сеть с именем **myVnet** с префикс адреса hello **10.0.0.0/16**.  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a>Создание общедоступного IP-адреса и сетевого интерфейса

требуется tooenable взаимодействия с виртуальной машиной hello в виртуальной сети hello, [общедоступный IP-адрес](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) и сетевого интерфейса.

1. Создание общедоступного IP-адреса. В этом примере создается общедоступный IP-адрес с именем **myPip**. 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. Создайте сетевую карту hello. В этом примере создается сетевая карта с именем **myNic**. 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-hello-network-security-group-and-an-rdp-rule"></a>Создание группы безопасности сети hello и правило протокола удаленного рабочего СТОЛА

возможности toolog toobe в tooyour виртуальную Машину с помощью протокола удаленного рабочего СТОЛА, необходимо toohave правило сетевой безопасности (NSG), позволяющий RDP-доступ через порт 3389. 

В этом примере создается группа безопасности сети с именем **myNsg**, которая содержит правило с именем **myRdpRule**, разрешающее трафик RDP через порт 3389. Дополнительные сведения о Nsg см. в разделе [Открытие портов tooa ВМ в Azure с помощью PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

```powershell
$nsgName = "myNsg"
$ruleName = "myRdpRule"
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


## <a name="create-a-variable-for-hello-virtual-network"></a>Создайте переменную для hello виртуальной сети

Создайте переменную для завершения hello виртуальной сети. 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-hello-credentials-for-hello-vm"></a>Получить учетные данные hello для hello виртуальной Машины

Hello следующий командлет будет открыто окно, можно будет ввести имя и пароль toouse пользователя новый под учетной записью локального администратора hello удаленного доступа hello виртуальной Машины. 

```powershell
$cred = Get-Credential
```

## <a name="set-variables-for-hello-vm-name-computer-name-and-hello-size-of-hello-vm"></a>Набор переменных для hello виртуальной Машины, имя, имя компьютера и hello размер hello виртуальной Машины

1. Создайте переменные hello имя виртуальной Машины и имя компьютера. В этом примере задает имя виртуальной Машины hello как **myVM** и имя компьютера hello как **myComputer**.

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    ```
2. Задайте размер hello hello виртуальной машины. В этом примере создается виртуальная машина размера **Standard_DS1_v2**. В разделе hello [размеры виртуальных Машин](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) Дополнительные сведения см.

    ```powershell
    $vmSize = "Standard_DS1_v2"
    ```

3. Добавьте hello имя виртуальной Машины и конфигурация виртуальной Машины toohello размера.

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-hello-vm-image-as-source-image-for-hello-new-vm"></a>Образ виртуальной Машины hello набор как источник изображения hello новой виртуальной Машины

Задать hello исходного образа с помощью идентификатора hello hello управляемый образ виртуальной Машины.

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-hello-os-configuration-and-add-hello-nic"></a>Задание конфигурации hello ОС и добавление hello сетевого адаптера.

Введите тип хранения hello (PremiumLRS или StandardLRS) и hello размер диска операционной системы hello. В следующем примере тип учетной записи hello слишком**PremiumLRS**, hello размер диска слишком**128 ГБ** и их кэширование слишком**ReadWrite**.

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm  -StorageAccountType PremiumLRS -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-hello-vm"></a>Создание виртуальной Машины hello

Создание новой виртуальной машины с помощью конфигурации hello, мы строится и хранится в hello hello **$vm** переменной.

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-hello-vm-was-created"></a>Убедитесь, что hello создания виртуальной Машины
По завершении вы увидите только что созданный виртуальной Машины в hello hello [портал Azure](https://portal.azure.com) под **Обзор** > **виртуальные машины**, или с помощью следующих hello Команды PowerShell:

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a>Дальнейшие действия
см. на новую виртуальную машину с помощью Azure PowerShell toomanage [Создание и управление виртуальными машинами Windows с помощью модуля Azure PowerShell hello](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

