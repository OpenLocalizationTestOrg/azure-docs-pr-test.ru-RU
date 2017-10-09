---
title: "хранилище данных Azure — локальные и географически избыточная aaaRestore | Документы Microsoft"
description: "Общие сведения о параметрах восстановления hello базы данных для восстановления базы данных в хранилище данных SQL Azure."
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: 3e01c65c-6708-4fd7-82f5-4e1b5f61d304
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: a96b898372b29d420e1416ca93a172ff8af47fc7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-restore"></a><span data-ttu-id="571f2-103">Восстановление хранилища данных SQL</span><span class="sxs-lookup"><span data-stu-id="571f2-103">SQL Data Warehouse restore</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="571f2-104">[Обзор][Overview]</span><span class="sxs-lookup"><span data-stu-id="571f2-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="571f2-105">[Портал][Portal]</span><span class="sxs-lookup"><span data-stu-id="571f2-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="571f2-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="571f2-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="571f2-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="571f2-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="571f2-108">Хранилище данных SQL предоставляет функции локального восстановления и геовосстановления, входящие в набор средств аварийного восстановления.</span><span class="sxs-lookup"><span data-stu-id="571f2-108">SQL Data Warehouse offers both local and geographical restores as part of its data warehouse disaster recovery capabilities.</span></span> <span data-ttu-id="571f2-109">С помощью данных хранилища резервных копий toorestore tooa восстановления хранилища данных в основном регионе hello, точек или использовать геоизбыточных архивов toorestore tooa другом географическом регионе.</span><span class="sxs-lookup"><span data-stu-id="571f2-109">Use data warehouse backups toorestore your data warehouse tooa restore point in hello primary region, or use geo-redundant backups toorestore tooa different geographical region.</span></span> <span data-ttu-id="571f2-110">В этой статье описываются особенности hello операция восстановления хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="571f2-110">This article explains hello specifics of restoring a data warehouse.</span></span>

## <a name="what-is-a-data-warehouse-restore"></a><span data-ttu-id="571f2-111">Что такое восстановление хранилища данных?</span><span class="sxs-lookup"><span data-stu-id="571f2-111">What is a data warehouse restore?</span></span>
<span data-ttu-id="571f2-112">Восстановление хранилища данных означает создание нового хранилища данных из резервной копии существующего или удаленного хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="571f2-112">A data warehouse restore is a new data warehouse that is created from a backup of an existing or deleted data warehouse.</span></span> <span data-ttu-id="571f2-113">Hello восстановленные данные хранилища повторно создает hello хранилища резервных копий данных на определенный момент.</span><span class="sxs-lookup"><span data-stu-id="571f2-113">hello restored data warehouse re-creates hello backed-up data warehouse at a specific time.</span></span> <span data-ttu-id="571f2-114">Так как хранилище данных SQL является распределенной системой, то восстановленное хранилище данных состоит из множества файлов резервных копий, которые хранятся в больших двоичных объектах Azure.</span><span class="sxs-lookup"><span data-stu-id="571f2-114">Since SQL Data Warehouse is a distributed system, a data warehouse restore is created from many backup files that are stored in Azure blobs.</span></span> 

<span data-ttu-id="571f2-115">Восстановление базы данных является важной частью любой стратегии непрерывности бизнес-процессов и аварийного восстановления, так как позволяет воссоздать данные после случайного повреждения или удаления.</span><span class="sxs-lookup"><span data-stu-id="571f2-115">Database restore is an essential part of any business continuity and disaster recovery strategy because it re-creates your data after accidental corruption or deletion.</span></span>

<span data-ttu-id="571f2-116">Дополнительные сведения можно найти в разделе </span><span class="sxs-lookup"><span data-stu-id="571f2-116">For more information, see:</span></span>

* [<span data-ttu-id="571f2-117">Архивация хранилища данных SQL</span><span class="sxs-lookup"><span data-stu-id="571f2-117">SQL Data Warehouse backups</span></span>](sql-data-warehouse-backups.md)
* [<span data-ttu-id="571f2-118">Общие сведения о непрерывности бизнес-процессов</span><span class="sxs-lookup"><span data-stu-id="571f2-118">Business continuity overview</span></span>](../sql-database/sql-database-business-continuity.md)

