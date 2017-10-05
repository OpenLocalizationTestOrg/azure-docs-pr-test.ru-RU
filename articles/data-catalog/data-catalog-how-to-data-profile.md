---
title: "Практическое руководство по созданию профилей данных для источников данных"
description: "В статье приведены инструкции по добавлению профилей данных уровня таблиц и столбцов при регистрации источников данных в каталоге данных Azure. В статье также объясняется, как профили данных помогают анализировать имеющиеся источники."
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
ms.openlocfilehash: 8f4174f0ed74706b8275c8b1f0a62753f2834fa2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="data-profile-data-sources"></a><span data-ttu-id="65f8a-103">Источники данных профиля данных</span><span class="sxs-lookup"><span data-stu-id="65f8a-103">Data profile data sources</span></span>
## <a name="introduction"></a><span data-ttu-id="65f8a-104">Введение</span><span class="sxs-lookup"><span data-stu-id="65f8a-104">Introduction</span></span>
<span data-ttu-id="65f8a-105">**Каталог данных Microsoft Azure** — это полностью управляемая облачная служба, выполняющая функции систем регистрации и обнаружения корпоративных источников данных.</span><span class="sxs-lookup"><span data-stu-id="65f8a-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="65f8a-106">Проще говоря, **каталог данных Azure** помогает пользователям обнаруживать, оценивать и использовать источники данных, что, в свою очередь, повышает для организаций ценность их существующей информации.</span><span class="sxs-lookup"><span data-stu-id="65f8a-106">In other words, **Azure Data Catalog** is all about helping people discover, understand, and use data sources, and helping organizations to get more value from their existing data.</span></span> <span data-ttu-id="65f8a-107">Если источник данных зарегистрирован в **каталоге данных Azure**, его метаданные копируются и индексируются службой, но на этом работа с ними не заканчивается.</span><span class="sxs-lookup"><span data-stu-id="65f8a-107">When a data source is registered with **Azure Data Catalog**, its metadata is copied and indexed by the service, but the story doesn’t end there.</span></span>

<span data-ttu-id="65f8a-108">Функция **профилирования данных** **каталога данных Azure** проверяет данные из поддерживаемых источников данных в каталоге и собирает статистику и информацию об этих данных.</span><span class="sxs-lookup"><span data-stu-id="65f8a-108">The **Data Profiling** feature of **Azure Data Catalog** examines the data from supported data sources in your catalog and collects statistics and information about that data.</span></span> <span data-ttu-id="65f8a-109">Включить профиль ресурсов данных — очень легко.</span><span class="sxs-lookup"><span data-stu-id="65f8a-109">It's easy to include a profile of your data assets.</span></span> <span data-ttu-id="65f8a-110">При регистрации ресурса данных выберите пункт **Включить профиль данных** в средстве регистрации источника данных.</span><span class="sxs-lookup"><span data-stu-id="65f8a-110">When you register a data asset, choose **Include Data Profile** in the data source registration tool.</span></span>

## <a name="what-is-data-profiling"></a><span data-ttu-id="65f8a-111">Что такое профилирование данных</span><span class="sxs-lookup"><span data-stu-id="65f8a-111">What is Data Profiling</span></span>
<span data-ttu-id="65f8a-112">Профилирование данных — это проверка данных в регистрируемом источнике данных, а также сбор статистики и информации об этих данных.</span><span class="sxs-lookup"><span data-stu-id="65f8a-112">Data profiling examines the data in the data source being registered, and collects statistics and information about that data.</span></span> <span data-ttu-id="65f8a-113">Во время поиска источника данных эта статистика может помочь вам определить пригодность данных для решения той или иной бизнес-задачи.</span><span class="sxs-lookup"><span data-stu-id="65f8a-113">During data source discovery, these statistics can help you determine the suitability of the data to solve their business problem.</span></span>

<!-- In [How to discover data sources](data-catalog-how-to-discover.md), you learn about **Azure Data Catalog's** extensive search capabilities including searching for data assets that have a profile. See [How to include a data profile when registering a data source](#howto). -->

<span data-ttu-id="65f8a-114">Профилирование данных поддерживают такие источники данных:</span><span class="sxs-lookup"><span data-stu-id="65f8a-114">The following data sources support data profiling:</span></span>

* <span data-ttu-id="65f8a-115">таблицы и представления SQL Server (включая базы данных SQL Azure и хранилище данных SQL Azure);</span><span class="sxs-lookup"><span data-stu-id="65f8a-115">SQL Server (including Azure SQL DB and Azure SQL Data Warehouse) tables and views</span></span>
* <span data-ttu-id="65f8a-116">таблицы и представления Oracle;</span><span class="sxs-lookup"><span data-stu-id="65f8a-116">Oracle tables and views</span></span>
* <span data-ttu-id="65f8a-117">таблицы и представления Teradata;</span><span class="sxs-lookup"><span data-stu-id="65f8a-117">Teradata tables and views</span></span>
* <span data-ttu-id="65f8a-118">таблицы Hive.</span><span class="sxs-lookup"><span data-stu-id="65f8a-118">Hive tables</span></span>

