---
title: "Различные способы создания виртуальной машины Linux в Azure | Microsoft Azure"
description: "Узнайте о различных способах создания виртуальных машин Linux в Azure, а также воспользуйтесь ссылками на инструменты и руководства по каждому из этих способов."
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
ms.openlocfilehash: b2f93579eb1c7a69d0dbd1b0ef112aed9b2168c3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="different-ways-to-create-a-linux-vm"></a><span data-ttu-id="314ae-103">Различные способы создания виртуальной машины Linux</span><span class="sxs-lookup"><span data-stu-id="314ae-103">Different ways to create a Linux VM</span></span>
<span data-ttu-id="314ae-104">Платформа Azure предоставляет гибкие решения по созданию виртуальных машин Linux. Здесь каждый пользователь найдет удобные для себя инструменты и рабочие процессы.</span><span class="sxs-lookup"><span data-stu-id="314ae-104">You have the flexibility in Azure to create a Linux virtual machine (VM) using tools and workflows comfortable to you.</span></span> <span data-ttu-id="314ae-105">В этой статье описаны разные решения и примеры создания виртуальных машин Linux, в том числе с помощью Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="314ae-105">This article summarizes these differences and examples for creating your Linux VMs, including the Azure CLI 2.0.</span></span> <span data-ttu-id="314ae-106">Вы также можете изучить варианты создания, в том числе с помощью [Azure CLI 1.0](creation-choices-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="314ae-106">You can also view creation choices including the [Azure CLI 1.0](creation-choices-nodejs.md).</span></span>

<span data-ttu-id="314ae-107">Интерфейс командной строки [Azure CLI 2.0](/cli/azure/install-az-cli2) доступен на разных платформах в виде пакета npm, включенных в дистрибутив пакетов или контейнера Docker.</span><span class="sxs-lookup"><span data-stu-id="314ae-107">The [Azure CLI 2.0](/cli/azure/install-az-cli2) is available across platforms via an npm package, distro-provided packages, or Docker container.</span></span> <span data-ttu-id="314ae-108">Установите оптимальную сборку для своей среды и войдите в учетную запись Azure с помощью команды [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="314ae-108">Install the most appropriate build for your environment and log in to an Azure account using [az login](/cli/azure/#login)</span></span>

* <span data-ttu-id="314ae-109">[Создание виртуальной машины Linux с помощью Azure CLI 2.0](quick-create-cli.md).</span><span class="sxs-lookup"><span data-stu-id="314ae-109">[Create a Linux VM with the Azure CLI 2.0](quick-create-cli.md)</span></span>
  
  * <span data-ttu-id="314ae-110">С помощью команды [az group create](/cli/azure/group#create) создайте группу ресурсов с именем *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="314ae-110">Create a resource group with [az group create](/cli/azure/group#create) named *myResourceGroup*:</span></span> 
   
    ```azurecli
    az group create --name myResourceGroup --location eastus
    ```
    
  * <span data-ttu-id="314ae-111">С помощью команды [az vm create](/cli/azure/vm#create) создайте виртуальную машину с именем *myVM*, используя последний образ *UbuntuLTS*, и сгенерируйте ключи SSH, если они еще не существуют в *~/.ssh*:</span><span class="sxs-lookup"><span data-stu-id="314ae-111">Create a VM with [az vm create](/cli/azure/vm#create) named *myVM* using the latest *UbuntuLTS* image and generate SSH keys if they do not already exist in *~/.ssh*:</span></span>

    ```azurecli
    az vm create \
        --resource-group myResourceGroup \
        --name myVM \
        --image UbuntuLTS \
        --generate-ssh-keys
    ```

* <span data-ttu-id="314ae-112">[Создание виртуальной машины Linux с помощью шаблона Azure](create-ssh-secured-vm-from-template.md).</span><span class="sxs-lookup"><span data-stu-id="314ae-112">[Create a Linux VM with an Azure template](create-ssh-secured-vm-from-template.md)</span></span>
  
  * <span data-ttu-id="314ae-113">В следующем примере с помощью команды [az group deployment create](/cli/azure/group/deployment#create) создается виртуальная машина на основе шаблона, сохраненного в репозитории GitHub:</span><span class="sxs-lookup"><span data-stu-id="314ae-113">The following example uses [az group deployment create](/cli/azure/group/deployment#create) to create a VM from a template stored on GitHub:</span></span>
    
    ```azurecli
    az group deployment create --resource-group myResourceGroup \ 
      --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
      --parameters @myparameters.json
    ```
* <span data-ttu-id="314ae-114">[Создание виртуальной машины Linux и ее настройка с помощью файла cloud-init](tutorial-automate-vm-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="314ae-114">[Create a Linux VM and customize with cloud-init](tutorial-automate-vm-deployment.md)</span></span>

* [<span data-ttu-id="314ae-115">Создание приложения с балансировкой нагрузки и высоким уровнем доступности на нескольких виртуальных машинах Linux</span><span class="sxs-lookup"><span data-stu-id="314ae-115">Create a load balanced and highly available application on multiple Linux VMs</span></span>](tutorial-load-balancer.md)


## <a name="azure-portal"></a><span data-ttu-id="314ae-116">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="314ae-116">Azure portal</span></span>
<span data-ttu-id="314ae-117">С помощью [портала Azure](https://portal.azure.com) можно быстро создать виртуальную машину, так как установка компонентов в локальной системе не требуется.</span><span class="sxs-lookup"><span data-stu-id="314ae-117">The [Azure portal](https://portal.azure.com) allows you to quickly create a VM since there is nothing to install on your system.</span></span> <span data-ttu-id="314ae-118">Для создания виртуальной машины используйте портал Azure:</span><span class="sxs-lookup"><span data-stu-id="314ae-118">Use the Azure portal to create the VM:</span></span>

* [<span data-ttu-id="314ae-119">Создание виртуальной машины Linux в Azure с помощью портала</span><span class="sxs-lookup"><span data-stu-id="314ae-119">Create a Linux VM using the Azure portal</span></span>](quick-create-portal.md) 


## <a name="operating-system-and-image-choices"></a><span data-ttu-id="314ae-120">Операционная система и варианты образов</span><span class="sxs-lookup"><span data-stu-id="314ae-120">Operating system and image choices</span></span>
<span data-ttu-id="314ae-121">При создании виртуальной машины можно выбрать образ для операционной системы, которую необходимо запустить.</span><span class="sxs-lookup"><span data-stu-id="314ae-121">When creating a VM, you choose an image based on the operating system you want to run.</span></span> <span data-ttu-id="314ae-122">Azure и партнеры предлагают множество образов, некоторые из которых содержат предустановленные приложения и средства.</span><span class="sxs-lookup"><span data-stu-id="314ae-122">Azure and its partners offer many images, some of which include applications and tools pre-installed.</span></span> <span data-ttu-id="314ae-123">Вы также можете передать один из созданных вами образов (см. [следующий раздел](#use-your-own-image)).</span><span class="sxs-lookup"><span data-stu-id="314ae-123">Or, upload one of your own images (see [the following section](#use-your-own-image)).</span></span>

### <a name="azure-images"></a><span data-ttu-id="314ae-124">Образы Azure</span><span class="sxs-lookup"><span data-stu-id="314ae-124">Azure images</span></span>
<span data-ttu-id="314ae-125">Чтобы просмотреть список доступных издателей, дистрибутивов и сборок, используйте команды [az vm image](/cli/azure/vm/image).</span><span class="sxs-lookup"><span data-stu-id="314ae-125">Use the [az vm image](/cli/azure/vm/image) commands to see what's available by publisher, distro release, and builds.</span></span>

<span data-ttu-id="314ae-126">Отображение списка доступных издателей:</span><span class="sxs-lookup"><span data-stu-id="314ae-126">List available publishers:</span></span>

```azurecli
az vm image list-publishers --location eastus
```

<span data-ttu-id="314ae-127">Отображение списка доступных продуктов (предложений) нужного издателя:</span><span class="sxs-lookup"><span data-stu-id="314ae-127">List available products (offers) for a given publisher:</span></span>

```azurecli
az vm image list-offers --publisher Canonical --location eastus
```

<span data-ttu-id="314ae-128">Отображение списка доступных номеров SKU (для дистрибутивов) требуемого предложения:</span><span class="sxs-lookup"><span data-stu-id="314ae-128">List available SKUs (distro releases) of a given offer:</span></span>

```azurecli
az vm image list-skus --publisher Canonical --offer UbuntuServer --location eastus
```

<span data-ttu-id="314ae-129">Отображение списка всех доступных образов для определенного выпуска:</span><span class="sxs-lookup"><span data-stu-id="314ae-129">List all available images for a given release:</span></span>

```azurecli
az vm image list --publisher Canonical --offer UbuntuServer --sku 16.04.0-LTS --location eastus
```

<span data-ttu-id="314ae-130">Дополнительные примеры просмотра и использования доступных образов см. в статье [Выбор образов виртуальных машин Linux с помощью интерфейса командной строки Azure (Azure CLI)](cli-ps-findimage.md).</span><span class="sxs-lookup"><span data-stu-id="314ae-130">For more examples on browsing and using available images, see [Navigate and select Azure virtual machine images with the Azure CLI](cli-ps-findimage.md).</span></span>

<span data-ttu-id="314ae-131">Команда [az vm create](/cli/azure/vm#create) содержит псевдонимы, которые можно использовать для быстрого доступа к самым распространенным дистрибутивам и их последним выпускам.</span><span class="sxs-lookup"><span data-stu-id="314ae-131">The [az vm create](/cli/azure/vm#create) command has aliases you can use to quickly access the more common distros and their latest releases.</span></span> <span data-ttu-id="314ae-132">Как правило, использовать псевдоним быстрее, чем указывать издателя, предложение, номер SKU и версию каждый раз при создании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="314ae-132">Using aliases is often quicker than specifying the publisher, offer, SKU, and version each time you create a VM:</span></span>

| <span data-ttu-id="314ae-133">Alias</span><span class="sxs-lookup"><span data-stu-id="314ae-133">Alias</span></span> | <span data-ttu-id="314ae-134">Издатель</span><span class="sxs-lookup"><span data-stu-id="314ae-134">Publisher</span></span> | <span data-ttu-id="314ae-135">ПРЕДЛОЖЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="314ae-135">Offer</span></span> | <span data-ttu-id="314ae-136">SKU</span><span class="sxs-lookup"><span data-stu-id="314ae-136">SKU</span></span> | <span data-ttu-id="314ae-137">Версия</span><span class="sxs-lookup"><span data-stu-id="314ae-137">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="314ae-138">CentOS</span><span class="sxs-lookup"><span data-stu-id="314ae-138">CentOS</span></span> |<span data-ttu-id="314ae-139">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="314ae-139">OpenLogic</span></span> |<span data-ttu-id="314ae-140">CentOS</span><span class="sxs-lookup"><span data-stu-id="314ae-140">Centos</span></span> |<span data-ttu-id="314ae-141">7,2</span><span class="sxs-lookup"><span data-stu-id="314ae-141">7.2</span></span> |<span data-ttu-id="314ae-142">последних</span><span class="sxs-lookup"><span data-stu-id="314ae-142">latest</span></span> |
| <span data-ttu-id="314ae-143">CoreOS</span><span class="sxs-lookup"><span data-stu-id="314ae-143">CoreOS</span></span> |<span data-ttu-id="314ae-144">CoreOS</span><span class="sxs-lookup"><span data-stu-id="314ae-144">CoreOS</span></span> |<span data-ttu-id="314ae-145">CoreOS</span><span class="sxs-lookup"><span data-stu-id="314ae-145">CoreOS</span></span> |<span data-ttu-id="314ae-146">Stable</span><span class="sxs-lookup"><span data-stu-id="314ae-146">Stable</span></span> |<span data-ttu-id="314ae-147">последняя</span><span class="sxs-lookup"><span data-stu-id="314ae-147">latest</span></span> |
| <span data-ttu-id="314ae-148">Debian</span><span class="sxs-lookup"><span data-stu-id="314ae-148">Debian</span></span> |<span data-ttu-id="314ae-149">credativ</span><span class="sxs-lookup"><span data-stu-id="314ae-149">credativ</span></span> |<span data-ttu-id="314ae-150">Debian</span><span class="sxs-lookup"><span data-stu-id="314ae-150">Debian</span></span> |<span data-ttu-id="314ae-151">8</span><span class="sxs-lookup"><span data-stu-id="314ae-151">8</span></span> |<span data-ttu-id="314ae-152">последняя</span><span class="sxs-lookup"><span data-stu-id="314ae-152">latest</span></span> |
| <span data-ttu-id="314ae-153">openSUSE</span><span class="sxs-lookup"><span data-stu-id="314ae-153">openSUSE</span></span> |<span data-ttu-id="314ae-154">SUSE</span><span class="sxs-lookup"><span data-stu-id="314ae-154">SUSE</span></span> |<span data-ttu-id="314ae-155">openSUSE</span><span class="sxs-lookup"><span data-stu-id="314ae-155">openSUSE</span></span> |<span data-ttu-id="314ae-156">13.2</span><span class="sxs-lookup"><span data-stu-id="314ae-156">13.2</span></span> |<span data-ttu-id="314ae-157">последних</span><span class="sxs-lookup"><span data-stu-id="314ae-157">latest</span></span> |
| <span data-ttu-id="314ae-158">RHEL</span><span class="sxs-lookup"><span data-stu-id="314ae-158">RHEL</span></span> |<span data-ttu-id="314ae-159">Redhat</span><span class="sxs-lookup"><span data-stu-id="314ae-159">Redhat</span></span> |<span data-ttu-id="314ae-160">RHEL</span><span class="sxs-lookup"><span data-stu-id="314ae-160">RHEL</span></span> |<span data-ttu-id="314ae-161">7,2</span><span class="sxs-lookup"><span data-stu-id="314ae-161">7.2</span></span> |<span data-ttu-id="314ae-162">последних</span><span class="sxs-lookup"><span data-stu-id="314ae-162">latest</span></span> |
| <span data-ttu-id="314ae-163">SLES</span><span class="sxs-lookup"><span data-stu-id="314ae-163">SLES</span></span> |<span data-ttu-id="314ae-164">SLES</span><span class="sxs-lookup"><span data-stu-id="314ae-164">SLES</span></span> |<span data-ttu-id="314ae-165">SLES</span><span class="sxs-lookup"><span data-stu-id="314ae-165">SLES</span></span> |<span data-ttu-id="314ae-166">12-SP1</span><span class="sxs-lookup"><span data-stu-id="314ae-166">12-SP1</span></span> |<span data-ttu-id="314ae-167">последних</span><span class="sxs-lookup"><span data-stu-id="314ae-167">latest</span></span> |
| <span data-ttu-id="314ae-168">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="314ae-168">UbuntuLTS</span></span> |<span data-ttu-id="314ae-169">Canonical</span><span class="sxs-lookup"><span data-stu-id="314ae-169">Canonical</span></span> |<span data-ttu-id="314ae-170">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="314ae-170">UbuntuServer</span></span> |<span data-ttu-id="314ae-171">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="314ae-171">14.04.4-LTS</span></span> |<span data-ttu-id="314ae-172">последних</span><span class="sxs-lookup"><span data-stu-id="314ae-172">latest</span></span> |

### <a name="use-your-own-image"></a><span data-ttu-id="314ae-173">Использование своего образа</span><span class="sxs-lookup"><span data-stu-id="314ae-173">Use your own image</span></span>
<span data-ttu-id="314ae-174">Если вам требуются особые настройки, используйте образ на основе имеющейся виртуальной машины Azure. Для этого запишите образ такой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="314ae-174">If you require specific customizations, you can use an image based on an existing Azure VM by capturing that VM.</span></span> <span data-ttu-id="314ae-175">Вы также можете отправить собственный образ, созданный на локальном диске.</span><span class="sxs-lookup"><span data-stu-id="314ae-175">You can also upload an image created on-premises.</span></span> <span data-ttu-id="314ae-176">Дополнительные сведения о поддерживаемых дистрибутивах и использовании собственных образов см. в следующих статьях.</span><span class="sxs-lookup"><span data-stu-id="314ae-176">For more information on supported distros and how to use your own images, see the following articles:</span></span>

* [<span data-ttu-id="314ae-177">Linux on Azure-Endorsed Distributions (Linux на дистрибутивах, рекомендованных для Azure)</span><span class="sxs-lookup"><span data-stu-id="314ae-177">Azure endorsed distributions</span></span>](endorsed-distros.md)
* [<span data-ttu-id="314ae-178">Information for Non-Endorsed Distributions (Информация о нерекомендованных дистрибутивах)</span><span class="sxs-lookup"><span data-stu-id="314ae-178">Information for non-endorsed distributions</span></span>](create-upload-generic.md)
* <span data-ttu-id="314ae-179">[Создание образа на основе существующей виртуальной машины Azure](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="314ae-179">[How to create an image from an existing Azure VM](tutorial-custom-images.md).</span></span>
  
  * <span data-ttu-id="314ae-180">Примеры команд для быстрого начала работы, с помощью которых можно создать образ на основе существующей виртуальной машины Azure:</span><span class="sxs-lookup"><span data-stu-id="314ae-180">Quick-start example commands to create an image from an existing Azure VM:</span></span>
    
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm generalize --resource-group myResourceGroup --name myVM
    az vm image create --resource-group myResourceGroup --source myVM --name myImage
    ```

## <a name="next-steps"></a><span data-ttu-id="314ae-181">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="314ae-181">Next steps</span></span>
* <span data-ttu-id="314ae-182">Создайте виртуальную машину Linux с помощью [интерфейса командной строки](quick-create-cli.md), [портала](quick-create-portal.md) или [шаблона Azure Resource Manager](../windows/cli-deploy-templates.md).</span><span class="sxs-lookup"><span data-stu-id="314ae-182">Create a Linux VM with the [CLI](quick-create-cli.md), from the [portal](quick-create-portal.md), or using an [Azure Resource Manager template](../windows/cli-deploy-templates.md).</span></span>
* <span data-ttu-id="314ae-183">После создания виртуальной машины Linux [прочтите статью о дисках и хранилище Azure](tutorial-manage-disks.md).</span><span class="sxs-lookup"><span data-stu-id="314ae-183">After creating a Linux VM, [learn about Azure disks and storage](tutorial-manage-disks.md).</span></span>
* <span data-ttu-id="314ae-184">Способы быстрого [сброса пароля или SSH-ключей и управления пользователями](using-vmaccess-extension.md).</span><span class="sxs-lookup"><span data-stu-id="314ae-184">Quick steps to [reset a password or SSH keys and manage users](using-vmaccess-extension.md).</span></span>
