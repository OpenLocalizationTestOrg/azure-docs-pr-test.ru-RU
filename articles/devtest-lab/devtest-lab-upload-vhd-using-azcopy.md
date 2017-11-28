---
title: "aaaUpload VHD-файл tooAzure DevTest Labs, с помощью AzCopy | Документы Microsoft"
description: "Отправка VHD файл toolab учетной записи хранилища с помощью AzCopy"
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
ms.openlocfilehash: 14f9e933b0bd27451f6bcb94841ecc381213e578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-azcopy"></a><span data-ttu-id="5c791-103">Отправка VHD файл toolab учетной записи хранилища с помощью AzCopy</span><span class="sxs-lookup"><span data-stu-id="5c791-103">Upload VHD file toolab's storage account using AzCopy</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="5c791-104">В Azure DevTest Labs VHD-файлы могут быть используется toocreate пользовательские образы, которые являются tooprovision используемых виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="5c791-104">In Azure DevTest Labs, VHD files can be used toocreate custom images, which are used tooprovision virtual machines.</span></span> <span data-ttu-id="5c791-105">Hello следующие шаги описывают с помощью программы командной строки tooupload hello AzCopy учетную запись хранения лаборатории файл виртуального жесткого диска tooa.</span><span class="sxs-lookup"><span data-stu-id="5c791-105">hello following steps walk you through using hello AzCopy command-line utility tooupload a VHD file tooa lab's storage account.</span></span> <span data-ttu-id="5c791-106">После отправки вашего VHD-файла, hello [дальнейшие действия раздела](#next-steps) перечислены некоторые статей, которые показывают, как toocreate пользовательского образа из hello отправили файл виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="5c791-106">Once you've uploaded your VHD file, hello [Next steps section](#next-steps) lists some articles that illustrate how toocreate a custom image from hello uploaded VHD file.</span></span> <span data-ttu-id="5c791-107">См. дополнительные сведения [о дисках и виртуальных жестких дисках для виртуальных машин Azure](../virtual-machines/linux/about-disks-and-vhds.md).</span><span class="sxs-lookup"><span data-stu-id="5c791-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

> [!NOTE] 
>  
> <span data-ttu-id="5c791-108">AzCopy является служебной программой командной строки только для Windows.</span><span class="sxs-lookup"><span data-stu-id="5c791-108">AzCopy is a Windows-only command-line utility.</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="5c791-109">Пошаговые инструкции</span><span class="sxs-lookup"><span data-stu-id="5c791-109">Step-by-step instructions</span></span>

