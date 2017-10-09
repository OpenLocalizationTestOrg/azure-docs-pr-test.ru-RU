---
title: "aaaAzure модели данных телеметрии приложения аналитики - телеметрии зависимости | Документы Microsoft"
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
ms.openlocfilehash: cd5ab7c61d3498e4aa2a0aa0c8b0d106a92912e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="dependency-telemetry-application-insights-data-model"></a><span data-ttu-id="417a2-103">Телеметрия зависимостей: модель данных Application Insights</span><span class="sxs-lookup"><span data-stu-id="417a2-103">Dependency telemetry: Application Insights data model</span></span>

<span data-ttu-id="417a2-104">Данные телеметрии зависимостей (в [Application Insights](app-insights-overview.md)) представляет взаимодействие компонента hello отслеживается с удаленного компонента, например SQL или конечной точки HTTP.</span><span class="sxs-lookup"><span data-stu-id="417a2-104">Dependency Telemetry (in [Application Insights](app-insights-overview.md)) represents an interaction of hello monitored component with a remote component such as SQL or an HTTP endpoint.</span></span>

## <a name="name"></a><span data-ttu-id="417a2-105">Имя</span><span class="sxs-lookup"><span data-stu-id="417a2-105">Name</span></span>

<span data-ttu-id="417a2-106">Имя команды hello, этот вызов зависимости для инициализации.</span><span class="sxs-lookup"><span data-stu-id="417a2-106">Name of hello command initiated with this dependency call.</span></span> <span data-ttu-id="417a2-107">Низкое значение кратности.</span><span class="sxs-lookup"><span data-stu-id="417a2-107">Low cardinality value.</span></span> <span data-ttu-id="417a2-108">Примерами являются имя хранимой процедуры и шаблон пути URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="417a2-108">Examples are stored procedure name and URL path template.</span></span>

## <a name="id"></a><span data-ttu-id="417a2-109">ИД</span><span class="sxs-lookup"><span data-stu-id="417a2-109">ID</span></span>

<span data-ttu-id="417a2-110">Идентификатор для экземпляра вызова зависимости.</span><span class="sxs-lookup"><span data-stu-id="417a2-110">Identifier of a dependency call instance.</span></span> <span data-ttu-id="417a2-111">Использовать для корреляции с hello запрос телеметрии элемент, соответствующий вызов toothis зависимости.</span><span class="sxs-lookup"><span data-stu-id="417a2-111">Used for correlation with hello request telemetry item corresponding toothis dependency call.</span></span> <span data-ttu-id="417a2-112">Дополнительные сведения см. на странице [корреляции](application-insights-correlation.md).</span><span class="sxs-lookup"><span data-stu-id="417a2-112">For more information, see [correlation](application-insights-correlation.md) page.</span></span>

## <a name="data"></a><span data-ttu-id="417a2-113">Данные</span><span class="sxs-lookup"><span data-stu-id="417a2-113">Data</span></span>

<span data-ttu-id="417a2-114">Команда, инициированная этим вызовом зависимости.</span><span class="sxs-lookup"><span data-stu-id="417a2-114">Command initiated by this dependency call.</span></span> <span data-ttu-id="417a2-115">Примерами являются оператор SQL и HTTP URL со всеми параметрами запроса.</span><span class="sxs-lookup"><span data-stu-id="417a2-115">Examples are SQL statement and HTTP URL with all query parameters.</span></span>

## <a name="type"></a><span data-ttu-id="417a2-116">Тип</span><span class="sxs-lookup"><span data-stu-id="417a2-116">Type</span></span>

<span data-ttu-id="417a2-117">Имя типа зависимости.</span><span class="sxs-lookup"><span data-stu-id="417a2-117">Dependency type name.</span></span> <span data-ttu-id="417a2-118">Низкое значение кратности для логической группировки зависимостей и интерпретации других полей, таких как commandName и resultCode.</span><span class="sxs-lookup"><span data-stu-id="417a2-118">Low cardinality value for logical grouping of dependencies and interpretation of other fields like commandName and resultCode.</span></span> <span data-ttu-id="417a2-119">Примерами являются SQL, таблица Azure и HTTP.</span><span class="sxs-lookup"><span data-stu-id="417a2-119">Examples are SQL, Azure table, and HTTP.</span></span>

