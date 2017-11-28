---
title: "копирования пользовательских виртуальной Машины Linux с помощью Azure CLI 2.0 или aaaUpload | Документы Microsoft"
description: "Загрузки или копирования настраиваемую виртуальную машину с помощью модели развертывания диспетчера ресурсов hello и hello Azure CLI 2.0"
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
ms.openlocfilehash: 79af897120a6ba7f4a427ba6c7d0c31b7b870bd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-vm-from-custom-disk-with-hello-azure-cli-20"></a><span data-ttu-id="62b26-103">Создайте виртуальную Машину Linux из пользовательского диска с hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="62b26-103">Create a Linux VM from custom disk with hello Azure CLI 2.0</span></span>

<!-- rename toocreate-vm-specialized -->

<span data-ttu-id="62b26-104">В этой статье показано, как tooupload настроенного виртуального жесткого диска (VHD) или скопировать существующий VHD в Azure и создания новых виртуальных машин Linux (ВМ) с hello пользовательского диска.</span><span class="sxs-lookup"><span data-stu-id="62b26-104">This article shows you how tooupload a customized virtual hard disk (VHD) or copy a an existing VHD in Azure and create new Linux virtual machines (VMs) from hello custom disk.</span></span> <span data-ttu-id="62b26-105">Можно установить и настроить требования tooyour дистрибутив Linux и затем использовать этот ДИСК tooquickly создания новой виртуальной машины Azure.</span><span class="sxs-lookup"><span data-stu-id="62b26-105">You can install and configure a Linux distro tooyour requirements and then use that VHD tooquickly create a new Azure virtual machine.</span></span>

