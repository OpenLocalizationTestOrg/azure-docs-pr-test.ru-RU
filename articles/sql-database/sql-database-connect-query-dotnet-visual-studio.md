---
title: "Использование Visual Studio и .NET для создания запросов к базе данных SQL Azure | Документация Майкрософт"
description: "В этой статье показано, как использовать Visual Studio для создания программы, которая подключается к базе данных SQL Azure, и создавать к ней запросы с помощью инструкций Transact-SQL."
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
ms.openlocfilehash: 105dab17823a7e7f6957a604833f4ecad35c14bd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="use-net-c-with-visual-studio-to-connect-and-query-an-azure-sql-database"></a><span data-ttu-id="c67c1-103">Использование .NET (C#) с Visual Studio для подключения и создания запросов к базе данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="c67c1-103">Use .NET (C#) with Visual Studio to connect and query an Azure SQL database</span></span>

<span data-ttu-id="c67c1-104">В этом кратком руководстве показано, как использовать [.NET Framework](https://www.microsoft.com/net/) для создания программы C# с помощью Visual Studio для подключения к базе данных SQL Azure, а затем с помощью инструкций Transact-SQL выполнить запрос к данным.</span><span class="sxs-lookup"><span data-stu-id="c67c1-104">This quick start tutorial demonstrates how to use the [.NET framework](https://www.microsoft.com/net/) to create a C# program with Visual Studio to connect to an Azure SQL database and use Transact-SQL statements to query data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c67c1-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c67c1-105">Prerequisites</span></span>

<span data-ttu-id="c67c1-106">Ниже указаны требования для работы с этим кратким руководством.</span><span class="sxs-lookup"><span data-stu-id="c67c1-106">To complete this quick start tutorial, make sure you have the following:</span></span>

- <span data-ttu-id="c67c1-107">База данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c67c1-107">An Azure SQL database.</span></span> <span data-ttu-id="c67c1-108">В этом кратком руководстве используются ресурсы, созданные в одном из этих кратких руководств:</span><span class="sxs-lookup"><span data-stu-id="c67c1-108">This quick start uses the resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="c67c1-109">Создание базы данных с помощью портала</span><span class="sxs-lookup"><span data-stu-id="c67c1-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="c67c1-110">Создание базы данных SQL Azure и отправка к ней запросов с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c67c1-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="c67c1-111">Создание базы данных с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="c67c1-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="c67c1-112">[Правило брандмауэра на уровне сервера](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) для общедоступного IP-адреса компьютера, на котором выполняются действия из этого краткого руководства.</span><span class="sxs-lookup"><span data-stu-id="c67c1-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for the public IP address of the computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="c67c1-113">Убедитесь, что установлен [Visual Studio Community 2017, Visual Studio Professional 2017 или Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="c67c1-113">An installation of [Visual Studio Community 2017, Visual Studio Professional 2017, or Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="c67c1-114">Сведения о подключении SQL Server</span><span class="sxs-lookup"><span data-stu-id="c67c1-114">SQL server connection information</span></span>

<span data-ttu-id="c67c1-115">Получите сведения о подключении, необходимые для подключения к базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c67c1-115">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="c67c1-116">Вам понадобится следующее: полное имя сервера, имя базы данных и сведения для входа.</span><span class="sxs-lookup"><span data-stu-id="c67c1-116">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="c67c1-117">Войдите на [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c67c1-117">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="c67c1-118">В меню слева выберите **Базы данных SQL** и на странице **Базы данных SQL** щелкните имя своей базы данных.</span><span class="sxs-lookup"><span data-stu-id="c67c1-118">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="c67c1-119">На странице **Обзор** базы данных просмотрите полное имя сервера, как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="c67c1-119">On the **Overview** page for your database, review the fully qualified server name as shown in the following image.</span></span> <span data-ttu-id="c67c1-120">Вы можете навести указатель мыши на имя сервера, чтобы отобразился пункт **Щелкните, чтобы скопировать**.</span><span class="sxs-lookup"><span data-stu-id="c67c1-120">You can hover over the server name to bring up the **Click to copy** option.</span></span> 

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="c67c1-122">Если вы забыли данные для входа на сервер базы данных SQL Azure, перейдите на соответствующую страницу, чтобы просмотреть имя администратора сервера.</span><span class="sxs-lookup"><span data-stu-id="c67c1-122">If you forget your Azure SQL Database server login information, navigate to the SQL Database server page to view the server admin name.</span></span> <span data-ttu-id="c67c1-123">При необходимости вы можете сбросить пароль.</span><span class="sxs-lookup"><span data-stu-id="c67c1-123">You can reset the password if necessary.</span></span>

5. <span data-ttu-id="c67c1-124">Щелкните **Показать строки подключения к базам данных**.</span><span class="sxs-lookup"><span data-stu-id="c67c1-124">Click **Show database connection strings**.</span></span>

6. <span data-ttu-id="c67c1-125">Просмотрите полную строку подключения **ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="c67c1-125">Review the complete **ADO.NET** connection string.</span></span>

    ![Строка подключения по протоколу ADO.NET](./media/sql-database-connect-query-dotnet/adonet-connection-string.png)

> [!IMPORTANT]
> <span data-ttu-id="c67c1-127">Необходимо настроить правила брандмауэра для общедоступного IP-адреса компьютера, на котором выполняются действия из этого руководства.</span><span class="sxs-lookup"><span data-stu-id="c67c1-127">You must have a firewall rule in place for the public IP address of the computer on which you perform this tutorial.</span></span> <span data-ttu-id="c67c1-128">Если вы используете другой компьютер или имеете другой общедоступный IP-адрес, создайте [правила брандмауэра на уровне сервера с помощью портала Azure](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="c67c1-128">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using the Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 
>
  
## <a name="create-a-new-visual-studio-project"></a><span data-ttu-id="c67c1-129">Создание проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c67c1-129">Create a new Visual Studio project</span></span>

1. <span data-ttu-id="c67c1-130">В Visual Studio выберите **Файл**, **Создать**, **Проект**.</span><span class="sxs-lookup"><span data-stu-id="c67c1-130">In Visual Studio, choose **File**, **New**, **Project**.</span></span> 
2. <span data-ttu-id="c67c1-131">Откройте диалоговое окно **Создать проект** и разверните **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="c67c1-131">In the **New Project** dialog, and expand **Visual C#**.</span></span>
3. <span data-ttu-id="c67c1-132">Выберите **Консольное приложение** и введите *sqltest* для имени проекта.</span><span class="sxs-lookup"><span data-stu-id="c67c1-132">Select **Console App** and enter *sqltest* for the project name.</span></span>
4. <span data-ttu-id="c67c1-133">Нажмите кнопку **ОК**, чтобы создать и открыть проект в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c67c1-133">Click **OK** to create and open the new project in Visual Studio</span></span>
4. <span data-ttu-id="c67c1-134">В обозревателе решений щелкните правой кнопкой мыши **sqltest** и щелкните **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="c67c1-134">In Solution Explorer, right-click **sqltest** and click **Manage NuGet Packages**.</span></span> 
5. <span data-ttu-id="c67c1-135">Щелкните **Обзор**, выполните поиск по запросу ```System.Data.SqlClient``` и выберите его по завершении поиска.</span><span class="sxs-lookup"><span data-stu-id="c67c1-135">On the **Browse**, search for ```System.Data.SqlClient``` and, when found, select it.</span></span>
6. <span data-ttu-id="c67c1-136">На странице **System.Data.SqlClient** щелкните **Установить**.</span><span class="sxs-lookup"><span data-stu-id="c67c1-136">In the **System.Data.SqlClient** page, click **Install**.</span></span>
7. <span data-ttu-id="c67c1-137">После завершения установки просмотрите изменения, а затем нажмите кнопку **ОК**, чтобы закрыть окно **предварительного просмотра**.</span><span class="sxs-lookup"><span data-stu-id="c67c1-137">When the install completes, review the changes and then click **OK** to close the **Preview** window.</span></span> 
8. <span data-ttu-id="c67c1-138">Если откроется окно **Прием условий лицензионного соглашения**, щелкните **Я принимаю**.</span><span class="sxs-lookup"><span data-stu-id="c67c1-138">If a **License Acceptance** window appears, click **I Accept**.</span></span>

## <a name="insert-code-to-query-sql-database"></a><span data-ttu-id="c67c1-139">Вставка кода для отправки запроса к базе данных SQL</span><span class="sxs-lookup"><span data-stu-id="c67c1-139">Insert code to query SQL database</span></span>
1. <span data-ttu-id="c67c1-140">Перейдите к (или откройте при необходимости) **Program.cs**.</span><span class="sxs-lookup"><span data-stu-id="c67c1-140">Switch to (or open if necessary) **Program.cs**</span></span>

2. <span data-ttu-id="c67c1-141">Замените содержимое **Program.cs** следующим кодом и добавьте соответствующие значения для сервера, базы данных, пользователя и пароля.</span><span class="sxs-lookup"><span data-stu-id="c67c1-141">Replace the contents of **Program.cs** with the following code and add the appropriate values for your server, database, user, and password.</span></span>

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

## <a name="run-the-code"></a><span data-ttu-id="c67c1-142">Выполнение кода</span><span class="sxs-lookup"><span data-stu-id="c67c1-142">Run the code</span></span>

1. <span data-ttu-id="c67c1-143">Нажмите клавишу **F5** для запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="c67c1-143">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="c67c1-144">Убедитесь, что возвращены первые 20 строк, а затем закройте окно приложения.</span><span class="sxs-lookup"><span data-stu-id="c67c1-144">Verify that the top 20 rows are returned and then close the application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c67c1-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c67c1-145">Next steps</span></span>

- <span data-ttu-id="c67c1-146">Узнайте, как [подключиться и отправить запрос к базе данных SQL Azure с помощью .NET Core](sql-database-connect-query-dotnet-core.md) в Windows, Linux и Mac OS.</span><span class="sxs-lookup"><span data-stu-id="c67c1-146">Learn how to [connect and query an Azure SQL database using .NET core](sql-database-connect-query-dotnet-core.md) on Windows/Linux/macOS.</span></span>  
- <span data-ttu-id="c67c1-147">См. дополнительные сведения о [начале работы с .NET Core в Windows, Linux и Mac OS с помощью командной строки](/dotnet/core/tutorials/using-with-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="c67c1-147">Learn about [Getting started with .NET Core on Windows/Linux/macOS using the command line](/dotnet/core/tutorials/using-with-xplat-cli).</span></span>
- <span data-ttu-id="c67c1-148">Узнайте, как спроектировать первую базу данных SQL с помощью [SSMS](sql-database-design-first-database.md) или [.NET](sql-database-design-first-database-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="c67c1-148">Learn how to [Design your first Azure SQL database using SSMS](sql-database-design-first-database.md) or [Design your first Azure SQL database using .NET](sql-database-design-first-database-csharp.md).</span></span>
- <span data-ttu-id="c67c1-149">Дополнительные сведения о .NET см. в [этой документации](https://docs.microsoft.com/dotnet/).</span><span class="sxs-lookup"><span data-stu-id="c67c1-149">For more information about .NET, see [.NET documentation](https://docs.microsoft.com/dotnet/).</span></span>
