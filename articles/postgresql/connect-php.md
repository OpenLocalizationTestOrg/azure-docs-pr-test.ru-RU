---
title: "aaaConnect tooAzure базы данных PostgreSQL, с помощью PHP | Документы Microsoft"
description: "Это краткое руководство содержит пример кода PHP можно использовать tooconnect и запроса данных из базы данных Azure для PostgreSQL."
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
ms.openlocfilehash: 008505e837e37cb8c7fea3fc164b3446c3580e46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-php-tooconnect-and-query-data"></a><span data-ttu-id="225e3-103">База данных Azure для PostgreSQL: использование PHP tooconnect и запроса данных</span><span class="sxs-lookup"><span data-stu-id="225e3-103">Azure Database for PostgreSQL: Use PHP tooconnect and query data</span></span>
<span data-ttu-id="225e3-104">Краткого руководства показано, как tooconnect tooan Azure этой базы данных с помощью PostgreSQL [PHP](http://php.net/manual/intro-whatis.php) приложения.</span><span class="sxs-lookup"><span data-stu-id="225e3-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using a [PHP](http://php.net/manual/intro-whatis.php) application.</span></span> <span data-ttu-id="225e3-105">Показано, как tooquery инструкций SQL toouse, вставка, обновление и удаление данных в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="225e3-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="225e3-106">В этой статье предполагается, что вы знакомы с разработки приложений с использованием PHP, но, чтобы новый tooworking с базой данных Azure для PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="225e3-106">This article assumes you are familiar with development using PHP, but that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="225e3-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="225e3-107">Prerequisites</span></span>
<span data-ttu-id="225e3-108">Это краткое руководство использует ресурсы hello, созданные в любой из этих руководствах по в качестве отправной точки.</span><span class="sxs-lookup"><span data-stu-id="225e3-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="225e3-109">Создание базы данных с помощью портала</span><span class="sxs-lookup"><span data-stu-id="225e3-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="225e3-110">Создание базы данных с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="225e3-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

## <a name="install-php"></a><span data-ttu-id="225e3-111">Установка PHP</span><span class="sxs-lookup"><span data-stu-id="225e3-111">Install PHP</span></span>
<span data-ttu-id="225e3-112">Установите PHP на своем сервере или создайте [веб-приложение](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) Azure с PHP.</span><span class="sxs-lookup"><span data-stu-id="225e3-112">Install PHP on your own server, or create an Azure [web app](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) that includes PHP.</span></span>

### <a name="windows"></a><span data-ttu-id="225e3-113">Windows</span><span class="sxs-lookup"><span data-stu-id="225e3-113">Windows</span></span>
- <span data-ttu-id="225e3-114">Скачайте [PHP 7.1.4 (x64) непотокобезопасной версии](http://windows.php.net/download#php-7.1).</span><span class="sxs-lookup"><span data-stu-id="225e3-114">Download [PHP 7.1.4 non-thread safe (x64) version](http://windows.php.net/download#php-7.1)</span></span>
- <span data-ttu-id="225e3-115">Установить PHP и ссылаться toohello [руководство по PHP](http://php.net/manual/install.windows.php) для дальнейшей настройки</span><span class="sxs-lookup"><span data-stu-id="225e3-115">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.windows.php) for further configuration</span></span>
- <span data-ttu-id="225e3-116">Hello код использует hello **pgsql** класса (ext/php_pgsql.dll), включенный в hello установки PHP.</span><span class="sxs-lookup"><span data-stu-id="225e3-116">hello code uses hello **pgsql** class (ext/php_pgsql.dll)  that is included in hello PHP installation.</span></span> 
- <span data-ttu-id="225e3-117">Включена hello **pgsql** расширения путем изменения файла конфигурации php.ini hello, как правило, расположенный `C:\Program Files\PHP\v7.1\php.ini`.</span><span class="sxs-lookup"><span data-stu-id="225e3-117">Enabled hello **pgsql** extension by editing hello php.ini configuration file, typically located at `C:\Program Files\PHP\v7.1\php.ini`.</span></span> <span data-ttu-id="225e3-118">файл конфигурации Hello должен содержать строки с текстом hello `extension=php_pgsql.so`.</span><span class="sxs-lookup"><span data-stu-id="225e3-118">hello configuration file should contain a line with hello text `extension=php_pgsql.so`.</span></span> <span data-ttu-id="225e3-119">Если он не отображается, добавьте текст hello и сохраните файл hello.</span><span class="sxs-lookup"><span data-stu-id="225e3-119">If it is not shown, add hello text and save hello file.</span></span> <span data-ttu-id="225e3-120">Если текст hello присутствует, но комментариями с префиксом точкой с запятой, раскомментируйте текста hello, удалив hello точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="225e3-120">If hello text is present, but commented with a semicolon prefix, uncomment hello text by removing hello semicolon.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="225e3-121">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="225e3-121">Linux (Ubuntu)</span></span>
- <span data-ttu-id="225e3-122">Скачайте [PHP 7.1.4 (x64) непотокобезопасной версии](http://php.net/downloads.php).</span><span class="sxs-lookup"><span data-stu-id="225e3-122">Download [PHP 7.1.4 non-thread safe (x64) version](http://php.net/downloads.php)</span></span> 
- <span data-ttu-id="225e3-123">Установить PHP и ссылаться toohello [руководство по PHP](http://php.net/manual/install.unix.php) для дальнейшей настройки</span><span class="sxs-lookup"><span data-stu-id="225e3-123">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.unix.php) for further configuration</span></span>
- <span data-ttu-id="225e3-124">Hello код использует hello **pgsql** класса (php_pgsql.so).</span><span class="sxs-lookup"><span data-stu-id="225e3-124">hello code uses hello **pgsql** class (php_pgsql.so).</span></span> <span data-ttu-id="225e3-125">Установите его, выполнив команду `sudo apt-get install php-pgsql`.</span><span class="sxs-lookup"><span data-stu-id="225e3-125">Install it by running `sudo apt-get install php-pgsql`.</span></span>
- <span data-ttu-id="225e3-126">Включена hello **pgsql** расширения путем редактирования hello `/etc/php/7.0/mods-available/pgsql.ini` файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="225e3-126">Enabled hello **pgsql** extension by editing hello `/etc/php/7.0/mods-available/pgsql.ini` configuration file.</span></span> <span data-ttu-id="225e3-127">файл конфигурации Hello должен содержать строки с текстом hello `extension=php_pgsql.so`.</span><span class="sxs-lookup"><span data-stu-id="225e3-127">hello configuration file should contain a line with hello text `extension=php_pgsql.so`.</span></span> <span data-ttu-id="225e3-128">Если он не отображается, добавьте текст hello и сохраните файл hello.</span><span class="sxs-lookup"><span data-stu-id="225e3-128">If it is not shown, add hello text and save hello file.</span></span> <span data-ttu-id="225e3-129">Если текст hello присутствует, но комментариями с префиксом точкой с запятой, раскомментируйте текста hello, удалив hello точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="225e3-129">If hello text is present, but commented with a semicolon prefix, uncomment hello text by removing hello semicolon.</span></span>

### <a name="macos"></a><span data-ttu-id="225e3-130">MacOS</span><span class="sxs-lookup"><span data-stu-id="225e3-130">MacOS</span></span>
- <span data-ttu-id="225e3-131">Скачайте [PHP версии 7.1.4](http://php.net/downloads.php).</span><span class="sxs-lookup"><span data-stu-id="225e3-131">Download [PHP 7.1.4 version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="225e3-132">Установить PHP и ссылаться toohello [руководство по PHP](http://php.net/manual/install.macosx.php) для дальнейшей настройки</span><span class="sxs-lookup"><span data-stu-id="225e3-132">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.macosx.php) for further configuration</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="225e3-133">Получение сведений о подключении</span><span class="sxs-lookup"><span data-stu-id="225e3-133">Get connection information</span></span>
<span data-ttu-id="225e3-134">Получите toohello tooconnect базы данных Azure для hello подключения сведения, необходимые для PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="225e3-134">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="225e3-135">Необходимо hello server полное имя и учетные данные входа.</span><span class="sxs-lookup"><span data-stu-id="225e3-135">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="225e3-136">Войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="225e3-136">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="225e3-137">Hello левого меню на портале Azure, щелкните **все ресурсы** и выполните поиск сервера hello, вы создали, таких как **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="225e3-137">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="225e3-138">Щелкните имя сервера hello **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="225e3-138">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="225e3-139">Выберите hello server **Обзор** страницы.</span><span class="sxs-lookup"><span data-stu-id="225e3-139">Select hello server's **Overview** page.</span></span> <span data-ttu-id="225e3-140">Запишите hello **имя сервера** и **имя входа администратора сервера**.</span><span class="sxs-lookup"><span data-stu-id="225e3-140">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="225e3-141">![База данных Azure для PostgreSQL. Учетные данные администратора сервера для входа](./media/connect-php/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="225e3-141">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-php/1-connection-string.png)</span></span>
5. <span data-ttu-id="225e3-142">Если вы забыли учетные данные входа сервера, перейдите toohello **Обзор** страница hello tooview: имя пользователя администратора сервера и, при необходимости переустановить пароль hello.</span><span class="sxs-lookup"><span data-stu-id="225e3-142">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="225e3-143">Подключение и создание таблицы</span><span class="sxs-lookup"><span data-stu-id="225e3-143">Connect and create a table</span></span>
<span data-ttu-id="225e3-144">Используйте следующие hello кода tooconnect и создание таблицы с помощью **CREATE TABLE** инструкции SQL, за которым следует **INSERT INTO** строк tooadd инструкций SQL в таблицу hello.</span><span class="sxs-lookup"><span data-stu-id="225e3-144">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements tooadd rows into hello table.</span></span>

<span data-ttu-id="225e3-145">Здравствуйте, способ вызова кода [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure базы данных PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="225e3-145">hello code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="225e3-146">Затем он вызывает метод [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun несколько раз несколько команд и [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello сведений, если каждый раз произошла ошибка.</span><span class="sxs-lookup"><span data-stu-id="225e3-146">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) several times toorun several commands, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello details if an error occurred each time.</span></span> <span data-ttu-id="225e3-147">Затем он вызывает метод [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello соединения.</span><span class="sxs-lookup"><span data-stu-id="225e3-147">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello connection.</span></span>

<span data-ttu-id="225e3-148">Замените hello `$host`, `$database`, `$user`, и `$password` параметры собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="225e3-148">Replace hello `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password") 
        or die("Failed toocreate connection toodatabase: ". pg_last_error(). "<br/>");
    print "Successfully created connection toodatabase.<br/>";

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

## <a name="read-data"></a><span data-ttu-id="225e3-149">Считывание данных</span><span class="sxs-lookup"><span data-stu-id="225e3-149">Read data</span></span>
<span data-ttu-id="225e3-150">Используйте следующие hello кода tooconnect и чтения данных с помощью hello **ВЫБЕРИТЕ** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="225e3-150">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

 <span data-ttu-id="225e3-151">Здравствуйте, способ вызова кода [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure базы данных PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="225e3-151">hello code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="225e3-152">Затем он вызывает метод [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun hello команды SELECT, сохранения результатов hello в результирующий набор и [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello сведений, если произошла ошибка.</span><span class="sxs-lookup"><span data-stu-id="225e3-152">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun hello SELECT command, keeping hello results in a result set, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello details if an error occurred.</span></span>  <span data-ttu-id="225e3-153">tooread hello результирующего набора, метод [pg_fetch_row()](http://php.net/manual/en/function.pg-fetch-row.php) вызывается в цикле, один раз на строку и строка hello извлекаются данные в виде массива `$row`, со значением одного данных каждого столбца в каждой позиции массива.</span><span class="sxs-lookup"><span data-stu-id="225e3-153">tooread hello result set, method [pg_fetch_row()](http://php.net/manual/en/function.pg-fetch-row.php) is called in a loop, once per row, and hello row data is retrieved in an array `$row`, with one data value per column in each array position.</span></span>  <span data-ttu-id="225e3-154">toofree hello результирующего набора, метод [pg_free_result()](http://php.net/manual/en/function.pg-free-result.php) вызывается.</span><span class="sxs-lookup"><span data-stu-id="225e3-154">toofree hello result set, method [pg_free_result()](http://php.net/manual/en/function.pg-free-result.php) is called.</span></span> <span data-ttu-id="225e3-155">Затем он вызывает метод [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello соединения.</span><span class="sxs-lookup"><span data-stu-id="225e3-155">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello connection.</span></span>

<span data-ttu-id="225e3-156">Замените hello `$host`, `$database`, `$user`, и `$password` параметры собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="225e3-156">Replace hello `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";
    
    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
                or die("Failed toocreate connection toodatabase: ". pg_last_error(). "<br/>");

    print "Successfully created connection toodatabase. <br/>";

    // Perform some SQL queries over hello connection.
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

## <a name="update-data"></a><span data-ttu-id="225e3-157">Обновление данных</span><span class="sxs-lookup"><span data-stu-id="225e3-157">Update data</span></span>
<span data-ttu-id="225e3-158">Используйте следующие hello кода tooconnect и обновления данных с помощью hello **обновление** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="225e3-158">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="225e3-159">Здравствуйте, способ вызова кода [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure базы данных PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="225e3-159">hello code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="225e3-160">Затем он вызывает метод [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun команды, и [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello сведений, если произошла ошибка.</span><span class="sxs-lookup"><span data-stu-id="225e3-160">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun a command, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello details if an error occurred.</span></span> <span data-ttu-id="225e3-161">Затем он вызывает метод [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello соединения.</span><span class="sxs-lookup"><span data-stu-id="225e3-161">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello connection.</span></span>

<span data-ttu-id="225e3-162">Замените hello `$host`, `$database`, `$user`, и `$password` параметры собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="225e3-162">Replace hello `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
                or die("Failed toocreate connection toodatabase: ". pg_last_error(). ".<br/>");

    print "Successfully created connection toodatabase. <br/>";

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


## <a name="delete-data"></a><span data-ttu-id="225e3-163">Удаление данных</span><span class="sxs-lookup"><span data-stu-id="225e3-163">Delete data</span></span>
<span data-ttu-id="225e3-164">Используйте следующие hello кода tooconnect и чтения данных с помощью hello **удалить** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="225e3-164">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

 <span data-ttu-id="225e3-165">Здравствуйте, способ вызова кода [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect слишком Azure базы данных PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="225e3-165">hello code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect too Azure Database for PostgreSQL.</span></span> <span data-ttu-id="225e3-166">Затем он вызывает метод [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun команды, и [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello сведений, если произошла ошибка.</span><span class="sxs-lookup"><span data-stu-id="225e3-166">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun a command, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello details if an error occurred.</span></span> <span data-ttu-id="225e3-167">Затем он вызывает метод [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello соединения.</span><span class="sxs-lookup"><span data-stu-id="225e3-167">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello connection.</span></span>

<span data-ttu-id="225e3-168">Замените hello `$host`, `$database`, `$user`, и `$password` параметры собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="225e3-168">Replace hello `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
            or die("Failed toocreate connection toodatabase: ". pg_last_error(). ". </br>");

    print "Successfully created connection toodatabase. <br/>";

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

## <a name="next-steps"></a><span data-ttu-id="225e3-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="225e3-169">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="225e3-170">Перенос базы данных с помощью экспорта и импорта</span><span class="sxs-lookup"><span data-stu-id="225e3-170">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
