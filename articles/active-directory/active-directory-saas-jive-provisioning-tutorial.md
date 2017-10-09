---
title: "Руководство по интеграции Azure Active Directory с Jive | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Jive."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6fbfdbe7-d66c-4305-9fea-76d6a6a92830
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: b1c0d0bc2d79427c055f577fe5f9d30d10f1bbdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-jive-for-user-provisioning"></a><span data-ttu-id="b1732-103">Руководство по настройке Jive для подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="b1732-103">Tutorial: Configuring Jive for User Provisioning</span></span>

<span data-ttu-id="b1732-104">Цель этого учебника Hello — hello действия, которые следует tooperform в Jive и Azure AD tooautomatically подготовки и Отмена подготовки учетных записей пользователей из Azure AD tooJive tooshow.</span><span class="sxs-lookup"><span data-stu-id="b1732-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Jive and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooJive.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b1732-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b1732-105">Prerequisites</span></span>

<span data-ttu-id="b1732-106">Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="b1732-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="b1732-107">клиент Azure Active Directory;</span><span class="sxs-lookup"><span data-stu-id="b1732-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="b1732-108">подписка Jive с поддержкой единого входа;</span><span class="sxs-lookup"><span data-stu-id="b1732-108">A Jive single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="b1732-109">учетная запись пользователя Jive с разрешениями администратора команды.</span><span class="sxs-lookup"><span data-stu-id="b1732-109">A user account in Jive with Team Admin permissions.</span></span>

## <a name="assigning-users-toojive"></a><span data-ttu-id="b1732-110">Назначение пользователей tooJive</span><span class="sxs-lookup"><span data-stu-id="b1732-110">Assigning users tooJive</span></span>

<span data-ttu-id="b1732-111">Azure Active Directory использует называемый «назначения» toodetermine пользователей, которые должны получать доступ tooselected приложений.</span><span class="sxs-lookup"><span data-stu-id="b1732-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="b1732-112">В контексте hello автоматический подготовки пользователей. учетной записи синхронизируются только hello пользователей и групп, назначенных» «tooan приложения в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b1732-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="b1732-113">Для настройки и включения hello подготовки службы, требуется toodecide какие пользователи или группы в Azure AD представляют Привет пользователям требуется доступ к приложению tooyour Jive.</span><span class="sxs-lookup"><span data-stu-id="b1732-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Jive app.</span></span> <span data-ttu-id="b1732-114">После приняла решение, можно назначить эти приложения Jive tooyour пользователей в соответствии с инструкциями hello здесь:</span><span class="sxs-lookup"><span data-stu-id="b1732-114">Once decided, you can assign these users tooyour Jive app by following hello instructions here:</span></span>

