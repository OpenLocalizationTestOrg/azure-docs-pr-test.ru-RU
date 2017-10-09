---
title: "Архивация виртуальных машин Linux в Azure | Документы Майкрософт"
description: "Защита виртуальных машин Linux путем их архивации с помощью службы архивации Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/27/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 7c00392d5185a2f067f2ee2717529dcbde1e71f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-linux--virtual-machines-in-azure"></a><span data-ttu-id="c95f9-103">Архивация виртуальных машин Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="c95f9-103">Back up Linux  virtual machines in Azure</span></span>

<span data-ttu-id="c95f9-104">Защиту данных можно обеспечить, выполняя архивацию через регулярные интервалы.</span><span class="sxs-lookup"><span data-stu-id="c95f9-104">You can protect your data by taking backups at regular intervals.</span></span> <span data-ttu-id="c95f9-105">Служба архивации Azure создает точки восстановления, которые хранятся в геоизбыточных хранилищах восстановления.</span><span class="sxs-lookup"><span data-stu-id="c95f9-105">Azure Backup creates recovery points that are stored in geo-redundant recovery vaults.</span></span> <span data-ttu-id="c95f9-106">При восстановлении из точки восстановления можно восстановить hello всей виртуальной Машины или лишь некоторые файлы.</span><span class="sxs-lookup"><span data-stu-id="c95f9-106">When you restore from a recovery point, you can restore hello whole VM or just specific files.</span></span> <span data-ttu-id="c95f9-107">В этой статье объясняется, как toorestore один файл tooa nginx работающей виртуальной Машины с Linux.</span><span class="sxs-lookup"><span data-stu-id="c95f9-107">This article explains how toorestore a single file tooa Linux VM running nginx.</span></span> <span data-ttu-id="c95f9-108">Если у вас еще нет toouse виртуальной Машины, можно создать один с помощью hello [краткое руководство Linux](quick-create-cli.md).</span><span class="sxs-lookup"><span data-stu-id="c95f9-108">If you don't already have a VM toouse, you can create one using hello [Linux quickstart](quick-create-cli.md).</span></span> <span data-ttu-id="c95f9-109">Из этого руководства вы узнаете, как выполнить следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="c95f9-109">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c95f9-110">Создание архива виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="c95f9-110">Create a backup of a VM</span></span>
> * <span data-ttu-id="c95f9-111">Планирование ежедневной архивации</span><span class="sxs-lookup"><span data-stu-id="c95f9-111">Schedule a daily backup</span></span>
> * <span data-ttu-id="c95f9-112">Восстановление файла из архива</span><span class="sxs-lookup"><span data-stu-id="c95f9-112">Restore a file from a backup</span></span>



## <a name="backup-overview"></a><span data-ttu-id="c95f9-113">Обзор службы архивации</span><span class="sxs-lookup"><span data-stu-id="c95f9-113">Backup overview</span></span>

<span data-ttu-id="c95f9-114">Когда служба резервного копирования Azure hello инициирует резервной копии, оно активирует tootake hello расширение резервного копирования моментального снимка в определенный момент.</span><span class="sxs-lookup"><span data-stu-id="c95f9-114">When hello Azure Backup service initiates a backup, it triggers hello backup extension tootake a point-in-time snapshot.</span></span> <span data-ttu-id="c95f9-115">Hello службы архивации Azure использует hello _VMSnapshotLinux_ расширения в Linux.</span><span class="sxs-lookup"><span data-stu-id="c95f9-115">hello Azure Backup service uses hello _VMSnapshotLinux_ extension in Linux.</span></span> <span data-ttu-id="c95f9-116">расширение Hello устанавливается во время hello первая резервная копия виртуальной Машины, если hello виртуальная машина работает под управлением.</span><span class="sxs-lookup"><span data-stu-id="c95f9-116">hello extension is installed during hello first VM backup if hello VM is running.</span></span> <span data-ttu-id="c95f9-117">Если hello Виртуальная машина не запущена, hello службы резервного копирования снимок hello базовое хранилище (так как не записывайте возникать при hello остановки виртуальной Машины).</span><span class="sxs-lookup"><span data-stu-id="c95f9-117">If hello VM is not running, hello Backup service takes a snapshot of hello underlying storage (since no application writes occur while hello VM is stopped).</span></span>

