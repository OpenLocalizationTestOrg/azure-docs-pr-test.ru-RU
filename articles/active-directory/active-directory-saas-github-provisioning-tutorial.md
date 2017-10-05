---
title: "Руководство по настройке GitHub для автоматической подготовки пользователей с помощью Azure Active Directory | Документация Майкрософт"
description: "Узнайте, как настроить Azure Active Directory для автоматической подготовки и отзыва учетных записей пользователей в GitHub."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: stevenpo
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: asmalser-msft
ms.openlocfilehash: 3cc70273e95dbf4913e7bbcd8a37bd9a52987b60
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-configuring-github-for-automatic-user-provisioning"></a><span data-ttu-id="1194a-103">Руководство по настройке GitHub для автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="1194a-103">Tutorial: Configuring GitHub for Automatic User Provisioning</span></span>


<span data-ttu-id="1194a-104">Цель этого руководства — показать, как в GitHub и Azure AD настроить автоматическую подготовку и отзыв учетных записей пользователей из Azure AD в GitHub.</span><span class="sxs-lookup"><span data-stu-id="1194a-104">The objective of this tutorial is to show you the steps you need to perform in GitHub and Azure AD to automatically provision and de-provision user accounts from Azure AD to GitHub.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="1194a-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1194a-105">Prerequisites</span></span>

