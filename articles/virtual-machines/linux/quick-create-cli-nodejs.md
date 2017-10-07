---
title: "Создание виртуальной машины Linux с помощью Azure CLI 1.0 | Документация Майкрософт"
description: "Создание виртуальной машины Linux в Azure с помощью Azure CLI 1.0"
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
ms.assetid: facb1115-2b4e-4ef3-9905-330e42beb686
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: 
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/15/2016
ms.author: v-livech
ms.openlocfilehash: ec1b34e4f539d2e95bb1f99fca3a6a0ec682ef51
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-linux-vm-using-the-azure-cli-10"></a><span data-ttu-id="31cb9-103">Создание виртуальной машины Linux с помощью Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="31cb9-103">Create a Linux VM using the Azure CLI 1.0</span></span>

<span data-ttu-id="31cb9-104">В этой статье мы расскажем, как быстро развернуть в Azure виртуальную машину Linux с помощью команды `azure vm quick-create` в интерфейсе командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="31cb9-104">This article shows how to quickly deploy a Linux virtual machine (VM) on Azure by using the `azure vm quick-create` command in the Azure command-line interface (CLI).</span></span> <span data-ttu-id="31cb9-105">Команда `quick-create` развертывает виртуальную машину в надежной базовой инфраструктуре, которую вы можете использовать для быстрой проверки или создания прототипа решения.</span><span class="sxs-lookup"><span data-stu-id="31cb9-105">The `quick-create` command deploys a VM inside a basic, secure infrastructure that you can use to prototype or test a concept rapidly.</span></span>

