---
title: "aaaGetting работы с Темпоральными таблицами в базе данных SQL Azure | Документы Microsoft"
description: "Узнайте, как tooget запущена с использованием временных таблиц в базе данных SQL Azure."
services: sql-database
documentationcenter: 
author: bonova
manager: jhubbard
editor: 
ms.assetid: c8c0f232-0751-4a7f-a36e-67a0b29fa1b8
ms.service: sql-database
ms.custom: develop databases
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sql-database
ms.date: 01/10/2017
ms.author: bonova
ms.openlocfilehash: 54f394b51df07aa2f9bb299f207e692171d23479
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-temporal-tables-in-azure-sql-database"></a>Приступая к работе с временными таблицами в базе данных SQL Azure
Темпоральные таблицы являются новой возможностью программирования базы данных SQL Azure, который позволяет вам tootrack и анализировать hello полный журнал изменений в данных, без необходимости hello дополнительного кода. Временных таблиц хранить тесно связанных tootime контекст данных, чтобы хранимых фактах можно интерпретировать как допустимый только в течение определенного периода hello. Эта особенность временных таблиц дает возможность эффективно выполнять анализ с учетом времени и получать ценную информацию об эволюции данных.

## <a name="temporal-scenario"></a>Сценарий использования временных таблиц
В этой статье рассмотрены hello действия tooutilize временных таблиц в рабочих приложениях. Предположим, что вы хотите tootrack действиями пользователя на новый веб-сайт, разработанного с нуля или на существующий веб-сайт, которые должны tooextend с аналитикой действия пользователя. В этом упрощенном примере предполагается, что число hello посещенные веб-страниц за период времени является признаком того, что требуется toobe захвата и наблюдения за веб-сайт hello базы данных, которая размещается в базе данных SQL Azure. Цель Hello hello исторического анализа активности пользователей веб-сайт tooredesign tooget входных данных и укажите для повышения удобства для посетителей hello.

Hello модели базы данных в этом сценарии очень прост — представлены метрика действия пользователя с одним целочисленным полем, **PageVisited**и фиксируется, а также основные сведения о профиле пользователя hello. Кроме того для анализа на основе времени, позволит набор строк для каждого пользователя, где каждая строка представляет hello количество страниц, посещения определенного пользователем в течение определенного периода времени.

![Схема](./media/sql-database-temporal-tables/AzureTemporal1.png)

К счастью, нет необходимости tooput никаких действий в toomaintain вашего приложения эти сведения для действия. С Темпоральными таблицами этот процесс выполняется автоматически - что дает полную гибкость во время создания веб-сайта и дополнительные toofocus времени на hello самого анализа данных. Здравствуйте, только что toodo tooensure, **WebSiteInfo** таблица настроена как [темпоральной с системным управлением версиями](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_0). конкретные шаги Hello tooutilize временных таблиц в этом сценарии описаны ниже.

## <a name="step-1-configure-tables-as-temporal"></a>Шаг 1. Настройка таблиц в качестве временных
В зависимости от того, начинаете вы разработку новых приложений или обновляете существующее приложение, вы создадите временные таблицы или измените существующие, добавляя в них временные атрибуты. В общем случае может потребоваться сделать и то, и другое. Выполните это с помощью [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) (SSMS), [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) (SSDT) или любого другого средства для разработки Transact-SQL.

> [!IMPORTANT]
> Рекомендуется всегда использовать hello последнюю версию среды Management Studio tooremain синхронизированы с tooMicrosoft обновления Azure и базы данных SQL. [Обновите среду SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).
> 
> 

### <a name="create-new-table"></a>Создание новой таблицы
Используйте пункт контекстного меню «Новой таблицы с системным управлением версиями» в редакторе запросов hello tooopen обозревателя объектов SSMS с помощью шаблона сценария временная таблица, а затем использовать шаблон hello toopopulate «Укажите значения для параметров шаблона» (Ctrl + Shift + M).

![SSMSNewTable](./media/sql-database-temporal-tables/AzureTemporal2.png)

В SSDT выбрали шаблона «Временная таблица (с системным управлением версиями)», при добавлении нового проекта базы данных toohello элементы. Что будет конструктор открыть таблицу и включить tooeasily можно указать hello таблице макета:

![SSDTNewTable](./media/sql-database-temporal-tables/AzureTemporal3.png)

