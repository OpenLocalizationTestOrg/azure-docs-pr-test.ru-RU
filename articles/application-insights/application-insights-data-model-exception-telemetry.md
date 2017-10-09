---
title: "aaaAzure модели данных телеметрии приложения аналитики - исключение телеметрии | Документы Microsoft"
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
ms.openlocfilehash: 4c2b7d1ac3816d5623db9a35819a48a68a13a9cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="exception-telemetry-application-insights-data-model"></a><span data-ttu-id="a38ad-103">Телеметрия исключений: модель данных Application Insights</span><span class="sxs-lookup"><span data-stu-id="a38ad-103">Exception telemetry: Application Insights data model</span></span>

<span data-ttu-id="a38ad-104">В [Application Insights](app-insights-overview.md), обработано или необработанное исключение, которое произошло во время выполнения приложения hello отслеживаемых представляет экземпляр исключения.</span><span class="sxs-lookup"><span data-stu-id="a38ad-104">In [Application Insights](app-insights-overview.md), an instance of Exception represents a handled or unhandled exception that occurred during execution of hello monitored application.</span></span>

## <a name="problem-id"></a><span data-ttu-id="a38ad-105">Идентификатор проблемы</span><span class="sxs-lookup"><span data-stu-id="a38ad-105">Problem Id</span></span>

<span data-ttu-id="a38ad-106">Идентификатор где hello возникло исключение в коде.</span><span class="sxs-lookup"><span data-stu-id="a38ad-106">Identifier of where hello exception was thrown in code.</span></span> <span data-ttu-id="a38ad-107">Используется для группирования исключений.</span><span class="sxs-lookup"><span data-stu-id="a38ad-107">Used for exceptions grouping.</span></span> <span data-ttu-id="a38ad-108">Обычно сочетание тип исключения и функцию из стека вызовов hello.</span><span class="sxs-lookup"><span data-stu-id="a38ad-108">Typically a combination of exception type and a function from hello call stack.</span></span>

<span data-ttu-id="a38ad-109">Максимальная длина: 1024 символа</span><span class="sxs-lookup"><span data-stu-id="a38ad-109">Max length: 1024 characters</span></span>

## <a name="severity-level"></a><span data-ttu-id="a38ad-110">Уровень серьезности</span><span class="sxs-lookup"><span data-stu-id="a38ad-110">Severity level</span></span>

<span data-ttu-id="a38ad-111">Уровень серьезности трассировки.</span><span class="sxs-lookup"><span data-stu-id="a38ad-111">Trace severity level.</span></span> <span data-ttu-id="a38ad-112">Возможные значения: `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span><span class="sxs-lookup"><span data-stu-id="a38ad-112">Value can be `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span></span>

## <a name="exception-details"></a><span data-ttu-id="a38ad-113">Сведения об исключении</span><span class="sxs-lookup"><span data-stu-id="a38ad-113">Exception details</span></span>

<span data-ttu-id="a38ad-114">(расширенный toobe)</span><span class="sxs-lookup"><span data-stu-id="a38ad-114">(toobe extended)</span></span>

## <a name="custom-properties"></a><span data-ttu-id="a38ad-115">Пользовательские свойства</span><span class="sxs-lookup"><span data-stu-id="a38ad-115">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="a38ad-116">Пользовательские измерения</span><span class="sxs-lookup"><span data-stu-id="a38ad-116">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a><span data-ttu-id="a38ad-117">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a38ad-117">Next steps</span></span>

- <span data-ttu-id="a38ad-118">В [этой статье](application-insights-data-model.md) представлены типы данных и модель данных для Application Insights.</span><span class="sxs-lookup"><span data-stu-id="a38ad-118">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="a38ad-119">Узнайте, каким образом слишком[диагностики исключений в веб-приложения с помощью Application Insights](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="a38ad-119">Learn how too[diagnose exceptions in your web apps with Application Insights](app-insights-asp-net-exceptions.md).</span></span>
- <span data-ttu-id="a38ad-120">Ознакомление с [платформами](app-insights-platforms.md), поддерживаемыми Application Insights.</span><span class="sxs-lookup"><span data-stu-id="a38ad-120">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
