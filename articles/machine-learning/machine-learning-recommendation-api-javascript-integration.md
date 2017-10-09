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
redirect_document_id: True
ms.openlocfilehash: 4c5f0eee4aa04ce823321d52985374c52850f0d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-recommendations---javascript-integration"></a><span data-ttu-id="d5838-103">Рекомендации по машинному обучению Azure — интеграция JavaScript</span><span class="sxs-lookup"><span data-stu-id="d5838-103">Azure Machine Learning Recommendations - JavaScript Integration</span></span>
> [!NOTE]
> <span data-ttu-id="d5838-104">Необходимо запустить с помощью службы Когнитивных рекомендации API hello вместо этой версии.</span><span class="sxs-lookup"><span data-stu-id="d5838-104">You should start using hello Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="d5838-105">Эта служба будет заменена Hello службы Когнитивных рекомендации и всех hello новых функций, которые будут реализованы существует.</span><span class="sxs-lookup"><span data-stu-id="d5838-105">hello Recommendations Cognitive Service will be replacing this service, and all hello new features will be developed there.</span></span> <span data-ttu-id="d5838-106">Она включает в себя новые возможности, такие как поддержка пакетной обработки, улучшенный обозреватель API, более четкое представление API, более согласованные процедуры регистрации и выставления счетов, и т. д.</span><span class="sxs-lookup"><span data-stu-id="d5838-106">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="d5838-107">Дополнительные сведения о [toohello перенос новой Когнитивных службы](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="d5838-107">Learn more about [Migrating toohello new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="d5838-108">В этом документе отображения как toointegrate сайта с использованием JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d5838-108">This document depict how toointegrate your site using JavaScript.</span></span> <span data-ttu-id="d5838-109">Hello JavaScript позволяет toosend получение данных события и рекомендации tooconsume после построения модели рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="d5838-109">hello JavaScript enables you toosend Data Acquisition events and tooconsume recommendations once you build a recommendation model.</span></span> <span data-ttu-id="d5838-110">Все операции, которые совершаются при помощи JS, можно выполнить непосредственно на сервере.</span><span class="sxs-lookup"><span data-stu-id="d5838-110">All operations done via JS can be also done from server side.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a><span data-ttu-id="d5838-111">1. Общая информация</span><span class="sxs-lookup"><span data-stu-id="d5838-111">1. General Overview</span></span>
<span data-ttu-id="d5838-112">Интеграция веб-сайта с рекомендациями Azure ML выполняется в 2 этапа.</span><span class="sxs-lookup"><span data-stu-id="d5838-112">Integrating your site with Azure ML Recommendations consist on 2 Phases:</span></span>

1. <span data-ttu-id="d5838-113">Отправка событий в рекомендации Azure ML.</span><span class="sxs-lookup"><span data-stu-id="d5838-113">Send Events into Azure ML Recommendations.</span></span> <span data-ttu-id="d5838-114">Это позволит toobuild модели рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="d5838-114">This will enable toobuild a recommendation model.</span></span>
2. <span data-ttu-id="d5838-115">Использование рекомендаций hello.</span><span class="sxs-lookup"><span data-stu-id="d5838-115">Consume hello recommendations.</span></span> <span data-ttu-id="d5838-116">После построения модели hello могут потреблять hello рекомендации.</span><span class="sxs-lookup"><span data-stu-id="d5838-116">After hello model is built you can consume hello recommendations.</span></span> <span data-ttu-id="d5838-117">(В этом документе не объясняют, как прочитать toobuild модели, hello краткое руководство по tooget Дополнительные сведения о том, как).</span><span class="sxs-lookup"><span data-stu-id="d5838-117">(This document does not explain how toobuild a model, read hello quick start guide tooget more information on how).</span></span>

<span data-ttu-id="d5838-118"><ins>Этап I</ins></span><span class="sxs-lookup"><span data-stu-id="d5838-118"><ins>Phase I</ins></span></span>

<span data-ttu-id="d5838-119">В hello первого этапа, можно вставить в HTML-страницы небольшой библиотека JavaScript, которая позволяет hello страницы toosend события, происходящие на HTML-странице hello в Azure ML рекомендации серверов (с помощью Data Market):</span><span class="sxs-lookup"><span data-stu-id="d5838-119">In hello first phase you insert into your html pages a small JavaScript library that enables hello page toosend events as they occur on hello html page into Azure ML Recommendations servers (via Data Market):</span></span>

![Рисунок1][1]

<span data-ttu-id="d5838-121"><ins>Этап II</ins></span><span class="sxs-lookup"><span data-stu-id="d5838-121"><ins>Phase II</ins></span></span>

<span data-ttu-id="d5838-122">В hello второй этап, когда требуется tooshow hello рекомендации на странице приветствия выбирается один из следующих вариантов hello:</span><span class="sxs-lookup"><span data-stu-id="d5838-122">In hello second phase when you want tooshow hello recommendations on hello page you select one of hello following options:</span></span>

<span data-ttu-id="d5838-123">1. сервер (этап hello визуализации страницы) вызывает рекомендации tooget сервера рекомендации машинного Обучения Azure (с помощью Data Market).</span><span class="sxs-lookup"><span data-stu-id="d5838-123">1.Your server (on hello phase of page rendering) calls Azure ML Recommendations Server (via Data Market) tooget recommendations.</span></span> <span data-ttu-id="d5838-124">Hello результатов включать список идентификаторов элементов. Сервер должен tooenrich hello результаты с элементами hello метаданных (например, изображения, описание) и отправить создан браузера toohello страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="d5838-124">hello results include a list of items id. Your server needs tooenrich hello results with hello items Meta data (e.g. images, description) and send hello created page toohello browser.</span></span>

![Рисунок2][2]

<span data-ttu-id="d5838-126">2. hello другой вариант — toouse hello небольшой JavaScript файл из одного tooget этап простой список рекомендуемых элементов.</span><span class="sxs-lookup"><span data-stu-id="d5838-126">2.hello other option is toouse hello small JavaScript file from phase one tooget a simple list of recommended items.</span></span> <span data-ttu-id="d5838-127">Здесь полученные данные Hello экономичные, чем один hello в первом варианте hello.</span><span class="sxs-lookup"><span data-stu-id="d5838-127">hello data received here is leaner than hello one in hello first option.</span></span>

![Рисунок3][3]

## <a name="2-prerequisites"></a><span data-ttu-id="d5838-129">2. Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d5838-129">2. Prerequisites</span></span>
1. <span data-ttu-id="d5838-130">Создайте новую модель с помощью API-интерфейсы hello.</span><span class="sxs-lookup"><span data-stu-id="d5838-130">Create a new model using hello APIs.</span></span> <span data-ttu-id="d5838-131">В разделе hello краткое руководство о том, как toodo его.</span><span class="sxs-lookup"><span data-stu-id="d5838-131">See hello Quick start guide on how toodo it.</span></span>
2. <span data-ttu-id="d5838-132">Закодируйте &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt;, используя base64.</span><span class="sxs-lookup"><span data-stu-id="d5838-132">Encode your &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt; with base64.</span></span> <span data-ttu-id="d5838-133">(Это будет использоваться для hello обычной проверки подлинности tooenable hello JS кода hello toocall API-интерфейсы).</span><span class="sxs-lookup"><span data-stu-id="d5838-133">(This will be used for hello basic authentication tooenable hello JS code toocall hello APIs).</span></span>

## <a name="3-send-data-acquisition-events-using-javascript"></a><span data-ttu-id="d5838-134">3. Отправка событий получения данных при помощи JavaScript</span><span class="sxs-lookup"><span data-stu-id="d5838-134">3. Send Data Acquisition events using JavaScript</span></span>
<span data-ttu-id="d5838-135">следующие шаги Hello упрощения отправлять события:</span><span class="sxs-lookup"><span data-stu-id="d5838-135">hello following steps facilitate sending events:</span></span>

1. <span data-ttu-id="d5838-136">Включите в код библиотеку JQuery.</span><span class="sxs-lookup"><span data-stu-id="d5838-136">Include JQuery library in your code.</span></span> <span data-ttu-id="d5838-137">Его можно загрузить из nuget в hello URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="d5838-137">You can download it from nuget in hello following URL.</span></span>
   
     <span data-ttu-id="d5838-138">http://www.nuget.org/packages/jQuery/1.8.2</span><span class="sxs-lookup"><span data-stu-id="d5838-138">http://www.nuget.org/packages/jQuery/1.8.2</span></span>
2. <span data-ttu-id="d5838-139">Включена библиотека hello скрипт рекомендаций Java из hello URL-адреса: http://aka.ms/RecoJSLib1</span><span class="sxs-lookup"><span data-stu-id="d5838-139">Include hello Recommendations Java Script library from hello following URL: http://aka.ms/RecoJSLib1</span></span>
3. <span data-ttu-id="d5838-140">Инициализируйте библиотеку Azure ML рекомендаций с соответствующими параметрами hello.</span><span class="sxs-lookup"><span data-stu-id="d5838-140">Initialize Azure ML Recommendations library with hello appropriate parameters.</span></span>
   
     <span data-ttu-id="d5838-141"><script>AzureMLRecommendationsStart («<base64encoding of username:key>», «< model_id >"); </script> 
4. Отправки hello соответствующее событие.</span><span class="sxs-lookup"><span data-stu-id="d5838-141"><script> AzureMLRecommendationsStart("<base64encoding of username:key>", "<model_id>"); </script>
4. Send hello appropriate event.</span></span> <span data-ttu-id="d5838-142">Раздел с подробными сведениями о всех типах событий см. ниже (пример события щелчка) <script> if (typeof AzureMLRecommendationsEvent=="undefined") {</span><span class="sxs-lookup"><span data-stu-id="d5838-142">See detailed section below on all type of events (example of click event)  <script> if (typeof AzureMLRecommendationsEvent=="undefined") {</span></span>         
                     <span data-ttu-id="d5838-143">AzureMLRecommendationsEvent = []; } AzureMLRecommendationsEvent.push({ event: "click", item: "18321116" }); </script></span><span class="sxs-lookup"><span data-stu-id="d5838-143">AzureMLRecommendationsEvent = []; } AzureMLRecommendationsEvent.push({ event: "click", item: "18321116" }); </script></span></span>

### <a name="31----limitations-and-browser-support"></a><span data-ttu-id="d5838-144">3.1.</span><span class="sxs-lookup"><span data-stu-id="d5838-144">3.1.</span></span>    <span data-ttu-id="d5838-145">Ограничения и поддержка браузеров</span><span class="sxs-lookup"><span data-stu-id="d5838-145">Limitations and Browser Support</span></span>
<span data-ttu-id="d5838-146">Данная реализация является справочной и представлена как есть.</span><span class="sxs-lookup"><span data-stu-id="d5838-146">This is a reference implementation and it is given as is.</span></span> <span data-ttu-id="d5838-147">Она должна поддерживаться во всех основных браузерах.</span><span class="sxs-lookup"><span data-stu-id="d5838-147">It should support all major browsers.</span></span>

### <a name="32----type-of-events"></a><span data-ttu-id="d5838-148">3.2.</span><span class="sxs-lookup"><span data-stu-id="d5838-148">3.2.</span></span>    <span data-ttu-id="d5838-149">Тип событий</span><span class="sxs-lookup"><span data-stu-id="d5838-149">Type of Events</span></span>
<span data-ttu-id="d5838-150">Существует 5 типов событий, которые поддерживает библиотеку hello: нажмите кнопку, щелкните рекомендацию, добавьте tooShop покупок, удалите из бюро покупок и покупки.</span><span class="sxs-lookup"><span data-stu-id="d5838-150">There are 5 types of event that hello library supports: Click, Recommendation Click, Add tooShop Cart, Remove from Shop Cart and Purchase.</span></span> <span data-ttu-id="d5838-151">Нет дополнительных событие, которое используется tooset hello пользовательский контекст входа.</span><span class="sxs-lookup"><span data-stu-id="d5838-151">There is an additional event that is used tooset hello user context called Login.</span></span>

#### <a name="321-click-event"></a><span data-ttu-id="d5838-152">3.2.1.</span><span class="sxs-lookup"><span data-stu-id="d5838-152">3.2.1.</span></span> <span data-ttu-id="d5838-153">Событие "Щелчок"</span><span class="sxs-lookup"><span data-stu-id="d5838-153">Click Event</span></span>
<span data-ttu-id="d5838-154">Это событие должно использоваться всякий раз, когда пользователь щелкает элемент.</span><span class="sxs-lookup"><span data-stu-id="d5838-154">This event should be used any time a user clicked on an item.</span></span> <span data-ttu-id="d5838-155">Обычно в том случае, когда пользователь щелкает элемент открывается новая страница с hello сведения об элементе; на этой странице должна активироваться это событие.</span><span class="sxs-lookup"><span data-stu-id="d5838-155">Usually when user clicks on an item a new page is opened with hello item details; in this page this event should be triggered.</span></span>

<span data-ttu-id="d5838-156">Параметры</span><span class="sxs-lookup"><span data-stu-id="d5838-156">Parameters:</span></span>

* <span data-ttu-id="d5838-157">event (строка, обязательный) — click.</span><span class="sxs-lookup"><span data-stu-id="d5838-157">event (string, mandatory) - “click”</span></span>
* <span data-ttu-id="d5838-158">элемент (string, обязательные) — уникальный идентификатор элемента hello</span><span class="sxs-lookup"><span data-stu-id="d5838-158">item (string, mandatory) - Unique identifier of hello item</span></span>
* <span data-ttu-id="d5838-159">itemName (string, необязательно) — имя hello элемента hello</span><span class="sxs-lookup"><span data-stu-id="d5838-159">itemName (string, optional) - hello name of hello item</span></span>
* <span data-ttu-id="d5838-160">itemDescription (string, необязательно) — описание hello элемента hello</span><span class="sxs-lookup"><span data-stu-id="d5838-160">itemDescription (string, optional) - hello description of hello item</span></span>
* <span data-ttu-id="d5838-161">itemCategory (string, необязательно) — hello категорию элемента hello</span><span class="sxs-lookup"><span data-stu-id="d5838-161">itemCategory (string, optional) - hello category of hello item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "click", item: "3111718" });
        </script>

<span data-ttu-id="d5838-162">Или с дополнительными данными:</span><span class="sxs-lookup"><span data-stu-id="d5838-162">Or with optional data:</span></span>

        <script>
            if (typeof AzureMLRecommendationsEvent === "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "click", item: "3111718", itemName: "Plane", itemDescription: "It is a big plane", itemCategory: "Aviation"});
        </script>


#### <a name="322-recommendation-click-event"></a><span data-ttu-id="d5838-163">3.2.2.</span><span class="sxs-lookup"><span data-stu-id="d5838-163">3.2.2.</span></span> <span data-ttu-id="d5838-164">Событие "щелчок рекомендации"</span><span class="sxs-lookup"><span data-stu-id="d5838-164">Recommendation Click Event</span></span>
<span data-ttu-id="d5838-165">Это событие должно использоваться всякий раз, когда пользователь щелкает элемент, который был получен из рекомендаций Azure ML в качестве рекомендованного элемента.</span><span class="sxs-lookup"><span data-stu-id="d5838-165">This event should be used any time a user clicked on an item that was received from Azure ML Recommendations as a recommended item.</span></span> <span data-ttu-id="d5838-166">Обычно в том случае, когда пользователь щелкает элемент открывается новая страница с hello сведения об элементе; на этой странице должна активироваться это событие.</span><span class="sxs-lookup"><span data-stu-id="d5838-166">Usually when user clicks on an item a new page is opened with hello item details; in this page this event should be triggered.</span></span>

<span data-ttu-id="d5838-167">Параметры</span><span class="sxs-lookup"><span data-stu-id="d5838-167">Parameters:</span></span>

* <span data-ttu-id="d5838-168">event (строка, обязательный) — recommendationclick.</span><span class="sxs-lookup"><span data-stu-id="d5838-168">event (string, mandatory) - “recommendationclick”</span></span>
* <span data-ttu-id="d5838-169">элемент (string, обязательные) — уникальный идентификатор элемента hello</span><span class="sxs-lookup"><span data-stu-id="d5838-169">item (string, mandatory) - Unique identifier of hello item</span></span>
* <span data-ttu-id="d5838-170">itemName (string, необязательно) — имя hello элемента hello</span><span class="sxs-lookup"><span data-stu-id="d5838-170">itemName (string, optional) - hello name of hello item</span></span>
* <span data-ttu-id="d5838-171">itemDescription (string, необязательно) — описание hello элемента hello</span><span class="sxs-lookup"><span data-stu-id="d5838-171">itemDescription (string, optional) - hello description of hello item</span></span>
* <span data-ttu-id="d5838-172">itemCategory (string, необязательно) — hello категорию элемента hello</span><span class="sxs-lookup"><span data-stu-id="d5838-172">itemCategory (string, optional) - hello category of hello item</span></span>
* <span data-ttu-id="d5838-173">начальные значения (массив строк, необязательно) - hello начальные значения, сформированных запросов рекомендацию hello.</span><span class="sxs-lookup"><span data-stu-id="d5838-173">seeds (string array, optional) - hello seeds that generated hello recommendation query.</span></span>
* <span data-ttu-id="d5838-174">recoList (массив строк, необязательно) - hello результат запроса рекомендация hello, вызвавшего hello элемента, который был щелкнут.</span><span class="sxs-lookup"><span data-stu-id="d5838-174">recoList (string array, optional) - hello result of hello recommendation request that generated hello item that was clicked.</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "recommendationclick", item: "18899918" });
        </script>

