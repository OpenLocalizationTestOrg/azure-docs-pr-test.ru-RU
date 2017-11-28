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
ms.openlocfilehash: d0cbf7883a8737bcb10e9dd251c9792a12993f77
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="back-up-linux--virtual-machines-in-azure"></a><span data-ttu-id="81045-103">Архивация виртуальных машин Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="81045-103">Back up Linux  virtual machines in Azure</span></span>

<span data-ttu-id="81045-104">Защиту данных можно обеспечить, выполняя архивацию через регулярные интервалы.</span><span class="sxs-lookup"><span data-stu-id="81045-104">You can protect your data by taking backups at regular intervals.</span></span> <span data-ttu-id="81045-105">Служба архивации Azure создает точки восстановления, которые хранятся в геоизбыточных хранилищах восстановления.</span><span class="sxs-lookup"><span data-stu-id="81045-105">Azure Backup creates recovery points that are stored in geo-redundant recovery vaults.</span></span> <span data-ttu-id="81045-106">Используя точку восстановления, можно восстановить всю виртуальную машину или только определенные файлы.</span><span class="sxs-lookup"><span data-stu-id="81045-106">When you restore from a recovery point, you can restore the whole VM or just specific files.</span></span> <span data-ttu-id="81045-107">В этой статье описана процедура восстановления одного файла на виртуальной машине Linux с помощью nginx.</span><span class="sxs-lookup"><span data-stu-id="81045-107">This article explains how to restore a single file to a Linux VM running nginx.</span></span> <span data-ttu-id="81045-108">Если у вас еще нет виртуальной машины, создайте ее, используя сведения, приведенные в статье [Создание виртуальной машины Linux с помощью Azure CLI](quick-create-cli.md).</span><span class="sxs-lookup"><span data-stu-id="81045-108">If you don't already have a VM to use, you can create one using the [Linux quickstart](quick-create-cli.md).</span></span> <span data-ttu-id="81045-109">Из этого руководства вы узнали, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="81045-109">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="81045-110">Создание архива виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="81045-110">Create a backup of a VM</span></span>
> * <span data-ttu-id="81045-111">Планирование ежедневной архивации</span><span class="sxs-lookup"><span data-stu-id="81045-111">Schedule a daily backup</span></span>
> * <span data-ttu-id="81045-112">Восстановление файла из архива</span><span class="sxs-lookup"><span data-stu-id="81045-112">Restore a file from a backup</span></span>



## <a name="backup-overview"></a><span data-ttu-id="81045-113">Обзор службы архивации</span><span class="sxs-lookup"><span data-stu-id="81045-113">Backup overview</span></span>

<span data-ttu-id="81045-114">Служба архивации Azure запускает архивацию. При этом модуль архивации создает снимок текущего состояния.</span><span class="sxs-lookup"><span data-stu-id="81045-114">When the Azure Backup service initiates a backup, it triggers the backup extension to take a point-in-time snapshot.</span></span> <span data-ttu-id="81045-115">Служба архивации Azure использует расширение _VMSnapshotLinux_ в Linux.</span><span class="sxs-lookup"><span data-stu-id="81045-115">The Azure Backup service uses the _VMSnapshotLinux_ extension in Linux.</span></span> <span data-ttu-id="81045-116">Расширение устанавливается во время первой архивации виртуальной машины, если виртуальная машина запущена.</span><span class="sxs-lookup"><span data-stu-id="81045-116">The extension is installed during the first VM backup if the VM is running.</span></span> <span data-ttu-id="81045-117">Если виртуальная машина не запущена, служба резервного копирования создает моментальный снимок базового хранилища (так как операции записи в приложении не выполняются, пока виртуальная машина остановлена).</span><span class="sxs-lookup"><span data-stu-id="81045-117">If the VM is not running, the Backup service takes a snapshot of the underlying storage (since no application writes occur while the VM is stopped).</span></span>

