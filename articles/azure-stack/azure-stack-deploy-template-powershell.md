---
title: "шаблоны aaaDeploy с помощью PowerShell в стек Azure | Документы Microsoft"
description: "Узнайте, как toodeploy виртуальной машины с помощью шаблона диспетчера ресурсов и PowerShell."
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: 12fe32d7-0a1a-4c02-835d-7b97f151ed0f
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: fb0d4b190e058b3c5c1273b6c91fc3d72dedeb1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-templates-in-azure-stack-using-powershell"></a><span data-ttu-id="a9685-103">Развертывание шаблонов в Azure Stack с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="a9685-103">Deploy templates in Azure Stack using PowerShell</span></span>
<span data-ttu-id="a9685-104">С помощью PowerShell toodeploy диспетчера ресурсов Azure шаблоны toohello пакет средств разработки Azure стека.</span><span class="sxs-lookup"><span data-stu-id="a9685-104">Use PowerShell toodeploy Azure Resource Manager templates toohello Azure Stack Development Kit.</span></span>  <span data-ttu-id="a9685-105">Шаблоны диспетчера ресурсов, развертывание и предоставление все ресурсы для приложения в один, согласованной операции.</span><span class="sxs-lookup"><span data-stu-id="a9685-105">Resource Manager templates deploy and provision all resources for your application in a single, coordinated operation.</span></span>

## <a name="run-azurerm-powershell-cmdlets"></a><span data-ttu-id="a9685-106">Выполнение командлетов PowerShell для AzureRM</span><span class="sxs-lookup"><span data-stu-id="a9685-106">Run AzureRM PowerShell cmdlets</span></span>
<span data-ttu-id="a9685-107">В этом примере выполняется toodeploy сценарий виртуальной машины tooAzure стека пакет средств разработки с помощью шаблона диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a9685-107">In this example, you run a script toodeploy a virtual machine tooAzure Stack Development Kit using a Resource Manager template.</span></span>  <span data-ttu-id="a9685-108">Прежде чем продолжить, убедитесь в наличии [настроить PowerShell](azure-stack-powershell-configure-user.md)</span><span class="sxs-lookup"><span data-stu-id="a9685-108">Before proceeding, ensure you have [configured PowerShell](azure-stack-powershell-configure-user.md)</span></span>  

<span data-ttu-id="a9685-109">Hello VHD, используемые в данном примере шаблоне — WindowsServer 2012-R2 Datacenter.</span><span class="sxs-lookup"><span data-stu-id="a9685-109">hello VHD used in this example template is WindowsServer-2012-R2-Datacenter.</span></span>

1. <span data-ttu-id="a9685-110">Go слишком<http://aka.ms/AzureStackGitHub>, поиск hello **101-simple-windows-vm** шаблона и сохраните его toohello следующие расположения: c:\\шаблоны\\ azuredeploy-101-simple-windows-vm.json.</span><span class="sxs-lookup"><span data-stu-id="a9685-110">Go too<http://aka.ms/AzureStackGitHub>, search for hello **101-simple-windows-vm** template, and save it toohello following location: c:\\templates\\azuredeploy-101-simple-windows-vm.json.</span></span>
2. <span data-ttu-id="a9685-111">В PowerShell запустите следующий скрипт развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="a9685-111">In PowerShell, run hello following deployment script.</span></span> <span data-ttu-id="a9685-112">Замените *username* и *пароль* имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="a9685-112">Replace *username* and *password* with your username and password.</span></span> <span data-ttu-id="a9685-113">При последующем использовании увеличивать значение hello для hello *$myNum* tooprevent параметр перезаписи развертывания.</span><span class="sxs-lookup"><span data-stu-id="a9685-113">On subsequent uses, increment hello value for hello *$myNum* parameter tooprevent overwriting your deployment.</span></span>
   
   ```PowerShell
       # Set Deployment Variables
       $myNum = "001" #Modify this per deployment
       $RGName = "myRG$myNum"
       $myLocation = "local"
   
       # Create Resource Group for Template Deployment
       New-AzureRmResourceGroup -Name $RGName -Location $myLocation
   
       # Deploy Simple IaaS Template
       New-AzureRmResourceGroupDeployment `
           -Name myDeployment$myNum `
           -ResourceGroupName $RGName `
           -TemplateFile c:\templates\azuredeploy-101-simple-windows-vm.json `
           -NewStorageAccountName mystorage$myNum `
           -DnsNameForPublicIP mydns$myNum `
           -AdminUsername <username> `
           -AdminPassword ("<password>" | ConvertTo-SecureString -AsPlainText -Force) `
           -VmName myVM$myNum `
           -WindowsOSVersion 2012-R2-Datacenter
   ```
3. <span data-ttu-id="a9685-114">Откройте hello Azure стека, щелкните **Обзор**, нажмите кнопку **виртуальные машины**и найдите на новую виртуальную машину (*myDeployment001*).</span><span class="sxs-lookup"><span data-stu-id="a9685-114">Open hello Azure Stack portal, click **Browse**, click **Virtual machines**, and look for your new virtual machine (*myDeployment001*).</span></span>


## <a name="next-steps"></a><span data-ttu-id="a9685-115">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a9685-115">Next steps</span></span>
[<span data-ttu-id="a9685-116">Развертывание шаблонов с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a9685-116">Deploy templates with Visual Studio</span></span>](azure-stack-deploy-template-visual-studio.md)

