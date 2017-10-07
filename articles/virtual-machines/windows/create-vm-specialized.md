---
title: "aaaCreate виртуальной Машине Windows на основе специализированного VHD в Azure | Документы Microsoft"
description: "Создание новой виртуальной Машины Windows путем присоединения специализированного диска управляемых как диска ОС hello, использование в модели развертывания диспетчера ресурсов hello."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3b7d3cd5-e3d7-4041-a2a7-0290447458ea
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: cynthn
ms.openlocfilehash: c72c6f4fb650e2664e87cf38ec9be62f0b2209fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-vm-from-a-specialized-disk"></a>Создание виртуальной машины Windows из специализированного диска

Создание новой виртуальной Машины путем присоединения специализированного диска управляемых как диска ОС hello, с помощью Powershell. Специализированного диска представляет собой копию виртуального жесткого диска (VHD) из существующей виртуальной Машины, который поддерживает учетные записи пользователей hello, приложений и других данных о состоянии из исходной виртуальной Машины. 

При использовании специализированных toocreate виртуального жесткого диска новой виртуальной Машины, приветствия новой виртуальной Машины сохраняет имя компьютера hello hello исходной виртуальной Машины. Другие сведения о компьютере также сохраняются и в некоторых случаях эти повторяющиеся данные могут вызвать проблемы. Следует учитывать, какие типы сведений о компьютере используют приложения при копировании виртуальной машины.

