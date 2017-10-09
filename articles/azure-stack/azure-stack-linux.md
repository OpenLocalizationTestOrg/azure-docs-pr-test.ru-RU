---
title: "гостевые системы aaaLinux стек Azure | Документы Microsoft"
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
ms.openlocfilehash: 225bed7d630b676ca760add25731e347516b5bf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-linux-virtual-machines-on-azure-stack"></a><span data-ttu-id="6d7d1-103">Развертывание виртуальных машин Linux в стек Azure</span><span class="sxs-lookup"><span data-stu-id="6d7d1-103">Deploy Linux virtual machines on Azure Stack</span></span>
<span data-ttu-id="6d7d1-104">Можно развернуть виртуальные машины Linux в Azure стека Development Kit hello, добавив изображений на основе Linux в Azure Marketplace стека hello.</span><span class="sxs-lookup"><span data-stu-id="6d7d1-104">You can deploy Linux virtual machines on hello Azure Stack Development Kit by adding a Linux-based image into hello Azure Stack Marketplace.</span></span> <span data-ttu-id="6d7d1-105">Несколько поставщиков Linux предоставили образы, которые могут быть добавлены в пакет средств разработки Azure стека, или можно создать собственные.</span><span class="sxs-lookup"><span data-stu-id="6d7d1-105">Several Linux vendors have provided images that can be added into an Azure Stack Development Kit or you can build your own.</span></span>

