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
# <a name="azure-database-for-postgresql-use-python-tooconnect-and-query-data"></a>База данных Azure для PostgreSQL: использование Python tooconnect и запроса данных
Это краткое руководство демонстрирует, как toouse [Python](https://python.org) tooconnect tooan базы данных Azure для PostgreSQL. Здесь также показано, как tooquery инструкций SQL toouse, вставка, обновление и удаление данных в базе данных hello из платформ Windows, macOS и Ubuntu Linux. Hello в этой статье предполагается, что представление о разработке с помощью Python и являются новый tooworking с базой данных Azure для PostgreSQL.

## <a name="prerequisites"></a>Предварительные требования
Это краткое руководство использует ресурсы hello, созданные в любой из этих руководствах по в качестве отправной точки.
- [Создание базы данных с помощью портала](quickstart-create-server-database-portal.md)
- [Создание базы данных SQL Azure и отправка к ней запросов с помощью Azure CLI](quickstart-create-server-database-azure-cli.md)

Кроме того, вам понадобится следующее:
- установить [Python](https://www.python.org/downloads/);
- Установить пакет [pip](https://pip.pypa.io/en/stable/installing/) (он уже установлен, если вы используете двоичные файлы Python 2 >=2.7.9 или Python 3 >= 3.4, скачанные с сайта [python.org](https://python.org)).

## <a name="install-hello-python-connection-libraries-for-postgresql"></a>Установка библиотеки подключений к hello Python для PostgreSQL
Установка hello [psycopg2](http://initd.org/psycopg/docs/install.html) пакет, который позволяет tooconnect и запрос hello базы данных. — psycopg2 [на PyPI](https://pypi.python.org/pypi/psycopg2/) в форме hello [колесика](http://pythonwheels.com/) пакетов для наиболее распространенных платформ hello (Linux OSX, Windows). Использование pip установить tooget hello двоичная версия модуля hello, включая все зависимости hello.

1. На своем компьютере запустите интерфейс командной строки:
    - В Linux запустите консоль Bash hello.
    - На macOS запустите hello терминалов.
    - В Windows запустите hello командную строку из меню "Пуск" hello.
2. Убедитесь, что вы используете последнюю версию hello pip при выполнении определенной команды, такие как:
    ```cmd
    pip install -U pip
    ```

3. Следующая команда tooinstall hello psycopg2 пакет выполнения hello:
    ```cmd
    pip install psycopg2
    ```

## <a name="get-connection-information"></a>Получение сведений о подключении
Получите toohello tooconnect базы данных Azure для hello подключения сведения, необходимые для PostgreSQL. Необходимо hello server полное имя и учетные данные входа.

1. Войдите в toohello [портал Azure](https://portal.azure.com/).
2. Hello левого меню на портале Azure, щелкните **все ресурсы** и выполните поиск **mypgserver 20170401** (hello server только что созданную).
3. Щелкните имя сервера hello **mypgserver 20170401**.
4. Выберите hello server **Обзор** страницы, а затем запишите hello **имя сервера** и **имя входа администратора сервера**.
 ![База данных Azure для PostgreSQL. Учетные данные администратора сервера для входа](./media/connect-python/1-connection-string.png)
5. Если вы забыли учетные данные входа сервера, перейдите toohello **Обзор** страница hello tooview: имя пользователя администратора сервера и, при необходимости переустановить пароль hello.

## <a name="how-toorun-python-code"></a>Как toorun кода Python
В этом разделе содержится всего четыре образца кода, каждый из которых выполняет определенную функцию. Hello следующие инструкции показывают как toocreate текстовый файл, Вставить блок кода, а затем сохраните файл hello, чтобы выполнить его позже. Быть убедиться, что toocreate четыре отдельных файлов, по одному для каждого блока кода.

- С помощью предпочитаемого текстового редактора создайте файл.
- Скопируйте и вставьте один из примеров кода hello в следующих разделах в текстовый файл hello hello. Замените hello **узла**, **dbname**, **пользователя**, и **пароль** параметров со значениями hello, указанный при создании hello сервер и базу данных.
- Сохраните hello файл с расширением .py hello (например postgres.py) в папку проекта. Если вы используете Операционную систему Windows hello, быть убедиться, что tooselect кодировку UTF-8 при сохранении файла hello. 
- Запустите консоль командной строки или Bash hello и изменить папку проекта tooyour hello каталога, например `cd postgres`.
-  Код toorun hello, тип hello команда Python, затем по имени файла hello, например `Python postgres.py`.

> [!NOTE]
> Начиная с версии 3 Python, может появиться ошибка hello `SyntaxError: Missing parentheses in call too'print'` при выполнении следующих блоков кода hello. В этом случае замените каждую команду вызова toohello `print "string"` с помощью вызова функции с помощью скобок, например `print("string")`.

## <a name="connect-create-table-and-insert-data"></a>Подключение, создание таблицы и вставка данных
Используйте следующие hello кода tooconnect и загружать данные при помощи hello [psycopg2.connect](http://initd.org/psycopg/docs/connection.html) функционировать с **вставить** инструкции SQL. Hello [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) функция является используется tooexecute hello SQL-запрос к базе данных PostgreSQL. Замените узел hello, dbname, пользователя и пароль параметры со значениями hello, указанный при создании hello сервера и базы данных.

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

После кода hello выполнен успешно, hello получается следующий результат:

![Выходные данные командной строки](media/connect-python/2-example-python-output.png)

## <a name="read-data"></a>Считывание данных
Используйте hello следующий код tooread hello вставленные данные с помощью [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) функционировать с **ВЫБЕРИТЕ** инструкции SQL. Эта функция принимает запрос и возвращает результирующий набор, доступная для итерации с использованием hello [cursor.fetchall()](http://initd.org/psycopg/docs/cursor.html#cursor.fetchall). Замените узел hello, dbname, пользователя и пароль параметры со значениями hello, указанный при создании hello сервера и базы данных.

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

## <a name="update-data"></a>Обновление данных
Используйте hello следующий код tooupdate hello инвентаризации строки, добавленного ранее с помощью [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) функционировать с **обновление** инструкции SQL. Замените узел hello, dbname, пользователя и пароль параметры со значениями hello, указанный при создании hello сервера и базы данных.

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

## <a name="delete-data"></a>Удаление данных
Используйте hello следующий код товара добавленного ранее с помощью toodelete [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) функционировать с **удалить** инструкции SQL. Замените узел hello, dbname, пользователя и пароль параметры со значениями hello, указанный при создании hello сервера и базы данных.

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

## <a name="next-steps"></a>Дальнейшие действия
> [!div class="nextstepaction"]
> [Перенос базы данных с помощью экспорта и импорта](./howto-migrate-using-export-and-import.md)
