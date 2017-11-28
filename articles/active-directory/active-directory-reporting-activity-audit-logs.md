---
title: "aaaAudit отчеты на портале Azure Active Directory hello | Документы Microsoft"
description: "Отчеты о действиях на портале Azure Active Directory hello аудита toohello введение"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: a1f93126-77d1-4345-ab7d-561066041161
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 1567673f5030fc707b017c069f2ba7587962e5cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="audit-activity-reports-in-hello-azure-active-directory-portal"></a><span data-ttu-id="318e7-103">Отчеты о действиях на портале Azure Active Directory hello аудита</span><span class="sxs-lookup"><span data-stu-id="318e7-103">Audit activity reports in hello Azure Active Directory portal</span></span> 

<span data-ttu-id="318e7-104">С отчетами в Azure Active Directory (Azure AD), можно получить сведения hello необходимы toodetermine, насколько среды.</span><span class="sxs-lookup"><span data-stu-id="318e7-104">With reporting in Azure Active Directory (Azure AD), you can get hello information you need toodetermine how your environment is doing.</span></span>

<span data-ttu-id="318e7-105">Архитектура системы создания отчетов в Azure AD Hello состоит из hello следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="318e7-105">hello reporting architecture in Azure AD consists of hello following components:</span></span>

- <span data-ttu-id="318e7-106">**Действие**</span><span class="sxs-lookup"><span data-stu-id="318e7-106">**Activity**</span></span> 
    - <span data-ttu-id="318e7-107">**Действия входа** — сведения об использовании hello управляемых приложений и действий входа пользователей</span><span class="sxs-lookup"><span data-stu-id="318e7-107">**Sign-in activities** – Information about hello usage of managed applications and user sign-in activities</span></span>
    - <span data-ttu-id="318e7-108">**Журналы аудита** — данные системных операций об управлении пользователями и группами, об управляемых приложениях и действиях с каталогами.</span><span class="sxs-lookup"><span data-stu-id="318e7-108">**Audit logs** - System activity information about users and group management, your managed applications and directory activities.</span></span>
- <span data-ttu-id="318e7-109">**Безопасность**</span><span class="sxs-lookup"><span data-stu-id="318e7-109">**Security**</span></span> 
    - <span data-ttu-id="318e7-110">**Рискованные входы** -рискованным вход является показателем для попытки входа, возможно, выполнены с тем, кто не hello законный владельцем учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="318e7-110">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> <span data-ttu-id="318e7-111">Дополнительные сведения см. в разделе "Вход, представляющий риск".</span><span class="sxs-lookup"><span data-stu-id="318e7-111">For more details, see Risky sign-ins.</span></span>
    - <span data-ttu-id="318e7-112">**Пользователи, находящиеся в группе риска**. Такая пометка означает, что конфиденциальность учетной записи пользователя, возможно, нарушена.</span><span class="sxs-lookup"><span data-stu-id="318e7-112">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="318e7-113">Дополнительные сведения см. в разделе "Пользователи, помеченные для события риска".</span><span class="sxs-lookup"><span data-stu-id="318e7-113">For more details, see Users flagged for risk.</span></span>

<span data-ttu-id="318e7-114">В этом разделе дается обзор действий аудита hello.</span><span class="sxs-lookup"><span data-stu-id="318e7-114">This topic gives you an overview of hello audit activities.</span></span>
 
## <a name="who-can-access-hello-data"></a><span data-ttu-id="318e7-115">Кто имеет доступ к данным hello?</span><span class="sxs-lookup"><span data-stu-id="318e7-115">Who can access hello data?</span></span>
* <span data-ttu-id="318e7-116">Пользователи с ролью администратора безопасности или безопасность чтения hello</span><span class="sxs-lookup"><span data-stu-id="318e7-116">Users in hello Security Admin or Security Reader role</span></span>
* <span data-ttu-id="318e7-117">Глобальные администраторы</span><span class="sxs-lookup"><span data-stu-id="318e7-117">Global Admins</span></span>
* <span data-ttu-id="318e7-118">Отдельные пользователи (не администраторы) могут просматривать собственные действия.</span><span class="sxs-lookup"><span data-stu-id="318e7-118">Individual users (non-admins) can see their own activities</span></span>


