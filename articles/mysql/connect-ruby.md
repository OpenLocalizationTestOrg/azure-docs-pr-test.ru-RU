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
# <a name="azure-database-for-mysql-use-ruby-tooconnect-and-query-data"></a>База данных Azure для MySQL: используйте Ruby tooconnect и запроса данных
Краткого руководства показано, как tooconnect tooan Azure этой базы данных MySQL с помощью [Ruby](https://www.ruby-lang.org) приложения и hello [mysql2](https://rubygems.org/gems/mysql2) gem из платформ Mac, Ubuntu Linux и Windows. Показано, как tooquery инструкций SQL toouse, вставка, обновление и удаление данных в базе данных hello. В этой статье предполагается, что вы знакомы с разработки, используя Ruby, но, чтобы новый tooworking с базой данных Azure для MySQL.

## <a name="prerequisites"></a>Предварительные требования
Это краткое руководство использует ресурсы hello, созданные в любой из этих руководствах по в качестве отправной точки.
- [Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Создание сервера базы данных Azure для MySQL с помощью портала Azure)
- [Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md) (Создание базы данных Azure для сервера MySQL с помощью Azure CLI)

## <a name="install-ruby"></a>Установка Ruby
Установите на компьютере Ruby, Gem и библиотека MySQL2 hello. 

### <a name="windows"></a>Windows
1. Загрузить и установить версию hello 2.3 [Ruby](http://rubyinstaller.org/downloads/).
2. Из меню "Пуск" hello, запустите новую командную строку (cmd).
3. Перейдите в каталог в hello Ruby каталог для версии 2.3. `cd c:\Ruby23-x64\bin`
4. Тест hello Ruby установки, выполнив команду hello `ruby -v` установленной версии toosee hello.
5. Проверьте установку Gem hello, выполнив команду hello `gem -v` установленной версии toosee hello.
6. Построить hello Mysql2 модуль для Ruby, с помощью Gem, выполнив команду hello `gem install mysql2`.

### <a name="macos"></a>MacOS
1. Установка с помощью Homebrew, выполнив команду hello Ruby `brew install ruby`. Дополнительные параметры установки см. в разделе hello Ruby [документацию по установке](https://www.ruby-lang.org/en/documentation/installation/#homebrew).
2. Тест hello Ruby установки, выполнив команду hello `ruby -v` установленной версии toosee hello.
3. Проверьте установку Gem hello, выполнив команду hello `gem -v` установленной версии toosee hello.
4. Построить hello Mysql2 модуль для Ruby, с помощью Gem, выполнив команду hello `gem install mysql2`.

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
1. Установите Ruby, выполнив команду hello `sudo apt-get install ruby-full`. Дополнительные параметры установки см. в разделе hello Ruby [документацию по установке](https://www.ruby-lang.org/en/documentation/installation/).
2. Тест hello Ruby установки, выполнив команду hello `ruby -v` установленной версии toosee hello.
3. Установите последние обновления hello для Gem, выполнив команду hello `sudo gem update --system`.
4. Проверьте установку Gem hello, выполнив команду hello `gem -v` установленной версии toosee hello.
5. Установите hello gcc, того же типа и других средств построения, выполнив команду hello `sudo apt-get install build-essential`.
6. Установите клиентские библиотеки developer Привет MySQL, выполнив команду hello `sudo apt-get install libmysqlclient-dev`.
7. Построить hello mysql2 модуль для Ruby, с помощью Gem, выполнив команду hello `sudo gem install mysql2`.

## <a name="get-connection-information"></a>Получение сведений о подключении
Получите toohello tooconnect базы данных Azure для hello подключения сведения, необходимые для MySQL. Необходимо hello server полное имя и учетные данные входа.

1. Войдите в toohello [портал Azure](https://portal.azure.com/).
2. Hello левого меню на портале Azure, щелкните **все ресурсы** и выполните поиск сервера hello, можно creased, такие как **myserver4demo**.
3. Щелкните имя сервера hello **myserver4demo**.
4. Выберите hello server **свойства** страницы. Запишите hello **имя сервера** и **имя входа администратора сервера**.
 ![Имя входа для администратора сервера в базе данных Azure для MySQL](./media/connect-ruby/1_server-properties-name-login.png)
5. Если вы забыли учетные данные входа сервера, перейдите toohello **Обзор** страница hello tooview: имя пользователя администратора сервера и, при необходимости переустановить пароль hello.

## <a name="run-ruby-code"></a>Выполнение кода Ruby 
1. Вставьте hello Ruby кода из разделов hello ниже в текстовых файлов и сохранения файлов hello в проект папку с .rb расширение файла, например `C:\rubymysql\createtable.rb` или `/home/username/rubymysql/createtable.rb`.
2. toorun hello кода, запустите командную строку hello или bash оболочки. Перейдите в папку проекта `cd rubymysql`.
3. Затем введите команду hello ruby следуют hello имя файла, например `ruby createtable.rb` toorun приложения hello.
4. На hello ОС Windows Если приложение hello ruby не находится в переменную среды path так, может потребоваться toouse hello полный путь toolaunch hello узел приложения, такие как`"c:\Ruby23-x64\bin\ruby.exe" createtable.rb`

## <a name="connect-and-create-a-table"></a>Подключение и создание таблицы
Используйте следующие hello кода tooconnect и создание таблицы с помощью **CREATE TABLE** инструкции SQL, за которым следует **INSERT INTO** строк tooadd инструкций SQL в таблицу hello.

использует код Hello [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) класса .new() метод tooconnect tooAzure базы данных для MySQL. Затем он вызывает метод [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) несколько раз toorun hello, CREATE TABLE, команд DROP и INSERT INTO. Затем он вызывает метод [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello соединения перед завершением работы.

Замените hello `host`, `database`, `username`, и `password` строки собственными значениями. 
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

## <a name="read-data"></a>Считывание данных
Используйте следующие hello кода tooconnect и чтения данных с помощью hello **ВЫБЕРИТЕ** инструкции SQL. 

использует код Hello [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) класса .new() метод tooconnect tooAzure базы данных для MySQL. Затем он вызывает метод [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) команд SELECT toorun hello. Затем он вызывает метод [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello соединения перед завершением работы.

Замените hello `host`, `database`, `username`, и `password` строки собственными значениями. 

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

## <a name="update-data"></a>Обновление данных
Используйте следующие hello кода tooconnect и обновления данных с помощью hello **обновление** инструкции SQL.

использует код Hello [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) класса .new() метод tooconnect tooAzure базы данных для MySQL. Затем он вызывает метод [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) команд UPDATE toorun hello. Затем он вызывает метод [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello соединения перед завершением работы.

Замените hello `host`, `database`, `username`, и `password` строки собственными значениями. 

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


## <a name="delete-data"></a>Удаление данных
Используйте следующие hello кода tooconnect и чтения данных с помощью hello **удалить** инструкции SQL. 

использует код Hello [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) класса .new() метод tooconnect tooAzure базы данных для MySQL. Затем он вызывает метод [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) команд DELETE toorun hello. Затем он вызывает метод [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello соединения перед завершением работы.

Замените hello `host`, `database`, `username`, и `password` строки собственными значениями. 

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

## <a name="next-steps"></a>Дальнейшие действия
> [!div class="nextstepaction"]
> [Перенос базы данных с помощью экспорта и импорта](./concepts-migrate-import-export.md)
