---
title: "хранилище данных Azure tooyour данных tooload aaaUse Redgate | Документы Microsoft"
description: "Узнайте, как toouse Redgate Studio платформы данных для сценариев хранилища данных."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 670aef98-31f7-4436-86c0-cc989a39fe7f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 6082390c07c8ffa73ebd8ab272ace00ba8bb1897
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-redgate-data-platform-studio"></a>Загрузка данных с помощью Redgate Data Platform Studio
> [!div class="op_single_selector"]
> * [Redgate](sql-data-warehouse-load-with-redgate.md)
> * [Фабрика данных](sql-data-warehouse-get-started-load-with-azure-data-factory.md)
> * [PolyBase;](sql-data-warehouse-get-started-load-with-polybase.md)
> * [BCP](sql-data-warehouse-load-with-bcp.md)
> 
> 

В этом учебнике показано как toouse [Studio платформы данных Redgate](http://www.red-gate.com/products/azure-development/data-platform-studio/) (диагностики) toomove данные из локального SQL Server tooAzure хранилище данных SQL. Studio платформы данных применяет исправления совместимости наиболее подходящий hello и оптимизации, поэтому он содержит быстрее других hello tooget способ работы с хранилищем данных SQL.

> [!NOTE]
> Компания [Redgate](http://www.red-gate.com) — это многолетний партнер корпорации Майкрософт, который предоставляет различные средства для базы данных SQL Server. Решение Data Platform Studio доступно бесплатно для коммерческого и некоммерческого использования.
> 
> 

## <a name="before-you-begin"></a>Перед началом работы
### <a name="create-or-identify-resources"></a>Создание или определение ресурсов
Перед запуском этого учебника, необходимо toohave:

* **Локальная база данных SQL Server**: hello данные нужно tooimport tooSQL хранилища данных требуется toocome из локального SQL Server (версии 2008 R2 или более поздней версии). Data Platform Studio не может импортировать данные напрямую из базы данных SQL Azure или из текстовых файлов.
* **Учетная запись хранения Azure**: Studio платформы данных готовит hello данных в хранилище больших двоичных объектов Azure перед загрузкой в хранилище данных SQL. Hello учетной записи хранилища необходимо использовать модель развертывания hello «диспетчер ресурсов» (по умолчанию hello) вместо модель развертывания «Классический» hello. При отсутствии учетной записи хранилища, узнайте, как tooCreate учетной записи хранилища. 
* **Хранилище данных SQL**: этого учебника перемещает hello данные из tooSQL в локальной среде SQL Server хранилища данных, поэтому требуется toohave хранилища данных. Если у вас еще нет в хранилище данных, узнайте, как tooCreate хранилище данных SQL Azure.

> [!NOTE]
> Повышение производительности, если учетная запись хранения hello и хранилище данных hello создаются в hello же области.
> 
> 

## <a name="step-1-sign-in-toodata-platform-studio-with-your-azure-account"></a>Шаг 1: Войдите в tooData Studio платформы с учетной записью Azure
Откройте браузер и перейдите toohello [Studio платформы данных](https://www.dataplatformstudio.com/) веб-сайта. Вход с hello одной учетной записью Azure, то используется toocreate hello хранилища учетной записи и хранилища данных. Если ваш адрес электронной почты связан с рабочую или учебную учетную запись и учетную запись Майкрософт, будет убедиться, что hello toochoose учетную запись, которая имеет доступ к ресурсам tooyour.

> [!NOTE]
> Если вы впервые используете Studio платформы данных, задаваемые toomanage разрешений приложения hello toogrant ресурсами Azure.
> 
> 

## <a name="step-2-start-hello-import-wizard"></a>Шаг 2: Запуск мастера импорта hello
Главный экран приветствия диагностики выберите hello импорта tooAzure хранилище данных SQL ссылку toostart приветствия мастера импорта.

![][1]

## <a name="step-3-install-hello-data-platform-studio-gateway"></a>Шаг 3: Установка hello шлюз Studio платформы данных
База данных SQL Server в локальной tooyour tooconnect, необходимо tooinstall hello диагностики шлюза. шлюз Hello — агент клиента, который предоставляет доступ tooyour в локальную среду, извлекает данные hello и передает его tooyour учетной записи хранилища. Данные никогда не проходят через серверы Redgate. hello tooinstall шлюз:

1. Нажмите кнопку hello **создать шлюз** ссылку
2. Загрузка и установка hello шлюза с помощью hello предоставленный установщика

![][2]

> [!NOTE]
> Hello шлюз можно установить на любом компьютере с базой данных SQL Server источника toohello доступа к сети. Он обращается к hello базы данных SQL Server с помощью проверки подлинности Windows с учетными данными hello hello текущего пользователя.
> 
> 

После установки hello tooConnected изменения состояния шлюза и выборе Далее.

## <a name="step-4-identify-hello-source-database"></a>Шаг 4: Определение hello базы данных-источника
В hello *введите имя сервера* текстовом поле введите имя hello hello сервера, на котором размещены базы данных и выберите **Далее**. Hello раскрывающегося меню, выберите базу данных hello нужные данные tooimport из.

![][3]

Проверяет hello выбранной базы данных для таблицы tooimport. По умолчанию диагностики импортирует все hello таблицы в базе данных hello. Можно выбрать или отменить выбор таблиц, развернув приветствия связывать все таблицы. Выберите hello далее кнопку toomove вперед.

## <a name="step-5-choose-a-storage-account-toostage-hello-data"></a>Шаг 5: Выберите данные hello toostage учетной записи хранилища
Диагностики запрашивает toostage hello расположения данных. Выберите имеющуюся учетную запись хранения в подписке и нажмите кнопку **Next** (Далее).

> [!NOTE]
> Диагностики будет создать новый контейнер больших двоичных объектов в выбранной учетной записи хранилища hello и использовать отдельные папки для каждого импорта.
> 
> 

![][4]

## <a name="step-6-select-a-data-warehouse"></a>Шаг 6. Выбор хранилища данных
Затем выберите оперативного [хранилище данных SQL Azure](http://aka.ms/sqldw) tooimport hello данных в базы данных. После выбора базы данных, вам потребуется tooenter hello учетные данные tooconnect toohello базы данных и выберите **Далее**.

![][5]

> [!NOTE]
> Диагностики объединяет таблицы с исходными данными hello в хранилище данных hello. Диагностики выдает предупреждение, если имя таблицы hello требует toooverwrite таблиц, существующих в хранилище данных hello. Можно удалить все существующие объекты в хранилище данных hello, отсчет удалить все существующие объекты перед импортом.
> 
> 

## <a name="step-7-import-hello-data"></a>Шаг 7: Импорт данных hello
Диагностики подтверждает, что хотелось бы tooimport hello данных. Просто нажмите кнопку Пуск hello импорта toobegin кнопку hello импорта данных.

![][6]

Диагностики отображает представление, где отображается ход hello извлечение и передача данных hello с hello в локальной среде SQL Server и hello ход выполнения импорта hello в хранилище данных SQL.

![][7]

После завершения импорта hello диагностики отображается сводка по импорту данных hello и изменение отчета о hello исправления совместимости, которые были выполнены.

![][8]

## <a name="next-steps"></a>Дальнейшие действия
tooexplore ваши данные в хранилище данных SQL, начните с просмотра:

* [Запросы к хранилищу данных SQL Azure (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)]
* [Визуализация данных с помощью Power BI][Visualize data with Power BI]

Дополнительные сведения о Studio платформы данных Redgate toolearn:

* [Посетите домашнюю страницу диагностики hello](http://www.dataplatformstudio.com/)
* [Демонстрационное видео DPS на Channel 9](https://channel9.msdn.com/Blogs/cloud-with-a-silver-lining/Loading-data-into-Azure-SQL-Datawarehouse-with-Redgate-Data-Platform-Studio)

Общие сведения о других способах toomigrate и загрузка данных в хранилище данных SQL см.:

* [Перенос tooSQL вашего решения хранилища данных][Migrate your solution tooSQL Data Warehouse]
* [Загрузка данных в хранилище данных Azure SQL](sql-data-warehouse-overview-load.md)

Дополнительные советы по разработке в разделе hello [Общие сведения о разработке хранилище данных SQL](sql-data-warehouse-overview-develop.md).

<!--Image references-->
[1]: media/sql-data-warehouse-redgate/2016-10-05_15-59-56.png
[2]: media/sql-data-warehouse-redgate/2016-10-05_11-16-07.png
[3]: media/sql-data-warehouse-redgate/2016-10-05_11-17-46.png
[4]: media/sql-data-warehouse-redgate/2016-10-05_11-20-41.png
[5]: media/sql-data-warehouse-redgate/2016-10-05_11-31-24.png
[6]: media/sql-data-warehouse-redgate/2016-10-05_11-32-20.png
[7]: media/sql-data-warehouse-redgate/2016-10-05_11-49-53.png
[8]: media/sql-data-warehouse-redgate/2016-10-05_12-57-10.png

<!--Article references-->
[Query Azure SQL Data Warehouse (Visual Studio)]: ./sql-data-warehouse-query-visual-studio.md
[Visualize data with Power BI]: ./sql-data-warehouse-get-started-visualize-with-power-bi.md
[Migrate your solution tooSQL Data Warehouse]: ./sql-data-warehouse-overview-migrate.md
[Load data into Azure SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
