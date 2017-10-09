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
# <a name="move-data-tooand-from-azure-blob-storage-using-python"></a><span data-ttu-id="f2546-103">Tooand перемещения данных из хранилища больших двоичных объектов с помощью Python</span><span class="sxs-lookup"><span data-stu-id="f2546-103">Move data tooand from Azure Blob Storage using Python</span></span>
<span data-ttu-id="f2546-104">В этом разделе описывается toolist, отправка и загрузка больших двоичных объектов с помощью Python API hello.</span><span class="sxs-lookup"><span data-stu-id="f2546-104">This topic describes how toolist, upload, and download blobs using hello Python API.</span></span> <span data-ttu-id="f2546-105">Hello Python API, предоставляемые в Azure SDK вы можете:</span><span class="sxs-lookup"><span data-stu-id="f2546-105">With hello Python API provided in Azure SDK, you can:</span></span>

* <span data-ttu-id="f2546-106">Создание контейнера</span><span class="sxs-lookup"><span data-stu-id="f2546-106">Create a container</span></span>
* <span data-ttu-id="f2546-107">Отправка BLOB-объекта в контейнер</span><span class="sxs-lookup"><span data-stu-id="f2546-107">Upload a blob into a container</span></span>
* <span data-ttu-id="f2546-108">Скачивание больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="f2546-108">Download blobs</span></span>
* <span data-ttu-id="f2546-109">Перечисление hello больших двоичных объектов в контейнере</span><span class="sxs-lookup"><span data-stu-id="f2546-109">List hello blobs in a container</span></span>
* <span data-ttu-id="f2546-110">Удаление большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="f2546-110">Delete a blob</span></span>

