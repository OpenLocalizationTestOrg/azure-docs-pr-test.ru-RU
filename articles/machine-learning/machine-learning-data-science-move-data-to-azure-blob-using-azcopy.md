---
title: "aaaMove tooand данных из хранилища больших двоичных объектов с помощью AzCopy | Документы Microsoft"
description: "Tooand перемещения данных из хранилища больших двоичных объектов с помощью AzCopy"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: c309ceb2-0e83-4a07-b16d-c997dcd62d5c
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: b381ba004ac16879b6c633950d03d13ad82d5b72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage-using-azcopy"></a>Tooand перемещения данных из хранилища больших двоичных объектов с помощью AzCopy
AzCopy является командной строки служебная программа, разработанная для передача, загрузка и копирование tooand данных из больших двоичных объектов Microsoft Azure, файл и хранилище таблиц.

Инструкции по установке на его использование с hello платформы Azure AzCopy и Дополнительные сведения см. в разделе [Приступая к работе с hello служебной программы командной строки AzCopy](../storage/common/storage-use-azcopy.md).

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> При использовании виртуальной Машины, которая была настроена с помощью сценариев hello, предоставляемые [обработки и анализа данных в виртуальных машинах в Azure](machine-learning-data-science-virtual-machines.md), а затем AzCopy уже установлены на hello виртуальной Машины.
> 
> [!NOTE]
> Хранилище больших двоичных объектов tooAzure подробное введение, см. в разделе слишком[основы больших двоичных объектов Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) и слишком[больших двоичных объектов Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).
> 
> 

## <a name="prerequisites"></a>Предварительные требования
В этом документе предполагается, что есть подписка Azure, учетная запись хранения и hello соответствующий ключ хранилища для этой учетной записи. Чтобы отправлять и скачивать данные, необходимо знать имя учетной записи хранения Azure и ее ключ.

* tooset копирование подписку Azure, см. [бесплатной пробной версии один месяц](https://azure.microsoft.com/pricing/free-trial/).
* Инструкции по созданию учетной записи хранения и получению сведений об учетной записи и ключах см. в статье [Об учетных записях хранения Azure](../storage/common/storage-create-storage-account.md).

## <a name="run-azcopy-commands"></a>Выполнение команд AzCopy
команды AzCopy toorun, откройте окно командной строки и перейдите в каталог установки AzCopy toohello на компьютере, где находится исполняемый файл AzCopy.exe hello. 

Базовый синтаксис команды AzCopy Hello таков:

    AzCopy /Source:<source> /Dest:<destination> [Options]

> [!NOTE]
> Можно добавить hello AzCopy tooyour системы путь установки и выполнить команды hello из любого каталога. По умолчанию AzCopy установлен слишком*% ProgramFiles (x86) %\Microsoft SDKs\Azure\AzCopy* или *%ProgramFiles%\Microsoft SDKs\Azure\AzCopy*.
> 
> 

## <a name="upload-files-tooan-azure-blob"></a>Отправка файлов tooan BLOB-объектов Azure
tooupload файл hello используйте следующую команду:

    # Upload from local file system
    AzCopy /Source:<your_local_directory> /Dest: https://<your_account_name>.blob.core.windows.net/<your_container_name> /DestKey:<your_account_key> /S


## <a name="download-files-from-an-azure-blob"></a>Скачивание файлов из большого двоичного объекта Azure
toodownload файл из BLOB-объекта Azure, hello используйте следующую команду:

    # Downloading blobs toolocal file system
    AzCopy /Source:https://<your_account_name>.blob.core.windows.net/<your_container_name>/<your_sub_directory_at_blob>  /Dest:<your_local_directory> /SourceKey:<your_account_key> /Pattern:<file_pattern> /S


## <a name="transfer-blobs-between-azure-containers"></a>Передача больших двоичных объектов между контейнерами Azure
tootransfer больших двоичных объектов между контейнерами Azure, используйте hello следующую команду:

    # Transferring blobs between Azure containers
    AzCopy /Source:https://<your_account_name1>.blob.core.windows.net/<your_container_name1>/<your_sub_directory_at_blob1> /Dest:https://<your_account_name2>.blob.core.windows.net/<your_container_name2>/<your_sub_directory_at_blob2> /SourceKey:<your_account_key1> /DestKey:<your_account_key2> /Pattern:<file_pattern> /S

    <your_account_name>: your storage account name
    <your_account_key>: your storage account key
    <your_container_name>: your container name
    <your_sub_directory_at_blob>: hello sub directory in hello container
    <your_local_directory>: directory of local file system where files toobe uploaded from or hello directory of local file system files toobe downloaded to
    <file_pattern>: pattern of file names toobe transferred. hello standard wildcards are supported


## <a name="tips-for-using-azcopy"></a>Советы по использованию AzCopy
> [!TIP]
> 1. При **отправке** с параметром */S* файлы отправляются рекурсивно. Без этого параметра файлы из подкаталогов не отправляются.  
> 2. Когда **Загрузка** файла, */S* поиск hello контейнера рекурсивно, пока все файлы в указанном каталоге hello и его подкаталогах или Здравствуйте, всех файлов, соответствующих заданному шаблону в заданный hello загружаются каталоге и его подкаталогах.  
> 3. Нельзя указать **файл определенным BLOB-объектом** toodownload, с помощью hello */Source* параметра. toodownload конкретного файла, укажите с помощью hello имя toodownload hello большого двоичного объекта файла */шаблона* параметра. **/S** параметр может иметь вид AzCopy используется toohave рекурсивно шаблон, имя файла. Без параметра pattern hello AzCopy загружает все файлы в этом каталоге.
> 
> 

