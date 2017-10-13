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
ms.date: 9/25/2017
ms.author: xiaofmao
ms.openlocfilehash: 381950321ac3a5ea8a43b76f3fba868da4be4682
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="azure-stack-storage-differences-and-considerations"></a><span data-ttu-id="a54d9-103">Хранилища Azure стека: Различия и рекомендации</span><span class="sxs-lookup"><span data-stu-id="a54d9-103">Azure Stack Storage: Differences and considerations</span></span>

<span data-ttu-id="a54d9-104">*Применяется к: стек Azure интегрированных систем и пакет средств разработки стек Azure*</span><span class="sxs-lookup"><span data-stu-id="a54d9-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="a54d9-105">Хранилище Azure стек — это набор облачных служб хранилища в Microsoft Azure стека.</span><span class="sxs-lookup"><span data-stu-id="a54d9-105">Azure Stack Storage is the set of storage cloud services in Microsoft Azure Stack.</span></span> <span data-ttu-id="a54d9-106">Стек хранилища, Azure предоставляет большого двоичного объекта, таблицы, очереди и функции управления учетную запись с Azure согласованную семантику.</span><span class="sxs-lookup"><span data-stu-id="a54d9-106">Azure Stack Storage provides blob, table, queue, and account management functionality with Azure-consistent semantics.</span></span>

<span data-ttu-id="a54d9-107">В этой статье перечислены известные различия стек хранилища Azure из хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="a54d9-107">This article summarizes the known Azure Stack Storage differences from Azure Storage.</span></span> <span data-ttu-id="a54d9-108">Он также содержатся другие вопросы, которые следует учитывать при развертывании Azure стека.</span><span class="sxs-lookup"><span data-stu-id="a54d9-108">It also summarizes other considerations to keep in mind when you deploy Azure Stack.</span></span> <span data-ttu-id="a54d9-109">Дополнительные сведения о высокоуровневых различия между стек Azure и Azure см. в разделе [основные вопросы](azure-stack-considerations.md) раздела.</span><span class="sxs-lookup"><span data-stu-id="a54d9-109">To learn about high-level differences between Azure Stack and Azure, see the [Key considerations](azure-stack-considerations.md) topic.</span></span>

## <a name="cheat-sheet-storage-differences"></a><span data-ttu-id="a54d9-110">Памятка: различия хранилища</span><span class="sxs-lookup"><span data-stu-id="a54d9-110">Cheat sheet: Storage differences</span></span>

