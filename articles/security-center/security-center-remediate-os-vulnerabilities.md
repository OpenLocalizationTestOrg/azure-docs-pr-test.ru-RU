---
title: "Исправление уязвимостей ОС в центре безопасности Azure | Документация Майкрософт"
description: "В этом документе объясняется, как выполнить рекомендацию центра безопасности Azure \"Remediate OS vulnerabilities\" (Исправить уязвимости ОС)."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 991d41f5-1d17-468d-a66d-83ec1308ab79
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: e6b251d5b97c57b3b6f79d14e53fbed5ca37ecb0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="remediate-os-vulnerabilities-in-azure-security-center"></a><span data-ttu-id="333ea-103">Исправление уязвимостей ОС в центре безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="333ea-103">Remediate OS vulnerabilities in Azure Security Center</span></span>
<span data-ttu-id="333ea-104">Центр безопасности Azure ежедневно анализирует конфигурации операционной системы виртуальной машины, которые могут сделать ее более уязвимой для атак, и рекомендует изменения конфигурации для устранения таких уязвимостей.</span><span class="sxs-lookup"><span data-stu-id="333ea-104">Azure Security Center analyzes daily your virtual machine (VM) operating system (OS) for configurations that could make the VM more vulnerable to attack and recommends configuration changes to address these vulnerabilities.</span></span> <span data-ttu-id="333ea-105">Центр безопасности рекомендует устранить уязвимости в случае, если конфигурация операционной системы виртуальной машины не будет соответствовать рекомендуемым правилам конфигурации.</span><span class="sxs-lookup"><span data-stu-id="333ea-105">Security Center recommends that you resolve vulnerabilities when your VM’s OS configuration does not match the recommended configuration rules.</span></span>

