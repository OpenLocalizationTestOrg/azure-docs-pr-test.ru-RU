---
title: "tooData aaaHow профилирования источников данных"
description: "Как tooarticle выделение как профили tooinclude уровня столбца и таблицы данных при регистрации источников данных в каталоге данных Azure и как данные toouse профили toounderstand источники данных."
services: data-catalog
documentationcenter: 
author: spelluru
manager: NA
editor: 
tags: 
ms.assetid: 94a8274b-5c9c-4962-a4b1-2fed38a3d919
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: 12c9f38501cdaee903d0dcbbdd0b82395f35a187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="data-profile-data-sources"></a><span data-ttu-id="4de43-103">Источники данных профиля данных</span><span class="sxs-lookup"><span data-stu-id="4de43-103">Data profile data sources</span></span>
## <a name="introduction"></a><span data-ttu-id="4de43-104">Введение</span><span class="sxs-lookup"><span data-stu-id="4de43-104">Introduction</span></span>
<span data-ttu-id="4de43-105">**Каталог данных Microsoft Azure** — это полностью управляемая облачная служба, выполняющая функции систем регистрации и обнаружения корпоративных источников данных.</span><span class="sxs-lookup"><span data-stu-id="4de43-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="4de43-106">Другими словами **каталога данных Azure** все о людях помочь обнаружить, понимать и использовать источники данных и помогает организациям tooget несколько значений из существующих данных.</span><span class="sxs-lookup"><span data-stu-id="4de43-106">In other words, **Azure Data Catalog** is all about helping people discover, understand, and use data sources, and helping organizations tooget more value from their existing data.</span></span> <span data-ttu-id="4de43-107">При регистрации источника данных с **каталога данных Azure**, его метаданные копируются и службой hello, но История hello не ограничивается не существует.</span><span class="sxs-lookup"><span data-stu-id="4de43-107">When a data source is registered with **Azure Data Catalog**, its metadata is copied and indexed by hello service, but hello story doesn’t end there.</span></span>

<span data-ttu-id="4de43-108">Hello **профилирование данных** функция **каталога данных Azure** проверяет hello данные из поддерживаемых источников данных в каталоге и собирает статистические данные и сведения об этих данных.</span><span class="sxs-lookup"><span data-stu-id="4de43-108">hello **Data Profiling** feature of **Azure Data Catalog** examines hello data from supported data sources in your catalog and collects statistics and information about that data.</span></span> <span data-ttu-id="4de43-109">Это легко tooinclude профиль ресурсов данных.</span><span class="sxs-lookup"><span data-stu-id="4de43-109">It's easy tooinclude a profile of your data assets.</span></span> <span data-ttu-id="4de43-110">При регистрации ресурса данных выберите **включить профиль данных** в средство регистрации источника данных hello.</span><span class="sxs-lookup"><span data-stu-id="4de43-110">When you register a data asset, choose **Include Data Profile** in hello data source registration tool.</span></span>

## <a name="what-is-data-profiling"></a><span data-ttu-id="4de43-111">Что такое профилирование данных</span><span class="sxs-lookup"><span data-stu-id="4de43-111">What is Data Profiling</span></span>
<span data-ttu-id="4de43-112">Профилирование данных проверяет данные hello в источнике данных hello регистрируемого и собирает статистические данные и сведения об этих данных.</span><span class="sxs-lookup"><span data-stu-id="4de43-112">Data profiling examines hello data in hello data source being registered, and collects statistics and information about that data.</span></span> <span data-ttu-id="4de43-113">Во время обнаружения источника данных может помочь статистику определения пригодности hello toosolve hello данных бизнес-задачи.</span><span class="sxs-lookup"><span data-stu-id="4de43-113">During data source discovery, these statistics can help you determine hello suitability of hello data toosolve their business problem.</span></span>

<!-- In [How toodiscover data sources](data-catalog-how-to-discover.md), you learn about **Azure Data Catalog's** extensive search capabilities including searching for data assets that have a profile. See [How tooinclude a data profile when registering a data source](#howto). -->

<span data-ttu-id="4de43-114">Hello следующие источники данных поддерживают профилирование данных:</span><span class="sxs-lookup"><span data-stu-id="4de43-114">hello following data sources support data profiling:</span></span>

* <span data-ttu-id="4de43-115">таблицы и представления SQL Server (включая базы данных SQL Azure и хранилище данных SQL Azure);</span><span class="sxs-lookup"><span data-stu-id="4de43-115">SQL Server (including Azure SQL DB and Azure SQL Data Warehouse) tables and views</span></span>
* <span data-ttu-id="4de43-116">таблицы и представления Oracle;</span><span class="sxs-lookup"><span data-stu-id="4de43-116">Oracle tables and views</span></span>
* <span data-ttu-id="4de43-117">таблицы и представления Teradata;</span><span class="sxs-lookup"><span data-stu-id="4de43-117">Teradata tables and views</span></span>
* <span data-ttu-id="4de43-118">таблицы Hive.</span><span class="sxs-lookup"><span data-stu-id="4de43-118">Hive tables</span></span>

