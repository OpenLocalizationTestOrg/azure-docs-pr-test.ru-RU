---
title: "Управление оповещениями системы безопасности в центре безопасности Azure | Документация Майкрософт"
description: "Этот документ помогает использовать возможности Центра безопасности Azure для управления и реагирования на оповещения безопасности."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: b88a8df7-6979-479b-8039-04da1b8737a7
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: yurid
ms.openlocfilehash: 56fcfbfdbe15749132ba6a27861142fd564063c3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="managing-and-responding-to-security-alerts-in-azure-security-center"></a><span data-ttu-id="1bdf1-103">Управление оповещениями безопасности в Центре безопасности Azure и реагирование на них</span><span class="sxs-lookup"><span data-stu-id="1bdf1-103">Managing and responding to security alerts in Azure Security Center</span></span>
<span data-ttu-id="1bdf1-104">Этот документ помогает использовать возможности центра безопасности Azure для управления оповещениями безопасности и реагирования на них.</span><span class="sxs-lookup"><span data-stu-id="1bdf1-104">This document helps you use Azure Security Center to manage and respond to security alerts.</span></span>

> [!NOTE]
> <span data-ttu-id="1bdf1-105">Чтобы включить расширенное обнаружение, выполните обновление до стандартного центра безопасности Azure.</span><span class="sxs-lookup"><span data-stu-id="1bdf1-105">To enable advanced detections, upgrade to Azure Security Center Standard.</span></span> <span data-ttu-id="1bdf1-106">Бесплатный пробный период составляет 60 дней.</span><span class="sxs-lookup"><span data-stu-id="1bdf1-106">A free 60-day trial is available.</span></span> <span data-ttu-id="1bdf1-107">Чтобы выполнить обновление, выберите ценовую категорию в [политике безопасности](security-center-policies.md).</span><span class="sxs-lookup"><span data-stu-id="1bdf1-107">To upgrade, select Pricing Tier in the [Security Policy](security-center-policies.md).</span></span> <span data-ttu-id="1bdf1-108">Дополнительные сведения см. на странице с [ценами центра безопасности Azure](security-center-pricing.md).</span><span class="sxs-lookup"><span data-stu-id="1bdf1-108">See [Azure Security Center pricing](security-center-pricing.md) to learn more.</span></span>
>
>

## <a name="what-are-security-alerts"></a><span data-ttu-id="1bdf1-109">Что такое оповещения системы безопасности?</span><span class="sxs-lookup"><span data-stu-id="1bdf1-109">What are security alerts?</span></span>
<span data-ttu-id="1bdf1-110">Центр безопасности автоматически собирает, анализирует и объединяет данные журналов, поступающие от ресурсов Azure, сети и подключенных решений партнеров, таких как брандмауэры и решения для защиты конечных точек, для выявления реальных угроз и сокращения ложных срабатываний.</span><span class="sxs-lookup"><span data-stu-id="1bdf1-110">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, the network, and connected partner solutions, like firewall and endpoint protection solutions, to detect real threats and reduce false positives.</span></span> <span data-ttu-id="1bdf1-111">Список приоритетных оповещений системы безопасности отображается в центре безопасности вместе с информацией, необходимой для быстрого анализа проблемы, и рекомендациями по устранению атаки.</span><span class="sxs-lookup"><span data-stu-id="1bdf1-111">A list of prioritized security alerts is shown in Security Center along with the information you need to quickly investigate the problem and recommendations for how to remediate an attack.</span></span>


> [!NOTE]
> <span data-ttu-id="1bdf1-112">Дополнительные сведения о способах обнаружения угроз в центре безопасности см. в статье [Возможности обнаружения центра безопасности Azure](security-center-detection-capabilities.md).</span><span class="sxs-lookup"><span data-stu-id="1bdf1-112">For more information about how Security Center detection capabilities work, read [Azure Security Center Detection Capabilities](security-center-detection-capabilities.md).</span></span>
>
>

