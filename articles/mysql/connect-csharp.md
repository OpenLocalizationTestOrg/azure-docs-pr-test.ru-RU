---
title: "Подключение tooAzure базы данных MySQL в C# | Документы Microsoft"
description: "Это краткое руководство содержит C# (.NET). пример кода можно использовать tooconnect и запроса данных из базы данных Azure для MySQL."
services: MySQL
author: seanli1988
ms.author: seal
manager: janders
editor: jasonwhowell
ms.service: MySQL-database
ms.custom: mvc
ms.devlang: csharp
ms.topic: hero-article
ms.date: 07/10/2017
ms.openlocfilehash: 0dca98186199a40ef9cc592b93c3b2e815260273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-net-c-tooconnect-and-query-data"></a><span data-ttu-id="3c3fb-103">База данных Azure для MySQL: tooconnect и запрашивают данные, используйте .NET (C#)</span><span class="sxs-lookup"><span data-stu-id="3c3fb-103">Azure Database for MySQL: Use .NET (C#) tooconnect and query data</span></span>
<span data-ttu-id="3c3fb-104">Это краткое руководство демонстрирует, как tooconnect tooan Azure этой базы данных MySQL с помощью приложения C#.</span><span class="sxs-lookup"><span data-stu-id="3c3fb-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using a C# application.</span></span> <span data-ttu-id="3c3fb-105">Показано, как tooquery инструкций SQL toouse, вставка, обновление и удаление данных в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="3c3fb-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="3c3fb-106">Hello в этой статье предполагается, что вы знакомы с разработка с использованием C#, а новый tooworking с базой данных Azure для MySQL, которые.</span><span class="sxs-lookup"><span data-stu-id="3c3fb-106">hello steps in this article assume that you are familiar with developing using C#, and that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3c3fb-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3c3fb-107">Prerequisites</span></span>
<span data-ttu-id="3c3fb-108">Это краткое руководство использует ресурсы hello, созданные в любой из этих руководствах по в качестве отправной точки.</span><span class="sxs-lookup"><span data-stu-id="3c3fb-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- <span data-ttu-id="3c3fb-109">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Создание сервера базы данных Azure для MySQL с помощью портала Azure)</span><span class="sxs-lookup"><span data-stu-id="3c3fb-109">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md)</span></span>
- <span data-ttu-id="3c3fb-110">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md) (Создание сервера базы данных Azure для MySQL с помощью Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="3c3fb-110">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md)</span></span>

