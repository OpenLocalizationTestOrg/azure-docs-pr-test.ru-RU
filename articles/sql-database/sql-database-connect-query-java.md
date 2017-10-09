---
title: "tooquery Java aaaUse базы данных SQL Azure | Документы Microsoft"
description: "В этом разделе показано, как toocreate Java toouse программу, которая соединяет tooan базы данных SQL Azure и запросов с помощью инструкций Transact-SQL."
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
ms.openlocfilehash: f014edbe38ca0e7b6e43f4eb4d2e53d3561bf3e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-java-tooquery-an-azure-sql-database"></a><span data-ttu-id="3da25-103">Используйте Java tooquery базы данных Azure SQL</span><span class="sxs-lookup"><span data-stu-id="3da25-103">Use Java tooquery an Azure SQL database</span></span>

<span data-ttu-id="3da25-104">В этом кратком руководстве показано, как toouse [Java](https://docs.microsoft.com/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server) tooconnect tooan Azure SQL базы данных и затем использовать данные tooquery инструкций Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="3da25-104">This quick start demonstrates how toouse [Java](https://docs.microsoft.com/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server) tooconnect tooan Azure SQL database and then use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3da25-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3da25-105">Prerequisites</span></span>

<span data-ttu-id="3da25-106">toocomplete этом краткое руководство по началу работы, убедитесь, что у вас есть hello следующие предварительные требования:</span><span class="sxs-lookup"><span data-stu-id="3da25-106">toocomplete this quick start tutorial, make sure you have hello following prerequisites:</span></span>

- <span data-ttu-id="3da25-107">База данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="3da25-107">An Azure SQL database.</span></span> <span data-ttu-id="3da25-108">В этом кратком руководстве использует ресурсы hello, созданные в одном из этих краткие руководства:</span><span class="sxs-lookup"><span data-stu-id="3da25-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="3da25-109">Создание базы данных с помощью портала</span><span class="sxs-lookup"><span data-stu-id="3da25-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="3da25-110">Создание базы данных SQL Azure и отправка к ней запросов с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3da25-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="3da25-111">Создание базы данных с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="3da25-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="3da25-112">Объект [правила брандмауэра уровня сервера](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) для hello общедоступный IP-адрес компьютера hello, используйте для этого краткого руководства.</span><span class="sxs-lookup"><span data-stu-id="3da25-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>

- <span data-ttu-id="3da25-113">Убедитесь, что установлен Java и связанное программное обеспечение для вашей операционной системы.</span><span class="sxs-lookup"><span data-stu-id="3da25-113">You have installed Java and related software for your operating system.</span></span>

    - <span data-ttu-id="3da25-114">**Mac OS.** Установите Homebrew и Java, а затем Maven.</span><span class="sxs-lookup"><span data-stu-id="3da25-114">**MacOS**: Install Homebrew and Java, and then install Maven.</span></span> <span data-ttu-id="3da25-115">Ознакомьтесь с шагами 1.2 и 1.3 в [этом руководстве](https://www.microsoft.com/sql-server/developer-get-started/java/mac/).</span><span class="sxs-lookup"><span data-stu-id="3da25-115">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/mac/).</span></span>
    - <span data-ttu-id="3da25-116">**Ubuntu**: hello Java Development Kit установки и установки Maven.</span><span class="sxs-lookup"><span data-stu-id="3da25-116">**Ubuntu**:  Install hello Java Development Kit, and install Maven.</span></span> <span data-ttu-id="3da25-117">Ознакомьтесь с шагами 1.2, 1.3 и 1.4 в [этом руководстве](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="3da25-117">See [Step 1.2, 1.3, and 1.4](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/).</span></span>
    - <span data-ttu-id="3da25-118">**Windows**: Установка hello Java Development Kit и Maven.</span><span class="sxs-lookup"><span data-stu-id="3da25-118">**Windows**: Install hello Java Development Kit, and Maven.</span></span> <span data-ttu-id="3da25-119">Ознакомьтесь с шагами 1.2 и 1.3 в [этом руководстве](https://www.microsoft.com/sql-server/developer-get-started/java/windows/).</span><span class="sxs-lookup"><span data-stu-id="3da25-119">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/windows/).</span></span>    

## <a name="sql-server-connection-information"></a><span data-ttu-id="3da25-120">Сведения о подключении SQL Server</span><span class="sxs-lookup"><span data-stu-id="3da25-120">SQL server connection information</span></span>

<span data-ttu-id="3da25-121">Получите базу данных Azure SQL toohello tooconnect в сведения, необходимые подключения hello.</span><span class="sxs-lookup"><span data-stu-id="3da25-121">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="3da25-122">Необходимо будет hello полное имя сервера, имя базы данных и сведения об имени входа в следующих процедурах hello.</span><span class="sxs-lookup"><span data-stu-id="3da25-122">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="3da25-123">Войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3da25-123">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="3da25-124">Выберите **баз данных SQL** hello левом меню и выберите базу данных на hello **баз данных SQL** страницы.</span><span class="sxs-lookup"><span data-stu-id="3da25-124">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="3da25-125">На hello **Обзор** страниц для базы данных, просмотрите hello полное имя сервера, как показано в hello после изображения: можно навести на toobring имя сервера hello копирование hello **щелкните toocopy** параметр.</span><span class="sxs-lookup"><span data-stu-id="3da25-125">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image: You can hover over hello server name toobring up hello **Click toocopy** option.</span></span>  

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="3da25-127">Если вы забыли учетные данные входа сервера, перейдите toohello базы данных SQL server tooview hello server admin имя страницы.</span><span class="sxs-lookup"><span data-stu-id="3da25-127">If you forget your server login information, navigate toohello SQL Database server page tooview hello server admin name.</span></span>  <span data-ttu-id="3da25-128">При необходимости hello сброс пароля.</span><span class="sxs-lookup"><span data-stu-id="3da25-128">If necessary, reset hello password.</span></span>     

## <a name="create-maven-project-and-dependencies"></a><span data-ttu-id="3da25-129">**Создание проекта Maven и зависимостей**</span><span class="sxs-lookup"><span data-stu-id="3da25-129">**Create Maven project and dependencies**</span></span>
1. <span data-ttu-id="3da25-130">Hello терминалов, создайте новый проект с именем Maven **sqltest**.</span><span class="sxs-lookup"><span data-stu-id="3da25-130">From hello terminal, create a new Maven project called **sqltest**.</span></span> 

   ```bash
   mvn archetype:generate "-DgroupId=com.sqldbsamples" "-DartifactId=sqltest" "-DarchetypeArtifactId=maven-archetype-quickstart" "-Dversion=1.0.0"
   ```

2. <span data-ttu-id="3da25-131">При появлении запроса введите **Y**.</span><span class="sxs-lookup"><span data-stu-id="3da25-131">Enter **Y** when prompted.</span></span>
3. <span data-ttu-id="3da25-132">Измените каталог слишком**sqltest** и откройте ***pom.xml*** с помощью любого текстового редактора.</span><span class="sxs-lookup"><span data-stu-id="3da25-132">Change directory too**sqltest** and open ***pom.xml*** with your favorite text editor.</span></span>  <span data-ttu-id="3da25-133">Добавить hello **драйвера Microsoft JDBC для SQL Server** зависимостей tooyour проекта с помощью hello следующий код:</span><span class="sxs-lookup"><span data-stu-id="3da25-133">Add hello **Microsoft JDBC Driver for SQL Server** tooyour project's dependencies using hello following code:</span></span>

   ```xml
   <dependency>
       <groupId>com.microsoft.sqlserver</groupId>
       <artifactId>mssql-jdbc</artifactId>
       <version>6.2.1.jre8</version>
   </dependency>
   ```

4. <span data-ttu-id="3da25-134">Кроме того, в ***pom.xml***, добавьте следующие свойства проекта tooyour hello.</span><span class="sxs-lookup"><span data-stu-id="3da25-134">Also in ***pom.xml***, add hello following properties tooyour project.</span></span>  <span data-ttu-id="3da25-135">Если отсутствует раздел свойств, его можно добавить после hello зависимостей.</span><span class="sxs-lookup"><span data-stu-id="3da25-135">If you don't have a properties section, you can add it after hello dependencies.</span></span>

   ```xml
   <properties>
       <maven.compiler.source>1.8</maven.compiler.source>
       <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   ```

5. <span data-ttu-id="3da25-136">Сохраните и закройте файл ***pom.xml***.</span><span class="sxs-lookup"><span data-stu-id="3da25-136">Save and close ***pom.xml***.</span></span>

## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="3da25-137">Вставьте код базы данных SQL tooquery</span><span class="sxs-lookup"><span data-stu-id="3da25-137">Insert code tooquery SQL database</span></span>

1. <span data-ttu-id="3da25-138">В проекте Maven уже должен быть файл с именем ***App.java***, расположенный в папке: \sqltest\src\main\java\com\sqlsamples\App.java.</span><span class="sxs-lookup"><span data-stu-id="3da25-138">You should already have a file called ***App.java*** in your Maven project located at:  ..\sqltest\src\main\java\com\sqlsamples\App.java</span></span>

2. <span data-ttu-id="3da25-139">Откройте файл hello и заменить его содержимое hello следующий код и добавить hello соответствующие значения для сервера, базы данных, пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="3da25-139">Open hello file and replace its contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

   ```java
   package com.sqldbsamples;

   import java.sql.Connection;
   import java.sql.Statement;
   import java.sql.PreparedStatement;
   import java.sql.ResultSet;
   import java.sql.DriverManager;

   public class App {

    public static void main(String[] args) {
    
        // Connect toodatabase
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

## <a name="run-hello-code"></a><span data-ttu-id="3da25-140">Выполнение кода hello</span><span class="sxs-lookup"><span data-stu-id="3da25-140">Run hello code</span></span>

1. <span data-ttu-id="3da25-141">Hello командной строки выполните следующие команды hello.</span><span class="sxs-lookup"><span data-stu-id="3da25-141">At hello command prompt, run hello following commands:</span></span>

   ```bash
   mvn package
   mvn -q exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   ```

2. <span data-ttu-id="3da25-142">Убедитесь, что возвращаются первые 20 строк hello и закройте окно приложения hello.</span><span class="sxs-lookup"><span data-stu-id="3da25-142">Verify that hello top 20 rows are returned and then close hello application window.</span></span>


## <a name="next-steps"></a><span data-ttu-id="3da25-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3da25-143">Next steps</span></span>
- [<span data-ttu-id="3da25-144">Проектирование первой базы данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="3da25-144">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="3da25-145">Microsoft JDBC Driver для SQL Server</span><span class="sxs-lookup"><span data-stu-id="3da25-145">Microsoft JDBC Driver for SQL Server</span></span>](https://github.com/microsoft/mssql-jdbc)
- [<span data-ttu-id="3da25-146">Сообщите о проблеме или задайте вопросы</span><span class="sxs-lookup"><span data-stu-id="3da25-146">Report issues/ask questions</span></span>](https://github.com/microsoft/mssql-jdbc/issues)

