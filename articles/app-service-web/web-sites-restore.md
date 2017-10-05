---
title: "Восстановление приложения в Azure"
description: "Узнайте, как восстановить приложение из резервной копии."
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
ms.openlocfilehash: 5fe74d992edb7028fa4a2500e427013d98ebc250
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="restore-an-app-in-azure"></a><span data-ttu-id="752b8-103">Восстановление приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="752b8-103">Restore an app in Azure</span></span>
<span data-ttu-id="752b8-104">В этой статье описывается, как в [службе приложений Azure](../app-service/app-service-value-prop-what-is.md) восстановить приложение, для которого ранее была создана резервная копия (ознакомьтесь с [архивацией приложения в Azure](web-sites-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="752b8-104">This article shows you how to restore an app in [Azure App Service](../app-service/app-service-value-prop-what-is.md) that you have previously backed up (see [Back up your app in Azure](web-sites-backup.md)).</span></span> <span data-ttu-id="752b8-105">Вы можете восстановить предыдущее состояние приложения и связанных с ним баз данных по запросу или создать новое приложение на основе одной из резервных копий исходного приложения.</span><span class="sxs-lookup"><span data-stu-id="752b8-105">You can restore your app with its linked databases on-demand to a previous state, or create a new app based on one of your original app's backup.</span></span> <span data-ttu-id="752b8-106">Служба приложений Azure поддерживает следующие базы данных для архивации и восстановления:</span><span class="sxs-lookup"><span data-stu-id="752b8-106">Azure App Service supports the following databases for backup and restore:</span></span>
- [<span data-ttu-id="752b8-107">База данных SQL</span><span class="sxs-lookup"><span data-stu-id="752b8-107">SQL Database</span></span>](https://azure.microsoft.com/en-us/services/sql-database/)
- <span data-ttu-id="752b8-108">[база данных Azure для MySQL (предварительная версия)](https://azure.microsoft.com/en-us/services/mysql);</span><span class="sxs-lookup"><span data-stu-id="752b8-108">[Azure Database for MySQL (Preview)](https://azure.microsoft.com/en-us/services/mysql)</span></span>
- <span data-ttu-id="752b8-109">[база данных Azure для PostgreSQL (предварительная версия)](https://azure.microsoft.com/en-us/services/postgres);</span><span class="sxs-lookup"><span data-stu-id="752b8-109">[Azure Database for PostgreSQL (Preview)](https://azure.microsoft.com/en-us/services/postgres)</span></span>
- <span data-ttu-id="752b8-110">[ClearDB MySQL](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview);</span><span class="sxs-lookup"><span data-stu-id="752b8-110">[ClearDB MySQL](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)</span></span>
- <span data-ttu-id="752b8-111">[MySQL в приложении](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app).</span><span class="sxs-lookup"><span data-stu-id="752b8-111">[MySQL in-app](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)</span></span>

<span data-ttu-id="752b8-112">Восстановление из резервных копий доступно для приложений, выполняемых на уровнях **Стандартный** и **Премиум**.</span><span class="sxs-lookup"><span data-stu-id="752b8-112">Restoring from backups is available to apps running in **Standard** and **Premium** tier.</span></span> <span data-ttu-id="752b8-113">Дополнительные сведения об увеличении масштаба приложения см. в статье [Увеличение масштаба приложения в Azure](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="752b8-113">For information about scaling up your app, see [Scale up an app in Azure](web-sites-scale.md).</span></span> <span data-ttu-id="752b8-114">Уровень **Премиум** позволяет создавать большее количество ежедневных резервных копий по сравнению с уровнем **Стандартный**.</span><span class="sxs-lookup"><span data-stu-id="752b8-114">**Premium** tier allows a greater number of daily backups to be performed than **Standard** tier.</span></span>

<a name="PreviousBackup"></a>

## <a name="restore-an-app-from-an-existing-backup"></a><span data-ttu-id="752b8-115">Восстановление приложения из существующей резервной копии</span><span class="sxs-lookup"><span data-stu-id="752b8-115">Restore an app from an existing backup</span></span>
1. <span data-ttu-id="752b8-116">На портале Azure в колонке **Параметры** своего приложения щелкните **Резервные копии**. Откроется колонка **Резервные копии**.</span><span class="sxs-lookup"><span data-stu-id="752b8-116">On the **Settings** blade of your app in the Azure Portal, click **Backups** to display the **Backups** blade.</span></span> <span data-ttu-id="752b8-117">Затем щелкните **Восстановить**.</span><span class="sxs-lookup"><span data-stu-id="752b8-117">Then click **Restore**.</span></span>
   
    ![Выбор команды "Восстановить сейчас"][ChooseRestoreNow]
2. <span data-ttu-id="752b8-119">В колонке **Восстановить** выберите источник резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="752b8-119">In the **Restore** blade, first select the backup source.</span></span>
   
    ![](./media/web-sites-restore/021ChooseSource1.png)
   
    <span data-ttu-id="752b8-120">Параметр **Архивная копия приложения** отображает все существующие резервные копии текущего приложения, позволяя легко выбрать одну из них.</span><span class="sxs-lookup"><span data-stu-id="752b8-120">The **App backup** option shows you all the existing backups of the current app, and you can easily select one.</span></span>
    <span data-ttu-id="752b8-121">Параметр **Служба хранилища** позволяет выбрать ZIP-файл любой резервной копии из любых имеющихся учетной записи хранения Azure и контейнера в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="752b8-121">The **Storage** option lets you select any backup ZIP file from any existing Azure Storage account and container in your subscription.</span></span>
    <span data-ttu-id="752b8-122">Если вы пытаетесь восстановить резервную копию другого приложения, используйте параметр **Служба хранилища** .</span><span class="sxs-lookup"><span data-stu-id="752b8-122">If you're trying to restore a backup of another app, use the **Storage** option.</span></span>
3. <span data-ttu-id="752b8-123">После этого укажите место назначения для восстановления приложения в разделе **Место назначения для восстановления**.</span><span class="sxs-lookup"><span data-stu-id="752b8-123">Then, specify the destination for the app restore in **Restore destination**.</span></span>
   
    ![](./media/web-sites-restore/022ChooseDestination1.png)
   
   > [!WARNING]
   > <span data-ttu-id="752b8-124">Если вы выберете **Перезаписать**, то все существующие данные в текущем приложении будут удалены и перезаписаны.</span><span class="sxs-lookup"><span data-stu-id="752b8-124">If you choose **Overwrite**, all existing data in your current app is erased and overwritten.</span></span> <span data-ttu-id="752b8-125">Прежде чем нажимать кнопку **ОК**, убедитесь, что это именно то, что вы хотите сделать.</span><span class="sxs-lookup"><span data-stu-id="752b8-125">Before you click **OK**, make sure that it is exactly what you want to do.</span></span>
   > 
   > 
   
    <span data-ttu-id="752b8-126">Вы также можете выбрать **Существующее приложение** для восстановления резервной копии приложения в другое приложение в той же группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="752b8-126">You can select **Existing App** to restore the app backup to another app in the same resoure group.</span></span> <span data-ttu-id="752b8-127">Прежде чем использовать этот параметр, необходимо создать другое приложение в группе ресурсов с конфигурацией базы данных, аналогичной конфигурации базы данных в резервной копии приложения.</span><span class="sxs-lookup"><span data-stu-id="752b8-127">Before you use this option, you should have already created another app in your resource group with mirroring database configuration to the one defined in the app backup.</span></span> <span data-ttu-id="752b8-128">Вы можете также **создать** приложение для восстановления содержимого.</span><span class="sxs-lookup"><span data-stu-id="752b8-128">You can also Create a **New** app to restore your content to.</span></span>

4. <span data-ttu-id="752b8-129">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="752b8-129">Click **OK**.</span></span>

<a name="StorageAccount"></a>

## <a name="download-or-delete-a-backup-from-a-storage-account"></a><span data-ttu-id="752b8-130">Скачивание и удаление резервной копии в учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="752b8-130">Download or delete a backup from a storage account</span></span>
1. <span data-ttu-id="752b8-131">На портале Azure в колонке **Обзор** выберите **Учетные записи хранения**.</span><span class="sxs-lookup"><span data-stu-id="752b8-131">From the main **Browse** blade of the Azure portal, select **Storage accounts**.</span></span> <span data-ttu-id="752b8-132">Откроется список существующих учетных записей хранения.</span><span class="sxs-lookup"><span data-stu-id="752b8-132">A list of your existing storage accounts is displayed.</span></span>
2. <span data-ttu-id="752b8-133">Выберите учетную запись, в которой хранится резервная копия, которую вы хотите скачать или удалить. Откроется колонка для учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="752b8-133">Select the storage account that contains the backup that you want to download or delete.The blade for the storage account is displayed.</span></span>
3. <span data-ttu-id="752b8-134">В ней выберите нужный контейнер.</span><span class="sxs-lookup"><span data-stu-id="752b8-134">In the storage account blade, select the container you want</span></span>
   
    ![Просмотр контейнеров][ViewContainers]
4. <span data-ttu-id="752b8-136">Выберите файл резервной копии, который вы хотите скачать или удалить.</span><span class="sxs-lookup"><span data-stu-id="752b8-136">Select backup file you want to download or delete.</span></span>
   
    ![ViewContainers](./media/web-sites-restore/03ViewFiles.png)
5. <span data-ttu-id="752b8-138">Щелкните **Скачать** или **Удалить**, в зависимости от того, что нужно сделать.</span><span class="sxs-lookup"><span data-stu-id="752b8-138">Click **Download** or **Delete** depending on what you want to do.</span></span>  

<a name="OperationLogs"></a>

## <a name="monitor-a-restore-operation"></a><span data-ttu-id="752b8-139">Мониторинг операции восстановления</span><span class="sxs-lookup"><span data-stu-id="752b8-139">Monitor a restore operation</span></span>
<span data-ttu-id="752b8-140">Чтобы просмотреть сведения о результате восстановления приложения (успешном или неудачном), перейдите к колонке **Журнал действий** на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="752b8-140">To see details about the success or failure of the app restore operation, navigate to the **Activity Log** blade in the Azure portal.</span></span>  
 

<span data-ttu-id="752b8-141">Прокрутите колонку вниз, чтобы найти нужную операцию восстановления, и выберите ее щелчком.</span><span class="sxs-lookup"><span data-stu-id="752b8-141">Scroll down to find the desired restore operation and click to select it.</span></span>

<span data-ttu-id="752b8-142">В колонке сведений отобразится вся доступная информация о выбранной операции восстановления.</span><span class="sxs-lookup"><span data-stu-id="752b8-142">The details blade displays the available information related to the restore operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="752b8-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="752b8-143">Next Steps</span></span>
<span data-ttu-id="752b8-144">Для архивации и восстановления приложений службы приложений можно использовать REST API (ознакомьтесь со статьей [Использование REST для резервного копирования и восстановления приложений службы приложений](websites-csm-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="752b8-144">You can backup and restore App Service apps using REST API (see [Use REST to back up and restore App Service apps](websites-csm-backup.md)).</span></span>


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
