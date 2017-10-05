---
title: "Подключение к базе данных Azure для MySQL с помощью Node.js | Документация Майкрософт"
description: "В этом кратком руководстве представлены примеры кода Node.js, которые можно использовать для подключения к базе данных Azure для MySQL и запроса данных из нее."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 07/17/2017
ms.openlocfilehash: 0c0bd4b707c114d2991e5f0473a4bfbe9e463e3c
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/29/2017
---
# <a name="azure-database-for-mysql-use-nodejs-to-connect-and-query-data"></a><span data-ttu-id="a9add-103">База данных Azure для MySQL: подключение и запрос данных с помощью Node.js</span><span class="sxs-lookup"><span data-stu-id="a9add-103">Azure Database for MySQL: Use Node.js to connect and query data</span></span>
<span data-ttu-id="a9add-104">В этом кратком руководстве описывается, как подключиться к базе данных Azure для MySQL при помощи [Node.js](https://nodejs.org/) на платформе Windows, Ubuntu Linux или Mac.</span><span class="sxs-lookup"><span data-stu-id="a9add-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using [Node.js](https://nodejs.org/) from Windows, Ubuntu Linux, and Mac platforms.</span></span> <span data-ttu-id="a9add-105">Здесь также показано, как использовать инструкции SQL для запроса, вставки, обновления и удаления данных в базе данных.</span><span class="sxs-lookup"><span data-stu-id="a9add-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="a9add-106">В этой статье предполагается, что у вас уже есть опыт разработки на Node.js и вы только начали работу с базой данных Azure для MySQL.</span><span class="sxs-lookup"><span data-stu-id="a9add-106">The steps in this article assume that you are familiar with developing using Node.js, and that you are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a9add-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a9add-107">Prerequisites</span></span>
<span data-ttu-id="a9add-108">В качестве отправной точки в этом кратком руководстве используются ресурсы, созданные в соответствии со следующими материалами:</span><span class="sxs-lookup"><span data-stu-id="a9add-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- <span data-ttu-id="a9add-109">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Создание сервера базы данных Azure для MySQL с помощью портала Azure)</span><span class="sxs-lookup"><span data-stu-id="a9add-109">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md)</span></span>
- <span data-ttu-id="a9add-110">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md) (Создание сервера базы данных Azure для MySQL с помощью Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="a9add-110">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md)</span></span>

