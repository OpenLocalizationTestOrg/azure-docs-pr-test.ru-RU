---
title: "aaaCreating образ виртуальной машины в локальной среде для hello Azure Marketplace | Документы Microsoft"
description: "Понимание и выполните шаги hello toocreate образ виртуальной Машины в локальной и развернуть toohello Azure Marketplace для других toopurchase."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 26dfbd5a-8685-4b19-987e-c20ca60540ec
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 04/29/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: c7a265330f1e494db8d0e981a38ee00d85746bb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="develop-an-on-premises-virtual-machine-image-for-hello-azure-marketplace"></a><span data-ttu-id="0ff24-103">Разработка образ виртуальной машины в локальной среде для hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="0ff24-103">Develop an on-premises virtual machine image for hello Azure Marketplace</span></span>
<span data-ttu-id="0ff24-104">Настоятельно рекомендуется разрабатывать непосредственно в облаке hello Azure виртуальные жесткие диски (VHD) с помощью протокола удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="0ff24-104">We strongly recommend that you develop Azure virtual hard disks (VHDs) directly in hello cloud by using Remote Desktop Protocol.</span></span> <span data-ttu-id="0ff24-105">Тем не менее если необходимо, она является возможные toodownload виртуального жесткого диска и разработки с помощью локальной инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="0ff24-105">However, if you must, it is possible toodownload a VHD and develop it by using on-premises infrastructure.</span></span>  

<span data-ttu-id="0ff24-106">Для разработки приложений в локальной среде, необходимо загрузить hello операционной системы hello создать виртуальный жесткий ДИСК виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="0ff24-106">For on-premises development, you must download hello operating system VHD of hello created VM.</span></span> <span data-ttu-id="0ff24-107">Эти действия входят в шаг 3.3, описанный ранее.</span><span class="sxs-lookup"><span data-stu-id="0ff24-107">These steps would take place as part of step 3.3, above.</span></span>  

## <a name="download-a-vhd-image"></a><span data-ttu-id="0ff24-108">Загрузка образа VHD</span><span class="sxs-lookup"><span data-stu-id="0ff24-108">Download a VHD image</span></span>
### <a name="locate-a-blob-url"></a><span data-ttu-id="0ff24-109">Поиск URL-адреса BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="0ff24-109">Locate a blob URL</span></span>
<span data-ttu-id="0ff24-110">В порядке toodownload hello виртуальный жесткий ДИСК сначала найдите URL-адрес большого двоичного объекта hello для диска операционной системы hello.</span><span class="sxs-lookup"><span data-stu-id="0ff24-110">In order toodownload hello VHD, first locate hello blob URL for hello operating system disk.</span></span>

