---
title: "проблемы aaaResolve Рассогласование данных с помощью средств Озера данных Azure для Visual Studio | Документы Microsoft"
description: "Сведения об устранении проблем неравномерного распределения данных с помощью средств Azure Data Lake для Visual Studio."
services: data-lake-analytics
documentationcenter: 
author: yanancai
manager: 
editor: 
ms.assetid: 
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/16/2016
ms.author: yanacai
ms.openlocfilehash: 3909fbd89eb40f061268cb7128f7fa84a3c33de7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-data-skew-problems-by-using-azure-data-lake-tools-for-visual-studio"></a>Решение проблем неравномерного распределения данных с помощью средств Azure Data Lake для Visual Studio

## <a name="what-is-data-skew"></a>Что такое неравномерное распределение данных?

Коротко говоря, неравномерное распределение данных — это чрезмерно представленное значение. Предположим, что вы присвоили 50 налога прошедшие tooaudit налоговых деклараций, один examiner для каждого из штатов США. examiner Вайоминг Hello, так как существует заполнение hello мал, имеет немного toodo. В Калифорнии Однако hello examiner хранится сильно загружен из-за состояния hello большое.
    ![Пример проблемы неравномерного распределения данных](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/data-skew-problem.png)

В нашем сценарии hello данных неравномерно распределяется по все прошедшие налогов, который означает, что некоторые прошедшие должен работать в более, чем другие. В свою работу часто возникают ситуаций, как в данном примере hello examiner налога. С более технической точки зрения одной вершины возвращает намного больше данных, чем его коллегами ситуацию, которая делает вершин hello работать более чем hello другим пользователям, которые в конечном итоге замедляет все задание. Что еще хуже, hello задания может закончится, так как вершины может иметь, например, ограничение 5 часов выполнения и ограничение 6 ГБ памяти.

## <a name="resolving-data-skew-problems"></a>Устранение неравномерного распределения данных

Средства Azure Data Lake для Visual Studio помогают обнаружить проблемы неравномерного распределения данных в задании. Если существует проблема, можно разрешить ее, попытавшись hello решения в этом разделе.

## <a name="solution-1-improve-table-partitioning"></a>Решение 1. Улучшение секционирования таблиц

### <a name="option-1-filter-hello-skewed-key-value-in-advance"></a>Вариант 1: Hello фильтра неравномерным значение ключа заранее

Если он не влияет на бизнес-логики, можно фильтровать значения повышение частоты hello заранее. Например при наличии большой объем 000-000-000 в столбце GUID, это может быть tooaggregate это значение. Прежде чем aggregate, можно написать «ГДЕ GUID! = «000 000 000» «toofilter hello высокочастотные значение.

### <a name="option-2-pick-a-different-partition-or-distribution-key"></a>Вариант 2. Выберите другой ключ секции или распределения

В hello предшествующий пример Если требуется, чтобы рабочая нагрузка налога аудита hello только toocheck все через hello страны, может улучшить распределение данных hello выбрав hello идентификатор в качестве ключа. Комплектации другой раздел или ключ распределения могут иногда hello данных более равномерно распределять, но необходимо убедиться, что этот вариант не влияет на бизнес-логики toomake. Для экземпляра toocalculate сумма налога hello для каждого состояния, может потребоваться toodesignate _состояние_ в качестве ключа секции hello. Если вы продолжите tooexperience эту проблему, попробуйте использовать параметр 3.

### <a name="option-3-add-more-partition-or-distribution-keys"></a>Вариант 3. Добавьте дополнительные ключи секции или распределения

Помимо использования одного _штата_ можно использовать несколько ключей для секционирования. Например, рассмотрите возможность добавления _ПОЧТОВЫЙ индекс_ как дополнительный раздел секцию данных ключа tooreduce размеров и более равномерно распределять данные hello.

### <a name="option-4-use-round-robin-distribution"></a>Вариант 4. Используйте распределение путем циклического перебора

