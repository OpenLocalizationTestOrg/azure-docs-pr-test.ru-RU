---
title: "базы данных служб Analysis Services aaaAzure резервного копирования и восстановления | Документы Microsoft"
description: "Описывает, как toobackup и восстановления служб Azure Analysis Services базы данных."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: cf0a782d237a95fdfa5ef628f998bd053aac0d9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="backup-and-restore"></a><span data-ttu-id="c6d85-103">Архивация и восстановление</span><span class="sxs-lookup"><span data-stu-id="c6d85-103">Backup and restore</span></span>

<span data-ttu-id="c6d85-104">Резервное копирование баз данных табличной модели в службах Analysis Services Azure является намного hello таким же как и для локальных служб Analysis.</span><span class="sxs-lookup"><span data-stu-id="c6d85-104">Backing up tabular model databases in Azure Analysis Services is much hello same as for on-premises Analysis Services.</span></span> <span data-ttu-id="c6d85-105">Hello основное различие заключается в хранения файлов резервных копий.</span><span class="sxs-lookup"><span data-stu-id="c6d85-105">hello primary difference is where you store your backup files.</span></span> <span data-ttu-id="c6d85-106">Файлы резервной копии необходимо сохранить контейнера tooa в [учетной записи хранилища Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="c6d85-106">Backup files must be saved tooa container in an [Azure storage account](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="c6d85-107">Можно использовать уже имеющиеся учетную запись хранения и контейнер либо создать их при настройке параметров хранилища для сервера.</span><span class="sxs-lookup"><span data-stu-id="c6d85-107">You can use a storage account and container you already have, or they can be created when configuring storage settings for your server.</span></span>

> [!NOTE]
> <span data-ttu-id="c6d85-108">Создание учетной записи хранения может привести к дополнительным расходам.</span><span class="sxs-lookup"><span data-stu-id="c6d85-108">Creating a storage account can result in a new billable service.</span></span> <span data-ttu-id="c6d85-109">toolearn более, в разделе [цены на хранилища Azure](https://azure.microsoft.com/pricing/details/storage/blobs/).</span><span class="sxs-lookup"><span data-stu-id="c6d85-109">toolearn more, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/blobs/).</span></span>
> 
> 

<span data-ttu-id="c6d85-110">Архивные копии сохраняются с расширением ABF.</span><span class="sxs-lookup"><span data-stu-id="c6d85-110">Backups are saved with an abf extension.</span></span> <span data-ttu-id="c6d85-111">Для табличных моделей в памяти сохраняются как данные, так и метаданные модели.</span><span class="sxs-lookup"><span data-stu-id="c6d85-111">For in-memory tabular models, both model data and metadata are stored.</span></span> <span data-ttu-id="c6d85-112">Для табличных моделей с прямым запросом (DirectQuery) сохраняются только метаданные моделей.</span><span class="sxs-lookup"><span data-stu-id="c6d85-112">For DirectQuery tabular models, only model metadata is stored.</span></span> <span data-ttu-id="c6d85-113">Резервные копии сжимаются и шифруются, в зависимости от выбранных параметров hello.</span><span class="sxs-lookup"><span data-stu-id="c6d85-113">Backups can be compressed and encrypted, depending on hello options you choose.</span></span> 



## <a name="configure-storage-settings"></a><span data-ttu-id="c6d85-114">Настройка параметров хранения</span><span class="sxs-lookup"><span data-stu-id="c6d85-114">Configure storage settings</span></span>
<span data-ttu-id="c6d85-115">Перед созданием резервной копии необходимо tooconfigure настройки хранилища для вашего сервера.</span><span class="sxs-lookup"><span data-stu-id="c6d85-115">Before backing up, you need tooconfigure storage settings for your server.</span></span>


### <a name="tooconfigure-storage-settings"></a><span data-ttu-id="c6d85-116">Параметры хранилища tooconfigure</span><span class="sxs-lookup"><span data-stu-id="c6d85-116">tooconfigure storage settings</span></span>
1.  <span data-ttu-id="c6d85-117">На портале Azure выберите **Параметры** и щелкните **Архивация**.</span><span class="sxs-lookup"><span data-stu-id="c6d85-117">In Azure portal > **Settings**, click **Backup**.</span></span>

    ![Архивация в параметрах](./media/analysis-services-backup/aas-backup-backups.png)

2.  <span data-ttu-id="c6d85-119">Щелкните **Включено**, а затем — **Параметры хранилища**.</span><span class="sxs-lookup"><span data-stu-id="c6d85-119">Click **Enabled**, then click **Storage Settings**.</span></span>

    ![Включение](./media/analysis-services-backup/aas-backup-enable.png)

3. <span data-ttu-id="c6d85-121">Выберите имеющуюся учетную запись хранения или создайте новую.</span><span class="sxs-lookup"><span data-stu-id="c6d85-121">Select your storage account or create a new one.</span></span>

4. <span data-ttu-id="c6d85-122">Выберите контейнер или создайте новый.</span><span class="sxs-lookup"><span data-stu-id="c6d85-122">Select a container or create a new one.</span></span>

    ![Выбор контейнера](./media/analysis-services-backup/aas-backup-container.png)

5. <span data-ttu-id="c6d85-124">Сохраните параметры архивации.</span><span class="sxs-lookup"><span data-stu-id="c6d85-124">Save your backup settings.</span></span>

    ![Сохранение параметров архивации](./media/analysis-services-backup/aas-backup-save.png)

## <a name="backup"></a><span data-ttu-id="c6d85-126">Резервное копирование</span><span class="sxs-lookup"><span data-stu-id="c6d85-126">Backup</span></span>

### <a name="toobackup-by-using-ssms"></a><span data-ttu-id="c6d85-127">toobackup с помощью среды SSMS</span><span class="sxs-lookup"><span data-stu-id="c6d85-127">toobackup by using SSMS</span></span>

1. <span data-ttu-id="c6d85-128">В среде SSMS щелкните правой кнопкой мыши базу данных и выберите **Архивировать**.</span><span class="sxs-lookup"><span data-stu-id="c6d85-128">In SSMS, right-click a database > **Back Up**.</span></span>

2. <span data-ttu-id="c6d85-129">В разделе **Резервное копирование базы данных** > **Файл резервной копии** нажмите кнопку **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="c6d85-129">In **Backup Database** > **Backup file**, click **Browse**.</span></span>

3. <span data-ttu-id="c6d85-130">В hello **сохранить файл как** диалогового окна, проверьте путь к папке hello, а затем введите имя для файла резервной копии hello.</span><span class="sxs-lookup"><span data-stu-id="c6d85-130">In hello **Save file as** dialog, verify hello folder path, and then type a name for hello backup file.</span></span> 

4. <span data-ttu-id="c6d85-131">В hello **Backup Database** диалоговое окно, выберите параметры.</span><span class="sxs-lookup"><span data-stu-id="c6d85-131">In hello **Backup Database** dialog, select options.</span></span>

    <span data-ttu-id="c6d85-132">**Позволяет создать файл перезаписать** -выберите этот параметр toooverwrite файлы резервной копии hello таким же именем.</span><span class="sxs-lookup"><span data-stu-id="c6d85-132">**Allow file overwrite** - Select this option toooverwrite backup files of hello same name.</span></span> <span data-ttu-id="c6d85-133">Если этот параметр не выбран, сохранении файла hello не может иметь hello точно такое же имя файла, который уже существует в hello же расположение.</span><span class="sxs-lookup"><span data-stu-id="c6d85-133">If this option is not selected, hello file you are saving cannot have hello same name as a file that already exists in hello same location.</span></span>

    <span data-ttu-id="c6d85-134">**Выполнить сжатие** -выберите данный параметр toocompress hello файл резервной копии.</span><span class="sxs-lookup"><span data-stu-id="c6d85-134">**Apply compression** - Select this option toocompress hello backup file.</span></span> <span data-ttu-id="c6d85-135">Сжатые архивные файлы экономят место на диске, но немного повышают использование ЦП.</span><span class="sxs-lookup"><span data-stu-id="c6d85-135">Compressed backup files save disk space, but require slightly higher CPU utilization.</span></span> 

    <span data-ttu-id="c6d85-136">**Зашифровать файл резервной копии** -выберите данный параметр tooencrypt hello файл резервной копии.</span><span class="sxs-lookup"><span data-stu-id="c6d85-136">**Encrypt backup file** - Select this option tooencrypt hello backup file.</span></span> <span data-ttu-id="c6d85-137">Этот параметр требует пользовательского пароля toosecure hello файл резервной копии.</span><span class="sxs-lookup"><span data-stu-id="c6d85-137">This option requires a user-supplied password toosecure hello backup file.</span></span> <span data-ttu-id="c6d85-138">Hello пароль предотвращает считывания резервных копий данных hello другим способом, чем операции восстановления.</span><span class="sxs-lookup"><span data-stu-id="c6d85-138">hello password prevents reading of hello backup data any other means than a restore operation.</span></span> <span data-ttu-id="c6d85-139">При выборе tooencrypt резервные копии, сохраните пароль hello в безопасном месте.</span><span class="sxs-lookup"><span data-stu-id="c6d85-139">If you choose tooencrypt backups, store hello password in a safe location.</span></span>

5. <span data-ttu-id="c6d85-140">Нажмите кнопку **ОК** toocreate и сохраните файл резервной копии hello.</span><span class="sxs-lookup"><span data-stu-id="c6d85-140">Click **OK** toocreate and save hello backup file.</span></span>


### <a name="powershell"></a><span data-ttu-id="c6d85-141">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c6d85-141">PowerShell</span></span>
<span data-ttu-id="c6d85-142">Используйте командлет [Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet).</span><span class="sxs-lookup"><span data-stu-id="c6d85-142">Use [Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet) cmdlet.</span></span>

## <a name="restore"></a><span data-ttu-id="c6d85-143">восстановление;</span><span class="sxs-lookup"><span data-stu-id="c6d85-143">Restore</span></span>
<span data-ttu-id="c6d85-144">При восстановлении файла резервной копии необходимо в учетной записи хранилища hello, настроенные для сервера.</span><span class="sxs-lookup"><span data-stu-id="c6d85-144">When restoring, your backup file must be in hello storage account you've configured for your server.</span></span> <span data-ttu-id="c6d85-145">Файл резервной копии из локальной учетной записи хранилища расположение tooyour toomove используйте [обозреватель хранилищ Microsoft Azure](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer) или hello [AzCopy](../storage/common/storage-use-azcopy.md) программы командной строки.</span><span class="sxs-lookup"><span data-stu-id="c6d85-145">If you need toomove a backup file from an on-premises location tooyour storage account, use [Microsoft Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer) or hello [AzCopy](../storage/common/storage-use-azcopy.md) command-line utility.</span></span> 



> [!NOTE]
> <span data-ttu-id="c6d85-146">Если производится восстановление с локального сервера, необходимо удалить все пользователи домена hello из роли модели hello и добавьте их обратно toohello роли в качестве пользователей Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c6d85-146">If you're restoring from an on-premises server, you must remove all hello domain users from hello model's roles and add them back toohello roles as Azure Active Directory users.</span></span>
> 
> 

### <a name="toorestore-by-using-ssms"></a><span data-ttu-id="c6d85-147">toorestore с помощью среды SSMS</span><span class="sxs-lookup"><span data-stu-id="c6d85-147">toorestore by using SSMS</span></span>

1. <span data-ttu-id="c6d85-148">В среде SSMS щелкните правой кнопкой мыши базу данных и выберите **Восстановить**.</span><span class="sxs-lookup"><span data-stu-id="c6d85-148">In SSMS, right-click a database > **Restore**.</span></span>

2. <span data-ttu-id="c6d85-149">В hello **Backup Database** диалоговое окно, в **файл резервной копии**, нажмите кнопку **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="c6d85-149">In hello **Backup Database** dialog, in **Backup file**, click **Browse**.</span></span>

3. <span data-ttu-id="c6d85-150">В hello **расположение файлов базы данных** диалоговое окно, выберите hello файл toorestore.</span><span class="sxs-lookup"><span data-stu-id="c6d85-150">In hello **Locate Database Files** dialog, select hello file you want toorestore.</span></span>

4. <span data-ttu-id="c6d85-151">В **инструкцию Restore database**выберите hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="c6d85-151">In **Restore database**, select hello database.</span></span>

5. <span data-ttu-id="c6d85-152">Укажите параметры.</span><span class="sxs-lookup"><span data-stu-id="c6d85-152">Specify options.</span></span> <span data-ttu-id="c6d85-153">Параметры безопасности, должны соответствовать hello параметры резервного копирования, которая использовалась при создании резервной копии.</span><span class="sxs-lookup"><span data-stu-id="c6d85-153">Security options must match hello backup options you used when backing up.</span></span>


### <a name="powershell"></a><span data-ttu-id="c6d85-154">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c6d85-154">PowerShell</span></span>

<span data-ttu-id="c6d85-155">Используйте командлет [Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet).</span><span class="sxs-lookup"><span data-stu-id="c6d85-155">Use [Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet) cmdlet.</span></span>


## <a name="related-information"></a><span data-ttu-id="c6d85-156">Связанные сведения</span><span class="sxs-lookup"><span data-stu-id="c6d85-156">Related information</span></span>

[<span data-ttu-id="c6d85-157">Учетные записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="c6d85-157">Azure storage accounts</span></span>](../storage/common/storage-create-storage-account.md)  
<span data-ttu-id="c6d85-158">[Высокая доступность](analysis-services-bcdr.md)   </span><span class="sxs-lookup"><span data-stu-id="c6d85-158">[High availability](analysis-services-bcdr.md)   </span></span>  
[<span data-ttu-id="c6d85-159">Управление службами Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="c6d85-159">Manage Azure Analysis Services</span></span>](analysis-services-manage.md)
