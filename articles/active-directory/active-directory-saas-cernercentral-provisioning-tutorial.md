---
title: "Руководство по настройке Cerner Central для автоматической подготовки пользователей с помощью Azure Active Directory | Документация Майкрософт"
description: "Узнайте, как Azure Active Directory tooautomatically tooconfigure подготовить список tooa пользователей в центральный Cerner."
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
ms.date: 05/26/2017
ms.author: asmalser-msft
ms.openlocfilehash: e96da98e783d24e7f34ae924824f909eead75f54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-cerner-central-for-automatic-user-provisioning"></a><span data-ttu-id="3778d-103">Руководство по настройке Cerner Central для автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="3778d-103">Tutorial: Configuring Cerner Central for Automatic User Provisioning</span></span>

<span data-ttu-id="3778d-104">Цель этого учебника Hello — hello действия, которые следует tooperform в центральный Cerner и Azure AD tooautomatically подготовки и Отмена подготовки учетных записей пользователей из списка пользователей Azure AD tooa в центральный Cerner tooshow.</span><span class="sxs-lookup"><span data-stu-id="3778d-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Cerner Central and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooa user roster in Cerner Central.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="3778d-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3778d-105">Prerequisites</span></span>

<span data-ttu-id="3778d-106">Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="3778d-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="3778d-107">Клиент Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3778d-107">An Azure Active Directory tenant</span></span>
*   <span data-ttu-id="3778d-108">Клиент Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="3778d-108">A Cerner Central tenant</span></span> 

