---
title: "Руководство по настройке LinkedIn Learning для автоматической подготовки пользователей с помощью Azure Active Directory | Документация Майкрософт"
description: "Узнайте, как tooconfigure Azure Active Directory tooautomatically подготовки и Отмена подготовки учетных записей пользователей tooLinkedIn обучения."
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
ms.date: 04/15/2017
ms.author: asmalser-msft
ms.openlocfilehash: e0503e09ab384723ffb73d6ef1df8be6abfc9294
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-linkedin-learning-for-automatic-user-provisioning"></a><span data-ttu-id="1b3bf-103">Руководство по настройке LinkedIn Learning для автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="1b3bf-103">Tutorial: Configuring LinkedIn Learning for Automatic User Provisioning</span></span>


<span data-ttu-id="1b3bf-104">Hello цель этого учебника — tooshow hello действия, которые следует tooperform в обучении LinkedIn и Azure AD tooautomatically подготовки и Отмена подготовки учетных записей пользователей из Azure AD tooLinkedIn обучения.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in LinkedIn Learning and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooLinkedIn Learning.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="1b3bf-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1b3bf-105">Prerequisites</span></span>

<span data-ttu-id="1b3bf-106">Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="1b3bf-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="1b3bf-107">Клиент Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-107">An Azure Active Directory tenant</span></span>
*   <span data-ttu-id="1b3bf-108">Клиент LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-108">A LinkedIn Learning tenant</span></span> 
*   <span data-ttu-id="1b3bf-109">Учетной записи администратора в обучении LinkedIn с toohello доступа LinkedIn центр учетных записей</span><span class="sxs-lookup"><span data-stu-id="1b3bf-109">An administrator account in LinkedIn Learning with access toohello LinkedIn Account Center</span></span>

