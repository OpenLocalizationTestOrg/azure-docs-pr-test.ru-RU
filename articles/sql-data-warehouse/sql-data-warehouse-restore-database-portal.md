---
title: "Восстановление хранилища данных SQL Azure (портал Azure) | Документация Майкрософт"
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
ms.openlocfilehash: f6bc8671410dc7015a8d2a4bea1ba11f9ae526c3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="restore-azure-sql-data-warehouse-portal"></a><span data-ttu-id="847d1-103">Восстановление хранилища данных SQL Azure (портал)</span><span class="sxs-lookup"><span data-stu-id="847d1-103">Restore Azure SQL Data Warehouse (portal)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="847d1-104">[Обзор][Overview]</span><span class="sxs-lookup"><span data-stu-id="847d1-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="847d1-105">[Портал][Portal]</span><span class="sxs-lookup"><span data-stu-id="847d1-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="847d1-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="847d1-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="847d1-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="847d1-107">[REST][REST]</span></span>
>
>
<span data-ttu-id="847d1-108">В этой статье вы узнаете, как восстановить хранилище данных SQL Azure с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="847d1-108">In this article, you will learn how to restore Azure SQL Data Warehouse by using the Azure portal.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="847d1-109">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="847d1-109">Before you begin</span></span>
<span data-ttu-id="847d1-110">**Проверьте ресурсы DTU.**</span><span class="sxs-lookup"><span data-stu-id="847d1-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="847d1-111">Каждый экземпляр хранилища данных SQL размещается на сервере SQL Server (например, myserver.database.windows.net), которому выделена квота единиц пропускной способности данных (DTU) по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="847d1-111">Each instance of SQL Data Warehouse is hosted by a SQL server (for example, myserver.database.windows.net) which has a default data throughput unit (DTU) quota.</span></span> <span data-ttu-id="847d1-112">Перед восстановлением хранилища данных SQL убедитесь, что у сервера SQL Server осталась достаточная квота DTU для восстанавливаемой базы данных.</span><span class="sxs-lookup"><span data-stu-id="847d1-112">Before you can restore SQL Data Warehouse, verify that your SQL server has enough remaining DTU quota for the database that you're restoring.</span></span> <span data-ttu-id="847d1-113">Чтобы узнать, как вычислить необходимую квоту DTU или запросить дополнительные единицы DTU, ознакомьтесь с разделом [Создание запроса в службу поддержки][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="847d1-113">To learn how to calculate DTU quota or to request more DTUs, see [Request a DTU quota change][Request a DTU quota change].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="847d1-114">Восстановление активной или приостановленной базы данных</span><span class="sxs-lookup"><span data-stu-id="847d1-114">Restore an active or paused database</span></span>
<span data-ttu-id="847d1-115">Процедура восстановления базы данных</span><span class="sxs-lookup"><span data-stu-id="847d1-115">To restore a database:</span></span>

