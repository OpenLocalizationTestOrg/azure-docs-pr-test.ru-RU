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
# <a name="move-data-tooand-from-azure-blob-storage-using-azcopy"></a><span data-ttu-id="84141-103">Tooand перемещения данных из хранилища больших двоичных объектов с помощью AzCopy</span><span class="sxs-lookup"><span data-stu-id="84141-103">Move data tooand from Azure Blob Storage using AzCopy</span></span>
<span data-ttu-id="84141-104">AzCopy является командной строки служебная программа, разработанная для передача, загрузка и копирование tooand данных из больших двоичных объектов Microsoft Azure, файл и хранилище таблиц.</span><span class="sxs-lookup"><span data-stu-id="84141-104">AzCopy is a command-line utility designed for uploading, downloading, and copying data tooand from Microsoft Azure blob, file, and table storage.</span></span>

<span data-ttu-id="84141-105">Инструкции по установке на его использование с hello платформы Azure AzCopy и Дополнительные сведения см. в разделе [Приступая к работе с hello служебной программы командной строки AzCopy](../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="84141-105">For instructions on installing AzCopy and additional information on using it with hello Azure platform, see [Getting Started with hello AzCopy Command-Line Utility](../storage/common/storage-use-azcopy.md).</span></span>

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> <span data-ttu-id="84141-106">При использовании виртуальной Машины, которая была настроена с помощью сценариев hello, предоставляемые [обработки и анализа данных в виртуальных машинах в Azure](machine-learning-data-science-virtual-machines.md), а затем AzCopy уже установлены на hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="84141-106">If you are using VM that was set up with hello scripts provided by [Data Science Virtual machines in Azure](machine-learning-data-science-virtual-machines.md), then AzCopy is already installed on hello VM.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="84141-107">Хранилище больших двоичных объектов tooAzure подробное введение, см. в разделе слишком[основы больших двоичных объектов Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) и слишком[больших двоичных объектов Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="84141-107">For a complete introduction tooAzure blob storage, refer too[Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and too[Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="84141-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="84141-108">Prerequisites</span></span>
<span data-ttu-id="84141-109">В этом документе предполагается, что есть подписка Azure, учетная запись хранения и hello соответствующий ключ хранилища для этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="84141-109">This document assumes that you have an Azure subscription, a storage account and hello corresponding storage key for that account.</span></span> <span data-ttu-id="84141-110">Чтобы отправлять и скачивать данные, необходимо знать имя учетной записи хранения Azure и ее ключ.</span><span class="sxs-lookup"><span data-stu-id="84141-110">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="84141-111">tooset копирование подписку Azure, см. [бесплатной пробной версии один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="84141-111">tooset up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="84141-112">Инструкции по созданию учетной записи хранения и получению сведений об учетной записи и ключах см. в статье [Об учетных записях хранения Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="84141-112">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

## <a name="run-azcopy-commands"></a><span data-ttu-id="84141-113">Выполнение команд AzCopy</span><span class="sxs-lookup"><span data-stu-id="84141-113">Run AzCopy commands</span></span>
<span data-ttu-id="84141-114">команды AzCopy toorun, откройте окно командной строки и перейдите в каталог установки AzCopy toohello на компьютере, где находится исполняемый файл AzCopy.exe hello.</span><span class="sxs-lookup"><span data-stu-id="84141-114">toorun AzCopy commands, open a command window and navigate toohello AzCopy installation directory on your computer, where hello AzCopy.exe executable is located.</span></span> 

<span data-ttu-id="84141-115">Базовый синтаксис команды AzCopy Hello таков:</span><span class="sxs-lookup"><span data-stu-id="84141-115">hello basic syntax for AzCopy commands is:</span></span>

    AzCopy /Source:<source> /Dest:<destination> [Options]

> [!NOTE]
> <span data-ttu-id="84141-116">Можно добавить hello AzCopy tooyour системы путь установки и выполнить команды hello из любого каталога.</span><span class="sxs-lookup"><span data-stu-id="84141-116">You can add hello AzCopy installation location tooyour system path and then run hello commands from any directory.</span></span> <span data-ttu-id="84141-117">По умолчанию AzCopy установлен слишком*% ProgramFiles (x86) %\Microsoft SDKs\Azure\AzCopy* или *%ProgramFiles%\Microsoft SDKs\Azure\AzCopy*.</span><span class="sxs-lookup"><span data-stu-id="84141-117">By default, AzCopy is installed too*%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy* or *%ProgramFiles%\Microsoft SDKs\Azure\AzCopy*.</span></span>
> 
> 

## <a name="upload-files-tooan-azure-blob"></a><span data-ttu-id="84141-118">Отправка файлов tooan BLOB-объектов Azure</span><span class="sxs-lookup"><span data-stu-id="84141-118">Upload files tooan Azure blob</span></span>
<span data-ttu-id="84141-119">tooupload файл hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="84141-119">tooupload a file, use hello following command:</span></span>

    # Upload from local file system
    AzCopy /Source:<your_local_directory> /Dest: https://<your_account_name>.blob.core.windows.net/<your_container_name> /DestKey:<your_account_key> /S


## <a name="download-files-from-an-azure-blob"></a><span data-ttu-id="84141-120">Скачивание файлов из большого двоичного объекта Azure</span><span class="sxs-lookup"><span data-stu-id="84141-120">Download files from an Azure blob</span></span>
<span data-ttu-id="84141-121">toodownload файл из BLOB-объекта Azure, hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="84141-121">toodownload a file from an Azure blob, use hello following command:</span></span>

    # Downloading blobs toolocal file system
    AzCopy /Source:https://<your_account_name>.blob.core.windows.net/<your_container_name>/<your_sub_directory_at_blob>  /Dest:<your_local_directory> /SourceKey:<your_account_key> /Pattern:<file_pattern> /S


## <a name="transfer-blobs-between-azure-containers"></a><span data-ttu-id="84141-122">Передача больших двоичных объектов между контейнерами Azure</span><span class="sxs-lookup"><span data-stu-id="84141-122">Transfer blobs between Azure containers</span></span>
<span data-ttu-id="84141-123">tootransfer больших двоичных объектов между контейнерами Azure, используйте hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="84141-123">tootransfer blobs between Azure containers, use hello following command:</span></span>

    # Transferring blobs between Azure containers
    AzCopy /Source:https://<your_account_name1>.blob.core.windows.net/<your_container_name1>/<your_sub_directory_at_blob1> /Dest:https://<your_account_name2>.blob.core.windows.net/<your_container_name2>/<your_sub_directory_at_blob2> /SourceKey:<your_account_key1> /DestKey:<your_account_key2> /Pattern:<file_pattern> /S

    <your_account_name>: your storage account name
    <your_account_key>: your storage account key
    <your_container_name>: your container name
    <your_sub_directory_at_blob>: hello sub directory in hello container
    <your_local_directory>: directory of local file system where files toobe uploaded from or hello directory of local file system files toobe downloaded to
    <file_pattern>: pattern of file names toobe transferred. hello standard wildcards are supported


## <a name="tips-for-using-azcopy"></a><span data-ttu-id="84141-124">Советы по использованию AzCopy</span><span class="sxs-lookup"><span data-stu-id="84141-124">Tips for using AzCopy</span></span>
> [!TIP]
> 1. <span data-ttu-id="84141-125">При **отправке** с параметром */S* файлы отправляются рекурсивно.</span><span class="sxs-lookup"><span data-stu-id="84141-125">When **uploading** files, */S* uploads files recursively.</span></span> <span data-ttu-id="84141-126">Без этого параметра файлы из подкаталогов не отправляются.</span><span class="sxs-lookup"><span data-stu-id="84141-126">Without this parameter, files in subdirectories are not uploaded.</span></span>  
> 2. <span data-ttu-id="84141-127">Когда **Загрузка** файла, */S* поиск hello контейнера рекурсивно, пока все файлы в указанном каталоге hello и его подкаталогах или Здравствуйте, всех файлов, соответствующих заданному шаблону в заданный hello загружаются каталоге и его подкаталогах.</span><span class="sxs-lookup"><span data-stu-id="84141-127">When **downloading** file, */S* searches hello container recursively until all files in hello specified directory and its subdirectories, or all files that match hello specified pattern in hello given directory and its subdirectories, are downloaded.</span></span>  
> 3. <span data-ttu-id="84141-128">Нельзя указать **файл определенным BLOB-объектом** toodownload, с помощью hello */Source* параметра.</span><span class="sxs-lookup"><span data-stu-id="84141-128">You cannot specify a **specific blob file** toodownload using hello */Source* parameter.</span></span> <span data-ttu-id="84141-129">toodownload конкретного файла, укажите с помощью hello имя toodownload hello большого двоичного объекта файла */шаблона* параметра.</span><span class="sxs-lookup"><span data-stu-id="84141-129">toodownload a specific file, specify hello blob file name toodownload using hello */Pattern* parameter.</span></span> <span data-ttu-id="84141-130">**/S** параметр может иметь вид AzCopy используется toohave рекурсивно шаблон, имя файла.</span><span class="sxs-lookup"><span data-stu-id="84141-130">**/S** parameter can be used toohave AzCopy look for a file name pattern recursively.</span></span> <span data-ttu-id="84141-131">Без параметра pattern hello AzCopy загружает все файлы в этом каталоге.</span><span class="sxs-lookup"><span data-stu-id="84141-131">Without hello pattern parameter, AzCopy downloads all files in that directory.</span></span>
> 
> 