<span data-ttu-id="c95f9-118">По умолчанию резервного копирования Azure принимает согласованное резервная копия файловой системы для виртуальной Машины Linux, но может быть настроенный tootake [согласованное резервное копирование приложений с помощью платформы сценариев до и после](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent).</span><span class="sxs-lookup"><span data-stu-id="c95f9-118">By default, Azure Backup takes a file system consistent backup for Linux VM but it can be configured tootake [application consistent backup using pre-script and post-script framework](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent).</span></span> <span data-ttu-id="c95f9-119">Hello службы архивации Azure делает снимок hello, hello данных после переносятся toohello хранилища.</span><span class="sxs-lookup"><span data-stu-id="c95f9-119">Once hello Azure Backup service takes hello snapshot, hello data is transferred toohello vault.</span></span> <span data-ttu-id="c95f9-120">эффективность toomaximize hello служба определяет и передает только hello блоков данных, которые были изменены с момента предыдущего резервного копирования hello.</span><span class="sxs-lookup"><span data-stu-id="c95f9-120">toomaximize efficiency, hello service identifies and transfers only hello blocks of data that have changed since hello previous backup.</span></span>

<span data-ttu-id="c95f9-121">После завершения передачи данных hello hello снимок удаляется и создается точка восстановления.</span><span class="sxs-lookup"><span data-stu-id="c95f9-121">When hello data transfer is complete, hello snapshot is removed and a recovery point is created.</span></span>


## <a name="create-a-backup"></a><span data-ttu-id="c95f9-122">Создание резервной копии</span><span class="sxs-lookup"><span data-stu-id="c95f9-122">Create a backup</span></span>
<span data-ttu-id="c95f9-123">Создание простого запланированного ежедневного резервного копирования tooa хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="c95f9-123">Create a simple scheduled daily backup tooa Recovery Services Vault.</span></span> 

1. <span data-ttu-id="c95f9-124">Войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c95f9-124">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="c95f9-125">Выберите в меню hello слева hello, **виртуальные машины**.</span><span class="sxs-lookup"><span data-stu-id="c95f9-125">In hello menu on hello left, select **Virtual machines**.</span></span> 
3. <span data-ttu-id="c95f9-126">Выберите из списка hello tooback ВМ вверх.</span><span class="sxs-lookup"><span data-stu-id="c95f9-126">From hello list, select a VM tooback up.</span></span>
4. <span data-ttu-id="c95f9-127">В колонке виртуальной Машины hello в hello **параметры** щелкните **резервного копирования**.</span><span class="sxs-lookup"><span data-stu-id="c95f9-127">On hello VM blade, in hello **Settings** section, click **Backup**.</span></span> <span data-ttu-id="c95f9-128">Hello **Enable backup** открывает колонку.</span><span class="sxs-lookup"><span data-stu-id="c95f9-128">hello **Enable backup** blade opens.</span></span>
5. <span data-ttu-id="c95f9-129">В **хранилище служб восстановления**, нажмите кнопку **создать новый** и укажите имя hello для нового хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="c95f9-129">In **Recovery Services vault**, click **Create new** and provide hello name for hello new vault.</span></span> <span data-ttu-id="c95f9-130">Новое хранилище создается в hello же группу ресурсов и расположение, как виртуальная машина hello.</span><span class="sxs-lookup"><span data-stu-id="c95f9-130">A new vault is created in hello same Resource Group and location as hello virtual machine.</span></span>
6. <span data-ttu-id="c95f9-131">Щелкните **Политика архивации**.</span><span class="sxs-lookup"><span data-stu-id="c95f9-131">Click **Backup policy**.</span></span> <span data-ttu-id="c95f9-132">В этом примере оставьте значения по умолчанию hello и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c95f9-132">For this example, keep hello defaults and click **OK**.</span></span>
7. <span data-ttu-id="c95f9-133">На hello **Enable backup** колонка, щелкните **включить архивацию**.</span><span class="sxs-lookup"><span data-stu-id="c95f9-133">On hello **Enable backup** blade, click **Enable Backup**.</span></span> <span data-ttu-id="c95f9-134">Это создает ежедневного резервного копирования на основе расписания по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="c95f9-134">This creates a daily backup based on hello default schedule.</span></span>
10. <span data-ttu-id="c95f9-135">toocreate начальной точки восстановления, на hello **резервного копирования** колонки щелкните **Архивировать сейчас**.</span><span class="sxs-lookup"><span data-stu-id="c95f9-135">toocreate an initial recovery point, on hello **Backup** blade click **Backup now**.</span></span>
11. <span data-ttu-id="c95f9-136">На hello **создать резервную копию** колонка, щелкните значок календаря hello, используйте hello календаря управления tooselect hello этой точки восстановления сохраняется и щелкните последний день **резервного копирования**.</span><span class="sxs-lookup"><span data-stu-id="c95f9-136">On hello **Backup Now** blade, click hello calendar icon, use hello calendar control tooselect hello last day this recovery point is retained, and click **Backup**.</span></span>
12. <span data-ttu-id="c95f9-137">В hello **резервного копирования** колонке ВМ, вы увидите hello количество точек восстановления, которые являются полными.</span><span class="sxs-lookup"><span data-stu-id="c95f9-137">In hello **Backup** blade for your VM, you will see hello number of recovery points that are complete.</span></span>

    ![Точки восстановления](./media/tutorial-backup-vms/backup-complete.png)

