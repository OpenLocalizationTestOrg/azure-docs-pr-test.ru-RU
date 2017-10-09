---
title: "событие aaaReal во время обработки с обработкой событий Stream Analytics | Документы Microsoft"
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
ms.openlocfilehash: a43c503d709609ba61e9932822d30bc2208906ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="reference-architecture-real-time-event-processing-with-microsoft-azure-stream-analytics"></a><span data-ttu-id="29836-104">Эталонная архитектура: обработка событий в режиме реального времени средствами Microsoft Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="29836-104">Reference architecture: Real-time event processing with Microsoft Azure Stream Analytics</span></span>
<span data-ttu-id="29836-105">Эталонная архитектура Hello для событий в реальном времени обработки при помощи Azure Stream Analytics — предполагаемого tooprovide универсальный проект для развертывания в режиме реального времени платформы как услуги (PaaS) решение обработки потока с помощью Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="29836-105">hello reference architecture for real-time event processing with Azure Stream Analytics is intended tooprovide a generic blueprint for deploying a real-time platform as a service (PaaS) stream-processing solution with Microsoft Azure.</span></span>

## <a name="summary"></a><span data-ttu-id="29836-106">Сводка</span><span class="sxs-lookup"><span data-stu-id="29836-106">Summary</span></span>
<span data-ttu-id="29836-107">В большинстве случаев аналитические решения основанными на возможности, такие как ETL (extract, transform, нагрузки) и хранения данных, где tooanalysis хранимых предыдущих данных.</span><span class="sxs-lookup"><span data-stu-id="29836-107">Traditionally, analytics solutions have been based on capabilities such as ETL (extract, transform, load) and data warehousing, where data is stored prior tooanalysis.</span></span> <span data-ttu-id="29836-108">Изменяющимся требованиям, включая дополнительные быстро поступающие данные, уже не хватает предела toohello существующей модели.</span><span class="sxs-lookup"><span data-stu-id="29836-108">Changing requirements, including more rapidly arriving data, are pushing this existing model toohello limit.</span></span> <span data-ttu-id="29836-109">данные tooanalyze возможность Hello внутри скользящего предыдущих toostorage потоки одного решения и пока не является новой возможностью, подход hello не было широко приняла через все отраслевых вертикалях.</span><span class="sxs-lookup"><span data-stu-id="29836-109">hello ability tooanalyze data within moving streams prior toostorage is one solution, and while it is not a new capability, hello approach has not been widely adopted across all industry verticals.</span></span> 

<span data-ttu-id="29836-110">Платформа Microsoft Azure предлагает богатый ассортимент аналитических технологий, позволяющих реализовать самые разные сценарии и решения с различными требованиями.</span><span class="sxs-lookup"><span data-stu-id="29836-110">Microsoft Azure provides an extensive catalog of analytics technologies that are capable of supporting an array of different solution scenarios and requirements.</span></span> <span data-ttu-id="29836-111">Выбор, какой toodeploy служб Azure для решения конца в конец может оказаться сложной задачей, учитывая hello спектр предложений.</span><span class="sxs-lookup"><span data-stu-id="29836-111">Selecting which Azure services toodeploy for an end-to-end solution can be a challenge given hello breadth of offerings.</span></span> <span data-ttu-id="29836-112">Этот документ предназначен возможности спроектированный toodescribe hello и взаимодействие hello различных служб Azure, которые поддерживают решение для потоковой передачи событий.</span><span class="sxs-lookup"><span data-stu-id="29836-112">This paper is designed toodescribe hello capabilities and interoperation of hello various Azure services that support an event-streaming solution.</span></span> <span data-ttu-id="29836-113">Здесь также описываются некоторые сценарии hello, в которых клиенты могут использовать преимущества такой подход.</span><span class="sxs-lookup"><span data-stu-id="29836-113">It also explains some of hello scenarios in which customers can benefit from this type of approach.</span></span>

