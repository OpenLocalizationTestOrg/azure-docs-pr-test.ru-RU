---
title: "aaaDeploy шаблона диспетчера ресурсов Azure в runbook службы автоматизации Azure | Документы Microsoft"
description: "Как toodeploy шаблона диспетчера ресурсов Azure хранятся в хранилище Azure из модуля runbook"
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
keywords: "powershell, runbook, json, служба автоматизации azure"
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 07/09/2017
ms.author: eslesar
ms.openlocfilehash: f489a8e8635a48f5a6a2f1a88e1c803f56f01832
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-azure-resource-manager-template-in-an-azure-automation-powershell-runbook"></a>Развертывание шаблона Azure Resource Manager в runbook PowerShell службы автоматизации Azure

Можно написать [runbook PowerShell службы автоматизации Azure](automation-first-runbook-textual-powershell.md), который развертывает ресурс Azure с помощью [шаблона управления ресурсами Azure](../azure-resource-manager/resource-manager-create-first-template.md).

Таким образом можно автоматизировать развертывание ресурсов Azure. Можно хранить шаблоны Resource Manager в центральном безопасном сетевом расположении, например в службе хранилища Azure.

В этом разделе мы создадим runbook PowerShell, использующий шаблон диспетчера ресурсов, хранящихся в [хранилища Azure](../storage/common/storage-introduction.md) toodeploy новую учетную запись хранилища Azure.

## <a name="prerequisites"></a>Предварительные требования

toocomplete этого учебника требуется hello следующие:

* Подписка Azure. Если у вас ее нет, [активируйте преимущества для подписчиков MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) или <a href="/pricing/free-account/" target="_blank">[зарегистрируйте бесплатную учетную запись](https://azure.microsoft.com/free/).
* [Учетная запись службы автоматизации](automation-sec-configure-azure-runas-account.md) toohold hello runbook и проверить подлинность tooAzure ресурсов.  Этой учетной записи необходимо разрешение toostart и остановить виртуальную машину hello.
* [Учетная запись хранения Azure](../storage/common/storage-create-storage-account.md) в какой из шаблонов диспетчера ресурсов toostore hello
* Azure PowerShell, установленный на локальном компьютере. В разделе [Установка и настройка Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) сведения о том, как tooget Azure PowerShell.

## <a name="create-hello-resource-manager-template"></a>Создание шаблона диспетчера ресурсов hello

В этом примере мы используем шаблон Resource Manager, который развертывает новую учетную запись хранения Azure.

В текстовом редакторе скопируйте hello следующий текст:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccountType": {
      "type": "string",
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS",
        "Premium_LRS"
      ],
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "sku": {
          "name": "[parameters('storageAccountType')]"
      },
      "kind": "Storage", 
      "properties": {
      }
    }
  ],
  "outputs": {
      "storageAccountName": {
          "type": "string",
          "value": "[variables('storageAccountName')]"
      }
  }
}
```

Сохраните файл hello локально как `TemplateTest.json`.

## <a name="save-hello-resource-manager-template-in-azure-storage"></a>Сохранение шаблона диспетчера ресурсов hello в хранилище Azure

Теперь мы используем toocreate PowerShell файловый ресурс службы хранилища Azure и отправить hello `TemplateTest.json` файла.
Инструкции о предоставлении совместного использования toocreate файл и отправить файл на портал Azure hello см [приступить к работе с хранилищем Windows Azure файл](../storage/files/storage-dotnet-how-to-use-files.md).

Запустите PowerShell на локальном компьютере и запустите hello, следующие команды toocreate общую папку отправить hello диспетчера ресурсов шаблона toothat общей папки.

```powershell
# Login tooAzure
Login-AzureRmAccount

# Get hello access key for your storage account
$key = Get-AzureRmStorageAccountKey -ResourceGroupName 'MyAzureAccount' -Name 'MyStorageAccount'

# Create an Azure Storage context using hello first access key
$context = New-AzureStorageContext -StorageAccountName 'MyStorageAccount' -StorageAccountKey $key[0].value

# Create a file share named 'resource-templates' in your Azure Storage account
$fileShare = New-AzureStorageShare -Name 'resource-templates' -Context $context

# Add hello TemplateTest.json file toohello new file share
# "TemplatePath" is hello path where you saved hello TemplateTest.json file
$templateFile = 'C:\TemplatePath'
Set-AzureStorageFileContent -ShareName $fileShare.Name -Context $context -Source $templateFile
```

## <a name="create-hello-powershell-runbook-script"></a>Создать сценарий runbook PowerShell hello

Теперь мы создайте сценарий PowerShell, который возвращает hello `TemplateTest.json` файла из хранилища Azure и развертывает toocreate шаблона hello новую учетную запись хранилища Azure.

В текстовом редакторе вставьте hello следующий текст:

```powershell
param (
    [Parameter(Mandatory=$true)]
    [string]
    $ResourceGroupName,

    [Parameter(Mandatory=$true)]
    [string]
    $StorageAccountName,

    [Parameter(Mandatory=$true)]
    [string]
    $StorageAccountKey,

    [Parameter(Mandatory=$true)]
    [string]
    $StorageFileName
)



