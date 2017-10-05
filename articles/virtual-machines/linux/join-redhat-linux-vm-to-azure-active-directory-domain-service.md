---
title: "Присоединение виртуальной машины RedHat Linux к доменным службам Azure Active Directory | Документация Майкрософт"
description: "Как присоединить существующую виртуальную машину RedHat Enterprise Linux 7 к доменным службам Azure Active Directory."
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/14/2016
ms.author: v-livech
ms.openlocfilehash: 2e46a0f3c9bdbe267d121b4bf62e25d5d411fcc2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="join-a-redhat-linux-vm-to-an-azure-active-directory-domain-service"></a><span data-ttu-id="1f9ae-103">Присоединение виртуальной машины RedHat Linux к доменным службам Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1f9ae-103">Join a RedHat Linux VM to an Azure Active Directory Domain Service</span></span>

<span data-ttu-id="1f9ae-104">В этой статье показано, как присоединить виртуальную машину RedHat Enterprise Linux (RHEL) 7 к управляемому домену доменных служб Azure Active Directory (AADDS).</span><span class="sxs-lookup"><span data-stu-id="1f9ae-104">This article shows you how to join a Red Hat Enterprise Linux (RHEL) 7 virtual machine to an Azure Active Directory Domain Services (AADDS) managed domain.</span></span>  <span data-ttu-id="1f9ae-105">Для этого необходимы следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="1f9ae-105">The requirements are:</span></span>

