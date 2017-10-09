---
title: "aaaCreate и управление виртуальными машинами Windows с hello модуля Azure PowerShell | Документы Microsoft"
description: "Учебник — Создание и управление виртуальными машинами Windows с hello модуля Azure PowerShell"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 20adcb673ef4de683e6ad82d048a9625a1dc838c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-with-hello-azure-powershell-module"></a>Создание и управление виртуальными машинами Windows с hello модуля Azure PowerShell

Виртуальные машины Azure предоставляют полностью настраиваемую и гибкую вычислительную среду. В этом руководстве рассматриваются основные элементы развертывания виртуальной машины Azure, например выбор ее размера, образа и ее развертывание. Вы узнаете, как выполнять следующие задачи:

> [!div class="checklist"]
> * Создать и присоединить tooa виртуальной Машины
> * Выбор и использование образов виртуальных машин
> * Просмотр и использование определенных размеров виртуальных машин
> * Изменение размера виртуальной машины
> * Просмотр виртуальной машины и оценка ее состояния

Этот учебник требует hello Azure PowerShell модуль версии 3.6 или более поздней версии. Запустите ` Get-Module -ListAvailable AzureRM` версии toofind hello. Получить tooupgrade [установите Azure PowerShell модуль](/powershell/azure/install-azurerm-ps).

## <a name="create-resource-group"></a>Создать группу ресурсов

Создание группы ресурсов с hello [New AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) команды. 

Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими. Группу ресурсов следует создавать до виртуальной машины. В этом примере имя группы ресурсов *myResourceGroupVM* создается в hello *EastUS* области. 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupVM -Location EastUS
```

Группа ресурсов Hello указывается при создании или изменении виртуальных Машин, который можно увидеть на протяжении этого учебника.

## <a name="create-virtual-machine"></a>Создание виртуальной машины

Виртуальная машина должна быть tooa подключенной виртуальной сети. Взаимодействовать с виртуальной машиной hello, используя общедоступный IP-адрес через сетевой адаптер.

### <a name="create-virtual-network"></a>Создание виртуальной сети

Создайте подсеть с помощью командлета [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24
```

