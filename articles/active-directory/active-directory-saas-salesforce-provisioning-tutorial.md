---
title: "Руководство по интеграции Azure Active Directory с Salesforce | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в приложении Salesforce."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 49384b8b-3836-4eb1-b438-1c46bb9baf6f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: a573a7ef79e28c50ae0923849a88f88af40f21be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-salesforce-for-automatic-user-provisioning"></a><span data-ttu-id="9e929-103">Руководство по настройке Salesforce для автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="9e929-103">Tutorial: Configuring Salesforce for Automatic User Provisioning</span></span>

<span data-ttu-id="9e929-104">Цель этого учебника — показать, как в Salesforce и Azure AD необходимо выполнять автоматическую подготовку и отмену подготовки учетных записей пользователей из Azure AD в Salesforce.</span><span class="sxs-lookup"><span data-stu-id="9e929-104">The objective of this tutorial is to show the steps required to perform in Salesforce and Azure AD to automatically provision and de-provision user accounts from Azure AD to Salesforce.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9e929-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9e929-105">Prerequisites</span></span>

<span data-ttu-id="9e929-106">Сценарий, описанный в этом учебнике, предполагает, что у вас уже имеется:</span><span class="sxs-lookup"><span data-stu-id="9e929-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="9e929-107">Клиент Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9e929-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="9e929-108">У вас должен быть действительный клиент для работы с Salesforce for Work или Salesforce for Education.</span><span class="sxs-lookup"><span data-stu-id="9e929-108">You must have a valid tenant for Salesforce for Work or Salesforce for Education.</span></span> <span data-ttu-id="9e929-109">Для любой из этих служб можно воспользоваться бесплатной пробной учетной записью.</span><span class="sxs-lookup"><span data-stu-id="9e929-109">You may use a free trial     account for either service.</span></span>
*   <span data-ttu-id="9e929-110">Учетная запись пользователя в Salesforce с разрешениями администратора группы.</span><span class="sxs-lookup"><span data-stu-id="9e929-110">A user account in Salesforce with Team Admin permissions.</span></span>

## <a name="assigning-users-to-salesforce"></a><span data-ttu-id="9e929-111">Назначение пользователей в Salesforce</span><span class="sxs-lookup"><span data-stu-id="9e929-111">Assigning users to Salesforce</span></span>

<span data-ttu-id="9e929-112">В Azure Active Directory для определения того, какие пользователи должны получать доступ к выбранным приложениям, используется концепция, называемая "назначение".</span><span class="sxs-lookup"><span data-stu-id="9e929-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="9e929-113">В контексте автоматической подготовки учетной записи синхронизированы только те записи и группы, которые были "назначены" приложению в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9e929-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="9e929-114">Перед настройкой и включением службы подготовки необходимо решить, какие пользователи или группы в Azure AD представляют пользователей, которым необходим доступ к приложению Salesforce.</span><span class="sxs-lookup"><span data-stu-id="9e929-114">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Salesforce app.</span></span> <span data-ttu-id="9e929-115">Когда этот вопрос будет решен, можно назначить этих пользователей приложению Salesforce, следуя перечисленным ниже указаниям.</span><span class="sxs-lookup"><span data-stu-id="9e929-115">Once decided, you can assign these users to your Salesforce app by following the instructions here:</span></span>

