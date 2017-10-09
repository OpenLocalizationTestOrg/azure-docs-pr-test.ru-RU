---
title: "aaaUpload пользовательского образа Linux с помощью Azure CLI 1.0 | Документы Microsoft"
description: "Создание и отправка tooAzure виртуального жесткого диска (VHD) с помощью образа Linux с помощью модели развертывания диспетчера ресурсов hello и hello Azure CLI 1.0."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a8c7818f-eb65-409e-aa91-ce5ae975c564
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/10/2016
ms.author: iainfou
ms.openlocfilehash: 0bbd232debee1e632233d1c010e388dbc1548bf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-image-by-using-hello-azure-cli-10"></a><span data-ttu-id="87d37-103">Передача и создание виртуальной Машины Linux из пользовательского образа с помощью hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="87d37-103">Upload and create a Linux VM from custom disk image by using hello Azure CLI 1.0</span></span>
<span data-ttu-id="87d37-104">В этой статье показано, как tooupload tooAzure виртуального жесткого диска (VHD) с помощью hello модели развертывания диспетчера ресурсов и создания виртуальных машин Linux из этого образа.</span><span class="sxs-lookup"><span data-stu-id="87d37-104">This article shows you how tooupload a virtual hard disk (VHD) tooAzure using hello Resource Manager deployment model and create Linux VMs from this custom image.</span></span> <span data-ttu-id="87d37-105">Эта функция позволяет вам tooinstall и настройте требования tooyour дистрибутив Linux и затем использовать этот виртуальный жесткий ДИСК tooquickly создания виртуальных машин (ВМ) Azure.</span><span class="sxs-lookup"><span data-stu-id="87d37-105">This functionality allows you tooinstall and configure a Linux distro tooyour requirements and then use that VHD tooquickly create Azure virtual machines (VMs).</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="87d37-106">Задача hello toocomplete версии CLI</span><span class="sxs-lookup"><span data-stu-id="87d37-106">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="87d37-107">Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.</span><span class="sxs-lookup"><span data-stu-id="87d37-107">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="87d37-108">[Azure CLI 1.0](#quick-commands) — нашей CLI для hello классический и ресурса управления развертывания моделей (в этой статье)</span><span class="sxs-lookup"><span data-stu-id="87d37-108">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="87d37-109">[Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -нашей нового поколения CLI для модели развертывания hello ресурсов управления</span><span class="sxs-lookup"><span data-stu-id="87d37-109">[Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="87d37-110">Быстрые команды</span><span class="sxs-lookup"><span data-stu-id="87d37-110">Quick commands</span></span>
<span data-ttu-id="87d37-111">При необходимости tooquickly выполнения задачи hello, hello следующий раздел сведения hello базовые команды tooupload tooAzure виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="87d37-111">If you need tooquickly accomplish hello task, hello following section details hello base commands tooupload a VM tooAzure.</span></span> <span data-ttu-id="87d37-112">Более подробные сведения и контекста, для каждого шага можно найти hello остальной части документа hello [начиная здесь](#requirements).</span><span class="sxs-lookup"><span data-stu-id="87d37-112">More detailed information and context for each step can be found hello rest of hello document, [starting here](#requirements).</span></span>

<span data-ttu-id="87d37-113">Убедитесь, что [hello Azure CLI 1.0](../../cli-install-nodejs.md) входа в систему и использование режима диспетчера ресурсов:</span><span class="sxs-lookup"><span data-stu-id="87d37-113">Make sure that you have [hello Azure CLI 1.0](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="87d37-114">В hello следующих примерах замените примеры имен параметров собственные значения.</span><span class="sxs-lookup"><span data-stu-id="87d37-114">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="87d37-115">Используемые имена параметров — `myResourceGroup`, `mystorageaccount`, и `myimages`.</span><span class="sxs-lookup"><span data-stu-id="87d37-115">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `myimages`.</span></span>

<span data-ttu-id="87d37-116">Сначала создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="87d37-116">First, create a resource group.</span></span> <span data-ttu-id="87d37-117">Hello следующий пример создает группу ресурсов с именем `myResourceGroup` в hello `WestUs` расположение:</span><span class="sxs-lookup"><span data-stu-id="87d37-117">hello following example creates a resource group named `myResourceGroup` in hello `WestUs` location:</span></span>

```azurecli
azure group create myResourceGroup --location "WestUS"
```

<span data-ttu-id="87d37-118">Создание учетной записи хранилища toohold виртуальных дисков.</span><span class="sxs-lookup"><span data-stu-id="87d37-118">Create a storage account toohold your virtual disks.</span></span> <span data-ttu-id="87d37-119">Hello следующий пример создает учетную запись хранения с именем `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="87d37-119">hello following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

<span data-ttu-id="87d37-120">Список hello ключи доступа для учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="87d37-120">List hello access keys for your storage account.</span></span> <span data-ttu-id="87d37-121">Запишите `key1`:</span><span class="sxs-lookup"><span data-stu-id="87d37-121">Make a note of `key1`:</span></span>

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
```

<span data-ttu-id="87d37-122">Создание контейнера в учетной записи хранилища с помощью ключа хранилища hello, который был получен.</span><span class="sxs-lookup"><span data-stu-id="87d37-122">Create a container within your storage account using hello storage key you obtained.</span></span> <span data-ttu-id="87d37-123">Hello следующий пример создает контейнер с именем `myimages` с помощью hello значение ключа хранилища из `key1`:</span><span class="sxs-lookup"><span data-stu-id="87d37-123">hello following example creates a container named `myimages` using hello storage key value from `key1`:</span></span>

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

<span data-ttu-id="87d37-124">И, наконец отправьте созданный контейнер toohello виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="87d37-124">Finally, upload your VHD toohello container you created.</span></span> <span data-ttu-id="87d37-125">Укажите локальный путь hello tooyour виртуальный жесткий ДИСК в разделе `/path/to/disk/mydisk.vhd`:</span><span class="sxs-lookup"><span data-stu-id="87d37-125">Specify hello local path tooyour VHD under `/path/to/disk/mydisk.vhd`:</span></span>

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

<span data-ttu-id="87d37-126">Теперь можно создать виртуальную машину из переданного виртуального диска [с помощью шаблона Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd).</span><span class="sxs-lookup"><span data-stu-id="87d37-126">You can now create a VM from your uploaded virtual disk [using a Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd).</span></span> <span data-ttu-id="87d37-127">Можно также использовать hello CLI, указав hello URI tooyour диска (`--image-urn`).</span><span class="sxs-lookup"><span data-stu-id="87d37-127">You can also use hello CLI by specifying hello URI tooyour disk (`--image-urn`).</span></span> <span data-ttu-id="87d37-128">Hello следующий пример создает Виртуальную машину с именем `myVM` с помощью виртуального диска hello ранее отправленные:</span><span class="sxs-lookup"><span data-stu-id="87d37-128">hello following example creates a VM named `myVM` using hello virtual disk previously uploaded:</span></span>

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
```

<span data-ttu-id="87d37-129">Hello целевой учетной записью хранения имеет toobe Здравствуйте таким же, как где загруженный виртуальный диск.</span><span class="sxs-lookup"><span data-stu-id="87d37-129">hello destination storage account has toobe hello same as where you uploaded your virtual disk to.</span></span> <span data-ttu-id="87d37-130">Также необходимо toospecify или ответить на запрос, все hello Дополнительные параметры, необходимые для hello `azure vm create` команды, такие как виртуальная сеть, общедоступный IP-адрес, имя пользователя и ключи SSH.</span><span class="sxs-lookup"><span data-stu-id="87d37-130">You also need toospecify, or answer prompts for, all hello additional parameters required by hello `azure vm create` command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="87d37-131">Вы можете прочитать больше о hello [доступных параметров диспетчера ресурсов CLI](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="87d37-131">You can read more about hello [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

## <a name="requirements"></a><span data-ttu-id="87d37-132">Требования</span><span class="sxs-lookup"><span data-stu-id="87d37-132">Requirements</span></span>
<span data-ttu-id="87d37-133">toocomplete hello следующие действия, необходимо:</span><span class="sxs-lookup"><span data-stu-id="87d37-133">toocomplete hello following steps, you need:</span></span>

* <span data-ttu-id="87d37-134">**Операционной системы Linux в VHD-файла** -установка [дистрибутив Linux в одобренных Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (или в разделе [сведения для распределений, отличных от одобренных](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa виртуальный диск в hello виртуального жесткого диска формат.</span><span class="sxs-lookup"><span data-stu-id="87d37-134">**Linux operating system installed in a .vhd file** - Install an [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtual disk in hello VHD format.</span></span> <span data-ttu-id="87d37-135">Несколько средств существует toocreate виртуальной Машины и виртуального жесткого диска:</span><span class="sxs-lookup"><span data-stu-id="87d37-135">Multiple tools exist toocreate a VM and VHD:</span></span>
  * <span data-ttu-id="87d37-136">Установка и настройка [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) или [KVM](http://www.linux-kvm.org/page/RunningKVM), отвечающий за toouse виртуальный жесткий ДИСК в формате изображения.</span><span class="sxs-lookup"><span data-stu-id="87d37-136">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care toouse VHD as your image format.</span></span> <span data-ttu-id="87d37-137">При необходимости вы можете [преобразовать образ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) с помощью `qemu-img convert`.</span><span class="sxs-lookup"><span data-stu-id="87d37-137">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="87d37-138">Кроме того, можно использовать Hyper-V [в Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) или [Windows Server 2012 и 2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="87d37-138">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="87d37-139">Hello более новый формат VHDX не поддерживается в Azure.</span><span class="sxs-lookup"><span data-stu-id="87d37-139">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="87d37-140">При создании виртуальной Машины, задайте hello формат виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="87d37-140">When you create a VM, specify VHD as hello format.</span></span> <span data-ttu-id="87d37-141">При необходимости можно преобразовать tooVHD диски VHDX с помощью [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) или hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) командлета PowerShell.</span><span class="sxs-lookup"><span data-stu-id="87d37-141">If needed, you can convert VHDX disks tooVHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or hello [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="87d37-142">Кроме того Azure не поддерживает передачи динамических виртуальных жестких дисков, поэтому требуется tooconvert toostatic такие диски VHD перед отправкой.</span><span class="sxs-lookup"><span data-stu-id="87d37-142">Further, Azure does not support uploading dynamic VHDs, so you need tooconvert such disks toostatic VHDs before uploading.</span></span> <span data-ttu-id="87d37-143">Можно использовать средства, такие как [утилиты Azure виртуального жесткого диска для GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert динамических дисков во время процесса hello передачи tooAzure.</span><span class="sxs-lookup"><span data-stu-id="87d37-143">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamic disks during hello process of uploading tooAzure.</span></span>
> 
> 

* <span data-ttu-id="87d37-144">Виртуальные машины, созданные из настраиваемого образа необходимо разместить в hello же учетной записи хранилища, само изображение hello</span><span class="sxs-lookup"><span data-stu-id="87d37-144">VMs created from your custom image must reside in hello same storage account as hello image itself</span></span>
  * <span data-ttu-id="87d37-145">Создание хранилища учетной записи и контейнер toohold образ и созданные виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="87d37-145">Create a storage account and container toohold both your custom image and created VMs</span></span>
  * <span data-ttu-id="87d37-146">После создания всех виртуальных машин можно спокойно удалить образ.</span><span class="sxs-lookup"><span data-stu-id="87d37-146">After you have created all your VMs, you can safely delete your image</span></span>

<span data-ttu-id="87d37-147">Убедитесь, что [hello Azure CLI 1.0](../../cli-install-nodejs.md) входа в систему и использование режима диспетчера ресурсов:</span><span class="sxs-lookup"><span data-stu-id="87d37-147">Make sure that you have [hello Azure CLI 1.0](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="87d37-148">В hello следующих примерах замените примеры имен параметров собственные значения.</span><span class="sxs-lookup"><span data-stu-id="87d37-148">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="87d37-149">Используемые имена параметров — `myResourceGroup`, `mystorageaccount`, и `myimages`.</span><span class="sxs-lookup"><span data-stu-id="87d37-149">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `myimages`.</span></span>

<span data-ttu-id="87d37-150"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="87d37-150"><a id="prepimage"> </a></span></span>

## <a name="prepare-hello-image-toobe-uploaded"></a><span data-ttu-id="87d37-151">Подготовка toobe изображения hello отправлен</span><span class="sxs-lookup"><span data-stu-id="87d37-151">Prepare hello image toobe uploaded</span></span>
<span data-ttu-id="87d37-152">Azure поддерживает различные дистрибутивы Linux (см. раздел [Рекомендованные дистрибутивы](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="87d37-152">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="87d37-153">следующие статьи Hello проводит пользователя через как tooprepare hello различных дистрибутивов Linux, которые поддерживаются в Azure:</span><span class="sxs-lookup"><span data-stu-id="87d37-153">hello following articles guide you through how tooprepare hello various Linux distributions that are supported on Azure:</span></span>

* <span data-ttu-id="87d37-154">**[Дистрибутивы на основе CentOS](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="87d37-154">**[CentOS-based Distributions](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="87d37-155">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="87d37-155">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="87d37-156">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="87d37-156">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="87d37-157">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="87d37-157">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="87d37-158">**[SLES и OpenSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="87d37-158">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="87d37-159">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="87d37-159">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="87d37-160">**[Прочее — нерекомендованные дистрибутивы](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="87d37-160">**[Other - Non-Endorsed Distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

<span data-ttu-id="87d37-161">См. также hello  **[замечания по установке Linux](create-upload-generic.md#general-linux-installation-notes)**  Общие рекомендации по подготовке образов Linux для Azure.</span><span class="sxs-lookup"><span data-stu-id="87d37-161">Also see hello **[Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="87d37-162">Hello [платформы Azure соглашения об уровне ОБСЛУЖИВАНИЯ](https://azure.microsoft.com/support/legal/sla/virtual-machines/) применяется tooVMs под управлением Linux, если один из hello одобренных распределения используется с данными конфигурации hello, как указано в списке поддерживаемых версиях только в [Linux в одобренных Azure Распределения](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="87d37-162">hello [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies tooVMs running Linux only when one of hello endorsed distributions is used with hello configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="create-a-resource-group"></a><span data-ttu-id="87d37-163">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="87d37-163">Create a resource group</span></span>
<span data-ttu-id="87d37-164">Группы ресурсов логически объединить все toosupport ресурсы Azure hello виртуальных машин, например hello виртуальных сетей и хранилища.</span><span class="sxs-lookup"><span data-stu-id="87d37-164">Resource groups logically bring together all hello Azure resources toosupport your virtual machines, such as hello virtual networking and storage.</span></span> <span data-ttu-id="87d37-165">Узнайте больше о группах ресурсов Azure [здесь](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="87d37-165">Read more about [Azure resource groups here](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="87d37-166">Перед загрузкой вашего пользовательского образа и создании виртуальных машин, необходимо сначала toocreate группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="87d37-166">Before uploading your custom disk image and creating VMs, you first need toocreate a resource group.</span></span> 

<span data-ttu-id="87d37-167">Hello следующий пример создает группу ресурсов с именем `myResourceGroup` в hello `WestUS` расположение:</span><span class="sxs-lookup"><span data-stu-id="87d37-167">hello following example creates a resource group named `myResourceGroup` in hello `WestUS` location:</span></span>

```azurecli
azure group create myResourceGroup --location "WestUS"
```

## <a name="create-a-storage-account"></a><span data-ttu-id="87d37-168">Создайте учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="87d37-168">Create a storage account</span></span>
<span data-ttu-id="87d37-169">Виртуальные машины хранятся в виде страничных BLOB-объектов в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="87d37-169">VMs are stored as page blobs within a storage account.</span></span> <span data-ttu-id="87d37-170">Узнайте больше о хранилище BLOB-объектов Azure [здесь](../../storage/common/storage-introduction.md#blob-storage).</span><span class="sxs-lookup"><span data-stu-id="87d37-170">Read more about [Azure blob storage here](../../storage/common/storage-introduction.md#blob-storage).</span></span> <span data-ttu-id="87d37-171">Следует создать учетную запись хранения для пользовательского образа диска и виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="87d37-171">You create a storage account for your custom disk image and VMs.</span></span> <span data-ttu-id="87d37-172">Все виртуальные машины, создаваемые на основе toobe необходимость образ вашего пользовательского диска, в hello одной учетной записи хранилища, что это изображение.</span><span class="sxs-lookup"><span data-stu-id="87d37-172">Any VMs that you create from your custom disk image need toobe in hello same storage account as that image.</span></span>

<span data-ttu-id="87d37-173">Hello следующий пример создает учетную запись хранения с именем `mystorageaccount` в ранее созданную группу ресурсов hello:</span><span class="sxs-lookup"><span data-stu-id="87d37-173">hello following example creates a storage account named `mystorageaccount` in hello resource group previously created:</span></span>

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

## <a name="list-storage-account-keys"></a><span data-ttu-id="87d37-174">Вывод списка ключей учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="87d37-174">List storage account keys</span></span>
<span data-ttu-id="87d37-175">Azure создает два 512-разрядных ключа доступа для каждой учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="87d37-175">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="87d37-176">Эти ключи доступа используются при проверке подлинности учетной записи хранилища toohello, например toocarry операций записи.</span><span class="sxs-lookup"><span data-stu-id="87d37-176">These access keys are used when authenticating toohello storage account, such as toocarry out write operations.</span></span> <span data-ttu-id="87d37-177">Дополнительные сведения о [управление доступ здесь toostorage](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="87d37-177">Read more about [managing access toostorage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="87d37-178">Можно просмотреть ключи доступа с hello `azure storage account keys list` команды.</span><span class="sxs-lookup"><span data-stu-id="87d37-178">You can view access keys with hello `azure storage account keys list` command.</span></span>

<span data-ttu-id="87d37-179">Просмотр ключей доступа к hello для hello хранилища созданную учетную запись:</span><span class="sxs-lookup"><span data-stu-id="87d37-179">View hello access keys for hello storage account you created:</span></span>

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
```

<span data-ttu-id="87d37-180">Hello выходные данные выглядят аналогично:</span><span class="sxs-lookup"><span data-stu-id="87d37-180">hello output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK

```
<span data-ttu-id="87d37-181">Запомните или запишите `key1` как он будет использоваться toointeract с вашей учетной записи хранения в hello дальнейшие действия.</span><span class="sxs-lookup"><span data-stu-id="87d37-181">Make a note of `key1` as you will use it toointeract with your storage account in hello next steps.</span></span>

## <a name="create-a-storage-container"></a><span data-ttu-id="87d37-182">Создание контейнера хранилища</span><span class="sxs-lookup"><span data-stu-id="87d37-182">Create a storage container</span></span>
<span data-ttu-id="87d37-183">В hello так же, создания разных каталогах toologically организации локальной файловой системе, создание контейнеров в учетной записи хранилища tooorganize виртуальных дисков и образов.</span><span class="sxs-lookup"><span data-stu-id="87d37-183">In hello same way that you create different directories toologically organize your local file system, you create containers within a storage account tooorganize your virtual disks and images.</span></span> <span data-ttu-id="87d37-184">Учетная запись хранения может содержать любое количество контейнеров.</span><span class="sxs-lookup"><span data-stu-id="87d37-184">A storage account can contain any number of containers.</span></span> 

<span data-ttu-id="87d37-185">Hello следующий пример создает контейнер с именем `myimages`, указав ключ доступа hello полученный в предыдущем шаге hello (`key1`):</span><span class="sxs-lookup"><span data-stu-id="87d37-185">hello following example creates a container named `myimages`, specifying hello access key obtained in hello previous step (`key1`):</span></span>

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

## <a name="upload-vhd"></a><span data-ttu-id="87d37-186">Передача VHD</span><span class="sxs-lookup"><span data-stu-id="87d37-186">Upload VHD</span></span>
<span data-ttu-id="87d37-187">Теперь можно передать ваш пользовательский образ диска.</span><span class="sxs-lookup"><span data-stu-id="87d37-187">Now you can actually upload your custom disk image.</span></span> <span data-ttu-id="87d37-188">Как и любые виртуальные диски виртуальных машин, ваш пользовательский образ диска передается и сохраняется как страничный BLOB-объект.</span><span class="sxs-lookup"><span data-stu-id="87d37-188">As with all virtual disks used by VMs, you upload and store your custom disk image as a page blob.</span></span>

<span data-ttu-id="87d37-189">Укажите ваш ключ доступа, контейнер hello, созданный на предыдущем шаге hello и затем hello путь toohello пользовательского образа на локальном компьютере:</span><span class="sxs-lookup"><span data-stu-id="87d37-189">Specify your access key, hello container you created in hello previous step, and then hello path toohello custom disk image on your local computer:</span></span>

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

## <a name="create-vm-from-custom-image"></a><span data-ttu-id="87d37-190">Создание виртуальной машины на основе пользовательского образа</span><span class="sxs-lookup"><span data-stu-id="87d37-190">Create VM from custom image</span></span>
<span data-ttu-id="87d37-191">При создании виртуальных машин из вашего пользовательского образа, укажите образ диска toohello URI hello.</span><span class="sxs-lookup"><span data-stu-id="87d37-191">When you create VMs from your custom disk image, specify hello URI toohello disk image.</span></span> <span data-ttu-id="87d37-192">Убедитесь, что hello совпадений учетной записи хранилища назначения, где хранится образ жесткого диска для пользовательских.</span><span class="sxs-lookup"><span data-stu-id="87d37-192">Ensure that hello destination storage account matches where your custom disk image is stored.</span></span> <span data-ttu-id="87d37-193">Можно создать с помощью hello Azure CLI или JSON диспетчера ресурсов шаблона виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="87d37-193">You can create your VM using hello Azure CLI or Resource Manager JSON template.</span></span>

### <a name="create-a-vm-using-hello-azure-cli"></a><span data-ttu-id="87d37-194">Создайте виртуальную Машину с помощью hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="87d37-194">Create a VM using hello Azure CLI</span></span>
<span data-ttu-id="87d37-195">Укажите hello `--image-urn` параметр с hello `azure vm create` toopoint команда tooyour пользовательского образа.</span><span class="sxs-lookup"><span data-stu-id="87d37-195">You specify hello `--image-urn` parameter with hello `azure vm create` command toopoint tooyour custom disk image.</span></span> <span data-ttu-id="87d37-196">Убедитесь, что `--storage-account-name` совпадений hello учетной записи хранилища, где хранится образ жесткого диска пользовательских.</span><span class="sxs-lookup"><span data-stu-id="87d37-196">Ensure that `--storage-account-name` matches hello storage account where your custom disk image is stored.</span></span> <span data-ttu-id="87d37-197">У вас toouse hello одного контейнера как hello toostore изображение пользовательского диска виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="87d37-197">You do not have toouse hello same container as hello custom disk image toostore your VMs.</span></span> <span data-ttu-id="87d37-198">Внесите любые дополнительные контейнеры toocreate убедиться, что в hello так же, как hello ранее перед отправкой диска пользовательских изображений.</span><span class="sxs-lookup"><span data-stu-id="87d37-198">Make sure toocreate any additional containers in hello same way as hello earlier steps before uploading your custom disk images.</span></span>

<span data-ttu-id="87d37-199">Hello следующий пример создает Виртуальную машину с именем `myVM` из вашего пользовательского образа:</span><span class="sxs-lookup"><span data-stu-id="87d37-199">hello following example creates a VM named `myVM` from your custom disk image:</span></span>

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
    --storage-account-name mystorageaccount
```

<span data-ttu-id="87d37-200">Вы по-прежнему требуется toospecify или ответить на запрос, все hello Дополнительные параметры, необходимые для hello `azure vm create` команды, такие как виртуальная сеть, общедоступный IP-адрес, имя пользователя и ключи SSH.</span><span class="sxs-lookup"><span data-stu-id="87d37-200">You still need toospecify, or answer prompts for, all hello additional parameters required by hello `azure vm create` command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="87d37-201">Дополнительные сведения о hello [доступных параметров диспетчера ресурсов CLI](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="87d37-201">Read more about hello [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

### <a name="create-a-vm-using-a-json-template"></a><span data-ttu-id="87d37-202">Создание виртуальной машины с помощью шаблона JSON</span><span class="sxs-lookup"><span data-stu-id="87d37-202">Create a VM using a JSON template</span></span>
<span data-ttu-id="87d37-203">Шаблоны Azure Resource Manager являются файлами JavaScript Object Notation (JSON), которые определяют среду hello нужно toobuild.</span><span class="sxs-lookup"><span data-stu-id="87d37-203">Azure Resource Manager templates are JavaScript Object Notation (JSON) files that define hello environment you wish toobuild.</span></span> <span data-ttu-id="87d37-204">шаблоны Hello разбиваются toodifferent поставщиков ресурсов, таких как вычислений или сети.</span><span class="sxs-lookup"><span data-stu-id="87d37-204">hello templates are broken down in toodifferent resource providers such as compute or network.</span></span> <span data-ttu-id="87d37-205">Можно использовать существующие шаблоны или создать собственный.</span><span class="sxs-lookup"><span data-stu-id="87d37-205">You can use existing templates or write your own.</span></span> <span data-ttu-id="87d37-206">Узнайте больше об [использовании Resource Manager и шаблонов](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="87d37-206">Read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="87d37-207">В рамках hello `Microsoft.Compute/virtualMachines` у поставщика шаблона `storageProfile` узел, который содержит сведения о конфигурации hello для виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="87d37-207">Within hello `Microsoft.Compute/virtualMachines` provider of your template, you have a `storageProfile` node that contains hello configuration details for your VM.</span></span> <span data-ttu-id="87d37-208">tooedit Hello двумя основными параметрами, которые являются hello `image` и `vhd` URI, которые точки tooyour пользовательского образа и новой виртуальной Машины виртуальный диск.</span><span class="sxs-lookup"><span data-stu-id="87d37-208">hello two main parameters tooedit are hello `image` and `vhd` URIs that point tooyour custom disk image and your new VM's virtual disk.</span></span> <span data-ttu-id="87d37-209">Hello ниже показан пример hello JSON с помощью пользовательского образа:</span><span class="sxs-lookup"><span data-stu-id="87d37-209">hello following shows an example of hello JSON for using a custom disk image:</span></span>

```json
"storageProfile": {
          "osDisk": {
            "name": "myVM",
            "osType": "Linux",
            "caching": "ReadWrite",
            "createOption": "FromImage",
            "image": {
              "uri": "https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd"
            },
            "vhd": {
              "uri": "https://mystorageaccount.blob.core.windows.net/vhds/newvmname.vhd"
            }
          }
```

<span data-ttu-id="87d37-210">Можно использовать [toocreate этот существующий шаблон виртуальной Машины из образа](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) или для чтения о [Создание собственных шаблонов диспетчера ресурсов Azure](../../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="87d37-210">You can use [this existing template toocreate a VM from a custom image](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) or read about [creating your own Azure Resource Manager templates](../../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 

<span data-ttu-id="87d37-211">После настройки шаблона, создания виртуальных машин с помощью hello `azure group deployment create` команды.</span><span class="sxs-lookup"><span data-stu-id="87d37-211">Once you have a template configured, you create your VMs using hello `azure group deployment create` command.</span></span> <span data-ttu-id="87d37-212">Укажите hello URI шаблона JSON с hello `--template-uri` параметр:</span><span class="sxs-lookup"><span data-stu-id="87d37-212">Specify hello URI of your JSON template with hello `--template-uri` parameter:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-uri https://uri.to.template/mytemplate.json
```

<span data-ttu-id="87d37-213">Если имеется файл JSON, хранящиеся локально на компьютере, можно использовать hello `--template-file` параметра вместо:</span><span class="sxs-lookup"><span data-stu-id="87d37-213">If you have a JSON file stored locally on your computer, you can use hello `--template-file` parameter instead:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a><span data-ttu-id="87d37-214">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="87d37-214">Next steps</span></span>
<span data-ttu-id="87d37-215">После подготовки и передачи пользовательского виртуального диска ознакомьтесь с дополнительными сведениями об [использовании Resource Manager и шаблонов](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="87d37-215">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="87d37-216">Вы также можете слишком[добавьте диск данных](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour новые виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="87d37-216">You may also want too[add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour new VMs.</span></span> <span data-ttu-id="87d37-217">При наличии приложений, выполняющихся на виртуальные машины, необходимо tooaccess, нужно убедиться, что слишком[открыть порты и конечные точки](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="87d37-217">If you have applications running on your VMs that you need tooaccess, be sure too[open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

