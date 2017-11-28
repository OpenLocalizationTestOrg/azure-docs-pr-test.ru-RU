---
title: "отчеты о действиях aaaSign в портале Azure Active Directory hello | Документы Microsoft"
description: "Отчеты о действиях в toosign введение в портале Azure Active Directory hello"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 4b18127b-d1d0-4bdc-8f9c-6a4c991c5f75
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 49590d625a08d7dc189a629b89bab2261c2b4780
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-activity-reports-in-hello-azure-active-directory-portal"></a><span data-ttu-id="6152f-103">Отчеты действия при входе в портал hello Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6152f-103">Sign-in activity reports in hello Azure Active Directory portal</span></span>

<span data-ttu-id="6152f-104">С отчетами Azure Active Directory (Azure AD) в hello [портал Azure](https://portal.azure.com), можно получить hello информацию, необходимую toodetermine, насколько среды.</span><span class="sxs-lookup"><span data-stu-id="6152f-104">With Azure Active Directory (Azure AD) reporting in hello [Azure portal](https://portal.azure.com), you can get hello information you need toodetermine how your environment is doing.</span></span>

<span data-ttu-id="6152f-105">Hello архитектуры в Azure Active Directory отчетов состоит из hello следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="6152f-105">hello reporting architecture in Azure Active Directory consists of hello following components:</span></span>

- <span data-ttu-id="6152f-106">**Действие**</span><span class="sxs-lookup"><span data-stu-id="6152f-106">**Activity**</span></span> 
    - <span data-ttu-id="6152f-107">**Действия входа** — сведения об использовании hello управляемых приложений и действий входа пользователей</span><span class="sxs-lookup"><span data-stu-id="6152f-107">**Sign-in activities** – Information about hello usage of managed applications and user sign-in activities</span></span>
    - <span data-ttu-id="6152f-108">**Журналы аудита** — данные системных операций об управлении пользователями и группами, об управляемых приложениях и действиях с каталогами.</span><span class="sxs-lookup"><span data-stu-id="6152f-108">**Audit logs** - System activity information about users and group management, your managed applications and directory activities.</span></span>
- <span data-ttu-id="6152f-109">**Безопасность**</span><span class="sxs-lookup"><span data-stu-id="6152f-109">**Security**</span></span> 
    - <span data-ttu-id="6152f-110">**Рискованные входы** -рискованным вход является показателем для попытки входа, возможно, выполнены с тем, кто не hello законный владельцем учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="6152f-110">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> <span data-ttu-id="6152f-111">Дополнительные сведения см. в разделе "Вход, представляющий риск".</span><span class="sxs-lookup"><span data-stu-id="6152f-111">For more details, see Risky sign-ins.</span></span>
    - <span data-ttu-id="6152f-112">**Пользователи, находящиеся в группе риска**. Такая пометка означает, что конфиденциальность учетной записи пользователя, возможно, нарушена.</span><span class="sxs-lookup"><span data-stu-id="6152f-112">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="6152f-113">Дополнительные сведения см. в разделе "Пользователи, помеченные для события риска".</span><span class="sxs-lookup"><span data-stu-id="6152f-113">For more details, see Users flagged for risk.</span></span>

<span data-ttu-id="6152f-114">В этом разделе дается обзор hello вход действий.</span><span class="sxs-lookup"><span data-stu-id="6152f-114">This topic gives you an overview of hello sign-in activities.</span></span>

## <a name="pre-requisite"></a><span data-ttu-id="6152f-115">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6152f-115">Pre-requisite</span></span>

### <a name="who-can-access-hello-data"></a><span data-ttu-id="6152f-116">Кто имеет доступ к данным hello?</span><span class="sxs-lookup"><span data-stu-id="6152f-116">Who can access hello data?</span></span>
* <span data-ttu-id="6152f-117">Пользователи с ролью администратора безопасности или безопасность чтения hello</span><span class="sxs-lookup"><span data-stu-id="6152f-117">Users in hello Security Admin or Security Reader role</span></span>
* <span data-ttu-id="6152f-118">Глобальные администраторы</span><span class="sxs-lookup"><span data-stu-id="6152f-118">Global Admins</span></span>
* <span data-ttu-id="6152f-119">Любой пользователь (не администратор) может получить доступ к своим данным о действиях входа.</span><span class="sxs-lookup"><span data-stu-id="6152f-119">Any user (non-admins) can access their own sign-ins</span></span> 

### <a name="what-azure-ad-license-do-you-need-tooaccess-sign-in-activity"></a><span data-ttu-id="6152f-120">Какая лицензия Azure AD требуются действия при входе tooaccess?</span><span class="sxs-lookup"><span data-stu-id="6152f-120">What Azure AD license do you need tooaccess sign-in activity?</span></span>
* <span data-ttu-id="6152f-121">Клиент должен иметь лицензию Azure AD Premium, связанные с ним отчет об активности до все учетное toosee hello</span><span class="sxs-lookup"><span data-stu-id="6152f-121">Your tenant must have an Azure AD Premium license associated with it toosee hello all up sign-in activity report</span></span>


## <a name="signs-in-activities"></a><span data-ttu-id="6152f-122">Действия входа</span><span class="sxs-lookup"><span data-stu-id="6152f-122">Signs-in activities</span></span>

<span data-ttu-id="6152f-123">Hello сведений, предоставляемых отчет вход пользователей hello находить ответы tooquestions, такие как:</span><span class="sxs-lookup"><span data-stu-id="6152f-123">With hello information provided by hello user sign-in report, you find answers tooquestions such as:</span></span>

* <span data-ttu-id="6152f-124">Что такое hello вход шаблон пользователя?</span><span class="sxs-lookup"><span data-stu-id="6152f-124">What is hello sign-in pattern of a user?</span></span>
* <span data-ttu-id="6152f-125">Сколько пользователей входили в течение недели?</span><span class="sxs-lookup"><span data-stu-id="6152f-125">How many users have users signed in over a week?</span></span>
* <span data-ttu-id="6152f-126">Что такое состояние hello эти входа в систему?</span><span class="sxs-lookup"><span data-stu-id="6152f-126">What’s hello status of these sign-ins?</span></span>

<span data-ttu-id="6152f-127">Первая запись tooall точки входа в действиях данные **входа в систему** hello действия из раздела **Azure Active**.</span><span class="sxs-lookup"><span data-stu-id="6152f-127">Your first entry point tooall sign-in activities data is **Sign-ins** in hello Activity section of **Azure Active**.</span></span>


<span data-ttu-id="6152f-128">![Действие входа](./media/active-directory-reporting-activity-sign-ins/61.png "Действие входа")</span><span class="sxs-lookup"><span data-stu-id="6152f-128">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/61.png "Sign-in activity")</span></span>


