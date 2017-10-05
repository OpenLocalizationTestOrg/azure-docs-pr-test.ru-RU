---
title: "Подключение к базе данных Azure для MySQL с помощью C++ | Документация Майкрософт"
description: "В этом кратком руководстве представлен пример кода C++, который можно использовать для подключения к базе данных Azure для MySQL и запроса данных из нее."
services: mysql
author: seanli1988
ms.author: seal
manager: janders
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: C++
ms.topic: hero-article
ms.date: 08/03/2017
ms.openlocfilehash: 63388b83b913d95136140fa4c56af0dbebbdad81
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-database-for-mysql-use-connectorc-to-connect-and-query-data"></a><span data-ttu-id="b92ba-103">База данных Azure для MySQL: подключение и запрос данных с помощью Connector/C++</span><span class="sxs-lookup"><span data-stu-id="b92ba-103">Azure Database for MySQL: Use Connector/C++ to connect and query data</span></span>
<span data-ttu-id="b92ba-104">В этом кратком руководстве объясняется, как подключиться к базе данных Azure для MySQL с помощью приложения C++.</span><span class="sxs-lookup"><span data-stu-id="b92ba-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using a C++ application.</span></span> <span data-ttu-id="b92ba-105">Здесь также показано, как использовать инструкции SQL для запроса, вставки, обновления и удаления данных в базе данных.</span><span class="sxs-lookup"><span data-stu-id="b92ba-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="b92ba-106">В этой статье предполагается, что у вас уже есть опыт разработки на C++ и вы только начали работу с базой данных Azure для MySQL.</span><span class="sxs-lookup"><span data-stu-id="b92ba-106">The steps in this article assume that you are familiar with developing using C++, and that you are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b92ba-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b92ba-107">Prerequisites</span></span>
<span data-ttu-id="b92ba-108">В качестве отправной точки в этом кратком руководстве используются ресурсы, созданные в соответствии со следующими материалами:</span><span class="sxs-lookup"><span data-stu-id="b92ba-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- <span data-ttu-id="b92ba-109">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Создание сервера базы данных Azure для MySQL с помощью портала Azure)</span><span class="sxs-lookup"><span data-stu-id="b92ba-109">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md)</span></span>
- <span data-ttu-id="b92ba-110">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md) (Создание сервера базы данных Azure для MySQL с помощью Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="b92ba-110">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md)</span></span>

