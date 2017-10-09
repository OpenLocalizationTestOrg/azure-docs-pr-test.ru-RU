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
# <a name="query-an-azure-search-index-using-search-explorer-in-hello-azure-portal"></a>Запрос с помощью обозревателя поиска в портале Azure hello индекс поиска Azure
> [!div class="op_single_selector"]
> * [Обзор](search-query-overview.md)
> * [Портал](search-explorer.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
> 
> 

В этой статье показано, как tooquery поиска Azure индекс с помощью **обозреватель поиска** в hello портал Azure. Поиск в обозревателе toosubmit простого или полного Lucene строки tooany существующий индекс запросов можно использовать в службе.

## <a name="open-hello-service-dashboard"></a>Привет открыть панель мониторинга службы
1. Нажмите кнопку **все ресурсы** полосы перехода hello в hello слева от оператора hello [портал Azure](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).
2. Выберите службу поиска Azure.

## <a name="select-an-index"></a>Выбор индекса

Выберите hello индекс хотелось бы toosearch из hello **индексы** плитки.

   ![](./media/search-explorer/pick-index.png)

## <a name="open-search-explorer"></a>Открытие обозревателя поиска

Щелкните панель поиска откройте hello tooslide плитки обозреватель поиска hello и панель результатов.

   ![](./media/search-explorer/search-explorer-tile.png)

## <a name="start-searching"></a>Начните поиск.

При использовании hello обозреватель поиска, можно указать [параметров запроса](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) запроса tooformulate hello.

1. В **строке запроса** введите запрос и нажмите кнопку **Поиск**. 

   Строка запроса Hello автоматически разбивается на правильный запрос hello toosubmit URL-адрес HTTP-запроса по hello REST API поиска Azure.   
   
   Можно использовать любой допустимый простого или полного Lucene синтаксис toocreate hello запроса. Hello `*` символ является поиск пуст или не задан эквивалентный tooan, который возвращает все документы в произвольном порядке.

2. В **результатов**, результаты запроса должны быть представлены в необработанный JSON, идентичные toohello полезные данные возвращаются в текст ответа HTTP при выдаче запросов программными средствами.

   ![](./media/search-explorer/search-bar.png)

## <a name="next-steps"></a>Дальнейшие действия

Hello следующие ресурсы предоставляют дополнительные сведения о синтаксисе и примеры.

 + [Простой синтаксис запросов](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) 
 + [Синтаксис запросов Lucene](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) 
 + [Примеры синтаксиса запросов Lucene для создания запросов в службе поиска Azure](https://docs.microsoft.com/azure/search/search-query-lucene-examples) 
 + [OData Expression Syntax for Azure Search](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search) (Синтаксис выражений OData для службы поиска Azure) 