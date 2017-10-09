---
title: "Примеры для хранилища aaaAzure с помощью .NET | Документы Microsoft"
description: "Просмотрите, загрузите и запустите образцы кода и приложений для хранилища Azure. Обнаружение, Приступая к работе образцы для больших двоичных объектов, очередей, таблиц и файлов, с помощью клиентских библиотек хранилища .NET hello."
services: storage
documentationcenter: na
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 01/12/2017
ms.author: seguler
ms.openlocfilehash: 6b02b596f77845fc5fa474fa235c2b5df6e94ad7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-samples-using-net"></a><span data-ttu-id="ad57e-104">Примеры для службы хранилища Azure с использованием .NET</span><span class="sxs-lookup"><span data-stu-id="ad57e-104">Azure Storage samples using .NET</span></span>

## <a name="net-sample-index"></a><span data-ttu-id="ad57e-105">Указатель по примерам для .NET</span><span class="sxs-lookup"><span data-stu-id="ad57e-105">.NET sample index</span></span>

<span data-ttu-id="ad57e-106">Hello следующей таблице представлены общие сведения о наши примеры репозитория и hello сценарии, описанные в каждой выборке.</span><span class="sxs-lookup"><span data-stu-id="ad57e-106">hello following table provides an overview of our samples repository and hello scenarios covered in each sample.</span></span> <span data-ttu-id="ad57e-107">Щелкните hello ссылки tooview hello соответствующие примеры кода в GitHub.</span><span class="sxs-lookup"><span data-stu-id="ad57e-107">Click on hello links tooview hello corresponding sample code in GitHub.</span></span>

