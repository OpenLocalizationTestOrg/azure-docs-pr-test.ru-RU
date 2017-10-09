---
title: "aaaRestore одной таблицы из резервной копии базы данных SQL Azure | Документы Microsoft"
description: "Узнайте, как toorestore один таблицу из резервной копии базы данных SQL Azure."
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: 340b41bd-9df8-47fb-adfc-03216de38a5e
ms.service: sql-database
ms.custom: business continuity
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: 696d2ac87a70bccdf063bfecb8255723404aa5bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorestore-a-single-table-from-an-azure-sql-database-backup"></a><span data-ttu-id="c3b57-103">Как toorestore один таблицу из резервной копии базы данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="c3b57-103">How toorestore a single table from an Azure SQL Database backup</span></span>
<span data-ttu-id="c3b57-104">Могут возникнуть ситуации, в которых случайно изменены некоторые данные в базе данных SQL, а теперь нужно toorecover hello один изменяемой таблицы.</span><span class="sxs-lookup"><span data-stu-id="c3b57-104">You may encounter a situation in which you accidentally modified some data in a SQL database and now you want toorecover hello single affected table.</span></span> <span data-ttu-id="c3b57-105">В этой статье описывается, как toorestore одной таблицы в базе данных из одной базы данных SQL hello [автоматического резервного копирования](sql-database-automated-backups.md).</span><span class="sxs-lookup"><span data-stu-id="c3b57-105">This article describes how toorestore a single table in a database from one of hello SQL Database [automatic backups](sql-database-automated-backups.md).</span></span>

## <a name="preparation-steps-rename-hello-table-and-restore-a-copy-of-hello-database"></a><span data-ttu-id="c3b57-106">Действия по подготовке: переименовать таблицу hello и восстановить копию базы данных hello</span><span class="sxs-lookup"><span data-stu-id="c3b57-106">Preparation steps: Rename hello table and restore a copy of hello database</span></span>
1. <span data-ttu-id="c3b57-107">Определите таблицу hello в нужных tooreplace hello восстановить копию базы данных Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="c3b57-107">Identify hello table in your Azure SQL database that you want tooreplace with hello restored copy.</span></span> <span data-ttu-id="c3b57-108">Используйте таблицу hello toorename Microsoft SQL Management Studio.</span><span class="sxs-lookup"><span data-stu-id="c3b57-108">Use Microsoft SQL Management Studio toorename hello table.</span></span> <span data-ttu-id="c3b57-109">Например, переименуйте таблицу hello как &lt;имя таблицы&gt;_old.</span><span class="sxs-lookup"><span data-stu-id="c3b57-109">For example, rename hello table as &lt;table name&gt;_old.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c3b57-110">tooavoid блокируются, убедитесь, что никакие действия, выполняемые для таблицы hello переименовываемый.</span><span class="sxs-lookup"><span data-stu-id="c3b57-110">tooavoid being blocked, make sure that there's no activity running on hello table that you are renaming.</span></span> <span data-ttu-id="c3b57-111">Если возникают какие-либо проблемы, выполняйте это действие в период обслуживания.</span><span class="sxs-lookup"><span data-stu-id="c3b57-111">If you encounter issues, make sure that perform this procedure during a maintenance window.</span></span>
   >

