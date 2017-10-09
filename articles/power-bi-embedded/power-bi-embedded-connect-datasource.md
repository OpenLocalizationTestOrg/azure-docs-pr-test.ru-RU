---
title: "Power BI Embedded - подключения источника данных tooa aaaMicrosoft"
description: "Power BI Embedded, подключить источники toodata"
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
ms.openlocfilehash: b1aad6e638104716d90f7e1d060eefcbc9daedbc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-data-source"></a><span data-ttu-id="91de5-103">Соединение с источником данных tooa</span><span class="sxs-lookup"><span data-stu-id="91de5-103">Connect tooa data source</span></span>
<span data-ttu-id="91de5-104">С **Power BI Embedded**вы сможете вставлять отчеты в свои приложения.</span><span class="sxs-lookup"><span data-stu-id="91de5-104">With **Power BI Embedded**, you can embed reports into your own app.</span></span> <span data-ttu-id="91de5-105">Если внедрение отчета Power BI в приложение, hello отчет подключается toohello исходные данные, **Импорт** копии данных hello или с помощью **непосредственное подключение** toohello источнику данных с помощью  **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="91de5-105">When you embed a Power BI report into your app, hello report connects toohello underlying data by **importing** a copy of hello data or by **connecting directly** toohello data source using **DirectQuery**.</span></span>

<span data-ttu-id="91de5-106">Ниже приведены hello различия между использованием **импорта** и **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="91de5-106">Here are hello differences between using **Import** and **DirectQuery**.</span></span>

| <span data-ttu-id="91de5-107">Импорт</span><span class="sxs-lookup"><span data-stu-id="91de5-107">Import</span></span> | <span data-ttu-id="91de5-108">DirectQuery</span><span class="sxs-lookup"><span data-stu-id="91de5-108">DirectQuery</span></span> |
| --- | --- |
| <span data-ttu-id="91de5-109">Таблицы, столбцы, *и данные* импортируются или копируются в наборе данных отчета hello.</span><span class="sxs-lookup"><span data-stu-id="91de5-109">Tables, columns, *and data* are imported or copied into hello report's dataset.</span></span> <span data-ttu-id="91de5-110">toosee изменения базовых данных, произошедших toohello, необходимо обновить или импортировать завершения, текущее набора данных еще раз.</span><span class="sxs-lookup"><span data-stu-id="91de5-110">toosee changes that occurred toohello underlying data, you must refresh, or import, a complete, current dataset again.</span></span> |<span data-ttu-id="91de5-111">Только *таблицы и столбцы* импортируются или копируются в наборе данных отчета hello.</span><span class="sxs-lookup"><span data-stu-id="91de5-111">Only *tables and columns* are imported or copied into hello report's dataset.</span></span> <span data-ttu-id="91de5-112">Всегда можно просмотреть hello самых последних данных.</span><span class="sxs-lookup"><span data-stu-id="91de5-112">You always view hello most current data.</span></span> |

<span data-ttu-id="91de5-113">Благодаря Power BI Embedded в настоящее время можно использовать DirectQuery с облачными источниками данных, но не с локальными источниками данных.</span><span class="sxs-lookup"><span data-stu-id="91de5-113">With Power BI Embedded, you can use DirectQuery with cloud data sources but not on-premises data sources at this time.</span></span>

> [!NOTE]
> <span data-ttu-id="91de5-114">Hello локальный шлюз данных не поддерживается с Power BI Embedded в данный момент.</span><span class="sxs-lookup"><span data-stu-id="91de5-114">hello On-Premises Data Gateway is not supported with Power BI Embedded at this time.</span></span> <span data-ttu-id="91de5-115">Это означает, что нельзя использовать DirectQuery для локальных источников данных.</span><span class="sxs-lookup"><span data-stu-id="91de5-115">This means you cannot use DirectQuery with on-premises data sources.</span></span>

## <a name="supported-data-sources"></a><span data-ttu-id="91de5-116">Поддерживаемые источники данных</span><span class="sxs-lookup"><span data-stu-id="91de5-116">Supported data sources</span></span>

