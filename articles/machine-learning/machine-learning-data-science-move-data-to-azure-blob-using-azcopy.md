---
title: "Перемещение данных в хранилище BLOB-объектов Azure и из него с помощью AzCopy | Документация Майкрософт"
description: "Перемещение данных в хранилище больших двоичных объектов Azure и из него с помощью AzCopy"
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
ms.openlocfilehash: a41ccdd5739a5b10cef201910abd639ae3126c02
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-to-and-from-azure-blob-storage-using-azcopy"></a><span data-ttu-id="96933-103">Перемещение данных в хранилище BLOB-объектов Azure и из него с помощью AzCopy</span><span class="sxs-lookup"><span data-stu-id="96933-103">Move data to and from Azure Blob Storage using AzCopy</span></span>
<span data-ttu-id="96933-104">AzCopy — это служебная программа командной строки, разработанная для отправки, скачивания и копирования данных из хранилищ BLOB-объектов, файлов и таблиц Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="96933-104">AzCopy is a command-line utility designed for uploading, downloading, and copying data to and from Microsoft Azure blob, file, and table storage.</span></span>

<span data-ttu-id="96933-105">Инструкции по установке программы AzCopy и дополнительные сведения о ее использовании с платформой Azure см. в статье [Приступая к работе со служебной программой командной строки AzCopy](../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="96933-105">For instructions on installing AzCopy and additional information on using it with the Azure platform, see [Getting Started with the AzCopy Command-Line Utility](../storage/common/storage-use-azcopy.md).</span></span>

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> <span data-ttu-id="96933-106">Если используется виртуальная машина, созданная с помощью скриптов, предоставленных [виртуальными машинами для обработки и анализа данных в Azure](machine-learning-data-science-virtual-machines.md), то программа AzCopy уже установлена на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="96933-106">If you are using VM that was set up with the scripts provided by [Data Science Virtual machines in Azure](machine-learning-data-science-virtual-machines.md), then AzCopy is already installed on the VM.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="96933-107">Полное описание базовых принципов использования хранилища BLOB-объектов Azure см. в статьях [Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) и [Основные понятия службы BLOB-объектов](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="96933-107">For a complete introduction to Azure blob storage, refer to [Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and to [Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="96933-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="96933-108">Prerequisites</span></span>
<span data-ttu-id="96933-109">Для выполнения указаний в этом документе у вас должна быть подписка Azure, учетная запись хранения и соответствующий ключ к хранилищу данных для этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="96933-109">This document assumes that you have an Azure subscription, a storage account and the corresponding storage key for that account.</span></span> <span data-ttu-id="96933-110">Чтобы отправлять и скачивать данные, необходимо знать имя учетной записи хранения Azure и ее ключ.</span><span class="sxs-lookup"><span data-stu-id="96933-110">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="96933-111">Сведения о настройке подписки Azure см. на странице [Создайте бесплатную учетную запись Azure уже сегодня](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="96933-111">To set up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="96933-112">Инструкции по созданию учетной записи хранения и получению сведений об учетной записи и ключах см. в статье [Об учетных записях хранения Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="96933-112">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

## <a name="run-azcopy-commands"></a><span data-ttu-id="96933-113">Выполнение команд AzCopy</span><span class="sxs-lookup"><span data-stu-id="96933-113">Run AzCopy commands</span></span>
<span data-ttu-id="96933-114">Чтобы выполнить команды AzCopy, откройте командное окно и перейдите к каталогу установки AzCopy на компьютере, где располагается исполняемый файл AzCopy.exe.</span><span class="sxs-lookup"><span data-stu-id="96933-114">To run AzCopy commands, open a command window and navigate to the AzCopy installation directory on your computer, where the AzCopy.exe executable is located.</span></span> 

<span data-ttu-id="96933-115">В командах AzCopy используется следующий базовый синтаксис:</span><span class="sxs-lookup"><span data-stu-id="96933-115">The basic syntax for AzCopy commands is:</span></span>

    AzCopy /Source:<source> /Dest:<destination> [Options]

> [!NOTE]
> <span data-ttu-id="96933-116">Можно добавить место установки AzCopy к системному пути, а затем выполнить команды из любого каталога.</span><span class="sxs-lookup"><span data-stu-id="96933-116">You can add the AzCopy installation location to your system path and then run the commands from any directory.</span></span> <span data-ttu-id="96933-117">По умолчанию AzCopy устанавливается в *%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy* или *%ProgramFiles%\Microsoft SDKs\Azure\AzCopy*.</span><span class="sxs-lookup"><span data-stu-id="96933-117">By default, AzCopy is installed to *%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy* or *%ProgramFiles%\Microsoft SDKs\Azure\AzCopy*.</span></span>
> 
> 

## <a name="upload-files-to-an-azure-blob"></a><span data-ttu-id="96933-118">Передача файлов в большой двоичный объект Azure</span><span class="sxs-lookup"><span data-stu-id="96933-118">Upload files to an Azure blob</span></span>
<span data-ttu-id="96933-119">Для отправки файла используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="96933-119">To upload a file, use the following command:</span></span>

    # Upload from local file system
    AzCopy /Source:<your_local_directory> /Dest: https://<your_account_name>.blob.core.windows.net/<your_container_name> /DestKey:<your_account_key> /S


## <a name="download-files-from-an-azure-blob"></a><span data-ttu-id="96933-120">Скачивание файлов из большого двоичного объекта Azure</span><span class="sxs-lookup"><span data-stu-id="96933-120">Download files from an Azure blob</span></span>
<span data-ttu-id="96933-121">Для скачивания файла из большого двоичного объекта Azure используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="96933-121">To download a file from an Azure blob, use the following command:</span></span>

    # Downloading blobs to local file system
    AzCopy /Source:https://<your_account_name>.blob.core.windows.net/<your_container_name>/<your_sub_directory_at_blob>  /Dest:<your_local_directory> /SourceKey:<your_account_key> /Pattern:<file_pattern> /S


## <a name="transfer-blobs-between-azure-containers"></a><span data-ttu-id="96933-122">Передача больших двоичных объектов между контейнерами Azure</span><span class="sxs-lookup"><span data-stu-id="96933-122">Transfer blobs between Azure containers</span></span>
<span data-ttu-id="96933-123">Для передачи больших двоичных объектов между контейнерами Azure используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="96933-123">To transfer blobs between Azure containers, use the following command:</span></span>

    # Transferring blobs between Azure containers
    AzCopy /Source:https://<your_account_name1>.blob.core.windows.net/<your_container_name1>/<your_sub_directory_at_blob1> /Dest:https://<your_account_name2>.blob.core.windows.net/<your_container_name2>/<your_sub_directory_at_blob2> /SourceKey:<your_account_key1> /DestKey:<your_account_key2> /Pattern:<file_pattern> /S

    <your_account_name>: your storage account name
    <your_account_key>: your storage account key
    <your_container_name>: your container name
    <your_sub_directory_at_blob>: the sub directory in the container
    <your_local_directory>: directory of local file system where files to be uploaded from or the directory of local file system files to be downloaded to
    <file_pattern>: pattern of file names to be transferred. The standard wildcards are supported


## <a name="tips-for-using-azcopy"></a><span data-ttu-id="96933-124">Советы по использованию AzCopy</span><span class="sxs-lookup"><span data-stu-id="96933-124">Tips for using AzCopy</span></span>
> [!TIP]
> 1. <span data-ttu-id="96933-125">При **отправке** с параметром */S* файлы отправляются рекурсивно.</span><span class="sxs-lookup"><span data-stu-id="96933-125">When **uploading** files, */S* uploads files recursively.</span></span> <span data-ttu-id="96933-126">Без этого параметра файлы из подкаталогов не отправляются.</span><span class="sxs-lookup"><span data-stu-id="96933-126">Without this parameter, files in subdirectories are not uploaded.</span></span>  
> 2. <span data-ttu-id="96933-127">При **скачивании** файла с параметром */S* выполняется рекурсивный поиск по контейнеру до тех пор, пока не будут скачаны все файлы в указанном каталоге и его подкаталогах или все файлы, соответствующие указанному шаблону в заданном каталоге или его подкаталогах.</span><span class="sxs-lookup"><span data-stu-id="96933-127">When **downloading** file, */S* searches the container recursively until all files in the specified directory and its subdirectories, or all files that match the specified pattern in the given directory and its subdirectories, are downloaded.</span></span>  
> 3. <span data-ttu-id="96933-128">При использовании параметра **/Source** нельзя указать *определенный файл большого двоичного объекта* для скачивания.</span><span class="sxs-lookup"><span data-stu-id="96933-128">You cannot specify a **specific blob file** to download using the */Source* parameter.</span></span> <span data-ttu-id="96933-129">Чтобы скачать определенный файл, укажите имя файла большого двоичного объекта для скачивания, используя параметр */Pattern* .</span><span class="sxs-lookup"><span data-stu-id="96933-129">To download a specific file, specify the blob file name to download using the */Pattern* parameter.</span></span> <span data-ttu-id="96933-130">**/S** можно использовать для рекурсивного поиска шаблона имени файла с помощью AzCopy.</span><span class="sxs-lookup"><span data-stu-id="96933-130">**/S** parameter can be used to have AzCopy look for a file name pattern recursively.</span></span> <span data-ttu-id="96933-131">Без параметра шаблона AzCopy скачивает все файлы, содержащиеся в этом каталоге.</span><span class="sxs-lookup"><span data-stu-id="96933-131">Without the pattern parameter, AzCopy downloads all files in that directory.</span></span>
> 
> 