Существует два варианта.
* [Передача VHD](#option-1-upload-a-specialized-vhd)
* [Копирование имеющейся виртуальной машины Azure](#option-2-copy-an-existing-azure-vm)

В этом разделе показано, как toouse Управление дисками. При наличии развертывания устаревших версий, для которой требуется использовать учетную запись хранения, см. статью [Создание виртуальной машины на основе специализированного VHD в учетной записи хранения](sa-create-vm-specialized.md).

## <a name="before-you-begin"></a>Перед началом работы
При использовании PowerShell убедитесь, что последняя версия модуля AzureRM.Compute PowerShell hello hello. 

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Дополнительные сведения см. в разделе [об управлении версиями Azure PowerShell](/powershell/azure/overview).


## <a name="option-1-upload-a-specialized-vhd"></a>Вариант 1. Передача специализированного VHD

Можно передать hello создания виртуального жесткого диска от виртуальной Машины, специализированный со средством виртуализации в локальной среде, как Hyper-V или виртуальной Машины экспортирован из другого облака.

### <a name="prepare-hello-vm"></a>Подготовка виртуальной Машины hello
Если предполагается toouse hello VHD как-является toocreate новой виртуальной Машины, убедитесь, выполняются следующие шаги hello. 
  
  * [Подготовка виртуального жесткого диска Windows tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). **Нет** generalize hello виртуальную Машину с помощью Sysprep.
  * Удалите все гостевой средств виртуализации и агентов, установленных на hello виртуальной Машины (например, средства VMware tools).
  * Обеспечить hello виртуальной Машины является настроенным toopull его IP-адрес и параметры DNS через DHCP. Это гарантирует, что этот сервер hello получает IP-адрес в пределах hello виртуальной сети при запуске. 


### <a name="get-hello-storage-account"></a>Получение учетной записи хранилища hello
Требуется хранилище учетной записи в Azure toostore hello отправки виртуального жесткого диска. Можно использовать существующую учетную запись хранения или создать новую. 

tooshow hello доступных учетных записей хранилища, введите следующую команду:

```powershell
Get-AzureRmStorageAccount
```

Toouse существующую учетную запись хранения следует продолжить toohello [hello передачи виртуального жесткого диска](#upload-the-vhd-to-your-storage-account) раздела.

Если вам требуется toocreate учетной записи хранилища, выполните следующие действия.

1. Требуется имя hello hello группы ресурсов, которой должен быть создан hello учетной записи хранилища. toofind out все hello группы ресурсов в вашей подписке типа:
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    Группа ресурсов с именем toocreate *myResourceGroup* в hello *Запад США* региона, введите:

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. Создать учетную запись хранилища с именем *mystorageaccount* в этой группе ресурсов с помощью hello [New AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) командлета:
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```

### <a name="upload-hello-vhd-tooyour-storage-account"></a>Отправка виртуального жесткого диска для hello tooyour учетной записи хранилища 
Используйте hello [AzureRmVhd добавить](/powershell/module/azurerm.compute/add-azurermvhd) командлет tooupload hello VHD tooa контейнера в учетной записи хранилища. В этом примере файл hello передачи *myVHD.vhd* из `"C:\Users\Public\Documents\Virtual hard disks\"` tooa учетной записи хранилища с именем *mystorageaccount* в hello *myResourceGroup* группы ресурсов. Hello файл сохраняется в контейнер hello *mycontainer* и hello новый файл будет называться *myUploadedVHD.vhd*.

```powershell
$resourceGroupName = "myResourceGroup"
$urlOfUploadedVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $resourceGroupName -Destination $urlOfUploadedVhd `
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

В зависимости от сетевого подключения и hello размер файла виртуального жесткого диска, эта команда может занять некоторое время toocomplete

### <a name="create-a-managed-disk-from-hello-vhd"></a>Создание управляемого диска из hello виртуального жесткого диска

Создание управляемого диска из hello специализированные VHD в учетной записи хранилища с помощью [New AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk). В этом примере используется **myOSDisk1** для hello имя диска, помещает hello диск в *StandardLRS* хранилища, а также используется *https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd* как hello URI для hello исходного VHD.

Создать новую группу ресурсов для hello новой виртуальной Машины.

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

Создать новый диск ОС hello из hello отправки виртуального жесткого диска. 

```powershell
$sourceUri = https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd)
$osDiskName = 'myOsDisk'
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig -AccountType StandardLRS  -Location $location -CreateOption Import `
    -SourceUri $sourceUri) `
    -ResourceGroupName $destinationResourceGroup
```

## <a name="option-2-copy-an-existing-azure-vm"></a>Вариант 2. Копирование существующей виртуальной машины Azure

Можно создать копию виртуальной Машины, которая использует управляемый дисков с помощью снимка виртуальной Машины hello, то с помощью этого моментального снимка toocreate нового управляемого диска и новой виртуальной Машины.


### <a name="take-a-snapshot-of-hello-os-disk"></a>Создание снимка hello диска ОС

Вы можете сделать моментальный снимок всей виртуальной машины (включая все диски) или одного диска. Hello следующие шаги показывают, как моментальный снимок виртуальной Машины с помощью только что hello ОС диска tootake hello [New AzureRmSnapshot](/powershell/module/azurerm.compute/new-azurermsnapshot) командлета. 

Задайте некоторые параметры. 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$vmName = 'myVM'
$location = 'westus' 
$snapshotName = 'mySnapshot'  
```

Получение hello объекта виртуальной Машины.

```powershell
$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $resourceGroupName
```
Получите имя диска ОС hello.

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $vm.StorageProfile.OsDisk.Name
```

Создайте конфигурацию hello моментальных снимков. 

 ```powershell
$snapshotConfig =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -OsType Windows -CreateOption Copy -Location $location 
```

Снимок "hello".

```powershell
$snapShot = New-AzureRmSnapshot -Snapshot $snapshotConfig -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName
```


Если планируется toouse hello моментального снимка toocreate виртуальной Машины, которая должна toobe высокопроизводительной, используйте параметр hello `-AccountType Premium_LRS` с помощью команды New-AzureRmSnapshot hello. параметр Hello создает hello моментальных снимков, чтобы оно хранится как диск управляемых Premium. Управляемые диски уровня "Премиум" дороже, чем управляемые диски уровня "Стандартный". Поэтому убедитесь, что действительно требуется Premium перед использованием параметра hello.

### <a name="create-a-new-disk-from-hello-snapshot"></a>Создать новый диск из моментального снимка hello

Создание управляемого диска из моментального снимка с помощью hello [New AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk). В этом примере используется *myOSDisk* для hello имя диска.

Создать новую группу ресурсов для hello новой виртуальной Машины.

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

Задайте имя диска ОС hello. 

```powershell
$osDiskName = 'myOsDisk'
```

Создание управляемого диска hello.

```powershell
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig  -Location $location -CreateOption Copy `
    -SourceResourceId $snapshot.Id) `
    -ResourceGroupName $destinationResourceGroup
```


## <a name="create-hello-new-vm"></a>Создание новой виртуальной Машины hello 

Создание сети и другие ресурсы toobe виртуальных Машин, используемых hello новой виртуальной Машины.

### <a name="create-hello-subnet-and-vnet"></a>Создание подсети hello и виртуальной сети

Создание виртуальной сети hello и подсеть hello [виртуальной сети](../../virtual-network/virtual-networks-overview.md).

Создайте подсеть hello. В этом примере создается подсеть с именем **mySubNet**, в группе ресурсов hello **myDestinationResourceGroup**, и задает hello префикс адреса подсети слишком**10.0.0.0/24**.
   
```powershell
$subnetName = 'mySubNet'
$singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
```

Создание виртуальной сети hello. В этом примере задает hello toobe имя виртуальной сети **myVnetName**, hello расположение слишком**Запад США**, и hello префикс адреса для виртуальной сети hello слишком**10.0.0.0/16**. 
   
```powershell
$vnetName = "myVnetName"
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $destinationResourceGroup -Location $location `
    -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
```    


### <a name="create-hello-network-security-group-and-an-rdp-rule"></a>Создание группы безопасности сети hello и правило протокола удаленного рабочего СТОЛА
возможности toolog toobe в tooyour виртуальную Машину с помощью протокола удаленного рабочего СТОЛА, необходимо toohave правило безопасности, которое разрешает RDP-доступ через порт 3389. Поскольку hello виртуального жесткого диска для новой виртуальной Машине был создан из существующей виртуальной Машине специализированные hello, вы можете использовать учетную запись из hello исходной виртуальной машины для протокола удаленного рабочего СТОЛА.

В этом примере задает hello NSG имя слишком**myNsg** и hello RDP имя правила слишком**myRdpRule**.

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $destinationResourceGroup -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

Дополнительные сведения о конечных точках и правила NSG см. в разделе [Открытие портов tooa ВМ в Azure с помощью PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="create-a-public-ip-address-and-nic"></a>Создание общедоступного IP-адреса и сетевой карты
требуется tooenable взаимодействия с виртуальной машиной hello в виртуальной сети hello, [общедоступный IP-адрес](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) и сетевого интерфейса.

Создайте hello общедоступный IP-адрес. В этом примере имя hello открытый IP-адреса задано слишком**myIP**.
   
```powershell
$ipName = "myIP"
$pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $destinationResourceGroup -Location $location `
   -AllocationMethod Dynamic
```       

Создайте сетевую карту hello. В этом примере имя сетевого Адаптера hello задано слишком**myNicName**.
   
```powershell
$nicName = "myNicName"
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $destinationResourceGroup `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```



### <a name="set-hello-vm-name-and-size"></a>Задайте имя виртуальной Машины hello и размер

В этом примере задает hello имя виртуальной Машины слишком*myVM* а hello виртуальной Машины, размер слишком*Standard_A2*.

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-hello-nic"></a>Добавить hello сетевого Адаптера
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    

### <a name="add-hello-os-disk"></a>Добавить диск hello ОС 

Добавить hello ОС диска toohello конфигурации с помощью [AzureRmVMOSDisk набор](/powershell/module/azurerm.compute/set-azurermvmosdisk). В этом примере устанавливается размер hello hello диска слишком*128 ГБ* и присоединяет hello управляемый диск — как *Windows* диска ОС.
 
```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -StorageAccountType StandardLRS `
    -DiskSizeInGB 128 -CreateOption Attach -Windows
```

### <a name="complete-hello-vm"></a>Завершить hello виртуальной Машины 

Создание виртуальной Машины с помощью hello [New AzureRMVM](/powershell/module/azurerm.compute/new-azurermvm)hello конфигураций, которые мы только что создали.

```powershell
New-AzureRmVM -ResourceGroupName $destinationResourceGroup -Location $location -VM $vm
```

Если команда будет выполнена успешно, вы увидите примерно такой результат.

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-hello-vm-was-created"></a>Убедитесь, что hello создания виртуальной Машины
Вы увидите hello вновь созданные ВМ в hello [портал Azure](https://portal.azure.com)в разделе **Обзор** > **виртуальные машины**, или с помощью следующих PowerShell hello команды:

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $destinationResourceGroup
$vmList.Name
```

## <a name="next-steps"></a>Дальнейшие действия
toosign в новой виртуальной машины tooyour, toohello обзор виртуальных Машин в hello [портала](https://portal.azure.com), нажмите кнопку **Connect**и откройте hello файл удаленного рабочего СТОЛА. Используйте учетные данные учетной записи hello объекта к исходной виртуальной машины toosign tooyour новой виртуальной машине. Дополнительные сведения см. в разделе [как tooconnect и вход в систему tooan Azure виртуальные машины под управлением Windows](connect-logon.md).

