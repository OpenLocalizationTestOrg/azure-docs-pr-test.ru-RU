---
title: "Подключение к базе данных Azure для PostgreSQL с помощью PHP | Документация Майкрософт"
description: "В этом кратком руководстве представлен пример кода PHP, который можно использовать для подключения к базе данных Azure для PostgreSQL и запроса данных из нее."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: php
ms.topic: quickstart
ms.date: 06/29/2017
ms.openlocfilehash: ed7c92e0689bca4056401d562271e3b6b7144dcf
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-postgresql-use-php-to-connect-and-query-data"></a><span data-ttu-id="0b07a-103">База данных Azure для PostgreSQL: подключение и запрос данных с помощью PHP</span><span class="sxs-lookup"><span data-stu-id="0b07a-103">Azure Database for PostgreSQL: Use PHP to connect and query data</span></span>
<span data-ttu-id="0b07a-104">В этом кратком руководстве объясняется, как подключиться к базе данных Azure для PostgreSQL с помощью приложения [PHP](http://php.net/manual/intro-whatis.php).</span><span class="sxs-lookup"><span data-stu-id="0b07a-104">This quickstart demonstrates how to connect to an Azure Database for PostgreSQL using a [PHP](http://php.net/manual/intro-whatis.php) application.</span></span> <span data-ttu-id="0b07a-105">Здесь также показано, как использовать инструкции SQL для запроса, вставки, обновления и удаления данных в базе данных.</span><span class="sxs-lookup"><span data-stu-id="0b07a-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="0b07a-106">В этой статье предполагается, что у вас уже есть опыт разработки на PHP, но вы только начали работу с базой данных Azure для PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="0b07a-106">This article assumes you are familiar with development using PHP, but that you are new to working with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0b07a-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0b07a-107">Prerequisites</span></span>
<span data-ttu-id="0b07a-108">В качестве отправной точки в этом кратком руководстве используются ресурсы, созданные в соответствии со следующими материалами:</span><span class="sxs-lookup"><span data-stu-id="0b07a-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="0b07a-109">Создание базы данных с помощью портала</span><span class="sxs-lookup"><span data-stu-id="0b07a-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="0b07a-110">Создание базы данных с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0b07a-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

## <a name="install-php"></a><span data-ttu-id="0b07a-111">Установка PHP</span><span class="sxs-lookup"><span data-stu-id="0b07a-111">Install PHP</span></span>
<span data-ttu-id="0b07a-112">Установите PHP на своем сервере или создайте [веб-приложение](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) Azure с PHP.</span><span class="sxs-lookup"><span data-stu-id="0b07a-112">Install PHP on your own server, or create an Azure [web app](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) that includes PHP.</span></span>

### <a name="windows"></a><span data-ttu-id="0b07a-113">Windows</span><span class="sxs-lookup"><span data-stu-id="0b07a-113">Windows</span></span>
- <span data-ttu-id="0b07a-114">Скачайте [PHP 7.1.4 (x64) непотокобезопасной версии](http://windows.php.net/download#php-7.1).</span><span class="sxs-lookup"><span data-stu-id="0b07a-114">Download [PHP 7.1.4 non-thread safe (x64) version](http://windows.php.net/download#php-7.1)</span></span>
- <span data-ttu-id="0b07a-115">Установите PHP и выполните настройку согласно инструкциям в [руководстве по PHP](http://php.net/manual/install.windows.php).</span><span class="sxs-lookup"><span data-stu-id="0b07a-115">Install PHP and refer to the [PHP manual](http://php.net/manual/install.windows.php) for further configuration</span></span>
- <span data-ttu-id="0b07a-116">В коде используется класс **pgsql** (ext/php_pgsql.dll), который устанавливается с PHP.</span><span class="sxs-lookup"><span data-stu-id="0b07a-116">The code uses the **pgsql** class (ext/php_pgsql.dll)  that is included in the PHP installation.</span></span> 
- <span data-ttu-id="0b07a-117">Включите расширение **pgsql**, изменив файл конфигурации php.ini. Как правило, он находится в папке `C:\Program Files\PHP\v7.1\php.ini`.</span><span class="sxs-lookup"><span data-stu-id="0b07a-117">Enabled the **pgsql** extension by editing the php.ini configuration file, typically located at `C:\Program Files\PHP\v7.1\php.ini`.</span></span> <span data-ttu-id="0b07a-118">Файл конфигурации должен содержать строку с текстом `extension=php_pgsql.so`.</span><span class="sxs-lookup"><span data-stu-id="0b07a-118">The configuration file should contain a line with the text `extension=php_pgsql.so`.</span></span> <span data-ttu-id="0b07a-119">Если текст не отображается, добавьте его и сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="0b07a-119">If it is not shown, add the text and save the file.</span></span> <span data-ttu-id="0b07a-120">Если текст есть, но закомментирован префиксом в виде точки с запятой, раскомментируйте его, удалив точку с запятой.</span><span class="sxs-lookup"><span data-stu-id="0b07a-120">If the text is present, but commented with a semicolon prefix, uncomment the text by removing the semicolon.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="0b07a-121">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="0b07a-121">Linux (Ubuntu)</span></span>
- <span data-ttu-id="0b07a-122">Скачайте [PHP 7.1.4 (x64) непотокобезопасной версии](http://php.net/downloads.php).</span><span class="sxs-lookup"><span data-stu-id="0b07a-122">Download [PHP 7.1.4 non-thread safe (x64) version](http://php.net/downloads.php)</span></span> 
- <span data-ttu-id="0b07a-123">Установите PHP и выполните настройку согласно инструкциям в [руководстве по PHP](http://php.net/manual/install.unix.php).</span><span class="sxs-lookup"><span data-stu-id="0b07a-123">Install PHP and refer to the [PHP manual](http://php.net/manual/install.unix.php) for further configuration</span></span>
- <span data-ttu-id="0b07a-124">В коде используется класс **pgsql** (php_pgsql.so).</span><span class="sxs-lookup"><span data-stu-id="0b07a-124">The code uses the **pgsql** class (php_pgsql.so).</span></span> <span data-ttu-id="0b07a-125">Установите его, выполнив команду `sudo apt-get install php-pgsql`.</span><span class="sxs-lookup"><span data-stu-id="0b07a-125">Install it by running `sudo apt-get install php-pgsql`.</span></span>
- <span data-ttu-id="0b07a-126">Включите расширение **pgsql**, изменив файл конфигурации `/etc/php/7.0/mods-available/pgsql.ini`.</span><span class="sxs-lookup"><span data-stu-id="0b07a-126">Enabled the **pgsql** extension by editing the `/etc/php/7.0/mods-available/pgsql.ini` configuration file.</span></span> <span data-ttu-id="0b07a-127">Файл конфигурации должен содержать строку с текстом `extension=php_pgsql.so`.</span><span class="sxs-lookup"><span data-stu-id="0b07a-127">The configuration file should contain a line with the text `extension=php_pgsql.so`.</span></span> <span data-ttu-id="0b07a-128">Если текст не отображается, добавьте его и сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="0b07a-128">If it is not shown, add the text and save the file.</span></span> <span data-ttu-id="0b07a-129">Если текст есть, но закомментирован префиксом в виде точки с запятой, раскомментируйте его, удалив точку с запятой.</span><span class="sxs-lookup"><span data-stu-id="0b07a-129">If the text is present, but commented with a semicolon prefix, uncomment the text by removing the semicolon.</span></span>

### <a name="macos"></a><span data-ttu-id="0b07a-130">MacOS</span><span class="sxs-lookup"><span data-stu-id="0b07a-130">MacOS</span></span>
- <span data-ttu-id="0b07a-131">Скачайте [PHP версии 7.1.4](http://php.net/downloads.php).</span><span class="sxs-lookup"><span data-stu-id="0b07a-131">Download [PHP 7.1.4 version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="0b07a-132">Установите PHP и выполните настройку согласно инструкциям в [руководстве по PHP](http://php.net/manual/install.macosx.php).</span><span class="sxs-lookup"><span data-stu-id="0b07a-132">Install PHP and refer to the [PHP manual](http://php.net/manual/install.macosx.php) for further configuration</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="0b07a-133">Получение сведений о подключении</span><span class="sxs-lookup"><span data-stu-id="0b07a-133">Get connection information</span></span>
<span data-ttu-id="0b07a-134">Получите сведения, необходимые для подключения к базе данных Azure.для PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="0b07a-134">Get the connection information needed to connect to the Azure Database for PostgreSQL.</span></span> <span data-ttu-id="0b07a-135">Вам потребуется полное имя сервера и учетные данные для входа.</span><span class="sxs-lookup"><span data-stu-id="0b07a-135">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="0b07a-136">Войдите на [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="0b07a-136">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="0b07a-137">В меню слева на портале Azure щелкните **Все ресурсы** и выполните поиск по имени созданного сервера, например **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="0b07a-137">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="0b07a-138">Щелкните имя сервера **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="0b07a-138">Click the server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="0b07a-139">Выберите страницу **обзора** сервера.</span><span class="sxs-lookup"><span data-stu-id="0b07a-139">Select the server's **Overview** page.</span></span> <span data-ttu-id="0b07a-140">Запишите значения **имени сервера** и **имени для входа администратора сервера**.</span><span class="sxs-lookup"><span data-stu-id="0b07a-140">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="0b07a-141">![База данных Azure для PostgreSQL. Учетные данные администратора сервера для входа](./media/connect-php/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="0b07a-141">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-php/1-connection-string.png)</span></span>
5. <span data-ttu-id="0b07a-142">Если вы забыли данные для входа на сервер, перейдите на страницу **Обзор**, чтобы просмотреть имя администратора сервера и при необходимости сбросить пароль.</span><span class="sxs-lookup"><span data-stu-id="0b07a-142">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="0b07a-143">Подключение и создание таблицы</span><span class="sxs-lookup"><span data-stu-id="0b07a-143">Connect and create a table</span></span>
<span data-ttu-id="0b07a-144">Используйте приведенный ниже код для подключения и создайте таблицу с помощью инструкции SQL **CREATE TABLE**. Добавьте строки в таблицу, применив инструкцию SQL **INSERT INTO**.</span><span class="sxs-lookup"><span data-stu-id="0b07a-144">Use the following code to connect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements to add rows into the table.</span></span>

<span data-ttu-id="0b07a-145">Код вызывает метод [pg_connect()](http://php.net/manual/en/function.pg-connect.php), чтобы подключиться к базе данных Azure для PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="0b07a-145">The code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) to connect to Azure Database for PostgreSQL.</span></span> <span data-ttu-id="0b07a-146">Затем он вызывает метод [pg_query()](http://php.net/manual/en/function.pg-query.php) несколько раз, чтобы выполнить несколько команд, и метод [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php), чтобы проверить сведения, если каждое выполнение завершилось ошибкой.</span><span class="sxs-lookup"><span data-stu-id="0b07a-146">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) several times to run several commands, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) to check the details if an error occurred each time.</span></span> <span data-ttu-id="0b07a-147">После этого вызывается метод [mysqli_close](http://php.net/manual/en/function.pg-close.php), чтобы разорвать подключение.</span><span class="sxs-lookup"><span data-stu-id="0b07a-147">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) to close the connection.</span></span>

<span data-ttu-id="0b07a-148">Замените значения параметров `$host`, `$database`, `$user` и `$password` своими значениями.</span><span class="sxs-lookup"><span data-stu-id="0b07a-148">Replace the `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password") 
        or die("Failed to create connection to database: ". pg_last_error(). "<br/>");
    print "Successfully created connection to database.<br/>";

    // Drop previous table of same name if one exists.
    $query = "DROP TABLE IF EXISTS inventory;";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");
    print "Finished dropping table (if existed).<br/>";

    // Create table.
    $query = "CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");
    print "Finished creating table.<br/>";

    // Insert some data into table.
    $name = '\'banana\'';
    $quantity = 150;
    $query = "INSERT INTO inventory (name, quantity) VALUES ($1, $2);";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");

    $name = '\'orange\'';
    $quantity = 154;
    $query = "INSERT INTO inventory (name, quantity) VALUES ($name, $quantity);";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");

    $name = '\'apple\'';
    $quantity = 100;
    $query = "INSERT INTO inventory (name, quantity) VALUES ($name, $quantity);";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error()). "<br/>";

    print "Inserted 3 rows of data.<br/>";

    // Closing connection
    pg_close($connection);
?>
```

## <a name="read-data"></a><span data-ttu-id="0b07a-149">Считывание данных</span><span class="sxs-lookup"><span data-stu-id="0b07a-149">Read data</span></span>
<span data-ttu-id="0b07a-150">Используйте указанный ниже код с инструкцией SQL **SELECT** для подключения и чтения данных.</span><span class="sxs-lookup"><span data-stu-id="0b07a-150">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> 

 <span data-ttu-id="0b07a-151">Код вызывает метод [pg_connect()](http://php.net/manual/en/function.pg-connect.php), чтобы подключиться к базе данных Azure для PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="0b07a-151">The code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) to connect to Azure Database for PostgreSQL.</span></span> <span data-ttu-id="0b07a-152">Затем он вызывает метод [pg_query()](http://php.net/manual/en/function.pg-query.php) для выполнения команды SELECT, сохраняя результаты в результирующем наборе, и метод [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php), чтобы проверить сведения, если произошла ошибка.</span><span class="sxs-lookup"><span data-stu-id="0b07a-152">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) to run the SELECT command, keeping the results in a result set, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) to check the details if an error occurred.</span></span>  <span data-ttu-id="0b07a-153">Чтобы считать данные результирующего набора, в цикле вызывается метод [pg_fetch_row()](http://php.net/manual/en/function.pg-fetch-row.php) для каждой строки. Данные строки извлекаются в виде массива `$row` с одним значением данных для каждого столбца в каждой позиции массива.</span><span class="sxs-lookup"><span data-stu-id="0b07a-153">To read the result set, method [pg_fetch_row()](http://php.net/manual/en/function.pg-fetch-row.php) is called in a loop, once per row, and the row data is retrieved in an array `$row`, with one data value per column in each array position.</span></span>  <span data-ttu-id="0b07a-154">Чтобы освободить результирующий набор, вызывается метод [pg_free_result()](http://php.net/manual/en/function.pg-free-result.php).</span><span class="sxs-lookup"><span data-stu-id="0b07a-154">To free the result set, method [pg_free_result()](http://php.net/manual/en/function.pg-free-result.php) is called.</span></span> <span data-ttu-id="0b07a-155">После этого вызывается метод [mysqli_close](http://php.net/manual/en/function.pg-close.php), чтобы разорвать подключение.</span><span class="sxs-lookup"><span data-stu-id="0b07a-155">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) to close the connection.</span></span>

<span data-ttu-id="0b07a-156">Замените значения параметров `$host`, `$database`, `$user` и `$password` своими значениями.</span><span class="sxs-lookup"><span data-stu-id="0b07a-156">Replace the `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";
    
    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
                or die("Failed to create connection to database: ". pg_last_error(). "<br/>");

    print "Successfully created connection to database. <br/>";

    // Perform some SQL queries over the connection.
    $query = "SELECT * from inventory";
    $result_set = pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");
    while ($row = pg_fetch_row($result_set))
    {
        print "Data row = ($row[0], $row[1], $row[2]). <br/>";
    }

    // Free result_set
    pg_free_result($result_set);

    // Closing connection
    pg_close($connection);
?>
```

## <a name="update-data"></a><span data-ttu-id="0b07a-157">Обновление данных</span><span class="sxs-lookup"><span data-stu-id="0b07a-157">Update data</span></span>
<span data-ttu-id="0b07a-158">Используйте указанный ниже код с инструкцией SQL **UPDATE** для подключения и обновления данных.</span><span class="sxs-lookup"><span data-stu-id="0b07a-158">Use the following code to connect and update the data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="0b07a-159">Код вызывает метод [pg_connect()](http://php.net/manual/en/function.pg-connect.php), чтобы подключиться к базе данных Azure для PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="0b07a-159">The code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) to connect to Azure Database for PostgreSQL.</span></span> <span data-ttu-id="0b07a-160">Затем он вызывает метод [pg_query()](http://php.net/manual/en/function.pg-query.php), чтобы выполнить команду, и метод [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php), чтобы проверить сведения, если произошла ошибка.</span><span class="sxs-lookup"><span data-stu-id="0b07a-160">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) to run a command, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) to check the details if an error occurred.</span></span> <span data-ttu-id="0b07a-161">После этого вызывается метод [mysqli_close](http://php.net/manual/en/function.pg-close.php), чтобы разорвать подключение.</span><span class="sxs-lookup"><span data-stu-id="0b07a-161">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) to close the connection.</span></span>

<span data-ttu-id="0b07a-162">Замените значения параметров `$host`, `$database`, `$user` и `$password` своими значениями.</span><span class="sxs-lookup"><span data-stu-id="0b07a-162">Replace the `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
                or die("Failed to create connection to database: ". pg_last_error(). ".<br/>");

    print "Successfully created connection to database. <br/>";

    // Modify some data in table.
    $new_quantity = 200;
    $name = '\'banana\'';
    $query = "UPDATE inventory SET quantity = $new_quantity WHERE name = $name;";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). ".<br/>");
    print "Updated 1 row of data. </br>";

    // Closing connection
    pg_close($connection);
?>
```


## <a name="delete-data"></a><span data-ttu-id="0b07a-163">Удаление данных</span><span class="sxs-lookup"><span data-stu-id="0b07a-163">Delete data</span></span>
<span data-ttu-id="0b07a-164">Используйте указанный ниже код с инструкцией SQL **DELETE** для подключения и чтения данных.</span><span class="sxs-lookup"><span data-stu-id="0b07a-164">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> 

 <span data-ttu-id="0b07a-165">Код вызывает метод [pg_connect()](http://php.net/manual/en/function.pg-connect.php), чтобы подключиться к базе данных Azure для PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="0b07a-165">The code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) to connect to  Azure Database for PostgreSQL.</span></span> <span data-ttu-id="0b07a-166">Затем он вызывает метод [pg_query()](http://php.net/manual/en/function.pg-query.php), чтобы выполнить команду, и метод [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php), чтобы проверить сведения, если произошла ошибка.</span><span class="sxs-lookup"><span data-stu-id="0b07a-166">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) to run a command, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) to check the details if an error occurred.</span></span> <span data-ttu-id="0b07a-167">После этого вызывается метод [mysqli_close](http://php.net/manual/en/function.pg-close.php), чтобы разорвать подключение.</span><span class="sxs-lookup"><span data-stu-id="0b07a-167">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) to close the connection.</span></span>

<span data-ttu-id="0b07a-168">Замените значения параметров `$host`, `$database`, `$user` и `$password` своими значениями.</span><span class="sxs-lookup"><span data-stu-id="0b07a-168">Replace the `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
            or die("Failed to create connection to database: ". pg_last_error(). ". </br>");

    print "Successfully created connection to database. <br/>";

    // Delete some data from table.
    $name = '\'orange\'';
    $query = "DELETE FROM inventory WHERE name = $name;";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). ". <br/>");
    print "Deleted 1 row of data. <br/>";

    // Closing connection
    pg_close($connection);
?>
```

## <a name="next-steps"></a><span data-ttu-id="0b07a-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0b07a-169">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="0b07a-170">Перенос базы данных с помощью экспорта и импорта</span><span class="sxs-lookup"><span data-stu-id="0b07a-170">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
