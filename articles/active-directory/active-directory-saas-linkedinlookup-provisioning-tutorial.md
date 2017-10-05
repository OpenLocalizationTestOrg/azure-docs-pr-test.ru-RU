---
title: "Руководство по настройке LinkedIn Lookup для автоматической подготовки пользователей с помощью Azure Active Directory | Документация Майкрософт"
description: "Узнайте, как настроить Azure Active Directory для автоматической подготовки и отзыва учетных записей пользователей в LinkedIn Lookup."
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
ms.date: 04/15/2017
ms.author: asmalser-msft
ms.openlocfilehash: 085a68cfe8f9e08b8722e8613994ee300a015776
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-linkedin-lookup-for-automatic-user-provisioning"></a><span data-ttu-id="f4bc2-103">Руководство по настройке LinkedIn Lookup для автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="f4bc2-103">Tutorial: Configuring LinkedIn Lookup for Automatic User Provisioning</span></span>


<span data-ttu-id="f4bc2-104">Цель этого руководства — показать, как настроить автоматическую подготовку и отзыв учетных записей пользователей Azure AD в LinkedIn Lookup.</span><span class="sxs-lookup"><span data-stu-id="f4bc2-104">The objective of this tutorial is to show you the steps you need to perform in LinkedIn Lookup and Azure AD to automatically provision and de-provision user accounts from Azure AD to LinkedIn Lookup.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f4bc2-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f4bc2-105">Prerequisites</span></span>

<span data-ttu-id="f4bc2-106">Сценарий, описанный в этом учебнике, предполагает, что у вас уже имеется:</span><span class="sxs-lookup"><span data-stu-id="f4bc2-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="f4bc2-107">Клиент Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f4bc2-107">An Azure Active Directory tenant</span></span>
*   <span data-ttu-id="f4bc2-108">Клиент LinkedIn Lookup.</span><span class="sxs-lookup"><span data-stu-id="f4bc2-108">A LinkedIn Lookup tenant</span></span> 
*   <span data-ttu-id="f4bc2-109">Учетная запись администратора в LinkedIn Lookup с доступом к центру учетных записей LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="f4bc2-109">An administrator account in LinkedIn Lookup with access to the LinkedIn Account Center</span></span>

