---
title: "безопасность базы данных SQL Azure для аварийного восстановления aaaConfigure | Документы Microsoft"
description: "В этом разделе объясняется вопросы безопасности для настройки и управления безопасностью после восстановления базы данных или отработки отказа tooa сервер-получатель hello для события сбоя центра обработки данных или иного сбоя"
services: sql-database
documentationcenter: na
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: c7c898c9-69d4-4e16-8b7e-720bbb3353dd
ms.service: sql-database
ms.custom: business continuity
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 10/13/2016
ms.author: sashan
ms.openlocfilehash: c3172568e1b8ad2a53958200aa6cf19b4a9434ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-manage-azure-sql-database-security-for-geo-restore-or-failover"></a><span data-ttu-id="9fac0-103">Настройка безопасности Базы данных SQL Azure и управление ею для геовосстановления или отработки отказа</span><span class="sxs-lookup"><span data-stu-id="9fac0-103">Configure and manage Azure SQL Database security for geo-restore or failover</span></span> 

> [!NOTE]
> <span data-ttu-id="9fac0-104">[Активная георепликация](sql-database-geo-replication-overview.md) теперь доступна для всех баз данных и всех уровней обслуживания.</span><span class="sxs-lookup"><span data-stu-id="9fac0-104">[Active geo-replication](sql-database-geo-replication-overview.md) is now available for all databases in all service tiers.</span></span>
>  

