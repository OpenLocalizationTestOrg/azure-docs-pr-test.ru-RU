---
title: "Ограничение доступности содержимого Azure CDN по странам | Документация Майкрософт"
description: "Узнайте, как ограничить доступ к содержимому Azure CDN, используя геофильтрацию."
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
ms.openlocfilehash: 30160088d9c770400f342e67527e1cf1cabc4f6b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="restrict-azure-cdn-content-by-country"></a><span data-ttu-id="6fa20-103">Ограничение доступности содержимого Azure CDN по странам</span><span class="sxs-lookup"><span data-stu-id="6fa20-103">Restrict Azure CDN content by country</span></span>

## <a name="overview"></a><span data-ttu-id="6fa20-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="6fa20-104">Overview</span></span>
<span data-ttu-id="6fa20-105">При запросе содержимого по умолчанию оно возвращается пользователю независимо от того, откуда был сделан запрос.</span><span class="sxs-lookup"><span data-stu-id="6fa20-105">When a user requests your content, by default, the content is served regardless of where the user made this request from.</span></span> <span data-ttu-id="6fa20-106">В некоторых случаях может потребоваться ограничить доступ к содержимому по стране.</span><span class="sxs-lookup"><span data-stu-id="6fa20-106">In some cases, you may want to restrict access to your content by country.</span></span> <span data-ttu-id="6fa20-107">В этой статье объясняется, как настроить функцию **геофильтрации** для разрешения или запрета доступа в зависимости от страны.</span><span class="sxs-lookup"><span data-stu-id="6fa20-107">This topic explains how to use the **Geo-Filtering** feature in order to configure the service to allow or block access by country.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6fa20-108">Продукты Verizon и Akamai обеспечивают аналогичные возможности геофильтрации, но их поддерживаемые ими коды стран немного отличаются.</span><span class="sxs-lookup"><span data-stu-id="6fa20-108">The Verizon and Akamai products provide the same geo-filtering functionality but have a small difference in te country codes they support.</span></span> <span data-ttu-id="6fa20-109">Ссылка на пояснение различий приведена в описании шага 3.</span><span class="sxs-lookup"><span data-stu-id="6fa20-109">See Step 3 for a link to the differences.</span></span>


