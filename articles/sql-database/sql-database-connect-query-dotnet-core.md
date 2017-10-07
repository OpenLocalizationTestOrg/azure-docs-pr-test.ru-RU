---
title: ".NET Core aaaUse tooquery базы данных SQL Azure | Документы Microsoft"
description: "В этом разделе показано, как toouse .NET Core toocreate программа, которая соединяет tooan базы данных SQL Azure и запросов с помощью инструкций Transact-SQL."
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
ms.openlocfilehash: 2d10c407f44f43b6baa3bf337cdd1173d9c9c35f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-net-core-c-tooquery-an-azure-sql-database"></a>Использовать tooquery .NET Core (C#) из базы данных Azure SQL

В этом учебнике быстрого запуска показано как toouse [.NET Core](https://www.microsoft.com/net/) на tooconnect программа tooan Azure SQL для Windows, Linux и macOS toocreate C# база данных и использовать данные tooquery инструкций Transact-SQL.

## <a name="prerequisites"></a>Предварительные требования

toocomplete этом краткое руководство по началу работы, убедитесь, что у вас есть следующие hello:

- База данных SQL Azure. В этом кратком руководстве использует ресурсы hello, созданные в одном из этих краткие руководства: 

   - [Создание базы данных с помощью портала](sql-database-get-started-portal.md)
   - [Создание базы данных SQL Azure и отправка к ней запросов с помощью Azure CLI](sql-database-get-started-cli.md)
   - [Создание базы данных с помощью PowerShell](sql-database-get-started-powershell.md)

- Объект [правила брандмауэра уровня сервера](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) для hello общедоступный IP-адрес компьютера hello, используйте для этого краткого руководства.
- Убедитесь, что установлен [.NET Core для вашей операционной системы](https://www.microsoft.com/net/core). 

## <a name="sql-server-connection-information"></a>Сведения о подключении SQL Server

Получите базу данных Azure SQL toohello tooconnect в сведения, необходимые подключения hello. Необходимо будет hello полное имя сервера, имя базы данных и сведения об имени входа в следующих процедурах hello.

1. Войдите в toohello [портал Azure](https://portal.azure.com/).
2. Выберите **баз данных SQL** hello левом меню и выберите базу данных на hello **баз данных SQL** страницы. 
3. На hello **Обзор** страницу для базы данных, просмотрите hello полное доменное имя сервера, как показано в hello после изображения. Можно навести на toobring имя сервера hello копирование hello **щелкните toocopy** параметр. 

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. Если вы забыли учетные данные входа для сервера базы данных SQL Azure, перейдите toohello базы данных SQL server tooview hello server admin имя страницы. При необходимости можно сбросить пароль hello.

5. Щелкните **Показать строки подключения к базам данных**.

6. Просмотрите hello завершения **ADO.NET** строку подключения.

    ![Строка подключения по протоколу ADO.NET](./media/sql-database-connect-query-dotnet/adonet-connection-string.png)

> [!IMPORTANT]
> Необходимо иметь правила брандмауэра на месте для hello общедоступный IP-адрес hello компьютера, на котором выполняется этот учебник. Если вы на другом компьютере или другой общий IP-адрес, создайте [правило брандмауэра уровня сервера с помощью портала Azure "hello"](sql-database-get-started-portal.md#create-a-server-level-firewall-rule). 
>
  
## <a name="create-a-new-net-project"></a>Создание проекта .NET

1. Откройте командную строку и создайте папку с именем *sqltest*. Перейдите в папку toohello, создаваемых и запускаемых hello следующую команду:

    ```
    dotnet new console
    ```

2. Откройте ***sqltest.csproj*** с помощью любого текстового редактора и добавьте System.Data.SqlClient в качестве зависимости с помощью hello, следующий код:

    ```xml
    <ItemGroup>
        <PackageReference Include="System.Data.SqlClient" Version="4.3.0" />
    </ItemGroup>
    ```

## <a name="insert-code-tooquery-sql-database"></a>Вставьте код базы данных SQL tooquery

1. В среде разработки или в предпочитаемом текстовом редакторе откройте **Program.cs**.

2. Замените содержимое hello hello ниже программный код и добавить hello соответствующие значения для сервера, базы данных, пользователя и пароль.

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

## <a name="run-hello-code"></a>Выполнение кода hello

1. Hello командной строки выполните следующие команды hello.

   ```csharp
   dotnet restore
   dotnet run
   ```

2. Убедитесь, что возвращаются первые 20 строк hello и закройте окно приложения hello.


## <a name="next-steps"></a>Дальнейшие действия

- [Начало работы с .NET Core в Windows и Linux/macOS hello командной строки](/dotnet/core/tutorials/using-with-xplat-cli).
- Узнайте, каким образом слишком[подключения и запроса к базе данных Azure SQL с помощью Visual Studio и hello .NET framework](sql-database-connect-query-dotnet-visual-studio.md).  
- Узнайте, каким образом слишком[проектирование первой базы данных Azure SQL с помощью среды SSMS](sql-database-design-first-database.md) или [проектирование первой базы данных Azure SQL с помощью .NET](sql-database-design-first-database-csharp.md).
- Дополнительные сведения о .NET см. в [этой документации](https://docs.microsoft.com/dotnet/).
