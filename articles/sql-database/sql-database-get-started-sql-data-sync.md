---
title: "aaaGetting к работе с SQL Azure Data Sync (Предварительная версия) | Документы Microsoft"
description: "Это руководство поможет вам приступить к работе с синхронизацией данных SQL Azure (предварительная версия)."
services: sql-database
documentationcenter: 
author: douglaslms
manager: craigg
editor: 
ms.assetid: a295a768-7ff2-4a86-a253-0090281c8efa
ms.service: sql-database
ms.custom: load & move data
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: douglasl
ms.openlocfilehash: 666d09237e42acc23ae3c8c81e60734a413f5949
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-sql-data-sync-preview"></a><span data-ttu-id="786af-103">Приступая к работе с синхронизацией данных SQL Azure (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="786af-103">Getting Started with Azure SQL Data Sync (Preview)</span></span>
<span data-ttu-id="786af-104">В этом учебнике вы узнаете, как tooset копирование синхронизации данных SQL Azure путем создания гибридных группы синхронизации, содержит экземпляры базы данных SQL Azure и SQL Server.</span><span class="sxs-lookup"><span data-stu-id="786af-104">In this tutorial, you learn how tooset up Azure SQL Data Sync by creating a hybrid sync group that contains both Azure SQL Database and SQL Server instances.</span></span> <span data-ttu-id="786af-105">Hello новых групп синхронизации полностью настроена и синхронизирует на hello запланированное время.</span><span class="sxs-lookup"><span data-stu-id="786af-105">hello new sync group is fully configured and synchronizes on hello schedule you set.</span></span>

<span data-ttu-id="786af-106">В этом руководстве предполагается, что у вас имеется некоторый опыт работы с базой данных SQL и SQL Server.</span><span class="sxs-lookup"><span data-stu-id="786af-106">This tutorial assumes that you have at least some prior experience with SQL Database and with SQL Server.</span></span> 

<span data-ttu-id="786af-107">Общие сведения о синхронизации данных SQL см. в разделе [Синхронизация данных](sql-database-sync-data.md).</span><span class="sxs-lookup"><span data-stu-id="786af-107">For an overview of SQL Data Sync, see [Sync data](sql-database-sync-data.md).</span></span>

<span data-ttu-id="786af-108">Полные примеры PowerShell, которые показывают, как tooconfigure SQL Data Sync см. статью hello в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="786af-108">For complete PowerShell examples that show how tooconfigure SQL Data Sync, see hello following articles:</span></span>
-   [<span data-ttu-id="786af-109">Используйте PowerShell toosync между несколькими базами данных Azure SQL</span><span class="sxs-lookup"><span data-stu-id="786af-109">Use PowerShell toosync between multiple Azure SQL databases</span></span>](scripts/sql-database-sync-data-between-sql-databases.md)
-   [<span data-ttu-id="786af-110">Используйте PowerShell toosync между базы данных SQL Azure и локальной базы данных SQL Server</span><span class="sxs-lookup"><span data-stu-id="786af-110">Use PowerShell toosync between an Azure SQL Database and a SQL Server on-premises database</span></span>](scripts/sql-database-sync-data-between-azure-onprem.md)

> [!NOTE]
> <span data-ttu-id="786af-111">Hello полный набор технических документов о синхронизации данных SQL Azure, ранее доступные в библиотеке MSDN, доступен в виде. PDF-документ.</span><span class="sxs-lookup"><span data-stu-id="786af-111">hello complete technical documentation set for Azure SQL Data Sync, formerly located on MSDN, is available as a .PDF document.</span></span> <span data-ttu-id="786af-112">Его можно скачать [здесь](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true).</span><span class="sxs-lookup"><span data-stu-id="786af-112">Download it [here](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true).</span></span>

## <a name="step-1---create-sync-group"></a><span data-ttu-id="786af-113">Шаг 1. Создание группы синхронизации</span><span class="sxs-lookup"><span data-stu-id="786af-113">Step 1 - Create sync group</span></span>

### <a name="locate-hello-data-sync-settings"></a><span data-ttu-id="786af-114">Поиск параметров синхронизации данных hello</span><span class="sxs-lookup"><span data-stu-id="786af-114">Locate hello Data Sync settings</span></span>

