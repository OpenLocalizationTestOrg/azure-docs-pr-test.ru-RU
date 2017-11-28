---
title: "Подключение tooAzure базы данных MySQL с помощью Java | Документы Microsoft"
description: "Это краткое руководство содержит пример кода Java можно использовать tooconnect и запроса данных из базы данных Azure для базы данных MySQL."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.topic: hero-article
ms.devlang: java
ms.date: 06/20/2017
ms.openlocfilehash: d584b5491d29700b36fae26800c59d93ceb3e265
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-java-tooconnect-and-query-data"></a><span data-ttu-id="ef87f-103">База данных Azure для MySQL: tooconnect и запрашивают данные, используйте Java</span><span class="sxs-lookup"><span data-stu-id="ef87f-103">Azure Database for MySQL: Use Java tooconnect and query data</span></span>
<span data-ttu-id="ef87f-104">Это краткое руководство демонстрирует, как tooconnect tooan Azure этой базы данных MySQL с помощью приложения Java.</span><span class="sxs-lookup"><span data-stu-id="ef87f-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using a Java application.</span></span> <span data-ttu-id="ef87f-105">Показано, как tooquery инструкций SQL toouse, вставка, обновление и удаление данных в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="ef87f-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="ef87f-106">Hello в этой статье предполагается, что вы знакомы с разработка с использованием Java и наличие новых tooworking с базой данных Azure для MySQL.</span><span class="sxs-lookup"><span data-stu-id="ef87f-106">hello steps in this article assume that you are familiar with developing using Java, and that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ef87f-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ef87f-107">Prerequisites</span></span>
<span data-ttu-id="ef87f-108">Это краткое руководство использует ресурсы hello, созданные в любой из этих руководствах по в качестве отправной точки.</span><span class="sxs-lookup"><span data-stu-id="ef87f-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- <span data-ttu-id="ef87f-109">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Создание сервера базы данных Azure для MySQL с помощью портала Azure)</span><span class="sxs-lookup"><span data-stu-id="ef87f-109">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md)</span></span>
- <span data-ttu-id="ef87f-110">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md) (Создание сервера базы данных Azure для MySQL с помощью Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="ef87f-110">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md)</span></span>

