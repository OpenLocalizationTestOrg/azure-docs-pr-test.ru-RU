---
title: "aaaBackup виртуальных машин Windows Azure | Документы Microsoft"
description: "Защита виртуальных машин Windows путем их архивации с помощью службы архивации Azure."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/27/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 1cd3e1940a83aacd160cba3c8613b63b6f3c11d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-windows-virtual-machines-in-azure"></a><span data-ttu-id="d40a8-103">Архивация виртуальных машин Windows в Azure</span><span class="sxs-lookup"><span data-stu-id="d40a8-103">Back up Windows virtual machines in Azure</span></span>

<span data-ttu-id="d40a8-104">Для защиты данных можно создавать архивы с регулярным интервалом.</span><span class="sxs-lookup"><span data-stu-id="d40a8-104">You can protect your data by taking backups at regular intervals.</span></span> <span data-ttu-id="d40a8-105">Служба архивации Azure создает точки восстановления, которые хранятся в геоизбыточных хранилищах восстановления.</span><span class="sxs-lookup"><span data-stu-id="d40a8-105">Azure Backup creates recovery points that are stored in geo-redundant recovery vaults.</span></span> <span data-ttu-id="d40a8-106">При восстановлении из точки восстановления можно восстановить hello всей виртуальной Машины или лишь некоторые файлы.</span><span class="sxs-lookup"><span data-stu-id="d40a8-106">When you restore from a recovery point, you can restore hello whole VM or just specific files.</span></span> <span data-ttu-id="d40a8-107">В этой статье объясняется, как toorestore один файл tooa виртуальной Машины под управлением Windows Server и IIS.</span><span class="sxs-lookup"><span data-stu-id="d40a8-107">This article explains how toorestore a single file tooa VM running Windows Server and IIS.</span></span> <span data-ttu-id="d40a8-108">Если у вас еще нет toouse виртуальной Машины, можно создать один с помощью hello [быстрый запуск Windows](quick-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d40a8-108">If you don't already have a VM toouse, you can create one using hello [Windows quickstart](quick-create-portal.md).</span></span> <span data-ttu-id="d40a8-109">Из этого руководства вы узнаете, как выполнить следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="d40a8-109">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d40a8-110">Создание архива виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="d40a8-110">Create a backup of a VM</span></span>
> * <span data-ttu-id="d40a8-111">Планирование ежедневной архивации</span><span class="sxs-lookup"><span data-stu-id="d40a8-111">Schedule a daily backup</span></span>
> * <span data-ttu-id="d40a8-112">Восстановление файла из архива</span><span class="sxs-lookup"><span data-stu-id="d40a8-112">Restore a file from a backup</span></span>




## <a name="backup-overview"></a><span data-ttu-id="d40a8-113">Обзор службы архивации</span><span class="sxs-lookup"><span data-stu-id="d40a8-113">Backup overview</span></span>

<span data-ttu-id="d40a8-114">Когда служба резервного копирования Azure hello инициирует задание резервного копирования, оно активирует tootake hello расширение резервного копирования моментального снимка в определенный момент.</span><span class="sxs-lookup"><span data-stu-id="d40a8-114">When hello Azure Backup service initiates a backup job, it triggers hello backup extension tootake a point-in-time snapshot.</span></span> <span data-ttu-id="d40a8-115">Hello службы архивации Azure использует hello _VMSnapshot_ расширения.</span><span class="sxs-lookup"><span data-stu-id="d40a8-115">hello Azure Backup service uses hello _VMSnapshot_ extension.</span></span> <span data-ttu-id="d40a8-116">расширение Hello устанавливается во время hello первая резервная копия виртуальной Машины, если hello виртуальная машина работает под управлением.</span><span class="sxs-lookup"><span data-stu-id="d40a8-116">hello extension is installed during hello first VM backup if hello VM is running.</span></span> <span data-ttu-id="d40a8-117">Если hello Виртуальная машина не запущена, hello службы резервного копирования снимок hello базовое хранилище (так как не записывайте возникать при hello остановки виртуальной Машины).</span><span class="sxs-lookup"><span data-stu-id="d40a8-117">If hello VM is not running, hello Backup service takes a snapshot of hello underlying storage (since no application writes occur while hello VM is stopped).</span></span>

<span data-ttu-id="d40a8-118">При создании моментального снимка ВМ Windows, служба резервного копирования hello координирует с помощью службы теневого копирования томов (VSS) tooget hello согласованный моментальный снимок диски hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d40a8-118">When taking a snapshot of Windows VMs, hello Backup service coordinates with hello Volume Shadow Copy Service (VSS) tooget a consistent snapshot of hello virtual machine's disks.</span></span> <span data-ttu-id="d40a8-119">Hello службы архивации Azure делает снимок hello, hello данных после переносятся toohello хранилища.</span><span class="sxs-lookup"><span data-stu-id="d40a8-119">Once hello Azure Backup service takes hello snapshot, hello data is transferred toohello vault.</span></span> <span data-ttu-id="d40a8-120">эффективность toomaximize hello служба определяет и передает только hello блоков данных, которые были изменены с момента предыдущего резервного копирования hello.</span><span class="sxs-lookup"><span data-stu-id="d40a8-120">toomaximize efficiency, hello service identifies and transfers only hello blocks of data that have changed since hello previous backup.</span></span>

<span data-ttu-id="d40a8-121">После завершения передачи данных hello hello снимок удаляется и создается точка восстановления.</span><span class="sxs-lookup"><span data-stu-id="d40a8-121">When hello data transfer is complete, hello snapshot is removed and a recovery point is created.</span></span>


## <a name="create-a-backup"></a><span data-ttu-id="d40a8-122">Создание резервной копии</span><span class="sxs-lookup"><span data-stu-id="d40a8-122">Create a backup</span></span>
<span data-ttu-id="d40a8-123">Создание простого запланированного ежедневного резервного копирования tooa хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="d40a8-123">Create a simple scheduled daily backup tooa Recovery Services Vault.</span></span> 

1. <span data-ttu-id="d40a8-124">Войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d40a8-124">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="d40a8-125">Выберите в меню hello слева hello, **виртуальные машины**.</span><span class="sxs-lookup"><span data-stu-id="d40a8-125">In hello menu on hello left, select **Virtual machines**.</span></span> 
3. <span data-ttu-id="d40a8-126">Выберите из списка hello tooback ВМ вверх.</span><span class="sxs-lookup"><span data-stu-id="d40a8-126">From hello list, select a VM tooback up.</span></span>
4. <span data-ttu-id="d40a8-127">В колонке виртуальной Машины hello в hello **параметры** щелкните **резервного копирования**.</span><span class="sxs-lookup"><span data-stu-id="d40a8-127">On hello VM blade, in hello **Settings** section, click **Backup**.</span></span> <span data-ttu-id="d40a8-128">Hello **Enable backup** открывает колонку.</span><span class="sxs-lookup"><span data-stu-id="d40a8-128">hello **Enable backup** blade opens.</span></span>
5. <span data-ttu-id="d40a8-129">В **хранилище служб восстановления**, нажмите кнопку **создать новый** и укажите имя hello для нового хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="d40a8-129">In **Recovery Services vault**, click **Create new** and provide hello name for hello new vault.</span></span> <span data-ttu-id="d40a8-130">Новое хранилище создается в hello же группу ресурсов и расположение, как виртуальная машина hello.</span><span class="sxs-lookup"><span data-stu-id="d40a8-130">A new vault is created in hello same Resource Group and location as hello virtual machine.</span></span>
6. <span data-ttu-id="d40a8-131">Щелкните **Политика архивации**.</span><span class="sxs-lookup"><span data-stu-id="d40a8-131">Click **Backup policy**.</span></span> <span data-ttu-id="d40a8-132">В этом примере оставьте значения по умолчанию hello и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d40a8-132">For this example, keep hello defaults and click **OK**.</span></span>
7. <span data-ttu-id="d40a8-133">На hello **Enable backup** колонка, щелкните **включить архивацию**.</span><span class="sxs-lookup"><span data-stu-id="d40a8-133">On hello **Enable backup** blade, click **Enable Backup**.</span></span> <span data-ttu-id="d40a8-134">Это создает ежедневного резервного копирования на основе расписания по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="d40a8-134">This creates a daily backup based on hello default schedule.</span></span>
10. <span data-ttu-id="d40a8-135">toocreate начальной точки восстановления, на hello **резервного копирования** колонки щелкните **Архивировать сейчас**.</span><span class="sxs-lookup"><span data-stu-id="d40a8-135">toocreate an initial recovery point, on hello **Backup** blade click **Backup now**.</span></span>
11. <span data-ttu-id="d40a8-136">На hello **создать резервную копию** колонка, щелкните значок календаря hello, используйте hello календаря управления tooselect hello этой точки восстановления сохраняется и щелкните последний день **резервного копирования**.</span><span class="sxs-lookup"><span data-stu-id="d40a8-136">On hello **Backup Now** blade, click hello calendar icon, use hello calendar control tooselect hello last day this recovery point is retained, and click **Backup**.</span></span>
12. <span data-ttu-id="d40a8-137">В hello **резервного копирования** колонке ВМ, вы увидите hello количество точек восстановления, которые являются полными.</span><span class="sxs-lookup"><span data-stu-id="d40a8-137">In hello **Backup** blade for your VM, you will see hello number of recovery points that are complete.</span></span>

    ![Точки восстановления](./media/tutorial-backup-vms/backup-complete.png)
    
<span data-ttu-id="d40a8-139">Первая резервная копия Hello занимает примерно 20 минут.</span><span class="sxs-lookup"><span data-stu-id="d40a8-139">hello first backup takes about 20 minutes.</span></span> <span data-ttu-id="d40a8-140">Продолжить toohello следующей части этого руководства, после завершения резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="d40a8-140">Proceed toohello next part of this tutorial after your backup is finished.</span></span>

## <a name="recover-a-file"></a><span data-ttu-id="d40a8-141">восстановление файла;</span><span class="sxs-lookup"><span data-stu-id="d40a8-141">Recover a file</span></span>

<span data-ttu-id="d40a8-142">Случайно удалить или сделать файл tooa изменения, можно использовать файл hello toorecover восстановление файлов из резервного хранилища.</span><span class="sxs-lookup"><span data-stu-id="d40a8-142">If you accidentally delete or make changes tooa file, you can use File Recovery toorecover hello file from your backup vault.</span></span> <span data-ttu-id="d40a8-143">Восстановление файлов использует сценарий, который выполняется на ВМ, hello точки восстановления hello toomount как локальный диск.</span><span class="sxs-lookup"><span data-stu-id="d40a8-143">File Recovery uses a script that runs on hello VM, toomount hello recovery point as local drive.</span></span> <span data-ttu-id="d40a8-144">Эти диски останется подключенного 12 часов, можно скопировать файлы из точки восстановления hello и восстановить их toohello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="d40a8-144">These drives will remain mounted for 12 hours so that you can copy files from hello recovery point and restore them toohello VM.</span></span>  

<span data-ttu-id="d40a8-145">В этом примере показано, как toorecover hello файл образа, который используется в веб-страницы по умолчанию hello в IIS.</span><span class="sxs-lookup"><span data-stu-id="d40a8-145">In this example, we show how toorecover hello image file that is used in hello default web page for IIS.</span></span> 

1. <span data-ttu-id="d40a8-146">Откройте браузер и подключитесь toohello IP-адрес страницы IIS по умолчанию hello tooshow hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="d40a8-146">Open a browser and connect toohello IP address of hello VM tooshow hello default IIS page.</span></span>

    ![Веб-страница IIS по умолчанию](./media/tutorial-backup-vms/iis-working.png)

2. <span data-ttu-id="d40a8-148">Подключите toohello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="d40a8-148">Connect toohello VM.</span></span>
3. <span data-ttu-id="d40a8-149">Откройте на hello виртуальной Машины, **проводнике** удалить файл hello и навигацию too\inetpub\wwwroot **iisstart.png**.</span><span class="sxs-lookup"><span data-stu-id="d40a8-149">On hello VM, open **File Explorer** and navigate too\inetpub\wwwroot and delete hello file **iisstart.png**.</span></span>
4. <span data-ttu-id="d40a8-150">На локальном компьютере отсутствует toosee браузера hello обновления, hello изображение на странице IIS по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="d40a8-150">On your local computer, refresh hello browser toosee that hello image on hello default IIS page is gone.</span></span>

    ![Веб-страница IIS по умолчанию](./media/tutorial-backup-vms/iis-broken.png)

5. <span data-ttu-id="d40a8-152">На локальном компьютере, откройте новую вкладку и выберите hello hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d40a8-152">On your local computer, open a new tab and go hello hello [Azure portal](https://portal.azure.com).</span></span>
6. <span data-ttu-id="d40a8-153">Выберите в меню hello слева hello, **виртуальные машины** и список hello формы виртуальных Машин select hello.</span><span class="sxs-lookup"><span data-stu-id="d40a8-153">In hello menu on hello left, select **Virtual machines** and select hello VM form hello list.</span></span>
8. <span data-ttu-id="d40a8-154">В колонке виртуальной Машины hello в hello **параметры** щелкните **резервного копирования**.</span><span class="sxs-lookup"><span data-stu-id="d40a8-154">On hello VM blade, in hello **Settings** section, click **Backup**.</span></span> <span data-ttu-id="d40a8-155">Hello **резервного копирования** открывает колонку.</span><span class="sxs-lookup"><span data-stu-id="d40a8-155">hello **Backup** blade opens.</span></span> 
9. <span data-ttu-id="d40a8-156">Выберите в меню hello hello верхней части колонки hello, **восстановления файла**.</span><span class="sxs-lookup"><span data-stu-id="d40a8-156">In hello menu at hello top of hello blade, select **File Recovery**.</span></span> <span data-ttu-id="d40a8-157">Hello **восстановления файла** открывает колонку.</span><span class="sxs-lookup"><span data-stu-id="d40a8-157">hello **File Recovery** blade opens.</span></span>
10. <span data-ttu-id="d40a8-158">В **шаг 1: выберите точку восстановления**, выберите точку восстановления из раскрывающегося списка hello.</span><span class="sxs-lookup"><span data-stu-id="d40a8-158">In **Step 1: Select recovery point**, select a recovery point from hello drop-down.</span></span>
11. <span data-ttu-id="d40a8-159">В **шаг 2: загрузить скрипт toobrowse и восстанавливать файлы**, щелкните hello **загрузки исполняемого файла** кнопки.</span><span class="sxs-lookup"><span data-stu-id="d40a8-159">In **Step 2: Download script toobrowse and recover files**, click hello **Download Executable** button.</span></span> <span data-ttu-id="d40a8-160">Сохраните файл tooyour hello **загружает** папки.</span><span class="sxs-lookup"><span data-stu-id="d40a8-160">Save hello file tooyour **Downloads** folder.</span></span>
12. <span data-ttu-id="d40a8-161">На локальном компьютере, откройте **проводнике** и перейдите tooyour **загружает** папку и скопируйте hello загрузили файл .exe.</span><span class="sxs-lookup"><span data-stu-id="d40a8-161">On your local computer, open **File Explorer** and navigate tooyour **Downloads** folder and copy hello downloaded .exe file.</span></span> <span data-ttu-id="d40a8-162">Имя файла Hello стоять ваше имя виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="d40a8-162">hello filename will be prefixed by your VM name.</span></span> 
13. <span data-ttu-id="d40a8-163">На ВМ (через hello RDP-подключение) вставьте toohello файл .exe hello рабочего стола виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d40a8-163">On your VM (over hello RDP connection) paste hello .exe file toohello Desktop of your VM.</span></span> 
14. <span data-ttu-id="d40a8-164">Перейдите на рабочий стол toohello вашей виртуальной машины и дважды щелкните hello .exe.</span><span class="sxs-lookup"><span data-stu-id="d40a8-164">Navigate toohello desktop of your VM and double-click on hello .exe.</span></span> <span data-ttu-id="d40a8-165">Будет Запустите командную строку и затем подключите точки восстановления hello как общая папка, которую можно использовать.</span><span class="sxs-lookup"><span data-stu-id="d40a8-165">This will launch a command prompt and then mount hello recovery point as a file share that you can access.</span></span> <span data-ttu-id="d40a8-166">После завершения создания общего ресурса hello, введите **q** tooclose hello командной строки.</span><span class="sxs-lookup"><span data-stu-id="d40a8-166">When it is finished creating hello share, type **q** tooclose hello command prompt.</span></span>
15. <span data-ttu-id="d40a8-167">На ВМ откройте **проводнике** и перейдите toohello букву диска, который был использован для hello общей папки.</span><span class="sxs-lookup"><span data-stu-id="d40a8-167">On your VM, open **File Explorer** and navigate toohello drive letter that was used for hello file share.</span></span>
16. <span data-ttu-id="d40a8-168">Перемещение по too\inetpub\wwwroot и копирования **iisstart.png** из файла hello совместного использования и вставьте его в \inetpub\wwwroot.</span><span class="sxs-lookup"><span data-stu-id="d40a8-168">Navigate too\inetpub\wwwroot and copy **iisstart.png** from hello file share and paste it into \inetpub\wwwroot.</span></span> <span data-ttu-id="d40a8-169">Например скопируйте F:\inetpub\wwwroot\iisstart.png и вставьте его в файл hello toorecover c:\inetpub\wwwroot.</span><span class="sxs-lookup"><span data-stu-id="d40a8-169">For example, copy F:\inetpub\wwwroot\iisstart.png and paste it into c:\inetpub\wwwroot toorecover hello file.</span></span>
17. <span data-ttu-id="d40a8-170">На локальном компьютере, откройте вкладку браузера hello, где вы подключены toohello IP-адрес страница hello ВМ отображение приветствия IIS по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d40a8-170">On your local computer, open hello browser tab where you are connected toohello IP address of hello VM showing hello IIS default page.</span></span> <span data-ttu-id="d40a8-171">Нажмите клавиши CTRL + F5 страницы браузера toorefresh hello.</span><span class="sxs-lookup"><span data-stu-id="d40a8-171">Press CTRL + F5 toorefresh hello browser page.</span></span> <span data-ttu-id="d40a8-172">Теперь вы увидите, hello образ был восстановлен.</span><span class="sxs-lookup"><span data-stu-id="d40a8-172">You should now see that hello image has been restored.</span></span>
18. <span data-ttu-id="d40a8-173">На локальном компьютере, вернитесь к предыдущему окну toohello вкладка «браузер» для hello портал Azure и в **Step 3: отключить диски hello после восстановления** щелкните hello **отключить диски** кнопки.</span><span class="sxs-lookup"><span data-stu-id="d40a8-173">On your local computer, go back toohello browser tab for hello Azure portal and in **Step 3: Unmount hello disks after recovery** click hello **Unmount Disks** button.</span></span> <span data-ttu-id="d40a8-174">Если этот этап будет пропущен toodo, автоматически закрыть монтирования toohello hello подключения через 12 часов.</span><span class="sxs-lookup"><span data-stu-id="d40a8-174">If you forget toodo this step, hello connection toohello mountpoint is automatically close after 12 hours.</span></span> <span data-ttu-id="d40a8-175">После этих 12 часов необходимо toodownload новый toocreate сценария новая точка монтирования.</span><span class="sxs-lookup"><span data-stu-id="d40a8-175">After those 12 hours, you need toodownload a new script toocreate a new mountpoint.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d40a8-176">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d40a8-176">Next steps</span></span>

<span data-ttu-id="d40a8-177">Из этого руководства вы узнали, как выполнить следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="d40a8-177">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d40a8-178">Создание архива виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="d40a8-178">Create a backup of a VM</span></span>
> * <span data-ttu-id="d40a8-179">Планирование ежедневной архивации</span><span class="sxs-lookup"><span data-stu-id="d40a8-179">Schedule a daily backup</span></span>
> * <span data-ttu-id="d40a8-180">Восстановление файла из архива</span><span class="sxs-lookup"><span data-stu-id="d40a8-180">Restore a file from a backup</span></span>

<span data-ttu-id="d40a8-181">Переместить следующий учебник toolearn toohello о мониторинге виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="d40a8-181">Advance toohello next tutorial toolearn about monitoring virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d40a8-182">Мониторинг виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="d40a8-182">Monitor virtual machines</span></span>](tutorial-monitoring.md)









