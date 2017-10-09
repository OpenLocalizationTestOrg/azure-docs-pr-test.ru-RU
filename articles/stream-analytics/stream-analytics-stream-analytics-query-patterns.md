---
title: "Примеры aaaQuery для распространенных шаблонов использования в Stream Analytics | Документы Microsoft"
description: "Общие шаблоны запросов Azure Stream Analytics"
keywords: "примеры запросов"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jenniehubbard
editor: cgronlun
ms.assetid: 6b9a7d00-fbcc-42f6-9cbb-8bbf0bbd3d0e
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/08/2017
ms.author: jenniehubbard
ms.openlocfilehash: c8f7a8ac661eaf0281f4140b02c42141b73040fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="query-examples-for-common-stream-analytics-usage-patterns"></a>Примеры запросов для распространенных шаблонов использования Stream Analytics
## <a name="introduction"></a>Введение
Запросы в Azure Stream Analytics выражаются на языке запросов на основе SQL. Эти запросы, описаны в hello [Справочник по языку запросов Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx) руководства. Это статье структуры решения tooseveral распространенными шаблонами запросов, на основе реальных сценариев. Он является незавершенным и по-прежнему toobe обновляется новых шаблонов на постоянной основе.

## <a name="query-example-convert-data-types"></a>Пример запроса: преобразование типов данных
**Описание**: определение типов hello свойств на hello входного потока.
Например, веса автомобиля hello поступает на hello входного потока, как строки и должен преобразовать слишком toobe**INT** tooperform **сумма** его.

**Входные данные**

| Убедитесь, | Время | Вес |
| --- | --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |"1000" |
| Honda |2015-01-01T00:00:02.0000000Z |"2000" |

**Выходные данные**:

| Убедитесь, | Вес |
| --- | --- |
| Honda |3000 |

**Решение**

    SELECT
        Make,
        SUM(CAST(Weight AS BIGINT)) AS Weight
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

**Объяснение**: использование **ПРИВЕДЕНИЯ** инструкции в hello **вес** его тип данных поля toospecify. Просмотреть список поддерживаемых типов данных в hello [типы данных (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835065.aspx).

## <a name="query-example-use-likenot-like-toodo-pattern-matching"></a>Пример запроса: используйте Like или Not как toodo соответствие шаблону
**Описание**: Проверьте, что значение поля для hello событие соответствует определенному шаблону.
Например проверьте, результат hello возвращает форм лицензии, которые начинаются с и заканчиваться 9.

**Входные данные**

| Убедитесь, | LicensePlate | Время |
| --- | --- | --- |
| Honda |ABC-123 |2015-01-01T00:00:01.0000000Z |
| Toyota |AAA-999 |2015-01-01T00:00:02.0000000Z |
| Nissan |ABC-369 |2015-01-01T00:00:03.0000000Z |

**Выходные данные**:

| Убедитесь, | LicensePlate | Время |
| --- | --- | --- |
| Toyota |AAA-999 |2015-01-01T00:00:02.0000000Z |
| Nissan |ABC-369 |2015-01-01T00:00:03.0000000Z |

**Решение**

    SELECT
        *
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LicensePlate LIKE 'A%9'

**Объяснение**: hello используйте **как** hello инструкции toocheck **LicensePlate** значение поля. Оно должно начинаться с А, затем должна идти любая строка из нуля или более символов и, наконец, цифра 9. 

## <a name="query-example-specify-logic-for-different-casesvalues-case-statements"></a>Пример запроса: укажите логику для различных случаев и значений (операторы CASE)
**Описание.** Укажите разные вычисления для поля на основе определенных условий.
Например введите описание строки сколько автомобили hello одинаковы, переданный особый случай 1.

**Входные данные**

| Убедитесь, | Время |
| --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |
| Toyota |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:03.0000000Z |

**Выходные данные**:

| CarsPassed | Время |
| --- | --- | --- |
| 1 Honda |2015-01-01T00:00:10.0000000Z |
| 2 Toyota |2015-01-01T00:00:10.0000000Z |

**Решение**

    SELECT
        CASE
            WHEN COUNT(*) = 1 THEN CONCAT('1 ', Make)
            ELSE CONCAT(CAST(COUNT(*) AS NVARCHAR(MAX)), ' ', Make, 's')
        END AS CarsPassed,
        System.TimeStamp AS Time
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

**Объяснение**: hello **случай** предложение позволяет нам tooprovide различных вычислений на основе определенных критериев (в нашем случае hello число автомобилей hello в окне статистические hello).

## <a name="query-example-send-data-toomultiple-outputs"></a>Пример запроса: Отправка выводит toomultiple данных
**Описание**: toomultiple отправки данных выходные данные целевых объектов из одного задания.
Например анализа данных для предупреждения на основе пороговых значений и архивное хранилище tooblob все события.

**Входные данные**

| Убедитесь, | Время |
| --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |
| Honda |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:01.0000000Z |
| Toyota |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:03.0000000Z |

**Выходные данные 1**:

| Убедитесь, | Время |
| --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |
| Honda |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:01.0000000Z |
| Toyota |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:03.0000000Z |

**Выходные данные 2**:

| Убедитесь, | Время | Count |
| --- | --- | --- |
| Toyota |2015-01-01T00:00:10.0000000Z |3 |

**Решение**

    SELECT
        *
    INTO
        ArchiveOutput
    FROM
        Input TIMESTAMP BY Time

    SELECT
        Make,
        System.TimeStamp AS Time,
        COUNT(*) AS [Count]
    INTO
        AlertOutput
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)
    HAVING
        [Count] >= 3