<span data-ttu-id="65f8a-119">Включение профилей данных при регистрации ресурсов данных помогает пользователям ответить на следующие вопросы об источниках данных:</span><span class="sxs-lookup"><span data-stu-id="65f8a-119">Including data profiles when registering data assets helps users answer questions about data sources, including:</span></span>

* <span data-ttu-id="65f8a-120">Могу ли я с помощью этого источника данных решить свою бизнес-проблему?</span><span class="sxs-lookup"><span data-stu-id="65f8a-120">Can it be used to solve my business problem?</span></span>
* <span data-ttu-id="65f8a-121">Соответствуют ли данные определенным стандартам или шаблонам?</span><span class="sxs-lookup"><span data-stu-id="65f8a-121">Does the data conform to particular standards or patterns?</span></span>
* <span data-ttu-id="65f8a-122">Каковы аномалии этого источника данных?</span><span class="sxs-lookup"><span data-stu-id="65f8a-122">What are some of the anomalies of the data source?</span></span>
* <span data-ttu-id="65f8a-123">Каковы возможные проблемы интеграции этих данных в мое приложение?</span><span class="sxs-lookup"><span data-stu-id="65f8a-123">What are possible challenges of integrating this data into my application?</span></span>

> [!NOTE]
> <span data-ttu-id="65f8a-124">Кроме того, вы можете добавить документацию в ресурс, чтобы описать, как данные можно интегрировать в приложение.</span><span class="sxs-lookup"><span data-stu-id="65f8a-124">You can also add documentation to an asset to describe how data could be integrated into an application.</span></span> <span data-ttu-id="65f8a-125">Ознакомьтесь со статьей [Как создать документацию по источникам данных](data-catalog-how-to-documentation.md).</span><span class="sxs-lookup"><span data-stu-id="65f8a-125">See [How to document data sources](data-catalog-how-to-documentation.md).</span></span>
>
>

<a name="howto"/>

## <a name="how-to-include-a-data-profile-when-registering-a-data-source"></a><span data-ttu-id="65f8a-126">Как включить профиль данных при регистрации источника данных</span><span class="sxs-lookup"><span data-stu-id="65f8a-126">How to include a data profile when registering a data source</span></span>
<span data-ttu-id="65f8a-127">Включить профиль источника данных очень легко.</span><span class="sxs-lookup"><span data-stu-id="65f8a-127">It's easy to include a profile of your data source.</span></span> <span data-ttu-id="65f8a-128">Когда вы регистрируете источник данных, на панели **Объекты для регистрации** средства регистрации источника данных выберите **Включить профиль данных**.</span><span class="sxs-lookup"><span data-stu-id="65f8a-128">When you register a data source, in the **Objects to be registered** panel of the data source registration tool, choose **Include Data Profile**.</span></span>

![](media/data-catalog-data-profile/data-catalog-register-profile.png)