<span data-ttu-id="6fa20-110">Сведения о рекомендациях по настройке этого типа ограничения см. в разделе [Рекомендации](cdn-restrict-access-by-country.md#considerations) в конце этой статьи.</span><span class="sxs-lookup"><span data-stu-id="6fa20-110">For information about considerations that apply to configuring this type of restriction, see the [Considerations](cdn-restrict-access-by-country.md#considerations) section at the end of the topic.</span></span>  

![фильтрации по стране](./media/cdn-filtering/cdn-country-filtering-akamai.png)

## <a name="step-1-define-the-directory-path"></a><span data-ttu-id="6fa20-112">Шаг 1. Определение пути к каталогу</span><span class="sxs-lookup"><span data-stu-id="6fa20-112">Step 1: Define the directory path</span></span>
<span data-ttu-id="6fa20-113">Выберите конечную точку на портале и найдите вкладку "Фильтрация по странам" на панели навигации слева, чтобы найти эту функцию.</span><span class="sxs-lookup"><span data-stu-id="6fa20-113">Select your endpoint within the portal, and find the Geo-Filtering tab on the left-hand navigation to find this feature.</span></span>

<span data-ttu-id="6fa20-114">При настройке фильтра страны необходимо указать относительный путь к каталогу, доступ к которому будет разрешен или запрещен.</span><span class="sxs-lookup"><span data-stu-id="6fa20-114">When configuring a country filter, you must specify the relative path to the location to which users will be allowed or denied access.</span></span> <span data-ttu-id="6fa20-115">Геофильтрацию можно применить ко всем файлам в корневом каталоге ("/") или к выбранным каталогам, указав к ним пути, например "/pictures/".</span><span class="sxs-lookup"><span data-stu-id="6fa20-115">You can apply geo-filtering for all your files with "/" or selected folders by specifying directory paths "/pictures/".</span></span> <span data-ttu-id="6fa20-116">Эту функцию также можно применить к одному файлу, указав файл и не ставя косую черту в конце, например "/pictures/city.png".</span><span class="sxs-lookup"><span data-stu-id="6fa20-116">You can also apply geo-filtering to a single file by specifying the file, and leaving out the trailing slash "/pictures/city.png".</span></span>

<span data-ttu-id="6fa20-117">Пример фильтра по каталогу:</span><span class="sxs-lookup"><span data-stu-id="6fa20-117">Example directory path filter:</span></span>

    /                                 
    /Photos/
    /Photos/Strasbourg/
      /Photos/Strasbourg/city.png

## <a name="step-2-define-the-action-block-or-allow"></a><span data-ttu-id="6fa20-118">Шаг 2. Определение действия: запрет или разрешение</span><span class="sxs-lookup"><span data-stu-id="6fa20-118">Step 2: Define the action: block or allow</span></span>
<span data-ttu-id="6fa20-119">**Запрет** : пользователям из указанных стран будет запрещен доступ к ресурсам, запрашиваемым по указанному рекурсивному пути.</span><span class="sxs-lookup"><span data-stu-id="6fa20-119">**Block:** Users from the specified countries will be denied access to assets requested from that recursive path.</span></span> <span data-ttu-id="6fa20-120">Если для этого пути не было настроено другой фильтрации по стране, то доступ для всех остальных пользователей будет разрешен.</span><span class="sxs-lookup"><span data-stu-id="6fa20-120">If no other country filtering options have been configured for that location, then all other users will be allowed access.</span></span>

<span data-ttu-id="6fa20-121">**Разрешение** : доступ к ресурсам, запрашиваемым по указанному рекурсивному пути, будет разрешен только пользователям из указанных стран.</span><span class="sxs-lookup"><span data-stu-id="6fa20-121">**Allow:** Only users from the specified countries will be allowed access to assets requested from that recursive path.</span></span>

## <a name="step-3-define-the-countries"></a><span data-ttu-id="6fa20-122">Шаг 3. Определение стран</span><span class="sxs-lookup"><span data-stu-id="6fa20-122">Step 3: Define the countries</span></span>
<span data-ttu-id="6fa20-123">Выберите страны, доступ из которых для выбранного пути нужно разрешить или запретить.</span><span class="sxs-lookup"><span data-stu-id="6fa20-123">Select the countries that you want to block or allow for the path.</span></span> 

<span data-ttu-id="6fa20-124">Правило запрета доступа /Photos/Strasbourg/ отфильтрует файлы, включая следующие:</span><span class="sxs-lookup"><span data-stu-id="6fa20-124">For example, the rule of blocking /Photos/Strasbourg/ will filter files including:</span></span>

    http://<endpoint>.azureedge.net/Photos/Strasbourg/1000.jpg
    http://<endpoint>.azureedge.net/Photos/Strasbourg/Cathedral/1000.jpg


### <a name="country-codes"></a><span data-ttu-id="6fa20-125">Коды стран</span><span class="sxs-lookup"><span data-stu-id="6fa20-125">Country codes</span></span>
<span data-ttu-id="6fa20-126">Функция **геофильтрации** использует коды стран, чтобы определить, из каких стран запрос к защищаемому каталогу будет разрешаться, а из каких — блокироваться.</span><span class="sxs-lookup"><span data-stu-id="6fa20-126">The **Geo-Filtering** feature uses country codes to define the countries from which a request will be allowed or blocked for a secured directory.</span></span> <span data-ttu-id="6fa20-127">Дополнительные сведения можно найти в списке [кодов стран для Azure CDN](https://msdn.microsoft.com/library/mt761717.aspx).</span><span class="sxs-lookup"><span data-stu-id="6fa20-127">You will find the country codes in [Azure CDN  Country Codes](https://msdn.microsoft.com/library/mt761717.aspx).</span></span> 

## <span data-ttu-id="6fa20-128"><a id="considerations"></a>Рекомендации</span><span class="sxs-lookup"><span data-stu-id="6fa20-128"><a id="considerations"></a>Considerations</span></span>
* <span data-ttu-id="6fa20-129">Чтобы изменения параметров фильтрации для вашей страны вступили в силу, в Akamai может потребоваться несколько минут, а в Verizon — до 90 минут.</span><span class="sxs-lookup"><span data-stu-id="6fa20-129">It may take up to 90 minutes for Verizon, or a couple minutes with Akamai, for changes to your country filtering configuration to take effect.</span></span>
* <span data-ttu-id="6fa20-130">Эта функция не поддерживает символы-шаблоны (например, *).</span><span class="sxs-lookup"><span data-stu-id="6fa20-130">This feature does not support wildcard characters (for example, ‘*’).</span></span>
* <span data-ttu-id="6fa20-131">Настройки геофильтрации, связанные с относительным путем, будут применяться рекурсивно к этому пути.</span><span class="sxs-lookup"><span data-stu-id="6fa20-131">The geo-filtering configuration associated with the relative path will be applied recursively to that path.</span></span>
* <span data-ttu-id="6fa20-132">К одному и тому же относительному пути может применяться только одно правило (нельзя создать несколько фильтров стран, которые указывают на один и тот же относительный путь).</span><span class="sxs-lookup"><span data-stu-id="6fa20-132">Only one rule can be applied to the same relative path (you cannot create multiple country filters that point to the same relative path.</span></span> <span data-ttu-id="6fa20-133">Однако к одному и тому же каталогу могут применяться несколько фильтров стран.</span><span class="sxs-lookup"><span data-stu-id="6fa20-133">However, a folder may have multiple country filters.</span></span> <span data-ttu-id="6fa20-134">Это возможно благодаря рекурсивной природе фильтров стран.</span><span class="sxs-lookup"><span data-stu-id="6fa20-134">This is due to the recursive nature of country filters.</span></span> <span data-ttu-id="6fa20-135">Другими словами, подкаталогу ранее настроенного каталога можно назначить другой фильтр страны.</span><span class="sxs-lookup"><span data-stu-id="6fa20-135">In other words, a subfolder of a previously configured folder can be assigned a different country filter.</span></span>