1.  <span data-ttu-id="786af-115">В браузере перейдите toohello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="786af-115">In your browser, navigate toohello Azure portal.</span></span>

2.  <span data-ttu-id="786af-116">Hello портала найдите базами данных SQL из панели мониторинга или значок hello баз данных SQL на панели инструментов hello.</span><span class="sxs-lookup"><span data-stu-id="786af-116">In hello portal, locate your SQL databases from your Dashboard or from hello SQL Databases icon on hello toolbar.</span></span>

    ![Список баз данных SQL Azure](media/sql-database-get-started-sql-data-sync/datasync-preview-sqldbs.png)

3.  <span data-ttu-id="786af-118">На hello **баз данных SQL** колонки, hello выберите существующую базу данных SQL требуется toouse как открывает hello базы данных основного сервера для синхронизации данных. hello SQL колонке базы данных.</span><span class="sxs-lookup"><span data-stu-id="786af-118">On hello **SQL databases** blade, select hello existing SQL database that you want toouse as hello hub database for Data Sync. hello SQL database blade opens.</span></span>

4.  <span data-ttu-id="786af-119">В колонке базы данных SQL hello для hello выбранной базы данных, выберите **синхронизировать базы данных tooother**.</span><span class="sxs-lookup"><span data-stu-id="786af-119">On hello SQL database blade for hello selected database, select **Sync tooother databases**.</span></span> <span data-ttu-id="786af-120">Открывает колонку Hello синхронизации данных.</span><span class="sxs-lookup"><span data-stu-id="786af-120">hello Data Sync blade opens.</span></span>

    ![Параметр базы данных tooother синхронизации](media/sql-database-get-started-sql-data-sync/datasync-preview-newsyncgroup.png)

### <a name="create-a-new-sync-group"></a><span data-ttu-id="786af-122">Создание группы синхронизации</span><span class="sxs-lookup"><span data-stu-id="786af-122">Create a new Sync Group</span></span>

1.  <span data-ttu-id="786af-123">В колонке hello синхронизации данных, выберите **новых групп синхронизации**.</span><span class="sxs-lookup"><span data-stu-id="786af-123">On hello Data Sync blade, select **New Sync Group**.</span></span> <span data-ttu-id="786af-124">Hello **новых групп синхронизации** открывает колонку с шага 1, **создать группу синхронизации**, выделенный.</span><span class="sxs-lookup"><span data-stu-id="786af-124">hello **New sync group** blade opens with Step 1, **Create sync group**, highlighted.</span></span> <span data-ttu-id="786af-125">Hello **создать группу синхронизации данных** также открывает колонку.</span><span class="sxs-lookup"><span data-stu-id="786af-125">hello **Create Data Sync Group** blade also opens.</span></span>