<span data-ttu-id="81045-118">По умолчанию Azure Backup создает резервную копию с согласованным состоянием файловой системы для виртуальной машины Linux, но эту службу можно настроить для создания [согласованных с приложениями резервных копий с помощью предварительного и последующего сценариев](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent).</span><span class="sxs-lookup"><span data-stu-id="81045-118">By default, Azure Backup takes a file system consistent backup for Linux VM but it can be configured to take [application consistent backup using pre-script and post-script framework](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent).</span></span> <span data-ttu-id="81045-119">После создания моментального снимка службой архивации Azure данные передаются в хранилище.</span><span class="sxs-lookup"><span data-stu-id="81045-119">Once the Azure Backup service takes the snapshot, the data is transferred to the vault.</span></span> <span data-ttu-id="81045-120">Для повышения эффективности служба анализирует блоки данных и передает только те из них, которые были изменены с момента предыдущего резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="81045-120">To maximize efficiency, the service identifies and transfers only the blocks of data that have changed since the previous backup.</span></span>

<span data-ttu-id="81045-121">После передачи данных служба удаляет моментальный снимок и создает точку восстановления.</span><span class="sxs-lookup"><span data-stu-id="81045-121">When the data transfer is complete, the snapshot is removed and a recovery point is created.</span></span>


## <a name="create-a-backup"></a><span data-ttu-id="81045-122">Создание резервной копии</span><span class="sxs-lookup"><span data-stu-id="81045-122">Create a backup</span></span>
<span data-ttu-id="81045-123">Создайте простую операцию ежедневной архивации в хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="81045-123">Create a simple scheduled daily backup to a Recovery Services Vault.</span></span> 

