---
title: "Гости Linux на стек Azure | Документы Microsoft"
description: "Узнайте, как создать виртуальные машины под управлением Linux стек Azure."
services: azure-stack
documentationcenter: 
author: anjayajodha
manager: byronr
editor: 
ms.assetid: d2155c59-902e-4f63-ac58-d19e6a765380
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: anajod
ms.openlocfilehash: 935cd31c4b38262b7e42271574a8a221377a3cec
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-linux-virtual-machines-on-azure-stack"></a><span data-ttu-id="01d8f-103">Развертывание виртуальных машин Linux в стек Azure</span><span class="sxs-lookup"><span data-stu-id="01d8f-103">Deploy Linux virtual machines on Azure Stack</span></span>
<span data-ttu-id="01d8f-104">Можно развернуть виртуальные машины Linux в пакет средств разработки Azure стека, добавив изображений на основе Linux в Azure Marketplace стека.</span><span class="sxs-lookup"><span data-stu-id="01d8f-104">You can deploy Linux virtual machines on the Azure Stack Development Kit by adding a Linux-based image into the Azure Stack Marketplace.</span></span> <span data-ttu-id="01d8f-105">Несколько поставщиков Linux предоставили образы, которые могут быть добавлены в пакет средств разработки Azure стека, или можно создать собственные.</span><span class="sxs-lookup"><span data-stu-id="01d8f-105">Several Linux vendors have provided images that can be added into an Azure Stack Development Kit or you can build your own.</span></span>

