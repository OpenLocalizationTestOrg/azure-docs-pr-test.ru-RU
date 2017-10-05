---
title: "Отчеты о действиях входа на портале Azure Active Directory | Документация Майкрософт"
description: "Общие сведения об отчетах о действиях входа на портале Azure Active Directory."
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
ms.openlocfilehash: b9e61950654ba427b09dd608d354589a0804aaa5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="sign-in-activity-reports-in-the-azure-active-directory-portal"></a><span data-ttu-id="6bc82-103">Отчеты о действиях входа на портале Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6bc82-103">Sign-in activity reports in the Azure Active Directory portal</span></span>

<span data-ttu-id="6bc82-104">Функция отчетов в Azure Active Directory (Azure AD) [на портале Azure](https://portal.azure.com) позволяет получать всю необходимую информацию, чтобы определить, как работает среда.</span><span class="sxs-lookup"><span data-stu-id="6bc82-104">With Azure Active Directory (Azure AD) reporting in the [Azure portal](https://portal.azure.com), you can get the information you need to determine how your environment is doing.</span></span>

<span data-ttu-id="6bc82-105">Архитектура создания отчетов в Azure Active Directory состоит из следующих компонентов.</span><span class="sxs-lookup"><span data-stu-id="6bc82-105">The reporting architecture in Azure Active Directory consists of the following components:</span></span>

- <span data-ttu-id="6bc82-106">**Действие**</span><span class="sxs-lookup"><span data-stu-id="6bc82-106">**Activity**</span></span> 
    - <span data-ttu-id="6bc82-107">**Действия входа** — информация об использовании управляемых приложений и действиях входа.</span><span class="sxs-lookup"><span data-stu-id="6bc82-107">**Sign-in activities** – Information about the usage of managed applications and user sign-in activities</span></span>
    - <span data-ttu-id="6bc82-108">**Журналы аудита** — данные системных операций об управлении пользователями и группами, об управляемых приложениях и действиях с каталогами.</span><span class="sxs-lookup"><span data-stu-id="6bc82-108">**Audit logs** - System activity information about users and group management, your managed applications and directory activities.</span></span>
- <span data-ttu-id="6bc82-109">**Безопасность**</span><span class="sxs-lookup"><span data-stu-id="6bc82-109">**Security**</span></span> 
    - <span data-ttu-id="6bc82-110">**Входы, представляющие риск**. Вход, представляющий риск, означает, что в систему пытался войти пользователь, который не является законным владельцем учетной записи.</span><span class="sxs-lookup"><span data-stu-id="6bc82-110">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span></span> <span data-ttu-id="6bc82-111">Дополнительные сведения см. в разделе "Вход, представляющий риск".</span><span class="sxs-lookup"><span data-stu-id="6bc82-111">For more details, see Risky sign-ins.</span></span>
    - <span data-ttu-id="6bc82-112">**Пользователи, находящиеся в группе риска**. Такая пометка означает, что конфиденциальность учетной записи пользователя, возможно, нарушена.</span><span class="sxs-lookup"><span data-stu-id="6bc82-112">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="6bc82-113">Дополнительные сведения см. в разделе "Пользователи, помеченные для события риска".</span><span class="sxs-lookup"><span data-stu-id="6bc82-113">For more details, see Users flagged for risk.</span></span>

<span data-ttu-id="6bc82-114">В этом разделе содержатся общие сведения о действиях входа.</span><span class="sxs-lookup"><span data-stu-id="6bc82-114">This topic gives you an overview of the sign-in activities.</span></span>

## <a name="pre-requisite"></a><span data-ttu-id="6bc82-115">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6bc82-115">Pre-requisite</span></span>

### <a name="who-can-access-the-data"></a><span data-ttu-id="6bc82-116">Кто может получить доступ к данным?</span><span class="sxs-lookup"><span data-stu-id="6bc82-116">Who can access the data?</span></span>
* <span data-ttu-id="6bc82-117">Пользователи с ролью администратора безопасности или читателя безопасности</span><span class="sxs-lookup"><span data-stu-id="6bc82-117">Users in the Security Admin or Security Reader role</span></span>
* <span data-ttu-id="6bc82-118">Глобальные администраторы</span><span class="sxs-lookup"><span data-stu-id="6bc82-118">Global Admins</span></span>
* <span data-ttu-id="6bc82-119">Любой пользователь (не администратор) может получить доступ к своим данным о действиях входа.</span><span class="sxs-lookup"><span data-stu-id="6bc82-119">Any user (non-admins) can access their own sign-ins</span></span> 

### <a name="what-azure-ad-license-do-you-need-to-access-sign-in-activity"></a><span data-ttu-id="6bc82-120">Какие лицензии Azure AD требуются для доступа к действию входа?</span><span class="sxs-lookup"><span data-stu-id="6bc82-120">What Azure AD license do you need to access sign-in activity?</span></span>
* <span data-ttu-id="6bc82-121">Для просмотра отчета о всех действиях входа с клиентом должна быть связана лицензия Azure AD Premium.</span><span class="sxs-lookup"><span data-stu-id="6bc82-121">Your tenant must have an Azure AD Premium license associated with it to see the all up sign-in activity report</span></span>


## <a name="signs-in-activities"></a><span data-ttu-id="6bc82-122">Действия входа</span><span class="sxs-lookup"><span data-stu-id="6bc82-122">Signs-in activities</span></span>

<span data-ttu-id="6bc82-123">Информация, доступная в отчете о входе пользователя, поможет вам ответить на такие вопросы:</span><span class="sxs-lookup"><span data-stu-id="6bc82-123">With the information provided by the user sign-in report, you find answers to questions such as:</span></span>

* <span data-ttu-id="6bc82-124">Что такое шаблон входа пользователя?</span><span class="sxs-lookup"><span data-stu-id="6bc82-124">What is the sign-in pattern of a user?</span></span>
* <span data-ttu-id="6bc82-125">Сколько пользователей входили в течение недели?</span><span class="sxs-lookup"><span data-stu-id="6bc82-125">How many users have users signed in over a week?</span></span>
* <span data-ttu-id="6bc82-126">Каков статус их входа?</span><span class="sxs-lookup"><span data-stu-id="6bc82-126">What’s the status of these sign-ins?</span></span>

<span data-ttu-id="6bc82-127">Знакомство с данными о действиях входа следует начать с раздела **События входа** в разделе "Действие" службы **Azure Active**.</span><span class="sxs-lookup"><span data-stu-id="6bc82-127">Your first entry point to all sign-in activities data is **Sign-ins** in the Activity section of **Azure Active**.</span></span>


<span data-ttu-id="6bc82-128">![Действие входа](./media/active-directory-reporting-activity-sign-ins/61.png "Действие входа")</span><span class="sxs-lookup"><span data-stu-id="6bc82-128">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/61.png "Sign-in activity")</span></span>


