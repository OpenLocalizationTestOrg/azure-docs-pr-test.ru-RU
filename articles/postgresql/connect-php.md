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
# <a name="azure-database-for-postgresql-use-php-tooconnect-and-query-data"></a>База данных Azure для PostgreSQL: использование PHP tooconnect и запроса данных
Краткого руководства показано, как tooconnect tooan Azure этой базы данных с помощью PostgreSQL [PHP](http://php.net/manual/intro-whatis.php) приложения. Показано, как tooquery инструкций SQL toouse, вставка, обновление и удаление данных в базе данных hello. В этой статье предполагается, что вы знакомы с разработки приложений с использованием PHP, но, чтобы новый tooworking с базой данных Azure для PostgreSQL.

## <a name="prerequisites"></a>Предварительные требования
Это краткое руководство использует ресурсы hello, созданные в любой из этих руководствах по в качестве отправной точки.
- [Создание базы данных с помощью портала](quickstart-create-server-database-portal.md)
- [Создание базы данных с помощью Azure CLI](quickstart-create-server-database-azure-cli.md)

## <a name="install-php"></a>Установка PHP
Установите PHP на своем сервере или создайте [веб-приложение](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) Azure с PHP.

### <a name="windows"></a>Windows
- Скачайте [PHP 7.1.4 (x64) непотокобезопасной версии](http://windows.php.net/download#php-7.1).
- Установить PHP и ссылаться toohello [руководство по PHP](http://php.net/manual/install.windows.php) для дальнейшей настройки
- Hello код использует hello **pgsql** класса (ext/php_pgsql.dll), включенный в hello установки PHP. 
- Включена hello **pgsql** расширения путем изменения файла конфигурации php.ini hello, как правило, расположенный `C:\Program Files\PHP\v7.1\php.ini`. файл конфигурации Hello должен содержать строки с текстом hello `extension=php_pgsql.so`. Если он не отображается, добавьте текст hello и сохраните файл hello. Если текст hello присутствует, но комментариями с префиксом точкой с запятой, раскомментируйте текста hello, удалив hello точкой с запятой.

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
- Скачайте [PHP 7.1.4 (x64) непотокобезопасной версии](http://php.net/downloads.php). 
- Установить PHP и ссылаться toohello [руководство по PHP](http://php.net/manual/install.unix.php) для дальнейшей настройки
- Hello код использует hello **pgsql** класса (php_pgsql.so). Установите его, выполнив команду `sudo apt-get install php-pgsql`.
- Включена hello **pgsql** расширения путем редактирования hello `/etc/php/7.0/mods-available/pgsql.ini` файла конфигурации. файл конфигурации Hello должен содержать строки с текстом hello `extension=php_pgsql.so`. Если он не отображается, добавьте текст hello и сохраните файл hello. Если текст hello присутствует, но комментариями с префиксом точкой с запятой, раскомментируйте текста hello, удалив hello точкой с запятой.

### <a name="macos"></a>MacOS
- Скачайте [PHP версии 7.1.4](http://php.net/downloads.php).
- Установить PHP и ссылаться toohello [руководство по PHP](http://php.net/manual/install.macosx.php) для дальнейшей настройки

## <a name="get-connection-information"></a>Получение сведений о подключении
Получите toohello tooconnect базы данных Azure для hello подключения сведения, необходимые для PostgreSQL. Необходимо hello server полное имя и учетные данные входа.

1. Войдите в toohello [портал Azure](https://portal.azure.com/).
2. Hello левого меню на портале Azure, щелкните **все ресурсы** и выполните поиск сервера hello, вы создали, таких как **mypgserver 20170401**.
3. Щелкните имя сервера hello **mypgserver 20170401**.
4. Выберите hello server **Обзор** страницы. Запишите hello **имя сервера** и **имя входа администратора сервера**.
 ![База данных Azure для PostgreSQL. Учетные данные администратора сервера для входа](./media/connect-php/1-connection-string.png)
5. Если вы забыли учетные данные входа сервера, перейдите toohello **Обзор** страница hello tooview: имя пользователя администратора сервера и, при необходимости переустановить пароль hello.

## <a name="connect-and-create-a-table"></a>Подключение и создание таблицы
Используйте следующие hello кода tooconnect и создание таблицы с помощью **CREATE TABLE** инструкции SQL, за которым следует **INSERT INTO** строк tooadd инструкций SQL в таблицу hello.

Здравствуйте, способ вызова кода [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure базы данных PostgreSQL. Затем он вызывает метод [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun несколько раз несколько команд и [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello сведений, если каждый раз произошла ошибка. Затем он вызывает метод [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello соединения.

Замените hello `$host`, `$database`, `$user`, и `$password` параметры собственными значениями. 

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

## <a name="read-data"></a>Считывание данных
Используйте следующие hello кода tooconnect и чтения данных с помощью hello **ВЫБЕРИТЕ** инструкции SQL. 

 Здравствуйте, способ вызова кода [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure базы данных PostgreSQL. Затем он вызывает метод [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun hello команды SELECT, сохранения результатов hello в результирующий набор и [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello сведений, если произошла ошибка.  tooread hello результирующего набора, метод [pg_fetch_row()](http://php.net/manual/en/function.pg-fetch-row.php) вызывается в цикле, один раз на строку и строка hello извлекаются данные в виде массива `$row`, со значением одного данных каждого столбца в каждой позиции массива.  toofree hello результирующего набора, метод [pg_free_result()](http://php.net/manual/en/function.pg-free-result.php) вызывается. Затем он вызывает метод [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello соединения.

Замените hello `$host`, `$database`, `$user`, и `$password` параметры собственными значениями. 

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

## <a name="update-data"></a>Обновление данных
Используйте следующие hello кода tooconnect и обновления данных с помощью hello **обновление** инструкции SQL.

Здравствуйте, способ вызова кода [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure базы данных PostgreSQL. Затем он вызывает метод [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun команды, и [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello сведений, если произошла ошибка. Затем он вызывает метод [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello соединения.

Замените hello `$host`, `$database`, `$user`, и `$password` параметры собственными значениями. 

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


## <a name="delete-data"></a>Удаление данных
Используйте следующие hello кода tooconnect и чтения данных с помощью hello **удалить** инструкции SQL. 

 Здравствуйте, способ вызова кода [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect слишком Azure базы данных PostgreSQL. Затем он вызывает метод [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun команды, и [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello сведений, если произошла ошибка. Затем он вызывает метод [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello соединения.

Замените hello `$host`, `$database`, `$user`, и `$password` параметры собственными значениями. 

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

## <a name="next-steps"></a>Дальнейшие действия
> [!div class="nextstepaction"]
> [Перенос базы данных с помощью экспорта и импорта](./howto-migrate-using-export-and-import.md)
