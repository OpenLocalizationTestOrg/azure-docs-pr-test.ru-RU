---
title: "Модель данных телеметрии Azure Application Insights — телеметрия зависимостей | Документы Майкрософт"
description: "Модель данных Application Insights для телеметрии зависимостей"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/17/2017
ms.author: bwren
ms.openlocfilehash: 2e97c3f951f46c32802aea543b93d5ab1bb76228
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="dependency-telemetry-application-insights-data-model"></a><span data-ttu-id="37ba8-103">Телеметрия зависимостей: модель данных Application Insights</span><span class="sxs-lookup"><span data-stu-id="37ba8-103">Dependency telemetry: Application Insights data model</span></span>

<span data-ttu-id="37ba8-104">Телеметрия зависимостей (в [Application Insights](app-insights-overview.md)) представляет взаимодействие отслеживаемого компонента с удаленным, таким как SQL или конечная точка HTTP.</span><span class="sxs-lookup"><span data-stu-id="37ba8-104">Dependency Telemetry (in [Application Insights](app-insights-overview.md)) represents an interaction of the monitored component with a remote component such as SQL or an HTTP endpoint.</span></span>

## <a name="name"></a><span data-ttu-id="37ba8-105">Имя</span><span class="sxs-lookup"><span data-stu-id="37ba8-105">Name</span></span>

<span data-ttu-id="37ba8-106">Имя команды, инициированной этим вызовом зависимости.</span><span class="sxs-lookup"><span data-stu-id="37ba8-106">Name of the command initiated with this dependency call.</span></span> <span data-ttu-id="37ba8-107">Низкое значение кратности.</span><span class="sxs-lookup"><span data-stu-id="37ba8-107">Low cardinality value.</span></span> <span data-ttu-id="37ba8-108">Примерами являются имя хранимой процедуры и шаблон пути URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="37ba8-108">Examples are stored procedure name and URL path template.</span></span>

## <a name="id"></a><span data-ttu-id="37ba8-109">ИД</span><span class="sxs-lookup"><span data-stu-id="37ba8-109">ID</span></span>

<span data-ttu-id="37ba8-110">Идентификатор для экземпляра вызова зависимости.</span><span class="sxs-lookup"><span data-stu-id="37ba8-110">Identifier of a dependency call instance.</span></span> <span data-ttu-id="37ba8-111">Используется для корреляции с элементом телеметрии запроса, соответствующим этому вызову зависимости.</span><span class="sxs-lookup"><span data-stu-id="37ba8-111">Used for correlation with the request telemetry item corresponding to this dependency call.</span></span> <span data-ttu-id="37ba8-112">Дополнительные сведения см. на странице [корреляции](application-insights-correlation.md).</span><span class="sxs-lookup"><span data-stu-id="37ba8-112">For more information, see [correlation](application-insights-correlation.md) page.</span></span>

## <a name="data"></a><span data-ttu-id="37ba8-113">Данные</span><span class="sxs-lookup"><span data-stu-id="37ba8-113">Data</span></span>

<span data-ttu-id="37ba8-114">Команда, инициированная этим вызовом зависимости.</span><span class="sxs-lookup"><span data-stu-id="37ba8-114">Command initiated by this dependency call.</span></span> <span data-ttu-id="37ba8-115">Примерами являются оператор SQL и HTTP URL со всеми параметрами запроса.</span><span class="sxs-lookup"><span data-stu-id="37ba8-115">Examples are SQL statement and HTTP URL with all query parameters.</span></span>

## <a name="type"></a><span data-ttu-id="37ba8-116">Тип</span><span class="sxs-lookup"><span data-stu-id="37ba8-116">Type</span></span>

<span data-ttu-id="37ba8-117">Имя типа зависимости.</span><span class="sxs-lookup"><span data-stu-id="37ba8-117">Dependency type name.</span></span> <span data-ttu-id="37ba8-118">Низкое значение кратности для логической группировки зависимостей и интерпретации других полей, таких как commandName и resultCode.</span><span class="sxs-lookup"><span data-stu-id="37ba8-118">Low cardinality value for logical grouping of dependencies and interpretation of other fields like commandName and resultCode.</span></span> <span data-ttu-id="37ba8-119">Примерами являются SQL, таблица Azure и HTTP.</span><span class="sxs-lookup"><span data-stu-id="37ba8-119">Examples are SQL, Azure table, and HTTP.</span></span>

