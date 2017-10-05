---
title: "Прогнозирование исправности автомобиля и манеры вождения с помощью Azure | Документация Майкрософт"
description: "Используйте возможности Cortana Intelligence, чтобы получить прогнозы и актуальную информацию об исправности и манере вождения автомобиля в режиме реального времени."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 09fad60b-2f48-488b-8a7e-47d1f969ec6f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: d202d314c61416cf306f760f93e0a4a88a1ab42b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook"></a><span data-ttu-id="64f3d-103">Сборник решений аналитики телеметрии автомобиля</span><span class="sxs-lookup"><span data-stu-id="64f3d-103">Vehicle telemetry analytics solution playbook</span></span>
<span data-ttu-id="64f3d-104">Из этого **меню** можно открыть разделы сборника тренировочных заданий.</span><span class="sxs-lookup"><span data-stu-id="64f3d-104">This **menu** links to the chapters in this playbook.</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

## <a name="overview"></a><span data-ttu-id="64f3d-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="64f3d-105">Overview</span></span>
<span data-ttu-id="64f3d-106">Суперкомпьютеры переместились из лаборатории в наши гаражи!</span><span class="sxs-lookup"><span data-stu-id="64f3d-106">Super computers have moved out of the lab and are now parked in our garage!</span></span> <span data-ttu-id="64f3d-107">Эти современные автомобили включают множество датчиков, предоставляя им возможность отслеживать и контролировать миллионы событий каждую секунду.</span><span class="sxs-lookup"><span data-stu-id="64f3d-107">These cutting-edge automobiles contain a myriad of sensors, giving them the ability to track and monitor millions of events every second.</span></span> <span data-ttu-id="64f3d-108">Мы ожидаем, что к 2020 году большая часть этих автомобилей будет подключена к Интернету.</span><span class="sxs-lookup"><span data-stu-id="64f3d-108">We expect that by 2020, most of these cars will have been connected to the Internet.</span></span> <span data-ttu-id="64f3d-109">Представьте себе освоение этого огромного количества данных для обеспечения лучшей безопасности, надежности и совершенно новых возможностей.</span><span class="sxs-lookup"><span data-stu-id="64f3d-109">Imagine tapping into this wealth of data to provide greater safety, reliability and a better driving experience!</span></span> <span data-ttu-id="64f3d-110">Корпорация Майкрософт воплотила эту мечту благодаря Cortana Intelligence.</span><span class="sxs-lookup"><span data-stu-id="64f3d-110">Microsoft has made this dream a reality with Cortana Intelligence.</span></span>

<span data-ttu-id="64f3d-111">Cortana Intelligence от корпорации Майкрософт — это полностью управляемое решение для работы с большими данными и расширенной аналитики, которое позволяет выполнять действия на основе обработанных данных.</span><span class="sxs-lookup"><span data-stu-id="64f3d-111">Microsoft’s Cortana Intelligence is a fully managed big data and advanced analytics suite that enables you to transform your data into intelligent action.</span></span> <span data-ttu-id="64f3d-112">Мы хотим представить вам шаблон решения аналитики телеметрии автомобиля Cortana Intelligence.</span><span class="sxs-lookup"><span data-stu-id="64f3d-112">We want to introduce you to the Cortana Intelligence Vehicle Telemetry Analytics Solution Template.</span></span> <span data-ttu-id="64f3d-113">Это решение демонстрирует, как дилеры, производители автомобилей и страховые компании могут использовать возможности Cortana Intelligence, чтобы получать прогнозы и актуальную информацию об исправности автомобиля и манере вождения в реальном времени.</span><span class="sxs-lookup"><span data-stu-id="64f3d-113">This solution demonstrates how car dealerships, automobile manufacturers, and insurance companies can use the capabilities of Cortana Intelligence to gain real-time and predictive insights on vehicle health and driving habits.</span></span> 

