---
title: "toocustomize aaaUsing init облака виртуальной Машины Linux во время создания в Azure | Документы Microsoft"
description: "Как облачные init toocustomize toouse в виртуальной Машине Linux во время создания с hello Azure CLI 1.0"
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
ms.openlocfilehash: b9f480bd04029956d0593bbef931795733cbc2f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-cloud-init-toocustomize-a-linux-vm-during-creation-with-hello-azure-cli-10"></a><span data-ttu-id="ad785-103">Использовать toocustomize init облака виртуальной Машины Linux во время создания с hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="ad785-103">Use cloud-init toocustomize a Linux VM during creation with hello Azure CLI 1.0</span></span>
<span data-ttu-id="ad785-104">В этой статье показано, как toomake tooset сценарий облака init hello имя узла, установленных пакетов обновления и управление учетными записями пользователей.</span><span class="sxs-lookup"><span data-stu-id="ad785-104">This article shows how toomake a cloud-init script tooset hello hostname, update installed packages, and manage user accounts.</span></span>  <span data-ttu-id="ad785-105">во время создания виртуальной Машины из Azure CLI hello вызываются Hello init облачных сценариев.</span><span class="sxs-lookup"><span data-stu-id="ad785-105">hello cloud-init scripts are called during hello VM creation from Azure CLI.</span></span>  <span data-ttu-id="ad785-106">требуются Hello статьи:</span><span class="sxs-lookup"><span data-stu-id="ad785-106">hello article requires:</span></span>

