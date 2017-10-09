---
title: "aaaConnect tooAzure хранилище данных SQL | Документы Microsoft"
description: "Строка как имя сервера toofind hello и подключение для вашей tooAzure хранилище данных SQL"
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: e52872ca-ae74-4e25-9c56-d49c85c8d0f0
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: f15e098026afb7c5efbbbfaf62b681e8cd7936bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooazure-sql-data-warehouse"></a>Подключение tooAzure хранилище данных SQL
Эта статья поможет вам получить tooSQL подключенного хранилища данных для hello первый раз.

## <a name="find-your-server-name"></a>Поиск имени сервера
Здравствуйте tooconnecting tooSQL первый шаг, хранилища данных требуется знать, как toofind имя вашего сервера.  Например имя сервера hello в следующий пример hello — sample.database.windows.net. toofind hello полное имя сервера:

1. Go toohello [портал Azure][Azure portal].
2. Щелкните **Базы данных SQL** 
3. Щелкните нужная tooconnect для hello база данных.
4. Найдите hello полное имя сервера.
   
    ![Полное имя сервера][1]

## <a name="supported-drivers-and-connection-strings"></a>Поддерживаемые драйверы и строки подключения
Хранилище данных SQL Azure поддерживает драйверы [ADO.NET][ADO.NET], [ODBC][ODBC], [PHP][PHP] и [JDBC][JDBC]. Выберите одну из hello перед последней версии драйверов toofind hello и документации. tooautomatically создания строки подключения hello hello драйвер, который вы используете из hello Azure портала, можно щелкнуть hello **Показать строки подключения базы данных** из предшествующих пример hello.  Ниже приведены примеры синтаксиса строк подключения для каждого драйвера.

> [!NOTE]
> Рассмотрите возможность установки hello подключения время ожидания too300 секунд tooallow вашей toosurvive подключения короткие периоды недоступности.
> 
> 

### <a name="adonet-connection-string-example"></a>Пример строки подключения ADO.NET
```C#
Server=tcp:{your_server}.database.windows.net,1433;Database={your_database};User ID={your_user_name};Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;
```

### <a name="odbc-connection-string-example"></a>Пример строки подключения ODBC
```C#
Driver={SQL Server Native Client 11.0};Server=tcp:{your_server}.database.windows.net,1433;Database={your_database};Uid={your_user_name};Pwd={your_password_here};Encrypt=yes;TrustServerCertificate=no;Connection Timeout=30;
```

### <a name="php-connection-string-example"></a>Пример строки подключения PHP
```PHP
Server: {your_server}.database.windows.net,1433 \r\nSQL Database: {your_database}\r\nUser Name: {your_user_name}\r\n\r\nPHP Data Objects(PDO) Sample Code:\r\n\r\ntry {\r\n   $conn = new PDO ( \"sqlsrv:server = tcp:{your_server}.database.windows.net,1433; Database = {your_database}\", \"{your_user_name}\", \"{your_password_here}\");\r\n    $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );\r\n}\r\ncatch ( PDOException $e ) {\r\n   print( \"Error connecting tooSQL Server.\" );\r\n   die(print_r($e));\r\n}\r\n\rSQL Server Extension Sample Code:\r\n\r\n$connectionInfo = array(\"UID\" => \"{your_user_name}\", \"pwd\" => \"{your_password_here}\", \"Database\" => \"{your_database}\", \"LoginTimeout\" => 30, \"Encrypt\" => 1, \"TrustServerCertificate\" => 0);\r\n$serverName = \"tcp:{your_server}.database.windows.net,1433\";\r\n$conn = sqlsrv_connect($serverName, $connectionInfo);
```

### <a name="jdbc-connection-string-example"></a>Пример строки подключения JDBC
```Java
jdbc:sqlserver://yourserver.database.windows.net:1433;database=yourdatabase;user={your_user_name};password={your_password_here};encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;
```

## <a name="connection-settings"></a>Параметры подключения
Хранилище данных SQL стандартизирует некоторые параметры при установке подключения и создании объектов. Такие параметры нельзя переопределить. К ним относятся следующие:

| Параметр базы данных | Значение |
|:--- |:--- |
| [ANSI_NULLS][ANSI_NULLS] |ВКЛ |
| [QUOTED_IDENTIFIERS][QUOTED_IDENTIFIERS] |ВКЛ |
| [DATEFORMAT][DATEFORMAT] |мдг |
| [DATEFIRST][DATEFIRST] |7 |

## <a name="next-steps"></a>Дальнейшие действия
tooconnect и запросов с помощью Visual Studio. в разделе [запроса с помощью Visual Studio][Query with Visual Studio]. toolearn Дополнительные сведения о параметры проверки подлинности, в разделе [tooAzure проверки подлинности хранилища данных SQL][Authentication tooAzure SQL Data Warehouse].

<!--Articles-->
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[Authentication tooAzure SQL Data Warehouse]: ./sql-data-warehouse-authentication.md

<!--MSDN references-->
[ADO.NET]: https://msdn.microsoft.com/library/e80y5yhx(v=vs.110).aspx
[ODBC]: https://msdn.microsoft.com/library/jj730314.aspx
[PHP]: https://msdn.microsoft.com/library/cc296172.aspx?f=255&MSPPError=-2147217396
[JDBC]: https://msdn.microsoft.com/library/mt484311(v=sql.110).aspx
[ANSI_NULLS]: https://msdn.microsoft.com/library/ms188048.aspx
[QUOTED_IDENTIFIERS]: https://msdn.microsoft.com/library/ms174393.aspx
[DATEFORMAT]: https://msdn.microsoft.com/library/ms189491.aspx
[DATEFIRST]: https://msdn.microsoft.com/library/ms181598.aspx

<!--Other-->
[Azure portal]: https://portal.azure.com

<!--Image references-->
[1]: media/sql-data-warehouse-connect-overview/get-server-name.png