<span data-ttu-id="b92ba-111">Также вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="b92ba-111">You also need to:</span></span>
- <span data-ttu-id="b92ba-112">установить [.NET Framework](https://www.microsoft.com/net/download);</span><span class="sxs-lookup"><span data-stu-id="b92ba-112">Install [.NET Framework](https://www.microsoft.com/net/download)</span></span>
- <span data-ttu-id="b92ba-113">установить [Visual Studio](https://www.visualstudio.com/downloads/);</span><span class="sxs-lookup"><span data-stu-id="b92ba-113">Install [Visual Studio](https://www.visualstudio.com/downloads/)</span></span>
- <span data-ttu-id="b92ba-114">установить [MySQL Connector/C++](https://dev.mysql.com/downloads/connector/cpp/);</span><span class="sxs-lookup"><span data-stu-id="b92ba-114">Install [MySQL Connector/C++](https://dev.mysql.com/downloads/connector/cpp/)</span></span> 
- <span data-ttu-id="b92ba-115">установить [Boost](http://www.boost.org/).</span><span class="sxs-lookup"><span data-stu-id="b92ba-115">Install [Boost](http://www.boost.org/)</span></span>

## <a name="install-visual-studio-and-net"></a><span data-ttu-id="b92ba-116">Установка Visual Studio и .NET</span><span class="sxs-lookup"><span data-stu-id="b92ba-116">Install Visual Studio and .NET</span></span>
<span data-ttu-id="b92ba-117">В этом разделе предполагается, что у вас уже есть опыт разработки с использованием .NET.</span><span class="sxs-lookup"><span data-stu-id="b92ba-117">The steps in this section assume that you are familiar with developing using .NET.</span></span>

### <a name="windows"></a><span data-ttu-id="b92ba-118">**Windows**</span><span class="sxs-lookup"><span data-stu-id="b92ba-118">**Windows**</span></span>
1. <span data-ttu-id="b92ba-119">Установите Visual Studio Community 2017, полнофункциональную расширяемую бесплатную среду IDE для создания современных приложений под Android, iOS, Windows, а также веб-приложений, приложений базы данных и облачных служб.</span><span class="sxs-lookup"><span data-stu-id="b92ba-119">Install Visual Studio 2017 Community, which is a full featured, extensible, free IDE for creating modern applications for Android, iOS, Windows, as well as web & database applications and cloud services.</span></span> <span data-ttu-id="b92ba-120">Вы можете установить полную версию .NET Framework или только .NET Core.</span><span class="sxs-lookup"><span data-stu-id="b92ba-120">You can install either the full .NET Framework or just .NET Core.</span></span> <span data-ttu-id="b92ba-121">Фрагменты кода в кратком руководстве работают с любой из них.</span><span class="sxs-lookup"><span data-stu-id="b92ba-121">The code snippets in the Quickstart work with either.</span></span> <span data-ttu-id="b92ba-122">Если среда Visual Studio уже установлена на вашем компьютере, то вы можете пропустить следующие два шага.</span><span class="sxs-lookup"><span data-stu-id="b92ba-122">If you already have Visual Studio installed on your machine, skip the next two steps.</span></span>
   - <span data-ttu-id="b92ba-123">Скачайте [установщик Visual Studio 2017](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15).</span><span class="sxs-lookup"><span data-stu-id="b92ba-123">Download the [Visual Studio 2017 installer](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15).</span></span> 
   - <span data-ttu-id="b92ba-124">Запустите установщик и выполните указанные действия, чтобы завершить установку.</span><span class="sxs-lookup"><span data-stu-id="b92ba-124">Run the installer and follow the installation prompts to complete the installation.</span></span>

### <a name="configure-visual-studio"></a><span data-ttu-id="b92ba-125">**Настройка Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="b92ba-125">**Configure Visual Studio**</span></span>
1. <span data-ttu-id="b92ba-126">В Visual Studio последовательно выберите элементы "Свойство проекта" > "Свойства конфигурации" > C/C++ > "Компоновщик" > "Общие" > "Дополнительные каталоги библиотек" и добавьте каталог lib\opt соединителя C++ (например, C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\lib\opt).</span><span class="sxs-lookup"><span data-stu-id="b92ba-126">From Visual Studio, project property > configuration properties > C/C++ > linker > general > additional library directories, add the lib\opt directory (i.e.: C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\lib\opt) of the c++ connector.</span></span>
2. <span data-ttu-id="b92ba-127">В Visual Studio последовательно выберите элементы "Свойство проекта" > "Свойства конфигурации" > C/C++ > "Общие" > "Дополнительные каталоги включаемых файлов".</span><span class="sxs-lookup"><span data-stu-id="b92ba-127">From Visual Studio, project property > configuration properties > C/C++ > general > additional include directories</span></span>
   - <span data-ttu-id="b92ba-128">Добавьте каталог include/ соединителя C++ (например, C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\include\)</span><span class="sxs-lookup"><span data-stu-id="b92ba-128">Add include/ directory of c++ connector (i.e.: C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\include\)</span></span>
   - <span data-ttu-id="b92ba-129">Добавьте корневой каталог библиотеки Boost (например, C:\boost_1_64_0\)</span><span class="sxs-lookup"><span data-stu-id="b92ba-129">Add Boost library's root directory (i.e.: C:\boost_1_64_0\)</span></span>
3. <span data-ttu-id="b92ba-130">В Visual Studio последовательно выберите "Свойство проекта" > "Свойства конфигурации" > C/C++ > "Компоновщик" > "Ввод" > "Дополнительные зависимости" и добавьте mysqlcppconn.lib в текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="b92ba-130">From Visual Studio, project property > configuration properties > C/C++ > linker > Input > Additional Dependencies, add mysqlcppconn.lib into the text field</span></span>
4. <span data-ttu-id="b92ba-131">Скопируйте файл mysqlcppconn.dll из папки библиотеки соединителя C++, указанной на шаге 3, в каталог, где хранится исполняемый файл приложения, или добавьте его в переменную среды, чтобы приложение смогло найти его.</span><span class="sxs-lookup"><span data-stu-id="b92ba-131">Either copy mysqlcppconn.dll from the c++ connector library folder in step 3 to the same directory as the application executable or add it to the environment variable so your application can find it.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="b92ba-132">Получение сведений о подключении</span><span class="sxs-lookup"><span data-stu-id="b92ba-132">Get connection information</span></span>
<span data-ttu-id="b92ba-133">Получите сведения о подключении, необходимые для подключения к базе данных Azure.для MySQL.</span><span class="sxs-lookup"><span data-stu-id="b92ba-133">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="b92ba-134">Вам потребуется полное имя сервера и учетные данные для входа.</span><span class="sxs-lookup"><span data-stu-id="b92ba-134">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="b92ba-135">Войдите на [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b92ba-135">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="b92ba-136">В меню слева на портале Azure щелкните **Все ресурсы** и выполните поиск по имени созданного сервера, например **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="b92ba-136">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="b92ba-137">Щелкните имя сервера.</span><span class="sxs-lookup"><span data-stu-id="b92ba-137">Click the server name.</span></span>
4. <span data-ttu-id="b92ba-138">Откройте страницу **свойств** сервера.</span><span class="sxs-lookup"><span data-stu-id="b92ba-138">Select the server's **Properties** page.</span></span> <span data-ttu-id="b92ba-139">Запишите значения **имени сервера** и **имени для входа администратора сервера**.</span><span class="sxs-lookup"><span data-stu-id="b92ba-139">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="b92ba-140">![Имя сервера базы данных Azure для MySQL](./media/connect-cpp/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="b92ba-140">![Azure Database for MySQL server name](./media/connect-cpp/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="b92ba-141">Если вы забыли данные для входа на сервер, перейдите на страницу **Обзор**, чтобы просмотреть имя администратора сервера и при необходимости сбросить пароль.</span><span class="sxs-lookup"><span data-stu-id="b92ba-141">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="b92ba-142">Подключение, создание таблицы и вставка данных</span><span class="sxs-lookup"><span data-stu-id="b92ba-142">Connect, create table, and insert data</span></span>
<span data-ttu-id="b92ba-143">Используйте приведенный ниже код для подключения и загрузки данных с помощью инструкций SQL **CREATE TABLE** и **INSERT INTO**.</span><span class="sxs-lookup"><span data-stu-id="b92ba-143">Use the following code to connect and load the data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span> <span data-ttu-id="b92ba-144">В коде используется класс sql::Driver с методом connect(), чтобы установить подключение к MySQL.</span><span class="sxs-lookup"><span data-stu-id="b92ba-144">The code uses sql::Driver class with the connect() method to establish a connection to MySQL.</span></span> <span data-ttu-id="b92ba-145">Затем код использует методы createStatement() и execute() для выполнения команд базы данных.</span><span class="sxs-lookup"><span data-stu-id="b92ba-145">Then the code uses method createStatement() and execute() to run the database commands.</span></span> 

<span data-ttu-id="b92ba-146">Замените значения параметров Host, DBName, User и Password значениями, указанными при создании сервера и базы данных.</span><span class="sxs-lookup"><span data-stu-id="b92ba-146">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```c++
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::Statement *stmt;
    sql::PreparedStatement *pstmt;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in the code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect to database. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }

    stmt = con>createStatement();
    stmt>execute("DROP TABLE IF EXISTS inventory");
    cout << "Finished dropping table (if existed)" << endl;
    stmt>execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);");
    cout << "Finished creating table" << endl;
    delete stmt;

    pstmt = con>prepareStatement("INSERT INTO inventory(name, quantity) VALUES(?,?)");
    pstmt>setString(1, "banana");
    pstmt>setInt(2, 150);
    pstmt>execute();
    cout << "One row inserted." << endl;

    pstmt>setString(1, "orange");
    pstmt>setInt(2, 154);
    pstmt>execute();
    cout << "One row inserted." << endl;

    pstmt>setString(1, "apple");
    pstmt>setInt(2, 100);
    pstmt>execute();
    cout << "One row inserted." << endl;
    
    delete pstmt;   
    delete con;
    system("pause");
    return 0;

```

## <a name="read-data"></a><span data-ttu-id="b92ba-147">Считывание данных</span><span class="sxs-lookup"><span data-stu-id="b92ba-147">Read data</span></span>

<span data-ttu-id="b92ba-148">Используйте указанный ниже код с инструкцией SQL **SELECT** для подключения и чтения данных.</span><span class="sxs-lookup"><span data-stu-id="b92ba-148">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="b92ba-149">В коде используется класс sql::Driver с методом connect(), чтобы установить подключение к MySQL.</span><span class="sxs-lookup"><span data-stu-id="b92ba-149">The code uses sql::Driver class with the connect() method to establish a connection to MySQL.</span></span> <span data-ttu-id="b92ba-150">Затем код использует методы prepareStatement() и executeQuery() для выполнения команд SELECT.</span><span class="sxs-lookup"><span data-stu-id="b92ba-150">Then the code uses method prepareStatement() and executeQuery() to run the select commands.</span></span> <span data-ttu-id="b92ba-151">Наконец, код использует метод next() для перехода к записям в итоговом наборе.</span><span class="sxs-lookup"><span data-stu-id="b92ba-151">Finally the code uses next() to advance to the records in the results.</span></span> <span data-ttu-id="b92ba-152">Затем используются методы getInt() и getString() для анализа значений в записи.</span><span class="sxs-lookup"><span data-stu-id="b92ba-152">Then the code uses getInt() and getString() to parse the values in the record.</span></span>

<span data-ttu-id="b92ba-153">Замените значения параметров Host, DBName, User и Password значениями, указанными при создании сервера и базы данных.</span><span class="sxs-lookup"><span data-stu-id="b92ba-153">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```csharp
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/resultset.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::PreparedStatement *pstmt;
    sql::ResultSet *result;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in the code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect to database. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }   

//  select  
    pstmt = con>prepareStatement("SELECT * FROM inventory;");
    result = pstmt>executeQuery();  
    
    while (result>next())
        printf("Reading from table=(%d, %s, %d)\n", result>getInt(1), result>getString(2).c_str(), result>getInt(3));   
    
    delete result;
    delete pstmt;   
    delete con;
    system("pause");
    return 0;
}
```

## <a name="update-data"></a><span data-ttu-id="b92ba-154">Обновление данных</span><span class="sxs-lookup"><span data-stu-id="b92ba-154">Update data</span></span>
<span data-ttu-id="b92ba-155">Используйте указанный ниже код с инструкцией SQL **UPDATE** для подключения и чтения данных.</span><span class="sxs-lookup"><span data-stu-id="b92ba-155">Use the following code to connect and read the data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="b92ba-156">В коде используется класс sql::Driver с методом connect(), чтобы установить подключение к MySQL.</span><span class="sxs-lookup"><span data-stu-id="b92ba-156">The code uses sql::Driver class with the connect() method to establish a connection to MySQL.</span></span> <span data-ttu-id="b92ba-157">Затем код использует методы prepareStatement() и executeQuery() для выполнения команд UPDATE.</span><span class="sxs-lookup"><span data-stu-id="b92ba-157">Then the code uses method prepareStatement() and executeQuery() to run the update commands.</span></span> 

<span data-ttu-id="b92ba-158">Замените значения параметров Host, DBName, User и Password значениями, указанными при создании сервера и базы данных.</span><span class="sxs-lookup"><span data-stu-id="b92ba-158">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```csharp
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::PreparedStatement *pstmt;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in the code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect to database. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }   

    //update
    pstmt = con>prepareStatement("UPDATE inventory SET quantity = ? WHERE name = ?");
    pstmt>setInt(1, 200);
    pstmt>setString(2, "banana");
    pstmt>executeQuery();
    printf("Row updated\n");
    
    delete con;
    delete pstmt;
    system("pause");
    return 0;
}
```


## <a name="delete-data"></a><span data-ttu-id="b92ba-159">Удаление данных</span><span class="sxs-lookup"><span data-stu-id="b92ba-159">Delete data</span></span>
<span data-ttu-id="b92ba-160">Используйте указанный ниже код с инструкцией SQL **DELETE** для подключения и чтения данных.</span><span class="sxs-lookup"><span data-stu-id="b92ba-160">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> <span data-ttu-id="b92ba-161">В коде используется класс sql::Driver с методом connect(), чтобы установить подключение к MySQL.</span><span class="sxs-lookup"><span data-stu-id="b92ba-161">The code uses sql::Driver class with the connect() method to establish a connection to MySQL.</span></span> <span data-ttu-id="b92ba-162">Затем код использует методы prepareStatement() и executeQuery() для выполнения команд DELETE.</span><span class="sxs-lookup"><span data-stu-id="b92ba-162">Then the code uses method prepareStatement() and executeQuery() to run the delete commands.</span></span>

<span data-ttu-id="b92ba-163">Замените значения параметров Host, DBName, User и Password значениями, указанными при создании сервера и базы данных.</span><span class="sxs-lookup"><span data-stu-id="b92ba-163">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```csharp
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/resultset.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::PreparedStatement *pstmt;
    sql::ResultSet *result;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in the code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect to database. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }
        
    //delete
    pstmt = con>prepareStatement("DELETE FROM inventory WHERE name = ?");
    pstmt>setString(1, "orange");
    result = pstmt>executeQuery();
    printf("Row deleted\n");    
    
    delete pstmt;
    delete con;
    delete result;
    system("pause");
    return 0;
}
```

## <a name="next-steps"></a><span data-ttu-id="b92ba-164">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b92ba-164">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="b92ba-165">Перенос базы данных MySQL в базу данных Azure для MySQL с помощью резервного копирования и восстановления</span><span class="sxs-lookup"><span data-stu-id="b92ba-165">Migrate your MySQL database to Azure Database for MySQL using dump and restore</span></span>](concepts-migrate-dump-restore.md)