## <a name="audit-logs"></a><span data-ttu-id="318e7-119">Журналы аудита</span><span class="sxs-lookup"><span data-stu-id="318e7-119">Audit logs</span></span>

<span data-ttu-id="318e7-120">журналы аудита Hello в Azure Active Directory предоставляют записей действий системы на соответствие.</span><span class="sxs-lookup"><span data-stu-id="318e7-120">hello audit logs in Azure Active Directory provide records of system activities for compliance.</span></span>  
<span data-ttu-id="318e7-121">Ваш первый tooall точки записи данных аудита является **журналы аудита** в hello **действия** раздел **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="318e7-121">Your first entry point tooall auditing data is **Audit logs** in hello **Activity** section of **Azure Active Directory**.</span></span>

<span data-ttu-id="318e7-122">![Журналы аудита](./media/active-directory-reporting-activity-audit-logs/61.png "Журналы аудита")</span><span class="sxs-lookup"><span data-stu-id="318e7-122">![Audit logs](./media/active-directory-reporting-activity-audit-logs/61.png "Audit logs")</span></span>

<span data-ttu-id="318e7-123">Журнал аудита содержит представление списка по умолчанию, в котором отображаются:</span><span class="sxs-lookup"><span data-stu-id="318e7-123">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="318e7-124">Hello дату и время вхождения hello</span><span class="sxs-lookup"><span data-stu-id="318e7-124">hello date and time of hello occurrence</span></span>
- <span data-ttu-id="318e7-125">Здравствуйте, инициатор или субъекта (*,*) действия</span><span class="sxs-lookup"><span data-stu-id="318e7-125">hello initiator / actor (*who*) of an activity</span></span> 
- <span data-ttu-id="318e7-126">Здравствуйте, действие (*что*)</span><span class="sxs-lookup"><span data-stu-id="318e7-126">hello activity (*what*)</span></span> 
- <span data-ttu-id="318e7-127">целевой Hello</span><span class="sxs-lookup"><span data-stu-id="318e7-127">hello target</span></span>

<span data-ttu-id="318e7-128">![Журналы аудита](./media/active-directory-reporting-activity-audit-logs/18.png "Журналы аудита")</span><span class="sxs-lookup"><span data-stu-id="318e7-128">![Audit logs](./media/active-directory-reporting-activity-audit-logs/18.png "Audit logs")</span></span>

<span data-ttu-id="318e7-129">Представление списка hello можно настроить, щелкнув **столбцы** инструментов hello.</span><span class="sxs-lookup"><span data-stu-id="318e7-129">You can customize hello list view by clicking **Columns** in hello toolbar.</span></span>

<span data-ttu-id="318e7-130">![Журналы аудита](./media/active-directory-reporting-activity-audit-logs/19.png "Журналы аудита")</span><span class="sxs-lookup"><span data-stu-id="318e7-130">![Audit logs](./media/active-directory-reporting-activity-audit-logs/19.png "Audit logs")</span></span>

<span data-ttu-id="318e7-131">Это позволяет toodisplay дополнительные поля или удалять поля, которые уже отображаются.</span><span class="sxs-lookup"><span data-stu-id="318e7-131">This enables you toodisplay additional fields or remove fields that are already displayed.</span></span>

<span data-ttu-id="318e7-132">![Журналы аудита](./media/active-directory-reporting-activity-audit-logs/21.png "Журналы аудита")</span><span class="sxs-lookup"><span data-stu-id="318e7-132">![Audit logs](./media/active-directory-reporting-activity-audit-logs/21.png "Audit logs")</span></span>


<span data-ttu-id="318e7-133">Щелкнув элемент в представлении списка hello, получение всех доступных сведений о нем.</span><span class="sxs-lookup"><span data-stu-id="318e7-133">By clicking an item in hello list view, you get all available details about it.</span></span>

