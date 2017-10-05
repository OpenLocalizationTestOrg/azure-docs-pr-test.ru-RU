---
title: "Подключение компьютеров для управления с помощью Azure Automation DSC | Документация Майкрософт"
description: "Настройка машин для управления с помощью Azure Automation DSC"
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
ms.openlocfilehash: cc9b1ea19b4e17374d47e12f970cb333a8051559
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="onboarding-machines-for-management-by-azure-automation-dsc"></a><span data-ttu-id="fe465-103">Подключение компьютеров для управления с помощью Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="fe465-103">Onboarding machines for management by Azure Automation DSC</span></span>

## <a name="why-manage-machines-with-azure-automation-dsc"></a><span data-ttu-id="fe465-104">В чем преимущества управления компьютерами с помощью службы Azure Automation DSC?</span><span class="sxs-lookup"><span data-stu-id="fe465-104">Why manage machines with Azure Automation DSC?</span></span>

<span data-ttu-id="fe465-105">Настройка требуемого состояния (DSC) с помощью службы автоматизации Azure так же проста, как и [настройка требуемого состояния с использованием PowerShell](https://technet.microsoft.com/library/dn249912.aspx). Это мощная служба управления конфигурациями для узлов DSC (физических и виртуальных машин), которую можно использовать в любом облачном или локальном центре обработки данных.</span><span class="sxs-lookup"><span data-stu-id="fe465-105">Like [PowerShell Desired State Configuration](https://technet.microsoft.com/library/dn249912.aspx), Azure Automation Desired State Configuration is a simple, yet powerful, configuration management service for DSC nodes (physical and virtual machines) in any cloud or on-premises datacenter.</span></span> <span data-ttu-id="fe465-106">Она обеспечивает быструю и простую масштабируемость тысяч компьютеров из безопасного центрального расположения.</span><span class="sxs-lookup"><span data-stu-id="fe465-106">It enables scalability across thousands of machines quickly and easily from a central, secure location.</span></span> <span data-ttu-id="fe465-107">Вы можете легко переносить компьютеры в облачную среду, присваивать им декларативные конфигурации, а также просматривать отчеты, отражающие соответствие каждого компьютера требуемому состоянию.</span><span class="sxs-lookup"><span data-stu-id="fe465-107">You can easily onboard machines, assign them declarative configurations, and view reports showing each machine's compliance to the desired state you specified.</span></span> <span data-ttu-id="fe465-108">Слой управления Azure Automation DSC используется для настройки требуемого состояния таким же образом, как слой управления службы автоматизации Azure используется в сценариях PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fe465-108">The Azure Automation DSC management layer is to DSC what the Azure Automation management layer is to PowerShell scripting.</span></span> <span data-ttu-id="fe465-109">Другими словами, служба автоматизации Azure помогает управлять сценариями PowerShell так же, как и конфигурациями DSC.</span><span class="sxs-lookup"><span data-stu-id="fe465-109">In other words, in the same way that Azure Automation helps you manage PowerShell scripts, it also helps you manage DSC configurations.</span></span> <span data-ttu-id="fe465-110">Дополнительные сведения о преимуществах использования DSC службы автоматизации Azure см. в статье [Обзор DSC службы автоматизации Azure](automation-dsc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fe465-110">To learn more about the benefits of using Azure Automation DSC, see [Azure Automation DSC overview](automation-dsc-overview.md).</span></span>

<span data-ttu-id="fe465-111">Службу Azure Automation DSC можно использовать для управления разными компьютерами. Их типы перечислены ниже.</span><span class="sxs-lookup"><span data-stu-id="fe465-111">Azure Automation DSC can be used to manage a variety of machines:</span></span>

* <span data-ttu-id="fe465-112">Виртуальные машины Azure (классические).</span><span class="sxs-lookup"><span data-stu-id="fe465-112">Azure virtual machines (classic)</span></span>
* <span data-ttu-id="fe465-113">Виртуальные машины Azure</span><span class="sxs-lookup"><span data-stu-id="fe465-113">Azure virtual machines</span></span>
* <span data-ttu-id="fe465-114">виртуальные машины Amazon Web Services (AWS);</span><span class="sxs-lookup"><span data-stu-id="fe465-114">Amazon Web Services (AWS) virtual machines</span></span>
* <span data-ttu-id="fe465-115">физические или виртуальные машины под управлением Windows, расположенные локально или в облачной службе, отличной от Azure или AWS;</span><span class="sxs-lookup"><span data-stu-id="fe465-115">Physical/virtual Windows machines on-premises, or in a cloud other than Azure/AWS</span></span>
* <span data-ttu-id="fe465-116">Физические или виртуальные машины под управлением Linux, расположенные локально, в Azure или облачной службе, отличной от Azure.</span><span class="sxs-lookup"><span data-stu-id="fe465-116">Physical/virtual Linux machines on-premises, in Azure, or in a cloud other than Azure</span></span>

<span data-ttu-id="fe465-117">Кроме того, если вы не готовы управлять конфигурацией компьютера из облака, платформа Azure Automation DSC может также использоваться как конечная точка только для отчетности.</span><span class="sxs-lookup"><span data-stu-id="fe465-117">In addition, if you are not ready to manage machine configuration from the cloud, Azure Automation DSC can also be used as a report-only endpoint.</span></span> <span data-ttu-id="fe465-118">Это позволяет задать (отправить) требуемую конфигурацию через DSC локально и просмотреть подробные сведения отчетов о соответствии узла требуемому состоянию в службе автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="fe465-118">This allows you to set (push) desired configuration through DSC on-premises and view rich reporting details on node compliance with the desired state in Azure Automation.</span></span>

<span data-ttu-id="fe465-119">В следующих разделах описываются способы подключения каждого типа компьютеров к службе Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="fe465-119">The following sections outline how you can onboard each type of machine to Azure Automation DSC.</span></span>

## <a name="azure-virtual-machines-classic"></a><span data-ttu-id="fe465-120">Виртуальные машины Azure (классические).</span><span class="sxs-lookup"><span data-stu-id="fe465-120">Azure virtual machines (classic)</span></span>

<span data-ttu-id="fe465-121">Служба Azure Automation DSC позволяет легко подключать виртуальные машины Azure (классические) для управления их настройками с помощью портала Azure или PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fe465-121">With Azure Automation DSC, you can easily onboard Azure virtual machines (classic) for configuration management using either the Azure portal, or PowerShell.</span></span> <span data-ttu-id="fe465-122">В процессе работы расширение DSC регистрирует виртуальную машину в службе Azure Automation DSC, исключая необходимость выполнения удаленного входа на виртуальную машину администратором.</span><span class="sxs-lookup"><span data-stu-id="fe465-122">Under the hood, and without an administrator having to remote into the VM, the Azure VM Desired State Configuration extension registers the VM with Azure Automation DSC.</span></span> <span data-ttu-id="fe465-123">Так как с виртуальными машинами Azure расширение DSC работает асинхронно, можно воспользоваться алгоритмом отслеживания хода выполнения и устранения неполадок, который приведен ниже в разделе [**Устранение неполадок при подключении виртуальной машины Azure**](#troubleshooting-azure-virtual-machine-onboarding) .</span><span class="sxs-lookup"><span data-stu-id="fe465-123">Since the Azure VM Desired State Configuration extension runs asynchronously, steps to track its progress or troubleshoot it are provided in the [**Troubleshooting Azure virtual machine onboarding**](#troubleshooting-azure-virtual-machine-onboarding) section below.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="fe465-124">портале Azure</span><span class="sxs-lookup"><span data-stu-id="fe465-124">Azure portal</span></span>

<span data-ttu-id="fe465-125">На [портале Azure](http://portal.azure.com/) последовательно выберите **Обзор** -> **Виртуальные машины (классика)**.</span><span class="sxs-lookup"><span data-stu-id="fe465-125">In the [Azure portal](http://portal.azure.com/), click **Browse** -> **Virtual machines (classic)**.</span></span> <span data-ttu-id="fe465-126">Выберите виртуальную машину Windows, которую необходимо подключить.</span><span class="sxs-lookup"><span data-stu-id="fe465-126">Select the Windows VM you want to onboard.</span></span> <span data-ttu-id="fe465-127">В колонке панели мониторинга виртуальной машины щелкните **Все параметры** -> **Расширения** -> **Добавить** -> **Azure Automation DSC** -> **Создать**.</span><span class="sxs-lookup"><span data-stu-id="fe465-127">On the virtual machine's dashboard blade, click **All settings** -> **Extensions** -> **Add** -> **Azure Automation DSC** -> **Create**.</span></span> <span data-ttu-id="fe465-128">Введите необходимые [значения локального диспетчера конфигураций DSC PowerShell](https://msdn.microsoft.com/powershell/dsc/metaconfig4), регистрационный ключ вашей учетной записи и URL-адрес регистрации. Кроме того, можно ввести конфигурацию узла, которая будет назначена виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="fe465-128">Enter the [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) required for your use case, your Automation account's registration key and registration URL, and optionally a node configuration to assign to the VM.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_1.png)

<span data-ttu-id="fe465-129">Сведения о поиске URL-адреса регистрации и ключа учетной записи службы автоматизации для подключения компьютера см. ниже в разделе [**Безопасная регистрация**](#secure-registration).</span><span class="sxs-lookup"><span data-stu-id="fe465-129">To find the registration URL and key for the Automation account to onboard the machine to, see the [**Secure registration**](#secure-registration) section below.</span></span>

### <a name="powershell"></a><span data-ttu-id="fe465-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fe465-130">PowerShell</span></span>

```powershell
# log in to both Azure Service Management and Azure Resource Manager
Add-AzureAccount
Add-AzureRmAccount

# fill in correct values for your VM/Automation account here
$VMName = ""
$ServiceName = ""
$AutomationAccountName = ""
$AutomationAccountResourceGroup = ""

# fill in the name of a Node Configuration in Azure Automation DSC, for this VM to conform to
$NodeConfigName = ""

# get Azure Automation DSC registration info
$Account = Get-AzureRmAutomationAccount -ResourceGroupName $AutomationAccountResourceGroup -Name $AutomationAccountName
$RegistrationInfo = $Account | Get-AzureRmAutomationRegistrationInfo

# use the DSC extension to onboard the VM for management with Azure Automation DSC
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

## <a name="azure-virtual-machines"></a><span data-ttu-id="fe465-131">Виртуальные машины Azure</span><span class="sxs-lookup"><span data-stu-id="fe465-131">Azure virtual machines</span></span>

<span data-ttu-id="fe465-132">Служба Azure Automation DSC позволяет легко подключать виртуальные машины Azure для управления конфигурацией с помощью портала Azure, шаблонов диспетчера ресурсов Azure или PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fe465-132">Azure Automation DSC lets you easily onboard Azure virtual machines for configuration management, using either the Azure portal, Azure Resource Manager templates, or PowerShell.</span></span> <span data-ttu-id="fe465-133">В процессе работы расширение DSC регистрирует виртуальную машину в службе Azure Automation DSC, исключая необходимость выполнения удаленного входа на виртуальную машину администратором.</span><span class="sxs-lookup"><span data-stu-id="fe465-133">Under the hood, and without an administrator having to remote into the VM, the Azure VM Desired State Configuration extension registers the VM with Azure Automation DSC.</span></span> <span data-ttu-id="fe465-134">Так как с виртуальными машинами Azure расширение DSC работает асинхронно, можно воспользоваться алгоритмом отслеживания хода выполнения и устранения неполадок, который приведен ниже в разделе [**Устранение неполадок при подключении виртуальной машины Azure**](#troubleshooting-azure-virtual-machine-onboarding) .</span><span class="sxs-lookup"><span data-stu-id="fe465-134">Since the Azure VM Desired State Configuration extension runs asynchronously, steps to track its progress or troubleshoot it are provided in the [**Troubleshooting Azure virtual machine onboarding**](#troubleshooting-azure-virtual-machine-onboarding) section below.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="fe465-135">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="fe465-135">Azure portal</span></span>

<span data-ttu-id="fe465-136">На [портале Azure](https://portal.azure.com/)перейдите к учетной записи службы автоматизации Azure, чтобы подключить виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="fe465-136">In the [Azure portal](https://portal.azure.com/), navigate to the Azure Automation account where you want to onboard virtual machines.</span></span> <span data-ttu-id="fe465-137">На панели мониторинга учетной записи службы автоматизации щелкните **Узлы DSC** -> **Добавить виртуальную машину Azure**.</span><span class="sxs-lookup"><span data-stu-id="fe465-137">On the Automation account dashboard, click **DSC Nodes** -> **Add Azure VM**.</span></span>

<span data-ttu-id="fe465-138">На странице **Выбор виртуальных машин для подключения**выберите одну или несколько виртуальных машин Azure для подключения.</span><span class="sxs-lookup"><span data-stu-id="fe465-138">Under **Select virtual machines to onboard**, select one or more Azure virtual machines to onboard.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_2.png)

<span data-ttu-id="fe465-139">В разделе **Настроить данные регистрации** введите необходимые вам [значения локального диспетчера конфигураций DSC PowerShell](https://msdn.microsoft.com/powershell/dsc/metaconfig4). Также можно ввести конфигурацию узла, которая будет назначена виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="fe465-139">Under **Configure registration data**, enter the [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) required for your use case, and optionally a node configuration to assign to the VM.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_3.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="fe465-140">Шаблоны диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="fe465-140">Azure Resource Manager templates</span></span>

<span data-ttu-id="fe465-141">Виртуальные машины Azure можно разворачивать и подключать к службе Azure Automation DSC с помощью шаблонов диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="fe465-141">Azure virtual machines can be deployed and onboarded to Azure Automation DSC via Azure Resource Manager templates.</span></span> <span data-ttu-id="fe465-142">Пример шаблона, подключающего существующую виртуальную машину к службе автоматизации Azure DSC, см. в статье [Configure a VM via DSC extension and Azure Automation DSC](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/) (Настройка виртуальной машины с помощью расширения DSC и Azure Automation DSC).</span><span class="sxs-lookup"><span data-stu-id="fe465-142">See [Configure a VM via DSC extension and Azure Automation DSC](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/) for an example template that onboards an existing VM to Azure Automation DSC.</span></span> <span data-ttu-id="fe465-143">Расположение ключа и URL-адреса регистрации, которые шаблон принимает в качестве входных данных, см. ниже в разделе [**Безопасная регистрация**](#secure-registration).</span><span class="sxs-lookup"><span data-stu-id="fe465-143">To find the registration key and registration URL taken as input in this template, see the [**Secure registration**](#secure-registration) section below.</span></span>

### <a name="powershell"></a><span data-ttu-id="fe465-144">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fe465-144">PowerShell</span></span>

<span data-ttu-id="fe465-145">На портале Azure виртуальные машины можно подключать с помощью командлета [Register-AzureRmAutomationDscNode](/powershell/module/azurerm.automation/register-azurermautomationdscnode) в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fe465-145">The [Register-AzureRmAutomationDscNode](/powershell/module/azurerm.automation/register-azurermautomationdscnode) cmdlet can be used to onboard virtual machines in the Azure portal via PowerShell.</span></span>

## <a name="amazon-web-services-aws-virtual-machines"></a><span data-ttu-id="fe465-146">виртуальные машины Amazon Web Services (AWS);</span><span class="sxs-lookup"><span data-stu-id="fe465-146">Amazon Web Services (AWS) virtual machines</span></span>

<span data-ttu-id="fe465-147">Вы можете легко подключить виртуальные машины Amazon Web Services для управления конфигурацией с помощью Azure Automation DSC, используя набор инструментов DSC AWS.</span><span class="sxs-lookup"><span data-stu-id="fe465-147">You can easily onboard Amazon Web Services virtual machines for configuration management by Azure Automation DSC using the AWS DSC Toolkit.</span></span> <span data-ttu-id="fe465-148">Дополнительные сведения об этом наборе инструментов см. [здесь](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/).</span><span class="sxs-lookup"><span data-stu-id="fe465-148">You can learn more about the toolkit [here](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/).</span></span>

## <a name="physicalvirtual-windows-machines-on-premises-or-in-a-cloud-other-than-azureaws"></a><span data-ttu-id="fe465-149">физические или виртуальные машины под управлением Windows, расположенные локально или в облачной службе, отличной от Azure или AWS;</span><span class="sxs-lookup"><span data-stu-id="fe465-149">Physical/virtual Windows machines on-premises, or in a cloud other than Azure/AWS</span></span>

<span data-ttu-id="fe465-150">Компьютеры под управлением Windows, расположенные локально или в облачных службах, отличных от Azure (например, в веб-службах Amazon), также можно подключить к службе Azure Automation DSC при наличии на них исходящего доступа к Интернету. Для этого требуется выполнить несколько простых шагов.</span><span class="sxs-lookup"><span data-stu-id="fe465-150">On-premises Windows machines and Windows machines in non-Azure clouds (such as Amazon Web Services) can also be onboarded to Azure Automation DSC, as long as they have outbound access to the internet, via a few simple steps:</span></span>

1. <span data-ttu-id="fe465-151">Убедитесь, что на компьютерах, которые будут подключены к службе автоматизации Azure DSC, установлена последняя версия [WMF 5](http://aka.ms/wmf5latest) .</span><span class="sxs-lookup"><span data-stu-id="fe465-151">Make sure the latest version of [WMF 5](http://aka.ms/wmf5latest) is installed on the machines you want to onboard to Azure Automation DSC.</span></span>
2. <span data-ttu-id="fe465-152">Создайте папку с необходимыми метаконфигурациями DSC, как указано ниже в разделе [**Создание метаконфигураций DSC**](#generating-dsc-metaconfigurations) .</span><span class="sxs-lookup"><span data-stu-id="fe465-152">Follow the directions in section [**Generating DSC metaconfigurations**](#generating-dsc-metaconfigurations) below to generate a folder containing the needed DSC metaconfigurations.</span></span>
3. <span data-ttu-id="fe465-153">Удаленно примените метаконфигурации PowerShell DSC на компьютерах, которые нужно подключить.</span><span class="sxs-lookup"><span data-stu-id="fe465-153">Remotely apply the PowerShell DSC metaconfiguration to the machines you want to onboard.</span></span> <span data-ttu-id="fe465-154">**Для выполнения этой команды на компьютере должна быть установлена последняя версия [WMF 5](http://aka.ms/wmf5latest)**.</span><span class="sxs-lookup"><span data-stu-id="fe465-154">**The machine this command is run from must have the latest version of [WMF 5](http://aka.ms/wmf5latest) installed**:</span></span>

    ```powershell
    Set-DscLocalConfigurationManager -Path C:\Users\joe\Desktop\DscMetaConfigs -ComputerName MyServer1, MyServer2
    ```

4. <span data-ttu-id="fe465-155">Если метаконфигурации PowerShell DSC не удалось применить удаленно, скопируйте папку метаконфигураций (см. шаг 2) на каждый компьютер, который нужно подключить.</span><span class="sxs-lookup"><span data-stu-id="fe465-155">If you cannot apply the PowerShell DSC metaconfigurations remotely, copy the metaconfigurations folder from step 2 onto each machine to onboard.</span></span> <span data-ttu-id="fe465-156">Затем локально вызовите **Set-DscLocalConfigurationManager** на каждом компьютере, который нужно подключить.</span><span class="sxs-lookup"><span data-stu-id="fe465-156">Then call **Set-DscLocalConfigurationManager** locally on each machine to onboard.</span></span>
5. <span data-ttu-id="fe465-157">С помощью портала Azure или командлетов убедитесь, что все компьютеры, которые нужно подключить, теперь отображаются как узлы DSC, зарегистрированные в вашей учетной записи службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="fe465-157">Using the Azure portal or cmdlets, check that the machines to onboard now show up as DSC nodes registered in your Azure Automation account.</span></span>

## <a name="physicalvirtual-linux-machines-on-premises-in-azure-or-in-a-cloud-other-than-azure"></a><span data-ttu-id="fe465-158">Физические или виртуальные машины под управлением Linux, расположенные локально, в Azure или облачной службе, отличной от Azure.</span><span class="sxs-lookup"><span data-stu-id="fe465-158">Physical/virtual Linux machines on-premises, in Azure, or in a cloud other than Azure</span></span>

<span data-ttu-id="fe465-159">Компьютеры под управлением Linux, расположенные локально, в Azure или в облачной службе, отличной от Azure, также можно подключить к службе автоматизации Azure DSC при наличии на них исходящего доступа к Интернету. Для этого требуется выполнить несколько простых шагов.</span><span class="sxs-lookup"><span data-stu-id="fe465-159">On-premises Linux machines, Linux machines in Azure, and Linux machines in non-Azure clouds can also be onboarded to Azure Automation DSC, as long as they have outbound access to the internet, via a few simple steps:</span></span>

1. <span data-ttu-id="fe465-160">Убедитесь, что на компьютерах, которые будут подключены к службе Azure Automation DSC, установлена последняя версия платформы[PowerShell Desired State Configuration для Linux](https://github.com/Microsoft/PowerShell-DSC-for-Linux).</span><span class="sxs-lookup"><span data-stu-id="fe465-160">Make sure the latest version of [PowerShell Desired State Configuration for Linux](https://github.com/Microsoft/PowerShell-DSC-for-Linux) is installed on the machines you want to onboard to Azure Automation DSC.</span></span>
2. <span data-ttu-id="fe465-161">Если [значения по умолчанию локального диспетчера конфигураций PowerShell DSC](https://msdn.microsoft.com/powershell/dsc/metaconfig4) соответствуют требуемым, а подключаемые компьютеры должны извлекать данные из Azure Automation DSC **и** передавать их туда, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="fe465-161">If the [PowerShell DSC Local Configuration Manager defaults](https://msdn.microsoft.com/powershell/dsc/metaconfig4) match your use case, and you want to onboard machines such that they **both** pull from and report to Azure Automation DSC:</span></span>

   + <span data-ttu-id="fe465-162">На каждом компьютере под управлением Linux, который будет подключен к службе Azure Automation DSC, используйте файл Register.py для подключения с помощью значений по умолчанию локального диспетчера конфигураций DSC PowerShell:</span><span class="sxs-lookup"><span data-stu-id="fe465-162">On each Linux machine to onboard to Azure Automation DSC, use Register.py to onboard using the PowerShell DSC Local Configuration Manager defaults:</span></span>

     `/opt/microsoft/dsc/Scripts/Register.py <Automation account registration key> <Automation account registration URL>`

   + <span data-ttu-id="fe465-163">Расположение ключа и URL-адреса регистрации для учетной записи службы автоматизации см. ниже в разделе [**Безопасная регистрация**](#secure-registration).</span><span class="sxs-lookup"><span data-stu-id="fe465-163">To find the registration key and registration URL for your Automation account, see the [**Secure registration**](#secure-registration) section below.</span></span>

     <span data-ttu-id="fe465-164">Если значения по умолчанию локального диспетчера конфигураций PowerShell DSC **не** **соответствуют** требуемым или подключаемые компьютеры должны подчиняться службе Azure Automation DSC, но не извлекать из нее параметры конфигурации или модули PowerShell, то выполните шаги 3–6.</span><span class="sxs-lookup"><span data-stu-id="fe465-164">If the PowerShell DSC Local Configuration Manager defaults **do** **not** match your use case, or you want to onboard machines such that they only report to Azure Automation DSC, but do not pull configuration or PowerShell modules from it,  follow steps 3 - 6.</span></span> <span data-ttu-id="fe465-165">В противном случае сразу перейдите к шагу 6.</span><span class="sxs-lookup"><span data-stu-id="fe465-165">Otherwise, proceed directly to step 6.</span></span>

3. <span data-ttu-id="fe465-166">Создайте папку с необходимыми метаконфигурациями DSC, как указано ниже в разделе [**Создание метаконфигураций DSC**](#generating-dsc-metaconfigurations) .</span><span class="sxs-lookup"><span data-stu-id="fe465-166">Follow the directions in the [**Generating DSC metaconfigurations**](#generating-dsc-metaconfigurations) section below to generate a folder containing the needed DSC metaconfigurations.</span></span>
4. <span data-ttu-id="fe465-167">Удаленно примените метаконфигурации PowerShell DSC на компьютерах, которые нужно подключить:</span><span class="sxs-lookup"><span data-stu-id="fe465-167">Remotely apply the PowerShell DSC metaconfiguration to the machines you want to onboard:</span></span>

    ```powershell
    $SecurePass = ConvertTo-SecureString -String "<root password>" -AsPlainText -Force
    $Cred = New-Object System.Management.Automation.PSCredential "root", $SecurePass
    $Opt = New-CimSessionOption -UseSsl -SkipCACheck -SkipCNCheck -SkipRevocationCheck

    # need a CimSession for each Linux machine to onboard

    $Session = New-CimSession -Credential $Cred -ComputerName <your Linux machine> -Port 5986 -Authentication basic -SessionOption $Opt

    Set-DscLocalConfigurationManager -CimSession $Session -Path C:\Users\joe\Desktop\DscMetaConfigs
    ```

<span data-ttu-id="fe465-168">Для выполнения этой команды на компьютере должна быть установлена последняя версия [WMF 5](http://aka.ms/wmf5latest) .</span><span class="sxs-lookup"><span data-stu-id="fe465-168">The machine this command is run from must have the latest version of [WMF 5](http://aka.ms/wmf5latest) installed.</span></span>

1. <span data-ttu-id="fe465-169">Если не удалось применить метаконфигурации PowerShell DSC удаленно, скопируйте соответствующую метаконфигурацию из папки (шаг 5) на каждый компьютер под управлением Linux, который нужно подключить.</span><span class="sxs-lookup"><span data-stu-id="fe465-169">If you cannot apply the PowerShell DSC metaconfigurations remotely, for each Linux machine to onboard, copy the metaconfiguration corresponding to that machine from the folder in step 5 onto the Linux machine.</span></span> <span data-ttu-id="fe465-170">Затем вызовите `SetDscLocalConfigurationManager.py` локально на каждом компьютере под управлением Linux, который нужно подключить к службе автоматизации Azure DSC:</span><span class="sxs-lookup"><span data-stu-id="fe465-170">Then call `SetDscLocalConfigurationManager.py` locally on each Linux machine you want to onboard to Azure Automation DSC:</span></span>

   `/opt/microsoft/dsc/Scripts/SetDscLocalConfigurationManager.py -configurationmof <path to metaconfiguration file>`

2. <span data-ttu-id="fe465-171">С помощью портала Azure или командлетов убедитесь, что все компьютеры, которые нужно подключить, теперь отображаются как узлы DSC, зарегистрированные в вашей учетной записи службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="fe465-171">Using the Azure portal or cmdlets, check that the machines to onboard now show up as DSC nodes registered in your Azure Automation account.</span></span>

## <a name="generating-dsc-metaconfigurations"></a><span data-ttu-id="fe465-172">Создание метаконфигураций DSC</span><span class="sxs-lookup"><span data-stu-id="fe465-172">Generating DSC metaconfigurations</span></span>

<span data-ttu-id="fe465-173">Для универсального внедрения любого компьютера в службу автоматизации Azure DSC можно создать [метаконфигурацию DSC](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig), при использовании которой агент DSC на соответствующем компьютере будет настроен на извлечение данных из службы автоматизации Azure и (или) передачу в эту службу отчетов.</span><span class="sxs-lookup"><span data-stu-id="fe465-173">To generically onboard any machine to Azure Automation DSC, a [DSC metaconfiguration](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) can be generated that, when applied, tells the DSC agent on the machine to pull from and/or report to Azure Automation DSC.</span></span> <span data-ttu-id="fe465-174">Метаконфигурации DSC для службы автоматизации Azure DSC можно создавать, используя либо конфигурацию PowerShell DSC, либо командлеты PowerShell в службе автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="fe465-174">DSC metaconfigurations for Azure Automation DSC can be generated using either a PowerShell DSC configuration, or the Azure Automation PowerShell cmdlets.</span></span>

> [!NOTE]
> <span data-ttu-id="fe465-175">Метаконфигурации DSC содержат секретные данные, необходимые при подключении компьютера к учетной записи службы автоматизации для управления.</span><span class="sxs-lookup"><span data-stu-id="fe465-175">DSC metaconfigurations contain the secrets needed to onboard a machine to an Automation account for management.</span></span> <span data-ttu-id="fe465-176">Обеспечьте должную защиту создаваемых метаконфигураций или удаляйте их сразу после использования.</span><span class="sxs-lookup"><span data-stu-id="fe465-176">Make sure to properly protect any DSC metaconfigurations you create, or delete them after use.</span></span>

### <a name="using-a-dsc-configuration"></a><span data-ttu-id="fe465-177">Использование конфигурации DSC</span><span class="sxs-lookup"><span data-stu-id="fe465-177">Using a DSC Configuration</span></span>

1. <span data-ttu-id="fe465-178">Запустите на компьютере, входящем в локальную среду, консоль PowerShell ISE от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="fe465-178">Open the PowerShell ISE as an administrator in a machine in your local environment.</span></span> <span data-ttu-id="fe465-179">На этом компьютере должна быть установлена последняя версия [WMF 5](http://aka.ms/wmf5latest) .</span><span class="sxs-lookup"><span data-stu-id="fe465-179">The machine must have the latest version of [WMF 5](http://aka.ms/wmf5latest) installed.</span></span>
2. <span data-ttu-id="fe465-180">Локально выполните следующий скрипт.</span><span class="sxs-lookup"><span data-stu-id="fe465-180">Copy the following script locally.</span></span> <span data-ttu-id="fe465-181">Этот сценарий содержит конфигурацию PowerShell DSC для создания метаконфигураций и команду, запускающую этот процесс.</span><span class="sxs-lookup"><span data-stu-id="fe465-181">This script contains a PowerShell DSC configuration for creating metaconfigurations, and a command to kick off the metaconfiguration creation.</span></span>

    ```powershell
    # The DSC configuration that will generate metaconfigurations
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

    # Create the metaconfigurations
    # TODO: edit the below as needed for your use case
    $Params = @{
        RegistrationUrl = '<fill me in>';
        RegistrationKey = '<fill me in>';
        ComputerName = @('<some VM to onboard>', '<some other VM to onboard>');
        NodeConfigurationName = 'SimpleConfig.webserver';
        RefreshFrequencyMins = 30;
        ConfigurationModeFrequencyMins = 15;
        RebootNodeIfNeeded = $False;
        AllowModuleOverwrite = $False;
        ConfigurationMode = 'ApplyAndMonitor';
        ActionAfterReboot = 'ContinueConfiguration';
        ReportOnly = $False;  # Set to $True to have machines only report to AA DSC but not pull from it
    }

    # Use PowerShell splatting to pass parameters to the DSC configuration being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    DscMetaConfigs @Params
    ```

3. <span data-ttu-id="fe465-182">Введите регистрационный ключ и URL-адрес для учетной записи автоматизации, а также имена виртуальных машин, которые необходимо внедрить.</span><span class="sxs-lookup"><span data-stu-id="fe465-182">Fill in the registration key and URL for your Automation account, as well as the names of the machines to onboard.</span></span> <span data-ttu-id="fe465-183">Все остальные параметры являются необязательными.</span><span class="sxs-lookup"><span data-stu-id="fe465-183">All other parameters are optional.</span></span> <span data-ttu-id="fe465-184">Расположение ключа и URL-адреса регистрации для учетной записи службы автоматизации см. ниже в разделе [**Безопасная регистрация**](#secure-registration).</span><span class="sxs-lookup"><span data-stu-id="fe465-184">To find the registration key and registration URL for your Automation account, see the [**Secure registration**](#secure-registration) section below.</span></span>
4. <span data-ttu-id="fe465-185">Если вы хотите, чтобы компьютеры передавали сведения о состоянии DSC в службу Azure Automation DSC, не извлекая конфигурацию или модули PowerShell, установите для параметра **ReportOnly** значение Тrue.</span><span class="sxs-lookup"><span data-stu-id="fe465-185">If you want the machines to report DSC status information to Azure Automation DSC, but not pull configuration or PowerShell modules, set the **ReportOnly** parameter to true.</span></span>
5. <span data-ttu-id="fe465-186">Выполните скрипт.</span><span class="sxs-lookup"><span data-stu-id="fe465-186">Run the script.</span></span> <span data-ttu-id="fe465-187">В рабочем каталоге появится папка **DscMetaConfigs**, содержащая метаконфигурации PowerShell DSC для подключаемых компьютеров (в качестве администратора):</span><span class="sxs-lookup"><span data-stu-id="fe465-187">You should now have a folder called **DscMetaConfigs** in your working directory, containing the PowerShell DSC metaconfigurations for the machines to onboard (as an administrator):</span></span>

    ```powershell
    Set-DscLocalConfigurationManager -Path ./DscMetaConfigs
    ```

### <a name="using-the-azure-automation-cmdlets"></a><span data-ttu-id="fe465-188">Использование командлетов службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="fe465-188">Using the Azure Automation cmdlets</span></span>

<span data-ttu-id="fe465-189">Если значения по умолчанию локального диспетчера конфигураций DSC PowerShell соответствуют требуемым и вы хотите внедрить компьютеры таким образом, чтобы позволить им извлекать данные из службы автоматизации Azure DSC и передавать в эту службу отчеты, легко создать необходимые конфигурации DSC позволят командлеты службы автоматизации Azure:</span><span class="sxs-lookup"><span data-stu-id="fe465-189">If the PowerShell DSC Local Configuration Manager defaults match your use case, and you want to onboard machines such that they both pull from and report to Azure Automation DSC, the Azure Automation cmdlets provide a simplified method of generating the DSC metaconfigurations needed:</span></span>

1. <span data-ttu-id="fe465-190">Запустите на компьютере, входящем в локальную среду, консоль PowerShell или PowerShell ISE от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="fe465-190">Open the PowerShell console or PowerShell ISE as an administrator in a machine in your local environment.</span></span>
2. <span data-ttu-id="fe465-191">Подключитесь к Azure Resource Manager с помощью командлета **Add-AzureRmAccount**</span><span class="sxs-lookup"><span data-stu-id="fe465-191">Connect to Azure Resource Manager using **Add-AzureRmAccount**</span></span>
3. <span data-ttu-id="fe465-192">Из учетной записи службы автоматизации, к которой будут подключены узлы, загрузите метаконфигурации DSC PowerShell для подключаемых компьютеров:</span><span class="sxs-lookup"><span data-stu-id="fe465-192">Download the PowerShell DSC metaconfigurations for the machines you want to onboard from the Automation account to which you want to onboard nodes:</span></span>

    ```powershell
    # Define the parameters for Get-AzureRmAutomationDscOnboardingMetaconfig using PowerShell Splatting
    $Params = @{

        ResourceGroupName = 'ContosoResources'; # The name of the ARM Resource Group that contains your Azure Automation Account
        AutomationAccountName = 'ContosoAutomation'; # The name of the Azure Automation Account where you want a node on-boarded to
        ComputerName = @('web01', 'web02', 'sql01'); # The names of the computers that the meta configuration will be generated for
        OutputFolder = "$env:UserProfile\Desktop\";
    }
    # Use PowerShell splatting to pass parameters to the Azure Automation cmdlet being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    Get-AzureRmAutomationDscOnboardingMetaconfig @Params
    ```
    
4. <span data-ttu-id="fe465-193">В рабочем каталоге появится папка ***DscMetaConfigs***, содержащая метаконфигурации PowerShell DSC для подключаемых компьютеров (в качестве администратора):</span><span class="sxs-lookup"><span data-stu-id="fe465-193">You should now have a folder called ***DscMetaConfigs***, containing the PowerShell DSC metaconfigurations for the machines to onboard (as an administrator):</span></span>
    
    ```powershell
    Set-DscLocalConfigurationManager -Path $env:UserProfile\Desktop\DscMetaConfigs
    ```

## <a name="secure-registration"></a><span data-ttu-id="fe465-194">Безопасная регистрация</span><span class="sxs-lookup"><span data-stu-id="fe465-194">Secure registration</span></span>

<span data-ttu-id="fe465-195">Компьютеры можно безопасно подключать к учетной записи службы автоматизации Azure с помощью протокола регистрации DSC WMF 5. Этот протокол позволяет узлу DSC проходить проверку подлинности на сервере отчетов или опрашивающем сервере PowerShell DSC V2 (включая Azure Automation DSC).</span><span class="sxs-lookup"><span data-stu-id="fe465-195">Machines can securely onboard to an Azure Automation account through the WMF 5 DSC registration protocol, which allows a DSC node to authenticate to a PowerShell DSC V2 Pull or Reporting server (including Azure Automation DSC).</span></span> <span data-ttu-id="fe465-196">Узел регистрируется на сервере с использованием **URL-адреса регистрации**, проходя аутентификацию с помощью **Регистрационного ключа**.</span><span class="sxs-lookup"><span data-stu-id="fe465-196">The node registers to the server at a **Registration URL**, authenticating using a **Registration key**.</span></span> <span data-ttu-id="fe465-197">Во время регистрации узел DSC и сервер отчетов или опрашивающий сервер DSC создают для этого узла уникальный сертификат, который будет использоваться для проверки подлинности после регистрации на сервере.</span><span class="sxs-lookup"><span data-stu-id="fe465-197">During registration, the DSC node and DSC Pull/Reporting server negotiate a unique certificate for this node to use for authentication to the server post-registration.</span></span> <span data-ttu-id="fe465-198">Этот процесс исключает возможность подмены подключенных узлов друг другом, например, если один из узлов взломан и является вредоносным.</span><span class="sxs-lookup"><span data-stu-id="fe465-198">This process prevents onboarded nodes from impersonating one another, such as if a node is compromised and behaving maliciously.</span></span> <span data-ttu-id="fe465-199">После регистрации регистрационный ключ повторно не используется для проверки подлинности и удаляется из узла.</span><span class="sxs-lookup"><span data-stu-id="fe465-199">After registration, the Registration key is not used for authentication again, and is deleted from the node.</span></span>

<span data-ttu-id="fe465-200">Данные, необходимые для протокола регистрации DSC, можно найти в колонке **Управление ключами** на портале предварительной версии Azure.</span><span class="sxs-lookup"><span data-stu-id="fe465-200">You can get the information required for the DSC registration protocol from the **Manage Keys** blade in the Azure preview portal.</span></span> <span data-ttu-id="fe465-201">Откройте эту колонку, щелкнув значок ключа на панели **Основные компоненты** в учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="fe465-201">Open this blade by clicking the key icon on the **Essentials** panel for the Automation account.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_4.png)

* <span data-ttu-id="fe465-202">«Регистрационный URL-адрес» — это поле «URL-адрес» в колонке «Управление ключами».</span><span class="sxs-lookup"><span data-stu-id="fe465-202">Registration URL is the URL field in the Manage Keys blade.</span></span>
* <span data-ttu-id="fe465-203">Регистрационный ключ — это поле «Первичный ключ доступа» или «Вторичный ключ доступа» в колонке «Управление ключами».</span><span class="sxs-lookup"><span data-stu-id="fe465-203">Registration key is the Primary Access Key or Secondary Access Key in the Manage Keys blade.</span></span> <span data-ttu-id="fe465-204">Можно использовать любой из этих ключей.</span><span class="sxs-lookup"><span data-stu-id="fe465-204">Either key can be used.</span></span>

<span data-ttu-id="fe465-205">Для повышения безопасности первичный и вторичный ключи доступа учетной записи службы автоматизации можно создавать повторно в любое время (в колонке **Управление ключами**). Это исключает возможность регистрации узла с помощью ранее использованных ключей.</span><span class="sxs-lookup"><span data-stu-id="fe465-205">For added security, the primary and secondary access keys of an Automation account can be regenerated at any time (on the **Manage Keys** blade) to prevent future node registrations using previous keys.</span></span>

## <a name="troubleshooting-azure-virtual-machine-onboarding"></a><span data-ttu-id="fe465-206">Устранение неполадок при подключении виртуальной машины Azure</span><span class="sxs-lookup"><span data-stu-id="fe465-206">Troubleshooting Azure virtual machine onboarding</span></span>

<span data-ttu-id="fe465-207">Служба Azure Automation DSC позволяет легко подключать виртуальные машины Microsoft Azure для управления конфигурациями.</span><span class="sxs-lookup"><span data-stu-id="fe465-207">Azure Automation DSC lets you easily onboard Azure Windows VMs for configuration management.</span></span> <span data-ttu-id="fe465-208">Расширение DSC для виртуальных машин Azure используется для регистрации виртуальных машин в службе Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="fe465-208">Under the hood, the Azure VM Desired State Configuration extension is used to register the VM with Azure Automation DSC.</span></span> <span data-ttu-id="fe465-209">Так как с виртуальными машинами Azure расширение DSC работает асинхронно, важно отслеживать ход выполнения и устранять неполадки.</span><span class="sxs-lookup"><span data-stu-id="fe465-209">Since the Azure VM Desired State Configuration extension runs asynchronously, tracking its progress and troubleshooting its execution may be important.</span></span>

> [!NOTE]
> <span data-ttu-id="fe465-210">Независимо от способа подключения виртуальной машины Microsoft Azure к службе Azure Automation DSC с расширением DSC для виртуальных машин Azure, узел будет отображаться как зарегистрированный в службе автоматизации Azure приблизительно через час.</span><span class="sxs-lookup"><span data-stu-id="fe465-210">Any method of onboarding an Azure Windows VM to Azure Automation DSC that uses the Azure VM Desired State Configuration extension could take up to an hour for the node to show up as registered in Azure Automation.</span></span> <span data-ttu-id="fe465-211">Это связано с тем, что расширение DSC для виртуальных машин Azure устанавливает на виртуальную машину платформу Windows Management Framework 5.0, которая требуется для размещения этой виртуальной машины в DSC службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="fe465-211">This is due to the installation of Windows Management Framework 5.0 on the VM by the Azure VM DSC extension, which is required to onboard the VM to Azure Automation DSC.</span></span>

<span data-ttu-id="fe465-212">Чтобы устранить неполадки или просмотреть состояние расширения DSC для виртуальных машин Azure, на портале Azure перейдите к подключаемой виртуальной машине и последовательно выберите **Все параметры** -> **Расширения** -> **DSC**.</span><span class="sxs-lookup"><span data-stu-id="fe465-212">To troubleshoot or view the status of the Azure VM Desired State Configuration extension, in the Azure portal navigate to the VM being onboarded, then click -> **All settings** -> **Extensions** -> **DSC**.</span></span> <span data-ttu-id="fe465-213">Для получения дополнительных сведений щелкните **Просмотреть подробные сведения о состоянии**.</span><span class="sxs-lookup"><span data-stu-id="fe465-213">For more details, you can click **View detailed status**.</span></span>

[![](./media/automation-dsc-onboarding/DSC_Onboarding_5.png)](https://technet.microsoft.com/library/dn249912.aspx)

## <a name="certificate-expiration-and-reregistration"></a><span data-ttu-id="fe465-214">Истечение срока действия сертификата и повторная регистрация</span><span class="sxs-lookup"><span data-stu-id="fe465-214">Certificate expiration and reregistration</span></span>

<span data-ttu-id="fe465-215">Возможно, после регистрации компьютера в качестве узла DSC на платформе Azure Automation DSC этот узел нужно будет зарегистрировать повторно. Такая необходимость может возникнуть по ряду причин.</span><span class="sxs-lookup"><span data-stu-id="fe465-215">After registering a machine as a DSC node in Azure Automation DSC, there are a number of reasons why you may need to reregister that node in the future:</span></span>

* <span data-ttu-id="fe465-216">После регистрации каждый узел автоматически согласовывает уникальный сертификат для проверки подлинности, срок действия которого составляет один год.</span><span class="sxs-lookup"><span data-stu-id="fe465-216">After registering, each node automatically negotiates a unique certificate for authentication that expires after one year.</span></span> <span data-ttu-id="fe465-217">В настоящее время протокол регистрации PowerShell DSC не может автоматически обновлять сертификаты при приближении даты окончания срока их действия, поэтому по истечении года необходимо повторно регистрировать узлы.</span><span class="sxs-lookup"><span data-stu-id="fe465-217">Currently, the PowerShell DSC registration protocol cannot automatically renew certificates when they are nearing expiration, so you need to reregister the nodes after a year's time.</span></span> <span data-ttu-id="fe465-218">Перед повторной регистрацией убедитесь, что на каждом узле работает Windows Management Framework 5.0 RTM.</span><span class="sxs-lookup"><span data-stu-id="fe465-218">Before reregistering, ensure that each node is running Windows Management Framework 5.0 RTM.</span></span> <span data-ttu-id="fe465-219">Если истек срок действия сертификата аутентификации узла и узел не зарегистрирован, то он не сможет взаимодействовать со службой автоматизации Azure и получит пометку "Не отвечает".</span><span class="sxs-lookup"><span data-stu-id="fe465-219">If a node's authentication certificate expires, and the node is not reregistered, the node will be unable to communicate with Azure Automation and will be marked 'Unresponsive.'</span></span> <span data-ttu-id="fe465-220">Повторная регистрация, выполненная не позднее чем через 90 дней с момента истечения срока действия сертификата или в любой момент после истечения срока действия сертификата, приведет к созданию и использованию нового сертификата.</span><span class="sxs-lookup"><span data-stu-id="fe465-220">Reregistration performed 90 days or less from the certificate expiration time, or at any point after the certificate expiration time, will result in a new certificate being generated and used.</span></span>
* <span data-ttu-id="fe465-221">Чтобы изменить какие-либо [значения локального диспетчера конфигураций PowerShell DSC](https://msdn.microsoft.com/powershell/dsc/metaconfig4) , заданные при первоначальной регистрации узла, например ConfigurationMode.</span><span class="sxs-lookup"><span data-stu-id="fe465-221">To change any [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) that were set during initial registration of the node, such as ConfigurationMode.</span></span> <span data-ttu-id="fe465-222">Сейчас эти значения агента DSC можно изменить только в ходе повторной регистрации.</span><span class="sxs-lookup"><span data-stu-id="fe465-222">Currently, these DSC agent values can only be changed through reregistration.</span></span> <span data-ttu-id="fe465-223">Единственным исключением является конфигурация узла, назначенная узлу, — ее можно изменить на платформе Azure Automation DSC напрямую.</span><span class="sxs-lookup"><span data-stu-id="fe465-223">The one exception is the Node Configuration assigned to the node -- this can be changed in Azure Automation DSC directly.</span></span>

<span data-ttu-id="fe465-224">Повторная регистрация узла выполняется аналогично первоначальной, то есть с помощью любого из средств, описанных в этом документе.</span><span class="sxs-lookup"><span data-stu-id="fe465-224">Reregistration can be performed in the same way you registered the node initially, using any of the onboarding methods described in this document.</span></span> <span data-ttu-id="fe465-225">Перед повторной регистрацией отменять регистрацию узла на платформе Azure Automation DSC не нужно.</span><span class="sxs-lookup"><span data-stu-id="fe465-225">You do not need to unregister a node from Azure Automation DSC before reregistering it.</span></span>

## <a name="related-articles"></a><span data-ttu-id="fe465-226">Связанные статьи</span><span class="sxs-lookup"><span data-stu-id="fe465-226">Related Articles</span></span>

* [<span data-ttu-id="fe465-227">Обзор Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="fe465-227">Azure Automation DSC overview</span></span>](automation-dsc-overview.md)
* [<span data-ttu-id="fe465-228">Командлеты Automation DSC Azure</span><span class="sxs-lookup"><span data-stu-id="fe465-228">Azure Automation DSC cmdlets</span></span>](/powershell/module/azurerm.automation/#automation)
* [<span data-ttu-id="fe465-229">Цены на Automation DSC Azure</span><span class="sxs-lookup"><span data-stu-id="fe465-229">Azure Automation DSC pricing</span></span>](https://azure.microsoft.com/pricing/details/automation/)
