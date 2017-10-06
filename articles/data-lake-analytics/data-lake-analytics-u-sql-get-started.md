---
title: "Начало работы с языком U-SQL | Документация Майкрософт"
description: "Основы hello объекта hello языка U-SQL."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 57143396-ab86-47dd-b6f8-613ba28c28d2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/23/2017
ms.author: saveenr
ms.openlocfilehash: 5edee0e0d85211e84b3d47895c53d71f0a19f083
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-u-sql"></a>Начало работы с U-SQL
U-SQL — это язык, объединяет декларативный SQL с принудительной C# toolet обрабатывать данные любых объемов. Через hello масштабируемого, распределенного запроса возможности U-SQL может эффективно анализировать данные в реляционных хранилищах, таких как базы данных SQL Azure. С помощью U-SQL вы можете обрабатывать неструктурированные данные, применяя схему к пользовательской логике чтения и вставки, а также определяемым пользователем функциям. Кроме того, U-SQL содержит расширения, который обеспечивает точное управление над тем, как tooexecute в масштабе. 

## <a name="learning-resources"></a>Учебные материалы

* Hello [U-SQL учебника](http://aka.ms/usqltutorial) Пошаговое руководство для большинства hello U-SQL языка. В этом документе рекомендуется использовать считывании для всех разработчиков, желающих toolearn U-SQL.
* Дополнительные сведения о hello **синтаксиса языка U-SQL**, hello в разделе [Справочник по языку U SQL](http://go.microsoft.com/fwlink/p/?LinkId=691348).
* toounderstand hello **принципы разработки U-SQL**, см. блоге Visual Studio hello [введение U-SQL — язык, который упрощает больших обработки данных](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).

## <a name="prerequisites"></a>Предварительные требования

Перед выполнением примеров hello U-SQL в этом документе, прочтите и выполните [учебника: сценарии разработки U-SQL, с помощью средств Озера данных для Visual Studio](data-lake-analytics-data-lake-tools-get-started.md). Этот учебник объясняется hello механизм использования U-SQL с помощью средств Озера данных Azure для Visual Studio.

## <a name="your-first-u-sql-script"></a>Первый скрипт U-SQL

Привет, выполнив скрипт U-SQL является простым также позволяют исследовать многие аспекты hello U-SQL языка.

```
@searchlog =
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM "/Samples/Data/SearchLog.tsv"
    USING Extractors.Tsv();

OUTPUT @searchlog   
    too"/output/SearchLog-first-u-sql.csv"
    USING Outputters.Csv();
```

Этот сценарий не содержит действий преобразования. Она считывает данные из hello исходный файл с именем `SearchLog.tsv`, schematizes его и записывает набор строк hello обратно в файл с именем SearchLog первый u sql.csv.

Обратите внимание, тип данных hello вопросительный знак Далее toohello в hello `Duration` поля. Это означает, что hello `Duration` поле может иметь значение null.

### <a name="key-concepts"></a>Основные понятия
* **Переменные строк**: tooa переменной можно назначить для каждого выражения запроса, который возвращает набор строк. U-SQL соответствует шаблону именования переменных hello T-SQL (`@searchlog`, например) в скрипте hello.
* Hello **ИЗВЛЕЧЬ** ключевое слово считывает данные из файла и определяется hello схемы для чтения. `Extractors.Tsv` — это встроенное средство извлечения U-SQL для файлов со значениями с разделением знаками табуляции. Можно разрабатывать пользовательские средства извлечения.
* Hello **ВЫВОДА** записывает данные из файла tooa набора строк. `Outputters.Csv()`— Это файл с разделителями запятыми для встроенных toocreate outputter U-SQL. Вы можете разработать собственные средства вывода.

### <a name="file-paths"></a>Пути к файлам

Hello ИЗВЛЕЧЕНИЯ и выходные данные инструкции используйте пути к файлам. Пути к файлам могут быть абсолютными или относительными.

Это следующий абсолютный путь к файлу ссылается файл tooa в хранилище Озера данных с именем `mystore`:

    adl://mystore.azuredatalakestore.net/Samples/Data/SearchLog.tsv

Следующий относительный путь к файлу начинается с `"/"`. Он ссылается файл tooa в учетной записи хранилища Озера данных по умолчанию hello:

    /output/SearchLog-first-u-sql.csv

## <a name="use-scalar-variables"></a>Использование скалярных переменных

Можно использовать скалярные переменные как хорошо toomake обслуживания сценарий проще. Hello предыдущий скрипт U-SQL также может быть записан следующим образом:

    DECLARE @in  string = "/Samples/Data/SearchLog.tsv";
    DECLARE @out string = "/output/SearchLog-scalar-variables.csv";

    @searchlog =
        EXTRACT UserId          int,
                Start           DateTime,
                Region          string,
                Query           string,
                Duration        int?,
                Urls            string,
                ClickedUrls     string
        FROM @in
        USING Extractors.Tsv();

    OUTPUT @searchlog   
        too@out
        USING Outputters.Csv();

## <a name="transform-rowsets"></a>Преобразования наборов строк

Используйте **ВЫБЕРИТЕ** tootransform наборы строк:

    @searchlog =
        EXTRACT UserId          int,
                Start           DateTime,
                Region          string,
                Query           string,
                Duration        int?,
                Urls            string,
                ClickedUrls     string
        FROM "/Samples/Data/SearchLog.tsv"
        USING Extractors.Tsv();

    @rs1 =
        SELECT Start, Region, Duration
        FROM @searchlog
    WHERE Region == "en-gb";

    OUTPUT @rs1   
        too"/output/SearchLog-transform-rowsets.csv"
        USING Outputters.Csv();

Здравствуйте, предложение WHERE использует [C# логическое выражение](https://msdn.microsoft.com/library/6a71f45d.aspx). Toodo языка, hello C# выражение можно использовать собственные выражения и функции. Можно даже выполнить более сложную фильтрацию, сочетая их с помощью логического объединения (and) и разделения (or).

Hello следующий скрипт использует метод DateTime.Parse() hello и вместе.

    @searchlog =
        EXTRACT UserId          int,
                Start           DateTime,
                Region          string,
                Query           string,
                Duration        int?,
                Urls            string,
                ClickedUrls     string
        FROM "/Samples/Data/SearchLog.tsv"
        USING Extractors.Tsv();

    @rs1 =
        SELECT Start, Region, Duration
        FROM @searchlog
    WHERE Region == "en-gb";

    @rs1 =
        SELECT Start, Region, Duration
        FROM @rs1
        WHERE Start >= DateTime.Parse("2012/02/16") AND Start <= DateTime.Parse("2012/02/17");

    OUTPUT @rs1   
        too"/output/SearchLog-transform-datetime.csv"
        USING Outputters.Csv();

 >[!NOTE]
 >второй запрос Hello работает на результат hello hello первый набор строк, создающий составной hello два фильтра. Также можно повторно использовать имя переменной, а лексически относятся имена hello.

## <a name="aggregate-rowsets"></a>Агрегированные наборы строк
U-SQL предоставляет hello знакомы ORDER BY, GROUP BY и агрегаты.

Hello следующий запрос находит общая длительность hello по регионам, а затем отображает hello верхней пять длительности в порядке.

Наборы строк U-SQL не сохранять их порядок для следующего запроса hello. Таким образом, tooorder выход, необходимо tooadd ORDER BY toohello выходных данных инструкции:

    DECLARE @outpref string = "/output/Searchlog-aggregation";
    DECLARE @out1    string = @outpref+"_agg.csv";
    DECLARE @out2    string = @outpref+"_top5agg.csv";

    @searchlog =
        EXTRACT UserId          int,
                Start           DateTime,
                Region          string,
                Query           string,
                Duration        int?,
                Urls            string,
                ClickedUrls     string
        FROM "/Samples/Data/SearchLog.tsv"
        USING Extractors.Tsv();

    @rs1 =
        SELECT
            Region,
            SUM(Duration) AS TotalDuration
        FROM @searchlog
    GROUP BY Region;

    @res =
        SELECT *
        FROM @rs1
        ORDER BY TotalDuration DESC
        FETCH 5 ROWS;

    OUTPUT @rs1
        too@out1
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

    OUTPUT @res
        too@out2
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

Hello U-SQL предложение ORDER BY, необходимо использовать предложения FETCH hello в выражении SELECT.

можно использовать toorestrict hello вывода toogroups, удовлетворяют условиям HAVING hello предложение U-SQL с Hello:

    @searchlog =
        EXTRACT UserId          int,
                Start           DateTime,
                Region          string,
                Query           string,
                Duration        int?,
                Urls            string,
                ClickedUrls     string
        FROM "/Samples/Data/SearchLog.tsv"
        USING Extractors.Tsv();

    @res =
        SELECT
            Region,
            SUM(Duration) AS TotalDuration
        FROM @searchlog
        GROUP BY Region
        HAVING SUM(Duration) > 200;

    OUTPUT @res
        too"/output/Searchlog-having.csv"
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

При использовании дополнительных статистических см hello hello U-SQL справочной документации для [статистической обработки, аналитические и ссылаться на функции](https://msdn.microsoft.com/en-us/library/azure/mt621335.aspx)

## <a name="next-steps"></a>Дальнейшие действия
* [Обзор аналитики озера данных Microsoft Azure](data-lake-analytics-overview.md)
* [Разработка скриптов U-SQL с помощью средств озера данных для Visual Studio](data-lake-analytics-data-lake-tools-get-started.md)