<span data-ttu-id="4de43-119">Включение профилей данных при регистрации ресурсов данных помогает пользователям ответить на следующие вопросы об источниках данных:</span><span class="sxs-lookup"><span data-stu-id="4de43-119">Including data profiles when registering data assets helps users answer questions about data sources, including:</span></span>

* <span data-ttu-id="4de43-120">Он может быть используется toosolve Мои бизнес-задачи?</span><span class="sxs-lookup"><span data-stu-id="4de43-120">Can it be used toosolve my business problem?</span></span>
* <span data-ttu-id="4de43-121">Hello данных соответствует стандартам tooparticular или шаблоны?</span><span class="sxs-lookup"><span data-stu-id="4de43-121">Does hello data conform tooparticular standards or patterns?</span></span>
* <span data-ttu-id="4de43-122">Какие существуют аномалий hello hello источника данных?</span><span class="sxs-lookup"><span data-stu-id="4de43-122">What are some of hello anomalies of hello data source?</span></span>
* <span data-ttu-id="4de43-123">Каковы возможные проблемы интеграции этих данных в мое приложение?</span><span class="sxs-lookup"><span data-stu-id="4de43-123">What are possible challenges of integrating this data into my application?</span></span>

> [!NOTE]
> <span data-ttu-id="4de43-124">Можно также добавить документации tooan активов toodescribe как интеграции данных в приложение.</span><span class="sxs-lookup"><span data-stu-id="4de43-124">You can also add documentation tooan asset toodescribe how data could be integrated into an application.</span></span> <span data-ttu-id="4de43-125">В разделе [как источники данных toodocument](data-catalog-how-to-documentation.md).</span><span class="sxs-lookup"><span data-stu-id="4de43-125">See [How toodocument data sources](data-catalog-how-to-documentation.md).</span></span>
>
>

<a name="howto"/>

## <a name="how-tooinclude-a-data-profile-when-registering-a-data-source"></a><span data-ttu-id="4de43-126">Как tooinclude данных профилирования при регистрации источника данных</span><span class="sxs-lookup"><span data-stu-id="4de43-126">How tooinclude a data profile when registering a data source</span></span>
<span data-ttu-id="4de43-127">Это легко tooinclude профиля источника данных.</span><span class="sxs-lookup"><span data-stu-id="4de43-127">It's easy tooinclude a profile of your data source.</span></span> <span data-ttu-id="4de43-128">При регистрации источника данных, в hello **toobe объектов зарегистрирован** панель регистрации источников данных hello инструмент, выберите **включить профиль данных**.</span><span class="sxs-lookup"><span data-stu-id="4de43-128">When you register a data source, in hello **Objects toobe registered** panel of hello data source registration tool, choose **Include Data Profile**.</span></span>

![](media/data-catalog-data-profile/data-catalog-register-profile.png)

