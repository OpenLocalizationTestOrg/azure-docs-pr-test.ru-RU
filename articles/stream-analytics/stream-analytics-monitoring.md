---
title: "Мониторинг заданий Stream Analytics aaaUnderstanding | Документы Microsoft"
description: "Основные сведения о мониторинге заданий в Stream Analytics"
keywords: "монитор запросов"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 5f5cc00f-4a7b-491e-89e1-dbafea46d399
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 36819025c7b2ddbf4b9694522f1b4820407ca5f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="understand-stream-analytics-job-monitoring-and-how-toomonitor-queries"></a>Понимать мониторинг заданий Stream Analytics и как toomonitor запросов

## <a name="introduction-hello-monitor-page"></a>Введение: страница объектов наблюдения hello
Здравствуйте, оба области основные показатели производительности, можно использовать toomonitor и устранение производительность запросов и задания портал Azure. toosee этих показателей Обзор вы заинтересованы в просмотре метрик для и hello представление задания Stream Analytics toohello **мониторинг** на странице Общие сведения о hello.  

![Мониторинг связи](./media/stream-analytics-monitoring/02-stream-analytics-monitoring-block.png)

будет открыто окно приветствия, как показано:

![Панель мониторинга заданий](./media/stream-analytics-monitoring/01-stream-analytics-monitoring.png)  

## <a name="metrics-available-for-stream-analytics"></a>Метрики, доступные в Stream Analytics
| Метрика                 | Определение                               |
| ---------------------- | ---------------------------------------- |
| Использование единиц потоковой передачи (%)       | Использование Hello hello единиц потоковой передачи присвоено задания tooa вкладку "масштабирование" hello hello задания. Как только этот индикатор достигнет 80 % и более существует высокая вероятность приостановки или отсрочки обработки события. |
| Входные события           | Объем данных, полученных заданием Stream Analytics hello, в число событий. Это может быть используется toovalidate, что события отправляются toohello источника входных данных. |
| Выходные события          | Объем данных, посланных hello Stream Analytics задания toohello выходные данные целевого объекта, в число событий. |
| Неупорядоченные события    | Количество событий, полученных в неверном порядке, были удалены или получили скорректированную метку времени, основании hello политика порядок событий. Это могут быть затронуты hello настройку параметра hello неупорядоченная временной интервал. |
| Ошибки преобразования данных | Количество ошибок преобразования данных, возникших в задании Stream Analytics. |
| Ошибки среды выполнения         | Общее количество ошибок, которые происходят во время выполнения задания Stream Analytics Hello. |
| События позднего ввода      | Число событий, позднее, поступающих от источника hello, которое либо был удален или их отметки времени было изменено, на основе конфигурации политики порядок событий hello позднее событий, Наступивших приветствия. |
| Запросы функций      | Количество вызовов toohello функции машинного обучения Azure (при его наличии). |
| Неудачные запросы функций | Количество неудачных вызовов функции машинного обучения Azure (при наличии). |
| События функций        | Количество событий, отправленных toohello функции машинного обучения Azure (при его наличии). |
| Байты входного события      | Объем данных, полученных заданием Stream Analytics hello, в байтах. Это может быть используется toovalidate, что события отправляются toohello источника входных данных. |


## <a name="customizing-monitoring-in-hello-azure-portal"></a>Настройка мониторинга в hello портал Azure
Можно настроить тип диаграммы метрик отображается, hello и временной диапазон в параметрах hello изменить диаграмму. Дополнительные сведения см. в разделе [как tooCustomize мониторинг](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).

  ![Диаграмма значений времени в мониторе запросов](./media/stream-analytics-monitoring/08-stream-analytics-monitoring.png)  


## <a name="get-help"></a>Получение справки
Дополнительную помощь и поддержку вы можете получить на нашем [форуме Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Дальнейшие действия
* [Введение tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Приступая к работе с Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Масштабирование заданий в службе Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Справочник по языку запросов Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Справочник по API-интерфейсу REST управления Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

