---
title: "Создание пользовательских образов виртуальных машин с помощью Azure PowerShell | Документация Майкрософт"
description: "Руководство по созданию пользовательского образа виртуальной машины с помощью Azure PowerShell."
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
ms.openlocfilehash: 96be2872a902a7d7063bf1dff7b4ca209a5b67c1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-powershell"></a><span data-ttu-id="e0c14-103">Создание пользовательского образа виртуальной машины Azure с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="e0c14-103">Create a custom image of an Azure VM using PowerShell</span></span>

<span data-ttu-id="e0c14-104">Пользовательские образы похожи на образы магазина, однако их можно создавать самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="e0c14-104">Custom images are like marketplace images, but you create them yourself.</span></span> <span data-ttu-id="e0c14-105">Пользовательские образы можно использовать для начальной загрузки конфигураций, например при предварительной загрузке приложений, конфигураций приложений и других конфигураций операционной системы.</span><span class="sxs-lookup"><span data-stu-id="e0c14-105">Custom images can be used to bootstrap configurations such as preloading applications, application configurations, and other OS configurations.</span></span> <span data-ttu-id="e0c14-106">В рамках этого руководства вы создадите собственный пользовательский образ виртуальной машины Azure.</span><span class="sxs-lookup"><span data-stu-id="e0c14-106">In this tutorial, you create your own custom image of an Azure virtual machine.</span></span> <span data-ttu-id="e0c14-107">Вы узнаете, как выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="e0c14-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e0c14-108">Подготовка виртуальной машины к использованию с помощью Sysprep</span><span class="sxs-lookup"><span data-stu-id="e0c14-108">Sysprep and generalize VMs</span></span>
> * <span data-ttu-id="e0c14-109">Создание пользовательского образа</span><span class="sxs-lookup"><span data-stu-id="e0c14-109">Create a custom image</span></span>
> * <span data-ttu-id="e0c14-110">Создание виртуальной машины из пользовательского образа</span><span class="sxs-lookup"><span data-stu-id="e0c14-110">Create a VM from a custom image</span></span>
> * <span data-ttu-id="e0c14-111">Получение списка всех образов в подписке</span><span class="sxs-lookup"><span data-stu-id="e0c14-111">List all the images in your subscription</span></span>
> * <span data-ttu-id="e0c14-112">Удаление образа</span><span class="sxs-lookup"><span data-stu-id="e0c14-112">Delete an image</span></span>

