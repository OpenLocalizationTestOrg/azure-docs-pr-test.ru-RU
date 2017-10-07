---
title: "aaaHow toouse PowerShell toomanage хранилища Azure File | Документы Microsoft"
description: "Узнайте хранилища Azure File toomanage toouse PowerShell."
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
ms.openlocfilehash: 7bd84c9cfa31782aedf4a209cb15d4b8d92e2737
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-powershell-toomanage-azure-file-storage"></a>Как toomanage toouse PowerShell хранилища Azure File
Можно использовать toocreate Azure PowerShell и управлять общими папками.

## <a name="install-hello-powershell-cmdlets-for-azure-storage"></a>Установка командлетов PowerShell hello для хранилища Azure
tooprepare toouse PowerShell, загрузить и установить командлеты Azure PowerShell hello. В разделе [как tooinstall и настройка Azure PowerShell](/powershell/azureps-cmdlets-docs) для hello установить точку и инструкции по установке.

> [!NOTE]
> Рекомендуется загрузить и установить или обновить toohello последнюю версию модуля Azure PowerShell.
> 
> 

Откройте окно Azure PowerShell. Для этого нажмите кнопку **Запустить** и введите **Windows PowerShell**. окно PowerShell Hello загружает hello модуля Azure Powershell.

## <a name="create-a-context-for-your-storage-account-and-key"></a>Создание объекта контекста и ключа для учетной записи хранения
Создайте hello контекста учетной записи хранилища. контекст Hello инкапсулирует hello ключ учетной записи хранения имени и учетной записи. Инструкции по копированию ключ учетной записи из hello [портал Azure](https://portal.azure.com), в разделе [представление и скопируйте ключи доступа к хранилищу](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys).

Замените `storage-account-name` и `storage-account-key` с помощью имени учетной записи хранилища и ключ в следующий пример hello.

```powershell
# create a context for account and key
$ctx=New-AzureStorageContext storage-account-name storage-account-key
```

## <a name="create-a-new-file-share"></a>Создание нового ресурса совместно используемых файлов
Создание нового ресурса hello, с именем `logs`.

```powershell
# create a new share
$s = New-AzureStorageShare logs -Context $ctx
```

У вас появится новый общий ресурс в хранилище файлов. Далее мы добавим каталог и файл.

> [!IMPORTANT]
> Hello имя файлового ресурса общего доступа должны указываться прописными буквами. Дополнительные сведения о присвоении имен общим папкам и файлам см. в статье [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx) (Именование общих ресурсов, каталогов, файлов и метаданных и ссылка на них).
> 
> 

## <a name="create-a-directory-in-hello-file-share"></a>Создайте каталог в общей папке hello
Создайте каталог в общей папке hello. В следующем примере hello, hello каталог `CustomLogs`.

```powershell
# create a directory in hello share
New-AzureStorageDirectory -Share $s -Path CustomLogs
```

## <a name="upload-a-local-file-toohello-directory"></a>Отправка toohello каталог локального файла
Теперь отправьте toohello каталог локального файла. Hello следующий пример отправляет файл из `C:\temp\Log1.txt`. Измените путь к файлу hello, которое указывает допустимый файл tooa на локальном компьютере.

```powershell
# upload a local file toohello new directory
Set-AzureStorageFileContent -Share $s -Source C:\temp\Log1.txt -Path CustomLogs
```

## <a name="list-hello-files-in-hello-directory"></a>Список файлов в каталоге hello, hello
toosee hello файл в каталоге hello, можно составить список всех файлов каталога hello. Эта команда возвращает hello файлы и подкаталоги (если таковые имеются) в каталоге CustomLogs hello.

```powershell
# list files in hello new directory
Get-AzureStorageFile -Share $s -Path CustomLogs | Get-AzureStorageFile
```

Get-AzureStorageFile возвращает список файлов и каталогов в каталоге, в который отправлен объект. «Get-AzureStorageFile-совместное использование $s» возвращает список файлов и каталогов в корневой каталог hello. tooget список файлов в подкаталоге, у вас есть hello подкаталог toopass tooGet-AzureStorageFile. При этом произойдет — первая часть команды hello канала toohello hello возвращает экземпляр directory hello подкаталог CustomLogs. Затем, передается в Get-AzureStorageFile, который возвращает hello файлов и каталогов в CustomLogs.

## <a name="copy-files"></a>Копирование файлов
Начиная с версии 0.9.7 Azure PowerShell, можно скопировать файл tooanother, большой двоичный объект файла tooa или tooa файла большого двоичного объекта. Ниже показано как tooperform их копирования операции с помощью командлетов PowerShell.

```powershell
# copy a file toohello new directory
Start-AzureStorageFileCopy -SrcShareName srcshare -SrcFilePath srcdir/hello.txt -DestShareName destshare -DestFilePath destdir/hellocopy.txt -Context $srcCtx -DestContext $destCtx

# copy a blob tooa file directory
Start-AzureStorageFileCopy -SrcContainerName srcctn -SrcBlobName hello2.txt -DestShareName hello -DestFilePath hellodir/hello2copy.txt -DestContext $ctx -Context $ctx
```
## <a name="next-steps"></a>Дальнейшие действия
Дополнительную информацию о хранилище файлов Azure см. по этим ссылкам.

* [Часто задаваемые вопросы](../storage-files-faq.md)
* [Troubleshoot Azure File storage problems in Windows](storage-troubleshoot-windows-file-connection-problems.md) (Устранение неполадок хранилища файлов Azure в Windows)      
* [Troubleshoot Azure File storage problems in Linux](storage-troubleshoot-linux-file-connection-problems.md) (Устранение неполадок хранилища файлов Azure в Linux)    