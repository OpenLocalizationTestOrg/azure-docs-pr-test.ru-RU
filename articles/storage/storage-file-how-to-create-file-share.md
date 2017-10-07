---
title: "aaaHow toocreate файловый ресурс Azure | Документы Microsoft"
description: "Как toocreate Azure общей папки в хранилище файлов Azure, с помощью hello портал Azure, PowerShell и hello Azure CLI."
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
ms.openlocfilehash: c4c59966b82d743fb4ecf79f48c0c8e61295d03d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-file-share-in-azure-file-storage"></a>Создание общей папки в хранилище файлов Azure
Можно создать общих ресурсов Azure с помощью [портал Azure](https://portal.azure.com/)hello командлеты PowerShell хранилища Azure, hello клиентских библиотек хранилища Azure или hello API REST хранилища Azure. В этом учебнике вы узнаете:
* [Как предоставить доступ toocreate файл Azure с помощью портала Azure hello](#Create file share through hello Portal)
* [Как toocreate Azure общей папки с помощью Powershell](#Create file share using PowerShell)
* [Как toocreate Azure общей папки с использованием интерфейса CLI](#create-file-share-using-command-line-interface-cli)

## <a name="prerequisites"></a>Предварительные требования
toocreate Azure файловый ресурс, можно использовать учетную запись хранения, которая уже существует, или [Создание учетной записи хранилища Azure](storage-create-storage-account.md). toocreate Azure файловый ресурс с помощью PowerShell, потребуется ключ учетной записи hello и имя учетной записи... Если планируется toouse Powershell или интерфейс командной строки, вам потребуется ключ учетной записи хранения.

## <a name="create-file-share-through-hello-portal"></a>Создайте общую папку через портал hello
1. **Колонка учетной записи tooStorage перейдите на портал Azure**:    
    ![Колонка учетной записи хранения](media/storage-file-how-to-create-file-share/create-file-share-portal1.png)

2. **Нажмите кнопку "Общая папка"**:    
    ![Нажмите кнопку hello файл общего ресурса кнопка "Добавить"](media/storage-file-how-to-create-file-share/create-file-share-portal2.png)

3. **Укажите имя и квоту. В настоящее время предусмотрено ограничение квоты — не более 5 ТБ**:    
    ![Укажите имя и нужный квоты для общей папки hello](media/storage-file-how-to-create-file-share/create-file-share-portal3.png)

4. **Просмотрите новую общую папку**: ![просмотр новой общей папки](media/storage-file-how-to-create-file-share/create-file-share-portal4.png)

5. **Отправьте файл**: ![отправка файла](media/storage-file-how-to-create-file-share/create-file-share-portal5.png)

6. **Перейдите в общую папку для управления каталогами и файлами**: ![обзор общей папки](media/storage-file-how-to-create-file-share/create-file-share-portal6.png)


## <a name="create-file-share-through-powershell"></a>Создание общей папки с помощью PowerShell
tooprepare toouse PowerShell, загрузить и установить командлеты Azure PowerShell hello. В разделе [как tooinstall и настройка Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) для hello установить точку и инструкции по установке.

> [!Note]  
> Рекомендуется загрузить и установить или обновить toohello последнюю версию модуля Azure PowerShell.

1. **Создать контекст для учетной записи хранилища и ключ** контекста hello инкапсулирует hello ключ учетной записи хранения имени и учетной записи. Инструкции по копированию ключа учетной записи с [портала Azure](https://portal.azure.com/) см. в разделе [Просмотр и копирование ключей доступа к хранилищу](storage-create-storage-account.md#view-and-copy-storage-access-keys).

    ```powershell
    $storageContext = New-AzureStorageContext <storage-account-name> <storage-account-key>
    ```
    
2. **Создайте новую общую папку**:    
    
    ```powershell
    $share = New-AzureStorageShare logs -Context $storageContext
    ```

> [!Note]  
> Hello имя файлового ресурса общего доступа должны указываться прописными буквами. Дополнительные сведения о присвоении имен общим папкам и файлам см. в статье [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx) (Именование общих ресурсов, каталогов, файлов и метаданных и ссылка на них).

## <a name="create-file-share-through-command-line-interface-cli"></a>Создание общей папки с помощью интерфейса командной строки (CLI)
1. **tooprepare toouse интерфейс командной строки (CLI), загрузите и установите hello Azure CLI.**  
    Дополнительные сведения см. в руководстве по [установке Azure CLI 2.0](/cli/azure/install-az-cli2.md), а также руководстве по [обзору Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).

2. **Создание учетной соединения строки toohello хранилища место toocreate hello папки.**  
    Замените ```<storage-account>``` и ```<resource_group>``` с вашей учетной записи имени и ресурсов группы хранения в следующий пример hello.

   ```azurecli
    current_env_conn_string = $(az storage account show-connection-string -n <storage-account> -g <resource-group> --query 'connectionString' -o tsv)

    if [[ $current_env_conn_string == "" ]]; then  
        echo "Couldn't retrieve hello connection string."
    fi
    ```

3. **Создайте общую папку**.
    ```azurecli
    az storage share create --name files --quota 2048 --connection-string $current_env_conn_string 1 > /dev/null
    ```

## <a name="next-steps"></a>Дальнейшие действия
* [Mount an Azure File share and access the share in Windows](storage-file-how-to-use-files-windows.md) (Подключение файлового ресурса Azure и доступ к нему в Windows)
* [Использование хранилища файлов Azure в Linux](storage-how-to-use-files-linux.md)
* [Mount Azure File share over SMB with macOS](storage-file-how-to-use-files-mac.md) (Использование хранилища файлов Azure с помощью протокола SMB в macOS)

Дополнительную информацию о хранилище файлов Azure см. по этим ссылкам.

* [Часто задаваемые вопросы](storage-files-faq.md)
* [Устранение неполадок](storage-troubleshoot-file-connection-problems.md)