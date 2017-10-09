---
title: "aaaVisualize данных хранилища данных SQL с помощью Power BI Microsoft Azure"
description: "Визуализация данных хранилища данных SQL с помощью Power BI"
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: d7fb89d1-da1d-4788-a111-68d0e3fda799
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: 0425cf5abe7bc001b2a41df4d09bf5f2e42527e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-data-with-power-bi"></a>Визуализация данных с помощью Power BI
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [машинное обучение Azure](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

В этом учебнике показано как toouse Power BI tooconnect tooSQL хранилища данных и создать базовый визуализации.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Data-Warehouse-Sample-Data-and-PowerBI/player]
> 
> 

## <a name="prerequisites"></a>Предварительные требования
toostep изучения этого руководства требуется:

* Хранилище данных SQL предварительно загружен с базы данных AdventureWorksDW hello. tooprovision это, см. в разделе [создать хранилище данных SQL] [ Create a SQL Data Warehouse] и выберите образец hello tooload данных. Если хранилище данных уже существует, но в нем нет демонстрационных данных, вы можете [загрузить их вручную][load sample data manually].

## <a name="1-connect-tooyour-database"></a>1. Подключение базы данных tooyour
tooopen Power BI и подключение базы данных AdventureWorksDW tooyour:

1. Вход в hello [портал Azure][Azure portal].
2. Щелкните **Базы данных SQL** и выберите базу данных хранилища данных SQL AdventureWorks.
   
    ![Поиск базы данных][1]
3. Нажмите кнопку «Открыть в Power BI» hello.
   
    ![Кнопка Power BI][2]
4. Теперь должна появиться страница подключения хранилища данных SQL hello, отображение веб-адресом базы данных. Нажмите кнопку «Далее».
   
    ![Power BI: подключение][3]
5. Введите имя сервера Azure SQL и пароль пользователя и будет базы данных полностью соединенными tooyour хранилище данных SQL.
   
    ![Power BI: вход][4]
6. После входа в Power BI, щелкните набор данных AdventureWorksDW hello левой колонке hello. Будет открыта hello базы данных.
   
    ![Power BI: открытие AdventureWorksDW][5]

## <a name="2-create-a-report"></a>2) Создание отчета
Вы являются tooanalyze Power BI теперь готовы toouse образцы данных AdventureWorksDW. Анализ tooperform hello, AdventureWorksDW имеет представление с именем AggregateSales. Это представление содержит несколько hello основные метрики для анализа продаж компании hello hello.

1. hello tooexpand AggregateSales представление, нажмите кнопку toocreate карту объем продаж, toopostal код, в области справа поля hello, в соответствии с его. Выберите столбцы tooselect hello PostalCode и SalesAmount их.
   
    ![Power BI: выбор AggregateSales][6]
   
    Power BI в автоматическом режиме распознает географические данные и наносит их на карту.
   
    ![Карта Power BI][7]
2. На этом этапе создается линейчатая диаграмма, на которой отображается сумма продаж в зависимости от доходов клиентов. toocreate этого перейдите toohello расширенный AggregateSales вид. Щелкните поле SalesAmount hello. Перетащите поле toohello hello доход клиента влево и вставьте его в оси.
   
    ![Power BI: выбор оси][8]
   
    Мы перешли hello линейчатой диаграммы по левой hello.
   
    ![Гистограмма Power BI][9]
3. На этом этапе создается график, на котором отображены продажи по дате заказа. toocreate этого перейдите toohello расширенный AggregateSales вид. Щелкните SalesAmount и OrderDate. В столбце визуализации hello выберите значок графика hello; Это первый значок hello вторую строку hello в визуализации.
   
    ![Power BI: выбор графика][10]
   
    Теперь у вас есть отчет, показывающий трех различных вариантах визуализации данных hello.
   
    ![График Power BI][11]

Ход выполнения можно сохранить в любой момент, выбрав в меню **Файл** пункт **Сохранить**.

## <a name="next-steps"></a>Дальнейшие действия
Мы предоставили вам toowarm некоторое время с образцами данных hello, см. статью как слишком[разработки][develop], [загрузить][load], или [ Перенос][migrate]. Или просмотрите hello [веб-сайт Power BI][Power BI website].

<!--Image references-->
[1]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-find-database.png
[2]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-button.png
[3]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-connect-to-azure.png
[4]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-sign-in.png
[5]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-open-adventureworks.png
[6]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-aggregatesales.png
[7]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-map.png
[8]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-chooseaxis.png
[9]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-bar.png
[10]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-prepare-line.png
[11]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-line.png
[12]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-save.png

<!--Article references-->
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[load sample data manually]: sql-data-warehouse-load-sample-databases.md
[connecting tooSQL Data Warehouse]: sql-data-warehouse-integrate-power-bi.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md

<!--Other-->
[Azure portal]: https://portal.azure.com/
[Power BI website]: http://www.powerbi.com/
