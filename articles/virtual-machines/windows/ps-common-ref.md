---
title: "aaaCommon PowerShell команды для виртуальных машин Azure | Документы Microsoft"
description: "Общие tooget команд PowerShell был начат, создание и управление ими в Azure виртуальные машины Windows."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ba3839a2-f3d5-4e19-a5de-95bfb1c0e61e
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: 3de9bd4d20259ced2c0aa8ef7a3f7d9520a071d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="common-powershell-commands-for-creating-and-managing-azure-virtual-machines"></a>Общие команды PowerShell для создания виртуальных машин Azure и управления ими

В этой статье рассматриваются некоторые приветствия команд Azure PowerShell можно использовать toocreate и управление виртуальными машинами в вашей подписке Azure.  Для получения более подробной справки о конкретных параметрах командной строки можно использовать *команду* **Get-Help**.

В разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) сведения об установке hello последнюю версию Azure PowerShell, выбрав подписку и вход в учетную запись tooyour.

Эти переменные могут быть полезными для вас, если работает несколько команд hello в этой статье:

- $location - расположение hello hello виртуальной машины. Можно использовать [Get AzureRmLocation](https://docs.microsoft.com/powershell/module/azurerm.resources/get-azurermlocation) toofind [географический регион](https://azure.microsoft.com/regions/) , которые работают для вас.
- $myResourceGroup - hello имя группы ресурсов hello, содержащей виртуальную машину hello.
- $myVM - имя hello hello виртуальной машины.

## <a name="create-a-vm"></a>Создание виртуальной машины

| Задача | Get-Help |
| ---- | ------- |
| Создание конфигурации виртуальной машины |$vm = [New-AzureRmVMConfig](https://docs.microsoft.com/powershell/module/azurerm.compute/new-azurermvmconfig) -VMName $myVM -VMSize "Standard_D1_v1"<BR></BR><BR></BR>Конфигурация виртуальной Машины Hello — используемые параметры toodefine или обновления для hello виртуальной Машины. Конфигурация Hello инициализируется с именем hello hello виртуальной Машины и ее [размер](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). |
| Добавление параметров конфигурации |$vm = [Set-AzureRmVMOperatingSystem](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) -VM $vm -Windows -ComputerName $myVM -Credential $cred -ProvisionVMAgent -EnableAutoUpdate<BR></BR><BR></BR>Параметры операционной системы, в том числе [учетные данные](https://technet.microsoft.com/library/hh849815.aspx) добавляются toohello объект конфигурации, созданный ранее с помощью New-AzureRmVMConfig. |
| Добавление сетевого интерфейса |$vm = [Add-AzureRmVMNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.5.0/Add-AzureRmVMNetworkInterface) -VM $vm -Id $nic.Id<BR></BR><BR></BR>Виртуальный компьютер должен иметь [сетевой интерфейс](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toocommunicate в виртуальной сети. Можно также использовать [Get AzureRmNetworkInterface](https://docs.microsoft.com/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) tooretrieve существующий объект сетевого интерфейса. |
| Указание образа платформы |$vm = [Set-AzureRmVMSourceImage](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmsourceimage) -VM $vm -PublisherName "имя_издателя" -Offer "предложение_издателя" -Skus "SKU_продукта" -Version "последняя_версия"<BR></BR><BR></BR>[Информации об изображении](cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) добавляется toohello объект конфигурации, созданный ранее с помощью New-AzureRmVMConfig. Hello объекта, возвращаемого из этой команды используется только при установке toouse диска hello операционной системы образа платформы. |
| Задать toouse диска операционной системы образа платформы |$vm = [Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmosdisk) -VM $vm -Name "myOSDisk" -VhdUri "http://mystore1.blob.core.windows.net/vhds/myOSDisk.vhd" -CreateOption FromImage<BR></BR><BR></BR>Имя Hello hello диска операционной системы и ее расположение в [хранения](../../storage/common/storage-powershell-guide-full.md) добавляется toohello объект конфигурации, созданный ранее. |
| Задать обобщенный образ toouse диска операционной системы |$vm = Set-AzureRmVMOSDisk -VM $vm -Name "myOSDisk" -SourceImageUri "https://mystore1.blob.core.windows.net/system/Microsoft.Compute/Images/myimages/myprefix-osDisk.{guid}.vhd" -VhdUri "https://mystore1.blob.core.windows.net/vhds/disk_name.vhd" -CreateOption FromImage -Windows<BR></BR><BR></BR>Имя Hello hello диска операционной системы, hello расположение исходного образа hello и расположение на диске hello в [хранения](../../storage/common/storage-powershell-guide-full.md) добавляется объект toohello конфигурации. |
| Установить специализированный образ toouse диска операционной системы |$vm = Set-AzureRmVMOSDisk -VM $vm -Name "myOSDisk" -VhdUri "http://mystore1.blob.core.windows.net/vhds/" -CreateOption Attach -Windows |
| Создание виртуальной машины |[New-AzureRmVM]() -ResourceGroupName $myResourceGroup -Location $location -VM $vm<BR></BR><BR></BR>Все ресурсы создаются в [группе ресурсов](../../azure-resource-manager/powershell-azure-resource-manager.md). Прежде чем выполнить эту команду, выполните командлеты New-AzureRmVMConfig, Set-AzureRmVMOperatingSystem, Set-AzureRmVMSourceImage, Add-AzureRmVMNetworkInterface и Set-AzureRmVMOSDisk. |

## <a name="get-information-about-vms"></a>Получение информации о виртуальных машинах

| Задача | Команда |
| ---- | ------- |
| Вывод списка виртуальных машин в подписке |[Get-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvm) |
| Вывод списка виртуальных машин в группе ресурсов |Get-AzureRmVM -ResourceGroupName $myResourceGroup<BR></BR><BR></BR>tooget список ресурсов, групп в вашей подписке, используйте [Get AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/get-azurermresourcegroup). |
| Получение информации о виртуальной машине |Get-AzureRmVM -ResourceGroupName $myResourceGroup -Name $myVM |

## <a name="manage-vms"></a>Управление виртуальными машинами
| Задача | Команда |
| --- | --- |
| Запуск виртуальной машины |[Start-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/start-azurermvm) -ResourceGroupName $myResourceGroup -Name $myVM |
| Остановка виртуальной машины |[Stop-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/stop-azurermvm) -ResourceGroupName $myResourceGroup -Name $myVM |
| Перезапуск выполняющейся виртуальной машины |[Restart-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/restart-azurermvm) -ResourceGroupName $myResourceGroup -Name $myVM |
| Удаление виртуальной машины |[Remove-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/remove-azurermvm) -ResourceGroupName $myResourceGroup -Name $myVM |
| Подготовка виртуальной машины к использованию |[Set-AzureRmVm](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvm) -ResourceGroupName $myResourceGroup -Name $myVM -Generalized<BR></BR><BR></BR>Выполните эту команду перед выполнением командлета Save-AzureRmVMImage. |
| Запись виртуальной машины |[Save-AzureRmVMImage](https://docs.microsoft.com/powershell/module/azurerm.compute/save-azurermvmimage) -ResourceGroupName $myResourceGroup -VMName $myVM -DestinationContainerName "myImageContainer" -VHDNamePrefix "myImagePrefix" -Path "C:\filepath\filename.json"<BR></BR><BR></BR>Виртуальная машина должна быть [подготовлен, завершение работы и обобщенный](prepare-for-upload-vhd-image.md) toocreate toobe используется изображение. Прежде чем выполнить эту команду, выполните командлет Set-AzureRmVm. |
| Обновление виртуальной машины |[Update-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/update-azurermvm) -ResourceGroupName $myResourceGroup -VM $vm<BR></BR><BR></BR>Получить hello с помощью Get-AzureRmVM текущую конфигурацию виртуальной Машины, измените параметры конфигурации на hello объекта виртуальной Машины и затем выполните следующую команду. |
| Добавить tooa диска данных виртуальной Машины |[Add-AzureRmVMDataDisk](https://docs.microsoft.com/powershell/module/azurerm.compute/add-azurermvmdatadisk) -VM $vm -Name "myDataDisk" -VhdUri "https://mystore1.blob.core.windows.net/vhds/myDataDisk.vhd" -LUN # -Caching ReadWrite -DiskSizeinGB # -CreateOption Empty<BR></BR><BR></BR>Использование Get-AzureRmVM tooget hello ВМ объекта. Укажите номер LUN hello и hello размер диска hello. Выполните обновление AzureRmVM tooapply hello изменения конфигурации toohello виртуальной Машины. диск Hello добавляемой не инициализирован. |
| Удаление диска данных от виртуальной машины |[Remove-AzureRmVMDataDisk](https://docs.microsoft.com/powershell/module/azurerm.compute/remove-azurermvmdatadisk) -VM $vm -Name "myDataDisk"<BR></BR><BR></BR>Использование Get-AzureRmVM tooget hello ВМ объекта. Выполните обновление AzureRmVM tooapply hello изменения конфигурации toohello виртуальной Машины. |
| Добавьте расширение tooa виртуальной Машины |[Set-AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) -ResourceGroupName $myResourceGroup -Location $location -VMName $myVM -Name "extensionName" -Publisher "publisherName" -Type "extensionType" -TypeHandlerVersion "#.#" -Settings $Settings -ProtectedSettings $ProtectedSettings<BR></BR><BR></BR>Выполните следующую команду с hello соответствующие [сведения о конфигурации](template-description.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#extensions) для нужных tooinstall расширения hello. |
| Удаление расширения виртуальной машины |[Remove-AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/remove-azurermvmextension) -ResourceGroupName $myResourceGroup -Name "extensionName" -VMName $myVM |

## <a name="next-steps"></a>Дальнейшие действия
* В разделе hello основные шаги для создания виртуальной машины в [создания виртуальной Машины Windows с помощью диспетчера ресурсов и PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

