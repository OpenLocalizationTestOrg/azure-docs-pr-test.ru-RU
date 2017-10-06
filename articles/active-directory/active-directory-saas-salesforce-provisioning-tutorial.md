---
title: "Руководство по интеграции Azure Active Directory с Salesforce | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Salesforce."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 49384b8b-3836-4eb1-b438-1c46bb9baf6f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: a916be8dbf0b4c6173cda873936a53cd1f3ff12b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-salesforce-for-automatic-user-provisioning"></a><span data-ttu-id="5d039-103">Руководство по настройке Salesforce для автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="5d039-103">Tutorial: Configuring Salesforce for Automatic User Provisioning</span></span>

<span data-ttu-id="5d039-104">Цель этого учебника Hello — tooshow hello действия требуется tooperform в Salesforce и Azure AD tooautomatically подготовки и Отмена подготовки учетных записей пользователей из Azure AD tooSalesforce.</span><span class="sxs-lookup"><span data-stu-id="5d039-104">hello objective of this tutorial is tooshow hello steps required tooperform in Salesforce and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooSalesforce.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5d039-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5d039-105">Prerequisites</span></span>

<span data-ttu-id="5d039-106">Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="5d039-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="5d039-107">клиент Azure Active Directory;</span><span class="sxs-lookup"><span data-stu-id="5d039-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="5d039-108">У вас должен быть действительный клиент для работы с Salesforce for Work или Salesforce for Education.</span><span class="sxs-lookup"><span data-stu-id="5d039-108">You must have a valid tenant for Salesforce for Work or Salesforce for Education.</span></span> <span data-ttu-id="5d039-109">Для любой из этих служб можно воспользоваться бесплатной пробной учетной записью.</span><span class="sxs-lookup"><span data-stu-id="5d039-109">You may use a free trial     account for either service.</span></span>
*   <span data-ttu-id="5d039-110">Учетная запись пользователя в Salesforce с разрешениями администратора группы.</span><span class="sxs-lookup"><span data-stu-id="5d039-110">A user account in Salesforce with Team Admin permissions.</span></span>

## <a name="assigning-users-toosalesforce"></a><span data-ttu-id="5d039-111">Назначение пользователей tooSalesforce</span><span class="sxs-lookup"><span data-stu-id="5d039-111">Assigning users tooSalesforce</span></span>

<span data-ttu-id="5d039-112">Azure Active Directory использует называемый «назначения» toodetermine пользователей, которые должны получать доступ tooselected приложений.</span><span class="sxs-lookup"><span data-stu-id="5d039-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="5d039-113">В контексте hello автоматический подготовки пользователей. учетной записи синхронизируются только hello пользователей и групп, назначенных» «tooan приложения в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5d039-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="5d039-114">Для настройки и включения hello подготовки службы, требуется toodecide какие пользователи и группы в Azure AD представляют Привет пользователей, которым требуется доступ к приложению Salesforce tooyour.</span><span class="sxs-lookup"><span data-stu-id="5d039-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Salesforce app.</span></span> <span data-ttu-id="5d039-115">После приняла решение, можно назначить эти приложения пользователям tooyour Salesforce, следуя инструкциям hello:</span><span class="sxs-lookup"><span data-stu-id="5d039-115">Once decided, you can assign these users tooyour Salesforce app by following hello instructions here:</span></span>

