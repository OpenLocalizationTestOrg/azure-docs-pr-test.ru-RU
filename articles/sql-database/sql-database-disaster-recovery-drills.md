---
title: "aaaSQL аварийного восстановления базы данных | Документы Microsoft"
description: "Дополнительные сведения, советы и рекомендации по использованию базы данных SQL Azure tooperform аварийного восстановления Детализирует toohelp keep устойчивым toofailures критически важных приложений и простоям."
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
ms.openlocfilehash: bf17857a19fdebddf0d4f55e4db3a1b33efb4e8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="performing-disaster-recovery-drill"></a><span data-ttu-id="6d9de-103">Отработка аварийного восстановления</span><span class="sxs-lookup"><span data-stu-id="6d9de-103">Performing Disaster Recovery Drill</span></span>
<span data-ttu-id="6d9de-104">Рекомендуется периодически проверять готовность приложений к рабочему процессу восстановления.</span><span class="sxs-lookup"><span data-stu-id="6d9de-104">It is recommended that validation of application readiness for recovery workflow is performed periodically.</span></span> <span data-ttu-id="6d9de-105">Проверка поведения приложения hello и последствия потери или hello нарушения данных, переход на другой ресурс включает в себя — хороший способ проектирования.</span><span class="sxs-lookup"><span data-stu-id="6d9de-105">Verifying hello application behavior and implications of data loss and/or hello disruption that failover involves is a good engineering practice.</span></span> <span data-ttu-id="6d9de-106">Эта процедура также является обязательной для большинства отраслевых стандартов в рамках сертификации непрерывности бизнес-процессов.</span><span class="sxs-lookup"><span data-stu-id="6d9de-106">It is also a requirement by most industry standards as part of business continuity certification.</span></span>

<span data-ttu-id="6d9de-107">Этапы отработки аварийного восстановления:</span><span class="sxs-lookup"><span data-stu-id="6d9de-107">Performing a disaster recovery drill consists of:</span></span>

* <span data-ttu-id="6d9de-108">моделирование сбоя уровня данных;</span><span class="sxs-lookup"><span data-stu-id="6d9de-108">Simulating data tier outage</span></span>
* <span data-ttu-id="6d9de-109">восстановление;</span><span class="sxs-lookup"><span data-stu-id="6d9de-109">Recovering</span></span>
* <span data-ttu-id="6d9de-110">проверка целостности приложения после восстановления.</span><span class="sxs-lookup"><span data-stu-id="6d9de-110">Validate application integrity post recovery</span></span>

<span data-ttu-id="6d9de-111">В зависимости от того, как вы [разработанные приложения для обеспечения непрерывности бизнеса](sql-database-business-continuity.md), tooexecute hello hello рабочий процесс детализации могут различаться.</span><span class="sxs-lookup"><span data-stu-id="6d9de-111">Depending on how you [designed your application for business continuity](sql-database-business-continuity.md), hello workflow tooexecute hello drill can vary.</span></span> <span data-ttu-id="6d9de-112">Ниже описано hello рекомендации штатное аварийного восстановления в контексте hello базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="6d9de-112">Below we describe hello best practices conducting a disaster recovery drill in hello context of Azure SQL Database.</span></span>

## <a name="geo-restore"></a><span data-ttu-id="6d9de-113">Геовосстановление</span><span class="sxs-lookup"><span data-stu-id="6d9de-113">Geo-restore</span></span>
<span data-ttu-id="6d9de-114">tooprevent hello возможной потери данных при проведении аварийного восстановления, рекомендуется выполнять в среде тестирования, создав копию hello рабочей среды и с его помощью детализации hello рабочий процесс приложения hello tooverify отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="6d9de-114">tooprevent hello potential data loss when conducting a disaster recovery drill, we recommend performing hello drill using a test environment by creating a copy of hello production environment and using it tooverify hello application’s failover workflow.</span></span>

