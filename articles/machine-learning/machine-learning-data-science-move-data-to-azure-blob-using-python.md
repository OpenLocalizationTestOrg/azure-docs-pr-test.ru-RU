---
title: "Перемещение данных в хранилище BLOB-объектов Azure и из него с помощью Python | Документация Майкрософт"
description: "Перемещение данных в хранилище больших двоичных объектов Azure и из него с помощью Python"
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
ms.openlocfilehash: 0eea1ff8e4f4c1d108445e1a1250b6fa8ff48910
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-to-and-from-azure-blob-storage-using-python"></a><span data-ttu-id="e6c3c-103">Перемещение данных в хранилище BLOB-объектов Azure и из него с помощью Python</span><span class="sxs-lookup"><span data-stu-id="e6c3c-103">Move data to and from Azure Blob Storage using Python</span></span>
<span data-ttu-id="e6c3c-104">В этой статье описывается получение списка, отправка и скачивание больших двоичных объектов с помощью API Python.</span><span class="sxs-lookup"><span data-stu-id="e6c3c-104">This topic describes how to list, upload, and download blobs using the Python API.</span></span> <span data-ttu-id="e6c3c-105">API на языке Python, предоставляемый с пакетом SDK для Azure, обеспечивает следующие возможности:</span><span class="sxs-lookup"><span data-stu-id="e6c3c-105">With the Python API provided in Azure SDK, you can:</span></span>

* <span data-ttu-id="e6c3c-106">Создание контейнера</span><span class="sxs-lookup"><span data-stu-id="e6c3c-106">Create a container</span></span>
* <span data-ttu-id="e6c3c-107">Отправка BLOB-объекта в контейнер</span><span class="sxs-lookup"><span data-stu-id="e6c3c-107">Upload a blob into a container</span></span>
* <span data-ttu-id="e6c3c-108">Скачивание больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="e6c3c-108">Download blobs</span></span>
* <span data-ttu-id="e6c3c-109">Перечисление BLOB-объектов в контейнере</span><span class="sxs-lookup"><span data-stu-id="e6c3c-109">List the blobs in a container</span></span>
* <span data-ttu-id="e6c3c-110">Удаление большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="e6c3c-110">Delete a blob</span></span>

