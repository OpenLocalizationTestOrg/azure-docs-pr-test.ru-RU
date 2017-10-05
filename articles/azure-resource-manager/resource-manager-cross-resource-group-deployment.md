---
title: "Развертывание ресурсов Azure в несколько групп ресурсов | Документация Майкрософт"
description: "Сведения о развертывании ресурсов в несколько групп ресурсов Azure."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/15/2017
ms.author: tomfitz
ms.openlocfilehash: d8b041213b269775175a810e585103d3c538557f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-azure-resources-to-more-than-one-resource-group"></a><span data-ttu-id="fbf3f-103">Развертывание ресурсов Azure в несколько групп ресурсов</span><span class="sxs-lookup"><span data-stu-id="fbf3f-103">Deploy Azure resources to more than one resource group</span></span>

<span data-ttu-id="fbf3f-104">Обычно развертывание всех ресурсов в шаблоне выполняется в отдельную группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="fbf3f-104">Typically, you deploy all the resources in your template to a single resource group.</span></span> <span data-ttu-id="fbf3f-105">Но иногда может потребоваться развернуть ресурсы вместе, но разместить их в разные группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="fbf3f-105">However, there are scenarios where you want to deploy a set of resources together but place them in different resource groups.</span></span> <span data-ttu-id="fbf3f-106">Например, вы захотите развернуть резервную копию виртуальной машины для Azure Site Recovery в отдельную группу ресурсов или расположение.</span><span class="sxs-lookup"><span data-stu-id="fbf3f-106">For example, you may want to deploy the backup virtual machine for Azure Site Recovery to a separate resource group and location.</span></span> <span data-ttu-id="fbf3f-107">Resource Manager позволяет использовать вложенные шаблоны, с помощью которых ресурсы можно развертывать в разные группы ресурсов, а не только в группу ресурсов родительского шаблона.</span><span class="sxs-lookup"><span data-stu-id="fbf3f-107">Resource Manager enables you to use nested templates to target different resource groups than the resource group used for the parent template.</span></span>

<span data-ttu-id="fbf3f-108">Группа ресурсов — это контейнер жизненного цикла приложения, в котором содержится коллекция его ресурсов.</span><span class="sxs-lookup"><span data-stu-id="fbf3f-108">The resource group is the lifecycle container for the application and its collection of resources.</span></span> <span data-ttu-id="fbf3f-109">Создание группы ресурсов выполняется вне шаблона. Затем вы указываете группу ресурсов, которая должна использоваться в процессе развертывания.</span><span class="sxs-lookup"><span data-stu-id="fbf3f-109">You create the resource group outside of the template, and specify the resource group to target during deployment.</span></span> <span data-ttu-id="fbf3f-110">Дополнительные сведения о группах ресурсов см. в статье [Общие сведения об Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fbf3f-110">For an introduction to resource groups, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

## <a name="example-template"></a><span data-ttu-id="fbf3f-111">Пример шаблона</span><span class="sxs-lookup"><span data-stu-id="fbf3f-111">Example template</span></span>

<span data-ttu-id="fbf3f-112">Чтобы подключиться к другому ресурсу, при развертывании используйте вложенный или связанный шаблон.</span><span class="sxs-lookup"><span data-stu-id="fbf3f-112">To target a different resource, you must use a nested or linked template during deployment.</span></span> <span data-ttu-id="fbf3f-113">Тип ресурса `Microsoft.Resources/deployments` предоставляет параметр `resourceGroup`, который позволяет указать другую группу ресурсов для вложенного развертывания.</span><span class="sxs-lookup"><span data-stu-id="fbf3f-113">The `Microsoft.Resources/deployments` resource type provides a `resourceGroup` parameter that enables you to specify a different resource group for the nested deployment.</span></span> <span data-ttu-id="fbf3f-114">Все группы ресурсов необходимо создать до выполнения развертывания.</span><span class="sxs-lookup"><span data-stu-id="fbf3f-114">All the resource groups must exist before running the deployment.</span></span> <span data-ttu-id="fbf3f-115">Код в приведенном ниже примере развертывает две учетные записи хранения: одну в группе ресурсов, указанной во время развертывания, и вторую в группе ресурсов `crossResourceGroupDeployment`:</span><span class="sxs-lookup"><span data-stu-id="fbf3f-115">The following example deploys two storage accounts - one in the resource group specified during deployment, and one in a resource group named `crossResourceGroupDeployment`:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "StorageAccountName1": {
            "type": "string"
        },
        "StorageAccountName2": {
            "type": "string"
        }
    },
    "variables": {},
    "resources": [
        {
            "apiVersion": "2017-05-10",
            "name": "nestedTemplate",
            "type": "Microsoft.Resources/deployments",
            "resourceGroup": "crossResourceGroupDeployment",
            "properties": {
                "mode": "Incremental",
                "template": {
                    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
                    "contentVersion": "1.0.0.0",
                    "parameters": {},
                    "variables": {},
                    "resources": [
                        {
                            "type": "Microsoft.Storage/storageAccounts",
                            "name": "[parameters('StorageAccountName2')]",
                            "apiVersion": "2015-06-15",
                            "location": "West US",
                            "properties": {
                                "accountType": "Standard_LRS"
                            }
                        }
                    ]
                },
                "parameters": {}
            }
        },
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[parameters('StorageAccountName1')]",
            "apiVersion": "2015-06-15",
            "location": "West US",
            "properties": {
                "accountType": "Standard_LRS"
            }
        }
    ]
}
```

<span data-ttu-id="fbf3f-116">Если в качестве значения параметра `resourceGroup` задать имя несуществующей группы ресурсов, развертывание завершится сбоем.</span><span class="sxs-lookup"><span data-stu-id="fbf3f-116">If you set `resourceGroup` to the name of a resource group that does not exist, the deployment fails.</span></span> <span data-ttu-id="fbf3f-117">Но если не указать значение параметра `resourceGroup`, Resource Manager будет использовать родительскую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="fbf3f-117">If you do not provide a value for `resourceGroup`, Resource Manager uses the parent resource group.</span></span>  

## <a name="deploy-the-template"></a><span data-ttu-id="fbf3f-118">Развертывание шаблона</span><span class="sxs-lookup"><span data-stu-id="fbf3f-118">Deploy the template</span></span>

<span data-ttu-id="fbf3f-119">Пример шаблона можно развернуть с помощью портала, Azure PowerShell или Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="fbf3f-119">To deploy the example template, you can use the portal, Azure PowerShell, or Azure CLI.</span></span> <span data-ttu-id="fbf3f-120">Используйте выпуски этих средств начиная с мая 2017 года.</span><span class="sxs-lookup"><span data-stu-id="fbf3f-120">For Azure PowerShell or Azure CLI, you must use a release from May 2017 or later.</span></span> <span data-ttu-id="fbf3f-121">Для работы с этими примерами шаблон необходимо сохранить локально как файл **crossrgdeployment.json**.</span><span class="sxs-lookup"><span data-stu-id="fbf3f-121">The examples assume you have saved the template locally as a file named **crossrgdeployment.json**.</span></span>

<span data-ttu-id="fbf3f-122">При использовании PowerShell выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="fbf3f-122">For PowerShell:</span></span>

```powershell
Login-AzureRmAccount