<span data-ttu-id="65f8a-129">Дополнительные сведения о том, как регистрировать источники данных, см. в статьях [Как регистрировать источники данных](data-catalog-how-to-register.md) и [Начало работы с каталогом данных Azure](data-catalog-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="65f8a-129">To learn more about how to register data sources, see [How to register data sources](data-catalog-how-to-register.md) and [Get started with Azure Data Catalog](data-catalog-get-started.md).</span></span>

## <a name="filtering-on-data-assets-that-include-data-profiles"></a><span data-ttu-id="65f8a-130">Фильтрация по ресурсам данных, которые включают в себя профили данных</span><span class="sxs-lookup"><span data-stu-id="65f8a-130">Filtering on data assets that include data profiles</span></span>
<span data-ttu-id="65f8a-131">Чтобы обнаружить ресурсы данных, которые включают в себя профили данных, вы можете использовать условие поиска `has:tableDataProfiles` или `has:columnsDataProfiles`.</span><span class="sxs-lookup"><span data-stu-id="65f8a-131">To discover data assets that include a data profile, you can include `has:tableDataProfiles` or `has:columnsDataProfiles` as one of your search terms.</span></span>

> [!NOTE]
> <span data-ttu-id="65f8a-132">Если в инструменте регистрации источников данных выбрать **Включить профиль данных** , то будут включены данные профиля уровня таблицы и столбца.</span><span class="sxs-lookup"><span data-stu-id="65f8a-132">Selecting **Include Data Profile** in the data source registration tool includes both table and column-level profile information.</span></span> <span data-ttu-id="65f8a-133">Тем не менее API каталога данных позволяет регистрировать ресурсы данных, содержащие только один набор данных профиля.</span><span class="sxs-lookup"><span data-stu-id="65f8a-133">However, the Data Catalog API allows data assets to be registered with only one set of profile information included.</span></span>
>
>

## <a name="viewing-data-profile-information"></a><span data-ttu-id="65f8a-134">Просмотр сведений о профиле данных</span><span class="sxs-lookup"><span data-stu-id="65f8a-134">Viewing data profile information</span></span>
<span data-ttu-id="65f8a-135">Найдя подходящий источник данных с профилем, вы можете просмотреть сведения об этом профиле данных.</span><span class="sxs-lookup"><span data-stu-id="65f8a-135">Once you find a suitable data source with a profile, you can view the data profile details.</span></span> <span data-ttu-id="65f8a-136">Для этого выберите ресурс данных и щелкните **Профиль данных** в окне портала каталога данных.</span><span class="sxs-lookup"><span data-stu-id="65f8a-136">To view the data profile, select a data asset and choose **Data Profile** in the Data Catalog portal window.</span></span>

![](media/data-catalog-data-profile/data-catalog-view.png)

<span data-ttu-id="65f8a-137">Профиль данных в **каталоге данных Azure** отображает сведения о профиле столбца и таблицы, в том числе приведенную ниже информацию.</span><span class="sxs-lookup"><span data-stu-id="65f8a-137">A data profile in **Azure Data Catalog** shows table and column profile information including:</span></span>

### <a name="object-data-profile"></a><span data-ttu-id="65f8a-138">Профиль данных объекта</span><span class="sxs-lookup"><span data-stu-id="65f8a-138">Object data profile</span></span>
* <span data-ttu-id="65f8a-139">Количество строк</span><span class="sxs-lookup"><span data-stu-id="65f8a-139">Number of rows</span></span>
* <span data-ttu-id="65f8a-140">Размер таблицы</span><span class="sxs-lookup"><span data-stu-id="65f8a-140">Table size</span></span>
* <span data-ttu-id="65f8a-141">Время последнего обновления объекта</span><span class="sxs-lookup"><span data-stu-id="65f8a-141">When the object was last updated</span></span>

### <a name="column-data-profile"></a><span data-ttu-id="65f8a-142">Профиль данных столбца</span><span class="sxs-lookup"><span data-stu-id="65f8a-142">Column data profile</span></span>
* <span data-ttu-id="65f8a-143">Тип данных столбца</span><span class="sxs-lookup"><span data-stu-id="65f8a-143">Column data type</span></span>
* <span data-ttu-id="65f8a-144">Количество уникальных значений</span><span class="sxs-lookup"><span data-stu-id="65f8a-144">Number of distinct values</span></span>
* <span data-ttu-id="65f8a-145">Количество строк со значением NULL</span><span class="sxs-lookup"><span data-stu-id="65f8a-145">Number of rows with NULL values</span></span>
* <span data-ttu-id="65f8a-146">Минимальное, максимальное, среднее и стандартное отклонение значений столбца</span><span class="sxs-lookup"><span data-stu-id="65f8a-146">Minimum, maximum, average, and standard deviation for column values</span></span>

## <a name="summary"></a><span data-ttu-id="65f8a-147">Сводка</span><span class="sxs-lookup"><span data-stu-id="65f8a-147">Summary</span></span>
<span data-ttu-id="65f8a-148">Профилирование данных дает возможность пользоваться информацией о зарегистрированных ресурсах данных и связанной с ними статистикой. Это позволяет определить, насколько те или иные данные подходят для решения бизнес-задач.</span><span class="sxs-lookup"><span data-stu-id="65f8a-148">Data profiling provides statistics and information about registered data assets to help you determine the suitability of the data to solve business problems.</span></span> <span data-ttu-id="65f8a-149">С помощью профилей данных можно не только аннотировать и документировать источники данных, но и предоставлять пользователям более точное описание своих данных.</span><span class="sxs-lookup"><span data-stu-id="65f8a-149">Along with annotating, and documenting data sources, data profiles can give users a deeper understanding of your data.</span></span>

## <a name="see-also"></a><span data-ttu-id="65f8a-150">См. также</span><span class="sxs-lookup"><span data-stu-id="65f8a-150">See Also</span></span>
* [<span data-ttu-id="65f8a-151">Как регистрировать источники данных</span><span class="sxs-lookup"><span data-stu-id="65f8a-151">How to register data sources</span></span>](data-catalog-how-to-register.md)
* [<span data-ttu-id="65f8a-152">Начало работы с каталогом данных Azure</span><span class="sxs-lookup"><span data-stu-id="65f8a-152">Get started with Azure Data Catalog</span></span>](data-catalog-get-started.md)
