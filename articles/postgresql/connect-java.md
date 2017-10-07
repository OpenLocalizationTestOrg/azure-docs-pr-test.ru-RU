---
title: "Подключение tooAzure базы данных PostgreSQL, с помощью Java | Документы Microsoft"
description: "Это краткое руководство содержит пример кода Java можно использовать tooconnect и запроса данных из базы данных Azure для PostgreSQL."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: java
ms.topic: quickstart
ms.date: 06/23/2017
ms.openlocfilehash: 8f6e0a47a0d6dfebf29eb56c31ccccabd7c2b670
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-java-tooconnect-and-query-data"></a><span data-ttu-id="d3627-103">База данных Azure для PostgreSQL: tooconnect и запрашивают данные, используйте Java</span><span class="sxs-lookup"><span data-stu-id="d3627-103">Azure Database for PostgreSQL: Use Java tooconnect and query data</span></span>
<span data-ttu-id="d3627-104">Это краткое руководство демонстрирует, как tooconnect tooan Azure этой базы данных PostgreSQL, с помощью приложения Java.</span><span class="sxs-lookup"><span data-stu-id="d3627-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using a Java application.</span></span> <span data-ttu-id="d3627-105">Показано, как tooquery инструкций SQL toouse, вставка, обновление и удаление данных в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="d3627-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="d3627-106">Hello в этой статье предполагается, что вы знакомы с разработка с использованием Java и наличие новых tooworking с базой данных Azure для PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="d3627-106">hello steps in this article assume that you are familiar with developing using Java, and that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d3627-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d3627-107">Prerequisites</span></span>
<span data-ttu-id="d3627-108">Это краткое руководство использует ресурсы hello, созданные в любой из этих руководствах по в качестве отправной точки.</span><span class="sxs-lookup"><span data-stu-id="d3627-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="d3627-109">Создание базы данных с помощью портала</span><span class="sxs-lookup"><span data-stu-id="d3627-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="d3627-110">Создание базы данных с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d3627-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="d3627-111">Также вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="d3627-111">You also need to:</span></span>
- <span data-ttu-id="d3627-112">Загрузите hello [драйвер JDBC PostgreSQL](https://jdbc.postgresql.org/download.html) сопоставления версии Java и hello Java Development Kit.</span><span class="sxs-lookup"><span data-stu-id="d3627-112">Download hello [PostgreSQL JDBC Driver](https://jdbc.postgresql.org/download.html) matching your version of Java and hello Java Development Kit.</span></span>
- <span data-ttu-id="d3627-113">Включите hello PostgreSQL JDBC jar-файл (например, postgresql-42.1.1.jar) в приложение классам.</span><span class="sxs-lookup"><span data-stu-id="d3627-113">Include hello PostgreSQL JDBC jar file (for example postgresql-42.1.1.jar) in your application classpath.</span></span> <span data-ttu-id="d3627-114">Дополнительные сведения см. на [странице по настройке пути к классу](https://jdbc.postgresql.org/documentation/head/classpath.html).</span><span class="sxs-lookup"><span data-stu-id="d3627-114">For more information, see [classpath details](https://jdbc.postgresql.org/documentation/head/classpath.html).</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="d3627-115">Получение сведений о подключении</span><span class="sxs-lookup"><span data-stu-id="d3627-115">Get connection information</span></span>
<span data-ttu-id="d3627-116">Получите toohello tooconnect базы данных Azure для hello подключения сведения, необходимые для PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="d3627-116">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="d3627-117">Необходимо hello server полное имя и учетные данные входа.</span><span class="sxs-lookup"><span data-stu-id="d3627-117">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="d3627-118">Войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d3627-118">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="d3627-119">Hello левого меню на портале Azure, щелкните **все ресурсы** и выполните поиск сервера hello, вы создали, таких как **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="d3627-119">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="d3627-120">Щелкните имя сервера hello **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="d3627-120">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="d3627-121">Выберите hello server **Обзор** страницы.</span><span class="sxs-lookup"><span data-stu-id="d3627-121">Select hello server's **Overview** page.</span></span> <span data-ttu-id="d3627-122">Запишите hello **имя сервера** и **имя входа администратора сервера**.</span><span class="sxs-lookup"><span data-stu-id="d3627-122">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="d3627-123">![База данных Azure для PostgreSQL. Учетные данные администратора сервера для входа](./media/connect-java/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="d3627-123">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-java/1-connection-string.png)</span></span>
5. <span data-ttu-id="d3627-124">Если вы забыли учетные данные входа сервера, перейдите toohello **Обзор** страница hello tooview: имя пользователя администратора сервера и, при необходимости переустановить пароль hello.</span><span class="sxs-lookup"><span data-stu-id="d3627-124">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="d3627-125">Подключение, создание таблицы и вставка данных</span><span class="sxs-lookup"><span data-stu-id="d3627-125">Connect, create table, and insert data</span></span>
<span data-ttu-id="d3627-126">Hello используйте следующий код tooconnect нагрузки hello данных и с помощью функции hello с **вставить** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="d3627-126">Use hello following code tooconnect and load hello data using hello function with an **INSERT** SQL statement.</span></span> <span data-ttu-id="d3627-127">Здравствуйте, методы [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html), и [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) , используемые tooconnect, удалите и создайте таблицу hello.</span><span class="sxs-lookup"><span data-stu-id="d3627-127">hello methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) are used tooconnect, drop, and create hello table.</span></span> <span data-ttu-id="d3627-128">Hello [prepareStatement](https://jdbc.postgresql.org/documentation/head/query.html) объект является команды insert hello используется toobuild с setString() и setInt() toobind hello значениями параметров.</span><span class="sxs-lookup"><span data-stu-id="d3627-128">hello [prepareStatement](https://jdbc.postgresql.org/documentation/head/query.html) object is used toobuild hello insert commands, with setString() and setInt() toobind hello parameter values.</span></span> <span data-ttu-id="d3627-129">Метод [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) запусков hello команду для каждого набора параметров.</span><span class="sxs-lookup"><span data-stu-id="d3627-129">Method [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) runs hello command for each set of parameters.</span></span> 

<span data-ttu-id="d3627-130">Замените hello узла, базы данных, пользователя и пароль параметры hello значения, заданные при создании собственного сервера и базы данных.</span><span class="sxs-lookup"><span data-stu-id="d3627-130">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class CreateTableInsertRows {

    public static void main (String[] args)  throws Exception
    {

        // Initialize connection variables.
        String host = "mypgserver-20170401.postgres.database.azure.com";
        String database = "mypgsqldb";
        String user = "mylogin@mypgserver-20170401";
        String password = "<server_admin_password>";

        // check that hello driver is installed
        try
        {
            Class.forName("org.postgresql.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("PostgreSQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("PostgreSQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:postgresql://%s/%s", host, database);
            
            // set up hello connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed toocreate connection toodatabase.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection toodatabase.");
        
            // Perform some SQL queries over hello connection.
            try
            {
                // Drop previous table of same name if one exists.
                Statement statement = connection.createStatement();
                statement.execute("DROP TABLE IF EXISTS inventory;");
                System.out.println("Finished dropping table (if existed).");
    
                // Create table.
                statement.execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);");
                System.out.println("Created table.");
    
                // Insert some data into table.
                int nRowsInserted = 0;
                PreparedStatement preparedStatement = connection.prepareStatement("INSERT INTO inventory (name, quantity) VALUES (?, ?);");
                preparedStatement.setString(1, "banana");
                preparedStatement.setInt(2, 150);
                nRowsInserted += preparedStatement.executeUpdate();

                preparedStatement.setString(1, "orange");
                preparedStatement.setInt(2, 154);
                nRowsInserted += preparedStatement.executeUpdate();

                preparedStatement.setString(1, "apple");
                preparedStatement.setInt(2, 100);
                nRowsInserted += preparedStatement.executeUpdate();
                System.out.println(String.format("Inserted %d row(s) of data.", nRowsInserted));
    
                // NOTE No need toocommit all changes toodatabase, as auto-commit is enabled by default.
    
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed toocreate connection toodatabase.");
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="read-data"></a><span data-ttu-id="d3627-131">Считывание данных</span><span class="sxs-lookup"><span data-stu-id="d3627-131">Read data</span></span>
<span data-ttu-id="d3627-132">Используйте hello следующий код tooread hello данных с помощью **ВЫБЕРИТЕ** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="d3627-132">Use hello following code tooread hello data with a **SELECT** SQL statement.</span></span> <span data-ttu-id="d3627-133">Здравствуйте, методы [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html), и [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) , используемые tooconnect можно создавать и выполнять инструкции select hello.</span><span class="sxs-lookup"><span data-stu-id="d3627-133">hello methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) are used tooconnect, create, and run hello select statement.</span></span> <span data-ttu-id="d3627-134">результаты Hello обрабатываются с использованием [ResultSet](https://www.postgresql.org/docs/7.4/static/jdbc-query.html) объекта.</span><span class="sxs-lookup"><span data-stu-id="d3627-134">hello results are processed using a [ResultSet](https://www.postgresql.org/docs/7.4/static/jdbc-query.html) object.</span></span> 

<span data-ttu-id="d3627-135">Замените hello узла, базы данных, пользователя и пароль параметры hello значения, заданные при создании собственного сервера и базы данных.</span><span class="sxs-lookup"><span data-stu-id="d3627-135">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class ReadTable {

    public static void main (String[] args)  throws Exception
    {

        // Initialize connection variables.
        String host = "mypgserver-20170401.postgres.database.azure.com";
        String database = "mypgsqldb";
        String user = "mylogin@mypgserver-20170401";
        String password = "<server_admin_password>";

        // check that hello driver is installed
        try
        {
            Class.forName("org.postgresql.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("PostgreSQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("PostgreSQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:postgresql://%s/%s", host, database);
            
            // set up hello connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed toocreate connection toodatabase.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection toodatabase.");
        
            // Perform some SQL queries over hello connection.
            try
            {
    
                Statement statement = connection.createStatement();
                ResultSet results = statement.executeQuery("SELECT * from inventory;");
                while (results.next())
                {
                    String outputString = 
                        String.format(
                            "Data row = (%s, %s, %s)",
                            results.getString(1),
                            results.getString(2),
                            results.getString(3));
                    System.out.println(outputString);
                }
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed toocreate connection toodatabase.");
        }
        System.out.println("Execution finished.");
    }
}

```

## <a name="update-data"></a><span data-ttu-id="d3627-136">Обновление данных</span><span class="sxs-lookup"><span data-stu-id="d3627-136">Update data</span></span>
<span data-ttu-id="d3627-137">Используйте hello следующий код toochange hello данных с помощью **обновление** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="d3627-137">Use hello following code toochange hello data with an **UPDATE** SQL statement.</span></span> <span data-ttu-id="d3627-138">Здравствуйте, методы [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html), и [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) , используемые tooconnect Подготовка и выполнение инструкции update hello.</span><span class="sxs-lookup"><span data-stu-id="d3627-138">hello methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) are used tooconnect, prepare, and run hello update statement.</span></span> 

<span data-ttu-id="d3627-139">Замените hello узла, базы данных, пользователя и пароль параметры hello значения, заданные при создании собственного сервера и базы данных.</span><span class="sxs-lookup"><span data-stu-id="d3627-139">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class UpdateTable {
    public static void main (String[] args)  throws Exception
    {

        // Initialize connection variables.
        String host = "mypgserver-20170401.postgres.database.azure.com";
        String database = "mypgsqldb";
        String user = "mylogin@mypgserver-20170401";
        String password = "<server_admin_password>";

        // check that hello driver is installed
        try
        {
            Class.forName("org.postgresql.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("PostgreSQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("PostgreSQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:postgresql://%s/%s", host, database);
            
            // set up hello connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed toocreate connection toodatabase.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection toodatabase.");
        
            // Perform some SQL queries over hello connection.
            try
            {
                // Modify some data in table.
                int nRowsUpdated = 0;
                PreparedStatement preparedStatement = connection.prepareStatement("UPDATE inventory SET quantity = ? WHERE name = ?;");
                preparedStatement.setInt(1, 200);
                preparedStatement.setString(2, "banana");
                nRowsUpdated += preparedStatement.executeUpdate();
                System.out.println(String.format("Updated %d row(s) of data.", nRowsUpdated));
    
                // NOTE No need toocommit all changes toodatabase, as auto-commit is enabled by default.
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed toocreate connection toodatabase.");
        }
        System.out.println("Execution finished.");
    }
}
```
## <a name="delete-data"></a><span data-ttu-id="d3627-140">Удаление данных</span><span class="sxs-lookup"><span data-stu-id="d3627-140">Delete data</span></span>
<span data-ttu-id="d3627-141">Используйте hello следующий код tooremove данных с помощью **удалить** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="d3627-141">Use hello following code tooremove data with a **DELETE** SQL statement.</span></span> <span data-ttu-id="d3627-142">Здравствуйте, методы [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html), и [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) , используемые tooconnect Подготовка и выполнение инструкции delete hello.</span><span class="sxs-lookup"><span data-stu-id="d3627-142">hello methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) are used tooconnect, prepare, and run hello delete statement.</span></span> 

<span data-ttu-id="d3627-143">Замените hello узла, базы данных, пользователя и пароль параметры hello значения, заданные при создании собственного сервера и базы данных.</span><span class="sxs-lookup"><span data-stu-id="d3627-143">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class DeleteTable {
    public static void main (String[] args)  throws Exception
    {

        // Initialize connection variables.
        String host = "mypgserver-20170401.postgres.database.azure.com";
        String database = "mypgsqldb";
        String user = "mylogin@mypgserver-20170401";
        String password = "<server_admin_password>";

        // check that hello driver is installed
        try
        {
            Class.forName("org.postgresql.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("PostgreSQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("PostgreSQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:postgresql://%s/%s", host, database);
            
            // set up hello connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed toocreate connection toodatabase.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection toodatabase.");
        
            // Perform some SQL queries over hello connection.
            try
            {
                // Delete some data from table.
                int nRowsDeleted = 0;
                PreparedStatement preparedStatement = connection.prepareStatement("DELETE FROM inventory WHERE name = ?;");
                preparedStatement.setString(1, "orange");
                nRowsDeleted += preparedStatement.executeUpdate();
                System.out.println(String.format("Deleted %d row(s) of data.", nRowsDeleted));
    
                // NOTE No need toocommit all changes toodatabase, as auto-commit is enabled by default.
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed toocreate connection toodatabase.");
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="d3627-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d3627-144">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="d3627-145">Перенос базы данных с помощью экспорта и импорта</span><span class="sxs-lookup"><span data-stu-id="d3627-145">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