<span data-ttu-id="e0c14-113">Для работы с этим руководством требуется модуль Azure PowerShell версии не ниже 3.6.</span><span class="sxs-lookup"><span data-stu-id="e0c14-113">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="e0c14-114">Чтобы узнать версию, выполните команду ` Get-Module -ListAvailable AzureRM`.</span><span class="sxs-lookup"><span data-stu-id="e0c14-114">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="e0c14-115">Если вам необходимо выполнить обновление, ознакомьтесь со статьей, посвященной [установке модуля Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="e0c14-115">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e0c14-116">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="e0c14-116">Before you begin</span></span>

<span data-ttu-id="e0c14-117">Ниже подробно описано, как преобразовать существующую виртуальную машину в многократно используемый пользовательский образ, на основе которого можно создавать экземпляры виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="e0c14-117">The steps below detail how to take an existing VM and turn it into a re-usable custom image that you can use to create new VM instances.</span></span>

<span data-ttu-id="e0c14-118">Для выполнения примера в этом руководстве требуется виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="e0c14-118">To complete the example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="e0c14-119">Этот [пример сценария](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) позволяет создать ее при необходимости.</span><span class="sxs-lookup"><span data-stu-id="e0c14-119">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="e0c14-120">При работе с примером по мере необходимости заменяйте имена групп ресурсов и виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="e0c14-120">When working through the tutorial, replace the resource group and VM names where needed.</span></span>

## <a name="prepare-vm"></a><span data-ttu-id="e0c14-121">Подготовка виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="e0c14-121">Prepare VM</span></span>

<span data-ttu-id="e0c14-122">Чтобы создать образ виртуальной машины, нужно подготовить ее к использованию, отозвав и пометив исходную виртуальную машину как универсальную в Azure.</span><span class="sxs-lookup"><span data-stu-id="e0c14-122">To create an image of a virtual machine, you need to prepare the VM by generalizing the VM, deallocating, and then marking the source VM as generalized in Azure.</span></span>

### <a name="generalize-the-windows-vm-using-sysprep"></a><span data-ttu-id="e0c14-123">Подготовка виртуальной машины Windows к использованию с помощью Sysprep</span><span class="sxs-lookup"><span data-stu-id="e0c14-123">Generalize the Windows VM using Sysprep</span></span>

<span data-ttu-id="e0c14-124">Помимо прочих действий Sysprep удаляет все сведения о вашей учетной записи и подготавливает машину к использованию в качестве образа.</span><span class="sxs-lookup"><span data-stu-id="e0c14-124">Sysprep removes all your personal account information, among other things, and prepares the machine to be used as an image.</span></span> <span data-ttu-id="e0c14-125">Сведения о Sysprep см. в статье [Использование программы Sysprep: введение](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="e0c14-125">For details about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>


1. <span data-ttu-id="e0c14-126">Подключитесь к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="e0c14-126">Connect to the virtual machine.</span></span>
2. <span data-ttu-id="e0c14-127">Откройте окно командной строки с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="e0c14-127">Open the Command Prompt window as an administrator.</span></span> <span data-ttu-id="e0c14-128">Измените каталог на *%windir%\system32\sysprep* и запустите файл *sysprep.exe*.</span><span class="sxs-lookup"><span data-stu-id="e0c14-128">Change the directory to *%windir%\system32\sysprep*, and then run *sysprep.exe*.</span></span>
3. <span data-ttu-id="e0c14-129">В диалоговом окне **Программа подготовки системы** выберите *Переход в окно приветствия системы (OOBE)* и убедитесь, что установлен флажок *Подготовка к использованию*.</span><span class="sxs-lookup"><span data-stu-id="e0c14-129">In the **System Preparation Tool** dialog box, select *Enter System Out-of-Box Experience (OOBE)*, and make sure that the *Generalize* check box is selected.</span></span>
4. <span data-ttu-id="e0c14-130">В разделе **Параметры завершения работы** выберите *Завершение работы* и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e0c14-130">In **Shutdown Options**, select *Shutdown* and then click **OK**.</span></span>
5. <span data-ttu-id="e0c14-131">После выполнения всех необходимых действий Sysprep завершает работу виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="e0c14-131">When Sysprep completes, it shuts down the virtual machine.</span></span> <span data-ttu-id="e0c14-132">**Не перезапускайте виртуальную машину.**</span><span class="sxs-lookup"><span data-stu-id="e0c14-132">**Do not restart the VM**.</span></span>

### <a name="deallocate-and-mark-the-vm-as-generalized"></a><span data-ttu-id="e0c14-133">Отмена выделения и пометка виртуальной машины как обобщенной</span><span class="sxs-lookup"><span data-stu-id="e0c14-133">Deallocate and mark the VM as generalized</span></span>

<span data-ttu-id="e0c14-134">Чтобы создать образ виртуальной машины, необходимо отменить ее выделение и пометить ее как универсальную в Azure.</span><span class="sxs-lookup"><span data-stu-id="e0c14-134">To create an image, the VM needs to be deallocated and marked as generalized in Azure.</span></span>

<span data-ttu-id="e0c14-135">Отмените выделение виртуальной машины с помощью командлета [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="e0c14-135">Deallocated the VM using [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Force
```

<span data-ttu-id="e0c14-136">Теперь задайте для виртуальной машины состояние `-Generalized`, выполнив командлет [Set-AzureRmVm](/powershell/module/azurerm.compute/set-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="e0c14-136">Set the status of the virtual machine to `-Generalized` using [Set-AzureRmVm](/powershell/module/azurerm.compute/set-azurermvm).</span></span> 
   
```powershell
Set-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Generalized
```


## <a name="create-the-image"></a><span data-ttu-id="e0c14-137">Создание образа</span><span class="sxs-lookup"><span data-stu-id="e0c14-137">Create the image</span></span>

<span data-ttu-id="e0c14-138">Теперь можно создать образ виртуальной машины с помощью командлетов [New-AzureRmImageConfig](/powershell/module/azurerm.compute/new-azurermimageconfig) и [New-AzureRmImage](/powershell/module/azurerm.compute/new-azurermimage).</span><span class="sxs-lookup"><span data-stu-id="e0c14-138">Now you can create an image of the VM by using [New-AzureRmImageConfig](/powershell/module/azurerm.compute/new-azurermimageconfig) and [New-AzureRmImage](/powershell/module/azurerm.compute/new-azurermimage).</span></span> <span data-ttu-id="e0c14-139">В следующем примере создается образ *myImage* из виртуальной машины *myVM*.</span><span class="sxs-lookup"><span data-stu-id="e0c14-139">The following example creates an image named *myImage* from a VM named *myVM*.</span></span>

<span data-ttu-id="e0c14-140">Получите виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="e0c14-140">Get the virtual machine.</span></span> 

```powershell
$vm = Get-AzureRmVM -Name myVM -ResourceGroupName myResourceGroupImages
```

<span data-ttu-id="e0c14-141">Создайте конфигурацию образа.</span><span class="sxs-lookup"><span data-stu-id="e0c14-141">Create the image configuration.</span></span>

```powershell
$image = New-AzureRmImageConfig -Location EastUS -SourceVirtualMachineId $vm.ID 
```

<span data-ttu-id="e0c14-142">Создайте образ.</span><span class="sxs-lookup"><span data-stu-id="e0c14-142">Create the image.</span></span>

```powershell
New-AzureRmImage -Image $image -ImageName myImage -ResourceGroupName myResourceGroupImages
``` 

 
## <a name="create-vms-from-the-image"></a><span data-ttu-id="e0c14-143">Создание виртуальных машин из образа</span><span class="sxs-lookup"><span data-stu-id="e0c14-143">Create VMs from the image</span></span>

<span data-ttu-id="e0c14-144">Теперь, когда образ готов, из него можно создать одну или несколько виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="e0c14-144">Now that you have an image, you can create one or more new VMs from the image.</span></span> <span data-ttu-id="e0c14-145">Создание виртуальной машины из образа очень похоже на создание виртуальной машины с помощью образа Marketplace.</span><span class="sxs-lookup"><span data-stu-id="e0c14-145">Creating a VM from a custom image is very similar to creating a VM using a Marketplace image.</span></span> <span data-ttu-id="e0c14-146">При использовании образа Marketplace требуются сведения об образе, его поставщике, предложении, номере SKU и версии.</span><span class="sxs-lookup"><span data-stu-id="e0c14-146">When you use a Marketplace image, you have to information about the image, image provider, offer, SKU and version.</span></span> <span data-ttu-id="e0c14-147">В случае пользовательского образа необходимо просто указать идентификатор его ресурса.</span><span class="sxs-lookup"><span data-stu-id="e0c14-147">With a custom image, you just need to provide the ID of the custom image resource.</span></span> 

<span data-ttu-id="e0c14-148">В следующем сценарии создается переменная *$image* для сохранения сведений о пользовательском образе с помощью командлета [Get-AzureRmImage](/powershell/module/azurerm.compute/get-azurermimage), затем выполняется командлет [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) и указывается идентификатор с помощью только что созданной переменной *$image*.</span><span class="sxs-lookup"><span data-stu-id="e0c14-148">In the following script, we create a variable *$image* to store information about the custom image using [Get-AzureRmImage](/powershell/module/azurerm.compute/get-azurermimage) and then we use [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) and specify the ID using the *$image* variable we just created.</span></span> 

<span data-ttu-id="e0c14-149">Этот сценарий создает виртуальную машину *myVMfromImage* из пользовательского образа в новой группе ресурсов *myResourceGroupFromImage* в расположении *Западная часть США*.</span><span class="sxs-lookup"><span data-stu-id="e0c14-149">The script creates a VM named *myVMfromImage* from our custom image in a new resource group named *myResourceGroupFromImage* in the *West US* location.</span></span>


```powershell
$cred = Get-Credential -Message "Enter a username and password for the virtual machine."

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

# Here is where we create a variable to store information about the image 
$image = Get-AzureRmImage `
    -ImageName myImage `
    -ResourceGroupName myResourceGroupImages

# Here is where we specify that we want to create the VM from and image and provide the image ID
$vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -Id $image.Id

$vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id

New-AzureRmVM `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -VM $vmConfig
```

## <a name="image-management"></a><span data-ttu-id="e0c14-150">Управление образами</span><span class="sxs-lookup"><span data-stu-id="e0c14-150">Image management</span></span> 

<span data-ttu-id="e0c14-151">Ниже приведены некоторые примеры распространенных задач управления образами, а также способы их выполнения с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e0c14-151">Here are some examples of common management image tasks and how to complete them using PowerShell.</span></span>

<span data-ttu-id="e0c14-152">Вывод списка всех образов по имени.</span><span class="sxs-lookup"><span data-stu-id="e0c14-152">List all images by name.</span></span>

```powershell
$images = Find-AzureRMResource -ResourceType Microsoft.Compute/images 
$images.name
```

<span data-ttu-id="e0c14-153">Удаление образа.</span><span class="sxs-lookup"><span data-stu-id="e0c14-153">Delete an image.</span></span> <span data-ttu-id="e0c14-154">В этом примере из *myResourceGroup* удаляется образ с именем *myOldImage*.</span><span class="sxs-lookup"><span data-stu-id="e0c14-154">This example deletes the image named *myOldImage* from the *myResourceGroup*.</span></span>

```powershell
Remove-AzureRmImage `
    -ImageName myOldImage `
    -ResourceGroupName myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="e0c14-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e0c14-155">Next steps</span></span>

<span data-ttu-id="e0c14-156">В рамках этого руководства вы создали пользовательский образ виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="e0c14-156">In this tutorial, you created a custom VM image.</span></span> <span data-ttu-id="e0c14-157">Вы научились выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="e0c14-157">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e0c14-158">Подготовка виртуальной машины к использованию с помощью Sysprep</span><span class="sxs-lookup"><span data-stu-id="e0c14-158">Sysprep and generalize VMs</span></span>
> * <span data-ttu-id="e0c14-159">Создание пользовательского образа</span><span class="sxs-lookup"><span data-stu-id="e0c14-159">Create a custom image</span></span>
> * <span data-ttu-id="e0c14-160">Создание виртуальной машины из пользовательского образа</span><span class="sxs-lookup"><span data-stu-id="e0c14-160">Create a VM from a custom image</span></span>
> * <span data-ttu-id="e0c14-161">Получение списка всех образов в подписке</span><span class="sxs-lookup"><span data-stu-id="e0c14-161">List all the images in your subscription</span></span>
> * <span data-ttu-id="e0c14-162">Удаление образа</span><span class="sxs-lookup"><span data-stu-id="e0c14-162">Delete an image</span></span>

<span data-ttu-id="e0c14-163">Перейдите к следующему руководству, чтобы узнать о высокодоступных виртуальных машинах.</span><span class="sxs-lookup"><span data-stu-id="e0c14-163">Advance to the next tutorial to learn about how highly available virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e0c14-164">Создание высокодоступных виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="e0c14-164">Create highly available VMs</span></span>](tutorial-availability-sets.md)



