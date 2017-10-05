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
# <a name="getting-started-with-temporal-tables-in-azure-sql-database"></a><span data-ttu-id="e2353-103">Приступая к работе с временными таблицами в базе данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="e2353-103">Getting Started with Temporal Tables in Azure SQL Database</span></span>
<span data-ttu-id="e2353-104">Временные таблицы — это новая программная возможность базы данных SQL Azure, которая позволяет отслеживать и анализировать полный журнал изменений в данных, не создавая какого-либо дополнительного пользовательского кода.</span><span class="sxs-lookup"><span data-stu-id="e2353-104">Temporal Tables are a new programmability feature of Azure SQL Database that allows you to track and analyze the full history of changes in your data, without the need for custom coding.</span></span> <span data-ttu-id="e2353-105">Во временных таблицах хранятся данные, тесно связанные с контекстом времени, чтобы хранимые факты можно было интерпретировать как действительные только в течение определенного периода.</span><span class="sxs-lookup"><span data-stu-id="e2353-105">Temporal Tables keep data closely related to time context so that stored facts can be interpreted as valid only within the specific period.</span></span> <span data-ttu-id="e2353-106">Эта особенность временных таблиц дает возможность эффективно выполнять анализ с учетом времени и получать ценную информацию об эволюции данных.</span><span class="sxs-lookup"><span data-stu-id="e2353-106">This property of Temporal Tables allows for efficient time-based analysis and getting insights from data evolution.</span></span>

## <a name="temporal-scenario"></a><span data-ttu-id="e2353-107">Сценарий использования временных таблиц</span><span class="sxs-lookup"><span data-stu-id="e2353-107">Temporal Scenario</span></span>
<span data-ttu-id="e2353-108">В данной статье показана последовательность действий для использования временных таблиц в прикладном сценарии.</span><span class="sxs-lookup"><span data-stu-id="e2353-108">This article illustrates the steps to utilize Temporal Tables in an application scenario.</span></span> <span data-ttu-id="e2353-109">Предположим, что вам нужно отслеживать активность пользователей на новом веб-сайте, который разрабатывался с нуля, или на существующем веб-сайте, который вы хотите дополнить возможностями анализа активности пользователей.</span><span class="sxs-lookup"><span data-stu-id="e2353-109">Suppose that you want to track user activity on a new website that is being developed from scratch or on an existing website that you want to extend with user activity analytics.</span></span> <span data-ttu-id="e2353-110">В этом упрощенном примере предположим, что количество посещаемых веб-страниц за определенный период времени является показателем, который необходимо записывать и отслеживать в базе данных веб-сайта, размещенной в базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="e2353-110">In this simplified example, we assume that the number of visited web pages during a period of time is an indicator that needs to be captured and monitored in the website database that is hosted on Azure SQL Database.</span></span> <span data-ttu-id="e2353-111">Цель исторического анализа активности пользователей — получить входные данные для переработки веб-сайта и улучшения его взаимодействия с посетителями.</span><span class="sxs-lookup"><span data-stu-id="e2353-111">The goal of the historical analysis of user activity is to get inputs to redesign website and provide better experience for the visitors.</span></span>

<span data-ttu-id="e2353-112">Модель базы данных в этом сценарии очень простая: метрика активности пользователей представлена одним целочисленным полем, **PageVisited**, а ее значение записывается вместе с основными сведениями в профиле пользователя.</span><span class="sxs-lookup"><span data-stu-id="e2353-112">The database model for this scenario is very simple - user activity metric is represented with a single integer field, **PageVisited**, and is captured along with basic information on the user profile.</span></span> <span data-ttu-id="e2353-113">Кроме того, для анализа с учетом времени следует выделить набор строк для каждого пользователя, где каждая строка представляет число страниц, посещенных определенным пользователем в течение определенного периода времени.</span><span class="sxs-lookup"><span data-stu-id="e2353-113">Additionally, for time based analysis, you would keep a series of rows for each user, where every row represents the number of pages a particular user visited within a specific period of time.</span></span>

![Схема](./media/sql-database-temporal-tables/AzureTemporal1.png)

