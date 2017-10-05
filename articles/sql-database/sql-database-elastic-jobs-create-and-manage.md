---
title: "Управление группами баз данных SQL Azure | Документация Майкрософт"
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
ms.openlocfilehash: d30cc74778e0b36dd632c2f040ce80d1ca8af5a5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-scaled-out-azure-sql-databases-using-elastic-jobs-preview"></a><span data-ttu-id="0210b-103">Создание развернутых баз данных SQL Azure и управление ими с помощью заданий обработки эластичных БД (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="0210b-103">Create and manage scaled out Azure SQL Databases using elastic jobs (preview)</span></span>


<span data-ttu-id="0210b-104">**Задания обработки эластичных баз данных** упрощают управление группами баз данных, выполнение таких административных задач, как изменение схем, управление учетными данными, обновление эталонных данных, сбор данных о производительности или сбор данных телеметрии клиентов.</span><span class="sxs-lookup"><span data-stu-id="0210b-104">**Elastic Database jobs** simplify management of groups of databases by executing administrative operations such as schema changes, credentials management, reference data updates, performance data collection or tenant (customer) telemetry collection.</span></span> <span data-ttu-id="0210b-105">В настоящий момент задания обработки эластичных баз данных доступны на портале Azure и через командлеты PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0210b-105">Elastic Database jobs is currently available through the Azure portal and PowerShell cmdlets.</span></span> <span data-ttu-id="0210b-106">Тем не менее портал Azure предоставляет ограниченные возможности, доступные для всех баз данных в [пуле эластичных баз данных (предварительная версия)](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="0210b-106">However, the Azure portal surfaces reduced functionality limited to execution across all databases in an [elastic pool (preview)](sql-database-elastic-pool.md).</span></span> <span data-ttu-id="0210b-107">Для доступа к дополнительным функциям и выполнения скриптов в группе баз данных, включающей определенное пользователем семейство или набор сегментов (созданный с помощью [клиентской библиотеки эластичных баз данных](sql-database-elastic-scale-introduction.md)), см. статью [Создание заданий обработки эластичных баз данных для Базы данных SQL и управление ими с помощью PowerShell (предварительная версия)](sql-database-elastic-jobs-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="0210b-107">To access additional features and execution of scripts across a group of databases including a custom-defined collection or a shard set (created using [Elastic Database client library](sql-database-elastic-scale-introduction.md)), see [Creating and managing jobs using PowerShell](sql-database-elastic-jobs-powershell.md).</span></span> <span data-ttu-id="0210b-108">Дополнительные сведения о заданиях см. в статье [Управление масштабируемыми облачными базами данных](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0210b-108">For more information about jobs, see [Elastic Database jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="0210b-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0210b-109">Prerequisites</span></span>
* <span data-ttu-id="0210b-110">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="0210b-110">An Azure subscription.</span></span> <span data-ttu-id="0210b-111">Бесплатная пробная версия доступна [здесь](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0210b-111">For a free trial, see [Free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="0210b-112">Пул эластичных баз данных.</span><span class="sxs-lookup"><span data-stu-id="0210b-112">An elastic pool.</span></span> <span data-ttu-id="0210b-113">Ознакомьтесь с [пулами эластичных баз данных](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="0210b-113">See [About elastic pools](sql-database-elastic-pool.md).</span></span>
* <span data-ttu-id="0210b-114">Установка компонентов службы заданий обработки эластичных баз данных.</span><span class="sxs-lookup"><span data-stu-id="0210b-114">Installation of elastic database job service components.</span></span> <span data-ttu-id="0210b-115">См. статью [Обзор установки заданий обработки эластичных баз данных](sql-database-elastic-jobs-service-installation.md).</span><span class="sxs-lookup"><span data-stu-id="0210b-115">See [Installing the elastic database job service](sql-database-elastic-jobs-service-installation.md).</span></span>

## <a name="creating-jobs"></a><span data-ttu-id="0210b-116">Создание заданий</span><span class="sxs-lookup"><span data-stu-id="0210b-116">Creating jobs</span></span>
1. <span data-ttu-id="0210b-117">На [портале Azure](https://portal.azure.com)в существующем пуле заданий обработки эластичных баз данных нажмите **Создать задание**.</span><span class="sxs-lookup"><span data-stu-id="0210b-117">Using the [Azure portal](https://portal.azure.com), from an existing elastic database job pool, click **Create job**.</span></span>
2. <span data-ttu-id="0210b-118">Введите имя пользователя и пароль администратора (создаются во время установки заданий) управляющей базы данных заданий (хранилище метаданных для заданий).</span><span class="sxs-lookup"><span data-stu-id="0210b-118">Type in the username and password of the database administrator (created at installation of Jobs) for the jobs control database (metadata storage for jobs).</span></span>
   
    ![Назовите задание, введите или вставьте код, а затем нажмите кнопку "Выполнить".][1]
3. <span data-ttu-id="0210b-120">В колонке **Создание задания** введите имя задания.</span><span class="sxs-lookup"><span data-stu-id="0210b-120">In the **Create Job** blade, type a name for the job.</span></span>
4. <span data-ttu-id="0210b-121">Введите имя пользователя и пароль для подключения к целевым базам данных. Эти учетные данные должны обладать достаточными разрешениями, иначе сценарий не выполнится.</span><span class="sxs-lookup"><span data-stu-id="0210b-121">Type the user name and password to connect to the target databases with sufficient permissions for script execution to succeed.</span></span>
5. <span data-ttu-id="0210b-122">Вставьте или введите сценарий T-SQL.</span><span class="sxs-lookup"><span data-stu-id="0210b-122">Paste or type in the T-SQL script.</span></span>
6. <span data-ttu-id="0210b-123">Щелкните **Сохранить**, а затем нажмите кнопку **Запустить**.</span><span class="sxs-lookup"><span data-stu-id="0210b-123">Click **Save** and then click **Run**.</span></span>
   
    ![Создание заданий и их выполнение][5]

## <a name="run-idempotent-jobs"></a><span data-ttu-id="0210b-125">Запуск идемпотентных заданий</span><span class="sxs-lookup"><span data-stu-id="0210b-125">Run idempotent jobs</span></span>
<span data-ttu-id="0210b-126">При запуске сценария для набора баз данных необходимо убедиться, что сценарий является идемпотентным.</span><span class="sxs-lookup"><span data-stu-id="0210b-126">When you run a script against a set of databases, you must be sure that the script is idempotent.</span></span> <span data-ttu-id="0210b-127">То есть в сценарий должна быть заложена возможность многоразового запуска, даже если он завершился сбоем до завершения выполнения.</span><span class="sxs-lookup"><span data-stu-id="0210b-127">That is, the script must be able to run multiple times, even if it has failed before in an incomplete state.</span></span> <span data-ttu-id="0210b-128">Например, при сбое сценария задание будет автоматически повторяться, пока не будет успешно выполнено (в установленных пределах, так как логика повтора в конечном итоге прекратит попытки).</span><span class="sxs-lookup"><span data-stu-id="0210b-128">For example, when a script fails, the job will be automatically retried until it succeeds (within limits, as the retry logic will eventually cease the retrying).</span></span> <span data-ttu-id="0210b-129">Чтобы сделать это, используйте предложение IF EXISTS и удалите все найденные экземпляры перед созданием нового объекта.</span><span class="sxs-lookup"><span data-stu-id="0210b-129">The way to do this is to use the an "IF EXISTS" clause and delete any found instance before creating a new object.</span></span> <span data-ttu-id="0210b-130">Ниже приведен пример.</span><span class="sxs-lookup"><span data-stu-id="0210b-130">An example is shown here:</span></span>

    IF EXISTS (SELECT name FROM sys.indexes
            WHERE name = N'IX_ProductVendor_VendorID')
    DROP INDEX IX_ProductVendor_VendorID ON Purchasing.ProductVendor;
    GO
    CREATE INDEX IX_ProductVendor_VendorID
    ON Purchasing.ProductVendor (VendorID);

<span data-ttu-id="0210b-131">Или используйте предложение IF NOT EXISTS перед созданием нового экземпляра:</span><span class="sxs-lookup"><span data-stu-id="0210b-131">Alternatively, use an "IF NOT EXISTS" clause before creating a new instance:</span></span>

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

<span data-ttu-id="0210b-132">Этот сценарий обновляет таблицу, созданную ранее.</span><span class="sxs-lookup"><span data-stu-id="0210b-132">This script then updates the table created previously.</span></span>

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN

    ALTER TABLE TestTable

    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO


## <a name="checking-job-status"></a><span data-ttu-id="0210b-133">Проверка состояния заданий</span><span class="sxs-lookup"><span data-stu-id="0210b-133">Checking job status</span></span>
<span data-ttu-id="0210b-134">После запуска задания вы можете проверить ход его выполнения.</span><span class="sxs-lookup"><span data-stu-id="0210b-134">After a job has begun, you can check on its progress.</span></span>

1. <span data-ttu-id="0210b-135">На странице пула эластичных баз данных щелкните **Управление заданиями**.</span><span class="sxs-lookup"><span data-stu-id="0210b-135">From the elastic pool page, click **Manage jobs**.</span></span>
   
    ![Щелкните "Управление заданиями".][2]
2. <span data-ttu-id="0210b-137">Щелкните имя (a) задания.</span><span class="sxs-lookup"><span data-stu-id="0210b-137">Click on the name (a) of a job.</span></span> <span data-ttu-id="0210b-138">**СОСТОЯНИЕ** может быть «Завершено» или «Ошибка».</span><span class="sxs-lookup"><span data-stu-id="0210b-138">The **STATUS** can be "Completed" or "Failed."</span></span> <span data-ttu-id="0210b-139">Сведения о задании отображаются (b) с датой и временем его создания и выполнения.</span><span class="sxs-lookup"><span data-stu-id="0210b-139">The job's details appear (b) with its date and time of creation and running.</span></span> <span data-ttu-id="0210b-140">В списке (c) ниже отображается ход выполнения сценария для каждой базы данных в пуле и отображаются сведения о его дате и времени.</span><span class="sxs-lookup"><span data-stu-id="0210b-140">The list (c) below the that shows the progress of the script against each database in the pool, giving its date and time details.</span></span>
   
    ![Проверка завершенного задания][3]

## <a name="checking-failed-jobs"></a><span data-ttu-id="0210b-142">Проверка невыполненных заданий</span><span class="sxs-lookup"><span data-stu-id="0210b-142">Checking failed jobs</span></span>
<span data-ttu-id="0210b-143">Если происходит сбой задания, можно просмотреть журнал его выполнения.</span><span class="sxs-lookup"><span data-stu-id="0210b-143">If a job fails, a log of its execution can found.</span></span> <span data-ttu-id="0210b-144">Щелкните имя невыполненного задания, чтобы просмотреть сведения о нем.</span><span class="sxs-lookup"><span data-stu-id="0210b-144">Click the name of the failed job to see its details.</span></span>

![Проверка невыполненного задания][4]

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-create-and-manage/screen-1.png
[2]: ./media/sql-database-elastic-jobs-create-and-manage/click-manage-jobs.png
[3]: ./media/sql-database-elastic-jobs-create-and-manage/running-jobs.png
[4]: ./media/sql-database-elastic-jobs-create-and-manage/failed.png
[5]: ./media/sql-database-elastic-jobs-create-and-manage/screen-2.png


