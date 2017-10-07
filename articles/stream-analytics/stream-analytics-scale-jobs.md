---
title: "пропускная способность для tooincrease заданий Stream Analytics aaaScale | Документы Microsoft"
description: "Узнайте, как tooscale заданий Stream Analytics, настроив входной секций, помощник по настройке определение запроса hello и установив задания единицы потоковой передачи."
keywords: "потоковая передача данных, обработка потоковой передачи данных, настройка аналитики"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 7e857ddb-71dd-4537-b7ab-4524335d7b35
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/22/2017
ms.author: jeffstok
ms.openlocfilehash: 4ba8f6b2f8bfebd52cfa07696b501b42cda21f75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="scale-azure-stream-analytics-jobs-tooincrease-stream-data-processing-throughput"></a>Масштабирование Azure Stream Analytics задания tooincrease поток обработки данных пропускной способности
В этой статье показано, как tootune Stream Analytics запрос tooincrease пропускной способности для задания Streaming Analytics. Вы узнаете, как задания tooscale Stream Analytics, настроив входной секций, определение запроса настройки аналитики hello и расчета и задания задания *единицы потоковой передачи* (SUs). 

## <a name="what-are-hello-parts-of-a-stream-analytics-job"></a>Что такое hello части задания Stream Analytics
Определение задания Stream Analytics включает запрос, а также входные и выходные данные. Входные данные:, где задания hello считывает hello поток данных из. Hello запроса используется tootransform hello данных входной поток, который вывода hello где задания hello отправляет результаты задания hello.  

Задание требует по крайней мере один источник входных данных для потока данных. Hello источник входного потока данных могут храниться в концентратор событий Azure или в хранилище больших двоичных объектов. Дополнительные сведения см. в разделе [tooAzure введение Stream Analytics](stream-analytics-introduction.md) и [приступить к использованию Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md).

## <a name="partitions-in-event-hubs-and-azure-storage"></a>Секции в концентраторах событий и в хранилище Azure
Масштабирование задания Stream Analytics использует секций в hello вход или выход. Секционирование позволяет разделить данные на подмножества на основе ключа секции. Процесс, который использует данные hello (например, задание Streaming Analytics) можно использовать и записи различных секций параллельно, что повышает производительность. При работе со Streaming Analytics можно воспользоваться преимуществами секционирования в концентраторах событий и в хранилище BLOB-объектов. 

Дополнительные сведения о секциях см. в разделе hello в следующих статьях:

