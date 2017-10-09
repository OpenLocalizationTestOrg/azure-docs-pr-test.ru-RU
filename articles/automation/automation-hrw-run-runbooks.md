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
# <a name="running-runbooks-on-a-hybrid-runbook-worker"></a>Запуск модулей runbook в гибридной рабочей роли Runbook 
Нет никаких различий в структуре hello модулей Runbook, которые запускаются в автоматизации Azure и те, которые работают на гибридную рабочую роль Runbook. Модули Runbook, которые можно использовать с каждым скорее существенно отличаются у менее так как модули Runbook, предназначенных для гибридной рабочей роли Runbook, обычно управлять ресурсами на локальном компьютере hello сам или к ресурсам в локальной среде hello, где он будет развернут, при модулей Runbook в службе автоматизации Azure обычно управлять ресурсами в облаке Azure hello.

Можно редактировать книгу для гибридной рабочей ролью Runbook в автоматизации Azure, но имеется трудности при попытке tootest hello runbook в редакторе hello.  модули PowerShell Hello, получающих доступ к локальным ресурсам hello может отсутствовать в среде автоматизации Azure в этом случае, произойдет сбой теста hello.  Если установить hello необходимые модули, то hello модуль runbook будет запущен, но он не будет возможности tooaccess локальных ресурсов для выполнения теста.

## <a name="starting-a-runbook-on-hybrid-runbook-worker"></a>Запуск runbook в гибридной рабочей роли Runbook
[Запуск модуля Runbook в службе автоматизации Azure](automation-starting-a-runbook.md) описываются различные методы запуска модуля Runbook.  Добавляет гибридной рабочей ролью Runbook **RunOn** вариант, где можно указать имя группы гибридных рабочих ролей Runbook hello.  Если группа указана, hello runbook извлекается и выполнялись hello рабочих процессов в этой группе.  Если этот параметр не указан, то он будет запущен в службе автоматизации Azure в обычном режиме.

При запуске модуля runbook в hello портал Azure, вам предоставляется **проведение** параметр, в котором можно выбрать **Azure** или **гибридной рабочей роли**.  При выборе **гибридной рабочей роли**, а затем из раскрывающегося списка можно выбрать группу hello.

Используйте hello **RunOn** параметра.  Можно использовать hello, следующая команда toostart runbook с именем Test-Runbook в Runbook группу гибридных рабочих ролей с именем MyHybridGroup, с помощью Windows PowerShell.

    Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -RunOn "MyHybridGroup"

