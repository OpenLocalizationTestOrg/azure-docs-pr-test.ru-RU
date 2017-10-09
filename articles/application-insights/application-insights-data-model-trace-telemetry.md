---
title: "aaaAzure модели данных телеметрии приложения аналитики - телеметрии трассировки | Документы Microsoft"
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
ms.openlocfilehash: dfdee958e07d57448ff41abc5cd33bfd05dac090
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="trace-telemetry-application-insights-data-model"></a><span data-ttu-id="6c02f-103">Телеметрия трассировки: модель данных Application Insights</span><span class="sxs-lookup"><span data-stu-id="6c02f-103">Trace telemetry: Application Insights data model</span></span>

<span data-ttu-id="6c02f-104">Телеметрия трассировки (в [Application Insights](app-insights-overview.md)) представляет инструкции трассировки стиля `printf`, доступные для текстового поиска.</span><span class="sxs-lookup"><span data-stu-id="6c02f-104">Trace telemetry (in [Application Insights](app-insights-overview.md)) represents `printf` style trace statements that are text-searched.</span></span> <span data-ttu-id="6c02f-105">`Log4Net`, `NLog` и другие записи файла журнала на основе текста преобразуются в экземпляры этого типа.</span><span class="sxs-lookup"><span data-stu-id="6c02f-105">`Log4Net`, `NLog`, and other text-based log file entries are translated into instances of this type.</span></span> <span data-ttu-id="6c02f-106">Hello трассировки не имеет измерения как расширения.</span><span class="sxs-lookup"><span data-stu-id="6c02f-106">hello trace does not have measurements as an extensibility.</span></span>

## <a name="message"></a><span data-ttu-id="6c02f-107">Сообщение</span><span class="sxs-lookup"><span data-stu-id="6c02f-107">Message</span></span>

<span data-ttu-id="6c02f-108">Сообщение трассировки.</span><span class="sxs-lookup"><span data-stu-id="6c02f-108">Trace message.</span></span>

<span data-ttu-id="6c02f-109">Максимальная длина: 32 768 символов</span><span class="sxs-lookup"><span data-stu-id="6c02f-109">Max length: 32768 characters</span></span>

## <a name="severity-level"></a><span data-ttu-id="6c02f-110">Уровень серьезности</span><span class="sxs-lookup"><span data-stu-id="6c02f-110">Severity level</span></span>

<span data-ttu-id="6c02f-111">Уровень серьезности трассировки.</span><span class="sxs-lookup"><span data-stu-id="6c02f-111">Trace severity level.</span></span> <span data-ttu-id="6c02f-112">Возможные значения: `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span><span class="sxs-lookup"><span data-stu-id="6c02f-112">Value can be `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span></span>

## <a name="custom-properties"></a><span data-ttu-id="6c02f-113">Пользовательские свойства</span><span class="sxs-lookup"><span data-stu-id="6c02f-113">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="next-steps"></a><span data-ttu-id="6c02f-114">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6c02f-114">Next steps</span></span>

- <span data-ttu-id="6c02f-115">[Просмотр журналов трассировки .NET в Application Insights](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="6c02f-115">[Explore .NET trace logs in Application Insights](app-insights-asp-net-trace-logs.md).</span></span>
- <span data-ttu-id="6c02f-116">[Просмотр журналов трассировки Java в Application Insights](app-insights-java-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="6c02f-116">[Explore Java trace logs in Application Insights](app-insights-java-trace-logs.md).</span></span>
- <span data-ttu-id="6c02f-117">В [этой статье](application-insights-data-model.md) представлены типы данных и модель данных для Application Insights.</span><span class="sxs-lookup"><span data-stu-id="6c02f-117">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- [<span data-ttu-id="6c02f-118">Написание пользовательской телеметрии трассировки</span><span class="sxs-lookup"><span data-stu-id="6c02f-118">Write custom trace telemetry</span></span>](app-insights-api-custom-events-metrics.md#tracktrace)
- <span data-ttu-id="6c02f-119">Ознакомление с [платформами](app-insights-platforms.md), поддерживаемыми Application Insights.</span><span class="sxs-lookup"><span data-stu-id="6c02f-119">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
