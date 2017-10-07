---
title: "aaaLoad данные из SQL Server в хранилище данных Azure SQL (SSIS) | Документы Microsoft"
description: "Показывает, как toocreate toomove данные пакета служб SQL Server Integration Services (SSIS) из самых разнообразных данных источники tooSQL хранилища данных."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: e2c252e9-0828-47c2-a808-e3bea46c134a
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 03/30/2017
ms.author: cakarst;douglasl;barbkess
ms.openlocfilehash: bb28a08807a5b07832b85f2f074c2acf912c1dc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-ssis"></a>Загрузка данных из SQL Server в хранилище данных SQL Azure (SSIS)
> [!div class="op_single_selector"]
> * [SSIS](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [PolyBase;](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [bcp](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

Создание данных tooload пакета SQL Server Integration Services (SSIS) из SQL Server в хранилище данных SQL Azure. При необходимости можно изменить структуру, преобразования и очистки данных hello при прохождении через hello потока данных служб SSIS.

Изучив данный учебник, вы научитесь:

* создание нового проекта служб Integration Services в Visual Studio;
* Подключение toodata источников, включая SQL Server (как к источнику) и хранилище данных SQL (в качестве назначения).
* Создайте пакет служб SSIS, которая загружает данные из источника hello в целевой hello.
* Здравствуйте, выполнения данных hello tooload пакетов служб SSIS.

В этом учебнике используется SQL Server в качестве источника данных hello. SQL Server может выполняться на локальном компьютере или на виртуальной машине Azure.

## <a name="basic-concepts"></a>Основные понятия
пакет Hello — hello единица работы служб SSIS. Связанные пакеты группируются в проекты. Вы можете создавать проекты и разрабатывать пакеты с помощью SQL Server Data Tools для Visual Studio. Hello конструирования процесс является visual процессом, в которой можно перетаскивать компоненты из hello элементов toohello конструктора, подключите их и задавать их свойства. После завершения пакета можно при необходимости развернуть ее tooSQL сервер для общего управления, мониторинга и безопасности.

## <a name="options-for-loading-data-with-ssis"></a>Параметры для загрузки данных с помощью служб SSIS
SQL Server Integration Services (SSIS) — это гибкий набор средств, предоставляющий различные возможности для подключения к хранилищу данных SQL и загрузки данных в это хранилище.

1. Используйте назначение ADO NET tooconnect tooSQL хранилища данных. В этом учебнике используется назначение ADO NET, так как он содержит hello минимальные параметры конфигурации.
2. Используйте назначение OLE DB tooconnect tooSQL хранилища данных. Этот параметр может предоставлять немного лучшую производительность, чем hello назначение ADO NET.
3. Используйте hello задача передачи BLOB-объектов Azure toostage hello данные в хранилище больших двоичных объектов Azure. Затем с помощью toolaunch задачи служб SSIS Выполнение SQL hello Polybase скрипт, который загружает данные hello в хранилище данных SQL. Этот параметр обеспечивает высокую производительность hello из трех параметров hello перечисленные здесь. tooget hello Azure BLOB-объекта с помощью задачи передачи, загрузите hello [Microsoft SQL Server 2016 Integration Services Feature Pack для Azure][Microsoft SQL Server 2016 Integration Services Feature Pack for Azure]. toolearn Дополнительные сведения о Polybase, в разделе [руководство по PolyBase][PolyBase Guide].

## <a name="before-you-start"></a>Перед началом работы
toostep изучения этого руководства требуется:

1. **SQL Server Integration Services (SSIS).** Службы SSIS — это компонент SQL Server. Для его использования требуется ознакомительная или лицензированная версия SQL Server. tooget ознакомительной версии SQL Server 2016 Preview в разделе [SQL Server оценок][SQL Server Evaluations].
2. **Visual Studio** tooget hello бесплатный выпуск Visual Studio Community см. в разделе [Visual Studio Community][Visual Studio Community].
3. **SQL Server Data Tools для Visual Studio (SSDT)**. tooget SQL Server Data Tools для Visual Studio, в разделе [загрузить SQL Server Data Tools (SSDT)][Download SQL Server Data Tools (SSDT)].
4. **Образец данных**. В этом учебнике используется образец данных, хранящихся в SQL Server в образце базы данных AdventureWorks hello как hello toobe источника данных, загружаются в хранилище данных SQL. hello tooget образца базы данных AdventureWorks в разделе [образцов баз данных AdventureWorks 2014][AdventureWorks 2014 Sample Databases].
5. **База данных хранилища данных SQL и разрешения на ее использование**. Этот учебник подключается tooa экземпляр хранилища данных SQL и загружает в нее данные. У вас есть разрешения toocreate toohave таблицы и tooload данных.
6. **Правило брандмауэра.** У вас есть toocreate правило брандмауэра хранилище данных SQL с hello IP-адрес локального компьютера перед загрузкой данных toohello хранилище данных SQL.

## <a name="step-1-create-a-new-integration-services-project"></a>Шаг 1. Создание нового проекта служб Integration Services
1. Запустите Visual Studio.
2. На hello **файл** последовательно выберите пункты **New | Проект**.
3. Перейдите toohello **установленные | Шаблоны | Бизнес-аналитики | Службы Integration Services** типов проектов.
4. Выберите **Проект служб Integration Services**. Введите **имя** и **расположение**, а затем нажмите кнопку **ОК**.

Visual Studio откроется и создаст новый проект служб Integration Services (SSIS). Затем Visual Studio откроется конструктор hello для hello один новый пакет служб SSIS (Package.dtsx) в проекте hello. Можно увидеть следующие области экрана приветствия:

* В левой части экрана приветствия hello **элементов** компонентов служб SSIS.
* В середине hello hello конструктора с несколькими вкладками. Как правило, используется по крайней мере hello **поток управления** и hello **потока данных** вкладок.
* На правом hello, hello **обозревателе решений** и hello **свойства** панелей.
  
    ![][01]

## <a name="step-2-create-hello-basic-data-flow"></a>Шаг 2: Создание потока данных hello
1. Перетащите задачу потока данных из центра toohello hello панели элементов конструктора hello (на hello **поток управления** вкладке).
   
    ![][02]
2. Дважды щелкните вкладку поток данных hello задачи потока данных tooswitch toohello.
3. Из списка hello других источников в hello панели элементов перетащите источник ADO.NET toohello конструктора. Адаптер источника hello по-прежнему выбран, измените ее имя слишком**источника SQL Server** в hello **свойства** области.
4. Из списка другие назначения hello в hello панели элементов перетащите конструктора toohello ADO.NET, назначение под hello источника ADO.NET. С hello адаптер загрузки данных по-прежнему выбран, измените ее имя слишком**назначения хранилища данных SQL** в hello **свойства** области.
   
    ![][09]

## <a name="step-3-configure-hello-source-adapter"></a>Шаг 3: Настройка адаптера источника hello
1. Дважды щелкните адаптер tooopen hello источника hello **Редактор источника ADO.NET**.
   
    ![][03]
2. На hello **диспетчера соединений** вкладка hello **Редактор источника ADO.NET**, щелкните hello **New** кнопку Далее toohello **диспетчера соединений ADO.NET**список hello tooopen **Настройка диспетчера соединений ADO.NET** диалоговое окно и создать параметры подключения для базы данных SQL Server hello, из которого этот учебник загружает данные.
   
    ![][04]
3. В hello **Настройка диспетчера соединений ADO.NET** диалогового окна выберите hello **New** hello tooopen кнопку **диспетчера соединений** диалоговое окно и создать новое подключение к данным.
   
    ![][05]
4. В hello **диспетчера соединений** диалогового окна поле, hello следующие действия.
   
   1. Для **поставщика**, выберите hello поставщик данных SqlClient.
   2. Для **имя сервера**, введите имя сервера SQL hello.
   3. В hello **входа на сервер toohello** выберите или введите сведения для проверки подлинности.
   4. В hello **базы данных tooa Connect** выберите образец базы данных AdventureWorks hello.
   5. Нажмите кнопку **Проверить подключение**.
      
       ![][06]
   6. В hello диалоговое окно, сообщающее hello результаты тестирования подключения hello выберите **ОК** tooreturn toohello **диспетчера соединений** диалоговое окно.
   7. В hello **диспетчера соединений** диалоговое окно, нажмите кнопку **ОК** tooreturn toohello **Настройка диспетчера соединений ADO.NET** диалоговое окно.
5. В hello **Настройка диспетчера соединений ADO.NET** диалоговое окно, нажмите кнопку **ОК** tooreturn toohello **Редактор источника ADO.NET**.
6. В hello **Редактор источника ADO.NET**, в hello **имя hello таблицы или представления hello** список, выберите hello **Sales.SalesOrderDetail** таблицы.
   
    ![][07]
7. Нажмите кнопку **предварительного просмотра** toosee hello первые 200 строк данных в исходной таблице hello в hello **Предварительный просмотр результатов запроса** диалоговое окно.
   
    ![][08]
8. В hello **Предварительный просмотр результатов запроса** диалоговое окно, нажмите кнопку **закрыть** tooreturn toohello **Редактор источника ADO.NET**.
9. В hello **Редактор источника ADO.NET**, нажмите кнопку **ОК** toofinish настройки источника данных hello.

## <a name="step-4-connect-hello-source-adapter-toohello-destination-adapter"></a>Шаг 4: Подключение адаптера назначения toohello адаптер источника hello
1. Выберите адаптер источника hello hello конструктора.
2. Выберите стрелку синий hello, начиная с адаптером источника hello и перетащите его редактор назначения toohello до попадания на месте.
   
    ![][10]
   
    В типичный пакет служб SSIS использовать несколько других компонентов из hello область элементов служб SSIS между hello источника и назначения toorestructure hello, преобразования и очистки данных при его прохождении через hello потока данных служб SSIS. tookeep как можно более простыми в этом примере мы подключаетесь hello непосредственно источника toohello назначения.

## <a name="step-5-configure-hello-destination-adapter"></a>Шаг 5: Настройка адаптера назначения hello
1. Дважды щелкните адаптер tooopen hello назначения hello **Редактор назначения ADO.NET**.
   
    ![][11]
2. На hello **диспетчера соединений** вкладка hello **Редактор назначения ADO.NET**, щелкните hello **New** кнопку Далее toohello **диспетчера соединений**список hello tooopen **Настройка диспетчера соединений ADO.NET** диалоговое окно и создать параметры подключения для базы данных хранилища данных SQL Azure hello, в которую этот учебник загружает данные.
3. В hello **Настройка диспетчера соединений ADO.NET** диалогового окна выберите hello **New** hello tooopen кнопку **диспетчера соединений** диалоговое окно и создать новое подключение к данным.
4. В hello **диспетчера соединений** диалогового окна поле, hello следующие действия.
   1. Для **поставщика**, выберите hello поставщик данных SqlClient.
   2. Для **имя сервера**, введите имя хранилища данных SQL hello.
   3. В hello **входа на сервер toohello** выберите **проверки подлинности SQL Server используйте** и введите сведения для проверки подлинности.
   4. В hello **базы данных tooa Connect** выберите существующую базу данных хранилища данных SQL.
   5. Нажмите кнопку **Проверить подключение**.
   6. В hello диалоговое окно, сообщающее hello результаты тестирования подключения hello выберите **ОК** tooreturn toohello **диспетчера соединений** диалоговое окно.
   7. В hello **диспетчера соединений** диалоговое окно, нажмите кнопку **ОК** tooreturn toohello **Настройка диспетчера соединений ADO.NET** диалоговое окно.
5. В hello **Настройка диспетчера соединений ADO.NET** диалоговое окно, нажмите кнопку **ОК** tooreturn toohello **Редактор назначения ADO.NET**.
6. В hello **Редактор назначения ADO.NET**, нажмите кнопку **New** Далее toohello **используют таблицу или представление** hello список tooopen **Create Table** диалоговое окно toocreate Новая целевая таблица со списком столбцов, который соответствует hello исходной таблицы.
   
    ![][12a]
7. В hello **Create Table** диалогового окна поле, hello следующие действия.
   
   1. Изменить имя целевой таблицы hello hello слишком**SalesOrderDetail**.
   2. Удалите hello **rowguid** столбца. Hello **uniqueidentifier** тип данных не поддерживается в хранилище данных SQL.
   3. Измените тип данных hello hello **LineTotal** столбец слишком**money**. Hello **десятичное** тип данных не поддерживается в хранилище данных SQL. Дополнительные сведения о поддерживаемых типах данных см. в статье [СОЗДАНИЕ ТАБЛИЦЫ (хранилище данных Azure SQL)][CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)].
      
       ![][12b]
   4. Нажмите кнопку **ОК** toocreate hello таблицы и возврат toohello **Редактор назначения ADO.NET**.
8. В hello **Редактор назначения ADO.NET**выберите hello **сопоставления** вкладке toosee как столбцы в источнике hello сопоставляются toocolumns в конечном hello.
   
    ![][13]
9. Нажмите кнопку **ОК** toofinish настройки источника данных hello.

## <a name="step-6-run-hello-package-tooload-hello-data"></a>Шаг 6: Проведение tooload hello hello пакета данных
Hello выполнения пакета, нажав кнопку hello **запустить** кнопки на панели инструментов hello или, выбрав один из hello **запуска** параметров на hello **отладки** меню.

При hello пакет начинает toorun, отображаются желтый wheels вращающийся tooindicate действия, а также hello количество строк, обработанных в данный момент.

![][14]

После завершения выполнения пакета hello, вы успешно tooindicate зеленые галочки в разделе а также hello общее число строк данных, загруженных из hello источник toohello назначения.

![][15]

Поздравляем! Вы успешно использовали tooload данных SQL Server Integration Services в хранилище данных SQL Azure.

## <a name="next-steps"></a>Дальнейшие действия
* Дополнительные сведения о потоке данных SSIS hello. Начните со статьи [Поток данных][Data Flow].
* Узнайте, как toodebug и устранение неполадок ваше право пакетов в среде разработки hello. Начните со статьи [Инструменты устранения неполадок при разработке пакета][Troubleshooting Tools for Package Development].
* Узнайте, как toodeploy your SSIS проекты и пакеты tooIntegration сервер служб или tooanother место хранения. Начните со статьи [Развертывание проектов и пакетов служб Integration Services (SSIS)][Deployment of Projects and Packages].

<!-- Image references -->
[01]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ssis-designer-01.png
[02]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ssis-data-flow-task-02.png
[03]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-source-03.png
[04]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-connection-manager-04.png
[05]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-connection-05.png
[06]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/test-connection-06.png
[07]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-source-07.png
[08]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/preview-data-08.png
[09]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/source-destination-09.png
[10]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/connect-source-destination-10.png
[11]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-destination-11.png
[12a]: ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/destination-query-before-12a.png
[12b]: ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/destination-query-after-12b.png
[13]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/column-mapping-13.png
[14]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/package-running-14.png
[15]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/package-success-15.png

<!-- Article references -->

<!-- MSDN references -->
[PolyBase Guide]: https://msdn.microsoft.com/library/mt143171.aspx
[Download SQL Server Data Tools (SSDT)]: https://msdn.microsoft.com/library/mt204009.aspx
[CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)]: https://msdn.microsoft.com/library/mt203953.aspx
[Data Flow]: https://msdn.microsoft.com/library/ms140080.aspx
[Troubleshooting Tools for Package Development]: https://msdn.microsoft.com/library/ms137625.aspx
[Deployment of Projects and Packages]: https://msdn.microsoft.com/library/hh213290.aspx

<!--Other Web references-->
[Microsoft SQL Server 2016 Integration Services Feature Pack for Azure]: http://go.microsoft.com/fwlink/?LinkID=626967
[SQL Server Evaluations]: https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016
[Visual Studio Community]: https://www.visualstudio.com/en-us/products/visual-studio-community-vs.aspx
[AdventureWorks 2014 Sample Databases]: https://msftdbprodsamples.codeplex.com/releases/view/125550
