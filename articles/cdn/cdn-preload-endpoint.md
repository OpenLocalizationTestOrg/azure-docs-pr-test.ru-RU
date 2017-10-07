---
title: "активы aaaPre нагрузки на конечной точке Azure CDN | Документы Microsoft"
description: "Узнайте, как toopre нагрузки кэшированного содержимого в конечной точке Azure CDN."
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
ms.openlocfilehash: 08ac4b834f1ac8ce59d22e65fa8adea11bafcf17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="pre-load-assets-on-an-azure-cdn-endpoint"></a><span data-ttu-id="0274e-103">Предварительная загрузка ресурсов на конечной точке CDN Azure</span><span class="sxs-lookup"><span data-stu-id="0274e-103">Pre-load assets on an Azure CDN endpoint</span></span>
[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

<span data-ttu-id="0274e-104">По умолчанию первое кэширование ресурсов происходит во время их запроса.</span><span class="sxs-lookup"><span data-stu-id="0274e-104">By default, assets are first cached as they are requested.</span></span> <span data-ttu-id="0274e-105">Это означает, что hello первый запрос в каждом регионе может занять больше времени, поскольку hello пограничных серверов не будет иметь hello содержимого в кэше и потребуется tooforward hello запроса toohello исходного сервера.</span><span class="sxs-lookup"><span data-stu-id="0274e-105">This means that hello first request from each region may take longer, since hello edge servers will not have hello content cached and will need tooforward hello request toohello origin server.</span></span> <span data-ttu-id="0274e-106">Предварительная загрузка содержимого позволяет избежать этой задержки первого вхождения.</span><span class="sxs-lookup"><span data-stu-id="0274e-106">Pre-loading content avoids this first hit latency.</span></span>

<span data-ttu-id="0274e-107">В дополнение к этому tooproviding максимальное удобство работы клиентов, предварительная загрузка кэшированных активы можно также уменьшить сетевой трафик на исходном сервере hello.</span><span class="sxs-lookup"><span data-stu-id="0274e-107">In addition tooproviding a better customer experience, pre-loading your cached assets can also reduce network traffic on hello origin server.</span></span>

> [!NOTE]
> <span data-ttu-id="0274e-108">Предварительная загрузка ресурсов полезно для больших событий или содержимого, который становится одновременно доступных tooa большое количество пользователей, например нового выпуска фильма или обновления программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="0274e-108">Pre-loading assets is useful for  large events or content that becomes simultaneously available tooa large number of users, such as a new movie release or a software update.</span></span>
> 
> 

<span data-ttu-id="0274e-109">В этом учебнике рассматривается предварительная загрузка кэшированного содержимого на все пограничные узлы Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="0274e-109">This tutorial walks you through pre-loading cached content on all Azure CDN edge nodes.</span></span>

## <a name="walkthrough"></a><span data-ttu-id="0274e-110">Пошаговое руководство</span><span class="sxs-lookup"><span data-stu-id="0274e-110">Walkthrough</span></span>
1. <span data-ttu-id="0274e-111">В hello [портала Azure](https://portal.azure.com), Обзор профиля CDN toohello, содержащий конечную точку hello нужно toopre нагрузки.</span><span class="sxs-lookup"><span data-stu-id="0274e-111">In hello [Azure Portal](https://portal.azure.com), browse toohello CDN profile containing hello endpoint you wish toopre-load.</span></span>  <span data-ttu-id="0274e-112">Открывает колонку профиля Hello.</span><span class="sxs-lookup"><span data-stu-id="0274e-112">hello profile blade opens.</span></span>
2. <span data-ttu-id="0274e-113">Щелкните конечную точку hello в списке hello.</span><span class="sxs-lookup"><span data-stu-id="0274e-113">Click hello endpoint in hello list.</span></span>  <span data-ttu-id="0274e-114">Открывает колонку Hello конечной точки.</span><span class="sxs-lookup"><span data-stu-id="0274e-114">hello endpoint blade opens.</span></span>
3. <span data-ttu-id="0274e-115">Из колонки конечной точки CDN hello нажмите кнопку загрузки hello.</span><span class="sxs-lookup"><span data-stu-id="0274e-115">From hello CDN endpoint blade, click hello load button.</span></span>
   
    ![Колонка конечной точки CDN](./media/cdn-preload-endpoint/cdn-endpoint-blade.png)
   
    <span data-ttu-id="0274e-117">Открывает колонку нагрузки Hello.</span><span class="sxs-lookup"><span data-stu-id="0274e-117">hello Load blade opens.</span></span>
   
    ![Колонка нагрузки CDN](./media/cdn-preload-endpoint/cdn-load-blade.png)
4. <span data-ttu-id="0274e-119">Введите полный путь hello каждого средства нужно tooload (например, `/pictures/kitten.png`) в hello **путь** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="0274e-119">Enter hello full path of each asset you wish tooload (e.g., `/pictures/kitten.png`) in hello **Path** textbox.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="0274e-120">Дополнительные **путь** текстовые поля будут отображаться после ввода текста tooallow toobuild в списке несколько ресурсов.</span><span class="sxs-lookup"><span data-stu-id="0274e-120">More **Path** textboxes will appear after you enter text tooallow you toobuild a list of multiple assets.</span></span>  <span data-ttu-id="0274e-121">Ресурсы можно удалить из списка hello, нажав кнопку с многоточием (...) hello.</span><span class="sxs-lookup"><span data-stu-id="0274e-121">You can delete assets from hello list by clicking hello ellipsis (...) button.</span></span>
   > 
   > <span data-ttu-id="0274e-122">Пути должны быть относительный URL-адрес, который соответствует hello следующие [регулярное выражение](https://msdn.microsoft.com/library/az24scfc.aspx):</span><span class="sxs-lookup"><span data-stu-id="0274e-122">Paths must be a relative URL that fits hello following [regular expression](https://msdn.microsoft.com/library/az24scfc.aspx):</span></span>  
   > ><span data-ttu-id="0274e-123">загрузка отдельного файла по пути `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`;</span><span class="sxs-lookup"><span data-stu-id="0274e-123">Load a single file path `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`;</span></span>  
   > ><span data-ttu-id="0274e-124">загрузку отдельного файла с помощью строки запроса `@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`.</span><span class="sxs-lookup"><span data-stu-id="0274e-124">Load a single file with query string `@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`</span></span>  
   > 
   > <span data-ttu-id="0274e-125">У каждого ресурса-контейнера должен быть собственный путь.</span><span class="sxs-lookup"><span data-stu-id="0274e-125">Each asset must have its own path.</span></span>  <span data-ttu-id="0274e-126">Для предварительной загрузки ресурсов-контейнеров не предусмотрено применение подстановочных знаков.</span><span class="sxs-lookup"><span data-stu-id="0274e-126">There is no wildcard functionality for pre-loading assets.</span></span>
   > 
   > 
   
    ![Кнопка загрузки](./media/cdn-preload-endpoint/cdn-load-paths.png)
5. <span data-ttu-id="0274e-128">Нажмите кнопку hello **нагрузки** кнопки.</span><span class="sxs-lookup"><span data-stu-id="0274e-128">Click hello **Load** button.</span></span>
   
    ![Кнопка загрузки](./media/cdn-preload-endpoint/cdn-load-button.png)

> [!NOTE]
> <span data-ttu-id="0274e-130">Существует ограничение: 10 запросов на загрузку в минуту на профиль CDN.</span><span class="sxs-lookup"><span data-stu-id="0274e-130">There is a limitation of 10 load requests per minute per CDN profile.</span></span> <span data-ttu-id="0274e-131">На запрос разрешено использовать до 50 путей.</span><span class="sxs-lookup"><span data-stu-id="0274e-131">50 paths are allowed per request.</span></span> <span data-ttu-id="0274e-132">Каждый путь имеет ограничение по длине, равное 1024 символам.</span><span class="sxs-lookup"><span data-stu-id="0274e-132">Each path has a path-length limit of 1024 characters.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="0274e-133">См. также</span><span class="sxs-lookup"><span data-stu-id="0274e-133">See also</span></span>
* [<span data-ttu-id="0274e-134">Очистка конечной точки сети CDN Azure</span><span class="sxs-lookup"><span data-stu-id="0274e-134">Purge an Azure CDN endpoint</span></span>](cdn-purge-endpoint.md)
* [<span data-ttu-id="0274e-135">Справочник по API REST CDN. Очистка и предварительная загрузка конечной точки</span><span class="sxs-lookup"><span data-stu-id="0274e-135">Azure CDN REST API reference - Purge or Pre-Load an Endpoint</span></span>](https://msdn.microsoft.com/library/mt634451.aspx)

