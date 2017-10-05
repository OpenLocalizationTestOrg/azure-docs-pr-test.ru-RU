---
title: "Архивация приложения в Azure"
description: "Узнайте, как создавать резервные копии приложений в службе приложений Azure."
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
ms.openlocfilehash: 77e983afaaba8e944ab1f337e1c28ced83b63205
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="back-up-your-app-in-azure"></a><span data-ttu-id="4dae3-103">Архивация приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="4dae3-103">Back up your app in Azure</span></span>
<span data-ttu-id="4dae3-104">Функция архивации и восстановления в [службе приложений Azure](../app-service/app-service-value-prop-what-is.md) позволяет легко создавать резервные копии приложений вручную или по расписанию.</span><span class="sxs-lookup"><span data-stu-id="4dae3-104">The Back up and Restore feature in [Azure App Service](../app-service/app-service-value-prop-what-is.md) lets you easily create app backups manually or on a schedule.</span></span> <span data-ttu-id="4dae3-105">Вы можете восстановить приложение до моментального снимка предыдущего состояния, перезаписав существующее приложение или восстановив другое.</span><span class="sxs-lookup"><span data-stu-id="4dae3-105">You can restore the app to a snapshot of a previous state by overwriting the existing app or restoring to another app.</span></span> 

<span data-ttu-id="4dae3-106">Сведения о восстановлении приложения из резервной копии см. в статье [Восстановление приложения в службе приложений Azure](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="4dae3-106">For information on restoring an app from backup, see [Restore an app in Azure](web-sites-restore.md).</span></span>

<a name="whatsbackedup"></a>

## <a name="what-gets-backed-up"></a><span data-ttu-id="4dae3-107">Что входит в резервную копию</span><span class="sxs-lookup"><span data-stu-id="4dae3-107">What gets backed up</span></span>
<span data-ttu-id="4dae3-108">Служба приложений может архивировать в учетную запись хранения Azure и контейнер, который вы настроили для использования вашим приложением, следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="4dae3-108">App Service can backup the following information to an Azure storage account and container that you have configured your app to use.</span></span> 

* <span data-ttu-id="4dae3-109">конфигурация приложения;</span><span class="sxs-lookup"><span data-stu-id="4dae3-109">App configuration</span></span>
* <span data-ttu-id="4dae3-110">содержимое файла;</span><span class="sxs-lookup"><span data-stu-id="4dae3-110">File content</span></span>
* <span data-ttu-id="4dae3-111">база данных, подключенная к приложению.</span><span class="sxs-lookup"><span data-stu-id="4dae3-111">Database connected to your app</span></span>

<span data-ttu-id="4dae3-112">Функция архивации поддерживается для следующих решений базы данных:</span><span class="sxs-lookup"><span data-stu-id="4dae3-112">The following database solutions are supported with backup feature:</span></span> 
   - [<span data-ttu-id="4dae3-113">База данных SQL</span><span class="sxs-lookup"><span data-stu-id="4dae3-113">SQL Database</span></span>](https://azure.microsoft.com/en-us/services/sql-database/)
   - <span data-ttu-id="4dae3-114">[база данных Azure для MySQL (предварительная версия)](https://azure.microsoft.com/en-us/services/mysql);</span><span class="sxs-lookup"><span data-stu-id="4dae3-114">[Azure Database for MySQL (Preview)](https://azure.microsoft.com/en-us/services/mysql)</span></span>
   - <span data-ttu-id="4dae3-115">[база данных Azure для PostgreSQL (предварительная версия)](https://azure.microsoft.com/en-us/services/postgres);</span><span class="sxs-lookup"><span data-stu-id="4dae3-115">[Azure Database for PostgreSQL (Preview)](https://azure.microsoft.com/en-us/services/postgres)</span></span>
   - <span data-ttu-id="4dae3-116">[ClearDB MySQL](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview);</span><span class="sxs-lookup"><span data-stu-id="4dae3-116">[ClearDB MySQL](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)</span></span>
   - <span data-ttu-id="4dae3-117">[MySQL в приложении](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app).</span><span class="sxs-lookup"><span data-stu-id="4dae3-117">[MySQL in-app](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)</span></span>
 

> [!NOTE]
>  <span data-ttu-id="4dae3-118">Каждая резервная копия является полной автономной копией приложения, а не добавочным обновлением.</span><span class="sxs-lookup"><span data-stu-id="4dae3-118">Each backup is a complete offline copy of your app, not an incremental update.</span></span>
>  

<a name="requirements"></a>

## <a name="requirements-and-restrictions"></a><span data-ttu-id="4dae3-119">Требования и ограничения</span><span class="sxs-lookup"><span data-stu-id="4dae3-119">Requirements and restrictions</span></span>
* <span data-ttu-id="4dae3-120">Для использования архивации и восстановления требуется, чтобы у плана службы приложений был уровень **Стандартный** или **Премиум**.</span><span class="sxs-lookup"><span data-stu-id="4dae3-120">The Back up and Restore feature requires the App Service plan to be in the **Standard** tier or **Premium** tier.</span></span> <span data-ttu-id="4dae3-121">Дополнительные сведения о масштабировании плана службы приложений для использования более высокого уровня см. в статье [Масштабирование веб-приложения в службе приложений Azure](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="4dae3-121">For more information about scaling your App Service plan to use a higher tier, see [Scale up an app in Azure](web-sites-scale.md).</span></span>  
  <span data-ttu-id="4dae3-122">Уровень **Премиум** позволяет создавать большее количество ежедневных резервных копий по сравнению с уровнем **Стандартный**.</span><span class="sxs-lookup"><span data-stu-id="4dae3-122">**Premium** tier allows a greater number of daily back ups than **Standard** tier.</span></span>
* <span data-ttu-id="4dae3-123">Вам потребуется учетная запись хранения Azure и контейнер в той же подписке, что и приложение, для которого вы хотите создавать резервные копии.</span><span class="sxs-lookup"><span data-stu-id="4dae3-123">You need an Azure storage account and container in the same subscription as the app that you want to backup.</span></span> <span data-ttu-id="4dae3-124">Дополнительные сведения об учетных записях хранения Azure доступны в разделе [ссылок](#moreaboutstorage) в конце этой статьи.</span><span class="sxs-lookup"><span data-stu-id="4dae3-124">For more information on Azure storage accounts, see the [links](#moreaboutstorage) at the end of this article.</span></span>
* <span data-ttu-id="4dae3-125">Резервная копия может вмещать до 10 ГБ содержимого приложения и базы данных.</span><span class="sxs-lookup"><span data-stu-id="4dae3-125">Backups can be up to 10 GB of app and database content.</span></span> <span data-ttu-id="4dae3-126">Если размер резервной копии превысит этот лимит, отобразится сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="4dae3-126">If the backup size exceeds this limit, you get an error .</span></span>

<a name="manualbackup"></a>

## <a name="create-a-manual-backup"></a><span data-ttu-id="4dae3-127">Создание резервной копии вручную</span><span class="sxs-lookup"><span data-stu-id="4dae3-127">Create a manual backup</span></span>
1. <span data-ttu-id="4dae3-128">На [портале Azure](https://portal.azure.com) перейдите к колонке своего приложения и выберите **Резервные копии**.</span><span class="sxs-lookup"><span data-stu-id="4dae3-128">In the [Azure Portal](https://portal.azure.com), navigate to your app's blade, select **Backups**.</span></span> <span data-ttu-id="4dae3-129">Откроется колонка **Резервные копии** .</span><span class="sxs-lookup"><span data-stu-id="4dae3-129">The **Backups** blade will be displayed.</span></span>
   
    ![Страница резервных копий][ChooseBackupsPage]
   
   > [!NOTE]
   > <span data-ttu-id="4dae3-131">Если вы видите сообщение, приведенное ниже, щелкните его, чтобы обновить план службы приложений, прежде чем продолжить архивацию.</span><span class="sxs-lookup"><span data-stu-id="4dae3-131">If you see the message below, click it to upgrade your App Service plan before you can proceed with backups.</span></span>
   > <span data-ttu-id="4dae3-132">Дополнительные сведения см. в разделе [Масштабирование веб-приложения в службе приложений Azure](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="4dae3-132">See [Scale up an app in Azure](web-sites-scale.md) for more information.</span></span>  
   > <span data-ttu-id="4dae3-133">![Выбор учетной записи хранения](./media/web-sites-backup/01UpgradePlan1.png)</span><span class="sxs-lookup"><span data-stu-id="4dae3-133">![Choose storage account](./media/web-sites-backup/01UpgradePlan1.png)</span></span>
   > 
   > 

2. <span data-ttu-id="4dae3-134">В колонке **Архивация** щелкните **Настройка**.
![Выбор параметра "Настройка"](./media/web-sites-backup/ClickConfigure1.png)</span><span class="sxs-lookup"><span data-stu-id="4dae3-134">In the **Backup** blade, Click **Configure**
![Click Configure](./media/web-sites-backup/ClickConfigure1.png)</span></span>
3. <span data-ttu-id="4dae3-135">В колонке **Резервная конфигурация** щелкните **Хранилище: не настроено**, чтобы настроить учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="4dae3-135">In the **Backup Configuration** blade, click **Storage: Not configured** to configure a storage account.</span></span>
   
    ![Выбор учетной записи хранения][ChooseStorageAccount]
4. <span data-ttu-id="4dae3-137">Выберите расположение резервной копии, щелкнув **Учетная запись хранения** > **Контейнер**.</span><span class="sxs-lookup"><span data-stu-id="4dae3-137">Choose your backup destination by selecting a **Storage Account** and **Container**.</span></span> <span data-ttu-id="4dae3-138">Эта учетная запись хранения должна принадлежать к той же подписке, что и приложение, резервную копию которого вы собираетесь создать.</span><span class="sxs-lookup"><span data-stu-id="4dae3-138">The storage account must belong to the same subscription as the app you want to back up.</span></span> <span data-ttu-id="4dae3-139">При необходимости в соответствующих колонках можно создать новую учетную запись хранения или новый контейнер.</span><span class="sxs-lookup"><span data-stu-id="4dae3-139">If you wish, you can create a new storage account or a new container in the respective blades.</span></span> <span data-ttu-id="4dae3-140">Закончив, щелкните **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="4dae3-140">When you're done, click **Select**.</span></span>
   
    ![Выбор учетной записи хранения](./media/web-sites-backup/02ChooseStorageAccount1-1.png)
5. <span data-ttu-id="4dae3-142">В колонке **Резервная конфигурация**, которая по-прежнему открыта, вы можете настроить **резервную копию базы данных**, а затем выбрать базы данных, которые необходимо включить в резервные копии (база данных SQL или MySQL), а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="4dae3-142">In the **Backup Configuration** blade that is still left open, you can configure **Backup Database**, then select the databases you want to include in the backups (SQL database or MySQL), then click **OK**.</span></span>  
   
    ![Выбор учетной записи хранения](./media/web-sites-backup/03ConfigureDatabase1.png)
   
   > [!NOTE]
   > <span data-ttu-id="4dae3-144">Чтобы база данных появилась в этом списке, ее строка подключения должна присутствовать в разделе **Строки подключения** колонки **Параметры приложения** вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="4dae3-144">For a database to appear in this list, its connection string must exist in the **Connection strings** section of the **Application settings** blade for your app.</span></span>
   > 
   > 
6. <span data-ttu-id="4dae3-145">В колонке **Резервная конфигурация** нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="4dae3-145">In the **Backup Configuration** blade, click **Save**.</span></span>    
7. <span data-ttu-id="4dae3-146">В колонке **Резервные копии** щелкните **Архивация**.</span><span class="sxs-lookup"><span data-stu-id="4dae3-146">In the  **Backups** blade, click **Backup**.</span></span>
   
    ![Кнопка создания резервной копии][BackUpNow]
   
    <span data-ttu-id="4dae3-148">Во время процесса архивации отображается сообщение о ходе выполнения.</span><span class="sxs-lookup"><span data-stu-id="4dae3-148">You see a progress message during the backup process.</span></span>

<span data-ttu-id="4dae3-149">После того как вы настроили учетную запись хранения и контейнер, вы можете вручную запустить архивацию в любой момент.</span><span class="sxs-lookup"><span data-stu-id="4dae3-149">Once the storage account and container is configured you can initiate a manual backup at any time.</span></span>  

<a name="automatedbackups"></a>

## <a name="configure-automated-backups"></a><span data-ttu-id="4dae3-150">Настройка автоматического резервного копирования</span><span class="sxs-lookup"><span data-stu-id="4dae3-150">Configure automated backups</span></span>
1. <span data-ttu-id="4dae3-151">В колонке **Резервная конфигурация** для параметра **Архивация по расписанию** установите значение **Вкл**.</span><span class="sxs-lookup"><span data-stu-id="4dae3-151">In the **Backup Configuration** blade, set **Scheduled backup** to **On**.</span></span> 
   
    ![Выбор учетной записи хранения](./media/web-sites-backup/05ScheduleBackup1.png)
2. <span data-ttu-id="4dae3-153">Появятся параметры расписания архивации. Выберите для параметра **Запланированная архивация** значение **Вкл**, а затем настройте необходимое расписание архивации и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="4dae3-153">Backup schedule options will show up, set **Scheduled Backup** to **On**, then configure the backup schedule as desired and click **OK**.</span></span>
   
    ![Включение автоматически создаваемых резервных копий][SetAutomatedBackupOn]

<a name="partialbackups"></a>

## <a name="configure-partial-backups"></a><span data-ttu-id="4dae3-155">Настройка частичной архивации</span><span class="sxs-lookup"><span data-stu-id="4dae3-155">Configure Partial Backups</span></span>
<span data-ttu-id="4dae3-156">Иногда не нужно создавать резервную копию всего приложения.</span><span class="sxs-lookup"><span data-stu-id="4dae3-156">Sometimes you don't want to backup everything on your app.</span></span> <span data-ttu-id="4dae3-157">Вот несколько таких случаев.</span><span class="sxs-lookup"><span data-stu-id="4dae3-157">Here are a few examples:</span></span>

* <span data-ttu-id="4dae3-158">У вас [настроена еженедельная архивация](web-sites-backup.md#configure-automated-backups) приложения со статическим содержимым, которое никогда не меняется. Это могут быть старые записи блога или изображения.</span><span class="sxs-lookup"><span data-stu-id="4dae3-158">You [set up weekly backups](web-sites-backup.md#configure-automated-backups) of your app that contains static content that never changes, such as old blog posts or images.</span></span>
* <span data-ttu-id="4dae3-159">Размер содержимого приложения превышает 10 ГБ (т. е. максимальный размер резервной копии, которую можно создать за раз).</span><span class="sxs-lookup"><span data-stu-id="4dae3-159">Your app has over 10 GB of content (that's the max amount you can backup at a time).</span></span>
* <span data-ttu-id="4dae3-160">Не нужно создавать резервную копию файлов журнала.</span><span class="sxs-lookup"><span data-stu-id="4dae3-160">You don't want to backup the log files.</span></span>

<span data-ttu-id="4dae3-161">Частичная архивация позволяет выбрать только те файлы, для которых нужно создать резервную копию.</span><span class="sxs-lookup"><span data-stu-id="4dae3-161">Partial backups allows you choose exactly which files you want to backup.</span></span>

### <a name="exclude-files-from-your-backup"></a><span data-ttu-id="4dae3-162">Исключение файлов из резервной копии</span><span class="sxs-lookup"><span data-stu-id="4dae3-162">Exclude files from your backup</span></span>
<span data-ttu-id="4dae3-163">Допустим, есть приложение, содержащее файлы журнала и статические изображения, которые были однажды архивированы и не будут изменяться.</span><span class="sxs-lookup"><span data-stu-id="4dae3-163">Suppose you have an app that contains log files and static images that have been backup once and are not going to change.</span></span> <span data-ttu-id="4dae3-164">В таких случаях вы можете исключить эти папки и файлы из будущих резервных копий.</span><span class="sxs-lookup"><span data-stu-id="4dae3-164">In such cases you can exclude those folders and files from being stored in your future backups.</span></span> <span data-ttu-id="4dae3-165">Чтобы исключить файлы и папки из резервных копий, создайте файл `_backup.filter` в папке `D:\home\site\wwwroot` своего приложения.</span><span class="sxs-lookup"><span data-stu-id="4dae3-165">To exclude files and folders from your backups, create a `_backup.filter` file in the `D:\home\site\wwwroot` folder of your app.</span></span> <span data-ttu-id="4dae3-166">В этом файле укажите список файлов и папок, которые вы хотите исключить.</span><span class="sxs-lookup"><span data-stu-id="4dae3-166">Specify the list of files and folders you want to exclude in this file.</span></span> 

<span data-ttu-id="4dae3-167">Самый простой способ получить доступ к файлам — использовать Kudu.</span><span class="sxs-lookup"><span data-stu-id="4dae3-167">An easy way to access your files is to use Kudu .</span></span> <span data-ttu-id="4dae3-168">Щелкните параметр **Дополнительные инструменты -> Вперед** для своего веб-приложения, чтобы получить доступ к Kudu.</span><span class="sxs-lookup"><span data-stu-id="4dae3-168">Click **Advanced Tools -> Go** setting for your web app to access Kudu.</span></span>

![Использование Kudu с помощью портала][kudu-portal]

<span data-ttu-id="4dae3-170">Определите папки, которые вы хотите исключить из резервных копий.</span><span class="sxs-lookup"><span data-stu-id="4dae3-170">Identify the folders that you want to exclude from your backups.</span></span>  <span data-ttu-id="4dae3-171">Например, вы хотите отфильтровать выделенные папки и файлы.</span><span class="sxs-lookup"><span data-stu-id="4dae3-171">For example , you want to filter out the highlighted folder and files.</span></span>

![Папка с изображениями][ImagesFolder]

<span data-ttu-id="4dae3-173">Создайте файл с именем `_backup.filter` и поместите в него приведенный выше список, при этом удалив `D:\home`.</span><span class="sxs-lookup"><span data-stu-id="4dae3-173">Create a file called `_backup.filter` and put the list above in the file, but remove `D:\home`.</span></span> <span data-ttu-id="4dae3-174">В одной строке указывайте один каталог или файл.</span><span class="sxs-lookup"><span data-stu-id="4dae3-174">List one directory or file per line.</span></span> <span data-ttu-id="4dae3-175">В результате содержимое файла будет выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="4dae3-175">So the content of the file should be:</span></span>
 ```bash
    \site\wwwroot\Images\brand.png
    \site\wwwroot\Images\2014
    \site\wwwroot\Images\2013
```

<span data-ttu-id="4dae3-176">Отправьте файл `_backup.filter` в каталог `D:\home\site\wwwroot\` своего сайта с помощью протокола [FTP](web-sites-deploy.md#ftp) или любым другим способом.</span><span class="sxs-lookup"><span data-stu-id="4dae3-176">Upload `_backup.filter` file to the `D:\home\site\wwwroot\` directory of your site using [ftp](web-sites-deploy.md#ftp) or any other method.</span></span> <span data-ttu-id="4dae3-177">При желании можно создать файл непосредственно с помощью `DebugConsole` Kudu и вставить в него содержимое.</span><span class="sxs-lookup"><span data-stu-id="4dae3-177">If you wish, you can create the file directly using Kudu  `DebugConsole` and insert the content there.</span></span>

<span data-ttu-id="4dae3-178">Выполните архивацию привычным для вас способом — [вручную](#create-a-manual-backup) или [автоматически](#configure-automated-backups).</span><span class="sxs-lookup"><span data-stu-id="4dae3-178">Run backups the same way you would normally do it, [manually](#create-a-manual-backup) or [automatically](#configure-automated-backups).</span></span> <span data-ttu-id="4dae3-179">Теперь любые файлы и папки, которые указаны в `_backup.filter`, будут исключены из будущих архиваций, инициированных по расписанию или вручную.</span><span class="sxs-lookup"><span data-stu-id="4dae3-179">Now, any files and folders that are specified in `_backup.filter` is excluded from the future backups scheduled or manually initiated.</span></span> 

> [!NOTE]
> <span data-ttu-id="4dae3-180">Восстановление частичных резервных копий сайта происходит так же, как и [восстановление обычных резервных копий](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="4dae3-180">You restore partial backups of your site the same way you would [restore a regular backup](web-sites-restore.md).</span></span> <span data-ttu-id="4dae3-181">Восстановление выполняется надлежащим образом.</span><span class="sxs-lookup"><span data-stu-id="4dae3-181">The restore process does the right thing.</span></span>
> 
> <span data-ttu-id="4dae3-182">При восстановлении полной резервной копии все содержимое сайта заменяется содержимым из резервной копии.</span><span class="sxs-lookup"><span data-stu-id="4dae3-182">When a full backup is restored, all content on the site is replaced with whatever is in the backup.</span></span> <span data-ttu-id="4dae3-183">Если файл, который находится на сайте, не включен в резервную копию, он удаляется.</span><span class="sxs-lookup"><span data-stu-id="4dae3-183">If a file is on the site, but not in the backup it gets deleted.</span></span> <span data-ttu-id="4dae3-184">Однако при восстановлении частичной резервной копии все содержимое, которое находится в каталогах или файлах из черного списка, остается неизменным.</span><span class="sxs-lookup"><span data-stu-id="4dae3-184">But when a partial backup is restored, any content that is located in one of the blacklisted directories, or any blacklisted file, is left as is.</span></span>
> 


<a name="aboutbackups"></a>

## <a name="how-backups-are-stored"></a><span data-ttu-id="4dae3-185">Как хранятся резервные копии</span><span class="sxs-lookup"><span data-stu-id="4dae3-185">How backups are stored</span></span>
<span data-ttu-id="4dae3-186">После создания одной или нескольких резервных копий приложения они отображаются в колонке **Контейнеры** вашей учетной записи хранения, как и ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="4dae3-186">After you have made one or more backups for your app, the backups are visible on the **Containers** blade of your storage account, and your app.</span></span> <span data-ttu-id="4dae3-187">В учетной записи хранения каждая резервная копия состоит из файла `.zip` с резервной копией данных и файла `.xml` с манифестом для содержимого файла `.zip`.</span><span class="sxs-lookup"><span data-stu-id="4dae3-187">In the storage account, each backup consists of a`.zip` file that contains the backup data and an `.xml` file that contains a manifest of the `.zip` file contents.</span></span> <span data-ttu-id="4dae3-188">Эти файлы можно распаковать и просмотреть, если необходимо получить доступ к резервным копиям без фактического восстановления приложения.</span><span class="sxs-lookup"><span data-stu-id="4dae3-188">You can unzip and browse these files if you want to access your backups without actually performing an app restore.</span></span>

<span data-ttu-id="4dae3-189">Резервная копия базы данных приложения хранится в корне ZIP-файла.</span><span class="sxs-lookup"><span data-stu-id="4dae3-189">The database backup for the app is stored in the root of the.zip file.</span></span> <span data-ttu-id="4dae3-190">Для базы данных SQL это файл BACPAC (без расширения), и его можно импортировать.</span><span class="sxs-lookup"><span data-stu-id="4dae3-190">For a SQL database, this is a BACPAC file (no file extension) and can be imported.</span></span> <span data-ttu-id="4dae3-191">Инструкции по созданию базы данных SQL на основе экспорта BACPAC-файла см. в статье [Импорт файла BACPAC для создания новой пользовательской базы данных](http://technet.microsoft.com/library/hh710052.aspx).</span><span class="sxs-lookup"><span data-stu-id="4dae3-191">To create a SQL database based on the BACPAC export, see [Import a BACPAC File to Create a New User Database](http://technet.microsoft.com/library/hh710052.aspx).</span></span>

> [!WARNING]
> <span data-ttu-id="4dae3-192">Изменение любого из этих файлов в контейнере **websitebackups** может привести к повреждению резервной копии и сделать восстановление из нее невозможным.</span><span class="sxs-lookup"><span data-stu-id="4dae3-192">Altering any of the files in your **websitebackups** container can cause the backup to become invalid and therefore non-restorable.</span></span>
> 
> 

<a name="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="4dae3-193">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4dae3-193">Next Steps</span></span>
<span data-ttu-id="4dae3-194">Сведения о восстановлении приложения из резервной копии см. в статье [Восстановление приложения в службе приложений Azure](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="4dae3-194">For information on restoring an app from a backup, see [Restore an app in Azure](web-sites-restore.md).</span></span> <span data-ttu-id="4dae3-195">Для архивации и восстановления приложений службы приложений можно также использовать REST API (см.статью [Использование REST для резервного копирования и восстановления приложений службы приложений](websites-csm-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="4dae3-195">You can also backup and restore App Service apps using REST API (see [Use REST to backup and restore App Service apps](websites-csm-backup.md)).</span></span>


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