* [Обзор функций концентраторов событий](../event-hubs/event-hubs-features.md#partitions)
* [Секционирование данных](https://docs.microsoft.com/azure/architecture/best-practices/data-partitioning#partitioning-azure-blob-storage)


## <a name="streaming-units-sus"></a>Единицы потоковой передачи
Единицы (SUs) представляют Привет ресурсов потоковой передачи и вычислительной мощности, которые требуются в порядок tooexecute задание Azure Stream Analytics. SUs предоставляет способ toodescribe hello относительный событий производительности на основе на смешанном показателе ЦП, памяти, обработки и чтения, а также скорости записи. Каждый SU соответствует tooroughly 1 МБ/с пропускной способности. 

Выбор количества SUs необходимы для конкретного задания зависит от конфигурации hello секции для входных данных hello и hello запрос, определенный для задания hello. Можно выбрать копирование tooyour квоты в SUs для задания. По умолчанию каждая подписка Azure имеет квоту копирование SUs too50 для всех заданий analytics hello в определенном регионе. tooincrease SUs для ваших подписок за эту квоту, обратитесь к [поддержки Майкрософт](http://support.microsoft.com). Для задания допустимые значения количества начинаются с 1, 3, 6 и затем по возрастающей с шагом в 6.

## <a name="embarrassingly-parallel-jobs"></a>Задания с усложненным параллелизмом
*Неудобно параллельные* задания является сценарием максимально масштабируемые hello, у нас есть в Azure Stream Analytics. Подключение одной секции экземпляр входной tooone hello раздела tooone запроса hello hello выходных данных. Это параллелизм имеет hello следующие требования:

1. Если логику запроса зависит от hello ключ обрабатывается по hello же экземпляр запроса, необходимо убедиться, что события hello проходят toohello одной секции входные данные. Для концентраторов событий, это означает, что данные события hello должен иметь hello **PartitionKey** заданным значением. Кроме того, можно использовать секционированные отправители. Для хранилища больших двоичных объектов, это означает, что события hello отправляются toohello папке секции. Если логику запроса требует hello ключ toobe обработки по hello же экземпляр запроса, можно игнорировать это требование. В качестве примера такой логики можно привести простой запрос select, project или filter.  

2. После размещения hello данных на стороне входной hello, необходимо убедиться, что запрос является секционированной. Для этого необходимо toouse **Partition By** на всех этапах hello. Несколько шагов являются допустимыми, но все они должны быть секционированы по hello таким же ключом. В настоящее время hello ключ разделов необходимо задать слишком**PartitionId** в порядке для полностью параллельных toobe задания hello.  

3. На данном этапе секционированные выходные данные поддерживаются только концентраторами событий и хранилищами BLOB-объектов. Для выходных данных концентратора событий, необходимо настроить toobe ключа секции hello **PartitionId**. Для вывода хранилища больших двоичных объектов у вас нет toodo ничего.  

4. Hello количество входных секций должно быть равно hello количество секций выходных данных. В настоящее время выходные данные хранилища BLOB-объектов не поддерживают секционирование. Но это неважно, он наследует hello схему запроса вышестоящего hello секционирования. Примеры значений секций, позволяющие выполнять задания с полной параллельной обработкой:  

   * 8 секций входных данных концентраторов событий и 8 секций выходных данных концентраторов событий;
   * 8 секций входных данных концентраторов событий и выходные данные хранилища BLOB-объектов;  
   * 8 секций входных данных хранилища BLOB-объектов и выходные данные хранилища BLOB-объектов;  
   * 8 секций входных данных хранилища BLOB-объектов и 8 секций выходных данных концентраторов событий.  

Hello следующих разделах рассматриваются некоторые примеры сценариев, которые являются неудобно параллельные.

### <a name="simple-query"></a>Простой запрос

* Входные данные — концентратор событий с 8 секциями.
* Выходные данные — концентратор событий с 8 секциями.

Запрос:

    SELECT TollBoothId
    FROM Input1 Partition By PartitionId
    WHERE TollBoothId > 100

Этот запрос является простым фильтром. Таким образом нам не нужен tooworry о секционировании hello входные данные, которые передаются toohello концентратора событий. Обратите внимание, что hello запрос включает **секции с PartitionId**, поэтому он удовлетворяет требованию #2 из более ранних версий. Для вывода hello, нам необходимо tooconfigure выходных данных концентратора hello событий в hello задания toohave hello разбиения набор ключей слишком**PartitionId**. Один последней проверке — toomake, убедитесь, что hello количество входных секций равно toohello количество секций выходных данных.

### <a name="query-with-a-grouping-key"></a>Запрос с ключом группирования

* Входные данные — концентратор событий с 8 секциями.
* Выходные данные — хранилище BLOB-объектов.

Запрос:

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

Этот запрос содержит ключ группирования. Таким образом hello же toobe основных требований, обрабатываемых hello же экземпляр, это означает, что события должны быть отправлены концентратора событий toohello секционированных образом запроса. Какой ключ следует использовать? Ключ **PartitionId** определяет логику задания. Мы стремимся фактически ключ Hello **TollBoothId**, Здравствуйте, поэтому **PartitionKey** значение данных о событиях hello следует **TollBoothId**. Это делается в запросе hello, задав **Partition By** слишком**PartitionId**. Поскольку выходные данные hello хранилища больших двоичных объектов, нам не нужен tooworry о настройке значения ключа раздела, согласно требование #4.

### <a name="multi-step-query-with-a-grouping-key"></a>Многоэтапный запрос с ключом группирования
* Входные данные — концентратор событий с 8 секциями.
* Выходные данные — экземпляр концентратора событий с 8 секциями.

Запрос:

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

Этот запрос содержит ключ группирования, поэтому hello же toobe основных требований, обрабатываемых hello того же экземпляра запроса. Мы используем hello же стратегии, как показано в предыдущем примере hello. В этом случае запрос hello состоит из нескольких шагов. Указан ли на каждом этапе параметр **Partition By PartitionId**? Да, поэтому запрос hello удовлетворяет требованию #3. Для вывода hello, нам необходимо ключ раздела hello tooset слишком**PartitionId**, как описано выше. Также можно увидеть, что она имеет hello одинаковое количество секций в качестве входного hello.

## <a name="example-scenarios-that-are-not-embarrassingly-parallel"></a>Примеры сценариев *без* усложненного параллелизма

В предыдущем разделе hello мы показали некоторые неудобно параллельные сценарии. В этом разделе обсуждаются сценарии, которые не соответствуют всем hello требования toobe неудобно параллельные. 

### <a name="mismatched-partition-count"></a>Несоответствие в числе секций
* Входные данные — концентратор событий с 8 секциями.
* Выходные данные — концентратор событий с 32 секциями.

В этом случае неважно, какой запрос hello. Если количество входных разделов hello не совпадает количество разделов hello выходные данные, не неудобно параллельные hello топологии.

### <a name="not-using-event-hubs-or-blob-storage-as-output"></a>Для выходных данных не используются концентраторы событий или хранилище BLOB-объектов
* Входные данные — концентратор событий с 8 секциями.
* Выходные данные — PowerBI.

В настоящее время выходные данные PowerBI не поддерживают секционирование. Таким образом этот сценарий не считается сценарием с усложненным параллелизмом.

### <a name="multi-step-query-with-different-partition-by-values"></a>Многоэтапный запрос с разными значениями параметра Partition By
* Входные данные — концентратор событий с 8 секциями.
* Выходные данные — концентратор событий с 8 секциями.

Запрос:

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By TollBoothId
    GROUP BY TumblingWindow(minute, 3), TollBoothId

Как видно, второй шаг hello использует **TollBoothId** как hello ключ секционирования. Этот шаг не является hello же в качестве первого шага hello и поэтому требует нам toodo в случайном порядке. 

Hello выше примерах некоторых заданий Stream Analytics, которые соответствуют слишком (или не) неудобно параллельные топологии. Если они соответствуют, они имеют возможность hello максимальный масштаб. Для заданий, не соответствующих ни одному из этих профилей, в дальнейшем будут выпущены обновления в отношении масштабирования. Теперь используйте hello Общие рекомендации в следующих разделах hello.

## <a name="calculate-hello-maximum-streaming-units-of-a-job"></a>Вычислить максимальное число единиц потоковой передачи hello задания
Общее число единиц потоковой передачи, которые могут использоваться в задании Stream Analytics Hello зависит от hello число шагов в hello запрос, определенный для задания hello и hello число разделов для каждого шага.

### <a name="steps-in-a-query"></a>Шаги в запросе
Запрос может иметь один или несколько шагов. Каждый шаг — вложенный запрос, определяется hello **WITH** ключевое слово. Hello запрос, который находится за пределами hello **WITH** ключевое слово (только для одного запроса) также считаются шага, например hello **ВЫБЕРИТЕ** инструкции в следующем запросе hello:

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute,3), TollBoothId

Этот запрос включает 2 шага.

> [!NOTE]
> Этот запрос является более подробно далее в статье hello.
>  

### <a name="partition-a-step"></a>Разделы шага
Секционирование шаг требует hello следующие условия:

* Hello источника входных данных должны быть секционированы. 
* Hello **ВЫБЕРИТЕ** инструкции запроса hello должны считать из секционированной входного источника.
* запрос Hello в пределах шага hello должен иметь hello **Partition By** ключевое слово.

При секционировании запроса hello входного события, обработанные и обработанные статистически в отдельной секции группы и выходные данные события создаются для каждой из групп hello. Объединенный агрегат, создать второй tooaggregate несекционированного шаг.

### <a name="calculate-hello-max-streaming-units-for-a-job"></a>Вычислить максимальный hello единицы для задания потоковой передачи
Все шаги несекционированного вместе можно увеличивать масштаб toosix единицы (SUs) для задания Stream Analytics потоковой передачи. SUs tooadd, шаг должны быть секционированы. Каждая секция может включать шесть единиц потоковой передачи.

<table border="1">
<tr><th>Запрос</th><th>SUs Max для задания hello</th></td>

<tr><td>
<ul>
<li>запрос Hello содержит один шаг.</li>
<li>шаг Hello не секционирована.</li>
</ul>
</td>
<td>6</td></tr>

<tr><td>
<ul>
<li>поток входных данных Hello секционируется по 3.</li>
<li>запрос Hello содержит один шаг.</li>
<li>шаг Hello секционирована.</li>
</ul>
</td>
<td>18</td></tr>

<tr><td>
<ul>
<li>Hello запросов содержит два шага.</li>
<li>Ни один из шагов hello секционирована.</li>
</ul>
</td>
<td>6</td></tr>

<tr><td>
<ul>
<li>поток входных данных Hello секционируется по 3.</li>
<li>Hello запросов содержит два шага. шаг ввода Hello секционирована и второй шаг hello не.</li>
<li>Hello <strong>ВЫБЕРИТЕ</strong> считывает инструкции hello секционированы входных данных.</li>
</ul>
</td>
<td>24 (18 и 6 секционированных и несекционированных шагов соответственно)</td></tr>
</table>

### <a name="examples-of-scaling"></a>Примеры масштабирования

Hello следующий запрос вычисляет hello количество машин в окне три минуты, через платный станции, которая имеет три tollbooths. Этот запрос можно масштабировать в сторону toosix SUs.

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

Дополнительные toouse SUs для hello запроса, оба hello потока входных данных и hello запроса должны быть секционированы. Поскольку раздел потока данных hello устанавливается too3, hello следующем измененном запросе можно масштабировать в сторону too18 SUs:

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

При секционировании запроса hello входные события обрабатываются и объединяются в отдельный раздел групп. События выхода также создаются для каждой из групп hello. Секционирование может вызвать некоторые непредвиденные результаты, если hello **GROUP BY** поле не является ключом секции hello hello потока входных данных. Например, hello **TollBoothId** поля в предыдущем запросе hello не является ключом секции hello **Input1**. результат Hello — приветствия, данные из пропускного пункта #1 могут быть распределены в нескольких секциях.

Каждый из hello **Input1** секций будет обрабатываться отдельно Stream Analytics. В результате нескольких записей количества car hello для hello же пропускного пункта в hello же «переворачивающееся» окно будет создан. Если невозможно изменить ключ секции входной hello, эту проблему можно устранить путем добавления шага не раздела, как следующий пример hello:

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute, 3), TollBoothId

Этот запрос может быть SUs масштабированный too24.

> [!NOTE]
> При объединении двух потоков, убедитесь, что потоки hello секционируются ключом секции hello столбца hello использовать toocreate hello соединения. Также убедитесь, что hello одинаковое количество секций в обоих потоках.
> 
> 

## <a name="configure-stream-analytics-streaming-units"></a>Настройка единиц потоковой передачи Stream Analytics

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. Найдите задание Stream Analytics hello tooscale и затем откройте его в список hello ресурсов.
3. В hello задания колонке в разделе **Настройка**, нажмите кнопку **шкалы**.

    ![Настройка задания Stream Analytics на портале Azure][img.stream.analytics.preview.portal.settings.scale]

4. Используйте hello ползунок tooset hello SUs для задания hello. Обратите внимание, что вы ограниченный toospecific SU параметры.


## <a name="monitor-job-performance"></a>Мониторинг производительности задания
Hello портала Azure вы можете отслеживать пропускную способность hello задания:

![Отслеживание заданий Azure Stream Analytics][img.stream.analytics.monitor.job]

Расчет hello ожидается пропускной способности hello рабочей нагрузки. Если пропускная способность hello меньше ожидаемого, настраивать раздел ввода hello, настройки запросов hello и добавить задание tooyour SUs.


## <a name="visualize-stream-analytics-throughput-at-scale-hello-raspberry-pi-scenario"></a>Визуализация пропускной способности Stream Analytics в масштабе: hello Raspberry Pi сценария
toohelp понять, как масштабировать заданий Stream Analytics, мы выполнили эксперимента, на основе введенных данных с устройства Raspberry Pi. Этом эксперименте сообщить нам увидеть эффект hello пропускной способности нескольких потоковой передачи единиц измерения и секции.

В этом сценарии hello устройство отправляет концентратора событий tooan датчиков данных (клиенты). Streaming Analytics обрабатывает данные hello и отправляет предупреждение или статистические данные в качестве концентратора событий tooanother выходных данных. 

Hello клиент отправляет данные датчиков в формате JSON. выходные данные Hello также находится в формате JSON. Hello данных выглядит следующим образом:

    {"devicetime":"2014-12-11T02:24:56.8850110Z","hmdt":42.7,"temp":72.6,"prss":98187.75,"lght":0.38,"dspl":"R-PI Olivier's Office"}

приветствия при следующем запросе является используется toosend оповещение, если индикатор отключена:

    SELECT AVG(lght),
     "LightOff" as AlertText
    FROM input TIMESTAMP
    BY devicetime
     WHERE
        lght< 0.05 GROUP BY TumblingWindow(second, 1)

### <a name="measure-throughput"></a>Измерения пропускной способности

В этом контексте пропускная способность — hello набора входных данных, обрабатываемых Stream Analytics в определенный промежуток времени. (Мы измеряется на 10 минут). tooachieve hello лучшей обработки пропускной способности для hello входные данные, как данные hello потока входных данных и секционирование hello запроса. Мы включили **COUNT()** в toomeasure запрос hello обрабатывались сколько входных событий. убедиться, что задание hello toomake не ожидала просто toocome события ввода, каждой секции концентратора событий ввода hello была предварительно загружена с 300 МБ входных данных.

Hello следующей таблице показаны результаты hello, который мы видели, когда мы увеличили hello число единиц потоковой передачи и соответствующая секция hello учитывается в концентраторы событий.  

<table border="1">
<tr><th>Секции ввода</th><th>Секции вывода</th><th>Единицы потоковой передачи</th><th>Поддерживаемая пропускная способность
</th></td>

<tr><td>12</td>
<td>12</td>
<td>6</td>
<td>4,06 МБ/с</td>
</tr>

<tr><td>12</td>
<td>12</td>
<td>12</td>
<td>8,06 МБ/с</td>
</tr>

<tr><td>48</td>
<td>48</td>
<td>48</td>
<td>38,32 МБ/с</td>
</tr>

<tr><td>192</td>
<td>192</td>
<td>192</td>
<td>172,67 МБ/с</td>
</tr>

<tr><td>480</td>
<td>480</td>
<td>480</td>
<td>454,27 МБ/с</td>
</tr>

<tr><td>720</td>
<td>720</td>
<td>720</td>
<td>609,69 МБ/с</td>
</tr>
</table>

И hello следующей диаграмме показано hello отношения между SUs и пропускной способности визуализации.

![img.stream.analytics.perfgraph][img.stream.analytics.perfgraph]

## <a name="get-help"></a>Получение справки
За дополнительной помощью обращайтесь на наш [форум Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Дальнейшие действия
* [Введение tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Приступая к работе с Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Справочник по языку запросов Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Справочник по API-интерфейсу REST управления Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Image references-->

[img.stream.analytics.monitor.job]: ./media/stream-analytics-scale-jobs/StreamAnalytics.job.monitor-NewPortal.png
[img.stream.analytics.configure.scale]: ./media/stream-analytics-scale-jobs/StreamAnalytics.configure.scale.png
[img.stream.analytics.perfgraph]: ./media/stream-analytics-scale-jobs/perf.png
[img.stream.analytics.streaming.units.scale]: ./media/stream-analytics-scale-jobs/StreamAnalyticsStreamingUnitsExample.jpg
[img.stream.analytics.preview.portal.settings.scale]: ./media/stream-analytics-scale-jobs/StreamAnalyticsPreviewPortalJobSettings-NewPortal.png   

<!--Link references-->

[microsoft.support]: http://support.microsoft.com
[azure.management.portal]: http://manage.windowsazure.com
[azure.event.hubs.developer.guide]: http://msdn.microsoft.com/library/azure/dn789972.aspx

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301

