---
title: "ресурсы Azure Service Bus aaaCreate с помощью шаблонов диспетчера ресурсов Azure | Документы Microsoft"
description: "Использование диспетчера ресурсов Azure tooautomate шаблоны hello Создание ресурсов служебной шины"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 24f6a207-0fa4-49cf-8a58-963f9e2fd655
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: e539902cae307b63ae7c332580e2064761331ec5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-service-bus-resources-using-azure-resource-manager-templates"></a>Создание ресурсов служебной шины с использованием шаблонов Azure Resource Manager

В этой статье описывается как toocreate и развертывания ресурсов служебной шины с помощью шаблонов диспетчера ресурсов Azure, PowerShell и hello поставщика ресурсов служебной шины.

Шаблоны Azure Resource Manager помогает определять hello toodeploy ресурсы для решения и toospecify параметры и переменные, которые позволяют tooinput значения для различных сред. шаблон Hello состоит из выражения, что tooconstruct значения можно использовать для развертывания и JSON. Подробные сведения о создании шаблонов диспетчера ресурсов Azure и обсуждение формата шаблона hello. в разделе [структуре и синтаксисе шаблонов диспетчера ресурсов Azure](../azure-resource-manager/resource-group-authoring-templates.md).

> [!NOTE]
> Здравствуйте, примеры в этой статье показано, как toouse Azure Resource Manager toocreate пространство имен служебной шины и обмена сообщениями (очередь) сущности. Другие примеры шаблона посетите hello [коллекции шаблонов быстрый запуск Azure] [ Azure Quickstart Templates gallery] и выполните поиск «Шина обслуживания».
>
>

## <a name="service-bus-resource-manager-templates"></a>Шаблоны Resource Manager для служебной шины

Эти шаблоны Azure Resource Manager для служебной шины доступны для скачивания и развертывания. Щелкните hello ссылкам подробные сведения о каждой из них с помощью шаблонов toohello ссылки на GitHub:

* [Создайте пространство имен служебной шины](service-bus-resource-manager-namespace.md)
* [Создание пространства имен служебной шины с очередью](service-bus-resource-manager-namespace-queue.md)
* [Создание пространства имен служебной шины с разделом и подпиской](service-bus-resource-manager-namespace-topic.md)
* [Создание пространства имен служебной шины с очередью и правилом авторизации](service-bus-resource-manager-namespace-auth-rule.md)
* [Создание пространства имен служебной шины с разделом, подпиской и правилом с помощью шаблона Azure Resource Manager](service-bus-resource-manager-namespace-topic-with-rule.md)

## <a name="deploy-with-powershell"></a>Развертывание с помощью PowerShell

Hello ниже описано, как toodeploy PowerShell toouse шаблона диспетчера ресурсов Azure, создает **Стандартная** уровня пространства имен шины обслуживания и очереди в этом пространстве имен. Этот пример основан на hello [создание пространства имен Service Bus с очередью](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue) шаблона. Приблизительное Hello рабочий процесс выглядит следующим образом:

1. Установите PowerShell.
2. Создание шаблона hello и (необязательно) файл параметров.
3. В PowerShell войдите в tooyour учетная запись Azure.
4. Создайте группу ресурсов, если ее еще нет.
5. Тестирование развертывания hello.
6. При желании установите режим развертывания hello.
7. Развертывание шаблона hello.

Подробные сведения о развертывании шаблонов Azure Resource Manager см. в статье [Deploy resources with Resource Manager templates and Azure PowerShell][Deploy resources with Azure Resource Manager templates] (Развертывание ресурсов с использованием шаблонов Resource Manager и Azure PowerShell).

### <a name="install-powershell"></a>Установка PowerShell

Установите Azure PowerShell, следуя инструкциям hello [Приступая к работе с Azure PowerShell](/powershell/azure/get-started-azureps).

### <a name="create-a-template"></a>Создание шаблона

Клон или копирования hello [201-servicebus создать очередь](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) шаблона из GitHub:

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "type": "string",
            "metadata": {
                "description": "Name of hello Service Bus namespace"
            }
        },
        "serviceBusQueueName": {
            "type": "string",
            "metadata": {
                "description": "Name of hello Queue"
            }
        },
        "serviceBusApiVersion": {
            "type": "string",
            "defaultValue": "2015-08-01",
            "metadata": {
                "description": "Service Bus ApiVersion used by hello template"
            }
        }
    },
    "variables": {
        "location": "[resourceGroup().location]",
        "sbVersion": "[parameters('serviceBusApiVersion')]",
        "defaultSASKeyName": "RootManageSharedAccessKey",
        "authRuleResourceId": "[resourceId('Microsoft.ServiceBus/namespaces/authorizationRules', parameters('serviceBusNamespaceName'), variables('defaultSASKeyName'))]"
    },
    "resources": [{
        "apiVersion": "[variables('sbVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "kind": "Messaging",
        "sku": {
            "name": "StandardSku",
            "tier": "Standard"
        },
        "resources": [{
            "apiVersion": "[variables('sbVersion')]",
            "name": "[parameters('serviceBusQueueName')]",
            "type": "Queues",
            "dependsOn": [
                "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
            ],
            "properties": {
                "path": "[parameters('serviceBusQueueName')]"
            }
        }]
    }],
    "outputs": {
        "NamespaceConnectionString": {
            "type": "string",
            "value": "[listkeys(variables('authRuleResourceId'), variables('sbVersion')).primaryConnectionString]"
        },
        "SharedAccessPolicyPrimaryKey": {
            "type": "string",
            "value": "[listkeys(variables('authRuleResourceId'), variables('sbVersion')).primaryKey]"
        }
    }
}
```

### <a name="create-a-parameters-file-optional"></a>Создание файла параметров (необязательно)

toouse файл необязательные параметры копирования hello [201-servicebus создать очередь](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json) файла. Замените значение hello `serviceBusNamespaceName` с именем hello пространства имен Service Bus hello нужны toocreate в этом развертывании и замените значение hello `serviceBusQueueName` с именем hello hello очереди требуется toocreate.

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "value": "<myNamespaceName>"
        },
        "serviceBusQueueName": {
            "value": "<myQueueName>"
        },
        "serviceBusApiVersion": {
            "value": "2015-08-01"
        }
    }
}
```

