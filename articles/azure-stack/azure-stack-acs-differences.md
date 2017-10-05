---
title: "Хранилища Azure стека: Различия и рекомендации"
description: "Сведения о различиях между стек хранилища Azure и хранилища Azure, а также рекомендации по развертыванию Azure стека."
services: azure-stack
documentationcenter: 
author: xiaofmao
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/22/2017
ms.author: xiaofmao
ms.openlocfilehash: beb2d26afb8ddc5e85b1828c71de5cbd9e678fe1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="azure-stack-storage-differences-and-considerations"></a><span data-ttu-id="ee086-103">Хранилища Azure стека: Различия и рекомендации</span><span class="sxs-lookup"><span data-stu-id="ee086-103">Azure Stack Storage: Differences and considerations</span></span>
<span data-ttu-id="ee086-104">Хранилище Azure стек — это набор облачных служб хранилища в Microsoft Azure стека.</span><span class="sxs-lookup"><span data-stu-id="ee086-104">Azure Stack Storage is the set of storage cloud services in Microsoft Azure Stack.</span></span> <span data-ttu-id="ee086-105">Стек хранилища, Azure предоставляет большого двоичного объекта, таблицы, очереди и функции управления учетную запись с Azure согласованную семантику.</span><span class="sxs-lookup"><span data-stu-id="ee086-105">Azure Stack Storage provides blob, table, queue, and account management functionality with Azure-consistent semantics.</span></span>

<span data-ttu-id="ee086-106">В этой статье перечислены известные различия стек хранилища Azure из хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="ee086-106">This article summarizes the known Azure Stack Storage differences from Azure Storage.</span></span> <span data-ttu-id="ee086-107">Он также содержатся другие вопросы, которые следует учитывать при развертывании Azure стека.</span><span class="sxs-lookup"><span data-stu-id="ee086-107">It also summarizes other considerations to keep in mind when you deploy Azure Stack.</span></span> <span data-ttu-id="ee086-108">Дополнительные сведения о высокоуровневых различия между стек Azure и Azure см. в разделе [основные вопросы](azure-stack-considerations.md) раздела.</span><span class="sxs-lookup"><span data-stu-id="ee086-108">To learn about high-level differences between Azure Stack and Azure, see the [Key considerations](azure-stack-considerations.md) topic.</span></span>

## <a name="cheat-sheet-storage-differences"></a><span data-ttu-id="ee086-109">Памятка: различия хранилища</span><span class="sxs-lookup"><span data-stu-id="ee086-109">Cheat sheet: Storage differences</span></span>

