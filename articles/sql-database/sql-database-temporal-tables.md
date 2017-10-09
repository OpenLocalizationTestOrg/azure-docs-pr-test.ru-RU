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
# <a name="getting-started-with-temporal-tables-in-azure-sql-database"></a><span data-ttu-id="c534e-103">Приступая к работе с временными таблицами в базе данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="c534e-103">Getting Started with Temporal Tables in Azure SQL Database</span></span>
<span data-ttu-id="c534e-104">Темпоральные таблицы являются новой возможностью программирования базы данных SQL Azure, который позволяет вам tootrack и анализировать hello полный журнал изменений в данных, без необходимости hello дополнительного кода.</span><span class="sxs-lookup"><span data-stu-id="c534e-104">Temporal Tables are a new programmability feature of Azure SQL Database that allows you tootrack and analyze hello full history of changes in your data, without hello need for custom coding.</span></span> <span data-ttu-id="c534e-105">Временных таблиц хранить тесно связанных tootime контекст данных, чтобы хранимых фактах можно интерпретировать как допустимый только в течение определенного периода hello.</span><span class="sxs-lookup"><span data-stu-id="c534e-105">Temporal Tables keep data closely related tootime context so that stored facts can be interpreted as valid only within hello specific period.</span></span> <span data-ttu-id="c534e-106">Эта особенность временных таблиц дает возможность эффективно выполнять анализ с учетом времени и получать ценную информацию об эволюции данных.</span><span class="sxs-lookup"><span data-stu-id="c534e-106">This property of Temporal Tables allows for efficient time-based analysis and getting insights from data evolution.</span></span>

## <a name="temporal-scenario"></a><span data-ttu-id="c534e-107">Сценарий использования временных таблиц</span><span class="sxs-lookup"><span data-stu-id="c534e-107">Temporal Scenario</span></span>
<span data-ttu-id="c534e-108">В этой статье рассмотрены hello действия tooutilize временных таблиц в рабочих приложениях.</span><span class="sxs-lookup"><span data-stu-id="c534e-108">This article illustrates hello steps tooutilize Temporal Tables in an application scenario.</span></span> <span data-ttu-id="c534e-109">Предположим, что вы хотите tootrack действиями пользователя на новый веб-сайт, разработанного с нуля или на существующий веб-сайт, которые должны tooextend с аналитикой действия пользователя.</span><span class="sxs-lookup"><span data-stu-id="c534e-109">Suppose that you want tootrack user activity on a new website that is being developed from scratch or on an existing website that you want tooextend with user activity analytics.</span></span> <span data-ttu-id="c534e-110">В этом упрощенном примере предполагается, что число hello посещенные веб-страниц за период времени является признаком того, что требуется toobe захвата и наблюдения за веб-сайт hello базы данных, которая размещается в базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c534e-110">In this simplified example, we assume that hello number of visited web pages during a period of time is an indicator that needs toobe captured and monitored in hello website database that is hosted on Azure SQL Database.</span></span> <span data-ttu-id="c534e-111">Цель Hello hello исторического анализа активности пользователей веб-сайт tooredesign tooget входных данных и укажите для повышения удобства для посетителей hello.</span><span class="sxs-lookup"><span data-stu-id="c534e-111">hello goal of hello historical analysis of user activity is tooget inputs tooredesign website and provide better experience for hello visitors.</span></span>

<span data-ttu-id="c534e-112">Hello модели базы данных в этом сценарии очень прост — представлены метрика действия пользователя с одним целочисленным полем, **PageVisited**и фиксируется, а также основные сведения о профиле пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="c534e-112">hello database model for this scenario is very simple - user activity metric is represented with a single integer field, **PageVisited**, and is captured along with basic information on hello user profile.</span></span> <span data-ttu-id="c534e-113">Кроме того для анализа на основе времени, позволит набор строк для каждого пользователя, где каждая строка представляет hello количество страниц, посещения определенного пользователем в течение определенного периода времени.</span><span class="sxs-lookup"><span data-stu-id="c534e-113">Additionally, for time based analysis, you would keep a series of rows for each user, where every row represents hello number of pages a particular user visited within a specific period of time.</span></span>

![Схема](./media/sql-database-temporal-tables/AzureTemporal1.png)

