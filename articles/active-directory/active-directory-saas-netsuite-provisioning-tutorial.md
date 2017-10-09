---
title: "Руководство по интеграции Azure Active Directory с NetSuite | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Netsuite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8a6d3994-ee33-4a6f-b0a2-9d0389467f16
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 5bb2989c1296b9f2abc9e8c84855731adc484aab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-netsuite-for-automatic-user-provisioning"></a><span data-ttu-id="3bb1b-103">Руководство по настройке Netsuite для автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="3bb1b-103">Tutorial: Configuring Netsuite for Automatic User Provisioning</span></span>

<span data-ttu-id="3bb1b-104">Цель этого учебника Hello — hello действия, которые следует tooperform в Netsuite и Azure AD tooautomatically подготовки и Отмена подготовки учетных записей пользователей из Azure AD tooNetsuite tooshow.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Netsuite and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooNetsuite.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3bb1b-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3bb1b-105">Prerequisites</span></span>

<span data-ttu-id="3bb1b-106">Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="3bb1b-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="3bb1b-107">клиент Azure Active Directory;</span><span class="sxs-lookup"><span data-stu-id="3bb1b-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="3bb1b-108">подписка Netsuite с поддержкой единого входа;</span><span class="sxs-lookup"><span data-stu-id="3bb1b-108">A Netsuite single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="3bb1b-109">учетная запись пользователя в Netsuite с разрешениями администратора команды.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-109">A user account in Netsuite with Team Admin permissions.</span></span>

## <a name="assigning-users-toonetsuite"></a><span data-ttu-id="3bb1b-110">Назначение пользователей tooNetsuite</span><span class="sxs-lookup"><span data-stu-id="3bb1b-110">Assigning users tooNetsuite</span></span>

<span data-ttu-id="3bb1b-111">Azure Active Directory использует называемый «назначения» toodetermine пользователей, которые должны получать доступ tooselected приложений.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="3bb1b-112">В контексте hello автоматический подготовки пользователей. учетной записи синхронизируются только hello пользователей и групп, назначенных» «tooan приложения в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD are synchronized.</span></span>

<span data-ttu-id="3bb1b-113">Для настройки и включения hello подготовки службы, требуется toodecide какие пользователи или группы в Azure AD представляют Привет пользователям требуется доступ к приложению Netsuite tooyour.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Netsuite app.</span></span> <span data-ttu-id="3bb1b-114">После приняла решение, можно назначить эти приложения Netsuite tooyour пользователей в соответствии с инструкциями hello здесь:</span><span class="sxs-lookup"><span data-stu-id="3bb1b-114">Once decided, you can assign these users tooyour Netsuite app by following hello instructions here:</span></span>

