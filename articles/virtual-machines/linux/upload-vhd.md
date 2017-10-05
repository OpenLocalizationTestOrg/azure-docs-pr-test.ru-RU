---
title: "Передача или копирование настраиваемой виртуальной машины Linux с помощью Azure CLI 2.0 | Документация Майкрософт"
description: "Передача или копирование настраиваемой виртуальной машины, используя модель развертывания Resource Manager и Azure CLI 2.0."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a8c7818f-eb65-409e-aa91-ce5ae975c564
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 07/06/2017
ms.author: cynthn
ms.openlocfilehash: 7c297725c26ea6c44403a10ecdcc3542f89f10b4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-linux-vm-from-custom-disk-with-the-azure-cli-20"></a><span data-ttu-id="40423-103">Создание виртуальной машины Linux на основе настраиваемого диска с помощью Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="40423-103">Create a Linux VM from custom disk with the Azure CLI 2.0</span></span>

<!-- rename to create-vm-specialized -->

<span data-ttu-id="40423-104">В этой статье показано, как передать настраиваемый виртуальный жесткий диск (VHD) или скопировать имеющейся VHD в Azure и создавать на основе настраиваемого диска виртуальные машины Linux.</span><span class="sxs-lookup"><span data-stu-id="40423-104">This article shows you how to upload a customized virtual hard disk (VHD) or copy a an existing VHD in Azure and create new Linux virtual machines (VMs) from the custom disk.</span></span> <span data-ttu-id="40423-105">Вы можете установить и настроить дистрибутив Linux в соответствии с требованиями, а затем использовать этот VHD для быстрого создания виртуальной машины Azure.</span><span class="sxs-lookup"><span data-stu-id="40423-105">You can install and configure a Linux distro to your requirements and then use that VHD to quickly create a new Azure virtual machine.</span></span>

