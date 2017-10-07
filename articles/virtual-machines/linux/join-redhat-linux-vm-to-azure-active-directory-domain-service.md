---
title: "aaaJoin tooan RedHat Linux VM Azure Active Directory доменных служб Active Directory | Документы Microsoft"
description: "Как toojoin существующие tooan RedHat Enterprise Linux 7 ВМ доменные службы Active Directory Azure."
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
ms.openlocfilehash: f3ba3c764e253191753f1cc5fc8c3b85c53818af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-redhat-linux-vm-tooan-azure-active-directory-domain-service"></a><span data-ttu-id="7bb9b-103">Присоединение виртуальной Машины с Linux RedHat tooan доменные службы Active Directory Azure</span><span class="sxs-lookup"><span data-stu-id="7bb9b-103">Join a RedHat Linux VM tooan Azure Active Directory Domain Service</span></span>

<span data-ttu-id="7bb9b-104">В этой статье показано, как toojoin tooan виртуальной машины Red Hat Enterprise Linux (RHEL) 7 Azure Active Directory домена службы (AADDS) Управление домена.</span><span class="sxs-lookup"><span data-stu-id="7bb9b-104">This article shows you how toojoin a Red Hat Enterprise Linux (RHEL) 7 virtual machine tooan Azure Active Directory Domain Services (AADDS) managed domain.</span></span>  <span data-ttu-id="7bb9b-105">Существуют следующие требования Hello.</span><span class="sxs-lookup"><span data-stu-id="7bb9b-105">hello requirements are:</span></span>