<span data-ttu-id="3c3fb-111">Также вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="3c3fb-111">You also need to:</span></span>
- <span data-ttu-id="3c3fb-112">Установить [.NET](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="3c3fb-112">Install [.NET](https://www.microsoft.com/net/download).</span></span> <span data-ttu-id="3c3fb-113">Следуйте указаниям hello hello связанной статье tooinstall .NET специально для вашей платформы (Windows, Ubuntu Linux или macOS).</span><span class="sxs-lookup"><span data-stu-id="3c3fb-113">Follow hello steps in hello linked article tooinstall .NET specifically for your platform (Windows, Ubuntu Linux, or macOS).</span></span> 
- <span data-ttu-id="3c3fb-114">Установить [Visual Studio](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="3c3fb-114">Install [Visual Studio](https://www.visualstudio.com/downloads/).</span></span>
- <span data-ttu-id="3c3fb-115">Установить [драйвер ODBC для MySQL](https://dev.mysql.com/downloads/connector/odbc/).</span><span class="sxs-lookup"><span data-stu-id="3c3fb-115">Install [ODBC Driver for MySQL](https://dev.mysql.com/downloads/connector/odbc/).</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="3c3fb-116">Получение сведений о подключении</span><span class="sxs-lookup"><span data-stu-id="3c3fb-116">Get connection information</span></span>
<span data-ttu-id="3c3fb-117">Получите toohello tooconnect базы данных Azure для hello подключения сведения, необходимые для MySQL.</span><span class="sxs-lookup"><span data-stu-id="3c3fb-117">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="3c3fb-118">Необходимо hello server полное имя и учетные данные входа.</span><span class="sxs-lookup"><span data-stu-id="3c3fb-118">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="3c3fb-119">Войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3c3fb-119">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="3c3fb-120">Hello левого меню на портале Azure, щелкните **все ресурсы** и выполните поиск сервера hello, вы создали, таких как **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="3c3fb-120">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="3c3fb-121">Щелкните имя сервера hello.</span><span class="sxs-lookup"><span data-stu-id="3c3fb-121">Click hello server name.</span></span>
4. <span data-ttu-id="3c3fb-122">Выберите hello server **свойства** страницы.</span><span class="sxs-lookup"><span data-stu-id="3c3fb-122">Select hello server's **Properties** page.</span></span> <span data-ttu-id="3c3fb-123">Запишите hello **имя сервера** и **имя входа администратора сервера**.</span><span class="sxs-lookup"><span data-stu-id="3c3fb-123">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="3c3fb-124">![Имя сервера базы данных Azure для MySQL](./media/connect-csharp/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="3c3fb-124">![Azure Database for MySQL server name](./media/connect-csharp/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="3c3fb-125">Если вы забыли учетные данные входа сервера, перейдите toohello **Обзор** страница hello tooview: имя пользователя администратора сервера и, при необходимости переустановить пароль hello.</span><span class="sxs-lookup"><span data-stu-id="3c3fb-125">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="3c3fb-126">Подключение, создание таблицы и вставка данных</span><span class="sxs-lookup"><span data-stu-id="3c3fb-126">Connect, create table, and insert data</span></span>
<span data-ttu-id="3c3fb-127">Используйте следующие hello кода tooconnect и загружать данные при помощи hello **CREATE TABLE** и **INSERT INTO** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="3c3fb-127">Use hello following code tooconnect and load hello data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span> <span data-ttu-id="3c3fb-128">Hello код использует класс ODBC с помощью метода [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish tooMySQL соединения.</span><span class="sxs-lookup"><span data-stu-id="3c3fb-128">hello code uses ODBC class with method [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="3c3fb-129">Затем hello кода использует метод [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), устанавливает свойства CommandText hello и вызывает метод [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) toorun hello базы данных команды.</span><span class="sxs-lookup"><span data-stu-id="3c3fb-129">Then hello code uses method [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), sets hello CommandText property, and calls method [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) toorun hello database commands.</span></span> 

<span data-ttu-id="3c3fb-130">Замените параметры узла, DBName, пользователя и пароль hello значениями hello, указанный при создании hello сервера и базы данных.</span><span class="sxs-lookup"><span data-stu-id="3c3fb-130">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using MySql.Data;
using System.Data.Odbc;

namespace driver
{
    class MySQLCreate
    {
        static void Main(string[] args)
        {
            var conn = new OdbcConnection("DRIVER={MySQL ODBC 5.3 unicode Driver}; Server=myserver4demo.mysql.database.azure.com; Port=3306;" +
            " Database=quickstartdb; Uid=myadmin@myserver4demo; Pwd=server_admin_password; sslverify=0; Option=3;MULTI_STATEMENTS=1");

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
                    @"INSERT INTO inventory (name, quantity) VALUES ({0}, {1});
                    INSERT INTO inventory (name, quantity) VALUES ({2}, {3});
                    INSERT INTO inventory (name, quantity) VALUES ({4}, {5});",
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

## <a name="read-data"></a><span data-ttu-id="3c3fb-131">Считывание данных</span><span class="sxs-lookup"><span data-stu-id="3c3fb-131">Read data</span></span>

<span data-ttu-id="3c3fb-132">Используйте следующие hello кода tooconnect и чтения данных с помощью hello **ВЫБЕРИТЕ** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="3c3fb-132">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="3c3fb-133">Hello код использует класс ODBC с помощью метода [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish tooMySQL соединения.</span><span class="sxs-lookup"><span data-stu-id="3c3fb-133">hello code uses ODBC class with method [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="3c3fb-134">Затем hello кода использует метод [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx) и метод [ExecuteReader()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executereader(v=vs.110).aspx) toorun hello базы данных команды.</span><span class="sxs-lookup"><span data-stu-id="3c3fb-134">Then hello code uses method [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx) and method [ExecuteReader()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executereader(v=vs.110).aspx) toorun hello database commands.</span></span> <span data-ttu-id="3c3fb-135">Здравствуйте, затем код использует [Read()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcdatareader.read(v=vs.110).aspx) tooadvance toohello записей в результатах hello.</span><span class="sxs-lookup"><span data-stu-id="3c3fb-135">Next hello code uses [Read()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcdatareader.read(v=vs.110).aspx) tooadvance toohello records in hello results.</span></span> <span data-ttu-id="3c3fb-136">Затем код hello использует GetInt32 GetString tooparse hello значения и в записи hello.</span><span class="sxs-lookup"><span data-stu-id="3c3fb-136">Then hello code uses GetInt32 and GetString tooparse hello values in hello record.</span></span>

<span data-ttu-id="3c3fb-137">Замените параметры узла, DBName, пользователя и пароль hello значениями hello, указанный при создании hello сервера и базы данных.</span><span class="sxs-lookup"><span data-stu-id="3c3fb-137">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using MySql.Data;
using System.Data.Odbc;


namespace driver
{
    class MySQLRead
    {

        static void Main(string[] args)
        {
            var conn = new OdbcConnection("DRIVER={MySQL ODBC 5.3 unicode Driver}; Server=myserver4demo.mysql.database.azure.com; Port=3306;" +
            " Database=quickstartdb; Uid=myadmin@myserver4demo; Pwd=server_admin_password; sslverify=0; Option=3;MULTI_STATEMENTS=1");

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

## <a name="update-data"></a><span data-ttu-id="3c3fb-138">Обновление данных</span><span class="sxs-lookup"><span data-stu-id="3c3fb-138">Update data</span></span>
<span data-ttu-id="3c3fb-139">Используйте следующие hello кода tooconnect и чтения данных с помощью hello **обновление** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="3c3fb-139">Use hello following code tooconnect and read hello data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="3c3fb-140">Hello код использует класс ODBC с помощью метода [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish tooMySQL соединения.</span><span class="sxs-lookup"><span data-stu-id="3c3fb-140">hello code uses ODBC class with method [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="3c3fb-141">Затем hello кода использует метод [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), устанавливает свойства CommandText hello и вызывает метод [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) toorun hello базы данных команды.</span><span class="sxs-lookup"><span data-stu-id="3c3fb-141">Then hello code uses method [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), sets hello CommandText property, and calls method [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) toorun hello database commands.</span></span>

<span data-ttu-id="3c3fb-142">Замените параметры узла, DBName, пользователя и пароль hello значениями hello, указанный при создании hello сервера и базы данных.</span><span class="sxs-lookup"><span data-stu-id="3c3fb-142">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Data.Odbc;

namespace driver
{
    class MySQLUpdate
    {
        static void Main(string[] args)
        {
            var conn = new OdbcConnection("DRIVER={MySQL ODBC 5.3 unicode Driver}; Server=myserver4demo.mysql.database.azure.com; Port=3306;" +
            " Database=quickstartdb; Uid=myadmin@myserver4demo; Pwd=server_admin_password; sslverify=0; Option=3;MULTI_STATEMENTS=1");

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


## <a name="delete-data"></a><span data-ttu-id="3c3fb-143">Удаление данных</span><span class="sxs-lookup"><span data-stu-id="3c3fb-143">Delete data</span></span>
<span data-ttu-id="3c3fb-144">Используйте следующие hello кода tooconnect и удаления данных с помощью hello **удалить** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="3c3fb-144">Use hello following code tooconnect and delete hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="3c3fb-145">Hello код использует класс ODBC с помощью метода [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish tooMySQL соединения.</span><span class="sxs-lookup"><span data-stu-id="3c3fb-145">hello code uses ODBC class with method [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="3c3fb-146">Затем hello кода использует метод [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), устанавливает свойства CommandText hello и вызывает метод [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) toorun hello базы данных команды.</span><span class="sxs-lookup"><span data-stu-id="3c3fb-146">Then hello code uses method [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), sets hello CommandText property, and calls method [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) toorun hello database commands.</span></span>

<span data-ttu-id="3c3fb-147">Замените параметры узла, DBName, пользователя и пароль hello значениями hello, указанный при создании hello сервера и базы данных.</span><span class="sxs-lookup"><span data-stu-id="3c3fb-147">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Data.Odbc;

namespace driver
{
    class MySQLDelete
    {
        static void Main(string[] args)
        {
            var conn = new OdbcConnection("DRIVER={MySQL ODBC 5.3 unicode Driver}; Server=myserver4demo.mysql.database.azure.com; Port=3306;" +
            " Database=quickstartdb; Uid=myadmin@myserver4demo; Pwd=server_admin_password; sslverify=0; Option=3;MULTI_STATEMENTS=1");

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

## <a name="next-steps"></a><span data-ttu-id="3c3fb-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3c3fb-148">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="3c3fb-149">Перенести вашей tooAzure базы данных MySQL базы данных MySQL с помощью дампа и восстановления</span><span class="sxs-lookup"><span data-stu-id="3c3fb-149">Migrate your MySQL database tooAzure Database for MySQL using dump and restore</span></span>](concepts-migrate-dump-restore.md)
