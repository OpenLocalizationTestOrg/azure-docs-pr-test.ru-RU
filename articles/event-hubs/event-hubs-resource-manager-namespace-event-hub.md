---
title: "Создание пространства имен и группы потребителей концентраторов событий Azure с помощью шаблона | Документация Майкрософт"
description: "Создание пространства имен концентраторов событий c концентратором событий и группой потребителей с помощью шаблонов Azure Resource Manager."
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 28bb4591-1fd7-444f-a327-4e67e8878798
ms.service: event-hubs
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/12/2017
ms.author: sethm;shvija
ms.openlocfilehash: eb9a80eec0326aaa605cb8b21aecbaeec94ff212
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-event-hubs-namespace-with-event-hub-and-consumer-group-using-an-azure-resource-manager-template"></a><span data-ttu-id="7a831-103">Создание пространства имен концентраторов событий с концентратором событий и группой потребителей с помощью шаблона Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7a831-103">Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template</span></span>

<span data-ttu-id="7a831-104">Из этой статьи вы узнаете, как с помощью шаблона Azure Resource Manager создать пространство имен типа EventHubs с одним концентратором событий и одной группой потребителей.</span><span class="sxs-lookup"><span data-stu-id="7a831-104">This article shows how to use an Azure Resource Manager template that creates a namespace of type Event Hubs, with one event hub and one consumer group.</span></span> <span data-ttu-id="7a831-105">Здесь показано, как определить развертываемые ресурсы и параметры, указываемые при развертывании.</span><span class="sxs-lookup"><span data-stu-id="7a831-105">The article shows how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="7a831-106">Этот шаблон можно использовать для собственных развертываний или изменить его в соответствии с вашими требованиями.</span><span class="sxs-lookup"><span data-stu-id="7a831-106">You can use this template for your own deployments, or customize it to meet your requirements</span></span>

