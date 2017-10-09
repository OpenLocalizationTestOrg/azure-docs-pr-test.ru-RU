---
title: "toodo aaaWhat hello Azure перебоев в работе службы, влияет на хранилище ключей Azure для события | Документы Microsoft"
description: "Узнайте, какие toodo события hello Azure перебоев в работе службы, влияет на хранилище ключей Azure."
services: key-vault
documentationcenter: 
author: adamglick
manager: mbaldwin
editor: 
ms.assetid: 19a9af63-3032-447b-9d1a-b0125f384edb
ms.service: key-vault
ms.workload: key-vault
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: sumedhb;aglick
ms.openlocfilehash: 88eec82ada401a28323b3eea126168185ba4cdb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-availability-and-redundancy"></a><span data-ttu-id="a4d56-103">Доступность и избыточность хранилища ключей Azure</span><span class="sxs-lookup"><span data-stu-id="a4d56-103">Azure Key Vault availability and redundancy</span></span>
<span data-ttu-id="a4d56-104">Хранилище ключей Azure поддерживает несколько уровней избыточности toomake ключи и секретные данные останутся доступными tooyour приложения даже если отдельные компоненты hello службы fail.</span><span class="sxs-lookup"><span data-stu-id="a4d56-104">Azure Key Vault features multiple layers of redundancy toomake sure that your keys and secrets remain available tooyour application even if individual components of hello service fail.</span></span>

<span data-ttu-id="a4d56-105">Hello содержимого хранилища ключей реплицируются в области hello и дополнительный регион tooa хотя бы 150 километров немедленно, но в рамках hello же geography.</span><span class="sxs-lookup"><span data-stu-id="a4d56-105">hello contents of your key vault are replicated within hello region and tooa secondary region at least 150 miles away but within hello same geography.</span></span> <span data-ttu-id="a4d56-106">Это обеспечивает высокий уровень надежности ключей и секретов.</span><span class="sxs-lookup"><span data-stu-id="a4d56-106">This maintains high durability of your keys and secrets.</span></span> <span data-ttu-id="a4d56-107">В разделе hello [Azure парных регионов](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions) сведения об определенном регионе пары.</span><span class="sxs-lookup"><span data-stu-id="a4d56-107">See hello [Azure paired regions](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions) document for details on specific region pairs.</span></span>

<span data-ttu-id="a4d56-108">При сбое на отдельные компоненты в службу хранилища ключей hello альтернативный компонентов в пределах области hello шаг tooserve в том, что не происходит ухудшения функциональности toomake запроса.</span><span class="sxs-lookup"><span data-stu-id="a4d56-108">If individual components within hello key vault service fail, alternate components within hello region step in tooserve your request toomake sure that there is no degradation of functionality.</span></span> <span data-ttu-id="a4d56-109">Нет необходимости tootake любое действие tootrigger это.</span><span class="sxs-lookup"><span data-stu-id="a4d56-109">You do not need tootake any action tootrigger this.</span></span> <span data-ttu-id="a4d56-110">Она происходит автоматически и будет прозрачным tooyou.</span><span class="sxs-lookup"><span data-stu-id="a4d56-110">It happens automatically and will be transparent tooyou.</span></span>

<span data-ttu-id="a4d56-111">В редких случаях hello недоступность весь регион Azure, автоматически направляются hello запросы, из которых хранилища ключей Azure в этом регионе (*отработку отказа*) tooa дополнительный регион.</span><span class="sxs-lookup"><span data-stu-id="a4d56-111">In hello rare event that an entire Azure region is unavailable, hello requests that you make of Azure Key Vault in that region are automatically routed (*failed over*) tooa secondary region.</span></span> <span data-ttu-id="a4d56-112">Когда основной регион hello снова станет доступной, запросы направляются обратно (*сбой обратно*) toohello первичного региона.</span><span class="sxs-lookup"><span data-stu-id="a4d56-112">When hello primary region is available again, requests are routed back (*failed back*) toohello primary region.</span></span> <span data-ttu-id="a4d56-113">Опять же необязательно tootake любое действие, так как это происходит автоматически.</span><span class="sxs-lookup"><span data-stu-id="a4d56-113">Again, you do not need tootake any action because this happens automatically.</span></span>

