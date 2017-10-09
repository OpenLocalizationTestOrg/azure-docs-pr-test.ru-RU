---
title: "AAA» запроса индекса (портал - поиска Azure) | Документы Microsoft»"
description: "Выполните запрос поиска в портале Azure hello поиск в обозревателе."
services: search
manager: jhubbard
documentationcenter: 
author: ashmaka
ms.assetid: 8e524188-73a7-44db-9e64-ae8bf66b05d3
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 07/10/2017
ms.author: ashmaka
ms.openlocfilehash: 56bab3ef8a66eeb053fbbeb6d322acb6824fb34b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="query-an-azure-search-index-using-search-explorer-in-hello-azure-portal"></a><span data-ttu-id="b5135-103">Запрос с помощью обозревателя поиска в портале Azure hello индекс поиска Azure</span><span class="sxs-lookup"><span data-stu-id="b5135-103">Query an Azure Search index using Search Explorer in hello Azure Portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b5135-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="b5135-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="b5135-105">Портал</span><span class="sxs-lookup"><span data-stu-id="b5135-105">Portal</span></span>](search-explorer.md)
> * [<span data-ttu-id="b5135-106">.NET</span><span class="sxs-lookup"><span data-stu-id="b5135-106">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="b5135-107">REST</span><span class="sxs-lookup"><span data-stu-id="b5135-107">REST</span></span>](search-query-rest-api.md)
> 
> 

<span data-ttu-id="b5135-108">В этой статье показано, как tooquery поиска Azure индекс с помощью **обозреватель поиска** в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b5135-108">This article shows you how tooquery an Azure Search index using **Search Explorer** in hello Azure portal.</span></span> <span data-ttu-id="b5135-109">Поиск в обозревателе toosubmit простого или полного Lucene строки tooany существующий индекс запросов можно использовать в службе.</span><span class="sxs-lookup"><span data-stu-id="b5135-109">You can use Search Explorer toosubmit simple or full Lucene query strings tooany existing index in your service.</span></span>

## <a name="open-hello-service-dashboard"></a><span data-ttu-id="b5135-110">Привет открыть панель мониторинга службы</span><span class="sxs-lookup"><span data-stu-id="b5135-110">Open hello service dashboard</span></span>
1. <span data-ttu-id="b5135-111">Нажмите кнопку **все ресурсы** полосы перехода hello в hello слева от оператора hello [портал Azure](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).</span><span class="sxs-lookup"><span data-stu-id="b5135-111">Click **All resources** in hello jump bar on hello left side of hello [Azure portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).</span></span>
2. <span data-ttu-id="b5135-112">Выберите службу поиска Azure.</span><span class="sxs-lookup"><span data-stu-id="b5135-112">Select your Azure Search service.</span></span>

## <a name="select-an-index"></a><span data-ttu-id="b5135-113">Выбор индекса</span><span class="sxs-lookup"><span data-stu-id="b5135-113">Select an index</span></span>

<span data-ttu-id="b5135-114">Выберите hello индекс хотелось бы toosearch из hello **индексы** плитки.</span><span class="sxs-lookup"><span data-stu-id="b5135-114">Select hello index you would like toosearch from hello **Indexes** tile.</span></span>

   ![](./media/search-explorer/pick-index.png)

## <a name="open-search-explorer"></a><span data-ttu-id="b5135-115">Открытие обозревателя поиска</span><span class="sxs-lookup"><span data-stu-id="b5135-115">Open Search Explorer</span></span>

<span data-ttu-id="b5135-116">Щелкните панель поиска откройте hello tooslide плитки обозреватель поиска hello и панель результатов.</span><span class="sxs-lookup"><span data-stu-id="b5135-116">Click on hello Search Explorer tile tooslide open hello search bar and results pane.</span></span>

   ![](./media/search-explorer/search-explorer-tile.png)

## <a name="start-searching"></a><span data-ttu-id="b5135-117">Начните поиск.</span><span class="sxs-lookup"><span data-stu-id="b5135-117">Start searching</span></span>

<span data-ttu-id="b5135-118">При использовании hello обозреватель поиска, можно указать [параметров запроса](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) запроса tooformulate hello.</span><span class="sxs-lookup"><span data-stu-id="b5135-118">When using hello Search Explorer, you can specify [query parameters](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) tooformulate hello query.</span></span>

1. <span data-ttu-id="b5135-119">В **строке запроса** введите запрос и нажмите кнопку **Поиск**.</span><span class="sxs-lookup"><span data-stu-id="b5135-119">In **Query string**, type a query and then press **Search**.</span></span> 

   <span data-ttu-id="b5135-120">Строка запроса Hello автоматически разбивается на правильный запрос hello toosubmit URL-адрес HTTP-запроса по hello REST API поиска Azure.</span><span class="sxs-lookup"><span data-stu-id="b5135-120">hello query string is automatically parsed into hello proper request URL toosubmit a HTTP request against hello Azure Search REST API.</span></span>   
   
   <span data-ttu-id="b5135-121">Можно использовать любой допустимый простого или полного Lucene синтаксис toocreate hello запроса.</span><span class="sxs-lookup"><span data-stu-id="b5135-121">You can use any valid simple or full Lucene query syntax toocreate hello request.</span></span> <span data-ttu-id="b5135-122">Hello `*` символ является поиск пуст или не задан эквивалентный tooan, который возвращает все документы в произвольном порядке.</span><span class="sxs-lookup"><span data-stu-id="b5135-122">hello `*` character is equivalent tooan empty or unspecified search that returns all documents in no particular order.</span></span>

2. <span data-ttu-id="b5135-123">В **результатов**, результаты запроса должны быть представлены в необработанный JSON, идентичные toohello полезные данные возвращаются в текст ответа HTTP при выдаче запросов программными средствами.</span><span class="sxs-lookup"><span data-stu-id="b5135-123">In  **Results**, query results are presented in raw JSON, identical toohello payload returned in an HTTP Response Body when issuing requests programmatically.</span></span>

   ![](./media/search-explorer/search-bar.png)

## <a name="next-steps"></a><span data-ttu-id="b5135-124">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b5135-124">Next steps</span></span>

<span data-ttu-id="b5135-125">Hello следующие ресурсы предоставляют дополнительные сведения о синтаксисе и примеры.</span><span class="sxs-lookup"><span data-stu-id="b5135-125">hello following resources provide additional query syntax information and examples.</span></span>

 + [<span data-ttu-id="b5135-126">Простой синтаксис запросов</span><span class="sxs-lookup"><span data-stu-id="b5135-126">Simple query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) 
 + [<span data-ttu-id="b5135-127">Синтаксис запросов Lucene</span><span class="sxs-lookup"><span data-stu-id="b5135-127">Lucene query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) 
 + [<span data-ttu-id="b5135-128">Примеры синтаксиса запросов Lucene для создания запросов в службе поиска Azure</span><span class="sxs-lookup"><span data-stu-id="b5135-128">Lucene query syntax examples</span></span>](https://docs.microsoft.com/azure/search/search-query-lucene-examples) 
 + <span data-ttu-id="b5135-129">[OData Expression Syntax for Azure Search](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search) (Синтаксис выражений OData для службы поиска Azure)</span><span class="sxs-lookup"><span data-stu-id="b5135-129">[OData Filter expression syntax](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search)</span></span> 