[<span data-ttu-id="5d039-116">Назначить пользователю или группе tooan корпоративного приложения</span><span class="sxs-lookup"><span data-stu-id="5d039-116">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toosalesforce"></a><span data-ttu-id="5d039-117">Важные советы для назначения пользователей tooSalesforce</span><span class="sxs-lookup"><span data-stu-id="5d039-117">Important tips for assigning users tooSalesforce</span></span>

*   <span data-ttu-id="5d039-118">Рекомендуется один назначенный hello tootest tooSalesforce настройки подготовки пользователя Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5d039-118">It is recommended that a single Azure AD user is assigned tooSalesforce tootest hello provisioning configuration.</span></span> <span data-ttu-id="5d039-119">Дополнительные пользователи и/или группы можно назначить позднее.</span><span class="sxs-lookup"><span data-stu-id="5d039-119">Additional users and/or groups may be assigned later.</span></span>

*  <span data-ttu-id="5d039-120">При назначении tooSalesforce пользователя, необходимо выбрать допустимой роли пользователя.</span><span class="sxs-lookup"><span data-stu-id="5d039-120">When assigning a user tooSalesforce, you must select a valid user role.</span></span> <span data-ttu-id="5d039-121">роль «Доступ по умолчанию» Hello не работает для подготовки</span><span class="sxs-lookup"><span data-stu-id="5d039-121">hello "Default Access" role does not work for provisioning</span></span>

    > [!NOTE]
    > <span data-ttu-id="5d039-122">Это приложение импортирует пользовательские роли из Salesforce в рамках hello подготовке, какой клиент hello может потребоваться tooselect при назначении пользователей</span><span class="sxs-lookup"><span data-stu-id="5d039-122">This app imports custom roles from Salesforce as part of hello provisioning process, which hello customer may want tooselect when assigning users</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="5d039-123">Включение автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="5d039-123">Enable Automated User Provisioning</span></span>

<span data-ttu-id="5d039-124">Этот раздел поможет выполнить подключение учетной записи пользователя в Azure AD tooSalesforce подготовки API и настройке подготовки службы toocreate hello, обновления и отключить учетные записи пользователей, назначенные в Salesforce, в зависимости от назначения пользователей и групп в Azure AD .</span><span class="sxs-lookup"><span data-stu-id="5d039-124">This section guides you through connecting your Azure AD tooSalesforce's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Salesforce based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="5d039-125">Можно также выбрать tooenabled на основе SAML единого входа для Salesforce, следуя инструкциям hello в [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5d039-125">You may also choose tooenabled SAML-based Single Sign-On for Salesforce, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="5d039-126">Единый вход можно настроить независимо от автоматической подготовки, хотя эти две возможности дополняют друг друга.</span><span class="sxs-lookup"><span data-stu-id="5d039-126">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-automatic-user-account-provisioning"></a><span data-ttu-id="5d039-127">tooconfigure автоматический подготовки пользователей. учетной записи:</span><span class="sxs-lookup"><span data-stu-id="5d039-127">tooconfigure automatic user account provisioning:</span></span>

<span data-ttu-id="5d039-128">Цель этого раздела Hello является toooutline как tooenable пользователя Подготовка пользователя Active Directory учетных записей tooSalesforce.</span><span class="sxs-lookup"><span data-stu-id="5d039-128">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooSalesforce.</span></span>

1. <span data-ttu-id="5d039-129">В hello [портал Azure](https://portal.azure.com), Обзор toohello **Azure Active Directory > корпоративных приложений > все приложения** раздела.</span><span class="sxs-lookup"><span data-stu-id="5d039-129">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="5d039-130">Если вы уже настроили Salesforce для единого входа, поиск экземпляра Salesforce с помощью поля поиска hello.</span><span class="sxs-lookup"><span data-stu-id="5d039-130">If you have already configured Salesforce for single sign-on, search for your instance of Salesforce using hello search field.</span></span> <span data-ttu-id="5d039-131">В противном случае выберите **добавить** и выполните поиск **Salesforce** в галерее приложения hello.</span><span class="sxs-lookup"><span data-stu-id="5d039-131">Otherwise, select **Add** and search for **Salesforce** in hello application gallery.</span></span> <span data-ttu-id="5d039-132">Выберите Salesforce из результатов поиска hello и добавить его в список tooyour приложений.</span><span class="sxs-lookup"><span data-stu-id="5d039-132">Select Salesforce from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="5d039-133">Выберите свой экземпляр Salesforce, а затем выберите hello **Provisioning** вкладки.</span><span class="sxs-lookup"><span data-stu-id="5d039-133">Select your instance of Salesforce, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="5d039-134">Набор hello **режим подготовки** слишком**автоматического**.</span><span class="sxs-lookup"><span data-stu-id="5d039-134">Set hello **Provisioning Mode** too**Automatic**.</span></span> 
<span data-ttu-id="5d039-135">![подготовка](./media/active-directory-saas-salesforce-provisioning-tutorial/provisioning.png)</span><span class="sxs-lookup"><span data-stu-id="5d039-135">![provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/provisioning.png)</span></span>

5. <span data-ttu-id="5d039-136">В разделе hello **учетные данные администратора** статьи, предоставляют hello следующие параметры конфигурации:</span><span class="sxs-lookup"><span data-stu-id="5d039-136">Under hello **Admin Credentials** section, provide hello following configuration settings:</span></span>
   
    <span data-ttu-id="5d039-137">а.</span><span class="sxs-lookup"><span data-stu-id="5d039-137">a.</span></span> <span data-ttu-id="5d039-138">В hello **имя пользователя администратора** введите имя, которое имеет hello учетной записи Salesforce **системный администратор** профиля в Salesforce.com.</span><span class="sxs-lookup"><span data-stu-id="5d039-138">In hello **Admin User Name** textbox, type a Salesforce account name that has hello **System Administrator** profile in Salesforce.com assigned.</span></span>
   
    <span data-ttu-id="5d039-139">b.</span><span class="sxs-lookup"><span data-stu-id="5d039-139">b.</span></span> <span data-ttu-id="5d039-140">В hello **пароль администратора** текстового поля, типа hello пароль для этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="5d039-140">In hello **Admin Password** textbox, type hello password for this account.</span></span>

6. <span data-ttu-id="5d039-141">tooget Salesforce маркера безопасности, откройте новую вкладку и войти в hello же учетная запись администратора Salesforce.</span><span class="sxs-lookup"><span data-stu-id="5d039-141">tooget your Salesforce security token, open a new tab and sign into hello same Salesforce admin account.</span></span> <span data-ttu-id="5d039-142">На hello правом верхнем углу страницы приветствия, щелкните свое имя и нажмите кнопку **мои параметры**.</span><span class="sxs-lookup"><span data-stu-id="5d039-142">On hello top right corner of hello page, click your name, and then click **My Settings**.</span></span>

     <span data-ttu-id="5d039-143">![Включение автоматической подготовки пользователей](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-my-settings.png "Включение автоматической подготовки пользователей")</span><span class="sxs-lookup"><span data-stu-id="5d039-143">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-my-settings.png "Enable automatic user provisioning")</span></span>
7. <span data-ttu-id="5d039-144">На панели навигации слева hello, нажмите кнопку **личных** tooexpand hello соответствующий раздел и нажмите кнопку **Сброс личного токена безопасности**.</span><span class="sxs-lookup"><span data-stu-id="5d039-144">On hello left navigation pane, click **Personal** tooexpand hello related section, and then click **Reset My Security Token**.</span></span>
  
    <span data-ttu-id="5d039-145">![Включение автоматической подготовки пользователей](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-personal-reset.png "Включение автоматической подготовки пользователей")</span><span class="sxs-lookup"><span data-stu-id="5d039-145">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-personal-reset.png "Enable automatic user provisioning")</span></span>
