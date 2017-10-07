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
# <a name="azure-database-for-mysql-use-connectorc-tooconnect-and-query-data"></a>База данных Azure для MySQL: tooconnect и запрашивают данные, использовать соединитель/C++
Это краткое руководство демонстрирует, как tooconnect tooan Azure этой базы данных MySQL с помощью приложения C++. Показано, как tooquery инструкций SQL toouse, вставка, обновление и удаление данных в базе данных hello. Hello в этой статье предполагается, что вы знакомы с разработка с использованием C++ и наличие новых tooworking с базой данных Azure для MySQL.

## <a name="prerequisites"></a>Предварительные требования
Это краткое руководство использует ресурсы hello, созданные в любой из этих руководствах по в качестве отправной точки.
- [Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Создание сервера базы данных Azure для MySQL с помощью портала Azure)
- [Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md) (Создание сервера базы данных Azure для MySQL с помощью Azure CLI)

Также вам потребуется:
- установить [.NET Framework](https://www.microsoft.com/net/download);
- установить [Visual Studio](https://www.visualstudio.com/downloads/);
- установить [MySQL Connector/C++](https://dev.mysql.com/downloads/connector/cpp/); 
- установить [Boost](http://www.boost.org/).

## <a name="install-visual-studio-and-net"></a>Установка Visual Studio и .NET
Hello в этом разделе предполагается, что вы знакомы с разработка с использованием .NET.

### <a name="windows"></a>**Windows**
1. Установите Visual Studio Community 2017, полнофункциональную расширяемую бесплатную среду IDE для создания современных приложений под Android, iOS, Windows, а также веб-приложений, приложений базы данных и облачных служб. Можно установить либо hello полной версии .NET Framework, либо просто .NET Core. фрагменты кода Hello в hello краткое руководство работать с. Если уже установлены на компьютере Visual Studio, пропустите следующие два шага hello.
   - Загрузите hello [установщик Visual Studio 2017 г](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15). 
   - Запустите установщик hello и следуйте hello установки приглашения toocomplete hello установки.

### <a name="configure-visual-studio"></a>**Настройка Visual Studio**
1. Из Visual Studio, проект свойство > Свойства конфигурации > C/C++ > компоновщика > Общие > Дополнительные каталоги библиотек, добавьте каталог lib\opt hello (т. е.: C:\Program Files (x86) \MySQL\MySQL C++ соединитель 1.1.9\lib\opt) hello c ++ соединитель.
2. В Visual Studio последовательно выберите элементы "Свойство проекта" > "Свойства конфигурации" > C/C++ > "Общие" > "Дополнительные каталоги включаемых файлов".
   - Добавьте каталог include/ соединителя C++ (например, C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\include\)
   - Добавьте корневой каталог библиотеки Boost (например, C:\boost_1_64_0\)
3. В Visual Studio проекта свойство > Свойства конфигурации > C/C++ > компоновщика > входных данных > дополнительных зависимостей, добавьте mysqlcppconn.lib в поле текста hello
4. Либо mysqlcppconn.dll копии из hello c ++ соединителя папку библиотеки в шаге 3 toohello же каталоге, что исполняемый файл приложения hello или добавить его toohello переменной среды, чтобы приложения могли найти его.

## <a name="get-connection-information"></a>Получение сведений о подключении
Получите toohello tooconnect базы данных Azure для hello подключения сведения, необходимые для MySQL. Необходимо hello server полное имя и учетные данные входа.

1. Войдите в toohello [портал Azure](https://portal.azure.com/).
2. Hello левого меню на портале Azure, щелкните **все ресурсы** и выполните поиск сервера hello, вы создали, таких как **myserver4demo**.
3. Щелкните имя сервера hello.
4. Выберите hello server **свойства** страницы. Запишите hello **имя сервера** и **имя входа администратора сервера**.
 ![Имя сервера базы данных Azure для MySQL](./media/connect-cpp/1_server-properties-name-login.png)
5. Если вы забыли учетные данные входа сервера, перейдите toohello **Обзор** страница hello tooview: имя пользователя администратора сервера и, при необходимости переустановить пароль hello.

## <a name="connect-create-table-and-insert-data"></a>Подключение, создание таблицы и вставка данных
Используйте следующие hello кода tooconnect и загружать данные при помощи hello **CREATE TABLE** и **INSERT INTO** инструкции SQL. Hello код использует класс sql::Driver с hello connect() метод tooestablish tooMySQL соединения. Затем hello код использует метод createStatement() и execute() toorun hello команд базы данных. 

Замените параметры узла, DBName, пользователя и пароль hello значениями hello, указанный при создании hello сервера и базы данных. 

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

## <a name="read-data"></a>Считывание данных

Используйте следующие hello кода tooconnect и чтения данных с помощью hello **ВЫБЕРИТЕ** инструкции SQL. Hello код использует класс sql::Driver с hello connect() метод tooestablish tooMySQL соединения. Затем hello код использует метод prepareStatement() и executeQuery() toorun hello выбрать команды. Наконец кода hello использует записи toohello tooadvance next() в результатах hello. Затем код hello использует getInt() getString() tooparse hello значения и в записи hello.

Замените параметры узла, DBName, пользователя и пароль hello значениями hello, указанный при создании hello сервера и базы данных. 

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

## <a name="update-data"></a>Обновление данных
Используйте следующие hello кода tooconnect и чтения данных с помощью hello **обновление** инструкции SQL. Hello код использует класс sql::Driver с hello connect() метод tooestablish tooMySQL соединения. Затем hello код использует метод prepareStatement() и executeQuery() toorun hello команды обновления. 

Замените параметры узла, DBName, пользователя и пароль hello значениями hello, указанный при создании hello сервера и базы данных. 

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


## <a name="delete-data"></a>Удаление данных
Используйте следующие hello кода tooconnect и чтения данных с помощью hello **удалить** инструкции SQL. Hello код использует класс sql::Driver с hello connect() метод tooestablish tooMySQL соединения. Затем hello код использует метод prepareStatement() executeQuery() toorun hello команд и удаления.

Замените параметры узла, DBName, пользователя и пароль hello значениями hello, указанный при создании hello сервера и базы данных. 

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

## <a name="next-steps"></a>Дальнейшие действия
> [!div class="nextstepaction"]
> [Перенести вашей tooAzure базы данных MySQL базы данных MySQL с помощью дампа и восстановления](concepts-migrate-dump-restore.md)
