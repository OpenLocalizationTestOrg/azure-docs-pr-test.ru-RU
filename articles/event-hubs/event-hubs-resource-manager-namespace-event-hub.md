---
title: "aaaCreate концентраторов событий Azure пространства имен и потребитель группу с помощью шаблона | Документы Microsoft"
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
ms.openlocfilehash: 74b0d6b3fbe848705e2c20e628aa4e5269b53edb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-with-event-hub-and-consumer-group-using-an-azure-resource-manager-template"></a><span data-ttu-id="7b54d-103">Создание пространства имен концентраторов событий с концентратором событий и группой потребителей с помощью шаблона Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7b54d-103">Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template</span></span>

<span data-ttu-id="7b54d-104">В этой статье показано, как toouse шаблона диспетчера ресурсов Azure, создает пространство имен типа концентраторов событий с концентратором одно событие и одной группе потребителей.</span><span class="sxs-lookup"><span data-stu-id="7b54d-104">This article shows how toouse an Azure Resource Manager template that creates a namespace of type Event Hubs, with one event hub and one consumer group.</span></span> <span data-ttu-id="7b54d-105">Hello статьи показано, как toodefine какие ресурсы развертываются с указанием как toodefine параметры, которые при выполнении развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="7b54d-105">hello article shows how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="7b54d-106">Этот шаблон используется для собственных развертывания или настройте его toomeet требований</span><span class="sxs-lookup"><span data-stu-id="7b54d-106">You can use this template for your own deployments, or customize it toomeet your requirements</span></span>

