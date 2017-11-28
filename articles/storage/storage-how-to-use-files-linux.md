---
title: "aaaUse хранилища Azure File с Linux | Документы Microsoft"
description: "Узнайте, как предоставить доступ по протоколу SMB на платформе Linux toomount файл Azure."
services: storage
documentationcenter: na
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 6edc37ce-698f-4d50-8fc1-591ad456175d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/8/2017
ms.author: renash
ms.openlocfilehash: ed6ba9b98f121d6629d858320ca3760384303ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-file-storage-with-linux"></a><span data-ttu-id="7b1ff-103">Использование хранилища файлов Azure в Linux</span><span class="sxs-lookup"><span data-stu-id="7b1ff-103">Use Azure File storage with Linux</span></span>
<span data-ttu-id="7b1ff-104">[Хранилище Azure файл](storage-dotnet-how-to-use-files.md) корпорации Майкрософт легко toouse облака файловую систему.</span><span class="sxs-lookup"><span data-stu-id="7b1ff-104">[Azure File storage](storage-dotnet-how-to-use-files.md) is Microsoft's easy toouse cloud file system.</span></span> <span data-ttu-id="7b1ff-105">Можно подключить Azure файловых ресурсов в ОС Linux с помощью hello [пакета cifs-utils](https://wiki.samba.org/index.php/LinuxCIFS_utils) из hello [Samba проекта](https://www.samba.org/).</span><span class="sxs-lookup"><span data-stu-id="7b1ff-105">Azure File shares can be mounted in Linux distributions using hello [cifs-utils package](https://wiki.samba.org/index.php/LinuxCIFS_utils) from hello [Samba project](https://www.samba.org/).</span></span> <span data-ttu-id="7b1ff-106">В этой статье показано два способа toomount Azure файловый ресурс: по запросу с hello `mount` команд и для загрузки путем создания записи в `/etc/fstab`.</span><span class="sxs-lookup"><span data-stu-id="7b1ff-106">This article shows two ways toomount an Azure File share: on-demand with hello `mount` command and on-boot by creating an entry in `/etc/fstab`.</span></span>

> [!NOTE]  
> <span data-ttu-id="7b1ff-107">В порядке toomount Azure файловый ресурс вне hello регион Azure, будет размещено в, например локально или в другом регионе Azure hello операционной системы должен поддерживать hello функциональные возможности шифрования SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="7b1ff-107">In order toomount an Azure File share outside of hello Azure region it is hosted in, such as on-premises or in a different Azure region, hello OS must support hello encryption functionality of SMB 3.0.</span></span> <span data-ttu-id="7b1ff-108">Функция шифрования протокола SMB 3.0 для Linux появилась в ядре версии 4.11.</span><span class="sxs-lookup"><span data-stu-id="7b1ff-108">Encryption feature for SMB 3.0 for Linux was introduced in 4.11 kernel.</span></span> <span data-ttu-id="7b1ff-109">Эта функция позволяет подключать общую папку файлов Azure из локальной среды или другого региона Azure.</span><span class="sxs-lookup"><span data-stu-id="7b1ff-109">This feature enables mounting of Azure File share from on-premises or a different Azure region.</span></span> <span data-ttu-id="7b1ff-110">Во время публикации hello эта функциональность была tooUbuntu backported из 16.04 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="7b1ff-110">At hello time of publishing, this functionality has been backported tooUbuntu from 16.04 and above.</span></span>


