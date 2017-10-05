---
title: "Общие сведения о хранилище BLOB-объектов Azure | Документация Майкрософт"
description: "Общие сведения о хранилище BLOB-объектов Azure"
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
ms.openlocfilehash: 051f1b37eab254d4ab4f806166ac8d0b8cab944d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-blob-storage"></a><span data-ttu-id="f594d-103">Общие сведения о хранилище BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="f594d-103">Introduction to Blob storage</span></span>

<span data-ttu-id="f594d-104">Хранилище BLOB-объектов Azure — это служба хранения большого количества неструктурированных данных объектов, таких как текстовые или двоичные данные, к которым можно получить доступ практически из любой точки мира по протоколу HTTP или HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f594d-104">Azure Blob storage is a service for storing large amounts of unstructured object data, such as text or binary data, that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="f594d-105">Хранилища BLOB-объектов можно использовать для предоставления данных в открытом доступе всему миру или для хранения данных от приложений в частном порядке.</span><span class="sxs-lookup"><span data-stu-id="f594d-105">You can use Blob storage to expose data publicly to the world, or to store application data privately.</span></span>

<span data-ttu-id="f594d-106">Наиболее частые способы использования хранилища BLOB-объектов:</span><span class="sxs-lookup"><span data-stu-id="f594d-106">Common uses of Blob storage include:</span></span>

* <span data-ttu-id="f594d-107">Обслуживание изображений или документов непосредственно в браузере.</span><span class="sxs-lookup"><span data-stu-id="f594d-107">Serving images or documents directly to a browser</span></span>
* <span data-ttu-id="f594d-108">Хранение файлов для распределенного доступа.</span><span class="sxs-lookup"><span data-stu-id="f594d-108">Storing files for distributed access</span></span>
* <span data-ttu-id="f594d-109">Потоковая передача видео и аудио.</span><span class="sxs-lookup"><span data-stu-id="f594d-109">Streaming video and audio</span></span>
* <span data-ttu-id="f594d-110">Хранение резервных копий и восстановление данных, аварийное восстановление и архивация</span><span class="sxs-lookup"><span data-stu-id="f594d-110">Storing data for backup and restore, disaster recovery, and archiving</span></span>
* <span data-ttu-id="f594d-111">Хранение данных для анализа локальной службой или службой, размещенной в Azure</span><span class="sxs-lookup"><span data-stu-id="f594d-111">Storing data for analysis by an on-premises or Azure-hosted service</span></span>

## <a name="blob-service-concepts"></a><span data-ttu-id="f594d-112">Основные понятия службы BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="f594d-112">Blob service concepts</span></span>

<span data-ttu-id="f594d-113">Служба Blob-объектов содержит следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="f594d-113">The Blob service contains the following components:</span></span>

![Архитектура большого двоичного объекта](./media/storage-blobs-introduction/blob1.png)