<span data-ttu-id="c534e-115">К счастью, нет необходимости tooput никаких действий в toomaintain вашего приложения эти сведения для действия.</span><span class="sxs-lookup"><span data-stu-id="c534e-115">Fortunately, you do not need tooput any effort in your app toomaintain this activity information.</span></span> <span data-ttu-id="c534e-116">С Темпоральными таблицами этот процесс выполняется автоматически - что дает полную гибкость во время создания веб-сайта и дополнительные toofocus времени на hello самого анализа данных.</span><span class="sxs-lookup"><span data-stu-id="c534e-116">With Temporal Tables, this process is automated - giving you full flexibility during website design and more time toofocus on hello data analysis itself.</span></span> <span data-ttu-id="c534e-117">Здравствуйте, только что toodo tooensure, **WebSiteInfo** таблица настроена как [темпоральной с системным управлением версиями](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_0).</span><span class="sxs-lookup"><span data-stu-id="c534e-117">hello only thing you have toodo is tooensure that **WebSiteInfo** table is configured as [temporal system-versioned](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_0).</span></span> <span data-ttu-id="c534e-118">конкретные шаги Hello tooutilize временных таблиц в этом сценарии описаны ниже.</span><span class="sxs-lookup"><span data-stu-id="c534e-118">hello exact steps tooutilize Temporal Tables in this scenario are described below.</span></span>

## <a name="step-1-configure-tables-as-temporal"></a><span data-ttu-id="c534e-119">Шаг 1. Настройка таблиц в качестве временных</span><span class="sxs-lookup"><span data-stu-id="c534e-119">Step 1: Configure tables as temporal</span></span>
<span data-ttu-id="c534e-120">В зависимости от того, начинаете вы разработку новых приложений или обновляете существующее приложение, вы создадите временные таблицы или измените существующие, добавляя в них временные атрибуты.</span><span class="sxs-lookup"><span data-stu-id="c534e-120">Depending on whether you are starting new development or upgrading existing application, you will either create temporal tables or modify existing ones by adding temporal attributes.</span></span> <span data-ttu-id="c534e-121">В общем случае может потребоваться сделать и то, и другое.</span><span class="sxs-lookup"><span data-stu-id="c534e-121">In general case, your scenario can be a mix of these two options.</span></span> <span data-ttu-id="c534e-122">Выполните это с помощью [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) (SSMS), [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) (SSDT) или любого другого средства для разработки Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="c534e-122">Perform these action using [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) (SSMS), [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) (SSDT) or any other Transact-SQL development tool.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c534e-123">Рекомендуется всегда использовать hello последнюю версию среды Management Studio tooremain синхронизированы с tooMicrosoft обновления Azure и базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="c534e-123">It is recommended that you always use hello latest version of Management Studio tooremain synchronized with updates tooMicrosoft Azure and SQL Database.</span></span> <span data-ttu-id="c534e-124">[Обновите среду SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="c534e-124">[Update SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span></span>
> 
> 

### <a name="create-new-table"></a><span data-ttu-id="c534e-125">Создание новой таблицы</span><span class="sxs-lookup"><span data-stu-id="c534e-125">Create new table</span></span>
<span data-ttu-id="c534e-126">Используйте пункт контекстного меню «Новой таблицы с системным управлением версиями» в редакторе запросов hello tooopen обозревателя объектов SSMS с помощью шаблона сценария временная таблица, а затем использовать шаблон hello toopopulate «Укажите значения для параметров шаблона» (Ctrl + Shift + M).</span><span class="sxs-lookup"><span data-stu-id="c534e-126">Use context menu item “New System-Versioned Table” in SSMS Object Explorer tooopen hello query editor with a temporal table template script and then use “Specify Values for Template Parameters” (Ctrl+Shift+M) toopopulate hello template:</span></span>

![SSMSNewTable](./media/sql-database-temporal-tables/AzureTemporal2.png)

<span data-ttu-id="c534e-128">В SSDT выбрали шаблона «Временная таблица (с системным управлением версиями)», при добавлении нового проекта базы данных toohello элементы.</span><span class="sxs-lookup"><span data-stu-id="c534e-128">In SSDT, chose “Temporal Table (System-Versioned)” template when adding new items toohello database project.</span></span> <span data-ttu-id="c534e-129">Что будет конструктор открыть таблицу и включить tooeasily можно указать hello таблице макета:</span><span class="sxs-lookup"><span data-stu-id="c534e-129">That will open table designer and enable you tooeasily specify hello table layout:</span></span>

