---
title: "aaaCreate подписки на раздел Azure Service Bus пространства имен с помощью шаблона диспетчера ресурсов Azure | Документы Microsoft"
description: "Создание пространства имен служебной шины с разделом и подпиской с помощью шаблона Azure Resource Manager."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: d3d55200-5c60-4b5f-822d-59974cafff0e
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: 9b5f7d8710e598b73c0a7ea3daf8c300f7fa9ecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-with-topic-and-subscription-using-an-azure-resource-manager-template"></a>Создание пространства имен служебной шины с разделом и подпиской с помощью шаблона Azure Resource Manager

В этой статье показано, как toouse шаблона диспетчера ресурсов Azure, создает пространство имен служебной шины и раздела и подписки в этом пространстве имен. Вы узнаете, как toodefine какие ресурсы развертываются с указанием как toodefine параметры, которые при выполнении развертывания hello. Этот шаблон используется для собственных развертывания или настройте его toomeet требований

Дополнительные сведения о создании шаблонов см. в статье [Создание шаблонов Azure Resource Manager][Authoring Azure Resource Manager templates].

Полный шаблон hello, в разделе hello [пространства имен Service Bus с помощью разделов и подписок] [ Service Bus namespace with topic and subscription] шаблона.

> [!NOTE]
> следующие шаблоны Azure Resource Manager Hello доступны для загрузки и развертывания.
> 
> * [Создайте пространство имен служебной шины](service-bus-resource-manager-namespace.md)
> * [Создание пространства имен служебной шины с очередью](service-bus-resource-manager-namespace-queue.md)
> * [Создание пространства имен служебной шины с очередью и правилом авторизации](service-bus-resource-manager-namespace-auth-rule.md)
> * [Создание пространства имен служебной шины с разделом, подпиской и правилом с помощью шаблона Azure Resource Manager](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> toocheck для hello последние шаблоны, посетите hello [шаблоны быстрый запуск Azure] [ Azure Quickstart Templates] коллекции и выполните поиск «Шина обслуживания».
> 
> 

## <a name="what-will-you-deploy"></a>Что вы развернете?

С помощью этого шаблона вы развернете пространство имен служебной шины с разделом и подпиской.

[Разделы и подписки служебной шины](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) предоставляют разновидность взаимодействия "один ко многим" в рамках схемы *публикации или подписки*.

toorun hello развертывания автоматически, нажмите кнопку hello следующие кнопки:

[![Развертывание tooAzure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-and-subscription%2Fazuredeploy.json)

## <a name="parameters"></a>Параметры

С помощью диспетчера ресурсов Azure можно определить параметры для значения требуется toospecify при развертывании шаблона hello. шаблон Hello имеется раздел с именем `Parameters` , содержащий все значения параметров hello. Следует определить параметр для те значения, которые будут различаться на основе hello проекта, в которой выполняется развертывание или на основании hello среды, в которой выполняется развертывание. Определяет параметры для значения, которые всегда останутся hello таким же. Каждое значение параметра используется в hello шаблона toodefine hello ресурсы, которые развертываются.

шаблон Hello определяет hello следующие параметры.

### <a name="servicebusnamespacename"></a>serviceBusNamespaceName
Имя Hello toocreate пространство имен Service Bus hello.

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="servicebustopicname"></a>serviceBusTopicName
Имя Hello раздел hello, создан в пространстве имен Service Bus hello.

```json
"serviceBusTopicName": {
"type": "string"
}
```

### <a name="servicebussubscriptionname"></a>serviceBusSubscriptionName
Имя Hello hello подписка, созданная в пространство имен Service Bus hello.

```json
"serviceBusSubscriptionName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a>serviceBusApiVersion
версия API служебной шины Hello hello шаблона.

```json
"serviceBusApiVersion": {
"type": "string"
}
```
## <a name="resources-toodeploy"></a>Toodeploy ресурсы
Создает стандартное пространство имен служебной шины типа **Messaging**с разделом и подпиской.

```json
"resources ": [{
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
            "name": "[parameters('serviceBusTopicName')]",
            "type": "Topics",
            "dependsOn": [
                "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
            ],
            "properties": {
                "path": "[parameters('serviceBusTopicName')]",
            },
            "resources": [{
                "apiVersion": "[variables('sbVersion')]",
                "name": "[parameters('serviceBusSubscriptionName')]",
                "type": "Subscriptions",
                "dependsOn": [
                    "[parameters('serviceBusTopicName')]"
                ],
                "properties": {}
            }]
        }]
    }]
```

## <a name="commands-toorun-deployment"></a>Команды toorun развертывания
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a>PowerShell
```powershell
New-AzureResourceGroupDeployment -Name \<deployment-name\> -ResourceGroupName \<resource-group-name\> -TemplateUri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-and-subscription/azuredeploy.json>
```

## <a name="azure-cli"></a>Инфраструктура CLI Azure
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-and-subscription/azuredeploy.json>
```

## <a name="next-steps"></a>Дальнейшие действия
Теперь, создания и развертывания ресурсов с помощью диспетчера ресурсов Azure, узнайте, как toomanage эти ресурсы в следующих статьях:

* [Управление служебной шиной с помощью PowerShell](service-bus-manage-with-ps.md)
* [Управление ресурсами Service Bus с помощью обозревателя Service Bus hello](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus topics and subscriptions]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Service Bus namespace with topic and subscription]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-topic-and-subscription/