<span data-ttu-id="c95f9-139">Первая резервная копия Hello занимает примерно 20 минут.</span><span class="sxs-lookup"><span data-stu-id="c95f9-139">hello first backup takes about 20 minutes.</span></span> <span data-ttu-id="c95f9-140">Продолжить toohello следующей части этого руководства, после завершения резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="c95f9-140">Proceed toohello next part of this tutorial after your backup is finished.</span></span>

## <a name="restore-a-file"></a><span data-ttu-id="c95f9-141">Восстановление файла</span><span class="sxs-lookup"><span data-stu-id="c95f9-141">Restore a file</span></span>

<span data-ttu-id="c95f9-142">Случайно удалить или сделать файл tooa изменения, можно использовать файл hello toorecover восстановление файлов из резервного хранилища.</span><span class="sxs-lookup"><span data-stu-id="c95f9-142">If you accidentally delete or make changes tooa file, you can use File Recovery toorecover hello file from your backup vault.</span></span> <span data-ttu-id="c95f9-143">Восстановление файлов использует сценарий, который выполняется на ВМ, hello точки восстановления hello toomount как локальный диск.</span><span class="sxs-lookup"><span data-stu-id="c95f9-143">File Recovery uses a script that runs on hello VM, toomount hello recovery point as local drive.</span></span> <span data-ttu-id="c95f9-144">Эти диски останется подключенного 12 часов, можно скопировать файлы из точки восстановления hello и восстановить их toohello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="c95f9-144">These drives will remain mounted for 12 hours so that you can copy files from hello recovery point and restore them toohello VM.</span></span>  

<span data-ttu-id="c95f9-145">В этом примере показано, как toorecover hello /var/www/html/index.nginx-debian.html веб-страницы по умолчанию nginx.</span><span class="sxs-lookup"><span data-stu-id="c95f9-145">In this example, we show how toorecover hello default nginx web page /var/www/html/index.nginx-debian.html.</span></span> <span data-ttu-id="c95f9-146">общедоступный IP-адрес Hello нашей виртуальной машины в этом примере — *13.69.75.209*.</span><span class="sxs-lookup"><span data-stu-id="c95f9-146">hello public IP address of our VM in this example is *13.69.75.209*.</span></span> <span data-ttu-id="c95f9-147">Можно найти hello IP-адрес виртуальной машины с помощью:</span><span class="sxs-lookup"><span data-stu-id="c95f9-147">You can find hello IP address of your vm using:</span></span>

 ```bash 
 az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
 ```

 
1. <span data-ttu-id="c95f9-148">На локальном компьютере откройте браузер и введите в hello общедоступный IP-адрес веб-страницы nginx ВМ toosee hello по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c95f9-148">On your local computer, open a browser and type in hello public IP address of your VM toosee hello default nginx web page.</span></span>

    ![Веб-страница nginx по умолчанию](./media/tutorial-backup-vms/nginx-working.png)

1. <span data-ttu-id="c95f9-150">Подключитесь к виртуальной машине по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="c95f9-150">SSH into your VM.</span></span>

    ```bash
    ssh 13.69.75.209
    ```
2. <span data-ttu-id="c95f9-151">Удалите /var/www/html/index.nginx-debian.html.</span><span class="sxs-lookup"><span data-stu-id="c95f9-151">Delete /var/www/html/index.nginx-debian.html.</span></span>

    ```bash
    sudo rm /var/www/html/index.nginx-debian.html
    ```
    
4. <span data-ttu-id="c95f9-152">На локальном компьютере, обновите браузер hello, нажав сочетание клавиш CTRL + F5 toosee, nginx страница по умолчанию отсутствует.</span><span class="sxs-lookup"><span data-stu-id="c95f9-152">On your local computer, refresh hello browser by hitting CTRL + F5 toosee that default nginx page is gone.</span></span>

    ![Веб-страница nginx по умолчанию](./media/tutorial-backup-vms/nginx-broken.png)
    
