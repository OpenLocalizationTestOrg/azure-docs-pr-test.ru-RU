---
title: "aaaConnect tooAzure базы данных PostgreSQL, используя Ruby | Документы Microsoft"
description: "Это краткое руководство содержит пример Ruby кода можно использовать tooconnect и запроса данных из базы данных Azure для PostgreSQL."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: ruby
ms.topic: quickstart
ms.date: 06/30/2017
ms.openlocfilehash: 7a0c8c92023452b40ca19d76fa659744f3e9a236
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-ruby-tooconnect-and-query-data"></a><span data-ttu-id="56411-103">База данных Azure для PostgreSQL: используйте Ruby tooconnect и запроса данных</span><span class="sxs-lookup"><span data-stu-id="56411-103">Azure Database for PostgreSQL: Use Ruby tooconnect and query data</span></span>
<span data-ttu-id="56411-104">Краткого руководства показано, как tooconnect tooan Azure этой базы данных с помощью PostgreSQL [Ruby](https://www.ruby-lang.org) приложения.</span><span class="sxs-lookup"><span data-stu-id="56411-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using a [Ruby](https://www.ruby-lang.org) application.</span></span> <span data-ttu-id="56411-105">Показано, как tooquery инструкций SQL toouse, вставка, обновление и удаление данных в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="56411-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="56411-106">В этой статье предполагается, что вы знакомы с разработки, используя Ruby, но, чтобы новый tooworking с базой данных Azure для PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="56411-106">This article assumes you are familiar with development using Ruby, but that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="56411-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="56411-107">Prerequisites</span></span>
<span data-ttu-id="56411-108">Это краткое руководство использует ресурсы hello, созданные в любой из этих руководствах по в качестве отправной точки.</span><span class="sxs-lookup"><span data-stu-id="56411-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="56411-109">Создание базы данных с помощью портала</span><span class="sxs-lookup"><span data-stu-id="56411-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="56411-110">Создание базы данных с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="56411-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

## <a name="install-ruby"></a><span data-ttu-id="56411-111">Установка Ruby</span><span class="sxs-lookup"><span data-stu-id="56411-111">Install Ruby</span></span>
<span data-ttu-id="56411-112">Установите Ruby на своем компьютере.</span><span class="sxs-lookup"><span data-stu-id="56411-112">Install Ruby on your own machine.</span></span> 

### <a name="windows"></a><span data-ttu-id="56411-113">Windows</span><span class="sxs-lookup"><span data-stu-id="56411-113">Windows</span></span>
- <span data-ttu-id="56411-114">Загрузка и установка hello последнюю версию [Ruby](http://rubyinstaller.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="56411-114">Download and Install hello latest version of [Ruby](http://rubyinstaller.org/downloads/).</span></span>
- <span data-ttu-id="56411-115">На hello завершить экрана приветствия установщика MSI, установите флажок "hello" с сообщением «выполнения 'ridk установить' tooinstall MSYS2 и инструментов разработки.»</span><span class="sxs-lookup"><span data-stu-id="56411-115">On hello finish screen of hello MSI installer, check hello box that says "Run 'ridk install' tooinstall MSYS2 and development toolchain."</span></span> <span data-ttu-id="56411-116">Нажмите кнопку **Готово** toolaunch hello Далее установщика.</span><span class="sxs-lookup"><span data-stu-id="56411-116">Then click **Finish** toolaunch hello next installer.</span></span>
- <span data-ttu-id="56411-117">запускает установщик RubyInstaller2 для Windows Hello.</span><span class="sxs-lookup"><span data-stu-id="56411-117">hello RubyInstaller2 for Windows installer launches.</span></span> <span data-ttu-id="56411-118">Введите 2 обновление репозитория hello MSYS2 tooinstall.</span><span class="sxs-lookup"><span data-stu-id="56411-118">Type 2 tooinstall hello MSYS2 repository update.</span></span> <span data-ttu-id="56411-119">После завершения и возвращает toohello запрос на установку, закройте командное окно приветствия.</span><span class="sxs-lookup"><span data-stu-id="56411-119">After it finishes and returns toohello installation prompt, close hello command window.</span></span>
- <span data-ttu-id="56411-120">Из меню "Пуск" hello, запустите новую командную строку (cmd).</span><span class="sxs-lookup"><span data-stu-id="56411-120">Launch a new command prompt (cmd) from hello Start menu.</span></span>
- <span data-ttu-id="56411-121">Тест hello Ruby установки `ruby -v` установленной версии toosee hello.</span><span class="sxs-lookup"><span data-stu-id="56411-121">Test hello Ruby installation `ruby -v` toosee hello version installed.</span></span>
- <span data-ttu-id="56411-122">Проверьте установку Gem hello `gem -v` установленной версии toosee hello.</span><span class="sxs-lookup"><span data-stu-id="56411-122">Test hello Gem installation `gem -v` toosee hello version installed.</span></span>
- <span data-ttu-id="56411-123">Построить hello PostgreSQL модуль для Ruby, с помощью Gem, выполнив команду hello `gem install pg`.</span><span class="sxs-lookup"><span data-stu-id="56411-123">Build hello PostgreSQL module for Ruby using Gem by running hello command `gem install pg`.</span></span>

### <a name="macos"></a><span data-ttu-id="56411-124">MacOS</span><span class="sxs-lookup"><span data-stu-id="56411-124">MacOS</span></span>
- <span data-ttu-id="56411-125">Установка с помощью Homebrew, выполнив команду hello Ruby `brew install ruby`.</span><span class="sxs-lookup"><span data-stu-id="56411-125">Install Ruby using Homebrew by running hello command `brew install ruby`.</span></span> <span data-ttu-id="56411-126">Дополнительные параметры установки см. в разделе hello Ruby [документацию по установке](https://www.ruby-lang.org/en/documentation/installation/#homebrew)</span><span class="sxs-lookup"><span data-stu-id="56411-126">For more installation options, see hello Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/#homebrew)</span></span>
- <span data-ttu-id="56411-127">Тест hello Ruby установки `ruby -v` установленной версии toosee hello.</span><span class="sxs-lookup"><span data-stu-id="56411-127">Test hello Ruby installation `ruby -v` toosee hello version installed.</span></span>
- <span data-ttu-id="56411-128">Проверьте установку Gem hello `gem -v` установленной версии toosee hello.</span><span class="sxs-lookup"><span data-stu-id="56411-128">Test hello Gem installation `gem -v` toosee hello version installed.</span></span>
- <span data-ttu-id="56411-129">Построить hello PostgreSQL модуль для Ruby, с помощью Gem, выполнив команду hello `gem install pg`.</span><span class="sxs-lookup"><span data-stu-id="56411-129">Build hello PostgreSQL module for Ruby using Gem by running hello command `gem install pg`.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="56411-130">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="56411-130">Linux (Ubuntu)</span></span>
- <span data-ttu-id="56411-131">Установите Ruby, выполнив команду hello `sudo apt-get install ruby-full`.</span><span class="sxs-lookup"><span data-stu-id="56411-131">Install Ruby by running hello command `sudo apt-get install ruby-full`.</span></span> <span data-ttu-id="56411-132">Дополнительные параметры установки см. в разделе hello Ruby [документацию по установке](https://www.ruby-lang.org/en/documentation/installation/).</span><span class="sxs-lookup"><span data-stu-id="56411-132">For more installation options, see hello Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/).</span></span>
- <span data-ttu-id="56411-133">Тест hello Ruby установки `ruby -v` установленной версии toosee hello.</span><span class="sxs-lookup"><span data-stu-id="56411-133">Test hello Ruby installation `ruby -v` toosee hello version installed.</span></span>
- <span data-ttu-id="56411-134">Установите последние обновления hello для Gem, выполнив команду hello `sudo gem update --system`.</span><span class="sxs-lookup"><span data-stu-id="56411-134">Install hello latest updates for Gem by running hello command `sudo gem update --system`.</span></span>
- <span data-ttu-id="56411-135">Проверьте установку Gem hello `gem -v` установленной версии toosee hello.</span><span class="sxs-lookup"><span data-stu-id="56411-135">Test hello Gem installation `gem -v` toosee hello version installed.</span></span>
- <span data-ttu-id="56411-136">Установите hello gcc, того же типа и других средств построения, выполнив команду hello `sudo apt-get install build-essential`.</span><span class="sxs-lookup"><span data-stu-id="56411-136">Install hello gcc, make, and other build tools by running hello command `sudo apt-get install build-essential`.</span></span>
- <span data-ttu-id="56411-137">Установите hello PostgreSQL библиотеки, выполнив команду hello `sudo apt-get install libpq-dev`.</span><span class="sxs-lookup"><span data-stu-id="56411-137">Install hello PostgreSQL libraries by running hello command `sudo apt-get install libpq-dev`.</span></span>
- <span data-ttu-id="56411-138">Построить с помощью Gem, выполнив команду hello модуль Ruby pg hello `sudo gem install pg`.</span><span class="sxs-lookup"><span data-stu-id="56411-138">Build hello Ruby pg module using Gem by running hello command `sudo gem install pg`.</span></span>

## <a name="run-ruby-code"></a><span data-ttu-id="56411-139">Выполнение кода Ruby</span><span class="sxs-lookup"><span data-stu-id="56411-139">Run Ruby code</span></span> 
- <span data-ttu-id="56411-140">Сохраните код hello в текстовый файл и сохраните файл hello в проект папку с .rb расширение файла, такие как `C:\rubypostgres\read.rb` или`/home/username/rubypostgres/read.rb`</span><span class="sxs-lookup"><span data-stu-id="56411-140">Save hello code into a text file, and save hello file into a project folder with file extension .rb, such as `C:\rubypostgres\read.rb` or `/home/username/rubypostgres/read.rb`</span></span>
- <span data-ttu-id="56411-141">toorun hello кода, запустите командную строку hello или bash оболочки.</span><span class="sxs-lookup"><span data-stu-id="56411-141">toorun hello code, launch hello command prompt or bash shell.</span></span> <span data-ttu-id="56411-142">Перейдите в каталог в папке проекта `cd rubypostgres`, после чего введите команду hello `ruby read.rb` toorun приложения hello.</span><span class="sxs-lookup"><span data-stu-id="56411-142">Change directory into your project folder `cd rubypostgres`, then type hello command `ruby read.rb` toorun hello application.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="56411-143">Получение сведений о подключении</span><span class="sxs-lookup"><span data-stu-id="56411-143">Get connection information</span></span>
<span data-ttu-id="56411-144">Получите toohello tooconnect базы данных Azure для hello подключения сведения, необходимые для PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="56411-144">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="56411-145">Необходимо hello server полное имя и учетные данные входа.</span><span class="sxs-lookup"><span data-stu-id="56411-145">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="56411-146">Войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="56411-146">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="56411-147">Hello левого меню на портале Azure, щелкните **все ресурсы** и выполните поиск сервера hello, вы создали, таких как **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="56411-147">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="56411-148">Щелкните имя сервера hello **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="56411-148">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="56411-149">Выберите hello server **Обзор** страницы.</span><span class="sxs-lookup"><span data-stu-id="56411-149">Select hello server's **Overview** page.</span></span> <span data-ttu-id="56411-150">Запишите hello **имя сервера** и **имя входа администратора сервера**.</span><span class="sxs-lookup"><span data-stu-id="56411-150">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="56411-151">![База данных Azure для PostgreSQL. Учетные данные администратора сервера для входа](./media/connect-ruby/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="56411-151">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-ruby/1-connection-string.png)</span></span>
5. <span data-ttu-id="56411-152">Если вы забыли учетные данные входа сервера, перейдите toohello **Обзор** имя пользователя администратора сервера hello tooview страницы.</span><span class="sxs-lookup"><span data-stu-id="56411-152">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name.</span></span> <span data-ttu-id="56411-153">При необходимости hello сброс пароля.</span><span class="sxs-lookup"><span data-stu-id="56411-153">If necessary, reset hello password.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="56411-154">Подключение и создание таблицы</span><span class="sxs-lookup"><span data-stu-id="56411-154">Connect and create a table</span></span>
<span data-ttu-id="56411-155">Используйте следующие hello кода tooconnect и создание таблицы с помощью **CREATE TABLE** инструкции SQL, за которым следует **INSERT INTO** строк tooadd инструкций SQL в таблицу hello.</span><span class="sxs-lookup"><span data-stu-id="56411-155">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements tooadd rows into hello table.</span></span>

<span data-ttu-id="56411-156">использует код Hello [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) объекта с помощью конструктора [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure базы данных PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="56411-156">hello code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="56411-157">Затем он вызывает метод [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello: команд DROP, CREATE TABLE и INSERT INTO.</span><span class="sxs-lookup"><span data-stu-id="56411-157">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello DROP, CREATE TABLE, and INSERT INTO commands.</span></span> <span data-ttu-id="56411-158">Hello код проверяет наличие ошибок с помощью hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) класса.</span><span class="sxs-lookup"><span data-stu-id="56411-158">hello code checks for errors using hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="56411-159">Затем он вызывает метод [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello соединения перед завершением работы.</span><span class="sxs-lookup"><span data-stu-id="56411-159">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="56411-160">Замените hello `host`, `database`, `user`, и `password` строки собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="56411-160">Replace hello `host`, `database`, `user`, and `password` strings with your own values.</span></span> 
```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :dbname => database, :port => '5432', :password => password)
    puts 'Successfully created connection toodatabase'

    # Drop previous table of same name if one exists
    connection.exec('DROP TABLE IF EXISTS inventory;')
    puts 'Finished dropping table (if existed).'

    # Drop previous table of same name if one exists.
    connection.exec('CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);')
    puts 'Finished creating table.'

    # Insert some data into table.
    connection.exec("INSERT INTO inventory VALUES(1, 'banana', 150)")
    connection.exec("INSERT INTO inventory VALUES(2, 'orange', 154)")
    connection.exec("INSERT INTO inventory VALUES(3, 'apple', 100)")
    puts 'Inserted 3 rows of data.'

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```

## <a name="read-data"></a><span data-ttu-id="56411-161">Считывание данных</span><span class="sxs-lookup"><span data-stu-id="56411-161">Read data</span></span>
<span data-ttu-id="56411-162">Используйте следующие hello кода tooconnect и чтения данных с помощью hello **ВЫБЕРИТЕ** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="56411-162">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="56411-163">использует код Hello [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) объекта с помощью конструктора [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure базы данных PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="56411-163">hello code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="56411-164">Затем он вызывает метод [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello команды SELECT, сохранения результатов hello в результирующий набор.</span><span class="sxs-lookup"><span data-stu-id="56411-164">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello SELECT command, keeping hello results in a result set.</span></span> <span data-ttu-id="56411-165">Hello результирующий набор сбора проходит по hello `resultSet.each do` цикла, руководствуясь hello hello текущие значения строки `row` переменной.</span><span class="sxs-lookup"><span data-stu-id="56411-165">hello result set collection is iterated over using hello `resultSet.each do` loop, keeping hello current row values in hello `row` variable.</span></span> <span data-ttu-id="56411-166">Hello код проверяет наличие ошибок с помощью hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) класса.</span><span class="sxs-lookup"><span data-stu-id="56411-166">hello code checks for errors using hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="56411-167">Затем он вызывает метод [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello соединения перед завершением работы.</span><span class="sxs-lookup"><span data-stu-id="56411-167">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="56411-168">Замените hello `host`, `database`, `user`, и `password` строки собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="56411-168">Replace hello `host`, `database`, `user`, and `password` strings with your own values.</span></span> 

```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :database => dbname, :port => '5432', :password => password)
    puts 'Successfully created connection toodatabase.'

    resultSet = connection.exec('SELECT * from inventory;')
    resultSet.each do |row|
        puts 'Data row = (%s, %s, %s)' % [row['id'], row['name'], row['quantity']]
    end

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```

## <a name="update-data"></a><span data-ttu-id="56411-169">Обновление данных</span><span class="sxs-lookup"><span data-stu-id="56411-169">Update data</span></span>
<span data-ttu-id="56411-170">Используйте следующие hello кода tooconnect и обновления данных с помощью hello **обновление** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="56411-170">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="56411-171">использует код Hello [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) объекта с помощью конструктора [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure базы данных PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="56411-171">hello code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="56411-172">Затем он вызывает метод [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello команды UPDATE.</span><span class="sxs-lookup"><span data-stu-id="56411-172">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello UPDATE command.</span></span> <span data-ttu-id="56411-173">Hello код проверяет наличие ошибок с помощью hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) класса.</span><span class="sxs-lookup"><span data-stu-id="56411-173">hello code checks for errors using hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="56411-174">Затем он вызывает метод [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello соединения перед завершением работы.</span><span class="sxs-lookup"><span data-stu-id="56411-174">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="56411-175">Замените hello `host`, `database`, `user`, и `password` строки собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="56411-175">Replace hello `host`, `database`, `user`, and `password` strings with your own values.</span></span> 

```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :dbname => database, :port => '5432', :password => password)
    puts 'Successfully created connection toodatabase.'

    # Modify some data in table.
    connection.exec('UPDATE inventory SET quantity = %d WHERE name = %s;' % [200, '\'banana\''])
    puts 'Updated 1 row of data.'

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```


## <a name="delete-data"></a><span data-ttu-id="56411-176">Удаление данных</span><span class="sxs-lookup"><span data-stu-id="56411-176">Delete data</span></span>
<span data-ttu-id="56411-177">Используйте следующие hello кода tooconnect и чтения данных с помощью hello **удалить** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="56411-177">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="56411-178">использует код Hello [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) объекта с помощью конструктора [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure базы данных PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="56411-178">hello code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="56411-179">Затем он вызывает метод [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello команды UPDATE.</span><span class="sxs-lookup"><span data-stu-id="56411-179">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello UPDATE command.</span></span> <span data-ttu-id="56411-180">Hello код проверяет наличие ошибок с помощью hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) класса.</span><span class="sxs-lookup"><span data-stu-id="56411-180">hello code checks for errors using hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="56411-181">Затем он вызывает метод [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello соединения перед завершением работы.</span><span class="sxs-lookup"><span data-stu-id="56411-181">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="56411-182">Замените hello `host`, `database`, `user`, и `password` строки собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="56411-182">Replace hello `host`, `database`, `user`, and `password` strings with your own values.</span></span> 

```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :dbname => database, :port => '5432', :password => password)
    puts 'Successfully created connection toodatabase.'

    # Modify some data in table.
    connection.exec('DELETE FROM inventory WHERE name = %s;' % ['\'orange\''])
    puts 'Deleted 1 row of data.'

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```

## <a name="next-steps"></a><span data-ttu-id="56411-183">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="56411-183">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="56411-184">Перенос базы данных с помощью экспорта и импорта</span><span class="sxs-lookup"><span data-stu-id="56411-184">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
