---
title: "Примеры для службы хранилища Azure с использованием .NET | Документация Майкрософт"
description: "Просмотрите, загрузите и запустите образцы кода и приложений для хранилища Azure. Воспользуйтесь примерами для начала работы с большими двоичными объектами, очередями, таблицами и файлами с помощью клиентских библиотек хранилища .NET."
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
ms.openlocfilehash: d2b6b3d9483f230ad25ae47255a4f28c1a67e064
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-storage-samples-using-net"></a><span data-ttu-id="9cd73-104">Примеры для службы хранилища Azure с использованием .NET</span><span class="sxs-lookup"><span data-stu-id="9cd73-104">Azure Storage samples using .NET</span></span>

## <a name="net-sample-index"></a><span data-ttu-id="9cd73-105">Указатель по примерам для .NET</span><span class="sxs-lookup"><span data-stu-id="9cd73-105">.NET sample index</span></span>

<span data-ttu-id="9cd73-106">В таблице ниже приведен обзор репозитория примеров и сценарии, описанные в каждом примере.</span><span class="sxs-lookup"><span data-stu-id="9cd73-106">The following table provides an overview of our samples repository and the scenarios covered in each sample.</span></span> <span data-ttu-id="9cd73-107">Щелкните ссылки для просмотра соответствующего примера кода на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="9cd73-107">Click on the links to view the corresponding sample code in GitHub.</span></span>

