---
title: "Управление решениями партнеров в центре безопасности Azure | Документация Майкрософт"
description: "В этом документе описывается, как центр безопасности Azure позволяет бегло отслеживать состояние работоспособности партнерских решений, интегрированных в вашу подписку Azure."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 70c076ef-3ad4-4000-a0c1-0ac0c9796ff1
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: terrylan
ms.openlocfilehash: 2ebb930e877c5027f4d7b0a316a7f5ebe84471b1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="monitoring-partner-solutions-with-azure-security-center"></a><span data-ttu-id="fa62a-103">Мониторинг решений партнеров с помощью центра безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="fa62a-103">Monitoring partner solutions with Azure Security Center</span></span>
<span data-ttu-id="fa62a-104">В этом документе описывается мониторинг состояния работоспособности партнерских решений в центре безопасности Azure.</span><span class="sxs-lookup"><span data-stu-id="fa62a-104">This document walks you through how to monitor the health status of your partner solutions in Azure Security Center.</span></span>

> [!NOTE]
> <span data-ttu-id="fa62a-105">В документе приводится обзор службы с помощью примера развертывания.</span><span class="sxs-lookup"><span data-stu-id="fa62a-105">This document introduces the service by using an example deployment.</span></span> <span data-ttu-id="fa62a-106">Этот документ не является пошаговым руководством.</span><span class="sxs-lookup"><span data-stu-id="fa62a-106">This document is not a step-by-step guide.</span></span>
>
>

## <a name="monitoring-partner-solutions"></a><span data-ttu-id="fa62a-107">Мониторинг решений партнеров</span><span class="sxs-lookup"><span data-stu-id="fa62a-107">Monitoring partner solutions</span></span>
<span data-ttu-id="fa62a-108">Плитка **Решения партнеров** в колонке **Центр безопасности** дает возможность бегло отслеживать состояние работоспособности решений партнеров, интегрированных в вашу подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="fa62a-108">The **Partner solutions** tile on the **Security Center** blade lets you monitor at a glance the health status of your partner solutions that are integrated with your Azure subscription.</span></span>

![Плитка "Решения партнеров"][1]

<span data-ttu-id="fa62a-110">В элементе **Решения партнеров** отображается количество решений партнеров, интегрированных с вашей подпиской.</span><span class="sxs-lookup"><span data-stu-id="fa62a-110">The **Partner solutions** tile displays the number of partner solutions integrated with your subscription.</span></span> <span data-ttu-id="fa62a-111">Если решения не интегрированы, в элементе отображается число ноль.</span><span class="sxs-lookup"><span data-stu-id="fa62a-111">If there are no solutions integrated, the tile displays the number zero.</span></span>

<span data-ttu-id="fa62a-112">Чтобы просмотреть состояние работоспособности партнерских решений, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="fa62a-112">To view the health of your partner solutions:</span></span>

1. <span data-ttu-id="fa62a-113">Выберите элемент **Решения партнеров** .</span><span class="sxs-lookup"><span data-stu-id="fa62a-113">Select the **Partner solutions** tile.</span></span> <span data-ttu-id="fa62a-114">Откроется колонка **Решения партнеров** со списком решений партнеров, подключенных к центру безопасности.</span><span class="sxs-lookup"><span data-stu-id="fa62a-114">The **Partner solutions** blade opens displaying a list of your partner solutions connected to Security Center.</span></span>

   ![Решения партнеров][3]

   <span data-ttu-id="fa62a-116">Поле состояния партнерского решения может содержать следующее значение:</span><span class="sxs-lookup"><span data-stu-id="fa62a-116">The status of a partner solution can be:</span></span>

   * <span data-ttu-id="fa62a-117">"Защищено" (зеленый) — нет никаких проблем с работоспособностью.</span><span class="sxs-lookup"><span data-stu-id="fa62a-117">Protected (green) - there is no health issue.</span></span>
   * <span data-ttu-id="fa62a-118">"Неисправно" (красный) — проблема работоспособности, которая требует немедленного внимания.</span><span class="sxs-lookup"><span data-stu-id="fa62a-118">Unhealthy (red) - there is a health issue that requires immediate attention.</span></span>
   * <span data-ttu-id="fa62a-119">"Создание отчетов остановлено" (оранжевый) — решение перестало сообщать о работоспособности.</span><span class="sxs-lookup"><span data-stu-id="fa62a-119">Stopped reporting (orange) - the solution has stopped reporting its health.</span></span>
   * <span data-ttu-id="fa62a-120">"Состояние защиты неизвестно" (оранжевый) — работоспособность решения неизвестна в данный момент, так как произошел сбой процесса добавления нового ресурса в существующее решение.</span><span class="sxs-lookup"><span data-stu-id="fa62a-120">Unknown protection status (orange) - the health of the solution is unknown at this time due to a failed process of adding a new resource to the existing solution.</span></span>
   * <span data-ttu-id="fa62a-121">"Не сообщается" (серый) — решение еще не сообщало о своем состоянии; такое состояние может отображаться для решения, если оно подключилось ранее и продолжает развертывание.</span><span class="sxs-lookup"><span data-stu-id="fa62a-121">Not reported (gray) - the solution has not reported anything yet, a solution's status may be unreported if it has recently been connected and is still deploying.</span></span>

