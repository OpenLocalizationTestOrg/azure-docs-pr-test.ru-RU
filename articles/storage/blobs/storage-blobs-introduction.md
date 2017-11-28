---
title: "aaaIntroduction tooAzure хранилища больших двоичных объектов | Документы Microsoft"
description: "Введение tooAzure хранилища больших двоичных объектов"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: robinsh
ms.openlocfilehash: 3431f826ae51d42dbced084ee60f9ff70a8168d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooblob-storage"></a><span data-ttu-id="d00e6-103">Введение tooBlob хранилища</span><span class="sxs-lookup"><span data-stu-id="d00e6-103">Introduction tooBlob storage</span></span>

<span data-ttu-id="d00e6-104">Хранилище Azure BLOB-объекта — это служба для хранения больших объемов данных неструктурированных объектов, таких как текст или двоичные данные, который может осуществляться из любого места в Здравствуй, мир! через HTTP или HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d00e6-104">Azure Blob storage is a service for storing large amounts of unstructured object data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="d00e6-105">Данные tooexpose хранилища больших двоичных объектов можно использовать публично world toohello или toostore данные приложения в частном порядке.</span><span class="sxs-lookup"><span data-stu-id="d00e6-105">You can use Blob storage tooexpose data publicly toohello world, or toostore application data privately.</span></span>

<span data-ttu-id="d00e6-106">Наиболее частые способы использования хранилища BLOB-объектов:</span><span class="sxs-lookup"><span data-stu-id="d00e6-106">Common uses of Blob storage include:</span></span>

* <span data-ttu-id="d00e6-107">Обслуживание образов или непосредственно документов tooa браузера</span><span class="sxs-lookup"><span data-stu-id="d00e6-107">Serving images or documents directly tooa browser</span></span>
* <span data-ttu-id="d00e6-108">Хранение файлов для распределенного доступа.</span><span class="sxs-lookup"><span data-stu-id="d00e6-108">Storing files for distributed access</span></span>
* <span data-ttu-id="d00e6-109">Потоковая передача видео и аудио.</span><span class="sxs-lookup"><span data-stu-id="d00e6-109">Streaming video and audio</span></span>
* <span data-ttu-id="d00e6-110">Хранение резервных копий и восстановление данных, аварийное восстановление и архивация</span><span class="sxs-lookup"><span data-stu-id="d00e6-110">Storing data for backup and restore, disaster recovery, and archiving</span></span>
* <span data-ttu-id="d00e6-111">Хранение данных для анализа локальной службой или службой, размещенной в Azure</span><span class="sxs-lookup"><span data-stu-id="d00e6-111">Storing data for analysis by an on-premises or Azure-hosted service</span></span>

## <a name="blob-service-concepts"></a><span data-ttu-id="d00e6-112">Основные понятия службы BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="d00e6-112">Blob service concepts</span></span>

<span data-ttu-id="d00e6-113">Hello службы BLOB-объектов содержит hello следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="d00e6-113">hello Blob service contains hello following components:</span></span>

![Архитектура большого двоичного объекта](./media/storage-blobs-introduction/blob1.png)

