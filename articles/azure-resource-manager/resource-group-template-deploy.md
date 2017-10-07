---
title: "aaaDeploy ресурсы с помощью PowerShell и шаблона | Документы Microsoft"
description: "С помощью диспетчера ресурсов Azure и Azure PowerShell toodeploy tooAzure ресурсов. Hello ресурсы определяются в шаблоне диспетчера ресурсов."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 55903f35-6c16-4c6d-bf52-dbf365605c3f
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 41506811ba3c2ea5df6313db70978ade50f71161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-powershell"></a>Развертывание ресурсов с использованием шаблонов Resource Manager и Azure PowerShell

В этом разделе объясняется, как toouse Azure PowerShell с toodeploy шаблонов диспетчера ресурсов вашей tooAzure ресурсов. Если вы не знакомы с основными понятиями hello развертывания и управлению решения Azure см [Обзор диспетчера ресурсов Azure](resource-group-overview.md).

шаблон диспетчера ресурсов Hello развертывание может быть локальный файл на компьютере или внешнем файле, расположенном в репозитория GitHub. шаблон Hello развертывания в этой статье доступен в hello [образец шаблона](#sample-template) раздел, или как [шаблона учетной записи хранилища в GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).

[!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install.md)]

<a id="deploy-local-template" />

## <a name="deploy-a-template-from-your-local-machine"></a>Развертывание шаблона с локального компьютера

При развертывании tooAzure ресурсы можно:

1. Войдите в tooyour учетная запись Azure
2. Создание группы ресурсов, выступающее в роли контейнера hello hello развертывания ресурсов. Имя группы ресурсов hello Hello может содержать только буквенно-цифровые символы, точки, символы подчеркивания, дефисы и скобки. Возможность ее too90 символов. не может заканчиваться точкой.
3. Развертывание toohello группы ресурсов hello шаблона, определяющий ресурсы toocreate hello

Шаблон может включать параметры, позволяющие toocustomize hello развертывания. Например, вы можете предоставить значения, предназначенные для конкретной среды (такой как среда разработки, тестирования и рабочая среда). Образец Hello шаблона определяет параметр для учетной записи хранения hello SKU.

Следующий пример Hello создает группу ресурсов и развертывает шаблона с локального компьютера:

```powershell
Login-AzureRmAccount
 
New-AzureRmResourceGroup -Name ExampleResourceGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

Hello развертывания может занять несколько минут toocomplete. По завершении появится сообщение, содержащее результат hello:

```powershell
ProvisioningState       : Succeeded
```

## <a name="deploy-a-template-from-an-external-source"></a>Развертывание шаблона из внешнего источника

Вместо сохранения шаблонов диспетчера ресурсов на локальном компьютере, то лучше toostore их во внешнем местоположении. Вы можете хранить шаблоны в репозитории системы управления версиями (например, GitHub). А также их можно хранить в учетной записи хранения Azure для общего доступа в организации.

использовать toodeploy шаблоном внешних hello **TemplateUri** параметра. Используйте hello URI в шаблоне образец hello toodeploy пример hello из GitHub.

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -storageAccountType Standard_GRS
```

Hello предыдущего примера требуется общедоступный код URI hello шаблона, который работает в большинстве случаев, поскольку шаблон не следует включать конфиденциальные данные. Если вам требуется toospecify конфиденциальные данные (например, пароль администратора), можно передайте в качестве безопасного параметра. Тем не менее если не требуется toobe ваш шаблон доступен из Интернета, можно защитить его путем сохранения его в контейнер закрытого хранения. Сведения о развертывании шаблона, требующего маркер подписанного URL-адреса (SAS), см. в статье [Развертывание частного шаблона Resource Manager с использованием токена SAS и Azure PowerShell](resource-manager-powershell-sas-token.md).

## <a name="parameter-files"></a>Файлы параметров

Вместо передачи параметров в качестве встроенных значений в скрипте, может оказаться проще toouse JSON-файл, содержащий значения параметров hello. файл параметров Hello должны быть hello следующий формат:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
     "storageAccountType": {
         "value": "Standard_GRS"
     }
  }
}
```

Обратите внимание, что раздел параметров hello содержит имя параметра, которое соответствует hello параметра, определенного в шаблоне (storageAccountType). файл параметров Hello содержит значение параметра hello. Это значение автоматически передается toohello шаблона во время развертывания. Можно создать несколько файлов параметров для различных сценариев развертывания и затем передайте файл hello соответствующий параметр. 

Скопируйте предшествующий пример hello и сохраните его как файл с именем `storage.parameters.json`.

использовать файл локального параметра toopass hello **TemplateParameterFile** параметр:

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json `
  -TemplateParameterFile c:\MyTemplates\storage.parameters.json
