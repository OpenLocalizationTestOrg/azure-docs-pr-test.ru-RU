---
title: "Отчет об анализе угроз, предоставляемый центром безопасности Azure | Документация Майкрософт"
description: "В этой статье описано, как использовать отчеты об анализе угроз, предоставляемые центром безопасности Azure, в процессе исследования, чтобы получить дополнительные сведения об оповещении системы безопасности."
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 5662e312-e8c2-4736-974e-576eeb333484
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: b4310cf4e6849c67031b3ec8b1fd5957e35f7ea6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-security-center-threat-intelligence-report"></a><span data-ttu-id="70fb0-103">Отчет об анализе угроз, предоставляемый центром безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="70fb0-103">Azure Security Center Threat Intelligence Report</span></span>
<span data-ttu-id="70fb0-104">Здесь содержатся сведения о том, как отчет центра безопасности Azure об анализе угроз позволяет получить подробные сведения касательно угрозы, из-за которой было создано оповещение системы безопасности.</span><span class="sxs-lookup"><span data-stu-id="70fb0-104">This document explains how Azure Security Center Threat Intelligent Reports can help you learn more about a threat that generated a security alert.</span></span>

## <a name="what-is-a-threat-intelligence-report"></a><span data-ttu-id="70fb0-105">Отчет об анализе угроз</span><span class="sxs-lookup"><span data-stu-id="70fb0-105">What is a threat intelligence report?</span></span>
<span data-ttu-id="70fb0-106">Функция обнаружения угроз в центре безопасности осуществляет мониторинг сведений о безопасности из ваших ресурсов Azure, сети и подключенных партнерских решений.</span><span class="sxs-lookup"><span data-stu-id="70fb0-106">Security Center threat detection works by monitoring security information from your Azure resources, the network, and connected partner solutions.</span></span> <span data-ttu-id="70fb0-107">Она анализирует эту информацию, часто сравнивая сведения из разных источников и определяя угрозы.</span><span class="sxs-lookup"><span data-stu-id="70fb0-107">It analyzes this information, often correlating information from multiple sources, to identify threats.</span></span> <span data-ttu-id="70fb0-108">Это часть [возможностей обнаружения](security-center-detection-capabilities.md) центра безопасности.</span><span class="sxs-lookup"><span data-stu-id="70fb0-108">This process is part of the Security Center [detection capabilities](security-center-detection-capabilities.md).</span></span>

<span data-ttu-id="70fb0-109">Когда центр безопасности выявляет угрозу, он активирует [оповещение системы безопасности](security-center-managing-and-responding-alerts.md), которое содержит подробные сведения о конкретном событии, включая рекомендации по исправлению.</span><span class="sxs-lookup"><span data-stu-id="70fb0-109">When Security Center identifies a threat, it will trigger a [security alert](security-center-managing-and-responding-alerts.md), which contains detailed information regarding a particular event, including suggestions for remediation.</span></span> <span data-ttu-id="70fb0-110">Чтобы упростить исследование и устранение угроз для групп реагирования на инциденты, в центре безопасности формируется отчет об анализе угроз, содержащий следующие сведения об обнаруженной угрозе:</span><span class="sxs-lookup"><span data-stu-id="70fb0-110">To assist incident response teams investigate and remediate threats, Security Center includes a threat intelligence report that contains information about the threat that was detected, including information such as the:</span></span>

* <span data-ttu-id="70fb0-111">удостоверение злоумышленника или имеющиеся связи (если такая информация доступна);</span><span class="sxs-lookup"><span data-stu-id="70fb0-111">Attacker’s identity or associations (if this information is available)</span></span>
* <span data-ttu-id="70fb0-112">цели злоумышленника;</span><span class="sxs-lookup"><span data-stu-id="70fb0-112">Attackers’ objectives</span></span>
* <span data-ttu-id="70fb0-113">текущие и исторические кампании атак (если такая информация доступна);</span><span class="sxs-lookup"><span data-stu-id="70fb0-113">Current and historical attack campaigns (if this information is available)</span></span>
* <span data-ttu-id="70fb0-114">тактики злоумышленника, применяемые инструменты и процедуры;</span><span class="sxs-lookup"><span data-stu-id="70fb0-114">Attackers’ tactics, tools and procedures</span></span>
* <span data-ttu-id="70fb0-115">связанные признаки компрометации, такие как URL-адреса и хэши файлов;</span><span class="sxs-lookup"><span data-stu-id="70fb0-115">Associated indicators of compromise (IoC) such as URLs and file hashes</span></span>
* <span data-ttu-id="70fb0-116">сведения о ресурсах или пользователях, подвергшихся атаке, включая данные об отрасли и регионе, которые помогают определить, если ли риск для ваших ресурсов Azure;</span><span class="sxs-lookup"><span data-stu-id="70fb0-116">Victimology, which is the industry and geographic prevalence to assist you in determining if your Azure resources are at risk</span></span>
* <span data-ttu-id="70fb0-117">сведения по устранению и исправлению.</span><span class="sxs-lookup"><span data-stu-id="70fb0-117">Mitigation and remediation information</span></span>