<span data-ttu-id="64f3d-114">Данное решение реализуется как [шаблон лямбда-архитектуры](https://en.wikipedia.org/wiki/Lambda_architecture) , демонстрируя полный потенциал платформы Cortana Intelligence для пакетной обработки в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="64f3d-114">The solution is implemented as a [lambda architecture pattern](https://en.wikipedia.org/wiki/Lambda_architecture) showing the full potential of the Cortana Intelligence platform for real-time and batch processing.</span></span> <span data-ttu-id="64f3d-115">Это решение:</span><span class="sxs-lookup"><span data-stu-id="64f3d-115">The solution:</span></span> 

* <span data-ttu-id="64f3d-116">предоставляет симулятор телематики автомобиля;</span><span class="sxs-lookup"><span data-stu-id="64f3d-116">provides a Vehicle Telematics simulator</span></span>
* <span data-ttu-id="64f3d-117">использует концентраторы событий для приема миллионов событий телеметрии имитаций автомобилей в Azure;</span><span class="sxs-lookup"><span data-stu-id="64f3d-117">leverages Event Hubs for ingesting millions of simulated vehicle telemetry events into Azure</span></span> 
* <span data-ttu-id="64f3d-118">использует Stream Analytics для более глубокого анализа работоспособности автомобилей в режиме реального времени;</span><span class="sxs-lookup"><span data-stu-id="64f3d-118">uses Stream Analytics to gain real-time insights on vehicle health</span></span>
* <span data-ttu-id="64f3d-119">сохраняет данные в долговременном хранилище для расширенного пакетного анализа;</span><span class="sxs-lookup"><span data-stu-id="64f3d-119">persists the data into long-term storage for richer batch analytics.</span></span> 
* <span data-ttu-id="64f3d-120">использует преимущества машинного обучения для выявления аномалий в режиме реального времени и пакетную обработку для прогнозирования состояний;</span><span class="sxs-lookup"><span data-stu-id="64f3d-120">takes advantage of Machine Learning for anomaly detection in real-time and batch processing to gain predictive insights.</span></span>
* <span data-ttu-id="64f3d-121">использует HDInsight для преобразования данных, а фабрика данных обеспечивает оркестрацию, планирование, управление ресурсами и мониторинг конвейера пакетной обработки;</span><span class="sxs-lookup"><span data-stu-id="64f3d-121">leverages HDInsight to transform data at scale and Data Factory to handle orchestration, scheduling, resource management, and monitoring of the batch processing pipeline</span></span> 
* <span data-ttu-id="64f3d-122">предоставляет расширенную панель мониторинга, предназначенную для визуализации данных в режиме реального времени и прогнозной аналитики с помощью Power BI.</span><span class="sxs-lookup"><span data-stu-id="64f3d-122">gives this solution a rich dashboard for real-time data and predictive analytics visualizations using Power BI</span></span>

## <a name="architecture"></a><span data-ttu-id="64f3d-123">Архитектура</span><span class="sxs-lookup"><span data-stu-id="64f3d-123">Architecture</span></span>
<span data-ttu-id="64f3d-124">![Схема архитектуры решения](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*Рис. 1. Архитектура решения аналитики телеметрии транспортного средства*</span><span class="sxs-lookup"><span data-stu-id="64f3d-124">![Solution architecture diagram](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*Figure 1 – Vehicle Telemetry Analytics Solution Architecture*</span></span>

<span data-ttu-id="64f3d-125">Это решение включает в себя следующие **компоненты Cortana Intelligence** и демонстрирует их комплексную интеграцию.</span><span class="sxs-lookup"><span data-stu-id="64f3d-125">This solution includes the following **Cortana Intelligence components** and showcases their end to end integration:</span></span>

* <span data-ttu-id="64f3d-126">**Концентраторы событий** принимают миллионы событий телеметрии автомобилей в Azure.</span><span class="sxs-lookup"><span data-stu-id="64f3d-126">**Event Hubs** for ingesting millions of vehicle telemetry events into Azure.</span></span>
* <span data-ttu-id="64f3d-127">**Stream Analytics** получает данные аналитики о работоспособности автомобиля в режиме реального времени и сохраняет их в долговременное хранилище для более детальной пакетной аналитики.</span><span class="sxs-lookup"><span data-stu-id="64f3d-127">**Stream Analytics** for gaining real-time insights on vehicle health and persists that data into long-term storage for richer batch analytics.</span></span>
* <span data-ttu-id="64f3d-128">**Машинное обучение** обнаруживает аномалии в режиме реального времени и выполняет пакетную обработку для прогнозирования состояний.</span><span class="sxs-lookup"><span data-stu-id="64f3d-128">**Machine Learning** for anomaly detection in real-time and batch processing to gain predictive insights.</span></span>
* <span data-ttu-id="64f3d-129">**HDInsight** используется для преобразования данных при масштабировании.</span><span class="sxs-lookup"><span data-stu-id="64f3d-129">**HDInsight** is leveraged to transform data at scale</span></span>
* <span data-ttu-id="64f3d-130">**Фабрика данных** предназначена для координации, планирования и мониторинга конвейера пакетной обработки, а также управления ресурсами.</span><span class="sxs-lookup"><span data-stu-id="64f3d-130">**Data Factory** handles orchestration, scheduling, resource management and monitoring of the batch processing pipeline.</span></span>
* <span data-ttu-id="64f3d-131">**Power BI** предоставляет для этого решения расширенную панель мониторинга для визуализации данных в режиме реального времени и прогнозной аналитики.</span><span class="sxs-lookup"><span data-stu-id="64f3d-131">**Power BI** gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span>

<span data-ttu-id="64f3d-132">Это решение обращается к двум разным **источникам данных**:</span><span class="sxs-lookup"><span data-stu-id="64f3d-132">This solution accesses two different **data sources**:</span></span> 

* <span data-ttu-id="64f3d-133">**Имитированные сигналы автомобиля и диагностики**: имитатор телематики автомобиля выдает диагностическую информацию и сигналы, которые соответствуют состоянию транспортного средства и стилю движения в определенный момент времени.</span><span class="sxs-lookup"><span data-stu-id="64f3d-133">**Simulated vehicle signals and diagnostics**: A vehicle telematics simulator emits diagnostic information and signals that correspond to the state of the vehicle and the driving pattern at a given point in time.</span></span> 
* <span data-ttu-id="64f3d-134">**Каталог автомобилей**: справочный набор данных для сопоставления VIN с моделью автомобиля.</span><span class="sxs-lookup"><span data-stu-id="64f3d-134">**Vehicle catalog**: A reference dataset containing a VIN to model mapping.</span></span>

