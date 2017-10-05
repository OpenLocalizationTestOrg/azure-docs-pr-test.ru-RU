---
title: "Руководство по интеграции Azure Active Directory с Citrix GoToMeeting | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Citrix GoToMeeting."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f59fedb-2cf8-48d2-a5fb-222ed943ff78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 1ddfcd991431a11e5c3e306bd5905003d094ac18
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-citrix-gotomeeting-for-automatic-user-provisioning"></a><span data-ttu-id="85c76-103">Руководство по настройке Citrix GoToMeeting для автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="85c76-103">Tutorial: Configuring Citrix GoToMeeting for Automatic User Provisioning</span></span>

<span data-ttu-id="85c76-104">Цель этого руководства — показать, как настроить автоматическую подготовку и отмену подготовки учетных записей пользователей Azure AD в Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="85c76-104">The objective of this tutorial is to show you the steps you need to perform in Citrix GoToMeeting and Azure AD to automatically provision and de-provision user accounts from Azure AD to Citrix GoToMeeting.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="85c76-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="85c76-105">Prerequisites</span></span>

<span data-ttu-id="85c76-106">Сценарий, описанный в этом учебнике, предполагает, что у вас уже имеется:</span><span class="sxs-lookup"><span data-stu-id="85c76-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="85c76-107">клиент Azure Active Directory;</span><span class="sxs-lookup"><span data-stu-id="85c76-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="85c76-108">подписка Citrix GoToMeeting с поддержкой единого входа;</span><span class="sxs-lookup"><span data-stu-id="85c76-108">A Citrix GoToMeeting single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="85c76-109">учетная запись пользователя в Citrix GoToMeeting с разрешениями администратора группы.</span><span class="sxs-lookup"><span data-stu-id="85c76-109">A user account in Citrix GoToMeeting with Team Admin permissions.</span></span>

## <a name="assigning-users-to-citrix-gotomeeting"></a><span data-ttu-id="85c76-110">Назначение пользователей в Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="85c76-110">Assigning users to Citrix GoToMeeting</span></span>

<span data-ttu-id="85c76-111">В Azure Active Directory для определения того, какие пользователи должны получать доступ к выбранным приложениям, используется концепция, называемая "назначение".</span><span class="sxs-lookup"><span data-stu-id="85c76-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="85c76-112">В контексте автоматической подготовки учетной записи будут синхронизированы только те записи и группы, которые были "назначены" приложению в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="85c76-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="85c76-113">Перед настройкой и включением службы подготовки необходимо решить, какие пользователи или группы в Azure AD представляют пользователей, которым требуется доступ к приложению Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="85c76-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Citrix GoToMeeting app.</span></span> <span data-ttu-id="85c76-114">После этого можно назначить этих пользователей для приложения Citrix GoToMeeting, выполнив следующие действия:</span><span class="sxs-lookup"><span data-stu-id="85c76-114">Once decided, you can assign these users to your Citrix GoToMeeting app by following the instructions here:</span></span>