## <a name="target"></a><span data-ttu-id="417a2-120">Цель</span><span class="sxs-lookup"><span data-stu-id="417a2-120">Target</span></span>

<span data-ttu-id="417a2-121">Целевой сайт вызова зависимости.</span><span class="sxs-lookup"><span data-stu-id="417a2-121">Target site of a dependency call.</span></span> <span data-ttu-id="417a2-122">Примерами являются имя сервера, адрес узла.</span><span class="sxs-lookup"><span data-stu-id="417a2-122">Examples are server name, host address.</span></span> <span data-ttu-id="417a2-123">Дополнительные сведения см. на странице [корреляции](application-insights-correlation.md).</span><span class="sxs-lookup"><span data-stu-id="417a2-123">For more information, see [correlation](application-insights-correlation.md) page.</span></span>

## <a name="duration"></a><span data-ttu-id="417a2-124">Длительность</span><span class="sxs-lookup"><span data-stu-id="417a2-124">Duration</span></span>

<span data-ttu-id="417a2-125">Длительность запроса в формате: `DD.HH:MM:SS.MMMMMM`.</span><span class="sxs-lookup"><span data-stu-id="417a2-125">Request duration in format: `DD.HH:MM:SS.MMMMMM`.</span></span> <span data-ttu-id="417a2-126">Должно быть меньше `1000` дн.</span><span class="sxs-lookup"><span data-stu-id="417a2-126">Must be less than `1000` days.</span></span>

## <a name="result-code"></a><span data-ttu-id="417a2-127">Код результата</span><span class="sxs-lookup"><span data-stu-id="417a2-127">Result code</span></span>

<span data-ttu-id="417a2-128">Код результата для вызова зависимости.</span><span class="sxs-lookup"><span data-stu-id="417a2-128">Result code of a dependency call.</span></span> <span data-ttu-id="417a2-129">Примерами являются код ошибки SQL и код состояния HTTP.</span><span class="sxs-lookup"><span data-stu-id="417a2-129">Examples are SQL error code and HTTP status code.</span></span>

## <a name="success"></a><span data-ttu-id="417a2-130">Успешно</span><span class="sxs-lookup"><span data-stu-id="417a2-130">Success</span></span>

<span data-ttu-id="417a2-131">Указание того, был ли вызов успешным.</span><span class="sxs-lookup"><span data-stu-id="417a2-131">Indication of successful or unsuccessful call.</span></span>

## <a name="custom-properties"></a><span data-ttu-id="417a2-132">Пользовательские свойства</span><span class="sxs-lookup"><span data-stu-id="417a2-132">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="417a2-133">Пользовательские измерения</span><span class="sxs-lookup"><span data-stu-id="417a2-133">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]


## <a name="next-steps"></a><span data-ttu-id="417a2-134">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="417a2-134">Next steps</span></span>

- <span data-ttu-id="417a2-135">Настройка отслеживания зависимостей для платформы [.NET](app-insights-asp-net-dependencies.md)</span><span class="sxs-lookup"><span data-stu-id="417a2-135">Set up dependency tracking for [.NET](app-insights-asp-net-dependencies.md).</span></span>
- <span data-ttu-id="417a2-136">Настройка отслеживания зависимостей для платформы [Java](app-insights-java-agent.md)</span><span class="sxs-lookup"><span data-stu-id="417a2-136">Set up dependency tracking for [Java](app-insights-java-agent.md).</span></span>
- [<span data-ttu-id="417a2-137">Создание телеметрии настраиваемых зависимостей</span><span class="sxs-lookup"><span data-stu-id="417a2-137">Write custom dependency telemetry</span></span>](app-insights-api-custom-events-metrics.md#trackdependency)
- <span data-ttu-id="417a2-138">В [этой статье](application-insights-data-model.md) представлены типы данных и модель данных для Application Insights.</span><span class="sxs-lookup"><span data-stu-id="417a2-138">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="417a2-139">Ознакомление с [платформами](app-insights-platforms.md), поддерживаемыми Application Insights.</span><span class="sxs-lookup"><span data-stu-id="417a2-139">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