![SSDTNewTable](./media/sql-database-temporal-tables/AzureTemporal3.png)

<span data-ttu-id="c534e-131">Вы также можете создания темпоральной таблицы путем указания инструкции Transact-SQL hello напрямую, как показано в приведенном ниже примере hello.</span><span class="sxs-lookup"><span data-stu-id="c534e-131">You can also a create temporal table by specifying hello Transact-SQL statements directly, as shown in hello example below.</span></span> <span data-ttu-id="c534e-132">Обратите внимание, что hello обязательные элементы всех темпоральных таблиц определения ПЕРИОДА hello и предложение SYSTEM_VERSIONING hello со ссылочной таблице tooanother пользователя, который будет сохранять предыдущие версии строк:</span><span class="sxs-lookup"><span data-stu-id="c534e-132">Note that hello mandatory elements of every temporal table are hello PERIOD definition and hello SYSTEM_VERSIONING clause with a reference tooanother user table that will store historical row versions:</span></span>

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

<span data-ttu-id="c534e-133">При создании таблицы с системным управлением версиями темпоральной таблицы журнала с конфигурацией по умолчанию hello, сопровождающие hello создается автоматически.</span><span class="sxs-lookup"><span data-stu-id="c534e-133">When you create system-versioned temporal table, hello accompanying history table with hello default configuration is automatically created.</span></span> <span data-ttu-id="c534e-134">Таблица журнала по умолчанию Hello содержит кластеризованный индекс сбалансированного дерева для столбцов периода hello (конец, начало) с включенным сжатием страниц.</span><span class="sxs-lookup"><span data-stu-id="c534e-134">hello default history table contains a clustered B-tree index on hello period columns (end, start) with page compression enabled.</span></span> <span data-ttu-id="c534e-135">Эта конфигурация является оптимальной для hello в большинстве случаев, в которых используются временных таблиц, особенно для [аудит данных](https://msdn.microsoft.com/library/mt631669.aspx#Anchor_0).</span><span class="sxs-lookup"><span data-stu-id="c534e-135">This configuration is optimal for hello majority of scenarios in which temporal tables are used, especially for [data auditing](https://msdn.microsoft.com/library/mt631669.aspx#Anchor_0).</span></span> 

<span data-ttu-id="c534e-136">В данном случае мы цель анализа тенденций на основе времени tooperform за более длительный журнал данных и с крупными наборами данных, поэтому hello вариант хранилища для таблицы журнала hello в кластеризованном индексе.</span><span class="sxs-lookup"><span data-stu-id="c534e-136">In this particular case, we aim tooperform time-based trend analysis over a longer data history and with bigger data sets, so hello storage choice for hello history table is a clustered columnstore index.</span></span> <span data-ttu-id="c534e-137">Кластеризованный индекс columnstore обеспечивает очень хорошее сжатие и производительность аналитических запросов.</span><span class="sxs-lookup"><span data-stu-id="c534e-137">A clustered columnstore provides very good compression and performance for analytical queries.</span></span> <span data-ttu-id="c534e-138">Временных таблиц предоставьте hello индексы tooconfigure гибкость hello текущих и временных таблиц в совершенно независимо друг от друга.</span><span class="sxs-lookup"><span data-stu-id="c534e-138">Temporal Tables give you hello flexibility tooconfigure indexes on hello current and temporal tables completely independently.</span></span> 

> [!NOTE]
> <span data-ttu-id="c534e-139">Индексы ColumnStore доступны только для уровня служб premium hello.</span><span class="sxs-lookup"><span data-stu-id="c534e-139">Columnstore indexes are only available in hello premium service tier.</span></span>
>

<span data-ttu-id="c534e-140">Привет, выполнив сценарий показывает, как индекс по умолчанию для таблицы журнала можно измененные toohello clustered columnstore:</span><span class="sxs-lookup"><span data-stu-id="c534e-140">hello following script shows how default index on history table can be changed toohello clustered columnstore:</span></span>

````
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory
ON dbo.WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON); 
````

