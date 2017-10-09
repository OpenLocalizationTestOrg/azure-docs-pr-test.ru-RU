---
title: "aaaAutomatically масштабирования единицы производительности концентраторов событий Azure | Документы Microsoft"
description: "Включить автоматическое увеличению на tooautomatically пространства имен, масштабирования единицы пропускной способности"
services: event-hubs
documentationcenter: na
author: ShubhaVijayasarathy
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: shvija;sethm
ms.openlocfilehash: 0f5216bcd619ccddc1fd4063a2f0131bfa36c7d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-scale-up-azure-event-hubs-throughput-units"></a><span data-ttu-id="d27e6-103">Автоматическое масштабирование единиц пропускной способности концентратора событий Azure</span><span class="sxs-lookup"><span data-stu-id="d27e6-103">Automatically scale up Azure Event Hubs throughput units</span></span>

## <a name="overview"></a><span data-ttu-id="d27e6-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="d27e6-104">Overview</span></span>

<span data-ttu-id="d27e6-105">Концентраторы событий Azure представляют собой платформу потоковой передачи платформы с высокой степенью масштабируемости.</span><span class="sxs-lookup"><span data-stu-id="d27e6-105">Azure Event Hubs is a highly scalable data streaming platform.</span></span> <span data-ttu-id="d27e6-106">Таким образом клиенты концентраторов событий часто повысить их использования после адаптации toohello службы.</span><span class="sxs-lookup"><span data-stu-id="d27e6-106">As such, Event Hubs customers often increase their usage after onboarding toohello service.</span></span> <span data-ttu-id="d27e6-107">Такого увеличения требуется возрастающее hello, предопределенные видеодрайвером пропускной способности единицы (TUs) tooscale концентраторов событий и обработки больших скоростью передачи.</span><span class="sxs-lookup"><span data-stu-id="d27e6-107">Such increases require increasing hello predetermined throughput units (TUs) tooscale Event Hubs and handle larger transfer rates.</span></span> <span data-ttu-id="d27e6-108">Hello *увеличению автоматически* функции концентраторов событий автоматически масштабируется hello число TUs toomeet потребностями.</span><span class="sxs-lookup"><span data-stu-id="d27e6-108">hello *Auto-inflate* feature of Event Hubs automatically scales up hello number of TUs toomeet usage needs.</span></span> <span data-ttu-id="d27e6-109">Увеличение единиц пропускной способности предотвращает сценарии регулирования, в которых:</span><span class="sxs-lookup"><span data-stu-id="d27e6-109">Increasing TUs prevents throttling scenarios, in which:</span></span>

* <span data-ttu-id="d27e6-110">скорости входящего трафика данных превышают установленные единицы пропускной способности;</span><span class="sxs-lookup"><span data-stu-id="d27e6-110">Data ingress rates exceed set TUs.</span></span>
* <span data-ttu-id="d27e6-111">скорости запросов исходящего трафика данных превышают установленные единицы пропускной способности.</span><span class="sxs-lookup"><span data-stu-id="d27e6-111">Data egress request rates exceed set TUs.</span></span>

## <a name="how-auto-inflate-works"></a><span data-ttu-id="d27e6-112">Как работает автоматическое расширение</span><span class="sxs-lookup"><span data-stu-id="d27e6-112">How Auto-inflate works</span></span>

<span data-ttu-id="d27e6-113">Трафик концентраторов событий контролируется с помощью единиц пропускной способности.</span><span class="sxs-lookup"><span data-stu-id="d27e6-113">Event Hubs traffic is controlled by throughput units.</span></span> <span data-ttu-id="d27e6-114">Одна единица пропускной способности разрешает входящий трафик со скоростью до 1 МБ/с и исходящий трафик со скоростью вдвое выше.</span><span class="sxs-lookup"><span data-stu-id="d27e6-114">A single TU allows 1 MB per second of ingress and twice that amount of egress.</span></span> <span data-ttu-id="d27e6-115">В концентраторах событий ценовой категории "Стандартный" можно настроить от 1 до 20 единиц пропускной способности.</span><span class="sxs-lookup"><span data-stu-id="d27e6-115">Standard Event Hubs can be configured with 1-20 throughput units.</span></span> <span data-ttu-id="d27e6-116">Увеличению автоматически включает toostart небольших единиц минимальная пропускная способность требуется hello.</span><span class="sxs-lookup"><span data-stu-id="d27e6-116">Auto-inflate enables you toostart small with hello minimum required throughput units.</span></span> <span data-ttu-id="d27e6-117">функция Hello затем автоматически масштабируется toohello максимальное количество единиц производительности, что нужно, в зависимости от hello увеличение трафика.</span><span class="sxs-lookup"><span data-stu-id="d27e6-117">hello feature then scales automatically toohello maximum limit of throughput units you need, depending on hello increase in your traffic.</span></span> <span data-ttu-id="d27e6-118">Увеличению автоматически предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="d27e6-118">Auto-inflate provides hello following benefits:</span></span>

