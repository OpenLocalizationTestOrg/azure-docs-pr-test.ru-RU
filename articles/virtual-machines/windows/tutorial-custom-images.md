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
# <a name="create-a-custom-image-of-an-azure-vm-using-powershell"></a><span data-ttu-id="d887a-103">Создание пользовательского образа виртуальной машины Azure с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="d887a-103">Create a custom image of an Azure VM using PowerShell</span></span>

<span data-ttu-id="d887a-104">Пользовательские образы похожи на образы магазина, однако их можно создавать самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="d887a-104">Custom images are like marketplace images, but you create them yourself.</span></span> <span data-ttu-id="d887a-105">Пользовательские изображения может быть конфигурации используется toobootstrap, такие как предварительной загрузки приложений, конфигурации приложений и других настроек операционной системы.</span><span class="sxs-lookup"><span data-stu-id="d887a-105">Custom images can be used toobootstrap configurations such as preloading applications, application configurations, and other OS configurations.</span></span> <span data-ttu-id="d887a-106">В рамках этого руководства вы создадите собственный пользовательский образ виртуальной машины Azure.</span><span class="sxs-lookup"><span data-stu-id="d887a-106">In this tutorial, you create your own custom image of an Azure virtual machine.</span></span> <span data-ttu-id="d887a-107">Вы узнаете, как выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="d887a-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d887a-108">Подготовка виртуальной машины к использованию с помощью Sysprep</span><span class="sxs-lookup"><span data-stu-id="d887a-108">Sysprep and generalize VMs</span></span>
> * <span data-ttu-id="d887a-109">Создание пользовательского образа</span><span class="sxs-lookup"><span data-stu-id="d887a-109">Create a custom image</span></span>
> * <span data-ttu-id="d887a-110">Создание виртуальной машины из пользовательского образа</span><span class="sxs-lookup"><span data-stu-id="d887a-110">Create a VM from a custom image</span></span>
> * <span data-ttu-id="d887a-111">Отображение списка всех образов hello в подписке</span><span class="sxs-lookup"><span data-stu-id="d887a-111">List all hello images in your subscription</span></span>
> * <span data-ttu-id="d887a-112">удалять образ.</span><span class="sxs-lookup"><span data-stu-id="d887a-112">Delete an image</span></span>

<span data-ttu-id="d887a-113">Этот учебник требует hello Azure PowerShell модуль версии 3.6 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="d887a-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="d887a-114">Запустите ` Get-Module -ListAvailable AzureRM` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="d887a-114">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="d887a-115">Получить tooupgrade [установите Azure PowerShell модуль](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="d887a-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d887a-116">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="d887a-116">Before you begin</span></span>

<span data-ttu-id="d887a-117">в следующих шагах Hello подробно, как tootake существующей виртуальной Машины и включите его в доступных для использования пользовательского образа, который можно использовать toocreate новые экземпляры виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="d887a-117">hello steps below detail how tootake an existing VM and turn it into a re-usable custom image that you can use toocreate new VM instances.</span></span>

<span data-ttu-id="d887a-118">Пример hello toocomplete в этом учебнике, необходимо иметь существующую виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="d887a-118">toocomplete hello example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="d887a-119">Этот [пример сценария](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) позволяет создать ее при необходимости.</span><span class="sxs-lookup"><span data-stu-id="d887a-119">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="d887a-120">Если заменить прохождение учебника hello группы ресурсов hello и ВМ имен при необходимости.</span><span class="sxs-lookup"><span data-stu-id="d887a-120">When working through hello tutorial, replace hello resource group and VM names where needed.</span></span>

## <a name="prepare-vm"></a><span data-ttu-id="d887a-121">Подготовка виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="d887a-121">Prepare VM</span></span>

<span data-ttu-id="d887a-122">toocreate образ виртуальной машины, необходимо tooprepare hello ВМ путем выявления hello виртуальной Машины, освобождение и пометки hello исходной виртуальной Машины, как обобщенный в Azure.</span><span class="sxs-lookup"><span data-stu-id="d887a-122">toocreate an image of a virtual machine, you need tooprepare hello VM by generalizing hello VM, deallocating, and then marking hello source VM as generalized in Azure.</span></span>

### <a name="generalize-hello-windows-vm-using-sysprep"></a><span data-ttu-id="d887a-123">Обобщить hello виртуальной Машины Windows с помощью программы Sysprep</span><span class="sxs-lookup"><span data-stu-id="d887a-123">Generalize hello Windows VM using Sysprep</span></span>

