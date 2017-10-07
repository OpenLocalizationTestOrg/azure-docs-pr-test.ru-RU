---
title: "Подготовка к использованию виртуальный жесткий ДИСК toocreate aaaUpload несколько виртуальных машин в Azure | Документы Microsoft"
description: "Отправьте обобщенный виртуальный жесткий ДИСК tooan хранилища Azure учетная запись toocreate toouse виртуальной Машины Windows с помощью модели развертывания диспетчера ресурсов hello."
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
ms.date: 05/18/2017
ms.author: cynthn
ms.openlocfilehash: aa1af2a0acf81685e62853de71afa51e819cb696
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-generalized-vhd-tooazure-toocreate-a-new-vm"></a>Отправка toocreate tooAzure новой виртуальной Машины обобщенный виртуальный жесткий ДИСК

В этом разделе рассматриваются отправки учетную запись хранения tooa универсальный неуправляемые диск и последующего создания новой виртуальной Машины с помощью отправки hello диска. Из универсального образа VHD удалены все сведения вашей личной учетной записи с помощью Sysprep. 

Toocreate виртуальной Машины на основе специализированного VHD в учетной записи хранения см [создания виртуальной Машины из специализированного VHD](sa-create-vm-specialized.md).

В этом разделе описывается использование учетных записей хранилища, но мы рекомендуем вместо toousing управляемых диски перемещаются заказчики. Полный обзор операций как tooprepare, передача и создание новой виртуальной Машины с помощью управляемых дисках, см. в разделе [Создание новой виртуальной Машины из обобщенный виртуальный жесткий ДИСК отправлен tooAzure, с помощью управляемых дисков](upload-generalized-managed.md).



## <a name="prepare-hello-vm"></a>Подготовка виртуальной Машины hello

Из универсального VHD удалены все данные вашей личной учетной записи с помощью Sysprep. Если предполагается toouse hello VHD как toocreate изображения следует новые виртуальные машины из:
  
  * [Подготовка виртуального жесткого диска Windows tooupload tooAzure](prepare-for-upload-vhd-image.md). 
  * Обобщить hello виртуальной машины с помощью программы Sysprep

### <a name="generalize-a-windows-virtual-machine-using-sysprep"></a>Обобщение виртуальной машины Windows с помощью Sysprep
В этом разделе показано, как toogeneralize вашей виртуальной машины Windows для использования в качестве образа. Sysprep удаляет все ваши личные сведения, помимо прочего и подготавливает toobe машины hello, используемое в качестве изображения. Дополнительные сведения о программе Sysprep см. в разделе [как tooUse Sysprep: введение](http://technet.microsoft.com/library/bb457073.aspx).

Убедитесь, что на компьютере hello ролей сервера hello поддерживаются программой Sysprep. Дополнительные сведения см. в статье [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles) (Поддержка серверных ролей в Sysprep).

> [!IMPORTANT]
> При запуске средства Sysprep перед отправкой tooAzure вашего виртуального жесткого диска для hello в первый раз убедитесь, что у вас есть [подготовки ВМ](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) перед запуском Sysprep. 
> 
> 

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


## <a name="upload-hello-vhd"></a>Отправка hello виртуального жесткого диска

Отправка виртуального жесткого диска для hello tooan учетной записи хранилища Azure.

### <a name="log-in-tooazure"></a>Войдите в tooAzure
Если у вас еще нет PowerShell версии 1.4 или выше установлены, чтение [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).

1. Откройте Azure PowerShell и войдите в tooyour учетная запись Azure. Откроется всплывающее окно учетные данные учетной записи Azure tooenter вы.
   
    ```powershell
    Login-AzureRmAccount
    ```
2. Получите подписку hello идентификаторы для доступных подписок.
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. Набор hello нужной подписки с идентификатором hello подписки. Замените `<subscriptionID>` с Идентификатором hello hello исправить подписки.
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

### <a name="get-hello-storage-account"></a>Получение учетной записи хранилища hello
Требуется учетная запись хранения в образе виртуальной Машины Azure toostore hello отправлен. Можно использовать существующую учетную запись хранения или создать новую. 

tooshow hello доступных учетных записей хранилища, введите следующую команду:

```powershell
Get-AzureRmStorageAccount
```

Toouse существующую учетную запись хранения следует продолжить toohello [загрузку образа виртуальной Машины hello](#upload-the-vm-vhd-to-your-storage-account) раздела.

Если вам требуется toocreate учетной записи хранилища, выполните следующие действия.

1. Требуется имя hello hello группы ресурсов, которой должен быть создан hello учетной записи хранилища. toofind out все hello группы ресурсов в вашей подписке типа:
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    Группа ресурсов с именем toocreate **myResourceGroup** в hello **Запад США** региона, введите:

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. Создать учетную запись хранилища с именем **mystorageaccount** в этой группе ресурсов с помощью hello [New AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) командлета:
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
 
### <a name="start-hello-upload"></a>Начать отправку hello 

Используйте hello [AzureRmVhd добавить](/powershell/module/azurerm.compute/add-azurermvhd) контейнера командлет tooupload hello изображения tooa вашей учетной записи хранилища. В этом примере файл hello передачи **myVHD.vhd** из `"C:\Users\Public\Documents\Virtual hard disks\"` tooa учетной записи хранилища с именем **mystorageaccount** в hello **myResourceGroup** группы ресурсов. Hello файла будут помещены в контейнер hello **mycontainer** и hello новый файл будет называться **myUploadedVHD.vhd**.

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


В случае успешного выполнения вы получаете ответ, который выглядит примерно toothis:

```powershell
MD5 hash is being calculated for hello file C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd.
MD5 hash calculation is completed.
Elapsed time for hello operation: 00:03:35
Creating new page blob of size 53687091712...
Elapsed time for upload: 01:12:49

LocalFilePath           DestinationUri
-------------           --------------
C:\Users\Public\Doc...  https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd
```

В зависимости от сетевого подключения и hello размер файла виртуального жесткого диска, эта команда может занять некоторое время toocomplete.


## <a name="create-a-new-vm"></a>Создание виртуальной машины 

Теперь можно hello используйте отправки виртуального жесткого диска toocreate новой виртуальной Машины. 

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
Hello следующий сценарий PowerShell показано, как tooset hello конфигураций виртуальных машин и используйте hello загрузить образ виртуальной Машины как hello источника для новой установки hello.



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

## <a name="verify-that-hello-vm-was-created"></a>Убедитесь, что hello создания виртуальной Машины
По завершении вы увидите только что созданный виртуальной Машины в hello hello [портал Azure](https://portal.azure.com) под **Обзор** > **виртуальные машины**, или с помощью следующих hello Команды PowerShell:

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a>Дальнейшие действия
см. на новую виртуальную машину с помощью Azure PowerShell toomanage [управление виртуальными машинами с помощью диспетчера ресурсов Azure и PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


