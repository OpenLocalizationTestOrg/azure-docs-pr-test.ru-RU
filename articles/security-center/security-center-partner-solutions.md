---
title: "решения партнеров aaaManaging в центр безопасности Azure | Документы Microsoft"
description: "В этом документе рассматриваются как Azure центр обеспечения безопасности монитора на быстро оценить состояние работоспособности hello партнера решений для интеграции с подпиской Azure."
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
ms.openlocfilehash: fc97aedf709b9044bfd3d4ecae0b58d5fa716bbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-partner-solutions-with-azure-security-center"></a><span data-ttu-id="c5299-103">Мониторинг решений партнеров с помощью центра безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="c5299-103">Monitoring partner solutions with Azure Security Center</span></span>
<span data-ttu-id="c5299-104">В этом документе рассматриваются как toomonitor hello состояния работоспособности ваших решений партнера в центр безопасности Azure.</span><span class="sxs-lookup"><span data-stu-id="c5299-104">This document walks you through how toomonitor hello health status of your partner solutions in Azure Security Center.</span></span>

> [!NOTE]
> <span data-ttu-id="c5299-105">В этом документе представлены hello службы с помощью пример развертывания.</span><span class="sxs-lookup"><span data-stu-id="c5299-105">This document introduces hello service by using an example deployment.</span></span> <span data-ttu-id="c5299-106">Этот документ не является пошаговым руководством.</span><span class="sxs-lookup"><span data-stu-id="c5299-106">This document is not a step-by-step guide.</span></span>
>
>

## <a name="monitoring-partner-solutions"></a><span data-ttu-id="c5299-107">Мониторинг решений партнеров</span><span class="sxs-lookup"><span data-stu-id="c5299-107">Monitoring partner solutions</span></span>
<span data-ttu-id="c5299-108">Hello **решения партнеров** плитки приветствия **центра обеспечения безопасности** колонке позволяет отслеживать в быстро оценить состояние работоспособности hello решений партнера, интегрированные с подпиской Azure.</span><span class="sxs-lookup"><span data-stu-id="c5299-108">hello **Partner solutions** tile on hello **Security Center** blade lets you monitor at a glance hello health status of your partner solutions that are integrated with your Azure subscription.</span></span>

![Плитка "Решения партнеров"][1]

<span data-ttu-id="c5299-110">Hello **решения партнеров** плитке отображается число hello решения партнеров, интегрированных с вашей подпиской.</span><span class="sxs-lookup"><span data-stu-id="c5299-110">hello **Partner solutions** tile displays hello number of partner solutions integrated with your subscription.</span></span> <span data-ttu-id="c5299-111">При наличии не решений интеграции плитки приветствия отображает hello нуль.</span><span class="sxs-lookup"><span data-stu-id="c5299-111">If there are no solutions integrated, hello tile displays hello number zero.</span></span>

<span data-ttu-id="c5299-112">работоспособность hello tooview партнера решений:</span><span class="sxs-lookup"><span data-stu-id="c5299-112">tooview hello health of your partner solutions:</span></span>

1. <span data-ttu-id="c5299-113">Выберите hello **решения партнеров** плитки.</span><span class="sxs-lookup"><span data-stu-id="c5299-113">Select hello **Partner solutions** tile.</span></span> <span data-ttu-id="c5299-114">Hello **решения партнеров** tooSecurity Center подключен откроется колонка со списком решений для партнера.</span><span class="sxs-lookup"><span data-stu-id="c5299-114">hello **Partner solutions** blade opens displaying a list of your partner solutions connected tooSecurity Center.</span></span>

   ![Решения партнеров][3]

   <span data-ttu-id="c5299-116">состояние Hello партнера решения может быть:</span><span class="sxs-lookup"><span data-stu-id="c5299-116">hello status of a partner solution can be:</span></span>

   * <span data-ttu-id="c5299-117">"Защищено" (зеленый) — нет никаких проблем с работоспособностью.</span><span class="sxs-lookup"><span data-stu-id="c5299-117">Protected (green) - there is no health issue.</span></span>
   * <span data-ttu-id="c5299-118">"Неисправно" (красный) — проблема работоспособности, которая требует немедленного внимания.</span><span class="sxs-lookup"><span data-stu-id="c5299-118">Unhealthy (red) - there is a health issue that requires immediate attention.</span></span>
   * <span data-ttu-id="c5299-119">Остановлена отчетов (оранжевый) — решение hello остановлена reporting его работоспособности.</span><span class="sxs-lookup"><span data-stu-id="c5299-119">Stopped reporting (orange) - hello solution has stopped reporting its health.</span></span>
   * <span data-ttu-id="c5299-120">Неизвестное состояние (оранжевый) - работоспособности hello решения hello неизвестно в данный момент из-за tooa не удалось выполнить процесс добавления новых существующее решение toohello ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c5299-120">Unknown protection status (orange) - hello health of hello solution is unknown at this time due tooa failed process of adding a new resource toohello existing solution.</span></span>
   * <span data-ttu-id="c5299-121">Не сообщается (серый) - ничего не сообщил hello решения, но состояние решение может быть недокументированных, если недавно был подключен и по-прежнему развертывание.</span><span class="sxs-lookup"><span data-stu-id="c5299-121">Not reported (gray) - hello solution has not reported anything yet, a solution's status may be unreported if it has recently been connected and is still deploying.</span></span>

