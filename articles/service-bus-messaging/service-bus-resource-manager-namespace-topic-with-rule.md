---
title: "aaaCreate подписки раздела шины обслуживания Azure и правила с помощью шаблона Azure Resource Manager | Документы Microsoft"
description: "Создание пространства имен служебной шины с разделом, подпиской и правилом с помощью шаблона Azure Resource Manager."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 9e0aaf58-0214-4bca-bd00-d29c08f9b1bc
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: dbc46da8491aee4d0c73bd4db90c696008920df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-with-topic-subscription-and-rule-using-an-azure-resource-manager-template"></a>Создание пространства имен служебной шины с разделом, подпиской и правилом с помощью шаблона Azure Resource Manager

В этой статье показано, как toouse шаблона диспетчера ресурсов Azure, создает пространство имен служебной шины с раздела, подписки и правила (фильтр). Вы узнаете, как toodefine какие ресурсы развертываются с указанием как toodefine параметры, которые при выполнении развертывания hello. Этот шаблон используется для собственных развертывания или настройте его toomeet требований

Дополнительные сведения о создании шаблонов см. в статье [Создание шаблонов Azure Resource Manager][Authoring Azure Resource Manager templates].

Дополнительные сведения о практиках и шаблонах соглашений об именовании ресурсов Azure см. в разделе [Recommended naming conventions for Azure resources][Recommended naming conventions for Azure resources] (Рекомендуемые соглашения об именовании ресурсов Azure).

Полный шаблон hello, в разделе hello [пространства имен Service Bus с раздела, подписки и правила] [ Service Bus namespace with topic, subscription, and rule] шаблона.

> [!NOTE]
> следующие шаблоны Azure Resource Manager Hello доступны для загрузки и развертывания.
> 
> * [Создание пространства имен служебной шины с очередью и правилом авторизации](service-bus-resource-manager-namespace-auth-rule.md)
> * [Создание пространства имен служебной шины с очередью](service-bus-resource-manager-namespace-queue.md)
> * [Создайте пространство имен служебной шины](service-bus-resource-manager-namespace.md)
> * [Создание пространства имен служебной шины с разделом и подпиской](service-bus-resource-manager-namespace-topic.md)
> 
> toocheck для hello последние шаблоны, посетите hello [шаблоны быстрый запуск Azure] [ Azure Quickstart Templates] коллекции и выполните поиск по Service Bus.
> 
> 

## <a name="what-will-you-deploy"></a>Что вы развернете?

С помощью этого шаблона вы развернете пространство имен служебной шины с разделом, подпиской и правилом (фильтром).

[Разделы и подписки служебной шины](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) предоставляют разновидность взаимодействия "один ко многим" в рамках схемы *публикации или подписки*. При использовании разделов и подписок, компоненты распределенного приложения не взаимодействуют напрямую друг с другом, вместо этого они обмениваются сообщениями через раздел, в котором действует как посредник. Tooa подписки раздела напоминает виртуальную очередь, получающую копии сообщений, отправленных toohello раздела. Фильтр подписки позволяет toospecify сообщений отправила разделе tooa должны появиться в подписку определенного раздела.

## <a name="what-are-rules-filters"></a>Что такое правила (фильтры)?

Во многих ситуациях сообщения с определенными характеристиками должны обрабатываться разными способами. tooenable это, можно настроить подписки toofind сообщений, которые имеют определенные свойства, а затем выполните изменения toothose свойства. Несмотря на то, что все сообщения, отправленные toohello разделе подписках Service Bus см можно скопировать только подмножество этих сообщений toohello виртуальную очередь подписки. Это возможно благодаря использованию фильтров подписок. toolearn Дополнительные сведения о правилах (фильтры), в разделе [правила и действия](service-bus-queues-topics-subscriptions.md#rules-and-actions).

toorun hello развертывания автоматически, нажмите кнопку hello следующие кнопки:

[![Развертывание tooAzure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-subscription-rule%2Fazuredeploy.json)

## <a name="parameters"></a>Параметры

С помощью диспетчера ресурсов Azure необходимо определить параметры для значения требуется toospecify при развертывании шаблона hello. шаблон Hello имеется раздел с именем `Parameters` , содержащий значения всех параметров hello. Следует определить параметр для тех значений, которые отличаются на основе hello проекта, в которой выполняется развертывание или на основании hello среды, в которой выполняется развертывание. Определяет параметры для hello значения, которые всегда остаются одинаковыми. Каждое значение параметра используется в hello шаблона toodefine hello ресурсы, которые развертываются.

шаблон Hello определяет hello следующие параметры:

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
### <a name="servicebusrulename"></a>serviceBusRuleName
Имя Hello rule(filter) hello, созданные в пространство имен Service Bus hello.

```json
   "serviceBusRuleName": {
   "type": "string",
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
Создает стандартное пространство имен служебной шины типа **Messaging** с разделом, подпиской и правилами.

```json
 "resources": [{
        "apiVersion": "[variables('sbVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "sku": {
            "name": "Standard",
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
                "path": "[parameters('serviceBusTopicName')]"
            },
            "resources": [{
                "apiVersion": "[variables('sbVersion')]",
                "name": "[parameters('serviceBusSubscriptionName')]",
                "type": "Subscriptions",
                "dependsOn": [
                    "[parameters('serviceBusTopicName')]"
                ],
                "properties": {},
                "resources": [{
                    "apiVersion": "[variables('sbVersion')]",
                    "name": "[parameters('serviceBusRuleName')]",
                    "type": "Rules",
                    "dependsOn": [
                        "[parameters('serviceBusSubscriptionName')]"
                    ],
                    "properties": {
                        "filter": {
                            "sqlExpression": "StoreName = 'Store1'"
                        },
                        "action": {
                            "sqlExpression": "set FilterTag = 'true'"
                        }
                    }
                }]
            }]
        }]
    }]
```

## <a name="commands-toorun-deployment"></a>Команды toorun развертывания
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a>PowerShell
```powershell
New-AzureResourceGroupDeployment -Name \<deployment-name\> -ResourceGroupName \<resource-group-name\> -TemplateUri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="azure-cli"></a>Инфраструктура CLI Azure
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="next-steps"></a>Дальнейшие действия
Теперь, создания и развертывания ресурсов с помощью диспетчера ресурсов Azure, узнайте, как toomanage эти ресурсы в следующих статьях:

* [Управление служебной шиной Azure](service-bus-management-libraries.md)
* [Управление служебной шиной с помощью PowerShell](service-bus-manage-with-ps.md)
* [Управление ресурсами Service Bus с помощью обозревателя Service Bus hello](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus topics and subscriptions]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Recommended naming conventions for Azure resources]: ../guidance/guidance-naming-conventions.md
[Service Bus namespace with topic, subscription, and rule]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-topic-subscription-rule/
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md

