---
title: "Рабочие процессы утверждения при управлении привилегированными пользователями Azure | Документация Майкрософт"
description: "Узнайте о рабочих процессах утверждения при управлении привилегированными пользователями (PIM)."
services: active-directory
documentationcenter: 
author: barclayn
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2017
ms.author: barclayn
ms.custom: pim
ms.openlocfilehash: cf6a9213fa0a1cba8725aabb42abe51b805ece7a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="approvals-preview"></a><span data-ttu-id="80b9e-103">Утверждения (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="80b9e-103">Approvals (Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="80b9e-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="80b9e-104">Overview</span></span>

<span data-ttu-id="80b9e-105">С помощью утверждений для управления привилегированными пользователями можно настроить роли, чтобы требовать утверждения при активации, а также выбрать одного или несколько пользователей или групп в качестве делегированных утверждающих лиц.</span><span class="sxs-lookup"><span data-stu-id="80b9e-105">With Approvals for Privileged Identity Management, you can configure roles to require approval for activation, and choose one or multiple users or groups as delegated approvers.</span></span> <span data-ttu-id="80b9e-106">Читайте дальше, чтобы узнать о настройке ролей и выборе утверждающих лиц.</span><span class="sxs-lookup"><span data-stu-id="80b9e-106">Keep reading to learn how to configure roles and select approvers.</span></span>

>[!NOTE]
<span data-ttu-id="80b9e-107">Необходимо учитывать, что эта функция еще находится в разработке, поэтому в ней могут возникать ошибки.</span><span class="sxs-lookup"><span data-stu-id="80b9e-107">Please keep in mind this feature is still in development, and you may encounter bugs.</span></span> <span data-ttu-id="80b9e-108">Функциональные возможности, включая текст и соглашения об именовании, могут измениться и не должны считаться окончательными.</span><span class="sxs-lookup"><span data-stu-id="80b9e-108">The functionality, including text and naming conventions are subject to change, and should not be considered final.</span></span>


## <a name="key-terminology"></a><span data-ttu-id="80b9e-109">Ключевые термины</span><span class="sxs-lookup"><span data-stu-id="80b9e-109">Key Terminology</span></span>

<span data-ttu-id="80b9e-110">*Пользователь с временной ролью* — это пользователь в организации, которому назначена роль Azure AD на условиях временной роли (требует активации).</span><span class="sxs-lookup"><span data-stu-id="80b9e-110">*Eligible Role User* – An eligible role user is a user within your organization that’s been assigned to an Azure AD role as eligible (role requires activation).</span></span>

<span data-ttu-id="80b9e-111">*Делегированное утверждающее лицо* — это один или несколько индивидуальных пользователей или групп в Azure AD, которые отвечают за утверждение запросов на активацию ролей.</span><span class="sxs-lookup"><span data-stu-id="80b9e-111">*Delegated Approver* – A delegated approver is one or multiple individuals or groups within your Azure AD who are responsible for approving requests for role activation.</span></span>

## <a name="scenarios"></a><span data-ttu-id="80b9e-112">Сценарии</span><span class="sxs-lookup"><span data-stu-id="80b9e-112">Scenarios</span></span>

<span data-ttu-id="80b9e-113">Закрытая предварительная версия поддерживает описанные ниже сценарии.</span><span class="sxs-lookup"><span data-stu-id="80b9e-113">The private preview supports the following scenarios:</span></span>

<span data-ttu-id="80b9e-114">**В качестве администратора привилегированных ролей вы можете выполнить следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="80b9e-114">**As a Privileged Role Administrator (PRA) you can:**</span></span>

-   <span data-ttu-id="80b9e-115">[включить утверждения для конкретных ролей](#enable-approval-for-specific-roles);</span><span class="sxs-lookup"><span data-stu-id="80b9e-115">[enable approval for specific roles](#enable-approval-for-specific-roles)</span></span>

-   <span data-ttu-id="80b9e-116">[указать утверждающих лиц и (или) группы с правом утверждения запросов](#specify-approver-users-and/or-groups-to-approve-requests);</span><span class="sxs-lookup"><span data-stu-id="80b9e-116">[specify approver users and/or groups to approve requests](#specify-approver-users-and/or-groups-to-approve-requests)</span></span>

-   <span data-ttu-id="80b9e-117">[просмотреть историю запросов и утверждений для всех привилегированных ролей](#view-request-and-approval-history-for-all-privileged-roles).</span><span class="sxs-lookup"><span data-stu-id="80b9e-117">[view request and approval history for all privileged roles](#view-request-and-approval-history-for-all-privileged-roles)</span></span>

<span data-ttu-id="80b9e-118">**В качестве назначенного утверждающего лица вы можете выполнить следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="80b9e-118">**As a designated approver, you can:**</span></span>

-   <span data-ttu-id="80b9e-119">[просмотреть запросы, ожидающие утверждения](#view-pending-approvals-requests);</span><span class="sxs-lookup"><span data-stu-id="80b9e-119">[view pending approvals (requests)](#view-pending-approvals-requests)</span></span>

-   <span data-ttu-id="80b9e-120">[утвердить или отклонить запросы на повышение роли (по одному и (или) массово)](#approve-or-reject-requests-for-role-elevation-single-and/or-bulk);</span><span class="sxs-lookup"><span data-stu-id="80b9e-120">[approve or reject requests for role elevation (single and/or bulk)](#approve-or-reject-requests-for-role-elevation-single-and/or-bulk)</span></span>

-   <span data-ttu-id="80b9e-121">[указать обоснование для своего утверждения или отказа](#provide-justification-for-my-approval/rejection).</span><span class="sxs-lookup"><span data-stu-id="80b9e-121">[provide justification for my approval/rejection](#provide-justification-for-my-approval/rejection)</span></span> 

<span data-ttu-id="80b9e-122">**В качестве пользователя с временной ролью вы можете выполнить следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="80b9e-122">**As an Eligible Role User you can:**</span></span>

-   <span data-ttu-id="80b9e-123">[запросить активацию роли, для которой требуется утверждение](#request-activation-of-a-role-that-requires-approval);</span><span class="sxs-lookup"><span data-stu-id="80b9e-123">[request activation of a role that requires approval](#request-activation-of-a-role-that-requires-approval)</span></span>

-   <span data-ttu-id="80b9e-124">[просмотреть состояние запроса на активацию](#view-the-status-of-your-request-to-activate);</span><span class="sxs-lookup"><span data-stu-id="80b9e-124">[view the status of your request to activate](#view-the-status-of-your-request-to-activate)</span></span>

-   <span data-ttu-id="80b9e-125">[выполнить задачу в Azure AD, если запрос на активацию утвержден](#complete-your-task-in-azure-ad-if-activation-was-approved).</span><span class="sxs-lookup"><span data-stu-id="80b9e-125">[complete your task in Azure AD if activation was approved](#complete-your-task-in-azure-ad-if-activation-was-approved)</span></span>

### <a name="navigation"></a><span data-ttu-id="80b9e-126">Навигации</span><span class="sxs-lookup"><span data-stu-id="80b9e-126">Navigation</span></span>

<span data-ttu-id="80b9e-127">Мы обновили меню навигации для поддержки функции утверждений.</span><span class="sxs-lookup"><span data-stu-id="80b9e-127">We've updated the navigation to support approvals</span></span>

![](media/azure-ad-pim-approval-workflow/image001.png)

<span data-ttu-id="80b9e-128">Целевая страница по умолчанию предоставляет удобный доступ к сведениям о PIM и новой документации по утверждениям.</span><span class="sxs-lookup"><span data-stu-id="80b9e-128">The default landing page provides convenient access to information about PIM and the new approvals documentation.</span></span>

![](media/azure-ad-pim-approval-workflow/image002.png)

<span data-ttu-id="80b9e-129">Мы также добавили новый раздел для всех пользователей PIM — "My Audit History" (Мой журнал аудита).</span><span class="sxs-lookup"><span data-stu-id="80b9e-129">We’ve also added a new section for all users of PIM, ‘My Audit History’.</span></span> <span data-ttu-id="80b9e-130">Здесь вы можете найти все сведения, относящиеся к вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="80b9e-130">Here you can find all the information relevant to your identity.</span></span> <span data-ttu-id="80b9e-131">В частности, здесь содержатся все ожидающие и выполненные запросы, решения, принятые вами об утверждении запросов, а также все прошлые активации ролей. И все это удобно собрано в одном месте.</span><span class="sxs-lookup"><span data-stu-id="80b9e-131">This includes all your pending and completed requests, any decisions you’ve made about the requests you resolve, and all your past role activations in one convenient location.</span></span>

![](media/azure-ad-pim-approval-workflow/image003.png)

### <a name="enable-approval-for-specific-roles"></a><span data-ttu-id="80b9e-132">Включение утверждений для конкретных ролей</span><span class="sxs-lookup"><span data-stu-id="80b9e-132">Enable approval for specific roles</span></span>

<span data-ttu-id="80b9e-133">Чтобы применить процедуру утверждения для определенной роли, сначала выберите в левой области навигации "Azure AD Directory Roles" (Роли каталога Azure AD).</span><span class="sxs-lookup"><span data-stu-id="80b9e-133">To enable approval for a specific role, first select Directory Roles from the left navigation.</span></span>

![](media/azure-ad-pim-approval-workflow/image004.png)

<span data-ttu-id="80b9e-134">В открывшемся меню ролей каталога слева найдите и выберите пункт "Параметры".</span><span class="sxs-lookup"><span data-stu-id="80b9e-134">Find and select settings in the Directory Roles left navigation</span></span>

![](media/azure-ad-pim-approval-workflow/image006.png)

<span data-ttu-id="80b9e-135">Выберите привилегированные роли:</span><span class="sxs-lookup"><span data-stu-id="80b9e-135">Select privileged Roles:</span></span>

![](media/azure-ad-pim-approval-workflow/image009.png)

<span data-ttu-id="80b9e-136">В разделе "Требуется утверждение" выберите "Включить":</span><span class="sxs-lookup"><span data-stu-id="80b9e-136">Select “Enable” in the Require approval section:</span></span>

![](media/azure-ad-pim-approval-workflow/image011.png)

<span data-ttu-id="80b9e-137">После этого в колонке отобразятся следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="80b9e-137">Once enabled, the blade will expand to show the following details:</span></span>

![](media/azure-ad-pim-approval-workflow/image013.png)

>[!NOTE]
<span data-ttu-id="80b9e-138">Если НЕ указать ни одного утверждающего лица, то утверждающими лицами по умолчанию станут администраторы привилегированных ролей.</span><span class="sxs-lookup"><span data-stu-id="80b9e-138">If you DO NOT specify any approvers, the PRA(s) become the default approver(s).</span></span> <span data-ttu-id="80b9e-139">Администраторы привилегированных ролей должны будут утверждать ВСЕ запросы на активацию этой роли.</span><span class="sxs-lookup"><span data-stu-id="80b9e-139">PRA(s) would be required to approve ALL activation requests for this role.</span></span>

### <a name="specify-approver-users-andor-groups-to-approve-requests"></a><span data-ttu-id="80b9e-140">Указание утверждающих лиц и (или) групп с правом утверждения запросов</span><span class="sxs-lookup"><span data-stu-id="80b9e-140">Specify approver users and/or groups to approve requests</span></span>

<span data-ttu-id="80b9e-141">Чтобы делегировать права утверждения, щелкните "Выбор утверждающих лиц":</span><span class="sxs-lookup"><span data-stu-id="80b9e-141">To delegate approval, click the option to “Select approvers”:</span></span>

![](media/azure-ad-pim-approval-workflow/image015.png)

<span data-ttu-id="80b9e-142">Когда загрузится колонка "Выбор утверждающих лиц", вы можете найти определенного пользователя или группу с помощью панели поиска в верхней части колонки или выбрать их в предварительно заполненном списке. По завершении нажмите кнопку "Выбрать".</span><span class="sxs-lookup"><span data-stu-id="80b9e-142">When the Select approvers blade loads, you may search for a specific user or group using the search bar at the top, or selecting from the pre-populated list, then click “Select” when finished:</span></span>

![](media/azure-ad-pim-approval-workflow/image017.png)

<span data-ttu-id="80b9e-143">Примечание. За один раз можно выбрать несколько пользователей или групп.</span><span class="sxs-lookup"><span data-stu-id="80b9e-143">Note: You may select multiple users or groups at a time.</span></span>

<span data-ttu-id="80b9e-144">Выбранные вами элементы отобразятся в списке выбранных утверждающих лиц, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="80b9e-144">Your selection will appear in the list of selected approvers as seen below:</span></span>

![](media/azure-ad-pim-approval-workflow/image019.png)

<span data-ttu-id="80b9e-145">Чтобы удалить утверждающее лицо, просто нажмите кнопку "Удалить" рядом с соответствующим именем.</span><span class="sxs-lookup"><span data-stu-id="80b9e-145">To remove an approver, simply click the Remove button next to their name.</span></span>

<span data-ttu-id="80b9e-146">Чтобы добавить других утверждающих лиц, повторите эту процедуру.</span><span class="sxs-lookup"><span data-stu-id="80b9e-146">To add additional approvers, repeat the process.</span></span>

## <a name="view-request-and-approval-history-for-all-privileged-roles"></a><span data-ttu-id="80b9e-147">Просмотр истории запросов и утверждений для всех привилегированных ролей</span><span class="sxs-lookup"><span data-stu-id="80b9e-147">View request and approval history for all privileged roles</span></span>

<span data-ttu-id="80b9e-148">Чтобы просмотреть историю запросов и утверждений для всех привилегированных ролей, выберите на панели мониторинга пункт "Журнал аудита".</span><span class="sxs-lookup"><span data-stu-id="80b9e-148">To view request and approval history for all privileged roles, select Audit History from the dashboard:</span></span>

![](media/azure-ad-pim-approval-workflow/image021.png)

>[!NOTE]
<span data-ttu-id="80b9e-149">Данные можно отсортировать по действию и выбрать вариант "Активация утверждена".</span><span class="sxs-lookup"><span data-stu-id="80b9e-149">You can sort the data by Action, and look for “Activation Approved”</span></span>

### <a name="view-pending-approvals-requests"></a><span data-ttu-id="80b9e-150">Просмотр запросов, ожидающих утверждения</span><span class="sxs-lookup"><span data-stu-id="80b9e-150">View pending approvals (requests)</span></span>

<span data-ttu-id="80b9e-151">При наличии запроса, ожидающего вашего утверждения, вы, как делегированное утверждающее лицо, получите уведомление по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="80b9e-151">As a delegated approver, you’ll receive email notifications when a request is pending your approval.</span></span> <span data-ttu-id="80b9e-152">Чтобы просмотреть эти запросы на портале PIM, на панели мониторинга (в новом меню навигации) выберите вкладку "Ожидающие утверждения запросы" на левой панели навигации.</span><span class="sxs-lookup"><span data-stu-id="80b9e-152">To view these requests in the PIM portal, from the dashboard (in the new navigation) select the “Pending Approval Requests” tab in the left navigation bar.</span></span>

![](media/azure-ad-pim-approval-workflow/image023.png)

<span data-ttu-id="80b9e-153">Отобразится список запросов, ожидающих утверждения:</span><span class="sxs-lookup"><span data-stu-id="80b9e-153">From there, you’ll see a list of requests pending approval:</span></span>

![](media/azure-ad-pim-approval-workflow/image024.png)

### <a name="approve-or-reject-requests-for-role-elevation-single-andor-bulk"></a><span data-ttu-id="80b9e-154">Утверждение или отклонение запросов на повышение роли (по одному и (или) массово)</span><span class="sxs-lookup"><span data-stu-id="80b9e-154">Approve or reject requests for role elevation (single and/or bulk)</span></span>

<span data-ttu-id="80b9e-155">Выберите запросы, которые необходимо утвердить или отклонить, а затем нажмите кнопку на панели действий, которая соответствует вашему решению:</span><span class="sxs-lookup"><span data-stu-id="80b9e-155">Select the requests you wish to approve or deny, and click the button in the action bar that corresponds with your decision:</span></span>

![](media/azure-ad-pim-approval-workflow/image025.png)

### <a name="provide-justification-for-my-approvalrejection"></a><span data-ttu-id="80b9e-156">Указание обоснования для своего утверждения или отказа</span><span class="sxs-lookup"><span data-stu-id="80b9e-156">Provide justification for my approval/rejection</span></span>

<span data-ttu-id="80b9e-157">Откроется новая колонка, позволяющая утвердить или отклонить несколько запросов одновременно.</span><span class="sxs-lookup"><span data-stu-id="80b9e-157">This will open a new blade to approve or deny multiple requests at once.</span></span> <span data-ttu-id="80b9e-158">Введите обоснование своего решения и щелкните "Утвердить" (или "Отклонить") в нижней части колонки:</span><span class="sxs-lookup"><span data-stu-id="80b9e-158">Enter a justification for your decision, and click approve (or deny) at the bottom or the blade:</span></span>

![](media/azure-ad-pim-approval-workflow/image029.png)

<span data-ttu-id="80b9e-159">Когда запрос обработан, значок состояния отразит принятое решение (в данном примере — "Утвердить"):</span><span class="sxs-lookup"><span data-stu-id="80b9e-159">When the request process is complete, the status symbol will reflect the decision you made (in this example, the decision is approve):</span></span>

![](media/azure-ad-pim-approval-workflow/image031.png)

### <a name="request-activation-of-a-role-that-requires-approval"></a><span data-ttu-id="80b9e-160">Запрос активации роли, для которой требуется утверждение</span><span class="sxs-lookup"><span data-stu-id="80b9e-160">Request activation of a role that requires approval</span></span>

<span data-ttu-id="80b9e-161">Чтобы запросить активацию роли, для которой требуется утверждение, можно использовать как старое меню навигации PIM, так и новое, потому что процесс активации роли не изменился.</span><span class="sxs-lookup"><span data-stu-id="80b9e-161">Requesting activation of a role that requires approval may be initiated from either the old PIM navigation, or the new navigation, as the process for role activation remains the same.</span></span> <span data-ttu-id="80b9e-162">Просто выберите в списке роль, которую необходимо активировать:</span><span class="sxs-lookup"><span data-stu-id="80b9e-162">Simply select a role from the list of roles to activate:</span></span>

![](media/azure-ad-pim-approval-workflow/image033.png)

<span data-ttu-id="80b9e-163">Если для привилегированной роли требуется выполнение Многофакторной идентификации, то сначала отобразится соответствующий запрос:</span><span class="sxs-lookup"><span data-stu-id="80b9e-163">If a privileged role requires Multi-Factor Authentication, you’ll be prompted to complete that task first:</span></span>

![](media/azure-ad-pim-approval-workflow/image035.png)

<span data-ttu-id="80b9e-164">По завершении щелкните "Активировать" и укажите обоснование (при необходимости):</span><span class="sxs-lookup"><span data-stu-id="80b9e-164">Once complete, click Activate and provide a justification (if required):</span></span>

![](media/azure-ad-pim-approval-workflow/image037.png)

<span data-ttu-id="80b9e-165">Запросившая сторона получит уведомление о том, что запрос ожидает утверждения:</span><span class="sxs-lookup"><span data-stu-id="80b9e-165">The requestor will see a notification that the request is pending approval:</span></span>

![](media/azure-ad-pim-approval-workflow/image039.png)

### <a name="view-the-status-of-your-request-to-activate"></a><span data-ttu-id="80b9e-166">Просмотр состояния запроса на активацию</span><span class="sxs-lookup"><span data-stu-id="80b9e-166">View the status of your request to activate</span></span>

<span data-ttu-id="80b9e-167">Чтобы просмотреть состояние запроса на активацию, ожидающего утверждения, необходимо воспользоваться новым меню навигации.</span><span class="sxs-lookup"><span data-stu-id="80b9e-167">Viewing the status of a pending request to activate must be accessed from the new navigation.</span></span> <span data-ttu-id="80b9e-168">На левой панели навигации выберите вкладку "Мои запросы":</span><span class="sxs-lookup"><span data-stu-id="80b9e-168">From the left navigation bar, select the “My Requests” tab:</span></span>

![](media/azure-ad-pim-approval-workflow/image041.png)

<span data-ttu-id="80b9e-169">Состояние запроса по умолчанию — "Ожидание", но можно переключиться на просмотр всех или отклоненных запросов.</span><span class="sxs-lookup"><span data-stu-id="80b9e-169">The request state defaults to “Pending”, but you can toggle to see all or denied requests.</span></span>

### <a name="complete-your-task-in-azure-ad-if-activation-was-approved"></a><span data-ttu-id="80b9e-170">Выполнение задачи в Azure AD, если запрос на активацию утвержден</span><span class="sxs-lookup"><span data-stu-id="80b9e-170">Complete your task in Azure AD if activation was approved</span></span>

<span data-ttu-id="80b9e-171">После утверждения запроса роль становится активной, и можно выполнять любые действия, для которых требуется эта роль.</span><span class="sxs-lookup"><span data-stu-id="80b9e-171">Once the request is approved, the role is active and you may proceed with any work that requires this role.</span></span>

![](media/azure-ad-pim-approval-workflow/image043.png)

## <a name="next-steps"></a><span data-ttu-id="80b9e-172">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="80b9e-172">Next steps</span></span>

<span data-ttu-id="80b9e-173">Ваш отзыв очень важен для нас.</span><span class="sxs-lookup"><span data-stu-id="80b9e-173">Your feedback is valuable to us.</span></span> <span data-ttu-id="80b9e-174">Вы можете связаться с нами, оставив свои комментарии или отзывы здесь!</span><span class="sxs-lookup"><span data-stu-id="80b9e-174">Please feel free to share comments or feedback with us here!</span></span>
