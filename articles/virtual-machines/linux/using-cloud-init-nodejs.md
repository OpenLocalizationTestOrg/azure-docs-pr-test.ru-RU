---
title: "Настройка создаваемой в Azure виртуальной машины Linux с помощью cloud-init | Документация Майкрософт"
description: "Как с помощью cloud-init настроить виртуальную машину Linux во время создания посредством Azure CLI 1.0."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/26/2016
ms.author: v-livech
ms.openlocfilehash: 0b6150bca333188666935b3c9aa02c4b33690db9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-cloud-init-to-customize-a-linux-vm-during-creation-with-the-azure-cli-10"></a><span data-ttu-id="63e95-103">Использование cloud-init для настройки виртуальной машины Linux во время создания с помощью Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="63e95-103">Use cloud-init to customize a Linux VM during creation with the Azure CLI 1.0</span></span>
<span data-ttu-id="63e95-104">В этой статье демонстрируется создание сценария cloud-init для задания имени узла, обновления установленных пакетов и управления учетными записями пользователей.</span><span class="sxs-lookup"><span data-stu-id="63e95-104">This article shows how to make a cloud-init script to set the hostname, update installed packages, and manage user accounts.</span></span>  <span data-ttu-id="63e95-105">Сценарии cloud-init вызываются во время создания виртуальной машины с помощью интерфейса командной строки Azure (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="63e95-105">The cloud-init scripts are called during the VM creation from Azure CLI.</span></span>  <span data-ttu-id="63e95-106">Для работы с этой статьей потребуется:</span><span class="sxs-lookup"><span data-stu-id="63e95-106">The article requires:</span></span>

* <span data-ttu-id="63e95-107">Учетная запись Azure ([получите бесплатную пробную версию](https://azure.microsoft.com/pricing/free-trial/)).</span><span class="sxs-lookup"><span data-stu-id="63e95-107">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="63e95-108">[Интерфейс командной строки Azure](../../cli-install-nodejs.md) с выполненным входом (с помощью команды `azure login`).</span><span class="sxs-lookup"><span data-stu-id="63e95-108">the [Azure CLI](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="63e95-109">Интерфейс командной строки Azure *нужно* переключить в режим Azure Resource Manager `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="63e95-109">the Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="63e95-110">Версии интерфейса командной строки для выполнения задачи</span><span class="sxs-lookup"><span data-stu-id="63e95-110">CLI versions to complete the task</span></span>
<span data-ttu-id="63e95-111">Вы можете выполнить задачу, используя одну из следующих версий интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="63e95-111">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="63e95-112">[Azure CLI 1.0](#quick-commands) — интерфейс командной строки для классической модели развертывания и модели развертывания Resource Manager (в этой статье).</span><span class="sxs-lookup"><span data-stu-id="63e95-112">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="63e95-113">[Azure CLI 2.0](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) — интерфейс командной строки следующего поколения для модели развертывания с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="63e95-113">[Azure CLI 2.0](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>

## <a name="quick-commands"></a><span data-ttu-id="63e95-114">Быстрые команды</span><span class="sxs-lookup"><span data-stu-id="63e95-114">Quick Commands</span></span>
<span data-ttu-id="63e95-115">Создайте сценарий cloud-init.txt, который задает имя узла, обновляет все пакеты и добавляет в Linux пользователя sudo.</span><span class="sxs-lookup"><span data-stu-id="63e95-115">Create a cloud-init.txt script that sets the hostname, updates all packages, and adds a sudo user to Linux.</span></span>

```sh
#cloud-config
hostname: myVMhostname
apt_upgrade: true
users:
  - name: myNewAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myVM
```
<span data-ttu-id="63e95-116">Создайте группу ресурсов для запуска виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="63e95-116">Create a resource group to launch VMs into.</span></span>

```azurecli
azure group create myResourceGroup westus
```

<span data-ttu-id="63e95-117">Создайте виртуальную машину Linux, используя cloud-init для ее настройки в процессе загрузки.</span><span class="sxs-lookup"><span data-stu-id="63e95-117">Create a Linux VM using cloud-init to configure it during boot.</span></span>

```azurecli
azure vm create \
  -g myResourceGroup \
  -n myVM \
  -l westus \
  -y Linux \
  -f myVMnic \
  -F myVNet \
  -P 10.0.0.0/22 \
  -j mySubnet \
  -k 10.0.0.0/24 \
  -Q canonical:ubuntuserver:14.04.2-LTS:latest \
  -M ~/.ssh/id_rsa.pub \
  -u myAdminUser \
  -C cloud-init.txt
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="63e95-118">Подробное пошаговое руководство</span><span class="sxs-lookup"><span data-stu-id="63e95-118">Detailed walkthrough</span></span>
### <a name="introduction"></a><span data-ttu-id="63e95-119">Введение</span><span class="sxs-lookup"><span data-stu-id="63e95-119">Introduction</span></span>
<span data-ttu-id="63e95-120">При запуске новой виртуальной машины Linux вы получаете стандартную виртуальную машину, не настроенную под ваши потребности.</span><span class="sxs-lookup"><span data-stu-id="63e95-120">When you launch a new Linux VM, you are getting a standard Linux VM with nothing customized or ready for your needs.</span></span> <span data-ttu-id="63e95-121">[Cloud-init](https://cloudinit.readthedocs.org) — это стандартный способ добавления сценария или параметров конфигурации в виртуальную машину Linux при ее первоначальной загрузке.</span><span class="sxs-lookup"><span data-stu-id="63e95-121">[Cloud-init](https://cloudinit.readthedocs.org) is a standard way to inject a script or configuration settings into that Linux VM as it is booting up for the first time.</span></span>

<span data-ttu-id="63e95-122">В Azure есть три разных способа внесения изменений в виртуальную машину Linux в процессе ее развертывания или загрузки.</span><span class="sxs-lookup"><span data-stu-id="63e95-122">On Azure, there are a three different ways to make changes onto a Linux VM as it is being deployed or booted.</span></span>

* <span data-ttu-id="63e95-123">Внедрить сценарии с помощью cloud-init.</span><span class="sxs-lookup"><span data-stu-id="63e95-123">Inject scripts using cloud-init.</span></span>
* <span data-ttu-id="63e95-124">Внедрить сценарии с помощью [расширения VMAccess](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)Azure.</span><span class="sxs-lookup"><span data-stu-id="63e95-124">Inject scripts using the Azure [VMAccess Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="63e95-125">Шаблон Azure с использованием cloud-init.</span><span class="sxs-lookup"><span data-stu-id="63e95-125">An Azure template using cloud-init.</span></span>
* <span data-ttu-id="63e95-126">Шаблон Azure с использованием расширения [CustomScriptExtention](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="63e95-126">An Azure template using [CustomScriptExtention](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="63e95-127">Для внедрения сценариев в любой момент после загрузки можно воспользоваться одним из ниже приведенных способов.</span><span class="sxs-lookup"><span data-stu-id="63e95-127">To inject scripts at any time after boot:</span></span>

* <span data-ttu-id="63e95-128">Подключиться по SSH для выполнения команд напрямую.</span><span class="sxs-lookup"><span data-stu-id="63e95-128">SSH to run commands directly</span></span>
* <span data-ttu-id="63e95-129">Внедрить сценарии с помощью [расширения VMAccess](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)Azure принудительно или через шаблон Azure.</span><span class="sxs-lookup"><span data-stu-id="63e95-129">Inject scripts using the Azure [VMAccess Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), either imperatively or in an Azure template</span></span>
* <span data-ttu-id="63e95-130">Воспользоваться средствами управления, такими как Ansible, Salt, Chef или Puppet.</span><span class="sxs-lookup"><span data-stu-id="63e95-130">Configuration management tools like Ansible, Salt, Chef, and Puppet.</span></span>

> [!NOTE]
> <span data-ttu-id="63e95-131">Расширение VMAccess выполняет сценарий от имени привилегированного пользователя, так же как при использовании протокола SSH.</span><span class="sxs-lookup"><span data-stu-id="63e95-131">: VMAccess Extension executes a script as root in the same way using SSH can.</span></span>  <span data-ttu-id="63e95-132">Однако применение расширения для виртуальных машин обеспечивает ряд предлагаемых Azure возможностей, которые могут быть полезны в некоторых сценариях.</span><span class="sxs-lookup"><span data-stu-id="63e95-132">However, using the VM extension enables several features that Azure offers that can be useful depending upon your scenario.</span></span>
> 
> 

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a><span data-ttu-id="63e95-133">Доступность cloud-init для псевдонимов быстрого создания образов виртуальных машин Azure:</span><span class="sxs-lookup"><span data-stu-id="63e95-133">Cloud-init availability on Azure VM quick-create image aliases:</span></span>
| <span data-ttu-id="63e95-134">Alias</span><span class="sxs-lookup"><span data-stu-id="63e95-134">Alias</span></span> | <span data-ttu-id="63e95-135">Издатель</span><span class="sxs-lookup"><span data-stu-id="63e95-135">Publisher</span></span> | <span data-ttu-id="63e95-136">ПРЕДЛОЖЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="63e95-136">Offer</span></span> | <span data-ttu-id="63e95-137">SKU</span><span class="sxs-lookup"><span data-stu-id="63e95-137">SKU</span></span> | <span data-ttu-id="63e95-138">Version (версия)</span><span class="sxs-lookup"><span data-stu-id="63e95-138">Version</span></span> | <span data-ttu-id="63e95-139">cloud-init</span><span class="sxs-lookup"><span data-stu-id="63e95-139">cloud-init</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="63e95-140">CentOS</span><span class="sxs-lookup"><span data-stu-id="63e95-140">CentOS</span></span> |<span data-ttu-id="63e95-141">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="63e95-141">OpenLogic</span></span> |<span data-ttu-id="63e95-142">CentOS</span><span class="sxs-lookup"><span data-stu-id="63e95-142">Centos</span></span> |<span data-ttu-id="63e95-143">7,2</span><span class="sxs-lookup"><span data-stu-id="63e95-143">7.2</span></span> |<span data-ttu-id="63e95-144">последних</span><span class="sxs-lookup"><span data-stu-id="63e95-144">latest</span></span> |<span data-ttu-id="63e95-145">Нет</span><span class="sxs-lookup"><span data-stu-id="63e95-145">no</span></span> |
| <span data-ttu-id="63e95-146">CoreOS</span><span class="sxs-lookup"><span data-stu-id="63e95-146">CoreOS</span></span> |<span data-ttu-id="63e95-147">CoreOS</span><span class="sxs-lookup"><span data-stu-id="63e95-147">CoreOS</span></span> |<span data-ttu-id="63e95-148">CoreOS</span><span class="sxs-lookup"><span data-stu-id="63e95-148">CoreOS</span></span> |<span data-ttu-id="63e95-149">Stable</span><span class="sxs-lookup"><span data-stu-id="63e95-149">Stable</span></span> |<span data-ttu-id="63e95-150">последних</span><span class="sxs-lookup"><span data-stu-id="63e95-150">latest</span></span> |<span data-ttu-id="63e95-151">Да</span><span class="sxs-lookup"><span data-stu-id="63e95-151">yes</span></span> |
| <span data-ttu-id="63e95-152">Debian</span><span class="sxs-lookup"><span data-stu-id="63e95-152">Debian</span></span> |<span data-ttu-id="63e95-153">credativ</span><span class="sxs-lookup"><span data-stu-id="63e95-153">credativ</span></span> |<span data-ttu-id="63e95-154">Debian</span><span class="sxs-lookup"><span data-stu-id="63e95-154">Debian</span></span> |<span data-ttu-id="63e95-155">8</span><span class="sxs-lookup"><span data-stu-id="63e95-155">8</span></span> |<span data-ttu-id="63e95-156">последних</span><span class="sxs-lookup"><span data-stu-id="63e95-156">latest</span></span> |<span data-ttu-id="63e95-157">Нет</span><span class="sxs-lookup"><span data-stu-id="63e95-157">no</span></span> |
| <span data-ttu-id="63e95-158">openSUSE</span><span class="sxs-lookup"><span data-stu-id="63e95-158">openSUSE</span></span> |<span data-ttu-id="63e95-159">SUSE</span><span class="sxs-lookup"><span data-stu-id="63e95-159">SUSE</span></span> |<span data-ttu-id="63e95-160">openSUSE</span><span class="sxs-lookup"><span data-stu-id="63e95-160">openSUSE</span></span> |<span data-ttu-id="63e95-161">13.2</span><span class="sxs-lookup"><span data-stu-id="63e95-161">13.2</span></span> |<span data-ttu-id="63e95-162">последних</span><span class="sxs-lookup"><span data-stu-id="63e95-162">latest</span></span> |<span data-ttu-id="63e95-163">Нет</span><span class="sxs-lookup"><span data-stu-id="63e95-163">no</span></span> |
| <span data-ttu-id="63e95-164">RHEL</span><span class="sxs-lookup"><span data-stu-id="63e95-164">RHEL</span></span> |<span data-ttu-id="63e95-165">Redhat</span><span class="sxs-lookup"><span data-stu-id="63e95-165">Redhat</span></span> |<span data-ttu-id="63e95-166">RHEL</span><span class="sxs-lookup"><span data-stu-id="63e95-166">RHEL</span></span> |<span data-ttu-id="63e95-167">7,2</span><span class="sxs-lookup"><span data-stu-id="63e95-167">7.2</span></span> |<span data-ttu-id="63e95-168">последних</span><span class="sxs-lookup"><span data-stu-id="63e95-168">latest</span></span> |<span data-ttu-id="63e95-169">Нет</span><span class="sxs-lookup"><span data-stu-id="63e95-169">no</span></span> |
| <span data-ttu-id="63e95-170">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="63e95-170">UbuntuLTS</span></span> |<span data-ttu-id="63e95-171">Canonical</span><span class="sxs-lookup"><span data-stu-id="63e95-171">Canonical</span></span> |<span data-ttu-id="63e95-172">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="63e95-172">UbuntuServer</span></span> |<span data-ttu-id="63e95-173">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="63e95-173">14.04.4-LTS</span></span> |<span data-ttu-id="63e95-174">последних</span><span class="sxs-lookup"><span data-stu-id="63e95-174">latest</span></span> |<span data-ttu-id="63e95-175">Да</span><span class="sxs-lookup"><span data-stu-id="63e95-175">yes</span></span> |

<span data-ttu-id="63e95-176">Корпорация Майкрософт работает со своими партнерами над тем, чтобы сценарии cloud-init были добавлены в образы, предоставляемые ими для Azure.</span><span class="sxs-lookup"><span data-stu-id="63e95-176">Microsoft is working with our partners to get cloud-init included and working in the images that they provide to Azure.</span></span>

## <a name="adding-a-cloud-init-script-to-the-vm-creation-with-the-azure-cli"></a><span data-ttu-id="63e95-177">Добавление сценария cloud-init в создаваемую виртуальную машину с помощью интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="63e95-177">Adding a cloud-init script to the VM creation with the Azure CLI</span></span>
<span data-ttu-id="63e95-178">Чтобы запустить сценарий cloud-init при создании виртуальной машины в Azure, укажите файл cloud-init с помощью параметра `--custom-data` интерфейса командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="63e95-178">To launch a cloud-init script when creating a VM in Azure, specify the cloud-init file using the Azure CLI `--custom-data` switch.</span></span>

<span data-ttu-id="63e95-179">Создайте группу ресурсов для запуска виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="63e95-179">Create a resource group to launch VMs into.</span></span>

```azurecli
azure group create myResourceGroup westus
```

<span data-ttu-id="63e95-180">Создайте виртуальную машину Linux, используя cloud-init для ее настройки в процессе загрузки.</span><span class="sxs-lookup"><span data-stu-id="63e95-180">Create a Linux VM using cloud-init to configure it during boot.</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubnet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud-init.txt
```

## <a name="creating-a-cloud-init-script-to-set-the-hostname-of-a-linux-vm"></a><span data-ttu-id="63e95-181">Создание сценария cloud-init для задания имени узла виртуальной машины Linux</span><span class="sxs-lookup"><span data-stu-id="63e95-181">Creating a cloud-init script to set the hostname of a Linux VM</span></span>
<span data-ttu-id="63e95-182">Один из самых простых, но наиболее важных параметров для любой виртуальной машины Linux — это имя узла.</span><span class="sxs-lookup"><span data-stu-id="63e95-182">One of the simplest and most important settings for any Linux VM would be the hostname.</span></span> <span data-ttu-id="63e95-183">Его можно легко задать с помощью приведенного ниже сценария cloud-init.</span><span class="sxs-lookup"><span data-stu-id="63e95-183">We can easily set this using cloud-init with this script.</span></span>  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a><span data-ttu-id="63e95-184">Пример сценария cloud-init с именем `cloud_config_hostname.txt`</span><span class="sxs-lookup"><span data-stu-id="63e95-184">Example cloud-init script named `cloud_config_hostname.txt`.</span></span>
```sh
#cloud-config
hostname: myservername
```

<span data-ttu-id="63e95-185">Во время первоначального запуска виртуальной машины этот сценарий cloud-init задает имя узла `myservername`.</span><span class="sxs-lookup"><span data-stu-id="63e95-185">During the initial startup of the VM, this cloud-init script sets the hostname to `myservername`.</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud_config_hostname.txt
```

<span data-ttu-id="63e95-186">Выполните вход и проверьте имя узла новой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="63e95-186">Login and verify the hostname of the new VM.</span></span>

```bash
ssh myVM
hostname
myservername
```

## <a name="creating-a-cloud-init-script-to-update-linux"></a><span data-ttu-id="63e95-187">Создание сценария cloud-init для обновления виртуальной машины Linux</span><span class="sxs-lookup"><span data-stu-id="63e95-187">Creating a cloud-init script to update Linux</span></span>
<span data-ttu-id="63e95-188">В целях безопасности виртуальную машину Ubuntu следует обновить при первой загрузке.</span><span class="sxs-lookup"><span data-stu-id="63e95-188">For security, you want your Ubuntu VM to update on the first boot.</span></span>  <span data-ttu-id="63e95-189">Это можно сделать с помощью приведенного ниже сценария (сценарий зависит от используемого дистрибутива Linux).</span><span class="sxs-lookup"><span data-stu-id="63e95-189">Using cloud-init we can do that with the follow script, depending on the Linux distribution you are using.</span></span>

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-the-debian-family"></a><span data-ttu-id="63e95-190">Пример сценария cloud-init `cloud_config_apt_upgrade.txt` для семейства Debian</span><span class="sxs-lookup"><span data-stu-id="63e95-190">Example cloud-init script `cloud_config_apt_upgrade.txt` for the Debian Family</span></span>
```sh
#cloud-config
apt_upgrade: true
```

<span data-ttu-id="63e95-191">После загрузки Linux все установленные пакеты обновляются через `apt-get`.</span><span class="sxs-lookup"><span data-stu-id="63e95-191">After Linux has booted, all the installed packages are updated via `apt-get`.</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud_config_apt_upgrade.txt
```

<span data-ttu-id="63e95-192">Выполните вход и проверьте, обновились ли все пакеты.</span><span class="sxs-lookup"><span data-stu-id="63e95-192">Login and verify all packages are updated.</span></span>

```bash
ssh myUbuntuVM
sudo apt-get upgrade
Reading package lists... Done
Building dependency tree
Reading state information... Done
Calculating upgrade... Done
The following packages have been kept back:
  linux-generic linux-headers-generic linux-image-generic
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
```

## <a name="creating-a-cloud-init-script-to-add-a-user-to-linux"></a><span data-ttu-id="63e95-193">Создание сценария cloud-init для добавления пользователя в Linux</span><span class="sxs-lookup"><span data-stu-id="63e95-193">Creating a cloud-init script to add a user to Linux</span></span>
<span data-ttu-id="63e95-194">Одна из первых задач, которую необходимо выполнить на любой из новых виртуальных машин Linux, — это добавление пользователя для себя или для того, чтобы не использовалась учетная запись `root`.</span><span class="sxs-lookup"><span data-stu-id="63e95-194">One of the first tasks on any new Linux VM is to add a user for yourself or to avoid using `root`.</span></span> <span data-ttu-id="63e95-195">Ключи SSH наиболее эффективны для обеспечения безопасности и удобства использования. Они добавляются в файл `~/.ssh/authorized_keys` с помощью данного сценария cloud-init.</span><span class="sxs-lookup"><span data-stu-id="63e95-195">SSH keys are best practice for security and for usability and they are added to the `~/.ssh/authorized_keys` file with this cloud-init script.</span></span>

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a><span data-ttu-id="63e95-196">Пример сценария cloud-init `cloud_config_add_users.txt` для семейства Debian</span><span class="sxs-lookup"><span data-stu-id="63e95-196">Example cloud-init script `cloud_config_add_users.txt` for Debian Family</span></span>
```sh
#cloud-config
users:
  - name: myCloudInitAddedAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myUbuntuVM
```

<span data-ttu-id="63e95-197">После загрузки Linux все внесенные в список пользователи создаются и добавляются в группу sudo.</span><span class="sxs-lookup"><span data-stu-id="63e95-197">After Linux has booted, all the listed users are created and added to the sudo group.</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud_config_add_users.txt
```

<span data-ttu-id="63e95-198">Выполните вход и проверьте созданного пользователя.</span><span class="sxs-lookup"><span data-stu-id="63e95-198">Login and verify the newly created user.</span></span>

```bash
ssh myVM
cat /etc/group
```

<span data-ttu-id="63e95-199">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="63e95-199">Output</span></span>

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a><span data-ttu-id="63e95-200">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="63e95-200">Next Steps</span></span>
<span data-ttu-id="63e95-201">Сценарии cloud-init становятся стандартным способом изменения виртуальной машины Linux при загрузке.</span><span class="sxs-lookup"><span data-stu-id="63e95-201">Cloud-init is becoming one standard way to modify your Linux VM on boot.</span></span> <span data-ttu-id="63e95-202">Azure также поддерживает расширения виртуальных машин, которые позволяют изменить виртуальную машину Linux при загрузке или во время ее выполнения.</span><span class="sxs-lookup"><span data-stu-id="63e95-202">Azure also has VM extensions, which allow you to modify your LinuxVM on boot or while it is running.</span></span> <span data-ttu-id="63e95-203">Например, можно воспользоваться расширением VMAccessExtension, предоставляемым в Azure, для сброса данных SSH или сведений о пользователях во время выполнения виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="63e95-203">For example, you can use the Azure VMAccessExtension to reset SSH or user information while the VM is running.</span></span> <span data-ttu-id="63e95-204">При использовании cloud-init для сброса пароля требуется перезагрузка.</span><span class="sxs-lookup"><span data-stu-id="63e95-204">With cloud-init, you would need a reboot to reset the password.</span></span>

[<span data-ttu-id="63e95-205">Обзор расширений и компонентов виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="63e95-205">About virtual machine extensions and features</span></span>](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="63e95-206">Управление пользователями, SSH и проверка или восстановление дисков в виртуальных машинах Azure с помощью расширения VMAccess</span><span class="sxs-lookup"><span data-stu-id="63e95-206">Manage users, SSH, and check or repair disks on Azure Linux VMs using the VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

