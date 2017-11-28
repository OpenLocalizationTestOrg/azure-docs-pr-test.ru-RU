---
title: "Использование программы bcp для загрузки данных в хранилище данных SQL | Документация Майкрософт"
description: "Узнайте, что такое программа bcp и как ее использовать в различных сценариях работы с хранилищем данных."
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
ms.openlocfilehash: 7596eac10fdf53380d85128265430ce07b551fe3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-with-bcp"></a><span data-ttu-id="33f26-103">Загрузка данных с помощью bcp</span><span class="sxs-lookup"><span data-stu-id="33f26-103">Load data with bcp</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="33f26-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="33f26-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)  
> * [<span data-ttu-id="33f26-105">Фабрика данных</span><span class="sxs-lookup"><span data-stu-id="33f26-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [<span data-ttu-id="33f26-106">PolyBase;</span><span class="sxs-lookup"><span data-stu-id="33f26-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [<span data-ttu-id="33f26-107">BCP</span><span class="sxs-lookup"><span data-stu-id="33f26-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="33f26-108">**[bcp][bcp]** — это программа командной строки для массовой загрузки, которая позволяет копировать данные между SQL Server, файлами данных и хранилищем данных SQL.</span><span class="sxs-lookup"><span data-stu-id="33f26-108">**[bcp][bcp]** is a command-line bulk load utility that allows you to copy data between SQL Server, data files, and SQL Data Warehouse.</span></span> <span data-ttu-id="33f26-109">С помощью программы bcp можно выполнять импорт большого количества строк в таблицы хранилища данных SQL или экспорт данных из таблиц SQL Server в файлы данных.</span><span class="sxs-lookup"><span data-stu-id="33f26-109">Use bcp to import large numbers of rows into SQL Data Warehouse tables or to export data from SQL Server tables into data files.</span></span> <span data-ttu-id="33f26-110">За исключением случаев использования с параметром queryout, для работы с программой bcp не требуется знание языка Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="33f26-110">Except when used with the queryout option, bcp requires no knowledge of Transact-SQL.</span></span>

<span data-ttu-id="33f26-111">Программа bcp — это быстрый и простой способ перемещения небольших наборов данных в базу данных хранилища данных SQL и из нее.</span><span class="sxs-lookup"><span data-stu-id="33f26-111">bcp is a quick and easy way to move smaller data sets into and out of a SQL Data Warehouse database.</span></span> <span data-ttu-id="33f26-112">Точный объем данных, который рекомендуется загружать или извлекать с помощью bcp, зависит от сетевого подключения с центром данных Azure.</span><span class="sxs-lookup"><span data-stu-id="33f26-112">The exact amount of data that is recommended to load/extract via bcp will depend on you network connection to the Azure data center.</span></span>  <span data-ttu-id="33f26-113">Обычно таблицы измерений можно быстро загружать и извлекать с помощью средства bcp, только если речь не идет о больших объемах данных.</span><span class="sxs-lookup"><span data-stu-id="33f26-113">Generally, dimension tables can be loaded and extracted readily with bcp, however, bcp is not recommended for loading or extracting large volumes of data.</span></span>  <span data-ttu-id="33f26-114">Polybase — это рекомендуемое средство для загрузки и извлечения больших объемов данных, так как оно более эффективно использует возможности массово-параллельной архитектуры хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="33f26-114">Polybase is the recommended tool for loading and extracting large volumes of data as it does a better job leveraging the massively parallel processing architecture of SQL Data Warehouse.</span></span>

<span data-ttu-id="33f26-115">С помощью программы bcp можно выполнять следующие действия.</span><span class="sxs-lookup"><span data-stu-id="33f26-115">With bcp you can:</span></span>

* <span data-ttu-id="33f26-116">Использовать простую программу командной строки для загрузки данных в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="33f26-116">Use a simple command-line utility to load data into SQL Data Warehouse.</span></span>
* <span data-ttu-id="33f26-117">Использовать простую программу командной строки для извлечения данных из хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="33f26-117">Use a simple command-line utility to extract data from SQL Data Warehouse.</span></span>

<span data-ttu-id="33f26-118">В этом учебнике показано, как выполнять следующие действия.</span><span class="sxs-lookup"><span data-stu-id="33f26-118">This tutorial will show you how to:</span></span>

* <span data-ttu-id="33f26-119">Импортировать данные в таблицу с помощью команды bcp in.</span><span class="sxs-lookup"><span data-stu-id="33f26-119">Import data into a table using the bcp in command</span></span>
* <span data-ttu-id="33f26-120">Экспортировать данные из таблицы с помощью команды bcp out.</span><span class="sxs-lookup"><span data-stu-id="33f26-120">Export data from a table uisng the bcp out command</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="33f26-121">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="33f26-121">Prerequisites</span></span>
<span data-ttu-id="33f26-122">Для выполнения этих действий необходимо иметь следующее:</span><span class="sxs-lookup"><span data-stu-id="33f26-122">To step through this tutorial, you need:</span></span>

* <span data-ttu-id="33f26-123">База данных хранилища данных SQL</span><span class="sxs-lookup"><span data-stu-id="33f26-123">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="33f26-124">Установленная служебная программа командной строки bcp</span><span class="sxs-lookup"><span data-stu-id="33f26-124">The bcp command line utility installed</span></span>
* <span data-ttu-id="33f26-125">Установленная служебная программа командной строки SQLCMD.</span><span class="sxs-lookup"><span data-stu-id="33f26-125">The SQLCMD command line utility installed</span></span>

> [!NOTE]
> <span data-ttu-id="33f26-126">Вы можете скачать служебные программы bcp и sqlcmd в [Центре загрузки Майкрософт][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="33f26-126">You can download the bcp and sqlcmd utilities from the [Microsoft Download Center][Microsoft Download Center].</span></span>
> 
> 

## <a name="import-data-into-sql-data-warehouse"></a><span data-ttu-id="33f26-127">Импорт данных в хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="33f26-127">Import data into SQL Data Warehouse</span></span>
<span data-ttu-id="33f26-128">Работая с этим учебником, вы создадите таблицу в хранилище данных SQL Azure и импортируете в нее данные.</span><span class="sxs-lookup"><span data-stu-id="33f26-128">In this tutorial, you will create a table in Azure SQL Data Warehouse and import data into the table.</span></span>

### <a name="step-1-create-a-table-in-azure-sql-data-warehouse"></a><span data-ttu-id="33f26-129">Шаг 1. Создание таблицы в хранилище данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="33f26-129">Step 1: Create a table in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="33f26-130">В командной строке выполните следующий запрос, чтобы создать таблицу для экземпляра с помощью sqlcmd:</span><span class="sxs-lookup"><span data-stu-id="33f26-130">From a command prompt, use sqlcmd to run the following query to create a table on your instance:</span></span>

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
> <span data-ttu-id="33f26-131">Дополнительные сведения о создании таблицы в хранилище данных SQL и параметрах, доступных в предложении WITH, см. в статьях, посвященных [таблицам в хранилище данных SQL][Table Overview] и [синтаксису инструкции CREATE TABLE][CREATE TABLE syntax].</span><span class="sxs-lookup"><span data-stu-id="33f26-131">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse and the  options available in the WITH clause.</span></span>
> 
> 

### <a name="step-2-create-a-source-data-file"></a><span data-ttu-id="33f26-132">Шаг 2. Создание файла источника данных</span><span class="sxs-lookup"><span data-stu-id="33f26-132">Step 2: Create a source data file</span></span>
<span data-ttu-id="33f26-133">Откройте блокнот и скопируйте следующие строки данных в новый текстовый файл, а затем сохраните этот файл в локальный временный каталог (C:\Temp\DimDate2.txt).</span><span class="sxs-lookup"><span data-stu-id="33f26-133">Open Notepad and copy the following lines of data into a new text file and then save this file to your local temp directory, C:\Temp\DimDate2.txt.</span></span>

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
> <span data-ttu-id="33f26-134">Важно помнить, что bcp.exe не поддерживает кодировку UTF-8.</span><span class="sxs-lookup"><span data-stu-id="33f26-134">It is important to remember that bcp.exe does not support the UTF-8 file encoding.</span></span> <span data-ttu-id="33f26-135">Используйте файлы в кодировке ASCII или UTF-16 для файлов при работе со средством bcp.exe.</span><span class="sxs-lookup"><span data-stu-id="33f26-135">Please use ASCII files or UTF-16 encoded files when using bcp.exe.</span></span>
> 
> 

### <a name="step-3-connect-and-import-the-data"></a><span data-ttu-id="33f26-136">Шаг 3. Подключение и импорт данных</span><span class="sxs-lookup"><span data-stu-id="33f26-136">Step 3: Connect and import the data</span></span>
<span data-ttu-id="33f26-137">С помощью программы bcp подключитесь и импортируйте данные, для чего замените в следующей команде значения соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="33f26-137">Using bcp, you can connect and import the data using the following command replacing the values as appropriate:</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="33f26-138">Вы можете убедиться, что данные загружены, выполнив следующий запрос с помощью sqlcmd:</span><span class="sxs-lookup"><span data-stu-id="33f26-138">You can verify the data was loaded by running the following query using sqlcmd:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="33f26-139">Вы получите следующие результаты:</span><span class="sxs-lookup"><span data-stu-id="33f26-139">This should return the following results:</span></span>

| <span data-ttu-id="33f26-140">DateId</span><span class="sxs-lookup"><span data-stu-id="33f26-140">DateId</span></span> | <span data-ttu-id="33f26-141">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="33f26-141">CalendarQuarter</span></span> | <span data-ttu-id="33f26-142">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="33f26-142">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="33f26-143">20150101</span><span class="sxs-lookup"><span data-stu-id="33f26-143">20150101</span></span> |<span data-ttu-id="33f26-144">1</span><span class="sxs-lookup"><span data-stu-id="33f26-144">1</span></span> |<span data-ttu-id="33f26-145">3</span><span class="sxs-lookup"><span data-stu-id="33f26-145">3</span></span> |
| <span data-ttu-id="33f26-146">20150201</span><span class="sxs-lookup"><span data-stu-id="33f26-146">20150201</span></span> |<span data-ttu-id="33f26-147">1</span><span class="sxs-lookup"><span data-stu-id="33f26-147">1</span></span> |<span data-ttu-id="33f26-148">3</span><span class="sxs-lookup"><span data-stu-id="33f26-148">3</span></span> |
| <span data-ttu-id="33f26-149">20150301</span><span class="sxs-lookup"><span data-stu-id="33f26-149">20150301</span></span> |<span data-ttu-id="33f26-150">1</span><span class="sxs-lookup"><span data-stu-id="33f26-150">1</span></span> |<span data-ttu-id="33f26-151">3</span><span class="sxs-lookup"><span data-stu-id="33f26-151">3</span></span> |
| <span data-ttu-id="33f26-152">20150401</span><span class="sxs-lookup"><span data-stu-id="33f26-152">20150401</span></span> |<span data-ttu-id="33f26-153">2</span><span class="sxs-lookup"><span data-stu-id="33f26-153">2</span></span> |<span data-ttu-id="33f26-154">4</span><span class="sxs-lookup"><span data-stu-id="33f26-154">4</span></span> |
| <span data-ttu-id="33f26-155">20150501</span><span class="sxs-lookup"><span data-stu-id="33f26-155">20150501</span></span> |<span data-ttu-id="33f26-156">2</span><span class="sxs-lookup"><span data-stu-id="33f26-156">2</span></span> |<span data-ttu-id="33f26-157">4</span><span class="sxs-lookup"><span data-stu-id="33f26-157">4</span></span> |
| <span data-ttu-id="33f26-158">20150601</span><span class="sxs-lookup"><span data-stu-id="33f26-158">20150601</span></span> |<span data-ttu-id="33f26-159">2</span><span class="sxs-lookup"><span data-stu-id="33f26-159">2</span></span> |<span data-ttu-id="33f26-160">4</span><span class="sxs-lookup"><span data-stu-id="33f26-160">4</span></span> |
| <span data-ttu-id="33f26-161">20150701</span><span class="sxs-lookup"><span data-stu-id="33f26-161">20150701</span></span> |<span data-ttu-id="33f26-162">3</span><span class="sxs-lookup"><span data-stu-id="33f26-162">3</span></span> |<span data-ttu-id="33f26-163">1</span><span class="sxs-lookup"><span data-stu-id="33f26-163">1</span></span> |
| <span data-ttu-id="33f26-164">20150801</span><span class="sxs-lookup"><span data-stu-id="33f26-164">20150801</span></span> |<span data-ttu-id="33f26-165">3</span><span class="sxs-lookup"><span data-stu-id="33f26-165">3</span></span> |<span data-ttu-id="33f26-166">1</span><span class="sxs-lookup"><span data-stu-id="33f26-166">1</span></span> |
| <span data-ttu-id="33f26-167">20150801</span><span class="sxs-lookup"><span data-stu-id="33f26-167">20150801</span></span> |<span data-ttu-id="33f26-168">3</span><span class="sxs-lookup"><span data-stu-id="33f26-168">3</span></span> |<span data-ttu-id="33f26-169">1</span><span class="sxs-lookup"><span data-stu-id="33f26-169">1</span></span> |
| <span data-ttu-id="33f26-170">20151001</span><span class="sxs-lookup"><span data-stu-id="33f26-170">20151001</span></span> |<span data-ttu-id="33f26-171">4</span><span class="sxs-lookup"><span data-stu-id="33f26-171">4</span></span> |<span data-ttu-id="33f26-172">2</span><span class="sxs-lookup"><span data-stu-id="33f26-172">2</span></span> |
| <span data-ttu-id="33f26-173">20151101</span><span class="sxs-lookup"><span data-stu-id="33f26-173">20151101</span></span> |<span data-ttu-id="33f26-174">4</span><span class="sxs-lookup"><span data-stu-id="33f26-174">4</span></span> |<span data-ttu-id="33f26-175">2</span><span class="sxs-lookup"><span data-stu-id="33f26-175">2</span></span> |
| <span data-ttu-id="33f26-176">20151201</span><span class="sxs-lookup"><span data-stu-id="33f26-176">20151201</span></span> |<span data-ttu-id="33f26-177">4</span><span class="sxs-lookup"><span data-stu-id="33f26-177">4</span></span> |<span data-ttu-id="33f26-178">2</span><span class="sxs-lookup"><span data-stu-id="33f26-178">2</span></span> |

### <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="33f26-179">Шаг 4. Создание статистики для вновь загруженных данных</span><span class="sxs-lookup"><span data-stu-id="33f26-179">Step 4: Create Statistics on your newly loaded data</span></span>
<span data-ttu-id="33f26-180">Хранилище данных SQL Azure пока не поддерживает автоматическое создание или автоматическое обновление статистики.</span><span class="sxs-lookup"><span data-stu-id="33f26-180">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span> <span data-ttu-id="33f26-181">Чтобы добиться максимально высокой производительности запросов, крайне важно сформировать статистические данные для всех столбцов всех таблиц после первой загрузки или после любых значительных изменений в данных.</span><span class="sxs-lookup"><span data-stu-id="33f26-181">In order to get the best performance from your queries, it's important that statistics be created on all columns of all tables after the first load or any substantial changes occur in the data.</span></span> <span data-ttu-id="33f26-182">Подробные сведения о работе со статистикой см. в статье [Управление статистикой таблиц в хранилище данных SQL][Statistics].</span><span class="sxs-lookup"><span data-stu-id="33f26-182">For a detailed explanation of statistics, see the [Statistics][Statistics] topic in the Develop group of topics.</span></span> <span data-ttu-id="33f26-183">Ниже приведен краткий пример создания статистики по табличным данным, загруженным в этом примере.</span><span class="sxs-lookup"><span data-stu-id="33f26-183">Below is a quick example of how to create statistics on the tabled loaded in this example</span></span>

<span data-ttu-id="33f26-184">Выполните следующие операторы CREATE STATISTICS из командной строки sqlcmd:</span><span class="sxs-lookup"><span data-stu-id="33f26-184">Execute the following CREATE STATISTICS statements from a sqlcmd prompt:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="export-data-from-sql-data-warehouse"></a><span data-ttu-id="33f26-185">Экспорт данных из хранилища данных SQL</span><span class="sxs-lookup"><span data-stu-id="33f26-185">Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="33f26-186">Работая с этим учебником, вы создадите файл данных из таблицы, находящейся в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="33f26-186">In this tutorial, you will create a data file from a table in SQL Data Warehouse.</span></span> <span data-ttu-id="33f26-187">Созданные данные будут экспортированы в новый файл данных DimDate2_export.txt.</span><span class="sxs-lookup"><span data-stu-id="33f26-187">We will export the data we created above to a new data file called DimDate2_export.txt.</span></span>

### <a name="step-1-export-the-data"></a><span data-ttu-id="33f26-188">Шаг 1. Экспорт данных</span><span class="sxs-lookup"><span data-stu-id="33f26-188">Step 1: Export the data</span></span>
<span data-ttu-id="33f26-189">С помощью программы bcp подключитесь и экспортируйте данные, для чего замените в следующей команде значения соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="33f26-189">Using the bcp utility, you can connect and export data using the following command replacing the values as appropriate:</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="33f26-190">Убедитесь, что данные экспортированы, открыв новый файл.</span><span class="sxs-lookup"><span data-stu-id="33f26-190">You can verify the data was exported correctly by opening the new file.</span></span> <span data-ttu-id="33f26-191">Данные в файле должны совпадать с приведенным далее текстом:</span><span class="sxs-lookup"><span data-stu-id="33f26-191">The data in the file should match the text below:</span></span>

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
> <span data-ttu-id="33f26-192">Из-за особенностей распределенных систем порядок данных, взятых из разных баз данных хранилища данных SQL, может не совпадать.</span><span class="sxs-lookup"><span data-stu-id="33f26-192">Due to the nature of distributed systems, the data order may not be the same across SQL Data Warehouse databases.</span></span> <span data-ttu-id="33f26-193">Другой вариант — вместо того, чтобы экспортировать всю таблицу, вы можете использовать в bcp функцию **queryout** , чтобы создать запрос на извлечение.</span><span class="sxs-lookup"><span data-stu-id="33f26-193">Another option is to use the **queryout** function of bcp to write a query extract rather than export the entire table.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="33f26-194">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="33f26-194">Next steps</span></span>
<span data-ttu-id="33f26-195">Общие сведения о загрузке см. в статье [Загрузка данных в хранилище данных SQL][Load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="33f26-195">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="33f26-196">Дополнительные советы по разработке см. в статье [Проектные решения и методики программирования для хранилища данных SQL][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="33f26-196">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

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
