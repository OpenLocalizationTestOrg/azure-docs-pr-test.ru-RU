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
# <a name="use-azure-file-storage-with-linux"></a>Использование хранилища файлов Azure в Linux
[Хранилище Azure файл](storage-dotnet-how-to-use-files.md) корпорации Майкрософт легко toouse облака файловую систему. Можно подключить Azure файловых ресурсов в ОС Linux с помощью hello [пакета cifs-utils](https://wiki.samba.org/index.php/LinuxCIFS_utils) из hello [Samba проекта](https://www.samba.org/). В этой статье показано два способа toomount Azure файловый ресурс: по запросу с hello `mount` команд и для загрузки путем создания записи в `/etc/fstab`.

> [!NOTE]  
> В порядке toomount Azure файловый ресурс вне hello регион Azure, будет размещено в, например локально или в другом регионе Azure hello операционной системы должен поддерживать hello функциональные возможности шифрования SMB 3.0. Функция шифрования протокола SMB 3.0 для Linux появилась в ядре версии 4.11. Эта функция позволяет подключать общую папку файлов Azure из локальной среды или другого региона Azure. Во время публикации hello эта функциональность была tooUbuntu backported из 16.04 и более поздних версий.


## <a name="prerequisities-for-mounting-an-azure-file-share-with-linux-and-hello-cifs-utils-package"></a>Соответствия предварительным условиям для подключения Azure файловый ресурс с Linux и hello пакет cifs-utils
* **Выбрать дистрибутив Linux, может быть установлен пакет hello cifs-utils**: Корпорация Майкрософт рекомендует следующие дистрибутивы Linux в коллекции образов Azure hello hello:

    * Ubuntu Server 14.04 или более поздней версии;
    * RHEL 7 или более поздней версии;
    * CentOS 7 или более поздней версии;
    * Debian 8;
    * openSUSE 13.2 или более поздней версии.
    * SUSE Linux Enterprise Server 12

* <a id="install-cifs-utils"></a>**Hello cifs-utils пакет установлен**: hello cifs-utils можно установить с помощью диспетчера пакетов hello в дистрибутив Linux hello по своему усмотрению. 

    На **Ubuntu** и **основе Debian** распределения, а использовать hello `apt-get` диспетчера пакетов:

    ```
    sudo apt-get update
    sudo apt-get install cifs-utils
    ```

    На **RHEL** и **CentOS**, использовать hello `yum` диспетчера пакетов:

    ```
    sudo yum install samba-client samba-common cifs-utils
    ```

    На **openSUSE**, использовать hello `zypper` диспетчера пакетов:

    ```
    sudo zypper install samba*
    ```

    В других дистрибутивах, используйте диспетчер hello соответствующий пакет или [компиляции из источника](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).

* **Выбрать разрешения папками и файлами hello hello подключенного общего ресурса**: В hello ниже примерах мы используем 0777, toogive чтение, запись и выполнение tooall разрешения пользователей. При необходимости можно заменить его другим [разрешением chmod](https://en.wikipedia.org/wiki/Chmod). 

* **Имя учетной записи хранения**: toomount Azure общей папки, будет необходимо hello имя учетной записи хранения hello.

* **Ключ учетной записи хранения**: toomount Azure общей папки, будет необходимо hello ключ хранилища первичный (или вторичная). В настоящее время ключи SAS для подключения не поддерживаются.

* **Убедитесь в открыт порт 445**: SMB устанавливает соединения через TCP-порт 445 - проверьте toosee, если ваш брандмауэр не блокирует TCP-порты 445 с клиентского компьютера.

## <a name="mount-hello-azure-file-share-on-demand-with-mount"></a>Подключения по требованию с помощью общего файла Azure hello`mount`
1. **[Установить пакет hello cifs средства для распространения Linux](#install-cifs-utils)**.

2. **Создайте папку для точки подключения hello**: это можно сделать в любом hello файловой системе.

    ```
    mkdir mymountpoint
    ```

3. **Используйте hello подключения команда toomount hello Azure общей папки**: помните tooreplace `<storage-account-name>`, `<share-name>`, и `<storage-account-key>` с hello соответствующие сведения.

    ```
    sudo mount -t cifs //<storage-account-name>.file.core.windows.net/<share-name> ./mymountpoint -o vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino
    ```

> [!Note]  
> Закончив с помощью hello Azure общей папки, можно использовать `sudo umount ./mymountpoint` toounmount hello папки.

## <a name="create-a-persistent-mount-point-for-hello-azure-file-share-with-etcfstab"></a>Создать точку hello Azure общей папки на постоянные подключения`/etc/fstab`
1. **[Установить пакет hello cifs средства для распространения Linux](#install-cifs-utils)**.

2. **Создайте папку для точки подключения hello**: это можно сделать в любом hello файловой системе, но необходимо toonote hello абсолютный путь к папке hello. Следующий пример Hello создает папку в корне.

    ```
    sudo mkdir /mymountpoint
    ```

3. **Используйте hello следующая команда слишком следующей строкой hello tooappend`/etc/fstab`**: помните tooreplace `<storage-account-name>`, `<share-name>`, и `<storage-account-key>` с hello соответствующие сведения.

    ```
    sudo bash -c 'echo "//<storage-account-name>.file.core.windows.net/<share-name> /mymountpoint cifs vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino" >> /etc/fstab'
    ```

> [!Note]  
> Можно использовать `sudo mount -a` toomount hello Azure общей папки после редактирования `/etc/fstab` вместо перезагрузки.

## <a name="feedback"></a>Отзыв
Пользователи Linux, мы хотим toohear от вас!

Hello хранилище файлов Azure для группы пользователей Linux форум для вас отзывы tooshare оценки и внедрению хранения файлов в Linux. По электронной почте [хранилища Azure File пользователями Linux](mailto:azurefileslinuxusers@microsoft.com) toojoin hello пользователей группы.

## <a name="next-steps"></a>Дальнейшие действия
Дополнительную информацию о хранилище файлов Azure см. по этим ссылкам.
* [Справочник по REST API службы файлов](http://msdn.microsoft.com/library/azure/dn167006.aspx)
* [Использование Azure PowerShell со службой хранилища Azure](storage-powershell-guide-full.md)
* [Как toouse AzCopy с хранилищем Microsoft Azure](storage-use-azcopy.md)
* [С помощью hello Azure CLI с помощью хранилища Azure](storage-azure-cli.md#create-and-manage-file-shares)
* [Часто задаваемые вопросы](storage-files-faq.md)
* [Устранение неполадок](storage-troubleshoot-file-connection-problems.md)