<span data-ttu-id="6152f-129">Журнал аудита содержит представление списка по умолчанию, в котором отображаются:</span><span class="sxs-lookup"><span data-stu-id="6152f-129">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="6152f-130">Hello связанных пользователей</span><span class="sxs-lookup"><span data-stu-id="6152f-130">hello related user</span></span>
- <span data-ttu-id="6152f-131">Hello приложения hello пользователь в системе</span><span class="sxs-lookup"><span data-stu-id="6152f-131">hello application hello user has signed-in to</span></span>
- <span data-ttu-id="6152f-132">Состояние регистрации Hello</span><span class="sxs-lookup"><span data-stu-id="6152f-132">hello sign-in status</span></span>
- <span data-ttu-id="6152f-133">время входа Hello</span><span class="sxs-lookup"><span data-stu-id="6152f-133">hello sign-in time</span></span>

<span data-ttu-id="6152f-134">![Действие входа](./media/active-directory-reporting-activity-sign-ins/41.png "Действие входа")</span><span class="sxs-lookup"><span data-stu-id="6152f-134">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/41.png "Sign-in activity")</span></span>

<span data-ttu-id="6152f-135">Представление списка hello можно настроить, щелкнув **столбцы** инструментов hello.</span><span class="sxs-lookup"><span data-stu-id="6152f-135">You can customize hello list view by clicking **Columns** in hello toolbar.</span></span>