- <span data-ttu-id="d27e6-119">Небольшое эффективного toostart масштабирования механизм и вертикального масштабирования, как вы увеличиваться.</span><span class="sxs-lookup"><span data-stu-id="d27e6-119">An efficient scaling mechanism toostart small and scale up as you grow.</span></span>
- <span data-ttu-id="d27e6-120">Автоматически масштабируйте указанного верхний предел toohello без проблем регулирования.</span><span class="sxs-lookup"><span data-stu-id="d27e6-120">Automatically scale toohello specified upper limit without throttling issues.</span></span>
- <span data-ttu-id="d27e6-121">Более широкие возможности управления масштабированием, как вы управляете и о том, сколько tooscale.</span><span class="sxs-lookup"><span data-stu-id="d27e6-121">More control over scaling, as you control when and how much tooscale.</span></span>

## <a name="enable-auto-inflate-on-a-namespace"></a><span data-ttu-id="d27e6-122">Включение автоматического расширения в пространстве имен</span><span class="sxs-lookup"><span data-stu-id="d27e6-122">Enable Auto-inflate on a namespace</span></span>

<span data-ttu-id="d27e6-123">Можно включить или отключить автоматическое увеличению на пространство имен, используя один из следующих методов hello:</span><span class="sxs-lookup"><span data-stu-id="d27e6-123">You can enable or disable Auto-inflate on a namespace using either of hello following methods:</span></span>

1. <span data-ttu-id="d27e6-124">Hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d27e6-124">hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d27e6-125">Шаблон Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d27e6-125">An Azure Resource Manager template.</span></span>

### <a name="enable-auto-inflate-through-hello-portal"></a><span data-ttu-id="d27e6-126">Включение автоматического увеличению через портал hello</span><span class="sxs-lookup"><span data-stu-id="d27e6-126">Enable Auto-inflate through hello portal</span></span>

<span data-ttu-id="d27e6-127">Функцию автоматического увеличению hello в пространстве имен можно включить при создании имен концентраторов событий:</span><span class="sxs-lookup"><span data-stu-id="d27e6-127">You can enable hello Auto-inflate feature on a namespace when creating an Event Hubs namespace:</span></span>
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate1.png)

<span data-ttu-id="d27e6-128">Если этот параметр включен, можно начать с малого числа единиц пропускной способности и повышать его по мере роста потребностей использования.</span><span class="sxs-lookup"><span data-stu-id="d27e6-128">With this option enabled, you can start small on your throughput units and scale up as your usage needs increase.</span></span> <span data-ttu-id="d27e6-129">Hello верхний предел для расширению не влияет на цены, зависящее от hello число TUs, используемый в час.</span><span class="sxs-lookup"><span data-stu-id="d27e6-129">hello upper limit for inflation does not affect pricing, which depends on hello number of TUs used per hour.</span></span>

<span data-ttu-id="d27e6-130">Можно также включить увеличению автоматически с помощью hello **шкалы** параметр в колонке параметров hello hello портала:</span><span class="sxs-lookup"><span data-stu-id="d27e6-130">You can also enable Auto-inflate using hello **Scale** option on hello settings blade in hello portal:</span></span>
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate2.png)

### <a name="enable-auto-inflate-using-an-azure-resource-manager-template"></a><span data-ttu-id="d27e6-131">Включение автоматического расширения с помощью шаблона Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d27e6-131">Enable Auto-Inflate using an Azure Resource Manager template</span></span>

<span data-ttu-id="d27e6-132">Вы можете включить автоматическое расширение во время развертывания шаблона Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d27e6-132">You can enable Auto-inflate during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="d27e6-133">Например, набор hello `isAutoInflateEnabled` свойство слишком**true** и задайте `maximumThroughputUnits` too10.</span><span class="sxs-lookup"><span data-stu-id="d27e6-133">For example, set hello `isAutoInflateEnabled` property too**true** and set `maximumThroughputUnits` too10.</span></span>

```json
"resources": [
        {
            "apiVersion": "2017-04-01",
            "name": "[parameters('namespaceName')]",
            "type": "Microsoft.EventHub/Namespaces",
            "location": "[variables('location')]",
            "sku": {
                "name": "Standard",
                "tier": "Standard"
            },
            "properties": {
                "isAutoInflateEnabled": true,
                "maximumThroughputUnits": 10
            },
            "resources": [
                {
                    "apiVersion": "2017-04-01",
                    "name": "[parameters('eventHubName')]",
                    "type": "EventHubs",
                    "dependsOn": [
                        "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
                    ],
                    "properties": {},
                    "resources": [
                        {
                            "apiVersion": "2017-04-01",
                            "name": "[parameters('consumerGroupName')]",
                            "type": "ConsumerGroups",
                            "dependsOn": [
                                "[parameters('eventHubName')]"
                            ],
                            "properties": {}
                        }
                    ]
                }
            ]
        }
    ]
```

<span data-ttu-id="d27e6-134">Полный шаблон hello, в разделе hello [пространства имен для создания концентраторов событий и включение увеличению](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) шаблона на GitHub.</span><span class="sxs-lookup"><span data-stu-id="d27e6-134">For hello complete template, see hello [Create Event Hubs namespace and enable inflate](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) template on GitHub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d27e6-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d27e6-135">Next steps</span></span>

<span data-ttu-id="d27e6-136">На сайте ссылкам hello, изучите более подробную концентраторов событий:</span><span class="sxs-lookup"><span data-stu-id="d27e6-136">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="d27e6-137">Обзор концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="d27e6-137">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="d27e6-138">Создание концентратора событий</span><span class="sxs-lookup"><span data-stu-id="d27e6-138">Create an Event Hub</span></span>](event-hubs-create.md)
