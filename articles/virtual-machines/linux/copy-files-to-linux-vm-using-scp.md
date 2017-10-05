---
title: "Перемещение файлов на виртуальные машины Linux в Azure и с них с помощью SCP | Документация Майкрософт"
description: "Безопасное перемещение файлов на виртуальную машину Linux в Azure и с нее с помощью SCP и пары ключей SSH."
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
ms.openlocfilehash: 736f7c11ec3de04f1ad52ee29d0a4c952c9b0545
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="move-files-to-and-from-a-linux-vm-using-scp"></a><span data-ttu-id="f266a-103">Перемещение файлов на виртуальную машину Linux и с нее с помощью SCP</span><span class="sxs-lookup"><span data-stu-id="f266a-103">Move files to and from a Linux VM using SCP</span></span>

<span data-ttu-id="f266a-104">В этой статье показано, как перемещать файлы между рабочей станцией и виртуальной машиной Azure под управлением Linux, используя протокол SCP.</span><span class="sxs-lookup"><span data-stu-id="f266a-104">This article shows how to move files from your workstation up to an Azure Linux VM, or from an Azure Linux VM down to your workstation, using Secure Copy (SCP).</span></span> <span data-ttu-id="f266a-105">Быстрое и безопасное перемещение файлов между рабочей станцией и виртуальной машиной с Linux является важной частью управления инфраструктурой Azure.</span><span class="sxs-lookup"><span data-stu-id="f266a-105">Moving files between your workstation and a Linux VM, quickly and securely, is critical for managing your Azure infrastructure.</span></span> 

