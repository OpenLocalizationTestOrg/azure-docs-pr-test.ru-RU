---
title: "Microsoft Power BI Embedded — подключение к источнику данных"
description: "Power BI Embedded, подключение к источникам данных"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 2a4caeb3-255d-4215-9554-0ca8e3568c13
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: 9f614bbc63eae788aa52132c8f0e42ad8963559a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-a-data-source"></a><span data-ttu-id="9ca33-103">Подключение к источнику данных</span><span class="sxs-lookup"><span data-stu-id="9ca33-103">Connect to a data source</span></span>
<span data-ttu-id="9ca33-104">С **Power BI Embedded**вы сможете вставлять отчеты в свои приложения.</span><span class="sxs-lookup"><span data-stu-id="9ca33-104">With **Power BI Embedded**, you can embed reports into your own app.</span></span> <span data-ttu-id="9ca33-105">При внедрении отчета Power BI в приложение отчет подключается к базовым данным путем **импорта** копии данных или **непосредственного подключения** к источнику данных с помощью **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="9ca33-105">When you embed a Power BI report into your app, the report connects to the underlying data by **importing** a copy of the data or by **connecting directly** to the data source using **DirectQuery**.</span></span>

<span data-ttu-id="9ca33-106">Ниже описаны различия между **импортом** и **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="9ca33-106">Here are the differences between using **Import** and **DirectQuery**.</span></span>

| <span data-ttu-id="9ca33-107">Импорт</span><span class="sxs-lookup"><span data-stu-id="9ca33-107">Import</span></span> | <span data-ttu-id="9ca33-108">DirectQuery</span><span class="sxs-lookup"><span data-stu-id="9ca33-108">DirectQuery</span></span> |
| --- | --- |
| <span data-ttu-id="9ca33-109">Таблицы, столбцы и *данные* импортируются или копируются в набор данных отчета.</span><span class="sxs-lookup"><span data-stu-id="9ca33-109">Tables, columns, *and data* are imported or copied into the report's dataset.</span></span> <span data-ttu-id="9ca33-110">Чтобы определить изменения в базовых данных, вам нужно повторно обновить или импортировать готовый текущий набор данных.</span><span class="sxs-lookup"><span data-stu-id="9ca33-110">To see changes that occurred to the underlying data, you must refresh, or import, a complete, current dataset again.</span></span> |<span data-ttu-id="9ca33-111">В набор данных отчета импортируются или копируются только *таблицы и столбцы* .</span><span class="sxs-lookup"><span data-stu-id="9ca33-111">Only *tables and columns* are imported or copied into the report's dataset.</span></span> <span data-ttu-id="9ca33-112">Вы всегда просматриваете самые последние данные.</span><span class="sxs-lookup"><span data-stu-id="9ca33-112">You always view the most current data.</span></span> |

<span data-ttu-id="9ca33-113">Благодаря Power BI Embedded в настоящее время можно использовать DirectQuery с облачными источниками данных, но не с локальными источниками данных.</span><span class="sxs-lookup"><span data-stu-id="9ca33-113">With Power BI Embedded, you can use DirectQuery with cloud data sources but not on-premises data sources at this time.</span></span>

> [!NOTE]
> <span data-ttu-id="9ca33-114">В настоящее время Power BI Embedded не поддерживает локальный шлюз данных.</span><span class="sxs-lookup"><span data-stu-id="9ca33-114">The On-Premises Data Gateway is not supported with Power BI Embedded at this time.</span></span> <span data-ttu-id="9ca33-115">Это означает, что нельзя использовать DirectQuery для локальных источников данных.</span><span class="sxs-lookup"><span data-stu-id="9ca33-115">This means you cannot use DirectQuery with on-premises data sources.</span></span>

## <a name="supported-data-sources"></a><span data-ttu-id="9ca33-116">Поддерживаемые источники данных</span><span class="sxs-lookup"><span data-stu-id="9ca33-116">Supported data sources</span></span>