<span data-ttu-id="d5838-175">Или с дополнительными данными:</span><span class="sxs-lookup"><span data-stu-id="d5838-175">Or with optional data:</span></span>

        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: eventName, item: "198", itemName: "Plane2", itemDescription: "It is a big plane2", itemCategory: "Default2", seeds: ["Seed1", "Seed2"], recoList: ["199", "198", "197"]                 });
        </script>


#### <a name="323-add-shopping-cart-event"></a><span data-ttu-id="d5838-176">3.2.3.</span><span class="sxs-lookup"><span data-stu-id="d5838-176">3.2.3.</span></span> <span data-ttu-id="d5838-177">Событие добавления товара в корзину</span><span class="sxs-lookup"><span data-stu-id="d5838-177">Add Shopping Cart Event</span></span>
<span data-ttu-id="d5838-178">Это событие должно использоваться при hello пользователь добавлять элемент toohello Корзина для покупок.</span><span class="sxs-lookup"><span data-stu-id="d5838-178">This event should be used when hello user add an item toohello shopping cart.</span></span>
<span data-ttu-id="d5838-179">Параметры</span><span class="sxs-lookup"><span data-stu-id="d5838-179">Parameters:</span></span>

* <span data-ttu-id="d5838-180">event (строка, обязательный) — addshopcart.</span><span class="sxs-lookup"><span data-stu-id="d5838-180">event (string, mandatory) - “addshopcart”</span></span>
* <span data-ttu-id="d5838-181">элемент (string, обязательные) — уникальный идентификатор элемента hello</span><span class="sxs-lookup"><span data-stu-id="d5838-181">item (string, mandatory) - Unique identifier of hello item</span></span>
* <span data-ttu-id="d5838-182">itemName (string, необязательно) — имя hello элемента hello</span><span class="sxs-lookup"><span data-stu-id="d5838-182">itemName (string, optional) - hello name of hello item</span></span>
* <span data-ttu-id="d5838-183">itemDescription (string, необязательно) — описание hello элемента hello</span><span class="sxs-lookup"><span data-stu-id="d5838-183">itemDescription (string, optional) - hello description of hello item</span></span>
* <span data-ttu-id="d5838-184">itemCategory (string, необязательно) — hello категорию элемента hello</span><span class="sxs-lookup"><span data-stu-id="d5838-184">itemCategory (string, optional) - hello category of hello item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "addshopcart", item: "13221118" });
        </script>

