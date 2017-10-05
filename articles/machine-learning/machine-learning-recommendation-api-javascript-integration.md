---
title: "Рекомендации по машинному обучению: интеграция JavaScript | Документация Майкрософт"
description: "Рекомендации по машинному обучению Azure — интеграция JavaScript — документация"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: bbbb5bb6-489d-4a62-a2ae-f36237e9e2e1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: TRUE
ms.openlocfilehash: 8f27962d097bffc2a03de80244ae41d6573a4bf3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-machine-learning-recommendations---javascript-integration"></a><span data-ttu-id="249ed-103">Рекомендации по машинному обучению Azure — интеграция JavaScript</span><span class="sxs-lookup"><span data-stu-id="249ed-103">Azure Machine Learning Recommendations - JavaScript Integration</span></span>
> [!NOTE]
> <span data-ttu-id="249ed-104">Начните использовать когнитивную службу API рекомендаций вместо этой версии.</span><span class="sxs-lookup"><span data-stu-id="249ed-104">You should start using the Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="249ed-105">Когнитивная служба рекомендаций заменит эту службу, и все новые функции будут разрабатываться в ней.</span><span class="sxs-lookup"><span data-stu-id="249ed-105">The Recommendations Cognitive Service will be replacing this service, and all the new features will be developed there.</span></span> <span data-ttu-id="249ed-106">Она включает в себя новые возможности, такие как поддержка пакетной обработки, улучшенный обозреватель API, более четкое представление API, более согласованные процедуры регистрации и выставления счетов, и т. д.</span><span class="sxs-lookup"><span data-stu-id="249ed-106">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="249ed-107">Узнайте больше о [переходе на новую когнитивную службу](http://aka.ms/recomigrate).</span><span class="sxs-lookup"><span data-stu-id="249ed-107">Learn more about [Migrating to the new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="249ed-108">В этом документе описан процесс интеграции веб-сайта с использованием JavaScript.</span><span class="sxs-lookup"><span data-stu-id="249ed-108">This document depict how to integrate your site using JavaScript.</span></span> <span data-ttu-id="249ed-109">JavaScript позволяет отправлять события получения данных и использовать рекомендации после построения модели рекомендации.</span><span class="sxs-lookup"><span data-stu-id="249ed-109">The JavaScript enables you to send Data Acquisition events and to consume recommendations once you build a recommendation model.</span></span> <span data-ttu-id="249ed-110">Все операции, которые совершаются при помощи JS, можно выполнить непосредственно на сервере.</span><span class="sxs-lookup"><span data-stu-id="249ed-110">All operations done via JS can be also done from server side.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a><span data-ttu-id="249ed-111">1. Общая информация</span><span class="sxs-lookup"><span data-stu-id="249ed-111">1. General Overview</span></span>
<span data-ttu-id="249ed-112">Интеграция веб-сайта с рекомендациями Azure ML выполняется в 2 этапа.</span><span class="sxs-lookup"><span data-stu-id="249ed-112">Integrating your site with Azure ML Recommendations consist on 2 Phases:</span></span>

1. <span data-ttu-id="249ed-113">Отправка событий в рекомендации Azure ML.</span><span class="sxs-lookup"><span data-stu-id="249ed-113">Send Events into Azure ML Recommendations.</span></span> <span data-ttu-id="249ed-114">Это позволит построить модель рекомендации.</span><span class="sxs-lookup"><span data-stu-id="249ed-114">This will enable to build a recommendation model.</span></span>
2. <span data-ttu-id="249ed-115">Потребление созданных рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="249ed-115">Consume the recommendations.</span></span> <span data-ttu-id="249ed-116">После построения модели можно использовать созданные рекомендации.</span><span class="sxs-lookup"><span data-stu-id="249ed-116">After the model is built you can consume the recommendations.</span></span> <span data-ttu-id="249ed-117">(В этом документе не объясняется, как создавать модель; подробные сведения можно найти в кратком руководстве по началу работы.)</span><span class="sxs-lookup"><span data-stu-id="249ed-117">(This document does not explain how to build a model, read the quick start guide to get more information on how).</span></span>

<span data-ttu-id="249ed-118"><ins>Этап I</ins></span><span class="sxs-lookup"><span data-stu-id="249ed-118"><ins>Phase I</ins></span></span>

<span data-ttu-id="249ed-119">На первом этапе на ваши HTML-страницы устанавливается небольшая библиотека JavaScript, которая позволяет странице отправлять события по мере их возникновения на HTML-странице на серверы рекомендаций Azure ML (через Data Market):</span><span class="sxs-lookup"><span data-stu-id="249ed-119">In the first phase you insert into your html pages a small JavaScript library that enables the page to send events as they occur on the html page into Azure ML Recommendations servers (via Data Market):</span></span>

![Рисунок1][1]

<span data-ttu-id="249ed-121"><ins>Этап II</ins></span><span class="sxs-lookup"><span data-stu-id="249ed-121"><ins>Phase II</ins></span></span>

<span data-ttu-id="249ed-122">На втором этапе, когда потребуется отобразить рекомендации на выбранной странице, необходимо задать один из следующих параметров:</span><span class="sxs-lookup"><span data-stu-id="249ed-122">In the second phase when you want to show the recommendations on the page you select one of the following options:</span></span>

<span data-ttu-id="249ed-123">1. Ваш сервер (на этапе отрисовки страницы) обращается к серверу рекомендаций Azure ML (через Data Market), чтобы получить рекомендации.</span><span class="sxs-lookup"><span data-stu-id="249ed-123">1.Your server (on the phase of page rendering) calls Azure ML Recommendations Server (via Data Market) to get recommendations.</span></span> <span data-ttu-id="249ed-124">В результаты попадает список идентификаторов элементов.</span><span class="sxs-lookup"><span data-stu-id="249ed-124">The results include a list of items id.</span></span> <span data-ttu-id="249ed-125">Ваш сервер должен дополнить результаты метаданными элементов (например, изображениями, описанием) и отправить созданную страницу в браузер.</span><span class="sxs-lookup"><span data-stu-id="249ed-125">Your server needs to enrich the results with the items Meta data (e.g. images, description) and send the created page to the browser.</span></span>

![Рисунок2][2]

<span data-ttu-id="249ed-127">2. Другой вариант заключается в использовании небольшого файла JavaScript из первого этапа, чтобы получить простой список рекомендованных элементов.</span><span class="sxs-lookup"><span data-stu-id="249ed-127">2.The other option is to use the small JavaScript file from phase one to get a simple list of recommended items.</span></span> <span data-ttu-id="249ed-128">Данные, извлекаемые при помощи этого способа, более компактны, чем в первом случае.</span><span class="sxs-lookup"><span data-stu-id="249ed-128">The data received here is leaner than the one in the first option.</span></span>

![Рисунок3][3]

## <a name="2-prerequisites"></a><span data-ttu-id="249ed-130">2. Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="249ed-130">2. Prerequisites</span></span>
1. <span data-ttu-id="249ed-131">Создайте новую модель при помощи интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="249ed-131">Create a new model using the APIs.</span></span> <span data-ttu-id="249ed-132">Чтобы узнать, как это сделать, обратитесь к краткому руководству по началу работы.</span><span class="sxs-lookup"><span data-stu-id="249ed-132">See the Quick start guide on how to do it.</span></span>
2. <span data-ttu-id="249ed-133">Закодируйте &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt;, используя base64.</span><span class="sxs-lookup"><span data-stu-id="249ed-133">Encode your &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt; with base64.</span></span> <span data-ttu-id="249ed-134">(Это будет использоваться для обычной проверки подлинности в целях включения кода JS для вызова интерфейсов API.)</span><span class="sxs-lookup"><span data-stu-id="249ed-134">(This will be used for the basic authentication to enable the JS code to call the APIs).</span></span>

## <a name="3-send-data-acquisition-events-using-javascript"></a><span data-ttu-id="249ed-135">3. Отправка событий получения данных при помощи JavaScript</span><span class="sxs-lookup"><span data-stu-id="249ed-135">3. Send Data Acquisition events using JavaScript</span></span>
<span data-ttu-id="249ed-136">Следующие шаги обеспечивают отправку событий.</span><span class="sxs-lookup"><span data-stu-id="249ed-136">The following steps facilitate sending events:</span></span>

1. <span data-ttu-id="249ed-137">Включите в код библиотеку JQuery.</span><span class="sxs-lookup"><span data-stu-id="249ed-137">Include JQuery library in your code.</span></span> <span data-ttu-id="249ed-138">Ее можно загрузить в NuGet по следующему URL-адресу.</span><span class="sxs-lookup"><span data-stu-id="249ed-138">You can download it from nuget in the following URL.</span></span>
   
     <span data-ttu-id="249ed-139">http://www.nuget.org/packages/jQuery/1.8.2</span><span class="sxs-lookup"><span data-stu-id="249ed-139">http://www.nuget.org/packages/jQuery/1.8.2</span></span>
2. <span data-ttu-id="249ed-140">Включите библиотеку рекомендаций Java Script, получив ее по следующему URL-адресу: http://aka.ms/RecoJSLib1.</span><span class="sxs-lookup"><span data-stu-id="249ed-140">Include the Recommendations Java Script library from the following URL: http://aka.ms/RecoJSLib1</span></span>
3. <span data-ttu-id="249ed-141">Выполните инициализацию библиотеки рекомендаций Azure ML, используя необходимые параметры.</span><span class="sxs-lookup"><span data-stu-id="249ed-141">Initialize Azure ML Recommendations library with the appropriate parameters.</span></span>
   
     <span data-ttu-id="249ed-142"><script> AzureMLRecommendationsStart ("<base64encoding of username:key>", "<model_id>"); </script> 
4. Отправьте соответствующее событие.</span><span class="sxs-lookup"><span data-stu-id="249ed-142"><script> AzureMLRecommendationsStart("<base64encoding of username:key>", "<model_id>"); </script>
4. Send the appropriate event.</span></span> <span data-ttu-id="249ed-143">Раздел с подробными сведениями о всех типах событий см. ниже (пример события щелчка) <script> if (typeof AzureMLRecommendationsEvent=="undefined") {</span><span class="sxs-lookup"><span data-stu-id="249ed-143">See detailed section below on all type of events (example of click event)  <script> if (typeof AzureMLRecommendationsEvent=="undefined") {</span></span>         
                     <span data-ttu-id="249ed-144">AzureMLRecommendationsEvent = []; } AzureMLRecommendationsEvent.push({ event: "click", item: "18321116" }); </script></span><span class="sxs-lookup"><span data-stu-id="249ed-144">AzureMLRecommendationsEvent = []; } AzureMLRecommendationsEvent.push({ event: "click", item: "18321116" }); </script></span></span>

### <a name="31----limitations-and-browser-support"></a><span data-ttu-id="249ed-145">3.1.</span><span class="sxs-lookup"><span data-stu-id="249ed-145">3.1.</span></span>    <span data-ttu-id="249ed-146">Ограничения и поддержка браузеров</span><span class="sxs-lookup"><span data-stu-id="249ed-146">Limitations and Browser Support</span></span>
<span data-ttu-id="249ed-147">Данная реализация является справочной и представлена как есть.</span><span class="sxs-lookup"><span data-stu-id="249ed-147">This is a reference implementation and it is given as is.</span></span> <span data-ttu-id="249ed-148">Она должна поддерживаться во всех основных браузерах.</span><span class="sxs-lookup"><span data-stu-id="249ed-148">It should support all major browsers.</span></span>

### <a name="32----type-of-events"></a><span data-ttu-id="249ed-149">3.2.</span><span class="sxs-lookup"><span data-stu-id="249ed-149">3.2.</span></span>    <span data-ttu-id="249ed-150">Тип событий</span><span class="sxs-lookup"><span data-stu-id="249ed-150">Type of Events</span></span>
<span data-ttu-id="249ed-151">Существуют 5 типов событий, которые поддерживаются библиотекой: щелчок мышью, щелчок рекомендации, добавление в корзину, удаление из корзины и приобретение.</span><span class="sxs-lookup"><span data-stu-id="249ed-151">There are 5 types of event that the library supports: Click, Recommendation Click, Add to Shop Cart, Remove from Shop Cart and Purchase.</span></span> <span data-ttu-id="249ed-152">Имеется дополнительное событие, которое используется для установки контекста пользователя под именем "Имя входа".</span><span class="sxs-lookup"><span data-stu-id="249ed-152">There is an additional event that is used to set the user context called Login.</span></span>

#### <a name="321-click-event"></a><span data-ttu-id="249ed-153">3.2.1.</span><span class="sxs-lookup"><span data-stu-id="249ed-153">3.2.1.</span></span> <span data-ttu-id="249ed-154">Событие "Щелчок"</span><span class="sxs-lookup"><span data-stu-id="249ed-154">Click Event</span></span>
<span data-ttu-id="249ed-155">Это событие должно использоваться всякий раз, когда пользователь щелкает элемент.</span><span class="sxs-lookup"><span data-stu-id="249ed-155">This event should be used any time a user clicked on an item.</span></span> <span data-ttu-id="249ed-156">Обычно, когда пользователь щелкает какой-нибудь элемент, открывается новая страница с подробными сведениями о нем; на этой странице и требуется запускать событие.</span><span class="sxs-lookup"><span data-stu-id="249ed-156">Usually when user clicks on an item a new page is opened with the item details; in this page this event should be triggered.</span></span>

<span data-ttu-id="249ed-157">Параметры</span><span class="sxs-lookup"><span data-stu-id="249ed-157">Parameters:</span></span>

* <span data-ttu-id="249ed-158">event (строка, обязательный) — click.</span><span class="sxs-lookup"><span data-stu-id="249ed-158">event (string, mandatory) - “click”</span></span>
* <span data-ttu-id="249ed-159">item (строка, обязательный) — уникальный идентификатор элемента.</span><span class="sxs-lookup"><span data-stu-id="249ed-159">item (string, mandatory) - Unique identifier of the item</span></span>
* <span data-ttu-id="249ed-160">itemName (строка, необязательный) — имя элемента.</span><span class="sxs-lookup"><span data-stu-id="249ed-160">itemName (string, optional) - the name of the item</span></span>
* <span data-ttu-id="249ed-161">itemDescription (строка, необязательный) — описание элемента.</span><span class="sxs-lookup"><span data-stu-id="249ed-161">itemDescription (string, optional) - the description of the item</span></span>
* <span data-ttu-id="249ed-162">itemCategory (строка, необязательный) — категория элемента.</span><span class="sxs-lookup"><span data-stu-id="249ed-162">itemCategory (string, optional) - the category of the item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "click", item: "3111718" });
        </script>

