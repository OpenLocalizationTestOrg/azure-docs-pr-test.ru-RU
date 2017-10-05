---
title: "Проверка конфигурации учетной записи службы автоматизации Azure | Документация Майкрософт"
description: "В этой статье описывается проверка правильной настройки конфигурации учетной записи службы автоматизации."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: magoedte
ms.openlocfilehash: 804e05f596e1d6d5f650e4c94a18eff6b7c3ba4e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="test-azure-automation-run-as-account-authentication"></a><span data-ttu-id="92650-103">Тестирование проверки подлинности учетной записи запуска от имени службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="92650-103">Test Azure Automation Run As account authentication</span></span>
<span data-ttu-id="92650-104">После успешного создания учетной записи службы автоматизации можно выполнить простой тест, чтобы убедиться, что вы сможете успешно пройти проверку подлинности в Azure Resource Manager или в классическом развертывании Azure с помощью созданной или обновленной учетной записи запуска от имени службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="92650-104">After an Automation account is successfully created, you can perform a simple test to confirm you are able to successfully authenticate in Azure Resource Manager or Azure classic deployment using your newly created or updated Automation Run As account.</span></span>    

## <a name="automation-run-as-authentication"></a><span data-ttu-id="92650-105">Проверка подлинности учетной записи запуска от имени службы автоматизации</span><span class="sxs-lookup"><span data-stu-id="92650-105">Automation Run As authentication</span></span>
<span data-ttu-id="92650-106">Используйте пример кода ниже для [создания Runbook PowerShell](automation-creating-importing-runbook.md), чтобы выполнить проверку подлинности с помощью учетной записи запуска от имени. Используйте этот код и в пользовательских модулях Runbook, чтобы выполнить проверку подлинности ресурсов в диспетчере ресурсов и управлять ими с помощью учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="92650-106">Use the sample code below to [create a PowerShell runbook](automation-creating-importing-runbook.md) to verify authentication using the Run As account and also in your custom runbooks to authenticate and manage Resource Manager resources with your Automation account.</span></span>   

    $connectionName = "AzureRunAsConnection"
    try
    {
        # Get the connection "AzureRunAsConnection "
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

        "Logging in to Azure..."
        Add-AzureRmAccount `
           -ServicePrincipal `
           -TenantId $servicePrincipalConnection.TenantId `
           -ApplicationId $servicePrincipalConnection.ApplicationId `
           -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint 
    }
    catch {
       if (!$servicePrincipalConnection)
       {
          $ErrorMessage = "Connection $connectionName not found."
          throw $ErrorMessage
      } else{
          Write-Error -Message $_.Exception
          throw $_.Exception
      }
    }

    #Get all ARM resources from all resource groups
    $ResourceGroups = Get-AzureRmResourceGroup 

    foreach ($ResourceGroup in $ResourceGroups)
    {    
       Write-Output ("Showing resources in resource group " + $ResourceGroup.ResourceGroupName)
       $Resources = Find-AzureRmResource -ResourceGroupNameContains $ResourceGroup.ResourceGroupName | Select ResourceName, ResourceType
       ForEach ($Resource in $Resources)
       {
          Write-Output ($Resource.ResourceName + " of type " +  $Resource.ResourceType)
       }
       Write-Output ("")
    } 

<span data-ttu-id="92650-107">Обратите внимание, что командлет **Add-AzureRmAccount**, применяемый для проверки подлинности в модуле Runbook, использует набор параметров *ServicePrincipalCertificate* .</span><span class="sxs-lookup"><span data-stu-id="92650-107">Notice the cmdlet used for authenticating in the runbook - **Add-AzureRmAccount**, uses the *ServicePrincipalCertificate* parameter set.</span></span>  <span data-ttu-id="92650-108">Он выполняет проверку подлинности с помощью сертификата субъекта-службы, а не учетных данных.</span><span class="sxs-lookup"><span data-stu-id="92650-108">It authenticates by using service principal certificate, not credentials.</span></span>  

<span data-ttu-id="92650-109">При [запуске модуля Runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) для проверки подлинности учетной записи запуска от имени будет создано [задание Runbook](automation-runbook-execution.md), откроется колонка "Задание", а состояние задания будет отображаться на плитке **Сводка по заданию**.</span><span class="sxs-lookup"><span data-stu-id="92650-109">When you [run the runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) to validate your Run As account, a [runbook job](automation-runbook-execution.md) is created, the Job blade is displayed, and the job status displayed in the **Job Summary** tile.</span></span> <span data-ttu-id="92650-110">Сначала задание получает состояние *В очереди* , указывающее на то, что задание ожидает, пока рабочая роль Runbook в облаке станет доступной.</span><span class="sxs-lookup"><span data-stu-id="92650-110">The job status will start as *Queued* indicating that it is waiting for a runbook worker in the cloud to become available.</span></span> <span data-ttu-id="92650-111">Как только рабочая роль затребует задание, оно получит состояние *Запущено*, а с началом фактического выполнения модуля Runbook — состояние *Выполняется*.</span><span class="sxs-lookup"><span data-stu-id="92650-111">It will then move to *Starting* when a worker claims the job, and then *Running* when the runbook actually starts running.</span></span>  <span data-ttu-id="92650-112">После выполнения задания Runbook должно отобразиться состояние **Выполнено**.</span><span class="sxs-lookup"><span data-stu-id="92650-112">When the runbook job completes, we should see a status of **Completed**.</span></span>

