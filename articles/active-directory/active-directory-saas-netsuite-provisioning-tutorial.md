---
title: "Руководство по интеграции Azure Active Directory с NetSuite | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Netsuite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8a6d3994-ee33-4a6f-b0a2-9d0389467f16
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 277c393536615fc8bfe8af0bc6d487115f04776c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-netsuite-for-automatic-user-provisioning"></a><span data-ttu-id="a502e-103">Руководство по настройке Netsuite для автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="a502e-103">Tutorial: Configuring Netsuite for Automatic User Provisioning</span></span>

<span data-ttu-id="a502e-104">Цель этого руководства — показать, как в Netsuite и Azure AD настроить автоматическую подготовку и отзыв учетных записей пользователей из Azure AD в Netsuite.</span><span class="sxs-lookup"><span data-stu-id="a502e-104">The objective of this tutorial is to show you the steps you need to perform in Netsuite and Azure AD to automatically provision and de-provision user accounts from Azure AD to Netsuite.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a502e-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a502e-105">Prerequisites</span></span>

<span data-ttu-id="a502e-106">Сценарий, описанный в этом учебнике, предполагает, что у вас уже имеется:</span><span class="sxs-lookup"><span data-stu-id="a502e-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="a502e-107">клиент Azure Active Directory;</span><span class="sxs-lookup"><span data-stu-id="a502e-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="a502e-108">подписка Netsuite с поддержкой единого входа;</span><span class="sxs-lookup"><span data-stu-id="a502e-108">A Netsuite single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="a502e-109">учетная запись пользователя в Netsuite с разрешениями администратора команды.</span><span class="sxs-lookup"><span data-stu-id="a502e-109">A user account in Netsuite with Team Admin permissions.</span></span>

## <a name="assigning-users-to-netsuite"></a><span data-ttu-id="a502e-110">Назначение пользователей в Netsuite</span><span class="sxs-lookup"><span data-stu-id="a502e-110">Assigning users to Netsuite</span></span>

<span data-ttu-id="a502e-111">В Azure Active Directory для определения того, какие пользователи должны получать доступ к выбранным приложениям, используется концепция, называемая "назначение".</span><span class="sxs-lookup"><span data-stu-id="a502e-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="a502e-112">В контексте автоматической подготовки учетной записи синхронизированы будут только те пользователи и группы, которые были "назначены" приложению в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a502e-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD are synchronized.</span></span>

<span data-ttu-id="a502e-113">Перед настройкой и включением службы подготовки необходимо решить, какие пользователи или группы в Azure AD представляют пользователей, которым требуется доступ к приложению Netsuite.</span><span class="sxs-lookup"><span data-stu-id="a502e-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Netsuite app.</span></span> <span data-ttu-id="a502e-114">Когда данное решение будет принято, можно будет назначить этих пользователей приложению Netsuite, следуя указаниям ниже.</span><span class="sxs-lookup"><span data-stu-id="a502e-114">Once decided, you can assign these users to your Netsuite app by following the instructions here:</span></span>

