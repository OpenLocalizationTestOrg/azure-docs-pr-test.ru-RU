---
title: "aaaLoad данных из CSV-файла в базе данных SQL Azure (bcp) | Документы Microsoft"
description: "Для данных небольшого объема использует bcp tooimport данные в базу данных SQL Azure."
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
ms.openlocfilehash: 9350e459aa844223820fbbd849a830cf0354d4e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-csv-into-azure-sql-database-flat-files"></a><span data-ttu-id="9e662-103">Загрузка данных из CSV-файла в базу данных SQL Azure (неструктурированные файлы)</span><span class="sxs-lookup"><span data-stu-id="9e662-103">Load data from CSV into Azure SQL Database (flat files)</span></span>
<span data-ttu-id="9e662-104">Можно использовать программы командной строки tooimport hello bcp данные из CSV-файла в базу данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="9e662-104">You can use hello bcp command-line utility tooimport data from a CSV file into Azure SQL Database.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9e662-105">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="9e662-105">Before you begin</span></span>
### <a name="prerequisites"></a><span data-ttu-id="9e662-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9e662-106">Prerequisites</span></span>
<span data-ttu-id="9e662-107">toocomplete hello шаги в этой статье, необходимо:</span><span class="sxs-lookup"><span data-stu-id="9e662-107">toocomplete hello steps in this article, you need:</span></span>

* <span data-ttu-id="9e662-108">Логический сервер и база данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="9e662-108">An Azure SQL Database logical server and database</span></span>
* <span data-ttu-id="9e662-109">Программа командной строки bcp Hello установлен</span><span class="sxs-lookup"><span data-stu-id="9e662-109">hello bcp command-line utility installed</span></span>
* <span data-ttu-id="9e662-110">Программа командной строки sqlcmd Hello установлен</span><span class="sxs-lookup"><span data-stu-id="9e662-110">hello sqlcmd command-line utility installed</span></span>

