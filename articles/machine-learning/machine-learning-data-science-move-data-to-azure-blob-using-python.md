---
title: "aaaMove tooand данных из хранилища больших двоичных объектов с помощью Python | Документы Microsoft"
description: "Tooand перемещения данных из хранилища больших двоичных объектов с помощью Python"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 24276252-b3dd-4edf-9e5d-f6803f8ccccc
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: c2be9600e0d6cb05bcf4109a8d554db522704ecb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage-using-python"></a>Tooand перемещения данных из хранилища больших двоичных объектов с помощью Python
В этом разделе описывается toolist, отправка и загрузка больших двоичных объектов с помощью Python API hello. Hello Python API, предоставляемые в Azure SDK вы можете:

* Создание контейнера
* Отправка BLOB-объекта в контейнер
* Скачивание больших двоичных объектов
* Перечисление hello больших двоичных объектов в контейнере
* Удаление большого двоичного объекта

Дополнительные сведения об использовании hello Python API см. в разделе [как tooUse hello службы хранилища больших двоичных объектов из Python](../storage/blobs/storage-python-how-to-use-blob-storage.md).

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> При использовании виртуальной Машины, которая была настроена с помощью сценариев hello, предоставляемые [обработки и анализа данных в виртуальных машинах в Azure](machine-learning-data-science-virtual-machines.md), а затем AzCopy уже установлены на hello виртуальной Машины.
> 
> [!NOTE]
> Хранилище больших двоичных объектов tooAzure подробное введение, см. в разделе слишком[основы больших двоичных объектов Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) и слишком[больших двоичных объектов Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).
> 
> 

## <a name="prerequisites"></a>Предварительные требования
В этом документе предполагается, что подписка Azure, учетная запись хранения и hello соответствующий ключ хранилища для этой учетной записи. Чтобы отправлять и скачивать данные, необходимо знать имя учетной записи хранения Azure и ее ключ.

* tooset копирование подписку Azure, см. [бесплатной пробной версии один месяц](https://azure.microsoft.com/pricing/free-trial/).
* Инструкции по созданию учетной записи хранения и получению сведений об учетной записи и ключах см. в статье [Об учетных записях хранения Azure](../storage/common/storage-create-storage-account.md).

## <a name="upload-data-tooblob"></a>Отправка данных tooBlob
Добавьте следующий фрагмент кода hello верхней части любого кода Python, в котором вы хотите tooprogrammatically доступа хранилища Azure hello:

    from azure.storage.blob import BlobService

Hello **BlobService** объектов позволяет работать с контейнерами и BLOB-объектов. Привет, следующий код создает объект BlobService, используя hello ключ учетной записи хранения имени и учетной записи. Замените имя учетной записи и ее ключ фактическими значениями.

    blob_service = BlobService(account_name="<your_account_name>", account_key="<your_account_key>")

Используйте следующие методы tooupload данных tooa blob hello.

1. Поместите\_блок\_большого двоичного объекта\_из\_пути (загружает содержимое файла из указанного пути hello hello)
2. Поместите\_block_blob\_из\_файла (загружает содержимое hello из уже открытого файла или потока)
3. put\_block\_blob\_from\_bytes (отправка массива байтов).
4. Поместите\_блок\_больших двоичных объектов\_из\_текст (передает указанный hello указанное текстовое значение, с помощью hello кодирование)

Следующий пример кода Hello отправляет контейнер tooa локальный файл:

    blob_service.put_block_blob_from_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

Hello следующий код передает все hello файлы (за исключением каталоги) в хранилище локального каталога tooblob:

    from azure.storage.blob import BlobService
    from os import listdir
    from os.path import isfile, join

    # Set parameters here
    ACCOUNT_NAME = "<your_account_name>"
    ACCOUNT_KEY = "<your_account_key>"
    CONTAINER_NAME = "<your_container_name>"
    LOCAL_DIRECT = "<your_local_directory>"        

    blob_service = BlobService(account_name=ACCOUNT_NAME, account_key=ACCOUNT_KEY)
    # find all files in hello LOCAL_DIRECT (excluding directory)
    local_file_list = [f for f in listdir(LOCAL_DIRECT) if isfile(join(LOCAL_DIRECT, f))]

    file_num = len(local_file_list)
    for i in range(file_num):
        local_file = join(LOCAL_DIRECT, local_file_list[i])
        blob_name = local_file_list[i]
        try:
            blob_service.put_block_blob_from_path(CONTAINER_NAME, blob_name, local_file)
        except:
            print "something wrong happened when uploading hello data %s"%blob_name


## <a name="download-data-from-blob"></a>Скачивание данных из большого двоичного объекта
Используйте следующие методы toodownload данные из большого двоичного объекта hello.

1. get\_blob\_to\_path.
2. get\_blob\_to\_file.
3. get\_blob\_to\_bytes.
4. get\_blob\_to\_text.

Эти методы, выполняющие hello необходимые фрагментации hello размер данных hello превышает 64 МБ.

Hello следующий код загружает hello содержимое большого двоичного объекта в локальном файле tooa контейнера:

    blob_service.get_blob_to_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

Hello следующий код загружает все большие двоичные объекты из контейнера. Он использует список\_большие двоичные объекты tooget hello список доступных большие двоичные объекты в контейнере hello и загружает их tooa локальный каталог.

    from azure.storage.blob import BlobService
    from os.path import join

    # Set parameters here
    ACCOUNT_NAME = "<your_account_name>"
    ACCOUNT_KEY = "<your_account_key>"
    CONTAINER_NAME = "<your_container_name>"
    LOCAL_DIRECT = "<your_local_directory>"        

    blob_service = BlobService(account_name=ACCOUNT_NAME, account_key=ACCOUNT_KEY)

    # List all blobs and download them one by one
    blobs = blob_service.list_blobs(CONTAINER_NAME)
    for blob in blobs:
        local_file = join(LOCAL_DIRECT, blob.name)
        try:
            blob_service.get_blob_to_path(CONTAINER_NAME, blob.name, local_file)
        except:
            print "something wrong happened when downloading hello data %s"%blob.name