1. <span data-ttu-id="847d1-116">Войдите на [портал Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="847d1-116">Sign in to the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="847d1-117">В левой области выберите **Обзор**, а затем — **Серверы SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="847d1-117">In the left pane, select **Browse**, and then select **SQL servers**.</span></span>

    ![Выбор "Обзор" > "Серверы SQL Server"](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. <span data-ttu-id="847d1-119">Найдите свой сервер и выберите его.</span><span class="sxs-lookup"><span data-stu-id="847d1-119">Find your server, and then select it.</span></span>

    ![Выбор своего сервера](./media/sql-data-warehouse-restore-database-portal/01-select-server.png)
4. <span data-ttu-id="847d1-121">Найдите экземпляр хранилища данных SQL, из которого требуется выполнить восстановление, и выберите его.</span><span class="sxs-lookup"><span data-stu-id="847d1-121">Find the instance of SQL Data Warehouse that you want to restore from, and then select it.</span></span>

    ![Выбор экземпляра хранилища данных SQL для восстановления](./media/sql-data-warehouse-restore-database-portal/01-select-active-dw.png)
5. <span data-ttu-id="847d1-123">В верхней части колонки "Хранилище данных" щелкните **Восстановить**.</span><span class="sxs-lookup"><span data-stu-id="847d1-123">At the top of the Data Warehouse blade, select **Restore**.</span></span>

    ![Выбор "Восстановить"](./media/sql-data-warehouse-restore-database-portal/01-select-restore-from-active.png)
6. <span data-ttu-id="847d1-125">Укажите новое значение в поле **Имя базы данных**.</span><span class="sxs-lookup"><span data-stu-id="847d1-125">Specify a new **Database name**.</span></span>
7. <span data-ttu-id="847d1-126">Выберите последнюю **точку восстановления**.</span><span class="sxs-lookup"><span data-stu-id="847d1-126">Select the latest **Restore point**.</span></span>

   <span data-ttu-id="847d1-127">Обязательно выберите последнюю точку восстановления.</span><span class="sxs-lookup"><span data-stu-id="847d1-127">Make sure you choose the latest restore point.</span></span> <span data-ttu-id="847d1-128">Так как точки восстановления отображаются в формате UTC, то по умолчанию может быть выбрана не самая последняя точка восстановления.</span><span class="sxs-lookup"><span data-stu-id="847d1-128">Because restore points are shown in Coordinated Universal Time (UTC), the default option might not be the latest restore point.</span></span>

      ![Выбор точки восстановления](./media/sql-data-warehouse-restore-database-portal/01-restore-blade-from-active.png)
8. <span data-ttu-id="847d1-130">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="847d1-130">Select **OK**.</span></span>
9. <span data-ttu-id="847d1-131">Начнется процесс восстановления базы данных, который можно отслеживать с помощью **уведомлений**.</span><span class="sxs-lookup"><span data-stu-id="847d1-131">The database restore process will begin, and you can use **NOTIFICATIONS** to monitor the process.</span></span>

> [!NOTE]
> <span data-ttu-id="847d1-132">Чтобы настроить базу данных после восстановления, ознакомьтесь с разделом [Настройка базы данных после восстановления][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="847d1-132">After the restore has finished, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
>
>

## <a name="restore-a-deleted-database"></a><span data-ttu-id="847d1-133">Восстановление удаленной базы данных.</span><span class="sxs-lookup"><span data-stu-id="847d1-133">Restore a deleted database</span></span>
<span data-ttu-id="847d1-134">Восстановление удаленной базы данных.</span><span class="sxs-lookup"><span data-stu-id="847d1-134">To restore a deleted database:</span></span>

1. <span data-ttu-id="847d1-135">Войдите на [портал Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="847d1-135">Sign in to the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="847d1-136">В левой области выберите **Обзор**, а затем — **Серверы SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="847d1-136">In the left pane, select **Browse**, and then select **SQL servers**.</span></span>

    ![Выбор "Обзор" > "Серверы SQL Server"](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. <span data-ttu-id="847d1-138">Найдите свой сервер и выберите его.</span><span class="sxs-lookup"><span data-stu-id="847d1-138">Find your server, and then select it.</span></span>

    ![Выбор своего сервера](./media/sql-data-warehouse-restore-database-portal/02-select-server.png)
4. <span data-ttu-id="847d1-140">Прокрутите внизу колонку своего сервера до раздела **Операции**.</span><span class="sxs-lookup"><span data-stu-id="847d1-140">Scroll down to the **Operations** section on your server's blade.</span></span>
5. <span data-ttu-id="847d1-141">Щелкните элемент **Удаленные базы данных**.</span><span class="sxs-lookup"><span data-stu-id="847d1-141">Select the **Deleted databases** tile.</span></span>

    ![Выбор элемента "Удаленные базы данных"](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dws.png)
6. <span data-ttu-id="847d1-143">Выберите удаленную базу данных, которую хотите восстановить.</span><span class="sxs-lookup"><span data-stu-id="847d1-143">Select the deleted database that you want to restore.</span></span>

    ![Выбор базы данных для восстановления](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dw.png)
7. <span data-ttu-id="847d1-145">Укажите новое значение в поле **Имя базы данных**.</span><span class="sxs-lookup"><span data-stu-id="847d1-145">Specify a new **Database name**.</span></span>

    ![Добавление имени для базы данных](./media/sql-data-warehouse-restore-database-portal/02-restore-blade-from-deleted.png)
8. <span data-ttu-id="847d1-147">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="847d1-147">Select **OK**.</span></span>
9. <span data-ttu-id="847d1-148">Начнется процесс восстановления базы данных, который можно отслеживать с помощью **уведомлений**.</span><span class="sxs-lookup"><span data-stu-id="847d1-148">The database restore process will begin, and you can use **NOTIFICATIONS** to monitor the process.</span></span>

> [!NOTE]
> <span data-ttu-id="847d1-149">Чтобы настроить базу данных после восстановления, ознакомьтесь с разделом [Настройка базы данных после восстановления][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="847d1-149">To configure your database after the restore has finished, see [Configure your database after recovery][Configure your database after recovery].</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="847d1-150">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="847d1-150">Next steps</span></span>
<span data-ttu-id="847d1-151">Дополнительные сведения о функциях, обеспечивающих непрерывность бизнес-процессов в выпусках Базы данных SQL Azure, см. в статье [Обзор обеспечения непрерывности бизнес-процессов с помощью базы данных SQL Azure][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="847d1-151">To learn about the business continuity features of Azure SQL Database editions, read the [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

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
