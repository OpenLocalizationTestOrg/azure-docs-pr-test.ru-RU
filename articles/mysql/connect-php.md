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
# <a name="azure-database-for-mysql-use-php-tooconnect-and-query-data"></a><span data-ttu-id="5286a-103">База данных Azure для MySQL: использование PHP tooconnect и запроса данных</span><span class="sxs-lookup"><span data-stu-id="5286a-103">Azure Database for MySQL: Use PHP tooconnect and query data</span></span>
<span data-ttu-id="5286a-104">Это краткое руководство демонстрирует, как tooconnect tooan Azure этой базы данных MySQL с помощью [PHP](http://php.net/manual/intro-whatis.php) приложения.</span><span class="sxs-lookup"><span data-stu-id="5286a-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using a [PHP](http://php.net/manual/intro-whatis.php) application.</span></span> <span data-ttu-id="5286a-105">Показано, как tooquery инструкций SQL toouse, вставка, обновление и удаление данных в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="5286a-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="5286a-106">В этой статье предполагается, что вы знакомы с разработки приложений с использованием PHP, но, чтобы новый tooworking с базой данных Azure для MySQL.</span><span class="sxs-lookup"><span data-stu-id="5286a-106">This article assumes you are familiar with development using PHP, but that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5286a-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5286a-107">Prerequisites</span></span>
<span data-ttu-id="5286a-108">Это краткое руководство использует ресурсы hello, созданные в любой из этих руководствах по в качестве отправной точки.</span><span class="sxs-lookup"><span data-stu-id="5286a-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- <span data-ttu-id="5286a-109">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Создание сервера базы данных Azure для MySQL с помощью портала Azure)</span><span class="sxs-lookup"><span data-stu-id="5286a-109">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md)</span></span>
- <span data-ttu-id="5286a-110">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md) (Создание сервера базы данных Azure для MySQL с помощью Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="5286a-110">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md)</span></span>

## <a name="install-php"></a><span data-ttu-id="5286a-111">Установка PHP</span><span class="sxs-lookup"><span data-stu-id="5286a-111">Install PHP</span></span>
<span data-ttu-id="5286a-112">Установите PHP на своем сервере или создайте [веб-приложение](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) Azure с PHP.</span><span class="sxs-lookup"><span data-stu-id="5286a-112">Install PHP on your own server, or create an Azure [web app](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) that includes PHP.</span></span>

