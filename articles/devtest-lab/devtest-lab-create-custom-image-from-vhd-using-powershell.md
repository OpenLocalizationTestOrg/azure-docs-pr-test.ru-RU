---
title: "Создание пользовательского образа Azure DevTest Labs из VHD-файла с помощью PowerShell | Документация Майкрософт"
description: "Автоматизация создания пользовательского образа в Azure DevTest Labs из VHD-файла с помощью PowerShell"
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
ms.openlocfilehash: a4729f70aae80a13233fbe96a5d8a56c0c9d01d3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-image-from-a-vhd-file-using-powershell"></a><span data-ttu-id="f3303-103">Создание пользовательского образа из VHD-файла с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="f3303-103">Create a custom image from a VHD file using PowerShell</span></span>

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="f3303-104">Пошаговые инструкции</span><span class="sxs-lookup"><span data-stu-id="f3303-104">Step-by-step instructions</span></span>

<span data-ttu-id="f3303-105">Чтобы создать пользовательский образ из VHD-файла с помощью PowerShell, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="f3303-105">The following steps walk you through creating a custom image from a VHD file using PowerShell:</span></span>

1. <span data-ttu-id="f3303-106">В командной строке PowerShell войдите в учетную запись Azure, вызвав командлет **Login-AzureRmAccount**.</span><span class="sxs-lookup"><span data-stu-id="f3303-106">At a PowerShell prompt, log in to your Azure account with the following call to the **Login-AzureRmAccount** cmdlet.</span></span>  
    
    ```PowerShell
    Login-AzureRmAccount
    ```

1.  <span data-ttu-id="f3303-107">Выберите необходимую подписку Azure, вызвав командлет **Select-AzureRmSubscription**.</span><span class="sxs-lookup"><span data-stu-id="f3303-107">Select the desired Azure subscription by calling the **Select-AzureRmSubscription** cmdlet.</span></span> <span data-ttu-id="f3303-108">Замените заполнитель для переменной **$subscriptionId** на идентификатор действующей подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="f3303-108">Replace the following placeholder for the **$subscriptionId** variable with a valid Azure subscription ID.</span></span> 

    ```PowerShell
    $subscriptionId = '<Specify your subscription ID here>'
    Select-AzureRmSubscription -SubscriptionId $subscriptionId
    ```

1.  <span data-ttu-id="f3303-109">Получите объект лаборатории, вызвав командлет **Get AzureRmResource**.</span><span class="sxs-lookup"><span data-stu-id="f3303-109">Get the lab object by calling the **Get-AzureRmResource** cmdlet.</span></span> <span data-ttu-id="f3303-110">Замените заполнители для переменных **$labRg** и **$labName** на соответствующие значения для своей среды.</span><span class="sxs-lookup"><span data-stu-id="f3303-110">Replace the following placeholders for the **$labRg** and **$labName** variables with the appropriate values for your environment.</span></span> 

    ```PowerShell
    $labRg = '<Specify your lab resource group name here>'
    $labName = '<Specify your lab name here>'
    $lab = Get-AzureRmResource -ResourceId ('/subscriptions/' + $subscriptionId + '/resourceGroups/' + $labRg + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    ```
 
1.  <span data-ttu-id="f3303-111">Получите значения учетной записи хранения лаборатории и ключа этой учетной записи из объекта лаборатории.</span><span class="sxs-lookup"><span data-stu-id="f3303-111">Get the lab storage account and lab storage account key values from the lab object.</span></span> 

    ```PowerShell
    $labStorageAccount = Get-AzureRmResource -ResourceId $lab.Properties.defaultStorageAccount 
    $labStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $labStorageAccount.ResourceGroupName -Name $labStorageAccount.ResourceName)[0].Value
    ```

1.  <span data-ttu-id="f3303-112">Замените заполнитель для переменной **$vhdUri** на URI своего VHD-файла.</span><span class="sxs-lookup"><span data-stu-id="f3303-112">Replace the following placeholder for the **$vhdUri** variable with the URI to your uploaded VHD file.</span></span> <span data-ttu-id="f3303-113">URI VHD-файла можно получить в колонке учетной записи хранилища BLOB-объектов на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="f3303-113">You can get the VHD file's URI from the storage account's blob blade in the Azure portal.</span></span>

    ```PowerShell
    $vhdUri = '<Specify the VHD URI here>'
    ```