# Authenticate tooAzure if running from Azure Automation
$ServicePrincipalConnection = Get-AutomationConnection -Name "AzureRunAsConnection"
Add-AzureRmAccount `
    -ServicePrincipal `
    -TenantId $ServicePrincipalConnection.TenantId `
    -ApplicationId $ServicePrincipalConnection.ApplicationId `
    -CertificateThumbprint $ServicePrincipalConnection.CertificateThumbprint | Write-Verbose

#Set hello parameter values for hello Resource Manager template
$Parameters = @{
    "storageAccountType"="Standard_LRS"
    }

# Create a new context
$Context = New-AzureStorageContext -StorageAccountKey $StorageAccountKey

Get-AzureStorageFileContent -ShareName 'resource-templates' -Context $Context -path 'TemplateTest.json' -Destination 'C:\Temp'

$TemplateFile = Join-Path -Path 'C:\Temp' -ChildPath $StorageFileName

# Deploy hello storage account
New-AzureRmResourceGroupDeployment -ResourceGroupName $ResourceGroupName -TemplateFile $TemplateFile -TemplateParameterObject $Parameters 
``` 

Сохраните файл hello локально как `DeployTemplate.ps1`.

## <a name="import-and-publish-hello-runbook-into-your-azure-automation-account"></a>Импорт и опубликовать hello runbook в учетную запись службы автоматизации Azure

Теперь мы использовать модуль hello tooimport PowerShell в учетную запись службы автоматизации Azure, а затем опубликовать hello runbook.
Сведения о том, как tooimport и опубликовать книгу в hello портала Azure см. в разделе [Создание или импорт модуля runbook в автоматизации Azure](automation-creating-importing-runbook.md).

tooimport `DeployTemplate.ps1` в вашу учетную запись автоматизации, как PowerShell runbook, запустите следующие команды PowerShell hello:

```powershell
# MyPath is hello path where you saved DeployTemplate.ps1
# MyResourceGroup is hello name of hello Azure ResourceGroup that contains your Azure Automation account
# MyAutomationAccount is hello name of your Automation account
$importParams = @{
    Path = 'C:\MyPath\DeployTemplate.ps1'
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Type = 'PowerShell'
}
Import-AzureRmAutomationRunbook @

# Publish hello runbook
$publishParams = @{
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Name = 'DeployTemplate'
}
Publish-AzureRmAutomationRunbook @publishParams
```

## <a name="start-hello-runbook"></a>Запустить hello runbook

Теперь мы начнем hello runbook с вызывающему Привет [AzureRmAutomationRunbook начала](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook?view=azurermps-4.1.0) командлета.

Сведения о том, как toostart runbook в hello портал Azure отображается [запуск runbook в автоматизации Azure](automation-starting-a-runbook.md).

Выполните следующие команды в консоль PowerShell hello hello.

```powershell
# Set up hello parameters for hello runbook
$runbookParams = @{
    ResourceGroupName = 'MyResourceGroup'
    StorageAccountName = 'MyStorageAccount'
    StorageAccountKey = $key[0].Value # We got this key earlier
    StorageFileName = 'TemplateTest.json' 
}

# Set up parameters for hello Start-AzureRmAutomationRunbook cmdlet
$startParams = @{
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Name = 'DeployTemplate'
    Parameters = $runbookParams
}

# Start hello runbook
$job = Start-AzureRmAutomationRunbook @startParams
```

Здравствуйте, runbook выполняется, а его состояние можно проверить, запустив `$job.Status`.

Hello runbook получает шаблона диспетчера ресурсов hello и использует его toodeploy новую учетную запись хранилища Azure.
Вы можете увидеть создания новой учетной записи хранения hello, выполнив следующую команду hello:
```powershell
Get-AzureRmStorageAccount
```

## <a name="summary"></a>Сводка

Вот и все! Теперь можно использовать все ресурсы Azure-службы автоматизации Azure и хранилища Azure и toodeploy шаблонов диспетчера ресурсов.

## <a name="next-steps"></a>Дальнейшие действия

* toolearn Дополнительные сведения о шаблонах диспетчера ресурсов. в разделе [Обзор диспетчера ресурсов Azure](../azure-resource-manager/resource-group-overview.md)
* tooget к работе с хранилищем Azure. в разделе [tooAzure введение хранилища](../storage/common/storage-introduction.md).
* toofind другие полезные Runbook автоматизации Azure в разделе [Runbook и модулей галерей для службы автоматизации Azure](automation-runbook-gallery.md).
* toofind других полезных шаблонов диспетчера ресурсов см. раздел [шаблоны быстрый запуск Azure](https://azure.microsoft.com/resources/templates/)