## <a name="managing-security-alerts"></a><span data-ttu-id="1bdf1-113">Управление оповещениями системы безопасности</span><span class="sxs-lookup"><span data-stu-id="1bdf1-113">Managing security alerts</span></span>
<span data-ttu-id="1bdf1-114">Текущие оповещения отображаются на плитке **Оповещения системы безопасности** .</span><span class="sxs-lookup"><span data-stu-id="1bdf1-114">You can review your current alerts by looking at the **Security alerts** tile.</span></span> <span data-ttu-id="1bdf1-115">Чтобы просмотреть дополнительные сведения о каждом оповещении, откройте портал Azure и сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="1bdf1-115">Open Azure Portal and follow the steps below to see more details about each alert:</span></span>

1. <span data-ttu-id="1bdf1-116">В центре безопасности на панели мониторинга вы увидите плитку **Оповещения системы безопасности** .</span><span class="sxs-lookup"><span data-stu-id="1bdf1-116">On the Security Center dashboard, you will see the **Security alerts** tile.</span></span>

    ![Плитка "Оповещения системы безопасности" в центре безопасности](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig1-ga.png)

2. <span data-ttu-id="1bdf1-118">Щелкните эту плитку, чтобы открыть колонку **Оповещения системы безопасности** с дополнительными сведениями об оповещениях, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="1bdf1-118">Click the tile to open the **Security alerts** blade that contains more details about the alerts as shown below.</span></span>

   ![Колонка "Оповещения системы безопасности" в центре безопасности](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig2-ga.png)

<span data-ttu-id="1bdf1-120">В нижней части этой колонки содержатся сведения для каждого оповещения.</span><span class="sxs-lookup"><span data-stu-id="1bdf1-120">In the bottom part of this blade are the details for each alert.</span></span> <span data-ttu-id="1bdf1-121">Чтобы отсортировать данные, щелкните соответствующий столбец.</span><span class="sxs-lookup"><span data-stu-id="1bdf1-121">To sort, click the column that you want to sort by.</span></span> <span data-ttu-id="1bdf1-122">Ниже приводятся определения столбцов:</span><span class="sxs-lookup"><span data-stu-id="1bdf1-122">The definition for each column is given below:</span></span>

* <span data-ttu-id="1bdf1-123">**Описание** — краткое описание оповещения.</span><span class="sxs-lookup"><span data-stu-id="1bdf1-123">**Description**: A brief explanation of the alert.</span></span>
* <span data-ttu-id="1bdf1-124">**Число**— список всех оповещений определенного типа, обнаруженных в определенный день.</span><span class="sxs-lookup"><span data-stu-id="1bdf1-124">**Count**: A list of all alerts of this specific type that were detected on a specific day.</span></span>
* <span data-ttu-id="1bdf1-125">**Обнаружено**— служба, отвечающая за активацию оповещения.</span><span class="sxs-lookup"><span data-stu-id="1bdf1-125">**Detected by**: The service that was responsible for triggering the alert.</span></span>
* <span data-ttu-id="1bdf1-126">**Дата**— дата возникновения события.</span><span class="sxs-lookup"><span data-stu-id="1bdf1-126">**Date**: The date that the event occurred.</span></span>
* <span data-ttu-id="1bdf1-127">**Состояние**— текущее состояние оповещения.</span><span class="sxs-lookup"><span data-stu-id="1bdf1-127">**State**: The current state for that alert.</span></span> <span data-ttu-id="1bdf1-128">Существует два типа состояний.</span><span class="sxs-lookup"><span data-stu-id="1bdf1-128">There are two types of states:</span></span>
  * <span data-ttu-id="1bdf1-129">**Активно**— обнаружено оповещение системы безопасности.</span><span class="sxs-lookup"><span data-stu-id="1bdf1-129">**Active**: The security alert has been detected.</span></span>
* <span data-ttu-id="1bdf1-130">**Серьезность** — уровень серьезности. Может быть высоким, средним или низким.</span><span class="sxs-lookup"><span data-stu-id="1bdf1-130">**Severity**: The severity level, which can be high, medium or low.</span></span>

