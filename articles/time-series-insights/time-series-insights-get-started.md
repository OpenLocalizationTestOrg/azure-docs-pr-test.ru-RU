---
title: "Создание среды Azure Time Series Insights | Документация Майкрософт"
description: "Это руководство содержит сведения о создании среды Time Series, ее подключении к источнику событий и способы анализа данных событий за несколько минут."
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
ms.openlocfilehash: eb710795916a2d7beea75a6408a0982fb4dc8750
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-new-time-series-insights-environment-in-the-azure-portal"></a><span data-ttu-id="fb503-103">Создание среды Time Series Insights на портале Azure</span><span class="sxs-lookup"><span data-stu-id="fb503-103">Create a new Time Series Insights environment in the Azure portal</span></span>

<span data-ttu-id="fb503-104">Time Series Insights — это ресурс Azure с входящим трафиком и объемом хранилища.</span><span class="sxs-lookup"><span data-stu-id="fb503-104">Time Series Insights environment is an Azure resource with ingress and storage capacity.</span></span> <span data-ttu-id="fb503-105">Клиенты подготавливают среды через портал Azure, используя требуемую емкость.</span><span class="sxs-lookup"><span data-stu-id="fb503-105">Customers provision environments via the Azure portal with the required capacity.</span></span>

## <a name="steps-to-create-the-environment"></a><span data-ttu-id="fb503-106">Процедура создания среды</span><span class="sxs-lookup"><span data-stu-id="fb503-106">Steps to create the environment</span></span>

<span data-ttu-id="fb503-107">Чтобы создать среду, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="fb503-107">Follow these steps to create your environment:</span></span>

1.  <span data-ttu-id="fb503-108">Выполните вход на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fb503-108">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="fb503-109">Щелкните знак плюс ("+") в верхнем левом углу.</span><span class="sxs-lookup"><span data-stu-id="fb503-109">Click the plus sign (“+”) in the top left corner.</span></span>
3.  <span data-ttu-id="fb503-110">В поле поиска выполните поиск по запросу Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="fb503-110">Search for “Time Series Insights” in the search box.</span></span>

  ![Создание среды Time Series Insights](media/get-started/getstarted-create-environment1.png)

4.  <span data-ttu-id="fb503-112">Выберите Time Series Insights и щелкните "Создать".</span><span class="sxs-lookup"><span data-stu-id="fb503-112">Select “Time Series Insights”, click “Create”.</span></span>

  ![Создание группы ресурсов Time Series Insights](media/get-started/getstarted-create-environment2.png)

5.  <span data-ttu-id="fb503-114">Укажите имя среды,</span><span class="sxs-lookup"><span data-stu-id="fb503-114">Specify environment name.</span></span> <span data-ttu-id="fb503-115">которое будет представлять ее в [обозревателе Time Series](https://insights.timeseries.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fb503-115">This name will represent the environment in [time series explorer](https://insights.timeseries.azure.com).</span></span>
6.  <span data-ttu-id="fb503-116">Выберите подписку.</span><span class="sxs-lookup"><span data-stu-id="fb503-116">Select a subscription.</span></span> <span data-ttu-id="fb503-117">Выберите подписку, содержащую источник событий.</span><span class="sxs-lookup"><span data-stu-id="fb503-117">Choose one that contains your event source.</span></span> <span data-ttu-id="fb503-118">Time Series Insights может автоматически определить ресурсы Центра Интернета вещей и концентратора событий Azure в одной подписке.</span><span class="sxs-lookup"><span data-stu-id="fb503-118">Time Series Insights can auto-detect Azure IoT Hub and Event Hub resources existing in the same subscription.</span></span>
7.  <span data-ttu-id="fb503-119">Выберите или создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="fb503-119">Select or create a resource group.</span></span> <span data-ttu-id="fb503-120">Группы ресурсов — это набор совместно используемых ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="fb503-120">A resource group is a collection of Azure resources used together.</span></span>
8.  <span data-ttu-id="fb503-121">Выберите расположение для размещения.</span><span class="sxs-lookup"><span data-stu-id="fb503-121">Select a hosting location.</span></span> <span data-ttu-id="fb503-122">Чтобы не перемещать данные между центрами обработки данных, выберите расположение, содержащее источник событий.</span><span class="sxs-lookup"><span data-stu-id="fb503-122">To avoid moving data across data centers, choose location that contains your event source.</span></span>
9.  <span data-ttu-id="fb503-123">Выберите ценовую категорию.</span><span class="sxs-lookup"><span data-stu-id="fb503-123">Select a pricing tier.</span></span>
10. <span data-ttu-id="fb503-124">Выберите емкость.</span><span class="sxs-lookup"><span data-stu-id="fb503-124">Select capacity.</span></span> <span data-ttu-id="fb503-125">Емкость среды можно изменить после ее создания.</span><span class="sxs-lookup"><span data-stu-id="fb503-125">You can change capacity of an environment after creation.</span></span>
11. <span data-ttu-id="fb503-126">Создайте среду.</span><span class="sxs-lookup"><span data-stu-id="fb503-126">Create your environment.</span></span> <span data-ttu-id="fb503-127">Вы также можете закрепить среду на панели мониторинга, чтобы к ней можно было быстро обратиться после каждого входа в систему.</span><span class="sxs-lookup"><span data-stu-id="fb503-127">You can also pin your environment to the dashboard for easy access whenever you sign in.</span></span>

  ![Закрепление Time Series Insights на панели мониторинга](media/get-started/getstarted-create-environment3.png)

## <a name="next-steps"></a><span data-ttu-id="fb503-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fb503-129">Next steps</span></span>

* <span data-ttu-id="fb503-130">[Определите политики доступа к данным](time-series-insights-data-access.md), чтобы получить доступ к среде на [портале Time Series Insights](https://insights.timeseries.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fb503-130">[Define data access policies](time-series-insights-data-access.md) to access your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
* <span data-ttu-id="fb503-131">[Создайте источник событий](time-series-insights-add-event-source.md).</span><span class="sxs-lookup"><span data-stu-id="fb503-131">[Create an event source](time-series-insights-add-event-source.md)</span></span>
* <span data-ttu-id="fb503-132">[Отправьте события](time-series-insights-send-events.md) в источник событий.</span><span class="sxs-lookup"><span data-stu-id="fb503-132">[Send events](time-series-insights-send-events.md) to the event source</span></span>
