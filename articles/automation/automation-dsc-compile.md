---
title: "aaaCompiling конфигурации в DSC службы автоматизации Azure | Документы Microsoft"
description: "В этой статье описывается как toocompile конфигурации требуемого состояния (DSC) для автоматизации Azure."
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
ms.openlocfilehash: b195311318a2d7431c4d6b29f4b9a5f3a0a0a9a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="compiling-configurations-in-azure-automation-dsc"></a><span data-ttu-id="011b0-103">Компилирование конфигураций в Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="011b0-103">Compiling configurations in Azure Automation DSC</span></span>

<span data-ttu-id="011b0-104">Можно скомпилировать конфигурации требуемого состояния (DSC) в службе автоматизации Azure двумя способами: в hello портал Azure, а также с помощью Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="011b0-104">You can compile Desired State Configuration (DSC) configurations in two ways with Azure Automation: in hello Azure portal, and with Windows PowerShell.</span></span> <span data-ttu-id="011b0-105">Hello Следующая таблица поможет определить, когда какой метод на основе hello характеристик каждого toouse:</span><span class="sxs-lookup"><span data-stu-id="011b0-105">hello following table will help you determine when toouse which method based on hello characteristics of each:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="011b0-106">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="011b0-106">Azure portal</span></span>

* <span data-ttu-id="011b0-107">Простейший способ с интерактивным пользовательским интерфейсом.</span><span class="sxs-lookup"><span data-stu-id="011b0-107">Simplest method with interactive user interface</span></span>
* <span data-ttu-id="011b0-108">Значения параметра простой формы tooprovide</span><span class="sxs-lookup"><span data-stu-id="011b0-108">Form tooprovide simple parameter values</span></span>
* <span data-ttu-id="011b0-109">Легко отслеживаемое состояние задания.</span><span class="sxs-lookup"><span data-stu-id="011b0-109">Easily track job state</span></span>
* <span data-ttu-id="011b0-110">Доступ с проверкой подлинности в Azure.</span><span class="sxs-lookup"><span data-stu-id="011b0-110">Access authenticated with Azure logon</span></span>

### <a name="windows-powershell"></a><span data-ttu-id="011b0-111">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="011b0-111">Windows PowerShell</span></span>

* <span data-ttu-id="011b0-112">Вызов из командной строки с помощью командлетов Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="011b0-112">Call from command line with Windows PowerShell cmdlets</span></span>
* <span data-ttu-id="011b0-113">Может быть добавлено в автоматизированное решение, состоящее из нескольких шагов.</span><span class="sxs-lookup"><span data-stu-id="011b0-113">Can be included in automated solution with multiple steps</span></span>
* <span data-ttu-id="011b0-114">Необходимо предоставить значения простых и сложных параметров.</span><span class="sxs-lookup"><span data-stu-id="011b0-114">Provide simple and complex parameter values</span></span>
* <span data-ttu-id="011b0-115">Отслеживание состояния задания</span><span class="sxs-lookup"><span data-stu-id="011b0-115">Track job state</span></span>
* <span data-ttu-id="011b0-116">Требуется клиент toosupport командлеты PowerShell</span><span class="sxs-lookup"><span data-stu-id="011b0-116">Client required toosupport PowerShell cmdlets</span></span>
* <span data-ttu-id="011b0-117">Передача данных ConfigurationData.</span><span class="sxs-lookup"><span data-stu-id="011b0-117">Pass ConfigurationData</span></span>
* <span data-ttu-id="011b0-118">Компилирование конфигураций, использующих учетные данные.</span><span class="sxs-lookup"><span data-stu-id="011b0-118">Compile configurations that use credentials</span></span>

<span data-ttu-id="011b0-119">После выбора метода компиляции, можно выполнить соответствующие процедуры hello ниже toostart компиляции.</span><span class="sxs-lookup"><span data-stu-id="011b0-119">Once you have decided on a compilation method, you can follow hello respective procedures below toostart compiling.</span></span>

## <a name="compiling-a-dsc-configuration-with-hello-azure-portal"></a><span data-ttu-id="011b0-120">При компиляции конфигурации DSC с hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="011b0-120">Compiling a DSC Configuration with hello Azure portal</span></span>

