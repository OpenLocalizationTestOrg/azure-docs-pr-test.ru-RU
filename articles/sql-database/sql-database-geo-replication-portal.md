---
title: "Портал Azure: георепликация базы данных SQL | Документация Майкрософт"
description: "Настройка георепликации для базы данных SQL Azure с помощью портала Azure и запуск отработки отказа."
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
ms.openlocfilehash: db90fad2fe397f0c8466db6bdc1bd8c8d1cf8f15
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configure-active-geo-replication-for-azure-sql-database-in-the-azure-portal-and-initiate-failover"></a><span data-ttu-id="b8b2d-103">Настройка активной георепликации для базы данных SQL Azure с помощью портала Azure и запуск отработки отказа</span><span class="sxs-lookup"><span data-stu-id="b8b2d-103">Configure active geo-replication for Azure SQL Database in the Azure portal and initiate failover</span></span>

<span data-ttu-id="b8b2d-104">В этой статье объясняется, как настроить активную георепликацию для базы данных SQL Azure с помощью [портала Azure](http://portal.azure.com) и запустить отработку отказа.</span><span class="sxs-lookup"><span data-stu-id="b8b2d-104">This article shows you how to configure active geo-replication for SQL Database in the [Azure portal](http://portal.azure.com) and to initiate failover.</span></span>

<span data-ttu-id="b8b2d-105">Сведения о запуске отработки отказа с помощью портала Azure см. в разделе [Запуск плановой или незапланированной отработки отказа для базы данных SQL Azure с помощью портала Azure](sql-database-geo-replication-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b8b2d-105">To initiate failover with the Azure portal, see [Initiate a planned or unplanned failover for Azure SQL Database with the Azure portal](sql-database-geo-replication-portal.md).</span></span>

<span data-ttu-id="b8b2d-106">Для настройки активной георепликации с помощью портала Azure необходим приведенный ниже ресурс.</span><span class="sxs-lookup"><span data-stu-id="b8b2d-106">To configure active geo-replication by using the Azure portal, you need the following resource:</span></span>

* <span data-ttu-id="b8b2d-107">База данных SQL Azure — база данных-источник, которую необходимо реплицировать в другом географическом регионе.</span><span class="sxs-lookup"><span data-stu-id="b8b2d-107">An Azure SQL database: The primary database that you want to replicate to a different geographical region.</span></span>

> [!Note]
<span data-ttu-id="b8b2d-108">Активная георепликация должна поддерживаться между базами данных в рамках одной подписки.</span><span class="sxs-lookup"><span data-stu-id="b8b2d-108">Active geo-replication must be between databases in the same subscription.</span></span>

## <a name="add-a-secondary-database"></a><span data-ttu-id="b8b2d-109">Добавление базы данных-получателя</span><span class="sxs-lookup"><span data-stu-id="b8b2d-109">Add a secondary database</span></span>
<span data-ttu-id="b8b2d-110">Следующие действия позволяют создать новую базу данных-получателя в связи георепликации.</span><span class="sxs-lookup"><span data-stu-id="b8b2d-110">The following steps create a new secondary database in a geo-replication partnership.</span></span>  

<span data-ttu-id="b8b2d-111">Добавить базу данных-получатель может только владелец или совладелец подписки.</span><span class="sxs-lookup"><span data-stu-id="b8b2d-111">To add a secondary database, you must be the subscription owner or co-owner.</span></span>

<span data-ttu-id="b8b2d-112">Базе данных-получателю присваивается такое же имя, как у базы данных-источника, и по умолчанию тот же уровень обслуживания.</span><span class="sxs-lookup"><span data-stu-id="b8b2d-112">The secondary database has the same name as the primary database and has, by default, the same service level.</span></span> <span data-ttu-id="b8b2d-113">База данных-получатель может быть отдельной базой данных или базой данных в эластичном пуле.</span><span class="sxs-lookup"><span data-stu-id="b8b2d-113">The secondary database can be a single database or a database in an elastic pool.</span></span> <span data-ttu-id="b8b2d-114">Чтобы узнать больше, ознакомьтесь с [уровнями служб](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="b8b2d-114">For more information, see [Service tiers](sql-database-service-tiers.md).</span></span>
<span data-ttu-id="b8b2d-115">После создания и заполнения базы данных-получателя начинается репликация данных из базы данных-источника в новую базу данных-получателя.</span><span class="sxs-lookup"><span data-stu-id="b8b2d-115">After the secondary is created and seeded, data begins replicating from the primary database to the new secondary database.</span></span>

> [!NOTE]
> <span data-ttu-id="b8b2d-116">Если база данных-партнер уже создана (например, в результате прекращения предыдущей связи георепликации), выполнение команды завершится сбоем.</span><span class="sxs-lookup"><span data-stu-id="b8b2d-116">If the partner database already exists (for example, as a result of terminating a previous geo-replication relationship) the command fails.</span></span>
> 

1. <span data-ttu-id="b8b2d-117">На [портале Azure](http://portal.azure.com) перейдите к базе данных, для которой нужно настроить георепликацию.</span><span class="sxs-lookup"><span data-stu-id="b8b2d-117">In the [Azure portal](http://portal.azure.com), browse to the database that you want to set up for geo-replication.</span></span>
2. <span data-ttu-id="b8b2d-118">На странице базы данных SQL выберите **Георепликация**, а затем выберите регион для создания базы данных-получателя.</span><span class="sxs-lookup"><span data-stu-id="b8b2d-118">On the SQL database page, select **geo-replication**, and then select the region to create the secondary database.</span></span> <span data-ttu-id="b8b2d-119">Можно выбрать любой регион, кроме региона, в котором размещена база данных-источник, но рекомендуется выбрать [сопряженный регион](../best-practices-availability-paired-regions.md).</span><span class="sxs-lookup"><span data-stu-id="b8b2d-119">You can select any region other than the region hosting the primary database, but we recommend the [paired region](../best-practices-availability-paired-regions.md).</span></span>
   
    ![Настройка георепликации](./media/sql-database-geo-replication-portal/configure-geo-replication.png)
3. <span data-ttu-id="b8b2d-121">Выберите или настройте сервер и ценовую категорию для базы данных-получателя.</span><span class="sxs-lookup"><span data-stu-id="b8b2d-121">Select or configure the server and pricing tier for the secondary database.</span></span>
   
    ![Настройка базы данных-получателя](./media/sql-database-geo-replication-portal/create-secondary.png)
4. <span data-ttu-id="b8b2d-123">По желанию добавьте базу данных-получатель в пул эластичных баз данных.</span><span class="sxs-lookup"><span data-stu-id="b8b2d-123">Optionally, you can add a secondary database to an elastic pool.</span></span> <span data-ttu-id="b8b2d-124">Чтобы создать базу данных-получатель, щелкните **Пул эластичных БД** и выберите пул на целевом сервере.</span><span class="sxs-lookup"><span data-stu-id="b8b2d-124">To create the secondary database in a pool, click **elastic pool** and select a pool on the target server.</span></span> <span data-ttu-id="b8b2d-125">Пул должен быть создан на целевом сервере заранее.</span><span class="sxs-lookup"><span data-stu-id="b8b2d-125">A pool must already exist on the target server.</span></span> <span data-ttu-id="b8b2d-126">Этот рабочий процесс не создает пул.</span><span class="sxs-lookup"><span data-stu-id="b8b2d-126">This workflow does not create a pool.</span></span>
5. <span data-ttu-id="b8b2d-127">Щелкните **Создать** , чтобы добавить базу данных-получатель.</span><span class="sxs-lookup"><span data-stu-id="b8b2d-127">Click **Create** to add the secondary.</span></span>
6. <span data-ttu-id="b8b2d-128">После создания базы данных-получателя начнется процесс заполнения.</span><span class="sxs-lookup"><span data-stu-id="b8b2d-128">The secondary database is created and the seeding process begins.</span></span>
   
    ![Настройка базы данных-получателя](./media/sql-database-geo-replication-portal/seeding0.png)
7. <span data-ttu-id="b8b2d-130">Как только процесс заполнения будет закончен, отобразится состояние базы данных-получателя.</span><span class="sxs-lookup"><span data-stu-id="b8b2d-130">When the seeding process is complete, the secondary database displays its status.</span></span>
   
    ![Заполнение завершено](./media/sql-database-geo-replication-portal/seeding-complete.png)

## <a name="initiate-a-failover"></a><span data-ttu-id="b8b2d-132">Запуск отработки отказа</span><span class="sxs-lookup"><span data-stu-id="b8b2d-132">Initiate a failover</span></span>

<span data-ttu-id="b8b2d-133">Базу данных-получатель можно сделать источником.</span><span class="sxs-lookup"><span data-stu-id="b8b2d-133">The secondary database can be switched to become the primary.</span></span>  

1. <span data-ttu-id="b8b2d-134">На [портале Azure](http://portal.azure.com) перейдите к базе данных-источнику в партнерстве георепликации.</span><span class="sxs-lookup"><span data-stu-id="b8b2d-134">In the [Azure portal](http://portal.azure.com), browse to the primary database in the geo-replication partnership.</span></span>
2. <span data-ttu-id="b8b2d-135">В колонке "База данных SQL" выберите **Все параметры** > **Георепликация**.</span><span class="sxs-lookup"><span data-stu-id="b8b2d-135">On the SQL Database blade, select **All settings** > **geo-replication**.</span></span>
3. <span data-ttu-id="b8b2d-136">В списке **Получатели** выберите базу данных, которая должна стать новым источником, и щелкните **Отработка отказа**.</span><span class="sxs-lookup"><span data-stu-id="b8b2d-136">In the **SECONDARIES** list, select the database you want to become the new primary and click **Failover**.</span></span>
   
    ![Отработка отказа](./media/sql-database-geo-replication-failover-portal/secondaries.png)
4. <span data-ttu-id="b8b2d-138">Выберите **Да** , чтобы запустить отработку отказа.</span><span class="sxs-lookup"><span data-stu-id="b8b2d-138">Click **Yes** to begin the failover.</span></span>

<span data-ttu-id="b8b2d-139">Команда немедленно переключит базу данных-получатель на роль базы данных-источника.</span><span class="sxs-lookup"><span data-stu-id="b8b2d-139">The command immediately switches the secondary database into the primary role.</span></span> 

<span data-ttu-id="b8b2d-140">В течение короткого периода (от 0 до 25 секунд), пока переключаются роли, обе базы данных будут недоступны.</span><span class="sxs-lookup"><span data-stu-id="b8b2d-140">There is a short period during which both databases are unavailable (on the order of 0 to 25 seconds) while the roles are switched.</span></span> <span data-ttu-id="b8b2d-141">Если база данных-источник имеет несколько баз данных-получателей, то команда автоматически перенастроит другие базы данных-получатели для подключения к новой базе данных-источнику.</span><span class="sxs-lookup"><span data-stu-id="b8b2d-141">If the primary database has multiple secondary databases, the command automatically reconfigures the other secondaries to connect to the new primary.</span></span> <span data-ttu-id="b8b2d-142">Обычно вся операция занимает меньше минуты.</span><span class="sxs-lookup"><span data-stu-id="b8b2d-142">The entire operation should take less than a minute to complete under normal circumstances.</span></span> 

> [!NOTE]
> <span data-ttu-id="b8b2d-143">Эта команда предназначена для быстрого восстановления базы данных в случае сбоя.</span><span class="sxs-lookup"><span data-stu-id="b8b2d-143">This command is designed for quick recovery of the database in case of an outage.</span></span> <span data-ttu-id="b8b2d-144">Она активирует отработку отказа без синхронизации данных (принудительная отработка отказа).</span><span class="sxs-lookup"><span data-stu-id="b8b2d-144">It triggers failover without data synchronization (forced failover).</span></span>  <span data-ttu-id="b8b2d-145">Если при отправке команды источник находится в сети и выполняет транзакции, некоторые данные могут быть утеряны.</span><span class="sxs-lookup"><span data-stu-id="b8b2d-145">If the primary is online and committing transactions when the command is issued some data loss may occur.</span></span> 
> 
> 

## <a name="remove-secondary-database"></a><span data-ttu-id="b8b2d-146">Удаление базы данных-получателя</span><span class="sxs-lookup"><span data-stu-id="b8b2d-146">Remove secondary database</span></span>
<span data-ttu-id="b8b2d-147">Данная операция безвозвратно отменяет репликацию в базу данных-получатель и превращает ее в обычную базу данных для чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="b8b2d-147">This operation permanently terminates the replication to the secondary database, and changes the role of the secondary to a regular read-write database.</span></span> <span data-ttu-id="b8b2d-148">Если подключение к базе данных-получателю прервется, команда будет выполнена, но после восстановления связи база данных-получатель не станет доступной для чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="b8b2d-148">If the connectivity to the secondary database is broken, the command succeeds but the secondary does not become read-write until after connectivity is restored.</span></span>  

1. <span data-ttu-id="b8b2d-149">На [портале Azure](http://portal.azure.com) перейдите к базе данных-источнику в партнерстве георепликации.</span><span class="sxs-lookup"><span data-stu-id="b8b2d-149">In the [Azure portal](http://portal.azure.com), browse to the primary database in the geo-replication partnership.</span></span>
2. <span data-ttu-id="b8b2d-150">На странице базы данных SQL выберите **Георепликация**.</span><span class="sxs-lookup"><span data-stu-id="b8b2d-150">On the SQL database page, select **geo-replication**.</span></span>
3. <span data-ttu-id="b8b2d-151">В списке **Получатели** выберите базу данных, которую нужно удалить из партнерства георепликации.</span><span class="sxs-lookup"><span data-stu-id="b8b2d-151">In the **SECONDARIES** list, select the database you want to remove from the geo-replication partnership.</span></span>
4. <span data-ttu-id="b8b2d-152">Щелкните **Остановить репликацию**.</span><span class="sxs-lookup"><span data-stu-id="b8b2d-152">Click **Stop Replication**.</span></span>
   
    ![Удаление базы данных-получателя](./media/sql-database-geo-replication-portal/remove-secondary.png)
5. <span data-ttu-id="b8b2d-154">Откроется окно подтверждения.</span><span class="sxs-lookup"><span data-stu-id="b8b2d-154">A confirmation window opens.</span></span> <span data-ttu-id="b8b2d-155">Нажмите кнопку **Да**, чтобы удалить базу данных из партнерства георепликации</span><span class="sxs-lookup"><span data-stu-id="b8b2d-155">Click **Yes** to remove the database from the geo-replication partnership.</span></span> <span data-ttu-id="b8b2d-156">(и сделать ее доступной для чтения и записи и не используемой в репликации).</span><span class="sxs-lookup"><span data-stu-id="b8b2d-156">(Set it to a read-write database not part of any replication.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="b8b2d-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b8b2d-157">Next steps</span></span>
* <span data-ttu-id="b8b2d-158">Дополнительные сведения об активной георепликации см. в статье [Обзор. Группы отработки отказа и активная георепликация](sql-database-geo-replication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b8b2d-158">To learn more about active geo-replication, see [active geo-replication](sql-database-geo-replication-overview.md).</span></span>
* <span data-ttu-id="b8b2d-159">Сведения об обеспечении непрерывности бизнес-процессов и возможные сценарии описаны в [обзоре непрерывности бизнес-процессов](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="b8b2d-159">For a business continuity overview and scenarios, see [Business continuity overview](sql-database-business-continuity.md).</span></span>