> [!NOTE]
> <span data-ttu-id="70fb0-118">Объем сведений в любом конкретном отчете будет отличаться. Уровень детализации зависит от активности вредоносных программ и их распространенности.</span><span class="sxs-lookup"><span data-stu-id="70fb0-118">The amount of information in any particular report will vary; the level of detail is based on the malware’s activity and prevalence.</span></span>
>
>

<span data-ttu-id="70fb0-119">Центр безопасности предусматривает три типа отчетов об угрозах, которые могут различаться в зависимости от атаки,</span><span class="sxs-lookup"><span data-stu-id="70fb0-119">Security Center has three types of threat reports, which can vary according to the attack.</span></span> <span data-ttu-id="70fb0-120">а именно:</span><span class="sxs-lookup"><span data-stu-id="70fb0-120">The reports available are:</span></span>

* <span data-ttu-id="70fb0-121">**отчет о группе действий**, в котором предоставлен подробный анализ злоумышленников, их целей и примененных тактик;</span><span class="sxs-lookup"><span data-stu-id="70fb0-121">**Activity Group Report**: provides deep dives into attackers, their objectives and tactics.</span></span>
* <span data-ttu-id="70fb0-122">**отчет о кампании**, сосредоточенный на определенных кампаниях атак;</span><span class="sxs-lookup"><span data-stu-id="70fb0-122">**Campaign Report**: focuses on details of specific attack campaigns.</span></span>
* <span data-ttu-id="70fb0-123">**сводный отчет об угрозах**, который включает в себя все элементы двух предыдущих отчетов.</span><span class="sxs-lookup"><span data-stu-id="70fb0-123">**Threat Summary Report**: covers all of the items in the previous two reports.</span></span>

<span data-ttu-id="70fb0-124">Эти сведения очень полезны в процессе [реагирования на инцидент](security-center-incident-response.md), когда ведется исследование, чтобы понять источник атаки, мотивацию злоумышленника и то, как избежать этой проблемы в дальнейшем.</span><span class="sxs-lookup"><span data-stu-id="70fb0-124">This type of information is very useful during the [incident response](security-center-incident-response.md) process, where there is an ongoing investigation to understand the source of the attack, the attacker’s motivations, and what to do to mitigate this issue moving forward.</span></span>

## <a name="how-to-access-the-threat-intelligence-report"></a><span data-ttu-id="70fb0-125">Получение доступа к отчету об анализе угроз</span><span class="sxs-lookup"><span data-stu-id="70fb0-125">How to access the threat intelligence report?</span></span>
<span data-ttu-id="70fb0-126">Текущие оповещения отображаются на плитке **Оповещения системы безопасности** .</span><span class="sxs-lookup"><span data-stu-id="70fb0-126">You can review your current alerts by looking at the **Security alerts** tile.</span></span> <span data-ttu-id="70fb0-127">Чтобы просмотреть дополнительные сведения о каждом оповещении, откройте портал Azure и сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="70fb0-127">Open the Azure Portal and follow the steps below to see more details about each alert:</span></span>

1. <span data-ttu-id="70fb0-128">В центре безопасности на панели мониторинга вы увидите плитку **Оповещения системы безопасности** .</span><span class="sxs-lookup"><span data-stu-id="70fb0-128">On the Security Center dashboard, you will see the **Security alerts** tile.</span></span>
2. <span data-ttu-id="70fb0-129">Щелкните плитку, чтобы открыть колонку **Оповещения системы безопасности**, содержащую подробные сведения об оповещениях, и выберите оповещение, для которого нужно просмотреть сведения.</span><span class="sxs-lookup"><span data-stu-id="70fb0-129">Click the tile to open the **Security alerts** blade that contains more details about the alerts and click in the security alert that you want to obtain more information about.</span></span>

    ![Оповещения безопасности](./media/security-center-threat-report/security-center-threat-report-fig1.png)
3. <span data-ttu-id="70fb0-131">В этом случае мы выберем колонку **Suspicious process executed** (Выполнение подозрительных процессов), содержащую сведения об оповещении. как показано на рисунке ниже.</span><span class="sxs-lookup"><span data-stu-id="70fb0-131">In this case the **Suspicious process executed** blade shows the details about the alert as shown in the figure below:</span></span>

    ![Сведения об оповещениях системы безопасности](./media/security-center-threat-report/security-center-threat-report-fig2.png)
