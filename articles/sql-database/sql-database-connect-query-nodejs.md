---
title: "Использование Node.js для создания запросов к базе данных SQL Azure | Документация Майкрософт"
description: "В этой статье показано, как использовать Node.js для создания программы, которая подключается к базе данных SQL Azure, и создавать к ней запросы с помощью инструкций Transact-SQL."
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
ms.openlocfilehash: 1907a95df9132c059d7985b6d5cd913536bf3403
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="use-nodejs-to-query-an-azure-sql-database"></a><span data-ttu-id="90c31-103">Использование Node.js для создания запросов к базе данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="90c31-103">Use Node.js to query an Azure SQL database</span></span>

<span data-ttu-id="90c31-104">В этом кратком руководстве показано, как использовать [Node.js](https://nodejs.org/en/) для создания программы, которая подключается к базе данных SQL Azure, а затем с помощью инструкций Transact-SQL выполнить запрос к данным.</span><span class="sxs-lookup"><span data-stu-id="90c31-104">This quick start tutorial demonstrates how to use [Node.js](https://nodejs.org/en/) to create a program to connect to an Azure SQL database and use Transact-SQL statements to query data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="90c31-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="90c31-105">Prerequisites</span></span>

<span data-ttu-id="90c31-106">Ниже указаны требования для работы с этим кратким руководством.</span><span class="sxs-lookup"><span data-stu-id="90c31-106">To complete this quick start tutorial, make sure you have the following:</span></span>

- <span data-ttu-id="90c31-107">База данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="90c31-107">An Azure SQL database.</span></span> <span data-ttu-id="90c31-108">В этом кратком руководстве используются ресурсы, созданные в одном из этих кратких руководств:</span><span class="sxs-lookup"><span data-stu-id="90c31-108">This quick start uses the resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="90c31-109">Создание базы данных с помощью портала</span><span class="sxs-lookup"><span data-stu-id="90c31-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="90c31-110">Создание базы данных SQL Azure и отправка к ней запросов с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="90c31-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="90c31-111">Создание базы данных с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="90c31-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="90c31-112">[Правило брандмауэра на уровне сервера](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) для общедоступного IP-адреса компьютера, на котором выполняются действия из этого краткого руководства.</span><span class="sxs-lookup"><span data-stu-id="90c31-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for the public IP address of the computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="90c31-113">Убедитесь, что установлен Node.js и связанное программное обеспечение для вашей операционной системы.</span><span class="sxs-lookup"><span data-stu-id="90c31-113">You have installed Node.js and related software for your operating system.</span></span>
    - <span data-ttu-id="90c31-114">**Mac OS.** Установите Homebrew и Node.js, а затем драйвер ODBC и SQLCMD.</span><span class="sxs-lookup"><span data-stu-id="90c31-114">**MacOS**: Install Homebrew and Node.js, and then install the ODBC driver and SQLCMD.</span></span> <span data-ttu-id="90c31-115">Ознакомьтесь с шагами 1.2 и 1.3 в [этом руководстве](https://www.microsoft.com/sql-server/developer-get-started/node/mac/).</span><span class="sxs-lookup"><span data-stu-id="90c31-115">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/mac/).</span></span>
    - <span data-ttu-id="90c31-116">**Ubuntu.** Установите Node.js, а затем драйвер ODBC и SQLCMD.</span><span class="sxs-lookup"><span data-stu-id="90c31-116">**Ubuntu**: Install Node.js, and then install the ODBC driver and SQLCMD.</span></span> <span data-ttu-id="90c31-117">Ознакомьтесь с шагами 1.2 и 1.3 в [этом руководстве](https://www.microsoft.com/sql-server/developer-get-started/node/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="90c31-117">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/ubuntu/) .</span></span>
    - <span data-ttu-id="90c31-118">**Windows.** Установите Chocolatey и Node.js, а затем драйвер ODBC и SQLCMD.</span><span class="sxs-lookup"><span data-stu-id="90c31-118">**Windows**: Install Chocolatey and Node.js, and then install the ODBC driver and SQL CMD.</span></span> <span data-ttu-id="90c31-119">Ознакомьтесь с шагами 1.2 и 1.3 в [этом руководстве](https://www.microsoft.com/sql-server/developer-get-started/node/windows/).</span><span class="sxs-lookup"><span data-stu-id="90c31-119">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/windows/).</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="90c31-120">Сведения о подключении SQL Server</span><span class="sxs-lookup"><span data-stu-id="90c31-120">SQL server connection information</span></span>

<span data-ttu-id="90c31-121">Получите сведения о подключении, необходимые для подключения к базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="90c31-121">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="90c31-122">Вам понадобится следующее: полное имя сервера, имя базы данных и сведения для входа.</span><span class="sxs-lookup"><span data-stu-id="90c31-122">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="90c31-123">Войдите на [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="90c31-123">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="90c31-124">В меню слева выберите **Базы данных SQL** и на странице **Базы данных SQL** щелкните имя своей базы данных.</span><span class="sxs-lookup"><span data-stu-id="90c31-124">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="90c31-125">На странице **Обзор** базы данных просмотрите полное имя сервера, как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="90c31-125">On the **Overview** page for your database, review the fully qualified server name as shown in the following image.</span></span> <span data-ttu-id="90c31-126">Вы можете навести указатель мыши на имя сервера, чтобы отобразился пункт **Щелкните, чтобы скопировать**.</span><span class="sxs-lookup"><span data-stu-id="90c31-126">You can hover over the server name to bring up the **Click to copy** option.</span></span> 

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="90c31-128">Если вы забыли данные для входа на сервер базы данных SQL Azure, перейдите к соответствующей странице, чтобы просмотреть имя администратора сервера и при необходимости сбросить пароль.</span><span class="sxs-lookup"><span data-stu-id="90c31-128">If you have forgotten the login information for your Azure SQL Database server, navigate to the SQL Database server page to view the server admin name and, if necessary, reset the password.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="90c31-129">Необходимо настроить правила брандмауэра для общедоступного IP-адреса компьютера, на котором выполняются действия из этого руководства.</span><span class="sxs-lookup"><span data-stu-id="90c31-129">You must have a firewall rule in place for the public IP address of the computer on which you perform this tutorial.</span></span> <span data-ttu-id="90c31-130">Если вы используете другой компьютер или имеете другой общедоступный IP-адрес, создайте [правила брандмауэра на уровне сервера с помощью портала Azure](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="90c31-130">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using the Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 

## <a name="create-a-nodejs-project"></a><span data-ttu-id="90c31-131">Создание проекта Node.js</span><span class="sxs-lookup"><span data-stu-id="90c31-131">Create a Node.js project</span></span>

<span data-ttu-id="90c31-132">Откройте командную строку и создайте папку с именем *sqltest*.</span><span class="sxs-lookup"><span data-stu-id="90c31-132">Open a command prompt and create a folder named *sqltest*.</span></span> <span data-ttu-id="90c31-133">Перейдите к созданной папке и выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="90c31-133">Navigate to the folder you created and run the following command:</span></span>

    
    npm init -y
    npm install tedious
    npm install async
    

## <a name="insert-code-to-query-sql-database"></a><span data-ttu-id="90c31-134">Вставка кода для отправки запроса к базе данных SQL</span><span class="sxs-lookup"><span data-stu-id="90c31-134">Insert code to query SQL database</span></span>

1. <span data-ttu-id="90c31-135">В среде разработки или в предпочитаемом текстовом редакторе создайте файл **sqltest.js**.</span><span class="sxs-lookup"><span data-stu-id="90c31-135">In your development environment or favorite text editor, create a new file, **sqltest.js**.</span></span>

2. <span data-ttu-id="90c31-136">Замените содержимое следующим кодом и добавьте соответствующие значения для сервера, базы данных, пользователя и пароля.</span><span class="sxs-lookup"><span data-stu-id="90c31-136">Replace the contents with the following code and add the appropriate values for your server, database, user, and password.</span></span>

   ```js
   var Connection = require('tedious').Connection;
   var Request = require('tedious').Request;

   // Create connection to database
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

   // Attempt to connect and execute queries if connection goes through
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
      { console.log('Reading rows from the Table...');

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

## <a name="run-the-code"></a><span data-ttu-id="90c31-137">Выполнение кода</span><span class="sxs-lookup"><span data-stu-id="90c31-137">Run the code</span></span>

1. <span data-ttu-id="90c31-138">В командной строке выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="90c31-138">At the command prompt, run the following commands:</span></span>

   ```js
   node sqltest.js
   ```

2. <span data-ttu-id="90c31-139">Убедитесь, что возвращены первые 20 строк, а затем закройте окно приложения.</span><span class="sxs-lookup"><span data-stu-id="90c31-139">Verify that the top 20 rows are returned and then close the application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="90c31-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="90c31-140">Next steps</span></span>

- <span data-ttu-id="90c31-141">Ознакомьтесь со сведениями о [драйвере Microsoft Node.js для SQL Server](https://docs.microsoft.com/sql/connect/node-js/node-js-driver-for-sql-server/).</span><span class="sxs-lookup"><span data-stu-id="90c31-141">Learn about the [Microsoft Node.js Driver for SQL Server](https://docs.microsoft.com/sql/connect/node-js/node-js-driver-for-sql-server/)</span></span>
- <span data-ttu-id="90c31-142">Узнайте, как [подключиться и отправить запрос к базе данных SQL Azure с помощью .NET Core](sql-database-connect-query-dotnet-core.md) в Windows, Linux и Mac OS.</span><span class="sxs-lookup"><span data-stu-id="90c31-142">Learn how to [connect and query an Azure SQL database using .NET core](sql-database-connect-query-dotnet-core.md) on Windows/Linux/macOS.</span></span>  
- <span data-ttu-id="90c31-143">См. дополнительные сведения о [начале работы с .NET Core в Windows, Linux и Mac OS с помощью командной строки](/dotnet/core/tutorials/using-with-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="90c31-143">Learn about [Getting started with .NET Core on Windows/Linux/macOS using the command line](/dotnet/core/tutorials/using-with-xplat-cli).</span></span>
- <span data-ttu-id="90c31-144">Узнайте, как спроектировать первую базу данных SQL с помощью [SSMS](sql-database-design-first-database.md) или [.NET](sql-database-design-first-database-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="90c31-144">Learn how to [Design your first Azure SQL database using SSMS](sql-database-design-first-database.md) or [Design your first Azure SQL database using .NET](sql-database-design-first-database-csharp.md).</span></span>
- <span data-ttu-id="90c31-145">Узнайте, как [подключиться и создавать запросы с помощью SSMS](sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="90c31-145">Learn how to [Connect and query with SSMS](sql-database-connect-query-ssms.md)</span></span>
- <span data-ttu-id="90c31-146">Узнайте, как [подключиться и создавать запросы помощью Visual Studio Code](sql-database-connect-query-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="90c31-146">Learn how to [Connect and query with Visual Studio Code](sql-database-connect-query-vscode.md).</span></span>


