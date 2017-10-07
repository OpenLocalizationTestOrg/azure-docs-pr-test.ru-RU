---
title: "Подключение tooAzure базы данных MySQL из Node.js | Документы Microsoft"
description: "Это краткое руководство входит несколько примеров кода Node.js, можно использовать tooconnect и запроса данных из базы данных Azure для MySQL."
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
ms.openlocfilehash: ed9a39b5ab003e8216cef1c0f6a95a75c3db8458
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-nodejs-tooconnect-and-query-data"></a><span data-ttu-id="a5a54-103">База данных Azure для MySQL: tooconnect и запрашивают данные, используйте Node.js</span><span class="sxs-lookup"><span data-stu-id="a5a54-103">Azure Database for MySQL: Use Node.js tooconnect and query data</span></span>
<span data-ttu-id="a5a54-104">Краткого руководства показано, как tooconnect tooan Azure этой базы данных MySQL с помощью [Node.js](https://nodejs.org/) из платформ Mac, Ubuntu Linux и Windows.</span><span class="sxs-lookup"><span data-stu-id="a5a54-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using [Node.js](https://nodejs.org/) from Windows, Ubuntu Linux, and Mac platforms.</span></span> <span data-ttu-id="a5a54-105">Показано, как tooquery инструкций SQL toouse, вставка, обновление и удаление данных в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="a5a54-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="a5a54-106">Hello в этой статье предполагается, что вы знакомы с разработка с использованием Node.js и новый tooworking с базой данных Azure для MySQL, которые.</span><span class="sxs-lookup"><span data-stu-id="a5a54-106">hello steps in this article assume that you are familiar with developing using Node.js, and that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a5a54-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a5a54-107">Prerequisites</span></span>
<span data-ttu-id="a5a54-108">Это краткое руководство использует ресурсы hello, созданные в любой из этих руководствах по в качестве отправной точки.</span><span class="sxs-lookup"><span data-stu-id="a5a54-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- <span data-ttu-id="a5a54-109">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Создание сервера базы данных Azure для MySQL с помощью портала Azure)</span><span class="sxs-lookup"><span data-stu-id="a5a54-109">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md)</span></span>
- <span data-ttu-id="a5a54-110">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md) (Создание сервера базы данных Azure для MySQL с помощью Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="a5a54-110">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md)</span></span>

