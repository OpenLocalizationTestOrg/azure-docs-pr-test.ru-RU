---
title: "Использование Ruby для создания запросов к базе данных SQL Azure | Документация Майкрософт"
description: "В этой статье показано, как использовать Ruby для создания программы, которая подключается к базе данных SQL Azure, и создавать к ней запросы с помощью инструкций Transact-SQL."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 94fec528-58ba-4352-ba0d-25ae4b273e90
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: Inactive
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: quickstart
ms.date: 07/15/2017
ms.author: carlrab
ms.openlocfilehash: 3427d216540451bc10b968f866d0fce0f6df3c54
ms.sourcegitcommit: 29bac59f1d62f38740b60274cb4912816ee775ea
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/29/2017
---
# <a name="use-ruby-to-query-an-azure-sql-database"></a>Использование Ruby для создания запросов к базе данных SQL Azure

В этом кратком руководстве показано, как использовать [Ruby](https://www.ruby-lang.org) для создания программы, которая подключается к базе данных SQL Azure, а затем с помощью инструкций Transact-SQL выполнить запрос данных.

## <a name="prerequisites"></a>Предварительные требования

Ниже указаны требования для работы с этим кратким руководством.

[!INCLUDE [prerequisites-create-db](../../includes/sql-database-connect-query-prerequisites-create-db-includes.md)]

- [Правило брандмауэра уровня сервера](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) для общедоступного IP-адреса компьютера, на котором выполняются действия из этого краткого руководства.

- Убедитесь, что установлен компонент Ruby и связанное программное обеспечение для вашей операционной системы.
    - **MacOS**: установите Homebrew, rbenv и ruby-build, Ruby и FreeTDS. Ознакомьтесь с шагами 1.2, 1.3, 1.4 и 1.5 в [этом руководстве](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/).
    - **Ubuntu**: установите необходимые компоненты для Ruby, rbenv и ruby-build, Ruby и FreeTDS. Ознакомьтесь с шагами 1.2, 1.3, 1.4 и 1.5 в [этом руководстве](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu/).

## <a name="sql-server-connection-information"></a>Сведения о подключении SQL Server

[!INCLUDE [prerequisites-server-connection-info](../../includes/sql-database-connect-query-prerequisites-server-connection-info-includes.md)]

> [!IMPORTANT]
> Необходимо настроить правила брандмауэра для общедоступного IP-адреса компьютера, на котором выполняются действия из этого руководства. Если вы используете другой компьютер или имеете другой общедоступный IP-адрес, создайте [правила брандмауэра на уровне сервера с помощью портала Azure](sql-database-get-started-portal.md#create-a-server-level-firewall-rule). 

## <a name="insert-code-to-query-sql-database"></a>Вставка кода для отправки запроса к базе данных SQL

1. Создайте файл **sqltest.rb** в избранном текстовом редакторе.

2. Замените содержимое следующим кодом и добавьте соответствующие значения для сервера, базы данных, пользователя и пароля.

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

## <a name="run-the-code"></a>Выполнение кода

1. В командной строке выполните следующие команды:

   ```bash
   ruby sqltest.rb
   ```

2. Убедитесь, что возвращены первые 20 строк, а затем закройте окно приложения.


## <a name="next-steps"></a>Дальнейшие действия
- [Проектирование первой базы данных SQL Azure](sql-database-design-first-database.md)
- [Просмотрите репозиторий GitHub для TinyTDS](https://github.com/rails-sqlserver/tiny_tds).
- [Сообщите о проблемах или задайте вопросы по TinyTDS](https://github.com/rails-sqlserver/tiny_tds/issues)
- [Ruby Drivers for SQL Server](https://docs.microsoft.com/sql/connect/ruby/ruby-driver-for-sql-server/) (Драйверы Ruby для SQL Server).
