---
title: "Руководство по настройке Slack для автоматической подготовки пользователей с помощью Azure Active Directory | Документация Майкрософт"
description: "Узнайте, как tooconfigure Azure Active Directory tooautomatically подготовки и Отмена подготовки учетных записей пользователей tooSlack."
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
ms.openlocfilehash: d0a565bbe0bd7e229b9dd99b1ebbaf67d93a2206
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-slack-for-automatic-user-provisioning"></a><span data-ttu-id="cc70f-103">Tutorial: Configuring Slack for Automatic User Provisioning (Учебник. Настройка Slack для автоматической подготовки пользователей)</span><span class="sxs-lookup"><span data-stu-id="cc70f-103">Tutorial: Configuring Slack for Automatic User Provisioning</span></span>


<span data-ttu-id="cc70f-104">Hello цель этого учебника — tooshow hello действия, которые следует tooperform в Slack и Azure AD tooautomatically подготовки и Отмена подготовки учетных записей пользователей из Azure AD tooSlack.</span><span class="sxs-lookup"><span data-stu-id="cc70f-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Slack and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooSlack.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="cc70f-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="cc70f-105">Prerequisites</span></span>

<span data-ttu-id="cc70f-106">Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="cc70f-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="cc70f-107">Клиент Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cc70f-107">An Azure Active Active directory tenant</span></span>
*   <span data-ttu-id="cc70f-108">Резерв клиента с hello [плюс плана](https://aadsyncfabric.slack.com/pricing) или лучше включена</span><span class="sxs-lookup"><span data-stu-id="cc70f-108">A Slack tenant with hello [Plus plan](https://aadsyncfabric.slack.com/pricing) or better enabled</span></span> 
*   <span data-ttu-id="cc70f-109">Учетная запись пользователя в Slack с разрешениями администратора группы</span><span class="sxs-lookup"><span data-stu-id="cc70f-109">A user account in Slack with Team Admin permissions</span></span> 

<span data-ttu-id="cc70f-110">Примечание: hello подготовки интеграции Azure AD использует hello [Slack SCIM API](https://api.slack.com/scim) это tooSlack доступных команд в hello плюс плана или более поздней.</span><span class="sxs-lookup"><span data-stu-id="cc70f-110">Note: hello Azure AD provisioning integration relies on hello [Slack SCIM API](https://api.slack.com/scim) which is available tooSlack teams on hello Plus plan or better.</span></span>

## <a name="assigning-users-tooslack"></a><span data-ttu-id="cc70f-111">Назначение пользователей tooSlack</span><span class="sxs-lookup"><span data-stu-id="cc70f-111">Assigning users tooSlack</span></span>

<span data-ttu-id="cc70f-112">Azure Active Directory использует называемый «назначения» toodetermine пользователей, которые должны получать доступ tooselected приложений.</span><span class="sxs-lookup"><span data-stu-id="cc70f-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="cc70f-113">В контексте hello автоматический подготовки пользователей. учетной записи будут синхронизированы только hello пользователей и групп, назначенных» «tooan приложения в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cc70f-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD will be synchronized.</span></span> 

<span data-ttu-id="cc70f-114">Для настройки и включения hello подготовки службы, вам потребуется toodecide какие пользователи или группы в Azure AD представляют Привет пользователям требуется доступ к приложению резерв tooyour.</span><span class="sxs-lookup"><span data-stu-id="cc70f-114">Before configuring and enabling hello provisioning service, you will need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Slack app.</span></span> <span data-ttu-id="cc70f-115">После приняла решение, можно назначить эти приложения резерв tooyour пользователей в соответствии с инструкциями hello здесь:</span><span class="sxs-lookup"><span data-stu-id="cc70f-115">Once decided, you can assign these users tooyour Slack app by following hello instructions here:</span></span>

[<span data-ttu-id="cc70f-116">Назначить пользователю или группе tooan корпоративного приложения</span><span class="sxs-lookup"><span data-stu-id="cc70f-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-tooslack"></a><span data-ttu-id="cc70f-117">Важные советы для назначения пользователей tooSlack</span><span class="sxs-lookup"><span data-stu-id="cc70f-117">Important tips for assigning users tooSlack</span></span>

*   <span data-ttu-id="cc70f-118">Рекомендуется один назначить hello tootest tooSlack настройки подготовки пользователя Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cc70f-118">It is recommended that a single Azure AD user be assigned tooSlack tootest hello provisioning configuration.</span></span> <span data-ttu-id="cc70f-119">Дополнительные пользователи и/или группы можно назначить позднее.</span><span class="sxs-lookup"><span data-stu-id="cc70f-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="cc70f-120">При назначении tooSlack пользователя, необходимо выбрать hello **пользователя** или роли «Группа» в диалоговом окне приветствия назначения.</span><span class="sxs-lookup"><span data-stu-id="cc70f-120">When assigning a user tooSlack, you must select hello **User** or "Group" role in hello assignment dialog.</span></span> <span data-ttu-id="cc70f-121">роль «Доступ по умолчанию» Hello не работает для подготовки.</span><span class="sxs-lookup"><span data-stu-id="cc70f-121">hello "Default Access" role does not work for provisioning.</span></span>


## <a name="configuring-user-provisioning-tooslack"></a><span data-ttu-id="cc70f-122">Настройка подготовки tooSlack пользователей</span><span class="sxs-lookup"><span data-stu-id="cc70f-122">Configuring user provisioning tooSlack</span></span> 

<span data-ttu-id="cc70f-123">Этот раздел поможет выполнить подключение учетной записи пользователя в Azure AD tooSlack подготовки API и настройке подготовки службы toocreate hello, обновления и отключить учетные записи пользователей, назначенные в Slack, в зависимости от назначения пользователей и групп в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cc70f-123">This section guides you through connecting your Azure AD tooSlack's user account provisioning API, and configuring hello provisioning service toocreate, update and disable assigned user accounts in Slack based on user and group assignment in Azure AD.</span></span>

<span data-ttu-id="cc70f-124">**Совет:** можно также выбрать tooenabled на основе SAML единого входа для Slack, следуя инструкциям hello в (портал Azure) [https://portal.azure.com].</span><span class="sxs-lookup"><span data-stu-id="cc70f-124">**Tip:** You may also choose tooenabled SAML-based Single Sign-On for Slack, following hello instructions provided in (Azure portal)[https://portal.azure.com].</span></span> <span data-ttu-id="cc70f-125">Единый вход можно настроить независимо от автоматической подготовки, хотя эти две возможности дополняют друг друга.</span><span class="sxs-lookup"><span data-stu-id="cc70f-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="tooconfigure-automatic-user-account-provisioning-tooslack-in-azure-ad"></a><span data-ttu-id="cc70f-126">tooconfigure автоматическая учетная запись подготовки tooSlack в Azure AD:</span><span class="sxs-lookup"><span data-stu-id="cc70f-126">tooconfigure automatic user account provisioning tooSlack in Azure AD:</span></span>


1)  <span data-ttu-id="cc70f-127">В hello [портал Azure](https://portal.azure.com), Обзор toohello **Azure Active Directory > корпоративных приложений > все приложения** раздела.</span><span class="sxs-lookup"><span data-stu-id="cc70f-127">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2) <span data-ttu-id="cc70f-128">Если вы уже настроили резерв для единого входа, поиск экземпляра Slack, с помощью поля поиска hello.</span><span class="sxs-lookup"><span data-stu-id="cc70f-128">If you have already configured Slack for single sign-on, search for your instance of Slack using hello search field.</span></span> <span data-ttu-id="cc70f-129">В противном случае выберите **добавить** и выполните поиск **Slack** в галерее приложения hello.</span><span class="sxs-lookup"><span data-stu-id="cc70f-129">Otherwise, select **Add** and search for **Slack** in hello application gallery.</span></span> <span data-ttu-id="cc70f-130">Выберите Slack из результатов поиска hello и добавить его в список tooyour приложений.</span><span class="sxs-lookup"><span data-stu-id="cc70f-130">Select Slack from hello search results, and add it tooyour list of applications.</span></span>

3)  <span data-ttu-id="cc70f-131">Выберите свой экземпляр резерва, а затем выберите hello **Provisioning** вкладки.</span><span class="sxs-lookup"><span data-stu-id="cc70f-131">Select your instance of Slack, then select hello **Provisioning** tab.</span></span>

4)  <span data-ttu-id="cc70f-132">Набор hello **режим подготовки** слишком**автоматического**.</span><span class="sxs-lookup"><span data-stu-id="cc70f-132">Set hello **Provisioning Mode** too**Automatic**.</span></span>

![Подготовка Slack](./media/active-directory-saas-slack-provisioning-tutorial/Slack1.PNG)

5)  <span data-ttu-id="cc70f-134">В разделе hello **учетные данные администратора** щелкните **авторизовать**.</span><span class="sxs-lookup"><span data-stu-id="cc70f-134">Under hello **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="cc70f-135">В новом окне браузера откроется диалоговое окно авторизации Slack.</span><span class="sxs-lookup"><span data-stu-id="cc70f-135">This opens a Slack authorization dialog in a new browser window.</span></span> 

6) <span data-ttu-id="cc70f-136">В новом окне приветствия войти в Slack, с помощью учетной записи администратора команды.</span><span class="sxs-lookup"><span data-stu-id="cc70f-136">In hello new window, sign into Slack using your Team Admin account.</span></span> <span data-ttu-id="cc70f-137">в hello результирующее диалоговое окно авторизации, выберите hello резерв команды, которые tooenable инициализацию и затем выберите **авторизовать**.</span><span class="sxs-lookup"><span data-stu-id="cc70f-137">in hello resulting authorization dialog, select hello Slack team that you want tooenable provisioning for, and then select **Authorize**.</span></span> <span data-ttu-id="cc70f-138">Hello Azure портала toocomplete после ее завершения, возвращаемый toohello настройки подготовки.</span><span class="sxs-lookup"><span data-stu-id="cc70f-138">Once completed, return toohello Azure portal toocomplete hello provisioning configuration.</span></span>

