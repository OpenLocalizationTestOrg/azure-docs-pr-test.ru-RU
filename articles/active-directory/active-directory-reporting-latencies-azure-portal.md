---
title: "aaaAzure Active Directory отчетов задержки | Документы Microsoft"
description: "Дополнительные сведения о hello количество времени, необходимое для создания отчетов tooshow события вверх на портале Azure"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 9b88958d-94a2-4f4b-a18c-616f0617a24e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi;dhanyahk
ms.reviewer: dhanyahk
ms.openlocfilehash: eee959331262ba59b313dd038cb54699dbef48a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-latencies"></a><span data-ttu-id="b161d-103">Задержки в отчетах Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b161d-103">Azure Active Directory reporting latencies</span></span>

<span data-ttu-id="b161d-104">С [reporting](active-directory-preview-explainer.md) в hello Azure Active Directory, вы получаете все hello информацию, необходимую toodetermine, насколько вашей среде.</span><span class="sxs-lookup"><span data-stu-id="b161d-104">With [reporting](active-directory-preview-explainer.md) in hello Azure Active Directory, you get all hello information you need toodetermine how your environment is doing.</span></span> <span data-ttu-id="b161d-105">объем времени, необходимое для создания отчетов, что данные tooshow вверх в hello портал Azure, также называемая задержки Hello.</span><span class="sxs-lookup"><span data-stu-id="b161d-105">hello amount of time it takes for reporting data tooshow up in hello Azure portal is also known as latency.</span></span> 

<span data-ttu-id="b161d-106">В этом разделе перечислены сведения о задержке hello для hello все категории отчетов в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b161d-106">This topic lists hello latency information for hello all reporting categories in hello Azure portal.</span></span> 


## <a name="activity-reports"></a><span data-ttu-id="b161d-107">Отчеты об активности</span><span class="sxs-lookup"><span data-stu-id="b161d-107">Activity reports</span></span>

<span data-ttu-id="b161d-108">Есть две области отчетов об активности:</span><span class="sxs-lookup"><span data-stu-id="b161d-108">There are two areas of activity reporting:</span></span>

- <span data-ttu-id="b161d-109">**Действия входа** — сведения об использовании hello управляемых приложений и действий входа пользователей</span><span class="sxs-lookup"><span data-stu-id="b161d-109">**Sign-in activities** – Information about hello usage of managed applications and user sign-in activities</span></span>
- <span data-ttu-id="b161d-110">**Журналы аудита** — информация системных операций об управлении пользователями и группами, об управляемых приложениях и действиях каталогов.</span><span class="sxs-lookup"><span data-stu-id="b161d-110">**Audit logs** - System activity information about users and group management, your managed applications and directory activities</span></span>

<span data-ttu-id="b161d-111">Hello в следующей таблице перечислены сведения о задержке hello для отчетов об активности.</span><span class="sxs-lookup"><span data-stu-id="b161d-111">hello following table lists hello latency information for activity reports.</span></span>

| <span data-ttu-id="b161d-112">Отчет</span><span class="sxs-lookup"><span data-stu-id="b161d-112">Report</span></span> | <span data-ttu-id="b161d-113">Минимальная</span><span class="sxs-lookup"><span data-stu-id="b161d-113">Minimum</span></span> | <span data-ttu-id="b161d-114">Средняя</span><span class="sxs-lookup"><span data-stu-id="b161d-114">Average</span></span> | <span data-ttu-id="b161d-115">Максимальная</span><span class="sxs-lookup"><span data-stu-id="b161d-115">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="b161d-116">Журналы аудита</span><span class="sxs-lookup"><span data-stu-id="b161d-116">Audit logs</span></span>             | <span data-ttu-id="b161d-117">30 минут</span><span class="sxs-lookup"><span data-stu-id="b161d-117">30 minutes</span></span>  | <span data-ttu-id="b161d-118">45 минут</span><span class="sxs-lookup"><span data-stu-id="b161d-118">45 Minutes</span></span> | <span data-ttu-id="b161d-119">1 час</span><span class="sxs-lookup"><span data-stu-id="b161d-119">1 hour</span></span>     |
| <span data-ttu-id="b161d-120">Вход в систему</span><span class="sxs-lookup"><span data-stu-id="b161d-120">Sign-ins</span></span>               | <span data-ttu-id="b161d-121">15 минут</span><span class="sxs-lookup"><span data-stu-id="b161d-121">15 minutes</span></span>  | <span data-ttu-id="b161d-122">15 минут</span><span class="sxs-lookup"><span data-stu-id="b161d-122">15 minutes</span></span> | <span data-ttu-id="b161d-123">2 часа*</span><span class="sxs-lookup"><span data-stu-id="b161d-123">2 hours*</span></span>   |