<span data-ttu-id="91de5-117">**DirectQuery**</span><span class="sxs-lookup"><span data-stu-id="91de5-117">**DirectQuery**</span></span>
* <span data-ttu-id="91de5-118">База данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="91de5-118">Azure SQL database</span></span>
* <span data-ttu-id="91de5-119">Хранилище данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="91de5-119">Azure SQL Data Warehouse</span></span>

<span data-ttu-id="91de5-120">**Импорт**</span><span class="sxs-lookup"><span data-stu-id="91de5-120">**Import**</span></span>

<span data-ttu-id="91de5-121">Можно импортировать с помощью любых hello доступных источников данных в Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="91de5-121">You can import using all of hello available data sources within Power BI Desktop.</span></span> <span data-ttu-id="91de5-122">Вы будете **не** быть может toorefresh этих данных в Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="91de5-122">You will **not** be able toorefresh that data within Power BI Embedded.</span></span> <span data-ttu-id="91de5-123">Будет иметь изменения tooupload tooyour PBIX файл tooPower BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="91de5-123">You will have tooupload changes tooyour PBIX file tooPower BI Embedded.</span></span> <span data-ttu-id="91de5-124">Это происходит из-за toono доступного шлюза.</span><span class="sxs-lookup"><span data-stu-id="91de5-124">This is due toono available gateway.</span></span> 

## <a name="benefits-of-using-directquery"></a><span data-ttu-id="91de5-125">Преимущества использования DirectQuery</span><span class="sxs-lookup"><span data-stu-id="91de5-125">Benefits of using DirectQuery</span></span>
<span data-ttu-id="91de5-126">Использование **DirectQuery**связано с такими преимуществами:</span><span class="sxs-lookup"><span data-stu-id="91de5-126">There are two primary benefits when using **DirectQuery**:</span></span>

* <span data-ttu-id="91de5-127">**DirectQuery** Здравствуйте, позволяет создавать визуализации на очень больших наборов данных, где в противном случае было бы нецелесообразной toofirst импорта всех данных.</span><span class="sxs-lookup"><span data-stu-id="91de5-127">**DirectQuery** lets you build visualizations over very large datasets, where it otherwise would be unfeasible toofirst import all of hello data.</span></span>
* <span data-ttu-id="91de5-128">Изменения в базовых данных могут потребовать обновления данных, а для некоторых отчетов hello требуется toodisplay текущего данных может потребоваться большой объем данных, делая повторный импорт данных нецелесообразным.</span><span class="sxs-lookup"><span data-stu-id="91de5-128">Underlying data changes can require a refresh of data, and for some reports, hello need toodisplay current data can require large data transfers, making re-importing data unfeasible.</span></span> <span data-ttu-id="91de5-129">В отчетах **DirectQuery** , напротив, всегда используются текущие данные.</span><span class="sxs-lookup"><span data-stu-id="91de5-129">By contrast, **DirectQuery** reports always use current data.</span></span>

## <a name="limitations-of-directquery"></a><span data-ttu-id="91de5-130">Ограничения DirectQuery</span><span class="sxs-lookup"><span data-stu-id="91de5-130">Limitations of DirectQuery</span></span>
   <span data-ttu-id="91de5-131">Существует несколько ограничений toousing **DirectQuery**:</span><span class="sxs-lookup"><span data-stu-id="91de5-131">There are a few limitations toousing **DirectQuery**:</span></span>

