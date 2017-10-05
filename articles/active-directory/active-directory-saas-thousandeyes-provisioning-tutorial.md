---
title: "Руководство по настройке ThousandEyes для автоматической подготовки пользователей с помощью Azure Active Directory | Документация Майкрософт"
description: "Узнайте, как настроить Azure Active Directory для автоматической подготовки и отзыва учетных записей пользователей в ThousandEyes."
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
ms.openlocfilehash: e6bc2eab3cc1adcf26857ed98d920177a51455ea
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-configuring-thousandeyes-for-automatic-user-provisioning"></a><span data-ttu-id="04c02-103">Руководство по настройке ThousandEyes для автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="04c02-103">Tutorial: Configuring ThousandEyes for Automatic User Provisioning</span></span>


<span data-ttu-id="04c02-104">Цель этого руководства — показать, как в ThousandEyes и Azure AD настроить автоматическую подготовку и отзыв учетных записей пользователей из Azure AD в ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="04c02-104">The objective of this tutorial is to show you the steps you need to perform in ThousandEyes and Azure AD to automatically provision and de-provision user accounts from Azure AD to ThousandEyes.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="04c02-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="04c02-105">Prerequisites</span></span>

<span data-ttu-id="04c02-106">Сценарий, описанный в этом учебнике, предполагает, что у вас уже имеется:</span><span class="sxs-lookup"><span data-stu-id="04c02-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="04c02-107">клиент Azure Active Directory;</span><span class="sxs-lookup"><span data-stu-id="04c02-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="04c02-108">клиент ThousandEyes с [планом Standard](https://www.thousandeyes.com/pricing) или выше;</span><span class="sxs-lookup"><span data-stu-id="04c02-108">A ThousandEyes tenant with the [Standard plan](https://www.thousandeyes.com/pricing) or better enabled</span></span> 
*   <span data-ttu-id="04c02-109">учетная запись пользователя ThousandEyes с разрешениями администратора.</span><span class="sxs-lookup"><span data-stu-id="04c02-109">A user account in ThousandEyes with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="04c02-110">Интеграция подготовки в Azure AD зависит от [API SCIM ThousandEyes](https://success.thousandeyes.com/PublicArticlePage?articleIdParam=kA044000000CnWrCAK), доступного для команд ThousandEyes, использующих план Standard или выше.</span><span class="sxs-lookup"><span data-stu-id="04c02-110">The Azure AD provisioning integration relies on the [ThousandEyes SCIM API](https://success.thousandeyes.com/PublicArticlePage?articleIdParam=kA044000000CnWrCAK), which is available to ThousandEyes teams on the Standard plan or better.</span></span>

## <a name="assigning-users-to-thousandeyes"></a><span data-ttu-id="04c02-111">Назначение пользователей в ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="04c02-111">Assigning users to ThousandEyes</span></span>

<span data-ttu-id="04c02-112">В Azure Active Directory для определения того, какие пользователи должны получать доступ к выбранным приложениям, используется концепция, называемая "назначение".</span><span class="sxs-lookup"><span data-stu-id="04c02-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="04c02-113">В контексте автоматической подготовки учетной записи будут синхронизированы только те записи и группы, которые были "назначены" приложению в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="04c02-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="04c02-114">Перед настройкой и включением службы подготовки необходимо решить, какие пользователи или группы в Azure AD представляют пользователей, которым требуется доступ к приложению ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="04c02-114">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your ThousandEyes app.</span></span> <span data-ttu-id="04c02-115">Приняв это решение, можно будет назначить этих пользователей для приложения ThousandEyes, выполнив следующие действия.</span><span class="sxs-lookup"><span data-stu-id="04c02-115">Once decided, you can assign these users to your ThousandEyes app by following the instructions here:</span></span>

[<span data-ttu-id="04c02-116">Назначение корпоративному приложению пользователя или группы</span><span class="sxs-lookup"><span data-stu-id="04c02-116">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-thousandeyes"></a><span data-ttu-id="04c02-117">Важные советы по назначению пользователей в ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="04c02-117">Important tips for assigning users to ThousandEyes</span></span>

*   <span data-ttu-id="04c02-118">Рекомендуется назначить одного пользователя Azure AD в ThousandEyes для тестирования конфигурации подготовки.</span><span class="sxs-lookup"><span data-stu-id="04c02-118">It is recommended that a single Azure AD user is assigned to ThousandEyes to test the provisioning configuration.</span></span> <span data-ttu-id="04c02-119">Дополнительные пользователи и/или группы можно назначить позднее.</span><span class="sxs-lookup"><span data-stu-id="04c02-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="04c02-120">При назначении пользователя в ThousandEyes в диалоговом окне назначения необходимо выбрать роль **пользователя** или другую действительную роль для конкретного приложения (если доступно).</span><span class="sxs-lookup"><span data-stu-id="04c02-120">When assigning a user to ThousandEyes, you must select either the **User** role, or another valid application-specific role (if available) in the assignment dialog.</span></span> <span data-ttu-id="04c02-121">Роль **Доступ по умолчанию** не подходит для подготовки, и эти пользователи пропускаются.</span><span class="sxs-lookup"><span data-stu-id="04c02-121">The **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-to-thousandeyes"></a><span data-ttu-id="04c02-122">Настройка подготовки учетных записей пользователей в ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="04c02-122">Configuring user provisioning to ThousandEyes</span></span> 

<span data-ttu-id="04c02-123">В этом разделе описывается подключение вашего каталога Azure AD к API подготовки учетных записей пользователей в ThousandEyes и настройка службы подготовки для создания, обновления и отключения назначенных учетных записей пользователей в ThousandEyes на основе назначения пользователей и групп в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="04c02-123">This section guides you through connecting your Azure AD to ThousandEyes's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in ThousandEyes based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="04c02-124">Для ThousandEyes можно также включить единый вход на основе SAML. Для этого следуйте инструкциям на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="04c02-124">You may also choose to enabled SAML-based Single Sign-On for ThousandEyes, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="04c02-125">Единый вход можно настроить независимо от автоматической подготовки, хотя эти две возможности дополняют друг друга.</span><span class="sxs-lookup"><span data-stu-id="04c02-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-to-thousandeyes-in-azure-ad"></a><span data-ttu-id="04c02-126">Настройка автоматической подготовки учетных записей пользователей для ThousandEyes в Azure AD</span><span class="sxs-lookup"><span data-stu-id="04c02-126">Configure automatic user account provisioning to ThousandEyes in Azure AD</span></span>


1. <span data-ttu-id="04c02-127">На [портале Azure](https://portal.azure.com) перейдите в раздел **Azure Active Directory > Корпоративные приложения > Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="04c02-127">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="04c02-128">Если в ThousandEyes уже настроен единый вход, найдите свой экземпляр ThousandEyes с помощью поля поиска.</span><span class="sxs-lookup"><span data-stu-id="04c02-128">If you have already configured ThousandEyes for single sign-on, search for your instance of ThousandEyes using the search field.</span></span> <span data-ttu-id="04c02-129">В противном случае щелкните **Добавить** и выполните поиск **ThousandEyes** в коллекции приложений.</span><span class="sxs-lookup"><span data-stu-id="04c02-129">Otherwise, select **Add** and search for **ThousandEyes** in the application gallery.</span></span> <span data-ttu-id="04c02-130">Выберите ThousandEyes в результатах поиска и добавьте в список приложений.</span><span class="sxs-lookup"><span data-stu-id="04c02-130">Select ThousandEyes from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="04c02-131">Выберите экземпляр ThousandEyes, а затем перейдите на вкладку **Подготовка**.</span><span class="sxs-lookup"><span data-stu-id="04c02-131">Select your instance of ThousandEyes, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="04c02-132">Для параметра **Режим подготовки к работе** выберите значение **Automatic** (Автоматически).</span><span class="sxs-lookup"><span data-stu-id="04c02-132">Set the **Provisioning Mode** to **Automatic**.</span></span>

    ![Подготовка ThousandEyes](./media/active-directory-saas-thousandeyes-provisioning-tutorial/ThousandEyes1.png)

5. <span data-ttu-id="04c02-134">В разделе **Учетные данные администратора** введите **секретный токен**, созданный вашей учетной записью ThousandEyes (его можно найти в своей учетной записи ThousandEyes: **Security & Authentication** (Безопасность и аутентификация)).</span><span class="sxs-lookup"><span data-stu-id="04c02-134">Under the **Admin Credentials** section, input the **Secret Token** generated by your ThousandEyes's account (you can find the token under your ThousandEyes account: **Security & Authentication**).</span></span> 

    ![Подготовка ThousandEyes](./media/active-directory-saas-thousandeyes-provisioning-tutorial/ThousandEyes2.png)

6. <span data-ttu-id="04c02-136">На портале Azure щелкните **Проверить подключение**, чтобы убедиться, что Azure AD может подключиться к приложению ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="04c02-136">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your ThousandEyes app.</span></span> <span data-ttu-id="04c02-137">Если установить подключение не удалось, убедитесь, что у учетной записи ThousandEyes есть разрешения администратора, и повторите шаг 5.</span><span class="sxs-lookup"><span data-stu-id="04c02-137">If the connection fails, ensure your ThousandEyes account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="04c02-138">В поле **Почтовое уведомление** введите адрес электронной почты пользователя или группы, которые должны получать уведомления об ошибках подготовки, а также установите флажок "Отправить уведомление по электронной почте при сбое".</span><span class="sxs-lookup"><span data-stu-id="04c02-138">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="04c02-139">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="04c02-139">Click **Save**.</span></span> 

9. <span data-ttu-id="04c02-140">В разделе "Сопоставления" выберите **Synchronize Azure Active Directory Users to ThousandEyes** (Синхронизировать пользователей Azure Active Directory с ThousandEyes).</span><span class="sxs-lookup"><span data-stu-id="04c02-140">Under the Mappings section, select **Synchronize Azure Active Directory Users to ThousandEyes**.</span></span>

10. <span data-ttu-id="04c02-141">В разделе **Сопоставления атрибутов** просмотрите пользовательские атрибуты, которые синхронизированы из Azure AD в ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="04c02-141">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to ThousandEyes.</span></span> <span data-ttu-id="04c02-142">Атрибуты, выбранные как свойства **Matching**, используются для сопоставления учетных записей пользователей в ThousandEyes для операций обновления.</span><span class="sxs-lookup"><span data-stu-id="04c02-142">The attributes selected as **Matching** properties are used to match the user accounts in ThousandEyes for update operations.</span></span> <span data-ttu-id="04c02-143">Нажмите кнопку "Сохранить", чтобы подтвердить все изменения.</span><span class="sxs-lookup"><span data-stu-id="04c02-143">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="04c02-144">Чтобы включить службу подготовки Azure AD для ThousandEyes, измените значение параметра **Состояние подготовки** на **Включено** в разделе **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="04c02-144">To enable the Azure AD provisioning service for ThousandEyes, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

12. <span data-ttu-id="04c02-145">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="04c02-145">Click **Save**.</span></span> 

<span data-ttu-id="04c02-146">После этого начнется начальная синхронизация всех пользователей и (или) групп, назначенных в ThousandEyes в разделе "Пользователи и группы".</span><span class="sxs-lookup"><span data-stu-id="04c02-146">This operation starts the initial synchronization of any users and/or groups assigned to ThousandEyes in the Users and Groups section.</span></span> <span data-ttu-id="04c02-147">Начальная синхронизация занимает больше времени, чем последующие операции синхронизации. Последующие операции синхронизации выполняются примерно каждые 20 минут, при условии, что служба запущена.</span><span class="sxs-lookup"><span data-stu-id="04c02-147">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="04c02-148">В разделе **Сведения о синхронизации** можно отслеживать ход выполнения и переходить по ссылкам для просмотра отчетов о подготовке, в которых зафиксированы все действия, выполняемые службой подготовки.</span><span class="sxs-lookup"><span data-stu-id="04c02-148">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service.</span></span>

<span data-ttu-id="04c02-149">Дополнительные сведения о чтении журналов подготовки Azure AD см. в руководстве по [отчетам об автоматической подготовке учетных записей](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="04c02-149">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="04c02-150">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="04c02-150">Additional resources</span></span>

* [<span data-ttu-id="04c02-151">Управление подготовкой учетных записей пользователей для корпоративных приложений</span><span class="sxs-lookup"><span data-stu-id="04c02-151">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="04c02-152">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="04c02-152">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="04c02-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="04c02-153">Next steps</span></span>

* [<span data-ttu-id="04c02-154">Сведения о просмотре журналов и получении отчетов о действиях по подготовке</span><span class="sxs-lookup"><span data-stu-id="04c02-154">Learn how to review logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
