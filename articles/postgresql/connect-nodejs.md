---
title: "Подключение tooAzure базы данных PostgreSQL из Node.js | Документы Microsoft"
description: "Это краткое руководство содержит пример кода Node.js можно использовать tooconnect и запроса данных из базы данных Azure для PostgreSQL."
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
ms.openlocfilehash: 9b269d72068ecc24bcf3fb447a2efeda512c698c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-nodejs-tooconnect-and-query-data"></a><span data-ttu-id="1fe2f-103">База данных Azure для PostgreSQL: использование Node.js tooconnect и запроса данных</span><span class="sxs-lookup"><span data-stu-id="1fe2f-103">Azure Database for PostgreSQL: Use Node.js tooconnect and query data</span></span>
<span data-ttu-id="1fe2f-104">Это краткое руководство демонстрирует, как tooconnect tooan Azure этой базы данных с помощью PostgreSQL [Node.js](https://nodejs.org/).</span><span class="sxs-lookup"><span data-stu-id="1fe2f-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using [Node.js](https://nodejs.org/).</span></span> <span data-ttu-id="1fe2f-105">Показано, как tooquery инструкций SQL toouse, вставка, обновление и удаление данных в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="1fe2f-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="1fe2f-106">Hello в этой статье предполагается, что вы знакомы с разработка с использованием Node.js и новый tooworking с базой данных Azure для PostgreSQL, которые.</span><span class="sxs-lookup"><span data-stu-id="1fe2f-106">hello steps in this article assume that you are familiar with developing using Node.js, and that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1fe2f-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1fe2f-107">Prerequisites</span></span>
<span data-ttu-id="1fe2f-108">Это краткое руководство использует ресурсы hello, созданные в любой из этих руководствах по в качестве отправной точки.</span><span class="sxs-lookup"><span data-stu-id="1fe2f-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="1fe2f-109">Создание базы данных с помощью портала</span><span class="sxs-lookup"><span data-stu-id="1fe2f-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="1fe2f-110">Создание базы данных SQL Azure и отправка к ней запросов с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="1fe2f-110">Create DB - CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="1fe2f-111">Также вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="1fe2f-111">You also need to:</span></span>
- <span data-ttu-id="1fe2f-112">Установите [Node.js](https://nodejs.org)</span><span class="sxs-lookup"><span data-stu-id="1fe2f-112">Install [Node.js](https://nodejs.org)</span></span>

## <a name="install-pg-client"></a><span data-ttu-id="1fe2f-113">Установка клиента pg</span><span class="sxs-lookup"><span data-stu-id="1fe2f-113">Install pg client</span></span>
<span data-ttu-id="1fe2f-114">Установите [pg](https://www.npmjs.com/package/pg), клиент PostgreSQL для Node.js.</span><span class="sxs-lookup"><span data-stu-id="1fe2f-114">Install [pg](https://www.npmjs.com/package/pg), which is a PostgreSQL client for Node.js.</span></span>

<span data-ttu-id="1fe2f-115">toodo таким образом, запустите диспетчер пакетов node hello (npm-файл) для JavaScript из клиента pg hello tooinstall командной строки.</span><span class="sxs-lookup"><span data-stu-id="1fe2f-115">toodo so, run hello node package manager (npm) for JavaScript from your command line tooinstall hello pg client.</span></span>
```bash
npm install pg
```

<span data-ttu-id="1fe2f-116">Проверка установки hello, перечисляя установленных пакетов hello.</span><span class="sxs-lookup"><span data-stu-id="1fe2f-116">Verify hello installation by listing hello packages installed.</span></span>
```bash
npm list
```

## <a name="get-connection-information"></a><span data-ttu-id="1fe2f-117">Получение сведений о подключении</span><span class="sxs-lookup"><span data-stu-id="1fe2f-117">Get connection information</span></span>
<span data-ttu-id="1fe2f-118">Получите toohello tooconnect базы данных Azure для hello подключения сведения, необходимые для PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="1fe2f-118">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="1fe2f-119">Необходимо hello server полное имя и учетные данные входа.</span><span class="sxs-lookup"><span data-stu-id="1fe2f-119">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="1fe2f-120">Войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1fe2f-120">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="1fe2f-121">Hello левого меню на портале Azure, щелкните **все ресурсы** и найдите только что созданный сервер hello.</span><span class="sxs-lookup"><span data-stu-id="1fe2f-121">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you just created.</span></span>
3. <span data-ttu-id="1fe2f-122">Щелкните имя сервера hello.</span><span class="sxs-lookup"><span data-stu-id="1fe2f-122">Click hello server name.</span></span>
4. <span data-ttu-id="1fe2f-123">Выберите hello server **Обзор** страницы.</span><span class="sxs-lookup"><span data-stu-id="1fe2f-123">Select hello server's **Overview** page.</span></span> <span data-ttu-id="1fe2f-124">Запишите hello **имя сервера** и **имя входа администратора сервера**.</span><span class="sxs-lookup"><span data-stu-id="1fe2f-124">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="1fe2f-125">![База данных Azure для PostgreSQL. Учетные данные администратора сервера для входа](./media/connect-nodejs/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="1fe2f-125">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-nodejs/1-connection-string.png)</span></span>
5. <span data-ttu-id="1fe2f-126">Если вы забыли учетные данные входа сервера, перейдите toohello **Обзор** страница hello tooview: имя пользователя администратора сервера и, при необходимости переустановить пароль hello.</span><span class="sxs-lookup"><span data-stu-id="1fe2f-126">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="running-hello-javascript-code-in-nodejs"></a><span data-ttu-id="1fe2f-127">Выполняет код JavaScript hello в Node.js</span><span class="sxs-lookup"><span data-stu-id="1fe2f-127">Running hello JavaScript code in Node.js</span></span>
<span data-ttu-id="1fe2f-128">Могут запускать Node.js из hello bash оболочки или окна командной строки, введя `node`, интерактивного запуска кода JavaScript в примере hello путем копирования и вставки его в строке приветствия.</span><span class="sxs-lookup"><span data-stu-id="1fe2f-128">You may launch Node.js from hello bash shell or windows command prompt by typing `node`, then run hello example JavaScript code interactively by copy and pasting it onto hello prompt.</span></span> <span data-ttu-id="1fe2f-129">Кроме того, вы можете сохранить hello код JavaScript в текстовый файл и запустите `node filename.js` с именем файла hello как toorun параметр его.</span><span class="sxs-lookup"><span data-stu-id="1fe2f-129">Alternatively, you may save hello JavaScript code into a text file and launch `node filename.js` with hello file name as a parameter toorun it.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="1fe2f-130">Подключение, создание таблицы и вставка данных</span><span class="sxs-lookup"><span data-stu-id="1fe2f-130">Connect, create table, and insert data</span></span>
<span data-ttu-id="1fe2f-131">Используйте следующие hello кода tooconnect и загружать данные при помощи hello **CREATE TABLE** и **INSERT INTO** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="1fe2f-131">Use hello following code tooconnect and load hello data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span>
<span data-ttu-id="1fe2f-132">Hello [pg. Клиент](https://github.com/brianc/node-postgres/wiki/Client) объект является используется toointerface с сервером PostgreSQL hello.</span><span class="sxs-lookup"><span data-stu-id="1fe2f-132">hello [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used toointerface with hello PostgreSQL server.</span></span> <span data-ttu-id="1fe2f-133">Hello [pg. Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) функция является используется tooestablish hello соединения toohello сервера.</span><span class="sxs-lookup"><span data-stu-id="1fe2f-133">hello [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="1fe2f-134">Hello [pg. Client.Query()](https://github.com/brianc/node-postgres/wiki/Query) функция является используется tooexecute hello SQL-запрос к базе данных PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="1fe2f-134">hello [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used tooexecute hello SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="1fe2f-135">Замените узел hello, dbname, пользователя и пароль параметры со значениями hello, указанный при создании hello сервера и базы данных.</span><span class="sxs-lookup"><span data-stu-id="1fe2f-135">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span>

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

## <a name="read-data"></a><span data-ttu-id="1fe2f-136">Считывание данных</span><span class="sxs-lookup"><span data-stu-id="1fe2f-136">Read data</span></span>
<span data-ttu-id="1fe2f-137">Используйте следующие hello кода tooconnect и чтения данных с помощью hello **ВЫБЕРИТЕ** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="1fe2f-137">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="1fe2f-138">Hello [pg. Клиент](https://github.com/brianc/node-postgres/wiki/Client) объект является используется toointerface с сервером PostgreSQL hello.</span><span class="sxs-lookup"><span data-stu-id="1fe2f-138">hello [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used toointerface with hello PostgreSQL server.</span></span> <span data-ttu-id="1fe2f-139">Hello [pg. Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) функция является используется tooestablish hello соединения toohello сервера.</span><span class="sxs-lookup"><span data-stu-id="1fe2f-139">hello [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="1fe2f-140">Hello [pg. Client.Query()](https://github.com/brianc/node-postgres/wiki/Query) функция является используется tooexecute hello SQL-запрос к базе данных PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="1fe2f-140">hello [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used tooexecute hello SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="1fe2f-141">Замените узел hello, dbname, пользователя и пароль параметры со значениями hello, указанный при создании hello сервера и базы данных.</span><span class="sxs-lookup"><span data-stu-id="1fe2f-141">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span> 

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
  
    console.log(`Running query tooPostgreSQL server: ${config.host}`);

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

## <a name="update-data"></a><span data-ttu-id="1fe2f-142">Обновление данных</span><span class="sxs-lookup"><span data-stu-id="1fe2f-142">Update data</span></span>
<span data-ttu-id="1fe2f-143">Используйте следующие hello кода tooconnect и чтения данных с помощью hello **обновление** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="1fe2f-143">Use hello following code tooconnect and read hello data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="1fe2f-144">Hello [pg. Клиент](https://github.com/brianc/node-postgres/wiki/Client) объект является используется toointerface с сервером PostgreSQL hello.</span><span class="sxs-lookup"><span data-stu-id="1fe2f-144">hello [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used toointerface with hello PostgreSQL server.</span></span> <span data-ttu-id="1fe2f-145">Hello [pg. Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) функция является используется tooestablish hello соединения toohello сервера.</span><span class="sxs-lookup"><span data-stu-id="1fe2f-145">hello [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="1fe2f-146">Hello [pg. Client.Query()](https://github.com/brianc/node-postgres/wiki/Query) функция является используется tooexecute hello SQL-запрос к базе данных PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="1fe2f-146">hello [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used tooexecute hello SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="1fe2f-147">Замените узел hello, dbname, пользователя и пароль параметры со значениями hello, указанный при создании hello сервера и базы данных.</span><span class="sxs-lookup"><span data-stu-id="1fe2f-147">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span> 

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

## <a name="delete-data"></a><span data-ttu-id="1fe2f-148">Удаление данных</span><span class="sxs-lookup"><span data-stu-id="1fe2f-148">Delete data</span></span>
<span data-ttu-id="1fe2f-149">Используйте следующие hello кода tooconnect и чтения данных с помощью hello **удалить** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="1fe2f-149">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> <span data-ttu-id="1fe2f-150">Hello [pg. Клиент](https://github.com/brianc/node-postgres/wiki/Client) объект является используется toointerface с сервером PostgreSQL hello.</span><span class="sxs-lookup"><span data-stu-id="1fe2f-150">hello [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used toointerface with hello PostgreSQL server.</span></span> <span data-ttu-id="1fe2f-151">Hello [pg. Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) функция является используется tooestablish hello соединения toohello сервера.</span><span class="sxs-lookup"><span data-stu-id="1fe2f-151">hello [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="1fe2f-152">Hello [pg. Client.Query()](https://github.com/brianc/node-postgres/wiki/Query) функция является используется tooexecute hello SQL-запрос к базе данных PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="1fe2f-152">hello [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used tooexecute hello SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="1fe2f-153">Замените узел hello, dbname, пользователя и пароль параметры со значениями hello, указанный при создании hello сервера и базы данных.</span><span class="sxs-lookup"><span data-stu-id="1fe2f-153">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="1fe2f-154">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1fe2f-154">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="1fe2f-155">Перенос базы данных с помощью экспорта и импорта</span><span class="sxs-lookup"><span data-stu-id="1fe2f-155">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
