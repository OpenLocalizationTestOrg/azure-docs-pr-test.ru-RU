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
# <a name="azure-database-for-postgresql-use-go-language-tooconnect-and-query-data"></a><span data-ttu-id="2c360-103">База данных Azure для PostgreSQL: используют команду Go языка tooconnect и запроса данных</span><span class="sxs-lookup"><span data-stu-id="2c360-103">Azure Database for PostgreSQL: Use Go language tooconnect and query data</span></span>
<span data-ttu-id="2c360-104">Краткого руководства показано, как tooan tooconnect базы данных Azure для использования PostgreSQL кода hello написаны в [Go](https://golang.org/) языка (golang).</span><span class="sxs-lookup"><span data-stu-id="2c360-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using code written in hello [Go](https://golang.org/) language (golang).</span></span> <span data-ttu-id="2c360-105">Показано, как tooquery инструкций SQL toouse, вставка, обновление и удаление данных в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="2c360-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="2c360-106">В этой статье предполагается, что вы знакомы с разработкой, с помощью команды Go, но, чтобы новый tooworking с базой данных Azure для PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="2c360-106">This article assumes you are familiar with development using Go, but that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2c360-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="2c360-107">Prerequisites</span></span>
<span data-ttu-id="2c360-108">Это краткое руководство использует ресурсы hello, созданные в любой из этих руководствах по в качестве отправной точки.</span><span class="sxs-lookup"><span data-stu-id="2c360-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="2c360-109">Создание базы данных с помощью портала</span><span class="sxs-lookup"><span data-stu-id="2c360-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="2c360-110">Создание базы данных с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="2c360-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

## <a name="install-go-and-pq-connector"></a><span data-ttu-id="2c360-111">Установка Go и соединителя pq</span><span class="sxs-lookup"><span data-stu-id="2c360-111">Install Go and pq connector</span></span>
<span data-ttu-id="2c360-112">Установка [Go](https://golang.org/doc/install) и hello [драйвер чисто Postgres Go (pq)](https://github.com/lib/pq) на компьютере.</span><span class="sxs-lookup"><span data-stu-id="2c360-112">Install [Go](https://golang.org/doc/install) and hello [Pure Go Postgres driver (pq)](https://github.com/lib/pq) on your own machine.</span></span> <span data-ttu-id="2c360-113">В зависимости от используемой платформы выполните действия hello.</span><span class="sxs-lookup"><span data-stu-id="2c360-113">Depending on your platform, follow hello steps:</span></span>

### <a name="windows"></a><span data-ttu-id="2c360-114">Windows</span><span class="sxs-lookup"><span data-stu-id="2c360-114">Windows</span></span>
1. <span data-ttu-id="2c360-115">[Загрузить](https://golang.org/dl/) и установить Go для Microsoft Windows, в соответствии с toohello [инструкции по установке](https://golang.org/doc/install).</span><span class="sxs-lookup"><span data-stu-id="2c360-115">[Download](https://golang.org/dl/) and install Go for Microsoft Windows according toohello [installation instructions](https://golang.org/doc/install).</span></span>
2. <span data-ttu-id="2c360-116">Откройте командную строку hello из меню "Пуск" hello.</span><span class="sxs-lookup"><span data-stu-id="2c360-116">Launch hello command prompt from hello start menu.</span></span>
3. <span data-ttu-id="2c360-117">Создайте папку для проекта, например</span><span class="sxs-lookup"><span data-stu-id="2c360-117">Make a folder for your project such.</span></span> <span data-ttu-id="2c360-118">`mkdir  %USERPROFILE%\go\src\postgresqlgo`.</span><span class="sxs-lookup"><span data-stu-id="2c360-118">`mkdir  %USERPROFILE%\go\src\postgresqlgo`.</span></span>
4. <span data-ttu-id="2c360-119">Измените каталог в папке проекта hello, такие как `cd %USERPROFILE%\go\src\postgresqlgo`.</span><span class="sxs-lookup"><span data-stu-id="2c360-119">Change directory into hello project folder, such as `cd %USERPROFILE%\go\src\postgresqlgo`.</span></span>
5. <span data-ttu-id="2c360-120">Задайте переменную среды hello для каталога GOPATH toopoint toohello исходного кода.</span><span class="sxs-lookup"><span data-stu-id="2c360-120">Set hello environment variable for GOPATH toopoint toohello source code directory.</span></span> <span data-ttu-id="2c360-121">`set GOPATH=%USERPROFILE%\go`.</span><span class="sxs-lookup"><span data-stu-id="2c360-121">`set GOPATH=%USERPROFILE%\go`.</span></span>
6. <span data-ttu-id="2c360-122">Установка hello [драйвер чисто Postgres Go (pq)](https://github.com/lib/pq) , выполнив hello `go get github.com/lib/pq` команды.</span><span class="sxs-lookup"><span data-stu-id="2c360-122">Install hello [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running hello `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="2c360-123">Таким образом установка Go, а затем выполните следующие команды в командную строку hello:</span><span class="sxs-lookup"><span data-stu-id="2c360-123">In summary, install Go, then run these commands in hello command prompt:</span></span>
   ```cmd
   mkdir  %USERPROFILE%\go\src\postgresqlgo
   cd %USERPROFILE%\go\src\postgresqlgo
   set GOPATH=%USERPROFILE%\go
   go get github.com/lib/pq
   ```

### <a name="linux-ubuntu"></a><span data-ttu-id="2c360-124">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="2c360-124">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="2c360-125">Запустите консоль Bash hello.</span><span class="sxs-lookup"><span data-stu-id="2c360-125">Launch hello Bash shell.</span></span> 
2. <span data-ttu-id="2c360-126">Установите Go, выполнив команду `sudo apt-get install golang-go`.</span><span class="sxs-lookup"><span data-stu-id="2c360-126">Install Go by running `sudo apt-get install golang-go`.</span></span>
3. <span data-ttu-id="2c360-127">Создайте папку для проекта в корневом каталоге, например `mkdir -p ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="2c360-127">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/postgresqlgo/`.</span></span>
4. <span data-ttu-id="2c360-128">Изменить каталог, в папку hello, такие как `cd ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="2c360-128">Change directory into hello folder, such as `cd ~/go/src/postgresqlgo/`.</span></span>
5. <span data-ttu-id="2c360-129">Набор hello GOPATH среды переменной toopoint tooa допустимым исходным каталогом, таким как к текущей домашней папки перейдите в каталог.</span><span class="sxs-lookup"><span data-stu-id="2c360-129">Set hello GOPATH environment variable toopoint tooa valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="2c360-130">В оболочке bash hello, запустите `export GOPATH=~/go` tooadd hello мере directory hello GOPATH для текущего сеанса оболочки hello.</span><span class="sxs-lookup"><span data-stu-id="2c360-130">At hello bash shell, run `export GOPATH=~/go` tooadd hello go directory as hello GOPATH for hello current shell session.</span></span>
6. <span data-ttu-id="2c360-131">Установка hello [драйвер чисто Postgres Go (pq)](https://github.com/lib/pq) , выполнив hello `go get github.com/lib/pq` команды.</span><span class="sxs-lookup"><span data-stu-id="2c360-131">Install hello [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running hello `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="2c360-132">Выполните следующие команды Bash:</span><span class="sxs-lookup"><span data-stu-id="2c360-132">In summary, run these bash commands:</span></span>
   ```bash
   sudo apt-get install golang-go
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

### <a name="apple-macos"></a><span data-ttu-id="2c360-133">Apple macOS</span><span class="sxs-lookup"><span data-stu-id="2c360-133">Apple macOS</span></span>
1. <span data-ttu-id="2c360-134">Загрузите и установите перейдите в соответствии с toohello [инструкции по установке](https://golang.org/doc/install) сопоставления вашей платформы.</span><span class="sxs-lookup"><span data-stu-id="2c360-134">Download and install Go according toohello [installation instructions](https://golang.org/doc/install)  matching your platform.</span></span> 
2. <span data-ttu-id="2c360-135">Запустите консоль Bash hello.</span><span class="sxs-lookup"><span data-stu-id="2c360-135">Launch hello Bash shell.</span></span> 
3. <span data-ttu-id="2c360-136">Создайте папку для проекта в корневом каталоге, например `mkdir -p ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="2c360-136">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/postgresqlgo/`.</span></span>
4. <span data-ttu-id="2c360-137">Изменить каталог, в папку hello, такие как `cd ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="2c360-137">Change directory into hello folder, such as `cd ~/go/src/postgresqlgo/`.</span></span>
5. <span data-ttu-id="2c360-138">Набор hello GOPATH среды переменной toopoint tooa допустимым исходным каталогом, таким как к текущей домашней папки перейдите в каталог.</span><span class="sxs-lookup"><span data-stu-id="2c360-138">Set hello GOPATH environment variable toopoint tooa valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="2c360-139">В оболочке bash hello, запустите `export GOPATH=~/go` tooadd hello мере directory hello GOPATH для текущего сеанса оболочки hello.</span><span class="sxs-lookup"><span data-stu-id="2c360-139">At hello bash shell, run `export GOPATH=~/go` tooadd hello go directory as hello GOPATH for hello current shell session.</span></span>
6. <span data-ttu-id="2c360-140">Установка hello [драйвер чисто Postgres Go (pq)](https://github.com/lib/pq) , выполнив hello `go get github.com/lib/pq` команды.</span><span class="sxs-lookup"><span data-stu-id="2c360-140">Install hello [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running hello `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="2c360-141">Установите Go, а затем выполните следующие команды Bash:</span><span class="sxs-lookup"><span data-stu-id="2c360-141">In summary, install Go, then run these bash commands:</span></span>
   ```bash
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

## <a name="get-connection-information"></a><span data-ttu-id="2c360-142">Получение сведений о подключении</span><span class="sxs-lookup"><span data-stu-id="2c360-142">Get connection information</span></span>
<span data-ttu-id="2c360-143">Получите toohello tooconnect базы данных Azure для hello подключения сведения, необходимые для PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="2c360-143">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="2c360-144">Необходимо hello server полное имя и учетные данные входа.</span><span class="sxs-lookup"><span data-stu-id="2c360-144">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="2c360-145">Войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2c360-145">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="2c360-146">Hello левого меню на портале Azure, щелкните **все ресурсы** и выполните поиск сервера hello, вы создали, таких как **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="2c360-146">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="2c360-147">Щелкните имя сервера hello **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="2c360-147">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="2c360-148">Выберите hello server **Обзор** страницы.</span><span class="sxs-lookup"><span data-stu-id="2c360-148">Select hello server's **Overview** page.</span></span> <span data-ttu-id="2c360-149">Запишите hello **имя сервера** и **имя входа администратора сервера**.</span><span class="sxs-lookup"><span data-stu-id="2c360-149">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="2c360-150">![База данных Azure для PostgreSQL. Учетные данные администратора сервера для входа](./media/connect-go/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="2c360-150">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-go/1-connection-string.png)</span></span>
5. <span data-ttu-id="2c360-151">Если вы забыли учетные данные входа сервера, перейдите toohello **Обзор** страницы и имя входа администратора сервера hello представления.</span><span class="sxs-lookup"><span data-stu-id="2c360-151">If you forget your server login information, navigate toohello **Overview** page, and view hello Server admin login name.</span></span> <span data-ttu-id="2c360-152">При необходимости hello сброс пароля.</span><span class="sxs-lookup"><span data-stu-id="2c360-152">If necessary, reset hello password.</span></span>

## <a name="build-and-run-go-code"></a><span data-ttu-id="2c360-153">Сборка и выполнение кода Go</span><span class="sxs-lookup"><span data-stu-id="2c360-153">Build and run Go code</span></span> 
1. <span data-ttu-id="2c360-154">toowrite Golang кода можно использовать простой текстовый редактор, например «Блокнот» в Microsoft Windows [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) или [Nano](https://www.nano-editor.org/) в Ubuntu или TextEdit в macOS.</span><span class="sxs-lookup"><span data-stu-id="2c360-154">toowrite Golang code, you can use a simple text editor, such as Notepad in Microsoft Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) or [Nano](https://www.nano-editor.org/) in Ubuntu, or TextEdit in macOS.</span></span> <span data-ttu-id="2c360-155">Если вы предпочитаете использовать полнофункциональную интерактивную среду разработки (IDE), попробуйте [Gogland](https://www.jetbrains.com/go/) от JetBrains, [Visual Studio Code](https://code.visualstudio.com/) от Майкрософт или [Atom](https://atom.io/).</span><span class="sxs-lookup"><span data-stu-id="2c360-155">If you prefer a richer Interactive Development Environment (IDE) try [Gogland](https://www.jetbrains.com/go/) by Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) by Microsoft, or [Atom](https://atom.io/).</span></span>
2. <span data-ttu-id="2c360-156">Вставьте код Golang hello с hello разделов ниже текстовые файлы и сохранить в папке проекта с расширением файла \*.go, такие как Windows-путь `%USERPROFILE%\go\src\postgresqlgo\createtable.go` или путь Linux `~/go/src/postgresqlgo/createtable.go`.</span><span class="sxs-lookup"><span data-stu-id="2c360-156">Paste hello Golang code from hello sections below into text files, and save into your project folder with file extension \*.go, such as Windows path `%USERPROFILE%\go\src\postgresqlgo\createtable.go` or Linux path `~/go/src/postgresqlgo/createtable.go`.</span></span>
3. <span data-ttu-id="2c360-157">Найдите hello `HOST`, `DATABASE`, `USER`, и `PASSWORD` константы в коде hello и замена значений пример hello собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="2c360-157">Locate hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` constants in hello code, and replace hello example values with your own values.</span></span>  
4. <span data-ttu-id="2c360-158">Запустите командную строку hello или bash оболочки.</span><span class="sxs-lookup"><span data-stu-id="2c360-158">Launch hello command prompt or bash shell.</span></span> <span data-ttu-id="2c360-159">Перейдите в папку проекта.</span><span class="sxs-lookup"><span data-stu-id="2c360-159">Change directory into your project folder.</span></span> <span data-ttu-id="2c360-160">В Windows это будет команда `cd %USERPROFILE%\go\src\postgresqlgo\`,</span><span class="sxs-lookup"><span data-stu-id="2c360-160">For example, on Windows `cd %USERPROFILE%\go\src\postgresqlgo\`.</span></span> <span data-ttu-id="2c360-161">а в Linux — `cd ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="2c360-161">On Linux `cd ~/go/src/postgresqlgo/`.</span></span> <span data-ttu-id="2c360-162">Некоторые из упомянутых сред IDE hello обеспечивают возможности отладки и выполнения без использования команд оболочки.</span><span class="sxs-lookup"><span data-stu-id="2c360-162">Some of hello IDE environments mentioned offer debug and runtime capabilities without requiring shell commands.</span></span>
5. <span data-ttu-id="2c360-163">Выполните код hello, введя команду hello `go run createtable.go` toocompile hello приложение и запустите его.</span><span class="sxs-lookup"><span data-stu-id="2c360-163">Run hello code by typing hello command `go run createtable.go` toocompile hello application and run it.</span></span> 
6. <span data-ttu-id="2c360-164">Кроме того, код toobuild hello в приложении машинного кода, `go build createtable.go`, запустите `createtable.exe` toorun приложения hello.</span><span class="sxs-lookup"><span data-stu-id="2c360-164">Alternatively, toobuild hello code into a native application, `go build createtable.go`, then launch `createtable.exe` toorun hello application.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="2c360-165">Подключение и создание таблицы</span><span class="sxs-lookup"><span data-stu-id="2c360-165">Connect and create a table</span></span>
<span data-ttu-id="2c360-166">Используйте следующие hello кода tooconnect и создание таблицы с помощью **CREATE TABLE** инструкции SQL, за которым следует **INSERT INTO** строк tooadd инструкций SQL в таблицу hello.</span><span class="sxs-lookup"><span data-stu-id="2c360-166">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements tooadd rows into hello table.</span></span>

<span data-ttu-id="2c360-167">Код Hello импортирует три пакета: hello [пакета sql](https://golang.org/pkg/database/sql/), hello [pq пакета](http://godoc.org/github.com/lib/pq) как драйвер toocommunicate с сервером Postgres hello и hello [fmt пакета](https://golang.org/pkg/fmt/) для печати Ввод и вывод в командной строке hello.</span><span class="sxs-lookup"><span data-stu-id="2c360-167">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [pq package](http://godoc.org/github.com/lib/pq) as a driver toocommunicate with hello Postgres server, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="2c360-168">Hello код вызывает метод [sql. Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure базы данных PostgreSQL и для проверки подключения hello, с помощью метода [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="2c360-168">hello code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database for PostgreSQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="2c360-169">Объект [дескриптор базы данных](https://golang.org/pkg/database/sql/#DB) для всех компонентов, удерживая hello пула соединений для сервера базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="2c360-169">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="2c360-170">hello вызовы кода Hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) метода несколько раз toorun несколько команд SQL.</span><span class="sxs-lookup"><span data-stu-id="2c360-170">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method several times toorun several SQL commands.</span></span> <span data-ttu-id="2c360-171">Каждый раз toocheck checkError() пользовательский метод, если произошла ошибка и панику tooexit при возникновении ошибки.</span><span class="sxs-lookup"><span data-stu-id="2c360-171">Each time a custom checkError() method toocheck if an error occurred and panic tooexit if an error occurs.</span></span>

<span data-ttu-id="2c360-172">Замените hello `HOST`, `DATABASE`, `USER`, и `PASSWORD` параметры собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="2c360-172">Replace hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 

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

## <a name="read-data"></a><span data-ttu-id="2c360-173">Считывание данных</span><span class="sxs-lookup"><span data-stu-id="2c360-173">Read data</span></span>
<span data-ttu-id="2c360-174">Используйте следующие hello кода tooconnect и чтения данных с помощью hello **ВЫБЕРИТЕ** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="2c360-174">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="2c360-175">Код Hello импортирует три пакета: hello [пакета sql](https://golang.org/pkg/database/sql/), hello [pq пакета](http://godoc.org/github.com/lib/pq) как драйвер toocommunicate с сервером Postgres hello и hello [fmt пакета](https://golang.org/pkg/fmt/) для печати Ввод и вывод в командной строке hello.</span><span class="sxs-lookup"><span data-stu-id="2c360-175">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [pq package](http://godoc.org/github.com/lib/pq) as a driver toocommunicate with hello Postgres server, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="2c360-176">Hello код вызывает метод [sql. Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure базы данных PostgreSQL и для проверки подключения hello, с помощью метода [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="2c360-176">hello code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database for PostgreSQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="2c360-177">Объект [дескриптор базы данных](https://golang.org/pkg/database/sql/#DB) для всех компонентов, удерживая hello пула соединений для сервера базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="2c360-177">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="2c360-178">запрос select Hello выполняется путем вызова метода [db. Query()](https://golang.org/pkg/database/sql/#DB.Query), а hello результирующие строки хранятся в переменной типа [строк](https://golang.org/pkg/database/sql/#Rows).</span><span class="sxs-lookup"><span data-stu-id="2c360-178">hello select query is run by calling method [db.Query()](https://golang.org/pkg/database/sql/#DB.Query), and hello resulting rows is kept in a variable of type [rows](https://golang.org/pkg/database/sql/#Rows).</span></span> <span data-ttu-id="2c360-179">Код Hello считывает hello значения данных столбца в текущей строке hello, с помощью метода [строк. Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) и проходит по hello строк, с помощью итератора hello [строк. Next()](https://golang.org/pkg/database/sql/#Rows.Next) пока существует больше нет строк.</span><span class="sxs-lookup"><span data-stu-id="2c360-179">hello code reads hello column data values in hello current row using method [rows.Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) and loops over hello rows using hello iterator [rows.Next()](https://golang.org/pkg/database/sql/#Rows.Next) until no more rows exist.</span></span> <span data-ttu-id="2c360-180">Значения столбцов для каждой строки являются консоли печатной toohello out. Каждый раз toocheck checkError() пользовательский метод, если произошла ошибка и панику tooexit при возникновении ошибки.</span><span class="sxs-lookup"><span data-stu-id="2c360-180">Each row's column values are printed toohello console out. Each time a custom checkError() method toocheck if an error occurred and panic tooexit if an error occurs.</span></span>

<span data-ttu-id="2c360-181">Замените hello `HOST`, `DATABASE`, `USER`, и `PASSWORD` параметры собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="2c360-181">Replace hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 

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

## <a name="update-data"></a><span data-ttu-id="2c360-182">Обновление данных</span><span class="sxs-lookup"><span data-stu-id="2c360-182">Update data</span></span>
<span data-ttu-id="2c360-183">Используйте следующие hello кода tooconnect и обновления данных с помощью hello **обновление** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="2c360-183">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="2c360-184">Код Hello импортирует три пакета: hello [пакета sql](https://golang.org/pkg/database/sql/), hello [pq пакета](http://godoc.org/github.com/lib/pq) как драйвер toocommunicate с сервером Postgres hello и hello [fmt пакета](https://golang.org/pkg/fmt/) для печати Ввод и вывод в командной строке hello.</span><span class="sxs-lookup"><span data-stu-id="2c360-184">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [pq package](http://godoc.org/github.com/lib/pq) as a driver toocommunicate with hello Postgres server, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="2c360-185">Hello код вызывает метод [sql. Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure базы данных PostgreSQL и для проверки подключения hello, с помощью метода [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="2c360-185">hello code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database for PostgreSQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="2c360-186">Объект [дескриптор базы данных](https://golang.org/pkg/database/sql/#DB) для всех компонентов, удерживая hello пула соединений для сервера базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="2c360-186">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="2c360-187">hello вызовы кода Hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) метод toorun hello инструкции SQL, которая обновляет таблицу hello.</span><span class="sxs-lookup"><span data-stu-id="2c360-187">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method toorun hello SQL statement that updates hello table.</span></span> <span data-ttu-id="2c360-188">Toocheck checkError() пользовательский метод, если произошла ошибка и панику tooexit, если ошибка возникает.</span><span class="sxs-lookup"><span data-stu-id="2c360-188">A custom checkError() method toocheck if an error occurred and panic tooexit if an error occurs.</span></span>

<span data-ttu-id="2c360-189">Замените hello `HOST`, `DATABASE`, `USER`, и `PASSWORD` параметры собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="2c360-189">Replace hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 
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

## <a name="delete-data"></a><span data-ttu-id="2c360-190">Удаление данных</span><span class="sxs-lookup"><span data-stu-id="2c360-190">Delete data</span></span>
<span data-ttu-id="2c360-191">Используйте следующие hello кода tooconnect и чтения данных с помощью hello **удалить** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="2c360-191">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="2c360-192">Код Hello импортирует три пакета: hello [пакета sql](https://golang.org/pkg/database/sql/), hello [pq пакета](http://godoc.org/github.com/lib/pq) как драйвер toocommunicate с сервером Postgres hello и hello [fmt пакета](https://golang.org/pkg/fmt/) для печати Ввод и вывод в командной строке hello.</span><span class="sxs-lookup"><span data-stu-id="2c360-192">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [pq package](http://godoc.org/github.com/lib/pq) as a driver toocommunicate with hello Postgres server, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="2c360-193">Hello код вызывает метод [sql. Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure базы данных PostgreSQL и для проверки подключения hello, с помощью метода [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="2c360-193">hello code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database for PostgreSQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="2c360-194">Объект [дескриптор базы данных](https://golang.org/pkg/database/sql/#DB) для всех компонентов, удерживая hello пула соединений для сервера базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="2c360-194">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="2c360-195">hello вызовы кода Hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) метод toorun hello инструкции SQL, которая обновляет таблицу hello.</span><span class="sxs-lookup"><span data-stu-id="2c360-195">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method toorun hello SQL statement that updates hello table.</span></span> <span data-ttu-id="2c360-196">Toocheck checkError() пользовательский метод, если произошла ошибка и панику tooexit, если ошибка возникает.</span><span class="sxs-lookup"><span data-stu-id="2c360-196">A custom checkError() method toocheck if an error occurred and panic tooexit if an error occurs.</span></span>

<span data-ttu-id="2c360-197">Замените hello `HOST`, `DATABASE`, `USER`, и `PASSWORD` параметры собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="2c360-197">Replace hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 
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

## <a name="next-steps"></a><span data-ttu-id="2c360-198">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2c360-198">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="2c360-199">Перенос базы данных с помощью экспорта и импорта</span><span class="sxs-lookup"><span data-stu-id="2c360-199">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
