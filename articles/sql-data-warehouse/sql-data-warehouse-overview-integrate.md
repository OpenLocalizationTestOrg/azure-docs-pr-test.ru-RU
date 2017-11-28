---
title: "aaaBuild интегрированных решений с хранилищем данных SQL | Документы Microsoft"
description: "Инструменты и партнерские решения, которые интегрируются с хранилищем данных SQL "
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: e2dc8f3f-10e3-4589-a4e2-50c67dfcf67f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: c8a4202dd84305bea4e4c2faf0e4791d026e794f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="leverage-other-services-with-sql-data-warehouse"></a><span data-ttu-id="d85c4-103">Интеграция других служб с хранилищем данных SQL</span><span class="sxs-lookup"><span data-stu-id="d85c4-103">Leverage other services with SQL Data Warehouse</span></span>
<span data-ttu-id="d85c4-104">В дополнение к этому tooits основные функциональные возможности, хранилище данных SQL позволяет пользователям tooleverage многие hello другие службы в Azure, наряду с его.</span><span class="sxs-lookup"><span data-stu-id="d85c4-104">In addition tooits core functionality, SQL Data Warehouse enables users tooleverage many of hello other services in Azure alongside it.</span></span>  <span data-ttu-id="d85c4-105">В частности в настоящее время перешли toodeeply интегрировать hello следующие действия:</span><span class="sxs-lookup"><span data-stu-id="d85c4-105">Specifically, we have currently taken steps toodeeply integrate with hello following:</span></span>

* <span data-ttu-id="d85c4-106">Power BI</span><span class="sxs-lookup"><span data-stu-id="d85c4-106">Power BI</span></span>
* <span data-ttu-id="d85c4-107">Фабрика данных Azure</span><span class="sxs-lookup"><span data-stu-id="d85c4-107">Azure Data Factory</span></span>
* <span data-ttu-id="d85c4-108">Машинное обучение Azure</span><span class="sxs-lookup"><span data-stu-id="d85c4-108">Azure Machine Learning</span></span>
* <span data-ttu-id="d85c4-109">Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d85c4-109">Azure Stream Analytics</span></span>

<span data-ttu-id="d85c4-110">Мы активно работаем над tooconnect с дополнительные службы по hello Azure экосистемы.</span><span class="sxs-lookup"><span data-stu-id="d85c4-110">We are working tooconnect with more services across hello Azure ecosystem.</span></span>

## <a name="power-bi"></a><span data-ttu-id="d85c4-111">Power BI</span><span class="sxs-lookup"><span data-stu-id="d85c4-111">Power BI</span></span>
<span data-ttu-id="d85c4-112">Интеграция с Power BI позволяет tooleverage hello вычислительной мощности хранилища данных SQL с hello динамические отчеты и визуализации Power BI.</span><span class="sxs-lookup"><span data-stu-id="d85c4-112">Power BI integration allows you tooleverage hello compute power of SQL Data Warehouse with hello dynamic reporting and visualization of Power BI.</span></span> <span data-ttu-id="d85c4-113">На данный момент интеграция с Power BI включает:</span><span class="sxs-lookup"><span data-stu-id="d85c4-113">Power BI integration currently includes:</span></span>

* <span data-ttu-id="d85c4-114">**Прямое соединение**: расширенное соединение с логической опорой на хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="d85c4-114">**Direct Connect**: A more advanced connection with logical pushdown against SQL Data Warehouse.</span></span>  <span data-ttu-id="d85c4-115">Это обеспечивает более быстрый анализ в большем масштабе.</span><span class="sxs-lookup"><span data-stu-id="d85c4-115">This provides faster analysis on a larger scale.</span></span>
* <span data-ttu-id="d85c4-116">**Открыть в Power BI**: кнопка «Открыть в Power BI» hello передает экземпляр сведения tooPower бизнес-Аналитики, что обеспечивает более эффективное подключение.</span><span class="sxs-lookup"><span data-stu-id="d85c4-116">**Open in Power BI**: hello 'Open in Power BI' button passes instance information tooPower BI, allowing for a more seamless connection.</span></span>

