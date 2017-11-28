---
title: "Руководство по интеграции Azure Active Directory с Jive | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Jive."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6fbfdbe7-d66c-4305-9fea-76d6a6a92830
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 957b152fdd40d08a867e788b0cb9f7d57ed481e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-jive-for-user-provisioning"></a><span data-ttu-id="fb424-103">Руководство по настройке Jive для подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="fb424-103">Tutorial: Configuring Jive for User Provisioning</span></span>

<span data-ttu-id="fb424-104">Цель этого руководства — показать, как в Jive и Azure AD настроить автоматическую подготовку и отзыв учетных записей пользователей из Azure AD в Jive.</span><span class="sxs-lookup"><span data-stu-id="fb424-104">The objective of this tutorial is to show you the steps you need to perform in Jive and Azure AD to automatically provision and de-provision user accounts from Azure AD to Jive.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fb424-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="fb424-105">Prerequisites</span></span>

<span data-ttu-id="fb424-106">Сценарий, описанный в этом учебнике, предполагает, что у вас уже имеется:</span><span class="sxs-lookup"><span data-stu-id="fb424-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="fb424-107">клиент Azure Active Directory;</span><span class="sxs-lookup"><span data-stu-id="fb424-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="fb424-108">подписка Jive с поддержкой единого входа;</span><span class="sxs-lookup"><span data-stu-id="fb424-108">A Jive single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="fb424-109">учетная запись пользователя Jive с разрешениями администратора команды.</span><span class="sxs-lookup"><span data-stu-id="fb424-109">A user account in Jive with Team Admin permissions.</span></span>

## <a name="assigning-users-to-jive"></a><span data-ttu-id="fb424-110">Назначение пользователей в Jive</span><span class="sxs-lookup"><span data-stu-id="fb424-110">Assigning users to Jive</span></span>

<span data-ttu-id="fb424-111">В Azure Active Directory для определения того, какие пользователи должны получать доступ к выбранным приложениям, используется концепция, называемая "назначение".</span><span class="sxs-lookup"><span data-stu-id="fb424-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="fb424-112">В контексте автоматической подготовки учетной записи будут синхронизированы только те записи и группы, которые были "назначены" приложению в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fb424-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="fb424-113">Перед настройкой и включением службы подготовки необходимо решить, какие пользователи или группы в Azure AD представляют пользователей, которым требуется доступ к приложению Jive.</span><span class="sxs-lookup"><span data-stu-id="fb424-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Jive app.</span></span> <span data-ttu-id="fb424-114">Когда данное решение будет принято, можно будет назначить этих пользователей приложению Jive, следуя указаниям ниже.</span><span class="sxs-lookup"><span data-stu-id="fb424-114">Once decided, you can assign these users to your Jive app by following the instructions here:</span></span>

