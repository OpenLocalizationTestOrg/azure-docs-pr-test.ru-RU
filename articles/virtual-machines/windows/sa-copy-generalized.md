---
title: "Создание неуправляемого образа универсальной виртуальной машины в Azure | Документы Майкрософт"
description: "Создание неуправляемого образа универсальной виртуальной машины Windows, который будет использоваться для создания нескольких копий виртуальной машины в Azure."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: d7f4a9558175835eba9096e6845726f21c7459d3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-create-an-unmanaged-vm-image-from-an-azure-vm"></a><span data-ttu-id="75ee4-103">Создание неуправляемого образа виртуальной машины на основе виртуальной машины Azure</span><span class="sxs-lookup"><span data-stu-id="75ee4-103">How to create an unmanaged VM image from an Azure VM</span></span>

<span data-ttu-id="75ee4-104">В этой статье описывается использование учетных записей хранения.</span><span class="sxs-lookup"><span data-stu-id="75ee4-104">This article covers using storage accounts.</span></span> <span data-ttu-id="75ee4-105">Мы рекомендуем использовать управляемые диски и управляемые образы вместо учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="75ee4-105">We recommend that you use managed disks and managed images instead of a storage account.</span></span> <span data-ttu-id="75ee4-106">Дополнительные сведения см. в статье [Запись управляемого образа универсальной виртуальной машины в Azure](capture-image-resource.md).</span><span class="sxs-lookup"><span data-stu-id="75ee4-106">For more information, see [Capture a managed image of a generalized VM in Azure](capture-image-resource.md).</span></span>

