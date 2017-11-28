---
title: "aaaFind отчеты в hello портал Azure | Документы Microsoft"
description: "Узнайте, как отчеты toofind действия Azure Active Directory в hello портал Azure."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: d93521f8-dc21-4feb-aaff-4bb300f04812
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: f8d7a968403e10ccc5319f27fedad38b1553ded0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="find-activity-reports-in-hello-azure-portal"></a><span data-ttu-id="61dfb-103">Найти отчеты о действиях в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="61dfb-103">Find activity reports in hello Azure portal</span></span>

<span data-ttu-id="61dfb-104">При перемещении из hello Azure классического портала toohello портал Azure, вы получаете новый просмотрите журналы действий Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="61dfb-104">If you are moving from hello Azure classic portal toohello Azure portal, you get a new look at Azure Active Directory (Azure AD) activity logs.</span></span> <span data-ttu-id="61dfb-105">В недавно [блога](https://blogs.technet.microsoft.com/enterprisemobility/2016/11/08/azuread-weve-just-turned-on-detailed-auditing-and-sign-in-logs-in-the-new-azure-portal/), мы объясним, как можно просмотреть в контексте hello ресурса hello, вы работаете в hello портал Azure о журналах действий.</span><span class="sxs-lookup"><span data-stu-id="61dfb-105">In a recent [blog post](https://blogs.technet.microsoft.com/enterprisemobility/2016/11/08/azuread-weve-just-turned-on-detailed-auditing-and-sign-in-logs-in-the-new-azure-portal/), we explain how you can see activity logs in hello context of hello resource you are working on in hello Azure portal.</span></span> <span data-ttu-id="61dfb-106">В этой статье описаны как toofind сообщает, который использовался в hello классический портал Azure в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="61dfb-106">In this article, we describe how toofind reports that you used in hello Azure classic portal in hello Azure portal.</span></span>

## <a name="whats-new"></a><span data-ttu-id="61dfb-107">Новые возможности</span><span class="sxs-lookup"><span data-stu-id="61dfb-107">What's new</span></span>

<span data-ttu-id="61dfb-108">Отчеты в классический портал Azure hello разделяются на категории:</span><span class="sxs-lookup"><span data-stu-id="61dfb-108">Reports in hello Azure classic portal are separated into categories:</span></span>

1.  <span data-ttu-id="61dfb-109">Отчеты о безопасности</span><span class="sxs-lookup"><span data-stu-id="61dfb-109">Security reports</span></span>
2.  <span data-ttu-id="61dfb-110">Отчеты об активности</span><span class="sxs-lookup"><span data-stu-id="61dfb-110">Activity reports</span></span>
3.  <span data-ttu-id="61dfb-111">Отчеты интегрированных приложений</span><span class="sxs-lookup"><span data-stu-id="61dfb-111">Integrated app reports</span></span>

### <a name="activity-and-integrated-app-reports"></a><span data-ttu-id="61dfb-112">Отчеты о действиях и отчеты интегрированных приложений</span><span class="sxs-lookup"><span data-stu-id="61dfb-112">Activity and integrated app reports</span></span>

<span data-ttu-id="61dfb-113">Для создания отчетов на основе контекста в hello портал Azure, существующие отчеты, объединяются в единое представление.</span><span class="sxs-lookup"><span data-stu-id="61dfb-113">For context-based reporting in hello Azure portal, existing reports are merged into a single view.</span></span> <span data-ttu-id="61dfb-114">Это один базовый API обеспечивает представление toohello данных hello.</span><span class="sxs-lookup"><span data-stu-id="61dfb-114">A single, underlying API provides hello data toohello view.</span></span>

<span data-ttu-id="61dfb-115">в этом представлении, на hello toosee **Azure Active Directory** колонки в разделе **действия**выберите **журналы аудита**.</span><span class="sxs-lookup"><span data-stu-id="61dfb-115">toosee this view, on hello **Azure Active Directory** blade, under **ACTIVITY**, select **Audit logs**.</span></span>

<span data-ttu-id="61dfb-116">![Журналы аудита](./media/active-directory-reporting-migration/482.png "Журналы аудита")</span><span class="sxs-lookup"><span data-stu-id="61dfb-116">![Audit logs](./media/active-directory-reporting-migration/482.png "Audit logs")</span></span>

<span data-ttu-id="61dfb-117">в этом представлении объединяются Hello следующие отчеты:</span><span class="sxs-lookup"><span data-stu-id="61dfb-117">hello following reports are consolidated in this view:</span></span>

-   <span data-ttu-id="61dfb-118">Отчет аудита</span><span class="sxs-lookup"><span data-stu-id="61dfb-118">Audit report</span></span>
-   <span data-ttu-id="61dfb-119">Действие сброса пароля</span><span class="sxs-lookup"><span data-stu-id="61dfb-119">Password reset activity</span></span>
-   <span data-ttu-id="61dfb-120">Действия регистрации сброса пароля</span><span class="sxs-lookup"><span data-stu-id="61dfb-120">Password reset registration activity</span></span>
-   <span data-ttu-id="61dfb-121">действия групп по самообслуживанию;</span><span class="sxs-lookup"><span data-stu-id="61dfb-121">Self-service groups activity</span></span>
-   <span data-ttu-id="61dfb-122">Операции изменения имен групп Office 365</span><span class="sxs-lookup"><span data-stu-id="61dfb-122">Office365 Group Name Changes</span></span>
-   <span data-ttu-id="61dfb-123">Действия по подготовке учетных записей</span><span class="sxs-lookup"><span data-stu-id="61dfb-123">Account provisioning activity</span></span>
-   <span data-ttu-id="61dfb-124">Состояние смены пароля</span><span class="sxs-lookup"><span data-stu-id="61dfb-124">Password rollover status</span></span>
-   <span data-ttu-id="61dfb-125">Ошибки подготовки учетной записи</span><span class="sxs-lookup"><span data-stu-id="61dfb-125">Account provisioning errors</span></span>


<span data-ttu-id="61dfb-126">отчет об использовании приложения Hello был усовершенствован и теперь включены в hello **входа в систему** представления.</span><span class="sxs-lookup"><span data-stu-id="61dfb-126">hello Application Usage report has been enhanced and is included in hello **Sign-ins** view.</span></span> <span data-ttu-id="61dfb-127">в этом представлении, на hello toosee **Azure Active Directory** колонки в разделе **действия**выберите **входа в систему**.</span><span class="sxs-lookup"><span data-stu-id="61dfb-127">toosee this view, on hello **Azure Active Directory** blade, under **ACTIVITY**, select **Sign-ins**.</span></span>

<span data-ttu-id="61dfb-128">![Представление событий входа](./media/active-directory-reporting-migration/483.png "Представление событий входа")</span><span class="sxs-lookup"><span data-stu-id="61dfb-128">![Sign-ins view](./media/active-directory-reporting-migration/483.png "Sign-ins view")</span></span>

<span data-ttu-id="61dfb-129">Hello **входа в систему** включает в себя всех пользователей входа в систему. Можно использовать эти сведения об использовании приложения tooget сведения.</span><span class="sxs-lookup"><span data-stu-id="61dfb-129">hello **Sign-ins** view includes all user sign-ins. You can use this information tooget application usage information.</span></span> <span data-ttu-id="61dfb-130">Сведения об использовании приложений можно просмотреть в hello **корпоративных приложений** Обзор в hello **УПРАВЛЕНИЕ** раздела.</span><span class="sxs-lookup"><span data-stu-id="61dfb-130">You also can view application usage information in hello **Enterprise applications** overview, in hello **MANAGE** section.</span></span>

<span data-ttu-id="61dfb-131">![Корпоративные приложения](./media/active-directory-reporting-migration/484.png "Корпоративные приложения")</span><span class="sxs-lookup"><span data-stu-id="61dfb-131">![Enterprise applications](./media/active-directory-reporting-migration/484.png "Enterprise applications")</span></span>

## <a name="access-a-specific-report"></a><span data-ttu-id="61dfb-132">Доступ к конкретному отчету</span><span class="sxs-lookup"><span data-stu-id="61dfb-132">Access a specific report</span></span>

<span data-ttu-id="61dfb-133">Несмотря на то, что hello портал Azure предлагает единое представление, также можно найти в конкретных отчетов.</span><span class="sxs-lookup"><span data-stu-id="61dfb-133">Although hello Azure portal offers a single view, you also can look at specific reports.</span></span>

### <a name="audit-logs"></a><span data-ttu-id="61dfb-134">Журналы аудита</span><span class="sxs-lookup"><span data-stu-id="61dfb-134">Audit logs</span></span>

<span data-ttu-id="61dfb-135">Отзывы toocustomer ответ в hello портал Azure можно использовать расширенный фильтрации tooaccess hello нужные данные.</span><span class="sxs-lookup"><span data-stu-id="61dfb-135">In response toocustomer feedback, in hello Azure portal, you can use advanced filtering tooaccess hello data you want.</span></span> <span data-ttu-id="61dfb-136">Можно использовать один фильтр — *категории действий*, перечисляя hello различные виды деятельности входит в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="61dfb-136">One filter you can use is an *activity category*, which lists hello different types of activity logs in Azure AD.</span></span> <span data-ttu-id="61dfb-137">toonarrow результатов toowhat, которую вы ищете, можно выбрать категорию.</span><span class="sxs-lookup"><span data-stu-id="61dfb-137">toonarrow results toowhat you are looking for, you can select a category.</span></span>

<span data-ttu-id="61dfb-138">Например, если вас интересуют только сброс связанные службы tooself пароля действий, вы можете hello **самостоятельного управления паролями** категории.</span><span class="sxs-lookup"><span data-stu-id="61dfb-138">For example, if you are interested only in activities related tooself-service password resets, you can choose hello **Self-service Password Management** category.</span></span> <span data-ttu-id="61dfb-139">Hello категорий, которые вы видите основаны на hello ресурс, который вы работаете.</span><span class="sxs-lookup"><span data-stu-id="61dfb-139">hello categories you see are based on hello resource you are working in.</span></span>  

<span data-ttu-id="61dfb-140">![Категория параметров на странице журналы аудита фильтра hello](./media/active-directory-reporting-migration/06.png "категорий параметров на странице журналы аудита фильтра hello")</span><span class="sxs-lookup"><span data-stu-id="61dfb-140">![Category options on hello Filter Audit Logs page](./media/active-directory-reporting-migration/06.png "Category options on hello Filter Audit Logs page")</span></span>

<span data-ttu-id="61dfb-141">Категории действий включают:</span><span class="sxs-lookup"><span data-stu-id="61dfb-141">Activity categories include:</span></span>

- <span data-ttu-id="61dfb-142">"Core Directory" (Основной каталог);</span><span class="sxs-lookup"><span data-stu-id="61dfb-142">Core Directory</span></span>
- <span data-ttu-id="61dfb-143">"Self-service Password Management" (Самостоятельное управление паролями);</span><span class="sxs-lookup"><span data-stu-id="61dfb-143">Self-service Password Management</span></span>
- <span data-ttu-id="61dfb-144">"Self-service Group Management" (Самостоятельное управление группами);</span><span class="sxs-lookup"><span data-stu-id="61dfb-144">Self-service Group Management</span></span>
- <span data-ttu-id="61dfb-145">"Account Provisioning" (Подготовка учетных записей).</span><span class="sxs-lookup"><span data-stu-id="61dfb-145">Account Provisioning</span></span>

### <a name="application-usage"></a><span data-ttu-id="61dfb-146">Использование приложений</span><span class="sxs-lookup"><span data-stu-id="61dfb-146">Application usage</span></span>

<span data-ttu-id="61dfb-147">tooview сведения об использовании приложения для всех приложений или для одного приложения в разделе **действия**выберите **входа в систему**. toonarrow hello результатов, можно фильтровать по имени пользователя или имени приложения.</span><span class="sxs-lookup"><span data-stu-id="61dfb-147">tooview details about application usage for all apps or for a single app, under **ACTIVITY**, select **Sign-ins**. toonarrow hello results, you can filter on user name or application name.</span></span>

<span data-ttu-id="61dfb-148">![Страница фильтрации событий входа](./media/active-directory-reporting-migration/07.png "Страница фильтрации событий входа")</span><span class="sxs-lookup"><span data-stu-id="61dfb-148">![Filter Sign-In Events page](./media/active-directory-reporting-migration/07.png "Filter Sign-In Events page")</span></span>

### <a name="security-reports"></a><span data-ttu-id="61dfb-149">Отчеты о безопасности</span><span class="sxs-lookup"><span data-stu-id="61dfb-149">Security reports</span></span>

#### <a name="azure-ad-anomalous-activity-reports"></a><span data-ttu-id="61dfb-150">Отчеты Azure AD об аномальных действиях</span><span class="sxs-lookup"><span data-stu-id="61dfb-150">Azure AD anomalous activity reports</span></span>

<span data-ttu-id="61dfb-151">Azure AD аномальных безопасности была tooprovide консолидированные отчеты из hello классический портал Azure в одном,.</span><span class="sxs-lookup"><span data-stu-id="61dfb-151">Azure AD anomalous activity security reports from hello Azure classic portal have been consolidated tooprovide you with one, central view.</span></span> <span data-ttu-id="61dfb-152">В этом представлении отображаются все события, связанные с угрозами безопасности, которые Azure AD может обнаружить и о которых может сообщить.</span><span class="sxs-lookup"><span data-stu-id="61dfb-152">This view shows all security-related risk events that Azure AD can detect and report on.</span></span>

<span data-ttu-id="61dfb-153">Привет, в следующей таблице перечислены отчеты аномальных hello Azure AD и соответствующие типы событий риска в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="61dfb-153">hello following table lists hello Azure AD anomalous activity security reports, and corresponding risk event types in hello Azure portal.</span></span>

| <span data-ttu-id="61dfb-154">Отчеты Azure AD об аномальных действиях</span><span class="sxs-lookup"><span data-stu-id="61dfb-154">Azure AD anomalous activity report</span></span> |  <span data-ttu-id="61dfb-155">Тип события риска в службе защиты идентификации</span><span class="sxs-lookup"><span data-stu-id="61dfb-155">Identity protection risk event type</span></span>|
| :--- | :--- |
| <span data-ttu-id="61dfb-156">Пользователи с утерянными учетными данными</span><span class="sxs-lookup"><span data-stu-id="61dfb-156">Users with leaked credentials</span></span> | <span data-ttu-id="61dfb-157">Утерянные учетные данные</span><span class="sxs-lookup"><span data-stu-id="61dfb-157">Leaked credentials</span></span> |
| <span data-ttu-id="61dfb-158">Нестандартные действия при входе</span><span class="sxs-lookup"><span data-stu-id="61dfb-158">Irregular sign-in activity</span></span> | <span data-ttu-id="61dfb-159">Невозможно tooatypical местоположений</span><span class="sxs-lookup"><span data-stu-id="61dfb-159">Impossible travel tooatypical locations</span></span> |
| <span data-ttu-id="61dfb-160">Попытки входа с возможно инфицированных устройств</span><span class="sxs-lookup"><span data-stu-id="61dfb-160">Sign-ins from possibly infected devices</span></span> | <span data-ttu-id="61dfb-161">Попытки входа с инфицированных устройств</span><span class="sxs-lookup"><span data-stu-id="61dfb-161">Sign-ins from infected devices</span></span>|
| <span data-ttu-id="61dfb-162">Попытки входа из неизвестных источников</span><span class="sxs-lookup"><span data-stu-id="61dfb-162">Sign-ins from unknown sources</span></span> | <span data-ttu-id="61dfb-163">Попытки входа с анонимных IP-адресов</span><span class="sxs-lookup"><span data-stu-id="61dfb-163">Sign-ins from anonymous IP addresses</span></span> |
| <span data-ttu-id="61dfb-164">Попытки входа с IP-адресов с подозрительными действиями</span><span class="sxs-lookup"><span data-stu-id="61dfb-164">Sign-ins from IP addresses with suspicious activity</span></span> | <span data-ttu-id="61dfb-165">Попытки входа с IP-адресов с подозрительными действиями</span><span class="sxs-lookup"><span data-stu-id="61dfb-165">Sign-ins from IP addresses with suspicious activity</span></span> |
| - | <span data-ttu-id="61dfb-166">Попытки входа из неизвестных расположений</span><span class="sxs-lookup"><span data-stu-id="61dfb-166">Sign-ins from unfamiliar locations</span></span> |

<span data-ttu-id="61dfb-167">сообщает Hello, следуя аномальных безопасности Azure AD не включаются как события риска в hello портала Azure:</span><span class="sxs-lookup"><span data-stu-id="61dfb-167">hello following Azure AD anomalous activity security reports are not included as risk events in hello Azure portal:</span></span>

* <span data-ttu-id="61dfb-168">"Операции входа после нескольких неудачных попыток";</span><span class="sxs-lookup"><span data-stu-id="61dfb-168">Sign-ins after multiple failures</span></span>
* <span data-ttu-id="61dfb-169">"Операции входа из нескольких географических регионов".</span><span class="sxs-lookup"><span data-stu-id="61dfb-169">Sign-ins from multiple geographies</span></span>

<span data-ttu-id="61dfb-170">Эти отчеты по-прежнему доступны в hello классический портал Azure, но они будут устаревшими в некоторый момент в будущем hello.</span><span class="sxs-lookup"><span data-stu-id="61dfb-170">These reports are still available in hello Azure classic portal, but they will be deprecated at some time in hello future.</span></span>

<span data-ttu-id="61dfb-171">Дополнительные сведения см. в статье [События риска Azure Active Directory](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="61dfb-171">For more information, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span>  


#### <a name="detected-risk-events"></a><span data-ttu-id="61dfb-172">Обнаруженные события риска</span><span class="sxs-lookup"><span data-stu-id="61dfb-172">Detected risk events</span></span>

<span data-ttu-id="61dfb-173">В hello портал Azure, можно воспользоваться отчетами о событиях, обнаруженных риска на hello **Azure Active Directory** колонки в разделе **безопасности**.</span><span class="sxs-lookup"><span data-stu-id="61dfb-173">In hello Azure portal, you can access reports about detected risk events on hello **Azure Active Directory** blade, under **SECURITY**.</span></span> <span data-ttu-id="61dfb-174">События обнаруженных рисков отслеживаются в hello следующие отчеты:</span><span class="sxs-lookup"><span data-stu-id="61dfb-174">Detected risk events are tracked in hello following reports:</span></span>   

- <span data-ttu-id="61dfb-175">пользователи под угрозой;</span><span class="sxs-lookup"><span data-stu-id="61dfb-175">Users at Risk</span></span>
- <span data-ttu-id="61dfb-176">события входа, представляющие риск.</span><span class="sxs-lookup"><span data-stu-id="61dfb-176">Risky Sign-ins</span></span>

<span data-ttu-id="61dfb-177">![Отчеты системы безопасности](./media/active-directory-reporting-migration/04.png "Отчеты системы безопасности")</span><span class="sxs-lookup"><span data-stu-id="61dfb-177">![Security reports](./media/active-directory-reporting-migration/04.png "Security reports")</span></span>

<span data-ttu-id="61dfb-178">Дополнительные сведения о безопасности отчетов см. по ссылкам ниже.</span><span class="sxs-lookup"><span data-stu-id="61dfb-178">For more information about security reports, see:</span></span>

- [<span data-ttu-id="61dfb-179">Пользователи на риск безопасности отчетов на портале Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="61dfb-179">Users at Risk security report in hello Azure Active Directory portal</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="61dfb-180">Рискованные отчетов входа в систему на портале Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="61dfb-180">Risky Sign-ins report in hello Azure Active Directory portal</span></span>](active-directory-reporting-security-risky-sign-ins.md)


## <a name="activity-reports-in-hello-azure-classic-portal-vs-hello-azure-portal"></a><span data-ttu-id="61dfb-181">Отчеты о действиях в hello классический портал Azure и hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="61dfb-181">Activity reports in hello Azure classic portal vs. hello Azure portal</span></span>

<span data-ttu-id="61dfb-182">Hello в этом разделе перечислены существующие отчеты в hello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="61dfb-182">hello table in this section lists existing reports in hello Azure classic portal.</span></span> <span data-ttu-id="61dfb-183">Он также описывает, как можно получить hello одинаковые данные в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="61dfb-183">It also describes how you can get hello same information in hello Azure portal.</span></span>

<span data-ttu-id="61dfb-184">tooview всех данных на hello аудита **Azure Active Directory** колонки в разделе **действия**, перейти слишком**журналы аудита**.</span><span class="sxs-lookup"><span data-stu-id="61dfb-184">tooview all auditing data, on hello **Azure Active Directory** blade, under **ACTIVITY**, go too**Audit logs**.</span></span>

<span data-ttu-id="61dfb-185">![Журналы аудита](./media/active-directory-reporting-migration/61.png "Журналы аудита")</span><span class="sxs-lookup"><span data-stu-id="61dfb-185">![Audit logs](./media/active-directory-reporting-migration/61.png "Audit logs")</span></span>

| <span data-ttu-id="61dfb-186">Классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="61dfb-186">Azure classic portal</span></span>                 | <span data-ttu-id="61dfb-187">toofind в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="61dfb-187">toofind in hello Azure portal</span></span>                                                         |
| ---                                  | ---                                                                        |
| <span data-ttu-id="61dfb-188">Журналы аудита</span><span class="sxs-lookup"><span data-stu-id="61dfb-188">Audit logs</span></span>                           | <span data-ttu-id="61dfb-189">Для параметра **Activity Category** (Категория действий) выберите **Core Directory** (Основной каталог).</span><span class="sxs-lookup"><span data-stu-id="61dfb-189">For **Activity Category**, select **Core Directory**.</span></span>                       |
| <span data-ttu-id="61dfb-190">Действие сброса пароля</span><span class="sxs-lookup"><span data-stu-id="61dfb-190">Password reset activity</span></span>              | <span data-ttu-id="61dfb-191">Для параметра **Activity Category** (Категория действий) выберите **Self service Password Management** (Самостоятельное управление паролями).</span><span class="sxs-lookup"><span data-stu-id="61dfb-191">For **Activity Category**, select **Self-service Password Management**.</span></span> |
| <span data-ttu-id="61dfb-192">Действия регистрации сброса пароля</span><span class="sxs-lookup"><span data-stu-id="61dfb-192">Password reset registration activity</span></span> | <span data-ttu-id="61dfb-193">Для параметра **Activity Category** (Категория действий) выберите **Self service Password Management** (Самостоятельное управление паролями).</span><span class="sxs-lookup"><span data-stu-id="61dfb-193">For **Activity Category**, select **Self-service Password Management**.</span></span>     |
| <span data-ttu-id="61dfb-194">Действия групп по самообслуживанию</span><span class="sxs-lookup"><span data-stu-id="61dfb-194">Self-service groups activity</span></span>         | <span data-ttu-id="61dfb-195">Для параметра **Activity Category** (Категория действий) выберите **Self service Group Management** (Самостоятельное управление группами).</span><span class="sxs-lookup"><span data-stu-id="61dfb-195">For **Activity Category**, select **Self-service Group Management**.</span></span>        |
| <span data-ttu-id="61dfb-196">Действия по подготовке учетных записей</span><span class="sxs-lookup"><span data-stu-id="61dfb-196">Account provisioning activity</span></span>        | <span data-ttu-id="61dfb-197">Для параметра **Activity Category** (Категория действий) выберите **Account User Provisioning** (Подготовка учетных записей пользователей).</span><span class="sxs-lookup"><span data-stu-id="61dfb-197">For **Activity Category**, select **Account User Provisioning**.</span></span>         |
| <span data-ttu-id="61dfb-198">Состояние смены пароля</span><span class="sxs-lookup"><span data-stu-id="61dfb-198">Password rollover status</span></span>             | <span data-ttu-id="61dfb-199">Для параметра **Activity Category** (Категория действий) выберите **Automatic App Password Rollover** (Автоматическая смена паролей приложений).</span><span class="sxs-lookup"><span data-stu-id="61dfb-199">For **Activity Category**, select **Automatic App Password Rollover**.</span></span>      |
| <span data-ttu-id="61dfb-200">Ошибки подготовки учетной записи</span><span class="sxs-lookup"><span data-stu-id="61dfb-200">Account provisioning errors</span></span>          | <span data-ttu-id="61dfb-201">Для параметра **Activity Category** (Категория действий) выберите **Account User Provisioning** (Подготовка учетных записей пользователей).</span><span class="sxs-lookup"><span data-stu-id="61dfb-201">For **Activity Category**, select **Account User Provisioning**.</span></span>        |
| <span data-ttu-id="61dfb-202">Операции изменения имен групп Office 365</span><span class="sxs-lookup"><span data-stu-id="61dfb-202">Office365 Group Name Changes</span></span>         | <span data-ttu-id="61dfb-203">Для параметра **Activity Category** (Категория действий) выберите **Self service Password Management** (Самостоятельное управление паролями).</span><span class="sxs-lookup"><span data-stu-id="61dfb-203">For **Activity Category**, select **Self-service Password Management**.</span></span> <span data-ttu-id="61dfb-204">Для параметра **Activity Resource Type** (Тип ресурсов действия) выберите **Группа**.</span><span class="sxs-lookup"><span data-stu-id="61dfb-204">For **Activity Resource Type**, select **Group**.</span></span> <span data-ttu-id="61dfb-205">Для параметра **Activity Source** (Источник действия) выберите **O365 groups** (Группы Office 365).</span><span class="sxs-lookup"><span data-stu-id="61dfb-205">For **Activity Source**, select **O365 groups**.</span></span>|

<span data-ttu-id="61dfb-206">tooview hello **использование приложения** отчета на hello **Azure Active Directory** колонки в разделе **УПРАВЛЕНИЕ**выберите **корпоративных приложений**, а затем выберите **входа в систему**.</span><span class="sxs-lookup"><span data-stu-id="61dfb-206">tooview hello **Application Usage** report, on hello **Azure Active Directory** blade, under **MANAGE**, select **Enterprise Applications**, and then select **Sign-ins**.</span></span>


<span data-ttu-id="61dfb-207">![Отчет о событиях входа в корпоративные приложения](./media/active-directory-reporting-migration/199.png "Отчет о событиях входа в корпоративные приложения")</span><span class="sxs-lookup"><span data-stu-id="61dfb-207">![Enterprise Applications Sign-Ins report](./media/active-directory-reporting-migration/199.png "Enterprise Applications Sign-Ins report")</span></span>

## <a name="next-steps"></a><span data-ttu-id="61dfb-208">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="61dfb-208">Next steps</span></span>

<span data-ttu-id="61dfb-209">Обзор отчетов см. в разделе hello [отчетов Azure Active Directory](active-directory-reporting-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="61dfb-209">For an overview of reporting, see hello [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span>
