---
title: "Копировать aaaRepeatable в фабрике данных Azure | Документы Microsoft"
description: "Узнайте, как tooavoid дублирует несмотря на то, что срез, который копирует данных выполняется более одного раза."
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
ms.openlocfilehash: 79a3fde2b700bf0a0e167479d6a86c5bee1bf7ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="repeatable-copy-in-azure-data-factory"></a>Повторяющаяся операция копирования в фабрике данных Azure

## <a name="repeatable-read-from-relational-sources"></a>Повторяющиеся операции чтения из реляционных источников
При копировании данных из хранилища реляционных данных, сохранить повторяемость в виду tooavoid непредвиденные результаты. В фабрике данных Azure можно вручную повторно выполнить срез. Вы можете также настроить для набора данных политику повтора, чтобы при сбое срез выполнялся повторно. При повторном запуске срез в любом случае необходимо toomake, hello и те же данные, что считывается независимо от того, как запустить несколько раз срез.  
 
> [!NOTE]
> Hello следующие образцы для Azure SQL но применимо tooany хранилища данных, которое поддерживает прямоугольный наборов данных. Может иметь tooadjust hello **тип** источника и hello **запроса** свойства (например: запрос вместо sqlReaderQuery) hello данных хранения.   

Обычно при чтении из реляционных хранилищ можно только hello данные tooread соответствующий toothat среза. Поэтому toodo способом будет с помощью hello WindowStart и WindowEnd системные переменные, доступные в фабрике данных Azure. Узнайте, как hello переменные и функции в фабрике данных Azure в hello [фабрики данных Azure - функции и системные переменные](data-factory-functions-variables.md) статьи. Пример: 

```json
"source": {
    "type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm\\'', WindowStart, WindowEnd)"
},
```
Этот запрос считывает данные, которые попадают в hello срез длительность диапазона (WindowStart -> WindowEnd) из таблицы hello MyTable. Запустите этого среза также всегда благодаря приветствия, считывается и тех же данных. 

В других случаях можно назвать tooread hello всю таблицу и задайте hello sqlReaderQuery следующим образом:

```json
"source": 
{            
    "type": "SqlSource",
    "sqlReaderQuery": "select * from MyTable"
},
```

## <a name="repeatable-write-toosqlsink"></a>Повторяющиеся записи tooSqlSink
При копировании данных слишком**Azure SQL или SQL Server** из других хранилищ данных необходимо повторяемость tookeep в виду tooavoid непредвиденные результаты. 

При копировании данных tooAzure базы данных SQL и SQL Server, действие копирования hello добавляет таблицу приемник toohello данных по умолчанию. Предположим выполняется копирование данных из CSV (значения с разделителями запятыми) файла содержащего две записи toohello в следующей таблице в базе данных SQL или SQL Server. При выполнении среза hello две записи, скопированный toohello таблицы SQL. 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

Предположим, что обнаружены ошибки в файле исходного кода и обновить hello количество для работы с 2 too4. Если повторно запустить срез данных hello этого периода вручную, вы найдете две новые записи добавляются tooAzure базы данных SQL и SQL Server. В этом примере предполагается, что ни один из столбцов hello в таблице hello имеет hello первичного ключа.

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

tooavoid такое поведение, требуется использовать toospecify UPSERT семантику с помощью одного из следующих двух механизмов hello:

### <a name="mechanism-1-using-sqlwritercleanupscript"></a>Механизм 1: использование sqlWriterCleanupScript
Можно использовать hello **sqlWriterCleanupScript** tooclean свойство копирование данных из таблицы приемника hello перед вставкой данных hello, когда выполняется срез. 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

При выполнении среза hello скрипт очистки выполняется первый toodelete данных, соответствующий фрагмент toohello из таблицы SQL hello. Действие копирования Hello затем вставляет данные в таблицы SQL hello. При повторном запуске hello срез, количества hello обновляется при необходимости.

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

Предположим, что hello плоский Шайба запись удаляется из исходной csv hello. Затем повторное выполнение среза hello приведет к получению hello следующий результат: 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```

Действие копирования Hello выполнялись hello очистки сценария toodelete hello соответствующих данных для этого среза. Затем он считывают hello входные данные из CSV-файла hello (который затем содержится только одна запись) и вставлены hello таблицы. 

### <a name="mechanism-2-using-sliceidentifiercolumnname"></a>Механизм 2: использование sliceIdentifierColumnName
> [!IMPORTANT]
> Сейчас sliceIdentifierColumnName не поддерживается для хранилища данных SQL Azure. 

Hello второй механизм tooachieve повторяемость является наличие выделенного столбца (sliceIdentifierColumnName) в hello целевой таблицы. Этот столбец будет использоваться фабрики данных Azure tooensure hello источника и назначения Оставайтесь синхронизированы. Такой подход работает, когда гибкие возможности изменения или определение схемы таблицы SQL hello назначения. 

Этот столбец используется фабрикой данных Azure в целях обеспечения и в процессе hello фабрики данных Azure не выполняет ни одной схеме изменяет toohello таблицы. Способ toouse этот подход:

1. Определение столбца типа **двоичный файл (32)** в конечном hello таблицы SQL. Для этого столбца не должно быть никаких ограничений. Для нашего примера давайте назовем столбец AdfSliceIdentifier.


    Исходная таблица:

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL
    )
    ```

    Целевая таблица: 

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL,
       [AdfSliceIdentifier] [binary](32) NULL
    )
    ```

2. Используйте его в действие hello копирования следующим образом:
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "AdfSliceIdentifier"
    }
    ```

Фабрика данных Azure помещают в этот столбец согласно необходимости tooensure hello источника и назначения сохранить синхронизацию. Hello значения этого столбца не должно использоваться за пределами этого контекста. 

Аналогичные toomechanism 1, действие копирования автоматически очищает данные hello для hello даны срез hello целевой таблицы SQL. Затем он вставляет данные из источника в целевую таблицу toohello. 

## <a name="next-steps"></a>Дальнейшие действия
Просмотрите следующие соединителя статьи, в которых для полные примеры JSON hello. 

- [База данных SQL Azure;](data-factory-azure-sql-connector.md)
- [Хранилище данных SQL Azure](data-factory-azure-sql-data-warehouse-connector.md)
- [SQL Server](data-factory-sqlserver-connector.md)