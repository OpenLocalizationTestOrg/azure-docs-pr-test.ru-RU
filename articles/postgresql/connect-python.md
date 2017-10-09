---
title: "Подключение tooAzure базы данных PostgreSQL из Python | Документы Microsoft"
description: "Это краткое руководство содержит пример кода Python, можно использовать tooconnect и запроса данных из базы данных Azure для PostgreSQL."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: python
ms.topic: quickstart
ms.date: 08/15/2017
ms.openlocfilehash: 7d6d9f5424fb39ad8837999d4788b4363c818887
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-python-tooconnect-and-query-data"></a><span data-ttu-id="656e5-103">База данных Azure для PostgreSQL: использование Python tooconnect и запроса данных</span><span class="sxs-lookup"><span data-stu-id="656e5-103">Azure Database for PostgreSQL: Use Python tooconnect and query data</span></span>
<span data-ttu-id="656e5-104">Это краткое руководство демонстрирует, как toouse [Python](https://python.org) tooconnect tooan базы данных Azure для PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="656e5-104">This quickstart demonstrates how toouse [Python](https://python.org) tooconnect tooan Azure Database for PostgreSQL.</span></span> <span data-ttu-id="656e5-105">Здесь также показано, как tooquery инструкций SQL toouse, вставка, обновление и удаление данных в базе данных hello из платформ Windows, macOS и Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="656e5-105">It also demonstrates how toouse SQL statements tooquery, insert, update, and delete data in hello database from macOS, Ubuntu Linux, and Windows platforms.</span></span> <span data-ttu-id="656e5-106">Hello в этой статье предполагается, что представление о разработке с помощью Python и являются новый tooworking с базой данных Azure для PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="656e5-106">hello steps in this article assume that you are familiar with developing using Python and are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="656e5-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="656e5-107">Prerequisites</span></span>
<span data-ttu-id="656e5-108">Это краткое руководство использует ресурсы hello, созданные в любой из этих руководствах по в качестве отправной точки.</span><span class="sxs-lookup"><span data-stu-id="656e5-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="656e5-109">Создание базы данных с помощью портала</span><span class="sxs-lookup"><span data-stu-id="656e5-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="656e5-110">Создание базы данных SQL Azure и отправка к ней запросов с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="656e5-110">Create DB - CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="656e5-111">Кроме того, вам понадобится следующее:</span><span class="sxs-lookup"><span data-stu-id="656e5-111">You also need:</span></span>
- <span data-ttu-id="656e5-112">установить [Python](https://www.python.org/downloads/);</span><span class="sxs-lookup"><span data-stu-id="656e5-112">[python](https://www.python.org/downloads/) installed</span></span>
- <span data-ttu-id="656e5-113">Установить пакет [pip](https://pip.pypa.io/en/stable/installing/) (он уже установлен, если вы используете двоичные файлы Python 2 >=2.7.9 или Python 3 >= 3.4, скачанные с сайта [python.org](https://python.org)).</span><span class="sxs-lookup"><span data-stu-id="656e5-113">[pip](https://pip.pypa.io/en/stable/installing/) package installed (pip is already installed if you're working with Python 2 >=2.7.9 or Python 3 >=3.4 binaries downloaded from [python.org](https://python.org).</span></span>

## <a name="install-hello-python-connection-libraries-for-postgresql"></a><span data-ttu-id="656e5-114">Установка библиотеки подключений к hello Python для PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="656e5-114">Install hello Python connection libraries for PostgreSQL</span></span>
<span data-ttu-id="656e5-115">Установка hello [psycopg2](http://initd.org/psycopg/docs/install.html) пакет, который позволяет tooconnect и запрос hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="656e5-115">Install hello [psycopg2](http://initd.org/psycopg/docs/install.html) package, which enables you tooconnect and query hello database.</span></span> <span data-ttu-id="656e5-116">— psycopg2 [на PyPI](https://pypi.python.org/pypi/psycopg2/) в форме hello [колесика](http://pythonwheels.com/) пакетов для наиболее распространенных платформ hello (Linux OSX, Windows).</span><span class="sxs-lookup"><span data-stu-id="656e5-116">psycopg2 is [available on PyPI](https://pypi.python.org/pypi/psycopg2/) in hello form of [wheel](http://pythonwheels.com/) packages for hello most common platforms (Linux, OSX, Windows).</span></span> <span data-ttu-id="656e5-117">Использование pip установить tooget hello двоичная версия модуля hello, включая все зависимости hello.</span><span class="sxs-lookup"><span data-stu-id="656e5-117">Use pip install tooget hello binary version of hello module including all hello dependencies.</span></span>

1. <span data-ttu-id="656e5-118">На своем компьютере запустите интерфейс командной строки:</span><span class="sxs-lookup"><span data-stu-id="656e5-118">On your own computer, launch a command-line interface:</span></span>
    - <span data-ttu-id="656e5-119">В Linux запустите консоль Bash hello.</span><span class="sxs-lookup"><span data-stu-id="656e5-119">On Linux, launch hello Bash shell.</span></span>
    - <span data-ttu-id="656e5-120">На macOS запустите hello терминалов.</span><span class="sxs-lookup"><span data-stu-id="656e5-120">On macOS, launch hello Terminal.</span></span>
    - <span data-ttu-id="656e5-121">В Windows запустите hello командную строку из меню "Пуск" hello.</span><span class="sxs-lookup"><span data-stu-id="656e5-121">On Windows, launch hello Command Prompt from hello Start Menu.</span></span>
2. <span data-ttu-id="656e5-122">Убедитесь, что вы используете последнюю версию hello pip при выполнении определенной команды, такие как:</span><span class="sxs-lookup"><span data-stu-id="656e5-122">Ensure that you are using hello most current version of pip by running a command such as:</span></span>
    ```cmd
    pip install -U pip
    ```

3. <span data-ttu-id="656e5-123">Следующая команда tooinstall hello psycopg2 пакет выполнения hello:</span><span class="sxs-lookup"><span data-stu-id="656e5-123">Run hello following command tooinstall hello psycopg2 package:</span></span>
    ```cmd
    pip install psycopg2
    ```

## <a name="get-connection-information"></a><span data-ttu-id="656e5-124">Получение сведений о подключении</span><span class="sxs-lookup"><span data-stu-id="656e5-124">Get connection information</span></span>
<span data-ttu-id="656e5-125">Получите toohello tooconnect базы данных Azure для hello подключения сведения, необходимые для PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="656e5-125">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="656e5-126">Необходимо hello server полное имя и учетные данные входа.</span><span class="sxs-lookup"><span data-stu-id="656e5-126">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="656e5-127">Войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="656e5-127">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="656e5-128">Hello левого меню на портале Azure, щелкните **все ресурсы** и выполните поиск **mypgserver 20170401** (hello server только что созданную).</span><span class="sxs-lookup"><span data-stu-id="656e5-128">From hello left-hand menu in Azure portal, click **All resources** and search for **mypgserver-20170401** (hello server you just created).</span></span>
3. <span data-ttu-id="656e5-129">Щелкните имя сервера hello **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="656e5-129">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="656e5-130">Выберите hello server **Обзор** страницы, а затем запишите hello **имя сервера** и **имя входа администратора сервера**.</span><span class="sxs-lookup"><span data-stu-id="656e5-130">Select hello server's **Overview** page, and then make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="656e5-131">![База данных Azure для PostgreSQL. Учетные данные администратора сервера для входа](./media/connect-python/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="656e5-131">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-python/1-connection-string.png)</span></span>
5. <span data-ttu-id="656e5-132">Если вы забыли учетные данные входа сервера, перейдите toohello **Обзор** страница hello tooview: имя пользователя администратора сервера и, при необходимости переустановить пароль hello.</span><span class="sxs-lookup"><span data-stu-id="656e5-132">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="how-toorun-python-code"></a><span data-ttu-id="656e5-133">Как toorun кода Python</span><span class="sxs-lookup"><span data-stu-id="656e5-133">How toorun Python code</span></span>
<span data-ttu-id="656e5-134">В этом разделе содержится всего четыре образца кода, каждый из которых выполняет определенную функцию.</span><span class="sxs-lookup"><span data-stu-id="656e5-134">This topic contains a total of four code samples, each of which performs a specific function.</span></span> <span data-ttu-id="656e5-135">Hello следующие инструкции показывают как toocreate текстовый файл, Вставить блок кода, а затем сохраните файл hello, чтобы выполнить его позже.</span><span class="sxs-lookup"><span data-stu-id="656e5-135">hello following instructions indicate how toocreate a text file, insert a code block, and then save hello file so that you can run it later.</span></span> <span data-ttu-id="656e5-136">Быть убедиться, что toocreate четыре отдельных файлов, по одному для каждого блока кода.</span><span class="sxs-lookup"><span data-stu-id="656e5-136">Be sure toocreate four separate files, one for each code block.</span></span>

- <span data-ttu-id="656e5-137">С помощью предпочитаемого текстового редактора создайте файл.</span><span class="sxs-lookup"><span data-stu-id="656e5-137">Using your favorite text editor, create a new file.</span></span>
- <span data-ttu-id="656e5-138">Скопируйте и вставьте один из примеров кода hello в следующих разделах в текстовый файл hello hello.</span><span class="sxs-lookup"><span data-stu-id="656e5-138">Copy and paste one of hello code samples in hello following sections into hello text file.</span></span> <span data-ttu-id="656e5-139">Замените hello **узла**, **dbname**, **пользователя**, и **пароль** параметров со значениями hello, указанный при создании hello сервер и базу данных.</span><span class="sxs-lookup"><span data-stu-id="656e5-139">Replace hello **host**, **dbname**, **user**, and **password** parameters with hello values that you specified when you created hello server and database.</span></span>
- <span data-ttu-id="656e5-140">Сохраните hello файл с расширением .py hello (например postgres.py) в папку проекта.</span><span class="sxs-lookup"><span data-stu-id="656e5-140">Save hello file with hello .py extension (for example postgres.py) into your project folder.</span></span> <span data-ttu-id="656e5-141">Если вы используете Операционную систему Windows hello, быть убедиться, что tooselect кодировку UTF-8 при сохранении файла hello.</span><span class="sxs-lookup"><span data-stu-id="656e5-141">If you are running hello Windows OS, be sure tooselect UTF-8 encoding when saving hello file.</span></span> 
- <span data-ttu-id="656e5-142">Запустите консоль командной строки или Bash hello и изменить папку проекта tooyour hello каталога, например `cd postgres`.</span><span class="sxs-lookup"><span data-stu-id="656e5-142">Launch hello Command Prompt or Bash shell and then change hello directory tooyour project folder, for example `cd postgres`.</span></span>
-  <span data-ttu-id="656e5-143">Код toorun hello, тип hello команда Python, затем по имени файла hello, например `Python postgres.py`.</span><span class="sxs-lookup"><span data-stu-id="656e5-143">toorun hello code, type hello Python command followed by hello file name, for example `Python postgres.py`.</span></span>

> [!NOTE]
> <span data-ttu-id="656e5-144">Начиная с версии 3 Python, может появиться ошибка hello `SyntaxError: Missing parentheses in call too'print'` при выполнении следующих блоков кода hello.</span><span class="sxs-lookup"><span data-stu-id="656e5-144">Starting in Python version 3, you may see hello error `SyntaxError: Missing parentheses in call too'print'` when running hello following code blocks.</span></span> <span data-ttu-id="656e5-145">В этом случае замените каждую команду вызова toohello `print "string"` с помощью вызова функции с помощью скобок, например `print("string")`.</span><span class="sxs-lookup"><span data-stu-id="656e5-145">If that happens, replace each call toohello command `print "string"` with a function call using parenthesis, such as `print("string")`.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="656e5-146">Подключение, создание таблицы и вставка данных</span><span class="sxs-lookup"><span data-stu-id="656e5-146">Connect, create table, and insert data</span></span>
<span data-ttu-id="656e5-147">Используйте следующие hello кода tooconnect и загружать данные при помощи hello [psycopg2.connect](http://initd.org/psycopg/docs/connection.html) функционировать с **вставить** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="656e5-147">Use hello following code tooconnect and load hello data using [psycopg2.connect](http://initd.org/psycopg/docs/connection.html) function with **INSERT** SQL statement.</span></span> <span data-ttu-id="656e5-148">Hello [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) функция является используется tooexecute hello SQL-запрос к базе данных PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="656e5-148">hello [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function is used tooexecute hello SQL query against PostgreSQL database.</span></span> <span data-ttu-id="656e5-149">Замените узел hello, dbname, пользователя и пароль параметры со значениями hello, указанный при создании hello сервера и базы данных.</span><span class="sxs-lookup"><span data-stu-id="656e5-149">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from hello portal
host = "mypgserver-20170401.postgres.database.azure.com"
user = "mylogin@mypgserver-20170401"
dbname = "mypgsqldb"
password = "<server_admin_password>"
sslmode = "require"

# Construct connection string
conn_string = "host={0} user={1} dbname={2} password={3} sslmode={4}".format(host, user, dbname, password, sslmode)
conn = psycopg2.connect(conn_string) 
print "Connection established"

cursor = conn.cursor()

# Drop previous table of same name if one exists
cursor.execute("DROP TABLE IF EXISTS inventory;")
print "Finished dropping table (if existed)"

# Create table
cursor.execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);")
print "Finished creating table"

# Insert some data into table
cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("banana", 150))
cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("orange", 154))
cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("apple", 100))
print "Inserted 3 rows of data"

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

<span data-ttu-id="656e5-150">После кода hello выполнен успешно, hello получается следующий результат:</span><span class="sxs-lookup"><span data-stu-id="656e5-150">After hello code runs successfully, hello output appears as follows:</span></span>

![Выходные данные командной строки](media/connect-python/2-example-python-output.png)

## <a name="read-data"></a><span data-ttu-id="656e5-152">Считывание данных</span><span class="sxs-lookup"><span data-stu-id="656e5-152">Read data</span></span>
<span data-ttu-id="656e5-153">Используйте hello следующий код tooread hello вставленные данные с помощью [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) функционировать с **ВЫБЕРИТЕ** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="656e5-153">Use hello following code tooread hello data inserted using [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function with **SELECT** SQL statement.</span></span> <span data-ttu-id="656e5-154">Эта функция принимает запрос и возвращает результирующий набор, доступная для итерации с использованием hello [cursor.fetchall()](http://initd.org/psycopg/docs/cursor.html#cursor.fetchall).</span><span class="sxs-lookup"><span data-stu-id="656e5-154">This function accepts a query and returns a result set that can be iterated over with hello use of [cursor.fetchall()](http://initd.org/psycopg/docs/cursor.html#cursor.fetchall).</span></span> <span data-ttu-id="656e5-155">Замените узел hello, dbname, пользователя и пароль параметры со значениями hello, указанный при создании hello сервера и базы данных.</span><span class="sxs-lookup"><span data-stu-id="656e5-155">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from hello portal
host = "mypgserver-20170401.postgres.database.azure.com"
user = "mylogin@mypgserver-20170401"
dbname = "mypgsqldb"
password = "<server_admin_password>"
sslmode = "require"

# Construct connection string
conn_string = "host={0} user={1} dbname={2} password={3} sslmode={4}".format(host, user, dbname, password, sslmode)
conn = psycopg2.connect(conn_string) 
print "Connection established"

cursor = conn.cursor()

# Fetch all rows from table
cursor.execute("SELECT * FROM inventory;")
rows = cursor.fetchall()

# Print all rows
for row in rows:
    print "Data row = (%s, %s, %s)" %(str(row[0]), str(row[1]), str(row[2]))

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

## <a name="update-data"></a><span data-ttu-id="656e5-156">Обновление данных</span><span class="sxs-lookup"><span data-stu-id="656e5-156">Update data</span></span>
<span data-ttu-id="656e5-157">Используйте hello следующий код tooupdate hello инвентаризации строки, добавленного ранее с помощью [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) функционировать с **обновление** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="656e5-157">Use hello following code tooupdate hello inventory row that you previously inserted using [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function with **UPDATE** SQL statement.</span></span> <span data-ttu-id="656e5-158">Замените узел hello, dbname, пользователя и пароль параметры со значениями hello, указанный при создании hello сервера и базы данных.</span><span class="sxs-lookup"><span data-stu-id="656e5-158">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from hello portal
host = "mypgserver-20170401.postgres.database.azure.com"
user = "mylogin@mypgserver-20170401"
dbname = "mypgsqldb"
password = "<server_admin_password>"
sslmode = "require"

# Construct connection string
conn_string = "host={0} user={1} dbname={2} password={3} sslmode={4}".format(host, user, dbname, password, sslmode)
conn = psycopg2.connect(conn_string) 
print "Connection established"

cursor = conn.cursor()

# Update a data row in hello table
cursor.execute("UPDATE inventory SET quantity = %s WHERE name = %s;", (200, "banana"))
print "Updated 1 row of data"

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

## <a name="delete-data"></a><span data-ttu-id="656e5-159">Удаление данных</span><span class="sxs-lookup"><span data-stu-id="656e5-159">Delete data</span></span>
<span data-ttu-id="656e5-160">Используйте hello следующий код товара добавленного ранее с помощью toodelete [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) функционировать с **удалить** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="656e5-160">Use hello following code toodelete an inventory item that you previously inserted using [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function with **DELETE** SQL statement.</span></span> <span data-ttu-id="656e5-161">Замените узел hello, dbname, пользователя и пароль параметры со значениями hello, указанный при создании hello сервера и базы данных.</span><span class="sxs-lookup"><span data-stu-id="656e5-161">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from hello portal
host = "mypgserver-20170401.postgres.database.azure.com"
user = "mylogin@mypgserver-20170401"
dbname = "mypgsqldb"
password = "<server_admin_password>"
sslmode = "require"

# Construct connection string
conn_string = "host={0} user={1} dbname={2} password={3} sslmode={4}".format(host, user, dbname, password, sslmode)
conn = psycopg2.connect(conn_string) 
print "Connection established"

cursor = conn.cursor()

# Delete data row from table
cursor.execute("DELETE FROM inventory WHERE name = %s;", ("orange",))
print "Deleted 1 row of data"

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

## <a name="next-steps"></a><span data-ttu-id="656e5-162">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="656e5-162">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="656e5-163">Перенос базы данных с помощью экспорта и импорта</span><span class="sxs-lookup"><span data-stu-id="656e5-163">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