![Диалоговое окно авторизации](./media/active-directory-saas-slack-provisioning-tutorial/Slack3.PNG)

7) <span data-ttu-id="cc70f-140">В hello портал Azure, щелкните **проверить подключение** tooensure Azure AD можно подключить tooyour резерв приложение.</span><span class="sxs-lookup"><span data-stu-id="cc70f-140">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Slack app.</span></span> <span data-ttu-id="cc70f-141">При сбое подключения hello, убедитесь, что резерв учетная запись имеет разрешения администратора команды и повторите попытку шаг «Авторизовать» hello.</span><span class="sxs-lookup"><span data-stu-id="cc70f-141">If hello connection fails, ensure your Slack account has Team Admin permissions and try hello "Authorize" step again.</span></span>

8) <span data-ttu-id="cc70f-142">Введите адрес электронной почты hello пользователя или группы, которые должны получить уведомления о подготовке ошибки в hello **уведомление по электронной почте** поле и установите флажок "hello" ниже.</span><span class="sxs-lookup"><span data-stu-id="cc70f-142">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox below.</span></span>

9) <span data-ttu-id="cc70f-143">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="cc70f-143">Click **Save**.</span></span> 

10) <span data-ttu-id="cc70f-144">Установите hello сопоставлений **tooSlack синхронизации Azure Active Directory — пользователи**.</span><span class="sxs-lookup"><span data-stu-id="cc70f-144">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooSlack**.</span></span>

