---
title: "aaaDeploy рабочей области машинного обучения с помощью диспетчера ресурсов Azure | Документы Microsoft"
description: "Как toodeploy в рабочую область для машинного обучения Azure с помощью шаблона диспетчера ресурсов Azure"
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
ms.openlocfilehash: 308959825bcbd670f6ce9b6dc381be767f172357
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-machine-learning-workspace-using-azure-resource-manager"></a>Развертывание рабочей области машинного обучения с помощью Azure Resource Manager
## <a name="introduction"></a>Введение
С помощью диспетчера ресурсов Azure, в шаблон развертывания вы можете сэкономить время, предоставляя toodeploy масштабируемый способ между собой компонентов механизм, с помощью проверки и повторите попытку. tooset копирование рабочие области машинного обучения Azure, например, требуется toofirst настроить учетную запись хранения Azure, а затем развернуть рабочую область. Представьте себе выполнение этого задания вручную для сотен рабочих областей. Альтернативой проще является toouse toodeploy шаблона диспетчера ресурсов Azure рабочую область Azure машинного обучения и все его зависимости. В этой статье представлено пошаговое выполнение этого процесса. Подробный обзор Azure Resource Manager см. в статье [Общие сведения об Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).

## <a name="step-by-step-create-a-machine-learning-workspace"></a>Пошаговое создание рабочей области машинного обучения
Сначала мы создадим группу ресурсов Azure, а затем развернем новую учетную запись хранения Azure и рабочую область машинного обучения Azure с помощью шаблона Resource Manager. После завершения развертывания hello, мы напечатает важные сведения о hello рабочих областей, которые были созданы (первичный ключ hello hello ИД рабочей области и рабочей toohello hello URL-адрес).

### <a name="create-an-azure-resource-manager-template"></a>Создание шаблона Azure Resource Manager
Рабочую область машинного обучения требует хранилища Azure tooit учетной записи toostore hello связанного набора данных.
Hello следующий шаблон использует имя hello hello toogenerate группы ресурсов hello имя учетной записи хранилища и имя рабочей области hello.  Она также использует имя учетной записи хранения hello как свойство при создании рабочей hello.

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
Сохраните этот шаблон как файл mlworkspace.json в папке C:\temp\.

### <a name="deploy-hello-resource-group-based-on-hello-template"></a>Развертывание группы ресурсов hello, основанных на шаблоне hello
* Откройте PowerShell.
* Установите модули для Azure Resource Manager и управления службами Azure.  

```
# Install hello Azure Resource Manager modules from hello PowerShell Gallery (press “A”)
Install-Module AzureRM -Scope CurrentUser

# Install hello Azure Service Management modules from hello PowerShell Gallery (press “A”)
Install-Module Azure -Scope CurrentUser
```

   Эти действия, загрузите и установите hello модули необходимые toocomplete hello оставшиеся шаги. Это достаточно выполнить один раз в среде hello, где выполняются команды PowerShell hello toobe.   

* Проверка подлинности tooAzure  

```
# Authenticate (enter your credentials in hello pop-up window)
Add-AzureRmAccount
```
Этот шаг должен toobe повторяется для каждого сеанса. После выполнения проверки подлинности должны отображаться сведения о подписке.

![Учетная запись Azure][1]

Теперь, когда у нас есть tooAzure доступ, можно создать группу ресурсов hello.

* Создание группы ресурсов

```
$rg = New-AzureRmResourceGroup -Name "uniquenamerequired523" -Location "South Central US"
$rg
```

Убедитесь, что задокументирована надлежащим образом, что группа ресурсов "hello". **ProvisioningState** должно отображаться состояние Succeeded.
Имя учетной записи хранилища hello toogenerate hello шаблона используется имя группы ресурсов Hello. Имя учетной записи хранения Hello должно быть от 3 до 24 символов и содержать только строчные буквы и цифры.

![Группа ресурсов][2]

* Развертывание группы ресурсов hello, внедрить новые рабочую область машинного обучения.

```
# Create a Resource Group, TemplateFile is hello location of hello JSON template.
$rgd = New-AzureRmResourceGroupDeployment -Name "demo" -TemplateFile "C:\temp\mlworkspace.json" -ResourceGroupName $rg.ResourceGroupName
```

После завершения развертывания hello, это просто tooaccess свойства hello рабочую область, которую вы развернули. Например можно получить доступ к hello токена первичного ключа.

```
# Access Azure ML Workspace Token after its deployment.
$rgd.Outputs.mlWorkspaceToken.Value
```

Другой способ tooretrieve маркеры существующую рабочую область — hello toouse команда Invoke-AzureRmResourceAction. Например можно перечислить hello первичного и вторичного маркеры всех рабочих областей.

```  
# List hello primary and secondary tokens of all workspaces
Get-AzureRmResource |? { $_.ResourceType -Like "*MachineLearning/workspaces*"} |% { Invoke-AzureRmResourceAction -ResourceId $_.ResourceId -Action listworkspacekeys -Force}  
```
После подготовки рабочей hello также можно автоматизировать многие задачи студии машинного обучения Azure с помощью hello [модуль PowerShell для машинного обучения Azure](http://aka.ms/amlps).

## <a name="next-steps"></a>Дальнейшие действия
* Узнайте больше о [создании шаблонов Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md). 
* Рассмотрим hello [репозиторий шаблоны быстрый запуск Azure](https://github.com/Azure/azure-quickstart-templates). 
* Просмотрите видео об [Azure Resource Manager](https://channel9.msdn.com/Events/Ignite/2015/C9-39). 

<!--Image references-->
[1]: ../media/machine-learning-deploy-with-resource-manager-template/azuresubscription.png
[2]: ../media/machine-learning-deploy-with-resource-manager-template/resourcegroupprovisioning.png


<!--Link references-->