Создайте виртуальную сеть с помощью командлета [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 ` 
  -Subnet $subnetConfig
```
### <a name="create-public-ip-address"></a>Создание общедоступного IP-адреса

Создайте общедоступный IP-адрес с помощью командлета [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):

```powershell
$pip = New-AzureRmPublicIpAddress ` 
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS ` 
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

### <a name="create-network-interface-card"></a>Создание сетевого адаптера

Создайте сетевой адаптер с помощью командлета [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):

```powershell
$nic = New-AzureRmNetworkInterface `
  -ResourceGroupName myResourceGroupVM  `
  -Location EastUS `
  -Name myNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

### <a name="create-network-security-group"></a>Создание группы безопасности сети

[Группа безопасности сети](../../virtual-network/virtual-networks-nsg.md) Azure управляет входящим и исходящим трафиком одной или нескольких виртуальных машин. Правила группы безопасности сети разрешают или запрещают передачу сетевого трафика на определенный порт или диапазон портов. Эти правила также могут включать префикс адреса источника, чтобы на виртуальную машину передавался только трафик от определенного источника. tooaccess hello IIS веб-сервер, установке, необходимо добавить правило для входящего трафика NSG.

использовать toocreate входящее правило NSG [AzureRmNetworkSecurityRuleConfig добавить](/powershell/module/azurerm.network/add-azurermnetworksecurityruleconfig). Hello следующий пример создает NSG правило с именем *myNSGRule* , открывает порт *3389* для hello виртуальной машины:

```powershell
$nsgRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNSGRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1000 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 3389 `
  -Access Allow
```

Создание с помощью NSG hello *myNSGRule* с [New AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupVM `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRule
```

Добавить подсеть toohello NSG hello в hello виртуальной сети с [AzureRmVirtualNetworkSubnetConfig набор](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):

```powershell
Set-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -VirtualNetwork $vnet `
    -NetworkSecurityGroup $nsg `
    -AddressPrefix 192.168.1.0/24
```

Обновление hello виртуальную сеть с [AzureRmVirtualNetwork набор](/powershell/module/azurerm.network/set-azurermvirtualnetwork):

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-machine"></a>Создание виртуальной машины

При создании виртуальной машины доступно несколько вариантов, таких как образ операционной системы, определение размера диска и учетные данные администратора. В этом примере создается виртуальная машина с именем *myVM* выполнение hello последнюю версию Windows Server 2016 Datacenter.

Укажите имя пользователя hello и пароль для учетной записи администратора hello на виртуальной машине hello [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Создание начальной настройки hello для hello виртуальной машины с [New AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig):

```powershell
$vm = New-AzureRmVMConfig -VMName myVM -VMSize Standard_D1
```

Добавить конфигурацию виртуальной машины toohello сведения операционной системы hello с [AzureRmVMOperatingSystem набор](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem):

```powershell
$vm = Set-AzureRmVMOperatingSystem `
    -VM $vm `
    -Windows `
    -ComputerName myVM `
    -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

Добавить конфигурацию виртуальной машины toohello сведения изображения hello с [AzureRmVMSourceImage набор](/powershell/module/azurerm.compute/set-azurermvmsourceimage):

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
```

Добавить hello операционной системы диска параметры toohello конфигурация виртуальной машины с [AzureRmVMOSDisk набор](/powershell/module/azurerm.compute/set-azurermvmosdisk):

```powershell
$vm = Set-AzureRmVMOSDisk `
    -VM $vm `
    -Name myOsDisk `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
```

Добавить hello сетевого интерфейса, созданный ранее toohello конфигурация виртуальной машины с [AzureRmVMNetworkInterface добавить](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

Создание виртуальной машины hello с [New AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroupVM -Location EastUS -VM $vm
```

## <a name="connect-toovm"></a>Подключение tooVM

После завершения развертывания hello создания удаленного рабочего стола с виртуальной машиной hello.

Выполните следующие команды tooreturn hello общедоступный IP-адрес виртуальной машины hello hello. Запишите этот IP-адрес для подключения tooit с вашего браузера tootest соединения через сеть на следующем шаге.

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroupVM  | Select IpAddress
```

Используйте hello следующая команда toocreate сеанс удаленного рабочего стола с виртуальной машиной hello. Замените hello hello IP-адрес *publicIPAddress* вашей виртуальной машины. При появлении запроса введите hello учетные данные, используемые при создании виртуальной машины hello.

```powershell
mstsc /v:<publicIpAddress>
```

## <a name="understand-vm-images"></a>Описание образов виртуальных машин

Hello Azure marketplace включает много образы виртуальных машин, которые можно использовать toocreate новой виртуальной машины. В предыдущих шагах hello виртуальная машина создана с помощью образа Windows Server 2016 — Datacenter hello. На этом этапе модуль PowerShell hello — магазин hello toosearch используется для других образов Windows, которые можно также в качестве базы для новых виртуальных машин. Этот процесс состоит из поиск hello издателя, предложения и имя образа hello (конфигурация). 

Используйте hello [Get AzureRmVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher) tooreturn команда список издателей изображения.  

```powersehll
Get-AzureRmVMImagePublisher -Location "EastUS"
```

Используйте hello [Get AzureRmVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer) tooreturn список предложений изображения. С помощью этой команды hello вернуть список будет отфильтрован по указанным издателем hello. 

```powershell
Get-AzureRmVMImageOffer -Location "EastUS" -PublisherName "MicrosoftWindowsServer"
```

```powershell
Offer             PublisherName          Location
-----             -------------          -------- 
Windows-HUB       MicrosoftWindowsServer EastUS 
WindowsServer     MicrosoftWindowsServer EastUS   
WindowsServer-HUB MicrosoftWindowsServer EastUS   
```

Hello [Get AzureRmVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) команды используется затем для фильтрации tooreturn имя издателя и предложение hello списка имен образов.

```powershell
Get-AzureRmVMImageSku -Location "EastUS" -PublisherName "MicrosoftWindowsServer" -Offer "WindowsServer"
```

```powershell
Skus                            Offer         PublisherName          Location
----                            -----         -------------          --------
2008-R2-SP1                     WindowsServer MicrosoftWindowsServer EastUS  
2008-R2-SP1-BYOL                WindowsServer MicrosoftWindowsServer EastUS  
2012-Datacenter                 WindowsServer MicrosoftWindowsServer EastUS  
2012-Datacenter-BYOL            WindowsServer MicrosoftWindowsServer EastUS  
2012-R2-Datacenter              WindowsServer MicrosoftWindowsServer EastUS  
2012-R2-Datacenter-BYOL         WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter                 WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter-Server-Core     WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter-with-Containers WindowsServer MicrosoftWindowsServer EastUS  
2016-Nano-Server                WindowsServer MicrosoftWindowsServer EastUS
```

Эти сведения можно использовать toodeploy виртуальной Машины с помощью специального образа. В этом примере задает имя образа hello hello объекта виртуальной Машины. См. в этом учебнике шаги завершения развертывания toohello предыдущих примерах.

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter-with-Containers `
    -Version latest
```

## <a name="understand-vm-sizes"></a>Описание размеров виртуальных машин

Размер виртуальной машины определяет hello объем вычислительных ресурсов, таких как ЦП, графического Процессора и памяти, сделанные доступными toohello виртуальной машины. Виртуальные машины должны toobe создана с размером соответствующего для hello ожидать рабочей нагрузки. При увеличении рабочей нагрузки размер существующей виртуальной машины может быть изменен.

### <a name="vm-sizes"></a>Размеры виртуальных машин

в следующей таблице Hello относит размеры вариантов использования.  

| Тип                     | Размеры           |    Описание       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| Универсальные         |DSv2, Dv2, DS, D, Av2, A0–A7| Сбалансированное соотношение ресурсов ЦП и памяти. Идеально подходит для разработки и тестирования и малого toomedium приложениям и данным решения.  |
| Оптимизированные для вычислений      | Fs, F             | Высокое соотношение ресурсов ЦП и памяти. Подходят для приложений со средним объемом трафика, сетевых устройств и пакетных процессов.        |
| Оптимизированные для памяти       | GS, G, DSv2, DS, Dv2, D   | Высокое соотношение ресурсов памяти и числа ядер. Идеально подходит для реляционных баз данных, кэши средний toolarge и аналитики в памяти.                 |
| Оптимизированные для хранилища       | Ls                | Высокая пропускная способность дисков и количество операций ввода-вывода. Идеальный вариант для работы с большими данными, а также с базами данных SQL и NoSQL.                                                         |
| Графический процессор           | NV, NC            | Специализированные виртуальные машины, предназначенные для ресурсоемкой отрисовки изображений и редактирования видео.       |
| Высокопроизводительные | H, A8–A11          | Виртуальные машины с самыми мощными ЦП, для которых можно настроить сетевые интерфейсы с высокой пропускной способностью (RDMA). 


### <a name="find-available-vm-sizes"></a>Поиск всех доступных размеров виртуальных машин

toosee список виртуальных Машин размеров, доступных в определенном регионе, используйте hello [Get AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) команды.

```powershell
Get-AzureRmVMSize -Location EastUS
```

## <a name="resize-a-vm"></a>Изменение размера виртуальной машины

После развертывания виртуальной Машины, ее можно изменять размер tooincrease или уменьшить выделения ресурсов.

Перед изменением размера виртуальной Машины, проверьте hello желаемый размер доступен на hello текущего кластера виртуальных Машин. Hello [Get AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) команда возвращает список размеров. 

```powershell
Get-AzureRmVMSize -ResourceGroupName myResourceGroupVM -VMName myVM 
```

При желании hello, что он доступен hello виртуальной Машины могут быть изменены из состояния включении, однако он не будет перезагружен во время операции hello.

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM 
$vm.HardwareProfile.VmSize = "Standard_D4"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
```

Если hello желаемый размер находится не на hello текущего кластера, hello ВМ потребностей, может произойти toobe освобождена до hello операцию изменения размера. Обратите внимание, что при hello виртуальная машина не будет включено обратно, удаляются все данные на диске временный hello и изменяйте hello общедоступный IP-адрес, если используется статический IP-адрес. 

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM
$vm.HardwareProfile.VmSize = "Standard_F4s"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
Start-AzureRmVM -ResourceGroupName myResourceGroupVM  -Name $vm.name
```

## <a name="vm-power-states"></a>Состояния включенной виртуальной машины

Включенная виртуальная машина Azure может находиться в одном из многих состояний. Это состояние представляет текущее состояние hello hello виртуальной Машины с точки зрения hello hello низкоуровневой оболочки. 

### <a name="power-states"></a>Состояния включения

| Состояние включения | Описание
|----|----|
| Starting | Указывает, что hello виртуальная машина запускается. |
| Выполнение | Указывает, что выполняется hello виртуальной машины. |
| Остановка | Указывает, что выполняется остановка виртуальной машины hello. | 
| Остановлено | Указывает, что этот hello виртуальная машина остановлена. Обратите внимание, что виртуальные машины в состоянии остановки hello взиматься плата за вычислительные операции.  |
| Отмена выделения | Указывает, что выполняется освобождение hello виртуальной машины. |
| Освобождено | Указывает, что для этой виртуальной машине hello полностью удалены из hello низкоуровневой оболочки, но по-прежнему доступны в плоскости управления hello. Виртуальные машины в состоянии освобождена hello не взимается вычислений. |
| - | Указывает на неизвестное состояние электропитания hello hello виртуальной машины. |

### <a name="find-power-state"></a>Поиск состояние включения

состояние конкретной виртуальной Машины, используйте hello hello tooretrieve [Get AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) команды. Быть toospecify убедиться, что допустимое имя для виртуальной машины и группе ресурсов. 

```powershell
Get-AzureRmVM `
    -ResourceGroupName myResourceGroup `
    -Name myVM `
    -Status | Select @{n="Status"; e={$_.Statuses[1].Code}}
```

Выходные данные:

```powershell
Status
------
PowerState/running
```

## <a name="management-tasks"></a>Задачи управления

Во время жизненного цикла hello виртуальной машины может понадобиться toorun задачи управления, такие как запуск, остановка или удаление виртуальной машины. Кроме того вы можете toocreate сценариев tooautomate повторяющихся или сложных задач. С помощью Azure PowerShell, многие часто встречающиеся задачи управления можно запускать из командной строки hello, или в скриптах.

### <a name="stop-virtual-machine"></a>Прекращение работы виртуальной машины

Остановите и освободите виртуальную машину с помощью командлета [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm):

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
```

Tookeep hello виртуальной машины в подготовленное состояние, используйте параметр - StayProvisioned hello.

### <a name="start-virtual-machine"></a>Запуск виртуальной машины

```powershell
Start-AzureRmVM -ResourceGroupName myResourceGroupVM -Name myVM
```

### <a name="delete-resource-group"></a>Удалить группу ресурсов

При удалении группы ресурсов будут также удалены все ресурсы, содержащиеся в ней.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroupVM -Force
```

## <a name="next-steps"></a>Дальнейшие действия

В рамках этого руководства вы изучили основы создания виртуальной машины и управления ею. Вы узнали, как выполнять следующие задачи:

> [!div class="checklist"]
> * Создать и присоединить tooa виртуальной Машины
> * Выбор и использование образов виртуальных машин
> * Просмотр и использование определенных размеров виртуальных машин
> * Изменение размера виртуальной машины
> * Просмотр виртуальной машины и оценка ее состояния

Переместить следующий учебник toolearn toohello о дисках виртуальных Машин.  

> [!div class="nextstepaction"]
> [Управление дисками Azure с помощью Azure CLI](./tutorial-manage-data-disk.md)