<span data-ttu-id="f266a-106">Для этой статьи необходима виртуальная машина Linux, развернутая в Azure с помощью [файлов открытого и закрытого ключей SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f266a-106">For this article, you need a Linux VM deployed in Azure using [SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="f266a-107">Кроме того, нужен клиент SCP для локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="f266a-107">You also need an SCP client for your local computer.</span></span> <span data-ttu-id="f266a-108">Он создан на основе SSH и включен в стандартную оболочку Bash на большинстве компьютеров Linux и Mac, а также в некоторые оболочки Windows.</span><span class="sxs-lookup"><span data-stu-id="f266a-108">It is built on top of SSH and included in the default Bash shell of most Linux and Mac computers and some Windows shells.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="f266a-109">Быстрые команды</span><span class="sxs-lookup"><span data-stu-id="f266a-109">Quick commands</span></span>

<span data-ttu-id="f266a-110">Копирование файла на виртуальную машину под управлением Linux</span><span class="sxs-lookup"><span data-stu-id="f266a-110">Copy a file up to the Linux VM</span></span>

```bash
scp file azureuser@azurehost:directory/targetfile
```

<span data-ttu-id="f266a-111">Копирование файла с виртуальной машины под управлением Linux</span><span class="sxs-lookup"><span data-stu-id="f266a-111">Copy a file down from the Linux VM</span></span>

```bash
scp azureuser@azurehost:directory/file targetfile
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="f266a-112">Подробное пошаговое руководство</span><span class="sxs-lookup"><span data-stu-id="f266a-112">Detailed walkthrough</span></span>

<span data-ttu-id="f266a-113">В качестве примера мы переместим файл конфигурации Azure на виртуальную машины Linux и извлечем каталог файлов журнала, используя SCP и ключи SSH.</span><span class="sxs-lookup"><span data-stu-id="f266a-113">As examples, we move an Azure configuration file up to a Linux VM and pull down a log file directory, both using SCP and SSH keys.</span></span>   

## <a name="ssh-key-pair-authentication"></a><span data-ttu-id="f266a-114">Аутентификация с помощью пары ключей SSH</span><span class="sxs-lookup"><span data-stu-id="f266a-114">SSH key pair authentication</span></span>

<span data-ttu-id="f266a-115">SCP использует SSH на транспортном уровне.</span><span class="sxs-lookup"><span data-stu-id="f266a-115">SCP uses SSH for the transport layer.</span></span> <span data-ttu-id="f266a-116">Протокол SSH осуществляет аутентификацию на целевом узле, перемещая файл в зашифрованный канал, который по умолчанию предоставляется для SSH-подключения.</span><span class="sxs-lookup"><span data-stu-id="f266a-116">SSH handles the authentication on the destination host, and it moves the file in an encrypted tunnel provided by default with SSH.</span></span> <span data-ttu-id="f266a-117">Для аутентификации SSH можно использовать имена пользователей и пароли.</span><span class="sxs-lookup"><span data-stu-id="f266a-117">For SSH authentication, usernames and passwords can be used.</span></span> <span data-ttu-id="f266a-118">Тем не менее по соображениям безопасности рекомендуется использовать аутентификацию с открытым и закрытым ключами SSH.</span><span class="sxs-lookup"><span data-stu-id="f266a-118">However, SSH public and private key authentication are recommended as a security best practice.</span></span> <span data-ttu-id="f266a-119">После аутентификации подключения с помощью SSH инструмент SCP начинает копирование файла.</span><span class="sxs-lookup"><span data-stu-id="f266a-119">Once SSH has authenticated the connection, SCP then begins copying the file.</span></span> <span data-ttu-id="f266a-120">При использовании правильно настроенного файла `~/.ssh/config`, а также открытого и закрытого ключей SSH подключение SCP можно установить, указав только имя сервера (или IP-адрес).</span><span class="sxs-lookup"><span data-stu-id="f266a-120">Using a properly configured `~/.ssh/config` and SSH public and private keys, the SCP connection can be established by just using a server name (or IP address).</span></span> <span data-ttu-id="f266a-121">При наличии только одного ключа SSH инструмент SCP будет искать его в каталоге `~/.ssh/` и использовать по умолчанию для входа на виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="f266a-121">If you only have one SSH key, SCP looks for it in the `~/.ssh/` directory, and uses it by default to log in to the VM.</span></span>

<span data-ttu-id="f266a-122">Дополнительные сведения о настройке файла `~/.ssh/config`, а также открытом и закрытом ключах SSH см. в статье [Как создать и использовать пару из открытого и закрытого ключей SSH для виртуальных машин Linux в Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f266a-122">For more information on configuring your `~/.ssh/config` and SSH public and private keys, see [Create SSH keys](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="scp-a-file-to-a-linux-vm"></a><span data-ttu-id="f266a-123">Копирование файла на виртуальную машину Linux с помощью SCP</span><span class="sxs-lookup"><span data-stu-id="f266a-123">SCP a file to a Linux VM</span></span>

<span data-ttu-id="f266a-124">В первом примере файл конфигурации Azure копируется на виртуальную машину Linux, которая используется для автоматизации развертывания.</span><span class="sxs-lookup"><span data-stu-id="f266a-124">For the first example, we copy an Azure configuration file up to a Linux VM that is used to deploy automation.</span></span> <span data-ttu-id="f266a-125">Так как этот файл содержит учетные данные API Azure, в том числе секреты, важно обеспечить его безопасность.</span><span class="sxs-lookup"><span data-stu-id="f266a-125">Because this file contains Azure API credentials, which include secrets, security is important.</span></span> <span data-ttu-id="f266a-126">Зашифрованный туннель, предоставляемый SSH-подключением, защищает содержимое файла.</span><span class="sxs-lookup"><span data-stu-id="f266a-126">The encrypted tunnel provided by SSH protects the contents of the file.</span></span>

<span data-ttu-id="f266a-127">Следующая команда копирует локальный файл *.azure/config* на виртуальную машину Azure с полным доменным именем *myserver.eastus.cloudapp.azure.com*. Имя пользователя администратора на этой виртуальной машине Azure — *azureuser*.</span><span class="sxs-lookup"><span data-stu-id="f266a-127">The following command copies the local *.azure/config* file to an Azure VM with FQDN *myserver.eastus.cloudapp.azure.com*. The admin user name on the Azure VM is *azureuser*.</span></span> <span data-ttu-id="f266a-128">Файл копируется в каталог */home/azureuser*.</span><span class="sxs-lookup"><span data-stu-id="f266a-128">The file is targeted to the */home/azureuser/* directory.</span></span> <span data-ttu-id="f266a-129">Подставьте собственные значения в эту команду.</span><span class="sxs-lookup"><span data-stu-id="f266a-129">Substitute your own values in this command.</span></span>

```bash
scp ~/.azure/config azureuser@myserver.eastus.cloudapp.com:/home/azureuser/config
```

## <a name="scp-a-directory-from-a-linux-vm"></a><span data-ttu-id="f266a-130">Копирование каталога с виртуальной машины Linux с помощью SCP</span><span class="sxs-lookup"><span data-stu-id="f266a-130">SCP a directory from a Linux VM</span></span>

<span data-ttu-id="f266a-131">В этом примере выполняется копирование каталога с файлами журнала с виртуальной машины Linux на вашу рабочую станцию.</span><span class="sxs-lookup"><span data-stu-id="f266a-131">For this example, we copy a directory of log files from the Linux VM down to your workstation.</span></span> <span data-ttu-id="f266a-132">Файл журнала может содержать или не содержать секретные данные.</span><span class="sxs-lookup"><span data-stu-id="f266a-132">A log file may or may not contain sensitive or secret data.</span></span> <span data-ttu-id="f266a-133">Однако применение SCP гарантирует шифрование содержимого файлов журналов.</span><span class="sxs-lookup"><span data-stu-id="f266a-133">However, using SCP ensures the contents of the log files are encrypted.</span></span> <span data-ttu-id="f266a-134">Самый простой способ передать каталог и файлы журналов на рабочую станцию — использовать SCP для безопасной передачи файлов.</span><span class="sxs-lookup"><span data-stu-id="f266a-134">Using SCP to transfer the files is the easiest way to get the log directory and files down to your workstation while also being secure.</span></span>

<span data-ttu-id="f266a-135">Следующая команда копирует файлы из каталога */home/azureuser/logs/* на виртуальной машине Azure в локальный каталог /tmp.</span><span class="sxs-lookup"><span data-stu-id="f266a-135">The following command copies files in the */home/azureuser/logs/* directory on the Azure VM to the local /tmp directory:</span></span>

```bash
scp -r azureuser@myserver.eastus.cloudapp.com:/home/azureuser/logs/. /tmp/
```

<span data-ttu-id="f266a-136">Если в командной строке используется флаг `-r`, SCP рекурсивно копирует файлы и каталоги из места в каталоге, указанного в команде.</span><span class="sxs-lookup"><span data-stu-id="f266a-136">The `-r` cli flag instructs SCP to recursively copy the files and directories from the point of the directory listed in the command.</span></span>  <span data-ttu-id="f266a-137">Обратите также внимание, что синтаксис для командной строки аналогичен синтаксису команды копирования `cp`.</span><span class="sxs-lookup"><span data-stu-id="f266a-137">Also notice that the command-line syntax is similar to a `cp` copy command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f266a-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f266a-138">Next steps</span></span>

* [<span data-ttu-id="f266a-139">Управление пользователями, SSH и проверка или восстановление дисков в виртуальных машинах Azure с помощью расширения VMAccess</span><span class="sxs-lookup"><span data-stu-id="f266a-139">Manage users, SSH, and check or repair disks on Azure Linux VMs using the VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)