<span data-ttu-id="249ed-163">Или с дополнительными данными:</span><span class="sxs-lookup"><span data-stu-id="249ed-163">Or with optional data:</span></span>

        <script>
            if (typeof AzureMLRecommendationsEvent === "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "click", item: "3111718", itemName: "Plane", itemDescription: "It is a big plane", itemCategory: "Aviation"});
        </script>


#### <a name="322-recommendation-click-event"></a><span data-ttu-id="249ed-164">3.2.2.</span><span class="sxs-lookup"><span data-stu-id="249ed-164">3.2.2.</span></span> <span data-ttu-id="249ed-165">Событие "щелчок рекомендации"</span><span class="sxs-lookup"><span data-stu-id="249ed-165">Recommendation Click Event</span></span>
<span data-ttu-id="249ed-166">Это событие должно использоваться всякий раз, когда пользователь щелкает элемент, который был получен из рекомендаций Azure ML в качестве рекомендованного элемента.</span><span class="sxs-lookup"><span data-stu-id="249ed-166">This event should be used any time a user clicked on an item that was received from Azure ML Recommendations as a recommended item.</span></span> <span data-ttu-id="249ed-167">Обычно, когда пользователь щелкает какой-нибудь элемент, открывается новая страница с подробными сведениями о нем; на этой странице и требуется запускать событие.</span><span class="sxs-lookup"><span data-stu-id="249ed-167">Usually when user clicks on an item a new page is opened with the item details; in this page this event should be triggered.</span></span>

<span data-ttu-id="249ed-168">Параметры</span><span class="sxs-lookup"><span data-stu-id="249ed-168">Parameters:</span></span>

* <span data-ttu-id="249ed-169">event (строка, обязательный) — recommendationclick.</span><span class="sxs-lookup"><span data-stu-id="249ed-169">event (string, mandatory) - “recommendationclick”</span></span>
* <span data-ttu-id="249ed-170">item (строка, обязательный) — уникальный идентификатор элемента.</span><span class="sxs-lookup"><span data-stu-id="249ed-170">item (string, mandatory) - Unique identifier of the item</span></span>
* <span data-ttu-id="249ed-171">itemName (строка, необязательный) — имя элемента.</span><span class="sxs-lookup"><span data-stu-id="249ed-171">itemName (string, optional) - the name of the item</span></span>
* <span data-ttu-id="249ed-172">itemDescription (строка, необязательный) — описание элемента.</span><span class="sxs-lookup"><span data-stu-id="249ed-172">itemDescription (string, optional) - the description of the item</span></span>
* <span data-ttu-id="249ed-173">itemCategory (строка, необязательный) — категория элемента.</span><span class="sxs-lookup"><span data-stu-id="249ed-173">itemCategory (string, optional) - the category of the item</span></span>
* <span data-ttu-id="249ed-174">seeds (массив строк, необязательный) — начальные значения, создавшие запрос рекомендации.</span><span class="sxs-lookup"><span data-stu-id="249ed-174">seeds (string array, optional) - the seeds that generated the recommendation query.</span></span>
* <span data-ttu-id="249ed-175">recoList (массив строк, необязательный) — результат запроса рекомендации, создавшего активированный элемент.</span><span class="sxs-lookup"><span data-stu-id="249ed-175">recoList (string array, optional) - the result of the recommendation request that generated the item that was clicked.</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "recommendationclick", item: "18899918" });
        </script>

