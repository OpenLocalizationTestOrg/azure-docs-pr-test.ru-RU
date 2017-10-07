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
# <a name="deploy-an-azure-resource-manager-template-in-an-azure-automation-powershell-runbook"></a><span data-ttu-id="59087-104">Развертывание шаблона Azure Resource Manager в runbook PowerShell службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="59087-104">Deploy an Azure Resource Manager template in an Azure Automation PowerShell runbook</span></span>

<span data-ttu-id="59087-105">Можно написать [runbook PowerShell службы автоматизации Azure](automation-first-runbook-textual-powershell.md), который развертывает ресурс Azure с помощью [шаблона управления ресурсами Azure](../azure-resource-manager/resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="59087-105">You can write an [Azure Automation PowerShell runbook](automation-first-runbook-textual-powershell.md) that deploys an Azure resource by using an [Azure Resource Management template](../azure-resource-manager/resource-manager-create-first-template.md).</span></span>

<span data-ttu-id="59087-106">Таким образом можно автоматизировать развертывание ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="59087-106">By doing this, you can automate deployment of Azure resources.</span></span> <span data-ttu-id="59087-107">Можно хранить шаблоны Resource Manager в центральном безопасном сетевом расположении, например в службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="59087-107">You can maintain your Resource Manager templates in a central,secure location such as Azure Storage.</span></span>

<span data-ttu-id="59087-108">В этом разделе мы создадим runbook PowerShell, использующий шаблон диспетчера ресурсов, хранящихся в [хранилища Azure](../storage/common/storage-introduction.md) toodeploy новую учетную запись хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="59087-108">In this topic, we create a PowerShell runbook that uses an Resource Manager template stored in [Azure Storage](../storage/common/storage-introduction.md) toodeploy a new Azure Storage account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59087-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="59087-109">Prerequisites</span></span>

<span data-ttu-id="59087-110">toocomplete этого учебника требуется hello следующие:</span><span class="sxs-lookup"><span data-stu-id="59087-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="59087-111">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="59087-111">Azure subscription.</span></span> <span data-ttu-id="59087-112">Если у вас ее нет, [активируйте преимущества для подписчиков MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) или <a href="/pricing/free-account/" target="_blank">[зарегистрируйте бесплатную учетную запись](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="59087-112">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or <a href="/pricing/free-account/" target="_blank">[sign up for a free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="59087-113">[Учетная запись службы автоматизации](automation-sec-configure-azure-runas-account.md) toohold hello runbook и проверить подлинность tooAzure ресурсов.</span><span class="sxs-lookup"><span data-stu-id="59087-113">[Automation account](automation-sec-configure-azure-runas-account.md) toohold hello runbook and authenticate tooAzure resources.</span></span>  <span data-ttu-id="59087-114">Этой учетной записи необходимо разрешение toostart и остановить виртуальную машину hello.</span><span class="sxs-lookup"><span data-stu-id="59087-114">This account must have permission toostart and stop hello virtual machine.</span></span>
* <span data-ttu-id="59087-115">[Учетная запись хранения Azure](../storage/common/storage-create-storage-account.md) в какой из шаблонов диспетчера ресурсов toostore hello</span><span class="sxs-lookup"><span data-stu-id="59087-115">[Azure Storage account](../storage/common/storage-create-storage-account.md) in which toostore hello Resource Manager template</span></span>
* <span data-ttu-id="59087-116">Azure PowerShell, установленный на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="59087-116">Azure Powershell installed on a local machine.</span></span> <span data-ttu-id="59087-117">В разделе [Установка и настройка Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) сведения о том, как tooget Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="59087-117">See [Install and configure Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) for information about how tooget Azure PowerShell.</span></span>

## <a name="create-hello-resource-manager-template"></a><span data-ttu-id="59087-118">Создание шаблона диспетчера ресурсов hello</span><span class="sxs-lookup"><span data-stu-id="59087-118">Create hello Resource Manager template</span></span>

<span data-ttu-id="59087-119">В этом примере мы используем шаблон Resource Manager, который развертывает новую учетную запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="59087-119">For this example, we use an Resource Manager template that deploys a new Azure Storage account.</span></span>

<span data-ttu-id="59087-120">В текстовом редакторе скопируйте hello следующий текст:</span><span class="sxs-lookup"><span data-stu-id="59087-120">In a text editor, copy hello following text:</span></span>

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

<span data-ttu-id="59087-121">Сохраните файл hello локально как `TemplateTest.json`.</span><span class="sxs-lookup"><span data-stu-id="59087-121">Save hello file locally as `TemplateTest.json`.</span></span>

## <a name="save-hello-resource-manager-template-in-azure-storage"></a><span data-ttu-id="59087-122">Сохранение шаблона диспетчера ресурсов hello в хранилище Azure</span><span class="sxs-lookup"><span data-stu-id="59087-122">Save hello Resource Manager template in Azure Storage</span></span>

<span data-ttu-id="59087-123">Теперь мы используем toocreate PowerShell файловый ресурс службы хранилища Azure и отправить hello `TemplateTest.json` файла.</span><span class="sxs-lookup"><span data-stu-id="59087-123">Now we use PowerShell toocreate an Azure Storage file share and upload hello `TemplateTest.json` file.</span></span>
<span data-ttu-id="59087-124">Инструкции о предоставлении совместного использования toocreate файл и отправить файл на портал Azure hello см [приступить к работе с хранилищем Windows Azure файл](../storage/files/storage-dotnet-how-to-use-files.md).</span><span class="sxs-lookup"><span data-stu-id="59087-124">For instructions on how toocreate a file share and upload a file in hello Azure portal, see [Get started with Azure File storage on Windows](../storage/files/storage-dotnet-how-to-use-files.md).</span></span>

<span data-ttu-id="59087-125">Запустите PowerShell на локальном компьютере и запустите hello, следующие команды toocreate общую папку отправить hello диспетчера ресурсов шаблона toothat общей папки.</span><span class="sxs-lookup"><span data-stu-id="59087-125">Launch PowerShell on your local machine, and run hello following commands toocreate a file share and upload hello Resource Manager template toothat file share.</span></span>

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

## <a name="create-hello-powershell-runbook-script"></a><span data-ttu-id="59087-126">Создать сценарий runbook PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="59087-126">Create hello PowerShell runbook script</span></span>

<span data-ttu-id="59087-127">Теперь мы создайте сценарий PowerShell, который возвращает hello `TemplateTest.json` файла из хранилища Azure и развертывает toocreate шаблона hello новую учетную запись хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="59087-127">Now we create a PowerShell script that gets hello `TemplateTest.json` file from Azure Storage and deploys hello template toocreate a new Azure Storage account.</span></span>

<span data-ttu-id="59087-128">В текстовом редакторе вставьте hello следующий текст:</span><span class="sxs-lookup"><span data-stu-id="59087-128">In a text editor, paste hello following text:</span></span>

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

<span data-ttu-id="59087-129">Сохраните файл hello локально как `DeployTemplate.ps1`.</span><span class="sxs-lookup"><span data-stu-id="59087-129">Save hello file locally as `DeployTemplate.ps1`.</span></span>

## <a name="import-and-publish-hello-runbook-into-your-azure-automation-account"></a><span data-ttu-id="59087-130">Импорт и опубликовать hello runbook в учетную запись службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="59087-130">Import and publish hello runbook into your Azure Automation account</span></span>

<span data-ttu-id="59087-131">Теперь мы использовать модуль hello tooimport PowerShell в учетную запись службы автоматизации Azure, а затем опубликовать hello runbook.</span><span class="sxs-lookup"><span data-stu-id="59087-131">Now we use PowerShell tooimport hello runbook into your Azure Automation account, and then publish hello runbook.</span></span>
<span data-ttu-id="59087-132">Сведения о том, как tooimport и опубликовать книгу в hello портала Azure см. в разделе [Создание или импорт модуля runbook в автоматизации Azure](automation-creating-importing-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="59087-132">For information about how tooimport and publish a runbook in hello Azure portal, see [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md).</span></span>

<span data-ttu-id="59087-133">tooimport `DeployTemplate.ps1` в вашу учетную запись автоматизации, как PowerShell runbook, запустите следующие команды PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="59087-133">tooimport `DeployTemplate.ps1` into your Automation account as a PowerShell runbook, run hello following PowerShell commands:</span></span>

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

## <a name="start-hello-runbook"></a><span data-ttu-id="59087-134">Запустить hello runbook</span><span class="sxs-lookup"><span data-stu-id="59087-134">Start hello runbook</span></span>

<span data-ttu-id="59087-135">Теперь мы начнем hello runbook с вызывающему Привет [AzureRmAutomationRunbook начала](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook?view=azurermps-4.1.0) командлета.</span><span class="sxs-lookup"><span data-stu-id="59087-135">Now we start hello runbook by calling hello [Start-AzureRmAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook?view=azurermps-4.1.0) cmdlet.</span></span>

<span data-ttu-id="59087-136">Сведения о том, как toostart runbook в hello портал Azure отображается [запуск runbook в автоматизации Azure](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="59087-136">For information about how toostart a runbook in hello Azure portal, see [Starting a runbook in Azure Automation](automation-starting-a-runbook.md).</span></span>

<span data-ttu-id="59087-137">Выполните следующие команды в консоль PowerShell hello hello.</span><span class="sxs-lookup"><span data-stu-id="59087-137">Run hello following commands in hello PowerShell console:</span></span>

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

<span data-ttu-id="59087-138">Здравствуйте, runbook выполняется, а его состояние можно проверить, запустив `$job.Status`.</span><span class="sxs-lookup"><span data-stu-id="59087-138">hello runbook runs, and you can check its status by running `$job.Status`.</span></span>

<span data-ttu-id="59087-139">Hello runbook получает шаблона диспетчера ресурсов hello и использует его toodeploy новую учетную запись хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="59087-139">hello runbook gets hello Resource Manager template and uses it toodeploy a new Azure Storage account.</span></span>
<span data-ttu-id="59087-140">Вы можете увидеть создания новой учетной записи хранения hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="59087-140">You can see that hello new storage account was created by running hello following command:</span></span>
```powershell
Get-AzureRmStorageAccount
```

## <a name="summary"></a><span data-ttu-id="59087-141">Сводка</span><span class="sxs-lookup"><span data-stu-id="59087-141">Summary</span></span>

<span data-ttu-id="59087-142">Вот и все!</span><span class="sxs-lookup"><span data-stu-id="59087-142">That's it!</span></span> <span data-ttu-id="59087-143">Теперь можно использовать все ресурсы Azure-службы автоматизации Azure и хранилища Azure и toodeploy шаблонов диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="59087-143">Now you can use Azure Automation and Azure Storage, and Resource Manager templates toodeploy all your Azure resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="59087-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="59087-144">Next steps</span></span>

* <span data-ttu-id="59087-145">toolearn Дополнительные сведения о шаблонах диспетчера ресурсов. в разделе [Обзор диспетчера ресурсов Azure](../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="59087-145">toolearn more about Resource Manager templates, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md)</span></span>
* <span data-ttu-id="59087-146">tooget к работе с хранилищем Azure. в разделе [tooAzure введение хранилища](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="59087-146">tooget started with Azure Storage, see [Introduction tooAzure Storage](../storage/common/storage-introduction.md).</span></span>
* <span data-ttu-id="59087-147">toofind другие полезные Runbook автоматизации Azure в разделе [Runbook и модулей галерей для службы автоматизации Azure](automation-runbook-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="59087-147">toofind other useful Azure Automation runbooks, see [Runbook and module galleries for Azure Automation](automation-runbook-gallery.md).</span></span>
* <span data-ttu-id="59087-148">toofind других полезных шаблонов диспетчера ресурсов см. раздел [шаблоны быстрый запуск Azure](https://azure.microsoft.com/resources/templates/)</span><span class="sxs-lookup"><span data-stu-id="59087-148">toofind other useful Resource Manager templates, see [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/)</span></span>

