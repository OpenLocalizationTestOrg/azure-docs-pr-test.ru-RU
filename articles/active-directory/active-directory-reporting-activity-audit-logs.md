---
title: "Отчеты о действиях аудита на портале Azure Active Directory | Документация Майкрософт"
description: "Общие сведения об отчетах о действиях аудита на портале Azure Active Directory."
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
ms.openlocfilehash: f2d0332d815c82d7d47625e020de2e9c5099deeb
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="audit-activity-reports-in-the-azure-active-directory-portal"></a><span data-ttu-id="bd64b-103">Отчеты о действиях аудита на портале Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bd64b-103">Audit activity reports in the Azure Active Directory portal</span></span> 

<span data-ttu-id="bd64b-104">Функция отчетов в Azure Active Directory (Azure AD) позволяет получать всю необходимую информацию, с помощью которой можно определить, как работает среда.</span><span class="sxs-lookup"><span data-stu-id="bd64b-104">With reporting in Azure Active Directory (Azure AD), you can get the information you need to determine how your environment is doing.</span></span>

<span data-ttu-id="bd64b-105">Архитектура создания отчетов в Azure AD состоит из следующих компонентов.</span><span class="sxs-lookup"><span data-stu-id="bd64b-105">The reporting architecture in Azure AD consists of the following components:</span></span>

- <span data-ttu-id="bd64b-106">**Действие**</span><span class="sxs-lookup"><span data-stu-id="bd64b-106">**Activity**</span></span> 
    - <span data-ttu-id="bd64b-107">**Действия входа** — информация об использовании управляемых приложений и действиях входа.</span><span class="sxs-lookup"><span data-stu-id="bd64b-107">**Sign-in activities** – Information about the usage of managed applications and user sign-in activities</span></span>
    - <span data-ttu-id="bd64b-108">**Журналы аудита** — данные системных операций об управлении пользователями и группами, об управляемых приложениях и действиях с каталогами.</span><span class="sxs-lookup"><span data-stu-id="bd64b-108">**Audit logs** - System activity information about users and group management, your managed applications and directory activities.</span></span>
- <span data-ttu-id="bd64b-109">**Безопасность**</span><span class="sxs-lookup"><span data-stu-id="bd64b-109">**Security**</span></span> 
    - <span data-ttu-id="bd64b-110">**Входы, представляющие риск**. Вход, представляющий риск, означает, что в систему пытался войти пользователь, который не является законным владельцем учетной записи.</span><span class="sxs-lookup"><span data-stu-id="bd64b-110">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span></span> <span data-ttu-id="bd64b-111">Дополнительные сведения см. в разделе "Вход, представляющий риск".</span><span class="sxs-lookup"><span data-stu-id="bd64b-111">For more details, see Risky sign-ins.</span></span>
    - <span data-ttu-id="bd64b-112">**Пользователи, находящиеся в группе риска**. Такая пометка означает, что конфиденциальность учетной записи пользователя, возможно, нарушена.</span><span class="sxs-lookup"><span data-stu-id="bd64b-112">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="bd64b-113">Дополнительные сведения см. в разделе "Пользователи, помеченные для события риска".</span><span class="sxs-lookup"><span data-stu-id="bd64b-113">For more details, see Users flagged for risk.</span></span>

<span data-ttu-id="bd64b-114">В этом разделе содержатся общие сведения о действиях аудита.</span><span class="sxs-lookup"><span data-stu-id="bd64b-114">This topic gives you an overview of the audit activities.</span></span>
 
## <a name="who-can-access-the-data"></a><span data-ttu-id="bd64b-115">Кто может получить доступ к данным?</span><span class="sxs-lookup"><span data-stu-id="bd64b-115">Who can access the data?</span></span>
* <span data-ttu-id="bd64b-116">Пользователи с ролью администратора безопасности или читателя безопасности</span><span class="sxs-lookup"><span data-stu-id="bd64b-116">Users in the Security Admin or Security Reader role</span></span>
* <span data-ttu-id="bd64b-117">Глобальные администраторы</span><span class="sxs-lookup"><span data-stu-id="bd64b-117">Global Admins</span></span>
* <span data-ttu-id="bd64b-118">Отдельные пользователи (не администраторы) могут просматривать собственные действия.</span><span class="sxs-lookup"><span data-stu-id="bd64b-118">Individual users (non-admins) can see their own activities</span></span>


