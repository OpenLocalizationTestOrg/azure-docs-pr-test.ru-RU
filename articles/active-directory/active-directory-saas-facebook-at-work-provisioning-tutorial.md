---
title: "Руководство по настройке подготовки пользователей в Workplace by Facebook | Документация Майкрософт"
description: "Узнайте, как tooautomatically подготовки и Отмена подготовки учетные записи из Azure AD tooWorkplace с Facebook."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6341e67e-8ce6-42dc-a4ea-7295904a53ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 33d294dbc8f441b29138408b3c9ca41f2141f8af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configure-workplace-by-facebook-for-user-provisioning"></a><span data-ttu-id="62e7b-103">Руководство по настройке Workplace by Facebook для подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="62e7b-103">Tutorial: Configure Workplace by Facebook for user provisioning</span></span>

<span data-ttu-id="62e7b-104">Этот учебник показывает, hello tooautomatically необходимые действия предоставлять и отзывать учетные записи пользователей из Azure Active Directory (Azure AD) tooWorkplace с Facebook.</span><span class="sxs-lookup"><span data-stu-id="62e7b-104">This tutorial shows you hello steps necessary tooautomatically provision and de-provision user accounts from Azure Active Directory (Azure AD) tooWorkplace by Facebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="62e7b-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="62e7b-105">Prerequisites</span></span>

<span data-ttu-id="62e7b-106">tooconfigure интеграция Azure AD в рабочей области с Facebook, необходимы следующие hello.</span><span class="sxs-lookup"><span data-stu-id="62e7b-106">tooconfigure Azure AD integration with Workplace by Facebook, you need hello following:</span></span>

- <span data-ttu-id="62e7b-107">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="62e7b-107">An Azure AD subscription</span></span>
- <span data-ttu-id="62e7b-108">подписка Workplace by Facebook с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="62e7b-108">A Workplace by Facebook single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="62e7b-109">tootest hello шаги в этом учебнике, придерживайтесь следующих рекомендаций:</span><span class="sxs-lookup"><span data-stu-id="62e7b-109">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="62e7b-110">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="62e7b-110">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="62e7b-111">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="62e7b-111">If you don't have an Azure AD trial environment, you can get a [one-month trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="assign-users-tooworkplace-by-facebook"></a><span data-ttu-id="62e7b-112">Назначить пользователей tooWorkplace с Facebook</span><span class="sxs-lookup"><span data-stu-id="62e7b-112">Assign users tooWorkplace by Facebook</span></span>

<span data-ttu-id="62e7b-113">Azure AD использует называемый «назначения» toodetermine пользователей, которые должны получать доступ tooselected приложений.</span><span class="sxs-lookup"><span data-stu-id="62e7b-113">Azure AD uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="62e7b-114">В контексте hello автоматический подготовки пользователей. учетной записи синхронизируются только hello пользователей и групп, которые были назначены tooan приложения в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="62e7b-114">In hello context of automatic user account provisioning, only hello users and groups that have been assigned tooan application in Azure AD are synchronized.</span></span>