[<span data-ttu-id="b1732-115">Назначить пользователю или группе tooan корпоративного приложения</span><span class="sxs-lookup"><span data-stu-id="b1732-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toojive"></a><span data-ttu-id="b1732-116">Важные советы для назначения пользователей tooJive</span><span class="sxs-lookup"><span data-stu-id="b1732-116">Important tips for assigning users tooJive</span></span>

*   <span data-ttu-id="b1732-117">Рекомендуется один назначить hello tootest tooJive настройки подготовки пользователя Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b1732-117">It is recommended that a single Azure AD user be assigned tooJive tootest hello provisioning configuration.</span></span> <span data-ttu-id="b1732-118">Дополнительные пользователи и/или группы можно назначить позднее.</span><span class="sxs-lookup"><span data-stu-id="b1732-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="b1732-119">При назначении tooJive пользователя, необходимо выбрать допустимой роли пользователя.</span><span class="sxs-lookup"><span data-stu-id="b1732-119">When assigning a user tooJive, you must select a valid user role.</span></span> <span data-ttu-id="b1732-120">роль «Доступ по умолчанию» Hello не работает для подготовки.</span><span class="sxs-lookup"><span data-stu-id="b1732-120">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="b1732-121">Включение подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="b1732-121">Enable User Provisioning</span></span>

<span data-ttu-id="b1732-122">Этот раздел поможет выполнить подключение учетной записи пользователя в Azure AD tooJive подготовки API и настройке подготовки службы toocreate hello, обновления и отключить учетные записи пользователей, назначенные в зависимости от назначения пользователей и групп в Azure AD Jive.</span><span class="sxs-lookup"><span data-stu-id="b1732-122">This section guides you through connecting your Azure AD tooJive's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Jive based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="b1732-123">Можно также выбрать tooenabled на основе SAML единого входа для Jive, следуя инструкциям hello в [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b1732-123">You may also choose tooenabled SAML-based Single Sign-On for Jive, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="b1732-124">Единый вход можно настроить независимо от автоматической подготовки, хотя эти две возможности дополняют друг друга.</span><span class="sxs-lookup"><span data-stu-id="b1732-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-user-account-provisioning"></a><span data-ttu-id="b1732-125">Подготовка учетной записи пользователя tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="b1732-125">tooconfigure user account provisioning:</span></span>

<span data-ttu-id="b1732-126">Цель этого раздела Hello является toooutline как tooenable пользователя Подготовка пользователя Active Directory учетных записей tooJive.</span><span class="sxs-lookup"><span data-stu-id="b1732-126">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooJive.</span></span>
<span data-ttu-id="b1732-127">В рамках этой процедуры не tooprovide требуется маркер безопасности пользователя, необходимо toorequest на сайте Jive.com.</span><span class="sxs-lookup"><span data-stu-id="b1732-127">As part of this procedure, you are required tooprovide a user security token you need toorequest from Jive.com.</span></span>

1. <span data-ttu-id="b1732-128">В hello [портал Azure](https://portal.azure.com), Обзор toohello **Azure Active Directory > корпоративных приложений > все приложения** раздела.</span><span class="sxs-lookup"><span data-stu-id="b1732-128">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="b1732-129">Если вы уже настроили Jive для единого входа, поиск экземпляра с помощью поля поиска hello Jive.</span><span class="sxs-lookup"><span data-stu-id="b1732-129">If you have already configured Jive for single sign-on, search for your instance of Jive using hello search field.</span></span> <span data-ttu-id="b1732-130">В противном случае выберите **добавить** и выполните поиск **Jive** в галерее приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b1732-130">Otherwise, select **Add** and search for **Jive** in hello application gallery.</span></span> <span data-ttu-id="b1732-131">Выберите Jive из результатов поиска hello и добавить его в список tooyour приложений.</span><span class="sxs-lookup"><span data-stu-id="b1732-131">Select Jive from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="b1732-132">Выберите свой экземпляр Jive, а затем выберите hello **Provisioning** вкладки.</span><span class="sxs-lookup"><span data-stu-id="b1732-132">Select your instance of Jive, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="b1732-133">Набор hello **режим подготовки** слишком**автоматического**.</span><span class="sxs-lookup"><span data-stu-id="b1732-133">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![подготовка](./media/active-directory-saas-jive-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="b1732-135">В разделе hello **учетные данные администратора** статьи, предоставляют hello следующие параметры конфигурации:</span><span class="sxs-lookup"><span data-stu-id="b1732-135">Under hello **Admin Credentials** section, provide hello following configuration settings:</span></span>
   
    <span data-ttu-id="b1732-136">а.</span><span class="sxs-lookup"><span data-stu-id="b1732-136">a.</span></span> <span data-ttu-id="b1732-137">В hello **имя пользователя администратора Jive** введите имя, которое имеет hello учетной записи Jive **системный администратор** профиля на сайте Jive.com.</span><span class="sxs-lookup"><span data-stu-id="b1732-137">In hello **Jive Admin User Name** textbox, type a Jive account name that has hello **System Administrator** profile in Jive.com assigned.</span></span>
   
    <span data-ttu-id="b1732-138">b.</span><span class="sxs-lookup"><span data-stu-id="b1732-138">b.</span></span> <span data-ttu-id="b1732-139">В hello **пароль администратора Jive** текстового поля, типа hello пароль для этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="b1732-139">In hello **Jive Admin Password** textbox, type hello password for this account.</span></span>
   
    <span data-ttu-id="b1732-140">c.</span><span class="sxs-lookup"><span data-stu-id="b1732-140">c.</span></span> <span data-ttu-id="b1732-141">В hello **URL-адрес клиента Jive** в текстовое поле URL-адрес клиента Jive типа hello.</span><span class="sxs-lookup"><span data-stu-id="b1732-141">In hello **Jive Tenant URL** textbox, type hello Jive tenant URL.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="b1732-142">URL-адрес клиента Jive Hello является URL-адрес, используемый в вашей организации toolog в tooJive.</span><span class="sxs-lookup"><span data-stu-id="b1732-142">hello Jive tenant URL is URL that is used by your organization toolog in tooJive.</span></span>  
      > <span data-ttu-id="b1732-143">Как правило, hello URL-адрес имеет следующий формат hello: **www.\< Организация\>. сайтом jive.com**.</span><span class="sxs-lookup"><span data-stu-id="b1732-143">Typically, hello URL has hello following format: **www.\<organization\>.jive.com**.</span></span>          

6. <span data-ttu-id="b1732-144">В hello портал Azure, щелкните **проверить подключение** tooensure Azure AD можно подключить приложение tooyour Jive.</span><span class="sxs-lookup"><span data-stu-id="b1732-144">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Jive app.</span></span>

7. <span data-ttu-id="b1732-145">Введите адрес электронной почты hello пользователя или группы, которые должны получить уведомления о подготовке ошибки в hello **уведомление по электронной почте** поле и установите флажок "hello" ниже.</span><span class="sxs-lookup"><span data-stu-id="b1732-145">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox below.</span></span>

8. <span data-ttu-id="b1732-146">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="b1732-146">Click **Save.**</span></span>

9. <span data-ttu-id="b1732-147">Установите hello сопоставлений **tooJive синхронизации Azure Active Directory — пользователи.**</span><span class="sxs-lookup"><span data-stu-id="b1732-147">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooJive.**</span></span>

10. <span data-ttu-id="b1732-148">В hello **сопоставления атрибутов** просмотрите hello атрибутов пользователей, которые синхронизируются из tooJive Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b1732-148">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooJive.</span></span> <span data-ttu-id="b1732-149">Здравствуйте, атрибуты, выбранные в качестве **сопоставление** свойства, используемые toomatch hello учетных записей пользователей в Jive для операций обновления.</span><span class="sxs-lookup"><span data-stu-id="b1732-149">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Jive for update operations.</span></span> <span data-ttu-id="b1732-150">Выберите toocommit кнопку hello сохранить все изменения.</span><span class="sxs-lookup"><span data-stu-id="b1732-150">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="b1732-151">tooenable hello подготовки службы Azure AD для Jive, изменение hello **состояние подготовки** слишком**на** в разделе "Параметры" hello</span><span class="sxs-lookup"><span data-stu-id="b1732-151">tooenable hello Azure AD provisioning service for Jive, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

12. <span data-ttu-id="b1732-152">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="b1732-152">Click **Save.**</span></span>

<span data-ttu-id="b1732-153">Он запускает hello первоначальной синхронизации все пользователи и группы, назначенные tooJive в hello пользователей и группы раздела.</span><span class="sxs-lookup"><span data-stu-id="b1732-153">It starts hello initial synchronization of any users and/or groups assigned tooJive in hello Users and Groups section.</span></span> <span data-ttu-id="b1732-154">Начальная синхронизация Hello принимает tooperform больше времени, чем последующие синхронизации, которые происходят примерно каждые 20 минут при условии, что запущена служба hello.</span><span class="sxs-lookup"><span data-stu-id="b1732-154">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="b1732-155">Можно использовать hello **сведения о синхронизации** статьи toomonitor хода выполнения и следуйте ссылки tooprovisioning отчеты о действиях, которые описывают все действия, выполняемые hello подготовки службы приложения Jive.</span><span class="sxs-lookup"><span data-stu-id="b1732-155">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Jive app.</span></span>

<span data-ttu-id="b1732-156">Теперь можно создать тестовую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="b1732-156">You can now create a test account.</span></span> <span data-ttu-id="b1732-157">Дождитесь копирование минут too20 tooverify, hello учетная запись была синхронизирована tooJive.</span><span class="sxs-lookup"><span data-stu-id="b1732-157">Wait for up too20 minutes tooverify that hello account has been synchronized tooJive.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b1732-158">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b1732-158">Additional resources</span></span>

* [<span data-ttu-id="b1732-159">Управление подготовкой учетных записей пользователей для корпоративных приложений</span><span class="sxs-lookup"><span data-stu-id="b1732-159">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b1732-160">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b1732-160">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="b1732-161">Настройка единого входа</span><span class="sxs-lookup"><span data-stu-id="b1732-161">Configure Single Sign-on</span></span>](active-directory-saas-jive-tutorial.md)