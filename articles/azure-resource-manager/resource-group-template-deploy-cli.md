---
title: "aaaDeploy ресурсами с помощью Azure CLI и шаблона | Документы Microsoft"
description: "С помощью диспетчера ресурсов Azure и Azure CLI toodeploy tooAzure ресурсов. Hello ресурсы определяются в шаблоне диспетчера ресурсов."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 493b7932-8d1e-4499-912c-26098282ec95
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/31/2017
ms.author: tomfitz
ms.openlocfilehash: 9f8bb9a8720399390a407030d2d32bcd97d32f13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-cli"></a>Развертывание ресурсов с использованием шаблонов Resource Manager и Azure CLI

В этом разделе объясняется, как toouse Azure CLI 2.0 с toodeploy шаблонов диспетчера ресурсов вашей tooAzure ресурсов. Если вы не знакомы с основными понятиями hello развертывания и управлению решения Azure см [Обзор диспетчера ресурсов Azure](resource-group-overview.md).  

шаблон диспетчера ресурсов Hello развертывание может быть локальный файл на компьютере или внешнем файле, расположенном в репозитория GitHub. шаблон Hello развертывания в этой статье доступен в hello [образец шаблона](#sample-template) раздел, или как [шаблона учетной записи хранилища в GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).

[!INCLUDE [sample-cli-install](../../includes/sample-cli-install.md)]

Если у вас установлен Azure CLI, можно использовать hello [оболочки облака](#deploy-template-from-cloud-shell).

## <a name="deploy-local-template"></a>Развертывание локального шаблона

При развертывании tooAzure ресурсы можно:

1. Войдите в tooyour учетная запись Azure
2. Создание группы ресурсов, выступающее в роли контейнера hello hello развертывания ресурсов. Имя группы ресурсов hello Hello может содержать только буквенно-цифровые символы, точки, символы подчеркивания, дефисы и скобки. Возможность ее too90 символов. не может заканчиваться точкой.
3. Развертывание toohello группы ресурсов hello шаблона, определяющий ресурсы toocreate hello

Шаблон может включать параметры, позволяющие toocustomize hello развертывания. Например, вы можете предоставить значения, предназначенные для конкретной среды (такой как среда разработки, тестирования и рабочая среда). Образец Hello шаблона определяет параметр для учетной записи хранения hello SKU. 

Следующий пример Hello создает группу ресурсов и развертывает шаблона с локального компьютера:

```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
```

Hello развертывания может занять несколько минут toocomplete. По завершении появится сообщение, содержащее результат hello:

```azurecli
"provisioningState": "Succeeded",
```

## <a name="deploy-external-template"></a>Развертывание внешнего шаблона

Вместо сохранения шаблонов диспетчера ресурсов на локальном компьютере, то лучше toostore их во внешнем местоположении. Вы можете хранить шаблоны в репозитории системы управления версиями (например, GitHub). А также их можно хранить в учетной записи хранения Azure для общего доступа в организации.

использовать toodeploy шаблоном внешних hello **шаблон uri** параметра. Используйте hello URI в шаблоне образец hello toodeploy пример hello из GitHub.
   
```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
    --parameters storageAccountType=Standard_GRS
```

Hello предыдущего примера требуется общедоступный код URI hello шаблона, который работает в большинстве случаев, поскольку шаблон не следует включать конфиденциальные данные. Если вам требуется toospecify конфиденциальные данные (например, пароль администратора), можно передайте в качестве безопасного параметра. Тем не менее если не требуется toobe ваш шаблон доступен из Интернета, можно защитить его путем сохранения его в контейнер закрытого хранения. Сведения о развертывании шаблона, требующего маркер подписанного URL-адреса (SAS), см. в статье [Развертывание частного шаблона Resource Manager с использованием токена SAS и Azure PowerShell](resource-manager-cli-sas-token.md).

## <a name="deploy-template-from-cloud-shell"></a>Развертывание шаблона из Cloud Shell

Можно использовать [оболочки облака](../cloud-shell/overview.md) toorun hello Azure CLI команды для развертывания шаблона. Тем не менее необходимо сначала загрузить шаблон в общей папке hello для вашей облачной среды. Если вы еще не использовали Cloud Shell, ознакомьтесь со статьей [Обзор Azure Cloud Shell (предварительная версия)](../cloud-shell/overview.md), чтобы узнать о настройке службы.

1. Войдите в toohello [портал Azure](https://portal.azure.com).   

2. Выберите свою группу ресурсов Cloud Shell. шаблон имени Hello `cloud-shell-storage-<region>`.

   ![Выбор группы ресурсов](./media/resource-group-template-deploy-cli/select-cs-resource-group.png)

3. Выберите учетную запись хранения hello для вашей облачной среды.

   ![Выбор учетной записи хранения](./media/resource-group-template-deploy-cli/select-storage.png)

4. Выберите **Файлы**.

   ![Выбор файлов](./media/resource-group-template-deploy-cli/select-files.png)

5. Выберите общую папку hello для облака оболочки. шаблон имени Hello `cs-<user>-<domain>-com-<uniqueGuid>`.

   ![Выбор общего файлового ресурса](./media/resource-group-template-deploy-cli/select-file-share.png)

6. Выберите **Добавить каталог**.

   ![Добавление каталога](./media/resource-group-template-deploy-cli/select-add-directory.png)

7. Назовите его **templates** и нажмите кнопку **ОК**.

   ![Присвоение имени каталогу](./media/resource-group-template-deploy-cli/name-templates.png)

8. Выберите новый каталог.

   ![Выбор каталога](./media/resource-group-template-deploy-cli/select-templates.png)

9. Щелкните **Отправить**.

   ![Кнопка "Отправить"](./media/resource-group-template-deploy-cli/select-upload.png)

10. Найдите и отправьте свой шаблон.

   ![Отправка файла](./media/resource-group-template-deploy-cli/upload-files.png)

11. Откройте hello строки.

   ![Открытие Cloud Shell](./media/resource-group-template-deploy-cli/start-cloud-shell.png)

12. Введите следующие команды в hello оболочки облака hello:

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageAccountType=Standard_GRS
   ```

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

использовать файл локального параметра toopass `@` toospecify локальный файл с именем storage.parameters.json.

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

## <a name="test-a-template-deployment"></a>Тестовое развертывание шаблона

использовать ваш шаблон и значения параметров без фактического развертывания все ресурсы, tootest [проверить развертывание группы az](/cli/azure/group/deployment#validate). 

```azurecli
az group deployment validate \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

Если ошибки не обнаружены, hello команда возвращает сведения о развертывании тестов hello. В частности, обратите внимание, что hello **ошибка** имеет значение null.

```azurecli
{
  "error": null,
  "properties": {
      ...
```

Если обнаруживается ошибка, hello команда возвращает сообщение об ошибке. Например toopass неправильное значение для учетной записи хранения hello SKU, система выдаст hello следующая ошибка:

```azurecli
{
  "error": {
    "code": "InvalidTemplate",
    "details": null,
    "message": "Deployment template validation failed: 'hello provided value 'badSKU' for hello template parameter 
      'storageAccountType' at line '13' and column '20' is not valid. hello parameter value is not part of hello allowed 
      value(s): 'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.",
    "target": null
  },
  "properties": null
}
```

Если шаблон содержит синтаксическую ошибку, команда hello возвращает ошибку, указывающую, что не удалось проанализировать шаблон hello. сообщение Hello указывает hello номер строки и положение hello Ошибка синтаксического анализа.

```azurecli
{
  "error": {
    "code": "InvalidTemplate",
    "details": null,
    "message": "Deployment template parse failed: 'After parsing a value an unexpected character was encountered:
      \". Path 'variables', line 31, position 3.'.",
    "target": null
  },
  "properties": null
}
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

полный режим toouse, используйте hello `mode` параметр:

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --mode Complete \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
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
* Примеры Hello в этой статье развертывания группы ресурсов tooa ресурсы в подписке по умолчанию. toouse другую подписку, в разделе [управления несколькими подписками Azure](/cli/azure/manage-azure-subscriptions-azure-cli).
* Полный пример сценария, развертывающего шаблон, см. в статье [Сценарий для развертывания шаблона Resource Manager](resource-manager-samples-cli-deploy.md).
* toodefine параметры в шаблоне, в статье toounderstand [понять структуру hello и синтаксис шаблоны Azure Resource Manager](resource-group-authoring-templates.md).
* Советы по устранению распространенных ошибок развертывания см. в разделе [Устранение распространенных ошибок развертывания в Azure с помощью Azure Resource Manager](resource-manager-common-deployment-errors.md).
* Сведения о развертывании шаблона, которому нужен токен SAS, см. в статье [Развертывание частного шаблона с помощью маркера SAS](resource-manager-cli-sas-token.md).
* Для получения рекомендаций по как предприятия могут использовать диспетчер ресурсов tooeffectively управление подписками см. в разделе [корпоративные функции формирования шаблонов - управление конкретные подписки](resource-manager-subscription-governance.md).
