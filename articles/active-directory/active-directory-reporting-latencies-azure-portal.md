---
title: "Задержки в отчетах Azure Active Directory | Документация Майкрософт"
description: "Узнайте, сколько времени необходимо для отображения событий отчетов на портале Azure."
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
ms.openlocfilehash: 93cb0baeab8f13f81257ed1bd32ed08561c54b72
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-reporting-latencies"></a><span data-ttu-id="77c3d-103">Задержки в отчетах Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="77c3d-103">Azure Active Directory reporting latencies</span></span>

<span data-ttu-id="77c3d-104">Функция [отчетов](active-directory-preview-explainer.md) в Azure Active Directory позволяет получать всю необходимую информацию, чтобы определить, как работает среда.</span><span class="sxs-lookup"><span data-stu-id="77c3d-104">With [reporting](active-directory-preview-explainer.md) in the Azure Active Directory, you get all the information you need to determine how your environment is doing.</span></span> <span data-ttu-id="77c3d-105">Время, затрачиваемое для отображения данных отчетов на портале Azure, также называется задержкой.</span><span class="sxs-lookup"><span data-stu-id="77c3d-105">The amount of time it takes for reporting data to show up in the Azure portal is also known as latency.</span></span> 

<span data-ttu-id="77c3d-106">В этой статье приведены сведения о задержках для всех категорий отчетов на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="77c3d-106">This topic lists the latency information for the all reporting categories in the Azure portal.</span></span> 


## <a name="activity-reports"></a><span data-ttu-id="77c3d-107">Отчеты об активности</span><span class="sxs-lookup"><span data-stu-id="77c3d-107">Activity reports</span></span>

<span data-ttu-id="77c3d-108">Есть две области отчетов об активности:</span><span class="sxs-lookup"><span data-stu-id="77c3d-108">There are two areas of activity reporting:</span></span>

- <span data-ttu-id="77c3d-109">**Действия входа** — информация об использовании управляемых приложений и действиях входа.</span><span class="sxs-lookup"><span data-stu-id="77c3d-109">**Sign-in activities** – Information about the usage of managed applications and user sign-in activities</span></span>
- <span data-ttu-id="77c3d-110">**Журналы аудита** — информация системных операций об управлении пользователями и группами, об управляемых приложениях и действиях каталогов.</span><span class="sxs-lookup"><span data-stu-id="77c3d-110">**Audit logs** - System activity information about users and group management, your managed applications and directory activities</span></span>

<span data-ttu-id="77c3d-111">В следующей таблице приведены сведения о задержках для отчетов об активности.</span><span class="sxs-lookup"><span data-stu-id="77c3d-111">The following table lists the latency information for activity reports.</span></span>

| <span data-ttu-id="77c3d-112">Отчет</span><span class="sxs-lookup"><span data-stu-id="77c3d-112">Report</span></span> | <span data-ttu-id="77c3d-113">Минимальная</span><span class="sxs-lookup"><span data-stu-id="77c3d-113">Minimum</span></span> | <span data-ttu-id="77c3d-114">Средняя</span><span class="sxs-lookup"><span data-stu-id="77c3d-114">Average</span></span> | <span data-ttu-id="77c3d-115">Максимальная</span><span class="sxs-lookup"><span data-stu-id="77c3d-115">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="77c3d-116">Журналы аудита</span><span class="sxs-lookup"><span data-stu-id="77c3d-116">Audit logs</span></span>             | <span data-ttu-id="77c3d-117">30 минут</span><span class="sxs-lookup"><span data-stu-id="77c3d-117">30 minutes</span></span>  | <span data-ttu-id="77c3d-118">45 минут</span><span class="sxs-lookup"><span data-stu-id="77c3d-118">45 Minutes</span></span> | <span data-ttu-id="77c3d-119">1 час</span><span class="sxs-lookup"><span data-stu-id="77c3d-119">1 hour</span></span>     |
| <span data-ttu-id="77c3d-120">Вход в систему</span><span class="sxs-lookup"><span data-stu-id="77c3d-120">Sign-ins</span></span>               | <span data-ttu-id="77c3d-121">15 минут</span><span class="sxs-lookup"><span data-stu-id="77c3d-121">15 minutes</span></span>  | <span data-ttu-id="77c3d-122">15 минут</span><span class="sxs-lookup"><span data-stu-id="77c3d-122">15 minutes</span></span> | <span data-ttu-id="77c3d-123">2 часа*</span><span class="sxs-lookup"><span data-stu-id="77c3d-123">2 hours*</span></span>   |