<table style="font-size:90%"><thead><tr><th style="font-size:110%"><span data-ttu-id="ad57e-108">Конечная точка</span><span class="sxs-lookup"><span data-stu-id="ad57e-108">Endpoint</span></span></th><th style="font-size:110%"><span data-ttu-id="ad57e-109">Сценарий</span><span class="sxs-lookup"><span data-stu-id="ad57e-109">Scenario</span></span></th><th style="font-size:110%"><span data-ttu-id="ad57e-110">Пример кода</span><span class="sxs-lookup"><span data-stu-id="ad57e-110">Sample Code</span></span></th></tr></thead><tbody> 
<tr> 
<td rowspan="16"><span data-ttu-id="ad57e-111"><b>Большой двоичный объект</b></span><span class="sxs-lookup"><span data-stu-id="ad57e-111"><b>Blob</b></span></span></td>
<td><span data-ttu-id="ad57e-112">Добавление больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="ad57e-112">Append Blob</span></span></td> 
<td><span data-ttu-id="ad57e-113"><a href="https://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.getappendblobreference.aspx">Пример метода CloudBlobContainer.GetAppendBlobReference</a></span><span class="sxs-lookup"><span data-stu-id="ad57e-113"><a href="https://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.getappendblobreference.aspx">CloudBlobContainer.GetAppendBlobReference Method Example</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="ad57e-114">Блочный BLOB-объект</span><span class="sxs-lookup"><span data-stu-id="ad57e-114">Block Blob</span></span></td>
<td><span data-ttu-id="ad57e-115"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Веб-приложение фотоальбома для хранилища BLOB-объектов Azure</a></span><span class="sxs-lookup"><span data-stu-id="ad57e-115"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="ad57e-116">Шифрование на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="ad57e-116">Client-Side Encryption</span></span></td>
<td><span data-ttu-id="ad57e-117"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/BlobGettingStarted/Program.cs">Примеры шифрования больших двоичных объектов</a></span><span class="sxs-lookup"><span data-stu-id="ad57e-117"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/BlobGettingStarted/Program.cs">Blob Encryption Samples</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="ad57e-118">Копирование BLOB-объекта</span><span class="sxs-lookup"><span data-stu-id="ad57e-118">Copy Blob</span></span></td>
<td><span data-ttu-id="ad57e-119"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Приступая к работе с большими двоичными объектами</a></span><span class="sxs-lookup"><span data-stu-id="ad57e-119"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="ad57e-120">Create Container (Создание контейнера)</span><span class="sxs-lookup"><span data-stu-id="ad57e-120">Create Container</span></span></td>
<td><span data-ttu-id="ad57e-121"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Веб-приложение фотоальбома для хранилища BLOB-объектов Azure</a></span><span class="sxs-lookup"><span data-stu-id="ad57e-121"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="ad57e-122">Delete BLOB (Удаление BLOB-объекта)</span><span class="sxs-lookup"><span data-stu-id="ad57e-122">Delete Blob</span></span></td>
<td><span data-ttu-id="ad57e-123"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Веб-приложение фотоальбома для хранилища BLOB-объектов Azure</a></span><span class="sxs-lookup"><span data-stu-id="ad57e-123"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="ad57e-124">Delete Container (Удаление контейнера)</span><span class="sxs-lookup"><span data-stu-id="ad57e-124">Delete Container</span></span></td>
<td><span data-ttu-id="ad57e-125"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Приступая к работе с большими двоичными объектами</a></span><span class="sxs-lookup"><span data-stu-id="ad57e-125"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="ad57e-126">Метаданные, свойства и статистика больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="ad57e-126">Blob Metadata/Properties/Stats</span></span></td>
<td><span data-ttu-id="ad57e-127"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Приступая к работе с большими двоичными объектами</a></span><span class="sxs-lookup"><span data-stu-id="ad57e-127"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="ad57e-128">ACL, метаданные и свойства контейнера</span><span class="sxs-lookup"><span data-stu-id="ad57e-128">Container ACL/Metadata/Properties</span></span></td>
<td><span data-ttu-id="ad57e-129"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Веб-приложение фотоальбома для хранилища BLOB-объектов Azure</a></span><span class="sxs-lookup"><span data-stu-id="ad57e-129"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="ad57e-130">Get Page Ranges (Получение диапазона страницы)</span><span class="sxs-lookup"><span data-stu-id="ad57e-130">Get Page Ranges</span></span></td>
<td><span data-ttu-id="ad57e-131"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Приступая к работе с большими двоичными объектами</a></span><span class="sxs-lookup"><span data-stu-id="ad57e-131"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="ad57e-132">Аренда большого двоичного объекта и контейнера</span><span class="sxs-lookup"><span data-stu-id="ad57e-132">Lease Blob/Container</span></span></td>
<td><span data-ttu-id="ad57e-133"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Приступая к работе с большими двоичными объектами</a></span><span class="sxs-lookup"><span data-stu-id="ad57e-133"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="ad57e-134">Список больших двоичных объектов и контейнеров</span><span class="sxs-lookup"><span data-stu-id="ad57e-134">List Blob/Container</span></span></td>
<td><span data-ttu-id="ad57e-135"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Приступая к работе с большими двоичными объектами</a></span><span class="sxs-lookup"><span data-stu-id="ad57e-135"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="ad57e-136">Страничный BLOB-объект</span><span class="sxs-lookup"><span data-stu-id="ad57e-136">Page Blob</span></span></td>
<td><span data-ttu-id="ad57e-137"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Приступая к работе с большими двоичными объектами</a></span><span class="sxs-lookup"><span data-stu-id="ad57e-137"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Getting Started with Blobs</a></span></span></td>
</tr>
<tr> 
<td><span data-ttu-id="ad57e-138">SAS</span><span class="sxs-lookup"><span data-stu-id="ad57e-138">SAS</span></span></td>
<td><span data-ttu-id="ad57e-139"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Приступая к работе с большими двоичными объектами</a></span><span class="sxs-lookup"><span data-stu-id="ad57e-139"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr>   
<tr> 
<td><span data-ttu-id="ad57e-140">Свойства службы</span><span class="sxs-lookup"><span data-stu-id="ad57e-140">Service Properties</span></span></td>
<td><span data-ttu-id="ad57e-141"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Приступая к работе с большими двоичными объектами</a></span><span class="sxs-lookup"><span data-stu-id="ad57e-141"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr>           
<tr> 
<td><span data-ttu-id="ad57e-142">Создание моментального снимка большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="ad57e-142">Snapshot Blob</span></span></td>
<td><span data-ttu-id="ad57e-143"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-back-up-with-incremental-snapshots/blob/master/Program.cs">Backup Azure Virtual Machine Disks with Incremental Snapshots</a> (Резервное копирование дисков виртуальной машины Azure с помощью добавочных моментальных снимков)</span><span class="sxs-lookup"><span data-stu-id="ad57e-143"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-back-up-with-incremental-snapshots/blob/master/Program.cs">Backup Azure Virtual Machine Disks with Incremental Snapshots</a></span></span></td>
</tr> 
<tr> 
<td rowspan="9"><span data-ttu-id="ad57e-144"><b>File</b></span><span class="sxs-lookup"><span data-stu-id="ad57e-144"><b>File</b></span></span></td>
<td><span data-ttu-id="ad57e-145">Создание общих папок, каталогов и файлов</span><span class="sxs-lookup"><span data-stu-id="ad57e-145">Create Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="ad57e-146"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Пример хранилища файлов .NET для службы хранилища Azure</a></span><span class="sxs-lookup"><span data-stu-id="ad57e-146"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="ad57e-147">Удаление общих папок, каталогов и файлов</span><span class="sxs-lookup"><span data-stu-id="ad57e-147">Delete Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="ad57e-148"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/master/FileStorage/GettingStarted.cs">Приступая к работе со службой файлов Azure в .NET</a></span><span class="sxs-lookup"><span data-stu-id="ad57e-148"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/master/FileStorage/GettingStarted.cs">Getting Started with Azure File Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="ad57e-149">Метаданные и свойства каталога</span><span class="sxs-lookup"><span data-stu-id="ad57e-149">Directory Properties/Metadata</span></span></td> 
<td><span data-ttu-id="ad57e-150"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Пример хранилища файлов .NET для службы хранилища Azure</a></span><span class="sxs-lookup"><span data-stu-id="ad57e-150"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="ad57e-151">Скачивание файлов</span><span class="sxs-lookup"><span data-stu-id="ad57e-151">Download Files</span></span></td> 
<td><span data-ttu-id="ad57e-152"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Пример хранилища файлов .NET для службы хранилища Azure</a></span><span class="sxs-lookup"><span data-stu-id="ad57e-152"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="ad57e-153">Метрики, метаданные и свойства файла</span><span class="sxs-lookup"><span data-stu-id="ad57e-153">File Properties/Metadata/Metrics</span></span></td> 
<td><span data-ttu-id="ad57e-154"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Пример хранилища файлов .NET для службы хранилища Azure</a></span><span class="sxs-lookup"><span data-stu-id="ad57e-154"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="ad57e-155">Свойства службы файлов</span><span class="sxs-lookup"><span data-stu-id="ad57e-155">File Service Properties</span></span></td> 
<td><span data-ttu-id="ad57e-156"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Пример хранилища файлов .NET для службы хранилища Azure</a></span><span class="sxs-lookup"><span data-stu-id="ad57e-156"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="ad57e-157">Список каталогов и файлов</span><span class="sxs-lookup"><span data-stu-id="ad57e-157">List Directories and Files</span></span></td> 
<td><span data-ttu-id="ad57e-158"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Пример хранилища файлов .NET для службы хранилища Azure</a></span><span class="sxs-lookup"><span data-stu-id="ad57e-158"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="ad57e-159">Список общих папок</span><span class="sxs-lookup"><span data-stu-id="ad57e-159">List Shares</span></span></td> 
<td><span data-ttu-id="ad57e-160"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Пример хранилища файлов .NET для службы хранилища Azure</a></span><span class="sxs-lookup"><span data-stu-id="ad57e-160"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="ad57e-161">Статистика, метаданные и свойства общей папки</span><span class="sxs-lookup"><span data-stu-id="ad57e-161">Share Properties/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="ad57e-162"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Пример хранилища файлов .NET для службы хранилища Azure</a></span><span class="sxs-lookup"><span data-stu-id="ad57e-162"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td rowspan="8"><span data-ttu-id="ad57e-163"><b>Очередь</b></span><span class="sxs-lookup"><span data-stu-id="ad57e-163"><b>Queue</b></span></span></td>
<td><span data-ttu-id="ad57e-164">Добавление сообщения</span><span class="sxs-lookup"><span data-stu-id="ad57e-164">Add Message</span></span></td> 
<td><span data-ttu-id="ad57e-165"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Приступая к работе со службой очередей Azure в .NET</a></span><span class="sxs-lookup"><span data-stu-id="ad57e-165"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="ad57e-166">Шифрование на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="ad57e-166">Client-Side Encryption</span></span></td> 
<td><span data-ttu-id="ad57e-167"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/QueueGettingStarted/Program.cs">Очередь шифрования на стороне клиента .NET для службы хранилища Azure</a></span><span class="sxs-lookup"><span data-stu-id="ad57e-167"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/QueueGettingStarted/Program.cs">Azure Storage .NET Queue Client-Side Encryption</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="ad57e-168">Создание очередей</span><span class="sxs-lookup"><span data-stu-id="ad57e-168">Create Queues</span></span></td> 
<td><span data-ttu-id="ad57e-169"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Приступая к работе со службой очередей Azure в .NET</a></span><span class="sxs-lookup"><span data-stu-id="ad57e-169"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="ad57e-170">Удаление сообщения и очереди</span><span class="sxs-lookup"><span data-stu-id="ad57e-170">Delete Message/Queue</span></span></td> 
<td><span data-ttu-id="ad57e-171"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Приступая к работе со службой очередей Azure в .NET</a></span><span class="sxs-lookup"><span data-stu-id="ad57e-171"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="ad57e-172">Просмотр сообщения</span><span class="sxs-lookup"><span data-stu-id="ad57e-172">Peek Message</span></span></td> 
<td><span data-ttu-id="ad57e-173"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Приступая к работе со службой очередей Azure в .NET</a></span><span class="sxs-lookup"><span data-stu-id="ad57e-173"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="ad57e-174">ACL, метаданные и статистика очереди</span><span class="sxs-lookup"><span data-stu-id="ad57e-174">Queue ACL/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="ad57e-175"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Приступая к работе со службой очередей Azure в .NET</a></span><span class="sxs-lookup"><span data-stu-id="ad57e-175"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="ad57e-176">Свойства службы очередей</span><span class="sxs-lookup"><span data-stu-id="ad57e-176">Queue Service Properties</span></span></td> 
<td><span data-ttu-id="ad57e-177"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Приступая к работе со службой очередей Azure в .NET</a></span><span class="sxs-lookup"><span data-stu-id="ad57e-177"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="ad57e-178">Сообщение об обновлении</span><span class="sxs-lookup"><span data-stu-id="ad57e-178">Update Message</span></span></td> 
<td><span data-ttu-id="ad57e-179"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Приступая к работе со службой очередей Azure в .NET</a></span><span class="sxs-lookup"><span data-stu-id="ad57e-179"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td rowspan="7"><span data-ttu-id="ad57e-180"><b>Таблица</b></span><span class="sxs-lookup"><span data-stu-id="ad57e-180"><b>Table</b></span></span></td>
<td><span data-ttu-id="ad57e-181">Создание таблицы</span><span class="sxs-lookup"><span data-stu-id="ad57e-181">Create Table</span></span></td> 
<td><span data-ttu-id="ad57e-182"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Управление параллелизмом с помощью службы хранилища Azure: пример приложения</a></span><span class="sxs-lookup"><span data-stu-id="ad57e-182"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="ad57e-183">Удаление сущности или таблицы</span><span class="sxs-lookup"><span data-stu-id="ad57e-183">Delete Entity/Table</span></span></td> 
<td><span data-ttu-id="ad57e-184"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a> (Приступая к работе с хранилищем таблиц Azure в .NET)</span><span class="sxs-lookup"><span data-stu-id="ad57e-184"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="ad57e-185">Вставка, слияние или замена сущностей</span><span class="sxs-lookup"><span data-stu-id="ad57e-185">Insert/Merge/Replace Entity</span></span></td> 
<td><span data-ttu-id="ad57e-186"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Управление параллелизмом с помощью службы хранилища Azure: пример приложения</a></span><span class="sxs-lookup"><span data-stu-id="ad57e-186"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="ad57e-187">Query Entities (Сущности запроса)</span><span class="sxs-lookup"><span data-stu-id="ad57e-187">Query Entities</span></span></td> 
<td><span data-ttu-id="ad57e-188"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a> (Приступая к работе с хранилищем таблиц Azure в .NET)</span><span class="sxs-lookup"><span data-stu-id="ad57e-188"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="ad57e-189">Запросы к таблицам</span><span class="sxs-lookup"><span data-stu-id="ad57e-189">Query Tables</span></span></td> 
<td><span data-ttu-id="ad57e-190"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a> (Приступая к работе с хранилищем таблиц Azure в .NET)</span><span class="sxs-lookup"><span data-stu-id="ad57e-190"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="ad57e-191">Свойства и ACL таблицы</span><span class="sxs-lookup"><span data-stu-id="ad57e-191">Table ACL/Properties</span></span></td> 
<td><span data-ttu-id="ad57e-192"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/AdvancedSamples.cs">Getting Started with Azure Table Storage in .NET</a> (Приступая к работе с хранилищем таблиц Azure в .NET)</span><span class="sxs-lookup"><span data-stu-id="ad57e-192"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/AdvancedSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="ad57e-193">Update Entity (Обновление сущности)</span><span class="sxs-lookup"><span data-stu-id="ad57e-193">Update Entity</span></span></td> 
<td><span data-ttu-id="ad57e-194"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Управление параллелизмом с помощью службы хранилища Azure: пример приложения</a></span><span class="sxs-lookup"><span data-stu-id="ad57e-194"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
</tbody> 
</table>
<br/>

