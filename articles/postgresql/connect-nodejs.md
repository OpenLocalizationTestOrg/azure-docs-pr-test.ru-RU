---
title: "Подключение к базе данных Azure для PostgreSQL с помощью Node.js | Документация Майкрософт"
description: "В этом кратком руководстве представлен пример кода Node.js, который можно использовать для подключения к базе данных Azure для PostgreSQL и запроса данных из нее."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: nodejs
ms.topic: quickstart
ms.date: 06/23/2017
ms.openlocfilehash: f6c98833c73b70bcf1f8ca53596a34f09807b276
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-postgresql-use-nodejs-to-connect-and-query-data"></a><span data-ttu-id="b4490-103">База данных Azure для PostgreSQL: подключение и запрос данных с помощью Node.js</span><span class="sxs-lookup"><span data-stu-id="b4490-103">Azure Database for PostgreSQL: Use Node.js to connect and query data</span></span>
<span data-ttu-id="b4490-104">В этом кратком руководстве объясняется, как подключиться к базе данных Azure для PostgreSQL с помощью [Node.js](https://nodejs.org/).</span><span class="sxs-lookup"><span data-stu-id="b4490-104">This quickstart demonstrates how to connect to an Azure Database for PostgreSQL using [Node.js](https://nodejs.org/).</span></span> <span data-ttu-id="b4490-105">Здесь также показано, как использовать инструкции SQL для запроса, вставки, обновления и удаления данных в базе данных.</span><span class="sxs-lookup"><span data-stu-id="b4490-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="b4490-106">В этой статье предполагается, что у вас уже есть опыт разработки на Node.js и вы только начали работу с базой данных Azure для PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="b4490-106">The steps in this article assume that you are familiar with developing using Node.js, and that you are new to working with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b4490-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b4490-107">Prerequisites</span></span>
<span data-ttu-id="b4490-108">В качестве отправной точки в этом кратком руководстве используются ресурсы, созданные в соответствии со следующими материалами:</span><span class="sxs-lookup"><span data-stu-id="b4490-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="b4490-109">Создание базы данных с помощью портала</span><span class="sxs-lookup"><span data-stu-id="b4490-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="b4490-110">Создание базы данных SQL Azure и отправка к ней запросов с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b4490-110">Create DB - CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="b4490-111">Также вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="b4490-111">You also need to:</span></span>
- <span data-ttu-id="b4490-112">Установите [Node.js](https://nodejs.org)</span><span class="sxs-lookup"><span data-stu-id="b4490-112">Install [Node.js](https://nodejs.org)</span></span>

## <a name="install-pg-client"></a><span data-ttu-id="b4490-113">Установка клиента pg</span><span class="sxs-lookup"><span data-stu-id="b4490-113">Install pg client</span></span>
<span data-ttu-id="b4490-114">Установите [pg](https://www.npmjs.com/package/pg), клиент PostgreSQL для Node.js.</span><span class="sxs-lookup"><span data-stu-id="b4490-114">Install [pg](https://www.npmjs.com/package/pg), which is a PostgreSQL client for Node.js.</span></span>

<span data-ttu-id="b4490-115">Для этого запустите диспетчер пакетов узла (npm) для JavaScript из командной строки.</span><span class="sxs-lookup"><span data-stu-id="b4490-115">To do so, run the node package manager (npm) for JavaScript from your command line to install the pg client.</span></span>
```bash
npm install pg
```

<span data-ttu-id="b4490-116">Проверьте установку, получив список установленных пакетов.</span><span class="sxs-lookup"><span data-stu-id="b4490-116">Verify the installation by listing the packages installed.</span></span>
```bash
npm list
```

## <a name="get-connection-information"></a><span data-ttu-id="b4490-117">Получение сведений о подключении</span><span class="sxs-lookup"><span data-stu-id="b4490-117">Get connection information</span></span>
<span data-ttu-id="b4490-118">Получите сведения, необходимые для подключения к базе данных Azure.для PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="b4490-118">Get the connection information needed to connect to the Azure Database for PostgreSQL.</span></span> <span data-ttu-id="b4490-119">Вам потребуется полное имя сервера и учетные данные для входа.</span><span class="sxs-lookup"><span data-stu-id="b4490-119">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="b4490-120">Войдите на [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b4490-120">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="b4490-121">На портале Azure в меню слева щелкните **Все ресурсы** и найдите только что созданный сервер.</span><span class="sxs-lookup"><span data-stu-id="b4490-121">From the left-hand menu in Azure portal, click **All resources** and search for the server you just created.</span></span>
3. <span data-ttu-id="b4490-122">Щелкните имя сервера.</span><span class="sxs-lookup"><span data-stu-id="b4490-122">Click the server name.</span></span>
4. <span data-ttu-id="b4490-123">Выберите страницу **обзора** сервера.</span><span class="sxs-lookup"><span data-stu-id="b4490-123">Select the server's **Overview** page.</span></span> <span data-ttu-id="b4490-124">Запишите значения **имени сервера** и **имени для входа администратора сервера**.</span><span class="sxs-lookup"><span data-stu-id="b4490-124">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="b4490-125">![База данных Azure для PostgreSQL. Учетные данные администратора сервера для входа](./media/connect-nodejs/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="b4490-125">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-nodejs/1-connection-string.png)</span></span>
5. <span data-ttu-id="b4490-126">Если вы забыли данные для входа на сервер, перейдите на страницу **Обзор**, чтобы просмотреть имя администратора сервера и при необходимости сбросить пароль.</span><span class="sxs-lookup"><span data-stu-id="b4490-126">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="running-the-javascript-code-in-nodejs"></a><span data-ttu-id="b4490-127">Выполнение кода JavaScript в Node.js</span><span class="sxs-lookup"><span data-stu-id="b4490-127">Running the JavaScript code in Node.js</span></span>
<span data-ttu-id="b4490-128">Node.js можно запустить из оболочки Bash или командной строки Windows при помощи команды `node`. Затем интерактивно запустите пример кода JavaScript, скопировав и вставив его в командную строку.</span><span class="sxs-lookup"><span data-stu-id="b4490-128">You may launch Node.js from the bash shell or windows command prompt by typing `node`, then run the example JavaScript code interactively by copy and pasting it onto the prompt.</span></span> <span data-ttu-id="b4490-129">Либо же можно сохранить код JavaScript в текстовый файл и запустить `node filename.js` с именем файла в качестве параметра для его выполнения.</span><span class="sxs-lookup"><span data-stu-id="b4490-129">Alternatively, you may save the JavaScript code into a text file and launch `node filename.js` with the file name as a parameter to run it.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="b4490-130">Подключение, создание таблицы и вставка данных</span><span class="sxs-lookup"><span data-stu-id="b4490-130">Connect, create table, and insert data</span></span>
<span data-ttu-id="b4490-131">Используйте приведенный ниже код для подключения и загрузки данных с помощью инструкций SQL **CREATE TABLE** и **INSERT INTO**.</span><span class="sxs-lookup"><span data-stu-id="b4490-131">Use the following code to connect and load the data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span>
<span data-ttu-id="b4490-132">Объект [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) используется для обмена данными с сервером PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="b4490-132">The [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used to interface with the PostgreSQL server.</span></span> <span data-ttu-id="b4490-133">Функция [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) используется для подключения к серверу.</span><span class="sxs-lookup"><span data-stu-id="b4490-133">The [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used to establish the connection to the server.</span></span> <span data-ttu-id="b4490-134">Функция [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) используется для выполнения SQL-запроса к базе данных PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="b4490-134">The [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used to execute the SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="b4490-135">Замените значения параметров host, dbname, user и password значениями, указанными при создании сервера и базы данных.</span><span class="sxs-lookup"><span data-stu-id="b4490-135">Replace the host, dbname, user, and password parameters with the values that you specified when you created the server and database.</span></span>

```javascript
const pg = require('pg');

const config = {
    host: '<your-db-server-name>.postgres.database.azure.com',
    // Do not hard code your username and password.
    // Consider using Node environment variables.
    user: '<your-db-username>',     
    password: '<your-password>',
    database: '<name-of-database>',
    port: 5432,
    ssl: true
};

const client = new pg.Client(config);

client.connect(err => {
    if (err) throw err;
    else {
        queryDatabase();
    }
});

function queryDatabase() {
    const query = `
        DROP TABLE IF EXISTS inventory;
        CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);
        INSERT INTO inventory (name, quantity) VALUES ('banana', 150);
        INSERT INTO inventory (name, quantity) VALUES ('orange', 154);
        INSERT INTO inventory (name, quantity) VALUES ('apple', 100);
    `;

    client
        .query(query)
        .then(() => {
            console.log('Table created successfully!');
            client.end(console.log('Closed client connection'));
        })
        .catch(err => console.log(err))
        .then(() => {
            console.log('Finished execution, exiting now');
            process.exit();
        });
}
```

## <a name="read-data"></a><span data-ttu-id="b4490-136">Считывание данных</span><span class="sxs-lookup"><span data-stu-id="b4490-136">Read data</span></span>
<span data-ttu-id="b4490-137">Используйте указанный ниже код с инструкцией SQL **SELECT** для подключения и чтения данных.</span><span class="sxs-lookup"><span data-stu-id="b4490-137">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="b4490-138">Объект [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) используется для обмена данными с сервером PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="b4490-138">The [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used to interface with the PostgreSQL server.</span></span> <span data-ttu-id="b4490-139">Функция [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) используется для подключения к серверу.</span><span class="sxs-lookup"><span data-stu-id="b4490-139">The [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used to establish the connection to the server.</span></span> <span data-ttu-id="b4490-140">Функция [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) используется для выполнения SQL-запроса к базе данных PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="b4490-140">The [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used to execute the SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="b4490-141">Замените значения параметров host, dbname, user и password значениями, указанными при создании сервера и базы данных.</span><span class="sxs-lookup"><span data-stu-id="b4490-141">Replace the host, dbname, user, and password parameters with the values that you specified when you created the server and database.</span></span> 

```javascript
const pg = require('pg');

const config = {
    host: '<your-db-server-name>.postgres.database.azure.com',
    // Do not hard code your username and password.
    // Consider using Node environment variables.
    user: '<your-db-username>',     
    password: '<your-password>',
    database: '<name-of-database>',
    port: 5432,
    ssl: true
};

const client = new pg.Client(config);

client.connect(err => {
    if (err) throw err;
    else { queryDatabase(); }
});

function queryDatabase() {
  
    console.log(`Running query to PostgreSQL server: ${config.host}`);

    const query = 'SELECT * FROM inventory;';

    client.query(query)
        .then(res => {
            const rows = res.rows;

            rows.map(row => {
                console.log(`Read: ${JSON.stringify(row)}`);
            });

            process.exit();
        })
        .catch(err => {
            console.log(err);
        });
}
```

## <a name="update-data"></a><span data-ttu-id="b4490-142">Обновление данных</span><span class="sxs-lookup"><span data-stu-id="b4490-142">Update data</span></span>
<span data-ttu-id="b4490-143">Используйте указанный ниже код с инструкцией SQL **UPDATE** для подключения и чтения данных.</span><span class="sxs-lookup"><span data-stu-id="b4490-143">Use the following code to connect and read the data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="b4490-144">Объект [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) используется для обмена данными с сервером PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="b4490-144">The [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used to interface with the PostgreSQL server.</span></span> <span data-ttu-id="b4490-145">Функция [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) используется для подключения к серверу.</span><span class="sxs-lookup"><span data-stu-id="b4490-145">The [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used to establish the connection to the server.</span></span> <span data-ttu-id="b4490-146">Функция [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) используется для выполнения SQL-запроса к базе данных PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="b4490-146">The [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used to execute the SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="b4490-147">Замените значения параметров host, dbname, user и password значениями, указанными при создании сервера и базы данных.</span><span class="sxs-lookup"><span data-stu-id="b4490-147">Replace the host, dbname, user, and password parameters with the values that you specified when you created the server and database.</span></span> 

```javascript
const pg = require('pg');

const config = {
    host: '<your-db-server-name>.postgres.database.azure.com',
    // Do not hard code your username and password.
    // Consider using Node environment variables.
    user: '<your-db-username>',     
    password: '<your-password>',
    database: '<name-of-database>',
    port: 5432,
    ssl: true
};

const client = new pg.Client(config);

client.connect(err => {
    if (err) throw err;
    else {
        queryDatabase();
    }
});

function queryDatabase() {
    const query = `
        UPDATE inventory 
        SET quantity= 1000 WHERE name='banana';
    `;

    client
        .query(query)
        .then(result => {
            console.log('Update completed');
            console.log(`Rows affected: ${result.rowCount}`);
        })
        .catch(err => {
            console.log(err);
            throw err;
        });
}
```

## <a name="delete-data"></a><span data-ttu-id="b4490-148">Удаление данных</span><span class="sxs-lookup"><span data-stu-id="b4490-148">Delete data</span></span>
<span data-ttu-id="b4490-149">Используйте указанный ниже код с инструкцией SQL **DELETE** для подключения и чтения данных.</span><span class="sxs-lookup"><span data-stu-id="b4490-149">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> <span data-ttu-id="b4490-150">Объект [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) используется для обмена данными с сервером PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="b4490-150">The [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used to interface with the PostgreSQL server.</span></span> <span data-ttu-id="b4490-151">Функция [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) используется для подключения к серверу.</span><span class="sxs-lookup"><span data-stu-id="b4490-151">The [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used to establish the connection to the server.</span></span> <span data-ttu-id="b4490-152">Функция [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) используется для выполнения SQL-запроса к базе данных PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="b4490-152">The [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used to execute the SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="b4490-153">Замените значения параметров host, dbname, user и password значениями, указанными при создании сервера и базы данных.</span><span class="sxs-lookup"><span data-stu-id="b4490-153">Replace the host, dbname, user, and password parameters with the values that you specified when you created the server and database.</span></span> 

```javascript
const pg = require('pg');

const config = {
    host: '<your-db-server-name>.postgres.database.azure.com',
    // Do not hard code your username and password.
    // Consider using Node environment variables.
    user: '<your-db-username>',     
    password: '<your-password>',
    database: '<name-of-database>',
    port: 5432,
    ssl: true
};

const client = new pg.Client(config);

client.connect(err => {
    if (err) {
        throw err;
    } else {
        queryDatabase();
    }
});

function queryDatabase() {
    const query = `
        DELETE FROM inventory 
        WHERE name = 'apple';
    `;

    client
        .query(query)
        .then(result => {
            console.log('Delete completed');
            console.log(`Rows affected: ${result.rowCount}`);
        })
        .catch(err => {
            console.log(err);
            throw err;
        });
}
```

## <a name="next-steps"></a><span data-ttu-id="b4490-154">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b4490-154">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="b4490-155">Перенос базы данных с помощью экспорта и импорта</span><span class="sxs-lookup"><span data-stu-id="b4490-155">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