**Объяснение**: hello **INTO** предложение сообщает Stream Analytics, который hello выводит данные toofrom toowrite hello этой инструкции.
первый запрос Hello является сквозной данных hello, мы получили tooan выхода, который мы назвали **ArchiveOutput**.
второй запрос Hello простой статистическую обработку и фильтрации и выполняет его отправляет результаты hello tooa подчиненных системой предупреждений.

Обратите внимание, что можно также повторно использовать результаты hello hello обобщенные табличные выражения (CTE) (такие как **WITH** операторов) в нескольких операторах выходных данных. Этот параметр имеет hello дополнительное преимущество открытия входного источника toohello меньшее число модулей чтения.
Например: 

    WITH AllRedCars AS (
        SELECT
            *
        FROM
            Input TIMESTAMP BY Time
        WHERE
            Color = 'red'
    )
    SELECT * INTO HondaOutput FROM AllRedCars WHERE Make = 'Honda'
    SELECT * INTO ToyotaOutput FROM AllRedCars WHERE Make = 'Toyota'

## <a name="query-example-count-unique-values"></a>Пример запроса: подсчет уникальных значений
**Описание**: количество hello уникальное поле значений, отображаемых в потоке hello в за период времени.
Например сколько уникальных делает автомобилей, передаются через кабинку hello в окне второй 2?

**Входные данные**

| Убедитесь, | Время |
| --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |
| Honda |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:01.0000000Z |
| Toyota |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:03.0000000Z |

**Выходные данные:**

| Count | Время |
| --- | --- |
| 2 |2015-01-01T00:00:02.000Z |
| 1 |2015-01-01T00:00:04.000Z |

**Решение.**

````
SELECT
     COUNT(DISTINCT Make) AS CountMake,
     System.TIMESTAMP AS TIME
FROM Input TIMESTAMP BY TIME
GROUP BY 
     TumblingWindow(second, 2)
````


**Описание:**
**COUNT (DISTINCT сделать)** Здравствуйте, возвращает количество уникальных значений в hello **сделать** столбец в пределах периода времени.

## <a name="query-example-determine-if-a-value-has-changed"></a>Пример запроса: определение изменения значения
**Описание**: просмотрите предыдущие toodetermine значение, если он отличается от текущего значения hello.
Например включен hello платный road приветствия же внесите текущего car hello предыдущих car hello?

**Входные данные**

| Убедитесь, | Время |
| --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |
| Toyota |2015-01-01T00:00:02.0000000Z |

**Выходные данные**:

