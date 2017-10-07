---
title: "aaaGuide по использованию PolyBase в хранилище данных SQL | Документы Microsoft"
description: "Правила и рекомендации по использованию PolyBase в сценариях с хранилищем данных SQL."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 4757fce1-96b3-48ea-8a51-be1385705f9f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 6/5/2016
ms.custom: loading
ms.author: cakarst;barbkess
ms.openlocfilehash: b05e4c5d528f2fe1c60d6855b5333065f0c908ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="guide-for-using-polybase-in-sql-data-warehouse"></a>Руководство по использованию PolyBase в хранилище данных SQL
Это руководство содержит практические сведения об использовании PolyBase в хранилище данных SQL.

tooget работы см. в разделе hello [загрузки данных с помощью PolyBase] [ Load data with PolyBase] учебника.

## <a name="rotating-storage-keys"></a>Ротация ключей хранилищ данных
Из tootime времени требуется хранилище больших двоичных объектов tooyour ключа доступа hello toochange по соображениям безопасности.

Здравствуйте, элегантный tooperform способом, эта задача является toofollow процесса, известного как «смена ключей hello». Возможно, вы уже заметили, что для учетной записи хранения больших двоичных объектов имеется два ключа хранения. Это необходимо для перехода

Ротация ключей учетной записи хранения Azure представляет собой простой процесс из трех шагов

1. Создайте второй учетные данные уровня базы данных, на основе ключа доступа к дополнительному хранилищу hello
2. Создайте второй внешний источник данных, основанных на этих учетных данных
3. Удалите и создайте hello внешних таблиц, указывающий toohello новый внешний источник данных

Если вы перенесли все внешние таблицы toohello новый внешний источник данных можно выполнять hello Очистка задачи:

1. Удалите первый внешний источник данных
2. Области DROP первой базы данных на основе ключа доступа hello основного хранилища учетных данных
3. Войдите в Azure и выполните повторное формирование hello первичный ключ доступа к hello в следующий раз

## <a name="query-azure-blob-storage-data"></a>Отправка запроса для данных хранилища больших двоичных объектов Azure
Запросы к внешним таблицам просто использовать имя таблицы hello так, будто он был реляционной таблице.

```sql
-- Query Azure storage resident data via external table.
SELECT * FROM [ext].[CarSensor_Data]
;
```

> [!NOTE]
> Запрос на внешнюю таблицу может завершиться с ошибкой hello *«запрос прерван — Достигнуто пороговое значение отклонения максимальное hello при чтении из внешнего источника»*. Это означает, что внешние данные содержат *«грязные»* записи. Запись данных считается «грязных», если hello фактические данные типы и количество столбцов не соответствуют определений столбцов hello hello внешней таблицы или hello данные не соответствуют toohello формат указанного внешнего файла. toofix это, убедитесь, что ваш внешней таблицы и определения формата внешнего файла указаны правильно и определения toothese соответствует данных из внешнего источника. В случае подмножество записей внешние данные "грязные", вы можете tooreject эти записи для запросов с помощью параметров отклонить hello в CREATE DDL ВНЕШНЕЙ таблицы.
> 
> 

## <a name="load-data-from-azure-blob-storage"></a>Загрузка данных из хранилища больших двоичных объектов Azure
В этом примере загружает данные из базы данных хранилища tooSQL хранилища BLOB-объектов Azure.

Хранение данных непосредственно удаляет hello время передачи данных для запросов. Хранение данных с индексом columnstore повышает производительность запросов для анализа запросов путем копирования too10x.

В этом примере данные tooload инструкции CREATE TABLE AS SELECT hello. Новая таблица Hello наследует hello столбцы с именем в запросе hello. Определение внешней таблицы hello наследование hello типы данных этих столбцов.

CREATE TABLE AS SELECT является высокопроизводительных инструкции Transact-SQL, который загружает данные hello в параллельных tooall hello вычислительные узлы хранилище данных SQL.  Оно было разработано для обработчика расширенной параллельной обработке (MPP) hello в Analytics Platform System и находится в хранилище данных SQL.

```sql
-- Load data from Azure blob storage tooSQL Data Warehouse

CREATE TABLE [dbo].[Customer_Speed]
WITH
(   
    CLUSTERED COLUMNSTORE INDEX
,    DISTRIBUTION = HASH([CarSensor_Data].[CustomerKey])
)
AS
SELECT *
FROM   [ext].[CarSensor_Data]
;
```

Ознакомьтесь с разделом [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].

## <a name="create-statistics-on-newly-loaded-data"></a>Создание статистики для вновь загруженных данных
Хранилище данных SQL Azure пока не поддерживает автоматическое создание или автоматическое обновление статистики.  В порядке tooget hello наилучшей производительности запросов очень важно создать статистику для всех столбцов всех таблиц после первой загрузки hello или любые существенные изменения происходят в данных hello.  Подробное описание статистики см. в разделе hello [статистики] [ Statistics] раздела hello разработка группы разделов.  Ниже приведен краткий пример порядка загрузки toocreate статистики по возвращающая hello в этом примере.