* <span data-ttu-id="91de5-132">Все таблицы должны находиться в одной базе данных.</span><span class="sxs-lookup"><span data-stu-id="91de5-132">All tables must come from a single database.</span></span>
* <span data-ttu-id="91de5-133">Если hello является слишком сложным, произойдет ошибка.</span><span class="sxs-lookup"><span data-stu-id="91de5-133">If hello query is overly complex, an error will occur.</span></span> <span data-ttu-id="91de5-134">Ошибка hello tooremedy необходимо внести изменения в запрос hello, менее сложна.</span><span class="sxs-lookup"><span data-stu-id="91de5-134">tooremedy hello error you must refactor hello query so it is less complex.</span></span> <span data-ttu-id="91de5-135">Если запрос hello должны быть сложными, вам потребуется tooimport hello данные вместо использования **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="91de5-135">If hello query must be complex, you will need tooimport hello data instead of using **DirectQuery**.</span></span>
* <span data-ttu-id="91de5-136">Фильтрация связей — ограниченный tooa одно направление, а не в обоих направлениях.</span><span class="sxs-lookup"><span data-stu-id="91de5-136">Relationship filtering is limited tooa single direction, rather than both directions.</span></span>
* <span data-ttu-id="91de5-137">Невозможно изменить тип данных столбца hello.</span><span class="sxs-lookup"><span data-stu-id="91de5-137">You cannot change hello data type of a column.</span></span>
* <span data-ttu-id="91de5-138">По умолчанию ограничения помещаются в выражения DAX, разрешенные в мерах.</span><span class="sxs-lookup"><span data-stu-id="91de5-138">By default, limitations are placed on DAX expressions allowed in measures.</span></span> <span data-ttu-id="91de5-139">Дополнительные сведения см. в разделе [DirectQuery и меры](#measures).</span><span class="sxs-lookup"><span data-stu-id="91de5-139">See [DirectQuery and measures](#measures).</span></span>

<a name="measures"/>

## <a name="directquery-and-measures"></a><span data-ttu-id="91de5-140">DirectQuery и меры</span><span class="sxs-lookup"><span data-stu-id="91de5-140">DirectQuery and measures</span></span>
<span data-ttu-id="91de5-141">tooensure запросов, отправляемых toohello базового источника данных имеют приемлемую производительность, ограничения накладываются на меры.</span><span class="sxs-lookup"><span data-stu-id="91de5-141">tooensure queries sent toohello underlying data source have acceptable performance, limitations are imposed on measures.</span></span> <span data-ttu-id="91de5-142">При использовании **Power BI Desktop**расширенные пользователи могут выбирать toobypass это ограничение, выбрав **файл > Параметры и настройки > Параметры**.</span><span class="sxs-lookup"><span data-stu-id="91de5-142">When using **Power BI Desktop**, advanced users can choose toobypass this limitation by choosing **File > Options and settings > Options**.</span></span> <span data-ttu-id="91de5-143">В hello **параметры** диалоговое окно, выберите **DirectQuery**и выберите параметр hello **разрешить неограниченные меры в режиме DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="91de5-143">In hello **Options** dialog, choose **DirectQuery**, and select hello option **Allow unrestricted measures in DirectQuery mode**.</span></span> <span data-ttu-id="91de5-144">При выборе этого параметра может использоваться любое выражение DAX, которое является допустимым для меры.</span><span class="sxs-lookup"><span data-stu-id="91de5-144">When that option is selected, any DAX expression that is valid for a measure can be used.</span></span> <span data-ttu-id="91de5-145">Пользователям необходимо иметь в виду; Тем не менее, некоторые выражения, которые выполняют очень хорошо при импорте данных hello может привести к очень медленного выполнения запросов toohello внутреннего источника, когда оно **DirectQuery** режим.</span><span class="sxs-lookup"><span data-stu-id="91de5-145">Users must be aware; however, that some expressions that perform very well when hello data is imported may result in very slow queries toohello backend source when in **DirectQuery** mode.</span></span> 

## <a name="see-also"></a><span data-ttu-id="91de5-146">См. также</span><span class="sxs-lookup"><span data-stu-id="91de5-146">See Also</span></span>
* [<span data-ttu-id="91de5-147">Начало работы с Microsoft Power BI Embedded (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="91de5-147">Get started with Microsoft Power BI Embedded</span></span>](power-bi-embedded-get-started.md)
* [<span data-ttu-id="91de5-148">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="91de5-148">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)

<span data-ttu-id="91de5-149">У вас имеются и другие вопросы?</span><span class="sxs-lookup"><span data-stu-id="91de5-149">More questions?</span></span> [<span data-ttu-id="91de5-150">Повторите hello сообщества Power BI</span><span class="sxs-lookup"><span data-stu-id="91de5-150">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

