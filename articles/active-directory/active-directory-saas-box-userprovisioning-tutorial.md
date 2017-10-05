---
title: "Руководство. Интеграция Azure Active Directory с Box | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Box."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1c959595-6e57-4954-9c0d-67ba03ee212b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 9f061f3f5a0a4825854b893150ceccc8951487de
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-box-for-automatic-user-provisioning"></a><span data-ttu-id="4fbac-103">Руководство по настройке Box для автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="4fbac-103">Tutorial: Configuring Box for Automatic User Provisioning</span></span>

<span data-ttu-id="4fbac-104">Цель этого руководства — показать, как настроить автоматическую подготовку и отмену подготовки учетных записей из Azure AD в Box.</span><span class="sxs-lookup"><span data-stu-id="4fbac-104">The objective of this tutorial is to show the steps you need to perform in Box and Azure AD to automatically provision and de-provision user accounts from Azure AD to Box.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4fbac-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4fbac-105">Prerequisites</span></span>

<span data-ttu-id="4fbac-106">Сценарий, описанный в этом учебнике, предполагает, что у вас уже имеется:</span><span class="sxs-lookup"><span data-stu-id="4fbac-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="4fbac-107">клиент Azure Active Directory;</span><span class="sxs-lookup"><span data-stu-id="4fbac-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="4fbac-108">подписка Box с поддержкой единого входа;</span><span class="sxs-lookup"><span data-stu-id="4fbac-108">A Box single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="4fbac-109">учетная запись пользователя в Box с разрешениями администратора группы.</span><span class="sxs-lookup"><span data-stu-id="4fbac-109">A user account in Box with Team Admin permissions.</span></span>

## <a name="assigning-users-to-box"></a><span data-ttu-id="4fbac-110">Назначение пользователей в Box</span><span class="sxs-lookup"><span data-stu-id="4fbac-110">Assigning users to Box</span></span> 

<span data-ttu-id="4fbac-111">В Azure Active Directory для определения того, какие пользователи должны получать доступ к выбранным приложениям, используется концепция, называемая "назначение".</span><span class="sxs-lookup"><span data-stu-id="4fbac-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="4fbac-112">В контексте автоматической подготовки учетной записи будут синхронизированы только те записи и группы, которые были "назначены" приложению в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4fbac-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="4fbac-113">Перед настройкой и включением службы подготовки необходимо решить, какие пользователи или группы в Azure AD представляют пользователей, которым требуется доступ к приложению Box.</span><span class="sxs-lookup"><span data-stu-id="4fbac-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Box app.</span></span> <span data-ttu-id="4fbac-114">После этого можно назначить этих пользователей для приложения Box, выполнив следующие действия:</span><span class="sxs-lookup"><span data-stu-id="4fbac-114">Once decided, you can assign these users to your Box app by following the instructions here:</span></span>