<span data-ttu-id="e2353-115">К счастью, вам не нужно программировать хранение этой информации об активности в приложении.</span><span class="sxs-lookup"><span data-stu-id="e2353-115">Fortunately, you do not need to put any effort in your app to maintain this activity information.</span></span> <span data-ttu-id="e2353-116">Благодаря временным таблицам этот процесс автоматизирован, что обеспечивает абсолютную гибкость во время разработки веб-сайта и позволяет больше времени уделить непосредственно анализу данных.</span><span class="sxs-lookup"><span data-stu-id="e2353-116">With Temporal Tables, this process is automated - giving you full flexibility during website design and more time to focus on the data analysis itself.</span></span> <span data-ttu-id="e2353-117">Единственное, что необходимо сделать, — убедиться, что таблица **WebSiteInfo** настроена как [временная с системным управлением версиями](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_0).</span><span class="sxs-lookup"><span data-stu-id="e2353-117">The only thing you have to do is to ensure that **WebSiteInfo** table is configured as [temporal system-versioned](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_0).</span></span> <span data-ttu-id="e2353-118">Конкретные шаги по использованию временных таблиц в этом сценарии описаны ниже.</span><span class="sxs-lookup"><span data-stu-id="e2353-118">The exact steps to utilize Temporal Tables in this scenario are described below.</span></span>

## <a name="step-1-configure-tables-as-temporal"></a><span data-ttu-id="e2353-119">Шаг 1. Настройка таблиц в качестве временных</span><span class="sxs-lookup"><span data-stu-id="e2353-119">Step 1: Configure tables as temporal</span></span>
<span data-ttu-id="e2353-120">В зависимости от того, начинаете вы разработку новых приложений или обновляете существующее приложение, вы создадите временные таблицы или измените существующие, добавляя в них временные атрибуты.</span><span class="sxs-lookup"><span data-stu-id="e2353-120">Depending on whether you are starting new development or upgrading existing application, you will either create temporal tables or modify existing ones by adding temporal attributes.</span></span> <span data-ttu-id="e2353-121">В общем случае может потребоваться сделать и то, и другое.</span><span class="sxs-lookup"><span data-stu-id="e2353-121">In general case, your scenario can be a mix of these two options.</span></span> <span data-ttu-id="e2353-122">Выполните это с помощью [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) (SSMS), [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) (SSDT) или любого другого средства для разработки Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="e2353-122">Perform these action using [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) (SSMS), [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) (SSDT) or any other Transact-SQL development tool.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e2353-123">Чтобы обеспечить синхронизацию с обновлениями Microsoft Azure и Базой данных SQL, рекомендуется всегда использовать последнюю версию Management Studio.</span><span class="sxs-lookup"><span data-stu-id="e2353-123">It is recommended that you always use the latest version of Management Studio to remain synchronized with updates to Microsoft Azure and SQL Database.</span></span> <span data-ttu-id="e2353-124">[Обновите среду SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="e2353-124">[Update SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span></span>
> 
> 

### <a name="create-new-table"></a><span data-ttu-id="e2353-125">Создание новой таблицы</span><span class="sxs-lookup"><span data-stu-id="e2353-125">Create new table</span></span>
<span data-ttu-id="e2353-126">Используйте пункт контекстного меню "New System-Versioned Table" (Новая таблица с системным управлением версиями) в обозревателе объектов SSMS, чтобы открыть редактор запросов с шаблоном сценария временной таблицы, а затем щелкните "Указать значения для параметров шаблона" (Ctrl+Shift+M) для заполнения шаблона.</span><span class="sxs-lookup"><span data-stu-id="e2353-126">Use context menu item “New System-Versioned Table” in SSMS Object Explorer to open the query editor with a temporal table template script and then use “Specify Values for Template Parameters” (Ctrl+Shift+M) to populate the template:</span></span>

![SSMSNewTable](./media/sql-database-temporal-tables/AzureTemporal2.png)

