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
# <a name="repeatable-copy-in-azure-data-factory"></a><span data-ttu-id="600b4-103">Повторяющаяся операция копирования в фабрике данных Azure</span><span class="sxs-lookup"><span data-stu-id="600b4-103">Repeatable copy in Azure Data Factory</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="600b4-104">Повторяющиеся операции чтения из реляционных источников</span><span class="sxs-lookup"><span data-stu-id="600b4-104">Repeatable read from relational sources</span></span>
<span data-ttu-id="600b4-105">При копировании данных из хранилища реляционных данных, сохранить повторяемость в виду tooavoid непредвиденные результаты.</span><span class="sxs-lookup"><span data-stu-id="600b4-105">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="600b4-106">В фабрике данных Azure можно вручную повторно выполнить срез.</span><span class="sxs-lookup"><span data-stu-id="600b4-106">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="600b4-107">Вы можете также настроить для набора данных политику повтора, чтобы при сбое срез выполнялся повторно.</span><span class="sxs-lookup"><span data-stu-id="600b4-107">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="600b4-108">При повторном запуске срез в любом случае необходимо toomake, hello и те же данные, что считывается независимо от того, как запустить несколько раз срез.</span><span class="sxs-lookup"><span data-stu-id="600b4-108">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span>  
 
> [!NOTE]
> <span data-ttu-id="600b4-109">Hello следующие образцы для Azure SQL но применимо tooany хранилища данных, которое поддерживает прямоугольный наборов данных.</span><span class="sxs-lookup"><span data-stu-id="600b4-109">hello following samples are for Azure SQL but are applicable tooany data store that supports rectangular datasets.</span></span> <span data-ttu-id="600b4-110">Может иметь tooadjust hello **тип** источника и hello **запроса** свойства (например: запрос вместо sqlReaderQuery) hello данных хранения.</span><span class="sxs-lookup"><span data-stu-id="600b4-110">You may have tooadjust hello **type** of source and hello **query** property (for example: query instead of sqlReaderQuery) for hello data store.</span></span>   

