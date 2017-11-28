---
title: "Руководство по интеграции Azure Active Directory с Dropbox for Business | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Dropbox для бизнеса."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f3a42e4-6897-4234-af84-b47c148ec3e1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 0fb01eab4f7c6c4516eac64a4343e46ea221f98d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-dropbox-for-business-for-automatic-user-provisioning"></a><span data-ttu-id="f6342-103">Руководство по настройке автоматической подготовки пользователей в Dropbox for Business</span><span class="sxs-lookup"><span data-stu-id="f6342-103">Tutorial: Configuring Dropbox for Business for Automatic User Provisioning</span></span>

<span data-ttu-id="f6342-104">Цель этого учебника Hello — tooshow hello действия, которые следует tooperform в Dropbox для бизнеса и Azure AD tooautomatically подготовки и Отмена подготовки учетных записей пользователей из Azure AD tooDropbox для бизнеса.</span><span class="sxs-lookup"><span data-stu-id="f6342-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Dropbox for Business and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooDropbox for Business.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f6342-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f6342-105">Prerequisites</span></span>

<span data-ttu-id="f6342-106">Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="f6342-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="f6342-107">клиент Azure Active Directory;</span><span class="sxs-lookup"><span data-stu-id="f6342-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="f6342-108">подписка Dropbox for Business с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="f6342-108">A Dropbox for Business single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="f6342-109">Учетная запись пользователя в Dropbox for Business с разрешениями администратора группы.</span><span class="sxs-lookup"><span data-stu-id="f6342-109">A user account in Dropbox for Business with Team Admin permissions.</span></span>

## <a name="assigning-users-toodropbox-for-business"></a><span data-ttu-id="f6342-110">Назначение пользователей tooDropbox для бизнеса</span><span class="sxs-lookup"><span data-stu-id="f6342-110">Assigning users tooDropbox for Business</span></span>

<span data-ttu-id="f6342-111">Azure Active Directory использует называемый «назначения» toodetermine пользователей, которые должны получать доступ tooselected приложений.</span><span class="sxs-lookup"><span data-stu-id="f6342-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="f6342-112">В контексте hello автоматический подготовки пользователей. учетной записи синхронизируются только hello пользователей и групп, назначенных» «tooan приложения в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f6342-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="f6342-113">Для настройки и включения hello подготовки службы, требуется toodecide какие пользователи или группы в Azure AD представляют Привет пользователей, которым требуется доступ tooyour Dropbox для бизнес-приложения.</span><span class="sxs-lookup"><span data-stu-id="f6342-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Dropbox for Business app.</span></span> <span data-ttu-id="f6342-114">После приняла решение, можно назначить эти пользователи tooyour Dropbox для бизнес-приложения в соответствии с инструкциями hello здесь:</span><span class="sxs-lookup"><span data-stu-id="f6342-114">Once decided, you can assign these users tooyour Dropbox for Business app by following hello instructions here:</span></span>

