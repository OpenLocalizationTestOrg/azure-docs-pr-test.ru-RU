---
title: "приложения SaaS aaaConfigure B2B совместной работы в Azure Active Directory | Документы Microsoft"
description: "Примеры кода и команд PowerShell для службы совместной работы Azure Active Directory B2B."
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: c3f22f81567c04ac23ef2316c09de718ecb15d26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-saas-apps-for-b2b-collaboration"></a><span data-ttu-id="c7877-103">Настройка приложений SaaS для службы совместной работы B2B</span><span class="sxs-lookup"><span data-stu-id="c7877-103">Configure SaaS apps for B2B collaboration</span></span>

<span data-ttu-id="c7877-104">Служба совместной работы Azure Active Directory (Azure AD) B2B работает с большинством приложений, которые интегрируются с Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7877-104">Azure Active Directory (Azure AD) B2B collaboration works with most apps that integrate with Azure AD.</span></span> <span data-ttu-id="c7877-105">Этот раздел содержит пошаговые инструкции по настройке некоторых популярных приложений SAS для использования со службой Azure AD B2B.</span><span class="sxs-lookup"><span data-stu-id="c7877-105">In this section, we walk through instructions for configuring some popular SaaS apps for use with Azure AD B2B.</span></span>

<span data-ttu-id="c7877-106">Прежде чем рассматривать инструкции для конкретного приложения, ознакомьтесь с общими правилами.</span><span class="sxs-lookup"><span data-stu-id="c7877-106">Before you look at app-specific instructions, here are some rules of thumb:</span></span>

* <span data-ttu-id="c7877-107">Для большинства приложений hello установки пользователь должен toohappen вручную.</span><span class="sxs-lookup"><span data-stu-id="c7877-107">For most of hello apps, user setup needs toohappen manually.</span></span> <span data-ttu-id="c7877-108">То есть пользователи должны создаваться вручную в также приложение hello.</span><span class="sxs-lookup"><span data-stu-id="c7877-108">That is, users must be created manually in hello app as well.</span></span>

* <span data-ttu-id="c7877-109">Для приложений, которые поддерживают автоматическую установку, например Dropbox различные приглашения создаются из приложения hello.</span><span class="sxs-lookup"><span data-stu-id="c7877-109">For apps that support automatic setup, such as Dropbox, separate invitations are created from hello apps.</span></span> <span data-ttu-id="c7877-110">Пользователям необходимо убедиться, что tooaccept каждое приглашение.</span><span class="sxs-lookup"><span data-stu-id="c7877-110">Users must be sure tooaccept each invitation.</span></span>

* <span data-ttu-id="c7877-111">В атрибутах пользователя hello, любые проблемы, связанные с диска профиля пользователя искаженное (UPD) в гостевых пользователей toomitigate всегда значение **идентификатор пользователя** слишком**user.mail**.</span><span class="sxs-lookup"><span data-stu-id="c7877-111">In hello user attributes, toomitigate any issues with mangled user profile disk (UPD) in guest users, always set **User Identifier** too**user.mail**.</span></span>


## <a name="dropbox-business"></a><span data-ttu-id="c7877-112">Dropbox для бизнеса</span><span class="sxs-lookup"><span data-stu-id="c7877-112">Dropbox Business</span></span>

<span data-ttu-id="c7877-113">tooenable toosign пользователей с помощью их учетных записей организации, необходимо вручную настроить toouse Dropbox бизнес Azure AD как поставщика удостоверений Security Assertion Markup Language (SAML).</span><span class="sxs-lookup"><span data-stu-id="c7877-113">tooenable users toosign in using their organization account, you must manually configure Dropbox Business toouse Azure AD as a Security Assertion Markup Language (SAML) identity provider.</span></span> <span data-ttu-id="c7877-114">Если Business общего банка данных не было настроенных toodo таким образом, оно не может запрашивать или разрешил toosign пользователей с помощью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7877-114">If Dropbox Business has not been configured toodo so, it cannot prompt or otherwise allow users toosign in using Azure AD.</span></span>

