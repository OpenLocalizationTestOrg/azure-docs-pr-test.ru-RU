---
title: "Учебник. Интеграция Azure Active Directory с DocuSign | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и DocuSign."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 294cd6b8-74d7-44bc-92bc-020ccd13ff12
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: 8562a8f9e05fb72d3331507b7da5c6afee38f9b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-docusign-for-user-provisioning"></a><span data-ttu-id="931fe-103">Руководство по настройке DocuSign для подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="931fe-103">Tutorial: Configuring DocuSign for User Provisioning</span></span>

<span data-ttu-id="931fe-104">Цель этого учебника Hello — hello действия, которые следует tooperform в DocuSign и Azure AD tooautomatically подготовки и Отмена подготовки учетных записей пользователей из Azure AD tooDocuSign tooshow.</span><span class="sxs-lookup"><span data-stu-id="931fe-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in DocuSign and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooDocuSign.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="931fe-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="931fe-105">Prerequisites</span></span>

<span data-ttu-id="931fe-106">Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="931fe-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="931fe-107">клиент Azure Active Directory;</span><span class="sxs-lookup"><span data-stu-id="931fe-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="931fe-108">подписка DocuSign с поддержкой единого входа;</span><span class="sxs-lookup"><span data-stu-id="931fe-108">A DocuSign single sign-on enabled subscription.</span></span>
*   <span data-ttu-id="931fe-109">учетная запись пользователя в DocuSign с разрешениями администратора группы.</span><span class="sxs-lookup"><span data-stu-id="931fe-109">A user account in DocuSign with Team Admin permissions.</span></span>

## <a name="assigning-users-toodocusign"></a><span data-ttu-id="931fe-110">Назначение пользователей tooDocuSign</span><span class="sxs-lookup"><span data-stu-id="931fe-110">Assigning users tooDocuSign</span></span>

<span data-ttu-id="931fe-111">Azure Active Directory использует называемый «назначения» toodetermine пользователей, которые должны получать доступ tooselected приложений.</span><span class="sxs-lookup"><span data-stu-id="931fe-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="931fe-112">В контексте hello автоматический подготовки пользователей. учетной записи синхронизируются только hello пользователей и групп, назначенных» «tooan приложения в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="931fe-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD are synchronized.</span></span>

<span data-ttu-id="931fe-113">Для настройки и включения hello подготовки службы, требуется toodecide какие пользователи или группы в Azure AD представляют Привет пользователям требуется доступ к приложению DocuSign tooyour.</span><span class="sxs-lookup"><span data-stu-id="931fe-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour DocuSign app.</span></span> <span data-ttu-id="931fe-114">После приняла решение, можно назначить эти приложения DocuSign tooyour пользователей в соответствии с инструкциями hello здесь:</span><span class="sxs-lookup"><span data-stu-id="931fe-114">Once decided, you can assign these users tooyour DocuSign app by following hello instructions here:</span></span>

