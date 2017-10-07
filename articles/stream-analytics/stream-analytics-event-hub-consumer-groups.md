---
title: "aaaDebug Azure Stream Analytics с приемников концентратора событий | Документы Microsoft"
description: "Рассматривайте рекомендации по группам потребителей концентраторов событий в заданиях Stream Analytics."
keywords: "ограничение концентратора событий, группа потребителей"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 89821e6273151de43b5e42d907e547c939e24824
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="debug-azure-stream-analytics-with-event-hub-receivers"></a>Отладка Azure Stream Analytics с помощью приемников концентратора событий

Концентраторы событий Azure можно использовать в Azure Stream Analytics tooingest или выходных данных данные из задания. Для использования концентраторов событий рекомендуется toouse нескольких групп потребителей, tooensure задания масштабируемости. Одна из причин — что hello число читателей в задании Stream Analytics hello для определенных входных данных влияет на hello числа агентов чтения в группе одного получателя. точное число приемников Hello основан на внутренние сведения для логики топологию hello. Hello количества получателей не предоставляется извне. Hello числа агентов чтения можно изменить во время запуска задания hello или при обновлении задания.

> [!NOTE]
> При изменении hello числа агентов чтения во время обновления задания tooaudit журналы записываются предупреждения об временной. Задания Stream Analytics восстанавливаются от этих временных сбоев автоматически.

## <a name="number-of-readers-per-partition-exceeds-event-hubs-limit-of-five"></a>Число модулей чтения каждого раздела превышает предельно допустимое число концентраторов событий (пять)

Сценарии, в какие hello числа агентов чтения на каждую секцию превышает предел концентраторов событий hello пяти hello следующее:

* Несколько инструкций SELECT: при использовании нескольких инструкций SELECT, которые ссылаются слишком**же** ввода концентратора событий, каждая инструкция SELECT вызывает новый приемник toobe создан.
* ОБЪЕДИНЕНИЕ: При использовании ОБЪЕДИНЕНИЯ является возможные toohave несколько входов, которые ссылаются toohello **же** концентратора и потребителем группы событий.
* САМОСОЕДИНЕНИЕ: При использовании операции СОЕДИНЕНИЯ SELF, это возможно toorefer toohello **же** концентратора событий несколько раз.

## <a name="solution"></a>Решение

Hello следующие рекомендации могут помочь успешного выполнения сценариев, в которых hello числа агентов чтения на каждую секцию превышает предел концентраторов событий hello пяти.

### <a name="split-your-query-into-multiple-steps-by-using-a-with-clause"></a>Разбиение запроса на несколько шагов с помощью предложения WITH

предложение WITH Hello указывает временный именованный результирующий набор, который может ссылаться предложение FROM в запросе hello. Предложение WITH hello определить hello области выполнения одиночной инструкции SELECT.

Например, вместо этого запроса:

```
SELECT foo 
INTO output1
FROM inputEventHub

SELECT bar
INTO output2
FROM inputEventHub 
…
```

Используйте этот:

```
WITH input (
   SELECT * FROM inputEventHub
) as data

SELECT foo
INTO output1
FROM data

SELECT bar
INTO output2
FROM data
…
```

### <a name="ensure-that-inputs-bind-toodifferent-consumer-groups"></a>Убедитесь, что входные данные привязки toodifferent групп потребителей

Для запросов, в которых три или более входов не подключенных toohello же потребителей концентраторов событий группы, создать отдельный потребителя группы. Это требует создания hello дополнительных входных данных Stream Analytics.


## <a name="get-help"></a>Получение справки
Дополнительную помощь вы можете получить на нашем [форуме Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Дальнейшие действия
* [Введение tooStream аналитика](stream-analytics-introduction.md)
* [Приступая к работе с Azure Stream Analytics: выявление мошенничества в режиме реального времени](stream-analytics-real-time-fraud-detection.md)
* [Масштабирование заданий Azure Stream Analytics для повышения пропускной способности базы данных](stream-analytics-scale-jobs.md)
* [Stream Analytics Query Language Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx) (Справочник по языку запросов Stream Analytics)
* [Stream Analytics management REST API reference](https://msdn.microsoft.com/library/azure/dn835031.aspx) (Справочник по API-интерфейсу REST для управления Stream Analytics)
