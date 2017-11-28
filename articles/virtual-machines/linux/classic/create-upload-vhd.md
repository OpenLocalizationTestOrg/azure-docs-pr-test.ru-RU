---
title: "Создание и передача виртуального жесткого диска Linux в Azure | Документация Майкрософт"
description: "Создание и передача виртуального жесткого диска Azure, содержащего операционную систему Linux, с использованием классической модели развертывания."
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
ms.openlocfilehash: 23c30c954875598ce3e01db137b0ef8cda9779f4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="creating-and-uploading-a-virtual-hard-disk-that-contains-the-linux-operating-system"></a><span data-ttu-id="488fa-103">Создание и передача виртуального жесткого диска с операционной системой Linux</span><span class="sxs-lookup"><span data-stu-id="488fa-103">Creating and Uploading a Virtual Hard Disk that Contains the Linux Operating System</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="488fa-104">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="488fa-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="488fa-105">В этой статье рассматривается использование классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="488fa-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="488fa-106">Для большинства новых развертываний Майкрософт рекомендует использовать модель диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="488fa-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="488fa-107">Вы можете также [передать пользовательский образ с помощью Azure Resource Manager](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="488fa-107">You can also [upload a custom disk image using Azure Resource Manager](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="488fa-108">В этой статье показано, как создать и передать виртуальный жесткий диск (VHD-файл), чтобы использовать его в качестве образа для создания виртуальных машин в Azure.</span><span class="sxs-lookup"><span data-stu-id="488fa-108">This article shows you how to create and upload a virtual hard disk (VHD) so you can use it as your own image to create virtual machines in Azure.</span></span> <span data-ttu-id="488fa-109">Узнайте, как подготовить операционную систему, чтобы использовать ее в качестве образа для создания нескольких виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="488fa-109">Learn how to prepare the operating system so you can use it to create multiple virtual machines based on that image.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="488fa-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="488fa-110">Prerequisites</span></span>
<span data-ttu-id="488fa-111">В данной статье предполагается, что у вас есть следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="488fa-111">This article assumes that you have the following items:</span></span>

