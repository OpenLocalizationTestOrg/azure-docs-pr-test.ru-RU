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
# <a name="event-telemetry-application-insights-data-model"></a>Телеметрия событий: модель данных Application Insights

Вы можете создавать события телеметрии элементы (в [Application Insights](app-insights-overview.md)) toorepresent событие, произошедшее в приложении. Обычно это взаимодействие с пользователем, например нажатие кнопки или оформление заказа. Кроме того, это может быть событие жизненного цикла приложения, такое как инициализация или изменение конфигурации. 

Семантически событий может или не может быть коррелированные toorequests. Однако при правильном использовании телеметрия событий важнее, чем запросы или трассировки. События представляют бизнес-телеметрии и должен быть tooseparate субъекта, менее агрессивными [выборки](app-insights-api-filtering-sampling.md).

## <a name="name"></a>Имя

Имя события. tooallow правильную группирования и полезных метрик, ограничения приложения таким образом, чтобы он создает несколько имен отдельное событие. Например, не используйте отдельное имя для каждого созданного экземпляра события.

Максимальная длина: 512 символов

## <a name="custom-properties"></a>Пользовательские свойства

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a>Пользовательские измерения

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a>Дальнейшие действия

- В [этой статье](application-insights-data-model.md) представлены типы данных и модель данных для Application Insights.
- [Написание пользовательской телеметрии событий](app-insights-api-custom-events-metrics.md#trackevent)
- Ознакомление с [платформами](app-insights-platforms.md), поддерживаемыми Application Insights.
