---
title: "aaaReset локальный пароль Windows без агента Azure | Документы Microsoft"
description: "Как tooreset hello пароль локальной учетной записи пользователя Windows, когда hello Azure гостевой агент не установлен или не работает на виртуальной Машине"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: cf353dd3-89c9-47f6-a449-f874f0957013
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 04/07/2017
ms.author: iainfou
ms.openlocfilehash: c559c31ea142f9cf50d2c5b6182c5355fec9bac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-local-windows-password-for-azure-vm"></a><span data-ttu-id="237b1-103">Как tooreset локальный пароль Windows для виртуальной Машины Azure</span><span class="sxs-lookup"><span data-stu-id="237b1-103">How tooreset local Windows password for Azure VM</span></span>
<span data-ttu-id="237b1-104">Вы можете сбросить пароль локального Windows hello виртуальной машины в Azure с помощью hello [портал Azure или Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) предоставляемых установлен агент Azure guest hello.</span><span class="sxs-lookup"><span data-stu-id="237b1-104">You can reset hello local Windows password of a VM in Azure using hello [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) provided hello Azure guest agent is installed.</span></span> <span data-ttu-id="237b1-105">Этот метод является основным способом hello tooreset пароль для виртуальной Машины Azure.</span><span class="sxs-lookup"><span data-stu-id="237b1-105">This method is hello primary way tooreset a password for an Azure VM.</span></span> <span data-ttu-id="237b1-106">При возникновении проблем с hello гостевой агент Azure не отвечает, было пройдено tooinstall после отправки пользовательского образа, можно вручную сбросить пароль Windows.</span><span class="sxs-lookup"><span data-stu-id="237b1-106">If you encounter issues with hello Azure guest agent not responding, or failing tooinstall after uploading a custom image, you can manually reset a Windows password.</span></span> <span data-ttu-id="237b1-107">В этой статье указаны как tooreset пароль локальной учетной записи путем присоединения hello tooanother виртуального диска исходной операционной системы виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="237b1-107">This article details how tooreset a local account password by attaching hello source OS virtual disk tooanother VM.</span></span> 

> [!WARNING]
> <span data-ttu-id="237b1-108">Этот метод следует использовать только в крайнем случае.</span><span class="sxs-lookup"><span data-stu-id="237b1-108">Only use this process as a last resort.</span></span> <span data-ttu-id="237b1-109">По возможности используйте tooreset пароля с помощью hello [портал Azure или Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) первой.</span><span class="sxs-lookup"><span data-stu-id="237b1-109">Always try tooreset a password using hello [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) first.</span></span>
> 
> 

## <a name="overview-of-hello-process"></a><span data-ttu-id="237b1-110">Общие сведения о процессе hello</span><span class="sxs-lookup"><span data-stu-id="237b1-110">Overview of hello process</span></span>
<span data-ttu-id="237b1-111">Hello основные действия по выполнению локальный пароль, сброс для виртуальной Машины Windows в Azure, если отсутствует агент Azure guest toohello доступа выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="237b1-111">hello core steps for performing a local password reset for a Windows VM in Azure when there is no access toohello Azure guest agent is as follows:</span></span>

* <span data-ttu-id="237b1-112">Удалите hello исходной виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="237b1-112">Delete hello source VM.</span></span> <span data-ttu-id="237b1-113">виртуальные диски Hello сохраняются.</span><span class="sxs-lookup"><span data-stu-id="237b1-113">hello virtual disks are retained.</span></span>
* <span data-ttu-id="237b1-114">Присоединение tooanother диска ОС ВМ источника hello виртуальной Машины на hello местоположения в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="237b1-114">Attach hello source VM's OS disk tooanother VM on hello same location within your Azure subscription.</span></span> <span data-ttu-id="237b1-115">Эта VM является ссылка tooas hello, устранение неполадок виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="237b1-115">This VM is referred tooas hello troubleshooting VM.</span></span>
* <span data-ttu-id="237b1-116">С помощью hello, устранение неполадок виртуальной Машины, создайте некоторые файлы конфигурации на диске операционной системы виртуальной Машины источника hello.</span><span class="sxs-lookup"><span data-stu-id="237b1-116">Using hello troubleshooting VM, create some config files on hello source VM's OS disk.</span></span>
* <span data-ttu-id="237b1-117">Отсоедините диск операционной системы виртуальной Машины hello от hello, устранение неполадок виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="237b1-117">Detach hello VM's OS disk from hello troubleshooting VM.</span></span>
* <span data-ttu-id="237b1-118">Используйте toocreate шаблона диспетчера ресурсов виртуальной Машины, с помощью hello исходный виртуальный диск.</span><span class="sxs-lookup"><span data-stu-id="237b1-118">Use a Resource Manager template toocreate a VM, using hello original virtual disk.</span></span>
* <span data-ttu-id="237b1-119">При hello новой виртуальной Машины загружается, hello файлов конфигурации вы создаете обновления hello пароля пользователя требуется hello.</span><span class="sxs-lookup"><span data-stu-id="237b1-119">When hello new VM boots, hello config files you create update hello password of hello required user.</span></span>