[<span data-ttu-id="4fbac-115">Назначение корпоративному приложению пользователя или группы</span><span class="sxs-lookup"><span data-stu-id="4fbac-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

## <a name="assign-users-and-groups"></a><span data-ttu-id="4fbac-116">Назначение пользователей и групп</span><span class="sxs-lookup"><span data-stu-id="4fbac-116">Assign users and groups</span></span>
<span data-ttu-id="4fbac-117">В портале Azure на вкладке **Box > Пользователи и группы** можно указать, каким пользователям и группам следует предоставить доступ к Box.</span><span class="sxs-lookup"><span data-stu-id="4fbac-117">The **Box > Users and Groups** tab in the Azure portal allows you to specify which users and groups should be granted access to Box.</span></span> <span data-ttu-id="4fbac-118">Назначение пользователей или группы приводит к указанным далее результатам.</span><span class="sxs-lookup"><span data-stu-id="4fbac-118">Assignment of a user or group causes the following things to occur:</span></span>

* <span data-ttu-id="4fbac-119">Azure AD позволяет назначенному пользователю (путем прямого назначения или членства в группе) проходить проверку подлинности в Box.</span><span class="sxs-lookup"><span data-stu-id="4fbac-119">Azure AD permits the assigned user (either by direct assignment or group membership) to authenticate to Box.</span></span> <span data-ttu-id="4fbac-120">Если пользователь не назначен, Azure AD запретит этому пользователю вход в Box, а на странице входа Azure AD будет показано сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="4fbac-120">If a user is not assigned, then Azure AD does not permit them to sign in to Box and returns an error on the Azure AD sign-in page.</span></span>
* <span data-ttu-id="4fbac-121">В [средство запуска приложений](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users)будет добавлена плитка приложения Box.</span><span class="sxs-lookup"><span data-stu-id="4fbac-121">An app tile for Box is added to the user's [application launcher](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).</span></span>
* <span data-ttu-id="4fbac-122">Если включена автоматическая подготовка, назначенные пользователи и (или) группы добавляются в очередь подготовки.</span><span class="sxs-lookup"><span data-stu-id="4fbac-122">If automatic provisioning is enabled, then the assigned users and/or groups are added to the provisioning queue to be automatically provisioned.</span></span>
  
  * <span data-ttu-id="4fbac-123">Если для подготовки были настроены только объекты пользователей, то в очередь подготовки помещаются все напрямую назначенные пользователи и все пользователи, входящие в назначенные группы.</span><span class="sxs-lookup"><span data-stu-id="4fbac-123">If only user objects were configured to be provisioned, then all directly assigned users are placed in the provisioning queue, and all users that are members of any assigned groups are placed in the provisioning queue.</span></span> 
  * <span data-ttu-id="4fbac-124">Если для подготовки были настроены объекты групп, то подготовку в Box проходят все назначенные объекты групп, а также пользователи, входящие в эти группы.</span><span class="sxs-lookup"><span data-stu-id="4fbac-124">If group objects were configured to be provisioned, then all assigned group objects are provisioned to Box, and all users that are members of those groups.</span></span> <span data-ttu-id="4fbac-125">Членство пользователей и групп сохраняется после записи в Box.</span><span class="sxs-lookup"><span data-stu-id="4fbac-125">The group and user memberships are preserved upon being written to Box.</span></span>

<span data-ttu-id="4fbac-126">На вкладке **Атрибуты > Единый вход** можно указать, какие атрибуты пользователя (или утверждения) будут представлены в Box при проверке подлинности на основе SAML. На вкладке **Атрибуты > Подготовка** можно указать, как атрибуты пользователей и групп будут передаваться из Azure AD в Box во время операций подготовки.</span><span class="sxs-lookup"><span data-stu-id="4fbac-126">You can use the **Attributes > Single Sign-On** tab to configure which user attributes (or claims) are presented to Box during SAML-based authentication, and the **Attributes > Provisioning** tab to configure how user and group attributes flow from Azure AD to Box during provisioning operations.</span></span>

### <a name="important-tips-for-assigning-users-to-box"></a><span data-ttu-id="4fbac-127">Важные рекомендации по назначению пользователей в Box</span><span class="sxs-lookup"><span data-stu-id="4fbac-127">Important tips for assigning users to Box</span></span> 

*   <span data-ttu-id="4fbac-128">Рекомендуется назначить одного пользователя Azure AD в Box для проверки конфигурации подготовки.</span><span class="sxs-lookup"><span data-stu-id="4fbac-128">It is recommended that a single Azure AD user assigned to Box to test the provisioning configuration.</span></span> <span data-ttu-id="4fbac-129">Дополнительные пользователи и/или группы можно назначить позднее.</span><span class="sxs-lookup"><span data-stu-id="4fbac-129">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="4fbac-130">При назначении пользователя Box необходимо выбрать допустимую роль пользователя.</span><span class="sxs-lookup"><span data-stu-id="4fbac-130">When assigning a user to box, you must select a valid user role.</span></span> <span data-ttu-id="4fbac-131">Роль "Доступ по умолчанию" не работает для подготовки.</span><span class="sxs-lookup"><span data-stu-id="4fbac-131">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="4fbac-132">Включение автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="4fbac-132">Enable Automated User Provisioning</span></span>

<span data-ttu-id="4fbac-133">В этом разделе описывается подключение к API подготовки учетной записи пользователя Azure AD в Box и настройка подготовки службы для создания, обновления и отмены назначения учетных записей пользователей в Box на основе назначения пользователей и групп в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4fbac-133">This section guides through connecting your Azure AD to Box's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Box based on user and group assignment in Azure AD.</span></span>

<span data-ttu-id="4fbac-134">Если включена автоматическая подготовка, назначенные пользователи и (или) группы добавляются в очередь подготовки.</span><span class="sxs-lookup"><span data-stu-id="4fbac-134">If automatic provisioning is enabled, then the assigned users and/or groups are added to the provisioning queue to be automatically provisioned.</span></span>
    
 * <span data-ttu-id="4fbac-135">Если для подготовки были настроены только объекты пользователей, то в очередь подготовки помещаются все напрямую назначенные пользователи и все пользователи, входящие в назначенные группы.</span><span class="sxs-lookup"><span data-stu-id="4fbac-135">If only user objects are configured to be provisioned, then directly assigned users are placed in the provisioning queue, and all users that are members of any assigned groups are placed in the provisioning queue.</span></span> 
    
 * <span data-ttu-id="4fbac-136">Если для подготовки были настроены объекты групп, то подготовку в Box проходят все назначенные объекты групп, а также пользователи, входящие в эти группы.</span><span class="sxs-lookup"><span data-stu-id="4fbac-136">If group objects were configured to be provisioned, then all assigned group objects are provisioned to Box, and all users that are members of those groups.</span></span> <span data-ttu-id="4fbac-137">Членство пользователей и групп сохраняется после записи в Box.</span><span class="sxs-lookup"><span data-stu-id="4fbac-137">The group and user memberships are preserved upon being written to Box.</span></span>

> [!TIP] 
> <span data-ttu-id="4fbac-138">Для Box можно также включить единый вход на основе SAML. Для этого следуйте инструкциям на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4fbac-138">You may also choose to enabled SAML-based Single Sign-On for Box, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="4fbac-139">Единый вход можно настроить независимо от автоматической подготовки, хотя эти две возможности дополняют друг друга.</span><span class="sxs-lookup"><span data-stu-id="4fbac-139">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-automatic-user-account-provisioning"></a><span data-ttu-id="4fbac-140">Настройка автоматической подготовки учетных записей пользователей:</span><span class="sxs-lookup"><span data-stu-id="4fbac-140">To configure automatic user account provisioning:</span></span>

<span data-ttu-id="4fbac-141">В этом разделе показано, как включить подготовку учетных записей пользователей Active Directory для Box.</span><span class="sxs-lookup"><span data-stu-id="4fbac-141">The objective of this section is to outline how to enable provisioning of Active Directory user accounts to Box.</span></span>

1. <span data-ttu-id="4fbac-142">На [портале Azure](https://portal.azure.com) перейдите в раздел **Azure Active Directory > Корпоративные приложения > Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="4fbac-142">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="4fbac-143">Если для Box уже настроен единый вход, найдите свой экземпляр Box с помощью поиска.</span><span class="sxs-lookup"><span data-stu-id="4fbac-143">If you have already configured Box for single sign-on, search for your instance of Box using the search field.</span></span> <span data-ttu-id="4fbac-144">В противном случае щелкните **Добавить** и найдите **Box** в коллекции приложений.</span><span class="sxs-lookup"><span data-stu-id="4fbac-144">Otherwise, select **Add** and search for **Box** in the application gallery.</span></span> <span data-ttu-id="4fbac-145">Выберите Box в результатах поиска и добавьте его в список приложений.</span><span class="sxs-lookup"><span data-stu-id="4fbac-145">Select Box from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="4fbac-146">Выберите экземпляр Box, а затем перейдите на вкладку **Подготовка**.</span><span class="sxs-lookup"><span data-stu-id="4fbac-146">Select your instance of Box, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="4fbac-147">Для параметра **Режим подготовки к работе** выберите значение **Automatic** (Автоматически).</span><span class="sxs-lookup"><span data-stu-id="4fbac-147">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![подготовка](./media/active-directory-saas-box-userprovisioning-tutorial/provisioning.png)

5. <span data-ttu-id="4fbac-149">В разделе **Учетные данные администратора** щелкните **Авторизация**, чтобы открыть диалоговое окно входа в систему в новом окне браузера.</span><span class="sxs-lookup"><span data-stu-id="4fbac-149">Under the **Admin Credentials** section, click **Authorize** to open a Box login dialog in a new browser window.</span></span>

6. <span data-ttu-id="4fbac-150">На странице **Войдите в систему, чтобы предоставить доступ к Box** введите необходимые учетные данные и нажмите кнопку **Авторизовать**.</span><span class="sxs-lookup"><span data-stu-id="4fbac-150">On the **Login to grant access to Box** page, provide the required credentials, and then click **Authorize**.</span></span> 
   
    <span data-ttu-id="4fbac-151">![Включение автоматической подготовки пользователей](./media/active-directory-saas-box-userprovisioning-tutorial/IC769546.png "Включение автоматической подготовки пользователей")</span><span class="sxs-lookup"><span data-stu-id="4fbac-151">![Enable automatic user provisioning](./media/active-directory-saas-box-userprovisioning-tutorial/IC769546.png "Enable automatic user provisioning")</span></span>

7. <span data-ttu-id="4fbac-152">Нажмите кнопку **Предоставить доступ к Box**, чтобы авторизовать операцию и вернуться на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="4fbac-152">Click **Grant access to Box** to authorize this operation and to return to the Azure portal.</span></span> 
   
    <span data-ttu-id="4fbac-153">![Включение автоматической подготовки пользователей](./media/active-directory-saas-box-userprovisioning-tutorial/IC769549.png "Включение автоматической подготовки пользователей")</span><span class="sxs-lookup"><span data-stu-id="4fbac-153">![Enable automatic user provisioning](./media/active-directory-saas-box-userprovisioning-tutorial/IC769549.png "Enable automatic user provisioning")</span></span>

8. <span data-ttu-id="4fbac-154">На портале Azure щелкните **Проверить подключение**, чтобы убедиться, что Azure AD может подключиться к приложению Box.</span><span class="sxs-lookup"><span data-stu-id="4fbac-154">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Box app.</span></span> <span data-ttu-id="4fbac-155">Если подключение отсутствует, убедитесь, что у учетной записи Box есть права администратора группы, и повторите шаг **"Авторизовать"**.</span><span class="sxs-lookup"><span data-stu-id="4fbac-155">If the connection fails, ensure your Box account has Team Admin permissions and try the **"Authorize"** step again.</span></span>

9. <span data-ttu-id="4fbac-156">В поле **Почтовое уведомление** введите адрес электронной почты пользователя или группы, которые должны получать уведомления об ошибках подготовки, а также установите флажок.</span><span class="sxs-lookup"><span data-stu-id="4fbac-156">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

10. <span data-ttu-id="4fbac-157">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="4fbac-157">Click **Save.**</span></span>

11. <span data-ttu-id="4fbac-158">В разделе "Сопоставления" выберите **Синхронизировать пользователей Azure Active Directory с Box**.</span><span class="sxs-lookup"><span data-stu-id="4fbac-158">Under the Mappings section, select **Synchronize Azure Active Directory Users to Box.**</span></span>

12. <span data-ttu-id="4fbac-159">В разделе **Сопоставления атрибутов** просмотрите пользовательские атрибуты, которые синхронизированы из Azure AD в Box.</span><span class="sxs-lookup"><span data-stu-id="4fbac-159">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Box.</span></span> <span data-ttu-id="4fbac-160">Атрибуты, выбранные как свойства **сопоставления**, используются для сопоставления учетных записей пользователей в Box для операций обновления.</span><span class="sxs-lookup"><span data-stu-id="4fbac-160">The attributes selected as **Matching** properties are used to match the user accounts in Box for update operations.</span></span> <span data-ttu-id="4fbac-161">Нажмите кнопку "Сохранить", чтобы подтвердить все изменения.</span><span class="sxs-lookup"><span data-stu-id="4fbac-161">Select the Save button to commit any changes.</span></span>

13. <span data-ttu-id="4fbac-162">Чтобы включить службу подготовки Azure AD для Box, в разделе "Параметры" измените значение параметра **Состояние подготовки** на **Включено**.</span><span class="sxs-lookup"><span data-stu-id="4fbac-162">To enable the Azure AD provisioning service for Box, change the **Provisioning Status** to **On** in the Settings section</span></span>

14. <span data-ttu-id="4fbac-163">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="4fbac-163">Click **Save.**</span></span>

<span data-ttu-id="4fbac-164">После этого будет запущена начальная синхронизация всех пользователей и групп, назначенных для Box в разделе "Пользователи и группы".</span><span class="sxs-lookup"><span data-stu-id="4fbac-164">That starts the initial synchronization of any users and/or groups assigned to Box in the Users and Groups section.</span></span> <span data-ttu-id="4fbac-165">Начальная синхронизация занимает больше времени, чем последующие операции синхронизации. Последующие операции синхронизации выполняются примерно каждые 20 минут, при условии, что служба запущена.</span><span class="sxs-lookup"><span data-stu-id="4fbac-165">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="4fbac-166">В разделе **Сведения о синхронизации** можно отслеживать ход выполнения и переходить по ссылкам для просмотра отчетов по подготовке, в которых зафиксированы все действия, выполняемые службой подготовки в приложении Box.</span><span class="sxs-lookup"><span data-stu-id="4fbac-166">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Box app.</span></span>

<span data-ttu-id="4fbac-167">Теперь можно создать тестовую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="4fbac-167">You can now create a test account.</span></span> <span data-ttu-id="4fbac-168">Подождите примерно 20 минут, чтобы убедиться, что учетная запись синхронизирована с Box.</span><span class="sxs-lookup"><span data-stu-id="4fbac-168">Wait for up to 20 minutes to verify that the account has been synchronized to box.</span></span>

<span data-ttu-id="4fbac-169">В клиенте Box список синхронизированных пользователей приводится в разделе **Управляемые пользователи** в **консоли администрирования**.</span><span class="sxs-lookup"><span data-stu-id="4fbac-169">In your Box tenant, synchronized users are listed under **Managed Users** in the **Admin Console**.</span></span>

<span data-ttu-id="4fbac-170">![Состояние интеграции](./media/active-directory-saas-box-userprovisioning-tutorial/IC769556.png "Состояние интеграции")</span><span class="sxs-lookup"><span data-stu-id="4fbac-170">![Integration status](./media/active-directory-saas-box-userprovisioning-tutorial/IC769556.png "Integration status")</span></span>


## <a name="additional-resources"></a><span data-ttu-id="4fbac-171">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="4fbac-171">Additional resources</span></span>

* [<span data-ttu-id="4fbac-172">Управление подготовкой учетных записей пользователей для корпоративных приложений</span><span class="sxs-lookup"><span data-stu-id="4fbac-172">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4fbac-173">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4fbac-173">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="4fbac-174">Настройка единого входа</span><span class="sxs-lookup"><span data-stu-id="4fbac-174">Configure Single Sign-on</span></span>](active-directory-saas-box-tutorial.md)