>[!NOTE]
> <span data-ttu-id="77c3d-124">Для некоторых данных активности входа в систему, поступающих из устаревших приложений Office, может потребоваться до 8 часов, чтобы данные отчетов отобразились.</span><span class="sxs-lookup"><span data-stu-id="77c3d-124">For some sign-ins activity data coming from legacy office applications, it can take to 8 hours for the reporting data to show up.</span></span> 


## <a name="security-reports"></a><span data-ttu-id="77c3d-125">Отчеты о безопасности</span><span class="sxs-lookup"><span data-stu-id="77c3d-125">Security reports</span></span>

<span data-ttu-id="77c3d-126">Есть две области отчетов о безопасности:</span><span class="sxs-lookup"><span data-stu-id="77c3d-126">There are two areas of security reporting:</span></span>

- <span data-ttu-id="77c3d-127">**Входы, представляющие риск**. Вход, представляющий риск, означает, что в систему пытался войти пользователь, который не является законным владельцем учетной записи.</span><span class="sxs-lookup"><span data-stu-id="77c3d-127">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span></span> 
- <span data-ttu-id="77c3d-128">**Пользователи, находящиеся в группе риска**. Такая пометка означает, что конфиденциальность учетной записи пользователя, возможно, нарушена.</span><span class="sxs-lookup"><span data-stu-id="77c3d-128">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> 

<span data-ttu-id="77c3d-129">В следующей таблице приведены сведения о задержках для отчетов о безопасности.</span><span class="sxs-lookup"><span data-stu-id="77c3d-129">The following table lists the latency information for security reports.</span></span>

| <span data-ttu-id="77c3d-130">Отчет</span><span class="sxs-lookup"><span data-stu-id="77c3d-130">Report</span></span> | <span data-ttu-id="77c3d-131">Минимальная</span><span class="sxs-lookup"><span data-stu-id="77c3d-131">Minimum</span></span> | <span data-ttu-id="77c3d-132">Средняя</span><span class="sxs-lookup"><span data-stu-id="77c3d-132">Average</span></span> | <span data-ttu-id="77c3d-133">Максимальная</span><span class="sxs-lookup"><span data-stu-id="77c3d-133">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="77c3d-134">пользователи под угрозой;</span><span class="sxs-lookup"><span data-stu-id="77c3d-134">Users at risk</span></span>          | <span data-ttu-id="77c3d-135">5 мин</span><span class="sxs-lookup"><span data-stu-id="77c3d-135">5 minutes</span></span>   | <span data-ttu-id="77c3d-136">15 минут</span><span class="sxs-lookup"><span data-stu-id="77c3d-136">15 minutes</span></span>  | <span data-ttu-id="77c3d-137">2 ч</span><span class="sxs-lookup"><span data-stu-id="77c3d-137">2 hours</span></span>  |
| <span data-ttu-id="77c3d-138">Вход, представляющий риск</span><span class="sxs-lookup"><span data-stu-id="77c3d-138">Risky sign-ins</span></span>         | <span data-ttu-id="77c3d-139">5 мин</span><span class="sxs-lookup"><span data-stu-id="77c3d-139">5 minutes</span></span>   | <span data-ttu-id="77c3d-140">15 минут</span><span class="sxs-lookup"><span data-stu-id="77c3d-140">15 minutes</span></span>  | <span data-ttu-id="77c3d-141">2 ч</span><span class="sxs-lookup"><span data-stu-id="77c3d-141">2 hours</span></span>  |