<span data-ttu-id="6bc82-129">Журнал аудита содержит представление списка по умолчанию, в котором отображаются:</span><span class="sxs-lookup"><span data-stu-id="6bc82-129">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="6bc82-130">пользователь;</span><span class="sxs-lookup"><span data-stu-id="6bc82-130">the related user</span></span>
- <span data-ttu-id="6bc82-131">приложение, в которое вошел пользователь;</span><span class="sxs-lookup"><span data-stu-id="6bc82-131">the application the user has signed-in to</span></span>
- <span data-ttu-id="6bc82-132">состояние входа;</span><span class="sxs-lookup"><span data-stu-id="6bc82-132">the sign-in status</span></span>
- <span data-ttu-id="6bc82-133">время входа.</span><span class="sxs-lookup"><span data-stu-id="6bc82-133">the sign-in time</span></span>

<span data-ttu-id="6bc82-134">![Действие входа](./media/active-directory-reporting-activity-sign-ins/41.png "Действие входа")</span><span class="sxs-lookup"><span data-stu-id="6bc82-134">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/41.png "Sign-in activity")</span></span>

<span data-ttu-id="6bc82-135">Представление списка можно настроить, щелкнув **Столбцы** на панели инструментов.</span><span class="sxs-lookup"><span data-stu-id="6bc82-135">You can customize the list view by clicking **Columns** in the toolbar.</span></span>