<span data-ttu-id="9e662-111">Можно загрузить служебные программы bcp и sqlcmd hello hello [центра загрузки Майкрософт][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="9e662-111">You can download hello bcp and sqlcmd utilities from hello [Microsoft Download Center][Microsoft Download Center].</span></span>

### <a name="data-in-ascii-or-utf-16-format"></a><span data-ttu-id="9e662-112">Данные в формате ASCII или UTF-16</span><span class="sxs-lookup"><span data-stu-id="9e662-112">Data in ASCII or UTF-16 format</span></span>
<span data-ttu-id="9e662-113">Если вы пытаетесь этот учебник с вашими собственными данными, данные требуют toouse hello ASCII или кодировку UTF-16, так как bcp поддерживает UTF-8.</span><span class="sxs-lookup"><span data-stu-id="9e662-113">If you are trying this tutorial with your own data, your data needs toouse hello ASCII or UTF-16 encoding since bcp does not support UTF-8.</span></span> 

## <a name="1-create-a-destination-table"></a><span data-ttu-id="9e662-114">1. Создание целевой таблицы</span><span class="sxs-lookup"><span data-stu-id="9e662-114">1. Create a destination table</span></span>
<span data-ttu-id="9e662-115">Определение таблицы в базе данных SQL как hello целевой таблицы.</span><span class="sxs-lookup"><span data-stu-id="9e662-115">Define a table in SQL Database as hello destination table.</span></span> <span data-ttu-id="9e662-116">Hello столбцов в таблице hello должно соответствовать toohello данных в каждой строке файла данных.</span><span class="sxs-lookup"><span data-stu-id="9e662-116">hello columns in hello table must correspond toohello data in each row of your data file.</span></span>

<span data-ttu-id="9e662-117">toocreate таблицу, откройте командную строку и использовать hello toorun sqlcmd.exe следующую команду:</span><span class="sxs-lookup"><span data-stu-id="9e662-117">toocreate a table, open a command prompt and use sqlcmd.exe toorun hello following command:</span></span>

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


## <a name="2-create-a-source-data-file"></a><span data-ttu-id="9e662-118">2. Создание файла источника данных</span><span class="sxs-lookup"><span data-stu-id="9e662-118">2. Create a source data file</span></span>
<span data-ttu-id="9e662-119">Откройте Блокнот и скопируйте hello следующие строки данных в новый текстовый файл и сохраните этот файл tooyour локальный временный каталог, C:\Temp\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="9e662-119">Open Notepad and copy hello following lines of data into a new text file and then save this file tooyour local temp directory, C:\Temp\DimDate2.txt.</span></span> <span data-ttu-id="9e662-120">Эти данные имеют формат ASCII.</span><span class="sxs-lookup"><span data-stu-id="9e662-120">This data is in ASCII format.</span></span>

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

<span data-ttu-id="9e662-121">(Необязательно) tooexport данные из базы данных SQL Server, откройте командную строку и запустите следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="9e662-121">(Optional) tooexport your own data from a SQL Server database, open a command prompt and run hello following command.</span></span> <span data-ttu-id="9e662-122">Замените значения TableName, ServerName, DatabaseName, Username и Password на собственные.</span><span class="sxs-lookup"><span data-stu-id="9e662-122">Replace TableName, ServerName, DatabaseName, Username, and Password with your own information.</span></span>

```bcp
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t , 
```

## <a name="3-load-hello-data"></a><span data-ttu-id="9e662-123">3. Загрузка данных hello</span><span class="sxs-lookup"><span data-stu-id="9e662-123">3. Load hello data</span></span>
<span data-ttu-id="9e662-124">tooload hello данных, откройте командную строку и запустите hello следующую команду, заменив своих собственных сведений значениями hello имя сервера, имя базы данных, имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="9e662-124">tooload hello data, open a command prompt and run hello following command, replacing hello values for Server Name, Database name, Username, and Password with your own information.</span></span>

```bcp
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ,
```

<span data-ttu-id="9e662-125">Используйте эти данные hello tooverify команда была загружена неправильно</span><span class="sxs-lookup"><span data-stu-id="9e662-125">Use this command tooverify hello data was loaded properly</span></span>

```bcp
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="9e662-126">Hello результаты должны выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9e662-126">hello results should look like this:</span></span>

| <span data-ttu-id="9e662-127">DateId</span><span class="sxs-lookup"><span data-stu-id="9e662-127">DateId</span></span> | <span data-ttu-id="9e662-128">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="9e662-128">CalendarQuarter</span></span> | <span data-ttu-id="9e662-129">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="9e662-129">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9e662-130">20150101</span><span class="sxs-lookup"><span data-stu-id="9e662-130">20150101</span></span> |<span data-ttu-id="9e662-131">1</span><span class="sxs-lookup"><span data-stu-id="9e662-131">1</span></span> |<span data-ttu-id="9e662-132">3</span><span class="sxs-lookup"><span data-stu-id="9e662-132">3</span></span> |
| <span data-ttu-id="9e662-133">20150201</span><span class="sxs-lookup"><span data-stu-id="9e662-133">20150201</span></span> |<span data-ttu-id="9e662-134">1</span><span class="sxs-lookup"><span data-stu-id="9e662-134">1</span></span> |<span data-ttu-id="9e662-135">3</span><span class="sxs-lookup"><span data-stu-id="9e662-135">3</span></span> |
| <span data-ttu-id="9e662-136">20150301</span><span class="sxs-lookup"><span data-stu-id="9e662-136">20150301</span></span> |<span data-ttu-id="9e662-137">1</span><span class="sxs-lookup"><span data-stu-id="9e662-137">1</span></span> |<span data-ttu-id="9e662-138">3</span><span class="sxs-lookup"><span data-stu-id="9e662-138">3</span></span> |
| <span data-ttu-id="9e662-139">20150401</span><span class="sxs-lookup"><span data-stu-id="9e662-139">20150401</span></span> |<span data-ttu-id="9e662-140">2</span><span class="sxs-lookup"><span data-stu-id="9e662-140">2</span></span> |<span data-ttu-id="9e662-141">4</span><span class="sxs-lookup"><span data-stu-id="9e662-141">4</span></span> |
| <span data-ttu-id="9e662-142">20150501</span><span class="sxs-lookup"><span data-stu-id="9e662-142">20150501</span></span> |<span data-ttu-id="9e662-143">2</span><span class="sxs-lookup"><span data-stu-id="9e662-143">2</span></span> |<span data-ttu-id="9e662-144">4</span><span class="sxs-lookup"><span data-stu-id="9e662-144">4</span></span> |
| <span data-ttu-id="9e662-145">20150601</span><span class="sxs-lookup"><span data-stu-id="9e662-145">20150601</span></span> |<span data-ttu-id="9e662-146">2</span><span class="sxs-lookup"><span data-stu-id="9e662-146">2</span></span> |<span data-ttu-id="9e662-147">4</span><span class="sxs-lookup"><span data-stu-id="9e662-147">4</span></span> |
| <span data-ttu-id="9e662-148">20150701</span><span class="sxs-lookup"><span data-stu-id="9e662-148">20150701</span></span> |<span data-ttu-id="9e662-149">3</span><span class="sxs-lookup"><span data-stu-id="9e662-149">3</span></span> |<span data-ttu-id="9e662-150">1</span><span class="sxs-lookup"><span data-stu-id="9e662-150">1</span></span> |
| <span data-ttu-id="9e662-151">20150801</span><span class="sxs-lookup"><span data-stu-id="9e662-151">20150801</span></span> |<span data-ttu-id="9e662-152">3</span><span class="sxs-lookup"><span data-stu-id="9e662-152">3</span></span> |<span data-ttu-id="9e662-153">1</span><span class="sxs-lookup"><span data-stu-id="9e662-153">1</span></span> |
| <span data-ttu-id="9e662-154">20150801</span><span class="sxs-lookup"><span data-stu-id="9e662-154">20150801</span></span> |<span data-ttu-id="9e662-155">3</span><span class="sxs-lookup"><span data-stu-id="9e662-155">3</span></span> |<span data-ttu-id="9e662-156">1</span><span class="sxs-lookup"><span data-stu-id="9e662-156">1</span></span> |
| <span data-ttu-id="9e662-157">20151001</span><span class="sxs-lookup"><span data-stu-id="9e662-157">20151001</span></span> |<span data-ttu-id="9e662-158">4</span><span class="sxs-lookup"><span data-stu-id="9e662-158">4</span></span> |<span data-ttu-id="9e662-159">2</span><span class="sxs-lookup"><span data-stu-id="9e662-159">2</span></span> |
| <span data-ttu-id="9e662-160">20151101</span><span class="sxs-lookup"><span data-stu-id="9e662-160">20151101</span></span> |<span data-ttu-id="9e662-161">4</span><span class="sxs-lookup"><span data-stu-id="9e662-161">4</span></span> |<span data-ttu-id="9e662-162">2</span><span class="sxs-lookup"><span data-stu-id="9e662-162">2</span></span> |
| <span data-ttu-id="9e662-163">20151201</span><span class="sxs-lookup"><span data-stu-id="9e662-163">20151201</span></span> |<span data-ttu-id="9e662-164">4</span><span class="sxs-lookup"><span data-stu-id="9e662-164">4</span></span> |<span data-ttu-id="9e662-165">2</span><span class="sxs-lookup"><span data-stu-id="9e662-165">2</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9e662-166">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9e662-166">Next steps</span></span>
<span data-ttu-id="9e662-167">toomigrate базы данных SQL Server, в разделе [миграции баз данных SQL Server](sql-database-cloud-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="9e662-167">toomigrate a SQL Server database, see [SQL Server database migration](sql-database-cloud-migrate.md).</span></span>

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
