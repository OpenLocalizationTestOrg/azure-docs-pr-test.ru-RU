---
title: "aaaRestore хранилище данных SQL Azure (портал Azure) | Документы Microsoft"
description: "Задачи портала Azure для восстановления хранилища данных SQL Azure."
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: barbkess
editor: 
ms.assetid: b0aef539-7657-4b0e-9899-74098f5c21bc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 09/21/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: cb225d2a21b61acab70a51b69c266f8d3ffacc9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="restore-azure-sql-data-warehouse-portal"></a><span data-ttu-id="67358-103">Восстановление хранилища данных SQL Azure (портал)</span><span class="sxs-lookup"><span data-stu-id="67358-103">Restore Azure SQL Data Warehouse (portal)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="67358-104">[Обзор][Overview]</span><span class="sxs-lookup"><span data-stu-id="67358-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="67358-105">[Портал][Portal]</span><span class="sxs-lookup"><span data-stu-id="67358-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="67358-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="67358-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="67358-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="67358-107">[REST][REST]</span></span>
>
>
<span data-ttu-id="67358-108">В этой статье вы узнаете, как toorestore хранилище данных SQL Azure с помощью hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="67358-108">In this article, you will learn how toorestore Azure SQL Data Warehouse by using hello Azure portal.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="67358-109">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="67358-109">Before you begin</span></span>
<span data-ttu-id="67358-110">**Проверьте ресурсы DTU.**</span><span class="sxs-lookup"><span data-stu-id="67358-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="67358-111">Каждый экземпляр хранилища данных SQL размещается на сервере SQL Server (например, myserver.database.windows.net), которому выделена квота единиц пропускной способности данных (DTU) по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="67358-111">Each instance of SQL Data Warehouse is hosted by a SQL server (for example, myserver.database.windows.net) which has a default data throughput unit (DTU) quota.</span></span> <span data-ttu-id="67358-112">Перед началом восстановления хранилища данных SQL, убедитесь, что SQL server имеет достаточно оставшиеся квоту DTU для базы данных hello, производится восстановление.</span><span class="sxs-lookup"><span data-stu-id="67358-112">Before you can restore SQL Data Warehouse, verify that your SQL server has enough remaining DTU quota for hello database that you're restoring.</span></span> <span data-ttu-id="67358-113">toolearn квоты DTU toocalculate или toorequest дополнительные Dtu. в статье [запроса на изменение квоты DTU][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="67358-113">toolearn how toocalculate DTU quota or toorequest more DTUs, see [Request a DTU quota change][Request a DTU quota change].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="67358-114">Восстановление активной или приостановленной базы данных</span><span class="sxs-lookup"><span data-stu-id="67358-114">Restore an active or paused database</span></span>
<span data-ttu-id="67358-115">toorestore базы данных:</span><span class="sxs-lookup"><span data-stu-id="67358-115">toorestore a database:</span></span>