4. <span data-ttu-id="70fb0-133">Объем сведений, доступных для каждого оповещения системы безопасности, отличается в зависимости от типа оповещения.</span><span class="sxs-lookup"><span data-stu-id="70fb0-133">The amount of information available for each security alert will vary according to the type of alert.</span></span> <span data-ttu-id="70fb0-134">В поле **Отчеты** будет содержаться ссылка на отчет об анализе угроз.</span><span class="sxs-lookup"><span data-stu-id="70fb0-134">In the **REPORTS** field you have a link to the threat intelligence report.</span></span> <span data-ttu-id="70fb0-135">Щелкните ее, после чего откроется новое окно браузера с PDF-файлом.</span><span class="sxs-lookup"><span data-stu-id="70fb0-135">Click on it and another browser window will appear with PDF file.</span></span>

   ![Выбор хранилища](./media/security-center-threat-report/security-center-threat-report-fig3.png)

<span data-ttu-id="70fb0-137">Здесь этот файл можно скачать, чтобы узнать больше об обнаруженной проблеме безопасности и предпринять действия на основе этих сведений.</span><span class="sxs-lookup"><span data-stu-id="70fb0-137">From here you can download the PDF for this report and read more about the security issue that was detected and take actions based on the information provided.</span></span>

## <a name="see-also"></a><span data-ttu-id="70fb0-138">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="70fb0-138">See also</span></span>
<span data-ttu-id="70fb0-139">Из этой статьи вы узнали, как отчеты центра безопасности Azure об анализе угроз могут помочь при исследовании оповещений системы безопасности.</span><span class="sxs-lookup"><span data-stu-id="70fb0-139">In this document, you learned how Azure Security Center Threat Intelligent Reports can help during an investigation about security alerts.</span></span> <span data-ttu-id="70fb0-140">Дополнительные сведения о Центре безопасности Azure см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="70fb0-140">To learn more about Azure Security Center, see the following:</span></span>

* <span data-ttu-id="70fb0-141">[Центр безопасности Azure: часто задаваемые вопросы](security-center-faq.md).</span><span class="sxs-lookup"><span data-stu-id="70fb0-141">[Azure Security Center FAQ](security-center-faq.md).</span></span> <span data-ttu-id="70fb0-142">Часто задаваемые вопросы об использовании этой службы.</span><span class="sxs-lookup"><span data-stu-id="70fb0-142">Find frequently asked questions about using the service.</span></span>
* [<span data-ttu-id="70fb0-143">Использование центра безопасности Azure для реагирования на инциденты</span><span class="sxs-lookup"><span data-stu-id="70fb0-143">Leveraging Azure Security Center for Incident Response</span></span>](security-center-incident-response.md)
* [<span data-ttu-id="70fb0-144">Возможности обнаружения центра безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="70fb0-144">Azure Security Center detection capabilities</span></span>](security-center-detection-capabilities.md)
* <span data-ttu-id="70fb0-145">[Руководство по планированию использования центра безопасности Azure и работе в нем](security-center-planning-and-operations-guide.md).</span><span class="sxs-lookup"><span data-stu-id="70fb0-145">[Azure Security Center planning and operations guide](security-center-planning-and-operations-guide.md).</span></span> <span data-ttu-id="70fb0-146">Узнайте, как спланировать работу в центре безопасности Azure, и получите рекомендации по переходу к его использованию.</span><span class="sxs-lookup"><span data-stu-id="70fb0-146">Learn how to plan and understand the design considerations to adopt Azure Security Center.</span></span>
* <span data-ttu-id="70fb0-147">[Управление оповещениями безопасности в Центре безопасности Azure и реагирование на них](security-center-managing-and-responding-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="70fb0-147">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md).</span></span> <span data-ttu-id="70fb0-148">Узнайте, как управлять оповещениями системы безопасности и реагировать на них.</span><span class="sxs-lookup"><span data-stu-id="70fb0-148">Learn how to manage and respond to security alerts.</span></span>
* [<span data-ttu-id="70fb0-149">Обработка инцидентов в центре безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="70fb0-149">Handling Security Incident in Azure Security Center</span></span>](security-center-incident.md)
* <span data-ttu-id="70fb0-150">[Блог по безопасности Azure](http://blogs.msdn.com/b/azuresecurity/).</span><span class="sxs-lookup"><span data-stu-id="70fb0-150">[Azure Security Blog](http://blogs.msdn.com/b/azuresecurity/).</span></span> <span data-ttu-id="70fb0-151">Записи блога, посвященные безопасности и соответствию требованиям в Azure.</span><span class="sxs-lookup"><span data-stu-id="70fb0-151">Find blog posts about Azure security and compliance.</span></span>
