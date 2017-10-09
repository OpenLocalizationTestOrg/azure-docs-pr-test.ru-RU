---
title: "руководство по aaaDesign для реплицированных таблиц - хранилище данных SQL Azure | Документы Microsoft"
description: "Рекомендации по проектированию реплицированных таблиц в схеме хранилища данных SQL Azure."
services: sql-data-warehouse
documentationcenter: NA
author: ronortloff
manager: jhubbard
editor: 
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 07/14/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 5d405b8c404c65177b387ba959126839c1cf8799
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="design-guidance-for-using-replicated-tables-in-azure-sql-data-warehouse"></a>Руководство по проектированию для использования реплицированных таблиц в хранилище данных SQL Azure
В данной статье представлены рекомендации по проектированию реплицированных таблиц в схеме хранилища данных SQL Azure. Используйте эти рекомендации tooimprove производительность за счет уменьшения сложности перемещения и запроса данных.

> [!NOTE]
> компонент Hello реплицируемой таблицы в настоящее время находится в общедоступной предварительной версии. Некоторые поведения — это toochange субъекта.
> 

## <a name="prerequisites"></a>Предварительные требования
В этой статье предполагается, что вы знакомы с распределением данных и основными понятиями перемещения данных в хранилище данных SQL.  Дополнительные сведения см. в статье [Распределенные данные](sql-data-warehouse-distributed-data.md). 

Как часть структуры таблиц понять, насколько возможно, связанные с данными и как выполнять запросы к данным hello.  Например, для этого можно использовать следующие вопросы:

- Размер таблицы hello?   
- Как часто обновлять таблицы hello   
- Имеются ли в хранилище данных таблицы фактов и таблицы измерений?   

## <a name="what-is-a-replicated-table"></a>Что такое реплицированная таблица?
Реплицированные таблицы имеет полную копию таблицы hello доступны на каждом вычислительном узле. Таблицы репликации удаляет данные tootransfer необходимость hello среди вычислительных узлов перед соединения или статистической обработки. Поскольку таблица hello имеет несколько копий, реплицированные таблицы лучше всего при размере таблицы hello сжатые меньше, чем 2 ГБ.

Hello следующей диаграмме показан реплицируемой таблицы, доступной на каждом вычислительном узле. В хранилище данных SQL hello реплицируемой таблицы является полностью копируются tooa базы данных распространителя на каждом вычислительном узле. 

![Реплицируемая таблица](media/guidance-for-using-replicated-tables/replicated-table.png "Реплицируемая таблица")  

Реплицированные таблицы отлично подходят для небольших таблиц измерения в схеме типа "звезда". Таблицы измерений обычно имеют размер, который делает возможным toostore и поддерживать несколько экземпляров. В измерениях хранятся описательные данные, которые изменяются редко, например имя и адрес клиента, а также сведения о продукте. Hello медленно изменяющихся характер данных hello приводит перестроение toofewer hello реплицируемой таблицы. 

Реплицированные таблицы подходят в ситуациях, когда:

- размер таблицы Hello на диске — меньше, чем 2 ГБ, вне зависимости от hello количество строк. размер hello toofind таблицы, можно использовать hello [DBCC PDW_SHOWSPACEUSED](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql) команды: `DBCC PDW_SHOWSPACEUSED('ReplTableCandidate')`. 
- Таблица Hello используется в соединениях, которые в противном случае потребуется перемещение данных. Например соединение в таблицах, распределенных хэш требует перемещения данных hello присоединяемый столбцы не являются hello же столбец распределения. Если одна из таблиц распределенного хэш hello мал, рассмотрите возможность реплицируемой таблицы. Для соединения в таблице с распределением методом циклического перебора требуется перемещение данных. В большинстве случаев вместо таких таблиц рекомендуется использовать реплицированные таблицы. 


Рассмотрите возможность преобразования существующего распределенного tooa таблицы реплицируются таблицу при:

- Использование операций перемещения данных, передающих hello данных tooall hello вычислительные узлы планы запроса. Hello BroadcastMoveOperation расходуется и снижает производительность запросов. использовать tooview операций перемещения данных в планах запросов [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql).
 
Реплицированные таблицы не может привести к hello лучшую производительность при:

- Таблица Hello имеет часто вставки, обновления и удаления операций. Эти операций языка обработки данных требуется повторное создание таблицы реплицируются hello. Зачастую перестроение приводит к снижению производительности.
- часто масштабируется Hello хранилища данных. Масштабирование хранилище данных изменяется hello количество вычислительных узлов, что влечет за собой повторное построение.
- Hello таблица содержит много столбцов, но данные обычно доступ только небольшое число столбцов. В этом случае вместо репликации hello всю таблицу, возможно, более эффективные toohash распространения hello таблицу и затем создать индекс для hello часто используемых столбцов. Когда запрос требует перемещения данных, хранилище данных SQL, перенос данных в hello запросить столбцы всего. 