<span data-ttu-id="e2353-128">В SSDT при добавлении новых элементов в проект базы данных выберите шаблон "Темпоральная таблица (с системным управлением версиями)".</span><span class="sxs-lookup"><span data-stu-id="e2353-128">In SSDT, chose “Temporal Table (System-Versioned)” template when adding new items to the database project.</span></span> <span data-ttu-id="e2353-129">Откроется конструктор таблиц, в котором вы сможете легко указать макет таблицы.</span><span class="sxs-lookup"><span data-stu-id="e2353-129">That will open table designer and enable you to easily specify the table layout:</span></span>

![SSDTNewTable](./media/sql-database-temporal-tables/AzureTemporal3.png)

<span data-ttu-id="e2353-131">Временную таблицу также можно создать, непосредственно указав инструкции Transact-SQL, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="e2353-131">You can also a create temporal table by specifying the Transact-SQL statements directly, as shown in the example below.</span></span> <span data-ttu-id="e2353-132">Обратите внимание, что обязательными элементами каждой временной таблицы являются определение PERIOD и предложение SYSTEM_VERSIONING со ссылкой на другую таблицу пользователя, в которой будут храниться исторические версии строк.</span><span class="sxs-lookup"><span data-stu-id="e2353-132">Note that the mandatory elements of every temporal table are the PERIOD definition and the SYSTEM_VERSIONING clause with a reference to another user table that will store historical row versions:</span></span>

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

<span data-ttu-id="e2353-133">При создании временной таблицы с системным управлением версиями автоматически создается сопутствующая таблица журнала с конфигурацией по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e2353-133">When you create system-versioned temporal table, the accompanying history table with the default configuration is automatically created.</span></span> <span data-ttu-id="e2353-134">Таблица журнала по умолчанию содержит кластеризованный индекс сбалансированного дерева в столбцах периода (конец и начало) с включенным сжатием страниц.</span><span class="sxs-lookup"><span data-stu-id="e2353-134">The default history table contains a clustered B-tree index on the period columns (end, start) with page compression enabled.</span></span> <span data-ttu-id="e2353-135">Эта конфигурация оптимальна для большинства сценариев, в которых используются временные таблицы, особенно для [аудита данных](https://msdn.microsoft.com/library/mt631669.aspx#Anchor_0).</span><span class="sxs-lookup"><span data-stu-id="e2353-135">This configuration is optimal for the majority of scenarios in which temporal tables are used, especially for [data auditing](https://msdn.microsoft.com/library/mt631669.aspx#Anchor_0).</span></span> 

<span data-ttu-id="e2353-136">В данном случае наша цель — выполнить анализ тенденций с учетом времени, используя журнал данных за длительный период и большие наборы данных, поэтому в качестве хранилища для таблицы журнала выбран кластеризованный индекс columnstore.</span><span class="sxs-lookup"><span data-stu-id="e2353-136">In this particular case, we aim to perform time-based trend analysis over a longer data history and with bigger data sets, so the storage choice for the history table is a clustered columnstore index.</span></span> <span data-ttu-id="e2353-137">Кластеризованный индекс columnstore обеспечивает очень хорошее сжатие и производительность аналитических запросов.</span><span class="sxs-lookup"><span data-stu-id="e2353-137">A clustered columnstore provides very good compression and performance for analytical queries.</span></span> <span data-ttu-id="e2353-138">Временные таблицы обеспечивают гибкость, позволяя настроить индексы для текущих и временных таблиц полностью независимо друг от друга.</span><span class="sxs-lookup"><span data-stu-id="e2353-138">Temporal Tables give you the flexibility to configure indexes on the current and temporal tables completely independently.</span></span> 

> [!NOTE]
> <span data-ttu-id="e2353-139">Индексы columnstore доступны только для уровня служб "Премиум".</span><span class="sxs-lookup"><span data-stu-id="e2353-139">Columnstore indexes are only available in the premium service tier.</span></span>
>

<span data-ttu-id="e2353-140">В следующем сценарии показано, как индекс по умолчанию в таблице журнала можно изменить на кластеризованный индекс columnstore.</span><span class="sxs-lookup"><span data-stu-id="e2353-140">The following script shows how default index on history table can be changed to the clustered columnstore:</span></span>

````
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory
ON dbo.WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON); 
````

