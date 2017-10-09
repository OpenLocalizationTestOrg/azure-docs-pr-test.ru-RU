---
title: "Подключение tooAzure базы данных PostgreSQL из C# | Документы Microsoft"
description: "Это краткое руководство содержит C# (.NET). пример кода можно использовать tooconnect и запроса данных из базы данных Azure для PostgreSQL."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: csharp
ms.topic: quickstart
ms.date: 06/23/2017
ms.openlocfilehash: 5ba7426f8ad263193cdb208b3531da0ceff181dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-net-c-tooconnect-and-query-data"></a><span data-ttu-id="18911-103">База данных Azure для PostgreSQL: tooconnect и запрашивают данные, используйте .NET (C#)</span><span class="sxs-lookup"><span data-stu-id="18911-103">Azure Database for PostgreSQL: Use .NET (C#) tooconnect and query data</span></span>
<span data-ttu-id="18911-104">Это краткое руководство демонстрирует, как tooconnect tooan Azure этой базы данных PostgreSQL, с помощью приложения C#.</span><span class="sxs-lookup"><span data-stu-id="18911-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using a C# application.</span></span> <span data-ttu-id="18911-105">Показано, как tooquery инструкций SQL toouse, вставка, обновление и удаление данных в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="18911-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="18911-106">Hello в этой статье предполагается, что вы знакомы с разработка с использованием C#, а новый tooworking с базой данных Azure для PostgreSQL, которые.</span><span class="sxs-lookup"><span data-stu-id="18911-106">hello steps in this article assume that you are familiar with developing using C#, and that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18911-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="18911-107">Prerequisites</span></span>
<span data-ttu-id="18911-108">Это краткое руководство использует ресурсы hello, созданные в любой из этих руководствах по в качестве отправной точки.</span><span class="sxs-lookup"><span data-stu-id="18911-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="18911-109">Создание базы данных с помощью портала</span><span class="sxs-lookup"><span data-stu-id="18911-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="18911-110">Создание базы данных SQL Azure и отправка к ней запросов с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="18911-110">Create DB - CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="18911-111">Также вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="18911-111">You also need to:</span></span>
- <span data-ttu-id="18911-112">установить [.NET Framework](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="18911-112">Install [.NET Framework](https://www.microsoft.com/net/download).</span></span> <span data-ttu-id="18911-113">Следуйте указаниям hello hello связанной статье tooinstall .NET специально для вашей платформы (Windows, Ubuntu Linux или macOS).</span><span class="sxs-lookup"><span data-stu-id="18911-113">Follow hello steps in hello linked article tooinstall .NET specifically for your platform (Windows, Ubuntu Linux, or macOS).</span></span> 
- <span data-ttu-id="18911-114">Установка [Visual Studio](https://www.visualstudio.com/downloads/) или код tootype и редактирования кода Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="18911-114">Install [Visual Studio](https://www.visualstudio.com/downloads/) or Visual Studio Code tootype and edit code.</span></span>
- <span data-ttu-id="18911-115">Установите библиотеку [Npgsql](http://www.npgsql.org/doc/index.html), как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="18911-115">Install [Npgsql](http://www.npgsql.org/doc/index.html) library as described below.</span></span>

## <a name="install-npgsql-references-into-your-visual-studio-solution"></a><span data-ttu-id="18911-116">Установка библиотеки Npgsql со ссылками в решении Visual Studio</span><span class="sxs-lookup"><span data-stu-id="18911-116">Install Npgsql references into your Visual Studio solution</span></span>
<span data-ttu-id="18911-117">tooconnect из hello C# tooPostgreSQL приложения, используйте вызывается поставщик Npgsql ADO.NET библиотеки с открытым исходным кодом hello.</span><span class="sxs-lookup"><span data-stu-id="18911-117">tooconnect from hello C# application tooPostgreSQL, use hello open source ADO.NET library called Npgsql.</span></span> <span data-ttu-id="18911-118">NuGet позволяет загрузить и легко управлять hello ссылки.</span><span class="sxs-lookup"><span data-stu-id="18911-118">NuGet helps download and manage hello references easily.</span></span>

1. <span data-ttu-id="18911-119">Создайте новое решение C# или откройте существующее.</span><span class="sxs-lookup"><span data-stu-id="18911-119">Create a new C# solution, or open an existing one:</span></span> 
   - <span data-ttu-id="18911-120">Создайте решение в Visual Studio, открыв меню "Файл" и последовательно выбрав **Создать** > **Проект**.</span><span class="sxs-lookup"><span data-stu-id="18911-120">Within Visual Studio, create a solution, by clicking File menu **New** > **Project**.</span></span>
   - <span data-ttu-id="18911-121">В hello диалоговое окно "новый проект" разверните **шаблоны** > **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="18911-121">In hello New Project dialogue, expand **Templates** > **Visual C#**.</span></span> 
   - <span data-ttu-id="18911-122">Выберите соответствующий шаблон, например **Console App (.NET Core)** (Консольное приложение (.NET Core)).</span><span class="sxs-lookup"><span data-stu-id="18911-122">Choose an appropriate template such as **Console App (.NET Core)**.</span></span>

2. <span data-ttu-id="18911-123">Используйте hello поставщик Npgsql tooinstall диспетчера пакетов Nuget.</span><span class="sxs-lookup"><span data-stu-id="18911-123">Use hello Nuget Package Manager tooinstall Npgsql:</span></span>
   - <span data-ttu-id="18911-124">Нажмите кнопку hello **средства** меню > **диспетчера пакетов NuGet** > **консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="18911-124">Click hello **Tools** menu > **NuGet Package Manager** > **Package Manager Console**.</span></span>
   - <span data-ttu-id="18911-125">В hello **консоль диспетчера пакетов**, тип`Install-Package Npgsql`</span><span class="sxs-lookup"><span data-stu-id="18911-125">In hello **Package Manager Console**, type `Install-Package Npgsql`</span></span>
   - <span data-ttu-id="18911-126">Hello установки команда загрузки hello Npgsql.dll и связанные сборки и добавляет их в качестве зависимостей в решении hello.</span><span class="sxs-lookup"><span data-stu-id="18911-126">hello install command downloads hello Npgsql.dll and related assemblies and adds them as dependencies in hello solution.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="18911-127">Получение сведений о подключении</span><span class="sxs-lookup"><span data-stu-id="18911-127">Get connection information</span></span>
<span data-ttu-id="18911-128">Получите toohello tooconnect базы данных Azure для hello подключения сведения, необходимые для PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="18911-128">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="18911-129">Необходимо hello server полное имя и учетные данные входа.</span><span class="sxs-lookup"><span data-stu-id="18911-129">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="18911-130">Войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="18911-130">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="18911-131">Hello левого меню на портале Azure, щелкните **все ресурсы** и выполните поиск сервера hello, вы создали, таких как **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="18911-131">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="18911-132">Щелкните имя сервера hello **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="18911-132">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="18911-133">Выберите hello server **Обзор** страницы.</span><span class="sxs-lookup"><span data-stu-id="18911-133">Select hello server's **Overview** page.</span></span> <span data-ttu-id="18911-134">Запишите hello **имя сервера** и **имя входа администратора сервера**.</span><span class="sxs-lookup"><span data-stu-id="18911-134">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="18911-135">![База данных Azure для PostgreSQL. Учетные данные администратора сервера для входа](./media/connect-csharp/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="18911-135">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-csharp/1-connection-string.png)</span></span>
5. <span data-ttu-id="18911-136">Если вы забыли учетные данные входа сервера, перейдите toohello **Обзор** страница hello tooview: имя пользователя администратора сервера и, при необходимости переустановить пароль hello.</span><span class="sxs-lookup"><span data-stu-id="18911-136">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="18911-137">Подключение, создание таблицы и вставка данных</span><span class="sxs-lookup"><span data-stu-id="18911-137">Connect, create table, and insert data</span></span>
<span data-ttu-id="18911-138">Используйте следующие hello кода tooconnect и загружать данные при помощи hello **CREATE TABLE** и **INSERT INTO** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="18911-138">Use hello following code tooconnect and load hello data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span> <span data-ttu-id="18911-139">Hello код использует класс NpgsqlCommand с методом [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish tooPostgreSQL соединения.</span><span class="sxs-lookup"><span data-stu-id="18911-139">hello code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish a connection tooPostgreSQL.</span></span> <span data-ttu-id="18911-140">Затем hello кода использует метод [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), устанавливает свойства CommandText hello и вызывает метод [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) toorun hello базы данных команды.</span><span class="sxs-lookup"><span data-stu-id="18911-140">Then hello code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), sets hello CommandText property, and calls method [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) toorun hello database commands.</span></span> 

<span data-ttu-id="18911-141">Замените параметры узла, DBName, пользователя и пароль hello значениями hello, указанный при создании hello сервера и базы данных.</span><span class="sxs-lookup"><span data-stu-id="18911-141">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Npgsql;

namespace Driver
{
    public class AzurePostgresCreate
    {
        // Obtain connection string information from hello portal
        //
        private static string Host = "mypgserver-20170401.postgres.database.azure.com";
        private static string User = "mylogin@mypgserver-20170401";
        private static string DBname = "mypgsqldb";
        private static string Password = "<server_admin_password>";
        private static string Port = "5432";

        static void Main(string[] args)
        {
            // Build connection string using parameters from portal
            //
            string connString =
                String.Format(
                    "Server={0}; User Id={1}; Database={2}; Port={3}; Password={4}; SSL Mode=Prefer; Trust Server Certificate=true",
                    Host,
                    User,
                    DBname,
                    Port,
                    Password);

            var conn = new NpgsqlConnection(connString);

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText = "DROP TABLE IF EXISTS inventory;";
            command.ExecuteNonQuery();
            Console.Out.WriteLine("Finished dropping table (if existed)");

            command.CommandText = "CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);";
            command.ExecuteNonQuery();
            Console.Out.WriteLine("Finished creating table");

            command.CommandText =
                String.Format(
                    @"
                                INSERT INTO inventory (name, quantity) VALUES ({0}, {1});
                                INSERT INTO inventory (name, quantity) VALUES ({2}, {3});
                                INSERT INTO inventory (name, quantity) VALUES ({4}, {5});
                            ",
                    "\'banana\'", 150,
                    "\'orange\'", 154,
                    "\'apple\'", 100
                    );

            int nRows = command.ExecuteNonQuery();
            Console.Out.WriteLine(String.Format("Number of rows inserted={0}", nRows));

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}
```

## <a name="read-data"></a><span data-ttu-id="18911-142">Считывание данных</span><span class="sxs-lookup"><span data-stu-id="18911-142">Read data</span></span>
<span data-ttu-id="18911-143">Используйте следующие hello кода tooconnect и чтения данных с помощью hello **ВЫБЕРИТЕ** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="18911-143">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="18911-144">Hello код использует класс NpgsqlCommand с методом [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish tooPostgreSQL соединения.</span><span class="sxs-lookup"><span data-stu-id="18911-144">hello code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish a connection tooPostgreSQL.</span></span> <span data-ttu-id="18911-145">Затем hello кода использует метод [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand) и метод [ExecuteReader()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteReader) toorun hello базы данных команды.</span><span class="sxs-lookup"><span data-stu-id="18911-145">Then hello code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand) and method [ExecuteReader()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteReader) toorun hello database commands.</span></span> <span data-ttu-id="18911-146">Здравствуйте, затем код использует [Read()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_Read) tooadvance toohello записей в результатах hello.</span><span class="sxs-lookup"><span data-stu-id="18911-146">Next hello code uses [Read()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_Read) tooadvance toohello records in hello results.</span></span> <span data-ttu-id="18911-147">Затем код hello использует [GetInt32()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetInt32_System_Int32_) и [GetString()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetString_System_Int32_) tooparse hello значения в записи hello.</span><span class="sxs-lookup"><span data-stu-id="18911-147">Then hello code uses [GetInt32()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetInt32_System_Int32_) and [GetString()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetString_System_Int32_) tooparse hello values in hello record.</span></span>

<span data-ttu-id="18911-148">Замените параметры узла, DBName, пользователя и пароль hello значениями hello, указанный при создании hello сервера и базы данных.</span><span class="sxs-lookup"><span data-stu-id="18911-148">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Npgsql;

namespace Driver
{
    public class AzurePostgresRead
    {
        // Obtain connection string information from hello portal
        //
        private static string Host = "mypgserver-20170401.postgres.database.azure.com";
        private static string User = "mylogin@mypgserver-20170401";
        private static string DBname = "mypgsqldb";
        private static string Password = "<server_admin_password>";
        private static string Port = "5432";

        static void Main(string[] args)
        {
            // Build connection string using parameters from portal
            //
            string connString =
                String.Format(
                    "Server={0}; User Id={1}; Database={2}; Port={3}; Password={4};",
                    Host,
                    User,
                    DBname,
                    Port,
                    Password);

            var conn = new NpgsqlConnection(connString);

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText = "SELECT * FROM inventory;";

            var reader = command.ExecuteReader();
            while (reader.Read())
            {
                Console.WriteLine(
                    string.Format(
                        "Reading from table=({0}, {1}, {2})",
                        reader.GetInt32(0).ToString(),
                        reader.GetString(1),
                        reader.GetInt32(2).ToString()
                        )
                    );
            }

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}
```


## <a name="update-data"></a><span data-ttu-id="18911-149">Обновление данных</span><span class="sxs-lookup"><span data-stu-id="18911-149">Update data</span></span>
<span data-ttu-id="18911-150">Используйте следующие hello кода tooconnect и чтения данных с помощью hello **обновление** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="18911-150">Use hello following code tooconnect and read hello data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="18911-151">Hello код использует класс NpgsqlCommand с методом [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish tooPostgreSQL соединения.</span><span class="sxs-lookup"><span data-stu-id="18911-151">hello code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish a connection tooPostgreSQL.</span></span> <span data-ttu-id="18911-152">Затем hello кода использует метод [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), устанавливает свойства CommandText hello и вызывает метод [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) toorun hello базы данных команды.</span><span class="sxs-lookup"><span data-stu-id="18911-152">Then hello code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), sets hello CommandText property, and calls method [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) toorun hello database commands.</span></span>

<span data-ttu-id="18911-153">Замените параметры узла, DBName, пользователя и пароль hello значениями hello, указанный при создании hello сервера и базы данных.</span><span class="sxs-lookup"><span data-stu-id="18911-153">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Npgsql;

namespace Driver
{
    public class AzurePostgresUpdate
    {
        // Obtain connection string information from hello portal
        //
        private static string Host = "mypgserver-20170401.postgres.database.azure.com";
        private static string User = "mylogin@mypgserver-20170401";
        private static string DBname = "mypgsqldb";
        private static string Password = "<server_admin_password>";
        private static string Port = "5432";

        static void Main(string[] args)
        {
            // Build connection string using parameters from portal
            //
            string connString =
                String.Format(
                    "Server={0}; User Id={1}; Database={2}; Port={3}; Password={4};",
                    Host,
                    User,
                    DBname,
                    Port,
                    Password);

            var conn = new NpgsqlConnection(connString);

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText =
            String.Format("UPDATE inventory SET quantity = {0} WHERE name = {1};",
                200,
                "\'banana\'"
                );

            int nRows = command.ExecuteNonQuery();
            Console.Out.WriteLine(String.Format("Number of rows updated={0}", nRows));

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}
```


## <a name="delete-data"></a><span data-ttu-id="18911-154">Удаление данных</span><span class="sxs-lookup"><span data-stu-id="18911-154">Delete data</span></span>
<span data-ttu-id="18911-155">Используйте следующие hello кода tooconnect и чтения данных с помощью hello **удалить** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="18911-155">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

 <span data-ttu-id="18911-156">Hello код использует класс NpgsqlCommand с методом [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish tooPostgreSQL соединения.</span><span class="sxs-lookup"><span data-stu-id="18911-156">hello code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish a connection tooPostgreSQL.</span></span> <span data-ttu-id="18911-157">Затем hello кода использует метод [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), устанавливает свойства CommandText hello и вызывает метод [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) toorun hello базы данных команды.</span><span class="sxs-lookup"><span data-stu-id="18911-157">Then hello code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), sets hello CommandText property, and calls method [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) toorun hello database commands.</span></span>

<span data-ttu-id="18911-158">Замените параметры узла, DBName, пользователя и пароль hello значениями hello, указанный при создании hello сервера и базы данных.</span><span class="sxs-lookup"><span data-stu-id="18911-158">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Npgsql;

namespace Driver
{
    public class AzurePostgresDelete
    {
        // Obtain connection string information from hello portal
        //
        private static string Host = "mypgserver-20170401.postgres.database.azure.com";
        private static string User = "mylogin@mypgserver-20170401";
        private static string DBname = "mypgsqldb";
        private static string Password = "<server_admin_password>";
        private static string Port = "5432";

        static void Main(string[] args)
        {
            // Build connection string using parameters from portal
            //
            string connString =
                String.Format(
                    "Server={0}; User Id={1}; Database={2}; Port={3}; Password={4};",
                    Host,
                    User,
                    DBname,
                    Port,
                    Password);

            var conn = new NpgsqlConnection(connString);

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText =
            String.Format("DELETE FROM inventory WHERE name = {0};",
                "\'orange\'");
            int nRows = command.ExecuteNonQuery();
            Console.Out.WriteLine(String.Format("Number of rows deleted={0}", nRows));

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="18911-159">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="18911-159">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="18911-160">Перенос базы данных с помощью экспорта и импорта</span><span class="sxs-lookup"><span data-stu-id="18911-160">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