| Убедитесь, | Время |
| --- | --- |
| Toyota |2015-01-01T00:00:02.0000000Z |

**Решение**

    SELECT
        Make,
        Time
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(minute, 1)) <> Make

**Объяснение**: использование **ЗАПАЗДЫВАНИЯ** toopeek в hello входной поток обратно в одно событие и получить hello **сделать** значение. Сравните его toohello **сделать** значение для hello текущего события и события hello выходные данные, если они отличаются.

## <a name="query-example-find-hello-first-event-in-a-window"></a>Пример запроса: hello найти первое событие в окне
**Описание**: поиск hello автомобиль в каждые 10 минут.

**Входные данные**

| LicensePlate | Убедитесь, | Время |
| --- | --- | --- |
| DXE 5291 |Honda |2015-07-27T00:00:05.0000000Z |
| YZK 5704 |Ford |2015-07-27T00:02:17.0000000Z |
| RMV 8282 |Honda |2015-07-27T00:05:01.0000000Z |
| YHN 6970 |Toyota |2015-07-27T00:06:00.0000000Z |
| VFE 1616 |Toyota |2015-07-27T00:09:31.0000000Z |
| QYF 9358 |Honda |2015-07-27T00:12:02.0000000Z |
| MDR 6128 |BMW |2015-07-27T00:13:45.0000000Z |

**Выходные данные**:

| LicensePlate | Убедитесь, | Время |
| --- | --- | --- |
| DXE 5291 |Honda |2015-07-27T00:00:05.0000000Z |
| QYF 9358 |Honda |2015-07-27T00:12:02.0000000Z |

**Решение**

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) = 1

Теперь создадим изменение hello проблему и найти hello автомобиль конкретной каждые 10 минут.

| LicensePlate | Убедитесь, | Время |
| --- | --- | --- |
| DXE 5291 |Honda |2015-07-27T00:00:05.0000000Z |
| YZK 5704 |Ford |2015-07-27T00:02:17.0000000Z |
| YHN 6970 |Toyota |2015-07-27T00:06:00.0000000Z |
| QYF 9358 |Honda |2015-07-27T00:12:02.0000000Z |
| MDR 6128 |BMW |2015-07-27T00:13:45.0000000Z |

**Решение**

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) OVER (PARTITION BY Make) = 1

## <a name="query-example-find-hello-last-event-in-a-window"></a>Пример запроса: поиск hello последнего события в окне
**Описание**: hello поиска последнего автомобиля в каждые 10 минут.

**Входные данные**

| LicensePlate | Убедитесь, | Время |
| --- | --- | --- |
| DXE 5291 |Honda |2015-07-27T00:00:05.0000000Z |
| YZK 5704 |Ford |2015-07-27T00:02:17.0000000Z |
| RMV 8282 |Honda |2015-07-27T00:05:01.0000000Z |
| YHN 6970 |Toyota |2015-07-27T00:06:00.0000000Z |
| VFE 1616 |Toyota |2015-07-27T00:09:31.0000000Z |
| QYF 9358 |Honda |2015-07-27T00:12:02.0000000Z |
| MDR 6128 |BMW |2015-07-27T00:13:45.0000000Z |

**Выходные данные**:

| LicensePlate | Убедитесь, | Время |
| --- | --- | --- |
| VFE 1616 |Toyota |2015-07-27T00:09:31.0000000Z |
| MDR 6128 |BMW |2015-07-27T00:13:45.0000000Z |

**Решение**

    WITH LastInWindow AS
    (
        SELECT 
            MAX(Time) AS LastEventTime
        FROM 
            Input TIMESTAMP BY Time
        GROUP BY 
            TumblingWindow(minute, 10)
    )
    SELECT 
        Input.LicensePlate,
        Input.Make,
        Input.Time
    FROM
        Input TIMESTAMP BY Time 
        INNER JOIN LastInWindow
        ON DATEDIFF(minute, Input, LastInWindow) BETWEEN 0 AND 10
        AND Input.Time = LastInWindow.LastEventTime

