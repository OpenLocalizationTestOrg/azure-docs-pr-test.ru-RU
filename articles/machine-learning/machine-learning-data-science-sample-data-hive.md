---
title: "aaaSample данные в таблицах Azure HDInsight Hive | Документы Microsoft"
description: "Уменьшение выборки данных в таблицах Hive Azure HDInsight (Hadopop)"
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: f31e8d01-0fd4-4a10-b1a7-35de3c327521
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: 5f86df9b5a18facc875f437abfb004dbe3a06ea4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sample-data-in-azure-hdinsight-hive-tables"></a>Выборка данных в таблицах Azure HDInsight Hive
В этой статье описывается как toodown образец данных, хранящихся в таблицах Azure HDInsight Hive, с помощью запросов Hive. Мы охватим три распространенных метода выборки:

* Универсальная случайная выборка
* Случайная выборка по группам
* Стратифицированная выборка

следующие Hello **меню** связывает tootopics, описывающие как toosample данные из различных средах хранилища.

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

**Для чего нужна выборка данных?**
При планировании tooanalyze dataset hello имеет большой размер, это обычно tooreduce данных рекомендуется toodown образец hello его tooa размер меньший, но репрезентативный и управляемость. Это способствует пониманию данных, их исследованию и проектированию характеристик. Его роль в hello командного процесса обработки и анализа данных — tooenable быстрого создания прототипов функций обработки данных hello и машинного обучения моделей.

Эта задача выборка является этапом hello [процесса обработки и анализа данных Team (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

## <a name="how-toosubmit-hive-queries"></a>Каким образом запросы Hive toosubmit
Запросы Hive могут передаваться из консоли командной строки Hadoop hello на головном узле кластера Hadoop hello hello. toodo это войдите hello головного узла кластера Hadoop hello, откройте консоль командной строки Hadoop hello и отправки запросов Hive hello оттуда. Инструкции по отправке запросов Hive в консоль командной строки Hadoop hello см. в разделе [как tooSubmit запросов Hive](machine-learning-data-science-move-hive-tables.md#submit).

## <a name="uniform"></a> Универсальная случайная выборка
Универсальный случайной выборки означает, что каждая строка в наборе данных hello имеет одинаковую вероятность производится выборка. Это можно реализовать путем добавления набора данных toohello rand() дополнительное поле в внутреннего запроса «select» hello и в hello это условие для этого поля случайных внешнего запроса «select».

Вот пример запроса:

    SET sampleRate=<sample rate, 0-1>;
    select
        field1, field2, …, fieldN
    from
        (
        select
            field1, field2, …, fieldN, rand() as samplekey
        from <hive table name>
        )a
    where samplekey<='${hiveconf:sampleRate}'

Здесь `<sample rate, 0-1>` указывает долю hello, hello пользователи должны toosample записей.

## <a name="group"></a> Случайная выборка по группам
Когда категориальные данные выборки, вы можете tooeither включить или исключить все экземпляры hello какого-либо определенного значения категориальной переменной. Это называется "выборкой по группам".
Например, при наличии категориальной переменной «Состояние» содержит значений NY, MA, ЦС, NJ, PA, и т. д, нужно записи из hello одинаковое состояние всегда быть вместе ли они выборки или нет.

Вот пример запроса с выборкой по группам:

    SET sampleRate=<sample rate, 0-1>;
    select
        b.field1, b.field2, …, b.catfield, …, b.fieldN
    from
        (
        select
            field1, field2, …, catfield, …, fieldN
        from <table name>
        )b
    join
        (
        select
            catfield
        from
            (
            select
                catfield, rand() as samplekey
            from <table name>
            group by catfield
            )a
        where samplekey<='${hiveconf:sampleRate}'
        )c
    on b.catfield=c.catfield

## <a name="stratified"></a>Стратифицированная выборка
В случае стратифицированной случайной выборки с относительно tooa категориальные переменной при получить образцы hello имеют то категориальные значения, которые в hello соотношения его как заполнение родительского hello, из какой hello образцы были получены. С помощью hello того же примера, как описано выше, предположим, что данные содержат вложенные заполнение по состояниям, например NJ имеет 100 наблюдений, NY есть 60 наблюдения и WA имеет 300 наблюдения. Если указать скорость hello стратифицированной выборки toobe 0,5, а затем hello получить образец должен иметь приблизительно 50, 30 и 150 наблюдений Джерси, NY и WA соответственно.

Вот пример запроса:

    SET sampleRate=<sample rate, 0-1>;
    select
        field1, field2, field3, ..., fieldN, state
    from
        (
        select
            field1, field2, field3, ..., fieldN, state,
            count(*) over (partition by state) as state_cnt,
              rank() over (partition by state order by rand()) as state_rank
          from <table name>
        ) a
    where state_rank <= state_cnt*'${hiveconf:sampleRate}'


Сведения о дополнительных методах выборки, доступных в Hive, см. на странице [руководства по выборке](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Sampling).