> [!NOTE]
<span data-ttu-id="31cb9-106">Чтобы создать виртуальную машину с использованием Azure CLI 2.0, изучите раздел [Создание виртуальной машины с помощью Azure CLI](../windows/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="31cb9-106">To create a VM using the Azure CLI 2.0, see [Create a VM with the Azure CLI](../windows/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="31cb9-107">Вы также можете быстро развернуть виртуальную машину Linux с помощью [портала Azure](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="31cb9-107">You can also quickly deploy a Linux VM by using the [Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="31cb9-108">В этой статье требуется использовать [файлы открытого и закрытого ключей SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="31cb9-108">The article requires an [SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="quick-commands"></a><span data-ttu-id="31cb9-109">Быстрые команды</span><span class="sxs-lookup"><span data-stu-id="31cb9-109">Quick commands</span></span>

<span data-ttu-id="31cb9-110">На примере ниже показано, как развернуть виртуальную машину CoreOS и подключить к ней ключ SSH (ваши значения аргументов могут отличаться).</span><span class="sxs-lookup"><span data-stu-id="31cb9-110">The following example shows how to deploy a CoreOS VM and attach your Secure Shell (SSH) key (your arguments might be different):</span></span>

```azurecli
azure vm quick-create -M ~/.ssh/id_rsa.pub -Q CoreOS
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="31cb9-111">Подробное пошаговое руководство</span><span class="sxs-lookup"><span data-stu-id="31cb9-111">Detailed walkthrough</span></span>

<span data-ttu-id="31cb9-112">Следующее руководство содержит инструкции по развертыванию ВМ UbuntuLTS с подробным описанием каждого шага.</span><span class="sxs-lookup"><span data-stu-id="31cb9-112">The following walkthrough has an UbuntuLTS VM being deployed, step by step, with explanations of what each step is doing.</span></span>

## <a name="vm-quick-create-aliases"></a><span data-ttu-id="31cb9-113">Использование псевдонимов команды quick-create</span><span class="sxs-lookup"><span data-stu-id="31cb9-113">VM quick-create aliases</span></span>

<span data-ttu-id="31cb9-114">Чтобы быстро выбрать дистрибутив, можно воспользоваться псевдонимами интерфейса командной строки Azure для большинства распространенных дистрибутивов ОС.</span><span class="sxs-lookup"><span data-stu-id="31cb9-114">A quick way to choose a distribution is to use the Azure CLI aliases mapped to the most common OS distributions.</span></span> <span data-ttu-id="31cb9-115">В следующей таблице перечислены псевдонимы (для интерфейса командной строки Azure версии 0.10).</span><span class="sxs-lookup"><span data-stu-id="31cb9-115">The following table lists the aliases (as of Azure CLI version 0.10).</span></span> <span data-ttu-id="31cb9-116">Все развертывания с использованием команды `quick-create` по умолчанию устанавливают резервные виртуальные машины с поддержкой хранилища на основе твердотельных накопителей (SSD), что обеспечивает более быструю подготовку к работе и доступ к диску с высокой производительностью.</span><span class="sxs-lookup"><span data-stu-id="31cb9-116">All deployments that use `quick-create` default to VMs that are backed by solid-state drive (SSD) storage, which offers faster provisioning and high-performance disk access.</span></span> <span data-ttu-id="31cb9-117">(Эти псевдонимы представляют лишь небольшую часть дистрибутивов, доступных в Azure.</span><span class="sxs-lookup"><span data-stu-id="31cb9-117">(These aliases represent a tiny portion of the available distributions on Azure.</span></span> <span data-ttu-id="31cb9-118">Чтобы найти другие образы в Azure Marketplace, выполните поиск в [PowerShell](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [Интернете](https://azure.microsoft.com/marketplace/virtual-machines/) или [загрузите собственный пользовательский образ](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).)</span><span class="sxs-lookup"><span data-stu-id="31cb9-118">Find more images in the Azure Marketplace by [searching for an image in PowerShell](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [on the web](https://azure.microsoft.com/marketplace/virtual-machines/), or [upload your own custom image](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).)</span></span>

| <span data-ttu-id="31cb9-119">Alias</span><span class="sxs-lookup"><span data-stu-id="31cb9-119">Alias</span></span> | <span data-ttu-id="31cb9-120">Издатель</span><span class="sxs-lookup"><span data-stu-id="31cb9-120">Publisher</span></span> | <span data-ttu-id="31cb9-121">ПРЕДЛОЖЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="31cb9-121">Offer</span></span> | <span data-ttu-id="31cb9-122">SKU</span><span class="sxs-lookup"><span data-stu-id="31cb9-122">SKU</span></span> | <span data-ttu-id="31cb9-123">Версия</span><span class="sxs-lookup"><span data-stu-id="31cb9-123">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="31cb9-124">CentOS</span><span class="sxs-lookup"><span data-stu-id="31cb9-124">CentOS</span></span> |<span data-ttu-id="31cb9-125">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="31cb9-125">OpenLogic</span></span> |<span data-ttu-id="31cb9-126">CentOS</span><span class="sxs-lookup"><span data-stu-id="31cb9-126">CentOS</span></span> |<span data-ttu-id="31cb9-127">7,2</span><span class="sxs-lookup"><span data-stu-id="31cb9-127">7.2</span></span> |<span data-ttu-id="31cb9-128">последних</span><span class="sxs-lookup"><span data-stu-id="31cb9-128">latest</span></span> |
| <span data-ttu-id="31cb9-129">CoreOS</span><span class="sxs-lookup"><span data-stu-id="31cb9-129">CoreOS</span></span> |<span data-ttu-id="31cb9-130">CoreOS</span><span class="sxs-lookup"><span data-stu-id="31cb9-130">CoreOS</span></span> |<span data-ttu-id="31cb9-131">CoreOS</span><span class="sxs-lookup"><span data-stu-id="31cb9-131">CoreOS</span></span> |<span data-ttu-id="31cb9-132">Stable</span><span class="sxs-lookup"><span data-stu-id="31cb9-132">Stable</span></span> |<span data-ttu-id="31cb9-133">последняя</span><span class="sxs-lookup"><span data-stu-id="31cb9-133">latest</span></span> |
| <span data-ttu-id="31cb9-134">Debian</span><span class="sxs-lookup"><span data-stu-id="31cb9-134">Debian</span></span> |<span data-ttu-id="31cb9-135">credativ</span><span class="sxs-lookup"><span data-stu-id="31cb9-135">credativ</span></span> |<span data-ttu-id="31cb9-136">Debian</span><span class="sxs-lookup"><span data-stu-id="31cb9-136">Debian</span></span> |<span data-ttu-id="31cb9-137">8</span><span class="sxs-lookup"><span data-stu-id="31cb9-137">8</span></span> |<span data-ttu-id="31cb9-138">последняя</span><span class="sxs-lookup"><span data-stu-id="31cb9-138">latest</span></span> |
| <span data-ttu-id="31cb9-139">openSUSE</span><span class="sxs-lookup"><span data-stu-id="31cb9-139">openSUSE</span></span> |<span data-ttu-id="31cb9-140">SUSE</span><span class="sxs-lookup"><span data-stu-id="31cb9-140">SUSE</span></span> |<span data-ttu-id="31cb9-141">openSUSE</span><span class="sxs-lookup"><span data-stu-id="31cb9-141">openSUSE</span></span> |<span data-ttu-id="31cb9-142">13.2</span><span class="sxs-lookup"><span data-stu-id="31cb9-142">13.2</span></span> |<span data-ttu-id="31cb9-143">последних</span><span class="sxs-lookup"><span data-stu-id="31cb9-143">latest</span></span> |
| <span data-ttu-id="31cb9-144">RHEL</span><span class="sxs-lookup"><span data-stu-id="31cb9-144">RHEL</span></span> |<span data-ttu-id="31cb9-145">Red Hat</span><span class="sxs-lookup"><span data-stu-id="31cb9-145">Red Hat</span></span> |<span data-ttu-id="31cb9-146">RHEL</span><span class="sxs-lookup"><span data-stu-id="31cb9-146">RHEL</span></span> |<span data-ttu-id="31cb9-147">7,2</span><span class="sxs-lookup"><span data-stu-id="31cb9-147">7.2</span></span> |<span data-ttu-id="31cb9-148">последних</span><span class="sxs-lookup"><span data-stu-id="31cb9-148">latest</span></span> |
| <span data-ttu-id="31cb9-149">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="31cb9-149">UbuntuLTS</span></span> |<span data-ttu-id="31cb9-150">Canonical</span><span class="sxs-lookup"><span data-stu-id="31cb9-150">Canonical</span></span> |<span data-ttu-id="31cb9-151">Сервер Ubuntu</span><span class="sxs-lookup"><span data-stu-id="31cb9-151">Ubuntu Server</span></span> |<span data-ttu-id="31cb9-152">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="31cb9-152">14.04.4-LTS</span></span> |<span data-ttu-id="31cb9-153">последних</span><span class="sxs-lookup"><span data-stu-id="31cb9-153">latest</span></span> |

<span data-ttu-id="31cb9-154">В следующих разделах для параметра **ImageURN** (`-Q`) используется псевдоним `UbuntuLTS`, чтобы развернуть виртуальную машину на базе сервера Ubuntu 14.04.4 LTS.</span><span class="sxs-lookup"><span data-stu-id="31cb9-154">The following sections use the `UbuntuLTS` alias for the **ImageURN** option (`-Q`) to deploy an Ubuntu 14.04.4 LTS Server.</span></span>

<span data-ttu-id="31cb9-155">В предыдущем примере команда `quick-create` вызывала только флаг `-M`, чтобы идентифицировать открытый ключ SSH для его передачи при отключении паролей SSH. Теперь необходимо ввести следующие аргументы:</span><span class="sxs-lookup"><span data-stu-id="31cb9-155">The previous `quick-create` example only called out the `-M` flag to identify the SSH public key to upload while disabling SSH passwords, so you are prompted for the following arguments:</span></span>

* <span data-ttu-id="31cb9-156">имя группы ресурсов (для своей первой группы ресурсов в Azure вы можете выбрать любое имя);</span><span class="sxs-lookup"><span data-stu-id="31cb9-156">resource group name (any string is typically fine for your first Azure resource group)</span></span>
* <span data-ttu-id="31cb9-157">имя виртуальной машины;</span><span class="sxs-lookup"><span data-stu-id="31cb9-157">VM name</span></span>
* <span data-ttu-id="31cb9-158">расположение (по умолчанию можно использовать `westus` или `westeurope`);</span><span class="sxs-lookup"><span data-stu-id="31cb9-158">location (`westus` or `westeurope` are good defaults)</span></span>
* <span data-ttu-id="31cb9-159">Linux (для Azure необходимо указать ОС, которую вы предпочитаете использовать);</span><span class="sxs-lookup"><span data-stu-id="31cb9-159">linux (to let Azure know which OS you want)</span></span>
* <span data-ttu-id="31cb9-160">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="31cb9-160">username</span></span>

<span data-ttu-id="31cb9-161">В приведенном ниже примере указаны все необходимые значения.</span><span class="sxs-lookup"><span data-stu-id="31cb9-161">The following example specifies all the values so that no further prompting is required.</span></span> <span data-ttu-id="31cb9-162">Так как в качестве файла открытого ключа формата SSH-RSA используется `~/.ssh/id_rsa.pub`, этот файл работает как есть.</span><span class="sxs-lookup"><span data-stu-id="31cb9-162">So long as you have an `~/.ssh/id_rsa.pub` as a ssh-rsa format public key file, it works as is:</span></span>

```azurecli
azure vm quick-create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --admin-username myAdminUser \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --image-urn UbuntuLTS
```

<span data-ttu-id="31cb9-163">В результате должен отобразиться следующий блок выходных данных.</span><span class="sxs-lookup"><span data-stu-id="31cb9-163">The output should look like the following output block:</span></span>

```azurecli
info:    Executing command vm quick-create
+ Listing virtual machine sizes available in the location "westus"
+ Looking up the VM "myVM"
info:    Verifying the public key SSH file: /Users/ahmet/.ssh/id_rsa.pub
info:    Using the VM Size "Standard_DS1"
info:    The [OS, Data] Disk or image configuration requires storage account
+ Looking up the storage account cli16330708391032639673
+ Looking up the NIC "examp-westu-1633070839-nic"
info:    An nic with given name "examp-westu-1633070839-nic" not found, creating a new one
+ Looking up the virtual network "examp-westu-1633070839-vnet"
info:    Preparing to create new virtual network and subnet
/ Creating a new virtual network "examp-westu-1633070839-vnet" [address prefix: "10.0.0.0/16"] with subnet "examp-westu-1633070839-snet" [address prefix: "10.+.1.0/24"]
+ Looking up the virtual network "examp-westu-1633070839-vnet"
+ Looking up the subnet "examp-westu-1633070839-snet" under the virtual network "examp-westu-1633070839-vnet"
info:    Found public ip parameters, trying to setup PublicIP profile
+ Looking up the public ip "examp-westu-1633070839-pip"
info:    PublicIP with given name "examp-westu-1633070839-pip" not found, creating a new one
+ Creating public ip "examp-westu-1633070839-pip"
+ Looking up the public ip "examp-westu-1633070839-pip"
+ Creating NIC "examp-westu-1633070839-nic"
+ Looking up the NIC "examp-westu-1633070839-nic"
+ Looking up the storage account clisto1710997031examplev
+ Creating VM "myVM"
+ Looking up the VM "myVM"
+ Looking up the NIC "examp-westu-1633070839-nic"
+ Looking up the public ip "examp-westu-1633070839-pip"
data:    Id                              :/subscriptions/2<--snip-->d/resourceGroups/exampleResourceGroup/providers/Microsoft.Compute/virtualMachines/exampleVMName
data:    ProvisioningState               :Succeeded
data:    Name                            :exampleVMName
data:    Location                        :westus
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_DS1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :Canonical
data:        Offer                       :UbuntuServer
data:        Sku                         :14.04.4-LTS
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :clic7fadb847357e9cf-os-1473374894359
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://cli16330708391032639673.blob.core.windows.net/vhds/clic7fadb847357e9cf-os-1473374894359.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM
data:      User Name                     :myAdminUser
data:      Linux Configuration:
data:        Disable Password Auth       :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-33-42-FB
data:          Provisioning State        :Succeeded
data:          Name                      :examp-westu-1633070839-nic
data:          Location                  :westus
data:            Public IP address       :138.91.247.29
data:            FQDN                    :examp-westu-1633070839-pip.westus.cloudapp.azure.com
data:
data:    Diagnostics Profile:
data:      BootDiagnostics Enabled       :true
data:      BootDiagnostics StorageUri    :https://clisto1710997031examplev.blob.core.windows.net/
data:
data:      Diagnostics Instance View:
info:    vm quick-create command OK
```

## <a name="log-in-to-the-new-vm"></a><span data-ttu-id="31cb9-164">Вход на новую ВМ</span><span class="sxs-lookup"><span data-stu-id="31cb9-164">Log in to the new VM</span></span>
<span data-ttu-id="31cb9-165">Войдите на виртуальную машину, используя общедоступный IP-адрес, указанный в выходных данных команды.</span><span class="sxs-lookup"><span data-stu-id="31cb9-165">Log in to your VM by using the public IP address listed in the output.</span></span> <span data-ttu-id="31cb9-166">Для этого также можно использовать указанное полное доменное имя.</span><span class="sxs-lookup"><span data-stu-id="31cb9-166">You can also use the fully qualified domain name (FQDN) that's listed:</span></span>

```bash
ssh -i ~/.ssh/id_rsa.pub ahmet@138.91.247.29
```

<span data-ttu-id="31cb9-167">Процесс входа в систему должен выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="31cb9-167">The login process should look something like the following output block:</span></span>

```bash
Warning: Permanently added '138.91.247.29' (ECDSA) to the list of known hosts.
Welcome to Ubuntu 14.04.4 LTS (GNU/Linux 3.19.0-65-generic x86_64)

 * Documentation:  https://help.ubuntu.com/

  System information as of Thu Sep  8 22:50:57 UTC 2016

  System load: 0.63              Memory usage: 2%   Processes:       81
  Usage of /:  39.6% of 1.94GB   Swap usage:   0%   Users logged in: 0

  Graph this data and manage this system at:
    https://landscape.canonical.com/

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.



The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

myAdminUser@myVM:~$
```

## <a name="next-steps"></a><span data-ttu-id="31cb9-168">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="31cb9-168">Next steps</span></span>
<span data-ttu-id="31cb9-169">С помощью команды `azure vm quick-create` можно быстро развернуть виртуальную машину, чтобы войти в оболочку Bash и начать работу.</span><span class="sxs-lookup"><span data-stu-id="31cb9-169">The `azure vm quick-create` command is the way to quickly deploy a VM so you can log in to a bash shell and get working.</span></span> <span data-ttu-id="31cb9-170">Однако использование `vm quick-create` не дает возможностей всестороннего контроля или создания более сложной среды.</span><span class="sxs-lookup"><span data-stu-id="31cb9-170">However, using `vm quick-create` does not give you extensive control nor does it enable you to create a more complex environment.</span></span>  <span data-ttu-id="31cb9-171">Чтобы развернуть виртуальную машину Linux, настроенную для вашей инфраструктуры, выполните инструкции, приведенные в любой из следующих статей:</span><span class="sxs-lookup"><span data-stu-id="31cb9-171">To deploy a Linux VM that's customized for your infrastructure, you can follow any of these articles:</span></span>

* [<span data-ttu-id="31cb9-172">Создание полной среды Linux с помощью интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="31cb9-172">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="31cb9-173">Создание виртуальной машины Linux с помощью шаблона Azure</span><span class="sxs-lookup"><span data-stu-id="31cb9-173">Create an SSH Secured Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

<span data-ttu-id="31cb9-174">Вы также можете [использовать драйвер Azure `docker-machine` с разными командами для быстрого создания виртуальной машины Linux в качестве узла Docker](docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="31cb9-174">You can also [use the `docker-machine` Azure driver with various commands to quickly create a Linux VM as a docker host](docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
