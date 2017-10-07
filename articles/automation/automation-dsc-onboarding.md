---
title: "aaaOnboarding машин для управления с помощью DSC службы автоматизации Azure | Документы Microsoft"
description: "Как toosetup компьютеров для управления с помощью DSC службы автоматизации Azure"
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
ms.assetid: da13e1f5-2a1c-443b-8e3b-9f0d6f9e4810
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 12/13/2016
ms.author: eslesar
ms.openlocfilehash: ef15801fec2ffea4ba62dcba2fbe9af09268e424
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="onboarding-machines-for-management-by-azure-automation-dsc"></a><span data-ttu-id="77ca4-103">Подключение компьютеров для управления с помощью Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="77ca4-103">Onboarding machines for management by Azure Automation DSC</span></span>

## <a name="why-manage-machines-with-azure-automation-dsc"></a><span data-ttu-id="77ca4-104">В чем преимущества управления компьютерами с помощью службы Azure Automation DSC?</span><span class="sxs-lookup"><span data-stu-id="77ca4-104">Why manage machines with Azure Automation DSC?</span></span>

<span data-ttu-id="77ca4-105">Настройка требуемого состояния (DSC) с помощью службы автоматизации Azure так же проста, как и [настройка требуемого состояния с использованием PowerShell](https://technet.microsoft.com/library/dn249912.aspx). Это мощная служба управления конфигурациями для узлов DSC (физических и виртуальных машин), которую можно использовать в любом облачном или локальном центре обработки данных.</span><span class="sxs-lookup"><span data-stu-id="77ca4-105">Like [PowerShell Desired State Configuration](https://technet.microsoft.com/library/dn249912.aspx), Azure Automation Desired State Configuration is a simple, yet powerful, configuration management service for DSC nodes (physical and virtual machines) in any cloud or on-premises datacenter.</span></span> <span data-ttu-id="77ca4-106">Она обеспечивает быструю и простую масштабируемость тысяч компьютеров из безопасного центрального расположения.</span><span class="sxs-lookup"><span data-stu-id="77ca4-106">It enables scalability across thousands of machines quickly and easily from a central, secure location.</span></span> <span data-ttu-id="77ca4-107">Вы можете легко присоединяться машины, назначьте их декларативной конфигурации и просмотр отчетов, отражающих каждого компьютера, состояние соответствия требуемой toohello указанный.</span><span class="sxs-lookup"><span data-stu-id="77ca4-107">You can easily onboard machines, assign them declarative configurations, and view reports showing each machine's compliance toohello desired state you specified.</span></span> <span data-ttu-id="77ca4-108">уровень управления Hello Azure Automation DSC — tooDSC какой уровень управления hello Azure Automation является tooPowerShell сценариев.</span><span class="sxs-lookup"><span data-stu-id="77ca4-108">hello Azure Automation DSC management layer is tooDSC what hello Azure Automation management layer is tooPowerShell scripting.</span></span> <span data-ttu-id="77ca4-109">Другими словами в hello аналогично, автоматизация Azure помогает управлять сценариев PowerShell, он также позволяет управлять конфигурациями DSC.</span><span class="sxs-lookup"><span data-stu-id="77ca4-109">In other words, in hello same way that Azure Automation helps you manage PowerShell scripts, it also helps you manage DSC configurations.</span></span> <span data-ttu-id="77ca4-110">toolearn Дополнительные сведения о hello преимущества использования Azure Automation DSC. в разделе [Обзор Azure Automation DSC](automation-dsc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="77ca4-110">toolearn more about hello benefits of using Azure Automation DSC, see [Azure Automation DSC overview](automation-dsc-overview.md).</span></span>

<span data-ttu-id="77ca4-111">Azure Automation DSC можно использовать toomanage различных компьютерах:</span><span class="sxs-lookup"><span data-stu-id="77ca4-111">Azure Automation DSC can be used toomanage a variety of machines:</span></span>

* <span data-ttu-id="77ca4-112">Виртуальные машины Azure (классические).</span><span class="sxs-lookup"><span data-stu-id="77ca4-112">Azure virtual machines (classic)</span></span>
* <span data-ttu-id="77ca4-113">Виртуальные машины Azure</span><span class="sxs-lookup"><span data-stu-id="77ca4-113">Azure virtual machines</span></span>
* <span data-ttu-id="77ca4-114">виртуальные машины Amazon Web Services (AWS);</span><span class="sxs-lookup"><span data-stu-id="77ca4-114">Amazon Web Services (AWS) virtual machines</span></span>
* <span data-ttu-id="77ca4-115">физические или виртуальные машины под управлением Windows, расположенные локально или в облачной службе, отличной от Azure или AWS;</span><span class="sxs-lookup"><span data-stu-id="77ca4-115">Physical/virtual Windows machines on-premises, or in a cloud other than Azure/AWS</span></span>
* <span data-ttu-id="77ca4-116">Физические или виртуальные машины под управлением Linux, расположенные локально, в Azure или облачной службе, отличной от Azure.</span><span class="sxs-lookup"><span data-stu-id="77ca4-116">Physical/virtual Linux machines on-premises, in Azure, or in a cloud other than Azure</span></span>

<span data-ttu-id="77ca4-117">Кроме того Если вы не готовы toomanage конфигурации машины из облака hello, Azure Automation DSC может также использоваться как конечную точку только для отчетов.</span><span class="sxs-lookup"><span data-stu-id="77ca4-117">In addition, if you are not ready toomanage machine configuration from hello cloud, Azure Automation DSC can also be used as a report-only endpoint.</span></span> <span data-ttu-id="77ca4-118">Это позволяет tooset (push) требуемой конфигурации с помощью DSC в локальной среде и просмотр сведений широкие возможности отчетности на соответствие узел hello требуемое состояние в службе автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="77ca4-118">This allows you tooset (push) desired configuration through DSC on-premises and view rich reporting details on node compliance with hello desired state in Azure Automation.</span></span>

<span data-ttu-id="77ca4-119">Hello в следующих разделах описываются способы подключения каждого типа машины tooAzure DSC службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="77ca4-119">hello following sections outline how you can onboard each type of machine tooAzure Automation DSC.</span></span>

## <a name="azure-virtual-machines-classic"></a><span data-ttu-id="77ca4-120">Виртуальные машины Azure (классические).</span><span class="sxs-lookup"><span data-stu-id="77ca4-120">Azure virtual machines (classic)</span></span>

<span data-ttu-id="77ca4-121">С помощью DSC службы автоматизации Azure можно легко присоединяться виртуальных машинах Azure (классические) для управления конфигурацией с помощью портала Azure hello или PowerShell.</span><span class="sxs-lookup"><span data-stu-id="77ca4-121">With Azure Automation DSC, you can easily onboard Azure virtual machines (classic) for configuration management using either hello Azure portal, or PowerShell.</span></span> <span data-ttu-id="77ca4-122">Кулисами hello и без администратор, имеющий tooremote в hello ВМ hello расширения для настройки требуемого состояния Azure VM регистрирует hello виртуальной Машины Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="77ca4-122">Under hello hood, and without an administrator having tooremote into hello VM, hello Azure VM Desired State Configuration extension registers hello VM with Azure Automation DSC.</span></span> <span data-ttu-id="77ca4-123">Поскольку hello расширения для настройки требуемого состояния Azure ВМ выполняется асинхронно, tootrack действия ход его выполнения или устранения неполадок приведены в hello [ **адаптации виртуальной машины Azure, устранение неполадок** ](#troubleshooting-azure-virtual-machine-onboarding)разделе ниже.</span><span class="sxs-lookup"><span data-stu-id="77ca4-123">Since hello Azure VM Desired State Configuration extension runs asynchronously, steps tootrack its progress or troubleshoot it are provided in hello [**Troubleshooting Azure virtual machine onboarding**](#troubleshooting-azure-virtual-machine-onboarding) section below.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="77ca4-124">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="77ca4-124">Azure portal</span></span>

<span data-ttu-id="77ca4-125">В hello [портал Azure](http://portal.azure.com/), нажмите кнопку **Обзор** -> **виртуальные машины (классические)**.</span><span class="sxs-lookup"><span data-stu-id="77ca4-125">In hello [Azure portal](http://portal.azure.com/), click **Browse** -> **Virtual machines (classic)**.</span></span> <span data-ttu-id="77ca4-126">Выберите, требуется tooonboard виртуальной Машины Windows hello.</span><span class="sxs-lookup"><span data-stu-id="77ca4-126">Select hello Windows VM you want tooonboard.</span></span> <span data-ttu-id="77ca4-127">На панели мониторинга виртуальной машины hello щелкните **все параметры** -> **расширения** -> **добавить**  ->   **Служба автоматизации Azure DSC** -> **создания**.</span><span class="sxs-lookup"><span data-stu-id="77ca4-127">On hello virtual machine's dashboard blade, click **All settings** -> **Extensions** -> **Add** -> **Azure Automation DSC** -> **Create**.</span></span> <span data-ttu-id="77ca4-128">Введите hello [значения локального диспетчера конфигураций DSC PowerShell](https://msdn.microsoft.com/powershell/dsc/metaconfig4) требуется для вашей учетной записи автоматизации регистрационный ключ и URL-адрес регистрации и при необходимости toohello tooassign конфигурации узла виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="77ca4-128">Enter hello [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) required for your use case, your Automation account's registration key and registration URL, and optionally a node configuration tooassign toohello VM.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_1.png)

<span data-ttu-id="77ca4-129">URL-адрес регистрации toofind hello и ключа для машины hello tooonboard учетной записи автоматизации hello, см. раздел hello [ **Secure регистрации** ](#secure-registration) разделе ниже.</span><span class="sxs-lookup"><span data-stu-id="77ca4-129">toofind hello registration URL and key for hello Automation account tooonboard hello machine to, see hello [**Secure registration**](#secure-registration) section below.</span></span>

### <a name="powershell"></a><span data-ttu-id="77ca4-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="77ca4-130">PowerShell</span></span>

```powershell
# log in tooboth Azure Service Management and Azure Resource Manager
Add-AzureAccount
Add-AzureRmAccount

# fill in correct values for your VM/Automation account here
$VMName = ""
$ServiceName = ""
$AutomationAccountName = ""
$AutomationAccountResourceGroup = ""

# fill in hello name of a Node Configuration in Azure Automation DSC, for this VM tooconform to
$NodeConfigName = ""

# get Azure Automation DSC registration info
$Account = Get-AzureRmAutomationAccount -ResourceGroupName $AutomationAccountResourceGroup -Name $AutomationAccountName
$RegistrationInfo = $Account | Get-AzureRmAutomationRegistrationInfo

# use hello DSC extension tooonboard hello VM for management with Azure Automation DSC
$VM = Get-AzureVM -Name $VMName -ServiceName $ServiceName

$PublicConfiguration = ConvertTo-Json -Depth 8 @{
    SasToken = ""
    ModulesUrl = "https://eus2oaasibizamarketprod1.blob.core.windows.net/automationdscpreview/RegistrationMetaConfigV2.zip"
    ConfigurationFunction = "RegistrationMetaConfigV2.ps1\RegistrationMetaConfigV2"

# update these PowerShell DSC Local Configuration Manager defaults if they do not match your use case.
# See https://technet.microsoft.com/library/dn249922.aspx?f=255&MSPPError=-2147217396 for more details
    Properties = @{
    RegistrationKey = @{
        UserName = 'notused'
        Password = 'PrivateSettingsRef:RegistrationKey'
    }
    RegistrationUrl = $RegistrationInfo.Endpoint
    NodeConfigurationName = $NodeConfigName
    ConfigurationMode = "ApplyAndMonitor"
    ConfigurationModeFrequencyMins = 15
    RefreshFrequencyMins = 30
    RebootNodeIfNeeded = $False
    ActionAfterReboot = "ContinueConfiguration"
    AllowModuleOverwrite = $False
    }
}

$PrivateConfiguration = ConvertTo-Json -Depth 8 @{
    Items = @{
        RegistrationKey = $RegistrationInfo.PrimaryKey
    }
}

$VM = Set-AzureVMExtension `
    -VM $vm `
    -Publisher Microsoft.Powershell `
    -ExtensionName DSC `
    -Version 2.19 `
    -PublicConfiguration $PublicConfiguration `
    -PrivateConfiguration $PrivateConfiguration `
    -ForceUpdate

$VM | Update-AzureVM
```

## <a name="azure-virtual-machines"></a><span data-ttu-id="77ca4-131">Виртуальные машины Azure</span><span class="sxs-lookup"><span data-stu-id="77ca4-131">Azure virtual machines</span></span>

<span data-ttu-id="77ca4-132">Azure Automation DSC позволяет легко присоединять виртуальные машины, Azure для управления конфигурацией с помощью портала Azure hello, шаблоны Azure Resource Manager или PowerShell.</span><span class="sxs-lookup"><span data-stu-id="77ca4-132">Azure Automation DSC lets you easily onboard Azure virtual machines for configuration management, using either hello Azure portal, Azure Resource Manager templates, or PowerShell.</span></span> <span data-ttu-id="77ca4-133">Кулисами hello и без администратор, имеющий tooremote в hello ВМ hello расширения для настройки требуемого состояния Azure VM регистрирует hello виртуальной Машины Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="77ca4-133">Under hello hood, and without an administrator having tooremote into hello VM, hello Azure VM Desired State Configuration extension registers hello VM with Azure Automation DSC.</span></span> <span data-ttu-id="77ca4-134">Поскольку hello расширения для настройки требуемого состояния Azure ВМ выполняется асинхронно, tootrack действия ход его выполнения или устранения неполадок приведены в hello [ **адаптации виртуальной машины Azure, устранение неполадок** ](#troubleshooting-azure-virtual-machine-onboarding)разделе ниже.</span><span class="sxs-lookup"><span data-stu-id="77ca4-134">Since hello Azure VM Desired State Configuration extension runs asynchronously, steps tootrack its progress or troubleshoot it are provided in hello [**Troubleshooting Azure virtual machine onboarding**](#troubleshooting-azure-virtual-machine-onboarding) section below.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="77ca4-135">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="77ca4-135">Azure portal</span></span>

<span data-ttu-id="77ca4-136">В hello [портал Azure](https://portal.azure.com/), перейдите toohello учетной записи службы автоматизации Azure место tooonboard виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="77ca4-136">In hello [Azure portal](https://portal.azure.com/), navigate toohello Azure Automation account where you want tooonboard virtual machines.</span></span> <span data-ttu-id="77ca4-137">Щелкните панель мониторинга учетной записи автоматизации hello **узлы DSC** -> **добавить виртуальную Машину Azure**.</span><span class="sxs-lookup"><span data-stu-id="77ca4-137">On hello Automation account dashboard, click **DSC Nodes** -> **Add Azure VM**.</span></span>

<span data-ttu-id="77ca4-138">В разделе **выберите виртуальные машины tooonboard**, выберите один или несколько на виртуальные машины Azure tooonboard.</span><span class="sxs-lookup"><span data-stu-id="77ca4-138">Under **Select virtual machines tooonboard**, select one or more Azure virtual machines tooonboard.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_2.png)

<span data-ttu-id="77ca4-139">В разделе **Настройка регистрационные данные**, введите hello [значения локального диспетчера конфигураций DSC PowerShell](https://msdn.microsoft.com/powershell/dsc/metaconfig4) необходимые для вашего случая использования и при необходимости toohello tooassign конфигурации узла виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="77ca4-139">Under **Configure registration data**, enter hello [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) required for your use case, and optionally a node configuration tooassign toohello VM.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_3.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="77ca4-140">Шаблоны диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="77ca4-140">Azure Resource Manager templates</span></span>

<span data-ttu-id="77ca4-141">Можно развернуть виртуальные машины Azure и tooAzure выставленных DSC службы автоматизации через шаблоны Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="77ca4-141">Azure virtual machines can be deployed and onboarded tooAzure Automation DSC via Azure Resource Manager templates.</span></span> <span data-ttu-id="77ca4-142">В разделе [Настройка виртуальной Машины через расширение DSC и Azure Automation DSC](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/) для шаблона, onboards tooAzure существующих виртуальных Машин DSC службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="77ca4-142">See [Configure a VM via DSC extension and Azure Automation DSC](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/) for an example template that onboards an existing VM tooAzure Automation DSC.</span></span> <span data-ttu-id="77ca4-143">toofind hello ключ и регистрации URL-адрес регистрации выполнены как входные данные в этом шаблоне см hello [ **Secure регистрации** ](#secure-registration) разделе ниже.</span><span class="sxs-lookup"><span data-stu-id="77ca4-143">toofind hello registration key and registration URL taken as input in this template, see hello [**Secure registration**](#secure-registration) section below.</span></span>

### <a name="powershell"></a><span data-ttu-id="77ca4-144">PowerShell</span><span class="sxs-lookup"><span data-stu-id="77ca4-144">PowerShell</span></span>

<span data-ttu-id="77ca4-145">Hello [AzureRmAutomationDscNode регистра](/powershell/module/azurerm.automation/register-azurermautomationdscnode) командлет можно использовать tooonboard виртуальных машин в hello портал Azure с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="77ca4-145">hello [Register-AzureRmAutomationDscNode](/powershell/module/azurerm.automation/register-azurermautomationdscnode) cmdlet can be used tooonboard virtual machines in hello Azure portal via PowerShell.</span></span>

## <a name="amazon-web-services-aws-virtual-machines"></a><span data-ttu-id="77ca4-146">виртуальные машины Amazon Web Services (AWS);</span><span class="sxs-lookup"><span data-stu-id="77ca4-146">Amazon Web Services (AWS) virtual machines</span></span>

<span data-ttu-id="77ca4-147">Вы можете легко присоединяться Amazon Web Services виртуальных машин для управления конфигурацией с DSC службы автоматизации Azure с помощью hello AWS DSC Toolkit.</span><span class="sxs-lookup"><span data-stu-id="77ca4-147">You can easily onboard Amazon Web Services virtual machines for configuration management by Azure Automation DSC using hello AWS DSC Toolkit.</span></span> <span data-ttu-id="77ca4-148">Дополнительные сведения о hello toolkit [здесь](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/).</span><span class="sxs-lookup"><span data-stu-id="77ca4-148">You can learn more about hello toolkit [here](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/).</span></span>

## <a name="physicalvirtual-windows-machines-on-premises-or-in-a-cloud-other-than-azureaws"></a><span data-ttu-id="77ca4-149">физические или виртуальные машины под управлением Windows, расположенные локально или в облачной службе, отличной от Azure или AWS;</span><span class="sxs-lookup"><span data-stu-id="77ca4-149">Physical/virtual Windows machines on-premises, or in a cloud other than Azure/AWS</span></span>

<span data-ttu-id="77ca4-150">Локальные компьютеры Windows и Windows машин в облаках без использования Azure (например, веб-службы Amazon) также могут tooAzure выставленных DSC службы автоматизации, при условии, что они имеют toohello исходящий доступ к Интернету, через несколько простых шагов:</span><span class="sxs-lookup"><span data-stu-id="77ca4-150">On-premises Windows machines and Windows machines in non-Azure clouds (such as Amazon Web Services) can also be onboarded tooAzure Automation DSC, as long as they have outbound access toohello internet, via a few simple steps:</span></span>

1. <span data-ttu-id="77ca4-151">Убедитесь, что hello последнюю версию [WMF 5](http://aka.ms/wmf5latest) устанавливается на компьютерах hello требуется tooonboard tooAzure DSC службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="77ca4-151">Make sure hello latest version of [WMF 5](http://aka.ms/wmf5latest) is installed on hello machines you want tooonboard tooAzure Automation DSC.</span></span>
2. <span data-ttu-id="77ca4-152">Следуйте приведенным инструкциям раздела hello [ **метаконфигурации создания DSC** ](#generating-dsc-metaconfigurations) ниже toogenerate папку, содержащую hello необходимости метаконфигурации DSC.</span><span class="sxs-lookup"><span data-stu-id="77ca4-152">Follow hello directions in section [**Generating DSC metaconfigurations**](#generating-dsc-metaconfigurations) below toogenerate a folder containing hello needed DSC metaconfigurations.</span></span>
3. <span data-ttu-id="77ca4-153">Удаленно применяются требуется tooonboard toohello машины hello PowerShell DSC метаконфигурации.</span><span class="sxs-lookup"><span data-stu-id="77ca4-153">Remotely apply hello PowerShell DSC metaconfiguration toohello machines you want tooonboard.</span></span> <span data-ttu-id="77ca4-154">**компьютер Hello, эта команда выполняется из должен иметь hello последнюю версию [WMF 5](http://aka.ms/wmf5latest) установлен**:</span><span class="sxs-lookup"><span data-stu-id="77ca4-154">**hello machine this command is run from must have hello latest version of [WMF 5](http://aka.ms/wmf5latest) installed**:</span></span>

    ```powershell
    Set-DscLocalConfigurationManager -Path C:\Users\joe\Desktop\DscMetaConfigs -ComputerName MyServer1, MyServer2
    ```

4. <span data-ttu-id="77ca4-155">Если не удается применить метаконфигурации PowerShell DSC hello удаленно, скопируйте папку метаконфигурации hello из шага 2 на каждой машине tooonboard.</span><span class="sxs-lookup"><span data-stu-id="77ca4-155">If you cannot apply hello PowerShell DSC metaconfigurations remotely, copy hello metaconfigurations folder from step 2 onto each machine tooonboard.</span></span> <span data-ttu-id="77ca4-156">Затем вызовите **Set-DscLocalConfigurationManager** локально на каждой машине tooonboard.</span><span class="sxs-lookup"><span data-stu-id="77ca4-156">Then call **Set-DscLocalConfigurationManager** locally on each machine tooonboard.</span></span>
5. <span data-ttu-id="77ca4-157">С помощью hello портал Azure или командлетов, убедитесь, что hello машины tooonboard теперь отображаются как узлы DSC зарегистрирован в вашей учетной записи службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="77ca4-157">Using hello Azure portal or cmdlets, check that hello machines tooonboard now show up as DSC nodes registered in your Azure Automation account.</span></span>

## <a name="physicalvirtual-linux-machines-on-premises-in-azure-or-in-a-cloud-other-than-azure"></a><span data-ttu-id="77ca4-158">Физические или виртуальные машины под управлением Linux, расположенные локально, в Azure или облачной службе, отличной от Azure.</span><span class="sxs-lookup"><span data-stu-id="77ca4-158">Physical/virtual Linux machines on-premises, in Azure, or in a cloud other than Azure</span></span>

<span data-ttu-id="77ca4-159">Компьютеры Linux локальных машин Linux в Azure, и компьютеры Linux в облаках без использования Azure также может быть встроен tooAzure DSC службы автоматизации, при условии, что они имеют toohello исходящий доступ к Интернету, через несколько простых шагов:</span><span class="sxs-lookup"><span data-stu-id="77ca4-159">On-premises Linux machines, Linux machines in Azure, and Linux machines in non-Azure clouds can also be onboarded tooAzure Automation DSC, as long as they have outbound access toohello internet, via a few simple steps:</span></span>

1. <span data-ttu-id="77ca4-160">Убедитесь, что hello последнюю версию [настройки требуемого состояния PowerShell для Linux](https://github.com/Microsoft/PowerShell-DSC-for-Linux) устанавливается на компьютерах hello требуется tooonboard tooAzure DSC службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="77ca4-160">Make sure hello latest version of [PowerShell Desired State Configuration for Linux](https://github.com/Microsoft/PowerShell-DSC-for-Linux) is installed on hello machines you want tooonboard tooAzure Automation DSC.</span></span>
2. <span data-ttu-id="77ca4-161">Если hello [значения по умолчанию локальный диспетчер конфигураций DSC PowerShell](https://msdn.microsoft.com/powershell/dsc/metaconfig4) соответствует вашей вариант использования, и требуется tooonboard машины, например, они **оба** по запросу из и отчетов tooAzure DSC службы автоматизации:</span><span class="sxs-lookup"><span data-stu-id="77ca4-161">If hello [PowerShell DSC Local Configuration Manager defaults](https://msdn.microsoft.com/powershell/dsc/metaconfig4) match your use case, and you want tooonboard machines such that they **both** pull from and report tooAzure Automation DSC:</span></span>

   + <span data-ttu-id="77ca4-162">На каждом Linux машины tooonboard tooAzure DSC службы автоматизации используйте tooonboard Register.py hello, который по умолчанию используется локальный диспетчер конфигураций DSC PowerShell с помощью:</span><span class="sxs-lookup"><span data-stu-id="77ca4-162">On each Linux machine tooonboard tooAzure Automation DSC, use Register.py tooonboard using hello PowerShell DSC Local Configuration Manager defaults:</span></span>

     `/opt/microsoft/dsc/Scripts/Register.py <Automation account registration key> <Automation account registration URL>`

   + <span data-ttu-id="77ca4-163">toofind hello регистрации ключа и регистрации URL-адрес для вашей учетной записи автоматизации в разделе hello [ **Secure регистрации** ](#secure-registration) разделе ниже.</span><span class="sxs-lookup"><span data-stu-id="77ca4-163">toofind hello registration key and registration URL for your Automation account, see hello [**Secure registration**](#secure-registration) section below.</span></span>

     <span data-ttu-id="77ca4-164">Если hello PowerShell DSC локальный диспетчер конфигураций по умолчанию **сделать** **не** соответствует вашей вариант использования, либо требуется tooonboard компьютеров таким образом, что они только о tooAzure DSC службы автоматизации, но не по запросу конфигурации и модули PowerShell, выполните шаги 3 – 6.</span><span class="sxs-lookup"><span data-stu-id="77ca4-164">If hello PowerShell DSC Local Configuration Manager defaults **do** **not** match your use case, or you want tooonboard machines such that they only report tooAzure Automation DSC, but do not pull configuration or PowerShell modules from it,  follow steps 3 - 6.</span></span> <span data-ttu-id="77ca4-165">В противном случае перейдите непосредственно toostep 6.</span><span class="sxs-lookup"><span data-stu-id="77ca4-165">Otherwise, proceed directly toostep 6.</span></span>

3. <span data-ttu-id="77ca4-166">Следуйте приведенным инструкциям hello hello [ **метаконфигурации создания DSC** ](#generating-dsc-metaconfigurations) ниже, в разделе toogenerate папку, содержащую необходимые hello DSC метаконфигурации.</span><span class="sxs-lookup"><span data-stu-id="77ca4-166">Follow hello directions in hello [**Generating DSC metaconfigurations**](#generating-dsc-metaconfigurations) section below toogenerate a folder containing hello needed DSC metaconfigurations.</span></span>
4. <span data-ttu-id="77ca4-167">Удаленно применяются требуется tooonboard toohello машины hello PowerShell DSC метаконфигурации.</span><span class="sxs-lookup"><span data-stu-id="77ca4-167">Remotely apply hello PowerShell DSC metaconfiguration toohello machines you want tooonboard:</span></span>

    ```powershell
    $SecurePass = ConvertTo-SecureString -String "<root password>" -AsPlainText -Force
    $Cred = New-Object System.Management.Automation.PSCredential "root", $SecurePass
    $Opt = New-CimSessionOption -UseSsl -SkipCACheck -SkipCNCheck -SkipRevocationCheck

    # need a CimSession for each Linux machine tooonboard

    $Session = New-CimSession -Credential $Cred -ComputerName <your Linux machine> -Port 5986 -Authentication basic -SessionOption $Opt

    Set-DscLocalConfigurationManager -CimSession $Session -Path C:\Users\joe\Desktop\DscMetaConfigs
    ```

<span data-ttu-id="77ca4-168">компьютер Hello, эта команда выполняется из должен иметь hello последнюю версию [WMF 5](http://aka.ms/wmf5latest) установлен.</span><span class="sxs-lookup"><span data-stu-id="77ca4-168">hello machine this command is run from must have hello latest version of [WMF 5](http://aka.ms/wmf5latest) installed.</span></span>

1. <span data-ttu-id="77ca4-169">Если не удается применить метаконфигурации PowerShell DSC hello удаленно, для каждого tooonboard машины Linux, скопируйте hello метаконфигурации соответствующая toothat машина из папки hello на шаге 5 на компьютере Linux hello.</span><span class="sxs-lookup"><span data-stu-id="77ca4-169">If you cannot apply hello PowerShell DSC metaconfigurations remotely, for each Linux machine tooonboard, copy hello metaconfiguration corresponding toothat machine from hello folder in step 5 onto hello Linux machine.</span></span> <span data-ttu-id="77ca4-170">Затем вызовите `SetDscLocalConfigurationManager.py` локально на каждом компьютере Linux требуется tooonboard tooAzure DSC службы автоматизации:</span><span class="sxs-lookup"><span data-stu-id="77ca4-170">Then call `SetDscLocalConfigurationManager.py` locally on each Linux machine you want tooonboard tooAzure Automation DSC:</span></span>

   `/opt/microsoft/dsc/Scripts/SetDscLocalConfigurationManager.py -configurationmof <path toometaconfiguration file>`

2. <span data-ttu-id="77ca4-171">С помощью hello портал Azure или командлетов, убедитесь, что hello машины tooonboard теперь отображаются как узлы DSC зарегистрирован в вашей учетной записи службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="77ca4-171">Using hello Azure portal or cmdlets, check that hello machines tooonboard now show up as DSC nodes registered in your Azure Automation account.</span></span>

## <a name="generating-dsc-metaconfigurations"></a><span data-ttu-id="77ca4-172">Создание метаконфигураций DSC</span><span class="sxs-lookup"><span data-stu-id="77ca4-172">Generating DSC metaconfigurations</span></span>

<span data-ttu-id="77ca4-173">toogenerically освоить любой компьютер tooAzure DSC службы автоматизации, [метаконфигурацию DSC](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) может быть создан, при применения, сообщает hello DSC агента на toopull машины hello из или получении отчета tooAzure DSC службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="77ca4-173">toogenerically onboard any machine tooAzure Automation DSC, a [DSC metaconfiguration](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) can be generated that, when applied, tells hello DSC agent on hello machine toopull from and/or report tooAzure Automation DSC.</span></span> <span data-ttu-id="77ca4-174">Метаконфигурации DSC для Azure Automation DSC может быть создан с помощью конфигурации PowerShell DSC или командлеты Azure Automation PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="77ca4-174">DSC metaconfigurations for Azure Automation DSC can be generated using either a PowerShell DSC configuration, or hello Azure Automation PowerShell cmdlets.</span></span>

> [!NOTE]
> <span data-ttu-id="77ca4-175">Метаконфигурации DSC содержат tooonboard hello необходимости секретные данные машина tooan учетной записи автоматизации для управления.</span><span class="sxs-lookup"><span data-stu-id="77ca4-175">DSC metaconfigurations contain hello secrets needed tooonboard a machine tooan Automation account for management.</span></span> <span data-ttu-id="77ca4-176">Убедитесь, что tooproperly защиты любого метаконфигурации DSC, создаваемые вами или удалить их после использования.</span><span class="sxs-lookup"><span data-stu-id="77ca4-176">Make sure tooproperly protect any DSC metaconfigurations you create, or delete them after use.</span></span>

### <a name="using-a-dsc-configuration"></a><span data-ttu-id="77ca4-177">Использование конфигурации DSC</span><span class="sxs-lookup"><span data-stu-id="77ca4-177">Using a DSC Configuration</span></span>

1. <span data-ttu-id="77ca4-178">Откройте hello интегрированной среды Сценариев PowerShell с правами администратора на компьютере в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="77ca4-178">Open hello PowerShell ISE as an administrator in a machine in your local environment.</span></span> <span data-ttu-id="77ca4-179">Hello компьютер должен иметь hello последнюю версию [WMF 5](http://aka.ms/wmf5latest) установлен.</span><span class="sxs-lookup"><span data-stu-id="77ca4-179">hello machine must have hello latest version of [WMF 5](http://aka.ms/wmf5latest) installed.</span></span>
2. <span data-ttu-id="77ca4-180">Скопируйте следующий скрипт локально hello.</span><span class="sxs-lookup"><span data-stu-id="77ca4-180">Copy hello following script locally.</span></span> <span data-ttu-id="77ca4-181">Этот скрипт содержит конфигурацию PowerShell DSC для создания метаконфигурации и команда tookick отключение создания метаконфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="77ca4-181">This script contains a PowerShell DSC configuration for creating metaconfigurations, and a command tookick off hello metaconfiguration creation.</span></span>

    ```powershell
    # hello DSC configuration that will generate metaconfigurations
    [DscLocalConfigurationManager()]
    Configuration DscMetaConfigs
    {

        param
        (
            [Parameter(Mandatory=$True)]
            [String]$RegistrationUrl,

            [Parameter(Mandatory=$True)]
            [String]$RegistrationKey,

            [Parameter(Mandatory=$True)]
            [String[]]$ComputerName,

            [Int]$RefreshFrequencyMins = 30,

            [Int]$ConfigurationModeFrequencyMins = 15,

            [String]$ConfigurationMode = "ApplyAndMonitor",

            [String]$NodeConfigurationName,

            [Boolean]$RebootNodeIfNeeded= $False,

            [String]$ActionAfterReboot = "ContinueConfiguration",

            [Boolean]$AllowModuleOverwrite = $False,

            [Boolean]$ReportOnly
        )

        if(!$NodeConfigurationName -or $NodeConfigurationName -eq "")
        {
            $ConfigurationNames = $null
        }
        else
        {
            $ConfigurationNames = @($NodeConfigurationName)
        }

        if($ReportOnly)
        {
        $RefreshMode = "PUSH"
        }
        else
        {
        $RefreshMode = "PULL"
        }

        Node $ComputerName
        {

            Settings
            {
                RefreshFrequencyMins = $RefreshFrequencyMins
                RefreshMode = $RefreshMode
                ConfigurationMode = $ConfigurationMode
                AllowModuleOverwrite = $AllowModuleOverwrite
                RebootNodeIfNeeded = $RebootNodeIfNeeded
                ActionAfterReboot = $ActionAfterReboot
                ConfigurationModeFrequencyMins = $ConfigurationModeFrequencyMins
            }

            if(!$ReportOnly)
            {
            ConfigurationRepositoryWeb AzureAutomationDSC
                {
                    ServerUrl = $RegistrationUrl
                    RegistrationKey = $RegistrationKey
                    ConfigurationNames = $ConfigurationNames
                }

                ResourceRepositoryWeb AzureAutomationDSC
                {
                ServerUrl = $RegistrationUrl
                RegistrationKey = $RegistrationKey
                }
            }

            ReportServerWeb AzureAutomationDSC
            {
                ServerUrl = $RegistrationUrl
                RegistrationKey = $RegistrationKey
            }
        }
    }

    # Create hello metaconfigurations
    # TODO: edit hello below as needed for your use case
    $Params = @{
        RegistrationUrl = '<fill me in>';
        RegistrationKey = '<fill me in>';
        ComputerName = @('<some VM tooonboard>', '<some other VM tooonboard>');
        NodeConfigurationName = 'SimpleConfig.webserver';
        RefreshFrequencyMins = 30;
        ConfigurationModeFrequencyMins = 15;
        RebootNodeIfNeeded = $False;
        AllowModuleOverwrite = $False;
        ConfigurationMode = 'ApplyAndMonitor';
        ActionAfterReboot = 'ContinueConfiguration';
        ReportOnly = $False;  # Set too$True toohave machines only report tooAA DSC but not pull from it
    }

    # Use PowerShell splatting toopass parameters toohello DSC configuration being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    DscMetaConfigs @Params
    ```

3. <span data-ttu-id="77ca4-182">Заполните hello регистрационный ключ и URL-адрес для учетной записи автоматизации, а также имена hello tooonboard машины hello.</span><span class="sxs-lookup"><span data-stu-id="77ca4-182">Fill in hello registration key and URL for your Automation account, as well as hello names of hello machines tooonboard.</span></span> <span data-ttu-id="77ca4-183">Все остальные параметры являются необязательными.</span><span class="sxs-lookup"><span data-stu-id="77ca4-183">All other parameters are optional.</span></span> <span data-ttu-id="77ca4-184">toofind hello регистрации ключа и регистрации URL-адрес для вашей учетной записи автоматизации в разделе hello [ **Secure регистрации** ](#secure-registration) разделе ниже.</span><span class="sxs-lookup"><span data-stu-id="77ca4-184">toofind hello registration key and registration URL for your Automation account, see hello [**Secure registration**](#secure-registration) section below.</span></span>
4. <span data-ttu-id="77ca4-185">Если требуется tooAzure hello машины tooreport DSC состояние сведения DSC службы автоматизации, но не по запросу, конфигурации и модули PowerShell, задайте hello **ReportOnly** tootrue параметра.</span><span class="sxs-lookup"><span data-stu-id="77ca4-185">If you want hello machines tooreport DSC status information tooAzure Automation DSC, but not pull configuration or PowerShell modules, set hello **ReportOnly** parameter tootrue.</span></span>
5. <span data-ttu-id="77ca4-186">Запустите сценарий hello.</span><span class="sxs-lookup"><span data-stu-id="77ca4-186">Run hello script.</span></span> <span data-ttu-id="77ca4-187">Вы создали папку с именем **DscMetaConfigs** в рабочий каталог, содержащий hello метаконфигурации PowerShell DSC для tooonboard машин hello (с правами администратора):</span><span class="sxs-lookup"><span data-stu-id="77ca4-187">You should now have a folder called **DscMetaConfigs** in your working directory, containing hello PowerShell DSC metaconfigurations for hello machines tooonboard (as an administrator):</span></span>

    ```powershell
    Set-DscLocalConfigurationManager -Path ./DscMetaConfigs
    ```

### <a name="using-hello-azure-automation-cmdlets"></a><span data-ttu-id="77ca4-188">С помощью командлетов службы автоматизации Azure hello</span><span class="sxs-lookup"><span data-stu-id="77ca4-188">Using hello Azure Automation cmdlets</span></span>

<span data-ttu-id="77ca4-189">Если значения по умолчанию hello локальный диспетчер конфигураций DSC PowerShell соответствует вашей вариант использования, и требуется tooonboard машин таким образом, что они извлекают из и сообщить tooAzure DSC службы автоматизации, командлеты автоматизации Azure hello предоставляют упрощенный метод создания hello DSC метаконфигурации при необходимости:</span><span class="sxs-lookup"><span data-stu-id="77ca4-189">If hello PowerShell DSC Local Configuration Manager defaults match your use case, and you want tooonboard machines such that they both pull from and report tooAzure Automation DSC, hello Azure Automation cmdlets provide a simplified method of generating hello DSC metaconfigurations needed:</span></span>

1. <span data-ttu-id="77ca4-190">Откройте консоль PowerShell hello или интегрированной среды Сценариев PowerShell с правами администратора на машине в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="77ca4-190">Open hello PowerShell console or PowerShell ISE as an administrator in a machine in your local environment.</span></span>
2. <span data-ttu-id="77ca4-191">Подключение с использованием диспетчера ресурсов tooAzure **добавить AzureRmAccount**</span><span class="sxs-lookup"><span data-stu-id="77ca4-191">Connect tooAzure Resource Manager using **Add-AzureRmAccount**</span></span>
3. <span data-ttu-id="77ca4-192">Загрузите PowerShell DSC метаконфигурации hello для машин hello требуется tooonboard из hello автоматизации учетной записи toowhich tooonboard узлах:</span><span class="sxs-lookup"><span data-stu-id="77ca4-192">Download hello PowerShell DSC metaconfigurations for hello machines you want tooonboard from hello Automation account toowhich you want tooonboard nodes:</span></span>

    ```powershell
    # Define hello parameters for Get-AzureRmAutomationDscOnboardingMetaconfig using PowerShell Splatting
    $Params = @{

        ResourceGroupName = 'ContosoResources'; # hello name of hello ARM Resource Group that contains your Azure Automation Account
        AutomationAccountName = 'ContosoAutomation'; # hello name of hello Azure Automation Account where you want a node on-boarded to
        ComputerName = @('web01', 'web02', 'sql01'); # hello names of hello computers that hello meta configuration will be generated for
        OutputFolder = "$env:UserProfile\Desktop\";
    }
    # Use PowerShell splatting toopass parameters toohello Azure Automation cmdlet being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    Get-AzureRmAutomationDscOnboardingMetaconfig @Params
    ```
    
4. <span data-ttu-id="77ca4-193">Вы создали папку с именем ***DscMetaConfigs***, содержащий hello метаконфигурации PowerShell DSC для tooonboard машин hello (с правами администратора):</span><span class="sxs-lookup"><span data-stu-id="77ca4-193">You should now have a folder called ***DscMetaConfigs***, containing hello PowerShell DSC metaconfigurations for hello machines tooonboard (as an administrator):</span></span>
    
    ```powershell
    Set-DscLocalConfigurationManager -Path $env:UserProfile\Desktop\DscMetaConfigs
    ```

## <a name="secure-registration"></a><span data-ttu-id="77ca4-194">Безопасная регистрация</span><span class="sxs-lookup"><span data-stu-id="77ca4-194">Secure registration</span></span>

<span data-ttu-id="77ca4-195">Машины могут безопасно подключить tooan учетной записи службы автоматизации Azure через протокол регистрации hello WMF 5 DSC, что позволяет узел tooauthenticate tooa PowerShell DSC V2 по запросу или службу отчетов сервера DSC (включая Azure Automation DSC).</span><span class="sxs-lookup"><span data-stu-id="77ca4-195">Machines can securely onboard tooan Azure Automation account through hello WMF 5 DSC registration protocol, which allows a DSC node tooauthenticate tooa PowerShell DSC V2 Pull or Reporting server (including Azure Automation DSC).</span></span> <span data-ttu-id="77ca4-196">Hello узел регистрируется сервер toohello **URL-адрес регистрации**, выполняющего проверку подлинности с помощью **регистрационный ключ**.</span><span class="sxs-lookup"><span data-stu-id="77ca4-196">hello node registers toohello server at a **Registration URL**, authenticating using a **Registration key**.</span></span> <span data-ttu-id="77ca4-197">Во время регистрации узла hello DSC и сервере запросу DSC-формирования отчетов согласовывать уникальный сертификат для этого узла toouse для проверки подлинности toohello сервера после регистрации.</span><span class="sxs-lookup"><span data-stu-id="77ca4-197">During registration, hello DSC node and DSC Pull/Reporting server negotiate a unique certificate for this node toouse for authentication toohello server post-registration.</span></span> <span data-ttu-id="77ca4-198">Этот процесс исключает возможность подмены подключенных узлов друг другом, например, если один из узлов взломан и является вредоносным.</span><span class="sxs-lookup"><span data-stu-id="77ca4-198">This process prevents onboarded nodes from impersonating one another, such as if a node is compromised and behaving maliciously.</span></span> <span data-ttu-id="77ca4-199">После регистрации hello регистрационный ключ не используется для проверки подлинности еще раз и удаляется из узла "hello".</span><span class="sxs-lookup"><span data-stu-id="77ca4-199">After registration, hello Registration key is not used for authentication again, and is deleted from hello node.</span></span>

<span data-ttu-id="77ca4-200">Можно получить hello сведения, необходимые для протокола регистрации hello DSC из hello **управление ключами** колонку на портале Azure предварительной версии hello.</span><span class="sxs-lookup"><span data-stu-id="77ca4-200">You can get hello information required for hello DSC registration protocol from hello **Manage Keys** blade in hello Azure preview portal.</span></span> <span data-ttu-id="77ca4-201">Откройте эту колонку, щелкнув значок ключа hello для hello **Essentials** панель для hello учетной записи автоматизации.</span><span class="sxs-lookup"><span data-stu-id="77ca4-201">Open this blade by clicking hello key icon on hello **Essentials** panel for hello Automation account.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_4.png)

* <span data-ttu-id="77ca4-202">URL-адрес регистрации — поле URL-адрес hello в колонке hello управление ключами.</span><span class="sxs-lookup"><span data-stu-id="77ca4-202">Registration URL is hello URL field in hello Manage Keys blade.</span></span>
* <span data-ttu-id="77ca4-203">Ключ регистрации — hello первичный ключ доступа или вторичный ключ доступа в колонке hello управление ключами.</span><span class="sxs-lookup"><span data-stu-id="77ca4-203">Registration key is hello Primary Access Key or Secondary Access Key in hello Manage Keys blade.</span></span> <span data-ttu-id="77ca4-204">Можно использовать любой из этих ключей.</span><span class="sxs-lookup"><span data-stu-id="77ca4-204">Either key can be used.</span></span>

<span data-ttu-id="77ca4-205">Для повышения безопасности могут быть повторно созданы hello первичный и вторичный ключи доступа учетной записи автоматизации в любое время (в hello **управление ключами** колонку) tooprevent регистраций будущих узла, с помощью предыдущих ключей.</span><span class="sxs-lookup"><span data-stu-id="77ca4-205">For added security, hello primary and secondary access keys of an Automation account can be regenerated at any time (on hello **Manage Keys** blade) tooprevent future node registrations using previous keys.</span></span>

## <a name="troubleshooting-azure-virtual-machine-onboarding"></a><span data-ttu-id="77ca4-206">Устранение неполадок при подключении виртуальной машины Azure</span><span class="sxs-lookup"><span data-stu-id="77ca4-206">Troubleshooting Azure virtual machine onboarding</span></span>

<span data-ttu-id="77ca4-207">Служба Azure Automation DSC позволяет легко подключать виртуальные машины Microsoft Azure для управления конфигурациями.</span><span class="sxs-lookup"><span data-stu-id="77ca4-207">Azure Automation DSC lets you easily onboard Azure Windows VMs for configuration management.</span></span> <span data-ttu-id="77ca4-208">Механизме hello hello расширения для настройки требуемого состояния Azure виртуальной Машины — используется tooregister hello виртуальной Машины с помощью DSC службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="77ca4-208">Under hello hood, hello Azure VM Desired State Configuration extension is used tooregister hello VM with Azure Automation DSC.</span></span> <span data-ttu-id="77ca4-209">Поскольку hello расширения для настройки требуемого состояния Azure ВМ выполняется асинхронно, отслеживания хода его выполнения и устранение неполадок выполнения могут быть важны.</span><span class="sxs-lookup"><span data-stu-id="77ca4-209">Since hello Azure VM Desired State Configuration extension runs asynchronously, tracking its progress and troubleshooting its execution may be important.</span></span>

> [!NOTE]
> <span data-ttu-id="77ca4-210">Любой метод адаптации tooAzure виртуальной Машины Windows Azure Automation DSC, использующего расширения настройки требуемого состояния Azure VM hello может занять час tooan tooshow узел hello вверх, зарегистрированного в службе автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="77ca4-210">Any method of onboarding an Azure Windows VM tooAzure Automation DSC that uses hello Azure VM Desired State Configuration extension could take up tooan hour for hello node tooshow up as registered in Azure Automation.</span></span> <span data-ttu-id="77ca4-211">Это происходит из-за установки Windows Management Framework 5.0 toohello на hello ВМ путем расширения Azure VM DSC hello, которое является обязательным tooonboard hello ВМ tooAzure DSC службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="77ca4-211">This is due toohello installation of Windows Management Framework 5.0 on hello VM by hello Azure VM DSC extension, which is required tooonboard hello VM tooAzure Automation DSC.</span></span>

<span data-ttu-id="77ca4-212">tootroubleshoot или представление состояния hello hello расширение настройки требуемого состояния Azure VM hello портал Azure перейдите toohello, выставленных виртуальной Машины, затем щелкните -> **все параметры** -> **расширения**   ->  **DSC**.</span><span class="sxs-lookup"><span data-stu-id="77ca4-212">tootroubleshoot or view hello status of hello Azure VM Desired State Configuration extension, in hello Azure portal navigate toohello VM being onboarded, then click -> **All settings** -> **Extensions** -> **DSC**.</span></span> <span data-ttu-id="77ca4-213">Для получения дополнительных сведений щелкните **Просмотреть подробные сведения о состоянии**.</span><span class="sxs-lookup"><span data-stu-id="77ca4-213">For more details, you can click **View detailed status**.</span></span>

[![](./media/automation-dsc-onboarding/DSC_Onboarding_5.png)](https://technet.microsoft.com/library/dn249912.aspx)

## <a name="certificate-expiration-and-reregistration"></a><span data-ttu-id="77ca4-214">Истечение срока действия сертификата и повторная регистрация</span><span class="sxs-lookup"><span data-stu-id="77ca4-214">Certificate expiration and reregistration</span></span>

<span data-ttu-id="77ca4-215">После регистрации компьютера в качестве узла DSC в Azure Automation DSC, существует ряд причин, почему может потребоваться tooreregister этого узла в hello будущих:</span><span class="sxs-lookup"><span data-stu-id="77ca4-215">After registering a machine as a DSC node in Azure Automation DSC, there are a number of reasons why you may need tooreregister that node in hello future:</span></span>

* <span data-ttu-id="77ca4-216">После регистрации каждый узел автоматически согласовывает уникальный сертификат для проверки подлинности, срок действия которого составляет один год.</span><span class="sxs-lookup"><span data-stu-id="77ca4-216">After registering, each node automatically negotiates a unique certificate for authentication that expires after one year.</span></span> <span data-ttu-id="77ca4-217">В настоящее время hello протокола регистрации PowerShell DSC не удается обновить автоматически сертификаты при они скоро истекает срок действия, требуется tooreregister hello узлы после времени года.</span><span class="sxs-lookup"><span data-stu-id="77ca4-217">Currently, hello PowerShell DSC registration protocol cannot automatically renew certificates when they are nearing expiration, so you need tooreregister hello nodes after a year's time.</span></span> <span data-ttu-id="77ca4-218">Перед повторной регистрацией убедитесь, что на каждом узле работает Windows Management Framework 5.0 RTM.</span><span class="sxs-lookup"><span data-stu-id="77ca4-218">Before reregistering, ensure that each node is running Windows Management Framework 5.0 RTM.</span></span> <span data-ttu-id="77ca4-219">Если истечения срока действия сертификата проверки подлинности узла и узла hello не зарегистрирован, hello узел будет невозможно toocommunicate в службе автоматизации Azure и будут помечены «Неотвечающим.»</span><span class="sxs-lookup"><span data-stu-id="77ca4-219">If a node's authentication certificate expires, and hello node is not reregistered, hello node will be unable toocommunicate with Azure Automation and will be marked 'Unresponsive.'</span></span> <span data-ttu-id="77ca4-220">Перерегистрация выполняется через 90 дней или меньше с момента истечения срока действия сертификата hello, или в любой момент после времени окончания срока действия сертификата hello, приведет к формируются и использовать новый сертификат.</span><span class="sxs-lookup"><span data-stu-id="77ca4-220">Reregistration performed 90 days or less from hello certificate expiration time, or at any point after hello certificate expiration time, will result in a new certificate being generated and used.</span></span>
* <span data-ttu-id="77ca4-221">toochange любой [значения локального диспетчера конфигураций DSC PowerShell](https://msdn.microsoft.com/powershell/dsc/metaconfig4) , заданные во время первоначальной регистрации hello узел, например ConfigurationMode.</span><span class="sxs-lookup"><span data-stu-id="77ca4-221">toochange any [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) that were set during initial registration of hello node, such as ConfigurationMode.</span></span> <span data-ttu-id="77ca4-222">Сейчас эти значения агента DSC можно изменить только в ходе повторной регистрации.</span><span class="sxs-lookup"><span data-stu-id="77ca4-222">Currently, these DSC agent values can only be changed through reregistration.</span></span> <span data-ttu-id="77ca4-223">Единственным исключением Hello hello конфигурации, назначенной toohello узел — это можно изменить в Azure Automation DSC непосредственно.</span><span class="sxs-lookup"><span data-stu-id="77ca4-223">hello one exception is hello Node Configuration assigned toohello node -- this can be changed in Azure Automation DSC directly.</span></span>

<span data-ttu-id="77ca4-224">Перерегистрация могут выполняться в hello так же, как вы зарегистрировали hello узел изначально одним из способов адаптации hello, описанные в этом документе.</span><span class="sxs-lookup"><span data-stu-id="77ca4-224">Reregistration can be performed in hello same way you registered hello node initially, using any of hello onboarding methods described in this document.</span></span> <span data-ttu-id="77ca4-225">Прежде чем зарегистрировать его не обязательно toounregister узла из DSC службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="77ca4-225">You do not need toounregister a node from Azure Automation DSC before reregistering it.</span></span>

## <a name="related-articles"></a><span data-ttu-id="77ca4-226">Связанные статьи</span><span class="sxs-lookup"><span data-stu-id="77ca4-226">Related Articles</span></span>

* [<span data-ttu-id="77ca4-227">Обзор Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="77ca4-227">Azure Automation DSC overview</span></span>](automation-dsc-overview.md)
* [<span data-ttu-id="77ca4-228">Командлеты Automation DSC Azure</span><span class="sxs-lookup"><span data-stu-id="77ca4-228">Azure Automation DSC cmdlets</span></span>](/powershell/module/azurerm.automation/#automation)
* [<span data-ttu-id="77ca4-229">Цены на Automation DSC Azure</span><span class="sxs-lookup"><span data-stu-id="77ca4-229">Azure Automation DSC pricing</span></span>](https://azure.microsoft.com/pricing/details/automation/)