<span data-ttu-id="6152f-136">![Действие входа](./media/active-directory-reporting-activity-sign-ins/19.png "Действие входа")</span><span class="sxs-lookup"><span data-stu-id="6152f-136">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/19.png "Sign-in activity")</span></span>

<span data-ttu-id="6152f-137">Это позволяет toodisplay дополнительные поля или удалять поля, которые уже отображаются.</span><span class="sxs-lookup"><span data-stu-id="6152f-137">This enables you toodisplay additional fields or remove fields that are already displayed.</span></span>

<span data-ttu-id="6152f-138">![Действие входа](./media/active-directory-reporting-activity-sign-ins/42.png "Действие входа")</span><span class="sxs-lookup"><span data-stu-id="6152f-138">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/42.png "Sign-in activity")</span></span>

<span data-ttu-id="6152f-139">Щелкнув элемент в представлении списка hello, получение всех доступных сведений о нем.</span><span class="sxs-lookup"><span data-stu-id="6152f-139">By clicking an item in hello list view, you get all available details about it.</span></span>

<span data-ttu-id="6152f-140">![Действие входа](./media/active-directory-reporting-activity-sign-ins/43.png "Действие входа")</span><span class="sxs-lookup"><span data-stu-id="6152f-140">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/43.png "Sign-in activity")</span></span>


## <a name="filtering-sign-in-activities"></a><span data-ttu-id="6152f-141">Фильтрация действий входа</span><span class="sxs-lookup"><span data-stu-id="6152f-141">Filtering sign-in activities</span></span>

<span data-ttu-id="6152f-142">toonarrow вниз hello сообщила tooa уровень данных, что работает автоматически, можно фильтровать hello данные входа в систему, используя hello следующие поля:</span><span class="sxs-lookup"><span data-stu-id="6152f-142">toonarrow down hello reported data tooa level that works for you, you can filter hello sign-ins data using hello following fields:</span></span>

- <span data-ttu-id="6152f-143">"Интервал времени	";</span><span class="sxs-lookup"><span data-stu-id="6152f-143">Time interval</span></span>
- <span data-ttu-id="6152f-144">Пользователь</span><span class="sxs-lookup"><span data-stu-id="6152f-144">User</span></span>
- <span data-ttu-id="6152f-145">Приложение</span><span class="sxs-lookup"><span data-stu-id="6152f-145">Application</span></span>
- <span data-ttu-id="6152f-146">Клиент</span><span class="sxs-lookup"><span data-stu-id="6152f-146">Client</span></span>
- <span data-ttu-id="6152f-147">состояние входа.</span><span class="sxs-lookup"><span data-stu-id="6152f-147">Sign-in status</span></span>

<span data-ttu-id="6152f-148">![Действие входа](./media/active-directory-reporting-activity-sign-ins/44.png "Действие входа")</span><span class="sxs-lookup"><span data-stu-id="6152f-148">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/44.png "Sign-in activity")</span></span>


<span data-ttu-id="6152f-149">Hello **интервал времени** фильтр включает tooyou toodefine период времени для hello возвращаемых данных.</span><span class="sxs-lookup"><span data-stu-id="6152f-149">hello **time interval** filter enables tooyou toodefine a timeframe for hello returned data.</span></span>  
<span data-ttu-id="6152f-150">Возможные значения:</span><span class="sxs-lookup"><span data-stu-id="6152f-150">Possible values are:</span></span>

- <span data-ttu-id="6152f-151">1 месяц</span><span class="sxs-lookup"><span data-stu-id="6152f-151">1 month</span></span>
- <span data-ttu-id="6152f-152">7 дней</span><span class="sxs-lookup"><span data-stu-id="6152f-152">7 days</span></span>
- <span data-ttu-id="6152f-153">24 часа</span><span class="sxs-lookup"><span data-stu-id="6152f-153">24 hours</span></span>
- <span data-ttu-id="6152f-154">Пользовательская</span><span class="sxs-lookup"><span data-stu-id="6152f-154">Custom</span></span>

<span data-ttu-id="6152f-155">При выборе пользовательского интервала времени можно настроить время начала и окончания.</span><span class="sxs-lookup"><span data-stu-id="6152f-155">When you select a custom timeframe, you can configure a start time and an end time.</span></span>