<span data-ttu-id="e2353-141">В обозревателе объектов временные таблицы представлены специальным значком, чтобы их было удобней отличать, а таблица журнала отображается как дочерний узел.</span><span class="sxs-lookup"><span data-stu-id="e2353-141">Temporal Tables are represented in the Object Explorer with the specific icon for easier identification, while its history table is displayed as a child node.</span></span>

![AlterTable](./media/sql-database-temporal-tables/AzureTemporal4.png)

### <a name="alter-existing-table-to-temporal"></a><span data-ttu-id="e2353-143">Преобразование существующей таблицы во временную</span><span class="sxs-lookup"><span data-stu-id="e2353-143">Alter existing table to temporal</span></span>
<span data-ttu-id="e2353-144">Рассмотрим альтернативный сценарий, в котором таблица WebsiteUserInfo уже существует, но не была предназначена для хранения журнала изменений.</span><span class="sxs-lookup"><span data-stu-id="e2353-144">Let’s cover the alternative scenario in which the WebsiteUserInfo table already exists, but was not designed to keep a history of changes.</span></span> <span data-ttu-id="e2353-145">В этом случае можно просто расширить существующую таблицу, превратив ее во временную, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="e2353-145">In this case, you can simply extend the existing table to become temporal, as shown in the following example:</span></span>

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

## <a name="step-2-run-your-workload-regularly"></a><span data-ttu-id="e2353-146">Шаг 2. Регулярный запуск рабочей нагрузки</span><span class="sxs-lookup"><span data-stu-id="e2353-146">Step 2: Run your workload regularly</span></span>
<span data-ttu-id="e2353-147">Главным преимуществом временных таблиц является то, что для отслеживания изменений вам не нужно каким-либо образом изменять или настраивать веб-сайт.</span><span class="sxs-lookup"><span data-stu-id="e2353-147">The main advantage of Temporal Tables is that you do not need to change or adjust your website in any way to perform change tracking.</span></span> <span data-ttu-id="e2353-148">После создания временных таблиц в них прозрачно сохраняются предыдущие версии строк каждый раз, когда вы вносите изменения в данные.</span><span class="sxs-lookup"><span data-stu-id="e2353-148">Once created, Temporal Tables transparently persist previous row versions every time you perform modifications on your data.</span></span> 

<span data-ttu-id="e2353-149">Чтобы использовать автоматическое отслеживание изменений в этой конкретной ситуации, мы просто будем изменять столбец **PagesVisited** каждый раз, когда пользователь будет завершать сеанс посещения веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="e2353-149">In order to leverage automatic change tracking for this particular scenario, let’s just update column **PagesVisited** every time when user ends her/his session on the website:</span></span>

````
UPDATE WebsiteUserInfo  SET [PagesVisited] = 5 
WHERE [UserID] = 1;
````

<span data-ttu-id="e2353-150">Важно отметить, что запросу на обновление не нужно знать точное время самой операции или то, как будут сохранены данные журнала для последующего анализа.</span><span class="sxs-lookup"><span data-stu-id="e2353-150">It is important to notice that the update query doesn’t need to know the exact time when the actual operation occurred nor how historical data will be preserved for future analysis.</span></span> <span data-ttu-id="e2353-151">Оба аспекта автоматически обрабатываются базой данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="e2353-151">Both aspects are automatically handled by the Azure SQL Database.</span></span> <span data-ttu-id="e2353-152">Следующая схема иллюстрирует, как при каждом обновлении создаются данные журнала.</span><span class="sxs-lookup"><span data-stu-id="e2353-152">The following diagram illustrates how history data is being generated on every update.</span></span>

![TemporalArchitecture](./media/sql-database-temporal-tables/AzureTemporal5.png)

## <a name="step-3-perform-historical-data-analysis"></a><span data-ttu-id="e2353-154">Шаг 3. Анализ данных журнала</span><span class="sxs-lookup"><span data-stu-id="e2353-154">Step 3: Perform historical data analysis</span></span>
<span data-ttu-id="e2353-155">Теперь, когда временное управления версиями системой включено, анализ данных журнала — дело всего одного запроса.</span><span class="sxs-lookup"><span data-stu-id="e2353-155">Now when temporal system-versioning is enabled, historical data analysis is just one query away from you.</span></span> <span data-ttu-id="e2353-156">В этой статье мы приведем несколько примеров распространенных сценариев анализа. Чтобы изучить все подробности, ознакомьтесь с возможностями предложения [FOR SYSTEM_TIME](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_3).</span><span class="sxs-lookup"><span data-stu-id="e2353-156">In this article, we will provide a few examples that address common analysis scenarios - to learn all details, explore various options introduced with the [FOR SYSTEM_TIME](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_3) clause.</span></span>

