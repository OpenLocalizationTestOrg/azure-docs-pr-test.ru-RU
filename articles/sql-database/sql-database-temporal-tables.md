---
title: "Приступая к работе с темпоральными таблицами в базе данных SQL Azure | Документация Майкрософт"
description: "Узнайте, как приступить к работе с временными таблицами в базе данных SQL Azure."
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
ms.openlocfilehash: d84db682089c65c2716d2d9bd92f7bc0ac47af27
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-temporal-tables-in-azure-sql-database"></a>Приступая к работе с временными таблицами в базе данных SQL Azure
Временные таблицы — это новая программная возможность базы данных SQL Azure, которая позволяет отслеживать и анализировать полный журнал изменений в данных, не создавая какого-либо дополнительного пользовательского кода. Во временных таблицах хранятся данные, тесно связанные с контекстом времени, чтобы хранимые факты можно было интерпретировать как действительные только в течение определенного периода. Эта особенность временных таблиц дает возможность эффективно выполнять анализ с учетом времени и получать ценную информацию об эволюции данных.

## <a name="temporal-scenario"></a>Сценарий использования временных таблиц
В данной статье показана последовательность действий для использования временных таблиц в прикладном сценарии. Предположим, что вам нужно отслеживать активность пользователей на новом веб-сайте, который разрабатывался с нуля, или на существующем веб-сайте, который вы хотите дополнить возможностями анализа активности пользователей. В этом упрощенном примере предположим, что количество посещаемых веб-страниц за определенный период времени является показателем, который необходимо записывать и отслеживать в базе данных веб-сайта, размещенной в базе данных SQL Azure. Цель исторического анализа активности пользователей — получить входные данные для переработки веб-сайта и улучшения его взаимодействия с посетителями.

Модель базы данных в этом сценарии очень простая: метрика активности пользователей представлена одним целочисленным полем, **PageVisited**, а ее значение записывается вместе с основными сведениями в профиле пользователя. Кроме того, для анализа с учетом времени следует выделить набор строк для каждого пользователя, где каждая строка представляет число страниц, посещенных определенным пользователем в течение определенного периода времени.

![Схема](./media/sql-database-temporal-tables/AzureTemporal1.png)

К счастью, вам не нужно программировать хранение этой информации об активности в приложении. Благодаря временным таблицам этот процесс автоматизирован, что обеспечивает абсолютную гибкость во время разработки веб-сайта и позволяет больше времени уделить непосредственно анализу данных. Единственное, что необходимо сделать, — убедиться, что таблица **WebSiteInfo** настроена как [временная с системным управлением версиями](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_0). Конкретные шаги по использованию временных таблиц в этом сценарии описаны ниже.

## <a name="step-1-configure-tables-as-temporal"></a>Шаг 1. Настройка таблиц в качестве временных
В зависимости от того, начинаете вы разработку новых приложений или обновляете существующее приложение, вы создадите временные таблицы или измените существующие, добавляя в них временные атрибуты. В общем случае может потребоваться сделать и то, и другое. Выполните это с помощью [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) (SSMS), [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) (SSDT) или любого другого средства для разработки Transact-SQL.

> [!IMPORTANT]
> Чтобы обеспечить синхронизацию с обновлениями Microsoft Azure и Базой данных SQL, рекомендуется всегда использовать последнюю версию Management Studio. [Обновите среду SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).
> 
> 

### <a name="create-new-table"></a>Создание новой таблицы
Используйте пункт контекстного меню "New System-Versioned Table" (Новая таблица с системным управлением версиями) в обозревателе объектов SSMS, чтобы открыть редактор запросов с шаблоном сценария временной таблицы, а затем щелкните "Указать значения для параметров шаблона" (Ctrl+Shift+M) для заполнения шаблона.

![SSMSNewTable](./media/sql-database-temporal-tables/AzureTemporal2.png)

В SSDT при добавлении новых элементов в проект базы данных выберите шаблон "Темпоральная таблица (с системным управлением версиями)". Откроется конструктор таблиц, в котором вы сможете легко указать макет таблицы.

![SSDTNewTable](./media/sql-database-temporal-tables/AzureTemporal3.png)

Временную таблицу также можно создать, непосредственно указав инструкции Transact-SQL, как показано в следующем примере. Обратите внимание, что обязательными элементами каждой временной таблицы являются определение PERIOD и предложение SYSTEM_VERSIONING со ссылкой на другую таблицу пользователя, в которой будут храниться исторические версии строк.

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

При создании временной таблицы с системным управлением версиями автоматически создается сопутствующая таблица журнала с конфигурацией по умолчанию. Таблица журнала по умолчанию содержит кластеризованный индекс сбалансированного дерева в столбцах периода (конец и начало) с включенным сжатием страниц. Эта конфигурация оптимальна для большинства сценариев, в которых используются временные таблицы, особенно для [аудита данных](https://msdn.microsoft.com/library/mt631669.aspx#Anchor_0). 

В данном случае наша цель — выполнить анализ тенденций с учетом времени, используя журнал данных за длительный период и большие наборы данных, поэтому в качестве хранилища для таблицы журнала выбран кластеризованный индекс columnstore. Кластеризованный индекс columnstore обеспечивает очень хорошее сжатие и производительность аналитических запросов. Временные таблицы обеспечивают гибкость, позволяя настроить индексы для текущих и временных таблиц полностью независимо друг от друга. 

> [!NOTE]
> Индексы columnstore доступны только для уровня служб "Премиум".
>

В следующем сценарии показано, как индекс по умолчанию в таблице журнала можно изменить на кластеризованный индекс columnstore.

````
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory
ON dbo.WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON); 
````

