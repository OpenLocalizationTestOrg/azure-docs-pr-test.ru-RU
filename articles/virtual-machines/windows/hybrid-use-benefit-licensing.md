---
title: "Преимущество использования гибридной для окна сервера и клиента Windows aaaAzure | Документы Microsoft"
description: "Узнайте, как toomaximize toobring преимущества вашей Windows Software Assurance локальной лицензии tooAzure"
services: virtual-machines-windows
documentationcenter: 
author: kmouss
manager: timlt
editor: 
ms.assetid: 332583b6-15a3-4efb-80c3-9082587828b0
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 5/26/2017
ms.author: xujing
ms.openlocfilehash: f24487320a60132aaf766a31f3e6f3726d4a3bd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-hybrid-use-benefit-for-windows-server-and-windows-client"></a>Преимущества гибридного использования Azure для сервера Windows Server и клиента Windows.
Для клиентов с программой Software Assurance, преимущество использования гибридной Azure позволяет toouse вашей лицензии Windows Server и клиента Windows в локальной среде и выполнения виртуальных машинах в Azure за небольшую стоимость. Преимущество гибридного использования Azure для Windows Server распространяется на Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 и Windows Server 2016. Преимущество гибридного использования Azure для клиента Windows распространяется на Windows 10. Дополнительные сведения см. в разделе hello [преимущество использования гибридной Azure лицензирования страницы](https://azure.microsoft.com/pricing/hybrid-use-benefit/).

>[!IMPORTANT]
>Azure гибридного использовать преимущества для клиентов Windows сейчас в предварительной версии, с помощью образа Windows 10 hello в hello Azure Marketplace. Они доступны только клиентам уровня "Корпоративный", использующим Windows 10 Корпоративная E3 или Windows 10 Корпоративная E5 для каждого пользователя либо Windows VDA для каждого пользователя (лицензии на подписку пользователя или дополнительные лицензии на подписку пользователя) ("соответствующие лицензии").
>
>

## <a name="ways-toouse-azure-hybrid-use-benefit"></a>Способы toouse преимущество использования гибридной Azure
Существует несколько способов toodeploy виртуальные машины Windows с hello преимущество использования гибридной Azure:

1. Можно развернуть виртуальные машины на основе [определенных образов из Marketplace](#deploy-a-vm-using-the-azure-marketplace), для которых предварительно настроены преимущества гибридного использования Azure: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 и Windows Server 2008 с пакетом обновления 1 (SP1).
2. Вы можете [передать настраиваемую виртуальную машину](#upload-a-windows-vhd) и [развернуть ее с помощью шаблона Resource Manager](#deploy-a-vm-via-resource-manager) или [Azure PowerShell](#detailed-powershell-deployment-walkthrough).

## <a name="deploy-a-vm-using-hello-azure-marketplace"></a>Развертывание виртуальной Машины с помощью hello Azure Marketplace
Следующие изображения доступны в hello предварительно настроенный преимущество использования гибридной Azure Marketplace: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 и Windows Server 2008SP1. Эти образы можно развертывать непосредственно из hello портал Azure, шаблоны диспетчера ресурсов и Azure PowerShell.

Вы можете развернуть эти изображения непосредственно из hello портал Azure. Для использования в шаблонах диспетчера ресурсов, а также с помощью Azure PowerShell просмотрите список образов hello следующим образом:

Для Windows Server:
```powershell
Get-AzureRmVMImagesku -Location westus -PublisherName MicrosoftWindowsServer -Offer WindowsServer
```
- 2016-Datacenter версии 2016.127.20170406 или выше;

- 2012-R2-Datacenter версии 4.127.20170406 или выше;

- 2012-Datacenter версии 3.127.20170406 или выше;

- 2008-R2-SP1 версии 2.127.20170406 или выше.

Для клиента Windows:
```powershell
Get-AzureRMVMImageSku -Location "West US" -Publisher "MicrosoftWindowsServer" `
    -Offer "Windows-HUB"
```

## <a name="upload-a-windows-server-vhd"></a>Отправка виртуального жесткого диска Windows Server
toodeploy виртуальной Машины Windows Server в Azure, необходимо сначала toocreate VHD, который содержит базовые сборки Windows. Этого виртуального жесткого диска необходимо соответствующим образом подготовить через Sysprep, прежде чем передать его tooAzure. Вы можете [Подробнее о требованиях к VHD hello и процесс выполнения Sysprep](upload-generalized-managed.md) и [поддержка Sysprep для ролей сервера](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles). Резервное копирование hello виртуальной Машины перед запуском Sysprep. 

Убедитесь, что у вас есть [последнюю версию Azure PowerShell установлена и настроена hello](/powershell/azure/overview). После подготовки вашего виртуального жесткого диска, отправьте hello учетной записи для хранилища Azure VHD tooyour с помощью hello `Add-AzureRmVhd` командлет следующим образом:

```powershell
Add-AzureRmVhd -ResourceGroupName "myResourceGroup" -LocalFilePath "C:\Path\To\myvhd.vhd" `
    -Destination "https://mystorageaccount.blob.core.windows.net/vhds/myvhd.vhd"
```

> [!NOTE]
> Microsoft SQL Server, SharePoint Server и Dynamics могут использовать также ваше лицензирование Software Assurance. По-прежнему требуется образ Windows Server tooprepare hello, установка компонентов приложения и соответствующим образом обеспечивая ключи многократной установки, а затем Отправка tooAzure образ диска hello. Просмотрите hello соответствующей документации для выполнения команды Sysprep с приложением, такие как [рекомендации по установке SQL Server с помощью Sysprep](https://msdn.microsoft.com/library/ee210754.aspx) или [создать SharePoint Server 2016 эталонный образ (Sysprep)](http://social.technet.microsoft.com/wiki/contents/articles/33789.build-a-sharepoint-server-2016-reference-image-sysprep.aspx).
>
>

Можно также получить дополнительные сведения о [передачи tooAzure процессе hello виртуального жесткого диска](upload-generalized-managed.md#upload-the-vhd-to-your-storage-account)


## <a name="deploy-a-vm-via-resource-manager-template"></a>Развертывание виртуальной машины с помощью шаблона Resource Manager
В шаблонах Resource Manager можно указывать дополнительный параметр для `licenseType`. Дополнительные сведения см. в статье [Создание шаблонов диспетчера ресурсов Azure](../../resource-group-authoring-templates.md). После tooAzure вашей отправки виртуального жесткого диска, измените вы тип лицензии hello tooinclude шаблона диспетчера ресурсов как часть hello вычислений поставщика и развертывания шаблона в обычном режиме.

Для Windows Server:
```json
"properties": {  
   "licenseType": "Windows_Server",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

Для клиента Windows toouse с помощью образа Marketplace Azure только:
```json
"properties": {  
   "licenseType": "Windows_Client",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

## <a name="deploy-a-vm-via-powershell-quickstart"></a>Краткое руководство по развертыванию виртуальной машины с помощью PowerShell
При развертывании виртуальной машины Windows Server с помощью PowerShell доступен дополнительный параметр для `-LicenseType`. После получения вашего tooAzure отправки виртуального жесткого диска Создание виртуальной Машины с помощью `New-AzureRmVM` и укажите тип, лицензировании hello следующим образом:

Для Windows Server:
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Server"
```

Для клиента Windows toouse с помощью образа Marketplace Azure только:
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Client"
```

Вы можете [чтение более подробное Пошаговое руководство по развертыванию виртуальной Машины в Azure с помощью PowerShell](hybrid-use-benefit-licensing.md#detailed-powershell-deployment-walkthrough) ниже, или для чтения на более описательное руководство также hello различных этапов[создания виртуальной Машины Windows с помощью диспетчера ресурсов и PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


## <a name="verify-your-vm-is-utilizing-hello-licensing-benefit"></a>Убедитесь, что ВМ использует преимущества лицензирования hello
После развертывания ВМ через hello PowerShell или метода развертывания диспетчера ресурсов проверить тип лицензии hello с `Get-AzureRmVM` следующим образом:

```powershell
Get-AzureRmVM -ResourceGroup "myResourceGroup" -Name "myVM"
```

Hello вывода будет примерно toohello следующий пример для Windows Server:

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              : Windows_Server
```

Этот выход, отличается от развертывания следующих виртуальных Машин без лицензирования преимущество использования гибридной Azure, такие как ВМ, развернутой прямо из коллекции Azure hello приветствия:

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              :
```

## <a name="detailed-powershell-deployment-walkthrough"></a>Подробное пошаговое руководство по развертыванию с помощью PowerShell
Hello следующие подробные Показать шаги PowerShell полное развертывание виртуальной машины. Дополнительный контекст можно прочитать как toohello фактическое командлеты и различные компоненты в [создания виртуальной Машины Windows с помощью диспетчера ресурсов и PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). В этом разделе описано, как создать группу ресурсов, учетную запись хранения, виртуальную сеть, а также, как определить и создать виртуальную машину.

Сначала выполните следующую команду, чтобы получить учетные данные, задать расположение и имя группы ресурсов.

```powershell
$cred = Get-Credential
$location = "West US"
$resourceGroupName = "myResourceGroup"
```

Создайте общедоступный IP-адрес.

```powershell
$publicIPName = "myPublicIP"
$publicIP = New-AzureRmPublicIpAddress -Name $publicIPName -ResourceGroupName $resourceGroupName `
    -Location $location -AllocationMethod "Dynamic"
```

Определите подсеть, сетевой адаптер и виртуальную сеть.

```powershell
$subnetName = "mySubnet"
$nicName = "myNIC"
$vnetName = "myVnet"
$subnetconfig = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/8
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName -Location $location `
    -AddressPrefix 10.0.0.0/8 -Subnet $subnetconfig
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $resourceGroupName -Location $location `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $publicIP.Id
```

Присвойте имя виртуальной машине и настройте ее конфигурацию.

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A1"
```

Определите операционную систему.

```powershell
$computerName = "myVM"
$vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

Добавьте к toohello сетевого Адаптера виртуальной Машины:

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

Определите toouse учетной записи хранилища hello:

```powershell
$storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -AccountName mystorageaccount
```

Присоединение и отправка виртуального жесткого диска, подходящим образом подготовлена, tooyour виртуальной Машины для использования

```powershell
$osDiskName = "licensing.vhd"
$osDiskUri = '{0}vhds/{1}{2}.vhd' -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/vhd/myvhd.vhd"
$vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption FromImage `
    -SourceImageUri $urlOfUploadedImageVhd -Windows
```

Наконец создайте ВМ и определите hello лицензирования тип tooutilize преимущество использования гибридной Azure:

Для Windows Server:
```powershell
New-AzureRmVM -ResourceGroupName $resourceGroupName -Location $location -VM $vm -LicenseType "Windows_Server"
```

## <a name="deploy-a-virtual-machine-scale-set-via-resource-manager-template"></a>Развертывание масштабируемого набора виртуальных машин с помощью шаблона Resource Manager
В шаблонах Resource Manager для масштабируемого набора виртуальных машин можно указывать дополнительный параметр для `licenseType`. Дополнительные сведения см. в статье [Создание шаблонов диспетчера ресурсов Azure](../../resource-group-authoring-templates.md). Свойство licenseType hello tooinclude шаблона диспетчера ресурсов редактировать как часть набора масштабирования hello virtualMachineProfile и развертывания шаблона обычным образом — см. в примере ниже с помощью образа Windows Server 2016:


```json
"virtualMachineProfile": {
    "storageProfile": {
        "osDisk": {
            "createOption": "FromImage"
        },
        "imageReference": {
            "publisher": "MicrosoftWindowsServer",
            "offer": "WindowsServer",
            "sku": "2016-Datacenter",
            "version": "latest"
        }
    },
    "licenseType": "Windows_Server",
    "osProfile": {
            "computerNamePrefix": "[parameters('vmssName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
    }
```

> [!NOTE]
> Поддержка развертывания масштабируемого набора виртуальных машин с преимуществами AHUB с использованием PowerShell и других средств SDK будет реализована в ближайшее время.
>

## <a name="next-steps"></a>Дальнейшие действия
Узнайте больше о [льготе на гибридное использование Microsoft Azure](https://azure.microsoft.com/pricing/hybrid-use-benefit/).

Узнайте больше об [использовании шаблонов Resource Manager](../../azure-resource-manager/resource-group-overview.md).

Дополнительные сведения о [преимущество использования гибридной Azure и Azure Site Recovery сделать перенос приложений tooAzure даже более экономически](https://azure.microsoft.com/blog/hybrid-use-benefit-migration-with-asr/).
