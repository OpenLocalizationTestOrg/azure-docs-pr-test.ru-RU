---
title: "aaaLoad данные из SQL Server в хранилище данных SQL Azure (PolyBase) | Документы Microsoft"
description: "Использует данные bcp tooexport tooflat файлов и SQL Server, хранилище больших двоичных объектов tooAzure данных tooimport AZCopy, PolyBase tooingest hello данных в хранилище данных SQL Azure."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 4d42786a-fb28-43c9-9c3b-72d19c0ecc11
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 89e2a91bc97642e9fc18545cb802b42d8dc4ad95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-azcopy"></a><span data-ttu-id="147df-103">Загрузка данных из SQL Server в хранилище данных SQL Azure (AZCopy)</span><span class="sxs-lookup"><span data-stu-id="147df-103">Load data from SQL Server into Azure SQL Data Warehouse (AZCopy)</span></span>
<span data-ttu-id="147df-104">Использование bcp и AZCopy служебные программы командной строки tooload данные из хранилища больших двоичных объектов tooAzure SQL Server.</span><span class="sxs-lookup"><span data-stu-id="147df-104">Use bcp and AZCopy command-line utilities tooload data from SQL Server tooAzure blob storage.</span></span> <span data-ttu-id="147df-105">Затем можно используйте данные hello tooload PolyBase или фабрики данных Azure в хранилище данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="147df-105">Then use PolyBase or Azure Data Factory tooload hello data into Azure SQL Data Warehouse.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="147df-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="147df-106">Prerequisites</span></span>
<span data-ttu-id="147df-107">toostep изучения этого руководства требуется:</span><span class="sxs-lookup"><span data-stu-id="147df-107">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="147df-108">База данных хранилища данных SQL</span><span class="sxs-lookup"><span data-stu-id="147df-108">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="147df-109">установить программы командной строки bcp Hello</span><span class="sxs-lookup"><span data-stu-id="147df-109">hello bcp command line utility installed</span></span>
* <span data-ttu-id="147df-110">Hello установлена программа командной строки SQLCMD</span><span class="sxs-lookup"><span data-stu-id="147df-110">hello SQLCMD command line utility installed</span></span>

