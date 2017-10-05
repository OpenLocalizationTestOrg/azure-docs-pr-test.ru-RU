---
title: "Повторяющаяся операция копирования в фабрике данных Azure | Документация Майкрософт"
description: "Узнайте, как избежать создания дубликатов даже при многократном выполнении среза, копирующего данные."
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
ms.openlocfilehash: 5b88a235915bf35fec701eee4a5f80beb4a67632
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="repeatable-copy-in-azure-data-factory"></a><span data-ttu-id="c2599-103">Повторяющаяся операция копирования в фабрике данных Azure</span><span class="sxs-lookup"><span data-stu-id="c2599-103">Repeatable copy in Azure Data Factory</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="c2599-104">Повторяющиеся операции чтения из реляционных источников</span><span class="sxs-lookup"><span data-stu-id="c2599-104">Repeatable read from relational sources</span></span>
<span data-ttu-id="c2599-105">При копировании данных из реляционных хранилищ важно помнить о повторяемости, чтобы избежать непредвиденных результатов.</span><span class="sxs-lookup"><span data-stu-id="c2599-105">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="c2599-106">В фабрике данных Azure можно вручную повторно выполнить срез.</span><span class="sxs-lookup"><span data-stu-id="c2599-106">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="c2599-107">Вы можете также настроить для набора данных политику повтора, чтобы при сбое срез выполнялся повторно.</span><span class="sxs-lookup"><span data-stu-id="c2599-107">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="c2599-108">При повторном выполнении среза в любом случае необходимо убедиться в том, что считываются те же данные, независимо от того, сколько раз выполняется срез.</span><span class="sxs-lookup"><span data-stu-id="c2599-108">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span>  
 
> [!NOTE]
> <span data-ttu-id="c2599-109">Приведенные ниже примеры предназначены для SQL Azure, но подходят для любого хранилища данных, поддерживающего прямоугольные наборы данных.</span><span class="sxs-lookup"><span data-stu-id="c2599-109">The following samples are for Azure SQL but are applicable to any data store that supports rectangular datasets.</span></span> <span data-ttu-id="c2599-110">Для хранилища данных может потребоваться настроить параметр **type** источника и свойство **query** (например, query вместо sqlReaderQuery).</span><span class="sxs-lookup"><span data-stu-id="c2599-110">You may have to adjust the **type** of source and the **query** property (for example: query instead of sqlReaderQuery) for the data store.</span></span>   

