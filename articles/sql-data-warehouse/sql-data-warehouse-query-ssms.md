---
title: "aaaConnect tooAzure хранилище данных SQL - SSMS | Документы Microsoft"
description: "Используйте SQL Server Management Studio (SSMS) tooconnect tooand запрос хранилище данных SQL Azure."
services: sql-data-warehouse
documentationcenter: 
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 299e50b3-e68a-471c-8aee-b0b9874781bd
ms.service: sql-data-warehouse
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: bcbaf7139d2e5183b388b8d58c015cf5ad726722
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-sql-server-management-studio-ssms"></a>Подключение tooSQL хранилища данных с SQL Server Management Studio (SSMS)
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [машинное обучение Azure](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

Используйте SQL Server Management Studio (SSMS) tooconnect tooand запрос хранилище данных SQL Azure. 

## <a name="prerequisites"></a>Предварительные требования
toouse этого учебника, необходимо:

* Существующее хранилище данных SQL. разделе toocreate, [создать хранилище данных SQL][Create a SQL Data Warehouse].
* Установленный SQL Server Management Studio (SSMS). [Установите SSMS][Install SSMS] бесплатно, если вы еще этого не сделали.
* Hello полное доменное имя сервера SQL server. toofind это, см. в разделе [подключения хранилища данных tooSQL][Connect tooSQL Data Warehouse].

## <a name="1-connect-tooyour-sql-data-warehouse"></a>1. Подключение tooyour хранилище данных SQL
1. Откройте среду SSMS.
2. Откройте обозреватель объектов. toodo это, выберите **файл** > **подключить к обозревателю объектов**.
   
    ![Обозреватель объектов SQL Server][1]
3. Заполните поля hello в окне tooServer Connect hello.
   
    ![Подключение tooServer][2]
   
   * **Имя сервера**. Введите hello **имя сервера** ранее определенных.
   * **Проверка подлинности**. Выберите **Проверка подлинности SQL Server** или **Встроенная проверка подлинности Active Directory**.
   * **Имя пользователя** и **Пароль**. Если вы выбрали проверку подлинности SQL Server, введите имя пользователя и пароль.
   * Щелкните **Подключить**.
4. tooexplore, разверните сервер Azure SQL. Вы можете просмотреть hello баз данных, связанных с сервером hello. Разверните AdventureWorksDW toosee hello таблицам образца базы данных.
   
    ![Обзор AdventureWorksDW][3]

## <a name="2-run-a-sample-query"></a>2) Запуск пробного запроса
Теперь, когда соединение было tooyour установленной базы данных, давайте написать запрос.

1. Щелкните правой кнопкой мыши базу данных в обозревателе объектов SQL Server.
2. Выберите пункт **Создать запрос**. Откроется окно нового запроса.
   
    ![Создать запрос][4]
3. Скопируйте этот запрос TSQL в окно запроса hello:
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. Выполните запрос hello. toodo, нажмите кнопку `Execute` или hello используйте следующий ярлык: `F5`.
   
    ![Выполнение запроса][5]
5. Взгляните на результаты запроса hello. В этом примере таблицы FactInternetSales hello содержит 60398 строк.
   
    ![Результаты запроса][6]

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы сможете подключиться и запросов, попробуйте [визуализация данных hello с PowerBI][visualizing hello data with PowerBI].

tooconfigure среды для проверки подлинности Azure Active Directory, в разделе [tooSQL хранилища данных проверки подлинности][Authenticate tooSQL Data Warehouse].

<!--Arcticles-->
[Connect tooSQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Authenticate tooSQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing hello data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md 

<!--Other-->
[Azure portal]: https://portal.azure.com
[Install SSMS]: https://msdn.microsoft.com/en-US/library/hh213248.aspx


<!--Image references-->

[1]: media/sql-data-warehouse-query-ssms/connect-object-explorer.png
[2]: media/sql-data-warehouse-query-ssms/connect-object-explorer1.png
[3]: media/sql-data-warehouse-query-ssms/explore-tables.png
[4]: media/sql-data-warehouse-query-ssms/new-query.png
[5]: media/sql-data-warehouse-query-ssms/execute-query.png
[6]: media/sql-data-warehouse-query-ssms/results.png
