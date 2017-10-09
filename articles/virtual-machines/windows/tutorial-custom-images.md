---
title: "aaaCreate пользовательских образов виртуальной Машины с hello Azure PowerShell | Документы Microsoft"
description: "Учебник - создать образ виртуальной Машины с помощью hello Azure PowerShell."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 3a759fe1b7e7b72f531399b0f4a99e341713c6a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-powershell"></a>Создание пользовательского образа виртуальной машины Azure с помощью PowerShell

Пользовательские образы похожи на образы магазина, однако их можно создавать самостоятельно. Пользовательские изображения может быть конфигурации используется toobootstrap, такие как предварительной загрузки приложений, конфигурации приложений и других настроек операционной системы. В рамках этого руководства вы создадите собственный пользовательский образ виртуальной машины Azure. Вы узнаете, как выполнять следующие задачи:

> [!div class="checklist"]
> * Подготовка виртуальной машины к использованию с помощью Sysprep
> * Создание пользовательского образа
> * Создание виртуальной машины из пользовательского образа
> * Отображение списка всех образов hello в подписке
> * удалять образ.

Этот учебник требует hello Azure PowerShell модуль версии 3.6 или более поздней версии. Запустите ` Get-Module -ListAvailable AzureRM` версии toofind hello. Получить tooupgrade [установите Azure PowerShell модуль](/powershell/azure/install-azurerm-ps).

## <a name="before-you-begin"></a>Перед началом работы

в следующих шагах Hello подробно, как tootake существующей виртуальной Машины и включите его в доступных для использования пользовательского образа, который можно использовать toocreate новые экземпляры виртуальной Машины.

Пример hello toocomplete в этом учебнике, необходимо иметь существующую виртуальную машину. Этот [пример сценария](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) позволяет создать ее при необходимости. Если заменить прохождение учебника hello группы ресурсов hello и ВМ имен при необходимости.

## <a name="prepare-vm"></a>Подготовка виртуальной машины

toocreate образ виртуальной машины, необходимо tooprepare hello ВМ путем выявления hello виртуальной Машины, освобождение и пометки hello исходной виртуальной Машины, как обобщенный в Azure.

### <a name="generalize-hello-windows-vm-using-sysprep"></a>Обобщить hello виртуальной Машины Windows с помощью программы Sysprep