2.  <span data-ttu-id="786af-126">На hello **создать группу синхронизации данных** колонке hello следующие действия:</span><span class="sxs-lookup"><span data-stu-id="786af-126">On hello **Create Data Sync Group** blade, do hello following things:</span></span>

    1.  <span data-ttu-id="786af-127">В hello **имя группы синхронизации** введите имя для новой группы синхронизации hello.</span><span class="sxs-lookup"><span data-stu-id="786af-127">In hello **Sync Group Name** field, enter a name for hello new sync group.</span></span>

    2.  <span data-ttu-id="786af-128">В hello **базы данных метаданных синхронизации** выберите ли toocreate новой базы данных (рекомендуется) или toouse существующей базы данных.</span><span class="sxs-lookup"><span data-stu-id="786af-128">In hello **Sync Metadata Database** section, choose whether toocreate a new database (recommended) or toouse an existing database.</span></span>

        > [!NOTE]
        > <span data-ttu-id="786af-129">Корпорация Майкрософт рекомендует создать toouse новую пустую базу данных, как hello синхронизации базы данных метаданных.</span><span class="sxs-lookup"><span data-stu-id="786af-129">Microsoft recommends that you create a new, empty database toouse as hello Sync Metadata Database.</span></span> <span data-ttu-id="786af-130">Служба синхронизации данных создает таблицы в этой базе данных и часто выполняет рабочую нагрузку.</span><span class="sxs-lookup"><span data-stu-id="786af-130">Data Sync creates tables in this database and runs a frequent workload.</span></span> <span data-ttu-id="786af-131">Эта база данных автоматически становятся как hello синхронизации базы данных метаданных для всех групп синхронизации в выбранной области hello.</span><span class="sxs-lookup"><span data-stu-id="786af-131">This database is automatically shared as hello Sync Metadata Database for all of your Sync groups in hello selected region.</span></span> <span data-ttu-id="786af-132">Нельзя изменить hello синхронизации базы данных метаданных, имени или ее обновления без его удаления.</span><span class="sxs-lookup"><span data-stu-id="786af-132">You can't change hello Sync Metadata Database, its name, or its service level without dropping it.</span></span>

        <span data-ttu-id="786af-133">Если вы выбрали параметр **Новая база данных**, щелкните **Создать новую базу данных**.</span><span class="sxs-lookup"><span data-stu-id="786af-133">If you chose **New database**, select **Create new database.**</span></span> <span data-ttu-id="786af-134">Hello **базы данных SQL** открывает колонку.</span><span class="sxs-lookup"><span data-stu-id="786af-134">hello **SQL Database** blade opens.</span></span> <span data-ttu-id="786af-135">На hello **базы данных SQL** колонки, задайте имя и настройте новую базу данных hello.</span><span class="sxs-lookup"><span data-stu-id="786af-135">On hello **SQL Database** blade, name and configure hello new database.</span></span> <span data-ttu-id="786af-136">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="786af-136">Then select **OK**.</span></span>

        <span data-ttu-id="786af-137">Если вы выбрали **использовать существующую базу данных**выберите hello базы данных из списка hello.</span><span class="sxs-lookup"><span data-stu-id="786af-137">If you chose **Use existing database**, select hello database from hello list.</span></span>

    3.  <span data-ttu-id="786af-138">В hello **автоматическая синхронизация** сначала выберите **на** или **Off**.</span><span class="sxs-lookup"><span data-stu-id="786af-138">In hello **Automatic Sync** section, first select **On** or **Off**.</span></span>

        <span data-ttu-id="786af-139">Если вы выбрали **на**, в hello **частота синхронизации** , введите число и выберите в секундах, минутах, часах или днях.</span><span class="sxs-lookup"><span data-stu-id="786af-139">If you chose **On**, in hello **Sync Frequency** section, enter a number and select Seconds, Minutes, Hours, or Days.</span></span>

        ![Указание частоты синхронизации](media/sql-database-get-started-sql-data-sync/datasync-preview-syncfreq.png)

    4.  <span data-ttu-id="786af-141">В hello **разрешения конфликтов** выберите «Приоритет концентратора» или «Значению члена».</span><span class="sxs-lookup"><span data-stu-id="786af-141">In hello **Conflict Resolution** section, select "Hub wins" or "Member wins."</span></span>

        ![Настройка устранения конфликтов](media/sql-database-get-started-sql-data-sync/datasync-preview-conflictres.png)

    5.  <span data-ttu-id="786af-143">Выберите **ОК** и дождитесь hello новый синхронизации группы toobe создан и развернут.</span><span class="sxs-lookup"><span data-stu-id="786af-143">Select **OK** and wait for hello new sync group toobe created and deployed.</span></span>

## <a name="step-2---add-sync-members"></a><span data-ttu-id="786af-144">Шаг 2. Добавление членов синхронизации</span><span class="sxs-lookup"><span data-stu-id="786af-144">Step 2 - Add sync members</span></span>

<span data-ttu-id="786af-145">После создания и развертывания, шаг 2 новых групп синхронизации hello **добавить участников синхронизации**, выделяется в hello **новых групп синхронизации** колонку.</span><span class="sxs-lookup"><span data-stu-id="786af-145">After hello new sync group is created and deployed, Step 2, **Add sync members**, is highlighted in hello **New sync group** blade.</span></span>

<span data-ttu-id="786af-146">В hello **базы данных-концентратора** введите учетные данные существующего hello для hello базы данных SQL сервера, на какие hello базы данных-концентратора.</span><span class="sxs-lookup"><span data-stu-id="786af-146">In hello **Hub Database** section, enter hello existing credentials for hello SQL Database server on which hello hub database is located.</span></span> <span data-ttu-id="786af-147">Не вводите *новые* учетные данные в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="786af-147">Don't enter *new* credentials in this section.</span></span>