## <a name="download-an-image"></a><span data-ttu-id="01d8f-106">Загрузить изображения</span><span class="sxs-lookup"><span data-stu-id="01d8f-106">Download an image</span></span>
1. <span data-ttu-id="01d8f-107">Загрузить и извлечь изображение Azure стека совместимой по следующим ссылкам или подготовить собственные:</span><span class="sxs-lookup"><span data-stu-id="01d8f-107">Download and extract an Azure Stack-compatible image from the following links, or prepare your own:</span></span>
   
   * [<span data-ttu-id="01d8f-108">Bitnami</span><span class="sxs-lookup"><span data-stu-id="01d8f-108">Bitnami</span></span>](https://bitnami.com/azure-stack)
   * [<span data-ttu-id="01d8f-109">CentOS</span><span class="sxs-lookup"><span data-stu-id="01d8f-109">CentOS</span></span>](http://olstacks.cloudapp.net/latest/)
   * [<span data-ttu-id="01d8f-110">CoreOS</span><span class="sxs-lookup"><span data-stu-id="01d8f-110">CoreOS</span></span>](https://stable.release.core-os.net/amd64-usr/current/coreos_production_azure_image.vhd.bz2)
   * [<span data-ttu-id="01d8f-111">SuSE</span><span class="sxs-lookup"><span data-stu-id="01d8f-111">SuSE</span></span>](https://download.suse.com/Download?buildid=VCFi7y7MsFQ~)
   * <span data-ttu-id="01d8f-112">[Ubuntu 14.04 LTS](https://partner-images.canonical.com/azure/azure_stack/) / [Ubuntu 16.04 LTS](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="01d8f-112">[Ubuntu 14.04 LTS](https://partner-images.canonical.com/azure/azure_stack/) / [Ubuntu 16.04 LTS](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
2. <span data-ttu-id="01d8f-113">Извлеките образ виртуального жесткого диска, при необходимости и [добавить изображение в Marketplace](azure-stack-add-vm-image.md).</span><span class="sxs-lookup"><span data-stu-id="01d8f-113">Extract the image VHD if necessary and [add the image to the Marketplace](azure-stack-add-vm-image.md).</span></span> <span data-ttu-id="01d8f-114">Убедитесь, что `OSType` параметра равным `Linux`.</span><span class="sxs-lookup"><span data-stu-id="01d8f-114">Make sure that the `OSType` parameter is set to `Linux`.</span></span>
3. <span data-ttu-id="01d8f-115">После добавления изображения в Marketplace создается элемент Marketplace и развертывании виртуальной машины Linux.</span><span class="sxs-lookup"><span data-stu-id="01d8f-115">After you've added the image to the Marketplace, a Marketplace item is created and you can deploy a Linux virtual machine.</span></span>

## <a name="prepare-your-own-image"></a><span data-ttu-id="01d8f-116">Подготовьте свой собственный образ</span><span class="sxs-lookup"><span data-stu-id="01d8f-116">Prepare your own image</span></span>
1. <span data-ttu-id="01d8f-117">Подготовьте свой собственный образ Linux с помощью одного из следующих инструкций:</span><span class="sxs-lookup"><span data-stu-id="01d8f-117">Prepare your own Linux image using one of the following instructions:</span></span>
   
   * [<span data-ttu-id="01d8f-118">Подготовка виртуальной машины на основе CentOS для Azure</span><span class="sxs-lookup"><span data-stu-id="01d8f-118">CentOS-based Distributions</span></span>](../virtual-machines/linux/create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [<span data-ttu-id="01d8f-119">Подготовка виртуального жесткого диска Debian для Azure</span><span class="sxs-lookup"><span data-stu-id="01d8f-119">Debian Linux</span></span>](../virtual-machines/linux/debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [<span data-ttu-id="01d8f-120">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="01d8f-120">Oracle Linux</span></span>](../virtual-machines/linux/oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [<span data-ttu-id="01d8f-121">Подготовка виртуальной машины на основе Red Hat для Azure</span><span class="sxs-lookup"><span data-stu-id="01d8f-121">Red Hat Enterprise Linux</span></span>](../virtual-machines/linux/redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [<span data-ttu-id="01d8f-122">Подготовка виртуальной машины SLES или openSUSE для Azure</span><span class="sxs-lookup"><span data-stu-id="01d8f-122">SLES & openSUSE</span></span>](../virtual-machines/linux/suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [<span data-ttu-id="01d8f-123">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="01d8f-123">Ubuntu</span></span>](../virtual-machines/linux/create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
2. <span data-ttu-id="01d8f-124">Загрузите и установите [агент Azure Linux](https://github.com/Azure/WALinuxAgent/)</span><span class="sxs-lookup"><span data-stu-id="01d8f-124">Download and install the [Azure Linux Agent](https://github.com/Azure/WALinuxAgent/)</span></span>
   
    <span data-ttu-id="01d8f-125">Azure Linux Agent версии 2.1.3 или более поздняя версия требуется для подготовки виртуальной Машины Linux в стеке Azure.</span><span class="sxs-lookup"><span data-stu-id="01d8f-125">The Azure Linux Agent version 2.1.3 or higher is required to provision your Linux VM on Azure Stack.</span></span> <span data-ttu-id="01d8f-126">Многие распределений, перечисленных выше, уже содержат эта версия агента или более поздней версии в виде пакета в их хранилищах (обычно называется `WALinuxAgent` или `walinuxagent`).</span><span class="sxs-lookup"><span data-stu-id="01d8f-126">Many of the distributions listed above already include this version of the agent or higher as a package in their repositories (typically called `WALinuxAgent` or `walinuxagent`).</span></span> <span data-ttu-id="01d8f-127">Тем не менее если версия пакет Azure агента, меньше, чем 2.1.3 (т. е. 2.0.18 или ниже), то необходимо установить агент вручную.</span><span class="sxs-lookup"><span data-stu-id="01d8f-127">However, if the version of the Azure agent package is less than 2.1.3 (i.e. 2.0.18 or lower), then you must install the agent manually.</span></span> <span data-ttu-id="01d8f-128">Установленная версия можно определить имя пакета или запустив `/usr/sbin/waagent -version` на виртуальной Машине.</span><span class="sxs-lookup"><span data-stu-id="01d8f-128">The installed version can be determined either from the package name or by running `/usr/sbin/waagent -version` on the VM.</span></span>
   
    <span data-ttu-id="01d8f-129">Следуйте инструкциям для установки агента Azure Linux вручную-</span><span class="sxs-lookup"><span data-stu-id="01d8f-129">Follow the instructions below to install the Azure Linux agent manually -</span></span>
   
   * <span data-ttu-id="01d8f-130">Во-первых, загрузите последнюю версию агента Azure Linux из [GitHub](https://github.com/Azure/WALinuxAgent/releases), пример:</span><span class="sxs-lookup"><span data-stu-id="01d8f-130">First, download the latest Azure Linux agent from [GitHub](https://github.com/Azure/WALinuxAgent/releases), example:</span></span>
     
            # wget https://github.com/Azure/WALinuxAgent/archive/v2.2.0.tar.gz
   * <span data-ttu-id="01d8f-131">Распакуйте агент Azure:</span><span class="sxs-lookup"><span data-stu-id="01d8f-131">Unpack the Azure agent:</span></span>
     
            # tar -vzxf v2.2.0.tar.gz
   * <span data-ttu-id="01d8f-132">Установка python дублирует</span><span class="sxs-lookup"><span data-stu-id="01d8f-132">Install python-setuptools</span></span>
     
        <span data-ttu-id="01d8f-133">**Debian и Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="01d8f-133">**Debian / Ubuntu**</span></span>
     
            # sudo apt-get update
            # sudo apt-get install python-setuptools
     
        <span data-ttu-id="01d8f-134">**Ubuntu 16.04 +**</span><span class="sxs-lookup"><span data-stu-id="01d8f-134">**Ubuntu 16.04+**</span></span>
     
            # sudo apt-get install python3-setuptools
     
        <span data-ttu-id="01d8f-135">**RHEL / CentOS и Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="01d8f-135">**RHEL / CentOS / Oracle Linux**</span></span>
     
            # sudo yum install python-setuptools
   * <span data-ttu-id="01d8f-136">Установите агент Azure:</span><span class="sxs-lookup"><span data-stu-id="01d8f-136">Install the Azure agent:</span></span>
     
            # cd WALinuxAgent-2.2.0
            # sudo python setup.py install --register-service
     
     <span data-ttu-id="01d8f-137">Системы с Python 2.x и Python 3.x установлен side-by-side может потребоваться выполнить следующую команду:</span><span class="sxs-lookup"><span data-stu-id="01d8f-137">Systems with Python 2.x and Python 3.x installed side-by-side may need to run the following command:</span></span>
     
         sudo python3 setup.py install --register-service
     <span data-ttu-id="01d8f-138">Дополнительные сведения см. в разделе агент Azure Linux [README](https://github.com/Azure/WALinuxAgent/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="01d8f-138">For more information, see the Azure Linux Agent [README](https://github.com/Azure/WALinuxAgent/blob/master/README.md).</span></span>
3. <span data-ttu-id="01d8f-139">[Добавить изображение в Marketplace](azure-stack-add-vm-image.md).</span><span class="sxs-lookup"><span data-stu-id="01d8f-139">[Add the image to the Marketplace](azure-stack-add-vm-image.md).</span></span> <span data-ttu-id="01d8f-140">Убедитесь, что `OSType` параметра равным `Linux`.</span><span class="sxs-lookup"><span data-stu-id="01d8f-140">Make sure that the `OSType` parameter is set to `Linux`.</span></span>
4. <span data-ttu-id="01d8f-141">После добавления изображения в Marketplace создается элемент Marketplace и развертывании виртуальной машины Linux.</span><span class="sxs-lookup"><span data-stu-id="01d8f-141">After you've added the image to the Marketplace, a Marketplace item is created and you can deploy a Linux virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="01d8f-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="01d8f-142">Next steps</span></span>
[<span data-ttu-id="01d8f-143">Часто задаваемые вопросы про Azure стека</span><span class="sxs-lookup"><span data-stu-id="01d8f-143">Frequently asked questions for Azure Stack</span></span>](azure-stack-faq.md)

