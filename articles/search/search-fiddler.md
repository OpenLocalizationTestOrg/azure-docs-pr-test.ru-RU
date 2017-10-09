---
title: "aaaHow toouse Fiddler tooevaluate и тестирования интерфейсы REST API поиска Azure | Документы Microsoft"
description: "Использование Fiddler для доступности службы поиска Azure tooverifying подход написания кода и ознакомление hello API-интерфейсов REST."
services: search
documentationcenter: 
author: HeidiSteen
manager: mblythe
editor: 
ms.assetid: 790e5779-c6a3-4a07-9d1e-d6739e6b87d2
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: heidist
ms.openlocfilehash: 2912e1180717d7b40a1e4f7f7f00daf2cc254f0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-fiddler-tooevaluate-and-test-azure-search-rest-apis"></a><span data-ttu-id="ec20d-103">С помощью Fiddler tooevaluate и тестирования интерфейсы REST API поиска Azure</span><span class="sxs-lookup"><span data-stu-id="ec20d-103">Use Fiddler tooevaluate and test Azure Search REST APIs</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="ec20d-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="ec20d-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="ec20d-105">Обозреватель поиска</span><span class="sxs-lookup"><span data-stu-id="ec20d-105">Search Explorer</span></span>](search-explorer.md)
> * [<span data-ttu-id="ec20d-106">Fiddler</span><span class="sxs-lookup"><span data-stu-id="ec20d-106">Fiddler</span></span>](search-fiddler.md)
> * [<span data-ttu-id="ec20d-107">.NET</span><span class="sxs-lookup"><span data-stu-id="ec20d-107">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="ec20d-108">REST</span><span class="sxs-lookup"><span data-stu-id="ec20d-108">REST</span></span>](search-query-rest-api.md)
>
>

