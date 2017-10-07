---
title: "Использование tooenable контекст пользователя aaaSending возможности Azure Application Insights | Документы Microsoft"
description: "Отслеживайте, как пользователи перемещаются по службе, назначив каждому из них строку уникального постоянного идентификатора в Application Insights."
services: application-insights
documentationcenter: 
author: abgreg
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: csharp
ms.topic: article
ms.date: 08/02/2017
ms.author: bwren
ms.openlocfilehash: 0e6c2348f53a3ea970060334179b0dd070925e82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
#  <a name="sending-user-context-tooenable-usage-experiences-in-azure-application-insights"></a>Отправка использование tooenable контекст пользователя возникает в Azure Application Insights

## <a name="tracking-users"></a>Отслеживание пользователей

Application Insights позволяет вам toomonitor и отслеживать пользователей через набор средств использования продукта: 
* [Пользователи, сеансы, события](https://docs.microsoft.com/azure/application-insights/app-insights-usage-segmentation)
* [Воронки](https://docs.microsoft.com/azure/application-insights/usage-funnels)
* [Сохранение](https://docs.microsoft.com/azure/application-insights/app-insights-usage-retention)
* когорты;
* [Книги](https://docs.microsoft.com/azure/application-insights/app-insights-usage-workbooks)

В tootrack порядке, что пользователь выполняет со временем Application Insights требуется идентификатор для каждого пользователя или сеанса. Включите эти идентификаторы в каждое представление пользовательского события или страницы.
- Для пользователей, воронок, инструментов хранения и когорт: включите идентификатор пользователя.
- Для сеансов: включите идентификатор сеанса.

Если приложение интегрировано с hello [JavaScript SDK](https://docs.microsoft.com/azure/application-insights/app-insights-javascript#set-up-application-insights-for-your-web-page), автоматически отслеживаются идентификатор пользователя.

## <a name="choosing-user-ids"></a>Выбор идентификаторов пользователей

Идентификаторы пользователей должны быть постоянными в tootrack сеансы пользователей поведение пользователей со временем. Существуют различные подходы для сохранения идентификатора hello.
- Определение пользователя, уже имеющееся в службе.
- Если службы hello браузера tooa доступ, его можно передать браузера hello куки-файл с Идентификатором его. Идентификатор Hello будет сохраняться для пребывания hello cookie в браузере пользователя hello.
- При необходимости можно использовать новый идентификатор каждого сеанса, но результаты hello о пользователях будут ограничены. Например не будет возможности toosee как поведение пользователя меняется со временем.

Идентификатор Hello должно быть идентификатором Guid или другой строковым недостаточно сложный tooidentify каждого пользователя уникально. Например, это может быть длинное случайное число.

Если идентификатор hello содержит персональные идентификационные сведения о пользователе hello, не соответствующее значение toosend tooApplication аналитики как идентификатор пользователя. Вы можете отправить такой код как [идентификатор пользователя с проверкой подлинности](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#authenticated-users), но не удовлетворяет hello требования идентификатор пользователя для сценариев использования.

## <a name="aspnet-apps-set-user-context-in-an-itelemetryinitializer"></a>Приложения ASP.NET: установка контекста пользователя в ITelemetryInitializer

Создание инициализатор телеметрии как подробно описано [здесь](https://docs.microsoft.com/azure/application-insights/app-insights-api-filtering-sampling#add-properties-itelemetryinitializer)и набор hello Context.User.Id и hello Context.Session.Id.

Этот пример устанавливает идентификатор tooan идентификатор пользователя hello, срок действия сеанса hello. По возможности используйте идентификатор пользователя, который сохраняется между сеансами.

*C#*

```C#

    using System;
    using System.Web;
    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.Extensibility;

    namespace MvcWebRole.Telemetry
    {
      /*
       * Custom TelemetryInitializer that sets hello user ID.
       *
       */
      public class MyTelemetryInitializer : ITelemetryInitializer
      {
        public void Initialize(ITelemetry telemetry)
        {
            // For a full experience, track each user across sessions. For an incomplete view of user 
            // behavior within a session, store user ID on hello HttpContext Session.
            // Set hello user ID if we haven't done so yet.
            if (HttpContext.Current.Session["UserId"] == null)
            {
                HttpContext.Current.Session["UserId"] = Guid.NewGuid();
            }

            // Set hello user id on hello Application Insights telemetry item.
            telemetry.Context.User.Id = (string)HttpContext.Current.Session["UserId"];

            // Set hello session id on hello Application Insights telemetry item.
            telemetry.Context.Session.Id = HttpContext.Current.Session.SessionID;
        }
      }
    }
```

## <a name="next-steps"></a>Дальнейшие действия
- опыт использования tooenable, начать отправку [пользовательские события](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) или [просмотры страниц](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).
- При отправке уже, пользовательские события и представления страницы, просмотр hello использования средств toolearn как пользователям использовать эту службу.
    * [Общие сведения об использовании](app-insights-usage-overview.md)
    * [Анализ пользователей, сеансов и событий в Application Insights](app-insights-usage-segmentation.md)
    * [Воронки](usage-funnels.md)
    * [Сохранение](app-insights-usage-retention.md)
    * [Книги](app-insights-usage-workbooks.md)