> [!NOTE]
> <span data-ttu-id="f4bc2-110">Для интеграции Azure Active Directory с LinkedIn Lookup используется протокол [SCIM](http://www.simplecloud.info/).</span><span class="sxs-lookup"><span data-stu-id="f4bc2-110">Azure Active Directory integrates with LinkedIn Lookup using the [SCIM](http://www.simplecloud.info/) protocol.</span></span>

## <a name="assigning-users-to-linkedin-lookup"></a><span data-ttu-id="f4bc2-111">Добавление пользователей в LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="f4bc2-111">Assigning users to LinkedIn Lookup</span></span>

<span data-ttu-id="f4bc2-112">В Azure Active Directory для определения того, какие пользователи должны получать доступ к выбранным приложениям, используется концепция, называемая "назначение".</span><span class="sxs-lookup"><span data-stu-id="f4bc2-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="f4bc2-113">В контексте автоматической подготовки учетной записи синхронизированы будут только те пользователи и группы, которые были "назначены" приложению в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4bc2-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD will be synchronized.</span></span> 

<span data-ttu-id="f4bc2-114">Перед настройкой и включением службы подготовки необходимо решить, какие пользователи или группы в Azure AD представляют пользователей, которым нужен доступ к LinkedIn Lookup.</span><span class="sxs-lookup"><span data-stu-id="f4bc2-114">Before configuring and enabling the provisioning service, you will need to decide what users and/or groups in Azure AD represent the users who need access to LinkedIn Lookup.</span></span> <span data-ttu-id="f4bc2-115">Когда этот вопрос будет решен, этих пользователей можно будет назначить приложению LinkedIn Lookup, следуя приведенным ниже указаниям.</span><span class="sxs-lookup"><span data-stu-id="f4bc2-115">Once decided, you can assign these users to LinkedIn Lookup by following the instructions here:</span></span>

[<span data-ttu-id="f4bc2-116">Назначение корпоративному приложению пользователя или группы</span><span class="sxs-lookup"><span data-stu-id="f4bc2-116">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-linkedin-lookup"></a><span data-ttu-id="f4bc2-117">Важные рекомендации по назначению пользователей приложению LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="f4bc2-117">Important tips for assigning users to LinkedIn Lookup</span></span>

*   <span data-ttu-id="f4bc2-118">Рекомендуем сначала назначить приложению LinkedIn Lookup одного пользователя Azure AD и с его помощью протестировать конфигурацию подготовки.</span><span class="sxs-lookup"><span data-stu-id="f4bc2-118">It is recommended that a single Azure AD user be assigned to LinkedIn Lookup to test the provisioning configuration.</span></span> <span data-ttu-id="f4bc2-119">Дополнительные пользователи и/или группы можно назначить позднее.</span><span class="sxs-lookup"><span data-stu-id="f4bc2-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="f4bc2-120">Назначая пользователя приложению LinkedIn Lookup, в диалоговом окне назначения необходимо выбрать роль **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="f4bc2-120">When assigning a user to LinkedIn Lookup, you must select the **User** role in the assignment dialog.</span></span> <span data-ttu-id="f4bc2-121">Роль "Доступ по умолчанию" не работает для подготовки.</span><span class="sxs-lookup"><span data-stu-id="f4bc2-121">The "Default Access" role does not work for provisioning.</span></span>


## <a name="configuring-user-provisioning-to-linkedin-lookup"></a><span data-ttu-id="f4bc2-122">Настройка подготовки пользователей в LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="f4bc2-122">Configuring user provisioning to LinkedIn Lookup</span></span>

<span data-ttu-id="f4bc2-123">В этом разделе мы подключим Azure AD к API подготовки учетных записей в LinkedIn Lookup (через протокол SCIM), а также настроим службу подготовки для создания, изменения и отключения назначенных учетных записей пользователей в LinkedIn Lookup, используя пользователей и группы в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4bc2-123">This section guides you through connecting your Azure AD to LinkedIn Lookup's SCIM user account provisioning API, and configuring the provisioning service to create, update and disable assigned user accounts in LinkedIn Lookup based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="f4bc2-124">Для LinkedIn Lookup также можно включить единый вход на основе SAML. Для этого следуйте инструкциям, указанным на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f4bc2-124">You may also choose to enabled SAML-based Single Sign-On for LinkedIn Lookup, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="f4bc2-125">Единый вход можно настроить независимо от автоматической подготовки, хотя две эти функции дополняют друг друга.</span><span class="sxs-lookup"><span data-stu-id="f4bc2-125">Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.</span></span>


### <a name="to-configure-automatic-user-account-provisioning-to-linkedin-lookup-in-azure-ad"></a><span data-ttu-id="f4bc2-126">Настройка автоматической подготовки учетных записей пользователей Azure AD в LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="f4bc2-126">To configure automatic user account provisioning to LinkedIn Lookup in Azure AD:</span></span>


<span data-ttu-id="f4bc2-127">Для начала необходимо получить токен доступа LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="f4bc2-127">The first step is to retrieve your LinkedIn access token.</span></span> <span data-ttu-id="f4bc2-128">Если вы являетесь администратором предприятия, то можете самостоятельно подготовить токен доступа.</span><span class="sxs-lookup"><span data-stu-id="f4bc2-128">If you are an Enterprise administrator, you can self-provision an access token.</span></span> <span data-ttu-id="f4bc2-129">В центре учетных записей откройте раздел **Параметры &gt; Глобальные параметры** и затем откройте панель **Параметры SCIM**.</span><span class="sxs-lookup"><span data-stu-id="f4bc2-129">In your account center, go to **Settings &gt; Global Settings** and open the **SCIM Setup** panel.</span></span>

> [!NOTE]
> <span data-ttu-id="f4bc2-130">При доступе к центру учетных записей напрямую, а не по ссылке, выполните следующие действия, чтобы открыть панель.</span><span class="sxs-lookup"><span data-stu-id="f4bc2-130">If you are accessing the account center directly rather than through a link, you can reach it using the following steps.</span></span>

1)  <span data-ttu-id="f4bc2-131">Войдите в центр учетных записей.</span><span class="sxs-lookup"><span data-stu-id="f4bc2-131">Sign in to Account Center.</span></span>

2)  <span data-ttu-id="f4bc2-132">Выберите **Администратор &gt; Параметры администратора**.</span><span class="sxs-lookup"><span data-stu-id="f4bc2-132">Select **Admin &gt; Admin Settings** .</span></span>

