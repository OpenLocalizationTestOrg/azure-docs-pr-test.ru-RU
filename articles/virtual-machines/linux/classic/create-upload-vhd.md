---
title: "aaaCreate и отправка tooAzure виртуального жесткого диска Linux | Документы Microsoft"
description: "Создание и отправка в Azure виртуального жесткого диска (VHD), содержащий hello Linux операционной системы с помощью hello классической модели развертывания"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8058ff98-db03-4309-9bf4-69842bd64dd4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: iainfou
ms.openlocfilehash: 77b01316386c4a6eb68c129fa68d42f0a8996edc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="creating-and-uploading-a-virtual-hard-disk-that-contains-hello-linux-operating-system"></a><span data-ttu-id="de7d6-103">Создание и загрузка виртуального жесткого диска, который содержит hello операционной системы Linux</span><span class="sxs-lookup"><span data-stu-id="de7d6-103">Creating and Uploading a Virtual Hard Disk that Contains hello Linux Operating System</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="de7d6-104">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="de7d6-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="de7d6-105">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="de7d6-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="de7d6-106">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="de7d6-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="de7d6-107">Вы можете также [передать пользовательский образ с помощью Azure Resource Manager](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="de7d6-107">You can also [upload a custom disk image using Azure Resource Manager](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="de7d6-108">В этой статье показано, как toocreate и передача виртуального жесткого диска (VHD), поэтому ее можно использовать в качестве собственного образа toocreate виртуальных машин в Azure.</span><span class="sxs-lookup"><span data-stu-id="de7d6-108">This article shows you how toocreate and upload a virtual hard disk (VHD) so you can use it as your own image toocreate virtual machines in Azure.</span></span> <span data-ttu-id="de7d6-109">Узнайте, как tooprepare hello операционной системы, чтобы вы могли использовать toocreate нескольких виртуальных машин на основе этого образа.</span><span class="sxs-lookup"><span data-stu-id="de7d6-109">Learn how tooprepare hello operating system so you can use it toocreate multiple virtual machines based on that image.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="de7d6-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="de7d6-110">Prerequisites</span></span>
<span data-ttu-id="de7d6-111">В этой статье предполагается, что hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="de7d6-111">This article assumes that you have hello following items:</span></span>