## <a name="overview-of-authentication-requirements-for-disaster-recovery"></a><span data-ttu-id="9fac0-105">Обзор требований к проверке подлинности для аварийного восстановления</span><span class="sxs-lookup"><span data-stu-id="9fac0-105">Overview of authentication requirements for disaster recovery</span></span>
<span data-ttu-id="9fac0-106">В этом разделе описываются требования tooconfigure hello проверки подлинности и управления [активной георепликации](sql-database-geo-replication-overview.md) и hello шагов требуется tooset копирование пользовательского доступа toohello баз данных-получателей.</span><span class="sxs-lookup"><span data-stu-id="9fac0-106">This topic describes hello authentication requirements tooconfigure and control [active geo-replication](sql-database-geo-replication-overview.md) and hello steps required tooset up user access toohello secondary database.</span></span> <span data-ttu-id="9fac0-107">В нем также рассматриваются как включить восстановленной базы данных toohello доступа после использования [геовосстановление](sql-database-recovery-using-backups.md#geo-restore).</span><span class="sxs-lookup"><span data-stu-id="9fac0-107">It also describes how enable access toohello recovered database after using [geo-restore](sql-database-recovery-using-backups.md#geo-restore).</span></span> <span data-ttu-id="9fac0-108">Дополнительные сведения о вариантах восстановления см. в статье [Обзор обеспечения непрерывности бизнес-процессов с помощью базы данных SQL Azure](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="9fac0-108">For more information on recovery options, see [Business Continuity Overview](sql-database-business-continuity.md).</span></span>

## <a name="disaster-recovery-with-contained-users"></a><span data-ttu-id="9fac0-109">Аварийное восстановление с поддержкой автономных пользователей</span><span class="sxs-lookup"><span data-stu-id="9fac0-109">Disaster recovery with contained users</span></span>
<span data-ttu-id="9fac0-110">В отличие от традиционных пользователей, который должен быть сопоставлен toologins в базе данных master hello, автономного пользователя полностью управляется самой базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="9fac0-110">Unlike traditional users, which must be mapped toologins in hello master database, a contained user is managed completely by hello database itself.</span></span> <span data-ttu-id="9fac0-111">Это имеет два преимущества.</span><span class="sxs-lookup"><span data-stu-id="9fac0-111">This has two benefits.</span></span> <span data-ttu-id="9fac0-112">В сценарии аварийного восстановления hello hello пользователи могут продолжать tooconnect toohello новой основной базы данных или восстановить с использованием геовосстановления без дополнительной настройки, поскольку hello базы данных управляет hello пользователями базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="9fac0-112">In hello disaster recovery scenario, hello users can continue tooconnect toohello new primary database or hello database recovered using geo-restore without any additional configuration, because hello database manages hello users.</span></span> <span data-ttu-id="9fac0-113">Кроме этого, с точки зрения входа такая конфигурация потенциально может иметь преимущества масштабируемости и производительности.</span><span class="sxs-lookup"><span data-stu-id="9fac0-113">There are also potential scalability and performance benefits from this configuration from a login perspective.</span></span> <span data-ttu-id="9fac0-114">Дополнительные сведения см. в статье [Пользователи автономной базы данных — создание переносимой базы данных](https://msdn.microsoft.com/library/ff929188.aspx).</span><span class="sxs-lookup"><span data-stu-id="9fac0-114">For more information, see [Contained Database Users - Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx).</span></span> 

<span data-ttu-id="9fac0-115">Основной недостаток Hello, что управление hello процесса аварийного восстановления в масштабе более сложной задачей.</span><span class="sxs-lookup"><span data-stu-id="9fac0-115">hello main trade-off is that managing hello disaster recovery process at scale is more challenging.</span></span> <span data-ttu-id="9fac0-116">При наличии нескольких баз данных, используйте приветствия содержится имя пользователя, обслуживание hello учетные данные с помощью пользователей в нескольких базах данных могут поставить под сомнение hello преимущества автономных пользователей.</span><span class="sxs-lookup"><span data-stu-id="9fac0-116">When you have multiple databases that use hello same login, maintaining hello credentials using contained users in multiple databases may negate hello benefits of contained users.</span></span> <span data-ttu-id="9fac0-117">Например политику смены паролей hello требует выполняться единообразно в нескольких базах данных, а не как hello при смене пароля для имени входа hello один раз в базе данных master hello.</span><span class="sxs-lookup"><span data-stu-id="9fac0-117">For example, hello password rotation policy requires that changes be made consistently in multiple databases rather than changing hello password for hello login once in hello master database.</span></span> <span data-ttu-id="9fac0-118">По этой причине, если имеется несколько баз данных, используйте hello же имя пользователя и пароль, не рекомендуется использование автономных пользователей.</span><span class="sxs-lookup"><span data-stu-id="9fac0-118">For this reason, if you have multiple databases that use hello same user name and password, using contained users is not recommended.</span></span> 

## <a name="how-tooconfigure-logins-and-users"></a><span data-ttu-id="9fac0-119">Как tooconfigure имена входа и пользователи</span><span class="sxs-lookup"><span data-stu-id="9fac0-119">How tooconfigure logins and users</span></span>
<span data-ttu-id="9fac0-120">При использовании имен входа и пользователей (а не автономных пользователей), необходимо выполнить дополнительные шаги tooinsure hello, этот же входа существуют в базе данных master hello.</span><span class="sxs-lookup"><span data-stu-id="9fac0-120">If you are using logins and users (rather than contained users), you must take extra steps tooinsure that hello same logins exist in hello master database.</span></span> <span data-ttu-id="9fac0-121">Hello следующих разделах рассматриваются вопросы участвующих и дополнительные действия hello.</span><span class="sxs-lookup"><span data-stu-id="9fac0-121">hello following sections outline hello steps involved and additional considerations.</span></span>

### <a name="set-up-user-access-tooa-secondary-or-recovered-database"></a><span data-ttu-id="9fac0-122">Настройка пользователя tooa получателей или восстанавливать базы данных access</span><span class="sxs-lookup"><span data-stu-id="9fac0-122">Set up user access tooa secondary or recovered database</span></span>
<span data-ttu-id="9fac0-123">Для hello баз данных-получателей toobe можно использовать как только для чтения базы данных-получателя и tooensure права доступа toohello новой первичной базы данных или hello базы данных восстановлен с помощью географическое восстановление hello главной базы данных hello целевого сервера должен иметь hello соответствующую конфигурацию безопасности на месте до восстановления hello.</span><span class="sxs-lookup"><span data-stu-id="9fac0-123">In order for hello secondary database toobe usable as a read-only secondary database, and tooensure proper access toohello new primary database or hello database recovered using geo-restore, hello master database of hello target server must have hello appropriate security configuration in place before hello recovery.</span></span>

<span data-ttu-id="9fac0-124">Далее в этом разделе описываются Hello конкретные разрешения для каждого шага.</span><span class="sxs-lookup"><span data-stu-id="9fac0-124">hello specific permissions for each step are described later in this topic.</span></span>

<span data-ttu-id="9fac0-125">Подготовка tooa доступ пользователя получателя географической репликации должно выполняться в рамках настройки георепликации.</span><span class="sxs-lookup"><span data-stu-id="9fac0-125">Preparing user access tooa geo-replication secondary should be performed as part configuring geo-replication.</span></span> <span data-ttu-id="9fac0-126">Подготовку доступа пользователей базы данных восстановлена geo toohello должна выполняться в любое время, когда hello исходный сервер подключен к сети (например, в составе детализации hello аварийного восстановления).</span><span class="sxs-lookup"><span data-stu-id="9fac0-126">Preparing user access toohello geo-restored databases should be performed at any time when hello original server is online (e.g. as part of hello DR drill).</span></span>

> [!NOTE]
> <span data-ttu-id="9fac0-127">Если не over или географическое восстановление сервера tooa, у которого нет имен входа, правильно настроен, tooit доступ будет toohello ограниченной учетной записи администратора сервера.</span><span class="sxs-lookup"><span data-stu-id="9fac0-127">If you fail over or geo-restore tooa server that does not have properly configured logins, access tooit will be limited toohello server admin account.</span></span>
> 
> 

<span data-ttu-id="9fac0-128">Настройка имен входа на целевом сервере hello включает следующие три действия:</span><span class="sxs-lookup"><span data-stu-id="9fac0-128">Setting up logins on hello target server involves three steps outlined below:</span></span>

#### <a name="1-determine-logins-with-access-toohello-primary-database"></a><span data-ttu-id="9fac0-129">1. Определение входных данных для доступа к toohello базы данных-источника:</span><span class="sxs-lookup"><span data-stu-id="9fac0-129">1. Determine logins with access toohello primary database:</span></span>
<span data-ttu-id="9fac0-130">Первым шагом Hello hello процесса является имя входа, которое необходимо копировать на целевом сервере hello toodetermine.</span><span class="sxs-lookup"><span data-stu-id="9fac0-130">hello first step of hello process is toodetermine which logins must be duplicated on hello target server.</span></span> <span data-ttu-id="9fac0-131">Это можно сделать с помощью двух инструкций SELECT, в hello логической базе данных master на исходном сервере hello и в hello основной базы данных.</span><span class="sxs-lookup"><span data-stu-id="9fac0-131">This is accomplished with a pair of SELECT statements, one in hello logical master database on hello source server and one in hello primary database itself.</span></span>

<span data-ttu-id="9fac0-132">Здравствуйте, только администратор сервера или членом hello **LoginManager** серверной роли можно определить приветствия имен входа на исходном сервере hello с hello, следующем за инструкцией SELECT.</span><span class="sxs-lookup"><span data-stu-id="9fac0-132">Only hello server admin or a member of hello **LoginManager** server role can determine hello logins on hello source server with hello following SELECT statement.</span></span> 

    SELECT [name], [sid] 
    FROM [sys].[sql_logins] 
    WHERE [type_desc] = 'SQL_Login'

<span data-ttu-id="9fac0-133">Только членом роли базы данных db_owner hello, hello пользователь dbo или администратор сервера может определять всех участников пользователя hello базы данных в базе данных-источнике hello.</span><span class="sxs-lookup"><span data-stu-id="9fac0-133">Only a member of hello db_owner database role, hello dbo user, or server admin, can determine all of hello database user principals in hello primary database.</span></span>

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

#### <a name="2-find-hello-sid-for-hello-logins-identified-in-step-1"></a><span data-ttu-id="9fac0-134">2. Найти hello SID для имен входа hello, определенных на шаге 1:</span><span class="sxs-lookup"><span data-stu-id="9fac0-134">2. Find hello SID for hello logins identified in step 1:</span></span>
<span data-ttu-id="9fac0-135">Сравнивая выходные данные hello hello запросов из предыдущего раздела hello и сопоставления hello идентификаторы безопасности, можно сопоставить пользователя toodatabase входа сервера hello.</span><span class="sxs-lookup"><span data-stu-id="9fac0-135">By comparing hello output of hello queries from hello previous section and matching hello SIDs, you can map hello server login toodatabase user.</span></span> <span data-ttu-id="9fac0-136">Имена входа, имеющие пользователя базы данных с соответствующими SID иметь базы данных toothat доступ пользователей в качестве участника-пользователя.</span><span class="sxs-lookup"><span data-stu-id="9fac0-136">Logins that have a database user with a matching SID have user access toothat database as that database user principal.</span></span> 

<span data-ttu-id="9fac0-137">Hello следующий запрос может быть используется toosee всех участников-пользователей hello и их SID в базе данных.</span><span class="sxs-lookup"><span data-stu-id="9fac0-137">hello following query can be used toosee all of hello user principals and their SIDs in a database.</span></span> <span data-ttu-id="9fac0-138">Этот запрос может выполнять только члены hello db_owner базы данных роли или администратор сервера.</span><span class="sxs-lookup"><span data-stu-id="9fac0-138">Only a member of hello db_owner database role or server admin can run this query.</span></span>

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

> [!NOTE]
> <span data-ttu-id="9fac0-139">Hello **INFORMATION_SCHEMA** и **sys** пользователи имеют *NULL* идентификаторы безопасности и hello **гостевой** SID является **0x00**.</span><span class="sxs-lookup"><span data-stu-id="9fac0-139">hello **INFORMATION_SCHEMA** and **sys** users have *NULL* SIDs, and hello **guest** SID is **0x00**.</span></span> <span data-ttu-id="9fac0-140">Hello **dbo** SID может начинаться с *0x01060000000001648000000000048454*, если создатель базы данных hello Здравствуйте, администратор сервера вместо членом **DbManager**.</span><span class="sxs-lookup"><span data-stu-id="9fac0-140">hello **dbo** SID may start with *0x01060000000001648000000000048454*, if hello database creator was hello server admin instead of a member of **DbManager**.</span></span>
> 
> 

#### <a name="3-create-hello-logins-on-hello-target-server"></a><span data-ttu-id="9fac0-141">3. Создайте имена входа hello на целевом сервере hello:</span><span class="sxs-lookup"><span data-stu-id="9fac0-141">3. Create hello logins on hello target server:</span></span>
<span data-ttu-id="9fac0-142">Hello последний шаг toogo toohello целевой сервер или серверы, а создать имена входа hello с hello соответствующие идентификаторы безопасности.</span><span class="sxs-lookup"><span data-stu-id="9fac0-142">hello last step is toogo toohello target server, or servers, and generate hello logins with hello appropriate SIDs.</span></span> <span data-ttu-id="9fac0-143">Hello базовый синтаксис выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="9fac0-143">hello basic syntax is as follows.</span></span>

    CREATE LOGIN [<login name>]
    WITH PASSWORD = <login password>,
    SID = <desired login SID>

> [!NOTE]
> <span data-ttu-id="9fac0-144">Если требуется toohello доступ пользователя toogrant получателя, но не toohello первичной, это можно сделать путем изменения hello имя входа пользователя на сервере-источнике hello, используя синтаксис hello.</span><span class="sxs-lookup"><span data-stu-id="9fac0-144">If you want toogrant user access toohello secondary, but not toohello primary, you can do that by altering hello user login on hello primary server by using hello following syntax.</span></span>
> 
> <span data-ttu-id="9fac0-145">ALTER LOGIN <login name> DISABLE</span><span class="sxs-lookup"><span data-stu-id="9fac0-145">ALTER LOGIN <login name> DISABLE</span></span>
> 
> <span data-ttu-id="9fac0-146">DISABLE не изменяет пароль hello, поэтому можно всегда включить его при необходимости.</span><span class="sxs-lookup"><span data-stu-id="9fac0-146">DISABLE doesn’t change hello password, so you can always enable it if needed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="9fac0-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9fac0-147">Next steps</span></span>
* <span data-ttu-id="9fac0-148">Дополнительные сведения об управлении доступом к базе данных и именами для входа см. в статье [Проверка подлинности и авторизация в базе данных SQL: предоставление доступа](sql-database-manage-logins.md).</span><span class="sxs-lookup"><span data-stu-id="9fac0-148">For more information on managing database access and logins, see [SQL Database security: Manage database access and login security](sql-database-manage-logins.md).</span></span>
* <span data-ttu-id="9fac0-149">Дополнительные сведения о пользователях автономной базы данных см. в статье [Пользователи автономной базы данных — создание переносимой базы данных](https://msdn.microsoft.com/library/ff929188.aspx).</span><span class="sxs-lookup"><span data-stu-id="9fac0-149">For more information on contained database users, see [Contained Database Users - Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx).</span></span>
* <span data-ttu-id="9fac0-150">Сведения об использовании и настройке активной георепликации см. в статье [Обзор. Группы отработки отказа и активная георепликация](sql-database-geo-replication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9fac0-150">For information about using and configuring active geo-replication, see [active geo-replication](sql-database-geo-replication-overview.md)</span></span>
* <span data-ttu-id="9fac0-151">Сведения об использовании геовосстановления см. в [этом разделе](sql-database-recovery-using-backups.md#geo-restore).</span><span class="sxs-lookup"><span data-stu-id="9fac0-151">For information about using geo-restore, see [geo-restore](sql-database-recovery-using-backups.md#geo-restore)</span></span>