## <a name="prerequisities-for-mounting-an-azure-file-share-with-linux-and-hello-cifs-utils-package"></a><span data-ttu-id="7b1ff-111">Соответствия предварительным условиям для подключения Azure файловый ресурс с Linux и hello пакет cifs-utils</span><span class="sxs-lookup"><span data-stu-id="7b1ff-111">Prerequisities for mounting an Azure File share with Linux and hello cifs-utils package</span></span>
* <span data-ttu-id="7b1ff-112">**Выбрать дистрибутив Linux, может быть установлен пакет hello cifs-utils**: Корпорация Майкрософт рекомендует следующие дистрибутивы Linux в коллекции образов Azure hello hello:</span><span class="sxs-lookup"><span data-stu-id="7b1ff-112">**Pick a Linux distribution that can have hello cifs-utils package installed**: Microsoft recommends hello following Linux distributions in hello Azure image gallery:</span></span>

    * <span data-ttu-id="7b1ff-113">Ubuntu Server 14.04 или более поздней версии;</span><span class="sxs-lookup"><span data-stu-id="7b1ff-113">Ubuntu Server 14.04+</span></span>
    * <span data-ttu-id="7b1ff-114">RHEL 7 или более поздней версии;</span><span class="sxs-lookup"><span data-stu-id="7b1ff-114">RHEL 7+</span></span>
    * <span data-ttu-id="7b1ff-115">CentOS 7 или более поздней версии;</span><span class="sxs-lookup"><span data-stu-id="7b1ff-115">CentOS 7+</span></span>
    * <span data-ttu-id="7b1ff-116">Debian 8;</span><span class="sxs-lookup"><span data-stu-id="7b1ff-116">Debian 8</span></span>
    * <span data-ttu-id="7b1ff-117">openSUSE 13.2 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="7b1ff-117">openSUSE 13.2+</span></span>
    * <span data-ttu-id="7b1ff-118">SUSE Linux Enterprise Server 12</span><span class="sxs-lookup"><span data-stu-id="7b1ff-118">SUSE Linux Enterprise Server 12</span></span>

* <span data-ttu-id="7b1ff-119"><a id="install-cifs-utils"></a>**Hello cifs-utils пакет установлен**: hello cifs-utils можно установить с помощью диспетчера пакетов hello в дистрибутив Linux hello по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="7b1ff-119"><a id="install-cifs-utils"></a>**hello cifs-utils package is installed**: hello cifs-utils can be installed using hello package manager on hello Linux distribution of your choice.</span></span> 

    <span data-ttu-id="7b1ff-120">На **Ubuntu** и **основе Debian** распределения, а использовать hello `apt-get` диспетчера пакетов:</span><span class="sxs-lookup"><span data-stu-id="7b1ff-120">On **Ubuntu** and **Debian-based** distributions, use hello `apt-get` package manager:</span></span>

    ```
    sudo apt-get update
    sudo apt-get install cifs-utils
    ```

    <span data-ttu-id="7b1ff-121">На **RHEL** и **CentOS**, использовать hello `yum` диспетчера пакетов:</span><span class="sxs-lookup"><span data-stu-id="7b1ff-121">On **RHEL** and **CentOS**, use hello `yum` package manager:</span></span>

    ```
    sudo yum install samba-client samba-common cifs-utils
    ```

    <span data-ttu-id="7b1ff-122">На **openSUSE**, использовать hello `zypper` диспетчера пакетов:</span><span class="sxs-lookup"><span data-stu-id="7b1ff-122">On **openSUSE**, use hello `zypper` package manager:</span></span>

    ```
    sudo zypper install samba*
    ```

    <span data-ttu-id="7b1ff-123">В других дистрибутивах, используйте диспетчер hello соответствующий пакет или [компиляции из источника](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).</span><span class="sxs-lookup"><span data-stu-id="7b1ff-123">On other distributions, use hello appropriate package manager or [compile from source](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).</span></span>