## <a name="risk-events"></a><span data-ttu-id="77c3d-142">События риска</span><span class="sxs-lookup"><span data-stu-id="77c3d-142">Risk events</span></span>

<span data-ttu-id="77c3d-143">Azure Active Directory использует адаптивные алгоритмы машинного обучения и эвристические методы, чтобы обнаруживать подозрительные действия, связанные с вашими учетными записями.</span><span class="sxs-lookup"><span data-stu-id="77c3d-143">Azure Active Directory uses adaptive machine learning algorithms and heuristics to detect suspicious actions that are related to your user accounts.</span></span> <span data-ttu-id="77c3d-144">Каждое обнаруженное подозрительное действие сохраняется в записи, которая называется событием риска.</span><span class="sxs-lookup"><span data-stu-id="77c3d-144">Each detected suspicious action is stored in a record called risk event.</span></span>

<span data-ttu-id="77c3d-145">В следующей таблице приведены сведения о задержках для событий риска.</span><span class="sxs-lookup"><span data-stu-id="77c3d-145">The following table lists the latency information for risk events.</span></span>

| <span data-ttu-id="77c3d-146">Отчет</span><span class="sxs-lookup"><span data-stu-id="77c3d-146">Report</span></span> | <span data-ttu-id="77c3d-147">Минимальная</span><span class="sxs-lookup"><span data-stu-id="77c3d-147">Minimum</span></span> | <span data-ttu-id="77c3d-148">Средняя</span><span class="sxs-lookup"><span data-stu-id="77c3d-148">Average</span></span> | <span data-ttu-id="77c3d-149">Максимальная</span><span class="sxs-lookup"><span data-stu-id="77c3d-149">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="77c3d-150">Попытки входа с анонимных IP-адресов</span><span class="sxs-lookup"><span data-stu-id="77c3d-150">Sign-ins from anonymous IP addresses</span></span> |<span data-ttu-id="77c3d-151">5 мин</span><span class="sxs-lookup"><span data-stu-id="77c3d-151">5 minutes</span></span> |<span data-ttu-id="77c3d-152">15 минут</span><span class="sxs-lookup"><span data-stu-id="77c3d-152">15 Minutes</span></span> |<span data-ttu-id="77c3d-153">2 ч</span><span class="sxs-lookup"><span data-stu-id="77c3d-153">2 hours</span></span> |
| <span data-ttu-id="77c3d-154">Попытки входа из неизвестных расположений</span><span class="sxs-lookup"><span data-stu-id="77c3d-154">Sign-ins from unfamiliar locations</span></span> |<span data-ttu-id="77c3d-155">5 мин</span><span class="sxs-lookup"><span data-stu-id="77c3d-155">5 minutes</span></span> |<span data-ttu-id="77c3d-156">15 минут</span><span class="sxs-lookup"><span data-stu-id="77c3d-156">15 Minutes</span></span> |<span data-ttu-id="77c3d-157">2 ч</span><span class="sxs-lookup"><span data-stu-id="77c3d-157">2 hours</span></span> |
| <span data-ttu-id="77c3d-158">Пользователи с утерянными учетными данными</span><span class="sxs-lookup"><span data-stu-id="77c3d-158">Users with leaked credentials</span></span> |<span data-ttu-id="77c3d-159">2 ч</span><span class="sxs-lookup"><span data-stu-id="77c3d-159">2 hours</span></span> |<span data-ttu-id="77c3d-160">4 ч</span><span class="sxs-lookup"><span data-stu-id="77c3d-160">4 hours</span></span> |<span data-ttu-id="77c3d-161">8 ч</span><span class="sxs-lookup"><span data-stu-id="77c3d-161">8 hours</span></span> |
| <span data-ttu-id="77c3d-162">Невозможно переместиться в нетипичные расположения</span><span class="sxs-lookup"><span data-stu-id="77c3d-162">Impossible travel to atypical locations</span></span> |<span data-ttu-id="77c3d-163">5 мин</span><span class="sxs-lookup"><span data-stu-id="77c3d-163">5 minutes</span></span> |<span data-ttu-id="77c3d-164">1 час</span><span class="sxs-lookup"><span data-stu-id="77c3d-164">1 hour</span></span> |<span data-ttu-id="77c3d-165">8 ч</span><span class="sxs-lookup"><span data-stu-id="77c3d-165">8 hours</span></span>  |
| <span data-ttu-id="77c3d-166">Попытки входа с инфицированных устройств</span><span class="sxs-lookup"><span data-stu-id="77c3d-166">Sign-ins from infected devices</span></span> |<span data-ttu-id="77c3d-167">2 ч</span><span class="sxs-lookup"><span data-stu-id="77c3d-167">2 hours</span></span> |<span data-ttu-id="77c3d-168">4 ч</span><span class="sxs-lookup"><span data-stu-id="77c3d-168">4 hours</span></span> |<span data-ttu-id="77c3d-169">8 ч</span><span class="sxs-lookup"><span data-stu-id="77c3d-169">8 hours</span></span>  |
| <span data-ttu-id="77c3d-170">Попытки входа с IP-адресов с подозрительными действиями</span><span class="sxs-lookup"><span data-stu-id="77c3d-170">Sign-ins from IP addresses with suspicious activity</span></span> |<span data-ttu-id="77c3d-171">2 ч</span><span class="sxs-lookup"><span data-stu-id="77c3d-171">2 hours</span></span> |<span data-ttu-id="77c3d-172">4 ч</span><span class="sxs-lookup"><span data-stu-id="77c3d-172">4 hours</span></span> |<span data-ttu-id="77c3d-173">8 ч</span><span class="sxs-lookup"><span data-stu-id="77c3d-173">8 hours</span></span>  |



