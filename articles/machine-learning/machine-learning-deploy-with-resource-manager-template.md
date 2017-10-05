---
title: "Развертывание рабочей области машинного обучения с помощью Azure Resource Manager | Документация Майкрософт"
description: "Развертывание рабочей области для Машинного обучения Azure с помощью шаблона Azure Resource Manager"
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
ms.openlocfilehash: 9e37780428b0867da63987ec4f7f843a8abeb907
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-machine-learning-workspace-using-azure-resource-manager"></a><span data-ttu-id="e26e1-103">Развертывание рабочей области машинного обучения с помощью Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e26e1-103">Deploy Machine Learning Workspace Using Azure Resource Manager</span></span>
## <a name="introduction"></a><span data-ttu-id="e26e1-104">Введение</span><span class="sxs-lookup"><span data-stu-id="e26e1-104">Introduction</span></span>
<span data-ttu-id="e26e1-105">Шаблон развертывания Azure Resource Manager позволяет сэкономить время, предоставляя масштабируемый способ развертывания взаимосвязанных компонентов с возможностью проверки и механизмом повтора.</span><span class="sxs-lookup"><span data-stu-id="e26e1-105">Using an Azure Resource Manager deployment template saves you time by giving you a scalable way to deploy interconnected components with a validation and retry mechanism.</span></span> <span data-ttu-id="e26e1-106">Чтобы настроить рабочие области Машинного обучения Azure, например, сначала необходимо настроить учетную запись хранения Azure, а затем развернуть рабочую область.</span><span class="sxs-lookup"><span data-stu-id="e26e1-106">To set up Azure Machine Learning Workspaces, for example, you need to first configure an Azure storage account and then deploy your workspace.</span></span> <span data-ttu-id="e26e1-107">Представьте себе выполнение этого задания вручную для сотен рабочих областей.</span><span class="sxs-lookup"><span data-stu-id="e26e1-107">Imagine doing this manually for hundreds of workspaces.</span></span> <span data-ttu-id="e26e1-108">Простой альтернативой является развертывание рабочей области машинного обучения Azure и всех ее зависимых компонентов с помощью шаблона Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e26e1-108">An easier alternative is to use an Azure Resource Manager template to deploy an Azure Machine Learning Workspace and all its dependencies.</span></span> <span data-ttu-id="e26e1-109">В этой статье представлено пошаговое выполнение этого процесса.</span><span class="sxs-lookup"><span data-stu-id="e26e1-109">This article takes you through this process step-by-step.</span></span> <span data-ttu-id="e26e1-110">Подробный обзор Azure Resource Manager см. в статье [Общие сведения об Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e26e1-110">For a great overview of Azure Resource Manager, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="step-by-step-create-a-machine-learning-workspace"></a><span data-ttu-id="e26e1-111">Пошаговое создание рабочей области машинного обучения</span><span class="sxs-lookup"><span data-stu-id="e26e1-111">Step-by-step: create a Machine Learning Workspace</span></span>
<span data-ttu-id="e26e1-112">Сначала мы создадим группу ресурсов Azure, а затем развернем новую учетную запись хранения Azure и рабочую область машинного обучения Azure с помощью шаблона Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e26e1-112">We will create an Azure resource group, then deploy a new Azure storage account and a new Azure Machine Learning Workspace using a Resource Manager template.</span></span> <span data-ttu-id="e26e1-113">После завершения развертывания мы выведем важные сведения о созданных рабочих областях (первичный ключ, идентификатор и URL-адрес рабочей области).</span><span class="sxs-lookup"><span data-stu-id="e26e1-113">Once the deployment is complete, we will print out important information about the workspaces that were created (the primary key, the workspaceID, and the URL to the workspace).</span></span>