* <span data-ttu-id="7b1ff-124">**Выбрать разрешения папками и файлами hello hello подключенного общего ресурса**: В hello ниже примерах мы используем 0777, toogive чтение, запись и выполнение tooall разрешения пользователей.</span><span class="sxs-lookup"><span data-stu-id="7b1ff-124">**Decide on hello directory/file permissions of hello mounted share**: In hello examples below, we use 0777, toogive read, write, and execute permissions tooall users.</span></span> <span data-ttu-id="7b1ff-125">При необходимости можно заменить его другим [разрешением chmod](https://en.wikipedia.org/wiki/Chmod).</span><span class="sxs-lookup"><span data-stu-id="7b1ff-125">You can replace it with other [chmod permissions](https://en.wikipedia.org/wiki/Chmod) as desired.</span></span> 

* <span data-ttu-id="7b1ff-126">**Имя учетной записи хранения**: toomount Azure общей папки, будет необходимо hello имя учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="7b1ff-126">**Storage Account Name**: toomount an Azure File share, you will need hello name of hello storage account.</span></span>

* <span data-ttu-id="7b1ff-127">**Ключ учетной записи хранения**: toomount Azure общей папки, будет необходимо hello ключ хранилища первичный (или вторичная).</span><span class="sxs-lookup"><span data-stu-id="7b1ff-127">**Storage Account Key**: toomount an Azure File share, you will need hello primary (or secondary) storage key.</span></span> <span data-ttu-id="7b1ff-128">В настоящее время ключи SAS для подключения не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="7b1ff-128">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="7b1ff-129">**Убедитесь в открыт порт 445**: SMB устанавливает соединения через TCP-порт 445 - проверьте toosee, если ваш брандмауэр не блокирует TCP-порты 445 с клиентского компьютера.</span><span class="sxs-lookup"><span data-stu-id="7b1ff-129">**Ensure port 445 is open**: SMB communicates over TCP port 445 - check toosee if your firewall is not blocking TCP ports 445 from client machine.</span></span>

## <a name="mount-hello-azure-file-share-on-demand-with-mount"></a><span data-ttu-id="7b1ff-130">Подключения по требованию с помощью общего файла Azure hello`mount`</span><span class="sxs-lookup"><span data-stu-id="7b1ff-130">Mount hello Azure File share on-demand with `mount`</span></span>
1. <span data-ttu-id="7b1ff-131">**[Установить пакет hello cifs средства для распространения Linux](#install-cifs-utils)**.</span><span class="sxs-lookup"><span data-stu-id="7b1ff-131">**[Install hello cifs-utils package for your Linux distribution](#install-cifs-utils)**.</span></span>

2. <span data-ttu-id="7b1ff-132">**Создайте папку для точки подключения hello**: это можно сделать в любом hello файловой системе.</span><span class="sxs-lookup"><span data-stu-id="7b1ff-132">**Create a folder for hello mount point**: This can be done anywhere on hello file system.</span></span>

    ```
    mkdir mymountpoint
    ```

3. <span data-ttu-id="7b1ff-133">**Используйте hello подключения команда toomount hello Azure общей папки**: помните tooreplace `<storage-account-name>`, `<share-name>`, и `<storage-account-key>` с hello соответствующие сведения.</span><span class="sxs-lookup"><span data-stu-id="7b1ff-133">**Use hello mount command toomount hello Azure File share**: Remember tooreplace `<storage-account-name>`, `<share-name>`, and `<storage-account-key>` with hello proper information.</span></span>

    ```
    sudo mount -t cifs //<storage-account-name>.file.core.windows.net/<share-name> ./mymountpoint -o vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino
    ```

> [!Note]  
> <span data-ttu-id="7b1ff-134">Закончив с помощью hello Azure общей папки, можно использовать `sudo umount ./mymountpoint` toounmount hello папки.</span><span class="sxs-lookup"><span data-stu-id="7b1ff-134">When you are done using hello Azure File share, you may use `sudo umount ./mymountpoint` toounmount hello share.</span></span>

## <a name="create-a-persistent-mount-point-for-hello-azure-file-share-with-etcfstab"></a><span data-ttu-id="7b1ff-135">Создать точку hello Azure общей папки на постоянные подключения`/etc/fstab`</span><span class="sxs-lookup"><span data-stu-id="7b1ff-135">Create a persistent mount point for hello Azure File share with `/etc/fstab`</span></span>
1. <span data-ttu-id="7b1ff-136">**[Установить пакет hello cifs средства для распространения Linux](#install-cifs-utils)**.</span><span class="sxs-lookup"><span data-stu-id="7b1ff-136">**[Install hello cifs-utils package for your Linux distribution](#install-cifs-utils)**.</span></span>

2. <span data-ttu-id="7b1ff-137">**Создайте папку для точки подключения hello**: это можно сделать в любом hello файловой системе, но необходимо toonote hello абсолютный путь к папке hello.</span><span class="sxs-lookup"><span data-stu-id="7b1ff-137">**Create a folder for hello mount point**: This can be done anywhere on hello file system, but you need toonote hello absolute path of hello folder.</span></span> <span data-ttu-id="7b1ff-138">Следующий пример Hello создает папку в корне.</span><span class="sxs-lookup"><span data-stu-id="7b1ff-138">hello following example creates a folder under root.</span></span>

    ```
    sudo mkdir /mymountpoint
    ```

3. <span data-ttu-id="7b1ff-139">**Используйте hello следующая команда слишком следующей строкой hello tooappend`/etc/fstab`**: помните tooreplace `<storage-account-name>`, `<share-name>`, и `<storage-account-key>` с hello соответствующие сведения.</span><span class="sxs-lookup"><span data-stu-id="7b1ff-139">**Use hello following command tooappend hello following line too`/etc/fstab`**: Remember tooreplace `<storage-account-name>`, `<share-name>`, and `<storage-account-key>` with hello proper information.</span></span>

    ```
    sudo bash -c 'echo "//<storage-account-name>.file.core.windows.net/<share-name> /mymountpoint cifs vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino" >> /etc/fstab'
    ```

> [!Note]  
> <span data-ttu-id="7b1ff-140">Можно использовать `sudo mount -a` toomount hello Azure общей папки после редактирования `/etc/fstab` вместо перезагрузки.</span><span class="sxs-lookup"><span data-stu-id="7b1ff-140">You can use `sudo mount -a` toomount hello Azure File share after editing `/etc/fstab` instead of rebooting.</span></span>

## <a name="feedback"></a><span data-ttu-id="7b1ff-141">Отзыв</span><span class="sxs-lookup"><span data-stu-id="7b1ff-141">Feedback</span></span>
<span data-ttu-id="7b1ff-142">Пользователи Linux, мы хотим toohear от вас!</span><span class="sxs-lookup"><span data-stu-id="7b1ff-142">Linux users, we want toohear from you!</span></span>

<span data-ttu-id="7b1ff-143">Hello хранилище файлов Azure для группы пользователей Linux форум для вас отзывы tooshare оценки и внедрению хранения файлов в Linux.</span><span class="sxs-lookup"><span data-stu-id="7b1ff-143">hello Azure File storage for Linux users' group provides a forum for you tooshare feedback as you evaluate and adopt File storage on Linux.</span></span> <span data-ttu-id="7b1ff-144">По электронной почте [хранилища Azure File пользователями Linux](mailto:azurefileslinuxusers@microsoft.com) toojoin hello пользователей группы.</span><span class="sxs-lookup"><span data-stu-id="7b1ff-144">Email [Azure File storage Linux Users](mailto:azurefileslinuxusers@microsoft.com) toojoin hello users' group.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b1ff-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7b1ff-145">Next steps</span></span>
<span data-ttu-id="7b1ff-146">Дополнительную информацию о хранилище файлов Azure см. по этим ссылкам.</span><span class="sxs-lookup"><span data-stu-id="7b1ff-146">See these links for more information about Azure File storage.</span></span>
* [<span data-ttu-id="7b1ff-147">Справочник по REST API службы файлов</span><span class="sxs-lookup"><span data-stu-id="7b1ff-147">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
* [<span data-ttu-id="7b1ff-148">Использование Azure PowerShell со службой хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="7b1ff-148">Using Azure PowerShell with Azure storage</span></span>](storage-powershell-guide-full.md)
* [<span data-ttu-id="7b1ff-149">Как toouse AzCopy с хранилищем Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="7b1ff-149">How toouse AzCopy with Microsoft Azure storage</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="7b1ff-150">С помощью hello Azure CLI с помощью хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="7b1ff-150">Using hello Azure CLI with Azure storage</span></span>](storage-azure-cli.md#create-and-manage-file-shares)
* [<span data-ttu-id="7b1ff-151">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="7b1ff-151">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="7b1ff-152">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="7b1ff-152">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)
