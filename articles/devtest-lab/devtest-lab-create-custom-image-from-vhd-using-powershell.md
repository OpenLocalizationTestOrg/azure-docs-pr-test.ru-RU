---
title: "aaaCreate Azure DevTest Labs образ из VHD-файла с помощью PowerShell | Документы Microsoft"
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
ms.openlocfilehash: 39b4005fa46cdf86cf0800ca376128134bcfb650
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vhd-file-using-powershell"></a><span data-ttu-id="c8f26-103">Создание пользовательского образа из VHD-файла с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="c8f26-103">Create a custom image from a VHD file using PowerShell</span></span>

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="c8f26-104">Пошаговые инструкции</span><span class="sxs-lookup"><span data-stu-id="c8f26-104">Step-by-step instructions</span></span>

<span data-ttu-id="c8f26-105">Hello следующие шаги содержат пошаговые инструкции по созданию настраиваемого образа из VHD-файла с помощью PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c8f26-105">hello following steps walk you through creating a custom image from a VHD file using PowerShell:</span></span>

1. <span data-ttu-id="c8f26-106">В командной строке PowerShell, войдите в tooyour учетная запись Azure с hello после вызова toohello **AzureRmAccount входа** командлета.</span><span class="sxs-lookup"><span data-stu-id="c8f26-106">At a PowerShell prompt, log in tooyour Azure account with hello following call toohello **Login-AzureRmAccount** cmdlet.</span></span>  
    
    ```PowerShell
    Login-AzureRmAccount
    ```

1.  <span data-ttu-id="c8f26-107">Выберите hello требуемого подписки Azure, вызывающему Привет **AzureRmSubscription выберите** командлета.</span><span class="sxs-lookup"><span data-stu-id="c8f26-107">Select hello desired Azure subscription by calling hello **Select-AzureRmSubscription** cmdlet.</span></span> <span data-ttu-id="c8f26-108">Замените следующие заполнитель для hello hello **$subscriptionId** переменных с идентификатором действительной подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="c8f26-108">Replace hello following placeholder for hello **$subscriptionId** variable with a valid Azure subscription ID.</span></span> 

    ```PowerShell
    $subscriptionId = '<Specify your subscription ID here>'
    Select-AzureRmSubscription -SubscriptionId $subscriptionId
    ```

1.  <span data-ttu-id="c8f26-109">Получить hello лабораторного объекта, вызывающего hello **Get-AzureRmResource** командлета.</span><span class="sxs-lookup"><span data-stu-id="c8f26-109">Get hello lab object by calling hello **Get-AzureRmResource** cmdlet.</span></span> <span data-ttu-id="c8f26-110">Замените следующие местозаполнители для hello hello **$labRg** и **$labName** переменных с hello соответствующие значения для вашей среды.</span><span class="sxs-lookup"><span data-stu-id="c8f26-110">Replace hello following placeholders for hello **$labRg** and **$labName** variables with hello appropriate values for your environment.</span></span> 

    ```PowerShell
    $labRg = '<Specify your lab resource group name here>'
    $labName = '<Specify your lab name here>'
    $lab = Get-AzureRmResource -ResourceId ('/subscriptions/' + $subscriptionId + '/resourceGroups/' + $labRg + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    ```
 
1.  <span data-ttu-id="c8f26-111">Получите учетную запись хранения лаборатории hello и учетную запись хранения лаборатории значения ключа из hello лабораторного объекта.</span><span class="sxs-lookup"><span data-stu-id="c8f26-111">Get hello lab storage account and lab storage account key values from hello lab object.</span></span> 

    ```PowerShell
    $labStorageAccount = Get-AzureRmResource -ResourceId $lab.Properties.defaultStorageAccount 
    $labStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $labStorageAccount.ResourceGroupName -Name $labStorageAccount.ResourceName)[0].Value
    ```

1.  <span data-ttu-id="c8f26-112">Замените следующие заполнитель для hello hello **$vhdUri** переменных с hello URI tooyour загружен файл виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="c8f26-112">Replace hello following placeholder for hello **$vhdUri** variable with hello URI tooyour uploaded VHD file.</span></span> <span data-ttu-id="c8f26-113">URI hello VHD-файл можно получить из колонки BLOB-объектов учетной записи хранилища hello в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c8f26-113">You can get hello VHD file's URI from hello storage account's blob blade in hello Azure portal.</span></span>

    ```PowerShell
    $vhdUri = '<Specify hello VHD URI here>'
    ```

