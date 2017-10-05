---
title: "Что делать, если прерывание работы службы Azure влияет на хранилище ключей Azure | Документация Майкрософт"
description: "Узнайте, что делать, если прерывание работы службы Azure влияет на хранилище ключей Azure."
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
ms.openlocfilehash: 6419d54c54e7d19103419262b79e7a5268b2268c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-key-vault-availability-and-redundancy"></a><span data-ttu-id="af64e-103">Доступность и избыточность хранилища ключей Azure</span><span class="sxs-lookup"><span data-stu-id="af64e-103">Azure Key Vault availability and redundancy</span></span>
<span data-ttu-id="af64e-104">Хранилище ключей Azure имеет несколько уровней избыточности, благодаря которым ключи и секреты остаются доступными для приложения даже при сбое отдельных компонентов службы.</span><span class="sxs-lookup"><span data-stu-id="af64e-104">Azure Key Vault features multiple layers of redundancy to make sure that your keys and secrets remain available to your application even if individual components of the service fail.</span></span>

<span data-ttu-id="af64e-105">Содержимое хранилища ключей реплицируется в пределах региона, а также в дополнительный регион, расположенный на расстоянии не менее 240 км от основного, но в той же географической области.</span><span class="sxs-lookup"><span data-stu-id="af64e-105">The contents of your key vault are replicated within the region and to a secondary region at least 150 miles away but within the same geography.</span></span> <span data-ttu-id="af64e-106">Это обеспечивает высокий уровень надежности ключей и секретов.</span><span class="sxs-lookup"><span data-stu-id="af64e-106">This maintains high durability of your keys and secrets.</span></span> <span data-ttu-id="af64e-107">В разделе [Непрерывность бизнес-процессов и аварийное восстановление в службах BizTalk: пары регионов Azure](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions) можно получить сведения об определенных парах регионов.</span><span class="sxs-lookup"><span data-stu-id="af64e-107">See the [Azure paired regions](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions) document for details on specific region pairs.</span></span>

<span data-ttu-id="af64e-108">При сбое отдельных компонентов службы хранилища ключей ваши запросы будут обслуживаться дополнительными компонентами в текущем регионе, чтобы не допустить снижения функциональности.</span><span class="sxs-lookup"><span data-stu-id="af64e-108">If individual components within the key vault service fail, alternate components within the region step in to serve your request to make sure that there is no degradation of functionality.</span></span> <span data-ttu-id="af64e-109">Для этого не нужно предпринимать какие-либо действия.</span><span class="sxs-lookup"><span data-stu-id="af64e-109">You do not need to take any action to trigger this.</span></span> <span data-ttu-id="af64e-110">Все выполняется автоматически и незаметно для вас.</span><span class="sxs-lookup"><span data-stu-id="af64e-110">It happens automatically and will be transparent to you.</span></span>

<span data-ttu-id="af64e-111">В редких случаях, когда становится недоступным весь регион Azure, ваши запросы к хранилищу ключей Azure в этом регионе автоматически перенаправляются в дополнительный регион (это называется *отработкой отказа*).</span><span class="sxs-lookup"><span data-stu-id="af64e-111">In the rare event that an entire Azure region is unavailable, the requests that you make of Azure Key Vault in that region are automatically routed (*failed over*) to a secondary region.</span></span> <span data-ttu-id="af64e-112">Когда основной регион снова становится доступным, запросы отправляются обратно в основной регион (это называется *восстановлением размещения*).</span><span class="sxs-lookup"><span data-stu-id="af64e-112">When the primary region is available again, requests are routed back (*failed back*) to the primary region.</span></span> <span data-ttu-id="af64e-113">Опять же, так как это происходит автоматически, то никаких дополнительных действий предпринимать не нужно.</span><span class="sxs-lookup"><span data-stu-id="af64e-113">Again, you do not need to take any action because this happens automatically.</span></span>

<span data-ttu-id="af64e-114">Существует несколько моментов, на которые следует обратить внимание.</span><span class="sxs-lookup"><span data-stu-id="af64e-114">There are a few caveats to be aware of:</span></span>

* <span data-ttu-id="af64e-115">В случае отработки отказа для региона на отработку отказа службы может потребоваться несколько минут.</span><span class="sxs-lookup"><span data-stu-id="af64e-115">In the event of a region failover, it may take a few minutes for the service to fail over.</span></span> <span data-ttu-id="af64e-116">Запросы, отправленные в это время, могут завершаться ошибкой, пока не завершится отработка отказа.</span><span class="sxs-lookup"><span data-stu-id="af64e-116">Requests that are made during this time may fail until the failover completes.</span></span>
* <span data-ttu-id="af64e-117">После завершения отработки отказа хранилище ключей находится в режиме только для чтения.</span><span class="sxs-lookup"><span data-stu-id="af64e-117">After a failover is complete, your key vault is in read-only mode.</span></span> <span data-ttu-id="af64e-118">В этом режиме поддерживаются следующие запросы:</span><span class="sxs-lookup"><span data-stu-id="af64e-118">Requests that are supported in this mode are:</span></span>
  * <span data-ttu-id="af64e-119">получение списка хранилищ ключей;</span><span class="sxs-lookup"><span data-stu-id="af64e-119">List key vaults</span></span>
  * <span data-ttu-id="af64e-120">получение свойств из хранилищ ключей;</span><span class="sxs-lookup"><span data-stu-id="af64e-120">Get properties of key vaults</span></span>
  * <span data-ttu-id="af64e-121">получение списка секретов;</span><span class="sxs-lookup"><span data-stu-id="af64e-121">List secrets</span></span>
  * <span data-ttu-id="af64e-122">получение секретов;</span><span class="sxs-lookup"><span data-stu-id="af64e-122">Get secrets</span></span>
  * <span data-ttu-id="af64e-123">получение списка ключей;</span><span class="sxs-lookup"><span data-stu-id="af64e-123">List keys</span></span>
  * <span data-ttu-id="af64e-124">получение ключей и их свойств;</span><span class="sxs-lookup"><span data-stu-id="af64e-124">Get (properties of) keys</span></span>
  * <span data-ttu-id="af64e-125">шифрование;</span><span class="sxs-lookup"><span data-stu-id="af64e-125">Encrypt</span></span>
  * <span data-ttu-id="af64e-126">расшифровка;</span><span class="sxs-lookup"><span data-stu-id="af64e-126">Decrypt</span></span>
  * <span data-ttu-id="af64e-127">оборачивание;</span><span class="sxs-lookup"><span data-stu-id="af64e-127">Wrap</span></span>
  * <span data-ttu-id="af64e-128">разворачивание;</span><span class="sxs-lookup"><span data-stu-id="af64e-128">Unwrap</span></span>
  * <span data-ttu-id="af64e-129">Проверка.</span><span class="sxs-lookup"><span data-stu-id="af64e-129">Verify</span></span>
  * <span data-ttu-id="af64e-130">вход;</span><span class="sxs-lookup"><span data-stu-id="af64e-130">Sign</span></span>
  * <span data-ttu-id="af64e-131">Архивация</span><span class="sxs-lookup"><span data-stu-id="af64e-131">Backup</span></span>
* <span data-ttu-id="af64e-132">После восстановления размещения становятся доступными все типы запросов (в том числе чтение *и* запись).</span><span class="sxs-lookup"><span data-stu-id="af64e-132">After a failover is failed back, all request types (including read *and* write requests) are available.</span></span>