<table style="font-size:90%"><thead><tr><th style="font-size:110%"><span data-ttu-id="9cd73-108">Конечная точка</span><span class="sxs-lookup"><span data-stu-id="9cd73-108">Endpoint</span></span></th><th style="font-size:110%"><span data-ttu-id="9cd73-109">Сценарий</span><span class="sxs-lookup"><span data-stu-id="9cd73-109">Scenario</span></span></th><th style="font-size:110%"><span data-ttu-id="9cd73-110">Пример кода</span><span class="sxs-lookup"><span data-stu-id="9cd73-110">Sample Code</span></span></th></tr></thead><tbody> 
<tr> 
<td rowspan="16"><span data-ttu-id="9cd73-111"><b>Большой двоичный объект</b></span><span class="sxs-lookup"><span data-stu-id="9cd73-111"><b>Blob</b></span></span></td>
<td><span data-ttu-id="9cd73-112">Добавление больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="9cd73-112">Append Blob</span></span></td> 
<td><span data-ttu-id="9cd73-113"><a href="https://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.getappendblobreference.aspx">Пример метода CloudBlobContainer.GetAppendBlobReference</a></span><span class="sxs-lookup"><span data-stu-id="9cd73-113"><a href="https://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.getappendblobreference.aspx">CloudBlobContainer.GetAppendBlobReference Method Example</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9cd73-114">Блочный BLOB-объект</span><span class="sxs-lookup"><span data-stu-id="9cd73-114">Block Blob</span></span></td>
<td><span data-ttu-id="9cd73-115"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Веб-приложение фотоальбома для хранилища BLOB-объектов Azure</a></span><span class="sxs-lookup"><span data-stu-id="9cd73-115"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="9cd73-116">Шифрование на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="9cd73-116">Client-Side Encryption</span></span></td>
<td><span data-ttu-id="9cd73-117"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/BlobGettingStarted/Program.cs">Примеры шифрования больших двоичных объектов</a></span><span class="sxs-lookup"><span data-stu-id="9cd73-117"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/BlobGettingStarted/Program.cs">Blob Encryption Samples</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="9cd73-118">Копирование BLOB-объекта</span><span class="sxs-lookup"><span data-stu-id="9cd73-118">Copy Blob</span></span></td>
<td><span data-ttu-id="9cd73-119"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Приступая к работе с большими двоичными объектами</a></span><span class="sxs-lookup"><span data-stu-id="9cd73-119"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="9cd73-120">Create Container (Создание контейнера)</span><span class="sxs-lookup"><span data-stu-id="9cd73-120">Create Container</span></span></td>
<td><span data-ttu-id="9cd73-121"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Веб-приложение фотоальбома для хранилища BLOB-объектов Azure</a></span><span class="sxs-lookup"><span data-stu-id="9cd73-121"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="9cd73-122">Delete BLOB (Удаление BLOB-объекта)</span><span class="sxs-lookup"><span data-stu-id="9cd73-122">Delete Blob</span></span></td>
<td><span data-ttu-id="9cd73-123"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Веб-приложение фотоальбома для хранилища BLOB-объектов Azure</a></span><span class="sxs-lookup"><span data-stu-id="9cd73-123"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="9cd73-124">Delete Container (Удаление контейнера)</span><span class="sxs-lookup"><span data-stu-id="9cd73-124">Delete Container</span></span></td>
<td><span data-ttu-id="9cd73-125"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Приступая к работе с большими двоичными объектами</a></span><span class="sxs-lookup"><span data-stu-id="9cd73-125"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="9cd73-126">Метаданные, свойства и статистика больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="9cd73-126">Blob Metadata/Properties/Stats</span></span></td>
<td><span data-ttu-id="9cd73-127"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Приступая к работе с большими двоичными объектами</a></span><span class="sxs-lookup"><span data-stu-id="9cd73-127"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="9cd73-128">ACL, метаданные и свойства контейнера</span><span class="sxs-lookup"><span data-stu-id="9cd73-128">Container ACL/Metadata/Properties</span></span></td>
<td><span data-ttu-id="9cd73-129"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Веб-приложение фотоальбома для хранилища BLOB-объектов Azure</a></span><span class="sxs-lookup"><span data-stu-id="9cd73-129"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="9cd73-130">Get Page Ranges (Получение диапазона страницы)</span><span class="sxs-lookup"><span data-stu-id="9cd73-130">Get Page Ranges</span></span></td>
<td><span data-ttu-id="9cd73-131"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Приступая к работе с большими двоичными объектами</a></span><span class="sxs-lookup"><span data-stu-id="9cd73-131"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="9cd73-132">Аренда большого двоичного объекта и контейнера</span><span class="sxs-lookup"><span data-stu-id="9cd73-132">Lease Blob/Container</span></span></td>
<td><span data-ttu-id="9cd73-133"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Приступая к работе с большими двоичными объектами</a></span><span class="sxs-lookup"><span data-stu-id="9cd73-133"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="9cd73-134">Список больших двоичных объектов и контейнеров</span><span class="sxs-lookup"><span data-stu-id="9cd73-134">List Blob/Container</span></span></td>
<td><span data-ttu-id="9cd73-135"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Приступая к работе с большими двоичными объектами</a></span><span class="sxs-lookup"><span data-stu-id="9cd73-135"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="9cd73-136">Страничный BLOB-объект</span><span class="sxs-lookup"><span data-stu-id="9cd73-136">Page Blob</span></span></td>
<td><span data-ttu-id="9cd73-137"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Приступая к работе с большими двоичными объектами</a></span><span class="sxs-lookup"><span data-stu-id="9cd73-137"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Getting Started with Blobs</a></span></span></td>
</tr>
<tr> 
<td><span data-ttu-id="9cd73-138">SAS</span><span class="sxs-lookup"><span data-stu-id="9cd73-138">SAS</span></span></td>
<td><span data-ttu-id="9cd73-139"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Приступая к работе с большими двоичными объектами</a></span><span class="sxs-lookup"><span data-stu-id="9cd73-139"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr>   
<tr> 
<td><span data-ttu-id="9cd73-140">Свойства службы</span><span class="sxs-lookup"><span data-stu-id="9cd73-140">Service Properties</span></span></td>
<td><span data-ttu-id="9cd73-141"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Приступая к работе с большими двоичными объектами</a></span><span class="sxs-lookup"><span data-stu-id="9cd73-141"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr>           
<tr> 
<td><span data-ttu-id="9cd73-142">Создание моментального снимка большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="9cd73-142">Snapshot Blob</span></span></td>
<td><span data-ttu-id="9cd73-143"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-back-up-with-incremental-snapshots/blob/master/Program.cs">Backup Azure Virtual Machine Disks with Incremental Snapshots</a> (Резервное копирование дисков виртуальной машины Azure с помощью добавочных моментальных снимков)</span><span class="sxs-lookup"><span data-stu-id="9cd73-143"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-back-up-with-incremental-snapshots/blob/master/Program.cs">Backup Azure Virtual Machine Disks with Incremental Snapshots</a></span></span></td>
</tr> 
<tr> 
<td rowspan="9"><span data-ttu-id="9cd73-144"><b>File</b></span><span class="sxs-lookup"><span data-stu-id="9cd73-144"><b>File</b></span></span></td>
<td><span data-ttu-id="9cd73-145">Создание общих папок, каталогов и файлов</span><span class="sxs-lookup"><span data-stu-id="9cd73-145">Create Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="9cd73-146"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Пример хранилища файлов .NET для службы хранилища Azure</a></span><span class="sxs-lookup"><span data-stu-id="9cd73-146"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="9cd73-147">Удаление общих папок, каталогов и файлов</span><span class="sxs-lookup"><span data-stu-id="9cd73-147">Delete Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="9cd73-148"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/master/FileStorage/GettingStarted.cs">Приступая к работе со службой файлов Azure в .NET</a></span><span class="sxs-lookup"><span data-stu-id="9cd73-148"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/master/FileStorage/GettingStarted.cs">Getting Started with Azure File Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9cd73-149">Метаданные и свойства каталога</span><span class="sxs-lookup"><span data-stu-id="9cd73-149">Directory Properties/Metadata</span></span></td> 
<td><span data-ttu-id="9cd73-150"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Пример хранилища файлов .NET для службы хранилища Azure</a></span><span class="sxs-lookup"><span data-stu-id="9cd73-150"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9cd73-151">Скачивание файлов</span><span class="sxs-lookup"><span data-stu-id="9cd73-151">Download Files</span></span></td> 
<td><span data-ttu-id="9cd73-152"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Пример хранилища файлов .NET для службы хранилища Azure</a></span><span class="sxs-lookup"><span data-stu-id="9cd73-152"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9cd73-153">Метрики, метаданные и свойства файла</span><span class="sxs-lookup"><span data-stu-id="9cd73-153">File Properties/Metadata/Metrics</span></span></td> 
<td><span data-ttu-id="9cd73-154"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Пример хранилища файлов .NET для службы хранилища Azure</a></span><span class="sxs-lookup"><span data-stu-id="9cd73-154"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9cd73-155">Свойства службы файлов</span><span class="sxs-lookup"><span data-stu-id="9cd73-155">File Service Properties</span></span></td> 
<td><span data-ttu-id="9cd73-156"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Пример хранилища файлов .NET для службы хранилища Azure</a></span><span class="sxs-lookup"><span data-stu-id="9cd73-156"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9cd73-157">Список каталогов и файлов</span><span class="sxs-lookup"><span data-stu-id="9cd73-157">List Directories and Files</span></span></td> 
<td><span data-ttu-id="9cd73-158"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Пример хранилища файлов .NET для службы хранилища Azure</a></span><span class="sxs-lookup"><span data-stu-id="9cd73-158"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="9cd73-159">Список общих папок</span><span class="sxs-lookup"><span data-stu-id="9cd73-159">List Shares</span></span></td> 
<td><span data-ttu-id="9cd73-160"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Пример хранилища файлов .NET для службы хранилища Azure</a></span><span class="sxs-lookup"><span data-stu-id="9cd73-160"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="9cd73-161">Статистика, метаданные и свойства общей папки</span><span class="sxs-lookup"><span data-stu-id="9cd73-161">Share Properties/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="9cd73-162"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Пример хранилища файлов .NET для службы хранилища Azure</a></span><span class="sxs-lookup"><span data-stu-id="9cd73-162"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td rowspan="8"><span data-ttu-id="9cd73-163"><b>Очередь</b></span><span class="sxs-lookup"><span data-stu-id="9cd73-163"><b>Queue</b></span></span></td>
<td><span data-ttu-id="9cd73-164">Добавление сообщения</span><span class="sxs-lookup"><span data-stu-id="9cd73-164">Add Message</span></span></td> 
<td><span data-ttu-id="9cd73-165"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Приступая к работе со службой очередей Azure в .NET</a></span><span class="sxs-lookup"><span data-stu-id="9cd73-165"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9cd73-166">Шифрование на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="9cd73-166">Client-Side Encryption</span></span></td> 
<td><span data-ttu-id="9cd73-167"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/QueueGettingStarted/Program.cs">Очередь шифрования на стороне клиента .NET для службы хранилища Azure</a></span><span class="sxs-lookup"><span data-stu-id="9cd73-167"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/QueueGettingStarted/Program.cs">Azure Storage .NET Queue Client-Side Encryption</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9cd73-168">Создание очередей</span><span class="sxs-lookup"><span data-stu-id="9cd73-168">Create Queues</span></span></td> 
<td><span data-ttu-id="9cd73-169"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Приступая к работе со службой очередей Azure в .NET</a></span><span class="sxs-lookup"><span data-stu-id="9cd73-169"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9cd73-170">Удаление сообщения и очереди</span><span class="sxs-lookup"><span data-stu-id="9cd73-170">Delete Message/Queue</span></span></td> 
<td><span data-ttu-id="9cd73-171"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Приступая к работе со службой очередей Azure в .NET</a></span><span class="sxs-lookup"><span data-stu-id="9cd73-171"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9cd73-172">Просмотр сообщения</span><span class="sxs-lookup"><span data-stu-id="9cd73-172">Peek Message</span></span></td> 
<td><span data-ttu-id="9cd73-173"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Приступая к работе со службой очередей Azure в .NET</a></span><span class="sxs-lookup"><span data-stu-id="9cd73-173"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9cd73-174">ACL, метаданные и статистика очереди</span><span class="sxs-lookup"><span data-stu-id="9cd73-174">Queue ACL/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="9cd73-175"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Приступая к работе со службой очередей Azure в .NET</a></span><span class="sxs-lookup"><span data-stu-id="9cd73-175"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9cd73-176">Свойства службы очередей</span><span class="sxs-lookup"><span data-stu-id="9cd73-176">Queue Service Properties</span></span></td> 
<td><span data-ttu-id="9cd73-177"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Приступая к работе со службой очередей Azure в .NET</a></span><span class="sxs-lookup"><span data-stu-id="9cd73-177"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9cd73-178">Сообщение об обновлении</span><span class="sxs-lookup"><span data-stu-id="9cd73-178">Update Message</span></span></td> 
<td><span data-ttu-id="9cd73-179"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Приступая к работе со службой очередей Azure в .NET</a></span><span class="sxs-lookup"><span data-stu-id="9cd73-179"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td rowspan="7"><span data-ttu-id="9cd73-180"><b>Таблица</b></span><span class="sxs-lookup"><span data-stu-id="9cd73-180"><b>Table</b></span></span></td>
<td><span data-ttu-id="9cd73-181">Создание таблицы</span><span class="sxs-lookup"><span data-stu-id="9cd73-181">Create Table</span></span></td> 
<td><span data-ttu-id="9cd73-182"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Управление параллелизмом с помощью службы хранилища Azure: пример приложения</a></span><span class="sxs-lookup"><span data-stu-id="9cd73-182"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9cd73-183">Удаление сущности или таблицы</span><span class="sxs-lookup"><span data-stu-id="9cd73-183">Delete Entity/Table</span></span></td> 
<td><span data-ttu-id="9cd73-184"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a> (Приступая к работе с хранилищем таблиц Azure в .NET)</span><span class="sxs-lookup"><span data-stu-id="9cd73-184"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9cd73-185">Вставка, слияние или замена сущностей</span><span class="sxs-lookup"><span data-stu-id="9cd73-185">Insert/Merge/Replace Entity</span></span></td> 
<td><span data-ttu-id="9cd73-186"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Управление параллелизмом с помощью службы хранилища Azure: пример приложения</a></span><span class="sxs-lookup"><span data-stu-id="9cd73-186"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9cd73-187">Query Entities (Сущности запроса)</span><span class="sxs-lookup"><span data-stu-id="9cd73-187">Query Entities</span></span></td> 
<td><span data-ttu-id="9cd73-188"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a> (Приступая к работе с хранилищем таблиц Azure в .NET)</span><span class="sxs-lookup"><span data-stu-id="9cd73-188"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9cd73-189">Запросы к таблицам</span><span class="sxs-lookup"><span data-stu-id="9cd73-189">Query Tables</span></span></td> 
<td><span data-ttu-id="9cd73-190"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a> (Приступая к работе с хранилищем таблиц Azure в .NET)</span><span class="sxs-lookup"><span data-stu-id="9cd73-190"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9cd73-191">Свойства и ACL таблицы</span><span class="sxs-lookup"><span data-stu-id="9cd73-191">Table ACL/Properties</span></span></td> 
<td><span data-ttu-id="9cd73-192"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/AdvancedSamples.cs">Getting Started with Azure Table Storage in .NET</a> (Приступая к работе с хранилищем таблиц Azure в .NET)</span><span class="sxs-lookup"><span data-stu-id="9cd73-192"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/AdvancedSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9cd73-193">Update Entity (Обновление сущности)</span><span class="sxs-lookup"><span data-stu-id="9cd73-193">Update Entity</span></span></td> 
<td><span data-ttu-id="9cd73-194"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Управление параллелизмом с помощью службы хранилища Azure: пример приложения</a></span><span class="sxs-lookup"><span data-stu-id="9cd73-194"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
</tbody> 
</table>
<br/>

