---
title: "Использование хранилища файлов Azure в Linux | Документация Майкрософт"
description: "Узнайте, как подключить общую папку Azure через протокол SMB с помощью Linux."
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
ms.openlocfilehash: 27b393a899c60a3a0393619f338a396dff659498
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="use-azure-file-storage-with-linux"></a><span data-ttu-id="3c0a5-103">Использование хранилища файлов Azure в Linux</span><span class="sxs-lookup"><span data-stu-id="3c0a5-103">Use Azure File storage with Linux</span></span>
<span data-ttu-id="3c0a5-104">[Хранилище файлов Azure](storage-dotnet-how-to-use-files.md) — это простая в использовании облачная файловая система Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="3c0a5-104">[Azure File storage](storage-dotnet-how-to-use-files.md) is Microsoft's easy to use cloud file system.</span></span> <span data-ttu-id="3c0a5-105">Общие папки Azure можно подключить в дистрибутивах Linux с помощью [пакета cifs-utils](https://wiki.samba.org/index.php/LinuxCIFS_utils) из [проекта Samba](https://www.samba.org/).</span><span class="sxs-lookup"><span data-stu-id="3c0a5-105">Azure File shares can be mounted in Linux distributions using the [cifs-utils package](https://wiki.samba.org/index.php/LinuxCIFS_utils) from the [Samba project](https://www.samba.org/).</span></span> <span data-ttu-id="3c0a5-106">В этой статье описаны два способа подключения общей папки Azure: по запросу с помощью команды `mount` и при загрузке путем создания записи в `/etc/fstab`.</span><span class="sxs-lookup"><span data-stu-id="3c0a5-106">This article shows two ways to mount an Azure File share: on-demand with the `mount` command and on-boot by creating an entry in `/etc/fstab`.</span></span>

> [!NOTE]  
> <span data-ttu-id="3c0a5-107">Чтобы подключить общую папку Azure за пределами региона Azure, в котором она размещается, например локально или в другом регионе Azure, операционная система должна поддерживать протокол функций шифрования SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="3c0a5-107">In order to mount an Azure File share outside of the Azure region it is hosted in, such as on-premises or in a different Azure region, the OS must support the encryption functionality of SMB 3.0.</span></span> <span data-ttu-id="3c0a5-108">Функция шифрования протокола SMB 3.0 для Linux появилась в ядре версии 4.11.</span><span class="sxs-lookup"><span data-stu-id="3c0a5-108">Encryption feature for SMB 3.0 for Linux was introduced in 4.11 kernel.</span></span> <span data-ttu-id="3c0a5-109">Эта функция позволяет подключать общую папку файлов Azure из локальной среды или другого региона Azure.</span><span class="sxs-lookup"><span data-stu-id="3c0a5-109">This feature enables mounting of Azure File share from on-premises or a different Azure region.</span></span> <span data-ttu-id="3c0a5-110">На момент публикации этой статьи функция была добавлена в дистрибутивы Ubuntu 16.04 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="3c0a5-110">At the time of publishing, this functionality has been backported to Ubuntu from 16.04 and above.</span></span>


