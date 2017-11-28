---
title: "aaaDeploy рабочей области машинного обучения с помощью диспетчера ресурсов Azure | Документы Microsoft"
description: "Как toodeploy в рабочую область для машинного обучения Azure с помощью шаблона диспетчера ресурсов Azure"
services: machine-learning
documentationcenter: 
author: ahgyger
manager: haining
editor: garye
ms.assetid: 4955ac4d-ff99-4908-aa27-69b6bfcc8e85
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/15/2017
ms.author: ahgyger
ms.openlocfilehash: 308959825bcbd670f6ce9b6dc381be767f172357
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-machine-learning-workspace-using-azure-resource-manager"></a><span data-ttu-id="fc2b6-103">Развертывание рабочей области машинного обучения с помощью Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fc2b6-103">Deploy Machine Learning Workspace Using Azure Resource Manager</span></span>
## <a name="introduction"></a><span data-ttu-id="fc2b6-104">Введение</span><span class="sxs-lookup"><span data-stu-id="fc2b6-104">Introduction</span></span>
<span data-ttu-id="fc2b6-105">С помощью диспетчера ресурсов Azure, в шаблон развертывания вы можете сэкономить время, предоставляя toodeploy масштабируемый способ между собой компонентов механизм, с помощью проверки и повторите попытку.</span><span class="sxs-lookup"><span data-stu-id="fc2b6-105">Using an Azure Resource Manager deployment template saves you time by giving you a scalable way toodeploy interconnected components with a validation and retry mechanism.</span></span> <span data-ttu-id="fc2b6-106">tooset копирование рабочие области машинного обучения Azure, например, требуется toofirst настроить учетную запись хранения Azure, а затем развернуть рабочую область.</span><span class="sxs-lookup"><span data-stu-id="fc2b6-106">tooset up Azure Machine Learning Workspaces, for example, you need toofirst configure an Azure storage account and then deploy your workspace.</span></span> <span data-ttu-id="fc2b6-107">Представьте себе выполнение этого задания вручную для сотен рабочих областей.</span><span class="sxs-lookup"><span data-stu-id="fc2b6-107">Imagine doing this manually for hundreds of workspaces.</span></span> <span data-ttu-id="fc2b6-108">Альтернативой проще является toouse toodeploy шаблона диспетчера ресурсов Azure рабочую область Azure машинного обучения и все его зависимости.</span><span class="sxs-lookup"><span data-stu-id="fc2b6-108">An easier alternative is toouse an Azure Resource Manager template toodeploy an Azure Machine Learning Workspace and all its dependencies.</span></span> <span data-ttu-id="fc2b6-109">В этой статье представлено пошаговое выполнение этого процесса.</span><span class="sxs-lookup"><span data-stu-id="fc2b6-109">This article takes you through this process step-by-step.</span></span> <span data-ttu-id="fc2b6-110">Подробный обзор Azure Resource Manager см. в статье [Общие сведения об Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fc2b6-110">For a great overview of Azure Resource Manager, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="step-by-step-create-a-machine-learning-workspace"></a><span data-ttu-id="fc2b6-111">Пошаговое создание рабочей области машинного обучения</span><span class="sxs-lookup"><span data-stu-id="fc2b6-111">Step-by-step: create a Machine Learning Workspace</span></span>
<span data-ttu-id="fc2b6-112">Сначала мы создадим группу ресурсов Azure, а затем развернем новую учетную запись хранения Azure и рабочую область машинного обучения Azure с помощью шаблона Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fc2b6-112">We will create an Azure resource group, then deploy a new Azure storage account and a new Azure Machine Learning Workspace using a Resource Manager template.</span></span> <span data-ttu-id="fc2b6-113">После завершения развертывания hello, мы напечатает важные сведения о hello рабочих областей, которые были созданы (первичный ключ hello hello ИД рабочей области и рабочей toohello hello URL-адрес).</span><span class="sxs-lookup"><span data-stu-id="fc2b6-113">Once hello deployment is complete, we will print out important information about hello workspaces that were created (hello primary key, hello workspaceID, and hello URL toohello workspace).</span></span>

### <a name="create-an-azure-resource-manager-template"></a><span data-ttu-id="fc2b6-114">Создание шаблона Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fc2b6-114">Create an Azure Resource Manager template</span></span>
<span data-ttu-id="fc2b6-115">Рабочую область машинного обучения требует хранилища Azure tooit учетной записи toostore hello связанного набора данных.</span><span class="sxs-lookup"><span data-stu-id="fc2b6-115">A Machine Learning Workspace requires an Azure storage account toostore hello dataset linked tooit.</span></span>
<span data-ttu-id="fc2b6-116">Hello следующий шаблон использует имя hello hello toogenerate группы ресурсов hello имя учетной записи хранилища и имя рабочей области hello.</span><span class="sxs-lookup"><span data-stu-id="fc2b6-116">hello following template uses hello name of hello resource group toogenerate hello storage account name and hello workspace name.</span></span>  <span data-ttu-id="fc2b6-117">Она также использует имя учетной записи хранения hello как свойство при создании рабочей hello.</span><span class="sxs-lookup"><span data-stu-id="fc2b6-117">It also uses hello storage account name as a property when creating hello workspace.</span></span>

```
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "variables": {
        "namePrefix": "[resourceGroup().name]",
        "location": "[resourceGroup().location]",
        "mlVersion": "2016-04-01",
        "stgVersion": "2015-06-15",
        "storageAccountName": "[concat(variables('namePrefix'),'stg')]",
        "mlWorkspaceName": "[concat(variables('namePrefix'),'mlwk')]",
        "mlResourceId": "[resourceId('Microsoft.MachineLearning/workspaces', variables('mlWorkspaceName'))]",
        "stgResourceId": "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]",
        "storageAccountType": "Standard_LRS"
    },
    "resources": [
        {
            "apiVersion": "[variables('stgVersion')]",
            "name": "[variables('storageAccountName')]",
            "type": "Microsoft.Storage/storageAccounts",
            "location": "[variables('location')]",
            "properties": {
                "accountType": "[variables('storageAccountType')]"
            }
        },
        {
            "apiVersion": "[variables('mlVersion')]",
            "type": "Microsoft.MachineLearning/workspaces",
            "name": "[variables('mlWorkspaceName')]",
            "location": "[variables('location')]",
            "dependsOn": ["[variables('stgResourceId')]"],
            "properties": {
                "UserStorageAccountId": "[variables('stgResourceId')]"
            }
        }
    ],
    "outputs": {
        "mlWorkspaceObject": {"type": "object", "value": "[reference(variables('mlResourceId'), variables('mlVersion'))]"},
        "mlWorkspaceToken": {"type": "string", "value": "[listWorkspaceKeys(variables('mlResourceId'), variables('mlVersion')).primaryToken]"},
        "mlWorkspaceWorkspaceID": {"type": "string", "value": "[reference(variables('mlResourceId'), variables('mlVersion')).WorkspaceId]"},
        "mlWorkspaceWorkspaceLink": {"type": "string", "value": "[concat('https://studio.azureml.net/Home/ViewWorkspace/', reference(variables('mlResourceId'), variables('mlVersion')).WorkspaceId)]"}
    }
}

```
<span data-ttu-id="fc2b6-118">Сохраните этот шаблон как файл mlworkspace.json в папке C:\temp\.</span><span class="sxs-lookup"><span data-stu-id="fc2b6-118">Save this template as mlworkspace.json file under c:\temp\.</span></span>

### <a name="deploy-hello-resource-group-based-on-hello-template"></a><span data-ttu-id="fc2b6-119">Развертывание группы ресурсов hello, основанных на шаблоне hello</span><span class="sxs-lookup"><span data-stu-id="fc2b6-119">Deploy hello resource group, based on hello template</span></span>
* <span data-ttu-id="fc2b6-120">Откройте PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fc2b6-120">Open PowerShell</span></span>
* <span data-ttu-id="fc2b6-121">Установите модули для Azure Resource Manager и управления службами Azure.</span><span class="sxs-lookup"><span data-stu-id="fc2b6-121">Install modules for Azure Resource Manager and Azure Service Management</span></span>  

```
# Install hello Azure Resource Manager modules from hello PowerShell Gallery (press “A”)
Install-Module AzureRM -Scope CurrentUser

# Install hello Azure Service Management modules from hello PowerShell Gallery (press “A”)
Install-Module Azure -Scope CurrentUser
```

   <span data-ttu-id="fc2b6-122">Эти действия, загрузите и установите hello модули необходимые toocomplete hello оставшиеся шаги.</span><span class="sxs-lookup"><span data-stu-id="fc2b6-122">These steps download and install hello modules necessary toocomplete hello remaining steps.</span></span> <span data-ttu-id="fc2b6-123">Это достаточно выполнить один раз в среде hello, где выполняются команды PowerShell hello toobe.</span><span class="sxs-lookup"><span data-stu-id="fc2b6-123">This only needs toobe done once in hello environment where you are executing hello PowerShell commands.</span></span>   

* <span data-ttu-id="fc2b6-124">Проверка подлинности tooAzure</span><span class="sxs-lookup"><span data-stu-id="fc2b6-124">Authenticate tooAzure</span></span>  

```
# Authenticate (enter your credentials in hello pop-up window)
Add-AzureRmAccount
```
<span data-ttu-id="fc2b6-125">Этот шаг должен toobe повторяется для каждого сеанса.</span><span class="sxs-lookup"><span data-stu-id="fc2b6-125">This step needs toobe repeated for each session.</span></span> <span data-ttu-id="fc2b6-126">После выполнения проверки подлинности должны отображаться сведения о подписке.</span><span class="sxs-lookup"><span data-stu-id="fc2b6-126">Once authenticated, your subscription information should be displayed.</span></span>

![Учетная запись Azure][1]

<span data-ttu-id="fc2b6-128">Теперь, когда у нас есть tooAzure доступ, можно создать группу ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="fc2b6-128">Now that we have access tooAzure, we can create hello resource group.</span></span>

* <span data-ttu-id="fc2b6-129">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="fc2b6-129">Create a resource group</span></span>

```
$rg = New-AzureRmResourceGroup -Name "uniquenamerequired523" -Location "South Central US"
$rg
```

<span data-ttu-id="fc2b6-130">Убедитесь, что задокументирована надлежащим образом, что группа ресурсов "hello".</span><span class="sxs-lookup"><span data-stu-id="fc2b6-130">Verify that hello resource group is correctly provisioned.</span></span> <span data-ttu-id="fc2b6-131">**ProvisioningState** должно отображаться состояние Succeeded.</span><span class="sxs-lookup"><span data-stu-id="fc2b6-131">**ProvisioningState** should be “Succeeded.”</span></span>
<span data-ttu-id="fc2b6-132">Имя учетной записи хранилища hello toogenerate hello шаблона используется имя группы ресурсов Hello.</span><span class="sxs-lookup"><span data-stu-id="fc2b6-132">hello resource group name is used by hello template toogenerate hello storage account name.</span></span> <span data-ttu-id="fc2b6-133">Имя учетной записи хранения Hello должно быть от 3 до 24 символов и содержать только строчные буквы и цифры.</span><span class="sxs-lookup"><span data-stu-id="fc2b6-133">hello storage account name must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span>

![Группа ресурсов][2]

* <span data-ttu-id="fc2b6-135">Развертывание группы ресурсов hello, внедрить новые рабочую область машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="fc2b6-135">Using hello resource group deployment, deploy a new Machine Learning Workspace.</span></span>

```
# Create a Resource Group, TemplateFile is hello location of hello JSON template.
$rgd = New-AzureRmResourceGroupDeployment -Name "demo" -TemplateFile "C:\temp\mlworkspace.json" -ResourceGroupName $rg.ResourceGroupName
```

<span data-ttu-id="fc2b6-136">После завершения развертывания hello, это просто tooaccess свойства hello рабочую область, которую вы развернули.</span><span class="sxs-lookup"><span data-stu-id="fc2b6-136">Once hello deployment is completed, it is straightforward tooaccess properties of hello workspace you deployed.</span></span> <span data-ttu-id="fc2b6-137">Например можно получить доступ к hello токена первичного ключа.</span><span class="sxs-lookup"><span data-stu-id="fc2b6-137">For example, you can access hello Primary Key Token.</span></span>

```
# Access Azure ML Workspace Token after its deployment.
$rgd.Outputs.mlWorkspaceToken.Value
```

<span data-ttu-id="fc2b6-138">Другой способ tooretrieve маркеры существующую рабочую область — hello toouse команда Invoke-AzureRmResourceAction.</span><span class="sxs-lookup"><span data-stu-id="fc2b6-138">Another way tooretrieve tokens of existing workspace is toouse hello Invoke-AzureRmResourceAction command.</span></span> <span data-ttu-id="fc2b6-139">Например можно перечислить hello первичного и вторичного маркеры всех рабочих областей.</span><span class="sxs-lookup"><span data-stu-id="fc2b6-139">For example, you can list hello primary and secondary tokens of all workspaces.</span></span>

```  
# List hello primary and secondary tokens of all workspaces
Get-AzureRmResource |? { $_.ResourceType -Like "*MachineLearning/workspaces*"} |% { Invoke-AzureRmResourceAction -ResourceId $_.ResourceId -Action listworkspacekeys -Force}  
```
<span data-ttu-id="fc2b6-140">После подготовки рабочей hello также можно автоматизировать многие задачи студии машинного обучения Azure с помощью hello [модуль PowerShell для машинного обучения Azure](http://aka.ms/amlps).</span><span class="sxs-lookup"><span data-stu-id="fc2b6-140">After hello workspace is provisioned, you can also automate many Azure Machine Learning Studio tasks using hello [PowerShell Module for Azure Machine Learning](http://aka.ms/amlps).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fc2b6-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fc2b6-141">Next Steps</span></span>
* <span data-ttu-id="fc2b6-142">Узнайте больше о [создании шаблонов Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="fc2b6-142">Learn more about [authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 
* <span data-ttu-id="fc2b6-143">Рассмотрим hello [репозиторий шаблоны быстрый запуск Azure](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="fc2b6-143">Have a look at hello [Azure Quickstart Templates Repository](https://github.com/Azure/azure-quickstart-templates).</span></span> 
* <span data-ttu-id="fc2b6-144">Просмотрите видео об [Azure Resource Manager](https://channel9.msdn.com/Events/Ignite/2015/C9-39).</span><span class="sxs-lookup"><span data-stu-id="fc2b6-144">Watch this video about [Azure Resource Manager](https://channel9.msdn.com/Events/Ignite/2015/C9-39).</span></span> 

<!--Image references-->
[1]: ../media/machine-learning-deploy-with-resource-manager-template/azuresubscription.png
[2]: ../media/machine-learning-deploy-with-resource-manager-template/resourcegroupprovisioning.png


<!--Link references-->