> [!NOTE]
> Hello **RunOn** toohello был добавлен параметр **Start-AzureAutomationRunbook** командлет в версии 0.9.1 Microsoft Azure PowerShell.  Вы должны [Загрузка последней версии hello](https://azure.microsoft.com/downloads/) при наличии более ранних один из уже установлен.  Требуется только tooinstall эту версию на рабочей станции, где hello runbook начиная с Windows PowerShell.  Нет необходимости tooinstall его на компьютере рабочей hello кроме случая, когда toostart модулей Runbook с этого компьютера.  Невозможно запустить в настоящее время книгу в гибридной рабочей роли Runbook из другого модуля runbook, так как это потребует hello последнюю версию Azure Powershell toobe установлен в вашей учетной записи автоматизации.  последнюю версию Hello автоматически обновляется в службе автоматизации Azure и автоматически сместить вниз работников toohello скоро.
>
>

## <a name="runbook-permissions"></a>Разрешения для модулей Runbook
Модулей Runbook, запущенных на гибридную рабочую роль Runbook нельзя использовать hello же метод, который обычно используется для проверки подлинности tooAzure ресурсы, так как они получают доступ к ресурсам за пределами Azure модулей Runbook.  Hello runbook можно предоставить собственную проверку подлинности toolocal ресурсы или можно указать tooprovide учетная запись запуска от имени для всех модулей Runbook контекст пользователя.

### <a name="runbook-authentication"></a>Проверка подлинности модуля Runbook
По умолчанию модулей Runbook будет выполняться в контексте hello hello локальной системной учетной записи локального компьютера hello, поэтому они должны предоставить свои собственные tooresources проверки подлинности, который получит доступ к.  

Можно использовать [учетные данные](http://msdn.microsoft.com/library/dn940015.aspx) и [сертификат](http://msdn.microsoft.com/library/dn940013.aspx) активы в модуле runbook с помощью командлетов, позволяющих toospecify учетные данные, вы можете проверять подлинность toodifferent ресурсов.  Hello следующем примере показан фрагмент runbook, который перезапускает компьютер.  Он получает имя актива и hello учетных данных компьютера hello из переменной активов учетные данные и затем использует эти значения с помощью командлета Restart-Computer hello.

    $Cred = Get-AzureRmAutomationCredential -ResourceGroupName "ResourceGroup01" -Name "MyCredential"
    $Computer = Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" -Name  "ComputerName"

    Restart-Computer -ComputerName $Computer -Credential $Cred

Можно также использовать [InlineScript](automation-powershell-workflow.md#inlinescript), что позволяет toorun блоки кода на другом компьютере с учетными данными, указанными с hello [общий параметр PSCredential](http://technet.microsoft.com/library/jj129719.aspx).

### <a name="runas-account"></a>Учетная запись запуска от имени
Вместо предоставления своей собственной проверки подлинности ресурсов toolocal модулей Runbook, можно указать **RunAs** учетной записи для группы гибридных рабочих ролей.  Указать [актива учетных данных](automation-credentials.md) с toolocal доступ к ресурсам, и все модули Runbook запускались эти учетные данные при работе в гибридной рабочей роли Runbook в группе hello.  

имя пользователя Hello для hello учетных данных должен быть в одном из следующих форматов hello:

* домен\имя пользователя;
* username@domain
* имя пользователя (для учетных записей локального toohello на локальном компьютере)

Используйте следующие процедуры toospecify учетную запись запуска от имени для группы гибридных рабочих ролей hello.

1. Создание [актива учетных данных](automation-credentials.md) с toolocal доступ к ресурсам.
2. Откройте учетную запись автоматизации hello в hello портал Azure.
3. Выберите hello **гибридных рабочих групп** плитку, а затем выберите группу hello.
4. Щелкните **Все параметры**, а затем — **Настройки группы гибридных рабочих ролей**.
5. Изменение **запуска от имени** из **по умолчанию** слишком**настраиваемый**.
6. Выберите учетные данные hello и нажмите кнопку **Сохранить**.

### <a name="automation-run-as-account"></a>Учетная запись запуска от имени службы автоматизации
В рамках процесса автоматизированной сборки для развертывания ресурсов в Azure может потребоваться доступ tooon локальных систем toosupport одну или несколько шагов в последовательности развертывания.  toosupport проверки подлинности с помощью hello запуска от имени учетной записи Azure, вам понадобится tooinstall hello запуска от имени учетной записи сертификат.  

Здравствуйте, следуя PowerShell runbook *RunAsCertificateToHybridWorker экспорта*, экспортирует hello запуска от имени сертификата из учетной записи службы автоматизации Azure и загрузку и импортирует его в хранилище сертификатов локального компьютера hello на Гибридная рабочая роль подключен toohello учетную запись.  После завершения этого шага, он проверяет, что работника hello прошедшего проверку подлинности tooAzure с помощью hello запуска от имени учетной записи.

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

Сохранить hello *экспорта RunAsCertificateToHybridWorker* runbook tooyour компьютер с `.ps1` расширения.  Импортировать его в учетную запись автоматизации и изменить модуль runbook hello, изменив значение переменной hello hello `$Password` с собственный пароль.  Публикации, а затем запустите runbook hello, предназначенных для hello группу гибридных рабочих ролей, запуска и проверки подлинности модулей Runbook с помощью hello запуска от имени учетной записи.  Hello задания поток отчеты hello попытки tooimport hello сертификат в хранилище локального компьютера hello и следующим с несколькими строками в зависимости от определенных сколько учетных записей автоматизации в подписке, и если проверка выполнена успешно.  

## <a name="troubleshooting-runbooks-on-hybrid-runbook-worker"></a>Устранение неполадок с модулями Runbook в гибридном компоненте Runbook Worker
Журналы сохраняются локально в каждом гибридном компоненте Worker по адресу C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes.  Гибридная рабочая роль также записывает ошибки и события в журнале событий Windows hello под **приложения и службы Logs\Microsoft-SMA\Operational**.  События, связанные toorunbooks выполнения в рабочем процессе hello записываются слишком**приложения и службы Logs\Microsoft-Automation\Operational**.  Hello **Microsoft SMA** журнала включает в себя множество дополнительные события связанные toohello runbook задания занесенный в стек toohello рабочей роли и hello обработку hello модуля Runbook.  При hello **автоматизации Microsoft** журнала событий не имеет большое количество событий с подробными сведениями, помощь в устранении неполадок hello выполнения runbook, по крайней мере, вы найдете hello результатов задания runbook hello.  

[Runbook, выходные и сообщений](automation-runbook-output-and-messages.md) отправляются tooAzure автоматизации из гибридные рабочие роли точно так же, как и задания runbook выполняются в облаке hello.  Можно также включить hello Verbose и hello потоков выполняется таким же способом, что и для других модулей Runbook.  

Если модули Runbook не завершаются успешно, и состояние задания hello сводки **Suspended**, см. в статье hello статьи об устранении неполадок [гибридной рабочей роли Runbook: задание runbook завершается с состоянием Приостановить](automation-troubleshooting-hybrid-runbook-worker.md#a-runbook-job-terminates-with-a-status-of-suspended).   

## <a name="next-steps"></a>Дальнейшие действия
* toolearn Дополнительные сведения о hello различные методы, которые можно использовать toostart runbook, в разделе [запуск Runbook в автоматизации Azure](automation-starting-a-runbook.md).  
* . в разделе toounderstand hello разные процедуры для работы с PowerShell и рабочий процесс PowerShell модули Runbook в автоматизации Azure с помощью текстового редактора hello, [редактирование Runbook в автоматизации Azure](automation-edit-textual-runbook.md)