<span data-ttu-id="c534e-141">Временных таблиц представлены в hello обозревателя объектов с hello определенный значок для удобства идентификации, пока соответствующей таблицей журнала отображается как дочерний узел.</span><span class="sxs-lookup"><span data-stu-id="c534e-141">Temporal Tables are represented in hello Object Explorer with hello specific icon for easier identification, while its history table is displayed as a child node.</span></span>

![AlterTable](./media/sql-database-temporal-tables/AzureTemporal4.png)

### <a name="alter-existing-table-tootemporal"></a><span data-ttu-id="c534e-143">Изменять существующие таблицы tootemporal</span><span class="sxs-lookup"><span data-stu-id="c534e-143">Alter existing table tootemporal</span></span>
<span data-ttu-id="c534e-144">Давайте охватывают hello альтернативного сценария, в какие hello WebsiteUserInfo таблица уже существует, но не спроектированных tookeep журнал изменений.</span><span class="sxs-lookup"><span data-stu-id="c534e-144">Let’s cover hello alternative scenario in which hello WebsiteUserInfo table already exists, but was not designed tookeep a history of changes.</span></span> <span data-ttu-id="c534e-145">В этом случае можно просто дополнить hello существующие таблицы toobecome темпоральной, как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="c534e-145">In this case, you can simply extend hello existing table toobecome temporal, as shown in hello following example:</span></span>

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

## <a name="step-2-run-your-workload-regularly"></a><span data-ttu-id="c534e-146">Шаг 2. Регулярный запуск рабочей нагрузки</span><span class="sxs-lookup"><span data-stu-id="c534e-146">Step 2: Run your workload regularly</span></span>
<span data-ttu-id="c534e-147">главным преимуществом Hello временных таблиц — не требуется toochange или настроить веб-сайт в системе отслеживания изменений tooperform любой способ.</span><span class="sxs-lookup"><span data-stu-id="c534e-147">hello main advantage of Temporal Tables is that you do not need toochange or adjust your website in any way tooperform change tracking.</span></span> <span data-ttu-id="c534e-148">После создания временных таблиц в них прозрачно сохраняются предыдущие версии строк каждый раз, когда вы вносите изменения в данные.</span><span class="sxs-lookup"><span data-stu-id="c534e-148">Once created, Temporal Tables transparently persist previous row versions every time you perform modifications on your data.</span></span> 

<span data-ttu-id="c534e-149">В порядке tooleverage автоматическое отслеживание изменений для этой конкретной ситуации, давайте просто обновить столбец **PagesVisited** каждый раз, когда пользователь завершает сеанс, her/his на веб-сайте hello:</span><span class="sxs-lookup"><span data-stu-id="c534e-149">In order tooleverage automatic change tracking for this particular scenario, let’s just update column **PagesVisited** every time when user ends her/his session on hello website:</span></span>

````
UPDATE WebsiteUserInfo  SET [PagesVisited] = 5 
WHERE [UserID] = 1;
````

<span data-ttu-id="c534e-150">Очень важно, что toonotice, hello запрос на обновление не требуется tooknow hello точное время возникновения фактическая операция hello, ни как данные журнала сохраняются для последующего анализа.</span><span class="sxs-lookup"><span data-stu-id="c534e-150">It is important toonotice that hello update query doesn’t need tooknow hello exact time when hello actual operation occurred nor how historical data will be preserved for future analysis.</span></span> <span data-ttu-id="c534e-151">Оба аспекты автоматически обрабатываются hello базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c534e-151">Both aspects are automatically handled by hello Azure SQL Database.</span></span> <span data-ttu-id="c534e-152">Hello следующая диаграмма иллюстрирует методом формирования данных журнала на каждое обновление.</span><span class="sxs-lookup"><span data-stu-id="c534e-152">hello following diagram illustrates how history data is being generated on every update.</span></span>

![TemporalArchitecture](./media/sql-database-temporal-tables/AzureTemporal5.png)

