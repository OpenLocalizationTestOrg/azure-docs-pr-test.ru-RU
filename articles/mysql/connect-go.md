---
title: "Подключение tooAzure базы данных MySQL с помощью Go | Документы Microsoft"
description: "Это краткое руководство входит несколько примеров кода Go можно использовать tooconnect и запроса данных из базы данных Azure для MySQL."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: go
ms.topic: hero-article
ms.date: 07/18/2017
ms.openlocfilehash: e8067b807ee729e04850c5325f476806bcd54983
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-go-language-tooconnect-and-query-data"></a>База данных Azure для MySQL: используют команду Go языка tooconnect и запроса данных
Краткого руководства показано, как tooan tooconnect базы данных Azure для MySQL с помощью кода hello написаны в [Go](https://golang.org/) язык, на основе Windows, Ubuntu Linux и Apple macOS платформы. Показано, как tooquery инструкций SQL toouse, вставка, обновление и удаление данных в базе данных hello. В этой статье предполагается, что вы знакомы с разработкой, с помощью команды Go, но, чтобы новый tooworking с базой данных Azure для MySQL.

## <a name="prerequisites"></a>Предварительные требования
Это краткое руководство использует ресурсы hello, созданные в любой из этих руководствах по в качестве отправной точки.
- [Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Создание сервера базы данных Azure для MySQL с помощью портала Azure)
- [Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md) (Создание базы данных Azure для сервера MySQL с помощью Azure CLI)

## <a name="install-go-and-mysql-connector"></a>Установка Go и соединителя MySQL
Установка [Go](https://golang.org/doc/install) и hello [go-sql драйвер для MySQL](https://github.com/go-sql-driver/mysql#installation) на компьютере. В зависимости от используемой платформы выполните действия hello.

### <a name="windows"></a>Windows
1. [Загрузить](https://golang.org/dl/) и установить Go для Microsoft Windows, в соответствии с toohello [инструкции по установке](https://golang.org/doc/install).
2. Откройте командную строку hello из меню "Пуск" hello.
3. Создайте папку для проекта, например `mkdir  %USERPROFILE%\go\src\mysqlgo`.
4. Измените каталог в папке проекта hello, такие как `cd %USERPROFILE%\go\src\mysqlgo`.
5. Задайте переменную среды hello для каталога GOPATH toopoint toohello исходного кода. `set GOPATH=%USERPROFILE%\go`.
6. Установка hello [go-sql драйвер для mysql](https://github.com/go-sql-driver/mysql#installation) , выполнив hello `go get github.com/go-sql-driver/mysql` команды.

   Таким образом установка Go, а затем выполните следующие команды в командную строку hello:
   ```cmd
   mkdir  %USERPROFILE%\go\src\mysqlgo
   cd %USERPROFILE%\go\src\mysqlgo
   set GOPATH=%USERPROFILE%\go
   go get github.com/go-sql-driver/mysql
   ```

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
1. Запустите консоль Bash hello. 
2. Установите Go, выполнив команду `sudo apt-get install golang-go`.
3. Создайте папку для проекта в корневом каталоге, например `mkdir -p ~/go/src/mysqlgo/`.
4. Изменить каталог, в папку hello, такие как `cd ~/go/src/mysqlgo/`.
5. Набор hello GOPATH среды переменной toopoint tooa допустимым исходным каталогом, таким как к текущей домашней папки перейдите в каталог. В оболочке bash hello, запустите `export GOPATH=~/go` tooadd hello мере directory hello GOPATH для текущего сеанса оболочки hello.
6. Установка hello [go-sql драйвер для mysql](https://github.com/go-sql-driver/mysql#installation) , выполнив hello `go get github.com/go-sql-driver/mysql` команды.

   Выполните следующие команды Bash:
   ```bash
   sudo apt-get install golang-go
   mkdir -p ~/go/src/mysqlgo/
   cd ~/go/src/mysqlgo/
   export GOPATH=~/go/
   go get github.com/go-sql-driver/mysql
   ```

### <a name="apple-macos"></a>Apple macOS
1. Загрузите и установите перейдите в соответствии с toohello [инструкции по установке](https://golang.org/doc/install) сопоставления вашей платформы. 
2. Запустите консоль Bash hello. 
3. Создайте папку для проекта в корневом каталоге, например `mkdir -p ~/go/src/mysqlgo/`.
4. Изменить каталог, в папку hello, такие как `cd ~/go/src/mysqlgo/`.
5. Набор hello GOPATH среды переменной toopoint tooa допустимым исходным каталогом, таким как к текущей домашней папки перейдите в каталог. В оболочке bash hello, запустите `export GOPATH=~/go` tooadd hello мере directory hello GOPATH для текущего сеанса оболочки hello.
6. Установка hello [go-sql драйвер для mysql](https://github.com/go-sql-driver/mysql#installation) , выполнив hello `go get github.com/go-sql-driver/mysql` команды.

   Установите Go, а затем выполните следующие команды Bash:
   ```bash
   mkdir -p ~/go/src/mysqlgo/
   cd ~/go/src/mysqlgo/
   export GOPATH=~/go/
   go get github.com/go-sql-driver/mysql
   ```

## <a name="get-connection-information"></a>Получение сведений о подключении
Получите toohello tooconnect базы данных Azure для hello подключения сведения, необходимые для MySQL. Необходимо hello server полное имя и учетные данные входа.

1. Войдите в toohello [портал Azure](https://portal.azure.com/).
2. Hello левого меню на портале Azure, щелкните **все ресурсы** и выполните поиск сервера hello, можно creased, такие как **myserver4demo**.
3. Щелкните имя сервера hello **myserver4demo**.
4. Выберите hello server **свойства** страницы. Запишите hello **имя сервера** и **имя входа администратора сервера**.
 ![Имя входа для администратора сервера в базе данных Azure для MySQL](./media/connect-go/1_server-properties-name-login.png)
5. Если вы забыли учетные данные входа сервера, перейдите toohello **Обзор** страница hello tooview: имя пользователя администратора сервера и, при необходимости переустановить пароль hello.
   

## <a name="build-and-run-go-code"></a>Сборка и выполнение кода Go 
1. toowrite Golang кода можно использовать простой текстовый редактор, например «Блокнот» в Microsoft Windows [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) или [Nano](https://www.nano-editor.org/) в Ubuntu или TextEdit в macOS. Если вы предпочитаете использовать полнофункциональную интерактивную среду разработки (IDE), попробуйте [Gogland](https://www.jetbrains.com/go/) от JetBrains, [Visual Studio Code](https://code.visualstudio.com/) от Майкрософт или [Atom](https://atom.io/).
2. Вставьте hello Go кода из разделов hello ниже в текстовые файлы и сохраните в папке проекта с расширением файла \*.go, такие как Windows-путь `%USERPROFILE%\go\src\mysqlgo\createtable.go` или путь Linux `~/go/src/mysqlgo/createtable.go`.
3. Найдите hello `HOST`, `DATABASE`, `USER`, и `PASSWORD` константы в коде hello и замена значений пример hello собственными значениями. 
4. Запустите командную строку hello или bash оболочки. Перейдите в папку проекта. В Windows это будет команда `cd %USERPROFILE%\go\src\mysqlgo\`, а в Linux — `cd ~/go/src/mysqlgo/`.  Некоторые редакторы IDE hello упомянутые обеспечивают возможности отладки и выполнения без использования команд оболочки.
5. Выполните код hello, введя команду hello `go run createtable.go` toocompile hello приложение и запустите его. 
6. Кроме того, код toobuild hello в приложении машинного кода, `go build createtable.go`, запустите `createtable.exe` toorun приложения hello.

## <a name="connect-create-table-and-insert-data"></a>Подключение, создание таблицы и вставка данных
Используйте следующие hello кода tooconnect toohello сервера, создайте таблицу и загружать данные при помощи hello **вставить** инструкции SQL. 

Код Hello импортирует три пакета: hello [пакета sql](https://golang.org/pkg/database/sql/), hello [драйвера перейдите sql для mysql](https://github.com/go-sql-driver/mysql#installation) как драйвер toocommunicate с hello базы данных Azure для MySQL и hello [fmt пакета](https://golang.org/pkg/fmt/)для печати ввода и вывода в командной строке hello.

Hello код вызывает метод [sql. Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure базы данных MySQL и для проверки подключения hello, с помощью метода [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping). Объект [дескриптор базы данных](https://golang.org/pkg/database/sql/#DB) для всех компонентов, удерживая hello пула соединений для сервера базы данных hello. hello вызовы кода Hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) метода несколько раз toorun несколько команд DDL. Привет код также использует hello [Prepare()](http://go-database-sql.org/prepared.html) и Exec() toorun подготовленных инструкций с различными параметрами tooinsert трех строк. Если произошла ошибка и панику tooexit каждый раз, метод пользовательских checkError() — используется toocheck.

Замените hello `host`, `database`, `user`, и `password` константы собственными значениями. 

```Go
package main

import (
    "database/sql"
    "fmt"

    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "myserver4demo.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@myserver4demo"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase.")

    // Drop previous table of same name if one exists.
    _, err = db.Exec("DROP TABLE IF EXISTS inventory;")
    checkError(err)
    fmt.Println("Finished dropping table (if existed).")

    // Create table.
    _, err = db.Exec("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);")
    checkError(err)
    fmt.Println("Finished creating table.")

    // Insert some data into table.
    sqlStatement, err := db.Prepare("INSERT INTO inventory (name, quantity) VALUES (?, ?);")
    res, err := sqlStatement.Exec("banana", 150)
    checkError(err)
    rowCount, err := res.RowsAffected()
    fmt.Printf("Inserted %d row(s) of data.\n", rowCount)

    res, err = sqlStatement.Exec("orange", 154)
    checkError(err)
    rowCount, err = res.RowsAffected()
    fmt.Printf("Inserted %d row(s) of data.\n", rowCount)

    res, err = sqlStatement.Exec("apple", 100)
    checkError(err)
    rowCount, err = res.RowsAffected()
    fmt.Printf("Inserted %d row(s) of data.\n", rowCount)
    fmt.Println("Done.")
}

```

## <a name="read-data"></a>Считывание данных
Используйте следующие hello кода tooconnect и чтения данных с помощью hello **ВЫБЕРИТЕ** инструкции SQL. 

Код Hello импортирует три пакета: hello [пакета sql](https://golang.org/pkg/database/sql/), hello [драйвера перейдите sql для mysql](https://github.com/go-sql-driver/mysql#installation) как драйвер toocommunicate с hello базы данных Azure для MySQL и hello [fmt пакета](https://golang.org/pkg/fmt/)для печати ввода и вывода в командной строке hello.

Hello код вызывает метод [sql. Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure базы данных MySQL и для проверки подключения hello, с помощью метода [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping). Объект [дескриптор базы данных](https://golang.org/pkg/database/sql/#DB) для всех компонентов, удерживая hello пула соединений для сервера базы данных hello. hello вызовы кода Hello [Query()](https://golang.org/pkg/database/sql/#DB.Query) команды select hello toorun метод. Затем он выполняет [Next()](https://golang.org/pkg/database/sql/#Rows.Next) tooiterate hello результирующего набора и [Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) значений столбцов tooparse hello, сохранение значение hello в переменные. Если произошла ошибка и панику tooexit каждый раз, метод пользовательских checkError() — используется toocheck.

Замените hello `host`, `database`, `user`, и `password` константы собственными значениями. 

```Go
package main

import (
    "database/sql"
    "fmt"

    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "myserver4demo.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@myserver4demo"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase.")

    // Variables for printing column data when scanned.
    var (
        id       int
        name     string
        quantity int
    )

    // Read some data from hello table.
    rows, err := db.Query("SELECT id, name, quantity from inventory;")
    checkError(err)
    defer rows.Close()
    fmt.Println("Reading data:")
    for rows.Next() {
        err := rows.Scan(&id, &name, &quantity)
        checkError(err)
        fmt.Printf("Data row = (%d, %s, %d)\n", id, name, quantity)
    }
    err = rows.Err()
    checkError(err)
    fmt.Println("Done.")
}
```

## <a name="update-data"></a>Обновление данных
Используйте следующие hello кода tooconnect и обновления данных с помощью hello **обновление** инструкции SQL. 

Код Hello импортирует три пакета: hello [пакета sql](https://golang.org/pkg/database/sql/), hello [драйвера перейдите sql для mysql](https://github.com/go-sql-driver/mysql#installation) как драйвер toocommunicate с hello базы данных Azure для MySQL и hello [fmt пакета](https://golang.org/pkg/fmt/)для печати ввода и вывода в командной строке hello.

Hello код вызывает метод [sql. Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure базы данных MySQL и для проверки подключения hello, с помощью метода [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping). Объект [дескриптор базы данных](https://golang.org/pkg/database/sql/#DB) для всех компонентов, удерживая hello пула соединений для сервера базы данных hello. hello вызовы кода Hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) команды update метод toorun hello. Если произошла ошибка и панику tooexit каждый раз, метод пользовательских checkError() — используется toocheck.

Замените hello `host`, `database`, `user`, и `password` константы собственными значениями. 

```Go
package main

import (
    "database/sql"
    "fmt"

    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "myserver4demo.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@myserver4demo"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase.")

    // Modify some data in table.
    rows, err := db.Exec("UPDATE inventory SET quantity = ? WHERE name = ?", 200, "banana")
    checkError(err)
    rowCount, err := rows.RowsAffected()
    fmt.Printf("Deleted %d row(s) of data.\n", rowCount)
    fmt.Println("Done.")
}
```

## <a name="delete-data"></a>Удаление данных
Используйте следующие hello кода tooconnect и удаление данных с помощью **удалить** инструкции SQL. 

Код Hello импортирует три пакета: hello [пакета sql](https://golang.org/pkg/database/sql/), hello [драйвера перейдите sql для mysql](https://github.com/go-sql-driver/mysql#installation) как драйвер toocommunicate с hello базы данных Azure для MySQL и hello [fmt пакета](https://golang.org/pkg/fmt/)для печати ввода и вывода в командной строке hello.

Hello код вызывает метод [sql. Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure базы данных MySQL и для проверки подключения hello, с помощью метода [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping). Объект [дескриптор базы данных](https://golang.org/pkg/database/sql/#DB) для всех компонентов, удерживая hello пула соединений для сервера базы данных hello. hello вызовы кода Hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) метод toorun hello удалить команду. Если произошла ошибка и панику tooexit каждый раз, метод пользовательских checkError() — используется toocheck.

Замените hello `host`, `database`, `user`, и `password` константы собственными значениями. 

```Go
package main

import (
    "database/sql"
    "fmt"
    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "myserver4demo.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@myserver4demo"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase.")

    // Modify some data in table.
    rows, err := db.Exec("DELETE FROM inventory WHERE name = ?", "orange")
    checkError(err)
    rowCount, err := rows.RowsAffected()
    fmt.Printf("Deleted %d row(s) of data.\n", rowCount)
    fmt.Println("Done.")
}
```

## <a name="next-steps"></a>Дальнейшие действия
> [!div class="nextstepaction"]
> [Перенос базы данных с помощью экспорта и импорта](./concepts-migrate-import-export.md)