#### <a name="outage-simulation"></a><span data-ttu-id="6d9de-115">Моделирование сбоя</span><span class="sxs-lookup"><span data-stu-id="6d9de-115">Outage simulation</span></span>
<span data-ttu-id="6d9de-116">toosimulate Здравствуйте сбоя, можно удалить или переименовать hello базы данных-источника.</span><span class="sxs-lookup"><span data-stu-id="6d9de-116">toosimulate hello outage, you can delete or rename hello source database.</span></span> <span data-ttu-id="6d9de-117">Это вызовет сбой подключения приложения.</span><span class="sxs-lookup"><span data-stu-id="6d9de-117">This causes application connectivity failures.</span></span>

#### <a name="recovery"></a><span data-ttu-id="6d9de-118">Восстановление</span><span class="sxs-lookup"><span data-stu-id="6d9de-118">Recovery</span></span>
* <span data-ttu-id="6d9de-119">Выполнить геовосстановление hello hello базы данных на другой сервер, как описано [здесь](sql-database-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="6d9de-119">Perform hello geo-restore of hello database into a different server as described [here](sql-database-disaster-recovery.md).</span></span>
* <span data-ttu-id="6d9de-120">Изменение hello приложения конфигурации tooconnect toohello восстановленной базы данных и следовать hello [настроить базу данных после восстановления](sql-database-disaster-recovery.md) руководство toocomplete hello восстановления.</span><span class="sxs-lookup"><span data-stu-id="6d9de-120">Change hello application configuration tooconnect toohello recovered database and follow hello [Configure a database after recovery](sql-database-disaster-recovery.md) guide toocomplete hello recovery.</span></span>

#### <a name="validation"></a><span data-ttu-id="6d9de-121">Проверка</span><span class="sxs-lookup"><span data-stu-id="6d9de-121">Validation</span></span>
* <span data-ttu-id="6d9de-122">Полный hello drill путем проверки hello целостность приложения post восстановления (включая строки подключения, имена входа, основные функциональные возможности тестирования или другой проверки части процедуры signoffs стандартного приложения).</span><span class="sxs-lookup"><span data-stu-id="6d9de-122">Complete hello drill by verifying hello application integrity post recovery (including connection strings, logins, basic functionality testing or other validations part of standard application signoffs procedures).</span></span>

## <a name="geo-replication"></a><span data-ttu-id="6d9de-123">Георепликация</span><span class="sxs-lookup"><span data-stu-id="6d9de-123">Geo-replication</span></span>
<span data-ttu-id="6d9de-124">Для базы данных, защищенной с помощью детализации hello географической репликации Упражнение подразумевает плановой отработки отказа toohello баз данных-получателей.</span><span class="sxs-lookup"><span data-stu-id="6d9de-124">For a database that is protected using geo-replication hello drill exercise involves planned failover toohello secondary database.</span></span> <span data-ttu-id="6d9de-125">Hello плановой отработки отказа гарантирует, что основной hello и баз данных-получателей hello останутся синхронизации после переключения ролей hello.</span><span class="sxs-lookup"><span data-stu-id="6d9de-125">hello planned failover ensures that hello primary and hello secondary databases remain in sync when hello roles are switched.</span></span> <span data-ttu-id="6d9de-126">В отличие от Здравствуйте внеплановой отработки отказа, эта операция приводит к потере данных, поэтому hello детализации могут быть выполнены в рабочей среде hello.</span><span class="sxs-lookup"><span data-stu-id="6d9de-126">Unlike hello unplanned failover, this operation does not result in data loss, so hello drill can be performed in hello production environment.</span></span>

#### <a name="outage-simulation"></a><span data-ttu-id="6d9de-127">Моделирование сбоя</span><span class="sxs-lookup"><span data-stu-id="6d9de-127">Outage simulation</span></span>
<span data-ttu-id="6d9de-128">toosimulate hello сбоя, можно отключить hello веб-приложения или базы данных виртуальной машиной, подключенной toohello.</span><span class="sxs-lookup"><span data-stu-id="6d9de-128">toosimulate hello outage, you can disable hello web application or virtual machine connected toohello database.</span></span> <span data-ttu-id="6d9de-129">В результате сбоев подключения к hello для hello веб-клиентов.</span><span class="sxs-lookup"><span data-stu-id="6d9de-129">This results in hello connectivity failures for hello web clients.</span></span>

#### <a name="recovery"></a><span data-ttu-id="6d9de-130">Восстановление</span><span class="sxs-lookup"><span data-stu-id="6d9de-130">Recovery</span></span>
* <span data-ttu-id="6d9de-131">Убедиться, что конфигурация приложения hello становились hello аварийного восстановления области точек toohello бывшая вторичная становящейся hello полностью доступны новом сервере-источнике.</span><span class="sxs-lookup"><span data-stu-id="6d9de-131">Make sure hello application configuration in hello DR region points toohello former secondary which becomes hello fully accessible new primary.</span></span>
* <span data-ttu-id="6d9de-132">Выполнить [Плановая отработка отказа](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) новой основной базу данных-получателя hello toomake</span><span class="sxs-lookup"><span data-stu-id="6d9de-132">Perform [planned failover](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) toomake hello secondary database a new primary</span></span>
* <span data-ttu-id="6d9de-133">Выполните hello [настроить базу данных после восстановления](sql-database-disaster-recovery.md) руководство toocomplete hello восстановления.</span><span class="sxs-lookup"><span data-stu-id="6d9de-133">Follow hello [Configure a database after recovery](sql-database-disaster-recovery.md) guide toocomplete hello recovery.</span></span>

#### <a name="validation"></a><span data-ttu-id="6d9de-134">Проверка</span><span class="sxs-lookup"><span data-stu-id="6d9de-134">Validation</span></span>
* <span data-ttu-id="6d9de-135">Полный hello drill путем проверки hello целостность приложения post восстановления (включая строки подключения, имена входа, основные функциональные возможности тестирования или другой проверки части процедуры signoffs стандартного приложения).</span><span class="sxs-lookup"><span data-stu-id="6d9de-135">Complete hello drill by verifying hello application integrity post recovery (including connection strings, logins, basic functionality testing or other validations part of standard application signoffs procedures).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d9de-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6d9de-136">Next steps</span></span>
* <span data-ttu-id="6d9de-137">toolearn о сценариев обеспечения непрерывности бизнеса, в разделе [сценариев непрерывности](sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="6d9de-137">toolearn about business continuity scenarios, see [Continuity scenarios](sql-database-business-continuity.md)</span></span>
* <span data-ttu-id="6d9de-138">toolearn о резервных копиях автоматических базы данных SQL Azure, в разделе [базы данных SQL автоматическое резервное копирование](sql-database-automated-backups.md)</span><span class="sxs-lookup"><span data-stu-id="6d9de-138">toolearn about Azure SQL Database automated backups, see [SQL Database automated backups](sql-database-automated-backups.md)</span></span>
* <span data-ttu-id="6d9de-139">toolearn об использовании автоматического создания резервных копий для восстановления, в разделе [восстановление базы данных из резервных копий, инициируемых службой hello](sql-database-recovery-using-backups.md)</span><span class="sxs-lookup"><span data-stu-id="6d9de-139">toolearn about using automated backups for recovery, see [restore a database from hello service-initiated backups](sql-database-recovery-using-backups.md)</span></span>
* <span data-ttu-id="6d9de-140">toolearn о быстрее параметры восстановления, в разделе [активной георепликации](sql-database-geo-replication-overview.md)</span><span class="sxs-lookup"><span data-stu-id="6d9de-140">toolearn about faster recovery options, see [active geo-replication](sql-database-geo-replication-overview.md)</span></span>  
