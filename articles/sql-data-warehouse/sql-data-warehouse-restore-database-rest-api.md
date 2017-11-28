---
title: "Хранилище данных SQL Azure (REST API) aaaRestore | Документы Microsoft"
description: "Задачи REST API для восстановления хранилища данных SQL."
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: fca922c6-b675-49c7-907e-5dcf26d451dd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: cf6678d71aafff71b1ea715f447e41e25f20d1b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-azure-sql-data-warehouse-rest-api"></a><span data-ttu-id="a7246-103">Восстановление хранилища данных SQL Azure (REST API)</span><span class="sxs-lookup"><span data-stu-id="a7246-103">Restore an Azure SQL Data Warehouse (REST API)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="a7246-104">[Обзор][Overview]</span><span class="sxs-lookup"><span data-stu-id="a7246-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="a7246-105">[Портал][Portal]</span><span class="sxs-lookup"><span data-stu-id="a7246-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="a7246-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="a7246-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="a7246-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="a7246-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="a7246-108">В этой статье вы узнаете, как хранилище данных SQL Azure с помощью toorestore hello REST API.</span><span class="sxs-lookup"><span data-stu-id="a7246-108">In this article you will learn how toorestore an Azure SQL Data Warehouse using hello REST API.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a7246-109">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="a7246-109">Before you begin</span></span>
<span data-ttu-id="a7246-110">**Проверьте ресурсы DTU.**</span><span class="sxs-lookup"><span data-stu-id="a7246-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="a7246-111">Каждое хранилище данных SQL размещается на сервере SQL Server (например, myserver.database.windows.net), которому выделена квота DTU по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a7246-111">Each SQL Data Warehouse is hosted by a SQL server (e.g. myserver.database.windows.net) which has a default DTU quota.</span></span>  <span data-ttu-id="a7246-112">Перед началом восстановления хранилища данных SQL, убедитесь, что hello, SQL server имеет достаточно оставшиеся квоту DTU для hello восстанавливаемой базы данных.</span><span class="sxs-lookup"><span data-stu-id="a7246-112">Before you can restore a SQL Data Warehouse, verify that hello your SQL server has enough remaining DTU quota for hello database being restored.</span></span> <span data-ttu-id="a7246-113">toolearn как необходимые toocalculate DTU или toorequest дополнительные DTU см [запроса на изменение квоты DTU][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="a7246-113">toolearn how toocalculate DTU needed or toorequest more DTU, see [Request a DTU quota change][Request a DTU quota change].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="a7246-114">Восстановление активной или приостановленной базы данных</span><span class="sxs-lookup"><span data-stu-id="a7246-114">Restore an active or paused database</span></span>
<span data-ttu-id="a7246-115">toorestore базы данных:</span><span class="sxs-lookup"><span data-stu-id="a7246-115">toorestore a database:</span></span>

1. <span data-ttu-id="a7246-116">Получите список hello точки восстановления базы данных с помощью операции Get точки восстановления базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="a7246-116">Get hello list of database restore points using hello Get Database Restore Points operation.</span></span>
2. <span data-ttu-id="a7246-117">Перед началом восстановления с помощью hello [Создание запроса на восстановление базы данных] [ Create database restore request] операции.</span><span class="sxs-lookup"><span data-stu-id="a7246-117">Begin your restore by using hello [Create database restore request][Create database restore request] operation.</span></span>
3. <span data-ttu-id="a7246-118">Отслеживать состояние hello восстановления с помощью hello [состояние операции базы данных] [ Database operation status] операции.</span><span class="sxs-lookup"><span data-stu-id="a7246-118">Track hello status of your restore by using hello [Database operation status][Database operation status] operation.</span></span>

> [!NOTE]
> <span data-ttu-id="a7246-119">После завершения восстановления hello восстановленной базы данных можно настроить, выполнив [настроить базу данных после восстановления][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="a7246-119">After hello restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-a-deleted-database"></a><span data-ttu-id="a7246-120">Восстановление удаленной базы данных.</span><span class="sxs-lookup"><span data-stu-id="a7246-120">Restore a deleted database</span></span>
<span data-ttu-id="a7246-121">toorestore удаленной базы данных:</span><span class="sxs-lookup"><span data-stu-id="a7246-121">toorestore a deleted database:</span></span>

1. <span data-ttu-id="a7246-122">Список всех доступных для восстановления удаленных баз данных с помощью hello [удаленные базы данных, могут быть восстановлены список] [ List restorable dropped databases] операции.</span><span class="sxs-lookup"><span data-stu-id="a7246-122">List all of your restorable deleted databases by using hello [List restorable dropped databases][List restorable dropped databases] operation.</span></span>
2. <span data-ttu-id="a7246-123">Получить сведения о hello hello удалить базы данных, которая toorestore с помощью hello [базы данных удалены Get, которые могут быть восстановлены] [ Get restorable dropped database] операции.</span><span class="sxs-lookup"><span data-stu-id="a7246-123">Get hello details for hello deleted database you want toorestore by using hello [Get restorable dropped database][Get restorable dropped database] operation.</span></span>
3. <span data-ttu-id="a7246-124">Перед началом восстановления с помощью hello [Создание запроса на восстановление базы данных] [ Create database restore request] операции.</span><span class="sxs-lookup"><span data-stu-id="a7246-124">Begin your restore by using hello [Create database restore request][Create database restore request] operation.</span></span>
4. <span data-ttu-id="a7246-125">Отслеживать состояние hello восстановления с помощью hello [состояние операции базы данных] [ Database operation status] операции.</span><span class="sxs-lookup"><span data-stu-id="a7246-125">Track hello status of your restore by using hello [Database operation status][Database operation status] operation.</span></span>

> [!NOTE]
> <span data-ttu-id="a7246-126">см. базы данных после завершения восстановления hello tooconfigure [настроить базу данных после восстановления][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="a7246-126">tooconfigure your database after hello restore has completed, see [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="a7246-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a7246-127">Next steps</span></span>
<span data-ttu-id="a7246-128">toolearn о функциях обеспечения непрерывности бизнеса hello выпусков базы данных SQL Azure, прочитайте hello [непрерывности бизнес-базы данных SQL Azure обзора][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="a7246-128">toolearn about hello business continuity features of Azure SQL Database editions, please read hello [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md

<!--MSDN references-->
[Create database restore request]: https://msdn.microsoft.com/library/azure/dn509571.aspx
[Database operation status]: https://msdn.microsoft.com/library/azure/dn720371.aspx
[Get restorable dropped database]: https://msdn.microsoft.com/library/azure/dn509574.aspx
[List restorable dropped databases]: https://msdn.microsoft.com/library/azure/dn509562.aspx
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx

<!--Other Web references-->
[Azure Portal]: https://portal.azure.com/
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
