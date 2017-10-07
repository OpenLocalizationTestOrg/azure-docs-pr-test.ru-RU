---
title: "tooquery Node.js aaaUse базы данных SQL Azure | Документы Microsoft"
description: "В этом разделе показано, как toocreate Node.js toouse программу, которая соединяет tooan базы данных SQL Azure и запросов с помощью инструкций Transact-SQL."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 53f70e37-5eb4-400d-972e-dd7ea0caacd4
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 07/05/2017
ms.author: carlrab
ms.openlocfilehash: 3870130a486c218eafeb9cf792a4275de7fd6551
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-nodejs-tooquery-an-azure-sql-database"></a>Использовать Node.js tooquery базы данных Azure SQL

В этом учебнике быстрого запуска показано как toouse [Node.js](https://nodejs.org/en/) toocreate tooan tooconnect программы Azure SQL базы данных и использовать данные tooquery инструкций Transact-SQL.

## <a name="prerequisites"></a>Предварительные требования

toocomplete этом краткое руководство по началу работы, убедитесь, что у вас есть следующие hello:

- База данных SQL Azure. В этом кратком руководстве использует ресурсы hello, созданные в одном из этих краткие руководства: 

   - [Создание базы данных с помощью портала](sql-database-get-started-portal.md)
   - [Создание базы данных SQL Azure и отправка к ней запросов с помощью Azure CLI](sql-database-get-started-cli.md)
   - [Создание базы данных с помощью PowerShell](sql-database-get-started-powershell.md)

- Объект [правила брандмауэра уровня сервера](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) для hello общедоступный IP-адрес компьютера hello, используйте для этого краткого руководства.
- Убедитесь, что установлен Node.js и связанное программное обеспечение для вашей операционной системы.
    - **MacOS**: Установка Homebrew и Node.js, а затем установить драйвер ODBC hello и SQLCMD. Ознакомьтесь с шагами 1.2 и 1.3 в [этом руководстве](https://www.microsoft.com/sql-server/developer-get-started/node/mac/).
    - **Ubuntu**: установите Node.js, а затем установить драйвер ODBC hello и SQLCMD. Ознакомьтесь с шагами 1.2 и 1.3 в [этом руководстве](https://www.microsoft.com/sql-server/developer-get-started/node/ubuntu/).
    - **Windows**: Установка Chocolatey и Node.js, а затем установить драйвер ODBC hello и SQL CMD. Ознакомьтесь с шагами 1.2 и 1.3 в [этом руководстве](https://www.microsoft.com/sql-server/developer-get-started/node/windows/).

## <a name="sql-server-connection-information"></a>Сведения о подключении SQL Server

Получите базу данных Azure SQL toohello tooconnect в сведения, необходимые подключения hello. Необходимо будет hello полное имя сервера, имя базы данных и сведения об имени входа в следующих процедурах hello.

1. Войдите в toohello [портал Azure](https://portal.azure.com/).
2. Выберите **баз данных SQL** hello левом меню и выберите базу данных на hello **баз данных SQL** страницы. 
3. На hello **Обзор** страницу для базы данных, просмотрите hello полное доменное имя сервера, как показано в hello после изображения. Можно навести на toobring имя сервера hello копирование hello **щелкните toocopy** параметр. 

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. Если вы забыли hello учетные данные для сервера базы данных SQL Azure, перейдите toohello базы данных SQL server страницы tooview hello server с именем admin и, при необходимости сбросить пароль hello.

> [!IMPORTANT]
> Необходимо иметь правила брандмауэра на месте для hello общедоступный IP-адрес hello компьютера, на котором выполняется этот учебник. Если вы на другом компьютере или другой общий IP-адрес, создайте [правило брандмауэра уровня сервера с помощью портала Azure "hello"](sql-database-get-started-portal.md#create-a-server-level-firewall-rule). 

## <a name="create-a-nodejs-project"></a>Создание проекта Node.js

Откройте командную строку и создайте папку с именем *sqltest*. Перейдите в папку toohello, создаваемых и запускаемых hello следующую команду:

    
    npm init -y
    npm install tedious
    npm install async
    

## <a name="insert-code-tooquery-sql-database"></a>Вставьте код базы данных SQL tooquery

1. В среде разработки или в предпочитаемом текстовом редакторе создайте файл **sqltest.js**.

2. Замените содержимое hello hello ниже программный код и добавить hello соответствующие значения для сервера, базы данных, пользователя и пароль.

   ```js
   var Connection = require('tedious').Connection;
   var Request = require('tedious').Request;

   // Create connection toodatabase
   var config = 
      {
        userName: 'someuser', // update me
        password: 'somepassword', // update me
        server: 'edmacasqlserver.database.windows.net', // update me
        options: 
           {
              database: 'somedb' //update me
              , encrypt: true
           }
      }
   var connection = new Connection(config);

   // Attempt tooconnect and execute queries if connection goes through
   connection.on('connect', function(err) 
      {
        if (err) 
          {
             console.log(err)
          }
       else
          {
              queryDatabase()
          }
      }
    );

   function queryDatabase()
      { console.log('Reading rows from hello Table...');

          // Read all rows from table
        request = new Request(
             "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName FROM [SalesLT].[ProductCategory] pc JOIN [SalesLT].[Product] p ON pc.productcategoryid = p.productcategoryid",
                function(err, rowCount, rows) 
                   {
                       console.log(rowCount + ' row(s) returned');
                       process.exit();
                   }
               );
    
        request.on('row', function(columns) {
           columns.forEach(function(column) {
               console.log("%s\t%s", column.metadata.colName, column.value);
            });
                });
        connection.execSql(request);
      }
```

## <a name="run-hello-code"></a>Выполнение кода hello

1. Hello командной строки выполните следующие команды hello.

   ```js
   node sqltest.js
   ```

2. Убедитесь, что возвращаются первые 20 строк hello и закройте окно приложения hello.

## <a name="next-steps"></a>Дальнейшие действия

- Дополнительные сведения о hello [драйвер Node.js для SQL Server](https://docs.microsoft.com/sql/connect/node-js/node-js-driver-for-sql-server/)
- Узнайте, каким образом слишком[подключения и запроса к базе данных Azure SQL с помощью .NET core](sql-database-connect-query-dotnet-core.md) на Windows, Linux и macOS.  
- Дополнительные сведения о [начало работы с .NET Core в Windows и Linux/macOS hello командной строки](/dotnet/core/tutorials/using-with-xplat-cli).
- Узнайте, каким образом слишком[проектирование первой базы данных Azure SQL с помощью среды SSMS](sql-database-design-first-database.md) или [проектирование первой базы данных Azure SQL с помощью .NET](sql-database-design-first-database-csharp.md).
- Узнайте, каким образом слишком[подключение и запрос с помощью SSMS](sql-database-connect-query-ssms.md)
- Узнайте, каким образом слишком[подключение и запрос с кодом Visual Studio](sql-database-connect-query-vscode.md).


