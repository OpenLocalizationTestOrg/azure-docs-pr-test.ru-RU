---
title: "предупреждения безопасности aaaManage в центр безопасности Azure | Документы Microsoft"
description: "Этот документ поможет вам toouse центра безопасности Azure возможности toomanage и реагировать toosecurity предупреждения."
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
ms.openlocfilehash: f1cb7e4770776827b75ed15893914678c1f44216
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="managing-and-responding-toosecurity-alerts-in-azure-security-center"></a><span data-ttu-id="6f5c7-103">Управление и отвечать на запросы toosecurity оповещения в центр безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="6f5c7-103">Managing and responding toosecurity alerts in Azure Security Center</span></span>
<span data-ttu-id="6f5c7-104">В этом документе помогает использовать toomanage центра безопасности Azure и отвечать toosecurity предупреждения.</span><span class="sxs-lookup"><span data-stu-id="6f5c7-104">This document helps you use Azure Security Center toomanage and respond toosecurity alerts.</span></span>

> [!NOTE]
> <span data-ttu-id="6f5c7-105">Расширенный tooenable обнаружений обновления tooAzure Security Center Standard.</span><span class="sxs-lookup"><span data-stu-id="6f5c7-105">tooenable advanced detections, upgrade tooAzure Security Center Standard.</span></span> <span data-ttu-id="6f5c7-106">Бесплатный пробный период составляет 60 дней.</span><span class="sxs-lookup"><span data-stu-id="6f5c7-106">A free 60-day trial is available.</span></span> <span data-ttu-id="6f5c7-107">tooupgrade выберите ценовую категорию hello [политики безопасности](security-center-policies.md).</span><span class="sxs-lookup"><span data-stu-id="6f5c7-107">tooupgrade, select Pricing Tier in hello [Security Policy](security-center-policies.md).</span></span> <span data-ttu-id="6f5c7-108">В разделе [центра безопасности Azure цены](security-center-pricing.md) toolearn дополнительные.</span><span class="sxs-lookup"><span data-stu-id="6f5c7-108">See [Azure Security Center pricing](security-center-pricing.md) toolearn more.</span></span>
>
>

## <a name="what-are-security-alerts"></a><span data-ttu-id="6f5c7-109">Что такое оповещения системы безопасности?</span><span class="sxs-lookup"><span data-stu-id="6f5c7-109">What are security alerts?</span></span>
<span data-ttu-id="6f5c7-110">Центр обеспечения безопасности автоматически собирает, анализирует и интегрирует данные журнала по вашим ресурсам Azure сети hello и подключение решения партнеров, как брандмауэр и конечной точки решения по защите, toodetect реальные угрозы, снижая ложных положительных результатов.</span><span class="sxs-lookup"><span data-stu-id="6f5c7-110">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, hello network, and connected partner solutions, like firewall and endpoint protection solutions, toodetect real threats and reduce false positives.</span></span> <span data-ttu-id="6f5c7-111">Список оповещений системы безопасности упорядоченный отображается в центре безопасности вместе с hello информацию, необходимую tooquickly исследовать проблему hello и рекомендаций по их атаки tooremediate.</span><span class="sxs-lookup"><span data-stu-id="6f5c7-111">A list of prioritized security alerts is shown in Security Center along with hello information you need tooquickly investigate hello problem and recommendations for how tooremediate an attack.</span></span>


> [!NOTE]
> <span data-ttu-id="6f5c7-112">Дополнительные сведения о способах обнаружения угроз в центре безопасности см. в статье [Возможности обнаружения центра безопасности Azure](security-center-detection-capabilities.md).</span><span class="sxs-lookup"><span data-stu-id="6f5c7-112">For more information about how Security Center detection capabilities work, read [Azure Security Center Detection Capabilities](security-center-detection-capabilities.md).</span></span>
>
>

## <a name="managing-security-alerts"></a><span data-ttu-id="6f5c7-113">Управление оповещениями системы безопасности</span><span class="sxs-lookup"><span data-stu-id="6f5c7-113">Managing security alerts</span></span>
<span data-ttu-id="6f5c7-114">Можно просмотреть текущее оповещения, просмотрев hello **оповещений системы безопасности** плитки.</span><span class="sxs-lookup"><span data-stu-id="6f5c7-114">You can review your current alerts by looking at hello **Security alerts** tile.</span></span> <span data-ttu-id="6f5c7-115">Откройте портал Azure и выполните действия hello ниже toosee Дополнительные сведения о каждом оповещении.</span><span class="sxs-lookup"><span data-stu-id="6f5c7-115">Open Azure Portal and follow hello steps below toosee more details about each alert:</span></span>