<span data-ttu-id="40423-106">Если необходимо создать несколько виртуальных машин на основе настраиваемого диска, создайте образ на основе виртуальной машины или VHD.</span><span class="sxs-lookup"><span data-stu-id="40423-106">If you want to create multiple VMs from your customized disk, you should create an image from your VM or VHD.</span></span> <span data-ttu-id="40423-107">Дополнительные сведения см. в статье [Создание пользовательского образа виртуальной машины Azure с помощью интерфейса командной строки](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="40423-107">For more information, see [Create a custom image of an Azure VM using the CLI](tutorial-custom-images.md).</span></span>

<span data-ttu-id="40423-108">Существует два варианта.</span><span class="sxs-lookup"><span data-stu-id="40423-108">You have two options:</span></span>
* [<span data-ttu-id="40423-109">Передача VHD</span><span class="sxs-lookup"><span data-stu-id="40423-109">Upload a VHD</span></span>](#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="40423-110">Копирование имеющейся виртуальной машины Azure</span><span class="sxs-lookup"><span data-stu-id="40423-110">Copy an existing Azure VM</span></span>](#option-2-copy-an-existing-azure-vm)

## <a name="quick-commands"></a><span data-ttu-id="40423-111">Быстрые команды</span><span class="sxs-lookup"><span data-stu-id="40423-111">Quick commands</span></span>

<span data-ttu-id="40423-112">При создании виртуальной машины, используя команду [az vm create](/cli/azure/vm#create), на основе настраиваемого или специализированного диска, вы **подключаете** диск (--attach-os-disk), вместо того чтобы указать настраиваемый образ или образ Marketplace (--image).</span><span class="sxs-lookup"><span data-stu-id="40423-112">When creating a new VM using [az vm create](/cli/azure/vm#create) from a customized or specialized disk you **attach** the disk (--attach-os-disk) instead of specifying a custom or marketplace image (--image).</span></span> <span data-ttu-id="40423-113">В следующем примере создается виртуальная машина с именем *myVM* на основе управляемого диска *myManagedDisk*, созданного из настраиваемого VHD.</span><span class="sxs-lookup"><span data-stu-id="40423-113">The following example creates a VM named *myVM* using the managed disk named *myManagedDisk* created from your customized VHD:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location eastus --name myVM \
   --os-type linux --attach-os-disk myManagedDisk
```

## <a name="requirements"></a><span data-ttu-id="40423-114">Требования</span><span class="sxs-lookup"><span data-stu-id="40423-114">Requirements</span></span>
<span data-ttu-id="40423-115">Чтобы выполнить приведенные ниже действия, требуется:</span><span class="sxs-lookup"><span data-stu-id="40423-115">To complete the following steps, you need:</span></span>

* <span data-ttu-id="40423-116">Виртуальная машина Linux, которая была подготовлена для использования в Azure.</span><span class="sxs-lookup"><span data-stu-id="40423-116">A Linux virtual machine that has been prepared for use in Azure.</span></span> <span data-ttu-id="40423-117">Раздел [Подготовка виртуальной машины](#prepare-the-vm) этой статьи содержит сведения о том, как найти информацию для конкретного дистрибутива касательно установки агента Linux для Azure (waagent), необходимого для правильной работы виртуальной машины в Azure, и сведения о том, как к ней подключиться по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="40423-117">The [Prepare the VM](#prepare-the-vm) section of this article covers how to find distro specific information on installing the Azure Linux Agent (waagent) which is required for the VM to work properly in Azure and for you to be able to connect to it using SSH.</span></span>
* <span data-ttu-id="40423-118">VHD-файл на основе имеющегося [рекомендуемого для Azure дистрибутива Linux](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (или см. [сведения о нерекомендованных дистрибутивах](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) на виртуальном диске в формате VHD.</span><span class="sxs-lookup"><span data-stu-id="40423-118">The VHD file from an existing [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) to a virtual disk in the VHD format.</span></span> <span data-ttu-id="40423-119">Для создания VHD-файлов существует несколько средств.</span><span class="sxs-lookup"><span data-stu-id="40423-119">Multiple tools exist to create a VM and VHD:</span></span>
  * <span data-ttu-id="40423-120">Установите и настройте [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) или [KVM](http://www.linux-kvm.org/page/RunningKVM), используя VHD в качестве формата образа.</span><span class="sxs-lookup"><span data-stu-id="40423-120">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care to use VHD as your image format.</span></span> <span data-ttu-id="40423-121">При необходимости вы можете [преобразовать образ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) с помощью команды **qemu-img convert**.</span><span class="sxs-lookup"><span data-stu-id="40423-121">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using **qemu-img convert**.</span></span>
  * <span data-ttu-id="40423-122">Кроме того, можно использовать Hyper-V [в Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) или [Windows Server 2012 и 2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="40423-122">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="40423-123">Более новый формат VHDX не поддерживается в Azure.</span><span class="sxs-lookup"><span data-stu-id="40423-123">The newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="40423-124">При создании виртуальной машины укажите формат VHD.</span><span class="sxs-lookup"><span data-stu-id="40423-124">When you create a VM, specify VHD as the format.</span></span> <span data-ttu-id="40423-125">При необходимости можно преобразовать диски VHDX в диски VHD с помощью команды [qemu-img convert](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) или командлета PowerShell [Convert-VHD](https://technet.microsoft.com/library/hh848454.aspx).</span><span class="sxs-lookup"><span data-stu-id="40423-125">If needed, you can convert VHDX disks to VHD using [qemu-img convert](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or the [Convert-VHD](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="40423-126">Кроме того, Azure не поддерживает отправку динамических дисков VHD, поэтому перед отправкой необходимо преобразовать такие диски в статические диски VHD.</span><span class="sxs-lookup"><span data-stu-id="40423-126">Further, Azure does not support uploading dynamic VHDs, so you need to convert such disks to static VHDs before uploading.</span></span> <span data-ttu-id="40423-127">Для преобразования динамических дисков во время передачи в Azure можно использовать [служебные программы Azure VHD для GO](https://github.com/Microsoft/azure-vhd-utils-for-go) .</span><span class="sxs-lookup"><span data-stu-id="40423-127">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) to convert dynamic disks during the process of uploading to Azure.</span></span>
> 
> 


* <span data-ttu-id="40423-128">Обязательно установите последнюю версию [Azure CLI 2.0](/cli/azure/install-az-cli2) и войдите в учетную запись Azure с помощью команды [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="40423-128">Make sure that you have the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="40423-129">В следующих примерах замените имена параметров собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="40423-129">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="40423-130">Примеры имен параметров: *myResourceGroup*, *mystorageaccount* и *mydisks*.</span><span class="sxs-lookup"><span data-stu-id="40423-130">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *mydisks*.</span></span>

<span data-ttu-id="40423-131"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="40423-131"><a id="prepimage"> </a></span></span>

## <a name="prepare-the-vm"></a><span data-ttu-id="40423-132">Подготовка виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="40423-132">Prepare the VM</span></span>

<span data-ttu-id="40423-133">Azure поддерживает различные дистрибутивы Linux (см. раздел [Рекомендованные дистрибутивы](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="40423-133">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="40423-134">В следующих статьях описывается подготовка различных дистрибутивов Linux, которые поддерживаются в Azure.</span><span class="sxs-lookup"><span data-stu-id="40423-134">The following articles guide you through how to prepare the various Linux distributions that are supported on Azure:</span></span>

* [<span data-ttu-id="40423-135">Подготовка виртуальной машины на основе CentOS для Azure</span><span class="sxs-lookup"><span data-stu-id="40423-135">CentOS-based Distributions</span></span>](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="40423-136">Подготовка виртуального жесткого диска Debian для Azure</span><span class="sxs-lookup"><span data-stu-id="40423-136">Debian Linux</span></span>](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="40423-137">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="40423-137">Oracle Linux</span></span>](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="40423-138">Подготовка виртуальной машины на основе Red Hat для Azure</span><span class="sxs-lookup"><span data-stu-id="40423-138">Red Hat Enterprise Linux</span></span>](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="40423-139">Подготовка виртуальной машины SLES или openSUSE для Azure</span><span class="sxs-lookup"><span data-stu-id="40423-139">SLES & openSUSE</span></span>](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="40423-140">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="40423-140">Ubuntu</span></span>](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="40423-141">Информация о нерекомендованных дистрибутивах</span><span class="sxs-lookup"><span data-stu-id="40423-141">Other - Non-Endorsed Distributions</span></span>](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

<span data-ttu-id="40423-142">Другие общие советы по подготовке образов Linux для Azure см. в разделе [Общие замечания по установке Linux](create-upload-generic.md#general-linux-installation-notes).</span><span class="sxs-lookup"><span data-stu-id="40423-142">Also see the [Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="40423-143">[Соглашение об уровне обслуживания платформы Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/) применяется к виртуальным машинам, работающим под управлением Linux, только в том случае, если используется один из рекомендуемых дистрибутивов из раздела "Поддерживаемые версии" статьи [Linux в Azure — рекомендованные дистрибутивы](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) с заданными параметрами конфигурации.</span><span class="sxs-lookup"><span data-stu-id="40423-143">The [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies to VMs running Linux only when one of the endorsed distributions is used with the configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

## <a name="option-1-upload-a-vhd"></a><span data-ttu-id="40423-144">Вариант 1. Передача VHD</span><span class="sxs-lookup"><span data-stu-id="40423-144">Option 1: Upload a VHD</span></span>

<span data-ttu-id="40423-145">Вы можете передать настраиваемый VHD, выполняемый на локальном компьютере или который вы экспортировали из другого облака.</span><span class="sxs-lookup"><span data-stu-id="40423-145">You can upload a customized VHD that you have running on a local machine or that you exported from another cloud.</span></span> <span data-ttu-id="40423-146">Чтобы создать виртуальную машину Azure с помощью VHD, необходимо передать VHD в учетную запись хранения и создать управляемый диск на основе VHD.</span><span class="sxs-lookup"><span data-stu-id="40423-146">To use the VHD to create a new Azure VM, you need to upload the VHD to a storage account and create a managed disk from the VHD.</span></span> 

### <a name="create-a-resource-group"></a><span data-ttu-id="40423-147">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="40423-147">Create a resource group</span></span>

<span data-ttu-id="40423-148">Перед отправкой пользовательского диска и созданием виртуальных машин необходимо создать группу ресурсов с помощью команды [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="40423-148">Before uploading your custom disk and creating VMs, you first need to create a resource group with [az group create](/cli/azure/group#create).</span></span>

<span data-ttu-id="40423-149">В указанном ниже примере создается группа ресурсов с именем *myResourceGroup* в расположении *eastus*. [Обзор управляемых дисков Azure](../windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="40423-149">The following example creates a resource group named *myResourceGroup* in the *eastus* location: [Azure Managed Disks overview](../windows/managed-disks-overview.md)</span></span>
```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

### <a name="create-a-storage-account"></a><span data-ttu-id="40423-150">Создайте учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="40423-150">Create a storage account</span></span>

<span data-ttu-id="40423-151">Создайте учетную запись хранения для пользовательского диска и виртуальных машин с помощью команды [az storage account create](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="40423-151">Create a storage account for your custom disk and VMs with [az storage account create](/cli/azure/storage/account#create).</span></span> 

<span data-ttu-id="40423-152">В следующем примере создается учетная запись хранения с именем *mystorageaccount* в ранее созданной группе ресурсов:</span><span class="sxs-lookup"><span data-stu-id="40423-152">The following example creates a storage account named *mystorageaccount* in the resource group previously created:</span></span>

```azurecli
az storage account create \
    --resource-group myResourceGroup \
    --location eastus \
    --name mystorageaccount \
    --kind Storage \
    --sku Standard_LRS
```

### <a name="list-storage-account-keys"></a><span data-ttu-id="40423-153">Вывод списка ключей учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="40423-153">List storage account keys</span></span>
<span data-ttu-id="40423-154">Azure создает два 512-разрядных ключа доступа для каждой учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="40423-154">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="40423-155">Эти ключи используются при проверке подлинности в учетной записи хранения, например, для выполнения операций записи.</span><span class="sxs-lookup"><span data-stu-id="40423-155">These access keys are used when authenticating to the storage account, like carrying out write operations.</span></span> <span data-ttu-id="40423-156">Узнайте больше об управлении доступом к хранилищу [здесь](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="40423-156">Read more about [managing access to storage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="40423-157">Просмотрите список ключей доступа с помощью команды [az storage account keys list](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="40423-157">You view the access keys with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span>

<span data-ttu-id="40423-158">Просмотрите ключи доступа для созданной учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="40423-158">View the access keys for the storage account you created:</span></span>

```azurecli
az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount
```

<span data-ttu-id="40423-159">Выходные данные должны быть следующего вида.</span><span class="sxs-lookup"><span data-stu-id="40423-159">The output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK
```
<span data-ttu-id="40423-160">Запишите значение **key1**, так как оно будет использоваться для работы с учетной записью хранения на следующих шагах.</span><span class="sxs-lookup"><span data-stu-id="40423-160">Make a note of **key1** as you will use it to interact with your storage account in the next steps.</span></span>

### <a name="create-a-storage-container"></a><span data-ttu-id="40423-161">Создание контейнера хранилища</span><span class="sxs-lookup"><span data-stu-id="40423-161">Create a storage container</span></span>
<span data-ttu-id="40423-162">Точно так же, как вы создаете различные каталоги для логической организации локальной файловой системы, вы создаете контейнеры в учетной записи хранения, чтобы упорядочить диски.</span><span class="sxs-lookup"><span data-stu-id="40423-162">In the same way that you create different directories to logically organize your local file system, you create containers within a storage account to organize your disks.</span></span> <span data-ttu-id="40423-163">Учетная запись хранения может содержать любое количество контейнеров.</span><span class="sxs-lookup"><span data-stu-id="40423-163">A storage account can contain any number of containers.</span></span> <span data-ttu-id="40423-164">Создайте контейнер с помощью команды [az storage container create](/cli/azure/storage/container#create).</span><span class="sxs-lookup"><span data-stu-id="40423-164">Create a container with [az storage container create](/cli/azure/storage/container#create).</span></span>

<span data-ttu-id="40423-165">В следующем примере создается контейнер с именем *mydisks*.</span><span class="sxs-lookup"><span data-stu-id="40423-165">The following example creates a container named *mydisks*:</span></span>

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

### <a name="upload-the-vhd"></a><span data-ttu-id="40423-166">Отправка виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="40423-166">Upload the VHD</span></span>
<span data-ttu-id="40423-167">Теперь передайте пользовательский диск с помощью команды [az storage blob upload](/cli/azure/storage/blob#upload).</span><span class="sxs-lookup"><span data-stu-id="40423-167">Now upload your custom disk with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="40423-168">Пользовательский диск передается и хранится как страничный BLOB-объект.</span><span class="sxs-lookup"><span data-stu-id="40423-168">You upload and store your custom disk as a page blob.</span></span>

<span data-ttu-id="40423-169">Укажите ключ доступа, созданный на предыдущем шаге контейнер и путь к пользовательскому диску на локальном компьютере:</span><span class="sxs-lookup"><span data-stu-id="40423-169">Specify your access key, the container you created in the previous step, and then the path to the custom disk on your local computer:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 \
    --container-name mydisks \
    --type page \
    --file /path/to/disk/mydisk.vhd \
    --name myDisk.vhd
```
<span data-ttu-id="40423-170">Передача VHD может занять некоторое время.</span><span class="sxs-lookup"><span data-stu-id="40423-170">Uploading the VHD may take a while.</span></span>

### <a name="create-a-managed-disk"></a><span data-ttu-id="40423-171">Создание управляемого диска</span><span class="sxs-lookup"><span data-stu-id="40423-171">Create a managed disk</span></span>


<span data-ttu-id="40423-172">Создайте управляемый диск из VHD, выполнив команду [az disk create](/cli/azure/disk#create).</span><span class="sxs-lookup"><span data-stu-id="40423-172">Create a managed disk from the VHD using [az disk create](/cli/azure/disk#create).</span></span> <span data-ttu-id="40423-173">В следующем примере создается управляемый диск с именем *myManagedDisk* из виртуального жесткого диска, переданного в учетную запись хранения и сохраненного в контейнере:</span><span class="sxs-lookup"><span data-stu-id="40423-173">The following example creates a managed disk named *myManagedDisk* from the VHD you uploaded to your named storage account and container:</span></span>

```azurecli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
  --source https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd
```
## <a name="option-2-copy-an-existing-vm"></a><span data-ttu-id="40423-174">Вариант 2. Копирование имеющейся виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="40423-174">Option 2: Copy an existing VM</span></span>

<span data-ttu-id="40423-175">Вы также можете создать настраиваемую виртуальную машину в Azure, а затем скопировать диск операционной системы и подключить его к новой виртуальной машине для создания другой копии.</span><span class="sxs-lookup"><span data-stu-id="40423-175">You can also create the customized VM in Azure and then copy the OS disk and attach it to a new VM to create another copy.</span></span> <span data-ttu-id="40423-176">Это нормально для тестирования, однако если вы хотите использовать имеющуюся виртуальную машину Azure в качестве модели для нескольких новых виртуальных машин, вместе этого вам необходимо будет создать **образ**.</span><span class="sxs-lookup"><span data-stu-id="40423-176">This is fine for testing, but if you want to use an existing Azure VM as the model for multiple new VMs, you really should create an **image** instead.</span></span> <span data-ttu-id="40423-177">Дополнительные сведения о создании образа на основе имеющейся виртуальной машины Azure см. в статье [Создание пользовательского образа виртуальной машины Azure с помощью интерфейса командной строки](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="40423-177">For more information about creating an image from an existing Azure VM, see [Create a custom image of an Azure VM using the CLI](tutorial-custom-images.md)</span></span>

### <a name="create-a-snapshot"></a><span data-ttu-id="40423-178">Создание моментального снимка</span><span class="sxs-lookup"><span data-stu-id="40423-178">Create a snapshot</span></span>

<span data-ttu-id="40423-179">В этом примере создается моментальный снимок виртуальной машины с именем *myVM* в группе ресурсов *myResourceGroup*, а также моментальный снимок с именем *osDiskSnapshot*.</span><span class="sxs-lookup"><span data-stu-id="40423-179">This example creates a snapshot of a VM named *myVM* in resource group *myResourceGroup* and creates a snapshot named *osDiskSnapshot*.</span></span>

```azure-cli
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create \
    -g myResourceGroup \
    --source "$osDiskId" \
    --name osDiskSnapshot
```
###  <a name="create-the-managed-disk"></a><span data-ttu-id="40423-180">Создание управляемого диска</span><span class="sxs-lookup"><span data-stu-id="40423-180">Create the managed disk</span></span>

<span data-ttu-id="40423-181">Создайте управляемый диск из моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="40423-181">Create a new managed disk from the snapshot.</span></span>

<span data-ttu-id="40423-182">Получите идентификатор моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="40423-182">Get the ID of the snapshot.</span></span> <span data-ttu-id="40423-183">В этом примере используется моментальный снимок с именем *osDiskSnapshot*, который находится в группе ресурсов *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="40423-183">In this example, the snapshot is named *osDiskSnapshot* and it is in the *myResourceGroup* resource group.</span></span>

```azure-cli
snapshotId=$(az snapshot show --name osDiskSnapshot --resource-group myResourceGroup --query [id] -o tsv)
```

<span data-ttu-id="40423-184">Создайте управляемый диск.</span><span class="sxs-lookup"><span data-stu-id="40423-184">Create the managed disk.</span></span> <span data-ttu-id="40423-185">В этом примере мы создадим управляемый диск с именем *myManagedDisk* на основе моментального снимка размером в 128 ГБ, который хранится в хранилище уровня "Стандартный".</span><span class="sxs-lookup"><span data-stu-id="40423-185">In this example, we will create a managed disk named *myManagedDisk* from our snapshot, that is 128GB in size in standard storage.</span></span>

```azure-cli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
    --sku Standard_LRS \
    --size-gb 128 \
    --source $snapshotId
```

## <a name="create-the-vm"></a><span data-ttu-id="40423-186">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="40423-186">Create the VM</span></span>

<span data-ttu-id="40423-187">Теперь создайте виртуальную машину, выполнив команду [az vm create](/cli/azure/vm#create), и подключите (--attach-os-disk) управляемый диск как диск операционной системы.</span><span class="sxs-lookup"><span data-stu-id="40423-187">Now, create your VM with [az vm create](/cli/azure/vm#create) and attach (--attach-os-disk) the managed disk as the OS disk.</span></span> <span data-ttu-id="40423-188">В следующем примере создается виртуальная машина с именем *myNewVM* на основе управляемого диска, созданного из отправленного ранее виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="40423-188">The following example creates a VM named *myNewVM* using the managed disk created from your uploaded VHD:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNewVM \
    --os-type linux \
    --attach-os-disk myManagedDisk
```

<span data-ttu-id="40423-189">Вы должны иметь возможность подключиться к виртуальной машине по протоколу SSH, используя учетные данные исходной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="40423-189">You should be able to SSH into the VM using the credentials from the source VM.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="40423-190">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="40423-190">Next steps</span></span>
<span data-ttu-id="40423-191">После подготовки и передачи пользовательского виртуального диска ознакомьтесь с дополнительными сведениями об [использовании Resource Manager и шаблонов](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="40423-191">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="40423-192">Возможно, вам также потребуется [добавить диск данных](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) для новых виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="40423-192">You may also want to [add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to your new VMs.</span></span> <span data-ttu-id="40423-193">Если на виртуальных машинах запущены приложения, к которым необходим доступ, [откройте порты и конечные точки](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="40423-193">If you have applications running on your VMs that you need to access, be sure to [open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

