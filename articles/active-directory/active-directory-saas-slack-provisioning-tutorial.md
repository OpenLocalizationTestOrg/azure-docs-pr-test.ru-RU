---
title: "Руководство по настройке Slack для автоматической подготовки пользователей с помощью Azure Active Directory | Документация Майкрософт"
description: "Узнайте, как настроить Azure Active Directory для автоматической подготовки и отмены подготовки учетных записей пользователей в Slack."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: sakula
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: asmalser-msft
ms.reviewer: asmalser
ms.openlocfilehash: 3cb49a4abb26c34a938c963c4cf326b5ccd490de
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-configuring-slack-for-automatic-user-provisioning"></a><span data-ttu-id="2fee5-103">Tutorial: Configuring Slack for Automatic User Provisioning (Учебник. Настройка Slack для автоматической подготовки пользователей)</span><span class="sxs-lookup"><span data-stu-id="2fee5-103">Tutorial: Configuring Slack for Automatic User Provisioning</span></span>


<span data-ttu-id="2fee5-104">Цель этого учебника — показать, как в Slack и Azure AD необходимо выполнять автоматическую подготовку и отмену подготовки учетных записей пользователей из Azure AD в Slack.</span><span class="sxs-lookup"><span data-stu-id="2fee5-104">The objective of this tutorial is to show you the steps you need to perform in Slack and Azure AD to automatically provision and de-provision user accounts from Azure AD to Slack.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="2fee5-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="2fee5-105">Prerequisites</span></span>