[<span data-ttu-id="3bb1b-115">Назначить пользователю или группе tooan корпоративного приложения</span><span class="sxs-lookup"><span data-stu-id="3bb1b-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toonetsuite"></a><span data-ttu-id="3bb1b-116">Важные советы для назначения пользователей tooNetsuite</span><span class="sxs-lookup"><span data-stu-id="3bb1b-116">Important tips for assigning users tooNetsuite</span></span>

*   <span data-ttu-id="3bb1b-117">Рекомендуется один назначенный hello tootest tooNetsuite настройки подготовки пользователя Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-117">It is recommended that a single Azure AD user is assigned tooNetsuite tootest hello provisioning configuration.</span></span> <span data-ttu-id="3bb1b-118">Дополнительные пользователи и/или группы можно назначить позднее.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="3bb1b-119">При назначении tooNetsuite пользователя, необходимо выбрать допустимой роли пользователя.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-119">When assigning a user tooNetsuite, you must select a valid user role.</span></span> <span data-ttu-id="3bb1b-120">роль «Доступ по умолчанию» Hello не работает для подготовки.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-120">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="3bb1b-121">Включение подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="3bb1b-121">Enable User Provisioning</span></span>

<span data-ttu-id="3bb1b-122">Этот раздел поможет выполнить подключение учетной записи пользователя в Azure AD tooNetsuite подготовки API и настройке подготовки службы toocreate hello, обновления и отключить учетные записи пользователей, назначенные в Netsuite, в зависимости от назначения пользователей и групп в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-122">This section guides you through connecting your Azure AD tooNetsuite's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Netsuite based on user and group assignment in Azure AD.</span></span>

> [!TIP] 
> <span data-ttu-id="3bb1b-123">Можно также выбрать tooenabled на основе SAML Single Sign-On для Netsuite, следуя инструкциям hello в [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3bb1b-123">You may also choose tooenabled SAML-based Single Sign-On for Netsuite, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="3bb1b-124">Единый вход можно настроить независимо от автоматической подготовки, хотя эти две возможности дополняют друг друга.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-user-account-provisioning"></a><span data-ttu-id="3bb1b-125">Подготовка учетной записи пользователя tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="3bb1b-125">tooconfigure user account provisioning:</span></span>

<span data-ttu-id="3bb1b-126">Цель этого раздела Hello является toooutline как tooenable пользователя Подготовка пользователя Active Directory учетных записей tooNetsuite.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-126">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooNetsuite.</span></span>

1. <span data-ttu-id="3bb1b-127">В hello [портал Azure](https://portal.azure.com), Обзор toohello **Azure Active Directory > корпоративных приложений > все приложения** раздела.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-127">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="3bb1b-128">Если вы уже настроили Netsuite для единого входа, поиск экземпляра Netsuite, с помощью поля поиска hello.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-128">If you have already configured Netsuite for single sign-on, search for your instance of Netsuite using hello search field.</span></span> <span data-ttu-id="3bb1b-129">В противном случае выберите **добавить** и выполните поиск **Netsuite** в галерее приложения hello.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-129">Otherwise, select **Add** and search for **Netsuite** in hello application gallery.</span></span> <span data-ttu-id="3bb1b-130">Выберите Netsuite из результатов поиска hello и добавить его в список tooyour приложений.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-130">Select Netsuite from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="3bb1b-131">Выберите свой экземпляр Netsuite, а затем выберите hello **Provisioning** вкладки.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-131">Select your instance of Netsuite, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="3bb1b-132">Набор hello **режим подготовки** слишком**автоматического**.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-132">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![подготовка](./media/active-directory-saas-netsuite-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="3bb1b-134">В разделе hello **учетные данные администратора** статьи, предоставляют hello следующие параметры конфигурации:</span><span class="sxs-lookup"><span data-stu-id="3bb1b-134">Under hello **Admin Credentials** section, provide hello following configuration settings:</span></span>
   
    <span data-ttu-id="3bb1b-135">а.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-135">a.</span></span> <span data-ttu-id="3bb1b-136">В hello **имя пользователя администратора** введите имя, которое имеет hello, учетной записи Netsuite **системный администратор** Netsuite.com назначен профиль.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-136">In hello **Admin User Name** textbox, type a Netsuite account name that has hello **System Administrator** profile in Netsuite.com assigned.</span></span>
   
    <span data-ttu-id="3bb1b-137">b.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-137">b.</span></span> <span data-ttu-id="3bb1b-138">В hello **пароль администратора** текстового поля, типа hello пароль для этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-138">In hello **Admin Password** textbox, type hello password for this account.</span></span>
      
6. <span data-ttu-id="3bb1b-139">В hello портал Azure, щелкните **проверить подключение** tooensure Azure AD можно подключить приложение Netsuite tooyour.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-139">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Netsuite app.</span></span>

7. <span data-ttu-id="3bb1b-140">В hello **уведомление по электронной почте** введите hello адрес электронной почты пользователя или группы, которые должны получать уведомления о подготовке ошибки и установите флажок "hello".</span><span class="sxs-lookup"><span data-stu-id="3bb1b-140">In hello **Notification Email** field, enter hello email address of a person or group who should receive provisioning error notifications, and check hello checkbox.</span></span>

8. <span data-ttu-id="3bb1b-141">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-141">Click **Save.**</span></span>

9. <span data-ttu-id="3bb1b-142">Установите hello сопоставлений **tooNetsuite синхронизации Azure Active Directory — пользователи.**</span><span class="sxs-lookup"><span data-stu-id="3bb1b-142">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooNetsuite.**</span></span>

10. <span data-ttu-id="3bb1b-143">В hello **сопоставления атрибутов** просмотрите hello атрибутов пользователей, которые синхронизируются из tooNetsuite Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-143">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooNetsuite.</span></span> <span data-ttu-id="3bb1b-144">Обратите внимание, что атрибуты, выбранные в качестве hello **сопоставление** свойства, используемые toomatch hello учетных записей пользователей в Netsuite для операций обновления.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-144">Note that hello attributes selected as **Matching** properties are used toomatch hello user accounts in Netsuite for update operations.</span></span> <span data-ttu-id="3bb1b-145">Выберите toocommit кнопку hello сохранить все изменения.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-145">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="3bb1b-146">tooenable hello подготовки службы Azure AD для Netsuite, изменение hello **состояние подготовки** слишком**на** в разделе "Параметры" hello</span><span class="sxs-lookup"><span data-stu-id="3bb1b-146">tooenable hello Azure AD provisioning service for Netsuite, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

12. <span data-ttu-id="3bb1b-147">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-147">Click **Save.**</span></span>

<span data-ttu-id="3bb1b-148">Он запускает hello первоначальной синхронизации все пользователи и группы, назначенные tooNetsuite в hello пользователей и группы раздела.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-148">It starts hello initial synchronization of any users and/or groups assigned tooNetsuite in hello Users and Groups section.</span></span> <span data-ttu-id="3bb1b-149">Обратите внимание, что начальная синхронизация hello принимает tooperform больше времени, чем последующие синхронизации, которые происходят примерно каждые 20 минут при условии, что запущена служба hello.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-149">Note that hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="3bb1b-150">Можно использовать hello **сведения о синхронизации** статьи toomonitor хода выполнения и следуйте ссылки tooprovisioning отчеты о действиях, описывающих все действия, выполняемые hello подготовки службы приложения Netsuite.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-150">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Netsuite app.</span></span>

<span data-ttu-id="3bb1b-151">Теперь можно создать тестовую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-151">You can now create a test account.</span></span> <span data-ttu-id="3bb1b-152">Дождитесь копирование минут too20 tooverify, hello учетная запись была синхронизирована tooNetsuite.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-152">Wait for up too20 minutes tooverify that hello account has been synchronized tooNetsuite.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3bb1b-153">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="3bb1b-153">Additional resources</span></span>

* [<span data-ttu-id="3bb1b-154">Управление подготовкой учетных записей пользователей для корпоративных приложений</span><span class="sxs-lookup"><span data-stu-id="3bb1b-154">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3bb1b-155">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3bb1b-155">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="3bb1b-156">Настройка единого входа</span><span class="sxs-lookup"><span data-stu-id="3bb1b-156">Configure Single Sign-on</span></span>](active-directory-saas-netsuite-tutorial.md)