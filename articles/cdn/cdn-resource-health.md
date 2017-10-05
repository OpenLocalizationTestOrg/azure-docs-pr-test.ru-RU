---
title: "Отслеживание работоспособности ресурсов Azure CDN | Документация Майкрософт"
description: "Узнайте, как отслеживать состояние ресурсов Azure CDN с помощью службы работоспособности ресурсов Azure."
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
ms.openlocfilehash: 37fe208f5087f318e665e76825127854b4a11c98
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-the-health-of-azure-cdn-resources"></a><span data-ttu-id="78111-103">Отслеживание работоспособности ресурсов Azure CDN</span><span class="sxs-lookup"><span data-stu-id="78111-103">Monitor the health of Azure CDN resources</span></span>
  
<span data-ttu-id="78111-104">Работоспособность ресурсов Azure CDN — это составная часть службы [работоспособности ресурсов Azure](../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="78111-104">Azure CDN Resource health is a subset of [Azure resource health](../resource-health/resource-health-overview.md).</span></span>  <span data-ttu-id="78111-105">Службу работоспособности ресурсов Azure можно использовать для отслеживания состояния работоспособности ресурсов CDN и получения практических рекомендаций по устранению неполадок.</span><span class="sxs-lookup"><span data-stu-id="78111-105">You can use Azure resource health to monitor the health of CDN resources and receive actionable guidance to troubleshoot problems.</span></span>

>[!IMPORTANT] 
><span data-ttu-id="78111-106">Служба работоспособности ресурсов Azure CDN учитывает состояние работоспособности глобальной доставки по сети CDN и возможностей интерфейса API.</span><span class="sxs-lookup"><span data-stu-id="78111-106">Azure CDN resource health only currently accounts for the health of global CDN delivery and API capabilities.</span></span>  <span data-ttu-id="78111-107">Она не проверяет отдельные конечные точки CDN.</span><span class="sxs-lookup"><span data-stu-id="78111-107">Azure CDN resource health does not verify individual CDN endpoints.</span></span>
>
><span data-ttu-id="78111-108">Сигналы, на которые полагается служба работоспособности ресурсов Azure CDN, могут быть отложены на период до 15 минут.</span><span class="sxs-lookup"><span data-stu-id="78111-108">The signals that feed Azure CDN resource health may be up to 15 minutes delayed.</span></span>

## <a name="how-to-find-azure-cdn-resource-health"></a><span data-ttu-id="78111-109">Как найти службу работоспособности ресурсов Azure CDN?</span><span class="sxs-lookup"><span data-stu-id="78111-109">How to find Azure CDN resource health</span></span>

1. <span data-ttu-id="78111-110">На [портале Azure](https://portal.azure.com) перейдите к профилю CDN.</span><span class="sxs-lookup"><span data-stu-id="78111-110">In the [Azure portal](https://portal.azure.com), browse to your CDN profile.</span></span>

2. <span data-ttu-id="78111-111">Нажмите кнопку **Параметры** .</span><span class="sxs-lookup"><span data-stu-id="78111-111">Click the **Settings** button.</span></span>

    ![Кнопка "Параметры"](./media/cdn-resource-health/cdn-profile-settings.png)

3. <span data-ttu-id="78111-113">В разделе *Поддержка и устранение неполадок*, щелкните **Работоспособность ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="78111-113">Under *Support + troubleshooting*, click **Resource health**.</span></span>

    ![Работоспособность ресурсов CDN](./media/cdn-resource-health/cdn-resource-health3.png)

>[!TIP] 
><span data-ttu-id="78111-115">Вы также можете найти ресурсы CDN в виде списка в элементе *Работоспособность ресурсов* в колонке *Справка и поддержка*.</span><span class="sxs-lookup"><span data-stu-id="78111-115">You can also find CDN resources listed in the *Resource health* tile in the *Help + support* blade.</span></span>  <span data-ttu-id="78111-116">Можно быстро перейти к колонке *Справка и поддержка*, щелкнув обведенный значок **?**</span><span class="sxs-lookup"><span data-stu-id="78111-116">You can quickly get to *Help + support* by clicking the circled **?**</span></span> <span data-ttu-id="78111-117">в правом верхнем углу портала.</span><span class="sxs-lookup"><span data-stu-id="78111-117">in the upper right corner of the portal.</span></span>
>
> ![Справка + поддержка](./media/cdn-resource-health/cdn-help-support.png)

## <a name="azure-cdn-specific-messages"></a><span data-ttu-id="78111-119">Сообщения, относящиеся к Azure CDN</span><span class="sxs-lookup"><span data-stu-id="78111-119">Azure CDN-specific messages</span></span>

<span data-ttu-id="78111-120">Состояния, связанные с работоспособностью ресурсов Azure CDN, перечислены ниже.</span><span class="sxs-lookup"><span data-stu-id="78111-120">Statuses related to Azure CDN resource health can be found below.</span></span>

|<span data-ttu-id="78111-121">Сообщение</span><span class="sxs-lookup"><span data-stu-id="78111-121">Message</span></span> | <span data-ttu-id="78111-122">Рекомендуемое действие</span><span class="sxs-lookup"><span data-stu-id="78111-122">Recommended Action</span></span> |
|---|---|
|<span data-ttu-id="78111-123">Возможно, вы остановили, удалили или неправильно настроили одну конечную точку CDN или несколько.</span><span class="sxs-lookup"><span data-stu-id="78111-123">You may have stopped, removed, or misconfigured one or more of your CDN endpoints</span></span> | <span data-ttu-id="78111-124">Возможно, вы остановили, удалили или неправильно настроили одну конечную точку CDN или несколько.</span><span class="sxs-lookup"><span data-stu-id="78111-124">You may have stopped, removed, or misconfigured one or more of your CDN endpoints.</span></span>|
|<span data-ttu-id="78111-125">К сожалению, служба управления CDN сейчас недоступна.</span><span class="sxs-lookup"><span data-stu-id="78111-125">We are sorry, the CDN management service is currently unavailable</span></span> | <span data-ttu-id="78111-126">Обновления состояния см. здесь позже. Если проблему не удается устранить спустя ожидаемый период времени, обратитесь в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="78111-126">Check back here for status updates; If your problem persists after the expected resolution time, contact support.</span></span>|
|<span data-ttu-id="78111-127">К сожалению, неустраненные проблемы с некоторыми поставщиками CDN могут влиять на ваши конечные точки CDN.</span><span class="sxs-lookup"><span data-stu-id="78111-127">We're sorry, your CDN endpoints may be impacted by ongoing issues with some of our CDN providers</span></span> | <span data-ttu-id="78111-128">Обновления состояния см. здесь позже. Используйте средство устранения проблем, чтобы узнать, как проверить источник и конечную точку CDN. Если проблему не удается устранить спустя ожидаемый период времени, обратитесь в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="78111-128">Check back here for status updates; Use the Troubleshoot tool to learn how to test your origin and CDN endpoint; If your problem persists after the expected resolution time, contact support.</span></span> |
|<span data-ttu-id="78111-129">К сожалению, во время изменения конфигурации конечных точек CDN возникли задержки при распространении данных.</span><span class="sxs-lookup"><span data-stu-id="78111-129">We're sorry, CDN endpoint configuration changes are experiencing propagation delays</span></span> | <span data-ttu-id="78111-130">Обновления состояния см. здесь позже. Если изменения конфигурации не полностью распространены в ожидаемый период времени, обратитесь в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="78111-130">Check back here for status updates; If your configuration changes are not fully propagated in the expected time, contact support.</span></span>|
|<span data-ttu-id="78111-131">К сожалению, возникли проблемы при загрузке вспомогательного портала.</span><span class="sxs-lookup"><span data-stu-id="78111-131">We're sorry, we are experiencing issues loading the supplemental portal</span></span> | <span data-ttu-id="78111-132">Обновления состояния см. здесь позже. Если проблему не удается устранить спустя ожидаемый период времени, обратитесь в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="78111-132">Check back here for status updates; If your problem persists after the expected resolution time, contact support.</span></span>|
<span data-ttu-id="78111-133">К сожалению, возникли проблемы с некоторыми поставщиками CDN.</span><span class="sxs-lookup"><span data-stu-id="78111-133">We are sorry, we are experiencing issues with some of our CDN providers</span></span> | <span data-ttu-id="78111-134">Обновления состояния см. здесь позже. Если проблему не удается устранить спустя ожидаемый период времени, обратитесь в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="78111-134">Check back here for status updates; If your problem persists after the expected resolution time, contact support.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="78111-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="78111-135">Next steps</span></span>

- <span data-ttu-id="78111-136">[Ознакомьтесь с обзором службы работоспособности ресурсов Azure](../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="78111-136">[Read an overview of Azure resource health](../resource-health/resource-health-overview.md)</span></span>
- <span data-ttu-id="78111-137">[Узнайте, как устранить неполадки со сжатием CDN](./cdn-troubleshoot-compression.md).</span><span class="sxs-lookup"><span data-stu-id="78111-137">[Troubleshoot issues with CDN compression](./cdn-troubleshoot-compression.md)</span></span>
- <span data-ttu-id="78111-138">[Узнайте, как устранить ошибки 404](./cdn-troubleshoot-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="78111-138">[Troubleshoot issues with 404 errors](./cdn-troubleshoot-endpoint.md)</span></span>