<span data-ttu-id="249ed-176">Или с дополнительными данными:</span><span class="sxs-lookup"><span data-stu-id="249ed-176">Or with optional data:</span></span>

        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: eventName, item: "198", itemName: "Plane2", itemDescription: "It is a big plane2", itemCategory: "Default2", seeds: ["Seed1", "Seed2"], recoList: ["199", "198", "197"]                 });
        </script>


#### <a name="323-add-shopping-cart-event"></a><span data-ttu-id="249ed-177">3.2.3.</span><span class="sxs-lookup"><span data-stu-id="249ed-177">3.2.3.</span></span> <span data-ttu-id="249ed-178">Событие добавления товара в корзину</span><span class="sxs-lookup"><span data-stu-id="249ed-178">Add Shopping Cart Event</span></span>
<span data-ttu-id="249ed-179">Это событие должно использоваться всякий раз, когда пользователь добавляет элемент в корзину.</span><span class="sxs-lookup"><span data-stu-id="249ed-179">This event should be used when the user add an item to the shopping cart.</span></span>
<span data-ttu-id="249ed-180">Параметры</span><span class="sxs-lookup"><span data-stu-id="249ed-180">Parameters:</span></span>

* <span data-ttu-id="249ed-181">event (строка, обязательный) — addshopcart.</span><span class="sxs-lookup"><span data-stu-id="249ed-181">event (string, mandatory) - “addshopcart”</span></span>
* <span data-ttu-id="249ed-182">item (строка, обязательный) — уникальный идентификатор элемента.</span><span class="sxs-lookup"><span data-stu-id="249ed-182">item (string, mandatory) - Unique identifier of the item</span></span>
* <span data-ttu-id="249ed-183">itemName (строка, необязательный) — имя элемента.</span><span class="sxs-lookup"><span data-stu-id="249ed-183">itemName (string, optional) - the name of the item</span></span>
* <span data-ttu-id="249ed-184">itemDescription (строка, необязательный) — описание элемента.</span><span class="sxs-lookup"><span data-stu-id="249ed-184">itemDescription (string, optional) - the description of the item</span></span>
* <span data-ttu-id="249ed-185">itemCategory (строка, необязательный) — категория элемента.</span><span class="sxs-lookup"><span data-stu-id="249ed-185">itemCategory (string, optional) - the category of the item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "addshopcart", item: "13221118" });
        </script>

