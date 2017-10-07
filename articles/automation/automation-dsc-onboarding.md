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
# <a name="onboarding-machines-for-management-by-azure-automation-dsc"></a>Подключение компьютеров для управления с помощью Azure Automation DSC

## <a name="why-manage-machines-with-azure-automation-dsc"></a>В чем преимущества управления компьютерами с помощью службы Azure Automation DSC?

Настройка требуемого состояния (DSC) с помощью службы автоматизации Azure так же проста, как и [настройка требуемого состояния с использованием PowerShell](https://technet.microsoft.com/library/dn249912.aspx). Это мощная служба управления конфигурациями для узлов DSC (физических и виртуальных машин), которую можно использовать в любом облачном или локальном центре обработки данных. Она обеспечивает быструю и простую масштабируемость тысяч компьютеров из безопасного центрального расположения. Вы можете легко присоединяться машины, назначьте их декларативной конфигурации и просмотр отчетов, отражающих каждого компьютера, состояние соответствия требуемой toohello указанный. уровень управления Hello Azure Automation DSC — tooDSC какой уровень управления hello Azure Automation является tooPowerShell сценариев. Другими словами в hello аналогично, автоматизация Azure помогает управлять сценариев PowerShell, он также позволяет управлять конфигурациями DSC. toolearn Дополнительные сведения о hello преимущества использования Azure Automation DSC. в разделе [Обзор Azure Automation DSC](automation-dsc-overview.md).

Azure Automation DSC можно использовать toomanage различных компьютерах:

* Виртуальные машины Azure (классические).
* Виртуальные машины Azure
* виртуальные машины Amazon Web Services (AWS);
* физические или виртуальные машины под управлением Windows, расположенные локально или в облачной службе, отличной от Azure или AWS;
* Физические или виртуальные машины под управлением Linux, расположенные локально, в Azure или облачной службе, отличной от Azure.

Кроме того Если вы не готовы toomanage конфигурации машины из облака hello, Azure Automation DSC может также использоваться как конечную точку только для отчетов. Это позволяет tooset (push) требуемой конфигурации с помощью DSC в локальной среде и просмотр сведений широкие возможности отчетности на соответствие узел hello требуемое состояние в службе автоматизации Azure.

Hello в следующих разделах описываются способы подключения каждого типа машины tooAzure DSC службы автоматизации.

## <a name="azure-virtual-machines-classic"></a>Виртуальные машины Azure (классические).

С помощью DSC службы автоматизации Azure можно легко присоединяться виртуальных машинах Azure (классические) для управления конфигурацией с помощью портала Azure hello или PowerShell. Кулисами hello и без администратор, имеющий tooremote в hello ВМ hello расширения для настройки требуемого состояния Azure VM регистрирует hello виртуальной Машины Azure Automation DSC. Поскольку hello расширения для настройки требуемого состояния Azure ВМ выполняется асинхронно, tootrack действия ход его выполнения или устранения неполадок приведены в hello [ **адаптации виртуальной машины Azure, устранение неполадок** ](#troubleshooting-azure-virtual-machine-onboarding)разделе ниже.

### <a name="azure-portal"></a>Портал Azure

В hello [портал Azure](http://portal.azure.com/), нажмите кнопку **Обзор** -> **виртуальные машины (классические)**. Выберите, требуется tooonboard виртуальной Машины Windows hello. На панели мониторинга виртуальной машины hello щелкните **все параметры** -> **расширения** -> **добавить**  ->   **Служба автоматизации Azure DSC** -> **создания**. Введите hello [значения локального диспетчера конфигураций DSC PowerShell](https://msdn.microsoft.com/powershell/dsc/metaconfig4) требуется для вашей учетной записи автоматизации регистрационный ключ и URL-адрес регистрации и при необходимости toohello tooassign конфигурации узла виртуальной Машины.

![](./media/automation-dsc-onboarding/DSC_Onboarding_1.png)

URL-адрес регистрации toofind hello и ключа для машины hello tooonboard учетной записи автоматизации hello, см. раздел hello [ **Secure регистрации** ](#secure-registration) разделе ниже.

### <a name="powershell"></a>PowerShell

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

## <a name="azure-virtual-machines"></a>Виртуальные машины Azure

Azure Automation DSC позволяет легко присоединять виртуальные машины, Azure для управления конфигурацией с помощью портала Azure hello, шаблоны Azure Resource Manager или PowerShell. Кулисами hello и без администратор, имеющий tooremote в hello ВМ hello расширения для настройки требуемого состояния Azure VM регистрирует hello виртуальной Машины Azure Automation DSC. Поскольку hello расширения для настройки требуемого состояния Azure ВМ выполняется асинхронно, tootrack действия ход его выполнения или устранения неполадок приведены в hello [ **адаптации виртуальной машины Azure, устранение неполадок** ](#troubleshooting-azure-virtual-machine-onboarding)разделе ниже.

### <a name="azure-portal"></a>Портал Azure

В hello [портал Azure](https://portal.azure.com/), перейдите toohello учетной записи службы автоматизации Azure место tooonboard виртуальных машин. Щелкните панель мониторинга учетной записи автоматизации hello **узлы DSC** -> **добавить виртуальную Машину Azure**.

В разделе **выберите виртуальные машины tooonboard**, выберите один или несколько на виртуальные машины Azure tooonboard.

![](./media/automation-dsc-onboarding/DSC_Onboarding_2.png)

В разделе **Настройка регистрационные данные**, введите hello [значения локального диспетчера конфигураций DSC PowerShell](https://msdn.microsoft.com/powershell/dsc/metaconfig4) необходимые для вашего случая использования и при необходимости toohello tooassign конфигурации узла виртуальной Машины.

![](./media/automation-dsc-onboarding/DSC_Onboarding_3.png)

### <a name="azure-resource-manager-templates"></a>Шаблоны диспетчера ресурсов Azure

Можно развернуть виртуальные машины Azure и tooAzure выставленных DSC службы автоматизации через шаблоны Azure Resource Manager. В разделе [Настройка виртуальной Машины через расширение DSC и Azure Automation DSC](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/) для шаблона, onboards tooAzure существующих виртуальных Машин DSC службы автоматизации. toofind hello ключ и регистрации URL-адрес регистрации выполнены как входные данные в этом шаблоне см hello [ **Secure регистрации** ](#secure-registration) разделе ниже.

### <a name="powershell"></a>PowerShell

Hello [AzureRmAutomationDscNode регистра](/powershell/module/azurerm.automation/register-azurermautomationdscnode) командлет можно использовать tooonboard виртуальных машин в hello портал Azure с помощью PowerShell.

## <a name="amazon-web-services-aws-virtual-machines"></a>виртуальные машины Amazon Web Services (AWS);

Вы можете легко присоединяться Amazon Web Services виртуальных машин для управления конфигурацией с DSC службы автоматизации Azure с помощью hello AWS DSC Toolkit. Дополнительные сведения о hello toolkit [здесь](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/).

## <a name="physicalvirtual-windows-machines-on-premises-or-in-a-cloud-other-than-azureaws"></a>физические или виртуальные машины под управлением Windows, расположенные локально или в облачной службе, отличной от Azure или AWS;

Локальные компьютеры Windows и Windows машин в облаках без использования Azure (например, веб-службы Amazon) также могут tooAzure выставленных DSC службы автоматизации, при условии, что они имеют toohello исходящий доступ к Интернету, через несколько простых шагов:

1. Убедитесь, что hello последнюю версию [WMF 5](http://aka.ms/wmf5latest) устанавливается на компьютерах hello требуется tooonboard tooAzure DSC службы автоматизации.
2. Следуйте приведенным инструкциям раздела hello [ **метаконфигурации создания DSC** ](#generating-dsc-metaconfigurations) ниже toogenerate папку, содержащую hello необходимости метаконфигурации DSC.
3. Удаленно применяются требуется tooonboard toohello машины hello PowerShell DSC метаконфигурации. **компьютер Hello, эта команда выполняется из должен иметь hello последнюю версию [WMF 5](http://aka.ms/wmf5latest) установлен**:

    ```powershell
    Set-DscLocalConfigurationManager -Path C:\Users\joe\Desktop\DscMetaConfigs -ComputerName MyServer1, MyServer2
    ```

4. Если не удается применить метаконфигурации PowerShell DSC hello удаленно, скопируйте папку метаконфигурации hello из шага 2 на каждой машине tooonboard. Затем вызовите **Set-DscLocalConfigurationManager** локально на каждой машине tooonboard.
5. С помощью hello портал Azure или командлетов, убедитесь, что hello машины tooonboard теперь отображаются как узлы DSC зарегистрирован в вашей учетной записи службы автоматизации Azure.

## <a name="physicalvirtual-linux-machines-on-premises-in-azure-or-in-a-cloud-other-than-azure"></a>Физические или виртуальные машины под управлением Linux, расположенные локально, в Azure или облачной службе, отличной от Azure.

Компьютеры Linux локальных машин Linux в Azure, и компьютеры Linux в облаках без использования Azure также может быть встроен tooAzure DSC службы автоматизации, при условии, что они имеют toohello исходящий доступ к Интернету, через несколько простых шагов:

1. Убедитесь, что hello последнюю версию [настройки требуемого состояния PowerShell для Linux](https://github.com/Microsoft/PowerShell-DSC-for-Linux) устанавливается на компьютерах hello требуется tooonboard tooAzure DSC службы автоматизации.
2. Если hello [значения по умолчанию локальный диспетчер конфигураций DSC PowerShell](https://msdn.microsoft.com/powershell/dsc/metaconfig4) соответствует вашей вариант использования, и требуется tooonboard машины, например, они **оба** по запросу из и отчетов tooAzure DSC службы автоматизации:

   + На каждом Linux машины tooonboard tooAzure DSC службы автоматизации используйте tooonboard Register.py hello, который по умолчанию используется локальный диспетчер конфигураций DSC PowerShell с помощью:

     `/opt/microsoft/dsc/Scripts/Register.py <Automation account registration key> <Automation account registration URL>`

   + toofind hello регистрации ключа и регистрации URL-адрес для вашей учетной записи автоматизации в разделе hello [ **Secure регистрации** ](#secure-registration) разделе ниже.

     Если hello PowerShell DSC локальный диспетчер конфигураций по умолчанию **сделать** **не** соответствует вашей вариант использования, либо требуется tooonboard компьютеров таким образом, что они только о tooAzure DSC службы автоматизации, но не по запросу конфигурации и модули PowerShell, выполните шаги 3 – 6. В противном случае перейдите непосредственно toostep 6.

3. Следуйте приведенным инструкциям hello hello [ **метаконфигурации создания DSC** ](#generating-dsc-metaconfigurations) ниже, в разделе toogenerate папку, содержащую необходимые hello DSC метаконфигурации.
4. Удаленно применяются требуется tooonboard toohello машины hello PowerShell DSC метаконфигурации.

    ```powershell
    $SecurePass = ConvertTo-SecureString -String "<root password>" -AsPlainText -Force
    $Cred = New-Object System.Management.Automation.PSCredential "root", $SecurePass
    $Opt = New-CimSessionOption -UseSsl -SkipCACheck -SkipCNCheck -SkipRevocationCheck

    # need a CimSession for each Linux machine tooonboard

    $Session = New-CimSession -Credential $Cred -ComputerName <your Linux machine> -Port 5986 -Authentication basic -SessionOption $Opt

    Set-DscLocalConfigurationManager -CimSession $Session -Path C:\Users\joe\Desktop\DscMetaConfigs
    ```

компьютер Hello, эта команда выполняется из должен иметь hello последнюю версию [WMF 5](http://aka.ms/wmf5latest) установлен.

1. Если не удается применить метаконфигурации PowerShell DSC hello удаленно, для каждого tooonboard машины Linux, скопируйте hello метаконфигурации соответствующая toothat машина из папки hello на шаге 5 на компьютере Linux hello. Затем вызовите `SetDscLocalConfigurationManager.py` локально на каждом компьютере Linux требуется tooonboard tooAzure DSC службы автоматизации:

   `/opt/microsoft/dsc/Scripts/SetDscLocalConfigurationManager.py -configurationmof <path toometaconfiguration file>`

2. С помощью hello портал Azure или командлетов, убедитесь, что hello машины tooonboard теперь отображаются как узлы DSC зарегистрирован в вашей учетной записи службы автоматизации Azure.

## <a name="generating-dsc-metaconfigurations"></a>Создание метаконфигураций DSC

toogenerically освоить любой компьютер tooAzure DSC службы автоматизации, [метаконфигурацию DSC](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) может быть создан, при применения, сообщает hello DSC агента на toopull машины hello из или получении отчета tooAzure DSC службы автоматизации. Метаконфигурации DSC для Azure Automation DSC может быть создан с помощью конфигурации PowerShell DSC или командлеты Azure Automation PowerShell hello.

> [!NOTE]
> Метаконфигурации DSC содержат tooonboard hello необходимости секретные данные машина tooan учетной записи автоматизации для управления. Убедитесь, что tooproperly защиты любого метаконфигурации DSC, создаваемые вами или удалить их после использования.

### <a name="using-a-dsc-configuration"></a>Использование конфигурации DSC

1. Откройте hello интегрированной среды Сценариев PowerShell с правами администратора на компьютере в локальной среде. Hello компьютер должен иметь hello последнюю версию [WMF 5](http://aka.ms/wmf5latest) установлен.
2. Скопируйте следующий скрипт локально hello. Этот скрипт содержит конфигурацию PowerShell DSC для создания метаконфигурации и команда tookick отключение создания метаконфигурации hello.

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

3. Заполните hello регистрационный ключ и URL-адрес для учетной записи автоматизации, а также имена hello tooonboard машины hello. Все остальные параметры являются необязательными. toofind hello регистрации ключа и регистрации URL-адрес для вашей учетной записи автоматизации в разделе hello [ **Secure регистрации** ](#secure-registration) разделе ниже.
4. Если требуется tooAzure hello машины tooreport DSC состояние сведения DSC службы автоматизации, но не по запросу, конфигурации и модули PowerShell, задайте hello **ReportOnly** tootrue параметра.
5. Запустите сценарий hello. Вы создали папку с именем **DscMetaConfigs** в рабочий каталог, содержащий hello метаконфигурации PowerShell DSC для tooonboard машин hello (с правами администратора):

    ```powershell
    Set-DscLocalConfigurationManager -Path ./DscMetaConfigs
    ```

### <a name="using-hello-azure-automation-cmdlets"></a>С помощью командлетов службы автоматизации Azure hello

Если значения по умолчанию hello локальный диспетчер конфигураций DSC PowerShell соответствует вашей вариант использования, и требуется tooonboard машин таким образом, что они извлекают из и сообщить tooAzure DSC службы автоматизации, командлеты автоматизации Azure hello предоставляют упрощенный метод создания hello DSC метаконфигурации при необходимости:

1. Откройте консоль PowerShell hello или интегрированной среды Сценариев PowerShell с правами администратора на машине в локальной среде.
2. Подключение с использованием диспетчера ресурсов tooAzure **добавить AzureRmAccount**
3. Загрузите PowerShell DSC метаконфигурации hello для машин hello требуется tooonboard из hello автоматизации учетной записи toowhich tooonboard узлах:

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
    
4. Вы создали папку с именем ***DscMetaConfigs***, содержащий hello метаконфигурации PowerShell DSC для tooonboard машин hello (с правами администратора):
    
    ```powershell
    Set-DscLocalConfigurationManager -Path $env:UserProfile\Desktop\DscMetaConfigs
    ```

## <a name="secure-registration"></a>Безопасная регистрация

Машины могут безопасно подключить tooan учетной записи службы автоматизации Azure через протокол регистрации hello WMF 5 DSC, что позволяет узел tooauthenticate tooa PowerShell DSC V2 по запросу или службу отчетов сервера DSC (включая Azure Automation DSC). Hello узел регистрируется сервер toohello **URL-адрес регистрации**, выполняющего проверку подлинности с помощью **регистрационный ключ**. Во время регистрации узла hello DSC и сервере запросу DSC-формирования отчетов согласовывать уникальный сертификат для этого узла toouse для проверки подлинности toohello сервера после регистрации. Этот процесс исключает возможность подмены подключенных узлов друг другом, например, если один из узлов взломан и является вредоносным. После регистрации hello регистрационный ключ не используется для проверки подлинности еще раз и удаляется из узла "hello".

Можно получить hello сведения, необходимые для протокола регистрации hello DSC из hello **управление ключами** колонку на портале Azure предварительной версии hello. Откройте эту колонку, щелкнув значок ключа hello для hello **Essentials** панель для hello учетной записи автоматизации.

![](./media/automation-dsc-onboarding/DSC_Onboarding_4.png)

* URL-адрес регистрации — поле URL-адрес hello в колонке hello управление ключами.
* Ключ регистрации — hello первичный ключ доступа или вторичный ключ доступа в колонке hello управление ключами. Можно использовать любой из этих ключей.

Для повышения безопасности могут быть повторно созданы hello первичный и вторичный ключи доступа учетной записи автоматизации в любое время (в hello **управление ключами** колонку) tooprevent регистраций будущих узла, с помощью предыдущих ключей.

## <a name="troubleshooting-azure-virtual-machine-onboarding"></a>Устранение неполадок при подключении виртуальной машины Azure

Служба Azure Automation DSC позволяет легко подключать виртуальные машины Microsoft Azure для управления конфигурациями. Механизме hello hello расширения для настройки требуемого состояния Azure виртуальной Машины — используется tooregister hello виртуальной Машины с помощью DSC службы автоматизации Azure. Поскольку hello расширения для настройки требуемого состояния Azure ВМ выполняется асинхронно, отслеживания хода его выполнения и устранение неполадок выполнения могут быть важны.

> [!NOTE]
> Любой метод адаптации tooAzure виртуальной Машины Windows Azure Automation DSC, использующего расширения настройки требуемого состояния Azure VM hello может занять час tooan tooshow узел hello вверх, зарегистрированного в службе автоматизации Azure. Это происходит из-за установки Windows Management Framework 5.0 toohello на hello ВМ путем расширения Azure VM DSC hello, которое является обязательным tooonboard hello ВМ tooAzure DSC службы автоматизации.

tootroubleshoot или представление состояния hello hello расширение настройки требуемого состояния Azure VM hello портал Azure перейдите toohello, выставленных виртуальной Машины, затем щелкните -> **все параметры** -> **расширения**   ->  **DSC**. Для получения дополнительных сведений щелкните **Просмотреть подробные сведения о состоянии**.

[![](./media/automation-dsc-onboarding/DSC_Onboarding_5.png)](https://technet.microsoft.com/library/dn249912.aspx)

## <a name="certificate-expiration-and-reregistration"></a>Истечение срока действия сертификата и повторная регистрация

После регистрации компьютера в качестве узла DSC в Azure Automation DSC, существует ряд причин, почему может потребоваться tooreregister этого узла в hello будущих:

* После регистрации каждый узел автоматически согласовывает уникальный сертификат для проверки подлинности, срок действия которого составляет один год. В настоящее время hello протокола регистрации PowerShell DSC не удается обновить автоматически сертификаты при они скоро истекает срок действия, требуется tooreregister hello узлы после времени года. Перед повторной регистрацией убедитесь, что на каждом узле работает Windows Management Framework 5.0 RTM. Если истечения срока действия сертификата проверки подлинности узла и узла hello не зарегистрирован, hello узел будет невозможно toocommunicate в службе автоматизации Azure и будут помечены «Неотвечающим.» Перерегистрация выполняется через 90 дней или меньше с момента истечения срока действия сертификата hello, или в любой момент после времени окончания срока действия сертификата hello, приведет к формируются и использовать новый сертификат.
* toochange любой [значения локального диспетчера конфигураций DSC PowerShell](https://msdn.microsoft.com/powershell/dsc/metaconfig4) , заданные во время первоначальной регистрации hello узел, например ConfigurationMode. Сейчас эти значения агента DSC можно изменить только в ходе повторной регистрации. Единственным исключением Hello hello конфигурации, назначенной toohello узел — это можно изменить в Azure Automation DSC непосредственно.

Перерегистрация могут выполняться в hello так же, как вы зарегистрировали hello узел изначально одним из способов адаптации hello, описанные в этом документе. Прежде чем зарегистрировать его не обязательно toounregister узла из DSC службы автоматизации Azure.

## <a name="related-articles"></a>Связанные статьи

* [Обзор Azure Automation DSC](automation-dsc-overview.md)
* [Командлеты Automation DSC Azure](/powershell/module/azurerm.automation/#automation)
* [Цены на Automation DSC Azure](https://azure.microsoft.com/pricing/details/automation/)
