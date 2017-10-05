---
title: "Подключение к базе данных Azure для MySQL с помощью Ruby | Документация Майкрософт"
description: "В этом кратком руководстве представлены примеры кода Ruby, которые можно использовать для подключения к базе данных Azure для MySQL и запроса данных из нее."
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
ms.openlocfilehash: e54f1dccbae060c52f48bfeb277c045b99a91715
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/29/2017
---
# <a name="azure-database-for-mysql-use-ruby-to-connect-and-query-data"></a><span data-ttu-id="efea9-103">База данных Azure для MySQL: подключение и запрос данных с помощью Ruby</span><span class="sxs-lookup"><span data-stu-id="efea9-103">Azure Database for MySQL: Use Ruby to connect and query data</span></span>
<span data-ttu-id="efea9-104">В этом кратком руководстве объясняется, как подключиться к базе данных Azure для MySQL с помощью приложения [Ruby](https://www.ruby-lang.org) и пакета [Mysql2](https://rubygems.org/gems/mysql2) на платформе Windows, Ubuntu Linux и Mac.</span><span class="sxs-lookup"><span data-stu-id="efea9-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using a [Ruby](https://www.ruby-lang.org) application and the [mysql2](https://rubygems.org/gems/mysql2) gem from Windows, Ubuntu Linux, and Mac platforms.</span></span> <span data-ttu-id="efea9-105">Здесь также показано, как использовать инструкции SQL для запроса, вставки, обновления и удаления данных в базе данных.</span><span class="sxs-lookup"><span data-stu-id="efea9-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="efea9-106">В этой статье предполагается, что у вас уже есть опыт разработки на Ruby, но вы только начали работу с базой данных Azure для MySQL.</span><span class="sxs-lookup"><span data-stu-id="efea9-106">This article assumes you are familiar with development using Ruby, but that you are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="efea9-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="efea9-107">Prerequisites</span></span>
<span data-ttu-id="efea9-108">В качестве отправной точки в этом кратком руководстве используются ресурсы, созданные в соответствии со следующими материалами:</span><span class="sxs-lookup"><span data-stu-id="efea9-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- <span data-ttu-id="efea9-109">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Создание сервера базы данных Azure для MySQL с помощью портала Azure)</span><span class="sxs-lookup"><span data-stu-id="efea9-109">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md)</span></span>
- <span data-ttu-id="efea9-110">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md) (Создание базы данных Azure для сервера MySQL с помощью Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="efea9-110">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md)</span></span>

## <a name="install-ruby"></a><span data-ttu-id="efea9-111">Установка Ruby</span><span class="sxs-lookup"><span data-stu-id="efea9-111">Install Ruby</span></span>
<span data-ttu-id="efea9-112">Установите Ruby, Gem и библиотеку MySQL2 на своем компьютере.</span><span class="sxs-lookup"><span data-stu-id="efea9-112">Install Ruby, Gem, and the MySQL2 library on your own machine.</span></span> 