## <a name="azure-code-samples-library"></a><span data-ttu-id="ad57e-195">Библиотека примеров кода Azure</span><span class="sxs-lookup"><span data-stu-id="ad57e-195">Azure Code Samples library</span></span>

<span data-ttu-id="ad57e-196">Полный образец библиотеки tooview hello перейдите toohello [образцы кода Azure](https://azure.microsoft.com/resources/samples/?service=storage) библиотеку, которая включает примеры для хранилища Azure, можно загрузить и запустить его локально.</span><span class="sxs-lookup"><span data-stu-id="ad57e-196">tooview hello complete sample library, go toohello [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=storage) library, which includes samples for Azure Storage that you can download and run locally.</span></span> <span data-ttu-id="ad57e-197">Hello кода образца библиотеки содержит пример кода в формате ZIP.</span><span class="sxs-lookup"><span data-stu-id="ad57e-197">hello Code Sample Library provides sample code in .zip format.</span></span> <span data-ttu-id="ad57e-198">Кроме того можно просмотреть и клонирование репозитория GitHub hello для каждого образца.</span><span class="sxs-lookup"><span data-stu-id="ad57e-198">Alternatively, you can browse and clone hello GitHub repository for each sample.</span></span>

[!INCLUDE [storage-dotnet-samples-include](../../../includes/storage-dotnet-samples-include.md)]

## <a name="getting-started-guides"></a><span data-ttu-id="ad57e-199">Руководства по началу работы</span><span class="sxs-lookup"><span data-stu-id="ad57e-199">Getting started guides</span></span>

<span data-ttu-id="ad57e-200">Извлечение hello следующие руководства, если вам нужны дополнительные сведения о tooinstall и приступить к работе с hello клиентских библиотек хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="ad57e-200">Check out hello following guides if you are looking for instructions on how tooinstall and get started with hello Azure Storage Client Libraries.</span></span>

* [<span data-ttu-id="ad57e-201">Приступая к работе со службой BLOB-объектов Azure в .NET</span><span class="sxs-lookup"><span data-stu-id="ad57e-201">Getting Started with Azure Blob Service in .NET</span></span>](../blobs/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="ad57e-202">Приступая к работе со службой очередей Azure в .NET</span><span class="sxs-lookup"><span data-stu-id="ad57e-202">Getting Started with Azure Queue Service in .NET</span></span>](../storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="ad57e-203">Приступая к работе со службой таблиц Azure в .NET</span><span class="sxs-lookup"><span data-stu-id="ad57e-203">Getting Started with Azure Table Service in .NET</span></span>](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [<span data-ttu-id="ad57e-204">Приступая к работе со службой файлов Azure в .NET</span><span class="sxs-lookup"><span data-stu-id="ad57e-204">Getting Started with Azure File Service in .NET</span></span>](../storage-dotnet-how-to-use-files.md)

## <a name="next-steps"></a><span data-ttu-id="ad57e-205">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ad57e-205">Next steps</span></span>

<span data-ttu-id="ad57e-206">Дополнительные сведения о примерах для других языков см. здесь:</span><span class="sxs-lookup"><span data-stu-id="ad57e-206">For information on samples for other languages:</span></span>

* <span data-ttu-id="ad57e-207">Java: [Azure Storage samples using Java](storage-samples-java.md) (Примеры для службы хранилища Azure с использованием Java)</span><span class="sxs-lookup"><span data-stu-id="ad57e-207">Java: [Azure Storage samples using Java](storage-samples-java.md)</span></span>
* <span data-ttu-id="ad57e-208">Все остальные языки: [Azure Storage samples](../storage-samples.md) (Примеры для службы хранилища Azure)</span><span class="sxs-lookup"><span data-stu-id="ad57e-208">All other languages: [Azure Storage samples](../storage-samples.md)</span></span>
