---
title: "Диагностика aaaSmart web изменений производительности приложения в Azure Application Insights | Документы Microsoft"
description: "Автоматическая диагностика пиков или шагов в данных телеметрии производительности из веб-приложения."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/16/2017
ms.author: cfreeman
ms.openlocfilehash: 8891762c4a4bfdb08b647fe3b702349eb30ec9c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-sudden-changes-in-your-app-telemetry"></a>Диагностика внезапных изменений в телеметрии приложения

*Эта функция предоставляется в предварительной версии.*

Диагностируйте внезапные изменения производительности или использования веб-приложения одним щелчком мыши! Hello смарт-диагностики доступна каждый раз при создании временной диаграммы в [Analytics](app-insights-analytics.md) в [Application Insights](app-insights-overview.md). Везде, где есть необычные изменение тренда hello результатов, например, пик или dip, смарт-диагностики обозначает шаблон измерений и связанных значений, которые могут объяснить hello изменений. Это поможет вам быстро диагностировать проблему hello. 

В этом примере смарт-диагностики определил шаблон значения свойств, связанных с изменением hello и подчеркивает hello различие между результаты с использованием и без этого шаблона:

![Пример результатов диагностики аналитики](./media/app-insights-analytics-diagnostics/analytics-result.png)
 

## <a name="diagnose-data-changes"></a>Диагностика изменений данных

1.  Выполните запрос в Analytics и отрисуйте его в виде диаграммы времени. 
2.  Щелкните любой из выделенных пиков, если он имеется.
 
    ![пик](./media/app-insights-analytics-diagnostics/peak.png)

    Диагностика занимает несколько секунд toodiscover шаблон.

3. Hello результатов диагностики вкладке отображается шаблон, которые могут помочь выяснить разрыв в данных.

    ![result](./media/app-insights-analytics-diagnostics/result.png)
 
    текст Hello указывает hello значения измерений, которые появляются toocorrelate с hello shift. В этом примере оно связано с конкретным запросом и конкретной версией браузера.

    Следует также обратить внимание hello двух компонентов hello диаграммы, с hello фильтра true и false. компонент false Hello показывает тренд без изменений. Другими словами нет изменений в результатах телеметрии hello, если мы исключить hello проблемный сочетаниями измерений, которые определил диагностики. В отличие от этого результаты hello в комбинации показывают требуются значительные изменения в пределах области выделены hello расследования. Показывает, что диагностики обнаружил сочетания свойств с объяснением hello изменений.

4.  Если шаблон hello является сложным, требуется toohover по сравнению с **Показать все** toosee hello измерений.

    ![показать все](./media/app-insights-analytics-diagnostics/show-all.png)
 
5.  В случае, если Диагностика находит не toonotify значительные шаблон о hello, откроется страница «нет результатов». На этом этапе запрос можно изменить. Например может сузить диапазон времени hello и группирования в запросе Analytics для дальнейшего анализа и потенциально более точные результаты.

Используя знания hello, что на одной странице веб-сайте возникла проблема в браузере, определенного, позволяют теперь переход на страницу прямой toohello проблему и изучить последние изменения.

## <a name="try-hello-demo"></a>Повторите Демонстрация hello

[Щелкните здесь, toosee Демонстрация](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA3VSTY%2FTQAy991dYPXWlLf0QIO2KIiGWA3duiMPsxEnMzhe2p6WIH48nVUsuGylRNPOe3%2FOzN5vFZgPfRhL4VZHPIGM%2BCdgHdESgpMjOKx0RnsgNKYuSF%2BjRaWUE7xKMGIoBgTpMSv2Z0jBxOWc1QBWEPjM4EMUCP2uc0A3x8E5HKMi%2BEQNC7oHRbIgKdJWdUk5vmr9PvdkArildit%2Fcrk0lBDjnyhBzk%2FKVxdTy0QhNY6RhDPYqdlCy9XMV96NjBZc68IH8y6Tzuf01iZxeIZ%2FI5DqMOYmaQQRXNUdz6qGb5WOdSKEXnOozHtEFK%2Bh0qnq5YQzGF9DcoinoqbcigkO0NOZRNGOZaaBkMuat5xznFOtULKhG%2BdrGlVDhy%2B8SMlsETV8dD6gTd0YrbsBrFq6U1v%2Filv4C%2FsJpRJuwUrQTZ0P7eIDOHLeD1X67e7%2Fe7dbbB9htH%2Ffbu4vQDfvhFez%2B8a1h%2F1f3VSy%2BJ4Ol1oN8X4qN0qMZWv44HJanzKFLeJIltKcRpcbomP7gbHNkdV2Xe1uqO3g%2BwzOl1c3PvbmMlC7KjKlry2GX0w4s%2FgFoo5%2BhBAMAAA%3D%3D&timespan=PT24H) над образцом данных.

## <a name="how-it-works"></a>Принцип работы

Смарт-диагностики используется алгоритм Дополнительно незащищенных машинного обучения, основании hello [DiffPatterns](app-insights-analytics-reference.md) операции. Выполняет поиск вероятные шаблоны, которые могут объяснить hello изменения данных. Анализирует hello влияние каждого кандидата на метрику hello и показан шаблон hello, лучше всего сопоставлены hello изменений.

## <a name="no-diagnostic-points"></a>Нет точек диагностики?

Смарт-диагностики работает только в том случае, когда выполняются следующие условия hello:

 * Включен параметр интеллектуальной диагностики. Найдите под значком параметров hello в аналитике.
 * выбран Hello параметр смарт-диагностики в параметрах Analytics. 
 * Ось времени: hello оси x диаграммы hello должен иметь тип `datetime`.
 * График или диаграмма с областями: диагностика работает только для этих типов диаграмм. Используйте `| render timechart` или `| render areachart` в конце hello запроса; или выберите из раскрывающегося списка выбора hello линии или области диаграммы.
 * Разрыв: Необходимо значительный разрыв в данных hello.
 * Достаточно tooanalyze точек.
 * Не более одного обобщить предложение в запросе hello.
 * Без предложения проекта, содержащего определение имени перед hello суммировать предложения.

 
 ## <a name="related-articles"></a>Связанные статьи

 * [Руководство по аналитике](app-insights-analytics-tour.md)
 * [Смарт-обнаружение](app-insights-proactive-diagnostics.md) автоматически оповещает пользователя tooperformance проблемы.
