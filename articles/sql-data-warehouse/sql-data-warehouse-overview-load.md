---
title: "aaaLoad данных в хранилище данных SQL Azure | Документы Microsoft"
description: "Узнайте hello распространенные сценарии загрузку данных в хранилище данных SQL. Они включают использование PolyBase, хранилища BLOB-объектов Azure, неструктурированных файлов и доставки диска. Кроме того, можно использовать сторонние средства."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 2253bf46-cf72-4de7-85ce-f267494d55fa
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: d1a5063f484e9bd95f854e27a4baed512148aad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-azure-sql-data-warehouse"></a>Загрузка данных в хранилище данных Azure SQL
Сводка параметров сценария hello и рекомендации для загрузки данных в хранилище данных SQL.

Hello сложнее всего загрузки данных обычно готовится данных hello hello нагрузки. Azure упрощает загрузку с помощью хранилища BLOB-объектов Azure как общее хранилище данных для многих служб hello и фабрики данных Azure с помощью перемещения tooorchestrate связью и обменом данными между hello служб Azure. Эти процессы интегрированы с технологией PolyBase, которая использует расширенной параллельной обработки данных (MPP) tooload в параллельном режиме из хранилища BLOB-объектов Azure в хранилище данных SQL. 

Инструкции по загрузке образцов баз данных в хранилище данных SQL см. в [этой статье][Load sample databases].

## <a name="load-from-azure-blob-storage"></a>Загрузка из хранилища BLOB-объектов Azure
Hello самый быстрый способ tooimport данные в хранилище данных SQL — toouse PolyBase tooload данные из хранилища BLOB-объектов Azure. PolyBase использует хранилище данных SQL в расширенной параллельной обработки (MPP) разработки tooload данные в параллельном режиме из хранилища BLOB-объектов Azure. toouse PolyBase, можно использовать команды T-SQL или конвейера фабрики данных Azure.

### <a name="1-use-polybase-and-t-sql"></a>1. Использование PolyBase и T-SQL
Процесс загрузки:

1. Переместить в хранилище больших двоичных объектов tooAzure данных или хранилища Озера данных Azure и их сохранения в текстовых файлах.
2. Настройка внешних объектов в хранилище данных SQL toodefine hello расположение и формат данных hello
3. Параллельное выполнение данных hello tooload команды T-SQL в новую таблицу базы данных.

<!-- 5. Schedule and run a loading job. --> 

См. в разделе [загрузки данных из хранилища BLOB-объектов Azure tooSQL хранилище данных (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].

### <a name="2-use-azure-data-factory"></a>2. Использование фабрики данных Azure
Для более простой способ toouse PolyBase можно создать конвейера фабрики данных Azure, использующей данные tooload PolyBase из хранилища BLOB-объектов Azure в хранилище данных SQL. Это быстрый tooconfigure, поскольку объекты T-SQL toodefine hello не требуется. Если вам требуется tooquery hello внешних данных без их импорта, используйте T-SQL. 

Процесс загрузки:

1. Переместить хранилище данных tooAzure BLOB-объектов и их сохранения в текстовых файлах. Сейчас фабрика данных Azure не поддерживает подключение к ADLS с использованием PolyBase.
2. Создайте данных hello tooingest конвейера фабрики данных Azure. Используйте параметр PolyBase hello.
4. Планирование и выполнение конвейера hello.

См. в разделе [загрузки данных из хранилища BLOB-объектов Azure tooSQL хранилище данных (фабрики данных Azure)][Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)].

## <a name="load-from-sql-server"></a>Загрузка из SQL Server
tooload tooSQL SQL Server Integration Services (SSIS) можно использовать хранилище данных передачи плоских файлов или поставлен tooMicrosoft дисков. Чтение toosee Сводка hello различных загрузке tootutorials процессы и ссылки.

tooplan перехода полного набора данных с SQL Server tooSQL хранилища данных. в разделе hello [Общие сведения о миграции][Migration overview]. 

### <a name="use-integration-services-ssis"></a>Использование служб интеграции (SSIS)
Если вы уже используете tooload пакеты Integration Services (SSIS) в SQL Server, можно обновить toouse вашей пакетов SQL Server, как исходный hello и хранилище данных SQL в качестве назначения hello. Это быстрый и простой toodo и является хорошим выбором, если вы не пытаетесь toomigrate вашей загрузки обработки данных toouse уже в облаке hello. компромисс Hello является hello нагрузки будет работать медленнее, чем с помощью PolyBase, так как это служб SSIS не нагрузки hello параллельного выполнения.

Процесс загрузки:

1. Измените экземпляр службы интеграции пакета toopoint toohello SQL Server для hello источника и базы данных хранилища данных SQL hello для назначения hello.
2. Перенос вашей tooSQL схемы хранилища данных, если он еще не существует.
3. Изменить сопоставление hello в пакеты используют только hello типы данных, поддерживаемые хранилищем данных SQL.
4. Планирование и запуск пакета hello.

