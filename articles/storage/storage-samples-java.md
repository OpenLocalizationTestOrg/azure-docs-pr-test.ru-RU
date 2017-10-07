---
title: "Примеры для хранилища aaaAzure с помощью Java | Документы Microsoft"
description: "Просмотрите, загрузите и запустите образцы кода и приложений для хранилища Azure. Обнаружение, Приступая к работе образцы для больших двоичных объектов, очередей, таблиц и файлов, с помощью клиентских библиотек хранилища hello Java."
services: storage
documentationcenter: na
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 01/12/2017
ms.author: seguler
ms.openlocfilehash: e3b8fbe86e82dd58c2a13a3c68760cbf6e9a6e4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-samples-using-java"></a><span data-ttu-id="9c6ba-104">Примеры для службы хранилища Azure с использованием Java</span><span class="sxs-lookup"><span data-stu-id="9c6ba-104">Azure Storage samples using Java</span></span>

## <a name="java-sample-index"></a><span data-ttu-id="9c6ba-105">Указатель по примерам для Java</span><span class="sxs-lookup"><span data-stu-id="9c6ba-105">Java sample index</span></span>

<span data-ttu-id="9c6ba-106">Hello следующей таблице представлены общие сведения о наши примеры репозитория и hello сценарии, описанные в каждой выборке.</span><span class="sxs-lookup"><span data-stu-id="9c6ba-106">hello following table provides an overview of our samples repository and hello scenarios covered in each sample.</span></span> <span data-ttu-id="9c6ba-107">Щелкните hello ссылки tooview hello соответствующие примеры кода в GitHub.</span><span class="sxs-lookup"><span data-stu-id="9c6ba-107">Click on hello links tooview hello corresponding sample code in GitHub.</span></span>