<span data-ttu-id="6bc82-136">![Действие входа](./media/active-directory-reporting-activity-sign-ins/19.png "Действие входа")</span><span class="sxs-lookup"><span data-stu-id="6bc82-136">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/19.png "Sign-in activity")</span></span>

<span data-ttu-id="6bc82-137">Здесь вы можете добавить или удалить отображаемые поля.</span><span class="sxs-lookup"><span data-stu-id="6bc82-137">This enables you to display additional fields or remove fields that are already displayed.</span></span>

<span data-ttu-id="6bc82-138">![Действие входа](./media/active-directory-reporting-activity-sign-ins/42.png "Действие входа")</span><span class="sxs-lookup"><span data-stu-id="6bc82-138">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/42.png "Sign-in activity")</span></span>

<span data-ttu-id="6bc82-139">Щелкнув элемент в представлении списка, вы получите дополнительные сведения о нем.</span><span class="sxs-lookup"><span data-stu-id="6bc82-139">By clicking an item in the list view, you get all available details about it.</span></span>

<span data-ttu-id="6bc82-140">![Действие входа](./media/active-directory-reporting-activity-sign-ins/43.png "Действие входа")</span><span class="sxs-lookup"><span data-stu-id="6bc82-140">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/43.png "Sign-in activity")</span></span>


## <a name="filtering-sign-in-activities"></a><span data-ttu-id="6bc82-141">Фильтрация действий входа</span><span class="sxs-lookup"><span data-stu-id="6bc82-141">Filtering sign-in activities</span></span>

<span data-ttu-id="6bc82-142">Для сужения результатов до нужного уровня вы можете отфильтровать данные о входах, используя следующие поля:</span><span class="sxs-lookup"><span data-stu-id="6bc82-142">To narrow down the reported data to a level that works for you, you can filter the sign-ins data using the following fields:</span></span>

- <span data-ttu-id="6bc82-143">"Интервал времени	";</span><span class="sxs-lookup"><span data-stu-id="6bc82-143">Time interval</span></span>
- <span data-ttu-id="6bc82-144">Пользователь</span><span class="sxs-lookup"><span data-stu-id="6bc82-144">User</span></span>
- <span data-ttu-id="6bc82-145">Приложение</span><span class="sxs-lookup"><span data-stu-id="6bc82-145">Application</span></span>
- <span data-ttu-id="6bc82-146">Клиент</span><span class="sxs-lookup"><span data-stu-id="6bc82-146">Client</span></span>
- <span data-ttu-id="6bc82-147">состояние входа.</span><span class="sxs-lookup"><span data-stu-id="6bc82-147">Sign-in status</span></span>

<span data-ttu-id="6bc82-148">![Действие входа](./media/active-directory-reporting-activity-sign-ins/44.png "Действие входа")</span><span class="sxs-lookup"><span data-stu-id="6bc82-148">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/44.png "Sign-in activity")</span></span>


<span data-ttu-id="6bc82-149">Фильтр по **интервалу времени** позволяет определить интервал времени для возвращаемых данных.</span><span class="sxs-lookup"><span data-stu-id="6bc82-149">The **time interval** filter enables to you to define a timeframe for the returned data.</span></span>  
<span data-ttu-id="6bc82-150">Возможные значения:</span><span class="sxs-lookup"><span data-stu-id="6bc82-150">Possible values are:</span></span>

- <span data-ttu-id="6bc82-151">1 месяц</span><span class="sxs-lookup"><span data-stu-id="6bc82-151">1 month</span></span>
- <span data-ttu-id="6bc82-152">7 дней</span><span class="sxs-lookup"><span data-stu-id="6bc82-152">7 days</span></span>
- <span data-ttu-id="6bc82-153">24 часа</span><span class="sxs-lookup"><span data-stu-id="6bc82-153">24 hours</span></span>
- <span data-ttu-id="6bc82-154">Пользовательская</span><span class="sxs-lookup"><span data-stu-id="6bc82-154">Custom</span></span>

<span data-ttu-id="6bc82-155">При выборе пользовательского интервала времени можно настроить время начала и окончания.</span><span class="sxs-lookup"><span data-stu-id="6bc82-155">When you select a custom timeframe, you can configure a start time and an end time.</span></span>

