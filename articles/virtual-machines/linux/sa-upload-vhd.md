---
title: "aaaUpload пользовательского диска Linux с помощью Azure CLI 2.0 | Документы Microsoft"
description: "Создание и отправка виртуального жесткого диска (VHD) tooAzure, с помощью модели развертывания диспетчера ресурсов hello и hello Azure CLI 2.0"
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
ms.date: 07/10/2017
ms.author: cynthn
ms.openlocfilehash: cf8556ab4dfe6c4e5eff4e99fe1ddc44393f774c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-with-hello-azure-cli-20"></a><span data-ttu-id="b4d13-103">Передача и создание виртуальной Машины Linux с пользовательской диска с hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="b4d13-103">Upload and create a Linux VM from custom disk with hello Azure CLI 2.0</span></span>
<span data-ttu-id="b4d13-104">В этой статье показано, как tooupload tooan виртуального жесткого диска (VHD) хранилища Azure учетной записи с hello Azure CLI 2.0 и создания виртуальных машин Linux с этого пользовательского диска.</span><span class="sxs-lookup"><span data-stu-id="b4d13-104">This article shows you how tooupload a virtual hard disk (VHD) tooan Azure storage account with hello Azure CLI 2.0 and create Linux VMs from this custom disk.</span></span> <span data-ttu-id="b4d13-105">Можно также выполнить следующие действия с hello [Azure CLI 1.0](upload-vhd-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b4d13-105">You can also perform these steps with hello [Azure CLI 1.0](upload-vhd-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="b4d13-106">Эта функция позволяет вам tooinstall и настройте требования tooyour дистрибутив Linux и затем использовать этот виртуальный жесткий ДИСК tooquickly создания виртуальных машин (ВМ) Azure.</span><span class="sxs-lookup"><span data-stu-id="b4d13-106">This functionality allows you tooinstall and configure a Linux distro tooyour requirements and then use that VHD tooquickly create Azure virtual machines (VMs).</span></span>

<span data-ttu-id="b4d13-107">В этом разделе используются учетные записи хранения для hello окончательного виртуальные жесткие диски, но можно также сделать эти шаги с помощью [управляемых дисках](upload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="b4d13-107">This topic uses storage accounts for hello final VHDs, but you can also do these steps using [managed disks](upload-vhd.md).</span></span> 

## <a name="quick-commands"></a><span data-ttu-id="b4d13-108">Быстрые команды</span><span class="sxs-lookup"><span data-stu-id="b4d13-108">Quick commands</span></span>
<span data-ttu-id="b4d13-109">При необходимости tooquickly выполнения задачи hello, hello следующий раздел сведения hello базовые команды tooupload tooAzure виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="b4d13-109">If you need tooquickly accomplish hello task, hello following section details hello base commands tooupload a VHD tooAzure.</span></span> <span data-ttu-id="b4d13-110">Более подробные сведения и контекста, для каждого шага можно найти hello остальной части документа hello [начиная здесь](#requirements).</span><span class="sxs-lookup"><span data-stu-id="b4d13-110">More detailed information and context for each step can be found hello rest of hello document, [starting here](#requirements).</span></span>

<span data-ttu-id="b4d13-111">Убедитесь, что hello последней [Azure CLI 2.0](/cli/azure/install-az-cli2) установлен и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="b4d13-111">Make sure that you have hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="b4d13-112">В hello следующих примерах замените примеры имен параметров собственные значения.</span><span class="sxs-lookup"><span data-stu-id="b4d13-112">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="b4d13-113">Используемые имена параметров — `myResourceGroup`, `mystorageaccount`, и `mydisks`.</span><span class="sxs-lookup"><span data-stu-id="b4d13-113">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `mydisks`.</span></span>

<span data-ttu-id="b4d13-114">Сначала создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="b4d13-114">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="b4d13-115">Hello следующий пример создает группу ресурсов с именем `myResourceGroup` в hello `WestUs` расположение:</span><span class="sxs-lookup"><span data-stu-id="b4d13-115">hello following example creates a resource group named `myResourceGroup` in hello `WestUs` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="b4d13-116">Создание учетной записи хранилища toohold виртуальных дисков с [создания учетной записи хранилища az](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="b4d13-116">Create a storage account toohold your virtual disks with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="b4d13-117">Hello следующий пример создает учетную запись хранения с именем `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="b4d13-117">hello following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

<span data-ttu-id="b4d13-118">Список hello ключи доступа для учетной записи хранилища с [список ключей учетной записи хранилища az](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="b4d13-118">List hello access keys for your storage account with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span> <span data-ttu-id="b4d13-119">Запишите `key1`:</span><span class="sxs-lookup"><span data-stu-id="b4d13-119">Make a note of `key1`:</span></span>

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
```

<span data-ttu-id="b4d13-120">Создание контейнера в учетной записи хранилища с помощью ключа хранилища hello получен с [создать контейнер хранилища az](/cli/azure/storage/container#create).</span><span class="sxs-lookup"><span data-stu-id="b4d13-120">Create a container within your storage account using hello storage key you obtained with [az storage container create](/cli/azure/storage/container#create).</span></span> <span data-ttu-id="b4d13-121">Hello следующий пример создает контейнер с именем `mydisks` с помощью hello значение ключа хранилища из `key1`:</span><span class="sxs-lookup"><span data-stu-id="b4d13-121">hello following example creates a container named `mydisks` using hello storage key value from `key1`:</span></span>

```azurecli
az storage container create --account-name mystorageaccount \
    --account-key key1 --name mydisks
```

<span data-ttu-id="b4d13-122">Наконец, отправьте toohello контейнера VHD был создан с [передачи BLOB-объекта хранилища az](/cli/azure/storage/blob#upload).</span><span class="sxs-lookup"><span data-stu-id="b4d13-122">Finally, upload your VHD toohello container you created with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="b4d13-123">Укажите локальный путь hello tooyour виртуальный жесткий ДИСК в разделе `/path/to/disk/mydisk.vhd`:</span><span class="sxs-lookup"><span data-stu-id="b4d13-123">Specify hello local path tooyour VHD under `/path/to/disk/mydisk.vhd`:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

<span data-ttu-id="b4d13-124">Укажите диск tooyour hello URI (`--image`) с [создания виртуальной машины az](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="b4d13-124">Specify hello URI tooyour disk (`--image`) with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="b4d13-125">Hello следующий пример создает Виртуальную машину с именем `myVM` с помощью виртуального диска hello ранее отправленные:</span><span class="sxs-lookup"><span data-stu-id="b4d13-125">hello following example creates a VM named `myVM` using hello virtual disk previously uploaded:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisk/myDisks.vhd \
    --use-unmanaged-disk
```

<span data-ttu-id="b4d13-126">Hello целевой учетной записью хранения имеет toobe Здравствуйте таким же, как где загруженный виртуальный диск.</span><span class="sxs-lookup"><span data-stu-id="b4d13-126">hello destination storage account has toobe hello same as where you uploaded your virtual disk to.</span></span> <span data-ttu-id="b4d13-127">Также необходимо toospecify или ответить на запрос, все hello Дополнительные параметры, необходимые для hello **создания виртуальной машины az** команды, такие как виртуальная сеть, общедоступный IP-адрес, имя пользователя и ключи SSH.</span><span class="sxs-lookup"><span data-stu-id="b4d13-127">You also need toospecify, or answer prompts for, all hello additional parameters required by hello **az vm create** command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="b4d13-128">Вы можете прочитать больше о hello [доступных параметров диспетчера ресурсов CLI](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="b4d13-128">You can read more about hello [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

## <a name="requirements"></a><span data-ttu-id="b4d13-129">Требования</span><span class="sxs-lookup"><span data-stu-id="b4d13-129">Requirements</span></span>
<span data-ttu-id="b4d13-130">toocomplete hello следующие действия, необходимо:</span><span class="sxs-lookup"><span data-stu-id="b4d13-130">toocomplete hello following steps, you need:</span></span>

* <span data-ttu-id="b4d13-131">**Операционной системы Linux в VHD-файла** -установка [дистрибутив Linux в одобренных Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (или в разделе [сведения для распределений, отличных от одобренных](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa виртуальный диск в hello виртуального жесткого диска формат.</span><span class="sxs-lookup"><span data-stu-id="b4d13-131">**Linux operating system installed in a .vhd file** - Install an [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtual disk in hello VHD format.</span></span> <span data-ttu-id="b4d13-132">Несколько средств существует toocreate виртуальной Машины и виртуального жесткого диска:</span><span class="sxs-lookup"><span data-stu-id="b4d13-132">Multiple tools exist toocreate a VM and VHD:</span></span>
  * <span data-ttu-id="b4d13-133">Установка и настройка [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) или [KVM](http://www.linux-kvm.org/page/RunningKVM), отвечающий за toouse виртуальный жесткий ДИСК в формате изображения.</span><span class="sxs-lookup"><span data-stu-id="b4d13-133">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care toouse VHD as your image format.</span></span> <span data-ttu-id="b4d13-134">При необходимости вы можете [преобразовать образ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) с помощью `qemu-img convert`.</span><span class="sxs-lookup"><span data-stu-id="b4d13-134">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="b4d13-135">Кроме того, можно использовать Hyper-V [в Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) или [Windows Server 2012 и 2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="b4d13-135">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="b4d13-136">Hello более новый формат VHDX не поддерживается в Azure.</span><span class="sxs-lookup"><span data-stu-id="b4d13-136">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="b4d13-137">При создании виртуальной Машины, задайте hello формат виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="b4d13-137">When you create a VM, specify VHD as hello format.</span></span> <span data-ttu-id="b4d13-138">При необходимости можно преобразовать tooVHD диски VHDX с помощью [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) или hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) командлета PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b4d13-138">If needed, you can convert VHDX disks tooVHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or hello [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="b4d13-139">Кроме того Azure не поддерживает передачи динамических виртуальных жестких дисков, поэтому требуется tooconvert toostatic такие диски VHD перед отправкой.</span><span class="sxs-lookup"><span data-stu-id="b4d13-139">Further, Azure does not support uploading dynamic VHDs, so you need tooconvert such disks toostatic VHDs before uploading.</span></span> <span data-ttu-id="b4d13-140">Можно использовать средства, такие как [утилиты Azure виртуального жесткого диска для GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert динамических дисков во время процесса hello передачи tooAzure.</span><span class="sxs-lookup"><span data-stu-id="b4d13-140">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamic disks during hello process of uploading tooAzure.</span></span>
> 
> 

* <span data-ttu-id="b4d13-141">Виртуальные машины, созданные с пользовательской диска необходимо разместить в hello же учетной записи хранилища, сам диск hello</span><span class="sxs-lookup"><span data-stu-id="b4d13-141">VMs created from your custom disk must reside in hello same storage account as hello disk itself</span></span>
  * <span data-ttu-id="b4d13-142">Создание хранилища учетной записи и контейнер toohold созданных виртуальных машин и пользовательского диска</span><span class="sxs-lookup"><span data-stu-id="b4d13-142">Create a storage account and container toohold both your custom disk and created VMs</span></span>
  * <span data-ttu-id="b4d13-143">Когда вы закончите создание всех виртуальных машин, диск можно спокойно удалить.</span><span class="sxs-lookup"><span data-stu-id="b4d13-143">After you have created all your VMs, you can safely delete your disk</span></span>

<span data-ttu-id="b4d13-144">Убедитесь, что hello последней [Azure CLI 2.0](/cli/azure/install-az-cli2) установлен и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="b4d13-144">Make sure that you have hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="b4d13-145">В hello следующих примерах замените примеры имен параметров собственные значения.</span><span class="sxs-lookup"><span data-stu-id="b4d13-145">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="b4d13-146">Используемые имена параметров — `myResourceGroup`, `mystorageaccount`, и `mydisks`.</span><span class="sxs-lookup"><span data-stu-id="b4d13-146">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `mydisks`.</span></span>

<span data-ttu-id="b4d13-147"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="b4d13-147"><a id="prepimage"> </a></span></span>

## <a name="prepare-hello-disk-toobe-uploaded"></a><span data-ttu-id="b4d13-148">Подготовка toobe диска hello отправлен</span><span class="sxs-lookup"><span data-stu-id="b4d13-148">Prepare hello disk toobe uploaded</span></span>
<span data-ttu-id="b4d13-149">Azure поддерживает различные дистрибутивы Linux (см. раздел [Рекомендованные дистрибутивы](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="b4d13-149">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="b4d13-150">следующие статьи Hello проводит пользователя через как tooprepare hello различных дистрибутивов Linux, которые поддерживаются в Azure:</span><span class="sxs-lookup"><span data-stu-id="b4d13-150">hello following articles guide you through how tooprepare hello various Linux distributions that are supported on Azure:</span></span>

* <span data-ttu-id="b4d13-151">**[Дистрибутивы на основе CentOS](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="b4d13-151">**[CentOS-based Distributions](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="b4d13-152">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="b4d13-152">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="b4d13-153">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="b4d13-153">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="b4d13-154">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="b4d13-154">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="b4d13-155">**[SLES и OpenSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="b4d13-155">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="b4d13-156">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="b4d13-156">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="b4d13-157">**[Прочее — нерекомендованные дистрибутивы](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="b4d13-157">**[Other - Non-Endorsed Distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

<span data-ttu-id="b4d13-158">См. также hello  **[замечания по установке Linux](create-upload-generic.md#general-linux-installation-notes)**  Общие рекомендации по подготовке образов Linux для Azure.</span><span class="sxs-lookup"><span data-stu-id="b4d13-158">Also see hello **[Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="b4d13-159">Hello [платформы Azure соглашения об уровне ОБСЛУЖИВАНИЯ](https://azure.microsoft.com/support/legal/sla/virtual-machines/) применяется tooVMs под управлением Linux, если один из hello одобренных распределения используется с данными конфигурации hello, как указано в списке поддерживаемых версиях только в [Linux в одобренных Azure Распределения](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b4d13-159">hello [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies tooVMs running Linux only when one of hello endorsed distributions is used with hello configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

## <a name="create-a-resource-group"></a><span data-ttu-id="b4d13-160">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="b4d13-160">Create a resource group</span></span>
<span data-ttu-id="b4d13-161">Группы ресурсов логически объединить все toosupport ресурсы Azure hello виртуальных машин, например hello виртуальных сетей и хранилища.</span><span class="sxs-lookup"><span data-stu-id="b4d13-161">Resource groups logically bring together all hello Azure resources toosupport your virtual machines, such as hello virtual networking and storage.</span></span> <span data-ttu-id="b4d13-162">См. дополнительные сведения о [группах ресурсов](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b4d13-162">For more information resource groups, see [resource groups overview](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="b4d13-163">Перед загрузкой пользовательского диска и создании виртуальных машин, необходимо сначала toocreate группу ресурсов с [Создание группы az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="b4d13-163">Before uploading your custom disk and creating VMs, you first need toocreate a resource group with [az group create](/cli/azure/group#create).</span></span>

<span data-ttu-id="b4d13-164">Hello следующий пример создает группу ресурсов с именем `myResourceGroup` в hello `westus` расположение:</span><span class="sxs-lookup"><span data-stu-id="b4d13-164">hello following example creates a resource group named `myResourceGroup` in hello `westus` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-a-storage-account"></a><span data-ttu-id="b4d13-165">Создать учетную запись хранения</span><span class="sxs-lookup"><span data-stu-id="b4d13-165">Create a storage account</span></span>

<span data-ttu-id="b4d13-166">Создайте учетную запись хранения для пользовательского диска и виртуальных машин с помощью команды [az storage account create](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="b4d13-166">Create a storage account for your custom disk and VMs with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="b4d13-167">Все виртуальные машины с неуправляемой диски, создаваемые на основе toobe потребности вашего пользовательского диска в hello же учетной записи хранилища этот диск.</span><span class="sxs-lookup"><span data-stu-id="b4d13-167">Any VMs with unmanaged disks that you create from your custom disk need toobe in hello same storage account as that disk.</span></span> 

<span data-ttu-id="b4d13-168">Hello следующий пример создает учетную запись хранения с именем `mystorageaccount` в ранее созданную группу ресурсов hello:</span><span class="sxs-lookup"><span data-stu-id="b4d13-168">hello following example creates a storage account named `mystorageaccount` in hello resource group previously created:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

## <a name="list-storage-account-keys"></a><span data-ttu-id="b4d13-169">Вывод списка ключей учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="b4d13-169">List storage account keys</span></span>
<span data-ttu-id="b4d13-170">Azure создает два 512-разрядных ключа доступа для каждой учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="b4d13-170">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="b4d13-171">Эти ключи доступа используются при проверке подлинности учетной записи хранилища toohello, например toocarry операций записи.</span><span class="sxs-lookup"><span data-stu-id="b4d13-171">These access keys are used when authenticating toohello storage account, such as toocarry out write operations.</span></span> <span data-ttu-id="b4d13-172">Дополнительные сведения о [управление доступ здесь toostorage](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="b4d13-172">Read more about [managing access toostorage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="b4d13-173">Просмотреть ключи доступа hello с [список ключей учетной записи хранилища az](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="b4d13-173">You view hello access keys with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span>

<span data-ttu-id="b4d13-174">Просмотр ключей доступа к hello для hello хранилища созданную учетную запись:</span><span class="sxs-lookup"><span data-stu-id="b4d13-174">View hello access keys for hello storage account you created:</span></span>

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
```

<span data-ttu-id="b4d13-175">Hello выходные данные выглядят аналогично:</span><span class="sxs-lookup"><span data-stu-id="b4d13-175">hello output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK
```
<span data-ttu-id="b4d13-176">Запомните или запишите `key1` как он будет использоваться toointeract с вашей учетной записи хранения в hello дальнейшие действия.</span><span class="sxs-lookup"><span data-stu-id="b4d13-176">Make a note of `key1` as you will use it toointeract with your storage account in hello next steps.</span></span>

## <a name="create-a-storage-container"></a><span data-ttu-id="b4d13-177">Создание контейнера хранилища</span><span class="sxs-lookup"><span data-stu-id="b4d13-177">Create a storage container</span></span>
<span data-ttu-id="b4d13-178">В hello так же, создания разных каталогах toologically организации локальной файловой системе, создайте контейнерам внутри tooorganize учетной записи хранения на дисках.</span><span class="sxs-lookup"><span data-stu-id="b4d13-178">In hello same way that you create different directories toologically organize your local file system, you create containers within a storage account tooorganize your disks.</span></span> <span data-ttu-id="b4d13-179">Учетная запись хранения может содержать любое количество контейнеров.</span><span class="sxs-lookup"><span data-stu-id="b4d13-179">A storage account can contain any number of containers.</span></span> <span data-ttu-id="b4d13-180">Создайте контейнер с помощью команды [az storage container create](/cli/azure/storage/container#create).</span><span class="sxs-lookup"><span data-stu-id="b4d13-180">Create a container with [az storage container create](/cli/azure/storage/container#create).</span></span>

<span data-ttu-id="b4d13-181">Hello следующий пример создает контейнер с именем `mydisks`:</span><span class="sxs-lookup"><span data-stu-id="b4d13-181">hello following example creates a container named `mydisks`:</span></span>

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

## <a name="upload-vhd"></a><span data-ttu-id="b4d13-182">Передача VHD</span><span class="sxs-lookup"><span data-stu-id="b4d13-182">Upload VHD</span></span>
<span data-ttu-id="b4d13-183">Теперь передайте пользовательский диск с помощью команды [az storage blob upload](/cli/azure/storage/blob#upload).</span><span class="sxs-lookup"><span data-stu-id="b4d13-183">Now upload your custom disk with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="b4d13-184">Пользовательский диск передается и хранится как страничный BLOB-объект.</span><span class="sxs-lookup"><span data-stu-id="b4d13-184">You upload and store your custom disk as a page blob.</span></span>

<span data-ttu-id="b4d13-185">Укажите ваш ключ доступа, контейнер hello, созданный на предыдущем шаге hello и затем hello toohello пользовательского диска на локальном компьютере:</span><span class="sxs-lookup"><span data-stu-id="b4d13-185">Specify your access key, hello container you created in hello previous step, and then hello path toohello custom disk on your local computer:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

## <a name="create-hello-vm"></a><span data-ttu-id="b4d13-186">Создание виртуальной Машины hello</span><span class="sxs-lookup"><span data-stu-id="b4d13-186">Create hello VM</span></span>
<span data-ttu-id="b4d13-187">toocreate виртуальную Машину с неуправляемой дисков, укажите диск tooyour hello URI (`--image`) с [создания виртуальной машины az](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="b4d13-187">toocreate a VM with unmanaged disks, specify hello URI tooyour disk (`--image`) with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="b4d13-188">Hello следующий пример создает Виртуальную машину с именем `myVM` с помощью виртуального диска hello ранее отправленные:</span><span class="sxs-lookup"><span data-stu-id="b4d13-188">hello following example creates a VM named `myVM` using hello virtual disk previously uploaded:</span></span>

<span data-ttu-id="b4d13-189">Укажите hello `--image` параметр с [создания виртуальной машины az](/cli/azure/vm#create) toopoint tooyour пользовательского диска.</span><span class="sxs-lookup"><span data-stu-id="b4d13-189">You specify hello `--image` parameter with [az vm create](/cli/azure/vm#create) toopoint tooyour custom disk.</span></span> <span data-ttu-id="b4d13-190">Убедитесь, что `--storage-account` совпадений hello учетной записи хранилища, где хранятся пользовательские диска.</span><span class="sxs-lookup"><span data-stu-id="b4d13-190">Ensure that `--storage-account` matches hello storage account where your custom disk is stored.</span></span> <span data-ttu-id="b4d13-191">У вас toouse hello одного контейнера как hello toostore пользовательского диска виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="b4d13-191">You do not have toouse hello same container as hello custom disk toostore your VMs.</span></span> <span data-ttu-id="b4d13-192">Внесите любые дополнительные контейнеры toocreate убедиться, что в hello так же, как hello ранее перед отправкой пользовательского диска.</span><span class="sxs-lookup"><span data-stu-id="b4d13-192">Make sure toocreate any additional containers in hello same way as hello earlier steps before uploading your custom disk.</span></span>

<span data-ttu-id="b4d13-193">Hello следующий пример создает Виртуальную машину с именем `myVM` с пользовательской диска:</span><span class="sxs-lookup"><span data-stu-id="b4d13-193">hello following example creates a VM named `myVM` from your custom disk:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd \
    --use-unmanaged-disk
```

<span data-ttu-id="b4d13-194">Вы по-прежнему требуется toospecify или ответить на запрос, все hello Дополнительные параметры, необходимые для hello **создания виртуальной машины az** команды, такие как имя пользователя и ключи SSH.</span><span class="sxs-lookup"><span data-stu-id="b4d13-194">You still need toospecify, or answer prompts for, all hello additional parameters required by hello **az vm create** command such as username and SSH keys.</span></span>


## <a name="resource-manager-template"></a><span data-ttu-id="b4d13-195">Шаблон Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b4d13-195">Resource Manager template</span></span>
<span data-ttu-id="b4d13-196">Шаблоны Azure Resource Manager являются файлами JavaScript Object Notation (JSON), которые определяют среду hello нужно toobuild.</span><span class="sxs-lookup"><span data-stu-id="b4d13-196">Azure Resource Manager templates are JavaScript Object Notation (JSON) files that define hello environment you wish toobuild.</span></span> <span data-ttu-id="b4d13-197">шаблоны Hello разбиваются toodifferent поставщиков ресурсов, таких как вычислений или сети.</span><span class="sxs-lookup"><span data-stu-id="b4d13-197">hello templates are broken down in toodifferent resource providers such as compute or network.</span></span> <span data-ttu-id="b4d13-198">Можно использовать существующие шаблоны или создать собственный.</span><span class="sxs-lookup"><span data-stu-id="b4d13-198">You can use existing templates or write your own.</span></span> <span data-ttu-id="b4d13-199">Узнайте больше об [использовании Resource Manager и шаблонов](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b4d13-199">Read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="b4d13-200">В рамках hello `Microsoft.Compute/virtualMachines` у поставщика шаблона `storageProfile` узел, который содержит сведения о конфигурации hello для виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="b4d13-200">Within hello `Microsoft.Compute/virtualMachines` provider of your template, you have a `storageProfile` node that contains hello configuration details for your VM.</span></span> <span data-ttu-id="b4d13-201">tooedit Hello двумя основными параметрами, которые являются hello `image` и `vhd` URI, которые точки tooyour пользовательского диска и виртуального диска новой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="b4d13-201">hello two main parameters tooedit are hello `image` and `vhd` URIs that point tooyour custom disk and your new VM's virtual disk.</span></span> <span data-ttu-id="b4d13-202">Hello ниже показан пример hello JSON для использования пользовательского диска:</span><span class="sxs-lookup"><span data-stu-id="b4d13-202">hello following shows an example of hello JSON for using a custom disk:</span></span>

```json
"storageProfile": {
          "osDisk": {
            "name": "myVM",
            "osType": "Linux",
            "caching": "ReadWrite",
            "createOption": "FromImage",
            "image": {
              "uri": "https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd"
            },
            "vhd": {
              "uri": "https://mystorageaccount.blob.core.windows.net/vhds/newvmname.vhd"
            }
          }
```

<span data-ttu-id="b4d13-203">Можно использовать [toocreate этот существующий шаблон виртуальной Машины из образа](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) или для чтения о [Создание собственных шаблонов диспетчера ресурсов Azure](../../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="b4d13-203">You can use [this existing template toocreate a VM from a custom image](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) or read about [creating your own Azure Resource Manager templates](../../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 

<span data-ttu-id="b4d13-204">После настройки шаблона использовать [создания развертывания группы az](/cli/azure/group/deployment#create) toocreate виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="b4d13-204">Once you have a template configured, use [az group deployment create](/cli/azure/group/deployment#create) toocreate your VMs.</span></span> <span data-ttu-id="b4d13-205">Укажите hello URI шаблона JSON с hello `--template-uri` параметр:</span><span class="sxs-lookup"><span data-stu-id="b4d13-205">Specify hello URI of your JSON template with hello `--template-uri` parameter:</span></span>

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-uri https://uri.to.template/mytemplate.json
```

<span data-ttu-id="b4d13-206">Если имеется файл JSON, хранящиеся локально на компьютере, можно использовать hello `--template-file` параметра вместо:</span><span class="sxs-lookup"><span data-stu-id="b4d13-206">If you have a JSON file stored locally on your computer, you can use hello `--template-file` parameter instead:</span></span>

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a><span data-ttu-id="b4d13-207">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b4d13-207">Next steps</span></span>
<span data-ttu-id="b4d13-208">После подготовки и передачи пользовательского виртуального диска ознакомьтесь с дополнительными сведениями об [использовании Resource Manager и шаблонов](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b4d13-208">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="b4d13-209">Вы также можете слишком[добавьте диск данных](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour новые виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="b4d13-209">You may also want too[add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour new VMs.</span></span> <span data-ttu-id="b4d13-210">При наличии приложений, выполняющихся на виртуальные машины, необходимо tooaccess, нужно убедиться, что слишком[открыть порты и конечные точки](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b4d13-210">If you have applications running on your VMs that you need tooaccess, be sure too[open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