### <a name="create-an-azure-resource-manager-template"></a><span data-ttu-id="e26e1-114">Создание шаблона Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e26e1-114">Create an Azure Resource Manager template</span></span>
<span data-ttu-id="e26e1-115">Рабочей области машинного обучения требуется учетная запись хранения Azure для хранения связанного с ней набора данных.</span><span class="sxs-lookup"><span data-stu-id="e26e1-115">A Machine Learning Workspace requires an Azure storage account to store the dataset linked to it.</span></span>
<span data-ttu-id="e26e1-116">В следующем шаблоне для создания имени учетной записи хранения и рабочей области используется имя группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e26e1-116">The following template uses the name of the resource group to generate the storage account name and the workspace name.</span></span>  <span data-ttu-id="e26e1-117">Имя учетной записи хранения также используется в качестве свойства при создании рабочей области.</span><span class="sxs-lookup"><span data-stu-id="e26e1-117">It also uses the storage account name as a property when creating the workspace.</span></span>

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
<span data-ttu-id="e26e1-118">Сохраните этот шаблон как файл mlworkspace.json в папке C:\temp\.</span><span class="sxs-lookup"><span data-stu-id="e26e1-118">Save this template as mlworkspace.json file under c:\temp\.</span></span>

### <a name="deploy-the-resource-group-based-on-the-template"></a><span data-ttu-id="e26e1-119">Развертывание группы ресурсов на основе шаблона</span><span class="sxs-lookup"><span data-stu-id="e26e1-119">Deploy the resource group, based on the template</span></span>
* <span data-ttu-id="e26e1-120">Откройте PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e26e1-120">Open PowerShell</span></span>
* <span data-ttu-id="e26e1-121">Установите модули для Azure Resource Manager и управления службами Azure.</span><span class="sxs-lookup"><span data-stu-id="e26e1-121">Install modules for Azure Resource Manager and Azure Service Management</span></span>  

```
# Install the Azure Resource Manager modules from the PowerShell Gallery (press “A”)
Install-Module AzureRM -Scope CurrentUser

# Install the Azure Service Management modules from the PowerShell Gallery (press “A”)
Install-Module Azure -Scope CurrentUser
```

   <span data-ttu-id="e26e1-122">При этом скачиваются и устанавливаются модули, необходимые для выполнения оставшихся действий.</span><span class="sxs-lookup"><span data-stu-id="e26e1-122">These steps download and install the modules necessary to complete the remaining steps.</span></span> <span data-ttu-id="e26e1-123">Их достаточно выполнить один раз в среде выполнения команд PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e26e1-123">This only needs to be done once in the environment where you are executing the PowerShell commands.</span></span>   

* <span data-ttu-id="e26e1-124">Проверка подлинности в Azure</span><span class="sxs-lookup"><span data-stu-id="e26e1-124">Authenticate to Azure</span></span>  

```
# Authenticate (enter your credentials in the pop-up window)
Add-AzureRmAccount
```
<span data-ttu-id="e26e1-125">Этот шаг необходимо выполнять для каждого сеанса.</span><span class="sxs-lookup"><span data-stu-id="e26e1-125">This step needs to be repeated for each session.</span></span> <span data-ttu-id="e26e1-126">После выполнения проверки подлинности должны отображаться сведения о подписке.</span><span class="sxs-lookup"><span data-stu-id="e26e1-126">Once authenticated, your subscription information should be displayed.</span></span>

![Учетная запись Azure][1]

<span data-ttu-id="e26e1-128">Получив доступ к Azure, мы можем создать группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e26e1-128">Now that we have access to Azure, we can create the resource group.</span></span>

* <span data-ttu-id="e26e1-129">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="e26e1-129">Create a resource group</span></span>

```
$rg = New-AzureRmResourceGroup -Name "uniquenamerequired523" -Location "South Central US"
$rg
```

<span data-ttu-id="e26e1-130">Убедитесь, что группа ресурсов должным образом подготовлена к работе.</span><span class="sxs-lookup"><span data-stu-id="e26e1-130">Verify that the resource group is correctly provisioned.</span></span> <span data-ttu-id="e26e1-131">**ProvisioningState** должно отображаться состояние Succeeded.</span><span class="sxs-lookup"><span data-stu-id="e26e1-131">**ProvisioningState** should be “Succeeded.”</span></span>
<span data-ttu-id="e26e1-132">Шаблон использует имя группы ресурсов для создания имени учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="e26e1-132">The resource group name is used by the template to generate the storage account name.</span></span> <span data-ttu-id="e26e1-133">Имя учетной записи хранения должно содержать от 3 до 24 знаков и состоять только из цифр и букв нижнего регистра.</span><span class="sxs-lookup"><span data-stu-id="e26e1-133">The storage account name must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span>