## <a name="audit-logs"></a><span data-ttu-id="bd64b-119">Журналы аудита</span><span class="sxs-lookup"><span data-stu-id="bd64b-119">Audit logs</span></span>

<span data-ttu-id="bd64b-120">Журналы аудита в Azure Active Directory содержат записи о действиях системы (необходимые для соответствия требованиям).</span><span class="sxs-lookup"><span data-stu-id="bd64b-120">The audit logs in Azure Active Directory provide records of system activities for compliance.</span></span>  
<span data-ttu-id="bd64b-121">Знакомство с данными аудита следует начать с **журналов аудита** в разделе **Действие** службы **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bd64b-121">Your first entry point to all auditing data is **Audit logs** in the **Activity** section of **Azure Active Directory**.</span></span>

<span data-ttu-id="bd64b-122">![Журналы аудита](./media/active-directory-reporting-activity-audit-logs/61.png "Журналы аудита")</span><span class="sxs-lookup"><span data-stu-id="bd64b-122">![Audit logs](./media/active-directory-reporting-activity-audit-logs/61.png "Audit logs")</span></span>

<span data-ttu-id="bd64b-123">Журнал аудита содержит представление списка по умолчанию, в котором отображаются:</span><span class="sxs-lookup"><span data-stu-id="bd64b-123">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="bd64b-124">дата и время выполнения действия;</span><span class="sxs-lookup"><span data-stu-id="bd64b-124">the date and time of the occurrence</span></span>
- <span data-ttu-id="bd64b-125">инициатор и субъект (*кто*) действия;</span><span class="sxs-lookup"><span data-stu-id="bd64b-125">the initiator / actor (*who*) of an activity</span></span> 
- <span data-ttu-id="bd64b-126">действие (*что*);</span><span class="sxs-lookup"><span data-stu-id="bd64b-126">the activity (*what*)</span></span> 
- <span data-ttu-id="bd64b-127">целевой объект.</span><span class="sxs-lookup"><span data-stu-id="bd64b-127">the target</span></span>

<span data-ttu-id="bd64b-128">![Журналы аудита](./media/active-directory-reporting-activity-audit-logs/18.png "Журналы аудита")</span><span class="sxs-lookup"><span data-stu-id="bd64b-128">![Audit logs](./media/active-directory-reporting-activity-audit-logs/18.png "Audit logs")</span></span>

<span data-ttu-id="bd64b-129">Представление списка можно настроить, щелкнув **Столбцы** на панели инструментов.</span><span class="sxs-lookup"><span data-stu-id="bd64b-129">You can customize the list view by clicking **Columns** in the toolbar.</span></span>

<span data-ttu-id="bd64b-130">![Журналы аудита](./media/active-directory-reporting-activity-audit-logs/19.png "Журналы аудита")</span><span class="sxs-lookup"><span data-stu-id="bd64b-130">![Audit logs](./media/active-directory-reporting-activity-audit-logs/19.png "Audit logs")</span></span>

<span data-ttu-id="bd64b-131">Здесь вы можете добавить или удалить отображаемые поля.</span><span class="sxs-lookup"><span data-stu-id="bd64b-131">This enables you to display additional fields or remove fields that are already displayed.</span></span>

<span data-ttu-id="bd64b-132">![Журналы аудита](./media/active-directory-reporting-activity-audit-logs/21.png "Журналы аудита")</span><span class="sxs-lookup"><span data-stu-id="bd64b-132">![Audit logs](./media/active-directory-reporting-activity-audit-logs/21.png "Audit logs")</span></span>


<span data-ttu-id="bd64b-133">Щелкнув элемент в представлении списка, вы получите дополнительные сведения о нем.</span><span class="sxs-lookup"><span data-stu-id="bd64b-133">By clicking an item in the list view, you get all available details about it.</span></span>

