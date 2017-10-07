---
title: "Подключение tooAzure базы данных MySQL из C++ | Документы Microsoft"
description: "Это краткое руководство содержит пример кода C++ можно использовать tooconnect и запроса данных из базы данных Azure для MySQL."
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
ms.openlocfilehash: d027597bf02b1eacab9b8808957399f6e54e63cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-connectorc-tooconnect-and-query-data"></a><span data-ttu-id="5cb32-103">База данных Azure для MySQL: tooconnect и запрашивают данные, использовать соединитель/C++</span><span class="sxs-lookup"><span data-stu-id="5cb32-103">Azure Database for MySQL: Use Connector/C++ tooconnect and query data</span></span>
<span data-ttu-id="5cb32-104">Это краткое руководство демонстрирует, как tooconnect tooan Azure этой базы данных MySQL с помощью приложения C++.</span><span class="sxs-lookup"><span data-stu-id="5cb32-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using a C++ application.</span></span> <span data-ttu-id="5cb32-105">Показано, как tooquery инструкций SQL toouse, вставка, обновление и удаление данных в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="5cb32-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="5cb32-106">Hello в этой статье предполагается, что вы знакомы с разработка с использованием C++ и наличие новых tooworking с базой данных Azure для MySQL.</span><span class="sxs-lookup"><span data-stu-id="5cb32-106">hello steps in this article assume that you are familiar with developing using C++, and that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5cb32-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5cb32-107">Prerequisites</span></span>
<span data-ttu-id="5cb32-108">Это краткое руководство использует ресурсы hello, созданные в любой из этих руководствах по в качестве отправной точки.</span><span class="sxs-lookup"><span data-stu-id="5cb32-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- <span data-ttu-id="5cb32-109">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Создание сервера базы данных Azure для MySQL с помощью портала Azure)</span><span class="sxs-lookup"><span data-stu-id="5cb32-109">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md)</span></span>
- <span data-ttu-id="5cb32-110">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md) (Создание сервера базы данных Azure для MySQL с помощью Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="5cb32-110">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md)</span></span>

