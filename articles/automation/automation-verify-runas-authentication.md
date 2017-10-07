---
title: "Настройка учетной записи службы автоматизации Azure aaaValidate | Документы Microsoft"
description: "Этой статье описывается, как tooconfirm hello конфигурации учетной записи автоматизации настроена правильно."
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
ms.openlocfilehash: 3a990dcc6661cf67c4b62592ce03d55a3791053a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="test-azure-automation-run-as-account-authentication"></a><span data-ttu-id="270aa-103">Тестирование проверки подлинности учетной записи запуска от имени службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="270aa-103">Test Azure Automation Run As account authentication</span></span>
<span data-ttu-id="270aa-104">После успешного создания учетной записи автоматизации можно выполнять tooconfirm простой тест, можно toosuccessfully проверку подлинности в Azure Resource Manager или развертывания Azure классические вновь созданных или обновленных автоматизации Запуск от имени учетной записи.</span><span class="sxs-lookup"><span data-stu-id="270aa-104">After an Automation account is successfully created, you can perform a simple test tooconfirm you are able toosuccessfully authenticate in Azure Resource Manager or Azure classic deployment using your newly created or updated Automation Run As account.</span></span>    

## <a name="automation-run-as-authentication"></a><span data-ttu-id="270aa-105">Проверка подлинности учетной записи запуска от имени службы автоматизации</span><span class="sxs-lookup"><span data-stu-id="270aa-105">Automation Run As authentication</span></span>
<span data-ttu-id="270aa-106">Используйте hello в образце кода ниже слишком[создать PowerShell runbook](automation-creating-importing-runbook.md) tooverify проверки подлинности с помощью hello запустите от имени учетной записи, так и в вашей настраиваемой документации по задачам tooauthenticate и управление ресурсами диспетчера ресурсов с помощью учетной записи автоматизации.</span><span class="sxs-lookup"><span data-stu-id="270aa-106">Use hello sample code below too[create a PowerShell runbook](automation-creating-importing-runbook.md) tooverify authentication using hello Run As account and also in your custom runbooks tooauthenticate and manage Resource Manager resources with your Automation account.</span></span>   

    $connectionName = "AzureRunAsConnection"
    try
    {
        # Get hello connection "AzureRunAsConnection "
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

        "Logging in tooAzure..."
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

<span data-ttu-id="270aa-107">Обратите внимание, hello командлет, используемый для проверки подлинности в модуле runbook hello - **добавить AzureRmAccount**, использует hello *ServicePrincipalCertificate* набор параметров.</span><span class="sxs-lookup"><span data-stu-id="270aa-107">Notice hello cmdlet used for authenticating in hello runbook - **Add-AzureRmAccount**, uses hello *ServicePrincipalCertificate* parameter set.</span></span>  <span data-ttu-id="270aa-108">Он выполняет проверку подлинности с помощью сертификата субъекта-службы, а не учетных данных.</span><span class="sxs-lookup"><span data-stu-id="270aa-108">It authenticates by using service principal certificate, not credentials.</span></span>  

<span data-ttu-id="270aa-109">При вы [запуска модуля runbook hello](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate учетной записи запуска от имени [задание runbook](automation-runbook-execution.md) — создан, отображается колонке hello задания, а состояние задания hello в hello **Сводка заданий**плитки.</span><span class="sxs-lookup"><span data-stu-id="270aa-109">When you [run hello runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate your Run As account, a [runbook job](automation-runbook-execution.md) is created, hello Job blade is displayed, and hello job status displayed in hello **Job Summary** tile.</span></span> <span data-ttu-id="270aa-110">состояние задания Hello будет запускаться как *в очереди* означает, что он ожидает runbook worker в доступных toobecome облака hello.</span><span class="sxs-lookup"><span data-stu-id="270aa-110">hello job status will start as *Queued* indicating that it is waiting for a runbook worker in hello cloud toobecome available.</span></span> <span data-ttu-id="270aa-111">Он будет двигаться слишком*запуск* когда исполнитель задания hello, а затем *под управлением* при hello runbook фактически начинает выполнение.</span><span class="sxs-lookup"><span data-stu-id="270aa-111">It will then move too*Starting* when a worker claims hello job, and then *Running* when hello runbook actually starts running.</span></span>  <span data-ttu-id="270aa-112">После завершения задания runbook hello, мы должны увидеть состояние **завершено**.</span><span class="sxs-lookup"><span data-stu-id="270aa-112">When hello runbook job completes, we should see a status of **Completed**.</span></span>

<span data-ttu-id="270aa-113">toosee Здравствуйте подробные результаты hello runbook, щелкните hello **вывода** плитки.</span><span class="sxs-lookup"><span data-stu-id="270aa-113">toosee hello detailed results of hello runbook, click on hello **Output** tile.</span></span>  <span data-ttu-id="270aa-114">На hello **вывода** колонку, вы увидите ее успешной проверки подлинности и возвращает список всех ресурсов во всех группах ресурсов в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="270aa-114">On hello **Output** blade, you should see it has successfully authenticated and returns a list of all resources in all resource groups in your subscription.</span></span>  

<span data-ttu-id="270aa-115">Необходимо помнить tooremove hello блок кода, начиная с комментария hello `#Get all ARM resources from all resource groups` при повторном использовании кода hello для Runbook.</span><span class="sxs-lookup"><span data-stu-id="270aa-115">Just remember tooremove hello block of code starting with hello comment `#Get all ARM resources from all resource groups` when you reuse hello code for your runbooks.</span></span>

## <a name="classic-run-as-authentication"></a><span data-ttu-id="270aa-116">Проверка подлинности классической учетной записи запуска от имени</span><span class="sxs-lookup"><span data-stu-id="270aa-116">Classic Run As authentication</span></span>
<span data-ttu-id="270aa-117">Используйте hello в образце кода ниже слишком[создать PowerShell runbook](automation-creating-importing-runbook.md) tooverify проверки подлинности с помощью классической "hello" запустите от имени учетной записи, так и в вашей настраиваемой документации по задачам tooauthenticate ресурсы и управлять ими в hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="270aa-117">Use hello sample code below too[create a PowerShell runbook](automation-creating-importing-runbook.md) tooverify authentication using hello Classic Run As account and also in your custom runbooks tooauthenticate and manage resources in hello classic deployment model.</span></span>  

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get hello connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate tooAzure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in hello Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting hello certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in hello Automation account."
    }

    Write-Verbose "Authenticating tooAzure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID
    
    #Get all VMs in hello subscription and return list with name of each
    Get-AzureVM | ft Name

<span data-ttu-id="270aa-118">При вы [запуска модуля runbook hello](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate учетной записи запуска от имени [задание runbook](automation-runbook-execution.md) — создан, отображается колонке hello задания, а состояние задания hello в hello **Сводка заданий**плитки.</span><span class="sxs-lookup"><span data-stu-id="270aa-118">When you [run hello runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate your Run As account, a [runbook job](automation-runbook-execution.md) is created, hello Job blade is displayed, and hello job status displayed in hello **Job Summary** tile.</span></span> <span data-ttu-id="270aa-119">состояние задания Hello будет запускаться как *в очереди* означает, что он ожидает runbook worker в доступных toobecome облака hello.</span><span class="sxs-lookup"><span data-stu-id="270aa-119">hello job status will start as *Queued* indicating that it is waiting for a runbook worker in hello cloud toobecome available.</span></span> <span data-ttu-id="270aa-120">Он будет двигаться слишком*запуск* когда исполнитель задания hello, а затем *под управлением* при hello runbook фактически начинает выполнение.</span><span class="sxs-lookup"><span data-stu-id="270aa-120">It will then move too*Starting* when a worker claims hello job, and then *Running* when hello runbook actually starts running.</span></span>  <span data-ttu-id="270aa-121">После завершения задания runbook hello, мы должны увидеть состояние **завершено**.</span><span class="sxs-lookup"><span data-stu-id="270aa-121">When hello runbook job completes, we should see a status of **Completed**.</span></span>

<span data-ttu-id="270aa-122">toosee Здравствуйте подробные результаты hello runbook, щелкните hello **вывода** плитки.</span><span class="sxs-lookup"><span data-stu-id="270aa-122">toosee hello detailed results of hello runbook, click on hello **Output** tile.</span></span>  <span data-ttu-id="270aa-123">На hello **вывода** колонку, вы увидите ее успешной проверки подлинности и возвращает список всех виртуальных машин Azure, VMName, развернутых в подписке.</span><span class="sxs-lookup"><span data-stu-id="270aa-123">On hello **Output** blade, you should see it has successfully authenticated and returns a list of all Azure VMs by VMName that are deployed in your subscription.</span></span>  

<span data-ttu-id="270aa-124">Необходимо помнить командлет hello tooremove **Get-AzureVM** при повторном использовании кода hello для Runbook.</span><span class="sxs-lookup"><span data-stu-id="270aa-124">Just remember tooremove hello cmdlet **Get-AzureVM** when you reuse hello code for your runbooks.</span></span>

## <a name="next-steps"></a><span data-ttu-id="270aa-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="270aa-125">Next steps</span></span>
* <span data-ttu-id="270aa-126">tooget к работе с PowerShell модули Runbook в разделе [Мой первый runbook PowerShell](automation-first-runbook-textual-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="270aa-126">tooget started with PowerShell runbooks, see [My first PowerShell runbook](automation-first-runbook-textual-powershell.md).</span></span>
* <span data-ttu-id="270aa-127">toolearn Дополнительные сведения о графических разработки. в разделе [графический разработки в Azure Automation](automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="270aa-127">toolearn more about Graphical Authoring, see [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span></span>