New-AzureRmResourceGroup -Name mainResourceGroup -Location "South Central US"
New-AzureRmResourceGroup -Name crossResourceGroupDeployment -Location "Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName mainResourceGroup `
  -TemplateFile c:\MyTemplates\crossrgdeployment.json
```

<span data-ttu-id="fbf3f-123">При использовании Azure CLI выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="fbf3f-123">For Azure CLI:</span></span>

```azurecli
az login

az group create --name mainResourceGroup --location "South Central US"
az group create --name crossResourceGroupDeployment --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group mainResourceGroup \
    --template-file crossrgdeployment.json
```

<span data-ttu-id="fbf3f-124">После завершения развертывания вы увидите две группы ресурсов,</span><span class="sxs-lookup"><span data-stu-id="fbf3f-124">After deployment completes, you see two resource groups.</span></span> <span data-ttu-id="fbf3f-125">в каждой из которых содержится учетная запись хранения.</span><span class="sxs-lookup"><span data-stu-id="fbf3f-125">Each resource group contains a storage account.</span></span>

## <a name="use-resourcegroup-function"></a><span data-ttu-id="fbf3f-126">Использование функции resourceGroup()</span><span class="sxs-lookup"><span data-stu-id="fbf3f-126">Use resourceGroup() function</span></span>

<span data-ttu-id="fbf3f-127">Для развертывания в нескольких группах ресурсов результат выполнения [функции resouceGroup()](resource-group-template-functions-resource.md#resourcegroup) зависит от способа указания вложенного шаблона.</span><span class="sxs-lookup"><span data-stu-id="fbf3f-127">For cross resource group deployments, the [resouceGroup() function](resource-group-template-functions-resource.md#resourcegroup) resolves differently based on how you specify the nested template.</span></span> 

<span data-ttu-id="fbf3f-128">При внедрении одного шаблона в другой функция resouceGroup() во вложенном шаблоне разрешается в родительской группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="fbf3f-128">If you embed one template within another template, resouceGroup() in the nested template resolves to the parent resource group.</span></span> <span data-ttu-id="fbf3f-129">Внедренный шаблон использует следующий формат:</span><span class="sxs-lookup"><span data-stu-id="fbf3f-129">An embedded template uses the following format:</span></span>

```json
"apiVersion": "2017-05-10",
"name": "embeddedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "template": {
        ...
        resourceGroup() refers to parent resource group
    }
}
```

<span data-ttu-id="fbf3f-130">При связывании отдельного шаблона функция resouceGroup() связывает разрешения шаблона с вложенной группой ресурсов.</span><span class="sxs-lookup"><span data-stu-id="fbf3f-130">If you link to a separate template, resouceGroup() in the linked template resolves to the nested resource group.</span></span> <span data-ttu-id="fbf3f-131">Связанный шаблон использует следующий формат:</span><span class="sxs-lookup"><span data-stu-id="fbf3f-131">A linked template uses the following format:</span></span>

```json
"apiVersion": "2017-05-10",
"name": "linkedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "templateLink": {
        ...
        resourceGroup() in linked template refers to linked resource group
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="fbf3f-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fbf3f-132">Next steps</span></span>

* <span data-ttu-id="fbf3f-133">Сведения об определении параметров в шаблоне см. в статье [Описание структуры и синтаксиса шаблонов Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="fbf3f-133">To understand how to define parameters in your template, see [Understand the structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="fbf3f-134">Советы по устранению распространенных ошибок развертывания см. в разделе [Устранение распространенных ошибок развертывания в Azure с помощью Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="fbf3f-134">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="fbf3f-135">Сведения о развертывании шаблона, которому нужен токен SAS, см. в статье [Развертывание частного шаблона с помощью маркера SAS](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="fbf3f-135">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
