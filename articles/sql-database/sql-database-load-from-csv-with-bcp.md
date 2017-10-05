---
title: "Загрузка данных из CSV-файла в базу данных SQL Azure (с использованием bcp) | Документация Майкрософт"
description: "Для импорта небольших объемов данных в базу данных SQL Azure используйте программу bcp."
services: sql-database
documentationcenter: NA
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 875f9b8d-f1a1-4895-b717-f45570fb7f80
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 84bebab7763bb21f73880a6c8b367a62b0c137d3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="load-data-from-csv-into-azure-sql-database-flat-files"></a><span data-ttu-id="d60fa-103">Загрузка данных из CSV-файла в базу данных SQL Azure (неструктурированные файлы)</span><span class="sxs-lookup"><span data-stu-id="d60fa-103">Load data from CSV into Azure SQL Database (flat files)</span></span>
<span data-ttu-id="d60fa-104">Для импорта данных из CSV-файла в базу данных SQL Azure можно использовать программу командной строки bcp.</span><span class="sxs-lookup"><span data-stu-id="d60fa-104">You can use the bcp command-line utility to import data from a CSV file into Azure SQL Database.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d60fa-105">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="d60fa-105">Before you begin</span></span>
### <a name="prerequisites"></a><span data-ttu-id="d60fa-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d60fa-106">Prerequisites</span></span>
<span data-ttu-id="d60fa-107">Для выполнения задач из этой статьи необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="d60fa-107">To complete the steps in this article, you need:</span></span>

* <span data-ttu-id="d60fa-108">Логический сервер и база данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="d60fa-108">An Azure SQL Database logical server and database</span></span>
* <span data-ttu-id="d60fa-109">установленная служебная программа командной строки bcp;</span><span class="sxs-lookup"><span data-stu-id="d60fa-109">The bcp command-line utility installed</span></span>
* <span data-ttu-id="d60fa-110">установленная служебная программа командной строки sqlcmd.</span><span class="sxs-lookup"><span data-stu-id="d60fa-110">The sqlcmd command-line utility installed</span></span>

