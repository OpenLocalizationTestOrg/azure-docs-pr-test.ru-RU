---
title: "aaaManage группы баз данных Azure SQL | Документы Microsoft"
description: "Пошаговая инструкция по созданию задания эластичной базы данных и управлению им."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: f858344d-085b-4022-935e-1b5fa20adbac
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: a73c4fb24c332fae0e917c18272724cccd56f29a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-scaled-out-azure-sql-databases-using-elastic-jobs-preview"></a><span data-ttu-id="83ca2-103">Создание развернутых баз данных SQL Azure и управление ими с помощью заданий обработки эластичных БД (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="83ca2-103">Create and manage scaled out Azure SQL Databases using elastic jobs (preview)</span></span>


<span data-ttu-id="83ca2-104">**Задания обработки эластичных баз данных** упрощают управление группами баз данных, выполнение таких административных задач, как изменение схем, управление учетными данными, обновление эталонных данных, сбор данных о производительности или сбор данных телеметрии клиентов.</span><span class="sxs-lookup"><span data-stu-id="83ca2-104">**Elastic Database jobs** simplify management of groups of databases by executing administrative operations such as schema changes, credentials management, reference data updates, performance data collection or tenant (customer) telemetry collection.</span></span> <span data-ttu-id="83ca2-105">Заданий эластичных баз данных в настоящее время доступна через портал Azure hello и командлеты PowerShell.</span><span class="sxs-lookup"><span data-stu-id="83ca2-105">Elastic Database jobs is currently available through hello Azure portal and PowerShell cmdlets.</span></span> <span data-ttu-id="83ca2-106">Однако hello Azure портала предоставляет доступ к ограниченной функциональности ограниченный tooexecution среди всех баз данных в [эластичного пула (Предварительная версия)](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="83ca2-106">However, hello Azure portal surfaces reduced functionality limited tooexecution across all databases in an [elastic pool (preview)](sql-database-elastic-pool.md).</span></span> <span data-ttu-id="83ca2-107">задать дополнительные функции tooaccess и выполнение сценариев между несколькими базами данных, включая коллекцию пользовательских или сегмент (создан с помощью [клиентской библиотеке эластичной базы данных](sql-database-elastic-scale-introduction.md)), в разделе [Создание и управление задания с помощью PowerShell](sql-database-elastic-jobs-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="83ca2-107">tooaccess additional features and execution of scripts across a group of databases including a custom-defined collection or a shard set (created using [Elastic Database client library](sql-database-elastic-scale-introduction.md)), see [Creating and managing jobs using PowerShell](sql-database-elastic-jobs-powershell.md).</span></span> <span data-ttu-id="83ca2-108">Дополнительные сведения о заданиях см. в статье [Управление масштабируемыми облачными базами данных](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="83ca2-108">For more information about jobs, see [Elastic Database jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="83ca2-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="83ca2-109">Prerequisites</span></span>
* <span data-ttu-id="83ca2-110">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="83ca2-110">An Azure subscription.</span></span> <span data-ttu-id="83ca2-111">Бесплатная пробная версия доступна [здесь](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="83ca2-111">For a free trial, see [Free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="83ca2-112">Пул эластичных баз данных.</span><span class="sxs-lookup"><span data-stu-id="83ca2-112">An elastic pool.</span></span> <span data-ttu-id="83ca2-113">Ознакомьтесь с [пулами эластичных баз данных](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="83ca2-113">See [About elastic pools](sql-database-elastic-pool.md).</span></span>
* <span data-ttu-id="83ca2-114">Установка компонентов службы заданий обработки эластичных баз данных.</span><span class="sxs-lookup"><span data-stu-id="83ca2-114">Installation of elastic database job service components.</span></span> <span data-ttu-id="83ca2-115">В разделе [Установка hello эластичной базы данных задание службы](sql-database-elastic-jobs-service-installation.md).</span><span class="sxs-lookup"><span data-stu-id="83ca2-115">See [Installing hello elastic database job service](sql-database-elastic-jobs-service-installation.md).</span></span>

## <a name="creating-jobs"></a><span data-ttu-id="83ca2-116">Создание заданий</span><span class="sxs-lookup"><span data-stu-id="83ca2-116">Creating jobs</span></span>
1. <span data-ttu-id="83ca2-117">С помощью hello [портал Azure](https://portal.azure.com), из существующего пула эластичной базы данных задание, щелкните **создать задание**.</span><span class="sxs-lookup"><span data-stu-id="83ca2-117">Using hello [Azure portal](https://portal.azure.com), from an existing elastic database job pool, click **Create job**.</span></span>
2. <span data-ttu-id="83ca2-118">Введите hello имя пользователя и пароль администратора базы данных hello (созданные во время установки заданий) для базы данных управления заданиями hello (хранилище метаданных для заданий).</span><span class="sxs-lookup"><span data-stu-id="83ca2-118">Type in hello username and password of hello database administrator (created at installation of Jobs) for hello jobs control database (metadata storage for jobs).</span></span>
   
    ![Имя задания hello, введите или вставьте код и нажмите кнопку выполнения][1]
3. <span data-ttu-id="83ca2-120">В hello **создать задание** колонки, введите имя для задания hello.</span><span class="sxs-lookup"><span data-stu-id="83ca2-120">In hello **Create Job** blade, type a name for hello job.</span></span>
4. <span data-ttu-id="83ca2-121">Введите hello пользователя имя и пароль tooconnect toohello целевой базы данных с разрешениями, достаточными для выполнения toosucceed сценария.</span><span class="sxs-lookup"><span data-stu-id="83ca2-121">Type hello user name and password tooconnect toohello target databases with sufficient permissions for script execution toosucceed.</span></span>
5. <span data-ttu-id="83ca2-122">Вставьте или введите в скрипте hello T-SQL.</span><span class="sxs-lookup"><span data-stu-id="83ca2-122">Paste or type in hello T-SQL script.</span></span>
6. <span data-ttu-id="83ca2-123">Щелкните **Сохранить**, а затем нажмите кнопку **Запустить**.</span><span class="sxs-lookup"><span data-stu-id="83ca2-123">Click **Save** and then click **Run**.</span></span>
   
    ![Создание заданий и их выполнение][5]

## <a name="run-idempotent-jobs"></a><span data-ttu-id="83ca2-125">Запуск идемпотентных заданий</span><span class="sxs-lookup"><span data-stu-id="83ca2-125">Run idempotent jobs</span></span>
<span data-ttu-id="83ca2-126">При выполнении сценария набор баз данных, необходимо убедиться, что hello скрипта является идемпотентной.</span><span class="sxs-lookup"><span data-stu-id="83ca2-126">When you run a script against a set of databases, you must be sure that hello script is idempotent.</span></span> <span data-ttu-id="83ca2-127">То есть hello скрипт должен быть toorun может несколько раз, даже если он завершается сбоем перед незавершенной.</span><span class="sxs-lookup"><span data-stu-id="83ca2-127">That is, hello script must be able toorun multiple times, even if it has failed before in an incomplete state.</span></span> <span data-ttu-id="83ca2-128">Например, при сбое скрипта, задания hello автоматически повторит до ее успешного выполнения (в пределах, как "Повторить" hello логику со временем, перестанут Повтор hello).</span><span class="sxs-lookup"><span data-stu-id="83ca2-128">For example, when a script fails, hello job will be automatically retried until it succeeds (within limits, as hello retry logic will eventually cease hello retrying).</span></span> <span data-ttu-id="83ca2-129">toodo способом Hello это предложение «IF EXISTS» toouse hello и удалить любой найден экземпляр перед созданием нового объекта.</span><span class="sxs-lookup"><span data-stu-id="83ca2-129">hello way toodo this is toouse hello an "IF EXISTS" clause and delete any found instance before creating a new object.</span></span> <span data-ttu-id="83ca2-130">Ниже приведен пример.</span><span class="sxs-lookup"><span data-stu-id="83ca2-130">An example is shown here:</span></span>

    IF EXISTS (SELECT name FROM sys.indexes
            WHERE name = N'IX_ProductVendor_VendorID')
    DROP INDEX IX_ProductVendor_VendorID ON Purchasing.ProductVendor;
    GO
    CREATE INDEX IX_ProductVendor_VendorID
    ON Purchasing.ProductVendor (VendorID);

<span data-ttu-id="83ca2-131">Или используйте предложение IF NOT EXISTS перед созданием нового экземпляра:</span><span class="sxs-lookup"><span data-stu-id="83ca2-131">Alternatively, use an "IF NOT EXISTS" clause before creating a new instance:</span></span>

    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
     CREATE TABLE TestTable(
      TestTableId INT PRIMARY KEY IDENTITY,
      InsertionTime DATETIME2
     );
    END
    GO

    INSERT INTO TestTable(InsertionTime) VALUES (sysutcdatetime());
    GO

<span data-ttu-id="83ca2-132">Затем этот скрипт обновляет hello таблицы, созданной ранее.</span><span class="sxs-lookup"><span data-stu-id="83ca2-132">This script then updates hello table created previously.</span></span>

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN

    ALTER TABLE TestTable

    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO


## <a name="checking-job-status"></a><span data-ttu-id="83ca2-133">Проверка состояния заданий</span><span class="sxs-lookup"><span data-stu-id="83ca2-133">Checking job status</span></span>
<span data-ttu-id="83ca2-134">После запуска задания вы можете проверить ход его выполнения.</span><span class="sxs-lookup"><span data-stu-id="83ca2-134">After a job has begun, you can check on its progress.</span></span>

1. <span data-ttu-id="83ca2-135">На странице приветствия эластичного пула нажмите **управление заданиями**.</span><span class="sxs-lookup"><span data-stu-id="83ca2-135">From hello elastic pool page, click **Manage jobs**.</span></span>
   
    ![Щелкните "Управление заданиями".][2]
2. <span data-ttu-id="83ca2-137">Щелкните hello имя (a) задания.</span><span class="sxs-lookup"><span data-stu-id="83ca2-137">Click on hello name (a) of a job.</span></span> <span data-ttu-id="83ca2-138">Hello **состояние** может быть «Завершено» или «Ошибка».</span><span class="sxs-lookup"><span data-stu-id="83ca2-138">hello **STATUS** can be "Completed" or "Failed."</span></span> <span data-ttu-id="83ca2-139">сведения о задании Hello отображаются (b) с его дату и время создания и выполнения.</span><span class="sxs-lookup"><span data-stu-id="83ca2-139">hello job's details appear (b) with its date and time of creation and running.</span></span> <span data-ttu-id="83ca2-140">Hello (c) ниже списке hello, показывающий ход выполнения hello hello скрипт для каждой базы данных в пуле hello, предоставления сведений о нем даты и времени.</span><span class="sxs-lookup"><span data-stu-id="83ca2-140">hello list (c) below hello that shows hello progress of hello script against each database in hello pool, giving its date and time details.</span></span>
   
    ![Проверка завершенного задания][3]

## <a name="checking-failed-jobs"></a><span data-ttu-id="83ca2-142">Проверка невыполненных заданий</span><span class="sxs-lookup"><span data-stu-id="83ca2-142">Checking failed jobs</span></span>
<span data-ttu-id="83ca2-143">Если происходит сбой задания, можно просмотреть журнал его выполнения.</span><span class="sxs-lookup"><span data-stu-id="83ca2-143">If a job fails, a log of its execution can found.</span></span> <span data-ttu-id="83ca2-144">Щелкните имя hello toosee hello не удалось выполнить задание сведений о нем.</span><span class="sxs-lookup"><span data-stu-id="83ca2-144">Click hello name of hello failed job toosee its details.</span></span>

![Проверка невыполненного задания][4]

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-create-and-manage/screen-1.png
[2]: ./media/sql-database-elastic-jobs-create-and-manage/click-manage-jobs.png
[3]: ./media/sql-database-elastic-jobs-create-and-manage/running-jobs.png
[4]: ./media/sql-database-elastic-jobs-create-and-manage/failed.png
[5]: ./media/sql-database-elastic-jobs-create-and-manage/screen-2.png