>[!NOTE]
> <span data-ttu-id="b161d-124">Некоторые данные действия входа в систему, поступающих от приложений прежних версий office может потребоваться too8 часов для hello, передает данные tooshow отчеты.</span><span class="sxs-lookup"><span data-stu-id="b161d-124">For some sign-ins activity data coming from legacy office applications, it can take too8 hours for hello reporting data tooshow up.</span></span> 


## <a name="security-reports"></a><span data-ttu-id="b161d-125">Отчеты о безопасности</span><span class="sxs-lookup"><span data-stu-id="b161d-125">Security reports</span></span>

<span data-ttu-id="b161d-126">Есть две области отчетов о безопасности:</span><span class="sxs-lookup"><span data-stu-id="b161d-126">There are two areas of security reporting:</span></span>

- <span data-ttu-id="b161d-127">**Рискованные входы** -рискованным вход является показателем для попытки входа, возможно, выполнены с тем, кто не hello законный владельцем учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="b161d-127">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> 
- <span data-ttu-id="b161d-128">**Пользователи, находящиеся в группе риска**. Такая пометка означает, что конфиденциальность учетной записи пользователя, возможно, нарушена.</span><span class="sxs-lookup"><span data-stu-id="b161d-128">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> 

<span data-ttu-id="b161d-129">Hello в следующей таблице перечислены сведения о задержке hello безопасности отчетов.</span><span class="sxs-lookup"><span data-stu-id="b161d-129">hello following table lists hello latency information for security reports.</span></span>

| <span data-ttu-id="b161d-130">Отчет</span><span class="sxs-lookup"><span data-stu-id="b161d-130">Report</span></span> | <span data-ttu-id="b161d-131">Минимальная</span><span class="sxs-lookup"><span data-stu-id="b161d-131">Minimum</span></span> | <span data-ttu-id="b161d-132">Средняя</span><span class="sxs-lookup"><span data-stu-id="b161d-132">Average</span></span> | <span data-ttu-id="b161d-133">Максимальная</span><span class="sxs-lookup"><span data-stu-id="b161d-133">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="b161d-134">пользователи под угрозой;</span><span class="sxs-lookup"><span data-stu-id="b161d-134">Users at risk</span></span>          | <span data-ttu-id="b161d-135">5 мин</span><span class="sxs-lookup"><span data-stu-id="b161d-135">5 minutes</span></span>   | <span data-ttu-id="b161d-136">15 минут</span><span class="sxs-lookup"><span data-stu-id="b161d-136">15 minutes</span></span>  | <span data-ttu-id="b161d-137">2 ч</span><span class="sxs-lookup"><span data-stu-id="b161d-137">2 hours</span></span>  |
| <span data-ttu-id="b161d-138">Вход, представляющий риск</span><span class="sxs-lookup"><span data-stu-id="b161d-138">Risky sign-ins</span></span>         | <span data-ttu-id="b161d-139">5 мин</span><span class="sxs-lookup"><span data-stu-id="b161d-139">5 minutes</span></span>   | <span data-ttu-id="b161d-140">15 минут</span><span class="sxs-lookup"><span data-stu-id="b161d-140">15 minutes</span></span>  | <span data-ttu-id="b161d-141">2 ч</span><span class="sxs-lookup"><span data-stu-id="b161d-141">2 hours</span></span>  |