<span data-ttu-id="bd64b-134">![Журналы аудита](./media/active-directory-reporting-activity-audit-logs/22.png "Журналы аудита")</span><span class="sxs-lookup"><span data-stu-id="bd64b-134">![Audit logs](./media/active-directory-reporting-activity-audit-logs/22.png "Audit logs")</span></span>


## <a name="filtering-audit-logs"></a><span data-ttu-id="bd64b-135">Фильтрация журналов аудита</span><span class="sxs-lookup"><span data-stu-id="bd64b-135">Filtering audit logs</span></span>

<span data-ttu-id="bd64b-136">Для сужения результатов до подходящего уровня вы можете отфильтровать данные аудита, используя следующие поля:</span><span class="sxs-lookup"><span data-stu-id="bd64b-136">To narrow down the reported data to a level that works for you, you can filter the audit data using the following fields:</span></span>

- <span data-ttu-id="bd64b-137">диапазон дат;</span><span class="sxs-lookup"><span data-stu-id="bd64b-137">Date range</span></span>
- <span data-ttu-id="bd64b-138">инициатор (субъект);</span><span class="sxs-lookup"><span data-stu-id="bd64b-138">Initiated by (Actor)</span></span>
- <span data-ttu-id="bd64b-139">Категория</span><span class="sxs-lookup"><span data-stu-id="bd64b-139">Category</span></span>
- <span data-ttu-id="bd64b-140">Тип ресурса действия</span><span class="sxs-lookup"><span data-stu-id="bd64b-140">Activity resource type</span></span>
- <span data-ttu-id="bd64b-141">Действие</span><span class="sxs-lookup"><span data-stu-id="bd64b-141">Activity</span></span>

<span data-ttu-id="bd64b-142">![Журналы аудита](./media/active-directory-reporting-activity-audit-logs/23.png "Журналы аудита")</span><span class="sxs-lookup"><span data-stu-id="bd64b-142">![Audit logs](./media/active-directory-reporting-activity-audit-logs/23.png "Audit logs")</span></span>


<span data-ttu-id="bd64b-143">Фильтр **диапазона дат** позволяет определить интервал времени для возвращаемых данных.</span><span class="sxs-lookup"><span data-stu-id="bd64b-143">The **date range** filter enables to you to define a timeframe for the returned data.</span></span>  
<span data-ttu-id="bd64b-144">Возможные значения:</span><span class="sxs-lookup"><span data-stu-id="bd64b-144">Possible values are:</span></span>

- <span data-ttu-id="bd64b-145">1 месяц</span><span class="sxs-lookup"><span data-stu-id="bd64b-145">1 month</span></span>
- <span data-ttu-id="bd64b-146">7 дней</span><span class="sxs-lookup"><span data-stu-id="bd64b-146">7 days</span></span>
- <span data-ttu-id="bd64b-147">24 часа</span><span class="sxs-lookup"><span data-stu-id="bd64b-147">24 hours</span></span>
- <span data-ttu-id="bd64b-148">Пользовательская</span><span class="sxs-lookup"><span data-stu-id="bd64b-148">Custom</span></span>

<span data-ttu-id="bd64b-149">При выборе пользовательского интервала времени можно настроить время начала и окончания.</span><span class="sxs-lookup"><span data-stu-id="bd64b-149">When you select a custom timeframe, you can configure a start time and an end time.</span></span>

<span data-ttu-id="bd64b-150">Фильтр **Инициатор** позволяет определить имя субъекта или его универсальное имя (UPN).</span><span class="sxs-lookup"><span data-stu-id="bd64b-150">The **initiated by** filter enables you to define an actor's name or its universal principal name (UPN).</span></span>

<span data-ttu-id="bd64b-151">С помощью фильтра **Категория** можно выбрать один из следующих фильтров:</span><span class="sxs-lookup"><span data-stu-id="bd64b-151">The **category** filter enables you to select one of the following filter:</span></span>