<span data-ttu-id="5c791-110">Здравствуйте, следуя обход действия можно выполнить с помощью Отправка VHD файлов tooAzure DevTest Labs с помощью [AzCopy](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="5c791-110">hello following steps walk you through uploading a VHD file tooAzure DevTest Labs using [AzCopy](http://aka.ms/downloadazcopy).</span></span> 

1. <span data-ttu-id="5c791-111">Получите имя hello hello лаборатории учетной записи хранилища с помощью портала Azure hello:</span><span class="sxs-lookup"><span data-stu-id="5c791-111">Get hello name of hello lab's storage account using hello Azure portal:</span></span>

1. <span data-ttu-id="5c791-112">Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="5c791-112">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="5c791-113">Выберите **дополнительные службы**, а затем выберите **DevTest Labs** из списка hello.</span><span class="sxs-lookup"><span data-stu-id="5c791-113">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="5c791-114">Выберите из списка hello лабораториям hello требуемой лаборатории.</span><span class="sxs-lookup"><span data-stu-id="5c791-114">From hello list of labs, select hello desired lab.</span></span>  

1. <span data-ttu-id="5c791-115">В колонке hello лаборатории выберите **конфигурации**.</span><span class="sxs-lookup"><span data-stu-id="5c791-115">On hello lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="5c791-116">В лаборатории hello **конфигурации** колонке выберите **пользовательских изображений (VHD)**.</span><span class="sxs-lookup"><span data-stu-id="5c791-116">On hello lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="5c791-117">На hello **пользовательских образов** колонке выберите **+ добавить**.</span><span class="sxs-lookup"><span data-stu-id="5c791-117">On hello **Custom images** blade, Select **+Add**.</span></span> 

1. <span data-ttu-id="5c791-118">На hello **настраиваемое изображение** колонке выберите **VHD**.</span><span class="sxs-lookup"><span data-stu-id="5c791-118">On hello **Custom image** blade, select **VHD**.</span></span>

1. <span data-ttu-id="5c791-119">На hello **VHD** колонке выберите **отправить VHD с помощью PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="5c791-119">On hello **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>

    ![Отправка VHD с помощью PowerShell](./media/devtest-lab-upload-vhd-using-azcopy/upload-image-using-psh.png)

1. <span data-ttu-id="5c791-121">Hello **отправить изображение с помощью PowerShell** колонке отображает toohello вызов **Add-AzureVhd** командлета.</span><span class="sxs-lookup"><span data-stu-id="5c791-121">hello **Upload an image using PowerShell** blade displays a call toohello **Add-AzureVhd** cmdlet.</span></span> <span data-ttu-id="5c791-122">Здравствуйте, первый параметр (*назначения*) содержит hello URI контейнера больших двоичных объектов (*отправляет*) в кодировке hello:</span><span class="sxs-lookup"><span data-stu-id="5c791-122">hello first parameter (*Destination*) contains hello URI for a blob container (*uploads*) in hello following format:</span></span>

    ```
    https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...
    ``` 

1. <span data-ttu-id="5c791-123">Запишите hello полный URI, поскольку он используется в последующих шагах.</span><span class="sxs-lookup"><span data-stu-id="5c791-123">Make note of hello full URI as it is used in later steps.</span></span>

1. <span data-ttu-id="5c791-124">Отправьте файл виртуального жесткого диска hello, с помощью AzCopy.</span><span class="sxs-lookup"><span data-stu-id="5c791-124">Upload hello VHD file using AzCopy:</span></span>
 
1. <span data-ttu-id="5c791-125">[Загрузите и установите последнюю версию hello AzCopy](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="5c791-125">[Download and install hello latest version of AzCopy](http://aka.ms/downloadazcopy).</span></span>

1. <span data-ttu-id="5c791-126">Откройте окно командной строки и перейдите в каталог установки toohello AzCopy.</span><span class="sxs-lookup"><span data-stu-id="5c791-126">Open a command window and navigate toohello AzCopy installation directory.</span></span> <span data-ttu-id="5c791-127">При необходимости можно добавить hello AzCopy tooyour системы путь установки.</span><span class="sxs-lookup"><span data-stu-id="5c791-127">Optionally, you can add hello AzCopy installation location tooyour system path.</span></span> <span data-ttu-id="5c791-128">По умолчанию AzCopy — установленных toohello следующий каталог:</span><span class="sxs-lookup"><span data-stu-id="5c791-128">By default, AzCopy is installed toohello following directory:</span></span>

    ```command-line
    %ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy
    ```

1. <span data-ttu-id="5c791-129">С помощью hello контейнера учетной записи хранилища ключей и BLOB-объект URI, запустите следующую команду в командной строке hello hello.</span><span class="sxs-lookup"><span data-stu-id="5c791-129">Using hello storage account key and blob container URI, run hello following command at hello command prompt.</span></span> <span data-ttu-id="5c791-130">Hello *vhdFileName* значение должно toobe в кавычки.</span><span class="sxs-lookup"><span data-stu-id="5c791-130">hello *vhdFileName* value needs toobe in quotes.</span></span> <span data-ttu-id="5c791-131">Hello процесс передачи файла виртуального жесткого диска может быть длительное время, в зависимости от размера hello hello VHD-файл и скорость подключения.</span><span class="sxs-lookup"><span data-stu-id="5c791-131">hello process of uploading a VHD file can be lengthy depending on hello size of hello VHD file and your connection speed.</span></span>   

    ```command-line
    AzCopy /Source:<sourceDirectory> /Dest:<blobContainerUri> /DestKey:<storageAccountKey> /Pattern:"<vhdFileName>" /BlobType:page
    ```

## <a name="next-steps"></a><span data-ttu-id="5c791-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5c791-132">Next steps</span></span>

- [<span data-ttu-id="5c791-133">Создание пользовательского образа в Azure DevTest Labs файла виртуального жесткого диска с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="5c791-133">Create a custom image in Azure DevTest Labs from a VHD file using hello Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="5c791-134">Создание пользовательского образа из VHD-файла с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="5c791-134">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)