#### <a name="324-remove-shopping-cart-event"></a><span data-ttu-id="249ed-186">3.2.4.</span><span class="sxs-lookup"><span data-stu-id="249ed-186">3.2.4.</span></span> <span data-ttu-id="249ed-187">Событие удаления товара из корзины</span><span class="sxs-lookup"><span data-stu-id="249ed-187">Remove Shopping Cart Event</span></span>
<span data-ttu-id="249ed-188">Это событие должно использоваться всякий раз, когда пользователь удаляет элемент из корзины.</span><span class="sxs-lookup"><span data-stu-id="249ed-188">This event should be used when the user removes an item to the shopping cart.</span></span>

<span data-ttu-id="249ed-189">Параметры</span><span class="sxs-lookup"><span data-stu-id="249ed-189">Parameters:</span></span>

* <span data-ttu-id="249ed-190">event (строка, обязательный) — removeshopcart.</span><span class="sxs-lookup"><span data-stu-id="249ed-190">event (string, mandatory) - “removeshopcart”</span></span>
* <span data-ttu-id="249ed-191">item (строка, обязательный) — уникальный идентификатор элемента.</span><span class="sxs-lookup"><span data-stu-id="249ed-191">item (string, mandatory) - Unique identifier of the item</span></span>
* <span data-ttu-id="249ed-192">itemName (строка, необязательный) — имя элемента.</span><span class="sxs-lookup"><span data-stu-id="249ed-192">itemName (string, optional) - the name of the item</span></span>
* <span data-ttu-id="249ed-193">itemDescription (строка, необязательный) — описание элемента.</span><span class="sxs-lookup"><span data-stu-id="249ed-193">itemDescription (string, optional) - the description of the item</span></span>
* <span data-ttu-id="249ed-194">itemCategory (строка, необязательный) — категория элемента.</span><span class="sxs-lookup"><span data-stu-id="249ed-194">itemCategory (string, optional) - the category of the item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "removeshopcart", item: "111118" });
        </script>

