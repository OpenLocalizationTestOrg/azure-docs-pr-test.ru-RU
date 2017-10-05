---
title: "Экспорт шаблона Resource Manager с помощью Azure PowerShell | Документация Майкрософт"
description: "Используйте Azure Resource Manager и Azure PowerShell для экспорта шаблона из группы ресурсов."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/01/2017
ms.author: tomfitz
ms.openlocfilehash: 7543811eb9448222b6e7c266756e68debc7d54be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="export-azure-resource-manager-templates-with-powershell"></a><span data-ttu-id="4dbea-103">Экспорт шаблонов Azure Resource Manager с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="4dbea-103">Export Azure Resource Manager templates with PowerShell</span></span>

<span data-ttu-id="4dbea-104">Resource Manager позволяет экспортировать шаблон из существующих ресурсов в подписке.</span><span class="sxs-lookup"><span data-stu-id="4dbea-104">Resource Manager enables you to export a Resource Manager template from existing resources in your subscription.</span></span> <span data-ttu-id="4dbea-105">Используя созданный шаблон, можно изучить синтаксис шаблонов или при необходимости автоматизировать повторное развертывание решения.</span><span class="sxs-lookup"><span data-stu-id="4dbea-105">You can use that generated template to learn about the template syntax or to automate the redeployment of your solution as needed.</span></span>

<span data-ttu-id="4dbea-106">Важно отметить, что экспортировать шаблон можно двумя разными способами.</span><span class="sxs-lookup"><span data-stu-id="4dbea-106">It is important to note that there are two different ways to export a template:</span></span>

* <span data-ttu-id="4dbea-107">Вы можете экспортировать шаблон, который использовался для развертывания.</span><span class="sxs-lookup"><span data-stu-id="4dbea-107">You can export the actual template that you used for a deployment.</span></span> <span data-ttu-id="4dbea-108">Он содержит все параметры и переменные, указанные в исходном шаблоне.</span><span class="sxs-lookup"><span data-stu-id="4dbea-108">The exported template includes all the parameters and variables exactly as they appeared in the original template.</span></span> <span data-ttu-id="4dbea-109">Этот подход полезен в тех случаях, когда требуется извлечь шаблон.</span><span class="sxs-lookup"><span data-stu-id="4dbea-109">This approach is helpful when you need to retrieve a template.</span></span>
* <span data-ttu-id="4dbea-110">Вы можете экспортировать шаблон, который представляет текущее состояние группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4dbea-110">You can export a template that represents the current state of the resource group.</span></span> <span data-ttu-id="4dbea-111">Он не основан на каком-либо шаблоне, который использовался для развертывания.</span><span class="sxs-lookup"><span data-stu-id="4dbea-111">The exported template is not based on any template that you used for deployment.</span></span> <span data-ttu-id="4dbea-112">Напротив, создается шаблон, который является моментальным снимком группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4dbea-112">Instead, it creates a template that is a snapshot of the resource group.</span></span> <span data-ttu-id="4dbea-113">Экспортированный шаблон содержит много жестко заданных значений и, скорее всего, меньше параметров, чем вы обычно определяете.</span><span class="sxs-lookup"><span data-stu-id="4dbea-113">The exported template has many hard-coded values and probably not as many parameters as you would typically define.</span></span> <span data-ttu-id="4dbea-114">Этот метод подходит, если вы изменили группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4dbea-114">This approach is useful when you have modified the resource group.</span></span> <span data-ttu-id="4dbea-115">и теперь на ее основе необходимо создать шаблон.</span><span class="sxs-lookup"><span data-stu-id="4dbea-115">Now, you need to capture the resource group as a template.</span></span>

<span data-ttu-id="4dbea-116">В этой статье показаны оба способа.</span><span class="sxs-lookup"><span data-stu-id="4dbea-116">This topic shows both approaches.</span></span>

## <a name="deploy-a-solution"></a><span data-ttu-id="4dbea-117">Развертывание решения</span><span class="sxs-lookup"><span data-stu-id="4dbea-117">Deploy a solution</span></span>

<span data-ttu-id="4dbea-118">Чтобы продемонстрировать оба подхода для экспорта шаблона, начнем с развертывания решения в подписку.</span><span class="sxs-lookup"><span data-stu-id="4dbea-118">To illustrate both approaches for exporting a template, let's start by deploying a solution to your subscription.</span></span> <span data-ttu-id="4dbea-119">Если у вас уже есть группа ресурсов в подписке, в которую необходимо выполнить экспорт, то не нужно развертывать это решение.</span><span class="sxs-lookup"><span data-stu-id="4dbea-119">If you already have a resource group in your subscription that you want to export, you do not have to deploy this solution.</span></span> <span data-ttu-id="4dbea-120">Оставшаяся часть этой статьи относится к шаблону для этого решения.</span><span class="sxs-lookup"><span data-stu-id="4dbea-120">However, the remainder of this article refers to the template for this solution.</span></span> <span data-ttu-id="4dbea-121">В примере сценария развертывается учетная запись хранения.</span><span class="sxs-lookup"><span data-stu-id="4dbea-121">The example script deploys a storage account.</span></span>

