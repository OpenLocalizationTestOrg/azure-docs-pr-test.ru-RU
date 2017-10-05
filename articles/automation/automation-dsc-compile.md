---
title: "Компиляция конфигураций в Azure Automation DSC | Документация Майкрософт"
description: "В этой статье описывается, как компилировать конфигурации службы настройки требуемого состояния (DSC) для службы автоматизации Azure."
services: automation
documentationcenter: na
author: eslesar
manager: carmonm
ms.assetid: 49f20b31-4fa5-4712-b1c7-8f4409f1aecc
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 02/07/2017
ms.author: magoedte; eslesar
ms.openlocfilehash: 1aadd604e676659475f00760af3b0bdfb13a4792
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="compiling-configurations-in-azure-automation-dsc"></a><span data-ttu-id="030e7-103">Компилирование конфигураций в Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="030e7-103">Compiling configurations in Azure Automation DSC</span></span>

<span data-ttu-id="030e7-104">Вы можете компилировать конфигурации службы настройки требуемого состояния (DSC) двумя способами: на портале Azure или с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="030e7-104">You can compile Desired State Configuration (DSC) configurations in two ways with Azure Automation: in the Azure portal, and with Windows PowerShell.</span></span> <span data-ttu-id="030e7-105">Нижеприведенная таблица поможет определить, когда и какой метод использовать с учетом характеристик каждого метода.</span><span class="sxs-lookup"><span data-stu-id="030e7-105">The following table will help you determine when to use which method based on the characteristics of each:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="030e7-106">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="030e7-106">Azure portal</span></span>

* <span data-ttu-id="030e7-107">Простейший способ с интерактивным пользовательским интерфейсом.</span><span class="sxs-lookup"><span data-stu-id="030e7-107">Simplest method with interactive user interface</span></span>
* <span data-ttu-id="030e7-108">Форма для предоставления значений простых параметров.</span><span class="sxs-lookup"><span data-stu-id="030e7-108">Form to provide simple parameter values</span></span>
* <span data-ttu-id="030e7-109">Легко отслеживаемое состояние задания.</span><span class="sxs-lookup"><span data-stu-id="030e7-109">Easily track job state</span></span>
* <span data-ttu-id="030e7-110">Доступ с проверкой подлинности в Azure.</span><span class="sxs-lookup"><span data-stu-id="030e7-110">Access authenticated with Azure logon</span></span>

### <a name="windows-powershell"></a><span data-ttu-id="030e7-111">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="030e7-111">Windows PowerShell</span></span>

* <span data-ttu-id="030e7-112">Вызов из командной строки с помощью командлетов Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="030e7-112">Call from command line with Windows PowerShell cmdlets</span></span>
* <span data-ttu-id="030e7-113">Может быть добавлено в автоматизированное решение, состоящее из нескольких шагов.</span><span class="sxs-lookup"><span data-stu-id="030e7-113">Can be included in automated solution with multiple steps</span></span>
* <span data-ttu-id="030e7-114">Необходимо предоставить значения простых и сложных параметров.</span><span class="sxs-lookup"><span data-stu-id="030e7-114">Provide simple and complex parameter values</span></span>
* <span data-ttu-id="030e7-115">Отслеживание состояния задания</span><span class="sxs-lookup"><span data-stu-id="030e7-115">Track job state</span></span>
* <span data-ttu-id="030e7-116">Для поддержки командлетов PowerShell необходим клиент.</span><span class="sxs-lookup"><span data-stu-id="030e7-116">Client required to support PowerShell cmdlets</span></span>
* <span data-ttu-id="030e7-117">Передача данных ConfigurationData.</span><span class="sxs-lookup"><span data-stu-id="030e7-117">Pass ConfigurationData</span></span>
* <span data-ttu-id="030e7-118">Компилирование конфигураций, использующих учетные данные.</span><span class="sxs-lookup"><span data-stu-id="030e7-118">Compile configurations that use credentials</span></span>

