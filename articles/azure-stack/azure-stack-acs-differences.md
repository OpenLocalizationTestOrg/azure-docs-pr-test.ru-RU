---
title: "Хранилища Azure стека: Различия и рекомендации"
description: "Понять hello различия между Azure стека и хранилищем Azure, а также рекомендации по развертыванию Azure стека."
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
ms.openlocfilehash: a1f8e2180b046b835c89fd658e2dbaff004b8786
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stack-storage-differences-and-considerations"></a><span data-ttu-id="0bb3a-103">Хранилища Azure стека: Различия и рекомендации</span><span class="sxs-lookup"><span data-stu-id="0bb3a-103">Azure Stack Storage: Differences and considerations</span></span>
<span data-ttu-id="0bb3a-104">Хранилище Azure стека — hello набор облачных служб хранилища в Microsoft Azure стека.</span><span class="sxs-lookup"><span data-stu-id="0bb3a-104">Azure Stack Storage is hello set of storage cloud services in Microsoft Azure Stack.</span></span> <span data-ttu-id="0bb3a-105">Стек хранилища, Azure предоставляет большого двоичного объекта, таблицы, очереди и функции управления учетную запись с Azure согласованную семантику.</span><span class="sxs-lookup"><span data-stu-id="0bb3a-105">Azure Stack Storage provides blob, table, queue, and account management functionality with Azure-consistent semantics.</span></span>

<span data-ttu-id="0bb3a-106">В этой статье перечислены известные различия стек хранилища Azure из хранилища Azure hello.</span><span class="sxs-lookup"><span data-stu-id="0bb3a-106">This article summarizes hello known Azure Stack Storage differences from Azure Storage.</span></span> <span data-ttu-id="0bb3a-107">Он также содержит сведения о tookeep другие вопросы в виду при развертывании Azure стека.</span><span class="sxs-lookup"><span data-stu-id="0bb3a-107">It also summarizes other considerations tookeep in mind when you deploy Azure Stack.</span></span> <span data-ttu-id="0bb3a-108">toolearn об отличиях высокого уровня стека Azure и Azure, в разделе hello [основные вопросы](azure-stack-considerations.md) раздела.</span><span class="sxs-lookup"><span data-stu-id="0bb3a-108">toolearn about high-level differences between Azure Stack and Azure, see hello [Key considerations](azure-stack-considerations.md) topic.</span></span>

## <a name="cheat-sheet-storage-differences"></a><span data-ttu-id="0bb3a-109">Памятка: различия хранилища</span><span class="sxs-lookup"><span data-stu-id="0bb3a-109">Cheat sheet: Storage differences</span></span>