<span data-ttu-id="d887a-124">Sysprep удаляет все ваши личные сведения, помимо прочего и подготавливает toobe машины hello, используемое в качестве изображения.</span><span class="sxs-lookup"><span data-stu-id="d887a-124">Sysprep removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="d887a-125">Дополнительные сведения о программе Sysprep см. в разделе [как tooUse Sysprep: введение](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="d887a-125">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>


1. <span data-ttu-id="d887a-126">Подключение toohello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d887a-126">Connect toohello virtual machine.</span></span>
2. <span data-ttu-id="d887a-127">Привет открыть окно командной строки с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="d887a-127">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="d887a-128">Измените каталог hello слишком*%windir%\system32\sysprep*, а затем запустите *sysprep.exe*.</span><span class="sxs-lookup"><span data-stu-id="d887a-128">Change hello directory too*%windir%\system32\sysprep*, and then run *sysprep.exe*.</span></span>
3. <span data-ttu-id="d887a-129">В hello **средство подготовки системы** выберите *Enter System Out-of-Box Experience (OOBE)*и убедитесь, что hello *Generalize* установлен флажок.</span><span class="sxs-lookup"><span data-stu-id="d887a-129">In hello **System Preparation Tool** dialog box, select *Enter System Out-of-Box Experience (OOBE)*, and make sure that hello *Generalize* check box is selected.</span></span>
4. <span data-ttu-id="d887a-130">В разделе **Параметры завершения работы** выберите *Завершение работы* и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d887a-130">In **Shutdown Options**, select *Shutdown* and then click **OK**.</span></span>
5. <span data-ttu-id="d887a-131">По завершении работы программы Sysprep завершает hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d887a-131">When Sysprep completes, it shuts down hello virtual machine.</span></span> <span data-ttu-id="d887a-132">**Не перезагружайте hello виртуальной Машины**.</span><span class="sxs-lookup"><span data-stu-id="d887a-132">**Do not restart hello VM**.</span></span>

### <a name="deallocate-and-mark-hello-vm-as-generalized"></a><span data-ttu-id="d887a-133">Выделение и пометить hello виртуальной Машины как обобщенный</span><span class="sxs-lookup"><span data-stu-id="d887a-133">Deallocate and mark hello VM as generalized</span></span>

<span data-ttu-id="d887a-134">toocreate изображения hello виртуальной Машины должен toobe освобожден и отмечается как обобщенный в Azure.</span><span class="sxs-lookup"><span data-stu-id="d887a-134">toocreate an image, hello VM needs toobe deallocated and marked as generalized in Azure.</span></span>

<span data-ttu-id="d887a-135">Освобожденные hello виртуальной Машины с помощью [Stop AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="d887a-135">Deallocated hello VM using [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Force
```

<span data-ttu-id="d887a-136">Задать состояние hello hello виртуальной машины слишком`-Generalized` с помощью [AzureRmVm набор](/powershell/module/azurerm.compute/set-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="d887a-136">Set hello status of hello virtual machine too`-Generalized` using [Set-AzureRmVm](/powershell/module/azurerm.compute/set-azurermvm).</span></span> 
   
```powershell
Set-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Generalized
```


## <a name="create-hello-image"></a><span data-ttu-id="d887a-137">Создание образа hello</span><span class="sxs-lookup"><span data-stu-id="d887a-137">Create hello image</span></span>

<span data-ttu-id="d887a-138">Теперь можно создавать с помощью образа виртуальной Машины hello [New AzureRmImageConfig](/powershell/module/azurerm.compute/new-azurermimageconfig) и [New AzureRmImage](/powershell/module/azurerm.compute/new-azurermimage).</span><span class="sxs-lookup"><span data-stu-id="d887a-138">Now you can create an image of hello VM by using [New-AzureRmImageConfig](/powershell/module/azurerm.compute/new-azurermimageconfig) and [New-AzureRmImage](/powershell/module/azurerm.compute/new-azurermimage).</span></span> <span data-ttu-id="d887a-139">Hello следующий пример создает образ с именем *myImage* из виртуальной Машины с именем *myVM*.</span><span class="sxs-lookup"><span data-stu-id="d887a-139">hello following example creates an image named *myImage* from a VM named *myVM*.</span></span>

<span data-ttu-id="d887a-140">Получение hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d887a-140">Get hello virtual machine.</span></span> 

```powershell
$vm = Get-AzureRmVM -Name myVM -ResourceGroupName myResourceGroupImages
```

<span data-ttu-id="d887a-141">Создайте конфигурацию hello изображения.</span><span class="sxs-lookup"><span data-stu-id="d887a-141">Create hello image configuration.</span></span>

```powershell
$image = New-AzureRmImageConfig -Location EastUS -SourceVirtualMachineId $vm.ID 
```

<span data-ttu-id="d887a-142">Создание образа hello.</span><span class="sxs-lookup"><span data-stu-id="d887a-142">Create hello image.</span></span>

```powershell
New-AzureRmImage -Image $image -ImageName myImage -ResourceGroupName myResourceGroupImages
``` 

 
## <a name="create-vms-from-hello-image"></a><span data-ttu-id="d887a-143">Создать виртуальные машины из образа hello</span><span class="sxs-lookup"><span data-stu-id="d887a-143">Create VMs from hello image</span></span>

<span data-ttu-id="d887a-144">Теперь, когда у вас есть образ, можно создать один или несколько новых виртуальных машин из образа hello.</span><span class="sxs-lookup"><span data-stu-id="d887a-144">Now that you have an image, you can create one or more new VMs from hello image.</span></span> <span data-ttu-id="d887a-145">Создание виртуальной Машины из образа — очень похожа toocreating ВМ с помощью образа Marketplace.</span><span class="sxs-lookup"><span data-stu-id="d887a-145">Creating a VM from a custom image is very similar toocreating a VM using a Marketplace image.</span></span> <span data-ttu-id="d887a-146">При использовании образа Marketplace, у вас есть tooinformation о hello изображения, поставщик образов, предложение, SKU и версии.</span><span class="sxs-lookup"><span data-stu-id="d887a-146">When you use a Marketplace image, you have tooinformation about hello image, image provider, offer, SKU and version.</span></span> <span data-ttu-id="d887a-147">С помощью пользовательского образа необходимо просто tooprovide идентификатор hello hello пользовательский ресурс изображения.</span><span class="sxs-lookup"><span data-stu-id="d887a-147">With a custom image, you just need tooprovide hello ID of hello custom image resource.</span></span> 

<span data-ttu-id="d887a-148">В следующий скрипт hello, мы создадим переменной *$image* toostore сведения об использовании настраиваемого образа hello [Get AzureRmImage](/powershell/module/azurerm.compute/get-azurermimage) и затем мы используем [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage)и укажите идентификатор hello, с помощью hello *$image* переменной мы только что создали.</span><span class="sxs-lookup"><span data-stu-id="d887a-148">In hello following script, we create a variable *$image* toostore information about hello custom image using [Get-AzureRmImage](/powershell/module/azurerm.compute/get-azurermimage) and then we use [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) and specify hello ID using hello *$image* variable we just created.</span></span> 

<span data-ttu-id="d887a-149">Hello скрипт создает Виртуальную машину с именем *myVMfromImage* из наших настраиваемого изображения в новую группу ресурсов с именем *myResourceGroupFromImage* в hello *Запад США* расположение.</span><span class="sxs-lookup"><span data-stu-id="d887a-149">hello script creates a VM named *myVMfromImage* from our custom image in a new resource group named *myResourceGroupFromImage* in hello *West US* location.</span></span>


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

## <a name="image-management"></a><span data-ttu-id="d887a-150">Управление образами</span><span class="sxs-lookup"><span data-stu-id="d887a-150">Image management</span></span> 

<span data-ttu-id="d887a-151">Ниже приведены некоторые примеры типичных задач управления изображения и как toocomplete их с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d887a-151">Here are some examples of common management image tasks and how toocomplete them using PowerShell.</span></span>

<span data-ttu-id="d887a-152">Вывод списка всех образов по имени.</span><span class="sxs-lookup"><span data-stu-id="d887a-152">List all images by name.</span></span>

```powershell
$images = Find-AzureRMResource -ResourceType Microsoft.Compute/images 
$images.name
```

<span data-ttu-id="d887a-153">Удаление образа.</span><span class="sxs-lookup"><span data-stu-id="d887a-153">Delete an image.</span></span> <span data-ttu-id="d887a-154">Этот пример удаляет hello изображение с именем *myOldImage* из hello *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="d887a-154">This example deletes hello image named *myOldImage* from hello *myResourceGroup*.</span></span>

```powershell
Remove-AzureRmImage `
    -ImageName myOldImage `
    -ResourceGroupName myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="d887a-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d887a-155">Next steps</span></span>

<span data-ttu-id="d887a-156">В рамках этого руководства вы создали пользовательский образ виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d887a-156">In this tutorial, you created a custom VM image.</span></span> <span data-ttu-id="d887a-157">Вы научились выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="d887a-157">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d887a-158">Подготовка виртуальной машины к использованию с помощью Sysprep</span><span class="sxs-lookup"><span data-stu-id="d887a-158">Sysprep and generalize VMs</span></span>
> * <span data-ttu-id="d887a-159">Создание пользовательского образа</span><span class="sxs-lookup"><span data-stu-id="d887a-159">Create a custom image</span></span>
> * <span data-ttu-id="d887a-160">Создание виртуальной машины из пользовательского образа</span><span class="sxs-lookup"><span data-stu-id="d887a-160">Create a VM from a custom image</span></span>
> * <span data-ttu-id="d887a-161">Отображение списка всех образов hello в подписке</span><span class="sxs-lookup"><span data-stu-id="d887a-161">List all hello images in your subscription</span></span>
> * <span data-ttu-id="d887a-162">удалять образ.</span><span class="sxs-lookup"><span data-stu-id="d887a-162">Delete an image</span></span>

<span data-ttu-id="d887a-163">Переместить следующий учебник toolearn toohello о том, как высокодоступные виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="d887a-163">Advance toohello next tutorial toolearn about how highly available virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d887a-164">Создание высокодоступных виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="d887a-164">Create highly available VMs</span></span>](tutorial-availability-sets.md)



