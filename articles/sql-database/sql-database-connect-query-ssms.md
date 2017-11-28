---
title: "SSMS: подключение и запрос данных в базе данных SQL Azure | Документация Майкрософт"
description: "Узнайте, как tooconnect tooSQL базы данных в Azure с помощью SQL Server Management Studio (SSMS). Выполните инструкции Transact-SQL (T-SQL) tooquery и изменения данных."
metacanonical: 
keywords: "подключение базы данных toosql, среды sql server management studio"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 7cd2a114-c13c-4ace-9088-97bd9d68de12
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 05/26/2017
ms.author: carlrab
ms.openlocfilehash: 769a3a1ecc34800bd345b64e89841f7147b144f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-use-sql-server-management-studio-tooconnect-and-query-data"></a><span data-ttu-id="8d63e-105">База данных SQL Azure: Использование SQL Server Management Studio tooconnect и запроса данных</span><span class="sxs-lookup"><span data-stu-id="8d63e-105">Azure SQL Database: Use SQL Server Management Studio tooconnect and query data</span></span>

<span data-ttu-id="8d63e-106">[SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) — это интегрированная среда для управления любой инфраструктуры SQL из SQL Server tooSQL базы данных для Microsoft Windows.</span><span class="sxs-lookup"><span data-stu-id="8d63e-106">[SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) is an integrated environment for managing any SQL infrastructure, from SQL Server tooSQL Database for Microsoft Windows.</span></span> <span data-ttu-id="8d63e-107">В этом кратком руководстве показано, как базы данных Azure SQL tooan tooconnect toouse SSMS, а затем tooquery инструкций используйте Transact-SQL, вставки, обновления и удаления данных в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="8d63e-107">This quick start demonstrates how toouse SSMS tooconnect tooan Azure SQL database, and then use Transact-SQL statements tooquery, insert, update, and delete data in hello database.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="8d63e-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8d63e-108">Prerequisites</span></span>

<span data-ttu-id="8d63e-109">В этом кратком руководстве в качестве отправной точки ресурсов hello создана в одном из этих краткие используется:</span><span class="sxs-lookup"><span data-stu-id="8d63e-109">This quick start uses as its starting point hello resources created in one of these quick starts:</span></span>