8. <span data-ttu-id="5d039-146">На hello **Сброс личного токена безопасности** щелкните **сбросить токен безопасности** кнопки.</span><span class="sxs-lookup"><span data-stu-id="5d039-146">On hello **Reset My Security Token** page, click **Reset Security Token** button.</span></span>

    <span data-ttu-id="5d039-147">![Включение автоматической подготовки пользователей](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-reset-token.png "Включение автоматической подготовки пользователей")</span><span class="sxs-lookup"><span data-stu-id="5d039-147">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-reset-token.png "Enable automatic user provisioning")</span></span>
9. <span data-ttu-id="5d039-148">Проверьте папки "Входящие" hello электронной почты для этой учетной записи администратора.</span><span class="sxs-lookup"><span data-stu-id="5d039-148">Check hello email inbox associated with this admin account.</span></span> <span data-ttu-id="5d039-149">Найдите сообщение электронной почты от Salesforce.com, содержащий hello новый маркер безопасности.</span><span class="sxs-lookup"><span data-stu-id="5d039-149">Look for an email from Salesforce.com that contains hello new security token.</span></span>
10. <span data-ttu-id="5d039-150">Hello токена, перейдите tooyour окна Azure AD скопируйте и вставьте его в hello **сокета маркера** поля.</span><span class="sxs-lookup"><span data-stu-id="5d039-150">Copy hello token, go tooyour Azure AD window, and paste it into hello **Socket Token** field.</span></span>

