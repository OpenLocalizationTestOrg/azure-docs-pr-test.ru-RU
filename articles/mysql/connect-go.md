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
# <a name="azure-database-for-mysql-use-go-language-tooconnect-and-query-data"></a><span data-ttu-id="258d3-103">База данных Azure для MySQL: используют команду Go языка tooconnect и запроса данных</span><span class="sxs-lookup"><span data-stu-id="258d3-103">Azure Database for MySQL: Use Go language tooconnect and query data</span></span>
<span data-ttu-id="258d3-104">Краткого руководства показано, как tooan tooconnect базы данных Azure для MySQL с помощью кода hello написаны в [Go](https://golang.org/) язык, на основе Windows, Ubuntu Linux и Apple macOS платформы.</span><span class="sxs-lookup"><span data-stu-id="258d3-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using code written in hello [Go](https://golang.org/) language from Windows, Ubuntu Linux, and Apple macOS platforms.</span></span> <span data-ttu-id="258d3-105">Показано, как tooquery инструкций SQL toouse, вставка, обновление и удаление данных в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="258d3-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="258d3-106">В этой статье предполагается, что вы знакомы с разработкой, с помощью команды Go, но, чтобы новый tooworking с базой данных Azure для MySQL.</span><span class="sxs-lookup"><span data-stu-id="258d3-106">This article assumes you are familiar with development using Go, but that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="258d3-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="258d3-107">Prerequisites</span></span>
<span data-ttu-id="258d3-108">Это краткое руководство использует ресурсы hello, созданные в любой из этих руководствах по в качестве отправной точки.</span><span class="sxs-lookup"><span data-stu-id="258d3-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- <span data-ttu-id="258d3-109">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Создание сервера базы данных Azure для MySQL с помощью портала Azure)</span><span class="sxs-lookup"><span data-stu-id="258d3-109">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md)</span></span>
- <span data-ttu-id="258d3-110">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md) (Создание базы данных Azure для сервера MySQL с помощью Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="258d3-110">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md)</span></span>