## <a name="detailed-steps"></a><span data-ttu-id="237b1-120">Подробные инструкции</span><span class="sxs-lookup"><span data-stu-id="237b1-120">Detailed steps</span></span>
<span data-ttu-id="237b1-121">По возможности используйте tooreset пароля с помощью hello [портал Azure или Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) перед попыткой hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="237b1-121">Always try tooreset a password using hello [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before trying hello following steps.</span></span> <span data-ttu-id="237b1-122">Прежде чем начать, обязательно сохраните резервную копию виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="237b1-122">Make sure you have a backup of your VM before you start.</span></span> 

1. <span data-ttu-id="237b1-123">Удалить hello затронутых ВМ на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="237b1-123">Delete hello affected VM in Azure portal.</span></span> <span data-ttu-id="237b1-124">Удаление hello ВМ только удаляет метаданные hello, ссылку на hello hello ВМ в Azure.</span><span class="sxs-lookup"><span data-stu-id="237b1-124">Deleting hello VM only deletes hello metadata, hello reference of hello VM within Azure.</span></span> <span data-ttu-id="237b1-125">виртуальные диски Hello сохраняются при удалении hello виртуальной Машины:</span><span class="sxs-lookup"><span data-stu-id="237b1-125">hello virtual disks are retained when hello VM is deleted:</span></span>
   
   * <span data-ttu-id="237b1-126">Выберите hello виртуальной Машины в hello портала Azure щелкните *удалить*:</span><span class="sxs-lookup"><span data-stu-id="237b1-126">Select hello VM in hello Azure portal, click *Delete*:</span></span>
     
     ![Удаление существующей виртуальной машины](./media/reset-local-password-without-agent/delete_vm.png)
2. <span data-ttu-id="237b1-128">Присоедините диск toohello hello исходной Виртуальной машины операционной системы, устранение неполадок виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="237b1-128">Attach hello source VM’s OS disk toohello troubleshooting VM.</span></span> <span data-ttu-id="237b1-129">Привет, устранение неполадок виртуальной Машины должны находиться в hello же регионе, что диск операционной системы виртуальной Машины источника hello (такие как `West US`):</span><span class="sxs-lookup"><span data-stu-id="237b1-129">hello troubleshooting VM must be in hello same region as hello source VM's OS disk (such as `West US`):</span></span>
   
   * <span data-ttu-id="237b1-130">Выберите hello, устранение неполадок виртуальной Машины в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="237b1-130">Select hello troubleshooting VM in hello Azure portal.</span></span> <span data-ttu-id="237b1-131">Щелкните *Диски* | *Подключить существующий*:</span><span class="sxs-lookup"><span data-stu-id="237b1-131">Click *Disks* | *Attach existing*:</span></span>
     
     ![Подключение существующего диска](./media/reset-local-password-without-agent/disks_attach_existing.png)
     
     <span data-ttu-id="237b1-133">Выберите *VHD-файл* и выберите учетную запись хранилища hello, который содержит источник виртуальной Машины:</span><span class="sxs-lookup"><span data-stu-id="237b1-133">Select *VHD File* and then select hello storage account that contains your source VM:</span></span>
     
     ![Выбор учетной записи хранения](./media/reset-local-password-without-agent/disks_select_storageaccount.PNG)
     
     <span data-ttu-id="237b1-135">Выберите исходный контейнер hello.</span><span class="sxs-lookup"><span data-stu-id="237b1-135">Select hello source container.</span></span> <span data-ttu-id="237b1-136">обычно является Hello исходный контейнер *виртуальные жесткие диски*:</span><span class="sxs-lookup"><span data-stu-id="237b1-136">hello source container is typically *vhds*:</span></span>
     
     ![Выбор контейнера хранилища](./media/reset-local-password-without-agent/disks_select_container.png)
     
     <span data-ttu-id="237b1-138">Выберите tooattach виртуального жесткого диска ОС hello.</span><span class="sxs-lookup"><span data-stu-id="237b1-138">Select hello OS vhd tooattach.</span></span> <span data-ttu-id="237b1-139">Нажмите кнопку *выберите* toocomplete hello процесс:</span><span class="sxs-lookup"><span data-stu-id="237b1-139">Click *Select* toocomplete hello process:</span></span>
     
     ![Выбор исходного виртуального диска](./media/reset-local-password-without-agent/disks_select_source_vhd.png)
3. <span data-ttu-id="237b1-141">Подключение toohello Устранение неполадок виртуальной Машины с помощью удаленного рабочего стола и убедитесь, что диск операционной системы виртуальной Машины источника hello отображается:</span><span class="sxs-lookup"><span data-stu-id="237b1-141">Connect toohello troubleshooting VM using Remote Desktop and ensure hello source VM's OS disk is visible:</span></span>
   
   * <span data-ttu-id="237b1-142">Выберите hello, устранение неполадок виртуальной Машины в hello портал Azure и нажмите кнопку *Connect*.</span><span class="sxs-lookup"><span data-stu-id="237b1-142">Select hello troubleshooting VM in hello Azure portal and click *Connect*.</span></span>
   * <span data-ttu-id="237b1-143">Откройте файл RDP hello, загрузки.</span><span class="sxs-lookup"><span data-stu-id="237b1-143">Open hello RDP file that downloads.</span></span> <span data-ttu-id="237b1-144">Введите hello пользователя и пароль для hello, устранение неполадок виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="237b1-144">Enter hello username and password of hello troubleshooting VM.</span></span>
   * <span data-ttu-id="237b1-145">В проводнике найдите диск данных hello присоединенной.</span><span class="sxs-lookup"><span data-stu-id="237b1-145">In File Explorer, look for hello data disk you attached.</span></span> <span data-ttu-id="237b1-146">Если hello исходный виртуальный жесткий ДИСК Виртуальной машины находится hello toohello диск, подключенный только данные, устранение неполадок виртуальной Машины, он должен быть hello диска «f:»:</span><span class="sxs-lookup"><span data-stu-id="237b1-146">If hello source VM’s VHD is hello only data disk attached toohello troubleshooting VM, it should be hello F: drive:</span></span>
     
     ![Просмотр подключенного диска данных](./media/reset-local-password-without-agent/troubleshooting_vm_fileexplorer.png)
4. <span data-ttu-id="237b1-148">Создание `gpt.ini` в `\Windows\System32\GroupPolicy` на диске hello исходной Виртуальной машины (если существует gpt.ini, переименуйте toogpt.ini.bak):</span><span class="sxs-lookup"><span data-stu-id="237b1-148">Create `gpt.ini` in `\Windows\System32\GroupPolicy` on hello source VM’s drive (if gpt.ini exists, rename toogpt.ini.bak):</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="237b1-149">Убедитесь, что не случайно создать hello следующие файлы в C:\Windows, hello диска ОС для hello, устранение неполадок виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="237b1-149">Make sure that you do not accidentally create hello following files in C:\Windows, hello OS drive for hello troubleshooting VM.</span></span> <span data-ttu-id="237b1-150">Создайте следующие файлы на диске hello ОС для виртуальной Машины, которой подключен как диск с данными источника hello.</span><span class="sxs-lookup"><span data-stu-id="237b1-150">Create hello following files in hello OS drive for your source VM that is attached as a data disk.</span></span>
   > 
   > 
   
   * <span data-ttu-id="237b1-151">Добавьте следующие строки в hello hello `gpt.ini` созданный файл:</span><span class="sxs-lookup"><span data-stu-id="237b1-151">Add hello following lines into hello `gpt.ini` file you created:</span></span>
     
     ```
     [General]
     gPCFunctionalityVersion=2
     gPCMachineExtensionNames=[{42B5FAAE-6536-11D2-AE5A-0000F87571E3}{40B6664F-4972-11D1-A7CA-0000F87571E3}]
     Version=1
     ```
     
     ![Создание файла gpt.ini](./media/reset-local-password-without-agent/create_gpt_ini.png)
5. <span data-ttu-id="237b1-153">Создайте файл `scripts.ini` в расположении `\Windows\System32\GroupPolicy\Machine\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="237b1-153">Create `scripts.ini` in `\Windows\System32\GroupPolicy\Machine\Scripts`.</span></span> <span data-ttu-id="237b1-154">Убедитесь, что отображаются скрытые папки.</span><span class="sxs-lookup"><span data-stu-id="237b1-154">Make sure hidden folders are shown.</span></span> <span data-ttu-id="237b1-155">При необходимости создайте hello `Machine` или `Scripts` папки.</span><span class="sxs-lookup"><span data-stu-id="237b1-155">If needed, create hello `Machine` or `Scripts` folders.</span></span>
   
   * <span data-ttu-id="237b1-156">Добавьте следующие строки hello hello `scripts.ini` созданный файл:</span><span class="sxs-lookup"><span data-stu-id="237b1-156">Add hello following lines hello `scripts.ini` file you created:</span></span>
     
     ```
     [Startup]
     0CmdLine=C:\Windows\System32\FixAzureVM.cmd
     0Parameters=
     ```
     
     ![Создание файла scripts.ini](./media/reset-local-password-without-agent/create_scripts_ini.png)
6. <span data-ttu-id="237b1-158">Создание `FixAzureVM.cmd` в `\Windows\System32` с hello следующие содержимое, заменив `<username>` и `<newpassword>` собственными значениями:</span><span class="sxs-lookup"><span data-stu-id="237b1-158">Create `FixAzureVM.cmd` in `\Windows\System32` with hello following contents, replacing `<username>` and `<newpassword>` with your own values:</span></span>
   
    ```
    net user <username> <newpassword> /add
    net localgroup administrators <username> /add
    net localgroup "remote desktop users" <username> /add

    ```

    ![Создание файла FixAzureVM.cmd](./media/reset-local-password-without-agent/create_fixazure_cmd.png)
   
    <span data-ttu-id="237b1-160">При определении нового пароля hello, должен удовлетворять требованиям к сложности пароля hello настроены для виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="237b1-160">You must meet hello configured password complexity requirements for your VM when defining hello new password.</span></span>
7. <span data-ttu-id="237b1-161">На портале Azure отсоедините диск hello от hello, устранение неполадок виртуальной Машины:</span><span class="sxs-lookup"><span data-stu-id="237b1-161">In Azure portal, detach hello disk from hello troubleshooting VM:</span></span>
   
   * <span data-ttu-id="237b1-162">Выберите hello, устранение неполадок виртуальной Машины в hello портал Azure, щелкните *дисков*.</span><span class="sxs-lookup"><span data-stu-id="237b1-162">Select hello troubleshooting VM in hello Azure portal, click *Disks*.</span></span>
   * <span data-ttu-id="237b1-163">Диск данных выберите hello присоединенные на шаге 2, нажмите кнопку *отсоединения*:</span><span class="sxs-lookup"><span data-stu-id="237b1-163">Select hello data disk attached in step 2, click *Detach*:</span></span>
     
     ![Отключение диска](./media/reset-local-password-without-agent/detach_disk.png)
8. <span data-ttu-id="237b1-165">Перед созданием виртуальной Машины, получите исходный диск hello URI tooyour ОС:</span><span class="sxs-lookup"><span data-stu-id="237b1-165">Before you create a VM, obtain hello URI tooyour source OS disk:</span></span>
   
   * <span data-ttu-id="237b1-166">Выберите hello учетной записи хранилища в hello портала Azure щелкните *большие двоичные объекты*.</span><span class="sxs-lookup"><span data-stu-id="237b1-166">Select hello storage account in hello Azure portal, click *Blobs*.</span></span>
   * <span data-ttu-id="237b1-167">Выберите контейнер hello.</span><span class="sxs-lookup"><span data-stu-id="237b1-167">Select hello container.</span></span> <span data-ttu-id="237b1-168">обычно является Hello исходный контейнер *виртуальные жесткие диски*:</span><span class="sxs-lookup"><span data-stu-id="237b1-168">hello source container is typically *vhds*:</span></span>
     
     ![Выбор большого двоичного объекта учетной записи хранения](./media/reset-local-password-without-agent/select_storage_details.png)
     
     <span data-ttu-id="237b1-170">Выберите источник виртуального жесткого диска операционной системы виртуальной Машины и нажмите кнопку hello *копирования* кнопку Далее toohello *URL-адрес* имя:</span><span class="sxs-lookup"><span data-stu-id="237b1-170">Select your source VM OS VHD and click hello *Copy* button next toohello *URL* name:</span></span>
     
     ![Копирование URI диска](./media/reset-local-password-without-agent/copy_source_vhd_uri.png)
9. <span data-ttu-id="237b1-172">Создайте виртуальную Машину с диска ОС ВМ hello источника:</span><span class="sxs-lookup"><span data-stu-id="237b1-172">Create a VM from hello source VM’s OS disk:</span></span>
   
   * <span data-ttu-id="237b1-173">Используйте [этого шаблона Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) toocreate ВМ с специализированные виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="237b1-173">Use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) toocreate a VM from a specialized VHD.</span></span> <span data-ttu-id="237b1-174">Нажмите кнопку hello `Deploy tooAzure` кнопку tooopen hello портал Azure с подробными сведениями шаблонного hello, заполняется автоматически.</span><span class="sxs-lookup"><span data-stu-id="237b1-174">Click hello `Deploy tooAzure` button tooopen hello Azure portal with hello templated details populated for you.</span></span>
   * <span data-ttu-id="237b1-175">Tooretain все предыдущие настройки hello для hello виртуальной Машины, установите *изменить шаблон* tooprovide существующей виртуальной сети, подсети, сетевой адаптер или общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="237b1-175">If you want tooretain all hello previous settings for hello VM, select *Edit template* tooprovide your existing VNet, subnet, network adapter, or public IP.</span></span>
   * <span data-ttu-id="237b1-176">В hello `OSDISKVHDURI` текстовом поле параметра, вставить hello в предшествующих шаг hello получить URI источника данных виртуального жесткого диска:</span><span class="sxs-lookup"><span data-stu-id="237b1-176">In hello `OSDISKVHDURI` parameter text box, paste hello URI of your source VHD obtain in hello preceding step:</span></span>
     
     ![Создание виртуальной машины на основе шаблона](./media/reset-local-password-without-agent/create_new_vm_from_template.png)
10. <span data-ttu-id="237b1-178">После hello, Новая виртуальная машина запущена, соединения toohello виртуальную Машину с помощью удаленного рабочего стола с hello новый пароль, указанный в hello `FixAzureVM.cmd` сценария.</span><span class="sxs-lookup"><span data-stu-id="237b1-178">After hello new VM is running, connect toohello VM using Remote Desktop with hello new password you specified in hello `FixAzureVM.cmd` script.</span></span>
11. <span data-ttu-id="237b1-179">Из вашего toohello удаленный сеанс новой виртуальной Машины, удалите hello следующие файлы tooclean hello среды:</span><span class="sxs-lookup"><span data-stu-id="237b1-179">From your remote session toohello new VM, remove hello following files tooclean up hello environment:</span></span>
    
    * <span data-ttu-id="237b1-180">Из расположения %windir%\System32</span><span class="sxs-lookup"><span data-stu-id="237b1-180">From %windir%\System32</span></span>
      * <span data-ttu-id="237b1-181">удалите файл FixAzureVM.cmd.</span><span class="sxs-lookup"><span data-stu-id="237b1-181">remove FixAzureVM.cmd</span></span>
    * <span data-ttu-id="237b1-182">Из расположения %windir%\System32\GroupPolicy\Machine\\</span><span class="sxs-lookup"><span data-stu-id="237b1-182">From %windir%\System32\GroupPolicy\Machine\\</span></span>
      * <span data-ttu-id="237b1-183">удалите файл scripts.ini.</span><span class="sxs-lookup"><span data-stu-id="237b1-183">remove scripts.ini</span></span>
    * <span data-ttu-id="237b1-184">Из расположения %windir%\System32\GroupPolicy</span><span class="sxs-lookup"><span data-stu-id="237b1-184">From %windir%\System32\GroupPolicy</span></span>
      * <span data-ttu-id="237b1-185">Удалите gpt.ini (если существовал gpt.ini и вы переименовали ее toogpt.ini.bak задней toogpt.ini .bak hello файл rename)</span><span class="sxs-lookup"><span data-stu-id="237b1-185">remove gpt.ini (if gpt.ini existed before, and you renamed it toogpt.ini.bak, rename hello .bak file back toogpt.ini)</span></span>

## <a name="next-steps"></a><span data-ttu-id="237b1-186">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="237b1-186">Next steps</span></span>
<span data-ttu-id="237b1-187">Если вы по-прежнему не удается подключиться с помощью удаленного рабочего стола, см. раздел hello [по устранению неполадок протокола удаленного рабочего СТОЛА](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="237b1-187">If you still cannot connect using Remote Desktop, see hello [RDP troubleshooting guide](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="237b1-188">Hello [подробное руководство по устранению неполадок протокола удаленного рабочего СТОЛА](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) рассматривается устранение неполадок методов, а не конкретные действия.</span><span class="sxs-lookup"><span data-stu-id="237b1-188">hello [detailed RDP troubleshooting guide](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) looks at troubleshooting methods rather than specific steps.</span></span> <span data-ttu-id="237b1-189">Вы также можете [отправить запрос в службу поддержки Azure](https://azure.microsoft.com/support/options/) и получить практическую помощь.</span><span class="sxs-lookup"><span data-stu-id="237b1-189">You can also [open an Azure support request](https://azure.microsoft.com/support/options/) for hands-on assistance.</span></span>