<span data-ttu-id="318e7-134">![Журналы аудита](./media/active-directory-reporting-activity-audit-logs/22.png "Журналы аудита")</span><span class="sxs-lookup"><span data-stu-id="318e7-134">![Audit logs](./media/active-directory-reporting-activity-audit-logs/22.png "Audit logs")</span></span>


## <a name="filtering-audit-logs"></a><span data-ttu-id="318e7-135">Фильтрация журналов аудита</span><span class="sxs-lookup"><span data-stu-id="318e7-135">Filtering audit logs</span></span>

<span data-ttu-id="318e7-136">toonarrow вниз hello сообщила tooa уровень данных, что работает автоматически, можно фильтровать hello данные аудита, используя hello следующие поля:</span><span class="sxs-lookup"><span data-stu-id="318e7-136">toonarrow down hello reported data tooa level that works for you, you can filter hello audit data using hello following fields:</span></span>

- <span data-ttu-id="318e7-137">диапазон дат;</span><span class="sxs-lookup"><span data-stu-id="318e7-137">Date range</span></span>
- <span data-ttu-id="318e7-138">инициатор (субъект);</span><span class="sxs-lookup"><span data-stu-id="318e7-138">Initiated by (Actor)</span></span>
- <span data-ttu-id="318e7-139">Категория</span><span class="sxs-lookup"><span data-stu-id="318e7-139">Category</span></span>
- <span data-ttu-id="318e7-140">Тип ресурса действия</span><span class="sxs-lookup"><span data-stu-id="318e7-140">Activity resource type</span></span>
- <span data-ttu-id="318e7-141">Действие</span><span class="sxs-lookup"><span data-stu-id="318e7-141">Activity</span></span>

<span data-ttu-id="318e7-142">![Журналы аудита](./media/active-directory-reporting-activity-audit-logs/23.png "Журналы аудита")</span><span class="sxs-lookup"><span data-stu-id="318e7-142">![Audit logs](./media/active-directory-reporting-activity-audit-logs/23.png "Audit logs")</span></span>


<span data-ttu-id="318e7-143">Hello **диапазон дат** фильтр включает tooyou toodefine период времени для hello возвращаемых данных.</span><span class="sxs-lookup"><span data-stu-id="318e7-143">hello **date range** filter enables tooyou toodefine a timeframe for hello returned data.</span></span>  
<span data-ttu-id="318e7-144">Возможные значения:</span><span class="sxs-lookup"><span data-stu-id="318e7-144">Possible values are:</span></span>

- <span data-ttu-id="318e7-145">1 месяц</span><span class="sxs-lookup"><span data-stu-id="318e7-145">1 month</span></span>
- <span data-ttu-id="318e7-146">7 дней</span><span class="sxs-lookup"><span data-stu-id="318e7-146">7 days</span></span>
- <span data-ttu-id="318e7-147">24 часа</span><span class="sxs-lookup"><span data-stu-id="318e7-147">24 hours</span></span>
- <span data-ttu-id="318e7-148">Пользовательская</span><span class="sxs-lookup"><span data-stu-id="318e7-148">Custom</span></span>

<span data-ttu-id="318e7-149">При выборе пользовательского интервала времени можно настроить время начала и окончания.</span><span class="sxs-lookup"><span data-stu-id="318e7-149">When you select a custom timeframe, you can configure a start time and an end time.</span></span>

<span data-ttu-id="318e7-150">Hello **инициировано** фильтр позволяет вам toodefine имя субъекта или имени универсального участника (UPN).</span><span class="sxs-lookup"><span data-stu-id="318e7-150">hello **initiated by** filter enables you toodefine an actor's name or its universal principal name (UPN).</span></span>

<span data-ttu-id="318e7-151">Hello **категории** фильтр позволяет tooselect один hello следующий фильтр:</span><span class="sxs-lookup"><span data-stu-id="318e7-151">hello **category** filter enables you tooselect one of hello following filter:</span></span>