В обозревателе объектов временные таблицы представлены специальным значком, чтобы их было удобней отличать, а таблица журнала отображается как дочерний узел.

![AlterTable](./media/sql-database-temporal-tables/AzureTemporal4.png)

### <a name="alter-existing-table-to-temporal"></a>Преобразование существующей таблицы во временную
Рассмотрим альтернативный сценарий, в котором таблица WebsiteUserInfo уже существует, но не была предназначена для хранения журнала изменений. В этом случае можно просто расширить существующую таблицу, превратив ее во временную, как показано в следующем примере.

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
Главным преимуществом временных таблиц является то, что для отслеживания изменений вам не нужно каким-либо образом изменять или настраивать веб-сайт. После создания временных таблиц в них прозрачно сохраняются предыдущие версии строк каждый раз, когда вы вносите изменения в данные. 

Чтобы использовать автоматическое отслеживание изменений в этой конкретной ситуации, мы просто будем изменять столбец **PagesVisited** каждый раз, когда пользователь будет завершать сеанс посещения веб-сайта.

````
UPDATE WebsiteUserInfo  SET [PagesVisited] = 5 
WHERE [UserID] = 1;
````

Важно отметить, что запросу на обновление не нужно знать точное время самой операции или то, как будут сохранены данные журнала для последующего анализа. Оба аспекта автоматически обрабатываются базой данных SQL Azure. Следующая схема иллюстрирует, как при каждом обновлении создаются данные журнала.

![TemporalArchitecture](./media/sql-database-temporal-tables/AzureTemporal5.png)

## <a name="step-3-perform-historical-data-analysis"></a>Шаг 3. Анализ данных журнала
Теперь, когда временное управления версиями системой включено, анализ данных журнала — дело всего одного запроса. В этой статье мы приведем несколько примеров распространенных сценариев анализа. Чтобы изучить все подробности, ознакомьтесь с возможностями предложения [FOR SYSTEM_TIME](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_3).

Чтобы просмотреть 10 лидирующих пользователей час назад, упорядоченных по числу посещаемых веб-страниц, выполните этот запрос.

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
SELECT TOP 10 * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME AS OF @hourAgo
ORDER BY PagesVisited DESC
````

Вы легко можете изменить этот запрос, чтобы анализировать посещения сайта день назад, месяц назад или любой момент в прошлом.

Чтобы выполнить простой статистический анализ за предыдущий день, используйте следующий пример.

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

Для поиска активности конкретного пользователя в течение периода времени используйте предложение CONTAINED IN.

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
Как правило, во время разработки приложения приходится менять схему временной таблицы. Для этого просто выполните обычные инструкции запустите ALTER TABLE, и база данных SQL Azure соответствующим образом распространит изменения на таблицу журнала. В следующем сценарии показано, как добавить дополнительный атрибут для отслеживания.

````
/*Add new column for tracking source IP address*/
ALTER TABLE dbo.WebsiteUserInfo 
ADD  [IPAddress] varchar(128) NOT NULL CONSTRAINT DF_Address DEFAULT 'N/A';
````

Аналогичным образом можно изменить определение столбца при активной рабочей нагрузке.

````
/*Increase the length of name column*/
ALTER TABLE dbo.WebsiteUserInfo 
    ALTER COLUMN  UserName nvarchar(256) NOT NULL;
````

Наконец, можно удалить столбец, который больше не нужен.

````
/*Drop unnecessary column */
ALTER TABLE dbo.WebsiteUserInfo 
    DROP COLUMN TemporaryColumn; 
````

В качестве альтернативы можно использовать последнюю версию [SSDT](https://msdn.microsoft.com/library/mt204009.aspx) , чтобы изменить схему временной таблицы при активном подключении к базе данных (интерактивный режим) или непосредственно в проекте базы данных (автономный режим).

## <a name="controlling-retention-of-historical-data"></a>Управление периодом удержания данных журнала
При использовании временных таблиц с системным управлением версиями таблица журнала может увеличить размер базы данных значительнее, чем обычные таблицы. Большая и постоянно растущая таблица журнала может стать проблемой из-за непосредственных затрат на хранилище, а также издержек производительности, накладываемых запросами временных данных. Следовательно, разработка политики хранения данных для управления данными в таблице журнала является важной составляющей планирования и управления жизненным циклом всех временных таблиц. При использовании базы данных SQL Azure доступны следующие подходы для управления данными журнала во временной таблице.

* [Секционирование таблиц.](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_2)
* [Пользовательский сценарий очистки](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_3)

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о темпоральных таблицах см. в [документации MSDN](https://msdn.microsoft.com/library/dn935015.aspx).
Посетите сайт Channel 9, чтобы ознакомиться с [историей успешного внедрения временных решений реальным клиентом](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) и посмотреть наглядную [демонстрацию временных решений](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).