<table style="font-size:90%"><thead><tr><th style="font-size:110%"><span data-ttu-id="9c6ba-108">Конечная точка</span><span class="sxs-lookup"><span data-stu-id="9c6ba-108">Endpoint</span></span></th><th style="font-size:110%"><span data-ttu-id="9c6ba-109">Сценарий</span><span class="sxs-lookup"><span data-stu-id="9c6ba-109">Scenario</span></span></th><th style="font-size:110%"><span data-ttu-id="9c6ba-110">Пример кода</span><span class="sxs-lookup"><span data-stu-id="9c6ba-110">Sample Code</span></span></th></tr></thead><tbody> 
<tr> 
<td rowspan="16"><span data-ttu-id="9c6ba-111"><b>Большой двоичный объект</b></span><span class="sxs-lookup"><span data-stu-id="9c6ba-111"><b>Blob</b></span></span></td>
<td><span data-ttu-id="9c6ba-112">Добавление больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="9c6ba-112">Append Blob</span></span></td> 
<td><span data-ttu-id="9c6ba-113"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Приступая к работе со службой BLOB-объектов Azure на языке Java)</span><span class="sxs-lookup"><span data-stu-id="9c6ba-113"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9c6ba-114">Блочный BLOB-объект</span><span class="sxs-lookup"><span data-stu-id="9c6ba-114">Block Blob</span></span></td>
<td><span data-ttu-id="9c6ba-115"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Приступая к работе со службой BLOB-объектов Azure на языке Java)</span><span class="sxs-lookup"><span data-stu-id="9c6ba-115"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="9c6ba-116">Шифрование на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="9c6ba-116">Client-Side Encryption</span></span></td>
<td><span data-ttu-id="9c6ba-117"><a href="https://github.com/Azure-Samples/storage-java-client-side-encryption">Приступая к работе с шифрованием на стороне клиента Azure в Java</a></span><span class="sxs-lookup"><span data-stu-id="9c6ba-117"><a href="https://github.com/Azure-Samples/storage-java-client-side-encryption">Getting Started with Azure Client Side Encryption in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="9c6ba-118">Копирование BLOB-объекта</span><span class="sxs-lookup"><span data-stu-id="9c6ba-118">Copy Blob</span></span></td>
<td><span data-ttu-id="9c6ba-119"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Приступая к работе со службой BLOB-объектов Azure на языке Java)</span><span class="sxs-lookup"><span data-stu-id="9c6ba-119"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="9c6ba-120">Create Container (Создание контейнера)</span><span class="sxs-lookup"><span data-stu-id="9c6ba-120">Create Container</span></span></td>
<td><span data-ttu-id="9c6ba-121"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Приступая к работе со службой BLOB-объектов Azure на языке Java)</span><span class="sxs-lookup"><span data-stu-id="9c6ba-121"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="9c6ba-122">Delete BLOB (Удаление BLOB-объекта)</span><span class="sxs-lookup"><span data-stu-id="9c6ba-122">Delete Blob</span></span></td>
<td><span data-ttu-id="9c6ba-123"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Приступая к работе со службой BLOB-объектов Azure на языке Java)</span><span class="sxs-lookup"><span data-stu-id="9c6ba-123"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="9c6ba-124">Delete Container (Удаление контейнера)</span><span class="sxs-lookup"><span data-stu-id="9c6ba-124">Delete Container</span></span></td>
<td><span data-ttu-id="9c6ba-125"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Приступая к работе со службой BLOB-объектов Azure на языке Java)</span><span class="sxs-lookup"><span data-stu-id="9c6ba-125"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="9c6ba-126">Метаданные, свойства и статистика больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="9c6ba-126">Blob Metadata/Properties/Stats</span></span></td>
<td><span data-ttu-id="9c6ba-127"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a> (Приступая к работе со службой BLOB-объектов Azure на языке Java)</span><span class="sxs-lookup"><span data-stu-id="9c6ba-127"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="9c6ba-128">ACL, метаданные и свойства контейнера</span><span class="sxs-lookup"><span data-stu-id="9c6ba-128">Container ACL/Metadata/Properties</span></span></td>
<td><span data-ttu-id="9c6ba-129"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a> (Приступая к работе со службой BLOB-объектов Azure на языке Java)</span><span class="sxs-lookup"><span data-stu-id="9c6ba-129"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="9c6ba-130">Get Page Ranges (Получение диапазона страницы)</span><span class="sxs-lookup"><span data-stu-id="9c6ba-130">Get Page Ranges</span></span></td>
<td><span data-ttu-id="9c6ba-131"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/CloudPageBlobTests.java">Пример тестов страничного BLOB-объекта</a></span><span class="sxs-lookup"><span data-stu-id="9c6ba-131"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/CloudPageBlobTests.java">Page Blob Tests Sample</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="9c6ba-132">Аренда большого двоичного объекта и контейнера</span><span class="sxs-lookup"><span data-stu-id="9c6ba-132">Lease Blob/Container</span></span></td>
<td><span data-ttu-id="9c6ba-133"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Приступая к работе со службой BLOB-объектов Azure на языке Java)</span><span class="sxs-lookup"><span data-stu-id="9c6ba-133"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="9c6ba-134">Список больших двоичных объектов и контейнеров</span><span class="sxs-lookup"><span data-stu-id="9c6ba-134">List Blob/Container</span></span></td>
<td><span data-ttu-id="9c6ba-135"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Приступая к работе со службой BLOB-объектов Azure на языке Java)</span><span class="sxs-lookup"><span data-stu-id="9c6ba-135"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="9c6ba-136">Страничный BLOB-объект</span><span class="sxs-lookup"><span data-stu-id="9c6ba-136">Page Blob</span></span></td>
<td><span data-ttu-id="9c6ba-137"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Приступая к работе со службой BLOB-объектов Azure на языке Java)</span><span class="sxs-lookup"><span data-stu-id="9c6ba-137"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr>
<tr> 
<td><span data-ttu-id="9c6ba-138">SAS</span><span class="sxs-lookup"><span data-stu-id="9c6ba-138">SAS</span></span></td>
<td><span data-ttu-id="9c6ba-139"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/SasTests.java">Пример тестов SAS</a></span><span class="sxs-lookup"><span data-stu-id="9c6ba-139"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/SasTests.java">SAS Tests Sample</a></span></span></td>
</tr>   
<tr> 
<td><span data-ttu-id="9c6ba-140">Свойства службы</span><span class="sxs-lookup"><span data-stu-id="9c6ba-140">Service Properties</span></span></td>
<td><span data-ttu-id="9c6ba-141"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a> (Приступая к работе со службой BLOB-объектов Azure на языке Java)</span><span class="sxs-lookup"><span data-stu-id="9c6ba-141"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr>           
<tr> 
<td><span data-ttu-id="9c6ba-142">Создание моментального снимка большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="9c6ba-142">Snapshot Blob</span></span></td>
<td><span data-ttu-id="9c6ba-143"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Приступая к работе со службой BLOB-объектов Azure на языке Java)</span><span class="sxs-lookup"><span data-stu-id="9c6ba-143"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td rowspan="9"><span data-ttu-id="9c6ba-144"><b>File</b></span><span class="sxs-lookup"><span data-stu-id="9c6ba-144"><b>File</b></span></span></td>
<td><span data-ttu-id="9c6ba-145">Создание общих папок, каталогов и файлов</span><span class="sxs-lookup"><span data-stu-id="9c6ba-145">Create Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="9c6ba-146"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a> (Приступая к работе с файловой службой Azure на языке Java)</span><span class="sxs-lookup"><span data-stu-id="9c6ba-146"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="9c6ba-147">Удаление общих папок, каталогов и файлов</span><span class="sxs-lookup"><span data-stu-id="9c6ba-147">Delete Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="9c6ba-148"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a> (Приступая к работе с файловой службой Azure на языке Java)</span><span class="sxs-lookup"><span data-stu-id="9c6ba-148"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9c6ba-149">Метаданные и свойства каталога</span><span class="sxs-lookup"><span data-stu-id="9c6ba-149">Directory Properties/Metadata</span></span></td> 
<td><span data-ttu-id="9c6ba-150"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a> (Приступая к работе с файловой службой Azure на языке Java)</span><span class="sxs-lookup"><span data-stu-id="9c6ba-150"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9c6ba-151">Скачивание файлов</span><span class="sxs-lookup"><span data-stu-id="9c6ba-151">Download Files</span></span></td> 
<td><span data-ttu-id="9c6ba-152"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a> (Приступая к работе с файловой службой Azure на языке Java)</span><span class="sxs-lookup"><span data-stu-id="9c6ba-152"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9c6ba-153">Метрики, метаданные и свойства файла</span><span class="sxs-lookup"><span data-stu-id="9c6ba-153">File Properties/Metadata/Metrics</span></span></td> 
<td><span data-ttu-id="9c6ba-154"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a> (Приступая к работе с файловой службой Azure на языке Java)</span><span class="sxs-lookup"><span data-stu-id="9c6ba-154"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9c6ba-155">Свойства службы файлов</span><span class="sxs-lookup"><span data-stu-id="9c6ba-155">File Service Properties</span></span></td> 
<td><span data-ttu-id="9c6ba-156"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a> (Приступая к работе с файловой службой Azure на языке Java)</span><span class="sxs-lookup"><span data-stu-id="9c6ba-156"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9c6ba-157">Список каталогов и файлов</span><span class="sxs-lookup"><span data-stu-id="9c6ba-157">List Directories and Files</span></span></td> 
<td><span data-ttu-id="9c6ba-158"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a> (Приступая к работе с файловой службой Azure на языке Java)</span><span class="sxs-lookup"><span data-stu-id="9c6ba-158"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="9c6ba-159">Список общих папок</span><span class="sxs-lookup"><span data-stu-id="9c6ba-159">List Shares</span></span></td> 
<td><span data-ttu-id="9c6ba-160"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a> (Приступая к работе с файловой службой Azure на языке Java)</span><span class="sxs-lookup"><span data-stu-id="9c6ba-160"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="9c6ba-161">Статистика, метаданные и свойства общей папки</span><span class="sxs-lookup"><span data-stu-id="9c6ba-161">Share Properties/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="9c6ba-162"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a> (Приступая к работе с файловой службой Azure на языке Java)</span><span class="sxs-lookup"><span data-stu-id="9c6ba-162"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td rowspan="8"><span data-ttu-id="9c6ba-163"><b>Очередь</b></span><span class="sxs-lookup"><span data-stu-id="9c6ba-163"><b>Queue</b></span></span></td>
<td><span data-ttu-id="9c6ba-164">Добавление сообщения</span><span class="sxs-lookup"><span data-stu-id="9c6ba-164">Add Message</span></span></td> 
<td><span data-ttu-id="9c6ba-165"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/queue/gettingstarted/QueueBasics.java">Примеры для клиентской библиотеки хранилища Azure для Java</a></span><span class="sxs-lookup"><span data-stu-id="9c6ba-165"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/queue/gettingstarted/QueueBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9c6ba-166">Шифрование на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="9c6ba-166">Client-Side Encryption</span></span></td> 
<td><span data-ttu-id="9c6ba-167"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/encryption/queue/gettingstarted/QueueGettingStarted.java">Примеры для клиентской библиотеки хранилища Azure для Java</a></span><span class="sxs-lookup"><span data-stu-id="9c6ba-167"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/encryption/queue/gettingstarted/QueueGettingStarted.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9c6ba-168">Создание очередей</span><span class="sxs-lookup"><span data-stu-id="9c6ba-168">Create Queues</span></span></td> 
<td><span data-ttu-id="9c6ba-169"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a> (Приступая к работе со службой очередей Azure на языке Java)</span><span class="sxs-lookup"><span data-stu-id="9c6ba-169"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9c6ba-170">Удаление сообщения и очереди</span><span class="sxs-lookup"><span data-stu-id="9c6ba-170">Delete Message/Queue</span></span></td> 
<td><span data-ttu-id="9c6ba-171"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a> (Приступая к работе со службой очередей Azure на языке Java)</span><span class="sxs-lookup"><span data-stu-id="9c6ba-171"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9c6ba-172">Просмотр сообщения</span><span class="sxs-lookup"><span data-stu-id="9c6ba-172">Peek Message</span></span></td> 
<td><span data-ttu-id="9c6ba-173"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a> (Приступая к работе со службой очередей Azure на языке Java)</span><span class="sxs-lookup"><span data-stu-id="9c6ba-173"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9c6ba-174">ACL, метаданные и статистика очереди</span><span class="sxs-lookup"><span data-stu-id="9c6ba-174">Queue ACL/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="9c6ba-175"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java</a> (Приступая к работе со службой очередей Azure на языке Java)</span><span class="sxs-lookup"><span data-stu-id="9c6ba-175"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9c6ba-176">Свойства службы очередей</span><span class="sxs-lookup"><span data-stu-id="9c6ba-176">Queue Service Properties</span></span></td> 
<td><span data-ttu-id="9c6ba-177"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java</a> (Приступая к работе со службой очередей Azure на языке Java)</span><span class="sxs-lookup"><span data-stu-id="9c6ba-177"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9c6ba-178">Сообщение об обновлении</span><span class="sxs-lookup"><span data-stu-id="9c6ba-178">Update Message</span></span></td> 
<td><span data-ttu-id="9c6ba-179"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a> (Приступая к работе со службой очередей Azure на языке Java)</span><span class="sxs-lookup"><span data-stu-id="9c6ba-179"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td rowspan="7"><span data-ttu-id="9c6ba-180"><b>Таблица</b></span><span class="sxs-lookup"><span data-stu-id="9c6ba-180"><b>Table</b></span></span></td>
<td><span data-ttu-id="9c6ba-181">Создание таблицы</span><span class="sxs-lookup"><span data-stu-id="9c6ba-181">Create Table</span></span></td> 
<td><span data-ttu-id="9c6ba-182"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a> (Приступая к работе со службой таблиц Azure на языке Java)</span><span class="sxs-lookup"><span data-stu-id="9c6ba-182"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9c6ba-183">Удаление сущности или таблицы</span><span class="sxs-lookup"><span data-stu-id="9c6ba-183">Delete Entity/Table</span></span></td> 
<td><span data-ttu-id="9c6ba-184"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a> (Приступая к работе со службой таблиц Azure на языке Java)</span><span class="sxs-lookup"><span data-stu-id="9c6ba-184"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9c6ba-185">Вставка, слияние или замена сущностей</span><span class="sxs-lookup"><span data-stu-id="9c6ba-185">Insert/Merge/Replace Entity</span></span></td> 
<td><span data-ttu-id="9c6ba-186"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Примеры для клиентской библиотеки хранилища Azure для Java</a></span><span class="sxs-lookup"><span data-stu-id="9c6ba-186"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9c6ba-187">Query Entities (Сущности запроса)</span><span class="sxs-lookup"><span data-stu-id="9c6ba-187">Query Entities</span></span></td> 
<td><span data-ttu-id="9c6ba-188"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a> (Приступая к работе со службой таблиц Azure на языке Java)</span><span class="sxs-lookup"><span data-stu-id="9c6ba-188"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9c6ba-189">Запросы к таблицам</span><span class="sxs-lookup"><span data-stu-id="9c6ba-189">Query Tables</span></span></td> 
<td><span data-ttu-id="9c6ba-190"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a> (Приступая к работе со службой таблиц Azure на языке Java)</span><span class="sxs-lookup"><span data-stu-id="9c6ba-190"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9c6ba-191">Свойства и ACL таблицы</span><span class="sxs-lookup"><span data-stu-id="9c6ba-191">Table ACL/Properties</span></span></td> 
<td><span data-ttu-id="9c6ba-192"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableAdvanced.java">Getting Started with Azure Table Service in Java</a> (Приступая к работе со службой таблиц Azure на языке Java)</span><span class="sxs-lookup"><span data-stu-id="9c6ba-192"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableAdvanced.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="9c6ba-193">Update Entity (Обновление сущности)</span><span class="sxs-lookup"><span data-stu-id="9c6ba-193">Update Entity</span></span></td> 
<td><span data-ttu-id="9c6ba-194"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Примеры для клиентской библиотеки хранилища Azure для Java</a></span><span class="sxs-lookup"><span data-stu-id="9c6ba-194"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
</tbody> 
</table>
<br/>

