---
title: "aaaMonitor hello работоспособности ресурсов Azure CDN | Документы Microsoft"
description: "Узнайте, как toomonitor hello работоспособности ресурсов Azure CDN с помощью исправности ресурсов Azure."
services: cdn
documentationcenter: .net
author: zhangmanling
manager: zhangmanling
editor: 
ms.assetid: bf23bd89-35b2-4aca-ac7f-68ee02953f31
ms.service: cdn
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 0a77e56d2fecae4bde6c83730c05375853a6638a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-hello-health-of-azure-cdn-resources"></a><span data-ttu-id="56aea-103">Монитор работоспособности hello ресурсов Azure CDN</span><span class="sxs-lookup"><span data-stu-id="56aea-103">Monitor hello health of Azure CDN resources</span></span>
  
<span data-ttu-id="56aea-104">Работоспособность ресурсов Azure CDN — это составная часть службы [работоспособности ресурсов Azure](../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="56aea-104">Azure CDN Resource health is a subset of [Azure resource health](../resource-health/resource-health-overview.md).</span></span>  <span data-ttu-id="56aea-105">Можно использовать работоспособности hello toomonitor работоспособности ресурсов Azure CDN ресурсов и получения пригодных к использованию руководство tootroubleshoot проблем.</span><span class="sxs-lookup"><span data-stu-id="56aea-105">You can use Azure resource health toomonitor hello health of CDN resources and receive actionable guidance tootroubleshoot problems.</span></span>

>[!IMPORTANT] 
><span data-ttu-id="56aea-106">Исправности ресурсов Azure CDN в настоящее время только учетные записи для hello работоспособности международной доставки CDN и возможности API.</span><span class="sxs-lookup"><span data-stu-id="56aea-106">Azure CDN resource health only currently accounts for hello health of global CDN delivery and API capabilities.</span></span>  <span data-ttu-id="56aea-107">Она не проверяет отдельные конечные точки CDN.</span><span class="sxs-lookup"><span data-stu-id="56aea-107">Azure CDN resource health does not verify individual CDN endpoints.</span></span>
>
><span data-ttu-id="56aea-108">сигнализирует Hello канала исправности ресурсов Azure CDN может быть активным too15 минут отложено.</span><span class="sxs-lookup"><span data-stu-id="56aea-108">hello signals that feed Azure CDN resource health may be up too15 minutes delayed.</span></span>

## <a name="how-toofind-azure-cdn-resource-health"></a><span data-ttu-id="56aea-109">Как toofind исправности ресурсов Azure CDN</span><span class="sxs-lookup"><span data-stu-id="56aea-109">How toofind Azure CDN resource health</span></span>

1. <span data-ttu-id="56aea-110">В hello [портал Azure](https://portal.azure.com), Обзор профиля CDN tooyour.</span><span class="sxs-lookup"><span data-stu-id="56aea-110">In hello [Azure portal](https://portal.azure.com), browse tooyour CDN profile.</span></span>

2. <span data-ttu-id="56aea-111">Нажмите кнопку hello **параметры** кнопки.</span><span class="sxs-lookup"><span data-stu-id="56aea-111">Click hello **Settings** button.</span></span>

    ![Кнопка "Параметры"](./media/cdn-resource-health/cdn-profile-settings.png)

3. <span data-ttu-id="56aea-113">В разделе *Поддержка и устранение неполадок*, щелкните **Работоспособность ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="56aea-113">Under *Support + troubleshooting*, click **Resource health**.</span></span>

    ![Работоспособность ресурсов CDN](./media/cdn-resource-health/cdn-resource-health3.png)

>[!TIP] 
><span data-ttu-id="56aea-115">Можно также найти CDN ресурсах, перечисленных в hello *исправности ресурсов* плитки в hello *Справка и поддержка* колонку.</span><span class="sxs-lookup"><span data-stu-id="56aea-115">You can also find CDN resources listed in hello *Resource health* tile in hello *Help + support* blade.</span></span>  <span data-ttu-id="56aea-116">Вы можете быстро получить слишком*Справка и поддержка* , щелкнув hello обведен **?**</span><span class="sxs-lookup"><span data-stu-id="56aea-116">You can quickly get too*Help + support* by clicking hello circled **?**</span></span> <span data-ttu-id="56aea-117">hello верхний правый угол hello портала.</span><span class="sxs-lookup"><span data-stu-id="56aea-117">in hello upper right corner of hello portal.</span></span>
>
> ![Справка + поддержка](./media/cdn-resource-health/cdn-help-support.png)

## <a name="azure-cdn-specific-messages"></a><span data-ttu-id="56aea-119">Сообщения, относящиеся к Azure CDN</span><span class="sxs-lookup"><span data-stu-id="56aea-119">Azure CDN-specific messages</span></span>

<span data-ttu-id="56aea-120">Ниже можно найти исправности ресурсов CDN связанные tooAzure состояния.</span><span class="sxs-lookup"><span data-stu-id="56aea-120">Statuses related tooAzure CDN resource health can be found below.</span></span>

|<span data-ttu-id="56aea-121">Сообщение</span><span class="sxs-lookup"><span data-stu-id="56aea-121">Message</span></span> | <span data-ttu-id="56aea-122">Рекомендуемое действие</span><span class="sxs-lookup"><span data-stu-id="56aea-122">Recommended Action</span></span> |
|---|---|
|<span data-ttu-id="56aea-123">Возможно, вы остановили, удалили или неправильно настроили одну конечную точку CDN или несколько.</span><span class="sxs-lookup"><span data-stu-id="56aea-123">You may have stopped, removed, or misconfigured one or more of your CDN endpoints</span></span> | <span data-ttu-id="56aea-124">Возможно, вы остановили, удалили или неправильно настроили одну конечную точку CDN или несколько.</span><span class="sxs-lookup"><span data-stu-id="56aea-124">You may have stopped, removed, or misconfigured one or more of your CDN endpoints.</span></span>|
|<span data-ttu-id="56aea-125">К сожалению, hello службы управления CDN в настоящее время недоступна</span><span class="sxs-lookup"><span data-stu-id="56aea-125">We are sorry, hello CDN management service is currently unavailable</span></span> | <span data-ttu-id="56aea-126">Следите за состоянием обновления. Hello ожидаемое время разрешения не помогли устранить проблему, обратитесь в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="56aea-126">Check back here for status updates; If your problem persists after hello expected resolution time, contact support.</span></span>|
|<span data-ttu-id="56aea-127">К сожалению, неустраненные проблемы с некоторыми поставщиками CDN могут влиять на ваши конечные точки CDN.</span><span class="sxs-lookup"><span data-stu-id="56aea-127">We're sorry, your CDN endpoints may be impacted by ongoing issues with some of our CDN providers</span></span> | <span data-ttu-id="56aea-128">Следите за состоянием обновления. Как использовать средство toolearn hello Устранение tootest исходной и конечной точки CDN; Hello ожидаемое время разрешения не помогли устранить проблему, обратитесь в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="56aea-128">Check back here for status updates; Use hello Troubleshoot tool toolearn how tootest your origin and CDN endpoint; If your problem persists after hello expected resolution time, contact support.</span></span> |
|<span data-ttu-id="56aea-129">К сожалению, во время изменения конфигурации конечных точек CDN возникли задержки при распространении данных.</span><span class="sxs-lookup"><span data-stu-id="56aea-129">We're sorry, CDN endpoint configuration changes are experiencing propagation delays</span></span> | <span data-ttu-id="56aea-130">Следите за состоянием обновления. Изменения конфигурации не распространяются полностью hello ожидаемого времени, обратитесь в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="56aea-130">Check back here for status updates; If your configuration changes are not fully propagated in hello expected time, contact support.</span></span>|
|<span data-ttu-id="56aea-131">К сожалению, возникли проблемы при загрузке дополнительный портал hello</span><span class="sxs-lookup"><span data-stu-id="56aea-131">We're sorry, we are experiencing issues loading hello supplemental portal</span></span> | <span data-ttu-id="56aea-132">Следите за состоянием обновления. Hello ожидаемое время разрешения не помогли устранить проблему, обратитесь в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="56aea-132">Check back here for status updates; If your problem persists after hello expected resolution time, contact support.</span></span>|
<span data-ttu-id="56aea-133">К сожалению, возникли проблемы с некоторыми поставщиками CDN.</span><span class="sxs-lookup"><span data-stu-id="56aea-133">We are sorry, we are experiencing issues with some of our CDN providers</span></span> | <span data-ttu-id="56aea-134">Следите за состоянием обновления. Hello ожидаемое время разрешения не помогли устранить проблему, обратитесь в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="56aea-134">Check back here for status updates; If your problem persists after hello expected resolution time, contact support.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="56aea-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="56aea-135">Next steps</span></span>

- <span data-ttu-id="56aea-136">[Ознакомьтесь с обзором службы работоспособности ресурсов Azure](../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="56aea-136">[Read an overview of Azure resource health](../resource-health/resource-health-overview.md)</span></span>
- <span data-ttu-id="56aea-137">[Узнайте, как устранить неполадки со сжатием CDN](./cdn-troubleshoot-compression.md).</span><span class="sxs-lookup"><span data-stu-id="56aea-137">[Troubleshoot issues with CDN compression](./cdn-troubleshoot-compression.md)</span></span>
- <span data-ttu-id="56aea-138">[Узнайте, как устранить ошибки 404](./cdn-troubleshoot-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="56aea-138">[Troubleshoot issues with 404 errors](./cdn-troubleshoot-endpoint.md)</span></span>