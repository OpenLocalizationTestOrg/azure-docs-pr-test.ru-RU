---
title: "aaaCreate изображение неуправляемые универсальной ВМ в Azure | Документы Microsoft"
description: "Создание образа неуправляемого обобщенный toocreate toouse виртуальной Машины Windows несколько копий виртуальной машины в Azure."
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
ms.openlocfilehash: b8a044d20313efa6dd9b9757e61154f922134476
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-unmanaged-vm-image-from-an-azure-vm"></a><span data-ttu-id="c3343-103">Как изображение toocreate неуправляемые виртуальной Машины из виртуальной Машины Azure</span><span class="sxs-lookup"><span data-stu-id="c3343-103">How toocreate an unmanaged VM image from an Azure VM</span></span>

<span data-ttu-id="c3343-104">В этой статье описывается использование учетных записей хранения.</span><span class="sxs-lookup"><span data-stu-id="c3343-104">This article covers using storage accounts.</span></span> <span data-ttu-id="c3343-105">Мы рекомендуем использовать управляемые диски и управляемые образы вместо учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="c3343-105">We recommend that you use managed disks and managed images instead of a storage account.</span></span> <span data-ttu-id="c3343-106">Дополнительные сведения см. в статье [Запись управляемого образа универсальной виртуальной машины в Azure](capture-image-resource.md).</span><span class="sxs-lookup"><span data-stu-id="c3343-106">For more information, see [Capture a managed image of a generalized VM in Azure](capture-image-resource.md).</span></span>

<span data-ttu-id="c3343-107">В этой статье показано, как Azure PowerShell toouse toocreate изображения универсальной ВМ Azure с помощью учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="c3343-107">This article shows you how toouse Azure PowerShell toocreate an image of a generalized Azure VM using a storage account.</span></span> <span data-ttu-id="c3343-108">Затем можно использовать образ toocreate hello другой виртуальной Машиной.</span><span class="sxs-lookup"><span data-stu-id="c3343-108">You can then use hello image toocreate another VM.</span></span> <span data-ttu-id="c3343-109">Hello образ содержит hello диска ОС и дисков данных hello, вложенные toohello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="c3343-109">hello image includes hello OS disk and hello data disks that are attached toohello virtual machine.</span></span> <span data-ttu-id="c3343-110">Hello изображение не содержит ресурсов hello виртуальной сети, поэтому требуется tooset эти ресурсы при создании hello новой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="c3343-110">hello image doesn't include hello virtual network resources, so you need tooset up those resources when you create hello new VM.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="c3343-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c3343-111">Prerequisites</span></span>
<span data-ttu-id="c3343-112">Необходима версия Azure PowerShell toohave 1.0.x или более новая версия.</span><span class="sxs-lookup"><span data-stu-id="c3343-112">You need toohave Azure PowerShell version 1.0.x or newer installed.</span></span> <span data-ttu-id="c3343-113">Если вы еще не установили PowerShell, прочтите [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) для действия по установке.</span><span class="sxs-lookup"><span data-stu-id="c3343-113">If you haven't already installed PowerShell, read [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for installation steps.</span></span>

