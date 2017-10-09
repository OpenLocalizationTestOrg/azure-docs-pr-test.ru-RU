---
title: "aaaConnect tooAzure базы данных PostgreSQL языке Go | Документы Microsoft"
description: "Это краткое руководство предоставляет Go программирования языка пример можно использовать tooconnect и запроса данных из базы данных Azure для PostgreSQL."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: go
ms.topic: quickstart
ms.date: 06/29/2017
ms.openlocfilehash: aa3c93da03116b8fcb54557494dccfad558e5f1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-go-language-tooconnect-and-query-data"></a>База данных Azure для PostgreSQL: используют команду Go языка tooconnect и запроса данных
Краткого руководства показано, как tooan tooconnect базы данных Azure для использования PostgreSQL кода hello написаны в [Go](https://golang.org/) языка (golang). Показано, как tooquery инструкций SQL toouse, вставка, обновление и удаление данных в базе данных hello. В этой статье предполагается, что вы знакомы с разработкой, с помощью команды Go, но, чтобы новый tooworking с базой данных Azure для PostgreSQL.

## <a name="prerequisites"></a>Предварительные требования
Это краткое руководство использует ресурсы hello, созданные в любой из этих руководствах по в качестве отправной точки.
- [Создание базы данных с помощью портала](quickstart-create-server-database-portal.md)
- [Создание базы данных с помощью Azure CLI](quickstart-create-server-database-azure-cli.md)

## <a name="install-go-and-pq-connector"></a>Установка Go и соединителя pq
Установка [Go](https://golang.org/doc/install) и hello [драйвер чисто Postgres Go (pq)](https://github.com/lib/pq) на компьютере. В зависимости от используемой платформы выполните действия hello.

### <a name="windows"></a>Windows
1. [Загрузить](https://golang.org/dl/) и установить Go для Microsoft Windows, в соответствии с toohello [инструкции по установке](https://golang.org/doc/install).
2. Откройте командную строку hello из меню "Пуск" hello.
3. Создайте папку для проекта, например `mkdir  %USERPROFILE%\go\src\postgresqlgo`.
4. Измените каталог в папке проекта hello, такие как `cd %USERPROFILE%\go\src\postgresqlgo`.
5. Задайте переменную среды hello для каталога GOPATH toopoint toohello исходного кода. `set GOPATH=%USERPROFILE%\go`.
6. Установка hello [драйвер чисто Postgres Go (pq)](https://github.com/lib/pq) , выполнив hello `go get github.com/lib/pq` команды.

   Таким образом установка Go, а затем выполните следующие команды в командную строку hello:
   ```cmd
   mkdir  %USERPROFILE%\go\src\postgresqlgo
   cd %USERPROFILE%\go\src\postgresqlgo
   set GOPATH=%USERPROFILE%\go
   go get github.com/lib/pq
   ```

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
1. Запустите консоль Bash hello. 
2. Установите Go, выполнив команду `sudo apt-get install golang-go`.
3. Создайте папку для проекта в корневом каталоге, например `mkdir -p ~/go/src/postgresqlgo/`.
4. Изменить каталог, в папку hello, такие как `cd ~/go/src/postgresqlgo/`.
5. Набор hello GOPATH среды переменной toopoint tooa допустимым исходным каталогом, таким как к текущей домашней папки перейдите в каталог. В оболочке bash hello, запустите `export GOPATH=~/go` tooadd hello мере directory hello GOPATH для текущего сеанса оболочки hello.
6. Установка hello [драйвер чисто Postgres Go (pq)](https://github.com/lib/pq) , выполнив hello `go get github.com/lib/pq` команды.

   Выполните следующие команды Bash:
   ```bash
   sudo apt-get install golang-go
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

### <a name="apple-macos"></a>Apple macOS
1. Загрузите и установите перейдите в соответствии с toohello [инструкции по установке](https://golang.org/doc/install) сопоставления вашей платформы. 
2. Запустите консоль Bash hello. 
3. Создайте папку для проекта в корневом каталоге, например `mkdir -p ~/go/src/postgresqlgo/`.
4. Изменить каталог, в папку hello, такие как `cd ~/go/src/postgresqlgo/`.
5. Набор hello GOPATH среды переменной toopoint tooa допустимым исходным каталогом, таким как к текущей домашней папки перейдите в каталог. В оболочке bash hello, запустите `export GOPATH=~/go` tooadd hello мере directory hello GOPATH для текущего сеанса оболочки hello.
6. Установка hello [драйвер чисто Postgres Go (pq)](https://github.com/lib/pq) , выполнив hello `go get github.com/lib/pq` команды.

   Установите Go, а затем выполните следующие команды Bash:
   ```bash
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

## <a name="get-connection-information"></a>Получение сведений о подключении
Получите toohello tooconnect базы данных Azure для hello подключения сведения, необходимые для PostgreSQL. Необходимо hello server полное имя и учетные данные входа.

1. Войдите в toohello [портал Azure](https://portal.azure.com/).
2. Hello левого меню на портале Azure, щелкните **все ресурсы** и выполните поиск сервера hello, вы создали, таких как **mypgserver 20170401**.
3. Щелкните имя сервера hello **mypgserver 20170401**.
4. Выберите hello server **Обзор** страницы. Запишите hello **имя сервера** и **имя входа администратора сервера**.
 ![База данных Azure для PostgreSQL. Учетные данные администратора сервера для входа](./media/connect-go/1-connection-string.png)
5. Если вы забыли учетные данные входа сервера, перейдите toohello **Обзор** страницы и имя входа администратора сервера hello представления. При необходимости hello сброс пароля.

## <a name="build-and-run-go-code"></a>Сборка и выполнение кода Go 
1. toowrite Golang кода можно использовать простой текстовый редактор, например «Блокнот» в Microsoft Windows [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) или [Nano](https://www.nano-editor.org/) в Ubuntu или TextEdit в macOS. Если вы предпочитаете использовать полнофункциональную интерактивную среду разработки (IDE), попробуйте [Gogland](https://www.jetbrains.com/go/) от JetBrains, [Visual Studio Code](https://code.visualstudio.com/) от Майкрософт или [Atom](https://atom.io/).
2. Вставьте код Golang hello с hello разделов ниже текстовые файлы и сохранить в папке проекта с расширением файла \*.go, такие как Windows-путь `%USERPROFILE%\go\src\postgresqlgo\createtable.go` или путь Linux `~/go/src/postgresqlgo/createtable.go`.
3. Найдите hello `HOST`, `DATABASE`, `USER`, и `PASSWORD` константы в коде hello и замена значений пример hello собственными значениями.  
4. Запустите командную строку hello или bash оболочки. Перейдите в папку проекта. В Windows это будет команда `cd %USERPROFILE%\go\src\postgresqlgo\`, а в Linux — `cd ~/go/src/postgresqlgo/`. Некоторые из упомянутых сред IDE hello обеспечивают возможности отладки и выполнения без использования команд оболочки.
5. Выполните код hello, введя команду hello `go run createtable.go` toocompile hello приложение и запустите его. 
6. Кроме того, код toobuild hello в приложении машинного кода, `go build createtable.go`, запустите `createtable.exe` toorun приложения hello.

## <a name="connect-and-create-a-table"></a>Подключение и создание таблицы
Используйте следующие hello кода tooconnect и создание таблицы с помощью **CREATE TABLE** инструкции SQL, за которым следует **INSERT INTO** строк tooadd инструкций SQL в таблицу hello.

Код Hello импортирует три пакета: hello [пакета sql](https://golang.org/pkg/database/sql/), hello [pq пакета](http://godoc.org/github.com/lib/pq) как драйвер toocommunicate с сервером Postgres hello и hello [fmt пакета](https://golang.org/pkg/fmt/) для печати Ввод и вывод в командной строке hello.

Hello код вызывает метод [sql. Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure базы данных PostgreSQL и для проверки подключения hello, с помощью метода [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping). Объект [дескриптор базы данных](https://golang.org/pkg/database/sql/#DB) для всех компонентов, удерживая hello пула соединений для сервера базы данных hello. hello вызовы кода Hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) метода несколько раз toorun несколько команд SQL. Каждый раз toocheck checkError() пользовательский метод, если произошла ошибка и панику tooexit при возникновении ошибки.

Замените hello `HOST`, `DATABASE`, `USER`, и `PASSWORD` параметры собственными значениями. 

```go
package main

import (
    "database/sql"
    "fmt"
    _ "github.com/lib/pq"
)

const (
    // Initialize connection constants.
    HOST     = "mypgserver-20170401.postgres.database.azure.com"
    DATABASE = "mypgsqldb"
    USER     = "mylogin@mypgserver-20170401"
    PASSWORD = "<server_admin_password>"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {
    // Initialize connection string.
    var connectionString string = fmt.Sprintf("host=%s user=%s password=%s dbname=%s sslmode=require", HOST, USER, PASSWORD, DATABASE)

    // Initialize connection object.
    db, err := sql.Open("postgres", connectionString)
    checkError(err)

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase")

    // Drop previous table of same name if one exists.
    _, err = db.Exec("DROP TABLE IF EXISTS inventory;")
    checkError(err)
    fmt.Println("Finished dropping table (if existed)")

    // Create table.
    _, err = db.Exec("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);")
    checkError(err)
    fmt.Println("Finished creating table")

    // Insert some data into table.
    sql_statement := "INSERT INTO inventory (name, quantity) VALUES ($1, $2);"
    _, err = db.Exec(sql_statement, "banana", 150)
    checkError(err)
    _, err = db.Exec(sql_statement, "orange", 154)
    checkError(err)
    _, err = db.Exec(sql_statement, "apple", 100)
    checkError(err)
    fmt.Println("Inserted 3 rows of data")
}
```

## <a name="read-data"></a>Считывание данных
Используйте следующие hello кода tooconnect и чтения данных с помощью hello **ВЫБЕРИТЕ** инструкции SQL. 

Код Hello импортирует три пакета: hello [пакета sql](https://golang.org/pkg/database/sql/), hello [pq пакета](http://godoc.org/github.com/lib/pq) как драйвер toocommunicate с сервером Postgres hello и hello [fmt пакета](https://golang.org/pkg/fmt/) для печати Ввод и вывод в командной строке hello.

Hello код вызывает метод [sql. Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure базы данных PostgreSQL и для проверки подключения hello, с помощью метода [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping). Объект [дескриптор базы данных](https://golang.org/pkg/database/sql/#DB) для всех компонентов, удерживая hello пула соединений для сервера базы данных hello. запрос select Hello выполняется путем вызова метода [db. Query()](https://golang.org/pkg/database/sql/#DB.Query), а hello результирующие строки хранятся в переменной типа [строк](https://golang.org/pkg/database/sql/#Rows). Код Hello считывает hello значения данных столбца в текущей строке hello, с помощью метода [строк. Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) и проходит по hello строк, с помощью итератора hello [строк. Next()](https://golang.org/pkg/database/sql/#Rows.Next) пока существует больше нет строк. Значения столбцов для каждой строки являются консоли печатной toohello out. Каждый раз toocheck checkError() пользовательский метод, если произошла ошибка и панику tooexit при возникновении ошибки.

Замените hello `HOST`, `DATABASE`, `USER`, и `PASSWORD` параметры собственными значениями. 

```go
package main

import (
    "database/sql"
    "fmt"
    _ "github.com/lib/pq"
)

const (
    // Initialize connection constants.
    HOST     = "mypgserver-20170401.postgres.database.azure.com"
    DATABASE = "mypgsqldb"
    USER     = "mylogin@mypgserver-20170401"
    PASSWORD = "<server_admin_password>"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString string = fmt.Sprintf("host=%s user=%s password=%s dbname=%s sslmode=require", HOST, USER, PASSWORD, DATABASE)

    // Initialize connection object.
    db, err := sql.Open("postgres", connectionString)
    checkError(err)

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase")

    // Read rows from table.
    var id int
    var name string
    var quantity int

    sql_statement := "SELECT * from inventory;"
    rows, err := db.Query(sql_statement)
    checkError(err)

    for rows.Next() {
        switch err := rows.Scan(&id, &name, &quantity); err {
        case sql.ErrNoRows:
            fmt.Println("No rows were returned")
        case nil:
            fmt.Printf("Data row = (%d, %s, %d)\n", id, name, quantity)
        default:
            checkError(err)
        }
    }
}
```

## <a name="update-data"></a>Обновление данных
Используйте следующие hello кода tooconnect и обновления данных с помощью hello **обновление** инструкции SQL.

Код Hello импортирует три пакета: hello [пакета sql](https://golang.org/pkg/database/sql/), hello [pq пакета](http://godoc.org/github.com/lib/pq) как драйвер toocommunicate с сервером Postgres hello и hello [fmt пакета](https://golang.org/pkg/fmt/) для печати Ввод и вывод в командной строке hello.

Hello код вызывает метод [sql. Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure базы данных PostgreSQL и для проверки подключения hello, с помощью метода [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping). Объект [дескриптор базы данных](https://golang.org/pkg/database/sql/#DB) для всех компонентов, удерживая hello пула соединений для сервера базы данных hello. hello вызовы кода Hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) метод toorun hello инструкции SQL, которая обновляет таблицу hello. Toocheck checkError() пользовательский метод, если произошла ошибка и панику tooexit, если ошибка возникает.

Замените hello `HOST`, `DATABASE`, `USER`, и `PASSWORD` параметры собственными значениями. 
```go
package main

import (
  "database/sql"
  _ "github.com/lib/pq"
  "fmt"
)

const (
    // Initialize connection constants.
    HOST     = "mypgserver-20170401.postgres.database.azure.com"
    DATABASE = "mypgsqldb"
    USER     = "mylogin@mypgserver-20170401"
    PASSWORD = "<server_admin_password>"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {
    
    // Initialize connection string.
    var connectionString string = 
        fmt.Sprintf("host=%s user=%s password=%s dbname=%s sslmode=require", HOST, USER, PASSWORD, DATABASE)

    // Initialize connection object.
    db, err := sql.Open("postgres", connectionString)
    checkError(err)

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase")

    // Modify some data in table.
    sql_statement := "UPDATE inventory SET quantity = $2 WHERE name = $1;"
    _, err = db.Exec(sql_statement, "banana", 200)
    checkError(err)
    fmt.Println("Updated 1 row of data")
}
```

## <a name="delete-data"></a>Удаление данных
Используйте следующие hello кода tooconnect и чтения данных с помощью hello **удалить** инструкции SQL. 

Код Hello импортирует три пакета: hello [пакета sql](https://golang.org/pkg/database/sql/), hello [pq пакета](http://godoc.org/github.com/lib/pq) как драйвер toocommunicate с сервером Postgres hello и hello [fmt пакета](https://golang.org/pkg/fmt/) для печати Ввод и вывод в командной строке hello.

Hello код вызывает метод [sql. Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure базы данных PostgreSQL и для проверки подключения hello, с помощью метода [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping). Объект [дескриптор базы данных](https://golang.org/pkg/database/sql/#DB) для всех компонентов, удерживая hello пула соединений для сервера базы данных hello. hello вызовы кода Hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) метод toorun hello инструкции SQL, которая обновляет таблицу hello. Toocheck checkError() пользовательский метод, если произошла ошибка и панику tooexit, если ошибка возникает.

Замените hello `HOST`, `DATABASE`, `USER`, и `PASSWORD` параметры собственными значениями. 
```go
package main

import (
  "database/sql"
  _ "github.com/lib/pq"
  "fmt"
)

const (
    // Initialize connection constants.
    HOST     = "mypgserver-20170401.postgres.database.azure.com"
    DATABASE = "mypgsqldb"
    USER     = "mylogin@mypgserver-20170401"
    PASSWORD = "<server_admin_password>"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {
    
    // Initialize connection string.
    var connectionString string = 
        fmt.Sprintf("host=%s user=%s password=%s dbname=%s sslmode=require", HOST, USER, PASSWORD, DATABASE)

    // Initialize connection object.
    db, err := sql.Open("postgres", connectionString)
    checkError(err)

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase")

    // Delete some data from table.
    sql_statement := "DELETE FROM inventory WHERE name = $1;"
    _, err = db.Exec(sql_statement, "orange")
    checkError(err)
    fmt.Println("Deleted 1 row of data")
}
```

## <a name="next-steps"></a>Дальнейшие действия
> [!div class="nextstepaction"]
> [Перенос базы данных с помощью экспорта и импорта](./howto-migrate-using-export-and-import.md)