2. <span data-ttu-id="c5299-122">Выберите партнерское решение.</span><span class="sxs-lookup"><span data-stu-id="c5299-122">Select a partner solution.</span></span> <span data-ttu-id="c5299-123">В этом примере, позволяет выбрать hello **Компанию Qualys** решения.</span><span class="sxs-lookup"><span data-stu-id="c5299-123">In this example, lets select hello **Qualys** solution.</span></span>  <span data-ttu-id="c5299-124">Стоечный модуль открывается, отображающая состояние hello hello партнера решения и решения hello связанные с ним ресурсы.</span><span class="sxs-lookup"><span data-stu-id="c5299-124">A blade opens showing you hello status of hello partner solution and hello solution's associated resources.</span></span> <span data-ttu-id="c5299-125">Выберите **консоли решения** возможности управления партнера hello tooopen для этого решения.</span><span class="sxs-lookup"><span data-stu-id="c5299-125">Select **Solution console** tooopen hello partner management experience for this solution.</span></span>

   ![Сведения о партнерском решении][4]
3. <span data-ttu-id="c5299-127">Вернитесь к предыдущему окну toohello **Компанию Qualys** и выберите **ВМ ссылку**.</span><span class="sxs-lookup"><span data-stu-id="c5299-127">Go back toohello **Qualys** blade and select **Link VM**.</span></span> <span data-ttu-id="c5299-128">Hello **ссылку приложения** открывает колонку.</span><span class="sxs-lookup"><span data-stu-id="c5299-128">hello **Link Applications** blade opens.</span></span> <span data-ttu-id="c5299-129">Здесь можно подключить решение партнера toohello ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c5299-129">Here you can connect resources toohello partner solution.</span></span>

   ![Решение toopartner ресурсы ссылку][5]

## <a name="next-steps"></a><span data-ttu-id="c5299-131">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c5299-131">Next steps</span></span>
<span data-ttu-id="c5299-132">В этом документе было введено toohello **решения партнеров** плитки в центре безопасности.</span><span class="sxs-lookup"><span data-stu-id="c5299-132">In this document, you were introduced toohello **Partner Solutions** tile in Security Center.</span></span> <span data-ttu-id="c5299-133">toolearn Дополнительные сведения о центра обеспечения безопасности, см. следующие статьи hello:</span><span class="sxs-lookup"><span data-stu-id="c5299-133">toolearn more about Security Center, see hello following articles:</span></span>

* <span data-ttu-id="c5299-134">[Установка политики безопасности в центр безопасности Azure](security-center-policies.md) — Узнайте как tooconfigure политики безопасности для вашей подписки Azure и группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c5299-134">[Setting security policies in Azure Security Center](security-center-policies.md) — Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="c5299-135">[Управление рекомендациями по безопасности в центре безопасности Azure](security-center-recommendations.md) — сведения об использовании рекомендаций для защиты ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="c5299-135">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="c5299-136">[Наблюдение за работоспособностью системы безопасности в центр безопасности Azure](security-center-monitoring.md) — Узнайте, как toomonitor hello работоспособности ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="c5299-136">[Security health monitoring in Azure Security Center](security-center-monitoring.md) — Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="c5299-137">[Управление и отвечает на запросы toosecurity предупреждения в центр безопасности Azure](security-center-managing-and-responding-alerts.md) — Дополнительные сведения как предупреждения toosecurity toomanage и отправки ответа.</span><span class="sxs-lookup"><span data-stu-id="c5299-137">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) — Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="c5299-138">[Центр безопасности Azure часто задаваемые вопросы о](security-center-faq.md) — часто задаваемые вопросы об использовании hello службы поиска.</span><span class="sxs-lookup"><span data-stu-id="c5299-138">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="c5299-139">[Блог Azure безопасности](http://blogs.msdn.com/b/azuresecurity/) — получить последние новости безопасности Azure hello и информацию.</span><span class="sxs-lookup"><span data-stu-id="c5299-139">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-partner-solutions/partner-solutions-tile.png
[3]: ./media/security-center-partner-solutions/partner-solutions.png
[4]: ./media/security-center-partner-solutions/partner-solutions-detail.png
[5]: ./media/security-center-partner-solutions/link-applications.png