3)  <span data-ttu-id="f4bc2-133">Щелкните **Расширенная интеграция** на левой боковой панели.</span><span class="sxs-lookup"><span data-stu-id="f4bc2-133">Click **Advanced Integrations** on the left sidebar.</span></span> <span data-ttu-id="f4bc2-134">Вы будете перенаправлены в центр учетных записей.</span><span class="sxs-lookup"><span data-stu-id="f4bc2-134">You are directed to the account center.</span></span>

4)  <span data-ttu-id="f4bc2-135">Щелкните **+ Добавить новую конфигурацию SCIM** и выполните инструкцию, заполнив каждое поле.</span><span class="sxs-lookup"><span data-stu-id="f4bc2-135">Click **+ Add new SCIM configuration** and follow the procedure by filling in each field.</span></span>

> <span data-ttu-id="f4bc2-136">Если автоматическое назначение лицензии отключено, синхронизируются только данные пользователя.</span><span class="sxs-lookup"><span data-stu-id="f4bc2-136">When auto­assign licenses is not enabled, it means that only user data is synced.</span></span>

![Подготовка LinkedIn Lookup](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_1.PNG)

> <span data-ttu-id="f4bc2-138">При автоматическом назначении лицензии необходимо отметить экземпляр приложения и тип лицензии.</span><span class="sxs-lookup"><span data-stu-id="f4bc2-138">When auto­license assignment is enabled, you need to note the application instance and license type.</span></span> <span data-ttu-id="f4bc2-139">Лицензии назначаются по мере получения запросов до тех пор, пока все лицензии не будут заняты.</span><span class="sxs-lookup"><span data-stu-id="f4bc2-139">Licenses are assigned on a first come, first serve basis until all the licenses are taken.</span></span>

![Подготовка LinkedIn Lookup](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_2.PNG)

5)  <span data-ttu-id="f4bc2-141">Щелкните **Создать токен**.</span><span class="sxs-lookup"><span data-stu-id="f4bc2-141">Click **Generate token**.</span></span> <span data-ttu-id="f4bc2-142">Токен доступа должен появиться в поле **Токен доступа**.</span><span class="sxs-lookup"><span data-stu-id="f4bc2-142">You should see your access token display under the **Access token** field.</span></span>

6)  <span data-ttu-id="f4bc2-143">Перед тем как закрыть эту страницу, сохраните токен доступа в буфере обмена или на компьютере.</span><span class="sxs-lookup"><span data-stu-id="f4bc2-143">Save your access token to your clipboard or computer before leaving the page.</span></span>

7) <span data-ttu-id="f4bc2-144">Затем войдите на [портал Azure](https://portal.azure.com) и перейдите в раздел **Azure Active Directory > Корпоративные приложения > Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f4bc2-144">Next, sign in to the [Azure portal](https://portal.azure.com), and browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

8) <span data-ttu-id="f4bc2-145">Если вы уже настроили единый вход для LinkedIn Lookup, найдите свой экземпляр LinkedIn Lookup с помощью поля поиска.</span><span class="sxs-lookup"><span data-stu-id="f4bc2-145">If you have already configured LinkedIn Lookup for single sign-on, search for your instance of LinkedIn Lookup using the search field.</span></span> <span data-ttu-id="f4bc2-146">В противном случае щелкните **Добавить** и выполните поиск **LinkedIn Lookup** в коллекции приложений.</span><span class="sxs-lookup"><span data-stu-id="f4bc2-146">Otherwise, select **Add** and search for **LinkedIn Lookup** in the application gallery.</span></span> <span data-ttu-id="f4bc2-147">Выберите LinkedIn Lookup в результатах поиска и добавьте это приложение в свой список приложений.</span><span class="sxs-lookup"><span data-stu-id="f4bc2-147">Select LinkedIn Lookup from the search results, and add it to your list of applications.</span></span>

9)  <span data-ttu-id="f4bc2-148">Выберите свой экземпляр LinkedIn Lookup и перейдите на вкладку **Подготовка**.</span><span class="sxs-lookup"><span data-stu-id="f4bc2-148">Select your instance of LinkedIn Lookup, then select the **Provisioning** tab.</span></span>

10) <span data-ttu-id="f4bc2-149">Для параметра **Режим подготовки к работе** выберите значение **Automatic** (Автоматически).</span><span class="sxs-lookup"><span data-stu-id="f4bc2-149">Set the **Provisioning Mode** to **Automatic**.</span></span>

![Подготовка LinkedIn Lookup](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_3.PNG)

11)  <span data-ttu-id="f4bc2-151">Заполните следующие поля в разделе **Учетные данные администратора**:</span><span class="sxs-lookup"><span data-stu-id="f4bc2-151">Fill in the following fields under **Admin Credentials** :</span></span>

