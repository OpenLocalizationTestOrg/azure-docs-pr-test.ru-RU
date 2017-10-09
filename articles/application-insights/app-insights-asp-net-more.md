---
title: "эффективность работы с Azure Application Insights aaaGet | Документы Microsoft"
description: "После Приступая к работе с помощью Application Insights, ниже приведена сводка функций hello изучения."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 7ec10a2d-c669-448d-8d45-b486ee32c8db
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: bwren
ms.openlocfilehash: 2023728afcf5aa5ecab8b957c8517d4872668765
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="more-telemetry-from-application-insights"></a>Дополнительные данные телеметрии из Application Insights
После того как вы [добавили Application Insights tooyour ASP.NET код](app-insights-asp-net.md), существует несколько вы можете делать tooget даже дополнительные телеметрии. 

| Действие | Что вы получаете|
|---|---|
|(Серверы IIS) [Установите монитор состояния](http://go.microsoft.com/fwlink/?LinkId=506648) на каждом компьютере-сервере.<br/>(Веб-приложениях azure) Панели hello Azure управления для веб-приложения hello откройте колонку hello Application Insights.| [**Счетчики производительности**](app-insights-performance-counters.md).<br/>[**Исключения**](app-insights-asp-net-exceptions.md) — подробные трассировки стека.<br/>[**Зависимости**](app-insights-asp-net-dependencies.md).|
|[Добавить hello JavaScript фрагмент tooyour веб-страницы](app-insights-javascript.md)|[Производительность страниц](app-insights-web-track-usage.md), исключения браузера, производительность вызовов AJAX. Пользовательская телеметрия на стороне клиента.|
|[Создайте веб-тесты на доступность](app-insights-monitor-web-app-availability.md)|Получение оповещений, когда сайт становится недоступным|
|Убедитесь, что MSBuild создает [файл BuildInfo.config](https://msdn.microsoft.com/library/dn449058.aspx)|[Создание заметок к диаграммам метрик](https://blogs.msdn.microsoft.com/visualstudioalm/2013/11/14/implementing-deployment-markers-in-application-insights/)
|[Напишите собственные события и систему телеметрии](app-insights-api-custom-events-metrics.md)|Учет бизнес-событий и метрик, отслеживание подробных сведений об использовании и многое другое|
|[Выполните профилирование активного сайта](https://aka.ms/AIProfilerPreview)|Подробные временные показатели функций из активного веб-приложения|






