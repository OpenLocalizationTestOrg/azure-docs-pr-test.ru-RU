---
title: "Автоматическое масштабирование единиц пропускной способности концентратора событий Azure | Документы Майкрософт"
description: "Включение автоматического расширения пространства имен для автоматического масштабирования единиц пропускной способности"
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
ms.openlocfilehash: b085091ea7bfd601efb0eee84144ddd091422d6e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="automatically-scale-up-azure-event-hubs-throughput-units"></a><span data-ttu-id="2476c-103">Автоматическое масштабирование единиц пропускной способности концентратора событий Azure</span><span class="sxs-lookup"><span data-stu-id="2476c-103">Automatically scale up Azure Event Hubs throughput units</span></span>

## <a name="overview"></a><span data-ttu-id="2476c-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="2476c-104">Overview</span></span>

<span data-ttu-id="2476c-105">Концентраторы событий Azure представляют собой платформу потоковой передачи платформы с высокой степенью масштабируемости.</span><span class="sxs-lookup"><span data-stu-id="2476c-105">Azure Event Hubs is a highly scalable data streaming platform.</span></span> <span data-ttu-id="2476c-106">По этой причине клиенты концентраторов событий часто повышают свое использование после адаптации к службе.</span><span class="sxs-lookup"><span data-stu-id="2476c-106">As such, Event Hubs customers often increase their usage after onboarding to the service.</span></span> <span data-ttu-id="2476c-107">Для такого повышения требуется увеличение предопределенных единиц пропускной способности для масштабирования концентраторов событий и обработки возросших скоростей передачи.</span><span class="sxs-lookup"><span data-stu-id="2476c-107">Such increases require increasing the predetermined throughput units (TUs) to scale Event Hubs and handle larger transfer rates.</span></span> <span data-ttu-id="2476c-108">Функция автоматического расширения *Auto-inflate* концентраторов событий автоматически масштабирует число единиц пропускной способности в соответствии с потребностями.</span><span class="sxs-lookup"><span data-stu-id="2476c-108">The *Auto-inflate* feature of Event Hubs automatically scales up the number of TUs to meet usage needs.</span></span> <span data-ttu-id="2476c-109">Увеличение единиц пропускной способности предотвращает сценарии регулирования, в которых:</span><span class="sxs-lookup"><span data-stu-id="2476c-109">Increasing TUs prevents throttling scenarios, in which:</span></span>

* <span data-ttu-id="2476c-110">скорости входящего трафика данных превышают установленные единицы пропускной способности;</span><span class="sxs-lookup"><span data-stu-id="2476c-110">Data ingress rates exceed set TUs.</span></span>
* <span data-ttu-id="2476c-111">скорости запросов исходящего трафика данных превышают установленные единицы пропускной способности.</span><span class="sxs-lookup"><span data-stu-id="2476c-111">Data egress request rates exceed set TUs.</span></span>

## <a name="how-auto-inflate-works"></a><span data-ttu-id="2476c-112">Как работает автоматическое расширение</span><span class="sxs-lookup"><span data-stu-id="2476c-112">How Auto-inflate works</span></span>

<span data-ttu-id="2476c-113">Трафик концентраторов событий контролируется с помощью единиц пропускной способности.</span><span class="sxs-lookup"><span data-stu-id="2476c-113">Event Hubs traffic is controlled by throughput units.</span></span> <span data-ttu-id="2476c-114">Одна единица пропускной способности разрешает входящий трафик со скоростью до 1 МБ/с и исходящий трафик со скоростью вдвое выше.</span><span class="sxs-lookup"><span data-stu-id="2476c-114">A single TU allows 1 MB per second of ingress and twice that amount of egress.</span></span> <span data-ttu-id="2476c-115">В концентраторах событий ценовой категории "Стандартный" можно настроить от 1 до 20 единиц пропускной способности.</span><span class="sxs-lookup"><span data-stu-id="2476c-115">Standard Event Hubs can be configured with 1-20 throughput units.</span></span> <span data-ttu-id="2476c-116">Автоматическое расширение позволяет начать с минимального числа единиц пропускной способности.</span><span class="sxs-lookup"><span data-stu-id="2476c-116">Auto-inflate enables you to start small with the minimum required throughput units.</span></span> <span data-ttu-id="2476c-117">Затем эта функция автоматически масштабируется до максимально необходимого количества единиц пропускной способности в рамках имеющихся ограничений по мере роста трафика.</span><span class="sxs-lookup"><span data-stu-id="2476c-117">The feature then scales automatically to the maximum limit of throughput units you need, depending on the increase in your traffic.</span></span> <span data-ttu-id="2476c-118">Функция автоматического расширения обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="2476c-118">Auto-inflate provides the following benefits:</span></span>