#### <a name="324-remove-shopping-cart-event"></a><span data-ttu-id="d5838-185">3.2.4.</span><span class="sxs-lookup"><span data-stu-id="d5838-185">3.2.4.</span></span> <span data-ttu-id="d5838-186">Событие удаления товара из корзины</span><span class="sxs-lookup"><span data-stu-id="d5838-186">Remove Shopping Cart Event</span></span>
<span data-ttu-id="d5838-187">Это событие следует использовать, когда пользователь hello удаляет элемент toohello корзину для покупок.</span><span class="sxs-lookup"><span data-stu-id="d5838-187">This event should be used when hello user removes an item toohello shopping cart.</span></span>

<span data-ttu-id="d5838-188">Параметры</span><span class="sxs-lookup"><span data-stu-id="d5838-188">Parameters:</span></span>

* <span data-ttu-id="d5838-189">event (строка, обязательный) — removeshopcart.</span><span class="sxs-lookup"><span data-stu-id="d5838-189">event (string, mandatory) - “removeshopcart”</span></span>
* <span data-ttu-id="d5838-190">элемент (string, обязательные) — уникальный идентификатор элемента hello</span><span class="sxs-lookup"><span data-stu-id="d5838-190">item (string, mandatory) - Unique identifier of hello item</span></span>
* <span data-ttu-id="d5838-191">itemName (string, необязательно) — имя hello элемента hello</span><span class="sxs-lookup"><span data-stu-id="d5838-191">itemName (string, optional) - hello name of hello item</span></span>
* <span data-ttu-id="d5838-192">itemDescription (string, необязательно) — описание hello элемента hello</span><span class="sxs-lookup"><span data-stu-id="d5838-192">itemDescription (string, optional) - hello description of hello item</span></span>
* <span data-ttu-id="d5838-193">itemCategory (string, необязательно) — hello категорию элемента hello</span><span class="sxs-lookup"><span data-stu-id="d5838-193">itemCategory (string, optional) - hello category of hello item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "removeshopcart", item: "111118" });
        </script>