1. <span data-ttu-id="c7877-115">tooadd hello общего банка данных приложения в Azure AD, выберите **корпоративных приложений** в hello левой панели, затем щелкните **добавить**.</span><span class="sxs-lookup"><span data-stu-id="c7877-115">tooadd hello Dropbox Business app into Azure AD, select **Enterprise applications** in hello left pane, and then click **Add**.</span></span>

  ![Кнопка «Добавить» Hello, на странице приложения hello предприятия](media/active-directory-b2b-configure-saas-apps/add-dropbox.png)

2. <span data-ttu-id="c7877-117">В hello **добавить приложение** окно, введите **dropbox** в hello поле поиска, а затем выберите **Dropbox для бизнеса** в списке результатов hello.</span><span class="sxs-lookup"><span data-stu-id="c7877-117">In hello **Add an application** window, enter **dropbox** in hello search box, and then select **Dropbox for Business** in hello results list.</span></span>

  ![Поиск «dropbox» на hello Добавление страницы приложения](media/active-directory-b2b-configure-saas-apps/add-app-dialog.png)

3. <span data-ttu-id="c7877-119">На hello **единого входа** выберите **единого входа** в hello левой панели, а затем введите **user.mail** в hello **идентификатор пользователя** поле.</span><span class="sxs-lookup"><span data-stu-id="c7877-119">On hello **Single sign-on** page, select **Single sign-on** in hello left pane, and then enter **user.mail** in hello **User Identifier** box.</span></span> <span data-ttu-id="c7877-120">(Этот идентификатор задан как имя участника-пользователя по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="c7877-120">(It's set as UPN by default.)</span></span>

  ![Настройка единого входа для приложения hello](media/active-directory-b2b-configure-saas-apps/configure-app-sso.png)

4. <span data-ttu-id="c7877-122">toouse сертификат hello toodownload для общего банка данных конфигурации, выберите **настроить DropBox**и выберите **SAML на адрес службы единого** в списке hello.</span><span class="sxs-lookup"><span data-stu-id="c7877-122">toodownload hello certificate toouse for Dropbox configuration, select **Configure DropBox**, and then select **SAML Single Sign On Service URL** in hello list.</span></span>

  ![Загрузка сертификата hello для общего банка данных конфигурации](media/active-directory-b2b-configure-saas-apps/download-certificate.png)

5. <span data-ttu-id="c7877-124">Вход tooDropbox с hello входа URL-адрес из hello **единого входа** страницы.</span><span class="sxs-lookup"><span data-stu-id="c7877-124">Sign in tooDropbox with hello sign-on URL from hello **Single sign-on** page.</span></span>

  ![Страница приветствия входа в Dropbox](media/active-directory-b2b-configure-saas-apps/sign-in-to-dropbox.png)

6. <span data-ttu-id="c7877-126">Выберите меню hello **консоли администрирования**.</span><span class="sxs-lookup"><span data-stu-id="c7877-126">On hello menu, select **Admin Console**.</span></span>

  ![ссылка «Консоли администрирования» Hello меню Dropbox hello](media/active-directory-b2b-configure-saas-apps/dropbox-menu.png)

7. <span data-ttu-id="c7877-128">В hello **проверки подлинности** выберите **дополнительные**, отправьте сертификат hello и затем в hello **URL-адрес входа** введите URL-адрес hello SAML единого входа.</span><span class="sxs-lookup"><span data-stu-id="c7877-128">In hello **Authentication** dialog box, select **More**, upload hello certificate and then, in hello **Sign in URL** box, enter hello SAML single sign-on URL.</span></span>

  ![Hello ссылку «Дополнительные» в hello Свернуть диалоговое окно проверки подлинности](media/active-directory-b2b-configure-saas-apps/dropbox-auth-01.png)

  ![Hello «В URL-адрес входа» в hello развернуть диалоговое окно проверки подлинности](media/active-directory-b2b-configure-saas-apps/paste-single-sign-on-URL.png)

8. <span data-ttu-id="c7877-131">Настройка автоматического пользователя tooconfigure в hello портал Azure, выберите **Provisioning** hello левой панели выберите **автоматического** в hello **режим подготовки** поле, а затем выберите **Авторизовать**.</span><span class="sxs-lookup"><span data-stu-id="c7877-131">tooconfigure automatic user setup in hello Azure portal, select **Provisioning** in hello left pane, select **Automatic** in hello **Provisioning Mode** box, and then select **Authorize**.</span></span>

  ![Настройка автоматической подготовки пользователей в hello портал Azure](media/active-directory-b2b-configure-saas-apps/set-up-automatic-provisioning.png)

<span data-ttu-id="c7877-133">После гостя или член пользователей были настроены в общий банк данных приложение hello, они получают отдельных приглашение из общего банка данных.</span><span class="sxs-lookup"><span data-stu-id="c7877-133">After guest or member users have been set up in hello Dropbox app, they receive a separate invitation from Dropbox.</span></span> <span data-ttu-id="c7877-134">toouse общего банка данных единого входа, приглашенным необходимо принять приглашение hello, щелкнув ссылку в нем.</span><span class="sxs-lookup"><span data-stu-id="c7877-134">toouse Dropbox single sign-on, invitees must accept hello invitation by clicking a link in it.</span></span>

## <a name="box"></a><span data-ttu-id="c7877-135">Box</span><span class="sxs-lookup"><span data-stu-id="c7877-135">Box</span></span>
<span data-ttu-id="c7877-136">Пользователи tooauthenticate поле гостевых пользователей с учетной записью Azure AD можно включить с помощью федерации на основании hello протокола SAML.</span><span class="sxs-lookup"><span data-stu-id="c7877-136">You can enable users tooauthenticate Box guest users with their Azure AD account by using federation that's based on hello SAML protocol.</span></span> <span data-ttu-id="c7877-137">В этой процедуре необходимо отправить tooBox.com метаданных.</span><span class="sxs-lookup"><span data-stu-id="c7877-137">In this procedure, you upload metadata tooBox.com.</span></span>

1. <span data-ttu-id="c7877-138">Добавьте поле приложение hello из hello корпоративных приложений.</span><span class="sxs-lookup"><span data-stu-id="c7877-138">Add hello Box app from hello enterprise apps.</span></span>

2. <span data-ttu-id="c7877-139">Настройка единого входа в hello следующий порядок:</span><span class="sxs-lookup"><span data-stu-id="c7877-139">Configure single sign-on in hello following order:</span></span>

  ![Настройте единый вход в Box.](media/active-directory-b2b-configure-saas-apps/configure-box-sso.png)

 <span data-ttu-id="c7877-141">а.</span><span class="sxs-lookup"><span data-stu-id="c7877-141">a.</span></span> <span data-ttu-id="c7877-142">В hello **URL-адрес входа** убедитесь, что hello URL-адрес входа правильно задан для поля в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c7877-142">In hello **Sign on URL** box, ensure that hello sign-on URL is set appropriately for Box in hello Azure portal.</span></span> <span data-ttu-id="c7877-143">Этот URL-адрес является hello URL-адреса клиента Box.com.</span><span class="sxs-lookup"><span data-stu-id="c7877-143">This URL is hello URL of your Box.com tenant.</span></span> <span data-ttu-id="c7877-144">Он должен соответствовать соглашению об именовании hello *https://.box.com*.</span><span class="sxs-lookup"><span data-stu-id="c7877-144">It should follow hello naming convention *https://.box.com*.</span></span>  
 <span data-ttu-id="c7877-145">Hello **идентификатор** не применяется toothis приложения, но она по-прежнему отображается как поле является обязательным.</span><span class="sxs-lookup"><span data-stu-id="c7877-145">hello **Identifier** does not apply toothis app, but it still appears as a mandatory field.</span></span>

 <span data-ttu-id="c7877-146">b.</span><span class="sxs-lookup"><span data-stu-id="c7877-146">b.</span></span> <span data-ttu-id="c7877-147">В hello **идентификатор пользователя** введите **user.mail** (для единого входа для учетной записи гостя).</span><span class="sxs-lookup"><span data-stu-id="c7877-147">In hello **User identifier** box, enter **user.mail** (for SSO for guest accounts).</span></span>

 <span data-ttu-id="c7877-148">c.</span><span class="sxs-lookup"><span data-stu-id="c7877-148">c.</span></span> <span data-ttu-id="c7877-149">В разделе **Сертификат подписи SAML** щелкните **Создать сертификат**.</span><span class="sxs-lookup"><span data-stu-id="c7877-149">Under **SAML Signing Certificate**, click **Create new certificate**.</span></span>

 <span data-ttu-id="c7877-150">d.</span><span class="sxs-lookup"><span data-stu-id="c7877-150">d.</span></span> <span data-ttu-id="c7877-151">toobegin Настройка вашей toouse клиента Box.com Azure AD в качестве поставщика удостоверений скачать файл метаданных hello и сохраните его в локальный диск tooyour.</span><span class="sxs-lookup"><span data-stu-id="c7877-151">toobegin configuring your Box.com tenant toouse Azure AD as an identity provider, download hello metadata file and then save it tooyour local drive.</span></span>

 <span data-ttu-id="c7877-152">д.</span><span class="sxs-lookup"><span data-stu-id="c7877-152">e.</span></span> <span data-ttu-id="c7877-153">Пересылка hello метаданных файла toohello поле Группа поддержки, который выполняет настройку единого входа для вас.</span><span class="sxs-lookup"><span data-stu-id="c7877-153">Forward hello metadata file toohello Box support team, which configures single sign-on for you.</span></span>

3. <span data-ttu-id="c7877-154">Для установки автоматического пользователя Azure AD, hello левой панели выберите **Provisioning**и выберите **авторизовать**.</span><span class="sxs-lookup"><span data-stu-id="c7877-154">For Azure AD automatic user setup, in hello left pane, select **Provisioning**, and then select **Authorize**.</span></span>

  ![Авторизовать панель инструментов tooconnect Azure AD](media/active-directory-b2b-configure-saas-apps/auth-azure-ad-to-connect-to-box.png)

<span data-ttu-id="c7877-156">Как приглашенным Dropbox приглашенным поле необходимо активировать их приглашения приложение hello поле.</span><span class="sxs-lookup"><span data-stu-id="c7877-156">Like Dropbox invitees, Box invitees must redeem their invitation from hello Box app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7877-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c7877-157">Next steps</span></span>

<span data-ttu-id="c7877-158">См. следующие статьи, посвященные совместной работы Azure AD B2B hello.</span><span class="sxs-lookup"><span data-stu-id="c7877-158">See hello following articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="c7877-159">Что такое служба совместной работы Azure AD B2B?</span><span class="sxs-lookup"><span data-stu-id="c7877-159">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="c7877-160">Свойства пользователя службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="c7877-160">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="c7877-161">Добавление роли пользователя tooa B2B совместной работы</span><span class="sxs-lookup"><span data-stu-id="c7877-161">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="c7877-162">Делегирование приглашений для службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="c7877-162">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="c7877-163">Динамические группы и служба совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="c7877-163">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="c7877-164">Примеры кода и команд PowerShell для службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="c7877-164">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="c7877-165">Основные сведения о токенах пользователей в службе совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="c7877-165">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="c7877-166">Сопоставление утверждений пользователя службы совместной работы B2B в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c7877-166">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="c7877-167">Доступ внешних пользователей к Office 365</span><span class="sxs-lookup"><span data-stu-id="c7877-167">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="c7877-168">Текущие ограничения службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="c7877-168">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