| <span data-ttu-id="ee086-110">Функция</span><span class="sxs-lookup"><span data-stu-id="ee086-110">Feature</span></span> | <span data-ttu-id="ee086-111">(Глобальная) Azure</span><span class="sxs-lookup"><span data-stu-id="ee086-111">Azure (global)</span></span> | <span data-ttu-id="ee086-112">Azure Stack</span><span class="sxs-lookup"><span data-stu-id="ee086-112">Azure Stack</span></span> |
| --- | --- | --- |
|<span data-ttu-id="ee086-113">Хранилище файлов</span><span class="sxs-lookup"><span data-stu-id="ee086-113">File storage</span></span>|<span data-ttu-id="ee086-114">Облачные файловых ресурсов SMB поддерживается</span><span class="sxs-lookup"><span data-stu-id="ee086-114">Cloud-based SMB file shares supported</span></span>|<span data-ttu-id="ee086-115">Не поддерживается</span><span class="sxs-lookup"><span data-stu-id="ee086-115">Not yet supported</span></span>
|<span data-ttu-id="ee086-116">Данные на rest шифрования</span><span class="sxs-lookup"><span data-stu-id="ee086-116">Data at rest encryption</span></span>|<span data-ttu-id="ee086-117">256-битного шифрования AES</span><span class="sxs-lookup"><span data-stu-id="ee086-117">256-bit AES encryption</span></span>|<span data-ttu-id="ee086-118">Не поддерживается</span><span class="sxs-lookup"><span data-stu-id="ee086-118">Not yet supported</span></span>
|<span data-ttu-id="ee086-119">Тип учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="ee086-119">Storage account type</span></span>|<span data-ttu-id="ee086-120">Учетные записи хранения BLOB-объектов общего назначения и Azure</span><span class="sxs-lookup"><span data-stu-id="ee086-120">General-purpose and Azure Blob storage accounts</span></span>|<span data-ttu-id="ee086-121">Общего назначения только</span><span class="sxs-lookup"><span data-stu-id="ee086-121">General-purpose only</span></span>
|<span data-ttu-id="ee086-122">Параметры репликации</span><span class="sxs-lookup"><span data-stu-id="ee086-122">Replication options</span></span>|<span data-ttu-id="ee086-123">Локально избыточное хранилище, геоизбыточное хранилище, геоизбыточное хранилище с доступом на чтение и зоны избыточным хранилищем</span><span class="sxs-lookup"><span data-stu-id="ee086-123">Locally redundant storage, geo-redundant storage, read-access geo-redundant storage, and zone-redundant storage</span></span>|<span data-ttu-id="ee086-124">Локально избыточное хранилище</span><span class="sxs-lookup"><span data-stu-id="ee086-124">Locally redundant storage</span></span>
|<span data-ttu-id="ee086-125">Хранилище уровня "Премиум"</span><span class="sxs-lookup"><span data-stu-id="ee086-125">Premium storage</span></span>|<span data-ttu-id="ee086-126">Полностью поддерживается</span><span class="sxs-lookup"><span data-stu-id="ee086-126">Fully supported</span></span>|<span data-ttu-id="ee086-127">Могут быть подготовлены, но не ограничение производительности или гарантии</span><span class="sxs-lookup"><span data-stu-id="ee086-127">Can be provisioned, but no performance limit or guarantee</span></span>
|<span data-ttu-id="ee086-128">Управляемые диски</span><span class="sxs-lookup"><span data-stu-id="ee086-128">Managed disks</span></span>|<span data-ttu-id="ee086-129">Premium и standard поддерживается</span><span class="sxs-lookup"><span data-stu-id="ee086-129">Premium and standard supported</span></span>|<span data-ttu-id="ee086-130">Не поддерживается</span><span class="sxs-lookup"><span data-stu-id="ee086-130">Not yet supported</span></span>
|<span data-ttu-id="ee086-131">Имя большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="ee086-131">Blob name</span></span>|<span data-ttu-id="ee086-132">1024 знаков (2048 байт)</span><span class="sxs-lookup"><span data-stu-id="ee086-132">1,024 characters (2,048 bytes)</span></span>|<span data-ttu-id="ee086-133">880 символов (1,760 байт)</span><span class="sxs-lookup"><span data-stu-id="ee086-133">880 characters (1,760 bytes)</span></span>
|<span data-ttu-id="ee086-134">Максимальный размер большого двоичного объекта блока</span><span class="sxs-lookup"><span data-stu-id="ee086-134">Block blob max size</span></span>|<span data-ttu-id="ee086-135">4,75 ТБ (100 МБ X 50 000 блоков)</span><span class="sxs-lookup"><span data-stu-id="ee086-135">4.75 TB (100 MB X 50,000 blocks)</span></span>|<span data-ttu-id="ee086-136">50 000 x 4 МБ (прибл. 195 ГБ)</span><span class="sxs-lookup"><span data-stu-id="ee086-136">50,000 X 4 MB (approx. 195 GB)</span></span>
|<span data-ttu-id="ee086-137">Копирование добавочного моментального снимка большого двоичного объекта страницы</span><span class="sxs-lookup"><span data-stu-id="ee086-137">Page blob incremental snapshot copy</span></span>|<span data-ttu-id="ee086-138">Premium и standard Azure страничные поддерживается</span><span class="sxs-lookup"><span data-stu-id="ee086-138">Premium and standard Azure page blobs supported</span></span>|<span data-ttu-id="ee086-139">Не поддерживается</span><span class="sxs-lookup"><span data-stu-id="ee086-139">Not yet supported</span></span>
|<span data-ttu-id="ee086-140">Максимальный размер большого двоичного объекта страницы</span><span class="sxs-lookup"><span data-stu-id="ee086-140">Page blob max size</span></span>|<span data-ttu-id="ee086-141">8 ТБ</span><span class="sxs-lookup"><span data-stu-id="ee086-141">8 TB</span></span>|<span data-ttu-id="ee086-142">1 TБ</span><span class="sxs-lookup"><span data-stu-id="ee086-142">1 TB</span></span>
|<span data-ttu-id="ee086-143">Размер страницы в большой двоичный объект страницы</span><span class="sxs-lookup"><span data-stu-id="ee086-143">Page blob page size</span></span>|<span data-ttu-id="ee086-144">512 байт</span><span class="sxs-lookup"><span data-stu-id="ee086-144">512 bytes</span></span>|<span data-ttu-id="ee086-145">4 КБ</span><span class="sxs-lookup"><span data-stu-id="ee086-145">4 KB</span></span>
|<span data-ttu-id="ee086-146">Размер ключа в ключ секционирования таблицы и строки</span><span class="sxs-lookup"><span data-stu-id="ee086-146">Table partition key and row key size</span></span>|<span data-ttu-id="ee086-147">1024 знаков (2048 байт)</span><span class="sxs-lookup"><span data-stu-id="ee086-147">1,024 characters (2,048 bytes)</span></span>|<span data-ttu-id="ee086-148">400 знаков (800 байт)</span><span class="sxs-lookup"><span data-stu-id="ee086-148">400 characters (800 bytes)</span></span>