* <span data-ttu-id="ad785-107">Учетная запись Azure ([получите бесплатную пробную версию](https://azure.microsoft.com/pricing/free-trial/)).</span><span class="sxs-lookup"><span data-stu-id="ad785-107">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="ad785-108">Hello [Azure CLI](../../cli-install-nodejs.md) вход в систему `azure login`.</span><span class="sxs-lookup"><span data-stu-id="ad785-108">hello [Azure CLI](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="ad785-109">Hello Azure CLI *должен находиться в* режим диспетчера ресурсов Azure `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="ad785-109">hello Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="ad785-110">Задача hello toocomplete версии CLI</span><span class="sxs-lookup"><span data-stu-id="ad785-110">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="ad785-111">Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.</span><span class="sxs-lookup"><span data-stu-id="ad785-111">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="ad785-112">[Azure CLI 1.0](#quick-commands) — нашей CLI для hello классический и ресурса управления развертывания моделей (в этой статье)</span><span class="sxs-lookup"><span data-stu-id="ad785-112">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="ad785-113">[Azure CLI 2.0](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -нашей нового поколения CLI для модели развертывания hello ресурсов управления</span><span class="sxs-lookup"><span data-stu-id="ad785-113">[Azure CLI 2.0](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="quick-commands"></a><span data-ttu-id="ad785-114">Быстрые команды</span><span class="sxs-lookup"><span data-stu-id="ad785-114">Quick Commands</span></span>
<span data-ttu-id="ad785-115">Создание облака init.txt скрипт, который задает имя узла hello, все пакеты обновления и добавляет tooLinux sudo пользователя.</span><span class="sxs-lookup"><span data-stu-id="ad785-115">Create a cloud-init.txt script that sets hello hostname, updates all packages, and adds a sudo user tooLinux.</span></span>

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
<span data-ttu-id="ad785-116">Создание виртуальных машин в toolaunch группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ad785-116">Create a resource group toolaunch VMs into.</span></span>

```azurecli
azure group create myResourceGroup westus
```

<span data-ttu-id="ad785-117">Создайте виртуальную Машину Linux с помощью облака init tooconfigure его во время загрузки.</span><span class="sxs-lookup"><span data-stu-id="ad785-117">Create a Linux VM using cloud-init tooconfigure it during boot.</span></span>

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

## <a name="detailed-walkthrough"></a><span data-ttu-id="ad785-118">Подробное пошаговое руководство</span><span class="sxs-lookup"><span data-stu-id="ad785-118">Detailed walkthrough</span></span>
### <a name="introduction"></a><span data-ttu-id="ad785-119">Введение</span><span class="sxs-lookup"><span data-stu-id="ad785-119">Introduction</span></span>
<span data-ttu-id="ad785-120">При запуске новой виртуальной машины Linux вы получаете стандартную виртуальную машину, не настроенную под ваши потребности.</span><span class="sxs-lookup"><span data-stu-id="ad785-120">When you launch a new Linux VM, you are getting a standard Linux VM with nothing customized or ready for your needs.</span></span> <span data-ttu-id="ad785-121">[Облако init](https://cloudinit.readthedocs.org) является tooinject стандартный способ скрипт или конфигурации параметры в этой виртуальной Машины Linux при загрузке для hello первый раз.</span><span class="sxs-lookup"><span data-stu-id="ad785-121">[Cloud-init](https://cloudinit.readthedocs.org) is a standard way tooinject a script or configuration settings into that Linux VM as it is booting up for hello first time.</span></span>

<span data-ttu-id="ad785-122">В Azure, существует три различных способа изменения toomake на виртуальной Машине Linux время развернут или загружен.</span><span class="sxs-lookup"><span data-stu-id="ad785-122">On Azure, there are a three different ways toomake changes onto a Linux VM as it is being deployed or booted.</span></span>

* <span data-ttu-id="ad785-123">Внедрить сценарии с помощью cloud-init.</span><span class="sxs-lookup"><span data-stu-id="ad785-123">Inject scripts using cloud-init.</span></span>
* <span data-ttu-id="ad785-124">Внедрить скриптов с использованием hello Azure [расширения VMAccess](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ad785-124">Inject scripts using hello Azure [VMAccess Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="ad785-125">Шаблон Azure с использованием cloud-init.</span><span class="sxs-lookup"><span data-stu-id="ad785-125">An Azure template using cloud-init.</span></span>
* <span data-ttu-id="ad785-126">Шаблон Azure с использованием расширения [CustomScriptExtention](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ad785-126">An Azure template using [CustomScriptExtention](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="ad785-127">сценарии tooinject в любое время после загрузки.</span><span class="sxs-lookup"><span data-stu-id="ad785-127">tooinject scripts at any time after boot:</span></span>

* <span data-ttu-id="ad785-128">Непосредственно команды toorun SSH</span><span class="sxs-lookup"><span data-stu-id="ad785-128">SSH toorun commands directly</span></span>
* <span data-ttu-id="ad785-129">Внедрить скриптов с использованием hello Azure [расширения VMAccess](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), принудительно или в шаблоне Azure</span><span class="sxs-lookup"><span data-stu-id="ad785-129">Inject scripts using hello Azure [VMAccess Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), either imperatively or in an Azure template</span></span>
* <span data-ttu-id="ad785-130">Воспользоваться средствами управления, такими как Ansible, Salt, Chef или Puppet.</span><span class="sxs-lookup"><span data-stu-id="ad785-130">Configuration management tools like Ansible, Salt, Chef, and Puppet.</span></span>

> [!NOTE]
> <span data-ttu-id="ad785-131">: Расширение VMAccess выполняет скрипт как корневой hello же можно с помощью SSH.</span><span class="sxs-lookup"><span data-stu-id="ad785-131">: VMAccess Extension executes a script as root in hello same way using SSH can.</span></span>  <span data-ttu-id="ad785-132">Тем не менее использование расширения ВМ hello позволяет несколько функций, Azure предлагает, которые могут быть полезны в зависимости от ситуации.</span><span class="sxs-lookup"><span data-stu-id="ad785-132">However, using hello VM extension enables several features that Azure offers that can be useful depending upon your scenario.</span></span>
> 
> 

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a><span data-ttu-id="ad785-133">Доступность cloud-init для псевдонимов быстрого создания образов виртуальных машин Azure:</span><span class="sxs-lookup"><span data-stu-id="ad785-133">Cloud-init availability on Azure VM quick-create image aliases:</span></span>
| <span data-ttu-id="ad785-134">Alias</span><span class="sxs-lookup"><span data-stu-id="ad785-134">Alias</span></span> | <span data-ttu-id="ad785-135">Издатель</span><span class="sxs-lookup"><span data-stu-id="ad785-135">Publisher</span></span> | <span data-ttu-id="ad785-136">ПРЕДЛОЖЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="ad785-136">Offer</span></span> | <span data-ttu-id="ad785-137">SKU</span><span class="sxs-lookup"><span data-stu-id="ad785-137">SKU</span></span> | <span data-ttu-id="ad785-138">Version (версия)</span><span class="sxs-lookup"><span data-stu-id="ad785-138">Version</span></span> | <span data-ttu-id="ad785-139">cloud-init</span><span class="sxs-lookup"><span data-stu-id="ad785-139">cloud-init</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="ad785-140">CentOS</span><span class="sxs-lookup"><span data-stu-id="ad785-140">CentOS</span></span> |<span data-ttu-id="ad785-141">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="ad785-141">OpenLogic</span></span> |<span data-ttu-id="ad785-142">CentOS</span><span class="sxs-lookup"><span data-stu-id="ad785-142">Centos</span></span> |<span data-ttu-id="ad785-143">7,2</span><span class="sxs-lookup"><span data-stu-id="ad785-143">7.2</span></span> |<span data-ttu-id="ad785-144">последних</span><span class="sxs-lookup"><span data-stu-id="ad785-144">latest</span></span> |<span data-ttu-id="ad785-145">Нет</span><span class="sxs-lookup"><span data-stu-id="ad785-145">no</span></span> |
| <span data-ttu-id="ad785-146">CoreOS</span><span class="sxs-lookup"><span data-stu-id="ad785-146">CoreOS</span></span> |<span data-ttu-id="ad785-147">CoreOS</span><span class="sxs-lookup"><span data-stu-id="ad785-147">CoreOS</span></span> |<span data-ttu-id="ad785-148">CoreOS</span><span class="sxs-lookup"><span data-stu-id="ad785-148">CoreOS</span></span> |<span data-ttu-id="ad785-149">Stable</span><span class="sxs-lookup"><span data-stu-id="ad785-149">Stable</span></span> |<span data-ttu-id="ad785-150">последних</span><span class="sxs-lookup"><span data-stu-id="ad785-150">latest</span></span> |<span data-ttu-id="ad785-151">Да</span><span class="sxs-lookup"><span data-stu-id="ad785-151">yes</span></span> |
| <span data-ttu-id="ad785-152">Debian</span><span class="sxs-lookup"><span data-stu-id="ad785-152">Debian</span></span> |<span data-ttu-id="ad785-153">credativ</span><span class="sxs-lookup"><span data-stu-id="ad785-153">credativ</span></span> |<span data-ttu-id="ad785-154">Debian</span><span class="sxs-lookup"><span data-stu-id="ad785-154">Debian</span></span> |<span data-ttu-id="ad785-155">8</span><span class="sxs-lookup"><span data-stu-id="ad785-155">8</span></span> |<span data-ttu-id="ad785-156">последних</span><span class="sxs-lookup"><span data-stu-id="ad785-156">latest</span></span> |<span data-ttu-id="ad785-157">Нет</span><span class="sxs-lookup"><span data-stu-id="ad785-157">no</span></span> |
| <span data-ttu-id="ad785-158">openSUSE</span><span class="sxs-lookup"><span data-stu-id="ad785-158">openSUSE</span></span> |<span data-ttu-id="ad785-159">SUSE</span><span class="sxs-lookup"><span data-stu-id="ad785-159">SUSE</span></span> |<span data-ttu-id="ad785-160">openSUSE</span><span class="sxs-lookup"><span data-stu-id="ad785-160">openSUSE</span></span> |<span data-ttu-id="ad785-161">13.2</span><span class="sxs-lookup"><span data-stu-id="ad785-161">13.2</span></span> |<span data-ttu-id="ad785-162">последних</span><span class="sxs-lookup"><span data-stu-id="ad785-162">latest</span></span> |<span data-ttu-id="ad785-163">Нет</span><span class="sxs-lookup"><span data-stu-id="ad785-163">no</span></span> |
| <span data-ttu-id="ad785-164">RHEL</span><span class="sxs-lookup"><span data-stu-id="ad785-164">RHEL</span></span> |<span data-ttu-id="ad785-165">Redhat</span><span class="sxs-lookup"><span data-stu-id="ad785-165">Redhat</span></span> |<span data-ttu-id="ad785-166">RHEL</span><span class="sxs-lookup"><span data-stu-id="ad785-166">RHEL</span></span> |<span data-ttu-id="ad785-167">7,2</span><span class="sxs-lookup"><span data-stu-id="ad785-167">7.2</span></span> |<span data-ttu-id="ad785-168">последних</span><span class="sxs-lookup"><span data-stu-id="ad785-168">latest</span></span> |<span data-ttu-id="ad785-169">Нет</span><span class="sxs-lookup"><span data-stu-id="ad785-169">no</span></span> |
| <span data-ttu-id="ad785-170">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="ad785-170">UbuntuLTS</span></span> |<span data-ttu-id="ad785-171">Canonical</span><span class="sxs-lookup"><span data-stu-id="ad785-171">Canonical</span></span> |<span data-ttu-id="ad785-172">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="ad785-172">UbuntuServer</span></span> |<span data-ttu-id="ad785-173">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="ad785-173">14.04.4-LTS</span></span> |<span data-ttu-id="ad785-174">последних</span><span class="sxs-lookup"><span data-stu-id="ad785-174">latest</span></span> |<span data-ttu-id="ad785-175">Да</span><span class="sxs-lookup"><span data-stu-id="ad785-175">yes</span></span> |

<span data-ttu-id="ad785-176">Microsoft является работа с наших партнеров tooget облака init включены и работу в том, что они предоставляют tooAzure образы hello.</span><span class="sxs-lookup"><span data-stu-id="ad785-176">Microsoft is working with our partners tooget cloud-init included and working in hello images that they provide tooAzure.</span></span>

## <a name="adding-a-cloud-init-script-toohello-vm-creation-with-hello-azure-cli"></a><span data-ttu-id="ad785-177">Добавление создания облака init скрипта toohello ВМ с hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ad785-177">Adding a cloud-init script toohello VM creation with hello Azure CLI</span></span>
<span data-ttu-id="ad785-178">toolaunch сценарий init облака при создании виртуальной Машины в Azure, укажите файл init облака hello, с помощью hello Azure CLI `--custom-data` переключения.</span><span class="sxs-lookup"><span data-stu-id="ad785-178">toolaunch a cloud-init script when creating a VM in Azure, specify hello cloud-init file using hello Azure CLI `--custom-data` switch.</span></span>

<span data-ttu-id="ad785-179">Создание виртуальных машин в toolaunch группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ad785-179">Create a resource group toolaunch VMs into.</span></span>

```azurecli
azure group create myResourceGroup westus
```

<span data-ttu-id="ad785-180">Создайте виртуальную Машину Linux с помощью облака init tooconfigure его во время загрузки.</span><span class="sxs-lookup"><span data-stu-id="ad785-180">Create a Linux VM using cloud-init tooconfigure it during boot.</span></span>

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

## <a name="creating-a-cloud-init-script-tooset-hello-hostname-of-a-linux-vm"></a><span data-ttu-id="ad785-181">Создание облака init сценария tooset hello имени узла виртуальной машины Linux</span><span class="sxs-lookup"><span data-stu-id="ad785-181">Creating a cloud-init script tooset hello hostname of a Linux VM</span></span>
<span data-ttu-id="ad785-182">Одним из hello простейшим и наиболее важные параметры для виртуальной Машины с Linux будет hello имя узла.</span><span class="sxs-lookup"><span data-stu-id="ad785-182">One of hello simplest and most important settings for any Linux VM would be hello hostname.</span></span> <span data-ttu-id="ad785-183">Его можно легко задать с помощью приведенного ниже сценария cloud-init.</span><span class="sxs-lookup"><span data-stu-id="ad785-183">We can easily set this using cloud-init with this script.</span></span>  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a><span data-ttu-id="ad785-184">Пример сценария cloud-init с именем `cloud_config_hostname.txt`</span><span class="sxs-lookup"><span data-stu-id="ad785-184">Example cloud-init script named `cloud_config_hostname.txt`.</span></span>
```sh
#cloud-config
hostname: myservername
```

<span data-ttu-id="ad785-185">Во время запуска начальной hello hello виртуальной Машины, этот сценарий облака init задает hello hostname, слишком`myservername`.</span><span class="sxs-lookup"><span data-stu-id="ad785-185">During hello initial startup of hello VM, this cloud-init script sets hello hostname too`myservername`.</span></span>

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

<span data-ttu-id="ad785-186">Имя входа и проверьте имя узла hello hello новой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="ad785-186">Login and verify hello hostname of hello new VM.</span></span>

```bash
ssh myVM
hostname
myservername
```

## <a name="creating-a-cloud-init-script-tooupdate-linux"></a><span data-ttu-id="ad785-187">Создание облака init сценария tooupdate Linux</span><span class="sxs-lookup"><span data-stu-id="ad785-187">Creating a cloud-init script tooupdate Linux</span></span>
<span data-ttu-id="ad785-188">В целях безопасности необходимо tooupdate вашей виртуальной Машине Ubuntu при первой загрузке hello.</span><span class="sxs-lookup"><span data-stu-id="ad785-188">For security, you want your Ubuntu VM tooupdate on hello first boot.</span></span>  <span data-ttu-id="ad785-189">С помощью init облака можно сделать с hello выполните скрипт, в зависимости от hello дистрибутив Linux, которые вы используете.</span><span class="sxs-lookup"><span data-stu-id="ad785-189">Using cloud-init we can do that with hello follow script, depending on hello Linux distribution you are using.</span></span>

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-hello-debian-family"></a><span data-ttu-id="ad785-190">Пример сценария в облаке init `cloud_config_apt_upgrade.txt` для hello Debian семейства</span><span class="sxs-lookup"><span data-stu-id="ad785-190">Example cloud-init script `cloud_config_apt_upgrade.txt` for hello Debian Family</span></span>
```sh
#cloud-config
apt_upgrade: true
```

<span data-ttu-id="ad785-191">После загрузки операционной системы Linux, все пакеты установки hello обновляются через `apt-get`.</span><span class="sxs-lookup"><span data-stu-id="ad785-191">After Linux has booted, all hello installed packages are updated via `apt-get`.</span></span>

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

<span data-ttu-id="ad785-192">Выполните вход и проверьте, обновились ли все пакеты.</span><span class="sxs-lookup"><span data-stu-id="ad785-192">Login and verify all packages are updated.</span></span>

```bash
ssh myUbuntuVM
sudo apt-get upgrade
Reading package lists... Done
Building dependency tree
Reading state information... Done
Calculating upgrade... Done
hello following packages have been kept back:
  linux-generic linux-headers-generic linux-image-generic
0 upgraded, 0 newly installed, 0 tooremove and 0 not upgraded.
```

## <a name="creating-a-cloud-init-script-tooadd-a-user-toolinux"></a><span data-ttu-id="ad785-193">Создание tooadd сценария облака init tooLinux пользователя</span><span class="sxs-lookup"><span data-stu-id="ad785-193">Creating a cloud-init script tooadd a user tooLinux</span></span>
<span data-ttu-id="ad785-194">Один из первых задач hello на все новые виртуальные Машины Linux — tooadd пользователя для себя, или с помощью tooavoid `root`.</span><span class="sxs-lookup"><span data-stu-id="ad785-194">One of hello first tasks on any new Linux VM is tooadd a user for yourself or tooavoid using `root`.</span></span> <span data-ttu-id="ad785-195">SSH ключи — это рекомендуется для безопасности и удобство использования и они добавляются toohello `~/.ssh/authorized_keys` файл с помощью этого сценария init облака.</span><span class="sxs-lookup"><span data-stu-id="ad785-195">SSH keys are best practice for security and for usability and they are added toohello `~/.ssh/authorized_keys` file with this cloud-init script.</span></span>

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a><span data-ttu-id="ad785-196">Пример сценария cloud-init `cloud_config_add_users.txt` для семейства Debian</span><span class="sxs-lookup"><span data-stu-id="ad785-196">Example cloud-init script `cloud_config_add_users.txt` for Debian Family</span></span>
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

<span data-ttu-id="ad785-197">После загрузки операционной системы Linux, все пользователи в списке hello являются группа создана и добавлена toohello sudo.</span><span class="sxs-lookup"><span data-stu-id="ad785-197">After Linux has booted, all hello listed users are created and added toohello sudo group.</span></span>

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

<span data-ttu-id="ad785-198">Имя входа и проверки hello только что созданный пользователь.</span><span class="sxs-lookup"><span data-stu-id="ad785-198">Login and verify hello newly created user.</span></span>

```bash
ssh myVM
cat /etc/group
```

<span data-ttu-id="ad785-199">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="ad785-199">Output</span></span>

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a><span data-ttu-id="ad785-200">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ad785-200">Next Steps</span></span>
<span data-ttu-id="ad785-201">Облако init становится один стандартный способ toomodify ВМ Linux во время загрузки.</span><span class="sxs-lookup"><span data-stu-id="ad785-201">Cloud-init is becoming one standard way toomodify your Linux VM on boot.</span></span> <span data-ttu-id="ad785-202">Azure также имеет расширения ВМ, позволяющих toomodify вашей LinuxVM во время загрузки или пока она запущена.</span><span class="sxs-lookup"><span data-stu-id="ad785-202">Azure also has VM extensions, which allow you toomodify your LinuxVM on boot or while it is running.</span></span> <span data-ttu-id="ad785-203">Например можно использовать hello Azure VMAccessExtension tooreset SSH или сведения о пользователе во время выполнения hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="ad785-203">For example, you can use hello Azure VMAccessExtension tooreset SSH or user information while hello VM is running.</span></span> <span data-ttu-id="ad785-204">С инициализацией облака потребуется перезагрузка tooreset hello пароль.</span><span class="sxs-lookup"><span data-stu-id="ad785-204">With cloud-init, you would need a reboot tooreset hello password.</span></span>

[<span data-ttu-id="ad785-205">Обзор расширений и компонентов виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="ad785-205">About virtual machine extensions and features</span></span>](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="ad785-206">Управлять пользователями, SSH и проверку или восстановление дисков на виртуальных машинах Linux в Azure с помощью hello расширения VMAccess</span><span class="sxs-lookup"><span data-stu-id="ad785-206">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

