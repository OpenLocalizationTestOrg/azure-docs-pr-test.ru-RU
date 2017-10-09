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
# <a name="compiling-configurations-in-azure-automation-dsc"></a>Компилирование конфигураций в Azure Automation DSC

Можно скомпилировать конфигурации требуемого состояния (DSC) в службе автоматизации Azure двумя способами: в hello портал Azure, а также с помощью Windows PowerShell. Hello Следующая таблица поможет определить, когда какой метод на основе hello характеристик каждого toouse:

### <a name="azure-portal"></a>Портал Azure

* Простейший способ с интерактивным пользовательским интерфейсом.
* Значения параметра простой формы tooprovide
* Легко отслеживаемое состояние задания.
* Доступ с проверкой подлинности в Azure.

### <a name="windows-powershell"></a>Windows PowerShell

* Вызов из командной строки с помощью командлетов Windows PowerShell.
* Может быть добавлено в автоматизированное решение, состоящее из нескольких шагов.
* Необходимо предоставить значения простых и сложных параметров.
* Отслеживание состояния задания
* Требуется клиент toosupport командлеты PowerShell
* Передача данных ConfigurationData.
* Компилирование конфигураций, использующих учетные данные.

После выбора метода компиляции, можно выполнить соответствующие процедуры hello ниже toostart компиляции.

## <a name="compiling-a-dsc-configuration-with-hello-azure-portal"></a>При компиляции конфигурации DSC с hello портал Azure

