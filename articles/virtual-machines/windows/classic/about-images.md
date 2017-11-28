---
title: "aaaAbout образов для виртуальных машин Windows | Документы Microsoft"
description: "Узнайте о том, как использовать образы с виртуальными машинами Windows в Azure."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 66ff3fab-8e7f-4dff-b8da-ab1c9c9c9af8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: cynthn
ms.openlocfilehash: c7cfa1d018a5e99d5b68f559ec9ae1f14e4dec8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="about-images-for-windows-virtual-machines"></a><span data-ttu-id="2a44b-103">Образы виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="2a44b-103">About images for Windows virtual machines</span></span>
> [!IMPORTANT]
> <span data-ttu-id="2a44b-104">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="2a44b-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="2a44b-105">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="2a44b-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="2a44b-106">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="2a44b-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="2a44b-107">Сведения о поиске и использование изображений в модели hello диспетчера ресурсов. в разделе [здесь](../../virtual-machines-windows-cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2a44b-107">For information about finding and using images in hello Resource Manager model, see [here](../../virtual-machines-windows-cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-about-images](../../../../includes/virtual-machines-common-classic-about-images.md)]

## <a name="working-with-images"></a><span data-ttu-id="2a44b-108">Работа с образами</span><span class="sxs-lookup"><span data-stu-id="2a44b-108">Working with images</span></span>

<span data-ttu-id="2a44b-109">Можно использовать модуль Azure PowerShell hello и hello Azure портала toomanage hello изображения доступен tooyour подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="2a44b-109">You can use hello Azure PowerShell module and hello Azure portal toomanage hello images available tooyour Azure subscription.</span></span> <span data-ttu-id="2a44b-110">Hello модуля Azure PowerShell предоставляет дополнительные параметры команды, чтобы точно определить, что можно проследить toosee или выполните.</span><span class="sxs-lookup"><span data-stu-id="2a44b-110">hello Azure PowerShell module provides more command options, so you can pinpoint exactly what you want toosee or do.</span></span> <span data-ttu-id="2a44b-111">Hello портал Azure предоставляет графический пользовательский Интерфейс для многих hello повседневных административных задач.</span><span class="sxs-lookup"><span data-stu-id="2a44b-111">hello Azure portal provides a GUI for many of hello everyday administrative tasks.</span></span>

<span data-ttu-id="2a44b-112">Вот несколько примеров использования модуля Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="2a44b-112">Here are some examples that use hello Azure PowerShell module.</span></span>

