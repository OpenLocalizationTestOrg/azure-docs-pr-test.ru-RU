---
title: "Использование Java для создания запросов к базе данных SQL Azure | Документация Майкрософт"
description: "В этой статье показано, как использовать Java для создания программы, которая подключается к базе данных SQL Azure, и создавать к ней запросы с помощью инструкций Transact-SQL."
services: sql-database
documentationcenter: 
author: ajlam
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: andrela
ms.openlocfilehash: 103b0755ab89a13297cfdc9ec72416664da8c1e9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="use-java-to-query-an-azure-sql-database"></a><span data-ttu-id="4f7e4-103">Использование Java для создания запросов к базе данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="4f7e4-103">Use Java to query an Azure SQL database</span></span>

<span data-ttu-id="4f7e4-104">В этом кратком руководстве показано, как использовать [Java](https://docs.microsoft.com/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server) для подключения к базе данных SQL Azure, а затем с помощью инструкций Transact-SQL выполнить запрос к данным.</span><span class="sxs-lookup"><span data-stu-id="4f7e4-104">This quick start demonstrates how to use [Java](https://docs.microsoft.com/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server) to connect to an Azure SQL database and then use Transact-SQL statements to query data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4f7e4-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4f7e4-105">Prerequisites</span></span>

<span data-ttu-id="4f7e4-106">Ниже указаны требования для работы с этим кратким руководством.</span><span class="sxs-lookup"><span data-stu-id="4f7e4-106">To complete this quick start tutorial, make sure you have the following prerequisites:</span></span>

- <span data-ttu-id="4f7e4-107">База данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="4f7e4-107">An Azure SQL database.</span></span> <span data-ttu-id="4f7e4-108">В этом кратком руководстве используются ресурсы, созданные в одном из этих кратких руководств:</span><span class="sxs-lookup"><span data-stu-id="4f7e4-108">This quick start uses the resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="4f7e4-109">Создание базы данных с помощью портала</span><span class="sxs-lookup"><span data-stu-id="4f7e4-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="4f7e4-110">Создание базы данных SQL Azure и отправка к ней запросов с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4f7e4-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="4f7e4-111">Создание базы данных с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="4f7e4-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="4f7e4-112">[Правило брандмауэра на уровне сервера](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) для общедоступного IP-адреса компьютера, на котором выполняются действия из этого краткого руководства.</span><span class="sxs-lookup"><span data-stu-id="4f7e4-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for the public IP address of the computer you use for this quick start tutorial.</span></span>

- <span data-ttu-id="4f7e4-113">Убедитесь, что установлен Java и связанное программное обеспечение для вашей операционной системы.</span><span class="sxs-lookup"><span data-stu-id="4f7e4-113">You have installed Java and related software for your operating system.</span></span>

    - <span data-ttu-id="4f7e4-114">**Mac OS.** Установите Homebrew и Java, а затем Maven.</span><span class="sxs-lookup"><span data-stu-id="4f7e4-114">**MacOS**: Install Homebrew and Java, and then install Maven.</span></span> <span data-ttu-id="4f7e4-115">Ознакомьтесь с шагами 1.2 и 1.3 в [этом руководстве](https://www.microsoft.com/sql-server/developer-get-started/java/mac/).</span><span class="sxs-lookup"><span data-stu-id="4f7e4-115">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/mac/).</span></span>
    - <span data-ttu-id="4f7e4-116">**Ubuntu.** Установите комплект разработчика Java и Maven.</span><span class="sxs-lookup"><span data-stu-id="4f7e4-116">**Ubuntu**:  Install the Java Development Kit, and install Maven.</span></span> <span data-ttu-id="4f7e4-117">Ознакомьтесь с шагами 1.2, 1.3 и 1.4 в [этом руководстве](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="4f7e4-117">See [Step 1.2, 1.3, and 1.4](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/).</span></span>
    - <span data-ttu-id="4f7e4-118">**Windows.** Установите комплект разработчика Java и Maven.</span><span class="sxs-lookup"><span data-stu-id="4f7e4-118">**Windows**: Install the Java Development Kit, and Maven.</span></span> <span data-ttu-id="4f7e4-119">Ознакомьтесь с шагами 1.2 и 1.3 в [этом руководстве](https://www.microsoft.com/sql-server/developer-get-started/java/windows/).</span><span class="sxs-lookup"><span data-stu-id="4f7e4-119">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/windows/).</span></span>    

## <a name="sql-server-connection-information"></a><span data-ttu-id="4f7e4-120">Сведения о подключении SQL Server</span><span class="sxs-lookup"><span data-stu-id="4f7e4-120">SQL server connection information</span></span>

<span data-ttu-id="4f7e4-121">Получите сведения о подключении, необходимые для подключения к базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="4f7e4-121">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="4f7e4-122">Вам понадобится следующее: полное имя сервера, имя базы данных и сведения для входа.</span><span class="sxs-lookup"><span data-stu-id="4f7e4-122">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="4f7e4-123">Войдите на [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4f7e4-123">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="4f7e4-124">В меню слева выберите **Базы данных SQL** и на странице **Базы данных SQL** щелкните имя своей базы данных.</span><span class="sxs-lookup"><span data-stu-id="4f7e4-124">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="4f7e4-125">На странице **Обзор** базы данных просмотрите полное имя сервера, как показано на рисунке ниже. Вы можете навести указатель мыши на имя сервера, чтобы отобразился пункт **Щелкните, чтобы скопировать**.</span><span class="sxs-lookup"><span data-stu-id="4f7e4-125">On the **Overview** page for your database, review the fully qualified server name as shown in the following image: You can hover over the server name to bring up the **Click to copy** option.</span></span>  

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="4f7e4-127">Если вы забыли данные для входа на сервер базы данных SQL, перейдите на соответствующую страницу, чтобы просмотреть имя администратора сервера.</span><span class="sxs-lookup"><span data-stu-id="4f7e4-127">If you forget your server login information, navigate to the SQL Database server page to view the server admin name.</span></span>  <span data-ttu-id="4f7e4-128">При необходимости сбросьте пароль.</span><span class="sxs-lookup"><span data-stu-id="4f7e4-128">If necessary, reset the password.</span></span>     

## <a name="create-maven-project-and-dependencies"></a><span data-ttu-id="4f7e4-129">**Создание проекта Maven и зависимостей**</span><span class="sxs-lookup"><span data-stu-id="4f7e4-129">**Create Maven project and dependencies**</span></span>
1. <span data-ttu-id="4f7e4-130">В терминале создайте проект Maven с именем **sqltest**.</span><span class="sxs-lookup"><span data-stu-id="4f7e4-130">From the terminal, create a new Maven project called **sqltest**.</span></span> 

   ```bash
   mvn archetype:generate "-DgroupId=com.sqldbsamples" "-DartifactId=sqltest" "-DarchetypeArtifactId=maven-archetype-quickstart" "-Dversion=1.0.0"
   ```

2. <span data-ttu-id="4f7e4-131">При появлении запроса введите **Y**.</span><span class="sxs-lookup"><span data-stu-id="4f7e4-131">Enter **Y** when prompted.</span></span>
3. <span data-ttu-id="4f7e4-132">Перейдите в каталог **sqltest** и откройте ***pom.xml*** с помощью предпочитаемого текстового редактора.</span><span class="sxs-lookup"><span data-stu-id="4f7e4-132">Change directory to **sqltest** and open ***pom.xml*** with your favorite text editor.</span></span>  <span data-ttu-id="4f7e4-133">Добавьте **Microsoft JDBC Driver для SQL Server** к зависимостям проекта, используя следующий код:</span><span class="sxs-lookup"><span data-stu-id="4f7e4-133">Add the **Microsoft JDBC Driver for SQL Server** to your project's dependencies using the following code:</span></span>

   ```xml
   <dependency>
       <groupId>com.microsoft.sqlserver</groupId>
       <artifactId>mssql-jdbc</artifactId>
       <version>6.2.1.jre8</version>
   </dependency>
   ```

4. <span data-ttu-id="4f7e4-134">В файле ***pom.xml*** добавьте в проект указанные ниже свойства.</span><span class="sxs-lookup"><span data-stu-id="4f7e4-134">Also in ***pom.xml***, add the following properties to your project.</span></span>  <span data-ttu-id="4f7e4-135">Если у вас нет раздела свойств, его можно добавить после зависимостей.</span><span class="sxs-lookup"><span data-stu-id="4f7e4-135">If you don't have a properties section, you can add it after the dependencies.</span></span>

   ```xml
   <properties>
       <maven.compiler.source>1.8</maven.compiler.source>
       <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   ```

5. <span data-ttu-id="4f7e4-136">Сохраните и закройте файл ***pom.xml***.</span><span class="sxs-lookup"><span data-stu-id="4f7e4-136">Save and close ***pom.xml***.</span></span>

## <a name="insert-code-to-query-sql-database"></a><span data-ttu-id="4f7e4-137">Вставка кода для отправки запроса к базе данных SQL</span><span class="sxs-lookup"><span data-stu-id="4f7e4-137">Insert code to query SQL database</span></span>

1. <span data-ttu-id="4f7e4-138">В проекте Maven уже должен быть файл с именем ***App.java***, расположенный в папке: \sqltest\src\main\java\com\sqlsamples\App.java.</span><span class="sxs-lookup"><span data-stu-id="4f7e4-138">You should already have a file called ***App.java*** in your Maven project located at:  ..\sqltest\src\main\java\com\sqlsamples\App.java</span></span>

2. <span data-ttu-id="4f7e4-139">Откройте файл, замените содержимое следующим кодом и добавьте соответствующие значения для сервера, базы данных, пользователя и пароля.</span><span class="sxs-lookup"><span data-stu-id="4f7e4-139">Open the file and replace its contents with the following code and add the appropriate values for your server, database, user, and password.</span></span>

   ```java
   package com.sqldbsamples;

   import java.sql.Connection;
   import java.sql.Statement;
   import java.sql.PreparedStatement;
   import java.sql.ResultSet;
   import java.sql.DriverManager;

   public class App {

    public static void main(String[] args) {
    
        // Connect to database
           String hostName = "your_server.database.windows.net";
           String dbName = "your_database";
           String user = "your_username";
           String password = "your_password";
           String url = String.format("jdbc:sqlserver://%s:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", hostName, dbName, user, password);
           Connection connection = null;

           try {
                   connection = DriverManager.getConnection(url);
                   String schema = connection.getSchema();
                   System.out.println("Successful connection - Schema: " + schema);

                   System.out.println("Query data example:");
                   System.out.println("=========================================");

                   // Create and execute a SELECT SQL statement.
                   String selectSql = "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName " 
                       + "FROM [SalesLT].[ProductCategory] pc "  
                       + "JOIN [SalesLT].[Product] p ON pc.productcategoryid = p.productcategoryid";
                
                   try (Statement statement = connection.createStatement();
                       ResultSet resultSet = statement.executeQuery(selectSql)) {

                           // Print results from select statement
                           System.out.println("Top 20 categories:");
                           while (resultSet.next())
                           {
                               System.out.println(resultSet.getString(1) + " "
                                   + resultSet.getString(2));
                           }
                    connection.close();
                   }                   
           }
           catch (Exception e) {
                   e.printStackTrace();
           }
       }
   }
   ```

## <a name="run-the-code"></a><span data-ttu-id="4f7e4-140">Выполнение кода</span><span class="sxs-lookup"><span data-stu-id="4f7e4-140">Run the code</span></span>

1. <span data-ttu-id="4f7e4-141">В командной строке выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="4f7e4-141">At the command prompt, run the following commands:</span></span>

   ```bash
   mvn package
   mvn -q exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   ```

2. <span data-ttu-id="4f7e4-142">Убедитесь, что возвращены первые 20 строк, а затем закройте окно приложения.</span><span class="sxs-lookup"><span data-stu-id="4f7e4-142">Verify that the top 20 rows are returned and then close the application window.</span></span>


## <a name="next-steps"></a><span data-ttu-id="4f7e4-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4f7e4-143">Next steps</span></span>
- [<span data-ttu-id="4f7e4-144">Проектирование первой базы данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="4f7e4-144">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="4f7e4-145">Microsoft JDBC Driver для SQL Server</span><span class="sxs-lookup"><span data-stu-id="4f7e4-145">Microsoft JDBC Driver for SQL Server</span></span>](https://github.com/microsoft/mssql-jdbc)
- [<span data-ttu-id="4f7e4-146">Сообщите о проблеме или задайте вопросы</span><span class="sxs-lookup"><span data-stu-id="4f7e4-146">Report issues/ask questions</span></span>](https://github.com/microsoft/mssql-jdbc/issues)