<span data-ttu-id="75ee4-107">В этой статье показано, как использовать Azure PowerShell для создания образа универсальной виртуальной машины Azure с помощью учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="75ee4-107">This article shows you how to use Azure PowerShell to create an image of a generalized Azure VM using a storage account.</span></span> <span data-ttu-id="75ee4-108">Такой образ можно затем использовать для создания другой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="75ee4-108">You can then use the image to create another VM.</span></span> <span data-ttu-id="75ee4-109">Этот образ включает в себя диск операционной системы и другие диски данных, присоединенные к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="75ee4-109">The image includes the OS disk and the data disks that are attached to the virtual machine.</span></span> <span data-ttu-id="75ee4-110">Образ не включает ресурсы виртуальной сети, поэтому их придется настроить при создании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="75ee4-110">The image doesn't include the virtual network resources, so you need to set up those resources when you create the new VM.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="75ee4-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="75ee4-111">Prerequisites</span></span>
<span data-ttu-id="75ee4-112">У вас должна быть установлена среда Azure PowerShell 1.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="75ee4-112">You need to have Azure PowerShell version 1.0.x or newer installed.</span></span> <span data-ttu-id="75ee4-113">Если вы еще не установили PowerShell, см. статью [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="75ee4-113">If you haven't already installed PowerShell, read [How to install and configure Azure PowerShell](/powershell/azure/overview) for installation steps.</span></span>

## <a name="generalize-the-vm"></a><span data-ttu-id="75ee4-114">Подготовка виртуальной машины к использованию</span><span class="sxs-lookup"><span data-stu-id="75ee4-114">Generalize the VM</span></span> 
<span data-ttu-id="75ee4-115">В этом разделе содержатся сведения о том, как обобщить виртуальную машину Windows для ее дальнейшего использования в качестве образа.</span><span class="sxs-lookup"><span data-stu-id="75ee4-115">This section shows you how to generalize your Windows virtual machine for use as an image.</span></span> <span data-ttu-id="75ee4-116">При подготовке виртуальной машины удаляются все сведения о вашей учетной записи и выполняется настройка ВМ для использования в качестве образа.</span><span class="sxs-lookup"><span data-stu-id="75ee4-116">Generalizing a VM removes all your personal account information, among other things, and prepares the machine to be used as an image.</span></span> <span data-ttu-id="75ee4-117">Сведения о Sysprep см. в статье [Использование программы Sysprep: введение](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="75ee4-117">For details about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="75ee4-118">Убедитесь, что Sysprep поддерживает роли сервера, запущенные на компьютере.</span><span class="sxs-lookup"><span data-stu-id="75ee4-118">Make sure the server roles running on the machine are supported by Sysprep.</span></span> <span data-ttu-id="75ee4-119">Дополнительные сведения см. в статье [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles) (Поддержка серверных ролей в Sysprep).</span><span class="sxs-lookup"><span data-stu-id="75ee4-119">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="75ee4-120">Если вы впервые отправляете виртуальный жесткий диск в Azure, перед запуском Sysprep [подготовьте виртуальную машину](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="75ee4-120">If you are uploading your VHD to Azure for the first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

<span data-ttu-id="75ee4-121">Можно также подготовить виртуальную машину Linux к использованию с помощью `sudo waagent -deprovision+user`, а затем использовать PowerShell для ее записи.</span><span class="sxs-lookup"><span data-stu-id="75ee4-121">You can also generalize a Linux VM using `sudo waagent -deprovision+user` and then use PowerShell to capture the VM.</span></span> <span data-ttu-id="75ee4-122">Сведения об использовании интерфейса командной строки для записи виртуальной машины см. в разделе [Как подготовить к работе и записать образ виртуальной машины Linux с помощью Azure CLI](../linux/capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="75ee4-122">For information about using the CLI to capture a VM, see [How to generalize and capture a Linux virtual machine using the Azure CLI ](../linux/capture-image.md).</span></span>


1. <span data-ttu-id="75ee4-123">Выполните вход на виртуальную машину Windows.</span><span class="sxs-lookup"><span data-stu-id="75ee4-123">Sign in to the Windows virtual machine.</span></span>
2. <span data-ttu-id="75ee4-124">Откройте окно командной строки с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="75ee4-124">Open the Command Prompt window as an administrator.</span></span> <span data-ttu-id="75ee4-125">Измените каталог на **%windir%\system32\sysprep** и запустите файл `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="75ee4-125">Change the directory to **%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="75ee4-126">В диалоговом окне **Программа подготовки системы** выберите **Переход в окно приветствия системы (OOBE)** и убедитесь, что установлен флажок **Подготовка к использованию**.</span><span class="sxs-lookup"><span data-stu-id="75ee4-126">In the **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that the **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="75ee4-127">В разделе **Параметры завершения работы** выберите **Завершение работы**.</span><span class="sxs-lookup"><span data-stu-id="75ee4-127">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="75ee4-128">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="75ee4-128">Click **OK**.</span></span>
   
    ![Запуск Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="75ee4-130">После выполнения всех необходимых действий Sysprep завершает работу виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="75ee4-130">When Sysprep completes, it shuts down the virtual machine.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="75ee4-131">Не перезапускайте виртуальную машину до завершения передачи VHD в Azure или создания образа виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="75ee4-131">Do not restart the VM until you are done uploading the VHD to Azure or creating an image from the VM.</span></span> <span data-ttu-id="75ee4-132">Если виртуальная машина случайно будет перезапущена, запустите инструмент Sysprep, чтобы повторно подготовить ее.</span><span class="sxs-lookup"><span data-stu-id="75ee4-132">If the VM accidentally gets restarted, run Sysprep to generalize it again.</span></span>
> 
> 

## <a name="log-in-to-azure-powershell"></a><span data-ttu-id="75ee4-133">Вход в Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="75ee4-133">Log in to Azure PowerShell</span></span>
1. <span data-ttu-id="75ee4-134">Откройте Azure PowerShell и войдите в свою учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="75ee4-134">Open Azure PowerShell and sign in to your Azure account.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
   
    <span data-ttu-id="75ee4-135">Откроется всплывающее окно для ввода данных учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="75ee4-135">A pop-up window opens for you to enter your Azure account credentials.</span></span>
2. <span data-ttu-id="75ee4-136">Получите идентификаторы доступных вам подписок.</span><span class="sxs-lookup"><span data-stu-id="75ee4-136">Get the subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="75ee4-137">Укажите соответствующую подписку с помощью идентификатора.</span><span class="sxs-lookup"><span data-stu-id="75ee4-137">Set the correct subscription using the subscription ID.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="deallocate-the-vm-and-set-the-state-to-generalized"></a><span data-ttu-id="75ee4-138">Отмена распределения для виртуальной машины и установка состояния "универсальный"</span><span class="sxs-lookup"><span data-stu-id="75ee4-138">Deallocate the VM and set the state to generalized</span></span>
1. <span data-ttu-id="75ee4-139">Отмените распределение ресурсов для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="75ee4-139">Deallocate the VM resources.</span></span>
   
    ```powershell
    Stop-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName>
    ```
   
    <span data-ttu-id="75ee4-140">*Состояние* виртуальной машины на портале Azure изменится с **Остановлено** на **Остановлено (освобождено)**.</span><span class="sxs-lookup"><span data-stu-id="75ee4-140">The *Status* for the VM in the Azure portal changes from **Stopped** to **Stopped (deallocated)**.</span></span>
2. <span data-ttu-id="75ee4-141">Теперь задайте для виртуальной машины состояние **Generalized**(Универсальная).</span><span class="sxs-lookup"><span data-stu-id="75ee4-141">Set the status of the virtual machine to **Generalized**.</span></span> 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName <resourceGroup> -Name <vmName> -Generalized
    ```
3. <span data-ttu-id="75ee4-142">Проверьте состояние виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="75ee4-142">Check the status of the VM.</span></span> <span data-ttu-id="75ee4-143">В разделе **OSState/generalized** для этой виртуальной машины параметр **DisplayStatus** должен иметь значение **VM generalized**.</span><span class="sxs-lookup"><span data-stu-id="75ee4-143">The **OSState/generalized** section for the VM should have the **DisplayStatus** set to **VM generalized**.</span></span>  
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName> -Status
    $vm.Statuses
    ```

## <a name="create-the-image"></a><span data-ttu-id="75ee4-144">Создание образа</span><span class="sxs-lookup"><span data-stu-id="75ee4-144">Create the image</span></span>

<span data-ttu-id="75ee4-145">Создайте неуправляемый образ виртуальной машины в целевом контейнере хранилища с помощью этой команды.</span><span class="sxs-lookup"><span data-stu-id="75ee4-145">Create an unmanaged virtual machine image in the destination storage container using this command.</span></span> <span data-ttu-id="75ee4-146">Образ будет создан в той же учетной записи хранения, что и исходная виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="75ee4-146">The image is created in the same storage account as the original virtual machine.</span></span> <span data-ttu-id="75ee4-147">Параметр `-Path` сохраняет копию шаблона JSON для исходной виртуальной машины на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="75ee4-147">The `-Path` parameter saves a copy of the JSON template for the source VM to your local computer.</span></span> <span data-ttu-id="75ee4-148">Параметр `-DestinationContainerName` содержит имя контейнера для хранения образов.</span><span class="sxs-lookup"><span data-stu-id="75ee4-148">The `-DestinationContainerName` parameter is the name of the container that you want to hold your images.</span></span> <span data-ttu-id="75ee4-149">Если такой контейнер не существует, он будет создан автоматически.</span><span class="sxs-lookup"><span data-stu-id="75ee4-149">If the container doesn't exist, it is created for you.</span></span>
   
```powershell
Save-AzureRmVMImage -ResourceGroupName <resourceGroupName> -Name <vmName> `
    -DestinationContainerName <destinationContainerName> -VHDNamePrefix <templateNamePrefix> `
    -Path <C:\local\Filepath\Filename.json>
```
   
<span data-ttu-id="75ee4-150">URL-адрес образа можно получить из шаблона файла JSON.</span><span class="sxs-lookup"><span data-stu-id="75ee4-150">You can get the URL of your image from the JSON file template.</span></span> <span data-ttu-id="75ee4-151">Перейдите к разделу **resources** > **storageProfile** > **osDisk** > **image** > **uri**, чтобы получить полный путь к образу.</span><span class="sxs-lookup"><span data-stu-id="75ee4-151">Go to the **resources** > **storageProfile** > **osDisk** > **image** > **uri** section for the complete path of your image.</span></span> <span data-ttu-id="75ee4-152">URL-адрес образа выглядит так: `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.</span><span class="sxs-lookup"><span data-stu-id="75ee4-152">The URL of the image looks like: `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.</span></span>
   
<span data-ttu-id="75ee4-153">Также вы также можете проверить URI на портале.</span><span class="sxs-lookup"><span data-stu-id="75ee4-153">You can also verify the URI in the portal.</span></span> <span data-ttu-id="75ee4-154">Образ копируется в контейнер **system** в вашей учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="75ee4-154">The image is copied to a container named **system** in your storage account.</span></span> 

## <a name="create-a-vm-from-the-image"></a><span data-ttu-id="75ee4-155">Создание виртуальной машины на основе образа</span><span class="sxs-lookup"><span data-stu-id="75ee4-155">Create a VM from the image</span></span>

<span data-ttu-id="75ee4-156">Теперь вы можете создать одну или несколько виртуальных машин на основе неуправляемого образа.</span><span class="sxs-lookup"><span data-stu-id="75ee4-156">Now you can create one or more VMs from the unmanaged image.</span></span>

### <a name="set-the-uri-of-the-vhd"></a><span data-ttu-id="75ee4-157">Указание универсального кода ресурса (URI) диска VHD</span><span class="sxs-lookup"><span data-stu-id="75ee4-157">Set the URI of the VHD</span></span>

<span data-ttu-id="75ee4-158">Код URI, который должен использовать диск VHD, имеет такой формат: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span><span class="sxs-lookup"><span data-stu-id="75ee4-158">The URI for the VHD to use is in the format: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span></span> <span data-ttu-id="75ee4-159">В этом примере диск VHD с именем **myVHD** находится в учетной записи хранения **mystorageaccount** в контейнере **mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="75ee4-159">In this example the VHD named **myVHD** is in the storage account **mystorageaccount** in the container **mycontainer**.</span></span>

```powershell
$imageURI = "https://mystorageaccount.blob.core.windows.net/mycontainer/myVhd.vhd"
```


### <a name="create-a-virtual-network"></a><span data-ttu-id="75ee4-160">Создать виртуальную сеть</span><span class="sxs-lookup"><span data-stu-id="75ee4-160">Create a virtual network</span></span>
<span data-ttu-id="75ee4-161">Создайте виртуальную сеть и подсеть [виртуальной сети](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="75ee4-161">Create the vNet and subnet of the [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="75ee4-162">Создание подсети.</span><span class="sxs-lookup"><span data-stu-id="75ee4-162">Create the subnet.</span></span> <span data-ttu-id="75ee4-163">В следующем примере создается подсеть с именем **mySubnet** в группе ресурсов **myResourceGroup** с префикс адреса **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="75ee4-163">The following sample creates a subnet named **mySubnet** in the resource group **myResourceGroup** with the address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="75ee4-164">Создание виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="75ee4-164">Create the virtual network.</span></span> <span data-ttu-id="75ee4-165">В следующем примере создается виртуальная сеть с именем **myVnet** в расположении **Запад США** с префиксом адреса **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="75ee4-165">The following sample creates a virtual network named **myVnet** in the **West US** location with the address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="75ee4-166">Создание общедоступного IP-адреса и сетевого интерфейса</span><span class="sxs-lookup"><span data-stu-id="75ee4-166">Create a public IP address and network interface</span></span>
<span data-ttu-id="75ee4-167">Чтобы обеспечить обмен данными с виртуальной машиной в виртуальной сети, требуются [общедоступный IP-адрес](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) и сетевой интерфейс.</span><span class="sxs-lookup"><span data-stu-id="75ee4-167">To enable communication with the virtual machine in the virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="75ee4-168">Создание общедоступного IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="75ee4-168">Create a public IP address.</span></span> <span data-ttu-id="75ee4-169">В этом примере создается общедоступный IP-адрес с именем **myPip**.</span><span class="sxs-lookup"><span data-stu-id="75ee4-169">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="75ee4-170">Создание сетевой карты.</span><span class="sxs-lookup"><span data-stu-id="75ee4-170">Create the NIC.</span></span> <span data-ttu-id="75ee4-171">В этом примере создается сетевая карта с именем **myNic**.</span><span class="sxs-lookup"><span data-stu-id="75ee4-171">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-the-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="75ee4-172">Создание группы безопасности сети и правила RDP</span><span class="sxs-lookup"><span data-stu-id="75ee4-172">Create the network security group and an RDP rule</span></span>
<span data-ttu-id="75ee4-173">Чтобы войти на виртуальную машину с помощью RDP, необходимо настроить правило безопасности, которое разрешает доступ RDP через порт 3389.</span><span class="sxs-lookup"><span data-stu-id="75ee4-173">To be able to log in to your VM using RDP, you need to have a security rule that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="75ee4-174">В этом примере создается группа безопасности сети с именем **myNsg**, которая содержит правило с именем **myRdpRule**, разрешающее трафик RDP через порт 3389.</span><span class="sxs-lookup"><span data-stu-id="75ee4-174">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="75ee4-175">Дополнительные сведения о группах безопасности сети см. в статье [Открытие портов для виртуальной машины в Azure с помощью PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="75ee4-175">For more information about NSGs, see [Opening ports to a VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


### <a name="create-a-variable-for-the-virtual-network"></a><span data-ttu-id="75ee4-176">Создание переменной для виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="75ee4-176">Create a variable for the virtual network</span></span>
<span data-ttu-id="75ee4-177">Создайте переменную для готовой виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="75ee4-177">Create a variable for the completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName
```

### <a name="create-the-vm"></a><span data-ttu-id="75ee4-178">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="75ee4-178">Create the VM</span></span>
<span data-ttu-id="75ee4-179">Следующий сценарий PowerShell выполняет настройку виртуальных машин и использует неуправляемый образ виртуальной машины в качестве источника новой установки.</span><span class="sxs-lookup"><span data-stu-id="75ee4-179">The following PowerShell completes the virtual machine configurations and uses unmanaged image as the source for the new installation.</span></span>

</br>

```powershell
    # Enter a new user name and password to use as the local administrator account 
    # for remotely accessing the VM.
    $cred = Get-Credential

    # Name of the storage account where the VHD is located. This example sets the 
    # storage account name as "myStorageAccount"
    $storageAccName = "myStorageAccount"

    # Name of the virtual machine. This example sets the VM name as "myVM".
    $vmName = "myVM"

    # Size of the virtual machine. This example creates "Standard_D2_v2" sized VM. 
    # See the VM sizes documentation for more information: 
    # https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/
    $vmSize = "Standard_D2_v2"

    # Computer name for the VM. This examples sets the computer name as "myComputer".
    $computerName = "myComputer"

    # Name of the disk that holds the OS. This example sets the 
    # OS disk name as "myOsDisk"
    $osDiskName = "myOsDisk"

    # Assign a SKU name. This example sets the SKU name as "Standard_LRS"
    # Valid values for -SkuName are: Standard_LRS - locally redundant storage, Standard_ZRS - zone redundant
    # storage, Standard_GRS - geo redundant storage, Standard_RAGRS - read access geo redundant storage,
    # Premium_LRS - premium locally redundant storage. 
    $skuName = "Standard_LRS"

    # Get the storage account where the uploaded image is stored
    $storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $rgName -AccountName $storageAccName

    # Set the VM name and size
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

    #Set the Windows operating system configuration and add the NIC
    $vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

    # Create the OS disk URI
    $osDiskUri = '{0}vhds/{1}-{2}.vhd' `
        -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName

    # Configure the OS disk to be created from the existing VHD image (-CreateOption fromImage).
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri `
        -CreateOption fromImage -SourceImageUri $imageURI -Windows

    # Create the new VM
    New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

### <a name="verify-that-the-vm-was-created"></a><span data-ttu-id="75ee4-180">Проверка создания виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="75ee4-180">Verify that the VM was created</span></span>
<span data-ttu-id="75ee4-181">После завершения процесса новая виртуальная машина должна отображаться на [портале Azure](https://portal.azure.com) (выберите элементы **Обзор** > **Виртуальные машины**). Ее можно также увидеть, выполнив следующие команды PowerShell.</span><span class="sxs-lookup"><span data-stu-id="75ee4-181">When complete, you should see the newly created VM in the [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using the following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="75ee4-182">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="75ee4-182">Next steps</span></span>
<span data-ttu-id="75ee4-183">Сведения об управлении созданной виртуальной машиной с помощью Azure PowerShell см. в статье [Управление виртуальными машинами Azure с помощью Azure Resource Manager и PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="75ee4-183">To manage your new virtual machine with Azure PowerShell, see [Manage virtual machines using Azure Resource Manager and PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


