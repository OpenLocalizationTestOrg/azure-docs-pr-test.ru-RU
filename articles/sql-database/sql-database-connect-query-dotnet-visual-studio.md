---
title: "aaaUse Visual Studio и .NET tooquery базы данных SQL Azure | Документы Microsoft"
description: "В этом разделе показано, как Visual Studio toouse toocreate программу, которая соединяет tooan базы данных SQL Azure и запросов с помощью инструкций Transact-SQL."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/05/2017
ms.author: carlrab
ms.openlocfilehash: 038cfb9c680217dfeea5a9996a0abed88cc80559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-net-c-with-visual-studio-tooconnect-and-query-an-azure-sql-database"></a><span data-ttu-id="912d6-103">Использование с tooconnect Visual Studio .NET (C#) и запроса к базе данных Azure SQL</span><span class="sxs-lookup"><span data-stu-id="912d6-103">Use .NET (C#) with Visual Studio tooconnect and query an Azure SQL database</span></span>

<span data-ttu-id="912d6-104">В этом учебнике быстрого запуска показано как toouse hello [.NET framework](https://www.microsoft.com/net/) toocreate C# программирования с использованием базы данных Azure SQL tooan tooconnect Visual Studio и использовать данные tooquery инструкций Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="912d6-104">This quick start tutorial demonstrates how toouse hello [.NET framework](https://www.microsoft.com/net/) toocreate a C# program with Visual Studio tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="912d6-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="912d6-105">Prerequisites</span></span>

<span data-ttu-id="912d6-106">toocomplete этом краткое руководство по началу работы, убедитесь, что у вас есть следующие hello:</span><span class="sxs-lookup"><span data-stu-id="912d6-106">toocomplete this quick start tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="912d6-107">База данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="912d6-107">An Azure SQL database.</span></span> <span data-ttu-id="912d6-108">В этом кратком руководстве использует ресурсы hello, созданные в одном из этих краткие руководства:</span><span class="sxs-lookup"><span data-stu-id="912d6-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="912d6-109">Создание базы данных с помощью портала</span><span class="sxs-lookup"><span data-stu-id="912d6-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="912d6-110">Создание базы данных SQL Azure и отправка к ней запросов с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="912d6-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="912d6-111">Создание базы данных с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="912d6-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="912d6-112">Объект [правила брандмауэра уровня сервера](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) для hello общедоступный IP-адрес компьютера hello, используйте для этого краткого руководства.</span><span class="sxs-lookup"><span data-stu-id="912d6-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="912d6-113">Убедитесь, что установлен [Visual Studio Community 2017, Visual Studio Professional 2017 или Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="912d6-113">An installation of [Visual Studio Community 2017, Visual Studio Professional 2017, or Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="912d6-114">Сведения о подключении SQL Server</span><span class="sxs-lookup"><span data-stu-id="912d6-114">SQL server connection information</span></span>

<span data-ttu-id="912d6-115">Получите базу данных Azure SQL toohello tooconnect в сведения, необходимые подключения hello.</span><span class="sxs-lookup"><span data-stu-id="912d6-115">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="912d6-116">Необходимо будет hello полное имя сервера, имя базы данных и сведения об имени входа в следующих процедурах hello.</span><span class="sxs-lookup"><span data-stu-id="912d6-116">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="912d6-117">Войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="912d6-117">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="912d6-118">Выберите **баз данных SQL** hello левом меню и выберите базу данных на hello **баз данных SQL** страницы.</span><span class="sxs-lookup"><span data-stu-id="912d6-118">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="912d6-119">На hello **Обзор** страницу для базы данных, просмотрите hello полное доменное имя сервера, как показано в hello после изображения.</span><span class="sxs-lookup"><span data-stu-id="912d6-119">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="912d6-120">Можно навести на toobring имя сервера hello копирование hello **щелкните toocopy** параметр.</span><span class="sxs-lookup"><span data-stu-id="912d6-120">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span> 

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="912d6-122">Если вы забыли учетные данные входа для сервера базы данных SQL Azure, перейдите toohello базы данных SQL server tooview hello server admin имя страницы.</span><span class="sxs-lookup"><span data-stu-id="912d6-122">If you forget your Azure SQL Database server login information, navigate toohello SQL Database server page tooview hello server admin name.</span></span> <span data-ttu-id="912d6-123">При необходимости можно сбросить пароль hello.</span><span class="sxs-lookup"><span data-stu-id="912d6-123">You can reset hello password if necessary.</span></span>

5. <span data-ttu-id="912d6-124">Щелкните **Показать строки подключения к базам данных**.</span><span class="sxs-lookup"><span data-stu-id="912d6-124">Click **Show database connection strings**.</span></span>

6. <span data-ttu-id="912d6-125">Просмотрите hello завершения **ADO.NET** строку подключения.</span><span class="sxs-lookup"><span data-stu-id="912d6-125">Review hello complete **ADO.NET** connection string.</span></span>

    ![Строка подключения по протоколу ADO.NET](./media/sql-database-connect-query-dotnet/adonet-connection-string.png)

> [!IMPORTANT]
> <span data-ttu-id="912d6-127">Необходимо иметь правила брандмауэра на месте для hello общедоступный IP-адрес hello компьютера, на котором выполняется этот учебник.</span><span class="sxs-lookup"><span data-stu-id="912d6-127">You must have a firewall rule in place for hello public IP address of hello computer on which you perform this tutorial.</span></span> <span data-ttu-id="912d6-128">Если вы на другом компьютере или другой общий IP-адрес, создайте [правило брандмауэра уровня сервера с помощью портала Azure "hello"](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="912d6-128">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using hello Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 
>
  
## <a name="create-a-new-visual-studio-project"></a><span data-ttu-id="912d6-129">Создание проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="912d6-129">Create a new Visual Studio project</span></span>

1. <span data-ttu-id="912d6-130">В Visual Studio выберите **Файл**, **Создать**, **Проект**.</span><span class="sxs-lookup"><span data-stu-id="912d6-130">In Visual Studio, choose **File**, **New**, **Project**.</span></span> 
2. <span data-ttu-id="912d6-131">В hello **новый проект** диалоговое окно и разверните **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="912d6-131">In hello **New Project** dialog, and expand **Visual C#**.</span></span>
3. <span data-ttu-id="912d6-132">Выберите **консольного приложения** и введите *sqltest* hello имени проекта.</span><span class="sxs-lookup"><span data-stu-id="912d6-132">Select **Console App** and enter *sqltest* for hello project name.</span></span>
4. <span data-ttu-id="912d6-133">Нажмите кнопку **ОК** toocreate и Привет открыть новый проект в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="912d6-133">Click **OK** toocreate and open hello new project in Visual Studio</span></span>
4. <span data-ttu-id="912d6-134">В обозревателе решений щелкните правой кнопкой мыши **sqltest** и щелкните **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="912d6-134">In Solution Explorer, right-click **sqltest** and click **Manage NuGet Packages**.</span></span> 
5. <span data-ttu-id="912d6-135">На hello **Обзор**, поиск ```System.Data.SqlClient``` и, если найдено, выберите его.</span><span class="sxs-lookup"><span data-stu-id="912d6-135">On hello **Browse**, search for ```System.Data.SqlClient``` and, when found, select it.</span></span>
6. <span data-ttu-id="912d6-136">В hello **System.Data.SqlClient** щелкните **установить**.</span><span class="sxs-lookup"><span data-stu-id="912d6-136">In hello **System.Data.SqlClient** page, click **Install**.</span></span>
7. <span data-ttu-id="912d6-137">По завершении установки hello просмотрите изменения hello и нажмите кнопку **ОК** tooclose hello **предварительного просмотра** окна.</span><span class="sxs-lookup"><span data-stu-id="912d6-137">When hello install completes, review hello changes and then click **OK** tooclose hello **Preview** window.</span></span> 
8. <span data-ttu-id="912d6-138">Если откроется окно **Прием условий лицензионного соглашения**, щелкните **Я принимаю**.</span><span class="sxs-lookup"><span data-stu-id="912d6-138">If a **License Acceptance** window appears, click **I Accept**.</span></span>

## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="912d6-139">Вставьте код базы данных SQL tooquery</span><span class="sxs-lookup"><span data-stu-id="912d6-139">Insert code tooquery SQL database</span></span>
1. <span data-ttu-id="912d6-140">Переключение слишком (или при необходимости откройте) **Program.cs**</span><span class="sxs-lookup"><span data-stu-id="912d6-140">Switch too(or open if necessary) **Program.cs**</span></span>

2. <span data-ttu-id="912d6-141">Замените содержимое hello **Program.cs** с hello ниже программный код и добавить hello соответствующие значения для сервера, базы данных, пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="912d6-141">Replace hello contents of **Program.cs** with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

```csharp
using System;
using System.Data.SqlClient;
using System.Text;

namespace sqltest
{
    class Program
    {
        static void Main(string[] args)
        {
            try 
            { 
                SqlConnectionStringBuilder builder = new SqlConnectionStringBuilder();
                builder.DataSource = "your_server.database.windows.net"; 
                builder.UserID = "your_user";            
                builder.Password = "your_password";     
                builder.InitialCatalog = "your_database";

                using (SqlConnection connection = new SqlConnection(builder.ConnectionString))
                {
                    Console.WriteLine("\nQuery data example:");
                    Console.WriteLine("=========================================\n");
                    
                    connection.Open();       
                    StringBuilder sb = new StringBuilder();
                    sb.Append("SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName ");
                    sb.Append("FROM [SalesLT].[ProductCategory] pc ");
                    sb.Append("JOIN [SalesLT].[Product] p ");
                    sb.Append("ON pc.productcategoryid = p.productcategoryid;");
                    String sql = sb.ToString();

                    using (SqlCommand command = new SqlCommand(sql, connection))
                    {
                        using (SqlDataReader reader = command.ExecuteReader())
                        {
                            while (reader.Read())
                            {
                                Console.WriteLine("{0} {1}", reader.GetString(0), reader.GetString(1));
                            }
                        }
                    }                    
                }
            }
            catch (SqlException e)
            {
                Console.WriteLine(e.ToString());
            }
            Console.ReadLine();
        }
    }
}
```

## <a name="run-hello-code"></a><span data-ttu-id="912d6-142">Выполнение кода hello</span><span class="sxs-lookup"><span data-stu-id="912d6-142">Run hello code</span></span>

1. <span data-ttu-id="912d6-143">Нажмите клавишу **F5** toorun приложения hello.</span><span class="sxs-lookup"><span data-stu-id="912d6-143">Press **F5** toorun hello application.</span></span>
2. <span data-ttu-id="912d6-144">Убедитесь, что возвращаются первые 20 строк hello и закройте окно приложения hello.</span><span class="sxs-lookup"><span data-stu-id="912d6-144">Verify that hello top 20 rows are returned and then close hello application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="912d6-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="912d6-145">Next steps</span></span>

- <span data-ttu-id="912d6-146">Узнайте, каким образом слишком[подключения и запроса к базе данных Azure SQL с помощью .NET core](sql-database-connect-query-dotnet-core.md) на Windows, Linux и macOS.</span><span class="sxs-lookup"><span data-stu-id="912d6-146">Learn how too[connect and query an Azure SQL database using .NET core](sql-database-connect-query-dotnet-core.md) on Windows/Linux/macOS.</span></span>  
- <span data-ttu-id="912d6-147">Дополнительные сведения о [начало работы с .NET Core в Windows и Linux/macOS hello командной строки](/dotnet/core/tutorials/using-with-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="912d6-147">Learn about [Getting started with .NET Core on Windows/Linux/macOS using hello command line](/dotnet/core/tutorials/using-with-xplat-cli).</span></span>
- <span data-ttu-id="912d6-148">Узнайте, каким образом слишком[проектирование первой базы данных Azure SQL с помощью среды SSMS](sql-database-design-first-database.md) или [проектирование первой базы данных Azure SQL с помощью .NET](sql-database-design-first-database-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="912d6-148">Learn how too[Design your first Azure SQL database using SSMS](sql-database-design-first-database.md) or [Design your first Azure SQL database using .NET](sql-database-design-first-database-csharp.md).</span></span>
- <span data-ttu-id="912d6-149">Дополнительные сведения о .NET см. в [этой документации](https://docs.microsoft.com/dotnet/).</span><span class="sxs-lookup"><span data-stu-id="912d6-149">For more information about .NET, see [.NET documentation](https://docs.microsoft.com/dotnet/).</span></span>