### <a name="metrics"></a><span data-ttu-id="ee086-149">Метрики</span><span class="sxs-lookup"><span data-stu-id="ee086-149">Metrics</span></span>
<span data-ttu-id="ee086-150">Кроме того, существуют некоторые различия с метриками хранилища:</span><span class="sxs-lookup"><span data-stu-id="ee086-150">There are also some differences with storage metrics:</span></span>
* <span data-ttu-id="ee086-151">Данные транзакций в метрик хранилища не различает пропускной способности внутренней или внешней сети.</span><span class="sxs-lookup"><span data-stu-id="ee086-151">The transaction data in storage metrics does not differentiate internal or external network bandwidth.</span></span>
* <span data-ttu-id="ee086-152">Данные транзакций в метрик хранилища не включают виртуальным машинам доступ к подключенные диски.</span><span class="sxs-lookup"><span data-stu-id="ee086-152">The transaction data in storage metrics does not include virtual machine access to the mounted disks.</span></span>

## <a name="api-version"></a><span data-ttu-id="ee086-153">Версия API</span><span class="sxs-lookup"><span data-stu-id="ee086-153">API version</span></span>
<span data-ttu-id="ee086-154">Стек хранилища Azure поддерживает следующие версии:</span><span class="sxs-lookup"><span data-stu-id="ee086-154">The following versions are supported with Azure Stack Storage:</span></span>

* <span data-ttu-id="ee086-155">Службы данных Azure хранилища: [версия 2015-04-05 REST API](https://docs.microsoft.com/en-us/rest/api/storageservices/Version-2015-04-05?redirectedfrom=MSDN)</span><span class="sxs-lookup"><span data-stu-id="ee086-155">Azure Storage data services: [2015-04-05 REST API version](https://docs.microsoft.com/en-us/rest/api/storageservices/Version-2015-04-05?redirectedfrom=MSDN)</span></span>
* <span data-ttu-id="ee086-156">Службы управления Azure хранилища: [2015-05-01-preview 2015-06-15 и 2016-01-01](https://docs.microsoft.com/en-us/rest/api/storagerp/?redirectedfrom=MSDN)</span><span class="sxs-lookup"><span data-stu-id="ee086-156">Azure Storage management services: [2015-05-01-preview, 2015-06-15, and 2016-01-01](https://docs.microsoft.com/en-us/rest/api/storagerp/?redirectedfrom=MSDN)</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ee086-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ee086-157">Next steps</span></span>

* [<span data-ttu-id="ee086-158">Начало работы со средствами разработки стек хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="ee086-158">Get started with Azure Stack Storage development tools</span></span>](azure-stack-storage-dev.md)
* [<span data-ttu-id="ee086-159">Введение в хранилище Azure стека</span><span class="sxs-lookup"><span data-stu-id="ee086-159">Introduction to Azure Stack Storage</span></span>](azure-stack-storage-overview.md)

