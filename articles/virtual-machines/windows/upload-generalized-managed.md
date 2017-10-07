---
title: "aaaCreate управляемого виртуальной Машины Azure на основе VHD обобщенный локальной | Документы Microsoft"
description: "Отправка обобщенный tooAzure виртуальный жесткий ДИСК и использовать его toocreate новых виртуальных машин, в модели развертывания диспетчера ресурсов hello."
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
ms.date: 05/19/2017
ms.author: cynthn
ms.openlocfilehash: 2fd0c0eec922e6ca8af4e712c1bceb1f9466105c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-generalized-vhd-and-use-it-toocreate-new-vms-in-azure"></a>Отправка обобщенный виртуальный жесткий ДИСК и использовать его toocreate новые виртуальные машины в Azure

Этот раздел поможет выполнить с помощью PowerShell tooupload VHD обобщенный tooAzure виртуальной Машины, создать образ на hello виртуальный жесткий ДИСК и создать новую виртуальную Машину из этого образа. Вы можете отправить диск VHD, экспортированный из локального инструмента виртуализации или из другого облака. С помощью [управляемых дисков](managed-disks-overview.md) для hello новой виртуальной Машины, упрощает управление виртуальными Машинами hello и предоставляет более высокую доступность при помещении hello виртуальной Машины в группу доступности. 

Если toouse образец скрипта, см. [образца сценария tooupload tooAzure виртуального жесткого диска и создание новой виртуальной Машины](../scripts/virtual-machines-windows-powershell-upload-generalized-script.md)

## <a name="before-you-begin"></a>Перед началом работы