> [!NOTE]
> <span data-ttu-id="1b3bf-110">Azure Active Directory интегрируется с LinkedIn обучения с помощью hello [SCIM](http://www.simplecloud.info/) протокола.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-110">Azure Active Directory integrates with LinkedIn Learning using hello [SCIM](http://www.simplecloud.info/) protocol.</span></span>

## <a name="assigning-users-toolinkedin-learning"></a><span data-ttu-id="1b3bf-111">Назначение пользователей tooLinkedIn обучения</span><span class="sxs-lookup"><span data-stu-id="1b3bf-111">Assigning users tooLinkedIn Learning</span></span>

<span data-ttu-id="1b3bf-112">Azure Active Directory использует называемый «назначения» toodetermine пользователей, которые должны получать доступ tooselected приложений.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="1b3bf-113">В контексте hello автоматический подготовки пользователей. учетной записи будут синхронизированы только hello пользователей и групп, назначенных» «tooan приложения в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD will be synchronized.</span></span> 

<span data-ttu-id="1b3bf-114">Для настройки и включения hello подготовки службы, вам потребуется toodecide каких пользователей или группы в Azure AD представляют Привет пользователей, которым требуется доступ tooLinkedIn обучения.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-114">Before configuring and enabling hello provisioning service, you will need toodecide what users and/or groups in Azure AD represent hello users who need access tooLinkedIn Learning.</span></span> <span data-ttu-id="1b3bf-115">После приняла решение, можно назначить эти пользователи tooLinkedIn обучения в соответствии с инструкциями hello здесь:</span><span class="sxs-lookup"><span data-stu-id="1b3bf-115">Once decided, you can assign these users tooLinkedIn Learning by following hello instructions here:</span></span>

[<span data-ttu-id="1b3bf-116">Назначить пользователю или группе tooan корпоративного приложения</span><span class="sxs-lookup"><span data-stu-id="1b3bf-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toolinkedin-learning"></a><span data-ttu-id="1b3bf-117">Важные советы для назначения пользователей tooLinkedIn обучения</span><span class="sxs-lookup"><span data-stu-id="1b3bf-117">Important tips for assigning users tooLinkedIn Learning</span></span>

*   <span data-ttu-id="1b3bf-118">Рекомендуется один назначить tooLinkedIn обучения tootest hello настройки подготовки пользователя Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-118">It is recommended that a single Azure AD user be assigned tooLinkedIn Learning tootest hello provisioning configuration.</span></span> <span data-ttu-id="1b3bf-119">Дополнительные пользователи и/или группы можно назначить позднее.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="1b3bf-120">При назначении tooLinkedIn пользователя обучения, необходимо выбрать hello **пользователя** роли в диалоговом окне приветствия назначения.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-120">When assigning a user tooLinkedIn Learning, you must select hello **User** role in hello assignment dialog.</span></span> <span data-ttu-id="1b3bf-121">роль «Доступ по умолчанию» Hello не работает для подготовки.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-121">hello "Default Access" role does not work for provisioning.</span></span>


## <a name="configuring-user-provisioning-toolinkedin-learning"></a><span data-ttu-id="1b3bf-122">Настройка подготовки tooLinkedIn пользователей обучения</span><span class="sxs-lookup"><span data-stu-id="1b3bf-122">Configuring user provisioning tooLinkedIn Learning</span></span>

<span data-ttu-id="1b3bf-123">Этот раздел поможет выполнить подключение учетной записи пользователя SCIM обучения tooLinkedIn Azure AD API подготовки и настройки подготовки службы toocreate hello, обновления и отключить учетные записи пользователей, назначенные в LinkedIn обучения на основе пользователя и группы Назначение в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-123">This section guides you through connecting your Azure AD tooLinkedIn Learning's SCIM user account provisioning API, and configuring hello provisioning service toocreate, update and disable assigned user accounts in LinkedIn Learning based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="1b3bf-124">Можно также выбрать tooenabled на основе SAML Single Sign-On для обучения LinkedIn, следуя инструкциям hello в [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1b3bf-124">You may also choose tooenabled SAML-based Single Sign-On for LinkedIn Learning, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="1b3bf-125">Единый вход можно настроить независимо от автоматической подготовки, хотя две эти функции дополняют друг друга.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-125">Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.</span></span>


### <a name="tooconfigure-automatic-user-account-provisioning-toolinkedin-learning-in-azure-ad"></a><span data-ttu-id="1b3bf-126">tooconfigure автоматической учетной подготовки tooLinkedIn обучения в Azure AD:</span><span class="sxs-lookup"><span data-stu-id="1b3bf-126">tooconfigure automatic user account provisioning tooLinkedIn Learning in Azure AD:</span></span>


<span data-ttu-id="1b3bf-127">Hello первым шагом является tooretrieve LinkedIn маркер доступа.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-127">hello first step is tooretrieve your LinkedIn access token.</span></span> <span data-ttu-id="1b3bf-128">Если вы являетесь администратором предприятия, то можете самостоятельно подготовить токен доступа.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-128">If you are an Enterprise administrator, you can self-provision an access token.</span></span> <span data-ttu-id="1b3bf-129">В ваш центр учетной записи перейдите слишком**параметры &gt; глобальные параметры** и откройте hello **SCIM установки** панель.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-129">In your account center, go too**Settings &gt; Global Settings** and open hello **SCIM Setup** panel.</span></span>

> [!NOTE]
> <span data-ttu-id="1b3bf-130">При доступе к центру учетных записей hello напрямую, а не через ссылку, может получить доступ с помощью hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-130">If you are accessing hello account center directly rather than through a link, you can reach it using hello following steps.</span></span>

1)  <span data-ttu-id="1b3bf-131">Войдите в центр tooAccount.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-131">Sign in tooAccount Center.</span></span>

2)  <span data-ttu-id="1b3bf-132">Выберите **Администратор &gt; Параметры администратора**.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-132">Select **Admin &gt; Admin Settings** .</span></span>