#### <a name="325-purchase-event"></a><span data-ttu-id="249ed-195">3.2.5.</span><span class="sxs-lookup"><span data-stu-id="249ed-195">3.2.5.</span></span> <span data-ttu-id="249ed-196">Событие покупки</span><span class="sxs-lookup"><span data-stu-id="249ed-196">Purchase Event</span></span>
<span data-ttu-id="249ed-197">Это событие должно использоваться всякий раз, когда пользователь выкупает свою корзину.</span><span class="sxs-lookup"><span data-stu-id="249ed-197">This event should be used when the user purchased his shopping cart.</span></span>

<span data-ttu-id="249ed-198">Параметры</span><span class="sxs-lookup"><span data-stu-id="249ed-198">Parameters:</span></span>

* <span data-ttu-id="249ed-199">event (строка) — purchase.</span><span class="sxs-lookup"><span data-stu-id="249ed-199">event (string) - “purchase”</span></span>
* <span data-ttu-id="249ed-200">items ( Purchased[] ) — массив, содержащий запись для каждого приобретенного элемента.</span><span class="sxs-lookup"><span data-stu-id="249ed-200">items ( Purchased[] ) - Array holding an entry for each item purchased.</span></span><br><br>
  <span data-ttu-id="249ed-201">Формат приобретенных элементов</span><span class="sxs-lookup"><span data-stu-id="249ed-201">Purchased format:</span></span>
  * <span data-ttu-id="249ed-202">item (строка) — уникальный идентификатор элемента.</span><span class="sxs-lookup"><span data-stu-id="249ed-202">item (string) - Unique identifier of the item.</span></span>
  * <span data-ttu-id="249ed-203">count (целое число или строка) — количество приобретенных элементов.</span><span class="sxs-lookup"><span data-stu-id="249ed-203">count (int or string) - number of items that were purchased.</span></span>
  * <span data-ttu-id="249ed-204">price (число с плавающей запятой или строка) (дополнительное поле) — цена элемента.</span><span class="sxs-lookup"><span data-stu-id="249ed-204">price (float or string) - optional field - the price of the item.</span></span>

