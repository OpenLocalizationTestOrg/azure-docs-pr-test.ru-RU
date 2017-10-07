---
title: "Портал Azure: георепликация базы данных SQL | Документация Майкрософт"
description: "Настройка географической репликации для базы данных SQL Azure в hello портал Azure и инициировать отработку отказа"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: d0b29822-714f-4633-a5ab-fb1a09d43ced
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/06/2016
ms.author: carlrab
ms.openlocfilehash: 09cbbdb040f36c42593e3be87ce6db2238f36656
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-geo-replication-for-azure-sql-database-in-hello-azure-portal-and-initiate-failover"></a><span data-ttu-id="0a90c-103">Настройка активной георепликации для базы данных SQL Azure в hello портал Azure и инициировать отработку отказа</span><span class="sxs-lookup"><span data-stu-id="0a90c-103">Configure active geo-replication for Azure SQL Database in hello Azure portal and initiate failover</span></span>

<span data-ttu-id="0a90c-104">В этой статье показано, как tooconfigure активной георепликации для базы данных SQL в hello [портал Azure](http://portal.azure.com) и tooinitiate перехода на другой ресурс.</span><span class="sxs-lookup"><span data-stu-id="0a90c-104">This article shows you how tooconfigure active geo-replication for SQL Database in hello [Azure portal](http://portal.azure.com) and tooinitiate failover.</span></span>

<span data-ttu-id="0a90c-105">tooinitiate переход на другой ресурс hello портал Azure в разделе [инициации плановой или незапланированной отработки отказа для базы данных SQL Azure с портала Azure hello](sql-database-geo-replication-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0a90c-105">tooinitiate failover with hello Azure portal, see [Initiate a planned or unplanned failover for Azure SQL Database with hello Azure portal](sql-database-geo-replication-portal.md).</span></span>

<span data-ttu-id="0a90c-106">tooconfigure активной георепликации с помощью hello портал Azure, требуется hello следующих ресурсов:</span><span class="sxs-lookup"><span data-stu-id="0a90c-106">tooconfigure active geo-replication by using hello Azure portal, you need hello following resource:</span></span>

* <span data-ttu-id="0a90c-107">Базы данных Azure SQL: hello базы данных-источника, которые должны tooreplicate tooa другом географическом регионе.</span><span class="sxs-lookup"><span data-stu-id="0a90c-107">An Azure SQL database: hello primary database that you want tooreplicate tooa different geographical region.</span></span>

> [!Note]
<span data-ttu-id="0a90c-108">Должен быть активной георепликации между базами данных в hello одной подписке.</span><span class="sxs-lookup"><span data-stu-id="0a90c-108">Active geo-replication must be between databases in hello same subscription.</span></span>

## <a name="add-a-secondary-database"></a><span data-ttu-id="0a90c-109">Добавление базы данных-получателя</span><span class="sxs-lookup"><span data-stu-id="0a90c-109">Add a secondary database</span></span>
<span data-ttu-id="0a90c-110">Hello следующие действия создадут новые базы данных-получателя в связи георепликации.</span><span class="sxs-lookup"><span data-stu-id="0a90c-110">hello following steps create a new secondary database in a geo-replication partnership.</span></span>  

<span data-ttu-id="0a90c-111">tooadd базы данных-получателя, необходимо быть владельцем подписки hello или совладелец.</span><span class="sxs-lookup"><span data-stu-id="0a90c-111">tooadd a secondary database, you must be hello subscription owner or co-owner.</span></span>

<span data-ttu-id="0a90c-112">База данных-получатель Hello имеет точно такое же имя в качестве базы данных-источника hello hello и по умолчанию hello того же уровня обслуживания.</span><span class="sxs-lookup"><span data-stu-id="0a90c-112">hello secondary database has hello same name as hello primary database and has, by default, hello same service level.</span></span> <span data-ttu-id="0a90c-113">Hello баз данных-получателей может быть одной базы данных или базы данных в пуле эластичных БД.</span><span class="sxs-lookup"><span data-stu-id="0a90c-113">hello secondary database can be a single database or a database in an elastic pool.</span></span> <span data-ttu-id="0a90c-114">Чтобы узнать больше, ознакомьтесь с [уровнями служб](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="0a90c-114">For more information, see [Service tiers](sql-database-service-tiers.md).</span></span>
<span data-ttu-id="0a90c-115">После hello получателя создается и заполняется, данных начинает репликации из hello базы данных-источника toohello базы данных-получателя.</span><span class="sxs-lookup"><span data-stu-id="0a90c-115">After hello secondary is created and seeded, data begins replicating from hello primary database toohello new secondary database.</span></span>

> [!NOTE]
> <span data-ttu-id="0a90c-116">Наличие hello участника базы данных (например, в результате завершения предыдущей связи георепликации) hello команда завершается ошибкой.</span><span class="sxs-lookup"><span data-stu-id="0a90c-116">If hello partner database already exists (for example, as a result of terminating a previous geo-replication relationship) hello command fails.</span></span>
> 

1. <span data-ttu-id="0a90c-117">В hello [портал Azure](http://portal.azure.com), просмотра toohello базы данных, которые должны tooset для географической репликации.</span><span class="sxs-lookup"><span data-stu-id="0a90c-117">In hello [Azure portal](http://portal.azure.com), browse toohello database that you want tooset up for geo-replication.</span></span>
2. <span data-ttu-id="0a90c-118">На странице базы данных SQL hello выберите **георепликации**и выберите hello области toocreate hello баз данных-получателей.</span><span class="sxs-lookup"><span data-stu-id="0a90c-118">On hello SQL database page, select **geo-replication**, and then select hello region toocreate hello secondary database.</span></span> <span data-ttu-id="0a90c-119">Можно выбрать любой регионе, отличном от региона hello размещение базы данных-источника hello, но мы рекомендуем hello [парном регионе](../best-practices-availability-paired-regions.md).</span><span class="sxs-lookup"><span data-stu-id="0a90c-119">You can select any region other than hello region hosting hello primary database, but we recommend hello [paired region](../best-practices-availability-paired-regions.md).</span></span>
   
    ![Настройка георепликации](./media/sql-database-geo-replication-portal/configure-geo-replication.png)
3. <span data-ttu-id="0a90c-121">Выбор или Настройка сервера hello и ценовую категорию для базы данных-получателя hello.</span><span class="sxs-lookup"><span data-stu-id="0a90c-121">Select or configure hello server and pricing tier for hello secondary database.</span></span>
   
    ![Настройка базы данных-получателя](./media/sql-database-geo-replication-portal/create-secondary.png)
4. <span data-ttu-id="0a90c-123">При необходимости можно добавить tooan эластичный пул баз данных-получателей.</span><span class="sxs-lookup"><span data-stu-id="0a90c-123">Optionally, you can add a secondary database tooan elastic pool.</span></span> <span data-ttu-id="0a90c-124">Щелкните toocreate hello базы данных-получателя в пуле, **эластичного пула** и выберите пул на целевом сервере hello.</span><span class="sxs-lookup"><span data-stu-id="0a90c-124">toocreate hello secondary database in a pool, click **elastic pool** and select a pool on hello target server.</span></span> <span data-ttu-id="0a90c-125">Пул должен уже существовать на целевом сервере hello.</span><span class="sxs-lookup"><span data-stu-id="0a90c-125">A pool must already exist on hello target server.</span></span> <span data-ttu-id="0a90c-126">Этот рабочий процесс не создает пул.</span><span class="sxs-lookup"><span data-stu-id="0a90c-126">This workflow does not create a pool.</span></span>
5. <span data-ttu-id="0a90c-127">Нажмите кнопку **создать** tooadd hello получателей.</span><span class="sxs-lookup"><span data-stu-id="0a90c-127">Click **Create** tooadd hello secondary.</span></span>
6. <span data-ttu-id="0a90c-128">создается база данных-получатель Hello и начинает процесс заполнения hello.</span><span class="sxs-lookup"><span data-stu-id="0a90c-128">hello secondary database is created and hello seeding process begins.</span></span>
   
    ![Настройка базы данных-получателя](./media/sql-database-geo-replication-portal/seeding0.png)
7. <span data-ttu-id="0a90c-130">После завершения процесса заполнения hello баз данных-получателей hello отображение его состояния.</span><span class="sxs-lookup"><span data-stu-id="0a90c-130">When hello seeding process is complete, hello secondary database displays its status.</span></span>
   
    ![Заполнение завершено](./media/sql-database-geo-replication-portal/seeding-complete.png)

## <a name="initiate-a-failover"></a><span data-ttu-id="0a90c-132">Запуск отработки отказа</span><span class="sxs-lookup"><span data-stu-id="0a90c-132">Initiate a failover</span></span>

<span data-ttu-id="0a90c-133">Hello баз данных-получателей может быть выключены toobecome hello основной.</span><span class="sxs-lookup"><span data-stu-id="0a90c-133">hello secondary database can be switched toobecome hello primary.</span></span>  

1. <span data-ttu-id="0a90c-134">В hello [портал Azure](http://portal.azure.com), Обзор toohello основной базой данных hello связи георепликации.</span><span class="sxs-lookup"><span data-stu-id="0a90c-134">In hello [Azure portal](http://portal.azure.com), browse toohello primary database in hello geo-replication partnership.</span></span>
2. <span data-ttu-id="0a90c-135">В колонке базы данных SQL hello, выберите **все параметры** > **георепликации**.</span><span class="sxs-lookup"><span data-stu-id="0a90c-135">On hello SQL Database blade, select **All settings** > **geo-replication**.</span></span>
3. <span data-ttu-id="0a90c-136">В hello **баз данных-ПОЛУЧАТЕЛЕЙ** список, выберите hello базы данных, которая toobecome hello новом сервере-источнике и нажмите кнопку **перехода на другой ресурс**.</span><span class="sxs-lookup"><span data-stu-id="0a90c-136">In hello **SECONDARIES** list, select hello database you want toobecome hello new primary and click **Failover**.</span></span>
   
    ![Отработка отказа](./media/sql-database-geo-replication-failover-portal/secondaries.png)
4. <span data-ttu-id="0a90c-138">Нажмите кнопку **Да** hello toobegin перехода на другой ресурс.</span><span class="sxs-lookup"><span data-stu-id="0a90c-138">Click **Yes** toobegin hello failover.</span></span>

<span data-ttu-id="0a90c-139">Команда Hello немедленно переключается hello базы данных-получателя в первичной роли hello.</span><span class="sxs-lookup"><span data-stu-id="0a90c-139">hello command immediately switches hello secondary database into hello primary role.</span></span> 

<span data-ttu-id="0a90c-140">Отсутствует короткий период, в течение которого обеих баз данных недоступны (в порядке hello 0 секунд too25) во время переключения ролей hello.</span><span class="sxs-lookup"><span data-stu-id="0a90c-140">There is a short period during which both databases are unavailable (on hello order of 0 too25 seconds) while hello roles are switched.</span></span> <span data-ttu-id="0a90c-141">Если база данных-источник hello имеет несколько баз данных-получателей, команда hello автоматически перенастройка hello других баз данных-получателей tooconnect toohello новом сервере-источнике.</span><span class="sxs-lookup"><span data-stu-id="0a90c-141">If hello primary database has multiple secondary databases, hello command automatically reconfigures hello other secondaries tooconnect toohello new primary.</span></span> <span data-ttu-id="0a90c-142">вся операция Hello занимает меньше минуты toocomplete в обычных условиях.</span><span class="sxs-lookup"><span data-stu-id="0a90c-142">hello entire operation should take less than a minute toocomplete under normal circumstances.</span></span> 

> [!NOTE]
> <span data-ttu-id="0a90c-143">Эта команда предназначена для быстрого восстановления hello базы данных в случае сбоя.</span><span class="sxs-lookup"><span data-stu-id="0a90c-143">This command is designed for quick recovery of hello database in case of an outage.</span></span> <span data-ttu-id="0a90c-144">Она активирует отработку отказа без синхронизации данных (принудительная отработка отказа).</span><span class="sxs-lookup"><span data-stu-id="0a90c-144">It triggers failover without data synchronization (forced failover).</span></span>  <span data-ttu-id="0a90c-145">Если основной hello находится в оперативном режиме и фиксации транзакций, когда hello команды потеря данных возможна.</span><span class="sxs-lookup"><span data-stu-id="0a90c-145">If hello primary is online and committing transactions when hello command is issued some data loss may occur.</span></span> 
> 
> 

## <a name="remove-secondary-database"></a><span data-ttu-id="0a90c-146">Удаление базы данных-получателя</span><span class="sxs-lookup"><span data-stu-id="0a90c-146">Remove secondary database</span></span>
<span data-ttu-id="0a90c-147">Эта операция безвозвратно завершает hello репликации toohello баз данных-получателей, а изменения hello роль базы данных hello получателей tooa регулярного чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="0a90c-147">This operation permanently terminates hello replication toohello secondary database, and changes hello role of hello secondary tooa regular read-write database.</span></span> <span data-ttu-id="0a90c-148">Если нарушена hello подключения toohello баз данных-получателей, hello команда выполняется успешно, но hello чтения и записи вторичных выполняет становится до, после восстановления подключения.</span><span class="sxs-lookup"><span data-stu-id="0a90c-148">If hello connectivity toohello secondary database is broken, hello command succeeds but hello secondary does not become read-write until after connectivity is restored.</span></span>  

1. <span data-ttu-id="0a90c-149">В hello [портал Azure](http://portal.azure.com), Обзор toohello основной базой данных hello связи георепликации.</span><span class="sxs-lookup"><span data-stu-id="0a90c-149">In hello [Azure portal](http://portal.azure.com), browse toohello primary database in hello geo-replication partnership.</span></span>
2. <span data-ttu-id="0a90c-150">На странице базы данных SQL hello выберите **георепликации**.</span><span class="sxs-lookup"><span data-stu-id="0a90c-150">On hello SQL database page, select **geo-replication**.</span></span>
3. <span data-ttu-id="0a90c-151">В hello **баз данных-ПОЛУЧАТЕЛЕЙ** список, выберите hello базы данных, которая tooremove из hello связи георепликации.</span><span class="sxs-lookup"><span data-stu-id="0a90c-151">In hello **SECONDARIES** list, select hello database you want tooremove from hello geo-replication partnership.</span></span>
4. <span data-ttu-id="0a90c-152">Щелкните **Остановить репликацию**.</span><span class="sxs-lookup"><span data-stu-id="0a90c-152">Click **Stop Replication**.</span></span>
   
    ![Удаление базы данных-получателя](./media/sql-database-geo-replication-portal/remove-secondary.png)
5. <span data-ttu-id="0a90c-154">Откроется окно подтверждения.</span><span class="sxs-lookup"><span data-stu-id="0a90c-154">A confirmation window opens.</span></span> <span data-ttu-id="0a90c-155">Нажмите кнопку **Да** базы данных hello tooremove из hello связи георепликации.</span><span class="sxs-lookup"><span data-stu-id="0a90c-155">Click **Yes** tooremove hello database from hello geo-replication partnership.</span></span> <span data-ttu-id="0a90c-156">(Задайте его tooa чтения и записи базы данных не является частью любой репликации.)</span><span class="sxs-lookup"><span data-stu-id="0a90c-156">(Set it tooa read-write database not part of any replication.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a90c-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0a90c-157">Next steps</span></span>
* <span data-ttu-id="0a90c-158">разделе toolearn Дополнительные сведения об активной георепликации [активной георепликации](sql-database-geo-replication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0a90c-158">toolearn more about active geo-replication, see [active geo-replication](sql-database-geo-replication-overview.md).</span></span>
* <span data-ttu-id="0a90c-159">Сведения об обеспечении непрерывности бизнес-процессов и возможные сценарии описаны в [обзоре непрерывности бизнес-процессов](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="0a90c-159">For a business continuity overview and scenarios, see [Business continuity overview](sql-database-business-continuity.md).</span></span>