3)  <span data-ttu-id="1b3bf-133">Нажмите кнопку **Advanced интеграций** на hello левой боковой панели.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-133">Click **Advanced Integrations** on hello left sidebar.</span></span> <span data-ttu-id="1b3bf-134">Вы являетесь направленной toohello центр учетных записей.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-134">You are directed toohello account center.</span></span>

4)  <span data-ttu-id="1b3bf-135">Нажмите кнопку **+ добавить новую конфигурацию SCIM** и выполните процедуру hello, заполнив каждого поля.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-135">Click **+ Add new SCIM configuration** and follow hello procedure by filling in each field.</span></span>

> <span data-ttu-id="1b3bf-136">Если автоматическое назначение лицензии отключено, синхронизируются только данные пользователя.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-136">When auto­assign licenses is not enabled, it means that only user data is synced.</span></span>

![Подготовка LinkedIn Learning](./media/active-directory-saas-linkedinlearning-provisioning-tutorial/linkedin_1.PNG)

> <span data-ttu-id="1b3bf-138">При включении назначения autolicense требуется toonote экземпляр приложения и типа лицензии.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-138">When auto­license assignment is enabled, you need toonote the application instance and license type.</span></span> <span data-ttu-id="1b3bf-139">По мере назначения лицензий, сначала служат основой пока взяты все лицензии hello.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-139">Licenses are assigned on a first come, first serve basis until all hello licenses are taken.</span></span>

![Подготовка LinkedIn Learning](./media/active-directory-saas-linkedinlearning-provisioning-tutorial/linkedin_2.PNG)

5)  <span data-ttu-id="1b3bf-141">Щелкните **Создать токен**.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-141">Click **Generate token**.</span></span> <span data-ttu-id="1b3bf-142">Вы увидите экрана маркера доступа в разделе hello **маркер доступа** поля.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-142">You should see your access token display under hello **Access token** field.</span></span>

6)  <span data-ttu-id="1b3bf-143">Сохраните буфер обмена tooyour токена доступа или компьютер перед выходом из страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-143">Save your access token tooyour clipboard or computer before leaving hello page.</span></span>

7) <span data-ttu-id="1b3bf-144">Затем войдите в toohello [портал Azure](https://portal.azure.com)и найдите toohello **Azure Active Directory > корпоративных приложений > все приложения** раздела.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-144">Next, sign in toohello [Azure portal](https://portal.azure.com), and browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

8) <span data-ttu-id="1b3bf-145">Если вы уже настроили LinkedIn обучения для единого входа, поиск экземпляра LinkedIn обучения с помощью поля поиска hello.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-145">If you have already configured LinkedIn Learning for single sign-on, search for your instance of LinkedIn Learning using hello search field.</span></span> <span data-ttu-id="1b3bf-146">В противном случае выберите **добавить** и выполните поиск **обучения LinkedIn** в галерее приложения hello.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-146">Otherwise, select **Add** and search for **LinkedIn Learning** in hello application gallery.</span></span> <span data-ttu-id="1b3bf-147">Выберите LinkedIn обучения из результатов поиска hello и добавить его в список tooyour приложений.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-147">Select LinkedIn Learning from hello search results, and add it tooyour list of applications.</span></span>

9)  <span data-ttu-id="1b3bf-148">Выберите свой экземпляр LinkedIn обучения, а затем выберите hello **Provisioning** вкладки.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-148">Select your instance of LinkedIn Learning, then select hello **Provisioning** tab.</span></span>

10) <span data-ttu-id="1b3bf-149">Набор hello **режим подготовки** слишком**автоматического**.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-149">Set hello **Provisioning Mode** too**Automatic**.</span></span>

![Подготовка LinkedIn Learning](./media/active-directory-saas-linkedinlearning-provisioning-tutorial/linkedin_3.PNG)

11)  <span data-ttu-id="1b3bf-151">Заполните следующие поля в группе hello **учетные данные администратора** :</span><span class="sxs-lookup"><span data-stu-id="1b3bf-151">Fill in hello following fields under **Admin Credentials** :</span></span>