## <a name="step-3-perform-historical-data-analysis"></a><span data-ttu-id="c534e-154">Шаг 3. Анализ данных журнала</span><span class="sxs-lookup"><span data-stu-id="c534e-154">Step 3: Perform historical data analysis</span></span>
<span data-ttu-id="c534e-155">Теперь, когда временное управления версиями системой включено, анализ данных журнала — дело всего одного запроса.</span><span class="sxs-lookup"><span data-stu-id="c534e-155">Now when temporal system-versioning is enabled, historical data analysis is just one query away from you.</span></span> <span data-ttu-id="c534e-156">В этой статье мы предоставить несколько примеров, которые устраняют распространенные сценарии анализа - toolearn все сведения, варианты предварен hello [FOR SYSTEM_TIME](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_3) предложения.</span><span class="sxs-lookup"><span data-stu-id="c534e-156">In this article, we will provide a few examples that address common analysis scenarios - toolearn all details, explore various options introduced with hello [FOR SYSTEM_TIME](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_3) clause.</span></span>

<span data-ttu-id="c534e-157">toosee hello top 10 пользователей, упорядоченных по номеру hello посещенные веб-страниц на один час назад, выполните этот запрос.</span><span class="sxs-lookup"><span data-stu-id="c534e-157">toosee hello top 10 users ordered by hello number of visited web pages as of an hour ago, run this query:</span></span>

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
SELECT TOP 10 * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME AS OF @hourAgo
ORDER BY PagesVisited DESC
````

<span data-ttu-id="c534e-158">Этот запрос можно легко изменить сайт hello tooanalyze посещает начиная с дня назад, месяц назад или в любой момент в прошлом hello нужно.</span><span class="sxs-lookup"><span data-stu-id="c534e-158">You can easily modify this query tooanalyze hello site visits as of a day ago, a month ago or at any point in hello past you wish.</span></span>

<span data-ttu-id="c534e-159">Основные статистического анализа tooperform для hello предыдущий день, используйте следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="c534e-159">tooperform basic statistical analysis for hello previous day, use hello following example:</span></span>

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

<span data-ttu-id="c534e-160">toosearch для действий конкретного пользователя, в течение периода времени, предложение CONTAINED IN hello используйте:</span><span class="sxs-lookup"><span data-stu-id="c534e-160">toosearch for activities of a specific user, within a period of time, use hello CONTAINED IN clause:</span></span>

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
DECLARE @twoHoursAgo datetime2 = DATEADD(HOUR, -2, SYSUTCDATETIME());
SELECT * FROM dbo.WebsiteUserInfo 
FOR SYSTEM_TIME CONTAINED IN (@twoHoursAgo, @hourAgo)
WHERE [UserID] = 1;
````

<span data-ttu-id="c534e-161">Графическое представление особенно удобно для временных запросов, так как можно отобразить тенденции и закономерности использования доступным и интуитивно понятным способом.</span><span class="sxs-lookup"><span data-stu-id="c534e-161">Graphic visualization is especially convenient for temporal queries as you can show trends and usage patterns in an intuitive way very easily:</span></span>

![TemporalGraph](./media/sql-database-temporal-tables/AzureTemporal6.png)

## <a name="evolving-table-schema"></a><span data-ttu-id="c534e-163">Развитие схемы таблицы</span><span class="sxs-lookup"><span data-stu-id="c534e-163">Evolving table schema</span></span>
<span data-ttu-id="c534e-164">Как правило необходимо будет toochange hello временная таблица схемы во время разработки приложения.</span><span class="sxs-lookup"><span data-stu-id="c534e-164">Typically, you will need toochange hello temporal table schema while you are doing app development.</span></span> <span data-ttu-id="c534e-165">Для этого просто запустите инструкций ALTER TABLE и базы данных SQL Azure надлежащим образом будет распространено таблицы журнала toohello изменения.</span><span class="sxs-lookup"><span data-stu-id="c534e-165">For that, simply run regular ALTER TABLE statements and Azure SQL Database will appropriately propagate changes toohello history table.</span></span> <span data-ttu-id="c534e-166">Hello следующий сценарий показывает, как можно добавить дополнительный атрибут для отслеживания:</span><span class="sxs-lookup"><span data-stu-id="c534e-166">hello following script shows how you can add additional attribute for tracking:</span></span>

````
/*Add new column for tracking source IP address*/
ALTER TABLE dbo.WebsiteUserInfo 
ADD  [IPAddress] varchar(128) NOT NULL CONSTRAINT DF_Address DEFAULT 'N/A';
````

