---
title: "aaaUpload VHD-файл tooAzure DevTest Labs, с помощью PowerShell | Документы Microsoft"
description: "Отправка VHD файл toolab учетной записи хранилища с помощью PowerShell"
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
ms.openlocfilehash: 9c3ee96e212457b0ef8203714b419350cb97f895
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-powershell"></a><span data-ttu-id="5129b-103">Отправка VHD файл toolab учетной записи хранилища с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="5129b-103">Upload VHD file toolab's storage account using PowerShell</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="5129b-104">В Azure DevTest Labs VHD-файлы могут быть используется toocreate пользовательские образы, которые являются tooprovision используемых виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="5129b-104">In Azure DevTest Labs, VHD files can be used toocreate custom images, which are used tooprovision virtual machines.</span></span> <span data-ttu-id="5129b-105">Hello следующие шаги описывают с помощью PowerShell tooupload учетную запись хранения лаборатории файл виртуального жесткого диска tooa.</span><span class="sxs-lookup"><span data-stu-id="5129b-105">hello following steps walk you through using PowerShell tooupload a VHD file tooa lab's storage account.</span></span> <span data-ttu-id="5129b-106">После отправки вашего VHD-файла, hello [дальнейшие действия раздела](#next-steps) перечислены некоторые статей, которые показывают, как toocreate пользовательского образа из hello отправили файл виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="5129b-106">Once you've uploaded your VHD file, hello [Next steps section](#next-steps) lists some articles that illustrate how toocreate a custom image from hello uploaded VHD file.</span></span> <span data-ttu-id="5129b-107">См. дополнительные сведения [о дисках и виртуальных жестких дисках для виртуальных машин Azure](../virtual-machines/linux/about-disks-and-vhds.md).</span><span class="sxs-lookup"><span data-stu-id="5129b-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="5129b-108">Пошаговые инструкции</span><span class="sxs-lookup"><span data-stu-id="5129b-108">Step-by-step instructions</span></span>

<span data-ttu-id="5129b-109">Здравствуйте, следуя обход действия можно выполнить с помощью Отправка VHD файлов tooAzure DevTest Labs, с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5129b-109">hello following steps walk you through uploading a VHD file tooAzure DevTest Labs using PowerShell.</span></span> 

1. <span data-ttu-id="5129b-110">Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="5129b-110">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="5129b-111">Выберите **дополнительные службы**, а затем выберите **DevTest Labs** из списка hello.</span><span class="sxs-lookup"><span data-stu-id="5129b-111">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="5129b-112">Выберите из списка hello лабораториям hello требуемой лаборатории.</span><span class="sxs-lookup"><span data-stu-id="5129b-112">From hello list of labs, select hello desired lab.</span></span>  

1. <span data-ttu-id="5129b-113">В колонке hello лаборатории выберите **конфигурации**.</span><span class="sxs-lookup"><span data-stu-id="5129b-113">On hello lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="5129b-114">В лаборатории hello **конфигурации** колонке выберите **пользовательских изображений (VHD)**.</span><span class="sxs-lookup"><span data-stu-id="5129b-114">On hello lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="5129b-115">На hello **пользовательских образов** колонке выберите **+ добавить**.</span><span class="sxs-lookup"><span data-stu-id="5129b-115">On hello **Custom images** blade, Select **+Add**.</span></span> 

1. <span data-ttu-id="5129b-116">На hello **настраиваемое изображение** колонке выберите **VHD**.</span><span class="sxs-lookup"><span data-stu-id="5129b-116">On hello **Custom image** blade, select **VHD**.</span></span>

1. <span data-ttu-id="5129b-117">На hello **VHD** колонке выберите **отправить VHD с помощью PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="5129b-117">On hello **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>

    ![Отправка VHD с помощью PowerShell](./media/devtest-lab-upload-vhd-using-powershell/upload-image-using-psh.png)

1. <span data-ttu-id="5129b-119">На hello **отправить изображение с помощью PowerShell** колонки, копирования hello созданный скрипт PowerShell tooa текстовый редактор.</span><span class="sxs-lookup"><span data-stu-id="5129b-119">On hello **Upload an image using PowerShell** blade, copy hello generated PowerShell script tooa text editor.</span></span>

1. <span data-ttu-id="5129b-120">Изменение hello **LocalFilePath** параметр hello **Add-AzureVhd** командлет toopoint toohello расположение файла виртуального жесткого диска, который необходимо tooupload hello.</span><span class="sxs-lookup"><span data-stu-id="5129b-120">Modify hello **LocalFilePath** parameter of hello **Add-AzureVhd** cmdlet toopoint toohello location of hello VHD file you want tooupload.</span></span>

1. <span data-ttu-id="5129b-121">В командной строке PowerShell выполните hello **Add-AzureVhd** командлета (с hello изменения **LocalFilePath** параметр).</span><span class="sxs-lookup"><span data-stu-id="5129b-121">At a PowerShell prompt, run hello **Add-AzureVhd** cmdlet (with hello modified **LocalFilePath** parameter).</span></span>

> [!WARNING] 
> 
> <span data-ttu-id="5129b-122">Hello процесс передачи файла виртуального жесткого диска может быть длительное время, в зависимости от размера hello hello VHD-файл и скорость подключения.</span><span class="sxs-lookup"><span data-stu-id="5129b-122">hello process of uploading a VHD file can be lengthy depending on hello size of hello VHD file and your connection speed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5129b-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5129b-123">Next steps</span></span>

- [<span data-ttu-id="5129b-124">Создание пользовательского образа в Azure DevTest Labs файла виртуального жесткого диска с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="5129b-124">Create a custom image in Azure DevTest Labs from a VHD file using hello Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="5129b-125">Создание пользовательского образа из VHD-файла с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="5129b-125">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)
