---
title: "aaaRun Runbook на Azure Automation гибридной рабочей ролью Runbook | Документы Microsoft"
description: "Также приводятся сведения о выполнении модулей Runbook на компьютерах в локальном центре обработки данных или поставщик облака hello гибридной рабочей роли Runbook."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 06227cda-f3d1-47fe-b3f8-436d2b9d81ee
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/22/2017
ms.author: magoedte
ms.openlocfilehash: 51961e02603e5690edd11e577594ad2ddea489a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="running-runbooks-on-a-hybrid-runbook-worker"></a><span data-ttu-id="3600d-103">Запуск модулей runbook в гибридной рабочей роли Runbook</span><span class="sxs-lookup"><span data-stu-id="3600d-103">Running runbooks on a Hybrid Runbook Worker</span></span> 
<span data-ttu-id="3600d-104">Нет никаких различий в структуре hello модулей Runbook, которые запускаются в автоматизации Azure и те, которые работают на гибридную рабочую роль Runbook.</span><span class="sxs-lookup"><span data-stu-id="3600d-104">There is no difference in hello structure of runbooks that run in Azure Automation and those that run on a Hybrid Runbook Worker.</span></span> <span data-ttu-id="3600d-105">Модули Runbook, которые можно использовать с каждым скорее существенно отличаются у менее так как модули Runbook, предназначенных для гибридной рабочей роли Runbook, обычно управлять ресурсами на локальном компьютере hello сам или к ресурсам в локальной среде hello, где он будет развернут, при модулей Runbook в службе автоматизации Azure обычно управлять ресурсами в облаке Azure hello.</span><span class="sxs-lookup"><span data-stu-id="3600d-105">Runbooks that you use with each most likely differ significantly though since runbooks targeting a Hybrid Runbook Worker typically manage resources on hello local computer itself or against resources in hello local environment where it is deployed, while runbooks in Azure Automation typically manage resources in hello Azure cloud.</span></span>

<span data-ttu-id="3600d-106">Можно редактировать книгу для гибридной рабочей ролью Runbook в автоматизации Azure, но имеется трудности при попытке tootest hello runbook в редакторе hello.</span><span class="sxs-lookup"><span data-stu-id="3600d-106">You can edit a runbook for Hybrid Runbook Worker in Azure Automation, but you may have difficulties if you try tootest hello runbook in hello editor.</span></span>  <span data-ttu-id="3600d-107">модули PowerShell Hello, получающих доступ к локальным ресурсам hello может отсутствовать в среде автоматизации Azure в этом случае, произойдет сбой теста hello.</span><span class="sxs-lookup"><span data-stu-id="3600d-107">hello PowerShell modules that access hello local resources may not be installed in your Azure Automation environment in which case, hello test would fail.</span></span>  <span data-ttu-id="3600d-108">Если установить hello необходимые модули, то hello модуль runbook будет запущен, но он не будет возможности tooaccess локальных ресурсов для выполнения теста.</span><span class="sxs-lookup"><span data-stu-id="3600d-108">If you do install hello required modules, then hello runbook will run, but it will not be able tooaccess local resources for a complete test.</span></span>