> [!NOTE]
> <span data-ttu-id="333ea-106">Дополнительные сведения о конкретных отслеживаемых конфигурациях доступны в [списке рекомендуемых правил конфигурации](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span><span class="sxs-lookup"><span data-stu-id="333ea-106">For more information on the specific configurations being monitored, see the [list of recommended configuration rules](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="333ea-107">Выполнение рекомендаций</span><span class="sxs-lookup"><span data-stu-id="333ea-107">Implement the recommendation</span></span>

> [!NOTE]
> <span data-ttu-id="333ea-108">В документе приводится обзор службы с помощью примера развертывания.</span><span class="sxs-lookup"><span data-stu-id="333ea-108">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="333ea-109">Этот документ не является пошаговым руководством.</span><span class="sxs-lookup"><span data-stu-id="333ea-109">This document is not a step-by-step guide.</span></span>
>
>

1. <span data-ttu-id="333ea-110">В колонке **Рекомендации** выберите **Устранение уязвимостей ОС**.</span><span class="sxs-lookup"><span data-stu-id="333ea-110">In the **Recommendations** blade, select **Remediate OS vulnerabilities**.</span></span>
   <span data-ttu-id="333ea-111">![Исправление уязвимостей ОС][1]</span><span class="sxs-lookup"><span data-stu-id="333ea-111">![Remediate OS vulnerabilities][1]</span></span>

    <span data-ttu-id="333ea-112">Откроется колонка **Устранение уязвимостей ОС**. В ней перечислены виртуальные машины с конфигурацией операционной системы, которая не соответствуют рекомендуемым правилам конфигурации.</span><span class="sxs-lookup"><span data-stu-id="333ea-112">The **Remediate OS vulnerabilities** blade opens and lists your VMs with OS configurations that do not match the recommended configuration rules.</span></span>  <span data-ttu-id="333ea-113">Для каждой виртуальной машины колонка содержит:</span><span class="sxs-lookup"><span data-stu-id="333ea-113">For each VM, the blade identifies:</span></span>

   * <span data-ttu-id="333ea-114">**Правила с ошибкой** — количество правил, не выполненных конфигурацией ОС виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="333ea-114">**FAILED RULES** -- The number of rules that the VM's OS configuration failed.</span></span>
   * <span data-ttu-id="333ea-115">**Время последнего сканирования** — дата и время последней проверки конфигурации ОС виртуальной машины, выполненной центром безопасности.</span><span class="sxs-lookup"><span data-stu-id="333ea-115">**LAST SCAN TIME** -- The date and time that Security Center last scanned the VM’s OS configuration.</span></span>
   * <span data-ttu-id="333ea-116">**Состояние** — текущее состояние рекомендации уязвимости:</span><span class="sxs-lookup"><span data-stu-id="333ea-116">**STATE** -- The current state of the vulnerability:</span></span>

     * <span data-ttu-id="333ea-117">"Открыто" — уязвимость еще не исправлена;</span><span class="sxs-lookup"><span data-stu-id="333ea-117">Open: The vulnerability has not been addressed yet</span></span>
     * <span data-ttu-id="333ea-118">"Выполняется" — уязвимость уже устраняется, вам ничего не нужно делать;</span><span class="sxs-lookup"><span data-stu-id="333ea-118">In Progress: The vulnerability is currently being applied, no action is required by you</span></span>
     * <span data-ttu-id="333ea-119">"Устранено" — уязвимость устранена (если проблема устранена, эта строка неактивна).</span><span class="sxs-lookup"><span data-stu-id="333ea-119">Resolved: The vulnerability was already addressed (when the issue has been resolved, the entry is grayed out)</span></span>
   * <span data-ttu-id="333ea-120">**Серьезность** — всем уязвимостям присваивается низкая серьезность, означающая, что уязвимость необходимо устранить, но она не требует немедленного внимания.</span><span class="sxs-lookup"><span data-stu-id="333ea-120">**SEVERITY** -- All vulnerabilities are set to a severity of Low, meaning a vulnerability should be addressed but does not require immediate attention.</span></span>

2. <span data-ttu-id="333ea-121">Выберите виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="333ea-121">Select a VM.</span></span> <span data-ttu-id="333ea-122">Откроется колонка для этой виртуальной машины, в которой отображены нарушенные правила.</span><span class="sxs-lookup"><span data-stu-id="333ea-122">A blade for that VM opens and displays the rules that have failed.</span></span>
   <span data-ttu-id="333ea-123">![Правила конфигурации, которые не были выполнены][2]</span><span class="sxs-lookup"><span data-stu-id="333ea-123">![Configuration rules that have failed][2]</span></span>

3. <span data-ttu-id="333ea-124">Выберите правило.</span><span class="sxs-lookup"><span data-stu-id="333ea-124">Select a rule.</span></span> <span data-ttu-id="333ea-125">В этом примере выберем **Пароль должен отвечать требованиям сложности**.</span><span class="sxs-lookup"><span data-stu-id="333ea-125">In this example, lets select **Password must meet complexity requirements**.</span></span> <span data-ttu-id="333ea-126">Откроется колонка, описывающая не выполненное правило и последствия этого.</span><span class="sxs-lookup"><span data-stu-id="333ea-126">A blade opens describing the failed rule and the impact.</span></span> <span data-ttu-id="333ea-127">Просмотрите эту информацию и решите, как будут применяться конфигурации операционной системы.</span><span class="sxs-lookup"><span data-stu-id="333ea-127">Review the details and consider how operating system configurations are applied.</span></span>
  <span data-ttu-id="333ea-128">![Описание правила, которое не выполнено][3]</span><span class="sxs-lookup"><span data-stu-id="333ea-128">![Description for the failed rule][3]</span></span>

  <span data-ttu-id="333ea-129">Центр безопасности использует перечисление общей конфигурации (CCE) для назначения уникальных идентификаторов для правил конфигурации.</span><span class="sxs-lookup"><span data-stu-id="333ea-129">Security Center uses Common Configuration Enumeration (CCE) to assign unique identifiers for configuration rules.</span></span> <span data-ttu-id="333ea-130">В этой колонке предоставляется следующая информация:</span><span class="sxs-lookup"><span data-stu-id="333ea-130">The following information is provided on this blade:</span></span>

  - <span data-ttu-id="333ea-131">"Имя" — имя правила;</span><span class="sxs-lookup"><span data-stu-id="333ea-131">NAME -- Name of rule</span></span>
  - <span data-ttu-id="333ea-132">"Серьезность" — указывает значение серьезности CCE: критическая ошибка, важное уведомление или предупреждение;</span><span class="sxs-lookup"><span data-stu-id="333ea-132">SEVERITY -- CCE severity value of critical, important, or warning</span></span>
  - <span data-ttu-id="333ea-133">"CCIED" — уникальный идентификатор CCE правила;</span><span class="sxs-lookup"><span data-stu-id="333ea-133">CCIED -- CCE unique identifier for the rule</span></span>
  - <span data-ttu-id="333ea-134">"Описание" — описание правила;</span><span class="sxs-lookup"><span data-stu-id="333ea-134">DESCRIPTION -- Description of rule</span></span>
  - <span data-ttu-id="333ea-135">"Уязвимость" — описание уязвимости или риска в случае, если правило не применяется;</span><span class="sxs-lookup"><span data-stu-id="333ea-135">VULNERABILITY -- Explanation of vulnerability or risk if rule is not applied</span></span>
  - <span data-ttu-id="333ea-136">"Воздействие" — влияние на работу организации в случае применения правила;</span><span class="sxs-lookup"><span data-stu-id="333ea-136">IMPACT -- Business impact when rule is applied</span></span>
  - <span data-ttu-id="333ea-137">"Ожидаемое значение" — ожидаемое значение при анализе центром безопасности конфигурации ОС виртуальной машины посредством правила;</span><span class="sxs-lookup"><span data-stu-id="333ea-137">EXPECTED VALUE -- Value expected when Security Center analyzes your VM OS configuration against the rule</span></span>
  - <span data-ttu-id="333ea-138">"Операция правила" — операция правила, используемая центром безопасности во время анализа конфигурации ОС виртуальной машины посредством правила;</span><span class="sxs-lookup"><span data-stu-id="333ea-138">RULE OPERATION -- Rule operation used by Security Center during analysis of your VM OS configuration against the rule</span></span>
  - <span data-ttu-id="333ea-139">"Фактическое значение" — значение, возвращаемое после анализа конфигурации ОС виртуальной машины посредством правила;</span><span class="sxs-lookup"><span data-stu-id="333ea-139">ACTUAL VALUE -- Value returned after analysis of your VM OS configuration against the rule</span></span>
  - <span data-ttu-id="333ea-140">"Результат вычисления" — результат анализа: проверка пройдена или нет.</span><span class="sxs-lookup"><span data-stu-id="333ea-140">EVALUATION RESULT –- Result of analysis: Pass, Fail</span></span>

## <a name="see-also"></a><span data-ttu-id="333ea-141">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="333ea-141">See also</span></span>
<span data-ttu-id="333ea-142">В этой статье объясняется, как выполнить рекомендацию центра безопасности "Remediate OS vulnerabilities" (Исправить уязвимости ОС).</span><span class="sxs-lookup"><span data-stu-id="333ea-142">This article showed you how to implement the Security Center recommendation "Remediate OS vulnerabilities."</span></span> <span data-ttu-id="333ea-143">Набор правил конфигурации можно просмотреть [здесь](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span><span class="sxs-lookup"><span data-stu-id="333ea-143">You can review the set of configuration rules [here](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span></span> <span data-ttu-id="333ea-144">Центр безопасности использует CCE (перечисление общей конфигурации) для назначения уникальных идентификаторов для правил конфигурации.</span><span class="sxs-lookup"><span data-stu-id="333ea-144">Security Center uses CCE (Common Configuration Enumeration) to assign unique identifiers for configuration rules.</span></span> <span data-ttu-id="333ea-145">Посетите сайт [CCE](https://nvd.nist.gov/cce/index.cfm) , чтобы получить дополнительную информацию.</span><span class="sxs-lookup"><span data-stu-id="333ea-145">Visit the [CCE](https://nvd.nist.gov/cce/index.cfm) site for more information.</span></span>

<span data-ttu-id="333ea-146">Дополнительные сведения о центре безопасности см. в следующих ресурсах:</span><span class="sxs-lookup"><span data-stu-id="333ea-146">To learn more about Security Center, see the following resources:</span></span>

* <span data-ttu-id="333ea-147">[Поддерживаемые платформы в центре безопасности Azure](security-center-os-coverage.md) — список поддерживаемых виртуальных машин Windows и Linux.</span><span class="sxs-lookup"><span data-stu-id="333ea-147">[Supported platforms in Azure Security Center](security-center-os-coverage.md) - Provides a list of supported Windows and Linux VMs.</span></span>
* <span data-ttu-id="333ea-148">[Настройка политик безопасности в центре безопасности Azure](security-center-policies.md). Узнайте, как настроить политики безопасности для подписок и групп ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="333ea-148">[Setting security policies in Azure Security Center](security-center-policies.md) - Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="333ea-149">[Управление рекомендациями по безопасности в Центре безопасности Azure](security-center-recommendations.md). Узнайте, как рекомендации могут помочь вам защитить ресурсы Azure.</span><span class="sxs-lookup"><span data-stu-id="333ea-149">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) - Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="333ea-150">[Наблюдение за работоспособностью системы безопасности в Центре безопасности Azure](security-center-monitoring.md). Узнайте, как отслеживать работоспособность ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="333ea-150">[Security health monitoring in Azure Security Center](security-center-monitoring.md) - Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="333ea-151">[Управление оповещениями безопасности в Центре безопасности Azure и реагирование на них](security-center-managing-and-responding-alerts.md). Узнайте, как управлять оповещениями системы безопасности и реагировать на них.</span><span class="sxs-lookup"><span data-stu-id="333ea-151">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) - Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="333ea-152">[Мониторинг решений партнеров с помощью центра безопасности Azure](security-center-partner-solutions.md) — узнайте, как отслеживать состояние работоспособности решений партнеров.</span><span class="sxs-lookup"><span data-stu-id="333ea-152">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) - Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="333ea-153">[Центр безопасности Azure: часто задаваемые вопросы](security-center-faq.md). Часто задаваемые вопросы об использовании этой службы.</span><span class="sxs-lookup"><span data-stu-id="333ea-153">[Azure Security Center FAQ](security-center-faq.md) - Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="333ea-154">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) (Блог по безопасности Azure). Публикации блога, посвященные безопасности и соответствию требованиям в Azure.</span><span class="sxs-lookup"><span data-stu-id="333ea-154">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) - Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-remediate-os-vulnerabilities/recommendation.png
[2]:./media/security-center-remediate-os-vulnerabilities/vm-remediate-os-vulnerabilities.png
[3]: ./media/security-center-remediate-os-vulnerabilities/vulnerability-details.png
