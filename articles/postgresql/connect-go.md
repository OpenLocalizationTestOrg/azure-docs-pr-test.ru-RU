---
title: "Подключение к базе данных Azure для PostgreSQL с помощью языка Go | Документация Майкрософт"
description: "В этом кратком руководстве представлен пример кода на языке программирования Go, который можно использовать для подключения к базе данных Azure для PostgreSQL и запроса данных из нее."
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
ms.openlocfilehash: a7555464879826c5e4f55929d23163b002664e81
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-postgresql-use-go-language-to-connect-and-query-data"></a><span data-ttu-id="74572-103">База данных Azure для PostgreSQL: подключение и запросы данных с помощью языка Go</span><span class="sxs-lookup"><span data-stu-id="74572-103">Azure Database for PostgreSQL: Use Go language to connect and query data</span></span>
<span data-ttu-id="74572-104">В этом кратком руководстве описывается, как подключиться к базе данных Azure для PostgreSQL с помощью кода на языке [Go](https://golang.org/) (golang).</span><span class="sxs-lookup"><span data-stu-id="74572-104">This quickstart demonstrates how to connect to an Azure Database for PostgreSQL using code written in the [Go](https://golang.org/) language (golang).</span></span> <span data-ttu-id="74572-105">Здесь также показано, как использовать инструкции SQL для запроса, вставки, обновления и удаления данных в базе данных.</span><span class="sxs-lookup"><span data-stu-id="74572-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="74572-106">В этой статье предполагается, что у вас уже есть опыт разработки на Go, и вы только начали работу с базой данных Azure для PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="74572-106">This article assumes you are familiar with development using Go, but that you are new to working with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="74572-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="74572-107">Prerequisites</span></span>
<span data-ttu-id="74572-108">В качестве отправной точки в этом кратком руководстве используются ресурсы, созданные в соответствии со следующими материалами:</span><span class="sxs-lookup"><span data-stu-id="74572-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="74572-109">Создание базы данных с помощью портала</span><span class="sxs-lookup"><span data-stu-id="74572-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="74572-110">Создание базы данных с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="74572-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

## <a name="install-go-and-pq-connector"></a><span data-ttu-id="74572-111">Установка Go и соединителя pq</span><span class="sxs-lookup"><span data-stu-id="74572-111">Install Go and pq connector</span></span>
<span data-ttu-id="74572-112">Установите язык [Go](https://golang.org/doc/install) и [драйвер Pure Go Postgres](https://github.com/lib/pq) на своем компьютере.</span><span class="sxs-lookup"><span data-stu-id="74572-112">Install [Go](https://golang.org/doc/install) and the [Pure Go Postgres driver (pq)](https://github.com/lib/pq) on your own machine.</span></span> <span data-ttu-id="74572-113">В зависимости от используемой платформы выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="74572-113">Depending on your platform, follow the steps:</span></span>

### <a name="windows"></a><span data-ttu-id="74572-114">Windows</span><span class="sxs-lookup"><span data-stu-id="74572-114">Windows</span></span>
1. <span data-ttu-id="74572-115">[Скачайте](https://golang.org/dl/) и установите Go для Microsoft Windows [согласно инструкциям по установке](https://golang.org/doc/install).</span><span class="sxs-lookup"><span data-stu-id="74572-115">[Download](https://golang.org/dl/) and install Go for Microsoft Windows according to the [installation instructions](https://golang.org/doc/install).</span></span>
2. <span data-ttu-id="74572-116">Запустите командную строку из меню "Пуск".</span><span class="sxs-lookup"><span data-stu-id="74572-116">Launch the command prompt from the start menu.</span></span>
3. <span data-ttu-id="74572-117">Создайте папку для проекта, например</span><span class="sxs-lookup"><span data-stu-id="74572-117">Make a folder for your project such.</span></span> <span data-ttu-id="74572-118">`mkdir  %USERPROFILE%\go\src\postgresqlgo`.</span><span class="sxs-lookup"><span data-stu-id="74572-118">`mkdir  %USERPROFILE%\go\src\postgresqlgo`.</span></span>
4. <span data-ttu-id="74572-119">Перейдите в папку проекта, например `cd %USERPROFILE%\go\src\postgresqlgo`.</span><span class="sxs-lookup"><span data-stu-id="74572-119">Change directory into the project folder, such as `cd %USERPROFILE%\go\src\postgresqlgo`.</span></span>
5. <span data-ttu-id="74572-120">В качестве значения для переменной среды GOPATH укажите путь к каталогу с исходным кодом.</span><span class="sxs-lookup"><span data-stu-id="74572-120">Set the environment variable for GOPATH to point to the source code directory.</span></span> <span data-ttu-id="74572-121">`set GOPATH=%USERPROFILE%\go`.</span><span class="sxs-lookup"><span data-stu-id="74572-121">`set GOPATH=%USERPROFILE%\go`.</span></span>
6. <span data-ttu-id="74572-122">Установите [драйвер Pure Go Postgres (pq)](https://github.com/lib/pq) с помощью команды `go get github.com/lib/pq`.</span><span class="sxs-lookup"><span data-stu-id="74572-122">Install the [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running the `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="74572-123">Установите Go, а затем выполните следующие команды в командной строке:</span><span class="sxs-lookup"><span data-stu-id="74572-123">In summary, install Go, then run these commands in the command prompt:</span></span>
   ```cmd
   mkdir  %USERPROFILE%\go\src\postgresqlgo
   cd %USERPROFILE%\go\src\postgresqlgo
   set GOPATH=%USERPROFILE%\go
   go get github.com/lib/pq
   ```

### <a name="linux-ubuntu"></a><span data-ttu-id="74572-124">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="74572-124">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="74572-125">Запустите оболочку Bash.</span><span class="sxs-lookup"><span data-stu-id="74572-125">Launch the Bash shell.</span></span> 
2. <span data-ttu-id="74572-126">Установите Go, выполнив команду `sudo apt-get install golang-go`.</span><span class="sxs-lookup"><span data-stu-id="74572-126">Install Go by running `sudo apt-get install golang-go`.</span></span>
3. <span data-ttu-id="74572-127">Создайте папку для проекта в корневом каталоге, например `mkdir -p ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="74572-127">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/postgresqlgo/`.</span></span>
4. <span data-ttu-id="74572-128">Перейдите в другую папку, например `cd ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="74572-128">Change directory into the folder, such as `cd ~/go/src/postgresqlgo/`.</span></span>
5. <span data-ttu-id="74572-129">В качестве значения для переменной среды GOPATH укажите путь к действительному исходному каталогу, например к текущей папке Go в корневом каталоге.</span><span class="sxs-lookup"><span data-stu-id="74572-129">Set the GOPATH environment variable to point to a valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="74572-130">В оболочке Bash выполните команду `export GOPATH=~/go`, чтобы добавить каталог Go в качестве значения переменной GOPATH для текущего сеанса оболочки.</span><span class="sxs-lookup"><span data-stu-id="74572-130">At the bash shell, run `export GOPATH=~/go` to add the go directory as the GOPATH for the current shell session.</span></span>
6. <span data-ttu-id="74572-131">Установите [драйвер Pure Go Postgres (pq)](https://github.com/lib/pq) с помощью команды `go get github.com/lib/pq`.</span><span class="sxs-lookup"><span data-stu-id="74572-131">Install the [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running the `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="74572-132">Выполните следующие команды Bash:</span><span class="sxs-lookup"><span data-stu-id="74572-132">In summary, run these bash commands:</span></span>
   ```bash
   sudo apt-get install golang-go
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

### <a name="apple-macos"></a><span data-ttu-id="74572-133">Apple macOS</span><span class="sxs-lookup"><span data-stu-id="74572-133">Apple macOS</span></span>
1. <span data-ttu-id="74572-134">Скачайте и установите Go согласно [инструкциям по установке](https://golang.org/doc/install) с учетом вашей платформы.</span><span class="sxs-lookup"><span data-stu-id="74572-134">Download and install Go according to the [installation instructions](https://golang.org/doc/install)  matching your platform.</span></span> 
2. <span data-ttu-id="74572-135">Запустите оболочку Bash.</span><span class="sxs-lookup"><span data-stu-id="74572-135">Launch the Bash shell.</span></span> 
3. <span data-ttu-id="74572-136">Создайте папку для проекта в корневом каталоге, например `mkdir -p ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="74572-136">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/postgresqlgo/`.</span></span>
4. <span data-ttu-id="74572-137">Перейдите в другую папку, например `cd ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="74572-137">Change directory into the folder, such as `cd ~/go/src/postgresqlgo/`.</span></span>
5. <span data-ttu-id="74572-138">В качестве значения для переменной среды GOPATH укажите путь к действительному исходному каталогу, например к текущей папке Go в корневом каталоге.</span><span class="sxs-lookup"><span data-stu-id="74572-138">Set the GOPATH environment variable to point to a valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="74572-139">В оболочке Bash выполните команду `export GOPATH=~/go`, чтобы добавить каталог Go в качестве значения переменной GOPATH для текущего сеанса оболочки.</span><span class="sxs-lookup"><span data-stu-id="74572-139">At the bash shell, run `export GOPATH=~/go` to add the go directory as the GOPATH for the current shell session.</span></span>
6. <span data-ttu-id="74572-140">Установите [драйвер Pure Go Postgres (pq)](https://github.com/lib/pq) с помощью команды `go get github.com/lib/pq`.</span><span class="sxs-lookup"><span data-stu-id="74572-140">Install the [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running the `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="74572-141">Установите Go, а затем выполните следующие команды Bash:</span><span class="sxs-lookup"><span data-stu-id="74572-141">In summary, install Go, then run these bash commands:</span></span>
   ```bash
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

## <a name="get-connection-information"></a><span data-ttu-id="74572-142">Получение сведений о подключении</span><span class="sxs-lookup"><span data-stu-id="74572-142">Get connection information</span></span>
<span data-ttu-id="74572-143">Получите сведения, необходимые для подключения к базе данных Azure.для PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="74572-143">Get the connection information needed to connect to the Azure Database for PostgreSQL.</span></span> <span data-ttu-id="74572-144">Вам потребуется полное имя сервера и учетные данные для входа.</span><span class="sxs-lookup"><span data-stu-id="74572-144">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="74572-145">Войдите на [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="74572-145">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="74572-146">В меню слева на портале Azure щелкните **Все ресурсы** и выполните поиск по имени созданного сервера, например **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="74572-146">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="74572-147">Щелкните имя сервера **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="74572-147">Click the server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="74572-148">Выберите страницу **обзора** сервера.</span><span class="sxs-lookup"><span data-stu-id="74572-148">Select the server's **Overview** page.</span></span> <span data-ttu-id="74572-149">Запишите значения **имени сервера** и **имени для входа администратора сервера**.</span><span class="sxs-lookup"><span data-stu-id="74572-149">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="74572-150">![База данных Azure для PostgreSQL. Учетные данные администратора сервера для входа](./media/connect-go/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="74572-150">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-go/1-connection-string.png)</span></span>
5. <span data-ttu-id="74572-151">Если вы забыли данные для входа на сервер, перейдите на страницу **Обзор**, где указано имя администратора сервера.</span><span class="sxs-lookup"><span data-stu-id="74572-151">If you forget your server login information, navigate to the **Overview** page, and view the Server admin login name.</span></span> <span data-ttu-id="74572-152">При необходимости сбросьте пароль.</span><span class="sxs-lookup"><span data-stu-id="74572-152">If necessary, reset the password.</span></span>

## <a name="build-and-run-go-code"></a><span data-ttu-id="74572-153">Сборка и выполнение кода Go</span><span class="sxs-lookup"><span data-stu-id="74572-153">Build and run Go code</span></span> 
1. <span data-ttu-id="74572-154">Для написания кода на Golang можно использовать простой текстовый редактор, например Блокнот в Microsoft Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) или [Nano](https://www.nano-editor.org/) в Ubuntu, а также TextEdit в macOS.</span><span class="sxs-lookup"><span data-stu-id="74572-154">To write Golang code, you can use a simple text editor, such as Notepad in Microsoft Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) or [Nano](https://www.nano-editor.org/) in Ubuntu, or TextEdit in macOS.</span></span> <span data-ttu-id="74572-155">Если вы предпочитаете использовать полнофункциональную интерактивную среду разработки (IDE), попробуйте [Gogland](https://www.jetbrains.com/go/) от JetBrains, [Visual Studio Code](https://code.visualstudio.com/) от Майкрософт или [Atom](https://atom.io/).</span><span class="sxs-lookup"><span data-stu-id="74572-155">If you prefer a richer Interactive Development Environment (IDE) try [Gogland](https://www.jetbrains.com/go/) by Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) by Microsoft, or [Atom](https://atom.io/).</span></span>
2. <span data-ttu-id="74572-156">Вставьте код Golang из приведенных ниже разделов в текстовые файлы и сохраните их с расширением \*.go в папке проекта, например `%USERPROFILE%\go\src\postgresqlgo\createtable.go` в Windows или `~/go/src/postgresqlgo/createtable.go` в Linux.</span><span class="sxs-lookup"><span data-stu-id="74572-156">Paste the Golang code from the sections below into text files, and save into your project folder with file extension \*.go, such as Windows path `%USERPROFILE%\go\src\postgresqlgo\createtable.go` or Linux path `~/go/src/postgresqlgo/createtable.go`.</span></span>
3. <span data-ttu-id="74572-157">Найдите константы `HOST`, `DATABASE`, `USER` и `PASSWORD` в коде и замените приведенные для примера значения своими собственными.</span><span class="sxs-lookup"><span data-stu-id="74572-157">Locate the `HOST`, `DATABASE`, `USER`, and `PASSWORD` constants in the code, and replace the example values with your own values.</span></span>  
4. <span data-ttu-id="74572-158">Запустите командную строку или оболочку Bash.</span><span class="sxs-lookup"><span data-stu-id="74572-158">Launch the command prompt or bash shell.</span></span> <span data-ttu-id="74572-159">Перейдите в папку проекта.</span><span class="sxs-lookup"><span data-stu-id="74572-159">Change directory into your project folder.</span></span> <span data-ttu-id="74572-160">В Windows это будет команда `cd %USERPROFILE%\go\src\postgresqlgo\`,</span><span class="sxs-lookup"><span data-stu-id="74572-160">For example, on Windows `cd %USERPROFILE%\go\src\postgresqlgo\`.</span></span> <span data-ttu-id="74572-161">а в Linux — `cd ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="74572-161">On Linux `cd ~/go/src/postgresqlgo/`.</span></span> <span data-ttu-id="74572-162">Некоторые из упомянутых сред IDE позволяют выполнять отладку и использовать среду выполнения без применения команд оболочки.</span><span class="sxs-lookup"><span data-stu-id="74572-162">Some of the IDE environments mentioned offer debug and runtime capabilities without requiring shell commands.</span></span>
5. <span data-ttu-id="74572-163">Выполните код с помощью команды `go run createtable.go`, чтобы скомпилировать и запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="74572-163">Run the code by typing the command `go run createtable.go` to compile the application and run it.</span></span> 
6. <span data-ttu-id="74572-164">Вы также можете создать код в собственном приложении. Для этого введите `go build createtable.go`, а затем выполните `createtable.exe`, чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="74572-164">Alternatively, to build the code into a native application, `go build createtable.go`, then launch `createtable.exe` to run the application.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="74572-165">Подключение и создание таблицы</span><span class="sxs-lookup"><span data-stu-id="74572-165">Connect and create a table</span></span>
<span data-ttu-id="74572-166">Используйте приведенный ниже код для подключения и создайте таблицу с помощью инструкции SQL **CREATE TABLE**. Добавьте строки в таблицу, применив инструкцию SQL **INSERT INTO**.</span><span class="sxs-lookup"><span data-stu-id="74572-166">Use the following code to connect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements to add rows into the table.</span></span>

<span data-ttu-id="74572-167">Код импортирует три пакета: [пакет sql](https://golang.org/pkg/database/sql/), [пакет pq](http://godoc.org/github.com/lib/pq) как драйвер для обмена данными с сервером Postgres и [пакет fmt](https://golang.org/pkg/fmt/) для вывода входных и выходных данных в командной строке.</span><span class="sxs-lookup"><span data-stu-id="74572-167">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [pq package](http://godoc.org/github.com/lib/pq) as a driver to communicate with the Postgres server, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="74572-168">Код вызывает метод [sql.Open()](http://godoc.org/github.com/lib/pq#Open) для подключения к базе данных Azure для PostgreSQL, а затем проверяет подключение с помощью метода [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="74572-168">The code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) to connect to Azure Database for PostgreSQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="74572-169">[Дескриптор базы данных](https://golang.org/pkg/database/sql/#DB) используется для всех компонентов. Он содержит пул подключений к серверу базы данных.</span><span class="sxs-lookup"><span data-stu-id="74572-169">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="74572-170">Этот код несколько раз вызывает метод [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) для выполнения нескольких команд SQL.</span><span class="sxs-lookup"><span data-stu-id="74572-170">The code calls the [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method several times to run several SQL commands.</span></span> <span data-ttu-id="74572-171">При каждом запуске пользовательский метод checkError() проверяет наличие ошибок и инициирует аварийный выход в случае их обнаружения.</span><span class="sxs-lookup"><span data-stu-id="74572-171">Each time a custom checkError() method to check if an error occurred and panic to exit if an error occurs.</span></span>

<span data-ttu-id="74572-172">Замените значения параметров `HOST`, `DATABASE`, `USER` и `PASSWORD` своими значениями.</span><span class="sxs-lookup"><span data-stu-id="74572-172">Replace the `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 

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
    fmt.Println("Successfully created connection to database")

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

## <a name="read-data"></a><span data-ttu-id="74572-173">Считывание данных</span><span class="sxs-lookup"><span data-stu-id="74572-173">Read data</span></span>
<span data-ttu-id="74572-174">Используйте указанный ниже код с инструкцией SQL **SELECT** для подключения и чтения данных.</span><span class="sxs-lookup"><span data-stu-id="74572-174">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="74572-175">Код импортирует три пакета: [пакет sql](https://golang.org/pkg/database/sql/), [пакет pq](http://godoc.org/github.com/lib/pq) как драйвер для обмена данными с сервером Postgres и [пакет fmt](https://golang.org/pkg/fmt/) для вывода входных и выходных данных в командной строке.</span><span class="sxs-lookup"><span data-stu-id="74572-175">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [pq package](http://godoc.org/github.com/lib/pq) as a driver to communicate with the Postgres server, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="74572-176">Код вызывает метод [sql.Open()](http://godoc.org/github.com/lib/pq#Open) для подключения к базе данных Azure для PostgreSQL, а затем проверяет подключение с помощью метода [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="74572-176">The code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) to connect to Azure Database for PostgreSQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="74572-177">[Дескриптор базы данных](https://golang.org/pkg/database/sql/#DB) используется для всех компонентов. Он содержит пул подключений к серверу базы данных.</span><span class="sxs-lookup"><span data-stu-id="74572-177">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="74572-178">Запрос выбора выполняется с помощью метода [db.Query()](https://golang.org/pkg/database/sql/#DB.Query), а итоговые строки сохраняются в переменной типа [rows](https://golang.org/pkg/database/sql/#Rows).</span><span class="sxs-lookup"><span data-stu-id="74572-178">The select query is run by calling method [db.Query()](https://golang.org/pkg/database/sql/#DB.Query), and the resulting rows is kept in a variable of type [rows](https://golang.org/pkg/database/sql/#Rows).</span></span> <span data-ttu-id="74572-179">Код считывает из столбцов значения данных в текущей строке с помощью метода [rows.Scan()](https://golang.org/pkg/database/sql/#Rows.Scan), а затем запускает цикл по строкам, используя итератор [сrows.Next()](https://golang.org/pkg/database/sql/#Rows.Next), пока строк больше не останется.</span><span class="sxs-lookup"><span data-stu-id="74572-179">The code reads the column data values in the current row using method [rows.Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) and loops over the rows using the iterator [rows.Next()](https://golang.org/pkg/database/sql/#Rows.Next) until no more rows exist.</span></span> <span data-ttu-id="74572-180">Значения столбцов для каждой строки выводятся на консоль. При каждом запуске пользовательский метод checkError() проверяет наличие ошибок и инициирует аварийный выход в случае их обнаружения.</span><span class="sxs-lookup"><span data-stu-id="74572-180">Each row's column values are printed to the console out. Each time a custom checkError() method to check if an error occurred and panic to exit if an error occurs.</span></span>

<span data-ttu-id="74572-181">Замените значения параметров `HOST`, `DATABASE`, `USER` и `PASSWORD` своими значениями.</span><span class="sxs-lookup"><span data-stu-id="74572-181">Replace the `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 

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
    fmt.Println("Successfully created connection to database")

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

## <a name="update-data"></a><span data-ttu-id="74572-182">Обновление данных</span><span class="sxs-lookup"><span data-stu-id="74572-182">Update data</span></span>
<span data-ttu-id="74572-183">Используйте указанный ниже код с инструкцией SQL **UPDATE** для подключения и обновления данных.</span><span class="sxs-lookup"><span data-stu-id="74572-183">Use the following code to connect and update the data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="74572-184">Код импортирует три пакета: [пакет sql](https://golang.org/pkg/database/sql/), [пакет pq](http://godoc.org/github.com/lib/pq) как драйвер для обмена данными с сервером Postgres и [пакет fmt](https://golang.org/pkg/fmt/) для вывода входных и выходных данных в командной строке.</span><span class="sxs-lookup"><span data-stu-id="74572-184">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [pq package](http://godoc.org/github.com/lib/pq) as a driver to communicate with the Postgres server, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="74572-185">Код вызывает метод [sql.Open()](http://godoc.org/github.com/lib/pq#Open) для подключения к базе данных Azure для PostgreSQL, а затем проверяет подключение с помощью метода [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="74572-185">The code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) to connect to Azure Database for PostgreSQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="74572-186">[Дескриптор базы данных](https://golang.org/pkg/database/sql/#DB) используется для всех компонентов. Он содержит пул подключений к серверу базы данных.</span><span class="sxs-lookup"><span data-stu-id="74572-186">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="74572-187">Этот код вызывает метод [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) для выполнения инструкции SQL, которая обновляет таблицу.</span><span class="sxs-lookup"><span data-stu-id="74572-187">The code calls the [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method to run the SQL statement that updates the table.</span></span> <span data-ttu-id="74572-188">Пользовательский метод checkError() применяется для проверки наличия ошибок и аварийного выхода при их обнаружении.</span><span class="sxs-lookup"><span data-stu-id="74572-188">A custom checkError() method to check if an error occurred and panic to exit if an error occurs.</span></span>

<span data-ttu-id="74572-189">Замените значения параметров `HOST`, `DATABASE`, `USER` и `PASSWORD` своими значениями.</span><span class="sxs-lookup"><span data-stu-id="74572-189">Replace the `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 
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
    fmt.Println("Successfully created connection to database")

    // Modify some data in table.
    sql_statement := "UPDATE inventory SET quantity = $2 WHERE name = $1;"
    _, err = db.Exec(sql_statement, "banana", 200)
    checkError(err)
    fmt.Println("Updated 1 row of data")
}
```

## <a name="delete-data"></a><span data-ttu-id="74572-190">Удаление данных</span><span class="sxs-lookup"><span data-stu-id="74572-190">Delete data</span></span>
<span data-ttu-id="74572-191">Используйте указанный ниже код с инструкцией SQL **DELETE** для подключения и чтения данных.</span><span class="sxs-lookup"><span data-stu-id="74572-191">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="74572-192">Код импортирует три пакета: [пакет sql](https://golang.org/pkg/database/sql/), [пакет pq](http://godoc.org/github.com/lib/pq) как драйвер для обмена данными с сервером Postgres и [пакет fmt](https://golang.org/pkg/fmt/) для вывода входных и выходных данных в командной строке.</span><span class="sxs-lookup"><span data-stu-id="74572-192">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [pq package](http://godoc.org/github.com/lib/pq) as a driver to communicate with the Postgres server, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="74572-193">Код вызывает метод [sql.Open()](http://godoc.org/github.com/lib/pq#Open) для подключения к базе данных Azure для PostgreSQL, а затем проверяет подключение с помощью метода [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="74572-193">The code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) to connect to Azure Database for PostgreSQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="74572-194">[Дескриптор базы данных](https://golang.org/pkg/database/sql/#DB) используется для всех компонентов. Он содержит пул подключений к серверу базы данных.</span><span class="sxs-lookup"><span data-stu-id="74572-194">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="74572-195">Этот код вызывает метод [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) для выполнения инструкции SQL, которая обновляет таблицу.</span><span class="sxs-lookup"><span data-stu-id="74572-195">The code calls the [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method to run the SQL statement that updates the table.</span></span> <span data-ttu-id="74572-196">Пользовательский метод checkError() применяется для проверки наличия ошибок и аварийного выхода при их обнаружении.</span><span class="sxs-lookup"><span data-stu-id="74572-196">A custom checkError() method to check if an error occurred and panic to exit if an error occurs.</span></span>

<span data-ttu-id="74572-197">Замените значения параметров `HOST`, `DATABASE`, `USER` и `PASSWORD` своими значениями.</span><span class="sxs-lookup"><span data-stu-id="74572-197">Replace the `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 
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
    fmt.Println("Successfully created connection to database")

    // Delete some data from table.
    sql_statement := "DELETE FROM inventory WHERE name = $1;"
    _, err = db.Exec(sql_statement, "orange")
    checkError(err)
    fmt.Println("Deleted 1 row of data")
}
```

## <a name="next-steps"></a><span data-ttu-id="74572-198">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="74572-198">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="74572-199">Перенос базы данных с помощью экспорта и импорта</span><span class="sxs-lookup"><span data-stu-id="74572-199">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
