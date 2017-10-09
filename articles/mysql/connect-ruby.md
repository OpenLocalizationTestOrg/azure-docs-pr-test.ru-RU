---
title: "Подключение tooAzure базы данных MySQL, используя Ruby | Документы Microsoft"
description: "Это краткое руководство несколько примеров, Ruby кода можно использовать tooconnect и запроса данных из базы данных Azure для MySQL."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: ruby
ms.topic: hero-article
ms.date: 07/13/2017
ms.openlocfilehash: ff0880dcc24e96f467c9092bc663ce3dc4c2637a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-ruby-tooconnect-and-query-data"></a><span data-ttu-id="7a506-103">База данных Azure для MySQL: используйте Ruby tooconnect и запроса данных</span><span class="sxs-lookup"><span data-stu-id="7a506-103">Azure Database for MySQL: Use Ruby tooconnect and query data</span></span>
<span data-ttu-id="7a506-104">Краткого руководства показано, как tooconnect tooan Azure этой базы данных MySQL с помощью [Ruby](https://www.ruby-lang.org) приложения и hello [mysql2](https://rubygems.org/gems/mysql2) gem из платформ Mac, Ubuntu Linux и Windows.</span><span class="sxs-lookup"><span data-stu-id="7a506-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using a [Ruby](https://www.ruby-lang.org) application and hello [mysql2](https://rubygems.org/gems/mysql2) gem from Windows, Ubuntu Linux, and Mac platforms.</span></span> <span data-ttu-id="7a506-105">Показано, как tooquery инструкций SQL toouse, вставка, обновление и удаление данных в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="7a506-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="7a506-106">В этой статье предполагается, что вы знакомы с разработки, используя Ruby, но, чтобы новый tooworking с базой данных Azure для MySQL.</span><span class="sxs-lookup"><span data-stu-id="7a506-106">This article assumes you are familiar with development using Ruby, but that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a506-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7a506-107">Prerequisites</span></span>
<span data-ttu-id="7a506-108">Это краткое руководство использует ресурсы hello, созданные в любой из этих руководствах по в качестве отправной точки.</span><span class="sxs-lookup"><span data-stu-id="7a506-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- <span data-ttu-id="7a506-109">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Создание сервера базы данных Azure для MySQL с помощью портала Azure)</span><span class="sxs-lookup"><span data-stu-id="7a506-109">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md)</span></span>
- <span data-ttu-id="7a506-110">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md) (Создание базы данных Azure для сервера MySQL с помощью Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="7a506-110">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md)</span></span>

## <a name="install-ruby"></a><span data-ttu-id="7a506-111">Установка Ruby</span><span class="sxs-lookup"><span data-stu-id="7a506-111">Install Ruby</span></span>
<span data-ttu-id="7a506-112">Установите на компьютере Ruby, Gem и библиотека MySQL2 hello.</span><span class="sxs-lookup"><span data-stu-id="7a506-112">Install Ruby, Gem, and hello MySQL2 library on your own machine.</span></span> 

