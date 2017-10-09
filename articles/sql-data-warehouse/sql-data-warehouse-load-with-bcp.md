---
title: "aaaUse bcp tooload данных в хранилище данных SQL | Документы Microsoft"
description: "Узнать, какие bcp и как toouse его для сценариев хранилища данных."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: f9467d11-fcd6-4131-a65a-2022d2c32d24
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 09a2980585097644924c71899f9e74fb32fbc26d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-bcp"></a>Загрузка данных с помощью bcp
> [!div class="op_single_selector"]
> * [Redgate](sql-data-warehouse-load-with-redgate.md)  
> * [Фабрика данных](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [PolyBase;](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [BCP](sql-data-warehouse-load-with-bcp.md)
> 
> 

**[BCP] [ bcp]**  — это программа командной строки массового нагрузки, которая позволяет вам toocopy данных между SQL Server, файлы данных и хранилище данных SQL. Использование bcp tooimport большого количества строк в таблицах хранилища данных SQL или tooexport данные из таблиц SQL Server в файлы данных. За исключением случаев использования с параметром queryout hello bcp не требует знания языка Transact-SQL.

Программа bcp является простым и быстрым способом toomove небольшие наборы данных в действие и из базы данных хранилища данных SQL. будет зависеть от Hello точное количество данных, рекомендуется использовать tooload или извлечение посредством bcp в сети центра обработки данных Azure toohello соединения.  Обычно таблицы измерений можно быстро загружать и извлекать с помощью средства bcp, только если речь не идет о больших объемах данных.  Polybase — hello, рекомендуется использовать средство для загрузки и извлечения больших объемов данных, как лучше всего выполняют использование hello архитектура расширенной параллельной обработки хранилища данных SQL.

С помощью программы bcp можно выполнять следующие действия.

* Используйте tooload простая программа командной строки данных в хранилище данных SQL.
* Используйте tooextract простая программа командной строки данных из хранилища данных SQL.

В этом учебнике показано, как выполнять следующие действия.

* Импорт данных в таблицу с использованием команды hello bcp
* Экспорт данных из таблицы bcp hello подписку команды

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="prerequisites"></a>Предварительные требования
toostep изучения этого руководства требуется:

* База данных хранилища данных SQL
* установить программы командной строки bcp Hello
* Hello установлена программа командной строки SQLCMD

> [!NOTE]
> Можно загрузить служебные программы bcp и sqlcmd hello hello [центра загрузки Майкрософт][Microsoft Download Center].
> 
> 

## <a name="import-data-into-sql-data-warehouse"></a>Импорт данных в хранилище данных SQL
В этом учебнике будет создать таблицу в хранилище данных SQL Azure и импортировать данные в таблицу hello.

### <a name="step-1-create-a-table-in-azure-sql-data-warehouse"></a>Шаг 1. Создание таблицы в хранилище данных SQL Azure
Из командной строки используйте следующие toocreate запроса таблицы в экземпляре hello toorun sqlcmd:

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

> [!NOTE]
> В разделе [Общие сведения о таблицах] [ Table Overview] или [синтаксис инструкции CREATE TABLE] [ CREATE TABLE syntax] Дополнительные сведения о создании таблиц в хранилище данных SQL и hello  параметры, доступные в предложении WITH hello.
> 
> 

### <a name="step-2-create-a-source-data-file"></a>Шаг 2. Создание файла источника данных
Откройте Блокнот и скопируйте hello следующие строки данных в новый текстовый файл и сохраните этот файл tooyour локальный временный каталог, C:\Temp\DimDate2.txt.

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

> [!NOTE]
> Это важные tooremember, bcp.exe не поддерживает кодировку UTF-8 hello файла. Используйте файлы в кодировке ASCII или UTF-16 для файлов при работе со средством bcp.exe.
> 
> 

### <a name="step-3-connect-and-import-hello-data"></a>Шаг 3: Подключение и импортировать данные hello
Использование программы bcp, можно подключиться и импортировать данные hello, с помощью hello, следующая команда вместо hello соответствующим образом значения:

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t  ','
```

Это можно проверить hello загрузки данных, выполнив hello в следующем запросе, с помощью программы sqlcmd.

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

Данный метод должен вернуть hello следующие результаты:

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

### <a name="step-4-create-statistics-on-your-newly-loaded-data"></a>Шаг 4. Создание статистики для вновь загруженных данных
Хранилище данных SQL Azure пока не поддерживает автоматическое создание или автоматическое обновление статистики. В порядке tooget hello наилучшей производительности запросов очень важно создать статистику для всех столбцов всех таблиц после первой загрузки hello или любые существенные изменения происходят в данных hello. Подробное описание статистики см. в разделе hello [статистики] [ Statistics] раздела hello разработка группы разделов. Ниже приведен краткий пример порядка загрузки toocreate статистики по возвращающая hello в этом примере

Выполните следующие инструкции CREATE STATISTICS в командной строке sqlcmd hello:

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="export-data-from-sql-data-warehouse"></a>Экспорт данных из хранилища данных SQL
Работая с этим учебником, вы создадите файл данных из таблицы, находящейся в хранилище данных SQL. Мы экспортируем hello данных, созданной ранее tooa вызывается DimDate2_export.txt новый файл данных.

### <a name="step-1-export-hello-data"></a>Шаг 1: Экспорт данных hello
Программа bcp hello можно подключиться и экспорт данных с помощью hello, следующая команда вместо hello соответствующим образом значения:

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
Вы можете проверить данные были правильно экспортированы путем открытия нового файла hello приветствия. Hello данные в файл hello должны соответствовать текст hello ниже:

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

> [!NOTE]
> Из-за особенностей toohello распределенных систем порядок hello данных может быть таким же hello по базам данных хранилища данных SQL. Другой вариант — toouse hello **queryout** функции bcp toowrite запрос извлечения, а не экспортировать hello всей таблицы.
> 
> 

## <a name="next-steps"></a>Дальнейшие действия
Общие сведения о загрузке см. в статье [Загрузка данных в хранилище данных SQL][Load data into SQL Data Warehouse].
Дополнительные советы по разработке см. в статье [Проектные решения и методики программирования для хранилища данных SQL][SQL Data Warehouse development overview].

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
