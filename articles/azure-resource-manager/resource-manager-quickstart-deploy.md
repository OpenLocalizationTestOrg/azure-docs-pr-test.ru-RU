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
# <a name="deploy-resources-tooazure"></a>Развертывание tooAzure ресурсы

В этом разделе показано, как ресурсы toodeploy tooyour подписки Azure. Можно использовать Azure PowerShell или Azure CLI toodeploy шаблона диспетчера ресурсов, который определяет hello инфраструктуры для вашего решения.

Введение tooconcepts для диспетчера ресурсов. в разделе [Обзор диспетчера ресурсов Azure](resource-group-overview.md).

## <a name="steps-for-deployment"></a>Этапы развертывания

В этом разделе предполагается развертывании hello [пример шаблона хранения](#example-storage-template) в этом разделе. Можно использовать другой шаблон, но hello переданных параметров отличаются от отображаемых в этом разделе.

После создания шаблона, указаны hello общие шаги по развертыванию ваш шаблон.

1. Войдите в учетную запись tooyour
2. Выберите toouse подписки hello (необходимо, только если у вас несколько подписок, и требуется toouse, который не подписки по умолчанию hello)
3. Создание группы ресурсов
4. Развертывание шаблона hello
5. Проверка состояния развертывания

Hello следующих разделах показано, как tooperform те шагов, при [PowerShell](#powershell) или [Azure CLI](#azure-cli).

## <a name="powershell"></a>PowerShell

1. tooinstall Azure PowerShell, в разделе [приступить к работе с помощью командлетов Azure PowerShell](/powershell/azure/overview).

2. tooquickly начало работы по развертыванию, выполните следующие командлеты hello.

  ```powershell
  Login-AzureRmAccount
  Set-AzureRmContext -SubscriptionID {subscription-id}

  New-AzureRmResourceGroup -Name ExampleGroup -Location "Central US"
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json 
  ```

  Hello `Set-AzureRmContext` командлета требуется только в том случае, если требуется toouse подписки, отличные от вашей подписки по умолчанию. toosee все подписки и идентификаторов, используйте:

  ```powershell
  Get-AzureRmSubscription
  ```

3. Hello развертывания может занять несколько минут toocomplete. По завершении появится сообщение следующего вида.

  ```powershell
  DeploymentName          : ExampleDeployment
  CorrelationId           : 07b3b233-8367-4a0b-b9bc-7aa189065665
  ResourceGroupName       : ExampleGroup
  ProvisioningState       : Succeeded
  ...
  ```

4. toosee, учетной записи группы и хранения ресурсов, которые были развернуты tooyour подписки, используйте:

  ```powershell
  Get-AzureRmResourceGroup -Name ExampleGroup
  Find-AzureRmResource -ResourceGroupNameEquals ExampleGroup
  ```

5. Параметры шаблона можно указать в качестве параметров PowerShell при развертывании шаблона. Hello предыдущий пример не включали никакие параметры шаблона, поэтому используются значения по умолчанию hello в шаблоне hello. toodeploy еще одно хранилище учетную запись, а также указать значения параметров для hello префикс имени хранилища и учетной записи хранилища hello SKU, используйте:

  ```powershell
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment2 -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json -storageNamePrefix "contoso" -storageSKU "Standard_GRS"
  ```

  Теперь в группе ресурсов две учетные записи хранения. 

## <a name="azure-cli"></a>Инфраструктура CLI Azure

1. tooinstall Azure CLI см. в разделе [установить CLI Azure 2.0](/cli/azure/install-az-cli2).

2. tooquickly начало работы по развертыванию, выполните следующие команды hello.

  ```azurecli
  az login
  az account set --subscription {subscription-id}

  az group create --name ExampleGroup --location "Central US"
  az group deployment create --name ExampleDeployment --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json
  ```

  Hello `az account set` команды необходим только в том случае, если требуется toouse подписки, отличные от вашей подписки по умолчанию. toosee все подписки и идентификаторов, используйте:

  ```azurecli
  az account list
  ```

3. Hello развертывания может занять несколько минут toocomplete. По завершении появится сообщение следующего вида.

  ```azurecli
  "provisioningState": "Succeeded",
  ```

4. toosee, учетной записи группы и хранения ресурсов, которые были развернуты tooyour подписки, используйте:

  ```azurecli
  az group show --name ExampleGroup
  az resource list --resource-group ExampleGroup
  ```

5. Параметры шаблона можно указать в качестве параметров PowerShell при развертывании шаблона. Hello предыдущий пример не включали никакие параметры шаблона, поэтому используются значения по умолчанию hello в шаблоне hello. toodeploy еще одно хранилище учетную запись, а также указать значения параметров для hello префикс имени хранилища и учетной записи хранилища hello SKU, используйте:

  ```azurecli
  az group deployment create --name ExampleDeployment2 --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json --parameters '{"storageNamePrefix":{"value":"contoso"},"storageSKU":{"value":"Standard_GRS"}}'
  ```

  Теперь в группе ресурсов две учетные записи хранения. 

## <a name="example-storage-template"></a>Пример шаблона хранилища

Используйте следующий пример шаблона toodeploy подписки tooyour учетной записи хранилища hello.

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

## <a name="next-steps"></a>Дальнейшие действия

* Подробные сведения об использовании шаблонов toodeploy PowerShell см. в разделе [развертывания ресурсов с помощью шаблонов диспетчера ресурсов и Azure PowerShell](/azure/azure-resource-manager/resource-group-template-deploy).
* Подробные сведения об использовании шаблонов toodeploy Azure CLI. в разделе [развертывания ресурсов с помощью шаблонов диспетчера ресурсов и Azure CLI](/azure/azure-resource-manager/resource-group-template-deploy-cli).



