---
title: "Обработка событий средствами Stream Analytics в режиме реального времени | Документация Майкрософт"
description: "Узнайте о том, как обрабатывать и анализировать события в режиме реального времени с помощью различных служб Azure."
keywords: "обработка в режиме реального времени, обработка событий, эталонная архитектура"
services: stream-analytics,event-hubs,storage,sql-database
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: 
ms.assetid: 11af48bc-313c-4527-8c80-91088dc9f3c6
ms.service: stream-analytics
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.author: jeffstok
ms.openlocfilehash: b3057be995e551aac0761c3ce40a8dbf828a5f29
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="reference-architecture-real-time-event-processing-with-microsoft-azure-stream-analytics"></a><span data-ttu-id="0a7aa-104">Эталонная архитектура: обработка событий в режиме реального времени средствами Microsoft Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="0a7aa-104">Reference architecture: Real-time event processing with Microsoft Azure Stream Analytics</span></span>
<span data-ttu-id="0a7aa-105">Эталонная архитектура для обработки событий в режиме реального времени с помощью инструментов Azure Stream Analytics определяет общие принципы развертывания решения для потоковой обработки данных в реальном времени в рамках модели «платформа как услуга» (platform as a service, PaaS) на базе службы Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="0a7aa-105">The reference architecture for real-time event processing with Azure Stream Analytics is intended to provide a generic blueprint for deploying a real-time platform as a service (PaaS) stream-processing solution with Microsoft Azure.</span></span>

## <a name="summary"></a><span data-ttu-id="0a7aa-106">Сводка</span><span class="sxs-lookup"><span data-stu-id="0a7aa-106">Summary</span></span>
<span data-ttu-id="0a7aa-107">Традиционно в основе аналитических решений лежат такие функциональные возможности и компоненты, как извлечение, преобразование и загрузка информации, а также хранилища данных, в которые информация заносится до анализа.</span><span class="sxs-lookup"><span data-stu-id="0a7aa-107">Traditionally, analytics solutions have been based on capabilities such as ETL (extract, transform, load) and data warehousing, where data is stored prior to analysis.</span></span> <span data-ttu-id="0a7aa-108">Изменение требований, в том числе повышение скорости поступления данных, привело к тому, что существующая модель себя исчерпала.</span><span class="sxs-lookup"><span data-stu-id="0a7aa-108">Changing requirements, including more rapidly arriving data, are pushing this existing model to the limit.</span></span> <span data-ttu-id="0a7aa-109">Одним из решений является анализ данных в составе динамических потоков перед их сохранением. Эта возможность не нова, однако такой подход не получил широкого распространения во всех направлениях отрасли.</span><span class="sxs-lookup"><span data-stu-id="0a7aa-109">The ability to analyze data within moving streams prior to storage is one solution, and while it is not a new capability, the approach has not been widely adopted across all industry verticals.</span></span> 

<span data-ttu-id="0a7aa-110">Платформа Microsoft Azure предлагает богатый ассортимент аналитических технологий, позволяющих реализовать самые разные сценарии и решения с различными требованиями.</span><span class="sxs-lookup"><span data-stu-id="0a7aa-110">Microsoft Azure provides an extensive catalog of analytics technologies that are capable of supporting an array of different solution scenarios and requirements.</span></span> <span data-ttu-id="0a7aa-111">Выбор оптимальной службы Azure для развертывания комплексного решения может оказаться непростой задачей с учетом всех возможных вариантов.</span><span class="sxs-lookup"><span data-stu-id="0a7aa-111">Selecting which Azure services to deploy for an end-to-end solution can be a challenge given the breadth of offerings.</span></span> <span data-ttu-id="0a7aa-112">В этом документе описаны возможности и принципы взаимодействия различных служб Azure, позволяющих реализовать решение для потоковой обработки событий.</span><span class="sxs-lookup"><span data-stu-id="0a7aa-112">This paper is designed to describe the capabilities and interoperation of the various Azure services that support an event-streaming solution.</span></span> <span data-ttu-id="0a7aa-113">В нем также рассматриваются возможные сценарии эффективного использования этого подхода клиентами.</span><span class="sxs-lookup"><span data-stu-id="0a7aa-113">It also explains some of the scenarios in which customers can benefit from this type of approach.</span></span>