## <a name="install-go-and-mysql-connector"></a><span data-ttu-id="258d3-111">Установка Go и соединителя MySQL</span><span class="sxs-lookup"><span data-stu-id="258d3-111">Install Go and MySQL connector</span></span>
<span data-ttu-id="258d3-112">Установка [Go](https://golang.org/doc/install) и hello [go-sql драйвер для MySQL](https://github.com/go-sql-driver/mysql#installation) на компьютере.</span><span class="sxs-lookup"><span data-stu-id="258d3-112">Install [Go](https://golang.org/doc/install) and hello [go-sql-driver for MySQL](https://github.com/go-sql-driver/mysql#installation) on your own machine.</span></span> <span data-ttu-id="258d3-113">В зависимости от используемой платформы выполните действия hello.</span><span class="sxs-lookup"><span data-stu-id="258d3-113">Depending on your platform, follow hello steps:</span></span>

### <a name="windows"></a><span data-ttu-id="258d3-114">Windows</span><span class="sxs-lookup"><span data-stu-id="258d3-114">Windows</span></span>
1. <span data-ttu-id="258d3-115">[Загрузить](https://golang.org/dl/) и установить Go для Microsoft Windows, в соответствии с toohello [инструкции по установке](https://golang.org/doc/install).</span><span class="sxs-lookup"><span data-stu-id="258d3-115">[Download](https://golang.org/dl/) and install Go for Microsoft Windows according toohello [installation instructions](https://golang.org/doc/install).</span></span>
2. <span data-ttu-id="258d3-116">Откройте командную строку hello из меню "Пуск" hello.</span><span class="sxs-lookup"><span data-stu-id="258d3-116">Launch hello command prompt from hello start menu.</span></span>
3. <span data-ttu-id="258d3-117">Создайте папку для проекта, например</span><span class="sxs-lookup"><span data-stu-id="258d3-117">Make a folder for your project such.</span></span> <span data-ttu-id="258d3-118">`mkdir  %USERPROFILE%\go\src\mysqlgo`.</span><span class="sxs-lookup"><span data-stu-id="258d3-118">`mkdir  %USERPROFILE%\go\src\mysqlgo`.</span></span>
4. <span data-ttu-id="258d3-119">Измените каталог в папке проекта hello, такие как `cd %USERPROFILE%\go\src\mysqlgo`.</span><span class="sxs-lookup"><span data-stu-id="258d3-119">Change directory into hello project folder, such as `cd %USERPROFILE%\go\src\mysqlgo`.</span></span>
5. <span data-ttu-id="258d3-120">Задайте переменную среды hello для каталога GOPATH toopoint toohello исходного кода.</span><span class="sxs-lookup"><span data-stu-id="258d3-120">Set hello environment variable for GOPATH toopoint toohello source code directory.</span></span> <span data-ttu-id="258d3-121">`set GOPATH=%USERPROFILE%\go`.</span><span class="sxs-lookup"><span data-stu-id="258d3-121">`set GOPATH=%USERPROFILE%\go`.</span></span>
6. <span data-ttu-id="258d3-122">Установка hello [go-sql драйвер для mysql](https://github.com/go-sql-driver/mysql#installation) , выполнив hello `go get github.com/go-sql-driver/mysql` команды.</span><span class="sxs-lookup"><span data-stu-id="258d3-122">Install hello [go-sql-driver for mysql](https://github.com/go-sql-driver/mysql#installation) by running hello `go get github.com/go-sql-driver/mysql` command.</span></span>

   <span data-ttu-id="258d3-123">Таким образом установка Go, а затем выполните следующие команды в командную строку hello:</span><span class="sxs-lookup"><span data-stu-id="258d3-123">In summary, install Go, then run these commands in hello command prompt:</span></span>
   ```cmd
   mkdir  %USERPROFILE%\go\src\mysqlgo
   cd %USERPROFILE%\go\src\mysqlgo
   set GOPATH=%USERPROFILE%\go
   go get github.com/go-sql-driver/mysql
   ```

### <a name="linux-ubuntu"></a><span data-ttu-id="258d3-124">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="258d3-124">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="258d3-125">Запустите консоль Bash hello.</span><span class="sxs-lookup"><span data-stu-id="258d3-125">Launch hello Bash shell.</span></span> 
2. <span data-ttu-id="258d3-126">Установите Go, выполнив команду `sudo apt-get install golang-go`.</span><span class="sxs-lookup"><span data-stu-id="258d3-126">Install Go by running `sudo apt-get install golang-go`.</span></span>
3. <span data-ttu-id="258d3-127">Создайте папку для проекта в корневом каталоге, например `mkdir -p ~/go/src/mysqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="258d3-127">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/mysqlgo/`.</span></span>
4. <span data-ttu-id="258d3-128">Изменить каталог, в папку hello, такие как `cd ~/go/src/mysqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="258d3-128">Change directory into hello folder, such as `cd ~/go/src/mysqlgo/`.</span></span>
5. <span data-ttu-id="258d3-129">Набор hello GOPATH среды переменной toopoint tooa допустимым исходным каталогом, таким как к текущей домашней папки перейдите в каталог.</span><span class="sxs-lookup"><span data-stu-id="258d3-129">Set hello GOPATH environment variable toopoint tooa valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="258d3-130">В оболочке bash hello, запустите `export GOPATH=~/go` tooadd hello мере directory hello GOPATH для текущего сеанса оболочки hello.</span><span class="sxs-lookup"><span data-stu-id="258d3-130">At hello bash shell, run `export GOPATH=~/go` tooadd hello go directory as hello GOPATH for hello current shell session.</span></span>
6. <span data-ttu-id="258d3-131">Установка hello [go-sql драйвер для mysql](https://github.com/go-sql-driver/mysql#installation) , выполнив hello `go get github.com/go-sql-driver/mysql` команды.</span><span class="sxs-lookup"><span data-stu-id="258d3-131">Install hello [go-sql-driver for mysql](https://github.com/go-sql-driver/mysql#installation) by running hello `go get github.com/go-sql-driver/mysql` command.</span></span>

   <span data-ttu-id="258d3-132">Выполните следующие команды Bash:</span><span class="sxs-lookup"><span data-stu-id="258d3-132">In summary, run these bash commands:</span></span>
   ```bash
   sudo apt-get install golang-go
   mkdir -p ~/go/src/mysqlgo/
   cd ~/go/src/mysqlgo/
   export GOPATH=~/go/
   go get github.com/go-sql-driver/mysql
   ```

### <a name="apple-macos"></a><span data-ttu-id="258d3-133">Apple macOS</span><span class="sxs-lookup"><span data-stu-id="258d3-133">Apple macOS</span></span>
1. <span data-ttu-id="258d3-134">Загрузите и установите перейдите в соответствии с toohello [инструкции по установке](https://golang.org/doc/install) сопоставления вашей платформы.</span><span class="sxs-lookup"><span data-stu-id="258d3-134">Download and install Go according toohello [installation instructions](https://golang.org/doc/install)  matching your platform.</span></span> 
2. <span data-ttu-id="258d3-135">Запустите консоль Bash hello.</span><span class="sxs-lookup"><span data-stu-id="258d3-135">Launch hello Bash shell.</span></span> 
3. <span data-ttu-id="258d3-136">Создайте папку для проекта в корневом каталоге, например `mkdir -p ~/go/src/mysqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="258d3-136">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/mysqlgo/`.</span></span>
4. <span data-ttu-id="258d3-137">Изменить каталог, в папку hello, такие как `cd ~/go/src/mysqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="258d3-137">Change directory into hello folder, such as `cd ~/go/src/mysqlgo/`.</span></span>
5. <span data-ttu-id="258d3-138">Набор hello GOPATH среды переменной toopoint tooa допустимым исходным каталогом, таким как к текущей домашней папки перейдите в каталог.</span><span class="sxs-lookup"><span data-stu-id="258d3-138">Set hello GOPATH environment variable toopoint tooa valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="258d3-139">В оболочке bash hello, запустите `export GOPATH=~/go` tooadd hello мере directory hello GOPATH для текущего сеанса оболочки hello.</span><span class="sxs-lookup"><span data-stu-id="258d3-139">At hello bash shell, run `export GOPATH=~/go` tooadd hello go directory as hello GOPATH for hello current shell session.</span></span>
6. <span data-ttu-id="258d3-140">Установка hello [go-sql драйвер для mysql](https://github.com/go-sql-driver/mysql#installation) , выполнив hello `go get github.com/go-sql-driver/mysql` команды.</span><span class="sxs-lookup"><span data-stu-id="258d3-140">Install hello [go-sql-driver for mysql](https://github.com/go-sql-driver/mysql#installation) by running hello `go get github.com/go-sql-driver/mysql` command.</span></span>

   <span data-ttu-id="258d3-141">Установите Go, а затем выполните следующие команды Bash:</span><span class="sxs-lookup"><span data-stu-id="258d3-141">In summary, install Go, then run these bash commands:</span></span>
   ```bash
   mkdir -p ~/go/src/mysqlgo/
   cd ~/go/src/mysqlgo/
   export GOPATH=~/go/
   go get github.com/go-sql-driver/mysql
   ```

## <a name="get-connection-information"></a><span data-ttu-id="258d3-142">Получение сведений о подключении</span><span class="sxs-lookup"><span data-stu-id="258d3-142">Get connection information</span></span>
<span data-ttu-id="258d3-143">Получите toohello tooconnect базы данных Azure для hello подключения сведения, необходимые для MySQL.</span><span class="sxs-lookup"><span data-stu-id="258d3-143">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="258d3-144">Необходимо hello server полное имя и учетные данные входа.</span><span class="sxs-lookup"><span data-stu-id="258d3-144">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="258d3-145">Войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="258d3-145">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="258d3-146">Hello левого меню на портале Azure, щелкните **все ресурсы** и выполните поиск сервера hello, можно creased, такие как **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="258d3-146">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have creased, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="258d3-147">Щелкните имя сервера hello **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="258d3-147">Click hello server name **myserver4demo**.</span></span>
4. <span data-ttu-id="258d3-148">Выберите hello server **свойства** страницы.</span><span class="sxs-lookup"><span data-stu-id="258d3-148">Select hello server's **Properties** page.</span></span> <span data-ttu-id="258d3-149">Запишите hello **имя сервера** и **имя входа администратора сервера**.</span><span class="sxs-lookup"><span data-stu-id="258d3-149">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="258d3-150">![Имя входа для администратора сервера в базе данных Azure для MySQL](./media/connect-go/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="258d3-150">![Azure Database for MySQL - Server Admin Login](./media/connect-go/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="258d3-151">Если вы забыли учетные данные входа сервера, перейдите toohello **Обзор** страница hello tooview: имя пользователя администратора сервера и, при необходимости переустановить пароль hello.</span><span class="sxs-lookup"><span data-stu-id="258d3-151">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>
   

## <a name="build-and-run-go-code"></a><span data-ttu-id="258d3-152">Сборка и выполнение кода Go</span><span class="sxs-lookup"><span data-stu-id="258d3-152">Build and run Go code</span></span> 
1. <span data-ttu-id="258d3-153">toowrite Golang кода можно использовать простой текстовый редактор, например «Блокнот» в Microsoft Windows [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) или [Nano](https://www.nano-editor.org/) в Ubuntu или TextEdit в macOS.</span><span class="sxs-lookup"><span data-stu-id="258d3-153">toowrite Golang code, you can use a simple text editor, such as Notepad in Microsoft Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) or [Nano](https://www.nano-editor.org/) in Ubuntu, or TextEdit in macOS.</span></span> <span data-ttu-id="258d3-154">Если вы предпочитаете использовать полнофункциональную интерактивную среду разработки (IDE), попробуйте [Gogland](https://www.jetbrains.com/go/) от JetBrains, [Visual Studio Code](https://code.visualstudio.com/) от Майкрософт или [Atom](https://atom.io/).</span><span class="sxs-lookup"><span data-stu-id="258d3-154">If you prefer a richer Interactive Development Environment (IDE) try [Gogland](https://www.jetbrains.com/go/) by Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) by Microsoft, or [Atom](https://atom.io/).</span></span>
2. <span data-ttu-id="258d3-155">Вставьте hello Go кода из разделов hello ниже в текстовые файлы и сохраните в папке проекта с расширением файла \*.go, такие как Windows-путь `%USERPROFILE%\go\src\mysqlgo\createtable.go` или путь Linux `~/go/src/mysqlgo/createtable.go`.</span><span class="sxs-lookup"><span data-stu-id="258d3-155">Paste hello Go code from hello sections below into text files, and save into your project folder with file extension \*.go, such as Windows path `%USERPROFILE%\go\src\mysqlgo\createtable.go` or Linux path `~/go/src/mysqlgo/createtable.go`.</span></span>
3. <span data-ttu-id="258d3-156">Найдите hello `HOST`, `DATABASE`, `USER`, и `PASSWORD` константы в коде hello и замена значений пример hello собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="258d3-156">Locate hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` constants in hello code, and replace hello example values with your own values.</span></span> 
4. <span data-ttu-id="258d3-157">Запустите командную строку hello или bash оболочки.</span><span class="sxs-lookup"><span data-stu-id="258d3-157">Launch hello command prompt or bash shell.</span></span> <span data-ttu-id="258d3-158">Перейдите в папку проекта.</span><span class="sxs-lookup"><span data-stu-id="258d3-158">Change directory into your project folder.</span></span> <span data-ttu-id="258d3-159">В Windows это будет команда `cd %USERPROFILE%\go\src\mysqlgo\`,</span><span class="sxs-lookup"><span data-stu-id="258d3-159">For example, on Windows `cd %USERPROFILE%\go\src\mysqlgo\`.</span></span> <span data-ttu-id="258d3-160">а в Linux — `cd ~/go/src/mysqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="258d3-160">On Linux `cd ~/go/src/mysqlgo/`.</span></span>  <span data-ttu-id="258d3-161">Некоторые редакторы IDE hello упомянутые обеспечивают возможности отладки и выполнения без использования команд оболочки.</span><span class="sxs-lookup"><span data-stu-id="258d3-161">Some of hello IDE editors mentioned offer debug and runtime capabilities without requiring shell commands.</span></span>
5. <span data-ttu-id="258d3-162">Выполните код hello, введя команду hello `go run createtable.go` toocompile hello приложение и запустите его.</span><span class="sxs-lookup"><span data-stu-id="258d3-162">Run hello code by typing hello command `go run createtable.go` toocompile hello application and run it.</span></span> 
6. <span data-ttu-id="258d3-163">Кроме того, код toobuild hello в приложении машинного кода, `go build createtable.go`, запустите `createtable.exe` toorun приложения hello.</span><span class="sxs-lookup"><span data-stu-id="258d3-163">Alternatively, toobuild hello code into a native application, `go build createtable.go`, then launch `createtable.exe` toorun hello application.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="258d3-164">Подключение, создание таблицы и вставка данных</span><span class="sxs-lookup"><span data-stu-id="258d3-164">Connect, create table, and insert data</span></span>
<span data-ttu-id="258d3-165">Используйте следующие hello кода tooconnect toohello сервера, создайте таблицу и загружать данные при помощи hello **вставить** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="258d3-165">Use hello following code tooconnect toohello server, create a table, and load hello data using an **INSERT** SQL statement.</span></span> 

<span data-ttu-id="258d3-166">Код Hello импортирует три пакета: hello [пакета sql](https://golang.org/pkg/database/sql/), hello [драйвера перейдите sql для mysql](https://github.com/go-sql-driver/mysql#installation) как драйвер toocommunicate с hello базы данных Azure для MySQL и hello [fmt пакета](https://golang.org/pkg/fmt/)для печати ввода и вывода в командной строке hello.</span><span class="sxs-lookup"><span data-stu-id="258d3-166">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver toocommunicate with hello Azure Database for MySQL, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="258d3-167">Hello код вызывает метод [sql. Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure базы данных MySQL и для проверки подключения hello, с помощью метода [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="258d3-167">hello code calls method [sql.Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure Database for MySQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="258d3-168">Объект [дескриптор базы данных](https://golang.org/pkg/database/sql/#DB) для всех компонентов, удерживая hello пула соединений для сервера базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="258d3-168">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="258d3-169">hello вызовы кода Hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) метода несколько раз toorun несколько команд DDL.</span><span class="sxs-lookup"><span data-stu-id="258d3-169">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method several times toorun several DDL commands.</span></span> <span data-ttu-id="258d3-170">Привет код также использует hello [Prepare()](http://go-database-sql.org/prepared.html) и Exec() toorun подготовленных инструкций с различными параметрами tooinsert трех строк.</span><span class="sxs-lookup"><span data-stu-id="258d3-170">hello code also uses hello [Prepare()](http://go-database-sql.org/prepared.html) and Exec() toorun prepared statements with different parameters tooinsert three rows.</span></span> <span data-ttu-id="258d3-171">Если произошла ошибка и панику tooexit каждый раз, метод пользовательских checkError() — используется toocheck.</span><span class="sxs-lookup"><span data-stu-id="258d3-171">Each time a custom checkError() method is used toocheck if an error occurred and panic tooexit.</span></span>

<span data-ttu-id="258d3-172">Замените hello `host`, `database`, `user`, и `password` константы собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="258d3-172">Replace hello `host`, `database`, `user`, and `password` constants with your own values.</span></span> 

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

## <a name="read-data"></a><span data-ttu-id="258d3-173">Считывание данных</span><span class="sxs-lookup"><span data-stu-id="258d3-173">Read data</span></span>
<span data-ttu-id="258d3-174">Используйте следующие hello кода tooconnect и чтения данных с помощью hello **ВЫБЕРИТЕ** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="258d3-174">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="258d3-175">Код Hello импортирует три пакета: hello [пакета sql](https://golang.org/pkg/database/sql/), hello [драйвера перейдите sql для mysql](https://github.com/go-sql-driver/mysql#installation) как драйвер toocommunicate с hello базы данных Azure для MySQL и hello [fmt пакета](https://golang.org/pkg/fmt/)для печати ввода и вывода в командной строке hello.</span><span class="sxs-lookup"><span data-stu-id="258d3-175">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver toocommunicate with hello Azure Database for MySQL, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="258d3-176">Hello код вызывает метод [sql. Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure базы данных MySQL и для проверки подключения hello, с помощью метода [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="258d3-176">hello code calls method [sql.Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure Database for MySQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="258d3-177">Объект [дескриптор базы данных](https://golang.org/pkg/database/sql/#DB) для всех компонентов, удерживая hello пула соединений для сервера базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="258d3-177">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="258d3-178">hello вызовы кода Hello [Query()](https://golang.org/pkg/database/sql/#DB.Query) команды select hello toorun метод.</span><span class="sxs-lookup"><span data-stu-id="258d3-178">hello code calls hello [Query()](https://golang.org/pkg/database/sql/#DB.Query) method toorun hello select command.</span></span> <span data-ttu-id="258d3-179">Затем он выполняет [Next()](https://golang.org/pkg/database/sql/#Rows.Next) tooiterate hello результирующего набора и [Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) значений столбцов tooparse hello, сохранение значение hello в переменные.</span><span class="sxs-lookup"><span data-stu-id="258d3-179">Then it runs [Next()](https://golang.org/pkg/database/sql/#Rows.Next) tooiterate through hello result set and [Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) tooparse hello column values, saving hello value into variables.</span></span> <span data-ttu-id="258d3-180">Если произошла ошибка и панику tooexit каждый раз, метод пользовательских checkError() — используется toocheck.</span><span class="sxs-lookup"><span data-stu-id="258d3-180">Each time a custom checkError() method is used toocheck if an error occurred and panic tooexit.</span></span>

<span data-ttu-id="258d3-181">Замените hello `host`, `database`, `user`, и `password` константы собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="258d3-181">Replace hello `host`, `database`, `user`, and `password` constants with your own values.</span></span> 

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

## <a name="update-data"></a><span data-ttu-id="258d3-182">Обновление данных</span><span class="sxs-lookup"><span data-stu-id="258d3-182">Update data</span></span>
<span data-ttu-id="258d3-183">Используйте следующие hello кода tooconnect и обновления данных с помощью hello **обновление** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="258d3-183">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span> 

<span data-ttu-id="258d3-184">Код Hello импортирует три пакета: hello [пакета sql](https://golang.org/pkg/database/sql/), hello [драйвера перейдите sql для mysql](https://github.com/go-sql-driver/mysql#installation) как драйвер toocommunicate с hello базы данных Azure для MySQL и hello [fmt пакета](https://golang.org/pkg/fmt/)для печати ввода и вывода в командной строке hello.</span><span class="sxs-lookup"><span data-stu-id="258d3-184">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver toocommunicate with hello Azure Database for MySQL, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="258d3-185">Hello код вызывает метод [sql. Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure базы данных MySQL и для проверки подключения hello, с помощью метода [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="258d3-185">hello code calls method [sql.Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure Database for MySQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="258d3-186">Объект [дескриптор базы данных](https://golang.org/pkg/database/sql/#DB) для всех компонентов, удерживая hello пула соединений для сервера базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="258d3-186">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="258d3-187">hello вызовы кода Hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) команды update метод toorun hello.</span><span class="sxs-lookup"><span data-stu-id="258d3-187">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method toorun hello update command.</span></span> <span data-ttu-id="258d3-188">Если произошла ошибка и панику tooexit каждый раз, метод пользовательских checkError() — используется toocheck.</span><span class="sxs-lookup"><span data-stu-id="258d3-188">Each time a custom checkError() method is used toocheck if an error occurred and panic tooexit.</span></span>

<span data-ttu-id="258d3-189">Замените hello `host`, `database`, `user`, и `password` константы собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="258d3-189">Replace hello `host`, `database`, `user`, and `password` constants with your own values.</span></span> 

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

## <a name="delete-data"></a><span data-ttu-id="258d3-190">Удаление данных</span><span class="sxs-lookup"><span data-stu-id="258d3-190">Delete data</span></span>
<span data-ttu-id="258d3-191">Используйте следующие hello кода tooconnect и удаление данных с помощью **удалить** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="258d3-191">Use hello following code tooconnect and remove data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="258d3-192">Код Hello импортирует три пакета: hello [пакета sql](https://golang.org/pkg/database/sql/), hello [драйвера перейдите sql для mysql](https://github.com/go-sql-driver/mysql#installation) как драйвер toocommunicate с hello базы данных Azure для MySQL и hello [fmt пакета](https://golang.org/pkg/fmt/)для печати ввода и вывода в командной строке hello.</span><span class="sxs-lookup"><span data-stu-id="258d3-192">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver toocommunicate with hello Azure Database for MySQL, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="258d3-193">Hello код вызывает метод [sql. Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure базы данных MySQL и для проверки подключения hello, с помощью метода [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="258d3-193">hello code calls method [sql.Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure Database for MySQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="258d3-194">Объект [дескриптор базы данных](https://golang.org/pkg/database/sql/#DB) для всех компонентов, удерживая hello пула соединений для сервера базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="258d3-194">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="258d3-195">hello вызовы кода Hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) метод toorun hello удалить команду.</span><span class="sxs-lookup"><span data-stu-id="258d3-195">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method toorun hello delete command.</span></span> <span data-ttu-id="258d3-196">Если произошла ошибка и панику tooexit каждый раз, метод пользовательских checkError() — используется toocheck.</span><span class="sxs-lookup"><span data-stu-id="258d3-196">Each time a custom checkError() method is used toocheck if an error occurred and panic tooexit.</span></span>

<span data-ttu-id="258d3-197">Замените hello `host`, `database`, `user`, и `password` константы собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="258d3-197">Replace hello `host`, `database`, `user`, and `password` constants with your own values.</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="258d3-198">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="258d3-198">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="258d3-199">Перенос базы данных с помощью экспорта и импорта</span><span class="sxs-lookup"><span data-stu-id="258d3-199">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