<span data-ttu-id="62e7b-115">Прежде чем решить, настройке и включении hello подготовки службы, какие пользователи и группы в Azure AD представляют Привет пользователей, которым требуется доступ tooyour рабочей области приложения Facebook.</span><span class="sxs-lookup"><span data-stu-id="62e7b-115">Before configuring and enabling hello provisioning service, decide what users and groups in Azure AD represent hello users who need access tooyour Workplace by Facebook app.</span></span> <span data-ttu-id="62e7b-116">Вы можете назначить эти пользователи tooyour рабочей области, приложением Facebook, следуя инструкциям hello [назначить пользователю или группе tooan корпоративного приложения](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="62e7b-116">You can then assign these users tooyour Workplace by Facebook app by following hello instructions in [Assign a user or group tooan enterprise app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal).</span></span>

>[!IMPORTANT]
>*   <span data-ttu-id="62e7b-117">Hello тест инициализации конфигурации путем назначения одной tooWorkplace пользователя Azure AD с Facebook.</span><span class="sxs-lookup"><span data-stu-id="62e7b-117">Test hello provisioning configuration by assigning a single Azure AD user tooWorkplace by Facebook.</span></span> <span data-ttu-id="62e7b-118">Дополнительных пользователей и группы можно будет назначить позже.</span><span class="sxs-lookup"><span data-stu-id="62e7b-118">Assign additional users and groups later.</span></span>
>*   <span data-ttu-id="62e7b-119">При назначении tooWorkplace пользователя с Facebook, необходимо выбрать допустимой роли пользователя.</span><span class="sxs-lookup"><span data-stu-id="62e7b-119">When you assign a user tooWorkplace by Facebook, you must select a valid user role.</span></span> <span data-ttu-id="62e7b-120">роли доступа по умолчанию Hello не работает для подготовки.</span><span class="sxs-lookup"><span data-stu-id="62e7b-120">hello Default Access role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="62e7b-121">Включение автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="62e7b-121">Enable automated user provisioning</span></span>

<span data-ttu-id="62e7b-122">Этот раздел поможет выполнить подключение учетной записи пользователя toohello Azure AD подготовки API из рабочей области с Facebook.</span><span class="sxs-lookup"><span data-stu-id="62e7b-122">This section guides you through connecting your Azure AD toohello user account provisioning API of Workplace by Facebook.</span></span> <span data-ttu-id="62e7b-123">Вы также узнаете, как обновить toocreate tooconfigure hello подготовки службы и отключить учетные записи пользователей, назначенные в рабочей области с Facebook.</span><span class="sxs-lookup"><span data-stu-id="62e7b-123">You also learn how tooconfigure hello provisioning service toocreate, update, and disable assigned user accounts in Workplace by Facebook.</span></span> <span data-ttu-id="62e7b-124">Это зависит от назначенных пользователей и групп в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="62e7b-124">This is based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="62e7b-125">Вы также можете tooenabled SSO на основе SAML для рабочей области с Facebook, по следующие hello следуйте инструкциям в hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="62e7b-125">You can also choose tooenabled SAML-based SSO for Workplace by Facebook, by following hello instructions provided in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="62e7b-126">Единый вход можно настроить независимо от автоматической подготовки, хотя две эти функции дополняют друг друга.</span><span class="sxs-lookup"><span data-stu-id="62e7b-126">SSO can be configured independently of automatic provisioning, though these two features complement each other.</span></span>

### <a name="configure-user-account-provisioning-tooworkplace-by-facebook-in-azure-ad"></a><span data-ttu-id="62e7b-127">Настройка учетной записи пользователя, подготовку tooWorkplace с Facebook в Azure AD</span><span class="sxs-lookup"><span data-stu-id="62e7b-127">Configure user account provisioning tooWorkplace by Facebook in Azure AD</span></span>

<span data-ttu-id="62e7b-128">Azure AD поддерживается tooautomatically hello возможность синхронизировать данные для учетной записи hello назначить пользователей tooWorkplace с Facebook.</span><span class="sxs-lookup"><span data-stu-id="62e7b-128">Azure AD supports hello ability tooautomatically synchronize hello account details of assigned users tooWorkplace by Facebook.</span></span> <span data-ttu-id="62e7b-129">Автоматический процесс синхронизации включает рабочей области по Facebook tooget hello данных tooauthorize пользователей для доступа, необходимые перед их выполнением toosign в для hello в первый раз.</span><span class="sxs-lookup"><span data-stu-id="62e7b-129">This automatic synchronization enables Workplace by Facebook tooget hello data it needs tooauthorize users for access, before them attempting toosign in for hello first time.</span></span> <span data-ttu-id="62e7b-130">Она также отменяет подготовку пользователей для Workplace by Facebook, если доступ для них отозван в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="62e7b-130">It also de-provisions users from Workplace by Facebook when access has been revoked in Azure AD.</span></span>

1. <span data-ttu-id="62e7b-131">В hello [портал Azure](https://portal.azure.com)выберите **Azure Active Directory** > **корпоративных приложений** > **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="62e7b-131">In hello [Azure portal](https://portal.azure.com), select **Azure Active Directory** > **Enterprise Apps** > **All applications**.</span></span>

2. <span data-ttu-id="62e7b-132">Если вы уже настроили рабочему месту с Facebook для единого входа, выполните поиск экземпляра рабочей области с Facebook с помощью поля поиска hello.</span><span class="sxs-lookup"><span data-stu-id="62e7b-132">If you have already configured Workplace by Facebook for SSO, search for your instance of Workplace by Facebook by using hello search field.</span></span> <span data-ttu-id="62e7b-133">В противном случае выберите **добавить** и выполните поиск **рабочему месту с Facebook** в галерее приложения hello.</span><span class="sxs-lookup"><span data-stu-id="62e7b-133">Otherwise, select **Add** and search for **Workplace by Facebook** in hello application gallery.</span></span> <span data-ttu-id="62e7b-134">Выберите **рабочему месту с Facebook** из hello результаты поиска и добавьте его tooyour список приложений.</span><span class="sxs-lookup"><span data-stu-id="62e7b-134">Select **Workplace by Facebook** from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="62e7b-135">Выберите свой экземпляр рабочему месту с Facebook, а затем выберите hello **Provisioning** вкладки.</span><span class="sxs-lookup"><span data-stu-id="62e7b-135">Select your instance of Workplace by Facebook, and then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="62e7b-136">Задать **режим подготовки** слишком**автоматического**.</span><span class="sxs-lookup"><span data-stu-id="62e7b-136">Set **Provisioning Mode** too**Automatic**.</span></span> 

    ![Снимок экрана параметров подготовки Workplace by Facebook](./media/active-directory-saas-facebook-at-work-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="62e7b-138">В разделе hello **учетные данные администратора** введите hello **секрет маркера** и hello **URL-адрес клиента** рабочего места администратора Facebook.</span><span class="sxs-lookup"><span data-stu-id="62e7b-138">Under hello **Admin Credentials** section, enter hello **Secret Token** and hello **Tenant URL** of your Workplace by Facebook administrator.</span></span>

6. <span data-ttu-id="62e7b-139">В hello портал Azure, выберите **проверить подключение** tooensure Azure AD могут подключаться tooyour рабочей области приложения Facebook.</span><span class="sxs-lookup"><span data-stu-id="62e7b-139">In hello Azure portal, select **Test Connection** tooensure Azure AD can connect tooyour Workplace by Facebook app.</span></span> <span data-ttu-id="62e7b-140">При сбое подключения hello, убедитесь в наличии разрешения администратора команды в рабочую область с учетной записью Facebook.</span><span class="sxs-lookup"><span data-stu-id="62e7b-140">If hello connection fails, ensure that your Workplace by Facebook account has Team Admin permissions.</span></span>

7. <span data-ttu-id="62e7b-141">Введите адрес электронной почты hello пользователя или группы, которые должны получить уведомления о подготовке ошибки в hello **уведомление по электронной почте** поля и приветствия установите флажок.</span><span class="sxs-lookup"><span data-stu-id="62e7b-141">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello check box.</span></span>

8. <span data-ttu-id="62e7b-142">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="62e7b-142">Select **Save**.</span></span>

9. <span data-ttu-id="62e7b-143">Установите hello сопоставлений **tooWorkplace синхронизации Azure Active Directory-пользователи с Facebook**.</span><span class="sxs-lookup"><span data-stu-id="62e7b-143">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooWorkplace by Facebook**.</span></span>

10. <span data-ttu-id="62e7b-144">В hello **сопоставления атрибутов** просмотрите hello атрибутов пользователей, которые синхронизируются из tooWorkplace Azure AD с Facebook.</span><span class="sxs-lookup"><span data-stu-id="62e7b-144">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooWorkplace by Facebook.</span></span> <span data-ttu-id="62e7b-145">Здравствуйте, атрибуты, выбранные в качестве **сопоставление** свойства, используемые toomatch hello учетных записей пользователей в рабочей области с Facebook для операций обновления.</span><span class="sxs-lookup"><span data-stu-id="62e7b-145">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Workplace by Facebook for update operations.</span></span> <span data-ttu-id="62e7b-146">Выберите любые изменения toocommit **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="62e7b-146">toocommit any changes, select **Save**.</span></span>

11. <span data-ttu-id="62e7b-147">tooenable hello подготовки службы Azure AD для рабочей области с Facebook, в hello **параметры** измените hello **состояние подготовки** слишком**на**.</span><span class="sxs-lookup"><span data-stu-id="62e7b-147">tooenable hello Azure AD provisioning service for Workplace by Facebook, in hello **Settings** section, change hello **Provisioning Status** too**On**.</span></span>

12. <span data-ttu-id="62e7b-148">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="62e7b-148">Select **Save**.</span></span>

<span data-ttu-id="62e7b-149">Дополнительные сведения о том, как tooconfigure автоматической подготовки, в разделе [hello Facebook документации](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers).</span><span class="sxs-lookup"><span data-stu-id="62e7b-149">For more information on how tooconfigure automatic provisioning, see [hello Facebook documentation](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers).</span></span>

<span data-ttu-id="62e7b-150">Теперь можно создать тестовую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="62e7b-150">You can now create a test account.</span></span> <span data-ttu-id="62e7b-151">Дождитесь копирование минут too20 tooverify, hello учетная запись была синхронизирована tooWorkplace с Facebook.</span><span class="sxs-lookup"><span data-stu-id="62e7b-151">Wait for up too20 minutes tooverify that hello account has been synchronized tooWorkplace by Facebook.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="62e7b-152">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="62e7b-152">Additional resources</span></span>

* [<span data-ttu-id="62e7b-153">Управление подготовкой учетных записей пользователей для корпоративных приложений</span><span class="sxs-lookup"><span data-stu-id="62e7b-153">Managing user account provisioning for enterprise apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="62e7b-154">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="62e7b-154">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="62e7b-155">Настройка единого входа</span><span class="sxs-lookup"><span data-stu-id="62e7b-155">Configure single sign-on</span></span>](active-directory-saas-facebook-at-work-tutorial.md)