<span data-ttu-id="6bc82-156">Фильтр по **пользователю** позволяет указать интересующее вас имя пользователя или имя участника-пользователя (UPN).</span><span class="sxs-lookup"><span data-stu-id="6bc82-156">The **user** filter enables you to specify the name or the user principal name (UPN) of the user you care about.</span></span>

<span data-ttu-id="6bc82-157">Фильтр по **приложению** позволяет указать имя интересующего вас приложения.</span><span class="sxs-lookup"><span data-stu-id="6bc82-157">The **application** filter enables you to specify the name of the application you care about.</span></span>

<span data-ttu-id="6bc82-158">Фильтр по **клиенту** позволяет указать сведения об интересующем вас устройстве.</span><span class="sxs-lookup"><span data-stu-id="6bc82-158">The **client** filter enables you to specify information about the device you care about.</span></span>

<span data-ttu-id="6bc82-159">В фильтре по **состоянию входа** можно выбрать один из следующих фильтров:</span><span class="sxs-lookup"><span data-stu-id="6bc82-159">The **sign-in status** filter enables you to select one of the following filter:</span></span>

- <span data-ttu-id="6bc82-160">Все</span><span class="sxs-lookup"><span data-stu-id="6bc82-160">All</span></span>
- <span data-ttu-id="6bc82-161">Успешно</span><span class="sxs-lookup"><span data-stu-id="6bc82-161">Success</span></span>
- <span data-ttu-id="6bc82-162">Сбой</span><span class="sxs-lookup"><span data-stu-id="6bc82-162">Failure</span></span>


## <a name="sign-in-activities-shortcuts"></a><span data-ttu-id="6bc82-163">Ярлыки для действий входа</span><span class="sxs-lookup"><span data-stu-id="6bc82-163">Sign-in activities shortcuts</span></span>

<span data-ttu-id="6bc82-164">Помимо Azure Active Directory, портал Azure предоставляет две дополнительные точки входа для данных о действиях входа:</span><span class="sxs-lookup"><span data-stu-id="6bc82-164">In addition to Azure Active Directory, the Azure portal provides you with two additional entry points to sign-in activities data:</span></span>

- <span data-ttu-id="6bc82-165">Пользователи и группы</span><span class="sxs-lookup"><span data-stu-id="6bc82-165">Users and groups</span></span>
- <span data-ttu-id="6bc82-166">корпоративные приложения.</span><span class="sxs-lookup"><span data-stu-id="6bc82-166">Enterprise applications</span></span>


### <a name="users-and-groups-sign-ins-activities"></a><span data-ttu-id="6bc82-167">Действия входа для пользователей и групп</span><span class="sxs-lookup"><span data-stu-id="6bc82-167">Users and groups sign-ins activities</span></span>

<span data-ttu-id="6bc82-168">Информация, доступная в отчете о входе пользователя, поможет вам ответить на такие вопросы:</span><span class="sxs-lookup"><span data-stu-id="6bc82-168">With the information provided by the user sign-in report, you find answers to questions such as:</span></span>

- <span data-ttu-id="6bc82-169">Что такое шаблон входа пользователя?</span><span class="sxs-lookup"><span data-stu-id="6bc82-169">What is the sign-in pattern of a user?</span></span>
- <span data-ttu-id="6bc82-170">Сколько пользователей входили в течение недели?</span><span class="sxs-lookup"><span data-stu-id="6bc82-170">How many users have users signed in over a week?</span></span>
- <span data-ttu-id="6bc82-171">Каков статус их входа?</span><span class="sxs-lookup"><span data-stu-id="6bc82-171">What’s the status of these sign-ins?</span></span>



<span data-ttu-id="6bc82-172">Знакомство с этими данными нужно начать с графика входов пользователей в разделе **Обзор**, который можно выбрать в колонке **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="6bc82-172">Your entry point to this data is the user sign-in graph in the **Overview** section under **Users and groups**.</span></span>