<span data-ttu-id="5cb32-111">Также вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="5cb32-111">You also need to:</span></span>
- <span data-ttu-id="5cb32-112">установить [.NET Framework](https://www.microsoft.com/net/download);</span><span class="sxs-lookup"><span data-stu-id="5cb32-112">Install [.NET Framework](https://www.microsoft.com/net/download)</span></span>
- <span data-ttu-id="5cb32-113">установить [Visual Studio](https://www.visualstudio.com/downloads/);</span><span class="sxs-lookup"><span data-stu-id="5cb32-113">Install [Visual Studio](https://www.visualstudio.com/downloads/)</span></span>
- <span data-ttu-id="5cb32-114">установить [MySQL Connector/C++](https://dev.mysql.com/downloads/connector/cpp/);</span><span class="sxs-lookup"><span data-stu-id="5cb32-114">Install [MySQL Connector/C++](https://dev.mysql.com/downloads/connector/cpp/)</span></span> 
- <span data-ttu-id="5cb32-115">установить [Boost](http://www.boost.org/).</span><span class="sxs-lookup"><span data-stu-id="5cb32-115">Install [Boost](http://www.boost.org/)</span></span>

## <a name="install-visual-studio-and-net"></a><span data-ttu-id="5cb32-116">Установка Visual Studio и .NET</span><span class="sxs-lookup"><span data-stu-id="5cb32-116">Install Visual Studio and .NET</span></span>
<span data-ttu-id="5cb32-117">Hello в этом разделе предполагается, что вы знакомы с разработка с использованием .NET.</span><span class="sxs-lookup"><span data-stu-id="5cb32-117">hello steps in this section assume that you are familiar with developing using .NET.</span></span>

### <a name="windows"></a><span data-ttu-id="5cb32-118">**Windows**</span><span class="sxs-lookup"><span data-stu-id="5cb32-118">**Windows**</span></span>
1. <span data-ttu-id="5cb32-119">Установите Visual Studio Community 2017, полнофункциональную расширяемую бесплатную среду IDE для создания современных приложений под Android, iOS, Windows, а также веб-приложений, приложений базы данных и облачных служб.</span><span class="sxs-lookup"><span data-stu-id="5cb32-119">Install Visual Studio 2017 Community, which is a full featured, extensible, free IDE for creating modern applications for Android, iOS, Windows, as well as web & database applications and cloud services.</span></span> <span data-ttu-id="5cb32-120">Можно установить либо hello полной версии .NET Framework, либо просто .NET Core.</span><span class="sxs-lookup"><span data-stu-id="5cb32-120">You can install either hello full .NET Framework or just .NET Core.</span></span> <span data-ttu-id="5cb32-121">фрагменты кода Hello в hello краткое руководство работать с.</span><span class="sxs-lookup"><span data-stu-id="5cb32-121">hello code snippets in hello Quickstart work with either.</span></span> <span data-ttu-id="5cb32-122">Если уже установлены на компьютере Visual Studio, пропустите следующие два шага hello.</span><span class="sxs-lookup"><span data-stu-id="5cb32-122">If you already have Visual Studio installed on your machine, skip hello next two steps.</span></span>
   - <span data-ttu-id="5cb32-123">Загрузите hello [установщик Visual Studio 2017 г](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15).</span><span class="sxs-lookup"><span data-stu-id="5cb32-123">Download hello [Visual Studio 2017 installer](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15).</span></span> 
   - <span data-ttu-id="5cb32-124">Запустите установщик hello и следуйте hello установки приглашения toocomplete hello установки.</span><span class="sxs-lookup"><span data-stu-id="5cb32-124">Run hello installer and follow hello installation prompts toocomplete hello installation.</span></span>

### <a name="configure-visual-studio"></a><span data-ttu-id="5cb32-125">**Настройка Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="5cb32-125">**Configure Visual Studio**</span></span>
1. <span data-ttu-id="5cb32-126">Из Visual Studio, проект свойство > Свойства конфигурации > C/C++ > компоновщика > Общие > Дополнительные каталоги библиотек, добавьте каталог lib\opt hello (т. е.: C:\Program Files (x86) \MySQL\MySQL C++ соединитель 1.1.9\lib\opt) hello c ++ соединитель.</span><span class="sxs-lookup"><span data-stu-id="5cb32-126">From Visual Studio, project property > configuration properties > C/C++ > linker > general > additional library directories, add hello lib\opt directory (i.e.: C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\lib\opt) of hello c++ connector.</span></span>
2. <span data-ttu-id="5cb32-127">В Visual Studio последовательно выберите элементы "Свойство проекта" > "Свойства конфигурации" > C/C++ > "Общие" > "Дополнительные каталоги включаемых файлов".</span><span class="sxs-lookup"><span data-stu-id="5cb32-127">From Visual Studio, project property > configuration properties > C/C++ > general > additional include directories</span></span>
   - <span data-ttu-id="5cb32-128">Добавьте каталог include/ соединителя C++ (например, C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\include\)</span><span class="sxs-lookup"><span data-stu-id="5cb32-128">Add include/ directory of c++ connector (i.e.: C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\include\)</span></span>
   - <span data-ttu-id="5cb32-129">Добавьте корневой каталог библиотеки Boost (например, C:\boost_1_64_0\)</span><span class="sxs-lookup"><span data-stu-id="5cb32-129">Add Boost library's root directory (i.e.: C:\boost_1_64_0\)</span></span>
3. <span data-ttu-id="5cb32-130">В Visual Studio проекта свойство > Свойства конфигурации > C/C++ > компоновщика > входных данных > дополнительных зависимостей, добавьте mysqlcppconn.lib в поле текста hello</span><span class="sxs-lookup"><span data-stu-id="5cb32-130">From Visual Studio, project property > configuration properties > C/C++ > linker > Input > Additional Dependencies, add mysqlcppconn.lib into hello text field</span></span>
4. <span data-ttu-id="5cb32-131">Либо mysqlcppconn.dll копии из hello c ++ соединителя папку библиотеки в шаге 3 toohello же каталоге, что исполняемый файл приложения hello или добавить его toohello переменной среды, чтобы приложения могли найти его.</span><span class="sxs-lookup"><span data-stu-id="5cb32-131">Either copy mysqlcppconn.dll from hello c++ connector library folder in step 3 toohello same directory as hello application executable or add it toohello environment variable so your application can find it.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="5cb32-132">Получение сведений о подключении</span><span class="sxs-lookup"><span data-stu-id="5cb32-132">Get connection information</span></span>
<span data-ttu-id="5cb32-133">Получите toohello tooconnect базы данных Azure для hello подключения сведения, необходимые для MySQL.</span><span class="sxs-lookup"><span data-stu-id="5cb32-133">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="5cb32-134">Необходимо hello server полное имя и учетные данные входа.</span><span class="sxs-lookup"><span data-stu-id="5cb32-134">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="5cb32-135">Войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5cb32-135">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="5cb32-136">Hello левого меню на портале Azure, щелкните **все ресурсы** и выполните поиск сервера hello, вы создали, таких как **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="5cb32-136">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="5cb32-137">Щелкните имя сервера hello.</span><span class="sxs-lookup"><span data-stu-id="5cb32-137">Click hello server name.</span></span>
4. <span data-ttu-id="5cb32-138">Выберите hello server **свойства** страницы.</span><span class="sxs-lookup"><span data-stu-id="5cb32-138">Select hello server's **Properties** page.</span></span> <span data-ttu-id="5cb32-139">Запишите hello **имя сервера** и **имя входа администратора сервера**.</span><span class="sxs-lookup"><span data-stu-id="5cb32-139">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="5cb32-140">![Имя сервера базы данных Azure для MySQL](./media/connect-cpp/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="5cb32-140">![Azure Database for MySQL server name](./media/connect-cpp/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="5cb32-141">Если вы забыли учетные данные входа сервера, перейдите toohello **Обзор** страница hello tooview: имя пользователя администратора сервера и, при необходимости переустановить пароль hello.</span><span class="sxs-lookup"><span data-stu-id="5cb32-141">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="5cb32-142">Подключение, создание таблицы и вставка данных</span><span class="sxs-lookup"><span data-stu-id="5cb32-142">Connect, create table, and insert data</span></span>
<span data-ttu-id="5cb32-143">Используйте следующие hello кода tooconnect и загружать данные при помощи hello **CREATE TABLE** и **INSERT INTO** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="5cb32-143">Use hello following code tooconnect and load hello data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span> <span data-ttu-id="5cb32-144">Hello код использует класс sql::Driver с hello connect() метод tooestablish tooMySQL соединения.</span><span class="sxs-lookup"><span data-stu-id="5cb32-144">hello code uses sql::Driver class with hello connect() method tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="5cb32-145">Затем hello код использует метод createStatement() и execute() toorun hello команд базы данных.</span><span class="sxs-lookup"><span data-stu-id="5cb32-145">Then hello code uses method createStatement() and execute() toorun hello database commands.</span></span> 

<span data-ttu-id="5cb32-146">Замените параметры узла, DBName, пользователя и пароль hello значениями hello, указанный при создании hello сервера и базы данных.</span><span class="sxs-lookup"><span data-stu-id="5cb32-146">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

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
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
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

## <a name="read-data"></a><span data-ttu-id="5cb32-147">Считывание данных</span><span class="sxs-lookup"><span data-stu-id="5cb32-147">Read data</span></span>

<span data-ttu-id="5cb32-148">Используйте следующие hello кода tooconnect и чтения данных с помощью hello **ВЫБЕРИТЕ** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="5cb32-148">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="5cb32-149">Hello код использует класс sql::Driver с hello connect() метод tooestablish tooMySQL соединения.</span><span class="sxs-lookup"><span data-stu-id="5cb32-149">hello code uses sql::Driver class with hello connect() method tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="5cb32-150">Затем hello код использует метод prepareStatement() и executeQuery() toorun hello выбрать команды.</span><span class="sxs-lookup"><span data-stu-id="5cb32-150">Then hello code uses method prepareStatement() and executeQuery() toorun hello select commands.</span></span> <span data-ttu-id="5cb32-151">Наконец кода hello использует записи toohello tooadvance next() в результатах hello.</span><span class="sxs-lookup"><span data-stu-id="5cb32-151">Finally hello code uses next() tooadvance toohello records in hello results.</span></span> <span data-ttu-id="5cb32-152">Затем код hello использует getInt() getString() tooparse hello значения и в записи hello.</span><span class="sxs-lookup"><span data-stu-id="5cb32-152">Then hello code uses getInt() and getString() tooparse hello values in hello record.</span></span>

<span data-ttu-id="5cb32-153">Замените параметры узла, DBName, пользователя и пароль hello значениями hello, указанный при создании hello сервера и базы данных.</span><span class="sxs-lookup"><span data-stu-id="5cb32-153">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

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
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
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

## <a name="update-data"></a><span data-ttu-id="5cb32-154">Обновление данных</span><span class="sxs-lookup"><span data-stu-id="5cb32-154">Update data</span></span>
<span data-ttu-id="5cb32-155">Используйте следующие hello кода tooconnect и чтения данных с помощью hello **обновление** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="5cb32-155">Use hello following code tooconnect and read hello data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="5cb32-156">Hello код использует класс sql::Driver с hello connect() метод tooestablish tooMySQL соединения.</span><span class="sxs-lookup"><span data-stu-id="5cb32-156">hello code uses sql::Driver class with hello connect() method tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="5cb32-157">Затем hello код использует метод prepareStatement() и executeQuery() toorun hello команды обновления.</span><span class="sxs-lookup"><span data-stu-id="5cb32-157">Then hello code uses method prepareStatement() and executeQuery() toorun hello update commands.</span></span> 

<span data-ttu-id="5cb32-158">Замените параметры узла, DBName, пользователя и пароль hello значениями hello, указанный при создании hello сервера и базы данных.</span><span class="sxs-lookup"><span data-stu-id="5cb32-158">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

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
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
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


## <a name="delete-data"></a><span data-ttu-id="5cb32-159">Удаление данных</span><span class="sxs-lookup"><span data-stu-id="5cb32-159">Delete data</span></span>
<span data-ttu-id="5cb32-160">Используйте следующие hello кода tooconnect и чтения данных с помощью hello **удалить** инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="5cb32-160">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> <span data-ttu-id="5cb32-161">Hello код использует класс sql::Driver с hello connect() метод tooestablish tooMySQL соединения.</span><span class="sxs-lookup"><span data-stu-id="5cb32-161">hello code uses sql::Driver class with hello connect() method tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="5cb32-162">Затем hello код использует метод prepareStatement() executeQuery() toorun hello команд и удаления.</span><span class="sxs-lookup"><span data-stu-id="5cb32-162">Then hello code uses method prepareStatement() and executeQuery() toorun hello delete commands.</span></span>

<span data-ttu-id="5cb32-163">Замените параметры узла, DBName, пользователя и пароль hello значениями hello, указанный при создании hello сервера и базы данных.</span><span class="sxs-lookup"><span data-stu-id="5cb32-163">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

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
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
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

## <a name="next-steps"></a><span data-ttu-id="5cb32-164">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5cb32-164">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="5cb32-165">Перенести вашей tooAzure базы данных MySQL базы данных MySQL с помощью дампа и восстановления</span><span class="sxs-lookup"><span data-stu-id="5cb32-165">Migrate your MySQL database tooAzure Database for MySQL using dump and restore</span></span>](concepts-migrate-dump-restore.md)
