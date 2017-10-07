---
title: "совместное использование aaaMount Azure файловый ресурс и hello доступа в Windows | Документы Microsoft"
description: "Подключите файлов Azure и общую папку hello доступа в Windows."
services: storage
documentationcenter: na
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
ms.openlocfilehash: 15ac468d9d7b8e0a195b024926ed4dd9790360d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="mount-an-azure-file-share-and-access-hello-share-in-windows"></a>Подключить файлов Azure и общую папку hello доступа в Windows
[Хранилище Azure файл](storage-dotnet-how-to-use-files.md) корпорации Майкрософт легко toouse облака файловую систему. Файловые ресурсы Azure можно подключить в Windows и Windows Server. В этой статье показано три разных способа toomount Azure файловый ресурс в Windows: с hello файл пользовательский Интерфейс через PowerShell, а также через командную строку hello. 

В порядке toomount Azure файловый ресурс-вне hello регион Azure, которую она размещается в, например локально или в другом регионе Azure hello операционной системы должен поддерживать SMB 3.0. 

В зависимости от версии операционной системы общую папку Azure можно подключить локально на компьютере под управлением Windows или на виртуальной машине Azure. Приведенной ниже таблице указаны hello 

| Версия Windows        | Версия SMB |Возможность подключения на виртуальной машине Azure|Возможность подключения в локальной среде|
|------------------------|-------------|---------------------|---------------------|
| Windows 7              | SMB 2.1     | Да                 | Нет                  |
| Windows Server 2008 R2 | SMB 2.1     | Да                 | Нет                  |
| Windows 8              | SMB 3.0     | Да                 | Да                 |
| Windows Server 2012    | SMB 3.0     | Да                 | Да                 |
| Windows Server 2012 R2 | SMB 3.0     | Да                 | Да                 |
| Windows 10             | SMB 3.0     | Да                 | Да                 |

> [!Note]  
> Мы всегда рекомендуем обратиться к самой последней КБ для используемой версии Windows hello.

## <a name="aprerequisites-for-mounting-azure-file-share-with-windows"></a></a>Предварительные требования для подключения общей папки Azure с помощью Windows 
* **Имя учетной записи хранения**: toomount Azure общей папки, будет необходимо hello имя учетной записи хранения hello.

* **Ключ учетной записи хранения**: toomount Azure общей папки, будет необходимо hello ключ хранилища первичный (или вторичная). В настоящее время ключи SAS для подключения не поддерживаются.

* **Откройте порт 445**: хранилище файлов Azure использует протокол SMB. SMB устанавливает соединения через TCP-порт 445 - проверьте toosee, если ваш брандмауэр не блокирует порты TCP 445 с клиентского компьютера.

## <a name="mount-hello-azure-file-share-with-file-explorer"></a>Подключить hello Azure общей папки с помощью проводника
> [!Note]  
> Обратите внимание, что hello в соответствии с инструкциями, отображаются на Windows 10 и могут немного отличаться в предыдущих версиях. 

1. **Откройте проводник**: это можно сделать путем открытия из меню "Пуск" hello, или нажатием сочетания Win + E.

2. **Перейдите в элемент «Этот PC» toohello hello левой стороны окна hello. Это приведет к изменению hello меню на ленте «hello». В меню "компьютер" hello, выберите «Подключение сетевого диска»**.
    
    ![Снимок экрана раскрывающегося меню «Подключение сетевого диска» hello](media/storage-file-how-to-use-files-windows/1_MountOnWindows10.png)