## <a name="data-warehouse-restore-points"></a><span data-ttu-id="571f2-119">Точки восстановления хранилища данных SQL</span><span class="sxs-lookup"><span data-stu-id="571f2-119">Data warehouse restore points</span></span>
<span data-ttu-id="571f2-120">Преимущество использования хранилища Azure Premium хранилище данных SQL использует больших двоичных объектов Azure для хранения моментальных снимков toobackup hello первичных данных хранилища.</span><span class="sxs-lookup"><span data-stu-id="571f2-120">As a benefit of using Azure Premium Storage, SQL Data Warehouse uses Azure Storage Blob snapshots toobackup hello primary data warehouse.</span></span> <span data-ttu-id="571f2-121">Каждый моментальный снимок содержит точку восстановления, которая представляет время hello hello моментальных снимков к работе.</span><span class="sxs-lookup"><span data-stu-id="571f2-121">Each snapshot has a restore point that represents hello time hello snapshot started.</span></span> <span data-ttu-id="571f2-122">toorestore хранилища данных, следует выбрать точку восстановления и выполните команду restore.</span><span class="sxs-lookup"><span data-stu-id="571f2-122">toorestore a data warehouse, you choose a restore point and issue a restore command.</span></span>  

<span data-ttu-id="571f2-123">Хранилище данных SQL всегда восстанавливает hello резервного копирования tooa новое хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="571f2-123">SQL Data Warehouse always restores hello backup tooa new data warehouse.</span></span> <span data-ttu-id="571f2-124">Можно сохранить hello восстановленных данных хранилища и hello текущего или удалите один из них.</span><span class="sxs-lookup"><span data-stu-id="571f2-124">You can either keep hello restored data warehouse and hello current one, or delete one of them.</span></span> <span data-ttu-id="571f2-125">Если требуется tooreplace hello текущего хранилища данных с помощью hello восстановления хранилища данных, можно переименовать.</span><span class="sxs-lookup"><span data-stu-id="571f2-125">If you want tooreplace hello current data warehouse with hello restored data warehouse, you can rename it.</span></span>

<span data-ttu-id="571f2-126">Если вам требуется toorestore хранилища данных, удаленных или приостановлена, вы можете [создать обращение в службу поддержки](sql-data-warehouse-get-started-create-support-ticket.md).</span><span class="sxs-lookup"><span data-stu-id="571f2-126">If you need toorestore a deleted or paused data warehouse, you can [create a support ticket](sql-data-warehouse-get-started-create-support-ticket.md).</span></span> 

<!-- 
### Can I restore a deleted data warehouse?

Yes, you can restore hello last available restore point.

Yes, for hello next seven calendar days. When you delete a data warehouse, SQL Data Warehouse actually keeps hello data warehouse and its snapshots for seven days just in case you need hello data. After seven days, you won't be able toorestore tooany of hello restore points. -->

## <a name="geo-redundant-restore"></a><span data-ttu-id="571f2-127">Геоизбыточное восстановление</span><span class="sxs-lookup"><span data-stu-id="571f2-127">Geo-redundant restore</span></span>
<span data-ttu-id="571f2-128">Вы можете восстановить поддержки хранилища данных SQL Azure уровня производительности выбранных область tooany хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="571f2-128">You can restore your data warehouse tooany region supporting Azure SQL Data Warehouse at your chosen performance level.</span></span> <span data-ttu-id="571f2-129">Обратите внимание на то, что 9000 и 18000 DWU не поддерживаются во всех регионах во время предварительного просмотра hello.</span><span class="sxs-lookup"><span data-stu-id="571f2-129">Please note that 9000 and 18000 DWU are not supported in all regions during hello preview.</span></span>

> [!NOTE]
> <span data-ttu-id="571f2-130">географически избыточное tooperform восстановления, вы не должны отказались от этой функции.</span><span class="sxs-lookup"><span data-stu-id="571f2-130">tooperform a geo-redundant restore you must not have opted out of this feature.</span></span>
> 
> 

## <a name="restore-timeline"></a><span data-ttu-id="571f2-131">Временная шкала восстановления</span><span class="sxs-lookup"><span data-stu-id="571f2-131">Restore timeline</span></span>
<span data-ttu-id="571f2-132">Можно восстановить базу данных tooany доступной точки восстановления в пределах hello последних семи дней.</span><span class="sxs-lookup"><span data-stu-id="571f2-132">You can restore a database tooany available restore point within hello last seven days.</span></span> <span data-ttu-id="571f2-133">Моментальные снимки запуск каждые четыре часа tooeight и доступны в течение семи дней.</span><span class="sxs-lookup"><span data-stu-id="571f2-133">Snapshots start every four tooeight hours and are available for seven days.</span></span> <span data-ttu-id="571f2-134">Если моментальный снимок старше семи дней, то срок его действия истекает и его точка восстановления перестает быть доступной.</span><span class="sxs-lookup"><span data-stu-id="571f2-134">When a snapshot is older than seven days, it expires and its restore point is no longer available.</span></span>

## <a name="restore-costs"></a><span data-ttu-id="571f2-135">Затраты на восстановление</span><span class="sxs-lookup"><span data-stu-id="571f2-135">Restore costs</span></span>
<span data-ttu-id="571f2-136">Hello хранилища плата за хранилище восстановленных данных hello оплачивается по тарифу хранилища Azure Premium hello.</span><span class="sxs-lookup"><span data-stu-id="571f2-136">hello storage charge for hello restored data warehouse is billed at hello Azure Premium Storage rate.</span></span> 