<span data-ttu-id="2fee5-106">Сценарий, описанный в этом учебнике, предполагает, что у вас уже имеется:</span><span class="sxs-lookup"><span data-stu-id="2fee5-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="2fee5-107">Клиент Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2fee5-107">An Azure Active Active directory tenant</span></span>
*   <span data-ttu-id="2fee5-108">Клиент Slack с включенным планом [Plus](https://aadsyncfabric.slack.com/pricing) или выше</span><span class="sxs-lookup"><span data-stu-id="2fee5-108">A Slack tenant with the [Plus plan](https://aadsyncfabric.slack.com/pricing) or better enabled</span></span> 
*   <span data-ttu-id="2fee5-109">Учетная запись пользователя в Slack с разрешениями администратора группы</span><span class="sxs-lookup"><span data-stu-id="2fee5-109">A user account in Slack with Team Admin permissions</span></span> 

<span data-ttu-id="2fee5-110">Примечание. Интеграция подготовки в Azure AD зависит от [API SCIM Slack](https://api.slack.com/scim), доступного для групп Slack в плане Plus или лучше.</span><span class="sxs-lookup"><span data-stu-id="2fee5-110">Note: The Azure AD provisioning integration relies on the [Slack SCIM API](https://api.slack.com/scim) which is available to Slack teams on the Plus plan or better.</span></span>

## <a name="assigning-users-to-slack"></a><span data-ttu-id="2fee5-111">Назначение пользователей в Slack</span><span class="sxs-lookup"><span data-stu-id="2fee5-111">Assigning users to Slack</span></span>

<span data-ttu-id="2fee5-112">В Azure Active Directory для определения того, какие пользователи должны получать доступ к выбранным приложениям, используется концепция, называемая "назначение".</span><span class="sxs-lookup"><span data-stu-id="2fee5-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="2fee5-113">В контексте автоматической подготовки учетной записи синхронизированы будут только те пользователи и группы, которые были "назначены" приложению в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2fee5-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD will be synchronized.</span></span> 

<span data-ttu-id="2fee5-114">Перед настройкой и включением службы подготовки необходимо решить, какие пользователи или группы в Azure AD представляют пользователей, которым необходим доступ к приложению Slack.</span><span class="sxs-lookup"><span data-stu-id="2fee5-114">Before configuring and enabling the provisioning service, you will need to decide what users and/or groups in Azure AD represent the users who need access to your Slack app.</span></span> <span data-ttu-id="2fee5-115">Когда этот вопрос будет решен, можно назначить этих пользователей приложению Slack, следуя нижеперечисленным указаниям.</span><span class="sxs-lookup"><span data-stu-id="2fee5-115">Once decided, you can assign these users to your Slack app by following the instructions here:</span></span>

[<span data-ttu-id="2fee5-116">Назначение корпоративному приложению пользователя или группы</span><span class="sxs-lookup"><span data-stu-id="2fee5-116">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-slack"></a><span data-ttu-id="2fee5-117">Важные рекомендации по назначению пользователей в Slack</span><span class="sxs-lookup"><span data-stu-id="2fee5-117">Important tips for assigning users to Slack</span></span>

*   <span data-ttu-id="2fee5-118">Рекомендуется назначить одного пользователя Azure AD в Slack для тестирования конфигурации подготовки.</span><span class="sxs-lookup"><span data-stu-id="2fee5-118">It is recommended that a single Azure AD user be assigned to Slack to test the provisioning configuration.</span></span> <span data-ttu-id="2fee5-119">Дополнительные пользователи и/или группы можно назначить позднее.</span><span class="sxs-lookup"><span data-stu-id="2fee5-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="2fee5-120">При назначении пользователя в Slack необходимо выбрать роль **Пользователь** или "Группа" в диалоговом окне назначения.</span><span class="sxs-lookup"><span data-stu-id="2fee5-120">When assigning a user to Slack, you must select the **User** or "Group" role in the assignment dialog.</span></span> <span data-ttu-id="2fee5-121">Роль "Доступ по умолчанию" не работает для подготовки.</span><span class="sxs-lookup"><span data-stu-id="2fee5-121">The "Default Access" role does not work for provisioning.</span></span>


## <a name="configuring-user-provisioning-to-slack"></a><span data-ttu-id="2fee5-122">Настройка подготовки учетных записей пользователей в Slack</span><span class="sxs-lookup"><span data-stu-id="2fee5-122">Configuring user provisioning to Slack</span></span> 

<span data-ttu-id="2fee5-123">В этом разделе описывается подключение к API подготовки учетной записи пользователя Azure AD в Slack и настройка подготовки службы для создания, обновления и отмены назначения учетных записей пользователей в Slack на основе назначения пользователей и групп в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2fee5-123">This section guides you through connecting your Azure AD to Slack's user account provisioning API, and configuring the provisioning service to create, update and disable assigned user accounts in Slack based on user and group assignment in Azure AD.</span></span>

<span data-ttu-id="2fee5-124">**Совет.** Для Slack также можно включить единый вход на основе SAML, следуя инструкциям на портале Azure [https://portal.azure.com].</span><span class="sxs-lookup"><span data-stu-id="2fee5-124">**Tip:** You may also choose to enabled SAML-based Single Sign-On for Slack, following the instructions provided in (Azure portal)[https://portal.azure.com].</span></span> <span data-ttu-id="2fee5-125">Единый вход можно настроить независимо от автоматической подготовки, хотя эти две возможности дополняют друг друга.</span><span class="sxs-lookup"><span data-stu-id="2fee5-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="to-configure-automatic-user-account-provisioning-to-slack-in-azure-ad"></a><span data-ttu-id="2fee5-126">Настройка автоматической подготовки учетных записей пользователей Azure AD в Slack.</span><span class="sxs-lookup"><span data-stu-id="2fee5-126">To configure automatic user account provisioning to Slack in Azure AD:</span></span>


1)  <span data-ttu-id="2fee5-127">На [портале Azure](https://portal.azure.com) перейдите в раздел **Azure Active Directory > Корпоративные приложения > Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="2fee5-127">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2) <span data-ttu-id="2fee5-128">Если в Slack уже настроен единый вход, найдите свой экземпляр Slack с помощью поля поиска.</span><span class="sxs-lookup"><span data-stu-id="2fee5-128">If you have already configured Slack for single sign-on, search for your instance of Slack using the search field.</span></span> <span data-ttu-id="2fee5-129">В противном случае щелкните **Добавить** и выполните поиск **Slack** в коллекции приложений.</span><span class="sxs-lookup"><span data-stu-id="2fee5-129">Otherwise, select **Add** and search for **Slack** in the application gallery.</span></span> <span data-ttu-id="2fee5-130">Выберите Slack в результатах поиска и добавьте его в список приложений.</span><span class="sxs-lookup"><span data-stu-id="2fee5-130">Select Slack from the search results, and add it to your list of applications.</span></span>

3)  <span data-ttu-id="2fee5-131">Выберите экземпляр Slack, а затем перейдите на вкладку **Подготовка**.</span><span class="sxs-lookup"><span data-stu-id="2fee5-131">Select your instance of Slack, then select the **Provisioning** tab.</span></span>

4)  <span data-ttu-id="2fee5-132">Для параметра **Режим подготовки к работе** выберите значение **Automatic** (Автоматически).</span><span class="sxs-lookup"><span data-stu-id="2fee5-132">Set the **Provisioning Mode** to **Automatic**.</span></span>

![Подготовка Slack](./media/active-directory-saas-slack-provisioning-tutorial/Slack1.PNG)

5)  <span data-ttu-id="2fee5-134">В разделе **Учетные данные администратора** щелкните **Авторизовать**.</span><span class="sxs-lookup"><span data-stu-id="2fee5-134">Under the **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="2fee5-135">В новом окне браузера откроется диалоговое окно авторизации Slack.</span><span class="sxs-lookup"><span data-stu-id="2fee5-135">This opens a Slack authorization dialog in a new browser window.</span></span> 

6) <span data-ttu-id="2fee5-136">В новом окне войдите в Slack с использованием учетной записи администратора группы.</span><span class="sxs-lookup"><span data-stu-id="2fee5-136">In the new window, sign into Slack using your Team Admin account.</span></span> <span data-ttu-id="2fee5-137">в открывшемся диалоговом окне авторизации выберите группу Slack, для которой необходимо включить подготовку, а затем выберите **Authorize** (Авторизовать).</span><span class="sxs-lookup"><span data-stu-id="2fee5-137">in the resulting authorization dialog, select the Slack team that you want to enable provisioning for, and then select **Authorize**.</span></span> <span data-ttu-id="2fee5-138">После завершения вернитесь на портал Azure для завершения настройки подготовки.</span><span class="sxs-lookup"><span data-stu-id="2fee5-138">Once completed, return to the Azure portal to complete the provisioning configuration.</span></span>

