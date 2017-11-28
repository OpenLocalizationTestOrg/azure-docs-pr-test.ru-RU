---
title: "поведение кэширования Azure CDN со строками запроса aaaControl | Документы Microsoft"
description: "Элементы управления, как файлы, если они содержат строки запросов в кэше toobe кэширования Azure строки запроса CDN."
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
ms.openlocfilehash: e7a138b2decec624a29eb703ad9a291d19c44ee8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings"></a><span data-ttu-id="23066-103">Управление режимом кэширования Azure CDN с помощью строк запросов</span><span class="sxs-lookup"><span data-stu-id="23066-103">Control Azure CDN caching behavior with query strings</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="23066-104">Стандартный</span><span class="sxs-lookup"><span data-stu-id="23066-104">Standard</span></span>](cdn-query-string.md)
> * [<span data-ttu-id="23066-105">Azure CDN уровня "Премиум" от Verizon</span><span class="sxs-lookup"><span data-stu-id="23066-105">Azure CDN Premium from Verizon</span></span>](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="23066-106">Обзор</span><span class="sxs-lookup"><span data-stu-id="23066-106">Overview</span></span>
<span data-ttu-id="23066-107">Элементы управления, как файлы, если они содержат строки запросов в кэше toobe кэширования строки запроса.</span><span class="sxs-lookup"><span data-stu-id="23066-107">Query string caching controls how files are toobe cached when they contain query strings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="23066-108">Hello Standard и Premium CDN продукты содержат hello же кэширования функциональные возможности строку запроса, но отличается hello пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="23066-108">hello Standard and Premium CDN products provide hello same query string caching functionality, but hello user interface differs.</span></span>  <span data-ttu-id="23066-109">В этом документе описывается интерфейс hello для **Azure CDN Standard из Akamai** и **Azure CDN Standard из Verizon**.</span><span class="sxs-lookup"><span data-stu-id="23066-109">This document describes hello interface for **Azure CDN Standard from Akamai** and **Azure CDN Standard from Verizon**.</span></span>  <span data-ttu-id="23066-110">Дополнительные сведения о кэшировании строк запроса с помощью **Azure CDN уровня "Премиум" от Verizon** см. в статье [Управление поведением кэширования запросов CDN с помощью строк запроса — уровень Premium](cdn-query-string-premium.md).</span><span class="sxs-lookup"><span data-stu-id="23066-110">For query string caching with **Azure CDN Premium from Verizon**, see [Controlling caching behavior of CDN requests with query strings - Premium](cdn-query-string-premium.md).</span></span>
> 
> 

<span data-ttu-id="23066-111">Доступны три режима:</span><span class="sxs-lookup"><span data-stu-id="23066-111">Three modes are available:</span></span>

* <span data-ttu-id="23066-112">**Пропускать строки запросов**: это режим по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="23066-112">**Ignore query strings**:  This is hello default mode.</span></span>  <span data-ttu-id="23066-113">на первый запрос hello и активов hello кэша Hello CDN граничного узла передаст строку hello запроса из исходной toohello hello запрашивающей стороны.</span><span class="sxs-lookup"><span data-stu-id="23066-113">hello CDN edge node will pass hello query string from hello requestor toohello origin on hello first request and cache hello asset.</span></span>  <span data-ttu-id="23066-114">Все последующие запросы для этого ресурса, которые обслуживаются hello граничного узла будет пропускать строки запроса hello до истечения срока действия кэшированного активов hello.</span><span class="sxs-lookup"><span data-stu-id="23066-114">All subsequent requests for that asset that are served from hello edge node will ignore hello query string until hello cached asset expires.</span></span>
* <span data-ttu-id="23066-115">**Обойти кэширование для URL-адреса со строками запроса**: В этом режиме запросы со строками запроса не кэшируются на hello CDN граничного узла.</span><span class="sxs-lookup"><span data-stu-id="23066-115">**Bypass caching for URL with query strings**:  In this mode, requests with query strings are not cached at hello CDN edge node.</span></span>  <span data-ttu-id="23066-116">Hello граничного узла извлекает активов hello непосредственно из источника hello и передает его toohello запрашивающей стороне с каждым запросом.</span><span class="sxs-lookup"><span data-stu-id="23066-116">hello edge node retrieves hello asset directly from hello origin and passes it toohello requestor with each request.</span></span>
* <span data-ttu-id="23066-117">**Кэширование каждого уникального URL-адреса**: этот режим обрабатывает каждый запрос со строкой запроса как уникальный ресурс-контейнер с собственным кэшем.</span><span class="sxs-lookup"><span data-stu-id="23066-117">**Cache every unique URL**:  This mode treats each request with a query string as a unique asset with its own cache.</span></span>  <span data-ttu-id="23066-118">Например, hello ответа от источника hello для запроса на *foo.ashx?q=bar* бы кэшированный на hello граничного узла и возвращается для последующих кэшей с такой же строки запроса.</span><span class="sxs-lookup"><span data-stu-id="23066-118">For example, hello response from hello origin for a request for *foo.ashx?q=bar* would be cached at hello edge node and returned for subsequent caches with that same query string.</span></span>  <span data-ttu-id="23066-119">Запрос *foo.ashx?q=somethingelse* как отдельный ресурс с свой собственный toolive времени будет кэшироваться.</span><span class="sxs-lookup"><span data-stu-id="23066-119">A request for *foo.ashx?q=somethingelse* would be cached as a separate asset with its own time toolive.</span></span>

## <a name="changing-query-string-caching-settings-for-standard-cdn-profiles"></a><span data-ttu-id="23066-120">Изменение параметров кэширования строки запроса для профилей CDN уровня "Стандартный"</span><span class="sxs-lookup"><span data-stu-id="23066-120">Changing query string caching settings for standard CDN profiles</span></span>
1. <span data-ttu-id="23066-121">Из колонки профиля CDN hello щелкните hello конечной точкой CDN необходимо toomanage.</span><span class="sxs-lookup"><span data-stu-id="23066-121">From hello CDN profile blade, click hello CDN endpoint you wish toomanage.</span></span>
   
    ![Конечные точки в колонке профиля CDN](./media/cdn-query-string/cdn-endpoints.png)
   
    <span data-ttu-id="23066-123">Открывает колонку конечной точки CDN Hello.</span><span class="sxs-lookup"><span data-stu-id="23066-123">hello CDN endpoint blade opens.</span></span>
2. <span data-ttu-id="23066-124">Нажмите кнопку hello **Настройка** кнопки.</span><span class="sxs-lookup"><span data-stu-id="23066-124">Click hello **Configure** button.</span></span>
   
    ![Кнопка управления в колонке профиля CDN](./media/cdn-query-string/cdn-config-btn.png)
   
    <span data-ttu-id="23066-126">Открывает колонку конфигурации CDN Hello.</span><span class="sxs-lookup"><span data-stu-id="23066-126">hello CDN Configuration blade opens.</span></span>
3. <span data-ttu-id="23066-127">Выберите значение из hello **режим кэширования строк запросов** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="23066-127">Select a setting from hello **Query string caching behavior** dropdown.</span></span>
   
    ![Параметры кэширования строк запроса CDN](./media/cdn-query-string/cdn-query-string.png)
4. <span data-ttu-id="23066-129">После выбора нажмите кнопку hello **Сохранить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="23066-129">After making your selection, click hello **Save** button.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="23066-130">изменения параметров Hello может оказаться сразу же отображается, сколько потребуется времени для hello toopropagate регистрации через hello CDN.</span><span class="sxs-lookup"><span data-stu-id="23066-130">hello settings changes may not be immediately visible, as it takes time for hello registration toopropagate through hello CDN.</span></span>  <span data-ttu-id="23066-131">Для профилей <b>Azure CDN от Akamai</b> распространение обычно занимает не более минуты.</span><span class="sxs-lookup"><span data-stu-id="23066-131">For <b>Azure CDN from Akamai</b> profiles, propagation will usually complete within one minute.</span></span>  <span data-ttu-id="23066-132">Для профилей <b>Azure CDN от Verizon</b> распространение обычно завершается в течение 90 минут, но в некоторых случаях может занимать больше времени.</span><span class="sxs-lookup"><span data-stu-id="23066-132">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
> 
> 

