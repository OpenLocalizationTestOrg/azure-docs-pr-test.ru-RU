---
title: "aaaExport шаблона диспетчера ресурсов с помощью Azure CLI | Документы Microsoft"
description: "С помощью диспетчера ресурсов Azure и Azure CLI tooexport шаблона из группы ресурсов."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/01/2017
ms.author: tomfitz
ms.openlocfilehash: 2d44a0a6e9717504d4c2a01254d826679b381f22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="export-azure-resource-manager-templates-with-azure-cli"></a><span data-ttu-id="3c02e-103">Экспорт шаблонов Azure Resource Manager с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3c02e-103">Export Azure Resource Manager templates with Azure CLI</span></span>

<span data-ttu-id="3c02e-104">Диспетчер ресурсов позволяет tooexport шаблона диспетчера ресурсов от существующих ресурсов в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="3c02e-104">Resource Manager enables you tooexport a Resource Manager template from existing resources in your subscription.</span></span> <span data-ttu-id="3c02e-105">Можно использовать, созданного шаблона toolearn о hello шаблона синтаксис или tooautomate hello повторное развертывание решения при необходимости.</span><span class="sxs-lookup"><span data-stu-id="3c02e-105">You can use that generated template toolearn about hello template syntax or tooautomate hello redeployment of your solution as needed.</span></span>

<span data-ttu-id="3c02e-106">Это важные toonote, что существует два разных способа tooexport шаблона:</span><span class="sxs-lookup"><span data-stu-id="3c02e-106">It is important toonote that there are two different ways tooexport a template:</span></span>

* <span data-ttu-id="3c02e-107">Вы можете экспортировать hello фактическое шаблона, который использовался для развертывания.</span><span class="sxs-lookup"><span data-stu-id="3c02e-107">You can export hello actual template that you used for a deployment.</span></span> <span data-ttu-id="3c02e-108">экспортированный шаблон Hello включает все параметры hello и переменные, точно так, как они выглядели в исходном шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="3c02e-108">hello exported template includes all hello parameters and variables exactly as they appeared in hello original template.</span></span> <span data-ttu-id="3c02e-109">Этот подход полезен при необходимости tooretrieve шаблона.</span><span class="sxs-lookup"><span data-stu-id="3c02e-109">This approach is helpful when you need tooretrieve a template.</span></span>
* <span data-ttu-id="3c02e-110">Вы можете экспортировать шаблон, который представляет текущее состояние группы ресурсов hello hello.</span><span class="sxs-lookup"><span data-stu-id="3c02e-110">You can export a template that represents hello current state of hello resource group.</span></span> <span data-ttu-id="3c02e-111">экспортированный шаблон Hello не основывается на любой шаблон, который использовался для развертывания.</span><span class="sxs-lookup"><span data-stu-id="3c02e-111">hello exported template is not based on any template that you used for deployment.</span></span> <span data-ttu-id="3c02e-112">Вместо этого он создает шаблон, который является моментальным снимком, группа ресурсов «hello».</span><span class="sxs-lookup"><span data-stu-id="3c02e-112">Instead, it creates a template that is a snapshot of hello resource group.</span></span> <span data-ttu-id="3c02e-113">экспортированный шаблон Hello имеет много жестко запрограммированных значений и, возможно, не все параметры, как обычно при определении.</span><span class="sxs-lookup"><span data-stu-id="3c02e-113">hello exported template has many hard-coded values and probably not as many parameters as you would typically define.</span></span> <span data-ttu-id="3c02e-114">Этот подход полезен, если вы изменили hello группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="3c02e-114">This approach is useful when you have modified hello resource group.</span></span> <span data-ttu-id="3c02e-115">Теперь требуется группа ресурсов hello toocapture как шаблон.</span><span class="sxs-lookup"><span data-stu-id="3c02e-115">Now, you need toocapture hello resource group as a template.</span></span>

<span data-ttu-id="3c02e-116">В этой статье показаны оба способа.</span><span class="sxs-lookup"><span data-stu-id="3c02e-116">This topic shows both approaches.</span></span>

## <a name="deploy-a-solution"></a><span data-ttu-id="3c02e-117">Развертывание решения</span><span class="sxs-lookup"><span data-stu-id="3c02e-117">Deploy a solution</span></span>

<span data-ttu-id="3c02e-118">Оба tooillustrate подходы для экспорта шаблона, давайте начнем, развернув решение tooyour подписки.</span><span class="sxs-lookup"><span data-stu-id="3c02e-118">tooillustrate both approaches for exporting a template, let's start by deploying a solution tooyour subscription.</span></span> <span data-ttu-id="3c02e-119">Если уже есть группа ресурсов в подписке, что требуется tooexport, у вас toodeploy этого решения.</span><span class="sxs-lookup"><span data-stu-id="3c02e-119">If you already have a resource group in your subscription that you want tooexport, you do not have toodeploy this solution.</span></span> <span data-ttu-id="3c02e-120">Однако hello оставшейся части этой статьи относится toohello шаблона для этого решения.</span><span class="sxs-lookup"><span data-stu-id="3c02e-120">However, hello remainder of this article refers toohello template for this solution.</span></span> <span data-ttu-id="3c02e-121">Пример сценария Hello развертывает учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="3c02e-121">hello example script deploys a storage account.</span></span>

