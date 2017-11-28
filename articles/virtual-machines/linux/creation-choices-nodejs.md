---
title: "Разные способы создания виртуальной машины Linux с помощью Azure CLI 1.0 | Документация Майкрософт"
description: "Узнайте о различных способах создания виртуальных машин Linux в Azure, а также воспользуйтесь ссылками на инструменты и руководства по каждому из этих способов."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f38f8a44-6c88-4490-a84a-46388212d24c
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: 
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 1eb90d44797d66f3e09811918ce5a7f4ad4287c6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="different-ways-to-create-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="97cbd-103">Различные способы создания виртуальных машин Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="97cbd-103">Different ways to create a Linux virtual machine in Azure</span></span>
<span data-ttu-id="97cbd-104">Платформа Azure предоставляет гибкие решения по созданию виртуальных машин Linux. Здесь каждый пользователь найдет удобные для себя инструменты и рабочие процессы.</span><span class="sxs-lookup"><span data-stu-id="97cbd-104">You have the flexibility in Azure to create a Linux virtual machine (VM) using tools and workflows comfortable to you.</span></span> <span data-ttu-id="97cbd-105">В этой статье описаны разные решения и примеры создания виртуальных машин Linux.</span><span class="sxs-lookup"><span data-stu-id="97cbd-105">This article summarizes these differences and examples for creating your Linux VMs.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="97cbd-106">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="97cbd-106">Azure CLI</span></span>
<span data-ttu-id="97cbd-107">Виртуальные машины в Azure можно создавать с помощью одной из следующих версий интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="97cbd-107">You can create VMs in Azure using one of the following CLI versions:</span></span>

- <span data-ttu-id="97cbd-108">Azure CLI 1.0 — интерфейс командной строки для классической модели развертывания и модели развертывания Resource Manager (в этой статье).</span><span class="sxs-lookup"><span data-stu-id="97cbd-108">Azure CLI 1.0 – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="97cbd-109">[Azure CLI 2.0](../windows/creation-choices.md) — интерфейс командной строки следующего поколения для модели развертывания с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="97cbd-109">[Azure CLI 2.0](../windows/creation-choices.md) - our next generation CLI for the resource management deployment model</span></span>

