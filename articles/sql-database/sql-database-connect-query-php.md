---
title: "tooquery PHP aaaUse базы данных SQL Azure | Документы Microsoft"
description: "В этом разделе показано, как PHP toouse toocreate программу, которая соединяет tooan базы данных SQL Azure и запросов с помощью инструкций Transact-SQL."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 4e71db4a-a 22f-4f1c-83e5-4a34a036ecf3
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: php
ms.topic: hero-article
ms.date: 08/08/2017
ms.author: carlrab
ms.openlocfilehash: 5fc49dcc42ab07cc1bec554be39bdf08dbd6f75e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-php-tooquery-an-azure-sql-database"></a>Использование PHP tooquery базы данных Azure SQL

В этом учебнике быстрого запуска показано как toouse [PHP](http://php.net/manual/en/intro-whatis.php) toocreate tooan tooconnect программы Azure SQL базы данных и использовать данные tooquery инструкций Transact-SQL.

## <a name="prerequisites"></a>Предварительные требования

toocomplete этом краткое руководство по началу работы, убедитесь, что у вас есть следующие hello:

- База данных SQL Azure. В этом кратком руководстве использует ресурсы hello, созданные в одном из этих краткие руководства: 

   - [Создание базы данных с помощью портала](sql-database-get-started-portal.md)
   - [Создание базы данных SQL Azure и отправка к ней запросов с помощью Azure CLI](sql-database-get-started-cli.md)
   - [Создание базы данных с помощью PowerShell](sql-database-get-started-powershell.md)

- Объект [правила брандмауэра уровня сервера](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) для hello общедоступный IP-адрес компьютера hello, используйте для этого краткого руководства.

- Убедитесь, что установлен PHP и связанное программное обеспечение для вашей операционной системы.

    - **MacOS**: установить Homebrew и PHP, установка драйвера ODBC hello и SQLCMD, а затем установите hello драйвера PHP для SQL Server. См. [шаги 1.2, 1.3 и 2.1](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/mac/).
    - **Ubuntu**: установить PHP и другие необходимые пакеты, а затем установить hello драйвера PHP для SQL Server. См. [шаги 1.2 и 2.1](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu/).
    - **Windows**: Установка hello последнюю версию PHP в IIS Express, последние версии драйверов Майкрософт для SQL Server в IIS Express, Chocolatey, драйвер ODBC hello и SQLCMD hello. См. [шаги 1.2 и 1.3](https://www.microsoft.com/sql-server/developer-get-started/php/windows/).    

## <a name="sql-server-connection-information"></a>Сведения о подключении SQL Server

Получите базу данных Azure SQL toohello tooconnect в сведения, необходимые подключения hello. Необходимо будет hello полное имя сервера, имя базы данных и сведения об имени входа в следующих процедурах hello.

1. Войдите в toohello [портал Azure](https://portal.azure.com/).
2. Выберите **баз данных SQL** hello левом меню и выберите базу данных на hello **баз данных SQL** страницы. 
3. На hello **Обзор** страницу для базы данных, просмотрите hello полное доменное имя сервера, как показано в hello после изображения. Можно навести на toobring имя сервера hello копирование hello **щелкните toocopy** параметр.  

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. Если вы забыли учетные данные входа сервера, перейдите toohello базы данных SQL server страницы tooview hello server с именем admin и, при необходимости сбросить пароль hello.     
    
## <a name="insert-code-tooquery-sql-database"></a>Вставьте код базы данных SQL tooquery

1. Создайте файл **sqltest.php** в предпочитаемом текстовом редакторе.  

2. Замените содержимое hello hello ниже программный код и добавить hello соответствующие значения для сервера, базы данных, пользователя и пароль.

   ```PHP
   <?php
   $serverName = "your_server.database.windows.net";
   $connectionOptions = array(
       "Database" => "your_database",
       "Uid" => "your_username",
       "PWD" => "your_password"
   );
   //Establishes hello connection
   $conn = sqlsrv_connect($serverName, $connectionOptions);
   $tsql= "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
           FROM [SalesLT].[ProductCategory] pc
           JOIN [SalesLT].[Product] p
        ON pc.productcategoryid = p.productcategoryid";
   $getResults= sqlsrv_query($conn, $tsql);
   echo ("Reading data from table" . PHP_EOL);
   if ($getResults == FALSE)
       echo (sqlsrv_errors());
   while ($row = sqlsrv_fetch_array($getResults, SQLSRV_FETCH_ASSOC)) {
    echo ($row['CategoryName'] . " " . $row['ProductName'] . PHP_EOL);
   }
   sqlsrv_free_stmt($getResults);
   ?>
   ```

## <a name="run-hello-code"></a>Выполнение кода hello

1. Hello командной строки выполните следующие команды hello.

   ```php
   php sqltest.php
   ```

2. Убедитесь, что возвращаются первые 20 строк hello и закройте окно приложения hello.

## <a name="next-steps"></a>Дальнейшие действия
- [Проектирование первой базы данных SQL Azure](sql-database-design-first-database.md)
- [Microsoft PHP Drivers for SQL Server](https://github.com/Microsoft/msphpsql/) (Драйверы Microsoft PHP для SQL Server)
- [Сообщите о проблемах или задайте вопросы](https://github.com/Microsoft/msphpsql/issues)