<span data-ttu-id="c2599-111">Обычно при чтении из реляционных хранилищ нужно считывать только данные, соответствующие этому срезу.</span><span class="sxs-lookup"><span data-stu-id="c2599-111">Usually, when reading from relational stores, you want to read only the data corresponding to that slice.</span></span> <span data-ttu-id="c2599-112">Сделать это можно с помощью системных переменных WindowStart и WindowEnd, доступных в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="c2599-112">A way to do so would be by using the WindowStart and WindowEnd system variables available in Azure Data Factory.</span></span> <span data-ttu-id="c2599-113">Сведения о переменных и функциях в фабрике данных Azure см. в статье [Фабрика данных Azure — функции и системные переменные](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="c2599-113">Read about the variables and functions in Azure Data Factory here in the [Azure Data Factory - Functions and System Variables](data-factory-functions-variables.md) article.</span></span> <span data-ttu-id="c2599-114">Пример:</span><span class="sxs-lookup"><span data-stu-id="c2599-114">Example:</span></span> 

```json
"source": {
    "type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm\\'', WindowStart, WindowEnd)"
},
```
<span data-ttu-id="c2599-115">Этот запрос считывает из таблицы MyTable все данные, которые попадают во временной диапазон среза (от WindowStart до WindowEnd).</span><span class="sxs-lookup"><span data-stu-id="c2599-115">This query reads data that falls in the slice duration range (WindowStart -> WindowEnd) from the table MyTable.</span></span> <span data-ttu-id="c2599-116">Повторное выполнение этого среза всегда возвращает одни и те же данные.</span><span class="sxs-lookup"><span data-stu-id="c2599-116">Rerun of this slice would also always ensure that the same data is read.</span></span> 

<span data-ttu-id="c2599-117">В других случаях может потребоваться чтение всей таблицы.Тогда sqlReaderQuery можно определить следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c2599-117">In other cases, you may wish to read the entire table and may define the sqlReaderQuery as follows:</span></span>

```json
"source": 
{            
    "type": "SqlSource",
    "sqlReaderQuery": "select * from MyTable"
},
```

## <a name="repeatable-write-to-sqlsink"></a><span data-ttu-id="c2599-118">Повторяемая запись в SqlSink</span><span class="sxs-lookup"><span data-stu-id="c2599-118">Repeatable write to SqlSink</span></span>
<span data-ttu-id="c2599-119">При копировании данных в **SQL Azure или SQL Server** из других хранилищ данных необходимо помнить о повторяемости, чтобы избежать незапланированных результатов.</span><span class="sxs-lookup"><span data-stu-id="c2599-119">When copying data to **Azure SQL/SQL Server** from other data stores, you need to keep repeatability in mind to avoid unintended outcomes.</span></span> 

<span data-ttu-id="c2599-120">Когда вы копируете данные в базу данных SQL Server, действие копирования по умолчанию добавляет данные в таблицу приемника.</span><span class="sxs-lookup"><span data-stu-id="c2599-120">When copying data to Azure SQL/SQL Server Database, the copy activity appends data to the sink table by default.</span></span> <span data-ttu-id="c2599-121">Предположим, что данные копируются из файла CSV (значения, разделенные запятыми), содержащего две записи, в следующую таблицу в базе данных SQL Server или Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="c2599-121">Say, you are copying data from a CSV (comma-separated values) file containing two records to the following table in an Azure SQL/SQL Server Database.</span></span> <span data-ttu-id="c2599-122">При выполнении среза в таблицу SQL копируются две записи.</span><span class="sxs-lookup"><span data-stu-id="c2599-122">When a slice runs, the two records are copied to the SQL table.</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

<span data-ttu-id="c2599-123">Теперь допустим, что в исходном файле вы нашли ошибку и изменили значение параметра Down Tube (изменив 2 на 4).</span><span class="sxs-lookup"><span data-stu-id="c2599-123">Suppose you found errors in source file and updated the quantity of Down Tube from 2 to 4.</span></span> <span data-ttu-id="c2599-124">Если вы вручную повторно выполните срез данных за тот же период, к базе данных Azure SQL или SQL Server будут добавлены две новые записи.</span><span class="sxs-lookup"><span data-stu-id="c2599-124">If you rerun the data slice for that period manually, you’ll find two new records appended to Azure SQL/SQL Server Database.</span></span> <span data-ttu-id="c2599-125">В этом примере предполагается, что ни один из столбцов таблицы не содержит ограничений первичного ключа.</span><span class="sxs-lookup"><span data-stu-id="c2599-125">This example assumes that none of the columns in the table has the primary key constraint.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="c2599-126">Чтобы избежать такого поведения, нужно указать семантику UPSERT, используя один из двух возможных механизмов.</span><span class="sxs-lookup"><span data-stu-id="c2599-126">To avoid this behavior, you need to specify UPSERT semantics by using one of the following two mechanisms:</span></span>

### <a name="mechanism-1-using-sqlwritercleanupscript"></a><span data-ttu-id="c2599-127">Механизм 1: использование sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="c2599-127">Mechanism 1: using sqlWriterCleanupScript</span></span>
<span data-ttu-id="c2599-128">Вы можете добавить свойство **sqlWriterCleanupScript**, чтобы при запуске среза очищать данные из таблицы-приемника перед вставкой данных.</span><span class="sxs-lookup"><span data-stu-id="c2599-128">You can use the **sqlWriterCleanupScript** property to clean up data from the sink table before inserting the data when a slice is run.</span></span> 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

<span data-ttu-id="c2599-129">Когда выполняется срез, сначала скрипт очистки удаляет из таблицы SQL все данные, соответствующие добавляемому фрагменту.</span><span class="sxs-lookup"><span data-stu-id="c2599-129">When a slice runs, the cleanup script is run first to delete data that corresponds to the slice from the SQL table.</span></span> <span data-ttu-id="c2599-130">Затем действие копирования вставляет данные в таблицу SQL.</span><span class="sxs-lookup"><span data-stu-id="c2599-130">The copy activity then inserts data into the SQL Table.</span></span> <span data-ttu-id="c2599-131">Если выполнить такой срез повторно, число будет изменено правильным образом.</span><span class="sxs-lookup"><span data-stu-id="c2599-131">If the slice is rerun, the quantity is updated as desired.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="c2599-132">Предположим, что запись Flat Washer удалена из исходного CSV-файла.</span><span class="sxs-lookup"><span data-stu-id="c2599-132">Suppose the Flat Washer record is removed from the original csv.</span></span> <span data-ttu-id="c2599-133">Тогда повторное выполнение среза даст такой результат:</span><span class="sxs-lookup"><span data-stu-id="c2599-133">Then rerunning the slice would produce the following result:</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="c2599-134">Действие копирования выполнило скрипт очистки, удалив соответствующие данные среза.</span><span class="sxs-lookup"><span data-stu-id="c2599-134">The copy activity ran the cleanup script to delete the corresponding data for that slice.</span></span> <span data-ttu-id="c2599-135">Затем оно получает входные данные из CSV-файла (теперь в нем всего одна запись) и вставляет их в таблицу.</span><span class="sxs-lookup"><span data-stu-id="c2599-135">Then it read the input from the csv (which then contained only one record) and inserted it into the Table.</span></span> 

### <a name="mechanism-2-using-sliceidentifiercolumnname"></a><span data-ttu-id="c2599-136">Механизм 2: использование sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="c2599-136">Mechanism 2: using sliceIdentifierColumnName</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c2599-137">Сейчас sliceIdentifierColumnName не поддерживается для хранилища данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c2599-137">Currently, sliceIdentifierColumnName is not supported for Azure SQL Data Warehouse.</span></span> 

<span data-ttu-id="c2599-138">Другой способ достижения повторяемости — выделение в целевой таблице специального столбца sliceIdentifierColumnName.</span><span class="sxs-lookup"><span data-stu-id="c2599-138">The second mechanism to achieve repeatability is by having a dedicated column (sliceIdentifierColumnName) in the target Table.</span></span> <span data-ttu-id="c2599-139">Этот столбец будет использовать фабрика данных Azure, чтобы синхронизировать источник и назначение.</span><span class="sxs-lookup"><span data-stu-id="c2599-139">This column would be used by Azure Data Factory to ensure the source and destination stay synchronized.</span></span> <span data-ttu-id="c2599-140">Такой подход работает при наличии гибкости в изменении или определении целевой схемы таблицы SQL.</span><span class="sxs-lookup"><span data-stu-id="c2599-140">This approach works when there is flexibility in changing or defining the destination SQL Table schema.</span></span> 

<span data-ttu-id="c2599-141">Фабрика данных Azure будет использовать этот столбец для достижения повторяемости, не изменяя при этом схему таблицы.</span><span class="sxs-lookup"><span data-stu-id="c2599-141">This column is used by Azure Data Factory for repeatability purposes and in the process Azure Data Factory does not make any schema changes to the Table.</span></span> <span data-ttu-id="c2599-142">Способ применения этого подхода:</span><span class="sxs-lookup"><span data-stu-id="c2599-142">Way to use this approach:</span></span>

1. <span data-ttu-id="c2599-143">Определите в целевой таблице SQL столбец двоичного типа (**binary (32)**).</span><span class="sxs-lookup"><span data-stu-id="c2599-143">Define a column of type **binary (32)** in the destination SQL Table.</span></span> <span data-ttu-id="c2599-144">Для этого столбца не должно быть никаких ограничений.</span><span class="sxs-lookup"><span data-stu-id="c2599-144">There should be no constraints on this column.</span></span> <span data-ttu-id="c2599-145">Для нашего примера давайте назовем столбец AdfSliceIdentifier.</span><span class="sxs-lookup"><span data-stu-id="c2599-145">Let's name this column as AdfSliceIdentifier for this example.</span></span>


    <span data-ttu-id="c2599-146">Исходная таблица:</span><span class="sxs-lookup"><span data-stu-id="c2599-146">Source table:</span></span>

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL
    )
    ```

    <span data-ttu-id="c2599-147">Целевая таблица:</span><span class="sxs-lookup"><span data-stu-id="c2599-147">Destination table:</span></span> 

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL,
       [AdfSliceIdentifier] [binary](32) NULL
    )
    ```