[<span data-ttu-id="f6342-115">Назначить пользователю или группе tooan корпоративного приложения</span><span class="sxs-lookup"><span data-stu-id="f6342-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toodropbox-for-business"></a><span data-ttu-id="f6342-116">Важные советы для назначения пользователей tooDropbox для бизнеса</span><span class="sxs-lookup"><span data-stu-id="f6342-116">Important tips for assigning users tooDropbox for Business</span></span>

*   <span data-ttu-id="f6342-117">Рекомендуется один назначенный tooDropbox для бизнеса tootest hello настройки подготовки пользователя Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f6342-117">It is recommended that a single Azure AD user is assigned tooDropbox for Business tootest hello provisioning configuration.</span></span> <span data-ttu-id="f6342-118">Дополнительные пользователи и/или группы можно назначить позднее.</span><span class="sxs-lookup"><span data-stu-id="f6342-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="f6342-119">При назначении tooDropbox пользователя для бизнеса, необходимо выбрать допустимой роли пользователя.</span><span class="sxs-lookup"><span data-stu-id="f6342-119">When assigning a user tooDropbox for Business, you must select a valid user role.</span></span> <span data-ttu-id="f6342-120">роль «Доступ по умолчанию» Hello не работает для подготовки...</span><span class="sxs-lookup"><span data-stu-id="f6342-120">hello "Default Access" role does not work for provisioning..</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="f6342-121">Включение автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="f6342-121">Enable Automated User Provisioning</span></span>

<span data-ttu-id="f6342-122">Этот раздел поможет выполнить подключение tooDropbox к Azure AD для учетной записи пользователя организации подготовки API и настройке подготовки службы toocreate hello, обновления и отключить учетные записи пользователей, назначенные в Dropbox для бизнеса на основе пользователя и группы Назначение в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f6342-122">This section guides you through connecting your Azure AD tooDropbox for Business's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Dropbox for Business based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="f6342-123">Можно также выбрать tooenabled на основе SAML единого входа для Dropbox для бизнеса, следуя инструкциям hello в [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f6342-123">You may also choose tooenabled SAML-based Single Sign-On for Dropbox for Business, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="f6342-124">Единый вход можно настроить независимо от автоматической подготовки, хотя эти две возможности дополняют друг друга.</span><span class="sxs-lookup"><span data-stu-id="f6342-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-automatic-user-account-provisioning"></a><span data-ttu-id="f6342-125">tooconfigure автоматический подготовки пользователей. учетной записи:</span><span class="sxs-lookup"><span data-stu-id="f6342-125">tooconfigure automatic user account provisioning:</span></span>

1. <span data-ttu-id="f6342-126">В hello [портал Azure](https://portal.azure.com), Обзор toohello **Azure Active Directory > корпоративных приложений > все приложения** раздела.</span><span class="sxs-lookup"><span data-stu-id="f6342-126">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="f6342-127">Если вы уже настроили Dropbox для бизнеса для единого входа, поиск экземпляра Dropbox для бизнеса, с помощью поля поиска hello.</span><span class="sxs-lookup"><span data-stu-id="f6342-127">If you have already configured Dropbox for Business for single sign-on, search for your instance of Dropbox for Business using hello search field.</span></span> <span data-ttu-id="f6342-128">В противном случае выберите **добавить** и выполните поиск **Dropbox для бизнеса** в галерее приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f6342-128">Otherwise, select **Add** and search for **Dropbox for Business** in hello application gallery.</span></span> <span data-ttu-id="f6342-129">Выберите из результатов поиска hello Dropbox для бизнеса и добавьте его tooyour список приложений.</span><span class="sxs-lookup"><span data-stu-id="f6342-129">Select Dropbox for Business from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="f6342-130">Выберите свой экземпляр Dropbox для бизнеса, а затем выберите hello **Provisioning** вкладки.</span><span class="sxs-lookup"><span data-stu-id="f6342-130">Select your instance of Dropbox for Business, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="f6342-131">Набор hello **режим подготовки** слишком**автоматического**.</span><span class="sxs-lookup"><span data-stu-id="f6342-131">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![подготовка](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="f6342-133">В разделе hello **учетные данные администратора** щелкните **авторизовать**.</span><span class="sxs-lookup"><span data-stu-id="f6342-133">Under hello **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="f6342-134">Откроется диалоговое окно входа в Dropbox for Business в новом окне браузера.</span><span class="sxs-lookup"><span data-stu-id="f6342-134">It opens a Dropbox for Business login dialog in a new browser window.</span></span>

6. <span data-ttu-id="f6342-135">На hello **входа toolink tooDropbox с Azure AD** диалогового окна входа в tooyour Dropbox для бизнеса.</span><span class="sxs-lookup"><span data-stu-id="f6342-135">On hello **Sign-in tooDropbox toolink with Azure AD** dialog, sign in tooyour Dropbox for Business tenant.</span></span>

     <span data-ttu-id="f6342-136">![Подготовка учетных записей пользователей](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769518.png "Подготовка учетных записей пользователей")</span><span class="sxs-lookup"><span data-stu-id="f6342-136">![User provisioning](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769518.png "User provisioning")</span></span>

7. <span data-ttu-id="f6342-137">Убедитесь, что хотелось бы tooyour изменения toomake Azure Active Directory разрешение toogive Dropbox для бизнеса.</span><span class="sxs-lookup"><span data-stu-id="f6342-137">Confirm that you would like toogive Azure Active Directory permission toomake changes tooyour Dropbox for Business tenant.</span></span> <span data-ttu-id="f6342-138">Нажмите кнопку **Разрешить**.</span><span class="sxs-lookup"><span data-stu-id="f6342-138">Click **Allow**.</span></span>
    
      <span data-ttu-id="f6342-139">![Подготовка учетных записей пользователей](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769519.png "Подготовка учетных записей пользователей")</span><span class="sxs-lookup"><span data-stu-id="f6342-139">![User provisioning](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769519.png "User provisioning")</span></span>

8. <span data-ttu-id="f6342-140">В hello портал Azure, щелкните **проверить подключение** tooensure Azure AD могут подключаться tooyour Dropbox для бизнес-приложения.</span><span class="sxs-lookup"><span data-stu-id="f6342-140">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Dropbox for Business app.</span></span> <span data-ttu-id="f6342-141">При сбое подключения hello убедитесь Dropbox для бизнеса учетная запись имеет разрешения администратора команды и повторите hello **«Авторизовать»** еще один шаг.</span><span class="sxs-lookup"><span data-stu-id="f6342-141">If hello connection fails, ensure your Dropbox for Business account has Team Admin permissions and try hello **"Authorize"** step again.</span></span>

9. <span data-ttu-id="f6342-142">Введите адрес электронной почты hello пользователя или группы, которые должны получить уведомления о подготовке ошибки в hello **уведомление по электронной почте** поле и установите флажок "hello".</span><span class="sxs-lookup"><span data-stu-id="f6342-142">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

10. <span data-ttu-id="f6342-143">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="f6342-143">Click **Save.**</span></span>

11. <span data-ttu-id="f6342-144">Установите hello сопоставлений **tooDropbox синхронизации Azure Active Directory-пользователи для бизнеса.**</span><span class="sxs-lookup"><span data-stu-id="f6342-144">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooDropbox for Business.**</span></span>

12. <span data-ttu-id="f6342-145">В hello **сопоставления атрибутов** просмотрите hello атрибутов пользователей, которые синхронизируются из tooDropbox Azure AD для бизнеса.</span><span class="sxs-lookup"><span data-stu-id="f6342-145">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooDropbox for Business.</span></span> <span data-ttu-id="f6342-146">Здравствуйте, атрибуты, выбранные в качестве **сопоставление** свойства, используемые toomatch hello учетных записей пользователей в Dropbox для бизнеса для операций обновления.</span><span class="sxs-lookup"><span data-stu-id="f6342-146">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Dropbox for Business for update operations.</span></span> <span data-ttu-id="f6342-147">Выберите toocommit кнопку hello сохранить все изменения.</span><span class="sxs-lookup"><span data-stu-id="f6342-147">Select hello Save button toocommit any changes.</span></span>

13. <span data-ttu-id="f6342-148">tooenable hello подготовки службы Azure AD для Dropbox для бизнеса, изменение hello **состояние подготовки** слишком**на** в разделе "Параметры" hello</span><span class="sxs-lookup"><span data-stu-id="f6342-148">tooenable hello Azure AD provisioning service for Dropbox for Business, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

14. <span data-ttu-id="f6342-149">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="f6342-149">Click **Save.**</span></span>

<span data-ttu-id="f6342-150">Он запускает hello первоначальной синхронизации все пользователи и группы, назначенные tooDropbox для бизнеса в hello пользователей и группы раздела.</span><span class="sxs-lookup"><span data-stu-id="f6342-150">It starts hello initial synchronization of any users and/or groups assigned tooDropbox for Business in hello Users and Groups section.</span></span> <span data-ttu-id="f6342-151">Начальная синхронизация Hello принимает tooperform больше времени, чем последующие синхронизации, которые происходят примерно каждые 20 минут при условии, что запущена служба hello.</span><span class="sxs-lookup"><span data-stu-id="f6342-151">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="f6342-152">Можно использовать hello **сведения о синхронизации** статьи toomonitor хода выполнения и следуйте ссылки tooprovisioning отчеты о действиях, которые описывают все действия, выполняемые hello подготовки службы на клиенте Dropbox для бизнес-приложения.</span><span class="sxs-lookup"><span data-stu-id="f6342-152">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Dropbox for Business app.</span></span>

<span data-ttu-id="f6342-153">Теперь можно создать тестовую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="f6342-153">You can now create a test account.</span></span> <span data-ttu-id="f6342-154">Дождитесь копирование минут too20 tooverify, hello учетная запись была синхронизирована tooDropbox для бизнеса.</span><span class="sxs-lookup"><span data-stu-id="f6342-154">Wait for up too20 minutes tooverify that hello account has been synchronized tooDropbox for Business.</span></span>

<span data-ttu-id="f6342-155">Об успешном завершении цикла подготовки пользователя говорит соответствующий статус.</span><span class="sxs-lookup"><span data-stu-id="f6342-155">A successfully completed user provisioning cycle is indicated by a related status.</span></span>

<span data-ttu-id="f6342-156">![Назначение пользователей](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/IC769523.png "Назначение пользователей")</span><span class="sxs-lookup"><span data-stu-id="f6342-156">![Assign users](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/IC769523.png "Assign users")</span></span>


## <a name="additional-resources"></a><span data-ttu-id="f6342-157">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="f6342-157">Additional resources</span></span>

* [<span data-ttu-id="f6342-158">Управление подготовкой учетных записей пользователей для корпоративных приложений</span><span class="sxs-lookup"><span data-stu-id="f6342-158">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f6342-159">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f6342-159">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="f6342-160">Настройка единого входа</span><span class="sxs-lookup"><span data-stu-id="f6342-160">Configure Single Sign-on</span></span>](active-directory-saas-dropboxforbusiness-tutorial.md)