11. <span data-ttu-id="5d039-151">В hello портал Azure, щелкните **проверить подключение** tooensure Azure AD можно подключить приложение tooyour Salesforce.</span><span class="sxs-lookup"><span data-stu-id="5d039-151">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Salesforce app.</span></span>

12. <span data-ttu-id="5d039-152">В hello **уведомление по электронной почте** введите hello адрес электронной почты пользователя или группы, которые должны получать уведомления о подготовке ошибки и установите флажок "hello" ниже.</span><span class="sxs-lookup"><span data-stu-id="5d039-152">In hello **Notification Email** field, enter hello email address of a person or group who should receive provisioning error notifications, and check hello checkbox below.</span></span>

13. <span data-ttu-id="5d039-153">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="5d039-153">Click **Save.**</span></span>  
    
14.  <span data-ttu-id="5d039-154">Установите hello сопоставлений **tooSalesforce синхронизации Azure Active Directory — пользователи.**</span><span class="sxs-lookup"><span data-stu-id="5d039-154">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooSalesforce.**</span></span>

15. <span data-ttu-id="5d039-155">В hello **сопоставления атрибутов** просмотрите hello атрибутов пользователей, которые синхронизируются из tooSalesforce Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5d039-155">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooSalesforce.</span></span> <span data-ttu-id="5d039-156">Обратите внимание, что атрибуты, выбранные в качестве hello **сопоставление** свойства, используемые toomatch hello учетные записи пользователей в Salesforce для операции обновления.</span><span class="sxs-lookup"><span data-stu-id="5d039-156">Note that hello attributes selected as **Matching** properties are used toomatch hello user accounts in Salesforce for update operations.</span></span> <span data-ttu-id="5d039-157">Выберите toocommit кнопку hello сохранить все изменения.</span><span class="sxs-lookup"><span data-stu-id="5d039-157">Select hello Save button toocommit any changes.</span></span>

16. <span data-ttu-id="5d039-158">tooenable hello подготовки службы Azure AD для Salesforce, изменение hello **состояние подготовки** слишком**на** в разделе "Параметры" hello</span><span class="sxs-lookup"><span data-stu-id="5d039-158">tooenable hello Azure AD provisioning service for Salesforce, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

17. <span data-ttu-id="5d039-159">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="5d039-159">Click **Save.**</span></span>

<span data-ttu-id="5d039-160">При этом запустится hello первоначальной синхронизации все пользователи и группы, назначенные tooSalesforce в hello пользователей и группы раздела.</span><span class="sxs-lookup"><span data-stu-id="5d039-160">This starts hello initial synchronization of any users and/or groups assigned tooSalesforce in hello Users and Groups section.</span></span> <span data-ttu-id="5d039-161">Обратите внимание, что начальная синхронизация hello принимает tooperform больше времени, чем последующие синхронизации, которые происходят примерно каждые 20 минут при условии, что запущена служба hello.</span><span class="sxs-lookup"><span data-stu-id="5d039-161">Note that hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="5d039-162">Можно использовать hello **сведения о синхронизации** статьи toomonitor хода выполнения и следуйте ссылки tooprovisioning отчеты о действиях, которые описывают все действия, выполняемые hello подготовки службы приложения Salesforce.</span><span class="sxs-lookup"><span data-stu-id="5d039-162">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Salesforce app.</span></span>

<span data-ttu-id="5d039-163">Теперь можно создать тестовую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="5d039-163">You can now create a test account.</span></span> <span data-ttu-id="5d039-164">Дождитесь копирование минут too20 tooverify, hello учетная запись была синхронизирована tooSalesforce.</span><span class="sxs-lookup"><span data-stu-id="5d039-164">Wait for up too20 minutes tooverify that hello account has been synchronized tooSalesforce.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5d039-165">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="5d039-165">Additional resources</span></span>

* [<span data-ttu-id="5d039-166">Управление подготовкой учетных записей пользователей для корпоративных приложений</span><span class="sxs-lookup"><span data-stu-id="5d039-166">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5d039-167">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5d039-167">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="5d039-168">Настройка единого входа</span><span class="sxs-lookup"><span data-stu-id="5d039-168">Configure Single Sign-on</span></span>](active-directory-saas-salesforce-tutorial.md)