* <span data-ttu-id="488fa-112">**Операционная система Linux, установленная в VHD-файле**. Вы установили [рекомендуемый для Azure дистрибутив Linux](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (или ознакомьтесь с [информацией о нерекомендованных дистрибутивах](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) на виртуальный диск в формате VHD.</span><span class="sxs-lookup"><span data-stu-id="488fa-112">**Linux operating system installed in a .vhd file** - You have installed an [Azure-endorsed Linux distribution](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) to a virtual disk in the VHD format.</span></span> <span data-ttu-id="488fa-113">Для создания VHD-файлов существует несколько средств.</span><span class="sxs-lookup"><span data-stu-id="488fa-113">Multiple tools exist to create a VM and VHD:</span></span>
  * <span data-ttu-id="488fa-114">Установите и настройте [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) или [KVM](http://www.linux-kvm.org/page/RunningKVM), используя VHD в качестве формата образа.</span><span class="sxs-lookup"><span data-stu-id="488fa-114">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care to use VHD as your image format.</span></span> <span data-ttu-id="488fa-115">При необходимости вы можете [преобразовать образ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) с помощью `qemu-img convert`.</span><span class="sxs-lookup"><span data-stu-id="488fa-115">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="488fa-116">Кроме того, можно использовать Hyper-V [в Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) или [Windows Server 2012 и 2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="488fa-116">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="488fa-117">Более новый формат VHDX не поддерживается в Azure.</span><span class="sxs-lookup"><span data-stu-id="488fa-117">The newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="488fa-118">При создании виртуальной машины укажите формат VHD.</span><span class="sxs-lookup"><span data-stu-id="488fa-118">When you create a VM, specify VHD as the format.</span></span> <span data-ttu-id="488fa-119">При необходимости можно преобразовать диски VHDX в диски VHD с помощью командлета PowerShell [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) или [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx).</span><span class="sxs-lookup"><span data-stu-id="488fa-119">If needed, you can convert VHDX disks to VHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or the [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="488fa-120">Кроме того, Azure не поддерживает отправку динамических дисков VHD, поэтому перед отправкой необходимо преобразовать такие диски в статические диски VHD.</span><span class="sxs-lookup"><span data-stu-id="488fa-120">Further, Azure does not support uploading dynamic VHDs, so you need to convert such disks to static VHDs before uploading.</span></span> <span data-ttu-id="488fa-121">Для преобразования динамических дисков во время передачи в Azure можно использовать [служебные программы Azure VHD для GO](https://github.com/Microsoft/azure-vhd-utils-for-go) .</span><span class="sxs-lookup"><span data-stu-id="488fa-121">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) to convert dynamic disks during the process of uploading to Azure.</span></span>

* <span data-ttu-id="488fa-122">**Интерфейс командной строки Azure**. Установите последнюю версию [интерфейса командной строки Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) для передачи VHD-файлов.</span><span class="sxs-lookup"><span data-stu-id="488fa-122">**Azure Command-line Interface** - Install the latest [Azure Command-Line Interface](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) to upload the VHD.</span></span>

<span data-ttu-id="488fa-123"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="488fa-123"><a id="prepimage"> </a></span></span>

## <a name="step-1-prepare-the-image-to-be-uploaded"></a><span data-ttu-id="488fa-124">Шаг 1. Подготовка образа для передачи</span><span class="sxs-lookup"><span data-stu-id="488fa-124">Step 1: Prepare the image to be uploaded</span></span>
<span data-ttu-id="488fa-125">Azure поддерживает различные дистрибутивы Linux (см. раздел [Рекомендованные дистрибутивы](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="488fa-125">Azure supports various Linux distributions (see [Endorsed Distributions](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="488fa-126">В следующих статьях описывается подготовка различных дистрибутивов Linux, которые поддерживаются в Azure.</span><span class="sxs-lookup"><span data-stu-id="488fa-126">The following articles guide you through how to prepare the various Linux distributions that are supported on Azure.</span></span> <span data-ttu-id="488fa-127">После выполнения указаний, описанных в приведенных ниже руководствах, вернитесь сюда. У вас уже будет VHD-файл для передачи в Azure.</span><span class="sxs-lookup"><span data-stu-id="488fa-127">After you complete the steps in the following guides, come back here once you have a VHD file that is ready to upload to Azure:</span></span>

* <span data-ttu-id="488fa-128">**[Дистрибутивы на основе CentOS](../create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="488fa-128">**[CentOS-based Distributions](../create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="488fa-129">**[Debian Linux](../debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="488fa-129">**[Debian Linux](../debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="488fa-130">**[Oracle Linux](../oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="488fa-130">**[Oracle Linux](../oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="488fa-131">**[Red Hat Enterprise Linux](../redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="488fa-131">**[Red Hat Enterprise Linux](../redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="488fa-132">**[SLES и OpenSUSE](../suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="488fa-132">**[SLES & openSUSE](../suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="488fa-133">**[Ubuntu](../create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="488fa-133">**[Ubuntu](../create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="488fa-134">**[Прочее — нерекомендованные дистрибутивы](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="488fa-134">**[Other - Non-Endorsed Distributions](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

> [!NOTE]
> <span data-ttu-id="488fa-135">Соглашение об уровне обслуживания платформы Azure применяется к виртуальным машинам, работающим под управлением Linux, только если используется один из рекомендуемых дистрибутивов с конфигурацией, указанной в разделе "Поддерживаемые дистрибутивы и версии" статьи [Linux в Azure — рекомендованные дистрибутивы](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="488fa-135">The Azure platform SLA applies to virtual machines running the Linux OS only when one of the endorsed distributions is used with the configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="488fa-136">Все дистрибутивы Linux в коллекции образов Azure — это рекомендуемые дистрибутивы, уже имеющие необходимую конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="488fa-136">All Linux distributions in the Azure image gallery are endorsed distributions with the required configuration.</span></span>
> 
> 

<span data-ttu-id="488fa-137">Другие общие советы по подготовке образов Linux для Azure см. в разделе **[Общие замечания по установке Linux](../create-upload-generic.md#general-linux-installation-notes)**.</span><span class="sxs-lookup"><span data-stu-id="488fa-137">Also see the **[Linux Installation Notes](../create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

<span data-ttu-id="488fa-138"><a id="connect"> </a></span><span class="sxs-lookup"><span data-stu-id="488fa-138"><a id="connect"> </a></span></span>

## <a name="step-2-prepare-the-connection-to-azure"></a><span data-ttu-id="488fa-139">Шаг 2. Подготовка подключения к Azure</span><span class="sxs-lookup"><span data-stu-id="488fa-139">Step 2: Prepare the connection to Azure</span></span>
<span data-ttu-id="488fa-140">Убедитесь, что вы используете интерфейс командной строки Azure в классической модели развертывания (`azure config mode asm`), а затем войдите со своей учетной записью.</span><span class="sxs-lookup"><span data-stu-id="488fa-140">Make sure you are using the Azure CLI in the classic deployment model (`azure config mode asm`), then log in to your account:</span></span>

```azurecli
azure login
```


<span data-ttu-id="488fa-141"><a id="upload"> </a></span><span class="sxs-lookup"><span data-stu-id="488fa-141"><a id="upload"> </a></span></span>

## <a name="step-3-upload-the-image-to-azure"></a><span data-ttu-id="488fa-142">Шаг 3. Передача образа в Azure</span><span class="sxs-lookup"><span data-stu-id="488fa-142">Step 3: Upload the image to Azure</span></span>
<span data-ttu-id="488fa-143">Для передачи VHD-файла нужна учетная запись хранения.</span><span class="sxs-lookup"><span data-stu-id="488fa-143">You need a storage account to upload your VHD file to.</span></span> <span data-ttu-id="488fa-144">Можно выбрать существующую учетную запись хранения или [создать новую](../../../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="488fa-144">You can either pick an existing storage account or [create a new one](../../../storage/common/storage-create-storage-account.md).</span></span>

<span data-ttu-id="488fa-145">Для передачи образа выполните следующую команду в командной строке Azure:</span><span class="sxs-lookup"><span data-stu-id="488fa-145">Use the Azure CLI to upload the image by using the following command:</span></span>

```azurecli
azure vm image create <ImageName> `
    --blob-url <BlobStorageURL>/<YourImagesFolder>/<VHDName> `
    --os Linux <PathToVHDFile>
```

<span data-ttu-id="488fa-146">В предыдущем примере:</span><span class="sxs-lookup"><span data-stu-id="488fa-146">In the previous example:</span></span>

* <span data-ttu-id="488fa-147">**BlobStorageURL** — URL-адрес для учетной записи хранения, которую вы планируете использовать.</span><span class="sxs-lookup"><span data-stu-id="488fa-147">**BlobStorageURL** is the URL for the storage account you plan to use</span></span>
* <span data-ttu-id="488fa-148">**YourImagesFolder** — контейнер внутри хранилища BLOB-объектов, где будут храниться образы.</span><span class="sxs-lookup"><span data-stu-id="488fa-148">**YourImagesFolder** is the container within blob storage where you want to store your images</span></span>
* <span data-ttu-id="488fa-149">**VHDName** — метка, которая отображается на портале для идентификации виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="488fa-149">**VHDName** is the label that appears in portal to identify the virtual hard disk.</span></span>
* <span data-ttu-id="488fa-150">**PathToVHDFile** — полный путь и имя VHD-файла на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="488fa-150">**PathToVHDFile** is the full path and name of the .vhd file on your machine.</span></span>

<span data-ttu-id="488fa-151">В следующей команде представлен полный пример:</span><span class="sxs-lookup"><span data-stu-id="488fa-151">The following command shows a complete example:</span></span>

```azurecli
azure vm image create myImage `
    --blob-url https://mystorage.blob.core.windows.net/vhds/myimage.vhd `
    --os Linux /home/ahmet/myimage.vhd
```

## <a name="step-4-create-a-vm-from-the-image"></a><span data-ttu-id="488fa-152">Шаг 4. Создание виртуальной машины из образа</span><span class="sxs-lookup"><span data-stu-id="488fa-152">Step 4: Create a VM from the image</span></span>
<span data-ttu-id="488fa-153">Создайте обычную виртуальную машину с помощью команды `azure vm create`.</span><span class="sxs-lookup"><span data-stu-id="488fa-153">You create a VM using `azure vm create` in the same way as a regular VM.</span></span> <span data-ttu-id="488fa-154">Укажите имя, присвоенное образу на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="488fa-154">Specify the name you gave your image in the previous step.</span></span> <span data-ttu-id="488fa-155">В следующем примере мы используем имя образа **myImage**, присвоенное на предыдущем шаге:</span><span class="sxs-lookup"><span data-stu-id="488fa-155">In the following example, we use the **myImage** image name given in the previous step:</span></span>

```azurecli
azure vm create --userName ops --password P@ssw0rd! --vm-size Small --ssh `
    --location "West US" "myDeployedVM" myImage
```

<span data-ttu-id="488fa-156">Для создания виртуальной машины следует указать свои имя пользователя и пароль, расположение, DNS-имя и имя образа.</span><span class="sxs-lookup"><span data-stu-id="488fa-156">To create your own VMs, provide your own username + password, location, DNS name, and image name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="488fa-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="488fa-157">Next steps</span></span>
<span data-ttu-id="488fa-158">Дополнительные сведения см. в [справочнике по Azure CLI для классической модели развертывания Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="488fa-158">For more information, see [Azure CLI reference for the Azure classic deployment model](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

[Step 1: Prepare the image to be uploaded]:#prepimage
[Step 2: Prepare the connection to Azure]:#connect
[Step 3: Upload the image to Azure]:#upload