| <span data-ttu-id="a54d9-111">Функция</span><span class="sxs-lookup"><span data-stu-id="a54d9-111">Feature</span></span> | <span data-ttu-id="a54d9-112">(Глобальная) Azure</span><span class="sxs-lookup"><span data-stu-id="a54d9-112">Azure (global)</span></span> | <span data-ttu-id="a54d9-113">Azure Stack</span><span class="sxs-lookup"><span data-stu-id="a54d9-113">Azure Stack</span></span> |
| --- | --- | --- |
|<span data-ttu-id="a54d9-114">Хранилище файлов</span><span class="sxs-lookup"><span data-stu-id="a54d9-114">File storage</span></span>|<span data-ttu-id="a54d9-115">Облачные файловых ресурсов SMB поддерживается</span><span class="sxs-lookup"><span data-stu-id="a54d9-115">Cloud-based SMB file shares supported</span></span>|<span data-ttu-id="a54d9-116">Не поддерживается</span><span class="sxs-lookup"><span data-stu-id="a54d9-116">Not yet supported</span></span>
|<span data-ttu-id="a54d9-117">Данные на rest шифрования</span><span class="sxs-lookup"><span data-stu-id="a54d9-117">Data at rest encryption</span></span>|<span data-ttu-id="a54d9-118">256-битного шифрования AES</span><span class="sxs-lookup"><span data-stu-id="a54d9-118">256-bit AES encryption</span></span>|<span data-ttu-id="a54d9-119">Не поддерживается</span><span class="sxs-lookup"><span data-stu-id="a54d9-119">Not yet supported</span></span>
|<span data-ttu-id="a54d9-120">Тип учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="a54d9-120">Storage account type</span></span>|<span data-ttu-id="a54d9-121">Учетные записи хранения BLOB-объектов общего назначения и Azure</span><span class="sxs-lookup"><span data-stu-id="a54d9-121">General-purpose and Azure Blob storage accounts</span></span>|<span data-ttu-id="a54d9-122">Общего назначения только</span><span class="sxs-lookup"><span data-stu-id="a54d9-122">General-purpose only</span></span>
|<span data-ttu-id="a54d9-123">Параметры репликации</span><span class="sxs-lookup"><span data-stu-id="a54d9-123">Replication options</span></span>|<span data-ttu-id="a54d9-124">Локально избыточное хранилище, геоизбыточное хранилище, геоизбыточное хранилище с доступом на чтение и зоны избыточным хранилищем</span><span class="sxs-lookup"><span data-stu-id="a54d9-124">Locally redundant storage, geo-redundant storage, read-access geo-redundant storage, and zone-redundant storage</span></span>|<span data-ttu-id="a54d9-125">Локально избыточное хранилище</span><span class="sxs-lookup"><span data-stu-id="a54d9-125">Locally redundant storage</span></span>
|<span data-ttu-id="a54d9-126">Хранилище уровня "Премиум"</span><span class="sxs-lookup"><span data-stu-id="a54d9-126">Premium storage</span></span>|<span data-ttu-id="a54d9-127">Полностью поддерживается</span><span class="sxs-lookup"><span data-stu-id="a54d9-127">Fully supported</span></span>|<span data-ttu-id="a54d9-128">Могут быть подготовлены, но не ограничение производительности или гарантии</span><span class="sxs-lookup"><span data-stu-id="a54d9-128">Can be provisioned, but no performance limit or guarantee</span></span>
|<span data-ttu-id="a54d9-129">Управляемые диски</span><span class="sxs-lookup"><span data-stu-id="a54d9-129">Managed disks</span></span>|<span data-ttu-id="a54d9-130">Premium и standard поддерживается</span><span class="sxs-lookup"><span data-stu-id="a54d9-130">Premium and standard supported</span></span>|<span data-ttu-id="a54d9-131">Не поддерживается</span><span class="sxs-lookup"><span data-stu-id="a54d9-131">Not yet supported</span></span>
|<span data-ttu-id="a54d9-132">Имя большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="a54d9-132">Blob name</span></span>|<span data-ttu-id="a54d9-133">1024 знаков (2048 байт)</span><span class="sxs-lookup"><span data-stu-id="a54d9-133">1,024 characters (2,048 bytes)</span></span>|<span data-ttu-id="a54d9-134">880 символов (1,760 байт)</span><span class="sxs-lookup"><span data-stu-id="a54d9-134">880 characters (1,760 bytes)</span></span>
|<span data-ttu-id="a54d9-135">Максимальный размер большого двоичного объекта блока</span><span class="sxs-lookup"><span data-stu-id="a54d9-135">Block blob max size</span></span>|<span data-ttu-id="a54d9-136">4,75 ТБ (100 МБ X 50 000 блоков)</span><span class="sxs-lookup"><span data-stu-id="a54d9-136">4.75 TB (100 MB X 50,000 blocks)</span></span>|<span data-ttu-id="a54d9-137">50 000 x 4 МБ (прибл. 195 ГБ)</span><span class="sxs-lookup"><span data-stu-id="a54d9-137">50,000 X 4 MB (approx. 195 GB)</span></span>
|<span data-ttu-id="a54d9-138">Копирование добавочного моментального снимка большого двоичного объекта страницы</span><span class="sxs-lookup"><span data-stu-id="a54d9-138">Page blob incremental snapshot copy</span></span>|<span data-ttu-id="a54d9-139">Premium и standard Azure страничные поддерживается</span><span class="sxs-lookup"><span data-stu-id="a54d9-139">Premium and standard Azure page blobs supported</span></span>|<span data-ttu-id="a54d9-140">Не поддерживается</span><span class="sxs-lookup"><span data-stu-id="a54d9-140">Not yet supported</span></span>
|<span data-ttu-id="a54d9-141">Максимальный размер большого двоичного объекта страницы</span><span class="sxs-lookup"><span data-stu-id="a54d9-141">Page blob max size</span></span>|<span data-ttu-id="a54d9-142">8 ТБ</span><span class="sxs-lookup"><span data-stu-id="a54d9-142">8 TB</span></span>|<span data-ttu-id="a54d9-143">1 TБ</span><span class="sxs-lookup"><span data-stu-id="a54d9-143">1 TB</span></span>
|<span data-ttu-id="a54d9-144">Размер страницы в большой двоичный объект страницы</span><span class="sxs-lookup"><span data-stu-id="a54d9-144">Page blob page size</span></span>|<span data-ttu-id="a54d9-145">512 байт</span><span class="sxs-lookup"><span data-stu-id="a54d9-145">512 bytes</span></span>|<span data-ttu-id="a54d9-146">4 КБ</span><span class="sxs-lookup"><span data-stu-id="a54d9-146">4 KB</span></span>
|<span data-ttu-id="a54d9-147">Размер ключа в ключ секционирования таблицы и строки</span><span class="sxs-lookup"><span data-stu-id="a54d9-147">Table partition key and row key size</span></span>|<span data-ttu-id="a54d9-148">1024 знаков (2048 байт)</span><span class="sxs-lookup"><span data-stu-id="a54d9-148">1,024 characters (2,048 bytes)</span></span>|<span data-ttu-id="a54d9-149">400 знаков (800 байт)</span><span class="sxs-lookup"><span data-stu-id="a54d9-149">400 characters (800 bytes)</span></span>