<span data-ttu-id="c534e-167">Аналогичным образом можно изменить определение столбца при активной рабочей нагрузке.</span><span class="sxs-lookup"><span data-stu-id="c534e-167">Similarly, you can change column definition while your workload is active:</span></span>

````
/*Increase hello length of name column*/
ALTER TABLE dbo.WebsiteUserInfo 
    ALTER COLUMN  UserName nvarchar(256) NOT NULL;
````

<span data-ttu-id="c534e-168">Наконец, можно удалить столбец, который больше не нужен.</span><span class="sxs-lookup"><span data-stu-id="c534e-168">Finally, you can remove a column that you do not need anymore.</span></span>

````
/*Drop unnecessary column */
ALTER TABLE dbo.WebsiteUserInfo 
    DROP COLUMN TemporaryColumn; 
````

<span data-ttu-id="c534e-169">Также можно использовать последнюю версию [SSDT](https://msdn.microsoft.com/library/mt204009.aspx) toochange временная схема таблицы, пока вы находитесь toohello подключенной базы данных (интерактивный режим) или как часть проекта базы данных hello (автономный режим).</span><span class="sxs-lookup"><span data-stu-id="c534e-169">Alternatively, use latest [SSDT](https://msdn.microsoft.com/library/mt204009.aspx) toochange temporal table schema while you are connected toohello database (online mode) or as part of hello database project (offline mode).</span></span>

## <a name="controlling-retention-of-historical-data"></a><span data-ttu-id="c534e-170">Управление периодом удержания данных журнала</span><span class="sxs-lookup"><span data-stu-id="c534e-170">Controlling retention of historical data</span></span>
<span data-ttu-id="c534e-171">С темпоральными таблицами с системным управлением версиями таблица журнала hello может увеличить размер базы данных hello больше, чем обычные таблицы.</span><span class="sxs-lookup"><span data-stu-id="c534e-171">With system-versioned temporal tables, hello history table may increase hello database size more than regular tables.</span></span> <span data-ttu-id="c534e-172">Большой и постоянно растущий объем таблицы журнала может стать проблемой не только из-за затрат на хранение toopure, а также налагающий производительности при выполнении темпоральных запросов.</span><span class="sxs-lookup"><span data-stu-id="c534e-172">A large and ever-growing history table can become an issue both due toopure storage costs as well as imposing a performance tax on temporal querying.</span></span> <span data-ttu-id="c534e-173">Таким образом Разработка политики хранения данных для управления данными в таблице журнала hello является важным аспектом планирования и управления жизненным циклом всех темпоральных таблиц hello.</span><span class="sxs-lookup"><span data-stu-id="c534e-173">Hence, developing a data retention policy for managing data in hello history table is an important aspect of planning and managing hello lifecycle of every temporal table.</span></span> <span data-ttu-id="c534e-174">С базой данных SQL Azure у вас есть следующие подходы к управлению данными журнала в темпоральной таблице hello hello:</span><span class="sxs-lookup"><span data-stu-id="c534e-174">With Azure SQL Database, you have hello following approaches for managing historical data in hello temporal table:</span></span>

* [<span data-ttu-id="c534e-175">Секционирование таблиц.</span><span class="sxs-lookup"><span data-stu-id="c534e-175">Table Partitioning</span></span>](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_2)
* [<span data-ttu-id="c534e-176">Пользовательский сценарий очистки</span><span class="sxs-lookup"><span data-stu-id="c534e-176">Custom Cleanup Script</span></span>](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_3)

## <a name="next-steps"></a><span data-ttu-id="c534e-177">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c534e-177">Next steps</span></span>
<span data-ttu-id="c534e-178">Дополнительные сведения о темпоральных таблицах см. в [документации MSDN](https://msdn.microsoft.com/library/dn935015.aspx).</span><span class="sxs-lookup"><span data-stu-id="c534e-178">For detailed information on Temporal Tables, check out [MSDN documentation](https://msdn.microsoft.com/library/dn935015.aspx).</span></span>
<span data-ttu-id="c534e-179">Посетите Channel 9 toohear [историю успеха temporal выполнению реальных клиентских](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) » и «Контрольное [live temporal демонстрации](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span><span class="sxs-lookup"><span data-stu-id="c534e-179">Visit Channel 9 toohear a [real customer temporal implemenation success story](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) and watch a [live temporal demonstration](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span></span>

