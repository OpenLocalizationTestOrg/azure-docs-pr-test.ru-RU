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
# <a name="use-ruby-tooquery-an-azure-sql-database"></a><span data-ttu-id="6f265-103">Используйте Ruby tooquery базы данных Azure SQL</span><span class="sxs-lookup"><span data-stu-id="6f265-103">Use Ruby tooquery an Azure SQL database</span></span>

<span data-ttu-id="6f265-104">В этом учебнике быстрого запуска показано как toouse [Ruby](https://www.ruby-lang.org) toocreate tooan tooconnect программы Azure SQL базы данных и использовать данные tooquery инструкций Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="6f265-104">This quick start tutorial demonstrates how toouse [Ruby](https://www.ruby-lang.org) toocreate a program tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6f265-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6f265-105">Prerequisites</span></span>

<span data-ttu-id="6f265-106">toocomplete этом краткое руководство по началу работы, убедитесь, что у вас есть hello следующие предварительные требования:</span><span class="sxs-lookup"><span data-stu-id="6f265-106">toocomplete this quick start tutorial, make sure you have hello following prerequisites:</span></span>

- <span data-ttu-id="6f265-107">База данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="6f265-107">An Azure SQL database.</span></span> <span data-ttu-id="6f265-108">В этом кратком руководстве использует ресурсы hello, созданные в одном из этих краткие руководства:</span><span class="sxs-lookup"><span data-stu-id="6f265-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="6f265-109">Создание базы данных с помощью портала</span><span class="sxs-lookup"><span data-stu-id="6f265-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="6f265-110">Создание базы данных SQL Azure и отправка к ней запросов с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="6f265-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="6f265-111">Создание базы данных с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="6f265-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="6f265-112">Объект [правила брандмауэра уровня сервера](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) для hello общедоступный IP-адрес компьютера hello, используйте для этого краткого руководства.</span><span class="sxs-lookup"><span data-stu-id="6f265-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="6f265-113">Убедитесь, что установлен Ruby и связанное программное обеспечение для вашей операционной системы.</span><span class="sxs-lookup"><span data-stu-id="6f265-113">You have installed Ruby and related software for your operating system.</span></span>
    - <span data-ttu-id="6f265-114">**MacOS**: установите Homebrew, rbenv и ruby-build, Ruby и FreeTDS.</span><span class="sxs-lookup"><span data-stu-id="6f265-114">**MacOS**: Install Homebrew, install rbenv and ruby-build, install Ruby, and then install FreeTDS.</span></span> <span data-ttu-id="6f265-115">Ознакомьтесь с шагами 1.2, 1.3, 1.4 и 1.5 в [этом руководстве](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/).</span><span class="sxs-lookup"><span data-stu-id="6f265-115">See [Step 1.2, 1.3, 1.4, and 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/).</span></span>
    - <span data-ttu-id="6f265-116">**Ubuntu**: установите необходимые компоненты для Ruby, rbenv и ruby-build, Ruby и FreeTDS.</span><span class="sxs-lookup"><span data-stu-id="6f265-116">**Ubuntu**: Install prerequisites for Ruby, install rbenv and ruby-build, install Ruby, and then install FreeTDS.</span></span> <span data-ttu-id="6f265-117">Ознакомьтесь с шагами 1.2, 1.3, 1.4 и 1.5 в [этом руководстве](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="6f265-117">See [Step 1.2, 1.3, 1.4, and 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu/).</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="6f265-118">Сведения о подключении SQL Server</span><span class="sxs-lookup"><span data-stu-id="6f265-118">SQL server connection information</span></span>

<span data-ttu-id="6f265-119">Получите базу данных Azure SQL toohello tooconnect в сведения, необходимые подключения hello.</span><span class="sxs-lookup"><span data-stu-id="6f265-119">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="6f265-120">Необходимо будет hello полное имя сервера, имя базы данных и сведения об имени входа в следующих процедурах hello.</span><span class="sxs-lookup"><span data-stu-id="6f265-120">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="6f265-121">Войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="6f265-121">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="6f265-122">Выберите **баз данных SQL** hello левом меню и выберите базу данных на hello **баз данных SQL** страницы.</span><span class="sxs-lookup"><span data-stu-id="6f265-122">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="6f265-123">На hello **Обзор** страниц для базы данных, просмотрите hello полное имя сервера.</span><span class="sxs-lookup"><span data-stu-id="6f265-123">On hello **Overview** page for your database, review hello fully qualified server name.</span></span> <span data-ttu-id="6f265-124">Можно навести на toobring имя сервера hello копирование hello **щелкните toocopy** параметра, как показано в hello после изображения:</span><span class="sxs-lookup"><span data-stu-id="6f265-124">You can hover over hello server name toobring up hello **Click toocopy** option, as shown in hello following image:</span></span>

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="6f265-126">Если вы забыли hello учетные данные для сервера базы данных SQL Azure, перейдите toohello базы данных SQL server страницы tooview hello server с именем admin и, при необходимости сбросить пароль hello.</span><span class="sxs-lookup"><span data-stu-id="6f265-126">If you have forgotten hello login information for your Azure SQL Database server, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6f265-127">Необходимо иметь правила брандмауэра на месте для hello общедоступный IP-адрес hello компьютера, на котором выполняется этот учебник.</span><span class="sxs-lookup"><span data-stu-id="6f265-127">You must have a firewall rule in place for hello public IP address of hello computer on which you perform this tutorial.</span></span> <span data-ttu-id="6f265-128">Если вы на другом компьютере или другой общий IP-адрес, создайте [правило брандмауэра уровня сервера с помощью портала Azure "hello"](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="6f265-128">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using hello Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 

## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="6f265-129">Вставьте код базы данных SQL tooquery</span><span class="sxs-lookup"><span data-stu-id="6f265-129">Insert code tooquery SQL database</span></span>

1. <span data-ttu-id="6f265-130">Создайте файл **sqltest.rb** в избранном текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="6f265-130">In your favorite text editor, create a new file, **sqltest.rb**</span></span>

2. <span data-ttu-id="6f265-131">Замените содержимое hello hello ниже программный код и добавить hello соответствующие значения для сервера, базы данных, пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="6f265-131">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

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

## <a name="run-hello-code"></a><span data-ttu-id="6f265-132">Выполнение кода hello</span><span class="sxs-lookup"><span data-stu-id="6f265-132">Run hello code</span></span>

1. <span data-ttu-id="6f265-133">Hello командной строки выполните следующие команды hello.</span><span class="sxs-lookup"><span data-stu-id="6f265-133">At hello command prompt, run hello following commands:</span></span>

   ```bash
   ruby sqltest.rb
   ```

2. <span data-ttu-id="6f265-134">Убедитесь, что возвращаются первые 20 строк hello и закройте окно приложения hello.</span><span class="sxs-lookup"><span data-stu-id="6f265-134">Verify that hello top 20 rows are returned and then close hello application window.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6f265-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6f265-135">Next Steps</span></span>
- [<span data-ttu-id="6f265-136">Проектирование первой базы данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="6f265-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- <span data-ttu-id="6f265-137">[Просмотрите репозиторий GitHub для TinyTDS](https://github.com/rails-sqlserver/tiny_tds).</span><span class="sxs-lookup"><span data-stu-id="6f265-137">[GitHub repository for TinyTDS](https://github.com/rails-sqlserver/tiny_tds)</span></span>
- [<span data-ttu-id="6f265-138">Сообщите о проблемах или задайте вопросы по TinyTDS</span><span class="sxs-lookup"><span data-stu-id="6f265-138">Report issues or ask questions about TinyTDS</span></span>](https://github.com/rails-sqlserver/tiny_tds/issues)
- <span data-ttu-id="6f265-139">[Ruby Drivers for SQL Server](https://docs.microsoft.com/sql/connect/ruby/ruby-driver-for-sql-server/) (Драйверы Ruby для SQL Server).</span><span class="sxs-lookup"><span data-stu-id="6f265-139">[Ruby Drivers for SQL Server](https://docs.microsoft.com/sql/connect/ruby/ruby-driver-for-sql-server/)</span></span>