| <span data-ttu-id="0bb3a-110">Функция</span><span class="sxs-lookup"><span data-stu-id="0bb3a-110">Feature</span></span> | <span data-ttu-id="0bb3a-111">(Глобальная) Azure</span><span class="sxs-lookup"><span data-stu-id="0bb3a-111">Azure (global)</span></span> | <span data-ttu-id="0bb3a-112">Azure Stack</span><span class="sxs-lookup"><span data-stu-id="0bb3a-112">Azure Stack</span></span> |
| --- | --- | --- |
|<span data-ttu-id="0bb3a-113">Хранилище файлов</span><span class="sxs-lookup"><span data-stu-id="0bb3a-113">File storage</span></span>|<span data-ttu-id="0bb3a-114">Облачные файловых ресурсов SMB поддерживается</span><span class="sxs-lookup"><span data-stu-id="0bb3a-114">Cloud-based SMB file shares supported</span></span>|<span data-ttu-id="0bb3a-115">Не поддерживается</span><span class="sxs-lookup"><span data-stu-id="0bb3a-115">Not yet supported</span></span>
|<span data-ttu-id="0bb3a-116">Данные на rest шифрования</span><span class="sxs-lookup"><span data-stu-id="0bb3a-116">Data at rest encryption</span></span>|<span data-ttu-id="0bb3a-117">256-битного шифрования AES</span><span class="sxs-lookup"><span data-stu-id="0bb3a-117">256-bit AES encryption</span></span>|<span data-ttu-id="0bb3a-118">Не поддерживается</span><span class="sxs-lookup"><span data-stu-id="0bb3a-118">Not yet supported</span></span>
|<span data-ttu-id="0bb3a-119">Тип учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="0bb3a-119">Storage account type</span></span>|<span data-ttu-id="0bb3a-120">Учетные записи хранения BLOB-объектов общего назначения и Azure</span><span class="sxs-lookup"><span data-stu-id="0bb3a-120">General-purpose and Azure Blob storage accounts</span></span>|<span data-ttu-id="0bb3a-121">Общего назначения только</span><span class="sxs-lookup"><span data-stu-id="0bb3a-121">General-purpose only</span></span>
|<span data-ttu-id="0bb3a-122">Параметры репликации</span><span class="sxs-lookup"><span data-stu-id="0bb3a-122">Replication options</span></span>|<span data-ttu-id="0bb3a-123">Локально избыточное хранилище, геоизбыточное хранилище, геоизбыточное хранилище с доступом на чтение и зоны избыточным хранилищем</span><span class="sxs-lookup"><span data-stu-id="0bb3a-123">Locally redundant storage, geo-redundant storage, read-access geo-redundant storage, and zone-redundant storage</span></span>|<span data-ttu-id="0bb3a-124">Локально избыточное хранилище</span><span class="sxs-lookup"><span data-stu-id="0bb3a-124">Locally redundant storage</span></span>
|<span data-ttu-id="0bb3a-125">Хранилище уровня "Премиум"</span><span class="sxs-lookup"><span data-stu-id="0bb3a-125">Premium storage</span></span>|<span data-ttu-id="0bb3a-126">Полностью поддерживается</span><span class="sxs-lookup"><span data-stu-id="0bb3a-126">Fully supported</span></span>|<span data-ttu-id="0bb3a-127">Могут быть подготовлены, но не ограничение производительности или гарантии</span><span class="sxs-lookup"><span data-stu-id="0bb3a-127">Can be provisioned, but no performance limit or guarantee</span></span>
|<span data-ttu-id="0bb3a-128">Управляемые диски</span><span class="sxs-lookup"><span data-stu-id="0bb3a-128">Managed disks</span></span>|<span data-ttu-id="0bb3a-129">Premium и standard поддерживается</span><span class="sxs-lookup"><span data-stu-id="0bb3a-129">Premium and standard supported</span></span>|<span data-ttu-id="0bb3a-130">Не поддерживается</span><span class="sxs-lookup"><span data-stu-id="0bb3a-130">Not yet supported</span></span>
|<span data-ttu-id="0bb3a-131">Имя большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="0bb3a-131">Blob name</span></span>|<span data-ttu-id="0bb3a-132">1024 знаков (2048 байт)</span><span class="sxs-lookup"><span data-stu-id="0bb3a-132">1,024 characters (2,048 bytes)</span></span>|<span data-ttu-id="0bb3a-133">880 символов (1,760 байт)</span><span class="sxs-lookup"><span data-stu-id="0bb3a-133">880 characters (1,760 bytes)</span></span>
|<span data-ttu-id="0bb3a-134">Максимальный размер большого двоичного объекта блока</span><span class="sxs-lookup"><span data-stu-id="0bb3a-134">Block blob max size</span></span>|<span data-ttu-id="0bb3a-135">4,75 ТБ (100 МБ X 50 000 блоков)</span><span class="sxs-lookup"><span data-stu-id="0bb3a-135">4.75 TB (100 MB X 50,000 blocks)</span></span>|<span data-ttu-id="0bb3a-136">50 000 x 4 МБ (прибл. 195 ГБ)</span><span class="sxs-lookup"><span data-stu-id="0bb3a-136">50,000 X 4 MB (approx. 195 GB)</span></span>
|<span data-ttu-id="0bb3a-137">Копирование добавочного моментального снимка большого двоичного объекта страницы</span><span class="sxs-lookup"><span data-stu-id="0bb3a-137">Page blob incremental snapshot copy</span></span>|<span data-ttu-id="0bb3a-138">Premium и standard Azure страничные поддерживается</span><span class="sxs-lookup"><span data-stu-id="0bb3a-138">Premium and standard Azure page blobs supported</span></span>|<span data-ttu-id="0bb3a-139">Не поддерживается</span><span class="sxs-lookup"><span data-stu-id="0bb3a-139">Not yet supported</span></span>
|<span data-ttu-id="0bb3a-140">Максимальный размер большого двоичного объекта страницы</span><span class="sxs-lookup"><span data-stu-id="0bb3a-140">Page blob max size</span></span>|<span data-ttu-id="0bb3a-141">8 ТБ</span><span class="sxs-lookup"><span data-stu-id="0bb3a-141">8 TB</span></span>|<span data-ttu-id="0bb3a-142">1 TБ</span><span class="sxs-lookup"><span data-stu-id="0bb3a-142">1 TB</span></span>
|<span data-ttu-id="0bb3a-143">Размер страницы в большой двоичный объект страницы</span><span class="sxs-lookup"><span data-stu-id="0bb3a-143">Page blob page size</span></span>|<span data-ttu-id="0bb3a-144">512 байт</span><span class="sxs-lookup"><span data-stu-id="0bb3a-144">512 bytes</span></span>|<span data-ttu-id="0bb3a-145">4 КБ</span><span class="sxs-lookup"><span data-stu-id="0bb3a-145">4 KB</span></span>
|<span data-ttu-id="0bb3a-146">Размер ключа в ключ секционирования таблицы и строки</span><span class="sxs-lookup"><span data-stu-id="0bb3a-146">Table partition key and row key size</span></span>|<span data-ttu-id="0bb3a-147">1024 знаков (2048 байт)</span><span class="sxs-lookup"><span data-stu-id="0bb3a-147">1,024 characters (2,048 bytes)</span></span>|<span data-ttu-id="0bb3a-148">400 знаков (800 байт)</span><span class="sxs-lookup"><span data-stu-id="0bb3a-148">400 characters (800 bytes)</span></span>

