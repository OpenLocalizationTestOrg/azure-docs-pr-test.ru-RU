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
# <a name="load-data-with-bcp"></a><span data-ttu-id="a6aa3-103">Загрузка данных с помощью bcp</span><span class="sxs-lookup"><span data-stu-id="a6aa3-103">Load data with bcp</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a6aa3-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="a6aa3-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)  
> * [<span data-ttu-id="a6aa3-105">Фабрика данных</span><span class="sxs-lookup"><span data-stu-id="a6aa3-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [<span data-ttu-id="a6aa3-106">PolyBase;</span><span class="sxs-lookup"><span data-stu-id="a6aa3-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [<span data-ttu-id="a6aa3-107">BCP</span><span class="sxs-lookup"><span data-stu-id="a6aa3-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="a6aa3-108">**[BCP] [ bcp]**  — это программа командной строки массового нагрузки, которая позволяет вам toocopy данных между SQL Server, файлы данных и хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="a6aa3-108">**[bcp][bcp]** is a command-line bulk load utility that allows you toocopy data between SQL Server, data files, and SQL Data Warehouse.</span></span> <span data-ttu-id="a6aa3-109">Использование bcp tooimport большого количества строк в таблицах хранилища данных SQL или tooexport данные из таблиц SQL Server в файлы данных.</span><span class="sxs-lookup"><span data-stu-id="a6aa3-109">Use bcp tooimport large numbers of rows into SQL Data Warehouse tables or tooexport data from SQL Server tables into data files.</span></span> <span data-ttu-id="a6aa3-110">За исключением случаев использования с параметром queryout hello bcp не требует знания языка Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="a6aa3-110">Except when used with hello queryout option, bcp requires no knowledge of Transact-SQL.</span></span>

<span data-ttu-id="a6aa3-111">Программа bcp является простым и быстрым способом toomove небольшие наборы данных в действие и из базы данных хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="a6aa3-111">bcp is a quick and easy way toomove smaller data sets into and out of a SQL Data Warehouse database.</span></span> <span data-ttu-id="a6aa3-112">будет зависеть от Hello точное количество данных, рекомендуется использовать tooload или извлечение посредством bcp в сети центра обработки данных Azure toohello соединения.</span><span class="sxs-lookup"><span data-stu-id="a6aa3-112">hello exact amount of data that is recommended tooload/extract via bcp will depend on you network connection toohello Azure data center.</span></span>  <span data-ttu-id="a6aa3-113">Обычно таблицы измерений можно быстро загружать и извлекать с помощью средства bcp, только если речь не идет о больших объемах данных.</span><span class="sxs-lookup"><span data-stu-id="a6aa3-113">Generally, dimension tables can be loaded and extracted readily with bcp, however, bcp is not recommended for loading or extracting large volumes of data.</span></span>  <span data-ttu-id="a6aa3-114">Polybase — hello, рекомендуется использовать средство для загрузки и извлечения больших объемов данных, как лучше всего выполняют использование hello архитектура расширенной параллельной обработки хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="a6aa3-114">Polybase is hello recommended tool for loading and extracting large volumes of data as it does a better job leveraging hello massively parallel processing architecture of SQL Data Warehouse.</span></span>

<span data-ttu-id="a6aa3-115">С помощью программы bcp можно выполнять следующие действия.</span><span class="sxs-lookup"><span data-stu-id="a6aa3-115">With bcp you can:</span></span>

* <span data-ttu-id="a6aa3-116">Используйте tooload простая программа командной строки данных в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="a6aa3-116">Use a simple command-line utility tooload data into SQL Data Warehouse.</span></span>
* <span data-ttu-id="a6aa3-117">Используйте tooextract простая программа командной строки данных из хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="a6aa3-117">Use a simple command-line utility tooextract data from SQL Data Warehouse.</span></span>

<span data-ttu-id="a6aa3-118">В этом учебнике показано, как выполнять следующие действия.</span><span class="sxs-lookup"><span data-stu-id="a6aa3-118">This tutorial will show you how to:</span></span>

* <span data-ttu-id="a6aa3-119">Импорт данных в таблицу с использованием команды hello bcp</span><span class="sxs-lookup"><span data-stu-id="a6aa3-119">Import data into a table using hello bcp in command</span></span>
* <span data-ttu-id="a6aa3-120">Экспорт данных из таблицы bcp hello подписку команды</span><span class="sxs-lookup"><span data-stu-id="a6aa3-120">Export data from a table uisng hello bcp out command</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="a6aa3-121">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a6aa3-121">Prerequisites</span></span>
<span data-ttu-id="a6aa3-122">toostep изучения этого руководства требуется:</span><span class="sxs-lookup"><span data-stu-id="a6aa3-122">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="a6aa3-123">База данных хранилища данных SQL</span><span class="sxs-lookup"><span data-stu-id="a6aa3-123">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="a6aa3-124">установить программы командной строки bcp Hello</span><span class="sxs-lookup"><span data-stu-id="a6aa3-124">hello bcp command line utility installed</span></span>
* <span data-ttu-id="a6aa3-125">Hello установлена программа командной строки SQLCMD</span><span class="sxs-lookup"><span data-stu-id="a6aa3-125">hello SQLCMD command line utility installed</span></span>

> [!NOTE]
> <span data-ttu-id="a6aa3-126">Можно загрузить служебные программы bcp и sqlcmd hello hello [центра загрузки Майкрософт][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="a6aa3-126">You can download hello bcp and sqlcmd utilities from hello [Microsoft Download Center][Microsoft Download Center].</span></span>
> 
> 

## <a name="import-data-into-sql-data-warehouse"></a><span data-ttu-id="a6aa3-127">Импорт данных в хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="a6aa3-127">Import data into SQL Data Warehouse</span></span>
<span data-ttu-id="a6aa3-128">В этом учебнике будет создать таблицу в хранилище данных SQL Azure и импортировать данные в таблицу hello.</span><span class="sxs-lookup"><span data-stu-id="a6aa3-128">In this tutorial, you will create a table in Azure SQL Data Warehouse and import data into hello table.</span></span>

### <a name="step-1-create-a-table-in-azure-sql-data-warehouse"></a><span data-ttu-id="a6aa3-129">Шаг 1. Создание таблицы в хранилище данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="a6aa3-129">Step 1: Create a table in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="a6aa3-130">Из командной строки используйте следующие toocreate запроса таблицы в экземпляре hello toorun sqlcmd:</span><span class="sxs-lookup"><span data-stu-id="a6aa3-130">From a command prompt, use sqlcmd toorun hello following query toocreate a table on your instance:</span></span>

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
> <span data-ttu-id="a6aa3-131">В разделе [Общие сведения о таблицах] [ Table Overview] или [синтаксис инструкции CREATE TABLE] [ CREATE TABLE syntax] Дополнительные сведения о создании таблиц в хранилище данных SQL и hello  параметры, доступные в предложении WITH hello.</span><span class="sxs-lookup"><span data-stu-id="a6aa3-131">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse and hello  options available in hello WITH clause.</span></span>
> 
> 

### <a name="step-2-create-a-source-data-file"></a><span data-ttu-id="a6aa3-132">Шаг 2. Создание файла источника данных</span><span class="sxs-lookup"><span data-stu-id="a6aa3-132">Step 2: Create a source data file</span></span>
<span data-ttu-id="a6aa3-133">Откройте Блокнот и скопируйте hello следующие строки данных в новый текстовый файл и сохраните этот файл tooyour локальный временный каталог, C:\Temp\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="a6aa3-133">Open Notepad and copy hello following lines of data into a new text file and then save this file tooyour local temp directory, C:\Temp\DimDate2.txt.</span></span>

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
> <span data-ttu-id="a6aa3-134">Это важные tooremember, bcp.exe не поддерживает кодировку UTF-8 hello файла.</span><span class="sxs-lookup"><span data-stu-id="a6aa3-134">It is important tooremember that bcp.exe does not support hello UTF-8 file encoding.</span></span> <span data-ttu-id="a6aa3-135">Используйте файлы в кодировке ASCII или UTF-16 для файлов при работе со средством bcp.exe.</span><span class="sxs-lookup"><span data-stu-id="a6aa3-135">Please use ASCII files or UTF-16 encoded files when using bcp.exe.</span></span>
> 
> 

### <a name="step-3-connect-and-import-hello-data"></a><span data-ttu-id="a6aa3-136">Шаг 3: Подключение и импортировать данные hello</span><span class="sxs-lookup"><span data-stu-id="a6aa3-136">Step 3: Connect and import hello data</span></span>
<span data-ttu-id="a6aa3-137">Использование программы bcp, можно подключиться и импортировать данные hello, с помощью hello, следующая команда вместо hello соответствующим образом значения:</span><span class="sxs-lookup"><span data-stu-id="a6aa3-137">Using bcp, you can connect and import hello data using hello following command replacing hello values as appropriate:</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="a6aa3-138">Это можно проверить hello загрузки данных, выполнив hello в следующем запросе, с помощью программы sqlcmd.</span><span class="sxs-lookup"><span data-stu-id="a6aa3-138">You can verify hello data was loaded by running hello following query using sqlcmd:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="a6aa3-139">Данный метод должен вернуть hello следующие результаты:</span><span class="sxs-lookup"><span data-stu-id="a6aa3-139">This should return hello following results:</span></span>

| <span data-ttu-id="a6aa3-140">DateId</span><span class="sxs-lookup"><span data-stu-id="a6aa3-140">DateId</span></span> | <span data-ttu-id="a6aa3-141">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="a6aa3-141">CalendarQuarter</span></span> | <span data-ttu-id="a6aa3-142">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="a6aa3-142">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a6aa3-143">20150101</span><span class="sxs-lookup"><span data-stu-id="a6aa3-143">20150101</span></span> |<span data-ttu-id="a6aa3-144">1</span><span class="sxs-lookup"><span data-stu-id="a6aa3-144">1</span></span> |<span data-ttu-id="a6aa3-145">3</span><span class="sxs-lookup"><span data-stu-id="a6aa3-145">3</span></span> |
| <span data-ttu-id="a6aa3-146">20150201</span><span class="sxs-lookup"><span data-stu-id="a6aa3-146">20150201</span></span> |<span data-ttu-id="a6aa3-147">1</span><span class="sxs-lookup"><span data-stu-id="a6aa3-147">1</span></span> |<span data-ttu-id="a6aa3-148">3</span><span class="sxs-lookup"><span data-stu-id="a6aa3-148">3</span></span> |
| <span data-ttu-id="a6aa3-149">20150301</span><span class="sxs-lookup"><span data-stu-id="a6aa3-149">20150301</span></span> |<span data-ttu-id="a6aa3-150">1</span><span class="sxs-lookup"><span data-stu-id="a6aa3-150">1</span></span> |<span data-ttu-id="a6aa3-151">3</span><span class="sxs-lookup"><span data-stu-id="a6aa3-151">3</span></span> |
| <span data-ttu-id="a6aa3-152">20150401</span><span class="sxs-lookup"><span data-stu-id="a6aa3-152">20150401</span></span> |<span data-ttu-id="a6aa3-153">2</span><span class="sxs-lookup"><span data-stu-id="a6aa3-153">2</span></span> |<span data-ttu-id="a6aa3-154">4</span><span class="sxs-lookup"><span data-stu-id="a6aa3-154">4</span></span> |
| <span data-ttu-id="a6aa3-155">20150501</span><span class="sxs-lookup"><span data-stu-id="a6aa3-155">20150501</span></span> |<span data-ttu-id="a6aa3-156">2</span><span class="sxs-lookup"><span data-stu-id="a6aa3-156">2</span></span> |<span data-ttu-id="a6aa3-157">4</span><span class="sxs-lookup"><span data-stu-id="a6aa3-157">4</span></span> |
| <span data-ttu-id="a6aa3-158">20150601</span><span class="sxs-lookup"><span data-stu-id="a6aa3-158">20150601</span></span> |<span data-ttu-id="a6aa3-159">2</span><span class="sxs-lookup"><span data-stu-id="a6aa3-159">2</span></span> |<span data-ttu-id="a6aa3-160">4</span><span class="sxs-lookup"><span data-stu-id="a6aa3-160">4</span></span> |
| <span data-ttu-id="a6aa3-161">20150701</span><span class="sxs-lookup"><span data-stu-id="a6aa3-161">20150701</span></span> |<span data-ttu-id="a6aa3-162">3</span><span class="sxs-lookup"><span data-stu-id="a6aa3-162">3</span></span> |<span data-ttu-id="a6aa3-163">1</span><span class="sxs-lookup"><span data-stu-id="a6aa3-163">1</span></span> |
| <span data-ttu-id="a6aa3-164">20150801</span><span class="sxs-lookup"><span data-stu-id="a6aa3-164">20150801</span></span> |<span data-ttu-id="a6aa3-165">3</span><span class="sxs-lookup"><span data-stu-id="a6aa3-165">3</span></span> |<span data-ttu-id="a6aa3-166">1</span><span class="sxs-lookup"><span data-stu-id="a6aa3-166">1</span></span> |
| <span data-ttu-id="a6aa3-167">20150801</span><span class="sxs-lookup"><span data-stu-id="a6aa3-167">20150801</span></span> |<span data-ttu-id="a6aa3-168">3</span><span class="sxs-lookup"><span data-stu-id="a6aa3-168">3</span></span> |<span data-ttu-id="a6aa3-169">1</span><span class="sxs-lookup"><span data-stu-id="a6aa3-169">1</span></span> |
| <span data-ttu-id="a6aa3-170">20151001</span><span class="sxs-lookup"><span data-stu-id="a6aa3-170">20151001</span></span> |<span data-ttu-id="a6aa3-171">4</span><span class="sxs-lookup"><span data-stu-id="a6aa3-171">4</span></span> |<span data-ttu-id="a6aa3-172">2</span><span class="sxs-lookup"><span data-stu-id="a6aa3-172">2</span></span> |
| <span data-ttu-id="a6aa3-173">20151101</span><span class="sxs-lookup"><span data-stu-id="a6aa3-173">20151101</span></span> |<span data-ttu-id="a6aa3-174">4</span><span class="sxs-lookup"><span data-stu-id="a6aa3-174">4</span></span> |<span data-ttu-id="a6aa3-175">2</span><span class="sxs-lookup"><span data-stu-id="a6aa3-175">2</span></span> |
| <span data-ttu-id="a6aa3-176">20151201</span><span class="sxs-lookup"><span data-stu-id="a6aa3-176">20151201</span></span> |<span data-ttu-id="a6aa3-177">4</span><span class="sxs-lookup"><span data-stu-id="a6aa3-177">4</span></span> |<span data-ttu-id="a6aa3-178">2</span><span class="sxs-lookup"><span data-stu-id="a6aa3-178">2</span></span> |

### <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="a6aa3-179">Шаг 4. Создание статистики для вновь загруженных данных</span><span class="sxs-lookup"><span data-stu-id="a6aa3-179">Step 4: Create Statistics on your newly loaded data</span></span>
<span data-ttu-id="a6aa3-180">Хранилище данных SQL Azure пока не поддерживает автоматическое создание или автоматическое обновление статистики.</span><span class="sxs-lookup"><span data-stu-id="a6aa3-180">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span> <span data-ttu-id="a6aa3-181">В порядке tooget hello наилучшей производительности запросов очень важно создать статистику для всех столбцов всех таблиц после первой загрузки hello или любые существенные изменения происходят в данных hello.</span><span class="sxs-lookup"><span data-stu-id="a6aa3-181">In order tooget hello best performance from your queries, it's important that statistics be created on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span> <span data-ttu-id="a6aa3-182">Подробное описание статистики см. в разделе hello [статистики] [ Statistics] раздела hello разработка группы разделов.</span><span class="sxs-lookup"><span data-stu-id="a6aa3-182">For a detailed explanation of statistics, see hello [Statistics][Statistics] topic in hello Develop group of topics.</span></span> <span data-ttu-id="a6aa3-183">Ниже приведен краткий пример порядка загрузки toocreate статистики по возвращающая hello в этом примере</span><span class="sxs-lookup"><span data-stu-id="a6aa3-183">Below is a quick example of how toocreate statistics on hello tabled loaded in this example</span></span>

<span data-ttu-id="a6aa3-184">Выполните следующие инструкции CREATE STATISTICS в командной строке sqlcmd hello:</span><span class="sxs-lookup"><span data-stu-id="a6aa3-184">Execute hello following CREATE STATISTICS statements from a sqlcmd prompt:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="export-data-from-sql-data-warehouse"></a><span data-ttu-id="a6aa3-185">Экспорт данных из хранилища данных SQL</span><span class="sxs-lookup"><span data-stu-id="a6aa3-185">Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="a6aa3-186">Работая с этим учебником, вы создадите файл данных из таблицы, находящейся в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="a6aa3-186">In this tutorial, you will create a data file from a table in SQL Data Warehouse.</span></span> <span data-ttu-id="a6aa3-187">Мы экспортируем hello данных, созданной ранее tooa вызывается DimDate2_export.txt новый файл данных.</span><span class="sxs-lookup"><span data-stu-id="a6aa3-187">We will export hello data we created above tooa new data file called DimDate2_export.txt.</span></span>

### <a name="step-1-export-hello-data"></a><span data-ttu-id="a6aa3-188">Шаг 1: Экспорт данных hello</span><span class="sxs-lookup"><span data-stu-id="a6aa3-188">Step 1: Export hello data</span></span>
<span data-ttu-id="a6aa3-189">Программа bcp hello можно подключиться и экспорт данных с помощью hello, следующая команда вместо hello соответствующим образом значения:</span><span class="sxs-lookup"><span data-stu-id="a6aa3-189">Using hello bcp utility, you can connect and export data using hello following command replacing hello values as appropriate:</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="a6aa3-190">Вы можете проверить данные были правильно экспортированы путем открытия нового файла hello приветствия.</span><span class="sxs-lookup"><span data-stu-id="a6aa3-190">You can verify hello data was exported correctly by opening hello new file.</span></span> <span data-ttu-id="a6aa3-191">Hello данные в файл hello должны соответствовать текст hello ниже:</span><span class="sxs-lookup"><span data-stu-id="a6aa3-191">hello data in hello file should match hello text below:</span></span>

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
> <span data-ttu-id="a6aa3-192">Из-за особенностей toohello распределенных систем порядок hello данных может быть таким же hello по базам данных хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="a6aa3-192">Due toohello nature of distributed systems, hello data order may not be hello same across SQL Data Warehouse databases.</span></span> <span data-ttu-id="a6aa3-193">Другой вариант — toouse hello **queryout** функции bcp toowrite запрос извлечения, а не экспортировать hello всей таблицы.</span><span class="sxs-lookup"><span data-stu-id="a6aa3-193">Another option is toouse hello **queryout** function of bcp toowrite a query extract rather than export hello entire table.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="a6aa3-194">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a6aa3-194">Next steps</span></span>
<span data-ttu-id="a6aa3-195">Общие сведения о загрузке см. в статье [Загрузка данных в хранилище данных SQL][Load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="a6aa3-195">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="a6aa3-196">Дополнительные советы по разработке см. в статье [Проектные решения и методики программирования для хранилища данных SQL][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="a6aa3-196">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

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