1.  <span data-ttu-id="c8f26-114">Создание образа с помощью hello hello **New AzureRmResourceGroupDeployment** командлета.</span><span class="sxs-lookup"><span data-stu-id="c8f26-114">Create hello custom image using hello **New-AzureRmResourceGroupDeployment** cmdlet.</span></span> <span data-ttu-id="c8f26-115">Замените следующие местозаполнители для hello hello **$customImageName** и **$customImageDescription** toomeaningful имена переменных среды.</span><span class="sxs-lookup"><span data-stu-id="c8f26-115">Replace hello following placeholders for hello **$customImageName** and **$customImageDescription** variables toomeaningful names for your environment.</span></span>

    ```PowerShell
    $customImageName = '<Specify hello custom image name>'
    $customImageDescription = '<Specify hello custom image description>'

    $parameters = @{existingLabName="$($lab.Name)"; existingVhdUri=$vhdUri; imageOsType='windows'; isVhdSysPrepped=$false; imageName=$customImageName; imageDescription=$customImageDescription}

    New-AzureRmResourceGroupDeployment -ResourceGroupName $lab.ResourceGroupName -Name CreateCustomImage -TemplateUri 'https://raw.githubusercontent.com/Azure/azure-devtestlab/master/Samples/201-dtl-create-customimage-from-vhd/azuredeploy.json' -TemplateParameterObject $parameters
    ```

## <a name="powershell-script-toocreate-a-custom-image-from-a-vhd-file"></a><span data-ttu-id="c8f26-116">Сценарий PowerShell toocreate пользовательского образа из VHD-файла</span><span class="sxs-lookup"><span data-stu-id="c8f26-116">PowerShell script toocreate a custom image from a VHD file</span></span>

<span data-ttu-id="c8f26-117">Hello следующий сценарий PowerShell можно использовать toocreate пользовательского образа из VHD-файл.</span><span class="sxs-lookup"><span data-stu-id="c8f26-117">hello following PowerShell script can be used toocreate a custom image from a VHD file.</span></span> <span data-ttu-id="c8f26-118">Замените заполнители hello (начиная и заканчивая угловые скобки) с соответствующими значениями hello вашим потребностям.</span><span class="sxs-lookup"><span data-stu-id="c8f26-118">Replace hello placeholders (starting and ending with angle brackets) with hello appropriate values for your needs.</span></span> 

```PowerShell
# Log in tooyour Azure account.  
Login-AzureRmAccount

# Select hello desired Azure subscription. 
$subscriptionId = '<Specify your subscription ID here>'
Select-AzureRmSubscription -SubscriptionId $subscriptionId

# Get hello lab object.
$labRg = '<Specify your lab resource group name here>'
$labName = '<Specify your lab name here>'
$lab = Get-AzureRmResource -ResourceId ('/subscriptions/' + $subscriptionId + '/resourceGroups/' + $labRg + '/providers/Microsoft.DevTestLab/labs/' + $labName)

# Get hello lab storage account and lab storage account key values.
$labStorageAccount = Get-AzureRmResource -ResourceId $lab.Properties.defaultStorageAccount 
$labStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $labStorageAccount.ResourceGroupName -Name $labStorageAccount.ResourceName)[0].Value

# Set hello URI of hello VHD file.  
$vhdUri = '<Specify hello VHD URI here>'

# Set hello custom image name and description values.
$customImageName = '<Specify hello custom image name>'
$customImageDescription = '<Specify hello custom image description>'

# Set up hello parameters object.
$parameters = @{existingLabName="$($lab.Name)"; existingVhdUri=$vhdUri; imageOsType='windows'; isVhdSysPrepped=$false; imageName=$customImageName; imageDescription=$customImageDescription}

# Create hello custom image. 
New-AzureRmResourceGroupDeployment -ResourceGroupName $lab.ResourceGroupName -Name CreateCustomImage -TemplateUri 'https://raw.githubusercontent.com/Azure/azure-devtestlab/master/Samples/201-dtl-create-customimage-from-vhd/azuredeploy.json' -TemplateParameterObject $parameters
```

## <a name="related-blog-posts"></a><span data-ttu-id="c8f26-119">Связанные записи в блогах</span><span class="sxs-lookup"><span data-stu-id="c8f26-119">Related blog posts</span></span>

- [<span data-ttu-id="c8f26-120">Custom images or formulas? (Пользовательские изображения или формулы?)</span><span class="sxs-lookup"><span data-stu-id="c8f26-120">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="c8f26-121">Copying Custom Images between Azure DevTest Labs (Копирование пользовательских образов между лабораториями для разработки и тестирования Azure)</span><span class="sxs-lookup"><span data-stu-id="c8f26-121">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="c8f26-122">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c8f26-122">Next steps</span></span>

- [<span data-ttu-id="c8f26-123">Добавление виртуальных Машин лаборатории tooyour</span><span class="sxs-lookup"><span data-stu-id="c8f26-123">Add a VM tooyour lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