> [!NOTE]
> <span data-ttu-id="147df-111">Можно загрузить служебные программы bcp и sqlcmd hello hello [центра загрузки Майкрософт][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="147df-111">You can download hello bcp and sqlcmd utilities from hello [Microsoft Download Center][Microsoft Download Center].</span></span>
> 
> 

## <a name="import-data-into-sql-data-warehouse"></a><span data-ttu-id="147df-112">Импорт данных в хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="147df-112">Import data into SQL Data Warehouse</span></span>
<span data-ttu-id="147df-113">В этом учебнике будет создать таблицу в хранилище данных SQL Azure и импортировать данные в таблицу hello.</span><span class="sxs-lookup"><span data-stu-id="147df-113">In this tutorial, you will create a table in Azure SQL Data Warehouse and import data into hello table.</span></span>

### <a name="step-1-create-a-table-in-azure-sql-data-warehouse"></a><span data-ttu-id="147df-114">Шаг 1. Создание таблицы в хранилище данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="147df-114">Step 1: Create a table in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="147df-115">Из командной строки используйте следующие toocreate запроса таблицы в экземпляре hello toorun sqlcmd:</span><span class="sxs-lookup"><span data-stu-id="147df-115">From a command prompt, use sqlcmd toorun hello following query toocreate a table on your instance:</span></span>

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
> <span data-ttu-id="147df-116">В разделе [Общие сведения о таблицах] [ Table Overview] или [синтаксис инструкции CREATE TABLE] [ CREATE TABLE syntax] Дополнительные сведения о создании таблиц в хранилище данных SQL и hello  параметры, доступные в предложении WITH hello.</span><span class="sxs-lookup"><span data-stu-id="147df-116">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse and hello  options available in hello WITH clause.</span></span>
> 
> 

### <a name="step-2-create-a-source-data-file"></a><span data-ttu-id="147df-117">Шаг 2. Создание файла источника данных</span><span class="sxs-lookup"><span data-stu-id="147df-117">Step 2: Create a source data file</span></span>
<span data-ttu-id="147df-118">Откройте Блокнот и скопируйте hello следующие строки данных в новый текстовый файл и сохраните этот файл tooyour локальный временный каталог, C:\Temp\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="147df-118">Open Notepad and copy hello following lines of data into a new text file and then save this file tooyour local temp directory, C:\Temp\DimDate2.txt.</span></span>

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
> <span data-ttu-id="147df-119">Это важные tooremember, bcp.exe не поддерживает кодировку UTF-8 hello файла.</span><span class="sxs-lookup"><span data-stu-id="147df-119">It is important tooremember that bcp.exe does not support hello UTF-8 file encoding.</span></span> <span data-ttu-id="147df-120">Используйте файлы в кодировке ASCII или UTF-16 для файлов при работе со средством bcp.exe.</span><span class="sxs-lookup"><span data-stu-id="147df-120">Please use ASCII files or UTF-16 encoded files when using bcp.exe.</span></span>
> 
> 

### <a name="step-3-connect-and-import-hello-data"></a><span data-ttu-id="147df-121">Шаг 3: Подключение и импортировать данные hello</span><span class="sxs-lookup"><span data-stu-id="147df-121">Step 3: Connect and import hello data</span></span>
<span data-ttu-id="147df-122">Использование программы bcp, можно подключиться и импортировать данные hello, с помощью hello, следующая команда вместо hello соответствующим образом значения:</span><span class="sxs-lookup"><span data-stu-id="147df-122">Using bcp, you can connect and import hello data using hello following command replacing hello values as appropriate:</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="147df-123">Это можно проверить hello загрузки данных, выполнив hello в следующем запросе, с помощью программы sqlcmd.</span><span class="sxs-lookup"><span data-stu-id="147df-123">You can verify hello data was loaded by running hello following query using sqlcmd:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="147df-124">Данный метод должен вернуть hello следующие результаты:</span><span class="sxs-lookup"><span data-stu-id="147df-124">This should return hello following results:</span></span>

| <span data-ttu-id="147df-125">DateId</span><span class="sxs-lookup"><span data-stu-id="147df-125">DateId</span></span> | <span data-ttu-id="147df-126">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="147df-126">CalendarQuarter</span></span> | <span data-ttu-id="147df-127">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="147df-127">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="147df-128">20150101</span><span class="sxs-lookup"><span data-stu-id="147df-128">20150101</span></span> |<span data-ttu-id="147df-129">1</span><span class="sxs-lookup"><span data-stu-id="147df-129">1</span></span> |<span data-ttu-id="147df-130">3</span><span class="sxs-lookup"><span data-stu-id="147df-130">3</span></span> |
| <span data-ttu-id="147df-131">20150201</span><span class="sxs-lookup"><span data-stu-id="147df-131">20150201</span></span> |<span data-ttu-id="147df-132">1</span><span class="sxs-lookup"><span data-stu-id="147df-132">1</span></span> |<span data-ttu-id="147df-133">3</span><span class="sxs-lookup"><span data-stu-id="147df-133">3</span></span> |
| <span data-ttu-id="147df-134">20150301</span><span class="sxs-lookup"><span data-stu-id="147df-134">20150301</span></span> |<span data-ttu-id="147df-135">1</span><span class="sxs-lookup"><span data-stu-id="147df-135">1</span></span> |<span data-ttu-id="147df-136">3</span><span class="sxs-lookup"><span data-stu-id="147df-136">3</span></span> |
| <span data-ttu-id="147df-137">20150401</span><span class="sxs-lookup"><span data-stu-id="147df-137">20150401</span></span> |<span data-ttu-id="147df-138">2</span><span class="sxs-lookup"><span data-stu-id="147df-138">2</span></span> |<span data-ttu-id="147df-139">4</span><span class="sxs-lookup"><span data-stu-id="147df-139">4</span></span> |
| <span data-ttu-id="147df-140">20150501</span><span class="sxs-lookup"><span data-stu-id="147df-140">20150501</span></span> |<span data-ttu-id="147df-141">2</span><span class="sxs-lookup"><span data-stu-id="147df-141">2</span></span> |<span data-ttu-id="147df-142">4</span><span class="sxs-lookup"><span data-stu-id="147df-142">4</span></span> |
| <span data-ttu-id="147df-143">20150601</span><span class="sxs-lookup"><span data-stu-id="147df-143">20150601</span></span> |<span data-ttu-id="147df-144">2</span><span class="sxs-lookup"><span data-stu-id="147df-144">2</span></span> |<span data-ttu-id="147df-145">4</span><span class="sxs-lookup"><span data-stu-id="147df-145">4</span></span> |
| <span data-ttu-id="147df-146">20150701</span><span class="sxs-lookup"><span data-stu-id="147df-146">20150701</span></span> |<span data-ttu-id="147df-147">3</span><span class="sxs-lookup"><span data-stu-id="147df-147">3</span></span> |<span data-ttu-id="147df-148">1</span><span class="sxs-lookup"><span data-stu-id="147df-148">1</span></span> |
| <span data-ttu-id="147df-149">20150801</span><span class="sxs-lookup"><span data-stu-id="147df-149">20150801</span></span> |<span data-ttu-id="147df-150">3</span><span class="sxs-lookup"><span data-stu-id="147df-150">3</span></span> |<span data-ttu-id="147df-151">1</span><span class="sxs-lookup"><span data-stu-id="147df-151">1</span></span> |
| <span data-ttu-id="147df-152">20150801</span><span class="sxs-lookup"><span data-stu-id="147df-152">20150801</span></span> |<span data-ttu-id="147df-153">3</span><span class="sxs-lookup"><span data-stu-id="147df-153">3</span></span> |<span data-ttu-id="147df-154">1</span><span class="sxs-lookup"><span data-stu-id="147df-154">1</span></span> |
| <span data-ttu-id="147df-155">20151001</span><span class="sxs-lookup"><span data-stu-id="147df-155">20151001</span></span> |<span data-ttu-id="147df-156">4</span><span class="sxs-lookup"><span data-stu-id="147df-156">4</span></span> |<span data-ttu-id="147df-157">2</span><span class="sxs-lookup"><span data-stu-id="147df-157">2</span></span> |
| <span data-ttu-id="147df-158">20151101</span><span class="sxs-lookup"><span data-stu-id="147df-158">20151101</span></span> |<span data-ttu-id="147df-159">4</span><span class="sxs-lookup"><span data-stu-id="147df-159">4</span></span> |<span data-ttu-id="147df-160">2</span><span class="sxs-lookup"><span data-stu-id="147df-160">2</span></span> |
| <span data-ttu-id="147df-161">20151201</span><span class="sxs-lookup"><span data-stu-id="147df-161">20151201</span></span> |<span data-ttu-id="147df-162">4</span><span class="sxs-lookup"><span data-stu-id="147df-162">4</span></span> |<span data-ttu-id="147df-163">2</span><span class="sxs-lookup"><span data-stu-id="147df-163">2</span></span> |

### <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="147df-164">Шаг 4. Создание статистики для вновь загруженных данных</span><span class="sxs-lookup"><span data-stu-id="147df-164">Step 4: Create Statistics on your newly loaded data</span></span>
<span data-ttu-id="147df-165">Хранилище данных SQL Azure пока не поддерживает автоматическое создание или автоматическое обновление статистики.</span><span class="sxs-lookup"><span data-stu-id="147df-165">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span> <span data-ttu-id="147df-166">В порядке tooget hello наилучшей производительности запросов очень важно создать статистику для всех столбцов всех таблиц после первой загрузки hello или любые существенные изменения происходят в данных hello.</span><span class="sxs-lookup"><span data-stu-id="147df-166">In order tooget hello best performance from your queries, it's important that statistics be created on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span> <span data-ttu-id="147df-167">Подробное описание статистики см. в разделе hello [статистики] [ Statistics] раздела hello разработка группы разделов.</span><span class="sxs-lookup"><span data-stu-id="147df-167">For a detailed explanation of statistics, see hello [Statistics][Statistics] topic in hello Develop group of topics.</span></span> <span data-ttu-id="147df-168">Ниже приведен краткий пример порядка загрузки toocreate статистики по возвращающая hello в этом примере</span><span class="sxs-lookup"><span data-stu-id="147df-168">Below is a quick example of how toocreate statistics on hello tabled loaded in this example</span></span>

<span data-ttu-id="147df-169">Выполните следующие инструкции CREATE STATISTICS в командной строке sqlcmd hello:</span><span class="sxs-lookup"><span data-stu-id="147df-169">Execute hello following CREATE STATISTICS statements from a sqlcmd prompt:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="export-data-from-sql-data-warehouse"></a><span data-ttu-id="147df-170">Экспорт данных из хранилища данных SQL</span><span class="sxs-lookup"><span data-stu-id="147df-170">Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="147df-171">Работая с этим учебником, вы создадите файл данных из таблицы, находящейся в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="147df-171">In this tutorial, you will create a data file from a table in SQL Data Warehouse.</span></span> <span data-ttu-id="147df-172">Мы экспортируем hello данных, созданной ранее tooa вызывается DimDate2_export.txt новый файл данных.</span><span class="sxs-lookup"><span data-stu-id="147df-172">We will export hello data we created above tooa new data file called DimDate2_export.txt.</span></span>

### <a name="step-1-export-hello-data"></a><span data-ttu-id="147df-173">Шаг 1: Экспорт данных hello</span><span class="sxs-lookup"><span data-stu-id="147df-173">Step 1: Export hello data</span></span>
<span data-ttu-id="147df-174">Программа bcp hello можно подключиться и экспорт данных с помощью hello, следующая команда вместо hello соответствующим образом значения:</span><span class="sxs-lookup"><span data-stu-id="147df-174">Using hello bcp utility, you can connect and export data using hello following command replacing hello values as appropriate:</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="147df-175">Вы можете проверить данные были правильно экспортированы путем открытия нового файла hello приветствия.</span><span class="sxs-lookup"><span data-stu-id="147df-175">You can verify hello data was exported correctly by opening hello new file.</span></span> <span data-ttu-id="147df-176">Hello данные в файл hello должны соответствовать текст hello ниже:</span><span class="sxs-lookup"><span data-stu-id="147df-176">hello data in hello file should match hello text below:</span></span>

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
> <span data-ttu-id="147df-177">Из-за особенностей toohello распределенных систем порядок hello данных может быть таким же hello по базам данных хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="147df-177">Due toohello nature of distributed systems, hello data order may not be hello same across SQL Data Warehouse databases.</span></span> <span data-ttu-id="147df-178">Другой вариант — toouse hello **queryout** функции bcp toowrite запрос извлечения, а не экспортировать hello всей таблицы.</span><span class="sxs-lookup"><span data-stu-id="147df-178">Another option is toouse hello **queryout** function of bcp toowrite a query extract rather than export hello entire table.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="147df-179">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="147df-179">Next steps</span></span>
<span data-ttu-id="147df-180">Общие сведения о загрузке см. в статье [Загрузка данных в хранилище данных SQL][Load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="147df-180">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="147df-181">Дополнительные советы по разработке см. в статье [Проектные решения и методики программирования для хранилища данных SQL][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="147df-181">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

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
