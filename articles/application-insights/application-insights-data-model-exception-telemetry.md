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
# <a name="exception-telemetry-application-insights-data-model"></a>Телеметрия исключений: модель данных Application Insights

В [Application Insights](app-insights-overview.md), обработано или необработанное исключение, которое произошло во время выполнения приложения hello отслеживаемых представляет экземпляр исключения.

## <a name="problem-id"></a>Идентификатор проблемы

Идентификатор где hello возникло исключение в коде. Используется для группирования исключений. Обычно сочетание тип исключения и функцию из стека вызовов hello.

Максимальная длина: 1024 символа

## <a name="severity-level"></a>Уровень серьезности

Уровень серьезности трассировки. Возможные значения: `Verbose`, `Information`, `Warning`, `Error`, `Critical`.

## <a name="exception-details"></a>Сведения об исключении

(расширенный toobe)

## <a name="custom-properties"></a>Пользовательские свойства

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a>Пользовательские измерения

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a>Дальнейшие действия

- В [этой статье](application-insights-data-model.md) представлены типы данных и модель данных для Application Insights.
- Узнайте, каким образом слишком[диагностики исключений в веб-приложения с помощью Application Insights](app-insights-asp-net-exceptions.md).
- Ознакомление с [платформами](app-insights-platforms.md), поддерживаемыми Application Insights.