* <span data-ttu-id="2a44b-113">**Получить все образы**:`Get-AzureVMImage`возвращает список всех образов hello, доступных в текущей подписке: образов и предоставленных Azure или партнерами.</span><span class="sxs-lookup"><span data-stu-id="2a44b-113">**Get all images**:`Get-AzureVMImage`returns a list of all hello images available in your current subscription: your images and those provided by Azure or partners.</span></span> <span data-ttu-id="2a44b-114">полученный список Hello может быть большим.</span><span class="sxs-lookup"><span data-stu-id="2a44b-114">hello resulting list could be large.</span></span> <span data-ttu-id="2a44b-115">Здравствуйте далее примерах показано, как tooget более короткому списку.</span><span class="sxs-lookup"><span data-stu-id="2a44b-115">hello next examples show how tooget a shorter list.</span></span>
* <span data-ttu-id="2a44b-116">**Получить семейства образов.** `Get-AzureVMImage | select ImageFamily` возвращает список семейств образов, отображая свойство строк **ImageFamily**.</span><span class="sxs-lookup"><span data-stu-id="2a44b-116">**Get image families**:`Get-AzureVMImage | select ImageFamily` gets a list of image families by showing strings **ImageFamily** property.</span></span>
* <span data-ttu-id="2a44b-117">**Получить все образы из указанного семейства.** `Get-AzureVMImage | Where-Object {$_.ImageFamily -eq $family}`</span><span class="sxs-lookup"><span data-stu-id="2a44b-117">**Get all images in a specific family**: `Get-AzureVMImage | Where-Object {$_.ImageFamily -eq $family}`</span></span>
* <span data-ttu-id="2a44b-118">**Поиск образов виртуальных Машин**: `Get-AzureVMImage | where {(gm –InputObject $_ -Name DataDiskConfigurations) -ne $null} | Select -Property Label, ImageName` этот командлет работает путем фильтрации свойство DataDiskConfiguration hello, которое применяется только tooVM изображения.</span><span class="sxs-lookup"><span data-stu-id="2a44b-118">**Find VM Images**: `Get-AzureVMImage | where {(gm –InputObject $_ -Name DataDiskConfigurations) -ne $null} | Select -Property Label, ImageName` This cmdlet works by filtering hello DataDiskConfiguration property, which only applies tooVM Images.</span></span> <span data-ttu-id="2a44b-119">В этом примере также фильтры hello вывода tooonly hello метки и имени образ.</span><span class="sxs-lookup"><span data-stu-id="2a44b-119">This example also filters hello output tooonly hello label and image name.</span></span>
* <span data-ttu-id="2a44b-120">**Сохранить обобщенный образ.** `Save-AzureVMImage –ServiceName "myServiceName" –Name "MyVMtoCapture" –OSState "Generalized" –ImageName "MyVmImage" –ImageLabel "This is my generalized image"`</span><span class="sxs-lookup"><span data-stu-id="2a44b-120">**Save a generalized image**: `Save-AzureVMImage –ServiceName "myServiceName" –Name "MyVMtoCapture" –OSState "Generalized" –ImageName "MyVmImage" –ImageLabel "This is my generalized image"`</span></span>
* <span data-ttu-id="2a44b-121">**Сохранить специализированный образ.** `Save-AzureVMImage –ServiceName "mySvc2" –Name "MyVMToCapture2" –ImageName "myFirstVMImageSP" –OSState "Specialized" -Verbose`</span><span class="sxs-lookup"><span data-stu-id="2a44b-121">**Save a specialized image**: `Save-AzureVMImage –ServiceName "mySvc2" –Name "MyVMToCapture2" –ImageName "myFirstVMImageSP" –OSState "Specialized" -Verbose`</span></span>

  > [!TIP]
  > <span data-ttu-id="2a44b-122">параметр OSState Hello является обязательным toocreate образ виртуальной Машины, который включает hello диска операционной системы и присоединенных дисков с данными.</span><span class="sxs-lookup"><span data-stu-id="2a44b-122">hello OSState parameter is required toocreate a VM image, which includes hello operating system disk and attached data disks.</span></span> <span data-ttu-id="2a44b-123">Если вы не используете параметр hello, hello командлет создает образ ОС.</span><span class="sxs-lookup"><span data-stu-id="2a44b-123">If you don’t use hello parameter, hello cmdlet creates an OS image.</span></span> <span data-ttu-id="2a44b-124">Hello значение параметра hello указывает ли hello образа, обобщенный или специальный, на основании hello диск операционной системы был подготовлен для повторного использования.</span><span class="sxs-lookup"><span data-stu-id="2a44b-124">hello value of hello parameter indicates whether hello image is generalized or specialized, based on whether hello operating system disk has been prepared for reuse.</span></span>

* <span data-ttu-id="2a44b-125">**Удалить образ.** `Remove-AzureVMImage –ImageName "MyOldVmImage"`</span><span class="sxs-lookup"><span data-stu-id="2a44b-125">**Delete an image**: `Remove-AzureVMImage –ImageName "MyOldVmImage"`</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a44b-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2a44b-126">Next Steps</span></span>
<span data-ttu-id="2a44b-127">Вы также можете [Создание машины Windows с помощью портала Azure hello](tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="2a44b-127">You can also [create a Windows machine using hello Azure portal](tutorial.md).</span></span>
