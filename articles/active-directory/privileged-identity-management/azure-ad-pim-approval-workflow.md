---
title: "рабочие процессы утверждения управления привилегированных удостоверений aaaAzure | Документы Microsoft"
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
ms.openlocfilehash: 4afaf5c138798a803eb3d3b7905b9361d65792cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="approvals-preview"></a><span data-ttu-id="9bc91-103">Утверждения (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="9bc91-103">Approvals (Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="9bc91-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="9bc91-104">Overview</span></span>

<span data-ttu-id="9bc91-105">С утверждениями для управления привилегированными пользователями можно настроить утверждения ролей toorequire для активации и как делегированного утверждающих, выберите один или несколько пользователей или групп.</span><span class="sxs-lookup"><span data-stu-id="9bc91-105">With Approvals for Privileged Identity Management, you can configure roles toorequire approval for activation, and choose one or multiple users or groups as delegated approvers.</span></span> <span data-ttu-id="9bc91-106">Продолжить чтение toolearn как tooconfigure ролей и выбрать утверждающих.</span><span class="sxs-lookup"><span data-stu-id="9bc91-106">Keep reading toolearn how tooconfigure roles and select approvers.</span></span>

>[!NOTE]
<span data-ttu-id="9bc91-107">Необходимо учитывать, что эта функция еще находится в разработке, поэтому в ней могут возникать ошибки.</span><span class="sxs-lookup"><span data-stu-id="9bc91-107">Please keep in mind this feature is still in development, and you may encounter bugs.</span></span> <span data-ttu-id="9bc91-108">Hello функциональные возможности, включая текст соглашения об именовании могут быть изменены и не должен рассматриваться окончательного.</span><span class="sxs-lookup"><span data-stu-id="9bc91-108">hello functionality, including text and naming conventions are subject to change, and should not be considered final.</span></span>


## <a name="key-terminology"></a><span data-ttu-id="9bc91-109">Ключевые термины</span><span class="sxs-lookup"><span data-stu-id="9bc91-109">Key Terminology</span></span>

<span data-ttu-id="9bc91-110">*Право пользователя роли* — подходящие роли пользователя — это пользователь в вашей организации, которой была предоставлена роль tooan Azure AD в качестве соответствующих (роль требует активации).</span><span class="sxs-lookup"><span data-stu-id="9bc91-110">*Eligible Role User* – An eligible role user is a user within your organization that’s been assigned tooan Azure AD role as eligible (role requires activation).</span></span>

<span data-ttu-id="9bc91-111">*Делегированное утверждающее лицо* — это один или несколько индивидуальных пользователей или групп в Azure AD, которые отвечают за утверждение запросов на активацию ролей.</span><span class="sxs-lookup"><span data-stu-id="9bc91-111">*Delegated Approver* – A delegated approver is one or multiple individuals or groups within your Azure AD who are responsible for approving requests for role activation.</span></span>

## <a name="scenarios"></a><span data-ttu-id="9bc91-112">Сценарии</span><span class="sxs-lookup"><span data-stu-id="9bc91-112">Scenarios</span></span>

<span data-ttu-id="9bc91-113">Hello личной предварительной версии поддерживает hello следующие сценарии:</span><span class="sxs-lookup"><span data-stu-id="9bc91-113">hello private preview supports hello following scenarios:</span></span>

<span data-ttu-id="9bc91-114">**В качестве администратора привилегированных ролей вы можете выполнить следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="9bc91-114">**As a Privileged Role Administrator (PRA) you can:**</span></span>

-   <span data-ttu-id="9bc91-115">[включить утверждения для конкретных ролей](#enable-approval-for-specific-roles);</span><span class="sxs-lookup"><span data-stu-id="9bc91-115">[enable approval for specific roles](#enable-approval-for-specific-roles)</span></span>

-   [<span data-ttu-id="9bc91-116">Укажите утверждающего запросов tooapprove пользователей или групп</span><span class="sxs-lookup"><span data-stu-id="9bc91-116">specify approver users and/or groups tooapprove requests</span></span>](#specify-approver-users-and/or-groups-to-approve-requests)

-   <span data-ttu-id="9bc91-117">[просмотреть историю запросов и утверждений для всех привилегированных ролей](#view-request-and-approval-history-for-all-privileged-roles).</span><span class="sxs-lookup"><span data-stu-id="9bc91-117">[view request and approval history for all privileged roles](#view-request-and-approval-history-for-all-privileged-roles)</span></span>

<span data-ttu-id="9bc91-118">**В качестве назначенного утверждающего лица вы можете выполнить следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="9bc91-118">**As a designated approver, you can:**</span></span>

-   <span data-ttu-id="9bc91-119">[просмотреть запросы, ожидающие утверждения](#view-pending-approvals-requests);</span><span class="sxs-lookup"><span data-stu-id="9bc91-119">[view pending approvals (requests)](#view-pending-approvals-requests)</span></span>

-   <span data-ttu-id="9bc91-120">[утвердить или отклонить запросы на повышение роли (по одному и (или) массово)](#approve-or-reject-requests-for-role-elevation-single-and/or-bulk);</span><span class="sxs-lookup"><span data-stu-id="9bc91-120">[approve or reject requests for role elevation (single and/or bulk)](#approve-or-reject-requests-for-role-elevation-single-and/or-bulk)</span></span>

-   <span data-ttu-id="9bc91-121">[указать обоснование для своего утверждения или отказа](#provide-justification-for-my-approval/rejection).</span><span class="sxs-lookup"><span data-stu-id="9bc91-121">[provide justification for my approval/rejection](#provide-justification-for-my-approval/rejection)</span></span> 

<span data-ttu-id="9bc91-122">**В качестве пользователя с временной ролью вы можете выполнить следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="9bc91-122">**As an Eligible Role User you can:**</span></span>

-   <span data-ttu-id="9bc91-123">[запросить активацию роли, для которой требуется утверждение](#request-activation-of-a-role-that-requires-approval);</span><span class="sxs-lookup"><span data-stu-id="9bc91-123">[request activation of a role that requires approval](#request-activation-of-a-role-that-requires-approval)</span></span>

-   [<span data-ttu-id="9bc91-124">Просмотр состояния hello tooactivate вашего запроса</span><span class="sxs-lookup"><span data-stu-id="9bc91-124">view hello status of your request tooactivate</span></span>](#view-the-status-of-your-request-to-activate)

-   <span data-ttu-id="9bc91-125">[выполнить задачу в Azure AD, если запрос на активацию утвержден](#complete-your-task-in-azure-ad-if-activation-was-approved).</span><span class="sxs-lookup"><span data-stu-id="9bc91-125">[complete your task in Azure AD if activation was approved](#complete-your-task-in-azure-ad-if-activation-was-approved)</span></span>

### <a name="navigation"></a><span data-ttu-id="9bc91-126">Навигации</span><span class="sxs-lookup"><span data-stu-id="9bc91-126">Navigation</span></span>

<span data-ttu-id="9bc91-127">Мы обновили hello навигации toosupport утверждений</span><span class="sxs-lookup"><span data-stu-id="9bc91-127">We've updated hello navigation toosupport approvals</span></span>

![](media/azure-ad-pim-approval-workflow/image001.png)

<span data-ttu-id="9bc91-128">Целевая страница по умолчанию Hello предоставляет удобный доступ tooinformation о PIM и hello новой документации утверждения.</span><span class="sxs-lookup"><span data-stu-id="9bc91-128">hello default landing page provides convenient access tooinformation about PIM and hello new approvals documentation.</span></span>

![](media/azure-ad-pim-approval-workflow/image002.png)

<span data-ttu-id="9bc91-129">Мы также добавили новый раздел для всех пользователей PIM — "My Audit History" (Мой журнал аудита).</span><span class="sxs-lookup"><span data-stu-id="9bc91-129">We’ve also added a new section for all users of PIM, ‘My Audit History’.</span></span> <span data-ttu-id="9bc91-130">Здесь вы можете найти все удостоверения tooyour соответствующие сведения hello.</span><span class="sxs-lookup"><span data-stu-id="9bc91-130">Here you can find all hello information relevant tooyour identity.</span></span> <span data-ttu-id="9bc91-131">Это включает все ожидающие и завершенных запросов, любые решения, которые вы внесли о hello запросов, которые можно устранить и все последние роли активаций в одном месте.</span><span class="sxs-lookup"><span data-stu-id="9bc91-131">This includes all your pending and completed requests, any decisions you’ve made about hello requests you resolve, and all your past role activations in one convenient location.</span></span>

![](media/azure-ad-pim-approval-workflow/image003.png)

### <a name="enable-approval-for-specific-roles"></a><span data-ttu-id="9bc91-132">Включение утверждений для конкретных ролей</span><span class="sxs-lookup"><span data-stu-id="9bc91-132">Enable approval for specific roles</span></span>

<span data-ttu-id="9bc91-133">tooenable утверждения для определенной роли, сначала выберите роли каталога hello левой панели навигации.</span><span class="sxs-lookup"><span data-stu-id="9bc91-133">tooenable approval for a specific role, first select Directory Roles from hello left navigation.</span></span>

![](media/azure-ad-pim-approval-workflow/image004.png)

<span data-ttu-id="9bc91-134">Найти и выбрать параметры в левой области навигации роли каталога hello</span><span class="sxs-lookup"><span data-stu-id="9bc91-134">Find and select settings in hello Directory Roles left navigation</span></span>

![](media/azure-ad-pim-approval-workflow/image006.png)

<span data-ttu-id="9bc91-135">Выберите привилегированные роли:</span><span class="sxs-lookup"><span data-stu-id="9bc91-135">Select privileged Roles:</span></span>

![](media/azure-ad-pim-approval-workflow/image009.png)

<span data-ttu-id="9bc91-136">Выберите «Включить» в hello требуют утверждения раздела:</span><span class="sxs-lookup"><span data-stu-id="9bc91-136">Select “Enable” in hello Require approval section:</span></span>

![](media/azure-ad-pim-approval-workflow/image011.png)

<span data-ttu-id="9bc91-137">После включения hello колонке будет расширяться hello tooshow приведенные ниже сведения:</span><span class="sxs-lookup"><span data-stu-id="9bc91-137">Once enabled, hello blade will expand tooshow hello following details:</span></span>

![](media/azure-ad-pim-approval-workflow/image013.png)

>[!NOTE]
<span data-ttu-id="9bc91-138">Если не указать любой утверждающих, hello PRA(s) становятся утверждающие лица по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="9bc91-138">If you DO NOT specify any approvers, hello PRA(s) become hello default approver(s).</span></span> <span data-ttu-id="9bc91-139">PRA(s) бы необходимые tooapprove запрашивает все активации для этой роли.</span><span class="sxs-lookup"><span data-stu-id="9bc91-139">PRA(s) would be required tooapprove ALL activation requests for this role.</span></span>

### <a name="specify-approver-users-andor-groups-tooapprove-requests"></a><span data-ttu-id="9bc91-140">Укажите утверждающего запросов tooapprove пользователей или групп</span><span class="sxs-lookup"><span data-stu-id="9bc91-140">Specify approver users and/or groups tooapprove requests</span></span>

<span data-ttu-id="9bc91-141">Утверждение toodelegate вариант hello слишком «выберите утверждающих»:</span><span class="sxs-lookup"><span data-stu-id="9bc91-141">toodelegate approval, click hello option too“Select approvers”:</span></span>

![](media/azure-ad-pim-approval-workflow/image015.png)

<span data-ttu-id="9bc91-142">При загрузке колонке выберите утверждающих hello может найти конкретного пользователя или группы с помощью панели поиска hello в верхней hello, или при выборе из списка предварительно заполненных hello, затем нажмите кнопку «Выбрать» после завершения:</span><span class="sxs-lookup"><span data-stu-id="9bc91-142">When hello Select approvers blade loads, you may search for a specific user or group using hello search bar at hello top, or selecting from hello pre-populated list, then click “Select” when finished:</span></span>

![](media/azure-ad-pim-approval-workflow/image017.png)

<span data-ttu-id="9bc91-143">Примечание. За один раз можно выбрать несколько пользователей или групп.</span><span class="sxs-lookup"><span data-stu-id="9bc91-143">Note: You may select multiple users or groups at a time.</span></span>

<span data-ttu-id="9bc91-144">Ваш выбор будет отображаться в списке hello выбранного утверждающих, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="9bc91-144">Your selection will appear in hello list of selected approvers as seen below:</span></span>

![](media/azure-ad-pim-approval-workflow/image019.png)

<span data-ttu-id="9bc91-145">tooremove утверждающего, просто щелкните имя следующего tootheir hello удаление кнопки.</span><span class="sxs-lookup"><span data-stu-id="9bc91-145">tooremove an approver, simply click hello Remove button next tootheir name.</span></span>

<span data-ttu-id="9bc91-146">Дополнительные утверждающие tooadd, процесс повторения hello.</span><span class="sxs-lookup"><span data-stu-id="9bc91-146">tooadd additional approvers, repeat hello process.</span></span>

## <a name="view-request-and-approval-history-for-all-privileged-roles"></a><span data-ttu-id="9bc91-147">Просмотр истории запросов и утверждений для всех привилегированных ролей</span><span class="sxs-lookup"><span data-stu-id="9bc91-147">View request and approval history for all privileged roles</span></span>

<span data-ttu-id="9bc91-148">Журнал tooview запроса и утверждения для всех привилегированных ролей, выберите журнал аудита hello панели мониторинга:</span><span class="sxs-lookup"><span data-stu-id="9bc91-148">tooview request and approval history for all privileged roles, select Audit History from hello dashboard:</span></span>

![](media/azure-ad-pim-approval-workflow/image021.png)

>[!NOTE]
<span data-ttu-id="9bc91-149">Можно сортировать данные hello действием и найти «Утверждено активации»</span><span class="sxs-lookup"><span data-stu-id="9bc91-149">You can sort hello data by Action, and look for “Activation Approved”</span></span>

### <a name="view-pending-approvals-requests"></a><span data-ttu-id="9bc91-150">Просмотр запросов, ожидающих утверждения</span><span class="sxs-lookup"><span data-stu-id="9bc91-150">View pending approvals (requests)</span></span>

<span data-ttu-id="9bc91-151">При наличии запроса, ожидающего вашего утверждения, вы, как делегированное утверждающее лицо, получите уведомление по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="9bc91-151">As a delegated approver, you’ll receive email notifications when a request is pending your approval.</span></span> <span data-ttu-id="9bc91-152">tooview эти запросы на вкладке панели мониторинга (в новый переход hello) выберите hello «ожидающие утверждения запросы» в hello портала управления персональными данными hello слева панели навигации.</span><span class="sxs-lookup"><span data-stu-id="9bc91-152">tooview these requests in hello PIM portal, from the dashboard (in hello new navigation) select hello “Pending Approval Requests” tab in hello left navigation bar.</span></span>

![](media/azure-ad-pim-approval-workflow/image023.png)

<span data-ttu-id="9bc91-153">Отобразится список запросов, ожидающих утверждения:</span><span class="sxs-lookup"><span data-stu-id="9bc91-153">From there, you’ll see a list of requests pending approval:</span></span>

![](media/azure-ad-pim-approval-workflow/image024.png)

### <a name="approve-or-reject-requests-for-role-elevation-single-andor-bulk"></a><span data-ttu-id="9bc91-154">Утверждение или отклонение запросов на повышение роли (по одному и (или) массово)</span><span class="sxs-lookup"><span data-stu-id="9bc91-154">Approve or reject requests for role elevation (single and/or bulk)</span></span>

<span data-ttu-id="9bc91-155">Выберите запросы hello обратиться tooapprove или запретить и нажмите кнопку "hello" в области действия, соответствующего решения:</span><span class="sxs-lookup"><span data-stu-id="9bc91-155">Select hello requests you wish tooapprove or deny, and click hello button in the action bar that corresponds with your decision:</span></span>

![](media/azure-ad-pim-approval-workflow/image025.png)

### <a name="provide-justification-for-my-approvalrejection"></a><span data-ttu-id="9bc91-156">Указание обоснования для своего утверждения или отказа</span><span class="sxs-lookup"><span data-stu-id="9bc91-156">Provide justification for my approval/rejection</span></span>

<span data-ttu-id="9bc91-157">Это будет открыть новый tooapprove колонке или запретить несколько запросов одновременно.</span><span class="sxs-lookup"><span data-stu-id="9bc91-157">This will open a new blade tooapprove or deny multiple requests at once.</span></span> <span data-ttu-id="9bc91-158">Введите обоснование для такого решения и нажмите кнопку Утвердить (или запретить) в нижней hello или колонке hello:</span><span class="sxs-lookup"><span data-stu-id="9bc91-158">Enter a justification for your decision, and click approve (or deny) at hello bottom or hello blade:</span></span>

![](media/azure-ad-pim-approval-workflow/image029.png)

<span data-ttu-id="9bc91-159">По завершении процесса запроса hello символе состояния hello будут отражать принятое (в этом примере hello решение является утверждение):</span><span class="sxs-lookup"><span data-stu-id="9bc91-159">When hello request process is complete, hello status symbol will reflect the decision you made (in this example, hello decision is approve):</span></span>

![](media/azure-ad-pim-approval-workflow/image031.png)

### <a name="request-activation-of-a-role-that-requires-approval"></a><span data-ttu-id="9bc91-160">Запрос активации роли, для которой требуется утверждение</span><span class="sxs-lookup"><span data-stu-id="9bc91-160">Request activation of a role that requires approval</span></span>

<span data-ttu-id="9bc91-161">Запрос активации роли, которая требует утверждения могут инициироваться из старого PIM навигации hello или hello новый переход, как процесс hello остается активации роли hello таким же.</span><span class="sxs-lookup"><span data-stu-id="9bc91-161">Requesting activation of a role that requires approval may be initiated from either hello old PIM navigation, or hello new navigation, as hello process for role activation remains hello same.</span></span> <span data-ttu-id="9bc91-162">Просто выберите роль из списка hello ролей для активации:</span><span class="sxs-lookup"><span data-stu-id="9bc91-162">Simply select a role from hello list of roles to activate:</span></span>

![](media/azure-ad-pim-approval-workflow/image033.png)

<span data-ttu-id="9bc91-163">Если для привилегированной роли требуется выполнение Многофакторной идентификации, то сначала отобразится соответствующий запрос:</span><span class="sxs-lookup"><span data-stu-id="9bc91-163">If a privileged role requires Multi-Factor Authentication, you’ll be prompted to complete that task first:</span></span>

![](media/azure-ad-pim-approval-workflow/image035.png)

<span data-ttu-id="9bc91-164">По завершении щелкните "Активировать" и укажите обоснование (при необходимости):</span><span class="sxs-lookup"><span data-stu-id="9bc91-164">Once complete, click Activate and provide a justification (if required):</span></span>

![](media/azure-ad-pim-approval-workflow/image037.png)

<span data-ttu-id="9bc91-165">Запрашивающая сторона Hello будет выведено уведомление, которое hello запрос ожидает утверждения:</span><span class="sxs-lookup"><span data-stu-id="9bc91-165">hello requestor will see a notification that hello request is pending approval:</span></span>

![](media/azure-ad-pim-approval-workflow/image039.png)

### <a name="view-hello-status-of-your-request-tooactivate"></a><span data-ttu-id="9bc91-166">Просмотр состояния hello tooactivate вашего запроса</span><span class="sxs-lookup"><span data-stu-id="9bc91-166">View hello status of your request tooactivate</span></span>

<span data-ttu-id="9bc91-167">Просмотр состояния hello tooactivate ожидающий запрос должен осуществляться новой панели навигации.</span><span class="sxs-lookup"><span data-stu-id="9bc91-167">Viewing hello status of a pending request tooactivate must be accessed from the new navigation.</span></span> <span data-ttu-id="9bc91-168">Hello левой панели навигации выберите вкладку «Мои запросы» hello.</span><span class="sxs-lookup"><span data-stu-id="9bc91-168">From hello left navigation bar, select hello “My Requests” tab:</span></span>

![](media/azure-ad-pim-approval-workflow/image041.png)

<span data-ttu-id="9bc91-169">состояние запроса Hello слишком по умолчанию «Ожидание», но можно переключить toosee все или отклоненных запросов.</span><span class="sxs-lookup"><span data-stu-id="9bc91-169">hello request state defaults too“Pending”, but you can toggle toosee all or denied requests.</span></span>

### <a name="complete-your-task-in-azure-ad-if-activation-was-approved"></a><span data-ttu-id="9bc91-170">Выполнение задачи в Azure AD, если запрос на активацию утвержден</span><span class="sxs-lookup"><span data-stu-id="9bc91-170">Complete your task in Azure AD if activation was approved</span></span>

<span data-ttu-id="9bc91-171">После утверждения запроса hello hello роли является активным и может продолжить работу, которую требуется эта роль.</span><span class="sxs-lookup"><span data-stu-id="9bc91-171">Once hello request is approved, hello role is active and you may proceed with any work that requires this role.</span></span>

![](media/azure-ad-pim-approval-workflow/image043.png)

## <a name="next-steps"></a><span data-ttu-id="9bc91-172">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9bc91-172">Next steps</span></span>

<span data-ttu-id="9bc91-173">Ваш отзыв будет полезен toous.</span><span class="sxs-lookup"><span data-stu-id="9bc91-173">Your feedback is valuable toous.</span></span> <span data-ttu-id="9bc91-174">Вы можете бесплатно tooshare комментарии или отзывы с нами здесь!</span><span class="sxs-lookup"><span data-stu-id="9bc91-174">Please feel free tooshare comments or feedback with us here!</span></span>