- <span data-ttu-id="bd64b-152">Все</span><span class="sxs-lookup"><span data-stu-id="bd64b-152">All</span></span>
- <span data-ttu-id="bd64b-153">Core category (Основная категория);</span><span class="sxs-lookup"><span data-stu-id="bd64b-153">Core category</span></span>
- <span data-ttu-id="bd64b-154">Core directory (Основной каталог);</span><span class="sxs-lookup"><span data-stu-id="bd64b-154">Core directory</span></span>
- <span data-ttu-id="bd64b-155">Self-service password management (Самостоятельное управление паролями);</span><span class="sxs-lookup"><span data-stu-id="bd64b-155">Self-service password management</span></span>
- <span data-ttu-id="bd64b-156">Самостоятельное управление группами</span><span class="sxs-lookup"><span data-stu-id="bd64b-156">Self-service group management</span></span>
- <span data-ttu-id="bd64b-157">Подготовка учетной записи — автоматическая смена паролей</span><span class="sxs-lookup"><span data-stu-id="bd64b-157">Account provisioning- Automated password rollover</span></span>
- <span data-ttu-id="bd64b-158">Приглашенные пользователи</span><span class="sxs-lookup"><span data-stu-id="bd64b-158">Invited users</span></span>
- <span data-ttu-id="bd64b-159">MIM Service (Служба MIM).</span><span class="sxs-lookup"><span data-stu-id="bd64b-159">MIM service</span></span>
- <span data-ttu-id="bd64b-160">Защита идентификации</span><span class="sxs-lookup"><span data-stu-id="bd64b-160">Identity Protection</span></span>
- <span data-ttu-id="bd64b-161">B2C</span><span class="sxs-lookup"><span data-stu-id="bd64b-161">B2C</span></span>

<span data-ttu-id="bd64b-162">С помощью фильтра **Тип ресурса действия** можно выбрать один из следующих фильтров:</span><span class="sxs-lookup"><span data-stu-id="bd64b-162">The **activity resource type** filter enables you to select one of the following filters:</span></span>

- <span data-ttu-id="bd64b-163">Все</span><span class="sxs-lookup"><span data-stu-id="bd64b-163">All</span></span> 
- <span data-ttu-id="bd64b-164">Группа</span><span class="sxs-lookup"><span data-stu-id="bd64b-164">Group</span></span>
- <span data-ttu-id="bd64b-165">Каталог</span><span class="sxs-lookup"><span data-stu-id="bd64b-165">Directory</span></span>
- <span data-ttu-id="bd64b-166">Пользователь</span><span class="sxs-lookup"><span data-stu-id="bd64b-166">User</span></span>
- <span data-ttu-id="bd64b-167">Приложение</span><span class="sxs-lookup"><span data-stu-id="bd64b-167">Application</span></span>
- <span data-ttu-id="bd64b-168">Политика</span><span class="sxs-lookup"><span data-stu-id="bd64b-168">Policy</span></span>
- <span data-ttu-id="bd64b-169">Устройство</span><span class="sxs-lookup"><span data-stu-id="bd64b-169">Device</span></span>
- <span data-ttu-id="bd64b-170">Другие</span><span class="sxs-lookup"><span data-stu-id="bd64b-170">Other</span></span>

<span data-ttu-id="bd64b-171">При выборе **группы** в качестве **типа ресурса действия** вы получите дополнительную категорию фильтра, позволяющую указать **источник**.</span><span class="sxs-lookup"><span data-stu-id="bd64b-171">When you select **Group** as **activity resource type**, you get an additional filter category that enables you to also provide a **Source**:</span></span>

- <span data-ttu-id="bd64b-172">Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd64b-172">Azure AD</span></span>
- <span data-ttu-id="bd64b-173">O365</span><span class="sxs-lookup"><span data-stu-id="bd64b-173">O365</span></span>


<span data-ttu-id="bd64b-174">Фильтр **Действие** зависит от выбранной категории и типа ресурса действия.</span><span class="sxs-lookup"><span data-stu-id="bd64b-174">The **activity** filter is based on the category and Activity resource type selection you make.</span></span> <span data-ttu-id="bd64b-175">Вы можете выбрать определенное действие или просмотреть все.</span><span class="sxs-lookup"><span data-stu-id="bd64b-175">You can select a specific activity you want to see or choose all.</span></span> 