### <a name="filtering-alerts"></a><span data-ttu-id="1bdf1-131">Фильтрация оповещений</span><span class="sxs-lookup"><span data-stu-id="1bdf1-131">Filtering alerts</span></span>
<span data-ttu-id="1bdf1-132">Оповещения можно фильтровать по дате, состоянию и уровни серьезности.</span><span class="sxs-lookup"><span data-stu-id="1bdf1-132">You can filter alerts based on date, state, and severity.</span></span> <span data-ttu-id="1bdf1-133">Фильтрация оповещений нужна в ситуациях, когда требуется сузить область просматриваемых оповещений системы безопасности.</span><span class="sxs-lookup"><span data-stu-id="1bdf1-133">Filtering alerts can be useful for scenarios where you need to narrow the scope of security alerts show.</span></span> <span data-ttu-id="1bdf1-134">Например, вам может потребоваться проверить оповещения системы безопасности, возникшие за последние 24 часа, поскольку вы исследуете потенциальное нарушение безопасности в системе.</span><span class="sxs-lookup"><span data-stu-id="1bdf1-134">For example, you might you want to address security alerts that occurred in the last 24 hours because you are investigating a potential breach in the system.</span></span>

1. <span data-ttu-id="1bdf1-135">В колонке **Оповещения системы безопасности** щелкните **Фильтр**.</span><span class="sxs-lookup"><span data-stu-id="1bdf1-135">Click **Filter** on the **Security Alerts** blade.</span></span> <span data-ttu-id="1bdf1-136">Откроется колонка **Фильтр** , в которой можно выбрать дату, состояние и уровень серьезности.</span><span class="sxs-lookup"><span data-stu-id="1bdf1-136">The **Filter** blade opens and you select the date, state, and severity values you wish to see.</span></span>

    ![Фильтрация оповещений в центре безопасности](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig3-2017.png)

### <a name="respond-to-security-alerts"></a><span data-ttu-id="1bdf1-138">Реагирование на оповещения системы безопасности</span><span class="sxs-lookup"><span data-stu-id="1bdf1-138">Respond to security alerts</span></span>
<span data-ttu-id="1bdf1-139">Выберите оповещение системы безопасности, чтобы получить дополнительные сведения о событиях, вызвавших оповещение, и (при необходимости) действиях, которые следует предпринять для устранения атаки.</span><span class="sxs-lookup"><span data-stu-id="1bdf1-139">Select a security alert to learn more about the event(s) that triggered the alert and what, if any, steps you need to take to remediate an attack.</span></span> <span data-ttu-id="1bdf1-140">Оповещения системы безопасности группируются по типу и дате.</span><span class="sxs-lookup"><span data-stu-id="1bdf1-140">Security alerts are grouped by type and date.</span></span> <span data-ttu-id="1bdf1-141">Если щелкнуть оповещение системы безопасности, откроется колонка, содержащая список сгруппированных оповещений.</span><span class="sxs-lookup"><span data-stu-id="1bdf1-141">Clicking a security alert will open a blade containing a list of the grouped alerts.</span></span>

![Реагирование на оповещения системы безопасности в Центре безопасности Azure](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig5-ga.png)

<span data-ttu-id="1bdf1-143">В этом случае запущенные оповещения относятся к подозрительной активности протокола удаленного рабочего стола (RDP).</span><span class="sxs-lookup"><span data-stu-id="1bdf1-143">In this case, the alerts that were triggered refer to suspicious Remote Desktop Protocol (RDP) activity.</span></span> <span data-ttu-id="1bdf1-144">В первом столбце показано, какие ресурсы подверглись атаке, во втором — количество атак на ресурс, в третьем — время атаки, в четвертом — состояние оповещения, а в пятом — уровень серьезности атаки.</span><span class="sxs-lookup"><span data-stu-id="1bdf1-144">The first column shows which resources were attacked; the second shows how many times the resource was attacked; the third shows the time of the attack; the fourth shows state of the alert; and the fifth shows the severity of the attack.</span></span> <span data-ttu-id="1bdf1-145">Ознакомьтесь с этими сведениями, затем щелкните ресурс, подвергшийся атаке. Откроется новая колонка.</span><span class="sxs-lookup"><span data-stu-id="1bdf1-145">After reviewing this information, click the resource that was attacked and a new blade will open.</span></span>

![Рекомендации по реагированию на оповещения системы безопасности в Центре безопасности Azure](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig6-ga.png)

