---
title: "aaaMove файлы tooand из виртуальных машин Linux Azure с SCP | Документы Microsoft"
description: "Безопасно перемещать файлы tooand из виртуальной Машины Linux в Azure с использованием точки подключения службы и пару ключей SSH."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: danlep
ms.openlocfilehash: 9e4dce667aa581df74aec3d45a6ba5e52f777d1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-files-tooand-from-a-linux-vm-using-scp"></a><span data-ttu-id="06683-103">Перемещение файлов tooand с ВМ Linux с помощью точки подключения службы</span><span class="sxs-lookup"><span data-stu-id="06683-103">Move files tooand from a Linux VM using SCP</span></span>

<span data-ttu-id="06683-104">В этой статье показано, как toomove файлы из рабочей станции вверх tooan виртуальной Машине Linux Azure или виртуальной Машине Linux Azure работы tooyour рабочей станции, с использованием безопасного копирования (SCP).</span><span class="sxs-lookup"><span data-stu-id="06683-104">This article shows how toomove files from your workstation up tooan Azure Linux VM, or from an Azure Linux VM down tooyour workstation, using Secure Copy (SCP).</span></span> <span data-ttu-id="06683-105">Быстрое и безопасное перемещение файлов между рабочей станцией и виртуальной машиной с Linux является важной частью управления инфраструктурой Azure.</span><span class="sxs-lookup"><span data-stu-id="06683-105">Moving files between your workstation and a Linux VM, quickly and securely, is critical for managing your Azure infrastructure.</span></span> 

