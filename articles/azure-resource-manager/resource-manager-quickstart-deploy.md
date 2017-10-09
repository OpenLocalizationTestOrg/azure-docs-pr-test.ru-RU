---
title: "ресурсы tooAzure aaaDeploy | Документы Microsoft"
description: "С помощью Azure PowerShell или Azure CLI tooAzure toodeploy ресурсов. Hello ресурсы определяются в шаблоне диспетчера ресурсов."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/16/2017
ms.author: tomfitz
ms.openlocfilehash: 0cd3f8ad45af1fb85c78899b56f6807d00b859f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-tooazure"></a><span data-ttu-id="94e5a-104">Развертывание tooAzure ресурсы</span><span class="sxs-lookup"><span data-stu-id="94e5a-104">Deploy resources tooAzure</span></span>

<span data-ttu-id="94e5a-105">В этом разделе показано, как ресурсы toodeploy tooyour подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="94e5a-105">This topic shows how toodeploy resources tooyour Azure subscription.</span></span> <span data-ttu-id="94e5a-106">Можно использовать Azure PowerShell или Azure CLI toodeploy шаблона диспетчера ресурсов, который определяет hello инфраструктуры для вашего решения.</span><span class="sxs-lookup"><span data-stu-id="94e5a-106">You can use either Azure PowerShell or Azure CLI toodeploy a Resource Manager template that defines hello infrastructure for your solution.</span></span>