```sql
create statistics [SensorKey] on [Customer_Speed] ([SensorKey]);
create statistics [CustomerKey] on [Customer_Speed] ([CustomerKey]);
create statistics [GeographyKey] on [Customer_Speed] ([GeographyKey]);
create statistics [Speed] on [Customer_Speed] ([Speed]);
create statistics [YearMeasured] on [Customer_Speed] ([YearMeasured]);
```

## <a name="export-data-tooazure-blob-storage"></a>Экспорт хранилища BLOB-объект данных tooAzure
В этом разделе показано, как tooexport данные из хранилища данных SQL tooAzure хранилище больших двоичных объектов. В этом примере используется CREATE EXTERNAL TABLE AS SELECT передаются высокой высокопроизводительных Transact-SQL инструкции tooexport hello данные в параллельном режиме из всех hello вычислительных узлов.

Hello пример создает внешнюю таблицу Weblogs2014 с помощью определения столбцов и данных из dbo. Таблица диалоги. Определение внешней таблицы Hello хранится в хранилище данных SQL и hello результаты инструкции SELECT hello, экспортированный toohello каталог «/ архивировать/log2014 /» в указанный источником данных hello контейнер больших двоичных объектов hello. Hello данные экспортируются в формате файла указанный текст hello.

```sql
CREATE EXTERNAL TABLE Weblogs2014 WITH
(
    LOCATION='/archive/log2014/',
    DATA_SOURCE=azure_storage,
    FILE_FORMAT=text_file_format
)
AS
SELECT
    Uri,
    DateRequested
FROM
    dbo.Weblogs
WHERE
    1=1
    AND DateRequested > '12/31/2013'
    AND DateRequested < '01/01/2015';
```
## <a name="isolate-loading-users"></a>Ограничение возможности загрузки для пользователей
Обычно имеется toohave необходимость нескольких пользователей, которые можно загружать данные в хранилища данных SQL. Поскольку hello [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] требуются разрешения УПРАВЛЕНИЯ hello базы данных, вы получите нескольких пользователей с помощью управления доступом по всем схемам. toolimit это, можно с помощью инструкции DENY УПРАВЛЕНИЯ hello.

Пример. Рассмотрим схемы базы данных schema_A для отдела A и schema_B для отдела B. Задайте пользователей базы данных user_A и user_B в качестве пользователей для загрузки PolyBase в отделе A и B соответственно. Им обоим предоставлены разрешения CONTROL для базы данных.
Создатели Hello схемы A и B теперь заблокировать их схем с помощью DENY:

```sql
   DENY CONTROL ON SCHEMA :: schema_A toouser_B;
   DENY CONTROL ON SCHEMA :: schema_B toouser_A;
```   
 Таким образом, user_A и user_B должны теперь блокировке hello схемы других подразделений.
 


## <a name="next-steps"></a>Дальнейшие действия
toolearn Дополнительные сведения о tooSQL перемещение данных хранилища данных. в разделе hello [Общие сведения о миграции данных][data migration overview].

<!--Image references-->

<!--Article references-->
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Load data with PolyBase]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[data migration overview]: ./sql-data-warehouse-overview-migrate.md

<!--MSDN references-->
[supported source/sink]: https://msdn.microsoft.com/library/dn894007.aspx
[copy activity]: https://msdn.microsoft.com/library/dn835035.aspx
[SQL Server destination adapter]: https://msdn.microsoft.com/library/ms141095.aspx
[SSIS]: https://msdn.microsoft.com/library/ms141026.aspx

[CREATE EXTERNAL DATA SOURCE (Transact-SQL)]: https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT (Transact-SQL)]: https://msdn.microsoft.com/library/dn935026.aspx
[CREATE EXTERNAL TABLE (Transact-SQL)]: https://msdn.microsoft.com/library/dn935021.aspx

[DROP EXTERNAL DATA SOURCE (Transact-SQL)]: https://msdn.microsoft.com/library/mt146367.aspx
[DROP EXTERNAL FILE FORMAT (Transact-SQL)]: https://msdn.microsoft.com/library/mt146379.aspx
[DROP EXTERNAL TABLE (Transact-SQL)]: https://msdn.microsoft.com/library/mt130698.aspx

[CREATE TABLE AS SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/mt204041.aspx
[INSERT...SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/ms174335.aspx
[CREATE MASTER KEY (Transact-SQL)]: https://msdn.microsoft.com/library/ms174382.aspx
[CREATE CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/ms189522.aspx
[CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/mt270260.aspx
[DROP CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/ms189450.aspx

<!-- External Links -->