### <a name="windows"></a><span data-ttu-id="7a506-113">Windows</span><span class="sxs-lookup"><span data-stu-id="7a506-113">Windows</span></span>
1. <span data-ttu-id="7a506-114">Загрузить и установить версию hello 2.3 [Ruby](http://rubyinstaller.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="7a506-114">Download and Install hello 2.3 version of [Ruby](http://rubyinstaller.org/downloads/).</span></span>
2. <span data-ttu-id="7a506-115">Из меню "Пуск" hello, запустите новую командную строку (cmd).</span><span class="sxs-lookup"><span data-stu-id="7a506-115">Launch a new command prompt (cmd) from hello Start menu.</span></span>
3. <span data-ttu-id="7a506-116">Перейдите в каталог в hello Ruby каталог для версии 2.3.</span><span class="sxs-lookup"><span data-stu-id="7a506-116">Change directory into hello Ruby directory for version 2.3.</span></span> `cd c:\Ruby23-x64\bin`
4. <span data-ttu-id="7a506-117">Тест hello Ruby установки, выполнив команду hello `ruby -v` установленной версии toosee hello.</span><span class="sxs-lookup"><span data-stu-id="7a506-117">Test hello Ruby installation by running hello command `ruby -v` toosee hello version installed.</span></span>
5. <span data-ttu-id="7a506-118">Проверьте установку Gem hello, выполнив команду hello `gem -v` установленной версии toosee hello.</span><span class="sxs-lookup"><span data-stu-id="7a506-118">Test hello Gem installation by running hello command `gem -v` toosee hello version installed.</span></span>
6. <span data-ttu-id="7a506-119">Построить hello Mysql2 модуль для Ruby, с помощью Gem, выполнив команду hello `gem install mysql2`.</span><span class="sxs-lookup"><span data-stu-id="7a506-119">Build hello Mysql2 module for Ruby using Gem by running hello command `gem install mysql2`.</span></span>

### <a name="macos"></a><span data-ttu-id="7a506-120">MacOS</span><span class="sxs-lookup"><span data-stu-id="7a506-120">MacOS</span></span>
1. <span data-ttu-id="7a506-121">Установка с помощью Homebrew, выполнив команду hello Ruby `brew install ruby`.</span><span class="sxs-lookup"><span data-stu-id="7a506-121">Install Ruby using Homebrew by running hello command `brew install ruby`.</span></span> <span data-ttu-id="7a506-122">Дополнительные параметры установки см. в разделе hello Ruby [документацию по установке](https://www.ruby-lang.org/en/documentation/installation/#homebrew).</span><span class="sxs-lookup"><span data-stu-id="7a506-122">For more installation options, see hello Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/#homebrew).</span></span>
2. <span data-ttu-id="7a506-123">Тест hello Ruby установки, выполнив команду hello `ruby -v` установленной версии toosee hello.</span><span class="sxs-lookup"><span data-stu-id="7a506-123">Test hello Ruby installation by running hello command `ruby -v` toosee hello version installed.</span></span>
3. <span data-ttu-id="7a506-124">Проверьте установку Gem hello, выполнив команду hello `gem -v` установленной версии toosee hello.</span><span class="sxs-lookup"><span data-stu-id="7a506-124">Test hello Gem installation by running hello command `gem -v` toosee hello version installed.</span></span>
4. <span data-ttu-id="7a506-125">Построить hello Mysql2 модуль для Ruby, с помощью Gem, выполнив команду hello `gem install mysql2`.</span><span class="sxs-lookup"><span data-stu-id="7a506-125">Build hello Mysql2 module for Ruby using Gem by running hello command `gem install mysql2`.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="7a506-126">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="7a506-126">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="7a506-127">Установите Ruby, выполнив команду hello `sudo apt-get install ruby-full`.</span><span class="sxs-lookup"><span data-stu-id="7a506-127">Install Ruby by running hello command `sudo apt-get install ruby-full`.</span></span> <span data-ttu-id="7a506-128">Дополнительные параметры установки см. в разделе hello Ruby [документацию по установке](https://www.ruby-lang.org/en/documentation/installation/).</span><span class="sxs-lookup"><span data-stu-id="7a506-128">For more installation options, see hello Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/).</span></span>
2. <span data-ttu-id="7a506-129">Тест hello Ruby установки, выполнив команду hello `ruby -v` установленной версии toosee hello.</span><span class="sxs-lookup"><span data-stu-id="7a506-129">Test hello Ruby installation by running hello command `ruby -v` toosee hello version installed.</span></span>
3. <span data-ttu-id="7a506-130">Установите последние обновления hello для Gem, выполнив команду hello `sudo gem update --system`.</span><span class="sxs-lookup"><span data-stu-id="7a506-130">Install hello latest updates for Gem by running hello command `sudo gem update --system`.</span></span>
4. <span data-ttu-id="7a506-131">Проверьте установку Gem hello, выполнив команду hello `gem -v` установленной версии toosee hello.</span><span class="sxs-lookup"><span data-stu-id="7a506-131">Test hello Gem installation by running hello command `gem -v` toosee hello version installed.</span></span>
5. <span data-ttu-id="7a506-132">Установите hello gcc, того же типа и других средств построения, выполнив команду hello `sudo apt-get install build-essential`.</span><span class="sxs-lookup"><span data-stu-id="7a506-132">Install hello gcc, make, and other build tools by running hello command `sudo apt-get install build-essential`.</span></span>
6. <span data-ttu-id="7a506-133">Установите клиентские библиотеки developer Привет MySQL, выполнив команду hello `sudo apt-get install libmysqlclient-dev`.</span><span class="sxs-lookup"><span data-stu-id="7a506-133">Install hello MySQL client developer libraries by running hello command `sudo apt-get install libmysqlclient-dev`.</span></span>
7. <span data-ttu-id="7a506-134">Построить hello mysql2 модуль для Ruby, с помощью Gem, выполнив команду hello `sudo gem install mysql2`.</span><span class="sxs-lookup"><span data-stu-id="7a506-134">Build hello mysql2 module for Ruby using Gem by running hello command `sudo gem install mysql2`.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="7a506-135">Получение сведений о подключении</span><span class="sxs-lookup"><span data-stu-id="7a506-135">Get connection information</span></span>
<span data-ttu-id="7a506-136">Получите toohello tooconnect базы данных Azure для hello подключения сведения, необходимые для MySQL.</span><span class="sxs-lookup"><span data-stu-id="7a506-136">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="7a506-137">Необходимо hello server полное имя и учетные данные входа.</span><span class="sxs-lookup"><span data-stu-id="7a506-137">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="7a506-138">Войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="7a506-138">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="7a506-139">Hello левого меню на портале Azure, щелкните **все ресурсы** и выполните поиск сервера hello, можно creased, такие как **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="7a506-139">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have creased, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="7a506-140">Щелкните имя сервера hello **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="7a506-140">Click hello server name **myserver4demo**.</span></span>
4. <span data-ttu-id="7a506-141">Выберите hello server **свойства** страницы.</span><span class="sxs-lookup"><span data-stu-id="7a506-141">Select hello server's **Properties** page.</span></span> <span data-ttu-id="7a506-142">Запишите hello **имя сервера** и **имя входа администратора сервера**.</span><span class="sxs-lookup"><span data-stu-id="7a506-142">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="7a506-143">![Имя входа для администратора сервера в базе данных Azure для MySQL](./media/connect-ruby/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="7a506-143">![Azure Database for MySQL - Server Admin Login](./media/connect-ruby/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="7a506-144">Если вы забыли учетные данные входа сервера, перейдите toohello **Обзор** страница hello tooview: имя пользователя администратора сервера и, при необходимости переустановить пароль hello.</span><span class="sxs-lookup"><span data-stu-id="7a506-144">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="run-ruby-code"></a><span data-ttu-id="7a506-145">Выполнение кода Ruby</span><span class="sxs-lookup"><span data-stu-id="7a506-145">Run Ruby code</span></span> 
1. <span data-ttu-id="7a506-146">Вставьте hello Ruby кода из разделов hello ниже в текстовых файлов и сохранения файлов hello в проект папку с .rb расширение файла, например `C:\rubymysql\createtable.rb` или `/home/username/rubymysql/createtable.rb`.</span><span class="sxs-lookup"><span data-stu-id="7a506-146">Paste hello Ruby code from hello sections below into text files, and save hello files into a project folder with file extension .rb, such as `C:\rubymysql\createtable.rb` or `/home/username/rubymysql/createtable.rb`.</span></span>
2. <span data-ttu-id="7a506-147">toorun hello кода, запустите командную строку hello или bash оболочки.</span><span class="sxs-lookup"><span data-stu-id="7a506-147">toorun hello code, launch hello command prompt or bash shell.</span></span> <span data-ttu-id="7a506-148">Перейдите в папку проекта `cd rubymysql`.</span><span class="sxs-lookup"><span data-stu-id="7a506-148">Change directory into your project folder `cd rubymysql`</span></span>
3. <span data-ttu-id="7a506-149">Затем введите команду hello ruby следуют hello имя файла, например `ruby createtable.rb` toorun приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7a506-149">Then type hello ruby command followed by hello file name, such as `ruby createtable.rb` toorun hello application.</span></span>
4. <span data-ttu-id="7a506-150">На hello ОС Windows Если приложение hello ruby не находится в переменную среды path так, может потребоваться toouse hello полный путь toolaunch hello узел приложения, такие как`"c:\Ruby23-x64\bin\ruby.exe" createtable.rb`</span><span class="sxs-lookup"><span data-stu-id="7a506-150">On hello Windows OS, if hello ruby application is not in your path environment variable, you may need toouse hello full path toolaunch hello node application, such as `"c:\Ruby23-x64\bin\ruby.exe" createtable.rb`</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="7a506-151">Подключение и создание таблицы</span><span class="sxs-lookup"><span data-stu-id="7a506-151">Connect and create a table</span></span>
<span data-ttu-id="7a506-152">Используйте следующие hello кода tooconnect и создание таблицы с помощью **CREATE TABLE** инструкции SQL, за которым следует **INSERT INTO** строк tooadd инструкций SQL в таблицу hello.</span><span class="sxs-lookup"><span data-stu-id="7a506-152">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements tooadd rows into hello table.</span></span>

<span data-ttu-id="7a506-153">использует код Hello [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) класса .new() метод tooconnect tooAzure базы данных для MySQL.</span><span class="sxs-lookup"><span data-stu-id="7a506-153">hello code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method tooconnect tooAzure Database for MySQL.</span></span> <span data-ttu-id="7a506-154">Затем он вызывает метод [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) несколько раз toorun hello, CREATE TABLE, команд DROP и INSERT INTO.</span><span class="sxs-lookup"><span data-stu-id="7a506-154">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) several times toorun hello DROP, CREATE TABLE, and INSERT INTO commands.</span></span> <span data-ttu-id="7a506-155">Затем он вызывает метод [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello соединения перед завершением работы.</span><span class="sxs-lookup"><span data-stu-id="7a506-155">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="7a506-156">Замените hello `host`, `database`, `username`, и `password` строки собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="7a506-156">Replace hello `host`, `database`, `username`, and `password` strings with your own values.</span></span> 
```ruby
require 'mysql2'

begin
    # Initialize connection variables.
    host = String('myserver4demo.mysql.database.azure.com')
    database = String('quickstartdb')
    username = String('myadmin@myserver4demo')
    password = String('yourpassword')

    # Initialize connection object.
    client = Mysql2::Client.new(:host => host, :username => username, :database => database, :password => password)
    puts 'Successfully created connection toodatabase.'

    # Drop previous table of same name if one exists
    client.query('DROP TABLE IF EXISTS inventory;')
    puts 'Finished dropping table (if existed).'

    # Drop previous table of same name if one exists.
    client.query('CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);')
    puts 'Finished creating table.'

    # Insert some data into table.
    client.query("INSERT INTO inventory VALUES(1, 'banana', 150)")
    client.query("INSERT INTO inventory VALUES(2, 'orange', 154)")
    client.query("INSERT INTO inventory VALUES(3, 'apple', 100)")
    puts 'Inserted 3 rows of data.'

# Error handling
rescue Exception => e
    puts e.message

# Cleanup
ensure
    client.close if client
    puts 'Done.'
end
```

## <a name="read-data"></a><span data-ttu-id="7a506-157">Считывание данных</span><span class="sxs-lookup"><span data-stu-id="7a506-157">Read data</span></span>
<span data-ttu-id="7a506-158">Используйте следующие hello кода tooconnect и чтения данных с помощью hello **ВЫБЕРИТЕ** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="7a506-158">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="7a506-159">использует код Hello [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) класса .new() метод tooconnect tooAzure базы данных для MySQL.</span><span class="sxs-lookup"><span data-stu-id="7a506-159">hello code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method tooconnect tooAzure Database for MySQL.</span></span> <span data-ttu-id="7a506-160">Затем он вызывает метод [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) команд SELECT toorun hello.</span><span class="sxs-lookup"><span data-stu-id="7a506-160">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello SELECT commands.</span></span> <span data-ttu-id="7a506-161">Затем он вызывает метод [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello соединения перед завершением работы.</span><span class="sxs-lookup"><span data-stu-id="7a506-161">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="7a506-162">Замените hello `host`, `database`, `username`, и `password` строки собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="7a506-162">Replace hello `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

```ruby
require 'mysql2'

begin
    # Initialize connection variables.
    host = String('myserver4demo.mysql.database.azure.com')
    database = String('quickstartdb')
    username = String('myadmin@myserver4demo')
    password = String('yourpassword')

    # Initialize connection object.
    client = Mysql2::Client.new(:host => host, :username => username, :database => database, :password => password)
    puts 'Successfully created connection toodatabase.'

    # Read data
    resultSet = client.query('SELECT * from inventory;')
    resultSet.each do |row|
        puts 'Data row = (%s, %s, %s)' % [row['id'], row['name'], row['quantity']]
    end
    puts 'Read ' + resultSet.count.to_s + ' row(s).'

# Error handling
rescue Exception => e
    puts e.message

# Cleanup
ensure
    client.close if client
    puts 'Done.'
end
```

## <a name="update-data"></a><span data-ttu-id="7a506-163">Обновление данных</span><span class="sxs-lookup"><span data-stu-id="7a506-163">Update data</span></span>
<span data-ttu-id="7a506-164">Используйте следующие hello кода tooconnect и обновления данных с помощью hello **обновление** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="7a506-164">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="7a506-165">использует код Hello [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) класса .new() метод tooconnect tooAzure базы данных для MySQL.</span><span class="sxs-lookup"><span data-stu-id="7a506-165">hello code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method tooconnect tooAzure Database for MySQL.</span></span> <span data-ttu-id="7a506-166">Затем он вызывает метод [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) команд UPDATE toorun hello.</span><span class="sxs-lookup"><span data-stu-id="7a506-166">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello UPDATE commands.</span></span> <span data-ttu-id="7a506-167">Затем он вызывает метод [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello соединения перед завершением работы.</span><span class="sxs-lookup"><span data-stu-id="7a506-167">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="7a506-168">Замените hello `host`, `database`, `username`, и `password` строки собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="7a506-168">Replace hello `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

```ruby
require 'mysql2'

begin
    # Initialize connection variables.
    host = String('myserver4demo.mysql.database.azure.com')
    database = String('quickstartdb')
    username = String('myadmin@myserver4demo')
    password = String('yourpassword')

    # Initialize connection object.
    client = Mysql2::Client.new(:host => host, :username => username, :database => database, :password => password)
    puts 'Successfully created connection toodatabase.'

    # Update data
   client.query('UPDATE inventory SET quantity = %d WHERE name = %s;' % [200, '\'banana\''])
   puts 'Updated 1 row of data.'

# Error handling
rescue Exception => e
    puts e.message

# Cleanup
ensure
    client.close if client
    puts 'Done.'
end
```


## <a name="delete-data"></a><span data-ttu-id="7a506-169">Удаление данных</span><span class="sxs-lookup"><span data-stu-id="7a506-169">Delete data</span></span>
<span data-ttu-id="7a506-170">Используйте следующие hello кода tooconnect и чтения данных с помощью hello **удалить** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="7a506-170">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="7a506-171">использует код Hello [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) класса .new() метод tooconnect tooAzure базы данных для MySQL.</span><span class="sxs-lookup"><span data-stu-id="7a506-171">hello code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method tooconnect tooAzure Database for MySQL.</span></span> <span data-ttu-id="7a506-172">Затем он вызывает метод [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) команд DELETE toorun hello.</span><span class="sxs-lookup"><span data-stu-id="7a506-172">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello DELETE commands.</span></span> <span data-ttu-id="7a506-173">Затем он вызывает метод [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello соединения перед завершением работы.</span><span class="sxs-lookup"><span data-stu-id="7a506-173">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="7a506-174">Замените hello `host`, `database`, `username`, и `password` строки собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="7a506-174">Replace hello `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

```ruby
require 'mysql2'

begin
    # Initialize connection variables.
    host = String('myserver4demo.mysql.database.azure.com')
    database = String('quickstartdb')
    username = String('myadmin@myserver4demo')
    password = String('yourpassword')

    # Initialize connection object.
    client = Mysql2::Client.new(:host => host, :username => username, :database => database, :password => password)
    puts 'Successfully created connection toodatabase.'

    # Delete data
    resultSet = client.query('DELETE FROM inventory WHERE name = %s;' % ['\'orange\''])
    puts 'Deleted 1 row.'

# Error handling
rescue Exception => e
    puts e.message

# Cleanup
ensure
    client.close if client
    puts 'Done.'
end
```

## <a name="next-steps"></a><span data-ttu-id="7a506-175">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7a506-175">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="7a506-176">Перенос базы данных с помощью экспорта и импорта</span><span class="sxs-lookup"><span data-stu-id="7a506-176">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
