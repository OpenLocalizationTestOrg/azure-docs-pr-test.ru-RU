---
title: "Результаты поиска toopage aaaHow в поиске Azure | Документы Microsoft"
description: "Разбивка на страницы в службе Поиск Azure, размещенной облачной службе поиска в Microsoft Azure."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
ms.assetid: a0a1d315-8624-4cdf-b38e-ba12569c6fcc
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/29/2016
ms.author: heidist
ms.openlocfilehash: e3abc1ca4d5994b0a77955379081a4fcfa5a7fa7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopage-search-results-in-azure-search"></a><span data-ttu-id="a397f-103">Отображением результатов поиска toopage в поиске Azure</span><span class="sxs-lookup"><span data-stu-id="a397f-103">How toopage search results in Azure Search</span></span>
<span data-ttu-id="a397f-104">Эта статья содержит рекомендации о том, как toouse hello API REST службы поиска Azure tooimplement стандартные элементы поиска страница результатов, например общего числа, получение документа, порядок сортировки и навигации.</span><span class="sxs-lookup"><span data-stu-id="a397f-104">This article provides guidance on how toouse hello Azure Search Service REST API tooimplement standard elements of a search results page, such as total counts, document retrieval, sort orders, and navigation.</span></span>

<span data-ttu-id="a397f-105">В каждом случае упомянутых ниже указываются параметры, связанные с страницы, задействованных или данные страницы результатов поиска tooyour с помощью hello [поиска документов](http://msdn.microsoft.com/library/azure/dn798927.aspx) tooyour запросов, отправленных службой поиска Azure.</span><span class="sxs-lookup"><span data-stu-id="a397f-105">In every case mentioned below, page-related options that contribute data or information tooyour search results page are specified through hello [Search Document](http://msdn.microsoft.com/library/azure/dn798927.aspx) requests sent tooyour Azure Search Service.</span></span> <span data-ttu-id="a397f-106">Запросы включают команды GET, путь и параметры запроса, которые сообщают о запрашиваемом службы hello и как tooformulate hello ответа.</span><span class="sxs-lookup"><span data-stu-id="a397f-106">Requests include a GET command, path, and query parameters that inform hello service what is being requested, and how tooformulate hello response.</span></span>

> [!NOTE]
> <span data-ttu-id="a397f-107">Допустимый запрос содержит несколько элементов, например URL-адрес службы и путь, HTTP-команду, `api-version` и т. д.</span><span class="sxs-lookup"><span data-stu-id="a397f-107">A valid request includes a number of elements, such as a service URL and path, HTTP verb, `api-version`, and so on.</span></span> <span data-ttu-id="a397f-108">Для краткости мы ограничиваются hello toohighlight примеры просто hello синтаксис, соответствующий toopagination.</span><span class="sxs-lookup"><span data-stu-id="a397f-108">For brevity, we trimmed hello examples toohighlight just hello syntax that is relevant toopagination.</span></span> <span data-ttu-id="a397f-109">См. в разделе hello [API REST службы поиска Azure](http://msdn.microsoft.com/library/azure/dn798935.aspx) Дополнительные сведения о синтаксисе запроса.</span><span class="sxs-lookup"><span data-stu-id="a397f-109">Please see hello [Azure Search Service REST API](http://msdn.microsoft.com/library/azure/dn798935.aspx) documentation for details about request syntax.</span></span>
> 
> 

## <a name="total-hits-and-page-counts"></a><span data-ttu-id="a397f-110">Общее количество совпадений и страниц</span><span class="sxs-lookup"><span data-stu-id="a397f-110">Total hits and Page Counts</span></span>
<span data-ttu-id="a397f-111">Отображается общее количество результатов, возвращенных запросом, а затем их возвращения результатов небольшими фрагментами hello, является основной toovirtually все страницы поиска.</span><span class="sxs-lookup"><span data-stu-id="a397f-111">Showing hello total number of results returned from a query, and then returning those results in smaller chunks, is fundamental toovirtually all search pages.</span></span>

![][1]

<span data-ttu-id="a397f-112">В поиске Azure используйте hello `$count`, `$top`, и `$skip` tooreturn параметры этих значений.</span><span class="sxs-lookup"><span data-stu-id="a397f-112">In Azure Search, you use hello `$count`, `$top`, and `$skip` parameters tooreturn these values.</span></span> <span data-ttu-id="a397f-113">Hello примере показан образец запроса для всего попаданий, возвращаются в виде `@OData.count`:</span><span class="sxs-lookup"><span data-stu-id="a397f-113">hello following example shows a sample request for total hits, returned as `@OData.count`:</span></span>

        GET /indexes/onlineCatalog/docs?$count=true

<span data-ttu-id="a397f-114">Получать документы в группах 15, а также показать Всего попаданий hello, начиная с первой страницы приветствия:</span><span class="sxs-lookup"><span data-stu-id="a397f-114">Retrieve documents in groups of 15, and also show hello total hits, starting at hello first page:</span></span>

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

<span data-ttu-id="a397f-115">Разбивки на страницы результатов требуются оба `$top` и `$skip`, где `$top` указывает, сколько элементов tooreturn в пакете, и `$skip` указывает, сколько элементов tooskip.</span><span class="sxs-lookup"><span data-stu-id="a397f-115">Paginating results requires both `$top` and `$skip`, where `$top` specifies how many items tooreturn in a batch, and `$skip` specifies how many items tooskip.</span></span> <span data-ttu-id="a397f-116">В hello следующий пример, каждой страницы отображаются hello рядом 15 элементы, обозначенном hello добавочной переходы в hello `$skip` параметра.</span><span class="sxs-lookup"><span data-stu-id="a397f-116">In hello following example, each page shows hello next 15 items, indicated by hello incremental jumps in hello `$skip` parameter.</span></span>

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=15&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=30&$count=true

## <a name="layout"></a><span data-ttu-id="a397f-117">Макет</span><span class="sxs-lookup"><span data-stu-id="a397f-117">Layout</span></span>
<span data-ttu-id="a397f-118">На странице результатов поиска может потребоваться tooshow эскиза, подмножество полей и страницей ссылку tooa полной версии продукта.</span><span class="sxs-lookup"><span data-stu-id="a397f-118">On a search results page, you might want tooshow a thumbnail image, a subset of fields, and a link tooa full product page.</span></span>

 ![][2]

<span data-ttu-id="a397f-119">В поиске Azure, можно использовать `$select` уточняющего запроса командой tooimplement это взаимодействие.</span><span class="sxs-lookup"><span data-stu-id="a397f-119">In Azure Search, you would use `$select` and a lookup command tooimplement this experience.</span></span>

<span data-ttu-id="a397f-120">tooreturn подмножество полей для мозаичного макета:</span><span class="sxs-lookup"><span data-stu-id="a397f-120">tooreturn a subset of fields for a tiled layout:</span></span>

        GET /indexes/ onlineCatalog/docs?search=*&$select=productName,imageFile,description,price,rating 

<span data-ttu-id="a397f-121">Изображения и файлам мультимедиа не непосредственно для поиска и должны храниться в другой платформы хранения, больших двоичных объектов Azure, например хранилище tooreduce затраты.</span><span class="sxs-lookup"><span data-stu-id="a397f-121">Images and media files are not directly searchable and should be stored in another storage platform, such as Azure Blob storage, tooreduce costs.</span></span> <span data-ttu-id="a397f-122">В документах и индекс hello определите поле, содержащее URL-адрес hello hello внешнего содержимого.</span><span class="sxs-lookup"><span data-stu-id="a397f-122">In hello index and documents, define a field that stores hello URL address of hello external content.</span></span> <span data-ttu-id="a397f-123">Затем можно использовать поле hello как ссылку на изображение.</span><span class="sxs-lookup"><span data-stu-id="a397f-123">You can then use hello field as an image reference.</span></span> <span data-ttu-id="a397f-124">изображение toohello Hello URL-адрес должен находиться в документе hello.</span><span class="sxs-lookup"><span data-stu-id="a397f-124">hello URL toohello image should be in hello document.</span></span>

<span data-ttu-id="a397f-125">странице описания продукта для tooretrieve **onClick** события, используйте [поиск документов](http://msdn.microsoft.com/library/azure/dn798929.aspx) toopass в ключе документа tooretrieve hello hello.</span><span class="sxs-lookup"><span data-stu-id="a397f-125">tooretrieve a product description page for an **onClick** event, use [Lookup Document](http://msdn.microsoft.com/library/azure/dn798929.aspx) toopass in hello key of hello document tooretrieve.</span></span> <span data-ttu-id="a397f-126">Тип данных Hello hello ключа является `Edm.String`.</span><span class="sxs-lookup"><span data-stu-id="a397f-126">hello data type of hello key is `Edm.String`.</span></span> <span data-ttu-id="a397f-127">В данном примере это *246810*.</span><span class="sxs-lookup"><span data-stu-id="a397f-127">In this example, it is *246810*.</span></span> 

        GET /indexes/onlineCatalog/docs/246810

## <a name="sort-by-relevance-rating-or-price"></a><span data-ttu-id="a397f-128">Сортировка по соответствию, оценке или цене</span><span class="sxs-lookup"><span data-stu-id="a397f-128">Sort by relevance, rating, or price</span></span>
<span data-ttu-id="a397f-129">Часто порядки сортировки по умолчанию toorelevance, но не общие toomake альтернативный порядок сортировки рукой, чтобы клиентов можно быстро передвинуть существующие результаты в другом порядке rank.</span><span class="sxs-lookup"><span data-stu-id="a397f-129">Sort orders often default toorelevance, but it's common toomake alternative sort orders readily available so that customers can quickly reshuffle existing results into a different rank order.</span></span>

 ![][3]

<span data-ttu-id="a397f-130">В поиске Azure сортировки основан на hello `$orderby` выражения для всех полей, которые индексируются как`"Sortable": true.`</span><span class="sxs-lookup"><span data-stu-id="a397f-130">In Azure Search, sorting is based on hello `$orderby` expression, for all fields that are indexed as `"Sortable": true.`</span></span>

<span data-ttu-id="a397f-131">Соответствие тесно связано с профилями оценки.</span><span class="sxs-lookup"><span data-stu-id="a397f-131">Relevance is strongly associated with scoring profiles.</span></span> <span data-ttu-id="a397f-132">Можно использовать hello оценка по умолчанию, которой зависит от порядка toorank анализа и статистики текста все результаты с более высокой оценкой переходом toodocuments с совпадением дополнительные или более строгое условие поиска.</span><span class="sxs-lookup"><span data-stu-id="a397f-132">You can use hello default scoring, which relies on text analysis and statistics toorank order all results, with higher scores going toodocuments with more or stronger matches on a search term.</span></span>

<span data-ttu-id="a397f-133">Альтернативные сортировки обычно связаны с **onClick** события, обратный вызов метода tooa, создает hello порядок сортировки.</span><span class="sxs-lookup"><span data-stu-id="a397f-133">Alternative sort orders are typically associated with **onClick** events that call back tooa method that builds hello sort order.</span></span> <span data-ttu-id="a397f-134">Например, если взять этот элемент страницы:</span><span class="sxs-lookup"><span data-stu-id="a397f-134">For example, given this page element:</span></span>

 ![][4]

<span data-ttu-id="a397f-135">Необходимо создать метод, который принимает параметр сортировки hello выбран в качестве входного и возвращает упорядоченный список для hello условие, связанное с этого параметра.</span><span class="sxs-lookup"><span data-stu-id="a397f-135">You would create a method that accepts hello selected sort option as input, and returns an ordered list for hello criteria associated with that option.</span></span>

 ![][5]

> [!NOTE]
> <span data-ttu-id="a397f-136">Оценка по умолчанию hello является достаточным для многих сценариев, рекомендуется вместо индексация релевантности пользовательский профиль повышения.</span><span class="sxs-lookup"><span data-stu-id="a397f-136">While hello default scoring is sufficient for many scenarios, we recommend basing relevance on a custom scoring profile instead.</span></span> <span data-ttu-id="a397f-137">Настраиваемый профиль оценки дает вида tooboost элементов, которые являются более эффективным tooyour бизнеса.</span><span class="sxs-lookup"><span data-stu-id="a397f-137">A custom scoring profile gives you a way tooboost items that are more beneficial tooyour business.</span></span> <span data-ttu-id="a397f-138">Дополнительные сведения см. в статье [Add scoring profiles to a search index (Azure Search Service REST API)](http://msdn.microsoft.com/library/azure/dn798928.aspx) (Добавление профилей оценки в индекс поиска (REST API службы поиска Azure)).</span><span class="sxs-lookup"><span data-stu-id="a397f-138">See [Add a scoring profile](http://msdn.microsoft.com/library/azure/dn798928.aspx) for more information.</span></span> 
> 
> 

## <a name="faceted-navigation"></a><span data-ttu-id="a397f-139">Фасетная навигация</span><span class="sxs-lookup"><span data-stu-id="a397f-139">Faceted navigation</span></span>
<span data-ttu-id="a397f-140">Навигация в поиске распространено на странице результатов, часто находится на стороне hello или верхней части страницы.</span><span class="sxs-lookup"><span data-stu-id="a397f-140">Search navigation is common on a results page, often located at hello side or top of a page.</span></span> <span data-ttu-id="a397f-141">В Поиске Azure фасетная навигация обеспечивает самостоятельный поиск на основе предварительно заданных фильтров.</span><span class="sxs-lookup"><span data-stu-id="a397f-141">In Azure Search, faceted navigation provides self-directed search based on predefined filters.</span></span> <span data-ttu-id="a397f-142">Дополнительные сведения см. в статье [Как реализовать фасетную навигацию в службе поиска Azure](search-faceted-navigation.md).</span><span class="sxs-lookup"><span data-stu-id="a397f-142">See [Faceted navigation in Azure Search](search-faceted-navigation.md) for details.</span></span>

## <a name="filters-at-hello-page-level"></a><span data-ttu-id="a397f-143">Фильтры на уровне страницы приветствия</span><span class="sxs-lookup"><span data-stu-id="a397f-143">Filters at hello page level</span></span>
<span data-ttu-id="a397f-144">Если проекту решения выделенной службы поиска страниц для определенных типов содержимого (например, сетевой розничный приложение, имеющее отделов, перечисленные в начале hello hello страницы), можно вставить выражение фильтра, наряду с **onClick** tooopen событий на страницу в предварительно профильтрованном состояния.</span><span class="sxs-lookup"><span data-stu-id="a397f-144">If your solution design included dedicated search pages for specific types of content (for example, an online retail application that has departments listed at hello top of hello page), you can insert a filter expression alongside an **onClick** event tooopen a page in a prefiltered state.</span></span> 

<span data-ttu-id="a397f-145">Можно отправлять фильтр с выражением поиска или без него.</span><span class="sxs-lookup"><span data-stu-id="a397f-145">You can send a filter with or without a search expression.</span></span> <span data-ttu-id="a397f-146">Например hello следующий запрос используется для фильтрации собственное имя, возвращая только те документы, которые соответствуют его.</span><span class="sxs-lookup"><span data-stu-id="a397f-146">For example, hello following request will filter on brand name, returning only those documents that match it.</span></span>

        GET /indexes/onlineCatalog/docs?$filter=brandname eq ‘Microsoft’ and category eq ‘Games’

<span data-ttu-id="a397f-147">Дополнительные сведения о выражениях `$filter` см. в статье [Search Documents (Azure Search Service REST API)](http://msdn.microsoft.com/library/azure/dn798927.aspx) (Поиск документов (REST API службы поиска Azure)).</span><span class="sxs-lookup"><span data-stu-id="a397f-147">See [Search Documents (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798927.aspx) for more information about `$filter` expressions.</span></span>

## <a name="see-also"></a><span data-ttu-id="a397f-148">См. также</span><span class="sxs-lookup"><span data-stu-id="a397f-148">See Also</span></span>
* [<span data-ttu-id="a397f-149">REST API службы поиска Azure</span><span class="sxs-lookup"><span data-stu-id="a397f-149">Azure Search Service REST API</span></span>](http://msdn.microsoft.com/library/azure/dn798935.aspx)
* [<span data-ttu-id="a397f-150">Операции с индексами</span><span class="sxs-lookup"><span data-stu-id="a397f-150">Index Operations</span></span>](http://msdn.microsoft.com/library/azure/dn798918.aspx)
* [<span data-ttu-id="a397f-151">Операции с документом.</span><span class="sxs-lookup"><span data-stu-id="a397f-151">Document Operations</span></span>](http://msdn.microsoft.com/library/azure/dn800962.aspx)
* [<span data-ttu-id="a397f-152">Поиск Azure: учебники, видеодемонстрации и примеры</span><span class="sxs-lookup"><span data-stu-id="a397f-152">Video and tutorials about Azure Search</span></span>](search-video-demo-tutorial-list.md)
* [<span data-ttu-id="a397f-153">Фасетная навигация в службе поиска Azure</span><span class="sxs-lookup"><span data-stu-id="a397f-153">Faceted Navigation in Azure Search</span></span>](search-faceted-navigation.md)

<!--Image references-->
[1]: ./media/search-pagination-page-layout/Pages-1-Viewing1ofNResults.PNG
[2]: ./media/search-pagination-page-layout/Pages-2-Tiled.PNG
[3]: ./media/search-pagination-page-layout/Pages-3-SortBy.png
[4]: ./media/search-pagination-page-layout/Pages-4-SortbyRelevance.png
[5]: ./media/search-pagination-page-layout/Pages-5-BuildSort.png 
