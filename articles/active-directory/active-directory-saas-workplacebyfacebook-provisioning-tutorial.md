---
title: "Руководство по интеграции Azure Active Directory с Workplace by Facebook | Документация Майкрософт"
description: "Сведения о настройке единого входа между Azure Active Directory и Workplace by Facebook."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6341e67e-8ce6-42dc-a4ea-7295904a53ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 9b22679c304248ed7ba7a6bd9eaf82b64f7143cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-workplace-by-facebook-for-user-provisioning"></a><span data-ttu-id="ff617-103">Руководство по настройке Workplace by Facebook для подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="ff617-103">Tutorial: Configuring Workplace by Facebook for User Provisioning</span></span>

<span data-ttu-id="ff617-104">Цель этого руководства — показать, как в Workplace by Facebook и Azure AD настроить автоматическую подготовку и отзыв учетных записей пользователей из Azure AD в Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="ff617-104">The objective of this tutorial is to show you the steps you need to perform in Workplace by Facebook and Azure AD to automatically provision and de-provision user accounts from Azure AD to Workplace by Facebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff617-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ff617-105">Prerequisites</span></span>

<span data-ttu-id="ff617-106">Чтобы настроить интеграцию Azure AD с Workplace by Facebook, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="ff617-106">To configure Azure AD integration with Workplace by Facebook, you need the following items:</span></span>

- <span data-ttu-id="ff617-107">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="ff617-107">An Azure AD subscription</span></span>
- <span data-ttu-id="ff617-108">подписка Workplace by Facebook с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="ff617-108">A Workplace by Facebook single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ff617-109">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="ff617-109">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ff617-110">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="ff617-110">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ff617-111">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="ff617-111">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ff617-112">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ff617-112">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="assigning-users-to-workplace-by-facebook"></a><span data-ttu-id="ff617-113">Назначение пользователей для Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="ff617-113">Assigning users to Workplace by Facebook</span></span>

<span data-ttu-id="ff617-114">В Azure Active Directory для определения того, какие пользователи должны получать доступ к выбранным приложениям, используется концепция, называемая "назначение".</span><span class="sxs-lookup"><span data-stu-id="ff617-114">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="ff617-115">В контексте автоматической подготовки учетной записи будут синхронизированы только те записи и группы, которые были "назначены" приложению в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ff617-115">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="ff617-116">Перед настройкой и включением службы подготовки необходимо решить, какие пользователи или группы в Azure AD представляют пользователей, которым требуется доступ к приложению Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="ff617-116">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Workplace by Facebook app.</span></span> <span data-ttu-id="ff617-117">Приняв это решение, можно будет назначить этих пользователей для приложения Workplace by Facebook, выполнив следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ff617-117">Once decided, you can assign these users to your Workplace by Facebook app by following the instructions here:</span></span>

