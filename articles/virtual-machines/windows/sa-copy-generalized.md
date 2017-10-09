---
title: "aaaCreate изображение неуправляемые универсальной ВМ в Azure | Документы Microsoft"
description: "Создание образа неуправляемого обобщенный toocreate toouse виртуальной Машины Windows несколько копий виртуальной машины в Azure."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: b8a044d20313efa6dd9b9757e61154f922134476
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-unmanaged-vm-image-from-an-azure-vm"></a>Как изображение toocreate неуправляемые виртуальной Машины из виртуальной Машины Azure

В этой статье описывается использование учетных записей хранения. Мы рекомендуем использовать управляемые диски и управляемые образы вместо учетной записи хранения. Дополнительные сведения см. в статье [Запись управляемого образа универсальной виртуальной машины в Azure](capture-image-resource.md).

В этой статье показано, как Azure PowerShell toouse toocreate изображения универсальной ВМ Azure с помощью учетной записи хранилища. Затем можно использовать образ toocreate hello другой виртуальной Машиной. Hello образ содержит hello диска ОС и дисков данных hello, вложенные toohello виртуальной машины. Hello изображение не содержит ресурсов hello виртуальной сети, поэтому требуется tooset эти ресурсы при создании hello новой виртуальной Машины. 

## <a name="prerequisites"></a>Предварительные требования
Необходима версия Azure PowerShell toohave 1.0.x или более новая версия. Если вы еще не установили PowerShell, прочтите [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) для действия по установке.