<span data-ttu-id="e6c3c-111">Дополнительные сведения об использовании Python API см. в статье [Использование хранилища BLOB-объектов Azure из Python](../storage/blobs/storage-python-how-to-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="e6c3c-111">For more information about using the Python API, see [How to Use the Blob Storage Service from Python](../storage/blobs/storage-python-how-to-use-blob-storage.md).</span></span>

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> <span data-ttu-id="e6c3c-112">Если используется виртуальная машина, созданная с помощью скриптов, предоставленных [виртуальными машинами для обработки и анализа данных в Azure](machine-learning-data-science-virtual-machines.md), то программа AzCopy уже установлена на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="e6c3c-112">If you are using VM that was set up with the scripts provided by [Data Science Virtual machines in Azure](machine-learning-data-science-virtual-machines.md), then AzCopy is already installed on the VM.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="e6c3c-113">Полное описание базовых принципов использования хранилища BLOB-объектов Azure см. в статьях [Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) и [Основные понятия службы BLOB-объектов](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="e6c3c-113">For a complete introduction to Azure blob storage, refer to [Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and to [Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="e6c3c-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e6c3c-114">Prerequisites</span></span>
<span data-ttu-id="e6c3c-115">Для выполнения указаний в этом документе у вас должна быть подписка Azure, учетная запись хранения и соответствующий ключ к хранилищу данных для этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="e6c3c-115">This document assumes that you have an Azure subscription, a storage account, and the corresponding storage key for that account.</span></span> <span data-ttu-id="e6c3c-116">Чтобы отправлять и скачивать данные, необходимо знать имя учетной записи хранения Azure и ее ключ.</span><span class="sxs-lookup"><span data-stu-id="e6c3c-116">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="e6c3c-117">Сведения о настройке подписки Azure см. на странице [Создайте бесплатную учетную запись Azure уже сегодня](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e6c3c-117">To set up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="e6c3c-118">Инструкции по созданию учетной записи хранения и получению сведений об учетной записи и ключах см. в статье [Об учетных записях хранения Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="e6c3c-118">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

## <a name="upload-data-to-blob"></a><span data-ttu-id="e6c3c-119">Отправка данных в большой двоичный объект</span><span class="sxs-lookup"><span data-stu-id="e6c3c-119">Upload Data to Blob</span></span>
<span data-ttu-id="e6c3c-120">Добавьте следующий фрагмент кода в начало любого кода Python, из которого планируется получать доступ к службе хранилища Azure программным способом:</span><span class="sxs-lookup"><span data-stu-id="e6c3c-120">Add the following snippet near the top of any Python code in which you wish to programmatically access Azure Storage:</span></span>

    from azure.storage.blob import BlobService

<span data-ttu-id="e6c3c-121">Объект **BlobService** позволяет работать с контейнерами и BLOB-объектами.</span><span class="sxs-lookup"><span data-stu-id="e6c3c-121">The **BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="e6c3c-122">Следующий код создает объект BlobService, используя имя и ключ учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="e6c3c-122">The following code creates a BlobService object using the storage account name and account key.</span></span> <span data-ttu-id="e6c3c-123">Замените имя учетной записи и ее ключ фактическими значениями.</span><span class="sxs-lookup"><span data-stu-id="e6c3c-123">Replace account name and account key with your real account and key.</span></span>

    blob_service = BlobService(account_name="<your_account_name>", account_key="<your_account_key>")

<span data-ttu-id="e6c3c-124">Используйте следующие методы для отправки данных в большой двоичный объект:</span><span class="sxs-lookup"><span data-stu-id="e6c3c-124">Use the following methods to upload data to a blob:</span></span>

1. <span data-ttu-id="e6c3c-125">put\_block\_blob\_from\_path (отправка содержимого файла из указанного пути).</span><span class="sxs-lookup"><span data-stu-id="e6c3c-125">put\_block\_blob\_from\_path (uploads the contents of a file from the specified path)</span></span>
2. <span data-ttu-id="e6c3c-126">put\_block_blob\_from\_file (отправка содержимого открытого файла или потока).</span><span class="sxs-lookup"><span data-stu-id="e6c3c-126">put\_block_blob\_from\_file (uploads the contents from an already opened file/stream)</span></span>
3. <span data-ttu-id="e6c3c-127">put\_block\_blob\_from\_bytes (отправка массива байтов).</span><span class="sxs-lookup"><span data-stu-id="e6c3c-127">put\_block\_blob\_from\_bytes (uploads an array of bytes)</span></span>
4. <span data-ttu-id="e6c3c-128">put\_block\_blob\_from\_text (отправка указанного текстового значения с использованием указанной кодировки).</span><span class="sxs-lookup"><span data-stu-id="e6c3c-128">put\_block\_blob\_from\_text (uploads the specified text value using the specified encoding)</span></span>

<span data-ttu-id="e6c3c-129">Следующий пример кода отправляет локальный файл в контейнер:</span><span class="sxs-lookup"><span data-stu-id="e6c3c-129">The following sample code uploads a local file to a container:</span></span>

    blob_service.put_block_blob_from_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

<span data-ttu-id="e6c3c-130">Следующий пример кода отправляет все файлы (за исключением каталогов) в локальном каталоге в хранилище больших двоичных объектов:</span><span class="sxs-lookup"><span data-stu-id="e6c3c-130">The following sample code uploads all the files (excluding directories) in a local directory to blob storage:</span></span>

    from azure.storage.blob import BlobService
    from os import listdir
    from os.path import isfile, join

    # Set parameters here
    ACCOUNT_NAME = "<your_account_name>"
    ACCOUNT_KEY = "<your_account_key>"
    CONTAINER_NAME = "<your_container_name>"
    LOCAL_DIRECT = "<your_local_directory>"        

    blob_service = BlobService(account_name=ACCOUNT_NAME, account_key=ACCOUNT_KEY)
    # find all files in the LOCAL_DIRECT (excluding directory)
    local_file_list = [f for f in listdir(LOCAL_DIRECT) if isfile(join(LOCAL_DIRECT, f))]

    file_num = len(local_file_list)
    for i in range(file_num):
        local_file = join(LOCAL_DIRECT, local_file_list[i])
        blob_name = local_file_list[i]
        try:
            blob_service.put_block_blob_from_path(CONTAINER_NAME, blob_name, local_file)
        except:
            print "something wrong happened when uploading the data %s"%blob_name


## <a name="download-data-from-blob"></a><span data-ttu-id="e6c3c-131">Скачивание данных из большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="e6c3c-131">Download Data from Blob</span></span>
<span data-ttu-id="e6c3c-132">Чтобы скачать данные из большого двоичного объекта, используйте следующие методы:</span><span class="sxs-lookup"><span data-stu-id="e6c3c-132">Use the following methods to download data from a blob:</span></span>

1. <span data-ttu-id="e6c3c-133">get\_blob\_to\_path.</span><span class="sxs-lookup"><span data-stu-id="e6c3c-133">get\_blob\_to\_path</span></span>
2. <span data-ttu-id="e6c3c-134">get\_blob\_to\_file.</span><span class="sxs-lookup"><span data-stu-id="e6c3c-134">get\_blob\_to\_file</span></span>
3. <span data-ttu-id="e6c3c-135">get\_blob\_to\_bytes.</span><span class="sxs-lookup"><span data-stu-id="e6c3c-135">get\_blob\_to\_bytes</span></span>
4. <span data-ttu-id="e6c3c-136">get\_blob\_to\_text.</span><span class="sxs-lookup"><span data-stu-id="e6c3c-136">get\_blob\_to\_text</span></span>

<span data-ttu-id="e6c3c-137">Это методы, которые выполняют необходимое фрагментирование данных, если их размер превышает 64 МБ.</span><span class="sxs-lookup"><span data-stu-id="e6c3c-137">These methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="e6c3c-138">Следующий пример кода скачивает содержимое большого двоичного объекта в контейнере в локальный файл:</span><span class="sxs-lookup"><span data-stu-id="e6c3c-138">The following sample code downloads the contents of a blob in a container to a local file:</span></span>

    blob_service.get_blob_to_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

<span data-ttu-id="e6c3c-139">Следующий пример кода скачивает все большие двоичные объекты в контейнере.</span><span class="sxs-lookup"><span data-stu-id="e6c3c-139">The following sample code downloads all blobs from a container.</span></span> <span data-ttu-id="e6c3c-140">Он использует метод list\_blobs для получения списка больших двоичных объектов, доступных в контейнере, и скачивает их в локальный каталог.</span><span class="sxs-lookup"><span data-stu-id="e6c3c-140">It uses list\_blobs to get the list of available blobs in the container and downloads them to a local directory.</span></span>

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
            print "something wrong happened when downloading the data %s"%blob.name