<span data-ttu-id="62b26-106">Следует toocreate несколько виртуальных машин с настроенные диска следует создать образ виртуальной Машины или виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="62b26-106">If you want toocreate multiple VMs from your customized disk, you should create an image from your VM or VHD.</span></span> <span data-ttu-id="62b26-107">Дополнительные сведения см. в разделе [создать образ виртуальной машины Azure с помощью hello CLI](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="62b26-107">For more information, see [Create a custom image of an Azure VM using hello CLI](tutorial-custom-images.md).</span></span>

<span data-ttu-id="62b26-108">Существует два варианта.</span><span class="sxs-lookup"><span data-stu-id="62b26-108">You have two options:</span></span>
* [<span data-ttu-id="62b26-109">Передача VHD</span><span class="sxs-lookup"><span data-stu-id="62b26-109">Upload a VHD</span></span>](#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="62b26-110">Копирование имеющейся виртуальной машины Azure</span><span class="sxs-lookup"><span data-stu-id="62b26-110">Copy an existing Azure VM</span></span>](#option-2-copy-an-existing-azure-vm)

## <a name="quick-commands"></a><span data-ttu-id="62b26-111">Быстрые команды</span><span class="sxs-lookup"><span data-stu-id="62b26-111">Quick commands</span></span>

<span data-ttu-id="62b26-112">При создании новой виртуальной Машины с помощью [создания виртуальной машины az](/cli/azure/vm#create) с специальную или специализированного диска вы **присоединения** hello диска (--присоединить os диск) вместо указания нестандартной проверки подлинности или marketplace изображения (--изображения).</span><span class="sxs-lookup"><span data-stu-id="62b26-112">When creating a new VM using [az vm create](/cli/azure/vm#create) from a customized or specialized disk you **attach** hello disk (--attach-os-disk) instead of specifying a custom or marketplace image (--image).</span></span> <span data-ttu-id="62b26-113">Hello следующий пример создает Виртуальную машину с именем *myVM* с помощью hello управляемого диска с именем *myManagedDisk* создан из вашего настроенного виртуального жесткого диска:</span><span class="sxs-lookup"><span data-stu-id="62b26-113">hello following example creates a VM named *myVM* using hello managed disk named *myManagedDisk* created from your customized VHD:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location eastus --name myVM \
   --os-type linux --attach-os-disk myManagedDisk
```

## <a name="requirements"></a><span data-ttu-id="62b26-114">Требования</span><span class="sxs-lookup"><span data-stu-id="62b26-114">Requirements</span></span>
<span data-ttu-id="62b26-115">toocomplete hello следующие действия, необходимо:</span><span class="sxs-lookup"><span data-stu-id="62b26-115">toocomplete hello following steps, you need:</span></span>

* <span data-ttu-id="62b26-116">Виртуальная машина Linux, которая была подготовлена для использования в Azure.</span><span class="sxs-lookup"><span data-stu-id="62b26-116">A Linux virtual machine that has been prepared for use in Azure.</span></span> <span data-ttu-id="62b26-117">Hello [hello подготовки виртуальной Машины](#prepare-the-vm) данной статьи рассматриваются как toofind дистрибутив определенные сведения об установке hello Azure Linux Agent (waagent) необходимый для toowork ВМ hello должным образом в Azure и вы toobe может tooconnect tooit с помощью SSH.</span><span class="sxs-lookup"><span data-stu-id="62b26-117">hello [Prepare hello VM](#prepare-the-vm) section of this article covers how toofind distro specific information on installing hello Azure Linux Agent (waagent) which is required for hello VM toowork properly in Azure and for you toobe able tooconnect tooit using SSH.</span></span>
* <span data-ttu-id="62b26-118">Hello VHD-файл из существующего [дистрибутив Linux в одобренных Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (или в разделе [сведения для распределений, отличных от одобренных](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa виртуальный диск в формате VHD hello.</span><span class="sxs-lookup"><span data-stu-id="62b26-118">hello VHD file from an existing [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtual disk in hello VHD format.</span></span> <span data-ttu-id="62b26-119">Несколько средств существует toocreate виртуальной Машины и виртуального жесткого диска:</span><span class="sxs-lookup"><span data-stu-id="62b26-119">Multiple tools exist toocreate a VM and VHD:</span></span>
  * <span data-ttu-id="62b26-120">Установка и настройка [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) или [KVM](http://www.linux-kvm.org/page/RunningKVM), отвечающий за toouse виртуальный жесткий ДИСК в формате изображения.</span><span class="sxs-lookup"><span data-stu-id="62b26-120">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care toouse VHD as your image format.</span></span> <span data-ttu-id="62b26-121">При необходимости вы можете [преобразовать образ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) с помощью команды **qemu-img convert**.</span><span class="sxs-lookup"><span data-stu-id="62b26-121">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using **qemu-img convert**.</span></span>
  * <span data-ttu-id="62b26-122">Кроме того, можно использовать Hyper-V [в Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) или [Windows Server 2012 и 2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="62b26-122">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="62b26-123">Hello более новый формат VHDX не поддерживается в Azure.</span><span class="sxs-lookup"><span data-stu-id="62b26-123">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="62b26-124">При создании виртуальной Машины, задайте hello формат виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="62b26-124">When you create a VM, specify VHD as hello format.</span></span> <span data-ttu-id="62b26-125">При необходимости можно преобразовать tooVHD диски VHDX с помощью [qemu img преобразовать](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) или hello [Convert-VHD](https://technet.microsoft.com/library/hh848454.aspx) командлета PowerShell.</span><span class="sxs-lookup"><span data-stu-id="62b26-125">If needed, you can convert VHDX disks tooVHD using [qemu-img convert](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or hello [Convert-VHD](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="62b26-126">Кроме того Azure не поддерживает передачи динамических виртуальных жестких дисков, поэтому требуется tooconvert toostatic такие диски VHD перед отправкой.</span><span class="sxs-lookup"><span data-stu-id="62b26-126">Further, Azure does not support uploading dynamic VHDs, so you need tooconvert such disks toostatic VHDs before uploading.</span></span> <span data-ttu-id="62b26-127">Можно использовать средства, такие как [утилиты Azure виртуального жесткого диска для GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert динамических дисков во время процесса hello передачи tooAzure.</span><span class="sxs-lookup"><span data-stu-id="62b26-127">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamic disks during hello process of uploading tooAzure.</span></span>
> 
> 


* <span data-ttu-id="62b26-128">Убедитесь, что hello последней [Azure CLI 2.0](/cli/azure/install-az-cli2) установлен и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="62b26-128">Make sure that you have hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="62b26-129">В hello следующих примерах замените примеры имен параметров собственные значения.</span><span class="sxs-lookup"><span data-stu-id="62b26-129">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="62b26-130">Примеры имен параметров: *myResourceGroup*, *mystorageaccount* и *mydisks*.</span><span class="sxs-lookup"><span data-stu-id="62b26-130">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *mydisks*.</span></span>

<span data-ttu-id="62b26-131"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="62b26-131"><a id="prepimage"> </a></span></span>

## <a name="prepare-hello-vm"></a><span data-ttu-id="62b26-132">Подготовка виртуальной Машины hello</span><span class="sxs-lookup"><span data-stu-id="62b26-132">Prepare hello VM</span></span>

<span data-ttu-id="62b26-133">Azure поддерживает различные дистрибутивы Linux (см. раздел [Рекомендованные дистрибутивы](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="62b26-133">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="62b26-134">следующие статьи Hello проводит пользователя через как tooprepare hello различных дистрибутивов Linux, которые поддерживаются в Azure:</span><span class="sxs-lookup"><span data-stu-id="62b26-134">hello following articles guide you through how tooprepare hello various Linux distributions that are supported on Azure:</span></span>

* [<span data-ttu-id="62b26-135">Подготовка виртуальной машины на основе CentOS для Azure</span><span class="sxs-lookup"><span data-stu-id="62b26-135">CentOS-based Distributions</span></span>](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="62b26-136">Подготовка виртуального жесткого диска Debian для Azure</span><span class="sxs-lookup"><span data-stu-id="62b26-136">Debian Linux</span></span>](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="62b26-137">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="62b26-137">Oracle Linux</span></span>](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="62b26-138">Подготовка виртуальной машины на основе Red Hat для Azure</span><span class="sxs-lookup"><span data-stu-id="62b26-138">Red Hat Enterprise Linux</span></span>](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="62b26-139">Подготовка виртуальной машины SLES или openSUSE для Azure</span><span class="sxs-lookup"><span data-stu-id="62b26-139">SLES & openSUSE</span></span>](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="62b26-140">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="62b26-140">Ubuntu</span></span>](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="62b26-141">Информация о нерекомендованных дистрибутивах</span><span class="sxs-lookup"><span data-stu-id="62b26-141">Other - Non-Endorsed Distributions</span></span>](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

<span data-ttu-id="62b26-142">См. также hello [замечания по установке Linux](create-upload-generic.md#general-linux-installation-notes) Общие рекомендации по подготовке образов Linux для Azure.</span><span class="sxs-lookup"><span data-stu-id="62b26-142">Also see hello [Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="62b26-143">Hello [платформы Azure соглашения об уровне ОБСЛУЖИВАНИЯ](https://azure.microsoft.com/support/legal/sla/virtual-machines/) применяется tooVMs под управлением Linux, если один из hello одобренных распределения используется с данными конфигурации hello, как указано в списке поддерживаемых версиях только в [Linux в одобренных Azure Распределения](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="62b26-143">hello [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies tooVMs running Linux only when one of hello endorsed distributions is used with hello configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

## <a name="option-1-upload-a-vhd"></a><span data-ttu-id="62b26-144">Вариант 1. Передача VHD</span><span class="sxs-lookup"><span data-stu-id="62b26-144">Option 1: Upload a VHD</span></span>

<span data-ttu-id="62b26-145">Вы можете передать настраиваемый VHD, выполняемый на локальном компьютере или который вы экспортировали из другого облака.</span><span class="sxs-lookup"><span data-stu-id="62b26-145">You can upload a customized VHD that you have running on a local machine or that you exported from another cloud.</span></span> <span data-ttu-id="62b26-146">виртуальный жесткий ДИСК toocreate hello toouse новой виртуальной Машины Azure, потребуется tooupload hello VHD tooa хранилище учетной записи и создания управляемой дисковой из hello виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="62b26-146">toouse hello VHD toocreate a new Azure VM, you need tooupload hello VHD tooa storage account and create a managed disk from hello VHD.</span></span> 

### <a name="create-a-resource-group"></a><span data-ttu-id="62b26-147">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="62b26-147">Create a resource group</span></span>

<span data-ttu-id="62b26-148">Перед загрузкой пользовательского диска и создании виртуальных машин, необходимо сначала toocreate группу ресурсов с [Создание группы az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="62b26-148">Before uploading your custom disk and creating VMs, you first need toocreate a resource group with [az group create](/cli/azure/group#create).</span></span>

<span data-ttu-id="62b26-149">Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *eastus* расположение: [Общие сведения о дисках управляемых Azure](../windows/managed-disks-overview.md)</span><span class="sxs-lookup"><span data-stu-id="62b26-149">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location: [Azure Managed Disks overview](../windows/managed-disks-overview.md)</span></span>
```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

### <a name="create-a-storage-account"></a><span data-ttu-id="62b26-150">Создать учетную запись хранения</span><span class="sxs-lookup"><span data-stu-id="62b26-150">Create a storage account</span></span>

<span data-ttu-id="62b26-151">Создайте учетную запись хранения для пользовательского диска и виртуальных машин с помощью команды [az storage account create](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="62b26-151">Create a storage account for your custom disk and VMs with [az storage account create](/cli/azure/storage/account#create).</span></span> 

<span data-ttu-id="62b26-152">Hello следующий пример создает учетную запись хранения с именем *mystorageaccount* в ранее созданную группу ресурсов hello:</span><span class="sxs-lookup"><span data-stu-id="62b26-152">hello following example creates a storage account named *mystorageaccount* in hello resource group previously created:</span></span>

```azurecli
az storage account create \
    --resource-group myResourceGroup \
    --location eastus \
    --name mystorageaccount \
    --kind Storage \
    --sku Standard_LRS
```

### <a name="list-storage-account-keys"></a><span data-ttu-id="62b26-153">Вывод списка ключей учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="62b26-153">List storage account keys</span></span>
<span data-ttu-id="62b26-154">Azure создает два 512-разрядных ключа доступа для каждой учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="62b26-154">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="62b26-155">Эти ключи доступа используются при проверке подлинности учетной записи хранилища toohello, как и выполнения операций записи.</span><span class="sxs-lookup"><span data-stu-id="62b26-155">These access keys are used when authenticating toohello storage account, like carrying out write operations.</span></span> <span data-ttu-id="62b26-156">Дополнительные сведения о [управление доступ здесь toostorage](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="62b26-156">Read more about [managing access toostorage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="62b26-157">Просмотреть ключи доступа hello с [список ключей учетной записи хранилища az](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="62b26-157">You view hello access keys with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span>

<span data-ttu-id="62b26-158">Просмотр ключей доступа к hello для hello хранилища созданную учетную запись:</span><span class="sxs-lookup"><span data-stu-id="62b26-158">View hello access keys for hello storage account you created:</span></span>

```azurecli
az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount
```

<span data-ttu-id="62b26-159">Hello выходные данные выглядят аналогично:</span><span class="sxs-lookup"><span data-stu-id="62b26-159">hello output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK
```
<span data-ttu-id="62b26-160">Запомните или запишите **key1** как он будет использоваться toointeract с вашей учетной записи хранения в hello дальнейшие действия.</span><span class="sxs-lookup"><span data-stu-id="62b26-160">Make a note of **key1** as you will use it toointeract with your storage account in hello next steps.</span></span>

### <a name="create-a-storage-container"></a><span data-ttu-id="62b26-161">Создание контейнера хранилища</span><span class="sxs-lookup"><span data-stu-id="62b26-161">Create a storage container</span></span>
<span data-ttu-id="62b26-162">В hello так же, создания разных каталогах toologically организации локальной файловой системе, создайте контейнерам внутри tooorganize учетной записи хранения на дисках.</span><span class="sxs-lookup"><span data-stu-id="62b26-162">In hello same way that you create different directories toologically organize your local file system, you create containers within a storage account tooorganize your disks.</span></span> <span data-ttu-id="62b26-163">Учетная запись хранения может содержать любое количество контейнеров.</span><span class="sxs-lookup"><span data-stu-id="62b26-163">A storage account can contain any number of containers.</span></span> <span data-ttu-id="62b26-164">Создайте контейнер с помощью команды [az storage container create](/cli/azure/storage/container#create).</span><span class="sxs-lookup"><span data-stu-id="62b26-164">Create a container with [az storage container create](/cli/azure/storage/container#create).</span></span>

<span data-ttu-id="62b26-165">Hello следующий пример создает контейнер с именем *mydisks*:</span><span class="sxs-lookup"><span data-stu-id="62b26-165">hello following example creates a container named *mydisks*:</span></span>

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

### <a name="upload-hello-vhd"></a><span data-ttu-id="62b26-166">Отправка hello виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="62b26-166">Upload hello VHD</span></span>
<span data-ttu-id="62b26-167">Теперь передайте пользовательский диск с помощью команды [az storage blob upload](/cli/azure/storage/blob#upload).</span><span class="sxs-lookup"><span data-stu-id="62b26-167">Now upload your custom disk with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="62b26-168">Пользовательский диск передается и хранится как страничный BLOB-объект.</span><span class="sxs-lookup"><span data-stu-id="62b26-168">You upload and store your custom disk as a page blob.</span></span>

<span data-ttu-id="62b26-169">Укажите ваш ключ доступа, контейнер hello, созданный на предыдущем шаге hello и затем hello toohello пользовательского диска на локальном компьютере:</span><span class="sxs-lookup"><span data-stu-id="62b26-169">Specify your access key, hello container you created in hello previous step, and then hello path toohello custom disk on your local computer:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 \
    --container-name mydisks \
    --type page \
    --file /path/to/disk/mydisk.vhd \
    --name myDisk.vhd
```
<span data-ttu-id="62b26-170">Отправка hello виртуального жесткого диска может занять некоторое время.</span><span class="sxs-lookup"><span data-stu-id="62b26-170">Uploading hello VHD may take a while.</span></span>

### <a name="create-a-managed-disk"></a><span data-ttu-id="62b26-171">Создание управляемого диска</span><span class="sxs-lookup"><span data-stu-id="62b26-171">Create a managed disk</span></span>


<span data-ttu-id="62b26-172">Создание управляемого диска из hello виртуального жесткого диска с помощью [создать диск az](/cli/azure/disk#create).</span><span class="sxs-lookup"><span data-stu-id="62b26-172">Create a managed disk from hello VHD using [az disk create](/cli/azure/disk#create).</span></span> <span data-ttu-id="62b26-173">Hello следующий пример создает управляемого диска с именем *myManagedDisk* из hello виртуальный жесткий ДИСК отправлен tooyour с именем учетной записи хранилища и контейнера:</span><span class="sxs-lookup"><span data-stu-id="62b26-173">hello following example creates a managed disk named *myManagedDisk* from hello VHD you uploaded tooyour named storage account and container:</span></span>

```azurecli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
  --source https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd
```
## <a name="option-2-copy-an-existing-vm"></a><span data-ttu-id="62b26-174">Вариант 2. Копирование имеющейся виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="62b26-174">Option 2: Copy an existing VM</span></span>

<span data-ttu-id="62b26-175">Можно также создать hello настроенных ВМ в Azure, а затем Копировать диск ОС hello и присоединить ее новой виртуальной Машины toocreate tooa другую копию.</span><span class="sxs-lookup"><span data-stu-id="62b26-175">You can also create hello customized VM in Azure and then copy hello OS disk and attach it tooa new VM toocreate another copy.</span></span> <span data-ttu-id="62b26-176">Это хорошо работает для тестирования, но если требуется toouse существующей ВМ Azure как модель hello несколько новых виртуальных машин, действительно следует создать **изображения** вместо него.</span><span class="sxs-lookup"><span data-stu-id="62b26-176">This is fine for testing, but if you want toouse an existing Azure VM as hello model for multiple new VMs, you really should create an **image** instead.</span></span> <span data-ttu-id="62b26-177">Дополнительные сведения о создании образа на основе существующей виртуальной Машине Azure см. в разделе [создать образ виртуальной машины Azure с помощью hello CLI](tutorial-custom-images.md)</span><span class="sxs-lookup"><span data-stu-id="62b26-177">For more information about creating an image from an existing Azure VM, see [Create a custom image of an Azure VM using hello CLI](tutorial-custom-images.md)</span></span>

### <a name="create-a-snapshot"></a><span data-ttu-id="62b26-178">Создание моментального снимка</span><span class="sxs-lookup"><span data-stu-id="62b26-178">Create a snapshot</span></span>

<span data-ttu-id="62b26-179">В этом примере создается моментальный снимок виртуальной машины с именем *myVM* в группе ресурсов *myResourceGroup*, а также моментальный снимок с именем *osDiskSnapshot*.</span><span class="sxs-lookup"><span data-stu-id="62b26-179">This example creates a snapshot of a VM named *myVM* in resource group *myResourceGroup* and creates a snapshot named *osDiskSnapshot*.</span></span>

```azure-cli
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create \
    -g myResourceGroup \
    --source "$osDiskId" \
    --name osDiskSnapshot
```
###  <a name="create-hello-managed-disk"></a><span data-ttu-id="62b26-180">Создание управляемого диска hello</span><span class="sxs-lookup"><span data-stu-id="62b26-180">Create hello managed disk</span></span>

<span data-ttu-id="62b26-181">Создание нового управляемого диска из моментального снимка hello.</span><span class="sxs-lookup"><span data-stu-id="62b26-181">Create a new managed disk from hello snapshot.</span></span>

<span data-ttu-id="62b26-182">Получите идентификатор hello hello моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="62b26-182">Get hello ID of hello snapshot.</span></span> <span data-ttu-id="62b26-183">В этом примере имя моментального снимка hello *osDiskSnapshot* и hello *myResourceGroup* группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="62b26-183">In this example, hello snapshot is named *osDiskSnapshot* and it is in hello *myResourceGroup* resource group.</span></span>

```azure-cli
snapshotId=$(az snapshot show --name osDiskSnapshot --resource-group myResourceGroup --query [id] -o tsv)
```

<span data-ttu-id="62b26-184">Создание управляемого диска hello.</span><span class="sxs-lookup"><span data-stu-id="62b26-184">Create hello managed disk.</span></span> <span data-ttu-id="62b26-185">В этом примере мы создадим управляемый диск с именем *myManagedDisk* на основе моментального снимка размером в 128 ГБ, который хранится в хранилище уровня "Стандартный".</span><span class="sxs-lookup"><span data-stu-id="62b26-185">In this example, we will create a managed disk named *myManagedDisk* from our snapshot, that is 128GB in size in standard storage.</span></span>

```azure-cli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
    --sku Standard_LRS \
    --size-gb 128 \
    --source $snapshotId
```

## <a name="create-hello-vm"></a><span data-ttu-id="62b26-186">Создание виртуальной Машины hello</span><span class="sxs-lookup"><span data-stu-id="62b26-186">Create hello VM</span></span>

<span data-ttu-id="62b26-187">Теперь создайте ВМ с [создания виртуальной машины az](/cli/azure/vm#create) и присоединения (--присоединить os диск) hello управляемых диск как диск ОС hello.</span><span class="sxs-lookup"><span data-stu-id="62b26-187">Now, create your VM with [az vm create](/cli/azure/vm#create) and attach (--attach-os-disk) hello managed disk as hello OS disk.</span></span> <span data-ttu-id="62b26-188">Hello следующий пример создает Виртуальную машину с именем *myNewVM* с помощью hello управляемого диск, созданный из вашего загруженного VHD-файла:</span><span class="sxs-lookup"><span data-stu-id="62b26-188">hello following example creates a VM named *myNewVM* using hello managed disk created from your uploaded VHD:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNewVM \
    --os-type linux \
    --attach-os-disk myManagedDisk
```

<span data-ttu-id="62b26-189">После этого можно будет tooSSH в hello виртуальной Машины с помощью учетных данных hello из hello исходной виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="62b26-189">You should be able tooSSH into hello VM using hello credentials from hello source VM.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="62b26-190">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="62b26-190">Next steps</span></span>
<span data-ttu-id="62b26-191">После подготовки и передачи пользовательского виртуального диска ознакомьтесь с дополнительными сведениями об [использовании Resource Manager и шаблонов](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="62b26-191">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="62b26-192">Вы также можете слишком[добавьте диск данных](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour новые виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="62b26-192">You may also want too[add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour new VMs.</span></span> <span data-ttu-id="62b26-193">При наличии приложений, выполняющихся на виртуальные машины, необходимо tooaccess, нужно убедиться, что слишком[открыть порты и конечные точки](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="62b26-193">If you have applications running on your VMs that you need tooaccess, be sure too[open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