## <a name="starting-a-runbook-on-hybrid-runbook-worker"></a><span data-ttu-id="3600d-109">Запуск runbook в гибридной рабочей роли Runbook</span><span class="sxs-lookup"><span data-stu-id="3600d-109">Starting a runbook on Hybrid Runbook Worker</span></span>
<span data-ttu-id="3600d-110">[Запуск модуля Runbook в службе автоматизации Azure](automation-starting-a-runbook.md) описываются различные методы запуска модуля Runbook.</span><span class="sxs-lookup"><span data-stu-id="3600d-110">[Starting a Runbook in Azure Automation](automation-starting-a-runbook.md) describes different methods for starting a runbook.</span></span>  <span data-ttu-id="3600d-111">Добавляет гибридной рабочей ролью Runbook **RunOn** вариант, где можно указать имя группы гибридных рабочих ролей Runbook hello.</span><span class="sxs-lookup"><span data-stu-id="3600d-111">Hybrid Runbook Worker adds a **RunOn** option where you can specify hello name of a Hybrid Runbook Worker Group.</span></span>  <span data-ttu-id="3600d-112">Если группа указана, hello runbook извлекается и выполнялись hello рабочих процессов в этой группе.</span><span class="sxs-lookup"><span data-stu-id="3600d-112">If a group is specified, then hello runbook is retrieved and run by of hello workers in that group.</span></span>  <span data-ttu-id="3600d-113">Если этот параметр не указан, то он будет запущен в службе автоматизации Azure в обычном режиме.</span><span class="sxs-lookup"><span data-stu-id="3600d-113">If this option is not specified, then it is run in Azure Automation as normal.</span></span>

<span data-ttu-id="3600d-114">При запуске модуля runbook в hello портал Azure, вам предоставляется **проведение** параметр, в котором можно выбрать **Azure** или **гибридной рабочей роли**.</span><span class="sxs-lookup"><span data-stu-id="3600d-114">When you start a runbook in hello Azure portal, you are presented with a **Run on** option where you can select **Azure** or **Hybrid Worker**.</span></span>  <span data-ttu-id="3600d-115">При выборе **гибридной рабочей роли**, а затем из раскрывающегося списка можно выбрать группу hello.</span><span class="sxs-lookup"><span data-stu-id="3600d-115">If you select **Hybrid Worker**, then you can select hello group from a dropdown.</span></span>

<span data-ttu-id="3600d-116">Используйте hello **RunOn** параметра.</span><span class="sxs-lookup"><span data-stu-id="3600d-116">Use hello **RunOn** parameter.</span></span>  <span data-ttu-id="3600d-117">Можно использовать hello, следующая команда toostart runbook с именем Test-Runbook в Runbook группу гибридных рабочих ролей с именем MyHybridGroup, с помощью Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3600d-117">You can use hello following command toostart a runbook named Test-Runbook on a Hybrid Runbook Worker Group named MyHybridGroup using Windows PowerShell.</span></span>

    Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -RunOn "MyHybridGroup"

> [!NOTE]
> <span data-ttu-id="3600d-118">Hello **RunOn** toohello был добавлен параметр **Start-AzureAutomationRunbook** командлет в версии 0.9.1 Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3600d-118">hello **RunOn** parameter was added toohello **Start-AzureAutomationRunbook** cmdlet in version 0.9.1 of Microsoft Azure PowerShell.</span></span>  <span data-ttu-id="3600d-119">Вы должны [Загрузка последней версии hello](https://azure.microsoft.com/downloads/) при наличии более ранних один из уже установлен.</span><span class="sxs-lookup"><span data-stu-id="3600d-119">You should [download hello latest version](https://azure.microsoft.com/downloads/) if you have an earlier one installed.</span></span>  <span data-ttu-id="3600d-120">Требуется только tooinstall эту версию на рабочей станции, где hello runbook начиная с Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3600d-120">You only need tooinstall this version on a workstation where you are starting hello runbook from Windows PowerShell.</span></span>  <span data-ttu-id="3600d-121">Нет необходимости tooinstall его на компьютере рабочей hello кроме случая, когда toostart модулей Runbook с этого компьютера.</span><span class="sxs-lookup"><span data-stu-id="3600d-121">You do not need tooinstall it on hello worker computer unless you intend toostart runbooks from that computer.</span></span>  <span data-ttu-id="3600d-122">Невозможно запустить в настоящее время книгу в гибридной рабочей роли Runbook из другого модуля runbook, так как это потребует hello последнюю версию Azure Powershell toobe установлен в вашей учетной записи автоматизации.</span><span class="sxs-lookup"><span data-stu-id="3600d-122">You cannot currently start a runbook on a Hybrid Runbook Worker from another runbook since this would require hello latest version of Azure Powershell toobe installed in your Automation account.</span></span>  <span data-ttu-id="3600d-123">последнюю версию Hello автоматически обновляется в службе автоматизации Azure и автоматически сместить вниз работников toohello скоро.</span><span class="sxs-lookup"><span data-stu-id="3600d-123">hello latest version is automatically updated in Azure Automation and automatically pushed down toohello workers soon.</span></span>
>
>