1. <span data-ttu-id="81045-124">Выполните вход на [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="81045-124">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="81045-125">В меню слева выберите **Виртуальные машины**.</span><span class="sxs-lookup"><span data-stu-id="81045-125">In the menu on the left, select **Virtual machines**.</span></span> 
3. <span data-ttu-id="81045-126">В этом списке выберите нужную виртуальную машину для архивации.</span><span class="sxs-lookup"><span data-stu-id="81045-126">From the list, select a VM to back up.</span></span>
4. <span data-ttu-id="81045-127">В колонке виртуальной машины в разделе **Параметры** щелкните **Архивация**.</span><span class="sxs-lookup"><span data-stu-id="81045-127">On the VM blade, in the **Settings** section, click **Backup**.</span></span> <span data-ttu-id="81045-128">Откроется колонка **Включение архивации**.</span><span class="sxs-lookup"><span data-stu-id="81045-128">The **Enable backup** blade opens.</span></span>
5. <span data-ttu-id="81045-129">В **хранилище служб восстановления** щелкните **Создать** и укажите имя нового хранилища.</span><span class="sxs-lookup"><span data-stu-id="81045-129">In **Recovery Services vault**, click **Create new** and provide the name for the new vault.</span></span> <span data-ttu-id="81045-130">Новое хранилище создается в той же группе ресурсов и в том же расположении, что и виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="81045-130">A new vault is created in the same Resource Group and location as the virtual machine.</span></span>
6. <span data-ttu-id="81045-131">Щелкните **Политика архивации**.</span><span class="sxs-lookup"><span data-stu-id="81045-131">Click **Backup policy**.</span></span> <span data-ttu-id="81045-132">Для этого примера оставьте значения по умолчанию и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="81045-132">For this example, keep the defaults and click **OK**.</span></span>
7. <span data-ttu-id="81045-133">В колонке **Включение архивации** щелкните **Включить архивацию**.</span><span class="sxs-lookup"><span data-stu-id="81045-133">On the **Enable backup** blade, click **Enable Backup**.</span></span> <span data-ttu-id="81045-134">При этом создается задание ежедневной архивации на основе расписания по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="81045-134">This creates a daily backup based on the default schedule.</span></span>
10. <span data-ttu-id="81045-135">Для создания начальной точки восстановления в колонке **Архивация** щелкните **Создать архив**.</span><span class="sxs-lookup"><span data-stu-id="81045-135">To create an initial recovery point, on the **Backup** blade click **Backup now**.</span></span>
11. <span data-ttu-id="81045-136">В колонке **Создать архив** щелкните значок календаря и с помощью элементов управления календарем выберите последний день сохранения этой точки восстановления, а затем нажмите кнопку **Архивировать**.</span><span class="sxs-lookup"><span data-stu-id="81045-136">On the **Backup Now** blade, click the calendar icon, use the calendar control to select the last day this recovery point is retained, and click **Backup**.</span></span>
12. <span data-ttu-id="81045-137">В колонке **Архивировать** виртуальной машины вы увидите количество выполненных точек восстановления.</span><span class="sxs-lookup"><span data-stu-id="81045-137">In the **Backup** blade for your VM, you will see the number of recovery points that are complete.</span></span>

    ![Точки восстановления](./media/tutorial-backup-vms/backup-complete.png)

<span data-ttu-id="81045-139">Первая архивация длится около 20 минут.</span><span class="sxs-lookup"><span data-stu-id="81045-139">The first backup takes about 20 minutes.</span></span> <span data-ttu-id="81045-140">После завершения архивации перейдите к следующей части этого руководства.</span><span class="sxs-lookup"><span data-stu-id="81045-140">Proceed to the next part of this tutorial after your backup is finished.</span></span>

## <a name="restore-a-file"></a><span data-ttu-id="81045-141">Восстановление файла</span><span class="sxs-lookup"><span data-stu-id="81045-141">Restore a file</span></span>

<span data-ttu-id="81045-142">Если вы случайно удалили файл или внесли в него ненужные изменения, его можно восстановить из резервного хранилища, используя функцию восстановления файлов.</span><span class="sxs-lookup"><span data-stu-id="81045-142">If you accidentally delete or make changes to a file, you can use File Recovery to recover the file from your backup vault.</span></span> <span data-ttu-id="81045-143">Восстановление файлов запускает скрипты на виртуальной машине, чтобы подключить точку восстановления в качестве локального диска.</span><span class="sxs-lookup"><span data-stu-id="81045-143">File Recovery uses a script that runs on the VM, to mount the recovery point as local drive.</span></span> <span data-ttu-id="81045-144">Эти диски остаются подключенными в течение 12 часов, чтобы вы могли скопировать файлы из точки восстановления и восстановить их на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="81045-144">These drives will remain mounted for 12 hours so that you can copy files from the recovery point and restore them to the VM.</span></span>  

<span data-ttu-id="81045-145">В этом примере показано, как восстановить веб-страницу nginx по умолчанию /var/www/html/index.nginx-debian.html.</span><span class="sxs-lookup"><span data-stu-id="81045-145">In this example, we show how to recover the default nginx web page /var/www/html/index.nginx-debian.html.</span></span> <span data-ttu-id="81045-146">Общедоступный IP-адрес виртуальной машины в этом примере — *13.69.75.209*.</span><span class="sxs-lookup"><span data-stu-id="81045-146">The public IP address of our VM in this example is *13.69.75.209*.</span></span> <span data-ttu-id="81045-147">IP-адрес виртуальной машины можно определить, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="81045-147">You can find the IP address of your vm using:</span></span>

 ```bash 
 az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
 ```

 
1. <span data-ttu-id="81045-148">На локальном компьютере откройте браузер и введите общедоступный IP-адрес виртуальной машины, чтобы увидеть веб-страницу nginx по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="81045-148">On your local computer, open a browser and type in the public IP address of your VM to see the default nginx web page.</span></span>

    ![Веб-страница nginx по умолчанию](./media/tutorial-backup-vms/nginx-working.png)

1. <span data-ttu-id="81045-150">Подключитесь к виртуальной машине по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="81045-150">SSH into your VM.</span></span>

    ```bash
    ssh 13.69.75.209
    ```
2. <span data-ttu-id="81045-151">Удалите /var/www/html/index.nginx-debian.html.</span><span class="sxs-lookup"><span data-stu-id="81045-151">Delete /var/www/html/index.nginx-debian.html.</span></span>

    ```bash
    sudo rm /var/www/html/index.nginx-debian.html
    ```
    
4. <span data-ttu-id="81045-152">На локальном компьютере обновите браузер, нажав сочетание клавиш CTRL+F5, чтобы увидеть, что страница nginx по умолчанию отсутствует.</span><span class="sxs-lookup"><span data-stu-id="81045-152">On your local computer, refresh the browser by hitting CTRL + F5 to see that default nginx page is gone.</span></span>

    ![Веб-страница nginx по умолчанию](./media/tutorial-backup-vms/nginx-broken.png)
    
1. <span data-ttu-id="81045-154">На локальном компьютере войдите на [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="81045-154">On your local computer, sign in to the [Azure portal](https://portal.azure.com/).</span></span>
6. <span data-ttu-id="81045-155">В меню слева выберите **Виртуальные машины**.</span><span class="sxs-lookup"><span data-stu-id="81045-155">In the menu on the left, select **Virtual machines**.</span></span> 
7. <span data-ttu-id="81045-156">Выберите пользователя из списка.</span><span class="sxs-lookup"><span data-stu-id="81045-156">From the list, select the VM.</span></span>
8. <span data-ttu-id="81045-157">В колонке виртуальной машины в разделе **Параметры** щелкните **Архивация**.</span><span class="sxs-lookup"><span data-stu-id="81045-157">On the VM blade, in the **Settings** section, click **Backup**.</span></span> <span data-ttu-id="81045-158">Откроется колонка **Архивация**.</span><span class="sxs-lookup"><span data-stu-id="81045-158">The **Backup** blade opens.</span></span> 
9. <span data-ttu-id="81045-159">В меню в верхней части колонки выберите **Восстановление файлов**.</span><span class="sxs-lookup"><span data-stu-id="81045-159">In the menu at the top of the blade, select **File Recovery**.</span></span> <span data-ttu-id="81045-160">Откроется колонка **Восстановление файлов**.</span><span class="sxs-lookup"><span data-stu-id="81045-160">The **File Recovery** blade opens.</span></span>
10. <span data-ttu-id="81045-161">В разделе **Шаг 1. Выбор точки восстановления** выберите точку восстановления из раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="81045-161">In **Step 1: Select recovery point**, select a recovery point from the drop-down.</span></span>
11. <span data-ttu-id="81045-162">В разделе **Шаг 2. Скачивание скрипта для просмотра и восстановления файлов** нажмите кнопку **Скачать исполняемый файл**.</span><span class="sxs-lookup"><span data-stu-id="81045-162">In **Step 2: Download script to browse and recover files**, click the **Download Executable** button.</span></span> <span data-ttu-id="81045-163">Сохраните скачанный файл на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="81045-163">Save the downloaded file to your local computer.</span></span>
7. <span data-ttu-id="81045-164">Щелкните **Скачать скрипт** для скачивания файла скрипта в локальное расположение.</span><span class="sxs-lookup"><span data-stu-id="81045-164">Click **Download script** to download the script file locally.</span></span>
8. <span data-ttu-id="81045-165">Откройте строку Bash и введите следующую команду, заменив *Linux_myVM_05-05-2017.sh* правильным путем и именем файла скрипта, который вы скачали, замените *azureuser* именем пользователя виртуальной машины, а *13.69.75.209* — общедоступным IP-адресом виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="81045-165">Open a Bash prompt and type the following, replacing *Linux_myVM_05-05-2017.sh* with the correct path and filename for the script that you downloaded, *azureuser* with the username for the VM and *13.69.75.209* with the public IP address for your VM.</span></span>
    
    ```bash
    scp Linux_myVM_05-05-2017.sh azureuser@13.69.75.209:
    ```
    
9. <span data-ttu-id="81045-166">На локальном компьютере установите SSH-подключение к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="81045-166">On your local computer, open an SSH connection to the VM.</span></span>

    ```bash
    ssh 13.69.75.209
    ```
    
10. <span data-ttu-id="81045-167">На виртуальной машине добавьте разрешения на выполнение для файла скрипта.</span><span class="sxs-lookup"><span data-stu-id="81045-167">On your VM, add execute permissions to the script file.</span></span>

    ```bash
    chmod +x Linux_myVM_05-05-2017.sh
    ```
    
11. <span data-ttu-id="81045-168">На виртуальной машине выполните скрипт, чтобы подключить точку восстановления в качестве файловой системы.</span><span class="sxs-lookup"><span data-stu-id="81045-168">On your VM, run the script to mount the recovery point as a filesystem.</span></span>

    ```bash
    ./Linux_myVM_05-05-2017.sh
    ```
    
12. <span data-ttu-id="81045-169">В результате выполнения скрипта вы получите путь к точке подключения.</span><span class="sxs-lookup"><span data-stu-id="81045-169">The output from the script gives you the path for the mount point.</span></span> <span data-ttu-id="81045-170">Результат будет выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="81045-170">The output looks similar to this:</span></span>

    ```bash
    Microsoft Azure VM Backup - File Recovery
    ______________________________________________
                          
    Connecting to recovery point using ISCSI service...
    
    Connection succeeded!
    
    Please wait while we attach volumes of the recovery point to this machine...
                         
    ************ Volumes of the recovery point and their mount paths on this machine ************

    Sr.No.  |  Disk  |  Volume  |  MountPath 

    1)  | /dev/sdc  |  /dev/sdc1  |  /home/azureuser/myVM-20170505191055/Volume1

    ************ Open File Explorer to browse for files. ************

    After recovery, to remove the disks and close the connection to the recovery point, please click 'Unmount Disks' in step 3 of the portal.

    Please enter 'q/Q' to exit...
    ```

12. <span data-ttu-id="81045-171">На виртуальной машине скопируйте веб-страницу nginx по умолчанию из точки подключения обратно в расположение, где был удален файл.</span><span class="sxs-lookup"><span data-stu-id="81045-171">On your VM, copy the nginx default web page from the mount point back to where you deleted the file.</span></span>

    ```bash
    sudo cp ~/myVM-20170505191055/Volume1/var/www/html/index.nginx-debian.html /var/www/html/
    ```
    
17. <span data-ttu-id="81045-172">На локальном компьютере откройте вкладку браузера с подключением к IP-адресу виртуальной машины, на которой отображается страница nginx по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="81045-172">On your local computer, open the browser tab where you are connected to the IP address of the VM showing the nginx default page.</span></span> <span data-ttu-id="81045-173">Нажмите CTRL+F5, чтобы обновить страницу в браузере.</span><span class="sxs-lookup"><span data-stu-id="81045-173">Press CTRL + F5 to refresh the browser page.</span></span> <span data-ttu-id="81045-174">Страница по умолчанию должна снова заработать.</span><span class="sxs-lookup"><span data-stu-id="81045-174">You should now see that the default page is working again.</span></span>

    ![Веб-страница nginx по умолчанию](./media/tutorial-backup-vms/nginx-working.png)

18. <span data-ttu-id="81045-176">На локальном компьютере вернитесь к вкладке браузера портала Azure и в разделе **Шаг 3. Отключение дисков после восстановления** нажмите кнопку **Отключить диски**.</span><span class="sxs-lookup"><span data-stu-id="81045-176">On your local computer, go back to the browser tab for the Azure portal and in **Step 3: Unmount the disks after recovery** click the **Unmount Disks** button.</span></span> <span data-ttu-id="81045-177">Если вы забудете сделать это, соединение с точкой подключения будет автоматически закрыто через 12 часов.</span><span class="sxs-lookup"><span data-stu-id="81045-177">If you forget to do this step, the connection to the mountpoint is automatically close after 12 hours.</span></span> <span data-ttu-id="81045-178">После этих 12 часов для создания нового соединения с точкой подключения потребуется скачать новый скрипт.</span><span class="sxs-lookup"><span data-stu-id="81045-178">After those 12 hours, you need to download a new script to create a new mountpoint.</span></span>


## <a name="next-steps"></a><span data-ttu-id="81045-179">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="81045-179">Next steps</span></span>

<span data-ttu-id="81045-180">Из этого руководства вы узнали, как выполнить следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="81045-180">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="81045-181">Создание архива виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="81045-181">Create a backup of a VM</span></span>
> * <span data-ttu-id="81045-182">Планирование ежедневной архивации</span><span class="sxs-lookup"><span data-stu-id="81045-182">Schedule a daily backup</span></span>
> * <span data-ttu-id="81045-183">Восстановление файла из архива</span><span class="sxs-lookup"><span data-stu-id="81045-183">Restore a file from a backup</span></span>

<span data-ttu-id="81045-184">Перейдите к следующему руководству, чтобы узнать о мониторинге виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="81045-184">Advance to the next tutorial to learn about monitoring virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="81045-185">Мониторинг виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="81045-185">Monitor virtual machines</span></span>](tutorial-monitoring.md)