1. <span data-ttu-id="6f5c7-116">На панели мониторинга hello центра обеспечения безопасности, вы увидите hello **оповещений системы безопасности** плитки.</span><span class="sxs-lookup"><span data-stu-id="6f5c7-116">On hello Security Center dashboard, you will see hello **Security alerts** tile.</span></span>

    ![Плитка "Оповещения системы безопасности" в центре безопасности](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig1-ga.png)

2. <span data-ttu-id="6f5c7-118">Нажмите кнопку hello tooopen плитки приветствия **оповещений системы безопасности** колонку, которая содержит дополнительные сведения о hello предупреждений, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="6f5c7-118">Click hello tile tooopen hello **Security alerts** blade that contains more details about hello alerts as shown below.</span></span>

   ![Hello колонке предупреждения безопасности в центре безопасности](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig2-ga.png)

<span data-ttu-id="6f5c7-120">В нижней части hello эту колонку, hello сведения для каждого предупреждения.</span><span class="sxs-lookup"><span data-stu-id="6f5c7-120">In hello bottom part of this blade are hello details for each alert.</span></span> <span data-ttu-id="6f5c7-121">toosort, щелкните нужный toosort по столбец hello.</span><span class="sxs-lookup"><span data-stu-id="6f5c7-121">toosort, click hello column that you want toosort by.</span></span> <span data-ttu-id="6f5c7-122">Определение Hello для каждого столбца, приведены ниже:</span><span class="sxs-lookup"><span data-stu-id="6f5c7-122">hello definition for each column is given below:</span></span>

* <span data-ttu-id="6f5c7-123">**Описание**: краткое описание оповещения hello.</span><span class="sxs-lookup"><span data-stu-id="6f5c7-123">**Description**: A brief explanation of hello alert.</span></span>
* <span data-ttu-id="6f5c7-124">**Число**— список всех оповещений определенного типа, обнаруженных в определенный день.</span><span class="sxs-lookup"><span data-stu-id="6f5c7-124">**Count**: A list of all alerts of this specific type that were detected on a specific day.</span></span>
* <span data-ttu-id="6f5c7-125">**Обнаружено**: hello службы, для запуска оповещения hello.</span><span class="sxs-lookup"><span data-stu-id="6f5c7-125">**Detected by**: hello service that was responsible for triggering hello alert.</span></span>
* <span data-ttu-id="6f5c7-126">**Дата**: hello Дата события hello произошла.</span><span class="sxs-lookup"><span data-stu-id="6f5c7-126">**Date**: hello date that hello event occurred.</span></span>
* <span data-ttu-id="6f5c7-127">**Состояние**: hello текущее состояние для данного предупреждения.</span><span class="sxs-lookup"><span data-stu-id="6f5c7-127">**State**: hello current state for that alert.</span></span> <span data-ttu-id="6f5c7-128">Существует два типа состояний.</span><span class="sxs-lookup"><span data-stu-id="6f5c7-128">There are two types of states:</span></span>
  * <span data-ttu-id="6f5c7-129">**Активные**: обнаружена hello предупреждения системы безопасности.</span><span class="sxs-lookup"><span data-stu-id="6f5c7-129">**Active**: hello security alert has been detected.</span></span>
* <span data-ttu-id="6f5c7-130">**Серьезность**: уровень серьезности hello, который может быть высокий, средний или низкий.</span><span class="sxs-lookup"><span data-stu-id="6f5c7-130">**Severity**: hello severity level, which can be high, medium or low.</span></span>