<span data-ttu-id="d60fa-111">Вы можете скачать служебные программы bcp и sqlcmd в [Центре загрузки Майкрософт][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="d60fa-111">You can download the bcp and sqlcmd utilities from the [Microsoft Download Center][Microsoft Download Center].</span></span>

### <a name="data-in-ascii-or-utf-16-format"></a><span data-ttu-id="d60fa-112">Данные в формате ASCII или UTF-16</span><span class="sxs-lookup"><span data-stu-id="d60fa-112">Data in ASCII or UTF-16 format</span></span>
<span data-ttu-id="d60fa-113">Чтобы выполнить действия, описанные в этом руководстве, необходимо использовать данные в формате ASCII или UTF-16, так как bcp не поддерживает кодировку UTF-8.</span><span class="sxs-lookup"><span data-stu-id="d60fa-113">If you are trying this tutorial with your own data, your data needs to use the ASCII or UTF-16 encoding since bcp does not support UTF-8.</span></span> 

## <a name="1-create-a-destination-table"></a><span data-ttu-id="d60fa-114">1. Создание целевой таблицы</span><span class="sxs-lookup"><span data-stu-id="d60fa-114">1. Create a destination table</span></span>
<span data-ttu-id="d60fa-115">Определите таблицу в базе данных SQL как целевую таблицу.</span><span class="sxs-lookup"><span data-stu-id="d60fa-115">Define a table in SQL Database as the destination table.</span></span> <span data-ttu-id="d60fa-116">Столбцы в таблице должны соответствовать данным в каждой строке файла данных.</span><span class="sxs-lookup"><span data-stu-id="d60fa-116">The columns in the table must correspond to the data in each row of your data file.</span></span>

<span data-ttu-id="d60fa-117">Чтобы создать таблицу, откройте окно командной строки и используйте sqlcmd.exe для выполнения следующей команды:</span><span class="sxs-lookup"><span data-stu-id="d60fa-117">To create a table, open a command prompt and use sqlcmd.exe to run the following command:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    CREATE TABLE DimDate2
    (
        DateId INT NOT NULL,
        CalendarQuarter TINYINT NOT NULL,
        FiscalQuarter TINYINT NOT NULL
    )
    ;
"
```


## <a name="2-create-a-source-data-file"></a><span data-ttu-id="d60fa-118">2) Создание файла источника данных</span><span class="sxs-lookup"><span data-stu-id="d60fa-118">2. Create a source data file</span></span>
<span data-ttu-id="d60fa-119">Откройте блокнот и скопируйте следующие строки данных в новый текстовый файл, а затем сохраните этот файл в локальный временный каталог (C:\Temp\DimDate2.txt).</span><span class="sxs-lookup"><span data-stu-id="d60fa-119">Open Notepad and copy the following lines of data into a new text file and then save this file to your local temp directory, C:\Temp\DimDate2.txt.</span></span> <span data-ttu-id="d60fa-120">Эти данные имеют формат ASCII.</span><span class="sxs-lookup"><span data-stu-id="d60fa-120">This data is in ASCII format.</span></span>

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

<span data-ttu-id="d60fa-121">Чтобы экспортировать данные из базы данных SQL Server, откройте окно командной строки и выполните команду ниже (необязательно).</span><span class="sxs-lookup"><span data-stu-id="d60fa-121">(Optional) To export your own data from a SQL Server database, open a command prompt and run the following command.</span></span> <span data-ttu-id="d60fa-122">Замените значения TableName, ServerName, DatabaseName, Username и Password на собственные.</span><span class="sxs-lookup"><span data-stu-id="d60fa-122">Replace TableName, ServerName, DatabaseName, Username, and Password with your own information.</span></span>

```bcp
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t , 
```

## <a name="3-load-the-data"></a><span data-ttu-id="d60fa-123">3. Загрузка данных</span><span class="sxs-lookup"><span data-stu-id="d60fa-123">3. Load the data</span></span>
<span data-ttu-id="d60fa-124">Чтобы загрузить данные, откройте окно командной строки и выполните следующую команду, подставив собственные значения имени сервера, базы данных, пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="d60fa-124">To load the data, open a command prompt and run the following command, replacing the values for Server Name, Database name, Username, and Password with your own information.</span></span>

```bcp
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ,
```

<span data-ttu-id="d60fa-125">Используйте команду ниже, чтобы убедиться, что данные загружены правильно.</span><span class="sxs-lookup"><span data-stu-id="d60fa-125">Use this command to verify the data was loaded properly</span></span>

```bcp
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="d60fa-126">Результат должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d60fa-126">The results should look like this:</span></span>

| <span data-ttu-id="d60fa-127">DateId</span><span class="sxs-lookup"><span data-stu-id="d60fa-127">DateId</span></span> | <span data-ttu-id="d60fa-128">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="d60fa-128">CalendarQuarter</span></span> | <span data-ttu-id="d60fa-129">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="d60fa-129">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d60fa-130">20150101</span><span class="sxs-lookup"><span data-stu-id="d60fa-130">20150101</span></span> |<span data-ttu-id="d60fa-131">1</span><span class="sxs-lookup"><span data-stu-id="d60fa-131">1</span></span> |<span data-ttu-id="d60fa-132">3</span><span class="sxs-lookup"><span data-stu-id="d60fa-132">3</span></span> |
| <span data-ttu-id="d60fa-133">20150201</span><span class="sxs-lookup"><span data-stu-id="d60fa-133">20150201</span></span> |<span data-ttu-id="d60fa-134">1</span><span class="sxs-lookup"><span data-stu-id="d60fa-134">1</span></span> |<span data-ttu-id="d60fa-135">3</span><span class="sxs-lookup"><span data-stu-id="d60fa-135">3</span></span> |
| <span data-ttu-id="d60fa-136">20150301</span><span class="sxs-lookup"><span data-stu-id="d60fa-136">20150301</span></span> |<span data-ttu-id="d60fa-137">1</span><span class="sxs-lookup"><span data-stu-id="d60fa-137">1</span></span> |<span data-ttu-id="d60fa-138">3</span><span class="sxs-lookup"><span data-stu-id="d60fa-138">3</span></span> |
| <span data-ttu-id="d60fa-139">20150401</span><span class="sxs-lookup"><span data-stu-id="d60fa-139">20150401</span></span> |<span data-ttu-id="d60fa-140">2</span><span class="sxs-lookup"><span data-stu-id="d60fa-140">2</span></span> |<span data-ttu-id="d60fa-141">4</span><span class="sxs-lookup"><span data-stu-id="d60fa-141">4</span></span> |
| <span data-ttu-id="d60fa-142">20150501</span><span class="sxs-lookup"><span data-stu-id="d60fa-142">20150501</span></span> |<span data-ttu-id="d60fa-143">2</span><span class="sxs-lookup"><span data-stu-id="d60fa-143">2</span></span> |<span data-ttu-id="d60fa-144">4</span><span class="sxs-lookup"><span data-stu-id="d60fa-144">4</span></span> |
| <span data-ttu-id="d60fa-145">20150601</span><span class="sxs-lookup"><span data-stu-id="d60fa-145">20150601</span></span> |<span data-ttu-id="d60fa-146">2</span><span class="sxs-lookup"><span data-stu-id="d60fa-146">2</span></span> |<span data-ttu-id="d60fa-147">4</span><span class="sxs-lookup"><span data-stu-id="d60fa-147">4</span></span> |
| <span data-ttu-id="d60fa-148">20150701</span><span class="sxs-lookup"><span data-stu-id="d60fa-148">20150701</span></span> |<span data-ttu-id="d60fa-149">3</span><span class="sxs-lookup"><span data-stu-id="d60fa-149">3</span></span> |<span data-ttu-id="d60fa-150">1</span><span class="sxs-lookup"><span data-stu-id="d60fa-150">1</span></span> |
| <span data-ttu-id="d60fa-151">20150801</span><span class="sxs-lookup"><span data-stu-id="d60fa-151">20150801</span></span> |<span data-ttu-id="d60fa-152">3</span><span class="sxs-lookup"><span data-stu-id="d60fa-152">3</span></span> |<span data-ttu-id="d60fa-153">1</span><span class="sxs-lookup"><span data-stu-id="d60fa-153">1</span></span> |
| <span data-ttu-id="d60fa-154">20150801</span><span class="sxs-lookup"><span data-stu-id="d60fa-154">20150801</span></span> |<span data-ttu-id="d60fa-155">3</span><span class="sxs-lookup"><span data-stu-id="d60fa-155">3</span></span> |<span data-ttu-id="d60fa-156">1</span><span class="sxs-lookup"><span data-stu-id="d60fa-156">1</span></span> |
| <span data-ttu-id="d60fa-157">20151001</span><span class="sxs-lookup"><span data-stu-id="d60fa-157">20151001</span></span> |<span data-ttu-id="d60fa-158">4</span><span class="sxs-lookup"><span data-stu-id="d60fa-158">4</span></span> |<span data-ttu-id="d60fa-159">2</span><span class="sxs-lookup"><span data-stu-id="d60fa-159">2</span></span> |
| <span data-ttu-id="d60fa-160">20151101</span><span class="sxs-lookup"><span data-stu-id="d60fa-160">20151101</span></span> |<span data-ttu-id="d60fa-161">4</span><span class="sxs-lookup"><span data-stu-id="d60fa-161">4</span></span> |<span data-ttu-id="d60fa-162">2</span><span class="sxs-lookup"><span data-stu-id="d60fa-162">2</span></span> |
| <span data-ttu-id="d60fa-163">20151201</span><span class="sxs-lookup"><span data-stu-id="d60fa-163">20151201</span></span> |<span data-ttu-id="d60fa-164">4</span><span class="sxs-lookup"><span data-stu-id="d60fa-164">4</span></span> |<span data-ttu-id="d60fa-165">2</span><span class="sxs-lookup"><span data-stu-id="d60fa-165">2</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d60fa-166">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d60fa-166">Next steps</span></span>
<span data-ttu-id="d60fa-167">Миграция базы данных SQL Server описана в статье [Миграция базы данных SQL Server в базу данных SQL в облаке](sql-database-cloud-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="d60fa-167">To migrate a SQL Server database, see [SQL Server database migration](sql-database-cloud-migrate.md).</span></span>

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