<span data-ttu-id="ef87f-111">Также вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="ef87f-111">You also need to:</span></span>
- <span data-ttu-id="ef87f-112">Загрузите драйвер JDBC hello [MySQL соединителя/J](https://dev.mysql.com/downloads/connector/j/)</span><span class="sxs-lookup"><span data-stu-id="ef87f-112">Download hello JDBC driver [MySQL Connector/J](https://dev.mysql.com/downloads/connector/j/)</span></span>
- <span data-ttu-id="ef87f-113">Включите hello JDBC jar-файл (например mysql соединитель java-5.1.42-bin.jar) в пути к классам вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="ef87f-113">Include hello JDBC jar file (for example mysql-connector-java-5.1.42-bin.jar) into your application classpath.</span></span> <span data-ttu-id="ef87f-114">Если возникнут сложности, изучите в документации по своей среде информацию о путях классов (например, [Apache Tomcat](https://tomcat.apache.org/tomcat-7.0-doc/class-loader-howto.html) или [Java SE](http://docs.oracle.com/javase/7/docs/technotes/tools/windows/classpath.html)).</span><span class="sxs-lookup"><span data-stu-id="ef87f-114">If you have trouble with this, please consult your environment's documentation for class path specifics, such as [Apache Tomcat](https://tomcat.apache.org/tomcat-7.0-doc/class-loader-howto.html) or [Java SE](http://docs.oracle.com/javase/7/docs/technotes/tools/windows/classpath.html)</span></span>
- <span data-ttu-id="ef87f-115">Убедитесь, что база данных Azure для обеспечения безопасности подключения MySQL настроена с брандмауэром Привет открыть и настройки SSL успешно изменено для tooconnect вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="ef87f-115">Ensure your Azure Database for MySQL connection security is configured with hello firewall opened and SSL settings adjusted for your application tooconnect successfully.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="ef87f-116">Получение сведений о подключении</span><span class="sxs-lookup"><span data-stu-id="ef87f-116">Get connection information</span></span>
<span data-ttu-id="ef87f-117">Получите toohello tooconnect базы данных Azure для hello подключения сведения, необходимые для MySQL.</span><span class="sxs-lookup"><span data-stu-id="ef87f-117">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="ef87f-118">Необходимо hello server полное имя и учетные данные входа.</span><span class="sxs-lookup"><span data-stu-id="ef87f-118">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="ef87f-119">Войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ef87f-119">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="ef87f-120">Hello левой панели щелкните **все ресурсы**и выполните поиск hello сервере был создан (например, **myserver4demo**).</span><span class="sxs-lookup"><span data-stu-id="ef87f-120">In hello left pane, click **All resources**, and then search for hello server you have created (for example, **myserver4demo**).</span></span>
3. <span data-ttu-id="ef87f-121">Щелкните имя сервера hello.</span><span class="sxs-lookup"><span data-stu-id="ef87f-121">Click hello server name.</span></span>
4. <span data-ttu-id="ef87f-122">Выберите hello server **свойства** страницы.</span><span class="sxs-lookup"><span data-stu-id="ef87f-122">Select hello server's **Properties** page.</span></span> <span data-ttu-id="ef87f-123">Запишите hello **имя сервера** и **имя входа администратора сервера**.</span><span class="sxs-lookup"><span data-stu-id="ef87f-123">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="ef87f-124">![Имя сервера базы данных Azure для MySQL](./media/connect-java/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="ef87f-124">![Azure Database for MySQL server name](./media/connect-java/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="ef87f-125">Если вы забыли учетные данные входа сервера, перейдите toohello **Обзор** страница hello tooview: имя пользователя администратора сервера и, при необходимости переустановить пароль hello.</span><span class="sxs-lookup"><span data-stu-id="ef87f-125">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="ef87f-126">Подключение, создание таблицы и вставка данных</span><span class="sxs-lookup"><span data-stu-id="ef87f-126">Connect, create table, and insert data</span></span>
<span data-ttu-id="ef87f-127">Hello используйте следующий код tooconnect нагрузки hello данных и с помощью функции hello с **вставить** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="ef87f-127">Use hello following code tooconnect and load hello data using hello function with an **INSERT** SQL statement.</span></span> <span data-ttu-id="ef87f-128">Hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) в противном случае используется tooconnect tooMySQL.</span><span class="sxs-lookup"><span data-stu-id="ef87f-128">hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used tooconnect tooMySQL.</span></span> <span data-ttu-id="ef87f-129">Методы [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) и execute(), используемые toodrop и создайте таблицу hello.</span><span class="sxs-lookup"><span data-stu-id="ef87f-129">Methods [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) and execute() are used toodrop and create hello table.</span></span> <span data-ttu-id="ef87f-130">Объект prepareStatement Hello является команды insert hello используется toobuild с setString() и setInt() toobind hello значениями параметров.</span><span class="sxs-lookup"><span data-stu-id="ef87f-130">hello prepareStatement object is used toobuild hello insert commands, with setString() and setInt() toobind hello parameter values.</span></span> <span data-ttu-id="ef87f-131">Метод executeUpdate() выполняет команду hello для каждого набора параметров tooinsert hello значений.</span><span class="sxs-lookup"><span data-stu-id="ef87f-131">Method executeUpdate() runs hello command for each set of parameters tooinsert hello values.</span></span> 

<span data-ttu-id="ef87f-132">Замените hello узла, базы данных, пользователя и пароль параметры hello значения, заданные при создании собственного сервера и базы данных.</span><span class="sxs-lookup"><span data-stu-id="ef87f-132">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class CreateTableInsertRows {

    public static void main (String[] args)  throws Exception
    {
        // Initialize connection variables. 
        String host = "myserver4demo.mysql.database.azure.com";
        String database = "quickstartdb";
        String user = "myadmin@myserver4demo";
        String password = "<server_admin_password>";

        // check that hello driver is installed
        try
        {
            Class.forName("com.mysql.jdbc.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("MySQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("MySQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:mysql://%s/%s", host, database);

            // Set connection properties.
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("useSSL", "true");
            properties.setProperty("verifyServerCertificate", "true");
            properties.setProperty("requireSSL", "false");

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

## <a name="read-data"></a><span data-ttu-id="ef87f-133">Считывание данных</span><span class="sxs-lookup"><span data-stu-id="ef87f-133">Read data</span></span>
<span data-ttu-id="ef87f-134">Используйте hello следующий код tooread hello данных с помощью **ВЫБЕРИТЕ** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="ef87f-134">Use hello following code tooread hello data with a **SELECT** SQL statement.</span></span> <span data-ttu-id="ef87f-135">Hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) в противном случае используется tooconnect tooMySQL.</span><span class="sxs-lookup"><span data-stu-id="ef87f-135">hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used tooconnect tooMySQL.</span></span> <span data-ttu-id="ef87f-136">Здравствуйте, методы [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) и executeQuery(), используемые tooconnect и выполните инструкцию select hello.</span><span class="sxs-lookup"><span data-stu-id="ef87f-136">hello methods [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) and executeQuery() are used tooconnect and run hello select statement.</span></span> <span data-ttu-id="ef87f-137">результаты Hello обрабатываются с использованием [ResultSet](https://docs.oracle.com/javase/tutorial/jdbc/basics/retrieving.html) объекта.</span><span class="sxs-lookup"><span data-stu-id="ef87f-137">hello results are processed using a [ResultSet](https://docs.oracle.com/javase/tutorial/jdbc/basics/retrieving.html) object.</span></span> 

<span data-ttu-id="ef87f-138">Замените hello узла, базы данных, пользователя и пароль параметры hello значения, заданные при создании собственного сервера и базы данных.</span><span class="sxs-lookup"><span data-stu-id="ef87f-138">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class ReadTable {

    public static void main (String[] args)  throws Exception
    {
        // Initialize connection variables.
        String host = "myserver4demo.mysql.database.azure.com";
        String database = "quickstartdb";
        String user = "myadmin@myserver4demo";
        String password = "<server_admin_password>";

        // check that hello driver is installed
        try
        {
            Class.forName("com.mysql.jdbc.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("MySQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("MySQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:mysql://%s/%s", host, database);

            // Set connection properties.
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("useSSL", "true");
            properties.setProperty("verifyServerCertificate", "true");
            properties.setProperty("requireSSL", "false");
            
            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed toocreate connection toodatabase", e);
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
                throw new SQLException("Encountered an error when executing given sql statement", e);
            }       
        }
        else {
            System.out.println("Failed toocreate connection toodatabase."); 
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="update-data"></a><span data-ttu-id="ef87f-139">Обновление данных</span><span class="sxs-lookup"><span data-stu-id="ef87f-139">Update data</span></span>
<span data-ttu-id="ef87f-140">Используйте hello следующий код toochange hello данных с помощью **обновление** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="ef87f-140">Use hello following code toochange hello data with an **UPDATE** SQL statement.</span></span> <span data-ttu-id="ef87f-141">Hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) в противном случае используется tooconnect tooMySQL.</span><span class="sxs-lookup"><span data-stu-id="ef87f-141">hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used tooconnect tooMySQL.</span></span> <span data-ttu-id="ef87f-142">Здравствуйте, методы [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) и executeUpdate() используется tooprepare и выполняются инструкции update hello.</span><span class="sxs-lookup"><span data-stu-id="ef87f-142">hello methods [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) and executeUpdate() are used tooprepare and run hello update statement.</span></span> 

<span data-ttu-id="ef87f-143">Замените hello узла, базы данных, пользователя и пароль параметры hello значения, заданные при создании собственного сервера и базы данных.</span><span class="sxs-lookup"><span data-stu-id="ef87f-143">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class UpdateTable {
    public static void main (String[] args)  throws Exception
    {
        // Initialize connection variables. 
        String host = "myserver4demo.mysql.database.azure.com";
        String database = "quickstartdb";
        String user = "myadmin@myserver4demo";
        String password = "<server_admin_password>";

        // check that hello driver is installed
        try
        {
            Class.forName("com.mysql.jdbc.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("MySQL JDBC driver NOT detected in library path.", e);
        }
        System.out.println("MySQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:mysql://%s/%s", host, database);
            
            // set up hello connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("useSSL", "true");
            properties.setProperty("verifyServerCertificate", "true");
            properties.setProperty("requireSSL", "false");

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

## <a name="delete-data"></a><span data-ttu-id="ef87f-144">Удаление данных</span><span class="sxs-lookup"><span data-stu-id="ef87f-144">Delete data</span></span>
<span data-ttu-id="ef87f-145">Используйте hello следующий код tooremove данных с помощью **удалить** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="ef87f-145">Use hello following code tooremove data with a **DELETE** SQL statement.</span></span> <span data-ttu-id="ef87f-146">Hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) в противном случае используется tooconnect tooMySQL.</span><span class="sxs-lookup"><span data-stu-id="ef87f-146">hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used tooconnect tooMySQL.</span></span>  <span data-ttu-id="ef87f-147">Здравствуйте, методы [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) и executeUpdate() используется tooprepare и выполняются инструкции update hello.</span><span class="sxs-lookup"><span data-stu-id="ef87f-147">hello methods [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) and executeUpdate() are used tooprepare and run hello update statement.</span></span> 

<span data-ttu-id="ef87f-148">Замените hello узла, базы данных, пользователя и пароль параметры hello значения, заданные при создании собственного сервера и базы данных.</span><span class="sxs-lookup"><span data-stu-id="ef87f-148">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class DeleteTable {
    public static void main (String[] args)  throws Exception
    {
        // Initialize connection variables.
        String host = "myserver4demo.mysql.database.azure.com";
        String database = "quickstartdb";
        String user = "myadmin@myserver4demo";
        String password = "<server_admin_password>";
        
        // check that hello driver is installed
        try
        {
            Class.forName("com.mysql.jdbc.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("MySQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("MySQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:mysql://%s/%s", host, database);
            
            // set up hello connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("useSSL", "true");
            properties.setProperty("verifyServerCertificate", "true");
            properties.setProperty("requireSSL", "false");
            
            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed toocreate connection toodatabase", e);
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

## <a name="next-steps"></a><span data-ttu-id="ef87f-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ef87f-149">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="ef87f-150">Перенести вашей tooAzure базы данных MySQL базы данных MySQL с помощью дампа и восстановления</span><span class="sxs-lookup"><span data-stu-id="ef87f-150">Migrate your MySQL database tooAzure Database for MySQL using dump and restore</span></span>](concepts-migrate-dump-restore.md)