### <a name="metrics"></a><span data-ttu-id="0bb3a-149">Метрики</span><span class="sxs-lookup"><span data-stu-id="0bb3a-149">Metrics</span></span>
<span data-ttu-id="0bb3a-150">Кроме того, существуют некоторые различия с метриками хранилища:</span><span class="sxs-lookup"><span data-stu-id="0bb3a-150">There are also some differences with storage metrics:</span></span>
* <span data-ttu-id="0bb3a-151">данные транзакций Hello в метрик хранилища не различает пропускной способности внутренней или внешней сети.</span><span class="sxs-lookup"><span data-stu-id="0bb3a-151">hello transaction data in storage metrics does not differentiate internal or external network bandwidth.</span></span>
* <span data-ttu-id="0bb3a-152">данные транзакций Hello в метрик хранилища не включают диски подключены toohello доступа виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0bb3a-152">hello transaction data in storage metrics does not include virtual machine access toohello mounted disks.</span></span>

## <a name="api-version"></a><span data-ttu-id="0bb3a-153">Версия API</span><span class="sxs-lookup"><span data-stu-id="0bb3a-153">API version</span></span>
<span data-ttu-id="0bb3a-154">Стек хранилища Azure поддерживаются следующие версии Hello:</span><span class="sxs-lookup"><span data-stu-id="0bb3a-154">hello following versions are supported with Azure Stack Storage:</span></span>

* <span data-ttu-id="0bb3a-155">Службы данных Azure хранилища: [версия 2015-04-05 REST API](https://docs.microsoft.com/en-us/rest/api/storageservices/Version-2015-04-05?redirectedfrom=MSDN)</span><span class="sxs-lookup"><span data-stu-id="0bb3a-155">Azure Storage data services: [2015-04-05 REST API version](https://docs.microsoft.com/en-us/rest/api/storageservices/Version-2015-04-05?redirectedfrom=MSDN)</span></span>
* <span data-ttu-id="0bb3a-156">Службы управления Azure хранилища: [2015-05-01-preview 2015-06-15 и 2016-01-01](https://docs.microsoft.com/en-us/rest/api/storagerp/?redirectedfrom=MSDN)</span><span class="sxs-lookup"><span data-stu-id="0bb3a-156">Azure Storage management services: [2015-05-01-preview, 2015-06-15, and 2016-01-01](https://docs.microsoft.com/en-us/rest/api/storagerp/?redirectedfrom=MSDN)</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0bb3a-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0bb3a-157">Next steps</span></span>

* [<span data-ttu-id="0bb3a-158">Начало работы со средствами разработки стек хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="0bb3a-158">Get started with Azure Stack Storage development tools</span></span>](azure-stack-storage-dev.md)
* [<span data-ttu-id="0bb3a-159">Введение tooAzure стек хранилища</span><span class="sxs-lookup"><span data-stu-id="0bb3a-159">Introduction tooAzure Stack Storage</span></span>](azure-stack-storage-overview.md)

