---
title: "Общие сведения об Azure Advisor | Документация Майкрософт"
description: "Использование Azure Advisor для оптимизации развернутых служб Azure."
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: 35678142550f9f887562f311a5e7d9516495cf53
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-azure-advisor"></a><span data-ttu-id="fa12b-103">Общие сведения об Azure Advisor</span><span class="sxs-lookup"><span data-stu-id="fa12b-103">Introduction to Azure Advisor</span></span>

<span data-ttu-id="fa12b-104">Узнайте о Помощнике по Azure и его основных возможностях, а также ознакомьтесь с ответами на часто задаваемые вопросы.</span><span class="sxs-lookup"><span data-stu-id="fa12b-104">Learn about Azure Advisor and its key capabilities, and get answers to frequently asked questions.</span></span>

## <a name="what-is-advisor"></a><span data-ttu-id="fa12b-105">Назначение Помощника</span><span class="sxs-lookup"><span data-stu-id="fa12b-105">What is Advisor?</span></span>
<span data-ttu-id="fa12b-106">Помощник по Azure — это персонализированный облачный консультант, который поможет следовать рекомендациям по оптимизации развернутых служб Azure.</span><span class="sxs-lookup"><span data-stu-id="fa12b-106">Advisor is a personalized cloud consultant that helps you follow best practices to optimize your Azure deployments.</span></span> <span data-ttu-id="fa12b-107">Он анализирует конфигурацию ресурсов и данные телеметрии их использования и рекомендует решения, которые помогут повысить эффективность затрат, производительность, уровень доступности и безопасности ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="fa12b-107">It analyzes your resource configuration and usage telemetry and then recommends solutions that can help you improve the cost effectiveness, performance, high availability, and security of your Azure resources.</span></span>

<span data-ttu-id="fa12b-108">С помощью Помощника можно:</span><span class="sxs-lookup"><span data-stu-id="fa12b-108">With Advisor, you can:</span></span>
* <span data-ttu-id="fa12b-109">получить упреждающие, действенные и персонализированные практические рекомендации;</span><span class="sxs-lookup"><span data-stu-id="fa12b-109">Get proactive, actionable, and personalized best practices recommendations.</span></span> 
* <span data-ttu-id="fa12b-110">повысить производительность, безопасность и уровень доступности ресурсов, выявляя при этом любые возможности сократить общие затраты на Azure;</span><span class="sxs-lookup"><span data-stu-id="fa12b-110">Improve the performance, security, and high availability of your resources, as you identify opportunities to reduce your overall Azure spend.</span></span>
* <span data-ttu-id="fa12b-111">получить рекомендации о доступных встроенных действиях.</span><span class="sxs-lookup"><span data-stu-id="fa12b-111">Get recommendations with proposed actions inline.</span></span>