## <a name="download-an-image"></a><span data-ttu-id="6d7d1-106">Загрузить изображения</span><span class="sxs-lookup"><span data-stu-id="6d7d1-106">Download an image</span></span>
1. <span data-ttu-id="6d7d1-107">Загрузить и извлечь из ссылкам hello Azure стека совместимое изображение или Подготовка собственные:</span><span class="sxs-lookup"><span data-stu-id="6d7d1-107">Download and extract an Azure Stack-compatible image from hello following links, or prepare your own:</span></span>
   
   * [<span data-ttu-id="6d7d1-108">Bitnami</span><span class="sxs-lookup"><span data-stu-id="6d7d1-108">Bitnami</span></span>](https://bitnami.com/azure-stack)
   * [<span data-ttu-id="6d7d1-109">CentOS</span><span class="sxs-lookup"><span data-stu-id="6d7d1-109">CentOS</span></span>](http://olstacks.cloudapp.net/latest/)
   * [<span data-ttu-id="6d7d1-110">CoreOS</span><span class="sxs-lookup"><span data-stu-id="6d7d1-110">CoreOS</span></span>](https://stable.release.core-os.net/amd64-usr/current/coreos_production_azure_image.vhd.bz2)
   * [<span data-ttu-id="6d7d1-111">SuSE</span><span class="sxs-lookup"><span data-stu-id="6d7d1-111">SuSE</span></span>](https://download.suse.com/Download?buildid=VCFi7y7MsFQ~)
   * <span data-ttu-id="6d7d1-112">[Ubuntu 14.04 LTS](https://partner-images.canonical.com/azure/azure_stack/) / [Ubuntu 16.04 LTS](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="6d7d1-112">[Ubuntu 14.04 LTS](https://partner-images.canonical.com/azure/azure_stack/) / [Ubuntu 16.04 LTS](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
2. <span data-ttu-id="6d7d1-113">Извлеките hello образа виртуального жесткого диска, при необходимости и [добавить toohello hello образа Marketplace](azure-stack-add-vm-image.md).</span><span class="sxs-lookup"><span data-stu-id="6d7d1-113">Extract hello image VHD if necessary and [add hello image toohello Marketplace](azure-stack-add-vm-image.md).</span></span> <span data-ttu-id="6d7d1-114">Убедитесь в том, что hello `OSType` параметра установлено слишком`Linux`.</span><span class="sxs-lookup"><span data-stu-id="6d7d1-114">Make sure that hello `OSType` parameter is set too`Linux`.</span></span>
3. <span data-ttu-id="6d7d1-115">После добавления toohello hello образа Marketplace создается элемент Marketplace и развертывании виртуальной машины Linux.</span><span class="sxs-lookup"><span data-stu-id="6d7d1-115">After you've added hello image toohello Marketplace, a Marketplace item is created and you can deploy a Linux virtual machine.</span></span>

## <a name="prepare-your-own-image"></a><span data-ttu-id="6d7d1-116">Подготовьте свой собственный образ</span><span class="sxs-lookup"><span data-stu-id="6d7d1-116">Prepare your own image</span></span>
1. <span data-ttu-id="6d7d1-117">Подготовьте свой собственный образ Linux с помощью одного из hello, следуйте инструкциям.</span><span class="sxs-lookup"><span data-stu-id="6d7d1-117">Prepare your own Linux image using one of hello following instructions:</span></span>
   
   * [<span data-ttu-id="6d7d1-118">Подготовка виртуальной машины на основе CentOS для Azure</span><span class="sxs-lookup"><span data-stu-id="6d7d1-118">CentOS-based Distributions</span></span>](../virtual-machines/linux/create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [<span data-ttu-id="6d7d1-119">Подготовка виртуального жесткого диска Debian для Azure</span><span class="sxs-lookup"><span data-stu-id="6d7d1-119">Debian Linux</span></span>](../virtual-machines/linux/debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [<span data-ttu-id="6d7d1-120">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="6d7d1-120">Oracle Linux</span></span>](../virtual-machines/linux/oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [<span data-ttu-id="6d7d1-121">Подготовка виртуальной машины на основе Red Hat для Azure</span><span class="sxs-lookup"><span data-stu-id="6d7d1-121">Red Hat Enterprise Linux</span></span>](../virtual-machines/linux/redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [<span data-ttu-id="6d7d1-122">Подготовка виртуальной машины SLES или openSUSE для Azure</span><span class="sxs-lookup"><span data-stu-id="6d7d1-122">SLES & openSUSE</span></span>](../virtual-machines/linux/suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [<span data-ttu-id="6d7d1-123">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="6d7d1-123">Ubuntu</span></span>](../virtual-machines/linux/create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
2. <span data-ttu-id="6d7d1-124">Загрузите и установите hello [агент Azure Linux](https://github.com/Azure/WALinuxAgent/)</span><span class="sxs-lookup"><span data-stu-id="6d7d1-124">Download and install hello [Azure Linux Agent](https://github.com/Azure/WALinuxAgent/)</span></span>
   
    <span data-ttu-id="6d7d1-125">Hello Azure Linux Agent версии 2.1.3 или выше является обязательным tooprovision ВМ Linux Azure стек.</span><span class="sxs-lookup"><span data-stu-id="6d7d1-125">hello Azure Linux Agent version 2.1.3 or higher is required tooprovision your Linux VM on Azure Stack.</span></span> <span data-ttu-id="6d7d1-126">Многие дистрибутивов hello, перечисленных выше, уже содержат эта версия агента hello или более поздней версии в виде пакета в их хранилищах (обычно называется `WALinuxAgent` или `walinuxagent`).</span><span class="sxs-lookup"><span data-stu-id="6d7d1-126">Many of hello distributions listed above already include this version of hello agent or higher as a package in their repositories (typically called `WALinuxAgent` or `walinuxagent`).</span></span> <span data-ttu-id="6d7d1-127">Однако если hello версии пакета Azure агента hello, меньше, чем 2.1.3 (т. е. 2.0.18 или ниже), то необходимо вручную установить агент hello.</span><span class="sxs-lookup"><span data-stu-id="6d7d1-127">However, if hello version of hello Azure agent package is less than 2.1.3 (i.e. 2.0.18 or lower), then you must install hello agent manually.</span></span> <span data-ttu-id="6d7d1-128">Hello установлены версии можно определить имя пакета hello или запустив `/usr/sbin/waagent -version` на hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="6d7d1-128">hello installed version can be determined either from hello package name or by running `/usr/sbin/waagent -version` on hello VM.</span></span>
   
    <span data-ttu-id="6d7d1-129">Следуйте инструкциям hello ниже tooinstall hello Azure Linux agent вручную-</span><span class="sxs-lookup"><span data-stu-id="6d7d1-129">Follow hello instructions below tooinstall hello Azure Linux agent manually -</span></span>
   
   * <span data-ttu-id="6d7d1-130">Во-первых, загрузите последнюю версию агента Azure Linux hello из [GitHub](https://github.com/Azure/WALinuxAgent/releases), пример:</span><span class="sxs-lookup"><span data-stu-id="6d7d1-130">First, download hello latest Azure Linux agent from [GitHub](https://github.com/Azure/WALinuxAgent/releases), example:</span></span>
     
            # wget https://github.com/Azure/WALinuxAgent/archive/v2.2.0.tar.gz
   * <span data-ttu-id="6d7d1-131">Распакуйте hello Azure агента:</span><span class="sxs-lookup"><span data-stu-id="6d7d1-131">Unpack hello Azure agent:</span></span>
     
            # tar -vzxf v2.2.0.tar.gz
   * <span data-ttu-id="6d7d1-132">Установка python дублирует</span><span class="sxs-lookup"><span data-stu-id="6d7d1-132">Install python-setuptools</span></span>
     
        <span data-ttu-id="6d7d1-133">**Debian и Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="6d7d1-133">**Debian / Ubuntu**</span></span>
     
            # sudo apt-get update
            # sudo apt-get install python-setuptools
     
        <span data-ttu-id="6d7d1-134">**Ubuntu 16.04 +**</span><span class="sxs-lookup"><span data-stu-id="6d7d1-134">**Ubuntu 16.04+**</span></span>
     
            # sudo apt-get install python3-setuptools
     
        <span data-ttu-id="6d7d1-135">**RHEL / CentOS и Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="6d7d1-135">**RHEL / CentOS / Oracle Linux**</span></span>
     
            # sudo yum install python-setuptools
   * <span data-ttu-id="6d7d1-136">Установите агент Azure hello:</span><span class="sxs-lookup"><span data-stu-id="6d7d1-136">Install hello Azure agent:</span></span>
     
            # cd WALinuxAgent-2.2.0
            # sudo python setup.py install --register-service
     
     <span data-ttu-id="6d7d1-137">Системы с Python 2.x и Python 3.x установлен side-by-side возможно, потребуется hello toorun следующую команду:</span><span class="sxs-lookup"><span data-stu-id="6d7d1-137">Systems with Python 2.x and Python 3.x installed side-by-side may need toorun hello following command:</span></span>
     
         sudo python3 setup.py install --register-service
     <span data-ttu-id="6d7d1-138">Дополнительные сведения см. в разделе hello Azure Linux Agent [README](https://github.com/Azure/WALinuxAgent/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="6d7d1-138">For more information, see hello Azure Linux Agent [README](https://github.com/Azure/WALinuxAgent/blob/master/README.md).</span></span>
3. <span data-ttu-id="6d7d1-139">[Добавить toohello hello образа Marketplace](azure-stack-add-vm-image.md).</span><span class="sxs-lookup"><span data-stu-id="6d7d1-139">[Add hello image toohello Marketplace](azure-stack-add-vm-image.md).</span></span> <span data-ttu-id="6d7d1-140">Убедитесь в том, что hello `OSType` параметра установлено слишком`Linux`.</span><span class="sxs-lookup"><span data-stu-id="6d7d1-140">Make sure that hello `OSType` parameter is set too`Linux`.</span></span>
4. <span data-ttu-id="6d7d1-141">После добавления toohello hello образа Marketplace создается элемент Marketplace и развертывании виртуальной машины Linux.</span><span class="sxs-lookup"><span data-stu-id="6d7d1-141">After you've added hello image toohello Marketplace, a Marketplace item is created and you can deploy a Linux virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d7d1-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6d7d1-142">Next steps</span></span>
[<span data-ttu-id="6d7d1-143">Часто задаваемые вопросы про Azure стека</span><span class="sxs-lookup"><span data-stu-id="6d7d1-143">Frequently asked questions for Azure Stack</span></span>](azure-stack-faq.md)

