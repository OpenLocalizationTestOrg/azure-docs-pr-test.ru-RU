---
title: "Руководство по интеграции Azure Active Directory с Workplace by Facebook | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и рабочей области с Facebook."
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
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 551ec353a5ec1da936373587688c299a6f4acca7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-workplace-by-facebook-for-user-provisioning"></a><span data-ttu-id="5077f-103">Руководство по настройке Workplace by Facebook для подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="5077f-103">Tutorial: Configuring Workplace by Facebook for User Provisioning</span></span>

<span data-ttu-id="5077f-104">Цель этого учебника Hello — tooshow hello действия, которые следует tooperform в рабочей области с Facebook и Azure AD tooautomatically подготовки и Отмена подготовки учетных записей пользователей из Azure AD tooWorkplace с Facebook.</span><span class="sxs-lookup"><span data-stu-id="5077f-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Workplace by Facebook and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooWorkplace by Facebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5077f-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5077f-105">Prerequisites</span></span>

<span data-ttu-id="5077f-106">tooconfigure интеграция Azure AD в рабочей области с Facebook, требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="5077f-106">tooconfigure Azure AD integration with Workplace by Facebook, you need hello following items:</span></span>

- <span data-ttu-id="5077f-107">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="5077f-107">An Azure AD subscription</span></span>
- <span data-ttu-id="5077f-108">подписка Workplace by Facebook с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="5077f-108">A Workplace by Facebook single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5077f-109">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="5077f-109">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5077f-110">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="5077f-110">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5077f-111">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="5077f-111">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5077f-112">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5077f-112">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="assigning-users-tooworkplace-by-facebook"></a><span data-ttu-id="5077f-113">Назначение пользователей tooWorkplace с Facebook</span><span class="sxs-lookup"><span data-stu-id="5077f-113">Assigning users tooWorkplace by Facebook</span></span>

<span data-ttu-id="5077f-114">Azure Active Directory использует называемый «назначения» toodetermine пользователей, которые должны получать доступ tooselected приложений.</span><span class="sxs-lookup"><span data-stu-id="5077f-114">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="5077f-115">В контексте hello автоматический подготовки пользователей. учетной записи синхронизируются только hello пользователей и групп, назначенных» «tooan приложения в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5077f-115">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="5077f-116">Для настройки и включения hello подготовки службы, требуется toodecide какие пользователи или группы в Azure AD представляют Привет пользователей, которым требуется доступ tooyour рабочей области приложения Facebook.</span><span class="sxs-lookup"><span data-stu-id="5077f-116">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Workplace by Facebook app.</span></span> <span data-ttu-id="5077f-117">После приняла решение, можно назначить эти пользователи tooyour рабочей области, приложением Facebook в соответствии с инструкциями hello здесь:</span><span class="sxs-lookup"><span data-stu-id="5077f-117">Once decided, you can assign these users tooyour Workplace by Facebook app by following hello instructions here:</span></span>

