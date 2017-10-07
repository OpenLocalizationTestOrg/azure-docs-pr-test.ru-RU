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
# <a name="test-azure-automation-run-as-account-authentication"></a>Тестирование проверки подлинности учетной записи запуска от имени службы автоматизации Azure
После успешного создания учетной записи автоматизации можно выполнять tooconfirm простой тест, можно toosuccessfully проверку подлинности в Azure Resource Manager или развертывания Azure классические вновь созданных или обновленных автоматизации Запуск от имени учетной записи.    

## <a name="automation-run-as-authentication"></a>Проверка подлинности учетной записи запуска от имени службы автоматизации
Используйте hello в образце кода ниже слишком[создать PowerShell runbook](automation-creating-importing-runbook.md) tooverify проверки подлинности с помощью hello запустите от имени учетной записи, так и в вашей настраиваемой документации по задачам tooauthenticate и управление ресурсами диспетчера ресурсов с помощью учетной записи автоматизации.   

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

Обратите внимание, hello командлет, используемый для проверки подлинности в модуле runbook hello - **добавить AzureRmAccount**, использует hello *ServicePrincipalCertificate* набор параметров.  Он выполняет проверку подлинности с помощью сертификата субъекта-службы, а не учетных данных.  

При вы [запуска модуля runbook hello](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate учетной записи запуска от имени [задание runbook](automation-runbook-execution.md) — создан, отображается колонке hello задания, а состояние задания hello в hello **Сводка заданий**плитки. состояние задания Hello будет запускаться как *в очереди* означает, что он ожидает runbook worker в доступных toobecome облака hello. Он будет двигаться слишком*запуск* когда исполнитель задания hello, а затем *под управлением* при hello runbook фактически начинает выполнение.  После завершения задания runbook hello, мы должны увидеть состояние **завершено**.

toosee Здравствуйте подробные результаты hello runbook, щелкните hello **вывода** плитки.  На hello **вывода** колонку, вы увидите ее успешной проверки подлинности и возвращает список всех ресурсов во всех группах ресурсов в вашей подписке.  

Необходимо помнить tooremove hello блок кода, начиная с комментария hello `#Get all ARM resources from all resource groups` при повторном использовании кода hello для Runbook.

## <a name="classic-run-as-authentication"></a>Проверка подлинности классической учетной записи запуска от имени
Используйте hello в образце кода ниже слишком[создать PowerShell runbook](automation-creating-importing-runbook.md) tooverify проверки подлинности с помощью классической "hello" запустите от имени учетной записи, так и в вашей настраиваемой документации по задачам tooauthenticate ресурсы и управлять ими в hello классической модели развертывания.  

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

При вы [запуска модуля runbook hello](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate учетной записи запуска от имени [задание runbook](automation-runbook-execution.md) — создан, отображается колонке hello задания, а состояние задания hello в hello **Сводка заданий**плитки. состояние задания Hello будет запускаться как *в очереди* означает, что он ожидает runbook worker в доступных toobecome облака hello. Он будет двигаться слишком*запуск* когда исполнитель задания hello, а затем *под управлением* при hello runbook фактически начинает выполнение.  После завершения задания runbook hello, мы должны увидеть состояние **завершено**.

toosee Здравствуйте подробные результаты hello runbook, щелкните hello **вывода** плитки.  На hello **вывода** колонку, вы увидите ее успешной проверки подлинности и возвращает список всех виртуальных машин Azure, VMName, развернутых в подписке.  

Необходимо помнить командлет hello tooremove **Get-AzureVM** при повторном использовании кода hello для Runbook.

## <a name="next-steps"></a>Дальнейшие действия
* tooget к работе с PowerShell модули Runbook в разделе [Мой первый runbook PowerShell](automation-first-runbook-textual-powershell.md).
* toolearn Дополнительные сведения о графических разработки. в разделе [графический разработки в Azure Automation](automation-graphical-authoring-intro.md).
