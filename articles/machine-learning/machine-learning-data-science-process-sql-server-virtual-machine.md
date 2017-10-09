---
title: "aaaExplore данных на виртуальной машине SQL Server в Azure | Документы Microsoft"
description: "Изучение данных и создание характеристик на виртуальной машине SQL Server в Azure"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: 
ms.assetid: 3949fb2c-ffab-49fb-908d-27d5e42f743b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: 67f4b058b0f6557ee15fd42795c918d68f1a9871
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="heading"></a>Обработка данных в виртуальной машине SQL Server на платформе Azure
В этом документе рассматриваются как tooexplore данные и создавать признаки для данных, хранящихся в виртуальной Машине SQL Server в Azure. Это можно сделать путем структурирования данных с помощью SQL или с использованием языка программирования, например Python.

> [!NOTE]
> Hello пример инструкции SQL в этом документе предполагается, что данные находятся в SQL Server. В противном случае обратитесь toohello облачных данных обработки и анализа процесса карты toolearn как toomove вашей tooSQL данные сервера.
> 
> 

## <a name="SQL"></a>Использование SQL
Описание hello следующих данных wrangling задачи в этом разделе, с помощью SQL:

1. [Просмотр данных](#sql-dataexploration)
2. [Создание характеристик](#sql-featuregen)

### <a name="sql-dataexploration"></a>Просмотр данных
Вот несколько примеры сценариев SQL, которые можно использовать tooexplore хранилищ данных в SQL Server.

> [!NOTE]
> Практический пример, можно использовать hello [dataset такси NYC](http://www.andresmh.com/nyctaxitrips/) и toohello IPNB под названием [wrangling NYC данных с помощью ноутбук IPython и SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) руководство с начала до конца.
> 
> 

1. Получение числа hello наблюдения за день
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. Получить уровней hello в категориальный столбец
   
    `select  distinct <column_name> from <databasename>`
3. Получить hello количество уровней в сочетании с двумя категориальные столбцы 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. Получить hello распространения для числовых столбцов.
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

### <a name="sql-featuregen"></a>Создание функций
В этом разделе мы опишем способы создания характеристик с помощью SQL:  

1. [Создание характеристик на основе количества](#sql-countfeature)
2. [Создание характеристик путем группирования данных](#sql-binningfeature)
3. [Развертывание компонентов hello из одного столбца](#sql-featurerollout)

> [!NOTE]
> После создания дополнительных компонентов можно добавлять их в виде столбцов toohello существующую таблицу или создать новую таблицу с дополнительные функции hello и первичный ключ, который можно объединить с исходной таблицей hello. 
> 
> 

### <a name="sql-countfeature"></a>Создание характеристик на основе количества
Hello следующих примерах показано два способа создания функции count. Первый метод Hello использует суммирования и второй метод использует hello hello предложение «where». Затем их можно объединить с hello исходной таблицы (с помощью первичных ключевых столбцов) toohave число функций вместе с исходными данными hello.

    select <column_name1>,<column_name2>,<column_name3>, COUNT(*) as Count_Features from <tablename> group by <column_name1>,<column_name2>,<column_name3> 

    select <column_name1>,<column_name2> , sum(1) as Count_Features from <tablename> 
    where <column_name3> = '<some_value>' group by <column_name1>,<column_name2> 

### <a name="sql-binningfeature"></a>Создание характеристик путем группирования данных
Hello следующем примере показано, как toogenerate сегментации функции путем сегментирования (с помощью пять ячеек) столбца числовых значений, можно использовать как компонент:

    `SELECT <column_name>, NTILE(5) OVER (ORDER BY <column_name>) AS BinNumber from <tablename>`


### <a name="sql-featurerollout"></a>Развертывание компонентов hello из одного столбца
В этом разделе показано как tooroll out одиночный столбец в таблице toogenerate дополнительные функции. пример Hello предполагается наличие Широта и долгота столбец в таблице hello, из которого вы пытаетесь toogenerate функции.

Ниже приведен краткий учебник на данные о местоположении широты и долготы (ресурсов из stackoverflow [как toomeasure hello точность широты и долготы?](http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude)). Это полезно toounderstand перед featurizing hello поле «расположение»:

* знак Hello указывает мы, являются ли вверх или вниз, Восточная или Западная по всему миру hello.
* Ненулевая цифра сотен указывает, что используется долгота, а не широта!
* цифра Hello десятков дает tooabout позиции 1 000 километров. Она указывает, на каком континенте или в каком океане мы находимся.
* Hello единиц (один десятичное) дает вверх километрах too111 (60 миля, около 69 миль). Она может приблизительно сообщить нам, в каком крупном регионе или стране мы находимся.
* первый десятичный разряд Hello стоит копирование км too11.1: она различает hello положение одного большого города из соседних большого города.
* Hello двух знаков после запятой стоит вверх too1.1 км: его можно разделить один village из hello рядом.
* Третий десятичный разряд Hello стоит копирование too110 m: можно указать, больших agricultural поля или учреждений университета.
* Четвертый десятичный разряд Hello стоит копирование too11 m: можно указать, участка земли. Это Типичная точность сопоставимых toohello Неисправленные GPS устройства с без помех.
* Пятый десятичный разряд Hello стоит копирование too1.1 m: его по ширине позволяет отличить деревьев друг от друга. Уровень точности toothis с коммерческих GPS-устройства могут быть осуществлены только с разностной исправления.
* шестой десятичный разряд Hello стоит копирование m: too0.11, это можно использовать для размещения структуры проектирования ландшафтов, подробно построение дороги. Этого уровня более чем достаточно для отслеживания движения ледников и рек. Его можно достичь с помощью тщательного измерения с использованием GPS, например при дифференциальной коррекции GPS.

сведения о расположении Hello может быть Признак следующим образом отделить региону, расположение и сведения о городе. Обратите внимание, что также можно вызывать конечную точку REST, такие как API службы Bing Maps см. в [найти расположение точкой](https://msdn.microsoft.com/library/ff701710.aspx) tooget сведения о регионе или районе hello.

    select 
        <location_columnname>
        ,round(<location_columnname>,0) as l1        
        ,l2=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 1 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),1,1) else '0' end     
        ,l3=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 2 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),2,1) else '0' end     
        ,l4=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 3 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),3,1) else '0' end     
        ,l5=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 4 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),4,1) else '0' end     
        ,l6=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 5 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),5,1) else '0' end     
        ,l7=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 6 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),6,1) else '0' end     
    from <tablename>

