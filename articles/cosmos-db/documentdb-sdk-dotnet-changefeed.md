---
title: "Пакет SDK и ресурсы обработчика веб-канала изменений в .NET для Azure DocumentDB | Документы Майкрософт"
description: "Сведения об API и пакете SDK для обработчика веб-канала изменений, включая даты выхода, даты выбытия и изменения, внесенные в каждую версию пакета SDK для обработчика веб-канала изменений в .NET для DocumentDB."
services: cosmos-db
documentationcenter: .net
author: ealsur
manager: kirillg
editor: mimig1
ms.assetid: f2dd9438-8879-4f74-bb6c-e1efc2cd0157
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/14/2017
ms.author: maquaran
ms.openlocfilehash: 40c796bc5af1220c46950a6fac062ffdd243e59f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="documentdb-net-change-feed-processor-sdk-download-and-release-notes"></a><span data-ttu-id="18d51-103">Пакет SDK для обработчика веб-канала изменений для DocumentDB .NET: скачивание и заметки о выпуске</span><span class="sxs-lookup"><span data-stu-id="18d51-103">DocumentDB .NET Change Feed Processor SDK: Download and release notes</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="18d51-104">.NET</span><span class="sxs-lookup"><span data-stu-id="18d51-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="18d51-105">Веб-канал изменений в .NET</span><span class="sxs-lookup"><span data-stu-id="18d51-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="18d51-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="18d51-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="18d51-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="18d51-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="18d51-108">Java</span><span class="sxs-lookup"><span data-stu-id="18d51-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="18d51-109">Python</span><span class="sxs-lookup"><span data-stu-id="18d51-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="18d51-110">REST</span><span class="sxs-lookup"><span data-stu-id="18d51-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="18d51-111">Поставщик ресурсов REST</span><span class="sxs-lookup"><span data-stu-id="18d51-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="18d51-112">SQL</span><span class="sxs-lookup"><span data-stu-id="18d51-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="18d51-113">**Скачивание пакета SDK**</span><span class="sxs-lookup"><span data-stu-id="18d51-113">**SDK download**</span></span></td><td>[<span data-ttu-id="18d51-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="18d51-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/)</td></tr>

<tr><td><span data-ttu-id="18d51-115">**Документация по API**</span><span class="sxs-lookup"><span data-stu-id="18d51-115">**API documentation**</span></span></td><td>[<span data-ttu-id="18d51-116">Справочная документация по изменению API библиотеки обработчика веб-каналов</span><span class="sxs-lookup"><span data-stu-id="18d51-116">Change Feed Processor library API reference documentation</span></span>](/dotnet/api/microsoft.azure.documents.changefeedprocessor?view=azure-dotnet)</td></tr>

<tr><td><span data-ttu-id="18d51-117">**Приступая к работе**</span><span class="sxs-lookup"><span data-stu-id="18d51-117">**Get started**</span></span></td><td>[<span data-ttu-id="18d51-118">Приступая к работе с пакетом SDK для обработчика веб-канала изменений в .NET для DocumentDB</span><span class="sxs-lookup"><span data-stu-id="18d51-118">Get started with the DocumentDB Change Feed Processor .NET SDK</span></span>](change-feed.md)</td></tr>

<tr><td><span data-ttu-id="18d51-119">**Текущая поддерживаемая платформа**</span><span class="sxs-lookup"><span data-stu-id="18d51-119">**Current supported framework**</span></span></td><td>[<span data-ttu-id="18d51-120">Microsoft .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="18d51-120">Microsoft .NET Framework 4.5</span></span>](https://www.microsoft.com/download/details.aspx?id=30653)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="18d51-121">Заметки о выпуске</span><span class="sxs-lookup"><span data-stu-id="18d51-121">Release notes</span></span>

### <a name="a-name110110"></a><span data-ttu-id="18d51-122"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="18d51-122"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="18d51-123">Добавлен метод для оценки оставшейся работы для обработки в веб-канале изменений.</span><span class="sxs-lookup"><span data-stu-id="18d51-123">Added a method to obtain an estimate of remaining work to be processed in the Change Feed.</span></span>
* <span data-ttu-id="18d51-124">Совместимость с [пакетом SDK для .NET для DocumentDB](documentdb-sdk-dotnet.md) версии 1.13.2 и выше.</span><span class="sxs-lookup"><span data-stu-id="18d51-124">Compatible with [DocumentDB .NET SDK](documentdb-sdk-dotnet.md) versions 1.13.2 and above.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="18d51-125"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="18d51-125"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="18d51-126">Пакет SDK общей доступности.</span><span class="sxs-lookup"><span data-stu-id="18d51-126">GA SDK</span></span>
* <span data-ttu-id="18d51-127">Совместимость с [пакетом SDK для .NET для DocumentDB](documentdb-sdk-dotnet.md) версии 1.14.1 и ниже.</span><span class="sxs-lookup"><span data-stu-id="18d51-127">Compatible with [DocumentDB .NET SDK](documentdb-sdk-dotnet.md) versions 1.14.1 and below.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="18d51-128">Даты выпуска и выбытия</span><span class="sxs-lookup"><span data-stu-id="18d51-128">Release & Retirement dates</span></span>
<span data-ttu-id="18d51-129">Корпорация Майкрософт отправит уведомление минимум за **12 месяцев** до вывода пакета SDK из эксплуатации, чтобы обеспечить более плавный переход на новую или поддерживаемую версию.</span><span class="sxs-lookup"><span data-stu-id="18d51-129">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span></span>

<span data-ttu-id="18d51-130">Новые функции, возможности и оптимизации добавляются только в текущую версию пакета SDK, поэтому рекомендуется как можно раньше обновлять пакет SDK до последней версии.</span><span class="sxs-lookup"><span data-stu-id="18d51-130">New features and functionality and optimizations are only added to the current SDK, as such it is recommended that you always upgrade to the latest SDK version as early as possible.</span></span> 

<span data-ttu-id="18d51-131">Любые запросы к Cosmos DB с помощью выведенного из эксплуатации пакета SDK будут отклонены службой.</span><span class="sxs-lookup"><span data-stu-id="18d51-131">Any request to Cosmos DB using a retired SDK will be rejected by the service.</span></span>

<br/>

| <span data-ttu-id="18d51-132">Version (версия)</span><span class="sxs-lookup"><span data-stu-id="18d51-132">Version</span></span> | <span data-ttu-id="18d51-133">Дата выпуска</span><span class="sxs-lookup"><span data-stu-id="18d51-133">Release Date</span></span> | <span data-ttu-id="18d51-134">Дата вывода</span><span class="sxs-lookup"><span data-stu-id="18d51-134">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="18d51-135">1.1.0</span><span class="sxs-lookup"><span data-stu-id="18d51-135">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="18d51-136">13 августа 2017 г.</span><span class="sxs-lookup"><span data-stu-id="18d51-136">August 13, 2017</span></span> |--- |
| [<span data-ttu-id="18d51-137">1.0.0</span><span class="sxs-lookup"><span data-stu-id="18d51-137">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="18d51-138">7 июля 2017 г.</span><span class="sxs-lookup"><span data-stu-id="18d51-138">July 07, 2017</span></span> |--- |


## <a name="faq"></a><span data-ttu-id="18d51-139">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="18d51-139">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="18d51-140">См. также</span><span class="sxs-lookup"><span data-stu-id="18d51-140">See also</span></span>
<span data-ttu-id="18d51-141">Дополнительные сведения о Cosmos DB см. на странице службы [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="18d51-141">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