> [!NOTE]
> <span data-ttu-id="3778d-109">Azure Active Directory интегрируется с с помощью hello центральный Cerner [SCIM](http://www.simplecloud.info/) протокола.</span><span class="sxs-lookup"><span data-stu-id="3778d-109">Azure Active Directory integrates with Cerner Central using hello [SCIM](http://www.simplecloud.info/) protocol.</span></span>

## <a name="assigning-users-toocerner-central"></a><span data-ttu-id="3778d-110">Назначение пользователей tooCerner центральный</span><span class="sxs-lookup"><span data-stu-id="3778d-110">Assigning users tooCerner Central</span></span>

<span data-ttu-id="3778d-111">Azure Active Directory использует называемый «назначения» toodetermine пользователей, которые должны получать доступ tooselected приложений.</span><span class="sxs-lookup"><span data-stu-id="3778d-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="3778d-112">В контексте hello автоматический подготовки пользователей. учетной записи синхронизируются только hello пользователей и групп, назначенных» «tooan приложения в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3778d-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD are synchronized.</span></span> 

<span data-ttu-id="3778d-113">Прежде чем настройка и включение hello подготовки службы, необходимо решить, какие пользователи или группы в Azure AD представляют Привет пользователей, которым требуется доступ tooCerner центральный.</span><span class="sxs-lookup"><span data-stu-id="3778d-113">Before configuring and enabling hello provisioning service, you should decide what users and/or groups in Azure AD represent hello users who need access tooCerner Central.</span></span> <span data-ttu-id="3778d-114">После приняла решение, можно назначить эти пользователи tooCerner центральный, следуя инструкциям hello:</span><span class="sxs-lookup"><span data-stu-id="3778d-114">Once decided, you can assign these users tooCerner Central by following hello instructions here:</span></span>

[<span data-ttu-id="3778d-115">Назначить пользователю или группе tooan корпоративного приложения</span><span class="sxs-lookup"><span data-stu-id="3778d-115">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toocerner-central"></a><span data-ttu-id="3778d-116">Важные советы для назначения пользователей tooCerner центральный</span><span class="sxs-lookup"><span data-stu-id="3778d-116">Important tips for assigning users tooCerner Central</span></span>

*   <span data-ttu-id="3778d-117">Рекомендуется один назначить hello центра tootest tooCerner настройки подготовки пользователя Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3778d-117">It is recommended that a single Azure AD user be assigned tooCerner Central tootest hello provisioning configuration.</span></span> <span data-ttu-id="3778d-118">Дополнительные пользователи и/или группы можно назначить позднее.</span><span class="sxs-lookup"><span data-stu-id="3778d-118">Additional users and/or groups may be assigned later.</span></span>

* <span data-ttu-id="3778d-119">По завершении первоначального тестирования для одного пользователя, центральный Cerner рекомендует назначение hello весь список пользователей предназначен tooaccess любой Cerner решения (не только центр Cerner) toobe подготовить tooCerner в список пользователя.</span><span class="sxs-lookup"><span data-stu-id="3778d-119">Once initial testing is complete for a single user, Cerner Central recommends assigning hello entire list of users intended tooaccess any Cerner solution (not just Cerner Central) toobe provisioned tooCerner’s user roster.</span></span>  <span data-ttu-id="3778d-120">Другие решения Cerner использовать этот список пользователей в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="3778d-120">Other Cerner solutions leverage this list of users in hello user roster.</span></span>

*   <span data-ttu-id="3778d-121">При присвоении пользователя tooCerner центральный, необходимо выбирать hello **пользователя** роли в диалоговом окне приветствия назначения.</span><span class="sxs-lookup"><span data-stu-id="3778d-121">When assigning a user tooCerner Central, you must select hello **User** role in hello assignment dialog.</span></span> <span data-ttu-id="3778d-122">Пользователи с ролью «Доступ по умолчанию» hello, исключаются из подготовки.</span><span class="sxs-lookup"><span data-stu-id="3778d-122">Users with hello "Default Access" role are excluded from provisioning.</span></span>


## <a name="configuring-user-provisioning-toocerner-central"></a><span data-ttu-id="3778d-123">Настройка подготовки tooCerner центральный пользователей</span><span class="sxs-lookup"><span data-stu-id="3778d-123">Configuring user provisioning tooCerner Central</span></span>

<span data-ttu-id="3778d-124">Этот раздел поможет выполнить подключение список пользователей центральный tooCerner Azure AD с помощью учетной записи пользователя Cerner SCIM подготовки API и настройке подготовки службы toocreate hello, обновления и отключить назначенный пользователь, на основе учетных записей в центральный Cerner для назначения пользователей и групп в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3778d-124">This section guides you through connecting your Azure AD tooCerner Central’s User Roster using Cerner's SCIM user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Cerner Central based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="3778d-125">Можно также выбрать tooenabled на основе SAML Single Sign-On для центрального Cerner, следуя hello следуйте инструкциям в [портал Azure (https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3778d-125">You may also choose tooenabled SAML-based Single Sign-On for Cerner Central, following hello instructions provided in [Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="3778d-126">Единый вход можно настроить независимо от автоматической подготовки, хотя две эти функции дополняют друг друга.</span><span class="sxs-lookup"><span data-stu-id="3778d-126">Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.</span></span> <span data-ttu-id="3778d-127">Дополнительные сведения см. в разделе hello [Cerner центральный единого входа учебника](active-directory-saas-cernercentral-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="3778d-127">For more information, see hello [Cerner Central single sign-on tutorial](active-directory-saas-cernercentral-tutorial.md).</span></span>


### <a name="tooconfigure-automatic-user-account-provisioning-toocerner-central-in-azure-ad"></a><span data-ttu-id="3778d-128">tooconfigure автоматическая учетная запись подготовки tooCerner центральный в Azure AD:</span><span class="sxs-lookup"><span data-stu-id="3778d-128">tooconfigure automatic user account provisioning tooCerner Central in Azure AD:</span></span>


<span data-ttu-id="3778d-129">В tooCerner учетных записей пользователя tooprovision порядок центральный вы требуется toorequest центральный Cerner системную учетную запись из Cerner, а также создания токена носителя OAuth, Azure AD можно использовать конечную точку SCIM tooconnect tooCerner.</span><span class="sxs-lookup"><span data-stu-id="3778d-129">In order tooprovision user accounts tooCerner Central, you’ll need toorequest a Cerner Central system account from Cerner, and generate an OAuth bearer token that Azure AD can use tooconnect tooCerner's SCIM endpoint.</span></span> <span data-ttu-id="3778d-130">Также рекомендуется выполнить интеграцию hello в изолированной среды Cerner перед развертыванием tooproduction.</span><span class="sxs-lookup"><span data-stu-id="3778d-130">It is also recommended that hello integration be performed in a Cerner sandbox environment before deploying tooproduction.</span></span>

1.  <span data-ttu-id="3778d-131">Hello первым шагом является управление hello Cerner людей hello tooensure и интеграция Azure AD учетная запись CernerCare, являющийся обязательным tooaccess hello документации необходимые toocomplete hello инструкции.</span><span class="sxs-lookup"><span data-stu-id="3778d-131">hello first step is tooensure hello people managing hello Cerner and Azure AD integration have a CernerCare account, which is required tooaccess hello documentation necessary toocomplete hello instructions.</span></span> <span data-ttu-id="3778d-132">При необходимости используйте URL-адреса hello ниже учетные записи CernerCare toocreate в каждой среде применимо.</span><span class="sxs-lookup"><span data-stu-id="3778d-132">If necessary, use hello URLs below toocreate CernerCare accounts in each applicable environment.</span></span>

   * <span data-ttu-id="3778d-133">Песочница: https://sandboxcernercare.com/accounts/create</span><span class="sxs-lookup"><span data-stu-id="3778d-133">Sandbox:  https://sandboxcernercare.com/accounts/create</span></span>

   * <span data-ttu-id="3778d-134">Производственная среда: https://cernercare.com/accounts/create</span><span class="sxs-lookup"><span data-stu-id="3778d-134">Production:  https://cernercare.com/accounts/create</span></span>  

2.  <span data-ttu-id="3778d-135">Далее создайте для Azure AD системную учетную запись.</span><span class="sxs-lookup"><span data-stu-id="3778d-135">Next, a system account must be created for Azure AD.</span></span> <span data-ttu-id="3778d-136">Используйте инструкции hello ниже toorequest системной учетной записи для "песочницы" и рабочей сред.</span><span class="sxs-lookup"><span data-stu-id="3778d-136">Use hello instructions below toorequest a System Account for your sandbox and production environments.</span></span>

   * <span data-ttu-id="3778d-137">Инструкции: https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account</span><span class="sxs-lookup"><span data-stu-id="3778d-137">Instructions:  https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account</span></span>

   * <span data-ttu-id="3778d-138">Песочница: https://sandboxcernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="3778d-138">Sandbox: https://sandboxcernercentral.com/system-accounts/</span></span>

   * <span data-ttu-id="3778d-139">Производственная среда: https://cernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="3778d-139">Production:  https://cernercentral.com/system-accounts/</span></span>

3.  <span data-ttu-id="3778d-140">Далее создайте токен носителя OAuth для каждой системной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="3778d-140">Next, generate an OAuth bearer token for each of your system accounts.</span></span> <span data-ttu-id="3778d-141">toodo это, выполните hello инструкциям ниже.</span><span class="sxs-lookup"><span data-stu-id="3778d-141">toodo this, follow hello instructions below.</span></span>

   * <span data-ttu-id="3778d-142">Инструкции: https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token</span><span class="sxs-lookup"><span data-stu-id="3778d-142">Instructions:  https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token</span></span>

   * <span data-ttu-id="3778d-143">Песочница: https://sandboxcernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="3778d-143">Sandbox: https://sandboxcernercentral.com/system-accounts/</span></span>

   * <span data-ttu-id="3778d-144">Производственная среда: https://cernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="3778d-144">Production:  https://cernercentral.com/system-accounts/</span></span>

4. <span data-ttu-id="3778d-145">Наконец вам нужно идентификаторы области списка tooacquire пользователей для обеих hello "песочницы" и рабочей сред в Cerner toocomplete hello конфигурации.</span><span class="sxs-lookup"><span data-stu-id="3778d-145">Finally, you need tooacquire User Roster Realm IDs for both hello sandbox and production environments in Cerner toocomplete hello configuration.</span></span> <span data-ttu-id="3778d-146">Сведения о том, как tooacquire, см.: https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM.</span><span class="sxs-lookup"><span data-stu-id="3778d-146">For information on how tooacquire this, see: https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM.</span></span> 

5. <span data-ttu-id="3778d-147">Теперь можно настроить tooCerner учетных записей пользователя tooprovision Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3778d-147">Now you can configure Azure AD tooprovision user accounts tooCerner.</span></span> <span data-ttu-id="3778d-148">Войдите в toohello [портал Azure](https://portal.azure.com)и найдите toohello **Azure Active Directory > корпоративных приложений > все приложения** раздела.</span><span class="sxs-lookup"><span data-stu-id="3778d-148">Sign in toohello [Azure portal](https://portal.azure.com), and browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

6. <span data-ttu-id="3778d-149">Если вы уже настроили центральный Cerner для единого входа, поиск экземпляра с помощью поля поиска hello центральный Cerner.</span><span class="sxs-lookup"><span data-stu-id="3778d-149">If you have already configured Cerner Central for single sign-on, search for your instance of Cerner Central using hello search field.</span></span> <span data-ttu-id="3778d-150">В противном случае выберите **добавить** и выполните поиск **Cerner центральный** в галерее приложения hello.</span><span class="sxs-lookup"><span data-stu-id="3778d-150">Otherwise, select **Add** and search for **Cerner Central** in hello application gallery.</span></span> <span data-ttu-id="3778d-151">Выберите центральный Cerner из результатов поиска hello и добавить его в список tooyour приложений.</span><span class="sxs-lookup"><span data-stu-id="3778d-151">Select Cerner Central from hello search results, and add it tooyour list of applications.</span></span>

7.  <span data-ttu-id="3778d-152">Выберите свой экземпляр центральный Cerner, а затем выберите hello **Provisioning** вкладки.</span><span class="sxs-lookup"><span data-stu-id="3778d-152">Select your instance of Cerner Central, then select hello **Provisioning** tab.</span></span>

8.  <span data-ttu-id="3778d-153">Набор hello **режим подготовки** слишком**автоматического**.</span><span class="sxs-lookup"><span data-stu-id="3778d-153">Set hello **Provisioning Mode** too**Automatic**.</span></span>

   ![Подготовка Cerner Central](./media/active-directory-saas-cernercentral-provisioning-tutorial/Cerner.PNG)

9.  <span data-ttu-id="3778d-155">Заполните следующие поля в группе hello **учетные данные администратора**:</span><span class="sxs-lookup"><span data-stu-id="3778d-155">Fill in hello following fields under **Admin Credentials**:</span></span>

   * <span data-ttu-id="3778d-156">В hello **URL-адрес клиента** введите URL-адрес в формате hello ниже, заменив «User-списка-область-ID» с Идентификатором hello сферы, полученного в шаге #4.</span><span class="sxs-lookup"><span data-stu-id="3778d-156">In hello **Tenant URL** field, enter a URL in hello format below, replacing "User-Roster-Realm-ID" with hello realm ID you acquired in step #4.</span></span>

> <span data-ttu-id="3778d-157">Песочница: https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span><span class="sxs-lookup"><span data-stu-id="3778d-157">Sandbox: https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span></span> 

> <span data-ttu-id="3778d-158">Рабочая среда: https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span><span class="sxs-lookup"><span data-stu-id="3778d-158">Production: https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span></span> 

   * <span data-ttu-id="3778d-159">В hello **секрет маркера** токена носителя OAuth hello, созданного на шаге #3 введите и нажмите кнопку **проверить подключение**.</span><span class="sxs-lookup"><span data-stu-id="3778d-159">In hello **Secret Token** field, enter hello OAuth bearer token you generated in step #3 and click **Test Connection**.</span></span>

   * <span data-ttu-id="3778d-160">Вы увидите уведомление об успехе hello upperright части портала.</span><span class="sxs-lookup"><span data-stu-id="3778d-160">You should see a success notification on hello upper­right side of your portal.</span></span>

10. <span data-ttu-id="3778d-161">Введите адрес электронной почты hello пользователя или группы, которые должны получить уведомления о подготовке ошибки в hello **уведомление по электронной почте** поле и установите флажок "hello" ниже.</span><span class="sxs-lookup"><span data-stu-id="3778d-161">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox below.</span></span>

11. <span data-ttu-id="3778d-162">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="3778d-162">Click **Save**.</span></span> 

12. <span data-ttu-id="3778d-163">В hello **сопоставления атрибутов** просмотрите пользователя hello и синхронизированы с Azure AD tooCerner центральный toobe атрибуты группы.</span><span class="sxs-lookup"><span data-stu-id="3778d-163">In hello **Attribute Mappings** section, review hello user and group attributes toobe synchronized from Azure AD tooCerner Central.</span></span> <span data-ttu-id="3778d-164">Здравствуйте, атрибуты, выбранные в качестве **сопоставление** свойства, используемые toomatch hello учетных записей и групп в центральный Cerner для операций обновления.</span><span class="sxs-lookup"><span data-stu-id="3778d-164">hello attributes selected as **Matching** properties are used toomatch hello user accounts and groups in Cerner Central for update operations.</span></span> <span data-ttu-id="3778d-165">Выберите toocommit кнопку hello сохранить все изменения.</span><span class="sxs-lookup"><span data-stu-id="3778d-165">Select hello Save button toocommit any changes.</span></span>

13. <span data-ttu-id="3778d-166">tooenable hello подготовки службы Azure AD для центрального Cerner, изменение hello **состояние подготовки** слишком**на** в hello **параметры** раздела</span><span class="sxs-lookup"><span data-stu-id="3778d-166">tooenable hello Azure AD provisioning service for Cerner Central, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

14. <span data-ttu-id="3778d-167">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="3778d-167">Click **Save**.</span></span> 

<span data-ttu-id="3778d-168">Запустится hello Первоначальная синхронизация всех пользователей и/или группам назначается tooCerner центральный в разделе hello пользователей и групп.</span><span class="sxs-lookup"><span data-stu-id="3778d-168">This starts hello initial synchronization of any users and/or groups assigned tooCerner Central in hello Users and Groups section.</span></span> <span data-ttu-id="3778d-169">Начальная синхронизация Hello принимает tooperform больше времени, чем последующие синхронизации, которые происходят примерно каждые 20 минут до тех пор, пока выполняется hello подготовки службы Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3778d-169">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello Azure AD provisioning service is running.</span></span> <span data-ttu-id="3778d-170">Можно использовать hello **сведения о синхронизации** статьи toomonitor хода выполнения и следуйте ссылки tooprovisioning отчеты о действиях, описывающих все действия, выполненные программой подготовки службы на центральный Cerner приложения hello.</span><span class="sxs-lookup"><span data-stu-id="3778d-170">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Cerner Central app.</span></span>

<span data-ttu-id="3778d-171">Дополнительные сведения о способ подготовки tooread hello Azure AD использует для входа см. в разделе [отчеты о автоматический подготовки пользователей. учетной записи](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="3778d-171">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3778d-172">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="3778d-172">Additional resources</span></span>

* [<span data-ttu-id="3778d-173">Cerner Central: публикация данных удостоверений с помощью Azure AD</span><span class="sxs-lookup"><span data-stu-id="3778d-173">Cerner Central: Publishing identity data using Azure AD</span></span>](https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+Azure+AD)
* [<span data-ttu-id="3778d-174">Руководство. Интеграция Azure Active Directory с Cerner Central</span><span class="sxs-lookup"><span data-stu-id="3778d-174">Tutorial: Configuring Cerner Central for single sign-on with Azure Active Directory</span></span>](active-directory-saas-cernercentral-tutorial.md)
* [<span data-ttu-id="3778d-175">Управление подготовкой учетных записей пользователей для корпоративных приложений</span><span class="sxs-lookup"><span data-stu-id="3778d-175">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="3778d-176">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3778d-176">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="3778d-177">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3778d-177">Next steps</span></span>
* <span data-ttu-id="3778d-178">[Узнайте, каким образом ведет журнал tooreview и get сообщает о действиях по подготовке](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="3778d-178">[Learn how tooreview logs and get reports on provisioning activity](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>