1. <span data-ttu-id="c95f9-154">На локальном компьютере, войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c95f9-154">On your local computer, sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
6. <span data-ttu-id="c95f9-155">Выберите в меню hello слева hello, **виртуальные машины**.</span><span class="sxs-lookup"><span data-stu-id="c95f9-155">In hello menu on hello left, select **Virtual machines**.</span></span> 
7. <span data-ttu-id="c95f9-156">Выберите из списка hello hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="c95f9-156">From hello list, select hello VM.</span></span>
8. <span data-ttu-id="c95f9-157">В колонке виртуальной Машины hello в hello **параметры** щелкните **резервного копирования**.</span><span class="sxs-lookup"><span data-stu-id="c95f9-157">On hello VM blade, in hello **Settings** section, click **Backup**.</span></span> <span data-ttu-id="c95f9-158">Hello **резервного копирования** открывает колонку.</span><span class="sxs-lookup"><span data-stu-id="c95f9-158">hello **Backup** blade opens.</span></span> 
9. <span data-ttu-id="c95f9-159">Выберите в меню hello hello верхней части колонки hello, **восстановления файла**.</span><span class="sxs-lookup"><span data-stu-id="c95f9-159">In hello menu at hello top of hello blade, select **File Recovery**.</span></span> <span data-ttu-id="c95f9-160">Hello **восстановления файла** открывает колонку.</span><span class="sxs-lookup"><span data-stu-id="c95f9-160">hello **File Recovery** blade opens.</span></span>
10. <span data-ttu-id="c95f9-161">В **шаг 1: выберите точку восстановления**, выберите точку восстановления из раскрывающегося списка hello.</span><span class="sxs-lookup"><span data-stu-id="c95f9-161">In **Step 1: Select recovery point**, select a recovery point from hello drop-down.</span></span>
11. <span data-ttu-id="c95f9-162">В **шаг 2: загрузить скрипт toobrowse и восстанавливать файлы**, щелкните hello **загрузки исполняемого файла** кнопки.</span><span class="sxs-lookup"><span data-stu-id="c95f9-162">In **Step 2: Download script toobrowse and recover files**, click hello **Download Executable** button.</span></span> <span data-ttu-id="c95f9-163">Сохраните hello загруженный файл tooyour локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="c95f9-163">Save hello downloaded file tooyour local computer.</span></span>
7. <span data-ttu-id="c95f9-164">Нажмите кнопку **загрузки скрипта** файл скрипта hello toodownload локально.</span><span class="sxs-lookup"><span data-stu-id="c95f9-164">Click **Download script** toodownload hello script file locally.</span></span>
8. <span data-ttu-id="c95f9-165">Откройте Bash строку и введите hello следующие, заменив *Linux_myVM_05-05-2017.sh* с hello Исправьте путь и имя файла для hello скрипт, который вы загрузили *azureuser* с именем пользователя hello для hello виртуальной Машины и *13.69.75.209* с hello общедоступный IP-адрес для виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="c95f9-165">Open a Bash prompt and type hello following, replacing *Linux_myVM_05-05-2017.sh* with hello correct path and filename for hello script that you downloaded, *azureuser* with hello username for hello VM and *13.69.75.209* with hello public IP address for your VM.</span></span>
    
    ```bash
    scp Linux_myVM_05-05-2017.sh azureuser@13.69.75.209:
    ```
    
9. <span data-ttu-id="c95f9-166">На локальном компьютере откройте toohello подключения SSH виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="c95f9-166">On your local computer, open an SSH connection toohello VM.</span></span>

    ```bash
    ssh 13.69.75.209
    ```
    
10. <span data-ttu-id="c95f9-167">На ВМ, добавьте выполнить файл сценария toohello разрешения.</span><span class="sxs-lookup"><span data-stu-id="c95f9-167">On your VM, add execute permissions toohello script file.</span></span>

    ```bash
    chmod +x Linux_myVM_05-05-2017.sh
    ```
    
11. <span data-ttu-id="c95f9-168">На ВМ запустите точки восстановления hello toomount сценария hello как файловая система.</span><span class="sxs-lookup"><span data-stu-id="c95f9-168">On your VM, run hello script toomount hello recovery point as a filesystem.</span></span>

    ```bash
    ./Linux_myVM_05-05-2017.sh
    ```
    
