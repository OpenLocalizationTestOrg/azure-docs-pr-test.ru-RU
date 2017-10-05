---
title: "Локальное создание образа виртуальной машины для Azure Marketplace | Документация Майкрософт"
description: "Узнайте и выполните действия по созданию локального образа виртуальной машины, а затем разверните его в Azure Marketplace и сделайте доступным для покупки."
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
ms.openlocfilehash: 8f6b9a9293dc149586e6e5fd55028170ea825b07
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="develop-an-on-premises-virtual-machine-image-for-the-azure-marketplace"></a><span data-ttu-id="a4ec7-103">Локальная разработка образа виртуальной машины для Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="a4ec7-103">Develop an on-premises virtual machine image for the Azure Marketplace</span></span>
<span data-ttu-id="a4ec7-104">Настоятельно рекомендуется разрабатывать виртуальные жесткие диски (VHD) Azure прямо в облаке, используя для этого протокол удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="a4ec7-104">We strongly recommend that you develop Azure virtual hard disks (VHDs) directly in the cloud by using Remote Desktop Protocol.</span></span> <span data-ttu-id="a4ec7-105">Однако при необходимости вы можете загрузить VHD и выполнить разработку в локальной инфраструктуре.</span><span class="sxs-lookup"><span data-stu-id="a4ec7-105">However, if you must, it is possible to download a VHD and develop it by using on-premises infrastructure.</span></span>  

<span data-ttu-id="a4ec7-106">Для локальной разработки необходимо загрузить VHD ОС созданной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="a4ec7-106">For on-premises development, you must download the operating system VHD of the created VM.</span></span> <span data-ttu-id="a4ec7-107">Эти действия входят в шаг 3.3, описанный ранее.</span><span class="sxs-lookup"><span data-stu-id="a4ec7-107">These steps would take place as part of step 3.3, above.</span></span>  

## <a name="download-a-vhd-image"></a><span data-ttu-id="a4ec7-108">Загрузка образа VHD</span><span class="sxs-lookup"><span data-stu-id="a4ec7-108">Download a VHD image</span></span>
### <a name="locate-a-blob-url"></a><span data-ttu-id="a4ec7-109">Поиск URL-адреса BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="a4ec7-109">Locate a blob URL</span></span>
<span data-ttu-id="a4ec7-110">Чтобы загрузить VHD, найдите URL-адрес большого двоичного объекта диска ОС.</span><span class="sxs-lookup"><span data-stu-id="a4ec7-110">In order to download the VHD, first locate the blob URL for the operating system disk.</span></span>

