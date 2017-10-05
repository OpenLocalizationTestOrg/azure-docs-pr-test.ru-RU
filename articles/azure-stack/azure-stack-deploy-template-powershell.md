---
title: "Развертывание шаблонов с помощью PowerShell в стек Azure | Документы Microsoft"
description: "Дополнительные сведения о развертывании виртуальной машины с помощью шаблона диспетчера ресурсов и PowerShell."
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
ms.openlocfilehash: 1f443898bcb9b422fc2db46f4e389ae51b043d87
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-templates-in-azure-stack-using-powershell"></a><span data-ttu-id="38cd0-103">Развертывание шаблонов в Azure Stack с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="38cd0-103">Deploy templates in Azure Stack using PowerShell</span></span>
<span data-ttu-id="38cd0-104">Использование PowerShell для развертывания пакета средств разработки Azure стека шаблонов диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="38cd0-104">Use PowerShell to deploy Azure Resource Manager templates to the Azure Stack Development Kit.</span></span>  <span data-ttu-id="38cd0-105">Шаблоны диспетчера ресурсов, развертывание и предоставление все ресурсы для приложения в один, согласованной операции.</span><span class="sxs-lookup"><span data-stu-id="38cd0-105">Resource Manager templates deploy and provision all resources for your application in a single, coordinated operation.</span></span>

## <a name="run-azurerm-powershell-cmdlets"></a><span data-ttu-id="38cd0-106">Выполнение командлетов PowerShell для AzureRM</span><span class="sxs-lookup"><span data-stu-id="38cd0-106">Run AzureRM PowerShell cmdlets</span></span>
<span data-ttu-id="38cd0-107">В этом примере выполнить сценарий для развертывания виртуальной машины в комплекте разработки Azure стека с помощью шаблона диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="38cd0-107">In this example, you run a script to deploy a virtual machine to Azure Stack Development Kit using a Resource Manager template.</span></span>  <span data-ttu-id="38cd0-108">Прежде чем продолжить, убедитесь в наличии [настроить PowerShell](azure-stack-powershell-configure-user.md)</span><span class="sxs-lookup"><span data-stu-id="38cd0-108">Before proceeding, ensure you have [configured PowerShell](azure-stack-powershell-configure-user.md)</span></span>  

<span data-ttu-id="38cd0-109">Виртуальный жесткий ДИСК, используемый в данном примере шаблоне — WindowsServer 2012-R2 Datacenter.</span><span class="sxs-lookup"><span data-stu-id="38cd0-109">The VHD used in this example template is WindowsServer-2012-R2-Datacenter.</span></span>

1. <span data-ttu-id="38cd0-110">Последовательно выберите пункты <http://aka.ms/AzureStackGitHub>, поиск **101-simple-windows-vm** шаблона и сохраните его в следующее расположение: c:\\шаблоны\\ azuredeploy-101-simple-windows-vm.json.</span><span class="sxs-lookup"><span data-stu-id="38cd0-110">Go to <http://aka.ms/AzureStackGitHub>, search for the **101-simple-windows-vm** template, and save it to the following location: c:\\templates\\azuredeploy-101-simple-windows-vm.json.</span></span>
2. <span data-ttu-id="38cd0-111">В PowerShell выполните следующий сценарий развертывания.</span><span class="sxs-lookup"><span data-stu-id="38cd0-111">In PowerShell, run the following deployment script.</span></span> <span data-ttu-id="38cd0-112">Замените *username* и *пароль* имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="38cd0-112">Replace *username* and *password* with your username and password.</span></span> <span data-ttu-id="38cd0-113">При последующем использовании увеличить значение для *$myNum* параметр для предотвращения перезаписи развертывания.</span><span class="sxs-lookup"><span data-stu-id="38cd0-113">On subsequent uses, increment the value for the *$myNum* parameter to prevent overwriting your deployment.</span></span>
   
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
3. <span data-ttu-id="38cd0-114">Открыть портала, нажмите кнопку Azure стека **Обзор**, нажмите кнопку **виртуальные машины**и найдите на новую виртуальную машину (*myDeployment001*).</span><span class="sxs-lookup"><span data-stu-id="38cd0-114">Open the Azure Stack portal, click **Browse**, click **Virtual machines**, and look for your new virtual machine (*myDeployment001*).</span></span>


## <a name="next-steps"></a><span data-ttu-id="38cd0-115">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="38cd0-115">Next steps</span></span>
[<span data-ttu-id="38cd0-116">Развертывание шаблонов с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="38cd0-116">Deploy templates with Visual Studio</span></span>](azure-stack-deploy-template-visual-studio.md)