1. В учетной записи службы автоматизации щелкните **DSC Configurations** (Конфигурации DSC).
2. Щелкните tooopen конфигурации колонке.
3. Нажмите кнопку **Компилировать**.
4. Если конфигурация hello не имеет параметров, можно запрашиваемые tooconfirm следует toocompile ли он. Если параметры конфигурации hello, hello **компиляции конфигурации** колонке будет открыт, чтобы обеспечить значения параметров. В разделе hello [ **базовых параметров** ](#basic-parameters) ниже, в разделе для получения сведений о параметрах.
5. Hello **задание компиляции** открывается колонка, чтобы отследить состояние задания компиляции hello и hello конфигурации узла (документам MOF конфигурации), она вызвана toobe обмена hello опрашивающего сервера Azure Automation DSC.

## <a name="compiling-a-dsc-configuration-with-windows-powershell"></a>Компилирование конфигурации DSC с помощью Windows PowerShell

Можно использовать [ `Start-AzureRmAutomationDscCompilationJob` ](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) toostart компиляции с помощью Windows PowerShell. Следующий пример кода Hello запускает компиляции конфигурации DSC, называемой **SampleConfig**.

```powershell
Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"
```

`Start-AzureRmAutomationDscCompilationJob`Возвращает компиляции заданий, которые можно использовать tootrack его состояние объекта. Затем можно использовать этот объект задания компиляции с [ `Get-AzureRmAutomationDscCompilationJob` ](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob) toodetermine hello состояние задания компиляции hello, и [ `Get-AzureRmAutomationDscCompilationJobOutput` ](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput) tooview свои потоки (output). Следующий образец кода Hello начинает компиляцию hello **SampleConfig** конфигурации, ожидает его завершения, а затем отображает свои потоки.

```powershell
$CompilationJob = Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"

while($CompilationJob.EndTime –eq $null -and $CompilationJob.Exception –eq $null)
{
    $CompilationJob = $CompilationJob | Get-AzureRmAutomationDscCompilationJob
    Start-Sleep -Seconds 3
}

$CompilationJob | Get-AzureRmAutomationDscCompilationJobOutput –Stream Any
```

## <a name="basic-parameters"></a>Базовые параметры
Объявление параметра в конфигурациях DSC, включая типы параметров и свойств, работает hello таким же как модулей Runbook службы автоматизации Azure. В разделе [запуск runbook в автоматизации Azure](automation-starting-a-runbook.md) toolearn Дополнительные сведения о параметрах runbook.

Hello следующий пример использует два параметра при вызове **FeatureName** и **IsPresent**, значений свойств в hello hello toodetermine **ParametersExample.sample** узла Конфигурация, созданные во время компиляции.

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

Вы можете скомпилировать конфигураций DSC, используйте базовых параметров портала Azure Automation DSC hello, или с помощью Azure PowerShell.

### <a name="portal"></a>Microsoft Azure

На портале hello, можно ввести значения параметров после нажатия кнопки **компиляции**.

![замещающий текст](./media/automation-dsc-compile/DSC_compiling_1.png)

### <a name="powershell"></a>PowerShell

PowerShell требуются параметры в [hashtable](http://technet.microsoft.com/library/hh847780.aspx) hello ключ совпадает с именем параметра hello, куда hello, значение равно значению параметра hello.

```powershell
$Parameters = @{
    "FeatureName" = "Web-Server"
    "IsPresent" = $False
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ParametersExample" -Parameters $Parameters
```

Сведения о передаче учетных данных PSCredentials в качестве параметров см. в разделе <a href="#credential-assets">**Активы учетных данных**</a> ниже.

## <a name="configurationdata"></a>ConfigurationData
**ConfigurationData** позволяет tooseparate отделение структурной конфигурации из какой-либо настройки среды при работе с PowerShell DSC. В разделе [отделение «Что» от «Where» в PowerShell DSC](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) toolearn Дополнительные сведения о **ConfigurationData**.

> [!NOTE]
> Можно использовать **ConfigurationData** при компиляции в Azure Automation DSC с помощью Azure PowerShell, но не в hello портал Azure.

Hello ниже примере DSC конфигурации используется **ConfigurationData** через hello **$ConfigurationData** и **$AllNodes** ключевые слова. Кроме того, потребуется hello [ **xWebAdministration** модуль](https://www.powershellgallery.com/packages/xWebAdministration/) в этом примере:

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

Можно скомпилировать конфигурацию DSC hello выше с помощью PowerShell. Hello под PowerShell добавляет два узла конфигурации toohello опрашивающего сервера Azure Automation DSC: **ConfigurationDataSample.MyVM1** и **ConfigurationDataSample.MyVM3**:

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

## <a name="assets"></a>Активы

Ссылки на средства hello же Azure Automation DSC конфигурации и модулей Runbook. Hello ниже для получения дополнительной информации см.:

* [Сертификаты](automation-certificates.md)
* [Подключения](automation-connections.md)
* [Учетные данные](automation-credentials.md)
* [Переменные](automation-variables.md)

### <a name="credential-assets"></a>Активы учетных данных

Хотя конфигурации DSC в службе автоматизации Azure могут ссылаться на ресурсы учетных данных с помощью командлета **Get-AzureRmAutomationCredential**, при необходимости эти ресурсы можно передавать и в качестве параметров. Если конфигурация принимает параметр **PSCredential** тип, как значение этого параметра, а не объект PSCredential, потребуется toopass hello строковое имя актива учетных данных службы автоматизации Azure. В фоновом hello hello Azure учетных данных службы автоматизации с таким именем будет получаться и переданный toohello конфигурации.

Хранение учетных данных безопасности в конфигурации узла (документам MOF конфигурации) требует шифрования hello учетных данных в MOF-файл конфигурации узла hello. Служба автоматизации Azure расширяет эти дополнительные и шифрует hello всей MOF-файл. Однако в настоящее время необходимо сообщить PowerShell DSC допустимо для toobe учетные данные, выводимые в виде обычного текста во время создания MOF конфигурации узла, так как PowerShell DSC не знает, что службы автоматизации Azure будет шифрования hello всей MOF-файл после его Создание через задание компиляции.

Можно определить PowerShell DSC, что допустимо для toobe учетные данные, выводимые в виде обычного текста в конфигурации узла hello созданный MOF-файлы с помощью [ **ConfigurationData**](#configurationdata). Необходимо передать `PSDscAllowPlainTextPassword = $true` через **ConfigurationData** для каждого узла блока имя, которое отображается в конфигурации hello DSC и использует учетные данные.

Hello пример конфигурации DSC, использующий актива учетных данных службы автоматизации.

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

Можно скомпилировать конфигурацию DSC hello выше с помощью PowerShell. Hello под PowerShell добавляет два узла конфигурации toohello опрашивающего сервера Azure Automation DSC: **CredentialSample.MyVM1** и **CredentialSample.MyVM2**.

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

## <a name="importing-node-configurations"></a>Импорт конфигураций узлов

Вы также можете импортировать конфигурации узла (MOF-файлы), скомпилированные за пределами Azure. Одним из преимуществ является то, что конфигурации узла могут быть заверены.
Настройка знаком узла подтверждается локально на управляемом узле агент hello DSC, гарантируя, что в этой конфигурации hello, примененные toohello узла поступает из авторизованного источника.

> [!NOTE]
> Заверенные конфигурации можно импортировать в учетную запись службы автоматизации Azure, но служба автоматизации Azure в настоящее время не поддерживает компиляцию заверенных конфигураций.

> [!NOTE]
> Файл конфигурации узла должно быть не больше 1 МБ tooallow его toobe, импортированные в службу автоматизации Azure.

Рассказывается, как на https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module toosign узла конфигурации.

### <a name="importing-a-node-configuration-in-hello-azure-portal"></a>Импорт конфигурации узла в hello портал Azure

1. В учетной записи службы автоматизации щелкните **DSC node configurations** (Конфигурации узла DSC).

    ![Конфигурации узла DSC](./media/automation-dsc-compile/node-config.png)
2. В hello **конфигурации узла DSC** колонка, щелкните **добавить NodeConfiguration**.
3. В hello **импорта** колонке нажмите кнопку Далее toohello hello папки значок **файла конфигурации узла** toobrowse textbox для файла конфигурации узла (MOF) на локальном компьютере.

    ![Поиск локального файла](./media/automation-dsc-compile/import-browse.png)
4. Введите имя в hello **имя конфигурации** текстового поля. Это имя должно совпадать с именем hello hello конфигурации, из которой была скомпилирована hello конфигурации узла.
5. Нажмите кнопку **ОК**.

### <a name="importing-a-node-configuration-with-powershell"></a>Импорт конфигурации узла с помощью PowerShell

Можно использовать hello [AzureRmAutomationDscNodeConfiguration импорта](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) tooimport командлет конфигурации узла, в свою учетную запись автоматизации.

```powershell
Import-AzureRmAutomationDscNodeConfiguration -AutomationAccountName "MyAutomationAccount" -ResourceGroupName "MyResourceGroup" -ConfigurationName "MyNodeConfiguration" -Path "C:\MyConfigurations\TestVM1.mof"
```



