---
title: "Руководство по настройке ZenDesk для автоматической подготовки пользователей с помощью Azure Active Directory | Документация Майкрософт"
description: "Узнайте, как настроить Azure Active Directory для автоматической подготовки и отзыва учетных записей пользователей в ZenDesk."
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
ms.openlocfilehash: 1a1414eefd20e6d7c025da08cfd5ae7c45daad33
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-configuring-zendesk-for-automatic-user-provisioning"></a><span data-ttu-id="5ec19-103">Руководство по настройке ZenDesk для автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="5ec19-103">Tutorial: Configuring ZenDesk for Automatic User Provisioning</span></span>


<span data-ttu-id="5ec19-104">Цель этого руководства — показать, как в ZenDesk и Azure AD настроить автоматическую подготовку и отзыв учетных записей пользователей из Azure AD в ZenDesk.</span><span class="sxs-lookup"><span data-stu-id="5ec19-104">The objective of this tutorial is to show you the steps you need to perform in ZenDesk and Azure AD to automatically provision and de-provision user accounts from Azure AD to ZenDesk.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="5ec19-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5ec19-105">Prerequisites</span></span>

<span data-ttu-id="5ec19-106">Сценарий, описанный в этом учебнике, предполагает, что у вас уже имеется:</span><span class="sxs-lookup"><span data-stu-id="5ec19-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="5ec19-107">клиент Azure Active Directory;</span><span class="sxs-lookup"><span data-stu-id="5ec19-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="5ec19-108">клиент ZenDesk с [планом Enterprise](https://www.zendesk.com/product/pricing/) или выше;</span><span class="sxs-lookup"><span data-stu-id="5ec19-108">A ZenDesk tenant with the [Enterprise plan](https://www.zendesk.com/product/pricing/) or better enabled</span></span> 
*   <span data-ttu-id="5ec19-109">учетная запись пользователя в ZenDesk с разрешениями администратора.</span><span class="sxs-lookup"><span data-stu-id="5ec19-109">A user account in ZenDesk with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="5ec19-110">Интеграция подготовки Azure AD зависит от [API SCIM ZenDesk](https://developer.zendesk.com/rest_api/docs/core/introduction#the-api), доступного для групп ZenDesk, использующих план Essential или выше.</span><span class="sxs-lookup"><span data-stu-id="5ec19-110">The Azure AD provisioning integration relies on the [ZenDesk REST API](https://developer.zendesk.com/rest_api/docs/core/introduction#the-api), which is available to ZenDesk teams on the Essential plan or better.</span></span>

## <a name="assigning-users-to-zendesk"></a><span data-ttu-id="5ec19-111">Назначение пользователей в ZenDesk</span><span class="sxs-lookup"><span data-stu-id="5ec19-111">Assigning users to ZenDesk</span></span>

<span data-ttu-id="5ec19-112">В Azure Active Directory для определения того, какие пользователи должны получать доступ к выбранным приложениям, используется концепция, называемая "назначение".</span><span class="sxs-lookup"><span data-stu-id="5ec19-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="5ec19-113">В контексте автоматической подготовки учетной записи синхронизированы будут только те пользователи и группы, которые были "назначены" приложению в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5ec19-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD are synchronized.</span></span> 

<span data-ttu-id="5ec19-114">Перед настройкой и включением службы подготовки необходимо решить, какие пользователи или группы в Azure AD представляют пользователей, которым требуется доступ к приложению ZenDesk.</span><span class="sxs-lookup"><span data-stu-id="5ec19-114">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your ZenDesk app.</span></span> <span data-ttu-id="5ec19-115">Когда данное решение будет принято, можно будет назначить этих пользователей приложению ZenDesk, следуя указаниям ниже.</span><span class="sxs-lookup"><span data-stu-id="5ec19-115">Once decided, you can assign these users to your ZenDesk app by following the instructions here:</span></span>

[<span data-ttu-id="5ec19-116">Назначение корпоративному приложению пользователя или группы</span><span class="sxs-lookup"><span data-stu-id="5ec19-116">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-zendesk"></a><span data-ttu-id="5ec19-117">Важные советы по назначению пользователей в ZenDesk</span><span class="sxs-lookup"><span data-stu-id="5ec19-117">Important tips for assigning users to ZenDesk</span></span>

*   <span data-ttu-id="5ec19-118">Рекомендуется назначить одного пользователя Azure AD в ZenDesk для тестирования конфигурации подготовки.</span><span class="sxs-lookup"><span data-stu-id="5ec19-118">It is recommended that a single Azure AD user is assigned to ZenDesk to test the provisioning configuration.</span></span> <span data-ttu-id="5ec19-119">Дополнительные пользователи и/или группы можно назначить позднее.</span><span class="sxs-lookup"><span data-stu-id="5ec19-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="5ec19-120">При назначении пользователя в ZenDesk в диалоговом окне назначения необходимо выбрать роль **пользователя** или другую действительную роль для конкретного приложения (если доступно).</span><span class="sxs-lookup"><span data-stu-id="5ec19-120">When assigning a user to ZenDesk, you must select either the **User** role, or another valid application-specific role (if available) in the assignment dialog.</span></span> <span data-ttu-id="5ec19-121">Роль **Доступ по умолчанию** не подходит для подготовки, и эти пользователи пропускаются.</span><span class="sxs-lookup"><span data-stu-id="5ec19-121">The **Default Access** role does not work for provisioning, and these users are skipped.</span></span>

> [!NOTE]
> <span data-ttu-id="5ec19-122">В качестве дополнительной возможности служба подготовки считывает все пользовательские роли, определенные в ZenDesk, и импортирует их в Azure AD, где они могут быть выбраны в диалоговом окне "Выбор роли".</span><span class="sxs-lookup"><span data-stu-id="5ec19-122">As an added feature, the provisioning service reads any custom roles defined in Zendesk, and imports them into Azure AD where they can be selected in the Select Role dialog.</span></span> <span data-ttu-id="5ec19-123">Эти роли будут доступны на портале Azure после включения службы подготовки и выполнения одного цикла синхронизации.</span><span class="sxs-lookup"><span data-stu-id="5ec19-123">These roles will be visible in the Azure portal after the provisioning service is enabled and one synchronization cycle has completed.</span></span>

## <a name="configuring-user-provisioning-to-zendesk"></a><span data-ttu-id="5ec19-124">Настройка подготовки учетных записей пользователей в ZenDesk</span><span class="sxs-lookup"><span data-stu-id="5ec19-124">Configuring user provisioning to ZenDesk</span></span> 

<span data-ttu-id="5ec19-125">В этом разделе описывается подключение вашего каталога Azure AD к API подготовки учетных записей пользователей в ZenDesk и настройка службы подготовки для создания, обновления и отключения назначенных учетных записей пользователей в ZenDesk на основе назначения пользователей и групп в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5ec19-125">This section guides you through connecting your Azure AD to ZenDesk's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in ZenDesk based on user and group assignment in Azure AD.</span></span>

> [!TIP] 
> <span data-ttu-id="5ec19-126">Для ZenDesk можно также включить единый вход на базе управления лицензиями. Для этого следуйте инструкциям, указанным на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5ec19-126">You may also choose to enabled SAML-based Single Sign-On for ZenDesk, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="5ec19-127">Единый вход можно настроить независимо от автоматической подготовки, хотя эти две возможности дополняют друг друга.</span><span class="sxs-lookup"><span data-stu-id="5ec19-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-to-zendesk-in-azure-ad"></a><span data-ttu-id="5ec19-128">Настройка автоматической подготовки учетных записей пользователей для ZenDesk в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ec19-128">Configure automatic user account provisioning to ZenDesk in Azure AD</span></span>


1. <span data-ttu-id="5ec19-129">На [портале Azure](https://portal.azure.com) перейдите в раздел **Azure Active Directory > Корпоративные приложения > Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="5ec19-129">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="5ec19-130">Если в ZenDesk уже настроен единый вход, найдите свой экземпляр ZenDesk с помощью поля поиска.</span><span class="sxs-lookup"><span data-stu-id="5ec19-130">If you have already configured ZenDesk for single sign-on, search for your instance of ZenDesk using the search field.</span></span> <span data-ttu-id="5ec19-131">В противном случае щелкните **Добавить** и выполните поиск **ZenDesk** в коллекции приложений.</span><span class="sxs-lookup"><span data-stu-id="5ec19-131">Otherwise, select **Add** and search for **ZenDesk** in the application gallery.</span></span> <span data-ttu-id="5ec19-132">Выберите ZenDesk в результатах поиска и добавьте в список приложений.</span><span class="sxs-lookup"><span data-stu-id="5ec19-132">Select ZenDesk from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="5ec19-133">Выберите экземпляр ZenDesk, а затем перейдите на вкладку **Подготовка**.</span><span class="sxs-lookup"><span data-stu-id="5ec19-133">Select your instance of ZenDesk, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="5ec19-134">Для параметра **Режим подготовки к работе** выберите значение **Automatic** (Автоматически).</span><span class="sxs-lookup"><span data-stu-id="5ec19-134">Set the **Provisioning Mode** to **Automatic**.</span></span>

    ![Подготовка ZenDesk](./media/active-directory-saas-zendesk-provisioning-tutorial/ZenDesk1.png)

5. <span data-ttu-id="5ec19-136">В разделе **Учетные данные администратора** введите **имя пользователя администратора, ключ токена и домен**, созданные вашей учетной записью ZenDesk (токен можно найти в своей учетной записи: выберите **Admin** > **API** > **Settings** ("Администрирование" > "API" > "Параметры")).</span><span class="sxs-lookup"><span data-stu-id="5ec19-136">Under the **Admin Credentials** section, input the **Admin Username&tokenkey&Domain** generated by your ZenDesk's account (you can find the token under your account: **Admin** > **API** > **Settings**).</span></span> 

    ![Подготовка ZenDesk](./media/active-directory-saas-zendesk-provisioning-tutorial/ZenDesk2.png)

6. <span data-ttu-id="5ec19-138">На портале Azure щелкните **Проверить подключение**, чтобы убедиться, что Azure AD может подключиться к приложению ZenDesk.</span><span class="sxs-lookup"><span data-stu-id="5ec19-138">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your ZenDesk app.</span></span> <span data-ttu-id="5ec19-139">Если установить подключение не удалось, убедитесь, что у учетной записи ZenDesk есть разрешения администратора, и повторите шаг 5.</span><span class="sxs-lookup"><span data-stu-id="5ec19-139">If the connection fails, ensure your ZenDesk account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="5ec19-140">В поле **Почтовое уведомление** введите адрес электронной почты пользователя или группы, которые должны получать уведомления об ошибках подготовки, а также установите флажок "Отправить уведомление по электронной почте при сбое".</span><span class="sxs-lookup"><span data-stu-id="5ec19-140">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="5ec19-141">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="5ec19-141">Click **Save**.</span></span> 

9. <span data-ttu-id="5ec19-142">В разделе "Сопоставления" выберите **Synchronize Azure Active Directory Users to ZenDesk** (Синхронизировать пользователей Azure Active Directory с ZenDesk).</span><span class="sxs-lookup"><span data-stu-id="5ec19-142">Under the Mappings section, select **Synchronize Azure Active Directory Users to ZenDesk**.</span></span>

10. <span data-ttu-id="5ec19-143">В разделе **Сопоставления атрибутов** просмотрите пользовательские атрибуты, которые синхронизированы из Azure AD в ZenDesk.</span><span class="sxs-lookup"><span data-stu-id="5ec19-143">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to ZenDesk.</span></span> <span data-ttu-id="5ec19-144">Атрибуты, выбранные как свойства **Matching**, используются для сопоставления учетных записей пользователей в ZenDesk для операций обновления.</span><span class="sxs-lookup"><span data-stu-id="5ec19-144">The attributes selected as **Matching** properties are used to match the user accounts in ZenDesk for update operations.</span></span> <span data-ttu-id="5ec19-145">Нажмите кнопку "Сохранить", чтобы подтвердить все изменения.</span><span class="sxs-lookup"><span data-stu-id="5ec19-145">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="5ec19-146">Чтобы включить службу подготовки Azure AD для ZenDesk, измените значение параметра **Состояние подготовки** на **Включено** в разделе **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="5ec19-146">To enable the Azure AD provisioning service for ZenDesk, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

12. <span data-ttu-id="5ec19-147">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="5ec19-147">Click **Save**.</span></span> 

<span data-ttu-id="5ec19-148">После этого начнется начальная синхронизация всех пользователей и (или) групп, назначенных в ZenDesk в разделе "Пользователи и группы".</span><span class="sxs-lookup"><span data-stu-id="5ec19-148">This operation starts the initial synchronization of any users and/or groups assigned to ZenDesk in the Users and Groups section.</span></span> <span data-ttu-id="5ec19-149">Начальная синхронизация занимает больше времени, чем последующие операции синхронизации. Последующие операции синхронизации выполняются примерно каждые 20 минут, при условии, что служба запущена.</span><span class="sxs-lookup"><span data-stu-id="5ec19-149">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="5ec19-150">В разделе **Сведения о синхронизации** можно отслеживать ход выполнения и переходить по ссылкам для просмотра отчетов о подготовке, в которых зафиксированы все действия, выполняемые службой подготовки.</span><span class="sxs-lookup"><span data-stu-id="5ec19-150">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service.</span></span>

<span data-ttu-id="5ec19-151">Дополнительные сведения о чтении журналов подготовки Azure AD см. в руководстве по [отчетам об автоматической подготовке учетных записей](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="5ec19-151">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="5ec19-152">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="5ec19-152">Additional resources</span></span>

* [<span data-ttu-id="5ec19-153">Управление подготовкой учетных записей пользователей для корпоративных приложений</span><span class="sxs-lookup"><span data-stu-id="5ec19-153">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="5ec19-154">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5ec19-154">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="5ec19-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5ec19-155">Next steps</span></span>

* [<span data-ttu-id="5ec19-156">Сведения о просмотре журналов и получении отчетов о действиях по подготовке</span><span class="sxs-lookup"><span data-stu-id="5ec19-156">Learn how to review logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
