---
title: "toocustomize aaaUse init облака виртуальной Машины Linux | Документы Microsoft"
description: "Как облачные init toocustomize toouse в виртуальной Машине Linux во время создания с hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 195c22cd-4629-4582-9ee3-9749493f1d72
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: e7297e162fc73f0da42f195bec2fcbe23b310c1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-cloud-init-toocustomize-a-linux-vm-during-creation"></a><span data-ttu-id="f834c-103">Использовать toocustomize init облака виртуальной Машины Linux во время создания</span><span class="sxs-lookup"><span data-stu-id="f834c-103">Use cloud-init toocustomize a Linux VM during creation</span></span>
<span data-ttu-id="f834c-104">В этой статье показано, как toomake tooset сценарий облака init hello имя узла, установленных пакетов обновления и управление учетными записями пользователей с hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="f834c-104">This article shows you how toomake a cloud-init script tooset hello hostname, update installed packages, and manage user accounts with hello Azure CLI 2.0.</span></span> <span data-ttu-id="f834c-105">При создании виртуальной машины (VM) из Azure CLI, называются Hello init облачных сценариев.</span><span class="sxs-lookup"><span data-stu-id="f834c-105">hello cloud-init scripts are called when you create a virtual machine (VM) from Azure CLI.</span></span> <span data-ttu-id="f834c-106">Дополнительные сведения по установке приложений, записи файлов конфигурации и включении ключей из хранилища Key Vault см. в [этом руководстве](tutorial-automate-vm-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="f834c-106">For a more in-depth overview on installing applications, writing configuration files, and injecting keys from Key Vault, see [this tutorial](tutorial-automate-vm-deployment.md).</span></span> <span data-ttu-id="f834c-107">Можно также выполнить следующие действия с hello [Azure CLI 1.0](using-cloud-init-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="f834c-107">You can also perform these steps with hello [Azure CLI 1.0](using-cloud-init-nodejs.md).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="f834c-108">Быстрые команды</span><span class="sxs-lookup"><span data-stu-id="f834c-108">Quick commands</span></span>
<span data-ttu-id="f834c-109">Создание облака init.txt скрипт, который задает имя узла hello, все пакеты обновления и добавляет tooLinux sudo пользователя.</span><span class="sxs-lookup"><span data-stu-id="f834c-109">Create a cloud-init.txt script that sets hello hostname, updates all packages, and adds a sudo user tooLinux.</span></span>

```yaml
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

<span data-ttu-id="f834c-110">Создание toolaunch группы ресурсов в виртуальные машины с [Создание группы az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="f834c-110">Create a resource group toolaunch VMs into with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="f834c-111">Hello следующем примере создается с именем группы ресурсов hello *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="f834c-111">hello following example creates hello resource group named *myResourceGroup*:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="f834c-112">Создание виртуальной Машины с Linux [создания виртуальной машины az](/cli/azure/vm#create) tooconfigure init облака с помощью его во время загрузки с hello `--custom-data` параметра.</span><span class="sxs-lookup"><span data-stu-id="f834c-112">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot with hello `--custom-data` parameter.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="f834c-113">Подробное пошаговое руководство</span><span class="sxs-lookup"><span data-stu-id="f834c-113">Detailed walkthrough</span></span>
<span data-ttu-id="f834c-114">При запуске новой виртуальной машины Linux вы получаете стандартную виртуальную машину, не настроенную под ваши потребности.</span><span class="sxs-lookup"><span data-stu-id="f834c-114">When you launch a new Linux VM, you are getting a standard Linux VM with nothing customized or ready for your needs.</span></span> <span data-ttu-id="f834c-115">[Облако init](https://cloudinit.readthedocs.org) является tooinject стандартный способ скрипт или конфигурации параметры в этой виртуальной Машины Linux при загрузке для hello первый раз.</span><span class="sxs-lookup"><span data-stu-id="f834c-115">[Cloud-init](https://cloudinit.readthedocs.org) is a standard way tooinject a script or configuration settings into that Linux VM as it is booting up for hello first time.</span></span>

<span data-ttu-id="f834c-116">В Azure, существует несколько способов изменения toomake на виртуальной Машине Linux время развернут или загружен.</span><span class="sxs-lookup"><span data-stu-id="f834c-116">On Azure, there are a few different ways toomake changes onto a Linux VM as it is being deployed or booted.</span></span>

* <span data-ttu-id="f834c-117">Внедрить сценарии с помощью cloud-init.</span><span class="sxs-lookup"><span data-stu-id="f834c-117">Inject scripts using cloud-init.</span></span>
* <span data-ttu-id="f834c-118">Внедрить скриптов с использованием hello Azure [расширения VMAccess](using-vmaccess-extension.md).</span><span class="sxs-lookup"><span data-stu-id="f834c-118">Inject scripts using hello Azure [VMAccess Extension](using-vmaccess-extension.md).</span></span>
* <span data-ttu-id="f834c-119">Шаблон Azure с использованием cloud-init.</span><span class="sxs-lookup"><span data-stu-id="f834c-119">An Azure template using cloud-init.</span></span>
* <span data-ttu-id="f834c-120">Шаблон Azure с использованием расширения [CustomScriptExtention](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="f834c-120">An Azure template using [CustomScriptExtention](extensions-customscript.md).</span></span>

<span data-ttu-id="f834c-121">сценарии tooinject в любое время после загрузки.</span><span class="sxs-lookup"><span data-stu-id="f834c-121">tooinject scripts at any time after boot:</span></span>

* <span data-ttu-id="f834c-122">Непосредственно команды toorun SSH</span><span class="sxs-lookup"><span data-stu-id="f834c-122">SSH toorun commands directly</span></span>
* <span data-ttu-id="f834c-123">Внедрить скриптов с использованием hello Azure [расширения VMAccess](using-vmaccess-extension.md), принудительно или в шаблоне Azure</span><span class="sxs-lookup"><span data-stu-id="f834c-123">Inject scripts using hello Azure [VMAccess Extension](using-vmaccess-extension.md), either imperatively or in an Azure template</span></span>
* <span data-ttu-id="f834c-124">Воспользоваться средствами управления, такими как Ansible, Salt, Chef или Puppet.</span><span class="sxs-lookup"><span data-stu-id="f834c-124">Configuration management tools like Ansible, Salt, Chef, and Puppet.</span></span>

> [!NOTE]
> <span data-ttu-id="f834c-125">Расширение VMAccess выполняет скрипт как корневой hello же можно с помощью SSH.</span><span class="sxs-lookup"><span data-stu-id="f834c-125">VMAccess Extension executes a script as root in hello same way using SSH can.</span></span> <span data-ttu-id="f834c-126">Тем не менее использование расширения ВМ hello позволяет несколько функций, Azure предлагает, которые могут быть полезны в зависимости от ситуации.</span><span class="sxs-lookup"><span data-stu-id="f834c-126">However, using hello VM extension enables several features that Azure offers that can be useful depending upon your scenario.</span></span>

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a><span data-ttu-id="f834c-127">Доступность cloud-init для псевдонимов быстрого создания образов виртуальных машин Azure:</span><span class="sxs-lookup"><span data-stu-id="f834c-127">Cloud-init availability on Azure VM quick-create image aliases:</span></span>
| <span data-ttu-id="f834c-128">Alias</span><span class="sxs-lookup"><span data-stu-id="f834c-128">Alias</span></span> | <span data-ttu-id="f834c-129">Издатель</span><span class="sxs-lookup"><span data-stu-id="f834c-129">Publisher</span></span> | <span data-ttu-id="f834c-130">ПРЕДЛОЖЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="f834c-130">Offer</span></span> | <span data-ttu-id="f834c-131">SKU</span><span class="sxs-lookup"><span data-stu-id="f834c-131">SKU</span></span> | <span data-ttu-id="f834c-132">Version (версия)</span><span class="sxs-lookup"><span data-stu-id="f834c-132">Version</span></span> | <span data-ttu-id="f834c-133">cloud-init</span><span class="sxs-lookup"><span data-stu-id="f834c-133">cloud-init</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="f834c-134">CentOS</span><span class="sxs-lookup"><span data-stu-id="f834c-134">CentOS</span></span> |<span data-ttu-id="f834c-135">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="f834c-135">OpenLogic</span></span> |<span data-ttu-id="f834c-136">CentOS</span><span class="sxs-lookup"><span data-stu-id="f834c-136">Centos</span></span> |<span data-ttu-id="f834c-137">7,2</span><span class="sxs-lookup"><span data-stu-id="f834c-137">7.2</span></span> |<span data-ttu-id="f834c-138">последних</span><span class="sxs-lookup"><span data-stu-id="f834c-138">latest</span></span> |<span data-ttu-id="f834c-139">Нет</span><span class="sxs-lookup"><span data-stu-id="f834c-139">no</span></span> |
| <span data-ttu-id="f834c-140">CoreOS</span><span class="sxs-lookup"><span data-stu-id="f834c-140">CoreOS</span></span> |<span data-ttu-id="f834c-141">CoreOS</span><span class="sxs-lookup"><span data-stu-id="f834c-141">CoreOS</span></span> |<span data-ttu-id="f834c-142">CoreOS</span><span class="sxs-lookup"><span data-stu-id="f834c-142">CoreOS</span></span> |<span data-ttu-id="f834c-143">Stable</span><span class="sxs-lookup"><span data-stu-id="f834c-143">Stable</span></span> |<span data-ttu-id="f834c-144">последних</span><span class="sxs-lookup"><span data-stu-id="f834c-144">latest</span></span> |<span data-ttu-id="f834c-145">Да</span><span class="sxs-lookup"><span data-stu-id="f834c-145">yes</span></span> |
| <span data-ttu-id="f834c-146">Debian</span><span class="sxs-lookup"><span data-stu-id="f834c-146">Debian</span></span> |<span data-ttu-id="f834c-147">credativ</span><span class="sxs-lookup"><span data-stu-id="f834c-147">credativ</span></span> |<span data-ttu-id="f834c-148">Debian</span><span class="sxs-lookup"><span data-stu-id="f834c-148">Debian</span></span> |<span data-ttu-id="f834c-149">8</span><span class="sxs-lookup"><span data-stu-id="f834c-149">8</span></span> |<span data-ttu-id="f834c-150">последних</span><span class="sxs-lookup"><span data-stu-id="f834c-150">latest</span></span> |<span data-ttu-id="f834c-151">Нет</span><span class="sxs-lookup"><span data-stu-id="f834c-151">no</span></span> |
| <span data-ttu-id="f834c-152">openSUSE</span><span class="sxs-lookup"><span data-stu-id="f834c-152">openSUSE</span></span> |<span data-ttu-id="f834c-153">SUSE</span><span class="sxs-lookup"><span data-stu-id="f834c-153">SUSE</span></span> |<span data-ttu-id="f834c-154">openSUSE</span><span class="sxs-lookup"><span data-stu-id="f834c-154">openSUSE</span></span> |<span data-ttu-id="f834c-155">13.2</span><span class="sxs-lookup"><span data-stu-id="f834c-155">13.2</span></span> |<span data-ttu-id="f834c-156">последних</span><span class="sxs-lookup"><span data-stu-id="f834c-156">latest</span></span> |<span data-ttu-id="f834c-157">Нет</span><span class="sxs-lookup"><span data-stu-id="f834c-157">no</span></span> |
| <span data-ttu-id="f834c-158">RHEL</span><span class="sxs-lookup"><span data-stu-id="f834c-158">RHEL</span></span> |<span data-ttu-id="f834c-159">Redhat</span><span class="sxs-lookup"><span data-stu-id="f834c-159">Redhat</span></span> |<span data-ttu-id="f834c-160">RHEL</span><span class="sxs-lookup"><span data-stu-id="f834c-160">RHEL</span></span> |<span data-ttu-id="f834c-161">7,2</span><span class="sxs-lookup"><span data-stu-id="f834c-161">7.2</span></span> |<span data-ttu-id="f834c-162">последних</span><span class="sxs-lookup"><span data-stu-id="f834c-162">latest</span></span> |<span data-ttu-id="f834c-163">Нет</span><span class="sxs-lookup"><span data-stu-id="f834c-163">no</span></span> |
| <span data-ttu-id="f834c-164">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="f834c-164">UbuntuLTS</span></span> |<span data-ttu-id="f834c-165">Canonical</span><span class="sxs-lookup"><span data-stu-id="f834c-165">Canonical</span></span> |<span data-ttu-id="f834c-166">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="f834c-166">UbuntuServer</span></span> |<span data-ttu-id="f834c-167">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="f834c-167">14.04.4-LTS</span></span> |<span data-ttu-id="f834c-168">последних</span><span class="sxs-lookup"><span data-stu-id="f834c-168">latest</span></span> |<span data-ttu-id="f834c-169">Да</span><span class="sxs-lookup"><span data-stu-id="f834c-169">yes</span></span> |

<span data-ttu-id="f834c-170">Можно работать с наших партнеров tooget облака init включены и работу в том, что они предоставляют tooAzure образы hello.</span><span class="sxs-lookup"><span data-stu-id="f834c-170">We are working with our partners tooget cloud-init included and working in hello images that they provide tooAzure.</span></span>

## <a name="add-a-cloud-init-script-toohello-vm-creation-with-hello-azure-cli"></a><span data-ttu-id="f834c-171">Добавить создания облака init скрипта toohello ВМ с hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f834c-171">Add a cloud-init script toohello VM creation with hello Azure CLI</span></span>
<span data-ttu-id="f834c-172">toolaunch сценарий init облака при создании виртуальной Машины в Azure, укажите файл init облака hello, с помощью hello Azure CLI `--custom-data` переключения.</span><span class="sxs-lookup"><span data-stu-id="f834c-172">toolaunch a cloud-init script when creating a VM in Azure, specify hello cloud-init file using hello Azure CLI `--custom-data` switch.</span></span>

<span data-ttu-id="f834c-173">Создание toolaunch группы ресурсов в виртуальные машины с [Создание группы az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="f834c-173">Create a resource group toolaunch VMs into with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="f834c-174">Hello следующем примере создается с именем группы ресурсов hello *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="f834c-174">hello following example creates hello resource group named *myResourceGroup*:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="f834c-175">Создание виртуальной Машины с Linux [создания виртуальной машины az](/cli/azure/vm#create) tooconfigure init облака с помощью его во время загрузки.</span><span class="sxs-lookup"><span data-stu-id="f834c-175">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="create-a-cloud-init-script-tooset-hello-hostname-of-a-linux-vm"></a><span data-ttu-id="f834c-176">Создание облака init сценария tooset hello имени узла виртуальной машины Linux</span><span class="sxs-lookup"><span data-stu-id="f834c-176">Create a cloud-init script tooset hello hostname of a Linux VM</span></span>
<span data-ttu-id="f834c-177">Одним из hello простейшим и наиболее важные параметры для виртуальной Машины с Linux будет hello имя узла.</span><span class="sxs-lookup"><span data-stu-id="f834c-177">One of hello simplest and most important settings for any Linux VM would be hello hostname.</span></span> <span data-ttu-id="f834c-178">Его можно легко задать с помощью приведенного ниже сценария cloud-init.</span><span class="sxs-lookup"><span data-stu-id="f834c-178">We can easily set this using cloud-init with this script.</span></span>  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a><span data-ttu-id="f834c-179">Пример сценария cloud-init с именем `cloud_config_hostname.txt`</span><span class="sxs-lookup"><span data-stu-id="f834c-179">Example cloud-init script named `cloud_config_hostname.txt`.</span></span>
```yaml
#cloud-config
hostname: myservername
```

<span data-ttu-id="f834c-180">Во время запуска начальной hello hello виртуальной Машины, этот сценарий облака init задает hello hostname, слишком*myservername*.</span><span class="sxs-lookup"><span data-stu-id="f834c-180">During hello initial startup of hello VM, this cloud-init script sets hello hostname too*myservername*.</span></span> <span data-ttu-id="f834c-181">Создание виртуальной Машины с Linux [создания виртуальной машины az](/cli/azure/vm#create) tooconfigure init облака с помощью его во время загрузки.</span><span class="sxs-lookup"><span data-stu-id="f834c-181">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

<span data-ttu-id="f834c-182">Имя входа и проверьте имя узла hello hello новой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="f834c-182">Login and verify hello hostname of hello new VM.</span></span>

```bash
ssh myVM
hostname
myservername
```

## <a name="create-a-cloud-init-script"></a><span data-ttu-id="f834c-183">Создание скрипта cloud-init</span><span class="sxs-lookup"><span data-stu-id="f834c-183">Create a cloud-init script</span></span>
<span data-ttu-id="f834c-184">В целях безопасности необходимо tooupdate вашей виртуальной Машине Ubuntu при первой загрузке hello.</span><span class="sxs-lookup"><span data-stu-id="f834c-184">For security, you want your Ubuntu VM tooupdate on hello first boot.</span></span> <span data-ttu-id="f834c-185">С помощью init облака можно сделать с hello выполните скрипт, в зависимости от hello дистрибутив Linux, которые вы используете.</span><span class="sxs-lookup"><span data-stu-id="f834c-185">Using cloud-init we can do that with hello follow script, depending on hello Linux distribution you are using.</span></span>

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-hello-debian-family"></a><span data-ttu-id="f834c-186">Пример сценария в облаке init `cloud_config_apt_upgrade.txt` для hello Debian семейства</span><span class="sxs-lookup"><span data-stu-id="f834c-186">Example cloud-init script `cloud_config_apt_upgrade.txt` for hello Debian Family</span></span>
```yaml
#cloud-config
apt_upgrade: true
```

<span data-ttu-id="f834c-187">После загрузки операционной системы Linux, все пакеты установки hello обновляются через **apt get**.</span><span class="sxs-lookup"><span data-stu-id="f834c-187">After Linux has booted, all hello installed packages are updated via **apt-get**.</span></span> <span data-ttu-id="f834c-188">Создание виртуальной Машины с Linux [создания виртуальной машины az](/cli/azure/vm#create) tooconfigure init облака с помощью его во время загрузки.</span><span class="sxs-lookup"><span data-stu-id="f834c-188">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_apt_upgrade.txt
```

<span data-ttu-id="f834c-189">Выполните вход и проверьте, обновились ли все пакеты.</span><span class="sxs-lookup"><span data-stu-id="f834c-189">Login and verify all packages are updated.</span></span>

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

## <a name="create-a-cloud-init-script-tooadd-a-user-toolinux"></a><span data-ttu-id="f834c-190">Создание tooadd сценария облака init tooLinux пользователя</span><span class="sxs-lookup"><span data-stu-id="f834c-190">Create a cloud-init script tooadd a user tooLinux</span></span>
<span data-ttu-id="f834c-191">Один из первых задач hello на все новые виртуальные Машины Linux — tooadd пользователя для себя, или с помощью tooavoid *корневой*.</span><span class="sxs-lookup"><span data-stu-id="f834c-191">One of hello first tasks on any new Linux VM is tooadd a user for yourself or tooavoid using *root*.</span></span> <span data-ttu-id="f834c-192">SSH ключи — это рекомендуется для безопасности и удобство использования и они добавляются toohello *~/.ssh/authorized_keys* файла с помощью этого сценария init облака.</span><span class="sxs-lookup"><span data-stu-id="f834c-192">SSH keys are best practice for security and for usability and they are added toohello *~/.ssh/authorized_keys* file with this cloud-init script.</span></span>

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a><span data-ttu-id="f834c-193">Пример сценария cloud-init `cloud_config_add_users.txt` для семейства Debian</span><span class="sxs-lookup"><span data-stu-id="f834c-193">Example cloud-init script `cloud_config_add_users.txt` for Debian Family</span></span>
```yaml
#cloud-config
users:
  - name: myCloudInitAddedAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myUbuntuVM
```

<span data-ttu-id="f834c-194">После загрузки операционной системы Linux, все пользователи в списке hello являются группа создана и добавлена toohello sudo.</span><span class="sxs-lookup"><span data-stu-id="f834c-194">After Linux has booted, all hello listed users are created and added toohello sudo group.</span></span> <span data-ttu-id="f834c-195">Создание виртуальной Машины с Linux [создания виртуальной машины az](/cli/azure/vm#create) tooconfigure init облака с помощью его во время загрузки.</span><span class="sxs-lookup"><span data-stu-id="f834c-195">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_add_users.txt
```

<span data-ttu-id="f834c-196">Имя входа и проверки hello только что созданный пользователь.</span><span class="sxs-lookup"><span data-stu-id="f834c-196">Login and verify hello newly created user.</span></span>

```bash
ssh myVM
cat /etc/group
```

<span data-ttu-id="f834c-197">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="f834c-197">Output</span></span>

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a><span data-ttu-id="f834c-198">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f834c-198">Next steps</span></span>
<span data-ttu-id="f834c-199">Облако init становится один стандартный способ toomodify ВМ Linux во время загрузки.</span><span class="sxs-lookup"><span data-stu-id="f834c-199">Cloud-init is becoming one standard way toomodify your Linux VM on boot.</span></span> <span data-ttu-id="f834c-200">Azure также имеет расширения ВМ, позволяющих toomodify вашей LinuxVM во время загрузки или пока она запущена.</span><span class="sxs-lookup"><span data-stu-id="f834c-200">Azure also has VM extensions, which allow you toomodify your LinuxVM on boot or while it is running.</span></span> <span data-ttu-id="f834c-201">Например можно использовать hello Azure VMAccessExtension tooreset SSH или сведения о пользователе во время выполнения hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="f834c-201">For example, you can use hello Azure VMAccessExtension tooreset SSH or user information while hello VM is running.</span></span> <span data-ttu-id="f834c-202">С инициализацией облака потребуется перезагрузка tooreset hello пароль.</span><span class="sxs-lookup"><span data-stu-id="f834c-202">With cloud-init, you would need a reboot tooreset hello password.</span></span>

[<span data-ttu-id="f834c-203">Обзор расширений и компонентов виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="f834c-203">About virtual machine extensions and features</span></span>](extensions-features.md)

[<span data-ttu-id="f834c-204">Управлять пользователями, SSH и проверку или восстановление дисков на виртуальных машинах Linux в Azure с помощью hello расширения VMAccess</span><span class="sxs-lookup"><span data-stu-id="f834c-204">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension</span></span>](using-vmaccess-extension.md)