2. <span data-ttu-id="c2599-148">Он будет использоваться в действии копирования следующим образом.</span><span class="sxs-lookup"><span data-stu-id="c2599-148">Use it in the copy activity as follows:</span></span>
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "AdfSliceIdentifier"
    }
    ```

<span data-ttu-id="c2599-149">Фабрика данных Azure заполняет этот столбец так, чтобы поддерживать синхронизацию источника и назначения.</span><span class="sxs-lookup"><span data-stu-id="c2599-149">Azure Data Factory populates this column as per its need to ensure the source and destination stay synchronized.</span></span> <span data-ttu-id="c2599-150">Значения этого столбца не следует использовать для других целей.</span><span class="sxs-lookup"><span data-stu-id="c2599-150">The values of this column should not be used outside of this context.</span></span> 

<span data-ttu-id="c2599-151">Как и при использовании первого механизма, действие копирования сначала автоматически удаляет из целевой таблицы SQL данные для заданного среза.</span><span class="sxs-lookup"><span data-stu-id="c2599-151">Similar to mechanism 1, Copy Activity automatically cleans up the data for the given slice from the destination SQL Table.</span></span> <span data-ttu-id="c2599-152">После этого данные из источника вставляются в целевую таблицу.</span><span class="sxs-lookup"><span data-stu-id="c2599-152">It then inserts data from source in to the destination table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c2599-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c2599-153">Next steps</span></span>
<span data-ttu-id="c2599-154">См. следующие статьи о соединителях, где есть полные примеры JSON:</span><span class="sxs-lookup"><span data-stu-id="c2599-154">Review the following connector articles that for complete JSON examples:</span></span> 

- [<span data-ttu-id="c2599-155">База данных SQL Azure;</span><span class="sxs-lookup"><span data-stu-id="c2599-155">Azure SQL Database</span></span>](data-factory-azure-sql-connector.md)
- [<span data-ttu-id="c2599-156">Хранилище данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="c2599-156">Azure SQL Data Warehouse</span></span>](data-factory-azure-sql-data-warehouse-connector.md)
- [<span data-ttu-id="c2599-157">SQL Server</span><span class="sxs-lookup"><span data-stu-id="c2599-157">SQL Server</span></span>](data-factory-sqlserver-connector.md)