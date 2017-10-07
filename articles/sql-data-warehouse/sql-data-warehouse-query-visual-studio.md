---
title: "aaaConnect tooAzure хранилище данных SQL - VSTS | Документы Microsoft"
description: "Отправка запросов к хранилищу данных SQL с помощью Visual Studio."
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: daace889-95e5-4826-b2fc-047eac9d6d95
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: 55eef4dff3e0647be5a735295bc89b43eb456079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-visual-studio-and-ssdt"></a>Подключиться с помощью Visual Studio и SSDT tooSQL хранилища данных
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [машинное обучение Azure](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

Используйте Visual Studio tooquery хранилище данных SQL Azure через несколько минут. Этот метод использует расширение hello SQL Server Data Tools (SSDT) в Visual Studio. 

## <a name="prerequisites"></a>Предварительные требования
toouse этого учебника, необходимо:

* Существующее хранилище данных SQL. разделе toocreate, [создать хранилище данных SQL][Create a SQL Data Warehouse].
* Расширение SSDT для Visual Studio. Скорее всего, оно уже есть, если на вашем компьютере установлено приложение Visual Studio. Инструкции по установке и доступные варианты установки см. в статье [Установка Visual Studio 2015 и SSDT для хранилища данных SQL][Installing Visual Studio and SSDT].
* Hello полное доменное имя сервера SQL server. toofind это, см. в разделе [подключения хранилища данных tooSQL][Connect tooSQL Data Warehouse].

## <a name="1-connect-tooyour-sql-data-warehouse"></a>1. Подключение tooyour хранилище данных SQL
1. Откройте Visual Studio 2013 или 2015.
2. Откройте обозреватель объектов SQL Server. toodo это, выберите **представление** > **обозреватель объектов SQL Server**.
   
    ![Обозреватель объектов SQL Server][1]
3. Нажмите кнопку hello **добавить SQL Server** значок.
   
    ![Добавить SQL Server][2]
4. Заполните поля hello в окне tooServer Connect hello.
   
    ![Подключение tooServer][3]
   
   * **Имя сервера**. Введите hello **имя сервера** ранее определенных.
   * **Проверка подлинности**. Выберите **Проверка подлинности SQL Server** или **Встроенная проверка подлинности Active Directory**.
   * **Имя пользователя** и **Пароль**. Если вы выбрали проверку подлинности SQL Server, введите имя пользователя и пароль.
   * Щелкните **Подключить**.
5. tooexplore, разверните сервер Azure SQL. Вы можете просмотреть hello баз данных, связанных с сервером hello. Разверните AdventureWorksDW toosee hello таблицам образца базы данных.
   
    ![Обзор AdventureWorksDW][4]

## <a name="2-run-a-sample-query"></a>2) Запуск пробного запроса
Теперь, когда соединение было tooyour установленной базы данных, давайте написать запрос.

1. Щелкните правой кнопкой мыши базу данных в обозревателе объектов SQL Server.
2. Выберите пункт **Создать запрос**. Откроется окно нового запроса.
   
    ![Создать запрос][5]
3. Скопируйте этот запрос TSQL в окно запроса hello:
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. Выполните запрос hello. toodo это, нажмите кнопку со стрелкой hello зеленый или использовать следующие сочетания hello: `CTRL` + `SHIFT` + `E`.
   
    ![Выполнение запроса][6]
5. Взгляните на результаты запроса hello. В этом примере таблицы FactInternetSales hello содержит 60398 строк.
   
    ![Результаты запроса][7]

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы сможете подключиться и запросов, попробуйте [визуализация данных hello с PowerBI][visualizing hello data with PowerBI].

tooconfigure среды для проверки подлинности Azure Active Directory, в разделе [tooSQL хранилища данных проверки подлинности][Authenticate tooSQL Data Warehouse].

<!--Arcticles-->
[Connect tooSQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[Authenticate tooSQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing hello data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md  

<!--Other-->
[Azure portal]: https://portal.azure.com

<!--Image references-->

[1]: media/sql-data-warehouse-query-visual-studio/open-ssdt.png
[2]: media/sql-data-warehouse-query-visual-studio/add-server.png
[3]: media/sql-data-warehouse-query-visual-studio/connection-dialog.png
[4]: media/sql-data-warehouse-query-visual-studio/explore-sample.png
[5]: media/sql-data-warehouse-query-visual-studio/new-query2.png
[6]: media/sql-data-warehouse-query-visual-studio/run-query.png
[7]: media/sql-data-warehouse-query-visual-studio/query-results.png