[<span data-ttu-id="931fe-115">Назначить пользователю или группе tooan корпоративного приложения</span><span class="sxs-lookup"><span data-stu-id="931fe-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toodocusign"></a><span data-ttu-id="931fe-116">Важные советы для назначения пользователей tooDocuSign</span><span class="sxs-lookup"><span data-stu-id="931fe-116">Important tips for assigning users tooDocuSign</span></span>

*   <span data-ttu-id="931fe-117">Рекомендуется один назначенный hello tootest tooDocuSign настройки подготовки пользователя Azure AD.</span><span class="sxs-lookup"><span data-stu-id="931fe-117">It is recommended that a single Azure AD user is assigned tooDocuSign tootest hello provisioning configuration.</span></span> <span data-ttu-id="931fe-118">Дополнительные пользователи и/или группы можно назначить позднее.</span><span class="sxs-lookup"><span data-stu-id="931fe-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="931fe-119">При назначении tooDocuSign пользователя, необходимо выбрать допустимой роли пользователя.</span><span class="sxs-lookup"><span data-stu-id="931fe-119">When assigning a user tooDocuSign, you must select a valid user role.</span></span> <span data-ttu-id="931fe-120">роль «Доступ по умолчанию» Hello не работает для подготовки.</span><span class="sxs-lookup"><span data-stu-id="931fe-120">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="931fe-121">Включение подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="931fe-121">Enable User Provisioning</span></span>

<span data-ttu-id="931fe-122">Этот раздел поможет выполнить подключение учетной записи пользователя в Azure AD tooDocuSign подготовки API и настройке подготовки службы toocreate hello, обновления и отключить учетные записи пользователей, назначенные в DocuSign, в зависимости от назначения пользователей и групп в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="931fe-122">This section guides you through connecting your Azure AD tooDocuSign's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in DocuSign based on user and group assignment in Azure AD.</span></span>

> [!Tip]
> <span data-ttu-id="931fe-123">Можно также выбрать tooenabled на основе SAML Single Sign-On для DocuSign, следуя инструкциям hello в [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="931fe-123">You may also choose tooenabled SAML-based Single Sign-On for DocuSign, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="931fe-124">Единый вход можно настроить независимо от автоматической подготовки, хотя эти две возможности дополняют друг друга.</span><span class="sxs-lookup"><span data-stu-id="931fe-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-user-account-provisioning"></a><span data-ttu-id="931fe-125">Подготовка учетной записи пользователя tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="931fe-125">tooconfigure user account provisioning:</span></span>

<span data-ttu-id="931fe-126">Цель этого раздела Hello является toooutline как tooenable пользователя Подготовка пользователя Active Directory учетных записей tooDocuSign.</span><span class="sxs-lookup"><span data-stu-id="931fe-126">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooDocuSign.</span></span>

1. <span data-ttu-id="931fe-127">В hello [портал Azure](https://portal.azure.com), Обзор toohello **Azure Active Directory > корпоративных приложений > все приложения** раздела.</span><span class="sxs-lookup"><span data-stu-id="931fe-127">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="931fe-128">Если вы уже настроили DocuSign для единого входа, поиск экземпляра DocuSign с помощью поля поиска hello.</span><span class="sxs-lookup"><span data-stu-id="931fe-128">If you have already configured DocuSign for single sign-on, search for your instance of DocuSign using hello search field.</span></span> <span data-ttu-id="931fe-129">В противном случае выберите **добавить** и выполните поиск **DocuSign** в галерее приложения hello.</span><span class="sxs-lookup"><span data-stu-id="931fe-129">Otherwise, select **Add** and search for **DocuSign** in hello application gallery.</span></span> <span data-ttu-id="931fe-130">Выберите DocuSign из результатов поиска hello и добавить его в список tooyour приложений.</span><span class="sxs-lookup"><span data-stu-id="931fe-130">Select DocuSign from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="931fe-131">Выберите свой экземпляр DocuSign, а затем выберите hello **Provisioning** вкладки.</span><span class="sxs-lookup"><span data-stu-id="931fe-131">Select your instance of DocuSign, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="931fe-132">Набор hello **режим подготовки** слишком**автоматического**.</span><span class="sxs-lookup"><span data-stu-id="931fe-132">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![подготовка](./media/active-directory-saas-docusign-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="931fe-134">В разделе hello **учетные данные администратора** статьи, предоставляют hello следующие параметры конфигурации:</span><span class="sxs-lookup"><span data-stu-id="931fe-134">Under hello **Admin Credentials** section, provide hello following configuration settings:</span></span>
   
    <span data-ttu-id="931fe-135">а.</span><span class="sxs-lookup"><span data-stu-id="931fe-135">a.</span></span> <span data-ttu-id="931fe-136">В hello **имя пользователя администратора** введите имя, которое имеет hello учетной записи DocuSign **системный администратор** профиля в DocuSign.com.</span><span class="sxs-lookup"><span data-stu-id="931fe-136">In hello **Admin User Name** textbox, type a DocuSign account name that has hello **System Administrator** profile in DocuSign.com assigned.</span></span>
   
    <span data-ttu-id="931fe-137">b.</span><span class="sxs-lookup"><span data-stu-id="931fe-137">b.</span></span> <span data-ttu-id="931fe-138">В hello **пароль администратора** текстового поля, типа hello пароль для этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="931fe-138">In hello **Admin Password** textbox, type hello password for this account.</span></span>

6. <span data-ttu-id="931fe-139">В hello портал Azure, щелкните **проверить подключение** tooensure Azure AD можно подключить приложение tooyour DocuSign.</span><span class="sxs-lookup"><span data-stu-id="931fe-139">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour DocuSign app.</span></span>

7. <span data-ttu-id="931fe-140">В hello **уведомление по электронной почте** введите hello адрес электронной почты пользователя или группы, которые должны получать уведомления о подготовке ошибки и установите флажок "hello".</span><span class="sxs-lookup"><span data-stu-id="931fe-140">In hello **Notification Email** field, enter hello email address of a person or group who should receive provisioning error notifications, and check hello checkbox.</span></span>

8. <span data-ttu-id="931fe-141">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="931fe-141">Click **Save.**</span></span>

9. <span data-ttu-id="931fe-142">Установите hello сопоставлений **tooDocuSign синхронизации Azure Active Directory — пользователи.**</span><span class="sxs-lookup"><span data-stu-id="931fe-142">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooDocuSign.**</span></span>

10. <span data-ttu-id="931fe-143">В hello **сопоставления атрибутов** просмотрите hello атрибутов пользователей, которые синхронизируются из tooDocuSign Azure AD.</span><span class="sxs-lookup"><span data-stu-id="931fe-143">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooDocuSign.</span></span> <span data-ttu-id="931fe-144">Здравствуйте, атрибуты, выбранные в качестве **сопоставление** свойства, используемые toomatch hello учетных записей пользователей в DocuSign для операций обновления.</span><span class="sxs-lookup"><span data-stu-id="931fe-144">hello attributes selected as **Matching** properties are used toomatch hello user accounts in DocuSign for update operations.</span></span> <span data-ttu-id="931fe-145">Выберите toocommit кнопку hello сохранить все изменения.</span><span class="sxs-lookup"><span data-stu-id="931fe-145">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="931fe-146">tooenable hello подготовки службы Azure AD для DocuSign, изменение hello **состояние подготовки** слишком**на** в разделе "Параметры" hello</span><span class="sxs-lookup"><span data-stu-id="931fe-146">tooenable hello Azure AD provisioning service for DocuSign, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

12. <span data-ttu-id="931fe-147">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="931fe-147">Click **Save.**</span></span>

<span data-ttu-id="931fe-148">Он запускает hello первоначальной синхронизации все пользователи и группы, назначенные tooDocuSign в hello пользователей и группы раздела.</span><span class="sxs-lookup"><span data-stu-id="931fe-148">It starts hello initial synchronization of any users and/or groups assigned tooDocuSign in hello Users and Groups section.</span></span> <span data-ttu-id="931fe-149">Начальная синхронизация Hello принимает tooperform больше времени, чем последующие синхронизации, которые происходят примерно каждые 20 минут при условии, что запущена служба hello.</span><span class="sxs-lookup"><span data-stu-id="931fe-149">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="931fe-150">Можно использовать hello **сведения о синхронизации** статьи toomonitor хода выполнения и следуйте ссылки tooprovisioning отчеты о действиях, которые описывают все действия, выполняемые hello подготовки службы в приложении DocuSign.</span><span class="sxs-lookup"><span data-stu-id="931fe-150">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your DocuSign app.</span></span>

<span data-ttu-id="931fe-151">Теперь можно создать тестовую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="931fe-151">You can now create a test account.</span></span> <span data-ttu-id="931fe-152">Дождитесь копирование минут too20 tooverify, hello учетная запись была синхронизирована tooDocuSign.</span><span class="sxs-lookup"><span data-stu-id="931fe-152">Wait for up too20 minutes tooverify that hello account has been synchronized tooDocuSign.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="931fe-153">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="931fe-153">Additional resources</span></span>

* [<span data-ttu-id="931fe-154">Управление подготовкой учетных записей пользователей для корпоративных приложений</span><span class="sxs-lookup"><span data-stu-id="931fe-154">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="931fe-155">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="931fe-155">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="931fe-156">Настройка единого входа</span><span class="sxs-lookup"><span data-stu-id="931fe-156">Configure Single Sign-on</span></span>](active-directory-saas-docusign-tutorial.md)