<span data-ttu-id="d85c4-117">В разделе [интеграция с Power BI](sql-data-warehouse-integrate-power-bi.md) или hello [документации по Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="d85c4-117">See [Integrate with Power BI](sql-data-warehouse-integrate-power-bi.md) or hello [Power BI documentation](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx) for more information.</span></span>

## <a name="azure-data-factory"></a><span data-ttu-id="d85c4-118">Фабрика данных Azure</span><span class="sxs-lookup"><span data-stu-id="d85c4-118">Azure Data Factory</span></span>
<span data-ttu-id="d85c4-119">Фабрика данных Azure предоставляет пользователям toocreate управляемой платформы, которые конвейеров сложных извлечения и загрузки.</span><span class="sxs-lookup"><span data-stu-id="d85c4-119">Azure Data Factory gives users a managed platform toocreate complex Extract-Load pipelines.</span></span>  <span data-ttu-id="d85c4-120">Интеграция хранилища данных SQL с фабрикой данных Azure включает hello следующее:</span><span class="sxs-lookup"><span data-stu-id="d85c4-120">SQL Data Warehouse's integration with Azure Data Factory includes hello following:</span></span>

* <span data-ttu-id="d85c4-121">**Хранимые процедуры**: координировать hello выполнение хранимых процедур в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="d85c4-121">**Stored Procedures**: Orchestrate hello execution of stored procedures on SQL Data Warehouse.</span></span>
* <span data-ttu-id="d85c4-122">**Копировать**: используйте ADF toomove данных в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="d85c4-122">**Copy**: Use ADF toomove data into SQL Data Warehouse.</span></span>  <span data-ttu-id="d85c4-123">Эта операция может использовать механизм перемещения ADF стандартные данные или охватывает PolyBase под hello.</span><span class="sxs-lookup"><span data-stu-id="d85c4-123">This operation can use ADF's standard data movement mechanism or PolyBase under hello covers.</span></span> 

<span data-ttu-id="d85c4-124">В разделе [интеграция с фабрикой данных Azure](sql-data-warehouse-integrate-azure-data-factory.md) или hello [фабрики данных Azure документации](https://azure.microsoft.com/documentation/services/data-factory/) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="d85c4-124">See [Integrate with Azure Data Factory](sql-data-warehouse-integrate-azure-data-factory.md) or hello [Azure Data Factory documentation](https://azure.microsoft.com/documentation/services/data-factory/) for more information.</span></span>

## <a name="azure-machine-learning"></a><span data-ttu-id="d85c4-125">Машинное обучение Azure</span><span class="sxs-lookup"><span data-stu-id="d85c4-125">Azure Machine Learning</span></span>
<span data-ttu-id="d85c4-126">Машинное обучение Azure — это служба полностью управляемая аналитика, что дает возможность пользователям toocreate сложные модели, используя большого набора средств для прогнозирующего.</span><span class="sxs-lookup"><span data-stu-id="d85c4-126">Azure Machine Learning is a fully managed analytics service which allows users toocreate intricate models leveraging a large set of predictive tools.</span></span>  <span data-ttu-id="d85c4-127">Хранилище данных SQL поддерживается в качестве источника и назначения для этих моделей с hello следующие функциональные возможности:</span><span class="sxs-lookup"><span data-stu-id="d85c4-127">SQL Data Warehouse is supported as both a source and destination for these models with hello following functionality:</span></span>

* <span data-ttu-id="d85c4-128">**Чтение данных:** масштабное использование моделей с помощью T-SQL в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="d85c4-128">**Read Data:** Drive models at scale using T-SQL against SQL Data Warehouse.</span></span>
* <span data-ttu-id="d85c4-129">**Записи данных:** фиксации изменений из любой модели обратно tooSQL хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="d85c4-129">**Write Data:** Commit changes from any model back tooSQL Data Warehouse.</span></span>

<span data-ttu-id="d85c4-130">В разделе [интеграция с машинного обучения Azure](sql-data-warehouse-integrate-azure-machine-learning.md) или hello [документации машинного обучения Azure](https://azure.microsoft.com/services/machine-learning/) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="d85c4-130">See [Integrate with Azure Machine Learning](sql-data-warehouse-integrate-azure-machine-learning.md) or hello [Azure Machine Learning documentation](https://azure.microsoft.com/services/machine-learning/) for more information.</span></span>

## <a name="azure-stream-analytics"></a><span data-ttu-id="d85c4-131">Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d85c4-131">Azure Stream Analytics</span></span>
<span data-ttu-id="d85c4-132">Azure Stream Analytics — это сложная полностью управляемая инфраструктура для обработки и потребления данных о событиях, создаваемых концентратором событий Azure.</span><span class="sxs-lookup"><span data-stu-id="d85c4-132">Azure Stream Analytics is a complex, fully managed infrastructure for processing and consuming event data generated from Azure Event Hub.</span></span>  <span data-ttu-id="d85c4-133">Интеграция с хранилищем данных SQL поддерживает потоковую передачу данных toobe эффективно обрабатываются и хранятся вместе с реляционных данных. Это позволяет более глубокого более расширенного анализа.</span><span class="sxs-lookup"><span data-stu-id="d85c4-133">Integration with SQL Data Warehouse allows for streaming data toobe effectively processed and stored alongside relational data enabling deeper, more advanced analysis.</span></span>  

* <span data-ttu-id="d85c4-134">**Выходные данные задания:** отправки выходных данных Stream Analytics непосредственно заданий tooSQL хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="d85c4-134">**Job Output:** Send output from Stream Analytics jobs directly tooSQL Data Warehouse.</span></span>

<span data-ttu-id="d85c4-135">В разделе [интеграция с Azure Stream Analytics](sql-data-warehouse-integrate-azure-stream-analytics.md) или hello [документации Azure Stream Analytics](https://azure.microsoft.com/documentation/services/stream-analytics/) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="d85c4-135">See [Integrate with Azure Stream Analytics](sql-data-warehouse-integrate-azure-stream-analytics.md) or hello [Azure Stream Analytics documentation](https://azure.microsoft.com/documentation/services/stream-analytics/) for more information.</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop/

[Azure Data Factory]: sql-data-warehouse-integrate-azure-data-factory.md
[Azure Machine Learning]: sql-data-warehouse-integrate-azure-machine-learning.md
[Azure Stream Analytics]: sql-data-warehouse-integrate-azure-stream-analytics.md
[Power BI]: sql-data-warehouse-integrate-power-bi.md
[Partners]: sql-data-warehouse-partner-business-intelligence.md

<!--MSDN references-->

<!--Other Web references-->