## <a name="risk-events"></a><span data-ttu-id="b161d-142">События риска</span><span class="sxs-lookup"><span data-stu-id="b161d-142">Risk events</span></span>

<span data-ttu-id="b161d-143">Azure Active Directory использует адаптивный машинного обучения алгоритмов и эвристики toodetect подозрительные действия, которые являются связанные tooyour учетных записей пользователей.</span><span class="sxs-lookup"><span data-stu-id="b161d-143">Azure Active Directory uses adaptive machine learning algorithms and heuristics toodetect suspicious actions that are related tooyour user accounts.</span></span> <span data-ttu-id="b161d-144">Каждое обнаруженное подозрительное действие сохраняется в записи, которая называется событием риска.</span><span class="sxs-lookup"><span data-stu-id="b161d-144">Each detected suspicious action is stored in a record called risk event.</span></span>

<span data-ttu-id="b161d-145">Hello в следующей таблице перечислены сведения о задержке hello для событий риска.</span><span class="sxs-lookup"><span data-stu-id="b161d-145">hello following table lists hello latency information for risk events.</span></span>

| <span data-ttu-id="b161d-146">Отчет</span><span class="sxs-lookup"><span data-stu-id="b161d-146">Report</span></span> | <span data-ttu-id="b161d-147">Минимальная</span><span class="sxs-lookup"><span data-stu-id="b161d-147">Minimum</span></span> | <span data-ttu-id="b161d-148">Средняя</span><span class="sxs-lookup"><span data-stu-id="b161d-148">Average</span></span> | <span data-ttu-id="b161d-149">Максимальная</span><span class="sxs-lookup"><span data-stu-id="b161d-149">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="b161d-150">Попытки входа с анонимных IP-адресов</span><span class="sxs-lookup"><span data-stu-id="b161d-150">Sign-ins from anonymous IP addresses</span></span> |<span data-ttu-id="b161d-151">5 мин</span><span class="sxs-lookup"><span data-stu-id="b161d-151">5 minutes</span></span> |<span data-ttu-id="b161d-152">15 минут</span><span class="sxs-lookup"><span data-stu-id="b161d-152">15 Minutes</span></span> |<span data-ttu-id="b161d-153">2 ч</span><span class="sxs-lookup"><span data-stu-id="b161d-153">2 hours</span></span> |
| <span data-ttu-id="b161d-154">Попытки входа из неизвестных расположений</span><span class="sxs-lookup"><span data-stu-id="b161d-154">Sign-ins from unfamiliar locations</span></span> |<span data-ttu-id="b161d-155">5 мин</span><span class="sxs-lookup"><span data-stu-id="b161d-155">5 minutes</span></span> |<span data-ttu-id="b161d-156">15 минут</span><span class="sxs-lookup"><span data-stu-id="b161d-156">15 Minutes</span></span> |<span data-ttu-id="b161d-157">2 ч</span><span class="sxs-lookup"><span data-stu-id="b161d-157">2 hours</span></span> |
| <span data-ttu-id="b161d-158">Пользователи с утерянными учетными данными</span><span class="sxs-lookup"><span data-stu-id="b161d-158">Users with leaked credentials</span></span> |<span data-ttu-id="b161d-159">2 ч</span><span class="sxs-lookup"><span data-stu-id="b161d-159">2 hours</span></span> |<span data-ttu-id="b161d-160">4 ч</span><span class="sxs-lookup"><span data-stu-id="b161d-160">4 hours</span></span> |<span data-ttu-id="b161d-161">8 ч</span><span class="sxs-lookup"><span data-stu-id="b161d-161">8 hours</span></span> |
| <span data-ttu-id="b161d-162">Невозможно tooatypical местоположений</span><span class="sxs-lookup"><span data-stu-id="b161d-162">Impossible travel tooatypical locations</span></span> |<span data-ttu-id="b161d-163">5 мин</span><span class="sxs-lookup"><span data-stu-id="b161d-163">5 minutes</span></span> |<span data-ttu-id="b161d-164">1 час</span><span class="sxs-lookup"><span data-stu-id="b161d-164">1 hour</span></span> |<span data-ttu-id="b161d-165">8 ч</span><span class="sxs-lookup"><span data-stu-id="b161d-165">8 hours</span></span>  |
| <span data-ttu-id="b161d-166">Попытки входа с инфицированных устройств</span><span class="sxs-lookup"><span data-stu-id="b161d-166">Sign-ins from infected devices</span></span> |<span data-ttu-id="b161d-167">2 ч</span><span class="sxs-lookup"><span data-stu-id="b161d-167">2 hours</span></span> |<span data-ttu-id="b161d-168">4 ч</span><span class="sxs-lookup"><span data-stu-id="b161d-168">4 hours</span></span> |<span data-ttu-id="b161d-169">8 ч</span><span class="sxs-lookup"><span data-stu-id="b161d-169">8 hours</span></span>  |
| <span data-ttu-id="b161d-170">Попытки входа с IP-адресов с подозрительными действиями</span><span class="sxs-lookup"><span data-stu-id="b161d-170">Sign-ins from IP addresses with suspicious activity</span></span> |<span data-ttu-id="b161d-171">2 ч</span><span class="sxs-lookup"><span data-stu-id="b161d-171">2 hours</span></span> |<span data-ttu-id="b161d-172">4 ч</span><span class="sxs-lookup"><span data-stu-id="b161d-172">4 hours</span></span> |<span data-ttu-id="b161d-173">8 ч</span><span class="sxs-lookup"><span data-stu-id="b161d-173">8 hours</span></span>  |