## <a name="prerequisities-for-mounting-an-azure-file-share-with-linux-and-the-cifs-utils-package"></a><span data-ttu-id="3c0a5-111">Предварительные требования для подключения общей папки Azure с помощью Linux и пакета cifs-utils</span><span class="sxs-lookup"><span data-stu-id="3c0a5-111">Prerequisities for mounting an Azure File share with Linux and the cifs-utils package</span></span>
* <span data-ttu-id="3c0a5-112">**Выберите дистрибутив Linux, в который можно установить пакет cifs-utils**. Корпорация Майкрософт рекомендует следующие дистрибутивы Linux в коллекции образов Azure:</span><span class="sxs-lookup"><span data-stu-id="3c0a5-112">**Pick a Linux distribution that can have the cifs-utils package installed**: Microsoft recommends the following Linux distributions in the Azure image gallery:</span></span>

    * <span data-ttu-id="3c0a5-113">Ubuntu Server 14.04 или более поздней версии;</span><span class="sxs-lookup"><span data-stu-id="3c0a5-113">Ubuntu Server 14.04+</span></span>
    * <span data-ttu-id="3c0a5-114">RHEL 7 или более поздней версии;</span><span class="sxs-lookup"><span data-stu-id="3c0a5-114">RHEL 7+</span></span>
    * <span data-ttu-id="3c0a5-115">CentOS 7 или более поздней версии;</span><span class="sxs-lookup"><span data-stu-id="3c0a5-115">CentOS 7+</span></span>
    * <span data-ttu-id="3c0a5-116">Debian 8;</span><span class="sxs-lookup"><span data-stu-id="3c0a5-116">Debian 8</span></span>
    * <span data-ttu-id="3c0a5-117">openSUSE 13.2 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="3c0a5-117">openSUSE 13.2+</span></span>
    * <span data-ttu-id="3c0a5-118">SUSE Linux Enterprise Server 12</span><span class="sxs-lookup"><span data-stu-id="3c0a5-118">SUSE Linux Enterprise Server 12</span></span>

* <span data-ttu-id="3c0a5-119"><a id="install-cifs-utils"></a>**Установите пакет cifs-utils**. Пакет cifs-utils можно установить с помощью диспетчера пакетов в дистрибутиве Linux по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="3c0a5-119"><a id="install-cifs-utils"></a>**The cifs-utils package is installed**: The cifs-utils can be installed using the package manager on the Linux distribution of your choice.</span></span> 

    <span data-ttu-id="3c0a5-120">В дистрибутивах **Ubuntu** и **на основе Debian** используйте диспетчер пакетов `apt-get`:</span><span class="sxs-lookup"><span data-stu-id="3c0a5-120">On **Ubuntu** and **Debian-based** distributions, use the `apt-get` package manager:</span></span>

    ```
    sudo apt-get update
    sudo apt-get install cifs-utils
    ```

    <span data-ttu-id="3c0a5-121">В **RHEL** и **CentOS** используйте диспетчер пакетов `yum`:</span><span class="sxs-lookup"><span data-stu-id="3c0a5-121">On **RHEL** and **CentOS**, use the `yum` package manager:</span></span>

    ```
    sudo yum install samba-client samba-common cifs-utils
    ```

    <span data-ttu-id="3c0a5-122">В **openSUSE** используйте диспетчер пакетов `zypper`:</span><span class="sxs-lookup"><span data-stu-id="3c0a5-122">On **openSUSE**, use the `zypper` package manager:</span></span>

    ```
    sudo zypper install samba*
    ```

    <span data-ttu-id="3c0a5-123">В других дистрибутивах используйте соответствующий диспетчер пакетов или выполните [компиляцию из источника](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).</span><span class="sxs-lookup"><span data-stu-id="3c0a5-123">On other distributions, use the appropriate package manager or [compile from source](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).</span></span>