<span data-ttu-id="9ca33-117">**DirectQuery**</span><span class="sxs-lookup"><span data-stu-id="9ca33-117">**DirectQuery**</span></span>
* <span data-ttu-id="9ca33-118">База данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="9ca33-118">Azure SQL database</span></span>
* <span data-ttu-id="9ca33-119">Хранилище данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="9ca33-119">Azure SQL Data Warehouse</span></span>

<span data-ttu-id="9ca33-120">**Импорт**</span><span class="sxs-lookup"><span data-stu-id="9ca33-120">**Import**</span></span>

<span data-ttu-id="9ca33-121">Для импорта можно использовать все доступные источники данных в Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="9ca33-121">You can import using all of the available data sources within Power BI Desktop.</span></span> <span data-ttu-id="9ca33-122">Вы **не** сможете обновить эти данные в Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="9ca33-122">You will **not** be able to refresh that data within Power BI Embedded.</span></span> <span data-ttu-id="9ca33-123">Потребуется передать изменения в PBIX-файле в Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="9ca33-123">You will have to upload changes to your PBIX file to Power BI Embedded.</span></span> <span data-ttu-id="9ca33-124">Это вызвано тем, что шлюз недоступен.</span><span class="sxs-lookup"><span data-stu-id="9ca33-124">This is due to no available gateway.</span></span> 

## <a name="benefits-of-using-directquery"></a><span data-ttu-id="9ca33-125">Преимущества использования DirectQuery</span><span class="sxs-lookup"><span data-stu-id="9ca33-125">Benefits of using DirectQuery</span></span>
<span data-ttu-id="9ca33-126">Использование **DirectQuery**связано с такими преимуществами:</span><span class="sxs-lookup"><span data-stu-id="9ca33-126">There are two primary benefits when using **DirectQuery**:</span></span>

* <span data-ttu-id="9ca33-127">**DirectQuery** позволяет создавать визуализации для очень больших наборов данных, для которых невозможно выполнить первоначальный импорт всех данных.</span><span class="sxs-lookup"><span data-stu-id="9ca33-127">**DirectQuery** lets you build visualizations over very large datasets, where it otherwise would be unfeasible to first import all of the data.</span></span>
* <span data-ttu-id="9ca33-128">При изменении базовых данных может потребоваться обновление данных, а для некоторых отчетов для отображения текущих данных может потребоваться передача большого объема данных, что делает повторный импорт данных невозможным.</span><span class="sxs-lookup"><span data-stu-id="9ca33-128">Underlying data changes can require a refresh of data, and for some reports, the need to display current data can require large data transfers, making re-importing data unfeasible.</span></span> <span data-ttu-id="9ca33-129">В отчетах **DirectQuery** , напротив, всегда используются текущие данные.</span><span class="sxs-lookup"><span data-stu-id="9ca33-129">By contrast, **DirectQuery** reports always use current data.</span></span>

## <a name="limitations-of-directquery"></a><span data-ttu-id="9ca33-130">Ограничения DirectQuery</span><span class="sxs-lookup"><span data-stu-id="9ca33-130">Limitations of DirectQuery</span></span>
   <span data-ttu-id="9ca33-131">Существуют некоторые ограничения на использование **DirectQuery**:</span><span class="sxs-lookup"><span data-stu-id="9ca33-131">There are a few limitations to using **DirectQuery**:</span></span>