<span data-ttu-id="a4ec7-111">Найдите URL-адрес большого двоичного объекта на новом [портале Microsoft Azure](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="a4ec7-111">Locate the blob URL from the new [Microsoft Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="a4ec7-112">Последовательно выберите пункты **Обзор** > **Виртуальные машины** и щелкните развернутую виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="a4ec7-112">Go to **Browse** > **VMs**, and then select the deployed VM.</span></span>
2. <span data-ttu-id="a4ec7-113">В разделе **Настройка** выберите плитку **Диски**. Откроется колонка "Диски".</span><span class="sxs-lookup"><span data-stu-id="a4ec7-113">Under **Configure**, select the **Disks** tile, which opens the Disks blade.</span></span>
   
   ![рисунок](media/marketplace-publishing-vm-image-creation-on-premise/img01.png)
3. <span data-ttu-id="a4ec7-115">Выберите **Диск ОС**. Откроется другая колонка со свойствами диска, включая расположение VHD.</span><span class="sxs-lookup"><span data-stu-id="a4ec7-115">Select the **OS Disk**, which opens another blade that displays disk properties, including the VHD location.</span></span>
4. <span data-ttu-id="a4ec7-116">Скопируйте этот URL-адрес большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="a4ec7-116">Copy this blob URL.</span></span>
   
   ![рисунок](media/marketplace-publishing-vm-image-creation-on-premise/img02.png)
5. <span data-ttu-id="a4ec7-118">Теперь удалите развернутую виртуальную машину, не удаляя резервные копии дисков.</span><span class="sxs-lookup"><span data-stu-id="a4ec7-118">Now, delete the deployed VM without deleting the backing disks.</span></span> <span data-ttu-id="a4ec7-119">Вместо удаления виртуальную машину можно также остановить.</span><span class="sxs-lookup"><span data-stu-id="a4ec7-119">You can also stop the VM instead of deleting it.</span></span> <span data-ttu-id="a4ec7-120">Не загружайте VHD ОС, пока виртуальная машина работает.</span><span class="sxs-lookup"><span data-stu-id="a4ec7-120">Do not download the operating system VHD when the VM is running.</span></span>
   
   ![рисунок](media/marketplace-publishing-vm-image-creation-on-premise/img03.png)

### <a name="download-a-vhd"></a><span data-ttu-id="a4ec7-122">Загрузка VHD</span><span class="sxs-lookup"><span data-stu-id="a4ec7-122">Download a VHD</span></span>
<span data-ttu-id="a4ec7-123">Если URL-адрес большого двоичного объекта известен, вы можете загрузить VHD с помощью [портала Azure](http://manage.windowsazure.com/) или PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a4ec7-123">After you know the blob URL, you can download the VHD by using the [Azure portal](http://manage.windowsazure.com/) or PowerShell.</span></span>  

> [!NOTE]
> <span data-ttu-id="a4ec7-124">На момент составления данного руководства новый портал Microsoft Azure еще не содержит функцию загрузки VHD.</span><span class="sxs-lookup"><span data-stu-id="a4ec7-124">At the time of this guide’s creation, the functionality to download a VHD is not yet present in the new Microsoft Azure portal.</span></span>  
> 
> 

<span data-ttu-id="a4ec7-125">**Загрузка VHD ОС через действующий [портал управления Azure](http://manage.windowsazure.com/)**</span><span class="sxs-lookup"><span data-stu-id="a4ec7-125">**Download the operating system VHD via the current [Azure portal](http://manage.windowsazure.com/)**</span></span>

1. <span data-ttu-id="a4ec7-126">Войдите на портал Azure, если вы еще этого не сделали.</span><span class="sxs-lookup"><span data-stu-id="a4ec7-126">Sign in to the Azure portal if you have not done so already.</span></span>
2. <span data-ttu-id="a4ec7-127">Откройте вкладку **Хранилище** .</span><span class="sxs-lookup"><span data-stu-id="a4ec7-127">Click the **Storage** tab.</span></span>
3. <span data-ttu-id="a4ec7-128">Выберите учетную запись хранения, в которой находится VHD.</span><span class="sxs-lookup"><span data-stu-id="a4ec7-128">Select the storage account within which the VHD is stored.</span></span>
   
   ![рисунок](media/marketplace-publishing-vm-image-creation-on-premise/img04.png)
4. <span data-ttu-id="a4ec7-130">Откроются свойства учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="a4ec7-130">This displays storage account properties.</span></span> <span data-ttu-id="a4ec7-131">Откройте вкладку **Контейнеры** .</span><span class="sxs-lookup"><span data-stu-id="a4ec7-131">Select the **Containers** tab.</span></span>
   
   ![рисунок](media/marketplace-publishing-vm-image-creation-on-premise/img05.png)
5. <span data-ttu-id="a4ec7-133">Выберите контейнер, в котором хранится VHD.</span><span class="sxs-lookup"><span data-stu-id="a4ec7-133">Select the container in which the VHD is stored.</span></span> <span data-ttu-id="a4ec7-134">По умолчанию при создании на портале VHD сохраняется в контейнере виртуальных жестких дисков.</span><span class="sxs-lookup"><span data-stu-id="a4ec7-134">By default, when created from the portal, the VHD is stored in a vhds container.</span></span>
   
   ![рисунок](media/marketplace-publishing-vm-image-creation-on-premise/img06.png)
6. <span data-ttu-id="a4ec7-136">Выберите соответствующий VHD ОС, сравнив его URL-адрес с адресом, который вы сохранили.</span><span class="sxs-lookup"><span data-stu-id="a4ec7-136">Select the correct operating system VHD by comparing the URL to the one you saved.</span></span>
7. <span data-ttu-id="a4ec7-137">Щелкните элемент **Загрузить**.</span><span class="sxs-lookup"><span data-stu-id="a4ec7-137">Click **Download**.</span></span>
   
   ![рисунок](media/marketplace-publishing-vm-image-creation-on-premise/img07.png)

### <a name="download-a-vhd-by-using-powershell"></a><span data-ttu-id="a4ec7-139">Загрузка VHD с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="a4ec7-139">Download a VHD by using PowerShell</span></span>
<span data-ttu-id="a4ec7-140">Наряду с порталом управления Azure для загрузки VHD ОС можно использовать командлет [Save-AzureVhd](http://msdn.microsoft.com/library/dn495297.aspx) .</span><span class="sxs-lookup"><span data-stu-id="a4ec7-140">In addition to using the Azure portal, you can use the [Save-AzureVhd](http://msdn.microsoft.com/library/dn495297.aspx) cmdlet to download the operating system VHD.</span></span>

        Save-AzureVhd –Source <storageURIOfVhd> `
        -LocalFilePath <diskLocationOnWorkstation> `
        -StorageKey <keyForStorageAccount>
<span data-ttu-id="a4ec7-141">Например: Save-AzureVhd -Source “https://baseimagevm.blob.core.windows.net/vhds/BaseImageVM-6820cq00-BaseImageVM-os-1411003770191.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\baseimagevm.vhd” -StorageKey <String></span><span class="sxs-lookup"><span data-stu-id="a4ec7-141">For example, Save-AzureVhd -Source “https://baseimagevm.blob.core.windows.net/vhds/BaseImageVM-6820cq00-BaseImageVM-os-1411003770191.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\baseimagevm.vhd” -StorageKey <String></span></span>

> [!NOTE]
> <span data-ttu-id="a4ec7-142">Командлет **Save-AzureVhd** также имеет параметр **NumberOfThreads**, позволяющий улучшить параллелизм и добиться оптимального использования доступной пропускной способности для загрузки.</span><span class="sxs-lookup"><span data-stu-id="a4ec7-142">**Save-AzureVhd** also has a **NumberOfThreads** option that can be used to increase parallelism to make the best use of available bandwidth for the download.</span></span>
> 
> 

## <a name="upload-vhds-to-an-azure-storage-account"></a><span data-ttu-id="a4ec7-143">Подключение VHD к учетной записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="a4ec7-143">Upload VHDs to an Azure storage account</span></span>
<span data-ttu-id="a4ec7-144">Если VHD подготовлен локально, его необходимо отправить в учетную запись хранения в Azure.</span><span class="sxs-lookup"><span data-stu-id="a4ec7-144">If you prepared your VHDs on-premises, you need to upload them into a storage account in Azure.</span></span> <span data-ttu-id="a4ec7-145">Это действие выполняется после локального создания VHD, но до сертификации образа виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="a4ec7-145">This step takes place after creating your VHD on-premises but before obtaining certification for your VM image.</span></span>

### <a name="create-a-storage-account-and-container"></a><span data-ttu-id="a4ec7-146">Создание учетной записи хранения и контейнера</span><span class="sxs-lookup"><span data-stu-id="a4ec7-146">Create a storage account and container</span></span>
<span data-ttu-id="a4ec7-147">Рекомендуется передавать VHD-диски в учетную запись хранения, размещенную в любом регионе на территории США.</span><span class="sxs-lookup"><span data-stu-id="a4ec7-147">We recommend that VHDs be uploaded into a storage account in a region in the United States.</span></span> <span data-ttu-id="a4ec7-148">Все VHD для одного и того же SKU необходимо поместить в один и тот же контейнер в одной и той же учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="a4ec7-148">All VHDs for a single SKU should be placed in a single container within a single storage account.</span></span>

<span data-ttu-id="a4ec7-149">Создать учетную запись хранения можно с помощью [портала Microsoft Azure](https://portal.azure.com/), PowerShell или программы командной строки Linux.</span><span class="sxs-lookup"><span data-stu-id="a4ec7-149">To create a storage account, you can use the [Microsoft Azure portal](https://portal.azure.com/), PowerShell, or the Linux command-line tool.</span></span>  

<span data-ttu-id="a4ec7-150">**Создание учетной записи хранения на портале Microsoft Azure**</span><span class="sxs-lookup"><span data-stu-id="a4ec7-150">**Create a storage account from the Microsoft Azure portal**</span></span>

1. <span data-ttu-id="a4ec7-151">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a4ec7-151">Click **New**.</span></span>
2. <span data-ttu-id="a4ec7-152">Выберите **Хранилище**.</span><span class="sxs-lookup"><span data-stu-id="a4ec7-152">Select **Storage**.</span></span>
3. <span data-ttu-id="a4ec7-153">Введите имя учетной записи хранения и выберите расположение.</span><span class="sxs-lookup"><span data-stu-id="a4ec7-153">Fill in the storage account name, and then select a location.</span></span>
   
   ![рисунок](media/marketplace-publishing-vm-image-creation-on-premise/img08.png)
4. <span data-ttu-id="a4ec7-155">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a4ec7-155">Click **Create**.</span></span>
5. <span data-ttu-id="a4ec7-156">Должна открыться колонка созданной учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="a4ec7-156">The blade for the created storage account should be open.</span></span> <span data-ttu-id="a4ec7-157">Если это не произошло, последовательно выберите **Обзор** > **Учетные записи хранения**.</span><span class="sxs-lookup"><span data-stu-id="a4ec7-157">If not, select **Browse** > **Storage Accounts**.</span></span> <span data-ttu-id="a4ec7-158">В колонке "Учетная запись хранения" выберите созданную учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="a4ec7-158">On the Storage account blade, select the storage account created.</span></span>
6. <span data-ttu-id="a4ec7-159">Выберите **Контейнеры**.</span><span class="sxs-lookup"><span data-stu-id="a4ec7-159">Select **Containers**.</span></span>
   
   ![рисунок](media/marketplace-publishing-vm-image-creation-on-premise/img09.png) 
7. <span data-ttu-id="a4ec7-161">В колонке "Контейнеры" выберите **Добавить**и введите имя и разрешения контейнера.</span><span class="sxs-lookup"><span data-stu-id="a4ec7-161">On the Containers blade, select **Add**, and then enter a container name and the container permissions.</span></span> <span data-ttu-id="a4ec7-162">Для разрешений контейнера выберите вариант **Частный** .</span><span class="sxs-lookup"><span data-stu-id="a4ec7-162">Select **Private** for container permissions.</span></span>

> [!TIP]
> <span data-ttu-id="a4ec7-163">Рекомендуется создавать по одному контейнеру для каждого номера SKU, который вы планируете опубликовать.</span><span class="sxs-lookup"><span data-stu-id="a4ec7-163">We recommend that you create one container per SKU that you are planning to publish.</span></span>
> 
> 

  ![рисунок](media/marketplace-publishing-vm-image-creation-on-premise/img10.png)

### <a name="create-a-storage-account-by-using-powershell"></a><span data-ttu-id="a4ec7-165">Создание учетной записи хранения с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="a4ec7-165">Create a storage account by using PowerShell</span></span>
<span data-ttu-id="a4ec7-166">В PowerShell создайте учетную запись хранения с помощью командлета [New-AzureStorageAccount](http://msdn.microsoft.com/library/dn495115.aspx) .</span><span class="sxs-lookup"><span data-stu-id="a4ec7-166">Using PowerShell, create a storage account by using the [New-AzureStorageAccount](http://msdn.microsoft.com/library/dn495115.aspx) cmdlet.</span></span>

        New-AzureStorageAccount -StorageAccountName “mystorageaccount” -Location “West US”

<span data-ttu-id="a4ec7-167">Затем создайте в этой учетной записи контейнер с помощью командлета [NewAzureStorageContainer](http://msdn.microsoft.com/library/dn495291.aspx) .</span><span class="sxs-lookup"><span data-stu-id="a4ec7-167">Then you can create a container within that storage account by using the [NewAzureStorageContainer](http://msdn.microsoft.com/library/dn495291.aspx) cmdlet.</span></span>

        New-AzureStorageContainer -Name “containername” -Permission “Off”

> [!NOTE]
> <span data-ttu-id="a4ec7-168">Эти команды предполагают, что контекст текущей учетной записи хранения уже настроен в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a4ec7-168">Those commands assume that the current storage account context has already been set in PowerShell.</span></span>   <span data-ttu-id="a4ec7-169">Дополнительные сведения о настройке PowerShell см. в статье о [настройке Azure PowerShell](marketplace-publishing-powershell-setup.md).</span><span class="sxs-lookup"><span data-stu-id="a4ec7-169">Refer to [Setting up Azure PowerShell](marketplace-publishing-powershell-setup.md) for more details on PowerShell setup.</span></span>  
> 
> ### <a name="create-a-storage-account-by-using-the-command-line-tool-for-mac-and-linux"></a><span data-ttu-id="a4ec7-170">Создание учетной записи хранения с помощью программы командной строки для Mac и Linux</span><span class="sxs-lookup"><span data-stu-id="a4ec7-170">Create a storage account by using the command-line tool for Mac and Linux</span></span>
> <span data-ttu-id="a4ec7-171">В [программе командной строки Linux](../virtual-machines/linux/cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)создайте учетную запись хранения следующим образом.</span><span class="sxs-lookup"><span data-stu-id="a4ec7-171">From [Linux command-line tool](../virtual-machines/linux/cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), create a storage account as follows.</span></span>
> 
> 

        azure storage account create mystorageaccount --location "West US"

<span data-ttu-id="a4ec7-172">Создайте контейнер следующим образом.</span><span class="sxs-lookup"><span data-stu-id="a4ec7-172">Create a container as follows.</span></span>

        azure storage container create containername --account-name mystorageaccount --accountkey <accountKey>

## <a name="upload-a-vhd"></a><span data-ttu-id="a4ec7-173">Отправка VHD</span><span class="sxs-lookup"><span data-stu-id="a4ec7-173">Upload a VHD</span></span>
<span data-ttu-id="a4ec7-174">Создав учетную запись хранения и контейнер, отправьте подготовленные VHD.</span><span class="sxs-lookup"><span data-stu-id="a4ec7-174">After the storage account and container are created, you can upload your prepared VHDs.</span></span> <span data-ttu-id="a4ec7-175">Для этого можно использовать PowerShell, программу командной строки Linux или другие средства управления хранилищем Azure.</span><span class="sxs-lookup"><span data-stu-id="a4ec7-175">You can use PowerShell, the Linux command-line tool, or other Azure Storage management tools.</span></span>

### <a name="upload-a-vhd-via-powershell"></a><span data-ttu-id="a4ec7-176">Отправка VHD с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="a4ec7-176">Upload a VHD via PowerShell</span></span>
<span data-ttu-id="a4ec7-177">Воспользуйтесь командлетом [Add-AzureVhd](http://msdn.microsoft.com/library/dn495173.aspx) .</span><span class="sxs-lookup"><span data-stu-id="a4ec7-177">Use the [Add-AzureVhd](http://msdn.microsoft.com/library/dn495173.aspx) cmdlet.</span></span>

        Add-AzureVhd –Destination “http://mystorageaccount.blob.core.windows.net/containername/vmsku.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\vmsku.vhd”

### <a name="upload-a-vhd-by-using-the-command-line-tool-for-mac-and-linux"></a><span data-ttu-id="a4ec7-178">Отправка VHD с помощью программы командной строки для Mac и Linux</span><span class="sxs-lookup"><span data-stu-id="a4ec7-178">Upload a VHD by using the command-line tool for Mac and Linux</span></span>
<span data-ttu-id="a4ec7-179">В [программе командной строки Linux](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) введите следующее: azure vm image create <image name> --location <Location of the data center> --OS Linux <LocationOfLocalVHD></span><span class="sxs-lookup"><span data-stu-id="a4ec7-179">With the [Linux command-line tool](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2), use the following: azure vm image create <image name> --location <Location of the data center> --OS Linux <LocationOfLocalVHD></span></span>

## <a name="see-also"></a><span data-ttu-id="a4ec7-180">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="a4ec7-180">See also</span></span>
* [<span data-ttu-id="a4ec7-181">Создание образа виртуальной машины для Marketplace</span><span class="sxs-lookup"><span data-stu-id="a4ec7-181">Creating a virtual machine image for the Marketplace</span></span>](marketplace-publishing-vm-image-creation.md)
* [<span data-ttu-id="a4ec7-182">Настройка Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a4ec7-182">Setting up Azure PowerShell</span></span>](marketplace-publishing-powershell-setup.md)