См. в разделе [загрузки данных из SQL Server tooAzure хранилища данных SQL (SSIS)][Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)].

### <a name="use-azcopy-recommended-for--10-tb-data"></a>Использование AZCopy (рекомендуется при объеме данных меньше 10 ТБ)
Если размер данных < 10 ТБ, можно экспортировать hello данные из файлов tooflat SQL Server, скопируйте хранилища больших двоичных объектов tooAzure hello файлы и затем использовать PolyBase tooload hello данных в хранилище данных SQL

Процесс загрузки:

1. Используйте hello bcp программы командной строки tooexport данные из файлов tooflat SQL Server.
2. Используйте hello AZCopy программы командной строки toocopy данные из хранилища больших двоичных объектов tooAzure неструктурированных файлов.
3. Используйте PolyBase tooload в хранилище данных SQL.

См. в разделе [загрузки данных из хранилища BLOB-объектов Azure tooSQL хранилище данных (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].

### <a name="use-bcp"></a>Использование программы bcp
Если у вас есть небольшой объем данных bcp tooload можно использовать непосредственно в хранилище данных SQL Azure.

Процесс загрузки:

1. Используйте hello bcp программы командной строки tooexport данные из файлов tooflat SQL Server.
2. Использовать bcp tooload данные из неструктурированных файлов непосредственно tooSQL хранилища данных.

См. в разделе [загрузки данных из SQL Server tooAzure хранилище данных SQL (bcp)][Load data from SQL Server tooAzure SQL Data Warehouse (bcp)].

### <a name="use-importexport-recommended-for--10-tb-data"></a>Использование импорта и экспорта (рекомендуется при объеме данных меньше 10 ТБ)
Если размер данных > 10 ТБ и предполагается toomove его tooAzure, мы рекомендуем использовать наши диска доставки службы [импорта и экспорта][Import/Export]. 

Процесс загрузки:

1. Используйте hello bcp программы командной строки tooexport данные из файлов tooflat SQL Server на переносимые дисков.
2. Поставка tooMicrosoft диски hello.
3. Microsoft загружает hello данные в хранилище данных SQL

## <a name="load-from-hdinsight"></a>Загрузка из HDInsight
Хранилище данных SQL поддерживает загрузку данных из HDInsight через PolyBase. процесс Hello hello такой же, как загрузка данных из хранилища больших двоичных объектов — с помощью PolyBase tooconnect tooHDInsight tooload данных. 

### <a name="1-use-polybase-and-t-sql"></a>1. Использование PolyBase и T-SQL
Процесс загрузки:

1. Перемещение вашей tooHDInsight данных и сохранить ее в текстовых файлах, формат ORC или Parquet.
2. Настройка внешних объектов в хранилище данных SQL toodefine hello расположение и формат данных hello.
3. Параллельное выполнение данных hello tooload команды T-SQL в новую таблицу базы данных.

См. в разделе [загрузки данных из хранилища BLOB-объектов Azure tooSQL хранилище данных (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].

## <a name="recommendations"></a>Рекомендации
Многие из наших партнеров предлагают решения для загрузки. toofind подробные сведения, см. список наших [решения партнеров][solution partners]. 

Если будут поступать данные из источника нереляционных tooload его в данных SQL в хранилище вам потребуется tootransform его в виде строк и столбцов перед их загрузкой. Hello преобразования данных не должны toobe в базе данных, могут храниться в текстовых файлах.

Создание статистики для вновь загруженных данных Хранилище данных SQL Azure пока не поддерживает автоматическое создание или автоматическое обновление статистики.  В порядке tooget hello наилучшей производительности запросов очень важно сначала загрузите toocreate статистику для всех столбцов всех таблиц после hello или любые существенные изменения происходят в данных hello.  Дополнительные сведения см. в статье [Управление статистикой таблиц в хранилище данных SQL][Statistics].

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные советы по разработке в разделе hello [Общие сведения о разработке][development overview].

<!--Image references-->

<!--Article references-->
[Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md
[Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)]: ./sql-data-warehouse-load-from-sql-server-with-integration-services.md
[Load data from SQL Server tooAzure SQL Data Warehouse (bcp)]: ./sql-data-warehouse-load-from-sql-server-with-bcp.md
[Load data from SQL Server tooAzure SQL Data Warehouse (AZCopy)]: ./sql-data-warehouse-load-from-sql-server-with-azcopy.md

[Load sample databases]: ./sql-data-warehouse-load-sample-databases.md
[Migration overview]: ./sql-data-warehouse-overview-migrate.md
[solution partners]: ./sql-data-warehouse-partner-business-intelligence.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->

<!--Other Web references-->
[Import/Export]: https://azure.microsoft.com/documentation/articles/storage-import-export-service/
