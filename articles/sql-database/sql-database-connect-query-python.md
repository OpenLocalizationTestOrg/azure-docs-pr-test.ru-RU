---
title: "Использование Python для создания запросов к базе данных SQL Azure | Документация Майкрософт"
description: "В этой статье показано, как использовать Python для создания программы, которая подключается к базе данных SQL Azure, и создавать к ней запросы с помощью инструкций Transact-SQL."
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
ms.openlocfilehash: afffcb9a4938bf97626f182bb4f4d099d807d411
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="use-python-to-query-an-azure-sql-database"></a><span data-ttu-id="fe557-103">Использование Python для создания запросов к базе данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="fe557-103">Use Python to query an Azure SQL database</span></span>

 <span data-ttu-id="fe557-104">В этом кратком руководстве показано, как использовать [Python](https://python.org) для подключения к базе данных SQL Azure, а затем с помощью инструкций Transact-SQL выполнить запрос к данным.</span><span class="sxs-lookup"><span data-stu-id="fe557-104">This quick start demonstrates how to use [Python](https://python.org) to connect to an Azure SQL database and use Transact-SQL statements to query data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe557-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="fe557-105">Prerequisites</span></span>

<span data-ttu-id="fe557-106">Ниже указаны требования для работы с этим кратким руководством.</span><span class="sxs-lookup"><span data-stu-id="fe557-106">To complete this quick start tutorial, make sure you have the following:</span></span>

- <span data-ttu-id="fe557-107">База данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="fe557-107">An Azure SQL database.</span></span> <span data-ttu-id="fe557-108">В этом кратком руководстве используются ресурсы, созданные в одном из этих кратких руководств:</span><span class="sxs-lookup"><span data-stu-id="fe557-108">This quick start uses the resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="fe557-109">Создание базы данных с помощью портала</span><span class="sxs-lookup"><span data-stu-id="fe557-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="fe557-110">Создание базы данных SQL Azure и отправка к ней запросов с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="fe557-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="fe557-111">Создание базы данных с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="fe557-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="fe557-112">[Правило брандмауэра на уровне сервера](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) для общедоступного IP-адреса компьютера, на котором выполняются действия из этого краткого руководства.</span><span class="sxs-lookup"><span data-stu-id="fe557-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for the public IP address of the computer you use for this quick start tutorial.</span></span>

- <span data-ttu-id="fe557-113">Убедитесь, что установлен Python и связанное программное обеспечение для вашей операционной системы.</span><span class="sxs-lookup"><span data-stu-id="fe557-113">You have installed Python and related software for your operating system.</span></span>

    - <span data-ttu-id="fe557-114">**Mac OS.** Установите Homebrew, Python, драйвер ODBC и SQLCMD, а затем драйвер Python для SQL Server.</span><span class="sxs-lookup"><span data-stu-id="fe557-114">**MacOS**: Install Homebrew and Python, install the ODBC driver and SQLCMD, and then install the Python Driver for SQL Server.</span></span> <span data-ttu-id="fe557-115">См. [шаги 1.2, 1.3 и 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/mac/).</span><span class="sxs-lookup"><span data-stu-id="fe557-115">See [Steps 1.2, 1.3, and 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/mac/).</span></span>
    - <span data-ttu-id="fe557-116">**Ubuntu.** Установите Python и другие необходимые пакеты, а затем установите драйвер Python для SQL Server.</span><span class="sxs-lookup"><span data-stu-id="fe557-116">**Ubuntu**:  Install Python and other required packages, and then install the Python Driver for SQL Server.</span></span> <span data-ttu-id="fe557-117">См. [шаги 1.2, 1.3 и 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="fe557-117">See [Steps 1.2, 1.3, and 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/ubuntu/).</span></span>
    - <span data-ttu-id="fe557-118">**Windows.** Установите последнюю версию Python (переменная среды теперь настраивается автоматически), драйвер ODBC и SQLCMD, а затем установите драйвер Python для SQL Server.</span><span class="sxs-lookup"><span data-stu-id="fe557-118">**Windows**: Install the newest version of Python (environment variable is now configured for you), install the ODBC driver and SQLCMD, and then install the Python Driver for SQL Server.</span></span> <span data-ttu-id="fe557-119">Ознакомьтесь с шагами 1.2, 1.3 и 2.1 в [этом руководстве](https://www.microsoft.com/sql-server/developer-get-started/python/windows/).</span><span class="sxs-lookup"><span data-stu-id="fe557-119">See [Step 1.2, 1.3, and 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/windows/).</span></span> 

## <a name="sql-server-connection-information"></a><span data-ttu-id="fe557-120">Сведения о подключении SQL Server</span><span class="sxs-lookup"><span data-stu-id="fe557-120">SQL server connection information</span></span>

<span data-ttu-id="fe557-121">Получите сведения о подключении, необходимые для подключения к базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="fe557-121">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="fe557-122">Вам понадобится следующее: полное имя сервера, имя базы данных и сведения для входа.</span><span class="sxs-lookup"><span data-stu-id="fe557-122">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="fe557-123">Войдите на [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="fe557-123">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="fe557-124">В меню слева выберите **Базы данных SQL** и на странице **Базы данных SQL** щелкните имя своей базы данных.</span><span class="sxs-lookup"><span data-stu-id="fe557-124">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="fe557-125">На странице **Обзор** базы данных просмотрите полное имя сервера, как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="fe557-125">On the **Overview** page for your database, review the fully qualified server name as shown in the following image.</span></span> <span data-ttu-id="fe557-126">Вы можете навести указатель мыши на имя сервера, чтобы отобразился пункт **Щелкните, чтобы скопировать**.</span><span class="sxs-lookup"><span data-stu-id="fe557-126">You can hover over the server name to bring up the **Click to copy** option.</span></span>  

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="fe557-128">Если вы забыли данные для входа на сервер, перейдите на соответствующую страницу, чтобы просмотреть имя администратора сервера и при необходимости сбросить пароль.</span><span class="sxs-lookup"><span data-stu-id="fe557-128">If you forget your server login information, navigate to the SQL Database server page to view the server admin name and, if necessary, reset the password.</span></span>     
    
## <a name="insert-code-to-query-sql-database"></a><span data-ttu-id="fe557-129">Вставка кода для отправки запроса к базе данных SQL</span><span class="sxs-lookup"><span data-stu-id="fe557-129">Insert code to query SQL database</span></span> 

1. <span data-ttu-id="fe557-130">Создайте файл **sqltest.py** в предпочитаемом текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="fe557-130">In your favorite text editor, create a new file, **sqltest.py**.</span></span>  

2. <span data-ttu-id="fe557-131">Замените содержимое следующим кодом и добавьте соответствующие значения для сервера, базы данных, пользователя и пароля.</span><span class="sxs-lookup"><span data-stu-id="fe557-131">Replace the contents with the following code and add the appropriate values for your server, database, user, and password.</span></span>

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

## <a name="run-the-code"></a><span data-ttu-id="fe557-132">Выполнение кода</span><span class="sxs-lookup"><span data-stu-id="fe557-132">Run the code</span></span>

1. <span data-ttu-id="fe557-133">В командной строке выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="fe557-133">At the command prompt, run the following commands:</span></span>

   ```Python
   python sqltest.py
   ```

2. <span data-ttu-id="fe557-134">Убедитесь, что возвращены первые 20 строк, а затем закройте окно приложения.</span><span class="sxs-lookup"><span data-stu-id="fe557-134">Verify that the top 20 rows are returned and then close the application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe557-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fe557-135">Next steps</span></span>

- [<span data-ttu-id="fe557-136">Проектирование первой базы данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="fe557-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- <span data-ttu-id="fe557-137">[Microsoft Python Drivers for SQL Server](https://docs.microsoft.com/sql/connect/python/python-driver-for-sql-server/) (Драйверы Microsoft Python для SQL Server)</span><span class="sxs-lookup"><span data-stu-id="fe557-137">[Microsoft Python Drivers for SQL Server](https://docs.microsoft.com/sql/connect/python/python-driver-for-sql-server/)</span></span>
- [<span data-ttu-id="fe557-138">Центр по разработке для Python</span><span class="sxs-lookup"><span data-stu-id="fe557-138">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/?v=17.23h)

