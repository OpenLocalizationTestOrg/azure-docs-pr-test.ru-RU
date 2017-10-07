---
title: "способы aaaDifferent toocreate виртуальной Машины Linux в Azure | Microsoft Azure"
description: "Дополнительные сведения различными способами hello toocreate виртуальной машины Linux в Azure, включая tootools ссылки и учебники для каждого метода."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f38f8a44-6c88-4490-a84a-46388212d24c
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 250e92c063c87a8c1279097dc2264777d95478d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="different-ways-toocreate-a-linux-vm"></a><span data-ttu-id="5a607-103">Различные способы toocreate ВМ Linux</span><span class="sxs-lookup"><span data-stu-id="5a607-103">Different ways toocreate a Linux VM</span></span>
<span data-ttu-id="5a607-104">У вас hello гибкость в Azure toocreate Linux виртуальной машины (VM) с помощью средства и рабочие процессы научились tooyou.</span><span class="sxs-lookup"><span data-stu-id="5a607-104">You have hello flexibility in Azure toocreate a Linux virtual machine (VM) using tools and workflows comfortable tooyou.</span></span> <span data-ttu-id="5a607-105">В этой статье приведены эти различия и примеры для создания виртуальных машин Linux, включая hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="5a607-105">This article summarizes these differences and examples for creating your Linux VMs, including hello Azure CLI 2.0.</span></span> <span data-ttu-id="5a607-106">Вы также можете просмотреть варианты создания, включая hello [Azure CLI 1.0](creation-choices-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="5a607-106">You can also view creation choices including hello [Azure CLI 1.0](creation-choices-nodejs.md).</span></span>

<span data-ttu-id="5a607-107">Hello [Azure CLI 2.0](/cli/azure/install-az-cli2) доступна на платформах через пакета npm, предоставляемых системой дистрибутив пакеты или контейнер Docker.</span><span class="sxs-lookup"><span data-stu-id="5a607-107">hello [Azure CLI 2.0](/cli/azure/install-az-cli2) is available across platforms via an npm package, distro-provided packages, or Docker container.</span></span> <span data-ttu-id="5a607-108">Установите сборку наиболее подходящий hello для вашей среды и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login)</span><span class="sxs-lookup"><span data-stu-id="5a607-108">Install hello most appropriate build for your environment and log in tooan Azure account using [az login](/cli/azure/#login)</span></span>

* [<span data-ttu-id="5a607-109">Создайте виртуальную Машину Linux с hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="5a607-109">Create a Linux VM with hello Azure CLI 2.0</span></span>](quick-create-cli.md)
  
  * <span data-ttu-id="5a607-110">С помощью команды [az group create](/cli/azure/group#create) создайте группу ресурсов с именем *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="5a607-110">Create a resource group with [az group create](/cli/azure/group#create) named *myResourceGroup*:</span></span> 
   
    ```azurecli
    az group create --name myResourceGroup --location eastus
    ```
    
  * <span data-ttu-id="5a607-111">Создайте виртуальную Машину с [создания виртуальной машины az](/cli/azure/vm#create) с именем *myVM* с помощью последней hello *UbuntuLTS* образ и создать ключи SSH, если они еще не существуют в *~/.ssh*:</span><span class="sxs-lookup"><span data-stu-id="5a607-111">Create a VM with [az vm create](/cli/azure/vm#create) named *myVM* using hello latest *UbuntuLTS* image and generate SSH keys if they do not already exist in *~/.ssh*:</span></span>

    ```azurecli
    az vm create \
        --resource-group myResourceGroup \
        --name myVM \
        --image UbuntuLTS \
        --generate-ssh-keys
    ```

* <span data-ttu-id="5a607-112">[Создание виртуальной машины Linux с помощью шаблона Azure](create-ssh-secured-vm-from-template.md).</span><span class="sxs-lookup"><span data-stu-id="5a607-112">[Create a Linux VM with an Azure template](create-ssh-secured-vm-from-template.md)</span></span>
  
  * <span data-ttu-id="5a607-113">Hello следующий пример использует [создания развертывания группы az](/cli/azure/group/deployment#create) toocreate виртуальной Машины из шаблона, сохраненного на GitHub:</span><span class="sxs-lookup"><span data-stu-id="5a607-113">hello following example uses [az group deployment create](/cli/azure/group/deployment#create) toocreate a VM from a template stored on GitHub:</span></span>
    
    ```azurecli
    az group deployment create --resource-group myResourceGroup \ 
      --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
      --parameters @myparameters.json
    ```
* <span data-ttu-id="5a607-114">[Создание виртуальной машины Linux и ее настройка с помощью файла cloud-init](tutorial-automate-vm-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="5a607-114">[Create a Linux VM and customize with cloud-init](tutorial-automate-vm-deployment.md)</span></span>

* [<span data-ttu-id="5a607-115">Создание приложения с балансировкой нагрузки и высоким уровнем доступности на нескольких виртуальных машинах Linux</span><span class="sxs-lookup"><span data-stu-id="5a607-115">Create a load balanced and highly available application on multiple Linux VMs</span></span>](tutorial-load-balancer.md)


## <a name="azure-portal"></a><span data-ttu-id="5a607-116">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="5a607-116">Azure portal</span></span>
<span data-ttu-id="5a607-117">Hello [портал Azure](https://portal.azure.com) позволяет tooquickly создания виртуальной Машины, так как нет ничего tooinstall в системе.</span><span class="sxs-lookup"><span data-stu-id="5a607-117">hello [Azure portal](https://portal.azure.com) allows you tooquickly create a VM since there is nothing tooinstall on your system.</span></span> <span data-ttu-id="5a607-118">Используйте hello Azure портала toocreate hello виртуальной Машины:</span><span class="sxs-lookup"><span data-stu-id="5a607-118">Use hello Azure portal toocreate hello VM:</span></span>

* [<span data-ttu-id="5a607-119">Создайте виртуальную Машину Linux с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="5a607-119">Create a Linux VM using hello Azure portal</span></span>](quick-create-portal.md) 


## <a name="operating-system-and-image-choices"></a><span data-ttu-id="5a607-120">Операционная система и варианты образов</span><span class="sxs-lookup"><span data-stu-id="5a607-120">Operating system and image choices</span></span>
<span data-ttu-id="5a607-121">При создании виртуальной Машины, вы выбираете изображение, зависящее от операционной системы требуется toorun hello.</span><span class="sxs-lookup"><span data-stu-id="5a607-121">When creating a VM, you choose an image based on hello operating system you want toorun.</span></span> <span data-ttu-id="5a607-122">Azure и партнеры предлагают множество образов, некоторые из которых содержат предустановленные приложения и средства.</span><span class="sxs-lookup"><span data-stu-id="5a607-122">Azure and its partners offer many images, some of which include applications and tools pre-installed.</span></span> <span data-ttu-id="5a607-123">Или передать один из собственных образов (см. [hello следующий раздел](#use-your-own-image)).</span><span class="sxs-lookup"><span data-stu-id="5a607-123">Or, upload one of your own images (see [hello following section](#use-your-own-image)).</span></span>

### <a name="azure-images"></a><span data-ttu-id="5a607-124">Образы Azure</span><span class="sxs-lookup"><span data-stu-id="5a607-124">Azure images</span></span>
<span data-ttu-id="5a607-125">Используйте hello [образа виртуальной машины az](/cli/azure/vm/image) команды toosee, доступные по издателям, дистрибутив версии и сборки.</span><span class="sxs-lookup"><span data-stu-id="5a607-125">Use hello [az vm image](/cli/azure/vm/image) commands toosee what's available by publisher, distro release, and builds.</span></span>

<span data-ttu-id="5a607-126">Отображение списка доступных издателей:</span><span class="sxs-lookup"><span data-stu-id="5a607-126">List available publishers:</span></span>

```azurecli
az vm image list-publishers --location eastus
```

<span data-ttu-id="5a607-127">Отображение списка доступных продуктов (предложений) нужного издателя:</span><span class="sxs-lookup"><span data-stu-id="5a607-127">List available products (offers) for a given publisher:</span></span>

```azurecli
az vm image list-offers --publisher Canonical --location eastus
```

<span data-ttu-id="5a607-128">Отображение списка доступных номеров SKU (для дистрибутивов) требуемого предложения:</span><span class="sxs-lookup"><span data-stu-id="5a607-128">List available SKUs (distro releases) of a given offer:</span></span>

```azurecli
az vm image list-skus --publisher Canonical --offer UbuntuServer --location eastus
```

<span data-ttu-id="5a607-129">Отображение списка всех доступных образов для определенного выпуска:</span><span class="sxs-lookup"><span data-stu-id="5a607-129">List all available images for a given release:</span></span>

```azurecli
az vm image list --publisher Canonical --offer UbuntuServer --sku 16.04.0-LTS --location eastus
```

<span data-ttu-id="5a607-130">Дополнительные примеры на просмотр и использование доступных образов см. в разделе [перехода, а затем выберите образы виртуальных машин Azure с hello Azure CLI](cli-ps-findimage.md).</span><span class="sxs-lookup"><span data-stu-id="5a607-130">For more examples on browsing and using available images, see [Navigate and select Azure virtual machine images with hello Azure CLI](cli-ps-findimage.md).</span></span>

<span data-ttu-id="5a607-131">Hello [создания виртуальной машины az](/cli/azure/vm#create) команда имеет tooquickly доступа можно использовать псевдонимы hello чаще дистрибутивы и их последние версии.</span><span class="sxs-lookup"><span data-stu-id="5a607-131">hello [az vm create](/cli/azure/vm#create) command has aliases you can use tooquickly access hello more common distros and their latest releases.</span></span> <span data-ttu-id="5a607-132">С помощью псевдонимов часто быстрее, чем указание hello издателя, предложение, SKU и версии каждый раз при создании виртуальной Машины:</span><span class="sxs-lookup"><span data-stu-id="5a607-132">Using aliases is often quicker than specifying hello publisher, offer, SKU, and version each time you create a VM:</span></span>

| <span data-ttu-id="5a607-133">Alias</span><span class="sxs-lookup"><span data-stu-id="5a607-133">Alias</span></span> | <span data-ttu-id="5a607-134">Издатель</span><span class="sxs-lookup"><span data-stu-id="5a607-134">Publisher</span></span> | <span data-ttu-id="5a607-135">ПРЕДЛОЖЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="5a607-135">Offer</span></span> | <span data-ttu-id="5a607-136">SKU</span><span class="sxs-lookup"><span data-stu-id="5a607-136">SKU</span></span> | <span data-ttu-id="5a607-137">Версия</span><span class="sxs-lookup"><span data-stu-id="5a607-137">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="5a607-138">CentOS</span><span class="sxs-lookup"><span data-stu-id="5a607-138">CentOS</span></span> |<span data-ttu-id="5a607-139">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="5a607-139">OpenLogic</span></span> |<span data-ttu-id="5a607-140">CentOS</span><span class="sxs-lookup"><span data-stu-id="5a607-140">Centos</span></span> |<span data-ttu-id="5a607-141">7,2</span><span class="sxs-lookup"><span data-stu-id="5a607-141">7.2</span></span> |<span data-ttu-id="5a607-142">последних</span><span class="sxs-lookup"><span data-stu-id="5a607-142">latest</span></span> |
| <span data-ttu-id="5a607-143">CoreOS</span><span class="sxs-lookup"><span data-stu-id="5a607-143">CoreOS</span></span> |<span data-ttu-id="5a607-144">CoreOS</span><span class="sxs-lookup"><span data-stu-id="5a607-144">CoreOS</span></span> |<span data-ttu-id="5a607-145">CoreOS</span><span class="sxs-lookup"><span data-stu-id="5a607-145">CoreOS</span></span> |<span data-ttu-id="5a607-146">Stable</span><span class="sxs-lookup"><span data-stu-id="5a607-146">Stable</span></span> |<span data-ttu-id="5a607-147">последняя</span><span class="sxs-lookup"><span data-stu-id="5a607-147">latest</span></span> |
| <span data-ttu-id="5a607-148">Debian</span><span class="sxs-lookup"><span data-stu-id="5a607-148">Debian</span></span> |<span data-ttu-id="5a607-149">credativ</span><span class="sxs-lookup"><span data-stu-id="5a607-149">credativ</span></span> |<span data-ttu-id="5a607-150">Debian</span><span class="sxs-lookup"><span data-stu-id="5a607-150">Debian</span></span> |<span data-ttu-id="5a607-151">8</span><span class="sxs-lookup"><span data-stu-id="5a607-151">8</span></span> |<span data-ttu-id="5a607-152">последняя</span><span class="sxs-lookup"><span data-stu-id="5a607-152">latest</span></span> |
| <span data-ttu-id="5a607-153">openSUSE</span><span class="sxs-lookup"><span data-stu-id="5a607-153">openSUSE</span></span> |<span data-ttu-id="5a607-154">SUSE</span><span class="sxs-lookup"><span data-stu-id="5a607-154">SUSE</span></span> |<span data-ttu-id="5a607-155">openSUSE</span><span class="sxs-lookup"><span data-stu-id="5a607-155">openSUSE</span></span> |<span data-ttu-id="5a607-156">13.2</span><span class="sxs-lookup"><span data-stu-id="5a607-156">13.2</span></span> |<span data-ttu-id="5a607-157">последних</span><span class="sxs-lookup"><span data-stu-id="5a607-157">latest</span></span> |
| <span data-ttu-id="5a607-158">RHEL</span><span class="sxs-lookup"><span data-stu-id="5a607-158">RHEL</span></span> |<span data-ttu-id="5a607-159">Redhat</span><span class="sxs-lookup"><span data-stu-id="5a607-159">Redhat</span></span> |<span data-ttu-id="5a607-160">RHEL</span><span class="sxs-lookup"><span data-stu-id="5a607-160">RHEL</span></span> |<span data-ttu-id="5a607-161">7,2</span><span class="sxs-lookup"><span data-stu-id="5a607-161">7.2</span></span> |<span data-ttu-id="5a607-162">последних</span><span class="sxs-lookup"><span data-stu-id="5a607-162">latest</span></span> |
| <span data-ttu-id="5a607-163">SLES</span><span class="sxs-lookup"><span data-stu-id="5a607-163">SLES</span></span> |<span data-ttu-id="5a607-164">SLES</span><span class="sxs-lookup"><span data-stu-id="5a607-164">SLES</span></span> |<span data-ttu-id="5a607-165">SLES</span><span class="sxs-lookup"><span data-stu-id="5a607-165">SLES</span></span> |<span data-ttu-id="5a607-166">12-SP1</span><span class="sxs-lookup"><span data-stu-id="5a607-166">12-SP1</span></span> |<span data-ttu-id="5a607-167">последних</span><span class="sxs-lookup"><span data-stu-id="5a607-167">latest</span></span> |
| <span data-ttu-id="5a607-168">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="5a607-168">UbuntuLTS</span></span> |<span data-ttu-id="5a607-169">Canonical</span><span class="sxs-lookup"><span data-stu-id="5a607-169">Canonical</span></span> |<span data-ttu-id="5a607-170">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="5a607-170">UbuntuServer</span></span> |<span data-ttu-id="5a607-171">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="5a607-171">14.04.4-LTS</span></span> |<span data-ttu-id="5a607-172">последних</span><span class="sxs-lookup"><span data-stu-id="5a607-172">latest</span></span> |

### <a name="use-your-own-image"></a><span data-ttu-id="5a607-173">Использование своего образа</span><span class="sxs-lookup"><span data-stu-id="5a607-173">Use your own image</span></span>
<span data-ttu-id="5a607-174">Если вам требуются особые настройки, используйте образ на основе имеющейся виртуальной машины Azure. Для этого запишите образ такой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="5a607-174">If you require specific customizations, you can use an image based on an existing Azure VM by capturing that VM.</span></span> <span data-ttu-id="5a607-175">Вы также можете отправить собственный образ, созданный на локальном диске.</span><span class="sxs-lookup"><span data-stu-id="5a607-175">You can also upload an image created on-premises.</span></span> <span data-ttu-id="5a607-176">Дополнительные сведения о поддерживаемых дистрибутивах и toouse собственные образы. в статье hello следующие статьи:</span><span class="sxs-lookup"><span data-stu-id="5a607-176">For more information on supported distros and how toouse your own images, see hello following articles:</span></span>

* [<span data-ttu-id="5a607-177">Linux on Azure-Endorsed Distributions (Linux на дистрибутивах, рекомендованных для Azure)</span><span class="sxs-lookup"><span data-stu-id="5a607-177">Azure endorsed distributions</span></span>](endorsed-distros.md)
* [<span data-ttu-id="5a607-178">Information for Non-Endorsed Distributions (Информация о нерекомендованных дистрибутивах)</span><span class="sxs-lookup"><span data-stu-id="5a607-178">Information for non-endorsed distributions</span></span>](create-upload-generic.md)
* <span data-ttu-id="5a607-179">[Как toocreate изображение из существующей виртуальной Машине Azure](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="5a607-179">[How toocreate an image from an existing Azure VM](tutorial-custom-images.md).</span></span>
  
  * <span data-ttu-id="5a607-180">Пример: быстрый запуск команды toocreate образ с существующей виртуальной Машине Azure:</span><span class="sxs-lookup"><span data-stu-id="5a607-180">Quick-start example commands toocreate an image from an existing Azure VM:</span></span>
    
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm generalize --resource-group myResourceGroup --name myVM
    az vm image create --resource-group myResourceGroup --source myVM --name myImage
    ```

## <a name="next-steps"></a><span data-ttu-id="5a607-181">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5a607-181">Next steps</span></span>
* <span data-ttu-id="5a607-182">Создайте виртуальную Машину Linux с hello [CLI](quick-create-cli.md), из hello [портала](quick-create-portal.md), или с помощью [шаблона Azure Resource Manager](../windows/cli-deploy-templates.md).</span><span class="sxs-lookup"><span data-stu-id="5a607-182">Create a Linux VM with hello [CLI](quick-create-cli.md), from hello [portal](quick-create-portal.md), or using an [Azure Resource Manager template](../windows/cli-deploy-templates.md).</span></span>
* <span data-ttu-id="5a607-183">После создания виртуальной машины Linux [прочтите статью о дисках и хранилище Azure](tutorial-manage-disks.md).</span><span class="sxs-lookup"><span data-stu-id="5a607-183">After creating a Linux VM, [learn about Azure disks and storage](tutorial-manage-disks.md).</span></span>
* <span data-ttu-id="5a607-184">Быстрое шаги слишком[сбросить пароль или SSH-ключи пользователей и управление ими](using-vmaccess-extension.md).</span><span class="sxs-lookup"><span data-stu-id="5a607-184">Quick steps too[reset a password or SSH keys and manage users](using-vmaccess-extension.md).</span></span>