#### <a name="325-purchase-event"></a><span data-ttu-id="d5838-194">3.2.5.</span><span class="sxs-lookup"><span data-stu-id="d5838-194">3.2.5.</span></span> <span data-ttu-id="d5838-195">Событие покупки</span><span class="sxs-lookup"><span data-stu-id="d5838-195">Purchase Event</span></span>
<span data-ttu-id="d5838-196">Это событие можно использовать при hello пользователь приобрел свою корзину для покупок.</span><span class="sxs-lookup"><span data-stu-id="d5838-196">This event should be used when hello user purchased his shopping cart.</span></span>

<span data-ttu-id="d5838-197">Параметры</span><span class="sxs-lookup"><span data-stu-id="d5838-197">Parameters:</span></span>

* <span data-ttu-id="d5838-198">event (строка) — purchase.</span><span class="sxs-lookup"><span data-stu-id="d5838-198">event (string) - “purchase”</span></span>
* <span data-ttu-id="d5838-199">items ( Purchased[] ) — массив, содержащий запись для каждого приобретенного элемента.</span><span class="sxs-lookup"><span data-stu-id="d5838-199">items ( Purchased[] ) - Array holding an entry for each item purchased.</span></span><br><br>
  <span data-ttu-id="d5838-200">Формат приобретенных элементов</span><span class="sxs-lookup"><span data-stu-id="d5838-200">Purchased format:</span></span>
  * <span data-ttu-id="d5838-201">элемент (строка) — уникальный идентификатор элемента hello.</span><span class="sxs-lookup"><span data-stu-id="d5838-201">item (string) - Unique identifier of hello item.</span></span>
  * <span data-ttu-id="d5838-202">count (целое число или строка) — количество приобретенных элементов.</span><span class="sxs-lookup"><span data-stu-id="d5838-202">count (int or string) - number of items that were purchased.</span></span>
  * <span data-ttu-id="d5838-203">Цена (число с плавающей запятой или строка) — необязательное поле - hello цена hello элемента.</span><span class="sxs-lookup"><span data-stu-id="d5838-203">price (float or string) - optional field - hello price of hello item.</span></span>

