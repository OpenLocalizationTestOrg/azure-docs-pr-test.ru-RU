---
title: "функции aaaCreate для данных в кластер Hadoop, с помощью запросов Hive | Документы Microsoft"
description: "Примеры запросов Hive, формирующие характеристики в данных, хранящихся в кластере Azure HDInsight Hadoop."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e8a94c71-979b-4707-b8fd-85b47d309a30
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: 686282bf0fb84ea82758d3c5b7de2bd90f0cf159
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-features-for-data-in-an-hadoop-cluster-using-hive-queries"></a>Создание характеристик для данных в кластере Hadoop с помощью запросов Hive
В этом документе показано, как функции toocreate для данных, сохранить в кластер Azure HDInsight Hadoop, с помощью запросов Hive. Эти запросы Hive использовать внедренные Hive определяемых пользователем функций (UDFs), сценарии hello, для которого предоставляются.

Hello требуемых операций toocreate функции могут быть большим объемом памяти. производительность запросов Hive Hello возрастает в таких случаях и можно повысить путем настройки определенных параметров. Hello помощник по настройке этих параметров рассматривается в последнем разделе hello.

Hello запросы, которые представлены ниже приведены несколько конкретных toohello [NYC такси обработки данных](http://chriswhong.com/open-data/foil_nyc_taxi/) сценарии также приведены в [репозитории GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts). Эти запросы уже есть указана схема данных и будут готовы toobe отправлен toorun. В последнем разделе hello также описаны параметры, которые пользователи могут настраивать, чтобы можно повысить производительность запросов Hive hello.

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

Это **меню** связывает tootopics, описано, как toocreate функции для данных в различных средах. Эта задача является этапом hello [процесса обработки и анализа данных Team (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

## <a name="prerequisites"></a>Предварительные требования
В этой статье предполагается, что вы:

* Создали учетную запись хранения Azure. Инструкции см. в разделе [Создание учетной записи хранения](../storage/common/storage-create-storage-account.md#create-a-storage-account).
* Подготовить настроенные кластеру с hello службы HDInsight.  Инструкции см. в статье [Настройка кластеров Azure HDInsight Hadoop для процесса обработки и анализа данных группы](machine-learning-data-science-customize-hadoop-cluster.md).
* Hello данные были отправленного tooHive таблиц в Azure HDInsight Hadoop кластеров. Если нет, выполните [Создание и загрузка таблиц данных tooHive](machine-learning-data-science-move-hive-tables.md) tooHive tooupload данных сначала таблиц.
* Включить toohello кластера удаленного доступа. При необходимости инструкции в разделе [доступа hello головного узла кластера Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).

## <a name="hive-featureengineering"></a>Создание функций
В этом разделе описаны некоторые примеры использования hello способами, в котором функции могут использоваться для создания использовании запросов Hive. После того, как дополнительные функции, можно добавить их в качестве столбцов toohello существующую таблицу или создать новую таблицу с дополнительные функции hello и первичным ключом, который можно объединить с исходной таблицей hello. Ниже приведены примеры hello.

1. [Возможность создания функций на основе частоты](#hive-frequencyfeature)
2. [Риски категориальных переменных в двоичной классификации](#hive-riskfeature)
3. [Извлечение признаков из полей даты и времени](#hive-datefeatures)
4. [Извлечение признаков из текстовых полей](#hive-textfeatures)
5. [Вычисления расстояния между координатами GPS](#hive-gpsdistance)

### <a name="hive-frequencyfeature"></a>Возможность создания функций на основе частоты
Часто бывает полезным toocalculate частоты hello hello уровни категориальной переменной, или частоты hello определенные комбинации уровней — от нескольких категориальные переменные. Пользователи могут использовать эти частот hello, выполнив сценарий toocalculate:

        select
            a.<column_name1>, a.<column_name2>, a.sub_count/sum(a.sub_count) over () as frequency
        from
        (
            select
                <column_name1>,<column_name2>, count(*) as sub_count
            from <databasename>.<tablename> group by <column_name1>, <column_name2>
        )a
        order by frequency desc;


### <a name="hive-riskfeature"></a>Риски категориальных переменных в двоичной классификации
В двоичной классификации нам нужна tooconvert нечисловые категориальные переменные в числовые признаки, когда hello модели используется только числовые функции. Чтобы это сделать, нужно заменить каждый нечисловой уровень числовым риском. В этом разделе демонстрируется некоторые универсальные запросов Hive, которые вычисляют значения риск hello (вероятность журнала) категориальные переменной.

        set smooth_param1=1;
        set smooth_param2=20;
        select
            <column_name1>,<column_name2>,
            ln((sum_target+${hiveconf:smooth_param1})/(record_count-sum_target+${hiveconf:smooth_param2}-${hiveconf:smooth_param1})) as risk
        from
            (
            select
                <column_nam1>, <column_name2>, sum(binary_target) as sum_target, sum(1) as record_count
            from
                (
                select
                    <column_name1>, <column_name2>, if(target_column>0,1,0) as binary_target
                from <databasename>.<tablename>
                )a
            group by <column_name1>, <column_name2>
            )b

В этом примере переменные `smooth_param1` и `smooth_param2` toosmooth hello риск значения вычисляются на основе данных hello. Риски имеют диапазон от -Inf до Inf. Риски > 0 указывает на hello вероятность того, что что hello целевой сервер равно too1 больше 0,5.

После расчета таблицы риск hello, пользователи могут назначать таблица tooa значений риска, присоединив ее с таблицей риск hello. присоединяемый запроса Hive Hello был представлен в предыдущем разделе.

### <a name="hive-datefeatures"></a>Извлечение функций из полей даты и времени
Язык Hive включает в себя набор функций, определяемых пользователем, для обработки полей даты и времени. В кусте, формат даты и времени по умолчанию hello является "гггг мм дд 00:00:00" ("1970-01-01 12:21:32" пример). В этом разделе показано, примеры, извлечь hello день месяца, hello месяца из поля даты и времени и другие примеры, преобразующие Строка даты и времени в формате, отличного от Строка даты и времени tooa формата по умолчанию hello в используемом по умолчанию форматирование.

        select day(<datetime field>), month(<datetime field>)
        from <databasename>.<tablename>;

Hive в запросе предполагается, что hello *&#60; поля datetime >* в формате даты и времени по умолчанию hello.

Если поля datetime не в формате по умолчанию hello, необходимые поля даты и времени tooconvert hello в отметку времени Unix сначала, а затем время Unix hello преобразования, Строка даты tooa и отметки времени, которая по умолчанию hello формата. Когда hello datetime в основной формат, пользователям можно применять hello внедренных datetime определяемых пользователем функций tooextract компоненты.

        select from_unixtime(unix_timestamp(<datetime field>,'<pattern of hello datetime field>'))
        from <databasename>.<tablename>;

В этом запросе, если hello *&#60; поля даты и времени >* имеет шаблон hello like *03/26/2015 12:04:39*, hello *"&#60; шаблон поля datetime hello >"* должно быть `'MM/dd/yyyy HH:mm:ss'`. tootest, пользователи могут запускать

        select from_unixtime(unix_timestamp('05/15/2015 09:32:10','MM/dd/yyyy HH:mm:ss'))
        from hivesampletable limit 1;

Hello *hivesampletable* в этом запросе предустанавливается на всех кластеров Azure HDInsight Hadoop по умолчанию при инициализации hello кластеров.

### <a name="hive-textfeatures"></a>Извлечение функций из текстовых полей
Если hello Hive таблицы есть текстовое поле, содержащее строку слов, которые разделяются пробелами, hello следующий запрос извлекает длину hello строку hello и hello количество слов в строке приветствия.

        select length(<text field>) as str_len, size(split(<text field>,' ')) as word_num
        from <databasename>.<tablename>;

### <a name="hive-gpsdistance"></a>Вычисление расстояния между координатами GPS
Hello запроса, приведенные в этом разделе можно непосредственно примененных toohello NYC такси обработки данных. Hello этот запрос предназначен tooshow как встроенный tooapply математические функции в функции toogenerate Hive.

Hello поля, используемые в этом запросе, координаты GPS hello раскладки и dropoff расположения с именем *раскладки\_долготы*, *раскладки\_широты*,  *dropoff\_долготы*, и *dropoff\_широты*. Hello запросы, которые вычисляют hello прямой расстояние между hello координаты раскладки и dropoff являются:

        set R=3959;
        set pi=radians(180);
        select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude,
            ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
            *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
            *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
            /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
            +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*
            pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance
        from nyctaxi.trip
        where pickup_longitude between -90 and 0
        and pickup_latitude between 30 and 90
        and dropoff_longitude between -90 and 0
        and dropoff_latitude between 30 and 90
        limit 10;

Hello математических формул, которые вычисляют hello расстояние между двумя Координаты GPS можно найти на hello <a href="http://www.movable-type.co.uk/scripts/latlong.html" target="_blank">сценарии тип доступные</a> сайтов, созданных Питер Lapisu. В его Javascript hello функция `toRad()` только *lat_or_lon*pi/180 *, который преобразует tooradians градусов. Здесь *lat_or_lon* — hello Широта и долгота. Поскольку куст обеспечивают функции hello `atan2`, но предоставляет функции hello `atan`, hello `atan2` реализуется функция `atan` функции hello выше запрос Hive, с использованием определения hello в <a href="http://en.wikipedia.org/wiki/Atan2" target="_blank"> Википедии</a>.

![Создание рабочей области](./media/machine-learning-data-science-create-features-hive/atan2new.png)

Полный список внедренных определяемые пользователем функции можно найти в hello куста **встроенные функции** раздела, посвященного hello <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-MathematicalFunctions" target="_blank">Apache Hive вики-сайте</a>).  

## <a name="tuning"></a>Дополнительные разделы: Настройка параметров Hive tooImprove скорость обработки запросов
Здравствуйте, параметр по умолчанию параметры Hive кластера может быть подходит для запросов Hive hello и hello данных, которые обрабатывают запросы hello. В этом разделе мы рассмотрим некоторые параметры, которые пользователи могут настраивать, повышающие производительность hello запросов Hive. Пользователи должны tooadd hello параметр настройки запросов перед hello запросы обработки данных.

1. **Размер кучи Java**: для запросов, включающих соединение больших наборов данных или обработки длинных записях **хватает размера кучи** является одной из распространенных ошибок hello. Это можно настроить, задав параметры *mapreduce.map.java.opts* и *mapreduce.task.io.sort.mb* toodesired значения. Пример:
   
        set mapreduce.map.java.opts=-Xmx4096m;
        set mapreduce.task.io.sort.mb=-Xmx1024m;

    Этот параметр выделяет пространства кучи tooJava 4 ГБ памяти, а также делает сортировки более эффективно, выделив дополнительную память для него. Это разумно tooplay с выделение памяти при наличии пробелов связанные tooheap ошибки сбоя задания.

1. **Размер блока DFS** : этот параметр задает hello наименьшая единица данных, hello хранилища системных файлов. Например если размер блока DFS hello составляет 128 МБ то любые данные, размер вверх too128MB и меньше, чем сохраняется в одном блоке, при данных, больше, чем 128 МБ будет выделено дополнительное блоки. Выбор размера очень небольшой блок вызывает большие накладные расходы в Hadoop, так как узел с именем hello tooprocess многие дополнительные запросы toofind hello соответствующего блока относится файл toohello. При работе с гигабайтами (или большими объемами) данных рекомендуем такую настройку:
   
        set dfs.block.size=128m;
2. **Оптимизация операции соединения в кусте** : во время операции объединения в framework сопоставления и сокращения hello, обычно выполняются в hello уменьшить этап, иногда, огромным увеличится, запланировав соединения в этапе сопоставления hello (также называется «mapjoins»). toodirect куста toodo, это когда это возможно, можно выбрать вариант:
   
        set hive.auto.convert.join=true;
3. **Указание числа hello модули сопоставления tooHive** : во время Hadoop позволяет hello пользователя tooset hello число reducers, обычно является число hello модули сопоставления не задается пользователем hello. Прием, обеспечивает определенную степень управления на этот номер является toochoose hello Hadoop переменные, *mapred.min.split.size* и *mapred.max.split.size* как hello размер каждой карты определяется задач:
   
        num_maps = max(mapred.min.split.size, min(mapred.max.split.size, dfs.block.size))
   
    Здравствуйте, как правило, значение по умолчанию *mapred.min.split.size* равно 0, что *mapred.max.split.size* — **Long.MAX** , а *dfs.block.size* составляет 64 МБ. Как видите, размер данных заданного hello, помощник по настройке этих параметров следует «Подготовка» их мы сможем tootune hello число использовать модули сопоставления.
4. Ниже приведены некоторые другие **дополнительные возможности** по оптимизации производительности Hive. Эти возможности toomap памяти, выделенной tooset hello и сокращать задачи и можно использовать в настройке производительности. Следует помнить, hello *mapreduce.reduce.memory.mb* не может превышать размер физической памяти hello каждый рабочий узел в кластере Hadoop hello.
   
        set mapreduce.map.memory.mb = 2048;
        set mapreduce.reduce.memory.mb=6144;
        set mapreduce.reduce.java.opts=-Xmx8192m;
        set mapred.reduce.tasks=128;
        set mapred.tasktracker.reduce.tasks.maximum=128;