[<span data-ttu-id="85c76-115">Назначение корпоративному приложению пользователя или группы</span><span class="sxs-lookup"><span data-stu-id="85c76-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-citrix-gotomeeting"></a><span data-ttu-id="85c76-116">Важные рекомендации по назначению пользователей для приложения Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="85c76-116">Important tips for assigning users to Citrix GoToMeeting</span></span>

*   <span data-ttu-id="85c76-117">Рекомендуется назначить одного пользователя Azure AD в Citrix GoToMeeting для тестирования конфигурации подготовки.</span><span class="sxs-lookup"><span data-stu-id="85c76-117">It is recommended that a single Azure AD user is assigned to Citrix GoToMeeting to test the provisioning configuration.</span></span> <span data-ttu-id="85c76-118">Дополнительные пользователи и/или группы можно назначить позднее.</span><span class="sxs-lookup"><span data-stu-id="85c76-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="85c76-119">При назначении пользователя для Citrix GoToMeeting необходимо выбрать допустимую роль пользователя.</span><span class="sxs-lookup"><span data-stu-id="85c76-119">When assigning a user to Citrix GoToMeeting, you must select a valid user role.</span></span> <span data-ttu-id="85c76-120">Роль "Доступ по умолчанию" не работает для подготовки.</span><span class="sxs-lookup"><span data-stu-id="85c76-120">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="85c76-121">Включение автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="85c76-121">Enable Automated User Provisioning</span></span>

<span data-ttu-id="85c76-122">В этом разделе описывается подключение к API подготовки учетной записи пользователя Azure AD в Citrix GoToMeeting и настройка подготовки службы для создания, обновления и отмены назначения учетных записей пользователей в Citrix GoToMeeting на основе назначения пользователей и групп в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="85c76-122">This section guides you through connecting your Azure AD to Citrix GoToMeeting's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Citrix GoToMeeting based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="85c76-123">Для Citrix GoToMeeting также можно включить единый вход на основе SAML. Для этого следуйте инструкциям, приведенным на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="85c76-123">You may also choose to enabled SAML-based Single Sign-On for Citrix GoToMeeting, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="85c76-124">Единый вход можно настроить независимо от автоматической подготовки, хотя эти две возможности дополняют друг друга.</span><span class="sxs-lookup"><span data-stu-id="85c76-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-automatic-user-account-provisioning"></a><span data-ttu-id="85c76-125">Настройка автоматической подготовки учетных записей пользователей:</span><span class="sxs-lookup"><span data-stu-id="85c76-125">To configure automatic user account provisioning:</span></span>

1. <span data-ttu-id="85c76-126">На [портале Azure](https://portal.azure.com) перейдите в раздел **Azure Active Directory > Корпоративные приложения > Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="85c76-126">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="85c76-127">Если вы уже настроили единый вход для Citrix GoToMeeting, найдите свой экземпляр Citrix GoToMeeting с помощью поиска.</span><span class="sxs-lookup"><span data-stu-id="85c76-127">If you have already configured Citrix GoToMeeting for single sign-on, search for your instance of Citrix GoToMeeting using the search field.</span></span> <span data-ttu-id="85c76-128">В противном случае щелкните **Добавить** и найдите **Citrix GoToMeeting** в коллекции приложений.</span><span class="sxs-lookup"><span data-stu-id="85c76-128">Otherwise, select **Add** and search for **Citrix GoToMeeting** in the application gallery.</span></span> <span data-ttu-id="85c76-129">Выберите Citrix GoToMeeting в результатах поиска и добавьте это приложение в свой список приложений.</span><span class="sxs-lookup"><span data-stu-id="85c76-129">Select Citrix GoToMeeting from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="85c76-130">Выберите свой экземпляр Citrix GoToMeeting и перейдите на вкладку **Подготовка**.</span><span class="sxs-lookup"><span data-stu-id="85c76-130">Select your instance of Citrix GoToMeeting, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="85c76-131">Для параметра **Режим подготовки** выберите значение **Автоматический**.</span><span class="sxs-lookup"><span data-stu-id="85c76-131">Set the **Provisioning** Mode to **Automatic**.</span></span> 

    ![подготовка](./media/active-directory-saas-citrixgotomeeting-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="85c76-133">В разделе "Учетные данные администратора" выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="85c76-133">Under the Admin Credentials section, perform the following steps:</span></span>
   
    <span data-ttu-id="85c76-134">а.</span><span class="sxs-lookup"><span data-stu-id="85c76-134">a.</span></span> <span data-ttu-id="85c76-135">В текстовом поле **Имя пользователя администратора Citrix GoToMeeting** введите имя пользователя администратора.</span><span class="sxs-lookup"><span data-stu-id="85c76-135">In the **Citrix GoToMeeting Admin User Name** textbox, type the user name of an administrator.</span></span>

    <span data-ttu-id="85c76-136">b.</span><span class="sxs-lookup"><span data-stu-id="85c76-136">b.</span></span> <span data-ttu-id="85c76-137">В текстовом поле **Пароль администратора Citrix GoToMeeting** введите пароль администратора.</span><span class="sxs-lookup"><span data-stu-id="85c76-137">In the **Citrix GoToMeeting Admin Password** textbox, the administrator's password.</span></span>

6. <span data-ttu-id="85c76-138">На портале Azure щелкните **Проверить подключение**, чтобы убедиться, что Azure AD может подключиться к приложению Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="85c76-138">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Citrix GoToMeeting app.</span></span> <span data-ttu-id="85c76-139">Если подключение отсутствует, убедитесь, что у учетной записи Citrix GoToMeeting есть права администратора группы, и повторите шаг **"Учетные данные администратора"**.</span><span class="sxs-lookup"><span data-stu-id="85c76-139">If the connection fails, ensure your Citrix GoToMeeting account has Team Admin permissions and try the **"Admin Credentials"** step again.</span></span>

7. <span data-ttu-id="85c76-140">В поле **Почтовое уведомление** введите адрес электронной почты пользователя или группы, которые должны получать уведомления об ошибках подготовки, а также установите флажок.</span><span class="sxs-lookup"><span data-stu-id="85c76-140">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

8. <span data-ttu-id="85c76-141">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="85c76-141">Click **Save.**</span></span>

9. <span data-ttu-id="85c76-142">В разделе "Сопоставления" выберите **Синхронизировать пользователей Azure Active Directory с Citrix GoToMeeting**.</span><span class="sxs-lookup"><span data-stu-id="85c76-142">Under the Mappings section, select **Synchronize Azure Active Directory Users to Citrix GoToMeeting.**</span></span>

10. <span data-ttu-id="85c76-143">В разделе **Сопоставления атрибутов** просмотрите пользовательские атрибуты, которые синхронизируются из Azure AD в Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="85c76-143">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Citrix GoToMeeting.</span></span> <span data-ttu-id="85c76-144">Атрибуты, выбранные как свойства **сопоставления**, используются для сопоставления учетных записей пользователей в Citrix GoToMeeting для операций обновления.</span><span class="sxs-lookup"><span data-stu-id="85c76-144">The attributes selected as **Matching** properties are used to match the user accounts in Citrix GoToMeeting for update operations.</span></span> <span data-ttu-id="85c76-145">Нажмите кнопку "Сохранить", чтобы подтвердить все изменения.</span><span class="sxs-lookup"><span data-stu-id="85c76-145">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="85c76-146">Чтобы включить службу подготовки Azure AD для Citrix GoToMeeting, в разделе "Параметры" установите переключатель **Состояние подготовки** в положение **Включено**.</span><span class="sxs-lookup"><span data-stu-id="85c76-146">To enable the Azure AD provisioning service for Citrix GoToMeeting, change the **Provisioning Status** to **On** in the Settings section</span></span>

12. <span data-ttu-id="85c76-147">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="85c76-147">Click **Save.**</span></span>

<span data-ttu-id="85c76-148">После этого будет запущена начальная синхронизация всех пользователей и групп, назначенных в Citrix GoToMeeting в разделе "Пользователи и группы".</span><span class="sxs-lookup"><span data-stu-id="85c76-148">It starts the initial synchronization of any users and/or groups assigned to Citrix GoToMeeting in the Users and Groups section.</span></span> <span data-ttu-id="85c76-149">Начальная синхронизация занимает больше времени, чем последующие операции синхронизации. Последующие операции синхронизации выполняются примерно каждые 20 минут, при условии, что служба запущена.</span><span class="sxs-lookup"><span data-stu-id="85c76-149">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="85c76-150">В разделе **Сведения о синхронизации** можно отслеживать ход синхронизации и с помощью ссылок просматривать отчеты по подготовке, в которых описаны все действия, выполняемые службой подготовки для Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="85c76-150">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Citrix GoToMeeting app.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="85c76-151">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="85c76-151">Additional resources</span></span>

* [<span data-ttu-id="85c76-152">Управление подготовкой учетных записей пользователей для корпоративных приложений</span><span class="sxs-lookup"><span data-stu-id="85c76-152">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="85c76-153">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="85c76-153">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="85c76-154">Настройка единого входа</span><span class="sxs-lookup"><span data-stu-id="85c76-154">Configure Single Sign-on</span></span>](active-directory-saas-citrix-gotomeeting-tutorial.md)