## <a name="generalize-hello-vm"></a><span data-ttu-id="c3343-114">Обобщить hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="c3343-114">Generalize hello VM</span></span> 
<span data-ttu-id="c3343-115">В этом разделе показано, как toogeneralize вашей виртуальной машины Windows для использования в качестве образа.</span><span class="sxs-lookup"><span data-stu-id="c3343-115">This section shows you how toogeneralize your Windows virtual machine for use as an image.</span></span> <span data-ttu-id="c3343-116">Универсализация ВМ удаляет все ваши личные сведения, помимо прочего и подготавливает toobe машины hello, используемое в качестве изображения.</span><span class="sxs-lookup"><span data-stu-id="c3343-116">Generalizing a VM removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="c3343-117">Дополнительные сведения о программе Sysprep см. в разделе [как tooUse Sysprep: введение](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="c3343-117">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="c3343-118">Убедитесь, что на компьютере hello ролей сервера hello поддерживаются программой Sysprep.</span><span class="sxs-lookup"><span data-stu-id="c3343-118">Make sure hello server roles running on hello machine are supported by Sysprep.</span></span> <span data-ttu-id="c3343-119">Дополнительные сведения см. в статье [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles) (Поддержка серверных ролей в Sysprep).</span><span class="sxs-lookup"><span data-stu-id="c3343-119">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c3343-120">При отправке вашего tooAzure виртуального жесткого диска для hello первый раз, убедитесь, что у вас есть [подготовки ВМ](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) перед запуском Sysprep.</span><span class="sxs-lookup"><span data-stu-id="c3343-120">If you are uploading your VHD tooAzure for hello first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

<span data-ttu-id="c3343-121">Кроме того, можно обобщить ВМ Linux с помощью `sudo waagent -deprovision+user` , а затем используйте PowerShell toocapture hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="c3343-121">You can also generalize a Linux VM using `sudo waagent -deprovision+user` and then use PowerShell toocapture hello VM.</span></span> <span data-ttu-id="c3343-122">Сведения об использовании toocapture CLI hello виртуальной Машины см. в разделе [как toogeneralize и виртуальных машин Linux с помощью отслеживания hello Azure CLI ](../linux/capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="c3343-122">For information about using hello CLI toocapture a VM, see [How toogeneralize and capture a Linux virtual machine using hello Azure CLI ](../linux/capture-image.md).</span></span>


1. <span data-ttu-id="c3343-123">Войдите в систему toohello виртуальной машины Windows.</span><span class="sxs-lookup"><span data-stu-id="c3343-123">Sign in toohello Windows virtual machine.</span></span>
2. <span data-ttu-id="c3343-124">Привет открыть окно командной строки с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="c3343-124">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="c3343-125">Измените каталог hello слишком**%windir%\system32\sysprep**, а затем запустите `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="c3343-125">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="c3343-126">В hello **средство подготовки системы** выберите **Enter System Out-of-Box Experience (OOBE)**и убедитесь, что hello **Generalize** установлен флажок.</span><span class="sxs-lookup"><span data-stu-id="c3343-126">In hello **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that hello **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="c3343-127">В разделе **Параметры завершения работы** выберите **Завершение работы**.</span><span class="sxs-lookup"><span data-stu-id="c3343-127">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="c3343-128">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c3343-128">Click **OK**.</span></span>
   
    ![Запуск Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="c3343-130">По завершении работы программы Sysprep завершает hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="c3343-130">When Sysprep completes, it shuts down hello virtual machine.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="c3343-131">Не перезагружайте hello виртуальной Машины, пока не выполняется отправка tooAzure hello виртуального жесткого диска или создание образа из hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="c3343-131">Do not restart hello VM until you are done uploading hello VHD tooAzure or creating an image from hello VM.</span></span> <span data-ttu-id="c3343-132">Hello ВМ случайно возвращает перезапуска, запустите Sysprep toogeneralize его еще раз.</span><span class="sxs-lookup"><span data-stu-id="c3343-132">If hello VM accidentally gets restarted, run Sysprep toogeneralize it again.</span></span>
> 
> 

## <a name="log-in-tooazure-powershell"></a><span data-ttu-id="c3343-133">Войдите в tooAzure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c3343-133">Log in tooAzure PowerShell</span></span>
1. <span data-ttu-id="c3343-134">Откройте Azure PowerShell и войдите в tooyour учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="c3343-134">Open Azure PowerShell and sign in tooyour Azure account.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
   
    <span data-ttu-id="c3343-135">Откроется всплывающее окно учетные данные учетной записи Azure tooenter вы.</span><span class="sxs-lookup"><span data-stu-id="c3343-135">A pop-up window opens for you tooenter your Azure account credentials.</span></span>
2. <span data-ttu-id="c3343-136">Получите подписку hello идентификаторы для доступных подписок.</span><span class="sxs-lookup"><span data-stu-id="c3343-136">Get hello subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="c3343-137">Набор hello нужной подписки с идентификатором hello подписки.</span><span class="sxs-lookup"><span data-stu-id="c3343-137">Set hello correct subscription using hello subscription ID.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="deallocate-hello-vm-and-set-hello-state-toogeneralized"></a><span data-ttu-id="c3343-138">Выделение hello ВМ и установить состояние toogeneralized hello</span><span class="sxs-lookup"><span data-stu-id="c3343-138">Deallocate hello VM and set hello state toogeneralized</span></span>
1. <span data-ttu-id="c3343-139">Неудачная попытка освобождения ресурсов виртуальной Машины hello.</span><span class="sxs-lookup"><span data-stu-id="c3343-139">Deallocate hello VM resources.</span></span>
   
    ```powershell
    Stop-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName>
    ```
   
    <span data-ttu-id="c3343-140">Hello *состояние* для hello ВМ в hello Azure портал изменения из **остановлена** слишком**остановлена (освобождена)**.</span><span class="sxs-lookup"><span data-stu-id="c3343-140">hello *Status* for hello VM in hello Azure portal changes from **Stopped** too**Stopped (deallocated)**.</span></span>
2. <span data-ttu-id="c3343-141">Задать состояние hello hello виртуальной машины слишком**универсальная**.</span><span class="sxs-lookup"><span data-stu-id="c3343-141">Set hello status of hello virtual machine too**Generalized**.</span></span> 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName <resourceGroup> -Name <vmName> -Generalized
    ```
3. <span data-ttu-id="c3343-142">Проверьте состояние hello hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="c3343-142">Check hello status of hello VM.</span></span> <span data-ttu-id="c3343-143">Hello **OSState/универсальные** статьи для hello виртуальная машина должна иметь hello **DisplayStatus** значение слишком**ВМ обобщенный**.</span><span class="sxs-lookup"><span data-stu-id="c3343-143">hello **OSState/generalized** section for hello VM should have hello **DisplayStatus** set too**VM generalized**.</span></span>  
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName> -Status
    $vm.Statuses
    ```

## <a name="create-hello-image"></a><span data-ttu-id="c3343-144">Создание образа hello</span><span class="sxs-lookup"><span data-stu-id="c3343-144">Create hello image</span></span>

<span data-ttu-id="c3343-145">Создание образа неуправляемые виртуальной машины в hello конечный контейнер хранилища с помощью этой команды.</span><span class="sxs-lookup"><span data-stu-id="c3343-145">Create an unmanaged virtual machine image in hello destination storage container using this command.</span></span> <span data-ttu-id="c3343-146">Hello образу в hello же учетная запись хранения, как hello исходной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="c3343-146">hello image is created in hello same storage account as hello original virtual machine.</span></span> <span data-ttu-id="c3343-147">Hello `-Path` сохраняет копию шаблона JSON hello для hello исходной виртуальной Машины tooyour локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="c3343-147">hello `-Path` parameter saves a copy of hello JSON template for hello source VM tooyour local computer.</span></span> <span data-ttu-id="c3343-148">Hello `-DestinationContainerName` параметр является именем hello hello контейнера, что вы хотите, чтобы toohold изображения.</span><span class="sxs-lookup"><span data-stu-id="c3343-148">hello `-DestinationContainerName` parameter is hello name of hello container that you want toohold your images.</span></span> <span data-ttu-id="c3343-149">Если контейнер hello не существует, он создается автоматически.</span><span class="sxs-lookup"><span data-stu-id="c3343-149">If hello container doesn't exist, it is created for you.</span></span>
   
```powershell
Save-AzureRmVMImage -ResourceGroupName <resourceGroupName> -Name <vmName> `
    -DestinationContainerName <destinationContainerName> -VHDNamePrefix <templateNamePrefix> `
    -Path <C:\local\Filepath\Filename.json>
```
   
<span data-ttu-id="c3343-150">Hello URL-адрес изображения можно получить из шаблона файла JSON hello.</span><span class="sxs-lookup"><span data-stu-id="c3343-150">You can get hello URL of your image from hello JSON file template.</span></span> <span data-ttu-id="c3343-151">Go toohello **ресурсов** > **storageProfile** > **osDisk** > **изображение**  >  **uri** раздел для hello полный путь данного изображения.</span><span class="sxs-lookup"><span data-stu-id="c3343-151">Go toohello **resources** > **storageProfile** > **osDisk** > **image** > **uri** section for hello complete path of your image.</span></span> <span data-ttu-id="c3343-152">Hello URL-адрес изображения hello выглядит следующим образом: `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.</span><span class="sxs-lookup"><span data-stu-id="c3343-152">hello URL of hello image looks like: `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.</span></span>
   
<span data-ttu-id="c3343-153">Можно также проверить hello URI портала hello.</span><span class="sxs-lookup"><span data-stu-id="c3343-153">You can also verify hello URI in hello portal.</span></span> <span data-ttu-id="c3343-154">изображение Hello является скопированный tooa контейнер с именем **системы** вашей учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="c3343-154">hello image is copied tooa container named **system** in your storage account.</span></span> 

## <a name="create-a-vm-from-hello-image"></a><span data-ttu-id="c3343-155">Создание виртуальной Машины из образа hello</span><span class="sxs-lookup"><span data-stu-id="c3343-155">Create a VM from hello image</span></span>

<span data-ttu-id="c3343-156">Теперь можно создать один или несколько виртуальных машин из неуправляемого образа hello.</span><span class="sxs-lookup"><span data-stu-id="c3343-156">Now you can create one or more VMs from hello unmanaged image.</span></span>

### <a name="set-hello-uri-of-hello-vhd"></a><span data-ttu-id="c3343-157">Набор hello URI hello виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="c3343-157">Set hello URI of hello VHD</span></span>

<span data-ttu-id="c3343-158">Hello URI для hello toouse виртуальный жесткий ДИСК имеет формат hello: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span><span class="sxs-lookup"><span data-stu-id="c3343-158">hello URI for hello VHD toouse is in hello format: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span></span> <span data-ttu-id="c3343-159">В этом примере hello виртуального жесткого диска с именем **myVHD** в учетной записи хранения hello **mystorageaccount** в контейнере hello **mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="c3343-159">In this example hello VHD named **myVHD** is in hello storage account **mystorageaccount** in hello container **mycontainer**.</span></span>

```powershell
$imageURI = "https://mystorageaccount.blob.core.windows.net/mycontainer/myVhd.vhd"
```


### <a name="create-a-virtual-network"></a><span data-ttu-id="c3343-160">Создать виртуальную сеть</span><span class="sxs-lookup"><span data-stu-id="c3343-160">Create a virtual network</span></span>
<span data-ttu-id="c3343-161">Создание виртуальной сети hello и подсеть hello [виртуальной сети](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c3343-161">Create hello vNet and subnet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="c3343-162">Создайте подсеть hello.</span><span class="sxs-lookup"><span data-stu-id="c3343-162">Create hello subnet.</span></span> <span data-ttu-id="c3343-163">Hello следующий пример создает подсеть с именем **mySubnet** в группе ресурсов hello **myResourceGroup** с префикс адреса hello **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="c3343-163">hello following sample creates a subnet named **mySubnet** in hello resource group **myResourceGroup** with hello address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="c3343-164">Создайте виртуальную сеть hello.</span><span class="sxs-lookup"><span data-stu-id="c3343-164">Create hello virtual network.</span></span> <span data-ttu-id="c3343-165">Hello следующий пример создает виртуальную сеть с именем **myVnet** в hello **Запад США** места, где префикс адреса hello **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="c3343-165">hello following sample creates a virtual network named **myVnet** in hello **West US** location with hello address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="c3343-166">Создание общедоступного IP-адреса и сетевого интерфейса</span><span class="sxs-lookup"><span data-stu-id="c3343-166">Create a public IP address and network interface</span></span>
<span data-ttu-id="c3343-167">требуется tooenable взаимодействия с виртуальной машиной hello в виртуальной сети hello, [общедоступный IP-адрес](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) и сетевого интерфейса.</span><span class="sxs-lookup"><span data-stu-id="c3343-167">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="c3343-168">Создание общедоступного IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="c3343-168">Create a public IP address.</span></span> <span data-ttu-id="c3343-169">В этом примере создается общедоступный IP-адрес с именем **myPip**.</span><span class="sxs-lookup"><span data-stu-id="c3343-169">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="c3343-170">Создайте сетевую карту hello.</span><span class="sxs-lookup"><span data-stu-id="c3343-170">Create hello NIC.</span></span> <span data-ttu-id="c3343-171">В этом примере создается сетевая карта с именем **myNic**.</span><span class="sxs-lookup"><span data-stu-id="c3343-171">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="c3343-172">Создание группы безопасности сети hello и правило протокола удаленного рабочего СТОЛА</span><span class="sxs-lookup"><span data-stu-id="c3343-172">Create hello network security group and an RDP rule</span></span>
<span data-ttu-id="c3343-173">возможности toolog toobe в tooyour виртуальную Машину с помощью протокола удаленного рабочего СТОЛА, необходимо toohave правило безопасности, которое разрешает RDP-доступ через порт 3389.</span><span class="sxs-lookup"><span data-stu-id="c3343-173">toobe able toolog in tooyour VM using RDP, you need toohave a security rule that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="c3343-174">В этом примере создается группа безопасности сети с именем **myNsg**, которая содержит правило с именем **myRdpRule**, разрешающее трафик RDP через порт 3389.</span><span class="sxs-lookup"><span data-stu-id="c3343-174">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="c3343-175">Дополнительные сведения о Nsg см. в разделе [Открытие портов tooa ВМ в Azure с помощью PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c3343-175">For more information about NSGs, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


### <a name="create-a-variable-for-hello-virtual-network"></a><span data-ttu-id="c3343-176">Создайте переменную для hello виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="c3343-176">Create a variable for hello virtual network</span></span>
<span data-ttu-id="c3343-177">Создайте переменную для завершения hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="c3343-177">Create a variable for hello completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName
```

### <a name="create-hello-vm"></a><span data-ttu-id="c3343-178">Создание виртуальной Машины hello</span><span class="sxs-lookup"><span data-stu-id="c3343-178">Create hello VM</span></span>
<span data-ttu-id="c3343-179">Hello следующие команды PowerShell завершает hello конфигураций виртуальных машин и использует неуправляемые изображения в качестве hello источника для новой установки hello.</span><span class="sxs-lookup"><span data-stu-id="c3343-179">hello following PowerShell completes hello virtual machine configurations and uses unmanaged image as hello source for hello new installation.</span></span>

</br>

```powershell
    # Enter a new user name and password toouse as hello local administrator account 
    # for remotely accessing hello VM.
    $cred = Get-Credential

    # Name of hello storage account where hello VHD is located. This example sets hello 
    # storage account name as "myStorageAccount"
    $storageAccName = "myStorageAccount"

    # Name of hello virtual machine. This example sets hello VM name as "myVM".
    $vmName = "myVM"

    # Size of hello virtual machine. This example creates "Standard_D2_v2" sized VM. 
    # See hello VM sizes documentation for more information: 
    # https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/
    $vmSize = "Standard_D2_v2"

    # Computer name for hello VM. This examples sets hello computer name as "myComputer".
    $computerName = "myComputer"

    # Name of hello disk that holds hello OS. This example sets hello 
    # OS disk name as "myOsDisk"
    $osDiskName = "myOsDisk"

    # Assign a SKU name. This example sets hello SKU name as "Standard_LRS"
    # Valid values for -SkuName are: Standard_LRS - locally redundant storage, Standard_ZRS - zone redundant
    # storage, Standard_GRS - geo redundant storage, Standard_RAGRS - read access geo redundant storage,
    # Premium_LRS - premium locally redundant storage. 
    $skuName = "Standard_LRS"

    # Get hello storage account where hello uploaded image is stored
    $storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $rgName -AccountName $storageAccName

    # Set hello VM name and size
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

    #Set hello Windows operating system configuration and add hello NIC
    $vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

    # Create hello OS disk URI
    $osDiskUri = '{0}vhds/{1}-{2}.vhd' `
        -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName

    # Configure hello OS disk toobe created from hello existing VHD image (-CreateOption fromImage).
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri `
        -CreateOption fromImage -SourceImageUri $imageURI -Windows

    # Create hello new VM
    New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

### <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="c3343-180">Убедитесь, что hello создания виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="c3343-180">Verify that hello VM was created</span></span>
<span data-ttu-id="c3343-181">По завершении вы увидите только что созданный виртуальной Машины в hello hello [портал Azure](https://portal.azure.com) под **Обзор** > **виртуальные машины**, или с помощью следующих hello Команды PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c3343-181">When complete, you should see hello newly created VM in hello [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="c3343-182">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c3343-182">Next steps</span></span>
<span data-ttu-id="c3343-183">см. на новую виртуальную машину с помощью Azure PowerShell toomanage [управление виртуальными машинами с помощью диспетчера ресурсов Azure и PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c3343-183">toomanage your new virtual machine with Azure PowerShell, see [Manage virtual machines using Azure Resource Manager and PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