<span data-ttu-id="7b54d-107">Дополнительные сведения о создании шаблонов см. в статье [Создание шаблонов Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="7b54d-107">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="7b54d-108">Полный шаблон hello, в разделе hello [шаблона группы концентратора и потребитель события] [ Event Hub and consumer group template] на GitHub.</span><span class="sxs-lookup"><span data-stu-id="7b54d-108">For hello complete template, see hello [Event hub and consumer group template][Event Hub and consumer group template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="7b54d-109">toocheck для hello последние шаблоны, посетите hello [шаблоны быстрый запуск Azure] [ Azure Quickstart Templates] коллекции и выполните поиск концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="7b54d-109">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Event Hubs.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="7b54d-110">Что вы развернете?</span><span class="sxs-lookup"><span data-stu-id="7b54d-110">What will you deploy?</span></span>
<span data-ttu-id="7b54d-111">С помощью этого шаблона вы развернете пространство имен концентраторов событий с концентратором событий и группой потребителей.</span><span class="sxs-lookup"><span data-stu-id="7b54d-111">With this template, you will deploy an Event Hubs namespace with an event hub and a consumer group.</span></span>

<span data-ttu-id="7b54d-112">[Концентраторы событий](event-hubs-what-is-event-hubs.md) событие обработки службы, используемой tooprovide событий и телеметрии входящих tooAzure в большом масштабе с небольшой задержкой и высокой степенью надежности.</span><span class="sxs-lookup"><span data-stu-id="7b54d-112">[Event Hubs](event-hubs-what-is-event-hubs.md) is an event processing service used tooprovide event and telemetry ingress tooAzure at massive scale, with low latency and high reliability.</span></span>

<span data-ttu-id="7b54d-113">toorun hello развертывания автоматически, нажмите кнопку hello следующие кнопки:</span><span class="sxs-lookup"><span data-stu-id="7b54d-113">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="7b54d-114">[![Развертывание tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-event-hubs-create-event-hub-and-consumer-group%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="7b54d-114">[![Deploy tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-event-hubs-create-event-hub-and-consumer-group%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="7b54d-115">Параметры</span><span class="sxs-lookup"><span data-stu-id="7b54d-115">Parameters</span></span>
<span data-ttu-id="7b54d-116">С помощью диспетчера ресурсов Azure можно определить параметры для значения требуется toospecify при развертывании шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="7b54d-116">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="7b54d-117">шаблон Hello имеется раздел с именем `Parameters` , содержащий значения всех параметров hello.</span><span class="sxs-lookup"><span data-stu-id="7b54d-117">hello template includes a section called `Parameters` that contains all hello parameter values.</span></span> <span data-ttu-id="7b54d-118">Следует определить параметр для те значения, которые могут меняться, на основе hello проекта, в которой выполняется развертывание или на основании toowhich среды hello, в которой выполняется развертывание.</span><span class="sxs-lookup"><span data-stu-id="7b54d-118">You should define a parameter for those values that will vary, based on hello project you are deploying or based on hello environment toowhich you are deploying.</span></span> <span data-ttu-id="7b54d-119">Определяет параметры для hello значения, которые всегда остаются одинаковыми.</span><span class="sxs-lookup"><span data-stu-id="7b54d-119">Do not define parameters for values that always stay hello same.</span></span> <span data-ttu-id="7b54d-120">Каждое значение параметра в шаблоне hello определяет hello ресурсы, которые развертываются.</span><span class="sxs-lookup"><span data-stu-id="7b54d-120">Each parameter value in hello template defines hello resources that are deployed.</span></span>

<span data-ttu-id="7b54d-121">шаблон Hello определяет hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="7b54d-121">hello template defines hello following parameters:</span></span>

### <a name="eventhubnamespacename"></a><span data-ttu-id="7b54d-122">eventHubNamespaceName</span><span class="sxs-lookup"><span data-stu-id="7b54d-122">eventHubNamespaceName</span></span>
<span data-ttu-id="7b54d-123">Имя пространства имен toocreate hello концентраторов событий Hello.</span><span class="sxs-lookup"><span data-stu-id="7b54d-123">hello name of hello Event Hubs namespace toocreate.</span></span>

```json
"eventHubNamespaceName": {
"type": "string"
}
```

### <a name="eventhubname"></a><span data-ttu-id="7b54d-124">eventHubName</span><span class="sxs-lookup"><span data-stu-id="7b54d-124">eventHubName</span></span>
<span data-ttu-id="7b54d-125">Имя Hello hello концентратора событий, созданные в пространстве имен концентраторы событий hello.</span><span class="sxs-lookup"><span data-stu-id="7b54d-125">hello name of hello event hub created in hello Event Hubs namespace.</span></span>

```json
"eventHubName": {
"type": "string"
}
```

### <a name="eventhubconsumergroupname"></a><span data-ttu-id="7b54d-126">eventHubConsumerGroupName</span><span class="sxs-lookup"><span data-stu-id="7b54d-126">eventHubConsumerGroupName</span></span>
<span data-ttu-id="7b54d-127">Имя группы потребителей hello, созданных для концентратора событий hello Hello.</span><span class="sxs-lookup"><span data-stu-id="7b54d-127">hello name of hello consumer group created for hello event hub.</span></span>

```json
"eventHubConsumerGroupName": {
"type": "string"
}
```

### <a name="apiversion"></a><span data-ttu-id="7b54d-128">версия_API</span><span class="sxs-lookup"><span data-stu-id="7b54d-128">apiVersion</span></span>
<span data-ttu-id="7b54d-129">версия Hello API hello шаблона.</span><span class="sxs-lookup"><span data-stu-id="7b54d-129">hello API version of hello template.</span></span>

```json
"apiVersion": {
"type": "string"
}
```

## <a name="resources-toodeploy"></a><span data-ttu-id="7b54d-130">Toodeploy ресурсы</span><span class="sxs-lookup"><span data-stu-id="7b54d-130">Resources toodeploy</span></span>
<span data-ttu-id="7b54d-131">Создает пространство имен типа **EventHubs** с концентратором событий и группой потребителей.</span><span class="sxs-lookup"><span data-stu-id="7b54d-131">Creates a namespace of type **EventHubs**, with an event hub and a consumer group.</span></span>

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

## <a name="commands-toorun-deployment"></a><span data-ttu-id="7b54d-132">Команды toorun развертывания</span><span class="sxs-lookup"><span data-stu-id="7b54d-132">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="7b54d-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7b54d-133">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json
```

## <a name="azure-cli"></a><span data-ttu-id="7b54d-134">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="7b54d-134">Azure CLI</span></span>
```cli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json][]
```

## <a name="next-steps"></a><span data-ttu-id="7b54d-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7b54d-135">Next steps</span></span>
<span data-ttu-id="7b54d-136">На сайте ссылкам hello, изучите более подробную концентраторов событий:</span><span class="sxs-lookup"><span data-stu-id="7b54d-136">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="7b54d-137">Обзор концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="7b54d-137">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="7b54d-138">Создание концентратора событий</span><span class="sxs-lookup"><span data-stu-id="7b54d-138">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="7b54d-139">Часто задаваемые вопросы о концентраторах событий</span><span class="sxs-lookup"><span data-stu-id="7b54d-139">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Using Azure PowerShell with Azure Resource Manager]: ../powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../xplat-cli-azure-resource-manager.md
[Event hub and consumer group template]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-event-hubs-create-event-hub-and-consumer-group/
