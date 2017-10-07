---
title: "Руководство по настройке Google Apps для автоматической подготовки пользователей в Azure | Документация Майкрософт"
description: "Узнайте, как tooautomatically подготовки и Отмена подготовки учетные записи из Azure AD tooGoogle приложений."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6dbd50b5-589f-4132-b9eb-a53a318a64e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: d1fa8449bd6013d1627b3552aaa19db1c0f4f46f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-google-apps-for-automatic-user-provisioning"></a><span data-ttu-id="ba454-103">Руководство по настройке Google Apps для автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="ba454-103">Tutorial: Configuring Google Apps for automatic user provisioning</span></span>

<span data-ttu-id="ba454-104">Цель этого учебника Hello — tooshow hello шаги требуются tooperform в Google Apps и Azure AD tooautomatically подготовки и отменять подготовки учетных записей пользователей из Azure AD tooGoogle приложений.</span><span class="sxs-lookup"><span data-stu-id="ba454-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Google Apps and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooGoogle Apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ba454-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ba454-105">Prerequisites</span></span>

<span data-ttu-id="ba454-106">Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="ba454-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="ba454-107">клиент Azure Active Directory;</span><span class="sxs-lookup"><span data-stu-id="ba454-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="ba454-108">Действительный клиент для Google Apps for Work или Google Apps for Education.</span><span class="sxs-lookup"><span data-stu-id="ba454-108">You must have a valid tenant for Google Apps for Work or Google Apps for Education.</span></span> <span data-ttu-id="ba454-109">Для любой из этих служб можно воспользоваться бесплатной пробной учетной записью.</span><span class="sxs-lookup"><span data-stu-id="ba454-109">You may use a free trial account for either service.</span></span>
*   <span data-ttu-id="ba454-110">Учетная запись пользователя Google Apps с разрешениями администратора команды.</span><span class="sxs-lookup"><span data-stu-id="ba454-110">A user account in Google Apps with Team Admin permissions.</span></span>

## <a name="assigning-users-toogoogle-apps"></a><span data-ttu-id="ba454-111">Назначение пользователей tooGoogle приложений</span><span class="sxs-lookup"><span data-stu-id="ba454-111">Assigning users tooGoogle Apps</span></span>

<span data-ttu-id="ba454-112">Azure Active Directory использует называемый «назначения» toodetermine пользователей, которые должны получать доступ tooselected приложений.</span><span class="sxs-lookup"><span data-stu-id="ba454-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="ba454-113">В контексте hello автоматический подготовки пользователей. учетной записи синхронизируются только hello пользователей и групп, назначенных» «tooan приложения в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ba454-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="ba454-114">Для настройки и включения hello подготовки службы, требуется toodecide какие пользователи или группы в Azure AD представляют Привет пользователям требуется доступ к приложению tooyour Google Apps.</span><span class="sxs-lookup"><span data-stu-id="ba454-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Google Apps app.</span></span> <span data-ttu-id="ba454-115">После приняла решение, можно назначить эти приложения пользователям tooyour Google Apps, следуя инструкциям hello: [назначить пользователю или группе tooan корпоративного приложения](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)</span><span class="sxs-lookup"><span data-stu-id="ba454-115">Once decided, you can assign these users tooyour Google Apps app by following hello instructions here: [Assign a user or group tooan enterprise app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)</span></span>

> [!IMPORTANT]
>*   <span data-ttu-id="ba454-116">Рекомендуется один назначить tooGoogle приложений tootest hello настройки подготовки пользователя Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ba454-116">It is recommended that a single Azure AD user be assigned tooGoogle Apps tootest hello provisioning configuration.</span></span> <span data-ttu-id="ba454-117">Дополнительные пользователи и/или группы можно назначить позднее.</span><span class="sxs-lookup"><span data-stu-id="ba454-117">Additional users and/or groups may be assigned later.</span></span>
>*   <span data-ttu-id="ba454-118">При назначении tooGoogle пользователя приложения, необходимо выбрать hello пользователя или роли «Группа» в диалоговом окне приветствия назначения.</span><span class="sxs-lookup"><span data-stu-id="ba454-118">When assigning a user tooGoogle Apps, you must select hello User or "Group" role in hello assignment dialog.</span></span> <span data-ttu-id="ba454-119">роль «Доступ по умолчанию» Hello не работает для подготовки.</span><span class="sxs-lookup"><span data-stu-id="ba454-119">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="ba454-120">Включение автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="ba454-120">Enable automated user provisioning</span></span>

