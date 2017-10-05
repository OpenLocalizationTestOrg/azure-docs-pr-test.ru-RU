---
title: "Развертывание ресурсов в Azure | Документация Майкрософт"
description: "Использование Azure PowerShell или Azure CLI для развертывания ресурсов в Azure. Эти ресурсы определяются в шаблоне Resource Manager."
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
ms.openlocfilehash: 19d5ec337a18b1a159de05ed611b2ccd0c15c592
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-resources-to-azure"></a><span data-ttu-id="e5fa3-104">Развертывание ресурсов в Azure</span><span class="sxs-lookup"><span data-stu-id="e5fa3-104">Deploy resources to Azure</span></span>

<span data-ttu-id="e5fa3-105">В этом разделе показано, как развернуть ресурсы в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="e5fa3-105">This topic shows how to deploy resources to your Azure subscription.</span></span> <span data-ttu-id="e5fa3-106">Можно использовать Azure PowerShell или Azure CLI, чтобы развернуть шаблон Resource Manager, определяющий инфраструктуру для решения.</span><span class="sxs-lookup"><span data-stu-id="e5fa3-106">You can use either Azure PowerShell or Azure CLI to deploy a Resource Manager template that defines the infrastructure for your solution.</span></span>

<span data-ttu-id="e5fa3-107">Введение в основные понятия Azure Resource Manager см. в статье [Общие сведения о диспетчере ресурсов Azure](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e5fa3-107">For an introduction to concepts of Resource Manager, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

## <a name="steps-for-deployment"></a><span data-ttu-id="e5fa3-108">Этапы развертывания</span><span class="sxs-lookup"><span data-stu-id="e5fa3-108">Steps for deployment</span></span>

<span data-ttu-id="e5fa3-109">В этом разделе предполагается, что вы развертываете [пример шаблона хранилища](#example-storage-template).</span><span class="sxs-lookup"><span data-stu-id="e5fa3-109">This topic assumes you are deploying the [example storage template](#example-storage-template) in this topic.</span></span> <span data-ttu-id="e5fa3-110">Можно использовать другой шаблон, но передаваемые для него параметры будут отличаться от показанных в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="e5fa3-110">You can use a different template, but the parameters you pass are different than what is shown in this topic.</span></span>

<span data-ttu-id="e5fa3-111">Ниже приведены общие действия по развертыванию созданного шаблона.</span><span class="sxs-lookup"><span data-stu-id="e5fa3-111">After creating a template, the general steps for deploying your template are:</span></span>

1. <span data-ttu-id="e5fa3-112">Вход в учетную запись</span><span class="sxs-lookup"><span data-stu-id="e5fa3-112">Log in to your account</span></span>
2. <span data-ttu-id="e5fa3-113">Выберите используемую подписку (только если у вас их несколько и требуется выбрать подписку, не используемую по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="e5fa3-113">Select the subscription to use (only necessary if you have multiple subscriptions, and you want to use one that is not the default subscription)</span></span>
3. <span data-ttu-id="e5fa3-114">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="e5fa3-114">Create a resource group</span></span>
4. <span data-ttu-id="e5fa3-115">Развертывание шаблона</span><span class="sxs-lookup"><span data-stu-id="e5fa3-115">Deploy the template</span></span>
5. <span data-ttu-id="e5fa3-116">Проверка состояния развертывания</span><span class="sxs-lookup"><span data-stu-id="e5fa3-116">Check your deployment status</span></span>

<span data-ttu-id="e5fa3-117">В разделах ниже показано, как выполнить эти действия с помощью [PowerShell](#powershell) или [Azure CLI](#azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e5fa3-117">The following sections show how to perform those steps with [PowerShell](#powershell) or [Azure CLI](#azure-cli).</span></span>

## <a name="powershell"></a><span data-ttu-id="e5fa3-118">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e5fa3-118">PowerShell</span></span>

1. <span data-ttu-id="e5fa3-119">Чтобы установить Azure PowerShell, ознакомьтесь с разделом [Get started with Azure PowerShell cmdlets](/powershell/azure/overview) (Приступая к работе с командлетами Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="e5fa3-119">To install Azure PowerShell, see [Get started with Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>

2. <span data-ttu-id="e5fa3-120">Чтобы быстро приступить к развертыванию, используйте следующие командлеты.</span><span class="sxs-lookup"><span data-stu-id="e5fa3-120">To quickly get started with deployment, use the following cmdlets:</span></span>

  ```powershell
  Login-AzureRmAccount
  Set-AzureRmContext -SubscriptionID {subscription-id}

  New-AzureRmResourceGroup -Name ExampleGroup -Location "Central US"
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json 
  ```

  <span data-ttu-id="e5fa3-121">Командлет `Set-AzureRmContext` требуется только в том случае, если вы хотите использовать подписку, отличную от вашей подписки по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e5fa3-121">The `Set-AzureRmContext` cmdlet is only needed if you want to use a subscription other than your default subscription.</span></span> <span data-ttu-id="e5fa3-122">Чтобы просмотреть все подписки и их идентификаторы, используйте следующий командлет.</span><span class="sxs-lookup"><span data-stu-id="e5fa3-122">To see all your subscriptions and their IDs, use:</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

3. <span data-ttu-id="e5fa3-123">Развертывание может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="e5fa3-123">The deployment can take a few minutes to complete.</span></span> <span data-ttu-id="e5fa3-124">По завершении появится сообщение следующего вида.</span><span class="sxs-lookup"><span data-stu-id="e5fa3-124">When it finishes, you see a message similar to:</span></span>

  ```powershell
  DeploymentName          : ExampleDeployment
  CorrelationId           : 07b3b233-8367-4a0b-b9bc-7aa189065665
  ResourceGroupName       : ExampleGroup
  ProvisioningState       : Succeeded
  ...
  ```

4. <span data-ttu-id="e5fa3-125">Чтобы убедиться, что группа ресурсов и учетная запись хранения были развернуты в вашей подписке, введите следующую команду.</span><span class="sxs-lookup"><span data-stu-id="e5fa3-125">To see that your resource group and storage account were deployed to your subscription, use:</span></span>

  ```powershell
  Get-AzureRmResourceGroup -Name ExampleGroup
  Find-AzureRmResource -ResourceGroupNameEquals ExampleGroup
  ```

5. <span data-ttu-id="e5fa3-126">Параметры шаблона можно указать в качестве параметров PowerShell при развертывании шаблона.</span><span class="sxs-lookup"><span data-stu-id="e5fa3-126">You can specify template parameters as PowerShell parameters when deploying a template.</span></span> <span data-ttu-id="e5fa3-127">Предыдущий пример не содержал каких-либо параметров шаблона, поэтому в нем использовались значения по умолчанию, заданные в шаблоне.</span><span class="sxs-lookup"><span data-stu-id="e5fa3-127">The earlier example did not include any template parameters, so the default values in the template were used.</span></span> <span data-ttu-id="e5fa3-128">Чтобы развернуть еще одну учетную запись хранения и указать значения параметров для префикса имени хранилища и номера SKU учетной записи хранения, используйте приведенный ниже командлет.</span><span class="sxs-lookup"><span data-stu-id="e5fa3-128">To deploy another storage account, and provide parameter values for the storage name prefix and the storage account SKU, use:</span></span>

  ```powershell
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment2 -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json -storageNamePrefix "contoso" -storageSKU "Standard_GRS"
  ```

  <span data-ttu-id="e5fa3-129">Теперь в группе ресурсов две учетные записи хранения.</span><span class="sxs-lookup"><span data-stu-id="e5fa3-129">You now have two storage accounts in your resource group.</span></span> 

## <a name="azure-cli"></a><span data-ttu-id="e5fa3-130">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="e5fa3-130">Azure CLI</span></span>

1. <span data-ttu-id="e5fa3-131">Чтобы установить Azure CLI, ознакомьтесь с разделом [Install Azure CLI 2.0](/cli/azure/install-az-cli2) (Установка Azure CLI 2.0).</span><span class="sxs-lookup"><span data-stu-id="e5fa3-131">To install Azure CLI, see [Install Azure CLI 2.0](/cli/azure/install-az-cli2).</span></span>

2. <span data-ttu-id="e5fa3-132">Чтобы быстро приступить к выполнению развертывания, воспользуйтесь следующими командами:</span><span class="sxs-lookup"><span data-stu-id="e5fa3-132">To quickly get started with deployment, use the following commands:</span></span>

  ```azurecli
  az login
  az account set --subscription {subscription-id}

  az group create --name ExampleGroup --location "Central US"
  az group deployment create --name ExampleDeployment --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json
  ```

  <span data-ttu-id="e5fa3-133">Выполнять команду `az account set` требуется только в том случае, если вы хотите использовать подписку, отличную от вашей подписки по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e5fa3-133">The `az account set` command is only needed if you want to use a subscription other than your default subscription.</span></span> <span data-ttu-id="e5fa3-134">Чтобы просмотреть все подписки и их идентификаторы, используйте следующий командлет.</span><span class="sxs-lookup"><span data-stu-id="e5fa3-134">To see all your subscriptions and their IDs, use:</span></span>

  ```azurecli
  az account list
  ```

3. <span data-ttu-id="e5fa3-135">Развертывание может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="e5fa3-135">The deployment can take a few minutes to complete.</span></span> <span data-ttu-id="e5fa3-136">По завершении появится сообщение следующего вида.</span><span class="sxs-lookup"><span data-stu-id="e5fa3-136">When it finishes, you see a message similar to:</span></span>

  ```azurecli
  "provisioningState": "Succeeded",
  ```

4. <span data-ttu-id="e5fa3-137">Чтобы убедиться, что группа ресурсов и учетная запись хранения были развернуты в вашей подписке, введите следующую команду.</span><span class="sxs-lookup"><span data-stu-id="e5fa3-137">To see that your resource group and storage account were deployed to your subscription, use:</span></span>

  ```azurecli
  az group show --name ExampleGroup
  az resource list --resource-group ExampleGroup
  ```

5. <span data-ttu-id="e5fa3-138">Параметры шаблона можно указать в качестве параметров PowerShell при развертывании шаблона.</span><span class="sxs-lookup"><span data-stu-id="e5fa3-138">You can specify template parameters as PowerShell parameters when deploying a template.</span></span> <span data-ttu-id="e5fa3-139">Предыдущий пример не содержал каких-либо параметров шаблона, поэтому в нем использовались значения по умолчанию, заданные в шаблоне.</span><span class="sxs-lookup"><span data-stu-id="e5fa3-139">The earlier example did not include any template parameters, so the default values in the template were used.</span></span> <span data-ttu-id="e5fa3-140">Чтобы развернуть еще одну учетную запись хранения и указать значения параметров для префикса имени хранилища и номера SKU учетной записи хранения, используйте приведенный ниже командлет.</span><span class="sxs-lookup"><span data-stu-id="e5fa3-140">To deploy another storage account, and provide parameter values for the storage name prefix and the storage account SKU, use:</span></span>

  ```azurecli
  az group deployment create --name ExampleDeployment2 --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json --parameters '{"storageNamePrefix":{"value":"contoso"},"storageSKU":{"value":"Standard_GRS"}}'
  ```

  <span data-ttu-id="e5fa3-141">Теперь в группе ресурсов две учетные записи хранения.</span><span class="sxs-lookup"><span data-stu-id="e5fa3-141">You now have two storage accounts in your resource group.</span></span> 

## <a name="example-storage-template"></a><span data-ttu-id="e5fa3-142">Пример шаблона хранилища</span><span class="sxs-lookup"><span data-stu-id="e5fa3-142">Example storage template</span></span>

<span data-ttu-id="e5fa3-143">Используйте приведенный пример шаблона для развертывания учетной записи хранение в своей подписке.</span><span class="sxs-lookup"><span data-stu-id="e5fa3-143">Use the following example template to deploy a storage account to your subscription:</span></span>

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
        "description": "The value to use for starting the storage account name."
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
        "description": "The type of replication to use for the storage account."
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

## <a name="next-steps"></a><span data-ttu-id="e5fa3-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e5fa3-144">Next steps</span></span>

* <span data-ttu-id="e5fa3-145">Дополнительные сведения о развертывании шаблонов с помощью PowerShell см. в статье [Развертывание ресурсов с использованием шаблонов Resource Manager и Azure PowerShell](/azure/azure-resource-manager/resource-group-template-deploy).</span><span class="sxs-lookup"><span data-stu-id="e5fa3-145">For detailed information about using PowerShell to deploy templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](/azure/azure-resource-manager/resource-group-template-deploy).</span></span>
* <span data-ttu-id="e5fa3-146">Дополнительные сведения о развертывании шаблонов с помощью Azure CLI см. в статье [Развертывание ресурсов с использованием шаблонов Resource Manager и Azure CLI](/azure/azure-resource-manager/resource-group-template-deploy-cli).</span><span class="sxs-lookup"><span data-stu-id="e5fa3-146">For detailed information about using Azure CLI to deploy templates, see [Deploy resources with Resource Manager templates and Azure CLI](/azure/azure-resource-manager/resource-group-template-deploy-cli).</span></span>