<span data-ttu-id="4de43-129">Дополнительные сведения о toolearn tooregister источники данных, в статье [как источники данных tooregister](data-catalog-how-to-register.md) и [приступить к работе с помощью каталога данных Azure](data-catalog-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4de43-129">toolearn more about how tooregister data sources, see [How tooregister data sources](data-catalog-how-to-register.md) and [Get started with Azure Data Catalog](data-catalog-get-started.md).</span></span>

## <a name="filtering-on-data-assets-that-include-data-profiles"></a><span data-ttu-id="4de43-130">Фильтрация по ресурсам данных, которые включают в себя профили данных</span><span class="sxs-lookup"><span data-stu-id="4de43-130">Filtering on data assets that include data profiles</span></span>
<span data-ttu-id="4de43-131">toodiscover средств данных, которые включают данные профиля, можно включить `has:tableDataProfiles` или `has:columnsDataProfiles` как одно из условий поиска.</span><span class="sxs-lookup"><span data-stu-id="4de43-131">toodiscover data assets that include a data profile, you can include `has:tableDataProfiles` or `has:columnsDataProfiles` as one of your search terms.</span></span>

> [!NOTE]
> <span data-ttu-id="4de43-132">При выборе **включить профиль данных** hello данных включает средство регистрации источника таблицы и сведения о профиле уровня столбца.</span><span class="sxs-lookup"><span data-stu-id="4de43-132">Selecting **Include Data Profile** in hello data source registration tool includes both table and column-level profile information.</span></span> <span data-ttu-id="4de43-133">Однако hello API каталога данных позволяет toobe активы данных зарегистрирован только один набор включены сведения о профиле.</span><span class="sxs-lookup"><span data-stu-id="4de43-133">However, hello Data Catalog API allows data assets toobe registered with only one set of profile information included.</span></span>
>
>

## <a name="viewing-data-profile-information"></a><span data-ttu-id="4de43-134">Просмотр сведений о профиле данных</span><span class="sxs-lookup"><span data-stu-id="4de43-134">Viewing data profile information</span></span>
<span data-ttu-id="4de43-135">После обнаружения источника данных подходящего с профилем, можно просмотреть сведения о профилях данных hello.</span><span class="sxs-lookup"><span data-stu-id="4de43-135">Once you find a suitable data source with a profile, you can view hello data profile details.</span></span> <span data-ttu-id="4de43-136">tooview hello данных профилирования выберите ресурса данных и **профиль данных** в окне портала каталога данных hello.</span><span class="sxs-lookup"><span data-stu-id="4de43-136">tooview hello data profile, select a data asset and choose **Data Profile** in hello Data Catalog portal window.</span></span>

![](media/data-catalog-data-profile/data-catalog-view.png)

<span data-ttu-id="4de43-137">Профиль данных в **каталоге данных Azure** отображает сведения о профиле столбца и таблицы, в том числе приведенную ниже информацию.</span><span class="sxs-lookup"><span data-stu-id="4de43-137">A data profile in **Azure Data Catalog** shows table and column profile information including:</span></span>

### <a name="object-data-profile"></a><span data-ttu-id="4de43-138">Профиль данных объекта</span><span class="sxs-lookup"><span data-stu-id="4de43-138">Object data profile</span></span>
* <span data-ttu-id="4de43-139">Количество строк</span><span class="sxs-lookup"><span data-stu-id="4de43-139">Number of rows</span></span>
* <span data-ttu-id="4de43-140">Размер таблицы</span><span class="sxs-lookup"><span data-stu-id="4de43-140">Table size</span></span>
* <span data-ttu-id="4de43-141">Время последнего обновления hello объекта</span><span class="sxs-lookup"><span data-stu-id="4de43-141">When hello object was last updated</span></span>

### <a name="column-data-profile"></a><span data-ttu-id="4de43-142">Профиль данных столбца</span><span class="sxs-lookup"><span data-stu-id="4de43-142">Column data profile</span></span>
* <span data-ttu-id="4de43-143">Тип данных столбца</span><span class="sxs-lookup"><span data-stu-id="4de43-143">Column data type</span></span>
* <span data-ttu-id="4de43-144">Количество уникальных значений</span><span class="sxs-lookup"><span data-stu-id="4de43-144">Number of distinct values</span></span>
* <span data-ttu-id="4de43-145">Количество строк со значением NULL</span><span class="sxs-lookup"><span data-stu-id="4de43-145">Number of rows with NULL values</span></span>
* <span data-ttu-id="4de43-146">Минимальное, максимальное, среднее и стандартное отклонение значений столбца</span><span class="sxs-lookup"><span data-stu-id="4de43-146">Minimum, maximum, average, and standard deviation for column values</span></span>

## <a name="summary"></a><span data-ttu-id="4de43-147">Сводка</span><span class="sxs-lookup"><span data-stu-id="4de43-147">Summary</span></span>
<span data-ttu-id="4de43-148">Профилирование данных предоставляет статистические данные и сведения о зарегистрированных данных активы toohelp определения пригодности hello hello данных toosolve бизнес-задач.</span><span class="sxs-lookup"><span data-stu-id="4de43-148">Data profiling provides statistics and information about registered data assets toohelp you determine hello suitability of hello data toosolve business problems.</span></span> <span data-ttu-id="4de43-149">С помощью профилей данных можно не только аннотировать и документировать источники данных, но и предоставлять пользователям более точное описание своих данных.</span><span class="sxs-lookup"><span data-stu-id="4de43-149">Along with annotating, and documenting data sources, data profiles can give users a deeper understanding of your data.</span></span>

## <a name="see-also"></a><span data-ttu-id="4de43-150">См. также</span><span class="sxs-lookup"><span data-stu-id="4de43-150">See Also</span></span>
* [<span data-ttu-id="4de43-151">Как источники данных tooregister</span><span class="sxs-lookup"><span data-stu-id="4de43-151">How tooregister data sources</span></span>](data-catalog-how-to-register.md)
* [<span data-ttu-id="4de43-152">Начало работы с каталогом данных Azure</span><span class="sxs-lookup"><span data-stu-id="4de43-152">Get started with Azure Data Catalog</span></span>](data-catalog-get-started.md)