- <span data-ttu-id="7bb9b-106">[учетная запись Azure](https://azure.microsoft.com/pricing/free-trial/);</span><span class="sxs-lookup"><span data-stu-id="7bb9b-106">[an Azure account](https://azure.microsoft.com/pricing/free-trial/)</span></span>

- <span data-ttu-id="7bb9b-107">[файлы открытого и закрытого ключа SSH](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="7bb9b-107">[SSH public and private key files](mac-create-ssh-keys.md)</span></span>

- <span data-ttu-id="7bb9b-108">[доменные службы Azure Active Directory](../../active-directory-domain-services/active-directory-ds-getting-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7bb9b-108">[an Azure Active Directory Domain Services DC](../../active-directory-domain-services/active-directory-ds-getting-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="quick-commands"></a><span data-ttu-id="7bb9b-109">Быстрые команды</span><span class="sxs-lookup"><span data-stu-id="7bb9b-109">Quick Commands</span></span>

<span data-ttu-id="7bb9b-110">_Замените все примеры параметров своими значениями_.</span><span class="sxs-lookup"><span data-stu-id="7bb9b-110">_Replace any examples with your own settings._</span></span>

### <a name="switch-hello-azure-cli-tooclassic-deployment-mode"></a><span data-ttu-id="7bb9b-111">Переключение режима развертывания tooclassic hello azure cli</span><span class="sxs-lookup"><span data-stu-id="7bb9b-111">Switch hello azure-cli tooclassic deployment mode</span></span>

```azurecli
azure config mode asm
```

### <a name="search-for-a-rhel-version-and-image"></a><span data-ttu-id="7bb9b-112">Поиск версии и образа RHEL</span><span class="sxs-lookup"><span data-stu-id="7bb9b-112">Search for a RHEL version and image</span></span>

```azurecli
azure vm image list | grep "Red Hat"
```

### <a name="create-a-redhat-linux-vm"></a><span data-ttu-id="7bb9b-113">Создание виртуальной машины Red Hat Linux</span><span class="sxs-lookup"><span data-stu-id="7bb9b-113">Create a Redhat Linux VM</span></span>

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

### <a name="ssh-toohello-vm"></a><span data-ttu-id="7bb9b-114">Toohello SSH виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="7bb9b-114">SSH toohello VM</span></span>

```bash
ssh -i ~/.ssh/id_rsa ahmet@myVM
```

### <a name="update-yum-packages"></a><span data-ttu-id="7bb9b-115">Обновление пакетов YUM</span><span class="sxs-lookup"><span data-stu-id="7bb9b-115">Update YUM packages</span></span>

```bash
sudo yum update
```

### <a name="install-packages-needed"></a><span data-ttu-id="7bb9b-116">Установка требуемых пакетов</span><span class="sxs-lookup"><span data-stu-id="7bb9b-116">Install packages needed</span></span>

```bash
sudo yum -y install realmd sssd krb5-workstation krb5-libs
```

<span data-ttu-id="7bb9b-117">Теперь, когда требуется hello пакеты устанавливаются на виртуальной машине Linux hello, следующая задача hello-toojoin hello виртуальной машины toohello управляемый домен.</span><span class="sxs-lookup"><span data-stu-id="7bb9b-117">Now that hello required packages are installed on hello Linux virtual machine, hello next task is toojoin hello virtual machine toohello managed domain.</span></span>

### <a name="discover-hello-aad-domain-services-managed-domain"></a><span data-ttu-id="7bb9b-118">Обнаружение управляемого домена доменных служб AAD hello</span><span class="sxs-lookup"><span data-stu-id="7bb9b-118">Discover hello AAD Domain Services managed domain</span></span>

```bash
sudo realm discover mydomain.com
```

### <a name="initialize-kerberos"></a><span data-ttu-id="7bb9b-119">Инициализация Kerberos</span><span class="sxs-lookup"><span data-stu-id="7bb9b-119">Initialize kerberos</span></span>

<span data-ttu-id="7bb9b-120">Убедитесь, что пользователь, принадлежащий группы администраторов контроллера домена, toohello «AAD».</span><span class="sxs-lookup"><span data-stu-id="7bb9b-120">Ensure that you specify a user who belongs toohello 'AAD DC Administrators' group.</span></span> <span data-ttu-id="7bb9b-121">Только эти пользователи могут присоединен к домену управляемых компьютеров toohello.</span><span class="sxs-lookup"><span data-stu-id="7bb9b-121">Only these users can join computers toohello managed domain.</span></span>

```bash
kinit ahmet@mydomain.com
```

### <a name="join-hello-machine-toohello-domain"></a><span data-ttu-id="7bb9b-122">Домену toohello машины hello</span><span class="sxs-lookup"><span data-stu-id="7bb9b-122">Join hello machine toohello domain</span></span>

```bash
sudo realm join --verbose mydomain.com -U 'ahmet@mydomain.com'
```

### <a name="verify-hello-machine-is-joined-toohello-domain"></a><span data-ttu-id="7bb9b-123">Убедитесь, что hello машины присоединены к домену toohello домена</span><span class="sxs-lookup"><span data-stu-id="7bb9b-123">Verify hello machine is joined toohello domain</span></span>

```bash
ssh -l ahmet@mydomain.com mydomain.cloudapp.net
```

## <a name="next-steps"></a><span data-ttu-id="7bb9b-124">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7bb9b-124">Next Steps</span></span>

* [<span data-ttu-id="7bb9b-125">Red Hat Update Infrastructure для предоставляемых по запросу виртуальных машин Red Hat Enterprise Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="7bb9b-125">Red Hat Update Infrastructure (RHUI) for on-demand Red Hat Enterprise Linux VMs in Azure</span></span>](update-infrastructure-redhat.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="7bb9b-126">Настройка хранилища ключей для виртуальных машин в Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7bb9b-126">Set up Key Vault for virtual machines in Azure Resource Manager</span></span>](key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="7bb9b-127">Развертывание и управление виртуальными машинами с помощью шаблонов диспетчера ресурсов Azure и hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7bb9b-127">Deploy and manage virtual machines by using Azure Resource Manager templates and hello Azure CLI</span></span>](../linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
