---
title: "Руководство по настройке Cerner Central для автоматической подготовки пользователей с помощью Azure Active Directory | Документация Майкрософт"
description: "Узнайте, как настроить Azure Active Directory для автоматической подготовки пользователей и их добавления в список в Cerner Central."
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
ms.openlocfilehash: 84613b7f8d7bd031d492a62da0bc53be96ac45a3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-configuring-cerner-central-for-automatic-user-provisioning"></a><span data-ttu-id="c9445-103">Руководство по настройке Cerner Central для автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="c9445-103">Tutorial: Configuring Cerner Central for Automatic User Provisioning</span></span>

<span data-ttu-id="c9445-104">Цель этого руководства — показать, как настроить автоматическую подготовку и отзыв учетных записей пользователей Azure AD в списке пользователей в Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="c9445-104">The objective of this tutorial is to show you the steps you need to perform in Cerner Central and Azure AD to automatically provision and de-provision user accounts from Azure AD to a user roster in Cerner Central.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="c9445-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c9445-105">Prerequisites</span></span>

<span data-ttu-id="c9445-106">Сценарий, описанный в этом учебнике, предполагает, что у вас уже имеется:</span><span class="sxs-lookup"><span data-stu-id="c9445-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="c9445-107">Клиент Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c9445-107">An Azure Active Directory tenant</span></span>
*   <span data-ttu-id="c9445-108">Клиент Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="c9445-108">A Cerner Central tenant</span></span> 

