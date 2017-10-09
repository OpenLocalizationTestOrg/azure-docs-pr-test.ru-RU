---
title: "aaaCreate и использование SSH пары ключей для виртуальных машин Linux в Azure | Документы Microsoft"
description: "Как toocreate и использования открытого и закрытого пару ключей SSH для виртуальных машин Linux в Azure tooimprove hello безопасности hello процесса проверки подлинности."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 34ae9482-da3e-4b2d-9d0d-9d672aa42498
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/14/2017
ms.author: iainfou
ms.openlocfilehash: 7fb94841d34d5bc006f3134adf91102ddce5f174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-use-an-ssh-public-and-private-key-pair-for-linux-vms-in-azure"></a><span data-ttu-id="51de5-103">Как связать toocreate и использования открытого и закрытого ключа SSH для виртуальных машин Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="51de5-103">How toocreate and use an SSH public and private key pair for Linux VMs in Azure</span></span>
<span data-ttu-id="51de5-104">С помощью пары ключей безопасного shell (SSH) можно создать в Azure, использовать ключи SSH для проверки подлинности, устраняя необходимость hello toolog пароли в виртуальные машины (VM).</span><span class="sxs-lookup"><span data-stu-id="51de5-104">With a secure shell (SSH) key pair, you can create virtual machines (VMs) in Azure that use SSH keys for authentication, eliminating hello need for passwords toolog in.</span></span> <span data-ttu-id="51de5-105">В этой статье показано, как создать и использовать пару открытого и закрытого ключа файл RSA версии 2 протокола SSH для виртуальных машин Linux tooquickly.</span><span class="sxs-lookup"><span data-stu-id="51de5-105">This article shows you how tooquickly generate and use an SSH protocol version 2 RSA public and private key file pair for Linux VMs.</span></span> <span data-ttu-id="51de5-106">Более подробные инструкции и Дополнительные примеры см. в разделе [подробные пар ключей SSH toocreate действия и сертификаты](create-ssh-keys-detailed.md).</span><span class="sxs-lookup"><span data-stu-id="51de5-106">For more detailed steps and additional examples, see [detailed steps toocreate SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

## <a name="create-an-ssh-key-pair"></a><span data-ttu-id="51de5-107">Создание пары ключей SSH</span><span class="sxs-lookup"><span data-stu-id="51de5-107">Create an SSH key pair</span></span>
<span data-ttu-id="51de5-108">Используйте hello `ssh-keygen` команды toocreate SSH файлы открытого и закрытого ключа, по умолчанию, созданные в hello `~/.ssh` каталога, но можно указать другое расположение и дополнительных парольную фразу (пароль tooaccess hello файл закрытого ключа) при запрос.</span><span class="sxs-lookup"><span data-stu-id="51de5-108">Use hello `ssh-keygen` command toocreate SSH public and private key files that are by default created in hello `~/.ssh` directory, but you can specify a different location and additional passphrase (a password tooaccess hello private key file) when prompted.</span></span> <span data-ttu-id="51de5-109">Запустите следующую команду в оболочке Bash hello, ответы на hello приглашения с своих собственных сведений.</span><span class="sxs-lookup"><span data-stu-id="51de5-109">Run hello following command from a Bash shell, answering hello prompts with your own information.</span></span>

```bash
ssh-keygen -t rsa -b 2048
```

## <a name="use-hello-ssh-key-pair"></a><span data-ttu-id="51de5-110">Используйте пару ключей SSH hello</span><span class="sxs-lookup"><span data-stu-id="51de5-110">Use hello SSH key pair</span></span>
<span data-ttu-id="51de5-111">Hello открытый ключ, который поместить на ВМ Linux в Azure, по умолчанию сохраняется в `~/.ssh/id_rsa.pub`, если не изменено расположение hello при их создании.</span><span class="sxs-lookup"><span data-stu-id="51de5-111">hello public key that you place on your Linux VM in Azure is by default stored in `~/.ssh/id_rsa.pub`, unless you changed hello location when you created them.</span></span> <span data-ttu-id="51de5-112">При использовании hello [Azure CLI 2.0](/cli/azure) toocreate ВМ, укажите расположение hello этот открытый ключ, при использовании hello [создания виртуальной машины az](/cli/azure/vm#create) с hello `--ssh-key-path` параметр.</span><span class="sxs-lookup"><span data-stu-id="51de5-112">If you use hello [Azure CLI 2.0](/cli/azure) toocreate your VM, specify hello location of this public key when you use hello [az vm create](/cli/azure/vm#create) with hello `--ssh-key-path` option.</span></span> <span data-ttu-id="51de5-113">Если скопируйте и вставьте содержимое файла открытого ключа toouse hello hello в hello портал Azure или шаблона диспетчера ресурсов, убедитесь, что не копировать все дополнительные пробелы.</span><span class="sxs-lookup"><span data-stu-id="51de5-113">If you copy and paste hello contents of hello public key file toouse in hello Azure portal or a Resource Manager template, make sure you don't copy any additional whitespace.</span></span> <span data-ttu-id="51de5-114">Например, если вы используете OS X, можно передать hello файла открытого ключа (по умолчанию **~/.ssh/id_rsa.pub**) слишком**pbcopy** toocopy hello содержимого (используется в других программ Linux, которые hello одинаково, например `xclip`).</span><span class="sxs-lookup"><span data-stu-id="51de5-114">For example, if you use OS X, you can pipe hello public key file (by default, **~/.ssh/id_rsa.pub**) too**pbcopy** toocopy hello contents (there are other Linux programs that do hello same thing, such as `xclip`).</span></span>

<span data-ttu-id="51de5-115">Если вы не работали с открытым ключом SSH, чтобы просмотреть его, выполните команду `cat`, заменив параметр `~/.ssh/id_rsa.pub` расположением файла собственного открытого ключа.</span><span class="sxs-lookup"><span data-stu-id="51de5-115">If you're not familiar with SSH public keys, you can see your public key by running `cat` as follows, replacing `~/.ssh/id_rsa.pub` with your own public key file location:</span></span>

```bash
cat ~/.ssh/id_rsa.pub
```

<span data-ttu-id="51de5-116">Hello открытым ключом на ВМ Azure, SSH tooyour виртуальной Машины с помощью hello IP-адрес или DNS-имя виртуальной Машины (Помните tooreplace `azureuser` и `myvm.westus.cloudapp.azure.com` ниже используя hello пользователя с правами администратора и hello полное имя домена — или IP-адрес):</span><span class="sxs-lookup"><span data-stu-id="51de5-116">With hello public key on your Azure VM, SSH tooyour VM using hello IP address or DNS name of your VM (remember tooreplace `azureuser` and `myvm.westus.cloudapp.azure.com` below with hello admin username and hello fully qualified domain name -- or IP address):</span></span>

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

<span data-ttu-id="51de5-117">При указании парольную фразу при создании вашего пары ключей, введите парольную фразу hello при появлении запроса во время процесса входа в систему hello.</span><span class="sxs-lookup"><span data-stu-id="51de5-117">If you provided a passphrase when you created your key pair, enter hello passphrase when prompted during hello login process.</span></span> <span data-ttu-id="51de5-118">(сервер hello добавляется tooyour `~/.ssh/known_hosts` папки и не будет запрашиваться tooconnect пока hello открытого ключа на виртуальной Машине Azure изменения или имя сервера hello удаляется из `~/.ssh/known_hosts`.)</span><span class="sxs-lookup"><span data-stu-id="51de5-118">(hello server is added tooyour `~/.ssh/known_hosts` folder, and you won't be asked tooconnect again until hello public key on your Azure VM changes or hello server name is removed from `~/.ssh/known_hosts`.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="51de5-119">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="51de5-119">Next steps</span></span>

<span data-ttu-id="51de5-120">Виртуальные машины, созданные с помощью ключей SSH, по умолчанию настраивается с помощью паролей отключено, принудительно атаки методом подбора toomake пытается значительно дороже, а следовательно и сложной.</span><span class="sxs-lookup"><span data-stu-id="51de5-120">VMs created using SSH keys are by default configured with passwords disabled, toomake brute-forced guessing attempts vastly more expensive and therefore difficult.</span></span> <span data-ttu-id="51de5-121">В этой статье описано создание простой пары ключей SSH для быстрого использования.</span><span class="sxs-lookup"><span data-stu-id="51de5-121">This topic describes creating a simple SSH key pair for quick usage.</span></span> <span data-ttu-id="51de5-122">Если необходима дополнительная помощь при создании вашего пару ключей SSH или требуются дополнительные сертификаты, см. раздел [подробные пар ключей SSH toocreate действия и сертификаты](create-ssh-keys-detailed.md).</span><span class="sxs-lookup"><span data-stu-id="51de5-122">If you need more assistance in creating your SSH key pair or require additional certificates, see [Detailed steps toocreate SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

<span data-ttu-id="51de5-123">Можно создать виртуальные машины, использующие вашей пару ключей SSH с помощью портала Azure hello, CLI и шаблонов.</span><span class="sxs-lookup"><span data-stu-id="51de5-123">You can create VMs that use your SSH key pair using hello Azure portal, CLI, and templates:</span></span>

* [<span data-ttu-id="51de5-124">Создание безопасного ВМ Linux с помощью hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="51de5-124">Create a secure Linux VM using hello Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="51de5-125">Создание безопасного ВМ Linux с помощью hello Azure CLI 2.0)</span><span class="sxs-lookup"><span data-stu-id="51de5-125">Create a secure Linux VM using hello Azure CLI 2.0)</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="51de5-126">Создание защищенной виртуальной машины Linux с помощью шаблона Azure</span><span class="sxs-lookup"><span data-stu-id="51de5-126">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