12. <span data-ttu-id="c95f9-169">Hello выходных данных из hello скрипт предоставляет hello путь для точки подключения hello.</span><span class="sxs-lookup"><span data-stu-id="c95f9-169">hello output from hello script gives you hello path for hello mount point.</span></span> <span data-ttu-id="c95f9-170">Hello выходные данные выглядят аналогично toothis:</span><span class="sxs-lookup"><span data-stu-id="c95f9-170">hello output looks similar toothis:</span></span>

    ```bash
    Microsoft Azure VM Backup - File Recovery
    ______________________________________________
                          
    Connecting toorecovery point using ISCSI service...
    
    Connection succeeded!
    
    Please wait while we attach volumes of hello recovery point toothis machine...
                         
    ************ Volumes of hello recovery point and their mount paths on this machine ************

    Sr.No.  |  Disk  |  Volume  |  MountPath 

    1)  | /dev/sdc  |  /dev/sdc1  |  /home/azureuser/myVM-20170505191055/Volume1

    ************ Open File Explorer toobrowse for files. ************

    After recovery, tooremove hello disks and close hello connection toohello recovery point, please click 'Unmount Disks' in step 3 of hello portal.

    Please enter 'q/Q' tooexit...
    ```

12. <span data-ttu-id="c95f9-171">На ВМ, скопируйте hello nginx по умолчанию веб-страницы из toowhere назад точки подключения hello удален файл hello.</span><span class="sxs-lookup"><span data-stu-id="c95f9-171">On your VM, copy hello nginx default web page from hello mount point back toowhere you deleted hello file.</span></span>

    ```bash
    sudo cp ~/myVM-20170505191055/Volume1/var/www/html/index.nginx-debian.html /var/www/html/
    ```
    
17. <span data-ttu-id="c95f9-172">На локальном компьютере, откройте вкладку браузера hello, где вы подключены toohello IP-адрес по умолчанию hello ВМ показывающий hello nginx страницу.</span><span class="sxs-lookup"><span data-stu-id="c95f9-172">On your local computer, open hello browser tab where you are connected toohello IP address of hello VM showing hello nginx default page.</span></span> <span data-ttu-id="c95f9-173">Нажмите клавиши CTRL + F5 страницы браузера toorefresh hello.</span><span class="sxs-lookup"><span data-stu-id="c95f9-173">Press CTRL + F5 toorefresh hello browser page.</span></span> <span data-ttu-id="c95f9-174">Теперь вы увидите, hello снова работает страница по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c95f9-174">You should now see that hello default page is working again.</span></span>

    ![Веб-страница nginx по умолчанию](./media/tutorial-backup-vms/nginx-working.png)

18. <span data-ttu-id="c95f9-176">На локальном компьютере, вернитесь к предыдущему окну toohello вкладка «браузер» для hello портал Azure и в **Step 3: отключить диски hello после восстановления** щелкните hello **отключить диски** кнопки.</span><span class="sxs-lookup"><span data-stu-id="c95f9-176">On your local computer, go back toohello browser tab for hello Azure portal and in **Step 3: Unmount hello disks after recovery** click hello **Unmount Disks** button.</span></span> <span data-ttu-id="c95f9-177">Если этот этап будет пропущен toodo, автоматически закрыть монтирования toohello hello подключения через 12 часов.</span><span class="sxs-lookup"><span data-stu-id="c95f9-177">If you forget toodo this step, hello connection toohello mountpoint is automatically close after 12 hours.</span></span> <span data-ttu-id="c95f9-178">После этих 12 часов необходимо toodownload новый toocreate сценария новая точка монтирования.</span><span class="sxs-lookup"><span data-stu-id="c95f9-178">After those 12 hours, you need toodownload a new script toocreate a new mountpoint.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c95f9-179">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c95f9-179">Next steps</span></span>

<span data-ttu-id="c95f9-180">Из этого руководства вы узнали, как выполнить следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="c95f9-180">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c95f9-181">Создание архива виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="c95f9-181">Create a backup of a VM</span></span>
> * <span data-ttu-id="c95f9-182">Планирование ежедневной архивации</span><span class="sxs-lookup"><span data-stu-id="c95f9-182">Schedule a daily backup</span></span>
> * <span data-ttu-id="c95f9-183">Восстановление файла из архива</span><span class="sxs-lookup"><span data-stu-id="c95f9-183">Restore a file from a backup</span></span>

<span data-ttu-id="c95f9-184">Переместить следующий учебник toolearn toohello о мониторинге виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="c95f9-184">Advance toohello next tutorial toolearn about monitoring virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c95f9-185">Мониторинг виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="c95f9-185">Monitor virtual machines</span></span>](tutorial-monitoring.md)