> [!NOTE]
> <span data-ttu-id="c9445-109">Для интеграции Azure Active Directory с Cerner Central используется протокол [SCIM](http://www.simplecloud.info/).</span><span class="sxs-lookup"><span data-stu-id="c9445-109">Azure Active Directory integrates with Cerner Central using the [SCIM](http://www.simplecloud.info/) protocol.</span></span>

## <a name="assigning-users-to-cerner-central"></a><span data-ttu-id="c9445-110">Добавление пользователей в Cerner Central</span><span class="sxs-lookup"><span data-stu-id="c9445-110">Assigning users to Cerner Central</span></span>

<span data-ttu-id="c9445-111">В Azure Active Directory для определения того, какие пользователи должны получать доступ к выбранным приложениям, используется концепция, называемая "назначение".</span><span class="sxs-lookup"><span data-stu-id="c9445-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="c9445-112">В контексте автоматической подготовки учетной записи синхронизированы будут только те пользователи и группы, которые были "назначены" приложению в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c9445-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD are synchronized.</span></span> 

<span data-ttu-id="c9445-113">Перед настройкой и включением службы подготовки необходимо решить, какие пользователи и (или) группы в Azure AD представляют пользователей, которым нужен доступ к Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="c9445-113">Before configuring and enabling the provisioning service, you should decide what users and/or groups in Azure AD represent the users who need access to Cerner Central.</span></span> <span data-ttu-id="c9445-114">Когда этот вопрос будет решен, этих пользователей можно будет назначить приложению Cerner Central, следуя приведенным ниже указаниям.</span><span class="sxs-lookup"><span data-stu-id="c9445-114">Once decided, you can assign these users to Cerner Central by following the instructions here:</span></span>

[<span data-ttu-id="c9445-115">Назначение корпоративному приложению пользователя или группы</span><span class="sxs-lookup"><span data-stu-id="c9445-115">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-cerner-central"></a><span data-ttu-id="c9445-116">Важные рекомендации по назначению пользователей приложению Cerner Central</span><span class="sxs-lookup"><span data-stu-id="c9445-116">Important tips for assigning users to Cerner Central</span></span>

*   <span data-ttu-id="c9445-117">Рекомендуем сначала назначить приложению Cerner Central одного пользователя Azure AD и с его помощью протестировать конфигурацию подготовки.</span><span class="sxs-lookup"><span data-stu-id="c9445-117">It is recommended that a single Azure AD user be assigned to Cerner Central to test the provisioning configuration.</span></span> <span data-ttu-id="c9445-118">Дополнительные пользователи и/или группы можно назначить позднее.</span><span class="sxs-lookup"><span data-stu-id="c9445-118">Additional users and/or groups may be assigned later.</span></span>

* <span data-ttu-id="c9445-119">По завершении первоначального тестирования отдельного пользователя Cerner Central порекомендует назначить целый список пользователей для доступа к любому решению Cerner (не только Cerner Central), которых следует подготовить и добавить в список пользователей Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="c9445-119">Once initial testing is complete for a single user, Cerner Central recommends assigning the entire list of users intended to access any Cerner solution (not just Cerner Central) to be provisioned to Cerner’s user roster.</span></span>  <span data-ttu-id="c9445-120">Другие решения Cerner используют этот перечень пользователей из списка пользователей.</span><span class="sxs-lookup"><span data-stu-id="c9445-120">Other Cerner solutions leverage this list of users in the user roster.</span></span>

*   <span data-ttu-id="c9445-121">Назначая пользователя приложению Cerner Central, в диалоговом окне назначения необходимо выбрать роль **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="c9445-121">When assigning a user to Cerner Central, you must select the **User** role in the assignment dialog.</span></span> <span data-ttu-id="c9445-122">Пользователи с ролью "Default Access" исключаются из подготовки.</span><span class="sxs-lookup"><span data-stu-id="c9445-122">Users with the "Default Access" role are excluded from provisioning.</span></span>


## <a name="configuring-user-provisioning-to-cerner-central"></a><span data-ttu-id="c9445-123">Настройка подготовки пользователей в Cerner Central</span><span class="sxs-lookup"><span data-stu-id="c9445-123">Configuring user provisioning to Cerner Central</span></span>

<span data-ttu-id="c9445-124">В этом разделе мы подключим Azure AD к списку пользователей Cerner Central с помощью API подготовки учетных записей Cerner (через протокол SCIM), а также настроим службу подготовки для создания, изменения и отключения назначенных учетных записей пользователей в Cerner Central на основе назначения пользователей и групп в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c9445-124">This section guides you through connecting your Azure AD to Cerner Central’s User Roster using Cerner's SCIM user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Cerner Central based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="c9445-125">Для Cerner Central также можно включить единый вход на основе SAML. Для этого следуйте инструкциям, указанным на [портале Azure(https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c9445-125">You may also choose to enabled SAML-based Single Sign-On for Cerner Central, following the instructions provided in [Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="c9445-126">Единый вход можно настроить независимо от автоматической подготовки, хотя две эти функции дополняют друг друга.</span><span class="sxs-lookup"><span data-stu-id="c9445-126">Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.</span></span> <span data-ttu-id="c9445-127">Дополнительные сведения см. в [руководстве по настройке единого входа в Cerner Central](active-directory-saas-cernercentral-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="c9445-127">For more information, see the [Cerner Central single sign-on tutorial](active-directory-saas-cernercentral-tutorial.md).</span></span>


### <a name="to-configure-automatic-user-account-provisioning-to-cerner-central-in-azure-ad"></a><span data-ttu-id="c9445-128">Настройка автоматической подготовки учетных записей пользователей Azure AD в Cerner Central</span><span class="sxs-lookup"><span data-stu-id="c9445-128">To configure automatic user account provisioning to Cerner Central in Azure AD:</span></span>


<span data-ttu-id="c9445-129">Для подготовки учетных записей пользователей в Cerner Central потребуется запросить у Cerner системную учетную запись Cerner Central и создать токен носителя OAuth, который Azure AD сможет использовать для подключения к конечной точке SCIM Cerner.</span><span class="sxs-lookup"><span data-stu-id="c9445-129">In order to provision user accounts to Cerner Central, you’ll need to request a Cerner Central system account from Cerner, and generate an OAuth bearer token that Azure AD can use to connect to Cerner's SCIM endpoint.</span></span> <span data-ttu-id="c9445-130">Также перед развертыванием в рабочей среде рекомендуется выполнить интеграцию в песочнице Cerner.</span><span class="sxs-lookup"><span data-stu-id="c9445-130">It is also recommended that the integration be performed in a Cerner sandbox environment before deploying to production.</span></span>

1.  <span data-ttu-id="c9445-131">Сначала убедитесь, что у пользователей, управляющих интеграцией Cerner и Azure AD, есть учетная запись CernerCare. Она требуется для доступа к документации, необходимой для выполнения инструкций.</span><span class="sxs-lookup"><span data-stu-id="c9445-131">The first step is to ensure the people managing the Cerner and Azure AD integration have a CernerCare account, which is required to access the documentation necessary to complete the instructions.</span></span> <span data-ttu-id="c9445-132">При необходимости воспользуйтесь указанным ниже URL-адресом, чтобы создавать учетные записи CernerCare в любой применимой среде.</span><span class="sxs-lookup"><span data-stu-id="c9445-132">If necessary, use the URLs below to create CernerCare accounts in each applicable environment.</span></span>

   * <span data-ttu-id="c9445-133">Песочница: https://sandboxcernercare.com/accounts/create</span><span class="sxs-lookup"><span data-stu-id="c9445-133">Sandbox:  https://sandboxcernercare.com/accounts/create</span></span>

   * <span data-ttu-id="c9445-134">Производственная среда: https://cernercare.com/accounts/create</span><span class="sxs-lookup"><span data-stu-id="c9445-134">Production:  https://cernercare.com/accounts/create</span></span>  

2.  <span data-ttu-id="c9445-135">Далее создайте для Azure AD системную учетную запись.</span><span class="sxs-lookup"><span data-stu-id="c9445-135">Next, a system account must be created for Azure AD.</span></span> <span data-ttu-id="c9445-136">Выполните инструкции ниже, чтобы отправить запрос на получение системной учетной записи для песочницы и рабочей среды.</span><span class="sxs-lookup"><span data-stu-id="c9445-136">Use the instructions below to request a System Account for your sandbox and production environments.</span></span>

   * <span data-ttu-id="c9445-137">Инструкции: https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account</span><span class="sxs-lookup"><span data-stu-id="c9445-137">Instructions:  https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account</span></span>

   * <span data-ttu-id="c9445-138">Песочница: https://sandboxcernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="c9445-138">Sandbox: https://sandboxcernercentral.com/system-accounts/</span></span>

   * <span data-ttu-id="c9445-139">Производственная среда: https://cernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="c9445-139">Production:  https://cernercentral.com/system-accounts/</span></span>

3.  <span data-ttu-id="c9445-140">Далее создайте токен носителя OAuth для каждой системной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="c9445-140">Next, generate an OAuth bearer token for each of your system accounts.</span></span> <span data-ttu-id="c9445-141">Для этого выполните приведенные ниже инструкции.</span><span class="sxs-lookup"><span data-stu-id="c9445-141">To do this, follow the instructions below.</span></span>

   * <span data-ttu-id="c9445-142">Инструкции: https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token</span><span class="sxs-lookup"><span data-stu-id="c9445-142">Instructions:  https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token</span></span>

   * <span data-ttu-id="c9445-143">Песочница: https://sandboxcernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="c9445-143">Sandbox: https://sandboxcernercentral.com/system-accounts/</span></span>

   * <span data-ttu-id="c9445-144">Производственная среда: https://cernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="c9445-144">Production:  https://cernercentral.com/system-accounts/</span></span>

4. <span data-ttu-id="c9445-145">Наконец, необходимо получить идентификаторы области списка пользователей для песочницы и рабочей среды в Cerner, чтобы завершить настройку.</span><span class="sxs-lookup"><span data-stu-id="c9445-145">Finally, you need to acquire User Roster Realm IDs for both the sandbox and production environments in Cerner to complete the configuration.</span></span> <span data-ttu-id="c9445-146">Сведения о получении идентификатора см. по адресу https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM.</span><span class="sxs-lookup"><span data-stu-id="c9445-146">For information on how to acquire this, see: https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM.</span></span> 

5. <span data-ttu-id="c9445-147">Теперь можно настроить Azure AD для подготовки учетных записей пользователей в Cerner.</span><span class="sxs-lookup"><span data-stu-id="c9445-147">Now you can configure Azure AD to provision user accounts to Cerner.</span></span> <span data-ttu-id="c9445-148">Войдите на [портал Azure](https://portal.azure.com) и перейдите в раздел **Azure Active Directory > Корпоративные приложения > Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c9445-148">Sign in to the [Azure portal](https://portal.azure.com), and browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

6. <span data-ttu-id="c9445-149">Если в Cerner Central уже настроен единый вход, найдите свой экземпляр Cerner Central с помощью поля поиска.</span><span class="sxs-lookup"><span data-stu-id="c9445-149">If you have already configured Cerner Central for single sign-on, search for your instance of Cerner Central using the search field.</span></span> <span data-ttu-id="c9445-150">В противном случае щелкните **Добавить** и выполните поиск **Cerner Central** в коллекции приложений.</span><span class="sxs-lookup"><span data-stu-id="c9445-150">Otherwise, select **Add** and search for **Cerner Central** in the application gallery.</span></span> <span data-ttu-id="c9445-151">Выберите Cerner Central в результатах поиска и добавьте его в свой список приложений.</span><span class="sxs-lookup"><span data-stu-id="c9445-151">Select Cerner Central from the search results, and add it to your list of applications.</span></span>

7.  <span data-ttu-id="c9445-152">Выберите экземпляр Cerner Central и перейдите на вкладку **Подготовка**.</span><span class="sxs-lookup"><span data-stu-id="c9445-152">Select your instance of Cerner Central, then select the **Provisioning** tab.</span></span>

8.  <span data-ttu-id="c9445-153">Для параметра **Режим подготовки к работе** выберите значение **Automatic** (Автоматически).</span><span class="sxs-lookup"><span data-stu-id="c9445-153">Set the **Provisioning Mode** to **Automatic**.</span></span>

   ![Подготовка Cerner Central](./media/active-directory-saas-cernercentral-provisioning-tutorial/Cerner.PNG)

9.  <span data-ttu-id="c9445-155">Заполните следующие поля в разделе **Учетные данные администратора**.</span><span class="sxs-lookup"><span data-stu-id="c9445-155">Fill in the following fields under **Admin Credentials**:</span></span>

   * <span data-ttu-id="c9445-156">В поле **URL-адрес клиента** введите URL-адрес в формате, указанном ниже, заменив User-Roster-Realm-ID идентификатором области, полученным на шаге 4.</span><span class="sxs-lookup"><span data-stu-id="c9445-156">In the **Tenant URL** field, enter a URL in the format below, replacing "User-Roster-Realm-ID" with the realm ID you acquired in step #4.</span></span>

> <span data-ttu-id="c9445-157">Песочница: https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span><span class="sxs-lookup"><span data-stu-id="c9445-157">Sandbox: https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span></span> 

> <span data-ttu-id="c9445-158">Рабочая среда: https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span><span class="sxs-lookup"><span data-stu-id="c9445-158">Production: https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span></span> 

   * <span data-ttu-id="c9445-159">В поле **Секретный токен** введите токен носителя OAuth, созданный на шаге 3, и нажмите кнопку **Проверить подключение**.</span><span class="sxs-lookup"><span data-stu-id="c9445-159">In the **Secret Token** field, enter the OAuth bearer token you generated in step #3 and click **Test Connection**.</span></span>

   * <span data-ttu-id="c9445-160">В правом верхнем углу портала должно отобразиться оповещение об успешной проверке подключения.</span><span class="sxs-lookup"><span data-stu-id="c9445-160">You should see a success notification on the upper­right side of your portal.</span></span>

10. <span data-ttu-id="c9445-161">В поле **Почтовое уведомление** введите адрес электронной почты пользователя или группы, которые должны получать уведомления об ошибках подготовки, а также установите флажок ниже.</span><span class="sxs-lookup"><span data-stu-id="c9445-161">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span></span>

11. <span data-ttu-id="c9445-162">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="c9445-162">Click **Save**.</span></span> 

12. <span data-ttu-id="c9445-163">В разделе **Сопоставления атрибутов** просмотрите атрибуты пользователей и групп Azure AD, которые будут синхронизированы с Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="c9445-163">In the **Attribute Mappings** section, review the user and group attributes to be synchronized from Azure AD to Cerner Central.</span></span> <span data-ttu-id="c9445-164">Атрибуты, которые выбраны в качестве свойств **Matching**, используются для сопоставления учетных записей пользователей и групп в Cerner Central для операций обновления.</span><span class="sxs-lookup"><span data-stu-id="c9445-164">The attributes selected as **Matching** properties are used to match the user accounts and groups in Cerner Central for update operations.</span></span> <span data-ttu-id="c9445-165">Нажмите кнопку "Сохранить", чтобы подтвердить все изменения.</span><span class="sxs-lookup"><span data-stu-id="c9445-165">Select the Save button to commit any changes.</span></span>

13. <span data-ttu-id="c9445-166">Чтобы включить службу подготовки Azure AD для Cerner Central, в разделе **Параметры** установите переключатель **Состояние подготовки** в положение **Включено**.</span><span class="sxs-lookup"><span data-stu-id="c9445-166">To enable the Azure AD provisioning service for Cerner Central, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

14. <span data-ttu-id="c9445-167">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="c9445-167">Click **Save**.</span></span> 

<span data-ttu-id="c9445-168">После этого будет запущена начальная синхронизация всех пользователей и (или) групп, назначенных приложению Cerner Central в разделе "Пользователи и группы".</span><span class="sxs-lookup"><span data-stu-id="c9445-168">This starts the initial synchronization of any users and/or groups assigned to Cerner Central in the Users and Groups section.</span></span> <span data-ttu-id="c9445-169">Начальная синхронизация занимает больше времени, чем последующие операции синхронизации. Последующие операции синхронизации выполняются примерно каждые 20 минут, при условии, что служба подготовки Azure AD запущена.</span><span class="sxs-lookup"><span data-stu-id="c9445-169">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the Azure AD provisioning service is running.</span></span> <span data-ttu-id="c9445-170">В разделе **Сведения о синхронизации** можно отслеживать ход синхронизации и с помощью ссылок просматривать отчеты по подготовке, в которых описаны все действия, выполняемые службой подготовки в отношении приложения Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="c9445-170">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Cerner Central app.</span></span>

<span data-ttu-id="c9445-171">Дополнительные сведения о чтении журналов подготовки Azure AD см. в руководстве по [отчетам об автоматической подготовке учетных записей](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="c9445-171">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c9445-172">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c9445-172">Additional resources</span></span>

* [<span data-ttu-id="c9445-173">Cerner Central: публикация данных удостоверений с помощью Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9445-173">Cerner Central: Publishing identity data using Azure AD</span></span>](https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+Azure+AD)
* [<span data-ttu-id="c9445-174">Руководство. Интеграция Azure Active Directory с Cerner Central</span><span class="sxs-lookup"><span data-stu-id="c9445-174">Tutorial: Configuring Cerner Central for single sign-on with Azure Active Directory</span></span>](active-directory-saas-cernercentral-tutorial.md)
* [<span data-ttu-id="c9445-175">Управление подготовкой учетных записей пользователей для корпоративных приложений</span><span class="sxs-lookup"><span data-stu-id="c9445-175">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="c9445-176">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c9445-176">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="c9445-177">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c9445-177">Next steps</span></span>
* <span data-ttu-id="c9445-178">[Сведения о просмотре журналов и получении отчетов о действиях по подготовке](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="c9445-178">[Learn how to review logs and get reports on provisioning activity](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>
