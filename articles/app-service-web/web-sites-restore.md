---
title: "aaaRestore приложения в Azure"
description: "Узнайте, как toorestore приложения из резервной копии."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 4444dbf7-363c-47e2-b24a-dbd45cb08491
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: 4b54029a9197064f990f29a3c4558c8322668714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-app-in-azure"></a><span data-ttu-id="ceb01-103">Восстановление приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="ceb01-103">Restore an app in Azure</span></span>
<span data-ttu-id="ceb01-104">В этой статье показано, как toorestore приложения в [службе приложений Azure](../app-service/app-service-value-prop-what-is.md) , вы уже создали резервные копии (см. [резервное копирование приложения в Azure](web-sites-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="ceb01-104">This article shows you how toorestore an app in [Azure App Service](../app-service/app-service-value-prop-what-is.md) that you have previously backed up (see [Back up your app in Azure](web-sites-backup.md)).</span></span> <span data-ttu-id="ceb01-105">Восстановите приложение с предыдущего состояния tooa по требованию привязанных баз данных или создайте новое приложение на основе одного из резервной копии исходного приложения.</span><span class="sxs-lookup"><span data-stu-id="ceb01-105">You can restore your app with its linked databases on-demand tooa previous state, or create a new app based on one of your original app's backup.</span></span> <span data-ttu-id="ceb01-106">Служба приложений Azure поддерживает следующие базы данных для резервного копирования и восстановления hello:</span><span class="sxs-lookup"><span data-stu-id="ceb01-106">Azure App Service supports hello following databases for backup and restore:</span></span>
- [<span data-ttu-id="ceb01-107">База данных SQL</span><span class="sxs-lookup"><span data-stu-id="ceb01-107">SQL Database</span></span>](https://azure.microsoft.com/en-us/services/sql-database/)
- <span data-ttu-id="ceb01-108">[база данных Azure для MySQL (предварительная версия)](https://azure.microsoft.com/en-us/services/mysql);</span><span class="sxs-lookup"><span data-stu-id="ceb01-108">[Azure Database for MySQL (Preview)](https://azure.microsoft.com/en-us/services/mysql)</span></span>
- <span data-ttu-id="ceb01-109">[база данных Azure для PostgreSQL (предварительная версия)](https://azure.microsoft.com/en-us/services/postgres);</span><span class="sxs-lookup"><span data-stu-id="ceb01-109">[Azure Database for PostgreSQL (Preview)](https://azure.microsoft.com/en-us/services/postgres)</span></span>
- <span data-ttu-id="ceb01-110">[ClearDB MySQL](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview);</span><span class="sxs-lookup"><span data-stu-id="ceb01-110">[ClearDB MySQL](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)</span></span>
- <span data-ttu-id="ceb01-111">[MySQL в приложении](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app).</span><span class="sxs-lookup"><span data-stu-id="ceb01-111">[MySQL in-app](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)</span></span>

<span data-ttu-id="ceb01-112">Восстановление из резервных копий является доступной tooapps в **Стандартная** и **Premium** уровня.</span><span class="sxs-lookup"><span data-stu-id="ceb01-112">Restoring from backups is available tooapps running in **Standard** and **Premium** tier.</span></span> <span data-ttu-id="ceb01-113">Дополнительные сведения об увеличении масштаба приложения см. в статье [Увеличение масштаба приложения в Azure](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="ceb01-113">For information about scaling up your app, see [Scale up an app in Azure](web-sites-scale.md).</span></span> <span data-ttu-id="ceb01-114">**Premium** уровня позволяет большего количества ежедневных резервных копий toobe, выполнить чем **Стандартная** уровня.</span><span class="sxs-lookup"><span data-stu-id="ceb01-114">**Premium** tier allows a greater number of daily backups toobe performed than **Standard** tier.</span></span>

<a name="PreviousBackup"></a>

## <a name="restore-an-app-from-an-existing-backup"></a><span data-ttu-id="ceb01-115">Восстановление приложения из существующей резервной копии</span><span class="sxs-lookup"><span data-stu-id="ceb01-115">Restore an app from an existing backup</span></span>
1. <span data-ttu-id="ceb01-116">На hello **параметры** колонке приложения в hello портала Azure щелкните **резервные копии** toodisplay hello **резервные копии** колонку.</span><span class="sxs-lookup"><span data-stu-id="ceb01-116">On hello **Settings** blade of your app in hello Azure Portal, click **Backups** toodisplay hello **Backups** blade.</span></span> <span data-ttu-id="ceb01-117">Затем щелкните **Восстановить**.</span><span class="sxs-lookup"><span data-stu-id="ceb01-117">Then click **Restore**.</span></span>
   
    ![Выбор команды "Восстановить сейчас"][ChooseRestoreNow]
2. <span data-ttu-id="ceb01-119">В hello **восстановить** колонки, первый источник резервного копирования выберите hello.</span><span class="sxs-lookup"><span data-stu-id="ceb01-119">In hello **Restore** blade, first select hello backup source.</span></span>
   
    ![](./media/web-sites-restore/021ChooseSource1.png)
   
    <span data-ttu-id="ceb01-120">Hello **приложение резервного копирования** на экране отображается все существующие резервные копии текущее приложение hello Здравствуйте, и вы можете легко выбрать один.</span><span class="sxs-lookup"><span data-stu-id="ceb01-120">hello **App backup** option shows you all hello existing backups of hello current app, and you can easily select one.</span></span>
    <span data-ttu-id="ceb01-121">Hello **хранения** параметр позволяет выбрать любой резервной копии ZIP-файл из существующей учетной записи хранилища Azure и контейнер в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="ceb01-121">hello **Storage** option lets you select any backup ZIP file from any existing Azure Storage account and container in your subscription.</span></span>
    <span data-ttu-id="ceb01-122">Если вы пытаетесь toorestore резервной копии другое приложение, используйте hello **хранения** параметр.</span><span class="sxs-lookup"><span data-stu-id="ceb01-122">If you're trying toorestore a backup of another app, use hello **Storage** option.</span></span>
3. <span data-ttu-id="ceb01-123">Укажите назначение hello для восстановления приложения hello в **назначения для восстановления**.</span><span class="sxs-lookup"><span data-stu-id="ceb01-123">Then, specify hello destination for hello app restore in **Restore destination**.</span></span>
   
    ![](./media/web-sites-restore/022ChooseDestination1.png)
   
   > [!WARNING]
   > <span data-ttu-id="ceb01-124">Если вы выберете **Перезаписать**, то все существующие данные в текущем приложении будут удалены и перезаписаны.</span><span class="sxs-lookup"><span data-stu-id="ceb01-124">If you choose **Overwrite**, all existing data in your current app is erased and overwritten.</span></span> <span data-ttu-id="ceb01-125">Прежде чем нажимать кнопку **ОК**, убедитесь, что это именно вы хотите toodo.</span><span class="sxs-lookup"><span data-stu-id="ceb01-125">Before you click **OK**, make sure that it is exactly what you want toodo.</span></span>
   > 
   > 
   
    <span data-ttu-id="ceb01-126">Можно выбрать **существующего приложения** toorestore приложение резервного копирования tooanother приложения hello в hello одной группе ресурс.</span><span class="sxs-lookup"><span data-stu-id="ceb01-126">You can select **Existing App** toorestore hello app backup tooanother app in hello same resoure group.</span></span> <span data-ttu-id="ceb01-127">Прежде чем использовать этот параметр, необходимо другое приложение, уже созданных в группе ресурсов с зеркальным отображением базы данных конфигурации toohello один определенный в резервную копию приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ceb01-127">Before you use this option, you should have already created another app in your resource group with mirroring database configuration toohello one defined in hello app backup.</span></span> <span data-ttu-id="ceb01-128">Можно также создать **New** toorestore приложения содержимого.</span><span class="sxs-lookup"><span data-stu-id="ceb01-128">You can also Create a **New** app toorestore your content to.</span></span>

4. <span data-ttu-id="ceb01-129">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ceb01-129">Click **OK**.</span></span>

<a name="StorageAccount"></a>

## <a name="download-or-delete-a-backup-from-a-storage-account"></a><span data-ttu-id="ceb01-130">Скачивание и удаление резервной копии в учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="ceb01-130">Download or delete a backup from a storage account</span></span>
1. <span data-ttu-id="ceb01-131">Из основной hello **Обзор** колонке hello Azure portal, **учетные записи хранения**.</span><span class="sxs-lookup"><span data-stu-id="ceb01-131">From hello main **Browse** blade of hello Azure portal, select **Storage accounts**.</span></span> <span data-ttu-id="ceb01-132">Откроется список существующих учетных записей хранения.</span><span class="sxs-lookup"><span data-stu-id="ceb01-132">A list of your existing storage accounts is displayed.</span></span>
2. <span data-ttu-id="ceb01-133">Выберите учетную запись хранения hello, содержащий резервную копию hello требуется берется колонке toodownload или delete.hello для учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="ceb01-133">Select hello storage account that contains hello backup that you want toodownload or delete.hello blade for hello storage account is displayed.</span></span>
3. <span data-ttu-id="ceb01-134">В колонке учетной записи хранилища hello выберите hello контейнера</span><span class="sxs-lookup"><span data-stu-id="ceb01-134">In hello storage account blade, select hello container you want</span></span>
   
    ![Просмотр контейнеров][ViewContainers]
4. <span data-ttu-id="ceb01-136">Выберите файл резервной копии, которые вы желаете toodownload или удалить.</span><span class="sxs-lookup"><span data-stu-id="ceb01-136">Select backup file you want toodownload or delete.</span></span>
   
    ![ViewContainers](./media/web-sites-restore/03ViewFiles.png)
5. <span data-ttu-id="ceb01-138">Нажмите кнопку **загрузки** или **удалить** в зависимости от того, что вы хотите toodo.</span><span class="sxs-lookup"><span data-stu-id="ceb01-138">Click **Download** or **Delete** depending on what you want toodo.</span></span>  

<a name="OperationLogs"></a>

## <a name="monitor-a-restore-operation"></a><span data-ttu-id="ceb01-139">Мониторинг операции восстановления</span><span class="sxs-lookup"><span data-stu-id="ceb01-139">Monitor a restore operation</span></span>
<span data-ttu-id="ceb01-140">toosee сведения об успешности hello операции восстановления приложения hello, перейдите toohello **журнал действий** колонки в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ceb01-140">toosee details about hello success or failure of hello app restore operation, navigate toohello **Activity Log** blade in hello Azure portal.</span></span>  
 

<span data-ttu-id="ceb01-141">Прокрутите вниз toofind hello требуемого восстановления операции и нажмите кнопку tooselect его.</span><span class="sxs-lookup"><span data-stu-id="ceb01-141">Scroll down toofind hello desired restore operation and click tooselect it.</span></span>

<span data-ttu-id="ceb01-142">Hello сведения колонке отображает hello доступные данные, относящиеся toohello операции восстановления.</span><span class="sxs-lookup"><span data-stu-id="ceb01-142">hello details blade displays hello available information related toohello restore operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ceb01-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ceb01-143">Next Steps</span></span>
<span data-ttu-id="ceb01-144">Выполнять резервное копирование и восстановление приложения служб приложений с помощью REST API (см. [tooback REST, используйте копирование и восстановление приложения служб приложений](websites-csm-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="ceb01-144">You can backup and restore App Service apps using REST API (see [Use REST tooback up and restore App Service apps](websites-csm-backup.md)).</span></span>


<!-- IMAGES -->
[ChooseRestoreNow]: ./media/web-sites-restore/02ChooseRestoreNow1.png
[ViewContainers]: ./media/web-sites-restore/03ViewContainers.png
[StorageAccountFile]: ./media/web-sites-restore/02StorageAccountFile.png
[BrowseCloudStorage]: ./media/web-sites-restore/03BrowseCloudStorage.png
[StorageAccountFileSelected]: ./media/web-sites-restore/04StorageAccountFileSelected.png
[ChooseRestoreSettings]: ./media/web-sites-restore/05ChooseRestoreSettings.png
[ChooseDBServer]: ./media/web-sites-restore/06ChooseDBServer.png
[RestoreToNewSQLDB]: ./media/web-sites-restore/07RestoreToNewSQLDB.png
[NewSQLDBConfig]: ./media/web-sites-restore/08NewSQLDBConfig.png
[RestoredContosoWebSite]: ./media/web-sites-restore/09RestoredContosoWebSite.png
[DashboardOperationLogsLink]: ./media/web-sites-restore/10DashboardOperationLogsLink.png
[ManagementServicesOperationLogsList]: ./media/web-sites-restore/11ManagementServicesOperationLogsList.png
[DetailsButton]: ./media/web-sites-restore/12DetailsButton.png
[OperationDetails]: ./media/web-sites-restore/13OperationDetails.png