<span data-ttu-id="7a831-107">Дополнительные сведения о создании шаблонов см. в статье [Создание шаблонов Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="7a831-107">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="7a831-108">Полный шаблон приведен в разделе [Event Hub and consumer group template][Event Hub and consumer group template] (Шаблон концентратора событий и группы потребителей) на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="7a831-108">For the complete template, see the [Event hub and consumer group template][Event Hub and consumer group template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="7a831-109">Чтобы узнать о новых шаблонах, изучите коллекцию [Шаблоны быстрого запуска Azure][Azure Quickstart Templates] и выполните в ней поиск по запросу "концентраторы событий".</span><span class="sxs-lookup"><span data-stu-id="7a831-109">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Event Hubs.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="7a831-110">Что вы развернете?</span><span class="sxs-lookup"><span data-stu-id="7a831-110">What will you deploy?</span></span>
<span data-ttu-id="7a831-111">С помощью этого шаблона вы развернете пространство имен концентраторов событий с концентратором событий и группой потребителей.</span><span class="sxs-lookup"><span data-stu-id="7a831-111">With this template, you will deploy an Event Hubs namespace with an event hub and a consumer group.</span></span>

<span data-ttu-id="7a831-112">[Концентраторы событий](event-hubs-what-is-event-hubs.md) — это служба обработки событий, используемая для крупномасштабной передачи данных событий и телеметрии в Azure. Работа службы характеризуется низкой задержкой и высокой надежностью.</span><span class="sxs-lookup"><span data-stu-id="7a831-112">[Event Hubs](event-hubs-what-is-event-hubs.md) is an event processing service used to provide event and telemetry ingress to Azure at massive scale, with low latency and high reliability.</span></span>

<span data-ttu-id="7a831-113">Чтобы выполнить развертывание автоматически, нажмите следующую кнопку.</span><span class="sxs-lookup"><span data-stu-id="7a831-113">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="7a831-114">[![Развертывание в Azure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-event-hubs-create-event-hub-and-consumer-group%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="7a831-114">[![Deploy to Azure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-event-hubs-create-event-hub-and-consumer-group%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="7a831-115">Параметры</span><span class="sxs-lookup"><span data-stu-id="7a831-115">Parameters</span></span>
<span data-ttu-id="7a831-116">С помощью диспетчера ресурсов Azure можно определить параметры значений, которые должны указываться на этапе развертывания шаблона.</span><span class="sxs-lookup"><span data-stu-id="7a831-116">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="7a831-117">В шаблоне есть раздел `Parameters` , содержащий все значения параметров.</span><span class="sxs-lookup"><span data-stu-id="7a831-117">The template includes a section called `Parameters` that contains all the parameter values.</span></span> <span data-ttu-id="7a831-118">Для изменяющихся значений нужно определить параметры с учетом развертываемого проекта либо окружения, где выполняется развертывание.</span><span class="sxs-lookup"><span data-stu-id="7a831-118">You should define a parameter for those values that will vary, based on the project you are deploying or based on the environment to which you are deploying.</span></span> <span data-ttu-id="7a831-119">Не определяйте параметры для значений, которые не меняются.</span><span class="sxs-lookup"><span data-stu-id="7a831-119">Do not define parameters for values that always stay the same.</span></span> <span data-ttu-id="7a831-120">Значение каждого параметра в шаблоне определяет развертываемые ресурсы.</span><span class="sxs-lookup"><span data-stu-id="7a831-120">Each parameter value in the template defines the resources that are deployed.</span></span>

<span data-ttu-id="7a831-121">Ниже описаны параметры, которые определяет шаблон.</span><span class="sxs-lookup"><span data-stu-id="7a831-121">The template defines the following parameters:</span></span>

### <a name="eventhubnamespacename"></a><span data-ttu-id="7a831-122">eventHubNamespaceName</span><span class="sxs-lookup"><span data-stu-id="7a831-122">eventHubNamespaceName</span></span>
<span data-ttu-id="7a831-123">Имя создаваемого пространства имен концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="7a831-123">The name of the Event Hubs namespace to create.</span></span>

```json
"eventHubNamespaceName": {
"type": "string"
}
```

### <a name="eventhubname"></a><span data-ttu-id="7a831-124">eventHubName</span><span class="sxs-lookup"><span data-stu-id="7a831-124">eventHubName</span></span>
<span data-ttu-id="7a831-125">Имя концентратора событий, создаваемого в пространстве имен концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="7a831-125">The name of the event hub created in the Event Hubs namespace.</span></span>

```json
"eventHubName": {
"type": "string"
}
```

### <a name="eventhubconsumergroupname"></a><span data-ttu-id="7a831-126">eventHubConsumerGroupName</span><span class="sxs-lookup"><span data-stu-id="7a831-126">eventHubConsumerGroupName</span></span>
<span data-ttu-id="7a831-127">Имя группы потребителей, создаваемой для концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="7a831-127">The name of the consumer group created for the event hub.</span></span>

```json
"eventHubConsumerGroupName": {
"type": "string"
}
```

### <a name="apiversion"></a><span data-ttu-id="7a831-128">версия_API</span><span class="sxs-lookup"><span data-stu-id="7a831-128">apiVersion</span></span>
<span data-ttu-id="7a831-129">Версия API шаблона.</span><span class="sxs-lookup"><span data-stu-id="7a831-129">The API version of the template.</span></span>

```json
"apiVersion": {
"type": "string"
}
```

## <a name="resources-to-deploy"></a><span data-ttu-id="7a831-130">Развертываемые ресурсы</span><span class="sxs-lookup"><span data-stu-id="7a831-130">Resources to deploy</span></span>
<span data-ttu-id="7a831-131">Создает пространство имен типа **EventHubs** с концентратором событий и группой потребителей.</span><span class="sxs-lookup"><span data-stu-id="7a831-131">Creates a namespace of type **EventHubs**, with an event hub and a consumer group.</span></span>

```json
"resources":[  
      {  
         "apiVersion":"[variables('ehVersion')]",
         "name":"[parameters('namespaceName')]",
         "type":"Microsoft.EventHub/namespaces",
         "location":"[variables('location')]",
         "sku":{  
            "name":"Standard",
            "tier":"Standard"
         },
         "resources":[  
            {  
               "apiVersion":"[variables('ehVersion')]",
               "name":"[parameters('eventHubName')]",
               "type":"EventHubs",
               "dependsOn":[  
                  "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
               ],
               "properties":{  
                  "path":"[parameters('eventHubName')]"
               },
               "resources":[  
                  {  
                     "apiVersion":"[variables('ehVersion')]",
                     "name":"[parameters('consumerGroupName')]",
                     "type":"ConsumerGroups",
                     "dependsOn":[  
                        "[parameters('eventHubName')]"
                     ],
                     "properties":{  

                     }
                  }
               ]
            }
         ]
      }
   ],
```

## <a name="commands-to-run-deployment"></a><span data-ttu-id="7a831-132">Команды для выполнения развертывания</span><span class="sxs-lookup"><span data-stu-id="7a831-132">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="7a831-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7a831-133">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json
```

## <a name="azure-cli"></a><span data-ttu-id="7a831-134">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="7a831-134">Azure CLI</span></span>
```cli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json][]
```

## <a name="next-steps"></a><span data-ttu-id="7a831-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7a831-135">Next steps</span></span>
<span data-ttu-id="7a831-136">Дополнительные сведения о концентраторах событий см. в следующих источниках:</span><span class="sxs-lookup"><span data-stu-id="7a831-136">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="7a831-137">Обзор концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="7a831-137">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="7a831-138">Создание концентратора событий</span><span class="sxs-lookup"><span data-stu-id="7a831-138">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="7a831-139">Часто задаваемые вопросы о концентраторах событий</span><span class="sxs-lookup"><span data-stu-id="7a831-139">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Using Azure PowerShell with Azure Resource Manager]: ../powershell-azure-resource-manager.md
[Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../xplat-cli-azure-resource-manager.md
[Event hub and consumer group template]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-event-hubs-create-event-hub-and-consumer-group/