Sysprep удаляет все ваши личные сведения, помимо прочего и подготавливает toobe машины hello, используемое в качестве изображения. Дополнительные сведения о программе Sysprep см. в разделе [как tooUse Sysprep: введение](http://technet.microsoft.com/library/bb457073.aspx).


1. Подключение toohello виртуальной машины.
2. Привет открыть окно командной строки с правами администратора. Измените каталог hello слишком*%windir%\system32\sysprep*, а затем запустите *sysprep.exe*.
3. В hello **средство подготовки системы** выберите *Enter System Out-of-Box Experience (OOBE)*и убедитесь, что hello *Generalize* установлен флажок.
4. В разделе **Параметры завершения работы** выберите *Завершение работы* и нажмите кнопку **ОК**.
5. По завершении работы программы Sysprep завершает hello виртуальной машины. **Не перезагружайте hello виртуальной Машины**.

### <a name="deallocate-and-mark-hello-vm-as-generalized"></a>Выделение и пометить hello виртуальной Машины как обобщенный

toocreate изображения hello виртуальной Машины должен toobe освобожден и отмечается как обобщенный в Azure.

Освобожденные hello виртуальной Машины с помощью [Stop AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Force
```

Задать состояние hello hello виртуальной машины слишком`-Generalized` с помощью [AzureRmVm набор](/powershell/module/azurerm.compute/set-azurermvm). 
   
```powershell
Set-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Generalized
```


## <a name="create-hello-image"></a>Создание образа hello

Теперь можно создавать с помощью образа виртуальной Машины hello [New AzureRmImageConfig](/powershell/module/azurerm.compute/new-azurermimageconfig) и [New AzureRmImage](/powershell/module/azurerm.compute/new-azurermimage). Hello следующий пример создает образ с именем *myImage* из виртуальной Машины с именем *myVM*.

Получение hello виртуальной машины. 

```powershell
$vm = Get-AzureRmVM -Name myVM -ResourceGroupName myResourceGroupImages
```

Создайте конфигурацию hello изображения.

```powershell
$image = New-AzureRmImageConfig -Location EastUS -SourceVirtualMachineId $vm.ID 
```

Создание образа hello.

```powershell
New-AzureRmImage -Image $image -ImageName myImage -ResourceGroupName myResourceGroupImages
``` 

 
## <a name="create-vms-from-hello-image"></a>Создать виртуальные машины из образа hello

Теперь, когда у вас есть образ, можно создать один или несколько новых виртуальных машин из образа hello. Создание виртуальной Машины из образа — очень похожа toocreating ВМ с помощью образа Marketplace. При использовании образа Marketplace, у вас есть tooinformation о hello изображения, поставщик образов, предложение, SKU и версии. С помощью пользовательского образа необходимо просто tooprovide идентификатор hello hello пользовательский ресурс изображения. 

В следующий скрипт hello, мы создадим переменной *$image* toostore сведения об использовании настраиваемого образа hello [Get AzureRmImage](/powershell/module/azurerm.compute/get-azurermimage) и затем мы используем [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage)и укажите идентификатор hello, с помощью hello *$image* переменной мы только что создали. 

Hello скрипт создает Виртуальную машину с именем *myVMfromImage* из наших настраиваемого изображения в новую группу ресурсов с именем *myResourceGroupFromImage* в hello *Запад США* расположение.


```powershell
$cred = Get-Credential -Message "Enter a username and password for hello virtual machine."

New-AzureRmResourceGroup -Name myResourceGroupFromImage -Location EastUS

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name MYvNET `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

$pip = New-AzureRmPublicIpAddress `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name "mypublicdns$(Get-Random)" `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4

  $nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

  $nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP

$nic = New-AzureRmNetworkInterface `
    -Name myNic `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $pip.Id `
    -NetworkSecurityGroupId $nsg.Id

$vmConfig = New-AzureRmVMConfig `
    -VMName myVMfromImage `
    -VMSize Standard_D1 | Set-AzureRmVMOperatingSystem -Windows `
        -ComputerName myComputer `
        -Credential $cred 

# Here is where we create a variable toostore information about hello image 
$image = Get-AzureRmImage `
    -ImageName myImage `
    -ResourceGroupName myResourceGroupImages

# Here is where we specify that we want toocreate hello VM from and image and provide hello image ID
$vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -Id $image.Id

$vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id

New-AzureRmVM `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -VM $vmConfig
```

## <a name="image-management"></a>Управление образами 

Ниже приведены некоторые примеры типичных задач управления изображения и как toocomplete их с помощью PowerShell.

Вывод списка всех образов по имени.

```powershell
$images = Find-AzureRMResource -ResourceType Microsoft.Compute/images 
$images.name
```

Удаление образа. Этот пример удаляет hello изображение с именем *myOldImage* из hello *myResourceGroup*.

```powershell
Remove-AzureRmImage `
    -ImageName myOldImage `
    -ResourceGroupName myResourceGroup
```

## <a name="next-steps"></a>Дальнейшие действия

В рамках этого руководства вы создали пользовательский образ виртуальной машины. Вы научились выполнять следующие задачи:

> [!div class="checklist"]
> * Подготовка виртуальной машины к использованию с помощью Sysprep
> * Создание пользовательского образа
> * Создание виртуальной машины из пользовательского образа
> * Отображение списка всех образов hello в подписке
> * удалять образ.

Переместить следующий учебник toolearn toohello о том, как высокодоступные виртуальные машины.

> [!div class="nextstepaction"]
> [Создание высокодоступных виртуальных машин](tutorial-availability-sets.md)



