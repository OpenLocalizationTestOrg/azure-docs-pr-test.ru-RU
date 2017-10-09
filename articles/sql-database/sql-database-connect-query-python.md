---
title: "tooquery Python aaaUse базы данных SQL Azure | Документы Microsoft"
description: "В этом разделе показано, как toocreate Python toouse программу, которая соединяет tooan базы данных SQL Azure и запросов с помощью инструкций Transact-SQL."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 452ad236-7a15-4f19-8ea7-df528052a3ad
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: hero-article
ms.date: 08/08/2017
ms.author: carlrab
ms.openlocfilehash: 6c786e7a61f5ed3e7d2395da59acfeae008e90e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-python-tooquery-an-azure-sql-database"></a><span data-ttu-id="611ce-103">Использовать tooquery Python базы данных Azure SQL</span><span class="sxs-lookup"><span data-stu-id="611ce-103">Use Python tooquery an Azure SQL database</span></span>

 <span data-ttu-id="611ce-104">В этом кратком руководстве показано, как toouse [Python](https://python.org) tooconnect tooan Azure SQL базы данных и использовать данные tooquery инструкций Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="611ce-104">This quick start demonstrates how toouse [Python](https://python.org) tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="611ce-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="611ce-105">Prerequisites</span></span>

<span data-ttu-id="611ce-106">toocomplete этом краткое руководство по началу работы, убедитесь, что у вас есть следующие hello:</span><span class="sxs-lookup"><span data-stu-id="611ce-106">toocomplete this quick start tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="611ce-107">База данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="611ce-107">An Azure SQL database.</span></span> <span data-ttu-id="611ce-108">В этом кратком руководстве использует ресурсы hello, созданные в одном из этих краткие руководства:</span><span class="sxs-lookup"><span data-stu-id="611ce-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="611ce-109">Создание базы данных с помощью портала</span><span class="sxs-lookup"><span data-stu-id="611ce-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="611ce-110">Создание базы данных SQL Azure и отправка к ней запросов с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="611ce-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="611ce-111">Создание базы данных с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="611ce-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="611ce-112">Объект [правила брандмауэра уровня сервера](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) для hello общедоступный IP-адрес компьютера hello, используйте для этого краткого руководства.</span><span class="sxs-lookup"><span data-stu-id="611ce-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>

- <span data-ttu-id="611ce-113">Убедитесь, что установлен Python и связанное программное обеспечение для вашей операционной системы.</span><span class="sxs-lookup"><span data-stu-id="611ce-113">You have installed Python and related software for your operating system.</span></span>

    - <span data-ttu-id="611ce-114">**MacOS**: установить Homebrew и Python, установка драйвера ODBC hello и SQLCMD, а затем установите hello драйвер Python для SQL Server.</span><span class="sxs-lookup"><span data-stu-id="611ce-114">**MacOS**: Install Homebrew and Python, install hello ODBC driver and SQLCMD, and then install hello Python Driver for SQL Server.</span></span> <span data-ttu-id="611ce-115">См. [шаги 1.2, 1.3 и 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/mac/).</span><span class="sxs-lookup"><span data-stu-id="611ce-115">See [Steps 1.2, 1.3, and 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/mac/).</span></span>
    - <span data-ttu-id="611ce-116">**Ubuntu**: установите Python и другие необходимые пакеты, а затем установить hello драйвер Python SQL Server.</span><span class="sxs-lookup"><span data-stu-id="611ce-116">**Ubuntu**:  Install Python and other required packages, and then install hello Python Driver for SQL Server.</span></span> <span data-ttu-id="611ce-117">См. [шаги 1.2, 1.3 и 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="611ce-117">See [Steps 1.2, 1.3, and 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/ubuntu/).</span></span>
    - <span data-ttu-id="611ce-118">**Windows**: установить новейшую версию Python (переменная среды теперь настроен для вас) hello и установки драйвера ODBC hello и SQLCMD установите hello драйвер Python для SQL Server.</span><span class="sxs-lookup"><span data-stu-id="611ce-118">**Windows**: Install hello newest version of Python (environment variable is now configured for you), install hello ODBC driver and SQLCMD, and then install hello Python Driver for SQL Server.</span></span> <span data-ttu-id="611ce-119">Ознакомьтесь с шагами 1.2, 1.3 и 2.1 в [этом руководстве](https://www.microsoft.com/sql-server/developer-get-started/python/windows/).</span><span class="sxs-lookup"><span data-stu-id="611ce-119">See [Step 1.2, 1.3, and 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/windows/).</span></span> 

## <a name="sql-server-connection-information"></a><span data-ttu-id="611ce-120">Сведения о подключении SQL Server</span><span class="sxs-lookup"><span data-stu-id="611ce-120">SQL server connection information</span></span>

<span data-ttu-id="611ce-121">Получите базу данных Azure SQL toohello tooconnect в сведения, необходимые подключения hello.</span><span class="sxs-lookup"><span data-stu-id="611ce-121">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="611ce-122">Необходимо будет hello полное имя сервера, имя базы данных и сведения об имени входа в следующих процедурах hello.</span><span class="sxs-lookup"><span data-stu-id="611ce-122">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="611ce-123">Войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="611ce-123">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="611ce-124">Выберите **баз данных SQL** hello левом меню и выберите базу данных на hello **баз данных SQL** страницы.</span><span class="sxs-lookup"><span data-stu-id="611ce-124">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="611ce-125">На hello **Обзор** страницу для базы данных, просмотрите hello полное доменное имя сервера, как показано в hello после изображения.</span><span class="sxs-lookup"><span data-stu-id="611ce-125">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="611ce-126">Можно навести на toobring имя сервера hello копирование hello **щелкните toocopy** параметр.</span><span class="sxs-lookup"><span data-stu-id="611ce-126">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span>  

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="611ce-128">Если вы забыли учетные данные входа сервера, перейдите toohello базы данных SQL server страницы tooview hello server с именем admin и, при необходимости сбросить пароль hello.</span><span class="sxs-lookup"><span data-stu-id="611ce-128">If you forget your server login information, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span>     
    
## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="611ce-129">Вставьте код базы данных SQL tooquery</span><span class="sxs-lookup"><span data-stu-id="611ce-129">Insert code tooquery SQL database</span></span> 

1. <span data-ttu-id="611ce-130">Создайте файл **sqltest.py** в предпочитаемом текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="611ce-130">In your favorite text editor, create a new file, **sqltest.py**.</span></span>  

2. <span data-ttu-id="611ce-131">Замените содержимое hello hello ниже программный код и добавить hello соответствующие значения для сервера, базы данных, пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="611ce-131">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

```Python
import pyodbc
server = 'your_server.database.windows.net'
database = 'your_database'
username = 'your_username'
password = 'your_password'
driver= '{ODBC Driver 13 for SQL Server}'
cnxn = pyodbc.connect('DRIVER='+driver+';PORT=1433;SERVER='+server+';PORT=1443;DATABASE='+database+';UID='+username+';PWD='+ password)
cursor = cnxn.cursor()
cursor.execute("SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName FROM [SalesLT].[ProductCategory] pc JOIN [SalesLT].[Product] p ON pc.productcategoryid = p.productcategoryid")
row = cursor.fetchone()
while row:
    print (str(row[0]) + " " + str(row[1]))
    row = cursor.fetchone()
```

## <a name="run-hello-code"></a><span data-ttu-id="611ce-132">Выполнение кода hello</span><span class="sxs-lookup"><span data-stu-id="611ce-132">Run hello code</span></span>

1. <span data-ttu-id="611ce-133">Hello командной строки выполните следующие команды hello.</span><span class="sxs-lookup"><span data-stu-id="611ce-133">At hello command prompt, run hello following commands:</span></span>

   ```Python
   python sqltest.py
   ```

2. <span data-ttu-id="611ce-134">Убедитесь, что возвращаются первые 20 строк hello и закройте окно приложения hello.</span><span class="sxs-lookup"><span data-stu-id="611ce-134">Verify that hello top 20 rows are returned and then close hello application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="611ce-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="611ce-135">Next steps</span></span>

- [<span data-ttu-id="611ce-136">Проектирование первой базы данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="611ce-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- <span data-ttu-id="611ce-137">[Microsoft Python Drivers for SQL Server](https://docs.microsoft.com/sql/connect/python/python-driver-for-sql-server/) (Драйверы Microsoft Python для SQL Server)</span><span class="sxs-lookup"><span data-stu-id="611ce-137">[Microsoft Python Drivers for SQL Server](https://docs.microsoft.com/sql/connect/python/python-driver-for-sql-server/)</span></span>
- [<span data-ttu-id="611ce-138">Центр по разработке для Python</span><span class="sxs-lookup"><span data-stu-id="611ce-138">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/?v=17.23h)

