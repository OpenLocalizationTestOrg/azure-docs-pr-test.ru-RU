---
title: "aaaCreate управляемый образ в Azure | Документы Microsoft"
description: "Создание управляемого образа универсальной виртуальной машины или виртуального жесткого диска в Azure. Изображения могут быть toocreate используется несколько виртуальных машин, использующих управляемый дисков."
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
ms.date: 02/27/2017
ms.author: cynthn
ms.openlocfilehash: d8cd6c2ce8c5d704de2c845abced85139944d682
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-image-of-a-generalized-vm-in-azure"></a>Создание управляемого образа универсальной виртуальной машины в Azure

Ресурс управляемого образа можно создать из универсальной виртуальной машины, которая хранится в виде управляемого диска или неуправляемых дисков в учетной записи хранения. Здравствуйте, изображение может затем быть toocreate используется несколько виртуальных машин. 


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


## <a name="create-a-managed-image-in-hello-portal"></a>Создать управляемый образ на портале hello 

1. Откройте hello [портала](https://portal.azure.com).
2. Щелкните hello плюс toocreate новый ресурс.
3. В поле фильтра поиска hello введите **изображения**.
4. Выберите **изображения** из результатов hello.
5. В hello **изображения** колонка, щелкните **создать**.
6. В **имя**, введите имя образа hello.
7. Если имеется несколько подписок, выберите hello правильный выбор из hello **подписки** раскрывающегося списка.
7. В **группы ресурсов** выберите **создать новый** и введите имя или выберите **из существующего** и выберите из раскрывающегося списка hello toouse группы ресурсов.
8. В **расположение**, выберите расположение hello группы ресурсов.
9. В **тип ОС** выберите hello тип операционной системы Windows или Linux.
11. В **BLOB-объекта хранилища**, нажмите кнопку **Обзор** toolook для hello виртуального жесткого диска в службе хранилища Azure.
12. В поле **Тип учетной записи** выберите Standard_LRS или Premium_LRS. Для уровня "Стандартный" используются жесткие диски, а для уровня "Премиум" — твердотельные накопители. Для обоих уровней используется локально избыточное хранилище.
13. В **кэширования диска** Здравствуйте, выберите соответствующий диск параметр кэширования. Параметры Hello **нет**, **только для чтения** и **находится**.
14. Необязательно: Можно также добавить образ toohello диска данных, щелкнув **+ добавить диск данных**.  
15. Завершив настройку параметров, нажмите кнопку **Создать**.
16. После создания образа hello, вы увидите его как **изображения** ресурс в список hello ресурсов в группе ресурсов hello выбрано.



## <a name="create-a-managed-image-of-a-vm-using-powershell"></a>Создание управляемого образа виртуальной машины с помощью PowerShell

Создание образа непосредственно из виртуальных Машин гарантирует, что это изображение hello приветствия включает все hello диски, связанные с hello виртуальной Машины, включая hello диска ОС и дисков данных.


Прежде чем начать, убедитесь, что последняя версия модуля AzureRM.Compute PowerShell hello hello. Запустите hello следующие tooinstall команды.

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Дополнительные сведения см. в разделе [об управлении версиями Azure PowerShell](/powershell/azure/overview).


1. Создайте несколько переменных.

    ```powershell
    $vmName = "myVM"
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $imageName = "myImage"
    ```
2. Убедитесь, что виртуальная машина была освобождена приветствия.

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. Задать состояние hello hello виртуальной машины слишком**универсальная**. 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized
    ```
    
4. Получение hello виртуальной машины. 

    ```powershell
    $vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName
    ```

5. Создайте конфигурацию hello изображения.

    ```powershell
    $image = New-AzureRmImageConfig -Location $location -SourceVirtualMachineId $vm.ID 
    ```
6. Создание образа hello.

    ```powershell
    New-AzureRmImage -Image $image -ImageName $imageName -ResourceGroupName $rgName
    ``` 



## <a name="create-a-managed-image-of-a-vhd-in-powershell"></a>Создание управляемого образа виртуального жесткого диска с помощью PowerShell

Создайте управляемый образ с помощью универсального виртуального жесткого диска ОС.


1.  Во-первых можно задать общие параметры hello:

    ```powershell
    $rgName = "myResourceGroupName"
    $vmName = "myVM"
    $location = "West Central US" 
    $imageName = "yourImageName"
    $osVhdUri = "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd"
    ```
2. Здравствуйте, Step\deallocate виртуальной Машины.

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. Пометьте виртуальной Машины как обобщенный hello.

    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized 
    ```
4.  Создайте образ hello, с помощью общего виртуального жесткого диска операционной системы.

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $osVhdUri
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```


## <a name="create-a-managed-image-from-a-snapshot-using-powershell"></a>Создание управляемого образа из моментального снимка с помощью PowerShell

Можно также создать управляемый образ из моментального снимка hello VHD из универсальной ВМ.

    
1. Создайте несколько переменных. 

    ```powershell
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $snapshotName = "mySnapshot"
    $imageName = "myImage"
    ```

2. Получение моментальных снимков hello.

   ```powershell
   $snapshot = Get-AzureRmSnapshot -ResourceGroupName $rgName -SnapshotName $snapshotName
   ```
   
3. Создайте конфигурацию hello изображения.

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsState Generalized -OsType Windows -SnapshotId $snapshot.Id
    ```
4. Создание образа hello.

    ```powershell
    New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ``` 
    

## <a name="next-steps"></a>Дальнейшие действия
- Теперь вы можете [создания виртуальной Машины из образа управляемого hello обобщенный](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).    

