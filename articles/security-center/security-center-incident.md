---
title: "Обработка оповещений системы безопасности в центре безопасности Azure | Документация Майкрософт"
description: "В документе описываются возможности центра безопасности Azure, используемые при управлении инцидентами."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: e8feb669-8f30-49eb-ba38-046edf3f9656
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: yurid
ms.openlocfilehash: a302f8cb2555eef469a24da2523fdd9b97cc5730
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="handling-security-incidents-in-azure-security-center"></a><span data-ttu-id="55c8e-103">Обработка инцидентов в центре безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="55c8e-103">Handling Security Incidents in Azure Security Center</span></span>
<span data-ttu-id="55c8e-104">Рассмотрение и исследование оповещений системы безопасности может занять много времени даже у самых опытных аналитиков в сфере безопасности, а многие пользователи даже не знают, с чего начать.</span><span class="sxs-lookup"><span data-stu-id="55c8e-104">Triaging and investigating security alerts can be time consuming for even the most skilled security analysts, and for many it is hard to even know where to begin.</span></span> <span data-ttu-id="55c8e-105">Используя [аналитику](security-center-detection-capabilities.md) для связывания данных из разных [оповещений системы безопасности](security-center-managing-and-responding-alerts.md), центр безопасности может предоставить общую картину кампании атак и все соответствующие оповещения. Это позволит вам быстро понять, какие действия выполнил злоумышленник и какие ресурсы затронуты.</span><span class="sxs-lookup"><span data-stu-id="55c8e-105">By using [analytics](security-center-detection-capabilities.md) to connect the information between distinct [security alerts](security-center-managing-and-responding-alerts.md), Security Center can provide you with a single view of an attack campaign and all of the related alerts – you can quickly understand what actions the attacker took and what resources were impacted.</span></span>

<span data-ttu-id="55c8e-106">В этом документе объясняется, как использовать возможности оповещений системы безопасности в центре безопасности при возникновении инцидентов.</span><span class="sxs-lookup"><span data-stu-id="55c8e-106">This document discusses how to use security alert capability in Security Center to assist you handling security incidents.</span></span>

## <a name="what-is-a-security-incident"></a><span data-ttu-id="55c8e-107">Что такое инцидент?</span><span class="sxs-lookup"><span data-stu-id="55c8e-107">What is a security incident?</span></span>
<span data-ttu-id="55c8e-108">В центре безопасности инцидентом считается совокупность всех оповещений для ресурса, которые соответствуют схемам [этапов нарушения безопасности](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/) .</span><span class="sxs-lookup"><span data-stu-id="55c8e-108">In Security Center, a security incident is an aggregation of all alerts for a resource that align with [kill chain](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/) patterns.</span></span> <span data-ttu-id="55c8e-109">Инциденты отображаются на плитке [Оповещения системы безопасности](security-center-managing-and-responding-alerts.md) и в одноименной колонке.</span><span class="sxs-lookup"><span data-stu-id="55c8e-109">Incidents appear in the [Security Alerts](security-center-managing-and-responding-alerts.md) tile and blade.</span></span> <span data-ttu-id="55c8e-110">Инцидент содержит список соответствующих оповещений, который позволяет получить дополнительные сведения о каждом происшествии.</span><span class="sxs-lookup"><span data-stu-id="55c8e-110">An Incident will reveal the list of related alerts, which enables you to obtain more information about each occurrence.</span></span>

## <a name="managing-security-incidents"></a><span data-ttu-id="55c8e-111">Управление инцидентами</span><span class="sxs-lookup"><span data-stu-id="55c8e-111">Managing security incidents</span></span>
<span data-ttu-id="55c8e-112">Текущие инциденты можно просматривать на плитке "Оповещения системы безопасности".</span><span class="sxs-lookup"><span data-stu-id="55c8e-112">You can review your current security incidents by looking at the security alerts tile.</span></span> <span data-ttu-id="55c8e-113">Войдите на портал Azure и выполните следующие действия, чтобы получить дополнительные сведения о каждом инциденте.</span><span class="sxs-lookup"><span data-stu-id="55c8e-113">Access the Azure Portal and follow the steps below to see more details about each security incident:</span></span>

1. <span data-ttu-id="55c8e-114">На панели мониторинга в центре безопасности вы увидите плитку **Оповещения системы безопасности** .</span><span class="sxs-lookup"><span data-stu-id="55c8e-114">On the Security Center dashboard, you will see the **Security alerts** tile.</span></span>

    ![Плитка "Оповещения системы безопасности" в центре безопасности](./media/security-center-incident/security-center-incident-fig1.png)

2. <span data-ttu-id="55c8e-116">Щелкните эту плитку, чтобы развернуть ее. Обнаруженный инцидент будет отображаться под диаграммой предупреждений безопасности, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="55c8e-116">Click on this tile to expand it and if a security incident is detected, it will appear under the security alerts graph as shown  below:</span></span>

    ![Инцидент](./media/security-center-incident/security-center-incident-fig2.png)

