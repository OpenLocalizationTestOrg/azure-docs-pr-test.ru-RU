---
title: "Руководство по настройке GitHub для автоматической подготовки пользователей с помощью Azure Active Directory | Документация Майкрософт"
description: "Узнайте, как tooconfigure Azure Active Directory tooautomatically подготовки и Отмена подготовки учетных записей пользователей tooGitHub."
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
ms.openlocfilehash: c1f0f7a42e4f8a94db3f409cd463e13bb1bc13bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-github-for-automatic-user-provisioning"></a><span data-ttu-id="838ad-103">Руководство по настройке GitHub для автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="838ad-103">Tutorial: Configuring GitHub for Automatic User Provisioning</span></span>


<span data-ttu-id="838ad-104">Цель этого учебника Hello — hello действия, которые следует tooperform в GitHub и Azure AD tooautomatically подготовки и Отмена подготовки учетных записей пользователей из Azure AD tooGitHub tooshow.</span><span class="sxs-lookup"><span data-stu-id="838ad-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in GitHub and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooGitHub.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="838ad-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="838ad-105">Prerequisites</span></span>

<span data-ttu-id="838ad-106">Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="838ad-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="838ad-107">клиент Azure Active Directory;</span><span class="sxs-lookup"><span data-stu-id="838ad-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="838ad-108">Клиент Github с hello [бизнес-планом](https://help.github.com/articles/organization-billing-plans/#business-plan) или лучше включена</span><span class="sxs-lookup"><span data-stu-id="838ad-108">A Github tenant with hello [Business plan](https://help.github.com/articles/organization-billing-plans/#business-plan) or better enabled</span></span> 
*   <span data-ttu-id="838ad-109">учетная запись пользователя в GitHub с разрешениями администратора.</span><span class="sxs-lookup"><span data-stu-id="838ad-109">A user account in GitHub with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="838ad-110">Hello подготовки интеграции Azure AD использует hello [GitHub SCIM API](https://developer.github.com/v3/scim/), являющийся tooGithub доступные команды на бизнес-планом hello и более.</span><span class="sxs-lookup"><span data-stu-id="838ad-110">hello Azure AD provisioning integration relies on hello [GitHub SCIM API](https://developer.github.com/v3/scim/), which is available tooGithub teams on hello Business plan or better.</span></span>

## <a name="assigning-users-toogithub"></a><span data-ttu-id="838ad-111">Назначение пользователей tooGitHub</span><span class="sxs-lookup"><span data-stu-id="838ad-111">Assigning users tooGitHub</span></span>

<span data-ttu-id="838ad-112">Azure Active Directory использует называемый «назначения» toodetermine пользователей, которые должны получать доступ tooselected приложений.</span><span class="sxs-lookup"><span data-stu-id="838ad-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="838ad-113">В контексте hello автоматический подготовки пользователей. учетной записи синхронизируются только hello пользователей и групп, назначенных» «tooan приложения в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="838ad-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="838ad-114">Перед Настройка и включение hello подготовки службы, необходимо toodecide какие пользователи или группы в Azure AD представляют Привет пользователям требуется доступ к приложению tooyour GitHub.</span><span class="sxs-lookup"><span data-stu-id="838ad-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour GitHub app.</span></span> <span data-ttu-id="838ad-115">После приняла решение, можно назначить эти приложения пользователям tooyour GitHub в соответствии с инструкциями hello здесь:</span><span class="sxs-lookup"><span data-stu-id="838ad-115">Once decided, you can assign these users tooyour GitHub app by following hello instructions here:</span></span>

[<span data-ttu-id="838ad-116">Назначить пользователю или группе tooan корпоративного приложения</span><span class="sxs-lookup"><span data-stu-id="838ad-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toogithub"></a><span data-ttu-id="838ad-117">Важные советы для назначения пользователей tooGitHub</span><span class="sxs-lookup"><span data-stu-id="838ad-117">Important tips for assigning users tooGitHub</span></span>

*   <span data-ttu-id="838ad-118">Рекомендуется один назначенный hello tootest tooGitHub настройки подготовки пользователя Azure AD.</span><span class="sxs-lookup"><span data-stu-id="838ad-118">It is recommended that a single Azure AD user is assigned tooGitHub tootest hello provisioning configuration.</span></span> <span data-ttu-id="838ad-119">Дополнительные пользователи и/или группы можно назначить позднее.</span><span class="sxs-lookup"><span data-stu-id="838ad-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="838ad-120">При назначении tooGitHub пользователя, необходимо выбрать либо hello **пользователя** роли или другой допустимый конкретного приложения (если доступно) в диалоговом окне приветствия назначения.</span><span class="sxs-lookup"><span data-stu-id="838ad-120">When assigning a user tooGitHub, you must select either hello **User** role, or another valid application-specific role (if available) in hello assignment dialog.</span></span> <span data-ttu-id="838ad-121">Hello **доступа по умолчанию** роль не будет работать для подготовки, и эти пользователи будут пропускаться.</span><span class="sxs-lookup"><span data-stu-id="838ad-121">hello **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-toogithub"></a><span data-ttu-id="838ad-122">Настройка подготовки tooGitHub пользователей</span><span class="sxs-lookup"><span data-stu-id="838ad-122">Configuring user provisioning tooGitHub</span></span> 

<span data-ttu-id="838ad-123">Этот раздел поможет выполнить подключение учетной записи пользователя в Azure AD tooGitHub подготовки API и настройке подготовки службы toocreate hello, обновления и отключить учетные записи пользователей, назначенные в GitHub, в зависимости от назначения пользователей и групп в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="838ad-123">This section guides you through connecting your Azure AD tooGitHub's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in GitHub based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="838ad-124">Можно также выбрать tooenabled на основе SAML Single Sign-On для GitHub, следуя инструкциям hello в [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="838ad-124">You may also choose tooenabled SAML-based Single Sign-On for GitHub, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="838ad-125">Единый вход можно настроить независимо от автоматической подготовки, хотя эти две возможности дополняют друг друга.</span><span class="sxs-lookup"><span data-stu-id="838ad-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-toogithub-in-azure-ad"></a><span data-ttu-id="838ad-126">Настройка учетной записи автоматического пользователя подготовки tooGitHub в Azure AD</span><span class="sxs-lookup"><span data-stu-id="838ad-126">Configure automatic user account provisioning tooGitHub in Azure AD</span></span>


1. <span data-ttu-id="838ad-127">В hello [портал Azure](https://portal.azure.com), Обзор toohello **Azure Active Directory > корпоративных приложений > все приложения** раздела.</span><span class="sxs-lookup"><span data-stu-id="838ad-127">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="838ad-128">Если вы уже настроили GitHub для единого входа, поиск экземпляра с помощью поля поиска hello GitHub.</span><span class="sxs-lookup"><span data-stu-id="838ad-128">If you have already configured GitHub for single sign-on, search for your instance of GitHub using hello search field.</span></span> <span data-ttu-id="838ad-129">В противном случае выберите **добавить** и выполните поиск **GitHub** в галерее приложения hello.</span><span class="sxs-lookup"><span data-stu-id="838ad-129">Otherwise, select **Add** and search for **GitHub** in hello application gallery.</span></span> <span data-ttu-id="838ad-130">Выберите GitHub из результатов поиска hello и добавить его в список tooyour приложений.</span><span class="sxs-lookup"><span data-stu-id="838ad-130">Select GitHub from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="838ad-131">Выберите свой экземпляр GitHub, а затем выберите hello **Provisioning** вкладки.</span><span class="sxs-lookup"><span data-stu-id="838ad-131">Select your instance of GitHub, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="838ad-132">Набор hello **режим подготовки** слишком**автоматического**.</span><span class="sxs-lookup"><span data-stu-id="838ad-132">Set hello **Provisioning Mode** too**Automatic**.</span></span>

    ![Подготовка GitHub](./media/active-directory-saas-github-provisioning-tutorial/GitHub1.png)

5. <span data-ttu-id="838ad-134">В разделе hello **учетные данные администратора** щелкните **авторизовать**.</span><span class="sxs-lookup"><span data-stu-id="838ad-134">Under hello **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="838ad-135">В новом окне браузера откроется диалоговое окно авторизации GitHub.</span><span class="sxs-lookup"><span data-stu-id="838ad-135">This operation opens a GitHub authorization dialog in a new browser window.</span></span> 

6. <span data-ttu-id="838ad-136">В новом окне приветствия войдите в GitHub с помощью учетной записи администратора.</span><span class="sxs-lookup"><span data-stu-id="838ad-136">In hello new window, sign into GitHub using your Admin account.</span></span> <span data-ttu-id="838ad-137">В hello полученный авторизации диалоговом выберите hello tooenable инициализацию и затем выберите группу GitHub **авторизовать**.</span><span class="sxs-lookup"><span data-stu-id="838ad-137">In hello resulting authorization dialog, select hello GitHub team that you want tooenable provisioning for, and then select **Authorize**.</span></span> <span data-ttu-id="838ad-138">Hello Azure портала toocomplete после ее завершения, возвращаемый toohello настройки подготовки.</span><span class="sxs-lookup"><span data-stu-id="838ad-138">Once completed, return toohello Azure portal toocomplete hello provisioning configuration.</span></span>

    ![Диалоговое окно авторизации](./media/active-directory-saas-github-provisioning-tutorial/GitHub2.png)

7. <span data-ttu-id="838ad-140">В hello портал Azure, входной **URL-адрес клиента** и нажмите кнопку **проверить подключение** tooensure Azure AD можно подключить приложение tooyour GitHub.</span><span class="sxs-lookup"><span data-stu-id="838ad-140">In hello Azure portal, input **Tenant URL** and click **Test Connection** tooensure Azure AD can connect tooyour GitHub app.</span></span> <span data-ttu-id="838ad-141">При сбое подключения hello, убедитесь в вашей учетной записи GitHub имеет разрешения администратора и **URL-адрес клиента** введено правильно, а затем повторите hello, «Авторизовать» еще один шаг (могут составлять **URL-адрес клиента** правилом: «https : //api.github.com/scim/v2/organizations/ + < Organizations_name >», можно найти организации в рамках учетной записи GitHub: **параметры** > **организаций**).</span><span class="sxs-lookup"><span data-stu-id="838ad-141">If hello connection fails, ensure your GitHub account has Admin permissions and **Tenant URl** is inputted correctly, then try hello "Authorize" step again (you can constitute **Tenant URL** by rule: "https://api.github.com/scim/v2/organizations/ + <Organizations_name>", you can find your organizations under your GitHub account: **Settings** > **Organizations**).</span></span>

    ![Диалоговое окно авторизации](./media/active-directory-saas-github-provisioning-tutorial/GitHub3.png)

8. <span data-ttu-id="838ad-143">Введите адрес электронной почты hello пользователя или группы, которые должны получить уведомления о подготовке ошибки в hello **уведомление по электронной почте** поле и проверьте hello флажок «Отправить уведомление по электронной почте при возникновении сбоя».</span><span class="sxs-lookup"><span data-stu-id="838ad-143">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox "Send an email notification when a failure occurs."</span></span>

9. <span data-ttu-id="838ad-144">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="838ad-144">Click **Save**.</span></span> 

10. <span data-ttu-id="838ad-145">Установите hello сопоставлений **tooGitHub синхронизации Azure Active Directory — пользователи**.</span><span class="sxs-lookup"><span data-stu-id="838ad-145">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooGitHub**.</span></span>

11. <span data-ttu-id="838ad-146">В hello **сопоставления атрибутов** просмотрите hello атрибутов пользователей, которые синхронизируются из tooGitHub Azure AD.</span><span class="sxs-lookup"><span data-stu-id="838ad-146">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooGitHub.</span></span> <span data-ttu-id="838ad-147">Здравствуйте, атрибуты, выбранные в качестве **сопоставление** свойства, используемые toomatch hello учетные записи пользователей в GitHub для операции обновления.</span><span class="sxs-lookup"><span data-stu-id="838ad-147">hello attributes selected as **Matching** properties are used toomatch hello user accounts in GitHub for update operations.</span></span> <span data-ttu-id="838ad-148">Выберите toocommit кнопку hello сохранить все изменения.</span><span class="sxs-lookup"><span data-stu-id="838ad-148">Select hello Save button toocommit any changes.</span></span>

12. <span data-ttu-id="838ad-149">tooenable hello подготовки службы Azure AD для GitHub, изменение hello **состояние подготовки** слишком**на** в hello **параметры** раздела</span><span class="sxs-lookup"><span data-stu-id="838ad-149">tooenable hello Azure AD provisioning service for GitHub, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

13. <span data-ttu-id="838ad-150">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="838ad-150">Click **Save**.</span></span> 

<span data-ttu-id="838ad-151">Эта операция запускает hello первоначальной синхронизации все пользователи и группы, назначенные tooGitHub в hello пользователей и группы раздела.</span><span class="sxs-lookup"><span data-stu-id="838ad-151">This operation starts hello initial synchronization of any users and/or groups assigned tooGitHub in hello Users and Groups section.</span></span> <span data-ttu-id="838ad-152">Начальная синхронизация Hello принимает tooperform больше времени, чем последующие синхронизации, которые происходят примерно каждые 20 минут при условии, что запущена служба hello.</span><span class="sxs-lookup"><span data-stu-id="838ad-152">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="838ad-153">Можно использовать hello **сведения о синхронизации** статьи toomonitor хода выполнения и следуйте ссылки tooprovisioning отчеты о действиях, которые описывают все действия, выполняемые hello подготовки службы.</span><span class="sxs-lookup"><span data-stu-id="838ad-153">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service.</span></span>

<span data-ttu-id="838ad-154">Дополнительные сведения о способ подготовки tooread hello Azure AD использует для входа см. в разделе [отчеты о автоматический подготовки пользователей. учетной записи](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="838ad-154">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="838ad-155">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="838ad-155">Additional resources</span></span>

* [<span data-ttu-id="838ad-156">Управление подготовкой учетных записей пользователей для корпоративных приложений</span><span class="sxs-lookup"><span data-stu-id="838ad-156">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="838ad-157">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="838ad-157">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="838ad-158">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="838ad-158">Next steps</span></span>

* [<span data-ttu-id="838ad-159">Узнайте, каким образом ведет журнал tooreview и получать отчеты о действиях по подготовке</span><span class="sxs-lookup"><span data-stu-id="838ad-159">Learn how tooreview logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