<span data-ttu-id="6bc82-173">![Действие входа](./media/active-directory-reporting-activity-sign-ins/45.png "Действие входа")</span><span class="sxs-lookup"><span data-stu-id="6bc82-173">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/45.png "Sign-in activity")</span></span>

<span data-ttu-id="6bc82-174">На графике входа еженедельно отображается количество входов всех пользователей за определенный промежуток времени,</span><span class="sxs-lookup"><span data-stu-id="6bc82-174">The user sign-in graph shows weekly aggregations of sign ins for all users in a given time period.</span></span> <span data-ttu-id="6bc82-175">который по умолчанию составляет 30 дней.</span><span class="sxs-lookup"><span data-stu-id="6bc82-175">The default for the time period is 30 days.</span></span>

<span data-ttu-id="6bc82-176">![Действие входа](./media/active-directory-reporting-activity-sign-ins/46.png "Действие входа")</span><span class="sxs-lookup"><span data-stu-id="6bc82-176">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/46.png "Sign-in activity")</span></span>

<span data-ttu-id="6bc82-177">Щелкнув день на графике входов, вы увидите подробный список действий входа за этот день.</span><span class="sxs-lookup"><span data-stu-id="6bc82-177">When you click on a day in the sign-in graph, you get a detailed list of the sign-in activities for this day.</span></span>

<span data-ttu-id="6bc82-178">![Действие входа](./media/active-directory-reporting-activity-sign-ins/41.png "Действие входа")</span><span class="sxs-lookup"><span data-stu-id="6bc82-178">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/41.png "Sign-in activity")</span></span>

<span data-ttu-id="6bc82-179">Каждая строка в списке действий входа содержит подробную информацию о выбранном входе и отвечает на такие вопросы:</span><span class="sxs-lookup"><span data-stu-id="6bc82-179">Each row in the sign-in activities list gives you the detailed information about the selected sign-in such as:</span></span>

* <span data-ttu-id="6bc82-180">Кто выполнил вход?</span><span class="sxs-lookup"><span data-stu-id="6bc82-180">Who has signed in?</span></span>
* <span data-ttu-id="6bc82-181">Какое связанное имя участника-пользователя фигурировало?</span><span class="sxs-lookup"><span data-stu-id="6bc82-181">What was the related UPN?</span></span>
* <span data-ttu-id="6bc82-182">Какое приложение было целью входа?</span><span class="sxs-lookup"><span data-stu-id="6bc82-182">What application was the target of the sign-in?</span></span>
* <span data-ttu-id="6bc82-183">С какого IP-адреса выполнен вход?</span><span class="sxs-lookup"><span data-stu-id="6bc82-183">What is the IP address of the sign-in?</span></span>
* <span data-ttu-id="6bc82-184">Каким был статус входа?</span><span class="sxs-lookup"><span data-stu-id="6bc82-184">What was the status of the sign-in?</span></span>

<span data-ttu-id="6bc82-185">С помощью параметра **События входа** можно полностью отобразить все входы пользователей.</span><span class="sxs-lookup"><span data-stu-id="6bc82-185">The **Sign-ins** option gives you a complete overview of all user sign-ins.</span></span>

<span data-ttu-id="6bc82-186">![Действие входа](./media/active-directory-reporting-activity-sign-ins/51.png "Действие входа")</span><span class="sxs-lookup"><span data-stu-id="6bc82-186">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/51.png "Sign-in activity")</span></span>



## <a name="usage-of-managed-applications"></a><span data-ttu-id="6bc82-187">Использование управляемых приложений</span><span class="sxs-lookup"><span data-stu-id="6bc82-187">Usage of managed applications</span></span>

<span data-ttu-id="6bc82-188">Представление данных входа, ориентированное на приложения, позволяет ответить на такие вопросы:</span><span class="sxs-lookup"><span data-stu-id="6bc82-188">With an application-centric view of your sign-in data, you can answer questions such as:</span></span>