Вы также можете создания темпоральной таблицы путем указания инструкции Transact-SQL hello напрямую, как показано в приведенном ниже примере hello. Обратите внимание, что hello обязательные элементы всех темпоральных таблиц определения ПЕРИОДА hello и предложение SYSTEM_VERSIONING hello со ссылочной таблице tooanother пользователя, который будет сохранять предыдущие версии строк:

````
CREATE TABLE WebsiteUserInfo 
(  
    [UserID] int NOT NULL PRIMARY KEY CLUSTERED 
  , [UserName] nvarchar(100) NOT NULL
  , [PagesVisited] int NOT NULL 
  , [ValidFrom] datetime2 (0) GENERATED ALWAYS AS ROW START
  , [ValidTo] datetime2 (0) GENERATED ALWAYS AS ROW END
  , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)
 )  
 WITH (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.WebsiteUserInfoHistory));
````

При создании таблицы с системным управлением версиями темпоральной таблицы журнала с конфигурацией по умолчанию hello, сопровождающие hello создается автоматически. Таблица журнала по умолчанию Hello содержит кластеризованный индекс сбалансированного дерева для столбцов периода hello (конец, начало) с включенным сжатием страниц. Эта конфигурация является оптимальной для hello в большинстве случаев, в которых используются временных таблиц, особенно для [аудит данных](https://msdn.microsoft.com/library/mt631669.aspx#Anchor_0). 

В данном случае мы цель анализа тенденций на основе времени tooperform за более длительный журнал данных и с крупными наборами данных, поэтому hello вариант хранилища для таблицы журнала hello в кластеризованном индексе. Кластеризованный индекс columnstore обеспечивает очень хорошее сжатие и производительность аналитических запросов. Временных таблиц предоставьте hello индексы tooconfigure гибкость hello текущих и временных таблиц в совершенно независимо друг от друга. 

> [!NOTE]
> Индексы ColumnStore доступны только для уровня служб premium hello.
>

Привет, выполнив сценарий показывает, как индекс по умолчанию для таблицы журнала можно измененные toohello clustered columnstore:

````
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory
ON dbo.WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON); 
````

Временных таблиц представлены в hello обозревателя объектов с hello определенный значок для удобства идентификации, пока соответствующей таблицей журнала отображается как дочерний узел.

![AlterTable](./media/sql-database-temporal-tables/AzureTemporal4.png)

### <a name="alter-existing-table-tootemporal"></a>Изменять существующие таблицы tootemporal
Давайте охватывают hello альтернативного сценария, в какие hello WebsiteUserInfo таблица уже существует, но не спроектированных tookeep журнал изменений. В этом случае можно просто дополнить hello существующие таблицы toobecome темпоральной, как показано в следующий пример hello:

````
ALTER TABLE WebsiteUserInfo 
ADD 
    ValidFrom datetime2 (0) GENERATED ALWAYS AS ROW START HIDDEN  
        constraint DF_ValidFrom DEFAULT DATEADD(SECOND, -1, SYSUTCDATETIME())
    , ValidTo datetime2 (0)  GENERATED ALWAYS AS ROW END HIDDEN   
        constraint DF_ValidTo DEFAULT '9999.12.31 23:59:59.99'
    , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo); 

ALTER TABLE WebsiteUserInfo  
SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.WebsiteUserInfoHistory));
GO

CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory
ON dbo.WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON); 
````

## <a name="step-2-run-your-workload-regularly"></a>Шаг 2. Регулярный запуск рабочей нагрузки
главным преимуществом Hello временных таблиц — не требуется toochange или настроить веб-сайт в системе отслеживания изменений tooperform любой способ. После создания временных таблиц в них прозрачно сохраняются предыдущие версии строк каждый раз, когда вы вносите изменения в данные. 

В порядке tooleverage автоматическое отслеживание изменений для этой конкретной ситуации, давайте просто обновить столбец **PagesVisited** каждый раз, когда пользователь завершает сеанс, her/his на веб-сайте hello:

````
UPDATE WebsiteUserInfo  SET [PagesVisited] = 5 
WHERE [UserID] = 1;
````

Очень важно, что toonotice, hello запрос на обновление не требуется tooknow hello точное время возникновения фактическая операция hello, ни как данные журнала сохраняются для последующего анализа. Оба аспекты автоматически обрабатываются hello базы данных SQL Azure. Hello следующая диаграмма иллюстрирует методом формирования данных журнала на каждое обновление.

![TemporalArchitecture](./media/sql-database-temporal-tables/AzureTemporal5.png)

