---
title: "Скачивание виртуального жесткого диска Windows из Azure | Документация Майкрософт"
description: "Скачайте виртуальный жесткий диск Windows с помощью портала Azure."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: davidmu
ms.openlocfilehash: d8bf89a4b7c2a158302f9ba09a182a3d8d062adc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="download-a-windows-vhd-from-azure"></a><span data-ttu-id="edf0d-103">Скачивание виртуального жесткого диска Windows из Azure</span><span class="sxs-lookup"><span data-stu-id="edf0d-103">Download a Windows VHD from Azure</span></span>

<span data-ttu-id="edf0d-104">В этой статье описано, как скачать файл [виртуального жесткого диска (VHD) Windows](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) из Azure, используя портал Azure.</span><span class="sxs-lookup"><span data-stu-id="edf0d-104">In this article, you learn how to download a [Windows virtual hard disk (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) file from Azure using the Azure portal.</span></span> 

<span data-ttu-id="edf0d-105">Виртуальные машины в Azure используют [диски](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) как место хранения операционной системы, приложений и данных.</span><span class="sxs-lookup"><span data-stu-id="edf0d-105">Virtual machines (VMs) in Azure use [disks](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) as a place to store an operating system, applications, and data.</span></span> <span data-ttu-id="edf0d-106">Все виртуальные машины Azure имеют как минимум два диска — диск операционной системы Windows и временный диск.</span><span class="sxs-lookup"><span data-stu-id="edf0d-106">All Azure VMs have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="edf0d-107">Диск операционной системы изначально создается из образа, при этом и диск операционной системы, и образ являются виртуальными жесткими дисками (VHD), расположенными в учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="edf0d-107">The operating system disk is initially created from an image, and both the operating system disk and the image are VHDs stored in an Azure storage account.</span></span> <span data-ttu-id="edf0d-108">Кроме того, виртуальные машины могут иметь один или несколько дисков данных, которые также хранятся на виртуальных жестких дисках.</span><span class="sxs-lookup"><span data-stu-id="edf0d-108">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span>

## <a name="stop-the-vm"></a><span data-ttu-id="edf0d-109">Остановка виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="edf0d-109">Stop the VM</span></span>

<span data-ttu-id="edf0d-110">VHD невозможно скачать из Azure, если он подключен к запущенной виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="edf0d-110">A VHD can’t be downloaded from Azure if it's attached to a running VM.</span></span> <span data-ttu-id="edf0d-111">Для скачивания VHD необходимо остановить виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="edf0d-111">You need to stop the VM to download a VHD.</span></span> <span data-ttu-id="edf0d-112">Чтобы использовать VHD в качестве [образа](tutorial-custom-images.md) для создания других виртуальных машин с помощью новых дисков, необходимо воспользоваться [Sysprep](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation) для подготовки к использованию операционной системы, которая содержится в файле, а затем остановить виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="edf0d-112">If you want to use a VHD as an [image](tutorial-custom-images.md) to create other VMs with new disks, you use [Sysprep](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation) to generalize the operating system contained in the file and then stop the VM.</span></span> <span data-ttu-id="edf0d-113">Для использования VHD в качестве диска для нового экземпляра существующей виртуальной машины или диска данных необходимо просто остановить виртуальную машину и отменить ее выделение.</span><span class="sxs-lookup"><span data-stu-id="edf0d-113">To use the VHD as a disk for a new instance of an existing VM or data disk, you only need to stop and deallocate the VM.</span></span>

<span data-ttu-id="edf0d-114">Чтобы использовать VHD как образ для создания других виртуальных машин, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="edf0d-114">To use the VHD as an image to create other VMs, complete these steps:</span></span>

1.  <span data-ttu-id="edf0d-115">Перейдите на [портал Azure](https://portal.azure.com/), если вы еще этого не сделали.</span><span class="sxs-lookup"><span data-stu-id="edf0d-115">If you haven't already done so, sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2.  <span data-ttu-id="edf0d-116">[Подключитесь к виртуальной машине](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="edf0d-116">[Connect to the VM](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 
3.  <span data-ttu-id="edf0d-117">На виртуальной машине откройте окно командной строки с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="edf0d-117">On the VM, open the Command Prompt window as an administrator.</span></span>
4.  <span data-ttu-id="edf0d-118">Измените каталог на *%windir%\system32\sysprep* и запустите файл sysprep.exe.</span><span class="sxs-lookup"><span data-stu-id="edf0d-118">Change the directory to *%windir%\system32\sysprep* and run sysprep.exe.</span></span>
5.  <span data-ttu-id="edf0d-119">В диалоговом окне "Программа подготовки системы" выберите **Переход в окно приветствия системы (OOBE)** и убедитесь, что установлен флажок **Подготовка к использованию**.</span><span class="sxs-lookup"><span data-stu-id="edf0d-119">In the System Preparation Tool dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that **Generalize** is selected.</span></span>
6.  <span data-ttu-id="edf0d-120">В разделе "Параметры завершения работы" выберите **Завершение работы** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="edf0d-120">In Shutdown Options, select **Shutdown**, and then click **OK**.</span></span> 

<span data-ttu-id="edf0d-121">Для использования VHD в качестве диска для нового экземпляра существующей виртуальной машины или диска данных выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="edf0d-121">To use the VHD as a disk for a new instance of an existing VM or data disk, complete these steps:</span></span>

1.  <span data-ttu-id="edf0d-122">В главном меню на портале Azure и щелкните **Виртуальные машины**.</span><span class="sxs-lookup"><span data-stu-id="edf0d-122">On the Hub menu in the Azure portal, click **Virtual Machines**.</span></span>
2.  <span data-ttu-id="edf0d-123">Выберите виртуальную машину из списка.</span><span class="sxs-lookup"><span data-stu-id="edf0d-123">Select the VM from the list.</span></span>
3.  <span data-ttu-id="edf0d-124">В колонке виртуальной машины нажмите кнопку **Остановить**.</span><span class="sxs-lookup"><span data-stu-id="edf0d-124">On the blade for the VM, click **Stop**.</span></span>

    ![Остановка виртуальной машины](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a><span data-ttu-id="edf0d-126">Создание URL-адреса SAS</span><span class="sxs-lookup"><span data-stu-id="edf0d-126">Generate SAS URL</span></span>

<span data-ttu-id="edf0d-127">Чтобы скачать VHD-файл, необходимо создать [подписанный URL-адрес (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="edf0d-127">To download the VHD file, you need to generate a [shared access signature (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span></span> <span data-ttu-id="edf0d-128">Когда этот URL-адрес создан, ему назначается срок действия.</span><span class="sxs-lookup"><span data-stu-id="edf0d-128">When the URL is generated, an expiration time is assigned to the URL.</span></span>

1.  <span data-ttu-id="edf0d-129">В меню колонки виртуальной машины щелкните **Диски**.</span><span class="sxs-lookup"><span data-stu-id="edf0d-129">On the menu of the blade for the VM, click **Disks**.</span></span>
2.  <span data-ttu-id="edf0d-130">Выберите диск операционной системы для виртуальной машины и щелкните **Экспорт**.</span><span class="sxs-lookup"><span data-stu-id="edf0d-130">Select the operating system disk for the VM, and then click **Export**.</span></span>
3.  <span data-ttu-id="edf0d-131">Задайте срок действия URL-адреса *36000*.</span><span class="sxs-lookup"><span data-stu-id="edf0d-131">Set the expiration time of the URL to *36000*.</span></span>
4.  <span data-ttu-id="edf0d-132">Нажмите кнопку **Создать URL-адрес**.</span><span class="sxs-lookup"><span data-stu-id="edf0d-132">Click **Generate URL**.</span></span>

    ![Создание URL-адреса](./media/download-vhd/export-generate.png)

> [!NOTE]
> <span data-ttu-id="edf0d-134">Заданное по умолчанию значение срока действия увеличивается, чтобы предоставить достаточно времени на скачивание большого VHD-файл для операционной системы Windows Server.</span><span class="sxs-lookup"><span data-stu-id="edf0d-134">The expiration time is increased from the default to provide enough time to download the large VHD file for a Windows Server operating system.</span></span> <span data-ttu-id="edf0d-135">Скачивание VHD-файл, содержащего операционную систему Windows Server, может занять несколько часов в зависимости от качества подключения.</span><span class="sxs-lookup"><span data-stu-id="edf0d-135">You can expect a VHD file that contains the Windows Server operating system to take several hours to download depending on your connection.</span></span> <span data-ttu-id="edf0d-136">Если вы скачиваете VHD для диска данных, то время, заданное по умолчанию, является достаточным.</span><span class="sxs-lookup"><span data-stu-id="edf0d-136">If you are downloading a VHD for a data disk, the default time is sufficient.</span></span> 
> 
> 

## <a name="download-vhd"></a><span data-ttu-id="edf0d-137">Скачивание VHD</span><span class="sxs-lookup"><span data-stu-id="edf0d-137">Download VHD</span></span>

1.  <span data-ttu-id="edf0d-138">Под созданным URL-адресом щелкните ссылку "Скачать VHD-файл".</span><span class="sxs-lookup"><span data-stu-id="edf0d-138">Under the URL that was generated, click Download the VHD file.</span></span>

    ![Скачивание VHD](./media/download-vhd/export-download.png)

2.  <span data-ttu-id="edf0d-140">Чтобы начать скачивание, может потребоваться нажать кнопку **Сохранить** в браузере.</span><span class="sxs-lookup"><span data-stu-id="edf0d-140">You may need to click **Save** in the browser to start the download.</span></span> <span data-ttu-id="edf0d-141">По умолчанию VHD-файлу присваивается имя *abcd*.</span><span class="sxs-lookup"><span data-stu-id="edf0d-141">The default name for the VHD file is *abcd*.</span></span>

    ![Нажатие кнопки "Сохранить" в браузере](./media/download-vhd/export-save.png)

## <a name="next-steps"></a><span data-ttu-id="edf0d-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="edf0d-143">Next steps</span></span>

- <span data-ttu-id="edf0d-144">Узнайте, как [передать VHD-файл в Azure](upload-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="edf0d-144">Learn how to [upload a VHD file to Azure](upload-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 
- <span data-ttu-id="edf0d-145">[Создание управляемых дисков из неуправляемых дисков в учетной записи хранения](attach-disk-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="edf0d-145">[Create managed disks from unmanaged disks in a storage account](attach-disk-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
- <span data-ttu-id="edf0d-146">[Управление дисками Azure с помощью PowerShell](tutorial-manage-data-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="edf0d-146">[Manage Azure disks with PowerShell](tutorial-manage-data-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