<span data-ttu-id="ba454-121">Этот раздел поможет выполнить подключение подготовки API учетной записи пользователя приложения tooGoogle Azure AD и настройке подготовки службы toocreate hello, обновления и отключить учетные записи пользователей, назначенные в Google Apps, в зависимости от назначения пользователей и групп в Azure AD .</span><span class="sxs-lookup"><span data-stu-id="ba454-121">This section guides you through connecting your Azure AD tooGoogle Apps's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Google Apps based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="ba454-122">Можно также выбрать tooenabled на основе SAML Single Sign-On для Google Apps, следуя инструкциям hello в [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ba454-122">You may also choose tooenabled SAML-based Single Sign-On for Google Apps, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="ba454-123">Единый вход можно настроить независимо от автоматической подготовки, хотя эти две возможности дополняют друг друга.</span><span class="sxs-lookup"><span data-stu-id="ba454-123">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="configure-automatic-user-account-provisioning"></a><span data-ttu-id="ba454-124">Настройка автоматической подготовки учетных записей пользователей</span><span class="sxs-lookup"><span data-stu-id="ba454-124">Configure automatic user account provisioning</span></span>

> [!NOTE]
> <span data-ttu-id="ba454-125">Другой возможных вариантов для автоматизации приложений tooGoogle подготовки пользователей – toouse [синхронизации каталогов Google Apps (GADS)](https://support.google.com/a/answer/106368?hl=en) которого подготавливает вашей локальной Active Directory удостоверения tooGoogle приложений.</span><span class="sxs-lookup"><span data-stu-id="ba454-125">Another viable option for automating user provisioning tooGoogle Apps is toouse [Google Apps Directory Sync (GADS)](https://support.google.com/a/answer/106368?hl=en) which provisions your on-premises Active Directory identities tooGoogle Apps.</span></span> <span data-ttu-id="ba454-126">В отличие от этого решение hello в этом учебнике подготавливает Azure Active Directory (облако) пользователей и групп с включенной поддержкой почты tooGoogle приложений.</span><span class="sxs-lookup"><span data-stu-id="ba454-126">In contrast, hello solution in this tutorial provisions your Azure Active Directory (cloud) users and mail-enabled groups tooGoogle Apps.</span></span> 

1. <span data-ttu-id="ba454-127">Вход в hello [консоли администрирования приложения Google](http://admin.google.com/) с помощью учетной записи администратора и нажмите кнопку **безопасности**.</span><span class="sxs-lookup"><span data-stu-id="ba454-127">Sign into hello [Google Apps Admin Console](http://admin.google.com/) using your administrator account, and click **Security**.</span></span> <span data-ttu-id="ba454-128">Если вы не видите ссылку hello, они могут быть скрыты в hello **другие элементы** меню hello нижней части экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="ba454-128">If you don't see hello link, it may be hidden under hello **More Controls** menu at hello bottom of hello screen.</span></span>
   
    ![Выбор элемента "Безопасность"][10]

2. <span data-ttu-id="ba454-130">На hello **безопасности** щелкните **Справочник по API**.</span><span class="sxs-lookup"><span data-stu-id="ba454-130">On hello **Security** page, click **API Reference**.</span></span>
   
    ![Выбор элемента "Справочник по API".][15]

3. <span data-ttu-id="ba454-132">Выберите команду **Enable API access**(Включить доступ через API).</span><span class="sxs-lookup"><span data-stu-id="ba454-132">Select **Enable API access**.</span></span>
   
    ![Выбор элемента "Справочник по API".][16]

    > [!IMPORTANT]
    > <span data-ttu-id="ba454-134">Для каждого пользователя, следует присвоить tooprovision tooGoogle приложений, их имена пользователей в Azure Active Directory *должен* быть равноценных tooa пользовательского домена.</span><span class="sxs-lookup"><span data-stu-id="ba454-134">For every user that you intend tooprovision tooGoogle Apps, their username in Azure Active Directory *must* be tied tooa custom domain.</span></span> <span data-ttu-id="ba454-135">Например, такие имена пользователей, как bob@contoso.onmicrosoft.com, не будут приняты Google Apps, а bob@contoso.com — будут.</span><span class="sxs-lookup"><span data-stu-id="ba454-135">For example, usernames that look like bob@contoso.onmicrosoft.com is not accepted by Google Apps, whereas bob@contoso.com is accepted.</span></span> <span data-ttu-id="ba454-136">Вы можете изменить текущий домен пользователя, изменив его свойства в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ba454-136">You can change an existing user's domain by editing their properties in Azure AD.</span></span> <span data-ttu-id="ba454-137">Инструкции для как tooset пользовательского домена для Azure Active Directory и Google Apps включены в следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ba454-137">Instructions for how tooset a custom domain for both Azure Active Directory and Google Apps are included in following steps.</span></span>
      
4. <span data-ttu-id="ba454-138">Если еще не добавлены tooyour имя пользовательского домена Azure Active Directory, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ba454-138">If you haven't added a custom domain name tooyour Azure Active Directory yet, then follow hello following steps:</span></span>
  
    <span data-ttu-id="ba454-139">а.</span><span class="sxs-lookup"><span data-stu-id="ba454-139">a.</span></span> <span data-ttu-id="ba454-140">В hello [портал Azure](https://portal.azure.com), на левой панели навигации hello, нажмите кнопку **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ba454-140">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span> <span data-ttu-id="ba454-141">В списке каталогов hello выберите свой каталог.</span><span class="sxs-lookup"><span data-stu-id="ba454-141">In hello directory list, select your directory.</span></span> 

    <span data-ttu-id="ba454-142">b.</span><span class="sxs-lookup"><span data-stu-id="ba454-142">b.</span></span> <span data-ttu-id="ba454-143">Нажмите кнопку **имя домена** на левой панели навигации hello и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="ba454-143">Click **Domains name** on hello left navigation pane, and then click **Add**.</span></span>
     
     ![Домен](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_1.png)

     ![Добавление домена](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_2.png)

    <span data-ttu-id="ba454-146">c.</span><span class="sxs-lookup"><span data-stu-id="ba454-146">c.</span></span> <span data-ttu-id="ba454-147">Введите имя домена в hello **доменное имя** поля.</span><span class="sxs-lookup"><span data-stu-id="ba454-147">Type your domain name into hello **Domain name** field.</span></span> <span data-ttu-id="ba454-148">Это имя домена должно быть hello таким же именем домена, требуется toouse Google Apps.</span><span class="sxs-lookup"><span data-stu-id="ba454-148">This domain name should be hello same domain name that you intend toouse for Google Apps.</span></span> <span data-ttu-id="ba454-149">Когда все будет готово, нажмите кнопку hello **добавить домен** кнопки.</span><span class="sxs-lookup"><span data-stu-id="ba454-149">When ready, click hello **Add Domain** button.</span></span>
     
     ![Доменное имя](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_3.png)

    <span data-ttu-id="ba454-151">d.</span><span class="sxs-lookup"><span data-stu-id="ba454-151">d.</span></span> <span data-ttu-id="ba454-152">Нажмите кнопку **Далее** toogo toohello проверки страницы.</span><span class="sxs-lookup"><span data-stu-id="ba454-152">Click **Next** toogo toohello verification page.</span></span> <span data-ttu-id="ba454-153">tooverify, что вы являетесь владельцем этого домена, необходимо изменить записи DNS домена hello в соответствии с toohello значения, представленные на этой странице.</span><span class="sxs-lookup"><span data-stu-id="ba454-153">tooverify that you own this domain, you must edit hello domain's DNS records according toohello values provided on this page.</span></span> <span data-ttu-id="ba454-154">Вы можете с помощью tooverify **записей MX** или **записи TXT**, в зависимости от выбора для hello **тип записи** параметр.</span><span class="sxs-lookup"><span data-stu-id="ba454-154">You may choose tooverify using either **MX records** or **TXT records**, depending on what you select for hello **Record Type** option.</span></span> <span data-ttu-id="ba454-155">Более полные инструкции как tooverify имя домена по умолчанию в Azure AD, [добавить собственные tooAzure имя домена AD](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="ba454-155">For more comprehensive instructions on how tooverify domain name with Azure AD, refer [Add your own domain name tooAzure AD](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409).</span></span>
     
     ![Домен](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_4.png)

    <span data-ttu-id="ba454-157">д.</span><span class="sxs-lookup"><span data-stu-id="ba454-157">e.</span></span> <span data-ttu-id="ba454-158">Повторите hello в предыдущих шагах, для всех доменов hello, следует присвоить tooadd tooyour каталога.</span><span class="sxs-lookup"><span data-stu-id="ba454-158">Repeat hello preceding steps for all hello domains that you intend tooadd tooyour directory.</span></span>

5. <span data-ttu-id="ba454-159">После подтверждения всех доменов в Azure AD необходимо подтвердить их в Google Apps.</span><span class="sxs-lookup"><span data-stu-id="ba454-159">Now that you have verified all your domains with Azure AD, you must now verify them again with Google Apps.</span></span> <span data-ttu-id="ba454-160">Для каждого домена, который еще не зарегистрирован с Google Apps выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="ba454-160">For each domain that isn't already registered with Google Apps, perform hello following steps:</span></span>
   
    <span data-ttu-id="ba454-161">а.</span><span class="sxs-lookup"><span data-stu-id="ba454-161">a.</span></span> <span data-ttu-id="ba454-162">В hello [консоли администрирования приложения Google](http://admin.google.com/), нажмите кнопку **домены**.</span><span class="sxs-lookup"><span data-stu-id="ba454-162">In hello [Google Apps Admin Console](http://admin.google.com/), click **Domains**.</span></span>
     
     ![Выбор элемента "Домены"][20]

    <span data-ttu-id="ba454-164">b.</span><span class="sxs-lookup"><span data-stu-id="ba454-164">b.</span></span> <span data-ttu-id="ba454-165">Щелкните **Add a domain or a domain alias**(Добавить домен или псевдоним домена).</span><span class="sxs-lookup"><span data-stu-id="ba454-165">Click **Add a domain or a domain alias**.</span></span>
     
     ![Добавление нового домена][21]

    <span data-ttu-id="ba454-167">c.</span><span class="sxs-lookup"><span data-stu-id="ba454-167">c.</span></span> <span data-ttu-id="ba454-168">Выберите **добавить другой домен**и введите имя hello, желательно tooadd домена hello.</span><span class="sxs-lookup"><span data-stu-id="ba454-168">Select **Add another domain**, and type in hello name of hello domain that you would like tooadd.</span></span>
     
     ![Ввод доменного имени][22]

    <span data-ttu-id="ba454-170">г)</span><span class="sxs-lookup"><span data-stu-id="ba454-170">d.</span></span> <span data-ttu-id="ba454-171">Щелкните **Continue and verify domain ownership** (Перейти к проверке владельца домена).</span><span class="sxs-lookup"><span data-stu-id="ba454-171">Click **Continue and verify domain ownership**.</span></span> <span data-ttu-id="ba454-172">Затем выполните шаги tooverify hello, что вы являетесь владельцем hello доменное имя.</span><span class="sxs-lookup"><span data-stu-id="ba454-172">Then follow hello steps tooverify that you own hello domain name.</span></span> <span data-ttu-id="ba454-173">Для подробных инструкций на tooverify домена с Google Apps. в статье.</span><span class="sxs-lookup"><span data-stu-id="ba454-173">For comprehensive instructions on how tooverify your domain with Google Apps, see.</span></span> <span data-ttu-id="ba454-174">[Как подтвердить право собственности на сайт](https://support.google.com/webmasters/answer/35179).</span><span class="sxs-lookup"><span data-stu-id="ba454-174">[Verify your site ownership with Google Apps](https://support.google.com/webmasters/answer/35179).</span></span>

    <span data-ttu-id="ba454-175">д.</span><span class="sxs-lookup"><span data-stu-id="ba454-175">e.</span></span> <span data-ttu-id="ba454-176">Повторите предыдущих шагах для дополнительных доменов, следует присвоить tooadd tooGoogle приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ba454-176">Repeat hello preceding steps for any additional domains that you intend tooadd tooGoogle Apps.</span></span>
     
     > [!WARNING]
     > <span data-ttu-id="ba454-177">Если изменить основной домен hello для вашего клиента Google Apps, и если имеется уже настроены единый вход в Azure AD, то у вас есть toorepeat шаг #3 в разделе [два шага: Включение единого входа](#step-two-enable-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="ba454-177">If you change hello primary domain for your Google Apps tenant, and if you have already configured single sign-on with Azure AD, then you have toorepeat step #3 under [Step Two: Enable Single Sign-On](#step-two-enable-single-sign-on).</span></span>
       
6. <span data-ttu-id="ba454-178">В hello [консоли администрирования приложения Google](http://admin.google.com/), нажмите кнопку **роли администратора**.</span><span class="sxs-lookup"><span data-stu-id="ba454-178">In hello [Google Apps Admin Console](http://admin.google.com/), click **Admin Roles**.</span></span>
   
     ![Выбор Google Apps][26]

7. <span data-ttu-id="ba454-180">Определить, какие администратора учетной записи, хотелось бы toouse toomanage подготовку учетных записей пользователей.</span><span class="sxs-lookup"><span data-stu-id="ba454-180">Determine which admin account you would like toouse toomanage user provisioning.</span></span> <span data-ttu-id="ba454-181">Для hello **роли администратора** для этой учетной записи, изменять hello **права** для этой роли.</span><span class="sxs-lookup"><span data-stu-id="ba454-181">For hello **admin role** of that account, edit hello **Privileges** for that role.</span></span> <span data-ttu-id="ba454-182">Убедитесь, что она содержит все hello **права доступа администратора API** таким образом, эта учетная запись может использоваться для подготовки.</span><span class="sxs-lookup"><span data-stu-id="ba454-182">Make sure it has all hello **Admin API Privileges** enabled so that this account can be used for provisioning.</span></span>
   
     ![Выбор Google Apps][27]
   
    > [!NOTE]
    > <span data-ttu-id="ba454-184">При настройке рабочей среде рекомендуется hello является toocreate учетной записи администратора в Google Apps специально для этого шага.</span><span class="sxs-lookup"><span data-stu-id="ba454-184">If you are configuring a production environment, hello best practice is toocreate an admin account in Google Apps specifically for this step.</span></span> <span data-ttu-id="ba454-185">Эти учетные записи должны иметь связанный с ним роли администратора, имеет необходимые привилегии API hello.</span><span class="sxs-lookup"><span data-stu-id="ba454-185">These accounts must have an admin role associated with it that has hello necessary API privileges.</span></span>
     
8. <span data-ttu-id="ba454-186">В hello [портал Azure](https://portal.azure.com), Обзор toohello **Azure Active Directory > корпоративных приложений > все приложения** раздела.</span><span class="sxs-lookup"><span data-stu-id="ba454-186">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

9. <span data-ttu-id="ba454-187">Если вы уже настроили Google Apps для единого входа, поиск экземпляра с помощью поля поиска hello Google Apps.</span><span class="sxs-lookup"><span data-stu-id="ba454-187">If you have already configured Google Apps for single sign-on, search for your instance of Google Apps using hello search field.</span></span> <span data-ttu-id="ba454-188">В противном случае выберите **добавить** и выполните поиск **Google Apps** в галерее приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ba454-188">Otherwise, select **Add** and search for **Google Apps** in hello application gallery.</span></span> <span data-ttu-id="ba454-189">Выберите из результатов поиска hello Google Apps и добавьте его tooyour список приложений.</span><span class="sxs-lookup"><span data-stu-id="ba454-189">Select Google Apps from hello search results, and add it tooyour list of applications.</span></span>

10. <span data-ttu-id="ba454-190">Выберите свой экземпляр Google Apps, а затем выберите hello **Provisioning** вкладки.</span><span class="sxs-lookup"><span data-stu-id="ba454-190">Select your instance of Google Apps, then select hello **Provisioning** tab.</span></span>

11. <span data-ttu-id="ba454-191">Набор hello **режим подготовки** слишком**автоматического**.</span><span class="sxs-lookup"><span data-stu-id="ba454-191">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

     ![подготовка](./media/active-directory-saas-google-apps-provisioning-tutorial/provisioning.png)

12. <span data-ttu-id="ba454-193">В разделе hello **учетные данные администратора** щелкните **авторизовать**.</span><span class="sxs-lookup"><span data-stu-id="ba454-193">Under hello **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="ba454-194">В новом окне браузера откроется диалоговое окно авторизации Google Apps.</span><span class="sxs-lookup"><span data-stu-id="ba454-194">It opens a Google Apps authorization dialog in a new browser window.</span></span>

13. <span data-ttu-id="ba454-195">Убедитесь, что хотелось бы toogive Azure Active Directory разрешение toomake изменения клиента tooyour Google Apps.</span><span class="sxs-lookup"><span data-stu-id="ba454-195">Confirm that you would like toogive Azure Active Directory permission toomake changes tooyour Google Apps tenant.</span></span> <span data-ttu-id="ba454-196">Нажмите кнопку **Принимаю**.</span><span class="sxs-lookup"><span data-stu-id="ba454-196">Click **Accept**.</span></span>
    
     ![Подтверждение разрешения][28]

14. <span data-ttu-id="ba454-198">В hello портал Azure, щелкните **проверить подключение** tooensure Azure AD можно подключить приложение tooyour Google Apps.</span><span class="sxs-lookup"><span data-stu-id="ba454-198">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Google Apps app.</span></span> <span data-ttu-id="ba454-199">При сбое подключения hello, убедитесь, ваша учетная запись Google Apps имеет разрешения администратора команды и повторите hello **«Авторизовать»** еще один шаг.</span><span class="sxs-lookup"><span data-stu-id="ba454-199">If hello connection fails, ensure your Google Apps account has Team Admin permissions and try hello **"Authorize"** step again.</span></span>

15. <span data-ttu-id="ba454-200">Введите адрес электронной почты hello пользователя или группы, которые должны получить уведомления о подготовке ошибки в hello **уведомление по электронной почте** поле и установите флажок "hello".</span><span class="sxs-lookup"><span data-stu-id="ba454-200">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

16. <span data-ttu-id="ba454-201">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="ba454-201">Click **Save.**</span></span>

17. <span data-ttu-id="ba454-202">Установите hello сопоставлений **tooGoogle синхронизации Azure Active Directory — пользователи приложения.**</span><span class="sxs-lookup"><span data-stu-id="ba454-202">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooGoogle Apps.**</span></span>

18. <span data-ttu-id="ba454-203">В hello **сопоставления атрибутов** просмотрите hello атрибутов пользователей, которые синхронизируются из Azure AD tooGoogle приложений.</span><span class="sxs-lookup"><span data-stu-id="ba454-203">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooGoogle Apps.</span></span> <span data-ttu-id="ba454-204">Здравствуйте, атрибуты, выбранные в качестве **сопоставление** свойства, используемые toomatch hello учетных записей пользователей в Google Apps для операций обновления.</span><span class="sxs-lookup"><span data-stu-id="ba454-204">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Google Apps for update operations.</span></span> <span data-ttu-id="ba454-205">Выберите toocommit кнопку hello сохранить все изменения.</span><span class="sxs-lookup"><span data-stu-id="ba454-205">Select hello Save button toocommit any changes.</span></span>

19. <span data-ttu-id="ba454-206">tooenable hello подготовки службы Azure AD для Google Apps, изменение hello **состояние подготовки** слишком**на** в разделе "Параметры" hello</span><span class="sxs-lookup"><span data-stu-id="ba454-206">tooenable hello Azure AD provisioning service for Google Apps, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

20. <span data-ttu-id="ba454-207">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="ba454-207">Click **Save.**</span></span>

<span data-ttu-id="ba454-208">Он запускает hello Первоначальная синхронизация всех пользователей и/или группам назначается tooGoogle приложений в разделе hello пользователей и групп.</span><span class="sxs-lookup"><span data-stu-id="ba454-208">It starts hello initial synchronization of any users and/or groups assigned tooGoogle Apps in hello Users and Groups section.</span></span> <span data-ttu-id="ba454-209">Начальная синхронизация Hello принимает tooperform больше времени, чем последующие синхронизации, которые происходят примерно каждые 20 минут при условии, что запущена служба hello.</span><span class="sxs-lookup"><span data-stu-id="ba454-209">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="ba454-210">Можно использовать hello **сведения о синхронизации** статьи toomonitor хода выполнения и следуйте ссылки tooprovisioning отчеты о действиях, которые описывают все действия, выполняемые hello подготовки службы приложения Google Apps.</span><span class="sxs-lookup"><span data-stu-id="ba454-210">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Google Apps app.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ba454-211">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ba454-211">Additional resources</span></span>

* [<span data-ttu-id="ba454-212">Управление подготовкой учетных записей пользователей для корпоративных приложений</span><span class="sxs-lookup"><span data-stu-id="ba454-212">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ba454-213">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ba454-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="ba454-214">Настройка единого входа</span><span class="sxs-lookup"><span data-stu-id="ba454-214">Configure Single Sign-on</span></span>](active-directory-saas-google-apps-tutorial.md)



<!--Image references-->

[10]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-security.png
[15]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-api-enabled.png
[20]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-add-another.png
[24]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-auth.png