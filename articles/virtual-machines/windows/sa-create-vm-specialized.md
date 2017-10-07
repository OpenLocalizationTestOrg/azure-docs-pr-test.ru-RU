---
title: "aaaCreate виртуальной Машины из специализированного диска в Azure | Документы Microsoft"
description: "Создание новой виртуальной Машины путем присоединения неуправляемые специализированного диска, в модели развертывания диспетчера ресурсов hello."
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
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: c88f213b6629a6c1d6ff5845e76c2f7719672714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-from-a-specialized-vhd-in-a-storage-account"></a>Создание виртуальной машины на основе специализированного VHD в учетной записи хранения

Создание новой виртуальной Машины путем присоединения специализированный неуправляемым диск как диск ОС hello, с помощью Powershell. Специализированного диска представляет собой копию виртуального жесткого диска из существующей виртуальной Машины, который поддерживает учетные записи пользователей hello, приложений и других данных о состоянии из исходной виртуальной Машины. 

Существует два варианта.
* [Передача VHD](create-vm-specialized.md#option-1-upload-a-specialized-vhd)
* [Скопируйте hello виртуальный жесткий ДИСК существующей виртуальной Машине Azure](create-vm-specialized.md#option-2-copy-an-existing-azure-vm)

## <a name="before-you-begin"></a>Перед началом работы
При использовании PowerShell убедитесь, что последняя версия модуля AzureRM.Compute PowerShell hello hello. Запустите hello следующие tooinstall команды.

```powershell
Install-Module AzureRM.Compute 
```
Дополнительные сведения см. в разделе [об управлении версиями Azure PowerShell](/powershell/azure/overview).


## <a name="option-1-upload-a-specialized-vhd"></a>Вариант 1. Передача специализированного VHD

Можно передать hello создания виртуального жесткого диска от виртуальной Машины, специализированный со средством виртуализации в локальной среде, как Hyper-V или виртуальной Машины экспортирован из другого облака.

### <a name="prepare-hello-vm"></a>Подготовка виртуальной Машины hello
Вы можете передать специализированный VHD, созданный с помощью локальной виртуальной машины, или VHD, экспортированный из другого облака. Специализированные виртуальный жесткий ДИСК поддерживает учетные записи пользователей hello, приложений и других данных о состоянии из исходной виртуальной Машины. Если предполагается toouse hello VHD как-является toocreate новой виртуальной Машины, убедитесь, выполняются следующие шаги hello. 
  
  * [Подготовка виртуального жесткого диска Windows tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). **Нет** generalize hello виртуальную Машину с помощью Sysprep.
  * Удалите все гостевой средств виртуализации и агентов, установленных на hello виртуальной Машины (т. е. средства VMware).
  * Обеспечить hello виртуальной Машины является настроенным toopull его IP-адрес и параметры DNS через DHCP. Это гарантирует, что этот сервер hello получает IP-адрес в пределах hello виртуальной сети при запуске. 


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
   
### <a name="upload-hello-vhd-tooyour-storage-account"></a>Отправка виртуального жесткого диска для hello tooyour учетной записи хранилища
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


## <a name="option-2-copy-hello-vhd-from-an-existing-azure-vm"></a>Вариант 2: Скопируйте hello виртуального жесткого диска из существующей виртуальной Машине Azure

При создании новой, повторяющиеся ВМ можно скопировать toouse учетной записи хранилища tooanother виртуального жесткого диска.

### <a name="before-you-begin"></a>Перед началом работы
Убедитесь, что выполнены следующие условия.

* Сведения о hello **источника и назначения учетных записей хранения**. Hello исходной виртуальной Машины необходимо toohave hello учетной записи и контейнер имена хранилища. Как правило, будет имя контейнера hello **виртуальные жесткие диски**. Необходимо также toohave целевой учетной записью хранения. Если у вас еще нет один, можно создать один с помощью портала hello (**более служб** > учетные записи хранения > Добавить) или с помощью hello [New AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) командлета. 
* Загружено и установлено hello [средство AzCopy](../../storage/common/storage-use-azcopy.md). 

### <a name="deallocate-hello-vm"></a>DEALLOCATE hello виртуальной Машины
Неудачная попытка освобождения hello виртуальную Машину, которая освобождает toobe VHD hello копируются. 

* **Портал**: щелкните **Виртуальные машины** > **myVM** > Остановить
* **PowerShell**: использование [Stop AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) toostop (освобождении) виртуальной Машины с именем hello **myVM** в группе ресурсов **myResourceGroup**.

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

Hello **состояние** для hello ВМ в hello Azure портал изменения из **остановлена** слишком**остановлена (освобождена)**.

### <a name="get-hello-storage-account-urls"></a>Получение URL-адреса учетной записи хранилища hello
Требуется URL-адреса hello hello источника и назначения учетных записей хранения. Hello URL-адреса выглядеть следующим образом: `https://<storageaccount>.blob.core.windows.net/<containerName>/`. Если известно имя учетной записи и контейнера хранилища hello, можно просто замените hello информации между toocreate скобки hello URL-адрес. 

Можно использовать hello портал Azure или Azure Powershell tooget hello, URL-адрес:

* **Портал**: щелкните hello  **>**  для **дополнительные службы** > **учетные записи хранения**  >   *Учетная запись хранения* > **большие двоичные объекты** и исходного файла виртуального жесткого диска, возможно, находится в hello **виртуальные жесткие диски** контейнера. Нажмите кнопку **свойства** для контейнера hello и копировать текст hello с меткой **URL-адрес**. Вам потребуется hello URL-адреса источника и назначения контейнеров обеих hello. 
* **PowerShell**: использование [Get AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) tooget hello сведения для виртуальной Машины с именем **myVM** в группе ресурсов hello **myResourceGroup**. В результатах hello папка hello **профиль хранилища** раздел для hello **Uri VHD-файла**. Первая часть Hello hello Uri — контейнер toohello hello URL-адрес и hello последней части — hello имени виртуального жесткого диска операционной системы для виртуальной Машины hello.

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
``` 

## <a name="get-hello-storage-access-keys"></a>Получить ключи доступа к хранилищу hello
Найти hello ключи доступа для hello источника и назначения учетные записи хранения. Дополнительные сведения о ключах доступа см. в статье [Об учетных записях хранения Azure](../../storage/common/storage-create-storage-account.md).

* **Портал.** Щелкните **Больше служб** > **Учетные записи хранения** > *учетная запись хранения* > **Ключи доступа**. Копировать ключ hello помечены как **key1**.
* **PowerShell**: использование [Get AzureRmStorageAccountKey](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) tooget hello хранилища ключ учетной записи хранения hello **mystorageaccount** в группе ресурсов hello  **myResourceGroup**. Копировать hello ключ с меткой **key1**.

```powershell
Get-AzureRmStorageAccountKey -Name mystorageaccount -ResourceGroupName myResourceGroup
```

### <a name="copy-hello-vhd"></a>Скопируйте hello виртуального жесткого диска
С помощью AzCopy можно копировать файлы между учетными записями хранения. Для hello конечный контейнер Если hello указанный контейнер не существует, он создается автоматически. 

toouse AzCopy, откройте командную строку на локальном компьютере и перейдите в папку toohello для установки AzCopy. Он будет выглядеть слишком*\Microsoft SDKs\Azure\AzCopy C:\Program Files (x86)*. 

toocopy hello все файлы в контейнере, используйте hello **/S** переключения. Это может быть hello используется toocopy виртуального жесткого диска операционной системы и Здравствуйте, все диски данных hello, если они находятся в одном контейнере. В этом примере показано, как все hello файлы в контейнере hello toocopy **mysourcecontainer** в учетной записи хранения **mysourcestorageaccount** toohello контейнера **mydestinationcontainer**  в hello **mydestinationstorageaccount** учетной записи хранилища. Замените приветствия имен учетных записей хранилища hello и контейнеры свои собственные. Замените ключи `<sourceStorageAccountKey1>` и `<destinationStorageAccountKey1>` своими собственными.

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
    /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
    /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> /S
```

Требуется только toocopy конкретного виртуального жесткого диска в контейнере с несколькими файлами, также можно указать имя файла hello, с помощью переключателя /Pattern hello. В этом примере hello только файл с именем **myFileName.vhd** будут скопированы.

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
  /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
  /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> `
  /Pattern:myFileName.vhd
```


По завершении отобразится сообщение следующего вида:

```
Finished 2 of total 2 file(s).
[2016/10/07 17:37:41] Transfer summary:
-----------------
Total files transferred: 2
Transfer successfully:   2
Transfer skipped:        0
Transfer failed:         0
Elapsed time:            00.00:13:07
```

### <a name="troubleshooting"></a>Устранение неполадок
* При использовании AZCopy, при возникновении ошибки hello «Серверу не удалось tooauthenticate hello запроса», убедитесь, что hello значение заголовка авторизации hello имеет правильный формат, включая подпись hello. При использовании 2 ключ или ключ hello дополнительного хранилища, попробуйте использовать ключ хранилища первичной или 1-го hello.

## <a name="create-hello-new-vm"></a>Создание новой виртуальной Машины hello 

Требуется toocreate сети и другие ресурсы toobe виртуальных Машин, используемых hello новой виртуальной Машины.

### <a name="create-hello-subnet-and-vnet"></a>Создание подсети hello и виртуальной сети

Создание виртуальной сети hello и подсеть hello [виртуальной сети](../../virtual-network/virtual-networks-overview.md).

1. Создайте подсеть hello. В этом примере создается подсеть с именем **mySubNet**, в группе ресурсов hello **myResourceGroup**, и задает hello префикс адреса подсети слишком**10.0.0.0/24**.
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubNet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. Создание виртуальной сети hello. В этом примере задает hello toobe имя виртуальной сети **myVnetName**, hello расположение слишком**Запад США**, и hello префикс адреса для виртуальной сети hello слишком**10.0.0.0/16**. 
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnetName"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-nic"></a>Создание общедоступного IP-адреса и сетевой карты
требуется tooenable взаимодействия с виртуальной машиной hello в виртуальной сети hello, [общедоступный IP-адрес](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) и сетевого интерфейса.

1. Создайте hello общедоступный IP-адрес. В этом примере имя hello открытый IP-адреса задано слишком**myIP**.
   
    ```powershell
    $ipName = "myIP"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. Создайте сетевую карту hello. В этом примере имя сетевого Адаптера hello задано слишком**myNicName**.
   
    ```powershell
    $nicName = "myNicName"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a>Создание группы безопасности сети hello и правило протокола удаленного рабочего СТОЛА
возможности toolog toobe в tooyour виртуальную Машину с помощью протокола удаленного рабочего СТОЛА, необходимо toohave правило безопасности, которое разрешает доступ RDP через порт 3389. Поскольку специальным hello виртуального жесткого диска для создания новой виртуальной Машины из существующего hello виртуальной Машины, после создания вы hello виртуальной Машины можно использовать существующую учетную запись из hello исходной виртуальной машины было toolog разрешение на использование протокола удаленного рабочего СТОЛА.
В этом примере задает hello NSG имя слишком**myNsg** и hello RDP имя правила слишком**myRdpRule**.

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

Дополнительные сведения о конечных точках и правила NSG см. в разделе [Открытие портов tooa ВМ в Azure с помощью PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="set-hello-vm-name-and-size"></a>Задайте имя виртуальной Машины hello и размер

В этом примере задает hello имя виртуальной Машины слишком «myVM» и hello ВМ размер слишком «Standard_A2».
```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-hello-nic"></a>Добавить hello сетевого Адаптера
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    
    
### <a name="configure-hello-os-disk"></a>Настройка диска hello ОС

1. Задайте hello URI для виртуального жесткого диска, загруженного или скопированного hello. В этом примере hello VHD-файл с именем **myOsDisk.vhd** сохраняется в учетную запись хранения с именем **myStorageAccount** в контейнер с именем **myContainer**.

    ```powershell
    $osDiskUri = "https://myStorageAccount.blob.core.windows.net/myContainer/myOsDisk.vhd"
    ```
2. Добавьте диск hello ОС. В этом примере при создании диска ОС hello hello термин «osDisk» — appened toohello ВМ имя toocreate hello имя диска ОС. В этом примере также указывает, этого виртуального жесткого диска на основе Windows должно быть вложенных toohello виртуальную Машину в качестве диска ОС hello.
    
    ```powershell
    $osDiskName = $vmName + "osDisk"
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption attach -Windows
    ```

Необязательно: При наличии дисков с данными, toobe необходимость присоединенного toohello виртуальной Машины, добавьте hello диски с данными с помощью URL-адреса hello данных виртуальные жесткие диски и hello соответствующий логический номер устройства (Lun).

```powershell
$dataDiskName = $vmName + "dataDisk"
$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -VhdUri $dataDiskUri -Lun 1 -CreateOption attach
```

При использовании учетной записи хранилища, hello данные и URL-адреса для диска операционной системы выглядеть примерно следующим образом: `https://StorageAccountName.blob.core.windows.net/BlobContainerName/DiskName.vhd`. Его можно найти на портале hello путем просмотра контейнера хранилища целевой toohello, щелкнув hello операционной системы или виртуального жесткого диска, который был скопирован, данные и скопировав в нее содержимое hello hello URL-адрес.


### <a name="complete-hello-vm"></a>Завершить hello виртуальной Машины 

Создайте виртуальную Машину с помощью hello конфигураций, которые мы только что создали hello.

```powershell
#Create hello new VM
New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
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
$vmList = Get-AzureRmVM -ResourceGroupName $rgName
$vmList.Name
```

## <a name="next-steps"></a>Дальнейшие действия
toosign в новой виртуальной машины tooyour, toohello обзор виртуальных Машин в hello [портала](https://portal.azure.com), нажмите кнопку **Connect**и откройте hello файл удаленного рабочего СТОЛА. Используйте учетные данные учетной записи hello объекта к исходной виртуальной машины toosign tooyour новой виртуальной машине. Дополнительные сведения см. в разделе [как tooconnect и вход в систему tooan Azure виртуальные машины под управлением Windows](connect-logon.md).

