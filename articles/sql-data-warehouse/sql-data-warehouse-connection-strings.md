---
title: "aaaDrivers для хранилища данных SQL | Документы Microsoft"
description: "Строки подключения и драйверы для хранилища данных SQL."
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 5c91f423-b550-4734-8094-c7f2c418ac8d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: a808839a8cfc49c2d7b16038c88ffb39a9f97825
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="drivers-for-azure-sql-data-warehouse"></a><span data-ttu-id="a7a7a-103">Драйверы для хранилища данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="a7a7a-103">Drivers for Azure SQL Data Warehouse</span></span>
<span data-ttu-id="a7a7a-104">Такие как подключения tooSQL хранилища данных с нескольких протоколов другое приложение [ADO.NET][ADO.NET], [ODBC][ODBC], [PHP] [ PHP] и [JDBC][JDBC].</span><span class="sxs-lookup"><span data-stu-id="a7a7a-104">You can connect tooSQL Data Warehouse with several different application protocols such as, [ADO.NET][ADO.NET], [ODBC][ODBC], [PHP][PHP] and [JDBC][JDBC].</span></span> <span data-ttu-id="a7a7a-105">Ниже приведены некоторые примеры строк подключения для каждого протокола.</span><span class="sxs-lookup"><span data-stu-id="a7a7a-105">Below are some examples of connections strings for each protocol.</span></span>  <span data-ttu-id="a7a7a-106">Можно также использовать hello Azure портала toobuild строки подключения.</span><span class="sxs-lookup"><span data-stu-id="a7a7a-106">You can also use hello Azure portal toobuild your connection string.</span></span>  <span data-ttu-id="a7a7a-107">toobuild строку соединения с помощью hello портал Azure перейдите tooyour колонке базы данных, в разделе *Essentials* щелкните *Показать строки подключения базы данных*.</span><span class="sxs-lookup"><span data-stu-id="a7a7a-107">toobuild your connection string using hello Azure portal, navigate tooyour database blade, under *Essentials* click on *Show database connection strings*.</span></span>

## <a name="sample-adonet-connection-string"></a><span data-ttu-id="a7a7a-108">Пример строки подключения по протоколу ADO.NET</span><span class="sxs-lookup"><span data-stu-id="a7a7a-108">Sample ADO.NET connection string</span></span>
```C#
Server=tcp:{your_server}.database.windows.net,1433;Database={your_database};User ID={your_user_name};Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;
```

## <a name="sample-odbc-connection-string"></a><span data-ttu-id="a7a7a-109">Пример строки подключения по протоколу ODBC</span><span class="sxs-lookup"><span data-stu-id="a7a7a-109">Sample ODBC connection string</span></span>
```C#
Driver={SQL Server Native Client 11.0};Server=tcp:{your_server}.database.windows.net,1433;Database={your_database};Uid={your_user_name};Pwd={your_password_here};Encrypt=yes;TrustServerCertificate=no;Connection Timeout=30;
```

## <a name="sample-php-connection-string"></a><span data-ttu-id="a7a7a-110">Пример строки подключения по протоколу PHP</span><span class="sxs-lookup"><span data-stu-id="a7a7a-110">Sample PHP connection string</span></span>
```PHP
Server: {your_server}.database.windows.net,1433 \r\nSQL Database: {your_database}\r\nUser Name: {your_user_name}\r\n\r\nPHP Data Objects(PDO) Sample Code:\r\n\r\ntry {\r\n   $conn = new PDO ( \"sqlsrv:server = tcp:{your_server}.database.windows.net,1433; Database = {your_database}\", \"{your_user_name}\", \"{your_password_here}\");\r\n    $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );\r\n}\r\ncatch ( PDOException $e ) {\r\n   print( \"Error connecting tooSQL Server.\" );\r\n   die(print_r($e));\r\n}\r\n\rSQL Server Extension Sample Code:\r\n\r\n$connectionInfo = array(\"UID\" => \"{your_user_name}\", \"pwd\" => \"{your_password_here}\", \"Database\" => \"{your_database}\", \"LoginTimeout\" => 30, \"Encrypt\" => 1, \"TrustServerCertificate\" => 0);\r\n$serverName = \"tcp:{your_server}.database.windows.net,1433\";\r\n$conn = sqlsrv_connect($serverName, $connectionInfo);
```

## <a name="sample-jdbc-connection-string"></a><span data-ttu-id="a7a7a-111">Пример строки подключения по протоколу JDBC</span><span class="sxs-lookup"><span data-stu-id="a7a7a-111">Sample JDBC connection string</span></span>
```Java
jdbc:sqlserver://yourserver.database.windows.net:1433;database=yourdatabase;user={your_user_name};password={your_password_here};encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;
```

> [!NOTE]
> <span data-ttu-id="a7a7a-112">Рассмотрим параметр hello подключения too300 ожидания в порядке tooallow hello подключения toosurvive небольшие периоды недоступности.</span><span class="sxs-lookup"><span data-stu-id="a7a7a-112">Consider setting hello connection timeout too300 seconds in order tooallow hello connection toosurvive short periods of  unavailability.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="a7a7a-113">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a7a7a-113">Next steps</span></span>
<span data-ttu-id="a7a7a-114">toostart запросов хранилищ данных в Visual Studio и других приложений, в разделе [запроса с помощью Visual Studio][Query with Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="a7a7a-114">toostart querying your data warehouse with Visual Studio and other applications, see [Query with Visual Studio][Query with Visual Studio].</span></span>

<!--Image references-->

<!--Azure.com references-->
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md

<!--MSDN references-->
[ADO.NET]: https://msdn.microsoft.com/library/e80y5yhx(v=vs.110).aspx
[ODBC]: https://msdn.microsoft.com/library/jj730314.aspx
[PHP]: https://msdn.microsoft.com/library/cc296172.aspx?f=255&MSPPError=-2147217396
[JDBC]: https://msdn.microsoft.com/library/mt484311(v=sql.110).aspx

<!--Other references-->
