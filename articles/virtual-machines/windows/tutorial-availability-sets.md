---
title: "aaaAvailability задает учебника для виртуальных машин Windows в Azure | Документы Microsoft"
description: "Дополнительные сведения о hello доступности наборов для виртуальных машин Windows в Azure."
documentationcenter: 
services: virtual-machines-windows
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
ms.date: 05/08/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 853775c5f126dd815c1933f9d71d2274a75ea661
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-availability-sets"></a>Каким образом задает toouse доступности

В этом учебнике вы узнаете, как tooincrease hello доступность и надежность решений для виртуальной машины в Azure, используя возможность вызывать группы доступности. Группы доступности убедитесь, что hello, развертываемым в Azure виртуальные машины распределены по нескольким кластерам изолированное оборудовании. Это гарантирует, что если происходит сбой оборудования или программного обеспечения в Azure, будут затронуты только подмножество виртуальных машин и что всего решения будет оставаться доступными и функциональными с точки зрения hello ваших клиентов, используя его. 

Из этого руководства вы узнаете, как выполнять такие задачи:

> [!div class="checklist"]
> * "Создать группу доступности"
> * Создание виртуальной машины в группе доступности
> * Проверка доступных размеров виртуальных машин

Этот учебник требует hello Azure PowerShell модуль версии 3.6 или более поздней версии. Запустите ` Get-Module -ListAvailable AzureRM` версии toofind hello. Получить tooupgrade [установите Azure PowerShell модуль](/powershell/azure/install-azurerm-ps).

## <a name="availability-set-overview"></a>Обзор групп доступности

Группа доступности — возможность логическое группирование, который можно использовать в Azure tooensure, изолированы друг от друга ресурсы hello виртуальных Машин, размещаемых в ней при развертывании в центре обработки данных Azure. Azure гарантирует, что hello поместить в группу доступности, запустите несколько физических серверов, виртуальных машин, вычислений стойки, устройства хранения и сетевых коммутаторов. Это гарантирует, что в событии hello оборудования или программного обеспечения Azure сбоя, будут затронуты только подмножество виртуальных машин и общую приложения будет работать и продолжить toobe tooyour доступны клиентам. С помощью групп доступности, tooleverage основных возможностей можно создать toobuild надежного облачных решений.

Рассмотрим стандартное решение на основе виртуальной машины, в котором может находиться 4 внешних веб-сервера и использоваться 2 внутренние виртуальные машины, содержащие базу данных. С помощью Azure необходимо два набора доступности toodefine перед развертыванием виртуальных машин: группа доступности одного уровня «web» hello и один набор доступности для уровня «database» hello. При создании новой виртуальной Машины, можно указать hello доступности виртуальной машины az toohello параметр «Создать», а Azure автоматически гарантирует, что hello виртуальных машин, создаваемых внутри hello доступных набор изолированы по нескольким ресурсам физического оборудования. Это означает, что если hello физическое оборудование, на котором один из веб-сервер или ВМ сервера базы данных выполняется на проблемы, вы знаете, hello другие экземпляры веб-сервера и базы данных виртуальных машин сможет продолжить работу нормально, так как они находятся на другое оборудование.

При необходимости toodeploy надежные решения на основе виртуальной Машины в Azure, следует всегда использовать группы доступности.

## <a name="create-an-availability-set"></a>"Создать группу доступности"

Создать группу доступности можно с помощью командлета [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset). В этом примере задается количество доменах обновления и отказоустойчивости на обоих hello *2* для обеспечения доступности hello набор *myAvailabilitySet* в hello *myResourceGroupAvailability*группы ресурсов.

Создайте группу ресурсов.

```powershell
New-AzureRmResourceGroup -Name myResourceGroupAvailability -Location EastUS
```


```powershell
New-AzureRmAvailabilitySet `
   -Location EastUS `
   -Name myAvailabilitySet `
   -ResourceGroupName myResourceGroupAvailability `
   -Managed `
   -PlatformFaultDomainCount 2 `
   -PlatformUpdateDomainCount 2
```

## <a name="create-vms-inside-an-availability-set"></a>Создание виртуальных машин в группе доступности