- <span data-ttu-id="1f9ae-106">[учетная запись Azure](https://azure.microsoft.com/pricing/free-trial/);</span><span class="sxs-lookup"><span data-stu-id="1f9ae-106">[an Azure account](https://azure.microsoft.com/pricing/free-trial/)</span></span>

- <span data-ttu-id="1f9ae-107">[файлы открытого и закрытого ключа SSH](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="1f9ae-107">[SSH public and private key files](mac-create-ssh-keys.md)</span></span>

- <span data-ttu-id="1f9ae-108">[доменные службы Azure Active Directory](../../active-directory-domain-services/active-directory-ds-getting-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1f9ae-108">[an Azure Active Directory Domain Services DC](../../active-directory-domain-services/active-directory-ds-getting-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="quick-commands"></a><span data-ttu-id="1f9ae-109">Быстрые команды</span><span class="sxs-lookup"><span data-stu-id="1f9ae-109">Quick Commands</span></span>

<span data-ttu-id="1f9ae-110">_Замените все примеры параметров своими значениями_.</span><span class="sxs-lookup"><span data-stu-id="1f9ae-110">_Replace any examples with your own settings._</span></span>

### <a name="switch-the-azure-cli-to-classic-deployment-mode"></a><span data-ttu-id="1f9ae-111">Переключение Azure CLI в режим классического развертывания</span><span class="sxs-lookup"><span data-stu-id="1f9ae-111">Switch the azure-cli to classic deployment mode</span></span>

```azurecli
azure config mode asm
```

### <a name="search-for-a-rhel-version-and-image"></a><span data-ttu-id="1f9ae-112">Поиск версии и образа RHEL</span><span class="sxs-lookup"><span data-stu-id="1f9ae-112">Search for a RHEL version and image</span></span>

```azurecli
azure vm image list | grep "Red Hat"
```

### <a name="create-a-redhat-linux-vm"></a><span data-ttu-id="1f9ae-113">Создание виртуальной машины Red Hat Linux</span><span class="sxs-lookup"><span data-stu-id="1f9ae-113">Create a Redhat Linux VM</span></span>

```azurecli
azure vm create myVM \
-o a879bbefc56a43abb0ce65052aac09f3__RHEL_7_2_Standard_Azure_RHUI-20161026220742 \
-g ahmet \
-p myPassword \
-e 22 \
-t "~/.ssh/id_rsa.pub" \
-z "Small" \
-l "West US"
```

### <a name="ssh-to-the-vm"></a><span data-ttu-id="1f9ae-114">Подключение к виртуальной машине по протоколу SSH</span><span class="sxs-lookup"><span data-stu-id="1f9ae-114">SSH to the VM</span></span>

```bash
ssh -i ~/.ssh/id_rsa ahmet@myVM
```

### <a name="update-yum-packages"></a><span data-ttu-id="1f9ae-115">Обновление пакетов YUM</span><span class="sxs-lookup"><span data-stu-id="1f9ae-115">Update YUM packages</span></span>

```bash
sudo yum update
```

### <a name="install-packages-needed"></a><span data-ttu-id="1f9ae-116">Установка требуемых пакетов</span><span class="sxs-lookup"><span data-stu-id="1f9ae-116">Install packages needed</span></span>

```bash
sudo yum -y install realmd sssd krb5-workstation krb5-libs
```

<span data-ttu-id="1f9ae-117">Теперь, когда все требуемые пакеты установлены на виртуальной машине Linux, мы готовы присоединить виртуальную машину к управляемому домену.</span><span class="sxs-lookup"><span data-stu-id="1f9ae-117">Now that the required packages are installed on the Linux virtual machine, the next task is to join the virtual machine to the managed domain.</span></span>

### <a name="discover-the-aad-domain-services-managed-domain"></a><span data-ttu-id="1f9ae-118">Поиск управляемого домена доменных служб AAD</span><span class="sxs-lookup"><span data-stu-id="1f9ae-118">Discover the AAD Domain Services managed domain</span></span>

```bash
sudo realm discover mydomain.com
```

### <a name="initialize-kerberos"></a><span data-ttu-id="1f9ae-119">Инициализация Kerberos</span><span class="sxs-lookup"><span data-stu-id="1f9ae-119">Initialize kerberos</span></span>

<span data-ttu-id="1f9ae-120">Обязательно укажите пользователя, который принадлежит к группе "Администраторы AAD AD".</span><span class="sxs-lookup"><span data-stu-id="1f9ae-120">Ensure that you specify a user who belongs to the 'AAD DC Administrators' group.</span></span> <span data-ttu-id="1f9ae-121">Только эти пользователи могут присоединять компьютеры к управляемому домену.</span><span class="sxs-lookup"><span data-stu-id="1f9ae-121">Only these users can join computers to the managed domain.</span></span>

```bash
kinit ahmet@mydomain.com
```

### <a name="join-the-machine-to-the-domain"></a><span data-ttu-id="1f9ae-122">Присоединение компьютера к домену</span><span class="sxs-lookup"><span data-stu-id="1f9ae-122">Join the machine to the domain</span></span>

```bash
sudo realm join --verbose mydomain.com -U 'ahmet@mydomain.com'
```

### <a name="verify-the-machine-is-joined-to-the-domain"></a><span data-ttu-id="1f9ae-123">Проверка присоединения компьютера к домену</span><span class="sxs-lookup"><span data-stu-id="1f9ae-123">Verify the machine is joined to the domain</span></span>

```bash
ssh -l ahmet@mydomain.com mydomain.cloudapp.net
```

## <a name="next-steps"></a><span data-ttu-id="1f9ae-124">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1f9ae-124">Next Steps</span></span>

* [<span data-ttu-id="1f9ae-125">Red Hat Update Infrastructure для предоставляемых по запросу виртуальных машин Red Hat Enterprise Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="1f9ae-125">Red Hat Update Infrastructure (RHUI) for on-demand Red Hat Enterprise Linux VMs in Azure</span></span>](update-infrastructure-redhat.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="1f9ae-126">Настройка хранилища ключей для виртуальных машин в Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1f9ae-126">Set up Key Vault for virtual machines in Azure Resource Manager</span></span>](key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="1f9ae-127">Развертывание виртуальных машин и управление ими с помощью шаблонов Azure Resource Manager и интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="1f9ae-127">Deploy and manage virtual machines by using Azure Resource Manager templates and the Azure CLI</span></span>](../linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