1.  <span data-ttu-id="f3303-114">Создайте пользовательский образ, используя командлет **New-AzureRmResourceGroupDeployment**.</span><span class="sxs-lookup"><span data-stu-id="f3303-114">Create the custom image using the **New-AzureRmResourceGroupDeployment** cmdlet.</span></span> <span data-ttu-id="f3303-115">Замените следующие заполнители для переменных **$customImageName** и **$customImageDescription** на значимые имена для своей среды.</span><span class="sxs-lookup"><span data-stu-id="f3303-115">Replace the following placeholders for the **$customImageName** and **$customImageDescription** variables to meaningful names for your environment.</span></span>

    ```PowerShell
    $customImageName = '<Specify the custom image name>'
    $customImageDescription = '<Specify the custom image description>'

    $parameters = @{existingLabName="$($lab.Name)"; existingVhdUri=$vhdUri; imageOsType='windows'; isVhdSysPrepped=$false; imageName=$customImageName; imageDescription=$customImageDescription}

    New-AzureRmResourceGroupDeployment -ResourceGroupName $lab.ResourceGroupName -Name CreateCustomImage -TemplateUri 'https://raw.githubusercontent.com/Azure/azure-devtestlab/master/Samples/201-dtl-create-customimage-from-vhd/azuredeploy.json' -TemplateParameterObject $parameters
    ```

## <a name="powershell-script-to-create-a-custom-image-from-a-vhd-file"></a><span data-ttu-id="f3303-116">Создание пользовательского образа из VHD-файла с помощью сценария PowerShell</span><span class="sxs-lookup"><span data-stu-id="f3303-116">PowerShell script to create a custom image from a VHD file</span></span>

<span data-ttu-id="f3303-117">Следующий сценарий PowerShell позволяет создать пользовательский образ из VHD-файла.</span><span class="sxs-lookup"><span data-stu-id="f3303-117">The following PowerShell script can be used to create a custom image from a VHD file.</span></span> <span data-ttu-id="f3303-118">Замените заполнители, выделенные угловыми скобками, на необходимые значения.</span><span class="sxs-lookup"><span data-stu-id="f3303-118">Replace the placeholders (starting and ending with angle brackets) with the appropriate values for your needs.</span></span> 

```PowerShell
# Log in to your Azure account.  
Login-AzureRmAccount

# Select the desired Azure subscription. 
$subscriptionId = '<Specify your subscription ID here>'
Select-AzureRmSubscription -SubscriptionId $subscriptionId

# Get the lab object.
$labRg = '<Specify your lab resource group name here>'
$labName = '<Specify your lab name here>'
$lab = Get-AzureRmResource -ResourceId ('/subscriptions/' + $subscriptionId + '/resourceGroups/' + $labRg + '/providers/Microsoft.DevTestLab/labs/' + $labName)

# Get the lab storage account and lab storage account key values.
$labStorageAccount = Get-AzureRmResource -ResourceId $lab.Properties.defaultStorageAccount 
$labStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $labStorageAccount.ResourceGroupName -Name $labStorageAccount.ResourceName)[0].Value

# Set the URI of the VHD file.  
$vhdUri = '<Specify the VHD URI here>'

# Set the custom image name and description values.
$customImageName = '<Specify the custom image name>'
$customImageDescription = '<Specify the custom image description>'

# Set up the parameters object.
$parameters = @{existingLabName="$($lab.Name)"; existingVhdUri=$vhdUri; imageOsType='windows'; isVhdSysPrepped=$false; imageName=$customImageName; imageDescription=$customImageDescription}

# Create the custom image. 
New-AzureRmResourceGroupDeployment -ResourceGroupName $lab.ResourceGroupName -Name CreateCustomImage -TemplateUri 'https://raw.githubusercontent.com/Azure/azure-devtestlab/master/Samples/201-dtl-create-customimage-from-vhd/azuredeploy.json' -TemplateParameterObject $parameters
```

## <a name="related-blog-posts"></a><span data-ttu-id="f3303-119">Связанные записи в блогах</span><span class="sxs-lookup"><span data-stu-id="f3303-119">Related blog posts</span></span>

- [<span data-ttu-id="f3303-120">Custom images or formulas? (Пользовательские изображения или формулы?)</span><span class="sxs-lookup"><span data-stu-id="f3303-120">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="f3303-121">Copying Custom Images between Azure DevTest Labs (Копирование пользовательских образов между лабораториями для разработки и тестирования Azure)</span><span class="sxs-lookup"><span data-stu-id="f3303-121">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="f3303-122">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f3303-122">Next steps</span></span>

- [<span data-ttu-id="f3303-123">Добавление виртуальной машины с артефактами в лабораторию в Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="f3303-123">Add a VM to your lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
