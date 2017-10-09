---
title: "aaaInvoke хранимой процедуры из действия копирования фабрики данных Azure | Документы Microsoft"
description: "Узнайте, как действие копирования tooinvoke хранимую процедуру в базе данных SQL Azure и SQL Server с фабрикой данных Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 986377118afb8c08607c2325fcc3ab00b3de9268
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-stored-procedure-from-copy-activity-in-azure-data-factory"></a>Вызов хранимой процедуры из действия копирования в фабрике данных Azure
При копировании данных в [SQL Server](data-factory-sqlserver-connector.md) или [базы данных SQL Azure](data-factory-azure-sql-connector.md), можно настроить hello **SqlSink** в tooinvoke действия копирования хранимой процедуры. Вы можете toouse hello хранимой процедуры tooperform перед вставкой данных в целевую таблицу toohello требуется дополнительная обработка (Объединение столбцов, поиск значений, вставлять в нескольких таблицах, т. д.). В этой функции используются [параметры с табличным значением](https://msdn.microsoft.com/library/bb675163.aspx). 

Следующий образец Hello показано, как tooinvoke хранимую процедуру в SQL Server базы данных из конвейера фабрики данных (действие копирования):  

## <a name="output-dataset-json"></a>Определение JSON выходного набора данных
В hello набор выходных данных JSON, задайте hello **тип** для: **SqlServerTable**. Задайте для него слишком**AzureSqlTable** toouse с базой данных Azure SQL. Здравствуйте, значение для **tableName** свойство должно соответствовать имени hello первый параметр hello хранимой процедуры.  

```json
{
  "name": "SqlOutput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlLinkedService",
    "typeProperties": {
      "tableName": "Marketing"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

## <a name="sqlsink-section-in-copy-activity-json"></a>Раздел SqlSink в определении JSON действия копирования
Определение hello **SqlSink** раздела действие копирования hello JSON. tooinvoke хранимой процедуры во время вставки данных в базу данных или объект назначения приемник hello, указать значения для **SqlWriterStoredProcedureName** и **SqlWriterTableType** свойства. Описание этих свойств см. в разделе [SqlSink раздел статьи соединителя SQL Server hello](data-factory-sqlserver-connector.md#sqlsink).

```json
"sink":
{
    "type": "SqlSink",
    "SqlWriterTableType": "MarketingType",
    "SqlWriterStoredProcedureName": "spOverwriteMarketing", 
    "storedProcedureParameters":
            {
                "stringData": 
                {
                    "value": "str1"     
                }
            }
}
```

## <a name="stored-procedure-definition"></a>Определение хранимой процедуры 
В базе данных, определить hello хранимой процедуры с hello одинаковые имена, как **SqlWriterStoredProcedureName**. Hello хранимой процедуры обрабатывает входные данные из хранилища данных источника hello и вставляет данные в таблицу в базе данных назначения hello. Имя Hello hello первый параметр хранимой процедуры должно соответствовать tableName hello, определенные в наборе данных hello JSON (маркетинг).

```sql
CREATE PROCEDURE spOverwriteMarketing @Marketing [dbo].[MarketingType] READONLY, @stringData varchar(256)
AS
BEGIN
    DELETE FROM [dbo].[Marketing] where ProfileID = @stringData
    INSERT [dbo].[Marketing](ProfileID, State)
    SELECT * FROM @Marketing
END
```

## <a name="table-type-definition"></a>Определение типа таблицы
В базе данных, определение типа таблицы hello с hello одинаковые имена, как **SqlWriterTableType**. Схема Hello hello табличного типа должна соответствовать схеме hello hello входного набора данных.

```sql
CREATE TYPE [dbo].[MarketingType] AS TABLE(
    [ProfileID] [varchar](256) NOT NULL,
    [State] [varchar](256) NOT NULL
)
```

## <a name="next-steps"></a>Дальнейшие действия
Просмотрите следующие соединителя статьи, в которых для полные примеры JSON hello. 

- [База данных SQL Azure;](data-factory-azure-sql-connector.md)
- [SQL Server](data-factory-sqlserver-connector.md)
