---
title: "Подключение tooAzure базы данных MySQL в Python | Документы Microsoft"
description: "Это краткое руководство предоставляет несколько Python code образцы tooconnect и запроса данных из базы данных Azure можно использовать для MySQL."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: python
ms.topic: hero-article
ms.date: 07/12/2017
ms.openlocfilehash: 9df5211adcab886a502fd138347aed8fb587cd5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-python-tooconnect-and-query-data"></a>База данных Azure для MySQL: использование Python tooconnect и запроса данных
Это краткое руководство демонстрирует, как toouse [Python](https://python.org) tooconnect tooan базы данных Azure для MySQL. В нем tooquery инструкций SQL, insert, update и delete данных в базе данных hello из платформ Mac OS, Ubuntu Linux и Windows. Hello в этой статье предполагается, что представление о разработке с помощью Python и являются новый tooworking с базой данных Azure для MySQL.

## <a name="prerequisites"></a>Предварительные требования
Это краткое руководство использует ресурсы hello, созданные в любой из этих руководствах по в качестве отправной точки.
- [Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Создание сервера базы данных Azure для MySQL с помощью портала Azure)
- [Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md) (Создание сервера базы данных Azure для MySQL с помощью Azure CLI)

## <a name="install-python-and-hello-mysql-connector"></a>Установка Python и hello соединителя MySQL
Установка [Python](https://www.python.org/downloads/) и hello [соединитель MySQL для Python](https://dev.mysql.com/downloads/connector/python/) на компьютере. В зависимости от используемой платформы выполните действия hello.

### <a name="windows"></a>Windows
1. Скачайте и установите Python 2.7 с веб-сайта [python.org](https://www.python.org/downloads/windows/). 
2. Проверьте установки Python hello, запустив hello командной строки. Выполните команду hello `C:\python27\python.exe -V` с помощью hello прописные V коммутатора toosee hello номер версии.
3. Установка соединителя hello Python для MySQL из [mysql.com](https://dev.mysql.com/downloads/connector/python/) соответствующую версию tooyour Python.

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
1. В Linux (Ubuntu) Python обычно устанавливается как часть установки по умолчанию hello.
2. Проверьте установки Python hello путем запуска команд bash hello. Выполните команду hello `python -V` с помощью hello прописные V коммутатора toosee hello номер версии.
3. Проверьте установку PIP hello, запустив hello `pip show pip -V` команды номер версии toosee hello. 
4. PIP может быть включен в некоторых версиях Python. Если PIP не установлен, может потребоваться установить hello [PIP] (https://pip.pypa.io/en/stable/installing/) пакета, выполнив команду `sudo apt-get install python-pip`.
5. Обновление PIP toohello последней версии, выполнив hello `pip install -U pip` команды.
6. Установите соединитель MySQL hello Python и его зависимостей с помощью команды hello PIP-адрес:

   ```bash
   sudo pip install mysql-connector-python-rf
   ```
 
### <a name="macos"></a>MacOS
1. В Mac OS Python обычно устанавливается как часть установки операционной системы по умолчанию hello.
2. Проверьте установки Python hello путем запуска команд bash hello. Выполните команду hello `python -V` с помощью hello прописные V коммутатора toosee hello номер версии.
3. Проверьте установку PIP hello, запустив hello `pip show pip -V` команды номер версии toosee hello.
4. PIP может быть включен в некоторых версиях Python. Если PIP не установлен, может потребоваться установить hello [PIP](https://pip.pypa.io/en/stable/installing/) пакета.
5. Обновление PIP toohello последней версии, выполнив hello `pip install -U pip` команды.
6. Установите соединитель MySQL hello Python и его зависимостей с помощью команды hello PIP-адрес:

   ```bash
   pip install mysql-connector-python-rf
   ```

## <a name="get-connection-information"></a>Получение сведений о подключении
Получите toohello tooconnect базы данных Azure для hello подключения сведения, необходимые для MySQL. Необходимо hello server полное имя и учетные данные входа.

1. Войдите в toohello [портал Azure](https://portal.azure.com/).
2. Hello левого меню на портале Azure, щелкните **все ресурсы** и выполните поиск сервера hello, можно creased, такие как **myserver4demo**.
3. Щелкните имя сервера hello **myserver4demo**.
4. Выберите hello server **свойства** страницы. Запишите hello **имя сервера** и **имя входа администратора сервера**.
 ![Имя входа для администратора сервера в базе данных Azure для MySQL](./media/connect-python/1_server-properties-name-login.png)
5. Если вы забыли учетные данные входа сервера, перейдите toohello **Обзор** страница hello tooview: имя пользователя администратора сервера и, при необходимости переустановить пароль hello.
   

## <a name="run-python-code"></a>Выполнение кода Python
- Вставьте код hello в текстовый файл и сохраните файл hello в проект папку с .py расширение файла, например C:\pythonmysql\createtable.py или /home/username/pythonmysql/createtable.py
- toorun hello кода, запустите командную строку hello или bash оболочки. Перейдите в папку проекта `cd pythonmysql`. Затем введите команду hello python, за которым следует имя файла hello `python createtable.py` toorun приложения hello. На hello ОС Windows Если python.exe не найден, вы может предоставить hello полный путь toohello исполняемый файл или добавить hello Python путь в переменной среды path hello. `C:\python27\python.exe createtable.py`

## <a name="connect-create-table-and-insert-data"></a>Подключение, создание таблицы и вставка данных
Используйте следующие hello кода tooconnect toohello сервера, создайте таблицу и загружать данные при помощи hello **вставить** инструкции SQL. 

В коде hello импорта библиотеки mysql.connector hello. Hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) функция является tooAzure используется tooconnect базы данных MySQL с помощью hello [аргументы соединения](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) в коллекции конфигурации hello. Hello код использует курсор для соединения hello и [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) метод выполняет запрос SQL hello в базу данных MySQL. 

Замените hello `host`, `user`, `password`, и `database` параметров со значениями hello, указанный при создании hello сервера и базы данных.

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from hello portal
config = {
  'host':'myserver4demo.mysql.database.azure.com',
  'user':'myadmin@myserver4demo',
  'password':'yourpassword',
  'database':'quickstartdb'
}

# Construct connection string
try:
   conn = mysql.connector.connect(**config)
   print("Connection established")
except mysql.connector.Error as err:
  if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
    print("Something is wrong with hello user name or password")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Drop previous table of same name if one exists
  cursor.execute("DROP TABLE IF EXISTS inventory;")
  print("Finished dropping table (if existed).")

  # Create table
  cursor.execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);")
  print("Finished creating table.")

  # Insert some data into table
  cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("banana", 150))
  print("Inserted",cursor.rowcount,"row(s) of data.")
  cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("orange", 154))
  print("Inserted",cursor.rowcount,"row(s) of data.")
  cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("apple", 100))
  print("Inserted",cursor.rowcount,"row(s) of data.")

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="read-data"></a>Считывание данных
Используйте следующие hello кода tooconnect и чтения данных с помощью hello **ВЫБЕРИТЕ** инструкции SQL. 

В коде hello импорта библиотеки mysql.connector hello. Hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) функция является tooAzure используется tooconnect базы данных MySQL с помощью hello [аргументы соединения](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) в коллекции конфигурации hello. Hello код использует курсор для соединения hello и [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) метод выполняет hello инструкции SQL для базы данных MySQL. строки данных Hello считываются с использованием hello [fetchall()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-fetchall.html) метод. Hello результирующий набор хранится в строке коллекции и для итератора используется tooloop по строкам hello.

Замените hello `host`, `user`, `password`, и `database` параметров со значениями hello, указанный при создании hello сервера и базы данных.

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from hello portal
config = {
  'host':'myserver4demo.mysql.database.azure.com',
  'user':'myadmin@myserver4demo',
  'password':'yourpassword',
  'database':'quickstartdb'
}

# Construct connection string
try:
   conn = mysql.connector.connect(**config)
   print("Connection established")
except mysql.connector.Error as err:
  if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
    print("Something is wrong with hello user name or password")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Read data
  cursor.execute("SELECT * FROM inventory;")
  rows = cursor.fetchall()
  print("Read",cursor.rowcount,"row(s) of data.")

  # Print all rows
  for row in rows:
    print("Data row = (%s, %s, %s)" %(str(row[0]), str(row[1]), str(row[2])))

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="update-data"></a>Обновление данных
Используйте следующие hello кода tooconnect и обновления данных с помощью hello **обновление** инструкции SQL. 

В коде hello импорта библиотеки mysql.connector hello.  Hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) функция является tooAzure используется tooconnect базы данных MySQL с помощью hello [аргументы соединения](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) в коллекции конфигурации hello. Hello код использует курсор для соединения hello и [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) метод выполняет hello инструкции SQL для базы данных MySQL. 

