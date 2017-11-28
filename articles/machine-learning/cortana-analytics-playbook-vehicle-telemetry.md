---
title: "aaaPredict vehicle работоспособности и управление им привычки - Azure | Документы Microsoft"
description: "Использовать возможности hello toogain Cortana аналитики в реальном времени и прогнозной аналитики на автомобиль работоспособности и пешком привычки."
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
ms.openlocfilehash: 54cc890ff39493bc040bb809721388349665720f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook"></a><span data-ttu-id="0197e-103">Сборник решений аналитики телеметрии автомобиля</span><span class="sxs-lookup"><span data-stu-id="0197e-103">Vehicle telemetry analytics solution playbook</span></span>
<span data-ttu-id="0197e-104">Это **меню** toohello главах этого репертуара ссылки.</span><span class="sxs-lookup"><span data-stu-id="0197e-104">This **menu** links toohello chapters in this playbook.</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

## <a name="overview"></a><span data-ttu-id="0197e-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="0197e-105">Overview</span></span>
<span data-ttu-id="0197e-106">Super компьютеров был перемещен из лаборатории hello и теперь выполнены в нерабочем в нашем гараже!</span><span class="sxs-lookup"><span data-stu-id="0197e-106">Super computers have moved out of hello lab and are now parked in our garage!</span></span> <span data-ttu-id="0197e-107">Эти современные автомобили содержат множество датчиков, предоставляя им возможность tootrack hello и отслеживать миллионы события каждую секунду.</span><span class="sxs-lookup"><span data-stu-id="0197e-107">These cutting-edge automobiles contain a myriad of sensors, giving them hello ability tootrack and monitor millions of events every second.</span></span> <span data-ttu-id="0197e-108">Мы предполагаем, что по 2020, большая часть этих машин будет была подключенных toohello Интернета.</span><span class="sxs-lookup"><span data-stu-id="0197e-108">We expect that by 2020, most of these cars will have been connected toohello Internet.</span></span> <span data-ttu-id="0197e-109">Представьте себе освоение массу данных tooprovide повышенной безопасности, надежности и лучше совершенно новые возможности!</span><span class="sxs-lookup"><span data-stu-id="0197e-109">Imagine tapping into this wealth of data tooprovide greater safety, reliability and a better driving experience!</span></span> <span data-ttu-id="0197e-110">Корпорация Майкрософт воплотила эту мечту благодаря Cortana Intelligence.</span><span class="sxs-lookup"><span data-stu-id="0197e-110">Microsoft has made this dream a reality with Cortana Intelligence.</span></span>

<span data-ttu-id="0197e-111">Cortana аналитики корпорации Майкрософт — это полностью управляемая большие данные и advanced analytics suite, обеспечивающий tootransform данных в действие интеллектуальной.</span><span class="sxs-lookup"><span data-stu-id="0197e-111">Microsoft’s Cortana Intelligence is a fully managed big data and advanced analytics suite that enables you tootransform your data into intelligent action.</span></span> <span data-ttu-id="0197e-112">Мы хотим toointroduce toohello Cortana аналитики транспортных средств телеметрии Analytics шаблон решения.</span><span class="sxs-lookup"><span data-stu-id="0197e-112">We want toointroduce you toohello Cortana Intelligence Vehicle Telemetry Analytics Solution Template.</span></span> <span data-ttu-id="0197e-113">Это решение демонстрирует дилеров автомобиля, автомобиль производители и страховых компаний можно использовать возможности hello toogain Cortana аналитики в реальном времени и привычки прогнозной аналитики на автомобиль работоспособности и управление им.</span><span class="sxs-lookup"><span data-stu-id="0197e-113">This solution demonstrates how car dealerships, automobile manufacturers, and insurance companies can use hello capabilities of Cortana Intelligence toogain real-time and predictive insights on vehicle health and driving habits.</span></span> 

