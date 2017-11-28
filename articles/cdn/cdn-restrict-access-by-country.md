---
title: "aaaRestrict содержимого Azure CDN по странам | Документы Microsoft"
description: "Узнайте, как функция фильтрации Geo toorestrict доступа tooyour Azure CDN содержимого с помощью hello."
services: cdn
documentationcenter: 
author: lichard
manager: akucer
editor: 
ms.assetid: 12c17cc5-28ee-4b0b-ba22-2266be2e786a
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: ffdd994612b6c9cfbf1a6e29d260709b4afa86e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="restrict-azure-cdn-content-by-country"></a><span data-ttu-id="cbf4a-103">Ограничение доступности содержимого Azure CDN по странам</span><span class="sxs-lookup"><span data-stu-id="cbf4a-103">Restrict Azure CDN content by country</span></span>

## <a name="overview"></a><span data-ttu-id="cbf4a-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="cbf4a-104">Overview</span></span>
<span data-ttu-id="cbf4a-105">Когда пользователь запрашивает контент, по умолчанию, независимо от того, где пользователь hello сделан этот запрос из обслуживается hello содержимого.</span><span class="sxs-lookup"><span data-stu-id="cbf4a-105">When a user requests your content, by default, hello content is served regardless of where hello user made this request from.</span></span> <span data-ttu-id="cbf4a-106">В некоторых случаях может потребоваться toorestrict доступа к содержимому tooyour по странам.</span><span class="sxs-lookup"><span data-stu-id="cbf4a-106">In some cases, you may want toorestrict access tooyour content by country.</span></span> <span data-ttu-id="cbf4a-107">В этом разделе объясняется как toouse hello **географическая фильтрация** компонентов в порядке tooconfigure hello tooallow или блокировать доступ к службе по странам.</span><span class="sxs-lookup"><span data-stu-id="cbf4a-107">This topic explains how toouse hello **Geo-Filtering** feature in order tooconfigure hello service tooallow or block access by country.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cbf4a-108">Hello Verizon и Akamai продукты содержат hello же функциональные возможности фильтрации geo, но имеют небольшими различиями в коды стран te, они поддерживают.</span><span class="sxs-lookup"><span data-stu-id="cbf4a-108">hello Verizon and Akamai products provide hello same geo-filtering functionality but have a small difference in te country codes they support.</span></span> <span data-ttu-id="cbf4a-109">Различия toohello связи см. шаг 3.</span><span class="sxs-lookup"><span data-stu-id="cbf4a-109">See Step 3 for a link toohello differences.</span></span>