**Объяснение**: hello запроса состоит из двух шагов. Hello первый один находит hello последняя отметка времени в windows 10 минут. второй шаг соединения Hello hello результаты первого запроса hello hello исходный поток toofind hello событий, которые соответствуют hello последней отметки времени в каждом окне. 

## <a name="query-example-detect-hello-absence-of-events"></a>Пример запроса: hello отсутствие событий обнаружения
**Описание.** Убедитесь, что в потоке отсутствует значение, соответствующее определенным условиям.
Например 2 последовательные cars из приветствия одинаковы введенные road платный hello в hello последние 90 секунд?

**Входные данные**

| Убедитесь, | LicensePlate | Время |
| --- | --- | --- |
| Honda |ABC-123 |2015-01-01T00:00:01.0000000Z |
| Honda |AAA-999 |2015-01-01T00:00:02.0000000Z |
| Toyota |DEF-987 |2015-01-01T00:00:03.0000000Z |
| Honda |GHI-345 |2015-01-01T00:00:04.0000000Z |

**Выходные данные**:

| Убедитесь, | Время | CurrentCarLicensePlate | FirstCarLicensePlate | FirstCarTime |
| --- | --- | --- | --- | --- |
| Honda |2015-01-01T00:00:02.0000000Z |AAA-999 |ABC-123 |2015-01-01T00:00:01.0000000Z |

**Решение**

    SELECT
        Make,
        Time,
        LicensePlate AS CurrentCarLicensePlate,
        LAG(LicensePlate, 1) OVER (LIMIT DURATION(second, 90)) AS FirstCarLicensePlate,
        LAG(Time, 1) OVER (LIMIT DURATION(second, 90)) AS FirstCarTime
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(second, 90)) = Make

**Объяснение**: использование **ЗАПАЗДЫВАНИЯ** toopeek в hello входной поток обратно в одно событие и получить hello **сделать** значение. Сравните его toohello **сделать** значение в hello текущего события, а затем выходное событие hello, если они являются hello таким же. Можно также использовать **ЗАПАЗДЫВАНИЯ** tooget данных о предыдущих car hello.

## <a name="query-example-detect-hello-duration-between-events"></a>Пример запроса: обнаружить hello время между событиями
**Описание**: найти hello длительность для данного события. Например имея навигации web, определите hello время, затраченное на компонент.

**Входные данные**  

| Пользователь | Функция | Событие | Время |
| --- | --- | --- | --- |
| user@location.com |RightMenu |Начало |2015-01-01T00:00:01.0000000Z |
| user@location.com |RightMenu |End |2015-01-01T00:00:08.0000000Z |

**Выходные данные**:  

| Пользователь | Функция | Длительность |
| --- | --- | --- |
| user@location.com |RightMenu |7 |

**Решение**

````
    SELECT
        [user], feature, DATEDIFF(second, LAST(Time) OVER (PARTITION BY [user], feature LIMIT DURATION(hour, 1) WHEN Event = 'start'), Time) as duration
    FROM input TIMESTAMP BY Time
    WHERE
        Event = 'end'
````