11) <span data-ttu-id="cc70f-145">В hello **сопоставления атрибутов** просмотрите hello атрибутов пользователей, которые будут синхронизированы из tooSlack Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cc70f-145">In hello **Attribute Mappings** section, review hello user attributes that will be synchronized from Azure AD tooSlack.</span></span> <span data-ttu-id="cc70f-146">Обратите внимание, что атрибуты, выбранные в качестве hello **сопоставление** свойства будут использоваться toomatch hello учетных записей пользователей в Slack для операций обновления.</span><span class="sxs-lookup"><span data-stu-id="cc70f-146">Note that hello attributes selected as **Matching** properties will be used toomatch hello user accounts in Slack for update operations.</span></span> <span data-ttu-id="cc70f-147">Выберите toocommit кнопку hello сохранить все изменения.</span><span class="sxs-lookup"><span data-stu-id="cc70f-147">Select hello Save button toocommit any changes.</span></span>

12) <span data-ttu-id="cc70f-148">tooenable hello подготовки службы Azure AD для Slack, изменение hello **состояние подготовки** слишком**на** в hello **параметры** раздела</span><span class="sxs-lookup"><span data-stu-id="cc70f-148">tooenable hello Azure AD provisioning service for Slack, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

13) <span data-ttu-id="cc70f-149">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="cc70f-149">Click **Save**.</span></span> 

