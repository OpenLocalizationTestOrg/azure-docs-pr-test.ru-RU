---
title: "Об образах виртуальных машин Windows | Документация Майкрософт"
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
ms.openlocfilehash: d421cee0becabdf81d865036d0c98b12b077152b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="about-images-for-windows-virtual-machines"></a><span data-ttu-id="9a0b0-103">Образы виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="9a0b0-103">About images for Windows virtual machines</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9a0b0-104">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="9a0b0-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="9a0b0-105">В этой статье рассматривается использование классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="9a0b0-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="9a0b0-106">Для большинства новых развертываний Майкрософт рекомендует использовать модель диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9a0b0-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="9a0b0-107">Дополнительные сведения о применении и поиске образов в модели Resource Manager см. [здесь](../../virtual-machines-windows-cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9a0b0-107">For information about finding and using images in the Resource Manager model, see [here](../../virtual-machines-windows-cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-about-images](../../../../includes/virtual-machines-common-classic-about-images.md)]

## <a name="working-with-images"></a><span data-ttu-id="9a0b0-108">Работа с образами</span><span class="sxs-lookup"><span data-stu-id="9a0b0-108">Working with images</span></span>

<span data-ttu-id="9a0b0-109">Для управления образами, доступными в вашей подписке Azure, можно использовать модуль Azure PowerShell и портал Azure.</span><span class="sxs-lookup"><span data-stu-id="9a0b0-109">You can use the Azure PowerShell module and the Azure portal to manage the images available to your Azure subscription.</span></span> <span data-ttu-id="9a0b0-110">Модуль Azure PowerShell предоставляет дополнительные параметры команд, поэтому можно точно определить, что нужно просмотреть или сделать.</span><span class="sxs-lookup"><span data-stu-id="9a0b0-110">The Azure PowerShell module provides more command options, so you can pinpoint exactly what you want to see or do.</span></span> <span data-ttu-id="9a0b0-111">Портал Azure предоставляет графический пользовательский интерфейс для выполнения множества повседневных задач администрирования.</span><span class="sxs-lookup"><span data-stu-id="9a0b0-111">The Azure portal provides a GUI for many of the everyday administrative tasks.</span></span>

<span data-ttu-id="9a0b0-112">Ниже приведены некоторые примеры использования модуля Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9a0b0-112">Here are some examples that use the Azure PowerShell module.</span></span>

* <span data-ttu-id="9a0b0-113">**Получить все образы.** `Get-AzureVMImage` возвращает список всех образов, доступных в вашей текущей подписке (ваши образы и образы, предоставляемые Azure или партнерами).</span><span class="sxs-lookup"><span data-stu-id="9a0b0-113">**Get all images**:`Get-AzureVMImage`returns a list of all the images available in your current subscription: your images and those provided by Azure or partners.</span></span> <span data-ttu-id="9a0b0-114">Итоговый список может быть большим.</span><span class="sxs-lookup"><span data-stu-id="9a0b0-114">The resulting list could be large.</span></span> <span data-ttu-id="9a0b0-115">В следующих примерах показано, как сократить список.</span><span class="sxs-lookup"><span data-stu-id="9a0b0-115">The next examples show how to get a shorter list.</span></span>
* <span data-ttu-id="9a0b0-116">**Получить семейства образов.** `Get-AzureVMImage | select ImageFamily` возвращает список семейств образов, отображая свойство строк **ImageFamily**.</span><span class="sxs-lookup"><span data-stu-id="9a0b0-116">**Get image families**:`Get-AzureVMImage | select ImageFamily` gets a list of image families by showing strings **ImageFamily** property.</span></span>
* <span data-ttu-id="9a0b0-117">**Получить все образы из указанного семейства.** `Get-AzureVMImage | Where-Object {$_.ImageFamily -eq $family}`</span><span class="sxs-lookup"><span data-stu-id="9a0b0-117">**Get all images in a specific family**: `Get-AzureVMImage | Where-Object {$_.ImageFamily -eq $family}`</span></span>
* <span data-ttu-id="9a0b0-118">**Найти образы виртуальных машин:** `Get-AzureVMImage | where {(gm –InputObject $_ -Name DataDiskConfigurations) -ne $null} | Select -Property Label, ImageName` Этот командлет проводит фильтрацию по свойству DataDiskConfiguration, которое применяется только к образам виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="9a0b0-118">**Find VM Images**: `Get-AzureVMImage | where {(gm –InputObject $_ -Name DataDiskConfigurations) -ne $null} | Select -Property Label, ImageName` This cmdlet works by filtering the DataDiskConfiguration property, which only applies to VM Images.</span></span> <span data-ttu-id="9a0b0-119">В этом примере выходные данные также фильтруются, и выводятся только метка и имя образа.</span><span class="sxs-lookup"><span data-stu-id="9a0b0-119">This example also filters the output to only the label and image name.</span></span>
* <span data-ttu-id="9a0b0-120">**Сохранить обобщенный образ.** `Save-AzureVMImage –ServiceName "myServiceName" –Name "MyVMtoCapture" –OSState "Generalized" –ImageName "MyVmImage" –ImageLabel "This is my generalized image"`</span><span class="sxs-lookup"><span data-stu-id="9a0b0-120">**Save a generalized image**: `Save-AzureVMImage –ServiceName "myServiceName" –Name "MyVMtoCapture" –OSState "Generalized" –ImageName "MyVmImage" –ImageLabel "This is my generalized image"`</span></span>
* <span data-ttu-id="9a0b0-121">**Сохранить специализированный образ.** `Save-AzureVMImage –ServiceName "mySvc2" –Name "MyVMToCapture2" –ImageName "myFirstVMImageSP" –OSState "Specialized" -Verbose`</span><span class="sxs-lookup"><span data-stu-id="9a0b0-121">**Save a specialized image**: `Save-AzureVMImage –ServiceName "mySvc2" –Name "MyVMToCapture2" –ImageName "myFirstVMImageSP" –OSState "Specialized" -Verbose`</span></span>

  > [!TIP]
  > <span data-ttu-id="9a0b0-122">Параметр OSState является обязательным для создания образа виртуальной машины, содержащего диск операционной системы и подключенные диски данных.</span><span class="sxs-lookup"><span data-stu-id="9a0b0-122">The OSState parameter is required to create a VM image, which includes the operating system disk and attached data disks.</span></span> <span data-ttu-id="9a0b0-123">Если не указать этот параметр, командлет создает образ ОС.</span><span class="sxs-lookup"><span data-stu-id="9a0b0-123">If you don’t use the parameter, the cmdlet creates an OS image.</span></span> <span data-ttu-id="9a0b0-124">Значение параметра указывает, является ли образ обобщенным или специальным и основывается ли он на диске операционной системы, подготовленном для повторного использования.</span><span class="sxs-lookup"><span data-stu-id="9a0b0-124">The value of the parameter indicates whether the image is generalized or specialized, based on whether the operating system disk has been prepared for reuse.</span></span>

* <span data-ttu-id="9a0b0-125">**Удалить образ.** `Remove-AzureVMImage –ImageName "MyOldVmImage"`</span><span class="sxs-lookup"><span data-stu-id="9a0b0-125">**Delete an image**: `Remove-AzureVMImage –ImageName "MyOldVmImage"`</span></span>

## <a name="next-steps"></a><span data-ttu-id="9a0b0-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9a0b0-126">Next Steps</span></span>
<span data-ttu-id="9a0b0-127">Вы можете [создать виртуальную машину Windows с помощью портала Azure](tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="9a0b0-127">You can also [create a Windows machine using the Azure portal](tutorial.md).</span></span>
