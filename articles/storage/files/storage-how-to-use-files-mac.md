---
title: "aaaMount Azure общей папки по протоколу SMB на macOS | Документы Microsoft"
description: "Узнайте, как toomount файл Azure предоставить доступ по протоколу SMB macOS."
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: 71aaec8a77b770fe147b783c0ab9f86830176bec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-share-over-smb-with-macos"></a>Подключение общей папки Azure через протокол SMB с помощью macOS
[Хранилище Azure файл](../storage-dotnet-how-to-use-files.md) службы корпорации Майкрософт, позволяющая toocreate и использование общих сетевых папок hello Azure использует отраслевой стандарт hello. Файловые ресурсы Azure можно подключить в macOS Sierra (10.12) и El Capitan (10.11). В этой статье показано toomount двумя различными способами Azure файловый ресурс на macOS с hello Finder пользовательского интерфейса и с помощью hello терминалов.

> [!Note]  
> Перед подключением общей папки Azure через протокол SMB, мы рекомендуем отключить подпись SMB-пакета. Если этого не сделать может привести снижению производительности при обращении к hello Azure общей папки из macOS. Подключение SMB шифруется, поэтому это не влияет на безопасность hello подключения. Из hello терминалов hello следующие команды отключит подписи SMB-пакетов, как описано в данном [статья службы поддержки Apple на отключение подписи SMB-пакетов](https://support.apple.com/HT205926):  
>    ```
>    sudo -s
>    echo "[default]" >> /etc/nsmb.conf
>    echo "signing_required=no" >> /etc/nsmb.conf
>    exit
>    ```

## <a name="prerequisites-for-mounting-an-azure-file-share-on-macos"></a>Предварительные требования для подключения общей папки Azure в macOS
* **Имя учетной записи хранения**: toomount Azure общей папки, будет необходимо hello имя учетной записи хранения hello.

* **Ключ учетной записи хранения**: toomount Azure общей папки, будет необходимо hello ключ хранилища первичный (или вторичная). В настоящее время ключи SAS для подключения не поддерживаются.

* **Откройте порт 445**: взаимодействие SMB выполняется через TCP-порт 445. На клиентском компьютере (hello Mac) Проверьте toomake том, что брандмауэр не блокирует порт 445 TCP.

## <a name="mount-an-azure-file-share-via-finder"></a>Подключение общей папки Azure через систему поиска
1. **Открыть в средстве поиска**: поиска должен быть открыт на macOS по умолчанию, но можно сделать это hello выбранного приложения, щелкнув hello» macOS сталкиваются значок» на закрепление hello:  
    ![значок сталкиваются Hello macOS](./media/storage-how-to-use-files-mac/mount-via-finder-1.png)

2. **Выберите «Подключиться tooServer» из меню «Go» hello**: с помощью UNC-путь hello из hello [необходимые компоненты](#preq), преобразовать две обратные косые черты hello начало (`\\`) слишком`smb://` и все другие символы обратной косой черты (`\`) tooforwards символы косой черты (`/`). Ссылка должна выглядеть hello следующим образом: ![диалоговое окно «Подключиться tooServer» hello](./media/storage-how-to-use-files-mac/mount-via-finder-2.png)

3. **Используйте hello папки имя и хранения ключ учетной записи при появлении запроса имени пользователя и пароля**: при нажатии кнопки «Подключить» в диалоговом окне «Подключиться tooServer» hello, появится для hello имя пользователя и пароль, (это будет autopopulated с вашей macOS имя пользователя). У вас есть возможность hello размещения ключ учетной записи имя/хранилище общей папки hello в вашей macOS цепочки ключей.

4. **Используйте hello Azure общую папку в случае необходимости**: после замены hello папки имя и хранения ключ учетной записи в hello имени пользователя и пароля, будет подключен hello общего ресурса. Можно использовать это как обычно используются локальной папки или общей папки, включая перетаскивание файлов в общей папке hello:

    ![Снимок подключенной общей папки Azure](./media/storage-how-to-use-files-mac/mount-via-finder-3.png)

## <a name="mount-an-azure-file-share-via-terminal"></a>Подключение общей папки Azure через терминал
1. Замените `<storage-account-name>` с именем hello вашей учетной записи хранилища. При появлении запроса укажите ключ учетной записи хранения в качестве пароля. 

    ```
    mount_smbfs //<storage-account-name>@<storage-account-name>.file.core.windows.net/<share-name> <desired-mount-point>
    ```

2. **Используйте hello Azure общую папку в случае необходимости**: hello Azure общей папки будет подключен в точке монтирования hello заданные hello предыдущей команды.  

    ![Моментальный снимок hello подключить Azure общей папки](./media/storage-how-to-use-files-mac/mount-via-terminal-1.png)

## <a name="next-steps"></a>Дальнейшие действия
Дополнительную информацию о хранилище файлов Azure см. по этим ссылкам.

* [Статья службы поддержки Apple - как tooconnect общий доступ к файлам на компьютере Mac](https://support.apple.com/HT204445)
* [Часто задаваемые вопросы](../storage-files-faq.md)
* [Troubleshoot Azure File storage problems in Windows](storage-troubleshoot-windows-file-connection-problems.md) (Устранение неполадок хранилища файлов Azure в Windows)      
* [Troubleshoot Azure File storage problems in Linux](storage-troubleshoot-linux-file-connection-problems.md) (Устранение неполадок хранилища файлов Azure в Linux)    