## <a name="target"></a><span data-ttu-id="37ba8-120">Цель</span><span class="sxs-lookup"><span data-stu-id="37ba8-120">Target</span></span>

<span data-ttu-id="37ba8-121">Целевой сайт вызова зависимости.</span><span class="sxs-lookup"><span data-stu-id="37ba8-121">Target site of a dependency call.</span></span> <span data-ttu-id="37ba8-122">Примерами являются имя сервера, адрес узла.</span><span class="sxs-lookup"><span data-stu-id="37ba8-122">Examples are server name, host address.</span></span> <span data-ttu-id="37ba8-123">Дополнительные сведения см. на странице [корреляции](application-insights-correlation.md).</span><span class="sxs-lookup"><span data-stu-id="37ba8-123">For more information, see [correlation](application-insights-correlation.md) page.</span></span>

## <a name="duration"></a><span data-ttu-id="37ba8-124">Длительность</span><span class="sxs-lookup"><span data-stu-id="37ba8-124">Duration</span></span>

<span data-ttu-id="37ba8-125">Длительность запроса в формате: `DD.HH:MM:SS.MMMMMM`.</span><span class="sxs-lookup"><span data-stu-id="37ba8-125">Request duration in format: `DD.HH:MM:SS.MMMMMM`.</span></span> <span data-ttu-id="37ba8-126">Должно быть меньше `1000` дн.</span><span class="sxs-lookup"><span data-stu-id="37ba8-126">Must be less than `1000` days.</span></span>

## <a name="result-code"></a><span data-ttu-id="37ba8-127">Код результата</span><span class="sxs-lookup"><span data-stu-id="37ba8-127">Result code</span></span>

<span data-ttu-id="37ba8-128">Код результата для вызова зависимости.</span><span class="sxs-lookup"><span data-stu-id="37ba8-128">Result code of a dependency call.</span></span> <span data-ttu-id="37ba8-129">Примерами являются код ошибки SQL и код состояния HTTP.</span><span class="sxs-lookup"><span data-stu-id="37ba8-129">Examples are SQL error code and HTTP status code.</span></span>

## <a name="success"></a><span data-ttu-id="37ba8-130">Успешно</span><span class="sxs-lookup"><span data-stu-id="37ba8-130">Success</span></span>

<span data-ttu-id="37ba8-131">Указание того, был ли вызов успешным.</span><span class="sxs-lookup"><span data-stu-id="37ba8-131">Indication of successful or unsuccessful call.</span></span>

## <a name="custom-properties"></a><span data-ttu-id="37ba8-132">Пользовательские свойства</span><span class="sxs-lookup"><span data-stu-id="37ba8-132">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="37ba8-133">Пользовательские измерения</span><span class="sxs-lookup"><span data-stu-id="37ba8-133">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]


## <a name="next-steps"></a><span data-ttu-id="37ba8-134">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="37ba8-134">Next steps</span></span>

- <span data-ttu-id="37ba8-135">Настройка отслеживания зависимостей для платформы [.NET](app-insights-asp-net-dependencies.md)</span><span class="sxs-lookup"><span data-stu-id="37ba8-135">Set up dependency tracking for [.NET](app-insights-asp-net-dependencies.md).</span></span>
- <span data-ttu-id="37ba8-136">Настройка отслеживания зависимостей для платформы [Java](app-insights-java-agent.md)</span><span class="sxs-lookup"><span data-stu-id="37ba8-136">Set up dependency tracking for [Java](app-insights-java-agent.md).</span></span>
- [<span data-ttu-id="37ba8-137">Создание телеметрии настраиваемых зависимостей</span><span class="sxs-lookup"><span data-stu-id="37ba8-137">Write custom dependency telemetry</span></span>](app-insights-api-custom-events-metrics.md#trackdependency)
- <span data-ttu-id="37ba8-138">В [этой статье](application-insights-data-model.md) представлены типы данных и модель данных для Application Insights.</span><span class="sxs-lookup"><span data-stu-id="37ba8-138">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="37ba8-139">Ознакомление с [платформами](app-insights-platforms.md), поддерживаемыми Application Insights.</span><span class="sxs-lookup"><span data-stu-id="37ba8-139">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
