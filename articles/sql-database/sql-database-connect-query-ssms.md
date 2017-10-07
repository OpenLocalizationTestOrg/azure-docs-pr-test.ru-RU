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
# <a name="azure-sql-database-use-sql-server-management-studio-tooconnect-and-query-data"></a>База данных SQL Azure: Использование SQL Server Management Studio tooconnect и запроса данных

[SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) — это интегрированная среда для управления любой инфраструктуры SQL из SQL Server tooSQL базы данных для Microsoft Windows. В этом кратком руководстве показано, как базы данных Azure SQL tooan tooconnect toouse SSMS, а затем tooquery инструкций используйте Transact-SQL, вставки, обновления и удаления данных в базе данных hello. 

## <a name="prerequisites"></a>Предварительные требования

В этом кратком руководстве в качестве отправной точки ресурсов hello создана в одном из этих краткие используется:

- [Создание базы данных с помощью портала](sql-database-get-started-portal.md)
- [Создание базы данных SQL Azure и отправка к ней запросов с помощью Azure CLI](sql-database-get-started-cli.md)
- [Создание базы данных с помощью PowerShell](sql-database-get-started-powershell.md)

Прежде чем начать, убедитесь, что установлен hello новейшую версию [SSMS](https://msdn.microsoft.com/library/mt238290.aspx). 

## <a name="sql-server-connection-information"></a>Сведения о подключении SQL Server

Получите базу данных Azure SQL toohello tooconnect в сведения, необходимые подключения hello. Необходимо будет hello полное имя сервера, имя базы данных и сведения об имени входа в следующих процедурах hello.

1. Войдите в toohello [портал Azure](https://portal.azure.com/).
2. Выберите **баз данных SQL** hello левом меню и выберите базу данных на hello **баз данных SQL** страницы. 
3. На hello **Обзор** страниц для базы данных, просмотрите hello полное имя сервера, как показано в приведенном ниже рисунке hello. Можно навести на toobring имя сервера hello копирование hello **щелкните toocopy** параметр.

   ![Сведения о подключении](./media/sql-database-connect-query-dotnet/server-name.png) 

4. Если вы забыли hello учетные данные для сервера базы данных SQL Azure, перейдите toohello базы данных SQL server страницы tooview hello server с именем admin и, при необходимости сбросить пароль hello. 

## <a name="connect-tooyour-database"></a>Подключение базы данных tooyour

С помощью SQL Server Management Studio tooestablish сервером базы данных SQL Azure tooyour соединения. 

> [!IMPORTANT]
> Логический сервер базы данных SQL Azure прослушивает порт 1433. При попытке tooconnect tooan базы данных SQL Azure логического сервера внутри корпоративного брандмауэра, этот порт должен быть открыт в hello корпоративного брандмауэра для подключения к toosuccessfully вы.
>

1. Откройте среду SQL Server Management Studio.

2. В hello **подключения tooServer** диалогового окна введите hello следующую информацию:

   | Настройка       | Рекомендуемое значение | Описание | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Тип сервера** | Ядро СУБД | Это обязательное значение. |
   | **Server name** (Имя сервера) | Hello полное имя сервера | Hello имя должно быть примерно следующим образом: **mynewserver20170313.database.windows.net**. |
   | **Аутентификация** | проверка подлинности SQL Server | Проверка подлинности SQL — тип hello только проверку подлинности, который мы указали в этом учебнике. |
   | **Имя входа** | Учетная запись администратора сервера Hello | Это учетная запись hello, указанный при создании сервера hello. |
   | **Пароль** | Hello пароль для учетной записи администратора сервера | Это hello пароль, указанный при создании сервера hello. |

   ![подключение tooserver](./media/sql-database-connect-query-ssms/connect.png)  

3. Нажмите кнопку **параметры** в hello **подключения tooserver** диалоговое окно. В hello **подключения toodatabase** введите **mySampleDatabase** базы данных toothis tooconnect.

   ![подключение toodb на сервере](./media/sql-database-connect-query-ssms/options-connect-to-db.png)  

4. Щелкните **Подключить**. Откроется окно обозревателя объектов Hello в среде SSMS. 

   ![подключенный tooserver](./media/sql-database-connect-query-ssms/connected.png)  

5. В обозревателе объектов разверните **баз данных** и разверните **mySampleDatabase** tooview объектов hello в образце hello базы данных.

## <a name="query-data"></a>Запрос данных

Используйте hello следующий код tooquery для hello 20 основных продуктов по категориям, используя hello [ВЫБЕРИТЕ](https://msdn.microsoft.com/library/ms189499.aspx) инструкции Transact-SQL.

1. В обозревателе объектов щелкните правой кнопкой мыши **mySampleDatabase** и выберите пункт **Новый запрос**. Пустое окно запроса, откроется tooyour подключенной базы данных.
2. В окне запроса hello введите приветствия при следующем запросе:

   ```sql
   SELECT pc.Name as CategoryName, p.name as ProductName
   FROM [SalesLT].[ProductCategory] pc
   JOIN [SalesLT].[Product] p
   ON pc.productcategoryid = p.productcategoryid;
   ```

3. На панели инструментов hello, нажмите кнопку **Execute** tooretrieve данные из таблицы Product и ProductCategory hello.

    ![query](./media/sql-database-connect-query-ssms/query.png)

## <a name="insert-data"></a>Добавление данных

Используйте следующие hello кода tooinsert новый продукт SalesLT.Product таблицу hello hello [вставить](https://msdn.microsoft.com/library/ms174335.aspx) инструкции Transact-SQL.

1. В окне запроса hello замените предыдущий запрос hello приветствия при следующем запросе:

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

2. На панели инструментов hello, нажмите кнопку **Execute** tooinsert новую строку в таблице Product hello.

    <img src="./media/sql-database-connect-query-ssms/insert.png" alt="insert" style="width: 780px;" />

## <a name="update-data"></a>Обновление данных

Используйте hello следующий код tooupdate hello новым продуктом, добавленный ранее с помощью hello [обновление](https://msdn.microsoft.com/library/ms177523.aspx) инструкции Transact-SQL.

1. В окне запроса hello замените предыдущий запрос hello приветствия при следующем запросе:

   ```sql
   UPDATE [SalesLT].[Product]
   SET [ListPrice] = 125
   WHERE Name = 'myNewProduct';
   ```

2. На панели инструментов hello, нажмите кнопку **Execute** tooupdate hello указанной строки в таблице Product hello.

    <img src="./media/sql-database-connect-query-ssms/update.png" alt="update" style="width: 780px;" />

## <a name="delete-data"></a>Удаление данных

Используйте hello следующий код toodelete hello новым продуктом, добавленный ранее с помощью hello [удалить](https://msdn.microsoft.com/library/ms189835.aspx) инструкции Transact-SQL.

1. В окне запроса hello замените предыдущий запрос hello приветствия при следующем запросе:

   ```sql
   DELETE FROM [SalesLT].[Product]
   WHERE Name = 'myNewProduct';
   ```

2. На панели инструментов hello, нажмите кнопку **Execute** toodelete hello указанной строки в таблице Product hello.

    <img src="./media/sql-database-connect-query-ssms/delete.png" alt="delete" style="width: 780px;" />

## <a name="next-steps"></a>Дальнейшие действия

- toolearn по созданию и управлению серверами и базами данных с помощью Transact-SQL, в разделе [Дополнительные сведения о базах данных и серверов баз данных SQL Azure](sql-database-servers-databases.md).
- Дополнительные сведения о решении SSMS см. в статье об [использовании SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx).
- tooconnect и запроса с помощью кода Visual Studio, в разделе [подключение и запрос с кодом Visual Studio](sql-database-connect-query-vscode.md).
- tooconnect и запросов с помощью .NET, в разделе [подключение и запрос с помощью .NET](sql-database-connect-query-dotnet.md).
- tooconnect и запрос с использованием PHP, в разделе [подключение и запрос с PHP](sql-database-connect-query-php.md).
- tooconnect и запрос с помощью Node.js, см. [подключение и запрос с Node.js](sql-database-connect-query-nodejs.md).
- tooconnect и запрос с помощью Java, в разделе [подключение и запрос с помощью Java](sql-database-connect-query-java.md).
- tooconnect и запрос с помощью Python, в разделе [подключение и запрос с Python](sql-database-connect-query-python.md).
- tooconnect и запрос, используя Ruby. в разделе [подключение и запрос с Ruby](sql-database-connect-query-ruby.md).