## <a name="contents"></a><span data-ttu-id="29836-114">Оглавление</span><span class="sxs-lookup"><span data-stu-id="29836-114">Contents</span></span>
* <span data-ttu-id="29836-115">Аннотация</span><span class="sxs-lookup"><span data-stu-id="29836-115">Executive Summary</span></span>
* <span data-ttu-id="29836-116">Аналитика времени tooReal введение</span><span class="sxs-lookup"><span data-stu-id="29836-116">Introduction tooReal-Time Analytics</span></span>
* <span data-ttu-id="29836-117">Ценность средств Azure для работы с данными в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="29836-117">Value Proposition of Real-Time Data in Azure</span></span>
* <span data-ttu-id="29836-118">Распространенные сценарии применения средств аналитики в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="29836-118">Common Scenarios for Real-Time Analytics</span></span>
* <span data-ttu-id="29836-119">Архитектура и компоненты</span><span class="sxs-lookup"><span data-stu-id="29836-119">Architecture and Components</span></span>
  * <span data-ttu-id="29836-120">Источники данных</span><span class="sxs-lookup"><span data-stu-id="29836-120">Data Sources</span></span>
  * <span data-ttu-id="29836-121">Уровень интеграции данных</span><span class="sxs-lookup"><span data-stu-id="29836-121">Data-Integration Layer</span></span>
  * <span data-ttu-id="29836-122">Уровень аналитики в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="29836-122">Real-time Analytics Layer</span></span>
  * <span data-ttu-id="29836-123">Уровень хранения данных</span><span class="sxs-lookup"><span data-stu-id="29836-123">Data Storage Layer</span></span>
  * <span data-ttu-id="29836-124">Уровень представления или потребления</span><span class="sxs-lookup"><span data-stu-id="29836-124">Presentation / Consumption Layer</span></span>
* <span data-ttu-id="29836-125">Заключение</span><span class="sxs-lookup"><span data-stu-id="29836-125">Conclusion</span></span>

<span data-ttu-id="29836-126">**Автор:** Чарльз Феддерсен (Charles Feddersen), архитектор решений, Научно-инновационный центр анализа данных (Data Insights Center of Excellence), корпорация Майкрософт</span><span class="sxs-lookup"><span data-stu-id="29836-126">**Author:** Charles Feddersen, Solution Architect, Data Insights Center of Excellence, Microsoft Corporation</span></span>

<span data-ttu-id="29836-127">**Опубликовано:** январь 2015 г.</span><span class="sxs-lookup"><span data-stu-id="29836-127">**Published:** January 2015</span></span>

<span data-ttu-id="29836-128">**Версия:** 1.0</span><span class="sxs-lookup"><span data-stu-id="29836-128">**Revision:** 1.0</span></span>

<span data-ttu-id="29836-129">**Ссылка для загрузки:** [Обработка событий в режиме реального времени средствами Microsoft Azure Stream Analytics](http://download.microsoft.com/download/6/2/3/623924DE-B083-4561-9624-C1AB62B5F82B/real-time-event-processing-with-microsoft-azure-stream-analytics.pdf)</span><span class="sxs-lookup"><span data-stu-id="29836-129">**Download:** [Real-Time Event Processing with Microsoft Azure Stream Analytics](http://download.microsoft.com/download/6/2/3/623924DE-B083-4561-9624-C1AB62B5F82B/real-time-event-processing-with-microsoft-azure-stream-analytics.pdf)</span></span>

## <a name="get-help"></a><span data-ttu-id="29836-130">Справка</span><span class="sxs-lookup"><span data-stu-id="29836-130">Get help</span></span>
<span data-ttu-id="29836-131">Дополнительную помощь и поддержку вы можете получить на нашем [форуме Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="29836-131">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="29836-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="29836-132">Next steps</span></span>
* [<span data-ttu-id="29836-133">Введение tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="29836-133">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="29836-134">Приступая к работе с Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="29836-134">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="29836-135">Масштабирование заданий в службе Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="29836-135">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="29836-136">Справочник по языку запросов Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="29836-136">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="29836-137">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="29836-137">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

