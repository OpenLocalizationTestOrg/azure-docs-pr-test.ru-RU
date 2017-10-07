---
title: "Подключение tooAzure базы данных MySQL из PHP | Документы Microsoft"
description: "Это краткое руководство входит несколько примеров кода PHP, можно использовать tooconnect и запроса данных из базы данных Azure для MySQL."
services: mysql
author: mswutao
ms.author: wuta
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.topic: hero-article
ms.date: 07/12/2017
ms.openlocfilehash: b928748c473c1aef320ae2183f237b5b845e83f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-php-tooconnect-and-query-data"></a>База данных Azure для MySQL: использование PHP tooconnect и запроса данных
Это краткое руководство демонстрирует, как tooconnect tooan Azure этой базы данных MySQL с помощью [PHP](http://php.net/manual/intro-whatis.php) приложения. Показано, как tooquery инструкций SQL toouse, вставка, обновление и удаление данных в базе данных hello. В этой статье предполагается, что вы знакомы с разработки приложений с использованием PHP, но, чтобы новый tooworking с базой данных Azure для MySQL.

## <a name="prerequisites"></a>Предварительные требования
Это краткое руководство использует ресурсы hello, созданные в любой из этих руководствах по в качестве отправной точки.
- [Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Создание сервера базы данных Azure для MySQL с помощью портала Azure)
- [Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md) (Создание сервера базы данных Azure для MySQL с помощью Azure CLI)

## <a name="install-php"></a>Установка PHP
Установите PHP на своем сервере или создайте [веб-приложение](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) Azure с PHP.

### <a name="macos"></a>MacOS
- Скачайте [PHP версии 7.1.4](http://php.net/downloads.php).
- Установить PHP и ссылаться toohello [руководство по PHP](http://php.net/manual/install.macosx.php) для дальнейшей настройки

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
- Скачайте [PHP 7.1.4 (x64) непотокобезопасной версии](http://php.net/downloads.php).
- Установить PHP и ссылаться toohello [руководство по PHP](http://php.net/manual/install.unix.php) для дальнейшей настройки

### <a name="windows"></a>Windows
- Скачайте [PHP 7.1.4 (x64) непотокобезопасной версии](http://windows.php.net/download#php-7.1).
- Установить PHP и ссылаться toohello [руководство по PHP](http://php.net/manual/install.windows.php) для дальнейшей настройки

## <a name="get-connection-information"></a>Получение сведений о подключении
Получите toohello tooconnect базы данных Azure для hello подключения сведения, необходимые для MySQL. Необходимо hello server полное имя и учетные данные входа.

1. Войдите в toohello [портал Azure](https://portal.azure.com/).
2. Hello левой панели щелкните **все ресурсы**и выполните поиск hello сервере был создан (например, **myserver4demo**).
3. Щелкните имя сервера hello.
4. Выберите hello server **свойства** страницы. Запишите hello **имя сервера** и **имя входа администратора сервера**.
 ![Имя сервера базы данных Azure для MySQL](./media/connect-php/1_server-properties-name-login.png)
5. Если вы забыли учетные данные входа сервера, перейдите toohello **Обзор** страница hello tooview: имя пользователя администратора сервера и, при необходимости переустановить пароль hello.

## <a name="connect-and-create-a-table"></a>Подключение и создание таблицы
Используйте следующие hello кода tooconnect и создание таблицы с помощью **CREATE TABLE** инструкции SQL. 

Hello код использует hello **MySQL улучшенное расширение** класса (mysqli), включенных в PHP. Здравствуйте, методы вызова кода [mysqli_init](http://php.net/manual/mysqli.init.php) и [mysqli_real_connect](http://php.net/manual/mysqli.real-connect.php) tooconnect tooMySQL. Затем он вызывает метод [mysqli_query](http://php.net/manual/mysqli.query.php) toorun hello запроса. Затем он вызывает метод [mysqli_close](http://php.net/manual/mysqli.close.php) tooclose hello соединения.

Замените параметры узла, имя пользователя, пароль и db_name hello собственные значения. 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

// Run hello create table query
if (mysqli_query($conn, '
CREATE TABLE Products (
`Id` INT NOT NULL AUTO_INCREMENT ,
`ProductName` VARCHAR(200) NOT NULL ,
`Color` VARCHAR(50) NOT NULL ,
`Price` DOUBLE NOT NULL ,
PRIMARY KEY (`Id`)
);
')) {
printf("Table created\n");
}

//Close hello connection
mysqli_close($conn);
?>
```

## <a name="insert-data"></a>Добавление данных
Используйте следующие hello кода tooconnect и вставка данных с помощью **вставить** инструкции SQL.

Hello код использует hello **MySQL улучшенное расширение** класса (mysqli), включенных в PHP. Hello код использует метод [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate подготовленные инструкции вставки, а затем привязывает hello параметров для каждого значения в столбце, вставленные с помощью метода [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php). Hello кода выполняется инструкция hello, с помощью метода [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) и впоследствии закрывается hello инструкцию, используя метод [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).

Замените параметры узла, имя пользователя, пароль и db_name hello собственные значения. 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

//Create an Insert prepared statement and run it
$product_name = 'BrandNewProduct';
$product_color = 'Blue';
$product_price = 15.5;
if ($stmt = mysqli_prepare($conn, "INSERT INTO Products (ProductName, Color, Price) VALUES (?, ?, ?)")) {
mysqli_stmt_bind_param($stmt, 'ssd', $product_name, $product_color, $product_price);
mysqli_stmt_execute($stmt);
printf("Insert: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));
mysqli_stmt_close($stmt);
}

// Close hello connection
mysqli_close($conn);
?>
```

## <a name="read-data"></a>Считывание данных
Используйте следующие hello кода tooconnect и чтения данных с помощью hello **ВЫБЕРИТЕ** инструкции SQL.  Hello код использует hello **MySQL улучшенное расширение** класса (mysqli), включенных в PHP. Hello код использует метод [mysqli_query](http://php.net/manual/mysqli.query.php) выполнения sql-запроса hello и использует [mysqli_fetch_assoc](http://php.net/manual/mysqli-result.fetch-assoc.php) toofetch метод hello результирующие строки.

Замените параметры узла, имя пользователя, пароль и db_name hello собственные значения. 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

//Run hello Select query
printf("Reading data from table: \n");
$res = mysqli_query($conn, 'SELECT * FROM Products');
while ($row = mysqli_fetch_assoc($res)) {
var_dump($row);
}

//Close hello connection
mysqli_close($conn);
?>
```

## <a name="update-data"></a>Обновление данных
Используйте следующие hello кода tooconnect и обновления данных с помощью hello **обновление** инструкции SQL.

Hello код использует hello **MySQL улучшенное расширение** класса (mysqli), включенных в PHP. Hello код использует метод [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate инструкцию обновления подготовленного привязывается hello параметров для каждого обновляемого столбца значения, с помощью метода [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php). Hello кода выполняется инструкция hello, с помощью метода [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) и впоследствии закрывается hello инструкцию, используя метод [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).

Замените параметры узла, имя пользователя, пароль и db_name hello собственные значения. 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

//Run hello Update statement
$product_name = 'BrandNewProduct';
$new_product_price = 15.1;
if ($stmt = mysqli_prepare($conn, "UPDATE Products SET Price = ? WHERE ProductName = ?")) {
mysqli_stmt_bind_param($stmt, 'ds', $new_product_price, $product_name);
mysqli_stmt_execute($stmt);
printf("Update: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));

//Close hello connection
mysqli_stmt_close($stmt);
}

mysqli_close($conn);
?>
```


## <a name="delete-data"></a>Удаление данных
Используйте следующие hello кода tooconnect и чтения данных с помощью hello **удалить** инструкции SQL. 

Hello код использует hello **MySQL улучшенное расширение** класса (mysqli), включенных в PHP. Hello код использует метод [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate подготовленного инструкция delete, а затем привязывает hello параметры для hello где предложения в инструкции hello, с помощью метода [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php). Hello кода выполняется инструкция hello, с помощью метода [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) и впоследствии закрывается hello инструкцию, используя метод [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).

Замените параметры узла, имя пользователя, пароль и db_name hello собственные значения. 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

//Run hello Delete statement
$product_name = 'BrandNewProduct';
if ($stmt = mysqli_prepare($conn, "DELETE FROM Products WHERE ProductName = ?")) {
mysqli_stmt_bind_param($stmt, 's', $product_name);
mysqli_stmt_execute($stmt);
printf("Delete: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));
mysqli_stmt_close($stmt);
}

//Close hello connection
mysqli_close($conn);
?>
```

## <a name="next-steps"></a>Дальнейшие действия
> [!div class="nextstepaction"]
> [Создание веб-приложения PHP в Azure с подключением к базе данных MySQL](../app-service-web/app-service-web-tutorial-php-mysql.md?toc=%2fazure%2fmysql%2ftoc.json)
