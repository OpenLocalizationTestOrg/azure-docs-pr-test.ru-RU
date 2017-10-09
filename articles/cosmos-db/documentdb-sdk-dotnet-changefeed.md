---
title: "aaaAzure DocumentDB изменение веб-канала процессора пакета SDK для .NET ре & сурсов | Документы Microsoft"
description: "Узнайте о hello, изменение канала процессора API и SDK, включая даты выхода, даты выбытия и изменения, выполняемые на каждой версии hello DocumentDB изменение веб-канала процессора пакета SDK для .NET."
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
ms.openlocfilehash: 7c001cc77f41c01445fb53328e9d99fd3d312c58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="documentdb-net-change-feed-processor-sdk-download-and-release-notes"></a><span data-ttu-id="0e321-103">Пакет SDK для обработчика веб-канала изменений для DocumentDB .NET: скачивание и заметки о выпуске</span><span class="sxs-lookup"><span data-stu-id="0e321-103">DocumentDB .NET Change Feed Processor SDK: Download and release notes</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0e321-104">.NET</span><span class="sxs-lookup"><span data-stu-id="0e321-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="0e321-105">Веб-канал изменений в .NET</span><span class="sxs-lookup"><span data-stu-id="0e321-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="0e321-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="0e321-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="0e321-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="0e321-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="0e321-108">Java</span><span class="sxs-lookup"><span data-stu-id="0e321-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="0e321-109">Python</span><span class="sxs-lookup"><span data-stu-id="0e321-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="0e321-110">REST</span><span class="sxs-lookup"><span data-stu-id="0e321-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="0e321-111">Поставщик ресурсов REST</span><span class="sxs-lookup"><span data-stu-id="0e321-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="0e321-112">SQL</span><span class="sxs-lookup"><span data-stu-id="0e321-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="0e321-113">**Скачивание пакета SDK**</span><span class="sxs-lookup"><span data-stu-id="0e321-113">**SDK download**</span></span></td><td>[<span data-ttu-id="0e321-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="0e321-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/)</td></tr>

<tr><td><span data-ttu-id="0e321-115">**Документация по API**</span><span class="sxs-lookup"><span data-stu-id="0e321-115">**API documentation**</span></span></td><td>[<span data-ttu-id="0e321-116">Справочная документация по изменению API библиотеки обработчика веб-каналов</span><span class="sxs-lookup"><span data-stu-id="0e321-116">Change Feed Processor library API reference documentation</span></span>](/dotnet/api/microsoft.azure.documents.changefeedprocessor?view=azure-dotnet)</td></tr>

<tr><td><span data-ttu-id="0e321-117">**Начало работы**</span><span class="sxs-lookup"><span data-stu-id="0e321-117">**Get started**</span></span></td><td>[<span data-ttu-id="0e321-118">Приступая к работе с hello DocumentDB изменение веб-канала процессора .NET SDK</span><span class="sxs-lookup"><span data-stu-id="0e321-118">Get started with hello DocumentDB Change Feed Processor .NET SDK</span></span>](change-feed.md)</td></tr>

<tr><td><span data-ttu-id="0e321-119">**Текущая поддерживаемая платформа**</span><span class="sxs-lookup"><span data-stu-id="0e321-119">**Current supported framework**</span></span></td><td>[<span data-ttu-id="0e321-120">Microsoft .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="0e321-120">Microsoft .NET Framework 4.5</span></span>](https://www.microsoft.com/download/details.aspx?id=30653)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="0e321-121">Заметки о выпуске</span><span class="sxs-lookup"><span data-stu-id="0e321-121">Release notes</span></span>

### <a name="a-name110110"></a><span data-ttu-id="0e321-122"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="0e321-122"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="0e321-123">Добавить метод tooobtain предполагаемого количества оставшихся рабочих toobe, обрабатываются в hello изменение веб-канала.</span><span class="sxs-lookup"><span data-stu-id="0e321-123">Added a method tooobtain an estimate of remaining work toobe processed in hello Change Feed.</span></span>
* <span data-ttu-id="0e321-124">Совместимость с [пакетом SDK для .NET для DocumentDB](documentdb-sdk-dotnet.md) версии 1.13.2 и выше.</span><span class="sxs-lookup"><span data-stu-id="0e321-124">Compatible with [DocumentDB .NET SDK](documentdb-sdk-dotnet.md) versions 1.13.2 and above.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="0e321-125"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="0e321-125"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="0e321-126">Пакет SDK общей доступности.</span><span class="sxs-lookup"><span data-stu-id="0e321-126">GA SDK</span></span>
* <span data-ttu-id="0e321-127">Совместимость с [пакетом SDK для .NET для DocumentDB](documentdb-sdk-dotnet.md) версии 1.14.1 и ниже.</span><span class="sxs-lookup"><span data-stu-id="0e321-127">Compatible with [DocumentDB .NET SDK](documentdb-sdk-dotnet.md) versions 1.14.1 and below.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="0e321-128">Даты выпуска и выбытия</span><span class="sxs-lookup"><span data-stu-id="0e321-128">Release & Retirement dates</span></span>
<span data-ttu-id="0e321-129">Корпорация Майкрософт предоставляет уведомления по крайней мере **12 месяцев** до снятия с учета в новой/поддерживаемой версии для hello перехода порядок toosmooth tooa пакет SDK.</span><span class="sxs-lookup"><span data-stu-id="0e321-129">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order toosmooth hello transition tooa newer/supported version.</span></span>

<span data-ttu-id="0e321-130">Новые функции и функциональные возможности и оптимизацию добавляются только toohello текущего пакета SDK, таким образом, рекомендуется, вы всегда обновления toohello последнюю версию пакета SDK как можно раньше.</span><span class="sxs-lookup"><span data-stu-id="0e321-130">New features and functionality and optimizations are only added toohello current SDK, as such it is recommended that you always upgrade toohello latest SDK version as early as possible.</span></span> 

<span data-ttu-id="0e321-131">Любой запрос tooCosmos базу данных, используя удалено SDK будут отклонены службой hello.</span><span class="sxs-lookup"><span data-stu-id="0e321-131">Any request tooCosmos DB using a retired SDK will be rejected by hello service.</span></span>

<br/>

| <span data-ttu-id="0e321-132">Version (версия)</span><span class="sxs-lookup"><span data-stu-id="0e321-132">Version</span></span> | <span data-ttu-id="0e321-133">Дата выпуска</span><span class="sxs-lookup"><span data-stu-id="0e321-133">Release Date</span></span> | <span data-ttu-id="0e321-134">Дата вывода</span><span class="sxs-lookup"><span data-stu-id="0e321-134">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="0e321-135">1.1.0</span><span class="sxs-lookup"><span data-stu-id="0e321-135">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="0e321-136">13 августа 2017 г.</span><span class="sxs-lookup"><span data-stu-id="0e321-136">August 13, 2017</span></span> |--- |
| [<span data-ttu-id="0e321-137">1.0.0</span><span class="sxs-lookup"><span data-stu-id="0e321-137">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="0e321-138">7 июля 2017 г.</span><span class="sxs-lookup"><span data-stu-id="0e321-138">July 07, 2017</span></span> |--- |


## <a name="faq"></a><span data-ttu-id="0e321-139">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="0e321-139">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="0e321-140">См. также</span><span class="sxs-lookup"><span data-stu-id="0e321-140">See also</span></span>
<span data-ttu-id="0e321-141">toolearn Дополнительные сведения о Cosmos DB. в разделе [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) страницы службы.</span><span class="sxs-lookup"><span data-stu-id="0e321-141">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