## <a name="step-3-perform-historical-data-analysis"></a>Шаг 3. Анализ данных журнала
Теперь, когда временное управления версиями системой включено, анализ данных журнала — дело всего одного запроса. В этой статье мы предоставить несколько примеров, которые устраняют распространенные сценарии анализа - toolearn все сведения, варианты предварен hello [FOR SYSTEM_TIME](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_3) предложения.

toosee hello top 10 пользователей, упорядоченных по номеру hello посещенные веб-страниц на один час назад, выполните этот запрос.

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
SELECT TOP 10 * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME AS OF @hourAgo
ORDER BY PagesVisited DESC
````

Этот запрос можно легко изменить сайт hello tooanalyze посещает начиная с дня назад, месяц назад или в любой момент в прошлом hello нужно.

Основные статистического анализа tooperform для hello предыдущий день, используйте следующий пример hello:

````
DECLARE @twoDaysAgo datetime2 = DATEADD(DAY, -2, SYSUTCDATETIME());
DECLARE @aDayAgo datetime2 = DATEADD(DAY, -1, SYSUTCDATETIME());

SELECT UserID, SUM (PagesVisited) as TotalVisitedPages, AVG (PagesVisited) as AverageVisitedPages,
MAX (PagesVisited) AS MaxVisitedPages, MIN (PagesVisited) AS MinVisitedPages,
STDEV (PagesVisited) as StDevViistedPages
FROM dbo.WebsiteUserInfo 
FOR SYSTEM_TIME BETWEEN @twoDaysAgo AND @aDayAgo
GROUP BY UserId
````

toosearch для действий конкретного пользователя, в течение периода времени, предложение CONTAINED IN hello используйте:

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
DECLARE @twoHoursAgo datetime2 = DATEADD(HOUR, -2, SYSUTCDATETIME());
SELECT * FROM dbo.WebsiteUserInfo 
FOR SYSTEM_TIME CONTAINED IN (@twoHoursAgo, @hourAgo)
WHERE [UserID] = 1;
````

Графическое представление особенно удобно для временных запросов, так как можно отобразить тенденции и закономерности использования доступным и интуитивно понятным способом.

![TemporalGraph](./media/sql-database-temporal-tables/AzureTemporal6.png)

## <a name="evolving-table-schema"></a>Развитие схемы таблицы
Как правило необходимо будет toochange hello временная таблица схемы во время разработки приложения. Для этого просто запустите инструкций ALTER TABLE и базы данных SQL Azure надлежащим образом будет распространено таблицы журнала toohello изменения. Hello следующий сценарий показывает, как можно добавить дополнительный атрибут для отслеживания:

````
/*Add new column for tracking source IP address*/
ALTER TABLE dbo.WebsiteUserInfo 
ADD  [IPAddress] varchar(128) NOT NULL CONSTRAINT DF_Address DEFAULT 'N/A';
````

Аналогичным образом можно изменить определение столбца при активной рабочей нагрузке.

````
/*Increase hello length of name column*/
ALTER TABLE dbo.WebsiteUserInfo 
    ALTER COLUMN  UserName nvarchar(256) NOT NULL;
````

Наконец, можно удалить столбец, который больше не нужен.

````
/*Drop unnecessary column */
ALTER TABLE dbo.WebsiteUserInfo 
    DROP COLUMN TemporaryColumn; 
````

Также можно использовать последнюю версию [SSDT](https://msdn.microsoft.com/library/mt204009.aspx) toochange временная схема таблицы, пока вы находитесь toohello подключенной базы данных (интерактивный режим) или как часть проекта базы данных hello (автономный режим).

## <a name="controlling-retention-of-historical-data"></a>Управление периодом удержания данных журнала
С темпоральными таблицами с системным управлением версиями таблица журнала hello может увеличить размер базы данных hello больше, чем обычные таблицы. Большой и постоянно растущий объем таблицы журнала может стать проблемой не только из-за затрат на хранение toopure, а также налагающий производительности при выполнении темпоральных запросов. Таким образом Разработка политики хранения данных для управления данными в таблице журнала hello является важным аспектом планирования и управления жизненным циклом всех темпоральных таблиц hello. С базой данных SQL Azure у вас есть следующие подходы к управлению данными журнала в темпоральной таблице hello hello:

* [Секционирование таблиц.](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_2)
* [Пользовательский сценарий очистки](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_3)

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о темпоральных таблицах см. в [документации MSDN](https://msdn.microsoft.com/library/dn935015.aspx).
Посетите Channel 9 toohear [историю успеха temporal выполнению реальных клиентских](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) » и «Контрольное [live temporal демонстрации](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).