<span data-ttu-id="fa12b-112">Воспользоваться Advisor можно с помощью [портала Azure](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="fa12b-112">You can access Advisor through the [Azure portal](https://aka.ms/azureadvisordashboard).</span></span> <span data-ttu-id="fa12b-113">Войдите на [портал](https://portal.azure.com), выберите **Обзор** и прокрутите экран до пункта **Помощник по Azure**.</span><span class="sxs-lookup"><span data-stu-id="fa12b-113">Sign in to the [portal](https://portal.azure.com), select **Browse**, and then scroll to **Azure Advisor**.</span></span> <span data-ttu-id="fa12b-114">Панель мониторинга Advisor отображает персонализированные рекомендации для выбранной подписки.</span><span class="sxs-lookup"><span data-stu-id="fa12b-114">The Advisor dashboard displays personalized recommendations for a selected subscription.</span></span> 

<span data-ttu-id="fa12b-115">Эти рекомендации разделены на четыре категории.</span><span class="sxs-lookup"><span data-stu-id="fa12b-115">The recommendations are divided into four categories:</span></span> 

* <span data-ttu-id="fa12b-116">**Высокий уровень доступности** — предназначены обеспечить и улучшить непрерывную работу критически важных бизнес-приложений.</span><span class="sxs-lookup"><span data-stu-id="fa12b-116">**High Availability**: To ensure and improve the continuity of your business-critical applications.</span></span> <span data-ttu-id="fa12b-117">Дополнительные сведения см. в разделе [Рекомендации Azure Advisor по высокой доступности](advisor-high-availability-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="fa12b-117">For more information, see [Advisor High Availability recommendations](advisor-high-availability-recommendations.md).</span></span>

* <span data-ttu-id="fa12b-118">**Безопасность** — предназначены для выявления угроз и уязвимостей, которые могут привести к нарушениям безопасности.</span><span class="sxs-lookup"><span data-stu-id="fa12b-118">**Security**: To detect threats and vulnerabilities that might lead to security breaches.</span></span> <span data-ttu-id="fa12b-119">Дополнительные сведения см. в разделе [Рекомендации Azure Advisor по безопасности](advisor-security-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="fa12b-119">For more information, see [Advisor Security recommendations](advisor-security-recommendations.md).</span></span>

* <span data-ttu-id="fa12b-120">**Производительность** — предназначены для повышения скорости работы ваших приложений.</span><span class="sxs-lookup"><span data-stu-id="fa12b-120">**Performance**: To improve the speed of your applications.</span></span> <span data-ttu-id="fa12b-121">Дополнительные сведения см. в разделе [Рекомендации Azure Advisor по производительности](advisor-performance-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="fa12b-121">For more information, see [Advisor Performance recommendations](advisor-performance-recommendations.md).</span></span>

* <span data-ttu-id="fa12b-122">**Стоимость** — предназначены оптимизировать и сократить общие издержки на Azure.</span><span class="sxs-lookup"><span data-stu-id="fa12b-122">**Cost**: To optimize and reduce your overall Azure spend.</span></span> <span data-ttu-id="fa12b-123">Дополнительные сведения см. в разделе [Рекомендации Azure Advisor по затратам](advisor-cost-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="fa12b-123">For more information, see [Advisor Cost recommendations](advisor-cost-recommendations.md).</span></span>

  ![Типы рекомендаций Advisor](./media/advisor-overview/advisor-all-tab-examples.png)

> [!NOTE]
> <span data-ttu-id="fa12b-125">Для доступа к рекомендациям Помощника необходимо сначала *зарегистрировать* в нем свою подписку.</span><span class="sxs-lookup"><span data-stu-id="fa12b-125">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="fa12b-126">Подписка регистрируется, когда *владелец подписки* открывает панель мониторинга Помощника и нажимает кнопку **Получить рекомендации**.</span><span class="sxs-lookup"><span data-stu-id="fa12b-126">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="fa12b-127">Выполнить данную *операцию достаточно всего один раз*.</span><span class="sxs-lookup"><span data-stu-id="fa12b-127">This is a *one-time operation*.</span></span> <span data-ttu-id="fa12b-128">После регистрации подписки рекомендации Помощника могут просматривать *владельцы*, *участники* или *читатели* подписки, группы ресурсов или конкретного ресурса.</span><span class="sxs-lookup"><span data-stu-id="fa12b-128">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

<span data-ttu-id="fa12b-129">Щелкните рекомендацию, чтобы узнать о ней больше.</span><span class="sxs-lookup"><span data-stu-id="fa12b-129">You can click a recommendation to learn more about it.</span></span> <span data-ttu-id="fa12b-130">Можно также узнать о действиях, которые можно выполнить, чтобы воспользоваться преимуществами предлагаемой возможности или устранить проблему.</span><span class="sxs-lookup"><span data-stu-id="fa12b-130">You can also learn about actions that you can perform to take advantage of an opportunity or resolve an issue.</span></span> 

<span data-ttu-id="fa12b-131">Advisor предлагает рекомендации со встроенными действиями и ссылками на документацию.</span><span class="sxs-lookup"><span data-stu-id="fa12b-131">Advisor offers recommendations with inline actions or documentation links.</span></span> <span data-ttu-id="fa12b-132">Щелкнув встроенное действие, можно ознакомиться с интерактивным руководством по его выполнению.</span><span class="sxs-lookup"><span data-stu-id="fa12b-132">Clicking an inline action takes you through a “guided user journey” to implement it.</span></span> <span data-ttu-id="fa12b-133">Щелкнув ссылку на документацию, можно ознакомиться с документацией, в которой описывается, как можно реализовать это действие вручную.</span><span class="sxs-lookup"><span data-stu-id="fa12b-133">Clicking a documentation link points you to documentation that describes how to manually implement the action.</span></span> 

<span data-ttu-id="fa12b-134">Помощник обновляет рекомендации ежечасно.</span><span class="sxs-lookup"><span data-stu-id="fa12b-134">Advisor updates recommendations hourly.</span></span> <span data-ttu-id="fa12b-135">Если вы не собираетесь немедленно реагировать на рекомендацию, можно отложить ее на определенное время или закрыть.</span><span class="sxs-lookup"><span data-stu-id="fa12b-135">If you don’t intend to take immediate action on a recommendation, you can snooze it for a specified time period or dismiss it.</span></span> 

## <a name="frequently-asked-questions"></a><span data-ttu-id="fa12b-136">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="fa12b-136">Frequently asked questions</span></span>

### <a name="how-do-i-access-advisor"></a><span data-ttu-id="fa12b-137">Как воспользоваться Advisor?</span><span class="sxs-lookup"><span data-stu-id="fa12b-137">How do I access Advisor?</span></span>
<span data-ttu-id="fa12b-138">Воспользоваться Advisor можно с помощью [портала Azure](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="fa12b-138">You can access Advisor through the [Azure portal](https://aka.ms/azureadvisordashboard).</span></span> <span data-ttu-id="fa12b-139">Войдите на [портал](https://portal.azure.com), выберите **Обзор** и прокрутите экран до пункта **Помощник по Azure**.</span><span class="sxs-lookup"><span data-stu-id="fa12b-139">Sign in to the [portal](https://portal.azure.com), select **Browse**, and then scroll to **Azure Advisor**.</span></span> <span data-ttu-id="fa12b-140">Панель мониторинга Advisor отображает персонализированные рекомендации для выбранной подписки.</span><span class="sxs-lookup"><span data-stu-id="fa12b-140">The Advisor dashboard displays personalized recommendations for a selected subscription.</span></span> 

<span data-ttu-id="fa12b-141">Рекомендации Advisor можно также просмотреть в колонке ресурса виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="fa12b-141">You can also view Advisor recommendations through the virtual machine resource blade.</span></span> <span data-ttu-id="fa12b-142">Выберите виртуальную машину и прокрутите меню до рекомендаций Advisor.</span><span class="sxs-lookup"><span data-stu-id="fa12b-142">Choose a virtual machine, and then scroll to Advisor recommendations in the menu.</span></span> 

### <a name="what-permissions-do-i-need-to-access-advisor"></a><span data-ttu-id="fa12b-143">Какие разрешения требуются для использования Advisor?</span><span class="sxs-lookup"><span data-stu-id="fa12b-143">What permissions do I need to access Advisor?</span></span>

<span data-ttu-id="fa12b-144">Для доступа к рекомендациям Помощника необходимо сначала *зарегистрировать* в нем свою подписку.</span><span class="sxs-lookup"><span data-stu-id="fa12b-144">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="fa12b-145">Подписка регистрируется, когда *владелец подписки* открывает панель мониторинга Помощника и нажимает кнопку **Получить рекомендации**.</span><span class="sxs-lookup"><span data-stu-id="fa12b-145">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="fa12b-146">Выполнить данную *операцию достаточно всего один раз*.</span><span class="sxs-lookup"><span data-stu-id="fa12b-146">This is a *one-time operation*.</span></span> <span data-ttu-id="fa12b-147">После регистрации подписки рекомендации Помощника могут просматривать *владельцы*, *участники* или *читатели* подписки, группы ресурсов или конкретного ресурса.</span><span class="sxs-lookup"><span data-stu-id="fa12b-147">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

### <a name="how-often-are-advisor-recommendations-updated"></a><span data-ttu-id="fa12b-148">Как часто обновляются рекомендации Advisor?</span><span class="sxs-lookup"><span data-stu-id="fa12b-148">How often are Advisor recommendations updated?</span></span>

<span data-ttu-id="fa12b-149">Помощник обновляет рекомендации каждый час.</span><span class="sxs-lookup"><span data-stu-id="fa12b-149">Advisor recommendations are updated hourly.</span></span>

### <a name="what-resources-does-advisor-provide-recommendations-for"></a><span data-ttu-id="fa12b-150">Для каких ресурсов Advisor предоставляет рекомендации?</span><span class="sxs-lookup"><span data-stu-id="fa12b-150">What resources does Advisor provide recommendations for?</span></span>

<span data-ttu-id="fa12b-151">Помощник предлагает рекомендации для виртуальных машин, групп доступности, шлюзов приложений, служб приложений, серверов SQL Server, баз данных SQL и кэша Redis.</span><span class="sxs-lookup"><span data-stu-id="fa12b-151">Advisor provides recommendations for virtual machines, availability sets, application gateways, App Services, SQL servers, SQL databases, and Redis Cache.</span></span>

### <a name="can-i-snooze-or-dismiss-a-recommendation"></a><span data-ttu-id="fa12b-152">Можно ли отложить или закрыть рекомендацию?</span><span class="sxs-lookup"><span data-stu-id="fa12b-152">Can I snooze or dismiss a recommendation?</span></span>

<span data-ttu-id="fa12b-153">Чтобы отложить или закрыть рекомендацию, нажмите кнопку **Отложить** или щелкните аналогичную ссылку.</span><span class="sxs-lookup"><span data-stu-id="fa12b-153">To snooze or dismiss a recommendation, click the **Snooze** button or link.</span></span> <span data-ttu-id="fa12b-154">Можно указать период времени, на который откладывается рекомендация, или выбрать значение **Никогда**, чтобы закрыть ее.</span><span class="sxs-lookup"><span data-stu-id="fa12b-154">You can specify a snooze time period or select **Never** to dismiss the recommendation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fa12b-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fa12b-155">Next steps</span></span>

<span data-ttu-id="fa12b-156">Чтобы узнать больше о рекомендациях Помощника, ознакомьтесь с приведенными ниже материалами.</span><span class="sxs-lookup"><span data-stu-id="fa12b-156">To learn more about Advisor recommendations, see:</span></span>

* [<span data-ttu-id="fa12b-157">Приступая к работе с Azure Advisor</span><span class="sxs-lookup"><span data-stu-id="fa12b-157">Get started with Advisor</span></span>](advisor-get-started.md)
* [<span data-ttu-id="fa12b-158">Рекомендации Azure Advisor по высокой доступности</span><span class="sxs-lookup"><span data-stu-id="fa12b-158">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)
* [<span data-ttu-id="fa12b-159">Рекомендации Azure Advisor по безопасности</span><span class="sxs-lookup"><span data-stu-id="fa12b-159">Advisor Security recommendations</span></span>](advisor-security-recommendations.md)
* [<span data-ttu-id="fa12b-160">Рекомендации Azure Advisor по производительности</span><span class="sxs-lookup"><span data-stu-id="fa12b-160">Advisor Performance recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="fa12b-161">Рекомендации Azure Advisor по затратам</span><span class="sxs-lookup"><span data-stu-id="fa12b-161">Advisor Cost recommendations</span></span>](advisor-cost-recommendations.md)