- <span data-ttu-id="318e7-152">Все</span><span class="sxs-lookup"><span data-stu-id="318e7-152">All</span></span>
- <span data-ttu-id="318e7-153">Core category (Основная категория);</span><span class="sxs-lookup"><span data-stu-id="318e7-153">Core category</span></span>
- <span data-ttu-id="318e7-154">Core directory (Основной каталог);</span><span class="sxs-lookup"><span data-stu-id="318e7-154">Core directory</span></span>
- <span data-ttu-id="318e7-155">Self-service password management (Самостоятельное управление паролями);</span><span class="sxs-lookup"><span data-stu-id="318e7-155">Self-service password management</span></span>
- <span data-ttu-id="318e7-156">Самостоятельное управление группами</span><span class="sxs-lookup"><span data-stu-id="318e7-156">Self-service group management</span></span>
- <span data-ttu-id="318e7-157">Подготовка учетной записи — автоматическая смена паролей</span><span class="sxs-lookup"><span data-stu-id="318e7-157">Account provisioning- Automated password rollover</span></span>
- <span data-ttu-id="318e7-158">Приглашенные пользователи</span><span class="sxs-lookup"><span data-stu-id="318e7-158">Invited users</span></span>
- <span data-ttu-id="318e7-159">MIM Service (Служба MIM).</span><span class="sxs-lookup"><span data-stu-id="318e7-159">MIM service</span></span>
- <span data-ttu-id="318e7-160">Защита идентификации</span><span class="sxs-lookup"><span data-stu-id="318e7-160">Identity Protection</span></span>
- <span data-ttu-id="318e7-161">B2C</span><span class="sxs-lookup"><span data-stu-id="318e7-161">B2C</span></span>

<span data-ttu-id="318e7-162">Hello **типа ресурса действия** фильтр позволяет tooselect одно из следующих hello фильтры:</span><span class="sxs-lookup"><span data-stu-id="318e7-162">hello **activity resource type** filter enables you tooselect one of hello following filters:</span></span>

- <span data-ttu-id="318e7-163">Все</span><span class="sxs-lookup"><span data-stu-id="318e7-163">All</span></span> 
- <span data-ttu-id="318e7-164">Группа</span><span class="sxs-lookup"><span data-stu-id="318e7-164">Group</span></span>
- <span data-ttu-id="318e7-165">Каталог</span><span class="sxs-lookup"><span data-stu-id="318e7-165">Directory</span></span>
- <span data-ttu-id="318e7-166">Пользователь</span><span class="sxs-lookup"><span data-stu-id="318e7-166">User</span></span>
- <span data-ttu-id="318e7-167">Приложение</span><span class="sxs-lookup"><span data-stu-id="318e7-167">Application</span></span>
- <span data-ttu-id="318e7-168">Политика</span><span class="sxs-lookup"><span data-stu-id="318e7-168">Policy</span></span>
- <span data-ttu-id="318e7-169">Устройство</span><span class="sxs-lookup"><span data-stu-id="318e7-169">Device</span></span>
- <span data-ttu-id="318e7-170">Другие</span><span class="sxs-lookup"><span data-stu-id="318e7-170">Other</span></span>

<span data-ttu-id="318e7-171">При выборе **группы** как **типа ресурса действия**, вы получаете дополнительный фильтр категорию, которая позволяет tooalso предоставляют **источника**:</span><span class="sxs-lookup"><span data-stu-id="318e7-171">When you select **Group** as **activity resource type**, you get an additional filter category that enables you tooalso provide a **Source**:</span></span>

- <span data-ttu-id="318e7-172">Azure AD</span><span class="sxs-lookup"><span data-stu-id="318e7-172">Azure AD</span></span>
- <span data-ttu-id="318e7-173">O365</span><span class="sxs-lookup"><span data-stu-id="318e7-173">O365</span></span>


<span data-ttu-id="318e7-174">Hello **действия** фильтр основан на категории hello и действия ресурса тип выбора, сделанного.</span><span class="sxs-lookup"><span data-stu-id="318e7-174">hello **activity** filter is based on hello category and Activity resource type selection you make.</span></span> <span data-ttu-id="318e7-175">Можно выбрать определенное действие, требуется toosee или выберите все.</span><span class="sxs-lookup"><span data-stu-id="318e7-175">You can select a specific activity you want toosee or choose all.</span></span> 