### <a name="windows"></a><span data-ttu-id="efea9-113">Windows</span><span class="sxs-lookup"><span data-stu-id="efea9-113">Windows</span></span>
1. <span data-ttu-id="efea9-114">Скачайте и установите [Ruby](http://rubyinstaller.org/downloads/) версии 2.3.</span><span class="sxs-lookup"><span data-stu-id="efea9-114">Download and Install the 2.3 version of [Ruby](http://rubyinstaller.org/downloads/).</span></span>
2. <span data-ttu-id="efea9-115">Запустите новую командную строку (cmd) из меню "Пуск".</span><span class="sxs-lookup"><span data-stu-id="efea9-115">Launch a new command prompt (cmd) from the Start menu.</span></span>
3. <span data-ttu-id="efea9-116">Перейдите в каталог Ruby версии 2.3.</span><span class="sxs-lookup"><span data-stu-id="efea9-116">Change directory into the Ruby directory for version 2.3.</span></span> `cd c:\Ruby23-x64\bin`
4. <span data-ttu-id="efea9-117">Выполните команду `ruby -v`, чтобы узнать установленную версию Ruby.</span><span class="sxs-lookup"><span data-stu-id="efea9-117">Test the Ruby installation by running the command `ruby -v` to see the version installed.</span></span>
5. <span data-ttu-id="efea9-118">Выполните команду `gem -v`, чтобы узнать установленную версию Gem.</span><span class="sxs-lookup"><span data-stu-id="efea9-118">Test the Gem installation by running the command `gem -v` to see the version installed.</span></span>
6. <span data-ttu-id="efea9-119">Создайте модуль Mysql2 для Ruby с помощью Gem, выполнив команду `gem install mysql2`.</span><span class="sxs-lookup"><span data-stu-id="efea9-119">Build the Mysql2 module for Ruby using Gem by running the command `gem install mysql2`.</span></span>

### <a name="macos"></a><span data-ttu-id="efea9-120">MacOS</span><span class="sxs-lookup"><span data-stu-id="efea9-120">MacOS</span></span>
1. <span data-ttu-id="efea9-121">Установите Ruby с помощью Homebrew, выполнив команду `brew install ruby`.</span><span class="sxs-lookup"><span data-stu-id="efea9-121">Install Ruby using Homebrew by running the command `brew install ruby`.</span></span> <span data-ttu-id="efea9-122">Дополнительные параметры установки см. в [документации по установке](https://www.ruby-lang.org/en/documentation/installation/#homebrew) Ruby.</span><span class="sxs-lookup"><span data-stu-id="efea9-122">For more installation options, see the Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/#homebrew).</span></span>
2. <span data-ttu-id="efea9-123">Выполните команду `ruby -v`, чтобы узнать установленную версию Ruby.</span><span class="sxs-lookup"><span data-stu-id="efea9-123">Test the Ruby installation by running the command `ruby -v` to see the version installed.</span></span>
3. <span data-ttu-id="efea9-124">Выполните команду `gem -v`, чтобы узнать установленную версию Gem.</span><span class="sxs-lookup"><span data-stu-id="efea9-124">Test the Gem installation by running the command `gem -v` to see the version installed.</span></span>
4. <span data-ttu-id="efea9-125">Создайте модуль Mysql2 для Ruby с помощью Gem, выполнив команду `gem install mysql2`.</span><span class="sxs-lookup"><span data-stu-id="efea9-125">Build the Mysql2 module for Ruby using Gem by running the command `gem install mysql2`.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="efea9-126">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="efea9-126">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="efea9-127">Установите Ruby, выполнив команду `sudo apt-get install ruby-full`.</span><span class="sxs-lookup"><span data-stu-id="efea9-127">Install Ruby by running the command `sudo apt-get install ruby-full`.</span></span> <span data-ttu-id="efea9-128">Дополнительные параметры установки см. в [документации по установке](https://www.ruby-lang.org/en/documentation/installation/) Ruby.</span><span class="sxs-lookup"><span data-stu-id="efea9-128">For more installation options, see the Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/).</span></span>
2. <span data-ttu-id="efea9-129">Выполните команду `ruby -v`, чтобы узнать установленную версию Ruby.</span><span class="sxs-lookup"><span data-stu-id="efea9-129">Test the Ruby installation by running the command `ruby -v` to see the version installed.</span></span>
3. <span data-ttu-id="efea9-130">Установите последние обновления для Gem, выполнив команду `sudo gem update --system`.</span><span class="sxs-lookup"><span data-stu-id="efea9-130">Install the latest updates for Gem by running the command `sudo gem update --system`.</span></span>
4. <span data-ttu-id="efea9-131">Выполните команду `gem -v`, чтобы узнать установленную версию Gem.</span><span class="sxs-lookup"><span data-stu-id="efea9-131">Test the Gem installation by running the command `gem -v` to see the version installed.</span></span>
5. <span data-ttu-id="efea9-132">Установите gcc, make и другие инструменты сборки, выполнив команду `sudo apt-get install build-essential`.</span><span class="sxs-lookup"><span data-stu-id="efea9-132">Install the gcc, make, and other build tools by running the command `sudo apt-get install build-essential`.</span></span>
6. <span data-ttu-id="efea9-133">Установите библиотеки разработчика клиента MySQL, выполнив команду `sudo apt-get install libmysqlclient-dev`.</span><span class="sxs-lookup"><span data-stu-id="efea9-133">Install the MySQL client developer libraries by running the command `sudo apt-get install libmysqlclient-dev`.</span></span>
7. <span data-ttu-id="efea9-134">Создайте модуль Mysql2 для Ruby с помощью Gem, выполнив команду `sudo gem install mysql2`.</span><span class="sxs-lookup"><span data-stu-id="efea9-134">Build the mysql2 module for Ruby using Gem by running the command `sudo gem install mysql2`.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="efea9-135">Получение сведений о подключении</span><span class="sxs-lookup"><span data-stu-id="efea9-135">Get connection information</span></span>
<span data-ttu-id="efea9-136">Получите сведения о подключении, необходимые для подключения к базе данных Azure.для MySQL.</span><span class="sxs-lookup"><span data-stu-id="efea9-136">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="efea9-137">Вам потребуется полное имя сервера и учетные данные для входа.</span><span class="sxs-lookup"><span data-stu-id="efea9-137">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="efea9-138">Войдите на [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="efea9-138">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="efea9-139">В меню слева на портале Azure щелкните **Все ресурсы** и выполните поиск по имени созданного сервера, например **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="efea9-139">From the left-hand menu in Azure portal, click **All resources** and search for the server you have creased, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="efea9-140">Щелкните имя сервера **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="efea9-140">Click the server name **myserver4demo**.</span></span>
4. <span data-ttu-id="efea9-141">Откройте страницу **свойств** сервера.</span><span class="sxs-lookup"><span data-stu-id="efea9-141">Select the server's **Properties** page.</span></span> <span data-ttu-id="efea9-142">Запишите значения **имени сервера** и **имени для входа администратора сервера**.</span><span class="sxs-lookup"><span data-stu-id="efea9-142">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="efea9-143">![Имя входа для администратора сервера в базе данных Azure для MySQL](./media/connect-ruby/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="efea9-143">![Azure Database for MySQL - Server Admin Login](./media/connect-ruby/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="efea9-144">Если вы забыли данные для входа на сервер, перейдите на страницу **Обзор**, чтобы просмотреть имя администратора сервера и при необходимости сбросить пароль.</span><span class="sxs-lookup"><span data-stu-id="efea9-144">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="run-ruby-code"></a><span data-ttu-id="efea9-145">Выполнение кода Ruby</span><span class="sxs-lookup"><span data-stu-id="efea9-145">Run Ruby code</span></span> 
1. <span data-ttu-id="efea9-146">Вставьте код Ruby из раздела ниже в текстовые файлы и сохраните файлы в папке проекта с расширением файла .rb, например `C:\rubymysql\createtable.rb` или `/home/username/rubymysql/createtable.rb`.</span><span class="sxs-lookup"><span data-stu-id="efea9-146">Paste the Ruby code from the sections below into text files, and save the files into a project folder with file extension .rb, such as `C:\rubymysql\createtable.rb` or `/home/username/rubymysql/createtable.rb`.</span></span>
2. <span data-ttu-id="efea9-147">Чтобы выполнить код, запустите командную строку или оболочку Bash.</span><span class="sxs-lookup"><span data-stu-id="efea9-147">To run the code, launch the command prompt or bash shell.</span></span> <span data-ttu-id="efea9-148">Перейдите в папку проекта `cd rubymysql`.</span><span class="sxs-lookup"><span data-stu-id="efea9-148">Change directory into your project folder `cd rubymysql`</span></span>
3. <span data-ttu-id="efea9-149">Введите команду Ruby, за которой следует имя файла, например `ruby createtable.rb`, чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="efea9-149">Then type the ruby command followed by the file name, such as `ruby createtable.rb` to run the application.</span></span>
4. <span data-ttu-id="efea9-150">В операционной системе Windows, если приложение Ruby не указано в переменной среды PATH, может потребоваться указать полный путь, чтобы запустить приложение Node, например `"c:\Ruby23-x64\bin\ruby.exe" createtable.rb`</span><span class="sxs-lookup"><span data-stu-id="efea9-150">On the Windows OS, if the ruby application is not in your path environment variable, you may need to use the full path to launch the node application, such as `"c:\Ruby23-x64\bin\ruby.exe" createtable.rb`</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="efea9-151">Подключение и создание таблицы</span><span class="sxs-lookup"><span data-stu-id="efea9-151">Connect and create a table</span></span>
<span data-ttu-id="efea9-152">Используйте приведенный ниже код для подключения и создайте таблицу с помощью инструкции SQL **CREATE TABLE**. Добавьте строки в таблицу, применив инструкцию SQL **INSERT INTO**.</span><span class="sxs-lookup"><span data-stu-id="efea9-152">Use the following code to connect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements to add rows into the table.</span></span>

<span data-ttu-id="efea9-153">Код использует класс [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) и метод .new(), чтобы подключиться к базе данных Azure для MySQL.</span><span class="sxs-lookup"><span data-stu-id="efea9-153">The code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method to connect to Azure Database for MySQL.</span></span> <span data-ttu-id="efea9-154">Затем он вызывает метод [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) несколько раз для выполнения команд DROP, CREATE TABLE и INSERT INTO.</span><span class="sxs-lookup"><span data-stu-id="efea9-154">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) several times to run the DROP, CREATE TABLE, and INSERT INTO commands.</span></span> <span data-ttu-id="efea9-155">После этого вызывается метод [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method), чтобы разорвать подключение перед завершением работы.</span><span class="sxs-lookup"><span data-stu-id="efea9-155">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="efea9-156">Замените строки `host`, `database`, `username` и `password` собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="efea9-156">Replace the `host`, `database`, `username`, and `password` strings with your own values.</span></span> 
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
    puts 'Successfully created connection to database.'

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

## <a name="read-data"></a><span data-ttu-id="efea9-157">Считывание данных</span><span class="sxs-lookup"><span data-stu-id="efea9-157">Read data</span></span>
<span data-ttu-id="efea9-158">Используйте указанный ниже код с инструкцией SQL **SELECT** для подключения и чтения данных.</span><span class="sxs-lookup"><span data-stu-id="efea9-158">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="efea9-159">Код использует класс [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) и метод .new(), чтобы подключиться к базе данных Azure для MySQL.</span><span class="sxs-lookup"><span data-stu-id="efea9-159">The code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method to connect to Azure Database for MySQL.</span></span> <span data-ttu-id="efea9-160">Затем он вызывает метод [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) для выполнения команды SELECT.</span><span class="sxs-lookup"><span data-stu-id="efea9-160">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) to run the SELECT commands.</span></span> <span data-ttu-id="efea9-161">После этого вызывается метод [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method), чтобы разорвать подключение перед завершением работы.</span><span class="sxs-lookup"><span data-stu-id="efea9-161">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="efea9-162">Замените строки `host`, `database`, `username` и `password` собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="efea9-162">Replace the `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

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
    puts 'Successfully created connection to database.'

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

## <a name="update-data"></a><span data-ttu-id="efea9-163">Обновление данных</span><span class="sxs-lookup"><span data-stu-id="efea9-163">Update data</span></span>
<span data-ttu-id="efea9-164">Используйте указанный ниже код с инструкцией SQL **UPDATE** для подключения и обновления данных.</span><span class="sxs-lookup"><span data-stu-id="efea9-164">Use the following code to connect and update the data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="efea9-165">Код использует класс [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) и метод .new(), чтобы подключиться к базе данных Azure для MySQL.</span><span class="sxs-lookup"><span data-stu-id="efea9-165">The code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method to connect to Azure Database for MySQL.</span></span> <span data-ttu-id="efea9-166">Затем он вызывает метод [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) для выполнения команды UPDATE.</span><span class="sxs-lookup"><span data-stu-id="efea9-166">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) to run the UPDATE commands.</span></span> <span data-ttu-id="efea9-167">После этого вызывается метод [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method), чтобы разорвать подключение перед завершением работы.</span><span class="sxs-lookup"><span data-stu-id="efea9-167">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="efea9-168">Замените строки `host`, `database`, `username` и `password` собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="efea9-168">Replace the `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

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
    puts 'Successfully created connection to database.'

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


## <a name="delete-data"></a><span data-ttu-id="efea9-169">Удаление данных</span><span class="sxs-lookup"><span data-stu-id="efea9-169">Delete data</span></span>
<span data-ttu-id="efea9-170">Используйте указанный ниже код с инструкцией SQL **DELETE** для подключения и чтения данных.</span><span class="sxs-lookup"><span data-stu-id="efea9-170">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="efea9-171">Код использует класс [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) и метод .new(), чтобы подключиться к базе данных Azure для MySQL.</span><span class="sxs-lookup"><span data-stu-id="efea9-171">The code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method to connect to Azure Database for MySQL.</span></span> <span data-ttu-id="efea9-172">Затем он вызывает метод [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) для выполнения команды DELETE.</span><span class="sxs-lookup"><span data-stu-id="efea9-172">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) to run the DELETE commands.</span></span> <span data-ttu-id="efea9-173">После этого вызывается метод [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method), чтобы разорвать подключение перед завершением работы.</span><span class="sxs-lookup"><span data-stu-id="efea9-173">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="efea9-174">Замените строки `host`, `database`, `username` и `password` собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="efea9-174">Replace the `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

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
    puts 'Successfully created connection to database.'

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

## <a name="next-steps"></a><span data-ttu-id="efea9-175">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="efea9-175">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="efea9-176">Перенос базы данных с помощью экспорта и импорта</span><span class="sxs-lookup"><span data-stu-id="efea9-176">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
