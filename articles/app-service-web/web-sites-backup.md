---
title: "aaaBack копию приложения в Azure"
description: "Узнайте, как резервные копии toocreate приложений в службе приложений Azure."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 6223b6bd-84ec-48df-943f-461d84605694
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: e41d93d322bbc48b45b28eeaa817928d83c2b9d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-your-app-in-azure"></a><span data-ttu-id="a2708-103">Архивация приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="a2708-103">Back up your app in Azure</span></span>
<span data-ttu-id="a2708-104">Здравствуйте, резервное копирование и восстановление из состава [службе приложений Azure](../app-service/app-service-value-prop-what-is.md) позволяет легко создавать резервные копии приложения, вручную или по расписанию.</span><span class="sxs-lookup"><span data-stu-id="a2708-104">hello Back up and Restore feature in [Azure App Service](../app-service/app-service-value-prop-what-is.md) lets you easily create app backups manually or on a schedule.</span></span> <span data-ttu-id="a2708-105">Можно восстановить снимок tooa приложения hello предыдущее состояние, восстановление приложения tooanother или перезаписи существующего приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a2708-105">You can restore hello app tooa snapshot of a previous state by overwriting hello existing app or restoring tooanother app.</span></span> 

<span data-ttu-id="a2708-106">Сведения о восстановлении приложения из резервной копии см. в статье [Восстановление приложения в службе приложений Azure](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="a2708-106">For information on restoring an app from backup, see [Restore an app in Azure](web-sites-restore.md).</span></span>

<a name="whatsbackedup"></a>

## <a name="what-gets-backed-up"></a><span data-ttu-id="a2708-107">Что входит в резервную копию</span><span class="sxs-lookup"><span data-stu-id="a2708-107">What gets backed up</span></span>
<span data-ttu-id="a2708-108">Службы приложений можно создавать резервные копии следующих hello сведения учетной записи хранилища Azure tooan и контейнера, что вы настроили toouse вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="a2708-108">App Service can backup hello following information tooan Azure storage account and container that you have configured your app toouse.</span></span> 

* <span data-ttu-id="a2708-109">конфигурация приложения;</span><span class="sxs-lookup"><span data-stu-id="a2708-109">App configuration</span></span>
* <span data-ttu-id="a2708-110">содержимое файла;</span><span class="sxs-lookup"><span data-stu-id="a2708-110">File content</span></span>
* <span data-ttu-id="a2708-111">Приложение tooyour подключенной базы данных</span><span class="sxs-lookup"><span data-stu-id="a2708-111">Database connected tooyour app</span></span>

<span data-ttu-id="a2708-112">функция резервного копирования поддерживает Hello следующие решения базы данных.</span><span class="sxs-lookup"><span data-stu-id="a2708-112">hello following database solutions are supported with backup feature:</span></span> 
   - [<span data-ttu-id="a2708-113">База данных SQL</span><span class="sxs-lookup"><span data-stu-id="a2708-113">SQL Database</span></span>](https://azure.microsoft.com/en-us/services/sql-database/)
   - <span data-ttu-id="a2708-114">[база данных Azure для MySQL (предварительная версия)](https://azure.microsoft.com/en-us/services/mysql);</span><span class="sxs-lookup"><span data-stu-id="a2708-114">[Azure Database for MySQL (Preview)](https://azure.microsoft.com/en-us/services/mysql)</span></span>
   - <span data-ttu-id="a2708-115">[база данных Azure для PostgreSQL (предварительная версия)](https://azure.microsoft.com/en-us/services/postgres);</span><span class="sxs-lookup"><span data-stu-id="a2708-115">[Azure Database for PostgreSQL (Preview)](https://azure.microsoft.com/en-us/services/postgres)</span></span>
   - <span data-ttu-id="a2708-116">[ClearDB MySQL](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview);</span><span class="sxs-lookup"><span data-stu-id="a2708-116">[ClearDB MySQL](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)</span></span>
   - <span data-ttu-id="a2708-117">[MySQL в приложении](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app).</span><span class="sxs-lookup"><span data-stu-id="a2708-117">[MySQL in-app](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)</span></span>
 

> [!NOTE]
>  <span data-ttu-id="a2708-118">Каждая резервная копия является полной автономной копией приложения, а не добавочным обновлением.</span><span class="sxs-lookup"><span data-stu-id="a2708-118">Each backup is a complete offline copy of your app, not an incremental update.</span></span>
>  

<a name="requirements"></a>

## <a name="requirements-and-restrictions"></a><span data-ttu-id="a2708-119">Требования и ограничения</span><span class="sxs-lookup"><span data-stu-id="a2708-119">Requirements and restrictions</span></span>
* <span data-ttu-id="a2708-120">Здравствуйте, создайте резервную копию, и функция восстановления требует hello toobe плана служб приложений в hello **Стандартная** уровня или **Premium** уровня.</span><span class="sxs-lookup"><span data-stu-id="a2708-120">hello Back up and Restore feature requires hello App Service plan toobe in hello **Standard** tier or **Premium** tier.</span></span> <span data-ttu-id="a2708-121">Дополнительные сведения о масштабировании вашей toouse план службы приложений более высокого уровня см. в разделе [масштабировать приложение в Azure](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="a2708-121">For more information about scaling your App Service plan toouse a higher tier, see [Scale up an app in Azure](web-sites-scale.md).</span></span>  
  <span data-ttu-id="a2708-122">Уровень **Премиум** позволяет создавать большее количество ежедневных резервных копий по сравнению с уровнем **Стандартный**.</span><span class="sxs-lookup"><span data-stu-id="a2708-122">**Premium** tier allows a greater number of daily back ups than **Standard** tier.</span></span>
* <span data-ttu-id="a2708-123">Требуется имя учетной записи хранилища Azure и контейнер в hello той же подписке, что требуется toobackup приложение hello.</span><span class="sxs-lookup"><span data-stu-id="a2708-123">You need an Azure storage account and container in hello same subscription as hello app that you want toobackup.</span></span> <span data-ttu-id="a2708-124">Дополнительные сведения об учетных записях хранения Azure см. в разделе hello [ссылки](#moreaboutstorage) конце hello в этой статье.</span><span class="sxs-lookup"><span data-stu-id="a2708-124">For more information on Azure storage accounts, see hello [links](#moreaboutstorage) at hello end of this article.</span></span>
* <span data-ttu-id="a2708-125">Резервные копии могут быть too10 Гбайт, приложение и база данных содержимого.</span><span class="sxs-lookup"><span data-stu-id="a2708-125">Backups can be up too10 GB of app and database content.</span></span> <span data-ttu-id="a2708-126">Если размер резервной копии hello превышает это ограничение, возникает сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="a2708-126">If hello backup size exceeds this limit, you get an error .</span></span>

<a name="manualbackup"></a>

## <a name="create-a-manual-backup"></a><span data-ttu-id="a2708-127">Создание резервной копии вручную</span><span class="sxs-lookup"><span data-stu-id="a2708-127">Create a manual backup</span></span>
1. <span data-ttu-id="a2708-128">В hello [портала Azure](https://portal.azure.com), перейдите в колонку tooyour приложения, выберите **резервные копии**.</span><span class="sxs-lookup"><span data-stu-id="a2708-128">In hello [Azure Portal](https://portal.azure.com), navigate tooyour app's blade, select **Backups**.</span></span> <span data-ttu-id="a2708-129">Hello **резервные копии** отображается колонку.</span><span class="sxs-lookup"><span data-stu-id="a2708-129">hello **Backups** blade will be displayed.</span></span>
   
    ![Страница резервных копий][ChooseBackupsPage]
   
   > [!NOTE]
   > <span data-ttu-id="a2708-131">Если вы видите сообщение hello, показанное ниже, выберите его tooupgrade плана служб приложений перед продолжением с резервными копиями.</span><span class="sxs-lookup"><span data-stu-id="a2708-131">If you see hello message below, click it tooupgrade your App Service plan before you can proceed with backups.</span></span>
   > <span data-ttu-id="a2708-132">Дополнительные сведения см. в разделе [Масштабирование веб-приложения в службе приложений Azure](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="a2708-132">See [Scale up an app in Azure](web-sites-scale.md) for more information.</span></span>  
   > <span data-ttu-id="a2708-133">![Выбор учетной записи хранения](./media/web-sites-backup/01UpgradePlan1.png)</span><span class="sxs-lookup"><span data-stu-id="a2708-133">![Choose storage account](./media/web-sites-backup/01UpgradePlan1.png)</span></span>
   > 
   > 

2. <span data-ttu-id="a2708-134">В hello **резервного копирования** колонка, щелкните **Настройка**
![нажмите кнопку настроить.](./media/web-sites-backup/ClickConfigure1.png)</span><span class="sxs-lookup"><span data-stu-id="a2708-134">In hello **Backup** blade, Click **Configure**
![Click Configure](./media/web-sites-backup/ClickConfigure1.png)</span></span>
3. <span data-ttu-id="a2708-135">В hello **конфигурация резервного копирования** колонка, щелкните **хранилища: не настроен** tooconfigure учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="a2708-135">In hello **Backup Configuration** blade, click **Storage: Not configured** tooconfigure a storage account.</span></span>
   
    ![Выбор учетной записи хранения][ChooseStorageAccount]
4. <span data-ttu-id="a2708-137">Выберите расположение резервной копии, щелкнув **Учетная запись хранения** > **Контейнер**.</span><span class="sxs-lookup"><span data-stu-id="a2708-137">Choose your backup destination by selecting a **Storage Account** and **Container**.</span></span> <span data-ttu-id="a2708-138">Учетная запись хранения Hello должны принадлежать toohello той же подписке, необходимо tooback приложение hello.</span><span class="sxs-lookup"><span data-stu-id="a2708-138">hello storage account must belong toohello same subscription as hello app you want tooback up.</span></span> <span data-ttu-id="a2708-139">При желании можно создать новую учетную запись хранения или новый контейнер в соответствующих колонках hello.</span><span class="sxs-lookup"><span data-stu-id="a2708-139">If you wish, you can create a new storage account or a new container in hello respective blades.</span></span> <span data-ttu-id="a2708-140">Закончив, щелкните **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="a2708-140">When you're done, click **Select**.</span></span>
   
    ![Выбор учетной записи хранения](./media/web-sites-backup/02ChooseStorageAccount1-1.png)
5. <span data-ttu-id="a2708-142">В hello **конфигурация резервного копирования** колонки, по-прежнему остается открытым, можно настроить **Backup Database**, выберите hello базы данных, вы должны tooinclude в резервных копиях hello (база данных SQL или MySQL), а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a2708-142">In hello **Backup Configuration** blade that is still left open, you can configure **Backup Database**, then select hello databases you want tooinclude in hello backups (SQL database or MySQL), then click **OK**.</span></span>  
   
    ![Выбор учетной записи хранения](./media/web-sites-backup/03ConfigureDatabase1.png)
   
   > [!NOTE]
   > <span data-ttu-id="a2708-144">Для tooappear базы данных, в этом списке, его строка подключения должен существовать в hello **строки подключения** раздел hello **параметры приложения** колонку для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="a2708-144">For a database tooappear in this list, its connection string must exist in hello **Connection strings** section of hello **Application settings** blade for your app.</span></span>
   > 
   > 
6. <span data-ttu-id="a2708-145">В hello **конфигурация резервного копирования** колонка, щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="a2708-145">In hello **Backup Configuration** blade, click **Save**.</span></span>    
7. <span data-ttu-id="a2708-146">В hello **резервные копии** колонка, щелкните **резервного копирования**.</span><span class="sxs-lookup"><span data-stu-id="a2708-146">In hello  **Backups** blade, click **Backup**.</span></span>
   
    ![Кнопка создания резервной копии][BackUpNow]
   
    <span data-ttu-id="a2708-148">Появится сообщение о ходе выполнения во время процесса резервного копирования hello.</span><span class="sxs-lookup"><span data-stu-id="a2708-148">You see a progress message during hello backup process.</span></span>

<span data-ttu-id="a2708-149">После завершения настройки учетной записи хранилища hello и контейнер может инициировать архивации вручную в любое время.</span><span class="sxs-lookup"><span data-stu-id="a2708-149">Once hello storage account and container is configured you can initiate a manual backup at any time.</span></span>  

<a name="automatedbackups"></a>

## <a name="configure-automated-backups"></a><span data-ttu-id="a2708-150">Настройка автоматического резервного копирования</span><span class="sxs-lookup"><span data-stu-id="a2708-150">Configure automated backups</span></span>
1. <span data-ttu-id="a2708-151">В hello **конфигурации резервного копирования** задать колонке **запланированное резервное копирование** слишком**на**.</span><span class="sxs-lookup"><span data-stu-id="a2708-151">In hello **Backup Configuration** blade, set **Scheduled backup** too**On**.</span></span> 
   
    ![Выбор учетной записи хранения](./media/web-sites-backup/05ScheduleBackup1.png)
2. <span data-ttu-id="a2708-153">Задать расписание резервного копирования, параметры будут отображаться, **запланированного резервного копирования** слишком**на**, можно настроить желаемым образом hello расписание резервного копирования и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a2708-153">Backup schedule options will show up, set **Scheduled Backup** too**On**, then configure hello backup schedule as desired and click **OK**.</span></span>
   
    ![Включение автоматически создаваемых резервных копий][SetAutomatedBackupOn]

<a name="partialbackups"></a>

## <a name="configure-partial-backups"></a><span data-ttu-id="a2708-155">Настройка частичной архивации</span><span class="sxs-lookup"><span data-stu-id="a2708-155">Configure Partial Backups</span></span>
<span data-ttu-id="a2708-156">Иногда необходимо исключить toobackup все данные в приложении.</span><span class="sxs-lookup"><span data-stu-id="a2708-156">Sometimes you don't want toobackup everything on your app.</span></span> <span data-ttu-id="a2708-157">Вот несколько таких случаев.</span><span class="sxs-lookup"><span data-stu-id="a2708-157">Here are a few examples:</span></span>

* <span data-ttu-id="a2708-158">У вас [настроена еженедельная архивация](web-sites-backup.md#configure-automated-backups) приложения со статическим содержимым, которое никогда не меняется. Это могут быть старые записи блога или изображения.</span><span class="sxs-lookup"><span data-stu-id="a2708-158">You [set up weekly backups](web-sites-backup.md#configure-automated-backups) of your app that contains static content that never changes, such as old blog posts or images.</span></span>
* <span data-ttu-id="a2708-159">Приложение имеет более 10 ГБ содержимого (то есть hello max сумму, которую можно создать резервные копии за раз).</span><span class="sxs-lookup"><span data-stu-id="a2708-159">Your app has over 10 GB of content (that's hello max amount you can backup at a time).</span></span>
* <span data-ttu-id="a2708-160">Файлы журнала toobackup hello не следует.</span><span class="sxs-lookup"><span data-stu-id="a2708-160">You don't want toobackup hello log files.</span></span>

<span data-ttu-id="a2708-161">Частичные резервные копии позволяет выбрать только набор файлов, вы хотите toobackup.</span><span class="sxs-lookup"><span data-stu-id="a2708-161">Partial backups allows you choose exactly which files you want toobackup.</span></span>

### <a name="exclude-files-from-your-backup"></a><span data-ttu-id="a2708-162">Исключение файлов из резервной копии</span><span class="sxs-lookup"><span data-stu-id="a2708-162">Exclude files from your backup</span></span>
<span data-ttu-id="a2708-163">Предположим, что у вас есть приложение, которое содержит файлы журналов и статические изображения, которые были резервного копирования один раз и не будут toochange.</span><span class="sxs-lookup"><span data-stu-id="a2708-163">Suppose you have an app that contains log files and static images that have been backup once and are not going toochange.</span></span> <span data-ttu-id="a2708-164">В таких случаях вы можете исключить эти папки и файлы из будущих резервных копий.</span><span class="sxs-lookup"><span data-stu-id="a2708-164">In such cases you can exclude those folders and files from being stored in your future backups.</span></span> <span data-ttu-id="a2708-165">tooexclude файлов и папок из резервных копий, создавать `_backup.filter` файла в hello `D:\home\site\wwwroot` папку приложения.</span><span class="sxs-lookup"><span data-stu-id="a2708-165">tooexclude files and folders from your backups, create a `_backup.filter` file in hello `D:\home\site\wwwroot` folder of your app.</span></span> <span data-ttu-id="a2708-166">Укажите список файлов и папок необходимо tooexclude в этом файле hello.</span><span class="sxs-lookup"><span data-stu-id="a2708-166">Specify hello list of files and folders you want tooexclude in this file.</span></span> 

<span data-ttu-id="a2708-167">Файлы — toouse Kudu tooaccess легко.</span><span class="sxs-lookup"><span data-stu-id="a2708-167">An easy way tooaccess your files is toouse Kudu .</span></span> <span data-ttu-id="a2708-168">Нажмите кнопку **Дополнительные инструменты -> Go** для вашей веб приложения tooaccess Kudu.</span><span class="sxs-lookup"><span data-stu-id="a2708-168">Click **Advanced Tools -> Go** setting for your web app tooaccess Kudu.</span></span>

![Использование Kudu с помощью портала][kudu-portal]

<span data-ttu-id="a2708-170">Определите hello папок, tooexclude из резервных копий.</span><span class="sxs-lookup"><span data-stu-id="a2708-170">Identify hello folders that you want tooexclude from your backups.</span></span>  <span data-ttu-id="a2708-171">Например вы хотите toofilter файлы и папки выделенный hello.</span><span class="sxs-lookup"><span data-stu-id="a2708-171">For example , you want toofilter out hello highlighted folder and files.</span></span>

![Папка с изображениями][ImagesFolder]

<span data-ttu-id="a2708-173">Создайте файл с именем `_backup.filter` в файл hello поместить hello выше списка, но удалить `D:\home`.</span><span class="sxs-lookup"><span data-stu-id="a2708-173">Create a file called `_backup.filter` and put hello list above in hello file, but remove `D:\home`.</span></span> <span data-ttu-id="a2708-174">В одной строке указывайте один каталог или файл.</span><span class="sxs-lookup"><span data-stu-id="a2708-174">List one directory or file per line.</span></span> <span data-ttu-id="a2708-175">Поэтому содержимое hello hello файла должно быть:</span><span class="sxs-lookup"><span data-stu-id="a2708-175">So hello content of hello file should be:</span></span>
 ```bash
    \site\wwwroot\Images\brand.png
    \site\wwwroot\Images\2014
    \site\wwwroot\Images\2013
```

<span data-ttu-id="a2708-176">Отправка `_backup.filter` файл toohello `D:\home\site\wwwroot\` каталога сайта с помощью [ftp](web-sites-deploy.md#ftp) или любой другой метод.</span><span class="sxs-lookup"><span data-stu-id="a2708-176">Upload `_backup.filter` file toohello `D:\home\site\wwwroot\` directory of your site using [ftp](web-sites-deploy.md#ftp) or any other method.</span></span> <span data-ttu-id="a2708-177">Если вы хотите, можно создать файл hello непосредственно с помощью Kudu `DebugConsole` и вставка содержимого hello существует.</span><span class="sxs-lookup"><span data-stu-id="a2708-177">If you wish, you can create hello file directly using Kudu  `DebugConsole` and insert hello content there.</span></span>

<span data-ttu-id="a2708-178">Выполнение архивации hello таким же образом, это обычно делается, [вручную](#create-a-manual-backup) или [автоматически](#configure-automated-backups).</span><span class="sxs-lookup"><span data-stu-id="a2708-178">Run backups hello same way you would normally do it, [manually](#create-a-manual-backup) or [automatically](#configure-automated-backups).</span></span> <span data-ttu-id="a2708-179">Теперь, все файлы и папки, указанные в `_backup.filter` исключается из hello следующие операции резервного копирования в план или запуск вручную.</span><span class="sxs-lookup"><span data-stu-id="a2708-179">Now, any files and folders that are specified in `_backup.filter` is excluded from hello future backups scheduled or manually initiated.</span></span> 

> [!NOTE]
> <span data-ttu-id="a2708-180">Восстановление частичные резервные копии вашего сайта hello так же, как [восстановить регулярного резервного копирования](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="a2708-180">You restore partial backups of your site hello same way you would [restore a regular backup](web-sites-restore.md).</span></span> <span data-ttu-id="a2708-181">процесс восстановления Hello hello правильно.</span><span class="sxs-lookup"><span data-stu-id="a2708-181">hello restore process does hello right thing.</span></span>
> 
> <span data-ttu-id="a2708-182">При восстановлении полной резервной копии все содержимое на сайте hello заменяется на hello резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="a2708-182">When a full backup is restored, all content on hello site is replaced with whatever is in hello backup.</span></span> <span data-ttu-id="a2708-183">Если файл находится на сайте hello, но не в резервной копии hello, она удаляется.</span><span class="sxs-lookup"><span data-stu-id="a2708-183">If a file is on hello site, but not in hello backup it gets deleted.</span></span> <span data-ttu-id="a2708-184">Но если частичная резервная копия будет восстановлена, любое содержимое, которое находится в одном из каталогов hello черный или любой черного списка файл оставляется.</span><span class="sxs-lookup"><span data-stu-id="a2708-184">But when a partial backup is restored, any content that is located in one of hello blacklisted directories, or any blacklisted file, is left as is.</span></span>
> 


<a name="aboutbackups"></a>

## <a name="how-backups-are-stored"></a><span data-ttu-id="a2708-185">Как хранятся резервные копии</span><span class="sxs-lookup"><span data-stu-id="a2708-185">How backups are stored</span></span>
<span data-ttu-id="a2708-186">После внесения одной или нескольких копий приложения hello резервные копии являются видимыми в hello **контейнеры** колонке вашей учетной записи хранилища и приложения.</span><span class="sxs-lookup"><span data-stu-id="a2708-186">After you have made one or more backups for your app, hello backups are visible on hello **Containers** blade of your storage account, and your app.</span></span> <span data-ttu-id="a2708-187">В учетной записи хранения hello, каждой резервной копии состоит из`.zip` файл, содержащий данные резервного копирования hello и `.xml` файл, содержащий манифест hello `.zip` содержимое файлов.</span><span class="sxs-lookup"><span data-stu-id="a2708-187">In hello storage account, each backup consists of a`.zip` file that contains hello backup data and an `.xml` file that contains a manifest of hello `.zip` file contents.</span></span> <span data-ttu-id="a2708-188">Можно распаковать и обзор эти файлы, если требуется tooaccess резервных копий без фактического выполнения восстановления в приложение.</span><span class="sxs-lookup"><span data-stu-id="a2708-188">You can unzip and browse these files if you want tooaccess your backups without actually performing an app restore.</span></span>

<span data-ttu-id="a2708-189">Hello резервной копии базы данных для приложения hello хранится в корневой hello the.zip файла.</span><span class="sxs-lookup"><span data-stu-id="a2708-189">hello database backup for hello app is stored in hello root of the.zip file.</span></span> <span data-ttu-id="a2708-190">Для базы данных SQL это файл BACPAC (без расширения), и его можно импортировать.</span><span class="sxs-lookup"><span data-stu-id="a2708-190">For a SQL database, this is a BACPAC file (no file extension) and can be imported.</span></span> <span data-ttu-id="a2708-191">toocreate на hello экспорта BACPAC основе базы данных SQL см. в разделе [импорта файла BACPAC tooCreate новой пользовательской базы данных](http://technet.microsoft.com/library/hh710052.aspx).</span><span class="sxs-lookup"><span data-stu-id="a2708-191">toocreate a SQL database based on hello BACPAC export, see [Import a BACPAC File tooCreate a New User Database](http://technet.microsoft.com/library/hh710052.aspx).</span></span>

> [!WARNING]
> <span data-ttu-id="a2708-192">Изменение любого файла hello в вашей **websitebackups** контейнер может привести к hello резервного копирования toobecome недопустимые и поэтому невосстановимой.</span><span class="sxs-lookup"><span data-stu-id="a2708-192">Altering any of hello files in your **websitebackups** container can cause hello backup toobecome invalid and therefore non-restorable.</span></span>
> 
> 

<a name="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="a2708-193">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a2708-193">Next Steps</span></span>
<span data-ttu-id="a2708-194">Сведения о восстановлении приложения из резервной копии см. в статье [Восстановление приложения в службе приложений Azure](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="a2708-194">For information on restoring an app from a backup, see [Restore an app in Azure](web-sites-restore.md).</span></span> <span data-ttu-id="a2708-195">Можно также резервное копирование и восстановление приложения служб приложений с помощью REST API (см. [использования REST toobackup и восстановление приложения служб приложений](websites-csm-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="a2708-195">You can also backup and restore App Service apps using REST API (see [Use REST toobackup and restore App Service apps](websites-csm-backup.md)).</span></span>


<!-- IMAGES -->
[ChooseBackupsPage]: ./media/web-sites-backup/01ChooseBackupsPage1.png
[ChooseStorageAccount]: ./media/web-sites-backup/02ChooseStorageAccount-1.png
[IncludedDatabases]: ./media/web-sites-backup/03IncludedDatabases.png
[BackUpNow]: ./media/web-sites-backup/04BackUpNow1.png
[BackupProgress]: ./media/web-sites-backup/05BackupProgress.png
[SetAutomatedBackupOn]: ./media/web-sites-backup/06SetAutomatedBackupOn1.png
[Frequency]: ./media/web-sites-backup/07Frequency.png
[StartDate]: ./media/web-sites-backup/08StartDate.png
[StartTime]: ./media/web-sites-backup/09StartTime.png
[SaveIcon]: ./media/web-sites-backup/10SaveIcon.png
[ImagesFolder]: ./media/web-sites-backup/11Images.png
[LogsFolder]: ./media/web-sites-backup/12Logs.png
[GhostUpgradeWarning]: ./media/web-sites-backup/13GhostUpgradeWarning.png
[kudu-portal]:./media/web-sites-backup/kudu-portal.PNG