<span data-ttu-id="e2353-157">Чтобы просмотреть 10 лидирующих пользователей час назад, упорядоченных по числу посещаемых веб-страниц, выполните этот запрос.</span><span class="sxs-lookup"><span data-stu-id="e2353-157">To see the top 10 users ordered by the number of visited web pages as of an hour ago, run this query:</span></span>

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
SELECT TOP 10 * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME AS OF @hourAgo
ORDER BY PagesVisited DESC
````

<span data-ttu-id="e2353-158">Вы легко можете изменить этот запрос, чтобы анализировать посещения сайта день назад, месяц назад или любой момент в прошлом.</span><span class="sxs-lookup"><span data-stu-id="e2353-158">You can easily modify this query to analyze the site visits as of a day ago, a month ago or at any point in the past you wish.</span></span>

<span data-ttu-id="e2353-159">Чтобы выполнить простой статистический анализ за предыдущий день, используйте следующий пример.</span><span class="sxs-lookup"><span data-stu-id="e2353-159">To perform basic statistical analysis for the previous day, use the following example:</span></span>

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

<span data-ttu-id="e2353-160">Для поиска активности конкретного пользователя в течение периода времени используйте предложение CONTAINED IN.</span><span class="sxs-lookup"><span data-stu-id="e2353-160">To search for activities of a specific user, within a period of time, use the CONTAINED IN clause:</span></span>

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
DECLARE @twoHoursAgo datetime2 = DATEADD(HOUR, -2, SYSUTCDATETIME());
SELECT * FROM dbo.WebsiteUserInfo 
FOR SYSTEM_TIME CONTAINED IN (@twoHoursAgo, @hourAgo)
WHERE [UserID] = 1;
````

<span data-ttu-id="e2353-161">Графическое представление особенно удобно для временных запросов, так как можно отобразить тенденции и закономерности использования доступным и интуитивно понятным способом.</span><span class="sxs-lookup"><span data-stu-id="e2353-161">Graphic visualization is especially convenient for temporal queries as you can show trends and usage patterns in an intuitive way very easily:</span></span>

![TemporalGraph](./media/sql-database-temporal-tables/AzureTemporal6.png)

## <a name="evolving-table-schema"></a><span data-ttu-id="e2353-163">Развитие схемы таблицы</span><span class="sxs-lookup"><span data-stu-id="e2353-163">Evolving table schema</span></span>
<span data-ttu-id="e2353-164">Как правило, во время разработки приложения приходится менять схему временной таблицы.</span><span class="sxs-lookup"><span data-stu-id="e2353-164">Typically, you will need to change the temporal table schema while you are doing app development.</span></span> <span data-ttu-id="e2353-165">Для этого просто выполните обычные инструкции запустите ALTER TABLE, и база данных SQL Azure соответствующим образом распространит изменения на таблицу журнала.</span><span class="sxs-lookup"><span data-stu-id="e2353-165">For that, simply run regular ALTER TABLE statements and Azure SQL Database will appropriately propagate changes to the history table.</span></span> <span data-ttu-id="e2353-166">В следующем сценарии показано, как добавить дополнительный атрибут для отслеживания.</span><span class="sxs-lookup"><span data-stu-id="e2353-166">The following script shows how you can add additional attribute for tracking:</span></span>

````
/*Add new column for tracking source IP address*/
ALTER TABLE dbo.WebsiteUserInfo 
ADD  [IPAddress] varchar(128) NOT NULL CONSTRAINT DF_Address DEFAULT 'N/A';
````

<span data-ttu-id="e2353-167">Аналогичным образом можно изменить определение столбца при активной рабочей нагрузке.</span><span class="sxs-lookup"><span data-stu-id="e2353-167">Similarly, you can change column definition while your workload is active:</span></span>