## <a name="runbook-permissions"></a><span data-ttu-id="3600d-124">Разрешения для модулей Runbook</span><span class="sxs-lookup"><span data-stu-id="3600d-124">Runbook permissions</span></span>
<span data-ttu-id="3600d-125">Модулей Runbook, запущенных на гибридную рабочую роль Runbook нельзя использовать hello же метод, который обычно используется для проверки подлинности tooAzure ресурсы, так как они получают доступ к ресурсам за пределами Azure модулей Runbook.</span><span class="sxs-lookup"><span data-stu-id="3600d-125">Runbooks running on a Hybrid Runbook Worker cannot use hello same method that is typically used for runbooks authenticating tooAzure resources, since they are accessing resources outside of Azure.</span></span>  <span data-ttu-id="3600d-126">Hello runbook можно предоставить собственную проверку подлинности toolocal ресурсы или можно указать tooprovide учетная запись запуска от имени для всех модулей Runbook контекст пользователя.</span><span class="sxs-lookup"><span data-stu-id="3600d-126">hello runbook can either provide its own authentication toolocal resources, or you can specify a RunAs account tooprovide a user context for all runbooks.</span></span>

### <a name="runbook-authentication"></a><span data-ttu-id="3600d-127">Проверка подлинности модуля Runbook</span><span class="sxs-lookup"><span data-stu-id="3600d-127">Runbook authentication</span></span>
<span data-ttu-id="3600d-128">По умолчанию модулей Runbook будет выполняться в контексте hello hello локальной системной учетной записи локального компьютера hello, поэтому они должны предоставить свои собственные tooresources проверки подлинности, который получит доступ к.</span><span class="sxs-lookup"><span data-stu-id="3600d-128">By default, runbooks will run in hello context of hello local System account on hello on-premises computer, so they must provide their own authentication tooresources that they will access.</span></span>  

