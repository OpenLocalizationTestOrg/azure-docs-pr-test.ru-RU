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
# <a name="use-php-tooquery-an-azure-sql-database"></a><span data-ttu-id="5b150-103">Использование PHP tooquery базы данных Azure SQL</span><span class="sxs-lookup"><span data-stu-id="5b150-103">Use PHP tooquery an Azure SQL database</span></span>

<span data-ttu-id="5b150-104">В этом учебнике быстрого запуска показано как toouse [PHP](http://php.net/manual/en/intro-whatis.php) toocreate tooan tooconnect программы Azure SQL базы данных и использовать данные tooquery инструкций Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="5b150-104">This quick start tutorial demonstrates how toouse [PHP](http://php.net/manual/en/intro-whatis.php) toocreate a program tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b150-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5b150-105">Prerequisites</span></span>

<span data-ttu-id="5b150-106">toocomplete этом краткое руководство по началу работы, убедитесь, что у вас есть следующие hello:</span><span class="sxs-lookup"><span data-stu-id="5b150-106">toocomplete this quick start tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="5b150-107">База данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="5b150-107">An Azure SQL database.</span></span> <span data-ttu-id="5b150-108">В этом кратком руководстве использует ресурсы hello, созданные в одном из этих краткие руководства:</span><span class="sxs-lookup"><span data-stu-id="5b150-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="5b150-109">Создание базы данных с помощью портала</span><span class="sxs-lookup"><span data-stu-id="5b150-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="5b150-110">Создание базы данных SQL Azure и отправка к ней запросов с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5b150-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="5b150-111">Создание базы данных с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b150-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="5b150-112">Объект [правила брандмауэра уровня сервера](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) для hello общедоступный IP-адрес компьютера hello, используйте для этого краткого руководства.</span><span class="sxs-lookup"><span data-stu-id="5b150-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>

- <span data-ttu-id="5b150-113">Убедитесь, что установлен PHP и связанное программное обеспечение для вашей операционной системы.</span><span class="sxs-lookup"><span data-stu-id="5b150-113">You have installed PHP and related software for your operating system.</span></span>

    - <span data-ttu-id="5b150-114">**MacOS**: установить Homebrew и PHP, установка драйвера ODBC hello и SQLCMD, а затем установите hello драйвера PHP для SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5b150-114">**MacOS**: Install Homebrew and PHP, install hello ODBC driver and SQLCMD, and then install hello PHP Driver for SQL Server.</span></span> <span data-ttu-id="5b150-115">См. [шаги 1.2, 1.3 и 2.1](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/mac/).</span><span class="sxs-lookup"><span data-stu-id="5b150-115">See [Steps 1.2, 1.3, and 2.1](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/mac/).</span></span>
    - <span data-ttu-id="5b150-116">**Ubuntu**: установить PHP и другие необходимые пакеты, а затем установить hello драйвера PHP для SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5b150-116">**Ubuntu**:  Install PHP and other required packages, and then install hello PHP Driver for SQL Server.</span></span> <span data-ttu-id="5b150-117">См. [шаги 1.2 и 2.1](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="5b150-117">See [Steps 1.2 and 2.1](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu/).</span></span>
    - <span data-ttu-id="5b150-118">**Windows**: Установка hello последнюю версию PHP в IIS Express, последние версии драйверов Майкрософт для SQL Server в IIS Express, Chocolatey, драйвер ODBC hello и SQLCMD hello.</span><span class="sxs-lookup"><span data-stu-id="5b150-118">**Windows**: Install hello newest version of PHP for IIS Express, hello newest version of Microsoft Drivers for SQL Server in IIS Express, Chocolatey, hello ODBC driver, and SQLCMD.</span></span> <span data-ttu-id="5b150-119">См. [шаги 1.2 и 1.3](https://www.microsoft.com/sql-server/developer-get-started/php/windows/).</span><span class="sxs-lookup"><span data-stu-id="5b150-119">See [Steps 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/php/windows/).</span></span>    

## <a name="sql-server-connection-information"></a><span data-ttu-id="5b150-120">Сведения о подключении SQL Server</span><span class="sxs-lookup"><span data-stu-id="5b150-120">SQL server connection information</span></span>

<span data-ttu-id="5b150-121">Получите базу данных Azure SQL toohello tooconnect в сведения, необходимые подключения hello.</span><span class="sxs-lookup"><span data-stu-id="5b150-121">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="5b150-122">Необходимо будет hello полное имя сервера, имя базы данных и сведения об имени входа в следующих процедурах hello.</span><span class="sxs-lookup"><span data-stu-id="5b150-122">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="5b150-123">Войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5b150-123">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="5b150-124">Выберите **баз данных SQL** hello левом меню и выберите базу данных на hello **баз данных SQL** страницы.</span><span class="sxs-lookup"><span data-stu-id="5b150-124">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="5b150-125">На hello **Обзор** страницу для базы данных, просмотрите hello полное доменное имя сервера, как показано в hello после изображения.</span><span class="sxs-lookup"><span data-stu-id="5b150-125">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="5b150-126">Можно навести на toobring имя сервера hello копирование hello **щелкните toocopy** параметр.</span><span class="sxs-lookup"><span data-stu-id="5b150-126">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span>  

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="5b150-128">Если вы забыли учетные данные входа сервера, перейдите toohello базы данных SQL server страницы tooview hello server с именем admin и, при необходимости сбросить пароль hello.</span><span class="sxs-lookup"><span data-stu-id="5b150-128">If you forget your server login information, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span>     
    
## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="5b150-129">Вставьте код базы данных SQL tooquery</span><span class="sxs-lookup"><span data-stu-id="5b150-129">Insert code tooquery SQL database</span></span>

1. <span data-ttu-id="5b150-130">Создайте файл **sqltest.php** в предпочитаемом текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="5b150-130">In your favorite text editor, create a new file, **sqltest.php**.</span></span>  

2. <span data-ttu-id="5b150-131">Замените содержимое hello hello ниже программный код и добавить hello соответствующие значения для сервера, базы данных, пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="5b150-131">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

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

## <a name="run-hello-code"></a><span data-ttu-id="5b150-132">Выполнение кода hello</span><span class="sxs-lookup"><span data-stu-id="5b150-132">Run hello code</span></span>

1. <span data-ttu-id="5b150-133">Hello командной строки выполните следующие команды hello.</span><span class="sxs-lookup"><span data-stu-id="5b150-133">At hello command prompt, run hello following commands:</span></span>

   ```php
   php sqltest.php
   ```

2. <span data-ttu-id="5b150-134">Убедитесь, что возвращаются первые 20 строк hello и закройте окно приложения hello.</span><span class="sxs-lookup"><span data-stu-id="5b150-134">Verify that hello top 20 rows are returned and then close hello application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b150-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5b150-135">Next steps</span></span>
- [<span data-ttu-id="5b150-136">Проектирование первой базы данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="5b150-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- <span data-ttu-id="5b150-137">[Microsoft PHP Drivers for SQL Server](https://github.com/Microsoft/msphpsql/) (Драйверы Microsoft PHP для SQL Server)</span><span class="sxs-lookup"><span data-stu-id="5b150-137">[Microsoft PHP Drivers for SQL Server](https://github.com/Microsoft/msphpsql/)</span></span>
- [<span data-ttu-id="5b150-138">Сообщите о проблемах или задайте вопросы</span><span class="sxs-lookup"><span data-stu-id="5b150-138">Report issues or ask questions</span></span>](https://github.com/Microsoft/msphpsql/issues)
