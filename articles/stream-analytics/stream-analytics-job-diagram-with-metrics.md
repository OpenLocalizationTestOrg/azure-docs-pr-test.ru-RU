---
title: "Отладка на основе данных в Azure Stream Analytics с помощью схемы заданий | Документация Майкрософт"
description: "Устраняйте неполадки задания Stream Analytics с помощью схемы и метрик заданий."
keywords: 
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 05/01/2017
ms.author: samacha
ms.openlocfilehash: 5b689c07bf8baa531c7a50ca50ed5140c1787e7b
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="data-driven-debugging-by-using-the-job-diagram"></a>Отладка на основе данных с помощью схемы заданий

Схема заданий в колонке **Мониторинг** на портале Azure может вам помочь визуализировать конвейер заданий. На ней представлены сведения о входных и выходных данных, а также о шагах запроса. С помощью схемы заданий можно проанализировать метрики на каждом шаге, чтобы быстро выявить источник проблемы при устранении неполадок.

## <a name="using-the-job-diagram"></a>Использование схемы заданий

На портале Azure в задании Stream Analytics в разделе **Поддержка и устранение неполадок** выберите **Схема заданий**:

![Схема заданий с метриками — расположение](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-1.png)

Выберите каждый шаг запроса, чтобы отобразить соответствующий раздел в области изменения запроса. В нижней области на странице отображается диаграмма метрик для шага.

![Схема заданий с метриками — базовое задание](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-2.png)

Для просмотра разделов входных данных концентраторов событий Azure выберите **...** Откроется контекстное меню. Кроме того, отобразится инструмент слияния входных данных.

![Схема заданий с метриками — развертывание раздела](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-3.png)

Чтобы просмотреть схему с метриками для одного раздела, выберите его узел. Метрики отображаются в нижней части страницы.

![Схема заданий с метриками — дополнительные метрики](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-4.png)

Чтобы увидеть схему метрик для слияния, выберите узел слияния. На следующей схеме видно, что события не были удалены или скорректированы.

![Схема заданий с метриками — сетка](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-5.png)

Чтобы просмотреть значения метрик и время, наведите указатель мыши на схему.

![Схема заданий с метриками — наведение](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-6.png)

## <a name="troubleshoot-by-using-metrics"></a>Устранение неполадок с помощью метрик

Метрика **QueryLastProcessedTime** указывает, на каком конкретном шаге были переданы данные. Учитывая топологию, вы можете проанализировать обратный процесс выполнения (начиная от обработчика выходных данных), чтобы понять, на каком шаге данные не передаются. Если данные на шаге не передавались, перейдите к шагу запроса перед текущим шагом. Проверьте, задано ли на предыдущем шаге запроса временное окно и достаточно ли было времени для вывода данных. Учтите, что временные окна имеют почасовую привязку.
 
Если на предыдущем этапе не обрабатываются входящие данные, используйте входные метрики, чтобы получить ответ на следующие вопросы о заданиях, получающих данные из источников входных данных. Если запрос разделен, проверьте каждый раздел.
 
### <a name="how-much-data-is-being-read"></a>Какой объем данных считывается?

*   **InputEventsSourcesTotal** содержит число прочитанных единиц данных, например больших двоичных объектов.
*   Метрика **InputEventsTotal** содержит число прочитанных событий. Эта метрика доступна для каждого раздела.
*   Метрика **InputEventsInBytesTotal** содержит число прочитанных байтов.
*   Метрика **InputEventsLastArrivalTime** обновляется после размещения в очереди каждого полученного события.
 
### <a name="is-time-moving-forward-if-actual-events-are-read-punctuation-might-not-be-issued"></a>Отсчитывается ли время? Если фактические события считываются, знаки препинания могут быть опущены.

*   Метрика **InputEventsLastPunctuationTime** указывает, когда знаки препинания используются для отсчета времени. Последовательность данных может быть заблокирована, если знаки препинания будут опущены.
 
### <a name="are-there-any-errors-in-the-input"></a>Есть ли ошибки во входных данных?

*   Метрика **InputEventsEventDataNullTotal** содержит число событий со значением null.
*   Метрика **InputEventsSerializerErrorsTotal** содержит число событий, десериализацию которых удалось выполнить правильно.
*   Метрика **InputEventsDegradedTotal** содержит число событий, в которых возникла ошибка, не связанная с десериализацией.
 
### <a name="are-events-being-dropped-or-adjusted"></a>Были ли события удалены или скорректированы?

*   Метрика **InputEventsEarlyTotal** содержит число событий с меткой времени для приложения до верхнего предела.
*   Метрика **InputEventsLateTotal** содержит число событий с меткой времени для приложения после верхнего предела.
*   Метрика **InputEventsDroppedBeforeApplicationStartTimeTotal** содержит число событий, удаленных до начала выполнения задания.
 
### <a name="are-we-falling-behind-in-reading-data"></a>Есть ли непрочитанные данные?

*   Метрика **InputEventsSourcesBackloggedTotal** сообщает, сколько сообщений должен прочитать концентратор событий, а также входные данные Центра Интернета вещей Azure.


## <a name="get-help"></a>Получение справки
Дополнительную помощь вы можете получить на нашем [форуме Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Дальнейшие действия
* [Что такое Stream Analytics?](stream-analytics-introduction.md)
* [Приступая к работе с Azure Stream Analytics: выявление мошенничества в режиме реального времени](stream-analytics-real-time-fraud-detection.md)
* [Масштабирование заданий Azure Stream Analytics для повышения пропускной способности базы данных](stream-analytics-scale-jobs.md)
* [Stream Analytics Query Language Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx) (Справочник по языку запросов Stream Analytics)
* [Stream Analytics management REST API reference](https://msdn.microsoft.com/library/azure/dn835031.aspx) (Справочник по API-интерфейсу REST для управления Stream Analytics)