## <a name="next-steps"></a><span data-ttu-id="b161d-174">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b161d-174">Next steps</span></span>

<span data-ttu-id="b161d-175">Если tooknow дополнительные hello об отчетах об активности в hello портал Azure, см.:</span><span class="sxs-lookup"><span data-stu-id="b161d-175">If you want tooknow more about hello activity reports in hello Azure portal, see:</span></span>

- [<span data-ttu-id="b161d-176">Отчеты действия при входе в портал hello Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b161d-176">Sign-in activity reports in hello Azure Active Directory portal</span></span>](active-directory-reporting-activity-sign-ins.md)
- [<span data-ttu-id="b161d-177">Отчеты о действиях на портале Azure Active Directory hello аудита</span><span class="sxs-lookup"><span data-stu-id="b161d-177">Audit activity reports in hello Azure Active Directory portal</span></span>](active-directory-reporting-activity-audit-logs.md)

<span data-ttu-id="b161d-178">Если вы хотите tooknow Дополнительные сведения об отчетах безопасности hello в hello портал Azure, см.:</span><span class="sxs-lookup"><span data-stu-id="b161d-178">If you want tooknow more about hello security reports in hello Azure portal, see:</span></span>

- [<span data-ttu-id="b161d-179">Пользователи на риск безопасности отчетов на портале Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="b161d-179">Users at risk security report in hello Azure Active Directory portal</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="b161d-180">Рискованные входы отчетов на портале Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="b161d-180">Risky sign-ins report in hello Azure Active Directory portal</span></span>](active-directory-reporting-security-risky-sign-ins.md)

<span data-ttu-id="b161d-181">Дополнительные сведения о событиях риска tooknow см [событий риска Azure Active Directory](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="b161d-181">If you want tooknow more about risk events, see [Azure Active Directory risk events](active-directory-reporting-risk-events.md).</span></span>
