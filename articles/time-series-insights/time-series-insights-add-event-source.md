---
title: "aaaAdd tooyour Azure Insights ряда времени событий исходной среды | Документы Microsoft"
description: "В этом учебнике подключения tooyour аналитики ряда времени событий исходной среды"
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
ms.openlocfilehash: 817df5e81cb4dc3d7376914a4651aabebadbcc32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-source-for-your-time-series-insights-environment-using-hello-ibiza-portal"></a><span data-ttu-id="0d027-103">Создать источник событий для среды времени серии аналитики портале Ibiza hello</span><span class="sxs-lookup"><span data-stu-id="0d027-103">Create an event source for your Time Series Insights environment using hello Ibiza portal</span></span>

<span data-ttu-id="0d027-104">Источник событий Time Series Insights является производным от брокеров событий, таких как концентраторы событий Azure.</span><span class="sxs-lookup"><span data-stu-id="0d027-104">Time Series Insights Event Source is derived from an event broker, like Azure Event Hubs.</span></span> <span data-ttu-id="0d027-105">Аналитики ряда времени непосредственно подключается tooEvent источников, передаче потока данных hello без необходимости toowrite пользователей одной строки кода.</span><span class="sxs-lookup"><span data-stu-id="0d027-105">Time Series Insights connects directly tooEvent Sources, ingesting hello data stream without requiring users toowrite a single line of code.</span></span> <span data-ttu-id="0d027-106">Сейчас Time Series Insights поддерживает концентраторы событий Azure и Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="0d027-106">Currently, Time Series Insights supports Azure Event Hubs and Azure IoT Hubs.</span></span> <span data-ttu-id="0d027-107">Дополнительные источники событий будет добавлена в будущем hello.</span><span class="sxs-lookup"><span data-stu-id="0d027-107">In hello future, more Event Sources will be added.</span></span>

## <a name="steps-tooadd-an-event-source-tooyour-environment"></a><span data-ttu-id="0d027-108">Действия tooadd среды tooyour источника событий</span><span class="sxs-lookup"><span data-stu-id="0d027-108">Steps tooadd an event source tooyour environment</span></span>

1.  <span data-ttu-id="0d027-109">Войдите в toohello [портал Ibiza](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0d027-109">Sign in toohello [Ibiza portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="0d027-110">Выберите «Все ресурсы» в меню hello hello левой части портала Ibiza hello.</span><span class="sxs-lookup"><span data-stu-id="0d027-110">Click “All resources” in hello menu on hello left side of hello Ibiza portal.</span></span>
3.  <span data-ttu-id="0d027-111">Выберите среду Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="0d027-111">Select your Time Series Insights environment.</span></span>

  ![Создать источник событий аналитики ряда времени hello](media/add-event-source/getstarted-create-event-source-1.png)

4.  <span data-ttu-id="0d027-113">Выберите "Источники событий" и щелкните "+ Добавить".</span><span class="sxs-lookup"><span data-stu-id="0d027-113">Select “Event Sources”, click “+ Add.”</span></span>

  ![Создать источник событий аналитики ряда времени hello - подробные сведения](media/add-event-source/getstarted-create-event-source-2.png)

5.  <span data-ttu-id="0d027-115">Укажите имя источника события hello hello.</span><span class="sxs-lookup"><span data-stu-id="0d027-115">Specify hello name of hello event source.</span></span> <span data-ttu-id="0d027-116">Это имя связано со всеми событиями из источника событий. Оно доступно во время выполнения запроса.</span><span class="sxs-lookup"><span data-stu-id="0d027-116">This name is associated with all events coming from this event source and is available at query time.</span></span>
6.  <span data-ttu-id="0d027-117">Выберите концентратор событий из списка hello ресурсов концентратора событий в текущей подписке hello.</span><span class="sxs-lookup"><span data-stu-id="0d027-117">Select an event hub from hello list of Event Hub resources in hello current subscription.</span></span> <span data-ttu-id="0d027-118">В противном случае выберите параметр импорта «параметры укажите концентратора событий вручную» toospecify концентратор событий в другую подписку.</span><span class="sxs-lookup"><span data-stu-id="0d027-118">Otherwise choose import option "Provide Event Hub settings manually” toospecify an event hub in another subscription.</span></span> <span data-ttu-id="0d027-119">События должны быть опубликованы в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="0d027-119">Events must be published in JSON format.</span></span>
7.  <span data-ttu-id="0d027-120">Выберите политику, которая разрешение чтения в концентратор событий hello.</span><span class="sxs-lookup"><span data-stu-id="0d027-120">Select policy that has read permission in hello event hub.</span></span>
8.  <span data-ttu-id="0d027-121">Укажите концентратор событий или группу потребителей.</span><span class="sxs-lookup"><span data-stu-id="0d027-121">Specify event hub consumer group.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="0d027-122">Убедитесь, что эта группа потребителей не используется другой службой (например, заданием Stream Analytics или другой средой Time Series Insights).</span><span class="sxs-lookup"><span data-stu-id="0d027-122">Make sure this consumer group is not used by any other service (such as Stream Analytics job or another Time Series Insights environment).</span></span> <span data-ttu-id="0d027-123">Если группа потребителей используется другими службами, считать операции отрицательно влияет для этой среды и hello других служб.</span><span class="sxs-lookup"><span data-stu-id="0d027-123">If consumer group is used by other services, read operation is negatively affected for this environment and hello other services.</span></span> <span data-ttu-id="0d027-124">При использовании как hello группа потребителей «$Default» может привести toopotential повторного использования другими пользователями.</span><span class="sxs-lookup"><span data-stu-id="0d027-124">If you are using “$Default” as hello consumer group, it could lead toopotential reuse by other readers.</span></span>

9.  <span data-ttu-id="0d027-125">Щелкните "Создать".</span><span class="sxs-lookup"><span data-stu-id="0d027-125">Click “Create.”</span></span>

<span data-ttu-id="0d027-126">После создания источника событий hello аналитики ряда времени с автоматическим запуском потоковой передачи данных в вашей среде.</span><span class="sxs-lookup"><span data-stu-id="0d027-126">After creation of hello event source, Time Series Insights will automatically start streaming data into your environment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d027-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0d027-127">Next steps</span></span>

* <span data-ttu-id="0d027-128">[Отправлять события](time-series-insights-send-events.md) toohello источник события</span><span class="sxs-lookup"><span data-stu-id="0d027-128">[Send events](time-series-insights-send-events.md) toohello event source</span></span>
* <span data-ttu-id="0d027-129">Просмотрите свою среду на [портале Time Series Insights](https://insights.timeseries.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0d027-129">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