<span data-ttu-id="318e7-176">Вы можете получить список hello всех действий аудита с помощью hello $ https://graph.windows.net/ Graph API tenantdomain/действия или auditActivityTypes? api-version = beta, где $tenantdomain = имя домена или см. в статье toohello [отчет аудита события](active-directory-reporting-audit-events.md).</span><span class="sxs-lookup"><span data-stu-id="318e7-176">You can get hello list of all Audit Activities using hello Graph API https://graph.windows.net/$tenantdomain/activities/auditActivityTypes?api-version=beta, where $tenantdomain = your domain name or refer toohello article [audit report events](active-directory-reporting-audit-events.md).</span></span>


## <a name="audit-logs-shortcuts"></a><span data-ttu-id="318e7-177">Ярлыки журналов аудита</span><span class="sxs-lookup"><span data-stu-id="318e7-177">Audit logs shortcuts</span></span>

<span data-ttu-id="318e7-178">Кроме слишком**Azure Active Directory**, hello портал Azure предоставляет две дополнительные точки входа tooaudit данных:</span><span class="sxs-lookup"><span data-stu-id="318e7-178">In addition too**Azure Active Directory**, hello Azure portal provides you with two additional entry points tooaudit data:</span></span>

- <span data-ttu-id="318e7-179">Пользователи и группы</span><span class="sxs-lookup"><span data-stu-id="318e7-179">Users and groups</span></span>
- <span data-ttu-id="318e7-180">корпоративные приложения.</span><span class="sxs-lookup"><span data-stu-id="318e7-180">Enterprise applications</span></span>

### <a name="users-and-groups-audit-logs"></a><span data-ttu-id="318e7-181">Журналы аудита пользователей и групп</span><span class="sxs-lookup"><span data-stu-id="318e7-181">Users and groups audit logs</span></span>

<span data-ttu-id="318e7-182">С именем пользователя и отчеты аудита на основе групп можно получить ответы tooquestions, такие как:</span><span class="sxs-lookup"><span data-stu-id="318e7-182">With user and group-based audit reports, you can get answers tooquestions such as:</span></span>

- <span data-ttu-id="318e7-183">Какие виды обновлений было примененных hello пользователей?</span><span class="sxs-lookup"><span data-stu-id="318e7-183">What types of updates have been applied hello users?</span></span>

- <span data-ttu-id="318e7-184">Сколько пользователей было изменено?</span><span class="sxs-lookup"><span data-stu-id="318e7-184">How many users were changed?</span></span>

- <span data-ttu-id="318e7-185">Сколько паролей было изменено?</span><span class="sxs-lookup"><span data-stu-id="318e7-185">How many passwords were changed?</span></span>

- <span data-ttu-id="318e7-186">Что делал администратор в каталоге?</span><span class="sxs-lookup"><span data-stu-id="318e7-186">What has an administrator done in a directory?</span></span>

- <span data-ttu-id="318e7-187">Что такое hello групп, которые были добавлены</span><span class="sxs-lookup"><span data-stu-id="318e7-187">What are hello groups that have been added?</span></span>

- <span data-ttu-id="318e7-188">В каких группах произошли изменения членства?</span><span class="sxs-lookup"><span data-stu-id="318e7-188">Are there groups with membership changes?</span></span>

- <span data-ttu-id="318e7-189">Hello владельцев группы были изменены?</span><span class="sxs-lookup"><span data-stu-id="318e7-189">Have hello owners of group been changed?</span></span>

- <span data-ttu-id="318e7-190">Какие лицензии была назначена пользователю или группе tooa?</span><span class="sxs-lookup"><span data-stu-id="318e7-190">What licenses have been assigned tooa group or a user?</span></span>

<span data-ttu-id="318e7-191">Если необходимо просто tooreview аудит данных, связанных toousers и групп, можно найти отфильтрованное представление в списке **журналы аудита** в hello **действия** раздел hello **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="318e7-191">If you just want tooreview auditing data that is related toousers and groups, you can find a filtered view under **Audit logs** in hello **Activity** section of hello **Users and Groups**.</span></span> <span data-ttu-id="318e7-192">Для этой точки в качестве **типа ресурса действия** предварительно выбрано значение **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="318e7-192">This entry point has **Users and groups** as preselected **Activity Resource Type**.</span></span>

