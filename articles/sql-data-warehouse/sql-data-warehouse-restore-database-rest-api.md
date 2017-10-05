---
title: "Восстановление хранилища данных SQL Azure (REST API) | Документация Майкрософт"
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
ms.openlocfilehash: 8656607611e7518e42b51b91774f55abec15c228
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="restore-an-azure-sql-data-warehouse-rest-api"></a><span data-ttu-id="dd5c9-103">Восстановление хранилища данных SQL Azure (REST API)</span><span class="sxs-lookup"><span data-stu-id="dd5c9-103">Restore an Azure SQL Data Warehouse (REST API)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="dd5c9-104">[Обзор][Overview]</span><span class="sxs-lookup"><span data-stu-id="dd5c9-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="dd5c9-105">[Портал][Portal]</span><span class="sxs-lookup"><span data-stu-id="dd5c9-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="dd5c9-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="dd5c9-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="dd5c9-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="dd5c9-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="dd5c9-108">Из этой статьи вы узнаете, как восстановить хранилище данных SQL Azure с помощью REST API.</span><span class="sxs-lookup"><span data-stu-id="dd5c9-108">In this article you will learn how to restore an Azure SQL Data Warehouse using the REST API.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="dd5c9-109">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="dd5c9-109">Before you begin</span></span>
<span data-ttu-id="dd5c9-110">**Проверьте ресурсы DTU.**</span><span class="sxs-lookup"><span data-stu-id="dd5c9-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="dd5c9-111">Каждое хранилище данных SQL размещается на сервере SQL Server (например, myserver.database.windows.net), которому выделена квота DTU по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="dd5c9-111">Each SQL Data Warehouse is hosted by a SQL server (e.g. myserver.database.windows.net) which has a default DTU quota.</span></span>  <span data-ttu-id="dd5c9-112">Перед восстановлением хранилища данных SQL убедитесь, что у сервера SQL Server осталась достаточная квота DTU для восстанавливаемой базы данных.</span><span class="sxs-lookup"><span data-stu-id="dd5c9-112">Before you can restore a SQL Data Warehouse, verify that the your SQL server has enough remaining DTU quota for the database being restored.</span></span> <span data-ttu-id="dd5c9-113">Чтобы узнать, как вычислить необходимое количество DTU или запросить дополнительные единицы DTU, ознакомьтесь с разделом [Создание запроса в службу поддержки][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="dd5c9-113">To learn how to calculate DTU needed or to request more DTU, see [Request a DTU quota change][Request a DTU quota change].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="dd5c9-114">Восстановление активной или приостановленной базы данных</span><span class="sxs-lookup"><span data-stu-id="dd5c9-114">Restore an active or paused database</span></span>
<span data-ttu-id="dd5c9-115">Процедура восстановления базы данных</span><span class="sxs-lookup"><span data-stu-id="dd5c9-115">To restore a database:</span></span>

1. <span data-ttu-id="dd5c9-116">Получите список точек восстановления базы данных с помощью операции Get Database Restore Points.</span><span class="sxs-lookup"><span data-stu-id="dd5c9-116">Get the list of database restore points using the Get Database Restore Points operation.</span></span>
2. <span data-ttu-id="dd5c9-117">Начните восстановление с помощью операции [Create Database Restore Request][Create database restore request].</span><span class="sxs-lookup"><span data-stu-id="dd5c9-117">Begin your restore by using the [Create database restore request][Create database restore request] operation.</span></span>
3. <span data-ttu-id="dd5c9-118">Отследите состояние восстановления с помощью операции [Database Operation Status][Database operation status].</span><span class="sxs-lookup"><span data-stu-id="dd5c9-118">Track the status of your restore by using the [Database operation status][Database operation status] operation.</span></span>

> [!NOTE]
> <span data-ttu-id="dd5c9-119">Чтобы настроить базу данных после восстановления, см. раздел [Настройка базы данных после восстановления][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="dd5c9-119">After the restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-a-deleted-database"></a><span data-ttu-id="dd5c9-120">Восстановление удаленной базы данных.</span><span class="sxs-lookup"><span data-stu-id="dd5c9-120">Restore a deleted database</span></span>
<span data-ttu-id="dd5c9-121">Восстановление удаленной базы данных.</span><span class="sxs-lookup"><span data-stu-id="dd5c9-121">To restore a deleted database:</span></span>

1. <span data-ttu-id="dd5c9-122">Создайте список всех удаленных баз данных, доступных для восстановления, с помощью операции [List Restorable Dropped Databases][List restorable dropped databases].</span><span class="sxs-lookup"><span data-stu-id="dd5c9-122">List all of your restorable deleted databases by using the [List restorable dropped databases][List restorable dropped databases] operation.</span></span>
2. <span data-ttu-id="dd5c9-123">Получите подробные сведения об удаленной базе данных, которую необходимо восстановить, с помощью операции [Get Restorable Dropped Database][Get restorable dropped database].</span><span class="sxs-lookup"><span data-stu-id="dd5c9-123">Get the details for the deleted database you want to restore by using the [Get restorable dropped database][Get restorable dropped database] operation.</span></span>
3. <span data-ttu-id="dd5c9-124">Начните восстановление с помощью операции [Create Database Restore Request][Create database restore request].</span><span class="sxs-lookup"><span data-stu-id="dd5c9-124">Begin your restore by using the [Create database restore request][Create database restore request] operation.</span></span>
4. <span data-ttu-id="dd5c9-125">Отследите состояние восстановления с помощью операции [Database Operation Status][Database operation status].</span><span class="sxs-lookup"><span data-stu-id="dd5c9-125">Track the status of your restore by using the [Database operation status][Database operation status] operation.</span></span>

> [!NOTE]
> <span data-ttu-id="dd5c9-126">Чтобы настроить базу данных после восстановления, см. раздел [Настройка базы данных после восстановления][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="dd5c9-126">To configure your database after the restore has completed, see [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="dd5c9-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dd5c9-127">Next steps</span></span>
<span data-ttu-id="dd5c9-128">Дополнительные сведения о функциях, обеспечивающих непрерывность бизнес-процессов в выпусках Базы данных SQL Azure, см. в статье [Обзор обеспечения непрерывности бизнес-процессов с помощью базы данных SQL Azure][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="dd5c9-128">To learn about the business continuity features of Azure SQL Database editions, please read the [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[How to install and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
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