<span data-ttu-id="571f2-137">Если навести на складе восстановленных данных взимается плата для хранилища по тарифу хранилища Azure Premium hello.</span><span class="sxs-lookup"><span data-stu-id="571f2-137">If you pause a restored data warehouse, you are charged for storage at hello Azure Premium Storage rate.</span></span> <span data-ttu-id="571f2-138">Приостановка Hello преимущество — не взиматься плата за вычислительные ресурсы DWU hello.</span><span class="sxs-lookup"><span data-stu-id="571f2-138">hello advantage of pausing is you are not charged for hello DWU computing resources.</span></span>

<span data-ttu-id="571f2-139">Ознакомиться с ценами на хранилище данных SQL можно [здесь](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span><span class="sxs-lookup"><span data-stu-id="571f2-139">For more information about SQL Data Warehouse pricing, see [SQL Data Warehouse Pricing](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span></span>

## <a name="uses-for-restore"></a><span data-ttu-id="571f2-140">Применение восстановления</span><span class="sxs-lookup"><span data-stu-id="571f2-140">Uses for restore</span></span>
<span data-ttu-id="571f2-141">Hello главным образом используется для восстановления хранилища данных — toorecover данные после случайную потерю данных или повреждения.</span><span class="sxs-lookup"><span data-stu-id="571f2-141">hello primary use for data warehouse restore is toorecover data after accidental data loss or corruption.</span></span>

<span data-ttu-id="571f2-142">Tooretain восстановления хранилища данных резервной копии также можно использовать для более семи дней.</span><span class="sxs-lookup"><span data-stu-id="571f2-142">You can also use data warehouse restore tooretain a backup for longer than seven days.</span></span> <span data-ttu-id="571f2-143">После восстановления резервной копии hello имеется hello хранилище данных через Интернет и его выполнение можно приостановить бесконечно toosave вычислительных затрат.</span><span class="sxs-lookup"><span data-stu-id="571f2-143">Once hello backup is restored, you have hello data warehouse online and can pause it indefinitely toosave compute costs.</span></span> <span data-ttu-id="571f2-144">База данных приостановлена Hello расходы на хранение скоростью hello хранилища Azure Premium.</span><span class="sxs-lookup"><span data-stu-id="571f2-144">hello paused database incurs storage charges at hello Azure Premium Storage rate.</span></span> 

## <a name="related-topics"></a><span data-ttu-id="571f2-145">Связанные разделы</span><span class="sxs-lookup"><span data-stu-id="571f2-145">Related topics</span></span>
### <a name="scenarios"></a><span data-ttu-id="571f2-146">Сценарии</span><span class="sxs-lookup"><span data-stu-id="571f2-146">Scenarios</span></span>
* <span data-ttu-id="571f2-147">Сведения об обеспечении непрерывности бизнес-процессов см. в [этом обзоре](../sql-database/sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="571f2-147">For a business continuity overview, see [Business continuity overview](../sql-database/sql-database-business-continuity.md)</span></span>

<!-- ### Tasks -->

<span data-ttu-id="571f2-148">tooperform хранилища данных восстановления, восстановление с помощью:</span><span class="sxs-lookup"><span data-stu-id="571f2-148">tooperform a data warehouse restore, restore using:</span></span>

* <span data-ttu-id="571f2-149">Azure портала, см. в разделе [восстановления хранилища данных, с помощью портала Azure hello](sql-data-warehouse-restore-database-portal.md)</span><span class="sxs-lookup"><span data-stu-id="571f2-149">Azure portal, see [Restore a data warehouse using hello Azure portal](sql-data-warehouse-restore-database-portal.md)</span></span>
* <span data-ttu-id="571f2-150">командлеты PowerShell (ознакомьтесь с разделом [Восстановление хранилища данных SQL Azure (PowerShell)](sql-data-warehouse-restore-database-powershell.md));</span><span class="sxs-lookup"><span data-stu-id="571f2-150">PowerShell cmdlets, see [Restore a data warehouse using PowerShell cmdlets](sql-data-warehouse-restore-database-powershell.md)</span></span>
* <span data-ttu-id="571f2-151">REST API см. в разделе [восстановления хранилища данных, с помощью API-интерфейсов REST hello](sql-data-warehouse-restore-database-rest-api.md)</span><span class="sxs-lookup"><span data-stu-id="571f2-151">REST APIs, see [Restore a data warehouse using hello REST APIs](sql-data-warehouse-restore-database-rest-api.md)</span></span>

<!-- ### Tutorials -->

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md

<!--MSDN references-->


<!--Other Web references-->