![Диалоговое окно авторизации](./media/active-directory-saas-slack-provisioning-tutorial/Slack3.PNG)

7) <span data-ttu-id="2fee5-140">На портале Azure щелкните **Проверить подключение**, чтобы убедиться, что Azure AD может подключиться к приложению Slack.</span><span class="sxs-lookup"><span data-stu-id="2fee5-140">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Slack app.</span></span> <span data-ttu-id="2fee5-141">Если подключение отсутствует, убедитесь, что у учетной записи Slack есть права администратора группы, и повторите шаг "Авторизовать".</span><span class="sxs-lookup"><span data-stu-id="2fee5-141">If the connection fails, ensure your Slack account has Team Admin permissions and try the "Authorize" step again.</span></span>

8) <span data-ttu-id="2fee5-142">В поле **Почтовое уведомление** введите адрес электронной почты пользователя или группы, которые должны получать уведомления об ошибках подготовки, а также установите флажок ниже.</span><span class="sxs-lookup"><span data-stu-id="2fee5-142">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span></span>

9) <span data-ttu-id="2fee5-143">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="2fee5-143">Click **Save**.</span></span> 

10) <span data-ttu-id="2fee5-144">В разделе сопоставления выберите **Synchronize Azure Active Directory Users to Slack** (Синхронизировать пользователей Azure Active Directory с Slack).</span><span class="sxs-lookup"><span data-stu-id="2fee5-144">Under the Mappings section, select **Synchronize Azure Active Directory Users to Slack**.</span></span>

11) <span data-ttu-id="2fee5-145">В разделе **Attribute Mappings** (Сопоставления атрибутов) следует просмотреть атрибуты пользователей, которые будут синхронизированы из Azure AD в Slack.</span><span class="sxs-lookup"><span data-stu-id="2fee5-145">In the **Attribute Mappings** section, review the user attributes that will be synchronized from Azure AD to Slack.</span></span> <span data-ttu-id="2fee5-146">Обратите внимание, что атрибуты, которые выбраны в качестве свойств **Matching** (Сопоставление), будут использоваться для сопоставления учетных записей пользователей в Slack для операций обновления.</span><span class="sxs-lookup"><span data-stu-id="2fee5-146">Note that the attributes selected as **Matching** properties will be used to match the user accounts in Slack for update operations.</span></span> <span data-ttu-id="2fee5-147">Нажмите кнопку "Сохранить", чтобы подтвердить все изменения.</span><span class="sxs-lookup"><span data-stu-id="2fee5-147">Select the Save button to commit any changes.</span></span>

12) <span data-ttu-id="2fee5-148">Чтобы включить службу подготовки Azure AD для Slack, измените значение параметра **Provisioning Status** (Статус подготовки) на **On** (Включено) в разделе **Настройки**.</span><span class="sxs-lookup"><span data-stu-id="2fee5-148">To enable the Azure AD provisioning service for Slack, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

13) <span data-ttu-id="2fee5-149">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="2fee5-149">Click **Save**.</span></span> 

<span data-ttu-id="2fee5-150">После этого начнется начальная синхронизация всех пользователей и групп, назначенные в Slack в разделе "Пользователи и группы".</span><span class="sxs-lookup"><span data-stu-id="2fee5-150">This will start the initial synchronization of any users and/or groups assigned to Slack in the Users and Groups section.</span></span> <span data-ttu-id="2fee5-151">Обратите внимание, что начальная синхронизация будет занимать больше времени, чем последующие синхронизации, выполняющиеся примерно каждые 10 минут, при условии, что служба запущена.</span><span class="sxs-lookup"><span data-stu-id="2fee5-151">Note that the initial sync will take longer to perform than subsequent syncs, which occur approximately every 10 minutes as long as the service is running.</span></span> <span data-ttu-id="2fee5-152">В разделе **Сведения о синхронизации** можно отслеживать ход выполнения и переходить по ссылкам для просмотра отчетов по подготовке, в которых зафиксированы все действия, выполняемые в приложении Slack службой подготовки.</span><span class="sxs-lookup"><span data-stu-id="2fee5-152">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Slack app.</span></span>

