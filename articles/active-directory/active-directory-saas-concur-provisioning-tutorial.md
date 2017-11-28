---
title: "Учебник. Интеграция Azure Active Directory с Concur | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Concur."
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
ms.openlocfilehash: 13ba364af26a5ce0f1d2b51aaa0f84a4c353b107
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-concur-for-user-provisioning"></a><span data-ttu-id="48e47-103">Руководство по настройке Concur для подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="48e47-103">Tutorial: Configuring Concur for User Provisioning</span></span>

<span data-ttu-id="48e47-104">Цель этого учебника Hello — hello действия, которые следует tooperform в Concur и Azure AD tooautomatically подготовки и Отмена подготовки учетных записей пользователей из Azure AD tooConcur tooshow.</span><span class="sxs-lookup"><span data-stu-id="48e47-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Concur and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooConcur.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="48e47-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="48e47-105">Prerequisites</span></span>

<span data-ttu-id="48e47-106">Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="48e47-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="48e47-107">клиент Azure Active Directory;</span><span class="sxs-lookup"><span data-stu-id="48e47-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="48e47-108">подписка Concur с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="48e47-108">A Concur single sign-on enabled subscription.</span></span>
*   <span data-ttu-id="48e47-109">Учетная запись пользователя в Concur с разрешениями администратора группы.</span><span class="sxs-lookup"><span data-stu-id="48e47-109">A user account in Concur with Team Admin permissions.</span></span>

## <a name="assigning-users-tooconcur"></a><span data-ttu-id="48e47-110">Назначение пользователей tooConcur</span><span class="sxs-lookup"><span data-stu-id="48e47-110">Assigning users tooConcur</span></span>

<span data-ttu-id="48e47-111">Azure Active Directory использует называемый «назначения» toodetermine пользователей, которые должны получать доступ tooselected приложений.</span><span class="sxs-lookup"><span data-stu-id="48e47-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="48e47-112">В контексте hello автоматический подготовки пользователей. учетной записи синхронизируются только hello пользователей и групп, назначенных» «tooan приложения в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48e47-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="48e47-113">Перед Настройка и включение hello подготовки службы, необходимо toodecide какие пользователи или группы в Azure AD представляют Привет пользователям требуется доступ к приложению tooyour Concur.</span><span class="sxs-lookup"><span data-stu-id="48e47-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Concur app.</span></span> <span data-ttu-id="48e47-114">После приняла решение, можно назначить эти приложения пользователям tooyour Concur, следуя инструкциям hello:</span><span class="sxs-lookup"><span data-stu-id="48e47-114">Once decided, you can assign these users tooyour Concur app by following hello instructions here:</span></span>

