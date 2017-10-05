---
title: "Учебник. Интеграция Azure Active Directory с Concur | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Concur."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: df47f55f-a894-4e01-a82e-0dbf55fc8af1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: cd35b6e2dc3171e9cffdb820bbc5b0d45ff58e07
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-concur-for-user-provisioning"></a><span data-ttu-id="7b1b1-103">Руководство по настройке Concur для подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="7b1b1-103">Tutorial: Configuring Concur for User Provisioning</span></span>

<span data-ttu-id="7b1b1-104">Цель этого руководства — показать, как в Concur и Azure AD необходимо выполнять автоматическую подготовку и отмену подготовки учетных записей пользователей из Azure AD в Concur.</span><span class="sxs-lookup"><span data-stu-id="7b1b1-104">The objective of this tutorial is to show you the steps you need to perform in Concur and Azure AD to automatically provision and de-provision user accounts from Azure AD to Concur.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7b1b1-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7b1b1-105">Prerequisites</span></span>

<span data-ttu-id="7b1b1-106">Сценарий, описанный в этом учебнике, предполагает, что у вас уже имеется:</span><span class="sxs-lookup"><span data-stu-id="7b1b1-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="7b1b1-107">Клиент Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7b1b1-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="7b1b1-108">подписка Concur с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="7b1b1-108">A Concur single sign-on enabled subscription.</span></span>
*   <span data-ttu-id="7b1b1-109">Учетная запись пользователя в Concur с разрешениями администратора группы.</span><span class="sxs-lookup"><span data-stu-id="7b1b1-109">A user account in Concur with Team Admin permissions.</span></span>

## <a name="assigning-users-to-concur"></a><span data-ttu-id="7b1b1-110">Назначение пользователей в Concur</span><span class="sxs-lookup"><span data-stu-id="7b1b1-110">Assigning users to Concur</span></span>

<span data-ttu-id="7b1b1-111">В Azure Active Directory для определения того, какие пользователи должны получать доступ к выбранным приложениям, используется концепция, называемая "назначение".</span><span class="sxs-lookup"><span data-stu-id="7b1b1-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="7b1b1-112">В контексте автоматической подготовки учетной записи будут синхронизированы только те записи и группы, которые были "назначены" приложению в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7b1b1-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="7b1b1-113">Перед настройкой и включением службы подготовки необходимо решить, какие пользователи или группы в Azure AD представляют пользователей, которым требуется доступ к приложению Concur.</span><span class="sxs-lookup"><span data-stu-id="7b1b1-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Concur app.</span></span> <span data-ttu-id="7b1b1-114">Когда этот вопрос будет решен, можно назначить этих пользователей приложению Concur, следуя приведенным ниже указаниям:</span><span class="sxs-lookup"><span data-stu-id="7b1b1-114">Once decided, you can assign these users to your Concur app by following the instructions here:</span></span>