<span data-ttu-id="d5838-204">Hello приведенном ниже примере показано покупки из 3 элементов (33, 34, 35) двух все заполнены поля (элемент, количество, цена) и второй (элемент 34) без цену.</span><span class="sxs-lookup"><span data-stu-id="d5838-204">hello example below shows purchase of 3 items (33, 34, 35), two with all fields populated (item, count, price) and one (item 34) without a price.</span></span>

        <script>
            if ( typeof AzureMLRecommendationsEvent == "undefined"){ AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "purchase", items: [{ item: "33", count: "1", price: "10" }, { item: "34", count: "2" }, { item: "35", count: "1", price: "210" }] });
        </script>

#### <a name="326-user-login-event"></a><span data-ttu-id="d5838-205">3.2.6.</span><span class="sxs-lookup"><span data-stu-id="d5838-205">3.2.6.</span></span> <span data-ttu-id="d5838-206">Событие входа пользователя</span><span class="sxs-lookup"><span data-stu-id="d5838-206">User Login Event</span></span>
<span data-ttu-id="d5838-207">Здравствуйте, Azure ML рекомендации библиотека создает и использовать куки-файла в порядке tooidentify события, полученные из браузера.</span><span class="sxs-lookup"><span data-stu-id="d5838-207">Azure ML Recommendations Event library creates and use a cookie in order tooidentify events that came from hello same browser.</span></span> <span data-ttu-id="d5838-208">В модели hello tooimprove порядок результатов Azure ML рекомендации обеспечивает tooset уникальный идентификатор пользователя, переопределяют hello использования файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="d5838-208">In order tooimprove hello model results Azure ML Recommendations enables tooset a user unique identification that will override hello cookie usage.</span></span>