[<span data-ttu-id="9e929-116">Назначение корпоративному приложению пользователя или группы</span><span class="sxs-lookup"><span data-stu-id="9e929-116">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-salesforce"></a><span data-ttu-id="9e929-117">Важные рекомендации по назначению пользователей в Salesforce</span><span class="sxs-lookup"><span data-stu-id="9e929-117">Important tips for assigning users to Salesforce</span></span>

*   <span data-ttu-id="9e929-118">Рекомендуется назначить одного пользователя Azure AD в Salesforce для тестирования конфигурации подготовки.</span><span class="sxs-lookup"><span data-stu-id="9e929-118">It is recommended that a single Azure AD user is assigned to Salesforce to test the provisioning configuration.</span></span> <span data-ttu-id="9e929-119">Дополнительные пользователи и/или группы можно назначить позднее.</span><span class="sxs-lookup"><span data-stu-id="9e929-119">Additional users and/or groups may be assigned later.</span></span>

*  <span data-ttu-id="9e929-120">При назначении пользователя в Salesforce необходимо выбрать допустимую роль пользователя.</span><span class="sxs-lookup"><span data-stu-id="9e929-120">When assigning a user to Salesforce, you must select a valid user role.</span></span> <span data-ttu-id="9e929-121">Роль "Доступ по умолчанию" не работает для подготовки.</span><span class="sxs-lookup"><span data-stu-id="9e929-121">The "Default Access" role does not work for provisioning</span></span>

    > [!NOTE]
    > <span data-ttu-id="9e929-122">Это приложение импортирует настраиваемые роли из Salesforce в рамках процесса подготовки, который клиент может выбрать при назначении пользователей</span><span class="sxs-lookup"><span data-stu-id="9e929-122">This app imports custom roles from Salesforce as part of the provisioning process, which the customer may want to select when assigning users</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="9e929-123">Включение автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="9e929-123">Enable Automated User Provisioning</span></span>

<span data-ttu-id="9e929-124">В этом разделе описывается подключение к API подготовки учетной записи пользователя Azure AD в Salesforce и настройка подготовки службы для создания, обновления и отмены назначения учетных записей пользователей в Salesforce на основе назначения пользователей и групп в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9e929-124">This section guides you through connecting your Azure AD to Salesforce's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Salesforce based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="9e929-125">Для Salesforce также можно включить единый вход на базе управления лицензиями. Для этого следуйте инструкциям, указанным на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9e929-125">You may also choose to enabled SAML-based Single Sign-On for Salesforce, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="9e929-126">Единый вход можно настроить независимо от автоматической подготовки, хотя эти две возможности дополняют друг друга.</span><span class="sxs-lookup"><span data-stu-id="9e929-126">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-automatic-user-account-provisioning"></a><span data-ttu-id="9e929-127">Настройка автоматической подготовки учетных записей пользователей:</span><span class="sxs-lookup"><span data-stu-id="9e929-127">To configure automatic user account provisioning:</span></span>

<span data-ttu-id="9e929-128">В этом разделе показано, как включить подготовку учетных записей пользователей Active Directory для Salesforce.</span><span class="sxs-lookup"><span data-stu-id="9e929-128">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Salesforce.</span></span>

1. <span data-ttu-id="9e929-129">На [портале Azure](https://portal.azure.com) перейдите в раздел **Azure Active Directory > Корпоративные приложения > Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="9e929-129">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="9e929-130">Если в Salesforce уже настроен единый вход, найдите свой экземпляр Salesforce с помощью поля поиска.</span><span class="sxs-lookup"><span data-stu-id="9e929-130">If you have already configured Salesforce for single sign-on, search for your instance of Salesforce using the search field.</span></span> <span data-ttu-id="9e929-131">В противном случае щелкните **Добавить** и выполните поиск **Salesforce** в коллекции приложений.</span><span class="sxs-lookup"><span data-stu-id="9e929-131">Otherwise, select **Add** and search for **Salesforce** in the application gallery.</span></span> <span data-ttu-id="9e929-132">Выберите Salesforce в результатах поиска и добавьте его в список приложений.</span><span class="sxs-lookup"><span data-stu-id="9e929-132">Select Salesforce from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="9e929-133">Выберите экземпляр Salesforce, а затем перейдите на вкладку **Подготовка**.</span><span class="sxs-lookup"><span data-stu-id="9e929-133">Select your instance of Salesforce, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="9e929-134">Для параметра **Режим подготовки к работе** выберите значение **Automatic** (Автоматически).</span><span class="sxs-lookup"><span data-stu-id="9e929-134">Set the **Provisioning Mode** to **Automatic**.</span></span> 
<span data-ttu-id="9e929-135">![подготовка](./media/active-directory-saas-salesforce-provisioning-tutorial/provisioning.png)</span><span class="sxs-lookup"><span data-stu-id="9e929-135">![provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/provisioning.png)</span></span>

5. <span data-ttu-id="9e929-136">В разделе **Учетные данные администратора** укажите следующие параметры конфигурации:</span><span class="sxs-lookup"><span data-stu-id="9e929-136">Under the **Admin Credentials** section, provide the following configuration settings:</span></span>
   
    <span data-ttu-id="9e929-137">а.</span><span class="sxs-lookup"><span data-stu-id="9e929-137">a.</span></span> <span data-ttu-id="9e929-138">В текстовом поле **Имя администратора** введите имя учетной записи Salesforce с профилем **системного администратора** в Salesforce.com.</span><span class="sxs-lookup"><span data-stu-id="9e929-138">In the **Admin User Name** textbox, type a Salesforce account name that has the **System Administrator** profile in Salesforce.com assigned.</span></span>
   
    <span data-ttu-id="9e929-139">b.</span><span class="sxs-lookup"><span data-stu-id="9e929-139">b.</span></span> <span data-ttu-id="9e929-140">В текстовом поле **Пароль администратора** введите пароль для этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="9e929-140">In the **Admin Password** textbox, type the password for this account.</span></span>

6. <span data-ttu-id="9e929-141">Для получения маркера безопасности Salesforce откройте новую вкладку и выполните вход с этой учетной записью администратора Salesforce.</span><span class="sxs-lookup"><span data-stu-id="9e929-141">To get your Salesforce security token, open a new tab and sign into the same Salesforce admin account.</span></span> <span data-ttu-id="9e929-142">В правом верхнем углу страницы щелкните свое имя и выберите команду **Мои параметры**.</span><span class="sxs-lookup"><span data-stu-id="9e929-142">On the top right corner of the page, click your name, and then click **My Settings**.</span></span>

     <span data-ttu-id="9e929-143">![Включение автоматической подготовки пользователей](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-my-settings.png "Включение автоматической подготовки пользователей")</span><span class="sxs-lookup"><span data-stu-id="9e929-143">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-my-settings.png "Enable automatic user provisioning")</span></span>
7. <span data-ttu-id="9e929-144">В области навигации слева щелкните **Personal** (Личное), чтобы развернуть соответствующий раздел, и выберите команду **Reset My Security Token** (Сброс маркера безопасности).</span><span class="sxs-lookup"><span data-stu-id="9e929-144">On the left navigation pane, click **Personal** to expand the related section, and then click **Reset My Security Token**.</span></span>
  
    <span data-ttu-id="9e929-145">![Включение автоматической подготовки пользователей](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-personal-reset.png "Включение автоматической подготовки пользователей")</span><span class="sxs-lookup"><span data-stu-id="9e929-145">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-personal-reset.png "Enable automatic user provisioning")</span></span>