## <a name="generalize-hello-vm"></a>Обобщить hello виртуальной Машины 
В этом разделе показано, как toogeneralize вашей виртуальной машины Windows для использования в качестве образа. Универсализация ВМ удаляет все ваши личные сведения, помимо прочего и подготавливает toobe машины hello, используемое в качестве изображения. Дополнительные сведения о программе Sysprep см. в разделе [как tooUse Sysprep: введение](http://technet.microsoft.com/library/bb457073.aspx).

Убедитесь, что на компьютере hello ролей сервера hello поддерживаются программой Sysprep. Дополнительные сведения см. в статье [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles) (Поддержка серверных ролей в Sysprep).

> [!IMPORTANT]
> При отправке вашего tooAzure виртуального жесткого диска для hello первый раз, убедитесь, что у вас есть [подготовки ВМ](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) перед запуском Sysprep. 
> 
> 

Кроме того, можно обобщить ВМ Linux с помощью `sudo waagent -deprovision+user` , а затем используйте PowerShell toocapture hello виртуальной Машины. Сведения об использовании toocapture CLI hello виртуальной Машины см. в разделе [как toogeneralize и виртуальных машин Linux с помощью отслеживания hello Azure CLI ](../linux/capture-image.md).


1. Войдите в систему toohello виртуальной машины Windows.
2. Привет открыть окно командной строки с правами администратора. Измените каталог hello слишком**%windir%\system32\sysprep**, а затем запустите `sysprep.exe`.
3. В hello **средство подготовки системы** выберите **Enter System Out-of-Box Experience (OOBE)**и убедитесь, что hello **Generalize** установлен флажок.
4. В разделе **Параметры завершения работы** выберите **Завершение работы**.
5. Нажмите кнопку **ОК**.
   
    ![Запуск Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. По завершении работы программы Sysprep завершает hello виртуальной машины. 

> [!IMPORTANT]
> Не перезагружайте hello виртуальной Машины, пока не выполняется отправка tooAzure hello виртуального жесткого диска или создание образа из hello виртуальной Машины. Hello ВМ случайно возвращает перезапуска, запустите Sysprep toogeneralize его еще раз.
> 
> 

## <a name="log-in-tooazure-powershell"></a>Войдите в tooAzure PowerShell
1. Откройте Azure PowerShell и войдите в tooyour учетная запись Azure.
   
    ```powershell
    Login-AzureRmAccount
    ```
   
    Откроется всплывающее окно учетные данные учетной записи Azure tooenter вы.
2. Получите подписку hello идентификаторы для доступных подписок.
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. Набор hello нужной подписки с идентификатором hello подписки.
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="deallocate-hello-vm-and-set-hello-state-toogeneralized"></a>Выделение hello ВМ и установить состояние toogeneralized hello
1. Неудачная попытка освобождения ресурсов виртуальной Машины hello.
   
    ```powershell
    Stop-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName>
    ```
   
    Hello *состояние* для hello ВМ в hello Azure портал изменения из **остановлена** слишком**остановлена (освобождена)**.
2. Задать состояние hello hello виртуальной машины слишком**универсальная**. 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName <resourceGroup> -Name <vmName> -Generalized
    ```
3. Проверьте состояние hello hello виртуальной Машины. Hello **OSState/универсальные** статьи для hello виртуальная машина должна иметь hello **DisplayStatus** значение слишком**ВМ обобщенный**.  
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName> -Status
    $vm.Statuses
    ```

## <a name="create-hello-image"></a>Создание образа hello

Создание образа неуправляемые виртуальной машины в hello конечный контейнер хранилища с помощью этой команды. Hello образу в hello же учетная запись хранения, как hello исходной виртуальной машины. Hello `-Path` сохраняет копию шаблона JSON hello для hello исходной виртуальной Машины tooyour локального компьютера. Hello `-DestinationContainerName` параметр является именем hello hello контейнера, что вы хотите, чтобы toohold изображения. Если контейнер hello не существует, он создается автоматически.
   
```powershell
Save-AzureRmVMImage -ResourceGroupName <resourceGroupName> -Name <vmName> `
    -DestinationContainerName <destinationContainerName> -VHDNamePrefix <templateNamePrefix> `
    -Path <C:\local\Filepath\Filename.json>
```
   
Hello URL-адрес изображения можно получить из шаблона файла JSON hello. Go toohello **ресурсов** > **storageProfile** > **osDisk** > **изображение**  >  **uri** раздел для hello полный путь данного изображения. Hello URL-адрес изображения hello выглядит следующим образом: `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.
   
Можно также проверить hello URI портала hello. изображение Hello является скопированный tooa контейнер с именем **системы** вашей учетной записи хранилища. 

## <a name="create-a-vm-from-hello-image"></a>Создание виртуальной Машины из образа hello

Теперь можно создать один или несколько виртуальных машин из неуправляемого образа hello.

### <a name="set-hello-uri-of-hello-vhd"></a>Набор hello URI hello виртуального жесткого диска

Hello URI для hello toouse виртуальный жесткий ДИСК имеет формат hello: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd. В этом примере hello виртуального жесткого диска с именем **myVHD** в учетной записи хранения hello **mystorageaccount** в контейнере hello **mycontainer**.

```powershell
$imageURI = "https://mystorageaccount.blob.core.windows.net/mycontainer/myVhd.vhd"
```


### <a name="create-a-virtual-network"></a>Создать виртуальную сеть
Создание виртуальной сети hello и подсеть hello [виртуальной сети](../../virtual-network/virtual-networks-overview.md).

1. Создайте подсеть hello. Hello следующий пример создает подсеть с именем **mySubnet** в группе ресурсов hello **myResourceGroup** с префикс адреса hello **10.0.0.0/24**.  
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. Создайте виртуальную сеть hello. Hello следующий пример создает виртуальную сеть с именем **myVnet** в hello **Запад США** места, где префикс адреса hello **10.0.0.0/16**.  
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-network-interface"></a>Создание общедоступного IP-адреса и сетевого интерфейса
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

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a>Создание группы безопасности сети hello и правило протокола удаленного рабочего СТОЛА
возможности toolog toobe в tooyour виртуальную Машину с помощью протокола удаленного рабочего СТОЛА, необходимо toohave правило безопасности, которое разрешает RDP-доступ через порт 3389. 

В этом примере создается группа безопасности сети с именем **myNsg**, которая содержит правило с именем **myRdpRule**, разрешающее трафик RDP через порт 3389. Дополнительные сведения о Nsg см. в разделе [Открытие портов tooa ВМ в Azure с помощью PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


### <a name="create-a-variable-for-hello-virtual-network"></a>Создайте переменную для hello виртуальной сети
Создайте переменную для завершения hello виртуальной сети. 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName
```

### <a name="create-hello-vm"></a>Создание виртуальной Машины hello
Hello следующие команды PowerShell завершает hello конфигураций виртуальных машин и использует неуправляемые изображения в качестве hello источника для новой установки hello.

</br>

```powershell
    # Enter a new user name and password toouse as hello local administrator account 
    # for remotely accessing hello VM.
    $cred = Get-Credential

    # Name of hello storage account where hello VHD is located. This example sets hello 
    # storage account name as "myStorageAccount"
    $storageAccName = "myStorageAccount"

    # Name of hello virtual machine. This example sets hello VM name as "myVM".
    $vmName = "myVM"

    # Size of hello virtual machine. This example creates "Standard_D2_v2" sized VM. 
    # See hello VM sizes documentation for more information: 
    # https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/
    $vmSize = "Standard_D2_v2"

    # Computer name for hello VM. This examples sets hello computer name as "myComputer".
    $computerName = "myComputer"

    # Name of hello disk that holds hello OS. This example sets hello 
    # OS disk name as "myOsDisk"
    $osDiskName = "myOsDisk"

    # Assign a SKU name. This example sets hello SKU name as "Standard_LRS"
    # Valid values for -SkuName are: Standard_LRS - locally redundant storage, Standard_ZRS - zone redundant
    # storage, Standard_GRS - geo redundant storage, Standard_RAGRS - read access geo redundant storage,
    # Premium_LRS - premium locally redundant storage. 
    $skuName = "Standard_LRS"

    # Get hello storage account where hello uploaded image is stored
    $storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $rgName -AccountName $storageAccName

    # Set hello VM name and size
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

    #Set hello Windows operating system configuration and add hello NIC
    $vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

    # Create hello OS disk URI
    $osDiskUri = '{0}vhds/{1}-{2}.vhd' `
        -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName

    # Configure hello OS disk toobe created from hello existing VHD image (-CreateOption fromImage).
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri `
        -CreateOption fromImage -SourceImageUri $imageURI -Windows

    # Create hello new VM
    New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

### <a name="verify-that-hello-vm-was-created"></a>Убедитесь, что hello создания виртуальной Машины
По завершении вы увидите только что созданный виртуальной Машины в hello hello [портал Azure](https://portal.azure.com) под **Обзор** > **виртуальные машины**, или с помощью следующих hello Команды PowerShell:

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a>Дальнейшие действия
см. на новую виртуальную машину с помощью Azure PowerShell toomanage [управление виртуальными машинами с помощью диспетчера ресурсов Azure и PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