<span data-ttu-id="1bdf1-147">В этой колонке в поле **Описание** содержатся дополнительные сведения о событии.</span><span class="sxs-lookup"><span data-stu-id="1bdf1-147">In the **Description** field of this blade you will find more details about this event.</span></span> <span data-ttu-id="1bdf1-148">Эти дополнительные сведения содержат причину появления предупреждения системы безопасности, целевой ресурс, IP-адрес источника (если применимо) и рекомендации по устранению этой причины.</span><span class="sxs-lookup"><span data-stu-id="1bdf1-148">These additional details offer insight into what triggered the security alert, the target resource, when applicable the source IP address, and recommendations about how to remediate.</span></span>  <span data-ttu-id="1bdf1-149">В некоторых случаях IP-адрес источника будет пустым (недоступным), так как не все журналы событий безопасности Windows включают IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="1bdf1-149">In some instances, the source IP address will be empty (not available) because not all Windows security events logs include the IP address.</span></span>

<span data-ttu-id="1bdf1-150">Исправления, предлагаемые Центром безопасности Azure, зависят от оповещения системы безопасности.</span><span class="sxs-lookup"><span data-stu-id="1bdf1-150">The remediation suggested by Security Center will vary according to the security alert.</span></span> <span data-ttu-id="1bdf1-151">В некоторых случаях для реализации рекомендуемого исправления могут потребоваться другие возможности Azure.</span><span class="sxs-lookup"><span data-stu-id="1bdf1-151">In some cases, you may have to use other Azure capabilities to implement the recommended remediation.</span></span> <span data-ttu-id="1bdf1-152">Например, чтобы ликвидировать эту атаку, необходимо поместить в черный список IP-адрес, с которого исходит атака, с помощью [списка управления доступом в сети](../virtual-network/virtual-networks-acl.md) или правила [группы безопасности сети](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="1bdf1-152">For example, the remediation for this attack is to blacklist the IP address that is generating this attack by using a [network ACL](../virtual-network/virtual-networks-acl.md) or a [network security group](../virtual-network/virtual-networks-nsg.md) rule.</span></span>

> [!NOTE]
> <span data-ttu-id="1bdf1-153">Дополнительные сведения о различных типах оповещений см. в статье [Типы оповещений системы безопасности в центре безопасности Azure](security-center-alerts-type.md).</span><span class="sxs-lookup"><span data-stu-id="1bdf1-153">For more information on the different types of alerts, read [Security Alerts by Type in Azure Security Center](security-center-alerts-type.md).</span></span>
>
>

## <a name="see-also"></a><span data-ttu-id="1bdf1-154">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="1bdf1-154">See also</span></span>
<span data-ttu-id="1bdf1-155">В этом документе вы ознакомились с подробными сведениями о настройке политик безопасности в Центре безопасности.</span><span class="sxs-lookup"><span data-stu-id="1bdf1-155">In this document, you learned how to configure security policies in Security Center.</span></span> <span data-ttu-id="1bdf1-156">Дополнительные сведения о Центре безопасности см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="1bdf1-156">To learn more about Security Center, see the following:</span></span>

* [<span data-ttu-id="1bdf1-157">Обработка инцидентов в центре безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="1bdf1-157">Handling Security Incident in Azure Security Center</span></span>](security-center-incident.md)
* [<span data-ttu-id="1bdf1-158">Возможности обнаружения центра безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="1bdf1-158">Azure Security Center Detection Capabilities</span></span>](security-center-detection-capabilities.md)
* [<span data-ttu-id="1bdf1-159">Руководство по планированию использования центра безопасности Azure и работе в нем</span><span class="sxs-lookup"><span data-stu-id="1bdf1-159">Azure Security Center Planning and Operations Guide</span></span>](security-center-planning-and-operations-guide.md)
* <span data-ttu-id="1bdf1-160">[Центр безопасности Azure: часто задаваемые вопросы](security-center-faq.md) — часто задаваемые вопросы об использовании этой службы.</span><span class="sxs-lookup"><span data-stu-id="1bdf1-160">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="1bdf1-161">[Блог по безопасности Azure](http://blogs.msdn.com/b/azuresecurity/) — публикации блога, посвященные безопасности и соответствию требованиям в Azure.</span><span class="sxs-lookup"><span data-stu-id="1bdf1-161">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Find blog posts about Azure security and compliance.</span></span>