* <span data-ttu-id="6bc82-189">Кто использует мои приложения?</span><span class="sxs-lookup"><span data-stu-id="6bc82-189">Who is using my applications?</span></span>
* <span data-ttu-id="6bc82-190">Какие три приложения являются самыми популярными в моей организации?</span><span class="sxs-lookup"><span data-stu-id="6bc82-190">What are the top 3 applications in your organization?</span></span>
* <span data-ttu-id="6bc82-191">Как обстоят дела с приложением, которое</span><span class="sxs-lookup"><span data-stu-id="6bc82-191">I have recently rolled out an application.</span></span> <span data-ttu-id="6bc82-192">было недавно создано и развернуто?</span><span class="sxs-lookup"><span data-stu-id="6bc82-192">How is it doing?</span></span>

<span data-ttu-id="6bc82-193">Знакомство с этими данными нужно начать с трех приложений, которые в отчете за последние 30 дней являются самыми популярными (раздел **Обзор**, который можно выбрать в колонке **Корпоративные приложения**).</span><span class="sxs-lookup"><span data-stu-id="6bc82-193">Your entry point to this data is the top 3 applications in your organization within the last 30 days report in the **Overview** section under **Enterprise applications**.</span></span>

<span data-ttu-id="6bc82-194">![Действие входа](./media/active-directory-reporting-activity-sign-ins/64.png "Действие входа")</span><span class="sxs-lookup"><span data-stu-id="6bc82-194">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/64.png "Sign-in activity")</span></span>

<span data-ttu-id="6bc82-195">В графике ниже (график использования приложений) отображены еженедельные входы в три самых популярных приложения за определенный промежуток времени,</span><span class="sxs-lookup"><span data-stu-id="6bc82-195">The app usage graph weekly aggregations of sign ins for your top 3 applications in a given time period.</span></span> <span data-ttu-id="6bc82-196">который по умолчанию составляет 30 дней.</span><span class="sxs-lookup"><span data-stu-id="6bc82-196">The default for the time period is 30 days.</span></span>

<span data-ttu-id="6bc82-197">![Действие входа](./media/active-directory-reporting-activity-sign-ins/47.png "Действие входа")</span><span class="sxs-lookup"><span data-stu-id="6bc82-197">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/47.png "Sign-in activity")</span></span>

<span data-ttu-id="6bc82-198">Если нужно, вы можете переместить фокус на определенное приложение.</span><span class="sxs-lookup"><span data-stu-id="6bc82-198">If you want to, you can set the focus on a specific application.</span></span>


<span data-ttu-id="6bc82-199">![Отчеты](./media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "Отчеты")</span><span class="sxs-lookup"><span data-stu-id="6bc82-199">![Reporting](./media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "Reporting")</span></span>

<span data-ttu-id="6bc82-200">Щелкнув день на графике использования приложений, вы увидите подробный список действий входа.</span><span class="sxs-lookup"><span data-stu-id="6bc82-200">When you click on a day in the app usage graph, you get a detailed list of the sign-in activities.</span></span>


<span data-ttu-id="6bc82-201">![Действие входа](./media/active-directory-reporting-activity-sign-ins/48.png "Действие входа")</span><span class="sxs-lookup"><span data-stu-id="6bc82-201">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/48.png "Sign-in activity")</span></span>


<span data-ttu-id="6bc82-202">С помощью параметра **Входов** можно полностью отобразить все события входа в ваши приложения.</span><span class="sxs-lookup"><span data-stu-id="6bc82-202">The **Sign-ins** option gives you a complete overview of all sign-in events to your applications.</span></span>

<span data-ttu-id="6bc82-203">![Действие входа](./media/active-directory-reporting-activity-sign-ins/49.png "Действие входа")</span><span class="sxs-lookup"><span data-stu-id="6bc82-203">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/49.png "Sign-in activity")</span></span>



## <a name="next-steps"></a><span data-ttu-id="6bc82-204">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6bc82-204">Next steps</span></span>

<span data-ttu-id="6bc82-205">Дополнительные сведения о кодах ошибок входа в систему см. в статье [Коды ошибок отчета об активности входа на портале Azure Active Directory](active-directory-reporting-activity-sign-ins-errors.md).</span><span class="sxs-lookup"><span data-stu-id="6bc82-205">If you want to know more about sign-in activity error codes, see the [Sign-in activity report error codes in the Azure Active Directory portal](active-directory-reporting-activity-sign-ins-errors.md).</span></span>