<span data-ttu-id="cc70f-150">Это приведет к запуску hello первоначальной синхронизации все пользователи и группы, назначенные tooSlack в hello пользователей и группы раздела.</span><span class="sxs-lookup"><span data-stu-id="cc70f-150">This will start hello initial synchronization of any users and/or groups assigned tooSlack in hello Users and Groups section.</span></span> <span data-ttu-id="cc70f-151">Обратите внимание, что hello начальной синхронизации будет иметь tooperform больше времени, чем последующие синхронизации, которые происходят примерно каждые 10 минут, при условии, что запущена служба hello.</span><span class="sxs-lookup"><span data-stu-id="cc70f-151">Note that hello initial sync will take longer tooperform than subsequent syncs, which occur approximately every 10 minutes as long as hello service is running.</span></span> <span data-ttu-id="cc70f-152">Можно использовать hello **сведения о синхронизации** статьи toomonitor хода выполнения и следуйте ссылки tooprovisioning отчеты о действиях, описывающих все действия, выполняемые hello подготовки службы в приложении резерв.</span><span class="sxs-lookup"><span data-stu-id="cc70f-152">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Slack app.</span></span>

## <a name="optional-configuring-group-object-provisioning-tooslack"></a><span data-ttu-id="cc70f-153">[Необязательно] Настройка подготовки tooSlack объекта группы</span><span class="sxs-lookup"><span data-stu-id="cc70f-153">[Optional] Configuring group object provisioning tooSlack</span></span> 

<span data-ttu-id="cc70f-154">При необходимости можно включить hello подготовки группы объектов из tooSlack Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cc70f-154">Optionally, you can enable hello provisioning of group objects from Azure AD tooSlack.</span></span> <span data-ttu-id="cc70f-155">Это поведение отличается от «присвоение группы пользователей», в этом объекте фактической группой hello Кроме tooits члены будут реплицированы с tooSlack Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cc70f-155">This is different from "assigning groups of users", in that hello actual group object in addition tooits members will be replicated from Azure AD tooSlack.</span></span> <span data-ttu-id="cc70f-156">Например, если в Azure AD есть группа с именем "Моя группа", идентичная группа с именем "Моя группа" будет создана в Slack.</span><span class="sxs-lookup"><span data-stu-id="cc70f-156">For example, if you have a group named "My Group" in Azure AD, an identitical group named "My Group" will be created inside Slack.</span></span>

### <a name="tooenable-provisioning-of-group-objects"></a><span data-ttu-id="cc70f-157">tooenable Подготовка группы объектов:</span><span class="sxs-lookup"><span data-stu-id="cc70f-157">tooenable provisioning of group objects:</span></span>

1) <span data-ttu-id="cc70f-158">Установите hello сопоставлений **tooSlack синхронизации группы Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cc70f-158">Under hello Mappings section, select **Synchronize Azure Active Directory Groups tooSlack**.</span></span>

2) <span data-ttu-id="cc70f-159">В колонке сопоставление атрибутов hello задайте tooYes включено.</span><span class="sxs-lookup"><span data-stu-id="cc70f-159">In hello Attribute Mapping blade, set Enabled tooYes.</span></span>

3) <span data-ttu-id="cc70f-160">В hello **сопоставления атрибутов** просмотрите hello группы атрибутов, которые будут синхронизированы из tooSlack Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cc70f-160">In hello **Attribute Mappings** section, review hello group attributes that will be synchronized from Azure AD tooSlack.</span></span> <span data-ttu-id="cc70f-161">Обратите внимание, что атрибуты, выбранные в качестве hello **сопоставление** свойства будут групп используется toomatch hello в Slack для операций обновления.</span><span class="sxs-lookup"><span data-stu-id="cc70f-161">Note that hello attributes selected as **Matching** properties will be used toomatch hello groups in Slack for update operations.</span></span> 

4) <span data-ttu-id="cc70f-162">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="cc70f-162">Click **Save**.</span></span>

<span data-ttu-id="cc70f-163">Это приведет к tooSlack объекты, связанные с любой группы в hello **пользователей и групп** статьи полностью синхронизируются с Azure AD tooSlack.</span><span class="sxs-lookup"><span data-stu-id="cc70f-163">This result in any group objects assigned tooSlack in hello **Users and Groups** section being fully synchronized from Azure AD tooSlack.</span></span> <span data-ttu-id="cc70f-164">Можно использовать hello **сведения о синхронизации** статьи toomonitor хода выполнения и следуйте ссылки tooprovisioning отчеты о действиях, описывающих все действия, выполняемые hello подготовки службы в приложении резерв.</span><span class="sxs-lookup"><span data-stu-id="cc70f-164">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Slack app.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="cc70f-165">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="cc70f-165">Additional Resources</span></span>

* [<span data-ttu-id="cc70f-166">Управление подготовкой учетных записей пользователей для корпоративных приложений</span><span class="sxs-lookup"><span data-stu-id="cc70f-166">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="cc70f-167">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cc70f-167">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
