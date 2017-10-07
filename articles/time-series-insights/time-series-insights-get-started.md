---
title: "aaaCreate среды аналитики ряда времени Azure | Документы Microsoft"
description: "В этом учебнике вы узнаете, как toocreate среды рядов, подключите его источник события tooan и готов tooanalyze данные события в минутах."
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
ms.openlocfilehash: 7120fc9a6e4d4a4972f8cb37e4d9945cfb746fd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-new-time-series-insights-environment-in-hello-azure-portal"></a><span data-ttu-id="79dc2-103">Создание новой среды времени серии аналитики в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="79dc2-103">Create a new Time Series Insights environment in hello Azure portal</span></span>

<span data-ttu-id="79dc2-104">Time Series Insights — это ресурс Azure с входящим трафиком и объемом хранилища.</span><span class="sxs-lookup"><span data-stu-id="79dc2-104">Time Series Insights environment is an Azure resource with ingress and storage capacity.</span></span> <span data-ttu-id="79dc2-105">Клиенты предоставить средах через портал Azure hello hello требуется емкость.</span><span class="sxs-lookup"><span data-stu-id="79dc2-105">Customers provision environments via hello Azure portal with hello required capacity.</span></span>

## <a name="steps-toocreate-hello-environment"></a><span data-ttu-id="79dc2-106">Действия toocreate hello среды</span><span class="sxs-lookup"><span data-stu-id="79dc2-106">Steps toocreate hello environment</span></span>

<span data-ttu-id="79dc2-107">Выполните эти шаги toocreate вашей среде.</span><span class="sxs-lookup"><span data-stu-id="79dc2-107">Follow these steps toocreate your environment:</span></span>

1.  <span data-ttu-id="79dc2-108">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="79dc2-108">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="79dc2-109">Щелкните hello левому верхнему углу hello "плюс" («+»).</span><span class="sxs-lookup"><span data-stu-id="79dc2-109">Click hello plus sign (“+”) in hello top left corner.</span></span>
3.  <span data-ttu-id="79dc2-110">Найдите «Дополнительная информация ряда времени» в поле поиска hello.</span><span class="sxs-lookup"><span data-stu-id="79dc2-110">Search for “Time Series Insights” in hello search box.</span></span>

  ![Создание среды времени серии аналитики hello](media/get-started/getstarted-create-environment1.png)

4.  <span data-ttu-id="79dc2-112">Выберите Time Series Insights и щелкните "Создать".</span><span class="sxs-lookup"><span data-stu-id="79dc2-112">Select “Time Series Insights”, click “Create”.</span></span>

  ![Создать группу ресурсов аналитики ряда времени hello](media/get-started/getstarted-create-environment2.png)

5.  <span data-ttu-id="79dc2-114">Укажите имя среды,</span><span class="sxs-lookup"><span data-stu-id="79dc2-114">Specify environment name.</span></span> <span data-ttu-id="79dc2-115">Это имя будет представлять среды hello в [explorer ряда времени](https://insights.timeseries.azure.com).</span><span class="sxs-lookup"><span data-stu-id="79dc2-115">This name will represent hello environment in [time series explorer](https://insights.timeseries.azure.com).</span></span>
6.  <span data-ttu-id="79dc2-116">Выберите подписку.</span><span class="sxs-lookup"><span data-stu-id="79dc2-116">Select a subscription.</span></span> <span data-ttu-id="79dc2-117">Выберите подписку, содержащую источник событий.</span><span class="sxs-lookup"><span data-stu-id="79dc2-117">Choose one that contains your event source.</span></span> <span data-ttu-id="79dc2-118">Аналитики ряда времени можно автоматического обнаружения центр IoT Azure и ресурсы концентратора событий, существующих в hello одной подписке.</span><span class="sxs-lookup"><span data-stu-id="79dc2-118">Time Series Insights can auto-detect Azure IoT Hub and Event Hub resources existing in hello same subscription.</span></span>
7.  <span data-ttu-id="79dc2-119">Выберите или создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="79dc2-119">Select or create a resource group.</span></span> <span data-ttu-id="79dc2-120">Группы ресурсов — это набор совместно используемых ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="79dc2-120">A resource group is a collection of Azure resources used together.</span></span>
8.  <span data-ttu-id="79dc2-121">Выберите расположение для размещения.</span><span class="sxs-lookup"><span data-stu-id="79dc2-121">Select a hosting location.</span></span> <span data-ttu-id="79dc2-122">Центрирует tooavoid перемещения данных по данным, выберите папку, содержащую источник события.</span><span class="sxs-lookup"><span data-stu-id="79dc2-122">tooavoid moving data across data centers, choose location that contains your event source.</span></span>
9.  <span data-ttu-id="79dc2-123">Выберите ценовую категорию.</span><span class="sxs-lookup"><span data-stu-id="79dc2-123">Select a pricing tier.</span></span>
10. <span data-ttu-id="79dc2-124">Выберите емкость.</span><span class="sxs-lookup"><span data-stu-id="79dc2-124">Select capacity.</span></span> <span data-ttu-id="79dc2-125">Емкость среды можно изменить после ее создания.</span><span class="sxs-lookup"><span data-stu-id="79dc2-125">You can change capacity of an environment after creation.</span></span>
11. <span data-ttu-id="79dc2-126">Создайте среду.</span><span class="sxs-lookup"><span data-stu-id="79dc2-126">Create your environment.</span></span> <span data-ttu-id="79dc2-127">Панели мониторинга toohello среды для упрощения доступа можно также закрепить при каждом входе.</span><span class="sxs-lookup"><span data-stu-id="79dc2-127">You can also pin your environment toohello dashboard for easy access whenever you sign in.</span></span>

  ![Создание toodashboard ПИН-кода hello аналитики ряда времени](media/get-started/getstarted-create-environment3.png)

## <a name="next-steps"></a><span data-ttu-id="79dc2-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="79dc2-129">Next steps</span></span>

* <span data-ttu-id="79dc2-130">[Определить политики доступа данных](time-series-insights-data-access.md) tooaccess в вашей среде [портала аналитики ряда времени](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="79dc2-130">[Define data access policies](time-series-insights-data-access.md) tooaccess your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
* [<span data-ttu-id="79dc2-131">Создание источника событий</span><span class="sxs-lookup"><span data-stu-id="79dc2-131">Create an event source</span></span>](time-series-insights-add-event-source.md)
* <span data-ttu-id="79dc2-132">[Отправлять события](time-series-insights-send-events.md) toohello источник события</span><span class="sxs-lookup"><span data-stu-id="79dc2-132">[Send events](time-series-insights-send-events.md) toohello event source</span></span>