2. <span data-ttu-id="c3b57-112">Восстановление резервной копии базы данных tooa точки времени, которые должны toorecover toousing hello [восстановитьточки-In_Time](sql-database-recovery-using-backups.md#point-in-time-restore) действия.</span><span class="sxs-lookup"><span data-stu-id="c3b57-112">Restore a backup of your database tooa point in time that you want toorecover toousing hello [Point-In_Time Restore](sql-database-recovery-using-backups.md#point-in-time-restore) steps.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c3b57-113">Имя Hello hello восстановления базы данных будет представлено в формате hello DBName + отметки времени; например **Adventureworks2012_2016-01-01T22-12Z**.</span><span class="sxs-lookup"><span data-stu-id="c3b57-113">hello name of hello restored database will be in hello DBName+TimeStamp format; for example, **Adventureworks2012_2016-01-01T22-12Z**.</span></span> <span data-ttu-id="c3b57-114">Этот шаг не приводит к перезаписи hello имя существующей базы данных на сервере hello.</span><span class="sxs-lookup"><span data-stu-id="c3b57-114">This step doesn't overwrite hello existing database name on hello server.</span></span> <span data-ttu-id="c3b57-115">Это средство безопасности, и она предназначена tooallow tooverify hello резервной копии базы данных перед их удалите их из текущей базы данных и присвойте hello восстановить базу данных для использования в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="c3b57-115">This is a safety measure, and it's intended tooallow you tooverify hello restored database before they drop their current database and rename hello restored database for production use.</span></span>
   
## <a name="copying-hello-table-from-hello-restored-database-by-using-hello-sql-database-migration-tool"></a><span data-ttu-id="c3b57-116">Копирование таблицы hello из hello восстановления базы данных с помощью средства миграции баз данных SQL hello</span><span class="sxs-lookup"><span data-stu-id="c3b57-116">Copying hello table from hello restored database by using hello SQL Database Migration tool</span></span>

1. <span data-ttu-id="c3b57-117">Загрузите и установите hello [мастер миграции баз данных SQL](https://sqlazuremw.codeplex.com).</span><span class="sxs-lookup"><span data-stu-id="c3b57-117">Download and install hello [SQL Database Migration Wizard](https://sqlazuremw.codeplex.com).</span></span>
2. <span data-ttu-id="c3b57-118">Откройте мастер миграции баз данных SQL, hello на hello **Выбор процесса** выберите **базы данных в группе анализ/перенос**и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="c3b57-118">Open hello SQL Database Migration Wizard, on hello **Select Process** page, select **Database under Analyze/Migrate**, and then click **Next**.</span></span>

   ![Мастер миграции баз данных SQL — выбор процесса](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/1.png)

3. <span data-ttu-id="c3b57-120">В hello **подключения tooServer** диалогового окна поле, примените hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="c3b57-120">In hello **Connect tooServer** dialog box, apply hello following settings:</span></span>

   * <span data-ttu-id="c3b57-121">Имя сервера: **ваш сервер SQL**.</span><span class="sxs-lookup"><span data-stu-id="c3b57-121">Server name: **Your SQL server**</span></span>
   * <span data-ttu-id="c3b57-122">Аутентификация: **аутентификация SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="c3b57-122">Authentication: **SQL Server Authentication**</span></span>
   * <span data-ttu-id="c3b57-123">Имя для входа: **ваше имя для входа**.</span><span class="sxs-lookup"><span data-stu-id="c3b57-123">Login: **Your login**</span></span>
   * <span data-ttu-id="c3b57-124">Пароль: **ваш пароль**.</span><span class="sxs-lookup"><span data-stu-id="c3b57-124">Password: **Your password**</span></span>
   * <span data-ttu-id="c3b57-125">База данных: **главная база данных (список всех баз данных)**.</span><span class="sxs-lookup"><span data-stu-id="c3b57-125">Database: **Master DB (List all databases)**</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c3b57-126">По умолчанию hello мастер сохраняет учетные данные входа.</span><span class="sxs-lookup"><span data-stu-id="c3b57-126">By default hello wizard saves your login information.</span></span> <span data-ttu-id="c3b57-127">Если этого не нужно делать, установите флажок **Forget Login Information** (Не запоминать учетные данные).</span><span class="sxs-lookup"><span data-stu-id="c3b57-127">If you don't want it to, select **Forget Login Information**.</span></span>
   >
   
     ![Мастер миграции баз данных SQL — выбор источника, шаг 1](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/2.png)
4. <span data-ttu-id="c3b57-129">В hello **Выбор источника** диалоговое окно, выберите hello восстановить имя базы данных из hello **действия по подготовке** статьи в качестве источника, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="c3b57-129">In hello **Select Source** dialog box, select hello restored database name from hello **Preparation steps** section as your source, and then click **Next**.</span></span>
   
    ![Мастер миграции баз данных SQL — выбор источника, шаг 2](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/3.png)
5. <span data-ttu-id="c3b57-131">В hello **Выбор объектов** диалоговое окно, выберите hello **выбрать конкретные объекты базы данных** и затем выбрать table(or tables) hello нужных toomigrate toohello целевого сервера.</span><span class="sxs-lookup"><span data-stu-id="c3b57-131">In hello **Choose Objects** dialog box, select hello **Select specific database objects** option, and then select hello table(or tables) that you want toomigrate toohello target server.</span></span>
   <span data-ttu-id="c3b57-132">![Мастер миграции баз данных SQL — выбор объектов](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/4.png)</span><span class="sxs-lookup"><span data-stu-id="c3b57-132">![SQL Database Migration wizard - Choose Objects](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/4.png)</span></span>
6. <span data-ttu-id="c3b57-133">На hello **Сводка мастера сценариев** щелкните **Да** при появлении запроса о ли вы будете готовы toogenerate сценарий SQL.</span><span class="sxs-lookup"><span data-stu-id="c3b57-133">On hello **Script Wizard Summary** page, click **Yes** when you’re prompted about whether you’re ready toogenerate a SQL script.</span></span> <span data-ttu-id="c3b57-134">Также имеется параметр hello toosave hello скрипта TSQL для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="c3b57-134">You also have hello option toosave hello TSQL Script for later use.</span></span>
   <span data-ttu-id="c3b57-135">![Мастер миграции баз данных SQL — сводка мастера сценариев](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/5.png)</span><span class="sxs-lookup"><span data-stu-id="c3b57-135">![SQL Database Migration wizard - Script Wizard Summary](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/5.png)</span></span>
7. <span data-ttu-id="c3b57-136">На hello **сводки результатов** щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="c3b57-136">On hello **Results Summary** page, click **Next**.</span></span>
   <span data-ttu-id="c3b57-137">![Мастер миграции баз данных SQL — сводка результатов](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/6.png)</span><span class="sxs-lookup"><span data-stu-id="c3b57-137">![SQL Database Migration wizard - Results Summary](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/6.png)</span></span>
8. <span data-ttu-id="c3b57-138">На hello **соединение с целевым сервером установки** щелкните **подключения tooServer**и введите сведения о hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c3b57-138">On hello **Setup Target Server Connection** page, click **Connect tooServer**, and then enter hello details as follows:</span></span>
   
   * <span data-ttu-id="c3b57-139">**Имя сервера**: экземпляр целевого сервера.</span><span class="sxs-lookup"><span data-stu-id="c3b57-139">**Server Name**: Target server instance</span></span>
   * <span data-ttu-id="c3b57-140">**проверка подлинности:** **проверка подлинности SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="c3b57-140">**Authentication**: **SQL Server authentication**.</span></span> <span data-ttu-id="c3b57-141">Введите свои учетные данные.</span><span class="sxs-lookup"><span data-stu-id="c3b57-141">Enter your login credentials.</span></span>
   * <span data-ttu-id="c3b57-142">**база данных:** **база данных master (список всех баз данных)**.</span><span class="sxs-lookup"><span data-stu-id="c3b57-142">**Database**: **Master DB (List all databases)**.</span></span> <span data-ttu-id="c3b57-143">Этот список будет содержать все hello базы данных на целевом сервере hello.</span><span class="sxs-lookup"><span data-stu-id="c3b57-143">This option lists all hello databases on hello target server.</span></span>
     
     ![Мастер миграции баз данных SQL — настройка подключения к целевому серверу](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/7.png)
9. <span data-ttu-id="c3b57-145">Нажмите кнопку **Connect**выберите целевую базу данных hello, toomove hello таблицы и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="c3b57-145">Click **Connect**, select hello target database that you want toomove hello table to, and then click **Next**.</span></span> <span data-ttu-id="c3b57-146">Это должно быть завершено выполнение скрипта ранее созданных hello, и вы увидите, что hello вновь перемещены таблицы копируются toohello целевой базы данных.</span><span class="sxs-lookup"><span data-stu-id="c3b57-146">This should finish running hello previously generated script, and you should see hello newly moved table copied toohello target database.</span></span>

## <a name="verification-step"></a><span data-ttu-id="c3b57-147">Проверка</span><span class="sxs-lookup"><span data-stu-id="c3b57-147">Verification step</span></span>

- <span data-ttu-id="c3b57-148">Запросов и тестирования hello вновь скопировать таблицу toomake том, что данные hello без изменений.</span><span class="sxs-lookup"><span data-stu-id="c3b57-148">Query and test hello newly copied table toomake sure that hello data is intact.</span></span> <span data-ttu-id="c3b57-149">После подтверждения, ее можно удалить hello переименовать таблицу **действия по подготовке** раздела.</span><span class="sxs-lookup"><span data-stu-id="c3b57-149">Upon confirmation, you can drop hello renamed table form **Preparation steps** section.</span></span> <span data-ttu-id="c3b57-150">(Например, &lt;имя таблицы&gt;_old.)</span><span class="sxs-lookup"><span data-stu-id="c3b57-150">(for example, &lt;table name&gt;_old).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3b57-151">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c3b57-151">Next steps</span></span>
[<span data-ttu-id="c3b57-152">Общие сведения об автоматическом резервном копировании базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="c3b57-152">SQL Database automatic backups</span></span>](sql-database-automated-backups.md)