![Добавлена база данных концентратора, группу toosync](media/sql-database-get-started-sql-data-sync/datasync-preview-hubadded.png)

## <a name="add-an-azure-sql-database"></a><span data-ttu-id="786af-149">Добавление базы данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="786af-149">Add an Azure SQL Database</span></span>

<span data-ttu-id="786af-150">В hello **база данных-участник** статьи, при необходимости добавьте к группе синхронизации toohello базы данных SQL Azure, выбрав **добавления базы данных Azure**.</span><span class="sxs-lookup"><span data-stu-id="786af-150">In hello **Member Database** section, optionally add an Azure SQL Database toohello sync group by selecting **Add an Azure Database**.</span></span> <span data-ttu-id="786af-151">Hello **Настройка базы данных Azure** открывает колонку.</span><span class="sxs-lookup"><span data-stu-id="786af-151">hello **Configure Azure Database** blade opens.</span></span>

<span data-ttu-id="786af-152">На hello **Настройка базы данных Azure** колонке hello следующие действия:</span><span class="sxs-lookup"><span data-stu-id="786af-152">On hello **Configure Azure Database** blade, do hello following things:</span></span>

1.  <span data-ttu-id="786af-153">В hello **имя члена синхронизации** укажите имя для нового участника синхронизации hello.</span><span class="sxs-lookup"><span data-stu-id="786af-153">In hello **Sync Member Name** field, provide a name for hello new sync member.</span></span> <span data-ttu-id="786af-154">Данное имя отличается от имени hello самой базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="786af-154">This name is distinct from hello name of hello database itself.</span></span>

2.  <span data-ttu-id="786af-155">В hello **подписки** hello выберите связанные подписки Azure для выставления.</span><span class="sxs-lookup"><span data-stu-id="786af-155">In hello **Subscription** field, select hello associated Azure subscription for billing purposes.</span></span>

3.  <span data-ttu-id="786af-156">В hello **Azure SQL Server** hello выберите существующий сервер базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="786af-156">In hello **Azure SQL Server** field, select hello existing SQL database server.</span></span>

4.  <span data-ttu-id="786af-157">В hello **базы данных SQL Azure** hello выберите существующую базу данных SQL.</span><span class="sxs-lookup"><span data-stu-id="786af-157">In hello **Azure SQL Database** field, select hello existing SQL database.</span></span>

5.  <span data-ttu-id="786af-158">В hello **направления синхронизации** выберите двусторонней синхронизации, toohello концентратора, или из hello концентратора.</span><span class="sxs-lookup"><span data-stu-id="786af-158">In hello **Sync Directions** field, select Bi-directional Sync, toohello Hub, or From hello Hub.</span></span>

    ![Добавление нового члена синхронизации для базы данных SQL](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadding.png)

6.  <span data-ttu-id="786af-160">В hello **Username** и **пароль** введите hello существующие учетные данные для hello базы данных SQL server, на какие hello расположена база данных-участник.</span><span class="sxs-lookup"><span data-stu-id="786af-160">In hello **Username** and **Password** fields, enter hello existing credentials for hello SQL Database server on which hello member database is located.</span></span> <span data-ttu-id="786af-161">Не вводите *новые* учетные данные в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="786af-161">Don't enter *new* credentials in this section.</span></span>

7.  <span data-ttu-id="786af-162">Выберите **ОК** и дождитесь hello новый синхронизации член toobe создан и развернут.</span><span class="sxs-lookup"><span data-stu-id="786af-162">Select **OK** and wait for hello new sync member toobe created and deployed.</span></span>

    ![Добавлен новый член синхронизации для базы данных SQL](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadded.png)

## <a name="add-an-on-premises-sql-server-database"></a><span data-ttu-id="786af-164">Добавление локальной базы данных SQL Server</span><span class="sxs-lookup"><span data-stu-id="786af-164">Add an on-premises SQL Server database</span></span>

