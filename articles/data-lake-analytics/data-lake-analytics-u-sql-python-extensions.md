---
title: "сценарии aaaExtend U-SQL для Python в аналитике Озера данных Azure | Документы Microsoft"
description: "Узнайте о том, как код toorun Python в скриптах U-SQL"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: c1c74e5e-3e4a-41ab-9e3f-e9085da1d315
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/20/2017
ms.author: saveenr
ms.openlocfilehash: f051f56f67522d4f2b8e6e54fd21a5c95ce3ba92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-get-started-with-extending-u-sql-with-python"></a>Руководство. Начало работы с расширением возможностей U-SQL c Python

Расширения Python для U-SQL позволяют разработчикам tooperform массово-параллельные выполнения кода Python. Привет, следующий пример иллюстрирует hello основные шаги:

* Используйте hello `REFERENCE ASSEMBLY` инструкции tooenable Python расширения для hello скрипт U-SQL
* С помощью hello `REDUCE` операции toopartition hello входные данные по ключу
* Hello Python расширения для U-SQL включают в себя встроенные редуктора (`Extension.Python.Reducer`) работают на каждый редуктора toohello вершин назначенный код Python
* Hello скрипт U-SQL содержит код Python внедренных hello, который содержит функцию с именем `usqlml_main` , pandas кадр данных в качестве входных данных принимает и возвращает pandas кадр данных в качестве выходных данных.

--

    REFERENCE ASSEMBLY [ExtPython];

    DECLARE @myScript = @"
    def get_mentions(tweet):
        return ';'.join( ( w[1:] for w in tweet.split() if w[0]=='@' ) )

    def usqlml_main(df):
        del df['time']
        del df['author']
        df['mentions'] = df.tweet.apply(get_mentions)
        del df['tweet']
        return df
    ";

    @t  = 
        SELECT * FROM 
           (VALUES
               ("D1","T1","A1","@foo Hello World @bar"),
               ("D2","T2","A2","@baz Hello World @beer")
           ) AS 
               D( date, time, author, tweet );

    @m  =
        REDUCE @t ON date
        PRODUCE date string, mentions string
        USING new Extension.Python.Reducer(pyScript:@myScript);

    OUTPUT @m
        too"/tweetmentions.csv"
        USING Outputters.Csv();

## <a name="how-python-integrates-with-u-sql"></a>Интеграция Python c U-SQL

### <a name="datatypes"></a>Типы данных

* Строковые и числовые столбцы из U-SQL преобразовываются без изменений между Pandas и U-SQL.
* Значения NULL U-SQL, преобразованный tooand из Pandas `NA` значения

### <a name="schemas"></a>Схемы

* Векторы индексов в Pandas не поддерживаются в U-SQL. Все кадры входных данных в функции hello Python всегда имеют 64-разрядных числовой индекс от 0 до hello количества строк минус 1. 
* Наборы данных U-SQL не могут содержать повторяемые имена столбцов.
* Имена столбцов в наборах данных не являются строками. 

### <a name="python-versions"></a>Версии Python
Поддерживается только версия Python 3.5.1 (скомпилированная для Windows). 

### <a name="standard-python-modules"></a>Стандартные модули Python
Включены все hello модули Python.

### <a name="additional-python-modules"></a>Дополнительные модули Python
Помимо hello стандартные библиотеки Python, включены несколько библиотек часто используемые python.

    pandas
    numpy
    numexpr

### <a name="exception-messages"></a>Сообщения об исключении
В настоящее время исключение в коде Python отображается в качестве общего сбоя вершины. В будущем hello hello задания U-SQL, сообщения об ошибках будут отображаться сообщение об исключении hello Python.

### <a name="input-and-output-size-limitations"></a>Ограничения размера входных и выходных данных
Каждая вершина имеет ограниченный объем памяти, назначенный tooit. В настоящее время он составляет 6 ГБ на единицу аналитики. Поскольку hello блоки входных и выходных данных должна существовать в памяти в коде Python hello, hello общий размер для hello ввода и вывода не может превышать 6 ГБ.

## <a name="see-also"></a>См. также
* [Обзор аналитики озера данных Microsoft Azure](data-lake-analytics-overview.md)
* [Разработка скриптов U-SQL с помощью средств озера данных для Visual Studio](data-lake-analytics-data-lake-tools-get-started.md)
* [Использование оконных функций U-SQL для заданий в службе аналитики озера данных Azure](data-lake-analytics-use-window-functions.md)