<span data-ttu-id="bd64b-176">Чтобы получить список всех действий аудита, используйте API Graph https://graph.windows.net/$tenantdomain/activities/auditActivityTypes?api-version=beta, где $tenantdomain — это доменное имя, или см. статью о [событиях в отчете аудита](active-directory-reporting-audit-events.md).</span><span class="sxs-lookup"><span data-stu-id="bd64b-176">You can get the list of all Audit Activities using the Graph API https://graph.windows.net/$tenantdomain/activities/auditActivityTypes?api-version=beta, where $tenantdomain = your domain name or refer to the article [audit report events](active-directory-reporting-audit-events.md).</span></span>


## <a name="audit-logs-shortcuts"></a><span data-ttu-id="bd64b-177">Ярлыки журналов аудита</span><span class="sxs-lookup"><span data-stu-id="bd64b-177">Audit logs shortcuts</span></span>

<span data-ttu-id="bd64b-178">Помимо **Azure Active Directory** портал Azure предоставляет две дополнительные точки входа для данных аудита:</span><span class="sxs-lookup"><span data-stu-id="bd64b-178">In addition to **Azure Active Directory**, the Azure portal provides you with two additional entry points to audit data:</span></span>

- <span data-ttu-id="bd64b-179">Пользователи и группы</span><span class="sxs-lookup"><span data-stu-id="bd64b-179">Users and groups</span></span>
- <span data-ttu-id="bd64b-180">корпоративные приложения.</span><span class="sxs-lookup"><span data-stu-id="bd64b-180">Enterprise applications</span></span>

### <a name="users-and-groups-audit-logs"></a><span data-ttu-id="bd64b-181">Журналы аудита пользователей и групп</span><span class="sxs-lookup"><span data-stu-id="bd64b-181">Users and groups audit logs</span></span>

<span data-ttu-id="bd64b-182">Отчеты аудита, касающиеся пользователей и групп, дают возможность ответить на такие вопросы:</span><span class="sxs-lookup"><span data-stu-id="bd64b-182">With user and group-based audit reports, you can get answers to questions such as:</span></span>

- <span data-ttu-id="bd64b-183">Обновления каких типов были применены к пользователям?</span><span class="sxs-lookup"><span data-stu-id="bd64b-183">What types of updates have been applied the users?</span></span>

- <span data-ttu-id="bd64b-184">Сколько пользователей было изменено?</span><span class="sxs-lookup"><span data-stu-id="bd64b-184">How many users were changed?</span></span>

- <span data-ttu-id="bd64b-185">Сколько паролей было изменено?</span><span class="sxs-lookup"><span data-stu-id="bd64b-185">How many passwords were changed?</span></span>

- <span data-ttu-id="bd64b-186">Что делал администратор в каталоге?</span><span class="sxs-lookup"><span data-stu-id="bd64b-186">What has an administrator done in a directory?</span></span>

- <span data-ttu-id="bd64b-187">Какие группы были добавлены?</span><span class="sxs-lookup"><span data-stu-id="bd64b-187">What are the groups that have been added?</span></span>

- <span data-ttu-id="bd64b-188">В каких группах произошли изменения членства?</span><span class="sxs-lookup"><span data-stu-id="bd64b-188">Are there groups with membership changes?</span></span>

- <span data-ttu-id="bd64b-189">Изменены ли владельцы групп?</span><span class="sxs-lookup"><span data-stu-id="bd64b-189">Have the owners of group been changed?</span></span>

- <span data-ttu-id="bd64b-190">Какие лицензии были назначены пользователю или группе?</span><span class="sxs-lookup"><span data-stu-id="bd64b-190">What licenses have been assigned to a group or a user?</span></span>