<span data-ttu-id="786af-165">В hello **база данных-участник** статьи, при необходимости добавьте к группе синхронизации локальной toohello SQL Server, выбрав **добавления базы данных локального**.</span><span class="sxs-lookup"><span data-stu-id="786af-165">In hello **Member Database** section, optionally add an on-premises SQL Server toohello sync group by selecting **Add an On-Premises Database**.</span></span> <span data-ttu-id="786af-166">Hello **Настройка локальной** открывает колонку.</span><span class="sxs-lookup"><span data-stu-id="786af-166">hello **Configure On-Premises** blade opens.</span></span>

<span data-ttu-id="786af-167">На hello **Настройка локальной** колонке hello следующие действия:</span><span class="sxs-lookup"><span data-stu-id="786af-167">On hello **Configure On-Premises** blade, do hello following things:</span></span>

1.  <span data-ttu-id="786af-168">Выберите **hello Выбор шлюза агента синхронизации**.</span><span class="sxs-lookup"><span data-stu-id="786af-168">Select **Choose hello Sync Agent Gateway**.</span></span> <span data-ttu-id="786af-169">Hello **выберите агент синхронизации** открывает колонку.</span><span class="sxs-lookup"><span data-stu-id="786af-169">hello **Select Sync Agent** blade opens.</span></span>

    ![Выберите шлюз агента синхронизации hello](media/sql-database-get-started-sql-data-sync/datasync-preview-choosegateway.png)