<span data-ttu-id="d5838-209">Это событие можно использовать после узел tooyour входа пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="d5838-209">This event should be used after hello user login tooyour site.</span></span>

<span data-ttu-id="d5838-210">Параметры</span><span class="sxs-lookup"><span data-stu-id="d5838-210">Parameters:</span></span>

* <span data-ttu-id="d5838-211">event (строка) — userlogin.</span><span class="sxs-lookup"><span data-stu-id="d5838-211">event (string) - “userlogin”</span></span>
* <span data-ttu-id="d5838-212">пользователь (строка) — уникальный идентификатор пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="d5838-212">user (string) - unique identification of hello user.</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "userlogin", user: “ABCD10AA” });
        </script>

## <a name="4-consume-recommendations-via-javascript"></a><span data-ttu-id="d5838-213">4. Использование рекомендаций с помощью JavaScript</span><span class="sxs-lookup"><span data-stu-id="d5838-213">4. Consume Recommendations via JavaScript</span></span>
<span data-ttu-id="d5838-214">Hello код, который использует hello рекомендации по некоторому событию JavaScript инициируется hello клиента веб-страницы.</span><span class="sxs-lookup"><span data-stu-id="d5838-214">hello code that consumes hello recommendation is triggered by some JavaScript event by hello client’s webpage.</span></span> <span data-ttu-id="d5838-215">Hello рекомендация ответ включает hello рекомендуемые идентификаторы элементов, их имена и их оценки.</span><span class="sxs-lookup"><span data-stu-id="d5838-215">hello recommendation response includes hello recommended items Ids, their names and their ratings.</span></span> <span data-ttu-id="d5838-216">Это наиболее toouse на стороне интеграции hello server следует сделать этот параметр только для отображения списка hello рекомендуемых элементов - более сложные обработки (например, добавление метаданных элемента hello).</span><span class="sxs-lookup"><span data-stu-id="d5838-216">It’s best toouse this option only for a list display of hello recommended items - more complex handling (such as adding hello item’s metadata) should be done on hello server side integration.</span></span>