<span data-ttu-id="cbf4a-110">Этот тип ограничения, сведения о вопросы, касающиеся tooconfiguring разделе hello [вопросы](cdn-restrict-access-by-country.md#considerations) раздел в конце hello hello раздела.</span><span class="sxs-lookup"><span data-stu-id="cbf4a-110">For information about considerations that apply tooconfiguring this type of restriction, see hello [Considerations](cdn-restrict-access-by-country.md#considerations) section at hello end of hello topic.</span></span>  

![фильтрации по стране](./media/cdn-filtering/cdn-country-filtering-akamai.png)

## <a name="step-1-define-hello-directory-path"></a><span data-ttu-id="cbf4a-112">Шаг 1: Определение путь к каталогу hello</span><span class="sxs-lookup"><span data-stu-id="cbf4a-112">Step 1: Define hello directory path</span></span>
<span data-ttu-id="cbf4a-113">Выберите конечную точку на портале hello и эта функция находится hello географическая фильтрация вкладка на левой навигационной toofind hello.</span><span class="sxs-lookup"><span data-stu-id="cbf4a-113">Select your endpoint within hello portal, and find hello Geo-Filtering tab on hello left-hand navigation toofind this feature.</span></span>

<span data-ttu-id="cbf4a-114">При настройке фильтра страны, необходимо указать hello относительный путь toohello расположение toowhich пользователей будет разрешен или запрещен доступ.</span><span class="sxs-lookup"><span data-stu-id="cbf4a-114">When configuring a country filter, you must specify hello relative path toohello location toowhich users will be allowed or denied access.</span></span> <span data-ttu-id="cbf4a-115">Геофильтрацию можно применить ко всем файлам в корневом каталоге ("/") или к выбранным каталогам, указав к ним пути, например "/pictures/".</span><span class="sxs-lookup"><span data-stu-id="cbf4a-115">You can apply geo-filtering for all your files with "/" or selected folders by specifying directory paths "/pictures/".</span></span> <span data-ttu-id="cbf4a-116">Также можно применить фильтрацию geo tooa отдельных файлов, указав файл hello и пропускают hello завершающей косой черты «/ pictures/city.png».</span><span class="sxs-lookup"><span data-stu-id="cbf4a-116">You can also apply geo-filtering tooa single file by specifying hello file, and leaving out hello trailing slash "/pictures/city.png".</span></span>

<span data-ttu-id="cbf4a-117">Пример фильтра по каталогу:</span><span class="sxs-lookup"><span data-stu-id="cbf4a-117">Example directory path filter:</span></span>

    /                                 
    /Photos/
    /Photos/Strasbourg/
      /Photos/Strasbourg/city.png

## <a name="step-2-define-hello-action-block-or-allow"></a><span data-ttu-id="cbf4a-118">Шаг 2: Определение действие hello: блокирующие или разрешающие</span><span class="sxs-lookup"><span data-stu-id="cbf4a-118">Step 2: Define hello action: block or allow</span></span>
<span data-ttu-id="cbf4a-119">**Блокировать:** пользователям hello указан странах будет запрещен доступ tooassets, запрашиваемый с этого пути рекурсивной.</span><span class="sxs-lookup"><span data-stu-id="cbf4a-119">**Block:** Users from hello specified countries will be denied access tooassets requested from that recursive path.</span></span> <span data-ttu-id="cbf4a-120">Если для этого пути не было настроено другой фильтрации по стране, то доступ для всех остальных пользователей будет разрешен.</span><span class="sxs-lookup"><span data-stu-id="cbf4a-120">If no other country filtering options have been configured for that location, then all other users will be allowed access.</span></span>

<span data-ttu-id="cbf4a-121">**Разрешить:** пользователям hello указан странах может tooassets доступа, запрашиваемый с этого пути рекурсивной.</span><span class="sxs-lookup"><span data-stu-id="cbf4a-121">**Allow:** Only users from hello specified countries will be allowed access tooassets requested from that recursive path.</span></span>

## <a name="step-3-define-hello-countries"></a><span data-ttu-id="cbf4a-122">Шаг 3: Определение странах hello</span><span class="sxs-lookup"><span data-stu-id="cbf4a-122">Step 3: Define hello countries</span></span>
<span data-ttu-id="cbf4a-123">Выберите hello странах, вы должны быть tooblock или разрешить для hello пути.</span><span class="sxs-lookup"><span data-stu-id="cbf4a-123">Select hello countries that you want tooblock or allow for hello path.</span></span> 

<span data-ttu-id="cbf4a-124">Например правило hello блокировки /Photos/Strasbourg/отфильтрует файлы в том числе:</span><span class="sxs-lookup"><span data-stu-id="cbf4a-124">For example, hello rule of blocking /Photos/Strasbourg/ will filter files including:</span></span>

    http://<endpoint>.azureedge.net/Photos/Strasbourg/1000.jpg
    http://<endpoint>.azureedge.net/Photos/Strasbourg/Cathedral/1000.jpg


### <a name="country-codes"></a><span data-ttu-id="cbf4a-125">Коды стран</span><span class="sxs-lookup"><span data-stu-id="cbf4a-125">Country codes</span></span>
<span data-ttu-id="cbf4a-126">Hello **географическая фильтрация** функция использует toodefine hello коды страны стран, из которых будут разрешены или заблокированы запрос для защищенной каталога.</span><span class="sxs-lookup"><span data-stu-id="cbf4a-126">hello **Geo-Filtering** feature uses country codes toodefine hello countries from which a request will be allowed or blocked for a secured directory.</span></span> <span data-ttu-id="cbf4a-127">Вы найдете hello коды стран в [коды стран CDN Azure](https://msdn.microsoft.com/library/mt761717.aspx).</span><span class="sxs-lookup"><span data-stu-id="cbf4a-127">You will find hello country codes in [Azure CDN  Country Codes](https://msdn.microsoft.com/library/mt761717.aspx).</span></span> 

## <span data-ttu-id="cbf4a-128"><a id="considerations"></a>Рекомендации</span><span class="sxs-lookup"><span data-stu-id="cbf4a-128"><a id="considerations"></a>Considerations</span></span>
* <span data-ttu-id="cbf4a-129">Он может занять too90 минут Verizon, или на несколько минут с Akamai, для изменения tooyour страны конфигурации tootake влияние фильтра.</span><span class="sxs-lookup"><span data-stu-id="cbf4a-129">It may take up too90 minutes for Verizon, or a couple minutes with Akamai, for changes tooyour country filtering configuration tootake effect.</span></span>
* <span data-ttu-id="cbf4a-130">Эта функция не поддерживает символы-шаблоны (например, *).</span><span class="sxs-lookup"><span data-stu-id="cbf4a-130">This feature does not support wildcard characters (for example, ‘*’).</span></span>
* <span data-ttu-id="cbf4a-131">Конфигурация географическая фильтрация Hello, связанные с относительным путем hello будет путь toothat применяются рекурсивно.</span><span class="sxs-lookup"><span data-stu-id="cbf4a-131">hello geo-filtering configuration associated with hello relative path will be applied recursively toothat path.</span></span>
* <span data-ttu-id="cbf4a-132">Только одно правило может быть применен toohello же относительный путь (не может создавать несколько фильтров, страны, toohello точки же относительный путь.</span><span class="sxs-lookup"><span data-stu-id="cbf4a-132">Only one rule can be applied toohello same relative path (you cannot create multiple country filters that point toohello same relative path.</span></span> <span data-ttu-id="cbf4a-133">Однако к одному и тому же каталогу могут применяться несколько фильтров стран.</span><span class="sxs-lookup"><span data-stu-id="cbf4a-133">However, a folder may have multiple country filters.</span></span> <span data-ttu-id="cbf4a-134">Это происходит из-за характера рекурсивные toohello фильтры страны.</span><span class="sxs-lookup"><span data-stu-id="cbf4a-134">This is due toohello recursive nature of country filters.</span></span> <span data-ttu-id="cbf4a-135">Другими словами, подкаталогу ранее настроенного каталога можно назначить другой фильтр страны.</span><span class="sxs-lookup"><span data-stu-id="cbf4a-135">In other words, a subfolder of a previously configured folder can be assigned a different country filter.</span></span>

