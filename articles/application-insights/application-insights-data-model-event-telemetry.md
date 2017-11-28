---
title: "Модель данных телеметрии Azure Application Insights — телеметрия событий | Документы Майкрософт"
description: "Модель данных Application Insights для телеметрии событий"
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
ms.openlocfilehash: 422e193ae10938954602a6ef8c49fd47f473bc01
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="event-telemetry-application-insights-data-model"></a><span data-ttu-id="7c084-103">Телеметрия событий: модель данных Application Insights</span><span class="sxs-lookup"><span data-stu-id="7c084-103">Event telemetry: Application Insights data model</span></span>

<span data-ttu-id="7c084-104">Элементы телеметрии событий, которые можно создавать в [Application Insights](app-insights-overview.md), представляют событие, произошедшее в приложении.</span><span class="sxs-lookup"><span data-stu-id="7c084-104">You can create event telemetry items (in [Application Insights](app-insights-overview.md)) to represent an event that occurred in your application.</span></span> <span data-ttu-id="7c084-105">Обычно это взаимодействие с пользователем, например нажатие кнопки или оформление заказа.</span><span class="sxs-lookup"><span data-stu-id="7c084-105">Typically it is a user interaction such as button click or order checkout.</span></span> <span data-ttu-id="7c084-106">Кроме того, это может быть событие жизненного цикла приложения, такое как инициализация или изменение конфигурации.</span><span class="sxs-lookup"><span data-stu-id="7c084-106">It can also be an application life cycle event like initialization or configuration update.</span></span> 

<span data-ttu-id="7c084-107">Семантически события могут как коррелировать, так и не коррелировать с запросами.</span><span class="sxs-lookup"><span data-stu-id="7c084-107">Semantically, events may or may not be correlated to requests.</span></span> <span data-ttu-id="7c084-108">Однако при правильном использовании телеметрия событий важнее, чем запросы или трассировки.</span><span class="sxs-lookup"><span data-stu-id="7c084-108">However, if used properly, event telemetry is more important than requests or traces.</span></span> <span data-ttu-id="7c084-109">События представляют бизнес-телеметрию и должны подвергаться отдельной, менее интенсивной [выборке](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="7c084-109">Events represent business telemetry and should be a subject to separate, less aggressive [sampling](app-insights-api-filtering-sampling.md).</span></span>

## <a name="name"></a><span data-ttu-id="7c084-110">Имя</span><span class="sxs-lookup"><span data-stu-id="7c084-110">Name</span></span>

<span data-ttu-id="7c084-111">Имя события.</span><span class="sxs-lookup"><span data-stu-id="7c084-111">Event name.</span></span> <span data-ttu-id="7c084-112">Чтобы обеспечить правильную группировку и значимость метрик, настройте в приложении создание небольшого количества имен отдельных событий.</span><span class="sxs-lookup"><span data-stu-id="7c084-112">To allow proper grouping and useful metrics, restrict your application so that it generates a small number of separate event names.</span></span> <span data-ttu-id="7c084-113">Например, не используйте отдельное имя для каждого созданного экземпляра события.</span><span class="sxs-lookup"><span data-stu-id="7c084-113">For example, don't use a separate name for each generated instance of an event.</span></span>

<span data-ttu-id="7c084-114">Максимальная длина: 512 символов</span><span class="sxs-lookup"><span data-stu-id="7c084-114">Max length: 512 characters</span></span>

## <a name="custom-properties"></a><span data-ttu-id="7c084-115">Пользовательские свойства</span><span class="sxs-lookup"><span data-stu-id="7c084-115">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="7c084-116">Пользовательские измерения</span><span class="sxs-lookup"><span data-stu-id="7c084-116">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a><span data-ttu-id="7c084-117">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7c084-117">Next steps</span></span>

- <span data-ttu-id="7c084-118">В [этой статье](application-insights-data-model.md) представлены типы данных и модель данных для Application Insights.</span><span class="sxs-lookup"><span data-stu-id="7c084-118">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- [<span data-ttu-id="7c084-119">Написание пользовательской телеметрии событий</span><span class="sxs-lookup"><span data-stu-id="7c084-119">Write custom event telemetry</span></span>](app-insights-api-custom-events-metrics.md#trackevent)
- <span data-ttu-id="7c084-120">Ознакомление с [платформами](app-insights-platforms.md), поддерживаемыми Application Insights.</span><span class="sxs-lookup"><span data-stu-id="7c084-120">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
