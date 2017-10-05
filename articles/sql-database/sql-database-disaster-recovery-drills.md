---
title: "Отработки аварийного восстановления базы данных SQL | Документация Майкрософт"
description: "Руководство и рекомендации по отработке аварийного восстановления в базе данных SQL Azure, что позволяет обеспечить устойчивость критически важных бизнес-приложений против сбоев и простоев."
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: b44a269c-fe2a-404f-b013-290030860bd1
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 07/31/2016
ms.author: sashan
ms.openlocfilehash: 1b1d65a41a794a566287dcffe3581ac58e2a965f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="performing-disaster-recovery-drill"></a><span data-ttu-id="5f1fe-103">Отработка аварийного восстановления</span><span class="sxs-lookup"><span data-stu-id="5f1fe-103">Performing Disaster Recovery Drill</span></span>
<span data-ttu-id="5f1fe-104">Рекомендуется периодически проверять готовность приложений к рабочему процессу восстановления.</span><span class="sxs-lookup"><span data-stu-id="5f1fe-104">It is recommended that validation of application readiness for recovery workflow is performed periodically.</span></span> <span data-ttu-id="5f1fe-105">Проверка поведения приложения и возможных последствий потери данных и нарушений работы, которая включает отработку отказа, предусмотрена стандартами разработки.</span><span class="sxs-lookup"><span data-stu-id="5f1fe-105">Verifying the application behavior and implications of data loss and/or the disruption that failover involves is a good engineering practice.</span></span> <span data-ttu-id="5f1fe-106">Эта процедура также является обязательной для большинства отраслевых стандартов в рамках сертификации непрерывности бизнес-процессов.</span><span class="sxs-lookup"><span data-stu-id="5f1fe-106">It is also a requirement by most industry standards as part of business continuity certification.</span></span>

<span data-ttu-id="5f1fe-107">Этапы отработки аварийного восстановления:</span><span class="sxs-lookup"><span data-stu-id="5f1fe-107">Performing a disaster recovery drill consists of:</span></span>

* <span data-ttu-id="5f1fe-108">моделирование сбоя уровня данных;</span><span class="sxs-lookup"><span data-stu-id="5f1fe-108">Simulating data tier outage</span></span>
* <span data-ttu-id="5f1fe-109">восстановление;</span><span class="sxs-lookup"><span data-stu-id="5f1fe-109">Recovering</span></span>
* <span data-ttu-id="5f1fe-110">проверка целостности приложения после восстановления.</span><span class="sxs-lookup"><span data-stu-id="5f1fe-110">Validate application integrity post recovery</span></span>

