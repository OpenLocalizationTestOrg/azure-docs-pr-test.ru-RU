---
title: "aaaGet работы с межбазовые запросы (вертикальное секционирование) | Документы Microsoft"
description: "как запрос toouse эластичной базы данных с вертикальное секционирование баз данных"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: e5b44b10-c432-4f96-b20e-08615ff4d5dd
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: torsteng
ms.openlocfilehash: 9e6183268e8bf87e3ac28f502711fcc05a7a3f52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-cross-database-queries-vertical-partitioning-preview"></a>Приступая к работе с межбазовыми запросами (вертикальное секционирование) (предварительная версия)
Запрос эластичной базы данных (Предварительная версия) для базы данных SQL Azure позволяет toorun запросов T-SQL, которые охватывают несколько баз данных с помощью одна точка подключения. В этом разделе также применяется[вертикальное секционирование баз данных](sql-database-elastic-query-vertical-partitioning.md).  

После завершения вы будете: Узнайте, как tooconfigure и использования базы данных SQL Azure tooperform запрос, охватывающих несколько связанных баз данных. 

Дополнительные сведения о функции запросов hello эластичной базы данных см. в разделе [Обзор запросов базы данных SQL Azure эластичной базы данных](sql-database-elastic-query-overview.md). 

## <a name="prerequisites"></a>Предварительные требования

Требуется наличие разрешения ALTER ANY EXTERNAL DATA SOURCE. Это разрешение входит в состав hello разрешение ALTER DATABASE. Разрешения ALTER ANY EXTERNAL DATA SOURCE, необходимые toorefer toohello базового источника данных.

## <a name="create-hello-sample-databases"></a>Создать hello образцы баз данных
toostart с необходимы две базы данных toocreate **клиентов** и **заказов**, Здравствуйте, либо в одной или разных логических серверов.   

Выполните следующие запросы на hello hello **заказов** hello toocreate базы данных **OrderInformation** таблицы и ввода данных образец hello. 

    CREATE TABLE [dbo].[OrderInformation]( 
        [OrderID] [int] NOT NULL, 
        [CustomerID] [int] NOT NULL 
        ) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (123, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (149, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (857, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (321, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (564, 8) 

Теперь, можно выполнить следующий запрос на hello **клиентов** hello toocreate базы данных **сведения о клиенте** таблицы и ввода данных образец hello. 

    CREATE TABLE [dbo].[CustomerInformation]( 
        [CustomerID] [int] NOT NULL, 
        [CustomerName] [varchar](50) NULL, 
        [Company] [varchar](50) NULL 
        CONSTRAINT [CustID] PRIMARY KEY CLUSTERED ([CustomerID] ASC) 
    ) 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (1, 'Jack', 'ABC') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (2, 'Steve', 'XYZ') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (3, 'Lylla', 'MNO') 

## <a name="create-database-objects"></a>Создание объектов базы данных
### <a name="database-scoped-master-key-and-credentials"></a>Главный ключ и учетные данные для конкретной базы данных
1. Откройте SQL Server Management Studio или SQL Server Data Tools в Visual Studio.
2. Подключения базы данных Orders toohello и выполните следующие команды T-SQL hello:
   
        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>'; 
        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred 
        WITH IDENTITY = '<username>', 
        SECRET = '<password>';  
   
    Hello «username» и «password» должно быть hello имя пользователя и пароль, используемые toologin в базу данных клиентам hello.
    Проверка подлинности с помощью Azure Active Directory и эластичных запросов сейчас не поддерживается.

### <a name="external-data-sources"></a>Внешние источники данных
toocreate внешнего источника данных, выполните следующую команду в базе данных заказов hello hello: 

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH 
        (TYPE = RDBMS, 
        LOCATION = '<server_name>.database.windows.net', 
        DATABASE_NAME = 'Customers', 
        CREDENTIAL = ElasticDBQueryCred, 
    ) ;

### <a name="external-tables"></a>Внешние таблицы
Создайте внешнюю таблицу Orders hello базе данных, который соответствует hello определение таблицы hello сведения о клиенте:

    CREATE EXTERNAL TABLE [dbo].[CustomerInformation] 
    ( [CustomerID] [int] NOT NULL, 
      [CustomerName] [varchar](50) NOT NULL, 
      [Company] [varchar](50) NOT NULL) 
    WITH 
    ( DATA_SOURCE = MyElasticDBQueryDataSrc) 

## <a name="execute-a-sample-elastic-database-t-sql-query"></a>Выполнение запроса T-SQL к примеру эластичной базы данных
После определения источника внешних данных и внешних таблиц теперь можно использовать tooquery T-SQL внешних таблиц. Выполните следующий запрос в базе данных заказов hello: 

    SELECT OrderInformation.CustomerID, OrderInformation.OrderId, CustomerInformation.CustomerName, CustomerInformation.Company 
    FROM OrderInformation 
    INNER JOIN CustomerInformation 
    ON CustomerInformation.CustomerID = OrderInformation.CustomerID 

## <a name="cost"></a>Стоимость
В настоящее время функция запроса hello эластичной базы данных включена в стоимость hello базы данных SQL Azure.  

Сведения о ценах см. на [странице с ценами на базы данных SQL](https://azure.microsoft.com/pricing/details/sql-database). 

## <a name="next-steps"></a>Дальнейшие действия

* Общие сведения об эластичных запросах см. в разделе [Обзор эластичных запросов к базе данных SQL Azure (предварительная версия)](sql-database-elastic-query-overview.md).
* Описание синтаксиса и примеры запросов вертикально секционированных данных см. в разделе [Запрос к нескольким облачным базам данных с разными схемами (предварительная версия)](sql-database-elastic-query-vertical-partitioning.md).
* Руководство по горизонтальному секционированию (сегментированию) см. в статье [Отчеты по масштабируемым облачным базам данных (предварительная версия)](sql-database-elastic-query-getting-started.md).
* Описание синтаксиса и примеры запросов горизонтально секционированных данных см. в разделе [Отчеты по масштабируемым облачным базам данных (предварительная версия)](sql-database-elastic-query-horizontal-partitioning.md).
* В описании [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) приведена хранимая процедура, которая выполняет инструкцию Transact-SQL для отдельной удаленной базы данных SQL Azure или набора баз данных, выступающих в качестве сегментов в схеме горизонтального секционирования.