<span data-ttu-id="600b4-111">Обычно при чтении из реляционных хранилищ можно только hello данные tooread соответствующий toothat среза.</span><span class="sxs-lookup"><span data-stu-id="600b4-111">Usually, when reading from relational stores, you want tooread only hello data corresponding toothat slice.</span></span> <span data-ttu-id="600b4-112">Поэтому toodo способом будет с помощью hello WindowStart и WindowEnd системные переменные, доступные в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="600b4-112">A way toodo so would be by using hello WindowStart and WindowEnd system variables available in Azure Data Factory.</span></span> <span data-ttu-id="600b4-113">Узнайте, как hello переменные и функции в фабрике данных Azure в hello [фабрики данных Azure - функции и системные переменные](data-factory-functions-variables.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="600b4-113">Read about hello variables and functions in Azure Data Factory here in hello [Azure Data Factory - Functions and System Variables](data-factory-functions-variables.md) article.</span></span> <span data-ttu-id="600b4-114">Пример:</span><span class="sxs-lookup"><span data-stu-id="600b4-114">Example:</span></span> 

```json
"source": {
    "type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm\\'', WindowStart, WindowEnd)"
},
```
<span data-ttu-id="600b4-115">Этот запрос считывает данные, которые попадают в hello срез длительность диапазона (WindowStart -> WindowEnd) из таблицы hello MyTable.</span><span class="sxs-lookup"><span data-stu-id="600b4-115">This query reads data that falls in hello slice duration range (WindowStart -> WindowEnd) from hello table MyTable.</span></span> <span data-ttu-id="600b4-116">Запустите этого среза также всегда благодаря приветствия, считывается и тех же данных.</span><span class="sxs-lookup"><span data-stu-id="600b4-116">Rerun of this slice would also always ensure that hello same data is read.</span></span> 

<span data-ttu-id="600b4-117">В других случаях можно назвать tooread hello всю таблицу и задайте hello sqlReaderQuery следующим образом:</span><span class="sxs-lookup"><span data-stu-id="600b4-117">In other cases, you may wish tooread hello entire table and may define hello sqlReaderQuery as follows:</span></span>

```json
"source": 
{            
    "type": "SqlSource",
    "sqlReaderQuery": "select * from MyTable"
},
```

## <a name="repeatable-write-toosqlsink"></a><span data-ttu-id="600b4-118">Повторяющиеся записи tooSqlSink</span><span class="sxs-lookup"><span data-stu-id="600b4-118">Repeatable write tooSqlSink</span></span>
<span data-ttu-id="600b4-119">При копировании данных слишком**Azure SQL или SQL Server** из других хранилищ данных необходимо повторяемость tookeep в виду tooavoid непредвиденные результаты.</span><span class="sxs-lookup"><span data-stu-id="600b4-119">When copying data too**Azure SQL/SQL Server** from other data stores, you need tookeep repeatability in mind tooavoid unintended outcomes.</span></span> 

<span data-ttu-id="600b4-120">При копировании данных tooAzure базы данных SQL и SQL Server, действие копирования hello добавляет таблицу приемник toohello данных по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="600b4-120">When copying data tooAzure SQL/SQL Server Database, hello copy activity appends data toohello sink table by default.</span></span> <span data-ttu-id="600b4-121">Предположим выполняется копирование данных из CSV (значения с разделителями запятыми) файла содержащего две записи toohello в следующей таблице в базе данных SQL или SQL Server.</span><span class="sxs-lookup"><span data-stu-id="600b4-121">Say, you are copying data from a CSV (comma-separated values) file containing two records toohello following table in an Azure SQL/SQL Server Database.</span></span> <span data-ttu-id="600b4-122">При выполнении среза hello две записи, скопированный toohello таблицы SQL.</span><span class="sxs-lookup"><span data-stu-id="600b4-122">When a slice runs, hello two records are copied toohello SQL table.</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

<span data-ttu-id="600b4-123">Предположим, что обнаружены ошибки в файле исходного кода и обновить hello количество для работы с 2 too4.</span><span class="sxs-lookup"><span data-stu-id="600b4-123">Suppose you found errors in source file and updated hello quantity of Down Tube from 2 too4.</span></span> <span data-ttu-id="600b4-124">Если повторно запустить срез данных hello этого периода вручную, вы найдете две новые записи добавляются tooAzure базы данных SQL и SQL Server.</span><span class="sxs-lookup"><span data-stu-id="600b4-124">If you rerun hello data slice for that period manually, you’ll find two new records appended tooAzure SQL/SQL Server Database.</span></span> <span data-ttu-id="600b4-125">В этом примере предполагается, что ни один из столбцов hello в таблице hello имеет hello первичного ключа.</span><span class="sxs-lookup"><span data-stu-id="600b4-125">This example assumes that none of hello columns in hello table has hello primary key constraint.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="600b4-126">tooavoid такое поведение, требуется использовать toospecify UPSERT семантику с помощью одного из следующих двух механизмов hello:</span><span class="sxs-lookup"><span data-stu-id="600b4-126">tooavoid this behavior, you need toospecify UPSERT semantics by using one of hello following two mechanisms:</span></span>

### <a name="mechanism-1-using-sqlwritercleanupscript"></a><span data-ttu-id="600b4-127">Механизм 1: использование sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="600b4-127">Mechanism 1: using sqlWriterCleanupScript</span></span>
<span data-ttu-id="600b4-128">Можно использовать hello **sqlWriterCleanupScript** tooclean свойство копирование данных из таблицы приемника hello перед вставкой данных hello, когда выполняется срез.</span><span class="sxs-lookup"><span data-stu-id="600b4-128">You can use hello **sqlWriterCleanupScript** property tooclean up data from hello sink table before inserting hello data when a slice is run.</span></span> 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

<span data-ttu-id="600b4-129">При выполнении среза hello скрипт очистки выполняется первый toodelete данных, соответствующий фрагмент toohello из таблицы SQL hello.</span><span class="sxs-lookup"><span data-stu-id="600b4-129">When a slice runs, hello cleanup script is run first toodelete data that corresponds toohello slice from hello SQL table.</span></span> <span data-ttu-id="600b4-130">Действие копирования Hello затем вставляет данные в таблицы SQL hello.</span><span class="sxs-lookup"><span data-stu-id="600b4-130">hello copy activity then inserts data into hello SQL Table.</span></span> <span data-ttu-id="600b4-131">При повторном запуске hello срез, количества hello обновляется при необходимости.</span><span class="sxs-lookup"><span data-stu-id="600b4-131">If hello slice is rerun, hello quantity is updated as desired.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="600b4-132">Предположим, что hello плоский Шайба запись удаляется из исходной csv hello.</span><span class="sxs-lookup"><span data-stu-id="600b4-132">Suppose hello Flat Washer record is removed from hello original csv.</span></span> <span data-ttu-id="600b4-133">Затем повторное выполнение среза hello приведет к получению hello следующий результат:</span><span class="sxs-lookup"><span data-stu-id="600b4-133">Then rerunning hello slice would produce hello following result:</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="600b4-134">Действие копирования Hello выполнялись hello очистки сценария toodelete hello соответствующих данных для этого среза.</span><span class="sxs-lookup"><span data-stu-id="600b4-134">hello copy activity ran hello cleanup script toodelete hello corresponding data for that slice.</span></span> <span data-ttu-id="600b4-135">Затем он считывают hello входные данные из CSV-файла hello (который затем содержится только одна запись) и вставлены hello таблицы.</span><span class="sxs-lookup"><span data-stu-id="600b4-135">Then it read hello input from hello csv (which then contained only one record) and inserted it into hello Table.</span></span> 

### <a name="mechanism-2-using-sliceidentifiercolumnname"></a><span data-ttu-id="600b4-136">Механизм 2: использование sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="600b4-136">Mechanism 2: using sliceIdentifierColumnName</span></span>
> [!IMPORTANT]
> <span data-ttu-id="600b4-137">Сейчас sliceIdentifierColumnName не поддерживается для хранилища данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="600b4-137">Currently, sliceIdentifierColumnName is not supported for Azure SQL Data Warehouse.</span></span> 

<span data-ttu-id="600b4-138">Hello второй механизм tooachieve повторяемость является наличие выделенного столбца (sliceIdentifierColumnName) в hello целевой таблицы.</span><span class="sxs-lookup"><span data-stu-id="600b4-138">hello second mechanism tooachieve repeatability is by having a dedicated column (sliceIdentifierColumnName) in hello target Table.</span></span> <span data-ttu-id="600b4-139">Этот столбец будет использоваться фабрики данных Azure tooensure hello источника и назначения Оставайтесь синхронизированы.</span><span class="sxs-lookup"><span data-stu-id="600b4-139">This column would be used by Azure Data Factory tooensure hello source and destination stay synchronized.</span></span> <span data-ttu-id="600b4-140">Такой подход работает, когда гибкие возможности изменения или определение схемы таблицы SQL hello назначения.</span><span class="sxs-lookup"><span data-stu-id="600b4-140">This approach works when there is flexibility in changing or defining hello destination SQL Table schema.</span></span> 

<span data-ttu-id="600b4-141">Этот столбец используется фабрикой данных Azure в целях обеспечения и в процессе hello фабрики данных Azure не выполняет ни одной схеме изменяет toohello таблицы.</span><span class="sxs-lookup"><span data-stu-id="600b4-141">This column is used by Azure Data Factory for repeatability purposes and in hello process Azure Data Factory does not make any schema changes toohello Table.</span></span> <span data-ttu-id="600b4-142">Способ toouse этот подход:</span><span class="sxs-lookup"><span data-stu-id="600b4-142">Way toouse this approach:</span></span>

1. <span data-ttu-id="600b4-143">Определение столбца типа **двоичный файл (32)** в конечном hello таблицы SQL.</span><span class="sxs-lookup"><span data-stu-id="600b4-143">Define a column of type **binary (32)** in hello destination SQL Table.</span></span> <span data-ttu-id="600b4-144">Для этого столбца не должно быть никаких ограничений.</span><span class="sxs-lookup"><span data-stu-id="600b4-144">There should be no constraints on this column.</span></span> <span data-ttu-id="600b4-145">Для нашего примера давайте назовем столбец AdfSliceIdentifier.</span><span class="sxs-lookup"><span data-stu-id="600b4-145">Let's name this column as AdfSliceIdentifier for this example.</span></span>


    <span data-ttu-id="600b4-146">Исходная таблица:</span><span class="sxs-lookup"><span data-stu-id="600b4-146">Source table:</span></span>

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL
    )
    ```

    <span data-ttu-id="600b4-147">Целевая таблица:</span><span class="sxs-lookup"><span data-stu-id="600b4-147">Destination table:</span></span> 

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL,
       [AdfSliceIdentifier] [binary](32) NULL
    )
    ```