<span data-ttu-id="249ed-205">В примере ниже показано приобретение 3 элементов (33, 34, 35), два со всеми заполненными полями (элемент, количество, цена) и одним (элемент 34) без цены.</span><span class="sxs-lookup"><span data-stu-id="249ed-205">The example below shows purchase of 3 items (33, 34, 35), two with all fields populated (item, count, price) and one (item 34) without a price.</span></span>

        <script>
            if ( typeof AzureMLRecommendationsEvent == "undefined"){ AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "purchase", items: [{ item: "33", count: "1", price: "10" }, { item: "34", count: "2" }, { item: "35", count: "1", price: "210" }] });
        </script>

#### <a name="326-user-login-event"></a><span data-ttu-id="249ed-206">3.2.6.</span><span class="sxs-lookup"><span data-stu-id="249ed-206">3.2.6.</span></span> <span data-ttu-id="249ed-207">Событие входа пользователя</span><span class="sxs-lookup"><span data-stu-id="249ed-207">User Login Event</span></span>
<span data-ttu-id="249ed-208">Библиотека рекомендаций Azure ML создает и использует файл cookie, чтобы определить события, полученные от аналогичного браузера.</span><span class="sxs-lookup"><span data-stu-id="249ed-208">Azure ML Recommendations Event library creates and use a cookie in order to identify events that came from the same browser.</span></span> <span data-ttu-id="249ed-209">Чтобы улучшить результаты модели, рекомендации Azure ML позволяют пользователю установить уникальный идентификатор, который переопределит используемые файлы cookie.</span><span class="sxs-lookup"><span data-stu-id="249ed-209">In order to improve the model results Azure ML Recommendations enables to set a user unique identification that will override the cookie usage.</span></span>