<span data-ttu-id="a4d56-114">Существует несколько toobe оговорками учитывать:</span><span class="sxs-lookup"><span data-stu-id="a4d56-114">There are a few caveats toobe aware of:</span></span>

* <span data-ttu-id="a4d56-115">Событие hello регион отработки отказа это может занять toofail службы hello в течение нескольких минут.</span><span class="sxs-lookup"><span data-stu-id="a4d56-115">In hello event of a region failover, it may take a few minutes for hello service toofail over.</span></span> <span data-ttu-id="a4d56-116">Запросы, направляемые в течение этого времени может завершиться ошибкой, до завершения отработки отказа hello.</span><span class="sxs-lookup"><span data-stu-id="a4d56-116">Requests that are made during this time may fail until hello failover completes.</span></span>
* <span data-ttu-id="a4d56-117">После завершения отработки отказа хранилище ключей находится в режиме только для чтения.</span><span class="sxs-lookup"><span data-stu-id="a4d56-117">After a failover is complete, your key vault is in read-only mode.</span></span> <span data-ttu-id="a4d56-118">В этом режиме поддерживаются следующие запросы:</span><span class="sxs-lookup"><span data-stu-id="a4d56-118">Requests that are supported in this mode are:</span></span>
  * <span data-ttu-id="a4d56-119">получение списка хранилищ ключей;</span><span class="sxs-lookup"><span data-stu-id="a4d56-119">List key vaults</span></span>
  * <span data-ttu-id="a4d56-120">получение свойств из хранилищ ключей;</span><span class="sxs-lookup"><span data-stu-id="a4d56-120">Get properties of key vaults</span></span>
  * <span data-ttu-id="a4d56-121">получение списка секретов;</span><span class="sxs-lookup"><span data-stu-id="a4d56-121">List secrets</span></span>
  * <span data-ttu-id="a4d56-122">получение секретов;</span><span class="sxs-lookup"><span data-stu-id="a4d56-122">Get secrets</span></span>
  * <span data-ttu-id="a4d56-123">получение списка ключей;</span><span class="sxs-lookup"><span data-stu-id="a4d56-123">List keys</span></span>
  * <span data-ttu-id="a4d56-124">получение ключей и их свойств;</span><span class="sxs-lookup"><span data-stu-id="a4d56-124">Get (properties of) keys</span></span>
  * <span data-ttu-id="a4d56-125">шифрование;</span><span class="sxs-lookup"><span data-stu-id="a4d56-125">Encrypt</span></span>
  * <span data-ttu-id="a4d56-126">расшифровка;</span><span class="sxs-lookup"><span data-stu-id="a4d56-126">Decrypt</span></span>
  * <span data-ttu-id="a4d56-127">оборачивание;</span><span class="sxs-lookup"><span data-stu-id="a4d56-127">Wrap</span></span>
  * <span data-ttu-id="a4d56-128">разворачивание;</span><span class="sxs-lookup"><span data-stu-id="a4d56-128">Unwrap</span></span>
  * <span data-ttu-id="a4d56-129">Проверка.</span><span class="sxs-lookup"><span data-stu-id="a4d56-129">Verify</span></span>
  * <span data-ttu-id="a4d56-130">вход;</span><span class="sxs-lookup"><span data-stu-id="a4d56-130">Sign</span></span>
  * <span data-ttu-id="a4d56-131">Архивация</span><span class="sxs-lookup"><span data-stu-id="a4d56-131">Backup</span></span>
* <span data-ttu-id="a4d56-132">После восстановления размещения становятся доступными все типы запросов (в том числе чтение *и* запись).</span><span class="sxs-lookup"><span data-stu-id="a4d56-132">After a failover is failed back, all request types (including read *and* write requests) are available.</span></span>

