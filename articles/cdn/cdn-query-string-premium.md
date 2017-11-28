---
title: "Управление режимом кэширования Azure CDN с помощью строк запросов (ценовая категория \"Премиум\") | Документация Майкрософт"
description: "Функция кэширования строк запроса Azure CDN управляет способом кэширования файлов, содержащих строки запроса."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 99db4a85-4f5f-431f-ac3a-69e05518c997
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 145067c2ce50b41c4783f4de4052c0e7cb529fc7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings---premium"></a><span data-ttu-id="cf51b-103">Управление режимом кэширования Azure CDN с помощью строк запросов (ценовая категория "Премиум")</span><span class="sxs-lookup"><span data-stu-id="cf51b-103">Control Azure CDN caching behavior with query strings - Premium</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cf51b-104">Стандартный</span><span class="sxs-lookup"><span data-stu-id="cf51b-104">Standard</span></span>](cdn-query-string.md)
> * [<span data-ttu-id="cf51b-105">Azure CDN уровня "Премиум" от Verizon</span><span class="sxs-lookup"><span data-stu-id="cf51b-105">Azure CDN Premium from Verizon</span></span>](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="cf51b-106">Обзор</span><span class="sxs-lookup"><span data-stu-id="cf51b-106">Overview</span></span>
<span data-ttu-id="cf51b-107">Функция кэширования строк запроса управляет способом кэширования файлов, содержащих строки запроса.</span><span class="sxs-lookup"><span data-stu-id="cf51b-107">Query string caching controls how files are to be cached when they contain query strings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cf51b-108">Продукты CDN уровня "Стандартный" и "Премиум" предоставляют одинаковые возможности кэширования строк запроса, но имеют разные пользовательские интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="cf51b-108">The Standard and Premium CDN products provide the same query string caching functionality, but the user interface differs.</span></span>  <span data-ttu-id="cf51b-109">В этом документе описывается пользовательский интерфейс для **Azure CDN уровня "Премиум" от Verizon**.</span><span class="sxs-lookup"><span data-stu-id="cf51b-109">This document describes the interface for **Azure CDN Premium from Verizon**.</span></span>  <span data-ttu-id="cf51b-110">Дополнительные сведения о кэшировании строк запроса с помощью **Azure CDN уровня "Стандартный" от Akamai** и **Azure CDN уровня "Стандартный" от Verizon** см. в статье [Управление режимом кэширования запросов CDN с использованием строк запроса](cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="cf51b-110">For query string caching with **Azure CDN Standard from Akamai** and **Azure CDN Standard from Verizon**, see [Controlling caching behavior of CDN requests with query strings](cdn-query-string.md).</span></span>
> 
> 

<span data-ttu-id="cf51b-111">Доступны три режима:</span><span class="sxs-lookup"><span data-stu-id="cf51b-111">Three modes are available:</span></span>

* <span data-ttu-id="cf51b-112">**стандартный кэш**: этот режим используется по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="cf51b-112">**standard-cache**:  This is the default mode.</span></span>  <span data-ttu-id="cf51b-113">Граничный узел CDN передает строку запроса от запрашивающей стороны в источник по первому запросу и кэширует ресурс-контейнер.</span><span class="sxs-lookup"><span data-stu-id="cf51b-113">The CDN edge node will pass the query string from the requestor to the origin on the first request and cache the asset.</span></span>  <span data-ttu-id="cf51b-114">Все последующие запросы к этому ресурсу, которые обслуживаются из граничного узла, будут пропускать строку запроса до истечения срока действия кэшированного ресурса.</span><span class="sxs-lookup"><span data-stu-id="cf51b-114">All subsequent requests for that asset that are served from the edge node will ignore the query string until the cached asset expires.</span></span>
* <span data-ttu-id="cf51b-115">**без кэша**: в этом режиме запросы со строками запроса не кэшируются в граничном узле CDN.</span><span class="sxs-lookup"><span data-stu-id="cf51b-115">**no-cache**:  In this mode, requests with query strings are not cached at the CDN edge node.</span></span>  <span data-ttu-id="cf51b-116">Граничный узел получает ресурс непосредственно из источника и передает его запрашивающей стороне с каждым запросом.</span><span class="sxs-lookup"><span data-stu-id="cf51b-116">The edge node retrieves the asset directly from the origin and passes it to the requestor with each request.</span></span>
* <span data-ttu-id="cf51b-117">**уникальный кэш**: этот режим обрабатывает каждый запрос со строкой запроса как уникальный ресурс с собственным кэшем.</span><span class="sxs-lookup"><span data-stu-id="cf51b-117">**unique-cache**:  This mode treats each request with a query string as a unique asset with its own cache.</span></span>  <span data-ttu-id="cf51b-118">Например, ответ из источника для запроса к *foo.ashx?q=bar* будет сохранен в кэше на граничном узле и возвращен для последующих кэшей с этой же строкой запроса.</span><span class="sxs-lookup"><span data-stu-id="cf51b-118">For example, the response from the origin for a request for *foo.ashx?q=bar* would be cached at the edge node and returned for subsequent caches with that same query string.</span></span>  <span data-ttu-id="cf51b-119">Запрос к *foo.ashx?q=somethingelse* будет кэшироваться как отдельный ресурс-контейнер с собственным сроком действия.</span><span class="sxs-lookup"><span data-stu-id="cf51b-119">A request for *foo.ashx?q=somethingelse* would be cached as a separate asset with its own time to live.</span></span>

## <a name="changing-query-string-caching-settings-for-premium-cdn-profiles"></a><span data-ttu-id="cf51b-120">Изменение параметров кэширования строки запроса для профилей CDN уровня "Премиум"</span><span class="sxs-lookup"><span data-stu-id="cf51b-120">Changing query string caching settings for premium CDN profiles</span></span>
1. <span data-ttu-id="cf51b-121">В колонке профиля сети CDN нажмите кнопку **Управление** .</span><span class="sxs-lookup"><span data-stu-id="cf51b-121">From the CDN profile blade, click the **Manage** button.</span></span>
   
    ![Кнопка управления в колонке профиля CDN](./media/cdn-query-string-premium/cdn-manage-btn.png)
   
    <span data-ttu-id="cf51b-123">Откроется портал управления CDN.</span><span class="sxs-lookup"><span data-stu-id="cf51b-123">The CDN management portal opens.</span></span>
2. <span data-ttu-id="cf51b-124">Наведите указатель мыши на вкладку **HTTP Large** (Большая платформа HTTP), а затем наведите указатель мыши на всплывающий элемент **Параметры кэша**.</span><span class="sxs-lookup"><span data-stu-id="cf51b-124">Hover over the **HTTP Large** tab, then hover over the **Cache Settings** flyout.</span></span>  <span data-ttu-id="cf51b-125">Щелкните **Кэширование строк запроса**.</span><span class="sxs-lookup"><span data-stu-id="cf51b-125">Click on **Query-String Caching**.</span></span>
   
    <span data-ttu-id="cf51b-126">Появятся параметры кэширования строк запроса.</span><span class="sxs-lookup"><span data-stu-id="cf51b-126">Query string caching options are displayed.</span></span>
   
    ![Параметры кэширования строк запроса CDN](./media/cdn-query-string-premium/cdn-query-string.png)
3. <span data-ttu-id="cf51b-128">После выбора нажмите кнопку **Обновить** .</span><span class="sxs-lookup"><span data-stu-id="cf51b-128">After making your selection, click the **Update** button.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cf51b-129">Изменения параметров вступают в силу не сразу, так как распространение регистрационных сведений по сети CDN может занять некоторое время.</span><span class="sxs-lookup"><span data-stu-id="cf51b-129">The settings changes may not be immediately visible, as it takes time for the registration to propagate through the CDN.</span></span>  <span data-ttu-id="cf51b-130">Для профилей <b>Azure CDN от Verizon</b> распространение обычно завершается в течение 90 минут, но в некоторых случаях может занимать больше времени.</span><span class="sxs-lookup"><span data-stu-id="cf51b-130">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
> 
> 