## <a name="contents"></a><span data-ttu-id="0a7aa-114">Оглавление</span><span class="sxs-lookup"><span data-stu-id="0a7aa-114">Contents</span></span>
* <span data-ttu-id="0a7aa-115">Аннотация</span><span class="sxs-lookup"><span data-stu-id="0a7aa-115">Executive Summary</span></span>
* <span data-ttu-id="0a7aa-116">Общие сведения об аналитике в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="0a7aa-116">Introduction to Real-Time Analytics</span></span>
* <span data-ttu-id="0a7aa-117">Ценность средств Azure для работы с данными в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="0a7aa-117">Value Proposition of Real-Time Data in Azure</span></span>
* <span data-ttu-id="0a7aa-118">Распространенные сценарии применения средств аналитики в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="0a7aa-118">Common Scenarios for Real-Time Analytics</span></span>
* <span data-ttu-id="0a7aa-119">Архитектура и компоненты</span><span class="sxs-lookup"><span data-stu-id="0a7aa-119">Architecture and Components</span></span>
  * <span data-ttu-id="0a7aa-120">Источники данных</span><span class="sxs-lookup"><span data-stu-id="0a7aa-120">Data Sources</span></span>
  * <span data-ttu-id="0a7aa-121">Уровень интеграции данных</span><span class="sxs-lookup"><span data-stu-id="0a7aa-121">Data-Integration Layer</span></span>
  * <span data-ttu-id="0a7aa-122">Уровень аналитики в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="0a7aa-122">Real-time Analytics Layer</span></span>
  * <span data-ttu-id="0a7aa-123">Уровень хранения данных</span><span class="sxs-lookup"><span data-stu-id="0a7aa-123">Data Storage Layer</span></span>
  * <span data-ttu-id="0a7aa-124">Уровень представления или потребления</span><span class="sxs-lookup"><span data-stu-id="0a7aa-124">Presentation / Consumption Layer</span></span>
* <span data-ttu-id="0a7aa-125">Заключение</span><span class="sxs-lookup"><span data-stu-id="0a7aa-125">Conclusion</span></span>

<span data-ttu-id="0a7aa-126">**Автор:** Чарльз Феддерсен (Charles Feddersen), архитектор решений, Научно-инновационный центр анализа данных (Data Insights Center of Excellence), корпорация Майкрософт</span><span class="sxs-lookup"><span data-stu-id="0a7aa-126">**Author:** Charles Feddersen, Solution Architect, Data Insights Center of Excellence, Microsoft Corporation</span></span>

<span data-ttu-id="0a7aa-127">**Опубликовано:** январь 2015 г.</span><span class="sxs-lookup"><span data-stu-id="0a7aa-127">**Published:** January 2015</span></span>

<span data-ttu-id="0a7aa-128">**Версия:** 1.0</span><span class="sxs-lookup"><span data-stu-id="0a7aa-128">**Revision:** 1.0</span></span>

<span data-ttu-id="0a7aa-129">**Ссылка для загрузки:** [Обработка событий в режиме реального времени средствами Microsoft Azure Stream Analytics](http://download.microsoft.com/download/6/2/3/623924DE-B083-4561-9624-C1AB62B5F82B/real-time-event-processing-with-microsoft-azure-stream-analytics.pdf)</span><span class="sxs-lookup"><span data-stu-id="0a7aa-129">**Download:** [Real-Time Event Processing with Microsoft Azure Stream Analytics](http://download.microsoft.com/download/6/2/3/623924DE-B083-4561-9624-C1AB62B5F82B/real-time-event-processing-with-microsoft-azure-stream-analytics.pdf)</span></span>

## <a name="get-help"></a><span data-ttu-id="0a7aa-130">Справка</span><span class="sxs-lookup"><span data-stu-id="0a7aa-130">Get help</span></span>
<span data-ttu-id="0a7aa-131">Дополнительную помощь и поддержку вы можете получить на нашем [форуме Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="0a7aa-131">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a7aa-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0a7aa-132">Next steps</span></span>
* [<span data-ttu-id="0a7aa-133">Введение в Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="0a7aa-133">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="0a7aa-134">Приступая к работе с Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="0a7aa-134">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="0a7aa-135">Масштабирование заданий в службе Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="0a7aa-135">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="0a7aa-136">Справочник по языку запросов Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="0a7aa-136">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="0a7aa-137">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="0a7aa-137">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