2. <span data-ttu-id="600b4-148">Используйте его в действие hello копирования следующим образом:</span><span class="sxs-lookup"><span data-stu-id="600b4-148">Use it in hello copy activity as follows:</span></span>
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "AdfSliceIdentifier"
    }
    ```

<span data-ttu-id="600b4-149">Фабрика данных Azure помещают в этот столбец согласно необходимости tooensure hello источника и назначения сохранить синхронизацию.</span><span class="sxs-lookup"><span data-stu-id="600b4-149">Azure Data Factory populates this column as per its need tooensure hello source and destination stay synchronized.</span></span> <span data-ttu-id="600b4-150">Hello значения этого столбца не должно использоваться за пределами этого контекста.</span><span class="sxs-lookup"><span data-stu-id="600b4-150">hello values of this column should not be used outside of this context.</span></span> 

<span data-ttu-id="600b4-151">Аналогичные toomechanism 1, действие копирования автоматически очищает данные hello для hello даны срез hello целевой таблицы SQL.</span><span class="sxs-lookup"><span data-stu-id="600b4-151">Similar toomechanism 1, Copy Activity automatically cleans up hello data for hello given slice from hello destination SQL Table.</span></span> <span data-ttu-id="600b4-152">Затем он вставляет данные из источника в целевую таблицу toohello.</span><span class="sxs-lookup"><span data-stu-id="600b4-152">It then inserts data from source in toohello destination table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="600b4-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="600b4-153">Next steps</span></span>
<span data-ttu-id="600b4-154">Просмотрите следующие соединителя статьи, в которых для полные примеры JSON hello.</span><span class="sxs-lookup"><span data-stu-id="600b4-154">Review hello following connector articles that for complete JSON examples:</span></span> 

- [<span data-ttu-id="600b4-155">База данных SQL Azure;</span><span class="sxs-lookup"><span data-stu-id="600b4-155">Azure SQL Database</span></span>](data-factory-azure-sql-connector.md)
- [<span data-ttu-id="600b4-156">Хранилище данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="600b4-156">Azure SQL Data Warehouse</span></span>](data-factory-azure-sql-data-warehouse-connector.md)
- [<span data-ttu-id="600b4-157">SQL Server</span><span class="sxs-lookup"><span data-stu-id="600b4-157">SQL Server</span></span>](data-factory-sqlserver-connector.md)