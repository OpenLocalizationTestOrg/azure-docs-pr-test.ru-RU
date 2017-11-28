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
# <a name="use-nodejs-tooquery-an-azure-sql-database"></a><span data-ttu-id="304d3-103">Использовать Node.js tooquery базы данных Azure SQL</span><span class="sxs-lookup"><span data-stu-id="304d3-103">Use Node.js tooquery an Azure SQL database</span></span>

<span data-ttu-id="304d3-104">В этом учебнике быстрого запуска показано как toouse [Node.js](https://nodejs.org/en/) toocreate tooan tooconnect программы Azure SQL базы данных и использовать данные tooquery инструкций Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="304d3-104">This quick start tutorial demonstrates how toouse [Node.js](https://nodejs.org/en/) toocreate a program tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="304d3-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="304d3-105">Prerequisites</span></span>

<span data-ttu-id="304d3-106">toocomplete этом краткое руководство по началу работы, убедитесь, что у вас есть следующие hello:</span><span class="sxs-lookup"><span data-stu-id="304d3-106">toocomplete this quick start tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="304d3-107">База данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="304d3-107">An Azure SQL database.</span></span> <span data-ttu-id="304d3-108">В этом кратком руководстве использует ресурсы hello, созданные в одном из этих краткие руководства:</span><span class="sxs-lookup"><span data-stu-id="304d3-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="304d3-109">Создание базы данных с помощью портала</span><span class="sxs-lookup"><span data-stu-id="304d3-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="304d3-110">Создание базы данных SQL Azure и отправка к ней запросов с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="304d3-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="304d3-111">Создание базы данных с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="304d3-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="304d3-112">Объект [правила брандмауэра уровня сервера](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) для hello общедоступный IP-адрес компьютера hello, используйте для этого краткого руководства.</span><span class="sxs-lookup"><span data-stu-id="304d3-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="304d3-113">Убедитесь, что установлен Node.js и связанное программное обеспечение для вашей операционной системы.</span><span class="sxs-lookup"><span data-stu-id="304d3-113">You have installed Node.js and related software for your operating system.</span></span>
    - <span data-ttu-id="304d3-114">**MacOS**: Установка Homebrew и Node.js, а затем установить драйвер ODBC hello и SQLCMD.</span><span class="sxs-lookup"><span data-stu-id="304d3-114">**MacOS**: Install Homebrew and Node.js, and then install hello ODBC driver and SQLCMD.</span></span> <span data-ttu-id="304d3-115">Ознакомьтесь с шагами 1.2 и 1.3 в [этом руководстве](https://www.microsoft.com/sql-server/developer-get-started/node/mac/).</span><span class="sxs-lookup"><span data-stu-id="304d3-115">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/mac/).</span></span>
    - <span data-ttu-id="304d3-116">**Ubuntu**: установите Node.js, а затем установить драйвер ODBC hello и SQLCMD.</span><span class="sxs-lookup"><span data-stu-id="304d3-116">**Ubuntu**: Install Node.js, and then install hello ODBC driver and SQLCMD.</span></span> <span data-ttu-id="304d3-117">Ознакомьтесь с шагами 1.2 и 1.3 в [этом руководстве](https://www.microsoft.com/sql-server/developer-get-started/node/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="304d3-117">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/ubuntu/) .</span></span>
    - <span data-ttu-id="304d3-118">**Windows**: Установка Chocolatey и Node.js, а затем установить драйвер ODBC hello и SQL CMD.</span><span class="sxs-lookup"><span data-stu-id="304d3-118">**Windows**: Install Chocolatey and Node.js, and then install hello ODBC driver and SQL CMD.</span></span> <span data-ttu-id="304d3-119">Ознакомьтесь с шагами 1.2 и 1.3 в [этом руководстве](https://www.microsoft.com/sql-server/developer-get-started/node/windows/).</span><span class="sxs-lookup"><span data-stu-id="304d3-119">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/windows/).</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="304d3-120">Сведения о подключении SQL Server</span><span class="sxs-lookup"><span data-stu-id="304d3-120">SQL server connection information</span></span>

<span data-ttu-id="304d3-121">Получите базу данных Azure SQL toohello tooconnect в сведения, необходимые подключения hello.</span><span class="sxs-lookup"><span data-stu-id="304d3-121">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="304d3-122">Необходимо будет hello полное имя сервера, имя базы данных и сведения об имени входа в следующих процедурах hello.</span><span class="sxs-lookup"><span data-stu-id="304d3-122">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="304d3-123">Войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="304d3-123">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="304d3-124">Выберите **баз данных SQL** hello левом меню и выберите базу данных на hello **баз данных SQL** страницы.</span><span class="sxs-lookup"><span data-stu-id="304d3-124">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="304d3-125">На hello **Обзор** страницу для базы данных, просмотрите hello полное доменное имя сервера, как показано в hello после изображения.</span><span class="sxs-lookup"><span data-stu-id="304d3-125">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="304d3-126">Можно навести на toobring имя сервера hello копирование hello **щелкните toocopy** параметр.</span><span class="sxs-lookup"><span data-stu-id="304d3-126">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span> 

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="304d3-128">Если вы забыли hello учетные данные для сервера базы данных SQL Azure, перейдите toohello базы данных SQL server страницы tooview hello server с именем admin и, при необходимости сбросить пароль hello.</span><span class="sxs-lookup"><span data-stu-id="304d3-128">If you have forgotten hello login information for your Azure SQL Database server, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="304d3-129">Необходимо иметь правила брандмауэра на месте для hello общедоступный IP-адрес hello компьютера, на котором выполняется этот учебник.</span><span class="sxs-lookup"><span data-stu-id="304d3-129">You must have a firewall rule in place for hello public IP address of hello computer on which you perform this tutorial.</span></span> <span data-ttu-id="304d3-130">Если вы на другом компьютере или другой общий IP-адрес, создайте [правило брандмауэра уровня сервера с помощью портала Azure "hello"](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="304d3-130">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using hello Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 

## <a name="create-a-nodejs-project"></a><span data-ttu-id="304d3-131">Создание проекта Node.js</span><span class="sxs-lookup"><span data-stu-id="304d3-131">Create a Node.js project</span></span>

<span data-ttu-id="304d3-132">Откройте командную строку и создайте папку с именем *sqltest*.</span><span class="sxs-lookup"><span data-stu-id="304d3-132">Open a command prompt and create a folder named *sqltest*.</span></span> <span data-ttu-id="304d3-133">Перейдите в папку toohello, создаваемых и запускаемых hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="304d3-133">Navigate toohello folder you created and run hello following command:</span></span>

    
    npm init -y
    npm install tedious
    npm install async
    

## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="304d3-134">Вставьте код базы данных SQL tooquery</span><span class="sxs-lookup"><span data-stu-id="304d3-134">Insert code tooquery SQL database</span></span>

1. <span data-ttu-id="304d3-135">В среде разработки или в предпочитаемом текстовом редакторе создайте файл **sqltest.js**.</span><span class="sxs-lookup"><span data-stu-id="304d3-135">In your development environment or favorite text editor, create a new file, **sqltest.js**.</span></span>

2. <span data-ttu-id="304d3-136">Замените содержимое hello hello ниже программный код и добавить hello соответствующие значения для сервера, базы данных, пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="304d3-136">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

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

## <a name="run-hello-code"></a><span data-ttu-id="304d3-137">Выполнение кода hello</span><span class="sxs-lookup"><span data-stu-id="304d3-137">Run hello code</span></span>

1. <span data-ttu-id="304d3-138">Hello командной строки выполните следующие команды hello.</span><span class="sxs-lookup"><span data-stu-id="304d3-138">At hello command prompt, run hello following commands:</span></span>

   ```js
   node sqltest.js
   ```

2. <span data-ttu-id="304d3-139">Убедитесь, что возвращаются первые 20 строк hello и закройте окно приложения hello.</span><span class="sxs-lookup"><span data-stu-id="304d3-139">Verify that hello top 20 rows are returned and then close hello application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="304d3-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="304d3-140">Next steps</span></span>

- <span data-ttu-id="304d3-141">Дополнительные сведения о hello [драйвер Node.js для SQL Server](https://docs.microsoft.com/sql/connect/node-js/node-js-driver-for-sql-server/)</span><span class="sxs-lookup"><span data-stu-id="304d3-141">Learn about hello [Microsoft Node.js Driver for SQL Server](https://docs.microsoft.com/sql/connect/node-js/node-js-driver-for-sql-server/)</span></span>
- <span data-ttu-id="304d3-142">Узнайте, каким образом слишком[подключения и запроса к базе данных Azure SQL с помощью .NET core](sql-database-connect-query-dotnet-core.md) на Windows, Linux и macOS.</span><span class="sxs-lookup"><span data-stu-id="304d3-142">Learn how too[connect and query an Azure SQL database using .NET core](sql-database-connect-query-dotnet-core.md) on Windows/Linux/macOS.</span></span>  
- <span data-ttu-id="304d3-143">Дополнительные сведения о [начало работы с .NET Core в Windows и Linux/macOS hello командной строки](/dotnet/core/tutorials/using-with-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="304d3-143">Learn about [Getting started with .NET Core on Windows/Linux/macOS using hello command line](/dotnet/core/tutorials/using-with-xplat-cli).</span></span>
- <span data-ttu-id="304d3-144">Узнайте, каким образом слишком[проектирование первой базы данных Azure SQL с помощью среды SSMS](sql-database-design-first-database.md) или [проектирование первой базы данных Azure SQL с помощью .NET](sql-database-design-first-database-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="304d3-144">Learn how too[Design your first Azure SQL database using SSMS](sql-database-design-first-database.md) or [Design your first Azure SQL database using .NET](sql-database-design-first-database-csharp.md).</span></span>
- <span data-ttu-id="304d3-145">Узнайте, каким образом слишком[подключение и запрос с помощью SSMS](sql-database-connect-query-ssms.md)</span><span class="sxs-lookup"><span data-stu-id="304d3-145">Learn how too[Connect and query with SSMS](sql-database-connect-query-ssms.md)</span></span>
- <span data-ttu-id="304d3-146">Узнайте, каким образом слишком[подключение и запрос с кодом Visual Studio](sql-database-connect-query-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="304d3-146">Learn how too[Connect and query with Visual Studio Code](sql-database-connect-query-vscode.md).</span></span>