### <a name="filtering-alerts"></a><span data-ttu-id="6f5c7-131">Фильтрация оповещений</span><span class="sxs-lookup"><span data-stu-id="6f5c7-131">Filtering alerts</span></span>
<span data-ttu-id="6f5c7-132">Оповещения можно фильтровать по дате, состоянию и уровни серьезности.</span><span class="sxs-lookup"><span data-stu-id="6f5c7-132">You can filter alerts based on date, state, and severity.</span></span> <span data-ttu-id="6f5c7-133">Фильтрация предупреждений может быть полезно для сценариев, в которых требуется область hello toonarrow Показать предупреждения системы безопасности.</span><span class="sxs-lookup"><span data-stu-id="6f5c7-133">Filtering alerts can be useful for scenarios where you need toonarrow hello scope of security alerts show.</span></span> <span data-ttu-id="6f5c7-134">Например, вы может оповещения безопасности tooaddress, произошедших в hello последние 24 часа, так как в системе hello анализируем потенциальных нарушений безопасности.</span><span class="sxs-lookup"><span data-stu-id="6f5c7-134">For example, you might you want tooaddress security alerts that occurred in hello last 24 hours because you are investigating a potential breach in hello system.</span></span>

1. <span data-ttu-id="6f5c7-135">Нажмите кнопку **фильтра** на hello **оповещений системы безопасности** колонку.</span><span class="sxs-lookup"><span data-stu-id="6f5c7-135">Click **Filter** on hello **Security Alerts** blade.</span></span> <span data-ttu-id="6f5c7-136">Hello **фильтра** открывает колонку и выборе hello, состояния, значения даты и серьезности нужно toosee.</span><span class="sxs-lookup"><span data-stu-id="6f5c7-136">hello **Filter** blade opens and you select hello date, state, and severity values you wish toosee.</span></span>

    ![Фильтрация оповещений в центре безопасности](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig3-2017.png)

### <a name="respond-toosecurity-alerts"></a><span data-ttu-id="6f5c7-138">Ответ toosecurity оповещения</span><span class="sxs-lookup"><span data-stu-id="6f5c7-138">Respond toosecurity alerts</span></span>
<span data-ttu-id="6f5c7-139">Выберите toolearn предупреждения безопасности Дополнительные сведения о события hello, вызвавшей предупреждение hello и что, если действия, необходимые tootake tooremediate атаки.</span><span class="sxs-lookup"><span data-stu-id="6f5c7-139">Select a security alert toolearn more about hello event(s) that triggered hello alert and what, if any, steps you need tootake tooremediate an attack.</span></span> <span data-ttu-id="6f5c7-140">Оповещения системы безопасности группируются по типу и дате.</span><span class="sxs-lookup"><span data-stu-id="6f5c7-140">Security alerts are grouped by type and date.</span></span> <span data-ttu-id="6f5c7-141">Если щелкнуть предупреждение системы безопасности откроется стоечный модуль, содержащий список оповещений, сгруппированных hello.</span><span class="sxs-lookup"><span data-stu-id="6f5c7-141">Clicking a security alert will open a blade containing a list of hello grouped alerts.</span></span>

![Ответ toosecurity оповещения в центр безопасности Azure](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig5-ga.png)

<span data-ttu-id="6f5c7-143">В этом случае hello оповещения, которые были предприняты ссылаться toosuspicious действия удаленного рабочего стола (RDP).</span><span class="sxs-lookup"><span data-stu-id="6f5c7-143">In this case, hello alerts that were triggered refer toosuspicious Remote Desktop Protocol (RDP) activity.</span></span> <span data-ttu-id="6f5c7-144">Первый столбец Hello показывает, какие ресурсы подверглась; Hello второй показывает, сколько раз был атаке hello ресурсов; Hello третий показывает время hello атакам hello. Hello в-четвертых показывается состояние hello предупреждение; и hello пятых показывает важность hello hello атаки.</span><span class="sxs-lookup"><span data-stu-id="6f5c7-144">hello first column shows which resources were attacked; hello second shows how many times hello resource was attacked; hello third shows hello time of hello attack; hello fourth shows state of hello alert; and hello fifth shows hello severity of hello attack.</span></span> <span data-ttu-id="6f5c7-145">После просмотра этих сведений, щелкните ресурс hello, который был атаке и открывается новая колонка.</span><span class="sxs-lookup"><span data-stu-id="6f5c7-145">After reviewing this information, click hello resource that was attacked and a new blade will open.</span></span>

![Предложения по предупреждения какие toodo о безопасности в центр безопасности Azure](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig6-ga.png)