<span data-ttu-id="5f1fe-111">Рабочий процесс отработки зависит от того, как вы [спроектировали приложение для обеспечения непрерывности бизнес-процессов](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="5f1fe-111">Depending on how you [designed your application for business continuity](sql-database-business-continuity.md), the workflow to execute the drill can vary.</span></span> <span data-ttu-id="5f1fe-112">Ниже приведены рекомендации по отработке аварийного восстановления с использованием базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="5f1fe-112">Below we describe the best practices conducting a disaster recovery drill in the context of Azure SQL Database.</span></span>

## <a name="geo-restore"></a><span data-ttu-id="5f1fe-113">Геовосстановление</span><span class="sxs-lookup"><span data-stu-id="5f1fe-113">Geo-restore</span></span>
<span data-ttu-id="5f1fe-114">Чтобы избежать потери данных при проведении отработки аварийного восстановления, рекомендуется выполнять отработку в тестовой среде. Для этого создайте копию рабочей среды и используйте ее для проверки рабочего процесса отработки отказа приложения.</span><span class="sxs-lookup"><span data-stu-id="5f1fe-114">To prevent the potential data loss when conducting a disaster recovery drill, we recommend performing the drill using a test environment by creating a copy of the production environment and using it to verify the application’s failover workflow.</span></span>

#### <a name="outage-simulation"></a><span data-ttu-id="5f1fe-115">Моделирование сбоя</span><span class="sxs-lookup"><span data-stu-id="5f1fe-115">Outage simulation</span></span>
<span data-ttu-id="5f1fe-116">Чтобы сымитировать сбой, можно удалить или переименовать базу данных-источник.</span><span class="sxs-lookup"><span data-stu-id="5f1fe-116">To simulate the outage, you can delete or rename the source database.</span></span> <span data-ttu-id="5f1fe-117">Это вызовет сбой подключения приложения.</span><span class="sxs-lookup"><span data-stu-id="5f1fe-117">This causes application connectivity failures.</span></span>

#### <a name="recovery"></a><span data-ttu-id="5f1fe-118">Восстановление</span><span class="sxs-lookup"><span data-stu-id="5f1fe-118">Recovery</span></span>
* <span data-ttu-id="5f1fe-119">Выполните геовосстановление базы данных на другой сервер, следуя инструкциям [здесь](sql-database-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="5f1fe-119">Perform the geo-restore of the database into a different server as described [here](sql-database-disaster-recovery.md).</span></span>
* <span data-ttu-id="5f1fe-120">Измените конфигурацию приложения, чтобы подключиться к восстановленной базе данных, и завершите восстановление, следуя инструкциям в статье [Восстановление базы данных SQL Azure или переход на базу данных-получатель при отказе](sql-database-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="5f1fe-120">Change the application configuration to connect to the recovered database and follow the [Configure a database after recovery](sql-database-disaster-recovery.md) guide to complete the recovery.</span></span>

#### <a name="validation"></a><span data-ttu-id="5f1fe-121">Проверка</span><span class="sxs-lookup"><span data-stu-id="5f1fe-121">Validation</span></span>
* <span data-ttu-id="5f1fe-122">Выполните отработку, проверив целостность приложения после восстановления (в том числе строки подключения, учетные данные, тестирование основных функций или другие проверки стандартной процедуры утверждения приложений).</span><span class="sxs-lookup"><span data-stu-id="5f1fe-122">Complete the drill by verifying the application integrity post recovery (including connection strings, logins, basic functionality testing or other validations part of standard application signoffs procedures).</span></span>

## <a name="geo-replication"></a><span data-ttu-id="5f1fe-123">Георепликация</span><span class="sxs-lookup"><span data-stu-id="5f1fe-123">Geo-replication</span></span>
<span data-ttu-id="5f1fe-124">Для базы данных, защищенной с помощью георепликации, в тренировочном упражнении предусмотрена плановая отработка отказа на базу данных-получатель.</span><span class="sxs-lookup"><span data-stu-id="5f1fe-124">For a database that is protected using geo-replication the drill exercise involves planned failover to the secondary database.</span></span> <span data-ttu-id="5f1fe-125">Плановая отработка отказа гарантирует, что база данных-источник и база данных-получатель останутся синхронизированы после переключения ролей.</span><span class="sxs-lookup"><span data-stu-id="5f1fe-125">The planned failover ensures that the primary and the secondary databases remain in sync when the roles are switched.</span></span> <span data-ttu-id="5f1fe-126">В отличие от незапланированной отработки отказа, эта операция не приводит к потере данных, поэтому отработку можно выполнить в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="5f1fe-126">Unlike the unplanned failover, this operation does not result in data loss, so the drill can be performed in the production environment.</span></span>

#### <a name="outage-simulation"></a><span data-ttu-id="5f1fe-127">Моделирование сбоя</span><span class="sxs-lookup"><span data-stu-id="5f1fe-127">Outage simulation</span></span>
<span data-ttu-id="5f1fe-128">Чтобы сымитировать сбой, можно отключить веб-приложение или виртуальную машину, подключенные к базе данных.</span><span class="sxs-lookup"><span data-stu-id="5f1fe-128">To simulate the outage, you can disable the web application or virtual machine connected to the database.</span></span> <span data-ttu-id="5f1fe-129">Это приведет к сбоям подключения веб-клиентов.</span><span class="sxs-lookup"><span data-stu-id="5f1fe-129">This results in the connectivity failures for the web clients.</span></span>

#### <a name="recovery"></a><span data-ttu-id="5f1fe-130">Восстановление</span><span class="sxs-lookup"><span data-stu-id="5f1fe-130">Recovery</span></span>
* <span data-ttu-id="5f1fe-131">Убедитесь, что конфигурация приложения в регионе аварийного восстановления указывает на бывшую базу данных-получатель, которая станет полностью доступной новой базой данных-источником.</span><span class="sxs-lookup"><span data-stu-id="5f1fe-131">Make sure the application configuration in the DR region points to the former secondary which becomes the fully accessible new primary.</span></span>
* <span data-ttu-id="5f1fe-132">Выполните [плановую отработку отказа](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) , чтобы база данных-получатель стала новой базой данных-источником.</span><span class="sxs-lookup"><span data-stu-id="5f1fe-132">Perform [planned failover](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) to make the secondary database a new primary</span></span>
* <span data-ttu-id="5f1fe-133">Следуйте инструкциям в руководстве [по настройке базы данных после восстановления](sql-database-disaster-recovery.md) , чтобы завершить восстановление.</span><span class="sxs-lookup"><span data-stu-id="5f1fe-133">Follow the [Configure a database after recovery](sql-database-disaster-recovery.md) guide to complete the recovery.</span></span>

#### <a name="validation"></a><span data-ttu-id="5f1fe-134">Проверка</span><span class="sxs-lookup"><span data-stu-id="5f1fe-134">Validation</span></span>
* <span data-ttu-id="5f1fe-135">Выполните отработку, проверив целостность приложения после восстановления (в том числе строки подключения, учетные данные, тестирование основных функций или другие проверки стандартной процедуры утверждения приложений).</span><span class="sxs-lookup"><span data-stu-id="5f1fe-135">Complete the drill by verifying the application integrity post recovery (including connection strings, logins, basic functionality testing or other validations part of standard application signoffs procedures).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5f1fe-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5f1fe-136">Next steps</span></span>
* <span data-ttu-id="5f1fe-137">Чтобы изучить сценарии обеспечения непрерывности бизнес-процессов, ознакомьтесь со [сценариями обеспечения непрерывности](sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="5f1fe-137">To learn about business continuity scenarios, see [Continuity scenarios](sql-database-business-continuity.md)</span></span>
* <span data-ttu-id="5f1fe-138">Чтобы узнать об автоматически создаваемых резервных копиях базы данных SQL Azure, ознакомьтесь с разделом [Общие сведения об автоматическом резервном копировании базы данных SQL](sql-database-automated-backups.md)</span><span class="sxs-lookup"><span data-stu-id="5f1fe-138">To learn about Azure SQL Database automated backups, see [SQL Database automated backups](sql-database-automated-backups.md)</span></span>
* <span data-ttu-id="5f1fe-139">Чтобы узнать об использовании создаваемых автоматически резервных копий для восстановления, ознакомьтесь с [восстановлением базы данных из резервных копий, инициируемых службой](sql-database-recovery-using-backups.md)</span><span class="sxs-lookup"><span data-stu-id="5f1fe-139">To learn about using automated backups for recovery, see [restore a database from the service-initiated backups](sql-database-recovery-using-backups.md)</span></span>
* <span data-ttu-id="5f1fe-140">Чтобы узнать о более быстрых вариантах восстановления, ознакомьтесь со сведениями об [активной георепликации](sql-database-geo-replication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5f1fe-140">To learn about faster recovery options, see [active geo-replication](sql-database-geo-replication-overview.md)</span></span>  