## <a name="next-steps"></a><span data-ttu-id="77c3d-174">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="77c3d-174">Next steps</span></span>

<span data-ttu-id="77c3d-175">Чтобы узнать больше про отчеты об активности на портале Azure, см. следующие статьи:</span><span class="sxs-lookup"><span data-stu-id="77c3d-175">If you want to know more about the activity reports in the Azure portal, see:</span></span>

- [<span data-ttu-id="77c3d-176">Отчеты о действиях входа на портале Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="77c3d-176">Sign-in activity reports in the Azure Active Directory portal</span></span>](active-directory-reporting-activity-sign-ins.md)
- [<span data-ttu-id="77c3d-177">Отчеты о действиях аудита на портале Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="77c3d-177">Audit activity reports in the Azure Active Directory portal</span></span>](active-directory-reporting-activity-audit-logs.md)

<span data-ttu-id="77c3d-178">Чтобы узнать больше про отчеты о безопасности на портале Azure, см. следующие статьи:</span><span class="sxs-lookup"><span data-stu-id="77c3d-178">If you want to know more about the security reports in the Azure portal, see:</span></span>

- [<span data-ttu-id="77c3d-179">Отчет системы безопасности о пользователях под угрозой на портале Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="77c3d-179">Users at risk security report in the Azure Active Directory portal</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="77c3d-180">Отчет о событиях входа, представляющих риск, на портале Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="77c3d-180">Risky sign-ins report in the Azure Active Directory portal</span></span>](active-directory-reporting-security-risky-sign-ins.md)

<span data-ttu-id="77c3d-181">Чтобы узнать больше про события риска, см. статью о [событиях риска в Azure Active Directory](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="77c3d-181">If you want to know more about risk events, see [Azure Active Directory risk events](active-directory-reporting-risk-events.md).</span></span>
