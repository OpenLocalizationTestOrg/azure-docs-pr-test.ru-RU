---
title: "VS Code: подключение и запрос данных в базе данных SQL Azure | Документация Майкрософт"
description: "Сведения о подключении к базе данных SQL в Azure с помощью Visual Studio Code и выполнении инструкций Transact-SQL (T-SQL) для запроса и изменения данных."
metacanonical: 
keywords: "подключение к базе данных SQL"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 676bd799-a571-4bb8-848b-fb1720007866
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/20/2017
ms.author: carlrab
ms.openlocfilehash: 4076b1e7ab3a70009217a1deff72da4bff0dc871
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-sql-database-use-visual-studio-code-to-connect-and-query-data"></a><span data-ttu-id="3d161-105">База данных SQL Azure: подключение и запрос данных с помощью Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="3d161-105">Azure SQL Database: Use Visual Studio Code to connect and query data</span></span>

<span data-ttu-id="3d161-106">[Visual Studio Code](https://code.visualstudio.com/docs) — это графический редактор кода для Linux, macOS и Windows, поддерживающий различные расширения, включая [расширение mssql](https://aka.ms/mssql-marketplace), для выполнения запросов к Microsoft SQL Server, базе данных SQL Azure и хранилищу данных SQL.</span><span class="sxs-lookup"><span data-stu-id="3d161-106">[Visual Studio Code](https://code.visualstudio.com/docs) is a graphical code editor for Linux, macOS, and Windows that supports extensions, including the [mssql extension](https://aka.ms/mssql-marketplace) for querying Microsoft SQL Server, Azure SQL Database, and SQL Data Warehouse.</span></span> <span data-ttu-id="3d161-107">В этом кратком руководстве показано, как, используя Visual Studio Code, подключиться к базе данных SQL Azure, а затем с помощью инструкций Transact-SQL выполнить запрос, вставку, обновление и удаление данных в базе данных.</span><span class="sxs-lookup"><span data-stu-id="3d161-107">This quick start demonstrates how to use Visual Studio Code to connect to an Azure SQL database, and then use Transact-SQL statements to query, insert, update, and delete data in the database.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3d161-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3d161-108">Prerequisites</span></span>

<span data-ttu-id="3d161-109">Начальной точкой в руководстве являются ресурсы, созданные в одном из этих кратких руководств:</span><span class="sxs-lookup"><span data-stu-id="3d161-109">This quick start uses as its starting point the resources created in one of these quick starts:</span></span>

- [<span data-ttu-id="3d161-110">Создание базы данных с помощью портала</span><span class="sxs-lookup"><span data-stu-id="3d161-110">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
- [<span data-ttu-id="3d161-111">Создание базы данных SQL Azure и отправка к ней запросов с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3d161-111">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
- [<span data-ttu-id="3d161-112">Создание базы данных с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="3d161-112">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

<span data-ttu-id="3d161-113">Сначала установите последнюю версию[Visual Studio Code](https://code.visualstudio.com/Download) и загрузите [расширение mssql](https://aka.ms/mssql-marketplace).</span><span class="sxs-lookup"><span data-stu-id="3d161-113">Before you start, make sure you have installed the newest version of [Visual Studio Code](https://code.visualstudio.com/Download) and loaded the [mssql extension](https://aka.ms/mssql-marketplace).</span></span> <span data-ttu-id="3d161-114">Руководство по установке расширения mssql см. в разделе [об установке VS Code](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode#install-vs-code) и на странице [расширения mssql для Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql).</span><span class="sxs-lookup"><span data-stu-id="3d161-114">For installation guidance for the mssql extension, see [Install VS Code](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode#install-vs-code) and see [mssql for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql).</span></span> 

## <a name="configure-vs-code"></a><span data-ttu-id="3d161-115">Настройка кода VS</span><span class="sxs-lookup"><span data-stu-id="3d161-115">Configure VS Code</span></span> 

### <a name="mac-os"></a><span data-ttu-id="3d161-116">**Mac OS**</span><span class="sxs-lookup"><span data-stu-id="3d161-116">**Mac OS**</span></span>
<span data-ttu-id="3d161-117">Для macOS необходимо установить OpenSSL. Это предварительное требование для платформы .NET Core, используемой для расширения mssql.</span><span class="sxs-lookup"><span data-stu-id="3d161-117">For macOS, you need to install OpenSSL which is a prerequiste for DotNet Core that mssql extention uses.</span></span> <span data-ttu-id="3d161-118">Откройте терминал и введите следующие команды для установки **brew** и **OpenSSL**.</span><span class="sxs-lookup"><span data-stu-id="3d161-118">Open your terminal and enter the following commands to install **brew** and **OpenSSL**.</span></span> 

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
brew install openssl
mkdir -p /usr/local/lib
ln -s /usr/local/opt/openssl/lib/libcrypto.1.0.0.dylib /usr/local/lib/
ln -s /usr/local/opt/openssl/lib/libssl.1.0.0.dylib /usr/local/lib/
```

### <a name="linux-ubuntu"></a><span data-ttu-id="3d161-119">**Linux (Ubuntu)**</span><span class="sxs-lookup"><span data-stu-id="3d161-119">**Linux (Ubuntu)**</span></span>

<span data-ttu-id="3d161-120">Специальная настройка не требуется.</span><span class="sxs-lookup"><span data-stu-id="3d161-120">No special configuration needed.</span></span>

### <a name="windows"></a><span data-ttu-id="3d161-121">**Windows**</span><span class="sxs-lookup"><span data-stu-id="3d161-121">**Windows**</span></span>

<span data-ttu-id="3d161-122">Специальная настройка не требуется.</span><span class="sxs-lookup"><span data-stu-id="3d161-122">No special configuration needed.</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="3d161-123">Сведения о подключении SQL Server</span><span class="sxs-lookup"><span data-stu-id="3d161-123">SQL server connection information</span></span>

<span data-ttu-id="3d161-124">Получите сведения о подключении, необходимые для подключения к базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="3d161-124">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="3d161-125">Вам понадобится следующее: полное имя сервера, имя базы данных и сведения для входа.</span><span class="sxs-lookup"><span data-stu-id="3d161-125">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="3d161-126">Войдите на [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3d161-126">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="3d161-127">В меню слева выберите **Базы данных SQL** и на странице **Базы данных SQL** щелкните имя своей базы данных.</span><span class="sxs-lookup"><span data-stu-id="3d161-127">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="3d161-128">На странице **Обзор** базы данных просмотрите полное имя сервера, как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="3d161-128">On the **Overview** page for your database, review the fully qualified server name as shown in the following image.</span></span> <span data-ttu-id="3d161-129">Вы можете навести указатель мыши на имя сервера, чтобы отобразился пункт **Щелкните, чтобы скопировать**.</span><span class="sxs-lookup"><span data-stu-id="3d161-129">You can hover over the server name to bring up the **Click to copy** option.</span></span>

   ![Сведения о подключении](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="3d161-131">Если вы забыли данные для входа на сервер базы данных SQL Azure, перейдите к соответствующей странице, чтобы просмотреть имя администратора сервера и при необходимости сбросить пароль.</span><span class="sxs-lookup"><span data-stu-id="3d161-131">If you have forgotten the login information for your Azure SQL Database server, navigate to the SQL Database server page to view the server admin name and, if necessary, reset the password.</span></span> 

## <a name="set-language-mode-to-sql"></a><span data-ttu-id="3d161-132">Выбор режима языка SQL</span><span class="sxs-lookup"><span data-stu-id="3d161-132">Set language mode to SQL</span></span>

<span data-ttu-id="3d161-133">В Visual Studio Code укажите для режима языка значение **SQL**, чтобы активировать команды mssql и T-SQL IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="3d161-133">Set the language mode is set to **SQL** in Visual Studio Code to enable mssql commands and T-SQL IntelliSense.</span></span>

1. <span data-ttu-id="3d161-134">Откройте новое окно Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="3d161-134">Open a new Visual Studio Code window.</span></span> 

2. <span data-ttu-id="3d161-135">В правом нижнем углу строки состояния щелкните **Обычный текст**.</span><span class="sxs-lookup"><span data-stu-id="3d161-135">Click **Plain Text** in the lower right-hand corner of the status bar.</span></span>
3. <span data-ttu-id="3d161-136">В открывшемся раскрывающемся меню **Выберите языковой режим** введите **SQL** и нажмите клавишу **ВВОД**, чтобы установить языковой режим SQL.</span><span class="sxs-lookup"><span data-stu-id="3d161-136">In the **Select language mode** drop-down menu that opens, type **SQL**, and then press **ENTER** to set the language mode to SQL.</span></span> 

   ![Языковой режим SQL](./media/sql-database-connect-query-vscode/vscode-language-mode.png)

## <a name="connect-to-your-database"></a><span data-ttu-id="3d161-138">Подключение к базе данных</span><span class="sxs-lookup"><span data-stu-id="3d161-138">Connect to your database</span></span>

<span data-ttu-id="3d161-139">С помощью Visual Studio Code подключитесь к серверу базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="3d161-139">Use Visual Studio Code to establish a connection to your Azure SQL Database server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3d161-140">Прежде чем продолжить, приготовьте сервер, базу данных и учетные данные.</span><span class="sxs-lookup"><span data-stu-id="3d161-140">Before continuing, make sure that you have your server, database, and login information ready.</span></span> <span data-ttu-id="3d161-141">Если при вводе данных профиля подключения переключиться с Visual Studio Code, понадобится начать создание профиля подключения заново.</span><span class="sxs-lookup"><span data-stu-id="3d161-141">Once you begin entering the connection profile information, if you change your focus from Visual Studio Code, you have to restart creating the connection profile.</span></span>
>

1. <span data-ttu-id="3d161-142">В VS Code нажмите клавиши **CTRL+SHIFT+P** (или **F1**), чтобы открыть палитру команд.</span><span class="sxs-lookup"><span data-stu-id="3d161-142">In VS Code, press **CTRL+SHIFT+P** (or **F1**) to open the Command Palette.</span></span>

2. <span data-ttu-id="3d161-143">Введите **sqlcon** и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="3d161-143">Type **sqlcon** and press **ENTER**.</span></span>

3. <span data-ttu-id="3d161-144">Нажмите клавишу **ВВОД**, чтобы выбрать **Create Connection Profile** (Создать профиль подключения).</span><span class="sxs-lookup"><span data-stu-id="3d161-144">Press **ENTER** to select **Create Connection Profile**.</span></span> <span data-ttu-id="3d161-145">Для экземпляра SQL Server будет создан профиль подключения.</span><span class="sxs-lookup"><span data-stu-id="3d161-145">This creates a connection profile for your SQL Server instance.</span></span>

4. <span data-ttu-id="3d161-146">Следуйте инструкциям на экране, чтобы указать свойства для нового профиля подключения.</span><span class="sxs-lookup"><span data-stu-id="3d161-146">Follow the prompts to specify the connection properties for the new connection profile.</span></span> <span data-ttu-id="3d161-147">Укажите все значения и нажмите клавишу **ВВОД** для продолжения.</span><span class="sxs-lookup"><span data-stu-id="3d161-147">After specifying each value, press **ENTER** to continue.</span></span> 

   | <span data-ttu-id="3d161-148">Настройка</span><span class="sxs-lookup"><span data-stu-id="3d161-148">Setting</span></span>       | <span data-ttu-id="3d161-149">Рекомендуемое значение</span><span class="sxs-lookup"><span data-stu-id="3d161-149">Suggested value</span></span> | <span data-ttu-id="3d161-150">Описание</span><span class="sxs-lookup"><span data-stu-id="3d161-150">Description</span></span> |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="3d161-151">**Имя сервера</span><span class="sxs-lookup"><span data-stu-id="3d161-151">**Server name</span></span> | <span data-ttu-id="3d161-152">Полное имя сервера</span><span class="sxs-lookup"><span data-stu-id="3d161-152">The fully qualified server name</span></span> | <span data-ttu-id="3d161-153">Имя должно быть примерно таким: **mynewserver20170313.database.windows.net**.</span><span class="sxs-lookup"><span data-stu-id="3d161-153">The name should be something like this: **mynewserver20170313.database.windows.net**.</span></span> |
   | <span data-ttu-id="3d161-154">**Database name** (Имя базы данных)</span><span class="sxs-lookup"><span data-stu-id="3d161-154">**Database name**</span></span> | <span data-ttu-id="3d161-155">mySampleDatabase</span><span class="sxs-lookup"><span data-stu-id="3d161-155">mySampleDatabase</span></span> | <span data-ttu-id="3d161-156">Имя базы данных, к которой устанавливается подключение.</span><span class="sxs-lookup"><span data-stu-id="3d161-156">The name of the database to which to connect.</span></span> |
   | <span data-ttu-id="3d161-157">**Аутентификация**</span><span class="sxs-lookup"><span data-stu-id="3d161-157">**Authentication**</span></span> | <span data-ttu-id="3d161-158">Имя для входа в SQL</span><span class="sxs-lookup"><span data-stu-id="3d161-158">SQL Login</span></span>| <span data-ttu-id="3d161-159">В рамках работы с этим руководством мы настроили только один тип проверки подлинности — проверку подлинности SQL.</span><span class="sxs-lookup"><span data-stu-id="3d161-159">SQL Authentication is the only authentication type that we have configured in this tutorial.</span></span> |
   | <span data-ttu-id="3d161-160">**Имя пользователя**</span><span class="sxs-lookup"><span data-stu-id="3d161-160">**User name**</span></span> | <span data-ttu-id="3d161-161">Учетная запись администратора сервера</span><span class="sxs-lookup"><span data-stu-id="3d161-161">The server admin account</span></span> | <span data-ttu-id="3d161-162">Это учетная запись, указанная при создании сервера.</span><span class="sxs-lookup"><span data-stu-id="3d161-162">This is the account that you specified when you created the server.</span></span> |
   | <span data-ttu-id="3d161-163">**Password (SQL Login)** (Пароль для входа в SQL)</span><span class="sxs-lookup"><span data-stu-id="3d161-163">**Password (SQL Login)**</span></span> | <span data-ttu-id="3d161-164">Пароль учетной записи администратора сервера</span><span class="sxs-lookup"><span data-stu-id="3d161-164">The password for your server admin account</span></span> | <span data-ttu-id="3d161-165">Это пароль, указанный при создании сервера.</span><span class="sxs-lookup"><span data-stu-id="3d161-165">This is the password that you specified when you created the server.</span></span> |
   | <span data-ttu-id="3d161-166">**Save Password?** (Сохранить пароль?)</span><span class="sxs-lookup"><span data-stu-id="3d161-166">**Save Password?**</span></span> | <span data-ttu-id="3d161-167">"Да" или "Нет"</span><span class="sxs-lookup"><span data-stu-id="3d161-167">Yes or No</span></span> | <span data-ttu-id="3d161-168">Выберите "Да", если вы не хотите вводить пароль каждый раз.</span><span class="sxs-lookup"><span data-stu-id="3d161-168">Select Yes if you do not want to enter the password each time.</span></span> |
   | <span data-ttu-id="3d161-169">**Укажите имя для этого профиля**</span><span class="sxs-lookup"><span data-stu-id="3d161-169">**Enter a name for this profile**</span></span> | <span data-ttu-id="3d161-170">Имя профиля, например **mySampleDatabase**.</span><span class="sxs-lookup"><span data-stu-id="3d161-170">A profile name, such as **mySampleDatabase**</span></span> | <span data-ttu-id="3d161-171">Сохраненное имя профиля повышает скорость подключения при последующих входах.</span><span class="sxs-lookup"><span data-stu-id="3d161-171">A saved profile name speeds your connection on subsequent logins.</span></span> | 

5. <span data-ttu-id="3d161-172">Нажмите клавишу **ESC**, чтобы закрыть сообщение с информацией о том, что профиль создан и подключен.</span><span class="sxs-lookup"><span data-stu-id="3d161-172">Press the **ESC** key to close the info message that informs you that the profile is created and connected.</span></span>

6. <span data-ttu-id="3d161-173">Проверьте состояние подключения в строке состояния.</span><span class="sxs-lookup"><span data-stu-id="3d161-173">Verify your connection in the status bar.</span></span>

   ![Состояние подключения](./media/sql-database-connect-query-vscode/vscode-connection-status.png)

## <a name="query-data"></a><span data-ttu-id="3d161-175">Запрос данных</span><span class="sxs-lookup"><span data-stu-id="3d161-175">Query data</span></span>

<span data-ttu-id="3d161-176">Используйте следующий код, чтобы запросить 20 основных продуктов из категории с помощью инструкции [SELECT](https://msdn.microsoft.com/library/ms189499.aspx) Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="3d161-176">Use the following code to query for the top 20 products by category using the [SELECT](https://msdn.microsoft.com/library/ms189499.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="3d161-177">В окне **редактора** введите в пустое окно запроса следующий запрос:</span><span class="sxs-lookup"><span data-stu-id="3d161-177">In the **Editor** window, enter the following query in the empty query window:</span></span>

   ```sql
   SELECT pc.Name as CategoryName, p.name as ProductName
   FROM [SalesLT].[ProductCategory] pc
   JOIN [SalesLT].[Product] p
   ON pc.productcategoryid = p.productcategoryid;
   ```

2. <span data-ttu-id="3d161-178">Нажмите клавиши **CTRL+SHIFT+E**, чтобы получить данные из таблиц Product и ProductCategory.</span><span class="sxs-lookup"><span data-stu-id="3d161-178">Press **CTRL+SHIFT+E** to retrieve data from the Product and ProductCategory tables.</span></span>

    ![Запрос](./media/sql-database-connect-query-vscode/query.png)

## <a name="insert-data"></a><span data-ttu-id="3d161-180">Добавление данных</span><span class="sxs-lookup"><span data-stu-id="3d161-180">Insert data</span></span>

<span data-ttu-id="3d161-181">Используйте указанный ниже код, чтобы вставить новый продукт в таблицу SalesLT.Product с помощью инструкции [INSERT](https://msdn.microsoft.com/library/ms174335.aspx) Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="3d161-181">Use the following code to insert a new product into the SalesLT.Product table using the [INSERT](https://msdn.microsoft.com/library/ms174335.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="3d161-182">В окне **редактора** удалите предыдущий запрос и введите следующий:</span><span class="sxs-lookup"><span data-stu-id="3d161-182">In the **Editor** window, delete the previous query and enter the following query:</span></span>

   ```sql
   INSERT INTO [SalesLT].[Product]
           ( [Name]
           , [ProductNumber]
           , [Color]
           , [ProductCategoryID]
           , [StandardCost]
           , [ListPrice]
           , [SellStartDate]
           )
     VALUES
           ('myNewProduct'
           ,123456789
           ,'NewColor'
           ,1
           ,100
           ,100
           ,GETDATE() );
   ```

2. <span data-ttu-id="3d161-183">Нажмите клавиши **CTRL+SHIFT+E**, чтобы вставить новую строку в таблицу Product.</span><span class="sxs-lookup"><span data-stu-id="3d161-183">Press **CTRL+SHIFT+E** to insert a new row in the Product table.</span></span>

## <a name="update-data"></a><span data-ttu-id="3d161-184">Обновление данных</span><span class="sxs-lookup"><span data-stu-id="3d161-184">Update data</span></span>

<span data-ttu-id="3d161-185">Используйте следующий код, чтобы обновить новый продукт, добавленный ранее, с помощью инструкции [UPDATE](https://msdn.microsoft.com/library/ms177523.aspx) Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="3d161-185">Use the following code to update the new product that you previously added using the [UPDATE](https://msdn.microsoft.com/library/ms177523.aspx) Transact-SQL statement.</span></span>

1.  <span data-ttu-id="3d161-186">В окне **редактора** удалите предыдущий запрос и введите следующий:</span><span class="sxs-lookup"><span data-stu-id="3d161-186">In the **Editor** window, delete the previous query and enter the following query:</span></span>

   ```sql
   UPDATE [SalesLT].[Product]
   SET [ListPrice] = 125
   WHERE Name = 'myNewProduct';
   ```

2. <span data-ttu-id="3d161-187">Нажмите клавиши **CTRL+SHIFT+E**, чтобы обновить указанную строку в таблице Product.</span><span class="sxs-lookup"><span data-stu-id="3d161-187">Press **CTRL+SHIFT+E** to update the specified row in the Product table.</span></span>

## <a name="delete-data"></a><span data-ttu-id="3d161-188">Удаление данных</span><span class="sxs-lookup"><span data-stu-id="3d161-188">Delete data</span></span>

<span data-ttu-id="3d161-189">Используйте следующий код, чтобы удалить новый продукт, добавленный ранее, с помощью инструкции [DELETE](https://msdn.microsoft.com/library/ms189835.aspx) Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="3d161-189">Use the following code to delete the new product that you previously added using the [DELETE](https://msdn.microsoft.com/library/ms189835.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="3d161-190">В окне **редактора** удалите предыдущий запрос и введите следующий:</span><span class="sxs-lookup"><span data-stu-id="3d161-190">In the **Editor** window, delete the previous query and enter the following query:</span></span>

   ```sql
   DELETE FROM [SalesLT].[Product]
   WHERE Name = 'myNewProduct';
   ```

2. <span data-ttu-id="3d161-191">Нажмите клавиши **CTRL+SHIFT+E**, чтобы удалить указанную строку из таблицы Product.</span><span class="sxs-lookup"><span data-stu-id="3d161-191">Press **CTRL+SHIFT+E** to delete the specified row in the Product table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d161-192">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3d161-192">Next steps</span></span>

- <span data-ttu-id="3d161-193">Дополнительные сведения о подключении к базе данных SQL с помощью SQL Server Management Studio и выполнении запроса к ней см. [здесь](sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="3d161-193">To connect and query using SQL Server Management Studio, see [Connect and query with SSMS](sql-database-connect-query-ssms.md).</span></span>
- <span data-ttu-id="3d161-194">Статью из журнала MSDN, посвященную использованию кода Visual Studio, можно просмотреть в записи блога о [создании базы данных IDE с помощью расширения MSSQL](https://msdn.microsoft.com/magazine/mt809115).</span><span class="sxs-lookup"><span data-stu-id="3d161-194">For an MSDN magazine article on using Visual Studio Code, see [Create a database IDE with MSSQL extension blog post](https://msdn.microsoft.com/magazine/mt809115).</span></span>
