---
title: "Настройка виртуальной машины Linux с помощью cloud-init | Документация Майкрософт"
description: "Как с помощью cloud-init и Azure CLI 2.0 настроить создаваемую виртуальную машину Linux"
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
ms.openlocfilehash: a7a6daad34525683579e25b9591ed28f2bf29c04
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-cloud-init-to-customize-a-linux-vm-during-creation"></a><span data-ttu-id="e2206-103">Настройка виртуальной машины Linux во время создания с помощью cloud-init</span><span class="sxs-lookup"><span data-stu-id="e2206-103">Use cloud-init to customize a Linux VM during creation</span></span>
<span data-ttu-id="e2206-104">В этой статье демонстрируется создание сценария cloud-init для задания имени узла, обновления установленных пакетов и управления учетными записями пользователей с помощью Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="e2206-104">This article shows you how to make a cloud-init script to set the hostname, update installed packages, and manage user accounts with the Azure CLI 2.0.</span></span> <span data-ttu-id="e2206-105">Скрипты cloud-init вызываются во время создания виртуальной машины с помощью Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="e2206-105">The cloud-init scripts are called when you create a virtual machine (VM) from Azure CLI.</span></span> <span data-ttu-id="e2206-106">Дополнительные сведения по установке приложений, записи файлов конфигурации и включении ключей из хранилища Key Vault см. в [этом руководстве](tutorial-automate-vm-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="e2206-106">For a more in-depth overview on installing applications, writing configuration files, and injecting keys from Key Vault, see [this tutorial](tutorial-automate-vm-deployment.md).</span></span> <span data-ttu-id="e2206-107">Эти действия можно также выполнить с помощью [Azure CLI 1.0](using-cloud-init-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="e2206-107">You can also perform these steps with the [Azure CLI 1.0](using-cloud-init-nodejs.md).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="e2206-108">Быстрые команды</span><span class="sxs-lookup"><span data-stu-id="e2206-108">Quick commands</span></span>
<span data-ttu-id="e2206-109">Создайте сценарий cloud-init.txt, который задает имя узла, обновляет все пакеты и добавляет в Linux пользователя sudo.</span><span class="sxs-lookup"><span data-stu-id="e2206-109">Create a cloud-init.txt script that sets the hostname, updates all packages, and adds a sudo user to Linux.</span></span>

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

<span data-ttu-id="e2206-110">Создайте группу ресурсов для запуска виртуальных машин с помощью команды [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="e2206-110">Create a resource group to launch VMs into with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="e2206-111">В следующем примере создается группа ресурсов с именем *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="e2206-111">The following example creates the resource group named *myResourceGroup*:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="e2206-112">Выполните команду [az vm create](/cli/azure/vm#create) с параметром `--custom-data`, чтобы создать и настроить (при загрузке) виртуальную машину Linux с помощью cloud-init.</span><span class="sxs-lookup"><span data-stu-id="e2206-112">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot with the `--custom-data` parameter.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="e2206-113">Подробное пошаговое руководство</span><span class="sxs-lookup"><span data-stu-id="e2206-113">Detailed walkthrough</span></span>
<span data-ttu-id="e2206-114">При запуске новой виртуальной машины Linux вы получаете стандартную виртуальную машину, не настроенную под ваши потребности.</span><span class="sxs-lookup"><span data-stu-id="e2206-114">When you launch a new Linux VM, you are getting a standard Linux VM with nothing customized or ready for your needs.</span></span> <span data-ttu-id="e2206-115">[Cloud-init](https://cloudinit.readthedocs.org) — это стандартный способ добавления сценария или параметров конфигурации в виртуальную машину Linux при ее первоначальной загрузке.</span><span class="sxs-lookup"><span data-stu-id="e2206-115">[Cloud-init](https://cloudinit.readthedocs.org) is a standard way to inject a script or configuration settings into that Linux VM as it is booting up for the first time.</span></span>

<span data-ttu-id="e2206-116">В Azure есть три способа внесения изменений в виртуальную машину Linux в процессе ее развертывания или загрузки.</span><span class="sxs-lookup"><span data-stu-id="e2206-116">On Azure, there are a few different ways to make changes onto a Linux VM as it is being deployed or booted.</span></span>

* <span data-ttu-id="e2206-117">Внедрить сценарии с помощью cloud-init.</span><span class="sxs-lookup"><span data-stu-id="e2206-117">Inject scripts using cloud-init.</span></span>
* <span data-ttu-id="e2206-118">Внедрить сценарии с помощью [расширения VMAccess](using-vmaccess-extension.md)Azure.</span><span class="sxs-lookup"><span data-stu-id="e2206-118">Inject scripts using the Azure [VMAccess Extension](using-vmaccess-extension.md).</span></span>
* <span data-ttu-id="e2206-119">Шаблон Azure с использованием cloud-init.</span><span class="sxs-lookup"><span data-stu-id="e2206-119">An Azure template using cloud-init.</span></span>
* <span data-ttu-id="e2206-120">Шаблон Azure с использованием расширения [CustomScriptExtention](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="e2206-120">An Azure template using [CustomScriptExtention](extensions-customscript.md).</span></span>

<span data-ttu-id="e2206-121">Для внедрения сценариев в любой момент после загрузки можно воспользоваться одним из ниже приведенных способов.</span><span class="sxs-lookup"><span data-stu-id="e2206-121">To inject scripts at any time after boot:</span></span>

* <span data-ttu-id="e2206-122">Подключиться по SSH для выполнения команд напрямую.</span><span class="sxs-lookup"><span data-stu-id="e2206-122">SSH to run commands directly</span></span>
* <span data-ttu-id="e2206-123">Внедрить сценарии с помощью [расширения VMAccess](using-vmaccess-extension.md)Azure принудительно или через шаблон Azure.</span><span class="sxs-lookup"><span data-stu-id="e2206-123">Inject scripts using the Azure [VMAccess Extension](using-vmaccess-extension.md), either imperatively or in an Azure template</span></span>
* <span data-ttu-id="e2206-124">Воспользоваться средствами управления, такими как Ansible, Salt, Chef или Puppet.</span><span class="sxs-lookup"><span data-stu-id="e2206-124">Configuration management tools like Ansible, Salt, Chef, and Puppet.</span></span>

> [!NOTE]
> <span data-ttu-id="e2206-125">Расширение VMAccess выполняет сценарий от имени привилегированного пользователя, так же как при использовании протокола SSH.</span><span class="sxs-lookup"><span data-stu-id="e2206-125">VMAccess Extension executes a script as root in the same way using SSH can.</span></span> <span data-ttu-id="e2206-126">Однако применение расширения для виртуальных машин обеспечивает ряд предлагаемых Azure возможностей, которые могут быть полезны в некоторых сценариях.</span><span class="sxs-lookup"><span data-stu-id="e2206-126">However, using the VM extension enables several features that Azure offers that can be useful depending upon your scenario.</span></span>

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a><span data-ttu-id="e2206-127">Доступность cloud-init для псевдонимов быстрого создания образов виртуальных машин Azure:</span><span class="sxs-lookup"><span data-stu-id="e2206-127">Cloud-init availability on Azure VM quick-create image aliases:</span></span>
| <span data-ttu-id="e2206-128">Alias</span><span class="sxs-lookup"><span data-stu-id="e2206-128">Alias</span></span> | <span data-ttu-id="e2206-129">Издатель</span><span class="sxs-lookup"><span data-stu-id="e2206-129">Publisher</span></span> | <span data-ttu-id="e2206-130">ПРЕДЛОЖЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="e2206-130">Offer</span></span> | <span data-ttu-id="e2206-131">SKU</span><span class="sxs-lookup"><span data-stu-id="e2206-131">SKU</span></span> | <span data-ttu-id="e2206-132">Version (версия)</span><span class="sxs-lookup"><span data-stu-id="e2206-132">Version</span></span> | <span data-ttu-id="e2206-133">cloud-init</span><span class="sxs-lookup"><span data-stu-id="e2206-133">cloud-init</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="e2206-134">CentOS</span><span class="sxs-lookup"><span data-stu-id="e2206-134">CentOS</span></span> |<span data-ttu-id="e2206-135">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="e2206-135">OpenLogic</span></span> |<span data-ttu-id="e2206-136">CentOS</span><span class="sxs-lookup"><span data-stu-id="e2206-136">Centos</span></span> |<span data-ttu-id="e2206-137">7,2</span><span class="sxs-lookup"><span data-stu-id="e2206-137">7.2</span></span> |<span data-ttu-id="e2206-138">последних</span><span class="sxs-lookup"><span data-stu-id="e2206-138">latest</span></span> |<span data-ttu-id="e2206-139">Нет</span><span class="sxs-lookup"><span data-stu-id="e2206-139">no</span></span> |
| <span data-ttu-id="e2206-140">CoreOS</span><span class="sxs-lookup"><span data-stu-id="e2206-140">CoreOS</span></span> |<span data-ttu-id="e2206-141">CoreOS</span><span class="sxs-lookup"><span data-stu-id="e2206-141">CoreOS</span></span> |<span data-ttu-id="e2206-142">CoreOS</span><span class="sxs-lookup"><span data-stu-id="e2206-142">CoreOS</span></span> |<span data-ttu-id="e2206-143">Stable</span><span class="sxs-lookup"><span data-stu-id="e2206-143">Stable</span></span> |<span data-ttu-id="e2206-144">последних</span><span class="sxs-lookup"><span data-stu-id="e2206-144">latest</span></span> |<span data-ttu-id="e2206-145">Да</span><span class="sxs-lookup"><span data-stu-id="e2206-145">yes</span></span> |
| <span data-ttu-id="e2206-146">Debian</span><span class="sxs-lookup"><span data-stu-id="e2206-146">Debian</span></span> |<span data-ttu-id="e2206-147">credativ</span><span class="sxs-lookup"><span data-stu-id="e2206-147">credativ</span></span> |<span data-ttu-id="e2206-148">Debian</span><span class="sxs-lookup"><span data-stu-id="e2206-148">Debian</span></span> |<span data-ttu-id="e2206-149">8</span><span class="sxs-lookup"><span data-stu-id="e2206-149">8</span></span> |<span data-ttu-id="e2206-150">последних</span><span class="sxs-lookup"><span data-stu-id="e2206-150">latest</span></span> |<span data-ttu-id="e2206-151">Нет</span><span class="sxs-lookup"><span data-stu-id="e2206-151">no</span></span> |
| <span data-ttu-id="e2206-152">openSUSE</span><span class="sxs-lookup"><span data-stu-id="e2206-152">openSUSE</span></span> |<span data-ttu-id="e2206-153">SUSE</span><span class="sxs-lookup"><span data-stu-id="e2206-153">SUSE</span></span> |<span data-ttu-id="e2206-154">openSUSE</span><span class="sxs-lookup"><span data-stu-id="e2206-154">openSUSE</span></span> |<span data-ttu-id="e2206-155">13.2</span><span class="sxs-lookup"><span data-stu-id="e2206-155">13.2</span></span> |<span data-ttu-id="e2206-156">последних</span><span class="sxs-lookup"><span data-stu-id="e2206-156">latest</span></span> |<span data-ttu-id="e2206-157">Нет</span><span class="sxs-lookup"><span data-stu-id="e2206-157">no</span></span> |
| <span data-ttu-id="e2206-158">RHEL</span><span class="sxs-lookup"><span data-stu-id="e2206-158">RHEL</span></span> |<span data-ttu-id="e2206-159">Redhat</span><span class="sxs-lookup"><span data-stu-id="e2206-159">Redhat</span></span> |<span data-ttu-id="e2206-160">RHEL</span><span class="sxs-lookup"><span data-stu-id="e2206-160">RHEL</span></span> |<span data-ttu-id="e2206-161">7,2</span><span class="sxs-lookup"><span data-stu-id="e2206-161">7.2</span></span> |<span data-ttu-id="e2206-162">последних</span><span class="sxs-lookup"><span data-stu-id="e2206-162">latest</span></span> |<span data-ttu-id="e2206-163">Нет</span><span class="sxs-lookup"><span data-stu-id="e2206-163">no</span></span> |
| <span data-ttu-id="e2206-164">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="e2206-164">UbuntuLTS</span></span> |<span data-ttu-id="e2206-165">Canonical</span><span class="sxs-lookup"><span data-stu-id="e2206-165">Canonical</span></span> |<span data-ttu-id="e2206-166">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="e2206-166">UbuntuServer</span></span> |<span data-ttu-id="e2206-167">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="e2206-167">14.04.4-LTS</span></span> |<span data-ttu-id="e2206-168">последних</span><span class="sxs-lookup"><span data-stu-id="e2206-168">latest</span></span> |<span data-ttu-id="e2206-169">Да</span><span class="sxs-lookup"><span data-stu-id="e2206-169">yes</span></span> |

<span data-ttu-id="e2206-170">Мы и наши партнеры работаем над тем, чтобы сценарии cloud-init были добавлены в образы, предоставляемые для Azure.</span><span class="sxs-lookup"><span data-stu-id="e2206-170">We are working with our partners to get cloud-init included and working in the images that they provide to Azure.</span></span>

## <a name="add-a-cloud-init-script-to-the-vm-creation-with-the-azure-cli"></a><span data-ttu-id="e2206-171">Добавление сценария cloud-init в создаваемую виртуальную машину с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e2206-171">Add a cloud-init script to the VM creation with the Azure CLI</span></span>
<span data-ttu-id="e2206-172">Чтобы запустить сценарий cloud-init при создании виртуальной машины в Azure, укажите файл cloud-init с помощью параметра `--custom-data` интерфейса командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="e2206-172">To launch a cloud-init script when creating a VM in Azure, specify the cloud-init file using the Azure CLI `--custom-data` switch.</span></span>

<span data-ttu-id="e2206-173">Создайте группу ресурсов для запуска виртуальных машин с помощью команды [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="e2206-173">Create a resource group to launch VMs into with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="e2206-174">В следующем примере создается группа ресурсов с именем *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="e2206-174">The following example creates the resource group named *myResourceGroup*:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="e2206-175">Выполните команду [az vm create](/cli/azure/vm#create) для создания виртуальной машины Linux, используя cloud-init для ее настройки в процессе загрузки.</span><span class="sxs-lookup"><span data-stu-id="e2206-175">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="create-a-cloud-init-script-to-set-the-hostname-of-a-linux-vm"></a><span data-ttu-id="e2206-176">Создание сценария cloud-init для задания имени узла виртуальной машины Linux</span><span class="sxs-lookup"><span data-stu-id="e2206-176">Create a cloud-init script to set the hostname of a Linux VM</span></span>
<span data-ttu-id="e2206-177">Один из самых простых, но наиболее важных параметров для любой виртуальной машины Linux — это имя узла.</span><span class="sxs-lookup"><span data-stu-id="e2206-177">One of the simplest and most important settings for any Linux VM would be the hostname.</span></span> <span data-ttu-id="e2206-178">Его можно легко задать с помощью приведенного ниже сценария cloud-init.</span><span class="sxs-lookup"><span data-stu-id="e2206-178">We can easily set this using cloud-init with this script.</span></span>  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a><span data-ttu-id="e2206-179">Пример сценария cloud-init с именем `cloud_config_hostname.txt`</span><span class="sxs-lookup"><span data-stu-id="e2206-179">Example cloud-init script named `cloud_config_hostname.txt`.</span></span>
```yaml
#cloud-config
hostname: myservername
```

<span data-ttu-id="e2206-180">Во время первоначального запуска виртуальной машины этот скрипт cloud-init задает имя узла *myservername*.</span><span class="sxs-lookup"><span data-stu-id="e2206-180">During the initial startup of the VM, this cloud-init script sets the hostname to *myservername*.</span></span> <span data-ttu-id="e2206-181">Выполните команду [az vm create](/cli/azure/vm#create) для создания виртуальной машины Linux, используя cloud-init для ее настройки в процессе загрузки.</span><span class="sxs-lookup"><span data-stu-id="e2206-181">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

<span data-ttu-id="e2206-182">Выполните вход и проверьте имя узла новой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="e2206-182">Login and verify the hostname of the new VM.</span></span>

```bash
ssh myVM
hostname
myservername
```

## <a name="create-a-cloud-init-script"></a><span data-ttu-id="e2206-183">Создание скрипта cloud-init</span><span class="sxs-lookup"><span data-stu-id="e2206-183">Create a cloud-init script</span></span>
<span data-ttu-id="e2206-184">В целях безопасности виртуальную машину Ubuntu следует обновить при первой загрузке.</span><span class="sxs-lookup"><span data-stu-id="e2206-184">For security, you want your Ubuntu VM to update on the first boot.</span></span> <span data-ttu-id="e2206-185">Это можно сделать с помощью приведенного ниже сценария (сценарий зависит от используемого дистрибутива Linux).</span><span class="sxs-lookup"><span data-stu-id="e2206-185">Using cloud-init we can do that with the follow script, depending on the Linux distribution you are using.</span></span>

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-the-debian-family"></a><span data-ttu-id="e2206-186">Пример сценария cloud-init `cloud_config_apt_upgrade.txt` для семейства Debian</span><span class="sxs-lookup"><span data-stu-id="e2206-186">Example cloud-init script `cloud_config_apt_upgrade.txt` for the Debian Family</span></span>
```yaml
#cloud-config
apt_upgrade: true
```

<span data-ttu-id="e2206-187">После загрузки Linux все установленные пакеты обновляются с помощью команды **apt-get**.</span><span class="sxs-lookup"><span data-stu-id="e2206-187">After Linux has booted, all the installed packages are updated via **apt-get**.</span></span> <span data-ttu-id="e2206-188">Выполните команду [az vm create](/cli/azure/vm#create) для создания виртуальной машины Linux, используя cloud-init для ее настройки в процессе загрузки.</span><span class="sxs-lookup"><span data-stu-id="e2206-188">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_apt_upgrade.txt
```

<span data-ttu-id="e2206-189">Выполните вход и проверьте, обновились ли все пакеты.</span><span class="sxs-lookup"><span data-stu-id="e2206-189">Login and verify all packages are updated.</span></span>

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

## <a name="create-a-cloud-init-script-to-add-a-user-to-linux"></a><span data-ttu-id="e2206-190">Создание сценария cloud-init для добавления пользователя в Linux</span><span class="sxs-lookup"><span data-stu-id="e2206-190">Create a cloud-init script to add a user to Linux</span></span>
<span data-ttu-id="e2206-191">Одна из первых задач, которую необходимо выполнить на любой из новых виртуальных машин Linux, — добавить пользователя для себя, чтобы не использовать учетную запись *root*.</span><span class="sxs-lookup"><span data-stu-id="e2206-191">One of the first tasks on any new Linux VM is to add a user for yourself or to avoid using *root*.</span></span> <span data-ttu-id="e2206-192">Ключи SSH наиболее эффективны для обеспечения безопасности и удобства использования. Они добавляются в файл *~/.ssh/authorized_keys* с помощью этого скрипта cloud-init.</span><span class="sxs-lookup"><span data-stu-id="e2206-192">SSH keys are best practice for security and for usability and they are added to the *~/.ssh/authorized_keys* file with this cloud-init script.</span></span>

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a><span data-ttu-id="e2206-193">Пример сценария cloud-init `cloud_config_add_users.txt` для семейства Debian</span><span class="sxs-lookup"><span data-stu-id="e2206-193">Example cloud-init script `cloud_config_add_users.txt` for Debian Family</span></span>
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

<span data-ttu-id="e2206-194">После загрузки Linux все внесенные в список пользователи создаются и добавляются в группу sudo.</span><span class="sxs-lookup"><span data-stu-id="e2206-194">After Linux has booted, all the listed users are created and added to the sudo group.</span></span> <span data-ttu-id="e2206-195">Выполните команду [az vm create](/cli/azure/vm#create) для создания виртуальной машины Linux, используя cloud-init для ее настройки в процессе загрузки.</span><span class="sxs-lookup"><span data-stu-id="e2206-195">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_add_users.txt
```

<span data-ttu-id="e2206-196">Выполните вход и проверьте созданного пользователя.</span><span class="sxs-lookup"><span data-stu-id="e2206-196">Login and verify the newly created user.</span></span>

```bash
ssh myVM
cat /etc/group
```

<span data-ttu-id="e2206-197">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="e2206-197">Output</span></span>

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a><span data-ttu-id="e2206-198">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e2206-198">Next steps</span></span>
<span data-ttu-id="e2206-199">Сценарии cloud-init становятся стандартным способом изменения виртуальной машины Linux при загрузке.</span><span class="sxs-lookup"><span data-stu-id="e2206-199">Cloud-init is becoming one standard way to modify your Linux VM on boot.</span></span> <span data-ttu-id="e2206-200">Azure также поддерживает расширения виртуальных машин, которые позволяют изменить виртуальную машину Linux при загрузке или во время ее выполнения.</span><span class="sxs-lookup"><span data-stu-id="e2206-200">Azure also has VM extensions, which allow you to modify your LinuxVM on boot or while it is running.</span></span> <span data-ttu-id="e2206-201">Например, можно воспользоваться расширением VMAccessExtension, предоставляемым в Azure, для сброса данных SSH или сведений о пользователях во время выполнения виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="e2206-201">For example, you can use the Azure VMAccessExtension to reset SSH or user information while the VM is running.</span></span> <span data-ttu-id="e2206-202">При использовании cloud-init для сброса пароля требуется перезагрузка.</span><span class="sxs-lookup"><span data-stu-id="e2206-202">With cloud-init, you would need a reboot to reset the password.</span></span>

[<span data-ttu-id="e2206-203">Обзор расширений и компонентов виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="e2206-203">About virtual machine extensions and features</span></span>](extensions-features.md)

[<span data-ttu-id="e2206-204">Управление пользователями, SSH и проверка или восстановление дисков в виртуальных машинах Azure с помощью расширения VMAccess</span><span class="sxs-lookup"><span data-stu-id="e2206-204">Manage users, SSH, and check or repair disks on Azure Linux VMs using the VMAccess Extension</span></span>](using-vmaccess-extension.md)