3. <span data-ttu-id="55c8e-118">Обратите внимание, что в описании инцидентов используется не такой значок, как в других оповещениях.</span><span class="sxs-lookup"><span data-stu-id="55c8e-118">Notice that the security incident description has a different icon compared to other alerts.</span></span> <span data-ttu-id="55c8e-119">Щелкните его, чтобы просмотреть дополнительные сведения об инциденте.</span><span class="sxs-lookup"><span data-stu-id="55c8e-119">Click on it to view more details about this incident.</span></span>

    ![Инцидент](./media/security-center-incident/security-center-incident-fig3.png)

4. <span data-ttu-id="55c8e-121">В колонке **инцидента** отобразятся подробные сведения об инциденте: его полное описание; уровень серьезности (здесь — высокий); текущее состояние (здесь — по-прежнему *активен*, то есть пользователь еще не принял никаких мер, что можно сделать, щелкнув инцидент правой кнопкой мыши в колонке **Оповещения системы безопасности**); атакуемый ресурс (здесь — *VM1*); действия по исправлению инцидента; а внизу — оповещения, которые включены в этот инцидент.</span><span class="sxs-lookup"><span data-stu-id="55c8e-121">On the **incident** blade you will see more details about this security incident, which includes its full description, its severity (which in this case is high), its current state (in this case it is still *active*, which implies the user hasn't taken an action to it - this can be done by right clicking on the incident in the **Security alerts** blade), the attacked resource (in this case *VM1*), the remediation steps for the incident, and in the bottom pane you have the alerts that were included in this incident.</span></span> <span data-ttu-id="55c8e-122">Если вы хотите получить дополнительные сведения о каждом оповещении, просто щелкните его, и откроется новая колонка, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="55c8e-122">If you want to obtain more information on each alert, just click on it and another blade will open, as shown below:</span></span>

    ![Инцидент](./media/security-center-incident/security-center-incident-fig4.png)

<span data-ttu-id="55c8e-124">Сведения в этой колонке будут разными в зависимости от оповещения.</span><span class="sxs-lookup"><span data-stu-id="55c8e-124">The information on this blade will vary according to the alert.</span></span> <span data-ttu-id="55c8e-125">Дополнительные сведения об управлении этими оповещениями см. в статье [Управление оповещениями безопасности в центре безопасности Azure и реагирование на них](security-center-managing-and-responding-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="55c8e-125">Read [Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) for more information on how to manage these alerts.</span></span> <span data-ttu-id="55c8e-126">Некоторые важные замечания, касающиеся работы этой функции.</span><span class="sxs-lookup"><span data-stu-id="55c8e-126">Some important considerations regarding this capability:</span></span>

* <span data-ttu-id="55c8e-127">С помощью нового фильтра можно настроить отображение только инцидента, только оповещений, а также и инцидента, и оповещений.</span><span class="sxs-lookup"><span data-stu-id="55c8e-127">A new filter enables you to customize your view to Incident only, Alerts only, or both.</span></span>
* <span data-ttu-id="55c8e-128">Одно и то же оповещение может существовать как часть инцидента (если он существует), а также отображаться в виде автономного оповещения.</span><span class="sxs-lookup"><span data-stu-id="55c8e-128">The same alert can exist as part of an Incident (if applicable), as well as to be visible as a standalone alert.</span></span>

## <a name="see-also"></a><span data-ttu-id="55c8e-129">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="55c8e-129">See also</span></span>
<span data-ttu-id="55c8e-130">Этот документ содержит подробные сведения о функции инцидентов в центре безопасности Azure.</span><span class="sxs-lookup"><span data-stu-id="55c8e-130">In this document, you learned how to use the security incident capability in Security Center.</span></span> <span data-ttu-id="55c8e-131">Дополнительные сведения о Центре безопасности см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="55c8e-131">To learn more about Security Center, see the following:</span></span>

* [<span data-ttu-id="55c8e-132">Управление оповещениями безопасности в Центре безопасности Azure и реагирование на них</span><span class="sxs-lookup"><span data-stu-id="55c8e-132">Managing and responding to security alerts in Azure Security Center</span></span>](security-center-managing-and-responding-alerts.md)
* [<span data-ttu-id="55c8e-133">Возможности обнаружения центра безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="55c8e-133">Azure Security Center Detection Capabilities</span></span>](security-center-detection-capabilities.md)
* [<span data-ttu-id="55c8e-134">Руководство по планированию использования центра безопасности Azure и работе в нем</span><span class="sxs-lookup"><span data-stu-id="55c8e-134">Azure Security Center Planning and Operations Guide</span></span>](security-center-planning-and-operations-guide.md)
* [<span data-ttu-id="55c8e-135">Управление оповещениями безопасности в Центре безопасности Azure и реагирование на них</span><span class="sxs-lookup"><span data-stu-id="55c8e-135">Managing and responding to security alerts in Azure Security Center</span></span>](security-center-managing-and-responding-alerts.md)
* <span data-ttu-id="55c8e-136">[Центр безопасности Azure: часто задаваемые вопросы](security-center-faq.md)— часто задаваемые вопросы об использовании этой службы.</span><span class="sxs-lookup"><span data-stu-id="55c8e-136">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="55c8e-137">[Блог по безопасности Azure](http://blogs.msdn.com/b/azuresecurity/) — публикации блога, посвященные безопасности и соответствию требованиям в Azure.</span><span class="sxs-lookup"><span data-stu-id="55c8e-137">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Find blog posts about Azure security and compliance.</span></span>