3. **Копировать hello UNC-путь в hello портал Azure в области «Подключиться» hello**: как toofind эти сведения можно найти подробное описание [здесь](storage-file-how-to-use-files-portal.md#connect-to-file-share).

    ![UNC-путь Hello hello Azure хранилища Connect области файла](media/storage-file-how-to-use-files-windows/portal_netuse_connect.png)

4. **Выберите букву диска hello и введите UNC-путь hello.** 
    
    ![Снимок экрана: диалоговое окно «Подключение сетевого диска» hello](media/storage-file-how-to-use-files-windows/2_MountOnWindows10.png)

5. **Используйте hello имя учетной записи хранилища, но с `Azure\` как имя пользователя hello и ключ учетной записи хранения, как пароль hello.**
    
    ![Снимок экрана диалоговое окно приветствия сетевых учетных данных](media/storage-file-how-to-use-files-windows/3_MountOnWindows10.png)

6. **Выберите общую папку Azure**.
    
    ![Общая папка Azure теперь подключена](media/storage-file-how-to-use-files-windows/4_MountOnWindows10.png)

7. **Когда вы готовы toodismount (или отключить) hello Azure общей папки, это можно сделать, щелкнув hello запись для общей папке hello под hello «сеть» в проводнике правой кнопкой мыши и выбрав пункт «Отключить»**.

## <a name="mount-hello-azure-file-share-with-powershell"></a>Подключить hello Azure общей папки с помощью PowerShell
1. **Используйте hello следующая команда toomount hello Azure общей папки**: помните tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` с hello соответствующие сведения.

    ```PowerShell
    $acctKey = ConvertTo-SecureString -String "<storage-account-key>" -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential -ArgumentList "Azure\<storage-account-name>", $acctKey
    New-PSDrive -Name <desired-drive-letter> -PSProvider FileSystem -Root "\\<storage-account-name>.file.core.windows.net\<share-name>" -Credential $credential
    ```

2. **Используйте hello Azure общую папку в случае необходимости**.

3. **Когда вы закончите, отключите hello Azure общую hello следующую команду с помощью**.

    ```PowerShell
    Remove-PSDrive -Name <desired-drive-letter>
    ```

> [!Note]  
> Вы можете использовать hello `-Persist` параметр на `New-PSDrive` toomake hello остальные видимым toohello общую папку файлов Azure hello операционной системы во время монтирования.

## <a name="mount-hello-azure-file-share-with-command-prompt"></a>Подключить hello Azure общей папки с помощью командной строки
1. **Используйте hello следующая команда toomount hello Azure общей папки**: помните tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` с hello соответствующие сведения.

    ```
    net use <desired-drive-letter>: \\<storage-account-name>.file.core.windows.net\<share-name> <storage-account-key> /user:Azure\<storage-account-name>
    ```

2. **Используйте hello Azure общую папку в случае необходимости**.

3. **Когда вы закончите, отключите hello Azure общую hello следующую команду с помощью**.

    ```
    net use <desired-drive-letter>: /delete
    ```

> [!Note]  
> Hello переподключение tooautomatically общую папку файлов Azure можно настроить при перезагрузке путем сохранения учетных данных hello в Windows. Здравствуй, следующая команда будет сохраняться hello учетные данные:
>   ```
>   cmdkey /add:<storage-account-name>.file.core.windows.net /user:AZURE\<storage-account-name> /pass:<storage-account-key>
>   ```

## <a name="next-steps"></a>Дальнейшие действия
Дополнительную информацию о хранилище файлов Azure см. по этим ссылкам.

* [Часто задаваемые вопросы](storage-files-faq.md)
* [Устранение неполадок](storage-troubleshoot-file-connection-problems.md)

### <a name="conceptual-articles-and-videos"></a>Тематические статьи и видео
* [Azure Files Storage: a frictionless cloud SMB file system for Windows and Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/) (Хранилище файлов Azure: удобная облачная файловая система SMB для Windows и Linux)
* [Как toouse хранилища Azure File с Linux](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-azure-file-storage"></a>Поддержка средств для работы с хранилищем файлов Azure
* [Использование Azure PowerShell со службой хранилища Azure](storage-powershell-guide-full.md)
* [Как toouse AzCopy с хранилищем Microsoft Azure](storage-use-azcopy.md)
* [С помощью hello Azure CLI со службой хранилища Azure](storage-azure-cli.md#create-and-manage-file-shares)
* [Устранение неполадок хранилища файлов Azure](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="blog-posts"></a>Записи блога
* [Хранилище файлов Azure стало общедоступным](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [Inside Azure File Storage](https://azure.microsoft.com/blog/inside-azure-file-storage/) (Хранилище файлов Azure: взгляд изнутри)
* [Введение в службы файлов Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [Миграция данных tooAzure файла](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a>Справочные материалы
* [Справочник по клиентской библиотеке хранилища для .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [Справочник по REST API службы файлов](http://msdn.microsoft.com/library/azure/dn167006.aspx)
