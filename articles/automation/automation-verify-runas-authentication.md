---
title: "Проверка конфигурации учетной записи службы автоматизации Azure | Документация Майкрософт"
description: "В этой статье описывается проверка правильной настройки конфигурации учетной записи службы автоматизации."
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
ms.openlocfilehash: 804e05f596e1d6d5f650e4c94a18eff6b7c3ba4e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="test-azure-automation-run-as-account-authentication"></a>Тестирование проверки подлинности учетной записи запуска от имени службы автоматизации Azure
После успешного создания учетной записи службы автоматизации можно выполнить простой тест, чтобы убедиться, что вы сможете успешно пройти проверку подлинности в Azure Resource Manager или в классическом развертывании Azure с помощью созданной или обновленной учетной записи запуска от имени службы автоматизации.    

## <a name="automation-run-as-authentication"></a>Проверка подлинности учетной записи запуска от имени службы автоматизации
Используйте пример кода ниже для [создания Runbook PowerShell](automation-creating-importing-runbook.md), чтобы выполнить проверку подлинности с помощью учетной записи запуска от имени. Используйте этот код и в пользовательских модулях Runbook, чтобы выполнить проверку подлинности ресурсов в диспетчере ресурсов и управлять ими с помощью учетной записи службы автоматизации.   

    $connectionName = "AzureRunAsConnection"
    try
    {
        # Get the connection "AzureRunAsConnection "
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

        "Logging in to Azure..."
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

Обратите внимание, что командлет **Add-AzureRmAccount**, применяемый для проверки подлинности в модуле Runbook, использует набор параметров *ServicePrincipalCertificate* .  Он выполняет проверку подлинности с помощью сертификата субъекта-службы, а не учетных данных.  

При [запуске модуля Runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) для проверки подлинности учетной записи запуска от имени будет создано [задание Runbook](automation-runbook-execution.md), откроется колонка "Задание", а состояние задания будет отображаться на плитке **Сводка по заданию**. Сначала задание получает состояние *В очереди* , указывающее на то, что задание ожидает, пока рабочая роль Runbook в облаке станет доступной. Как только рабочая роль затребует задание, оно получит состояние *Запущено*, а с началом фактического выполнения модуля Runbook — состояние *Выполняется*.  После выполнения задания Runbook должно отобразиться состояние **Выполнено**.

Чтобы просмотреть подробные результаты задания Runbook, щелкните плитку **Выходные данные** .  В колонке **Выходные данные** должна быть информация о том, что модуль прошел проверку подлинности и вернул список всех ресурсов во всех группах ресурсов подписки.  

Не забудьте удалить блок кода, начиная с комментария `#Get all ARM resources from all resource groups`, при его повторном использовании для модулей Runbook.

## <a name="classic-run-as-authentication"></a>Проверка подлинности классической учетной записи запуска от имени
Используйте пример кода ниже для [создания Runbook PowerShell](automation-creating-importing-runbook.md), чтобы выполнить проверку подлинности с помощью классической учетной записи запуска от имени. Используйте этот код и в пользовательских модулях Runbook, чтобы выполнить проверку подлинности ресурсов и управлять ими в классической модели развертывания.  

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get the connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate to Azure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in the Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting the certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in the Automation account."
    }

    Write-Verbose "Authenticating to Azure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID
    
    #Get all VMs in the subscription and return list with name of each
    Get-AzureVM | ft Name

При [запуске модуля Runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) для проверки подлинности учетной записи запуска от имени будет создано [задание Runbook](automation-runbook-execution.md), откроется колонка "Задание", а состояние задания будет отображаться на плитке **Сводка по заданию**. Сначала задание получает состояние *В очереди* , указывающее на то, что задание ожидает, пока рабочая роль Runbook в облаке станет доступной. Как только рабочая роль затребует задание, оно получит состояние *Запущено*, а с началом фактического выполнения модуля Runbook — состояние *Выполняется*.  После выполнения задания Runbook должно отобразиться состояние **Выполнено**.

Чтобы просмотреть подробные результаты задания Runbook, щелкните плитку **Выходные данные** .  В колонке **Выходные данные** должна быть информация о том, что модуль прошел проверку подлинности и вернул список всех виртуальных машин по имени, развернутых в подписке.  

Не забудьте удалить командлет **Get-AzureVM** при повторном использовании кода для модулей Runbook.

## <a name="next-steps"></a>Дальнейшие действия
* Сведения о том, как начать работу с модулями Runbook, см. в статье [Мой первый модуль Runbook PowerShell](automation-first-runbook-textual-powershell.md).
* Дополнительные сведения о графической разработке в службе автоматизации Azure см. в [этой статье](automation-graphical-authoring-intro.md).