<span data-ttu-id="97cbd-110">Интерфейс командной строки Azure CLI 1.0 доступен на разных платформах с использованием пакета npm, предоставленных для дистрибутивов пакетов или контейнера Docker.</span><span class="sxs-lookup"><span data-stu-id="97cbd-110">The Azure CLI 1.0 is available across platforms via an npm package, distro-provided packages, or Docker container.</span></span> <span data-ttu-id="97cbd-111">Дополнительные сведения об [установке и настройке интерфейса командной строки Azure](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="97cbd-111">You can read more about [how to install and configure the Azure CLI](../../cli-install-nodejs.md).</span></span> <span data-ttu-id="97cbd-112">В приведенных ниже руководствах содержатся примеры использования Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="97cbd-112">The following tutorials provide examples on using the Azure CLI 1.0.</span></span> <span data-ttu-id="97cbd-113">В каждой из этих статей подробно описана соответствующая команда быстрого запуска интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="97cbd-113">Read each article for more details on the CLI quick-start commands shown:</span></span>

* [<span data-ttu-id="97cbd-114">Создание виртуальной машины Linux в Azure с помощью интерфейса командной строки</span><span class="sxs-lookup"><span data-stu-id="97cbd-114">Create a Linux VM from the Azure CLI for dev and test</span></span>](quick-create-cli-nodejs.md)
  
  * <span data-ttu-id="97cbd-115">Следующий пример демонстрирует создание виртуальной машины CoreOS при помощи открытого ключа с именем *azure_id_rsa.pub*:</span><span class="sxs-lookup"><span data-stu-id="97cbd-115">The following example creates a CoreOS VM using a public key named *azure_id_rsa.pub*:</span></span>
    
    ```azurecli
    azure vm quick-create -ssh-publickey-file ~/.ssh/azure_id_rsa.pub \
      --image-urn CoreOS
    ```
* [<span data-ttu-id="97cbd-116">Создание защищенной виртуальной машины Linux с помощью шаблона Azure</span><span class="sxs-lookup"><span data-stu-id="97cbd-116">Create a secured Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md)
  
  * <span data-ttu-id="97cbd-117">В следующем примере виртуальная машина создается на основе шаблона, который хранится на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="97cbd-117">The following example creates a VM using a template stored on GitHub:</span></span>
    
    ```azurecli
    azure group create --name myResourceGroup --location eastus 
      --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
    ```
* [<span data-ttu-id="97cbd-118">Создание полной среды Linux с помощью интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="97cbd-118">Create a complete Linux environment using the Azure CLI</span></span>](create-cli-complete-nodejs.md)
  
  * <span data-ttu-id="97cbd-119">Включает создание балансировщика нагрузки и нескольких виртуальных машин в группе доступности.</span><span class="sxs-lookup"><span data-stu-id="97cbd-119">Includes creating a load balancer and multiple VMs in an availability set.</span></span>
* [<span data-ttu-id="97cbd-120">Добавление диска к виртуальной машине Linux</span><span class="sxs-lookup"><span data-stu-id="97cbd-120">Add a disk to a Linux VM</span></span>](add-disk.md)
  
  * <span data-ttu-id="97cbd-121">В следующем примере показано, как добавить диск объемом *5* ГБ к существующей виртуальной машине с именем *myVM*:</span><span class="sxs-lookup"><span data-stu-id="97cbd-121">The following example adds a *5* Gb disk to an existing VM named *myVM*:</span></span>
    
    ```azurecli
    azure vm disk attach-new \
        --resource-group myResourceGroup \
        --vm-name myVM \
        --size-in-GB 5
    ```

## <a name="azure-portal"></a><span data-ttu-id="97cbd-122">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="97cbd-122">Azure portal</span></span>
<span data-ttu-id="97cbd-123">С помощью [портала Azure](https://portal.azure.com) можно быстро создать виртуальную машину, так как установка компонентов в локальной системе не требуется.</span><span class="sxs-lookup"><span data-stu-id="97cbd-123">The [Azure portal](https://portal.azure.com) allows you to quickly create a VM since there is nothing to install on your system.</span></span> <span data-ttu-id="97cbd-124">Для создания виртуальной машины используйте портал Azure:</span><span class="sxs-lookup"><span data-stu-id="97cbd-124">Use the Azure portal to create the VM:</span></span>

* [<span data-ttu-id="97cbd-125">Создание виртуальной машины Linux в Azure с помощью портала</span><span class="sxs-lookup"><span data-stu-id="97cbd-125">Create a Linux VM using the Azure portal</span></span>](quick-create-portal.md) 

## <a name="operating-system-and-image-choices"></a><span data-ttu-id="97cbd-126">Операционная система и варианты образов</span><span class="sxs-lookup"><span data-stu-id="97cbd-126">Operating system and image choices</span></span>
<span data-ttu-id="97cbd-127">При создании виртуальной машины можно выбрать образ для операционной системы, которую необходимо запустить.</span><span class="sxs-lookup"><span data-stu-id="97cbd-127">When creating a VM, you choose an image based on the operating system you want to run.</span></span> <span data-ttu-id="97cbd-128">Azure и партнеры предлагают множество образов, некоторые из которых содержат предустановленные приложения и средства.</span><span class="sxs-lookup"><span data-stu-id="97cbd-128">Azure and its partners offer many images, some of which include applications and tools pre-installed.</span></span> <span data-ttu-id="97cbd-129">Вы также можете передать один из созданных вами образов (см. [следующий раздел](#use-your-own-image)).</span><span class="sxs-lookup"><span data-stu-id="97cbd-129">Or, upload one of your own images (see [the following section](#use-your-own-image)).</span></span>

### <a name="azure-images"></a><span data-ttu-id="97cbd-130">Образы Azure</span><span class="sxs-lookup"><span data-stu-id="97cbd-130">Azure images</span></span>
<span data-ttu-id="97cbd-131">Чтобы просмотреть список доступных издателей, дистрибутивов и сборок, используйте команды интерфейса командной строки `azure vm image` .</span><span class="sxs-lookup"><span data-stu-id="97cbd-131">Use the `azure vm image` CLI commands to see what's available by publisher, distro release, and builds.</span></span>

<span data-ttu-id="97cbd-132">Отображение списка доступных издателей:</span><span class="sxs-lookup"><span data-stu-id="97cbd-132">List available publishers as follows:</span></span>

```azurecli
azure vm image list-publishers --location eastus
```

<span data-ttu-id="97cbd-133">Отображение списка доступных продуктов (предложений) нужного издателя:</span><span class="sxs-lookup"><span data-stu-id="97cbd-133">List available products (offers) for a given publisher as follows:</span></span>

```azurecli
azure vm image list-offers --location eastus --publisher Canonical
```

<span data-ttu-id="97cbd-134">Отображение списка доступных номеров SKU (дистрибутивов) требуемого предложения:</span><span class="sxs-lookup"><span data-stu-id="97cbd-134">List available SKUs (distro releases) of a given offer as follows:</span></span>

```azurecli
azure vm image list-skus --location eastus --publisher Canonical --offer UbuntuServer
```

<span data-ttu-id="97cbd-135">Отображение списка всех доступных образов для определенного выпуска:</span><span class="sxs-lookup"><span data-stu-id="97cbd-135">List all available images for a given release follows:</span></span>

```azurecli
azure vm image list --location eastus --publisher Canonical --offer UbuntuServer --sku 16.04.0-LTS
```

<span data-ttu-id="97cbd-136">С командами `azure vm quick-create` и `azure vm create` также можно использовать псевдонимы для быстрого доступа к самым распространенным дистрибутивам и их последним выпускам.</span><span class="sxs-lookup"><span data-stu-id="97cbd-136">The `azure vm quick-create` and `azure vm create` commands have aliases you can use to quickly access the more common distros and their latest releases.</span></span> <span data-ttu-id="97cbd-137">Как правило, использовать псевдоним быстрее, чем указывать издателя, предложение, номер SKU и версию каждый раз при создании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="97cbd-137">Using aliases is often quicker than specifying the publisher, offer, SKU, and version each time you create a VM:</span></span>

| <span data-ttu-id="97cbd-138">Alias</span><span class="sxs-lookup"><span data-stu-id="97cbd-138">Alias</span></span> | <span data-ttu-id="97cbd-139">Издатель</span><span class="sxs-lookup"><span data-stu-id="97cbd-139">Publisher</span></span> | <span data-ttu-id="97cbd-140">ПРЕДЛОЖЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="97cbd-140">Offer</span></span> | <span data-ttu-id="97cbd-141">SKU</span><span class="sxs-lookup"><span data-stu-id="97cbd-141">SKU</span></span> | <span data-ttu-id="97cbd-142">Версия</span><span class="sxs-lookup"><span data-stu-id="97cbd-142">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="97cbd-143">CentOS</span><span class="sxs-lookup"><span data-stu-id="97cbd-143">CentOS</span></span> |<span data-ttu-id="97cbd-144">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="97cbd-144">OpenLogic</span></span> |<span data-ttu-id="97cbd-145">CentOS</span><span class="sxs-lookup"><span data-stu-id="97cbd-145">Centos</span></span> |<span data-ttu-id="97cbd-146">7,2</span><span class="sxs-lookup"><span data-stu-id="97cbd-146">7.2</span></span> |<span data-ttu-id="97cbd-147">последних</span><span class="sxs-lookup"><span data-stu-id="97cbd-147">latest</span></span> |
| <span data-ttu-id="97cbd-148">CoreOS</span><span class="sxs-lookup"><span data-stu-id="97cbd-148">CoreOS</span></span> |<span data-ttu-id="97cbd-149">CoreOS</span><span class="sxs-lookup"><span data-stu-id="97cbd-149">CoreOS</span></span> |<span data-ttu-id="97cbd-150">CoreOS</span><span class="sxs-lookup"><span data-stu-id="97cbd-150">CoreOS</span></span> |<span data-ttu-id="97cbd-151">Stable</span><span class="sxs-lookup"><span data-stu-id="97cbd-151">Stable</span></span> |<span data-ttu-id="97cbd-152">последняя</span><span class="sxs-lookup"><span data-stu-id="97cbd-152">latest</span></span> |
| <span data-ttu-id="97cbd-153">Debian</span><span class="sxs-lookup"><span data-stu-id="97cbd-153">Debian</span></span> |<span data-ttu-id="97cbd-154">credativ</span><span class="sxs-lookup"><span data-stu-id="97cbd-154">credativ</span></span> |<span data-ttu-id="97cbd-155">Debian</span><span class="sxs-lookup"><span data-stu-id="97cbd-155">Debian</span></span> |<span data-ttu-id="97cbd-156">8</span><span class="sxs-lookup"><span data-stu-id="97cbd-156">8</span></span> |<span data-ttu-id="97cbd-157">последняя</span><span class="sxs-lookup"><span data-stu-id="97cbd-157">latest</span></span> |
| <span data-ttu-id="97cbd-158">openSUSE</span><span class="sxs-lookup"><span data-stu-id="97cbd-158">openSUSE</span></span> |<span data-ttu-id="97cbd-159">SUSE</span><span class="sxs-lookup"><span data-stu-id="97cbd-159">SUSE</span></span> |<span data-ttu-id="97cbd-160">openSUSE</span><span class="sxs-lookup"><span data-stu-id="97cbd-160">openSUSE</span></span> |<span data-ttu-id="97cbd-161">13.2</span><span class="sxs-lookup"><span data-stu-id="97cbd-161">13.2</span></span> |<span data-ttu-id="97cbd-162">последних</span><span class="sxs-lookup"><span data-stu-id="97cbd-162">latest</span></span> |
| <span data-ttu-id="97cbd-163">RHEL</span><span class="sxs-lookup"><span data-stu-id="97cbd-163">RHEL</span></span> |<span data-ttu-id="97cbd-164">Redhat</span><span class="sxs-lookup"><span data-stu-id="97cbd-164">Redhat</span></span> |<span data-ttu-id="97cbd-165">RHEL</span><span class="sxs-lookup"><span data-stu-id="97cbd-165">RHEL</span></span> |<span data-ttu-id="97cbd-166">7,2</span><span class="sxs-lookup"><span data-stu-id="97cbd-166">7.2</span></span> |<span data-ttu-id="97cbd-167">последних</span><span class="sxs-lookup"><span data-stu-id="97cbd-167">latest</span></span> |
| <span data-ttu-id="97cbd-168">SLES</span><span class="sxs-lookup"><span data-stu-id="97cbd-168">SLES</span></span> |<span data-ttu-id="97cbd-169">SLES</span><span class="sxs-lookup"><span data-stu-id="97cbd-169">SLES</span></span> |<span data-ttu-id="97cbd-170">SLES</span><span class="sxs-lookup"><span data-stu-id="97cbd-170">SLES</span></span> |<span data-ttu-id="97cbd-171">12-SP1</span><span class="sxs-lookup"><span data-stu-id="97cbd-171">12-SP1</span></span> |<span data-ttu-id="97cbd-172">последних</span><span class="sxs-lookup"><span data-stu-id="97cbd-172">latest</span></span> |
| <span data-ttu-id="97cbd-173">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="97cbd-173">UbuntuLTS</span></span> |<span data-ttu-id="97cbd-174">Canonical</span><span class="sxs-lookup"><span data-stu-id="97cbd-174">Canonical</span></span> |<span data-ttu-id="97cbd-175">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="97cbd-175">UbuntuServer</span></span> |<span data-ttu-id="97cbd-176">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="97cbd-176">14.04.4-LTS</span></span> |<span data-ttu-id="97cbd-177">последних</span><span class="sxs-lookup"><span data-stu-id="97cbd-177">latest</span></span> |

### <a name="use-your-own-image"></a><span data-ttu-id="97cbd-178">Использование своего образа</span><span class="sxs-lookup"><span data-stu-id="97cbd-178">Use your own image</span></span>
<span data-ttu-id="97cbd-179">Если вам требуются особые настройки, используйте образ на основе имеющейся виртуальной машины Azure. Для этого *запишите* образ такой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="97cbd-179">If you require specific customizations, you can use an image based on an existing Azure VM by *capturing* that VM.</span></span> <span data-ttu-id="97cbd-180">Вы также можете отправить собственный образ, созданный на локальном диске.</span><span class="sxs-lookup"><span data-stu-id="97cbd-180">You can also upload an image created on-premises.</span></span> <span data-ttu-id="97cbd-181">Дополнительные сведения о поддерживаемых дистрибутивах и использовании собственных образов см. в следующих статьях.</span><span class="sxs-lookup"><span data-stu-id="97cbd-181">For more information on supported distros and how to use your own images, see the following articles:</span></span>

* [<span data-ttu-id="97cbd-182">Linux on Azure-Endorsed Distributions (Linux на дистрибутивах, рекомендованных для Azure)</span><span class="sxs-lookup"><span data-stu-id="97cbd-182">Azure endorsed distributions</span></span>](endorsed-distros.md)
* [<span data-ttu-id="97cbd-183">Information for Non-Endorsed Distributions (Информация о нерекомендованных дистрибутивах)</span><span class="sxs-lookup"><span data-stu-id="97cbd-183">Information for non-endorsed distributions</span></span>](create-upload-generic.md)
* [<span data-ttu-id="97cbd-184">Передача пользовательского образа диска и создание виртуальной машины Linux на его основе</span><span class="sxs-lookup"><span data-stu-id="97cbd-184">Upload and create a Linux VM from custom disk image</span></span>](upload-vhd.md)
* <span data-ttu-id="97cbd-185">[Как записать образ виртуальной машины Linux для его использования в качестве шаблона Resource Manager](capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="97cbd-185">[How to capture a Linux virtual machine as a Resource Manager template](capture-image.md).</span></span>
  
  * <span data-ttu-id="97cbd-186">Примеры команд для быстрой записи существующей виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="97cbd-186">Quick-start example commands to capture an existing VM:</span></span>
    
    ```azurecli
    azure vm deallocate --resource-group myResourceGroup --vm-name myVM
    azure vm generalize --resource-group myResourceGroup --vm-name myVM
    azure vm capture --resource-group myResourceGroup --vm-name myVM --vhd-name-prefix myCapturedVM
    ```

## <a name="next-steps"></a><span data-ttu-id="97cbd-187">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="97cbd-187">Next steps</span></span>
* <span data-ttu-id="97cbd-188">Создайте виртуальную машину Linux с помощью [портала](quick-create-portal.md), [интерфейса командной строки](quick-create-cli.md) или [шаблона Azure Resource Manager](../windows/cli-deploy-templates.md).</span><span class="sxs-lookup"><span data-stu-id="97cbd-188">Create a Linux VM from the [portal](quick-create-portal.md), with the [CLI](quick-create-cli.md), or using an [Azure Resource Manager template](../windows/cli-deploy-templates.md).</span></span>
* <span data-ttu-id="97cbd-189">После создания виртуальной машины Linux [добавьте диск данных](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="97cbd-189">After creating a Linux VM, [add a data disk](add-disk.md).</span></span>
* <span data-ttu-id="97cbd-190">Способы быстрого [сброса пароля или SSH-ключей и управления пользователями](using-vmaccess-extension.md)</span><span class="sxs-lookup"><span data-stu-id="97cbd-190">Quick steps to [reset a password or SSH keys and manage users](using-vmaccess-extension.md)</span></span>