1. <span data-ttu-id="67358-116">Войдите в toohello [портал Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="67358-116">Sign in toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="67358-117">Hello левой панели выберите **Обзор**, а затем выберите **серверов SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="67358-117">In hello left pane, select **Browse**, and then select **SQL servers**.</span></span>

    ![Выбор "Обзор" > "Серверы SQL Server"](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. <span data-ttu-id="67358-119">Найдите свой сервер и выберите его.</span><span class="sxs-lookup"><span data-stu-id="67358-119">Find your server, and then select it.</span></span>

    ![Выбор своего сервера](./media/sql-data-warehouse-restore-database-portal/01-select-server.png)
4. <span data-ttu-id="67358-121">Найти hello экземпляр хранилища данных SQL требуется toorestore из и выберите его.</span><span class="sxs-lookup"><span data-stu-id="67358-121">Find hello instance of SQL Data Warehouse that you want toorestore from, and then select it.</span></span>

    ![Выберите экземпляр hello toorestore хранилище данных SQL](./media/sql-data-warehouse-restore-database-portal/01-select-active-dw.png)
5. <span data-ttu-id="67358-123">Hello верхней части колонки hello хранилища данных, выберите **восстановить**.</span><span class="sxs-lookup"><span data-stu-id="67358-123">At hello top of hello Data Warehouse blade, select **Restore**.</span></span>

    ![Выбор "Восстановить"](./media/sql-data-warehouse-restore-database-portal/01-select-restore-from-active.png)
6. <span data-ttu-id="67358-125">Укажите новое значение в поле **Имя базы данных**.</span><span class="sxs-lookup"><span data-stu-id="67358-125">Specify a new **Database name**.</span></span>
7. <span data-ttu-id="67358-126">Выберите hello последней **точку восстановления**.</span><span class="sxs-lookup"><span data-stu-id="67358-126">Select hello latest **Restore point**.</span></span>

   <span data-ttu-id="67358-127">Убедитесь в том, что выбрано hello последнюю точку восстановления.</span><span class="sxs-lookup"><span data-stu-id="67358-127">Make sure you choose hello latest restore point.</span></span> <span data-ttu-id="67358-128">Поскольку точки восстановления, отображаются в формате UTC, параметр по умолчанию hello может быть hello последнюю точку восстановления.</span><span class="sxs-lookup"><span data-stu-id="67358-128">Because restore points are shown in Coordinated Universal Time (UTC), hello default option might not be hello latest restore point.</span></span>

      ![Выбор точки восстановления](./media/sql-data-warehouse-restore-database-portal/01-restore-blade-from-active.png)
8. <span data-ttu-id="67358-130">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="67358-130">Select **OK**.</span></span>
9. <span data-ttu-id="67358-131">начнется процесс восстановления базы данных Hello, а также можно использовать **уведомления** toomonitor hello процесса.</span><span class="sxs-lookup"><span data-stu-id="67358-131">hello database restore process will begin, and you can use **NOTIFICATIONS** toomonitor hello process.</span></span>

> [!NOTE]
> <span data-ttu-id="67358-132">После завершения восстановления hello восстановленной базы данных можно настроить, выполнив [настроить базу данных после восстановления][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="67358-132">After hello restore has finished, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
>
>

## <a name="restore-a-deleted-database"></a><span data-ttu-id="67358-133">Восстановление удаленной базы данных.</span><span class="sxs-lookup"><span data-stu-id="67358-133">Restore a deleted database</span></span>
<span data-ttu-id="67358-134">toorestore удаленной базы данных:</span><span class="sxs-lookup"><span data-stu-id="67358-134">toorestore a deleted database:</span></span>

1. <span data-ttu-id="67358-135">Войдите в toohello [портал Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="67358-135">Sign in toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="67358-136">Hello левой панели выберите **Обзор**, а затем выберите **серверов SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="67358-136">In hello left pane, select **Browse**, and then select **SQL servers**.</span></span>

    ![Выбор "Обзор" > "Серверы SQL Server"](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. <span data-ttu-id="67358-138">Найдите свой сервер и выберите его.</span><span class="sxs-lookup"><span data-stu-id="67358-138">Find your server, and then select it.</span></span>

    ![Выбор своего сервера](./media/sql-data-warehouse-restore-database-portal/02-select-server.png)
4. <span data-ttu-id="67358-140">Прокрутите вниз toohello **операции** раздел в колонке сервера.</span><span class="sxs-lookup"><span data-stu-id="67358-140">Scroll down toohello **Operations** section on your server's blade.</span></span>
5. <span data-ttu-id="67358-141">Выберите hello **удаленных баз данных** плитки.</span><span class="sxs-lookup"><span data-stu-id="67358-141">Select hello **Deleted databases** tile.</span></span>

    ![Выберите плитку баз данных удалено hello](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dws.png)
6. <span data-ttu-id="67358-143">Выберите hello удалить базу данных, что необходимо toorestore.</span><span class="sxs-lookup"><span data-stu-id="67358-143">Select hello deleted database that you want toorestore.</span></span>

    ![Выберите toorestore базы данных](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dw.png)
7. <span data-ttu-id="67358-145">Укажите новое значение в поле **Имя базы данных**.</span><span class="sxs-lookup"><span data-stu-id="67358-145">Specify a new **Database name**.</span></span>

    ![Добавьте имя для базы данных hello](./media/sql-data-warehouse-restore-database-portal/02-restore-blade-from-deleted.png)
8. <span data-ttu-id="67358-147">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="67358-147">Select **OK**.</span></span>
9. <span data-ttu-id="67358-148">начнется процесс восстановления базы данных Hello, а также можно использовать **уведомления** toomonitor hello процесса.</span><span class="sxs-lookup"><span data-stu-id="67358-148">hello database restore process will begin, and you can use **NOTIFICATIONS** toomonitor hello process.</span></span>

> [!NOTE]
> <span data-ttu-id="67358-149">см. базы данных после завершения восстановления hello tooconfigure [настроить базу данных после восстановления][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="67358-149">tooconfigure your database after hello restore has finished, see [Configure your database after recovery][Configure your database after recovery].</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="67358-150">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="67358-150">Next steps</span></span>
<span data-ttu-id="67358-151">toolearn о функциях обеспечения непрерывности бизнеса hello выпусков базы данных SQL Azure, чтение hello [непрерывности бизнес-базы данных SQL Azure обзора][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="67358-151">toolearn about hello business continuity features of Azure SQL Database editions, read hello [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change

<!--MSDN references-->

<!--Blog references-->

<!--Other Web references-->
[Azure portal]: https://portal.azure.com/