* <span data-ttu-id="3c0a5-124">**Выберите разрешения к каталогу и файлам подключаемой общей папки**. В приведенных ниже примерах используется разрешение 0777, чтобы все пользователи имели право на чтение, запись и выполнение файлов.</span><span class="sxs-lookup"><span data-stu-id="3c0a5-124">**Decide on the directory/file permissions of the mounted share**: In the examples below, we use 0777, to give read, write, and execute permissions to all users.</span></span> <span data-ttu-id="3c0a5-125">При необходимости можно заменить его другим [разрешением chmod](https://en.wikipedia.org/wiki/Chmod).</span><span class="sxs-lookup"><span data-stu-id="3c0a5-125">You can replace it with other [chmod permissions](https://en.wikipedia.org/wiki/Chmod) as desired.</span></span> 

* <span data-ttu-id="3c0a5-126">**Имя учетной записи хранения**: чтобы подключить общую папку Azure, вам потребуется имя учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="3c0a5-126">**Storage Account Name**: To mount an Azure File share, you will need the name of the storage account.</span></span>

* <span data-ttu-id="3c0a5-127">**Ключ учетной записи хранения**: чтобы подключить общую папку Azure, вам потребуется первичный (или вторичный) ключ учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="3c0a5-127">**Storage Account Key**: To mount an Azure File share, you will need the primary (or secondary) storage key.</span></span> <span data-ttu-id="3c0a5-128">В настоящее время ключи SAS для подключения не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="3c0a5-128">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="3c0a5-129">**Откройте порт 445**. Взаимодействие SMB выполняется через TCP-порт 445. Проверьте, чтобы брандмауэр не блокировал TCP-порты 445 с клиентского компьютера.</span><span class="sxs-lookup"><span data-stu-id="3c0a5-129">**Ensure port 445 is open**: SMB communicates over TCP port 445 - check to see if your firewall is not blocking TCP ports 445 from client machine.</span></span>

## <a name="mount-the-azure-file-share-on-demand-with-mount"></a><span data-ttu-id="3c0a5-130">Подключение общей папки Azure по требованию с помощью `mount`</span><span class="sxs-lookup"><span data-stu-id="3c0a5-130">Mount the Azure File share on-demand with `mount`</span></span>
1. <span data-ttu-id="3c0a5-131">**[Установите пакет cifs-utils для вашего дистрибутива Linux](#install-cifs-utils)**.</span><span class="sxs-lookup"><span data-stu-id="3c0a5-131">**[Install the cifs-utils package for your Linux distribution](#install-cifs-utils)**.</span></span>

2. <span data-ttu-id="3c0a5-132">**Создайте папку для точки подключения**. Это можно сделать в любом месте файловой системы.</span><span class="sxs-lookup"><span data-stu-id="3c0a5-132">**Create a folder for the mount point**: This can be done anywhere on the file system.</span></span>

    ```
    mkdir mymountpoint
    ```

3. <span data-ttu-id="3c0a5-133">**Используйте команду mount для подключения общей папки Azure**. Не забудьте заменить значения `<storage-account-name>`, `<share-name>` и `<storage-account-key>` соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="3c0a5-133">**Use the mount command to mount the Azure File share**: Remember to replace `<storage-account-name>`, `<share-name>`, and `<storage-account-key>` with the proper information.</span></span>

    ```
    sudo mount -t cifs //<storage-account-name>.file.core.windows.net/<share-name> ./mymountpoint -o vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino
    ```

> [!Note]  
> <span data-ttu-id="3c0a5-134">Чтобы отключить общую папку Azure, выполните команду `sudo umount ./mymountpoint`.</span><span class="sxs-lookup"><span data-stu-id="3c0a5-134">When you are done using the Azure File share, you may use `sudo umount ./mymountpoint` to unmount the share.</span></span>

## <a name="create-a-persistent-mount-point-for-the-azure-file-share-with-etcfstab"></a><span data-ttu-id="3c0a5-135">Создание постоянной точки подключения для общей папки Azure с помощью `/etc/fstab`</span><span class="sxs-lookup"><span data-stu-id="3c0a5-135">Create a persistent mount point for the Azure File share with `/etc/fstab`</span></span>
1. <span data-ttu-id="3c0a5-136">**[Установите пакет cifs-utils для вашего дистрибутива Linux](#install-cifs-utils)**.</span><span class="sxs-lookup"><span data-stu-id="3c0a5-136">**[Install the cifs-utils package for your Linux distribution](#install-cifs-utils)**.</span></span>

2. <span data-ttu-id="3c0a5-137">**Создайте папку для точки подключения**. Это можно сделать в любом месте файловой системы, но необходимо отметить абсолютный путь к папке.</span><span class="sxs-lookup"><span data-stu-id="3c0a5-137">**Create a folder for the mount point**: This can be done anywhere on the file system, but you need to note the absolute path of the folder.</span></span> <span data-ttu-id="3c0a5-138">В следующем примере создается папка в корне.</span><span class="sxs-lookup"><span data-stu-id="3c0a5-138">The following example creates a folder under root.</span></span>

    ```
    sudo mkdir /mymountpoint
    ```

3. <span data-ttu-id="3c0a5-139">**Используйте следующую команду, чтобы добавить следующую строку в `/etc/fstab`**. Не забудьте заменить значения `<storage-account-name>`, `<share-name>` и `<storage-account-key>` соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="3c0a5-139">**Use the following command to append the following line to `/etc/fstab`**: Remember to replace `<storage-account-name>`, `<share-name>`, and `<storage-account-key>` with the proper information.</span></span>

    ```
    sudo bash -c 'echo "//<storage-account-name>.file.core.windows.net/<share-name> /mymountpoint cifs vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino" >> /etc/fstab'
    ```

> [!Note]  
> <span data-ttu-id="3c0a5-140">Вместо перезагрузки можно использовать `sudo mount -a`, чтобы подключить общую папку после изменения `/etc/fstab`.</span><span class="sxs-lookup"><span data-stu-id="3c0a5-140">You can use `sudo mount -a` to mount the Azure File share after editing `/etc/fstab` instead of rebooting.</span></span>

## <a name="feedback"></a><span data-ttu-id="3c0a5-141">Отзыв</span><span class="sxs-lookup"><span data-stu-id="3c0a5-141">Feedback</span></span>
<span data-ttu-id="3c0a5-142">Пользователи Linux, нам очень интересно ваше мнение!</span><span class="sxs-lookup"><span data-stu-id="3c0a5-142">Linux users, we want to hear from you!</span></span>

<span data-ttu-id="3c0a5-143">Хранилище файлов Azure для группы пользователей Linux включает форум, где можно поделиться своим мнением и опытом адаптации хранилища файлов в Linux.</span><span class="sxs-lookup"><span data-stu-id="3c0a5-143">The Azure File storage for Linux users' group provides a forum for you to share feedback as you evaluate and adopt File storage on Linux.</span></span> <span data-ttu-id="3c0a5-144">Чтобы вступить в группу пользователей, отправьте электронное письмо в группу [Пользователи хранилища файлов Azure в Linux](mailto:azurefileslinuxusers@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="3c0a5-144">Email [Azure File storage Linux Users](mailto:azurefileslinuxusers@microsoft.com) to join the users' group.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c0a5-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3c0a5-145">Next steps</span></span>
<span data-ttu-id="3c0a5-146">Дополнительную информацию о хранилище файлов Azure см. по этим ссылкам.</span><span class="sxs-lookup"><span data-stu-id="3c0a5-146">See these links for more information about Azure File storage.</span></span>
* [<span data-ttu-id="3c0a5-147">Справочник по REST API службы файлов</span><span class="sxs-lookup"><span data-stu-id="3c0a5-147">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
* [<span data-ttu-id="3c0a5-148">Использование Azure PowerShell со службой хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="3c0a5-148">Using Azure PowerShell with Azure storage</span></span>](storage-powershell-guide-full.md)
* [<span data-ttu-id="3c0a5-149">Перенос данных с помощью AzCopy для Windows</span><span class="sxs-lookup"><span data-stu-id="3c0a5-149">How to use AzCopy with Microsoft Azure storage</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="3c0a5-150">Использование Azure CLI 2.0 со службой хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="3c0a5-150">Using the Azure CLI with Azure storage</span></span>](storage-azure-cli.md#create-and-manage-file-shares)
* [<span data-ttu-id="3c0a5-151">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="3c0a5-151">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="3c0a5-152">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="3c0a5-152">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)