2.  <span data-ttu-id="786af-171">На hello **hello Выбор шлюза агента синхронизации** колонке выберите ли toouse существующего агента или создать новый агент.</span><span class="sxs-lookup"><span data-stu-id="786af-171">On hello **Choose hello Sync Agent Gateway** blade, choose whether toouse an existing agent or create a new agent.</span></span>

    <span data-ttu-id="786af-172">Если вы выбрали **существующие агенты**, выберите hello существующий агент из списка hello.</span><span class="sxs-lookup"><span data-stu-id="786af-172">If you chose **Existing agents**, select hello existing agent from hello list.</span></span>

    <span data-ttu-id="786af-173">Если вы выбрали **создайте новый агент**, hello следующие действия:</span><span class="sxs-lookup"><span data-stu-id="786af-173">If you chose **Create a new agent**, do hello following things:</span></span>

    1.  <span data-ttu-id="786af-174">Загрузите программное обеспечение агента синхронизации клиента hello по ссылке hello и установить его на компьютере hello, где находится hello SQL Server.</span><span class="sxs-lookup"><span data-stu-id="786af-174">Download hello client sync agent software from hello link provided and install it on hello computer where hello SQL Server is located.</span></span>
 
        > [!IMPORTANT]
        > <span data-ttu-id="786af-175">У вас есть tooopen исходящих TCP-порт 1433 hello брандмауэра toolet hello клиентского агента в связи с сервером hello.</span><span class="sxs-lookup"><span data-stu-id="786af-175">You have tooopen outbound TCP port 1433 in hello firewall toolet hello client agent communicate with hello server.</span></span>


    2.  <span data-ttu-id="786af-176">Введите имя для hello агента.</span><span class="sxs-lookup"><span data-stu-id="786af-176">Enter a name for hello agent.</span></span>

    3.  <span data-ttu-id="786af-177">Выберите **Создание и генерация ключа**.</span><span class="sxs-lookup"><span data-stu-id="786af-177">Select **Create and Generate Key**.</span></span>

    4.  <span data-ttu-id="786af-178">Копировать буфер toohello ключа агента hello.</span><span class="sxs-lookup"><span data-stu-id="786af-178">Copy hello agent key toohello clipboard.</span></span>
        
        ![Создание агента синхронизации](media/sql-database-get-started-sql-data-sync/datasync-preview-selectsyncagent.png)

    5.  <span data-ttu-id="786af-180">Выберите **ОК** tooclose hello **выберите агент синхронизации** колонку.</span><span class="sxs-lookup"><span data-stu-id="786af-180">Select **OK** tooclose hello **Select Sync Agent** blade.</span></span>

    6.  <span data-ttu-id="786af-181">На компьютере SQL Server hello найдите и запустите приложение hello агент синхронизации клиента.</span><span class="sxs-lookup"><span data-stu-id="786af-181">On hello SQL Server computer, locate and run hello Client Sync Agent app.</span></span>

        ![клиентское приложение агента синхронизации данных Hello](media/sql-database-get-started-sql-data-sync/datasync-preview-clientagent.png)

    7.  <span data-ttu-id="786af-183">В приложении агента синхронизации hello выберите **отправить ключ агента**.</span><span class="sxs-lookup"><span data-stu-id="786af-183">In hello sync agent app, select **Submit Agent Key**.</span></span> <span data-ttu-id="786af-184">Hello **синхронизации метаданных базы данных конфигурации** откроется диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="786af-184">hello **Sync Metadata Database Configuration** dialog box opens.</span></span>

    8.  <span data-ttu-id="786af-185">В hello **синхронизации метаданных базы данных конфигурации** диалоговое окно, вставить в ключ агента hello, скопированные из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="786af-185">In hello **Sync Metadata Database Configuration** dialog box, paste in hello agent key copied from hello Azure portal.</span></span> <span data-ttu-id="786af-186">Также предоставляют hello существующие учетные данные для сервера базы данных SQL Azure hello, на какие hello находится база данных метаданных.</span><span class="sxs-lookup"><span data-stu-id="786af-186">Also provide hello existing credentials for hello Azure SQL Database server on which hello metadata database is located.</span></span> <span data-ttu-id="786af-187">(Если вы создали новую базу данных метаданных, это база данных находится на hello сервере базы данных-концентратора hello.) Выберите **ОК** и дождитесь toofinish конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="786af-187">(If you created a new metadata database, this database is on hello same server as hello hub database.) Select **OK** and wait for hello configuration toofinish.</span></span>

        ![Введите учетные данные ключа и сервера агента hello](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-enterkey.png)

        >   [!NOTE] 
        >   <span data-ttu-id="786af-189">Если возникли ошибка брандмауэра на этом этапе у вас есть toocreate правило брандмауэра Azure tooallow входящего трафика с компьютера SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="786af-189">If you get a firewall error at this point, you have toocreate a firewall rule on Azure tooallow incoming traffic from hello SQL Server computer.</span></span> <span data-ttu-id="786af-190">Можно создать правило hello вручную на портале hello, но может оказаться проще toocreate его в SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="786af-190">You can create hello rule manually in hello portal, but you may find it easier toocreate it in SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="786af-191">В среде SSMS попробуйте tooconnect toohello концентратора и база данных в Azure.</span><span class="sxs-lookup"><span data-stu-id="786af-191">In SSMS, try tooconnect toohello hub database on Azure.</span></span> <span data-ttu-id="786af-192">Введите ее имя как \<имя_центральной_базы_данных\>.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="786af-192">Enter its name as \<hub_database_name\>.database.windows.net.</span></span> <span data-ttu-id="786af-193">Следуйте указаниям hello hello hello диалогового окна поле tooconfigure правило брандмауэра Azure.</span><span class="sxs-lookup"><span data-stu-id="786af-193">Follow hello steps in hello dialog box tooconfigure hello Azure firewall rule.</span></span> <span data-ttu-id="786af-194">После этого вернитесь toohello клиентский агент синхронизации приложения.</span><span class="sxs-lookup"><span data-stu-id="786af-194">Then return toohello Client Sync Agent app.</span></span>

    9.  <span data-ttu-id="786af-195">В приложение hello агент синхронизации клиента, щелкните **зарегистрировать** tooregister базы данных SQL Server с агентом hello.</span><span class="sxs-lookup"><span data-stu-id="786af-195">In hello Client Sync Agent app, click **Register** tooregister a SQL Server database with hello agent.</span></span> <span data-ttu-id="786af-196">Hello **конфигурация SQL Server** откроется диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="786af-196">hello **SQL Server Configuration** dialog box opens.</span></span>

        ![Добавление и настройка базы данных SQL Server](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-adddb.png)

    10. <span data-ttu-id="786af-198">В hello **конфигурация SQL Server** диалогового окна выберите ли tooconnect с помощью проверки подлинности SQL Server или проверка подлинности Windows.</span><span class="sxs-lookup"><span data-stu-id="786af-198">In hello **SQL Server Configuration** dialog box, choose whether tooconnect by using SQL Server authentication or Windows authentication.</span></span> <span data-ttu-id="786af-199">Если выбрана проверка подлинности SQL Server, введите учетные данные существующего hello.</span><span class="sxs-lookup"><span data-stu-id="786af-199">If you chose SQL Server authentication, enter hello existing credentials.</span></span> <span data-ttu-id="786af-200">Укажите имена SQL Server hello и hello hello базы данных, в которое следует toosync.</span><span class="sxs-lookup"><span data-stu-id="786af-200">Provide hello SQL Server name and hello name of hello database that you want toosync.</span></span> <span data-ttu-id="786af-201">Выберите **Проверка соединения** tootest параметры.</span><span class="sxs-lookup"><span data-stu-id="786af-201">Select **Test connection** tootest your settings.</span></span> <span data-ttu-id="786af-202">Затем нажмите кнопку **Save** (Сохранить).</span><span class="sxs-lookup"><span data-stu-id="786af-202">Then select **Save**.</span></span> <span data-ttu-id="786af-203">Hello зарегистрированной базы данных отображается в списке hello.</span><span class="sxs-lookup"><span data-stu-id="786af-203">hello registered database appears in hello list.</span></span>

        ![База данных SQL Server зарегистрирована](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-dbadded.png)

    11. <span data-ttu-id="786af-205">Теперь можно закрыть приложение hello агент синхронизации клиента.</span><span class="sxs-lookup"><span data-stu-id="786af-205">You can now close hello Client Sync Agent app.</span></span>

    12. <span data-ttu-id="786af-206">На hello hello портала **Настройка локальной** колонке выберите **выберите hello базы данных.**</span><span class="sxs-lookup"><span data-stu-id="786af-206">In hello portal, on hello **Configure On-Premises** blade, select **Select hello Database.**</span></span> <span data-ttu-id="786af-207">Hello **Выбор базы данных** открывает колонку.</span><span class="sxs-lookup"><span data-stu-id="786af-207">hello **Select Database** blade opens.</span></span>

    13. <span data-ttu-id="786af-208">На hello **Выбор базы данных** колонки в hello **имя члена синхронизации** укажите имя для нового участника синхронизации hello.</span><span class="sxs-lookup"><span data-stu-id="786af-208">On hello **Select Database** blade, in hello **Sync Member Name** field, provide a name for hello new sync member.</span></span> <span data-ttu-id="786af-209">Данное имя отличается от имени hello самой базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="786af-209">This name is distinct from hello name of hello database itself.</span></span> <span data-ttu-id="786af-210">Выберите базу данных hello из списка hello.</span><span class="sxs-lookup"><span data-stu-id="786af-210">Select hello database from hello list.</span></span> <span data-ttu-id="786af-211">В hello **направления синхронизации** выберите двусторонней синхронизации, toohello концентратора, или из hello концентратора.</span><span class="sxs-lookup"><span data-stu-id="786af-211">In hello **Sync Directions** field, select Bi-directional Sync, toohello Hub, or From hello Hub.</span></span>

        ![Выберите hello в локальную базу данных](media/sql-database-get-started-sql-data-sync/datasync-preview-selectdb.png)

    14. <span data-ttu-id="786af-213">Выберите **ОК** tooclose hello **Выбор базы данных** колонку.</span><span class="sxs-lookup"><span data-stu-id="786af-213">Select **OK** tooclose hello **Select Database** blade.</span></span> <span data-ttu-id="786af-214">Выберите **ОК** tooclose hello **Настройка локальной** колонки и ожидания hello новые синхронизации toobe член создан и развернут.</span><span class="sxs-lookup"><span data-stu-id="786af-214">Then select **OK** tooclose hello **Configure On-Premises** blade and wait for hello new sync member toobe created and deployed.</span></span> <span data-ttu-id="786af-215">Наконец, нажмите кнопку **ОК** tooclose hello **выбрать элементы синхронизации** колонку.</span><span class="sxs-lookup"><span data-stu-id="786af-215">Finally, click **OK** tooclose hello **Select sync members** blade.</span></span>

        ![На локальную базу данных, добавленные toosync группы](media/sql-database-get-started-sql-data-sync/datasync-preview-onpremadded.png)

