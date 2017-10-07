---
title: "aaaSmart обнаружения в Azure Application Insights | Документы Microsoft"
description: "Служба Application Insights автоматически выполняет углубленный анализ телеметрии вашего приложения и предупреждает о потенциальных проблемах."
services: application-insights
documentationcenter: windows
author: rakefetj
manager: carmonm
ms.assetid: 2eeb4a35-c7a1-49f7-9b68-4f4b860938b2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: bwren
ms.openlocfilehash: f794476088fc69154eda2077b7a5cdc769fab3a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="smart-detection-in-application-insights"></a>Интеллектуальное обнаружение в Application Insights
 Функция интеллектуального обнаружения автоматически предупреждает о потенциальных проблемах с производительностью в веб-приложении. Он выполняет упреждающее анализа телеметрии hello, которое приложение отправляет слишком[Application Insights](app-insights-overview.md). В случае внезапного увеличения частоты сбоев или числа аномальных тенденций в производительности клиента или сервера вы получите оповещение. Эта функция не требует настройки. Она работает, если приложение отправляет достаточный объем данных телеметрии.

Оповещения об обнаружении смарт-доступны как из hello сообщения электронной почты, получаемых, так и из колонки hello смарт-обнаружение.

## <a name="review-your-smart-detections"></a>Просмотр интеллектуального обнаружения
Просматривать результаты обнаружения можно двумя способами.

* **В сообщениях электронной почты** , получаемых из Application Insights. Вот типичный пример:
  
    ![Оповещение по электронной почте](./media/app-insights-proactive-diagnostics/03.png)
  
    Нажмите большую кнопку tooopen hello более подробно в портал hello.
* **Плитка смарт-обнаружение Hello** на общие сведения о приложении колонке показывает количество последних оповещений. Щелкните плитку hello toosee список последних оповещений.

![Просмотр последних результатов обнаружения](./media/app-insights-proactive-diagnostics/04.png)

Выберите оповещения toosee сведения о нем.

## <a name="what-problems-are-detected"></a>Какие проблемы можно обнаружить?
Существует три типа обнаружения:

* [Интеллектуальное обнаружение. Аномальные сбои.](app-insights-proactive-failure-diagnostics.md) Мы используем машинного обучения tooset hello ожидается Частота сбоев запросов для приложения, сопоставление с нагрузочных тестов и других факторов. Если частота сбоев hello выйдет за пределы ожидаемого конверт hello, вам будет отправлено оповещение.
* [Интеллектуальное обнаружение. Аномалии производительности.](app-insights-proactive-performance-diagnostics.md) Получать уведомления, если время отклика продолжительность операции или зависимость, замедляя базовые сравниваемых toohistorical или определяются аномальных шаблон времени отклика или время загрузки страницы.   
* [Интеллектуальное обнаружение. Неполадки облачной службы Azure.](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/) Вы получаете оповещения в том случае, если приложение размещено в облачных службах Azure и в экземпляре роли происходят сбои при запуске, частый перезапуск или сбои среды выполнения.

(ссылки на справку hello в каждом уведомлении перейти toohello статьи по этой теме.)

## <a name="video"></a>Видео

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>Дальнейшие действия
Эти средства диагностики помогут проверить hello телеметрии из приложения:

* [Обозреватель метрик](app-insights-metrics-explorer.md)
* [Обозреватель поиска](app-insights-diagnostic-search.md)
* [Аналитика, мощный язык запросов](app-insights-analytics-tour.md)

Интеллектуальное обнаружение — это полностью автоматическая функция. Но возможно хотелось бы tooset некоторые дополнительные предупреждений?

* [Настройка оповещений в Application Insights](app-insights-alerts.md)
* [Доступность веб-тестов](app-insights-monitor-web-app-availability.md) 