<span data-ttu-id="6f5c7-147">В hello **описание** поля этой колонки вы найдете дополнительные сведения о данном событии.</span><span class="sxs-lookup"><span data-stu-id="6f5c7-147">In hello **Description** field of this blade you will find more details about this event.</span></span> <span data-ttu-id="6f5c7-148">Эти дополнительные сведения являются понять, какие триггеру hello безопасности предупреждения, hello целевой ресурс, когда применимо hello исходный IP-адрес и рекомендации о том, как tooremediate.</span><span class="sxs-lookup"><span data-stu-id="6f5c7-148">These additional details offer insight into what triggered hello security alert, hello target resource, when applicable hello source IP address, and recommendations about how tooremediate.</span></span>  <span data-ttu-id="6f5c7-149">В некоторых случаях hello исходный IP-адрес будет быть пустым (недоступно), так как не все журналы событий безопасности Windows включают hello IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="6f5c7-149">In some instances, hello source IP address will be empty (not available) because not all Windows security events logs include hello IP address.</span></span>

<span data-ttu-id="6f5c7-150">исправления Hello предложенными центра обеспечения безопасности зависит соответствующим предупреждения системы безопасности toohello.</span><span class="sxs-lookup"><span data-stu-id="6f5c7-150">hello remediation suggested by Security Center will vary according toohello security alert.</span></span> <span data-ttu-id="6f5c7-151">В некоторых случаях может иметь других возможностей Azure tooimplement toouse hello Рекомендуемые исправления.</span><span class="sxs-lookup"><span data-stu-id="6f5c7-151">In some cases, you may have toouse other Azure capabilities tooimplement hello recommended remediation.</span></span> <span data-ttu-id="6f5c7-152">Например, hello исправления для такой атаки является tooblacklist hello IP-адрес, создающего такой атаки с помощью [сетевых ACL](../virtual-network/virtual-networks-acl.md) или [сетевой группы безопасности](../virtual-network/virtual-networks-nsg.md) правило.</span><span class="sxs-lookup"><span data-stu-id="6f5c7-152">For example, hello remediation for this attack is tooblacklist hello IP address that is generating this attack by using a [network ACL](../virtual-network/virtual-networks-acl.md) or a [network security group](../virtual-network/virtual-networks-nsg.md) rule.</span></span>

> [!NOTE]
> <span data-ttu-id="6f5c7-153">Дополнительные сведения о различных типах оповещений hello [оповещений системы безопасности по типу в центр безопасности Azure](security-center-alerts-type.md).</span><span class="sxs-lookup"><span data-stu-id="6f5c7-153">For more information on hello different types of alerts, read [Security Alerts by Type in Azure Security Center](security-center-alerts-type.md).</span></span>
>
>

## <a name="see-also"></a><span data-ttu-id="6f5c7-154">См. также</span><span class="sxs-lookup"><span data-stu-id="6f5c7-154">See also</span></span>
<span data-ttu-id="6f5c7-155">В этом документе вы узнали, каким образом tooconfigure политики безопасности в центре безопасности.</span><span class="sxs-lookup"><span data-stu-id="6f5c7-155">In this document, you learned how tooconfigure security policies in Security Center.</span></span> <span data-ttu-id="6f5c7-156">toolearn Дополнительные сведения о центра обеспечения безопасности, см. ниже hello:</span><span class="sxs-lookup"><span data-stu-id="6f5c7-156">toolearn more about Security Center, see hello following:</span></span>

* [<span data-ttu-id="6f5c7-157">Обработка инцидентов в центре безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="6f5c7-157">Handling Security Incident in Azure Security Center</span></span>](security-center-incident.md)
* [<span data-ttu-id="6f5c7-158">Возможности обнаружения центра безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="6f5c7-158">Azure Security Center Detection Capabilities</span></span>](security-center-detection-capabilities.md)
* [<span data-ttu-id="6f5c7-159">Руководство по планированию использования центра безопасности Azure и работе в нем</span><span class="sxs-lookup"><span data-stu-id="6f5c7-159">Azure Security Center Planning and Operations Guide</span></span>](security-center-planning-and-operations-guide.md)
* <span data-ttu-id="6f5c7-160">[Центр безопасности Azure часто задаваемые вопросы о](security-center-faq.md) — часто задаваемые вопросы об использовании hello службы поиска.</span><span class="sxs-lookup"><span data-stu-id="6f5c7-160">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="6f5c7-161">[Блог по безопасности Azure](http://blogs.msdn.com/b/azuresecurity/) — публикации блога, посвященные безопасности и соответствию требованиям в Azure.</span><span class="sxs-lookup"><span data-stu-id="6f5c7-161">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Find blog posts about Azure security and compliance.</span></span>
