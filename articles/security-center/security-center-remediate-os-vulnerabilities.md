---
title: "уязвимости aaaRemediate ОС в центр безопасности Azure | Документы Microsoft"
description: "В этом документе показано, как tooimplement hello рекомендации центра безопасности Azure ** ОС устранять уязвимости **."
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
ms.openlocfilehash: 704103f7fb15835943d74b665d2bd56cb5e0a36d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="remediate-os-vulnerabilities-in-azure-security-center"></a><span data-ttu-id="7e2e1-103">Исправление уязвимостей ОС в центре безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="7e2e1-103">Remediate OS vulnerabilities in Azure Security Center</span></span>
<span data-ttu-id="7e2e1-104">Центр безопасности Azure ежедневно анализирует виртуальной машины (VM) операционной системы (ОС), для виртуальной Машины hello конфигураций, которые могут выполнять более уязвимыми tooattack и рекомендует Конфигурация изменяется tooaddress эти уязвимости.</span><span class="sxs-lookup"><span data-stu-id="7e2e1-104">Azure Security Center analyzes daily your virtual machine (VM) operating system (OS) for configurations that could make hello VM more vulnerable tooattack and recommends configuration changes tooaddress these vulnerabilities.</span></span> <span data-ttu-id="7e2e1-105">Центр безопасности Майкрософт рекомендует устраняют уязвимости, когда конфигурация ОС Виртуальной машины не соответствует hello рекомендуемые конфигурации правила.</span><span class="sxs-lookup"><span data-stu-id="7e2e1-105">Security Center recommends that you resolve vulnerabilities when your VM’s OS configuration does not match hello recommended configuration rules.</span></span>