**Объяснение**: hello используйте **ПОСЛЕДНЕГО** последние функции tooretrieve hello **время** значение в тип событий, hello **запустить**. Hello **последний** функция использует **PARTITION BY [пользователь]** tooindicate, hello результат вычисляется на уникальный пользователя. Hello запрос имеет максимальное пороговое значение 1 час hello разницу во времени между **запустить** и **остановить** события, но можно изменить при необходимости **(ограничение DURATION(hour, 1)**.

## <a name="query-example-detect-hello-duration-of-a-condition"></a>Пример запроса: определить длительность hello условия
**Описание.** Определите продолжительность условия.
Предположим, произошла ошибка, которая привела к неправильному отображению массы всех автомобилей (больше 9 тонн). Мы хотим длительность hello toocompute ошибки hello.

**Входные данные**

| Убедитесь, | Время | Вес |
| --- | --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |2000 |
| Toyota |2015-01-01T00:00:02.0000000Z |25000 |
| Honda |2015-01-01T00:00:03.0000000Z |26000 |
| Toyota |2015-01-01T00:00:04.0000000Z |25000 |
| Honda |2015-01-01T00:00:05.0000000Z |26000 |
| Toyota |2015-01-01T00:00:06.0000000Z |25000 |
| Honda |2015-01-01T00:00:07.0000000Z |26000 |
| Toyota |2015-01-01T00:00:08.0000000Z |2000 |

**Выходные данные**:

| StartFault | EndFault |
| --- | --- |
| 2015-01-01T00:00:02.000Z |2015-01-01T00:00:07.000Z |

**Решение**

````
    WITH SelectPreviousEvent AS
    (
    SELECT
    *,
        LAG([time]) OVER (LIMIT DURATION(hour, 24)) as previousTime,
        LAG([weight]) OVER (LIMIT DURATION(hour, 24)) as previousWeight
    FROM input TIMESTAMP BY [time]
    )

    SELECT 
        LAG(time) OVER (LIMIT DURATION(hour, 24) WHEN previousWeight < 20000 ) [StartFault],
        previousTime [EndFault]
    FROM SelectPreviousEvent
    WHERE
        [weight] < 20000
        AND previousWeight > 20000
````

**Объяснение**: использование **ЗАПАЗДЫВАНИЯ** tooview hello входного потока на 24 часа и выполните поиск экземпляров where **StartFault** и **StopFault** занимаемых hello Вес < 20000.

## <a name="query-example-fill-missing-values"></a>Пример запроса: заполнить отсутствующие значения
**Описание**: hello поток событий, в которых отсутствуют значения, создают поток событий с регулярными интервалами.
Например можно создайте событие каждые 5 секунд, которое сообщает hello недавно обнаружена точка данных.

**Входные данные**

| t | value |
| --- | --- |
| "2014-01-01T06:01:00" |1 |
| "2014-01-01T06:01:05" |2 |
| "2014-01-01T06:01:10" |3 |
| "2014-01-01T06:01:15" |4 |
| "2014-01-01T06:01:30" |5 |
| "2014-01-01T06:01:35" |6 |

**Выходные данные (первые 10 строк)**:

| windowend | lastevent.t | lastevent.value |
| --- | --- | --- |
| 2014-01-01T14:01:00.000Z |2014-01-01T14:01:00.000Z |1 |
| 2014-01-01T14:01:05.000Z |2014-01-01T14:01:05.000Z |2 |
| 2014-01-01T14:01:10.000Z |2014-01-01T14:01:10.000Z |3 |
| 2014-01-01T14:01:15.000Z |2014-01-01T14:01:15.000Z |4 |
| 2014-01-01T14:01:20.000Z |2014-01-01T14:01:15.000Z |4 |
| 2014-01-01T14:01:25.000Z |2014-01-01T14:01:15.000Z |4 |
| 2014-01-01T14:01:30.000Z |2014-01-01T14:01:30.000Z |5 |
| 2014-01-01T14:01:35.000Z |2014-01-01T14:01:35.000Z |6 |
| 2014-01-01T14:01:40.000Z |2014-01-01T14:01:35.000Z |6 |
| 2014-01-01T14:01:45.000Z |2014-01-01T14:01:35.000Z |6 |

**Решение**

    SELECT
        System.Timestamp AS windowEnd,
        TopOne() OVER (ORDER BY t DESC) AS lastEvent
    FROM
        input TIMESTAMP BY t
    GROUP BY HOPPINGWINDOW(second, 300, 5)


**Объяснение**: этот запрос приводит к возникновению события каждые 5 секунд и выходы hello последнего события, который ранее был получен. Hello [окна «прыгающие» окна](https://msdn.microsoft.com/library/dn835041.aspx "окна «прыгающие» окна — Azure Stream Analytics") длительность определяет, насколько далеко назад hello запрос выглядит toofind hello последнее событие (300 секунд, в этом примере).

## <a name="get-help"></a>Получение справки
За дополнительной помощью обращайтесь на наш [форум Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Дальнейшие действия
* [Введение tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Приступая к работе с Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Масштабирование заданий в службе Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Справочник по языку запросов Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Справочник по API-интерфейсу REST управления Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

