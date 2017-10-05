---
title: "Модель данных телеметрии Azure Application Insights — телеметрия трассировки | Документы Майкрософт"
description: "Модель данных Application Insights для телеметрии трассировки"
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
ms.openlocfilehash: e1da0d6a6fbd9ca5486936c326ade667d7b01006
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="trace-telemetry-application-insights-data-model"></a><span data-ttu-id="b5706-103">Телеметрия трассировки: модель данных Application Insights</span><span class="sxs-lookup"><span data-stu-id="b5706-103">Trace telemetry: Application Insights data model</span></span>

<span data-ttu-id="b5706-104">Телеметрия трассировки (в [Application Insights](app-insights-overview.md)) представляет инструкции трассировки стиля `printf`, доступные для текстового поиска.</span><span class="sxs-lookup"><span data-stu-id="b5706-104">Trace telemetry (in [Application Insights](app-insights-overview.md)) represents `printf` style trace statements that are text-searched.</span></span> <span data-ttu-id="b5706-105">`Log4Net`, `NLog` и другие записи файла журнала на основе текста преобразуются в экземпляры этого типа.</span><span class="sxs-lookup"><span data-stu-id="b5706-105">`Log4Net`, `NLog`, and other text-based log file entries are translated into instances of this type.</span></span> <span data-ttu-id="b5706-106">Трассировка не имеет измерений в качестве расширения.</span><span class="sxs-lookup"><span data-stu-id="b5706-106">The trace does not have measurements as an extensibility.</span></span>

## <a name="message"></a><span data-ttu-id="b5706-107">Сообщение</span><span class="sxs-lookup"><span data-stu-id="b5706-107">Message</span></span>

<span data-ttu-id="b5706-108">Сообщение трассировки.</span><span class="sxs-lookup"><span data-stu-id="b5706-108">Trace message.</span></span>

<span data-ttu-id="b5706-109">Максимальная длина: 32 768 символов</span><span class="sxs-lookup"><span data-stu-id="b5706-109">Max length: 32768 characters</span></span>

## <a name="severity-level"></a><span data-ttu-id="b5706-110">Уровень серьезности</span><span class="sxs-lookup"><span data-stu-id="b5706-110">Severity level</span></span>

<span data-ttu-id="b5706-111">Уровень серьезности трассировки.</span><span class="sxs-lookup"><span data-stu-id="b5706-111">Trace severity level.</span></span> <span data-ttu-id="b5706-112">Возможные значения: `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span><span class="sxs-lookup"><span data-stu-id="b5706-112">Value can be `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span></span>

## <a name="custom-properties"></a><span data-ttu-id="b5706-113">Пользовательские свойства</span><span class="sxs-lookup"><span data-stu-id="b5706-113">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="next-steps"></a><span data-ttu-id="b5706-114">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b5706-114">Next steps</span></span>

- <span data-ttu-id="b5706-115">[Просмотр журналов трассировки .NET в Application Insights](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="b5706-115">[Explore .NET trace logs in Application Insights](app-insights-asp-net-trace-logs.md).</span></span>
- <span data-ttu-id="b5706-116">[Просмотр журналов трассировки Java в Application Insights](app-insights-java-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="b5706-116">[Explore Java trace logs in Application Insights](app-insights-java-trace-logs.md).</span></span>
- <span data-ttu-id="b5706-117">В [этой статье](application-insights-data-model.md) представлены типы данных и модель данных для Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b5706-117">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- [<span data-ttu-id="b5706-118">Написание пользовательской телеметрии трассировки</span><span class="sxs-lookup"><span data-stu-id="b5706-118">Write custom trace telemetry</span></span>](app-insights-api-custom-events-metrics.md#tracktrace)
- <span data-ttu-id="b5706-119">Ознакомление с [платформами](app-insights-platforms.md), поддерживаемыми Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b5706-119">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