Замените hello `host`, `user`, `password`, и `database` параметров со значениями hello, указанный при создании hello сервера и базы данных.

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from hello portal
config = {
  'host':'myserver4demo.mysql.database.azure.com',
  'user':'myadmin@myserver4demo',
  'password':'yourpassword',
  'database':'quickstartdb'
}

# Construct connection string
try:
   conn = mysql.connector.connect(**config)
   print("Connection established")
except mysql.connector.Error as err:
  if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
    print("Something is wrong with hello user name or password")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Update a data row in hello table
  cursor.execute("UPDATE inventory SET quantity = %s WHERE name = %s;", (200, "banana"))
  print("Updated",cursor.rowcount,"row(s) of data.")

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="delete-data"></a>Удаление данных
Используйте следующие hello кода tooconnect и удаление данных с помощью **удалить** инструкции SQL. 

В коде hello импорта библиотеки mysql.connector hello.  Hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) функция является tooAzure используется tooconnect базы данных MySQL с помощью hello [аргументы соединения](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) в коллекции конфигурации hello. Hello код использует курсор для соединения hello и [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) метод выполняет запрос SQL hello в базу данных MySQL. 

Замените hello `host`, `user`, `password`, и `database` параметров со значениями hello, указанный при создании hello сервера и базы данных.

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from hello portal
config = {
  'host':'myserver4demo.mysql.database.azure.com',
  'user':'myadmin@myserver4demo',
  'password':'yourpassword',
  'database':'quickstartdb'
}

# Construct connection string
try:
   conn = mysql.connector.connect(**config)
   print("Connection established.")
except mysql.connector.Error as err:
  if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
    print("Something is wrong with hello user name or password.")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist.")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Delete a data row in hello table
  cursor.execute("DELETE FROM inventory WHERE name=%(param1)s;", {'param1':"orange"})
  print("Deleted",cursor.rowcount,"row(s) of data.")

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="next-steps"></a>Дальнейшие действия
> [!div class="nextstepaction"]
> [Перенос базы данных с помощью экспорта и импорта](./concepts-migrate-import-export.md)
