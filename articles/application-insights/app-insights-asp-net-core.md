---
title: "aaaAzure Application Insights для ASP.NET Core | Документы Microsoft"
description: "Отслеживайте доступность, производительность и использование веб-приложений."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 3b722e47-38bd-4667-9ba4-65b7006c074c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: a7a27f9eef1daec5b0deae9fd88906e646980659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-aspnet-core"></a>Application Insights для ASP.NET Core
[Application Insights](app-insights-overview.md) позволяет осуществлять мониторинг доступности, производительности и использования вашего веб-приложения. Отзыв hello, получаемых о hello производительность и эффективность работы приложения в hello подстановки можно сделать правильный выбор hello направления проектирования hello в каждом жизненного цикла разработки.

![Пример](./media/app-insights-asp-net-core/sample.png)

Вам потребуется подписка [Microsoft Azure](http://azure.com). Войдите, используя учетную запись Майкрософт, которая уже может быть у вас для Windows, XBox Live или других облачных служб Майкрософт. В группу могут входить tooAzure организации подписки: попросите владельца tooadd hello tooit с учетной записью Майкрософт.

## <a name="getting-started"></a>Приступая к работе

* В обозревателе решений Visual Studio щелкните проект правой кнопкой мыши и выберите **Настроить Application Insights** или **Добавить > Application Insights**. [Подробнее](app-insights-asp-net.md).
* Если вы не видите эти команды меню, выполните hello [вручную getting Started руководства](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Getting-Started). Может потребоваться toodo это если проект был создан с помощью версии Visual Studio до 2017 г.

## <a name="using-application-insights"></a>Работа с Application Insights
Вход в hello [портал Microsoft Azure](https://portal.azure.com)выберите **все ресурсы** или **Application Insights**, а затем выберите приложение создано toomonitor ресурсов hello.

В отдельном окне браузера некоторое время поработайте с приложением. Вы увидите данные в Application Insights диаграммы hello. (Может потребоваться tooclick обновления.) Во время разработки объем этих данных будет небольшим, однако эти диаграммы станут по-настоящему полезными после публикации приложения, когда их будет использовать много пользователей. 

страница обзора Hello отображаются графики производительности: время ответа сервера, время загрузки страницы, а также счетчики запросов с ошибками. Щелкните любой диаграммы toosee дополнительные диаграммы и данных.

Представления в портале hello делятся на три основные категории:

* [Обозреватель метрик](app-insights-metrics-explorer.md) показано диаграмм и таблиц, метрики и счетчиков, например, время отклика, сбоев или метрики, созданных вами самостоятельно с hello [API](app-insights-api-custom-events-metrics.md). Фильтр и сегмент данных hello путем лучшего понимания приложения и его пользователей tooget значения свойства.
* [Поиск обозреватель](app-insights-diagnostic-search.md) перечислены отдельные события, такие как определенные запросы, исключения, журнала трассировки или события, созданные самостоятельно с hello [API](app-insights-api-custom-events-metrics.md). Фильтрации и поиска в событиях hello и переходов между проблемы tooinvestigate связанные события.
* [Analytics](app-insights-analytics.md) позволяет выполнять SQL-подобные запросы данных телеметрии и является мощным средством диагностики и анализа.

## <a name="alerts"></a>Оповещения
* Вы автоматически получаете [оповещения превентивной диагностики](app-insights-proactive-diagnostics.md), которые сообщают о необычных изменениях в частоте сбоев и других метриках.
* Настройка [тестов доступности](app-insights-monitor-web-app-availability.md) tootest веб-узла постоянно местоположений по всему миру и получите сообщение электронной почты, сразу после сбоя теста.
* Настройка [метрики оповещений](app-insights-monitor-web-app-availability.md) tooknow Если метрик, таких как время ответа или исключение ставки выходит за допустимые границы.

## <a name="video"></a>Видео

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player] 

## <a name="open-source"></a>Открытый исходный код
[Читать и оставлять toohello кода](https://github.com/Microsoft/ApplicationInsights-aspnetcore#recent-updates)


## <a name="next-steps"></a>Дальнейшие действия
* [Добавить веб-страницы телеметрии tooyour](app-insights-javascript.md) toomonitor страниц об использовании и производительности.
* [Мониторинг зависимостей](app-insights-asp-net-dependencies.md) toosee Если REST, SQL или другим внешним ресурсам замедляют вы работу.
* [Используйте hello API](app-insights-api-custom-events-metrics.md) toosend собственные события и метрики для более подробного представления производительности и использовании приложения.
* [Проверяет доступность](app-insights-monitor-web-app-availability.md) проверьте приложение постоянно из вокруг Здравствуй, мир. 