<span data-ttu-id="a9add-111">Также вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="a9add-111">You also need to:</span></span>
- <span data-ttu-id="a9add-112">установить среду выполнения [Node.js](https://nodejs.org);</span><span class="sxs-lookup"><span data-stu-id="a9add-112">Install the [Node.js](https://nodejs.org) runtime.</span></span>
- <span data-ttu-id="a9add-113">установить пакет [MySQL2](https://www.npmjs.com/package/mysql2) для подключения к MySQL из приложения Node.js.</span><span class="sxs-lookup"><span data-stu-id="a9add-113">Install [mysql2](https://www.npmjs.com/package/mysql2) package to connect to MySQL from the Node.js application.</span></span> 

## <a name="install-nodejs-and-the-mysql-connector"></a><span data-ttu-id="a9add-114">Установка Node.js и соединителя MySQL</span><span class="sxs-lookup"><span data-stu-id="a9add-114">Install Node.js and the MySQL connector</span></span>
<span data-ttu-id="a9add-115">В зависимости от используемой платформы выполните соответствующие инструкции для установки Node.js.</span><span class="sxs-lookup"><span data-stu-id="a9add-115">Depending on your platform, follow the appropriate instructions to install Node.js.</span></span> <span data-ttu-id="a9add-116">Используйте NPM, чтобы установить пакет MySQL2 и его зависимости в папку проекта.</span><span class="sxs-lookup"><span data-stu-id="a9add-116">Use npm to install the mysql2 package and its dependencies into your project folder.</span></span>

### <a name="windows"></a><span data-ttu-id="a9add-117">**Windows**</span><span class="sxs-lookup"><span data-stu-id="a9add-117">**Windows**</span></span>
1. <span data-ttu-id="a9add-118">Войдите на [страницу скачиваемых файлов Node.js](https://nodejs.org/en/download/) и выберите нужный установщик Windows.</span><span class="sxs-lookup"><span data-stu-id="a9add-118">Visit the [Node.js downloads page](https://nodejs.org/en/download/) and select your desired Windows installer option.</span></span>
2. <span data-ttu-id="a9add-119">Создайте папку локального проекта, например `nodejsmysql`.</span><span class="sxs-lookup"><span data-stu-id="a9add-119">Make a local project folder such as `nodejsmysql`.</span></span> 
3. <span data-ttu-id="a9add-120">Запустите командную строку и с помощью команды cd перейдите в папку каталога, например `cd c:\nodejsmysql\`.</span><span class="sxs-lookup"><span data-stu-id="a9add-120">Launch the command prompt and cd into the project folder, such as `cd c:\nodejsmysql\`</span></span>
4. <span data-ttu-id="a9add-121">Запустите средство NPM, чтобы установить библиотеку MySQL2 в папке проекта.</span><span class="sxs-lookup"><span data-stu-id="a9add-121">Run the NPM tool to install the mysql2 library into the project folder.</span></span>

   ```cmd
   cd c:\nodejsmysql\
   "C:\Program Files\nodejs\npm" install mysql2
   "C:\Program Files\nodejs\npm" list
   ```

5. <span data-ttu-id="a9add-122">Проверьте установку, проверив текст вывода `npm list` для `mysql2@1.3.5`.</span><span class="sxs-lookup"><span data-stu-id="a9add-122">Verify the installation by checking the `npm list` output text for `mysql2@1.3.5`.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="a9add-123">**Linux (Ubuntu)**</span><span class="sxs-lookup"><span data-stu-id="a9add-123">**Linux (Ubuntu)**</span></span>
1. <span data-ttu-id="a9add-124">Чтобы установить **Node.js** и **NPM** (диспетчер пакетов для Node.js), выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a9add-124">Run the following commands to install **Node.js** and **npm** the package manager for Node.js.</span></span>

   ```bash
   sudo apt-get install -y nodejs npm
   ```

2. <span data-ttu-id="a9add-125">Выполните следующие команды, чтобы создать папку проекта `mysqlnodejs` и установить в этой папке пакет MySQL2.</span><span class="sxs-lookup"><span data-stu-id="a9add-125">Run the following commands to make a project folder `mysqlnodejs` and install the mysql2 package into that folder.</span></span>

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```
3. <span data-ttu-id="a9add-126">Проверьте установку, проверив текст вывода списка NPM для `mysql2@1.3.5`.</span><span class="sxs-lookup"><span data-stu-id="a9add-126">Verify the installation by checking npm list output text for `mysql2@1.3.5`.</span></span>

### <a name="mac-os"></a><span data-ttu-id="a9add-127">**Mac OS**</span><span class="sxs-lookup"><span data-stu-id="a9add-127">**Mac OS**</span></span>
1. <span data-ttu-id="a9add-128">Чтобы установить **brew** (простой в использовании диспетчер пакетов для Mac OS X) и **Node.js**, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a9add-128">Enter the following commands to install **brew**, an easy-to-use package manager for Mac OS X and **Node.js**.</span></span>

   ```bash
   ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
   brew install node
   ```
2. <span data-ttu-id="a9add-129">Выполните следующие команды, чтобы создать папку проекта `mysqlnodejs` и установить в этой папке пакет MySQL2.</span><span class="sxs-lookup"><span data-stu-id="a9add-129">Run the following commands to make a project folder `mysqlnodejs` and install the mysql2 package into that folder.</span></span>

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```

3. <span data-ttu-id="a9add-130">Проверьте установку, проверив текст вывода `npm list` для `mysql2@1.3.6`.</span><span class="sxs-lookup"><span data-stu-id="a9add-130">Verify the installation by checking the `npm list` output text for `mysql2@1.3.6`.</span></span> <span data-ttu-id="a9add-131">Номера версии могут отличаться, когда будут выпущены новые обновления.</span><span class="sxs-lookup"><span data-stu-id="a9add-131">The version number may vary as new patches are released.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="a9add-132">Получение сведений о подключении</span><span class="sxs-lookup"><span data-stu-id="a9add-132">Get connection information</span></span>
<span data-ttu-id="a9add-133">Получите сведения о подключении, необходимые для подключения к базе данных Azure.для MySQL.</span><span class="sxs-lookup"><span data-stu-id="a9add-133">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="a9add-134">Вам потребуется полное имя сервера и учетные данные для входа.</span><span class="sxs-lookup"><span data-stu-id="a9add-134">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="a9add-135">Войдите на [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a9add-135">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="a9add-136">В левой области щелкните **Все ресурсы** и выполните поиск по имени созданного сервера (например, **myserver4demo**).</span><span class="sxs-lookup"><span data-stu-id="a9add-136">In the left pane, click **All resources**, and then search for the server you have created (for example, **myserver4demo**).</span></span>
3. <span data-ttu-id="a9add-137">Щелкните имя сервера **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="a9add-137">Click the server name **myserver4demo**.</span></span>
4. <span data-ttu-id="a9add-138">Откройте страницу **свойств** сервера.</span><span class="sxs-lookup"><span data-stu-id="a9add-138">Select the server's **Properties** page.</span></span> <span data-ttu-id="a9add-139">Запишите значения **имени сервера** и **имени для входа администратора сервера**.</span><span class="sxs-lookup"><span data-stu-id="a9add-139">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="a9add-140">![Имя входа для администратора сервера в базе данных Azure для MySQL](./media/connect-nodejs/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="a9add-140">![Azure Database for MySQL - Server Admin Login](./media/connect-nodejs/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="a9add-141">Если вы забыли данные для входа на сервер, перейдите на страницу **Обзор**, чтобы просмотреть имя администратора сервера и при необходимости сбросить пароль.</span><span class="sxs-lookup"><span data-stu-id="a9add-141">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="running-the-javascript-code-in-nodejs"></a><span data-ttu-id="a9add-142">Выполнение кода JavaScript в Node.js</span><span class="sxs-lookup"><span data-stu-id="a9add-142">Running the JavaScript code in Node.js</span></span>
1. <span data-ttu-id="a9add-143">Вставьте код JavaScript в текстовые файлы и сохраните его в папку проекта с расширением файла JS, например C:\nodejsmysql\createtable.js or /home/username/nodejsmysql/createtable.js.</span><span class="sxs-lookup"><span data-stu-id="a9add-143">Paste the JavaScript code into text files, and save into a project folder with file extension .js, such as C:\nodejsmysql\createtable.js or /home/username/nodejsmysql/createtable.js</span></span>
2. <span data-ttu-id="a9add-144">Запустите командную строку или оболочку Bash.</span><span class="sxs-lookup"><span data-stu-id="a9add-144">Launch the command prompt or bash shell.</span></span> <span data-ttu-id="a9add-145">Перейдите в папку проекта `cd nodejsmysql`.</span><span class="sxs-lookup"><span data-stu-id="a9add-145">Change directory into your project folder `cd nodejsmysql`.</span></span>
3. <span data-ttu-id="a9add-146">Чтобы запустить приложение, введите команду Node, за которой следует имя файла, например `node createtable.js`.</span><span class="sxs-lookup"><span data-stu-id="a9add-146">To run the application, type the node command followed by the file name, such as `node createtable.js`.</span></span>
4. <span data-ttu-id="a9add-147">В Windows, если приложение Node не указано в переменной среды PATH, может потребоваться указать полный путь, чтобы запустить приложение Node, например `"C:\Program Files\nodejs\node.exe" createtable.js`.</span><span class="sxs-lookup"><span data-stu-id="a9add-147">On Windows, if the node application is not in your environment variable path, you may need to use the full path to launch the node application, such as `"C:\Program Files\nodejs\node.exe" createtable.js`</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="a9add-148">Подключение, создание таблицы и вставка данных</span><span class="sxs-lookup"><span data-stu-id="a9add-148">Connect, create table, and insert data</span></span>
<span data-ttu-id="a9add-149">Используйте приведенный ниже код для подключения и загрузки данных с помощью инструкций SQL **CREATE TABLE** и **INSERT INTO**.</span><span class="sxs-lookup"><span data-stu-id="a9add-149">Use the following code to connect and load the data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span>

<span data-ttu-id="a9add-150">Метод [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) используется для обмена данными с сервером MySQL.</span><span class="sxs-lookup"><span data-stu-id="a9add-150">The [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used to interface with the MySQL server.</span></span> <span data-ttu-id="a9add-151">Функция [connect()](https://github.com/mysqljs/mysql#establishing-connections) используется для подключения к серверу.</span><span class="sxs-lookup"><span data-stu-id="a9add-151">The [connect()](https://github.com/mysqljs/mysql#establishing-connections) function is used to establish the connection to the server.</span></span> <span data-ttu-id="a9add-152">Функция [query()](https://github.com/mysqljs/mysql#performing-queries) используется для выполнения SQL-запроса к базе данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="a9add-152">The [query()](https://github.com/mysqljs/mysql#performing-queries) function is used to execute the SQL query against MySQL database.</span></span> 

<span data-ttu-id="a9add-153">Замените параметры `host`, `user`, `password` и `database` значениями, указанными при создании сервера и базы данных.</span><span class="sxs-lookup"><span data-stu-id="a9add-153">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'myserver4demo.mysql.database.azure.com',
    user: 'myadmin@myserver4demo',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
    if (err) { 
        console.log("!!! Cannot connect !!! Error:");
        throw err;
    }
    else
    {
       console.log("Connection established.");
           queryDatabase();
    }   
});

function queryDatabase(){
       conn.query('DROP TABLE IF EXISTS inventory;', function (err, results, fields) { 
            if (err) throw err; 
            console.log('Dropped inventory table if existed.');
        })
       conn.query('CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);', 
            function (err, results, fields) {
                if (err) throw err;
            console.log('Created inventory table.');
        })
       conn.query('INSERT INTO inventory (name, quantity) VALUES (?, ?);', ['banana', 150], 
            function (err, results, fields) {
                if (err) throw err;
            else console.log('Inserted ' + results.affectedRows + ' row(s).');
        })
       conn.query('INSERT INTO inventory (name, quantity) VALUES (?, ?);', ['orange', 154], 
            function (err, results, fields) {
                if (err) throw err;
            console.log('Inserted ' + results.affectedRows + ' row(s).');
        })
       conn.query('INSERT INTO inventory (name, quantity) VALUES (?, ?);', ['apple', 100], 
        function (err, results, fields) {
                if (err) throw err;
            console.log('Inserted ' + results.affectedRows + ' row(s).');
        })
       conn.end(function (err) { 
        if (err) throw err;
        else  console.log('Done.') 
        });
};
```

## <a name="read-data"></a><span data-ttu-id="a9add-154">Считывание данных</span><span class="sxs-lookup"><span data-stu-id="a9add-154">Read data</span></span>
<span data-ttu-id="a9add-155">Используйте указанный ниже код с инструкцией SQL **SELECT** для подключения и чтения данных.</span><span class="sxs-lookup"><span data-stu-id="a9add-155">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="a9add-156">Метод [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) используется для обмена данными с сервером MySQL.</span><span class="sxs-lookup"><span data-stu-id="a9add-156">The [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used to interface with the MySQL server.</span></span> <span data-ttu-id="a9add-157">Метод [connect()](https://github.com/mysqljs/mysql#establishing-connections) используется для подключения к серверу.</span><span class="sxs-lookup"><span data-stu-id="a9add-157">The [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used to establish the connection to the server.</span></span> <span data-ttu-id="a9add-158">Метод [query()](https://github.com/mysqljs/mysql#performing-queries) используется для выполнения SQL-запроса к базе данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="a9add-158">The [query()](https://github.com/mysqljs/mysql#performing-queries) method is used to execute the SQL query against MySQL database.</span></span> <span data-ttu-id="a9add-159">Массив результатов используется для хранения результатов запроса.</span><span class="sxs-lookup"><span data-stu-id="a9add-159">The results array is used to hold the results of the query.</span></span>

<span data-ttu-id="a9add-160">Замените параметры `host`, `user`, `password` и `database` значениями, указанными при создании сервера и базы данных.</span><span class="sxs-lookup"><span data-stu-id="a9add-160">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'myserver4demo.mysql.database.azure.com',
    user: 'myadmin@myserver4demo',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
        if (err) { 
            console.log("!!! Cannot connect !!! Error:");
            throw err;
        }
        else {
            console.log("Connection established.");
            readData();
        }   
    });

function readData(){
        conn.query('SELECT * FROM inventory', 
            function (err, results, fields) {
                if (err) throw err;
                else console.log('Selected ' + results.length + ' row(s).');
                for (i = 0; i < results.length; i++) {
                    console.log('Row: ' + JSON.stringify(results[i]));
                }
                console.log('Done.');
            })
       conn.end(
           function (err) { 
                if (err) throw err;
                else  console.log('Closing connection.') 
        });
};
```

## <a name="update-data"></a><span data-ttu-id="a9add-161">Обновление данных</span><span class="sxs-lookup"><span data-stu-id="a9add-161">Update data</span></span>
<span data-ttu-id="a9add-162">Используйте указанный ниже код с инструкцией SQL **UPDATE** для подключения и чтения данных.</span><span class="sxs-lookup"><span data-stu-id="a9add-162">Use the following code to connect and read the data using a **UPDATE** SQL statement.</span></span> 

<span data-ttu-id="a9add-163">Метод [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) используется для обмена данными с сервером MySQL.</span><span class="sxs-lookup"><span data-stu-id="a9add-163">The [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used to interface with the MySQL server.</span></span> <span data-ttu-id="a9add-164">Метод [connect()](https://github.com/mysqljs/mysql#establishing-connections) используется для подключения к серверу.</span><span class="sxs-lookup"><span data-stu-id="a9add-164">The [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used to establish the connection to the server.</span></span> <span data-ttu-id="a9add-165">Метод [query()](https://github.com/mysqljs/mysql#performing-queries) используется для выполнения SQL-запроса к базе данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="a9add-165">The [query()](https://github.com/mysqljs/mysql#performing-queries) method is used to execute the SQL query against MySQL database.</span></span> 

<span data-ttu-id="a9add-166">Замените параметры `host`, `user`, `password` и `database` значениями, указанными при создании сервера и базы данных.</span><span class="sxs-lookup"><span data-stu-id="a9add-166">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'myserver4demo.mysql.database.azure.com',
    user: 'myadmin@myserver4demo',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
        if (err) { 
            console.log("!!! Cannot connect !!! Error:");
            throw err;
        }
        else {
            console.log("Connection established.");
            updateData();
        }   
    });

function updateData(){
       conn.query('UPDATE inventory SET quantity = ? WHERE name = ?', [200, 'banana'], 
            function (err, results, fields) {
                if (err) throw err;
                else console.log('Updated ' + results.affectedRows + ' row(s).');
        })
       conn.end(
           function (err) { 
                if (err) throw err;
                else  console.log('Done.') 
        });
};
```

## <a name="delete-data"></a><span data-ttu-id="a9add-167">Удаление данных</span><span class="sxs-lookup"><span data-stu-id="a9add-167">Delete data</span></span>
<span data-ttu-id="a9add-168">Используйте указанный ниже код с инструкцией SQL **DELETE** для подключения и чтения данных.</span><span class="sxs-lookup"><span data-stu-id="a9add-168">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="a9add-169">Метод [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) используется для обмена данными с сервером MySQL.</span><span class="sxs-lookup"><span data-stu-id="a9add-169">The [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used to interface with the MySQL server.</span></span> <span data-ttu-id="a9add-170">Метод [connect()](https://github.com/mysqljs/mysql#establishing-connections) используется для подключения к серверу.</span><span class="sxs-lookup"><span data-stu-id="a9add-170">The [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used to establish the connection to the server.</span></span> <span data-ttu-id="a9add-171">Метод [query()](https://github.com/mysqljs/mysql#performing-queries) используется для выполнения SQL-запроса к базе данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="a9add-171">The [query()](https://github.com/mysqljs/mysql#performing-queries) method is used to execute the SQL query against MySQL database.</span></span> 

<span data-ttu-id="a9add-172">Замените параметры `host`, `user`, `password` и `database` значениями, указанными при создании сервера и базы данных.</span><span class="sxs-lookup"><span data-stu-id="a9add-172">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'myserver4demo.mysql.database.azure.com',
    user: 'myadmin@myserver4demo',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
        if (err) { 
            console.log("!!! Cannot connect !!! Error:");
            throw err;
        }
        else {
            console.log("Connection established.");
            deleteData();
        }   
    });

function deleteData(){
       conn.query('DELETE FROM inventory WHERE name = ?', ['orange'], 
            function (err, results, fields) {
                if (err) throw err;
                else console.log('Deleted ' + results.affectedRows + ' row(s).');
        })
       conn.end(
           function (err) { 
                if (err) throw err;
                else  console.log('Done.') 
        });
};
```

## <a name="next-steps"></a><span data-ttu-id="a9add-173">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a9add-173">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="a9add-174">Перенос базы данных с помощью экспорта и импорта</span><span class="sxs-lookup"><span data-stu-id="a9add-174">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