Если не удается найти подходящего ключа для секции и распространения, можно попробовать toouse циклическое распределение. При распределении путем циклического перебора все строки обрабатываются одинаково и случайным образом помещаются в соответствующий контейнер. Возвращает равномерного распределения данных Hello, но он приводит к потере сведений местоположению, недостаток, который может снизить производительность работы при выполнении некоторых операций. Кроме того при выполнении статистической обработки для ключа асимметричные hello все равно hello Рассогласование данных проблема не будет устранена. toolearn Дополнительные сведения о циклическое распределение распределения таблицы hello U-SQL см. в разделе [CREATE TABLE (U-SQL): создание таблицы со схемой](https://msdn.microsoft.com/en-us/library/mt706196.aspx#dis_sch).

## <a name="solution-2-improve-hello-query-plan"></a>Решение 2: Улучшить план запроса hello

### <a name="option-1-use-hello-create-statistics-statement"></a>Вариант 1: Использование инструкции CREATE STATISTICS hello

U-SQL предоставляет инструкции CREATE STATISTICS hello в таблицах. Эта инструкция предоставляет дополнительные оптимизатор запросов toohello сведения о hello характеристики данных, таких как распределение значений, хранящихся в таблице. Для большинства запросов оптимизатор запросов hello уже приводит к возникновению ошибки hello необходимую статистику для плана запроса высокого качества. В некоторых случаях может потребоваться tooimprove производительность запросов, создав дополнительную статистику с помощью инструкции CREATE STATISTICS, либо изменив hello конструктор запросов. Дополнительные сведения см. в разделе hello [CREATE STATISTICS (U-SQL)](https://msdn.microsoft.com/en-us/library/azure/mt771898.aspx) страницы.

Пример кода:

    CREATE STATISTICS IF NOT EXISTS stats_SampleTable_date ON SampleDB.dbo.SampleTable(date) WITH FULLSCAN;

>[!NOTE]
>Статистика не обновляется автоматически. При обновлении данных hello в таблице без повторного создания статистики hello hello производительность запросов может ухудшиться.

### <a name="option-2-use-skewfactor"></a>Вариант 2. Используйте SKEWFACTOR

Если требуется toosum hello налога для каждого состояния, должны использовать GROUP BY поле "состояние" подход, который не избежать Рассогласование данных hello. Тем не менее можно задать подсказку данных в вашей tooidentify запрос, который искажению данных ключи, чтобы оптимизатор hello можно подготовить план выполнения.

Как правило можно установить для параметра hello как 0,5 и 1, то есть не наклон интенсивной наклона и 1 значение 0,5. Поскольку указание hello влияет на оптимизацию плана выполнения для текущей инструкции hello и все подчиненные инструкции, быть убедиться, что указание hello tooadd hello потенциальных неравномерным key-wise статистической обработки.

    SKEWFACTOR (columns) = x

    Provides a hint that hello given columns have a skew factor x from 0 (no skew) through 1 (very heavy skew).

Пример кода:

    //Add a SKEWFACTOR hint.
    @Impressions =
        SELECT * FROM
        searchDM.SML.PageView(@start, @end) AS PageView
        OPTION(SKEWFACTOR(Query)=0.5)
        ;

    //Query 1 for key: Query, ClientId
    @Sessions =
        SELECT
            ClientId,
            Query,
            SUM(PageClicks) AS Clicks
        FROM
            @Impressions
        GROUP BY
            Query, ClientId
        ;

    //Query 2 for Key: Query
    @Display =
        SELECT * FROM @Sessions
            INNER JOIN @Campaigns
                ON @Sessions.Query == @Campaigns.Query
        ;   

### <a name="option-3-use-rowcount"></a>Вариант 3. Использование ROWCOUNT  
Кроме tooSKEWFACTOR для определенного неравномерным ключа соединения случаев, если известно, что hello другого набора связанных строк невелико, оптимизатор hello можно определить путем добавления Указание количества СТРОК в инструкции hello U-SQL перед ПРИСОЕДИНЕНИЕМ. Таким образом, оптимизатор может выбрать, toohelp широковещательных соединения стратегия повышения производительности. Имейте в виду, что количество СТРОК не была устранена hello Рассогласование данных, но он может предложить некоторые дополнительные справочные материалы.

    OPTION(ROWCOUNT = n)

    Identify a small row set before JOIN by providing an estimated integer row count.

Пример кода:

    //Unstructured (24-hour daily log impressions)
    @Huge   = EXTRACT ClientId int, ...
                FROM @"wasb://ads@wcentralus/2015/10/30/{*}.nif"
                ;

    //Small subset (that is, ForgetMe opt out)
    @Small  = SELECT * FROM @Huge
                WHERE Bing.ForgetMe(x,y,z)
                OPTION(ROWCOUNT=500)
                ;

    //Result (not enough information toodetermine simple broadcast JOIN)
    @Remove = SELECT * FROM Bing.Sessions
                INNER JOIN @Small ON Sessions.Client == @Small.Client
                ;

## <a name="solution-3-improve-hello-user-defined-reducer-and-combiner"></a>Решение 3: Улучшить редуктора определяемых пользователем hello и функции объединения

Иногда можно написать определяемый пользователем оператор toodeal с логикой сложным процессом и грамотно сконструированные редуктора и функции объединения может снизить проблема Рассогласование данных в некоторых случаях.

### <a name="option-1-use-a-recursive-reducer-if-possible"></a>Вариант 1. По возможности используйте рекурсивный редуктор

По умолчанию определяемый пользователем редуктор выполняется в нерекурсивном режиме, а это означает, что уменьшенный объем работы для ключа распределяется в одну вершину. Но если данные искажены hello огромный наборы данных могут обрабатываться в одной вершины и запуска в течение долгого времени.

tooimprove производительности, можно добавить атрибут в toorun редуктора toodefine вашего кода, в режиме рекурсивной. Затем hello огромный наборов данных можно распределенных toomultiple вершин и запустить параллельно, что ускоряет вашу работу.

toochange toorecursive редуктора нерекурсивного необходимо toomake убедитесь, что ваш алгоритм ассоциативных. Например сумма hello имеет ассоциативность и МЕДИАНА hello не является. Необходимо также убедиться, что hello входные и выходные данные для редуктора поддерживать hello toomake одной схеме.

Атрибут для рекурсивного редуктора:

    [SqlUserDefinedReducer(IsRecursive = true)]

Пример кода:

    [SqlUserDefinedReducer(IsRecursive = true)]
    public class TopNReducer : IReducer
    {
        public override IEnumerable<IRow>
            Reduce(IRowset input, IUpdatableRow output)
        {
            //Your reducer code goes here.
        }
    }

### <a name="option-2-use-row-level-combiner-mode-if-possible"></a>Вариант 2. По возможности используйте режим средства объединения на уровне строк

Аналогичные указания ROWCOUNT toohello для определенного соединения неравномерным ключа вариантов, режим функции объединения предпринимает наборы toomultiple toodistribute огромное значение неравномерным ключ вершин, чтобы hello работы могут быть выполнены одновременно. Режим средства объединения не устранит проблему неравномерного распределения данных, но может дополнительно помочь с обработкой массивных наборов неравномерно распределенных значений ключей.

По умолчанию режим hello функции объединения является полной резервной копии, то есть hello слева набора строк и набор вправо строк не могут быть разделены. Установка режима hello как влево или вправо/внутренний позволяет уровня строки соединения. Hello система разделяет hello соответствующих наборов строк и распространяет их в несколько вершин, параллельное выполнение. Тем не менее прежде чем настраивать режим функции объединения hello, будьте внимательны, что tooensure, hello соответствующие наборы строк могут быть разделены.

в следующем примере Hello показан набор отдельных строк слева. Каждой строке вывода зависит от одной входной строки слева hello и потенциально зависит все строки из hello справа с hello же значение ключа. Если устанавливается режим hello функции объединения как слева, hello система разделяет hello огромный слева-набора строк в небольших описаний и назначает им toomultiple вершин.

![Иллюстрация режима средства объединения](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/combiner-mode-illustration.png)

>[!NOTE]
>Если режим hello неправильный функции объединения hello комбинация является менее эффективным и hello результаты могут оказаться некорректными.

Атрибуты режима средства объединения:

- [SqlUserDefinedCombiner(Mode=CombinerMode.Full)]: Every output row potentially depends on all hello input rows from left and right with hello same key value.

- SqlUserDefinedCombiner(Mode=CombinerMode.Left): Каждая строка выходных данных зависит от одной входной строки слева hello (и потенциально все строки из hello справа с hello же значение ключа).

- qlUserDefinedCombiner(Mode=CombinerMode.Right): каждая строка выходных данных зависит от одной входной строки из правой hello (и потенциально все строки из левой hello с hello же значение ключа).

- SqlUserDefinedCombiner(Mode=CombinerMode.Inner): Каждая строка выходных данных зависит от одной входной строки из слева hello и hello справа с hello же значение.

Пример кода:

    [SqlUserDefinedCombiner(Mode = CombinerMode.Right)]
    public class WatsonDedupCombiner : ICombiner
    {
        public override IEnumerable<IRow>
            Combine(IRowset left, IRowset right, IUpdatableRow output)
        {
        //Your combiner code goes here.
        }
    }