[<span data-ttu-id="ff617-118">Назначение корпоративному приложению пользователя или группы</span><span class="sxs-lookup"><span data-stu-id="ff617-118">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-workplace-by-facebook"></a><span data-ttu-id="ff617-119">Важные советы по назначению пользователей в Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="ff617-119">Important tips for assigning users to Workplace by Facebook</span></span>

*   <span data-ttu-id="ff617-120">Рекомендуется назначить одного пользователя Azure AD в Workplace by Facebook для тестирования конфигурации подготовки.</span><span class="sxs-lookup"><span data-stu-id="ff617-120">It is recommended that a single Azure AD user is assigned to Workplace by Facebook to test the provisioning configuration.</span></span> <span data-ttu-id="ff617-121">Дополнительные пользователи и/или группы можно назначить позднее.</span><span class="sxs-lookup"><span data-stu-id="ff617-121">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="ff617-122">При назначении пользователя Workplace by Facebook необходимо выбрать допустимую роль пользователя.</span><span class="sxs-lookup"><span data-stu-id="ff617-122">When assigning a user to Workplace by Facebook, you must select a valid user role.</span></span> <span data-ttu-id="ff617-123">Роль "Доступ по умолчанию" не работает для подготовки.</span><span class="sxs-lookup"><span data-stu-id="ff617-123">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="ff617-124">Включение подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="ff617-124">Enable User Provisioning</span></span>

<span data-ttu-id="ff617-125">В этом разделе описывается подключение вашего каталога Azure AD к API подготовки учетных записей пользователей в Workplace by Facebook и настройка службы подготовки для создания, обновления и отключения назначенных учетных записей пользователей в Workplace by Facebook на основе назначения пользователей и групп в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ff617-125">This section guides you through connecting your Azure AD to Workplace by Facebook's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Workplace by Facebook based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="ff617-126">Для Workplace by Facebook можно также включить единый вход на основе SAML. Для этого следуйте инструкциям, приведенным на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ff617-126">You may also choose to enabled SAML-based Single Sign-On for Workplace by Facebook, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="ff617-127">Единый вход можно настроить независимо от автоматической подготовки, хотя эти две возможности дополняют друг друга.</span><span class="sxs-lookup"><span data-stu-id="ff617-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-user-account-provisioning-to-workplace-by-facebook-in-azure-ad"></a><span data-ttu-id="ff617-128">Настройка подготовки учетных записей пользователей в Workplace by Facebook в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff617-128">To configure user account provisioning to Workplace by Facebook in Azure AD:</span></span>

<span data-ttu-id="ff617-129">В этом разделе описано, как включить подготовку учетных записей пользователей Active Directory для Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="ff617-129">The objective of this section is to outline how to enable provisioning of Active Directory user accounts to Workplace by Facebook.</span></span>

<span data-ttu-id="ff617-130">Azure AD поддерживает автоматическую синхронизацию сведений об учетных записях назначенных пользователей с Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="ff617-130">Azure AD supports the ability to automatically synchronize the account details of assigned users to Workplace by Facebook.</span></span> <span data-ttu-id="ff617-131">Эта автоматическая синхронизация позволяет Workplace by Facebook получить данные, необходимые для авторизации доступа пользователя до первого входа пользователя в систему.</span><span class="sxs-lookup"><span data-stu-id="ff617-131">This automatic synchronization enables Workplace by Facebook to get the data it needs to authorize users for access, before them attempting to sign in for the first time.</span></span> <span data-ttu-id="ff617-132">Она также отменяет подготовку пользователей для Workplace by Facebook, если доступ для них отозван в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ff617-132">It also de-provisions users from Workplace by Facebook when access has been revoked in Azure AD.</span></span>

1. <span data-ttu-id="ff617-133">На [портале Azure](https://portal.azure.com) перейдите в раздел **Azure Active Directory** > **Корпоративные приложения** > **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ff617-133">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory** > **Enterprise Apps** > **All applications** section.</span></span>

2. <span data-ttu-id="ff617-134">Если в Workplace by Facebook уже настроен единый вход, найдите свой экземпляр Workplace by Facebook с помощью поля поиска.</span><span class="sxs-lookup"><span data-stu-id="ff617-134">If you have already configured Workplace by Facebook for single sign-on, search for your instance of Workplace by Facebook using the search field.</span></span> <span data-ttu-id="ff617-135">В противном случае щелкните **Добавить** и найдите **Workplace by Facebook** в коллекции приложений.</span><span class="sxs-lookup"><span data-stu-id="ff617-135">Otherwise, select **Add** and search for **Workplace by Facebook** in the application gallery.</span></span> <span data-ttu-id="ff617-136">Выберите Workplace by Facebook в результатах поиска и добавьте в список приложений.</span><span class="sxs-lookup"><span data-stu-id="ff617-136">Select Workplace by Facebook from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="ff617-137">Выберите экземпляр Workplace by Facebook, а затем перейдите на вкладку **Подготовка**.</span><span class="sxs-lookup"><span data-stu-id="ff617-137">Select your instance of Workplace by Facebook, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="ff617-138">Для параметра **Режим подготовки к работе** выберите значение **Automatic** (Автоматически).</span><span class="sxs-lookup"><span data-stu-id="ff617-138">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![подготовка](./media/active-directory-saas-workplacebyfacebook-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="ff617-140">В разделе **Учетные данные администратора** введите секретный токен и URL-адрес клиента администратора Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="ff617-140">Under the **Admin Credentials** section, enter the Secret Token and the Tenant URL of your Workplace by Facebook administrator.</span></span>

6. <span data-ttu-id="ff617-141">На портале Azure щелкните **Проверить подключение** и убедитесь, что Azure AD может подключиться к приложению Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="ff617-141">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Workplace by Facebook app.</span></span> <span data-ttu-id="ff617-142">Если подключение отсутствует, убедитесь, что у учетной записи Workplace by Facebook есть разрешения администратора команды.</span><span class="sxs-lookup"><span data-stu-id="ff617-142">If the connection fails, ensure your Workplace by Facebook account has Team Admin permissions.</span></span>

7. <span data-ttu-id="ff617-143">В поле **Почтовое уведомление** введите адрес электронной почты пользователя или группы, которые должны получать уведомления об ошибках подготовки, а также установите флажок.</span><span class="sxs-lookup"><span data-stu-id="ff617-143">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

8. <span data-ttu-id="ff617-144">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="ff617-144">Click **Save.**</span></span>

9. <span data-ttu-id="ff617-145">В разделе "Сопоставления" выберите **Synchronize Azure Active Directory Users to Workplace by Facebook** (Синхронизировать пользователей Azure Active Directory с Workplace by Facebook).</span><span class="sxs-lookup"><span data-stu-id="ff617-145">Under the Mappings section, select **Synchronize Azure Active Directory Users to Workplace by Facebook.**</span></span>

10. <span data-ttu-id="ff617-146">В разделе **Сопоставления атрибутов** просмотрите пользовательские атрибуты, которые синхронизированы из Azure AD в Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="ff617-146">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Workplace by Facebook.</span></span> <span data-ttu-id="ff617-147">Атрибуты, выбранные как свойства **Matching**, используются для сопоставления учетных записей пользователей в Workplace by Facebook для операций обновления.</span><span class="sxs-lookup"><span data-stu-id="ff617-147">The attributes selected as **Matching** properties are used to match the user accounts in Workplace by Facebook for update operations.</span></span> <span data-ttu-id="ff617-148">Нажмите кнопку "Сохранить", чтобы подтвердить все изменения.</span><span class="sxs-lookup"><span data-stu-id="ff617-148">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="ff617-149">Чтобы включить службу подготовки Azure AD для Workplace by Facebook, измените значение параметра **Состояние подготовки** на **Включено** в разделе **Настройки**.</span><span class="sxs-lookup"><span data-stu-id="ff617-149">To enable the Azure AD provisioning service for Workplace by Facebook, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

12. <span data-ttu-id="ff617-150">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="ff617-150">Click **Save.**</span></span>

<span data-ttu-id="ff617-151">Дополнительные сведения о настройке автоматической подготовки см. на странице [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers).</span><span class="sxs-lookup"><span data-stu-id="ff617-151">For more information on how to configure automatic provisioning, see [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)</span></span>

<span data-ttu-id="ff617-152">Теперь можно создать тестовую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="ff617-152">You can now create a test account.</span></span> <span data-ttu-id="ff617-153">Подождите примерно 20 минут, чтобы убедиться, что учетная запись была синхронизирована с Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="ff617-153">Wait for up to 20 minutes to verify that the account has been synchronized to Workplace by Facebook.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ff617-154">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ff617-154">Additional resources</span></span>

* [<span data-ttu-id="ff617-155">Управление подготовкой учетных записей пользователей для корпоративных приложений</span><span class="sxs-lookup"><span data-stu-id="ff617-155">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ff617-156">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ff617-156">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="ff617-157">Настройка единого входа</span><span class="sxs-lookup"><span data-stu-id="ff617-157">Configure Single Sign-on</span></span>](active-directory-saas-workplacebyfacebook-tutorial.md)