8. <span data-ttu-id="9e929-146">На странице **Reset My Security Token** (Сброс маркера безопасности) нажмите кнопку **Reset Security Token** (Сбросить маркер безопасности).</span><span class="sxs-lookup"><span data-stu-id="9e929-146">On the **Reset My Security Token** page, click **Reset Security Token** button.</span></span>

    <span data-ttu-id="9e929-147">![Включение автоматической подготовки пользователей](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-reset-token.png "Включение автоматической подготовки пользователей")</span><span class="sxs-lookup"><span data-stu-id="9e929-147">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-reset-token.png "Enable automatic user provisioning")</span></span>
9. <span data-ttu-id="9e929-148">Проверьте входящие сообщения в почтовом ящике, связанном с этой учетной записью администратора.</span><span class="sxs-lookup"><span data-stu-id="9e929-148">Check the email inbox associated with this admin account.</span></span> <span data-ttu-id="9e929-149">Найдите сообщение от Salesforce.com с новым маркером безопасности.</span><span class="sxs-lookup"><span data-stu-id="9e929-149">Look for an email from Salesforce.com that contains the new security token.</span></span>
10. <span data-ttu-id="9e929-150">Скопируйте маркер, перейдите к окну Azure AD и вставьте его в поле **Маркер сокета**.</span><span class="sxs-lookup"><span data-stu-id="9e929-150">Copy the token, go to your Azure AD window, and paste it into the **Socket Token** field.</span></span>

11. <span data-ttu-id="9e929-151">На портале Azure щелкните **Проверить подключение**, чтобы убедиться, что Azure AD может подключиться к приложению Salesforce.</span><span class="sxs-lookup"><span data-stu-id="9e929-151">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Salesforce app.</span></span>