## <a name="use-replicated-tables-with-simple-query-predicates"></a>Использование реплицированных таблиц с предикатами простого запроса
Прежде чем выбрать toodistribute или репликации таблицы, подумайте о hello типов запросов плана toorun hello для таблицы. Когда это возможно:

- Используйте реплицированные таблицы для запросов с предикатами простого запроса, например равенства или неравенства.
- Используйте распределенные таблицы для запросов с предикатами сложного запроса, например LIKE или NOT LIKE.

Процессор запросов выполните лучше всего при hello работа распределяется по всем hello вычислительных узлов. Например, запросы, которые запускают вычисления для каждой строки таблицы, выполняются более эффективно в распределенных таблицах, чем реплицированных. Поскольку реплицируемой таблицы хранятся в полном объеме на каждом вычислительном узле, процессор запрос к реплицируемой таблицы запускает hello всю таблицу на каждом вычислительном узле. Hello лишние вычисления может снизить производительность запроса.

Например, в этом запросе содержится сложный предикат.  Он выполняется быстрее, когда в качестве поставщика выступает распределенная таблица вместо реплицированной таблицы. В этом примере для поставщика можно выполнить хэш-распределение или распределение методом циклического перебора.

```sql

SELECT EnglishProductName 
FROM DimProduct 
WHERE EnglishDescription LIKE '%frame%comfortable%'

```

## <a name="convert-existing-round-robin-tables-tooreplicated-tables"></a>Преобразование существующих таблиц tooreplicated таблиц циклический перебор
При наличии таблиц циклический перебор, рекомендуется их преобразования tooreplicated таблицы, если они удовлетворяют условиям, приведенным в этой статье. Реплицированные таблицы повышает производительность для циклического таблицы так, как они устраняют необходимость hello для перемещения данных.  Для соединений в циклической таблице всегда требуется перемещение данных. 

В этом примере используется [CTAS](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) tooa таблицы DimSalesTerritory hello toochange реплицированная таблица. В данном примере неважно, была ли таблица DimSalesTerritory хэш-распределена или распределена методом циклического перебора.

```sql
CREATE TABLE [dbo].[DimSalesTerritory_REPLICATE]   
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = REPLICATE  
  )  
AS SELECT * FROM [dbo].[DimSalesTerritory]
OPTION  (LABEL  = 'CTAS : DimSalesTerritory_REPLICATE') 

--Create statistics on new table
CREATE STATISTICS [SalesTerritoryKey] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryKey]);
CREATE STATISTICS [SalesTerritoryAlternateKey] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryAlternateKey]);
CREATE STATISTICS [SalesTerritoryRegion] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryRegion]);
CREATE STATISTICS [SalesTerritoryCountry] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryCountry]);
CREATE STATISTICS [SalesTerritoryGroup] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryGroup]);

-- Switch table names
RENAME OBJECT [dbo].[DimSalesTerritory] too[DimSalesTerritory_old];
RENAME OBJECT [dbo].[DimSalesTerritory_REPLICATE] too[DimSalesTerritory];

DROP TABLE [dbo].[DimSalesTerritory_old];
```  

### <a name="query-performance-example-for-round-robin-versus-replicated"></a>Пример производительности запросов для циклической и реплицированной таблиц 

Поскольку hello вся таблица уже существует на каждом вычислительном узле реплицируемой таблицы не требует перемещения данных для соединения. Циклического распределенных таблиц измерений hello, соединение копирует hello таблицу измерения в полной tooeach вычислительных узлов. данные toomove hello, hello план запроса содержит эта операция называется BroadcastMoveOperation. Операции перемещения данных данного типа снижают производительность запросов. Устранить это можно с помощью реплицированных таблиц. действия плана запроса tooview, использовать hello [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql) представления системного каталога. 

Например, в следующем запросе к схема AdventureWorks hello hello ` FactInternetSales` таблицы распределенных хэш. Hello `DimDate` и `DimSalesTerritory` меньшего размера таблицы измерения. Этот запрос возвращает hello общий объем продаж в Северной Америке для 2004 финансовом году.
 
```sql
SELECT [TotalSalesAmount] = SUM(SalesAmount)
FROM dbo.FactInternetSales s
INNER JOIN dbo.DimDate d
  ON d.DateKey = s.OrderDateKey
INNER JOIN dbo.DimSalesTerritory t
  ON t.SalesTerritoryKey = s.SalesTerritoryKey
WHERE d.FiscalYear = 2004
  AND t.SalesTerritoryGroup = 'North America'
```
Мы повторно создали таблицы `DimDate` и `DimSalesTerritory` как циклические таблицы. В результате запроса hello показал hello, следуя плана запроса, который имеет несколько вещания переноса операций: 
 
![План запроса с циклическим перебором](media/design-guidance-for-replicated-tables/round-robin-tables-query-plan.jpg) 

Повторно создан `DimDate` и `DimSalesTerritory` как в реплицированных таблицах и запущена hello запрос повторно. Hello результирующий план запроса намного короче, и не иметь любой передает переход.