<span data-ttu-id="f2546-111">Дополнительные сведения об использовании hello Python API см. в разделе [как tooUse hello службы хранилища больших двоичных объектов из Python](../storage/blobs/storage-python-how-to-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="f2546-111">For more information about using hello Python API, see [How tooUse hello Blob Storage Service from Python](../storage/blobs/storage-python-how-to-use-blob-storage.md).</span></span>

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> <span data-ttu-id="f2546-112">При использовании виртуальной Машины, которая была настроена с помощью сценариев hello, предоставляемые [обработки и анализа данных в виртуальных машинах в Azure](machine-learning-data-science-virtual-machines.md), а затем AzCopy уже установлены на hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="f2546-112">If you are using VM that was set up with hello scripts provided by [Data Science Virtual machines in Azure](machine-learning-data-science-virtual-machines.md), then AzCopy is already installed on hello VM.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="f2546-113">Хранилище больших двоичных объектов tooAzure подробное введение, см. в разделе слишком[основы больших двоичных объектов Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) и слишком[больших двоичных объектов Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="f2546-113">For a complete introduction tooAzure blob storage, refer too[Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and too[Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="f2546-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f2546-114">Prerequisites</span></span>
<span data-ttu-id="f2546-115">В этом документе предполагается, что подписка Azure, учетная запись хранения и hello соответствующий ключ хранилища для этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="f2546-115">This document assumes that you have an Azure subscription, a storage account, and hello corresponding storage key for that account.</span></span> <span data-ttu-id="f2546-116">Чтобы отправлять и скачивать данные, необходимо знать имя учетной записи хранения Azure и ее ключ.</span><span class="sxs-lookup"><span data-stu-id="f2546-116">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="f2546-117">tooset копирование подписку Azure, см. [бесплатной пробной версии один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f2546-117">tooset up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="f2546-118">Инструкции по созданию учетной записи хранения и получению сведений об учетной записи и ключах см. в статье [Об учетных записях хранения Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="f2546-118">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

## <a name="upload-data-tooblob"></a><span data-ttu-id="f2546-119">Отправка данных tooBlob</span><span class="sxs-lookup"><span data-stu-id="f2546-119">Upload Data tooBlob</span></span>
<span data-ttu-id="f2546-120">Добавьте следующий фрагмент кода hello верхней части любого кода Python, в котором вы хотите tooprogrammatically доступа хранилища Azure hello:</span><span class="sxs-lookup"><span data-stu-id="f2546-120">Add hello following snippet near hello top of any Python code in which you wish tooprogrammatically access Azure Storage:</span></span>

    from azure.storage.blob import BlobService

<span data-ttu-id="f2546-121">Hello **BlobService** объектов позволяет работать с контейнерами и BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="f2546-121">hello **BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="f2546-122">Привет, следующий код создает объект BlobService, используя hello ключ учетной записи хранения имени и учетной записи.</span><span class="sxs-lookup"><span data-stu-id="f2546-122">hello following code creates a BlobService object using hello storage account name and account key.</span></span> <span data-ttu-id="f2546-123">Замените имя учетной записи и ее ключ фактическими значениями.</span><span class="sxs-lookup"><span data-stu-id="f2546-123">Replace account name and account key with your real account and key.</span></span>

    blob_service = BlobService(account_name="<your_account_name>", account_key="<your_account_key>")

<span data-ttu-id="f2546-124">Используйте следующие методы tooupload данных tooa blob hello.</span><span class="sxs-lookup"><span data-stu-id="f2546-124">Use hello following methods tooupload data tooa blob:</span></span>

1. <span data-ttu-id="f2546-125">Поместите\_блок\_большого двоичного объекта\_из\_пути (загружает содержимое файла из указанного пути hello hello)</span><span class="sxs-lookup"><span data-stu-id="f2546-125">put\_block\_blob\_from\_path (uploads hello contents of a file from hello specified path)</span></span>
2. <span data-ttu-id="f2546-126">Поместите\_block_blob\_из\_файла (загружает содержимое hello из уже открытого файла или потока)</span><span class="sxs-lookup"><span data-stu-id="f2546-126">put\_block_blob\_from\_file (uploads hello contents from an already opened file/stream)</span></span>
3. <span data-ttu-id="f2546-127">put\_block\_blob\_from\_bytes (отправка массива байтов).</span><span class="sxs-lookup"><span data-stu-id="f2546-127">put\_block\_blob\_from\_bytes (uploads an array of bytes)</span></span>
4. <span data-ttu-id="f2546-128">Поместите\_блок\_больших двоичных объектов\_из\_текст (передает указанный hello указанное текстовое значение, с помощью hello кодирование)</span><span class="sxs-lookup"><span data-stu-id="f2546-128">put\_block\_blob\_from\_text (uploads hello specified text value using hello specified encoding)</span></span>

<span data-ttu-id="f2546-129">Следующий пример кода Hello отправляет контейнер tooa локальный файл:</span><span class="sxs-lookup"><span data-stu-id="f2546-129">hello following sample code uploads a local file tooa container:</span></span>

    blob_service.put_block_blob_from_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

<span data-ttu-id="f2546-130">Hello следующий код передает все hello файлы (за исключением каталоги) в хранилище локального каталога tooblob:</span><span class="sxs-lookup"><span data-stu-id="f2546-130">hello following sample code uploads all hello files (excluding directories) in a local directory tooblob storage:</span></span>

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


## <a name="download-data-from-blob"></a><span data-ttu-id="f2546-131">Скачивание данных из большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="f2546-131">Download Data from Blob</span></span>
<span data-ttu-id="f2546-132">Используйте следующие методы toodownload данные из большого двоичного объекта hello.</span><span class="sxs-lookup"><span data-stu-id="f2546-132">Use hello following methods toodownload data from a blob:</span></span>

1. <span data-ttu-id="f2546-133">get\_blob\_to\_path.</span><span class="sxs-lookup"><span data-stu-id="f2546-133">get\_blob\_to\_path</span></span>
2. <span data-ttu-id="f2546-134">get\_blob\_to\_file.</span><span class="sxs-lookup"><span data-stu-id="f2546-134">get\_blob\_to\_file</span></span>
3. <span data-ttu-id="f2546-135">get\_blob\_to\_bytes.</span><span class="sxs-lookup"><span data-stu-id="f2546-135">get\_blob\_to\_bytes</span></span>
4. <span data-ttu-id="f2546-136">get\_blob\_to\_text.</span><span class="sxs-lookup"><span data-stu-id="f2546-136">get\_blob\_to\_text</span></span>

<span data-ttu-id="f2546-137">Эти методы, выполняющие hello необходимые фрагментации hello размер данных hello превышает 64 МБ.</span><span class="sxs-lookup"><span data-stu-id="f2546-137">These methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="f2546-138">Hello следующий код загружает hello содержимое большого двоичного объекта в локальном файле tooa контейнера:</span><span class="sxs-lookup"><span data-stu-id="f2546-138">hello following sample code downloads hello contents of a blob in a container tooa local file:</span></span>

    blob_service.get_blob_to_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

<span data-ttu-id="f2546-139">Hello следующий код загружает все большие двоичные объекты из контейнера.</span><span class="sxs-lookup"><span data-stu-id="f2546-139">hello following sample code downloads all blobs from a container.</span></span> <span data-ttu-id="f2546-140">Он использует список\_большие двоичные объекты tooget hello список доступных большие двоичные объекты в контейнере hello и загружает их tooa локальный каталог.</span><span class="sxs-lookup"><span data-stu-id="f2546-140">It uses list\_blobs tooget hello list of available blobs in hello container and downloads them tooa local directory.</span></span>

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