12. <span data-ttu-id="9e929-152">В поле **Почтовое уведомление** введите адрес электронной почты пользователя или группы, которые должны получать уведомления об ошибках подготовки, а также установите флажок ниже.</span><span class="sxs-lookup"><span data-stu-id="9e929-152">In the **Notification Email** field, enter the email address of a person or group who should receive provisioning error notifications, and check the checkbox below.</span></span>

13. <span data-ttu-id="9e929-153">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="9e929-153">Click **Save.**</span></span>  
    
14.  <span data-ttu-id="9e929-154">В разделе сопоставления выберите **Synchronize Azure Active Directory Users to Salesforce** (Синхронизировать пользователей Azure Active Directory с Salesforce).</span><span class="sxs-lookup"><span data-stu-id="9e929-154">Under the Mappings section, select **Synchronize Azure Active Directory Users to Salesforce.**</span></span>

15. <span data-ttu-id="9e929-155">В разделе **Attribute Mappings** (Сопоставление атрибутов) просмотрите пользовательские атрибуты, которые синхронизированы из Azure AD в Salesforce.</span><span class="sxs-lookup"><span data-stu-id="9e929-155">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Salesforce.</span></span> <span data-ttu-id="9e929-156">Обратите внимание, что атрибуты, которые выбраны в качестве свойств **Matching** (Сопоставление), будут использоваться для сопоставления учетных записей пользователей в Salesforce для операций обновления.</span><span class="sxs-lookup"><span data-stu-id="9e929-156">Note that the attributes selected as **Matching** properties are used to match the user accounts in Salesforce for update operations.</span></span> <span data-ttu-id="9e929-157">Нажмите кнопку "Сохранить", чтобы подтвердить все изменения.</span><span class="sxs-lookup"><span data-stu-id="9e929-157">Select the Save button to commit any changes.</span></span>

16. <span data-ttu-id="9e929-158">Чтобы включить службу подготовки Azure AD для Salesforce, измените значение параметра **Provisioning Status** (Статус подготовки) на **On** (Включено) в разделе "Настройки".</span><span class="sxs-lookup"><span data-stu-id="9e929-158">To enable the Azure AD provisioning service for Salesforce, change the **Provisioning Status** to **On** in the Settings section</span></span>

17. <span data-ttu-id="9e929-159">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="9e929-159">Click **Save.**</span></span>

<span data-ttu-id="9e929-160">После этого начнется начальная синхронизация всех пользователей и групп, назначенная в Salesforce в разделе "Пользователи и группы".</span><span class="sxs-lookup"><span data-stu-id="9e929-160">This starts the initial synchronization of any users and/or groups assigned to Salesforce in the Users and Groups section.</span></span> <span data-ttu-id="9e929-161">Обратите внимание, что начальная синхронизация занимает больше времени, чем последующие операции синхронизации. Последующие операции синхронизации выполняются примерно каждые 20 минут, при условии, что служба запущена.</span><span class="sxs-lookup"><span data-stu-id="9e929-161">Note that the initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="9e929-162">В разделе **Сведения о синхронизации** можно отслеживать ход выполнения и переходить по ссылкам для просмотра отчетов по подготовке, в которых зафиксированы все действия, выполняемые в приложении Salesforce службой подготовки.</span><span class="sxs-lookup"><span data-stu-id="9e929-162">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Salesforce app.</span></span>

<span data-ttu-id="9e929-163">Теперь можно создать тестовую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="9e929-163">You can now create a test account.</span></span> <span data-ttu-id="9e929-164">Подождите до 20 минут и убедитесь, что учетная запись синхронизирована с песочницей Salesforce.</span><span class="sxs-lookup"><span data-stu-id="9e929-164">Wait for up to 20 minutes to verify that the account has been synchronized to Salesforce.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9e929-165">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="9e929-165">Additional resources</span></span>

* [<span data-ttu-id="9e929-166">Управление подготовкой учетных записей пользователей для корпоративных приложений</span><span class="sxs-lookup"><span data-stu-id="9e929-166">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9e929-167">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9e929-167">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="9e929-168">Настройка единого входа</span><span class="sxs-lookup"><span data-stu-id="9e929-168">Configure Single Sign-on</span></span>](active-directory-saas-salesforce-tutorial.md)