![Группа ресурсов][2]

* <span data-ttu-id="e26e1-135">Разверните новую рабочую область машинного обучения с помощью развертывания группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e26e1-135">Using the resource group deployment, deploy a new Machine Learning Workspace.</span></span>

```
# Create a Resource Group, TemplateFile is the location of the JSON template.
$rgd = New-AzureRmResourceGroupDeployment -Name "demo" -TemplateFile "C:\temp\mlworkspace.json" -ResourceGroupName $rg.ResourceGroupName
```

<span data-ttu-id="e26e1-136">После завершения развертывания очень просто получить доступ к свойствам развернутой рабочей области.</span><span class="sxs-lookup"><span data-stu-id="e26e1-136">Once the deployment is completed, it is straightforward to access properties of the workspace you deployed.</span></span> <span data-ttu-id="e26e1-137">Например, можно получить доступ к сведениям о маркере первичного ключа.</span><span class="sxs-lookup"><span data-stu-id="e26e1-137">For example, you can access the Primary Key Token.</span></span>

```
# Access Azure ML Workspace Token after its deployment.
$rgd.Outputs.mlWorkspaceToken.Value
```

<span data-ttu-id="e26e1-138">Другой способ получения маркеров существующей рабочей области — использовать команду Invoke-AzureRmResourceAction.</span><span class="sxs-lookup"><span data-stu-id="e26e1-138">Another way to retrieve tokens of existing workspace is to use the Invoke-AzureRmResourceAction command.</span></span> <span data-ttu-id="e26e1-139">Например, можно отобразить список основных и дополнительных маркеров всех рабочих областей.</span><span class="sxs-lookup"><span data-stu-id="e26e1-139">For example, you can list the primary and secondary tokens of all workspaces.</span></span>

```  
# List the primary and secondary tokens of all workspaces
Get-AzureRmResource |? { $_.ResourceType -Like "*MachineLearning/workspaces*"} |% { Invoke-AzureRmResourceAction -ResourceId $_.ResourceId -Action listworkspacekeys -Force}  
```
<span data-ttu-id="e26e1-140">После подготовки рабочей области к работе можно автоматизировать многие задачи Студии машинного обучения Azure с помощью [модуля PowerShell для Машинного обучения Azure](http://aka.ms/amlps).</span><span class="sxs-lookup"><span data-stu-id="e26e1-140">After the workspace is provisioned, you can also automate many Azure Machine Learning Studio tasks using the [PowerShell Module for Azure Machine Learning](http://aka.ms/amlps).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e26e1-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e26e1-141">Next Steps</span></span>
* <span data-ttu-id="e26e1-142">Узнайте больше о [создании шаблонов Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="e26e1-142">Learn more about [authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 
* <span data-ttu-id="e26e1-143">Просмотрите [репозиторий шаблонов быстрого запуска Azure](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="e26e1-143">Have a look at the [Azure Quickstart Templates Repository](https://github.com/Azure/azure-quickstart-templates).</span></span> 
* <span data-ttu-id="e26e1-144">Просмотрите видео об [Azure Resource Manager](https://channel9.msdn.com/Events/Ignite/2015/C9-39).</span><span class="sxs-lookup"><span data-stu-id="e26e1-144">Watch this video about [Azure Resource Manager](https://channel9.msdn.com/Events/Ignite/2015/C9-39).</span></span> 

<!--Image references-->
[1]: ../media/machine-learning-deploy-with-resource-manager-template/azuresubscription.png
[2]: ../media/machine-learning-deploy-with-resource-manager-template/resourcegroupprovisioning.png


<!--Link references-->