* <span data-ttu-id="f594d-115">**Учетная запись хранения**. Весь доступ к хранилищу Azure осуществляется с помощью учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="f594d-115">**Storage Account:** All access to Azure Storage is done through a storage account.</span></span> <span data-ttu-id="f594d-116">Это может быть **учетная запись хранения общего назначения** или **учетная запись хранилища BLOB-объектов**, специально предназначенная для хранения больших двоичных объектов и других объектов.</span><span class="sxs-lookup"><span data-stu-id="f594d-116">This storage account can be a **General-purpose storage account** or a **Blob storage account** that is specialized for storing objects/blobs.</span></span> <span data-ttu-id="f594d-117">См. дополнительные сведения [об учетных записях хранения Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f594d-117">See [About Azure storage accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) for more information.</span></span>

* <span data-ttu-id="f594d-118">**Контейнер**. В контейнере группируется набор BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="f594d-118">**Container:** A container provides a grouping of a set of blobs.</span></span> <span data-ttu-id="f594d-119">Все BLOB-объекты должны содержаться в контейнере.</span><span class="sxs-lookup"><span data-stu-id="f594d-119">All blobs must be in a container.</span></span> <span data-ttu-id="f594d-120">Учетная запись может содержать неограниченное число контейнеров.</span><span class="sxs-lookup"><span data-stu-id="f594d-120">An account can contain an unlimited number of containers.</span></span> <span data-ttu-id="f594d-121">Контейнер может хранить неограниченное количество больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="f594d-121">A container can store an unlimited number of blobs.</span></span> <span data-ttu-id="f594d-122">Учтите, что все знаки в имени контейнера должны быть строчными.</span><span class="sxs-lookup"><span data-stu-id="f594d-122">Note that the container name must be lowercase.</span></span>

* <span data-ttu-id="f594d-123">**BLOB-объект**. Файл любого типа и размера.</span><span class="sxs-lookup"><span data-stu-id="f594d-123">**Blob:** A file of any type and size.</span></span> <span data-ttu-id="f594d-124">Служба хранилища Azure предлагает три типа больших двоичных объектов: блочные, страничные и добавочные.</span><span class="sxs-lookup"><span data-stu-id="f594d-124">Azure Storage offers three types of blobs: block blobs, page blobs, and append blobs.</span></span>
  
    <span data-ttu-id="f594d-125">*Блочные BLOB-объекты* идеально подходят для хранения текстовых и двоичных файлов, таких как документы и файлы мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="f594d-125">*Block blobs* are ideal for storing text or binary files, such as documents and media files.</span></span> <span data-ttu-id="f594d-126">*Добавочные большие двоичные объекты* схожи с блочными BLOB-объектами, так как они состоят из блоков, однако они оптимизированы для операций добавления и поэтому полезны для сценариев ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="f594d-126">*Append blobs* are similar to block blobs in that they are made up of blocks, but they are optimized for append operations, so they are useful for logging scenarios.</span></span> <span data-ttu-id="f594d-127">Один блочный BLOB-объект может содержать до 50 000 блоков размером до 100 МБ каждый с общим размером немного более 4,75 ТБ (100 МБ X 50 000).</span><span class="sxs-lookup"><span data-stu-id="f594d-127">A single block blob can contain up to 50,000 blocks of up to 100 MB each, for a total size of slightly more than 4.75 TB (100 MB X 50,000).</span></span> <span data-ttu-id="f594d-128">Один добавочный BLOB-объект может содержать до 50 000 блоков размером до 4 МБ каждый с общим размером немного более 195 ГБ (4 МБ X 50 000).</span><span class="sxs-lookup"><span data-stu-id="f594d-128">A single append blob can contain up to 50,000 blocks of up to 4 MB each, for a total size of slightly more than 195 GB (4 MB X 50,000).</span></span>
  
    <span data-ttu-id="f594d-129">*Страничные BLOB-объекты* могут иметь размер до 1 ТБ. Они более эффективны для частых операций чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="f594d-129">*Page blobs* can be up to 1 TB in size, and are more efficient for frequent read/write operations.</span></span> <span data-ttu-id="f594d-130">Служба "Виртуальные машины Azure" использует страничные BLOB-объекты в качестве дисков данных и дисков операционной системы.</span><span class="sxs-lookup"><span data-stu-id="f594d-130">Azure Virtual Machines uses page blobs as OS and data disks.</span></span>
  
    <span data-ttu-id="f594d-131">Дополнительные сведения об именовании контейнеров и больших двоичных объектов см. в статье, посвященной [именованию контейнеров, больших двоичных объектов и метаданных, а также создание ссылок на них](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata).</span><span class="sxs-lookup"><span data-stu-id="f594d-131">For details about naming containers and blobs, see [Naming and Referencing Containers, Blobs, and Metadata](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f594d-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f594d-132">Next steps</span></span>

* [<span data-ttu-id="f594d-133">создать учетную запись хранения;</span><span class="sxs-lookup"><span data-stu-id="f594d-133">Create a storage account</span></span>](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [<span data-ttu-id="f594d-134">Начало работы с хранилищем BLOB-объектов с использованием .NET</span><span class="sxs-lookup"><span data-stu-id="f594d-134">Getting started with Blob storage using .NET</span></span>](storage-dotnet-how-to-use-blobs.md)