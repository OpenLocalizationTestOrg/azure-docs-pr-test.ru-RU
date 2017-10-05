---
title: "Предварительная загрузка ресурсов на конечной точке Azure CDN | Документация Майкрософт"
description: "Узнайте, как предварительно загружать кэшированное содержимое в конечной точке Azure CDN."
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 5ea3eba5-1335-413e-9af3-3918ce608a83
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 1f2dcd9a91bb6e883cbef06373c1acd98bf8d45f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="pre-load-assets-on-an-azure-cdn-endpoint"></a><span data-ttu-id="94173-103">Предварительная загрузка ресурсов на конечной точке CDN Azure</span><span class="sxs-lookup"><span data-stu-id="94173-103">Pre-load assets on an Azure CDN endpoint</span></span>
[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

<span data-ttu-id="94173-104">По умолчанию первое кэширование ресурсов происходит во время их запроса.</span><span class="sxs-lookup"><span data-stu-id="94173-104">By default, assets are first cached as they are requested.</span></span> <span data-ttu-id="94173-105">Это означает, что выполнение первого запроса в каждом регионе может занять больше времени, так как на пограничных серверах не будет кэшированного содержимого, а запрос потребуется пересылать на сервер-источник.</span><span class="sxs-lookup"><span data-stu-id="94173-105">This means that the first request from each region may take longer, since the edge servers will not have the content cached and will need to forward the request to the origin server.</span></span> <span data-ttu-id="94173-106">Предварительная загрузка содержимого позволяет избежать этой задержки первого вхождения.</span><span class="sxs-lookup"><span data-stu-id="94173-106">Pre-loading content avoids this first hit latency.</span></span>

<span data-ttu-id="94173-107">Помимо повышения удобства работы клиентов предварительная загрузка кэшированных ресурсов также может снизить объем сетевого трафика на сервере-источнике.</span><span class="sxs-lookup"><span data-stu-id="94173-107">In addition to providing a better customer experience, pre-loading your cached assets can also reduce network traffic on the origin server.</span></span>

> [!NOTE]
> <span data-ttu-id="94173-108">Предварительная загрузка ресурсов полезна для крупномасштабных событий или содержимого, которое становится доступным одновременно большому числу пользователей, например выход нового фильма или выпуск обновления программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="94173-108">Pre-loading assets is useful for  large events or content that becomes simultaneously available to a large number of users, such as a new movie release or a software update.</span></span>
> 
> 

<span data-ttu-id="94173-109">В этом учебнике рассматривается предварительная загрузка кэшированного содержимого на все пограничные узлы Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="94173-109">This tutorial walks you through pre-loading cached content on all Azure CDN edge nodes.</span></span>

## <a name="walkthrough"></a><span data-ttu-id="94173-110">Пошаговое руководство</span><span class="sxs-lookup"><span data-stu-id="94173-110">Walkthrough</span></span>
1. <span data-ttu-id="94173-111">На [портале Azure](https://portal.azure.com)перейдите к профилю сети CDN, содержащему конечную точку, которую необходимо предварительно загрузить.</span><span class="sxs-lookup"><span data-stu-id="94173-111">In the [Azure Portal](https://portal.azure.com), browse to the CDN profile containing the endpoint you wish to pre-load.</span></span>  <span data-ttu-id="94173-112">Откроется колонка профиля.</span><span class="sxs-lookup"><span data-stu-id="94173-112">The profile blade opens.</span></span>
2. <span data-ttu-id="94173-113">Щелкните конечную точку в списке.</span><span class="sxs-lookup"><span data-stu-id="94173-113">Click the endpoint in the list.</span></span>  <span data-ttu-id="94173-114">Откроется колонка конечной точки.</span><span class="sxs-lookup"><span data-stu-id="94173-114">The endpoint blade opens.</span></span>
3. <span data-ttu-id="94173-115">В колонке конечной точки CDN нажмите кнопку загрузки.</span><span class="sxs-lookup"><span data-stu-id="94173-115">From the CDN endpoint blade, click the load button.</span></span>
   
    ![Колонка конечной точки CDN](./media/cdn-preload-endpoint/cdn-endpoint-blade.png)
   
    <span data-ttu-id="94173-117">Откроется колонка загрузки.</span><span class="sxs-lookup"><span data-stu-id="94173-117">The Load blade opens.</span></span>
   
    ![Колонка нагрузки CDN](./media/cdn-preload-endpoint/cdn-load-blade.png)
4. <span data-ttu-id="94173-119">Введите полный путь к каждому ресурсу-контейнеру, который нужно загрузить (например, `/pictures/kitten.png`) в текстовом поле **Путь** .</span><span class="sxs-lookup"><span data-stu-id="94173-119">Enter the full path of each asset you wish to load (e.g., `/pictures/kitten.png`) in the **Path** textbox.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="94173-120">После ввода текста появятся дополнительные поля **Путь** для формирования списка из нескольких ресурсов.</span><span class="sxs-lookup"><span data-stu-id="94173-120">More **Path** textboxes will appear after you enter text to allow you to build a list of multiple assets.</span></span>  <span data-ttu-id="94173-121">Ресурсы можно удалить из списка, нажав кнопку с многоточием (...).</span><span class="sxs-lookup"><span data-stu-id="94173-121">You can delete assets from the list by clicking the ellipsis (...) button.</span></span>
   > 
   > <span data-ttu-id="94173-122">Пути должны быть относительными URL-адресами, которые соответствуют приведенному ниже [регулярному выражению](https://msdn.microsoft.com/library/az24scfc.aspx):</span><span class="sxs-lookup"><span data-stu-id="94173-122">Paths must be a relative URL that fits the following [regular expression](https://msdn.microsoft.com/library/az24scfc.aspx):</span></span>  
   > ><span data-ttu-id="94173-123">загрузка отдельного файла по пути `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`;</span><span class="sxs-lookup"><span data-stu-id="94173-123">Load a single file path `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`;</span></span>  
   > ><span data-ttu-id="94173-124">загрузку отдельного файла с помощью строки запроса `@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`.</span><span class="sxs-lookup"><span data-stu-id="94173-124">Load a single file with query string `@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`</span></span>  
   > 
   > <span data-ttu-id="94173-125">У каждого ресурса-контейнера должен быть собственный путь.</span><span class="sxs-lookup"><span data-stu-id="94173-125">Each asset must have its own path.</span></span>  <span data-ttu-id="94173-126">Для предварительной загрузки ресурсов-контейнеров не предусмотрено применение подстановочных знаков.</span><span class="sxs-lookup"><span data-stu-id="94173-126">There is no wildcard functionality for pre-loading assets.</span></span>
   > 
   > 
   
    ![Кнопка загрузки](./media/cdn-preload-endpoint/cdn-load-paths.png)
5. <span data-ttu-id="94173-128">Нажмите кнопку **Загрузить** .</span><span class="sxs-lookup"><span data-stu-id="94173-128">Click the **Load** button.</span></span>
   
    ![Кнопка загрузки](./media/cdn-preload-endpoint/cdn-load-button.png)

> [!NOTE]
> <span data-ttu-id="94173-130">Существует ограничение: 10 запросов на загрузку в минуту на профиль CDN.</span><span class="sxs-lookup"><span data-stu-id="94173-130">There is a limitation of 10 load requests per minute per CDN profile.</span></span> <span data-ttu-id="94173-131">На запрос разрешено использовать до 50 путей.</span><span class="sxs-lookup"><span data-stu-id="94173-131">50 paths are allowed per request.</span></span> <span data-ttu-id="94173-132">Каждый путь имеет ограничение по длине, равное 1024 символам.</span><span class="sxs-lookup"><span data-stu-id="94173-132">Each path has a path-length limit of 1024 characters.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="94173-133">См. также</span><span class="sxs-lookup"><span data-stu-id="94173-133">See also</span></span>
* [<span data-ttu-id="94173-134">Очистка конечной точки сети CDN Azure</span><span class="sxs-lookup"><span data-stu-id="94173-134">Purge an Azure CDN endpoint</span></span>](cdn-purge-endpoint.md)
* [<span data-ttu-id="94173-135">Справочник по API REST CDN. Очистка и предварительная загрузка конечной точки</span><span class="sxs-lookup"><span data-stu-id="94173-135">Azure CDN REST API reference - Purge or Pre-Load an Endpoint</span></span>](https://msdn.microsoft.com/library/mt634451.aspx)