<span data-ttu-id="92650-113">Чтобы просмотреть подробные результаты задания Runbook, щелкните плитку **Выходные данные** .</span><span class="sxs-lookup"><span data-stu-id="92650-113">To see the detailed results of the runbook, click on the **Output** tile.</span></span>  <span data-ttu-id="92650-114">В колонке **Выходные данные** должна быть информация о том, что модуль прошел проверку подлинности и вернул список всех ресурсов во всех группах ресурсов подписки.</span><span class="sxs-lookup"><span data-stu-id="92650-114">On the **Output** blade, you should see it has successfully authenticated and returns a list of all resources in all resource groups in your subscription.</span></span>  

<span data-ttu-id="92650-115">Не забудьте удалить блок кода, начиная с комментария `#Get all ARM resources from all resource groups`, при его повторном использовании для модулей Runbook.</span><span class="sxs-lookup"><span data-stu-id="92650-115">Just remember to remove the block of code starting with the comment `#Get all ARM resources from all resource groups` when you reuse the code for your runbooks.</span></span>

## <a name="classic-run-as-authentication"></a><span data-ttu-id="92650-116">Проверка подлинности классической учетной записи запуска от имени</span><span class="sxs-lookup"><span data-stu-id="92650-116">Classic Run As authentication</span></span>
<span data-ttu-id="92650-117">Используйте пример кода ниже для [создания Runbook PowerShell](automation-creating-importing-runbook.md), чтобы выполнить проверку подлинности с помощью классической учетной записи запуска от имени. Используйте этот код и в пользовательских модулях Runbook, чтобы выполнить проверку подлинности ресурсов и управлять ими в классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="92650-117">Use the sample code below to [create a PowerShell runbook](automation-creating-importing-runbook.md) to verify authentication using the Classic Run As account and also in your custom runbooks to authenticate and manage resources in the classic deployment model.</span></span>  

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get the connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate to Azure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in the Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting the certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in the Automation account."
    }

    Write-Verbose "Authenticating to Azure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID
    
    #Get all VMs in the subscription and return list with name of each
    Get-AzureVM | ft Name

<span data-ttu-id="92650-118">При [запуске модуля Runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) для проверки подлинности учетной записи запуска от имени будет создано [задание Runbook](automation-runbook-execution.md), откроется колонка "Задание", а состояние задания будет отображаться на плитке **Сводка по заданию**.</span><span class="sxs-lookup"><span data-stu-id="92650-118">When you [run the runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) to validate your Run As account, a [runbook job](automation-runbook-execution.md) is created, the Job blade is displayed, and the job status displayed in the **Job Summary** tile.</span></span> <span data-ttu-id="92650-119">Сначала задание получает состояние *В очереди* , указывающее на то, что задание ожидает, пока рабочая роль Runbook в облаке станет доступной.</span><span class="sxs-lookup"><span data-stu-id="92650-119">The job status will start as *Queued* indicating that it is waiting for a runbook worker in the cloud to become available.</span></span> <span data-ttu-id="92650-120">Как только рабочая роль затребует задание, оно получит состояние *Запущено*, а с началом фактического выполнения модуля Runbook — состояние *Выполняется*.</span><span class="sxs-lookup"><span data-stu-id="92650-120">It will then move to *Starting* when a worker claims the job, and then *Running* when the runbook actually starts running.</span></span>  <span data-ttu-id="92650-121">После выполнения задания Runbook должно отобразиться состояние **Выполнено**.</span><span class="sxs-lookup"><span data-stu-id="92650-121">When the runbook job completes, we should see a status of **Completed**.</span></span>

<span data-ttu-id="92650-122">Чтобы просмотреть подробные результаты задания Runbook, щелкните плитку **Выходные данные** .</span><span class="sxs-lookup"><span data-stu-id="92650-122">To see the detailed results of the runbook, click on the **Output** tile.</span></span>  <span data-ttu-id="92650-123">В колонке **Выходные данные** должна быть информация о том, что модуль прошел проверку подлинности и вернул список всех виртуальных машин по имени, развернутых в подписке.</span><span class="sxs-lookup"><span data-stu-id="92650-123">On the **Output** blade, you should see it has successfully authenticated and returns a list of all Azure VMs by VMName that are deployed in your subscription.</span></span>  

<span data-ttu-id="92650-124">Не забудьте удалить командлет **Get-AzureVM** при повторном использовании кода для модулей Runbook.</span><span class="sxs-lookup"><span data-stu-id="92650-124">Just remember to remove the cmdlet **Get-AzureVM** when you reuse the code for your runbooks.</span></span>

## <a name="next-steps"></a><span data-ttu-id="92650-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="92650-125">Next steps</span></span>
* <span data-ttu-id="92650-126">Сведения о том, как начать работу с модулями Runbook, см. в статье [Мой первый модуль Runbook PowerShell](automation-first-runbook-textual-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="92650-126">To get started with PowerShell runbooks, see [My first PowerShell runbook](automation-first-runbook-textual-powershell.md).</span></span>
* <span data-ttu-id="92650-127">Дополнительные сведения о графической разработке в службе автоматизации Azure см. в [этой статье](automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="92650-127">To learn more about Graphical Authoring, see [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span></span>
