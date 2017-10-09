---
title: "VS Code: подключение и запрос данных в базе данных SQL Azure | Документация Майкрософт"
description: "Узнайте, как tooconnect tooSQL базы данных в Azure с помощью кода Visual Studio. Выполните инструкции Transact-SQL (T-SQL) tooquery и изменения данных."
metacanonical: 
keywords: "подключение базы данных toosql"
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
ms.openlocfilehash: ed8bdbfc3271b463a21cde5ff6b5f05fd0ff51d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-use-visual-studio-code-tooconnect-and-query-data"></a><span data-ttu-id="69c35-105">База данных SQL Azure: Использование Visual Studio Code tooconnect и запроса данных</span><span class="sxs-lookup"><span data-stu-id="69c35-105">Azure SQL Database: Use Visual Studio Code tooconnect and query data</span></span>

<span data-ttu-id="69c35-106">[Код Visual Studio](https://code.visualstudio.com/docs) — это код графический редактор для Linux, macOS, и Windows, которые поддерживает расширения, включая hello [mssql расширения](https://aka.ms/mssql-marketplace) для выполнения запросов Microsoft SQL Server, базы данных SQL Azure и хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="69c35-106">[Visual Studio Code](https://code.visualstudio.com/docs) is a graphical code editor for Linux, macOS, and Windows that supports extensions, including hello [mssql extension](https://aka.ms/mssql-marketplace) for querying Microsoft SQL Server, Azure SQL Database, and SQL Data Warehouse.</span></span> <span data-ttu-id="69c35-107">В этом кратком руководстве показано, как базы данных Azure SQL tooan tooconnect toouse кода Visual Studio, а затем tooquery инструкций используйте Transact-SQL, вставки, обновления и удаления данных в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="69c35-107">This quick start demonstrates how toouse Visual Studio Code tooconnect tooan Azure SQL database, and then use Transact-SQL statements tooquery, insert, update, and delete data in hello database.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="69c35-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="69c35-108">Prerequisites</span></span>

<span data-ttu-id="69c35-109">В этом кратком руководстве в качестве отправной точки ресурсов hello создана в одном из этих краткие используется:</span><span class="sxs-lookup"><span data-stu-id="69c35-109">This quick start uses as its starting point hello resources created in one of these quick starts:</span></span>

- [<span data-ttu-id="69c35-110">Создание базы данных с помощью портала</span><span class="sxs-lookup"><span data-stu-id="69c35-110">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
- [<span data-ttu-id="69c35-111">Создание базы данных SQL Azure и отправка к ней запросов с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="69c35-111">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
- [<span data-ttu-id="69c35-112">Создание базы данных с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="69c35-112">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

<span data-ttu-id="69c35-113">Прежде чем начать, убедитесь, что установлен hello новейшую версию [кода Visual Studio](https://code.visualstudio.com/Download) и загружаются hello [mssql расширение](https://aka.ms/mssql-marketplace).</span><span class="sxs-lookup"><span data-stu-id="69c35-113">Before you start, make sure you have installed hello newest version of [Visual Studio Code](https://code.visualstudio.com/Download) and loaded hello [mssql extension](https://aka.ms/mssql-marketplace).</span></span> <span data-ttu-id="69c35-114">Руководство по установке для расширения mssql hello, в разделе [установки VS Code](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode#install-vs-code) и в разделе [mssql для Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql).</span><span class="sxs-lookup"><span data-stu-id="69c35-114">For installation guidance for hello mssql extension, see [Install VS Code](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode#install-vs-code) and see [mssql for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql).</span></span> 

## <a name="configure-vs-code"></a><span data-ttu-id="69c35-115">Настройка кода VS</span><span class="sxs-lookup"><span data-stu-id="69c35-115">Configure VS Code</span></span> 

### <a name="mac-os"></a><span data-ttu-id="69c35-116">**Mac OS**</span><span class="sxs-lookup"><span data-stu-id="69c35-116">**Mac OS**</span></span>
<span data-ttu-id="69c35-117">MacOS необходимо tooinstall OpenSSL, являющийся необходимого компонента для DotNet Core этого расширения mssql использует.</span><span class="sxs-lookup"><span data-stu-id="69c35-117">For macOS, you need tooinstall OpenSSL which is a prerequiste for DotNet Core that mssql extention uses.</span></span> <span data-ttu-id="69c35-118">Откройте терминала и введите следующие команды tooinstall hello **brew** и **OpenSSL**.</span><span class="sxs-lookup"><span data-stu-id="69c35-118">Open your terminal and enter hello following commands tooinstall **brew** and **OpenSSL**.</span></span> 

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
brew install openssl
mkdir -p /usr/local/lib
ln -s /usr/local/opt/openssl/lib/libcrypto.1.0.0.dylib /usr/local/lib/
ln -s /usr/local/opt/openssl/lib/libssl.1.0.0.dylib /usr/local/lib/
```

### <a name="linux-ubuntu"></a><span data-ttu-id="69c35-119">**Linux (Ubuntu)**</span><span class="sxs-lookup"><span data-stu-id="69c35-119">**Linux (Ubuntu)**</span></span>

<span data-ttu-id="69c35-120">Специальная настройка не требуется.</span><span class="sxs-lookup"><span data-stu-id="69c35-120">No special configuration needed.</span></span>

### <a name="windows"></a><span data-ttu-id="69c35-121">**Windows**</span><span class="sxs-lookup"><span data-stu-id="69c35-121">**Windows**</span></span>

<span data-ttu-id="69c35-122">Специальная настройка не требуется.</span><span class="sxs-lookup"><span data-stu-id="69c35-122">No special configuration needed.</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="69c35-123">Сведения о подключении SQL Server</span><span class="sxs-lookup"><span data-stu-id="69c35-123">SQL server connection information</span></span>

<span data-ttu-id="69c35-124">Получите базу данных Azure SQL toohello tooconnect в сведения, необходимые подключения hello.</span><span class="sxs-lookup"><span data-stu-id="69c35-124">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="69c35-125">Необходимо будет hello полное имя сервера, имя базы данных и сведения об имени входа в следующих процедурах hello.</span><span class="sxs-lookup"><span data-stu-id="69c35-125">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="69c35-126">Войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="69c35-126">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="69c35-127">Выберите **баз данных SQL** hello левом меню и выберите базу данных на hello **баз данных SQL** страницы.</span><span class="sxs-lookup"><span data-stu-id="69c35-127">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="69c35-128">На hello **Обзор** страницу для базы данных, просмотрите hello полное доменное имя сервера, как показано в hello после изображения.</span><span class="sxs-lookup"><span data-stu-id="69c35-128">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="69c35-129">Можно навести на toobring имя сервера hello копирование hello **щелкните toocopy** параметр.</span><span class="sxs-lookup"><span data-stu-id="69c35-129">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span>

   ![Сведения о подключении](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="69c35-131">Если вы забыли hello учетные данные для сервера базы данных SQL Azure, перейдите toohello базы данных SQL server страницы tooview hello server с именем admin и, при необходимости сбросить пароль hello.</span><span class="sxs-lookup"><span data-stu-id="69c35-131">If you have forgotten hello login information for your Azure SQL Database server, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span> 

## <a name="set-language-mode-toosql"></a><span data-ttu-id="69c35-132">Режим tooSQL набор языка</span><span class="sxs-lookup"><span data-stu-id="69c35-132">Set language mode tooSQL</span></span>

<span data-ttu-id="69c35-133">Набор hello языка режим слишком**SQL** в командах mssql tooenable кода Visual Studio и T-SQL IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="69c35-133">Set hello language mode is set too**SQL** in Visual Studio Code tooenable mssql commands and T-SQL IntelliSense.</span></span>

1. <span data-ttu-id="69c35-134">Откройте новое окно Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="69c35-134">Open a new Visual Studio Code window.</span></span> 

2. <span data-ttu-id="69c35-135">Нажмите кнопку **обычный текст** в нижнем правом углу hello hello строки состояния.</span><span class="sxs-lookup"><span data-stu-id="69c35-135">Click **Plain Text** in hello lower right-hand corner of hello status bar.</span></span>
3. <span data-ttu-id="69c35-136">В hello **режим выбора языка** раскрывающееся меню, которое открывается, тип **SQL**и нажмите клавишу **ввод** tooset hello языка режим tooSQL.</span><span class="sxs-lookup"><span data-stu-id="69c35-136">In hello **Select language mode** drop-down menu that opens, type **SQL**, and then press **ENTER** tooset hello language mode tooSQL.</span></span> 

   ![Языковой режим SQL](./media/sql-database-connect-query-vscode/vscode-language-mode.png)

## <a name="connect-tooyour-database"></a><span data-ttu-id="69c35-138">Подключение базы данных tooyour</span><span class="sxs-lookup"><span data-stu-id="69c35-138">Connect tooyour database</span></span>

<span data-ttu-id="69c35-139">С помощью Visual Studio Code tooestablish сервером базы данных SQL Azure tooyour соединения.</span><span class="sxs-lookup"><span data-stu-id="69c35-139">Use Visual Studio Code tooestablish a connection tooyour Azure SQL Database server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="69c35-140">Прежде чем продолжить, приготовьте сервер, базу данных и учетные данные.</span><span class="sxs-lookup"><span data-stu-id="69c35-140">Before continuing, make sure that you have your server, database, and login information ready.</span></span> <span data-ttu-id="69c35-141">После началом ввода данных профиля подключения hello, при изменении фокуса ввода из кода Visual Studio, вы сможете toorestart Создание профиля подключения hello.</span><span class="sxs-lookup"><span data-stu-id="69c35-141">Once you begin entering hello connection profile information, if you change your focus from Visual Studio Code, you have toorestart creating hello connection profile.</span></span>
>

1. <span data-ttu-id="69c35-142">В VS Code нажмите **CTRL + SHIFT + P** (или **F1**) tooopen hello палитры команд.</span><span class="sxs-lookup"><span data-stu-id="69c35-142">In VS Code, press **CTRL+SHIFT+P** (or **F1**) tooopen hello Command Palette.</span></span>

2. <span data-ttu-id="69c35-143">Введите **sqlcon** и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="69c35-143">Type **sqlcon** and press **ENTER**.</span></span>

3. <span data-ttu-id="69c35-144">Нажмите клавишу **ввод** tooselect **создать профиль подключения**.</span><span class="sxs-lookup"><span data-stu-id="69c35-144">Press **ENTER** tooselect **Create Connection Profile**.</span></span> <span data-ttu-id="69c35-145">Для экземпляра SQL Server будет создан профиль подключения.</span><span class="sxs-lookup"><span data-stu-id="69c35-145">This creates a connection profile for your SQL Server instance.</span></span>

4. <span data-ttu-id="69c35-146">Соблюдают hello приглашения toospecify hello подключения для нового профиля подключения hello.</span><span class="sxs-lookup"><span data-stu-id="69c35-146">Follow hello prompts toospecify hello connection properties for hello new connection profile.</span></span> <span data-ttu-id="69c35-147">После ввода каждого значения, нажмите клавишу **ввод** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="69c35-147">After specifying each value, press **ENTER** toocontinue.</span></span> 

   | <span data-ttu-id="69c35-148">Настройка</span><span class="sxs-lookup"><span data-stu-id="69c35-148">Setting</span></span>       | <span data-ttu-id="69c35-149">Рекомендуемое значение</span><span class="sxs-lookup"><span data-stu-id="69c35-149">Suggested value</span></span> | <span data-ttu-id="69c35-150">Описание</span><span class="sxs-lookup"><span data-stu-id="69c35-150">Description</span></span> |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="69c35-151">**Имя сервера</span><span class="sxs-lookup"><span data-stu-id="69c35-151">**Server name</span></span> | <span data-ttu-id="69c35-152">Hello полное имя сервера</span><span class="sxs-lookup"><span data-stu-id="69c35-152">hello fully qualified server name</span></span> | <span data-ttu-id="69c35-153">Hello имя должно быть примерно следующим образом: **mynewserver20170313.database.windows.net**.</span><span class="sxs-lookup"><span data-stu-id="69c35-153">hello name should be something like this: **mynewserver20170313.database.windows.net**.</span></span> |
   | <span data-ttu-id="69c35-154">**Database name** (Имя базы данных)</span><span class="sxs-lookup"><span data-stu-id="69c35-154">**Database name**</span></span> | <span data-ttu-id="69c35-155">mySampleDatabase</span><span class="sxs-lookup"><span data-stu-id="69c35-155">mySampleDatabase</span></span> | <span data-ttu-id="69c35-156">Имя Hello tooconnect toowhich hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="69c35-156">hello name of hello database toowhich tooconnect.</span></span> |
   | <span data-ttu-id="69c35-157">**Аутентификация**</span><span class="sxs-lookup"><span data-stu-id="69c35-157">**Authentication**</span></span> | <span data-ttu-id="69c35-158">Имя для входа в SQL</span><span class="sxs-lookup"><span data-stu-id="69c35-158">SQL Login</span></span>| <span data-ttu-id="69c35-159">Проверка подлинности SQL — тип hello только проверку подлинности, который мы указали в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="69c35-159">SQL Authentication is hello only authentication type that we have configured in this tutorial.</span></span> |
   | <span data-ttu-id="69c35-160">**Имя пользователя**</span><span class="sxs-lookup"><span data-stu-id="69c35-160">**User name**</span></span> | <span data-ttu-id="69c35-161">Учетная запись администратора сервера Hello</span><span class="sxs-lookup"><span data-stu-id="69c35-161">hello server admin account</span></span> | <span data-ttu-id="69c35-162">Это учетная запись hello, указанный при создании сервера hello.</span><span class="sxs-lookup"><span data-stu-id="69c35-162">This is hello account that you specified when you created hello server.</span></span> |
   | <span data-ttu-id="69c35-163">**Password (SQL Login)** (Пароль для входа в SQL)</span><span class="sxs-lookup"><span data-stu-id="69c35-163">**Password (SQL Login)**</span></span> | <span data-ttu-id="69c35-164">Hello пароль для учетной записи администратора сервера</span><span class="sxs-lookup"><span data-stu-id="69c35-164">hello password for your server admin account</span></span> | <span data-ttu-id="69c35-165">Это hello пароль, указанный при создании сервера hello.</span><span class="sxs-lookup"><span data-stu-id="69c35-165">This is hello password that you specified when you created hello server.</span></span> |
   | <span data-ttu-id="69c35-166">**Save Password?** (Сохранить пароль?)</span><span class="sxs-lookup"><span data-stu-id="69c35-166">**Save Password?**</span></span> | <span data-ttu-id="69c35-167">"Да" или "Нет"</span><span class="sxs-lookup"><span data-stu-id="69c35-167">Yes or No</span></span> | <span data-ttu-id="69c35-168">Если не требуется пароль hello tooenter каждый раз, нажмите кнопку "Да".</span><span class="sxs-lookup"><span data-stu-id="69c35-168">Select Yes if you do not want tooenter hello password each time.</span></span> |
   | <span data-ttu-id="69c35-169">**Укажите имя для этого профиля**</span><span class="sxs-lookup"><span data-stu-id="69c35-169">**Enter a name for this profile**</span></span> | <span data-ttu-id="69c35-170">Имя профиля, например **mySampleDatabase**.</span><span class="sxs-lookup"><span data-stu-id="69c35-170">A profile name, such as **mySampleDatabase**</span></span> | <span data-ttu-id="69c35-171">Сохраненное имя профиля повышает скорость подключения при последующих входах.</span><span class="sxs-lookup"><span data-stu-id="69c35-171">A saved profile name speeds your connection on subsequent logins.</span></span> | 

5. <span data-ttu-id="69c35-172">Нажмите клавишу hello **ESC** ключа tooclose hello информационное сообщение, информирующее о том, что профиль hello создается и подключены.</span><span class="sxs-lookup"><span data-stu-id="69c35-172">Press hello **ESC** key tooclose hello info message that informs you that hello profile is created and connected.</span></span>

6. <span data-ttu-id="69c35-173">Проверки подключения в строке состояния hello.</span><span class="sxs-lookup"><span data-stu-id="69c35-173">Verify your connection in hello status bar.</span></span>

   ![Состояние подключения](./media/sql-database-connect-query-vscode/vscode-connection-status.png)

## <a name="query-data"></a><span data-ttu-id="69c35-175">Запрос данных</span><span class="sxs-lookup"><span data-stu-id="69c35-175">Query data</span></span>

<span data-ttu-id="69c35-176">Используйте hello следующий код tooquery для hello 20 основных продуктов по категориям, используя hello [ВЫБЕРИТЕ](https://msdn.microsoft.com/library/ms189499.aspx) инструкции Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="69c35-176">Use hello following code tooquery for hello top 20 products by category using hello [SELECT](https://msdn.microsoft.com/library/ms189499.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="69c35-177">В hello **редактор** окне приветствия при следующем запросе в hello пустое окно запроса введите:</span><span class="sxs-lookup"><span data-stu-id="69c35-177">In hello **Editor** window, enter hello following query in hello empty query window:</span></span>

   ```sql
   SELECT pc.Name as CategoryName, p.name as ProductName
   FROM [SalesLT].[ProductCategory] pc
   JOIN [SalesLT].[Product] p
   ON pc.productcategoryid = p.productcategoryid;
   ```

2. <span data-ttu-id="69c35-178">Нажмите клавишу **CTRL + SHIFT + E** tooretrieve данные из таблицы Product и ProductCategory hello.</span><span class="sxs-lookup"><span data-stu-id="69c35-178">Press **CTRL+SHIFT+E** tooretrieve data from hello Product and ProductCategory tables.</span></span>

    ![Запрос](./media/sql-database-connect-query-vscode/query.png)

## <a name="insert-data"></a><span data-ttu-id="69c35-180">Добавление данных</span><span class="sxs-lookup"><span data-stu-id="69c35-180">Insert data</span></span>

<span data-ttu-id="69c35-181">Используйте следующие hello кода tooinsert новый продукт SalesLT.Product таблицу hello hello [вставить](https://msdn.microsoft.com/library/ms174335.aspx) инструкции Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="69c35-181">Use hello following code tooinsert a new product into hello SalesLT.Product table using hello [INSERT](https://msdn.microsoft.com/library/ms174335.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="69c35-182">В hello **редактор** , удалите предыдущий запрос hello и введите приветствия при следующем запросе:</span><span class="sxs-lookup"><span data-stu-id="69c35-182">In hello **Editor** window, delete hello previous query and enter hello following query:</span></span>

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

2. <span data-ttu-id="69c35-183">Нажмите клавишу **CTRL + SHIFT + E** tooinsert новую строку в таблице Product hello.</span><span class="sxs-lookup"><span data-stu-id="69c35-183">Press **CTRL+SHIFT+E** tooinsert a new row in hello Product table.</span></span>

## <a name="update-data"></a><span data-ttu-id="69c35-184">Обновление данных</span><span class="sxs-lookup"><span data-stu-id="69c35-184">Update data</span></span>

<span data-ttu-id="69c35-185">Используйте hello следующий код tooupdate hello новым продуктом, добавленный ранее с помощью hello [обновление](https://msdn.microsoft.com/library/ms177523.aspx) инструкции Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="69c35-185">Use hello following code tooupdate hello new product that you previously added using hello [UPDATE](https://msdn.microsoft.com/library/ms177523.aspx) Transact-SQL statement.</span></span>

1.  <span data-ttu-id="69c35-186">В hello **редактор** , удалите предыдущий запрос hello и введите приветствия при следующем запросе:</span><span class="sxs-lookup"><span data-stu-id="69c35-186">In hello **Editor** window, delete hello previous query and enter hello following query:</span></span>

   ```sql
   UPDATE [SalesLT].[Product]
   SET [ListPrice] = 125
   WHERE Name = 'myNewProduct';
   ```

2. <span data-ttu-id="69c35-187">Нажмите клавишу **CTRL + SHIFT + E** tooupdate hello указанной строки в таблице Product hello.</span><span class="sxs-lookup"><span data-stu-id="69c35-187">Press **CTRL+SHIFT+E** tooupdate hello specified row in hello Product table.</span></span>

## <a name="delete-data"></a><span data-ttu-id="69c35-188">Удаление данных</span><span class="sxs-lookup"><span data-stu-id="69c35-188">Delete data</span></span>

<span data-ttu-id="69c35-189">Используйте hello следующий код toodelete hello новым продуктом, добавленный ранее с помощью hello [удалить](https://msdn.microsoft.com/library/ms189835.aspx) инструкции Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="69c35-189">Use hello following code toodelete hello new product that you previously added using hello [DELETE](https://msdn.microsoft.com/library/ms189835.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="69c35-190">В hello **редактор** , удалите предыдущий запрос hello и введите приветствия при следующем запросе:</span><span class="sxs-lookup"><span data-stu-id="69c35-190">In hello **Editor** window, delete hello previous query and enter hello following query:</span></span>

   ```sql
   DELETE FROM [SalesLT].[Product]
   WHERE Name = 'myNewProduct';
   ```

2. <span data-ttu-id="69c35-191">Нажмите клавишу **CTRL + SHIFT + E** toodelete hello указанной строки в таблице Product hello.</span><span class="sxs-lookup"><span data-stu-id="69c35-191">Press **CTRL+SHIFT+E** toodelete hello specified row in hello Product table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="69c35-192">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="69c35-192">Next steps</span></span>

- <span data-ttu-id="69c35-193">tooconnect и запрос с помощью SQL Server Management Studio, в разделе [подключение и запрос с помощью SSMS](sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="69c35-193">tooconnect and query using SQL Server Management Studio, see [Connect and query with SSMS](sql-database-connect-query-ssms.md).</span></span>
- <span data-ttu-id="69c35-194">Статью из журнала MSDN, посвященную использованию кода Visual Studio, можно просмотреть в записи блога о [создании базы данных IDE с помощью расширения MSSQL](https://msdn.microsoft.com/magazine/mt809115).</span><span class="sxs-lookup"><span data-stu-id="69c35-194">For an MSDN magazine article on using Visual Studio Code, see [Create a database IDE with MSSQL extension blog post](https://msdn.microsoft.com/magazine/mt809115).</span></span>