<span data-ttu-id="ec20d-109">В этой статье объясняется, как toouse Fiddler, доступной в качестве [бесплатно загрузить с Telerik](http://www.telerik.com/fiddler), tooissue HTTP запросы tooand просмотреть ответы с помощью hello REST API поиска Azure без необходимости toowrite любой код.</span><span class="sxs-lookup"><span data-stu-id="ec20d-109">This article explains how toouse Fiddler, available as a [free download from Telerik](http://www.telerik.com/fiddler), tooissue HTTP requests tooand view responses using hello Azure Search REST API, without having toowrite any code.</span></span> <span data-ttu-id="ec20d-110">Поиск Azure — это полностью управляемая облачная служба поиска в Microsoft Azure с простым программным управлением через API-интерфейсы REST и .NET.</span><span class="sxs-lookup"><span data-stu-id="ec20d-110">Azure Search is fully-managed, hosted cloud search service on Microsoft Azure, easily programmable through .NET and REST APIs.</span></span> <span data-ttu-id="ec20d-111">Hello описаны на API-интерфейс REST службы поиска Azure [MSDN](https://msdn.microsoft.com/library/azure/dn798935.aspx).</span><span class="sxs-lookup"><span data-stu-id="ec20d-111">hello Azure Search service REST APIs are documented on [MSDN](https://msdn.microsoft.com/library/azure/dn798935.aspx).</span></span>

<span data-ttu-id="ec20d-112">Привет, выполнив действия будет создать индекс, отправлять документы, индекс hello запросов и запроса hello системы сведения о службах.</span><span class="sxs-lookup"><span data-stu-id="ec20d-112">In hello following steps, you'll create an index, upload documents, query hello index, and then query hello system for service information.</span></span>

<span data-ttu-id="ec20d-113">Эти шаги toocomplete, вам потребуется службы поиска Azure и `api-key`.</span><span class="sxs-lookup"><span data-stu-id="ec20d-113">toocomplete these steps, you will need an Azure Search service and `api-key`.</span></span> <span data-ttu-id="ec20d-114">В разделе [Создание службы поиска Azure на портале hello](search-create-service-portal.md) инструкции о том, как tooget работы.</span><span class="sxs-lookup"><span data-stu-id="ec20d-114">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for instructions on how tooget started.</span></span>

## <a name="create-an-index"></a><span data-ttu-id="ec20d-115">Создание индекса</span><span class="sxs-lookup"><span data-stu-id="ec20d-115">Create an index</span></span>
1. <span data-ttu-id="ec20d-116">Запустите Fiddler.</span><span class="sxs-lookup"><span data-stu-id="ec20d-116">Start Fiddler.</span></span> <span data-ttu-id="ec20d-117">На hello **файл** меню выберите Отключить **запись трафика** toohide лишние HTTP действий, которые являются несвязанными toohello текущей задачи.</span><span class="sxs-lookup"><span data-stu-id="ec20d-117">On hello **File** menu, turn off **Capture Traffic** toohide extraneous HTTP activity that is unrelated toohello current task.</span></span>
2. <span data-ttu-id="ec20d-118">На hello **Composer** вкладке будет сформулировать запрос, который выглядит как следующий снимок экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="ec20d-118">On hello **Composer** tab, you'll formulate a request that looks like hello following screen shot.</span></span>

      ![][1]
3. <span data-ttu-id="ec20d-119">Выберите **PUT**.</span><span class="sxs-lookup"><span data-stu-id="ec20d-119">Select **PUT**.</span></span>
4. <span data-ttu-id="ec20d-120">Введите URL-адрес, на который указывает URL-адрес службы hello, атрибуты запроса и hello api-version.</span><span class="sxs-lookup"><span data-stu-id="ec20d-120">Enter a URL that specifies hello service URL, request attributes, and hello api-version.</span></span> <span data-ttu-id="ec20d-121">Несколько tookeep указателей помните:</span><span class="sxs-lookup"><span data-stu-id="ec20d-121">A few pointers tookeep in mind:</span></span>

   * <span data-ttu-id="ec20d-122">Используйте HTTPS в качестве префикса hello.</span><span class="sxs-lookup"><span data-stu-id="ec20d-122">Use HTTPS as hello prefix.</span></span>
   * <span data-ttu-id="ec20d-123">Атрибут запроса: "/indexes/hotels".</span><span class="sxs-lookup"><span data-stu-id="ec20d-123">Request attribute is "/indexes/hotels".</span></span> <span data-ttu-id="ec20d-124">Это заставляет toocreate поиска индекс с именем «гостиницы».</span><span class="sxs-lookup"><span data-stu-id="ec20d-124">This tells Search toocreate an index named 'hotels'.</span></span>
   * <span data-ttu-id="ec20d-125">Версия API вводится строчными буквами, в виде "?api-version=2016-09-01".</span><span class="sxs-lookup"><span data-stu-id="ec20d-125">Api-version is lowercase, specified as "?api-version=2016-09-01".</span></span> <span data-ttu-id="ec20d-126">Версии API имеют важное значение, так как обновления Поиска Azure разворачиваются на регулярной основе.</span><span class="sxs-lookup"><span data-stu-id="ec20d-126">API versions are important because Azure Search deploys updates regularly.</span></span> <span data-ttu-id="ec20d-127">В редких случаях обновление службы может вызвать критические изменения toohello API.</span><span class="sxs-lookup"><span data-stu-id="ec20d-127">On rare occasions, a service update may introduce a breaking change toohello API.</span></span> <span data-ttu-id="ec20d-128">Поэтому службе поиска Azure требуется версия API каждого запроса, чтобы вы могли полностью контролировать используемый запрос.</span><span class="sxs-lookup"><span data-stu-id="ec20d-128">For this reason, Azure Search requires an api-version on each request so that you are in full control over which one is used.</span></span>

     <span data-ttu-id="ec20d-129">Hello полный URL-адрес должен выглядеть примерно toohello следующий пример.</span><span class="sxs-lookup"><span data-stu-id="ec20d-129">hello full URL should look similar toohello following example.</span></span>

             https://my-app.search.windows.net/indexes/hotels?api-version=2016-09-01
5. <span data-ttu-id="ec20d-130">Укажите заголовок запроса hello, заменив значения, которые являются допустимыми для службы узла hello и ключ api.</span><span class="sxs-lookup"><span data-stu-id="ec20d-130">Specify hello request header, replacing hello host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
6. <span data-ttu-id="ec20d-131">В текст запроса вставьте hello поля, составляющие определение индекса hello.</span><span class="sxs-lookup"><span data-stu-id="ec20d-131">In Request Body, paste in hello fields that make up hello index definition.</span></span>

          {
         "name": "hotels",  
         "fields": [
           {"name": "hotelId", "type": "Edm.String", "key":true, "searchable": false},
           {"name": "baseRate", "type": "Edm.Double"},
           {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
           {"name": "hotelName", "type": "Edm.String"},
           {"name": "category", "type": "Edm.String"},
           {"name": "tags", "type": "Collection(Edm.String)"},
           {"name": "parkingIncluded", "type": "Edm.Boolean"},
           {"name": "smokingAllowed", "type": "Edm.Boolean"},
           {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
           {"name": "rating", "type": "Edm.Int32"},
           {"name": "location", "type": "Edm.GeographyPoint"}
          ]
         }
7. <span data-ttu-id="ec20d-132">Нажмите **Execute (Выполнить)**.</span><span class="sxs-lookup"><span data-stu-id="ec20d-132">Click **Execute**.</span></span>

<span data-ttu-id="ec20d-133">Через несколько секунд появится ответ HTTP 201 в список сеансов hello, возвращающее hello индекс был создан успешно.</span><span class="sxs-lookup"><span data-stu-id="ec20d-133">In a few seconds, you should see an HTTP 201 response in hello session list, indicating hello index was created successfully.</span></span>

<span data-ttu-id="ec20d-134">Если вы получаете HTTP 504, убедитесь, что hello URL-адрес указывает протокол HTTPS.</span><span class="sxs-lookup"><span data-stu-id="ec20d-134">If you get HTTP 504, verify hello URL specifies HTTPS.</span></span> <span data-ttu-id="ec20d-135">Если вы видите HTTP 400 или 404, tooverify тело запроса hello Проверьте наличие были без ошибок копирования и вставки.</span><span class="sxs-lookup"><span data-stu-id="ec20d-135">If you see HTTP 400 or 404, check hello request body tooverify there were no copy-paste errors.</span></span> <span data-ttu-id="ec20d-136">HTTP 403 обычно указывает на проблему с hello ключ api (недопустимый ключ или синтаксис неполадки как указывается hello api ключ).</span><span class="sxs-lookup"><span data-stu-id="ec20d-136">An HTTP 403 typically indicates a problem with hello api-key (either an invalid key or a syntax problem with how hello api-key is specified).</span></span>

## <a name="load-documents"></a><span data-ttu-id="ec20d-137">Загрузка документов</span><span class="sxs-lookup"><span data-stu-id="ec20d-137">Load documents</span></span>
<span data-ttu-id="ec20d-138">На hello **Composer** , документы toopost запрос будет выглядеть вкладка hello следующее.</span><span class="sxs-lookup"><span data-stu-id="ec20d-138">On hello **Composer** tab, your request toopost documents will look like hello following.</span></span> <span data-ttu-id="ec20d-139">текст Hello hello запроса содержит данные поиска hello отелях 4.</span><span class="sxs-lookup"><span data-stu-id="ec20d-139">hello body of hello request contains hello search data for 4 hotels.</span></span>

   ![][2]

1. <span data-ttu-id="ec20d-140">Выберите **POST**.</span><span class="sxs-lookup"><span data-stu-id="ec20d-140">Select **POST**.</span></span>
2. <span data-ttu-id="ec20d-141">Введите URL-адрес, начинающийся с HTTPS, далее URL-адрес вашей службы, а затем "/indexes/<'indexname'>/docs/index?api-version=2016-09-01".</span><span class="sxs-lookup"><span data-stu-id="ec20d-141">Enter a URL that starts with HTTPS, followed by your service URL, followed by "/indexes/<'indexname'>/docs/index?api-version=2016-09-01".</span></span> <span data-ttu-id="ec20d-142">Hello полный URL-адрес должен выглядеть примерно toohello следующий пример.</span><span class="sxs-lookup"><span data-stu-id="ec20d-142">hello full URL should look similar toohello following example.</span></span>

         https://my-app.search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
3. <span data-ttu-id="ec20d-143">Заголовок запроса должен быть hello же как и раньше.</span><span class="sxs-lookup"><span data-stu-id="ec20d-143">Request Header should be hello same as before.</span></span> <span data-ttu-id="ec20d-144">Помните, заменить узла hello и ключ api со значениями, которые являются допустимыми для службы.</span><span class="sxs-lookup"><span data-stu-id="ec20d-144">Remember that you replaced hello host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. <span data-ttu-id="ec20d-145">Hello текст запроса содержит четыре документы toobe добавлены toohello гостиницы индекса.</span><span class="sxs-lookup"><span data-stu-id="ec20d-145">hello Request Body contains four documents toobe added toohello hotels index.</span></span>

         {
         "value": [
         {
             "@search.action": "upload",
             "hotelId": "1",
             "baseRate": 199.0,
             "description": "Best hotel in town",
             "hotelName": "Fancy Stay",
             "category": "Luxury",
             "tags": ["pool", "view", "wifi", "concierge"],
             "parkingIncluded": false,
             "smokingAllowed": false,
             "lastRenovationDate": "2010-06-27T00:00:00Z",
             "rating": 5,
             "location": { "type": "Point", "coordinates": [-122.131577, 47.678581] }
           },
           {
             "@search.action": "upload",
             "hotelId": "2",
             "baseRate": 79.99,
             "description": "Cheapest hotel in town",
             "hotelName": "Roach Motel",
             "category": "Budget",
             "tags": ["motel", "budget"],
             "parkingIncluded": true,
             "smokingAllowed": true,
             "lastRenovationDate": "1982-04-28T00:00:00Z",
             "rating": 1,
             "location": { "type": "Point", "coordinates": [-122.131577, 49.678581] }
           },
           {
             "@search.action": "upload",
             "hotelId": "3",
             "baseRate": 279.99,
             "description": "Surprisingly expensive",
             "hotelName": "Dew Drop Inn",
             "category": "Bed and Breakfast",
             "tags": ["charming", "quaint"],
             "parkingIncluded": true,
             "smokingAllowed": false,
             "lastRenovationDate": null,
             "rating": 4,
             "location": { "type": "Point", "coordinates": [-122.33207, 47.60621] }
           },
           {
             "@search.action": "upload",
             "hotelId": "4",
             "baseRate": 220.00,
             "description": "This could be hello one",
             "hotelName": "A Hotel for Everyone",
             "category": "Basic hotel",
             "tags": ["pool", "wifi"],
             "parkingIncluded": true,
             "smokingAllowed": false,
             "lastRenovationDate": null,
             "rating": 4,
             "location": { "type": "Point", "coordinates": [-122.12151, 47.67399] }
           }
          ]
         }
5. <span data-ttu-id="ec20d-146">Нажмите **Execute (Выполнить)**.</span><span class="sxs-lookup"><span data-stu-id="ec20d-146">Click **Execute**.</span></span>

<span data-ttu-id="ec20d-147">Через несколько секунд появится ответ HTTP 200 в список сеансов hello.</span><span class="sxs-lookup"><span data-stu-id="ec20d-147">In a few seconds, you should see an HTTP 200 response in hello session list.</span></span> <span data-ttu-id="ec20d-148">Это указывает на приветствия документы успешно создан.</span><span class="sxs-lookup"><span data-stu-id="ec20d-148">This indicates hello documents were created successfully.</span></span> <span data-ttu-id="ec20d-149">Если вы получаете 207, по крайней мере один документ сбой tooupload.</span><span class="sxs-lookup"><span data-stu-id="ec20d-149">If you get a 207, at least one document failed tooupload.</span></span> <span data-ttu-id="ec20d-150">Если код 404, имеется синтаксическая ошибка в hello заголовок или текст запроса hello.</span><span class="sxs-lookup"><span data-stu-id="ec20d-150">If you get a 404, you have a syntax error in either hello header or body of hello request.</span></span>

## <a name="query-hello-index"></a><span data-ttu-id="ec20d-151">Индекс hello запросов</span><span class="sxs-lookup"><span data-stu-id="ec20d-151">Query hello index</span></span>
<span data-ttu-id="ec20d-152">После загрузки индекса и документов можно формировать запросы к ним.</span><span class="sxs-lookup"><span data-stu-id="ec20d-152">Now that an index and documents are loaded, you can issue queries against them.</span></span>  <span data-ttu-id="ec20d-153">На hello **Composer** вкладке **получить** команду, которая запрашивает службы будет выглядеть аналогично toohello следующий снимок экрана.</span><span class="sxs-lookup"><span data-stu-id="ec20d-153">On hello **Composer** tab, a **GET** command that queries your service will look similar toohello following screen shot.</span></span>

   ![][3]

1. <span data-ttu-id="ec20d-154">Выберите **GET**.</span><span class="sxs-lookup"><span data-stu-id="ec20d-154">Select **GET**.</span></span>
2. <span data-ttu-id="ec20d-155">Введите URL, начинающийся с HTTPS, далее URL вашей службы, далее "/indexes/<'indexname'>/docs?", далее параметры запроса.</span><span class="sxs-lookup"><span data-stu-id="ec20d-155">Enter a URL that starts with HTTPS, followed by your service URL, followed by "/indexes/<'indexname'>/docs?", followed by query parameters.</span></span> <span data-ttu-id="ec20d-156">В качестве примера используйте hello URL-адреса, заменив имя узла образец hello допустимый для службы.</span><span class="sxs-lookup"><span data-stu-id="ec20d-156">By way of example, use hello following URL, replacing hello sample host name with one that is valid for your service.</span></span>

         https://my-app.search.windows.net/indexes/hotels/docs?search=motel&facet=category&facet=rating,values:1|2|3|4|5&api-version=2016-09-01

   <span data-ttu-id="ec20d-157">Этот запрос выполняет поиск по hello термин «motel» и извлекает аспект категории для оценки.</span><span class="sxs-lookup"><span data-stu-id="ec20d-157">This query searches on hello term “motel” and retrieves facet categories for ratings.</span></span>
3. <span data-ttu-id="ec20d-158">Заголовок запроса должен быть hello же как и раньше.</span><span class="sxs-lookup"><span data-stu-id="ec20d-158">Request Header should be hello same as before.</span></span> <span data-ttu-id="ec20d-159">Помните, заменить узла hello и ключ api со значениями, которые являются допустимыми для службы.</span><span class="sxs-lookup"><span data-stu-id="ec20d-159">Remember that you replaced hello host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444

<span data-ttu-id="ec20d-160">код ответа Hello должен 200 и hello ответа вывод должен выглядеть примерно toohello следующий снимок экрана.</span><span class="sxs-lookup"><span data-stu-id="ec20d-160">hello response code should be 200, and hello response output should look similar toohello following screen shot.</span></span>

   ![][4]

<span data-ttu-id="ec20d-161">Hello следующий пример взят из hello [операцию поиска индекса (API поиска Azure)](http://msdn.microsoft.com/library/dn798927.aspx) на сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="ec20d-161">hello following example query is from hello [Search Index operation (Azure Search API)](http://msdn.microsoft.com/library/dn798927.aspx) on MSDN.</span></span> <span data-ttu-id="ec20d-162">Многие примеры запросов hello в этом разделе содержат пробелы, которые не разрешены в Fiddler.</span><span class="sxs-lookup"><span data-stu-id="ec20d-162">Many of hello example queries in this topic include spaces, which are not allowed in Fiddler.</span></span> <span data-ttu-id="ec20d-163">Замените каждый пространства с символ «+» перед вставкой в hello строку запроса перед выполнением запроса hello в Fiddler.</span><span class="sxs-lookup"><span data-stu-id="ec20d-163">Replace each space with a + character before pasting in hello query string before attempting hello query in Fiddler.</span></span>

<span data-ttu-id="ec20d-164">**До замены пробелов:**</span><span class="sxs-lookup"><span data-stu-id="ec20d-164">**Before spaces are replaced:**</span></span>

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2016-09-01

<span data-ttu-id="ec20d-165">**После замены пробелов символом +:**</span><span class="sxs-lookup"><span data-stu-id="ec20d-165">**After spaces are replaced with +:**</span></span>

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate+desc&api-version=2016-09-01

## <a name="query-hello-system"></a><span data-ttu-id="ec20d-166">Система hello запроса</span><span class="sxs-lookup"><span data-stu-id="ec20d-166">Query hello system</span></span>
<span data-ttu-id="ec20d-167">Можно также запросить hello системы tooget счетчики и хранения использование документов.</span><span class="sxs-lookup"><span data-stu-id="ec20d-167">You can also query hello system tooget document counts and storage consumption.</span></span> <span data-ttu-id="ec20d-168">На hello **Composer** , ваш запрос будет выглядеть примерно следующее toohello, а hello ответе возвращается число для hello число документов и используемого пространства.</span><span class="sxs-lookup"><span data-stu-id="ec20d-168">On hello **Composer** tab, your request will look similar toohello following, and hello response will return a count for hello number of documents and space used.</span></span>

 ![][5]

1. <span data-ttu-id="ec20d-169">Выберите **GET**.</span><span class="sxs-lookup"><span data-stu-id="ec20d-169">Select **GET**.</span></span>
2. <span data-ttu-id="ec20d-170">Введите URL, включающий URL-адрес вашей службы, а затем "/indexes/hotels/stats?api-version=2016-09-01":</span><span class="sxs-lookup"><span data-stu-id="ec20d-170">Enter a URL that includes your service URL, followed by "/indexes/hotels/stats?api-version=2016-09-01":</span></span>

         https://my-app.search.windows.net/indexes/hotels/stats?api-version=2016-09-01
3. <span data-ttu-id="ec20d-171">Укажите заголовок запроса hello, заменив значения, которые являются допустимыми для службы узла hello и ключ api.</span><span class="sxs-lookup"><span data-stu-id="ec20d-171">Specify hello request header, replacing hello host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. <span data-ttu-id="ec20d-172">Текст запроса hello оставьте пустым.</span><span class="sxs-lookup"><span data-stu-id="ec20d-172">Leave hello request body empty.</span></span>
5. <span data-ttu-id="ec20d-173">Нажмите **Execute (Выполнить)**.</span><span class="sxs-lookup"><span data-stu-id="ec20d-173">Click **Execute**.</span></span> <span data-ttu-id="ec20d-174">Вы увидите код состояния HTTP 200 в список сеансов hello.</span><span class="sxs-lookup"><span data-stu-id="ec20d-174">You should see an HTTP 200 status code in hello session list.</span></span> <span data-ttu-id="ec20d-175">Выберите запись hello учтена для вашей команды.</span><span class="sxs-lookup"><span data-stu-id="ec20d-175">Select hello entry posted for your command.</span></span>
6. <span data-ttu-id="ec20d-176">Нажмите кнопку hello **инспекторы** щелкните hello **заголовки** вкладку и hello, а затем выберите формат JSON.</span><span class="sxs-lookup"><span data-stu-id="ec20d-176">Click hello **Inspectors** tab, click hello **Headers** tab, and then select hello JSON format.</span></span> <span data-ttu-id="ec20d-177">Вы увидите hello документа число и размер для хранения (в КБ).</span><span class="sxs-lookup"><span data-stu-id="ec20d-177">You should see hello document count and storage size (in KB).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec20d-178">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ec20d-178">Next steps</span></span>
<span data-ttu-id="ec20d-179">В разделе [управление службой поиска в Azure](search-manage.md) toomanaging подход без кода и использования службы поиска Azure.</span><span class="sxs-lookup"><span data-stu-id="ec20d-179">See [Manage your Search service on Azure](search-manage.md) for a no-code approach toomanaging and using Azure Search.</span></span>

<!--Image References-->
[1]: ./media/search-fiddler/AzureSearch_Fiddler1_PutIndex.png
[2]: ./media/search-fiddler/AzureSearch_Fiddler2_PostDocs.png
[3]: ./media/search-fiddler/AzureSearch_Fiddler3_Query.png
[4]: ./media/search-fiddler/AzureSearch_Fiddler4_QueryResults.png
[5]: ./media/search-fiddler/AzureSearch_Fiddler5_QueryStats.png