Эти функции на основе расположения можно дополнительно используется toogenerate число дополнительных функций как описано выше. 

> [!TIP]
> Можно программным образом вставить записи hello, с помощью выбранного языка. Может потребоваться tooinsert данных hello в блоки повышения эффективности записи tooimprove (пример того, как toodo этот использовании pyodbc см [tooaccess образец HelloWorld SQLServer с python](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python)). Другой вариант — tooinsert данные в базе данных hello, с помощью hello [служебная программа BCP](https://msdn.microsoft.com/library/ms162802.aspx).
> 
> 

### <a name="sql-aml"></a>Подключение tooAzure машинного обучения
Hello только что созданный компонент может добавляются как таблица tooan существующий столбец или хранится в новую таблицу и объединена с исходной таблицей hello для машинного обучения. Функции можно создать или получить доступ, уже созданы с помощью hello [импорта данных] [ import-data] в машинном обучении Azure как показано ниже:

![считыватели azureml][1] 

## <a name="python"></a>Использование языка программирования, например Python
С помощью Python tooexplore данных и создавать функции при схожие данные tooprocessing hello данные хранятся в SQL Server в BLOB-объектов Azure с помощью Python, как описано в документе [данные больших двоичных объектов Azure процесс в среде обработки и анализа данных](machine-learning-data-science-process-data-blob.md). Hello данных должен toobe загружаются из базы данных hello в кадр данных pandas и затем обрабатываются. Мы документа hello процесс соединения toohello базы данных и загрузку данных hello в кадр данных hello в этом разделе.

Hello следующий формат строки соединения может быть база данных SQL Server используется tooconnect tooa из Python, с помощью pyodbc (заменить имя сервера, dbname, имя пользователя и пароль особые значения):

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

Hello [Pandas библиотеки](http://pandas.pydata.org/) в Python предоставляет широкий набор средств анализа данных и структур данных для работы с данными для программирования Python. Приведенный ниже код Hello считывает hello результаты, возвращенные из базы данных SQL Server, в кадр данных Pandas:

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

Теперь можно работать с кадра данных Pandas hello, как описано в статье hello [данные больших двоичных объектов Azure процесс в среде обработки и анализа данных](machine-learning-data-science-process-data-blob.md).

## <a name="azure-data-science-in-action-example"></a>Пример применения обработки данных в Azure на практике
Пошаговое руководство с начала до конца пример hello процесс обработки и анализа данных Azure, используя открытый набор данных, в разделе [Azure процесс обработки и анализа данных в действие](machine-learning-data-science-process-sql-walkthrough.md).

[1]: ./media/machine-learning-data-science-process-sql-server-virtual-machine/reader_db_featurizedinput.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

