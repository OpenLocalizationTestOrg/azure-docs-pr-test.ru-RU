---
title: "aaaAzure модели данных телеметрии приложения аналитики - телеметрии события | Документы Microsoft"
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
ms.openlocfilehash: cd7dc3c5f4f3df22b7a52ee79fcad566a27a9f4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="event-telemetry-application-insights-data-model"></a><span data-ttu-id="aabd0-103">Телеметрия событий: модель данных Application Insights</span><span class="sxs-lookup"><span data-stu-id="aabd0-103">Event telemetry: Application Insights data model</span></span>

<span data-ttu-id="aabd0-104">Вы можете создавать события телеметрии элементы (в [Application Insights](app-insights-overview.md)) toorepresent событие, произошедшее в приложении.</span><span class="sxs-lookup"><span data-stu-id="aabd0-104">You can create event telemetry items (in [Application Insights](app-insights-overview.md)) toorepresent an event that occurred in your application.</span></span> <span data-ttu-id="aabd0-105">Обычно это взаимодействие с пользователем, например нажатие кнопки или оформление заказа.</span><span class="sxs-lookup"><span data-stu-id="aabd0-105">Typically it is a user interaction such as button click or order checkout.</span></span> <span data-ttu-id="aabd0-106">Кроме того, это может быть событие жизненного цикла приложения, такое как инициализация или изменение конфигурации.</span><span class="sxs-lookup"><span data-stu-id="aabd0-106">It can also be an application life cycle event like initialization or configuration update.</span></span> 

<span data-ttu-id="aabd0-107">Семантически событий может или не может быть коррелированные toorequests.</span><span class="sxs-lookup"><span data-stu-id="aabd0-107">Semantically, events may or may not be correlated toorequests.</span></span> <span data-ttu-id="aabd0-108">Однако при правильном использовании телеметрия событий важнее, чем запросы или трассировки.</span><span class="sxs-lookup"><span data-stu-id="aabd0-108">However, if used properly, event telemetry is more important than requests or traces.</span></span> <span data-ttu-id="aabd0-109">События представляют бизнес-телеметрии и должен быть tooseparate субъекта, менее агрессивными [выборки](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="aabd0-109">Events represent business telemetry and should be a subject tooseparate, less aggressive [sampling](app-insights-api-filtering-sampling.md).</span></span>

## <a name="name"></a><span data-ttu-id="aabd0-110">Имя</span><span class="sxs-lookup"><span data-stu-id="aabd0-110">Name</span></span>

<span data-ttu-id="aabd0-111">Имя события.</span><span class="sxs-lookup"><span data-stu-id="aabd0-111">Event name.</span></span> <span data-ttu-id="aabd0-112">tooallow правильную группирования и полезных метрик, ограничения приложения таким образом, чтобы он создает несколько имен отдельное событие.</span><span class="sxs-lookup"><span data-stu-id="aabd0-112">tooallow proper grouping and useful metrics, restrict your application so that it generates a small number of separate event names.</span></span> <span data-ttu-id="aabd0-113">Например, не используйте отдельное имя для каждого созданного экземпляра события.</span><span class="sxs-lookup"><span data-stu-id="aabd0-113">For example, don't use a separate name for each generated instance of an event.</span></span>

<span data-ttu-id="aabd0-114">Максимальная длина: 512 символов</span><span class="sxs-lookup"><span data-stu-id="aabd0-114">Max length: 512 characters</span></span>

## <a name="custom-properties"></a><span data-ttu-id="aabd0-115">Пользовательские свойства</span><span class="sxs-lookup"><span data-stu-id="aabd0-115">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="aabd0-116">Пользовательские измерения</span><span class="sxs-lookup"><span data-stu-id="aabd0-116">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a><span data-ttu-id="aabd0-117">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="aabd0-117">Next steps</span></span>

- <span data-ttu-id="aabd0-118">В [этой статье](application-insights-data-model.md) представлены типы данных и модель данных для Application Insights.</span><span class="sxs-lookup"><span data-stu-id="aabd0-118">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- [<span data-ttu-id="aabd0-119">Написание пользовательской телеметрии событий</span><span class="sxs-lookup"><span data-stu-id="aabd0-119">Write custom event telemetry</span></span>](app-insights-api-custom-events-metrics.md#trackevent)
- <span data-ttu-id="aabd0-120">Ознакомление с [платформами](app-insights-platforms.md), поддерживаемыми Application Insights.</span><span class="sxs-lookup"><span data-stu-id="aabd0-120">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