<span data-ttu-id="6152f-156">Hello **пользователя** фильтр включает имя hello toospecify или hello имя участника-пользователя (UPN) пользователя hello, важные для вас.</span><span class="sxs-lookup"><span data-stu-id="6152f-156">hello **user** filter enables you toospecify hello name or hello user principal name (UPN) of hello user you care about.</span></span>

<span data-ttu-id="6152f-157">Hello **приложения** фильтр включает имя hello toospecify приложения hello, важные для вас.</span><span class="sxs-lookup"><span data-stu-id="6152f-157">hello **application** filter enables you toospecify hello name of hello application you care about.</span></span>

<span data-ttu-id="6152f-158">Hello **клиента** фильтр позволяет toospecify сведения об устройстве hello, важные для вас.</span><span class="sxs-lookup"><span data-stu-id="6152f-158">hello **client** filter enables you toospecify information about hello device you care about.</span></span>

<span data-ttu-id="6152f-159">Hello **состояния входа** фильтр позволяет tooselect один hello следующий фильтр:</span><span class="sxs-lookup"><span data-stu-id="6152f-159">hello **sign-in status** filter enables you tooselect one of hello following filter:</span></span>

- <span data-ttu-id="6152f-160">Все</span><span class="sxs-lookup"><span data-stu-id="6152f-160">All</span></span>
- <span data-ttu-id="6152f-161">Успешно</span><span class="sxs-lookup"><span data-stu-id="6152f-161">Success</span></span>
- <span data-ttu-id="6152f-162">Сбой</span><span class="sxs-lookup"><span data-stu-id="6152f-162">Failure</span></span>


## <a name="sign-in-activities-shortcuts"></a><span data-ttu-id="6152f-163">Ярлыки для действий входа</span><span class="sxs-lookup"><span data-stu-id="6152f-163">Sign-in activities shortcuts</span></span>

<span data-ttu-id="6152f-164">В дополнение к этому tooAzure Active Directory hello портал Azure предоставляет два дополнительную операцию точек действий в toosign данные:</span><span class="sxs-lookup"><span data-stu-id="6152f-164">In addition tooAzure Active Directory, hello Azure portal provides you with two additional entry points toosign-in activities data:</span></span>

- <span data-ttu-id="6152f-165">Пользователи и группы</span><span class="sxs-lookup"><span data-stu-id="6152f-165">Users and groups</span></span>
- <span data-ttu-id="6152f-166">корпоративные приложения.</span><span class="sxs-lookup"><span data-stu-id="6152f-166">Enterprise applications</span></span>


### <a name="users-and-groups-sign-ins-activities"></a><span data-ttu-id="6152f-167">Действия входа для пользователей и групп</span><span class="sxs-lookup"><span data-stu-id="6152f-167">Users and groups sign-ins activities</span></span>

<span data-ttu-id="6152f-168">Hello сведений, предоставляемых отчет вход пользователей hello находить ответы tooquestions, такие как:</span><span class="sxs-lookup"><span data-stu-id="6152f-168">With hello information provided by hello user sign-in report, you find answers tooquestions such as:</span></span>

- <span data-ttu-id="6152f-169">Что такое hello вход шаблон пользователя?</span><span class="sxs-lookup"><span data-stu-id="6152f-169">What is hello sign-in pattern of a user?</span></span>
- <span data-ttu-id="6152f-170">Сколько пользователей входили в течение недели?</span><span class="sxs-lookup"><span data-stu-id="6152f-170">How many users have users signed in over a week?</span></span>
- <span data-ttu-id="6152f-171">Что такое состояние hello эти входа в систему?</span><span class="sxs-lookup"><span data-stu-id="6152f-171">What’s hello status of these sign-ins?</span></span>



<span data-ttu-id="6152f-172">Данные точки toothis входа — hello пользователя войти граф в hello **Обзор** раздела **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="6152f-172">Your entry point toothis data is hello user sign-in graph in hello **Overview** section under **Users and groups**.</span></span>

