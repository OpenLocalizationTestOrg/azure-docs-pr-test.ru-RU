---
title: "aaaReport масштабируемых облачных базах данных (горизонтальное секционирование) | Документы Microsoft"
description: "как toouse кросс-запросов к базе данных"
services: sql-database
documentationcenter: 
manager: jhubbard
author: MladjoA
ms.assetid: c81ef5e3-41e9-4fd2-8631-868f2e168147
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: mlandzic
ms.openlocfilehash: e34f398f8d408cffd91a70fc2cfbda73daec3550
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="report-across-scaled-out-cloud-databases-preview"></a>Отчеты по масштабируемым облачным базам данных (предварительная версия)
С помощью [эластичных запросов](sql-database-elastic-query-overview.md)можно создавать отчеты из нескольких баз данных SQL Azure из одной точки подключения. Hello баз данных должны быть горизонтально секционированы (также называемая «сегментированных»).

При наличии существующей базы данных, в разделе [перенос существующих баз данных базы данных вне tooscaled](sql-database-elastic-convert-to-use-elastic-tools.md).

объекты SQL hello toounderstand нужны tooquery см. в разделе [запросов в нескольких базах данных горизонтально секционированные](sql-database-elastic-query-horizontal-partitioning.md).

## <a name="prerequisites"></a>Предварительные требования
Загрузите и запустите hello [Приступая к работе с образцом эластичной базы данных средства](sql-database-elastic-scale-get-started.md).

## <a name="create-a-shard-map-manager-using-hello-sample-app"></a>Создать пример приложения hello с помощью диспетчера карты сегментов
Здесь вы создадите карта сегментов manager вместе с несколькими сегментами, следуют вставки данных в сегментах hello. Если вы столкнулись tooalready установки сегментов с сегментированных данных в них, можно пропустить следующие шаги hello и переместить следующий раздел toohello.

1. Построение и запуск hello **Приступая к работе со средствами эластичной базы данных** образец приложения. Выполните действия hello до шага 7 в разделе "hello" [загрузить и запустить пример приложения hello](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app). В конце hello шаг 7 вы увидите hello, выполнив в командной строке:

    ![окно командной строки.][1]