## <a name="azure-code-samples-library"></a><span data-ttu-id="9cd73-195">Библиотека примеров кода Azure</span><span class="sxs-lookup"><span data-stu-id="9cd73-195">Azure Code Samples library</span></span>

<span data-ttu-id="9cd73-196">Чтобы просмотреть полную библиотеку примеров, перейдите в [библиотеку примеров кода Azure](https://azure.microsoft.com/resources/samples/?service=storage), включающую примеры для службы хранилища Azure, которые можно скачать и запустить локально.</span><span class="sxs-lookup"><span data-stu-id="9cd73-196">To view the complete sample library, go to the [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=storage) library, which includes samples for Azure Storage that you can download and run locally.</span></span> <span data-ttu-id="9cd73-197">Пример библиотеки кода содержит пример кода в формате ZIP.</span><span class="sxs-lookup"><span data-stu-id="9cd73-197">The Code Sample Library provides sample code in .zip format.</span></span> <span data-ttu-id="9cd73-198">Кроме того, можно просмотреть и клонировать репозиторий GitHub для каждого примера.</span><span class="sxs-lookup"><span data-stu-id="9cd73-198">Alternatively, you can browse and clone the GitHub repository for each sample.</span></span>

[!INCLUDE [storage-dotnet-samples-include](../../includes/storage-dotnet-samples-include.md)]

## <a name="getting-started-guides"></a><span data-ttu-id="9cd73-199">Руководства по началу работы</span><span class="sxs-lookup"><span data-stu-id="9cd73-199">Getting started guides</span></span>

<span data-ttu-id="9cd73-200">Ознакомьтесь со следующими руководствами, если вам нужны инструкции по установке клиентских библиотек службы хранилища Azure и началу работы с ними.</span><span class="sxs-lookup"><span data-stu-id="9cd73-200">Check out the following guides if you are looking for instructions on how to install and get started with the Azure Storage Client Libraries.</span></span>

* [<span data-ttu-id="9cd73-201">Приступая к работе со службой BLOB-объектов Azure в .NET</span><span class="sxs-lookup"><span data-stu-id="9cd73-201">Getting Started with Azure Blob Service in .NET</span></span>](storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="9cd73-202">Приступая к работе со службой очередей Azure в .NET</span><span class="sxs-lookup"><span data-stu-id="9cd73-202">Getting Started with Azure Queue Service in .NET</span></span>](storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="9cd73-203">Приступая к работе со службой таблиц Azure в .NET</span><span class="sxs-lookup"><span data-stu-id="9cd73-203">Getting Started with Azure Table Service in .NET</span></span>](storage-dotnet-how-to-use-tables.md)
* [<span data-ttu-id="9cd73-204">Приступая к работе со службой файлов Azure в .NET</span><span class="sxs-lookup"><span data-stu-id="9cd73-204">Getting Started with Azure File Service in .NET</span></span>](storage-dotnet-how-to-use-files.md)

## <a name="next-steps"></a><span data-ttu-id="9cd73-205">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9cd73-205">Next steps</span></span>

<span data-ttu-id="9cd73-206">Дополнительные сведения о примерах для других языков см. здесь:</span><span class="sxs-lookup"><span data-stu-id="9cd73-206">For information on samples for other languages:</span></span>

* <span data-ttu-id="9cd73-207">Java: [Azure Storage samples using Java](storage-samples-java.md) (Примеры для службы хранилища Azure с использованием Java)</span><span class="sxs-lookup"><span data-stu-id="9cd73-207">Java: [Azure Storage samples using Java](storage-samples-java.md)</span></span>
* <span data-ttu-id="9cd73-208">Все остальные языки: [Azure Storage samples](storage-samples.md) (Примеры для службы хранилища Azure)</span><span class="sxs-lookup"><span data-stu-id="9cd73-208">All other languages: [Azure Storage samples](storage-samples.md)</span></span>
