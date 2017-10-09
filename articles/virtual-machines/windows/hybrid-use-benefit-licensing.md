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
# <a name="azure-hybrid-use-benefit-for-windows-server-and-windows-client"></a><span data-ttu-id="a3977-103">Преимущества гибридного использования Azure для сервера Windows Server и клиента Windows.</span><span class="sxs-lookup"><span data-stu-id="a3977-103">Azure Hybrid Use Benefit for Windows Server and Windows Client</span></span>
<span data-ttu-id="a3977-104">Для клиентов с программой Software Assurance, преимущество использования гибридной Azure позволяет toouse вашей лицензии Windows Server и клиента Windows в локальной среде и выполнения виртуальных машинах в Azure за небольшую стоимость.</span><span class="sxs-lookup"><span data-stu-id="a3977-104">For customers with Software Assurance, Azure Hybrid Use Benefit allows you toouse your on-premises Windows Server and Windows Client licenses and run Windows virtual machines in Azure at a reduced cost.</span></span> <span data-ttu-id="a3977-105">Преимущество гибридного использования Azure для Windows Server распространяется на Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 и Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="a3977-105">Azure Hybrid Use Benefit for Windows Server includes Windows Server 2008R2, Windows Server 2012, Windows Server 2012R2, and Windows Server 2016.</span></span> <span data-ttu-id="a3977-106">Преимущество гибридного использования Azure для клиента Windows распространяется на Windows 10.</span><span class="sxs-lookup"><span data-stu-id="a3977-106">Azure Hybrid Use Benefit for Windows Client includes Windows 10.</span></span> <span data-ttu-id="a3977-107">Дополнительные сведения см. в разделе hello [преимущество использования гибридной Azure лицензирования страницы](https://azure.microsoft.com/pricing/hybrid-use-benefit/).</span><span class="sxs-lookup"><span data-stu-id="a3977-107">For more information, please see hello [Azure Hybrid Use Benefit licensing page](https://azure.microsoft.com/pricing/hybrid-use-benefit/).</span></span>

>[!IMPORTANT]
><span data-ttu-id="a3977-108">Azure гибридного использовать преимущества для клиентов Windows сейчас в предварительной версии, с помощью образа Windows 10 hello в hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="a3977-108">Azure Hybrid Use Benefits for Windows Client is currently in Preview using hello Windows 10 image in hello Azure Marketplace.</span></span> <span data-ttu-id="a3977-109">Они доступны только клиентам уровня "Корпоративный", использующим Windows 10 Корпоративная E3 или Windows 10 Корпоративная E5 для каждого пользователя либо Windows VDA для каждого пользователя (лицензии на подписку пользователя или дополнительные лицензии на подписку пользователя) ("соответствующие лицензии").</span><span class="sxs-lookup"><span data-stu-id="a3977-109">Only Enterprise customers with Windows 10 Enterprise E3/E5 per user or Windows VDA per user (User Subscription Licenses or Add-on User Subscription Licenses) (“Qualifying Licenses”) are eligible.</span></span>
>
>

## <a name="ways-toouse-azure-hybrid-use-benefit"></a><span data-ttu-id="a3977-110">Способы toouse преимущество использования гибридной Azure</span><span class="sxs-lookup"><span data-stu-id="a3977-110">Ways toouse Azure Hybrid Use Benefit</span></span>
<span data-ttu-id="a3977-111">Существует несколько способов toodeploy виртуальные машины Windows с hello преимущество использования гибридной Azure:</span><span class="sxs-lookup"><span data-stu-id="a3977-111">There are a couple of different ways toodeploy Windows VMs with hello Azure Hybrid Use Benefit:</span></span>

1. <span data-ttu-id="a3977-112">Можно развернуть виртуальные машины на основе [определенных образов из Marketplace](#deploy-a-vm-using-the-azure-marketplace), для которых предварительно настроены преимущества гибридного использования Azure: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 и Windows Server 2008 с пакетом обновления 1 (SP1).</span><span class="sxs-lookup"><span data-stu-id="a3977-112">You can deploy VMs from [specific Marketplace images](#deploy-a-vm-using-the-azure-marketplace) that are pre-configured with Azure Hybrid Use Benefit - Windows Server 2016, Windows Server 2012R2, Windows Server 2012 and Windows Server 2008SP1.</span></span>
2. <span data-ttu-id="a3977-113">Вы можете [передать настраиваемую виртуальную машину](#upload-a-windows-vhd) и [развернуть ее с помощью шаблона Resource Manager](#deploy-a-vm-via-resource-manager) или [Azure PowerShell](#detailed-powershell-deployment-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="a3977-113">You can [upload a custom VM](#upload-a-windows-vhd) and [deploy using a Resource Manager template](#deploy-a-vm-via-resource-manager) or [Azure PowerShell](#detailed-powershell-deployment-walkthrough).</span></span>

## <a name="deploy-a-vm-using-hello-azure-marketplace"></a><span data-ttu-id="a3977-114">Развертывание виртуальной Машины с помощью hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="a3977-114">Deploy a VM using hello Azure Marketplace</span></span>
<span data-ttu-id="a3977-115">Следующие изображения доступны в hello предварительно настроенный преимущество использования гибридной Azure Marketplace: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 и Windows Server 2008SP1.</span><span class="sxs-lookup"><span data-stu-id="a3977-115">Following images are available in hello Marketplace pre-configured with Azure Hybrid Use Benefit: Windows Server 2016, Windows Server 2012R2, Windows Server 2012 and Windows Server 2008SP1.</span></span> <span data-ttu-id="a3977-116">Эти образы можно развертывать непосредственно из hello портал Azure, шаблоны диспетчера ресурсов и Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a3977-116">These images can be deployed directly from hello Azure portal, Resource Manager templates, or Azure PowerShell.</span></span>

<span data-ttu-id="a3977-117">Вы можете развернуть эти изображения непосредственно из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a3977-117">You can deploy these images directly from hello Azure portal.</span></span> <span data-ttu-id="a3977-118">Для использования в шаблонах диспетчера ресурсов, а также с помощью Azure PowerShell просмотрите список образов hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a3977-118">For use in Resource Manager templates and with Azure PowerShell, view hello list of images as follows:</span></span>

<span data-ttu-id="a3977-119">Для Windows Server:</span><span class="sxs-lookup"><span data-stu-id="a3977-119">For Windows Server:</span></span>
```powershell
Get-AzureRmVMImagesku -Location westus -PublisherName MicrosoftWindowsServer -Offer WindowsServer
```
- <span data-ttu-id="a3977-120">2016-Datacenter версии 2016.127.20170406 или выше;</span><span class="sxs-lookup"><span data-stu-id="a3977-120">2016-Datacenter version 2016.127.20170406 or above</span></span>

- <span data-ttu-id="a3977-121">2012-R2-Datacenter версии 4.127.20170406 или выше;</span><span class="sxs-lookup"><span data-stu-id="a3977-121">2012-R2-Datacenter version 4.127.20170406 or above</span></span>

- <span data-ttu-id="a3977-122">2012-Datacenter версии 3.127.20170406 или выше;</span><span class="sxs-lookup"><span data-stu-id="a3977-122">2012-Datacenter version 3.127.20170406 or above</span></span>

- <span data-ttu-id="a3977-123">2008-R2-SP1 версии 2.127.20170406 или выше.</span><span class="sxs-lookup"><span data-stu-id="a3977-123">2008-R2-SP1 version 2.127.20170406 or above</span></span>

<span data-ttu-id="a3977-124">Для клиента Windows:</span><span class="sxs-lookup"><span data-stu-id="a3977-124">For Windows Client:</span></span>
```powershell
Get-AzureRMVMImageSku -Location "West US" -Publisher "MicrosoftWindowsServer" `
    -Offer "Windows-HUB"
```

## <a name="upload-a-windows-server-vhd"></a><span data-ttu-id="a3977-125">Отправка виртуального жесткого диска Windows Server</span><span class="sxs-lookup"><span data-stu-id="a3977-125">Upload a Windows Server VHD</span></span>
<span data-ttu-id="a3977-126">toodeploy виртуальной Машины Windows Server в Azure, необходимо сначала toocreate VHD, который содержит базовые сборки Windows.</span><span class="sxs-lookup"><span data-stu-id="a3977-126">toodeploy a Windows Server VM in Azure, you first need toocreate a VHD that contains your base Windows build.</span></span> <span data-ttu-id="a3977-127">Этого виртуального жесткого диска необходимо соответствующим образом подготовить через Sysprep, прежде чем передать его tooAzure.</span><span class="sxs-lookup"><span data-stu-id="a3977-127">This VHD must be appropriately prepared via Sysprep before you upload it tooAzure.</span></span> <span data-ttu-id="a3977-128">Вы можете [Подробнее о требованиях к VHD hello и процесс выполнения Sysprep](upload-generalized-managed.md) и [поддержка Sysprep для ролей сервера](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span><span class="sxs-lookup"><span data-stu-id="a3977-128">You can [read more about hello VHD requirements and Sysprep process](upload-generalized-managed.md) and [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span></span> <span data-ttu-id="a3977-129">Резервное копирование hello виртуальной Машины перед запуском Sysprep.</span><span class="sxs-lookup"><span data-stu-id="a3977-129">Back up hello VM before running Sysprep.</span></span> 

<span data-ttu-id="a3977-130">Убедитесь, что у вас есть [последнюю версию Azure PowerShell установлена и настроена hello](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a3977-130">Make sure you have [installed and configured hello latest Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="a3977-131">После подготовки вашего виртуального жесткого диска, отправьте hello учетной записи для хранилища Azure VHD tooyour с помощью hello `Add-AzureRmVhd` командлет следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a3977-131">Once you have prepared your VHD, upload hello VHD tooyour Azure Storage account using hello `Add-AzureRmVhd` cmdlet as follows:</span></span>

```powershell
Add-AzureRmVhd -ResourceGroupName "myResourceGroup" -LocalFilePath "C:\Path\To\myvhd.vhd" `
    -Destination "https://mystorageaccount.blob.core.windows.net/vhds/myvhd.vhd"
```

> [!NOTE]
> <span data-ttu-id="a3977-132">Microsoft SQL Server, SharePoint Server и Dynamics могут использовать также ваше лицензирование Software Assurance.</span><span class="sxs-lookup"><span data-stu-id="a3977-132">Microsoft SQL Server, SharePoint Server, and Dynamics can also utilize your Software Assurance licensing.</span></span> <span data-ttu-id="a3977-133">По-прежнему требуется образ Windows Server tooprepare hello, установка компонентов приложения и соответствующим образом обеспечивая ключи многократной установки, а затем Отправка tooAzure образ диска hello.</span><span class="sxs-lookup"><span data-stu-id="a3977-133">You still need tooprepare hello Windows Server image by installing your application components and providing license keys accordingly, then uploading hello disk image tooAzure.</span></span> <span data-ttu-id="a3977-134">Просмотрите hello соответствующей документации для выполнения команды Sysprep с приложением, такие как [рекомендации по установке SQL Server с помощью Sysprep](https://msdn.microsoft.com/library/ee210754.aspx) или [создать SharePoint Server 2016 эталонный образ (Sysprep)](http://social.technet.microsoft.com/wiki/contents/articles/33789.build-a-sharepoint-server-2016-reference-image-sysprep.aspx).</span><span class="sxs-lookup"><span data-stu-id="a3977-134">Review hello appropriate documentation for running Sysprep with your application, such as [Considerations for Installing SQL Server using Sysprep](https://msdn.microsoft.com/library/ee210754.aspx) or [Build a SharePoint Server 2016 Reference Image (Sysprep)](http://social.technet.microsoft.com/wiki/contents/articles/33789.build-a-sharepoint-server-2016-reference-image-sysprep.aspx).</span></span>
>
>

<span data-ttu-id="a3977-135">Можно также получить дополнительные сведения о [передачи tooAzure процессе hello виртуального жесткого диска](upload-generalized-managed.md#upload-the-vhd-to-your-storage-account)</span><span class="sxs-lookup"><span data-stu-id="a3977-135">You can also read more about [uploading hello VHD tooAzure process](upload-generalized-managed.md#upload-the-vhd-to-your-storage-account)</span></span>


## <a name="deploy-a-vm-via-resource-manager-template"></a><span data-ttu-id="a3977-136">Развертывание виртуальной машины с помощью шаблона Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a3977-136">Deploy a VM via Resource Manager Template</span></span>
<span data-ttu-id="a3977-137">В шаблонах Resource Manager можно указывать дополнительный параметр для `licenseType`.</span><span class="sxs-lookup"><span data-stu-id="a3977-137">Within your Resource Manager templates, an additional parameter for `licenseType` can be specified.</span></span> <span data-ttu-id="a3977-138">Дополнительные сведения см. в статье [Создание шаблонов диспетчера ресурсов Azure](../../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a3977-138">You can read more about [authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span> <span data-ttu-id="a3977-139">После tooAzure вашей отправки виртуального жесткого диска, измените вы тип лицензии hello tooinclude шаблона диспетчера ресурсов как часть hello вычислений поставщика и развертывания шаблона в обычном режиме.</span><span class="sxs-lookup"><span data-stu-id="a3977-139">Once you have your VHD uploaded tooAzure, edit you Resource Manager template tooinclude hello license type as part of hello compute provider and deploy your template as normal:</span></span>

<span data-ttu-id="a3977-140">Для Windows Server:</span><span class="sxs-lookup"><span data-stu-id="a3977-140">For Windows Server:</span></span>
```json
"properties": {  
   "licenseType": "Windows_Server",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

<span data-ttu-id="a3977-141">Для клиента Windows toouse с помощью образа Marketplace Azure только:</span><span class="sxs-lookup"><span data-stu-id="a3977-141">For Windows Client toouse with Azure Marketplace Image only:</span></span>
```json
"properties": {  
   "licenseType": "Windows_Client",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

## <a name="deploy-a-vm-via-powershell-quickstart"></a><span data-ttu-id="a3977-142">Краткое руководство по развертыванию виртуальной машины с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="a3977-142">Deploy a VM via PowerShell quickstart</span></span>
<span data-ttu-id="a3977-143">При развертывании виртуальной машины Windows Server с помощью PowerShell доступен дополнительный параметр для `-LicenseType`.</span><span class="sxs-lookup"><span data-stu-id="a3977-143">When deploying your Windows Server VM via PowerShell, you have an additional parameter for `-LicenseType`.</span></span> <span data-ttu-id="a3977-144">После получения вашего tooAzure отправки виртуального жесткого диска Создание виртуальной Машины с помощью `New-AzureRmVM` и укажите тип, лицензировании hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a3977-144">Once you have your VHD uploaded tooAzure, you create a VM using `New-AzureRmVM` and specify hello licensing type as follows:</span></span>

<span data-ttu-id="a3977-145">Для Windows Server:</span><span class="sxs-lookup"><span data-stu-id="a3977-145">For Windows Server:</span></span>
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Server"
```

<span data-ttu-id="a3977-146">Для клиента Windows toouse с помощью образа Marketplace Azure только:</span><span class="sxs-lookup"><span data-stu-id="a3977-146">For Windows Client toouse with Azure Marketplace Image only:</span></span>
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Client"
```

<span data-ttu-id="a3977-147">Вы можете [чтение более подробное Пошаговое руководство по развертыванию виртуальной Машины в Azure с помощью PowerShell](hybrid-use-benefit-licensing.md#detailed-powershell-deployment-walkthrough) ниже, или для чтения на более описательное руководство также hello различных этапов[создания виртуальной Машины Windows с помощью диспетчера ресурсов и PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a3977-147">You can [read a more detailed walkthrough on deploying a VM in Azure via PowerShell](hybrid-use-benefit-licensing.md#detailed-powershell-deployment-walkthrough) below, or read a more descriptive guide on hello different steps too[create a Windows VM using Resource Manager and PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


## <a name="verify-your-vm-is-utilizing-hello-licensing-benefit"></a><span data-ttu-id="a3977-148">Убедитесь, что ВМ использует преимущества лицензирования hello</span><span class="sxs-lookup"><span data-stu-id="a3977-148">Verify your VM is utilizing hello licensing benefit</span></span>
<span data-ttu-id="a3977-149">После развертывания ВМ через hello PowerShell или метода развертывания диспетчера ресурсов проверить тип лицензии hello с `Get-AzureRmVM` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a3977-149">Once you have deployed your VM through either hello PowerShell or Resource Manager deployment method, verify hello license type with `Get-AzureRmVM` as follows:</span></span>

```powershell
Get-AzureRmVM -ResourceGroup "myResourceGroup" -Name "myVM"
```

<span data-ttu-id="a3977-150">Hello вывода будет примерно toohello следующий пример для Windows Server:</span><span class="sxs-lookup"><span data-stu-id="a3977-150">hello output is similar toohello following example for Windows Server:</span></span>

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              : Windows_Server
```

<span data-ttu-id="a3977-151">Этот выход, отличается от развертывания следующих виртуальных Машин без лицензирования преимущество использования гибридной Azure, такие как ВМ, развернутой прямо из коллекции Azure hello приветствия:</span><span class="sxs-lookup"><span data-stu-id="a3977-151">This output contrasts with hello following VM deployed without Azure Hybrid Use Benefit licensing, such as a VM deployed straight from hello Azure Gallery:</span></span>

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              :
```

## <a name="detailed-powershell-deployment-walkthrough"></a><span data-ttu-id="a3977-152">Подробное пошаговое руководство по развертыванию с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="a3977-152">Detailed PowerShell deployment walkthrough</span></span>
<span data-ttu-id="a3977-153">Hello следующие подробные Показать шаги PowerShell полное развертывание виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="a3977-153">hello following detailed PowerShell steps show a full deployment of a VM.</span></span> <span data-ttu-id="a3977-154">Дополнительный контекст можно прочитать как toohello фактическое командлеты и различные компоненты в [создания виртуальной Машины Windows с помощью диспетчера ресурсов и PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a3977-154">You can read more context as toohello actual cmdlets and different components being created in [Create a Windows VM using Resource Manager and PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="a3977-155">В этом разделе описано, как создать группу ресурсов, учетную запись хранения, виртуальную сеть, а также, как определить и создать виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="a3977-155">You step through creating your resource group, storage account, and virtual networking, then define your VM and finally create your VM.</span></span>

<span data-ttu-id="a3977-156">Сначала выполните следующую команду, чтобы получить учетные данные, задать расположение и имя группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a3977-156">First, securely obtain credentials, set a location, and resource group name:</span></span>

```powershell
$cred = Get-Credential
$location = "West US"
$resourceGroupName = "myResourceGroup"
```

<span data-ttu-id="a3977-157">Создайте общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="a3977-157">Create a public IP:</span></span>

```powershell
$publicIPName = "myPublicIP"
$publicIP = New-AzureRmPublicIpAddress -Name $publicIPName -ResourceGroupName $resourceGroupName `
    -Location $location -AllocationMethod "Dynamic"
```

<span data-ttu-id="a3977-158">Определите подсеть, сетевой адаптер и виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="a3977-158">Define your subnet, NIC, and VNET:</span></span>

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

<span data-ttu-id="a3977-159">Присвойте имя виртуальной машине и настройте ее конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="a3977-159">Name your VM and create a VM config:</span></span>

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A1"
```

<span data-ttu-id="a3977-160">Определите операционную систему.</span><span class="sxs-lookup"><span data-stu-id="a3977-160">Define your OS:</span></span>

```powershell
$computerName = "myVM"
$vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

<span data-ttu-id="a3977-161">Добавьте к toohello сетевого Адаптера виртуальной Машины:</span><span class="sxs-lookup"><span data-stu-id="a3977-161">Add your NIC toohello VM:</span></span>

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

<span data-ttu-id="a3977-162">Определите toouse учетной записи хранилища hello:</span><span class="sxs-lookup"><span data-stu-id="a3977-162">Define hello storage account toouse:</span></span>

```powershell
$storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -AccountName mystorageaccount
```

<span data-ttu-id="a3977-163">Присоединение и отправка виртуального жесткого диска, подходящим образом подготовлена, tooyour виртуальной Машины для использования</span><span class="sxs-lookup"><span data-stu-id="a3977-163">Upload your VHD, suitably prepared, and attach tooyour VM for use:</span></span>

```powershell
$osDiskName = "licensing.vhd"
$osDiskUri = '{0}vhds/{1}{2}.vhd' -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/vhd/myvhd.vhd"
$vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption FromImage `
    -SourceImageUri $urlOfUploadedImageVhd -Windows
```

<span data-ttu-id="a3977-164">Наконец создайте ВМ и определите hello лицензирования тип tooutilize преимущество использования гибридной Azure:</span><span class="sxs-lookup"><span data-stu-id="a3977-164">Finally, create your VM and define hello licensing type tooutilize Azure Hybrid Use Benefit:</span></span>

<span data-ttu-id="a3977-165">Для Windows Server:</span><span class="sxs-lookup"><span data-stu-id="a3977-165">For Windows Server:</span></span>
```powershell
New-AzureRmVM -ResourceGroupName $resourceGroupName -Location $location -VM $vm -LicenseType "Windows_Server"
```

## <a name="deploy-a-virtual-machine-scale-set-via-resource-manager-template"></a><span data-ttu-id="a3977-166">Развертывание масштабируемого набора виртуальных машин с помощью шаблона Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a3977-166">Deploy a virtual machine scale set via Resource Manager template</span></span>
<span data-ttu-id="a3977-167">В шаблонах Resource Manager для масштабируемого набора виртуальных машин можно указывать дополнительный параметр для `licenseType`.</span><span class="sxs-lookup"><span data-stu-id="a3977-167">Within your VMSS Resource Manager templates, an additional parameter for `licenseType` must be specified.</span></span> <span data-ttu-id="a3977-168">Дополнительные сведения см. в статье [Создание шаблонов диспетчера ресурсов Azure](../../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a3977-168">You can read more about [authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span> <span data-ttu-id="a3977-169">Свойство licenseType hello tooinclude шаблона диспетчера ресурсов редактировать как часть набора масштабирования hello virtualMachineProfile и развертывания шаблона обычным образом — см. в примере ниже с помощью образа Windows Server 2016:</span><span class="sxs-lookup"><span data-stu-id="a3977-169">Edit your Resource Manager template tooinclude hello licenseType property as part of hello scale set’s virtualMachineProfile and deploy your template as normal - see example below using 2016 Windows Server image:</span></span>


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
> <span data-ttu-id="a3977-170">Поддержка развертывания масштабируемого набора виртуальных машин с преимуществами AHUB с использованием PowerShell и других средств SDK будет реализована в ближайшее время.</span><span class="sxs-lookup"><span data-stu-id="a3977-170">Support for deploying a virtual machine scale set with AHUB benefits through PowerShell and other SDK tools is coming soon.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="a3977-171">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a3977-171">Next steps</span></span>
<span data-ttu-id="a3977-172">Узнайте больше о [льготе на гибридное использование Microsoft Azure](https://azure.microsoft.com/pricing/hybrid-use-benefit/).</span><span class="sxs-lookup"><span data-stu-id="a3977-172">Read more about [Azure Hybrid Use Benefit licensing](https://azure.microsoft.com/pricing/hybrid-use-benefit/).</span></span>

<span data-ttu-id="a3977-173">Узнайте больше об [использовании шаблонов Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a3977-173">Learn more about [using Resource Manager templates](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="a3977-174">Дополнительные сведения о [преимущество использования гибридной Azure и Azure Site Recovery сделать перенос приложений tooAzure даже более экономически](https://azure.microsoft.com/blog/hybrid-use-benefit-migration-with-asr/).</span><span class="sxs-lookup"><span data-stu-id="a3977-174">Learn more about [Azure Hybrid Use Benefit and Azure Site Recovery make migrating applications tooAzure even more cost-effective](https://azure.microsoft.com/blog/hybrid-use-benefit-migration-with-asr/).</span></span>