<span data-ttu-id="6152f-173">![Действие входа](./media/active-directory-reporting-activity-sign-ins/45.png "Действие входа")</span><span class="sxs-lookup"><span data-stu-id="6152f-173">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/45.png "Sign-in activity")</span></span>

<span data-ttu-id="6152f-174">Hello пользователя войти графике показано еженедельное агрегаты входа модули для всех пользователей в определенный период времени.</span><span class="sxs-lookup"><span data-stu-id="6152f-174">hello user sign-in graph shows weekly aggregations of sign ins for all users in a given time period.</span></span> <span data-ttu-id="6152f-175">по умолчанию Hello для hello срок — 30 дней.</span><span class="sxs-lookup"><span data-stu-id="6152f-175">hello default for hello time period is 30 days.</span></span>

<span data-ttu-id="6152f-176">![Действие входа](./media/active-directory-reporting-activity-sign-ins/46.png "Действие входа")</span><span class="sxs-lookup"><span data-stu-id="6152f-176">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/46.png "Sign-in activity")</span></span>

<span data-ttu-id="6152f-177">При нажатии на день hello входа в диаграмме отображается подробный список hello вход действий за этот день.</span><span class="sxs-lookup"><span data-stu-id="6152f-177">When you click on a day in hello sign-in graph, you get a detailed list of hello sign-in activities for this day.</span></span>

<span data-ttu-id="6152f-178">![Действие входа](./media/active-directory-reporting-activity-sign-ins/41.png "Действие входа")</span><span class="sxs-lookup"><span data-stu-id="6152f-178">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/41.png "Sign-in activity")</span></span>

<span data-ttu-id="6152f-179">Каждая строка hello действия входа в списке обеспечивает hello подробные сведения о выбранной hello вход как:</span><span class="sxs-lookup"><span data-stu-id="6152f-179">Each row in hello sign-in activities list gives you hello detailed information about hello selected sign-in such as:</span></span>

* <span data-ttu-id="6152f-180">Кто выполнил вход?</span><span class="sxs-lookup"><span data-stu-id="6152f-180">Who has signed in?</span></span>
* <span data-ttu-id="6152f-181">Каково было hello связаны имя участника-пользователя?</span><span class="sxs-lookup"><span data-stu-id="6152f-181">What was hello related UPN?</span></span>
* <span data-ttu-id="6152f-182">Какие приложения была целью hello hello входа в систему?</span><span class="sxs-lookup"><span data-stu-id="6152f-182">What application was hello target of hello sign-in?</span></span>
* <span data-ttu-id="6152f-183">Что такое hello IP-адрес входа в hello</span><span class="sxs-lookup"><span data-stu-id="6152f-183">What is hello IP address of hello sign-in?</span></span>
* <span data-ttu-id="6152f-184">Была состояние hello hello входа в систему?</span><span class="sxs-lookup"><span data-stu-id="6152f-184">What was hello status of hello sign-in?</span></span>

<span data-ttu-id="6152f-185">Hello **входа в систему** параметр дает полный обзор всех попытках входа пользователя.</span><span class="sxs-lookup"><span data-stu-id="6152f-185">hello **Sign-ins** option gives you a complete overview of all user sign-ins.</span></span>

<span data-ttu-id="6152f-186">![Действие входа](./media/active-directory-reporting-activity-sign-ins/51.png "Действие входа")</span><span class="sxs-lookup"><span data-stu-id="6152f-186">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/51.png "Sign-in activity")</span></span>



## <a name="usage-of-managed-applications"></a><span data-ttu-id="6152f-187">Использование управляемых приложений</span><span class="sxs-lookup"><span data-stu-id="6152f-187">Usage of managed applications</span></span>

<span data-ttu-id="6152f-188">Представление данных входа, ориентированное на приложения, позволяет ответить на такие вопросы:</span><span class="sxs-lookup"><span data-stu-id="6152f-188">With an application-centric view of your sign-in data, you can answer questions such as:</span></span>