<span data-ttu-id="249ed-210">Это событие должно использоваться после входа пользователя на ваш веб-сайт.</span><span class="sxs-lookup"><span data-stu-id="249ed-210">This event should be used after the user login to your site.</span></span>

<span data-ttu-id="249ed-211">Параметры</span><span class="sxs-lookup"><span data-stu-id="249ed-211">Parameters:</span></span>

* <span data-ttu-id="249ed-212">event (строка) — userlogin.</span><span class="sxs-lookup"><span data-stu-id="249ed-212">event (string) - “userlogin”</span></span>
* <span data-ttu-id="249ed-213">user (строка) — уникальный идентификатор пользователя.</span><span class="sxs-lookup"><span data-stu-id="249ed-213">user (string) - unique identification of the user.</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "userlogin", user: “ABCD10AA” });
        </script>

## <a name="4-consume-recommendations-via-javascript"></a><span data-ttu-id="249ed-214">4. Использование рекомендаций с помощью JavaScript</span><span class="sxs-lookup"><span data-stu-id="249ed-214">4. Consume Recommendations via JavaScript</span></span>
<span data-ttu-id="249ed-215">Код, использующий рекомендацию, запускается через то же событие JavaScript на веб-странице клиента.</span><span class="sxs-lookup"><span data-stu-id="249ed-215">The code that consumes the recommendation is triggered by some JavaScript event by the client’s webpage.</span></span> <span data-ttu-id="249ed-216">Ответ на рекомендацию включает идентификаторы рекомендуемых элементов, их имена и рейтинги.</span><span class="sxs-lookup"><span data-stu-id="249ed-216">The recommendation response includes the recommended items Ids, their names and their ratings.</span></span> <span data-ttu-id="249ed-217">Рекомендуется использовать этот параметр только для отображения списка рекомендуемых элементов. Более сложная обработка (например, добавление метаданных элемента) должна выполняться при интеграции на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="249ed-217">It’s best to use this option only for a list display of the recommended items - more complex handling (such as adding the item’s metadata) should be done on the server side integration.</span></span>

### <a name="41-consume-recommendations"></a><span data-ttu-id="249ed-218">4.1. Потребление рекомендаций</span><span class="sxs-lookup"><span data-stu-id="249ed-218">4.1 Consume Recommendations</span></span>
<span data-ttu-id="249ed-219">Чтобы использовать рекомендации, потребуется включить необходимые библиотеки JavaScript в вашу страницу и вызвать метод AzureMLRecommendationsStart.</span><span class="sxs-lookup"><span data-stu-id="249ed-219">To consume recommendations you need to include the required JavaScript libraries in your page and to call AzureMLRecommendationsStart.</span></span> <span data-ttu-id="249ed-220">См. раздел 2.</span><span class="sxs-lookup"><span data-stu-id="249ed-220">See section 2.</span></span>