### <a name="41-consume-recommendations"></a><span data-ttu-id="d5838-217">4.1. Потребление рекомендаций</span><span class="sxs-lookup"><span data-stu-id="d5838-217">4.1 Consume Recommendations</span></span>
<span data-ttu-id="d5838-218">tooconsume рекомендации, необходимые tooinclude hello необходимые библиотеки JavaScript в страницу и toocall AzureMLRecommendationsStart.</span><span class="sxs-lookup"><span data-stu-id="d5838-218">tooconsume recommendations you need tooinclude hello required JavaScript libraries in your page and toocall AzureMLRecommendationsStart.</span></span> <span data-ttu-id="d5838-219">См. раздел 2.</span><span class="sxs-lookup"><span data-stu-id="d5838-219">See section 2.</span></span>

<span data-ttu-id="d5838-220">tooconsume рекомендаций для одного или нескольких элементов требуется вызывается метод toocall: AzureMLRecommendationsGetI2IRecommendation.</span><span class="sxs-lookup"><span data-stu-id="d5838-220">tooconsume recommendations for one or more items you need toocall a method called: AzureMLRecommendationsGetI2IRecommendation.</span></span>

<span data-ttu-id="d5838-221">Параметры</span><span class="sxs-lookup"><span data-stu-id="d5838-221">Parameters:</span></span>

