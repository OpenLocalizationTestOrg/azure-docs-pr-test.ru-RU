---
title: "группы ресурсов toomultiple aaaDeploy ресурсы Azure | Документы Microsoft"
description: "Показывает, как группировать tootarget больше, чем один ресурс Azure во время развертывания."
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
ms.openlocfilehash: 93a39a26e0ca18dfcb5c6e8de95c38a64186d6de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-azure-resources-toomore-than-one-resource-group"></a><span data-ttu-id="67478-103">Развертывание toomore ресурсы Azure, чем одной группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="67478-103">Deploy Azure resources toomore than one resource group</span></span>

<span data-ttu-id="67478-104">Как правило все ресурсы hello развернуть в ваш шаблон tooa единой группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="67478-104">Typically, you deploy all hello resources in your template tooa single resource group.</span></span> <span data-ttu-id="67478-105">Однако существуют сценарии, где требуется набор ресурсов toodeploy друг с другом, но поместить их в разные группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="67478-105">However, there are scenarios where you want toodeploy a set of resources together but place them in different resource groups.</span></span> <span data-ttu-id="67478-106">Например может потребоваться toodeploy hello резервного копирования виртуальной машины для Azure Site Recovery tooa отдельной группе ресурсов и расположение.</span><span class="sxs-lookup"><span data-stu-id="67478-106">For example, you may want toodeploy hello backup virtual machine for Azure Site Recovery tooa separate resource group and location.</span></span> <span data-ttu-id="67478-107">Диспетчер ресурсов позволяет toouse вложенные шаблоны tootarget разные группы ресурсов чем hello группы ресурсов, используемой для hello родительского шаблона.</span><span class="sxs-lookup"><span data-stu-id="67478-107">Resource Manager enables you toouse nested templates tootarget different resource groups than hello resource group used for hello parent template.</span></span>