<span data-ttu-id="249ed-221">Чтобы использовать рекомендации для одного или нескольких элементов, потребуется вызвать метод AzureMLRecommendationsGetI2IRecommendation.</span><span class="sxs-lookup"><span data-stu-id="249ed-221">To consume recommendations for one or more items you need to call a method called: AzureMLRecommendationsGetI2IRecommendation.</span></span>

<span data-ttu-id="249ed-222">Параметры</span><span class="sxs-lookup"><span data-stu-id="249ed-222">Parameters:</span></span>

* <span data-ttu-id="249ed-223">items (массив строк) — один или несколько элементов, по которым будут получены рекомендации.</span><span class="sxs-lookup"><span data-stu-id="249ed-223">items (array of strings) - One or more items to get recommendations for.</span></span> <span data-ttu-id="249ed-224">При использовании сборки Fbt здесь можно задать только один элемент.</span><span class="sxs-lookup"><span data-stu-id="249ed-224">If you consume an Fbt build then you can set here only one item.</span></span>
* <span data-ttu-id="249ed-225">numberOfResults (целое число) — количество необходимых результатов.</span><span class="sxs-lookup"><span data-stu-id="249ed-225">numberOfResults (int) - number of required results.</span></span>
* <span data-ttu-id="249ed-226">includeMetadata (логический, необязательный) — если задано значение true, указывает, что поле метаданных должно заполняться в результате.</span><span class="sxs-lookup"><span data-stu-id="249ed-226">includeMetadata (boolean, optional) - if set to ‘true’ indicates that the metadata field must be populated in the result.</span></span>
* <span data-ttu-id="249ed-227">Функция обработки — функция, которая будет обрабатывать возвращенные рекомендации.</span><span class="sxs-lookup"><span data-stu-id="249ed-227">Processing function - a function that will handle the recommendations returned.</span></span> <span data-ttu-id="249ed-228">Данные возвращаются как массив следующих объектов:</span><span class="sxs-lookup"><span data-stu-id="249ed-228">The data is returned as an array of:</span></span>
  * <span data-ttu-id="249ed-229">item — уникальный идентификатор элемента.</span><span class="sxs-lookup"><span data-stu-id="249ed-229">Item - item unique id</span></span>
  * <span data-ttu-id="249ed-230">name — имя элемента (если существует в каталоге).</span><span class="sxs-lookup"><span data-stu-id="249ed-230">name - item name (if exist in catalog)</span></span>
  * <span data-ttu-id="249ed-231">rating — рейтинг рекомендации.</span><span class="sxs-lookup"><span data-stu-id="249ed-231">rating - recommendation rating</span></span>
  * <span data-ttu-id="249ed-232">metadata — строка, представляющая метаданные элемента.</span><span class="sxs-lookup"><span data-stu-id="249ed-232">metadata - a string that represents the metadata of the item</span></span>

<span data-ttu-id="249ed-233">Например, в следующем коде выполняется запрос 8 рекомендаций для элемента 64f6eb0d-947a-4c18-a16c-888da9e228ba (при этом значение параметра includeMetadata не указано, а это означает, что возврат метаданных не требуется), после чего результаты помещаются в буфер.</span><span class="sxs-lookup"><span data-stu-id="249ed-233">Example: The following code requests 8 recommendations for item "64f6eb0d-947a-4c18-a16c-888da9e228ba" (and by not specifying includeMetadata - it implicitly says that no metadata is required), it then concatenate the results into a buffer.</span></span>

        <script>
             var reco = AzureMLRecommendationsGetI2IRecommendation(["64f6eb0d-947a-4c18-a16c-888da9e228ba"], 8, false, function (reco) {
                 var buff = "";
                 for (var ii = 0; ii < reco.length; ii++) {
                       buff += reco[ii].item + "," + reco[ii].name + "," + reco[ii].rating + "\n";
                 }
                 alert(buff);
            });
        </script>


[1]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing1.png
[2]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing2.png
[3]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing3.png