## <a name="azure-code-samples-library"></a><span data-ttu-id="9c6ba-195">Библиотека примеров кода Azure</span><span class="sxs-lookup"><span data-stu-id="9c6ba-195">Azure Code Samples library</span></span>

<span data-ttu-id="9c6ba-196">Полный образец библиотеки tooview hello перейдите toohello [образцы кода Azure](https://azure.microsoft.com/resources/samples/?service=storage) библиотеку, которая включает примеры для хранилища Azure, можно загрузить и запустить его локально.</span><span class="sxs-lookup"><span data-stu-id="9c6ba-196">tooview hello complete sample library, go toohello [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=storage) library, which includes samples for Azure Storage that you can download and run locally.</span></span> <span data-ttu-id="9c6ba-197">Hello кода образца библиотеки содержит пример кода в формате ZIP.</span><span class="sxs-lookup"><span data-stu-id="9c6ba-197">hello Code Sample Library provides sample code in .zip format.</span></span> <span data-ttu-id="9c6ba-198">Кроме того можно просмотреть и клонирование репозитория GitHub hello для каждого образца.</span><span class="sxs-lookup"><span data-stu-id="9c6ba-198">Alternatively, you can browse and clone hello GitHub repository for each sample.</span></span>

[!INCLUDE [storage-java-samples-include](../../includes/storage-java-samples-include.md)]

## <a name="getting-started-guides"></a><span data-ttu-id="9c6ba-199">Руководства по началу работы</span><span class="sxs-lookup"><span data-stu-id="9c6ba-199">Getting started guides</span></span>

<span data-ttu-id="9c6ba-200">Извлечение hello следующие руководства, если вам нужны дополнительные сведения о tooinstall и приступить к работе с hello клиентских библиотек хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="9c6ba-200">Check out hello following guides if you are looking for instructions on how tooinstall and get started with hello Azure Storage Client Libraries.</span></span>

* <span data-ttu-id="9c6ba-201">[Getting Started with Azure Blob Service in Java](storage-java-how-to-use-blob-storage.md) (Приступая к работе со службой BLOB-объектов Azure на языке Java)</span><span class="sxs-lookup"><span data-stu-id="9c6ba-201">[Getting Started with Azure Blob Service in Java](storage-java-how-to-use-blob-storage.md)</span></span>
* <span data-ttu-id="9c6ba-202">[Getting Started with Azure Queue Service in Java](storage-java-how-to-use-queue-storage.md) (Приступая к работе со службой очередей Azure на языке Java)</span><span class="sxs-lookup"><span data-stu-id="9c6ba-202">[Getting Started with Azure Queue Service in Java](storage-java-how-to-use-queue-storage.md)</span></span>
* <span data-ttu-id="9c6ba-203">[Getting Started with Azure Table Service in Java](storage-java-how-to-use-table-storage.md) (Приступая к работе со службой таблиц Azure на языке Java)</span><span class="sxs-lookup"><span data-stu-id="9c6ba-203">[Getting Started with Azure Table Service in Java](storage-java-how-to-use-table-storage.md)</span></span>
* <span data-ttu-id="9c6ba-204">[Getting Started with Azure File Service in Java](storage-java-how-to-use-file-storage.md) (Приступая к работе с файловой службой Azure на языке Java)</span><span class="sxs-lookup"><span data-stu-id="9c6ba-204">[Getting Started with Azure File Service in Java](storage-java-how-to-use-file-storage.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c6ba-205">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9c6ba-205">Next steps</span></span>

<span data-ttu-id="9c6ba-206">Дополнительные сведения о примерах для других языков см. здесь:</span><span class="sxs-lookup"><span data-stu-id="9c6ba-206">For information on samples for other languages:</span></span>

* <span data-ttu-id="9c6ba-207">.NET: [Azure Storage samples using .NET](storage-samples-dotnet.md) (Примеры для службы хранилища Azure с использованием .NET)</span><span class="sxs-lookup"><span data-stu-id="9c6ba-207">.NET: [Azure Storage samples using .NET](storage-samples-dotnet.md)</span></span>
* <span data-ttu-id="9c6ba-208">Все остальные языки: [Azure Storage samples](storage-samples.md) (Примеры для службы хранилища Azure)</span><span class="sxs-lookup"><span data-stu-id="9c6ba-208">All other languages: [Azure Storage samples](storage-samples.md)</span></span>