- <span data-ttu-id="2476c-119">Эффективный механизм масштабирования, позволяющий начать с малого и расширяться по мере роста.</span><span class="sxs-lookup"><span data-stu-id="2476c-119">An efficient scaling mechanism to start small and scale up as you grow.</span></span>
- <span data-ttu-id="2476c-120">Автоматическое масштабирование до указанного верхнего предела без проблем регулирования.</span><span class="sxs-lookup"><span data-stu-id="2476c-120">Automatically scale to the specified upper limit without throttling issues.</span></span>
- <span data-ttu-id="2476c-121">Более высокая степень контроля масштабирования, так как вы управляете тем, когда и насколько следует масштабировать.</span><span class="sxs-lookup"><span data-stu-id="2476c-121">More control over scaling, as you control when and how much to scale.</span></span>

## <a name="enable-auto-inflate-on-a-namespace"></a><span data-ttu-id="2476c-122">Включение автоматического расширения в пространстве имен</span><span class="sxs-lookup"><span data-stu-id="2476c-122">Enable Auto-inflate on a namespace</span></span>

<span data-ttu-id="2476c-123">Вы можете включать или отключать автоматическое расширение в пространстве имен, используя один из следующих способов:</span><span class="sxs-lookup"><span data-stu-id="2476c-123">You can enable or disable Auto-inflate on a namespace using either of the following methods:</span></span>

1. <span data-ttu-id="2476c-124">[Портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2476c-124">The [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="2476c-125">Шаблон Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2476c-125">An Azure Resource Manager template.</span></span>

### <a name="enable-auto-inflate-through-the-portal"></a><span data-ttu-id="2476c-126">Включение автоматического расширения на портале</span><span class="sxs-lookup"><span data-stu-id="2476c-126">Enable Auto-inflate through the portal</span></span>

<span data-ttu-id="2476c-127">Вы можете включить функцию автоматического расширения в пространстве имен при создании пространства имен концентраторов событий:</span><span class="sxs-lookup"><span data-stu-id="2476c-127">You can enable the Auto-inflate feature on a namespace when creating an Event Hubs namespace:</span></span>
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate1.png)

<span data-ttu-id="2476c-128">Если этот параметр включен, можно начать с малого числа единиц пропускной способности и повышать его по мере роста потребностей использования.</span><span class="sxs-lookup"><span data-stu-id="2476c-128">With this option enabled, you can start small on your throughput units and scale up as your usage needs increase.</span></span> <span data-ttu-id="2476c-129">Верхний предел для расширения не влияет на цены, которые зависят от числа единиц пропускной способности, используемых в час.</span><span class="sxs-lookup"><span data-stu-id="2476c-129">The upper limit for inflation does not affect pricing, which depends on the number of TUs used per hour.</span></span>

<span data-ttu-id="2476c-130">Вы также можете включить автоматическое расширение с помощью параметра **Scale** (Масштабировать) в колонке параметров на портале:</span><span class="sxs-lookup"><span data-stu-id="2476c-130">You can also enable Auto-inflate using the **Scale** option on the settings blade in the portal:</span></span>
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate2.png)

### <a name="enable-auto-inflate-using-an-azure-resource-manager-template"></a><span data-ttu-id="2476c-131">Включение автоматического расширения с помощью шаблона Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2476c-131">Enable Auto-Inflate using an Azure Resource Manager template</span></span>

<span data-ttu-id="2476c-132">Вы можете включить автоматическое расширение во время развертывания шаблона Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2476c-132">You can enable Auto-inflate during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="2476c-133">Например, задайте для свойства `isAutoInflateEnabled` значение **true** и установите для `maximumThroughputUnits` значение 10.</span><span class="sxs-lookup"><span data-stu-id="2476c-133">For example, set the `isAutoInflateEnabled` property to **true** and set `maximumThroughputUnits` to 10.</span></span>

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

<span data-ttu-id="2476c-134">Полный шаблон см. в разделе [Создание пространства имен концентраторов событий и включение расширения](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="2476c-134">For the complete template, see the [Create Event Hubs namespace and enable inflate](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) template on GitHub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2476c-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2476c-135">Next steps</span></span>

<span data-ttu-id="2476c-136">Дополнительные сведения о концентраторах событий см. в следующих источниках:</span><span class="sxs-lookup"><span data-stu-id="2476c-136">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="2476c-137">Обзор концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="2476c-137">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="2476c-138">Создание концентратора событий</span><span class="sxs-lookup"><span data-stu-id="2476c-138">Create an Event Hub</span></span>](event-hubs-create.md)