* <span data-ttu-id="6152f-189">Кто использует мои приложения?</span><span class="sxs-lookup"><span data-stu-id="6152f-189">Who is using my applications?</span></span>
* <span data-ttu-id="6152f-190">Что такое top 3 приложения hello в вашей организации?</span><span class="sxs-lookup"><span data-stu-id="6152f-190">What are hello top 3 applications in your organization?</span></span>
* <span data-ttu-id="6152f-191">Как обстоят дела с приложением, которое</span><span class="sxs-lookup"><span data-stu-id="6152f-191">I have recently rolled out an application.</span></span> <span data-ttu-id="6152f-192">было недавно создано и развернуто?</span><span class="sxs-lookup"><span data-stu-id="6152f-192">How is it doing?</span></span>

<span data-ttu-id="6152f-193">Запись toothis точка данных является hello основных 3 приложений в вашей организации в отчете последние 30 дней hello в hello **Обзор** раздела **корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="6152f-193">Your entry point toothis data is hello top 3 applications in your organization within hello last 30 days report in hello **Overview** section under **Enterprise applications**.</span></span>

<span data-ttu-id="6152f-194">![Действие входа](./media/active-directory-reporting-activity-sign-ins/64.png "Действие входа")</span><span class="sxs-lookup"><span data-stu-id="6152f-194">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/64.png "Sign-in activity")</span></span>

<span data-ttu-id="6152f-195">Hello приложения использования graph еженедельно агрегаты входа для приложений первые 3 в указанный период времени.</span><span class="sxs-lookup"><span data-stu-id="6152f-195">hello app usage graph weekly aggregations of sign ins for your top 3 applications in a given time period.</span></span> <span data-ttu-id="6152f-196">по умолчанию Hello для hello срок — 30 дней.</span><span class="sxs-lookup"><span data-stu-id="6152f-196">hello default for hello time period is 30 days.</span></span>

<span data-ttu-id="6152f-197">![Действие входа](./media/active-directory-reporting-activity-sign-ins/47.png "Действие входа")</span><span class="sxs-lookup"><span data-stu-id="6152f-197">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/47.png "Sign-in activity")</span></span>

<span data-ttu-id="6152f-198">Если вы хотите, можно задать hello фокус на определенное приложение.</span><span class="sxs-lookup"><span data-stu-id="6152f-198">If you want to, you can set hello focus on a specific application.</span></span>


<span data-ttu-id="6152f-199">![Отчеты](./media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "Отчеты")</span><span class="sxs-lookup"><span data-stu-id="6152f-199">![Reporting](./media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "Reporting")</span></span>

<span data-ttu-id="6152f-200">При нажатии на день в графиках использования приложения hello, вы получаете подробный список hello вход действий.</span><span class="sxs-lookup"><span data-stu-id="6152f-200">When you click on a day in hello app usage graph, you get a detailed list of hello sign-in activities.</span></span>


<span data-ttu-id="6152f-201">![Действие входа](./media/active-directory-reporting-activity-sign-ins/48.png "Действие входа")</span><span class="sxs-lookup"><span data-stu-id="6152f-201">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/48.png "Sign-in activity")</span></span>


<span data-ttu-id="6152f-202">Hello **входа в систему** параметр дает полный обзор всех событий входа tooyour приложений.</span><span class="sxs-lookup"><span data-stu-id="6152f-202">hello **Sign-ins** option gives you a complete overview of all sign-in events tooyour applications.</span></span>

<span data-ttu-id="6152f-203">![Действие входа](./media/active-directory-reporting-activity-sign-ins/49.png "Действие входа")</span><span class="sxs-lookup"><span data-stu-id="6152f-203">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/49.png "Sign-in activity")</span></span>



## <a name="next-steps"></a><span data-ttu-id="6152f-204">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6152f-204">Next steps</span></span>

<span data-ttu-id="6152f-205">Tooknow Дополнительные сведения о кодах ошибок действия при входе, в статье hello [входа действие отчета коды ошибок на портале Azure Active Directory hello](active-directory-reporting-activity-sign-ins-errors.md).</span><span class="sxs-lookup"><span data-stu-id="6152f-205">If you want tooknow more about sign-in activity error codes, see hello [Sign-in activity report error codes in hello Azure Active Directory portal](active-directory-reporting-activity-sign-ins-errors.md).</span></span>