* <span data-ttu-id="de7d6-112">**Операционной системы Linux в VHD-файла** -установки [дистрибутив Linux в одобренных Azure](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (или в разделе [сведения для распределений, отличных от одобренных](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa виртуального диска в формате VHD hello.</span><span class="sxs-lookup"><span data-stu-id="de7d6-112">**Linux operating system installed in a .vhd file** - You have installed an [Azure-endorsed Linux distribution](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtual disk in hello VHD format.</span></span> <span data-ttu-id="de7d6-113">Несколько средств существует toocreate виртуальной Машины и виртуального жесткого диска:</span><span class="sxs-lookup"><span data-stu-id="de7d6-113">Multiple tools exist toocreate a VM and VHD:</span></span>
  * <span data-ttu-id="de7d6-114">Установка и настройка [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) или [KVM](http://www.linux-kvm.org/page/RunningKVM), отвечающий за toouse виртуальный жесткий ДИСК в формате изображения.</span><span class="sxs-lookup"><span data-stu-id="de7d6-114">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care toouse VHD as your image format.</span></span> <span data-ttu-id="de7d6-115">При необходимости вы можете [преобразовать образ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) с помощью `qemu-img convert`.</span><span class="sxs-lookup"><span data-stu-id="de7d6-115">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="de7d6-116">Кроме того, можно использовать Hyper-V [в Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) или [Windows Server 2012 и 2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="de7d6-116">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="de7d6-117">Hello более новый формат VHDX не поддерживается в Azure.</span><span class="sxs-lookup"><span data-stu-id="de7d6-117">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="de7d6-118">При создании виртуальной Машины, задайте hello формат виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="de7d6-118">When you create a VM, specify VHD as hello format.</span></span> <span data-ttu-id="de7d6-119">При необходимости можно преобразовать tooVHD диски VHDX с помощью [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) или hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) командлета PowerShell.</span><span class="sxs-lookup"><span data-stu-id="de7d6-119">If needed, you can convert VHDX disks tooVHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or hello [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="de7d6-120">Кроме того Azure не поддерживает передачи динамических виртуальных жестких дисков, поэтому требуется tooconvert toostatic такие диски VHD перед отправкой.</span><span class="sxs-lookup"><span data-stu-id="de7d6-120">Further, Azure does not support uploading dynamic VHDs, so you need tooconvert such disks toostatic VHDs before uploading.</span></span> <span data-ttu-id="de7d6-121">Можно использовать средства, такие как [утилиты Azure виртуального жесткого диска для GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert динамических дисков во время процесса hello передачи tooAzure.</span><span class="sxs-lookup"><span data-stu-id="de7d6-121">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamic disks during hello process of uploading tooAzure.</span></span>

* <span data-ttu-id="de7d6-122">**Интерфейс командной строки Azure** -последние hello установки [интерфейса командной строки Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooupload hello виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="de7d6-122">**Azure Command-line Interface** - Install hello latest [Azure Command-Line Interface](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooupload hello VHD.</span></span>

<span data-ttu-id="de7d6-123"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="de7d6-123"><a id="prepimage"> </a></span></span>

## <a name="step-1-prepare-hello-image-toobe-uploaded"></a><span data-ttu-id="de7d6-124">Шаг 1: Подготовка отправлен toobe изображения hello</span><span class="sxs-lookup"><span data-stu-id="de7d6-124">Step 1: Prepare hello image toobe uploaded</span></span>
<span data-ttu-id="de7d6-125">Azure поддерживает различные дистрибутивы Linux (см. раздел [Рекомендованные дистрибутивы](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="de7d6-125">Azure supports various Linux distributions (see [Endorsed Distributions](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="de7d6-126">следующие статьи Hello начнется как tooprepare hello различных дистрибутивов Linux, которые поддерживаются в Azure.</span><span class="sxs-lookup"><span data-stu-id="de7d6-126">hello following articles guide you through how tooprepare hello various Linux distributions that are supported on Azure.</span></span> <span data-ttu-id="de7d6-127">После выполнения шагов hello в следующие руководства hello, могут быть вернитесь сюда, получив файл виртуального жесткого диска, готовы tooupload tooAzure:</span><span class="sxs-lookup"><span data-stu-id="de7d6-127">After you complete hello steps in hello following guides, come back here once you have a VHD file that is ready tooupload tooAzure:</span></span>

* <span data-ttu-id="de7d6-128">**[Дистрибутивы на основе CentOS](../create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="de7d6-128">**[CentOS-based Distributions](../create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="de7d6-129">**[Debian Linux](../debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="de7d6-129">**[Debian Linux](../debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="de7d6-130">**[Oracle Linux](../oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="de7d6-130">**[Oracle Linux](../oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="de7d6-131">**[Red Hat Enterprise Linux](../redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="de7d6-131">**[Red Hat Enterprise Linux](../redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="de7d6-132">**[SLES и OpenSUSE](../suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="de7d6-132">**[SLES & openSUSE](../suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="de7d6-133">**[Ubuntu](../create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="de7d6-133">**[Ubuntu](../create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="de7d6-134">**[Прочее — нерекомендованные дистрибутивы](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="de7d6-134">**[Other - Non-Endorsed Distributions](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

> [!NOTE]
> <span data-ttu-id="de7d6-135">Hello соглашения об уровне ОБСЛУЖИВАНИЯ платформы Azure применяется toovirtual компьютеров под управлением ОС Linux только в том случае, если один из hello одобренных распределения используется с hello сведения о конфигурации, как указано в списке поддерживаемых версиях hello [Linux в распределениях Azure-Endorsed ](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="de7d6-135">hello Azure platform SLA applies toovirtual machines running hello Linux OS only when one of hello endorsed distributions is used with hello configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="de7d6-136">Все дистрибутивы Linux в коллекции образов Azure hello являются индоссированный распределения с требуемой конфигурацией hello.</span><span class="sxs-lookup"><span data-stu-id="de7d6-136">All Linux distributions in hello Azure image gallery are endorsed distributions with hello required configuration.</span></span>
> 
> 

<span data-ttu-id="de7d6-137">См. также hello  **[замечания по установке Linux](../create-upload-generic.md#general-linux-installation-notes)**  Общие рекомендации по подготовке образов Linux для Azure.</span><span class="sxs-lookup"><span data-stu-id="de7d6-137">Also see hello **[Linux Installation Notes](../create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

<span data-ttu-id="de7d6-138"><a id="connect"> </a></span><span class="sxs-lookup"><span data-stu-id="de7d6-138"><a id="connect"> </a></span></span>

## <a name="step-2-prepare-hello-connection-tooazure"></a><span data-ttu-id="de7d6-139">Шаг 2: Подготовка tooAzure подключения hello</span><span class="sxs-lookup"><span data-stu-id="de7d6-139">Step 2: Prepare hello connection tooAzure</span></span>
<span data-ttu-id="de7d6-140">Убедитесь, что вы используете hello Azure CLI в hello классической модели развертывания (`azure config mode asm`), затем войдите в учетную запись tooyour:</span><span class="sxs-lookup"><span data-stu-id="de7d6-140">Make sure you are using hello Azure CLI in hello classic deployment model (`azure config mode asm`), then log in tooyour account:</span></span>

```azurecli
azure login
```


<span data-ttu-id="de7d6-141"><a id="upload"> </a></span><span class="sxs-lookup"><span data-stu-id="de7d6-141"><a id="upload"> </a></span></span>

## <a name="step-3-upload-hello-image-tooazure"></a><span data-ttu-id="de7d6-142">Шаг 3: Отправка tooAzure изображения hello</span><span class="sxs-lookup"><span data-stu-id="de7d6-142">Step 3: Upload hello image tooAzure</span></span>
<span data-ttu-id="de7d6-143">Необходимо tooupload учетной записи хранения файла виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="de7d6-143">You need a storage account tooupload your VHD file to.</span></span> <span data-ttu-id="de7d6-144">Можно выбрать существующую учетную запись хранения или [создать новую](../../../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="de7d6-144">You can either pick an existing storage account or [create a new one](../../../storage/common/storage-create-storage-account.md).</span></span>

<span data-ttu-id="de7d6-145">Используйте hello Azure CLI tooupload hello образ с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="de7d6-145">Use hello Azure CLI tooupload hello image by using hello following command:</span></span>

```azurecli
azure vm image create <ImageName> `
    --blob-url <BlobStorageURL>/<YourImagesFolder>/<VHDName> `
    --os Linux <PathToVHDFile>
```

<span data-ttu-id="de7d6-146">В предыдущем примере hello:</span><span class="sxs-lookup"><span data-stu-id="de7d6-146">In hello previous example:</span></span>

* <span data-ttu-id="de7d6-147">**BlobStorageURL** hello URL-адрес для учетной записи хранения hello планирование toouse</span><span class="sxs-lookup"><span data-stu-id="de7d6-147">**BlobStorageURL** is hello URL for hello storage account you plan toouse</span></span>
* <span data-ttu-id="de7d6-148">**YourImagesFolder** — контейнер hello в хранилище больших двоичных объектов, место toostore изображений</span><span class="sxs-lookup"><span data-stu-id="de7d6-148">**YourImagesFolder** is hello container within blob storage where you want toostore your images</span></span>
* <span data-ttu-id="de7d6-149">**VHDName** — hello метка, которая отображается в портале tooidentify hello виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="de7d6-149">**VHDName** is hello label that appears in portal tooidentify hello virtual hard disk.</span></span>
* <span data-ttu-id="de7d6-150">**PathToVHDFile** hello полный путь и имя hello VHD-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="de7d6-150">**PathToVHDFile** is hello full path and name of hello .vhd file on your machine.</span></span>

<span data-ttu-id="de7d6-151">Следующая команда Hello приведен пример:</span><span class="sxs-lookup"><span data-stu-id="de7d6-151">hello following command shows a complete example:</span></span>

```azurecli
azure vm image create myImage `
    --blob-url https://mystorage.blob.core.windows.net/vhds/myimage.vhd `
    --os Linux /home/ahmet/myimage.vhd
```

## <a name="step-4-create-a-vm-from-hello-image"></a><span data-ttu-id="de7d6-152">Шаг 4: Создайте виртуальную Машину из образа hello</span><span class="sxs-lookup"><span data-stu-id="de7d6-152">Step 4: Create a VM from hello image</span></span>
<span data-ttu-id="de7d6-153">Создание виртуальной Машины с помощью `azure vm create` в hello так же, как обычный виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="de7d6-153">You create a VM using `azure vm create` in hello same way as a regular VM.</span></span> <span data-ttu-id="de7d6-154">Укажите имя hello Вы дали образа на предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="de7d6-154">Specify hello name you gave your image in hello previous step.</span></span> <span data-ttu-id="de7d6-155">В следующем примере hello, мы используем hello **myImage** имя изображения, указанного в предыдущем шаге hello:</span><span class="sxs-lookup"><span data-stu-id="de7d6-155">In hello following example, we use hello **myImage** image name given in hello previous step:</span></span>

```azurecli
azure vm create --userName ops --password P@ssw0rd! --vm-size Small --ssh `
    --location "West US" "myDeployedVM" myImage
```

<span data-ttu-id="de7d6-156">toocreate собственные виртуальные машины предоставляют свои собственные пользователя + пароль, расположение, DNS-имя и имя образа.</span><span class="sxs-lookup"><span data-stu-id="de7d6-156">toocreate your own VMs, provide your own username + password, location, DNS name, and image name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="de7d6-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="de7d6-157">Next steps</span></span>
<span data-ttu-id="de7d6-158">Дополнительные сведения см. в разделе [ссылку Azure CLI для hello Azure классической модели развертывания](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="de7d6-158">For more information, see [Azure CLI reference for hello Azure classic deployment model](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

[Step 1: Prepare hello image toobe uploaded]:#prepimage
[Step 2: Prepare hello connection tooAzure]:#connect
[Step 3: Upload hello image tooAzure]:#upload