* <span data-ttu-id="f4bc2-152">В **URL-адрес клиента** введите https://api.linkedin.com.</span><span class="sxs-lookup"><span data-stu-id="f4bc2-152">In the **Tenant URL** field, enter https://api.linkedin.com.</span></span>

* <span data-ttu-id="f4bc2-153">В поле **Секретный токен** введите токен доступа, созданный на шаге 1, и нажмите кнопку **Проверить подключение**.</span><span class="sxs-lookup"><span data-stu-id="f4bc2-153">In the **Secret Token** field, enter the access token you generated in step 1 and click **Test Connection** .</span></span>

* <span data-ttu-id="f4bc2-154">Вы должны увидеть оповещение об успешной проверке подключения в правом верхнем углу портала.</span><span class="sxs-lookup"><span data-stu-id="f4bc2-154">You should see a success notification on the upper­right side of   your portal.</span></span>

12) <span data-ttu-id="f4bc2-155">В поле **Почтовое уведомление** введите адрес электронной почты пользователя или группы, которые должны получать уведомления об ошибках подготовки, а также установите флажок ниже.</span><span class="sxs-lookup"><span data-stu-id="f4bc2-155">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span></span>

13) <span data-ttu-id="f4bc2-156">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="f4bc2-156">Click **Save**.</span></span> 

14) <span data-ttu-id="f4bc2-157">В разделе **Сопоставления атрибутов** просмотрите атрибуты пользователей и групп, которые будут синхронизированы из Azure AD в LinkedIn Lookup.</span><span class="sxs-lookup"><span data-stu-id="f4bc2-157">In the **Attribute Mappings** section, review the user and group attributes that will be synchronized from Azure AD to LinkedIn Lookup.</span></span> <span data-ttu-id="f4bc2-158">Обратите внимание, что атрибуты, которые выбраны в качестве свойств **сопоставления**, будут использоваться для сопоставления учетных записей пользователей и групп для операций обновления в LinkedIn Lookup.</span><span class="sxs-lookup"><span data-stu-id="f4bc2-158">Note that the attributes selected as **Matching** properties will be used to match the user accounts and groups in LinkedIn Lookup for update operations.</span></span> <span data-ttu-id="f4bc2-159">Нажмите кнопку "Сохранить", чтобы подтвердить все изменения.</span><span class="sxs-lookup"><span data-stu-id="f4bc2-159">Select the Save button to commit any changes.</span></span>

![Подготовка LinkedIn Lookup](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_4.PNG)

15) <span data-ttu-id="f4bc2-161">Чтобы включить службу подготовки Azure AD для LinkedIn Lookup, в разделе **Параметры** установите переключатель **Состояние подготовки** в положение **Включено**.</span><span class="sxs-lookup"><span data-stu-id="f4bc2-161">To enable the Azure AD provisioning service for LinkedIn Lookup, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

16) <span data-ttu-id="f4bc2-162">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="f4bc2-162">Click **Save**.</span></span> 

<span data-ttu-id="f4bc2-163">После этого будет запущена начальная синхронизация всех пользователей и групп, назначенных приложению LinkedIn Lookup в разделе "Пользователи и группы".</span><span class="sxs-lookup"><span data-stu-id="f4bc2-163">This will start the initial synchronization of any users and/or groups assigned to LinkedIn Lookup in the Users and Groups section.</span></span> <span data-ttu-id="f4bc2-164">Обратите внимание, что начальная синхронизация будет занимать больше времени, чем последующие операции синхронизации. Последующие операции синхронизации выполняются примерно каждые 20 минут, при условии, что служба запущена.</span><span class="sxs-lookup"><span data-stu-id="f4bc2-164">Note that the initial sync will take longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="f4bc2-165">В разделе **Сведения о синхронизации** можно отслеживать ход синхронизации и с помощью ссылок просматривать отчеты по подготовке, в которых описаны все действия, выполняемые службой подготовки в отношении приложения LinkedIn Lookup.</span><span class="sxs-lookup"><span data-stu-id="f4bc2-165">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your LinkedIn Lookup app.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="f4bc2-166">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="f4bc2-166">Additional Resources</span></span>

* [<span data-ttu-id="f4bc2-167">Управление подготовкой учетных записей пользователей для корпоративных приложений</span><span class="sxs-lookup"><span data-stu-id="f4bc2-167">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="f4bc2-168">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f4bc2-168">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