<span data-ttu-id="06683-106">Для этой статьи необходима виртуальная машина Linux, развернутая в Azure с помощью [файлов открытого и закрытого ключей SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="06683-106">For this article, you need a Linux VM deployed in Azure using [SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="06683-107">Кроме того, нужен клиент SCP для локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="06683-107">You also need an SCP client for your local computer.</span></span> <span data-ttu-id="06683-108">При разработке на основе SSH и включены в оболочке Bash по умолчанию hello большинство компьютеров Linux и Mac и некоторые оболочки Windows.</span><span class="sxs-lookup"><span data-stu-id="06683-108">It is built on top of SSH and included in hello default Bash shell of most Linux and Mac computers and some Windows shells.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="06683-109">Быстрые команды</span><span class="sxs-lookup"><span data-stu-id="06683-109">Quick commands</span></span>

<span data-ttu-id="06683-110">Скопируйте файл вверх toohello ВМ Linux</span><span class="sxs-lookup"><span data-stu-id="06683-110">Copy a file up toohello Linux VM</span></span>

```bash
scp file azureuser@azurehost:directory/targetfile
```

<span data-ttu-id="06683-111">Скопируйте файл вниз с hello ВМ Linux</span><span class="sxs-lookup"><span data-stu-id="06683-111">Copy a file down from hello Linux VM</span></span>

```bash
scp azureuser@azurehost:directory/file targetfile
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="06683-112">Подробное пошаговое руководство</span><span class="sxs-lookup"><span data-stu-id="06683-112">Detailed walkthrough</span></span>

<span data-ttu-id="06683-113">В качестве примеров, мы переместить в файл конфигурации Azure вверх tooa виртуальной Машины Linux и открыть его в каталог файла журнала, как с помощью клавиш SCP и SSH.</span><span class="sxs-lookup"><span data-stu-id="06683-113">As examples, we move an Azure configuration file up tooa Linux VM and pull down a log file directory, both using SCP and SSH keys.</span></span>   

## <a name="ssh-key-pair-authentication"></a><span data-ttu-id="06683-114">Аутентификация с помощью пары ключей SSH</span><span class="sxs-lookup"><span data-stu-id="06683-114">SSH key pair authentication</span></span>

<span data-ttu-id="06683-115">Точка подключения службы использует SSH для hello транспортного уровня.</span><span class="sxs-lookup"><span data-stu-id="06683-115">SCP uses SSH for hello transport layer.</span></span> <span data-ttu-id="06683-116">SSH дескрипторы hello проверки подлинности на конечном узле hello и он перемещает файл hello в зашифрованный канал SSH в состав по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="06683-116">SSH handles hello authentication on hello destination host, and it moves hello file in an encrypted tunnel provided by default with SSH.</span></span> <span data-ttu-id="06683-117">Для аутентификации SSH можно использовать имена пользователей и пароли.</span><span class="sxs-lookup"><span data-stu-id="06683-117">For SSH authentication, usernames and passwords can be used.</span></span> <span data-ttu-id="06683-118">Тем не менее по соображениям безопасности рекомендуется использовать аутентификацию с открытым и закрытым ключами SSH.</span><span class="sxs-lookup"><span data-stu-id="06683-118">However, SSH public and private key authentication are recommended as a security best practice.</span></span> <span data-ttu-id="06683-119">После SSH прошел проверку соединения hello, SCP затем начинает копирование файла hello.</span><span class="sxs-lookup"><span data-stu-id="06683-119">Once SSH has authenticated hello connection, SCP then begins copying hello file.</span></span> <span data-ttu-id="06683-120">С помощью правильно настроенного `~/.ssh/config` и открытые и закрытые ключи SSH, hello SCP соединение может быть установлено с использованием только имя сервера (или IP-адрес).</span><span class="sxs-lookup"><span data-stu-id="06683-120">Using a properly configured `~/.ssh/config` and SSH public and private keys, hello SCP connection can be established by just using a server name (or IP address).</span></span> <span data-ttu-id="06683-121">Если имеется только один ключ SSH, SCP ищет его в hello `~/.ssh/` каталога и использует его по умолчанию toolog в toohello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="06683-121">If you only have one SSH key, SCP looks for it in hello `~/.ssh/` directory, and uses it by default toolog in toohello VM.</span></span>

<span data-ttu-id="06683-122">Дополнительные сведения о настройке файла `~/.ssh/config`, а также открытом и закрытом ключах SSH см. в статье [Как создать и использовать пару из открытого и закрытого ключей SSH для виртуальных машин Linux в Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="06683-122">For more information on configuring your `~/.ssh/config` and SSH public and private keys, see [Create SSH keys](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="scp-a-file-tooa-linux-vm"></a><span data-ttu-id="06683-123">Точка подключения службы tooa файл виртуальной Машины с Linux</span><span class="sxs-lookup"><span data-stu-id="06683-123">SCP a file tooa Linux VM</span></span>

<span data-ttu-id="06683-124">Первый пример hello мы скопировать файл конфигурации Azure вверх tooa виртуальной Машины Linux, которое используется toodeploy автоматизации.</span><span class="sxs-lookup"><span data-stu-id="06683-124">For hello first example, we copy an Azure configuration file up tooa Linux VM that is used toodeploy automation.</span></span> <span data-ttu-id="06683-125">Так как этот файл содержит учетные данные API Azure, в том числе секреты, важно обеспечить его безопасность.</span><span class="sxs-lookup"><span data-stu-id="06683-125">Because this file contains Azure API credentials, which include secrets, security is important.</span></span> <span data-ttu-id="06683-126">Hello зашифрованные туннель SSH, предоставляемые защищает hello содержимое файла hello.</span><span class="sxs-lookup"><span data-stu-id="06683-126">hello encrypted tunnel provided by SSH protects hello contents of hello file.</span></span>

<span data-ttu-id="06683-127">Здравствуйте, следующие команды копий hello локальной *.azure/config* файл tooan ВМ Azure с полным доменным ИМЕНЕМ *myserver.eastus.cloudapp.azure.com*. — имя пользователя администратора hello на виртуальной Машине Azure hello *azureuser* .</span><span class="sxs-lookup"><span data-stu-id="06683-127">hello following command copies hello local *.azure/config* file tooan Azure VM with FQDN *myserver.eastus.cloudapp.azure.com*. hello admin user name on hello Azure VM is *azureuser*.</span></span> <span data-ttu-id="06683-128">Hello файл является целевой toohello */home/azureuser/* каталога.</span><span class="sxs-lookup"><span data-stu-id="06683-128">hello file is targeted toohello */home/azureuser/* directory.</span></span> <span data-ttu-id="06683-129">Подставьте собственные значения в эту команду.</span><span class="sxs-lookup"><span data-stu-id="06683-129">Substitute your own values in this command.</span></span>

```bash
scp ~/.azure/config azureuser@myserver.eastus.cloudapp.com:/home/azureuser/config
```

## <a name="scp-a-directory-from-a-linux-vm"></a><span data-ttu-id="06683-130">Копирование каталога с виртуальной машины Linux с помощью SCP</span><span class="sxs-lookup"><span data-stu-id="06683-130">SCP a directory from a Linux VM</span></span>

<span data-ttu-id="06683-131">В этом примере мы копируем каталог файлов журнала из hello ВМ Linux работы tooyour рабочей станции.</span><span class="sxs-lookup"><span data-stu-id="06683-131">For this example, we copy a directory of log files from hello Linux VM down tooyour workstation.</span></span> <span data-ttu-id="06683-132">Файл журнала может содержать или не содержать секретные данные.</span><span class="sxs-lookup"><span data-stu-id="06683-132">A log file may or may not contain sensitive or secret data.</span></span> <span data-ttu-id="06683-133">Тем не менее с помощью SCP гарантирует, что зашифрованные hello содержимое файлов журналов hello.</span><span class="sxs-lookup"><span data-stu-id="06683-133">However, using SCP ensures hello contents of hello log files are encrypted.</span></span> <span data-ttu-id="06683-134">С помощью файлов hello tootransfer SCP является наиболее простым способом tooget hello Здравствуйте, при этом безопасный каталог журнала и файлы работы tooyour рабочей станции.</span><span class="sxs-lookup"><span data-stu-id="06683-134">Using SCP tootransfer hello files is hello easiest way tooget hello log directory and files down tooyour workstation while also being secure.</span></span>

<span data-ttu-id="06683-135">Hello следующая команда копирует файлы в hello */home/azureuser/журналы/* каталог в каталоге/tmp локального toohello виртуальной Машины Azure hello:</span><span class="sxs-lookup"><span data-stu-id="06683-135">hello following command copies files in hello */home/azureuser/logs/* directory on hello Azure VM toohello local /tmp directory:</span></span>

```bash
scp -r azureuser@myserver.eastus.cloudapp.com:/home/azureuser/logs/. /tmp/
```

<span data-ttu-id="06683-136">Hello `-r` cli флаг указывает, что точка подключения службы toorecursively копирования hello файлы и каталоги из точки hello hello каталог, который указан в команде hello.</span><span class="sxs-lookup"><span data-stu-id="06683-136">hello `-r` cli flag instructs SCP toorecursively copy hello files and directories from hello point of hello directory listed in hello command.</span></span>  <span data-ttu-id="06683-137">Также Обратите внимание, что hello синтаксис командной строки — примерно tooa `cp` скопируйте команду.</span><span class="sxs-lookup"><span data-stu-id="06683-137">Also notice that hello command-line syntax is similar tooa `cp` copy command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="06683-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="06683-138">Next steps</span></span>

* [<span data-ttu-id="06683-139">Управлять пользователями, SSH и проверку или восстановление дисков на виртуальных машинах Linux в Azure с помощью hello расширения VMAccess</span><span class="sxs-lookup"><span data-stu-id="06683-139">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