- Перед отправкой tooAzure любого виртуального жесткого диска, необходимо следовать [Подготовка виртуального жесткого диска Windows или VHDX tooAzure tooupload](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
- Просмотрите [план миграции hello дисков tooManaged](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks) перед началом переноса слишком[управляемых дисков](managed-disks-overview.md).
- Убедитесь, что последняя версия модуля AzureRM.Compute PowerShell hello hello. Запустите hello следующие tooinstall команды.

    ```powershell
    Install-Module AzureRM.Compute -RequiredVersion 2.6.0
    ```
    Дополнительные сведения см. в разделе [об управлении версиями Azure PowerShell](/powershell/azure/overview).


## <a name="generalize-hello-windows-vm-using-sysprep"></a>Обобщить hello виртуальной Машины Windows с помощью программы Sysprep

Sysprep удаляет все ваши личные сведения, помимо прочего и подготавливает toobe машины hello, используемое в качестве изображения. Дополнительные сведения о программе Sysprep см. в разделе [как tooUse Sysprep: введение](http://technet.microsoft.com/library/bb457073.aspx).

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
6. По завершении работы программы Sysprep завершает hello виртуальной машины. Не перезагружайте hello виртуальной Машины.



## <a name="log-in-tooazure"></a>Войдите в tooAzure
Если у вас еще нет PowerShell версии 1.4 или выше установлены, чтение [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).

1. Откройте Azure PowerShell и войдите в tooyour учетная запись Azure. Откроется всплывающее окно учетные данные учетной записи Azure tooenter вы.
   
    ```powershell
    Login-AzureRmAccount
    ```
2. Получите подписку hello идентификаторы для доступных подписок.
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. Набор hello нужной подписки с идентификатором hello подписки. Замените  *<subscriptionID>*  с Идентификатором hello hello исправить подписки.
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="get-hello-storage-account"></a>Получение учетной записи хранилища hello
Требуется учетная запись хранения в образе виртуальной Машины Azure toostore hello отправлен. Можно использовать существующую учетную запись хранения или создать новую. 

Если вы будете использовать toocreate VHD hello управляемого диска для виртуальной Машины, hello расположение учетной записи хранения необходимо местоположения hello, в которых будет создаваться hello виртуальной Машины.

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

    Группа ресурсов с именем toocreate **myResourceGroup** в hello **Восток США** региона, введите:

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "East US"
    ```

2. Создать учетную запись хранилища с именем **mystorageaccount** в этой группе ресурсов с помощью hello [New AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) командлета:
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "East US"`
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
    Допустимые значения -SkuName перечислены ниже.
   
   * **Standard_LRS** — локально избыточное хранилище. 
   * **Standard_ZRS** — хранилище, избыточное в пределах зоны.
   * **Standard_GRS** — геоизбыточное хранилище. 
   * **Standard_RAGRS** — геоизбыточное хранилище с доступом только для чтения. 
   * **Premium_LRS** — локально избыточное хранилище уровня "Премиум". 

## <a name="upload-hello-vhd-tooyour-storage-account"></a>Отправка виртуального жесткого диска для hello tooyour учетной записи хранилища

Используйте hello [AzureRmVhd добавить](https://msdn.microsoft.com/library/mt603554.aspx) командлет tooupload hello VHD tooa контейнера в учетной записи хранилища. В этом примере файл hello передачи *myVHD.vhd* из *» C:\Users\Public\Documents\Virtual жестких дисков\"*  tooa учетной записи хранилища с именем *mystorageaccount*в hello *myResourceGroup* группы ресурсов. Hello файла будут помещены в контейнер hello *mycontainer* и hello новый файл будет называться *myUploadedVHD.vhd*.

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

В зависимости от сетевого подключения и hello размер файла виртуального жесткого диска, эта команда может занять некоторое время toocomplete

Сохранить hello **конечный URI** toouse путь к более поздней версии, если вы собираетесь toocreate управляемого диска или новой виртуальной Машины с помощью hello отправлены виртуального жесткого диска.

### <a name="other-options-for-uploading-a-vhd"></a>Другие возможности загрузки виртуального жесткого диска
 
 
Можно также передать учетную запись хранения tooyour виртуального жесткого диска с помощью одного из следующих hello:

- [AzCopy](http://aka.ms/downloadazcopy)
- [API копирования BLOB-объекта хранилища Azure](https://msdn.microsoft.com/library/azure/dd894037.aspx)
- [Обозреватель хранилищ Azure для передачи больших двоичных объектов](https://azurestorageexplorer.codeplex.com/)
- [Справочник по API REST служб хранилища импорта и экспорта](https://msdn.microsoft.com/library/dn529096.aspx)
-   Мы рекомендуем использовать службу импорта и экспорта, если предполагаемое время передачи больше 7 дней. Можно использовать [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) tooestimate время hello из единицу размера и передачи данных. 
    Импорт и экспорт можно использовать toocopy tooa Стандартная учетная запись хранения. Вам потребуется toocopy из учетной записи хранения toopremium стандартного хранилища с помощью таких средств, как AzCopy.


## <a name="create-a-managed-image-from-hello-uploaded-vhd"></a>Создавать управляемые отправить изображение из hello виртуального жесткого диска 

Создайте управляемый образ с помощью универсального виртуального жесткого диска ОС. Замените значения hello своих собственных сведений.


1.  Во-первых можно задать общие параметры hello:

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    $vmSize = "Standard_DS1_v2"
    $location = "East US" 
    $imageName = "yourImageName"
    ```

4.  Создайте образ hello, с помощью общего виртуального жесткого диска операционной системы.

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $urlOfUploadedImageVhd
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```

## <a name="create-a-virtual-network"></a>Создать виртуальную сеть
Создание виртуальной сети hello и подсеть hello [виртуальной сети](../../virtual-network/virtual-networks-overview.md).

1. Создайте подсеть hello. В этом примере создается подсеть с именем *mySubnet* с префикс адреса hello *10.0.0.0/24*.  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. Создайте виртуальную сеть hello. В этом примере создается виртуальная сеть с именем *myVnet* с префикс адреса hello *10.0.0.0/16*.  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a>Создание общедоступного IP-адреса и сетевого интерфейса

требуется tooenable взаимодействия с виртуальной машиной hello в виртуальной сети hello, [общедоступный IP-адрес](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) и сетевого интерфейса.

1. Создание общедоступного IP-адреса. В этом примере создается общедоступный IP-адрес с именем *myPip*. 
   
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

В этом примере создается группа безопасности сети с именем *myNsg*, которая содержит правило с именем *myRdpRule*, разрешающее трафик RDP через порт 3389. Дополнительные сведения о Nsg см. в разделе [Открытие портов tooa ВМ в Azure с помощью PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

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

## <a name="add-hello-vm-name-and-size-toohello-vm-configuration"></a>Добавьте hello имя виртуальной Машины и конфигурация виртуальной Машины toohello размера.

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-hello-vm-image-as-source-image-for-hello-new-vm"></a>Образ виртуальной Машины hello набор как источник изображения hello новой виртуальной Машины

Задать hello исходного образа с помощью идентификатора hello hello управляемый образ виртуальной Машины.

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-hello-os-configuration-and-add-hello-nic"></a>Задание конфигурации hello ОС и добавление hello сетевого адаптера.

Введите тип хранения hello (PremiumLRS или StandardLRS) и hello размер диска операционной системы hello. В следующем примере тип учетной записи hello слишком*PremiumLRS*, hello размер диска слишком*128 ГБ* и их кэширование слишком*ReadWrite*.

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-hello-vm"></a>Создание виртуальной Машины hello

Создание новой виртуальной Машины с помощью hello конфигурации хранятся в hello hello **$vm** переменной.

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

toosign в новой виртуальной машины tooyour, toohello обзор виртуальных Машин в hello [портала](https://portal.azure.com), нажмите кнопку **Connect**и откройте hello файл удаленного рабочего СТОЛА. Используйте учетные данные учетной записи hello объекта к исходной виртуальной машины toosign tooyour новой виртуальной машине. Дополнительные сведения см. в разделе [как tooconnect и вход в систему tooan Azure виртуальные машины под управлением Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

