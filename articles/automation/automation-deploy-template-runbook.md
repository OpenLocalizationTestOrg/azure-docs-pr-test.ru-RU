---
title: "Развертывание шаблона Azure Resource Manager в runbook службы автоматизации Azure | Документация Майкрософт"
description: "Как развернуть шаблон Azure Resource Manager, хранящийся в службе хранилища Azure, из runbook."
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
ms.openlocfilehash: e511eee2f9eac3969b15ad3d45558dc7034f330a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-an-azure-resource-manager-template-in-an-azure-automation-powershell-runbook"></a><span data-ttu-id="aaf76-104">Развертывание шаблона Azure Resource Manager в runbook PowerShell службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="aaf76-104">Deploy an Azure Resource Manager template in an Azure Automation PowerShell runbook</span></span>

<span data-ttu-id="aaf76-105">Можно написать [runbook PowerShell службы автоматизации Azure](automation-first-runbook-textual-powershell.md), который развертывает ресурс Azure с помощью [шаблона управления ресурсами Azure](../azure-resource-manager/resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="aaf76-105">You can write an [Azure Automation PowerShell runbook](automation-first-runbook-textual-powershell.md) that deploys an Azure resource by using an [Azure Resource Management template](../azure-resource-manager/resource-manager-create-first-template.md).</span></span>

<span data-ttu-id="aaf76-106">Таким образом можно автоматизировать развертывание ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="aaf76-106">By doing this, you can automate deployment of Azure resources.</span></span> <span data-ttu-id="aaf76-107">Можно хранить шаблоны Resource Manager в центральном безопасном сетевом расположении, например в службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="aaf76-107">You can maintain your Resource Manager templates in a central,secure location such as Azure Storage.</span></span>

<span data-ttu-id="aaf76-108">В этом разделе мы создадим runbook PowerShell, использующий шаблон Resource Manager, который расположен в [службе хранилища Azure](../storage/common/storage-introduction.md), для развертывания новой учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="aaf76-108">In this topic, we create a PowerShell runbook that uses an Resource Manager template stored in [Azure Storage](../storage/common/storage-introduction.md) to deploy a new Azure Storage account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aaf76-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="aaf76-109">Prerequisites</span></span>

<span data-ttu-id="aaf76-110">Для работы с этим учебником требуется:</span><span class="sxs-lookup"><span data-stu-id="aaf76-110">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="aaf76-111">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="aaf76-111">Azure subscription.</span></span> <span data-ttu-id="aaf76-112">Если у вас ее нет, [активируйте преимущества для подписчиков MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) или <a href="/pricing/free-account/" target="_blank">[зарегистрируйте бесплатную учетную запись](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="aaf76-112">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or <a href="/pricing/free-account/" target="_blank">[sign up for a free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="aaf76-113">[Учетная запись службы автоматизации](automation-sec-configure-azure-runas-account.md) , чтобы хранить модуль Runbook и выполнять проверку подлинности ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="aaf76-113">[Automation account](automation-sec-configure-azure-runas-account.md) to hold the runbook and authenticate to Azure resources.</span></span>  <span data-ttu-id="aaf76-114">Эта учетная запись должна иметь разрешение на запуск и остановку виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="aaf76-114">This account must have permission to start and stop the virtual machine.</span></span>
* <span data-ttu-id="aaf76-115">[Учетная запись хранения Azure](../storage/common/storage-create-storage-account.md) для хранения шаблона Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="aaf76-115">[Azure Storage account](../storage/common/storage-create-storage-account.md) in which to store the Resource Manager template</span></span>
* <span data-ttu-id="aaf76-116">Azure PowerShell, установленный на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="aaf76-116">Azure Powershell installed on a local machine.</span></span> <span data-ttu-id="aaf76-117">Дополнительные сведения о получении Azure PowerShell см. в статье [Install and configure Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) (Установка и настройка Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="aaf76-117">See [Install and configure Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) for information about how to get Azure PowerShell.</span></span>

## <a name="create-the-resource-manager-template"></a><span data-ttu-id="aaf76-118">Создание шаблона Resource Manager</span><span class="sxs-lookup"><span data-stu-id="aaf76-118">Create the Resource Manager template</span></span>

<span data-ttu-id="aaf76-119">В этом примере мы используем шаблон Resource Manager, который развертывает новую учетную запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="aaf76-119">For this example, we use an Resource Manager template that deploys a new Azure Storage account.</span></span>

<span data-ttu-id="aaf76-120">Скопируйте приведенный ниже текст в текстовый редактор.</span><span class="sxs-lookup"><span data-stu-id="aaf76-120">In a text editor, copy the following text:</span></span>

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

<span data-ttu-id="aaf76-121">Сохраните файл локально как `TemplateTest.json`.</span><span class="sxs-lookup"><span data-stu-id="aaf76-121">Save the file locally as `TemplateTest.json`.</span></span>

## <a name="save-the-resource-manager-template-in-azure-storage"></a><span data-ttu-id="aaf76-122">Сохранение шаблона Resource Manager в службе хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="aaf76-122">Save the Resource Manager template in Azure Storage</span></span>

<span data-ttu-id="aaf76-123">Теперь мы используем PowerShell, чтобы создать файловый ресурс службы хранилища Azure, и передадим в него файл `TemplateTest.json`.</span><span class="sxs-lookup"><span data-stu-id="aaf76-123">Now we use PowerShell to create an Azure Storage file share and upload the `TemplateTest.json` file.</span></span>
<span data-ttu-id="aaf76-124">Инструкции по созданию файлового ресурса и передаче файла на портал Azure см. в разделе [Приступая к работе с хранилищем файлов Azure в Windows](../storage/files/storage-dotnet-how-to-use-files.md).</span><span class="sxs-lookup"><span data-stu-id="aaf76-124">For instructions on how to create a file share and upload a file in the Azure portal, see [Get started with Azure File storage on Windows](../storage/files/storage-dotnet-how-to-use-files.md).</span></span>

<span data-ttu-id="aaf76-125">Запустите PowerShell на локальном компьютере и выполните приведенные команды, чтобы создать файловый ресурс и передать в него шаблон Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="aaf76-125">Launch PowerShell on your local machine, and run the following commands to create a file share and upload the Resource Manager template to that file share.</span></span>

```powershell
# Login to Azure
Login-AzureRmAccount

# Get the access key for your storage account
$key = Get-AzureRmStorageAccountKey -ResourceGroupName 'MyAzureAccount' -Name 'MyStorageAccount'

# Create an Azure Storage context using the first access key
$context = New-AzureStorageContext -StorageAccountName 'MyStorageAccount' -StorageAccountKey $key[0].value

# Create a file share named 'resource-templates' in your Azure Storage account
$fileShare = New-AzureStorageShare -Name 'resource-templates' -Context $context

# Add the TemplateTest.json file to the new file share
# "TemplatePath" is the path where you saved the TemplateTest.json file
$templateFile = 'C:\TemplatePath'
Set-AzureStorageFileContent -ShareName $fileShare.Name -Context $context -Source $templateFile
```

## <a name="create-the-powershell-runbook-script"></a><span data-ttu-id="aaf76-126">Создание сценария runbook PowerShell</span><span class="sxs-lookup"><span data-stu-id="aaf76-126">Create the PowerShell runbook script</span></span>

<span data-ttu-id="aaf76-127">Теперь мы создадим сценарий PowerShell, который получает файл `TemplateTest.json` из службы хранилища Azure и развертывает шаблон для создания новой учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="aaf76-127">Now we create a PowerShell script that gets the `TemplateTest.json` file from Azure Storage and deploys the template to create a new Azure Storage account.</span></span>

<span data-ttu-id="aaf76-128">Вставьте приведенный ниже текст в текстовый редактор.</span><span class="sxs-lookup"><span data-stu-id="aaf76-128">In a text editor, paste the following text:</span></span>

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



# Authenticate to Azure if running from Azure Automation
$ServicePrincipalConnection = Get-AutomationConnection -Name "AzureRunAsConnection"
Add-AzureRmAccount `
    -ServicePrincipal `
    -TenantId $ServicePrincipalConnection.TenantId `
    -ApplicationId $ServicePrincipalConnection.ApplicationId `
    -CertificateThumbprint $ServicePrincipalConnection.CertificateThumbprint | Write-Verbose

#Set the parameter values for the Resource Manager template
$Parameters = @{
    "storageAccountType"="Standard_LRS"
    }

# Create a new context
$Context = New-AzureStorageContext -StorageAccountKey $StorageAccountKey

Get-AzureStorageFileContent -ShareName 'resource-templates' -Context $Context -path 'TemplateTest.json' -Destination 'C:\Temp'

$TemplateFile = Join-Path -Path 'C:\Temp' -ChildPath $StorageFileName

# Deploy the storage account
New-AzureRmResourceGroupDeployment -ResourceGroupName $ResourceGroupName -TemplateFile $TemplateFile -TemplateParameterObject $Parameters 
``` 

<span data-ttu-id="aaf76-129">Сохраните файл локально как `DeployTemplate.ps1`.</span><span class="sxs-lookup"><span data-stu-id="aaf76-129">Save the file locally as `DeployTemplate.ps1`.</span></span>

## <a name="import-and-publish-the-runbook-into-your-azure-automation-account"></a><span data-ttu-id="aaf76-130">Импорт runbook в учетную запись службы автоматизации Azure и его публикация</span><span class="sxs-lookup"><span data-stu-id="aaf76-130">Import and publish the runbook into your Azure Automation account</span></span>

<span data-ttu-id="aaf76-131">Теперь мы используем PowerShell, чтобы импортировать runbook в учетную запись службы автоматизации Azure, а затем опубликовать его.</span><span class="sxs-lookup"><span data-stu-id="aaf76-131">Now we use PowerShell to import the runbook into your Azure Automation account, and then publish the runbook.</span></span>
<span data-ttu-id="aaf76-132">Сведения о том, как импортировать и опубликовать runbook на портале Azure, см. в разделе [Создание или импорт модуля Runbook в службе автоматизации Azure](automation-creating-importing-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="aaf76-132">For information about how to import and publish a runbook in the Azure portal, see [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md).</span></span>

<span data-ttu-id="aaf76-133">Чтобы импортировать `DeployTemplate.ps1` в свою учетную запись автоматизации как runbook PowerShell, выполните следующие команды PowerShell.</span><span class="sxs-lookup"><span data-stu-id="aaf76-133">To import `DeployTemplate.ps1` into your Automation account as a PowerShell runbook, run the following PowerShell commands:</span></span>

```powershell
# MyPath is the path where you saved DeployTemplate.ps1
# MyResourceGroup is the name of the Azure ResourceGroup that contains your Azure Automation account
# MyAutomationAccount is the name of your Automation account
$importParams = @{
    Path = 'C:\MyPath\DeployTemplate.ps1'
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Type = 'PowerShell'
}
Import-AzureRmAutomationRunbook @

# Publish the runbook
$publishParams = @{
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Name = 'DeployTemplate'
}
Publish-AzureRmAutomationRunbook @publishParams
```

## <a name="start-the-runbook"></a><span data-ttu-id="aaf76-134">Запуск модуля runbook</span><span class="sxs-lookup"><span data-stu-id="aaf76-134">Start the runbook</span></span>

<span data-ttu-id="aaf76-135">Теперь мы запустим runbook, вызвав командлет [AzureRmAutomationRunbook начала](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook?view=azurermps-4.1.0).</span><span class="sxs-lookup"><span data-stu-id="aaf76-135">Now we start the runbook by calling the [Start-AzureRmAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook?view=azurermps-4.1.0) cmdlet.</span></span>

<span data-ttu-id="aaf76-136">Сведения о том, как запустить runbook на портале Azure, см. в разделе [Запуск модуля Runbook в службе автоматизации Azure](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="aaf76-136">For information about how to start a runbook in the Azure portal, see [Starting a runbook in Azure Automation](automation-starting-a-runbook.md).</span></span>

<span data-ttu-id="aaf76-137">В консоли PowerShell выполните следующие команды.</span><span class="sxs-lookup"><span data-stu-id="aaf76-137">Run the following commands in the PowerShell console:</span></span>

```powershell
# Set up the parameters for the runbook
$runbookParams = @{
    ResourceGroupName = 'MyResourceGroup'
    StorageAccountName = 'MyStorageAccount'
    StorageAccountKey = $key[0].Value # We got this key earlier
    StorageFileName = 'TemplateTest.json' 
}

# Set up parameters for the Start-AzureRmAutomationRunbook cmdlet
$startParams = @{
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Name = 'DeployTemplate'
    Parameters = $runbookParams
}

# Start the runbook
$job = Start-AzureRmAutomationRunbook @startParams
```

<span data-ttu-id="aaf76-138">Запустится runbook. Его состояние можно проверить, выполнив команду `$job.Status`.</span><span class="sxs-lookup"><span data-stu-id="aaf76-138">The runbook runs, and you can check its status by running `$job.Status`.</span></span>

<span data-ttu-id="aaf76-139">Модуль runbook получает шаблон Resource Manager и использует его для развертывания новой учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="aaf76-139">The runbook gets the Resource Manager template and uses it to deploy a new Azure Storage account.</span></span>
<span data-ttu-id="aaf76-140">Вы увидите, что учетная запись хранения создана, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="aaf76-140">You can see that the new storage account was created by running the following command:</span></span>
```powershell
Get-AzureRmStorageAccount
```

## <a name="summary"></a><span data-ttu-id="aaf76-141">Сводка</span><span class="sxs-lookup"><span data-stu-id="aaf76-141">Summary</span></span>

<span data-ttu-id="aaf76-142">Вот и все!</span><span class="sxs-lookup"><span data-stu-id="aaf76-142">That's it!</span></span> <span data-ttu-id="aaf76-143">Теперь с помощью службы автоматизации Azure, службы хранилища Azure и шаблонов Resource Manager можно развернуть все свои ресурсы Azure.</span><span class="sxs-lookup"><span data-stu-id="aaf76-143">Now you can use Azure Automation and Azure Storage, and Resource Manager templates to deploy all your Azure resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aaf76-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="aaf76-144">Next steps</span></span>

* <span data-ttu-id="aaf76-145">Дополнительные сведения о шаблонах Resource Manager см. в статье [Общие сведения о диспетчере ресурсов Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="aaf76-145">To learn more about Resource Manager templates, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md)</span></span>
* <span data-ttu-id="aaf76-146">Чтобы приступить к работе со службой хранилища Azure, изучите раздел [Введение в хранилище Microsoft Azure](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="aaf76-146">To get started with Azure Storage, see [Introduction to Azure Storage](../storage/common/storage-introduction.md).</span></span>
* <span data-ttu-id="aaf76-147">Другие полезные runbook службы автоматизации Azure приведены в разделе [Коллекции модулей Runbook и других модулей для службы автоматизации Azure](automation-runbook-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="aaf76-147">To find other useful Azure Automation runbooks, see [Runbook and module galleries for Azure Automation](automation-runbook-gallery.md).</span></span>
* <span data-ttu-id="aaf76-148">Другие полезные шаблоны Resource Manager можно найти на странице [Шаблоны быстрого запуска Azure](https://azure.microsoft.com/resources/templates/).</span><span class="sxs-lookup"><span data-stu-id="aaf76-148">To find other useful Resource Manager templates, see [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/)</span></span>

