---
title: "Руководство по интеграции Azure Active Directory с Citrix GoToMeeting | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Citrix GoToMeeting."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f59fedb-2cf8-48d2-a5fb-222ed943ff78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 3c6eed5309dfa384c292b0cf63f8aa58988add81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-citrix-gotomeeting-for-automatic-user-provisioning"></a><span data-ttu-id="1aee5-103">Руководство по настройке Citrix GoToMeeting для автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="1aee5-103">Tutorial: Configuring Citrix GoToMeeting for Automatic User Provisioning</span></span>

<span data-ttu-id="1aee5-104">Цель этого учебника Hello — tooshow hello действия, которые следует tooperform в Citrix GoToMeeting и Azure AD tooautomatically подготовки и Отмена подготовки учетных записей пользователей из Azure AD tooCitrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="1aee5-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Citrix GoToMeeting and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooCitrix GoToMeeting.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1aee5-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1aee5-105">Prerequisites</span></span>

<span data-ttu-id="1aee5-106">Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="1aee5-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="1aee5-107">клиент Azure Active Directory;</span><span class="sxs-lookup"><span data-stu-id="1aee5-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="1aee5-108">подписка Citrix GoToMeeting с поддержкой единого входа;</span><span class="sxs-lookup"><span data-stu-id="1aee5-108">A Citrix GoToMeeting single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="1aee5-109">учетная запись пользователя в Citrix GoToMeeting с разрешениями администратора группы.</span><span class="sxs-lookup"><span data-stu-id="1aee5-109">A user account in Citrix GoToMeeting with Team Admin permissions.</span></span>

## <a name="assigning-users-toocitrix-gotomeeting"></a><span data-ttu-id="1aee5-110">Назначение пользователей tooCitrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="1aee5-110">Assigning users tooCitrix GoToMeeting</span></span>

<span data-ttu-id="1aee5-111">Azure Active Directory использует называемый «назначения» toodetermine пользователей, которые должны получать доступ tooselected приложений.</span><span class="sxs-lookup"><span data-stu-id="1aee5-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="1aee5-112">В контексте hello автоматический подготовки пользователей. учетной записи синхронизируются только hello пользователей и групп, назначенных» «tooan приложения в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1aee5-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="1aee5-113">Для настройки и включения hello подготовки службы, требуется toodecide какие пользователи или группы в Azure AD представляют Привет пользователей, которым требуется доступ tooyour приложение Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="1aee5-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Citrix GoToMeeting app.</span></span> <span data-ttu-id="1aee5-114">После приняла решение, можно назначить эти пользователи tooyour приложение Citrix GoToMeeting в соответствии с инструкциями hello здесь:</span><span class="sxs-lookup"><span data-stu-id="1aee5-114">Once decided, you can assign these users tooyour Citrix GoToMeeting app by following hello instructions here:</span></span>