3.  <span data-ttu-id="786af-217">tooconnect tooSQL Data Sync и hello локальный агент, добавьте вашей роли пользователя имя toohello `DataSync_Executor`.</span><span class="sxs-lookup"><span data-stu-id="786af-217">tooconnect tooSQL Data Sync and hello local agent, add your user name toohello role `DataSync_Executor`.</span></span> <span data-ttu-id="786af-218">Синхронизация данных создает эту роль на экземпляре SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="786af-218">Data Sync creates this role on hello SQL Server instance.</span></span>

## <a name="step-3---configure-sync-group"></a><span data-ttu-id="786af-219">Шаг 3. Настройка группы синхронизации</span><span class="sxs-lookup"><span data-stu-id="786af-219">Step 3 - Configure sync group</span></span>

<span data-ttu-id="786af-220">После создания и развертывания, шаг 3 hello новым участникам группы синхронизации **Настройка группы синхронизации**, выделяется в hello **новых групп синхронизации** колонку.</span><span class="sxs-lookup"><span data-stu-id="786af-220">After hello new sync group members are created and deployed, Step 3, **Configure sync group**, is highlighted in hello **New sync group** blade.</span></span>

1.  <span data-ttu-id="786af-221">На hello **таблиц** колонке выберите базу данных из списка hello синхронизации членов группы, а затем выберите **обновление схемы**.</span><span class="sxs-lookup"><span data-stu-id="786af-221">On hello **Tables** blade, select a database from hello list of sync group members, and then select **Refresh schema**.</span></span>