* <span data-ttu-id="9ca33-132">Все таблицы должны находиться в одной базе данных.</span><span class="sxs-lookup"><span data-stu-id="9ca33-132">All tables must come from a single database.</span></span>
* <span data-ttu-id="9ca33-133">Если запрос слишком сложный, произойдет ошибка.</span><span class="sxs-lookup"><span data-stu-id="9ca33-133">If the query is overly complex, an error will occur.</span></span> <span data-ttu-id="9ca33-134">Для исправления ошибки необходимо изменить запрос так, чтобы он был менее сложным.</span><span class="sxs-lookup"><span data-stu-id="9ca33-134">To remedy the error you must refactor the query so it is less complex.</span></span> <span data-ttu-id="9ca33-135">Если запрос должен быть сложным, необходимо импортировать данные, а не использовать **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="9ca33-135">If the query must be complex, you will need to import the data instead of using **DirectQuery**.</span></span>
* <span data-ttu-id="9ca33-136">Фильтрация по связи может выполняться только в одном направлении, а не в обоих направлениях.</span><span class="sxs-lookup"><span data-stu-id="9ca33-136">Relationship filtering is limited to a single direction, rather than both directions.</span></span>
* <span data-ttu-id="9ca33-137">Невозможно изменить тип данных столбца.</span><span class="sxs-lookup"><span data-stu-id="9ca33-137">You cannot change the data type of a column.</span></span>
* <span data-ttu-id="9ca33-138">По умолчанию ограничения помещаются в выражения DAX, разрешенные в мерах.</span><span class="sxs-lookup"><span data-stu-id="9ca33-138">By default, limitations are placed on DAX expressions allowed in measures.</span></span> <span data-ttu-id="9ca33-139">Дополнительные сведения см. в разделе [DirectQuery и меры](#measures).</span><span class="sxs-lookup"><span data-stu-id="9ca33-139">See [DirectQuery and measures](#measures).</span></span>

<a name="measures"/>

## <a name="directquery-and-measures"></a><span data-ttu-id="9ca33-140">DirectQuery и меры</span><span class="sxs-lookup"><span data-stu-id="9ca33-140">DirectQuery and measures</span></span>
<span data-ttu-id="9ca33-141">Чтобы обеспечить приемлемую производительность запросов к базовому источнику данных, на меры накладываются ограничения.</span><span class="sxs-lookup"><span data-stu-id="9ca33-141">To ensure queries sent to the underlying data source have acceptable performance, limitations are imposed on measures.</span></span> <span data-ttu-id="9ca33-142">При использовании **Power BI Desktop** опытные пользователи могут обойти это ограничение. Для этого нужно выбрать **Файл > Параметры и настройки > Параметры**.</span><span class="sxs-lookup"><span data-stu-id="9ca33-142">When using **Power BI Desktop**, advanced users can choose to bypass this limitation by choosing **File > Options and settings > Options**.</span></span> <span data-ttu-id="9ca33-143">В диалоговом окне **Параметры** выберите **DirectQuery** и установите параметр **Разрешить неограниченные меры в режиме DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="9ca33-143">In the **Options** dialog, choose **DirectQuery**, and select the option **Allow unrestricted measures in DirectQuery mode**.</span></span> <span data-ttu-id="9ca33-144">При выборе этого параметра может использоваться любое выражение DAX, которое является допустимым для меры.</span><span class="sxs-lookup"><span data-stu-id="9ca33-144">When that option is selected, any DAX expression that is valid for a measure can be used.</span></span> <span data-ttu-id="9ca33-145">Тем не менее пользователям следует помнить о том, что некоторые выражения, которые хорошо работают при импорте данных, могут привести к ощутимому замедлению запросов к серверному источнику в режиме **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="9ca33-145">Users must be aware; however, that some expressions that perform very well when the data is imported may result in very slow queries to the backend source when in **DirectQuery** mode.</span></span> 

## <a name="see-also"></a><span data-ttu-id="9ca33-146">См. также</span><span class="sxs-lookup"><span data-stu-id="9ca33-146">See Also</span></span>
* [<span data-ttu-id="9ca33-147">Начало работы с Microsoft Power BI Embedded (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="9ca33-147">Get started with Microsoft Power BI Embedded</span></span>](power-bi-embedded-get-started.md)
* [<span data-ttu-id="9ca33-148">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="9ca33-148">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)

<span data-ttu-id="9ca33-149">У вас имеются и другие вопросы?</span><span class="sxs-lookup"><span data-stu-id="9ca33-149">More questions?</span></span> [<span data-ttu-id="9ca33-150">Попробуйте задать их в сообществе Power BI</span><span class="sxs-lookup"><span data-stu-id="9ca33-150">Try the Power BI Community</span></span>](http://community.powerbi.com/)