Виртуальные машины должны toobe создается в том, что правильно распределены по оборудованию hello toomake набор доступности hello. Не удается добавить группу существующей виртуальной Машины tooan доступности после его создания. 

оборудование Hello в расположении делится на toomultiple домены обновления и домены отказоустойчивости. **Домен обновления** — это группа виртуальных машин и физического оборудования, можно перезагрузить в hello то же время. Виртуальные машины в hello же **домен сбоя** совместно используют общее хранилище, а также общие выключателем источника и сети. 

При создании виртуальной Машины с помощью конфигурации с помощью [New AzureRMVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) укажите hello доступности с помощью hello `-AvailabilitySetId` параметр toospecify hello идентификатор набора доступности hello.

Создать 2 виртуальные машины с [New AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) в группе доступности hello.

```powershell
$availabilitySet = Get-AzureRmAvailabilitySet `
    -ResourceGroupName myResourceGroupAvailability `
    -Name myAvailabilitySet

$cred = Get-Credential -Message "Enter a username and password for hello virtual machine."

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupAvailability `
    -Location EastUS `
    -Name MYvNET `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

for ($i=1; $i -le 2; $i++)
{
   $pip = New-AzureRmPublicIpAddress `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -Name "mypublicdns$(Get-Random)" `
        -AllocationMethod Static `
        -IdleTimeoutInMinutes 4

   $nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
        -Name myNetworkSecurityGroupRuleRDP$i `
        -Protocol Tcp `
        -Direction Inbound `
        -Priority 1000 `
        -SourceAddressPrefix * `
        -SourcePortRange * `
        -DestinationAddressPrefix * `
        -DestinationPortRange 3389 `
        -Access Allow

   $nsg = New-AzureRmNetworkSecurityGroup `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -Name myNetworkSecurityGroup$i `
        -SecurityRules $nsgRuleRDP

   $nic = New-AzureRmNetworkInterface `
        -Name myNic$i `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -SubnetId $vnet.Subnets[0].Id `
        -PublicIpAddressId $pip.Id `
        -NetworkSecurityGroupId $nsg.Id

   # Here is where we specify hello availability set
   $vm = New-AzureRmVMConfig `
        -VMName myVM$i `
        -VMSize Standard_D1 `
        -AvailabilitySetId $availabilitySet.Id

   $vm = Set-AzureRmVMOperatingSystem `
        -VM $vm `
        -Windows -ComputerName myVM$i `   
        -Credential $cred `
        -ProvisionVMAgent `
        -EnableAutoUpdate
   $vm = Set-AzureRmVMSourceImage `
        -VM $vm `
        -PublisherName MicrosoftWindowsServer `
        -Offer WindowsServer `
        -Skus 2016-Datacenter `
        -Version latest
   $vm = Set-AzureRmVMOSDisk `
        -VM $vm `
        -Name myOsDisk$i `
        -DiskSizeInGB 128 `
        -CreateOption FromImage `
        -Caching ReadWrite
   $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
   New-AzureRmVM `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -VM $vm
}

```

Он принимает toocreate несколько минут, а также настроить обе виртуальные машины. По завершении вы получите 2 виртуальные машины, распределенные по hello базового оборудования. 

## <a name="check-for-available-vm-sizes"></a>Знакомство с доступными размерами виртуальной машины 

Можно добавить дополнительные виртуальные машины toohello доступности более поздней версии, но необходимо tooknow какие размеры виртуальных Машин доступны на оборудовании hello. Используйте [Get AzureRMVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) toolist все доступные размеры hello на оборудовании hello кластера для группы доступности hello.

```powershell
Get-AzureRmVMSize `
   -AvailabilitySetName myAvailabilitySet `
   -ResourceGroupName myResourceGroupAvailability  
```

## <a name="next-steps"></a>Дальнейшие действия

Из этого руководства вы узнали, как выполнять такие задачи:

> [!div class="checklist"]
> * "Создать группу доступности"
> * Создание виртуальной машины в группе доступности
> * Проверка доступных размеров виртуальных машин

Переместить следующий учебник toolearn toohello о наборы масштабирования виртуальных машин.

> [!div class="nextstepaction"]
> [Создание масштабируемого набора виртуальных машин](tutorial-create-vmss.md)