### <a name="macos"></a><span data-ttu-id="5286a-113">MacOS</span><span class="sxs-lookup"><span data-stu-id="5286a-113">MacOS</span></span>
- <span data-ttu-id="5286a-114">Скачайте [PHP версии 7.1.4](http://php.net/downloads.php).</span><span class="sxs-lookup"><span data-stu-id="5286a-114">Download [PHP 7.1.4 version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="5286a-115">Установить PHP и ссылаться toohello [руководство по PHP](http://php.net/manual/install.macosx.php) для дальнейшей настройки</span><span class="sxs-lookup"><span data-stu-id="5286a-115">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.macosx.php) for further configuration</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="5286a-116">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="5286a-116">Linux (Ubuntu)</span></span>
- <span data-ttu-id="5286a-117">Скачайте [PHP 7.1.4 (x64) непотокобезопасной версии](http://php.net/downloads.php).</span><span class="sxs-lookup"><span data-stu-id="5286a-117">Download [PHP 7.1.4 non-thread safe (x64) version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="5286a-118">Установить PHP и ссылаться toohello [руководство по PHP](http://php.net/manual/install.unix.php) для дальнейшей настройки</span><span class="sxs-lookup"><span data-stu-id="5286a-118">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.unix.php) for further configuration</span></span>

### <a name="windows"></a><span data-ttu-id="5286a-119">Windows</span><span class="sxs-lookup"><span data-stu-id="5286a-119">Windows</span></span>
- <span data-ttu-id="5286a-120">Скачайте [PHP 7.1.4 (x64) непотокобезопасной версии](http://windows.php.net/download#php-7.1).</span><span class="sxs-lookup"><span data-stu-id="5286a-120">Download [PHP 7.1.4 non-thread safe (x64) version](http://windows.php.net/download#php-7.1)</span></span>
- <span data-ttu-id="5286a-121">Установить PHP и ссылаться toohello [руководство по PHP](http://php.net/manual/install.windows.php) для дальнейшей настройки</span><span class="sxs-lookup"><span data-stu-id="5286a-121">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.windows.php) for further configuration</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="5286a-122">Получение сведений о подключении</span><span class="sxs-lookup"><span data-stu-id="5286a-122">Get connection information</span></span>
<span data-ttu-id="5286a-123">Получите toohello tooconnect базы данных Azure для hello подключения сведения, необходимые для MySQL.</span><span class="sxs-lookup"><span data-stu-id="5286a-123">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="5286a-124">Необходимо hello server полное имя и учетные данные входа.</span><span class="sxs-lookup"><span data-stu-id="5286a-124">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="5286a-125">Войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5286a-125">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="5286a-126">Hello левой панели щелкните **все ресурсы**и выполните поиск hello сервере был создан (например, **myserver4demo**).</span><span class="sxs-lookup"><span data-stu-id="5286a-126">In hello left pane, click **All resources**, and then search for hello server you have created (for example, **myserver4demo**).</span></span>
3. <span data-ttu-id="5286a-127">Щелкните имя сервера hello.</span><span class="sxs-lookup"><span data-stu-id="5286a-127">Click hello server name.</span></span>
4. <span data-ttu-id="5286a-128">Выберите hello server **свойства** страницы.</span><span class="sxs-lookup"><span data-stu-id="5286a-128">Select hello server's **Properties** page.</span></span> <span data-ttu-id="5286a-129">Запишите hello **имя сервера** и **имя входа администратора сервера**.</span><span class="sxs-lookup"><span data-stu-id="5286a-129">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="5286a-130">![Имя сервера базы данных Azure для MySQL](./media/connect-php/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="5286a-130">![Azure Database for MySQL server name](./media/connect-php/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="5286a-131">Если вы забыли учетные данные входа сервера, перейдите toohello **Обзор** страница hello tooview: имя пользователя администратора сервера и, при необходимости переустановить пароль hello.</span><span class="sxs-lookup"><span data-stu-id="5286a-131">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="5286a-132">Подключение и создание таблицы</span><span class="sxs-lookup"><span data-stu-id="5286a-132">Connect and create a table</span></span>
<span data-ttu-id="5286a-133">Используйте следующие hello кода tooconnect и создание таблицы с помощью **CREATE TABLE** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="5286a-133">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement.</span></span> 

<span data-ttu-id="5286a-134">Hello код использует hello **MySQL улучшенное расширение** класса (mysqli), включенных в PHP.</span><span class="sxs-lookup"><span data-stu-id="5286a-134">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="5286a-135">Здравствуйте, методы вызова кода [mysqli_init](http://php.net/manual/mysqli.init.php) и [mysqli_real_connect](http://php.net/manual/mysqli.real-connect.php) tooconnect tooMySQL.</span><span class="sxs-lookup"><span data-stu-id="5286a-135">hello code call methods [mysqli_init](http://php.net/manual/mysqli.init.php) and [mysqli_real_connect](http://php.net/manual/mysqli.real-connect.php) tooconnect tooMySQL.</span></span> <span data-ttu-id="5286a-136">Затем он вызывает метод [mysqli_query](http://php.net/manual/mysqli.query.php) toorun hello запроса.</span><span class="sxs-lookup"><span data-stu-id="5286a-136">Then it calls method [mysqli_query](http://php.net/manual/mysqli.query.php) toorun hello query.</span></span> <span data-ttu-id="5286a-137">Затем он вызывает метод [mysqli_close](http://php.net/manual/mysqli.close.php) tooclose hello соединения.</span><span class="sxs-lookup"><span data-stu-id="5286a-137">Then it calls method [mysqli_close](http://php.net/manual/mysqli.close.php) tooclose hello connection.</span></span>

<span data-ttu-id="5286a-138">Замените параметры узла, имя пользователя, пароль и db_name hello собственные значения.</span><span class="sxs-lookup"><span data-stu-id="5286a-138">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

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

## <a name="insert-data"></a><span data-ttu-id="5286a-139">Добавление данных</span><span class="sxs-lookup"><span data-stu-id="5286a-139">Insert data</span></span>
<span data-ttu-id="5286a-140">Используйте следующие hello кода tooconnect и вставка данных с помощью **вставить** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="5286a-140">Use hello following code tooconnect and insert data using an **INSERT** SQL statement.</span></span>

<span data-ttu-id="5286a-141">Hello код использует hello **MySQL улучшенное расширение** класса (mysqli), включенных в PHP.</span><span class="sxs-lookup"><span data-stu-id="5286a-141">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="5286a-142">Hello код использует метод [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate подготовленные инструкции вставки, а затем привязывает hello параметров для каждого значения в столбце, вставленные с помощью метода [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span><span class="sxs-lookup"><span data-stu-id="5286a-142">hello code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate a prepared insert statement, then binds hello parameters for each inserted column value using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="5286a-143">Hello кода выполняется инструкция hello, с помощью метода [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) и впоследствии закрывается hello инструкцию, используя метод [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span><span class="sxs-lookup"><span data-stu-id="5286a-143">hello code runs hello statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes hello statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="5286a-144">Замените параметры узла, имя пользователя, пароль и db_name hello собственные значения.</span><span class="sxs-lookup"><span data-stu-id="5286a-144">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

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

## <a name="read-data"></a><span data-ttu-id="5286a-145">Считывание данных</span><span class="sxs-lookup"><span data-stu-id="5286a-145">Read data</span></span>
<span data-ttu-id="5286a-146">Используйте следующие hello кода tooconnect и чтения данных с помощью hello **ВЫБЕРИТЕ** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="5286a-146">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span>  <span data-ttu-id="5286a-147">Hello код использует hello **MySQL улучшенное расширение** класса (mysqli), включенных в PHP.</span><span class="sxs-lookup"><span data-stu-id="5286a-147">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="5286a-148">Hello код использует метод [mysqli_query](http://php.net/manual/mysqli.query.php) выполнения sql-запроса hello и использует [mysqli_fetch_assoc](http://php.net/manual/mysqli-result.fetch-assoc.php) toofetch метод hello результирующие строки.</span><span class="sxs-lookup"><span data-stu-id="5286a-148">hello code uses method [mysqli_query](http://php.net/manual/mysqli.query.php) perform hello sql query, and uses [mysqli_fetch_assoc](http://php.net/manual/mysqli-result.fetch-assoc.php) method toofetch hello resulting rows.</span></span>

<span data-ttu-id="5286a-149">Замените параметры узла, имя пользователя, пароль и db_name hello собственные значения.</span><span class="sxs-lookup"><span data-stu-id="5286a-149">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

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

## <a name="update-data"></a><span data-ttu-id="5286a-150">Обновление данных</span><span class="sxs-lookup"><span data-stu-id="5286a-150">Update data</span></span>
<span data-ttu-id="5286a-151">Используйте следующие hello кода tooconnect и обновления данных с помощью hello **обновление** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="5286a-151">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="5286a-152">Hello код использует hello **MySQL улучшенное расширение** класса (mysqli), включенных в PHP.</span><span class="sxs-lookup"><span data-stu-id="5286a-152">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="5286a-153">Hello код использует метод [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate инструкцию обновления подготовленного привязывается hello параметров для каждого обновляемого столбца значения, с помощью метода [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span><span class="sxs-lookup"><span data-stu-id="5286a-153">hello code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate a prepared update statement, then binds hello parameters for each updated column value using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="5286a-154">Hello кода выполняется инструкция hello, с помощью метода [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) и впоследствии закрывается hello инструкцию, используя метод [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span><span class="sxs-lookup"><span data-stu-id="5286a-154">hello code runs hello statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes hello statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="5286a-155">Замените параметры узла, имя пользователя, пароль и db_name hello собственные значения.</span><span class="sxs-lookup"><span data-stu-id="5286a-155">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

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


## <a name="delete-data"></a><span data-ttu-id="5286a-156">Удаление данных</span><span class="sxs-lookup"><span data-stu-id="5286a-156">Delete data</span></span>
<span data-ttu-id="5286a-157">Используйте следующие hello кода tooconnect и чтения данных с помощью hello **удалить** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="5286a-157">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="5286a-158">Hello код использует hello **MySQL улучшенное расширение** класса (mysqli), включенных в PHP.</span><span class="sxs-lookup"><span data-stu-id="5286a-158">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="5286a-159">Hello код использует метод [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate подготовленного инструкция delete, а затем привязывает hello параметры для hello где предложения в инструкции hello, с помощью метода [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span><span class="sxs-lookup"><span data-stu-id="5286a-159">hello code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate a prepared delete statement, then binds hello parameters for hello where clause in hello statement using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="5286a-160">Hello кода выполняется инструкция hello, с помощью метода [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) и впоследствии закрывается hello инструкцию, используя метод [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span><span class="sxs-lookup"><span data-stu-id="5286a-160">hello code runs hello statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes hello statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="5286a-161">Замените параметры узла, имя пользователя, пароль и db_name hello собственные значения.</span><span class="sxs-lookup"><span data-stu-id="5286a-161">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="5286a-162">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5286a-162">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="5286a-163">Создание веб-приложения PHP в Azure с подключением к базе данных MySQL</span><span class="sxs-lookup"><span data-stu-id="5286a-163">Build a PHP and MySQL web app in Azure</span></span>](../app-service-web/app-service-web-tutorial-php-mysql.md?toc=%2fazure%2fmysql%2ftoc.json)