<span data-ttu-id="318e7-193">![Журналы аудита](./media/active-directory-reporting-activity-audit-logs/93.png "Журналы аудита")</span><span class="sxs-lookup"><span data-stu-id="318e7-193">![Audit logs](./media/active-directory-reporting-activity-audit-logs/93.png "Audit logs")</span></span>

### <a name="enterprise-applications-audit-logs"></a><span data-ttu-id="318e7-194">Журналы аудита корпоративных приложений</span><span class="sxs-lookup"><span data-stu-id="318e7-194">Enterprise applications audit logs</span></span>

<span data-ttu-id="318e7-195">Отчеты аудита с от приложения, можно получить ответы tooquestions, такие как:</span><span class="sxs-lookup"><span data-stu-id="318e7-195">With application-based audit reports, you can get answers tooquestions such as:</span></span>

* <span data-ttu-id="318e7-196">Что такое hello приложения, которые были добавлены или обновлены?</span><span class="sxs-lookup"><span data-stu-id="318e7-196">What are hello applications that have been added or updated?</span></span>
* <span data-ttu-id="318e7-197">Что такое hello приложений, которые были удалены</span><span class="sxs-lookup"><span data-stu-id="318e7-197">What are hello applications that have been removed?</span></span>
* <span data-ttu-id="318e7-198">Изменился ли участник-служба для приложения?</span><span class="sxs-lookup"><span data-stu-id="318e7-198">Has a service principle for an application changed?</span></span>
* <span data-ttu-id="318e7-199">Изменены имена hello приложений?</span><span class="sxs-lookup"><span data-stu-id="318e7-199">Have hello names of applications been changed?</span></span>
* <span data-ttu-id="318e7-200">Кто дали согласие tooan приложения?</span><span class="sxs-lookup"><span data-stu-id="318e7-200">Who gave consent tooan application?</span></span>

<span data-ttu-id="318e7-201">Если необходимо просто tooreview аудит данных, связанных tooyour приложений можно найти отфильтрованное представление в списке **журналы аудита** в hello **действия** раздел hello **корпоративных приложений**  колонку.</span><span class="sxs-lookup"><span data-stu-id="318e7-201">If you just want tooreview auditing data that is related tooyour applications, you can find a filtered view under **Audit logs** in hello **Activity** section of hello **Enterprise applications** blade.</span></span> <span data-ttu-id="318e7-202">Для этой точки в качестве **типа ресурса действия** предварительно выбрано значение **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="318e7-202">This entry point has **Enterprise applications** as preselected **Activity Resource Type**.</span></span>

<span data-ttu-id="318e7-203">![Журналы аудита](./media/active-directory-reporting-activity-audit-logs/134.png "Журналы аудита")</span><span class="sxs-lookup"><span data-stu-id="318e7-203">![Audit logs](./media/active-directory-reporting-activity-audit-logs/134.png "Audit logs")</span></span>

<span data-ttu-id="318e7-204">Можно включить фильтрацию дальнейшей работы toojust **группы** или просто **пользователей**.</span><span class="sxs-lookup"><span data-stu-id="318e7-204">You can filter this view further down toojust **groups** or just **users**.</span></span>

<span data-ttu-id="318e7-205">![Журналы аудита](./media/active-directory-reporting-activity-audit-logs/25.png "Журналы аудита")</span><span class="sxs-lookup"><span data-stu-id="318e7-205">![Audit logs](./media/active-directory-reporting-activity-audit-logs/25.png "Audit logs")</span></span>


## <a name="next-steps"></a><span data-ttu-id="318e7-206">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="318e7-206">Next steps</span></span>

<span data-ttu-id="318e7-207">Обзор отчетов см. в разделе hello [отчетов Azure Active Directory](active-directory-reporting-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="318e7-207">For an overview of reporting, see hello [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span>

