---
title: "Руководство по настройке ZenDesk для автоматической подготовки пользователей с помощью Azure Active Directory | Документация Майкрософт"
description: "Узнайте, как tooconfigure Azure Active Directory tooautomatically подготовки и Отмена подготовки учетных записей пользователей tooZenDesk."
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
ms.openlocfilehash: 200e8790ec1755f5cf927274ceb38527dd993f3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-zendesk-for-automatic-user-provisioning"></a><span data-ttu-id="9db21-103">Руководство по настройке ZenDesk для автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="9db21-103">Tutorial: Configuring ZenDesk for Automatic User Provisioning</span></span>


<span data-ttu-id="9db21-104">Цель этого учебника Hello — hello действия, которые следует tooperform в ZenDesk и Azure AD tooautomatically подготовки и Отмена подготовки учетных записей пользователей из Azure AD tooZenDesk tooshow.</span><span class="sxs-lookup"><span data-stu-id="9db21-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in ZenDesk and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooZenDesk.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="9db21-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9db21-105">Prerequisites</span></span>

<span data-ttu-id="9db21-106">Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="9db21-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="9db21-107">клиент Azure Active Directory;</span><span class="sxs-lookup"><span data-stu-id="9db21-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="9db21-108">Клиент ZenDesk с hello [плана корпоративного](https://www.zendesk.com/product/pricing/) или лучше включена</span><span class="sxs-lookup"><span data-stu-id="9db21-108">A ZenDesk tenant with hello [Enterprise plan](https://www.zendesk.com/product/pricing/) or better enabled</span></span> 
*   <span data-ttu-id="9db21-109">учетная запись пользователя в ZenDesk с разрешениями администратора.</span><span class="sxs-lookup"><span data-stu-id="9db21-109">A user account in ZenDesk with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="9db21-110">Hello подготовки интеграции Azure AD использует hello [ZenDesk REST API](https://developer.zendesk.com/rest_api/docs/core/introduction#the-api), являющийся tooZenDesk доступные команды на Essential плана hello и более.</span><span class="sxs-lookup"><span data-stu-id="9db21-110">hello Azure AD provisioning integration relies on hello [ZenDesk REST API](https://developer.zendesk.com/rest_api/docs/core/introduction#the-api), which is available tooZenDesk teams on hello Essential plan or better.</span></span>

## <a name="assigning-users-toozendesk"></a><span data-ttu-id="9db21-111">Назначение пользователей tooZenDesk</span><span class="sxs-lookup"><span data-stu-id="9db21-111">Assigning users tooZenDesk</span></span>

<span data-ttu-id="9db21-112">Azure Active Directory использует называемый «назначения» toodetermine пользователей, которые должны получать доступ tooselected приложений.</span><span class="sxs-lookup"><span data-stu-id="9db21-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="9db21-113">В контексте hello автоматический подготовки пользователей. учетной записи синхронизируются только hello пользователей и групп, назначенных» «tooan приложения в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9db21-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD are synchronized.</span></span> 

<span data-ttu-id="9db21-114">Перед Настройка и включение hello подготовки службы, необходимо toodecide какие пользователи или группы в Azure AD представляют Привет пользователям требуется доступ к приложению tooyour ZenDesk.</span><span class="sxs-lookup"><span data-stu-id="9db21-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour ZenDesk app.</span></span> <span data-ttu-id="9db21-115">После приняла решение, можно назначить эти приложения пользователям tooyour ZenDesk в соответствии с инструкциями hello здесь:</span><span class="sxs-lookup"><span data-stu-id="9db21-115">Once decided, you can assign these users tooyour ZenDesk app by following hello instructions here:</span></span>

[<span data-ttu-id="9db21-116">Назначить пользователю или группе tooan корпоративного приложения</span><span class="sxs-lookup"><span data-stu-id="9db21-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toozendesk"></a><span data-ttu-id="9db21-117">Важные советы для назначения пользователей tooZenDesk</span><span class="sxs-lookup"><span data-stu-id="9db21-117">Important tips for assigning users tooZenDesk</span></span>

*   <span data-ttu-id="9db21-118">Рекомендуется один назначенный hello tootest tooZenDesk настройки подготовки пользователя Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9db21-118">It is recommended that a single Azure AD user is assigned tooZenDesk tootest hello provisioning configuration.</span></span> <span data-ttu-id="9db21-119">Дополнительные пользователи и/или группы можно назначить позднее.</span><span class="sxs-lookup"><span data-stu-id="9db21-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="9db21-120">При назначении tooZenDesk пользователя, необходимо выбрать либо hello **пользователя** роли или другой допустимый конкретного приложения (если доступно) в диалоговом окне приветствия назначения.</span><span class="sxs-lookup"><span data-stu-id="9db21-120">When assigning a user tooZenDesk, you must select either hello **User** role, or another valid application-specific role (if available) in hello assignment dialog.</span></span> <span data-ttu-id="9db21-121">Hello **доступа по умолчанию** роль не будет работать для подготовки, и эти пользователи будут пропускаться.</span><span class="sxs-lookup"><span data-stu-id="9db21-121">hello **Default Access** role does not work for provisioning, and these users are skipped.</span></span>

> [!NOTE]
> <span data-ttu-id="9db21-122">Добавлены функции hello подготовки службы считывает все пользовательские роли, определенные в Zendesk, а импортирует их в Azure AD, где они могут быть выбраны в диалоговом окне выберите роль hello.</span><span class="sxs-lookup"><span data-stu-id="9db21-122">As an added feature, hello provisioning service reads any custom roles defined in Zendesk, and imports them into Azure AD where they can be selected in hello Select Role dialog.</span></span> <span data-ttu-id="9db21-123">Эти роли будут отображаться в hello портал Azure, после включения hello подготовки службы, и завершена одного цикла синхронизации.</span><span class="sxs-lookup"><span data-stu-id="9db21-123">These roles will be visible in hello Azure portal after hello provisioning service is enabled and one synchronization cycle has completed.</span></span>

## <a name="configuring-user-provisioning-toozendesk"></a><span data-ttu-id="9db21-124">Настройка подготовки tooZenDesk пользователей</span><span class="sxs-lookup"><span data-stu-id="9db21-124">Configuring user provisioning tooZenDesk</span></span> 

<span data-ttu-id="9db21-125">Этот раздел поможет выполнить подключение учетной записи пользователя в Azure AD tooZenDesk подготовки API и настройке подготовки службы toocreate hello, обновления и отключить учетные записи пользователей, назначенные в ZenDesk, в зависимости от назначения пользователей и групп в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9db21-125">This section guides you through connecting your Azure AD tooZenDesk's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in ZenDesk based on user and group assignment in Azure AD.</span></span>

> [!TIP] 
> <span data-ttu-id="9db21-126">Можно также выбрать tooenabled на основе SAML Single Sign-On для ZenDesk, следуя инструкциям hello в [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9db21-126">You may also choose tooenabled SAML-based Single Sign-On for ZenDesk, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="9db21-127">Единый вход можно настроить независимо от автоматической подготовки, хотя эти две возможности дополняют друг друга.</span><span class="sxs-lookup"><span data-stu-id="9db21-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-toozendesk-in-azure-ad"></a><span data-ttu-id="9db21-128">Настройка учетной записи автоматического пользователя подготовки tooZenDesk в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9db21-128">Configure automatic user account provisioning tooZenDesk in Azure AD</span></span>


1. <span data-ttu-id="9db21-129">В hello [портал Azure](https://portal.azure.com), Обзор toohello **Azure Active Directory > корпоративных приложений > все приложения** раздела.</span><span class="sxs-lookup"><span data-stu-id="9db21-129">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="9db21-130">Если вы уже настроили для единого входа ZenDesk, поиск экземпляра ZenDesk с помощью поля поиска hello.</span><span class="sxs-lookup"><span data-stu-id="9db21-130">If you have already configured ZenDesk for single sign-on, search for your instance of ZenDesk using hello search field.</span></span> <span data-ttu-id="9db21-131">В противном случае выберите **добавить** и выполните поиск **ZenDesk** в галерее приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9db21-131">Otherwise, select **Add** and search for **ZenDesk** in hello application gallery.</span></span> <span data-ttu-id="9db21-132">Выберите ZenDesk из результатов поиска hello и добавить его в список tooyour приложений.</span><span class="sxs-lookup"><span data-stu-id="9db21-132">Select ZenDesk from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="9db21-133">Выберите свой экземпляр ZenDesk, а затем выберите hello **Provisioning** вкладки.</span><span class="sxs-lookup"><span data-stu-id="9db21-133">Select your instance of ZenDesk, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="9db21-134">Набор hello **режим подготовки** слишком**автоматического**.</span><span class="sxs-lookup"><span data-stu-id="9db21-134">Set hello **Provisioning Mode** too**Automatic**.</span></span>

    ![Подготовка ZenDesk](./media/active-directory-saas-zendesk-provisioning-tutorial/ZenDesk1.png)

5. <span data-ttu-id="9db21-136">Под hello **учетные данные администратора** раздел, входной hello **пользователя с правами администратора & tokenkey & домена** созданные учетной записи на ZenDesk (hello токен можно найти в рамках учетной записи: **администратора**   >  **API** > **параметры**).</span><span class="sxs-lookup"><span data-stu-id="9db21-136">Under hello **Admin Credentials** section, input hello **Admin Username&tokenkey&Domain** generated by your ZenDesk's account (you can find hello token under your account: **Admin** > **API** > **Settings**).</span></span> 

    ![Подготовка ZenDesk](./media/active-directory-saas-zendesk-provisioning-tutorial/ZenDesk2.png)

6. <span data-ttu-id="9db21-138">В hello портал Azure, щелкните **проверить подключение** tooensure Azure AD можно подключить приложение tooyour ZenDesk.</span><span class="sxs-lookup"><span data-stu-id="9db21-138">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour ZenDesk app.</span></span> <span data-ttu-id="9db21-139">При сбое подключения hello, убедитесь, что ваша учетная запись ZenDesk имеет разрешения администратора и повторите шаг 5.</span><span class="sxs-lookup"><span data-stu-id="9db21-139">If hello connection fails, ensure your ZenDesk account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="9db21-140">Введите адрес электронной почты hello пользователя или группы, которые должны получить уведомления о подготовке ошибки в hello **уведомление по электронной почте** поле и проверьте hello флажок «Отправить уведомление по электронной почте при возникновении сбоя».</span><span class="sxs-lookup"><span data-stu-id="9db21-140">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="9db21-141">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="9db21-141">Click **Save**.</span></span> 

9. <span data-ttu-id="9db21-142">Установите hello сопоставлений **tooZenDesk синхронизации Azure Active Directory — пользователи**.</span><span class="sxs-lookup"><span data-stu-id="9db21-142">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooZenDesk**.</span></span>

10. <span data-ttu-id="9db21-143">В hello **сопоставления атрибутов** просмотрите hello атрибутов пользователей, которые синхронизируются из tooZenDesk Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9db21-143">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooZenDesk.</span></span> <span data-ttu-id="9db21-144">Здравствуйте, атрибуты, выбранные в качестве **сопоставление** свойства, используемые toomatch hello учетных записей пользователей в ZenDesk для операций обновления.</span><span class="sxs-lookup"><span data-stu-id="9db21-144">hello attributes selected as **Matching** properties are used toomatch hello user accounts in ZenDesk for update operations.</span></span> <span data-ttu-id="9db21-145">Выберите toocommit кнопку hello сохранить все изменения.</span><span class="sxs-lookup"><span data-stu-id="9db21-145">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="9db21-146">tooenable hello подготовки службы Azure AD для ZenDesk, изменение hello **состояние подготовки** слишком**на** в hello **параметры** раздела</span><span class="sxs-lookup"><span data-stu-id="9db21-146">tooenable hello Azure AD provisioning service for ZenDesk, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

12. <span data-ttu-id="9db21-147">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="9db21-147">Click **Save**.</span></span> 

<span data-ttu-id="9db21-148">Эта операция запускает hello первоначальной синхронизации все пользователи и группы, назначенные tooZenDesk в hello пользователей и группы раздела.</span><span class="sxs-lookup"><span data-stu-id="9db21-148">This operation starts hello initial synchronization of any users and/or groups assigned tooZenDesk in hello Users and Groups section.</span></span> <span data-ttu-id="9db21-149">Начальная синхронизация Hello принимает tooperform больше времени, чем последующие синхронизации, которые происходят примерно каждые 20 минут при условии, что запущена служба hello.</span><span class="sxs-lookup"><span data-stu-id="9db21-149">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="9db21-150">Можно использовать hello **сведения о синхронизации** статьи toomonitor хода выполнения и следуйте ссылки tooprovisioning отчеты о действиях, которые описывают все действия, выполняемые hello подготовки службы.</span><span class="sxs-lookup"><span data-stu-id="9db21-150">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service.</span></span>

<span data-ttu-id="9db21-151">Дополнительные сведения о способ подготовки tooread hello Azure AD использует для входа см. в разделе [отчеты о автоматический подготовки пользователей. учетной записи](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="9db21-151">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="9db21-152">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="9db21-152">Additional resources</span></span>

* [<span data-ttu-id="9db21-153">Управление подготовкой учетных записей пользователей для корпоративных приложений</span><span class="sxs-lookup"><span data-stu-id="9db21-153">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="9db21-154">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9db21-154">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="9db21-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9db21-155">Next steps</span></span>

* [<span data-ttu-id="9db21-156">Узнайте, каким образом ведет журнал tooreview и получать отчеты о действиях по подготовке</span><span class="sxs-lookup"><span data-stu-id="9db21-156">Learn how tooreview logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