<span data-ttu-id="3600d-129">Можно использовать [учетные данные](http://msdn.microsoft.com/library/dn940015.aspx) и [сертификат](http://msdn.microsoft.com/library/dn940013.aspx) активы в модуле runbook с помощью командлетов, позволяющих toospecify учетные данные, вы можете проверять подлинность toodifferent ресурсов.</span><span class="sxs-lookup"><span data-stu-id="3600d-129">You can use [Credential](http://msdn.microsoft.com/library/dn940015.aspx) and [Certificate](http://msdn.microsoft.com/library/dn940013.aspx) assets in your runbook with cmdlets that allow you toospecify credentials so you can authenticate toodifferent resources.</span></span>  <span data-ttu-id="3600d-130">Hello следующем примере показан фрагмент runbook, который перезапускает компьютер.</span><span class="sxs-lookup"><span data-stu-id="3600d-130">hello following example shows a portion of a runbook that restarts a computer.</span></span>  <span data-ttu-id="3600d-131">Он получает имя актива и hello учетных данных компьютера hello из переменной активов учетные данные и затем использует эти значения с помощью командлета Restart-Computer hello.</span><span class="sxs-lookup"><span data-stu-id="3600d-131">It retrieves credentials from a credential asset and hello name of hello computer from a variable asset and then uses these values with hello Restart-Computer cmdlet.</span></span>

    $Cred = Get-AzureRmAutomationCredential -ResourceGroupName "ResourceGroup01" -Name "MyCredential"
    $Computer = Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" -Name  "ComputerName"

    Restart-Computer -ComputerName $Computer -Credential $Cred

<span data-ttu-id="3600d-132">Можно также использовать [InlineScript](automation-powershell-workflow.md#inlinescript), что позволяет toorun блоки кода на другом компьютере с учетными данными, указанными с hello [общий параметр PSCredential](http://technet.microsoft.com/library/jj129719.aspx).</span><span class="sxs-lookup"><span data-stu-id="3600d-132">You can also leverage [InlineScript](automation-powershell-workflow.md#inlinescript), which  allows you toorun blocks of code on another computer with credentials specified by hello [PSCredential common parameter](http://technet.microsoft.com/library/jj129719.aspx).</span></span>

### <a name="runas-account"></a><span data-ttu-id="3600d-133">Учетная запись запуска от имени</span><span class="sxs-lookup"><span data-stu-id="3600d-133">RunAs account</span></span>
<span data-ttu-id="3600d-134">Вместо предоставления своей собственной проверки подлинности ресурсов toolocal модулей Runbook, можно указать **RunAs** учетной записи для группы гибридных рабочих ролей.</span><span class="sxs-lookup"><span data-stu-id="3600d-134">Instead of having runbooks provide their own authentication toolocal resources, you can specify a **RunAs** account for a Hybrid worker group.</span></span>  <span data-ttu-id="3600d-135">Указать [актива учетных данных](automation-credentials.md) с toolocal доступ к ресурсам, и все модули Runbook запускались эти учетные данные при работе в гибридной рабочей роли Runbook в группе hello.</span><span class="sxs-lookup"><span data-stu-id="3600d-135">You specify a [credential asset](automation-credentials.md) that has access toolocal resources, and all runbooks run under these credentials when running on a Hybrid Runbook Worker in hello group.</span></span>  

<span data-ttu-id="3600d-136">имя пользователя Hello для hello учетных данных должен быть в одном из следующих форматов hello:</span><span class="sxs-lookup"><span data-stu-id="3600d-136">hello user name for hello credential must be in one of hello following formats:</span></span>

* <span data-ttu-id="3600d-137">домен\имя пользователя;</span><span class="sxs-lookup"><span data-stu-id="3600d-137">domain\username</span></span>
* username@domain
* <span data-ttu-id="3600d-138">имя пользователя (для учетных записей локального toohello на локальном компьютере)</span><span class="sxs-lookup"><span data-stu-id="3600d-138">username (for accounts local toohello on-premises computer)</span></span>

<span data-ttu-id="3600d-139">Используйте следующие процедуры toospecify учетную запись запуска от имени для группы гибридных рабочих ролей hello.</span><span class="sxs-lookup"><span data-stu-id="3600d-139">Use hello following procedure toospecify a RunAs account for a Hybrid worker group:</span></span>

1. <span data-ttu-id="3600d-140">Создание [актива учетных данных](automation-credentials.md) с toolocal доступ к ресурсам.</span><span class="sxs-lookup"><span data-stu-id="3600d-140">Create a [credential asset](automation-credentials.md) with access toolocal resources.</span></span>
2. <span data-ttu-id="3600d-141">Откройте учетную запись автоматизации hello в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="3600d-141">Open hello Automation account in hello Azure portal.</span></span>
3. <span data-ttu-id="3600d-142">Выберите hello **гибридных рабочих групп** плитку, а затем выберите группу hello.</span><span class="sxs-lookup"><span data-stu-id="3600d-142">Select hello **Hybrid Worker Groups** tile, and then select hello group.</span></span>
4. <span data-ttu-id="3600d-143">Щелкните **Все параметры**, а затем — **Настройки группы гибридных рабочих ролей**.</span><span class="sxs-lookup"><span data-stu-id="3600d-143">Select **All settings** and then **Hybrid worker group settings**.</span></span>
5. <span data-ttu-id="3600d-144">Изменение **запуска от имени** из **по умолчанию** слишком**настраиваемый**.</span><span class="sxs-lookup"><span data-stu-id="3600d-144">Change **Run As** from **Default** too**Custom**.</span></span>
6. <span data-ttu-id="3600d-145">Выберите учетные данные hello и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="3600d-145">Select hello credential and click **Save**.</span></span>

### <a name="automation-run-as-account"></a><span data-ttu-id="3600d-146">Учетная запись запуска от имени службы автоматизации</span><span class="sxs-lookup"><span data-stu-id="3600d-146">Automation Run As account</span></span>
<span data-ttu-id="3600d-147">В рамках процесса автоматизированной сборки для развертывания ресурсов в Azure может потребоваться доступ tooon локальных систем toosupport одну или несколько шагов в последовательности развертывания.</span><span class="sxs-lookup"><span data-stu-id="3600d-147">As part of your automated build process for deploying resources in Azure, you may require access tooon-premise systems toosupport a task or set of steps in your deployment sequence.</span></span>  <span data-ttu-id="3600d-148">toosupport проверки подлинности с помощью hello запуска от имени учетной записи Azure, вам понадобится tooinstall hello запуска от имени учетной записи сертификат.</span><span class="sxs-lookup"><span data-stu-id="3600d-148">toosupport authentication against Azure using hello Run As account, you need tooinstall hello Run As account certificate.</span></span>  

<span data-ttu-id="3600d-149">Здравствуйте, следуя PowerShell runbook *RunAsCertificateToHybridWorker экспорта*, экспортирует hello запуска от имени сертификата из учетной записи службы автоматизации Azure и загрузку и импортирует его в хранилище сертификатов локального компьютера hello на Гибридная рабочая роль подключен toohello учетную запись.</span><span class="sxs-lookup"><span data-stu-id="3600d-149">hello following PowerShell runbook, *Export-RunAsCertificateToHybridWorker*, exports hello Run As certificate from your Azure Automation account and downloads and imports it into hello local machine certificate store on a Hybrid worker connected toohello same account.</span></span>  <span data-ttu-id="3600d-150">После завершения этого шага, он проверяет, что работника hello прошедшего проверку подлинности tooAzure с помощью hello запуска от имени учетной записи.</span><span class="sxs-lookup"><span data-stu-id="3600d-150">Once that step is completed, it verifies hello worker can successfully authenticate tooAzure using hello Run As account.</span></span>

    <#PSScriptInfo
    .VERSION 1.0
    .GUID 3a796b9a-623d-499d-86c8-c249f10a6986
    .AUTHOR Azure Automation Team
    .COMPANYNAME Microsoft
    .COPYRIGHT 
    .TAGS Azure Automation 
    .LICENSEURI 
    .PROJECTURI 
    .ICONURI 
    .EXTERNALMODULEDEPENDENCIES 
    .REQUIREDSCRIPTS 
    .EXTERNALSCRIPTDEPENDENCIES 
    .RELEASENOTES
    #>

    <#  
    .SYNOPSIS  
    Exports hello Run As certificate from an Azure Automation account tooa hybrid worker in that account. 
  
    .DESCRIPTION  
    This runbook exports hello Run As certificate from an Azure Automation account tooa hybrid worker in that account.
    Run this runbook in hello hybrid worker where you want hello certificate installed.
    This allows hello use of hello AzureRunAsConnection tooauthenticate tooAzure and manage Azure resources from runbooks running in hello hybrid worker.

    .EXAMPLE
    .\Export-RunAsCertificateToHybridWorker

    .NOTES
    AUTHOR: Azure Automation Team 
    LASTEDIT: 2016.10.13
    #>

    [OutputType([string])] 

    # Set hello password used for this certificate
    $Password = "YourStrongPasswordForTheCert"

    # Stop on errors
    $ErrorActionPreference = 'stop'

    # Get hello management certificate that will be used toomake calls into Azure Service Management resources
    $RunAsCert = Get-AutomationCertificate -Name "AzureRunAsCertificate"
       
    # location toostore temporary certificate in hello Automation service host
    $CertPath = Join-Path $env:temp  "AzureRunAsCertificate.pfx"
   
    # Save hello certificate
    $Cert = $RunAsCert.Export("pfx",$Password)
    Set-Content -Value $Cert -Path $CertPath -Force -Encoding Byte | Write-Verbose 

    Write-Output ("Importing certificate into $env:computername local machine root store from " + $CertPath)
    $SecurePassword = ConvertTo-SecureString $Password -AsPlainText -Force
    Import-PfxCertificate -FilePath $CertPath -CertStoreLocation Cert:\LocalMachine\My -Password $SecurePassword -Exportable | Write-Verbose

    # Test that authentication tooAzure Resource Manager is working
    $RunAsConnection = Get-AutomationConnection -Name "AzureRunAsConnection" 
    
    Add-AzureRmAccount `
      -ServicePrincipal `
      -TenantId $RunAsConnection.TenantId `
      -ApplicationId $RunAsConnection.ApplicationId `
      -CertificateThumbprint $RunAsConnection.CertificateThumbprint | Write-Verbose

    Set-AzureRmContext -SubscriptionId $RunAsConnection.SubscriptionID | Write-Verbose

    # List automation accounts tooconfirm Azure Resource Manager calls are working
    Get-AzureRmAutomationAccount | Select AutomationAccountName

<span data-ttu-id="3600d-151">Сохранить hello *экспорта RunAsCertificateToHybridWorker* runbook tooyour компьютер с `.ps1` расширения.</span><span class="sxs-lookup"><span data-stu-id="3600d-151">Save hello *Export-RunAsCertificateToHybridWorker* runbook tooyour computer with a `.ps1` extension.</span></span>  <span data-ttu-id="3600d-152">Импортировать его в учетную запись автоматизации и изменить модуль runbook hello, изменив значение переменной hello hello `$Password` с собственный пароль.</span><span class="sxs-lookup"><span data-stu-id="3600d-152">Import it into your Automation account and edit hello runbook, changing hello value of hello variable `$Password` with your own password.</span></span>  <span data-ttu-id="3600d-153">Публикации, а затем запустите runbook hello, предназначенных для hello группу гибридных рабочих ролей, запуска и проверки подлинности модулей Runbook с помощью hello запуска от имени учетной записи.</span><span class="sxs-lookup"><span data-stu-id="3600d-153">Publish and then run hello runbook targeting hello Hybrid Worker group that run and authenticate runbooks using hello Run As account.</span></span>  <span data-ttu-id="3600d-154">Hello задания поток отчеты hello попытки tooimport hello сертификат в хранилище локального компьютера hello и следующим с несколькими строками в зависимости от определенных сколько учетных записей автоматизации в подписке, и если проверка выполнена успешно.</span><span class="sxs-lookup"><span data-stu-id="3600d-154">hello job stream reports hello attempt tooimport hello certificate into hello local machine store, and follows with multiple lines depending on how many Automation accounts are defined in your subscription and if authentication is successful.</span></span>  

## <a name="troubleshooting-runbooks-on-hybrid-runbook-worker"></a><span data-ttu-id="3600d-155">Устранение неполадок с модулями Runbook в гибридном компоненте Runbook Worker</span><span class="sxs-lookup"><span data-stu-id="3600d-155">Troubleshooting runbooks on Hybrid Runbook Worker</span></span>
<span data-ttu-id="3600d-156">Журналы сохраняются локально в каждом гибридном компоненте Worker по адресу C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes.</span><span class="sxs-lookup"><span data-stu-id="3600d-156">Logs are stored locally on each hybrid worker at C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes.</span></span>  <span data-ttu-id="3600d-157">Гибридная рабочая роль также записывает ошибки и события в журнале событий Windows hello под **приложения и службы Logs\Microsoft-SMA\Operational**.</span><span class="sxs-lookup"><span data-stu-id="3600d-157">Hybrid worker also records errors and events in hello Windows event log under **Application and Services Logs\Microsoft-SMA\Operational**.</span></span>  <span data-ttu-id="3600d-158">События, связанные toorunbooks выполнения в рабочем процессе hello записываются слишком**приложения и службы Logs\Microsoft-Automation\Operational**.</span><span class="sxs-lookup"><span data-stu-id="3600d-158">Events related toorunbooks executed on hello worker are written too**Application and Services Logs\Microsoft-Automation\Operational**.</span></span>  <span data-ttu-id="3600d-159">Hello **Microsoft SMA** журнала включает в себя множество дополнительные события связанные toohello runbook задания занесенный в стек toohello рабочей роли и hello обработку hello модуля Runbook.</span><span class="sxs-lookup"><span data-stu-id="3600d-159">hello **Microsoft-SMA** log includes many more events related toohello runbook job pushed toohello worker and hello processing of hello runbook.</span></span>  <span data-ttu-id="3600d-160">При hello **автоматизации Microsoft** журнала событий не имеет большое количество событий с подробными сведениями, помощь в устранении неполадок hello выполнения runbook, по крайней мере, вы найдете hello результатов задания runbook hello.</span><span class="sxs-lookup"><span data-stu-id="3600d-160">While hello **Microsoft-Automation** event log does not have many events with details assisting with hello troubleshooting of runbook execution, you will at least find hello results of hello runbook job.</span></span>  

<span data-ttu-id="3600d-161">[Runbook, выходные и сообщений](automation-runbook-output-and-messages.md) отправляются tooAzure автоматизации из гибридные рабочие роли точно так же, как и задания runbook выполняются в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="3600d-161">[Runbook output and messages](automation-runbook-output-and-messages.md) are sent tooAzure Automation from hybrid workers just like runbook jobs run in hello cloud.</span></span>  <span data-ttu-id="3600d-162">Можно также включить hello Verbose и hello потоков выполняется таким же способом, что и для других модулей Runbook.</span><span class="sxs-lookup"><span data-stu-id="3600d-162">You can also enable hello Verbose and Progress streams hello same way you would for other runbooks.</span></span>  

<span data-ttu-id="3600d-163">Если модули Runbook не завершаются успешно, и состояние задания hello сводки **Suspended**, см. в статье hello статьи об устранении неполадок [гибридной рабочей роли Runbook: задание runbook завершается с состоянием Приостановить](automation-troubleshooting-hybrid-runbook-worker.md#a-runbook-job-terminates-with-a-status-of-suspended).</span><span class="sxs-lookup"><span data-stu-id="3600d-163">If your runbooks are not completing successfully and hello job summary shows a status of **Suspended**, please review hello troubleshooting article [Hybrid Runbook Worker: A runbook job terminates with a status of Suspended](automation-troubleshooting-hybrid-runbook-worker.md#a-runbook-job-terminates-with-a-status-of-suspended).</span></span>   

## <a name="next-steps"></a><span data-ttu-id="3600d-164">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3600d-164">Next steps</span></span>
* <span data-ttu-id="3600d-165">toolearn Дополнительные сведения о hello различные методы, которые можно использовать toostart runbook, в разделе [запуск Runbook в автоматизации Azure](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="3600d-165">toolearn more about hello different methods that can be used toostart a runbook, see [Starting a Runbook in Azure Automation](automation-starting-a-runbook.md).</span></span>  
* <span data-ttu-id="3600d-166">. в разделе toounderstand hello разные процедуры для работы с PowerShell и рабочий процесс PowerShell модули Runbook в автоматизации Azure с помощью текстового редактора hello, [редактирование Runbook в автоматизации Azure](automation-edit-textual-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="3600d-166">toounderstand hello different procedures for working with PowerShell and PowerShell Workflow runbooks in Azure Automation using hello textual editor, see [Editing a Runbook in Azure Automation](automation-edit-textual-runbook.md)</span></span>
