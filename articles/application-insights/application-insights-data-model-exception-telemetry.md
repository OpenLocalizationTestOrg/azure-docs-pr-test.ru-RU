---
title: "Модель данных телеметрии Azure Application Insights — телеметрия исключений | Документы Майкрософт"
description: "Модель данных Application Insights для телеметрии исключений"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/25/2017
ms.author: bwren
ms.openlocfilehash: 6b220b0cb6719bac606f599d657d08ab847c7590
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="exception-telemetry-application-insights-data-model"></a><span data-ttu-id="388dd-103">Телеметрия исключений: модель данных Application Insights</span><span class="sxs-lookup"><span data-stu-id="388dd-103">Exception telemetry: Application Insights data model</span></span>

<span data-ttu-id="388dd-104">В [Application Insights](app-insights-overview.md) экземпляр исключения представляет обработанное или необработанное исключение, возникшее во время выполнения отслеживаемого приложения.</span><span class="sxs-lookup"><span data-stu-id="388dd-104">In [Application Insights](app-insights-overview.md), an instance of Exception represents a handled or unhandled exception that occurred during execution of the monitored application.</span></span>

## <a name="problem-id"></a><span data-ttu-id="388dd-105">Идентификатор проблемы</span><span class="sxs-lookup"><span data-stu-id="388dd-105">Problem Id</span></span>

<span data-ttu-id="388dd-106">Идентификатор места в коде, где возникло исключение.</span><span class="sxs-lookup"><span data-stu-id="388dd-106">Identifier of where the exception was thrown in code.</span></span> <span data-ttu-id="388dd-107">Используется для группирования исключений.</span><span class="sxs-lookup"><span data-stu-id="388dd-107">Used for exceptions grouping.</span></span> <span data-ttu-id="388dd-108">Обычно это сочетание типа исключения и функции из стека вызовов.</span><span class="sxs-lookup"><span data-stu-id="388dd-108">Typically a combination of exception type and a function from the call stack.</span></span>

<span data-ttu-id="388dd-109">Максимальная длина: 1024 символа</span><span class="sxs-lookup"><span data-stu-id="388dd-109">Max length: 1024 characters</span></span>

## <a name="severity-level"></a><span data-ttu-id="388dd-110">Уровень серьезности</span><span class="sxs-lookup"><span data-stu-id="388dd-110">Severity level</span></span>

<span data-ttu-id="388dd-111">Уровень серьезности трассировки.</span><span class="sxs-lookup"><span data-stu-id="388dd-111">Trace severity level.</span></span> <span data-ttu-id="388dd-112">Возможные значения: `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span><span class="sxs-lookup"><span data-stu-id="388dd-112">Value can be `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span></span>

## <a name="exception-details"></a><span data-ttu-id="388dd-113">Сведения об исключении</span><span class="sxs-lookup"><span data-stu-id="388dd-113">Exception details</span></span>

<span data-ttu-id="388dd-114">(Эти сведения будут добавлены позже.)</span><span class="sxs-lookup"><span data-stu-id="388dd-114">(To be extended)</span></span>

## <a name="custom-properties"></a><span data-ttu-id="388dd-115">Пользовательские свойства</span><span class="sxs-lookup"><span data-stu-id="388dd-115">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="388dd-116">Пользовательские измерения</span><span class="sxs-lookup"><span data-stu-id="388dd-116">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a><span data-ttu-id="388dd-117">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="388dd-117">Next steps</span></span>

- <span data-ttu-id="388dd-118">В [этой статье](application-insights-data-model.md) представлены типы данных и модель данных для Application Insights.</span><span class="sxs-lookup"><span data-stu-id="388dd-118">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="388dd-119">Вы можете научиться [диагностировать исключения в веб-приложениях с помощью Application Insights](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="388dd-119">Learn how to [diagnose exceptions in your web apps with Application Insights](app-insights-asp-net-exceptions.md).</span></span>
- <span data-ttu-id="388dd-120">Ознакомление с [платформами](app-insights-platforms.md), поддерживаемыми Application Insights.</span><span class="sxs-lookup"><span data-stu-id="388dd-120">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
