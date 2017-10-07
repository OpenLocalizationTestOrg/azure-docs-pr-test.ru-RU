---
title: "aaaOverview метрик в Microsoft Azure | Документы Microsoft"
description: "Узнайте, как мониторинг toocustomize диаграммы в Azure."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: c36031eb-4df5-4cd5-9479-311d493a40d2
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: robb
ms.openlocfilehash: 4196b2e9bda713e9a0abc349eed78685abcaf194
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-metrics-in-microsoft-azure"></a>Обзор метрик в Microsoft Azure
Всем службам Azure отслеживать ключевые показатели, которые позволяют вам toomonitor hello состояния, производительности, доступности и использования служб. Можно просмотреть эти показатели в hello портал Azure, и можно также использовать hello [API-интерфейса REST](https://msdn.microsoft.com/library/azure/dn931930.aspx) или [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooaccess hello полного набора метрик, программными средствами.

Для некоторых служб может понадобиться tooturn диагностику в порядке toosee каких-либо метрик. В других языках, таких как виртуальные машины вы получите базового набора метрик, но требуется tooenable hello полный набор метрик высокой частотой. В разделе [включить наблюдение и диагностику](insights-how-to-use-diagnostics.md) toolearn дополнительные.

## <a name="using-monitoring-charts"></a>Использование диаграмм мониторинга
Диаграмма любой из метрик hello может их за любой период времени, можно выбрать.

1. В hello [портала Azure](https://portal.azure.com/), нажмите кнопку **Обзор**, и затем ресурса вы заинтересованы в мониторинге.
2. Hello **мониторинг** раздел содержит hello наиболее важные показатели для каждого ресурса Azure. Например, у веб-приложения есть **запросы и ошибки**, а у виртуальной машины — **процент использования ЦП** и **операции чтения и записи диска**: ![группа связанных элементов "Мониторинг"](./media/insights-how-to-customize-monitoring/Insights_MonitoringChart.png)
3. Щелкнув любой диаграмме будет отображаться вы hello **метрика** колонку. В колонке hello Кроме toohello graph — это таблица, показывающую агрегаты hello показателей (например, среднего, минимального и максимального диапазона времени hello выбранный вами). Ниже, являются hello правил оповещений для ресурса hello.
    ![Колонка "Метрика"](./media/insights-how-to-customize-monitoring/Insights_MetricBlade.png)
4. toocustomize hello строк, которые отображаются, щелкните hello **изменить** кнопку на диаграмме hello, или hello **изменение диаграммы** на колонка метрики hello.
5. В колонке hello изменить запрос можно выполнить три действия:
   
   * Изменить диапазон времени hello
   * Переключение внешний вид hello между строке и строки
   * выбрать другие метрики. ![Изменение запроса](./media/insights-how-to-customize-monitoring/Insights_EditQuery.png)
6. Изменение интервала времени hello так же легко, как при выборе другого диапазона (такие как **последний час**) и щелкнув **Сохранить** hello нижней части колонки hello. Вы также можете **настраиваемый**, что позволяет toochoose любого периода времени по hello последних двух недель. Например можно увидеть hello всего две недели или 1 часу за вчера. Введите в поле tooenter hello текст другого час.
    ![Настраиваемый интервал времени](./media/insights-how-to-customize-monitoring/Insights_CustomTime.png)
7. Ниже диапазона времени hello канал можно выбрать любое количество tooshow метрик на диаграмме hello.
8. При нажатии кнопки "Сохранить" будут сохранены изменения для данного ресурса. Например если у вас есть две виртуальные машины и изменить диаграмму на одном, он не влияет на hello других.

## <a name="creating-side-by-side-charts"></a>Создание диаграмм, расположенных рядом друг с другом
Hello мощные hello портала можно добавить столько диаграмм.

1. В hello **...**  меню hello верхней части колонки щелкните hello **Добавление плиток**:  
    ![Меню "Добавить"](./media/insights-how-to-customize-monitoring/Insights_AddMenu.png)
2. Затем, то можно выбрать выбрать диаграмму hello **коллекции** hello правой части экрана: ![коллекции](./media/insights-how-to-customize-monitoring/Insights_Gallery.png)
3. Если вы не видите hello показателя, всегда можно добавить одним из hello предустановленный набор метрик и **изменить** hello диаграммы tooshow hello метрику, необходимо.

## <a name="monitoring-usage-quotas"></a>Мониторинг квот использования
Большинство метрик показывают тенденции во времени, но некоторые данные, например квоты на использование, представляют собой сведения на определенный момент времени с пороговым значением.

Также можно увидеть квоты на использование hello колонке ресурсов, которые назначены квоты:

![Использование](./media/insights-how-to-customize-monitoring/Insights_UsageChart.png)

Как с метриками, можно использовать hello [API-интерфейса REST](https://msdn.microsoft.com/library/azure/dn931963.aspx) или [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooaccess hello полный набор квот на использование программного.

## <a name="next-steps"></a>Дальнейшие действия
* [Получайте уведомления](insights-receive-alert-notifications.md) , когда метрика достигает порогового значения.
* [Включить наблюдение и диагностику](insights-how-to-use-diagnostics.md) toocollect подробные показатели высокой частотой в службе.
* [Автоматически масштабировать числа экземпляров](insights-how-to-scale.md) toomake убедиться, что служба становится доступной и отвечать на запросы.
* [Контролировать производительность приложений](../application-insights/app-insights-azure-web-apps.md) Если toounderstand точно как код работает в облаке hello.
* Используйте [Application Insights для приложений JavaScript и веб-страницы](../application-insights/app-insights-web-track-usage.md) tooget аналитика клиента о браузерах hello, посетите веб-страницу.
* [Отслеживайте доступность и скорость реагирования любой веб-страницы](../application-insights/app-insights-monitor-web-app-availability.md) с помощью Application Insights, так вы сможете узнать, что страница не работает.

