---
title: "AAA Azure Stream Analytics управляемых данными отладку с помощью схемы задания hello | Документы Microsoft"
description: "Устранение неполадок в задание Stream Analytics с помощью схемы задания hello и метрики."
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 05/01/2017
ms.author: jeffstok
ms.openlocfilehash: 1af884d485bebb06b034da01a13f7f8240516571
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="data-driven-debugging-by-using-hello-job-diagram"></a>Отладка с использованием схемы hello задания на основе данных

Задание Hello к схеме для hello **мониторинг** колонки в hello Azure портал позволяет наглядно представить конвейер задания. На ней представлены сведения о входных и выходных данных, а также о шагах запроса. Можно использовать hello задания схемы tooexamine hello показатели для каждого шага, toomore быстро изолировать hello источник проблемы при устранении неполадок.

## <a name="using-hello-job-diagram"></a>С помощью схемы задания hello

В hello портал Azure при работе в задание Stream Analytics в группе **поддержки + Устранение неполадок**выберите **схема задания**:

![Схема заданий с метриками — расположение](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-1.png)

Выберите каждый шаг toosee hello соответствующего раздела запроса в запросе области редактирования. Диаграмма метрик для hello шаг отображается в нижней области на странице приветствия.

![Схема заданий с метриками — базовое задание](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-2.png)

Выберите секции hello toosee входа hello концентраторов событий Azure **...** Откроется контекстное меню. Также можно просмотреть входные слияния hello.

![Схема заданий с метриками — развертывание раздела](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-3.png)

toosee hello метрики диаграммы для только одной секции, узел раздела выберите hello. метрики Hello отображаются внизу hello страницы приветствия.

![Схема заданий с метриками — дополнительные метрики](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-4.png)

toosee hello диаграмма метрик для слияния, выберите hello узел слияния. Hello, следующая диаграмма показывает, что события не были удалены или изменены.

![Схема заданий с метриками — сетка](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-5.png)

сведения о hello toosee значение метрики hello и времени, toohello точки диаграммы.

![Схема заданий с метриками — наведение](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-6.png)

## <a name="troubleshoot-by-using-metrics"></a>Устранение неполадок с помощью метрик

Hello **QueryLastProcessedTime** Метрика показывает, когда конкретный шаг полученных данных. Просмотрев hello топологии, можно работать назад от hello toosee процессора на выходные данные шага не получает данные. Если шаг получает данные, перейдите toohello действия запроса перед его. Проверьте hello предыдущего действия запроса есть временное окно, и если прошло достаточно времени для него toooutput данных. (Обратите внимание, времени пребывание час привязанных toohello windows.)
 
Если hello действия предыдущего запроса, процессор ввода используйте hello ввода метрики toohelp ответов hello следующие целевые вопросы. о заданиях, получающих данные из источников входных данных. Если запрос hello секционирована, изучите каждой секции.
 
### <a name="how-much-data-is-being-read"></a>Какой объем данных считывается?

*   **InputEventsSourcesTotal** hello число единиц данных чтения. Например hello количество больших двоичных объектов.
*   **InputEventsTotal** hello число событий, которые чтения. Эта метрика доступна для каждого раздела.
*   **InputEventsInBytesTotal** hello число считанных байтов.
*   Метрика **InputEventsLastArrivalTime** обновляется после размещения в очереди каждого полученного события.
 
### <a name="is-time-moving-forward-if-actual-events-are-read-punctuation-might-not-be-issued"></a>Отсчитывается ли время? Если фактические события считываются, знаки препинания могут быть опущены.

*   **InputEventsLastPunctuationTime** указывает выдачи знакам препинания tookeep время перемещение вперед. Последовательность данных может быть заблокирована, если знаки препинания будут опущены.
 
### <a name="are-there-any-errors-in-hello-input"></a>Существуют ли ошибки во входном файле hello?

*   Метрика **InputEventsEventDataNullTotal** содержит число событий со значением null.
*   Метрика **InputEventsSerializerErrorsTotal** содержит число событий, десериализацию которых удалось выполнить правильно.
*   Метрика **InputEventsDegradedTotal** содержит число событий, в которых возникла ошибка, не связанная с десериализацией.
 
### <a name="are-events-being-dropped-or-adjusted"></a>Были ли события удалены или скорректированы?

*   **InputEventsEarlyTotal** hello число событий, которые имеют отметку времени приложения перед hello верхнего предела.
*   **InputEventsLateTotal** hello число событий, которые имеют отметку времени приложения после hello верхнего предела.
*   **InputEventsDroppedBeforeApplicationStartTimeTotal** номер события hello удалена перед выполнением время начала задания hello.
 
### <a name="are-we-falling-behind-in-reading-data"></a>Есть ли непрочитанные данные?

*   **InputEventsSourcesBackloggedTotal** сообщает, сколько дополнительные сообщения должны toobe чтения для концентраторов событий и центр IoT Azure входных данных.


## <a name="get-help"></a>Получение справки
Дополнительную помощь вы можете получить на нашем [форуме Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Дальнейшие действия
* [Введение tooStream аналитика](stream-analytics-introduction.md)
* [Приступая к работе с Azure Stream Analytics: выявление мошенничества в режиме реального времени](stream-analytics-real-time-fraud-detection.md)
* [Масштабирование заданий Azure Stream Analytics для повышения пропускной способности базы данных](stream-analytics-scale-jobs.md)
* [Stream Analytics Query Language Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx) (Справочник по языку запросов Stream Analytics)
* [Stream Analytics management REST API reference](https://msdn.microsoft.com/library/azure/dn835031.aspx) (Справочник по API-интерфейсу REST для управления Stream Analytics)