[<span data-ttu-id="a502e-115">Назначение корпоративному приложению пользователя или группы</span><span class="sxs-lookup"><span data-stu-id="a502e-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-netsuite"></a><span data-ttu-id="a502e-116">Важные советы по назначению пользователей в Netsuite</span><span class="sxs-lookup"><span data-stu-id="a502e-116">Important tips for assigning users to Netsuite</span></span>

*   <span data-ttu-id="a502e-117">Рекомендуется назначить одного пользователя Azure AD в Netsuite для тестирования конфигурации подготовки.</span><span class="sxs-lookup"><span data-stu-id="a502e-117">It is recommended that a single Azure AD user is assigned to Netsuite to test the provisioning configuration.</span></span> <span data-ttu-id="a502e-118">Дополнительные пользователи и/или группы можно назначить позднее.</span><span class="sxs-lookup"><span data-stu-id="a502e-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="a502e-119">При назначении пользователя Netsuite необходимо выбрать допустимую роль пользователя.</span><span class="sxs-lookup"><span data-stu-id="a502e-119">When assigning a user to Netsuite, you must select a valid user role.</span></span> <span data-ttu-id="a502e-120">Роль "Доступ по умолчанию" не работает для подготовки.</span><span class="sxs-lookup"><span data-stu-id="a502e-120">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="a502e-121">Включение подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="a502e-121">Enable User Provisioning</span></span>

<span data-ttu-id="a502e-122">В этом разделе описывается подключение вашего каталога Azure AD к API подготовки учетных записей пользователей в Netsuite и настройка службы подготовки для создания, обновления и отключения назначенных учетных записей пользователей в Netsuite на основе назначения пользователей и групп в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a502e-122">This section guides you through connecting your Azure AD to Netsuite's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Netsuite based on user and group assignment in Azure AD.</span></span>

> [!TIP] 
> <span data-ttu-id="a502e-123">Для Netsuite можно также включить единый вход на основе SAML. Для этого следуйте инструкциям на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a502e-123">You may also choose to enabled SAML-based Single Sign-On for Netsuite, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="a502e-124">Единый вход можно настроить независимо от автоматической подготовки, хотя эти две возможности дополняют друг друга.</span><span class="sxs-lookup"><span data-stu-id="a502e-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-user-account-provisioning"></a><span data-ttu-id="a502e-125">Настройка подготовки учетных записей пользователей</span><span class="sxs-lookup"><span data-stu-id="a502e-125">To configure user account provisioning:</span></span>

<span data-ttu-id="a502e-126">В этом разделе показано, как включить подготовку учетных записей пользователей Active Directory для Netsuite.</span><span class="sxs-lookup"><span data-stu-id="a502e-126">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Netsuite.</span></span>

1. <span data-ttu-id="a502e-127">На [портале Azure](https://portal.azure.com) перейдите в раздел **Azure Active Directory > Корпоративные приложения > Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a502e-127">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="a502e-128">Если в Netsuite уже настроен единый вход, найдите свой экземпляр Netsuite с помощью поля поиска.</span><span class="sxs-lookup"><span data-stu-id="a502e-128">If you have already configured Netsuite for single sign-on, search for your instance of Netsuite using the search field.</span></span> <span data-ttu-id="a502e-129">В противном случае щелкните **Добавить** и выполните поиск **Netsuite** в коллекции приложений.</span><span class="sxs-lookup"><span data-stu-id="a502e-129">Otherwise, select **Add** and search for **Netsuite** in the application gallery.</span></span> <span data-ttu-id="a502e-130">Выберите Netsuite в результатах поиска и добавьте в список приложений.</span><span class="sxs-lookup"><span data-stu-id="a502e-130">Select Netsuite from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="a502e-131">Выберите экземпляр Netsuite, а затем перейдите на вкладку **Подготовка**.</span><span class="sxs-lookup"><span data-stu-id="a502e-131">Select your instance of Netsuite, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="a502e-132">Для параметра **Режим подготовки к работе** выберите значение **Automatic** (Автоматически).</span><span class="sxs-lookup"><span data-stu-id="a502e-132">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![Подготовка](./media/active-directory-saas-netsuite-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="a502e-134">В разделе **Учетные данные администратора** укажите следующие параметры конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a502e-134">Under the **Admin Credentials** section, provide the following configuration settings:</span></span>
   
    <span data-ttu-id="a502e-135">а.</span><span class="sxs-lookup"><span data-stu-id="a502e-135">a.</span></span> <span data-ttu-id="a502e-136">В текстовом поле **Имя пользователя администратора** введите имя учетной записи Netsuite, которой на сайте Netsuite.com назначен профиль **System Administrator** (Системный администратор).</span><span class="sxs-lookup"><span data-stu-id="a502e-136">In the **Admin User Name** textbox, type a Netsuite account name that has the **System Administrator** profile in Netsuite.com assigned.</span></span>
   
    <span data-ttu-id="a502e-137">b.</span><span class="sxs-lookup"><span data-stu-id="a502e-137">b.</span></span> <span data-ttu-id="a502e-138">В текстовом поле **Пароль администратора** введите пароль для этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="a502e-138">In the **Admin Password** textbox, type the password for this account.</span></span>
      
6. <span data-ttu-id="a502e-139">На портале Azure щелкните **Проверить подключение**, чтобы убедиться, что Azure AD может подключиться к приложению Netsuite.</span><span class="sxs-lookup"><span data-stu-id="a502e-139">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Netsuite app.</span></span>

7. <span data-ttu-id="a502e-140">В поле **Почтовое уведомление** введите адрес электронной почты пользователя или группы, которые должны получать уведомления об ошибках подготовки, а также установите флажок.</span><span class="sxs-lookup"><span data-stu-id="a502e-140">In the **Notification Email** field, enter the email address of a person or group who should receive provisioning error notifications, and check the checkbox.</span></span>

8. <span data-ttu-id="a502e-141">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="a502e-141">Click **Save.**</span></span>

9. <span data-ttu-id="a502e-142">В разделе "Сопоставления" выберите **Synchronize Azure Active Directory Users to Netsuite** (Синхронизировать пользователей Azure Active Directory с Netsuite).</span><span class="sxs-lookup"><span data-stu-id="a502e-142">Under the Mappings section, select **Synchronize Azure Active Directory Users to Netsuite.**</span></span>

10. <span data-ttu-id="a502e-143">В разделе **Сопоставления атрибутов** просмотрите пользовательские атрибуты, которые синхронизированы из Azure AD в Netsuite.</span><span class="sxs-lookup"><span data-stu-id="a502e-143">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Netsuite.</span></span> <span data-ttu-id="a502e-144">Обратите внимание, что атрибуты, выбранные как свойства **Matching**, используются для сопоставления учетных записей пользователей в Netsuite для операций обновления.</span><span class="sxs-lookup"><span data-stu-id="a502e-144">Note that the attributes selected as **Matching** properties are used to match the user accounts in Netsuite for update operations.</span></span> <span data-ttu-id="a502e-145">Нажмите кнопку "Сохранить", чтобы подтвердить все изменения.</span><span class="sxs-lookup"><span data-stu-id="a502e-145">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="a502e-146">Чтобы включить службу подготовки Azure AD для Netsuite, измените значение параметра **Состояние подготовки** на **Включено** в разделе "Параметры".</span><span class="sxs-lookup"><span data-stu-id="a502e-146">To enable the Azure AD provisioning service for Netsuite, change the **Provisioning Status** to **On** in the Settings section</span></span>

12. <span data-ttu-id="a502e-147">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="a502e-147">Click **Save.**</span></span>

<span data-ttu-id="a502e-148">После этого будет запущена начальная синхронизация всех пользователей и групп, назначенных для Netsuite в разделе "Пользователи и группы".</span><span class="sxs-lookup"><span data-stu-id="a502e-148">It starts the initial synchronization of any users and/or groups assigned to Netsuite in the Users and Groups section.</span></span> <span data-ttu-id="a502e-149">Обратите внимание, что начальная синхронизация занимает больше времени, чем последующие операции синхронизации. Последующие операции синхронизации выполняются примерно каждые 20 минут, при условии, что служба запущена.</span><span class="sxs-lookup"><span data-stu-id="a502e-149">Note that the initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="a502e-150">В разделе **Сведения о синхронизации** можно отслеживать ход выполнения и переходить по ссылкам для просмотра отчетов по подготовке, в которых зафиксированы все действия, выполняемые с приложением Netsuite службой подготовки.</span><span class="sxs-lookup"><span data-stu-id="a502e-150">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Netsuite app.</span></span>

<span data-ttu-id="a502e-151">Теперь можно создать тестовую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="a502e-151">You can now create a test account.</span></span> <span data-ttu-id="a502e-152">Подождите примерно 20 минут, чтобы убедиться, что учетная запись синхронизирована с Netsuite.</span><span class="sxs-lookup"><span data-stu-id="a502e-152">Wait for up to 20 minutes to verify that the account has been synchronized to Netsuite.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a502e-153">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="a502e-153">Additional resources</span></span>

* [<span data-ttu-id="a502e-154">Управление подготовкой учетных записей пользователей для корпоративных приложений</span><span class="sxs-lookup"><span data-stu-id="a502e-154">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a502e-155">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a502e-155">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="a502e-156">Настройка единого входа</span><span class="sxs-lookup"><span data-stu-id="a502e-156">Configure Single Sign-on</span></span>](active-directory-saas-netsuite-tutorial.md)