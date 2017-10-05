---
title: "Создание интегрированных решений с помощью хранилища данных SQL | Документация Майкрософт"
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
ms.openlocfilehash: d407c29f99fd7537590ec787febd84a9e3f4f353
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="leverage-other-services-with-sql-data-warehouse"></a><span data-ttu-id="5aabc-103">Интеграция других служб с хранилищем данных SQL</span><span class="sxs-lookup"><span data-stu-id="5aabc-103">Leverage other services with SQL Data Warehouse</span></span>
<span data-ttu-id="5aabc-104">Помимо базовых возможностей, хранилище данных SQL позволяет пользователям дополнительно использовать многие другие службы в Azure.</span><span class="sxs-lookup"><span data-stu-id="5aabc-104">In addition to its core functionality, SQL Data Warehouse enables users to leverage many of the other services in Azure alongside it.</span></span>  <span data-ttu-id="5aabc-105">В частности, мы приняли меры по глубокой интеграции со следующими службами:</span><span class="sxs-lookup"><span data-stu-id="5aabc-105">Specifically, we have currently taken steps to deeply integrate with the following:</span></span>

* <span data-ttu-id="5aabc-106">Power BI</span><span class="sxs-lookup"><span data-stu-id="5aabc-106">Power BI</span></span>
* <span data-ttu-id="5aabc-107">Фабрика данных Azure</span><span class="sxs-lookup"><span data-stu-id="5aabc-107">Azure Data Factory</span></span>
* <span data-ttu-id="5aabc-108">Машинное обучение Azure</span><span class="sxs-lookup"><span data-stu-id="5aabc-108">Azure Machine Learning</span></span>
* <span data-ttu-id="5aabc-109">Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="5aabc-109">Azure Stream Analytics</span></span>

<span data-ttu-id="5aabc-110">Мы работаем над возможностями подключения к большему количеству служб в экосистеме Azure.</span><span class="sxs-lookup"><span data-stu-id="5aabc-110">We are working to connect with more services across the Azure ecosystem.</span></span>

## <a name="power-bi"></a><span data-ttu-id="5aabc-111">Power BI</span><span class="sxs-lookup"><span data-stu-id="5aabc-111">Power BI</span></span>
<span data-ttu-id="5aabc-112">Интеграция с Power BI позволяет использовать вычислительные ресурсы хранилища данных SQL с возможностью создания динамических отчетов и визуализацией Power BI.</span><span class="sxs-lookup"><span data-stu-id="5aabc-112">Power BI integration allows you to leverage the compute power of SQL Data Warehouse with the dynamic reporting and visualization of Power BI.</span></span> <span data-ttu-id="5aabc-113">На данный момент интеграция с Power BI включает:</span><span class="sxs-lookup"><span data-stu-id="5aabc-113">Power BI integration currently includes:</span></span>

* <span data-ttu-id="5aabc-114">**Прямое соединение**: расширенное соединение с логической опорой на хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="5aabc-114">**Direct Connect**: A more advanced connection with logical pushdown against SQL Data Warehouse.</span></span>  <span data-ttu-id="5aabc-115">Это обеспечивает более быстрый анализ в большем масштабе.</span><span class="sxs-lookup"><span data-stu-id="5aabc-115">This provides faster analysis on a larger scale.</span></span>
* <span data-ttu-id="5aabc-116">**Открыть в Power BI**: кнопка "Открыть в Power BI" передает сведения об экземпляре в Power BI, повышая надежность соединения.</span><span class="sxs-lookup"><span data-stu-id="5aabc-116">**Open in Power BI**: The 'Open in Power BI' button passes instance information to Power BI, allowing for a more seamless connection.</span></span>

<span data-ttu-id="5aabc-117">Дополнительные сведения см. в статье [Использование Power BI с хранилищем данных SQL](sql-data-warehouse-integrate-power-bi.md) или в [документации по Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx).</span><span class="sxs-lookup"><span data-stu-id="5aabc-117">See [Integrate with Power BI](sql-data-warehouse-integrate-power-bi.md) or the [Power BI documentation](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx) for more information.</span></span>

## <a name="azure-data-factory"></a><span data-ttu-id="5aabc-118">Фабрика данных Azure</span><span class="sxs-lookup"><span data-stu-id="5aabc-118">Azure Data Factory</span></span>
<span data-ttu-id="5aabc-119">Фабрика данных Azure предоставляет пользователям управляемую платформу для создания сложных конвейеров извлечения и загрузки.</span><span class="sxs-lookup"><span data-stu-id="5aabc-119">Azure Data Factory gives users a managed platform to create complex Extract-Load pipelines.</span></span>  <span data-ttu-id="5aabc-120">Интеграция хранилища данных SQL с фабрикой данных Azure включает следующее.</span><span class="sxs-lookup"><span data-stu-id="5aabc-120">SQL Data Warehouse's integration with Azure Data Factory includes the following:</span></span>