<span data-ttu-id="1194a-106">Сценарий, описанный в этом учебнике, предполагает, что у вас уже имеется:</span><span class="sxs-lookup"><span data-stu-id="1194a-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="1194a-107">клиент Azure Active Directory;</span><span class="sxs-lookup"><span data-stu-id="1194a-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="1194a-108">клиент GitHub с включенным планом [Business](https://help.github.com/articles/organization-billing-plans/#business-plan) или выше;</span><span class="sxs-lookup"><span data-stu-id="1194a-108">A Github tenant with the [Business plan](https://help.github.com/articles/organization-billing-plans/#business-plan) or better enabled</span></span> 
*   <span data-ttu-id="1194a-109">учетная запись пользователя в GitHub с разрешениями администратора.</span><span class="sxs-lookup"><span data-stu-id="1194a-109">A user account in GitHub with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="1194a-110">Интеграция подготовки в Azure AD зависит от [API SCIM GitHub](https://developer.github.com/v3/scim/), доступного для команд GitHub, использующих план Business или выше.</span><span class="sxs-lookup"><span data-stu-id="1194a-110">The Azure AD provisioning integration relies on the [GitHub SCIM API](https://developer.github.com/v3/scim/), which is available to Github teams on the Business plan or better.</span></span>

## <a name="assigning-users-to-github"></a><span data-ttu-id="1194a-111">Назначение пользователей в GitHub</span><span class="sxs-lookup"><span data-stu-id="1194a-111">Assigning users to GitHub</span></span>

<span data-ttu-id="1194a-112">В Azure Active Directory для определения того, какие пользователи должны получать доступ к выбранным приложениям, используется концепция, называемая "назначение".</span><span class="sxs-lookup"><span data-stu-id="1194a-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="1194a-113">В контексте автоматической подготовки учетной записи будут синхронизированы только те записи и группы, которые были "назначены" приложению в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1194a-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="1194a-114">Перед настройкой и включением службы подготовки необходимо решить, какие пользователи или группы в Azure AD представляют пользователей, которым требуется доступ к приложению GitHub.</span><span class="sxs-lookup"><span data-stu-id="1194a-114">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your GitHub app.</span></span> <span data-ttu-id="1194a-115">Когда этот вопрос будет решен, можно назначить этих пользователей приложению GitHub, следуя приведенным ниже указаниям.</span><span class="sxs-lookup"><span data-stu-id="1194a-115">Once decided, you can assign these users to your GitHub app by following the instructions here:</span></span>

[<span data-ttu-id="1194a-116">Назначение корпоративному приложению пользователя или группы</span><span class="sxs-lookup"><span data-stu-id="1194a-116">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-github"></a><span data-ttu-id="1194a-117">Важные советы по назначению пользователей в GitHub</span><span class="sxs-lookup"><span data-stu-id="1194a-117">Important tips for assigning users to GitHub</span></span>

*   <span data-ttu-id="1194a-118">Рекомендуется назначить одного пользователя Azure AD в GitHub для тестирования конфигурации подготовки.</span><span class="sxs-lookup"><span data-stu-id="1194a-118">It is recommended that a single Azure AD user is assigned to GitHub to test the provisioning configuration.</span></span> <span data-ttu-id="1194a-119">Дополнительные пользователи и/или группы можно назначить позднее.</span><span class="sxs-lookup"><span data-stu-id="1194a-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="1194a-120">При назначении пользователя в GitHub в диалоговом окне назначения необходимо выбрать роль **пользователя** или другую действительную роль для конкретного приложения (если доступно).</span><span class="sxs-lookup"><span data-stu-id="1194a-120">When assigning a user to GitHub, you must select either the **User** role, or another valid application-specific role (if available) in the assignment dialog.</span></span> <span data-ttu-id="1194a-121">Роль **Доступ по умолчанию** не подходит для подготовки, и эти пользователи пропускаются.</span><span class="sxs-lookup"><span data-stu-id="1194a-121">The **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-to-github"></a><span data-ttu-id="1194a-122">Настройка подготовки учетных записей пользователей в GitHub</span><span class="sxs-lookup"><span data-stu-id="1194a-122">Configuring user provisioning to GitHub</span></span> 

<span data-ttu-id="1194a-123">В этом разделе описывается подключение вашего каталога Azure AD к API подготовки учетных записей пользователей в GitHub и настройка службы подготовки для создания, обновления и отключения назначенных учетных записей пользователей в GitHub на основе назначения пользователей и групп в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1194a-123">This section guides you through connecting your Azure AD to GitHub's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in GitHub based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="1194a-124">Для GitHub можно также включить единый вход на основе SAML. Для этого следуйте инструкциям на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1194a-124">You may also choose to enabled SAML-based Single Sign-On for GitHub, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="1194a-125">Единый вход можно настроить независимо от автоматической подготовки, хотя эти две возможности дополняют друг друга.</span><span class="sxs-lookup"><span data-stu-id="1194a-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-to-github-in-azure-ad"></a><span data-ttu-id="1194a-126">Настройка автоматической подготовки учетных записей пользователей для GitHub в Azure AD</span><span class="sxs-lookup"><span data-stu-id="1194a-126">Configure automatic user account provisioning to GitHub in Azure AD</span></span>


1. <span data-ttu-id="1194a-127">На [портале Azure](https://portal.azure.com) перейдите в раздел **Azure Active Directory > Корпоративные приложения > Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="1194a-127">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="1194a-128">Если в GitHub уже настроен единый вход, найдите свой экземпляр GitHub с помощью поля поиска.</span><span class="sxs-lookup"><span data-stu-id="1194a-128">If you have already configured GitHub for single sign-on, search for your instance of GitHub using the search field.</span></span> <span data-ttu-id="1194a-129">В противном случае щелкните **Добавить** и выполните поиск **GitHub** в коллекции приложений.</span><span class="sxs-lookup"><span data-stu-id="1194a-129">Otherwise, select **Add** and search for **GitHub** in the application gallery.</span></span> <span data-ttu-id="1194a-130">Выберите GitHub в результатах поиска и добавьте в список приложений.</span><span class="sxs-lookup"><span data-stu-id="1194a-130">Select GitHub from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="1194a-131">Выберите экземпляр GitHub, а затем перейдите на вкладку **Подготовка**.</span><span class="sxs-lookup"><span data-stu-id="1194a-131">Select your instance of GitHub, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="1194a-132">Для параметра **Режим подготовки к работе** выберите значение **Automatic** (Автоматически).</span><span class="sxs-lookup"><span data-stu-id="1194a-132">Set the **Provisioning Mode** to **Automatic**.</span></span>

    ![Подготовка GitHub](./media/active-directory-saas-github-provisioning-tutorial/GitHub1.png)

5. <span data-ttu-id="1194a-134">В разделе **Учетные данные администратора** щелкните **Авторизовать**.</span><span class="sxs-lookup"><span data-stu-id="1194a-134">Under the **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="1194a-135">В новом окне браузера откроется диалоговое окно авторизации GitHub.</span><span class="sxs-lookup"><span data-stu-id="1194a-135">This operation opens a GitHub authorization dialog in a new browser window.</span></span> 

6. <span data-ttu-id="1194a-136">В новом окне войдите в GitHub с использованием учетной записи администратора.</span><span class="sxs-lookup"><span data-stu-id="1194a-136">In the new window, sign into GitHub using your Admin account.</span></span> <span data-ttu-id="1194a-137">В открывшемся диалоговом окне авторизации выберите команду GitHub, для которой необходимо включить подготовку, а затем щелкните **Авторизовать**.</span><span class="sxs-lookup"><span data-stu-id="1194a-137">In the resulting authorization dialog, select the GitHub team that you want to enable provisioning for, and then select **Authorize**.</span></span> <span data-ttu-id="1194a-138">После завершения вернитесь на портал Azure для завершения настройки подготовки.</span><span class="sxs-lookup"><span data-stu-id="1194a-138">Once completed, return to the Azure portal to complete the provisioning configuration.</span></span>

    ![Диалоговое окно авторизации](./media/active-directory-saas-github-provisioning-tutorial/GitHub2.png)

7. <span data-ttu-id="1194a-140">На портале Azure введите **URL-адрес клиента** и щелкните **Проверить подключение**, чтобы убедиться в том, что Azure AD может подключиться к вашему приложению GitHub.</span><span class="sxs-lookup"><span data-stu-id="1194a-140">In the Azure portal, input **Tenant URL** and click **Test Connection** to ensure Azure AD can connect to your GitHub app.</span></span> <span data-ttu-id="1194a-141">Если установить подключение не удалось, убедитесь, что у вашей учетной записи GitHub имеются разрешения администратора и **URL-адрес клиента** введен правильно, а затем повторите авторизацию. **URL-адрес клиента** можно указать в формате https://api.github.com/scim/v2/organizations/ + <название_организации>, а свои организации можно найти в учетной записи GitHub, выбрав **Параметры** > **Организации**.</span><span class="sxs-lookup"><span data-stu-id="1194a-141">If the connection fails, ensure your GitHub account has Admin permissions and **Tenant URl** is inputted correctly, then try the "Authorize" step again (you can constitute **Tenant URL** by rule: "https://api.github.com/scim/v2/organizations/ + <Organizations_name>", you can find your organizations under your GitHub account: **Settings** > **Organizations**).</span></span>

    ![Диалоговое окно авторизации](./media/active-directory-saas-github-provisioning-tutorial/GitHub3.png)

8. <span data-ttu-id="1194a-143">В поле **Почтовое уведомление** введите адрес электронной почты пользователя или группы, которые должны получать уведомления об ошибках подготовки, а также установите флажок "Отправить уведомление по электронной почте при сбое".</span><span class="sxs-lookup"><span data-stu-id="1194a-143">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox "Send an email notification when a failure occurs."</span></span>

9. <span data-ttu-id="1194a-144">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="1194a-144">Click **Save**.</span></span> 

10. <span data-ttu-id="1194a-145">В разделе "Сопоставления" выберите **Synchronize Azure Active Directory Users to GitHub** (Синхронизировать пользователей Azure Active Directory с GitHub).</span><span class="sxs-lookup"><span data-stu-id="1194a-145">Under the Mappings section, select **Synchronize Azure Active Directory Users to GitHub**.</span></span>

11. <span data-ttu-id="1194a-146">В разделе **Сопоставления атрибутов** просмотрите пользовательские атрибуты, которые синхронизированы из Azure AD в GitHub.</span><span class="sxs-lookup"><span data-stu-id="1194a-146">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to GitHub.</span></span> <span data-ttu-id="1194a-147">Атрибуты, выбранные как свойства **Matching**, используются для сопоставления учетных записей пользователей в GitHub для операций обновления.</span><span class="sxs-lookup"><span data-stu-id="1194a-147">The attributes selected as **Matching** properties are used to match the user accounts in GitHub for update operations.</span></span> <span data-ttu-id="1194a-148">Нажмите кнопку "Сохранить", чтобы подтвердить все изменения.</span><span class="sxs-lookup"><span data-stu-id="1194a-148">Select the Save button to commit any changes.</span></span>

12. <span data-ttu-id="1194a-149">Чтобы включить службу подготовки Azure AD для GitHub, в разделе **Параметры** измените значение параметра **Состояние подготовки** на **Включено**.</span><span class="sxs-lookup"><span data-stu-id="1194a-149">To enable the Azure AD provisioning service for GitHub, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

13. <span data-ttu-id="1194a-150">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="1194a-150">Click **Save**.</span></span> 

<span data-ttu-id="1194a-151">После этого начнется начальная синхронизация всех пользователей и (или) групп, назначенных в GitHub в разделе "Пользователи и группы".</span><span class="sxs-lookup"><span data-stu-id="1194a-151">This operation starts the initial synchronization of any users and/or groups assigned to GitHub in the Users and Groups section.</span></span> <span data-ttu-id="1194a-152">Начальная синхронизация занимает больше времени, чем последующие операции синхронизации. Последующие операции синхронизации выполняются примерно каждые 20 минут, при условии, что служба запущена.</span><span class="sxs-lookup"><span data-stu-id="1194a-152">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="1194a-153">В разделе **Сведения о синхронизации** можно отслеживать ход выполнения и переходить по ссылкам для просмотра отчетов о подготовке, в которых зафиксированы все действия, выполняемые службой подготовки.</span><span class="sxs-lookup"><span data-stu-id="1194a-153">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service.</span></span>

<span data-ttu-id="1194a-154">Дополнительные сведения о чтении журналов подготовки Azure AD см. в руководстве по [отчетам об автоматической подготовке учетных записей](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="1194a-154">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="1194a-155">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="1194a-155">Additional resources</span></span>

* [<span data-ttu-id="1194a-156">Управление подготовкой учетных записей пользователей для корпоративных приложений</span><span class="sxs-lookup"><span data-stu-id="1194a-156">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="1194a-157">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1194a-157">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="1194a-158">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1194a-158">Next steps</span></span>

* [<span data-ttu-id="1194a-159">Сведения о просмотре журналов и получении отчетов о действиях по подготовке</span><span class="sxs-lookup"><span data-stu-id="1194a-159">Learn how to review logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
