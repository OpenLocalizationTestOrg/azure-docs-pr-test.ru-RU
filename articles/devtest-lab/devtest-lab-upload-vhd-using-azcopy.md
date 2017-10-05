---
title: "Отправка VHD-файла в Azure Labs DevTest с помощью AzCopy | Документация Майкрософт"
description: "Отправка VHD-файла в учетную запись хранения лаборатории с помощью AzCopy"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: a4f43354740d9f17570932b0b9c753f46d67dc33
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="upload-vhd-file-to-labs-storage-account-using-azcopy"></a><span data-ttu-id="ed110-103">Отправка VHD-файла в учетную запись хранения лаборатории с помощью AzCopy</span><span class="sxs-lookup"><span data-stu-id="ed110-103">Upload VHD file to lab's storage account using AzCopy</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="ed110-104">В Azure DevTest Labs с помощью VHD-файлов можно создать пользовательские образы, используемые для подготовки виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="ed110-104">In Azure DevTest Labs, VHD files can be used to create custom images, which are used to provision virtual machines.</span></span> <span data-ttu-id="ed110-105">Ниже приведены пошаговые инструкции по отправке VHD-файла в учетную запись хранения лаборатории с помощью служебной программы командной строки AzCopy.</span><span class="sxs-lookup"><span data-stu-id="ed110-105">The following steps walk you through using the AzCopy command-line utility to upload a VHD file to a lab's storage account.</span></span> <span data-ttu-id="ed110-106">После отправки VHD-файла переходите к разделу [Дальнейшие действия](#next-steps), где перечислены несколько статей, в которых описывается создание пользовательского образа из загруженного VHD-файла.</span><span class="sxs-lookup"><span data-stu-id="ed110-106">Once you've uploaded your VHD file, the [Next steps section](#next-steps) lists some articles that illustrate how to create a custom image from the uploaded VHD file.</span></span> <span data-ttu-id="ed110-107">Дополнительные сведения о дисках и виртуальных жестких дисках в Azure см. в статье [О дисках и виртуальных жестких дисках для виртуальных машин Azure](../virtual-machines/linux/about-disks-and-vhds.md)</span><span class="sxs-lookup"><span data-stu-id="ed110-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

> [!NOTE] 
>  
> <span data-ttu-id="ed110-108">AzCopy является служебной программой командной строки только для Windows.</span><span class="sxs-lookup"><span data-stu-id="ed110-108">AzCopy is a Windows-only command-line utility.</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="ed110-109">Пошаговые инструкции</span><span class="sxs-lookup"><span data-stu-id="ed110-109">Step-by-step instructions</span></span>

<span data-ttu-id="ed110-110">Ниже приведены пошаговые инструкции по отправке VHD-файла в Azure DevTest Labs с помощью [AzCopy](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="ed110-110">The following steps walk you through uploading a VHD file to Azure DevTest Labs using [AzCopy](http://aka.ms/downloadazcopy).</span></span> 

1. <span data-ttu-id="ed110-111">Узнайте имя учетной записи хранения лаборатории с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="ed110-111">Get the name of the lab's storage account using the Azure portal:</span></span>

1. <span data-ttu-id="ed110-112">Войдите на [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="ed110-112">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="ed110-113">Щелкните **Другие службы**, а затем выберите в списке **DevTest Labs**.</span><span class="sxs-lookup"><span data-stu-id="ed110-113">Select **More services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="ed110-114">Из списка лабораторий выберите нужную лабораторию.</span><span class="sxs-lookup"><span data-stu-id="ed110-114">From the list of labs, select the desired lab.</span></span>  

1. <span data-ttu-id="ed110-115">В колонке лаборатории выберите **Конфигурация**.</span><span class="sxs-lookup"><span data-stu-id="ed110-115">On the lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="ed110-116">В колонке **Configuration** (Конфигурация) лаборатории выберите **Custom images (VHDs)** (Пользовательские образы (VHD)).</span><span class="sxs-lookup"><span data-stu-id="ed110-116">On the lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="ed110-117">В колонке **Custom images** (Пользовательские образы) выберите **+Add** (+ Добавить).</span><span class="sxs-lookup"><span data-stu-id="ed110-117">On the **Custom images** blade, Select **+Add**.</span></span> 

1. <span data-ttu-id="ed110-118">В колонке **Custom images** (Пользовательские образы) выберите **VHD**.</span><span class="sxs-lookup"><span data-stu-id="ed110-118">On the **Custom image** blade, select **VHD**.</span></span>

1. <span data-ttu-id="ed110-119">В колонке **VHD** щелкните **Upload a VHD file using PowerShell** (Отправить VHD-файл с помощью PowerShell).</span><span class="sxs-lookup"><span data-stu-id="ed110-119">On the **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>

    ![Отправка VHD с помощью PowerShell](./media/devtest-lab-upload-vhd-using-azcopy/upload-image-using-psh.png)

1. <span data-ttu-id="ed110-121">В колонке **Upload an image using PowerShell** (Отправка образа с помощью PowerShell) отображается вызов командлета **Add-AzureVhd**.</span><span class="sxs-lookup"><span data-stu-id="ed110-121">The **Upload an image using PowerShell** blade displays a call to the **Add-AzureVhd** cmdlet.</span></span> <span data-ttu-id="ed110-122">Первый параметр (*Назначение*) содержит URI для контейнера больших двоичных объектов (*отправки*) в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="ed110-122">The first parameter (*Destination*) contains the URI for a blob container (*uploads*) in the following format:</span></span>

    ```
    https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...
    ``` 

1. <span data-ttu-id="ed110-123">Запишите полный URI, так как он понадобится вам дальше.</span><span class="sxs-lookup"><span data-stu-id="ed110-123">Make note of the full URI as it is used in later steps.</span></span>

1. <span data-ttu-id="ed110-124">Отправьте VHD-файл с помощью AzCopy.</span><span class="sxs-lookup"><span data-stu-id="ed110-124">Upload the VHD file using AzCopy:</span></span>
 
1. <span data-ttu-id="ed110-125">[Скачайте и установите последнюю версию AzCopy](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="ed110-125">[Download and install the latest version of AzCopy](http://aka.ms/downloadazcopy).</span></span>

1. <span data-ttu-id="ed110-126">Откройте окно командной строки и перейдите к каталогу установки AzCopy.</span><span class="sxs-lookup"><span data-stu-id="ed110-126">Open a command window and navigate to the AzCopy installation directory.</span></span> <span data-ttu-id="ed110-127">При необходимости можно добавить место установки AzCopy к системному пути.</span><span class="sxs-lookup"><span data-stu-id="ed110-127">Optionally, you can add the AzCopy installation location to your system path.</span></span> <span data-ttu-id="ed110-128">По умолчанию AzCopy устанавливается в следующий каталог:</span><span class="sxs-lookup"><span data-stu-id="ed110-128">By default, AzCopy is installed to the following directory:</span></span>

    ```command-line
    %ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy
    ```

1. <span data-ttu-id="ed110-129">Используя ключ учетной записи и URI контейнера больших двоичных объектов, выполните следующую команду в командной строке.</span><span class="sxs-lookup"><span data-stu-id="ed110-129">Using the storage account key and blob container URI, run the following command at the command prompt.</span></span> <span data-ttu-id="ed110-130">Значение *vhdFileName* должно быть заключено в кавычки.</span><span class="sxs-lookup"><span data-stu-id="ed110-130">The *vhdFileName* value needs to be in quotes.</span></span> <span data-ttu-id="ed110-131">В зависимости от размера VHD-файла и скорости подключения процесс передачи файла может занять длительное время.</span><span class="sxs-lookup"><span data-stu-id="ed110-131">The process of uploading a VHD file can be lengthy depending on the size of the VHD file and your connection speed.</span></span>   

    ```command-line
    AzCopy /Source:<sourceDirectory> /Dest:<blobContainerUri> /DestKey:<storageAccountKey> /Pattern:"<vhdFileName>" /BlobType:page
    ```

## <a name="next-steps"></a><span data-ttu-id="ed110-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ed110-132">Next steps</span></span>

- [<span data-ttu-id="ed110-133">Управление пользовательскими образами Azure DevTest Labs для создания виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="ed110-133">Create a custom image in Azure DevTest Labs from a VHD file using the Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="ed110-134">Создание пользовательского образа из VHD-файла с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="ed110-134">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)