Дополнительные сведения см. в разделе hello [параметры](../azure-resource-manager/resource-group-template-deploy.md#parameter-files) раздела.

### <a name="log-in-tooazure-and-set-hello-azure-subscription"></a>Войдите в tooAzure и задать hello подписки Azure

В командной строке PowerShell выполните следующую команду hello:

```powershell
Login-AzureRmAccount
```

Все запрашиваемые toolog на tooyour учетная запись Azure. После входа в систему запустите следующие команды tooview hello доступных подписок.

```powershell
Get-AzureRMSubscription
```

Эта команда возвращает список доступных подписок Azure. Выберите подписку для hello текущего сеанса, выполнив следующую команду hello. Замените `<YourSubscriptionId>` hello GUID для hello подписки Azure необходимо toouse.

```powershell
Set-AzureRmContext -SubscriptionID <YourSubscriptionId>
```

### <a name="set-hello-resource-group"></a>Группа ресурсов набор hello

Если нет существующего ресурса группы, создайте новую группу ресурсов с hello ** New AzureRmResourceGroup ** команды. Укажите имя группы ресурсов hello и место toouse hello. Например:

```powershell
New-AzureRmResourceGroup -Name MyDemoRG -Location "West US"
```

В случае успешного выполнения отображается сводка hello новую группу ресурсов.

```powershell
ResourceGroupName : MyDemoRG
Location          : westus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/<GUID>/resourceGroups/MyDemoRG
```

### <a name="test-hello-deployment"></a>Тестирование развертывания hello

Проверка развертывания, выполнив hello `Test-AzureRmResourceGroupDeployment` командлета. При тестировании hello развертывания, укажите параметры, точно так, как при выполнении развертывания hello.

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

### <a name="create-hello-deployment"></a>Создание развертывания hello

toocreate hello новое развертывание, запустите hello `New-AzureRmResourceGroupDeployment` командлет и укажите необходимые параметры hello при появлении запроса. Hello параметры включают имя для вашего развертывания hello имя группы ресурсов и hello путь или URL-адрес файла шаблона toohello. Если hello **режим** параметр не указан, значение по умолчанию hello **Incremental** используется. Дополнительные сведения см. в статье [Добавочные и полные развертывания](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments).

Здравствуйте, следующие командные строки вы hello трех параметров в окне PowerShell hello:

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

toospecify файл параметров используйте следующую команду hello.

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json -TemplateParameterFile <path tooparameters file>\azuredeploy.parameters.json
```

Также можно использовать встроенные параметры, при запуске командлета развертывания hello. Команда Hello выглядит следующим образом:

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json -parameterName "parameterValue"
```

toorun [завершения](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments) развертывания, набор hello **режим** параметр слишком**завершить**:

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -Mode Complete -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

### <a name="verify-hello-deployment"></a>Проверка развертывания hello
Если ресурсы hello успешно развертывается, сводка hello развертывания отображается в окне PowerShell hello:

```powershell
DeploymentName    : MyDemoDeployment
ResourceGroupName : MyDemoRG
ProvisioningState : Succeeded
Timestamp         : 4/19/2016 10:38:30 PM
Mode              : Incremental
TemplateLink      :
Parameters        :
                    Name             Type                       Value
                    ===============  =========================  ==========
                    serviceBusNamespaceName  String             <namespaceName>
                    serviceBusQueueName  String                 <queueName>
                    serviceBusApiVersion  String                2015-08-01

```

## <a name="next-steps"></a>Дальнейшие действия
Теперь вы увидели hello базовый рабочий процесс и команды для развертывания шаблона диспетчера ресурсов Azure. Для получения дополнительных сведений посетите hello ссылкам:

* [Общие сведения о диспетчере ресурсов Azure][Azure Resource Manager overview]
* [Развертывание ресурсов с использованием шаблонов Resource Manager и Azure PowerShell][Deploy resources with Azure Resource Manager templates]
* [Создание шаблонов диспетчера ресурсов Azure](../azure-resource-manager/resource-group-authoring-templates.md)

[Azure Resource Manager overview]: ../azure-resource-manager/resource-group-overview.md
[Deploy resources with Azure Resource Manager templates]: ../azure-resource-manager/resource-group-template-deploy.md
[Azure Quickstart Templates gallery]: https://azure.microsoft.com/documentation/templates/?term=service+bus