<span data-ttu-id="030e7-119">После выбора метода компиляции вы можете выполнять процедуры, описанные ниже, чтобы начать компилирование.</span><span class="sxs-lookup"><span data-stu-id="030e7-119">Once you have decided on a compilation method, you can follow the respective procedures below to start compiling.</span></span>

## <a name="compiling-a-dsc-configuration-with-the-azure-portal"></a><span data-ttu-id="030e7-120">Компилирование конфигурации DSC с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="030e7-120">Compiling a DSC Configuration with the Azure portal</span></span>

1. <span data-ttu-id="030e7-121">В учетной записи службы автоматизации щелкните **DSC Configurations** (Конфигурации DSC).</span><span class="sxs-lookup"><span data-stu-id="030e7-121">From your Automation account, click **DSC Configurations**.</span></span>
2. <span data-ttu-id="030e7-122">Щелкните конфигурацию, чтобы открыть ее колонку.</span><span class="sxs-lookup"><span data-stu-id="030e7-122">Click a configuration to open its blade.</span></span>
3. <span data-ttu-id="030e7-123">Нажмите кнопку **Компилировать**.</span><span class="sxs-lookup"><span data-stu-id="030e7-123">Click **Compile**.</span></span>
4. <span data-ttu-id="030e7-124">Если конфигурация не имеет параметров, нужно будет подтвердить ее компилирование.</span><span class="sxs-lookup"><span data-stu-id="030e7-124">If the configuration has no parameters, you will be prompted to confirm whether you want to compile it.</span></span> <span data-ttu-id="030e7-125">Если конфигурация имеет параметры, то отобразится колонка **Compile Configuration** (Компилирование конфигурации), в которой можно указать значения параметров.</span><span class="sxs-lookup"><span data-stu-id="030e7-125">If the configuration has parameters, the **Compile Configuration** blade will open so you can provide parameter values.</span></span> <span data-ttu-id="030e7-126">Дополнительные сведения о параметрах см. в разделе [**Базовые параметры**](#basic-parameters) ниже.</span><span class="sxs-lookup"><span data-stu-id="030e7-126">See the [**Basic Parameters**](#basic-parameters) section below for further details on parameters.</span></span>
5. <span data-ttu-id="030e7-127">Откроется колонка **Задание компилирования** , где вы можете отследить статус задания компилирования, а также конфигурации узла (документы конфигурации MOF), которые это задание расположило на опрашивающем сервере Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="030e7-127">The **Compilation Job** blade is opened so that you can track the compilation job's status, and the node configurations (MOF configuration documents) it caused to be placed on the Azure Automation DSC Pull Server.</span></span>

## <a name="compiling-a-dsc-configuration-with-windows-powershell"></a><span data-ttu-id="030e7-128">Компилирование конфигурации DSC с помощью Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="030e7-128">Compiling a DSC Configuration with Windows PowerShell</span></span>

<span data-ttu-id="030e7-129">Чтобы начать компилирование с помощью Windows PowerShell, вы можете использовать [`Start-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) .</span><span class="sxs-lookup"><span data-stu-id="030e7-129">You can use [`Start-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) to start compiling with Windows PowerShell.</span></span> <span data-ttu-id="030e7-130">В следующем примере кода запускается компилирование конфигурации DSC под именем **SampleConfig**.</span><span class="sxs-lookup"><span data-stu-id="030e7-130">The following sample code starts compilation of a DSC configuration called **SampleConfig**.</span></span>

```powershell
Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"
```

<span data-ttu-id="030e7-131">`Start-AzureRmAutomationDscCompilationJob` возвращает объект задания компилирования, с помощью которого вы можете отслеживать состояние.</span><span class="sxs-lookup"><span data-stu-id="030e7-131">`Start-AzureRmAutomationDscCompilationJob` returns a compilation job object that you can use to track its status.</span></span> <span data-ttu-id="030e7-132">После этого вы можете использовать этот объект задания компилирования с помощью [`Get-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob), чтобы определить статус задания компилирования, или с помощью [`Get-AzureRmAutomationDscCompilationJobOutput`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput), чтобы просматривать его потоки (выходные данные).</span><span class="sxs-lookup"><span data-stu-id="030e7-132">You can then use this compilation job object with [`Get-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob) to determine the status of the compilation job, and [`Get-AzureRmAutomationDscCompilationJobOutput`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput) to view its streams (output).</span></span> <span data-ttu-id="030e7-133">В следующем примере кода мы запускаем компилирование конфигурации **SampleConfig** , ждем, пока оно завершится, а затем отображаем его потоки.</span><span class="sxs-lookup"><span data-stu-id="030e7-133">The following sample code starts compilation of the **SampleConfig** configuration, waits until it has completed, and then displays its streams.</span></span>

```powershell
$CompilationJob = Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"

while($CompilationJob.EndTime –eq $null -and $CompilationJob.Exception –eq $null)
{
    $CompilationJob = $CompilationJob | Get-AzureRmAutomationDscCompilationJob
    Start-Sleep -Seconds 3
}

$CompilationJob | Get-AzureRmAutomationDscCompilationJobOutput –Stream Any
```

## <a name="basic-parameters"></a><span data-ttu-id="030e7-134">Базовые параметры</span><span class="sxs-lookup"><span data-stu-id="030e7-134">Basic Parameters</span></span>
<span data-ttu-id="030e7-135">Объявление параметров, в том числе типов и свойств параметров, в конфигурациях DSC выполняется так же, как и в модулях Runbook службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="030e7-135">Parameter declaration in DSC configurations, including parameter types and properties, works the same as in Azure Automation runbooks.</span></span> <span data-ttu-id="030e7-136">Дополнительные сведения о параметрах модуля Runbook см. в статье [Запуск модуля Runbook в службе автоматизации Azure](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="030e7-136">See [Starting a runbook in Azure Automation](automation-starting-a-runbook.md) to learn more about runbook parameters.</span></span>

<span data-ttu-id="030e7-137">Чтобы определить значения свойств в конфигурации узла **ParametersExample.sample**, созданной во время компилирования, в следующем примере используются два параметра — **FeatureName** и **IsPresent**.</span><span class="sxs-lookup"><span data-stu-id="030e7-137">The following example uses two parameters called **FeatureName** and **IsPresent**, to determine the values of properties in the **ParametersExample.sample** node configuration, generated during compilation.</span></span>

```powershell
Configuration ParametersExample
{
    param(
        [Parameter(Mandatory=$true)]

        [string] $FeatureName,

        [Parameter(Mandatory=$true)]
        [boolean] $IsPresent
    )

    $EnsureString = "Present"
    if($IsPresent -eq $false)
    {
        $EnsureString = "Absent"
    }

    Node "sample"
    {
        WindowsFeature ($FeatureName + "Feature")
        {
            Ensure = $EnsureString
            Name = $FeatureName
        }
    }
}
```

<span data-ttu-id="030e7-138">Вы можете компилировать конфигурации DSC, использующие базовые параметры, на портале Azure Automation DSC или с помощью Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="030e7-138">You can compile DSC Configurations that use basic parameters in the Azure Automation DSC portal, or with Azure PowerShell:</span></span>

### <a name="portal"></a><span data-ttu-id="030e7-139">Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="030e7-139">Portal</span></span>

<span data-ttu-id="030e7-140">Чтобы ввести значения параметров на портале, нажмите кнопку **Компилировать**.</span><span class="sxs-lookup"><span data-stu-id="030e7-140">In the portal, you can enter parameter values after clicking **Compile**.</span></span>

![замещающий текст](./media/automation-dsc-compile/DSC_compiling_1.png)

### <a name="powershell"></a><span data-ttu-id="030e7-142">PowerShell</span><span class="sxs-lookup"><span data-stu-id="030e7-142">PowerShell</span></span>

<span data-ttu-id="030e7-143">Для модуля PowerShell нужны параметры в таблице [hashtable](http://technet.microsoft.com/library/hh847780.aspx) , в которой раздел соответствует имени параметра, а значение — значению параметра.</span><span class="sxs-lookup"><span data-stu-id="030e7-143">PowerShell requires parameters in a [hashtable](http://technet.microsoft.com/library/hh847780.aspx) where the key matches the parameter name, and the value equals the parameter value.</span></span>

```powershell
$Parameters = @{
    "FeatureName" = "Web-Server"
    "IsPresent" = $False
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ParametersExample" -Parameters $Parameters
```

<span data-ttu-id="030e7-144">Сведения о передаче учетных данных PSCredentials в качестве параметров см. в разделе <a href="#credential-assets">**Активы учетных данных**</a> ниже.</span><span class="sxs-lookup"><span data-stu-id="030e7-144">For information about passing PSCredentials as parameters, see <a href="#credential-assets">**Credential Assets**</a> below.</span></span>

## <a name="configurationdata"></a><span data-ttu-id="030e7-145">ConfigurationData</span><span class="sxs-lookup"><span data-stu-id="030e7-145">ConfigurationData</span></span>
<span data-ttu-id="030e7-146">Параметр **ConfigurationData** позволяет при использовании PowerShell DSC отделить конфигурацию структуры от любой конфигурации среды.</span><span class="sxs-lookup"><span data-stu-id="030e7-146">**ConfigurationData** allows you to separate structural configuration from any environment specific configuration while using PowerShell DSC.</span></span> <span data-ttu-id="030e7-147">Дополнительные сведения о **ConfigurationData** см. в публикации блога [Separating "What" from "Where" in PowerShell DSC](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) (Разница между "что" и "где" в DSC PowerShell).</span><span class="sxs-lookup"><span data-stu-id="030e7-147">See [Separating "What" from "Where" in PowerShell DSC](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) to learn more about **ConfigurationData**.</span></span>

> [!NOTE]
> <span data-ttu-id="030e7-148">Вы можете использовать **ConfigurationData**, когда выполняете компилирование на платформе Azure Automation DSC с помощью Azure PowerShell. Не следует использовать этот параметр на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="030e7-148">You can use **ConfigurationData** when compiling in Azure Automation DSC using Azure PowerShell, but not in the Azure portal.</span></span>

<span data-ttu-id="030e7-149">В приведенном ниже примере конфигурации DSC параметр **ConfigurationData** используется через ключевые слова **$ConfigurationData** и **$AllNodes**.</span><span class="sxs-lookup"><span data-stu-id="030e7-149">The following example DSC configuration uses **ConfigurationData** via the **$ConfigurationData** and **$AllNodes** keywords.</span></span> <span data-ttu-id="030e7-150">Для этого примера также понадобится [модуль **xWebAdministration**](https://www.powershellgallery.com/packages/xWebAdministration/):</span><span class="sxs-lookup"><span data-stu-id="030e7-150">You'll also need the [**xWebAdministration** module](https://www.powershellgallery.com/packages/xWebAdministration/) for this example:</span></span>

```powershell
Configuration ConfigurationDataSample
{
    Import-DscResource -ModuleName xWebAdministration -Name MSFT_xWebsite

    Write-Verbose $ConfigurationData.NonNodeData.SomeMessage

    Node $AllNodes.Where{$_.Role -eq "WebServer"}.NodeName
    {
        xWebsite Site
        {
            Name = $Node.SiteName
            PhysicalPath = $Node.SiteContents
            Ensure   = "Present"
        }
    }
}
```

<span data-ttu-id="030e7-151">Вы можете компилировать конфигурацию DSC, показанную выше, с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="030e7-151">You can compile the DSC configuration above with PowerShell.</span></span> <span data-ttu-id="030e7-152">Команда PowerShell ниже добавляет две конфигурации узла в опрашивающий сервер службы автоматизации Azure: **ConfigurationDataSample.MyVM1** и **ConfigurationDataSample.MyVM3**:</span><span class="sxs-lookup"><span data-stu-id="030e7-152">The below PowerShell adds two node configurations to the Azure Automation DSC Pull Server: **ConfigurationDataSample.MyVM1** and **ConfigurationDataSample.MyVM3**:</span></span>

```powershell
$ConfigData = @{
    AllNodes = @(
        @{
            NodeName = "MyVM1"
            Role = "WebServer"
        },
        @{
            NodeName = "MyVM2"
            Role = "SQLServer"
        },
        @{
            NodeName = "MyVM3"
            Role = "WebServer"
        }
    )

    NonNodeData = @{
        SomeMessage = "I love Azure Automation DSC!"
    }
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ConfigurationDataSample" -ConfigurationData $ConfigData
```

## <a name="assets"></a><span data-ttu-id="030e7-153">Активы</span><span class="sxs-lookup"><span data-stu-id="030e7-153">Assets</span></span>

<span data-ttu-id="030e7-154">Ссылки на активы одинаковы в конфигурациях и модулях Runbook платформы Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="030e7-154">Asset references are the same in Azure Automation DSC configurations and runbooks.</span></span> <span data-ttu-id="030e7-155">Дополнительную информацию см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="030e7-155">See the following for more information:</span></span>

* [<span data-ttu-id="030e7-156">Сертификаты</span><span class="sxs-lookup"><span data-stu-id="030e7-156">Certificates</span></span>](automation-certificates.md)
* [<span data-ttu-id="030e7-157">Подключения</span><span class="sxs-lookup"><span data-stu-id="030e7-157">Connections</span></span>](automation-connections.md)
* [<span data-ttu-id="030e7-158">Учетные данные</span><span class="sxs-lookup"><span data-stu-id="030e7-158">Credentials</span></span>](automation-credentials.md)
* [<span data-ttu-id="030e7-159">Переменные</span><span class="sxs-lookup"><span data-stu-id="030e7-159">Variables</span></span>](automation-variables.md)

### <a name="credential-assets"></a><span data-ttu-id="030e7-160">Активы учетных данных</span><span class="sxs-lookup"><span data-stu-id="030e7-160">Credential Assets</span></span>

<span data-ttu-id="030e7-161">Хотя конфигурации DSC в службе автоматизации Azure могут ссылаться на ресурсы учетных данных с помощью командлета **Get-AzureRmAutomationCredential**, при необходимости эти ресурсы можно передавать и в качестве параметров.</span><span class="sxs-lookup"><span data-stu-id="030e7-161">While DSC configurations in Azure Automation can reference credential assets using **Get-AzureRmAutomationCredential**, credential assets can also be passed in via parameters, if desired.</span></span> <span data-ttu-id="030e7-162">Если конфигурация принимает параметр типа **PSCredential** , в качестве значения этого параметра нужно использовать имя строки ресурса учетных данных (используется в службе автоматизации Azure), а не объект PSCredential.</span><span class="sxs-lookup"><span data-stu-id="030e7-162">If a configuration takes a parameter of **PSCredential** type, then you need to pass the string name of an Azure Automation credential asset as that parameter’s value, rather than a PSCredential object.</span></span> <span data-ttu-id="030e7-163">Названный так актив учетных данных, используемых для службы автоматизации Azure, будет в фоновом режиме извлечен и передан в конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="030e7-163">Behind the scenes, the Azure Automation credential asset with that name will be retrieved and passed to the configuration.</span></span>

<span data-ttu-id="030e7-164">Чтобы обеспечить безопасность учетных данных в конфигурациях узла (документы конфигурации MOF), учетные данные нужно зашифровать в MOF-файле конфигурации узла.</span><span class="sxs-lookup"><span data-stu-id="030e7-164">Keeping credentials secure in node configurations (MOF configuration documents) requires encrypting the credentials in the node configuration MOF file.</span></span> <span data-ttu-id="030e7-165">Служба автоматизации Azure делает больше — она зашифровывает MOF-файл целиком.</span><span class="sxs-lookup"><span data-stu-id="030e7-165">Azure Automation takes this one step further and encrypts the entire MOF file.</span></span> <span data-ttu-id="030e7-166">Но сейчас в модуле DSC PowerShell нужно подтверждать, что учетные данные можно отображать в формате обычного текста во время создания MOF-файла конфигурации узла. Это связано с тем, что модулю DSC PowerShell неизвестно, что, когда MOF-файл будет создан с помощью задачи компилирования, служба автоматизации Azure будет шифровать его целиком.</span><span class="sxs-lookup"><span data-stu-id="030e7-166">However, currently you must tell PowerShell DSC it is okay for credentials to be outputted in plain text during node configuration MOF generation, because PowerShell DSC doesn’t know that Azure Automation will be encrypting the entire MOF file after its generation via a compilation job.</span></span>

<span data-ttu-id="030e7-167">Вы можете подтвердить в модуле DSC PowerShell, что учетные данные можно отобразить в формате обычного текста в MOF-файлах конфигурации узлов, использующих [**ConfigurationData**](#configurationdata).</span><span class="sxs-lookup"><span data-stu-id="030e7-167">You can tell PowerShell DSC that it is okay for credentials to be outputted in plain text in the generated node configuration MOFs using [**ConfigurationData**](#configurationdata).</span></span> <span data-ttu-id="030e7-168">`PSDscAllowPlainTextPassword = $true` следует передать через **ConfigurationData** для каждого имени блока узла, которое отображается в конфигурации DSC и для которого нужны учетные данные.</span><span class="sxs-lookup"><span data-stu-id="030e7-168">You should pass `PSDscAllowPlainTextPassword = $true` via **ConfigurationData** for each node block’s name that appears in the DSC configuration and uses credentials.</span></span>

<span data-ttu-id="030e7-169">В следующем примере показана конфигурация DSC, использующая актив учетных данных автоматизации.</span><span class="sxs-lookup"><span data-stu-id="030e7-169">The following example shows a DSC configuration that uses an Automation credential asset.</span></span>

```powershell
Configuration CredentialSample
{
    $Cred = Get-AzureRmAutomationCredential -ResourceGroupName "ResourceGroup01" -AutomationAccountName "AutomationAcct" -Name "SomeCredentialAsset"

    Node $AllNodes.NodeName
    {
        File ExampleFile
        {
            SourcePath = "\\Server\share\path\file.ext"
            DestinationPath = "C:\destinationPath"
            Credential = $Cred
        }
    }
}
```

<span data-ttu-id="030e7-170">Вы можете компилировать конфигурацию DSC, показанную выше, с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="030e7-170">You can compile the DSC configuration above with PowerShell.</span></span> <span data-ttu-id="030e7-171">Команда PowerShell ниже добавляет две конфигурации узла в опрашивающий сервер службы автоматизации Azure: **CredentialSample.MyVM1** и **CredentialSample.MyVM2**.</span><span class="sxs-lookup"><span data-stu-id="030e7-171">The below PowerShell adds two node configurations to the Azure Automation DSC Pull Server:  **CredentialSample.MyVM1** and **CredentialSample.MyVM2**.</span></span>

```powershell
$ConfigData = @{
    AllNodes = @(
        @{
            NodeName = "*"
            PSDscAllowPlainTextPassword = $True
        },
        @{
            NodeName = "MyVM1"
        },
        @{
            NodeName = "MyVM2"
        }
    )
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "CredentialSample" -ConfigurationData $ConfigData
```

## <a name="importing-node-configurations"></a><span data-ttu-id="030e7-172">Импорт конфигураций узлов</span><span class="sxs-lookup"><span data-stu-id="030e7-172">Importing node configurations</span></span>

<span data-ttu-id="030e7-173">Вы также можете импортировать конфигурации узла (MOF-файлы), скомпилированные за пределами Azure.</span><span class="sxs-lookup"><span data-stu-id="030e7-173">You can also import node configuratons (MOFs) that you have compiled outside of Azure.</span></span> <span data-ttu-id="030e7-174">Одним из преимуществ является то, что конфигурации узла могут быть заверены.</span><span class="sxs-lookup"><span data-stu-id="030e7-174">One advantage of this is that node confiturations can be signed.</span></span>
<span data-ttu-id="030e7-175">Заверенная конфигурация узла проверяется локально на управляемом узле агентом DSC. Тем самым гарантируется, что конфигурация, применяемая к узлу, передана из авторизованного источника.</span><span class="sxs-lookup"><span data-stu-id="030e7-175">A signed node configuration is verified locally on a managed node by the DSC agent, ensuring that the configuration being applied to the node comes from an authorized source.</span></span>

> [!NOTE]
> <span data-ttu-id="030e7-176">Заверенные конфигурации можно импортировать в учетную запись службы автоматизации Azure, но служба автоматизации Azure в настоящее время не поддерживает компиляцию заверенных конфигураций.</span><span class="sxs-lookup"><span data-stu-id="030e7-176">You can use import signed configurations into your Azure Automation account, but Azure Automation does not currently support compiling signed configurations.</span></span>

> [!NOTE]
> <span data-ttu-id="030e7-177">Размер файла конфигурации узла не должен превышать 1 МБ, чтобы его можно было импортировать в службу автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="030e7-177">A node configuration file must be no larger than 1 MB to allow it to be imported into Azure Automation.</span></span>

<span data-ttu-id="030e7-178">Сведения о том, как заверить конфигурацию узла, см. по следующей ссылке: https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module.</span><span class="sxs-lookup"><span data-stu-id="030e7-178">You can learn how to sign node configurations at https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module.</span></span>

### <a name="importing-a-node-configuration-in-the-azure-portal"></a><span data-ttu-id="030e7-179">Импорт конфигурации узла на портале Azure</span><span class="sxs-lookup"><span data-stu-id="030e7-179">Importing a node configuration in the Azure portal</span></span>

1. <span data-ttu-id="030e7-180">В учетной записи службы автоматизации щелкните **DSC node configurations** (Конфигурации узла DSC).</span><span class="sxs-lookup"><span data-stu-id="030e7-180">From your Automation account, click **DSC node configurations**.</span></span>

    ![Конфигурации узла DSC](./media/automation-dsc-compile/node-config.png)
2. <span data-ttu-id="030e7-182">В колонке **DSC node configurations** (Конфигурации узла DSC) щелкните **Add a NodeConfiguration** (Добавить конфигурацию узла).</span><span class="sxs-lookup"><span data-stu-id="030e7-182">In the **DSC node configurations** blade, click **Add a NodeConfiguration**.</span></span>
3. <span data-ttu-id="030e7-183">В колонке **Import** (Импорт) щелкните значок папки рядом с текстовым полем **Node Configuration File** (Файл конфигурации узла), чтобы найти файл конфигурации узла (MOF) на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="030e7-183">In the **Import** blade, click the folder icon next to the **Node Configuration File** textbox to browse for a node configuration file (MOF) on your local computer.</span></span>

    ![Поиск локального файла](./media/automation-dsc-compile/import-browse.png)
4. <span data-ttu-id="030e7-185">В текстовом поле **Configuration Name** (Имя конфигурации) введите имя.</span><span class="sxs-lookup"><span data-stu-id="030e7-185">Enter a name in the **Configuration Name** textbox.</span></span> <span data-ttu-id="030e7-186">Это имя должно совпадать с именем конфигурации, из которой была скомпилирована данная конфигурация узла.</span><span class="sxs-lookup"><span data-stu-id="030e7-186">This name must match the name of the configuration from which the node configuration was compiled.</span></span>
5. <span data-ttu-id="030e7-187">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="030e7-187">Click **OK**.</span></span>

### <a name="importing-a-node-configuration-with-powershell"></a><span data-ttu-id="030e7-188">Импорт конфигурации узла с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="030e7-188">Importing a node configuration with PowerShell</span></span>

<span data-ttu-id="030e7-189">Для импорта конфигурации узла в учетную запись службы автоматизации можно использовать командлет [Import-AzureRmAutomationDscNodeConfiguration](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration).</span><span class="sxs-lookup"><span data-stu-id="030e7-189">You can use the [Import-AzureRmAutomationDscNodeConfiguration](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) cmdlet to import a node configuration into your automation account.</span></span>

```powershell
Import-AzureRmAutomationDscNodeConfiguration -AutomationAccountName "MyAutomationAccount" -ResourceGroupName "MyResourceGroup" -ConfigurationName "MyNodeConfiguration" -Path "C:\MyConfigurations\TestVM1.mof"
```