````
/*Increase the length of name column*/
ALTER TABLE dbo.WebsiteUserInfo 
    ALTER COLUMN  UserName nvarchar(256) NOT NULL;
````

<span data-ttu-id="e2353-168">Наконец, можно удалить столбец, который больше не нужен.</span><span class="sxs-lookup"><span data-stu-id="e2353-168">Finally, you can remove a column that you do not need anymore.</span></span>

````
/*Drop unnecessary column */
ALTER TABLE dbo.WebsiteUserInfo 
    DROP COLUMN TemporaryColumn; 
````

<span data-ttu-id="e2353-169">В качестве альтернативы можно использовать последнюю версию [SSDT](https://msdn.microsoft.com/library/mt204009.aspx) , чтобы изменить схему временной таблицы при активном подключении к базе данных (интерактивный режим) или непосредственно в проекте базы данных (автономный режим).</span><span class="sxs-lookup"><span data-stu-id="e2353-169">Alternatively, use latest [SSDT](https://msdn.microsoft.com/library/mt204009.aspx) to change temporal table schema while you are connected to the database (online mode) or as part of the database project (offline mode).</span></span>

## <a name="controlling-retention-of-historical-data"></a><span data-ttu-id="e2353-170">Управление периодом удержания данных журнала</span><span class="sxs-lookup"><span data-stu-id="e2353-170">Controlling retention of historical data</span></span>
<span data-ttu-id="e2353-171">При использовании временных таблиц с системным управлением версиями таблица журнала может увеличить размер базы данных значительнее, чем обычные таблицы.</span><span class="sxs-lookup"><span data-stu-id="e2353-171">With system-versioned temporal tables, the history table may increase the database size more than regular tables.</span></span> <span data-ttu-id="e2353-172">Большая и постоянно растущая таблица журнала может стать проблемой из-за непосредственных затрат на хранилище, а также издержек производительности, накладываемых запросами временных данных.</span><span class="sxs-lookup"><span data-stu-id="e2353-172">A large and ever-growing history table can become an issue both due to pure storage costs as well as imposing a performance tax on temporal querying.</span></span> <span data-ttu-id="e2353-173">Следовательно, разработка политики хранения данных для управления данными в таблице журнала является важной составляющей планирования и управления жизненным циклом всех временных таблиц.</span><span class="sxs-lookup"><span data-stu-id="e2353-173">Hence, developing a data retention policy for managing data in the history table is an important aspect of planning and managing the lifecycle of every temporal table.</span></span> <span data-ttu-id="e2353-174">При использовании базы данных SQL Azure доступны следующие подходы для управления данными журнала во временной таблице.</span><span class="sxs-lookup"><span data-stu-id="e2353-174">With Azure SQL Database, you have the following approaches for managing historical data in the temporal table:</span></span>

* [<span data-ttu-id="e2353-175">Секционирование таблиц.</span><span class="sxs-lookup"><span data-stu-id="e2353-175">Table Partitioning</span></span>](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_2)
* [<span data-ttu-id="e2353-176">Пользовательский сценарий очистки</span><span class="sxs-lookup"><span data-stu-id="e2353-176">Custom Cleanup Script</span></span>](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_3)

## <a name="next-steps"></a><span data-ttu-id="e2353-177">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e2353-177">Next steps</span></span>
<span data-ttu-id="e2353-178">Дополнительные сведения о темпоральных таблицах см. в [документации MSDN](https://msdn.microsoft.com/library/dn935015.aspx).</span><span class="sxs-lookup"><span data-stu-id="e2353-178">For detailed information on Temporal Tables, check out [MSDN documentation](https://msdn.microsoft.com/library/dn935015.aspx).</span></span>
<span data-ttu-id="e2353-179">Посетите сайт Channel 9, чтобы ознакомиться с [историей успешного внедрения временных решений реальным клиентом](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) и посмотреть наглядную [демонстрацию временных решений](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span><span class="sxs-lookup"><span data-stu-id="e2353-179">Visit Channel 9 to hear a [real customer temporal implemenation success story](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) and watch a [live temporal demonstration](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span></span>

