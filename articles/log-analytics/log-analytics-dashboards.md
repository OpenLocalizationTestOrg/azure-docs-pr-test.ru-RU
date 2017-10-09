---
title: "aaaCreate настраиваемую панель мониторинга в службе анализа журналов Azure | Документы Microsoft"
description: "Это руководство поможет вам понять, как панели мониторинга службы анализа журналов можно визуализации всех ваших запросов поиска журналов, предоставляя один дисторсии tooview вашей среде."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: abb07f6c-b356-4f15-85f5-60e4415d0ba2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 73fcf131a91c743d473f37d5a40d52eaf78a7ba3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-dashboard-for-use-in-log-analytics"></a>Создание пользовательской панели мониторинга для Log Analytics

>[!NOTE]
> Если обновленный toohello рабочей области [языка запросов новый журнал аналитики](log-analytics-log-search-upgrade.md), то нельзя создать новые панели мониторинга или изменение существующих панелей мониторинга. 

Это руководство поможет вам понять, как панели мониторинга службы анализа журналов можно визуализации всех ваших запросов поиска журналов, предоставляя один дисторсии tooview вашей среде.

![Пример панели мониторинга](./media/log-analytics-dashboards/oms-dashboards-example-dash.png)

Все hello настраиваемых панелей мониторинга, созданные на портале OMS hello, также доступны в hello мобильные приложения OMS. См. следующие страницы, Дополнительные сведения о приложениях hello hello.

* [OMS мобильного приложения из магазина Microsoft hello](http://www.windowsphone.com/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865)
* [Мобильное приложение OMS в Apple iTunes](https://itunes.apple.com/app/microsoft-operations-management/id1042424859?mt=8)

![панель мониторинга на мобильном устройстве](./media/log-analytics-dashboards/oms-search-mobile.png)

## <a name="how-do-i-create-my-dashboard"></a>Создание панели мониторинга
toobegin toohello последовательно выберите «Обзор» OMS. Вы увидите hello **Моя панель мониторинга** плитки слева hello. Щелкните его toodrill вниз на информационную панель.

![Обзор](./media/log-analytics-dashboards/oms-dashboards-overview.png)

## <a name="adding-a-tile"></a>Добавление плитки
В разделе панелей мониторинга сведения на плитках берутся из сохраненных запросов поиска журналов. В службе OMS есть много уже готовых запросов поиска журналов, поэтому вы сможете сразу приступить к созданию панели мониторинга. Используйте hello описанных ниже действий, характеризующих как toobegin.

В hello Моя панель мониторинга представления, щелкните **Настройка** tooenter режим настройки.

![Инструкция в виде рисунков](./media/log-analytics-dashboards/oms-dashboards-pictorial01.png)

 Откроется hello правой части страницы приветствия Hello панель показывает все рабочую область сохраненных запросов поиска журналов. toovisualize сохраненный журнал поиска как плитку, наведите указатель мыши на сохраненные условия поиска и нажмите кнопку hello **, а также** символов.

![Добавление плиток 1](./media/log-analytics-dashboards/oms-dashboards-pictorial02.png)

При нажатии кнопки hello **, а также** symbol, новая Плитка отображается в hello представление Моя панель мониторинга.

![Добавление плиток 2](./media/log-analytics-dashboards/oms-dashboards-pictorial03.png)

## <a name="edit-a-tile"></a>Изменение плитки
В hello Моя панель мониторинга представления, щелкните **Настройка** tooenter режим настройки. Щелкните плитку hello требуется tooedit. Правая панель Hello изменения tooedit и обеспечивает выбор вариантов:

![Изменение плитки](./media/log-analytics-dashboards/oms-dashboards-pictorial04.png)

![Изменение плитки](./media/log-analytics-dashboards/oms-dashboards-pictorial05.png)

### <a name="tile-visualizations"></a>Визуализация плиток
Существует три вида toochoose визуализации плитки из:

| тип диаграммы | назначение |
| --- | --- |
| ![Линейчатая диаграмма](./media/log-analytics-dashboards/oms-dashboards-bar-chart.png) |Отображает временную шкалу результатов сохраненного поиска по журналу в виде линейчатой диаграммы или списка результатов по полям (зависит от того, сортирует ли поиск по журналу найденные результаты по полям). |
| ![метрика](./media/log-analytics-dashboards/oms-dashboards-metric.png) |На ней показывается число, которое означает, сколько раз был найден элемент по запросу поиска журнала. Плитки с метрикой позволяют tooset пороговое значение, которое будет выделяться плитки приветствия при достижении порога hello. |
| ![line](./media/log-analytics-dashboards/oms-dashboards-line.png) |Отображает временную шкалу совпадения результатов сохраненного поиска по журналу со значениями в виде графика. |

### <a name="threshold"></a>Пороговое значение
Пороговое значение можно создать на плитки с помощью hello визуализацию в виде метрики. Выберите toocreate пороговое значение на плитке приветствия. Выберите ли toohighlight hello карточки при hello значение — выше или ниже порогового значения выбранного hello, задайте пороговое значение hello ниже.

## <a name="organizing-hello-dashboard"></a>Упорядочение панели мониторинга hello
tooorganize перейдите toohello Моя панель мониторинга представления панели мониторинга и нажмите кнопку **Настройка** tooenter режим настройки. Щелкните и перетащите плитку hello нужны toomove и переместите его toowhere требуется вашей toobe плитки.

![Упорядочение панели мониторинга](./media/log-analytics-dashboards/oms-dashboards-organize.png)

## <a name="remove-a-tile"></a>Удаление плитки
tooremove плитки, перейдите в представление toohello Моя панель мониторинга и нажмите кнопку **Настройка** tooenter режим настройки. Плитка приветствия выберите tooremove и нажмите на правой панели hello выберите **удалить плитку**.

![Удаление плитки](./media/log-analytics-dashboards/oms-dashboards-remove-tile.png)

## <a name="next-steps"></a>Дальнейшие действия
* Создание [оповещения](log-analytics-alerts.md) в уведомлениях toogenerate анализа журналов и tooremediate проблем.