<span data-ttu-id="a5a54-111">Также вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="a5a54-111">You also need to:</span></span>
- <span data-ttu-id="a5a54-112">Установка hello [Node.js](https://nodejs.org) среды выполнения.</span><span class="sxs-lookup"><span data-stu-id="a5a54-112">Install hello [Node.js](https://nodejs.org) runtime.</span></span>
- <span data-ttu-id="a5a54-113">Установка [mysql2](https://www.npmjs.com/package/mysql2) пакета tooMySQL tooconnect из Node.js приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a5a54-113">Install [mysql2](https://www.npmjs.com/package/mysql2) package tooconnect tooMySQL from hello Node.js application.</span></span> 

## <a name="install-nodejs-and-hello-mysql-connector"></a><span data-ttu-id="a5a54-114">Установка Node.js и hello соединителя MySQL</span><span class="sxs-lookup"><span data-stu-id="a5a54-114">Install Node.js and hello MySQL connector</span></span>
<span data-ttu-id="a5a54-115">В зависимости от используемой платформы выполните соответствующие инструкции hello tooinstall Node.js.</span><span class="sxs-lookup"><span data-stu-id="a5a54-115">Depending on your platform, follow hello appropriate instructions tooinstall Node.js.</span></span> <span data-ttu-id="a5a54-116">Используйте npm tooinstall hello mysql2 пакет и его зависимости в папку проекта.</span><span class="sxs-lookup"><span data-stu-id="a5a54-116">Use npm tooinstall hello mysql2 package and its dependencies into your project folder.</span></span>

### <a name="windows"></a><span data-ttu-id="a5a54-117">**Windows**</span><span class="sxs-lookup"><span data-stu-id="a5a54-117">**Windows**</span></span>
1. <span data-ttu-id="a5a54-118">Посетите hello [Node.js загружает страницу](https://nodejs.org/en/download/) и выберите нужный режим установщика Windows.</span><span class="sxs-lookup"><span data-stu-id="a5a54-118">Visit hello [Node.js downloads page](https://nodejs.org/en/download/) and select your desired Windows installer option.</span></span>
2. <span data-ttu-id="a5a54-119">Создайте папку локального проекта, например `nodejsmysql`.</span><span class="sxs-lookup"><span data-stu-id="a5a54-119">Make a local project folder such as `nodejsmysql`.</span></span> 
3. <span data-ttu-id="a5a54-120">Запустите командную строку hello и компакт-диска в папку проекта hello, такие как`cd c:\nodejsmysql\`</span><span class="sxs-lookup"><span data-stu-id="a5a54-120">Launch hello command prompt and cd into hello project folder, such as `cd c:\nodejsmysql\`</span></span>
4. <span data-ttu-id="a5a54-121">Запустите hello NPM средство tooinstall hello mysql2 библиотеки в папку проекта hello.</span><span class="sxs-lookup"><span data-stu-id="a5a54-121">Run hello NPM tool tooinstall hello mysql2 library into hello project folder.</span></span>

   ```cmd
   cd c:\nodejsmysql\
   "C:\Program Files\nodejs\npm" install mysql2
   "C:\Program Files\nodejs\npm" list
   ```

5. <span data-ttu-id="a5a54-122">Проверить hello hello `npm list` вывода текста для `mysql2@1.3.5`.</span><span class="sxs-lookup"><span data-stu-id="a5a54-122">Verify hello installation by checking hello `npm list` output text for `mysql2@1.3.5`.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="a5a54-123">**Linux (Ubuntu)**</span><span class="sxs-lookup"><span data-stu-id="a5a54-123">**Linux (Ubuntu)**</span></span>
1. <span data-ttu-id="a5a54-124">Выполнения hello следующими командами tooinstall **Node.js** и **npm** диспетчера пакетов приветствия для Node.js.</span><span class="sxs-lookup"><span data-stu-id="a5a54-124">Run hello following commands tooinstall **Node.js** and **npm** hello package manager for Node.js.</span></span>

   ```bash
   sudo apt-get install -y nodejs npm
   ```

2. <span data-ttu-id="a5a54-125">Запустите следующие команды toomake hello в папку проекта `mysqlnodejs` и установить пакет mysql2 hello в этой папке.</span><span class="sxs-lookup"><span data-stu-id="a5a54-125">Run hello following commands toomake a project folder `mysqlnodejs` and install hello mysql2 package into that folder.</span></span>

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```
3. <span data-ttu-id="a5a54-126">Проверить, просмотрев текст вывод списка npm для установки hello `mysql2@1.3.5`.</span><span class="sxs-lookup"><span data-stu-id="a5a54-126">Verify hello installation by checking npm list output text for `mysql2@1.3.5`.</span></span>

### <a name="mac-os"></a><span data-ttu-id="a5a54-127">**Mac OS**</span><span class="sxs-lookup"><span data-stu-id="a5a54-127">**Mac OS**</span></span>
1. <span data-ttu-id="a5a54-128">Введите следующие команды tooinstall hello **brew**, диспетчер пакетов для использования для Mac OS X и **Node.js**.</span><span class="sxs-lookup"><span data-stu-id="a5a54-128">Enter hello following commands tooinstall **brew**, an easy-to-use package manager for Mac OS X and **Node.js**.</span></span>

   ```bash
   ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
   brew install node
   ```
2. <span data-ttu-id="a5a54-129">Запустите следующие команды toomake hello в папку проекта `mysqlnodejs` и установить пакет mysql2 hello в этой папке.</span><span class="sxs-lookup"><span data-stu-id="a5a54-129">Run hello following commands toomake a project folder `mysqlnodejs` and install hello mysql2 package into that folder.</span></span>

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```

3. <span data-ttu-id="a5a54-130">Проверить hello hello `npm list` вывода текста для `mysql2@1.3.6`.</span><span class="sxs-lookup"><span data-stu-id="a5a54-130">Verify hello installation by checking hello `npm list` output text for `mysql2@1.3.6`.</span></span> <span data-ttu-id="a5a54-131">Hello номер версии может изменяться будут выпущены новые обновления.</span><span class="sxs-lookup"><span data-stu-id="a5a54-131">hello version number may vary as new patches are released.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="a5a54-132">Получение сведений о подключении</span><span class="sxs-lookup"><span data-stu-id="a5a54-132">Get connection information</span></span>
<span data-ttu-id="a5a54-133">Получите toohello tooconnect базы данных Azure для hello подключения сведения, необходимые для MySQL.</span><span class="sxs-lookup"><span data-stu-id="a5a54-133">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="a5a54-134">Необходимо hello server полное имя и учетные данные входа.</span><span class="sxs-lookup"><span data-stu-id="a5a54-134">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="a5a54-135">Войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a5a54-135">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="a5a54-136">Hello левой панели щелкните **все ресурсы**и выполните поиск hello сервере был создан (например, **myserver4demo**).</span><span class="sxs-lookup"><span data-stu-id="a5a54-136">In hello left pane, click **All resources**, and then search for hello server you have created (for example, **myserver4demo**).</span></span>
3. <span data-ttu-id="a5a54-137">Щелкните имя сервера hello **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="a5a54-137">Click hello server name **myserver4demo**.</span></span>
4. <span data-ttu-id="a5a54-138">Выберите hello server **свойства** страницы.</span><span class="sxs-lookup"><span data-stu-id="a5a54-138">Select hello server's **Properties** page.</span></span> <span data-ttu-id="a5a54-139">Запишите hello **имя сервера** и **имя входа администратора сервера**.</span><span class="sxs-lookup"><span data-stu-id="a5a54-139">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="a5a54-140">![Имя входа для администратора сервера в базе данных Azure для MySQL](./media/connect-nodejs/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="a5a54-140">![Azure Database for MySQL - Server Admin Login](./media/connect-nodejs/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="a5a54-141">Если вы забыли учетные данные входа сервера, перейдите toohello **Обзор** страница hello tooview: имя пользователя администратора сервера и, при необходимости переустановить пароль hello.</span><span class="sxs-lookup"><span data-stu-id="a5a54-141">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="running-hello-javascript-code-in-nodejs"></a><span data-ttu-id="a5a54-142">Выполняет код JavaScript hello в Node.js</span><span class="sxs-lookup"><span data-stu-id="a5a54-142">Running hello JavaScript code in Node.js</span></span>
1. <span data-ttu-id="a5a54-143">Вставьте код JavaScript hello в текстовые файлы и сохранить в папку проекта с расширением .js файла, например C:\nodejsmysql\createtable.js или /home/username/nodejsmysql/createtable.js</span><span class="sxs-lookup"><span data-stu-id="a5a54-143">Paste hello JavaScript code into text files, and save into a project folder with file extension .js, such as C:\nodejsmysql\createtable.js or /home/username/nodejsmysql/createtable.js</span></span>
2. <span data-ttu-id="a5a54-144">Запустите командную строку hello или bash оболочки.</span><span class="sxs-lookup"><span data-stu-id="a5a54-144">Launch hello command prompt or bash shell.</span></span> <span data-ttu-id="a5a54-145">Перейдите в папку проекта `cd nodejsmysql`.</span><span class="sxs-lookup"><span data-stu-id="a5a54-145">Change directory into your project folder `cd nodejsmysql`.</span></span>
3. <span data-ttu-id="a5a54-146">приложение hello toorun, введите команду узел hello следуют hello имя файла, например `node createtable.js`.</span><span class="sxs-lookup"><span data-stu-id="a5a54-146">toorun hello application, type hello node command followed by hello file name, such as `node createtable.js`.</span></span>
4. <span data-ttu-id="a5a54-147">В Windows Если приложение hello узел не находится в переменной путь к среде, может потребоваться toouse hello полный путь toolaunch hello узел приложения, такие как`"C:\Program Files\nodejs\node.exe" createtable.js`</span><span class="sxs-lookup"><span data-stu-id="a5a54-147">On Windows, if hello node application is not in your environment variable path, you may need toouse hello full path toolaunch hello node application, such as `"C:\Program Files\nodejs\node.exe" createtable.js`</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="a5a54-148">Подключение, создание таблицы и вставка данных</span><span class="sxs-lookup"><span data-stu-id="a5a54-148">Connect, create table, and insert data</span></span>
<span data-ttu-id="a5a54-149">Используйте следующие hello кода tooconnect и загружать данные при помощи hello **CREATE TABLE** и **INSERT INTO** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="a5a54-149">Use hello following code tooconnect and load hello data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span>

<span data-ttu-id="a5a54-150">Hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) в противном случае используется toointerface с сервером MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="a5a54-150">hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used toointerface with hello MySQL server.</span></span> <span data-ttu-id="a5a54-151">Hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) функция является используется tooestablish hello соединения toohello сервера.</span><span class="sxs-lookup"><span data-stu-id="a5a54-151">hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) function is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="a5a54-152">Hello [query()](https://github.com/mysqljs/mysql#performing-queries) функция является используется tooexecute hello SQL-запрос к базе данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="a5a54-152">hello [query()](https://github.com/mysqljs/mysql#performing-queries) function is used tooexecute hello SQL query against MySQL database.</span></span> 

<span data-ttu-id="a5a54-153">Замените hello `host`, `user`, `password`, и `database` параметров со значениями hello, указанный при создании hello сервера и базы данных.</span><span class="sxs-lookup"><span data-stu-id="a5a54-153">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

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

## <a name="read-data"></a><span data-ttu-id="a5a54-154">Считывание данных</span><span class="sxs-lookup"><span data-stu-id="a5a54-154">Read data</span></span>
<span data-ttu-id="a5a54-155">Используйте следующие hello кода tooconnect и чтения данных с помощью hello **ВЫБЕРИТЕ** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="a5a54-155">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="a5a54-156">Hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) в противном случае используется toointerface с сервером MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="a5a54-156">hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used toointerface with hello MySQL server.</span></span> <span data-ttu-id="a5a54-157">Hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) в противном случае используется tooestablish hello соединения toohello сервера.</span><span class="sxs-lookup"><span data-stu-id="a5a54-157">hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="a5a54-158">Hello [query()](https://github.com/mysqljs/mysql#performing-queries) метод является используется tooexecute hello SQL-запрос к базе данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="a5a54-158">hello [query()](https://github.com/mysqljs/mysql#performing-queries) method is used tooexecute hello SQL query against MySQL database.</span></span> <span data-ttu-id="a5a54-159">Массив результатов Hello — используется toohold hello результаты запроса hello.</span><span class="sxs-lookup"><span data-stu-id="a5a54-159">hello results array is used toohold hello results of hello query.</span></span>

<span data-ttu-id="a5a54-160">Замените hello `host`, `user`, `password`, и `database` параметров со значениями hello, указанный при создании hello сервера и базы данных.</span><span class="sxs-lookup"><span data-stu-id="a5a54-160">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

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

## <a name="update-data"></a><span data-ttu-id="a5a54-161">Обновление данных</span><span class="sxs-lookup"><span data-stu-id="a5a54-161">Update data</span></span>
<span data-ttu-id="a5a54-162">Используйте следующие hello кода tooconnect и чтения данных с помощью hello **обновление** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="a5a54-162">Use hello following code tooconnect and read hello data using a **UPDATE** SQL statement.</span></span> 

<span data-ttu-id="a5a54-163">Hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) в противном случае используется toointerface с сервером MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="a5a54-163">hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used toointerface with hello MySQL server.</span></span> <span data-ttu-id="a5a54-164">Hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) в противном случае используется tooestablish hello соединения toohello сервера.</span><span class="sxs-lookup"><span data-stu-id="a5a54-164">hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="a5a54-165">Hello [query()](https://github.com/mysqljs/mysql#performing-queries) метод является используется tooexecute hello SQL-запрос к базе данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="a5a54-165">hello [query()](https://github.com/mysqljs/mysql#performing-queries) method is used tooexecute hello SQL query against MySQL database.</span></span> 

<span data-ttu-id="a5a54-166">Замените hello `host`, `user`, `password`, и `database` параметров со значениями hello, указанный при создании hello сервера и базы данных.</span><span class="sxs-lookup"><span data-stu-id="a5a54-166">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

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

## <a name="delete-data"></a><span data-ttu-id="a5a54-167">Удаление данных</span><span class="sxs-lookup"><span data-stu-id="a5a54-167">Delete data</span></span>
<span data-ttu-id="a5a54-168">Используйте следующие hello кода tooconnect и чтения данных с помощью hello **удалить** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="a5a54-168">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="a5a54-169">Hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) в противном случае используется toointerface с сервером MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="a5a54-169">hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used toointerface with hello MySQL server.</span></span> <span data-ttu-id="a5a54-170">Hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) в противном случае используется tooestablish hello соединения toohello сервера.</span><span class="sxs-lookup"><span data-stu-id="a5a54-170">hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="a5a54-171">Hello [query()](https://github.com/mysqljs/mysql#performing-queries) метод является используется tooexecute hello SQL-запрос к базе данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="a5a54-171">hello [query()](https://github.com/mysqljs/mysql#performing-queries) method is used tooexecute hello SQL query against MySQL database.</span></span> 

<span data-ttu-id="a5a54-172">Замените hello `host`, `user`, `password`, и `database` параметров со значениями hello, указанный при создании hello сервера и базы данных.</span><span class="sxs-lookup"><span data-stu-id="a5a54-172">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="a5a54-173">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a5a54-173">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="a5a54-174">Перенос базы данных с помощью экспорта и импорта</span><span class="sxs-lookup"><span data-stu-id="a5a54-174">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