[<span data-ttu-id="fb424-115">Назначение корпоративному приложению пользователя или группы</span><span class="sxs-lookup"><span data-stu-id="fb424-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-jive"></a><span data-ttu-id="fb424-116">Важные рекомендации по назначению пользователей в Jive</span><span class="sxs-lookup"><span data-stu-id="fb424-116">Important tips for assigning users to Jive</span></span>

*   <span data-ttu-id="fb424-117">Рекомендуется назначить одного пользователя Azure AD в Jive для тестирования конфигурации подготовки.</span><span class="sxs-lookup"><span data-stu-id="fb424-117">It is recommended that a single Azure AD user be assigned to Jive to test the provisioning configuration.</span></span> <span data-ttu-id="fb424-118">Дополнительные пользователи и/или группы можно назначить позднее.</span><span class="sxs-lookup"><span data-stu-id="fb424-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="fb424-119">При назначении пользователя Jive необходимо выбрать допустимую роль пользователя.</span><span class="sxs-lookup"><span data-stu-id="fb424-119">When assigning a user to Jive, you must select a valid user role.</span></span> <span data-ttu-id="fb424-120">Роль "Доступ по умолчанию" не работает для подготовки.</span><span class="sxs-lookup"><span data-stu-id="fb424-120">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="fb424-121">Включение подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="fb424-121">Enable User Provisioning</span></span>

<span data-ttu-id="fb424-122">В этом разделе описывается подключение вашего каталога Azure AD к API подготовки учетных записей пользователей в Jive и настройка службы подготовки для создания, обновления и отключения назначенных учетных записей пользователей в Jive на основе назначения пользователей и групп в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fb424-122">This section guides you through connecting your Azure AD to Jive's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Jive based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="fb424-123">Для Jive можно также включить единый вход на основе SAML. Для этого следуйте инструкциям на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fb424-123">You may also choose to enabled SAML-based Single Sign-On for Jive, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="fb424-124">Единый вход можно настроить независимо от автоматической подготовки, хотя эти две возможности дополняют друг друга.</span><span class="sxs-lookup"><span data-stu-id="fb424-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-user-account-provisioning"></a><span data-ttu-id="fb424-125">Настройка подготовки учетных записей пользователей</span><span class="sxs-lookup"><span data-stu-id="fb424-125">To configure user account provisioning:</span></span>

<span data-ttu-id="fb424-126">В этом разделе показано, как включить подготовку учетных записей пользователей Active Directory для Jive.</span><span class="sxs-lookup"><span data-stu-id="fb424-126">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Jive.</span></span>
<span data-ttu-id="fb424-127">В рамках этой процедуры потребуется предоставить маркер безопасности пользователя, который необходимо запросить на веб-сайте Jive.com.</span><span class="sxs-lookup"><span data-stu-id="fb424-127">As part of this procedure, you are required to provide a user security token you need to request from Jive.com.</span></span>

1. <span data-ttu-id="fb424-128">На [портале Azure](https://portal.azure.com) перейдите в раздел **Azure Active Directory > Корпоративные приложения > Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="fb424-128">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="fb424-129">Если в Jive уже настроен единый вход, найдите свой экземпляр Jive с помощью поля поиска.</span><span class="sxs-lookup"><span data-stu-id="fb424-129">If you have already configured Jive for single sign-on, search for your instance of Jive using the search field.</span></span> <span data-ttu-id="fb424-130">В противном случае щелкните **Добавить** и выполните поиск **Jive** в коллекции приложений.</span><span class="sxs-lookup"><span data-stu-id="fb424-130">Otherwise, select **Add** and search for **Jive** in the application gallery.</span></span> <span data-ttu-id="fb424-131">Выберите Jive в результатах поиска и добавьте в список приложений.</span><span class="sxs-lookup"><span data-stu-id="fb424-131">Select Jive from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="fb424-132">Выберите экземпляр Jive, а затем перейдите на вкладку **Подготовка**.</span><span class="sxs-lookup"><span data-stu-id="fb424-132">Select your instance of Jive, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="fb424-133">Для параметра **Режим подготовки к работе** выберите значение **Automatic** (Автоматически).</span><span class="sxs-lookup"><span data-stu-id="fb424-133">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![Подготовка](./media/active-directory-saas-jive-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="fb424-135">В разделе **Учетные данные администратора** укажите следующие параметры конфигурации.</span><span class="sxs-lookup"><span data-stu-id="fb424-135">Under the **Admin Credentials** section, provide the following configuration settings:</span></span>
   
    <span data-ttu-id="fb424-136">а.</span><span class="sxs-lookup"><span data-stu-id="fb424-136">a.</span></span> <span data-ttu-id="fb424-137">В текстовом поле **Имя пользователя администратора Jive** введите имя учетной записи Jive, которой в Jive.com назначен профиль **Системный администратор**.</span><span class="sxs-lookup"><span data-stu-id="fb424-137">In the **Jive Admin User Name** textbox, type a Jive account name that has the **System Administrator** profile in Jive.com assigned.</span></span>
   
    <span data-ttu-id="fb424-138">b.</span><span class="sxs-lookup"><span data-stu-id="fb424-138">b.</span></span> <span data-ttu-id="fb424-139">В текстовом поле **Пароль администратора Jive** введите пароль для этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="fb424-139">In the **Jive Admin Password** textbox, type the password for this account.</span></span>
   
    <span data-ttu-id="fb424-140">c.</span><span class="sxs-lookup"><span data-stu-id="fb424-140">c.</span></span> <span data-ttu-id="fb424-141">В текстовом поле **URL-адрес клиента Jive** введите URL-адрес клиента Jive.</span><span class="sxs-lookup"><span data-stu-id="fb424-141">In the **Jive Tenant URL** textbox, type the Jive tenant URL.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="fb424-142">URL-адрес клиента Jive — это URL-адрес, используемый вашей организацией для входа в Jive.</span><span class="sxs-lookup"><span data-stu-id="fb424-142">The Jive tenant URL is URL that is used by your organization to log in to Jive.</span></span>  
      > <span data-ttu-id="fb424-143">Как правило, этот URL-адрес имеет следующий формат: **www.\<организация\>.jive.com**.</span><span class="sxs-lookup"><span data-stu-id="fb424-143">Typically, the URL has the following format: **www.\<organization\>.jive.com**.</span></span>          

6. <span data-ttu-id="fb424-144">На портале Azure щелкните **Проверить подключение**, чтобы убедиться, что Azure AD может подключиться к приложению Jive.</span><span class="sxs-lookup"><span data-stu-id="fb424-144">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Jive app.</span></span>

7. <span data-ttu-id="fb424-145">В поле **Почтовое уведомление** введите адрес электронной почты пользователя или группы, которые должны получать уведомления об ошибках подготовки, а также установите флажок ниже.</span><span class="sxs-lookup"><span data-stu-id="fb424-145">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span></span>

8. <span data-ttu-id="fb424-146">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="fb424-146">Click **Save.**</span></span>

9. <span data-ttu-id="fb424-147">В разделе "Сопоставления" выберите **Synchronize Azure Active Directory Users to Jive** (Синхронизировать пользователей Azure Active Directory с Jive).</span><span class="sxs-lookup"><span data-stu-id="fb424-147">Under the Mappings section, select **Synchronize Azure Active Directory Users to Jive.**</span></span>

10. <span data-ttu-id="fb424-148">В разделе **Сопоставления атрибутов** просмотрите пользовательские атрибуты, которые синхронизированы из Azure AD в Jive.</span><span class="sxs-lookup"><span data-stu-id="fb424-148">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Jive.</span></span> <span data-ttu-id="fb424-149">Атрибуты, выбранные как свойства **Matching**, используются для сопоставления учетных записей пользователей в Jive для операций обновления.</span><span class="sxs-lookup"><span data-stu-id="fb424-149">The attributes selected as **Matching** properties are used to match the user accounts in Jive for update operations.</span></span> <span data-ttu-id="fb424-150">Нажмите кнопку "Сохранить", чтобы подтвердить все изменения.</span><span class="sxs-lookup"><span data-stu-id="fb424-150">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="fb424-151">Чтобы включить службу подготовки Azure AD для Jive, в разделе "Параметры" измените значение параметра **Состояние подготовки** на **Включено**.</span><span class="sxs-lookup"><span data-stu-id="fb424-151">To enable the Azure AD provisioning service for Jive, change the **Provisioning Status** to **On** in the Settings section</span></span>

12. <span data-ttu-id="fb424-152">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="fb424-152">Click **Save.**</span></span>

<span data-ttu-id="fb424-153">После этого будет запущена начальная синхронизация всех пользователей и групп, назначенных для Jive в разделе "Пользователи и группы".</span><span class="sxs-lookup"><span data-stu-id="fb424-153">It starts the initial synchronization of any users and/or groups assigned to Jive in the Users and Groups section.</span></span> <span data-ttu-id="fb424-154">Начальная синхронизация занимает больше времени, чем последующие операции синхронизации. Последующие операции синхронизации выполняются примерно каждые 20 минут, при условии, что служба запущена.</span><span class="sxs-lookup"><span data-stu-id="fb424-154">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="fb424-155">В разделе **Сведения о синхронизации** можно отслеживать ход выполнения и переходить по ссылкам для просмотра отчетов по подготовке, в которых зафиксированы все действия, выполняемые с приложением Jive службой подготовки.</span><span class="sxs-lookup"><span data-stu-id="fb424-155">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Jive app.</span></span>

<span data-ttu-id="fb424-156">Теперь можно создать тестовую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="fb424-156">You can now create a test account.</span></span> <span data-ttu-id="fb424-157">Подождите примерно 20 минут, чтобы убедиться, что учетная запись синхронизирована с Jive.</span><span class="sxs-lookup"><span data-stu-id="fb424-157">Wait for up to 20 minutes to verify that the account has been synchronized to Jive.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fb424-158">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="fb424-158">Additional resources</span></span>

* [<span data-ttu-id="fb424-159">Управление подготовкой учетных записей пользователей для корпоративных приложений</span><span class="sxs-lookup"><span data-stu-id="fb424-159">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fb424-160">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fb424-160">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="fb424-161">Настройка единого входа</span><span class="sxs-lookup"><span data-stu-id="fb424-161">Configure Single Sign-on</span></span>](active-directory-saas-jive-tutorial.md)