<span data-ttu-id="94e5a-107">Введение tooconcepts для диспетчера ресурсов. в разделе [Обзор диспетчера ресурсов Azure](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="94e5a-107">For an introduction tooconcepts of Resource Manager, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

## <a name="steps-for-deployment"></a><span data-ttu-id="94e5a-108">Этапы развертывания</span><span class="sxs-lookup"><span data-stu-id="94e5a-108">Steps for deployment</span></span>

<span data-ttu-id="94e5a-109">В этом разделе предполагается развертывании hello [пример шаблона хранения](#example-storage-template) в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="94e5a-109">This topic assumes you are deploying hello [example storage template](#example-storage-template) in this topic.</span></span> <span data-ttu-id="94e5a-110">Можно использовать другой шаблон, но hello переданных параметров отличаются от отображаемых в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="94e5a-110">You can use a different template, but hello parameters you pass are different than what is shown in this topic.</span></span>

<span data-ttu-id="94e5a-111">После создания шаблона, указаны hello общие шаги по развертыванию ваш шаблон.</span><span class="sxs-lookup"><span data-stu-id="94e5a-111">After creating a template, hello general steps for deploying your template are:</span></span>

1. <span data-ttu-id="94e5a-112">Войдите в учетную запись tooyour</span><span class="sxs-lookup"><span data-stu-id="94e5a-112">Log in tooyour account</span></span>
2. <span data-ttu-id="94e5a-113">Выберите toouse подписки hello (необходимо, только если у вас несколько подписок, и требуется toouse, который не подписки по умолчанию hello)</span><span class="sxs-lookup"><span data-stu-id="94e5a-113">Select hello subscription toouse (only necessary if you have multiple subscriptions, and you want toouse one that is not hello default subscription)</span></span>
3. <span data-ttu-id="94e5a-114">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="94e5a-114">Create a resource group</span></span>
4. <span data-ttu-id="94e5a-115">Развертывание шаблона hello</span><span class="sxs-lookup"><span data-stu-id="94e5a-115">Deploy hello template</span></span>
5. <span data-ttu-id="94e5a-116">Проверка состояния развертывания</span><span class="sxs-lookup"><span data-stu-id="94e5a-116">Check your deployment status</span></span>

<span data-ttu-id="94e5a-117">Hello следующих разделах показано, как tooperform те шагов, при [PowerShell](#powershell) или [Azure CLI](#azure-cli).</span><span class="sxs-lookup"><span data-stu-id="94e5a-117">hello following sections show how tooperform those steps with [PowerShell](#powershell) or [Azure CLI](#azure-cli).</span></span>

## <a name="powershell"></a><span data-ttu-id="94e5a-118">PowerShell</span><span class="sxs-lookup"><span data-stu-id="94e5a-118">PowerShell</span></span>

1. <span data-ttu-id="94e5a-119">tooinstall Azure PowerShell, в разделе [приступить к работе с помощью командлетов Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="94e5a-119">tooinstall Azure PowerShell, see [Get started with Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>

2. <span data-ttu-id="94e5a-120">tooquickly начало работы по развертыванию, выполните следующие командлеты hello.</span><span class="sxs-lookup"><span data-stu-id="94e5a-120">tooquickly get started with deployment, use hello following cmdlets:</span></span>

  ```powershell
  Login-AzureRmAccount
  Set-AzureRmContext -SubscriptionID {subscription-id}

  New-AzureRmResourceGroup -Name ExampleGroup -Location "Central US"
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json 
  ```

  <span data-ttu-id="94e5a-121">Hello `Set-AzureRmContext` командлета требуется только в том случае, если требуется toouse подписки, отличные от вашей подписки по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="94e5a-121">hello `Set-AzureRmContext` cmdlet is only needed if you want toouse a subscription other than your default subscription.</span></span> <span data-ttu-id="94e5a-122">toosee все подписки и идентификаторов, используйте:</span><span class="sxs-lookup"><span data-stu-id="94e5a-122">toosee all your subscriptions and their IDs, use:</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

3. <span data-ttu-id="94e5a-123">Hello развертывания может занять несколько минут toocomplete.</span><span class="sxs-lookup"><span data-stu-id="94e5a-123">hello deployment can take a few minutes toocomplete.</span></span> <span data-ttu-id="94e5a-124">По завершении появится сообщение следующего вида.</span><span class="sxs-lookup"><span data-stu-id="94e5a-124">When it finishes, you see a message similar to:</span></span>

  ```powershell
  DeploymentName          : ExampleDeployment
  CorrelationId           : 07b3b233-8367-4a0b-b9bc-7aa189065665
  ResourceGroupName       : ExampleGroup
  ProvisioningState       : Succeeded
  ...
  ```

4. <span data-ttu-id="94e5a-125">toosee, учетной записи группы и хранения ресурсов, которые были развернуты tooyour подписки, используйте:</span><span class="sxs-lookup"><span data-stu-id="94e5a-125">toosee that your resource group and storage account were deployed tooyour subscription, use:</span></span>

  ```powershell
  Get-AzureRmResourceGroup -Name ExampleGroup
  Find-AzureRmResource -ResourceGroupNameEquals ExampleGroup
  ```

5. <span data-ttu-id="94e5a-126">Параметры шаблона можно указать в качестве параметров PowerShell при развертывании шаблона.</span><span class="sxs-lookup"><span data-stu-id="94e5a-126">You can specify template parameters as PowerShell parameters when deploying a template.</span></span> <span data-ttu-id="94e5a-127">Hello предыдущий пример не включали никакие параметры шаблона, поэтому используются значения по умолчанию hello в шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="94e5a-127">hello earlier example did not include any template parameters, so hello default values in hello template were used.</span></span> <span data-ttu-id="94e5a-128">toodeploy еще одно хранилище учетную запись, а также указать значения параметров для hello префикс имени хранилища и учетной записи хранилища hello SKU, используйте:</span><span class="sxs-lookup"><span data-stu-id="94e5a-128">toodeploy another storage account, and provide parameter values for hello storage name prefix and hello storage account SKU, use:</span></span>

  ```powershell
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment2 -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json -storageNamePrefix "contoso" -storageSKU "Standard_GRS"
  ```

  <span data-ttu-id="94e5a-129">Теперь в группе ресурсов две учетные записи хранения.</span><span class="sxs-lookup"><span data-stu-id="94e5a-129">You now have two storage accounts in your resource group.</span></span> 

## <a name="azure-cli"></a><span data-ttu-id="94e5a-130">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="94e5a-130">Azure CLI</span></span>

1. <span data-ttu-id="94e5a-131">tooinstall Azure CLI см. в разделе [установить CLI Azure 2.0](/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="94e5a-131">tooinstall Azure CLI, see [Install Azure CLI 2.0](/cli/azure/install-az-cli2).</span></span>

2. <span data-ttu-id="94e5a-132">tooquickly начало работы по развертыванию, выполните следующие команды hello.</span><span class="sxs-lookup"><span data-stu-id="94e5a-132">tooquickly get started with deployment, use hello following commands:</span></span>

  ```azurecli
  az login
  az account set --subscription {subscription-id}

  az group create --name ExampleGroup --location "Central US"
  az group deployment create --name ExampleDeployment --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json
  ```

  <span data-ttu-id="94e5a-133">Hello `az account set` команды необходим только в том случае, если требуется toouse подписки, отличные от вашей подписки по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="94e5a-133">hello `az account set` command is only needed if you want toouse a subscription other than your default subscription.</span></span> <span data-ttu-id="94e5a-134">toosee все подписки и идентификаторов, используйте:</span><span class="sxs-lookup"><span data-stu-id="94e5a-134">toosee all your subscriptions and their IDs, use:</span></span>

  ```azurecli
  az account list
  ```

3. <span data-ttu-id="94e5a-135">Hello развертывания может занять несколько минут toocomplete.</span><span class="sxs-lookup"><span data-stu-id="94e5a-135">hello deployment can take a few minutes toocomplete.</span></span> <span data-ttu-id="94e5a-136">По завершении появится сообщение следующего вида.</span><span class="sxs-lookup"><span data-stu-id="94e5a-136">When it finishes, you see a message similar to:</span></span>

  ```azurecli
  "provisioningState": "Succeeded",
  ```

4. <span data-ttu-id="94e5a-137">toosee, учетной записи группы и хранения ресурсов, которые были развернуты tooyour подписки, используйте:</span><span class="sxs-lookup"><span data-stu-id="94e5a-137">toosee that your resource group and storage account were deployed tooyour subscription, use:</span></span>

  ```azurecli
  az group show --name ExampleGroup
  az resource list --resource-group ExampleGroup
  ```

5. <span data-ttu-id="94e5a-138">Параметры шаблона можно указать в качестве параметров PowerShell при развертывании шаблона.</span><span class="sxs-lookup"><span data-stu-id="94e5a-138">You can specify template parameters as PowerShell parameters when deploying a template.</span></span> <span data-ttu-id="94e5a-139">Hello предыдущий пример не включали никакие параметры шаблона, поэтому используются значения по умолчанию hello в шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="94e5a-139">hello earlier example did not include any template parameters, so hello default values in hello template were used.</span></span> <span data-ttu-id="94e5a-140">toodeploy еще одно хранилище учетную запись, а также указать значения параметров для hello префикс имени хранилища и учетной записи хранилища hello SKU, используйте:</span><span class="sxs-lookup"><span data-stu-id="94e5a-140">toodeploy another storage account, and provide parameter values for hello storage name prefix and hello storage account SKU, use:</span></span>

  ```azurecli
  az group deployment create --name ExampleDeployment2 --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json --parameters '{"storageNamePrefix":{"value":"contoso"},"storageSKU":{"value":"Standard_GRS"}}'
  ```

  <span data-ttu-id="94e5a-141">Теперь в группе ресурсов две учетные записи хранения.</span><span class="sxs-lookup"><span data-stu-id="94e5a-141">You now have two storage accounts in your resource group.</span></span> 

## <a name="example-storage-template"></a><span data-ttu-id="94e5a-142">Пример шаблона хранилища</span><span class="sxs-lookup"><span data-stu-id="94e5a-142">Example storage template</span></span>

<span data-ttu-id="94e5a-143">Используйте следующий пример шаблона toodeploy подписки tooyour учетной записи хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="94e5a-143">Use hello following example template toodeploy a storage account tooyour subscription:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "hello value toouse for starting hello storage account name."
      }
    },
    "storageSKU": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_ZRS",
        "Standard_GRS",
        "Standard_RAGRS",
        "Premium_LRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "hello type of replication toouse for hello storage account."
      }
    }
  },
  "variables": {
    "storageName": "[concat(parameters('storageNamePrefix'), uniqueString(resourceGroup().id))]"
  },
  "resources": [
    {
      "name": "[variables('storageName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-05-01",
      "sku": {
        "name": "[parameters('storageSKU')]"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {
      }
    }
  ],
  "outputs": {  }
}
```

## <a name="next-steps"></a><span data-ttu-id="94e5a-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="94e5a-144">Next steps</span></span>

* <span data-ttu-id="94e5a-145">Подробные сведения об использовании шаблонов toodeploy PowerShell см. в разделе [развертывания ресурсов с помощью шаблонов диспетчера ресурсов и Azure PowerShell](/azure/azure-resource-manager/resource-group-template-deploy).</span><span class="sxs-lookup"><span data-stu-id="94e5a-145">For detailed information about using PowerShell toodeploy templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](/azure/azure-resource-manager/resource-group-template-deploy).</span></span>
* <span data-ttu-id="94e5a-146">Подробные сведения об использовании шаблонов toodeploy Azure CLI. в разделе [развертывания ресурсов с помощью шаблонов диспетчера ресурсов и Azure CLI](/azure/azure-resource-manager/resource-group-template-deploy-cli).</span><span class="sxs-lookup"><span data-stu-id="94e5a-146">For detailed information about using Azure CLI toodeploy templates, see [Deploy resources with Resource Manager templates and Azure CLI](/azure/azure-resource-manager/resource-group-template-deploy-cli).</span></span>