- [<span data-ttu-id="8d63e-110">Создание базы данных с помощью портала</span><span class="sxs-lookup"><span data-stu-id="8d63e-110">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
- [<span data-ttu-id="8d63e-111">Создание базы данных SQL Azure и отправка к ней запросов с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8d63e-111">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
- [<span data-ttu-id="8d63e-112">Создание базы данных с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="8d63e-112">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

<span data-ttu-id="8d63e-113">Прежде чем начать, убедитесь, что установлен hello новейшую версию [SSMS](https://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="8d63e-113">Before you start, make sure you have installed hello newest version of [SSMS](https://msdn.microsoft.com/library/mt238290.aspx).</span></span> 

## <a name="sql-server-connection-information"></a><span data-ttu-id="8d63e-114">Сведения о подключении SQL Server</span><span class="sxs-lookup"><span data-stu-id="8d63e-114">SQL server connection information</span></span>

<span data-ttu-id="8d63e-115">Получите базу данных Azure SQL toohello tooconnect в сведения, необходимые подключения hello.</span><span class="sxs-lookup"><span data-stu-id="8d63e-115">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="8d63e-116">Необходимо будет hello полное имя сервера, имя базы данных и сведения об имени входа в следующих процедурах hello.</span><span class="sxs-lookup"><span data-stu-id="8d63e-116">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="8d63e-117">Войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="8d63e-117">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="8d63e-118">Выберите **баз данных SQL** hello левом меню и выберите базу данных на hello **баз данных SQL** страницы.</span><span class="sxs-lookup"><span data-stu-id="8d63e-118">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="8d63e-119">На hello **Обзор** страниц для базы данных, просмотрите hello полное имя сервера, как показано в приведенном ниже рисунке hello.</span><span class="sxs-lookup"><span data-stu-id="8d63e-119">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello image below.</span></span> <span data-ttu-id="8d63e-120">Можно навести на toobring имя сервера hello копирование hello **щелкните toocopy** параметр.</span><span class="sxs-lookup"><span data-stu-id="8d63e-120">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span>

   ![Сведения о подключении](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="8d63e-122">Если вы забыли hello учетные данные для сервера базы данных SQL Azure, перейдите toohello базы данных SQL server страницы tooview hello server с именем admin и, при необходимости сбросить пароль hello.</span><span class="sxs-lookup"><span data-stu-id="8d63e-122">If you have forgotten hello login information for your Azure SQL Database server, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span> 

## <a name="connect-tooyour-database"></a><span data-ttu-id="8d63e-123">Подключение базы данных tooyour</span><span class="sxs-lookup"><span data-stu-id="8d63e-123">Connect tooyour database</span></span>

<span data-ttu-id="8d63e-124">С помощью SQL Server Management Studio tooestablish сервером базы данных SQL Azure tooyour соединения.</span><span class="sxs-lookup"><span data-stu-id="8d63e-124">Use SQL Server Management Studio tooestablish a connection tooyour Azure SQL Database server.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="8d63e-125">Логический сервер базы данных SQL Azure прослушивает порт 1433.</span><span class="sxs-lookup"><span data-stu-id="8d63e-125">An Azure SQL Database logical server listens on port 1433.</span></span> <span data-ttu-id="8d63e-126">При попытке tooconnect tooan базы данных SQL Azure логического сервера внутри корпоративного брандмауэра, этот порт должен быть открыт в hello корпоративного брандмауэра для подключения к toosuccessfully вы.</span><span class="sxs-lookup"><span data-stu-id="8d63e-126">If you are attempting tooconnect tooan Azure SQL Database logical server from within a corporate firewall, this port must be open in hello corporate firewall for you toosuccessfully connect.</span></span>
>

1. <span data-ttu-id="8d63e-127">Откройте среду SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="8d63e-127">Open SQL Server Management Studio.</span></span>

2. <span data-ttu-id="8d63e-128">В hello **подключения tooServer** диалогового окна введите hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="8d63e-128">In hello **Connect tooServer** dialog box, enter hello following information:</span></span>

   | <span data-ttu-id="8d63e-129">Настройка</span><span class="sxs-lookup"><span data-stu-id="8d63e-129">Setting</span></span>       | <span data-ttu-id="8d63e-130">Рекомендуемое значение</span><span class="sxs-lookup"><span data-stu-id="8d63e-130">Suggested value</span></span> | <span data-ttu-id="8d63e-131">Описание</span><span class="sxs-lookup"><span data-stu-id="8d63e-131">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="8d63e-132">**Тип сервера**</span><span class="sxs-lookup"><span data-stu-id="8d63e-132">**Server type**</span></span> | <span data-ttu-id="8d63e-133">Ядро СУБД</span><span class="sxs-lookup"><span data-stu-id="8d63e-133">Database engine</span></span> | <span data-ttu-id="8d63e-134">Это обязательное значение.</span><span class="sxs-lookup"><span data-stu-id="8d63e-134">This value is required.</span></span> |
   | <span data-ttu-id="8d63e-135">**Server name** (Имя сервера)</span><span class="sxs-lookup"><span data-stu-id="8d63e-135">**Server name**</span></span> | <span data-ttu-id="8d63e-136">Hello полное имя сервера</span><span class="sxs-lookup"><span data-stu-id="8d63e-136">hello fully qualified server name</span></span> | <span data-ttu-id="8d63e-137">Hello имя должно быть примерно следующим образом: **mynewserver20170313.database.windows.net**.</span><span class="sxs-lookup"><span data-stu-id="8d63e-137">hello name should be something like this: **mynewserver20170313.database.windows.net**.</span></span> |
   | <span data-ttu-id="8d63e-138">**Аутентификация**</span><span class="sxs-lookup"><span data-stu-id="8d63e-138">**Authentication**</span></span> | <span data-ttu-id="8d63e-139">проверка подлинности SQL Server</span><span class="sxs-lookup"><span data-stu-id="8d63e-139">SQL Server Authentication</span></span> | <span data-ttu-id="8d63e-140">Проверка подлинности SQL — тип hello только проверку подлинности, который мы указали в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="8d63e-140">SQL Authentication is hello only authentication type that we have configured in this tutorial.</span></span> |
   | <span data-ttu-id="8d63e-141">**Имя входа**</span><span class="sxs-lookup"><span data-stu-id="8d63e-141">**Login**</span></span> | <span data-ttu-id="8d63e-142">Учетная запись администратора сервера Hello</span><span class="sxs-lookup"><span data-stu-id="8d63e-142">hello server admin account</span></span> | <span data-ttu-id="8d63e-143">Это учетная запись hello, указанный при создании сервера hello.</span><span class="sxs-lookup"><span data-stu-id="8d63e-143">This is hello account that you specified when you created hello server.</span></span> |
   | <span data-ttu-id="8d63e-144">**Пароль**</span><span class="sxs-lookup"><span data-stu-id="8d63e-144">**Password**</span></span> | <span data-ttu-id="8d63e-145">Hello пароль для учетной записи администратора сервера</span><span class="sxs-lookup"><span data-stu-id="8d63e-145">hello password for your server admin account</span></span> | <span data-ttu-id="8d63e-146">Это hello пароль, указанный при создании сервера hello.</span><span class="sxs-lookup"><span data-stu-id="8d63e-146">This is hello password that you specified when you created hello server.</span></span> |

   ![подключение tooserver](./media/sql-database-connect-query-ssms/connect.png)  

3. <span data-ttu-id="8d63e-148">Нажмите кнопку **параметры** в hello **подключения tooserver** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="8d63e-148">Click **Options** in hello **Connect tooserver** dialog box.</span></span> <span data-ttu-id="8d63e-149">В hello **подключения toodatabase** введите **mySampleDatabase** базы данных toothis tooconnect.</span><span class="sxs-lookup"><span data-stu-id="8d63e-149">In hello **Connect toodatabase** section, enter **mySampleDatabase** tooconnect toothis database.</span></span>

   ![подключение toodb на сервере](./media/sql-database-connect-query-ssms/options-connect-to-db.png)  

4. <span data-ttu-id="8d63e-151">Щелкните **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="8d63e-151">Click **Connect**.</span></span> <span data-ttu-id="8d63e-152">Откроется окно обозревателя объектов Hello в среде SSMS.</span><span class="sxs-lookup"><span data-stu-id="8d63e-152">hello Object Explorer window opens in SSMS.</span></span> 

   ![подключенный tooserver](./media/sql-database-connect-query-ssms/connected.png)  

5. <span data-ttu-id="8d63e-154">В обозревателе объектов разверните **баз данных** и разверните **mySampleDatabase** tooview объектов hello в образце hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="8d63e-154">In Object Explorer, expand **Databases** and then expand **mySampleDatabase** tooview hello objects in hello sample database.</span></span>

## <a name="query-data"></a><span data-ttu-id="8d63e-155">Запрос данных</span><span class="sxs-lookup"><span data-stu-id="8d63e-155">Query data</span></span>

<span data-ttu-id="8d63e-156">Используйте hello следующий код tooquery для hello 20 основных продуктов по категориям, используя hello [ВЫБЕРИТЕ](https://msdn.microsoft.com/library/ms189499.aspx) инструкции Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="8d63e-156">Use hello following code tooquery for hello top 20 products by category using hello [SELECT](https://msdn.microsoft.com/library/ms189499.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="8d63e-157">В обозревателе объектов щелкните правой кнопкой мыши **mySampleDatabase** и выберите пункт **Новый запрос**.</span><span class="sxs-lookup"><span data-stu-id="8d63e-157">In Object Explorer, right-click **mySampleDatabase** and click **New Query**.</span></span> <span data-ttu-id="8d63e-158">Пустое окно запроса, откроется tooyour подключенной базы данных.</span><span class="sxs-lookup"><span data-stu-id="8d63e-158">A blank query window opens that is connected tooyour database.</span></span>
2. <span data-ttu-id="8d63e-159">В окне запроса hello введите приветствия при следующем запросе:</span><span class="sxs-lookup"><span data-stu-id="8d63e-159">In hello query window, enter hello following query:</span></span>

   ```sql
   SELECT pc.Name as CategoryName, p.name as ProductName
   FROM [SalesLT].[ProductCategory] pc
   JOIN [SalesLT].[Product] p
   ON pc.productcategoryid = p.productcategoryid;
   ```

3. <span data-ttu-id="8d63e-160">На панели инструментов hello, нажмите кнопку **Execute** tooretrieve данные из таблицы Product и ProductCategory hello.</span><span class="sxs-lookup"><span data-stu-id="8d63e-160">On hello toolbar, click **Execute** tooretrieve data from hello Product and ProductCategory tables.</span></span>

    ![query](./media/sql-database-connect-query-ssms/query.png)

## <a name="insert-data"></a><span data-ttu-id="8d63e-162">Добавление данных</span><span class="sxs-lookup"><span data-stu-id="8d63e-162">Insert data</span></span>

<span data-ttu-id="8d63e-163">Используйте следующие hello кода tooinsert новый продукт SalesLT.Product таблицу hello hello [вставить](https://msdn.microsoft.com/library/ms174335.aspx) инструкции Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="8d63e-163">Use hello following code tooinsert a new product into hello SalesLT.Product table using hello [INSERT](https://msdn.microsoft.com/library/ms174335.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="8d63e-164">В окне запроса hello замените предыдущий запрос hello приветствия при следующем запросе:</span><span class="sxs-lookup"><span data-stu-id="8d63e-164">In hello query window, replace hello previous query with hello following query:</span></span>

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

2. <span data-ttu-id="8d63e-165">На панели инструментов hello, нажмите кнопку **Execute** tooinsert новую строку в таблице Product hello.</span><span class="sxs-lookup"><span data-stu-id="8d63e-165">On hello toolbar, click **Execute**  tooinsert a new row in hello Product table.</span></span>

    <img src="./media/sql-database-connect-query-ssms/insert.png" alt="insert" style="width: 780px;" />

## <a name="update-data"></a><span data-ttu-id="8d63e-166">Обновление данных</span><span class="sxs-lookup"><span data-stu-id="8d63e-166">Update data</span></span>

<span data-ttu-id="8d63e-167">Используйте hello следующий код tooupdate hello новым продуктом, добавленный ранее с помощью hello [обновление](https://msdn.microsoft.com/library/ms177523.aspx) инструкции Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="8d63e-167">Use hello following code tooupdate hello new product that you previously added using hello [UPDATE](https://msdn.microsoft.com/library/ms177523.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="8d63e-168">В окне запроса hello замените предыдущий запрос hello приветствия при следующем запросе:</span><span class="sxs-lookup"><span data-stu-id="8d63e-168">In hello query window, replace hello previous query with hello following query:</span></span>

   ```sql
   UPDATE [SalesLT].[Product]
   SET [ListPrice] = 125
   WHERE Name = 'myNewProduct';
   ```

2. <span data-ttu-id="8d63e-169">На панели инструментов hello, нажмите кнопку **Execute** tooupdate hello указанной строки в таблице Product hello.</span><span class="sxs-lookup"><span data-stu-id="8d63e-169">On hello toolbar, click **Execute** tooupdate hello specified row in hello Product table.</span></span>

    <img src="./media/sql-database-connect-query-ssms/update.png" alt="update" style="width: 780px;" />

## <a name="delete-data"></a><span data-ttu-id="8d63e-170">Удаление данных</span><span class="sxs-lookup"><span data-stu-id="8d63e-170">Delete data</span></span>

<span data-ttu-id="8d63e-171">Используйте hello следующий код toodelete hello новым продуктом, добавленный ранее с помощью hello [удалить](https://msdn.microsoft.com/library/ms189835.aspx) инструкции Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="8d63e-171">Use hello following code toodelete hello new product that you previously added using hello [DELETE](https://msdn.microsoft.com/library/ms189835.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="8d63e-172">В окне запроса hello замените предыдущий запрос hello приветствия при следующем запросе:</span><span class="sxs-lookup"><span data-stu-id="8d63e-172">In hello query window, replace hello previous query with hello following query:</span></span>

   ```sql
   DELETE FROM [SalesLT].[Product]
   WHERE Name = 'myNewProduct';
   ```

2. <span data-ttu-id="8d63e-173">На панели инструментов hello, нажмите кнопку **Execute** toodelete hello указанной строки в таблице Product hello.</span><span class="sxs-lookup"><span data-stu-id="8d63e-173">On hello toolbar, click **Execute** toodelete hello specified row in hello Product table.</span></span>

    <img src="./media/sql-database-connect-query-ssms/delete.png" alt="delete" style="width: 780px;" />

## <a name="next-steps"></a><span data-ttu-id="8d63e-174">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8d63e-174">Next steps</span></span>

- <span data-ttu-id="8d63e-175">toolearn по созданию и управлению серверами и базами данных с помощью Transact-SQL, в разделе [Дополнительные сведения о базах данных и серверов баз данных SQL Azure](sql-database-servers-databases.md).</span><span class="sxs-lookup"><span data-stu-id="8d63e-175">toolearn about creating and managing servers and databases with Transact-SQL, see [Learn about Azure SQL Database servers and databases](sql-database-servers-databases.md).</span></span>
- <span data-ttu-id="8d63e-176">Дополнительные сведения о решении SSMS см. в статье об [использовании SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx).</span><span class="sxs-lookup"><span data-stu-id="8d63e-176">For information about SSMS, see [Use SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx).</span></span>
- <span data-ttu-id="8d63e-177">tooconnect и запроса с помощью кода Visual Studio, в разделе [подключение и запрос с кодом Visual Studio](sql-database-connect-query-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="8d63e-177">tooconnect and query using Visual Studio Code, see [Connect and query with Visual Studio Code](sql-database-connect-query-vscode.md).</span></span>
- <span data-ttu-id="8d63e-178">tooconnect и запросов с помощью .NET, в разделе [подключение и запрос с помощью .NET](sql-database-connect-query-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="8d63e-178">tooconnect and query using .NET, see [Connect and query with .NET](sql-database-connect-query-dotnet.md).</span></span>
- <span data-ttu-id="8d63e-179">tooconnect и запрос с использованием PHP, в разделе [подключение и запрос с PHP](sql-database-connect-query-php.md).</span><span class="sxs-lookup"><span data-stu-id="8d63e-179">tooconnect and query using PHP, see [Connect and query with PHP](sql-database-connect-query-php.md).</span></span>
- <span data-ttu-id="8d63e-180">tooconnect и запрос с помощью Node.js, см. [подключение и запрос с Node.js](sql-database-connect-query-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="8d63e-180">tooconnect and query using Node.js, see [Connect and query with Node.js](sql-database-connect-query-nodejs.md).</span></span>
- <span data-ttu-id="8d63e-181">tooconnect и запрос с помощью Java, в разделе [подключение и запрос с помощью Java](sql-database-connect-query-java.md).</span><span class="sxs-lookup"><span data-stu-id="8d63e-181">tooconnect and query using Java, see [Connect and query with Java](sql-database-connect-query-java.md).</span></span>
- <span data-ttu-id="8d63e-182">tooconnect и запрос с помощью Python, в разделе [подключение и запрос с Python](sql-database-connect-query-python.md).</span><span class="sxs-lookup"><span data-stu-id="8d63e-182">tooconnect and query using Python, see [Connect and query with Python](sql-database-connect-query-python.md).</span></span>
- <span data-ttu-id="8d63e-183">tooconnect и запрос, используя Ruby. в разделе [подключение и запрос с Ruby](sql-database-connect-query-ruby.md).</span><span class="sxs-lookup"><span data-stu-id="8d63e-183">tooconnect and query using Ruby, see [Connect and query with Ruby](sql-database-connect-query-ruby.md).</span></span>