* <span data-ttu-id="1b3bf-152">В hello **URL-адрес клиента** введите https://api.linkedin.com.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-152">In hello **Tenant URL** field, enter https://api.linkedin.com.</span></span>

* <span data-ttu-id="1b3bf-153">В hello **секрет маркера** введите hello маркер доступа, созданный на шаге 1 и нажмите кнопку **проверить подключение** .</span><span class="sxs-lookup"><span data-stu-id="1b3bf-153">In hello **Secret Token** field, enter hello access token you generated in step 1 and click **Test Connection** .</span></span>

* <span data-ttu-id="1b3bf-154">Вы увидите уведомление об успехе hello upperright части портала.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-154">You should see a success notification on hello upper­right side of   your portal.</span></span>

12) <span data-ttu-id="1b3bf-155">Введите адрес электронной почты hello пользователя или группы, которые должны получить уведомления о подготовке ошибки в hello **уведомление по электронной почте** поле и установите флажок "hello" ниже.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-155">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox below.</span></span>

13) <span data-ttu-id="1b3bf-156">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-156">Click **Save**.</span></span> 

14) <span data-ttu-id="1b3bf-157">В hello **сопоставления атрибутов** просмотрите hello атрибуты пользователя и группы, которые будут синхронизированы с Azure AD tooLinkedIn обучения.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-157">In hello **Attribute Mappings** section, review hello user and group attributes that will be synchronized from Azure AD tooLinkedIn Learning.</span></span> <span data-ttu-id="1b3bf-158">Обратите внимание, что атрибуты, выбранные в качестве hello **сопоставление** свойства будут использоваться toomatch hello учетных записей и групп в обучении LinkedIn для операций обновления.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-158">Note that hello attributes selected as **Matching** properties will be used toomatch hello user accounts and groups in LinkedIn Learning for update operations.</span></span> <span data-ttu-id="1b3bf-159">Выберите toocommit кнопку hello сохранить все изменения.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-159">Select hello Save button toocommit any changes.</span></span>

![Подготовка LinkedIn Learning](./media/active-directory-saas-linkedinlearning-provisioning-tutorial/linkedin_4.PNG)

15) <span data-ttu-id="1b3bf-161">tooenable hello подготовки службы Azure AD для обучения LinkedIn, изменение hello **состояние подготовки** слишком**на** в hello **параметры** раздела</span><span class="sxs-lookup"><span data-stu-id="1b3bf-161">tooenable hello Azure AD provisioning service for LinkedIn Learning, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

16) <span data-ttu-id="1b3bf-162">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-162">Click **Save**.</span></span> 

<span data-ttu-id="1b3bf-163">Это приведет к запуску hello Первоначальная синхронизация всех пользователей и/или группам назначается tooLinkedIn обучения в разделе hello пользователей и групп.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-163">This will start hello initial synchronization of any users and/or groups assigned tooLinkedIn Learning in hello Users and Groups section.</span></span> <span data-ttu-id="1b3bf-164">Обратите внимание, что hello начальной синхронизации будет иметь tooperform больше времени, чем последующие синхронизации, которые происходят примерно каждые 20 минут при условии, что запущена служба hello.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-164">Note that hello initial sync will take longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="1b3bf-165">Можно использовать hello **сведения о синхронизации** статьи toomonitor хода выполнения и следуйте ссылки tooprovisioning отчеты о действиях, описывающих все действия, выполняемые hello подготовки службы в приложении LinkedIn обучения.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-165">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your LinkedIn Learning app.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="1b3bf-166">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="1b3bf-166">Additional Resources</span></span>

* [<span data-ttu-id="1b3bf-167">Управление подготовкой учетных записей пользователей для корпоративных приложений</span><span class="sxs-lookup"><span data-stu-id="1b3bf-167">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="1b3bf-168">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1b3bf-168">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