> [!NOTE]
> <span data-ttu-id="7e2e1-106">Дополнительные сведения о конкретных конфигураций hello отслеживается в разделе hello [список правил Рекомендуемая конфигурация](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span><span class="sxs-lookup"><span data-stu-id="7e2e1-106">For more information on hello specific configurations being monitored, see hello [list of recommended configuration rules](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="7e2e1-107">Реализация рекомендаций hello</span><span class="sxs-lookup"><span data-stu-id="7e2e1-107">Implement hello recommendation</span></span>

> [!NOTE]
> <span data-ttu-id="7e2e1-108">В этом документе представлены hello службы с помощью пример развертывания.</span><span class="sxs-lookup"><span data-stu-id="7e2e1-108">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="7e2e1-109">Этот документ не является пошаговым руководством.</span><span class="sxs-lookup"><span data-stu-id="7e2e1-109">This document is not a step-by-step guide.</span></span>
>
>

1. <span data-ttu-id="7e2e1-110">В hello **рекомендации** колонке выберите **уязвимостей исправлять ОС**.</span><span class="sxs-lookup"><span data-stu-id="7e2e1-110">In hello **Recommendations** blade, select **Remediate OS vulnerabilities**.</span></span>
   <span data-ttu-id="7e2e1-111">![Исправление уязвимостей ОС][1]</span><span class="sxs-lookup"><span data-stu-id="7e2e1-111">![Remediate OS vulnerabilities][1]</span></span>

    <span data-ttu-id="7e2e1-112">Hello **уязвимостей исправлять ОС** колонке открывает и список виртуальных машин с конфигурациями операционной системы, которые не соответствуют hello рекомендуемые конфигурации правила.</span><span class="sxs-lookup"><span data-stu-id="7e2e1-112">hello **Remediate OS vulnerabilities** blade opens and lists your VMs with OS configurations that do not match hello recommended configuration rules.</span></span>  <span data-ttu-id="7e2e1-113">Для каждой виртуальной Машины идентифицирует hello колонки:</span><span class="sxs-lookup"><span data-stu-id="7e2e1-113">For each VM, hello blade identifies:</span></span>

   * <span data-ttu-id="7e2e1-114">**Сбой ПРАВИЛА** --сбой hello количества правил, hello конфигурацию операционной системы Виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="7e2e1-114">**FAILED RULES** -- hello number of rules that hello VM's OS configuration failed.</span></span>
   * <span data-ttu-id="7e2e1-115">**ВРЕМЯ ПОСЛЕДНЕЙ проверки** — hello даты и времени, что центр обеспечения безопасности последней проверки конфигурации операционной системы виртуальной Машины hello.</span><span class="sxs-lookup"><span data-stu-id="7e2e1-115">**LAST SCAN TIME** -- hello date and time that Security Center last scanned hello VM’s OS configuration.</span></span>
   * <span data-ttu-id="7e2e1-116">**СОСТОЯНИЕ** --hello уязвимость hello текущее состояние:</span><span class="sxs-lookup"><span data-stu-id="7e2e1-116">**STATE** -- hello current state of hello vulnerability:</span></span>

     * <span data-ttu-id="7e2e1-117">Открытые: hello уязвимость не будет устранена еще</span><span class="sxs-lookup"><span data-stu-id="7e2e1-117">Open: hello vulnerability has not been addressed yet</span></span>
     * <span data-ttu-id="7e2e1-118">В данный момент: Hello уязвимости в настоящее время, применяется, не требуется никаких действий с вашей стороны</span><span class="sxs-lookup"><span data-stu-id="7e2e1-118">In Progress: hello vulnerability is currently being applied, no action is required by you</span></span>
     * <span data-ttu-id="7e2e1-119">Разрешить: hello уязвимость уже устранена (когда hello проблема будет устранена, запись hello выделен серым)</span><span class="sxs-lookup"><span data-stu-id="7e2e1-119">Resolved: hello vulnerability was already addressed (when hello issue has been resolved, hello entry is grayed out)</span></span>
   * <span data-ttu-id="7e2e1-120">**СЕРЬЕЗНОСТЬ** --все уязвимости задаются tooa серьезность низкий, то есть уязвимость, должны быть устранены, но не требует немедленного внимания.</span><span class="sxs-lookup"><span data-stu-id="7e2e1-120">**SEVERITY** -- All vulnerabilities are set tooa severity of Low, meaning a vulnerability should be addressed but does not require immediate attention.</span></span>

2. <span data-ttu-id="7e2e1-121">Выберите виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="7e2e1-121">Select a VM.</span></span> <span data-ttu-id="7e2e1-122">Стоечный модуль для этой виртуальной Машины открывает и отображает hello правила, которые не удалось.</span><span class="sxs-lookup"><span data-stu-id="7e2e1-122">A blade for that VM opens and displays hello rules that have failed.</span></span>
   <span data-ttu-id="7e2e1-123">![Правила конфигурации, которые не были выполнены][2]</span><span class="sxs-lookup"><span data-stu-id="7e2e1-123">![Configuration rules that have failed][2]</span></span>

3. <span data-ttu-id="7e2e1-124">Выберите правило.</span><span class="sxs-lookup"><span data-stu-id="7e2e1-124">Select a rule.</span></span> <span data-ttu-id="7e2e1-125">В этом примере выберем **Пароль должен отвечать требованиям сложности**.</span><span class="sxs-lookup"><span data-stu-id="7e2e1-125">In this example, lets select **Password must meet complexity requirements**.</span></span> <span data-ttu-id="7e2e1-126">Стоечный модуль открывает описания hello не удалось выполнить правило и hello последствия.</span><span class="sxs-lookup"><span data-stu-id="7e2e1-126">A blade opens describing hello failed rule and hello impact.</span></span> <span data-ttu-id="7e2e1-127">Просмотрите сведения о hello и рассмотрите возможность применения конфигурации операционных систем.</span><span class="sxs-lookup"><span data-stu-id="7e2e1-127">Review hello details and consider how operating system configurations are applied.</span></span>
  <span data-ttu-id="7e2e1-128">![Описание для hello не удалось выполнить правило][3]</span><span class="sxs-lookup"><span data-stu-id="7e2e1-128">![Description for hello failed rule][3]</span></span>

  <span data-ttu-id="7e2e1-129">Центр обеспечения безопасности использует перечисление распространенные конфигурации (CCE) tooassign уникальные идентификаторы для настройки правил.</span><span class="sxs-lookup"><span data-stu-id="7e2e1-129">Security Center uses Common Configuration Enumeration (CCE) tooassign unique identifiers for configuration rules.</span></span> <span data-ttu-id="7e2e1-130">в этой колонке предоставляется Hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="7e2e1-130">hello following information is provided on this blade:</span></span>

  - <span data-ttu-id="7e2e1-131">"Имя" — имя правила;</span><span class="sxs-lookup"><span data-stu-id="7e2e1-131">NAME -- Name of rule</span></span>
  - <span data-ttu-id="7e2e1-132">"Серьезность" — указывает значение серьезности CCE: критическая ошибка, важное уведомление или предупреждение;</span><span class="sxs-lookup"><span data-stu-id="7e2e1-132">SEVERITY -- CCE severity value of critical, important, or warning</span></span>
  - <span data-ttu-id="7e2e1-133">CCIED--CCE уникальный идентификатор правила hello</span><span class="sxs-lookup"><span data-stu-id="7e2e1-133">CCIED -- CCE unique identifier for hello rule</span></span>
  - <span data-ttu-id="7e2e1-134">"Описание" — описание правила;</span><span class="sxs-lookup"><span data-stu-id="7e2e1-134">DESCRIPTION -- Description of rule</span></span>
  - <span data-ttu-id="7e2e1-135">"Уязвимость" — описание уязвимости или риска в случае, если правило не применяется;</span><span class="sxs-lookup"><span data-stu-id="7e2e1-135">VULNERABILITY -- Explanation of vulnerability or risk if rule is not applied</span></span>
  - <span data-ttu-id="7e2e1-136">"Воздействие" — влияние на работу организации в случае применения правила;</span><span class="sxs-lookup"><span data-stu-id="7e2e1-136">IMPACT -- Business impact when rule is applied</span></span>
  - <span data-ttu-id="7e2e1-137">ОЖИДАЕМОЕ значение — Значение, ожидаемое при центра обеспечения безопасности анализирует конфигурацию ОС виртуальной Машины соответствие правилу hello</span><span class="sxs-lookup"><span data-stu-id="7e2e1-137">EXPECTED VALUE -- Value expected when Security Center analyzes your VM OS configuration against hello rule</span></span>
  - <span data-ttu-id="7e2e1-138">— ПРАВИЛА правило операцию используемого центра обеспечения безопасности во время анализа конфигурации ОС виртуальной Машины соответствие правилу hello</span><span class="sxs-lookup"><span data-stu-id="7e2e1-138">RULE OPERATION -- Rule operation used by Security Center during analysis of your VM OS configuration against hello rule</span></span>
  - <span data-ttu-id="7e2e1-139">ФАКТИЧЕСКОЕ значение — Значение, возвращаемое после анализа конфигурации ОС виртуальной Машины соответствие правилу hello</span><span class="sxs-lookup"><span data-stu-id="7e2e1-139">ACTUAL VALUE -- Value returned after analysis of your VM OS configuration against hello rule</span></span>
  - <span data-ttu-id="7e2e1-140">"Результат вычисления" — результат анализа: проверка пройдена или нет.</span><span class="sxs-lookup"><span data-stu-id="7e2e1-140">EVALUATION RESULT –- Result of analysis: Pass, Fail</span></span>

## <a name="see-also"></a><span data-ttu-id="7e2e1-141">См. также</span><span class="sxs-lookup"><span data-stu-id="7e2e1-141">See also</span></span>
<span data-ttu-id="7e2e1-142">В этой статье показано, как tooimplement hello центра обеспечения безопасности рекомендаций» исправьте ОС уязвимостей.»</span><span class="sxs-lookup"><span data-stu-id="7e2e1-142">This article showed you how tooimplement hello Security Center recommendation "Remediate OS vulnerabilities."</span></span> <span data-ttu-id="7e2e1-143">Вы можете просмотреть hello набор правил конфигурации [здесь](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span><span class="sxs-lookup"><span data-stu-id="7e2e1-143">You can review hello set of configuration rules [here](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span></span> <span data-ttu-id="7e2e1-144">Центр обеспечения безопасности использует уникальные идентификаторы tooassign CCE (перечисление распространенные конфигурации) для настройки правил.</span><span class="sxs-lookup"><span data-stu-id="7e2e1-144">Security Center uses CCE (Common Configuration Enumeration) tooassign unique identifiers for configuration rules.</span></span> <span data-ttu-id="7e2e1-145">Посетите hello [CCE](https://nvd.nist.gov/cce/index.cfm) сайт для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="7e2e1-145">Visit hello [CCE](https://nvd.nist.gov/cce/index.cfm) site for more information.</span></span>

<span data-ttu-id="7e2e1-146">toolearn Дополнительные сведения о центра обеспечения безопасности, см. следующие ресурсы hello:</span><span class="sxs-lookup"><span data-stu-id="7e2e1-146">toolearn more about Security Center, see hello following resources:</span></span>

* <span data-ttu-id="7e2e1-147">[Поддерживаемые платформы в центре безопасности Azure](security-center-os-coverage.md) — список поддерживаемых виртуальных машин Windows и Linux.</span><span class="sxs-lookup"><span data-stu-id="7e2e1-147">[Supported platforms in Azure Security Center](security-center-os-coverage.md) - Provides a list of supported Windows and Linux VMs.</span></span>
* <span data-ttu-id="7e2e1-148">[Установка политики безопасности в центр безопасности Azure](security-center-policies.md) -Узнайте, как tooconfigure политики безопасности для вашей подписки Azure и группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7e2e1-148">[Setting security policies in Azure Security Center](security-center-policies.md) - Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="7e2e1-149">[Управление рекомендациями по безопасности в Центре безопасности Azure](security-center-recommendations.md). Узнайте, как рекомендации могут помочь вам защитить ресурсы Azure.</span><span class="sxs-lookup"><span data-stu-id="7e2e1-149">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) - Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="7e2e1-150">[Наблюдение за работоспособностью системы безопасности в центр безопасности Azure](security-center-monitoring.md) -Узнайте, как toomonitor hello работоспособности ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="7e2e1-150">[Security health monitoring in Azure Security Center](security-center-monitoring.md) - Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="7e2e1-151">[Управление и отвечает на запросы toosecurity предупреждения в центр безопасности Azure](security-center-managing-and-responding-alerts.md) -Узнайте, как предупреждения toosecurity toomanage и отправки ответа.</span><span class="sxs-lookup"><span data-stu-id="7e2e1-151">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) - Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="7e2e1-152">[Мониторинг решений партнера с центром обеспечения безопасности Azure](security-center-partner-solutions.md) -Узнайте, как toomonitor hello состояние работоспособности решений для партнера.</span><span class="sxs-lookup"><span data-stu-id="7e2e1-152">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) - Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="7e2e1-153">[Центр безопасности Azure часто задаваемые вопросы о](security-center-faq.md) -часто задаваемые вопросы об использовании hello службы поиска.</span><span class="sxs-lookup"><span data-stu-id="7e2e1-153">[Azure Security Center FAQ](security-center-faq.md) - Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="7e2e1-154">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) (Блог по безопасности Azure). Публикации блога, посвященные безопасности и соответствию требованиям в Azure.</span><span class="sxs-lookup"><span data-stu-id="7e2e1-154">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) - Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-remediate-os-vulnerabilities/recommendation.png
[2]:./media/security-center-remediate-os-vulnerabilities/vm-remediate-os-vulnerabilities.png
[3]: ./media/security-center-remediate-os-vulnerabilities/vulnerability-details.png