[<span data-ttu-id="48e47-115">Назначить пользователю или группе tooan корпоративного приложения</span><span class="sxs-lookup"><span data-stu-id="48e47-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-tooconcur"></a><span data-ttu-id="48e47-116">Важные советы для назначения пользователей tooConcur</span><span class="sxs-lookup"><span data-stu-id="48e47-116">Important tips for assigning users tooConcur</span></span>

*   <span data-ttu-id="48e47-117">Рекомендуется один назначить hello tootest tooConcur настройки подготовки пользователя Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48e47-117">It is recommended that a single Azure AD user be assigned tooConcur tootest hello provisioning configuration.</span></span> <span data-ttu-id="48e47-118">Дополнительные пользователи и/или группы можно назначить позднее.</span><span class="sxs-lookup"><span data-stu-id="48e47-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="48e47-119">При назначении tooConcur пользователя, необходимо выбрать допустимой роли пользователя.</span><span class="sxs-lookup"><span data-stu-id="48e47-119">When assigning a user tooConcur, you must select a valid user role.</span></span> <span data-ttu-id="48e47-120">роль «Доступ по умолчанию» Hello не работает для подготовки.</span><span class="sxs-lookup"><span data-stu-id="48e47-120">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="48e47-121">Включение подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="48e47-121">Enable user provisioning</span></span>

<span data-ttu-id="48e47-122">Этот раздел поможет выполнить подключение учетной записи пользователя в Azure AD tooConcur подготовки API и настройке подготовки службы toocreate hello, обновления и отключить учетные записи пользователей, назначенные в Concur, в зависимости от назначения пользователей и групп в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48e47-122">This section guides you through connecting your Azure AD tooConcur's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Concur based on user and group assignment in Azure AD.</span></span>

> [!Tip] 
> <span data-ttu-id="48e47-123">Можно также выбрать tooenabled на основе SAML Single Sign-On для Concur, следуя инструкциям hello в [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="48e47-123">You may also choose tooenabled SAML-based Single Sign-On for Concur, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="48e47-124">Единый вход можно настроить независимо от автоматической подготовки, хотя эти две возможности дополняют друг друга.</span><span class="sxs-lookup"><span data-stu-id="48e47-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-user-account-provisioning"></a><span data-ttu-id="48e47-125">Подготовка учетной записи пользователя tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="48e47-125">tooconfigure user account provisioning:</span></span>

<span data-ttu-id="48e47-126">Цель этого раздела Hello является toooutline как tooenable Подготовка пользователя Active Directory учетных записей tooConcur.</span><span class="sxs-lookup"><span data-stu-id="48e47-126">hello objective of this section is toooutline how tooenable provisioning of Active Directory user accounts tooConcur.</span></span>

<span data-ttu-id="48e47-127">в приложения tooenable Здравствуйте службы расходов, должен toobe соответствующая настройка и использование профиля администратора веб-службы.</span><span class="sxs-lookup"><span data-stu-id="48e47-127">tooenable apps in hello Expense Service, there has toobe proper setup and use of a Web Service Admin profile.</span></span> <span data-ttu-id="48e47-128">Не добавляйте hello WS Admin роли tooyour существующий профиль администратора, используемой для T & E административных функций.</span><span class="sxs-lookup"><span data-stu-id="48e47-128">Don't add hello WS Admin role tooyour existing administrator profile that you use for T&E administrative functions.</span></span>

<span data-ttu-id="48e47-129">Консультантам concur или администратору клиента hello необходимо создать отдельные профиля администратора веб-службы и Здравствуйте, администратор клиента должен использовать этот профиль для функций hello администратора веб-службы (например, включение приложения).</span><span class="sxs-lookup"><span data-stu-id="48e47-129">Concur Consultants or hello client administrator must create a distinct Web Service Administrator profile and hello Client administrator must use this profile for hello Web Services Administrator functions (for example, enabling apps).</span></span> <span data-ttu-id="48e47-130">Эти профили должны быть отделены от администратора клиентов hello ежедневного T & E профиля администратора (hello T & E профиля администратора не следует hello назначенной роли WSAdmin).</span><span class="sxs-lookup"><span data-stu-id="48e47-130">These profiles must be kept separate from hello client administrator's daily T&E admin profile (hello T&E admin profile should not have hello WSAdmin role assigned).</span></span>

<span data-ttu-id="48e47-131">При создании профиля toobe hello, используется для включения приложение hello, введите имя администратора клиента hello в поля профиля пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="48e47-131">When you create hello profile toobe used for enabling hello app, enter hello client administrator's name into hello user profile fields.</span></span> <span data-ttu-id="48e47-132">Это назначает профиль toohello владения.</span><span class="sxs-lookup"><span data-stu-id="48e47-132">This assigns ownership toohello profile.</span></span> <span data-ttu-id="48e47-133">После создания одного или нескольких профилей hello клиент должен выполнить вход hello tooclick этот профиль «*включить*» кнопки для партнерского приложения в меню веб-служб hello.</span><span class="sxs-lookup"><span data-stu-id="48e47-133">Once one or more profiles is created, hello client must log in with this profile tooclick hello "*Enable*" button for a Partner App within hello Web Services menu.</span></span>

<span data-ttu-id="48e47-134">Для hello следующие причины это действие не должно выполняться с профилем hello, который используется для обычного администрирования T & E.</span><span class="sxs-lookup"><span data-stu-id="48e47-134">For hello following reasons, this action should not be done with hello profile they use for normal T&E administration.</span></span>

* <span data-ttu-id="48e47-135">Hello клиент имеет toobe hello, нажимает кнопку «*Да*» в диалоговом окне приветствия, которое отображается после включения приложения.</span><span class="sxs-lookup"><span data-stu-id="48e47-135">hello client has toobe hello one that clicks "*Yes*" on hello dialogue window that is displayed after an app is enabled.</span></span> <span data-ttu-id="48e47-136">Это нажатие означает, что клиент hello рассматривается для tooaccess приложения hello партнера свои данные, вы или партнер hello невозможно нажать кнопку, кнопку Да.</span><span class="sxs-lookup"><span data-stu-id="48e47-136">This click acknowledges hello client is willing for hello Partner application tooaccess their data, so you or hello Partner cannot click that Yes button.</span></span>

* <span data-ttu-id="48e47-137">Если администратор клиента, включил приложения с помощью hello T & E профиля администратора уходит из компании hello (приведет к hello профиль будет деактивирован), все приложения, включенные с использованием этого профиля недоступна, пока не приложение hello включен с другой active WS Admin профиль.</span><span class="sxs-lookup"><span data-stu-id="48e47-137">If a client administrator that has enabled an app using hello T&E admin profile leaves hello company (resulting in hello profile being inactivated), any apps enabled using that profile does not function until hello app is enabled with another active WS Admin profile.</span></span> <span data-ttu-id="48e47-138">Именно поэтому предполагаемого отдельные профили WS Admin toocreate.</span><span class="sxs-lookup"><span data-stu-id="48e47-138">This is why you are supposed toocreate distinct WS Admin profiles.</span></span>

* <span data-ttu-id="48e47-139">Если администратор покинет компанию hello, имя hello связан toohello профилем WS Admin могут быть измененные toohello замены администратору при необходимости без ущерба для hello включена, что приложение, поскольку этот профиль не требуется деактивировать.</span><span class="sxs-lookup"><span data-stu-id="48e47-139">If an administrator leaves hello company, hello name associated toohello WS Admin profile can be changed toohello replacement administrator if desired without impacting hello enabled app because that profile does not need inactivated.</span></span>

<span data-ttu-id="48e47-140">**tooconfigure подготовки пользователей, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="48e47-140">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="48e47-141">Войдите на tooyour **Concur** клиента.</span><span class="sxs-lookup"><span data-stu-id="48e47-141">Log on tooyour **Concur** tenant.</span></span>

2. <span data-ttu-id="48e47-142">Из hello **администрирования** последовательно выберите пункты **веб-службы**.</span><span class="sxs-lookup"><span data-stu-id="48e47-142">From hello **Administration** menu, select **Web Services**.</span></span>
   
    <span data-ttu-id="48e47-143">![Клиент Concur](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Клиент Concur")</span><span class="sxs-lookup"><span data-stu-id="48e47-143">![Concur tenant](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Concur tenant")</span></span>

3. <span data-ttu-id="48e47-144">На hello слева от hello **веб-службы** выберите **включить партнерское приложение**.</span><span class="sxs-lookup"><span data-stu-id="48e47-144">On hello left side, from hello **Web Services** pane, select **Enable Partner Application**.</span></span>
   
    <span data-ttu-id="48e47-145">![Включение партнерского приложения](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "Включение партнерского приложения")</span><span class="sxs-lookup"><span data-stu-id="48e47-145">![Enable Partner Application](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "Enable Partner Application")</span></span>

4. <span data-ttu-id="48e47-146">Из hello **включения приложений** выберите **Azure Active Directory**, а затем нажмите кнопку **включить**.</span><span class="sxs-lookup"><span data-stu-id="48e47-146">From hello **Enable Application** list, select **Azure Active Directory**, and then click **Enable**.</span></span>
   
    <span data-ttu-id="48e47-147">![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")</span><span class="sxs-lookup"><span data-stu-id="48e47-147">![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")</span></span>

5. <span data-ttu-id="48e47-148">Нажмите кнопку **Да** tooclose hello **подтверждение действия** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="48e47-148">Click **Yes** tooclose hello **Confirm Action** dialog.</span></span>
   
    <span data-ttu-id="48e47-149">![Подтверждение действия](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "Подтверждение действия")</span><span class="sxs-lookup"><span data-stu-id="48e47-149">![Confirm Action](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "Confirm Action")</span></span>

6. <span data-ttu-id="48e47-150">В hello [портал Azure](https://portal.azure.com), Обзор toohello **Azure Active Directory > корпоративных приложений > все приложения** раздела.</span><span class="sxs-lookup"><span data-stu-id="48e47-150">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

7. <span data-ttu-id="48e47-151">Если вы уже настроили Concur для единого входа, поиск экземпляра Concur, с помощью поля поиска hello.</span><span class="sxs-lookup"><span data-stu-id="48e47-151">If you have already configured Concur for single sign-on, search for your instance of Concur using hello search field.</span></span> <span data-ttu-id="48e47-152">В противном случае выберите **добавить** и выполните поиск **Concur** в галерее приложения hello.</span><span class="sxs-lookup"><span data-stu-id="48e47-152">Otherwise, select **Add** and search for **Concur** in hello application gallery.</span></span> <span data-ttu-id="48e47-153">Выберите Concur из результатов поиска hello и добавить его в список tooyour приложений.</span><span class="sxs-lookup"><span data-stu-id="48e47-153">Select Concur from hello search results, and add it tooyour list of applications.</span></span>

8. <span data-ttu-id="48e47-154">Выберите свой экземпляр Concur, а затем выберите hello **Provisioning** вкладки.</span><span class="sxs-lookup"><span data-stu-id="48e47-154">Select your instance of Concur, then select hello **Provisioning** tab.</span></span>

9. <span data-ttu-id="48e47-155">Набор hello **режим подготовки** слишком**автоматического**.</span><span class="sxs-lookup"><span data-stu-id="48e47-155">Set hello **Provisioning Mode** too**Automatic**.</span></span> 
 
    ![подготовка](./media/active-directory-saas-concur-provisioning-tutorial/provisioning.png)

10. <span data-ttu-id="48e47-157">В разделе hello **учетные данные администратора** введите hello **имя пользователя** и hello **пароль** администратора Concur.</span><span class="sxs-lookup"><span data-stu-id="48e47-157">Under hello **Admin Credentials** section, enter hello **user name** and hello **password** of your Concur administrator.</span></span>

11. <span data-ttu-id="48e47-158">В hello портал Azure, щелкните **проверить подключение** tooensure Azure AD можно подключить приложение tooyour Concur.</span><span class="sxs-lookup"><span data-stu-id="48e47-158">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Concur app.</span></span> <span data-ttu-id="48e47-159">При сбое подключения hello, убедитесь, что ваша учетная запись Concur имеет разрешения администратора команды.</span><span class="sxs-lookup"><span data-stu-id="48e47-159">If hello connection fails, ensure your Concur account has Team Admin permissions.</span></span>

12. <span data-ttu-id="48e47-160">Введите адрес электронной почты hello пользователя или группы, которые должны получить уведомления о подготовке ошибки в hello **уведомление по электронной почте** поле и установите флажок "hello".</span><span class="sxs-lookup"><span data-stu-id="48e47-160">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

13. <span data-ttu-id="48e47-161">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="48e47-161">Click **Save.**</span></span>

14. <span data-ttu-id="48e47-162">Установите hello сопоставлений **tooConcur синхронизации Azure Active Directory — пользователи.**</span><span class="sxs-lookup"><span data-stu-id="48e47-162">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooConcur.**</span></span>

15. <span data-ttu-id="48e47-163">В hello **сопоставления атрибутов** просмотрите hello атрибутов пользователей, которые синхронизируются из tooConcur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48e47-163">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooConcur.</span></span> <span data-ttu-id="48e47-164">Здравствуйте, атрибуты, выбранные в качестве **сопоставление** свойства, используемые toomatch hello учетных записей пользователей в Concur для операций обновления.</span><span class="sxs-lookup"><span data-stu-id="48e47-164">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Concur for update operations.</span></span> <span data-ttu-id="48e47-165">Выберите toocommit кнопку hello сохранить все изменения.</span><span class="sxs-lookup"><span data-stu-id="48e47-165">Select hello Save button toocommit any changes.</span></span>

16. <span data-ttu-id="48e47-166">tooenable hello подготовки службы Azure AD для Concur, изменение hello **состояние подготовки** слишком**на** в hello **параметры** раздела</span><span class="sxs-lookup"><span data-stu-id="48e47-166">tooenable hello Azure AD provisioning service for Concur, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

17. <span data-ttu-id="48e47-167">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="48e47-167">Click **Save.**</span></span>

<span data-ttu-id="48e47-168">Теперь можно создать тестовую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="48e47-168">You can now create a test account.</span></span> <span data-ttu-id="48e47-169">Дождитесь копирование минут too20 tooverify, hello учетная запись была синхронизирована tooConcur.</span><span class="sxs-lookup"><span data-stu-id="48e47-169">Wait for up too20 minutes tooverify that hello account has been synchronized tooConcur.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="48e47-170">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="48e47-170">Additional resources</span></span>

* [<span data-ttu-id="48e47-171">Управление подготовкой учетных записей пользователей для корпоративных приложений</span><span class="sxs-lookup"><span data-stu-id="48e47-171">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="48e47-172">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="48e47-172">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="48e47-173">Настройка единого входа</span><span class="sxs-lookup"><span data-stu-id="48e47-173">Configure Single Sign-on</span></span>](active-directory-saas-concur-tutorial.md)

