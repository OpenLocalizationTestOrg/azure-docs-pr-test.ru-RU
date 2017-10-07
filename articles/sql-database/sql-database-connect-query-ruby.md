---
title: "aaaUse Ruby tooquery базы данных SQL Azure | Документы Microsoft"
description: "В этом разделе показано, как toouse Ruby toocreate программу, которая соединяет tooan базы данных SQL Azure и запросов с помощью инструкций Transact-SQL."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 94fec528-58ba-4352-ba0d-25ae4b273e90
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: hero-article
ms.date: 07/14/2017
ms.author: carlrab
ms.openlocfilehash: 0d4b16b8aacb5e376ab80cbe37569130f2fd52b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-ruby-tooquery-an-azure-sql-database"></a>Используйте Ruby tooquery базы данных Azure SQL

В этом учебнике быстрого запуска показано как toouse [Ruby](https://www.ruby-lang.org) toocreate tooan tooconnect программы Azure SQL базы данных и использовать данные tooquery инструкций Transact-SQL.

## <a name="prerequisites"></a>Предварительные требования

toocomplete этом краткое руководство по началу работы, убедитесь, что у вас есть hello следующие предварительные требования:

- База данных SQL Azure. В этом кратком руководстве использует ресурсы hello, созданные в одном из этих краткие руководства: 

   - [Создание базы данных с помощью портала](sql-database-get-started-portal.md)
   - [Создание базы данных SQL Azure и отправка к ней запросов с помощью Azure CLI](sql-database-get-started-cli.md)
   - [Создание базы данных с помощью PowerShell](sql-database-get-started-powershell.md)

- Объект [правила брандмауэра уровня сервера](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) для hello общедоступный IP-адрес компьютера hello, используйте для этого краткого руководства.
- Убедитесь, что установлен Ruby и связанное программное обеспечение для вашей операционной системы.
    - **MacOS**: установите Homebrew, rbenv и ruby-build, Ruby и FreeTDS. Ознакомьтесь с шагами 1.2, 1.3, 1.4 и 1.5 в [этом руководстве](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/).
    - **Ubuntu**: установите необходимые компоненты для Ruby, rbenv и ruby-build, Ruby и FreeTDS. Ознакомьтесь с шагами 1.2, 1.3, 1.4 и 1.5 в [этом руководстве](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu/).

## <a name="sql-server-connection-information"></a>Сведения о подключении SQL Server

Получите базу данных Azure SQL toohello tooconnect в сведения, необходимые подключения hello. Необходимо будет hello полное имя сервера, имя базы данных и сведения об имени входа в следующих процедурах hello.

1. Войдите в toohello [портал Azure](https://portal.azure.com/).
2. Выберите **баз данных SQL** hello левом меню и выберите базу данных на hello **баз данных SQL** страницы. 
3. На hello **Обзор** страниц для базы данных, просмотрите hello полное имя сервера. Можно навести на toobring имя сервера hello копирование hello **щелкните toocopy** параметра, как показано в hello после изображения:

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. Если вы забыли hello учетные данные для сервера базы данных SQL Azure, перейдите toohello базы данных SQL server страницы tooview hello server с именем admin и, при необходимости сбросить пароль hello.

> [!IMPORTANT]
> Необходимо иметь правила брандмауэра на месте для hello общедоступный IP-адрес hello компьютера, на котором выполняется этот учебник. Если вы на другом компьютере или другой общий IP-адрес, создайте [правило брандмауэра уровня сервера с помощью портала Azure "hello"](sql-database-get-started-portal.md#create-a-server-level-firewall-rule). 

## <a name="insert-code-tooquery-sql-database"></a>Вставьте код базы данных SQL tooquery

1. Создайте файл **sqltest.rb** в избранном текстовом редакторе.

2. Замените содержимое hello hello ниже программный код и добавить hello соответствующие значения для сервера, базы данных, пользователя и пароль.

```ruby
require 'tiny_tds'
server = 'your_server.database.windows.net'
database = 'your_database'
username = 'your_username'
password = 'your_password'
client = TinyTds::Client.new username: username, password: password, 
    host: server, port: 1433, database: database, azure: true

puts "Reading data from table"
tsql = "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
        FROM [SalesLT].[ProductCategory] pc
        JOIN [SalesLT].[Product] p
        ON pc.productcategoryid = p.productcategoryid"
result = client.execute(tsql)
result.each do |row|
    puts row
end
```

## <a name="run-hello-code"></a>Выполнение кода hello

1. Hello командной строки выполните следующие команды hello.

   ```bash
   ruby sqltest.rb
   ```

2. Убедитесь, что возвращаются первые 20 строк hello и закройте окно приложения hello.


## <a name="next-steps"></a>Дальнейшие действия
- [Проектирование первой базы данных SQL Azure](sql-database-design-first-database.md)
- [Просмотрите репозиторий GitHub для TinyTDS](https://github.com/rails-sqlserver/tiny_tds).
- [Сообщите о проблемах или задайте вопросы по TinyTDS](https://github.com/rails-sqlserver/tiny_tds/issues)
- [Ruby Drivers for SQL Server](https://docs.microsoft.com/sql/connect/ruby/ruby-driver-for-sql-server/) (Драйверы Ruby для SQL Server).