* <span data-ttu-id="d00e6-115">**Учетная запись хранения:** обращаться к tooAzure хранилища осуществляется через учетную запись хранилища.</span><span class="sxs-lookup"><span data-stu-id="d00e6-115">**Storage Account:** All access tooAzure Storage is done through a storage account.</span></span> <span data-ttu-id="d00e6-116">Это может быть **учетная запись хранения общего назначения** или **учетная запись хранилища BLOB-объектов**, специально предназначенная для хранения больших двоичных объектов и других объектов.</span><span class="sxs-lookup"><span data-stu-id="d00e6-116">This storage account can be a **General-purpose storage account** or a **Blob storage account** that is specialized for storing objects/blobs.</span></span> <span data-ttu-id="d00e6-117">См. дополнительные сведения [об учетных записях хранения Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d00e6-117">See [About Azure storage accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) for more information.</span></span>

* <span data-ttu-id="d00e6-118">**Контейнер**. В контейнере группируется набор BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="d00e6-118">**Container:** A container provides a grouping of a set of blobs.</span></span> <span data-ttu-id="d00e6-119">Все BLOB-объекты должны содержаться в контейнере.</span><span class="sxs-lookup"><span data-stu-id="d00e6-119">All blobs must be in a container.</span></span> <span data-ttu-id="d00e6-120">Учетная запись может содержать неограниченное число контейнеров.</span><span class="sxs-lookup"><span data-stu-id="d00e6-120">An account can contain an unlimited number of containers.</span></span> <span data-ttu-id="d00e6-121">Контейнер может хранить неограниченное количество больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="d00e6-121">A container can store an unlimited number of blobs.</span></span> <span data-ttu-id="d00e6-122">Обратите внимание, что имя контейнера hello должны быть строчными.</span><span class="sxs-lookup"><span data-stu-id="d00e6-122">Note that hello container name must be lowercase.</span></span>

* <span data-ttu-id="d00e6-123">**BLOB-объект**. Файл любого типа и размера.</span><span class="sxs-lookup"><span data-stu-id="d00e6-123">**Blob:** A file of any type and size.</span></span> <span data-ttu-id="d00e6-124">Служба хранилища Azure предлагает три типа больших двоичных объектов: блочные, страничные и добавочные.</span><span class="sxs-lookup"><span data-stu-id="d00e6-124">Azure Storage offers three types of blobs: block blobs, page blobs, and append blobs.</span></span>
  
    <span data-ttu-id="d00e6-125">*Блочные BLOB-объекты* идеально подходят для хранения текстовых и двоичных файлов, таких как документы и файлы мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="d00e6-125">*Block blobs* are ideal for storing text or binary files, such as documents and media files.</span></span> <span data-ttu-id="d00e6-126">*Добавление BLOB-объектов* являются аналогичные tooblock большие двоичные объекты, они состоят из блоков, но они должны быть оптимизированы для операций добавления, поэтому они могут использоваться для сценариев ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="d00e6-126">*Append blobs* are similar tooblock blobs in that they are made up of blocks, but they are optimized for append operations, so they are useful for logging scenarios.</span></span> <span data-ttu-id="d00e6-127">Одного большого двоичного объекта может содержать копию too50 000 блоков вверх too100 МБ, до общего размера более чем 4,75 ТБ (100 МБ X 50 000).</span><span class="sxs-lookup"><span data-stu-id="d00e6-127">A single block blob can contain up too50,000 blocks of up too100 MB each, for a total size of slightly more than 4.75 TB (100 MB X 50,000).</span></span> <span data-ttu-id="d00e6-128">Один добавочный большой двоичный объект может содержать копию too50 000 блоков вверх too4 МБ, до общего размера более чем 195 ГБ (4 МБ X 50 000).</span><span class="sxs-lookup"><span data-stu-id="d00e6-128">A single append blob can contain up too50,000 blocks of up too4 MB each, for a total size of slightly more than 195 GB (4 MB X 50,000).</span></span>
  
    <span data-ttu-id="d00e6-129">*Страничные большие двоичные объекты* может быть вверх too1 ТБ и более эффективны для операций часто чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="d00e6-129">*Page blobs* can be up too1 TB in size, and are more efficient for frequent read/write operations.</span></span> <span data-ttu-id="d00e6-130">Служба "Виртуальные машины Azure" использует страничные BLOB-объекты в качестве дисков данных и дисков операционной системы.</span><span class="sxs-lookup"><span data-stu-id="d00e6-130">Azure Virtual Machines uses page blobs as OS and data disks.</span></span>
  
    <span data-ttu-id="d00e6-131">Дополнительные сведения об именовании контейнеров и больших двоичных объектов см. в статье, посвященной [именованию контейнеров, больших двоичных объектов и метаданных, а также создание ссылок на них](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata).</span><span class="sxs-lookup"><span data-stu-id="d00e6-131">For details about naming containers and blobs, see [Naming and Referencing Containers, Blobs, and Metadata](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d00e6-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d00e6-132">Next steps</span></span>

* [<span data-ttu-id="d00e6-133">создать учетную запись хранения;</span><span class="sxs-lookup"><span data-stu-id="d00e6-133">Create a storage account</span></span>](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [<span data-ttu-id="d00e6-134">Начало работы с хранилищем BLOB-объектов с использованием .NET</span><span class="sxs-lookup"><span data-stu-id="d00e6-134">Getting started with Blob storage using .NET</span></span>](storage-dotnet-how-to-use-blobs.md)