![План запроса с репликацией](media/design-guidance-for-replicated-tables/replicated-tables-query-plan.jpg) 


## <a name="performance-considerations-for-modifying-replicated-tables"></a>Рекомендации по повышению производительности для изменения реплицированных таблиц
Хранилище данных SQL реализует реплицированной таблицы, сохраняя главной версии таблицы hello. Он копирует hello базы данных распространителя главной версии tooone на каждом вычислительном узле. При наличии изменений, хранилище данных SQL обновляет сначала hello главную таблицу. Затем он требуется повторное создание таблиц hello на каждом вычислительном узле. Перестроение реплицируемой таблицы включает копирование hello таблицы tooeach вычислительных узлов и последующее перестроение индексов hello.

Перестроение требуется после следующего:
- Загрузка или изменение данных
- хранилище данных Hello — другой параметр DWU масштабированный tooa
- Обновление определения таблицы

Перестроение не требуется после следующего:
- Выполнение операции приостановки
- Выполнение операции возобновления

Перестроение Hello не происходит немедленно после изменения данных. Вместо этого hello перестройка инициируется hello первый раз, запрос выбирает данные из таблицы hello.  В инструкции select начальной hello из таблицы hello находятся действия toorebuild hello реплицируемой таблицы.  Так как в запросе hello выполняется перестроение hello, hello влияние toohello начальной инструкции select может быть значительной в зависимости от размера таблицы hello hello.  Если участвуют несколько реплицируемых таблиц, требующие повторной сборки, каждая копия будет перестроен последовательно как действия в рамках инструкции hello.  согласованность данных toomaintain во время перестроения hello hello реплицируются hello таблице применяется монопольная блокировка таблицы.  Hello Блокировка предотвращает все таблицы access toohello hello время перестроения hello. 

### <a name="use-indexes-conservatively"></a>Консервативный подход к использованию индексов
Стандартные рекомендации индексирования относятся tooreplicated таблиц. Хранилище данных SQL перестраивает каждый индекс реплицируемой таблицы в процессе перестроения hello. Используйте индексы только в том случае, если hello выигрыш в производительности перевешивает стоимость hello перестроение индексов hello.  
 
### <a name="batch-data-loads"></a>Пакетная загрузка данных
При загрузке данных в реплицированных таблицах, попробуйте toominimize перестроение путем объединения загружает пакет. Выполните все загрузки hello в пакетном режиме, перед выполнением инструкции select.

Например, ниже представлен шаблон загрузки данных из четырех источников и запуска четырех операций перестроения. 

- Загрузка из источника 1.
- Инструкция SELECT вызывает перестроение 1.
- Загрузка из источника 2.
- Инструкция SELECT вызывает перестроение 2.
- Загрузка из источника 3.
- Инструкция SELECT вызывает перестроение 3.
- Загрузка из источника 4.
- Инструкция SELECT вызывает перестроение 4.

Например, ниже представлен шаблон загрузки данных из четырех источников и запуска только одной операции перестроения.

- Загрузка из источника 1.
- Загрузка из источника 2.
- Загрузка из источника 3.
- Загрузка из источника 4.
- Инструкция SELECT вызывает перестроение.


### <a name="rebuild-a-replicated-table-after-a-batch-load"></a>Перестроение реплицированной таблицы после пакетной загрузки
tooensure согласованного выполнения запросов, рекомендуется принудительное обновление таблиц, реплицированных hello после загрузки пакета. В противном случае — первый запрос hello должен ожидать toorefresh hello таблиц, включая перестроение индексов hello. В зависимости от размера hello и количество затронутых реплицированных таблицах влияние на производительность hello может оказаться значительным.  

Этот запрос использует hello [sys.pdw_replicated_table_cache_state](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-pdw-replicated-table-cache-state-transact-sql) hello toolist динамического административного Представления в реплицированных таблицах, которые были изменены, но не может быть перестроен.

```sql 
SELECT [ReplicatedTable] = t.[name]
  FROM sys.tables t  
  JOIN sys.pdw_replicated_table_cache_state c  
    ON c.object_id = t.object_id 
  JOIN sys.pdw_table_distribution_properties p 
    ON p.object_id = t.object_id 
  WHERE c.[state] = 'NotReady'
    AND p.[distribution_policy_desc] = 'REPLICATE'
```
 
tooforce перестроения, запустите следующие инструкции для каждой таблицы в предшествующих выходных данных hello hello. 

```sql
SELECT TOP 1 * FROM [ReplicatedTable]
``` 
 
## <a name="next-steps"></a>Дальнейшие действия 
toocreate реплицированной таблицы, используйте один из следующих инструкций:

- [CREATE TABLE (хранилище данных Azure SQL)](https://docs.microsoft.com/sql/t-sql/statements/create-table-azure-sql-data-warehouse)
- [CREATE TABLE AS SELECT (хранилище данных Azure SQL)](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse)

Обзор распределенных таблиц см. в разделе [Распределенные таблицы](sql-data-warehouse-tables-distribute.md).