* <span data-ttu-id="5aabc-121">**Хранимые процедуры**: управление выполнением хранимых процедур в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="5aabc-121">**Stored Procedures**: Orchestrate the execution of stored procedures on SQL Data Warehouse.</span></span>
* <span data-ttu-id="5aabc-122">**Действие копирования.** Используйте ADF для перемещения данных в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="5aabc-122">**Copy**: Use ADF to move data into SQL Data Warehouse.</span></span>  <span data-ttu-id="5aabc-123">В основе этой операции может использоваться стандартный механизм перемещения данных ADF или PolyBase.</span><span class="sxs-lookup"><span data-stu-id="5aabc-123">This operation can use ADF's standard data movement mechanism or PolyBase under the covers.</span></span> 

<span data-ttu-id="5aabc-124">Дополнительные сведения см. в статье [Работа с фабрикой данных Azure и хранилищем данных SQL](sql-data-warehouse-integrate-azure-data-factory.md) или в [документации по фабрике данных Azure](https://azure.microsoft.com/documentation/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="5aabc-124">See [Integrate with Azure Data Factory](sql-data-warehouse-integrate-azure-data-factory.md) or the [Azure Data Factory documentation](https://azure.microsoft.com/documentation/services/data-factory/) for more information.</span></span>

## <a name="azure-machine-learning"></a><span data-ttu-id="5aabc-125">Машинное обучение Azure</span><span class="sxs-lookup"><span data-stu-id="5aabc-125">Azure Machine Learning</span></span>
<span data-ttu-id="5aabc-126">Машинное обучение Azure — это полностью управляемая аналитическая служба, позволяющая пользователям создавать сложные модели с использованием крупного набора прогнозируемых инструментов.</span><span class="sxs-lookup"><span data-stu-id="5aabc-126">Azure Machine Learning is a fully managed analytics service which allows users to create intricate models leveraging a large set of predictive tools.</span></span>  <span data-ttu-id="5aabc-127">Хранилище данных SQL поддерживается в качестве источника и цели для этих моделей со следующими возможностями.</span><span class="sxs-lookup"><span data-stu-id="5aabc-127">SQL Data Warehouse is supported as both a source and destination for these models with the following functionality:</span></span>

* <span data-ttu-id="5aabc-128">**Чтение данных:** масштабное использование моделей с помощью T-SQL в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="5aabc-128">**Read Data:** Drive models at scale using T-SQL against SQL Data Warehouse.</span></span>
* <span data-ttu-id="5aabc-129">**Запись данных:** применение изменений любой модели в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="5aabc-129">**Write Data:** Commit changes from any model back to SQL Data Warehouse.</span></span>

<span data-ttu-id="5aabc-130">Дополнительные сведения см. в статье [Использование машинного обучения Azure с хранилищем данных SQL](sql-data-warehouse-integrate-azure-machine-learning.md) или в [документации по машинному обучению Azure](https://azure.microsoft.com/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="5aabc-130">See [Integrate with Azure Machine Learning](sql-data-warehouse-integrate-azure-machine-learning.md) or the [Azure Machine Learning documentation](https://azure.microsoft.com/services/machine-learning/) for more information.</span></span>

## <a name="azure-stream-analytics"></a><span data-ttu-id="5aabc-131">Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="5aabc-131">Azure Stream Analytics</span></span>
<span data-ttu-id="5aabc-132">Azure Stream Analytics — это сложная полностью управляемая инфраструктура для обработки и потребления данных о событиях, создаваемых концентратором событий Azure.</span><span class="sxs-lookup"><span data-stu-id="5aabc-132">Azure Stream Analytics is a complex, fully managed infrastructure for processing and consuming event data generated from Azure Event Hub.</span></span>  <span data-ttu-id="5aabc-133">Интеграция с хранилищем данных SQL обеспечивает эффективную обработку и хранение потоковых данных наряду с реляционными данными, предоставляя более глубокий и расширенный анализ.</span><span class="sxs-lookup"><span data-stu-id="5aabc-133">Integration with SQL Data Warehouse allows for streaming data to be effectively processed and stored alongside relational data enabling deeper, more advanced analysis.</span></span>  

* <span data-ttu-id="5aabc-134">**Выходные данные заданий:** отправка выходных данных заданий Stream Analytics напрямую в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="5aabc-134">**Job Output:** Send output from Stream Analytics jobs directly to SQL Data Warehouse.</span></span>

<span data-ttu-id="5aabc-135">Дополнительные сведения см. в статье [Работа со службой Azure Stream Analytics и хранилищем данных SQL](sql-data-warehouse-integrate-azure-stream-analytics.md) или в [документации по Azure Stream Analytics](https://azure.microsoft.com/documentation/services/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="5aabc-135">See [Integrate with Azure Stream Analytics](sql-data-warehouse-integrate-azure-stream-analytics.md) or the [Azure Stream Analytics documentation](https://azure.microsoft.com/documentation/services/stream-analytics/) for more information.</span></span>

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
