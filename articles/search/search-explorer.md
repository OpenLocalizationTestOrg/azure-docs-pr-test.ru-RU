---
title: "Отправка запросов в индекс службы поиска Azure с помощью портала | Документация Майкрософт"
description: "Создайте поисковый запрос в проводнике поиска на портале Azure."
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
ms.openlocfilehash: dd68d8ed073bf7b8666ddef35a2f1f84df690b4b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="query-an-azure-search-index-using-search-explorer-in-the-azure-portal"></a><span data-ttu-id="afb08-103">Отправка запросов в индекс службы поиска Azure с использованием обозревателя поиска на портале Azure</span><span class="sxs-lookup"><span data-stu-id="afb08-103">Query an Azure Search index using Search Explorer in the Azure Portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="afb08-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="afb08-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="afb08-105">Портал</span><span class="sxs-lookup"><span data-stu-id="afb08-105">Portal</span></span>](search-explorer.md)
> * [<span data-ttu-id="afb08-106">.NET</span><span class="sxs-lookup"><span data-stu-id="afb08-106">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="afb08-107">REST</span><span class="sxs-lookup"><span data-stu-id="afb08-107">REST</span></span>](search-query-rest-api.md)
> 
> 

<span data-ttu-id="afb08-108">В этой статье показано, как отправлять запросы в индекс службы поиска Azure с помощью **обозревателя поиска** на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="afb08-108">This article shows you how to query an Azure Search index using **Search Explorer** in the Azure portal.</span></span> <span data-ttu-id="afb08-109">Используйте обозреватель поиска, чтобы отправить простые строки запросов или расширенные строки запросов Lucene в любой имеющийся индекс в службе.</span><span class="sxs-lookup"><span data-stu-id="afb08-109">You can use Search Explorer to submit simple or full Lucene query strings to any existing index in your service.</span></span>

## <a name="open-the-service-dashboard"></a><span data-ttu-id="afb08-110">Открытие панели мониторинга службы</span><span class="sxs-lookup"><span data-stu-id="afb08-110">Open the service dashboard</span></span>
1. <span data-ttu-id="afb08-111">Щелкните **Все ресурсы** на панели переходов слева на [портале Azure](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).</span><span class="sxs-lookup"><span data-stu-id="afb08-111">Click **All resources** in the jump bar on the left side of the [Azure portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).</span></span>
2. <span data-ttu-id="afb08-112">Выберите службу поиска Azure.</span><span class="sxs-lookup"><span data-stu-id="afb08-112">Select your Azure Search service.</span></span>

## <a name="select-an-index"></a><span data-ttu-id="afb08-113">Выбор индекса</span><span class="sxs-lookup"><span data-stu-id="afb08-113">Select an index</span></span>

<span data-ttu-id="afb08-114">Выберите индекс, в котором нужно выполнить поиск, на плитке **Индексы**.</span><span class="sxs-lookup"><span data-stu-id="afb08-114">Select the index you would like to search from the **Indexes** tile.</span></span>

   ![](./media/search-explorer/pick-index.png)

## <a name="open-search-explorer"></a><span data-ttu-id="afb08-115">Открытие обозревателя поиска</span><span class="sxs-lookup"><span data-stu-id="afb08-115">Open Search Explorer</span></span>

<span data-ttu-id="afb08-116">Щелкните плитку обозревателя поиска, чтобы открыть панель поиска и область результатов.</span><span class="sxs-lookup"><span data-stu-id="afb08-116">Click on the Search Explorer tile to slide open the search bar and results pane.</span></span>

   ![](./media/search-explorer/search-explorer-tile.png)

## <a name="start-searching"></a><span data-ttu-id="afb08-117">Начните поиск.</span><span class="sxs-lookup"><span data-stu-id="afb08-117">Start searching</span></span>

<span data-ttu-id="afb08-118">При использовании обозревателя поиска можно указать [параметры запроса](https://docs.microsoft.com/rest/api/searchservice/Search-Documents), чтобы сформировать запрос.</span><span class="sxs-lookup"><span data-stu-id="afb08-118">When using the Search Explorer, you can specify [query parameters](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) to formulate the query.</span></span>

1. <span data-ttu-id="afb08-119">В **строке запроса** введите запрос и нажмите кнопку **Поиск**.</span><span class="sxs-lookup"><span data-stu-id="afb08-119">In **Query string**, type a query and then press **Search**.</span></span> 

   <span data-ttu-id="afb08-120">Строка запроса автоматически преобразуется в правильный URL-адрес запроса для отправки HTTP-запроса в REST API службы поиска Azure.</span><span class="sxs-lookup"><span data-stu-id="afb08-120">The query string is automatically parsed into the proper request URL to submit a HTTP request against the Azure Search REST API.</span></span>   
   
   <span data-ttu-id="afb08-121">Используйте любой допустимый простой синтаксис запросов или синтаксис расширенных запросов Lucene, чтобы создать запрос.</span><span class="sxs-lookup"><span data-stu-id="afb08-121">You can use any valid simple or full Lucene query syntax to create the request.</span></span> <span data-ttu-id="afb08-122">Знак `*` эквивалентен пустому полю поиска или неуказанным условиям поиска, который возвращает все документы в произвольном порядке.</span><span class="sxs-lookup"><span data-stu-id="afb08-122">The `*` character is equivalent to an empty or unspecified search that returns all documents in no particular order.</span></span>

2. <span data-ttu-id="afb08-123">В области **результатов** результаты запроса будут представлены в необработанном формате JSON аналогично полезным данным, возвращенным в тексте HTTP-ответа при программной отправке запросов.</span><span class="sxs-lookup"><span data-stu-id="afb08-123">In  **Results**, query results are presented in raw JSON, identical to the payload returned in an HTTP Response Body when issuing requests programmatically.</span></span>

   ![](./media/search-explorer/search-bar.png)

## <a name="next-steps"></a><span data-ttu-id="afb08-124">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="afb08-124">Next steps</span></span>

<span data-ttu-id="afb08-125">Дополнительные сведения о синтаксисе запросов и примеры см. в следующих ресурсах.</span><span class="sxs-lookup"><span data-stu-id="afb08-125">The following resources provide additional query syntax information and examples.</span></span>

 + [<span data-ttu-id="afb08-126">Простой синтаксис запросов</span><span class="sxs-lookup"><span data-stu-id="afb08-126">Simple query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) 
 + [<span data-ttu-id="afb08-127">Синтаксис запросов Lucene</span><span class="sxs-lookup"><span data-stu-id="afb08-127">Lucene query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) 
 + [<span data-ttu-id="afb08-128">Примеры синтаксиса запросов Lucene для создания запросов в службе поиска Azure</span><span class="sxs-lookup"><span data-stu-id="afb08-128">Lucene query syntax examples</span></span>](https://docs.microsoft.com/azure/search/search-query-lucene-examples) 
 + <span data-ttu-id="afb08-129">[OData Expression Syntax for Azure Search](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search) (Синтаксис выражений OData для службы поиска Azure)</span><span class="sxs-lookup"><span data-stu-id="afb08-129">[OData Filter expression syntax](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search)</span></span> 