## <a name="optional-configuring-group-object-provisioning-to-slack"></a><span data-ttu-id="2fee5-153">[Необязательно] Настройка подготовки групповых объектов в Slack</span><span class="sxs-lookup"><span data-stu-id="2fee5-153">[Optional] Configuring group object provisioning to Slack</span></span> 

<span data-ttu-id="2fee5-154">При необходимости можно включить подготовку групповых объектов из Azure AD в Slack.</span><span class="sxs-lookup"><span data-stu-id="2fee5-154">Optionally, you can enable the provisioning of group objects from Azure AD to Slack.</span></span> <span data-ttu-id="2fee5-155">Это отличается от "назначения групп пользователей" в том, что реальный групповой объект в дополнение к ее участникам будет реплицирован из Azure AD в Slack.</span><span class="sxs-lookup"><span data-stu-id="2fee5-155">This is different from "assigning groups of users", in that the actual group object in addition to its members will be replicated from Azure AD to Slack.</span></span> <span data-ttu-id="2fee5-156">Например, если в Azure AD есть группа с именем "Моя группа", идентичная группа с именем "Моя группа" будет создана в Slack.</span><span class="sxs-lookup"><span data-stu-id="2fee5-156">For example, if you have a group named "My Group" in Azure AD, an identitical group named "My Group" will be created inside Slack.</span></span>

### <a name="to-enable-provisioning-of-group-objects"></a><span data-ttu-id="2fee5-157">Включение подготовки групповых объектов</span><span class="sxs-lookup"><span data-stu-id="2fee5-157">To enable provisioning of group objects:</span></span>

1) <span data-ttu-id="2fee5-158">В разделе сопоставления выберите **Synchronize Azure Active Directory Groups to Slack** (Синхронизировать группы Azure Active Directory с Slack).</span><span class="sxs-lookup"><span data-stu-id="2fee5-158">Under the Mappings section, select **Synchronize Azure Active Directory Groups to Slack**.</span></span>

2) <span data-ttu-id="2fee5-159">В колонке сопоставления атрибутов для параметра Enabled (Включено) выберите значение Yes (Да).</span><span class="sxs-lookup"><span data-stu-id="2fee5-159">In the Attribute Mapping blade, set Enabled to Yes.</span></span>

3) <span data-ttu-id="2fee5-160">В разделе **Attribute Mappings** (Сопоставления атрибутов) следует просмотреть атрибуты групп, которые будут синхронизированы из Azure AD в Slack.</span><span class="sxs-lookup"><span data-stu-id="2fee5-160">In the **Attribute Mappings** section, review the group attributes that will be synchronized from Azure AD to Slack.</span></span> <span data-ttu-id="2fee5-161">Обратите внимание, что атрибуты выбран в качестве **сопоставление** свойств будет использоваться для сопоставления групп в Slack для операции обновления.</span><span class="sxs-lookup"><span data-stu-id="2fee5-161">Note that the attributes selected as **Matching** properties will be used to match the groups in Slack for update operations.</span></span> 

4) <span data-ttu-id="2fee5-162">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="2fee5-162">Click **Save**.</span></span>

<span data-ttu-id="2fee5-163">В результате все групповые объекты, назначенные в Slack в разделе **Пользователи и группы**, полностью синхронизируются из Azure AD в Slack.</span><span class="sxs-lookup"><span data-stu-id="2fee5-163">This result in any group objects assigned to Slack in the **Users and Groups** section being fully synchronized from Azure AD to Slack.</span></span> <span data-ttu-id="2fee5-164">В разделе **Сведения о синхронизации** можно отслеживать ход выполнения и переходить по ссылкам для просмотра отчетов по подготовке, в которых зафиксированы все действия, выполняемые в приложении Slack службой подготовки.</span><span class="sxs-lookup"><span data-stu-id="2fee5-164">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Slack app.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="2fee5-165">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="2fee5-165">Additional Resources</span></span>

* [<span data-ttu-id="2fee5-166">Управление подготовкой учетных записей пользователей для корпоративных приложений</span><span class="sxs-lookup"><span data-stu-id="2fee5-166">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="2fee5-167">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2fee5-167">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
