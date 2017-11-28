---
title: "aaaDownload Linux VHD из Azure | Документы Microsoft"
description: "Загрузите VHD Linux с помощью Azure CLI hello и hello портал Azure."
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
ms.openlocfilehash: 7e08e985a64a6be581b8f5eedcce60fbd314eaf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="download-a-linux-vhd-from-azure"></a><span data-ttu-id="a509a-103">Скачивание виртуального жесткого диска Linux из Azure</span><span class="sxs-lookup"><span data-stu-id="a509a-103">Download a Linux VHD from Azure</span></span>

<span data-ttu-id="a509a-104">В этой статье вы узнаете, как toodownload [Linux виртуального жесткого диска (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) hello файл из Azure с помощью Azure CLI и на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="a509a-104">In this article, you learn how toodownload a [Linux virtual hard disk (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) file from Azure using hello Azure CLI and Azure portal.</span></span> 

<span data-ttu-id="a509a-105">Виртуальные машины (VM Azure используется) [дисков](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toostore месте операционной системы, приложений и данных.</span><span class="sxs-lookup"><span data-stu-id="a509a-105">Virtual machines (VMs) in Azure use [disks](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) as a place toostore an operating system, applications, and data.</span></span> <span data-ttu-id="a509a-106">Все виртуальные машины Azure имеют как минимум два диска — диск операционной системы Windows и временный диск.</span><span class="sxs-lookup"><span data-stu-id="a509a-106">All Azure VMs have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="a509a-107">диск операционной системы Hello изначально создается из образа, а hello диска операционной системы и образа hello, виртуальные жесткие диски хранятся в учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="a509a-107">hello operating system disk is initially created from an image, and both hello operating system disk and hello image are VHDs stored in an Azure storage account.</span></span> <span data-ttu-id="a509a-108">Кроме того, виртуальные машины могут иметь один или несколько дисков данных, которые также хранятся на виртуальных жестких дисках.</span><span class="sxs-lookup"><span data-stu-id="a509a-108">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span>

<span data-ttu-id="a509a-109">Установите интерфейс командной строки [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2), если это еще не сделано.</span><span class="sxs-lookup"><span data-stu-id="a509a-109">If you haven't already done so, install [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span></span>

## <a name="stop-hello-vm"></a><span data-ttu-id="a509a-110">Остановить hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="a509a-110">Stop hello VM</span></span>

<span data-ttu-id="a509a-111">Не удается загрузить виртуальный жесткий ДИСК из Azure, если он подключен tooa запуск виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a509a-111">A VHD can’t be downloaded from Azure if it's attached tooa running VM.</span></span> <span data-ttu-id="a509a-112">Необходимо toostop hello toodownload виртуального жесткого диска для виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a509a-112">You need toostop hello VM toodownload a VHD.</span></span> <span data-ttu-id="a509a-113">Если требуется toouse VHD как [изображения](tutorial-custom-images.md) toocreate другие виртуальные машины с помощью новых дисков требуется toodeprovision и обобщения hello операционной системы, содержащихся в hello файла и остановить hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a509a-113">If you want toouse a VHD as an [image](tutorial-custom-images.md) toocreate other VMs with new disks, you need toodeprovision and generalize hello operating system contained in hello file and stop hello VM.</span></span> <span data-ttu-id="a509a-114">hello toouse виртуальный жесткий ДИСК как диск для нового экземпляра существующей ВМ или диск данных, нужно только toostop, а освобождать hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a509a-114">toouse hello VHD as a disk for a new instance of an existing VM or data disk, you only need toostop and deallocate hello VM.</span></span>

<span data-ttu-id="a509a-115">toouse hello VHD как toocreate изображения других виртуальных машин, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="a509a-115">toouse hello VHD as an image toocreate other VMs, complete these steps:</span></span>

1. <span data-ttu-id="a509a-116">Использовать SSH, имя учетной записи hello и hello общедоступный IP-адрес tooit tooconnect hello виртуальной Машины и сделать.</span><span class="sxs-lookup"><span data-stu-id="a509a-116">Use SSH, hello account name, and hello public IP address of hello VM tooconnect tooit and deprovision it.</span></span> <span data-ttu-id="a509a-117">Здравствуйте, "+" пользователя параметра также приведет к удалению hello последняя подготовленного пользователя учетной записи.</span><span class="sxs-lookup"><span data-stu-id="a509a-117">hello +user parameter also removes hello last provisioned user account.</span></span> <span data-ttu-id="a509a-118">Если учетные данные учетной записи в toohello виртуальной Машины встраивание, пропустите это + параметр пользователя.</span><span class="sxs-lookup"><span data-stu-id="a509a-118">If you are baking account credentials in toohello VM, leave out this +user parameter.</span></span> <span data-ttu-id="a509a-119">Hello следующий пример удаляет hello последняя подготовленного пользователя учетной записи:</span><span class="sxs-lookup"><span data-stu-id="a509a-119">hello following example removes hello last provisioned user account:</span></span>

    ```bash
    ssh azureuser@40.118.249.235
    sudo waagent -deprovision+user -force
    exit 
    ```

2. <span data-ttu-id="a509a-120">Войдите в tooyour учетная запись Azure с [входа az](https://docs.microsoft.com/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="a509a-120">Sign in tooyour Azure account with [az login](https://docs.microsoft.com/cli/azure/#login).</span></span>
3. <span data-ttu-id="a509a-121">Остановка и освобождать hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a509a-121">Stop and deallocate hello VM.</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="a509a-122">Обобщить hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a509a-122">Generalize hello VM.</span></span> 

    ```azurecli
    az vm generalize --resource-group myResourceGroup --name myVM
    ``` 

<span data-ttu-id="a509a-123">hello toouse виртуальный жесткий ДИСК как диск для нового экземпляра существующей ВМ или диск данных, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="a509a-123">toouse hello VHD as a disk for a new instance of an existing VM or data disk, complete these steps:</span></span>

1.  <span data-ttu-id="a509a-124">Войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a509a-124">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2.  <span data-ttu-id="a509a-125">Hello концентратора меню **виртуальные машины**.</span><span class="sxs-lookup"><span data-stu-id="a509a-125">On hello Hub menu, click **Virtual Machines**.</span></span>
3.  <span data-ttu-id="a509a-126">Выберите hello виртуальной Машины из списка hello.</span><span class="sxs-lookup"><span data-stu-id="a509a-126">Select hello VM from hello list.</span></span>
4.  <span data-ttu-id="a509a-127">В колонке hello для hello виртуальной Машины, нажмите кнопку **остановить**.</span><span class="sxs-lookup"><span data-stu-id="a509a-127">On hello blade for hello VM, click **Stop**.</span></span>

    ![Остановка виртуальной машины](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a><span data-ttu-id="a509a-129">Создание URL-адреса SAS</span><span class="sxs-lookup"><span data-stu-id="a509a-129">Generate SAS URL</span></span>

<span data-ttu-id="a509a-130">toodownload hello VHD-файл, необходимо toogenerate [подписанного URL-адреса (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="a509a-130">toodownload hello VHD file, you need toogenerate a [shared access signature (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span></span> <span data-ttu-id="a509a-131">При формировании URL-адрес hello срок его действия назначается toohello URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="a509a-131">When hello URL is generated, an expiration time is assigned toohello URL.</span></span>

1.  <span data-ttu-id="a509a-132">Hello колонка hello для hello виртуальной Машины в меню **дисков**.</span><span class="sxs-lookup"><span data-stu-id="a509a-132">On hello menu of hello blade for hello VM, click **Disks**.</span></span>
2.  <span data-ttu-id="a509a-133">Выберите диск операционной системы hello для hello виртуальной Машины и нажмите кнопку **Экспорт**.</span><span class="sxs-lookup"><span data-stu-id="a509a-133">Select hello operating system disk for hello VM, and then click **Export**.</span></span>
3.  <span data-ttu-id="a509a-134">Нажмите кнопку **Создать URL-адрес**.</span><span class="sxs-lookup"><span data-stu-id="a509a-134">Click **Generate URL**.</span></span>

    ![Создание URL-адреса](./media/download-vhd/export-generate.png)

## <a name="download-vhd"></a><span data-ttu-id="a509a-136">Скачивание VHD</span><span class="sxs-lookup"><span data-stu-id="a509a-136">Download VHD</span></span>

1.  <span data-ttu-id="a509a-137">В группе hello URL-адрес, созданный выберите загруженный файл VHD hello.</span><span class="sxs-lookup"><span data-stu-id="a509a-137">Under hello URL that was generated, click Download hello VHD file.</span></span>

    ![Скачивание VHD](./media/download-vhd/export-download.png)

2.  <span data-ttu-id="a509a-139">Может потребоваться tooclick **Сохранить** в браузере toostart hello hello для загрузки.</span><span class="sxs-lookup"><span data-stu-id="a509a-139">You may need tooclick **Save** in hello browser toostart hello download.</span></span> <span data-ttu-id="a509a-140">имя по умолчанию Hello hello VHD-файл — *abcd*.</span><span class="sxs-lookup"><span data-stu-id="a509a-140">hello default name for hello VHD file is *abcd*.</span></span>

    ![Нажмите кнопку "Сохранить" в браузере hello](./media/download-vhd/export-save.png)

## <a name="next-steps"></a><span data-ttu-id="a509a-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a509a-142">Next steps</span></span>

- <span data-ttu-id="a509a-143">Узнайте, каким образом слишком[передача и создание виртуальной Машины Linux с пользовательской диска с hello Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a509a-143">Learn how too[upload and create a Linux VM from custom disk with hello Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 
- <span data-ttu-id="a509a-144">[Управление дисками Azure hello Azure CLI](tutorial-manage-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a509a-144">[Manage Azure disks hello Azure CLI](tutorial-manage-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