<span data-ttu-id="bd64b-191">Если нужно только просмотреть данные аудита, связанные с пользователями и группами, отфильтрованное представление вы можете найти, щелкнув элемент **Журналы аудита** в разделе **Действие** колонки **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="bd64b-191">If you just want to review auditing data that is related to users and groups, you can find a filtered view under **Audit logs** in the **Activity** section of the **Users and Groups**.</span></span> <span data-ttu-id="bd64b-192">Для этой точки в качестве **типа ресурса действия** предварительно выбрано значение **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="bd64b-192">This entry point has **Users and groups** as preselected **Activity Resource Type**.</span></span>

<span data-ttu-id="bd64b-193">![Журналы аудита](./media/active-directory-reporting-activity-audit-logs/93.png "Журналы аудита")</span><span class="sxs-lookup"><span data-stu-id="bd64b-193">![Audit logs](./media/active-directory-reporting-activity-audit-logs/93.png "Audit logs")</span></span>

### <a name="enterprise-applications-audit-logs"></a><span data-ttu-id="bd64b-194">Журналы аудита корпоративных приложений</span><span class="sxs-lookup"><span data-stu-id="bd64b-194">Enterprise applications audit logs</span></span>

<span data-ttu-id="bd64b-195">Отчеты аудита, касающиеся приложений, дают возможность ответить на такие вопросы:</span><span class="sxs-lookup"><span data-stu-id="bd64b-195">With application-based audit reports, you can get answers to questions such as:</span></span>

* <span data-ttu-id="bd64b-196">Какие приложения были добавлены или обновлены?</span><span class="sxs-lookup"><span data-stu-id="bd64b-196">What are the applications that have been added or updated?</span></span>
* <span data-ttu-id="bd64b-197">Какие приложения были удалены?</span><span class="sxs-lookup"><span data-stu-id="bd64b-197">What are the applications that have been removed?</span></span>
* <span data-ttu-id="bd64b-198">Изменился ли участник-служба для приложения?</span><span class="sxs-lookup"><span data-stu-id="bd64b-198">Has a service principle for an application changed?</span></span>
* <span data-ttu-id="bd64b-199">Изменены ли имена приложений?</span><span class="sxs-lookup"><span data-stu-id="bd64b-199">Have the names of applications been changed?</span></span>
* <span data-ttu-id="bd64b-200">Кто дал согласие на использование приложения?</span><span class="sxs-lookup"><span data-stu-id="bd64b-200">Who gave consent to an application?</span></span>

<span data-ttu-id="bd64b-201">Если нужно только просмотреть данные аудита, связанные с приложениями, отфильтрованное представление вы можете найти, щелкнув элемент **Журналы аудита** в разделе **Действие** колонки **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="bd64b-201">If you just want to review auditing data that is related to your applications, you can find a filtered view under **Audit logs** in the **Activity** section of the **Enterprise applications** blade.</span></span> <span data-ttu-id="bd64b-202">Для этой точки в качестве **типа ресурса действия** предварительно выбрано значение **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="bd64b-202">This entry point has **Enterprise applications** as preselected **Activity Resource Type**.</span></span>

<span data-ttu-id="bd64b-203">![Журналы аудита](./media/active-directory-reporting-activity-audit-logs/134.png "Журналы аудита")</span><span class="sxs-lookup"><span data-stu-id="bd64b-203">![Audit logs](./media/active-directory-reporting-activity-audit-logs/134.png "Audit logs")</span></span>

<span data-ttu-id="bd64b-204">Вы также можете отфильтровать это представление по **группам** или **пользователям**.</span><span class="sxs-lookup"><span data-stu-id="bd64b-204">You can filter this view further down to just **groups** or just **users**.</span></span>

<span data-ttu-id="bd64b-205">![Журналы аудита](./media/active-directory-reporting-activity-audit-logs/25.png "Журналы аудита")</span><span class="sxs-lookup"><span data-stu-id="bd64b-205">![Audit logs](./media/active-directory-reporting-activity-audit-logs/25.png "Audit logs")</span></span>


## <a name="next-steps"></a><span data-ttu-id="bd64b-206">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bd64b-206">Next steps</span></span>

<span data-ttu-id="bd64b-207">Общие сведения об отчетах Azure Active Directory см. в [этой статье](active-directory-reporting-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="bd64b-207">For an overview of reporting, see the [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span>