1. <span data-ttu-id="011b0-121">В учетной записи службы автоматизации щелкните **DSC Configurations** (Конфигурации DSC).</span><span class="sxs-lookup"><span data-stu-id="011b0-121">From your Automation account, click **DSC Configurations**.</span></span>
2. <span data-ttu-id="011b0-122">Щелкните tooopen конфигурации колонке.</span><span class="sxs-lookup"><span data-stu-id="011b0-122">Click a configuration tooopen its blade.</span></span>
3. <span data-ttu-id="011b0-123">Нажмите кнопку **Компилировать**.</span><span class="sxs-lookup"><span data-stu-id="011b0-123">Click **Compile**.</span></span>
4. <span data-ttu-id="011b0-124">Если конфигурация hello не имеет параметров, можно запрашиваемые tooconfirm следует toocompile ли он.</span><span class="sxs-lookup"><span data-stu-id="011b0-124">If hello configuration has no parameters, you will be prompted tooconfirm whether you want toocompile it.</span></span> <span data-ttu-id="011b0-125">Если параметры конфигурации hello, hello **компиляции конфигурации** колонке будет открыт, чтобы обеспечить значения параметров.</span><span class="sxs-lookup"><span data-stu-id="011b0-125">If hello configuration has parameters, hello **Compile Configuration** blade will open so you can provide parameter values.</span></span> <span data-ttu-id="011b0-126">В разделе hello [ **базовых параметров** ](#basic-parameters) ниже, в разделе для получения сведений о параметрах.</span><span class="sxs-lookup"><span data-stu-id="011b0-126">See hello [**Basic Parameters**](#basic-parameters) section below for further details on parameters.</span></span>
5. <span data-ttu-id="011b0-127">Hello **задание компиляции** открывается колонка, чтобы отследить состояние задания компиляции hello и hello конфигурации узла (документам MOF конфигурации), она вызвана toobe обмена hello опрашивающего сервера Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="011b0-127">hello **Compilation Job** blade is opened so that you can track hello compilation job's status, and hello node configurations (MOF configuration documents) it caused toobe placed on hello Azure Automation DSC Pull Server.</span></span>

## <a name="compiling-a-dsc-configuration-with-windows-powershell"></a><span data-ttu-id="011b0-128">Компилирование конфигурации DSC с помощью Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="011b0-128">Compiling a DSC Configuration with Windows PowerShell</span></span>

<span data-ttu-id="011b0-129">Можно использовать [ `Start-AzureRmAutomationDscCompilationJob` ](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) toostart компиляции с помощью Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="011b0-129">You can use [`Start-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) toostart compiling with Windows PowerShell.</span></span> <span data-ttu-id="011b0-130">Следующий пример кода Hello запускает компиляции конфигурации DSC, называемой **SampleConfig**.</span><span class="sxs-lookup"><span data-stu-id="011b0-130">hello following sample code starts compilation of a DSC configuration called **SampleConfig**.</span></span>

```powershell
Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"
```

<span data-ttu-id="011b0-131">`Start-AzureRmAutomationDscCompilationJob`Возвращает компиляции заданий, которые можно использовать tootrack его состояние объекта.</span><span class="sxs-lookup"><span data-stu-id="011b0-131">`Start-AzureRmAutomationDscCompilationJob` returns a compilation job object that you can use tootrack its status.</span></span> <span data-ttu-id="011b0-132">Затем можно использовать этот объект задания компиляции с [ `Get-AzureRmAutomationDscCompilationJob` ](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob) toodetermine hello состояние задания компиляции hello, и [ `Get-AzureRmAutomationDscCompilationJobOutput` ](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput) tooview свои потоки (output).</span><span class="sxs-lookup"><span data-stu-id="011b0-132">You can then use this compilation job object with [`Get-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob) toodetermine hello status of hello compilation job, and [`Get-AzureRmAutomationDscCompilationJobOutput`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput) tooview its streams (output).</span></span> <span data-ttu-id="011b0-133">Следующий образец кода Hello начинает компиляцию hello **SampleConfig** конфигурации, ожидает его завершения, а затем отображает свои потоки.</span><span class="sxs-lookup"><span data-stu-id="011b0-133">hello following sample code starts compilation of hello **SampleConfig** configuration, waits until it has completed, and then displays its streams.</span></span>

```powershell
$CompilationJob = Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"

while($CompilationJob.EndTime –eq $null -and $CompilationJob.Exception –eq $null)
{
    $CompilationJob = $CompilationJob | Get-AzureRmAutomationDscCompilationJob
    Start-Sleep -Seconds 3
}

$CompilationJob | Get-AzureRmAutomationDscCompilationJobOutput –Stream Any
```

## <a name="basic-parameters"></a><span data-ttu-id="011b0-134">Базовые параметры</span><span class="sxs-lookup"><span data-stu-id="011b0-134">Basic Parameters</span></span>
<span data-ttu-id="011b0-135">Объявление параметра в конфигурациях DSC, включая типы параметров и свойств, работает hello таким же как модулей Runbook службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="011b0-135">Parameter declaration in DSC configurations, including parameter types and properties, works hello same as in Azure Automation runbooks.</span></span> <span data-ttu-id="011b0-136">В разделе [запуск runbook в автоматизации Azure](automation-starting-a-runbook.md) toolearn Дополнительные сведения о параметрах runbook.</span><span class="sxs-lookup"><span data-stu-id="011b0-136">See [Starting a runbook in Azure Automation](automation-starting-a-runbook.md) toolearn more about runbook parameters.</span></span>

<span data-ttu-id="011b0-137">Hello следующий пример использует два параметра при вызове **FeatureName** и **IsPresent**, значений свойств в hello hello toodetermine **ParametersExample.sample** узла Конфигурация, созданные во время компиляции.</span><span class="sxs-lookup"><span data-stu-id="011b0-137">hello following example uses two parameters called **FeatureName** and **IsPresent**, toodetermine hello values of properties in hello **ParametersExample.sample** node configuration, generated during compilation.</span></span>

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

<span data-ttu-id="011b0-138">Вы можете скомпилировать конфигураций DSC, используйте базовых параметров портала Azure Automation DSC hello, или с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="011b0-138">You can compile DSC Configurations that use basic parameters in hello Azure Automation DSC portal, or with Azure PowerShell:</span></span>

### <a name="portal"></a><span data-ttu-id="011b0-139">Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="011b0-139">Portal</span></span>

<span data-ttu-id="011b0-140">На портале hello, можно ввести значения параметров после нажатия кнопки **компиляции**.</span><span class="sxs-lookup"><span data-stu-id="011b0-140">In hello portal, you can enter parameter values after clicking **Compile**.</span></span>

![замещающий текст](./media/automation-dsc-compile/DSC_compiling_1.png)

### <a name="powershell"></a><span data-ttu-id="011b0-142">PowerShell</span><span class="sxs-lookup"><span data-stu-id="011b0-142">PowerShell</span></span>

<span data-ttu-id="011b0-143">PowerShell требуются параметры в [hashtable](http://technet.microsoft.com/library/hh847780.aspx) hello ключ совпадает с именем параметра hello, куда hello, значение равно значению параметра hello.</span><span class="sxs-lookup"><span data-stu-id="011b0-143">PowerShell requires parameters in a [hashtable](http://technet.microsoft.com/library/hh847780.aspx) where hello key matches hello parameter name, and hello value equals hello parameter value.</span></span>

```powershell
$Parameters = @{
    "FeatureName" = "Web-Server"
    "IsPresent" = $False
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ParametersExample" -Parameters $Parameters
```

<span data-ttu-id="011b0-144">Сведения о передаче учетных данных PSCredentials в качестве параметров см. в разделе <a href="#credential-assets">**Активы учетных данных**</a> ниже.</span><span class="sxs-lookup"><span data-stu-id="011b0-144">For information about passing PSCredentials as parameters, see <a href="#credential-assets">**Credential Assets**</a> below.</span></span>

## <a name="configurationdata"></a><span data-ttu-id="011b0-145">ConfigurationData</span><span class="sxs-lookup"><span data-stu-id="011b0-145">ConfigurationData</span></span>
<span data-ttu-id="011b0-146">**ConfigurationData** позволяет tooseparate отделение структурной конфигурации из какой-либо настройки среды при работе с PowerShell DSC.</span><span class="sxs-lookup"><span data-stu-id="011b0-146">**ConfigurationData** allows you tooseparate structural configuration from any environment specific configuration while using PowerShell DSC.</span></span> <span data-ttu-id="011b0-147">В разделе [отделение «Что» от «Where» в PowerShell DSC](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) toolearn Дополнительные сведения о **ConfigurationData**.</span><span class="sxs-lookup"><span data-stu-id="011b0-147">See [Separating "What" from "Where" in PowerShell DSC](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) toolearn more about **ConfigurationData**.</span></span>

> [!NOTE]
> <span data-ttu-id="011b0-148">Можно использовать **ConfigurationData** при компиляции в Azure Automation DSC с помощью Azure PowerShell, но не в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="011b0-148">You can use **ConfigurationData** when compiling in Azure Automation DSC using Azure PowerShell, but not in hello Azure portal.</span></span>

<span data-ttu-id="011b0-149">Hello ниже примере DSC конфигурации используется **ConfigurationData** через hello **$ConfigurationData** и **$AllNodes** ключевые слова.</span><span class="sxs-lookup"><span data-stu-id="011b0-149">hello following example DSC configuration uses **ConfigurationData** via hello **$ConfigurationData** and **$AllNodes** keywords.</span></span> <span data-ttu-id="011b0-150">Кроме того, потребуется hello [ **xWebAdministration** модуль](https://www.powershellgallery.com/packages/xWebAdministration/) в этом примере:</span><span class="sxs-lookup"><span data-stu-id="011b0-150">You'll also need hello [**xWebAdministration** module](https://www.powershellgallery.com/packages/xWebAdministration/) for this example:</span></span>

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

<span data-ttu-id="011b0-151">Можно скомпилировать конфигурацию DSC hello выше с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="011b0-151">You can compile hello DSC configuration above with PowerShell.</span></span> <span data-ttu-id="011b0-152">Hello под PowerShell добавляет два узла конфигурации toohello опрашивающего сервера Azure Automation DSC: **ConfigurationDataSample.MyVM1** и **ConfigurationDataSample.MyVM3**:</span><span class="sxs-lookup"><span data-stu-id="011b0-152">hello below PowerShell adds two node configurations toohello Azure Automation DSC Pull Server: **ConfigurationDataSample.MyVM1** and **ConfigurationDataSample.MyVM3**:</span></span>

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

## <a name="assets"></a><span data-ttu-id="011b0-153">Активы</span><span class="sxs-lookup"><span data-stu-id="011b0-153">Assets</span></span>

<span data-ttu-id="011b0-154">Ссылки на средства hello же Azure Automation DSC конфигурации и модулей Runbook.</span><span class="sxs-lookup"><span data-stu-id="011b0-154">Asset references are hello same in Azure Automation DSC configurations and runbooks.</span></span> <span data-ttu-id="011b0-155">Hello ниже для получения дополнительной информации см.:</span><span class="sxs-lookup"><span data-stu-id="011b0-155">See hello following for more information:</span></span>

* [<span data-ttu-id="011b0-156">Сертификаты</span><span class="sxs-lookup"><span data-stu-id="011b0-156">Certificates</span></span>](automation-certificates.md)
* [<span data-ttu-id="011b0-157">Подключения</span><span class="sxs-lookup"><span data-stu-id="011b0-157">Connections</span></span>](automation-connections.md)
* [<span data-ttu-id="011b0-158">Учетные данные</span><span class="sxs-lookup"><span data-stu-id="011b0-158">Credentials</span></span>](automation-credentials.md)
* [<span data-ttu-id="011b0-159">Переменные</span><span class="sxs-lookup"><span data-stu-id="011b0-159">Variables</span></span>](automation-variables.md)

### <a name="credential-assets"></a><span data-ttu-id="011b0-160">Активы учетных данных</span><span class="sxs-lookup"><span data-stu-id="011b0-160">Credential Assets</span></span>

<span data-ttu-id="011b0-161">Хотя конфигурации DSC в службе автоматизации Azure могут ссылаться на ресурсы учетных данных с помощью командлета **Get-AzureRmAutomationCredential**, при необходимости эти ресурсы можно передавать и в качестве параметров.</span><span class="sxs-lookup"><span data-stu-id="011b0-161">While DSC configurations in Azure Automation can reference credential assets using **Get-AzureRmAutomationCredential**, credential assets can also be passed in via parameters, if desired.</span></span> <span data-ttu-id="011b0-162">Если конфигурация принимает параметр **PSCredential** тип, как значение этого параметра, а не объект PSCredential, потребуется toopass hello строковое имя актива учетных данных службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="011b0-162">If a configuration takes a parameter of **PSCredential** type, then you need toopass hello string name of an Azure Automation credential asset as that parameter’s value, rather than a PSCredential object.</span></span> <span data-ttu-id="011b0-163">В фоновом hello hello Azure учетных данных службы автоматизации с таким именем будет получаться и переданный toohello конфигурации.</span><span class="sxs-lookup"><span data-stu-id="011b0-163">Behind hello scenes, hello Azure Automation credential asset with that name will be retrieved and passed toohello configuration.</span></span>

<span data-ttu-id="011b0-164">Хранение учетных данных безопасности в конфигурации узла (документам MOF конфигурации) требует шифрования hello учетных данных в MOF-файл конфигурации узла hello.</span><span class="sxs-lookup"><span data-stu-id="011b0-164">Keeping credentials secure in node configurations (MOF configuration documents) requires encrypting hello credentials in hello node configuration MOF file.</span></span> <span data-ttu-id="011b0-165">Служба автоматизации Azure расширяет эти дополнительные и шифрует hello всей MOF-файл.</span><span class="sxs-lookup"><span data-stu-id="011b0-165">Azure Automation takes this one step further and encrypts hello entire MOF file.</span></span> <span data-ttu-id="011b0-166">Однако в настоящее время необходимо сообщить PowerShell DSC допустимо для toobe учетные данные, выводимые в виде обычного текста во время создания MOF конфигурации узла, так как PowerShell DSC не знает, что службы автоматизации Azure будет шифрования hello всей MOF-файл после его Создание через задание компиляции.</span><span class="sxs-lookup"><span data-stu-id="011b0-166">However, currently you must tell PowerShell DSC it is okay for credentials toobe outputted in plain text during node configuration MOF generation, because PowerShell DSC doesn’t know that Azure Automation will be encrypting hello entire MOF file after its generation via a compilation job.</span></span>

<span data-ttu-id="011b0-167">Можно определить PowerShell DSC, что допустимо для toobe учетные данные, выводимые в виде обычного текста в конфигурации узла hello созданный MOF-файлы с помощью [ **ConfigurationData**](#configurationdata).</span><span class="sxs-lookup"><span data-stu-id="011b0-167">You can tell PowerShell DSC that it is okay for credentials toobe outputted in plain text in hello generated node configuration MOFs using [**ConfigurationData**](#configurationdata).</span></span> <span data-ttu-id="011b0-168">Необходимо передать `PSDscAllowPlainTextPassword = $true` через **ConfigurationData** для каждого узла блока имя, которое отображается в конфигурации hello DSC и использует учетные данные.</span><span class="sxs-lookup"><span data-stu-id="011b0-168">You should pass `PSDscAllowPlainTextPassword = $true` via **ConfigurationData** for each node block’s name that appears in hello DSC configuration and uses credentials.</span></span>

<span data-ttu-id="011b0-169">Hello пример конфигурации DSC, использующий актива учетных данных службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="011b0-169">hello following example shows a DSC configuration that uses an Automation credential asset.</span></span>

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

<span data-ttu-id="011b0-170">Можно скомпилировать конфигурацию DSC hello выше с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="011b0-170">You can compile hello DSC configuration above with PowerShell.</span></span> <span data-ttu-id="011b0-171">Hello под PowerShell добавляет два узла конфигурации toohello опрашивающего сервера Azure Automation DSC: **CredentialSample.MyVM1** и **CredentialSample.MyVM2**.</span><span class="sxs-lookup"><span data-stu-id="011b0-171">hello below PowerShell adds two node configurations toohello Azure Automation DSC Pull Server:  **CredentialSample.MyVM1** and **CredentialSample.MyVM2**.</span></span>

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

## <a name="importing-node-configurations"></a><span data-ttu-id="011b0-172">Импорт конфигураций узлов</span><span class="sxs-lookup"><span data-stu-id="011b0-172">Importing node configurations</span></span>

<span data-ttu-id="011b0-173">Вы также можете импортировать конфигурации узла (MOF-файлы), скомпилированные за пределами Azure.</span><span class="sxs-lookup"><span data-stu-id="011b0-173">You can also import node configuratons (MOFs) that you have compiled outside of Azure.</span></span> <span data-ttu-id="011b0-174">Одним из преимуществ является то, что конфигурации узла могут быть заверены.</span><span class="sxs-lookup"><span data-stu-id="011b0-174">One advantage of this is that node confiturations can be signed.</span></span>
<span data-ttu-id="011b0-175">Настройка знаком узла подтверждается локально на управляемом узле агент hello DSC, гарантируя, что в этой конфигурации hello, примененные toohello узла поступает из авторизованного источника.</span><span class="sxs-lookup"><span data-stu-id="011b0-175">A signed node configuration is verified locally on a managed node by hello DSC agent, ensuring that hello configuration being applied toohello node comes from an authorized source.</span></span>

> [!NOTE]
> <span data-ttu-id="011b0-176">Заверенные конфигурации можно импортировать в учетную запись службы автоматизации Azure, но служба автоматизации Azure в настоящее время не поддерживает компиляцию заверенных конфигураций.</span><span class="sxs-lookup"><span data-stu-id="011b0-176">You can use import signed configurations into your Azure Automation account, but Azure Automation does not currently support compiling signed configurations.</span></span>

> [!NOTE]
> <span data-ttu-id="011b0-177">Файл конфигурации узла должно быть не больше 1 МБ tooallow его toobe, импортированные в службу автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="011b0-177">A node configuration file must be no larger than 1 MB tooallow it toobe imported into Azure Automation.</span></span>

<span data-ttu-id="011b0-178">Рассказывается, как на https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module toosign узла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="011b0-178">You can learn how toosign node configurations at https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module.</span></span>

### <a name="importing-a-node-configuration-in-hello-azure-portal"></a><span data-ttu-id="011b0-179">Импорт конфигурации узла в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="011b0-179">Importing a node configuration in hello Azure portal</span></span>

1. <span data-ttu-id="011b0-180">В учетной записи службы автоматизации щелкните **DSC node configurations** (Конфигурации узла DSC).</span><span class="sxs-lookup"><span data-stu-id="011b0-180">From your Automation account, click **DSC node configurations**.</span></span>

    ![Конфигурации узла DSC](./media/automation-dsc-compile/node-config.png)
2. <span data-ttu-id="011b0-182">В hello **конфигурации узла DSC** колонка, щелкните **добавить NodeConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="011b0-182">In hello **DSC node configurations** blade, click **Add a NodeConfiguration**.</span></span>
3. <span data-ttu-id="011b0-183">В hello **импорта** колонке нажмите кнопку Далее toohello hello папки значок **файла конфигурации узла** toobrowse textbox для файла конфигурации узла (MOF) на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="011b0-183">In hello **Import** blade, click hello folder icon next toohello **Node Configuration File** textbox toobrowse for a node configuration file (MOF) on your local computer.</span></span>

    ![Поиск локального файла](./media/automation-dsc-compile/import-browse.png)
4. <span data-ttu-id="011b0-185">Введите имя в hello **имя конфигурации** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="011b0-185">Enter a name in hello **Configuration Name** textbox.</span></span> <span data-ttu-id="011b0-186">Это имя должно совпадать с именем hello hello конфигурации, из которой была скомпилирована hello конфигурации узла.</span><span class="sxs-lookup"><span data-stu-id="011b0-186">This name must match hello name of hello configuration from which hello node configuration was compiled.</span></span>
5. <span data-ttu-id="011b0-187">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="011b0-187">Click **OK**.</span></span>

### <a name="importing-a-node-configuration-with-powershell"></a><span data-ttu-id="011b0-188">Импорт конфигурации узла с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="011b0-188">Importing a node configuration with PowerShell</span></span>

<span data-ttu-id="011b0-189">Можно использовать hello [AzureRmAutomationDscNodeConfiguration импорта](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) tooimport командлет конфигурации узла, в свою учетную запись автоматизации.</span><span class="sxs-lookup"><span data-stu-id="011b0-189">You can use hello [Import-AzureRmAutomationDscNodeConfiguration](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) cmdlet tooimport a node configuration into your automation account.</span></span>

```powershell
Import-AzureRmAutomationDscNodeConfiguration -AutomationAccountName "MyAutomationAccount" -ResourceGroupName "MyResourceGroup" -ConfigurationName "MyNodeConfiguration" -Path "C:\MyConfigurations\TestVM1.mof"
```