[<span data-ttu-id="7b1b1-115">Назначение корпоративному приложению пользователя или группы</span><span class="sxs-lookup"><span data-stu-id="7b1b1-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-concur"></a><span data-ttu-id="7b1b1-116">Важные рекомендации по назначению пользователей в Concur</span><span class="sxs-lookup"><span data-stu-id="7b1b1-116">Important tips for assigning users to Concur</span></span>

*   <span data-ttu-id="7b1b1-117">Рекомендуется назначить одного пользователя Azure AD в Concur для тестирования конфигурации подготовки.</span><span class="sxs-lookup"><span data-stu-id="7b1b1-117">It is recommended that a single Azure AD user be assigned to Concur to test the provisioning configuration.</span></span> <span data-ttu-id="7b1b1-118">Дополнительные пользователи и/или группы можно назначить позднее.</span><span class="sxs-lookup"><span data-stu-id="7b1b1-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="7b1b1-119">При назначении пользователя Concur необходимо выбрать допустимую роль пользователя.</span><span class="sxs-lookup"><span data-stu-id="7b1b1-119">When assigning a user to Concur, you must select a valid user role.</span></span> <span data-ttu-id="7b1b1-120">Роль "Доступ по умолчанию" не работает для подготовки.</span><span class="sxs-lookup"><span data-stu-id="7b1b1-120">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="7b1b1-121">Включение подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="7b1b1-121">Enable user provisioning</span></span>

<span data-ttu-id="7b1b1-122">В этом разделе описывается подключение к API подготовки учетной записи пользователя Azure AD в Concur и настройка подготовки службы для создания, обновления и отмены назначения учетных записей пользователей в Concur на основе назначения пользователей и групп в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7b1b1-122">This section guides you through connecting your Azure AD to Concur's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Concur based on user and group assignment in Azure AD.</span></span>

> [!Tip] 
> <span data-ttu-id="7b1b1-123">Для Concur также можно включить единый вход на базе управления лицензиями. Для этого следуйте инструкциям, указанным на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7b1b1-123">You may also choose to enabled SAML-based Single Sign-On for Concur, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="7b1b1-124">Единый вход можно настроить независимо от автоматической подготовки, хотя эти две возможности дополняют друг друга.</span><span class="sxs-lookup"><span data-stu-id="7b1b1-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-user-account-provisioning"></a><span data-ttu-id="7b1b1-125">Чтобы настроить подготовку учетных записей пользователей:</span><span class="sxs-lookup"><span data-stu-id="7b1b1-125">To configure user account provisioning:</span></span>

<span data-ttu-id="7b1b1-126">В этом разделе показано, как включить подготовку учетных записей пользователей Active Directory для Concur.</span><span class="sxs-lookup"><span data-stu-id="7b1b1-126">The objective of this section is to outline how to enable provisioning of Active Directory user accounts to Concur.</span></span>

<span data-ttu-id="7b1b1-127">Для включения приложений в Expense Service требуется должным образом организовать настройку и использование профиля администратора веб-служб.</span><span class="sxs-lookup"><span data-stu-id="7b1b1-127">To enable apps in the Expense Service, there has to be proper setup and use of a Web Service Admin profile.</span></span> <span data-ttu-id="7b1b1-128">Не добавляйте роль администратора веб-служб в имеющийся профиль администратора, используемый для выполнения административных функций T&E.</span><span class="sxs-lookup"><span data-stu-id="7b1b1-128">Don't add the WS Admin role to your existing administrator profile that you use for T&E administrative functions.</span></span>

<span data-ttu-id="7b1b1-129">Представителю Concur Consultants или администратору клиента следует создать отдельный профиль администратора веб-служб, и администратор клиента должен использовать этот профиль для выполнения функций администратора веб-служб (например, для включения приложений).</span><span class="sxs-lookup"><span data-stu-id="7b1b1-129">Concur Consultants or the client administrator must create a distinct Web Service Administrator profile and the Client administrator must use this profile for the Web Services Administrator functions (for example, enabling apps).</span></span> <span data-ttu-id="7b1b1-130">Эти профили должны храниться отдельно от профиля повседневных административных задач T&E администратора клиента (профилю администратора T&E не должна быть назначена роль WSAdmin).</span><span class="sxs-lookup"><span data-stu-id="7b1b1-130">These profiles must be kept separate from the client administrator's daily T&E admin profile (the T&E admin profile should not have the WSAdmin role assigned).</span></span>

<span data-ttu-id="7b1b1-131">При создании профиля, который будет использоваться для включения приложения, введите имя администратора клиента в полях профиля пользователя.</span><span class="sxs-lookup"><span data-stu-id="7b1b1-131">When you create the profile to be used for enabling the app, enter the client administrator's name into the user profile fields.</span></span> <span data-ttu-id="7b1b1-132">Таким образом профилю предоставляются права владения.</span><span class="sxs-lookup"><span data-stu-id="7b1b1-132">This assigns ownership to the profile.</span></span> <span data-ttu-id="7b1b1-133">После создания одного или нескольких профилей клиент должен войти в этот профиль, чтобы нажать кнопку *Включить* для партнерского приложения в меню веб-служб.</span><span class="sxs-lookup"><span data-stu-id="7b1b1-133">Once one or more profiles is created, the client must log in with this profile to click the "*Enable*" button for a Partner App within the Web Services menu.</span></span>

<span data-ttu-id="7b1b1-134">По следующим причинам это действие не следует выполнять для профиля, который используется для повседневного администрирования T&E.</span><span class="sxs-lookup"><span data-stu-id="7b1b1-134">For the following reasons, this action should not be done with the profile they use for normal T&E administration.</span></span>

* <span data-ttu-id="7b1b1-135">Именно клиент должен нажать кнопку*Да*в диалоговом окне, отображаемом после включения приложения.</span><span class="sxs-lookup"><span data-stu-id="7b1b1-135">The client has to be the one that clicks "*Yes*" on the dialogue window that is displayed after an app is enabled.</span></span> <span data-ttu-id="7b1b1-136">Нажимая эту кнопку, клиент дает согласие на то, чтобы партнерское приложение осуществляло доступ к его данным, поэтому ни вы, ни партнер не можете нажать эту кнопку.</span><span class="sxs-lookup"><span data-stu-id="7b1b1-136">This click acknowledges the client is willing for the Partner application to access their data, so you or the Partner cannot click that Yes button.</span></span>

* <span data-ttu-id="7b1b1-137">Если администратор клиента, который включил приложение с помощью профиля администратора T&E, увольняется из компании (в результате чего этот профиль деактивируется), все приложения, включенные с помощью данного профиля, не будут работать до их включения с помощью другого активного профиля администратора веб-служб.</span><span class="sxs-lookup"><span data-stu-id="7b1b1-137">If a client administrator that has enabled an app using the T&E admin profile leaves the company (resulting in the profile being inactivated), any apps enabled using that profile does not function until the app is enabled with another active WS Admin profile.</span></span> <span data-ttu-id="7b1b1-138">Именно поэтому так важно создавать отдельные профили администратора веб-служб.</span><span class="sxs-lookup"><span data-stu-id="7b1b1-138">This is why you are supposed to create distinct WS Admin profiles.</span></span>

* <span data-ttu-id="7b1b1-139">В случае увольнения администратора имя, связанное с профилем администратора веб-служб, можно изменить на имя замещающего администратора без негативных последствий для включенного приложения, так как деактивировать профиль при этом не требуется.</span><span class="sxs-lookup"><span data-stu-id="7b1b1-139">If an administrator leaves the company, the name associated to the WS Admin profile can be changed to the replacement administrator if desired without impacting the enabled app because that profile does not need inactivated.</span></span>

<span data-ttu-id="7b1b1-140">**Чтобы настроить подготовку учетных записей пользователей, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="7b1b1-140">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="7b1b1-141">Выполните вход в свой клиент **Concur**.</span><span class="sxs-lookup"><span data-stu-id="7b1b1-141">Log on to your **Concur** tenant.</span></span>

2. <span data-ttu-id="7b1b1-142">В меню **Administration** (Администрирование) выберите пункт **Web Services** (Веб-службы).</span><span class="sxs-lookup"><span data-stu-id="7b1b1-142">From the **Administration** menu, select **Web Services**.</span></span>
   
    <span data-ttu-id="7b1b1-143">![Клиент Concur](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Клиент Concur")</span><span class="sxs-lookup"><span data-stu-id="7b1b1-143">![Concur tenant](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Concur tenant")</span></span>

3. <span data-ttu-id="7b1b1-144">Слева от области **Web Services** (Веб-службы) выберите **Enable Partner Application** (Включить партнерское приложение).</span><span class="sxs-lookup"><span data-stu-id="7b1b1-144">On the left side, from the **Web Services** pane, select **Enable Partner Application**.</span></span>
   
    <span data-ttu-id="7b1b1-145">![Включение партнерского приложения](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "Включение партнерского приложения")</span><span class="sxs-lookup"><span data-stu-id="7b1b1-145">![Enable Partner Application](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "Enable Partner Application")</span></span>

4. <span data-ttu-id="7b1b1-146">В списке **Enable Application** (Включить приложение) выберите значение **Azure Active Directory**, а затем нажмите кнопку **Enable** (Включить).</span><span class="sxs-lookup"><span data-stu-id="7b1b1-146">From the **Enable Application** list, select **Azure Active Directory**, and then click **Enable**.</span></span>
   
    <span data-ttu-id="7b1b1-147">![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")</span><span class="sxs-lookup"><span data-stu-id="7b1b1-147">![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")</span></span>

5. <span data-ttu-id="7b1b1-148">Нажмите кнопку **Да**, чтобы закрыть диалоговое окно **Подтверждение действия**.</span><span class="sxs-lookup"><span data-stu-id="7b1b1-148">Click **Yes** to close the **Confirm Action** dialog.</span></span>
   
    <span data-ttu-id="7b1b1-149">![Подтверждение действия](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "Подтверждение действия")</span><span class="sxs-lookup"><span data-stu-id="7b1b1-149">![Confirm Action](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "Confirm Action")</span></span>

6. <span data-ttu-id="7b1b1-150">На [портале Azure](https://portal.azure.com) перейдите в раздел **Azure Active Directory > Корпоративные приложения > Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="7b1b1-150">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

7. <span data-ttu-id="7b1b1-151">Если в Concur уже настроен единый вход, найдите свой экземпляр Concur с помощью поля поиска.</span><span class="sxs-lookup"><span data-stu-id="7b1b1-151">If you have already configured Concur for single sign-on, search for your instance of Concur using the search field.</span></span> <span data-ttu-id="7b1b1-152">В противном случае щелкните **Добавить** и выполните поиск **Concur** в коллекции приложений.</span><span class="sxs-lookup"><span data-stu-id="7b1b1-152">Otherwise, select **Add** and search for **Concur** in the application gallery.</span></span> <span data-ttu-id="7b1b1-153">Выберите Concur в результатах поиска и добавьте его в список приложений.</span><span class="sxs-lookup"><span data-stu-id="7b1b1-153">Select Concur from the search results, and add it to your list of applications.</span></span>

8. <span data-ttu-id="7b1b1-154">Выберите экземпляр Concur, а затем перейдите на вкладку **Подготовка**.</span><span class="sxs-lookup"><span data-stu-id="7b1b1-154">Select your instance of Concur, then select the **Provisioning** tab.</span></span>

9. <span data-ttu-id="7b1b1-155">Для параметра **Режим подготовки к работе** выберите значение **Automatic** (Автоматически).</span><span class="sxs-lookup"><span data-stu-id="7b1b1-155">Set the **Provisioning Mode** to **Automatic**.</span></span> 
 
    ![подготовка](./media/active-directory-saas-concur-provisioning-tutorial/provisioning.png)

10. <span data-ttu-id="7b1b1-157">В разделе **Учетные данные администратора** введите **имя пользователя** и **пароль** вашего администратора Concur.</span><span class="sxs-lookup"><span data-stu-id="7b1b1-157">Under the **Admin Credentials** section, enter the **user name** and the **password** of your Concur administrator.</span></span>

11. <span data-ttu-id="7b1b1-158">На портале Azure щелкните **Проверить подключение**, чтобы убедиться, что Azure AD может подключиться к приложению Concur.</span><span class="sxs-lookup"><span data-stu-id="7b1b1-158">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Concur app.</span></span> <span data-ttu-id="7b1b1-159">При сбое соединения убедитесь, что ваша учетная запись Concur имеет разрешения администратора команды.</span><span class="sxs-lookup"><span data-stu-id="7b1b1-159">If the connection fails, ensure your Concur account has Team Admin permissions.</span></span>

12. <span data-ttu-id="7b1b1-160">В поле **Почтовое уведомление** введите адрес электронной почты пользователя или группы, которые должны получать уведомления об ошибках подготовки, а также установите флажок.</span><span class="sxs-lookup"><span data-stu-id="7b1b1-160">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

13. <span data-ttu-id="7b1b1-161">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="7b1b1-161">Click **Save.**</span></span>

14. <span data-ttu-id="7b1b1-162">В разделе сопоставления выберите **Synchronize Azure Active Directory Users to Concur** (Синхронизировать пользователей Azure Active Directory с Concur).</span><span class="sxs-lookup"><span data-stu-id="7b1b1-162">Under the Mappings section, select **Synchronize Azure Active Directory Users to Concur.**</span></span>

15. <span data-ttu-id="7b1b1-163">В разделе **Сопоставления атрибутов** просмотрите пользовательские атрибуты, которые синхронизированы из Azure AD в Concur.</span><span class="sxs-lookup"><span data-stu-id="7b1b1-163">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Concur.</span></span> <span data-ttu-id="7b1b1-164">Атрибуты, выбранные как свойства **сопоставления**, используются для сопоставления учетных записей пользователей в Concur для операций обновления.</span><span class="sxs-lookup"><span data-stu-id="7b1b1-164">The attributes selected as **Matching** properties are used to match the user accounts in Concur for update operations.</span></span> <span data-ttu-id="7b1b1-165">Нажмите кнопку "Сохранить", чтобы подтвердить все изменения.</span><span class="sxs-lookup"><span data-stu-id="7b1b1-165">Select the Save button to commit any changes.</span></span>

16. <span data-ttu-id="7b1b1-166">Чтобы включить службу подготовки Azure AD для Concur, измените значение параметра **Состояние подготовки** на **Включено** в разделе **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="7b1b1-166">To enable the Azure AD provisioning service for Concur, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

17. <span data-ttu-id="7b1b1-167">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="7b1b1-167">Click **Save.**</span></span>

<span data-ttu-id="7b1b1-168">Теперь можно создать тестовую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="7b1b1-168">You can now create a test account.</span></span> <span data-ttu-id="7b1b1-169">Подождите примерно 20 минут, чтобы убедиться, что учетная запись была синхронизирована с Concur.</span><span class="sxs-lookup"><span data-stu-id="7b1b1-169">Wait for up to 20 minutes to verify that the account has been synchronized to Concur.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7b1b1-170">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="7b1b1-170">Additional resources</span></span>

* [<span data-ttu-id="7b1b1-171">Управление подготовкой учетных записей пользователей для корпоративных приложений</span><span class="sxs-lookup"><span data-stu-id="7b1b1-171">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7b1b1-172">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7b1b1-172">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="7b1b1-173">Настройка единого входа</span><span class="sxs-lookup"><span data-stu-id="7b1b1-173">Configure Single Sign-on</span></span>](active-directory-saas-concur-tutorial.md)

