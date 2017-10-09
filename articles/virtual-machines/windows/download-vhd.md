---
title: "aaaDownload виртуального жесткого диска Windows из Azure | Документы Microsoft"
description: "Загрузка виртуального жесткого диска в Windows с помощью портала Azure hello."
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
ms.openlocfilehash: d0ca8842db98f22751f01648c0ba4e5cde090043
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="download-a-windows-vhd-from-azure"></a><span data-ttu-id="43916-103">Скачивание виртуального жесткого диска Windows из Azure</span><span class="sxs-lookup"><span data-stu-id="43916-103">Download a Windows VHD from Azure</span></span>

<span data-ttu-id="43916-104">В этой статье вы узнаете, как toodownload [Windows виртуального жесткого диска (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) файл из Azure с помощью hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="43916-104">In this article, you learn how toodownload a [Windows virtual hard disk (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) file from Azure using hello Azure portal.</span></span> 

<span data-ttu-id="43916-105">Виртуальные машины (VM Azure используется) [дисков](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toostore месте операционной системы, приложений и данных.</span><span class="sxs-lookup"><span data-stu-id="43916-105">Virtual machines (VMs) in Azure use [disks](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) as a place toostore an operating system, applications, and data.</span></span> <span data-ttu-id="43916-106">Все виртуальные машины Azure имеют как минимум два диска — диск операционной системы Windows и временный диск.</span><span class="sxs-lookup"><span data-stu-id="43916-106">All Azure VMs have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="43916-107">диск операционной системы Hello изначально создается из образа, а hello диска операционной системы и образа hello, виртуальные жесткие диски хранятся в учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="43916-107">hello operating system disk is initially created from an image, and both hello operating system disk and hello image are VHDs stored in an Azure storage account.</span></span> <span data-ttu-id="43916-108">Кроме того, виртуальные машины могут иметь один или несколько дисков данных, которые также хранятся на виртуальных жестких дисках.</span><span class="sxs-lookup"><span data-stu-id="43916-108">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span>

## <a name="stop-hello-vm"></a><span data-ttu-id="43916-109">Остановить hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="43916-109">Stop hello VM</span></span>

<span data-ttu-id="43916-110">Не удается загрузить виртуальный жесткий ДИСК из Azure, если он подключен tooa запуск виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="43916-110">A VHD can’t be downloaded from Azure if it's attached tooa running VM.</span></span> <span data-ttu-id="43916-111">Необходимо toostop hello toodownload виртуального жесткого диска для виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="43916-111">You need toostop hello VM toodownload a VHD.</span></span> <span data-ttu-id="43916-112">Если требуется VHD как toouse [изображения](tutorial-custom-images.md) toocreate использовать другие виртуальные машины с помощью новых дисков [Sysprep](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation) toogeneralize hello операционной системы, содержащихся в файле hello и затем остановить hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="43916-112">If you want toouse a VHD as an [image](tutorial-custom-images.md) toocreate other VMs with new disks, you use [Sysprep](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation) toogeneralize hello operating system contained in hello file and then stop hello VM.</span></span> <span data-ttu-id="43916-113">hello toouse виртуальный жесткий ДИСК как диск для нового экземпляра существующей ВМ или диск данных, нужно только toostop, а освобождать hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="43916-113">toouse hello VHD as a disk for a new instance of an existing VM or data disk, you only need toostop and deallocate hello VM.</span></span>

<span data-ttu-id="43916-114">toouse hello VHD как toocreate изображения других виртуальных машин, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="43916-114">toouse hello VHD as an image toocreate other VMs, complete these steps:</span></span>

1.  <span data-ttu-id="43916-115">Если это еще не сделано, войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="43916-115">If you haven't already done so, sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2.  <span data-ttu-id="43916-116">[Подключение виртуальной Машины toohello](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="43916-116">[Connect toohello VM](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 
3.  <span data-ttu-id="43916-117">На hello виртуальной Машины откройте окно командной строки hello с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="43916-117">On hello VM, open hello Command Prompt window as an administrator.</span></span>
4.  <span data-ttu-id="43916-118">Измените каталог hello слишком*%windir%\system32\sysprep* и запустите sysprep.exe.</span><span class="sxs-lookup"><span data-stu-id="43916-118">Change hello directory too*%windir%\system32\sysprep* and run sysprep.exe.</span></span>
5.  <span data-ttu-id="43916-119">В средство подготовки системы диалоговое окно «hello», выберите **Enter System Out-of-Box Experience (OOBE)**и убедитесь, что **Generalize** выбран.</span><span class="sxs-lookup"><span data-stu-id="43916-119">In hello System Preparation Tool dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that **Generalize** is selected.</span></span>
6.  <span data-ttu-id="43916-120">В разделе "Параметры завершения работы" выберите **Завершение работы** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="43916-120">In Shutdown Options, select **Shutdown**, and then click **OK**.</span></span> 

<span data-ttu-id="43916-121">hello toouse виртуальный жесткий ДИСК как диск для нового экземпляра существующей ВМ или диск данных, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="43916-121">toouse hello VHD as a disk for a new instance of an existing VM or data disk, complete these steps:</span></span>

1.  <span data-ttu-id="43916-122">Hello концентратора в hello портала Azure выберите команду меню **виртуальные машины**.</span><span class="sxs-lookup"><span data-stu-id="43916-122">On hello Hub menu in hello Azure portal, click **Virtual Machines**.</span></span>
2.  <span data-ttu-id="43916-123">Выберите hello виртуальной Машины из списка hello.</span><span class="sxs-lookup"><span data-stu-id="43916-123">Select hello VM from hello list.</span></span>
3.  <span data-ttu-id="43916-124">В колонке hello для hello виртуальной Машины, нажмите кнопку **остановить**.</span><span class="sxs-lookup"><span data-stu-id="43916-124">On hello blade for hello VM, click **Stop**.</span></span>

    ![Остановка виртуальной машины](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a><span data-ttu-id="43916-126">Создание URL-адреса SAS</span><span class="sxs-lookup"><span data-stu-id="43916-126">Generate SAS URL</span></span>

<span data-ttu-id="43916-127">toodownload hello VHD-файл, необходимо toogenerate [подписанного URL-адреса (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="43916-127">toodownload hello VHD file, you need toogenerate a [shared access signature (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span></span> <span data-ttu-id="43916-128">При формировании URL-адрес hello срок его действия назначается toohello URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="43916-128">When hello URL is generated, an expiration time is assigned toohello URL.</span></span>

1.  <span data-ttu-id="43916-129">Hello колонка hello для hello виртуальной Машины в меню **дисков**.</span><span class="sxs-lookup"><span data-stu-id="43916-129">On hello menu of hello blade for hello VM, click **Disks**.</span></span>
2.  <span data-ttu-id="43916-130">Выберите диск операционной системы hello для hello виртуальной Машины и нажмите кнопку **Экспорт**.</span><span class="sxs-lookup"><span data-stu-id="43916-130">Select hello operating system disk for hello VM, and then click **Export**.</span></span>
3.  <span data-ttu-id="43916-131">Задайте время истечения срока действия hello hello URL-адрес слишком*36000*.</span><span class="sxs-lookup"><span data-stu-id="43916-131">Set hello expiration time of hello URL too*36000*.</span></span>
4.  <span data-ttu-id="43916-132">Нажмите кнопку **Создать URL-адрес**.</span><span class="sxs-lookup"><span data-stu-id="43916-132">Click **Generate URL**.</span></span>

    ![Создание URL-адреса](./media/download-vhd/export-generate.png)

> [!NOTE]
> <span data-ttu-id="43916-134">время истечения срока действия Hello увеличено с tooprovide по умолчанию hello достаточное количество времени, toodownload hello большой VHD-файл для операционной системы Windows Server.</span><span class="sxs-lookup"><span data-stu-id="43916-134">hello expiration time is increased from hello default tooprovide enough time toodownload hello large VHD file for a Windows Server operating system.</span></span> <span data-ttu-id="43916-135">Можно ожидать VHD-файл, содержащий несколько toodownload часов в зависимости от подключения к tootake операционной системы Windows Server hello.</span><span class="sxs-lookup"><span data-stu-id="43916-135">You can expect a VHD file that contains hello Windows Server operating system tootake several hours toodownload depending on your connection.</span></span> <span data-ttu-id="43916-136">Если вы загружаете VHD для диска с данными, достаточно времени по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="43916-136">If you are downloading a VHD for a data disk, hello default time is sufficient.</span></span> 
> 
> 

## <a name="download-vhd"></a><span data-ttu-id="43916-137">Скачивание VHD</span><span class="sxs-lookup"><span data-stu-id="43916-137">Download VHD</span></span>

1.  <span data-ttu-id="43916-138">В группе hello URL-адрес, созданный выберите загруженный файл VHD hello.</span><span class="sxs-lookup"><span data-stu-id="43916-138">Under hello URL that was generated, click Download hello VHD file.</span></span>

    ![Скачивание VHD](./media/download-vhd/export-download.png)

2.  <span data-ttu-id="43916-140">Может потребоваться tooclick **Сохранить** в браузере toostart hello hello для загрузки.</span><span class="sxs-lookup"><span data-stu-id="43916-140">You may need tooclick **Save** in hello browser toostart hello download.</span></span> <span data-ttu-id="43916-141">имя по умолчанию Hello hello VHD-файл — *abcd*.</span><span class="sxs-lookup"><span data-stu-id="43916-141">hello default name for hello VHD file is *abcd*.</span></span>

    ![Нажмите кнопку "Сохранить" в браузере hello](./media/download-vhd/export-save.png)

## <a name="next-steps"></a><span data-ttu-id="43916-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="43916-143">Next steps</span></span>

- <span data-ttu-id="43916-144">Узнайте, каким образом слишком[передать файл виртуального жесткого диска tooAzure](upload-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="43916-144">Learn how too[upload a VHD file tooAzure](upload-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 
- <span data-ttu-id="43916-145">[Создание управляемых дисков из неуправляемых дисков в учетной записи хранения](attach-disk-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="43916-145">[Create managed disks from unmanaged disks in a storage account](attach-disk-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
- <span data-ttu-id="43916-146">[Управление дисками Azure с помощью PowerShell](tutorial-manage-data-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="43916-146">[Manage Azure disks with PowerShell](tutorial-manage-data-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