[<span data-ttu-id="1aee5-115">Назначить пользователю или группе tooan корпоративного приложения</span><span class="sxs-lookup"><span data-stu-id="1aee5-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toocitrix-gotomeeting"></a><span data-ttu-id="1aee5-116">Важные советы для назначения пользователей tooCitrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="1aee5-116">Important tips for assigning users tooCitrix GoToMeeting</span></span>

*   <span data-ttu-id="1aee5-117">Рекомендуется один назначенный tooCitrix GoToMeeting tootest hello настройки подготовки пользователя Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1aee5-117">It is recommended that a single Azure AD user is assigned tooCitrix GoToMeeting tootest hello provisioning configuration.</span></span> <span data-ttu-id="1aee5-118">Дополнительные пользователи и/или группы можно назначить позднее.</span><span class="sxs-lookup"><span data-stu-id="1aee5-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="1aee5-119">При присвоении пользователя tooCitrix GoToMeeting, необходимо выбирать допустимой роли пользователя.</span><span class="sxs-lookup"><span data-stu-id="1aee5-119">When assigning a user tooCitrix GoToMeeting, you must select a valid user role.</span></span> <span data-ttu-id="1aee5-120">роль «Доступ по умолчанию» Hello не работает для подготовки.</span><span class="sxs-lookup"><span data-stu-id="1aee5-120">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="1aee5-121">Включение автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="1aee5-121">Enable Automated User Provisioning</span></span>

<span data-ttu-id="1aee5-122">Этот раздел поможет выполнить подключение подготовки API учетной записи пользователя GoToMeeting tooCitrix Azure AD и настройке подготовки службы toocreate hello, обновления и отключить пользователей, назначенные учетные записи в Citrix GoToMeeting на основе пользователей и группы Назначение в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1aee5-122">This section guides you through connecting your Azure AD tooCitrix GoToMeeting's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Citrix GoToMeeting based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="1aee5-123">Можно также выбрать tooenabled на основе SAML единого входа для Citrix GoToMeeting, следуя инструкциям hello в [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1aee5-123">You may also choose tooenabled SAML-based Single Sign-On for Citrix GoToMeeting, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="1aee5-124">Единый вход можно настроить независимо от автоматической подготовки, хотя эти две возможности дополняют друг друга.</span><span class="sxs-lookup"><span data-stu-id="1aee5-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-automatic-user-account-provisioning"></a><span data-ttu-id="1aee5-125">tooconfigure автоматический подготовки пользователей. учетной записи:</span><span class="sxs-lookup"><span data-stu-id="1aee5-125">tooconfigure automatic user account provisioning:</span></span>

1. <span data-ttu-id="1aee5-126">В hello [портал Azure](https://portal.azure.com), Обзор toohello **Azure Active Directory > корпоративных приложений > все приложения** раздела.</span><span class="sxs-lookup"><span data-stu-id="1aee5-126">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="1aee5-127">Если вы уже настроили Citrix GoToMeeting для единого входа, поиск экземпляра с помощью поля поиска hello Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="1aee5-127">If you have already configured Citrix GoToMeeting for single sign-on, search for your instance of Citrix GoToMeeting using hello search field.</span></span> <span data-ttu-id="1aee5-128">В противном случае выберите **добавить** и выполните поиск **Citrix GoToMeeting** в галерее приложения hello.</span><span class="sxs-lookup"><span data-stu-id="1aee5-128">Otherwise, select **Add** and search for **Citrix GoToMeeting** in hello application gallery.</span></span> <span data-ttu-id="1aee5-129">Выберите из результатов поиска hello Citrix GoToMeeting и добавьте его tooyour список приложений.</span><span class="sxs-lookup"><span data-stu-id="1aee5-129">Select Citrix GoToMeeting from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="1aee5-130">Выберите свой экземпляр Citrix GoToMeeting, а затем выберите hello **Provisioning** вкладки.</span><span class="sxs-lookup"><span data-stu-id="1aee5-130">Select your instance of Citrix GoToMeeting, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="1aee5-131">Набор hello **Provisioning** режиме слишком**автоматического**.</span><span class="sxs-lookup"><span data-stu-id="1aee5-131">Set hello **Provisioning** Mode too**Automatic**.</span></span> 

    ![подготовка](./media/active-directory-saas-citrixgotomeeting-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="1aee5-133">В области hello раздел учетные данные администратора выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="1aee5-133">Under hello Admin Credentials section, perform hello following steps:</span></span>
   
    <span data-ttu-id="1aee5-134">а.</span><span class="sxs-lookup"><span data-stu-id="1aee5-134">a.</span></span> <span data-ttu-id="1aee5-135">В hello **имя пользователя администратора Citrix GoToMeeting** текстовом поле введите имя пользователя hello администратора.</span><span class="sxs-lookup"><span data-stu-id="1aee5-135">In hello **Citrix GoToMeeting Admin User Name** textbox, type hello user name of an administrator.</span></span>

    <span data-ttu-id="1aee5-136">b.</span><span class="sxs-lookup"><span data-stu-id="1aee5-136">b.</span></span> <span data-ttu-id="1aee5-137">В hello **пароль администратора Citrix GoToMeeting** в текстовое поле пароля администратора hello.</span><span class="sxs-lookup"><span data-stu-id="1aee5-137">In hello **Citrix GoToMeeting Admin Password** textbox, hello administrator's password.</span></span>

6. <span data-ttu-id="1aee5-138">В hello портал Azure, щелкните **проверить подключение** tooensure Azure AD могут подключаться tooyour приложение Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="1aee5-138">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Citrix GoToMeeting app.</span></span> <span data-ttu-id="1aee5-139">При сбое подключения hello, убедитесь в вашей учетной записи Citrix GoToMeeting имеет разрешения администратора команды и повторите hello **«Учетные данные администратора»** еще один шаг.</span><span class="sxs-lookup"><span data-stu-id="1aee5-139">If hello connection fails, ensure your Citrix GoToMeeting account has Team Admin permissions and try hello **"Admin Credentials"** step again.</span></span>

7. <span data-ttu-id="1aee5-140">Введите адрес электронной почты hello пользователя или группы, которые должны получить уведомления о подготовке ошибки в hello **уведомление по электронной почте** поле и установите флажок "hello".</span><span class="sxs-lookup"><span data-stu-id="1aee5-140">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

8. <span data-ttu-id="1aee5-141">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="1aee5-141">Click **Save.**</span></span>

9. <span data-ttu-id="1aee5-142">Установите hello сопоставлений **синхронизации Azure Active Directory — пользователи tooCitrix GoToMeeting.**</span><span class="sxs-lookup"><span data-stu-id="1aee5-142">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooCitrix GoToMeeting.**</span></span>

10. <span data-ttu-id="1aee5-143">В hello **сопоставления атрибутов** просмотрите hello атрибутов пользователей, которые синхронизируются из Azure AD tooCitrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="1aee5-143">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooCitrix GoToMeeting.</span></span> <span data-ttu-id="1aee5-144">Здравствуйте, атрибуты, выбранные в качестве **сопоставление** свойства, используемые toomatch hello учетных записей пользователей в Citrix GoToMeeting для операций обновления.</span><span class="sxs-lookup"><span data-stu-id="1aee5-144">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Citrix GoToMeeting for update operations.</span></span> <span data-ttu-id="1aee5-145">Выберите toocommit кнопку hello сохранить все изменения.</span><span class="sxs-lookup"><span data-stu-id="1aee5-145">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="1aee5-146">tooenable hello подготовки службы Azure AD для Citrix GoToMeeting, изменение hello **состояние подготовки** слишком**на** в разделе "Параметры" hello</span><span class="sxs-lookup"><span data-stu-id="1aee5-146">tooenable hello Azure AD provisioning service for Citrix GoToMeeting, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

12. <span data-ttu-id="1aee5-147">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="1aee5-147">Click **Save.**</span></span>

<span data-ttu-id="1aee5-148">Он запускает hello Первоначальная синхронизация всех пользователей и/или группам назначается tooCitrix GoToMeeting в разделе hello пользователей и групп.</span><span class="sxs-lookup"><span data-stu-id="1aee5-148">It starts hello initial synchronization of any users and/or groups assigned tooCitrix GoToMeeting in hello Users and Groups section.</span></span> <span data-ttu-id="1aee5-149">Начальная синхронизация Hello принимает tooperform больше времени, чем последующие синхронизации, которые происходят примерно каждые 20 минут при условии, что запущена служба hello.</span><span class="sxs-lookup"><span data-stu-id="1aee5-149">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="1aee5-150">Можно использовать hello **сведения о синхронизации** статьи toomonitor хода выполнения и следуйте ссылки tooprovisioning отчеты о действиях, которые описывают все действия, выполняемые hello подготовки службы в приложении Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="1aee5-150">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Citrix GoToMeeting app.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1aee5-151">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="1aee5-151">Additional resources</span></span>

* [<span data-ttu-id="1aee5-152">Управление подготовкой учетных записей пользователей для корпоративных приложений</span><span class="sxs-lookup"><span data-stu-id="1aee5-152">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1aee5-153">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1aee5-153">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="1aee5-154">Настройка единого входа</span><span class="sxs-lookup"><span data-stu-id="1aee5-154">Configure Single Sign-on</span></span>](active-directory-saas-citrix-gotomeeting-tutorial.md)