```azurecli
az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name NewStorage \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
```  

## <a name="save-template-from-deployment-history"></a><span data-ttu-id="3c02e-122">Сохранение шаблона из журнала развертываний</span><span class="sxs-lookup"><span data-stu-id="3c02e-122">Save template from deployment history</span></span>

<span data-ttu-id="3c02e-123">Можно извлечь шаблон из журнала развертывания с помощью hello [az группы развертывания экспорта](/cli/azure/group/deployment#export) команды.</span><span class="sxs-lookup"><span data-stu-id="3c02e-123">You can retrieve a template from your deployment history by using hello [az group deployment export](/cli/azure/group/deployment#export) command.</span></span> <span data-ttu-id="3c02e-124">Следующий пример сохраняет hello шаблона ранее развертывание Hello:</span><span class="sxs-lookup"><span data-stu-id="3c02e-124">hello following example saves hello template that you previously deploy:</span></span>

```azurecli
az group deployment export --name NewStorage --resource-group ExampleGroup
```

<span data-ttu-id="3c02e-125">Возвращает шаблон hello.</span><span class="sxs-lookup"><span data-stu-id="3c02e-125">It returns hello template.</span></span> <span data-ttu-id="3c02e-126">Скопируйте hello JSON и сохраните как файл.</span><span class="sxs-lookup"><span data-stu-id="3c02e-126">Copy hello JSON, and save as a file.</span></span> <span data-ttu-id="3c02e-127">Обратите внимание, что hello точное шаблон, который используется для развертывания.</span><span class="sxs-lookup"><span data-stu-id="3c02e-127">Notice that it is hello exact template you used for deployment.</span></span> <span data-ttu-id="3c02e-128">Hello параметры и переменные соответствуют шаблону hello из GitHub.</span><span class="sxs-lookup"><span data-stu-id="3c02e-128">hello parameters and variables match hello template from GitHub.</span></span> <span data-ttu-id="3c02e-129">Этот шаблон можно развернуть повторно.</span><span class="sxs-lookup"><span data-stu-id="3c02e-129">You can redeploy this template.</span></span>


## <a name="export-resource-group-as-template"></a><span data-ttu-id="3c02e-130">Экспорт группы ресурсов в виде шаблона</span><span class="sxs-lookup"><span data-stu-id="3c02e-130">Export resource group as template</span></span>

<span data-ttu-id="3c02e-131">Вместо извлечения шаблона из журнала развертывания hello, вы можете получить шаблон, который представляет текущее состояние hello группы ресурсов с помощью hello [экспорта группы az](/cli/azure/group#export) команды.</span><span class="sxs-lookup"><span data-stu-id="3c02e-131">Instead of retrieving a template from hello deployment history, you can retrieve a template that represents hello current state of a resource group by using hello [az group export](/cli/azure/group#export) command.</span></span> <span data-ttu-id="3c02e-132">Эта команда используется в том случае, если вы внесли многие группы ресурсов tooyour изменения и не существующий шаблон представляет все изменения hello.</span><span class="sxs-lookup"><span data-stu-id="3c02e-132">You use this command when you have made many changes tooyour resource group and no existing template represents all hello changes.</span></span>

```azurecli
az group export --name ExampleGroup
```

<span data-ttu-id="3c02e-133">Возвращает шаблон hello.</span><span class="sxs-lookup"><span data-stu-id="3c02e-133">It returns hello template.</span></span> <span data-ttu-id="3c02e-134">Скопируйте hello JSON и сохраните как файл.</span><span class="sxs-lookup"><span data-stu-id="3c02e-134">Copy hello JSON, and save as a file.</span></span> <span data-ttu-id="3c02e-135">Обратите внимание, что это отличается от шаблона hello в GitHub.</span><span class="sxs-lookup"><span data-stu-id="3c02e-135">Notice that it is different than hello template in GitHub.</span></span> <span data-ttu-id="3c02e-136">У него другие параметры и нет переменных.</span><span class="sxs-lookup"><span data-stu-id="3c02e-136">It has different parameters and no variables.</span></span> <span data-ttu-id="3c02e-137">хранилище Hello SKU и расположение являются жестко toovalues.</span><span class="sxs-lookup"><span data-stu-id="3c02e-137">hello storage SKU and location are hard-coded toovalues.</span></span> <span data-ttu-id="3c02e-138">Hello пример hello экспортированный шаблон, но ваш шаблон имеет имя параметра немного отличается.</span><span class="sxs-lookup"><span data-stu-id="3c02e-138">hello following example shows hello exported template, but your template has a slightly different parameter name:</span></span>

```json
{
  "parameters": {
    "storageAccounts_mcyzaljiv7qncstandardsa_name": {
      "type": "String",
      "defaultValue": null
    }
  },
  "variables": {},
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "resources": [
    {
      "tags": {},
      "dependsOn": [],
      "apiVersion": "2016-01-01",
      "sku": {
        "name": "Standard_LRS",
        "tier": "Standard"
      },
      "kind": "Storage",
      "type": "Microsoft.Storage/storageAccounts",
      "location": "centralus",
      "name": "[parameters('storageAccounts_mcyzaljiv7qncstandardsa_name')]",
      "properties": {}
    }
  ],
  "contentVersion": "1.0.0.0"
}
```

<span data-ttu-id="3c02e-139">Можно повторно развернуть этот шаблон, но он требует угадывания уникальное имя для учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="3c02e-139">You can redeploy this template, but it requires guessing a unique name for hello storage account.</span></span> <span data-ttu-id="3c02e-140">Имя параметра Hello немного отличается.</span><span class="sxs-lookup"><span data-stu-id="3c02e-140">hello name of your parameter is slightly different.</span></span>

```azurecli
az group deployment create --name NewStorage --resource-group ExampleGroup \
  --template-file examplegroup.json \
  --parameters "{\"storageAccounts_mcyzaljiv7qncstandardsa_name\":{\"value\":\"tfstore0501\"}}"
```

## <a name="customize-exported-template"></a><span data-ttu-id="3c02e-141">Настройка экспортированного шаблона</span><span class="sxs-lookup"><span data-stu-id="3c02e-141">Customize exported template</span></span>

<span data-ttu-id="3c02e-142">Вы можете изменить этот шаблон toomake его toouse проще и гибче.</span><span class="sxs-lookup"><span data-stu-id="3c02e-142">You can modify this template toomake it easier toouse and more flexible.</span></span> <span data-ttu-id="3c02e-143">tooallow для дополнительных местоположений, изменение hello расположение свойство toouse hello местоположения hello группа ресурсов:</span><span class="sxs-lookup"><span data-stu-id="3c02e-143">tooallow for more locations, change hello location property toouse hello same location as hello resource group:</span></span>

```json
"location": "[resourceGroup().location]",
```

<span data-ttu-id="3c02e-144">tooavoid наличие tooguess uniques имени для учетной записи хранилища, удаление параметра hello hello имени учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="3c02e-144">tooavoid having tooguess a uniques name for storage account, remove hello parameter for hello storage account name.</span></span> <span data-ttu-id="3c02e-145">Добавьте параметр для суффикса имени хранилища и номер SKU хранилища:</span><span class="sxs-lookup"><span data-stu-id="3c02e-145">Add a parameter for a storage name suffix, and a storage SKU:</span></span>

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

<span data-ttu-id="3c02e-146">Добавьте переменную, которая создает hello имя учетной записи хранилища с помощью функции hello uniqueString:</span><span class="sxs-lookup"><span data-stu-id="3c02e-146">Add a variable that constructs hello storage account name with hello uniqueString function:</span></span>

```json
"variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
```

<span data-ttu-id="3c02e-147">Задайте имя hello переменной toohello учетной записи хранилища hello:</span><span class="sxs-lookup"><span data-stu-id="3c02e-147">Set hello name of hello storage account toohello variable:</span></span>

```json
"name": "[variables('storageAccountName')]",
```

<span data-ttu-id="3c02e-148">Задайте для параметра toohello hello SKU:</span><span class="sxs-lookup"><span data-stu-id="3c02e-148">Set hello SKU toohello parameter:</span></span>

```json
"sku": {
    "name": "[parameters('storageAccountType')]",
    "tier": "Standard"
},
```

<span data-ttu-id="3c02e-149">Ваш шаблон теперь выглядит так:</span><span class="sxs-lookup"><span data-stu-id="3c02e-149">Your template now looks like:</span></span>

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

<span data-ttu-id="3c02e-150">Повторное развертывание hello измененный шаблон.</span><span class="sxs-lookup"><span data-stu-id="3c02e-150">Redeploy hello modified template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c02e-151">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3c02e-151">Next steps</span></span>
* <span data-ttu-id="3c02e-152">Сведения об использовании портала tooexport hello шаблона см. в разделе [Экспорт шаблона диспетчера ресурсов Azure с существующие ресурсы](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="3c02e-152">For information about using hello portal tooexport a template, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="3c02e-153">toodefine параметры в шаблоне, в разделе [разработки шаблонов](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="3c02e-153">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="3c02e-154">Советы по устранению распространенных ошибок развертывания см. в разделе [Устранение распространенных ошибок развертывания в Azure с помощью Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="3c02e-154">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>