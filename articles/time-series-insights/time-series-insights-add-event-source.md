---
title: "Добавление источника событий в среду Azure Time Series Insights | Документация Майкрософт"
description: "Это руководство содержит сведения о подключении источника событий к среде Time Series Insights"
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: santoshb
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: omravi
ms.openlocfilehash: ffa2eaf3680e68ac14aabf49b6308caeb173fd43
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-event-source-for-your-time-series-insights-environment-using-the-ibiza-portal"></a><span data-ttu-id="e9996-103">Создание источника событий для среды Time Series Insights с помощью портала Ibiza</span><span class="sxs-lookup"><span data-stu-id="e9996-103">Create an event source for your Time Series Insights environment using the Ibiza portal</span></span>

<span data-ttu-id="e9996-104">Источник событий Time Series Insights является производным от брокеров событий, таких как концентраторы событий Azure.</span><span class="sxs-lookup"><span data-stu-id="e9996-104">Time Series Insights Event Source is derived from an event broker, like Azure Event Hubs.</span></span> <span data-ttu-id="e9996-105">Time Series Insights подключаются напрямую к источникам событий, принимая поток данных, при этом у пользователей нет необходимости писать код.</span><span class="sxs-lookup"><span data-stu-id="e9996-105">Time Series Insights connects directly to Event Sources, ingesting the data stream without requiring users to write a single line of code.</span></span> <span data-ttu-id="e9996-106">Сейчас Time Series Insights поддерживает концентраторы событий Azure и Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="e9996-106">Currently, Time Series Insights supports Azure Event Hubs and Azure IoT Hubs.</span></span> <span data-ttu-id="e9996-107">В дальнейшем будут добавлены дополнительные источники событий.</span><span class="sxs-lookup"><span data-stu-id="e9996-107">In the future, more Event Sources will be added.</span></span>

## <a name="steps-to-add-an-event-source-to-your-environment"></a><span data-ttu-id="e9996-108">Процедура добавления источника событий в среду</span><span class="sxs-lookup"><span data-stu-id="e9996-108">Steps to add an event source to your environment</span></span>

1.  <span data-ttu-id="e9996-109">Войдите на [портал Ibiza](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e9996-109">Sign in to the [Ibiza portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="e9996-110">В меню слева на портале Ibiza щелкните "Все ресурсы".</span><span class="sxs-lookup"><span data-stu-id="e9996-110">Click “All resources” in the menu on the left side of the Ibiza portal.</span></span>
3.  <span data-ttu-id="e9996-111">Выберите среду Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="e9996-111">Select your Time Series Insights environment.</span></span>

  ![Создание источника событий Time Series Insights](media/add-event-source/getstarted-create-event-source-1.png)

4.  <span data-ttu-id="e9996-113">Выберите "Источники событий" и щелкните "+ Добавить".</span><span class="sxs-lookup"><span data-stu-id="e9996-113">Select “Event Sources”, click “+ Add.”</span></span>

  ![Создание источника событий Time Series Insights — сведения](media/add-event-source/getstarted-create-event-source-2.png)

5.  <span data-ttu-id="e9996-115">Укажите имя источника событий.</span><span class="sxs-lookup"><span data-stu-id="e9996-115">Specify the name of the event source.</span></span> <span data-ttu-id="e9996-116">Это имя связано со всеми событиями из источника событий. Оно доступно во время выполнения запроса.</span><span class="sxs-lookup"><span data-stu-id="e9996-116">This name is associated with all events coming from this event source and is available at query time.</span></span>
6.  <span data-ttu-id="e9996-117">Выберите концентратор событий в списке ресурсов концентратора событий в текущей подписке.</span><span class="sxs-lookup"><span data-stu-id="e9996-117">Select an event hub from the list of Event Hub resources in the current subscription.</span></span> <span data-ttu-id="e9996-118">В противном случае выберите параметр импорта "Указать параметры концентратора событий вручную", чтобы выбрать концентратор событий в другой подписке.</span><span class="sxs-lookup"><span data-stu-id="e9996-118">Otherwise choose import option "Provide Event Hub settings manually” to specify an event hub in another subscription.</span></span> <span data-ttu-id="e9996-119">События должны быть опубликованы в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="e9996-119">Events must be published in JSON format.</span></span>
7.  <span data-ttu-id="e9996-120">Выберите политику с разрешением на чтение в концентраторе событий.</span><span class="sxs-lookup"><span data-stu-id="e9996-120">Select policy that has read permission in the event hub.</span></span>
8.  <span data-ttu-id="e9996-121">Укажите концентратор событий или группу потребителей.</span><span class="sxs-lookup"><span data-stu-id="e9996-121">Specify event hub consumer group.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="e9996-122">Убедитесь, что эта группа потребителей не используется другой службой (например, заданием Stream Analytics или другой средой Time Series Insights).</span><span class="sxs-lookup"><span data-stu-id="e9996-122">Make sure this consumer group is not used by any other service (such as Stream Analytics job or another Time Series Insights environment).</span></span> <span data-ttu-id="e9996-123">Если группа потребителей используется другими службами, это негативно скажется на операции чтения в этой среде и в других службах.</span><span class="sxs-lookup"><span data-stu-id="e9996-123">If consumer group is used by other services, read operation is negatively affected for this environment and the other services.</span></span> <span data-ttu-id="e9996-124">Использование $Default в качестве группы потребителей может потенциально привести к ее повторному использованию другими читателями.</span><span class="sxs-lookup"><span data-stu-id="e9996-124">If you are using “$Default” as the consumer group, it could lead to potential reuse by other readers.</span></span>

9.  <span data-ttu-id="e9996-125">Щелкните "Создать".</span><span class="sxs-lookup"><span data-stu-id="e9996-125">Click “Create.”</span></span>

<span data-ttu-id="e9996-126">После создания источника событий Time Series Insights автоматически запустит передачу данных в среду.</span><span class="sxs-lookup"><span data-stu-id="e9996-126">After creation of the event source, Time Series Insights will automatically start streaming data into your environment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e9996-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e9996-127">Next steps</span></span>

* <span data-ttu-id="e9996-128">[Отправьте события](time-series-insights-send-events.md) в источник событий.</span><span class="sxs-lookup"><span data-stu-id="e9996-128">[Send events](time-series-insights-send-events.md) to the event source</span></span>
* <span data-ttu-id="e9996-129">Просмотрите свою среду на [портале Time Series Insights](https://insights.timeseries.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e9996-129">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