* <span data-ttu-id="d5838-222">элементы (массив строк) — один или несколько элементов tooget рекомендации.</span><span class="sxs-lookup"><span data-stu-id="d5838-222">items (array of strings) - One or more items tooget recommendations for.</span></span> <span data-ttu-id="d5838-223">При использовании сборки Fbt здесь можно задать только один элемент.</span><span class="sxs-lookup"><span data-stu-id="d5838-223">If you consume an Fbt build then you can set here only one item.</span></span>
* <span data-ttu-id="d5838-224">numberOfResults (целое число) — количество необходимых результатов.</span><span class="sxs-lookup"><span data-stu-id="d5838-224">numberOfResults (int) - number of required results.</span></span>
* <span data-ttu-id="d5838-225">includeMetadata (логическое значение, необязательно) — Если задать too'true "Указывает, должны быть заполнены поля метаданных hello в результате hello.</span><span class="sxs-lookup"><span data-stu-id="d5838-225">includeMetadata (boolean, optional) - if set too‘true’ indicates that hello metadata field must be populated in hello result.</span></span>
* <span data-ttu-id="d5838-226">Функция обработки - функция, которая будет обрабатывать возвращаемые рекомендации hello.</span><span class="sxs-lookup"><span data-stu-id="d5838-226">Processing function - a function that will handle hello recommendations returned.</span></span> <span data-ttu-id="d5838-227">Hello данные возвращаются в виде массива:</span><span class="sxs-lookup"><span data-stu-id="d5838-227">hello data is returned as an array of:</span></span>
  * <span data-ttu-id="d5838-228">item — уникальный идентификатор элемента.</span><span class="sxs-lookup"><span data-stu-id="d5838-228">Item - item unique id</span></span>
  * <span data-ttu-id="d5838-229">name — имя элемента (если существует в каталоге).</span><span class="sxs-lookup"><span data-stu-id="d5838-229">name - item name (if exist in catalog)</span></span>
  * <span data-ttu-id="d5838-230">rating — рейтинг рекомендации.</span><span class="sxs-lookup"><span data-stu-id="d5838-230">rating - recommendation rating</span></span>
  * <span data-ttu-id="d5838-231">метаданные - строка, представляющая hello метаданных элемента hello</span><span class="sxs-lookup"><span data-stu-id="d5838-231">metadata - a string that represents hello metadata of hello item</span></span>

<span data-ttu-id="d5838-232">Пример: hello, следующий код запрашивает 8 рекомендации для элемента «64f6eb0d-947a-4c18-a16c-888da9e228ba» (и, не указывая includeMetadata - он неявно говорится, что метаданные не требуется), затем объединить результаты hello в буфер.</span><span class="sxs-lookup"><span data-stu-id="d5838-232">Example: hello following code requests 8 recommendations for item "64f6eb0d-947a-4c18-a16c-888da9e228ba" (and by not specifying includeMetadata - it implicitly says that no metadata is required), it then concatenate hello results into a buffer.</span></span>

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
