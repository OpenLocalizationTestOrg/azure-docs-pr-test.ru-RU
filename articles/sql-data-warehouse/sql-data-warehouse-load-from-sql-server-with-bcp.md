---
title: "aaaLoad данные из SQL Server в хранилище данных SQL Azure (bcp) | Документы Microsoft"
description: "Для данных небольшого объема использует bcp tooexport данные из файлов tooflat SQL Server и импортировать hello данные непосредственно в хранилище данных SQL Azure."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: f87d8d7c-8276-43c5-90e7-d4ccc0e3a224
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: a03b5403d123e8814ae73a7cce8e6851c8b264a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-flat-files"></a>Загрузка данных из SQL Server в хранилище данных SQL Azure (неструктурированные файлы)
> [!div class="op_single_selector"]
> * [SSIS](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [PolyBase;](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [bcp](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

Для небольших наборов данных можно использовать данные tooexport программы командной строки bcp hello из SQL Server и затем загрузить его напрямую tooAzure хранилище данных SQL.

В этом руководстве описывается, как с помощью bcp выполнять следующие действия:

* Экспортировать таблицу из из SQL Server с помощью команды bcp hello команды (или создайте простой образец файла)
* Импорт таблицы hello из неструктурированного файла tooSQL хранилища данных.
* Создание статистики для hello загрузки данных.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="before-you-begin"></a>Перед началом работы
### <a name="prerequisites"></a>Предварительные требования
toostep изучения этого руководства требуется:

* База данных хранилища данных SQL
* Программа командной строки bcp Hello установлен
* Программа командной строки sqlcmd Hello установлен

Можно загрузить служебные программы bcp и sqlcmd hello hello [центра загрузки Майкрософт][Microsoft Download Center].

### <a name="data-in-ascii-or-utf-16-format"></a>Данные в формате ASCII или UTF-16
Если вы пытаетесь этот учебник с вашими собственными данными, данные требуют toouse hello ASCII или кодировку UTF-16, так как bcp поддерживает UTF-8. 

PolyBase поддерживает UTF-8, но еще не поддерживает UTF-16. Обратите внимание, что если требуется toocombine bcp с PolyBase вам потребуется hello данных tootransform tooUTF-8 после экспорта из SQL Server. 

## <a name="1-create-a-destination-table"></a>1. Создание целевой таблицы
Определение таблицы в хранилище данных SQL, который будет hello целевой таблице для загрузки hello. Hello столбцов в таблице hello должно соответствовать toohello данных в каждой строке файла данных.

toocreate таблицу, откройте командную строку и использовать hello toorun sqlcmd.exe следующую команду:

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    CREATE TABLE DimDate2
    (
        DateId INT NOT NULL,
        CalendarQuarter TINYINT NOT NULL,
        FiscalQuarter TINYINT NOT NULL
    )
    WITH
    (
        CLUSTERED COLUMNSTORE INDEX,
        DISTRIBUTION = ROUND_ROBIN
    );
"
```


## <a name="2-create-a-source-data-file"></a>2. Создание файла источника данных
Откройте Блокнот и скопируйте hello следующие строки данных в новый текстовый файл и сохраните этот файл tooyour локальный временный каталог, C:\Temp\DimDate2.txt. Эти данные имеют формат ASCII.

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

(Необязательно) tooexport данные из базы данных SQL Server, откройте командную строку и запустите следующую команду hello. Замените значения TableName, ServerName, DatabaseName, Username и Password на собственные.

```sql
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t ','
```



## <a name="3-load-hello-data"></a>3. Загрузка данных hello
tooload hello данных, откройте командную строку и запустите hello следующую команду, заменив своих собственных сведений значениями hello имя сервера, имя базы данных, имя пользователя и пароль.

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ','
```

Используйте эти данные hello tooverify команда была загружена неправильно

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

Hello результаты должны выглядеть следующим образом:

| DateId | CalendarQuarter | FiscalQuarter |
| --- | --- | --- |
| 20150101 |1 |3 |
| 20150201 |1 |3 |
| 20150301 |1 |3 |
| 20150401 |2 |4 |
| 20150501 |2 |4 |
| 20150601 |2 |4 |
| 20150701 |3 |1 |
| 20150801 |3 |1 |
| 20150801 |3 |1 |
| 20151001 |4 |2 |
| 20151101 |4 |2 |
| 20151201 |4 |2 |

## <a name="4-create-statistics"></a>4. Создание статистики
Хранилище данных SQL пока не поддерживает автоматическое создание или автоматическое обновление статистики. tooget hello наилучшую производительность запросов, является важным toocreate статистику для всех столбцов всех таблиц после первой загрузки hello или после любой значительных изменений в данных hello. Дополнительные сведения см. в статье об [управлении статистикой][Statistics]. 

Выполните следующие команды toocreate статистики для вновь загруженных таблицы hello.

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="5-export-data-from-sql-data-warehouse"></a>5. Экспорт данных из хранилища данных SQL
Для практики можно экспортировать данные hello, которая загружается обратно из хранилища данных SQL.  Команда tooexport Hello hello ровно то же, что экспорт из SQL Server.

Однако есть различия в результатах hello. Поскольку данные hello хранятся в распределенные места в хранилище данных SQL, при экспорте данных каждый вычислительный узел записывает его данных toohello выходного файла. порядок Hello hello данные в выходной файл hello является вероятностью toobe отличается от порядка hello hello данных во входном файле hello.

### <a name="export-a-table-and-compare-exported-results"></a>Экспорт таблицы и сравнение результатов экспорта
toosee hello экспортированных данных, откройте командную строку и выполните следующую команду, используя свои собственные параметры. Имя сервера — имя hello Azure логического сервера SQL.

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
Вы можете проверить данные были правильно экспортированы путем открытия нового файла hello приветствия. Hello данные в файле hello должен соответствовать текст hello ниже, но скорее всего будут отсортированы в порядке, отличающемся:

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

### <a name="export-hello-results-of-a-query"></a>Экспорт hello результатов запроса
Можно использовать hello **queryout** функции bcp tooexport hello результатов запроса, вместо экспорта hello всей таблицы. 

## <a name="next-steps"></a>Дальнейшие действия
Общие сведения о загрузке см. в статье [Загрузка данных в хранилище данных SQL][Load data into SQL Data Warehouse].
Дополнительные советы по разработке см. в статье [Проектные решения и методики программирования для хранилища данных SQL][SQL Data Warehouse development overview].
Дополнительные сведения о создании таблицы в хранилище данных SQL см. в статьях, посвященных [таблицам в хранилище данных SQL][Table Overview] и [синтаксису инструкции CREATE TABLE][CREATE TABLE syntax].

<!--Image references-->

<!--Article references-->

[Load data into SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[Table Overview]: ./sql-data-warehouse-tables-overview.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