2. <span data-ttu-id="fa62a-122">Выберите партнерское решение.</span><span class="sxs-lookup"><span data-stu-id="fa62a-122">Select a partner solution.</span></span> <span data-ttu-id="fa62a-123">В этом примере мы выберем решение **Qualys**.</span><span class="sxs-lookup"><span data-stu-id="fa62a-123">In this example, lets select the **Qualys** solution.</span></span>  <span data-ttu-id="fa62a-124">Откроется колонка, в которой отображается состояние партнерского решения и связанных с ним ресурсов.</span><span class="sxs-lookup"><span data-stu-id="fa62a-124">A blade opens showing you the status of the partner solution and the solution's associated resources.</span></span> <span data-ttu-id="fa62a-125">Нажмите кнопку **Консоль решений** , чтобы открыть партнерский интерфейс управления для этого решения.</span><span class="sxs-lookup"><span data-stu-id="fa62a-125">Select **Solution console** to open the partner management experience for this solution.</span></span>

   ![Сведения о партнерском решении][4]
3. <span data-ttu-id="fa62a-127">Вернитесь к колонке **Qualys** и выберите **Связать виртуальную машину**.</span><span class="sxs-lookup"><span data-stu-id="fa62a-127">Go back to the **Qualys** blade and select **Link VM**.</span></span> <span data-ttu-id="fa62a-128">Откроется колонка **Связь приложений** .</span><span class="sxs-lookup"><span data-stu-id="fa62a-128">The **Link Applications** blade opens.</span></span> <span data-ttu-id="fa62a-129">В ней можно подключить ресурсы к решению партнера.</span><span class="sxs-lookup"><span data-stu-id="fa62a-129">Here you can connect resources to the partner solution.</span></span>

   ![Связывание ресурсов с решением партнера][5]

## <a name="next-steps"></a><span data-ttu-id="fa62a-131">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fa62a-131">Next steps</span></span>
<span data-ttu-id="fa62a-132">В этом документе представлена плитка **Решения партнеров** в центре безопасности.</span><span class="sxs-lookup"><span data-stu-id="fa62a-132">In this document, you were introduced to the **Partner Solutions** tile in Security Center.</span></span> <span data-ttu-id="fa62a-133">Дополнительные сведения о центре безопасности см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="fa62a-133">To learn more about Security Center, see the following articles:</span></span>

* <span data-ttu-id="fa62a-134">[Настройка политик безопасности в центре безопасности Azure](security-center-policies.md) — сведения о настройке политик безопасности для подписок и групп ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="fa62a-134">[Setting security policies in Azure Security Center](security-center-policies.md) — Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="fa62a-135">[Управление рекомендациями по безопасности в центре безопасности Azure](security-center-recommendations.md) — сведения об использовании рекомендаций для защиты ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="fa62a-135">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="fa62a-136">[Наблюдение за работоспособностью системы безопасности в Центре безопасности Azure](security-center-monitoring.md) — узнайте, как отслеживать работоспособность ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="fa62a-136">[Security health monitoring in Azure Security Center](security-center-monitoring.md) — Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="fa62a-137">[Управление оповещениями безопасности в центре безопасности Azure и реагирование на них](security-center-managing-and-responding-alerts.md) — сведения об управлении оповещениями системы безопасности и реагировании на них.</span><span class="sxs-lookup"><span data-stu-id="fa62a-137">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) — Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="fa62a-138">[Центр безопасности Azure: часто задаваемые вопросы](security-center-faq.md) — часто задаваемые вопросы об использовании этой службы.</span><span class="sxs-lookup"><span data-stu-id="fa62a-138">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="fa62a-139">[Блог по безопасности Azure](http://blogs.msdn.com/b/azuresecurity/) — последние новости и сведения об обеспечении безопасности в Azure.</span><span class="sxs-lookup"><span data-stu-id="fa62a-139">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-partner-solutions/partner-solutions-tile.png
[3]: ./media/security-center-partner-solutions/partner-solutions.png
[4]: ./media/security-center-partner-solutions/partner-solutions-detail.png
[5]: ./media/security-center-partner-solutions/link-applications.png