<span data-ttu-id="0ff24-111">Найдите новый URL-адрес большого двоичного объекта hello из hello [портал Microsoft Azure](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="0ff24-111">Locate hello blob URL from hello new [Microsoft Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="0ff24-112">Go слишком**Обзор** > **виртуальные машины**, и затем выберите hello развертывания ВМ.</span><span class="sxs-lookup"><span data-stu-id="0ff24-112">Go too**Browse** > **VMs**, and then select hello deployed VM.</span></span>
2. <span data-ttu-id="0ff24-113">В разделе **Настройка**выберите hello **дисков** плитки, который открывает колонку диски hello.</span><span class="sxs-lookup"><span data-stu-id="0ff24-113">Under **Configure**, select hello **Disks** tile, which opens hello Disks blade.</span></span>
   
   ![рисунок](media/marketplace-publishing-vm-image-creation-on-premise/img01.png)
3. <span data-ttu-id="0ff24-115">Выберите hello **диска ОС**, который открывается другая панель, отображающий свойства диска, включая расположение виртуального жесткого диска hello.</span><span class="sxs-lookup"><span data-stu-id="0ff24-115">Select hello **OS Disk**, which opens another blade that displays disk properties, including hello VHD location.</span></span>
4. <span data-ttu-id="0ff24-116">Скопируйте этот URL-адрес большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="0ff24-116">Copy this blob URL.</span></span>
   
   ![рисунок](media/marketplace-publishing-vm-image-creation-on-premise/img02.png)
5. <span data-ttu-id="0ff24-118">Теперь, удалить hello развертывания ВМ без удаления hello резервного дисков.</span><span class="sxs-lookup"><span data-stu-id="0ff24-118">Now, delete hello deployed VM without deleting hello backing disks.</span></span> <span data-ttu-id="0ff24-119">Также можно остановить hello виртуальной Машины, а не удаляйте его.</span><span class="sxs-lookup"><span data-stu-id="0ff24-119">You can also stop hello VM instead of deleting it.</span></span> <span data-ttu-id="0ff24-120">Не загружать hello операционной системы при запуске hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="0ff24-120">Do not download hello operating system VHD when hello VM is running.</span></span>
   
   ![рисунок](media/marketplace-publishing-vm-image-creation-on-premise/img03.png)

### <a name="download-a-vhd"></a><span data-ttu-id="0ff24-122">Загрузка VHD</span><span class="sxs-lookup"><span data-stu-id="0ff24-122">Download a VHD</span></span>
<span data-ttu-id="0ff24-123">После того, как URL-адрес большого двоичного объекта hello, hello виртуального жесткого диска можно загрузить с помощью hello [портал Azure](http://manage.windowsazure.com/) или PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0ff24-123">After you know hello blob URL, you can download hello VHD by using hello [Azure portal](http://manage.windowsazure.com/) or PowerShell.</span></span>  

> [!NOTE]
> <span data-ttu-id="0ff24-124">Во время создания в этом руководстве hello toodownload функции hello виртуального жесткого диска еще не присутствуют в hello новый портал Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="0ff24-124">At hello time of this guide’s creation, hello functionality toodownload a VHD is not yet present in hello new Microsoft Azure portal.</span></span>  
> 
> 

<span data-ttu-id="0ff24-125">**Загрузка операционной системы hello виртуальный жесткий ДИСК через hello текущей [портал Azure](http://manage.windowsazure.com/)**</span><span class="sxs-lookup"><span data-stu-id="0ff24-125">**Download hello operating system VHD via hello current [Azure portal](http://manage.windowsazure.com/)**</span></span>

1. <span data-ttu-id="0ff24-126">Войдите в портал Azure toohello, если вы еще не сделано.</span><span class="sxs-lookup"><span data-stu-id="0ff24-126">Sign in toohello Azure portal if you have not done so already.</span></span>
2. <span data-ttu-id="0ff24-127">Нажмите кнопку hello **хранения** вкладки.</span><span class="sxs-lookup"><span data-stu-id="0ff24-127">Click hello **Storage** tab.</span></span>
3. <span data-ttu-id="0ff24-128">Выберите учетную запись хранения hello, в течение которого hello хранится виртуальный жесткий ДИСК.</span><span class="sxs-lookup"><span data-stu-id="0ff24-128">Select hello storage account within which hello VHD is stored.</span></span>
   
   ![рисунок](media/marketplace-publishing-vm-image-creation-on-premise/img04.png)
4. <span data-ttu-id="0ff24-130">Откроются свойства учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="0ff24-130">This displays storage account properties.</span></span> <span data-ttu-id="0ff24-131">Выберите hello **контейнеры** вкладки.</span><span class="sxs-lookup"><span data-stu-id="0ff24-131">Select hello **Containers** tab.</span></span>
   
   ![рисунок](media/marketplace-publishing-vm-image-creation-on-premise/img05.png)
5. <span data-ttu-id="0ff24-133">Выберите контейнер hello, в которой hello хранится виртуальный жесткий ДИСК.</span><span class="sxs-lookup"><span data-stu-id="0ff24-133">Select hello container in which hello VHD is stored.</span></span> <span data-ttu-id="0ff24-134">По умолчанию при создании из портала hello hello виртуального жесткого диска хранится в контейнере VHD-файлов.</span><span class="sxs-lookup"><span data-stu-id="0ff24-134">By default, when created from hello portal, hello VHD is stored in a vhds container.</span></span>
   
   ![рисунок](media/marketplace-publishing-vm-image-creation-on-premise/img06.png)
6. <span data-ttu-id="0ff24-136">Выберите подходящую операционную систему hello виртуального жесткого диска путем сравнения toohello hello URL-адрес, который был сохранен.</span><span class="sxs-lookup"><span data-stu-id="0ff24-136">Select hello correct operating system VHD by comparing hello URL toohello one you saved.</span></span>
7. <span data-ttu-id="0ff24-137">Щелкните элемент **Загрузить**.</span><span class="sxs-lookup"><span data-stu-id="0ff24-137">Click **Download**.</span></span>
   
   ![рисунок](media/marketplace-publishing-vm-image-creation-on-premise/img07.png)

### <a name="download-a-vhd-by-using-powershell"></a><span data-ttu-id="0ff24-139">Загрузка VHD с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="0ff24-139">Download a VHD by using PowerShell</span></span>
<span data-ttu-id="0ff24-140">В дополнение к этому toousing hello портал Azure, вы можете использовать hello [Save-AzureVhd](http://msdn.microsoft.com/library/dn495297.aspx) командлет toodownload hello операционной системы.</span><span class="sxs-lookup"><span data-stu-id="0ff24-140">In addition toousing hello Azure portal, you can use hello [Save-AzureVhd](http://msdn.microsoft.com/library/dn495297.aspx) cmdlet toodownload hello operating system VHD.</span></span>

        Save-AzureVhd –Source <storageURIOfVhd> `
        -LocalFilePath <diskLocationOnWorkstation> `
        -StorageKey <keyForStorageAccount>
<span data-ttu-id="0ff24-141">Например: Save-AzureVhd -Source “https://baseimagevm.blob.core.windows.net/vhds/BaseImageVM-6820cq00-BaseImageVM-os-1411003770191.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\baseimagevm.vhd” -StorageKey <String></span><span class="sxs-lookup"><span data-stu-id="0ff24-141">For example, Save-AzureVhd -Source “https://baseimagevm.blob.core.windows.net/vhds/BaseImageVM-6820cq00-BaseImageVM-os-1411003770191.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\baseimagevm.vhd” -StorageKey <String></span></span>

> [!NOTE]
> <span data-ttu-id="0ff24-142">**Save-AzureVhd** также имеет **NumberOfThreads** , возможность использовать tooincrease toomake параллелизма hello эффективно использовать доступную пропускную способность для скачивания hello.</span><span class="sxs-lookup"><span data-stu-id="0ff24-142">**Save-AzureVhd** also has a **NumberOfThreads** option that can be used tooincrease parallelism toomake hello best use of available bandwidth for hello download.</span></span>
> 
> 

## <a name="upload-vhds-tooan-azure-storage-account"></a><span data-ttu-id="0ff24-143">Отправить учетную запись хранилища Azure tooan виртуальных жестких дисков</span><span class="sxs-lookup"><span data-stu-id="0ff24-143">Upload VHDs tooan Azure storage account</span></span>
<span data-ttu-id="0ff24-144">Если подготовки виртуальных жестких дисков в локальной необходимо tooupload их в хранилища учетной записи в Azure.</span><span class="sxs-lookup"><span data-stu-id="0ff24-144">If you prepared your VHDs on-premises, you need tooupload them into a storage account in Azure.</span></span> <span data-ttu-id="0ff24-145">Это действие выполняется после локального создания VHD, но до сертификации образа виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0ff24-145">This step takes place after creating your VHD on-premises but before obtaining certification for your VM image.</span></span>

### <a name="create-a-storage-account-and-container"></a><span data-ttu-id="0ff24-146">Создание учетной записи хранения и контейнера</span><span class="sxs-lookup"><span data-stu-id="0ff24-146">Create a storage account and container</span></span>
<span data-ttu-id="0ff24-147">Мы рекомендуем, что виртуальные жесткие диски будет передан в учетной записи хранения в регионе США hello.</span><span class="sxs-lookup"><span data-stu-id="0ff24-147">We recommend that VHDs be uploaded into a storage account in a region in hello United States.</span></span> <span data-ttu-id="0ff24-148">Все VHD для одного и того же SKU необходимо поместить в один и тот же контейнер в одной и той же учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="0ff24-148">All VHDs for a single SKU should be placed in a single container within a single storage account.</span></span>

<span data-ttu-id="0ff24-149">toocreate учетной записи хранилища можно использовать hello [портал Microsoft Azure](https://portal.azure.com/), PowerShell или средство командной строки hello Linux.</span><span class="sxs-lookup"><span data-stu-id="0ff24-149">toocreate a storage account, you can use hello [Microsoft Azure portal](https://portal.azure.com/), PowerShell, or hello Linux command-line tool.</span></span>  

<span data-ttu-id="0ff24-150">**Создать учетную запись хранилища с портала Microsoft Azure hello**</span><span class="sxs-lookup"><span data-stu-id="0ff24-150">**Create a storage account from hello Microsoft Azure portal**</span></span>

1. <span data-ttu-id="0ff24-151">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="0ff24-151">Click **New**.</span></span>
2. <span data-ttu-id="0ff24-152">Выберите **Хранилище**.</span><span class="sxs-lookup"><span data-stu-id="0ff24-152">Select **Storage**.</span></span>
3. <span data-ttu-id="0ff24-153">Введите имя учетной записи хранения hello и выберите местоположение.</span><span class="sxs-lookup"><span data-stu-id="0ff24-153">Fill in hello storage account name, and then select a location.</span></span>
   
   ![рисунок](media/marketplace-publishing-vm-image-creation-on-premise/img08.png)
4. <span data-ttu-id="0ff24-155">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="0ff24-155">Click **Create**.</span></span>
5. <span data-ttu-id="0ff24-156">Hello колонке hello, учетная запись хранения создана должен быть открыт.</span><span class="sxs-lookup"><span data-stu-id="0ff24-156">hello blade for hello created storage account should be open.</span></span> <span data-ttu-id="0ff24-157">Если это не произошло, последовательно выберите **Обзор** > **Учетные записи хранения**.</span><span class="sxs-lookup"><span data-stu-id="0ff24-157">If not, select **Browse** > **Storage Accounts**.</span></span> <span data-ttu-id="0ff24-158">Hello хранения промежуточных колонки, выберите создать учетную запись хранения hello.</span><span class="sxs-lookup"><span data-stu-id="0ff24-158">On hello Storage account blade, select hello storage account created.</span></span>
6. <span data-ttu-id="0ff24-159">Выберите **Контейнеры**.</span><span class="sxs-lookup"><span data-stu-id="0ff24-159">Select **Containers**.</span></span>
   
   ![рисунок](media/marketplace-publishing-vm-image-creation-on-premise/img09.png) 
7. <span data-ttu-id="0ff24-161">В колонке контейнеры hello, выберите **добавить**, а затем введите имя и hello контейнера разрешениями для контейнера.</span><span class="sxs-lookup"><span data-stu-id="0ff24-161">On hello Containers blade, select **Add**, and then enter a container name and hello container permissions.</span></span> <span data-ttu-id="0ff24-162">Для разрешений контейнера выберите вариант **Частный** .</span><span class="sxs-lookup"><span data-stu-id="0ff24-162">Select **Private** for container permissions.</span></span>

> [!TIP]
> <span data-ttu-id="0ff24-163">Рекомендуется создать один контейнер на планировании toopublish SKU.</span><span class="sxs-lookup"><span data-stu-id="0ff24-163">We recommend that you create one container per SKU that you are planning toopublish.</span></span>
> 
> 

  ![рисунок](media/marketplace-publishing-vm-image-creation-on-premise/img10.png)

### <a name="create-a-storage-account-by-using-powershell"></a><span data-ttu-id="0ff24-165">Создание учетной записи хранения с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="0ff24-165">Create a storage account by using PowerShell</span></span>
<span data-ttu-id="0ff24-166">С помощью PowerShell, создать учетную запись хранилища с помощью hello [New AzureStorageAccount](http://msdn.microsoft.com/library/dn495115.aspx) командлета.</span><span class="sxs-lookup"><span data-stu-id="0ff24-166">Using PowerShell, create a storage account by using hello [New-AzureStorageAccount](http://msdn.microsoft.com/library/dn495115.aspx) cmdlet.</span></span>

        New-AzureStorageAccount -StorageAccountName “mystorageaccount” -Location “West US”

<span data-ttu-id="0ff24-167">Затем вы можете создать контейнер в этой учетной записи хранения с помощью hello [NewAzureStorageContainer](http://msdn.microsoft.com/library/dn495291.aspx) командлета.</span><span class="sxs-lookup"><span data-stu-id="0ff24-167">Then you can create a container within that storage account by using hello [NewAzureStorageContainer](http://msdn.microsoft.com/library/dn495291.aspx) cmdlet.</span></span>

        New-AzureStorageContainer -Name “containername” -Permission “Off”

> [!NOTE]
> <span data-ttu-id="0ff24-168">Эти команды предполагают, что этот контекст учетной записи хранилища текущего hello уже задано в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0ff24-168">Those commands assume that hello current storage account context has already been set in PowerShell.</span></span>   <span data-ttu-id="0ff24-169">См. слишком[Настройка Azure PowerShell](marketplace-publishing-powershell-setup.md) Дополнительные сведения об установке PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0ff24-169">Refer too[Setting up Azure PowerShell](marketplace-publishing-powershell-setup.md) for more details on PowerShell setup.</span></span>  
> 
> ### <a name="create-a-storage-account-by-using-hello-command-line-tool-for-mac-and-linux"></a><span data-ttu-id="0ff24-170">Создать учетную запись хранилища с помощью средства командной строки hello для Mac и Linux</span><span class="sxs-lookup"><span data-stu-id="0ff24-170">Create a storage account by using hello command-line tool for Mac and Linux</span></span>
> <span data-ttu-id="0ff24-171">В [программе командной строки Linux](../virtual-machines/linux/cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)создайте учетную запись хранения следующим образом.</span><span class="sxs-lookup"><span data-stu-id="0ff24-171">From [Linux command-line tool](../virtual-machines/linux/cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), create a storage account as follows.</span></span>
> 
> 

        azure storage account create mystorageaccount --location "West US"

<span data-ttu-id="0ff24-172">Создайте контейнер следующим образом.</span><span class="sxs-lookup"><span data-stu-id="0ff24-172">Create a container as follows.</span></span>

        azure storage container create containername --account-name mystorageaccount --accountkey <accountKey>

## <a name="upload-a-vhd"></a><span data-ttu-id="0ff24-173">Отправка VHD</span><span class="sxs-lookup"><span data-stu-id="0ff24-173">Upload a VHD</span></span>
<span data-ttu-id="0ff24-174">После создания учетной записи хранилища hello и контейнер можно передать подготовленные виртуальные жесткие диски.</span><span class="sxs-lookup"><span data-stu-id="0ff24-174">After hello storage account and container are created, you can upload your prepared VHDs.</span></span> <span data-ttu-id="0ff24-175">Можно использовать PowerShell, средства командной строки hello Linux или других средств управления в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="0ff24-175">You can use PowerShell, hello Linux command-line tool, or other Azure Storage management tools.</span></span>

### <a name="upload-a-vhd-via-powershell"></a><span data-ttu-id="0ff24-176">Отправка VHD с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="0ff24-176">Upload a VHD via PowerShell</span></span>
<span data-ttu-id="0ff24-177">Используйте hello [Add-AzureVhd](http://msdn.microsoft.com/library/dn495173.aspx) командлета.</span><span class="sxs-lookup"><span data-stu-id="0ff24-177">Use hello [Add-AzureVhd](http://msdn.microsoft.com/library/dn495173.aspx) cmdlet.</span></span>

        Add-AzureVhd –Destination “http://mystorageaccount.blob.core.windows.net/containername/vmsku.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\vmsku.vhd”

### <a name="upload-a-vhd-by-using-hello-command-line-tool-for-mac-and-linux"></a><span data-ttu-id="0ff24-178">Отправить VHD с помощью средства командной строки hello для Mac и Linux</span><span class="sxs-lookup"><span data-stu-id="0ff24-178">Upload a VHD by using hello command-line tool for Mac and Linux</span></span>
<span data-ttu-id="0ff24-179">С hello [средство командной строки Linux](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2), используйте ниже hello: Создание образа виртуальной машины azure <image name> --расположение <Location of hello data center> --ОС Linux<LocationOfLocalVHD></span><span class="sxs-lookup"><span data-stu-id="0ff24-179">With hello [Linux command-line tool](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2), use hello following: azure vm image create <image name> --location <Location of hello data center> --OS Linux <LocationOfLocalVHD></span></span>

## <a name="see-also"></a><span data-ttu-id="0ff24-180">См. также</span><span class="sxs-lookup"><span data-stu-id="0ff24-180">See also</span></span>
* [<span data-ttu-id="0ff24-181">Создание образа виртуальной машины для hello Marketplace</span><span class="sxs-lookup"><span data-stu-id="0ff24-181">Creating a virtual machine image for hello Marketplace</span></span>](marketplace-publishing-vm-image-creation.md)
* [<span data-ttu-id="0ff24-182">Настройка Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0ff24-182">Setting up Azure PowerShell</span></span>](marketplace-publishing-powershell-setup.md)

