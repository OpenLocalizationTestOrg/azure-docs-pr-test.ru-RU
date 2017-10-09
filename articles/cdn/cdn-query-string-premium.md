---
title: "aaaControl поведение кэширования Azure CDN со строками запроса - Premium | Документы Microsoft"
description: "Элементы управления, как файлы, если они содержат строки запросов в кэше toobe кэширования Azure строки запроса CDN."
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
ms.openlocfilehash: 5c97cf0230ae13fd378bfce49481f3135a5ef101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings---premium"></a><span data-ttu-id="19e80-103">Управление режимом кэширования Azure CDN с помощью строк запросов (ценовая категория "Премиум")</span><span class="sxs-lookup"><span data-stu-id="19e80-103">Control Azure CDN caching behavior with query strings - Premium</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="19e80-104">Стандартный</span><span class="sxs-lookup"><span data-stu-id="19e80-104">Standard</span></span>](cdn-query-string.md)
> * [<span data-ttu-id="19e80-105">Azure CDN уровня "Премиум" от Verizon</span><span class="sxs-lookup"><span data-stu-id="19e80-105">Azure CDN Premium from Verizon</span></span>](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="19e80-106">Обзор</span><span class="sxs-lookup"><span data-stu-id="19e80-106">Overview</span></span>
<span data-ttu-id="19e80-107">Элементы управления, как файлы, если они содержат строки запросов в кэше toobe кэширования строки запроса.</span><span class="sxs-lookup"><span data-stu-id="19e80-107">Query string caching controls how files are toobe cached when they contain query strings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="19e80-108">Hello Standard и Premium CDN продукты содержат hello же кэширования функциональные возможности строку запроса, но отличается hello пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="19e80-108">hello Standard and Premium CDN products provide hello same query string caching functionality, but hello user interface differs.</span></span>  <span data-ttu-id="19e80-109">В этом документе описывается интерфейс hello для **Azure CDN Premium из Verizon**.</span><span class="sxs-lookup"><span data-stu-id="19e80-109">This document describes hello interface for **Azure CDN Premium from Verizon**.</span></span>  <span data-ttu-id="19e80-110">Дополнительные сведения о кэшировании строк запроса с помощью **Azure CDN уровня "Стандартный" от Akamai** и **Azure CDN уровня "Стандартный" от Verizon** см. в статье [Управление режимом кэширования запросов CDN с использованием строк запроса](cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="19e80-110">For query string caching with **Azure CDN Standard from Akamai** and **Azure CDN Standard from Verizon**, see [Controlling caching behavior of CDN requests with query strings](cdn-query-string.md).</span></span>
> 
> 

<span data-ttu-id="19e80-111">Доступны три режима:</span><span class="sxs-lookup"><span data-stu-id="19e80-111">Three modes are available:</span></span>

* <span data-ttu-id="19e80-112">**кэш Standard**: это режим по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="19e80-112">**standard-cache**:  This is hello default mode.</span></span>  <span data-ttu-id="19e80-113">на первый запрос hello и активов hello кэша Hello CDN граничного узла передаст строку hello запроса из исходной toohello hello запрашивающей стороны.</span><span class="sxs-lookup"><span data-stu-id="19e80-113">hello CDN edge node will pass hello query string from hello requestor toohello origin on hello first request and cache hello asset.</span></span>  <span data-ttu-id="19e80-114">Все последующие запросы для этого ресурса, которые обслуживаются hello граничного узла будет пропускать строки запроса hello до истечения срока действия кэшированного активов hello.</span><span class="sxs-lookup"><span data-stu-id="19e80-114">All subsequent requests for that asset that are served from hello edge node will ignore hello query string until hello cached asset expires.</span></span>
* <span data-ttu-id="19e80-115">**Нет-cache**: В этом режиме запросы со строками запроса не кэшируются на hello CDN граничного узла.</span><span class="sxs-lookup"><span data-stu-id="19e80-115">**no-cache**:  In this mode, requests with query strings are not cached at hello CDN edge node.</span></span>  <span data-ttu-id="19e80-116">Hello граничного узла извлекает активов hello непосредственно из источника hello и передает его toohello запрашивающей стороне с каждым запросом.</span><span class="sxs-lookup"><span data-stu-id="19e80-116">hello edge node retrieves hello asset directly from hello origin and passes it toohello requestor with each request.</span></span>
* <span data-ttu-id="19e80-117">**уникальный кэш**: этот режим обрабатывает каждый запрос со строкой запроса как уникальный ресурс с собственным кэшем.</span><span class="sxs-lookup"><span data-stu-id="19e80-117">**unique-cache**:  This mode treats each request with a query string as a unique asset with its own cache.</span></span>  <span data-ttu-id="19e80-118">Например, hello ответа от источника hello для запроса на *foo.ashx?q=bar* бы кэшированный на hello граничного узла и возвращается для последующих кэшей с такой же строки запроса.</span><span class="sxs-lookup"><span data-stu-id="19e80-118">For example, hello response from hello origin for a request for *foo.ashx?q=bar* would be cached at hello edge node and returned for subsequent caches with that same query string.</span></span>  <span data-ttu-id="19e80-119">Запрос *foo.ashx?q=somethingelse* как отдельный ресурс с свой собственный toolive времени будет кэшироваться.</span><span class="sxs-lookup"><span data-stu-id="19e80-119">A request for *foo.ashx?q=somethingelse* would be cached as a separate asset with its own time toolive.</span></span>

## <a name="changing-query-string-caching-settings-for-premium-cdn-profiles"></a><span data-ttu-id="19e80-120">Изменение параметров кэширования строки запроса для профилей CDN уровня "Премиум"</span><span class="sxs-lookup"><span data-stu-id="19e80-120">Changing query string caching settings for premium CDN profiles</span></span>
1. <span data-ttu-id="19e80-121">В колонке профиля CDN hello выберите hello **управление** кнопки.</span><span class="sxs-lookup"><span data-stu-id="19e80-121">From hello CDN profile blade, click hello **Manage** button.</span></span>
   
    ![Кнопка управления в колонке профиля CDN](./media/cdn-query-string-premium/cdn-manage-btn.png)
   
    <span data-ttu-id="19e80-123">Открытие портала управления CDN Hello.</span><span class="sxs-lookup"><span data-stu-id="19e80-123">hello CDN management portal opens.</span></span>
2. <span data-ttu-id="19e80-124">Наведите указатель мыши hello **HTTP больших** , а затем наведите указатель мыши hello **параметры кэша** всплывающим меню.</span><span class="sxs-lookup"><span data-stu-id="19e80-124">Hover over hello **HTTP Large** tab, then hover over hello **Cache Settings** flyout.</span></span>  <span data-ttu-id="19e80-125">Щелкните **Кэширование строк запроса**.</span><span class="sxs-lookup"><span data-stu-id="19e80-125">Click on **Query-String Caching**.</span></span>
   
    <span data-ttu-id="19e80-126">Появятся параметры кэширования строк запроса.</span><span class="sxs-lookup"><span data-stu-id="19e80-126">Query string caching options are displayed.</span></span>
   
    ![Параметры кэширования строк запроса CDN](./media/cdn-query-string-premium/cdn-query-string.png)
3. <span data-ttu-id="19e80-128">После выбора нажмите кнопку hello **обновление** кнопки.</span><span class="sxs-lookup"><span data-stu-id="19e80-128">After making your selection, click hello **Update** button.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="19e80-129">изменения параметров Hello может оказаться сразу же отображается, сколько потребуется времени для hello toopropagate регистрации через hello CDN.</span><span class="sxs-lookup"><span data-stu-id="19e80-129">hello settings changes may not be immediately visible, as it takes time for hello registration toopropagate through hello CDN.</span></span>  <span data-ttu-id="19e80-130">Для профилей <b>Azure CDN от Verizon</b> распространение обычно завершается в течение 90 минут, но в некоторых случаях может занимать больше времени.</span><span class="sxs-lookup"><span data-stu-id="19e80-130">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
> 
> 