```powershell
New-AzureRmResourceGroup -Name ExampleGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup `
  -DeploymentName NewStorage
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json
```  

## <a name="save-template-from-deployment-history"></a><span data-ttu-id="4dbea-122">Сохранение шаблона из журнала развертываний</span><span class="sxs-lookup"><span data-stu-id="4dbea-122">Save template from deployment history</span></span>

<span data-ttu-id="4dbea-123">Шаблон можно извлечь из журнала развертываний с помощью команды [Save-AzureRmResourceGroupDeploymentTemplate](/powershell/module/azurerm.resources/save-azurermresourcegroupdeploymenttemplate).</span><span class="sxs-lookup"><span data-stu-id="4dbea-123">You can retrieve a template from your deployment history by using the [Save-AzureRmResourceGroupDeploymentTemplate](/powershell/module/azurerm.resources/save-azurermresourcegroupdeploymenttemplate) command.</span></span> <span data-ttu-id="4dbea-124">В следующем примере сохраняется шаблон, который вы ранее развернули:</span><span class="sxs-lookup"><span data-stu-id="4dbea-124">The following example saves the template that you previously deploy:</span></span>

```powershell
Save-AzureRmResourceGroupDeploymentTemplate -ResourceGroupName ExampleGroup -DeploymentName NewStorage
```

<span data-ttu-id="4dbea-125">Эта команда возвращает расположение шаблона.</span><span class="sxs-lookup"><span data-stu-id="4dbea-125">It returns the location of the template.</span></span>

```powershell
Path
----
C:\Users\exampleuser\NewStorage.json
```

<span data-ttu-id="4dbea-126">Откройте файл и обратите внимание, что это точно такой же шаблон, как используемый для развертывания.</span><span class="sxs-lookup"><span data-stu-id="4dbea-126">Open the file, and notice that it is the exact template you used for deployment.</span></span> <span data-ttu-id="4dbea-127">Параметры и переменные соответствуют шаблону из GitHub.</span><span class="sxs-lookup"><span data-stu-id="4dbea-127">The parameters and variables match the template from GitHub.</span></span> <span data-ttu-id="4dbea-128">Этот шаблон можно развернуть повторно.</span><span class="sxs-lookup"><span data-stu-id="4dbea-128">You can redeploy this template.</span></span>

## <a name="export-resource-group-as-template"></a><span data-ttu-id="4dbea-129">Экспорт группы ресурсов в виде шаблона</span><span class="sxs-lookup"><span data-stu-id="4dbea-129">Export resource group as template</span></span>

<span data-ttu-id="4dbea-130">Вместо извлечения шаблона из журнала развертываний можно получить шаблон, который представляет текущее состояние группы ресурсов. Для этого используйте команду [Export-AzureRmResourceGroup](/powershell/module/azurerm.resources/export-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="4dbea-130">Instead of retrieving a template from the deployment history, you can retrieve a template that represents the current state of a resource group by using the [Export-AzureRmResourceGroup](/powershell/module/azurerm.resources/export-azurermresourcegroup) command.</span></span> <span data-ttu-id="4dbea-131">Эта команда используется, когда в группе ресурсов внесено много изменений и ни один из существующих шаблонов не содержит всех изменений.</span><span class="sxs-lookup"><span data-stu-id="4dbea-131">You use this command when you have made many changes to your resource group and no existing template represents all the changes.</span></span>

```powershell
Export-AzureRmResourceGroup -ResourceGroupName ExampleGroup
```

<span data-ttu-id="4dbea-132">Эта команда возвращает расположение шаблона.</span><span class="sxs-lookup"><span data-stu-id="4dbea-132">It returns the location of the template.</span></span>

```powershell
Path
----
C:\Users\exampleuser\ExampleGroup.json
```

<span data-ttu-id="4dbea-133">Откройте файл и обратите внимание, что он отличается от шаблона в GitHub.</span><span class="sxs-lookup"><span data-stu-id="4dbea-133">Open the file, and notice that it is different than the template in GitHub.</span></span> <span data-ttu-id="4dbea-134">У него другие параметры и нет переменных.</span><span class="sxs-lookup"><span data-stu-id="4dbea-134">It has different parameters and no variables.</span></span> <span data-ttu-id="4dbea-135">Номер SKU хранилища и расположение жестко заданы в значениях.</span><span class="sxs-lookup"><span data-stu-id="4dbea-135">The storage SKU and location are hard-coded to values.</span></span> <span data-ttu-id="4dbea-136">В следующем примере показан экспортированный шаблон, но в вашем шаблоне имя параметра будет немного отличаться:</span><span class="sxs-lookup"><span data-stu-id="4dbea-136">The following example shows the exported template, but your template has a slightly different parameter name:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccounts_nf3mvst4nqb36standardsa_name": {
      "defaultValue": null,
      "type": "String"
    }
  },
  "variables": {},
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "sku": {
        "name": "Standard_LRS",
        "tier": "Standard"
      },
      "kind": "Storage",
      "name": "[parameters('storageAccounts_nf3mvst4nqb36standardsa_name')]",
      "apiVersion": "2016-01-01",
      "location": "southcentralus",
      "tags": {},
      "properties": {},
      "dependsOn": []
    }
  ]
}
```