2. В окне приветствия командной строки, введите «1» и нажмите клавишу **ввод**. Это создает диспетчера карты сегментов hello и добавляет два сервера toohello сегментов. Затем введите «3» и нажмите клавишу **ввод**; повторите действие hello четыре раза. Это позволит вставить строки демонстрационных данных в свои сегменты.
3. Hello [портал Azure](https://portal.azure.com) должны отобразиться три новых баз данных сервера:

   ![Подтверждение Visual Studio][2]

   На этом этапе межбазовые запросы поддерживаются с помощью клиентских библиотек hello эластичной базы данных. Например используйте параметр 4 в командном окне приветствия. Hello результаты из нескольких сегментов запроса всегда являются **UNION ALL** hello результатов из всех сегментах.

   В следующем разделе hello мы создадим конечной точке образец базы данных, который поддерживает обширные возможности запрос hello данных по сегментам.

## <a name="create-an-elastic-query-database"></a>Создание запросов к эластичной базе данных
1. Откройте hello [портал Azure](https://portal.azure.com) и войдите в систему.
2. Создать новую базу данных Azure SQL в hello же сервере, что настройки сегментов. Имя базы данных hello «ElasticDBQuery».

    ![Портал Azure и ценовая категория][3]

    > [!NOTE]
    > Можно использовать существующую базу данных. Если это можно сделать, он не должен быть один из сегментов hello, желательно tooexecute ваших запросов. Эта база данных будет использоваться для создания hello объекты метаданных для запроса эластичной базы данных.
    >

## <a name="create-database-objects"></a>Создание объектов базы данных
### <a name="database-scoped-master-key-and-credentials"></a>Главный ключ и учетные данные для конкретной базы данных
Это диспетчера карты сегментов toohello используется tooconnect и hello сегментов:

1. Откройте SQL Server Management Studio или SQL Server Data Tools в Visual Studio.
2. Подключите tooElasticDBQuery базы данных, выполните следующие команды T-SQL hello:

        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred
        WITH IDENTITY = '<username>',
        SECRET = '<password>';

    «username» и «password» должен быть hello же, как учетные данные, используемые в шаге 6 процедуры [загрузить и запустить пример приложения hello](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app) в [Приступая к работе со средствами эластичной базы данных](sql-database-elastic-scale-get-started.md).

### <a name="external-data-sources"></a>Внешние источники данных
toocreate внешнего источника данных, выполните следующую команду в базе данных ElasticDBQuery hello hello:

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH
      (TYPE = SHARD_MAP_MANAGER,
      LOCATION = '<server_name>.database.windows.net',
      DATABASE_NAME = 'ElasticScaleStarterKit_ShardMapManagerDb',
      CREDENTIAL = ElasticDBQueryCred,
       SHARD_MAP_NAME = 'CustomerIDShardMap'
    ) ;

 «CustomerIDShardMap» — hello имя карты сегментов hello, при создании карты сегментов hello и карты сегментов диспетчера с помощью средства образец hello эластичной базы данных. Тем не менее если вы использовали пользовательские настройки для данного образца, затем следует имя сопоставления сегментов hello, выбранное в приложении.

### <a name="external-tables"></a>Внешние таблицы
Создайте внешнюю таблицу, которая соответствует таблицу Customers hello на сегменты hello, выполнив следующую команду в базе данных ElasticDBQuery hello:

    CREATE EXTERNAL TABLE [dbo].[Customers]
    ( [CustomerId] [int] NOT NULL,
      [Name] [nvarchar](256) NOT NULL,
      [RegionId] [int] NOT NULL)
    WITH
    ( DATA_SOURCE = MyElasticDBQueryDataSrc,
      DISTRIBUTION = SHARDED([CustomerId])
    ) ;

## <a name="execute-a-sample-elastic-database-t-sql-query"></a>Выполнение запроса T-SQL к примеру эластичной базы данных
После определения источника внешних данных и внешних таблиц теперь можно использовать полный T-SQL для внешних таблиц.

Выполните следующий запрос в базе данных ElasticDBQuery hello:

    select count(CustomerId) from [dbo].[Customers]

Можно заметить этого запроса hello объединяет результаты из всех сегментов hello и предоставляет hello следующие выходные данные:

![Сведения о выходных данных][4]

## <a name="import-elastic-database-query-results-tooexcel"></a>Импорт tooExcel результаты запроса эластичной базы данных
 Можно импортировать результаты hello из файла Excel tooan запроса.

1. Запустите Excel 2013.
2. Перейдите toohello **данные** ленты.
3. Щелкните **Из других источников**, а затем — **Из SQL Server**.

   ![Импорт в Excel из других источников][5]
4. В hello **мастер подключения данных** введите учетные данные имя и имя входа сервера hello. Нажмите кнопку **Далее**.
5. В диалоговом окне приветствия **hello выберите базу данных, содержащую данные hello**выберите hello **ElasticDBQuery** базы данных.
6. Выберите hello **клиентов** из таблицы в представлении списка hello и нажмите кнопку **Далее**. Нажмите кнопку **Готово**.
7. В hello **импорта данных** форме, в разделе **выберите способ tooview эти данные в книге**выберите **таблицы** и нажмите кнопку **ОК**.

Здравствуйте, все строки из **клиентов** листа Excel hello заполнение таблицы, хранимые в разных сегментах.

Теперь можно использовать мощные функции Excel по визуализации данных. Можно использовать строку подключения hello именем сервера, имя базы данных и учетные данные tooconnect бизнес-Аналитики и данные интеграции средства toohello запроса эластичной базы данных. Убедитесь, что в качестве источника данных для вашего инструмента поддерживается SQL Server. Можно ссылаться toohello эластичной запрос к базе данных и внешних таблиц так же, как и любой другой базы данных SQL Server и таблицах SQL Server, то для подключения toowith средством.

### <a name="cost"></a>Стоимость
Без дополнительной платы применения функции hello запроса эластичной базы данных не существует.

Сведения о ценах см. на [странице с ценами на базу данных SQL](https://azure.microsoft.com/pricing/details/sql-database/).

## <a name="next-steps"></a>Дальнейшие действия

* Общие сведения об эластичных запросах см. в разделе [Обзор эластичных запросов к базе данных SQL Azure (предварительная версия)](sql-database-elastic-query-overview.md).
* Руководств по вертикальному секционированию см. в статье [Приступая к работе с межбазовыми запросами (вертикальное секционирование) (предварительная версия)](sql-database-elastic-query-getting-started-vertical.md).
* Описание синтаксиса и примеры запросов вертикально секционированных данных см. в разделе [Запрос к нескольким облачным базам данных с разными схемами (предварительная версия)](sql-database-elastic-query-vertical-partitioning.md).
* Описание синтаксиса и примеры запросов горизонтально секционированных данных см. в разделе [Отчеты по масштабируемым облачным базам данных (предварительная версия)](sql-database-elastic-query-horizontal-partitioning.md).
* В описании [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) приведена хранимая процедура, которая выполняет инструкцию Transact-SQL для отдельной удаленной базы данных SQL Azure или набора баз данных, выступающих в качестве сегментов в схеме горизонтального секционирования.


<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
