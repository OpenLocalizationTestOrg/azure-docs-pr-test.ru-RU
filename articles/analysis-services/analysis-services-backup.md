---
title: "Архивация и восстановление базы данных Azure Analysis Services | Документы Майкрософт"
description: "Описывает, как выполнять архивацию и восстановление базы данных Analysis Services Azure."
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
ms.openlocfilehash: bffa481a498b130ef1f2388a5ba856da5d164ee0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="backup-and-restore"></a><span data-ttu-id="10bb3-103">Архивация и восстановление</span><span class="sxs-lookup"><span data-stu-id="10bb3-103">Backup and restore</span></span>

<span data-ttu-id="10bb3-104">Архивация баз данных табличной модели в Azure Analysis Services во многом аналогична процедуре для локальных служб Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="10bb3-104">Backing up tabular model databases in Azure Analysis Services is much the same as for on-premises Analysis Services.</span></span> <span data-ttu-id="10bb3-105">Основное различие заключается в расположении для хранения архивных файлов.</span><span class="sxs-lookup"><span data-stu-id="10bb3-105">The primary difference is where you store your backup files.</span></span> <span data-ttu-id="10bb3-106">Архивные файлы следует сохранять в контейнер в [учетной записи хранения Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="10bb3-106">Backup files must be saved to a container in an [Azure storage account](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="10bb3-107">Можно использовать уже имеющиеся учетную запись хранения и контейнер либо создать их при настройке параметров хранилища для сервера.</span><span class="sxs-lookup"><span data-stu-id="10bb3-107">You can use a storage account and container you already have, or they can be created when configuring storage settings for your server.</span></span>

> [!NOTE]
> <span data-ttu-id="10bb3-108">Создание учетной записи хранения может привести к дополнительным расходам.</span><span class="sxs-lookup"><span data-stu-id="10bb3-108">Creating a storage account can result in a new billable service.</span></span> <span data-ttu-id="10bb3-109">Дополнительные сведения см. на [странице с ценами на службу хранилища Azure](https://azure.microsoft.com/pricing/details/storage/blobs/).</span><span class="sxs-lookup"><span data-stu-id="10bb3-109">To learn more, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/blobs/).</span></span>
> 
> 

<span data-ttu-id="10bb3-110">Архивные копии сохраняются с расширением ABF.</span><span class="sxs-lookup"><span data-stu-id="10bb3-110">Backups are saved with an abf extension.</span></span> <span data-ttu-id="10bb3-111">Для табличных моделей в памяти сохраняются как данные, так и метаданные модели.</span><span class="sxs-lookup"><span data-stu-id="10bb3-111">For in-memory tabular models, both model data and metadata are stored.</span></span> <span data-ttu-id="10bb3-112">Для табличных моделей с прямым запросом (DirectQuery) сохраняются только метаданные моделей.</span><span class="sxs-lookup"><span data-stu-id="10bb3-112">For DirectQuery tabular models, only model metadata is stored.</span></span> <span data-ttu-id="10bb3-113">В зависимости от выбранных вами параметров архивные копии могут быть сжаты и зашифрованы.</span><span class="sxs-lookup"><span data-stu-id="10bb3-113">Backups can be compressed and encrypted, depending on the options you choose.</span></span> 



## <a name="configure-storage-settings"></a><span data-ttu-id="10bb3-114">Настройка параметров хранения</span><span class="sxs-lookup"><span data-stu-id="10bb3-114">Configure storage settings</span></span>
<span data-ttu-id="10bb3-115">Перед архивацией нужно настроить для сервера параметры хранения.</span><span class="sxs-lookup"><span data-stu-id="10bb3-115">Before backing up, you need to configure storage settings for your server.</span></span>


### <a name="to-configure-storage-settings"></a><span data-ttu-id="10bb3-116">Порядок настройки параметров хранения</span><span class="sxs-lookup"><span data-stu-id="10bb3-116">To configure storage settings</span></span>
1.  <span data-ttu-id="10bb3-117">На портале Azure выберите **Параметры** и щелкните **Архивация**.</span><span class="sxs-lookup"><span data-stu-id="10bb3-117">In Azure portal > **Settings**, click **Backup**.</span></span>

    ![Архивация в параметрах](./media/analysis-services-backup/aas-backup-backups.png)

2.  <span data-ttu-id="10bb3-119">Щелкните **Включено**, а затем — **Параметры хранилища**.</span><span class="sxs-lookup"><span data-stu-id="10bb3-119">Click **Enabled**, then click **Storage Settings**.</span></span>

    ![Включение](./media/analysis-services-backup/aas-backup-enable.png)

3. <span data-ttu-id="10bb3-121">Выберите имеющуюся учетную запись хранения или создайте новую.</span><span class="sxs-lookup"><span data-stu-id="10bb3-121">Select your storage account or create a new one.</span></span>

4. <span data-ttu-id="10bb3-122">Выберите контейнер или создайте новый.</span><span class="sxs-lookup"><span data-stu-id="10bb3-122">Select a container or create a new one.</span></span>

    ![Выбор контейнера](./media/analysis-services-backup/aas-backup-container.png)

5. <span data-ttu-id="10bb3-124">Сохраните параметры архивации.</span><span class="sxs-lookup"><span data-stu-id="10bb3-124">Save your backup settings.</span></span>

    ![Сохранение параметров архивации](./media/analysis-services-backup/aas-backup-save.png)

## <a name="backup"></a><span data-ttu-id="10bb3-126">Резервное копирование</span><span class="sxs-lookup"><span data-stu-id="10bb3-126">Backup</span></span>

### <a name="to-backup-by-using-ssms"></a><span data-ttu-id="10bb3-127">Архивация с помощью SSMS</span><span class="sxs-lookup"><span data-stu-id="10bb3-127">To backup by using SSMS</span></span>

1. <span data-ttu-id="10bb3-128">В среде SSMS щелкните правой кнопкой мыши базу данных и выберите **Архивировать**.</span><span class="sxs-lookup"><span data-stu-id="10bb3-128">In SSMS, right-click a database > **Back Up**.</span></span>

2. <span data-ttu-id="10bb3-129">В разделе **Резервное копирование базы данных** > **Файл резервной копии** нажмите кнопку **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="10bb3-129">In **Backup Database** > **Backup file**, click **Browse**.</span></span>

3. <span data-ttu-id="10bb3-130">В диалоговом окне **Сохранить файл как** проверьте путь к папке, а затем введите имя для архивного файла.</span><span class="sxs-lookup"><span data-stu-id="10bb3-130">In the **Save file as** dialog, verify the folder path, and then type a name for the backup file.</span></span> 

4. <span data-ttu-id="10bb3-131">Выберите параметры в диалоговом окне **Резервное копирование базы данных**.</span><span class="sxs-lookup"><span data-stu-id="10bb3-131">In the **Backup Database** dialog, select options.</span></span>

    <span data-ttu-id="10bb3-132">**Разрешить перезапись файлов** —выберите этот параметр, чтобы перезаписывать архивные файлы с тем же именем.</span><span class="sxs-lookup"><span data-stu-id="10bb3-132">**Allow file overwrite** - Select this option to overwrite backup files of the same name.</span></span> <span data-ttu-id="10bb3-133">Если этот параметр не выбран, сохраняемый файл не может иметь то же имя, что и файл, который уже существует в этом расположении.</span><span class="sxs-lookup"><span data-stu-id="10bb3-133">If this option is not selected, the file you are saving cannot have the same name as a file that already exists in the same location.</span></span>

    <span data-ttu-id="10bb3-134">**Применить сжатие** — выберите этот параметр, чтобы сжать архивный файл.</span><span class="sxs-lookup"><span data-stu-id="10bb3-134">**Apply compression** - Select this option to compress the backup file.</span></span> <span data-ttu-id="10bb3-135">Сжатые архивные файлы экономят место на диске, но немного повышают использование ЦП.</span><span class="sxs-lookup"><span data-stu-id="10bb3-135">Compressed backup files save disk space, but require slightly higher CPU utilization.</span></span> 

    <span data-ttu-id="10bb3-136">**Зашифровать файл резервной копии** — выберите этот параметр, чтобы зашифровать архивный файл.</span><span class="sxs-lookup"><span data-stu-id="10bb3-136">**Encrypt backup file** - Select this option to encrypt the backup file.</span></span> <span data-ttu-id="10bb3-137">Этот параметр требует от пользователя ввести пароль для защиты файла.</span><span class="sxs-lookup"><span data-stu-id="10bb3-137">This option requires a user-supplied password to secure the backup file.</span></span> <span data-ttu-id="10bb3-138">Пароль не позволяет считать архивный файл иными способами, кроме операции восстановления.</span><span class="sxs-lookup"><span data-stu-id="10bb3-138">The password prevents reading of the backup data any other means than a restore operation.</span></span> <span data-ttu-id="10bb3-139">Если вы решили шифровать архивные копии, сохраните пароль в безопасном месте.</span><span class="sxs-lookup"><span data-stu-id="10bb3-139">If you choose to encrypt backups, store the password in a safe location.</span></span>

5. <span data-ttu-id="10bb3-140">Нажмите кнопку **ОК** для создания и сохранения архивного файла.</span><span class="sxs-lookup"><span data-stu-id="10bb3-140">Click **OK** to create and save the backup file.</span></span>


### <a name="powershell"></a><span data-ttu-id="10bb3-141">PowerShell</span><span class="sxs-lookup"><span data-stu-id="10bb3-141">PowerShell</span></span>
<span data-ttu-id="10bb3-142">Используйте командлет [Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet).</span><span class="sxs-lookup"><span data-stu-id="10bb3-142">Use [Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet) cmdlet.</span></span>

## <a name="restore"></a><span data-ttu-id="10bb3-143">Восстановление</span><span class="sxs-lookup"><span data-stu-id="10bb3-143">Restore</span></span>
<span data-ttu-id="10bb3-144">При восстановлении файл архивной копии должен находиться в учетной записи хранения, настроенной для вашего сервера.</span><span class="sxs-lookup"><span data-stu-id="10bb3-144">When restoring, your backup file must be in the storage account you've configured for your server.</span></span> <span data-ttu-id="10bb3-145">Если нужно переместить файл архивной копии из локального расположения в учетную запись хранилища, используйте [обозреватель хранилищ Microsoft Azure](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer) или служебную программу командной строки [AzCopy](../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="10bb3-145">If you need to move a backup file from an on-premises location to your storage account, use [Microsoft Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer) or the [AzCopy](../storage/common/storage-use-azcopy.md) command-line utility.</span></span> 



> [!NOTE]
> <span data-ttu-id="10bb3-146">Если вы выполняете восстановление с локального сервера, нужно сначала удалить всех пользователей домена из ролей модели, а затем снова добавить их в роли в качестве пользователей Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="10bb3-146">If you're restoring from an on-premises server, you must remove all the domain users from the model's roles and add them back to the roles as Azure Active Directory users.</span></span>
> 
> 

### <a name="to-restore-by-using-ssms"></a><span data-ttu-id="10bb3-147">Восстановление с помощью SSMS</span><span class="sxs-lookup"><span data-stu-id="10bb3-147">To restore by using SSMS</span></span>

1. <span data-ttu-id="10bb3-148">В среде SSMS щелкните правой кнопкой мыши базу данных и выберите **Восстановить**.</span><span class="sxs-lookup"><span data-stu-id="10bb3-148">In SSMS, right-click a database > **Restore**.</span></span>

2. <span data-ttu-id="10bb3-149">В разделе **Файл резервной копии** диалогового окна **Резервное копирование базы данных** нажмите кнопку **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="10bb3-149">In the **Backup Database** dialog, in **Backup file**, click **Browse**.</span></span>

3. <span data-ttu-id="10bb3-150">В диалоговом окне **Расположение файлов базы данных** выберите файл, который требуется восстановить.</span><span class="sxs-lookup"><span data-stu-id="10bb3-150">In the **Locate Database Files** dialog, select the file you want to restore.</span></span>

4. <span data-ttu-id="10bb3-151">В области **Восстановление базы данных** выберите базу данных.</span><span class="sxs-lookup"><span data-stu-id="10bb3-151">In **Restore database**, select the database.</span></span>

5. <span data-ttu-id="10bb3-152">Укажите параметры.</span><span class="sxs-lookup"><span data-stu-id="10bb3-152">Specify options.</span></span> <span data-ttu-id="10bb3-153">Параметры безопасности должны соответствовать параметрам, использовавшимся при архивации.</span><span class="sxs-lookup"><span data-stu-id="10bb3-153">Security options must match the backup options you used when backing up.</span></span>


### <a name="powershell"></a><span data-ttu-id="10bb3-154">PowerShell</span><span class="sxs-lookup"><span data-stu-id="10bb3-154">PowerShell</span></span>

<span data-ttu-id="10bb3-155">Используйте командлет [Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet).</span><span class="sxs-lookup"><span data-stu-id="10bb3-155">Use [Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet) cmdlet.</span></span>


## <a name="related-information"></a><span data-ttu-id="10bb3-156">Связанные сведения</span><span class="sxs-lookup"><span data-stu-id="10bb3-156">Related information</span></span>

[<span data-ttu-id="10bb3-157">Учетные записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="10bb3-157">Azure storage accounts</span></span>](../storage/common/storage-create-storage-account.md)  
<span data-ttu-id="10bb3-158">[Высокая доступность](analysis-services-bcdr.md)   </span><span class="sxs-lookup"><span data-stu-id="10bb3-158">[High availability](analysis-services-bcdr.md)   </span></span>  
[<span data-ttu-id="10bb3-159">Управление службами Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="10bb3-159">Manage Azure Analysis Services</span></span>](analysis-services-manage.md)
