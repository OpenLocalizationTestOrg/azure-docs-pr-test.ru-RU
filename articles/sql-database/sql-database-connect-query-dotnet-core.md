---
title: "Использование .NET Core для создания запросов к базе данных SQL Azure | Документация Майкрософт"
description: "Из этой статьи вы узнаете, как использовать .NET Core для создания программы, которая подключается к базе данных SQL Azure, и создавать к ней запросы с помощью инструкций Transact-SQL."
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
ms.openlocfilehash: 046322624d3b89bb983acee863534256fee94b60
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="use-net-core-c-to-query-an-azure-sql-database"></a><span data-ttu-id="e72f0-103">Использование .NET Core (C#) для создания запросов к базе данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="e72f0-103">Use .NET Core (C#) to query an Azure SQL database</span></span>

<span data-ttu-id="e72f0-104">В этом кратком руководстве показано, как использовать [.NET Core](https://www.microsoft.com/net/) в Windows, Linux и Mac OS для создания программы C#, которая подключается к базе данных SQL Azure, а затем с помощью инструкций Transact-SQL выполнить запрос к данным.</span><span class="sxs-lookup"><span data-stu-id="e72f0-104">This quick start tutorial demonstrates how to use [.NET Core](https://www.microsoft.com/net/) on Windows/Linux/macOS to create a C# program to connect to an Azure SQL database and use Transact-SQL statements to query data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e72f0-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e72f0-105">Prerequisites</span></span>

<span data-ttu-id="e72f0-106">Ниже указаны требования для работы с этим кратким руководством.</span><span class="sxs-lookup"><span data-stu-id="e72f0-106">To complete this quick start tutorial, make sure you have the following:</span></span>

- <span data-ttu-id="e72f0-107">База данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="e72f0-107">An Azure SQL database.</span></span> <span data-ttu-id="e72f0-108">В этом кратком руководстве используются ресурсы, созданные в одном из этих кратких руководств:</span><span class="sxs-lookup"><span data-stu-id="e72f0-108">This quick start uses the resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="e72f0-109">Создание базы данных с помощью портала</span><span class="sxs-lookup"><span data-stu-id="e72f0-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="e72f0-110">Создание базы данных SQL Azure и отправка к ней запросов с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e72f0-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="e72f0-111">Создание базы данных с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="e72f0-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="e72f0-112">[Правило брандмауэра на уровне сервера](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) для общедоступного IP-адреса компьютера, на котором выполняются действия из этого краткого руководства.</span><span class="sxs-lookup"><span data-stu-id="e72f0-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for the public IP address of the computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="e72f0-113">Убедитесь, что установлен [.NET Core для вашей операционной системы](https://www.microsoft.com/net/core).</span><span class="sxs-lookup"><span data-stu-id="e72f0-113">You have installed [.NET Core for your operating system](https://www.microsoft.com/net/core).</span></span> 

## <a name="sql-server-connection-information"></a><span data-ttu-id="e72f0-114">Сведения о подключении SQL Server</span><span class="sxs-lookup"><span data-stu-id="e72f0-114">SQL server connection information</span></span>

<span data-ttu-id="e72f0-115">Получите сведения о подключении, необходимые для подключения к базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="e72f0-115">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="e72f0-116">Вам понадобится следующее: полное имя сервера, имя базы данных и сведения для входа.</span><span class="sxs-lookup"><span data-stu-id="e72f0-116">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="e72f0-117">Войдите на [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e72f0-117">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="e72f0-118">В меню слева выберите **Базы данных SQL** и на странице **Базы данных SQL** щелкните имя своей базы данных.</span><span class="sxs-lookup"><span data-stu-id="e72f0-118">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="e72f0-119">На странице **Обзор** базы данных просмотрите полное имя сервера, как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="e72f0-119">On the **Overview** page for your database, review the fully qualified server name as shown in the following image.</span></span> <span data-ttu-id="e72f0-120">Вы можете навести указатель мыши на имя сервера, чтобы отобразился пункт **Щелкните, чтобы скопировать**.</span><span class="sxs-lookup"><span data-stu-id="e72f0-120">You can hover over the server name to bring up the **Click to copy** option.</span></span> 

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="e72f0-122">Если вы забыли данные для входа на сервер базы данных SQL Azure, перейдите на соответствующую страницу, чтобы просмотреть имя администратора сервера.</span><span class="sxs-lookup"><span data-stu-id="e72f0-122">If you forget your Azure SQL Database server login information, navigate to the SQL Database server page to view the server admin name.</span></span> <span data-ttu-id="e72f0-123">При необходимости вы можете сбросить пароль.</span><span class="sxs-lookup"><span data-stu-id="e72f0-123">You can reset the password if necessary.</span></span>

5. <span data-ttu-id="e72f0-124">Щелкните **Показать строки подключения к базам данных**.</span><span class="sxs-lookup"><span data-stu-id="e72f0-124">Click **Show database connection strings**.</span></span>

6. <span data-ttu-id="e72f0-125">Просмотрите полную строку подключения **ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="e72f0-125">Review the complete **ADO.NET** connection string.</span></span>

    ![Строка подключения по протоколу ADO.NET](./media/sql-database-connect-query-dotnet/adonet-connection-string.png)

> [!IMPORTANT]
> <span data-ttu-id="e72f0-127">Необходимо настроить правила брандмауэра для общедоступного IP-адреса компьютера, на котором выполняются действия из этого руководства.</span><span class="sxs-lookup"><span data-stu-id="e72f0-127">You must have a firewall rule in place for the public IP address of the computer on which you perform this tutorial.</span></span> <span data-ttu-id="e72f0-128">Если вы используете другой компьютер или имеете другой общедоступный IP-адрес, создайте [правила брандмауэра на уровне сервера с помощью портала Azure](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="e72f0-128">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using the Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 
>
  
## <a name="create-a-new-net-project"></a><span data-ttu-id="e72f0-129">Создание проекта .NET</span><span class="sxs-lookup"><span data-stu-id="e72f0-129">Create a new .NET project</span></span>

1. <span data-ttu-id="e72f0-130">Откройте командную строку и создайте папку с именем *sqltest*.</span><span class="sxs-lookup"><span data-stu-id="e72f0-130">Open a command prompt and create a folder named *sqltest*.</span></span> <span data-ttu-id="e72f0-131">Перейдите к созданной папке и выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e72f0-131">Navigate to the folder you created and run the following command:</span></span>

    ```
    dotnet new console
    ```

2. <span data-ttu-id="e72f0-132">Откройте ***sqltest.csproj*** с помощью предпочитаемого текстового редактора и добавьте System.Data.SqlClient в качестве зависимости, используя следующий код:</span><span class="sxs-lookup"><span data-stu-id="e72f0-132">Open ***sqltest.csproj*** with your favorite text editor and add System.Data.SqlClient as a dependency using the following code:</span></span>

    ```xml
    <ItemGroup>
        <PackageReference Include="System.Data.SqlClient" Version="4.3.0" />
    </ItemGroup>
    ```

## <a name="insert-code-to-query-sql-database"></a><span data-ttu-id="e72f0-133">Вставка кода для отправки запроса к базе данных SQL</span><span class="sxs-lookup"><span data-stu-id="e72f0-133">Insert code to query SQL database</span></span>

1. <span data-ttu-id="e72f0-134">В среде разработки или в предпочитаемом текстовом редакторе откройте **Program.cs**.</span><span class="sxs-lookup"><span data-stu-id="e72f0-134">In your development environment or favorite text editor open **Program.cs**</span></span>

2. <span data-ttu-id="e72f0-135">Замените содержимое следующим кодом и добавьте соответствующие значения для сервера, базы данных, пользователя и пароля.</span><span class="sxs-lookup"><span data-stu-id="e72f0-135">Replace the contents with the following code and add the appropriate values for your server, database, user, and password.</span></span>

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

## <a name="run-the-code"></a><span data-ttu-id="e72f0-136">Выполнение кода</span><span class="sxs-lookup"><span data-stu-id="e72f0-136">Run the code</span></span>

1. <span data-ttu-id="e72f0-137">В командной строке выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="e72f0-137">At the command prompt, run the following commands:</span></span>

   ```csharp
   dotnet restore
   dotnet run
   ```

2. <span data-ttu-id="e72f0-138">Убедитесь, что возвращены первые 20 строк, а затем закройте окно приложения.</span><span class="sxs-lookup"><span data-stu-id="e72f0-138">Verify that the top 20 rows are returned and then close the application window.</span></span>


## <a name="next-steps"></a><span data-ttu-id="e72f0-139">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e72f0-139">Next steps</span></span>

- <span data-ttu-id="e72f0-140">[Начало работы с .NET Core в Windows, Linux и Mac OS с помощью командной строки](/dotnet/core/tutorials/using-with-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="e72f0-140">[Getting started with .NET Core on Windows/Linux/macOS using the command line](/dotnet/core/tutorials/using-with-xplat-cli).</span></span>
- <span data-ttu-id="e72f0-141">Узнайте, как [подключиться и отправить запрос к базе данных SQL Azure с помощью .NET Framework и Visual Studio](sql-database-connect-query-dotnet-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="e72f0-141">Learn how to [connect and query an Azure SQL database using the .NET framework and Visual Studio](sql-database-connect-query-dotnet-visual-studio.md).</span></span>  
- <span data-ttu-id="e72f0-142">Узнайте, как спроектировать первую базу данных SQL с помощью [SSMS](sql-database-design-first-database.md) или [.NET](sql-database-design-first-database-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="e72f0-142">Learn how to [Design your first Azure SQL database using SSMS](sql-database-design-first-database.md) or [Design your first Azure SQL database using .NET](sql-database-design-first-database-csharp.md).</span></span>
- <span data-ttu-id="e72f0-143">Дополнительные сведения о .NET см. в [этой документации](https://docs.microsoft.com/dotnet/).</span><span class="sxs-lookup"><span data-stu-id="e72f0-143">For more information about .NET, see [.NET documentation](https://docs.microsoft.com/dotnet/).</span></span>
