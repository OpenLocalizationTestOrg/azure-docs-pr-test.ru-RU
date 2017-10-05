---
title: "Управление режимом кэширования Azure CDN с помощью строк запросов | Документация Майкрософт"
description: "Функция кэширования строк запроса Azure CDN управляет способом кэширования файлов, содержащих строки запроса."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 17410e4f-130e-489c-834e-7ca6d6f9778d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 8d79626fa8516f226a82d3dac693c2033904c91d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings"></a><span data-ttu-id="61437-103">Управление режимом кэширования Azure CDN с помощью строк запросов</span><span class="sxs-lookup"><span data-stu-id="61437-103">Control Azure CDN caching behavior with query strings</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="61437-104">Стандартный</span><span class="sxs-lookup"><span data-stu-id="61437-104">Standard</span></span>](cdn-query-string.md)
> * [<span data-ttu-id="61437-105">Azure CDN уровня "Премиум" от Verizon</span><span class="sxs-lookup"><span data-stu-id="61437-105">Azure CDN Premium from Verizon</span></span>](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="61437-106">Обзор</span><span class="sxs-lookup"><span data-stu-id="61437-106">Overview</span></span>
<span data-ttu-id="61437-107">Функция кэширования строк запроса управляет способом кэширования файлов, содержащих строки запроса.</span><span class="sxs-lookup"><span data-stu-id="61437-107">Query string caching controls how files are to be cached when they contain query strings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="61437-108">Продукты CDN уровня "Стандартный" и "Премиум" предоставляют одинаковые возможности кэширования строк запроса, но имеют разные пользовательские интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="61437-108">The Standard and Premium CDN products provide the same query string caching functionality, but the user interface differs.</span></span>  <span data-ttu-id="61437-109">В этом документе описывается пользовательский интерфейс для **Azure CDN уровня "Стандартный" от Akamai** и **Azure CDN уровня "Стандартный" от Verizon**.</span><span class="sxs-lookup"><span data-stu-id="61437-109">This document describes the interface for **Azure CDN Standard from Akamai** and **Azure CDN Standard from Verizon**.</span></span>  <span data-ttu-id="61437-110">Дополнительные сведения о кэшировании строк запроса с помощью **Azure CDN уровня "Премиум" от Verizon** см. в статье [Управление поведением кэширования запросов CDN с помощью строк запроса — уровень Premium](cdn-query-string-premium.md).</span><span class="sxs-lookup"><span data-stu-id="61437-110">For query string caching with **Azure CDN Premium from Verizon**, see [Controlling caching behavior of CDN requests with query strings - Premium](cdn-query-string-premium.md).</span></span>
> 
> 

<span data-ttu-id="61437-111">Доступны три режима:</span><span class="sxs-lookup"><span data-stu-id="61437-111">Three modes are available:</span></span>

* <span data-ttu-id="61437-112">**Пропуск строк запроса**: этот режим используется по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="61437-112">**Ignore query strings**:  This is the default mode.</span></span>  <span data-ttu-id="61437-113">Граничный узел CDN передает строку запроса от запрашивающей стороны в источник по первому запросу и кэширует ресурс-контейнер.</span><span class="sxs-lookup"><span data-stu-id="61437-113">The CDN edge node will pass the query string from the requestor to the origin on the first request and cache the asset.</span></span>  <span data-ttu-id="61437-114">Все последующие запросы к этому ресурсу, которые обслуживаются из граничного узла, будут пропускать строку запроса до истечения срока действия кэшированного ресурса.</span><span class="sxs-lookup"><span data-stu-id="61437-114">All subsequent requests for that asset that are served from the edge node will ignore the query string until the cached asset expires.</span></span>
* <span data-ttu-id="61437-115">**Обход кэширования для URL-адресов со строками запроса**: в этом режиме запросы со строками запроса не кэшируются в граничном узле CDN.</span><span class="sxs-lookup"><span data-stu-id="61437-115">**Bypass caching for URL with query strings**:  In this mode, requests with query strings are not cached at the CDN edge node.</span></span>  <span data-ttu-id="61437-116">Граничный узел получает ресурс непосредственно из источника и передает его запрашивающей стороне с каждым запросом.</span><span class="sxs-lookup"><span data-stu-id="61437-116">The edge node retrieves the asset directly from the origin and passes it to the requestor with each request.</span></span>
* <span data-ttu-id="61437-117">**Кэширование каждого уникального URL-адреса**: этот режим обрабатывает каждый запрос со строкой запроса как уникальный ресурс-контейнер с собственным кэшем.</span><span class="sxs-lookup"><span data-stu-id="61437-117">**Cache every unique URL**:  This mode treats each request with a query string as a unique asset with its own cache.</span></span>  <span data-ttu-id="61437-118">Например, ответ из источника для запроса к *foo.ashx?q=bar* будет сохранен в кэше на граничном узле и возвращен для последующих кэшей с этой же строкой запроса.</span><span class="sxs-lookup"><span data-stu-id="61437-118">For example, the response from the origin for a request for *foo.ashx?q=bar* would be cached at the edge node and returned for subsequent caches with that same query string.</span></span>  <span data-ttu-id="61437-119">Запрос к *foo.ashx?q=somethingelse* будет кэшироваться как отдельный ресурс-контейнер с собственным сроком действия.</span><span class="sxs-lookup"><span data-stu-id="61437-119">A request for *foo.ashx?q=somethingelse* would be cached as a separate asset with its own time to live.</span></span>

## <a name="changing-query-string-caching-settings-for-standard-cdn-profiles"></a><span data-ttu-id="61437-120">Изменение параметров кэширования строки запроса для профилей CDN уровня "Стандартный"</span><span class="sxs-lookup"><span data-stu-id="61437-120">Changing query string caching settings for standard CDN profiles</span></span>
1. <span data-ttu-id="61437-121">В колонке профиля CDN щелкните конечную точку CDN, которой хотите управлять.</span><span class="sxs-lookup"><span data-stu-id="61437-121">From the CDN profile blade, click the CDN endpoint you wish to manage.</span></span>
   
    ![Конечные точки в колонке профиля CDN](./media/cdn-query-string/cdn-endpoints.png)
   
    <span data-ttu-id="61437-123">Откроется колонка конечной точки CDN.</span><span class="sxs-lookup"><span data-stu-id="61437-123">The CDN endpoint blade opens.</span></span>
2. <span data-ttu-id="61437-124">Нажмите кнопку **Настроить** .</span><span class="sxs-lookup"><span data-stu-id="61437-124">Click the **Configure** button.</span></span>
   
    ![Кнопка управления в колонке профиля CDN](./media/cdn-query-string/cdn-config-btn.png)
   
    <span data-ttu-id="61437-126">Откроется колонка настройки CDN.</span><span class="sxs-lookup"><span data-stu-id="61437-126">The CDN Configuration blade opens.</span></span>
3. <span data-ttu-id="61437-127">Выберите параметр из раскрывающегося списка **Query string caching behavior** (Режим кэширования строки запроса).</span><span class="sxs-lookup"><span data-stu-id="61437-127">Select a setting from the **Query string caching behavior** dropdown.</span></span>
   
    ![Параметры кэширования строк запроса CDN](./media/cdn-query-string/cdn-query-string.png)
4. <span data-ttu-id="61437-129">После выбора нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="61437-129">After making your selection, click the **Save** button.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="61437-130">Изменения параметров вступают в силу не сразу, так как распространение регистрационных сведений по сети CDN может занять некоторое время.</span><span class="sxs-lookup"><span data-stu-id="61437-130">The settings changes may not be immediately visible, as it takes time for the registration to propagate through the CDN.</span></span>  <span data-ttu-id="61437-131">Для профилей <b>Azure CDN от Akamai</b> распространение обычно занимает не более минуты.</span><span class="sxs-lookup"><span data-stu-id="61437-131">For <b>Azure CDN from Akamai</b> profiles, propagation will usually complete within one minute.</span></span>  <span data-ttu-id="61437-132">Для профилей <b>Azure CDN от Verizon</b> распространение обычно завершается в течение 90 минут, но в некоторых случаях может занимать больше времени.</span><span class="sxs-lookup"><span data-stu-id="61437-132">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
> 
> 