<span data-ttu-id="4dbea-137">Вы можете повторно развернуть этот шаблон, но в нем требуется подобрать уникальное имя для учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="4dbea-137">You can redeploy this template, but it requires guessing a unique name for the storage account.</span></span> <span data-ttu-id="4dbea-138">Имя вашего параметра будет немного отличаться.</span><span class="sxs-lookup"><span data-stu-id="4dbea-138">The name of your parameter is slightly different.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup `
  -TemplateFile C:\Users\exampleuser\ExampleGroup.json `
  -storageAccounts_nf3mvst4nqb36standardsa_name tfnewstorage0501
```

## <a name="customize-exported-template"></a><span data-ttu-id="4dbea-139">Настройка экспортированного шаблона</span><span class="sxs-lookup"><span data-stu-id="4dbea-139">Customize exported template</span></span>

<span data-ttu-id="4dbea-140">Этот шаблон можно изменить, чтобы сделать его более гибким и простым в использовании.</span><span class="sxs-lookup"><span data-stu-id="4dbea-140">You can modify this template to make it easier to use and more flexible.</span></span> <span data-ttu-id="4dbea-141">Чтобы можно было использовать больше расположений, настройте для свойства location такое же значение расположения, как у группы ресурсов:</span><span class="sxs-lookup"><span data-stu-id="4dbea-141">To allow for more locations, change the location property to use the same location as the resource group:</span></span>

```json
"location": "[resourceGroup().location]",
```

<span data-ttu-id="4dbea-142">Чтобы не было необходимости подбирать уникальное имя учетной записи хранения, удалите параметр имени учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="4dbea-142">To avoid having to guess a uniques name for storage account, remove the parameter for the storage account name.</span></span> <span data-ttu-id="4dbea-143">Добавьте параметр для суффикса имени хранилища и номер SKU хранилища:</span><span class="sxs-lookup"><span data-stu-id="4dbea-143">Add a parameter for a storage name suffix, and a storage SKU:</span></span>

```json
"parameters": {
    "storageSuffix": {
      "type": "string",
      "defaultValue": "standardsa"
    },
    "storageAccountType": {
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS"
      ],
      "type": "string",
      "metadata": {
        "description": "Storage Account type"
      }
    }
},
```

<span data-ttu-id="4dbea-144">Добавьте переменную, которая создает имя учетной записи хранения с помощью функции uniqueString:</span><span class="sxs-lookup"><span data-stu-id="4dbea-144">Add a variable that constructs the storage account name with the uniqueString function:</span></span>

```json
"variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
```

<span data-ttu-id="4dbea-145">Задайте переменной имя учетной записи хранения:</span><span class="sxs-lookup"><span data-stu-id="4dbea-145">Set the name of the storage account to the variable:</span></span>

```json
"name": "[variables('storageAccountName')]",
```

<span data-ttu-id="4dbea-146">Задайте параметру номер SKU:</span><span class="sxs-lookup"><span data-stu-id="4dbea-146">Set the SKU to the parameter:</span></span>

```json
"sku": {
    "name": "[parameters('storageAccountType')]",
    "tier": "Standard"
},
```

<span data-ttu-id="4dbea-147">Ваш шаблон теперь выглядит так:</span><span class="sxs-lookup"><span data-stu-id="4dbea-147">Your template now looks like:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageSuffix": {
      "type": "string",
      "defaultValue": "standardsa"
    },
    "storageAccountType": {
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS"
      ],
      "type": "string",
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), parameters('storageSuffix'))]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "sku": {
        "name": "[parameters('storageAccountType')]",
        "tier": "Standard"
      },
      "kind": "Storage",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {},
      "dependsOn": []
    }
  ]
}
```

<span data-ttu-id="4dbea-148">Повторно разверните измененный шаблон.</span><span class="sxs-lookup"><span data-stu-id="4dbea-148">Redeploy the modified template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4dbea-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4dbea-149">Next steps</span></span>
* <span data-ttu-id="4dbea-150">Дополнительные сведения об экспорте шаблона с помощью портала см. в статье [Экспорт шаблона Azure Resource Manager из существующих ресурсов](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="4dbea-150">For information about using the portal to export a template, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="4dbea-151">Сведения об определении параметров в шаблоне см. в разделе [Создание шаблонов](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="4dbea-151">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="4dbea-152">Советы по устранению распространенных ошибок развертывания см. в разделе [Устранение распространенных ошибок развертывания в Azure с помощью Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="4dbea-152">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