[<span data-ttu-id="5077f-118">Назначить пользователю или группе tooan корпоративного приложения</span><span class="sxs-lookup"><span data-stu-id="5077f-118">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-tooworkplace-by-facebook"></a><span data-ttu-id="5077f-119">Важные советы для назначения пользователей tooWorkplace с Facebook</span><span class="sxs-lookup"><span data-stu-id="5077f-119">Important tips for assigning users tooWorkplace by Facebook</span></span>

*   <span data-ttu-id="5077f-120">Рекомендуется один tooWorkplace назначен пользователь Azure AD путем настройки подготовки hello tootest Facebook.</span><span class="sxs-lookup"><span data-stu-id="5077f-120">It is recommended that a single Azure AD user is assigned tooWorkplace by Facebook tootest hello provisioning configuration.</span></span> <span data-ttu-id="5077f-121">Дополнительные пользователи и/или группы можно назначить позднее.</span><span class="sxs-lookup"><span data-stu-id="5077f-121">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="5077f-122">При назначении tooWorkplace пользователя с Facebook, необходимо выбрать допустимой роли пользователя.</span><span class="sxs-lookup"><span data-stu-id="5077f-122">When assigning a user tooWorkplace by Facebook, you must select a valid user role.</span></span> <span data-ttu-id="5077f-123">роль «Доступ по умолчанию» Hello не работает для подготовки.</span><span class="sxs-lookup"><span data-stu-id="5077f-123">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="5077f-124">Включение подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="5077f-124">Enable User Provisioning</span></span>

<span data-ttu-id="5077f-125">Этот раздел поможет выполнить подключение к Azure AD tooWorkplace учетной записью Facebook подготовки API и настройке подготовки службы toocreate hello, обновления и отключить учетные записи пользователей, назначенные в рабочей области с Facebook, на основе пользователя и группы Назначение в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5077f-125">This section guides you through connecting your Azure AD tooWorkplace by Facebook's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Workplace by Facebook based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="5077f-126">Можно также выбрать tooenabled на основе SAML Single Sign-On для рабочей области с Facebook, следуя инструкциям hello в [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5077f-126">You may also choose tooenabled SAML-based Single Sign-On for Workplace by Facebook, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="5077f-127">Единый вход можно настроить независимо от автоматической подготовки, хотя эти две возможности дополняют друг друга.</span><span class="sxs-lookup"><span data-stu-id="5077f-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-user-account-provisioning-tooworkplace-by-facebook-in-azure-ad"></a><span data-ttu-id="5077f-128">tooconfigure учетная запись подготовки tooWorkplace с Facebook в Azure AD:</span><span class="sxs-lookup"><span data-stu-id="5077f-128">tooconfigure user account provisioning tooWorkplace by Facebook in Azure AD:</span></span>

<span data-ttu-id="5077f-129">Цель этого раздела Hello является toooutline как tooenable Подготовка пользователя Active Directory учетных записей tooWorkplace с Facebook.</span><span class="sxs-lookup"><span data-stu-id="5077f-129">hello objective of this section is toooutline how tooenable provisioning of Active Directory user accounts tooWorkplace by Facebook.</span></span>

<span data-ttu-id="5077f-130">Azure AD поддерживается tooautomatically hello возможность синхронизировать данные для учетной записи hello назначить пользователей tooWorkplace с Facebook.</span><span class="sxs-lookup"><span data-stu-id="5077f-130">Azure AD supports hello ability tooautomatically synchronize hello account details of assigned users tooWorkplace by Facebook.</span></span> <span data-ttu-id="5077f-131">Автоматический процесс синхронизации включает рабочей области по Facebook tooget hello данных tooauthorize пользователей для доступа, необходимые перед их выполнением toosign в для hello в первый раз.</span><span class="sxs-lookup"><span data-stu-id="5077f-131">This automatic synchronization enables Workplace by Facebook tooget hello data it needs tooauthorize users for access, before them attempting toosign in for hello first time.</span></span> <span data-ttu-id="5077f-132">Она также отменяет подготовку пользователей для Workplace by Facebook, если доступ для них отозван в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5077f-132">It also de-provisions users from Workplace by Facebook when access has been revoked in Azure AD.</span></span>

1. <span data-ttu-id="5077f-133">В hello [портал Azure](https://portal.azure.com), Обзор toohello **Azure Active Directory** > **корпоративных приложений** > **всех приложений** раздела.</span><span class="sxs-lookup"><span data-stu-id="5077f-133">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory** > **Enterprise Apps** > **All applications** section.</span></span>

2. <span data-ttu-id="5077f-134">Если вы уже настроили рабочему месту с Facebook для единого входа, поиск экземпляра рабочей области с Facebook с помощью поля поиска hello.</span><span class="sxs-lookup"><span data-stu-id="5077f-134">If you have already configured Workplace by Facebook for single sign-on, search for your instance of Workplace by Facebook using hello search field.</span></span> <span data-ttu-id="5077f-135">В противном случае выберите **добавить** и выполните поиск **рабочему месту с Facebook** в галерее приложения hello.</span><span class="sxs-lookup"><span data-stu-id="5077f-135">Otherwise, select **Add** and search for **Workplace by Facebook** in hello application gallery.</span></span> <span data-ttu-id="5077f-136">Выбор рабочей области с Facebook из результатов поиска hello и добавьте его tooyour список приложений.</span><span class="sxs-lookup"><span data-stu-id="5077f-136">Select Workplace by Facebook from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="5077f-137">Выберите свой экземпляр рабочему месту с Facebook, а затем выберите hello **Provisioning** вкладки.</span><span class="sxs-lookup"><span data-stu-id="5077f-137">Select your instance of Workplace by Facebook, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="5077f-138">Набор hello **режим подготовки** слишком**автоматического**.</span><span class="sxs-lookup"><span data-stu-id="5077f-138">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![подготовка](./media/active-directory-saas-workplacebyfacebook-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="5077f-140">В разделе hello **учетные данные администратора** статьи, введите секрет маркера hello и hello URL-адрес клиента рабочего места администратора Facebook.</span><span class="sxs-lookup"><span data-stu-id="5077f-140">Under hello **Admin Credentials** section, enter hello Secret Token and hello Tenant URL of your Workplace by Facebook administrator.</span></span>

6. <span data-ttu-id="5077f-141">В hello портал Azure, щелкните **проверить подключение** tooensure Azure AD могут подключаться tooyour рабочей области приложения Facebook.</span><span class="sxs-lookup"><span data-stu-id="5077f-141">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Workplace by Facebook app.</span></span> <span data-ttu-id="5077f-142">При сбое подключения hello, убедитесь, что рабочую область с учетной записью Facebook имеет разрешения администратора команды.</span><span class="sxs-lookup"><span data-stu-id="5077f-142">If hello connection fails, ensure your Workplace by Facebook account has Team Admin permissions.</span></span>

7. <span data-ttu-id="5077f-143">Введите адрес электронной почты hello пользователя или группы, которые должны получить уведомления о подготовке ошибки в hello **уведомление по электронной почте** поле и установите флажок "hello".</span><span class="sxs-lookup"><span data-stu-id="5077f-143">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

8. <span data-ttu-id="5077f-144">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="5077f-144">Click **Save.**</span></span>

9. <span data-ttu-id="5077f-145">Установите hello сопоставлений **tooWorkplace синхронизации Azure Active Directory-пользователи с Facebook.**</span><span class="sxs-lookup"><span data-stu-id="5077f-145">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooWorkplace by Facebook.**</span></span>

10. <span data-ttu-id="5077f-146">В hello **сопоставления атрибутов** просмотрите hello атрибутов пользователей, которые синхронизируются из tooWorkplace Azure AD с Facebook.</span><span class="sxs-lookup"><span data-stu-id="5077f-146">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooWorkplace by Facebook.</span></span> <span data-ttu-id="5077f-147">Здравствуйте, атрибуты, выбранные в качестве **сопоставление** свойства, используемые toomatch hello учетных записей пользователей в рабочей области с Facebook для операций обновления.</span><span class="sxs-lookup"><span data-stu-id="5077f-147">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Workplace by Facebook for update operations.</span></span> <span data-ttu-id="5077f-148">Выберите toocommit кнопку hello сохранить все изменения.</span><span class="sxs-lookup"><span data-stu-id="5077f-148">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="5077f-149">tooenable hello подготовки службы Azure AD для рабочей области с Facebook, изменение hello **состояние подготовки** слишком**на** в hello **параметры** раздела</span><span class="sxs-lookup"><span data-stu-id="5077f-149">tooenable hello Azure AD provisioning service for Workplace by Facebook, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

12. <span data-ttu-id="5077f-150">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="5077f-150">Click **Save.**</span></span>

<span data-ttu-id="5077f-151">Дополнительные сведения о том, как tooconfigure автоматической подготовки, в разделе [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)</span><span class="sxs-lookup"><span data-stu-id="5077f-151">For more information on how tooconfigure automatic provisioning, see [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)</span></span>

<span data-ttu-id="5077f-152">Теперь можно создать тестовую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="5077f-152">You can now create a test account.</span></span> <span data-ttu-id="5077f-153">Дождитесь копирование минут too20 tooverify, hello учетная запись была синхронизирована tooWorkplace с Facebook.</span><span class="sxs-lookup"><span data-stu-id="5077f-153">Wait for up too20 minutes tooverify that hello account has been synchronized tooWorkplace by Facebook.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5077f-154">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="5077f-154">Additional resources</span></span>

* [<span data-ttu-id="5077f-155">Управление подготовкой учетных записей пользователей для корпоративных приложений</span><span class="sxs-lookup"><span data-stu-id="5077f-155">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5077f-156">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5077f-156">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="5077f-157">Настройка единого входа</span><span class="sxs-lookup"><span data-stu-id="5077f-157">Configure Single Sign-on</span></span>](active-directory-saas-workplacebyfacebook-tutorial.md)