<span data-ttu-id="67478-108">Группа ресурсов Hello находится hello жизненный цикл контейнера для приложения hello и его ресурсы.</span><span class="sxs-lookup"><span data-stu-id="67478-108">hello resource group is hello lifecycle container for hello application and its collection of resources.</span></span> <span data-ttu-id="67478-109">Создать группу ресурсов hello за пределами шаблона hello и укажите tootarget группы ресурсов hello во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="67478-109">You create hello resource group outside of hello template, and specify hello resource group tootarget during deployment.</span></span> <span data-ttu-id="67478-110">Введение tooresource группы, в разделе [Обзор диспетчера ресурсов Azure](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="67478-110">For an introduction tooresource groups, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

## <a name="example-template"></a><span data-ttu-id="67478-111">Пример шаблона</span><span class="sxs-lookup"><span data-stu-id="67478-111">Example template</span></span>

<span data-ttu-id="67478-112">tootarget другой ресурс, необходимо использовать шаблон вложенной или связанной во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="67478-112">tootarget a different resource, you must use a nested or linked template during deployment.</span></span> <span data-ttu-id="67478-113">Hello `Microsoft.Resources/deployments` обеспечивает `resourceGroup` параметр, который позволяет toospecify другой группе ресурсов для hello вложенные развертывания.</span><span class="sxs-lookup"><span data-stu-id="67478-113">hello `Microsoft.Resources/deployments` resource type provides a `resourceGroup` parameter that enables you toospecify a different resource group for hello nested deployment.</span></span> <span data-ttu-id="67478-114">Все группы ресурсов hello должен существовать до запуска развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="67478-114">All hello resource groups must exist before running hello deployment.</span></span> <span data-ttu-id="67478-115">Hello примере развертывает две учетные записи хранилища — один в группе ресурсов hello, указанное во время развертывания и по одному в группу ресурсов с именем `crossResourceGroupDeployment`:</span><span class="sxs-lookup"><span data-stu-id="67478-115">hello following example deploys two storage accounts - one in hello resource group specified during deployment, and one in a resource group named `crossResourceGroupDeployment`:</span></span>

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

<span data-ttu-id="67478-116">Если задать `resourceGroup` toohello имя группы ресурсов, который не существует, развертывание hello завершается с ошибкой.</span><span class="sxs-lookup"><span data-stu-id="67478-116">If you set `resourceGroup` toohello name of a resource group that does not exist, hello deployment fails.</span></span> <span data-ttu-id="67478-117">Если не указано значение для `resourceGroup`, диспетчер ресурсов использует hello родительской группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="67478-117">If you do not provide a value for `resourceGroup`, Resource Manager uses hello parent resource group.</span></span>  

## <a name="deploy-hello-template"></a><span data-ttu-id="67478-118">Развертывание шаблона hello</span><span class="sxs-lookup"><span data-stu-id="67478-118">Deploy hello template</span></span>

<span data-ttu-id="67478-119">Пример шаблона toodeploy hello, можно использовать портал hello, Azure PowerShell или Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="67478-119">toodeploy hello example template, you can use hello portal, Azure PowerShell, or Azure CLI.</span></span> <span data-ttu-id="67478-120">Используйте выпуски этих средств начиная с мая 2017 года.</span><span class="sxs-lookup"><span data-stu-id="67478-120">For Azure PowerShell or Azure CLI, you must use a release from May 2017 or later.</span></span> <span data-ttu-id="67478-121">Hello примерах предполагается, сохраненные локально hello шаблон в файл с именем **crossrgdeployment.json**.</span><span class="sxs-lookup"><span data-stu-id="67478-121">hello examples assume you have saved hello template locally as a file named **crossrgdeployment.json**.</span></span>

<span data-ttu-id="67478-122">При использовании PowerShell выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="67478-122">For PowerShell:</span></span>

```powershell
Login-AzureRmAccount

New-AzureRmResourceGroup -Name mainResourceGroup -Location "South Central US"
New-AzureRmResourceGroup -Name crossResourceGroupDeployment -Location "Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName mainResourceGroup `
  -TemplateFile c:\MyTemplates\crossrgdeployment.json
```

<span data-ttu-id="67478-123">При использовании Azure CLI выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="67478-123">For Azure CLI:</span></span>

```azurecli
az login

az group create --name mainResourceGroup --location "South Central US"
az group create --name crossResourceGroupDeployment --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group mainResourceGroup \
    --template-file crossrgdeployment.json
```

<span data-ttu-id="67478-124">После завершения развертывания вы увидите две группы ресурсов,</span><span class="sxs-lookup"><span data-stu-id="67478-124">After deployment completes, you see two resource groups.</span></span> <span data-ttu-id="67478-125">в каждой из которых содержится учетная запись хранения.</span><span class="sxs-lookup"><span data-stu-id="67478-125">Each resource group contains a storage account.</span></span>

## <a name="use-resourcegroup-function"></a><span data-ttu-id="67478-126">Использование функции resourceGroup()</span><span class="sxs-lookup"><span data-stu-id="67478-126">Use resourceGroup() function</span></span>

<span data-ttu-id="67478-127">Для кросс-развертывания группы ресурсов, hello [resouceGroup() функция](resource-group-template-functions-resource.md#resourcegroup) разрешает различаются в зависимости от способа задания hello вложенных шаблонов.</span><span class="sxs-lookup"><span data-stu-id="67478-127">For cross resource group deployments, hello [resouceGroup() function](resource-group-template-functions-resource.md#resourcegroup) resolves differently based on how you specify hello nested template.</span></span> 

<span data-ttu-id="67478-128">При внедрении один шаблон в другой шаблон resouceGroup() в вложенных шаблонов hello устраняет toohello родительской группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="67478-128">If you embed one template within another template, resouceGroup() in hello nested template resolves toohello parent resource group.</span></span> <span data-ttu-id="67478-129">Внедренные шаблон использует hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="67478-129">An embedded template uses hello following format:</span></span>

```json
"apiVersion": "2017-05-10",
"name": "embeddedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "template": {
        ...
        resourceGroup() refers tooparent resource group
    }
}
```

<span data-ttu-id="67478-130">При связывании отдельный шаблон tooa resouceGroup() в hello связанного шаблона разрешает toohello группы вложенных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="67478-130">If you link tooa separate template, resouceGroup() in hello linked template resolves toohello nested resource group.</span></span> <span data-ttu-id="67478-131">Связанный шаблон использует hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="67478-131">A linked template uses hello following format:</span></span>

```json
"apiVersion": "2017-05-10",
"name": "linkedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "templateLink": {
        ...
        resourceGroup() in linked template refers toolinked resource group
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="67478-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="67478-132">Next steps</span></span>

* <span data-ttu-id="67478-133">toodefine параметры в шаблоне, в статье toounderstand [понять структуру hello и синтаксис шаблоны Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="67478-133">toounderstand how toodefine parameters in your template, see [Understand hello structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="67478-134">Советы по устранению распространенных ошибок развертывания см. в разделе [Устранение распространенных ошибок развертывания в Azure с помощью Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="67478-134">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="67478-135">Сведения о развертывании шаблона, которому нужен токен SAS, см. в статье [Развертывание частного шаблона с помощью маркера SAS](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="67478-135">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
