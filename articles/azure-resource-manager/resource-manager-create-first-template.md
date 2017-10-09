---
title: "Первый шаблон диспетчера ресурсов Azure aaaCreate | Документы Microsoft"
description: "Пошаговое руководство по toocreating первый шаблон диспетчера ресурсов Azure. Он показывает, как toouse hello ссылка на шаблон для шаблона hello toocreate учетной записи хранилища."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 07/27/2017
ms.topic: get-started-article
ms.author: tomfitz
ms.openlocfilehash: 92e6d6bb7094fe0e4537ee080704967862804bdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-your-first-azure-resource-manager-template"></a>Создание и развертывание первого шаблона Azure Resource Manager
Этот раздел поможет выполнить этапы создания вашего первого шаблона Azure Resource Manager hello. Шаблоны диспетчера ресурсов являются JSON-файлов, которые определяют ресурсы hello нужна toodeploy в решении. hello toounderstand основные понятия, связанные с развертыванием и управлением решений Azure, в разделе [Обзор диспетчера ресурсов Azure](resource-group-overview.md). Если вы используете существующие ресурсы и требуется tooget шаблона для этих ресурсов, см. раздел [Экспорт шаблона диспетчера ресурсов Azure с существующие ресурсы](resource-manager-export-template.md).

шаблоны toocreate и проверьте, требуется редактор JSON. например [Visual Studio Code](https://code.visualstudio.com/). Это упрощенный кроссплатформенный редактор с открытым исходным кодом. Для создания шаблонов Resource Manager мы настоятельно рекомендуем использовать Visual Studio Code. В этой статье предполагается, что вы используете VS Code. Но вы можете использовать и другой редактор JSON (например, Visual Studio).

## <a name="prerequisites"></a>Предварительные требования

* Visual Studio Code. При необходимости установите его со страницы [https://code.visualstudio.com/](https://code.visualstudio.com/).
* Подписка Azure. Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.

## <a name="create-template"></a>Создание шаблона

Давайте начнем с простой шаблон, который развертывает подписки tooyour учетной записи хранилища.

1. Выберите **Файл** > **Создать файл**. 

   ![Создание файла](./media/resource-manager-create-first-template/new-file.png)

2. Скопируйте и вставьте следующий синтаксис JSON в свой файл hello:

   ```json
   {
     "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
     "contentVersion": "1.0.0.0",
     "parameters": {
     },
     "variables": {
     },
     "resources": [
       {
         "name": "[concat('storage', uniqueString(resourceGroup().id))]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "sku": {
           "name": "Standard_LRS"
         },
         "kind": "Storage",
         "location": "South Central US",
         "tags": {},
         "properties": {}
       }
     ],
     "outputs": {  }
   }
   ```

   Имена учетной записи хранения имеет несколько ограничений, которые делают их трудно tooset. Hello имя должно быть в диапазоне от 3 до 24 символов в длину, используйте только цифры и строчные буквы и быть уникальными. Hello предыдущий шаблон использует hello [uniqueString](resource-group-template-functions-string.md#uniquestring) функции toogenerate хэш-значения. toogive этот хэш-значения в нескольких то есть, он добавляет префикс hello *хранения*. 

3. Сохраните этот файл как **azuredeploy.json** tooa локальную папку.

   ![Сохранение шаблона](./media/resource-manager-create-first-template/save-template.png)

## <a name="deploy-template"></a>Развертывание шаблона

Вам будут готовы toodeploy этот шаблон. Можно использовать PowerShell или Azure CLI toocreate группу ресурсов. Разверните группу ресурсов toothat учетной записи хранилища.

* Для PowerShell используйте следующие команды из hello папку, содержащую шаблон hello hello:

   ```powershell
   Login-AzureRmAccount
   
   New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
   New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json
   ```

* Для локальной установки Azure CLI используйте следующие команды из hello папку, содержащую шаблон hello hello.

   ```azurecli
   az login

   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file azuredeploy.json
   ```

После завершения развертывания в группе ресурсов hello существует вашей учетной записи хранилища.

## <a name="deploy-template-from-cloud-shell"></a>Развертывание шаблона из Cloud Shell

Можно использовать [оболочки облака](../cloud-shell/overview.md) toorun hello Azure CLI команды для развертывания шаблона. Тем не менее необходимо сначала загрузить шаблон в общей папке hello для вашей облачной среды. Если вы еще не использовали Cloud Shell, ознакомьтесь со статьей [Обзор Azure Cloud Shell (предварительная версия)](../cloud-shell/overview.md), чтобы узнать о настройке службы.

1. Войдите в toohello [портал Azure](https://portal.azure.com).   

2. Выберите свою группу ресурсов Cloud Shell. шаблон имени Hello `cloud-shell-storage-<region>`.

   ![Выбор группы ресурсов](./media/resource-manager-create-first-template/select-cs-resource-group.png)

3. Выберите учетную запись хранения hello для вашей облачной среды.

   ![Выбор учетной записи хранения](./media/resource-manager-create-first-template/select-storage.png)

4. Выберите **Файлы**.

   ![Выбор файлов](./media/resource-manager-create-first-template/select-files.png)

5. Выберите общую папку hello для облака оболочки. шаблон имени Hello `cs-<user>-<domain>-com-<uniqueGuid>`.

   ![Выбор общего файлового ресурса](./media/resource-manager-create-first-template/select-file-share.png)

6. Выберите **Добавить каталог**.

   ![Добавление каталога](./media/resource-manager-create-first-template/select-add-directory.png)

7. Назовите его **templates** и нажмите кнопку **ОК**.

   ![Присвоение имени каталогу](./media/resource-manager-create-first-template/name-templates.png)

8. Выберите новый каталог.

   ![Выбор каталога](./media/resource-manager-create-first-template/select-templates.png)

9. Щелкните **Отправить**.

   ![Кнопка "Отправить"](./media/resource-manager-create-first-template/select-upload.png)

10. Найдите и отправьте свой шаблон.

   ![Отправка файла](./media/resource-manager-create-first-template/upload-files.png)

11. Откройте hello строки.

   ![Открытие Cloud Shell](./media/resource-manager-create-first-template/start-cloud-shell.png)

12. Введите следующие команды в hello оболочки облака hello:

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json
   ```

После завершения развертывания в группе ресурсов hello существует вашей учетной записи хранилища.

## <a name="customize-hello-template"></a>Настройка шаблона hello

шаблон Hello работает отлично, но не обладает гибкостью. Он всегда развертывает локально избыточное хранилище tooSouth центральной части США. Имя Hello всегда является *хранения* следуют хэш-значения. с помощью шаблона hello для различных сценариев tooenable добавить шаблон toohello параметров.

Hello пример hello раздела параметров с двумя параметрами. Здравствуйте, первый параметр `storageSKU` позволяет типа hello toospecify избыточности. Этот параметр ограничивает число hello значения, которые можно передать в toovalues, которые являются допустимыми для учетной записи хранилища. Он также задает значение по умолчанию. Здравствуйте, второй параметр `storageNamePrefix` является набор tooallow до 11 символов. Он задает значение по умолчанию.

```json
"parameters": {
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
  },
  "storageNamePrefix": {
    "type": "string",
    "maxLength": 11,
    "defaultValue": "storage",
    "metadata": {
      "description": "hello value toouse for starting hello storage account name. Use only lowercase letters and numbers."
    }
  }
},
```

В разделе "переменные" hello, добавьте переменную с именем `storageName`. Он объединяет значение префикса hello из параметров hello и хэш-код от hello [uniqueString](resource-group-template-functions-string.md#uniquestring) функции. Она использует hello [toLower](resource-group-template-functions-string.md#tolower) функции tooconvert toolowercase все символы.

```json
"variables": {
  "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
},
```

toouse эти новые значения для вашей учетной записи, измените определение ресурса hello:

```json
"resources": [
  {
    "name": "[variables('storageName')]",
    "type": "Microsoft.Storage/storageAccounts",
    "apiVersion": "2016-01-01",
    "sku": {
      "name": "[parameters('storageSKU')]"
    },
    "kind": "Storage",
    "location": "[resourceGroup().location]",
    "tags": {},
    "properties": {}
  }
],
```

Обратите внимание, что hello теперь задано имя учетной записи хранения hello toohello переменной, которая была добавлена. Имя SKU Hello задано toohello значение параметра hello. Задайте расположение Hello hello местоположения hello группы ресурсов.

Сохраните файл. 

После завершения шагов hello в этой статье, ваш шаблон теперь выглядит следующим образом.

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
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
    },   
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "hello value toouse for starting hello storage account name. Use only lowercase letters and numbers."
      }
    }
  },
  "variables": {
    "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
  },
  "resources": [
    {
      "name": "[variables('storageName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-01-01",
      "sku": {
        "name": "[parameters('storageSKU')]"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {}
    }
  ],
  "outputs": {  }
}
```

## <a name="redeploy-template"></a>Повторное развертывание шаблона

Повторное развертывание шаблона hello с разными значениями.

Для PowerShell используйте команду:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json -storageNamePrefix newstore -storageSKU Standard_RAGRS
```

Для интерфейса командной строки Azure:

```azurecli
az group deployment create --resource-group examplegroup --template-file azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

Для hello оболочки облака необходимо отправьте измененный шаблон toohello файлового ресурса. Перезаписать существующий файл hello. Затем с помощью hello следующую команду:

```azurecli
az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

## <a name="clean-up-resources"></a>Очистка ресурсов

Если больше не нужен, удалите ресурсы hello развернутые путем удаления группы ресурсов hello.

Для PowerShell используйте команду:

```powershell
Remove-AzureRmResourceGroup -Name examplegroup
```

Для интерфейса командной строки Azure:

```azurecli
az group delete --name examplegroup
```

## <a name="next-steps"></a>Дальнейшие действия
* toolearn Дополнительные сведения о структуре hello шаблона, в разделе [шаблоны разработки Azure Resource Manager](resource-group-authoring-templates.md).
* toolearn о свойствах hello для учетной записи хранения в разделе [ссылка на шаблон учетных записей хранения](/azure/templates/microsoft.storage/storageaccounts).
* tooview завершения шаблоны для различных типов решений, см. hello [шаблоны быстрый запуск Azure](https://azure.microsoft.com/documentation/templates/).