### <a name="metrics"></a><span data-ttu-id="a54d9-150">Метрики</span><span class="sxs-lookup"><span data-stu-id="a54d9-150">Metrics</span></span>
<span data-ttu-id="a54d9-151">Кроме того, существуют некоторые различия с метриками хранилища:</span><span class="sxs-lookup"><span data-stu-id="a54d9-151">There are also some differences with storage metrics:</span></span>
* <span data-ttu-id="a54d9-152">Данные транзакций в метрик хранилища не различает пропускной способности внутренней или внешней сети.</span><span class="sxs-lookup"><span data-stu-id="a54d9-152">The transaction data in storage metrics does not differentiate internal or external network bandwidth.</span></span>
* <span data-ttu-id="a54d9-153">Данные транзакций в метрик хранилища не включают виртуальным машинам доступ к подключенные диски.</span><span class="sxs-lookup"><span data-stu-id="a54d9-153">The transaction data in storage metrics does not include virtual machine access to the mounted disks.</span></span>

## <a name="api-version"></a><span data-ttu-id="a54d9-154">Версия API</span><span class="sxs-lookup"><span data-stu-id="a54d9-154">API version</span></span>
<span data-ttu-id="a54d9-155">Стек хранилища Azure поддерживает следующие версии:</span><span class="sxs-lookup"><span data-stu-id="a54d9-155">The following versions are supported with Azure Stack Storage:</span></span>

* <span data-ttu-id="a54d9-156">Службы данных Azure хранилища: [версия 2015-04-05 REST API](https://docs.microsoft.com/rest/api/storageservices/Version-2015-04-05?redirectedfrom=MSDN)</span><span class="sxs-lookup"><span data-stu-id="a54d9-156">Azure Storage data services: [2015-04-05 REST API version](https://docs.microsoft.com/rest/api/storageservices/Version-2015-04-05?redirectedfrom=MSDN)</span></span>
* <span data-ttu-id="a54d9-157">Службы управления Azure хранилища: [2015-05-01-preview 2015-06-15 и 2016-01-01](https://docs.microsoft.com/rest/api/storagerp/?redirectedfrom=MSDN)</span><span class="sxs-lookup"><span data-stu-id="a54d9-157">Azure Storage management services: [2015-05-01-preview, 2015-06-15, and 2016-01-01](https://docs.microsoft.com/rest/api/storagerp/?redirectedfrom=MSDN)</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a54d9-158">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a54d9-158">Next steps</span></span>

* [<span data-ttu-id="a54d9-159">Начало работы со средствами разработки стек хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="a54d9-159">Get started with Azure Stack Storage development tools</span></span>](azure-stack-storage-dev.md)
* [<span data-ttu-id="a54d9-160">Введение в хранилище Azure стека</span><span class="sxs-lookup"><span data-stu-id="a54d9-160">Introduction to Azure Stack Storage</span></span>](azure-stack-storage-overview.md)