```

toopass файл внешнего параметра использовать hello **TemplateParameterUri** параметр:

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.parameters.json
```

Можно использовать встроенные параметры и локального параметра файлов в hello же операции развертывания. Например можно указать некоторые значения в файле локального параметра hello и добавить другие встроенные значения во время развертывания. При указании значения для параметра в файл локального параметра hello и встроенные hello встроенного значение имеет приоритет.

Тем не менее при использовании внешнего файла параметров нельзя передавать другие значения в командной строке или локальном файле. При указании файла параметров в hello **TemplateParameterUri** параметр, все встроенные параметры игнорируются. Укажите все значения параметров в файле внешних hello. Если шаблон включает конфиденциальное значение, нельзя включать в файл параметров hello, добавьте хранилище ключей, значение tooa или динамически предоставляют встроенные значения параметра.

Если шаблон включает параметр с hello точно такое же имя в качестве одного из параметров hello в hello команду PowerShell, PowerShell представляет параметр hello из шаблона с постфиксной hello **FromTemplate**. Например, параметр с именем **ResourceGroupName** на шаблон конфликтует с hello **ResourceGroupName** параметр в hello [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment)командлета. Запрос tooprovide являются значение для **ResourceGroupNameFromTemplate**. В общем случае следует избегать этой путаницы, не присвоив имена параметров с hello точно такое же имя в качестве параметров, используемых для операций развертывания.

## <a name="test-a-template-deployment"></a>Тестовое развертывание шаблона

использовать ваш шаблон и значения параметров без фактического развертывания все ресурсы, tootest [AzureRmResourceGroupDeployment теста](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment). 

```powershell
Test-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

Если ошибки не обнаружены, завершения выполнения команды hello без ответа. Если обнаруживается ошибка, hello команда возвращает сообщение об ошибке. Например toopass неправильное значение для учетной записи хранения hello SKU, система выдаст hello следующая ошибка:

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName testgroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType badSku

Code    : InvalidTemplate
Message : Deployment template validation failed: 'hello provided value 'badSku' for hello template parameter 'storageAccountType'
          at line '15' and column '24' is not valid. hello parameter value is not part of hello allowed value(s):
          'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.
Details :
```

Если шаблон содержит синтаксическую ошибку, команда hello возвращает ошибку, указывающую, что не удалось проанализировать шаблон hello. сообщение Hello указывает hello номер строки и положение hello Ошибка синтаксического анализа.

```powershell
Test-AzureRmResourceGroupDeployment : After parsing a value an unexpected character was encountered: 
  ". Path 'variables', line 31, position 3.
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

полный режим toouse, используйте hello `Mode` параметр:

```powershell
New-AzureRmResourceGroupDeployment -Mode Complete -Name ExampleDeployment `
  -ResourceGroupName ExampleResourceGroup -TemplateFile c:\MyTemplates\storage.json 
```

## <a name="sample-template"></a>Пример шаблона

Hello следующий шаблон используется для hello примеры в этом разделе. Скопируйте и сохраните его как файл с именем storage.json. toounderstand как toocreate этого шаблона, в разделе [создать свой первый диспетчера ресурсов Azure](resource-manager-create-first-template.md).  

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

## <a name="next-steps"></a>Дальнейшие действия
* Примеры Hello в этой статье развертывания группы ресурсов tooa ресурсы в подписке по умолчанию. toouse другую подписку, в разделе [управления несколькими подписками Azure](/powershell/azure/manage-subscriptions-azureps).
* Полный пример сценария, развертывающего шаблон, см. в статье [Сценарий для развертывания шаблона Resource Manager](resource-manager-samples-powershell-deploy.md).
* toodefine параметры в шаблоне, в статье toounderstand [понять структуру hello и синтаксис шаблоны Azure Resource Manager](resource-group-authoring-templates.md).
* Советы по устранению распространенных ошибок развертывания см. в разделе [Устранение распространенных ошибок развертывания в Azure с помощью Azure Resource Manager](resource-manager-common-deployment-errors.md).
* Сведения о развертывании шаблона, которому нужен токен SAS, см. в статье [Развертывание частного шаблона с помощью маркера SAS](resource-manager-powershell-sas-token.md).
* Для получения рекомендаций по как предприятия могут использовать диспетчер ресурсов tooeffectively управление подписками см. в разделе [корпоративные функции формирования шаблонов - управление конкретные подписки](resource-manager-subscription-governance.md).