<span data-ttu-id="0197e-114">Hello решение реализуется как [lambda-архитектура шаблон](https://en.wikipedia.org/wiki/Lambda_architecture) hello всеми возможностями платформы аналитики Cortana hello для отображения в режиме реального времени и пакетной обработки.</span><span class="sxs-lookup"><span data-stu-id="0197e-114">hello solution is implemented as a [lambda architecture pattern](https://en.wikipedia.org/wiki/Lambda_architecture) showing hello full potential of hello Cortana Intelligence platform for real-time and batch processing.</span></span> <span data-ttu-id="0197e-115">решение Hello.</span><span class="sxs-lookup"><span data-stu-id="0197e-115">hello solution:</span></span> 

* <span data-ttu-id="0197e-116">предоставляет симулятор телематики автомобиля;</span><span class="sxs-lookup"><span data-stu-id="0197e-116">provides a Vehicle Telematics simulator</span></span>
* <span data-ttu-id="0197e-117">использует концентраторы событий для приема миллионов событий телеметрии имитаций автомобилей в Azure;</span><span class="sxs-lookup"><span data-stu-id="0197e-117">leverages Event Hubs for ingesting millions of simulated vehicle telemetry events into Azure</span></span> 
* <span data-ttu-id="0197e-118">использует поток toogain в режиме реального времени по аналитике на автомобиль работоспособности</span><span class="sxs-lookup"><span data-stu-id="0197e-118">uses Stream Analytics toogain real-time insights on vehicle health</span></span>
* <span data-ttu-id="0197e-119">сохраняет данные hello в долговременном хранилище для расширенную аналитику пакета.</span><span class="sxs-lookup"><span data-stu-id="0197e-119">persists hello data into long-term storage for richer batch analytics.</span></span> 
* <span data-ttu-id="0197e-120">использует машинного обучения для обнаружения аномалий в режиме реального времени и пакетной обработки toogain прогнозной аналитики.</span><span class="sxs-lookup"><span data-stu-id="0197e-120">takes advantage of Machine Learning for anomaly detection in real-time and batch processing toogain predictive insights.</span></span>
* <span data-ttu-id="0197e-121">использует данные tootransform HDInsight на масштаб и orchestration toohandle фабрики данных, планирование, управление ресурсами и мониторинг hello конвейера обработки пакета</span><span class="sxs-lookup"><span data-stu-id="0197e-121">leverages HDInsight tootransform data at scale and Data Factory toohandle orchestration, scheduling, resource management, and monitoring of hello batch processing pipeline</span></span> 
* <span data-ttu-id="0197e-122">предоставляет расширенную панель мониторинга, предназначенную для визуализации данных в режиме реального времени и прогнозной аналитики с помощью Power BI.</span><span class="sxs-lookup"><span data-stu-id="0197e-122">gives this solution a rich dashboard for real-time data and predictive analytics visualizations using Power BI</span></span>

## <a name="architecture"></a><span data-ttu-id="0197e-123">Архитектура</span><span class="sxs-lookup"><span data-stu-id="0197e-123">Architecture</span></span>
<span data-ttu-id="0197e-124">![Схема архитектуры решения](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*Рис. 1. Архитектура решения аналитики телеметрии транспортного средства*</span><span class="sxs-lookup"><span data-stu-id="0197e-124">![Solution architecture diagram](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*Figure 1 – Vehicle Telemetry Analytics Solution Architecture*</span></span>

<span data-ttu-id="0197e-125">Это решение включает в себя следующие hello **компонентов аналитики Cortana** и демонстрирует интеграцию их tooend:</span><span class="sxs-lookup"><span data-stu-id="0197e-125">This solution includes hello following **Cortana Intelligence components** and showcases their end tooend integration:</span></span>

* <span data-ttu-id="0197e-126">**Концентраторы событий** принимают миллионы событий телеметрии автомобилей в Azure.</span><span class="sxs-lookup"><span data-stu-id="0197e-126">**Event Hubs** for ingesting millions of vehicle telemetry events into Azure.</span></span>
* <span data-ttu-id="0197e-127">**Stream Analytics** получает данные аналитики о работоспособности автомобиля в режиме реального времени и сохраняет их в долговременное хранилище для более детальной пакетной аналитики.</span><span class="sxs-lookup"><span data-stu-id="0197e-127">**Stream Analytics** for gaining real-time insights on vehicle health and persists that data into long-term storage for richer batch analytics.</span></span>
* <span data-ttu-id="0197e-128">**Машинное Обучение** для обнаружения аномалий в режиме реального времени и пакетной обработки toogain прогнозной аналитики.</span><span class="sxs-lookup"><span data-stu-id="0197e-128">**Machine Learning** for anomaly detection in real-time and batch processing toogain predictive insights.</span></span>
* <span data-ttu-id="0197e-129">**HDInsight** tootransform использовать данные в масштабе</span><span class="sxs-lookup"><span data-stu-id="0197e-129">**HDInsight** is leveraged tootransform data at scale</span></span>
* <span data-ttu-id="0197e-130">**Фабрика данных** обрабатывает orchestration, планирование, управление ресурсами и мониторинг hello конвейера обработки пакета.</span><span class="sxs-lookup"><span data-stu-id="0197e-130">**Data Factory** handles orchestration, scheduling, resource management and monitoring of hello batch processing pipeline.</span></span>
* <span data-ttu-id="0197e-131">**Power BI** предоставляет для этого решения расширенную панель мониторинга для визуализации данных в режиме реального времени и прогнозной аналитики.</span><span class="sxs-lookup"><span data-stu-id="0197e-131">**Power BI** gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span>

<span data-ttu-id="0197e-132">Это решение обращается к двум разным **источникам данных**:</span><span class="sxs-lookup"><span data-stu-id="0197e-132">This solution accesses two different **data sources**:</span></span> 

* <span data-ttu-id="0197e-133">**Имитируемые vehicle сигналы и диагностика**: vehicle симулятора telematics выдает диагностические данные и сигналы, которые соответствуют toohello состояние hello vehicle и hello пешком шаблон в определенный момент времени.</span><span class="sxs-lookup"><span data-stu-id="0197e-133">**Simulated vehicle signals and diagnostics**: A vehicle telematics simulator emits diagnostic information and signals that correspond toohello state of hello vehicle and hello driving pattern at a given point in time.</span></span> 
* <span data-ttu-id="0197e-134">**Vehicle каталога**: эталонного набора данных, содержащее сопоставление toomodel VIN.</span><span class="sxs-lookup"><span data-stu-id="0197e-134">**Vehicle catalog**: A reference dataset containing a VIN toomodel mapping.</span></span>