2.  <span data-ttu-id="786af-222">Из списка доступных таблиц hello выберите hello таблиц, которые должны toosync.</span><span class="sxs-lookup"><span data-stu-id="786af-222">From hello list of available tables, select hello tables that you want toosync.</span></span>

    ![Выберите таблицы toosync](media/sql-database-get-started-sql-data-sync/datasync-preview-tables.png)

3.  <span data-ttu-id="786af-224">По умолчанию выбраны все столбцы в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="786af-224">By default, all columns in hello table are selected.</span></span> <span data-ttu-id="786af-225">Если вы не хотите toosync все столбцы hello, отключите hello флажки для столбцов hello, что вы не хотите toosync.</span><span class="sxs-lookup"><span data-stu-id="786af-225">If you don't want toosync all hello columns, disable hello checkbox for hello columns that you don't want toosync.</span></span> <span data-ttu-id="786af-226">Убедитесь, что выбран tooleave hello первичного ключевого столбца.</span><span class="sxs-lookup"><span data-stu-id="786af-226">Be sure tooleave hello primary key column selected.</span></span>

    ![Выбор полей toosync](media/sql-database-get-started-sql-data-sync/datasync-preview-tables2.png)

4.  <span data-ttu-id="786af-228">Наконец, щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="786af-228">Finally, select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="786af-229">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="786af-229">Next steps</span></span>
<span data-ttu-id="786af-230">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="786af-230">Congratulations.</span></span> <span data-ttu-id="786af-231">Вы создали группу синхронизации, которая включает и экземпляр базы данных SQL, и базу данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="786af-231">You have created a sync group that includes both a SQL Database instance and a SQL Server database.</span></span>

<span data-ttu-id="786af-232">Дополнительные сведения о базе данных SQL и синхронизации данных SQL:</span><span class="sxs-lookup"><span data-stu-id="786af-232">For more info about SQL Database and SQL Data Sync, see:</span></span>

-   [<span data-ttu-id="786af-233">Загрузите hello технической документации завершения синхронизации данных SQL</span><span class="sxs-lookup"><span data-stu-id="786af-233">Download hello complete SQL Data Sync technical documentation</span></span>](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true)
-   [<span data-ttu-id="786af-234">Загрузить документацию по API REST для синхронизации данных SQL hello</span><span class="sxs-lookup"><span data-stu-id="786af-234">Download hello SQL Data Sync REST API documentation</span></span>](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_REST_API.pdf?raw=true)
-   [<span data-ttu-id="786af-235">Обзор Базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="786af-235">SQL Database Overview</span></span>](sql-database-technical-overview.md)
-   [<span data-ttu-id="786af-236">Управление жизненным циклом базы данных</span><span class="sxs-lookup"><span data-stu-id="786af-236">Database Lifecycle Management</span></span>](https://msdn.microsoft.com/library/jj907294.aspx)
